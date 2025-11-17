---
kb_id: KB_REF_029
title: "Source Code Best Practices and Coding Standards"
category: Source Code
keywords: [best_practices, code_style, error_handling, memory_safety, null_checks, performance, documentation, testing, coding_standards]
related_files: [
  "src/",
  ".clang-format"
]
difficulty: intermediate
use_case: "Writing clean, safe, and maintainable rAthena code"
version: rAthena 2024
last_updated: 2024-01-15
---

# Source Code Best Practices and Coding Standards

## Quick Reference

### **Always Check Null Pointers**
```cpp
// ✅ CORRECT
struct map_session_data *sd = script_rid2sd(st);
if (!sd || !sd->bl.prev) {
    return 1;
}
pc_heal(sd, 100, 0, 0);
```

### **Always Validate Input**
```cpp
// ✅ CORRECT
int item_id = script_getnum(st, 2);
if (item_id < 0 || !itemdb_exists(item_id)) {
    ShowError("Invalid item ID: %d\n", item_id);
    return 1;
}
```

### **Always Free Allocated Memory**
```cpp
// ✅ CORRECT
char *str = aStrdup("Hello");
// ... use str ...
aFree(str);
```

---

## Table of Contents
1. [Code Style and Formatting](#code-style-and-formatting)
2. [Null Pointer Safety](#null-pointer-safety)
3. [Input Validation](#input-validation)
4. [Memory Management](#memory-management)
5. [Error Handling](#error-handling)
6. [Performance Considerations](#performance-considerations)
7. [Documentation Standards](#documentation-standards)
8. [Testing Guidelines](#testing-guidelines)
9. [Common Mistakes to Avoid](#common-mistakes-to-avoid)
10. [Code Review Checklist](#code-review-checklist)

---

## Code Style and Formatting

### **1. Indentation**

**Use TABS, not spaces** (rAthena standard):

```cpp
// ✅ CORRECT
void my_function(int value) {
→   if (value > 0) {
→   →   ShowInfo("Positive value: %d\n", value);
→   }
}

// ❌ WRONG - Using spaces
void my_function(int value) {
    if (value > 0) {
        ShowInfo("Positive value: %d\n", value);
    }
}
```

---

### **2. Brace Style**

**Opening brace on same line** (K&R style):

```cpp
// ✅ CORRECT
if (condition) {
    // code
} else {
    // code
}

for (int i = 0; i < 10; i++) {
    // code
}

// ❌ WRONG - Allman style
if (condition)
{
    // code
}
```

---

### **3. Naming Conventions**

```cpp
// Functions: lowercase_with_underscores
void pc_heal_player(struct map_session_data *sd, int hp);

// Structs: lowercase_with_underscores
struct map_session_data { ... };

// Enums: UPPERCASE or e_prefix
enum e_race { RC_FORMLESS, RC_UNDEAD, ... };

// Constants: UPPERCASE
#define MAX_INVENTORY 100
const int MAX_PARTY = 12;

// Global variables: avoid! If needed, descriptive names
int battle_config_base_exp_rate;

// Local variables: short, descriptive
int hp, sp;
struct map_session_data *sd;
```

---

### **4. Function Length**

**Keep functions short and focused** (< 100 lines ideal):

```cpp
// ✅ GOOD - Short, focused function
int calculate_damage(int atk, int def) {
    int damage = atk - def;
    return max(1, damage);
}

// ❌ BAD - 500-line monster function
int process_everything(...) {
    // Hundreds of lines doing multiple things
}
```

**If function is too long, split it**:

```cpp
// Split into smaller helper functions
static int calculate_base_damage(...) { ... }
static int apply_modifiers(...) { ... }
static int apply_defense(...) { ... }

int calculate_final_damage(...) {
    int base = calculate_base_damage(...);
    int modified = apply_modifiers(base, ...);
    int final = apply_defense(modified, ...);
    return final;
}
```

---

### **5. Comments**

**Comment WHY, not WHAT**:

```cpp
// ❌ BAD - Obvious comment
// Add 1 to hp
hp = hp + 1;

// ✅ GOOD - Explains reason
// Prevent death from fall damage by ensuring minimum 1 HP
hp = max(hp, 1);

// ✅ GOOD - Complex logic explanation
// Apply diminishing returns for high DEF values
// Formula: effective_def = base_def / (1 + base_def / 100)
// This prevents defense from being too powerful at high values
if (def > 100) {
    def = def / (1 + def / 100);
}
```

**Document function purposes**:

```cpp
/**
 * Heals a player and shows visual effect
 * @param sd: Player to heal
 * @param hp: Amount of HP to restore
 * @param sp: Amount of SP to restore
 * @param type: Heal type (0=silent, 1=with effect)
 * @return: Actual HP restored (capped by max HP)
 */
int pc_heal(struct map_session_data *sd, int hp, int sp, int type) {
    // Implementation
}
```

---

## Null Pointer Safety

### **Rule: Always Check Before Dereferencing**

```cpp
// ❌ WRONG - No null check
void bad_function(struct map_session_data *sd) {
    pc_heal(sd, 100, 0, 0);  // CRASH if sd is NULL!
}

// ✅ CORRECT - Null check
void good_function(struct map_session_data *sd) {
    if (!sd) {
        ShowError("good_function: NULL player pointer!\n");
        return;
    }

    pc_heal(sd, 100, 0, 0);  // Safe
}
```

---

### **Check Player Session State**

```cpp
// ✅ CORRECT - Full session validation
void process_player_action(struct map_session_data *sd) {
    // Check if pointer is valid
    if (!sd) {
        ShowError("Invalid player pointer!\n");
        return;
    }

    // Check if player is still in game (bl.prev != NULL)
    if (!sd->bl.prev) {
        ShowError("Player not on map!\n");
        return;
    }

    // Safe to proceed
    ShowInfo("Processing action for %s\n", sd->status.name);
}
```

---

### **Script Command Null Checks**

```cpp
// ✅ CORRECT - Script command pattern
BUILDIN_FUNC(my_command)
{
    struct map_session_data *sd = script_rid2sd(st);

    // ALWAYS check if player is attached
    if (!sd) {
        ShowError("my_command: No player attached!\n");
        script_pushint(st, 0);
        return 1;  // Failure
    }

    // Safe to use sd
    script_pushint(st, sd->status.base_level);
    return 0;  // Success
}
```

---

## Input Validation

### **1. Validate All User Input**

```cpp
// ❌ WRONG - No validation
BUILDIN_FUNC(bad_command)
{
    struct map_session_data *sd = script_rid2sd(st);
    int item_id = script_getnum(st, 2);
    int amount = script_getnum(st, 3);

    // What if item_id is invalid? What if amount is negative?
    pc_giveitem(sd, item_id, amount, LOG_TYPE_SCRIPT);
}

// ✅ CORRECT - Full validation
BUILDIN_FUNC(good_command)
{
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) return 1;

    int item_id = script_getnum(st, 2);
    int amount = script_getnum(st, 3);

    // Validate item ID
    if (!itemdb_exists(item_id)) {
        ShowError("good_command: Invalid item ID %d\n", item_id);
        clif_displaymessage(sd->fd, "Invalid item!");
        script_pushint(st, 0);
        return 0;
    }

    // Validate amount
    if (amount <= 0 || amount > MAX_AMOUNT) {
        ShowError("good_command: Invalid amount %d\n", amount);
        clif_displaymessage(sd->fd, "Invalid amount!");
        script_pushint(st, 0);
        return 0;
    }

    // Safe to proceed
    int result = pc_giveitem(sd, item_id, amount, LOG_TYPE_SCRIPT);
    script_pushint(st, result);
    return 0;
}
```

---

### **2. Validate Ranges**

```cpp
// ✅ CORRECT - Range validation
int set_player_stat(struct map_session_data *sd, int stat_type, int value) {
    if (!sd) return 0;

    // Validate stat type
    if (stat_type < SP_STR || stat_type > SP_LUK) {
        ShowError("Invalid stat type: %d\n", stat_type);
        return 0;
    }

    // Validate value range
    if (value < 1 || value > 99) {
        ShowError("Stat value out of range: %d (must be 1-99)\n", value);
        return 0;
    }

    // Safe to apply
    pc_statusup(sd, stat_type, value - status_get_base_status(sd, stat_type));
    return 1;
}
```

---

### **3. Sanitize String Input**

```cpp
// ✅ CORRECT - String sanitization
void process_chat_message(struct map_session_data *sd, const char *message) {
    if (!sd || !message) return;

    // Ensure null termination
    char safe_message[CHAT_SIZE_MAX];
    safestrncpy(safe_message, message, sizeof(safe_message));

    // Validate length
    if (strlen(safe_message) == 0) {
        ShowWarning("Empty chat message from %s\n", sd->status.name);
        return;
    }

    // Escape for SQL if needed
    char escaped[CHAT_SIZE_MAX * 2];
    SQL->EscapeString(map->mysql_handle, escaped, safe_message);

    // Safe to use
    ShowInfo("Chat from %s: %s\n", sd->status.name, safe_message);
}
```

---

## Memory Management

### **1. Always Free What You Allocate**

```cpp
// ❌ WRONG - Memory leak
char *create_message() {
    char *msg = (char*)aMalloc(100);
    strcpy(msg, "Hello");
    return msg;  // Who frees this?
}

// ✅ CORRECT - Clear ownership
char *create_message_caller_frees() {
    char *msg = (char*)aMalloc(100);
    strcpy(msg, "Hello");
    return msg;  // Caller must free with aFree()
}

// Or better:
void create_message_no_alloc(char *buffer, size_t size) {
    safestrncpy(buffer, "Hello", size);  // No allocation needed
}
```

---

### **2. Use rAthena Memory Functions**

```cpp
// ✅ ALWAYS use rAthena memory functions
char *str = (char*)aMalloc(100);     // NOT malloc()
char *str2 = aStrdup("Hello");       // NOT strdup()
char *str3 = aCalloc(10, 100);       // NOT calloc()
char *str4 = aRealloc(str, 200);     // NOT realloc()
aFree(str);                          // NOT free()
```

**Why?** rAthena's memory manager:
- Tracks allocations for leak detection
- Provides better error messages
- Integrates with debugging tools

---

### **3. Script Return Strings**

```cpp
// ❌ WRONG - Memory leak
BUILDIN_FUNC(bad_get_string)
{
    char *str = (char*)aMalloc(100);
    strcpy(str, "Hello");
    script_pushstr(st, str);  // Leaked if script doesn't use it!
    return 0;
}

// ✅ CORRECT - Use aStrdup for script strings
BUILDIN_FUNC(good_get_string)
{
    script_pushstr(st, aStrdup("Hello"));  // Script engine will free this
    return 0;
}

// ✅ CORRECT - Constant strings
BUILDIN_FUNC(good_get_const_string)
{
    script_pushconststr(st, "Hello");  // No allocation, no free needed
    return 0;
}
```

---

### **4. Check Allocation Success**

```cpp
// ✅ CORRECT - Check allocation
char *str = (char*)aMalloc(1000000000);  // Very large allocation
if (!str) {
    ShowError("Failed to allocate memory!\n");
    return 0;
}

// Use str...
aFree(str);
```

---

## Error Handling

### **1. Use ShowError/ShowWarning**

```cpp
// ✅ CORRECT - Proper error reporting
if (!itemdb_exists(item_id)) {
    ShowError("process_item: Invalid item ID %d\n", item_id);
    return 0;
}

if (amount > MAX_AMOUNT) {
    ShowWarning("process_item: Amount %d exceeds maximum %d, capping\n",
                amount, MAX_AMOUNT);
    amount = MAX_AMOUNT;
}

ShowInfo("Processed item %d x%d for player %s\n",
         item_id, amount, sd->status.name);
```

---

### **2. Return Appropriate Values**

```cpp
// ✅ CORRECT - Clear return values
/**
 * @return: 1 on success, 0 on failure
 */
int process_action(struct map_session_data *sd) {
    if (!sd) {
        ShowError("process_action: NULL player\n");
        return 0;  // Failure
    }

    // Process...

    return 1;  // Success
}

// Usage:
if (!process_action(sd)) {
    ShowError("Failed to process action!\n");
    return;
}
```

---

### **3. Handle Edge Cases**

```cpp
// ✅ CORRECT - Handle edge cases
int divide_safe(int a, int b) {
    // Edge case: division by zero
    if (b == 0) {
        ShowWarning("divide_safe: Division by zero, returning 0\n");
        return 0;
    }

    // Edge case: integer overflow
    if (a == INT_MIN && b == -1) {
        ShowWarning("divide_safe: Integer overflow, returning max\n");
        return INT_MAX;
    }

    return a / b;
}
```

---

## Performance Considerations

### **1. Avoid Unnecessary Calculations**

```cpp
// ❌ SLOW - Repeated database lookups
for (int i = 0; i < 1000; i++) {
    std::shared_ptr<item_data> item = item_db.find(501);
    ShowInfo("Item: %s\n", item->name.c_str());
}

// ✅ FAST - Cache the lookup
std::shared_ptr<item_data> item = item_db.find(501);
if (item) {
    for (int i = 0; i < 1000; i++) {
        ShowInfo("Item: %s\n", item->name.c_str());
    }
}
```

---

### **2. Use Appropriate Data Structures**

```cpp
// ❌ SLOW - Linear search in array
int find_player_index(struct map_session_data *players[], int count, int char_id) {
    for (int i = 0; i < count; i++) {
        if (players[i]->status.char_id == char_id) {
            return i;
        }
    }
    return -1;  // O(n) lookup
}

// ✅ FAST - Use hash map
std::unordered_map<int, struct map_session_data*> player_map;

// Insert: O(1)
player_map[sd->status.char_id] = sd;

// Lookup: O(1)
auto it = player_map.find(char_id);
if (it != player_map.end()) {
    struct map_session_data *sd = it->second;
}
```

---

### **3. Minimize String Operations**

```cpp
// ❌ SLOW - Repeated string concatenation
char message[1000] = "";
for (int i = 0; i < 100; i++) {
    strcat(message, "Item ");  // O(n) each iteration = O(n²) total
}

// ✅ FAST - Use sprintf or single buffer
char message[1000];
int offset = 0;
for (int i = 0; i < 100; i++) {
    offset += sprintf(message + offset, "Item ");  // O(1) append
}
```

---

### **4. Avoid Allocations in Hot Paths**

```cpp
// ❌ SLOW - Allocation every call
void process_damage(int damage) {
    char *msg = (char*)aMalloc(100);  // Allocation in hot path!
    sprintf(msg, "Damage: %d", damage);
    ShowInfo("%s\n", msg);
    aFree(msg);
}

// ✅ FAST - Stack allocation
void process_damage(int damage) {
    char msg[100];  // Stack allocation, no malloc overhead
    sprintf(msg, "Damage: %d", damage);
    ShowInfo("%s\n", msg);
}
```

---

## Documentation Standards

### **1. Function Documentation**

```cpp
/**
 * Heals a player and optionally shows visual effect
 * @param sd: Target player (must not be NULL)
 * @param hp: Amount of HP to restore (negative values will damage)
 * @param sp: Amount of SP to restore (negative values will consume)
 * @param type: Heal type
 *              - 0: Silent heal (no effect)
 *              - 1: Normal heal (with effect)
 *              - 2: Item heal (different effect)
 * @return: Actual HP restored (may be less than requested due to max HP cap)
 * @note: Will cap healing to max HP/SP
 * @warning: Caller must ensure sd is valid!
 */
int pc_heal(struct map_session_data *sd, int hp, int sp, int type) {
    // Implementation
}
```

---

### **2. Complex Algorithm Documentation**

```cpp
/**
 * Calculate weapon damage using Renewal formula
 *
 * Formula breakdown:
 * 1. Base ATK = (Status ATK + Weapon ATK + Refine Bonus)
 * 2. Weapon Multiplier = (Base ATK * Weapon Mastery * Card Modifiers)
 * 3. Final ATK = Weapon Multiplier * Skill Modifier
 * 4. Apply DEF reduction: Damage = Final ATK - (Target DEF * 0.5)
 * 5. Apply random variance: Damage += random(-5%, +5%)
 *
 * @see battle.cpp:battle_calc_weapon_attack for full implementation
 * @see doc/damage_formulas.txt for detailed explanation
 */
static struct Damage calculate_weapon_damage(...) {
    // Implementation
}
```

---

### **3. TODO/FIXME Comments**

```cpp
// TODO: Implement support for 4th job classes
// FIXME: This function crashes if sd->inventory is NULL
// HACK: Temporary workaround for client bug, remove when client is fixed
// NOTE: This behavior differs from official servers
```

---

## Testing Guidelines

### **1. Unit Testing Pattern**

```cpp
// Test function
void test_damage_calculation() {
    // Setup
    int atk = 100;
    int def = 50;

    // Execute
    int damage = calculate_damage(atk, def);

    // Verify
    if (damage == 50) {
        ShowInfo("test_damage_calculation: PASS\n");
    } else {
        ShowError("test_damage_calculation: FAIL (expected 50, got %d)\n", damage);
    }
}

// Call from OnInit
OnInit:
    test_damage_calculation();
    end;
```

---

### **2. Edge Case Testing**

```cpp
// Test edge cases
void test_divide_function() {
    // Normal case
    assert(divide_safe(10, 2) == 5);

    // Edge case: division by zero
    assert(divide_safe(10, 0) == 0);

    // Edge case: integer overflow
    assert(divide_safe(INT_MIN, -1) == INT_MAX);

    // Edge case: negative numbers
    assert(divide_safe(-10, 2) == -5);

    ShowInfo("All tests passed!\n");
}
```

---

### **3. In-Game Testing**

```
@job 0  # Test with Novice
@job 4001  # Test with Swordsman
@blevel 1  # Test at level 1
@blevel 99  # Test at level 99
@item 501 0  # Test with 0 items
@item 501 30000  # Test with max stack
@monster 1002 1  # Test single mob
@monster 1002 1000  # Test many mobs
```

---

## Common Mistakes to Avoid

### **1. Off-By-One Errors**

```cpp
// ❌ WRONG - Array out of bounds
int arr[10];
for (int i = 0; i <= 10; i++) {  // Should be i < 10
    arr[i] = 0;  // Writes to arr[10] = out of bounds!
}

// ✅ CORRECT
for (int i = 0; i < 10; i++) {
    arr[i] = 0;
}
```

---

### **2. Skill Level Index Confusion**

```cpp
// ❌ WRONG - Skill levels are 1-indexed, arrays are 0-indexed
uint16 skill_lv = 10;
int cast_time = skill->cast[skill_lv];  // Out of bounds!

// ✅ CORRECT
uint16 skill_lv = 10;
int cast_time = skill->cast[skill_lv - 1];  // Array index 9
```

---

### **3. Integer Overflow**

```cpp
// ❌ WRONG - Overflow risk
int damage = atk * multiplier;  // What if atk=100000, multiplier=100000?

// ✅ CORRECT - Use larger type
int64 damage = (int64)atk * multiplier;
if (damage > INT_MAX) damage = INT_MAX;
```

---

### **4. Modifying Const Data**

```cpp
// ❌ WRONG - Modifying const string
const char *str = script_getstr(st, 2);
str[0] = 'X';  // CRASH!

// ✅ CORRECT - Copy if you need to modify
const char *str = script_getstr(st, 2);
char *copy = aStrdup(str);
copy[0] = 'X';
aFree(copy);
```

---

### **5. Ignoring Return Values**

```cpp
// ❌ WRONG - Ignoring failure
pc_giveitem(sd, item_id, amount, LOG_TYPE_SCRIPT);
// What if inventory is full?

// ✅ CORRECT - Check return value
int result = pc_giveitem(sd, item_id, amount, LOG_TYPE_SCRIPT);
if (result != 0) {
    clif_displaymessage(sd->fd, "Inventory full!");
}
```

---

## Code Review Checklist

Before committing code, check:

- [ ] **Null checks**: All pointers checked before use
- [ ] **Input validation**: All user input validated
- [ ] **Memory leaks**: All allocations have corresponding frees
- [ ] **Error handling**: All errors logged and handled
- [ ] **Documentation**: Complex functions have comments
- [ ] **Naming**: Variables and functions have clear names
- [ ] **Formatting**: Code follows rAthena style (tabs, braces)
- [ ] **Testing**: Code tested with edge cases
- [ ] **Performance**: No obvious performance issues
- [ ] **Compiler warnings**: No warnings when compiled with `-Wall`

---

## Related References

- **Source Structure**: [KB_REF_SourceCodeStructure.md]
- **Common Modifications**: [KB_REF_CommonSrcModifications.md]
- **Compilation/Debugging**: [KB_REF_CompilationDebugging.md]
- **Database Work**: [KB_REF_DatabaseCPP.md]

---

**End of KB_REF_029 - Source Code Best Practices**
