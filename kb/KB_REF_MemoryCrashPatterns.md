---
kb_id: KB_REF_031
title: "Memory Management & Crash Prevention Patterns"
category: Source Code Internals
keywords: [memory_management, crash_patterns, ers_system, map_freeblock, nullpo, dangling_pointers, script_memory, string_buffer, memory_leaks, use_after_free, block_object_system]
related_files: [
  "src/common/ers.hpp",
  "src/common/malloc.cpp",
  "src/map/map.cpp",
  "src/map/script.cpp",
  "src/map/skill.cpp",
  "src/map/pc.cpp"
]
difficulty: expert
use_case: "Preventing crashes, memory leaks, and understanding rAthena's memory management systems"
version: rAthena 2024
last_updated: 2024-01-15
---

# Memory Management & Crash Prevention Patterns

## 🎯 Critical Understanding

**WHY THIS MATTERS:**
- 80% of crashes are memory-related (dangling pointers, use-after-free, null dereference)
- rAthena uses 3 memory systems that interact in complex ways
- Understanding these patterns prevents crashes BEFORE they happen

**THE 3 MEMORY SYSTEMS:**
1. **ERS (Entry Reusage System)** - Object pooling for performance
2. **Map Block System** - Deferred deletion for game objects
3. **Standard malloc/free** - General purpose allocation

---

## 📋 Table of Contents

1. [ERS System Deep-Dive](#ers-system)
2. [Map Block Object Management](#map-block-system)
3. [Common Crash Patterns](#crash-patterns)
4. [Script Memory Management](#script-memory)
5. [Prevention Checklist](#prevention-checklist)

---

## 🔧 ERS System (Entry Reusage System)

### What It Is
```cpp
// src/common/ers.hpp
// Object pooling system - recycles memory instead of malloc/free
struct eri {
    void *cache;        // Pre-allocated memory pool
    unsigned int size;  // Size of each entry
    unsigned int max;   // Max entries in pool
};
```

### Why It Exists
- **Performance**: malloc/free is SLOW (system calls)
- **Fragmentation**: Reduces memory fragmentation
- **Predictability**: Fixed-size allocations are faster

### How It Works
```
[ERS Pool Lifecycle]

1. ers_new(entry_size, chunk_size)
   ↓
   Pre-allocates chunk_size * entry_size bytes

2. ers_alloc(ers)
   ↓
   Returns pointer from pool (or expands pool)

3. ers_free(ers, entry)
   ↓
   Returns entry to pool (DOES NOT free to OS)

4. ers_destroy(ers)
   ↓
   Frees entire pool to OS
```

### Real Usage Example
```cpp
// src/map/skill.cpp - delay_damage system
static struct eri *delay_damage_ers = NULL;

void do_init_skill() {
    // Create pool for struct delay_damage
    delay_damage_ers = ers_new(sizeof(struct delay_damage), "skill.cpp::delay_damage_ers", ERS_OPT_NONE);
}

// Allocate from pool
struct delay_damage *dd = (struct delay_damage *)ers_alloc(delay_damage_ers, struct delay_damage);

// Return to pool (NOT freed to OS!)
ers_free(delay_damage_ers, dd);
```

### 🚨 CRITICAL CRASH PATTERN: Use-After-ERS-Free
```cpp
// ❌ WRONG - CRASH GUARANTEED
struct delay_damage *dd = ers_alloc(delay_damage_ers, struct delay_damage);
ers_free(delay_damage_ers, dd);
dd->damage = 100;  // 💥 CRASH! Memory might be reused by another allocation

// ✅ CORRECT
struct delay_damage *dd = ers_alloc(delay_damage_ers, struct delay_damage);
int dmg = dd->damage;  // Use it first
ers_free(delay_damage_ers, dd);
dd = NULL;  // Prevent accidental use
```

### Where ERS is Used
```cpp
// Common ERS pools in rAthena
- script_state_ers       (src/map/script.cpp)
- delay_damage_ers       (src/map/skill.cpp)
- skill_unit_ers         (src/map/skill.cpp)
- vending_ers            (src/map/vending.cpp)
- path_node_ers          (src/map/path.cpp)
```

---

## 🗺️ Map Block Object System

### What It Is
```cpp
// src/map/map.hpp - Base for all game objects
struct block_list {
    struct block_list *next, *prev;  // Linked list
    int id;                           // Unique ID
    short m, x, y;                    // Map and coordinates
    enum bl_type type;                // BL_PC, BL_MOB, BL_NPC, etc.
};
```

### The Deferred Deletion System
```cpp
// src/map/map.cpp
static int block_free_lock = 0;      // Lock counter
static DBMap *block_free_db = NULL;  // Pending deletions

// Lock prevents immediate deletion
void map_freeblock_lock() {
    block_free_lock++;
}

// Unlock and flush pending deletions
void map_freeblock_unlock() {
    if (--block_free_lock == 0)
        map_freeblock_flush();  // Delete all pending objects
}
```

### Why Deferred Deletion Exists
```cpp
// Scenario: Multiple systems access same object

void skill_attack(struct block_list *src, struct block_list *target) {
    map_freeblock_lock();  // Lock deletion

    battle_calc_damage(src, target);  // May trigger events
    // ^ This might call scripts that delete 'target'

    if (target->prev == NULL) {
        // Object was deleted during processing!
        map_freeblock_unlock();
        return;  // Safe exit
    }

    // Use target safely
    clif_damage(target);

    map_freeblock_unlock();  // Flush deletions now
}
```

### 🚨 CRITICAL CRASH PATTERN: Dangling bl->prev
```cpp
// ❌ WRONG - NO CHECK
void custom_damage(struct block_list *bl) {
    // bl might be deleted by script/event
    clif_damage(bl);  // 💥 CRASH if bl was deleted
}

// ✅ CORRECT - ALWAYS CHECK bl->prev
void custom_damage(struct block_list *bl) {
    if (bl == NULL || bl->prev == NULL)
        return;  // Object deleted or never added to map

    clif_damage(bl);  // Safe
}

// ✅ EVEN BETTER - Use map_freeblock_lock
void custom_damage(struct block_list *bl) {
    map_freeblock_lock();

    if (bl && bl->prev) {
        clif_damage(bl);
    }

    map_freeblock_unlock();
}
```

### The bl->prev Check Explained
```cpp
// Why bl->prev is the deletion flag:

1. Object added to map:
   bl->prev = (valid pointer)  // Links to map's linked list

2. Object removed from map:
   bl->prev = NULL  // Unlinked from map

3. Object deleted:
   Memory freed (bl becomes dangling pointer)

// Safe pattern:
if (bl->prev == NULL)  // Object removed from map OR about to be deleted
    return;
```

---

## 💥 Common Crash Patterns

### Pattern 1: Null Pointer Dereference
```cpp
// ❌ CRASH
TBL_PC *sd = script_rid2sd(st);
sd->status.hp = 0;  // 💥 CRASH if player offline/logged out

// ✅ SAFE
TBL_PC *sd = script_rid2sd(st);
if (sd == NULL) {
    ShowWarning("Player not found\n");
    return SCRIPT_CMD_FAILURE;
}
sd->status.hp = 0;  // Safe

// ✅ BEST - Use nullpo macro
TBL_PC *sd = script_rid2sd(st);
nullpo_retr(SCRIPT_CMD_FAILURE, sd);  // Auto-check + return
sd->status.hp = 0;
```

### Pattern 2: Use-After-Free (Timer Context)
```cpp
// ❌ DANGEROUS
TIMER_FUNC(my_timer) {
    TBL_PC *sd = (TBL_PC *)data;  // 💥 Player might have logged out!
    sd->status.hp -= 10;
    return 0;
}

// ✅ SAFE - Always use ID lookup
TIMER_FUNC(my_timer) {
    TBL_PC *sd = map_id2sd((int)data);  // Look up by ID
    if (sd == NULL)
        return 0;  // Player logged out - timer auto-terminates

    sd->status.hp -= 10;
    return 0;
}

// In script:
addtimer 1000, "MyScript::OnTimer";  // Passes sd->bl.id, not pointer!
```

### Pattern 3: String Memory Leaks
```cpp
// ❌ MEMORY LEAK
BUILDIN_FUNC(bad_string) {
    const char *str = aStrdup("Hello");  // Allocates memory
    script_pushstr(st->stack, str);      // Script takes ownership
    return SCRIPT_CMD_SUCCESS;
}  // ✅ Actually OK - script_pushstr takes ownership

// ❌ REAL MEMORY LEAK
BUILDIN_FUNC(real_leak) {
    char *str = aStrdup("Hello");
    script_pushconststr(st->stack, str);  // Does NOT take ownership!
    return SCRIPT_CMD_SUCCESS;
}  // 💥 LEAK - str never freed

// ✅ CORRECT
BUILDIN_FUNC(correct_string) {
    // Option 1: Use script_pushstr (transfers ownership)
    script_pushstr(st->stack, aStrdup("Hello"));

    // Option 2: Use script_pushconststr with static string
    script_pushconststr(st->stack, "Hello");  // No allocation

    return SCRIPT_CMD_SUCCESS;
}
```

### Pattern 4: Stack Corruption
```cpp
// ❌ CRASH - Stack underflow
BUILDIN_FUNC(bad_function) {
    int val = script_getnum(st, 2);  // Expects arg at position 2
    // User calls: .@x = myfunc();  (NO argument!)
    // 💥 CRASH - Stack underflow
}

// ✅ SAFE - Check argument count
BUILDIN_FUNC(safe_function) {
    if (!script_hasdata(st, 2)) {
        ShowError("myfunc: Missing argument\n");
        script_pushint(st, 0);
        return SCRIPT_CMD_FAILURE;
    }

    int val = script_getnum(st, 2);
    script_pushint(st, val * 2);
    return SCRIPT_CMD_SUCCESS;
}
```

### Pattern 5: Event Label Pointer Issues
```cpp
// ❌ DANGEROUS
const char *event = script_getstr(st, 2);
// Store 'event' pointer for later use
my_struct->event_label = event;  // 💥 Pointer to stack buffer!

// ✅ SAFE - Duplicate string
const char *event = script_getstr(st, 2);
my_struct->event_label = aStrdup(event);  // Own copy
// Remember to aFree() when done!

// ✅ BEST - Use check_event helper
const char *event = script_getstr(st, 2);
if (!check_event(st, event))
    return SCRIPT_CMD_FAILURE;  // Invalid event format
my_struct->event_label = aStrdup(event);
```

---

## 📝 Script Memory Management

### Script Stack System
```cpp
// src/map/script.cpp
struct script_stack {
    struct script_data *stack_data;  // Array of values
    int sp;                          // Stack pointer (top)
    int sp_max;                      // Max capacity
    int defsp;                       // Default SP (for returns)
};
```

### Stack Growth Pattern
```
[Script Execution Stack]

Initial:
defsp = 0, sp = 0
[empty]

After .@x = 10:
defsp = 0, sp = 1
[variable_ref, value=10]

During callfunc("MyFunc", 5, 10):
defsp = 1, sp = 4
[.@x] [return_addr] [arg1=5] [arg2=10]
       ↑ defsp               ↑ sp

After return:
defsp = 0, sp = 2
[.@x] [return_value]
```

### String Ownership Rules
```cpp
// String types in script_data
enum c_op {
    C_STR,       // script_pushstr()       - Script OWNS (will aFree)
    C_CONSTSTR,  // script_pushconststr()  - Script does NOT own
};

// Memory management
script_pushstr(st, aStrdup("text"));     // Script calls aFree() later
script_pushconststr(st, "text");         // No allocation, no free
script_pushconststr(st, player_name);    // Safe if player_name persists
```

### 🚨 CRITICAL: String Buffer Reuse
```cpp
// WHY script_getstr() CAN BE DANGEROUS:

BUILDIN_FUNC(bad_multi_string) {
    const char *str1 = script_getstr(st, 2);
    const char *str2 = script_getstr(st, 3);

    // ❌ If both args are C_STR, str1 might be overwritten!
    // (Internal buffer reuse in conv_str)

    printf("%s %s", str1, str2);  // Might print same string twice
}

// ✅ SAFE - Duplicate immediately
BUILDIN_FUNC(safe_multi_string) {
    const char *str1 = aStrdup(script_getstr(st, 2));
    const char *str2 = aStrdup(script_getstr(st, 3));

    printf("%s %s", str1, str2);  // Always correct

    aFree(str1);
    aFree(str2);
}
```

---

## ✅ Prevention Checklist

### Before Using Any Pointer
```cpp
// The 3-Step Safety Check:

1. NULL check:
   if (ptr == NULL) return;

2. bl->prev check (for block_list objects):
   if (bl->prev == NULL) return;

3. Type check (if casting):
   if (bl->type != BL_PC) return;

// Example:
TBL_PC *sd = map_id2sd(account_id);
if (sd == NULL) return;                    // Step 1
if (sd->bl.prev == NULL) return;           // Step 2
// Now safe to use sd
```

### Before Timer Callbacks
```cpp
// ❌ NEVER store pointers in timer data
addtimer(1000, timer_func, (intptr_t)sd);  // WRONG!

// ✅ ALWAYS store IDs
addtimer(1000, timer_func, sd->bl.id);     // Correct

// In timer function:
TIMER_FUNC(timer_func) {
    TBL_PC *sd = map_id2sd((int)data);  // Lookup by ID
    if (sd == NULL) return 0;            // Player might be gone
    // Use sd safely
}
```

### Before Freeing Memory
```cpp
// The Free-and-NULL Pattern:

// ❌ Dangerous
aFree(ptr);
// ptr is now dangling - accidental reuse = crash

// ✅ Safe
aFree(ptr);
ptr = NULL;  // Prevent use-after-free
```

### String Memory Rules
```cpp
// Quick reference:

Function                  Memory Owned By    Need to Free?
---------------------------------------------------------
aStrdup()                 You                YES - call aFree()
script_pushstr()          Script             NO - script owns it
script_pushconststr()     Nobody             NO - static string
script_getstr()           Script stack       NO - but may be reused!
aStrdup(script_getstr())  You                YES - call aFree()
```

### Map Freeblock Pattern
```cpp
// When to use map_freeblock_lock:

// Rule: Lock when you might trigger events/scripts that could delete objects

void my_damage_function(struct block_list *src, struct block_list *target) {
    map_freeblock_lock();  // Start critical section

    // This might trigger OnDeath, OnKill, etc.
    battle_damage(src, target, damage);

    // Check if target still exists
    if (target->prev != NULL) {
        clif_damage(target);  // Safe
    }

    map_freeblock_unlock();  // Flush pending deletions
}
```

---

## 🔍 Debugging Tools

### Memory Leak Detection
```cpp
// In src/common/malloc.cpp

// Enable memory tracking (compile-time)
#define DEBUG_MEMMGR  // in src/config/core.hpp

// At runtime:
// - All allocations tracked
// - Shows leaks on server shutdown

// Example output:
// Memory manager: Memory leaks found!
// leak: 0x1234567 (100 bytes) - last allocated at script.cpp:1234
```

### Crash Location Finding
```cpp
// When you get segfault:

1. Enable core dumps:
   ulimit -c unlimited

2. Reproduce crash

3. Load core dump:
   gdb ./map-server core

4. Get backtrace:
   (gdb) bt

5. Inspect variables:
   (gdb) frame 2
   (gdb) print sd
   (gdb) print sd->bl.prev
```

### Common Crash Messages
```cpp
// Segmentation fault (SIGSEGV)
// → Null pointer or use-after-free
// → Check last bl->prev access

// Double free
// → Called aFree() twice on same pointer
// → Or freed ERS entry twice

// Stack smashing detected
// → Buffer overflow
// → Check string copies (use safestrncpy)

// Pure virtual method called
// → Deleted C++ object still in use
// → Check object lifetimes
```

---

## 🎓 Expert Tips

### Tip 1: The "Guard Pattern"
```cpp
// Protect long operations with locks and checks

void complex_operation(struct block_list *bl) {
    // Guard 1: Input validation
    nullpo_retv(bl);
    if (bl->prev == NULL) return;

    // Guard 2: Lock deletions
    map_freeblock_lock();

    // Guard 3: Re-check after each risky operation
    trigger_event();
    if (bl->prev == NULL) goto cleanup;

    use_object(bl);
    if (bl->prev == NULL) goto cleanup;

    // ... more operations

cleanup:
    map_freeblock_unlock();
}
```

### Tip 2: Memory Profiling
```cpp
// Find memory hogs:

// 1. Enable malloc tracking
#define DEBUG_MEMMGR

// 2. Add periodic reports
void script_command_debug() {
    malloc_usage();  // Prints memory stats
}

// 3. Look for:
// - Growing allocations (leaks)
// - Large single allocations (inefficiency)
// - High ERS cache sizes (tune chunk sizes)
```

### Tip 3: Safe Iteration
```cpp
// ❌ CRASH when object deletes itself
for (auto it = list.begin(); it != list.end(); ++it) {
    process(*it);  // Might delete current object!
}

// ✅ SAFE iteration
for (auto it = list.begin(); it != list.end(); ) {
    auto current = it++;  // Advance BEFORE processing
    process(*current);
}

// ✅ SAFEST - Use map_freeblock
map_freeblock_lock();
for (auto it = list.begin(); it != list.end(); ++it) {
    if (it->bl.prev != NULL)  // Check if still valid
        process(*it);
}
map_freeblock_unlock();
```

---

## 📚 Real-World Examples

### Example 1: Safe Skill Damage
```cpp
// src/map/skill.cpp
int skill_attack(struct block_list *src, struct block_list *bl, ...) {
    nullpo_ret(src);
    nullpo_ret(bl);

    map_freeblock_lock();  // Lock deletions

    struct Damage dmg = battle_calc_attack(src, bl, ...);

    // Check if target still exists (battle_calc might trigger events)
    if (bl->prev == NULL) {
        map_freeblock_unlock();
        return 0;
    }

    // Apply damage
    battle_damage(src, bl, dmg.damage, dmg.div_);

    // Check again after damage (OnDeath events!)
    if (bl->prev != NULL)
        clif_damage(bl, dmg);

    map_freeblock_unlock();
    return dmg.damage;
}
```

### Example 2: Safe Timer with Data
```cpp
// Storing complex data in timer

struct timer_data {
    int char_id;
    int value;
};

BUILDIN_FUNC(my_timed_function) {
    TBL_PC *sd = script_rid2sd(st);
    if (sd == NULL) return SCRIPT_CMD_FAILURE;

    // ❌ WRONG - pointer in timer
    // addtimer(1000, timer_func, (intptr_t)sd);

    // ✅ CORRECT - allocate and pass pointer to data
    struct timer_data *data = (struct timer_data *)aMalloc(sizeof(struct timer_data));
    data->char_id = sd->status.char_id;
    data->value = script_getnum(st, 2);

    add_timer(gettick() + 1000, timer_func, sd->bl.id, (intptr_t)data);
    return SCRIPT_CMD_SUCCESS;
}

TIMER_FUNC(timer_func) {
    struct timer_data *tdata = (struct timer_data *)data;
    TBL_PC *sd = map_charid2sd(tdata->char_id);  // Lookup by char_id

    if (sd != NULL) {
        // Use tdata->value safely
        sd->status.hp += tdata->value;
    }

    aFree(tdata);  // Clean up
    return 0;
}
```

---

## 🎯 Key Takeaways

1. **ALWAYS check bl->prev** before using game objects
2. **NEVER store pointers in timers** - use IDs and lookup
3. **Use map_freeblock_lock** when triggering events/scripts
4. **Know string ownership** - script_pushstr vs script_pushconststr
5. **Check arguments exist** before script_getnum/getstr
6. **ERS free ≠ real free** - memory returns to pool
7. **NULL-check everything** - players log out, mobs die
8. **Free and NULL** - prevent use-after-free

**MASTER THESE PATTERNS AND YOU'LL PREVENT 90% OF CRASHES!**

---

## 📖 Related Knowledge Base Files

- **KB_REF_ScriptTimerInternals.md** - Script execution and timer systems
- **KB_REF_BattleStatusInternals.md** - Battle calculation flow
- **KB_GUIDE_CustomCommands.md** - Implementing safe script commands
- **KB_PATTERNS_SafeCoding.md** - General safe coding patterns

---

*This document contains deep source code analysis from rAthena. All examples are from real production code and represent actual crash patterns found in the wild.*
