---
kb_id: KB_REF_040
title: "rAthena Source Code Best Practices Guide"
category: Source Code Development
keywords: [best_practices, coding_standards, code_quality, safety, memory_management, performance, error_handling, testing, git, code_review, refactoring, anti_patterns, security]
related_files: [
  "src/common/malloc.hpp",
  "src/common/ers.hpp",
  "src/common/nullpo.hpp",
  "src/common/showmsg.hpp",
  "src/common/utilities.hpp",
  "src/common/strlib.hpp",
  "src/map/skill.cpp",
  "src/map/pc.cpp",
  "src/map/clif.cpp"
]
difficulty: intermediate
use_case: "Comprehensive guide for writing safe, maintainable, and high-quality C++ code for rAthena"
version: rAthena 2024
last_updated: 2024-01-15
---

# rAthena Source Code Best Practices Guide

## Table of Contents

1. [Code Style & Formatting](#code-style)
2. [Safety Patterns](#safety-patterns)
3. [Memory Management](#memory-management)
4. [Performance Optimization](#performance)
5. [Error Handling](#error-handling)
6. [Testing & Debugging](#testing)
7. [Common Mistakes](#common-mistakes)
8. [Documentation Standards](#documentation)
9. [Git Best Practices](#git-practices)
10. [Code Review Checklist](#code-review)
11. [Refactoring Guidelines](#refactoring)
12. [Real Anti-Patterns from rAthena](#anti-patterns)

---

## 1. Code Style & Formatting {#code-style}

### Naming Conventions

**Use lowercase_with_underscores for everything:**

```cpp
// CORRECT
int32 skill_get_range(uint16 skill_id, uint16 skill_lv);
struct map_session_data *sd;
class skill_database;
void pc_calcstatus(map_session_data *sd, enum e_status_calc_opt opt);

// WRONG
int32 SkillGetRange(uint16 skillId, uint16 skillLv);  // camelCase
int32 GetSkillRange(uint16 skill_id, uint16 skill_lv);  // PascalCase
struct MapSessionData *sd;  // PascalCase for structs
```

**Constants and Macros:**
```cpp
#define MAX_SKILL_LEVEL 13
#define SKILLUNITTIMER_INTERVAL 100
#define ALC_MARK __FILE__, __LINE__, __func__

enum e_damage_type {
    DMG_NORMAL,
    DMG_PICKUP_ITEM,
    DMG_SPLASH
};
```

### Indentation & Braces

**Use TABS for indentation, K&R brace style:**

```cpp
// CORRECT - K&R style (opening brace on same line)
int32 skill_castend_nodamage_id(block_list *src, block_list *bl, uint16 skill_id, uint16 skill_lv) {
	if (!src || !bl)
		return 0;

	if (skill_id == 0) {
		ShowError("skill_castend_nodamage_id: Invalid skill_id %d\n", skill_id);
		return 0;
	}

	// Function body
	return 1;
}

// WRONG - Allman style
int32 skill_castend_nodamage_id(block_list *src, block_list *bl, uint16 skill_id, uint16 skill_lv)
{  // Opening brace on new line - WRONG for rAthena
	// ...
}
```

**Single-line conditionals:**
```cpp
// Braces optional for single statements, but use consistent style
if (!sd)
	return 0;

// Or with braces (preferred for clarity)
if (!sd) {
	return 0;
}

// For multiple statements, ALWAYS use braces
if (!sd) {
	ShowError("sd is null\n");
	return 0;
}
```

### File Headers

**Every source file must have a copyright header:**

```cpp
// Copyright (c) rAthena Dev Teams - Licensed under GNU GPL
// For more information, see LICENCE in the main folder

#ifndef SKILL_HPP
#define SKILL_HPP

#include <common/cbasetypes.hpp>
// ... more includes
```

### Include Order

**Standard include order:**

```cpp
#include "local_header.hpp"      // Current module's header first

#include <array>                 // C++ standard library
#include <cmath>
#include <cstdio>
#include <cstring>

#include <common/cbasetypes.hpp> // Common rAthena headers
#include <common/ers.hpp>
#include <common/malloc.hpp>
#include <common/nullpo.hpp>

#include "battle.hpp"            // Other map server headers (alphabetical)
#include "clif.hpp"
#include "pc.hpp"
#include "status.hpp"
```

---

## 2. Safety Patterns {#safety-patterns}

### NULL/nullptr Checks - ALWAYS

**NEVER assume a pointer is valid. ALWAYS check:**

```cpp
// CORRECT - Always check pointers
int32 skill_attack(int32 attack_type, block_list* src, block_list *dsrc,
                   block_list *bl, uint16 skill_id, uint16 skill_lv) {
	nullpo_ret(src);      // Returns 0 if src is NULL
	nullpo_ret(dsrc);
	nullpo_ret(bl);

	// Now safe to use these pointers
	// ...
}

// Using nullpo variants
void some_function(map_session_data *sd) {
	nullpo_retv(sd);   // Returns void if NULL

	// For custom messages
	nullpo_ret_f(sd, "Player data is null in some_function for account %d", account_id);

	// For custom return values
	nullpo_retr(-1, sd);  // Returns -1 if NULL
}

// WRONG - No null checks
int32 skill_attack(int32 attack_type, block_list* src, block_list *dsrc,
                   block_list *bl, uint16 skill_id, uint16 skill_lv) {
	// CRASH WAITING TO HAPPEN!
	int32 src_type = src->type;  // What if src is NULL?
}
```

**Check before dereferencing:**

```cpp
// CORRECT
map_session_data *sd = map_id2sd(account_id);
if (!sd) {
	ShowWarning("Player not found: %d\n", account_id);
	return 0;
}
sd->status.zeny += amount;  // Safe

// WRONG - Dereferencing without checking
map_session_data *sd = map_id2sd(account_id);
sd->status.zeny += amount;  // CRASH if sd is NULL!
```

### Input Validation

**Validate ALL input from client or external sources:**

```cpp
// CORRECT - Validate skill level range
void skill_use(map_session_data *sd, uint16 skill_id, uint16 skill_lv) {
	nullpo_retv(sd);

	// Validate skill exists
	if (!skill_check(skill_id)) {
		ShowError("Invalid skill_id %d requested by player %d\n",
		          skill_id, sd->status.account_id);
		return;
	}

	// Validate level (skills are 0-indexed but use 1-based levels)
	if (skill_lv < 1 || skill_lv > MAX_SKILL_LEVEL) {
		ShowWarning("Invalid skill_lv %d for skill %d\n", skill_lv, skill_id);
		return;
	}

	// Cap the value to safe range
	skill_lv = cap_value(skill_lv, 1, MAX_SKILL_LEVEL);
}

// WRONG - No validation
void skill_use(map_session_data *sd, uint16 skill_id, uint16 skill_lv) {
	// What if skill_lv is 999? Array overflow!
	int32 sp_cost = skill_db[skill_id]->sp[skill_lv];
}
```

### Bounds Checking

**Always validate array indices:**

```cpp
// CORRECT - Use cap_value to ensure bounds
int32 index = cap_value(item_index, 0, MAX_INVENTORY - 1);
item = &sd->inventory.u.items_inventory[index];

// CORRECT - Check before accessing
if (item_index < 0 || item_index >= MAX_INVENTORY) {
	ShowError("Invalid inventory index %d\n", item_index);
	return 0;
}
item = &sd->inventory.u.items_inventory[item_index];

// WRONG - No bounds checking
item = &sd->inventory.u.items_inventory[item_index];  // Buffer overflow!
```

**Use safe utility functions:**

```cpp
// From src/common/utilities.hpp

// Cap a value between min and max
skill_lv = cap_value(skill_lv, 1, MAX_SKILL_LEVEL);

// Safe addition with overflow detection
int64 result;
if (rathena::util::safe_addition(a, b, result)) {
	ShowError("Integer overflow detected in addition\n");
	return 0;
}

// Safe addition with cap
int32 new_zeny = rathena::util::safe_addition_cap(sd->status.zeny, amount, MAX_ZENY);
```

---

## 3. Memory Management {#memory-management}

### Use aMalloc/aFree, NOT malloc/free

**rAthena has its own memory manager with leak tracking:**

```cpp
// CORRECT - Use rAthena's memory manager
struct some_data *data = (struct some_data *)aMalloc(sizeof(struct some_data));
if (!data) {
	ShowFatalError("Failed to allocate memory\n");
	return 0;
}
aFree(data);

// CORRECT - Use CREATE macro
struct some_data *data;
CREATE(data, struct some_data, 1);

// For arrays
struct item *items;
CREATE(items, struct item, MAX_INVENTORY);
aFree(items);

// WRONG - Don't use standard malloc/free
struct some_data *data = (struct some_data *)malloc(sizeof(struct some_data));
free(data);  // Memory leak tracking won't work!
```

**Memory allocation macros:**

```cpp
// From src/common/malloc.hpp

#define aMalloc(n)         _mmalloc(n, ALC_MARK)
#define aCalloc(m,n)       _mcalloc(m, n, ALC_MARK)
#define aRealloc(p,n)      _mrealloc(p, n, ALC_MARK)
#define aStrdup(p)         _mstrdup(p, ALC_MARK)
#define aFree(p)           _mfree(p, ALC_MARK)

#define CREATE(result, type, number) \
	(result) = (type *)aCalloc((number), sizeof(type))

#define RECREATE(result, type, number) \
	(result) = (type *)aRealloc((result), sizeof(type) * (number))
```

### Entry Reusage System (ERS)

**Use ERS for frequently allocated/freed structures:**

```cpp
// ERS is a memory pool system that reduces allocation overhead
// Perfect for structures that are created/destroyed frequently

// From src/map/skill.cpp
static struct eri *skill_timer_ers = nullptr;

// Initialize in init function
void skill_init() {
	skill_timer_ers = ers_new(sizeof(struct skill_timerskill),
	                          "skill_timer_ers",
	                          ERS_OPT_NONE);
}

// Allocate from pool
struct skill_timerskill *timer_data;
timer_data = ers_alloc(skill_timer_ers, struct skill_timerskill);

// Free back to pool (reusable)
ers_free(skill_timer_ers, timer_data);

// Cleanup in final function
void skill_final() {
	ers_destroy(skill_timer_ers);
}
```

**When to use ERS vs aMalloc:**

- **Use ERS:** Frequently allocated/freed small structures (skill timers, quest data, temporary buffs)
- **Use aMalloc:** One-time allocations, large buffers, variable-sized data

### Memory Leak Prevention

**Always free what you allocate:**

```cpp
// CORRECT - Paired allocation/deallocation
char *buffer = (char *)aMalloc(1024);
if (!buffer) {
	return 0;
}

// ... use buffer ...

aFree(buffer);  // Always free!

// WRONG - Memory leak
char *buffer = (char *)aMalloc(1024);
if (some_error) {
	return 0;  // LEAK! Forgot to free buffer
}
aFree(buffer);
```

**Use early returns carefully:**

```cpp
// CORRECT - Free before all return paths
char *buffer = (char *)aMalloc(1024);
if (!buffer) {
	return 0;
}

if (error_condition) {
	aFree(buffer);  // Free before return
	return 0;
}

// ... more code ...

aFree(buffer);
return 1;

// BETTER - Use scope-based cleanup when possible
{
	CREATE_BUFFER(buffer, char, 1024);  // Stack-allocated on GCC

	// ... use buffer ...

	// Automatically cleaned up at end of scope
	DELETE_BUFFER(buffer);
}
```

---

## 4. Performance Optimization {#performance}

### Cache Lookups

**Don't repeat expensive lookups in loops:**

```cpp
// WRONG - Repeated expensive lookups
for (int i = 0; i < MAX_INVENTORY; i++) {
	if (pc_checkskill(sd, SM_BASH) > 5) {  // Lookup every iteration!
		// ...
	}
}

// CORRECT - Cache the lookup
int32 bash_lv = pc_checkskill(sd, SM_BASH);
for (int i = 0; i < MAX_INVENTORY; i++) {
	if (bash_lv > 5) {  // Use cached value
		// ...
	}
}

// WRONG - Repeated database lookups
for (auto &item : inventory) {
	struct item_data *id = itemdb_search(item.nameid);  // DB lookup each time
	if (id->type == IT_WEAPON) {
		// ...
	}
}

// CORRECT - Cache the lookup if used multiple times
struct item_data *id = itemdb_search(item.nameid);
if (!id) continue;

if (id->type == IT_WEAPON) {
	// ... use id ...
}
```

### Avoid Allocations in Loops

**Move allocations outside of hot loops:**

```cpp
// WRONG - Allocating inside loop
for (int i = 0; i < 1000; i++) {
	char *buffer = (char *)aMalloc(256);
	sprintf(buffer, "Item %d", i);
	// ...
	aFree(buffer);
}

// CORRECT - Single allocation, reuse
char buffer[256];
for (int i = 0; i < 1000; i++) {
	sprintf(buffer, "Item %d", i);
	// ...
}

// CORRECT - Stack buffer when size is known
CREATE_BUFFER(buffer, char, 256);
for (int i = 0; i < 1000; i++) {
	sprintf(buffer, "Item %d", i);
	// ...
}
DELETE_BUFFER(buffer);
```

### Early Returns

**Exit early to avoid unnecessary computation:**

```cpp
// CORRECT - Early return pattern
int32 skill_check_condition(map_session_data *sd, uint16 skill_id, uint16 skill_lv) {
	nullpo_ret(sd);

	// Quick checks first
	if (skill_id == 0)
		return 0;

	if (skill_lv < 1 || skill_lv > MAX_SKILL_LEVEL)
		return 0;

	if (pc_isdead(sd))
		return 0;

	// Expensive checks only if needed
	if (!skill_check_pc_partner(sd, skill_id, &skill_lv, 1, 0))
		return 0;

	// ... rest of function
	return 1;
}

// WRONG - Deep nesting, all checks even if unnecessary
int32 skill_check_condition(map_session_data *sd, uint16 skill_id, uint16 skill_lv) {
	if (sd != nullptr) {
		if (skill_id != 0) {
			if (skill_lv >= 1 && skill_lv <= MAX_SKILL_LEVEL) {
				if (!pc_isdead(sd)) {
					// ... deeply nested code
				}
			}
		}
	}
}
```

### Use const References for Large Objects

```cpp
// CORRECT - Pass by const reference
void process_skill_data(const std::shared_ptr<s_skill_db> &skill_data) {
	// No copy, read-only access
}

// WRONG - Pass by value (copies the shared_ptr)
void process_skill_data(std::shared_ptr<s_skill_db> skill_data) {
	// Unnecessary copy overhead
}
```

### String Operations

**Use safe string functions:**

```cpp
// CORRECT - Use safestrncpy (always null-terminates)
char name[NAME_LENGTH];
safestrncpy(name, player_name, sizeof(name));

// WRONG - strncpy doesn't guarantee null-termination
strncpy(name, player_name, sizeof(name));  // May not be null-terminated!

// CORRECT - safesnprintf (always null-terminates)
char message[256];
safesnprintf(message, sizeof(message), "Player %s has %d zeny", sd->status.name, sd->status.zeny);

// Use trim to remove whitespace
char *trimmed = trim(input_string);
```

---

## 5. Error Handling {#error-handling}

### Use Proper Error Reporting Functions

**rAthena provides several error reporting levels:**

```cpp
// From src/common/showmsg.hpp

// ShowMessage - General messages (white)
ShowMessage("Server starting...\n");

// ShowStatus - Status updates (green)
ShowStatus("Loading skill database...\n");

// ShowInfo - Information (cyan)
ShowInfo("Player %s logged in\n", sd->status.name);

// ShowNotice - Important notices (yellow)
ShowNotice("Server is shutting down in 5 minutes\n");

// ShowWarning - Non-critical issues (yellow/orange)
ShowWarning("Invalid item ID %d in player inventory\n", item_id);

// ShowDebug - Debug information (gray) - only in DEBUG builds
ShowDebug("skill_check_condition: skill_id=%d, skill_lv=%d\n", skill_id, skill_lv);

// ShowError - Errors that are handled (red)
ShowError("Failed to load map: %s\n", mapname);

// ShowFatalError - Critical errors that cause shutdown (bright red)
ShowFatalError("Failed to connect to database\n");
```

### Error Reporting Best Practices

```cpp
// CORRECT - Provide context and useful information
if (!itemdb_exists(item_id)) {
	ShowError("pc_additem: Invalid item_id %d for player %s (AID:%d/CID:%d)\n",
	          item_id, sd->status.name, sd->status.account_id, sd->status.char_id);
	return 1;
}

// WRONG - Vague error message
if (!itemdb_exists(item_id)) {
	ShowError("Invalid item\n");  // Which item? Which player? Where?
	return 1;
}

// CORRECT - Use appropriate error level
if (amount > MAX_AMOUNT) {
	ShowWarning("Amount %d exceeds maximum, capping to %d\n", amount, MAX_AMOUNT);
	amount = MAX_AMOUNT;  // Handle the error, continue
}

// WRONG - Using error for non-critical issues
if (amount > MAX_AMOUNT) {
	ShowError("Amount exceeds maximum\n");  // Should be ShowWarning
	amount = MAX_AMOUNT;
}
```

### Return Value Patterns

**Use consistent return values:**

```cpp
// Standard return patterns:
// 0 = success
// 1 = failure/error
// -1 = specific error condition (documented)

// CORRECT
int32 pc_additem(map_session_data *sd, struct item *item_data, int32 amount) {
	nullpo_retr(1, sd);
	nullpo_retr(1, item_data);

	if (amount <= 0) {
		ShowError("pc_additem: Invalid amount %d\n", amount);
		return 1;  // Error
	}

	// ... add item logic ...

	return 0;  // Success
}

// For functions returning pointers:
// Return NULL/nullptr on failure, valid pointer on success

struct item_data *itemdb_search(t_itemid nameid) {
	if (nameid == 0)
		return nullptr;  // Invalid ID

	auto it = itemdb.find(nameid);
	if (it == itemdb.end())
		return nullptr;  // Not found

	return it->second.get();  // Found
}
```

---

## 6. Testing & Debugging {#testing}

### Debug Builds

**Always test in debug builds first:**

```bash
# Build with debug symbols and checks
cmake -DCMAKE_BUILD_TYPE=Debug ..
cmake --build .

# This enables:
# - NULLPO_CHECK (null pointer checks)
# - Memory leak detection
# - Assert statements
# - ShowDebug messages
```

### Use ShowDebug for Development

```cpp
// ShowDebug only appears in DEBUG builds
#ifdef DEBUG
	ShowDebug("skill_attack: src=%s, target=%s, skill=%d, damage=%d\n",
	          status_get_name(src), status_get_name(bl), skill_id, damage);
#endif

// Or use ShowDebug directly (automatically disabled in release)
ShowDebug("Processing %d items in inventory\n", sd->inventory_data_count);
```

### GDB Debugging

**Essential GDB commands for rAthena:**

```bash
# Start server in GDB
gdb ./map-server

# Set breakpoint
break skill_attack
break skill.cpp:1234

# Run with arguments
run --map-config conf/map-server.conf

# When crashed, get backtrace
bt
bt full  # With variable values

# Inspect variables
print sd->status.name
print *bl
print skill_db[skill_id]

# Conditional breakpoints
break pc_additem if item_id == 501

# Continue execution
continue
```

### Unit Testing

**Test edge cases:**

```cpp
// Test boundary conditions
void test_skill_level_validation() {
	// Test minimum
	assert(skill_check_level(skill_id, 1) == true);

	// Test maximum
	assert(skill_check_level(skill_id, MAX_SKILL_LEVEL) == true);

	// Test below minimum
	assert(skill_check_level(skill_id, 0) == false);

	// Test above maximum
	assert(skill_check_level(skill_id, MAX_SKILL_LEVEL + 1) == false);

	// Test negative (integer underflow)
	assert(skill_check_level(skill_id, -1) == false);
}

// Test null pointer handling
void test_null_pointers() {
	assert(skill_attack(src, NULL, bl, skill_id, skill_lv) == 0);
	assert(skill_attack(NULL, dsrc, bl, skill_id, skill_lv) == 0);
}
```

### Common Debug Scenarios

**Tracking memory issues:**

```cpp
// Enable memory manager logging
#define LOG_MEMMGR

// Check for memory leaks at shutdown
malloc_memory_check();

// Verify pointer validity
if (!malloc_verify_ptr(ptr)) {
	ShowError("Invalid pointer detected: %p\n", ptr);
}

// Get memory usage statistics
size_t memory_used = malloc_usage();
ShowInfo("Memory usage: %zu bytes\n", memory_used);
```

---

## 7. Common Mistakes {#common-mistakes}

### Off-by-One Errors

```cpp
// WRONG - Off-by-one (will access index 100 which is out of bounds)
for (int i = 0; i <= MAX_INVENTORY; i++) {  // Should be <, not <=
	process_item(&sd->inventory.u.items_inventory[i]);
}

// CORRECT
for (int i = 0; i < MAX_INVENTORY; i++) {
	process_item(&sd->inventory.u.items_inventory[i]);
}

// WRONG - String buffer overflow
char name[24];
strncpy(name, input, 24);  // If input is 24 chars, no room for null terminator!

// CORRECT
char name[NAME_LENGTH];
safestrncpy(name, input, sizeof(name));  // Always null-terminates
```

### Skill Level Array Indexing

**CRITICAL: Skill levels are 1-based but arrays are 0-indexed!**

```cpp
// Skills use levels 1-10, but arrays are indexed 0-9

// CORRECT - Subtract 1 for array access
int32 sp_cost = skill_db.find(skill_id)->sp[skill_lv - 1];

// WRONG - Direct indexing
int32 sp_cost = skill_db.find(skill_id)->sp[skill_lv];  // Off by one!

// CORRECT - Using the skill_get_lv macro which handles this
#define skill_get_lv(id, lv, arrvar) do {\
	if (!skill_check(id))\
		return 0;\
	int32 lv_idx = min(lv, MAX_SKILL_LEVEL) - 1;\  // Converts to 0-based
	// ... extrapolation for levels > MAX_SKILL_LEVEL
	return arrvar[lv_idx];\
} while(0)
```

### Integer Overflow

```cpp
// WRONG - Integer overflow possible
int32 total_damage = base_damage * multiplier;  // Overflow if values are large!

// CORRECT - Use safe_multiplication
int64 total_damage;
if (rathena::util::safe_multiplication(base_damage, multiplier, total_damage)) {
	ShowWarning("Integer overflow in damage calculation\n");
	total_damage = INT_MAX;  // Cap to maximum
}

// WRONG - Zeny overflow
sd->status.zeny += amount;  // Can overflow!

// CORRECT - Check before addition
if (sd->status.zeny > MAX_ZENY - amount) {
	ShowWarning("Zeny overflow prevented for player %s\n", sd->status.name);
	sd->status.zeny = MAX_ZENY;
} else {
	sd->status.zeny += amount;
}

// BETTER - Use safe_addition_cap
sd->status.zeny = rathena::util::safe_addition_cap(sd->status.zeny, amount, MAX_ZENY);
```

### Buffer Overflow

```cpp
// WRONG - sprintf can overflow
char message[128];
sprintf(message, "Player %s has %d items", sd->status.name, count);  // Overflow if name is long!

// CORRECT - Use safesnprintf
char message[128];
safesnprintf(message, sizeof(message), "Player %s has %d items", sd->status.name, count);

// WRONG - strcpy can overflow
char buffer[64];
strcpy(buffer, input);  // Overflow if input > 64 bytes!

// CORRECT - Use safestrncpy
char buffer[64];
safestrncpy(buffer, input, sizeof(buffer));
```

### Signed/Unsigned Comparison

```cpp
// WRONG - Comparing signed with unsigned
int32 item_count = -1;  // Error value
if (item_count < MAX_INVENTORY) {  // MAX_INVENTORY is unsigned, comparison fails!
	// This will be true because -1 becomes a huge unsigned number!
}

// CORRECT - Cast or use same signedness
if (item_count >= 0 && (uint32)item_count < MAX_INVENTORY) {
	// ...
}

// BETTER - Use signed types for values that can be negative
int32 item_count = get_item_count();
if (item_count < 0) {
	ShowError("Invalid item count\n");
	return;
}
if (item_count < (int32)MAX_INVENTORY) {
	// ...
}
```

### Type Confusion

```cpp
// WRONG - Using wrong type for item IDs
int32 item_id = 501;  // Should be t_itemid!

// CORRECT - Use proper types
t_itemid item_id = 501;

// WRONG - Using int for flags (wastes memory in structs)
struct item_data {
	int32 is_weapon;  // Only needs 1 byte!
	int32 is_armor;
};

// CORRECT - Use appropriate sized types
struct item_data {
	uint8 is_weapon : 1;  // Bitfield
	uint8 is_armor : 1;
	// Or
	bool is_weapon;  // 1 byte
	bool is_armor;
};
```

---

## 8. Documentation Standards {#documentation}

### Comment What WHY, Not WHAT

```cpp
// WRONG - Comments describe WHAT code does (obvious from code itself)
// Increment player zeny by amount
sd->status.zeny += amount;

// Loop through inventory
for (int i = 0; i < MAX_INVENTORY; i++) {
	// Check if item exists
	if (sd->inventory.u.items_inventory[i].nameid == 0)
		continue;
}

// CORRECT - Comments explain WHY, context, and non-obvious behavior
// Add zeny reward for quest completion
// Note: This bypasses the normal MAX_ZENY check because quest rewards
// are server-controlled and should always succeed
sd->status.zeny += amount;

// Search for broken equipment to repair
// We only check weapon/armor slots (EQP_WEAPON | EQP_ARMOR)
// because accessories cannot break in official behavior
for (int i = 0; i < MAX_INVENTORY; i++) {
	if (sd->inventory.u.items_inventory[i].nameid == 0)
		continue;

	// ...
}
```

### Function Documentation

**Document complex functions with headers:**

```cpp
/**
 * Calculate final skill damage after all modifiers
 * @param src: Source of the skill (attacker)
 * @param target: Target of the skill (defender)
 * @param skill_id: Skill being used
 * @param skill_lv: Level of the skill (1-based, 1-10 or 1-MAX_SKILL_LEVEL)
 * @param base_damage: Base damage before modifiers
 * @param flag: Flags affecting damage calculation (BCT_ENEMY, etc.)
 * @return Final damage value after all modifiers, or 0 on error
 *
 * Notes:
 * - Applies elemental modifiers, card effects, skill multipliers
 * - Handles special cases like boss monsters (20% reduction)
 * - May return 0 if target has invincibility status
 */
int32 battle_calc_skill_damage(block_list *src, block_list *target,
                               uint16 skill_id, uint16 skill_lv,
                               int32 base_damage, uint32 flag) {
	// Implementation
}

// For simple/obvious functions, a brief comment is sufficient
// Get skill name from skill ID
const char* skill_get_name(uint16 skill_id) {
	return skill_db.find(skill_id)->name;
}
```

### Documenting Workarounds and Known Issues

```cpp
// CORRECT - Document workarounds with explanation
// FIXME: This is a temporary workaround for issue #1234
// The proper fix requires refactoring the entire skill system
// Remove this once the refactor is complete
if (skill_id == AB_ADORAMUS) {
	skill_lv = min(skill_lv, 10);  // Cap to 10 to prevent crash
}

// TODO: Implement proper skill level scaling for expanded classes
// Currently uses the same formula as rebirth classes

// HACK: Client sends incorrect packet for GM_FULLSTRIP
// We need to swap the bytes to get the correct target ID
if (skill_id == GM_FULLSTRIP) {
	target_id = (target_id >> 16) | (target_id << 16);
}

// BUG: Race condition between trade window and vending
// See issue #5678 for detailed explanation
// Temporary mitigation: Lock inventory during trade
```

### Inline Comments for Complex Logic

```cpp
// Complex damage formula - explain each step
int32 damage = base_damage;

// Apply ATK/MATK multipliers (skill specific)
damage = damage * skill_multiplier / 100;

// Apply elemental modifier (fire vs water = 200%, etc.)
damage = damage * element_table[skill_element][target_element] / 100;

// Apply card effects (addrace, addsize, addelement)
damage = damage * (100 + card_bonus) / 100;

// Apply final reduction (boss monsters take 20% less damage)
if (target->type == BL_MOB && ((mob_data*)target)->status.mode & MD_BOSS)
	damage = damage * 80 / 100;
```

---

## 9. Git Best Practices {#git-practices}

### Commit Messages

**Use clear, descriptive commit messages:**

```bash
# CORRECT - Clear, concise, describes change
git commit -m "Fix integer overflow in zeny transaction"

git commit -m "Add null pointer check in skill_castend_nodamage_id

Fixes crash when target dies during skill cast.
Resolves #1234"

git commit -m "Refactor skill damage calculation

- Split battle_calc_damage into smaller functions
- Extract element modifier calculation
- Add unit tests for edge cases"

# WRONG - Vague, non-descriptive
git commit -m "fix bug"
git commit -m "update"
git commit -m "changes"
git commit -m "WIP"
```

**Commit message format from rAthena history:**

```bash
# Good examples from actual commits:
"Fixed Songs Not Preventing Attacks (#9578)"
"Fixed a possible crash with RODEX"
"Removed some map_freeblock_unlock calls (#9574)"
"Update cost indicator when changing jobs (#9584)"
"Improved strnpcinfo (#9589)"
"Autobonus on Kill (#9594)"
```

### Atomic Commits

**One logical change per commit:**

```bash
# CORRECT - Each commit is one logical change
git add src/map/skill.cpp
git commit -m "Fix skill cooldown not resetting on death"

git add src/map/pc.cpp
git commit -m "Add validation for job change packet"

git add src/map/trade.cpp
git commit -m "Prevent item duplication in trade window"

# WRONG - Multiple unrelated changes in one commit
git add src/map/skill.cpp src/map/pc.cpp src/map/trade.cpp
git commit -m "Various fixes"
```

### Branch Naming

**Use descriptive branch names:**

```bash
# CORRECT - Describes the purpose
git checkout -b fix/skill-cooldown-reset
git checkout -b feature/new-guild-system
git checkout -b refactor/split-skill-functions
git checkout -b hotfix/critical-duplication-exploit

# WRONG - Non-descriptive
git checkout -b patch1
git checkout -b my-changes
git checkout -b test
```

### Before Committing

**Pre-commit checklist:**

```bash
# 1. Build successfully
cmake --build . --target all

# 2. Run any existing tests
ctest

# 3. Check what you're committing
git status
git diff --cached

# 4. No debug code
# Remove: printf, cout, commented code, test hacks

# 5. No merge conflicts
git diff --check
```

---

## 10. Code Review Checklist {#code-review}

### Security Review

- [ ] All client input is validated
- [ ] No SQL injection vulnerabilities
- [ ] No buffer overflows (use safe string functions)
- [ ] Integer overflow checks for arithmetic
- [ ] Proper bounds checking on array access
- [ ] No hardcoded credentials or sensitive data
- [ ] Proper permission checks for GM commands

### Safety Review

- [ ] All pointers are null-checked before use
- [ ] No use-after-free vulnerabilities
- [ ] Memory allocations are freed
- [ ] No memory leaks in error paths
- [ ] Return values are checked
- [ ] Error conditions are handled properly

### Performance Review

- [ ] No allocations inside hot loops
- [ ] Database lookups are cached when used multiple times
- [ ] Early returns for common cases
- [ ] No unnecessary deep copying of large structures
- [ ] Efficient algorithms (avoid O(n²) when O(n) exists)

### Code Quality Review

- [ ] Follows naming conventions (lowercase_with_underscores)
- [ ] Proper indentation (tabs, K&R braces)
- [ ] Functions are not too long (< 100 lines ideal)
- [ ] No code duplication (DRY principle)
- [ ] Clear variable names (no single letter except loops)
- [ ] Comments explain WHY, not WHAT
- [ ] No commented-out code (use git history)

### Correctness Review

- [ ] Skill levels are properly indexed (1-based to 0-based)
- [ ] No off-by-one errors
- [ ] Edge cases are handled (0, negative, max values)
- [ ] Signed/unsigned comparisons are correct
- [ ] Type sizes are appropriate (uint8 vs uint32)
- [ ] Return values match documentation

---

## 11. Refactoring Guidelines {#refactoring}

### When to Refactor

**Refactor when:**
- Function exceeds ~100 lines
- You copy-paste code more than once
- Function has more than 4 parameters
- Deeply nested code (> 3 levels)
- Same pattern appears in multiple places
- Code is hard to understand or test

**Don't refactor when:**
- Code works and is rarely modified
- Refactoring would break existing plugins
- You don't have time to test thoroughly
- It's a micro-optimization with no measurable benefit

### Extract Function

**Before - Long function:**

```cpp
int32 skill_castend_nodamage_id(block_list *src, block_list *bl,
                                uint16 skill_id, uint16 skill_lv) {
	// 500 lines of mixed logic
	if (skill_id == AL_HEAL) {
		int32 heal = skill_lv * 10;
		heal += status_get_max_hp(bl) / 10;
		heal = heal * (100 + pc_checkskill(sd, AL_HEAL)) / 100;
		status_heal(bl, heal, 0, 0);
		clif_skill_nodamage(src, bl, skill_id, heal, 1);
	} else if (skill_id == AL_BLESSING) {
		// Another 50 lines
	}
	// ... 20 more skills
}
```

**After - Extracted functions:**

```cpp
static int32 skill_heal(block_list *src, block_list *bl, uint16 skill_lv) {
	int32 heal = skill_lv * 10;
	heal += status_get_max_hp(bl) / 10;

	if (src->type == BL_PC) {
		map_session_data *sd = (map_session_data *)src;
		heal = heal * (100 + pc_checkskill(sd, AL_HEAL)) / 100;
	}

	return heal;
}

int32 skill_castend_nodamage_id(block_list *src, block_list *bl,
                                uint16 skill_id, uint16 skill_lv) {
	switch (skill_id) {
		case AL_HEAL: {
			int32 heal = skill_heal(src, bl, skill_lv);
			status_heal(bl, heal, 0, 0);
			clif_skill_nodamage(src, bl, skill_id, heal, 1);
			break;
		}
		case AL_BLESSING:
			skill_blessing(src, bl, skill_lv);
			break;
		// ... more skills
	}
}
```

### Replace Magic Numbers

**Before:**

```cpp
if (item_type == 4) {  // What is 4?
	// ...
}

damage = base_damage * 150 / 100;  // Why 150?
```

**After:**

```cpp
enum e_item_types {
	IT_HEALING = 0,
	IT_USABLE = 2,
	IT_ETC = 3,
	IT_WEAPON = 4,
	IT_ARMOR = 5
};

if (item_type == IT_WEAPON) {
	// ...
}

#define SKILL_DAMAGE_MULTIPLIER 150
damage = base_damage * SKILL_DAMAGE_MULTIPLIER / 100;

// Or better, from database
damage = base_damage * skill_db.find(skill_id)->damage_multiplier / 100;
```

### Simplify Conditionals

**Before:**

```cpp
if (sd != nullptr && sd->status.base_level >= 99 && sd->status.job_level >= 50
    && pc_checkskill(sd, NV_BASIC) >= 9 && sd->status.class_ == JOB_NOVICE) {
	// Can become super novice
}
```

**After:**

```cpp
bool can_become_super_novice(map_session_data *sd) {
	if (!sd)
		return false;

	if (sd->status.class_ != JOB_NOVICE)
		return false;

	if (sd->status.base_level < 99 || sd->status.job_level < 50)
		return false;

	if (pc_checkskill(sd, NV_BASIC) < 9)
		return false;

	return true;
}

if (can_become_super_novice(sd)) {
	// Can become super novice
}
```

---

## 12. Real Anti-Patterns from rAthena {#anti-patterns}

### Anti-Pattern 1: Not Checking Map Coordinates

**Problem:**

```cpp
// WRONG - No validation
int16 x = packet->x;
int16 y = packet->y;
pc_setpos(sd, sd->mapindex, x, y, CLR_TELEPORT);
```

**Why it's bad:**
- Client can send invalid coordinates (negative, outside map bounds)
- Causes crashes, exploits (walking through walls)

**Solution:**

```cpp
// CORRECT - Validate coordinates
int16 x = packet->x;
int16 y = packet->y;

if (!map_getcell(sd->bl.m, x, y, CELL_CHKPASS)) {
	ShowWarning("Invalid coordinates (%d,%d) sent by player %s\n",
	            x, y, sd->status.name);
	return;
}

if (x < 0 || x >= map[sd->bl.m].xs || y < 0 || y >= map[sd->bl.m].ys) {
	ShowWarning("Out of bounds coordinates for map %s\n",
	            map[sd->bl.m].name);
	return;
}

pc_setpos(sd, sd->mapindex, x, y, CLR_TELEPORT);
```

### Anti-Pattern 2: Trusting Client Item Counts

**Problem:**

```cpp
// WRONG - Trust client packet
void trade_additem(map_session_data *sd, int32 index, int32 amount) {
	sd->deal.item[slot].index = index;
	sd->deal.item[slot].amount = amount;  // What if amount > actual amount?
}
```

**Why it's bad:**
- Client can send amount = 999999 even if they only have 1
- Item duplication exploit

**Solution:**

```cpp
// CORRECT - Verify against server inventory
void trade_additem(map_session_data *sd, int32 index, int32 amount) {
	nullpo_retv(sd);

	if (index < 0 || index >= MAX_INVENTORY) {
		ShowWarning("Invalid inventory index %d\n", index);
		return;
	}

	// Check if player actually has the item
	if (sd->inventory.u.items_inventory[index].nameid == 0) {
		ShowWarning("Player trying to trade non-existent item at index %d\n", index);
		return;
	}

	// Verify amount
	if (amount <= 0 || amount > sd->inventory.u.items_inventory[index].amount) {
		ShowWarning("Invalid trade amount %d (has %d)\n",
		            amount, sd->inventory.u.items_inventory[index].amount);
		return;
	}

	// Additional check in impossible_trade_check() before finalizing
	sd->deal.item[slot].index = index;
	sd->deal.item[slot].amount = amount;
}
```

### Anti-Pattern 3: Forgetting Map Free Block

**Problem:**

```cpp
// WRONG - Memory leak in map system
void some_skill_function() {
	map_foreachinrange(skill_area_sub, src, range, type, src, skill_id, skill_lv);
	// Forgot to call map_freeblock_unlock()
}
```

**Why it's bad:**
- map_foreachinrange locks memory blocks
- Forgetting to unlock causes memory leaks
- Eventually server runs out of memory

**Solution:**

```cpp
// CORRECT - Always pair lock/unlock
void some_skill_function() {
	map_freeblock_lock();
	map_foreachinrange(skill_area_sub, src, range, type, src, skill_id, skill_lv);
	map_freeblock_unlock();
}

// Recent refactor removed many of these (see commit bb70dd34)
// But still important when manually using the map block system
```

### Anti-Pattern 4: Race Conditions in State Changes

**Problem:**

```cpp
// WRONG - Race condition
void skill_cast_complete() {
	if (sd->state.casting) {
		sd->state.casting = 0;
		apply_skill_effect();
	}
}

// What if player starts casting again between check and set?
```

**Why it's bad:**
- Multiple timers/packets can execute simultaneously
- Skill can execute multiple times
- Items consumed multiple times

**Solution:**

```cpp
// CORRECT - Atomic state change with validation
void skill_cast_complete(map_session_data *sd, uint16 skill_id) {
	nullpo_retv(sd);

	// Verify skill being cast matches
	if (!sd->state.casting || sd->ud.skill_id != skill_id) {
		return;  // Not casting or different skill
	}

	// Atomically clear state before executing
	sd->state.casting = 0;
	uint16 cast_skill = sd->ud.skill_id;
	sd->ud.skill_id = 0;

	// Now safe to execute
	apply_skill_effect(sd, cast_skill);
}
```

### Anti-Pattern 5: String Buffer Assumptions

**Problem:**

```cpp
// WRONG - Assumes string is null-terminated
void parse_player_name(char *packet_name) {
	char name[NAME_LENGTH];
	strcpy(name, packet_name);  // What if packet_name isn't null-terminated?
	printf("Player: %s\n", name);  // Can read past buffer!
}
```

**Why it's bad:**
- Client can send malicious packets without null terminators
- Buffer overflow, information leak
- Can crash server or expose memory

**Solution:**

```cpp
// CORRECT - Always use safe string functions
void parse_player_name(char *packet_name, int32 packet_length) {
	char name[NAME_LENGTH];

	// Safely copy with maximum length
	safestrncpy(name, packet_name, sizeof(name));

	// Or if you need exact length check
	if (packet_length >= NAME_LENGTH) {
		ShowWarning("Player name too long (%d bytes)\n", packet_length);
		return;
	}

	memcpy(name, packet_name, packet_length);
	name[packet_length] = '\0';  // Ensure null termination

	ShowInfo("Player: %s\n", name);
}
```

### Anti-Pattern 6: Not Validating Skill Prerequisites

**Problem:**

```cpp
// WRONG - No prerequisite checking
void use_combo_skill(map_session_data *sd, uint16 skill_id) {
	// What if player doesn't have the prerequisite skills learned?
	execute_skill(sd, skill_id);
}
```

**Why it's bad:**
- Client can be modified to send any skill ID
- Players can use skills they don't know
- Breaks game balance, exploits

**Solution:**

```cpp
// CORRECT - Validate prerequisites
void use_combo_skill(map_session_data *sd, uint16 skill_id) {
	nullpo_retv(sd);

	// Check if player has learned the skill
	uint16 skill_lv = pc_checkskill(sd, skill_id);
	if (skill_lv == 0) {
		ShowWarning("Player %s trying to use unlearned skill %d\n",
		            sd->status.name, skill_id);
		return;
	}

	// Check prerequisites (defined in skill_tree_db)
	if (!pc_check_skillup(sd, skill_id)) {
		ShowWarning("Player %s doesn't meet prerequisites for skill %d\n",
		            sd->status.name, skill_id);
		return;
	}

	// Check SP, items, weapon, state requirements
	if (!skill_check_condition(sd, skill_id, skill_lv)) {
		return;
	}

	execute_skill(sd, skill_id, skill_lv);
}
```

---

## Summary: Golden Rules

### The Seven Commandments of rAthena Development

1. **ALWAYS check pointers for NULL** - Use nullpo_ret/retv/retr
2. **NEVER trust client input** - Validate everything
3. **Use aMalloc/aFree** - NOT malloc/free
4. **Check array bounds** - Use cap_value, validate indices
5. **Handle errors properly** - ShowError, ShowWarning, return codes
6. **Comment the WHY, not the WHAT** - Explain intent and context
7. **Test in DEBUG builds first** - Catch errors early

### Quick Reference Table

| Task | WRONG | CORRECT |
|------|-------|---------|
| Null check | `if (sd->bl.id)` | `if (!sd) return; if (sd->bl.id)` |
| Memory alloc | `malloc(size)` | `aMalloc(size)` |
| String copy | `strcpy(dst, src)` | `safestrncpy(dst, src, sizeof(dst))` |
| Format string | `sprintf(buf, fmt, ...)` | `safesnprintf(buf, sizeof(buf), fmt, ...)` |
| Skill level index | `arr[skill_lv]` | `arr[skill_lv - 1]` |
| Bounds check | `if (idx < MAX)` | `if (idx >= 0 && idx < MAX)` |
| Loop iteration | `i <= MAX_INVENTORY` | `i < MAX_INVENTORY` |
| Integer overflow | `a + b` | `safe_addition(a, b, result)` |
| Error message | `ShowError("error")` | `ShowError("func: error in %s\n", context)` |
| Git commit | `"fix stuff"` | `"Fix skill cooldown reset on death"` |

---

## Additional Resources

- **KB_REF_CompilationDebugging.md** - GDB debugging, build flags
- **KB_REF_SecurityExploits.md** - Security vulnerabilities and prevention
- **KB_REF_MemoryCrashPatterns.md** - Common crash causes
- **KB_REF_SourceCodeStructure.md** - File organization and architecture

---

**Last Updated:** 2024-01-15
**Maintainer:** rAthena Development Team
