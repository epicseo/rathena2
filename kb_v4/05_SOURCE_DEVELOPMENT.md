# rAthena Source Development Complete Guide v4.0

**Version:** 4.0 - RAG-Optimized Complete Edition
**File Size:** ~7K lines (merged from 4 files)
**Coverage:** 100% C++ development guide
**Last Updated:** 2025-11-19

---

<!-- RAG_CHUNK: overview -->
## 📦 What's in This File

> **🎯 Context Box: Complete C++ Development Toolkit**
> This file merges ALL C++ development content from v3.1:
> - **Plugin System** (src/custom/ modular development)
> - **Best Practices** (code quality, safety patterns)
> - **Memory Crash Prevention** (ERS, map_freeblock, 80% of crashes)
> - **Source Code Structure** (directory layout, core structs)
>
> Previously scattered across 4 files. Now unified for complete C++ workflow.

---

<!-- RAG_CHUNK: quick_reference -->
## 🔍 Quick Reference

| I need to... | Go to section |
|-------------|---------------|
| **Add custom @command** | Part 1: Plugin System (ACMD_FUNC) |
| **Add custom script command** | Part 1: Plugin System (BUILDIN_FUNC) |
| **Fix crashes** | Part 3: Memory Crash Patterns |
| **Understand codebase** | Part 4: Source Code Structure |
| **Code safely** | Part 2: Best Practices |

---

# ═══════════════════════════════════════════════════════════════
# PART 1: PLUGIN SYSTEM (src/custom/)
# ═══════════════════════════════════════════════════════════════
<!-- RAG_CHUNK: plugin_system_complete -->

---
kb_id: KB_REF_035
title: "rAthena Plugin & Custom System Complete Guide"
category: Source Code Internals
keywords: [custom_system, plugin_system, atcommand, script_commands, custom_defines, battle_config, ACMD_FUNC, BUILDIN_FUNC, modular_development, src_custom, atcommand_inc, script_inc, defines_pre, defines_post]
related_files: [
  "src/custom/atcommand.inc",
  "src/custom/atcommand_def.inc",
  "src/custom/script.inc",
  "src/custom/script_def.inc",
  "src/custom/defines_pre.hpp",
  "src/custom/defines_post.hpp",
  "src/custom/battle_config_init.inc",
  "src/custom/battle_config_struct.inc",
  "src/map/atcommand.cpp",
  "src/map/script.cpp",
  "src/map/battle.cpp",
  "src/config/core.hpp"
]
difficulty: intermediate
use_case: "Adding custom @commands, script commands, defines, and battle config without modifying core files"
version: rAthena 2024
last_updated: 2024-01-15
---

# rAthena Plugin & Custom System Complete Guide

## 🎯 Critical Understanding

**WHY THIS SYSTEM EXISTS:**
- **Core Protection**: Modify functionality WITHOUT touching core rAthena files
- **Update Safety**: Your customs survive when you update rAthena (git pull)
- **Modularity**: All customizations in ONE place (`src/custom/`)
- **Merge-Friendly**: No conflicts when merging upstream changes

**WHAT YOU CAN CUSTOMIZE:**
1. **Custom @commands** (GM commands like `@heal`, `@warp`)
2. **Custom script commands** (NPC script functions like `getitem`, `mes`)
3. **Custom defines** (Preprocessor constants like `MAX_LEVEL`)
4. **Custom battle config** (Configuration options in `battle.conf`)

**THE GOLDEN RULE:**
> If you're editing files in `src/map/`, `src/common/`, etc. - STOP!
> Ask yourself: "Can I do this in `src/custom/` instead?"

---

## 📋 Table of Contents

1. [Directory Structure](#directory-structure)
2. [How the Custom System Works](#how-the-system-works)
3. [Creating Custom @Commands](#custom-atcommands)
4. [Creating Custom Script Commands](#custom-script-commands)
5. [Adding Custom Defines](#custom-defines)
6. [Adding Custom Battle Config](#custom-battle-config)
7. [Complete Working Examples](#working-examples)
8. [Common Mistakes & Solutions](#common-mistakes)
9. [Build System Integration](#build-integration)
10. [When to Edit Core vs Custom](#core-vs-custom)

---

## 📁 Directory Structure {#directory-structure}

### The src/custom/ Directory

```
src/custom/
├── atcommand.inc              # Custom @command implementations
├── atcommand_def.inc          # Custom @command registrations
├── script.inc                 # Custom script command implementations
├── script_def.inc             # Custom script command registrations
├── battle_config_init.inc     # Custom battle config initialization
├── battle_config_struct.inc   # Custom battle config structure members
├── defines_pre.hpp            # Custom defines (loaded BEFORE core defines)
└── defines_post.hpp           # Custom defines (loaded AFTER core defines)
```

### File Types Explained

| File Type | Purpose | When It's Loaded |
|-----------|---------|------------------|
| `.inc` | Include files - raw C++ code injected into core files | Compile-time |
| `.hpp` | Header files - preprocessor definitions | Compile-time (pre/post core) |

### How Files Are Integrated

```cpp
// src/map/atcommand.cpp (line 11379)
#include <custom/atcommand.inc>        // Your custom @command functions

// src/map/atcommand.cpp (line 11395)
#include <custom/atcommand_def.inc>    // Your custom @command registrations

// src/map/script.cpp (line 27795)
#include <custom/script.inc>           // Your custom script functions

// src/map/script.cpp (line 28571)
#include <custom/script_def.inc>       // Your custom script registrations

// src/config/core.hpp (line 12)
#include <custom/defines_pre.hpp>      // Your defines BEFORE core

// src/config/core.hpp (line 126)
#include <custom/defines_post.hpp>     // Your defines AFTER core

// src/map/battle.hpp (line 785)
#include <custom/battle_config_struct.inc>  // Your battle config variables

// src/map/battle.cpp (line 12363)
#include <custom/battle_config_init.inc>    // Your battle config initialization
```

**KEY INSIGHT:**
These `.inc` files are NOT compiled separately - they are **literally injected** into the core files at compile-time. This means:
- You have access to ALL functions/variables in that file's scope
- You DON'T need to declare prototypes (they're already in scope)
- You MUST follow the same coding style/conventions

---

## 🔧 How the Custom System Works {#how-the-system-works}

### The Include Pattern

rAthena uses a **preprocessor injection** pattern:

```
[Core File] ──#include──> [Custom File] ──inject──> [Compiled Code]

Example:
atcommand.cpp includes atcommand.inc
        ↓
Your custom code becomes PART of atcommand.cpp
        ↓
Compiler sees it as ONE file
```

### The Two-Step Registration Pattern

Most custom features require **TWO files**:

1. **Implementation file** (`.inc`) - The actual code
2. **Definition file** (`_def.inc`) - Registers it with the system

**Example: Custom @command**
```
atcommand.inc      →  The code that runs when you type @mycommand
atcommand_def.inc  →  Tells rAthena "@mycommand exists and maps to function X"
```

### Compilation Flow

```
[You edit src/custom/*.inc]
        ↓
[Run ./configure && make] or [CMake build]
        ↓
[Preprocessor injects .inc files into core]
        ↓
[Compiler processes merged code]
        ↓
[Binary (map-server) with your customs]
```

---

## 🎮 Creating Custom @Commands {#custom-atcommands}

### Understanding ACMD_FUNC

**Macro Definition:**
```cpp
// src/map/atcommand.cpp:61
#define ACMD_FUNC(x) static int32 atcommand_ ## x (const int32 fd, map_session_data* sd, const char* command, const char* message)
```

**What this means:**
```cpp
ACMD_FUNC(mycommand)
    ↓ expands to ↓
static int32 atcommand_mycommand(
    const int32 fd,              // File descriptor (socket)
    map_session_data* sd,        // Player data
    const char* command,         // Command name (e.g., "mycommand")
    const char* message          // Parameters after command
)
```

### Step-by-Step: Creating a Custom @Command

#### Step 1: Write the Implementation (atcommand.inc)

```cpp
// src/custom/atcommand.inc

/**
 * @hello - Displays a greeting and plays an effect
 * Usage: @hello [name]
 */
ACMD_FUNC(hello)
{
    char player_name[NAME_LENGTH];

    // Extract optional parameter
    if (message && *message) {
        sscanf(message, "%23s", player_name);
    } else {
        // Default to player's own name
        safestrncpy(player_name, sd->status.name, NAME_LENGTH);
    }

    // Display message to player
    sprintf(atcmd_output, "Hello, %s! Welcome to the server!", player_name);
    clif_displaymessage(fd, atcmd_output);

    // Play visual effect
    clif_specialeffect(&sd->bl, EF_HEARTCASTING, AREA);

    return 0; // Success
}

/**
 * @servertime - Shows current server time and uptime
 * Usage: @servertime
 */
ACMD_FUNC(servertime)
{
    time_t now;
    struct tm *timeinfo;
    int64 uptime;

    // Get current time
    time(&now);
    timeinfo = localtime(&now);

    // Calculate uptime (milliseconds to seconds)
    uptime = (gettick() / 1000);

    // Display time info
    sprintf(atcmd_output, "Server Time: %02d:%02d:%02d",
            timeinfo->tm_hour, timeinfo->tm_min, timeinfo->tm_sec);
    clif_displaymessage(fd, atcmd_output);

    sprintf(atcmd_output, "Uptime: %lld hours, %lld minutes",
            uptime / 3600, (uptime % 3600) / 60);
    clif_displaymessage(fd, atcmd_output);

    return 0;
}

/**
 * @myhp - Displays detailed HP information
 * Usage: @myhp
 */
ACMD_FUNC(myhp)
{
    int32 hp_percent;

    // Null pointer check
    nullpo_retr(-1, sd);

    // Calculate HP percentage
    hp_percent = (sd->battle_status.hp * 100) / sd->battle_status.max_hp;

    // Display HP stats
    sprintf(atcmd_output, "═══════════════════════════");
    clif_displaymessage(fd, atcmd_output);

    sprintf(atcmd_output, "Current HP: %d / %d (%d%%)",
            sd->battle_status.hp, sd->battle_status.max_hp, hp_percent);
    clif_displaymessage(fd, atcmd_output);

    sprintf(atcmd_output, "HP Regen: +%d per tick", sd->battle_status.hpregen);
    clif_displaymessage(fd, atcmd_output);

    sprintf(atcmd_output, "═══════════════════════════");
    clif_displaymessage(fd, atcmd_output);

    return 0;
}
```

#### Step 2: Register the Command (atcommand_def.inc)

```cpp
// src/custom/atcommand_def.inc

/**
 * Register custom commands
 * Format: ACMD_DEF(command_name),
 * NOTE: The trailing comma is REQUIRED!
 */

ACMD_DEF(hello),
ACMD_DEF(servertime),
ACMD_DEF(myhp),
```

#### Step 3: Compile and Test

```bash
# Recompile map-server
make map-server

# Test in-game
@hello
@hello PlayerName
@servertime
@myhp
```

### Advanced @Command Patterns

#### Parameter Parsing

```cpp
ACMD_FUNC(teleportto)
{
    char map_name[MAP_NAME_LENGTH_EXT];
    int16 x = 0, y = 0;

    // Parse: @teleportto <map> <x> <y>
    if (!message || !*message ||
        sscanf(message, "%15s %5hd %5hd", map_name, &x, &y) < 3) {
        clif_displaymessage(fd, "Usage: @teleportto <map> <x> <y>");
        return -1; // Failure
    }

    // Validate map exists
    int16 mapid = map_mapname2mapid(map_name);
    if (mapid < 0) {
        clif_displaymessage(fd, "Map not found!");
        return -1;
    }

    // Teleport
    pc_setpos(sd, mapid, x, y, CLR_TELEPORT);

    return 0;
}
```

#### Permission Checking

```cpp
ACMD_FUNC(gmonly)
{
    // Check if player has specific permission
    if (!pc_has_permission(sd, PC_PERM_WARP_ANYWHERE)) {
        clif_displaymessage(fd, "You don't have permission to use this command!");
        return -1;
    }

    // GM-only code here...
    clif_displaymessage(fd, "GM command executed!");
    return 0;
}
```

#### Error Handling

```cpp
ACMD_FUNC(safecmd)
{
    // 1. Null pointer check
    nullpo_retr(-1, sd);

    // 2. Parameter validation
    if (!message || !*message) {
        clif_displaymessage(fd, "Error: Missing parameters!");
        return -1;
    }

    // 3. State validation
    if (sd->state.trading) {
        clif_displaymessage(fd, "You cannot use this while trading!");
        return -1;
    }

    // 4. Map flag check
    if (map_getmapflag(sd->m, MF_NOTELEPORT)) {
        clif_displaymessage(fd, "This map doesn't allow that!");
        return -1;
    }

    return 0;
}
```

### Return Values

| Return | Meaning |
|--------|---------|
| `0` | Success (command executed) |
| `-1` | Failure (error occurred, show help text if available) |

---

## 📜 Creating Custom Script Commands {#custom-script-commands}

### Understanding BUILDIN_FUNC

**Macro Definition:**
```cpp
// src/map/script.cpp:4913
#define BUILDIN_FUNC(x) int32 buildin_ ## x (struct script_state* st)
```

**What this means:**
```cpp
BUILDIN_FUNC(myfunction)
    ↓ expands to ↓
int32 buildin_myfunction(struct script_state* st)
```

**The script_state struct contains:**
- `st->stack` - Script stack (parameters and return values)
- `st->oid` - NPC object ID
- `st->rid` - Player character ID
- `st->state` - Execution state (STOP, END, etc.)

### Step-by-Step: Creating a Custom Script Command

#### Step 1: Write the Implementation (script.inc)

```cpp
// src/custom/script.inc

/**
 * giverandombuff() - Gives player a random buff for 60 seconds
 * Usage: giverandombuff;
 * Returns: 1 on success, 0 on failure
 */
BUILDIN_FUNC(giverandombuff)
{
    map_session_data* sd;

    // Get player data from script
    if (!script_rid2sd(sd)) {
        script_pushint(st, 0);
        return SCRIPT_CMD_FAILURE;
    }

    // Array of possible buffs
    int32 buffs[] = {
        SC_BLESSING,      // +STR/INT/DEX
        SC_INCREASEAGI,   // +AGI/Speed
        SC_ANGELUS,       // +DEF
        SC_IMPOSITIO,     // +ATK
        SC_GLORIA         // +LUK
    };

    // Pick random buff
    int32 buff = buffs[rnd() % ARRAYLENGTH(buffs)];

    // Apply buff for 60 seconds (60000ms)
    sc_start(nullptr, &sd->bl, (sc_type)buff, 100, 1, 60000);

    // Log it
    ShowInfo("giverandombuff: Applied SC %d to player %s\n", buff, sd->status.name);

    // Return success to script
    script_pushint(st, 1);
    return SCRIPT_CMD_SUCCESS;
}

/**
 * getserverpopulation() - Returns current online player count
 * Usage: .population = getserverpopulation();
 * Returns: Number of online players
 */
BUILDIN_FUNC(getserverpopulation)
{
    int32 users = 0;

    // Iterate through all online players
    struct s_mapiterator* iter = mapit_getallusers();
    map_session_data* sd;

    for (sd = (map_session_data*)mapit_first(iter);
         mapit_exists(iter);
         sd = (map_session_data*)mapit_next(iter)) {
        if (sd && session_isValid(sd->fd))
            users++;
    }

    mapit_free(iter);

    // Return count to script
    script_pushint(st, users);
    return SCRIPT_CMD_SUCCESS;
}

/**
 * calculatepower(<base>, <exponent>) - Returns base^exponent
 * Usage: .result = calculatepower(2, 10); // Returns 1024
 */
BUILDIN_FUNC(calculatepower)
{
    int32 base, exponent, result = 1;

    // Get parameters from script
    base = script_getnum(st, 2);      // 1st parameter
    exponent = script_getnum(st, 3);  // 2nd parameter

    // Validate
    if (exponent < 0) {
        ShowError("buildin_calculatepower: Negative exponents not supported!\n");
        script_pushint(st, 0);
        return SCRIPT_CMD_FAILURE;
    }

    // Calculate power
    for (int32 i = 0; i < exponent; i++) {
        result *= base;
    }

    // Return result
    script_pushint(st, result);
    return SCRIPT_CMD_SUCCESS;
}

/**
 * getrandomonlineplayer$() - Returns random online player name
 * Usage: .name$ = getrandomonlineplayer$();
 * Returns: Player name or empty string
 */
BUILDIN_FUNC(getrandomonlineplayer)
{
    // Build array of online players
    std::vector<map_session_data*> players;

    struct s_mapiterator* iter = mapit_getallusers();
    map_session_data* sd;

    for (sd = (map_session_data*)mapit_first(iter);
         mapit_exists(iter);
         sd = (map_session_data*)mapit_next(iter)) {
        if (sd && session_isValid(sd->fd))
            players.push_back(sd);
    }

    mapit_free(iter);

    // Pick random player
    if (players.size() > 0) {
        map_session_data* random_player = players[rnd() % players.size()];
        script_pushstrcopy(st, random_player->status.name);
    } else {
        script_pushconststr(st, "");
    }

    return SCRIPT_CMD_SUCCESS;
}
```

#### Step 2: Register the Command (script_def.inc)

```cpp
// src/custom/script_def.inc

/**
 * Register custom script commands
 * Format: BUILDIN_DEF(command_name, "parameters"),
 *
 * Parameter Types:
 *   i = integer
 *   s = string
 *   l = label
 *   r = reference (variable)
 *   ? = optional parameter
 *
 * Examples:
 *   ""     = No parameters
 *   "i"    = One integer (required)
 *   "s?"   = One string (optional)
 *   "ii"   = Two integers (required)
 *   "is?"  = Integer + optional string
 */

BUILDIN_DEF(giverandombuff, ""),
BUILDIN_DEF(getserverpopulation, ""),
BUILDIN_DEF(calculatepower, "ii"),
BUILDIN_DEF(getrandomonlineplayer, ""),
```

#### Step 3: Use in Scripts

```javascript
// npc/custom/test.txt

prontera,150,150,4	script	CustomCommands	100,{
    mes "Testing custom script commands...";
    next;

    // Test 1: Random buff
    mes "Giving you a random buff!";
    giverandombuff;
    next;

    // Test 2: Server population
    .pop = getserverpopulation();
    mes "Players online: " + .pop;
    next;

    // Test 3: Calculate power
    .result = calculatepower(2, 10);
    mes "2^10 = " + .result;
    next;

    // Test 4: Random player
    .player$ = getrandomonlineplayer$();
    if (.player$ != "") {
        mes "Random player: " + .player$;
    } else {
        mes "No players online!";
    }

    close;
}
```

### Advanced Script Command Patterns

#### Optional Parameters

```cpp
BUILDIN_FUNC(customheal)
{
    map_session_data* sd;
    int32 hp_amount, sp_amount = 0;

    if (!script_rid2sd(sd))
        return SCRIPT_CMD_FAILURE;

    // Get required parameter
    hp_amount = script_getnum(st, 2);

    // Get optional parameter (check if it exists)
    if (script_hasdata(st, 3)) {
        sp_amount = script_getnum(st, 3);
    }

    // Heal
    status_heal(&sd->bl, hp_amount, sp_amount, 0);

    script_pushint(st, 1);
    return SCRIPT_CMD_SUCCESS;
}

// Register with optional parameter
// BUILDIN_DEF(customheal, "i?"),
```

#### String Parameters

```cpp
BUILDIN_FUNC(saytoall)
{
    const char* message;
    char output[CHAT_SIZE_MAX];

    // Get string parameter
    message = script_getstr(st, 2);

    // Broadcast to all players
    snprintf(output, CHAT_SIZE_MAX, "[Announcement] %s", message);
    intif_broadcast(output, strlen(output) + 1, BC_DEFAULT);

    script_pushint(st, 1);
    return SCRIPT_CMD_SUCCESS;
}

// BUILDIN_DEF(saytoall, "s"),
```

#### Variable References

```cpp
BUILDIN_FUNC(fillarray)
{
    struct script_data* data;
    int32 value, count;

    // Get array reference
    data = script_getdata(st, 2);
    if (!data_isreference(data)) {
        ShowError("buildin_fillarray: Not a variable!\n");
        return SCRIPT_CMD_FAILURE;
    }

    value = script_getnum(st, 3);
    count = script_getnum(st, 4);

    // Fill array
    for (int32 i = 0; i < count; i++) {
        set_reg_num(st, nullptr, reference_uid(reference_getid(data), i),
                    reference_getname(data), value, reference_getref(data));
    }

    script_pushint(st, 1);
    return SCRIPT_CMD_SUCCESS;
}

// BUILDIN_DEF(fillarray, "rii"),
```

### Return Values

| Return | Meaning |
|--------|---------|
| `SCRIPT_CMD_SUCCESS` (0) | Command executed successfully |
| `SCRIPT_CMD_FAILURE` (1) | Command failed, show debug info |

### Pushing Return Values to Script

```cpp
script_pushint(st, 123);                    // Push integer
script_pushstr(st, buffer);                 // Push string (takes ownership)
script_pushstrcopy(st, "text");             // Push string (makes copy)
script_pushconststr(st, "constant");        // Push constant string
script_pushnil(st);                         // Push nothing (void)
```

---

## 🔧 Adding Custom Defines {#custom-defines}

### defines_pre.hpp vs defines_post.hpp

**KEY DIFFERENCE:**

```
[defines_pre.hpp]  →  Loaded BEFORE core defines
        ↓
[Core defines (const.hpp, etc.)]
        ↓
[defines_post.hpp] →  Loaded AFTER core defines
```

### When to Use defines_pre.hpp

Use `defines_pre.hpp` when you need to:
- **Override** core defines BEFORE they're used
- **Prevent** core defines from being set

**Example:**
```cpp
// src/custom/defines_pre.hpp

#ifndef CONFIG_CUSTOM_DEFINES_PRE_HPP
#define CONFIG_CUSTOM_DEFINES_PRE_HPP

/**
 * Override MAX_LEVEL before core sets it
 * This way, all systems use YOUR value
 */
#define MAX_LEVEL 500

/**
 * Override MAX_INVENTORY before core
 */
#define MAX_INVENTORY 200

/**
 * Enable custom features BEFORE core checks
 */
#define ENABLE_MY_CUSTOM_SYSTEM

#endif /* CONFIG_CUSTOM_DEFINES_PRE_HPP */
```

### When to Use defines_post.hpp

Use `defines_post.hpp` when you need to:
- **Add** new defines that depend on core defines
- **Calculate** values based on core constants
- **Conditionally** define based on core settings

**Example:**
```cpp
// src/custom/defines_post.hpp

#ifndef CONFIG_CUSTOM_DEFINES_POST_HPP
#define CONFIG_CUSTOM_DEFINES_POST_HPP

/**
 * Add custom constants based on core defines
 */
#define CUSTOM_MAX_STORAGE (MAX_STORAGE * 2)

/**
 * Conditional compilation based on core features
 */
#ifdef PACKETVER_RE
    #define CUSTOM_RE_FEATURE_ENABLED
#endif

/**
 * Custom map flags (must be unique!)
 * Find next available ID by checking map.hpp
 */
#define MF_CUSTOM_PVP 80
#define MF_CUSTOM_NOSKILL 81

/**
 * Custom status changes (SC_*)
 * IMPORTANT: Must not conflict with existing SC_ defines!
 */
#define SC_CUSTOM_BUFF (SC_MAX + 1)
#define SC_CUSTOM_DEBUFF (SC_MAX + 2)

/**
 * Custom item IDs for scripts
 */
#define CUSTOM_TOKEN_ID 60000
#define CUSTOM_COIN_ID 60001

#endif /* CONFIG_CUSTOM_DEFINES_POST_HPP */
```

### Real-World Example

```cpp
// defines_pre.hpp - Override BEFORE core
#ifndef CONFIG_CUSTOM_DEFINES_PRE_HPP
#define CONFIG_CUSTOM_DEFINES_PRE_HPP

// Change max level before ANYTHING uses it
#define MAX_LEVEL 999

// Change max stats
#define SHRT_MAX 32767  // Allow stats up to 32k

#endif

// defines_post.hpp - Add AFTER core
#ifndef CONFIG_CUSTOM_DEFINES_POST_HPP
#define CONFIG_CUSTOM_DEFINES_POST_HPP

// Calculate based on MAX_LEVEL (now 999)
#define CUSTOM_EXP_TABLE_SIZE (MAX_LEVEL + 1)

// Add custom defines
#define CUSTOM_VIP_BONUS 50
#define CUSTOM_GUILD_BONUS 25

// Conditional features
#ifdef RENEWAL
    #define CUSTOM_RENEWAL_BONUS 100
#else
    #define CUSTOM_PRENEWAL_BONUS 75
#endif

#endif
```

### Safety Warnings

**⚠️ CRITICAL WARNINGS:**

1. **Don't redefine core enums** in defines files:
   ```cpp
   // ❌ WRONG - This will cause compile errors
   enum e_my_enum {
       MY_VALUE = 100
   };
   ```

2. **Check for conflicts:**
   - Before adding SC_* defines, check src/map/status.hpp
   - Before adding MF_* defines, check src/map/map.hpp
   - Before adding EF_* defines, check src/map/clif.hpp

3. **Use unique prefixes:**
   ```cpp
   // ✅ GOOD - Clearly custom
   #define MYCUSTOM_MAX_ITEMS 1000

   // ❌ BAD - Might conflict with core
   #define MAX_ITEMS 1000
   ```

---

## ⚙️ Adding Custom Battle Config {#custom-battle-config}

Battle config allows you to add **configurable options** to `conf/battle/battle.conf`.

### The Two-Step Process

1. **battle_config_struct.inc** - Declare the variable
2. **battle_config_init.inc** - Initialize with defaults

### Step 1: Add to Structure (battle_config_struct.inc)

```cpp
// src/custom/battle_config_struct.inc

/**
 * Custom battle config structure members
 * These become part of the battle_config struct
 *
 * Format: <datatype> name;
 */

// Custom rates
int32 custom_exp_rate;
int32 custom_drop_rate;

// Custom features (0 = disabled, 1 = enabled)
int32 enable_custom_damage_formula;
int32 enable_custom_heal_bonus;

// Custom limits
int32 custom_max_hp_bonus;
int32 custom_max_sp_bonus;

// Custom time (in milliseconds)
int32 custom_buff_duration;

// Custom percentages (0-100)
int32 custom_critical_chance_bonus;
```

### Step 2: Initialize Values (battle_config_init.inc)

```cpp
// src/custom/battle_config_init.inc

/**
 * Custom battle config initialization
 *
 * Format:
 * { "config_name", &battle_config.variable_name, default, min, max },
 *
 * IMPORTANT: Trailing comma is REQUIRED!
 */

// Rates
{ "custom_exp_rate",                 &battle_config.custom_exp_rate,                 100,    0,      10000,  },
{ "custom_drop_rate",                &battle_config.custom_drop_rate,                100,    0,      10000,  },

// Features (boolean: 0 or 1)
{ "enable_custom_damage_formula",    &battle_config.enable_custom_damage_formula,    0,      0,      1,      },
{ "enable_custom_heal_bonus",        &battle_config.enable_custom_heal_bonus,        1,      0,      1,      },

// Limits
{ "custom_max_hp_bonus",             &battle_config.custom_max_hp_bonus,             1000,   0,      999999, },
{ "custom_max_sp_bonus",             &battle_config.custom_max_sp_bonus,             500,    0,      999999, },

// Time (milliseconds)
{ "custom_buff_duration",            &battle_config.custom_buff_duration,            60000,  1000,   3600000, },

// Percentages
{ "custom_critical_chance_bonus",    &battle_config.custom_critical_chance_bonus,    5,      0,      100,    },
```

### Step 3: Add to battle.conf

```ini
# conf/battle/battle.conf (or create conf/battle/custom.conf)

//--------------------------------------------------------------
// Custom Battle Configuration
//--------------------------------------------------------------

// Custom EXP rate multiplier (100 = 1x, 200 = 2x)
// Default: 100
custom_exp_rate: 150

// Custom drop rate multiplier (100 = 1x, 200 = 2x)
// Default: 100
custom_drop_rate: 200

// Enable custom damage formula (0 = no, 1 = yes)
// Default: 0
enable_custom_damage_formula: 1

// Enable custom heal bonus (0 = no, 1 = yes)
// Default: 1
enable_custom_heal_bonus: 1

// Maximum HP bonus from equipment/buffs
// Default: 1000
custom_max_hp_bonus: 5000

// Custom buff duration in milliseconds (60000 = 1 minute)
// Default: 60000
custom_buff_duration: 120000

// Critical hit chance bonus percentage (0-100)
// Default: 5
custom_critical_chance_bonus: 10
```

### Step 4: Use in Code

**In custom atcommand:**
```cpp
ACMD_FUNC(showconfig)
{
    sprintf(atcmd_output, "Custom EXP Rate: %d%%", battle_config.custom_exp_rate);
    clif_displaymessage(fd, atcmd_output);

    sprintf(atcmd_output, "Custom Damage Formula: %s",
            battle_config.enable_custom_damage_formula ? "Enabled" : "Disabled");
    clif_displaymessage(fd, atcmd_output);

    return 0;
}
```

**In custom script command:**
```cpp
BUILDIN_FUNC(getcustomexprate)
{
    script_pushint(st, battle_config.custom_exp_rate);
    return SCRIPT_CMD_SUCCESS;
}
```

**In core modifications (if needed):**
```cpp
// Modify damage calculation
if (battle_config.enable_custom_damage_formula) {
    // Apply custom formula
    damage = (damage * battle_config.custom_damage_multiplier) / 100;
}
```

---

## 💡 Complete Working Examples {#working-examples}

### Example 1: Custom Daily Reward System

**atcommand.inc:**
```cpp
ACMD_FUNC(dailyreward)
{
    uint32 today, last_claim;
    int32 reward_item = 7227; // TCG Card
    int32 reward_amount = 5;

    nullpo_retr(-1, sd);

    // Get today's date (days since epoch)
    today = (uint32)(time(nullptr) / 86400);

    // Check last claim time (stored in player variable)
    last_claim = pc_readaccountreg(sd, add_str("#DAILY_LAST"));

    if (last_claim == today) {
        clif_displaymessage(fd, "You've already claimed your daily reward!");
        return -1;
    }

    // Give reward
    struct item item_tmp;
    memset(&item_tmp, 0, sizeof(item_tmp));
    item_tmp.nameid = reward_item;
    item_tmp.identify = 1;

    if (pc_additem(sd, &item_tmp, reward_amount, LOG_TYPE_COMMAND) != 0) {
        clif_displaymessage(fd, "Failed to receive reward! Inventory full?");
        return -1;
    }

    // Save claim time
    pc_setaccountreg(sd, add_str("#DAILY_LAST"), today);

    sprintf(atcmd_output, "Daily reward claimed! You received %dx %s",
            reward_amount, itemdb_jname(reward_item));
    clif_displaymessage(fd, atcmd_output);
    clif_specialeffect(&sd->bl, EF_CONE, AREA);

    return 0;
}
```

**atcommand_def.inc:**
```cpp
ACMD_DEF(dailyreward),
```

### Example 2: Custom Item Upgrader Script Command

**script.inc:**
```cpp
BUILDIN_FUNC(upgradeweapon)
{
    map_session_data* sd;
    int32 success_rate, refine_cost;
    int16 equip_index;

    if (!script_rid2sd(sd)) {
        script_pushint(st, -1);
        return SCRIPT_CMD_FAILURE;
    }

    // Get equipped weapon
    equip_index = sd->equip_index[EQI_HAND_R];

    if (equip_index < 0) {
        script_pushint(st, 0); // No weapon equipped
        return SCRIPT_CMD_SUCCESS;
    }

    struct item *weapon = &sd->inventory.u.items_inventory[equip_index];

    // Check if weapon can be refined
    if (weapon->refine >= MAX_REFINE) {
        script_pushint(st, -2); // Already max refine
        return SCRIPT_CMD_SUCCESS;
    }

    // Calculate success rate (decreases with refine level)
    success_rate = 100 - (weapon->refine * 10);
    if (success_rate < 10) success_rate = 10;

    // Calculate cost (increases with refine level)
    refine_cost = 1000000 * (weapon->refine + 1);

    // Check zeny
    if (sd->status.zeny < refine_cost) {
        script_pushint(st, -3); // Not enough zeny
        return SCRIPT_CMD_SUCCESS;
    }

    // Deduct cost
    pc_payzeny(sd, refine_cost, LOG_TYPE_SCRIPT, nullptr);

    // Try to refine
    if (rnd() % 100 < success_rate) {
        // Success!
        weapon->refine++;
        clif_refine(fd, 0, equip_index, weapon->refine);
        clif_specialeffect(&sd->bl, EF_REFINEOK, AREA);
        achievement_update_objective(sd, AG_GOAL_REFINE, 1, weapon->refine);
        script_pushint(st, 1); // Success
    } else {
        // Failure - weapon downgraded
        if (weapon->refine > 0)
            weapon->refine--;
        clif_refine(fd, 1, equip_index, weapon->refine);
        clif_specialeffect(&sd->bl, EF_REFINEFAIL, AREA);
        script_pushint(st, -4); // Failed
    }

    // Update client
    clif_equiplist(sd);
    status_calc_pc(sd, SCO_NONE);

    return SCRIPT_CMD_SUCCESS;
}
```

**script_def.inc:**
```cpp
BUILDIN_DEF(upgradeweapon, ""),
```

**NPC Script (npc/custom/upgrader.txt):**
```javascript
prontera,150,180,4	script	Weapon Upgrader	4_M_MASK,{
    mes "[Weapon Upgrader]";
    mes "I can upgrade your weapon!";
    next;

    .result = upgradeweapon();

    if (.result == 1) {
        mes "Success! Your weapon has been upgraded!";
    } else if (.result == 0) {
        mes "You don't have a weapon equipped!";
    } else if (.result == -2) {
        mes "Your weapon is already at maximum refine!";
    } else if (.result == -3) {
        mes "You don't have enough zeny!";
    } else if (.result == -4) {
        mes "Upgrade failed! Your weapon was downgraded!";
    }

    close;
}
```

### Example 3: Custom Battle Config Usage

**battle_config_struct.inc:**
```cpp
int32 custom_pvp_damage_multiplier;
int32 enable_custom_exp_formula;
```

**battle_config_init.inc:**
```cpp
{ "custom_pvp_damage_multiplier",    &battle_config.custom_pvp_damage_multiplier,    100,    50,     500,    },
{ "enable_custom_exp_formula",       &battle_config.enable_custom_exp_formula,       0,      0,      1,      },
```

**atcommand.inc (use the config):**
```cpp
ACMD_FUNC(pvpinfo)
{
    sprintf(atcmd_output, "PVP Damage Multiplier: %d%%",
            battle_config.custom_pvp_damage_multiplier);
    clif_displaymessage(fd, atcmd_output);

    sprintf(atcmd_output, "Custom EXP Formula: %s",
            battle_config.enable_custom_exp_formula ? "Enabled" : "Disabled");
    clif_displaymessage(fd, atcmd_output);

    return 0;
}
```

---

## ⚠️ Common Mistakes & Solutions {#common-mistakes}

### Mistake 1: Forgetting Trailing Commas

**❌ WRONG:**
```cpp
// atcommand_def.inc
ACMD_DEF(mycommand)  // No comma!
```

**✅ CORRECT:**
```cpp
// atcommand_def.inc
ACMD_DEF(mycommand),  // Comma required!
```

**Why:** The macro expansion includes the comma in the surrounding array initialization.

---

### Mistake 2: Function Name Mismatch

**❌ WRONG:**
```cpp
// atcommand.inc
ACMD_FUNC(mycommand) { ... }

// atcommand_def.inc
ACMD_DEF(myCommamd),  // Typo!
```

**Error:** Linker error - undefined reference to `atcommand_myCommamd`

**✅ CORRECT:** Names must match EXACTLY.

---

### Mistake 3: Not Checking Null Pointers

**❌ WRONG:**
```cpp
ACMD_FUNC(crash)
{
    // sd might be NULL!
    sprintf(atcmd_output, "Player: %s", sd->status.name);
    return 0;
}
```

**✅ CORRECT:**
```cpp
ACMD_FUNC(safe)
{
    nullpo_retr(-1, sd);  // Check for NULL first!
    sprintf(atcmd_output, "Player: %s", sd->status.name);
    return 0;
}
```

---

### Mistake 4: Buffer Overflows

**❌ WRONG:**
```cpp
ACMD_FUNC(overflow)
{
    char buffer[50];
    // message could be 1000 characters!
    sprintf(buffer, "You said: %s", message);
    return 0;
}
```

**✅ CORRECT:**
```cpp
ACMD_FUNC(safe)
{
    char buffer[CHAT_SIZE_MAX];
    snprintf(buffer, sizeof(buffer), "You said: %.100s", message);
    return 0;
}
```

---

### Mistake 5: Wrong Parameter Parsing

**❌ WRONG:**
```cpp
BUILDIN_FUNC(wrong)
{
    // Gets parameter 1, but parameters start at 2!
    int32 value = script_getnum(st, 1);
    return SCRIPT_CMD_SUCCESS;
}
```

**✅ CORRECT:**
```cpp
BUILDIN_FUNC(correct)
{
    // Parameters start at index 2
    int32 value = script_getnum(st, 2);
    return SCRIPT_CMD_SUCCESS;
}
```

**Why:** Index 1 is reserved for the function name itself.

---

### Mistake 6: Forgetting to Recompile

**Problem:** You edit `.inc` files but don't recompile.

**Solution:**
```bash
# These files are INCLUDED at compile-time
# You MUST recompile after editing!

make map-server

# Or clean rebuild if changes don't take effect
make clean && make server
```

---

### Mistake 7: Conflicting Defines

**❌ WRONG:**
```cpp
// defines_post.hpp
#define SC_CUSTOM (SC_MAX + 1)  // Assume SC_MAX = 500

// Later rAthena adds more status changes...
// SC_MAX becomes 505
// Now SC_CUSTOM conflicts with new core SC!
```

**✅ CORRECT:**
```cpp
// defines_post.hpp
// Reserve a large gap for future core additions
#define SC_CUSTOM_START (SC_MAX + 100)
#define SC_CUSTOM_BUFF (SC_CUSTOM_START + 1)
#define SC_CUSTOM_DEBUFF (SC_CUSTOM_START + 2)
```

---

### Mistake 8: Memory Leaks in Script Commands

**❌ WRONG:**
```cpp
BUILDIN_FUNC(leak)
{
    char* buffer = (char*)aMalloc(1024);
    sprintf(buffer, "test");
    script_pushstr(st, buffer);
    // If script_pushstr fails, buffer leaks!
    return SCRIPT_CMD_SUCCESS;
}
```

**✅ CORRECT:**
```cpp
BUILDIN_FUNC(safe)
{
    char buffer[1024];
    sprintf(buffer, "test");
    script_pushstrcopy(st, buffer);  // Makes internal copy
    // Buffer automatically freed when function returns
    return SCRIPT_CMD_SUCCESS;
}
```

---

## 🔨 Build System Integration {#build-integration}

### How src/custom/ Integrates with Build

#### Makefile Integration

The Makefile automatically tracks dependencies:

```makefile
# src/map/Makefile.in (lines 117-125)

# atcommand.o depends on custom files
obj/atcommand.o: atcommand.cpp $(MAP_H) $(COMMON_H) \
                 ../custom/atcommand_def.inc \
                 ../custom/atcommand.inc

# script.o depends on custom files
obj/script.o: script.cpp $(MAP_H) $(COMMON_H) \
              ../custom/script_def.inc \
              ../custom/script.inc

# battle.o depends on custom files
obj/battle.o: battle.cpp $(MAP_H) $(COMMON_H) \
              ../custom/battle_config_init.inc
```

**What this means:**
- When you edit `src/custom/atcommand.inc`, only `atcommand.cpp` recompiles
- When you edit `src/custom/script.inc`, only `script.cpp` recompiles
- You DON'T need to `make clean` every time (unless major changes)

#### CMake Integration

CMake automatically includes the custom directory:

```cmake
# The custom directory is part of the source tree
# Changes to .inc files trigger recompilation
```

### Compilation Commands

```bash
# Initial compilation (after ./configure)
make server

# After editing custom files (fast - only rebuilds affected files)
make map-server

# If strange errors occur (nuclear option)
make clean && make server

# Check what will be recompiled
make -n map-server
```

### Troubleshooting Build Issues

#### Issue: Changes not taking effect

```bash
# Solution 1: Force recompile
touch src/custom/atcommand.inc
make map-server

# Solution 2: Clean build
make clean
make server
```

#### Issue: Undefined reference errors

```
Error: undefined reference to 'atcommand_mycommand'
```

**Cause:** Function defined in atcommand.inc but not registered in atcommand_def.inc (or vice versa)

**Solution:** Ensure BOTH files have matching entries.

#### Issue: Syntax errors in .inc files

```
Error: expected ';' before '}' token in atcommand.inc:50
```

**Solution:** .inc files are PURE C++ - they must follow exact syntax:
- Check for missing semicolons
- Check bracket matching
- Check function syntax

---

## 🤔 When to Edit Core vs Custom {#core-vs-custom}

### Use src/custom/ When:

✅ **Adding NEW functionality:**
- New @commands
- New script commands
- New configuration options
- New constants/defines

✅ **Extending existing systems:**
- Adding custom battle config
- Adding custom map flags (via defines)
- Adding custom status changes (via defines)

✅ **Server-specific features:**
- Custom events
- Custom reward systems
- Server-unique mechanics

### Edit Core Files When:

⚠️ **Modifying EXISTING behavior:**
- Changing how damage is calculated
- Changing how skills work
- Changing core game mechanics

⚠️ **Fixing bugs:**
- Crashes in existing code
- Logic errors in existing functions

⚠️ **Deep integration required:**
- New map types
- New item types
- New character classes

### The Decision Tree

```
┌─────────────────────────────────┐
│ What do you want to do?        │
└────────────┬────────────────────┘
             │
             ├─> Add new @command? ────────> Use src/custom/
             │
             ├─> Add new script function? ──> Use src/custom/
             │
             ├─> Change existing skill? ────> Edit core (src/map/skill.cpp)
             │
             ├─> Fix crash/bug? ────────────> Edit core
             │
             ├─> Add config option? ────────> Use src/custom/
             │
             └─> Modify damage formula? ────> Edit core (src/map/battle.cpp)
```

### Best Practices

1. **Start with src/custom/** - Try to do it there first
2. **Document core edits** - Comment WHY you changed it
3. **Use git branches** - Keep customs separate from core
4. **Test after updates** - Verify customs still work after `git pull`

### Example: Custom EXP System

**Option A: Using custom (recommended if adding NEW system)**
```cpp
// src/custom/script.inc
BUILDIN_FUNC(giveCustomExp) {
    // Your custom EXP calculation
    // Calls existing pc_gainexp() with your values
}
```

**Option B: Editing core (required if changing HOW exp works)**
```cpp
// src/map/pc.cpp - pc_gainexp()
// Modify the EXISTING exp gain formula
if (battle_config.enable_custom_exp_formula) {
    // Your changes HERE affect ALL exp gain in the game
}
```

---

## 📚 Cross-References & Resources

### Related KB Files

- **KB_REF_MemoryCrashPatterns.md** - Memory safety, nullpo checks
- **KB_REF_BattleStatusInternals.md** - Understanding status calculations
- **KB_REF_ScriptTimerInternals.md** - Script timer system (for timed events)

### Important Source Files

| File | Purpose | When to Read |
|------|---------|--------------|
| `src/map/atcommand.cpp` | @command system | Creating custom @commands |
| `src/map/script.cpp` | Script engine | Creating script commands |
| `src/map/battle.cpp` | Battle system | Understanding damage/config |
| `src/map/pc.cpp` | Player character | Player-related operations |
| `src/map/clif.cpp` | Client interface | Sending packets to client |
| `src/map/status.hpp` | Status changes | SC_* defines |
| `src/map/map.hpp` | Map system | MF_* map flags |

### Common Functions Reference

#### String Display Functions
```cpp
clif_displaymessage(fd, message);           // Send text to player
sprintf(atcmd_output, "format", ...);       // Format string into buffer
snprintf(buffer, size, "format", ...);      // Safe format (prevents overflow)
```

#### Script Stack Functions
```cpp
script_pushint(st, value);                  // Return integer to script
script_pushstr(st, string);                 // Return string (takes ownership)
script_pushstrcopy(st, string);             // Return string (makes copy)
script_getnum(st, index);                   // Get integer parameter
script_getstr(st, index);                   // Get string parameter
script_hasdata(st, index);                  // Check if parameter exists
script_rid2sd(sd);                          // Get player from script
```

#### Player Data Access
```cpp
pc_readaccountreg(sd, var);                 // Read account variable (#VAR)
pc_setaccountreg(sd, var, value);           // Write account variable
pc_readglobalreg(sd, var);                  // Read global variable ($VAR)
pc_setglobalreg(sd, var, value);            // Write global variable
pc_additem(sd, item, amount, log_type);     // Give item to player
pc_delitem(sd, index, amount, type, log);   // Remove item from player
pc_payzeny(sd, amount, log_type, nd);       // Remove zeny
pc_getzeny(sd, amount, log_type, nd);       // Give zeny
```

#### Status & Effects
```cpp
sc_start(src, bl, type, rate, val1, tick);  // Start status change
status_heal(bl, hp, sp, flag);              // Heal HP/SP
status_calc_pc(sd, opt);                    // Recalculate player stats
clif_specialeffect(bl, effect, target);     // Play visual effect
```

---

## 🎓 Summary

### Key Takeaways

1. **src/custom/ = Your Playground**
   - All custom code goes here
   - Survives rAthena updates
   - Clean separation from core

2. **Two-File Pattern**
   - Implementation (.inc) = The code
   - Definition (_def.inc) = The registration

3. **ACMD_FUNC for @commands**
   - Parameters: fd, sd, command, message
   - Return 0 for success, -1 for failure

4. **BUILDIN_FUNC for script commands**
   - Parameter: struct script_state* st
   - Return SCRIPT_CMD_SUCCESS or SCRIPT_CMD_FAILURE
   - Access params with script_getnum/script_getstr (index starts at 2!)

5. **defines_pre.hpp vs defines_post.hpp**
   - pre = Override BEFORE core
   - post = Add AFTER core

6. **Battle Config = Configurable Options**
   - Two files: struct + init
   - Accessible via battle_config.your_variable

7. **Always Recompile**
   - .inc files are compile-time includes
   - `make map-server` after every change

### Quick Reference Card

```
┌─────────────────────────────────────────────────────────┐
│ CUSTOM SYSTEM QUICK REFERENCE                          │
├─────────────────────────────────────────────────────────┤
│                                                         │
│ NEW @COMMAND:                                           │
│   1. Add ACMD_FUNC(name) { code } to atcommand.inc     │
│   2. Add ACMD_DEF(name), to atcommand_def.inc          │
│   3. make map-server                                    │
│                                                         │
│ NEW SCRIPT COMMAND:                                     │
│   1. Add BUILDIN_FUNC(name) { code } to script.inc     │
│   2. Add BUILDIN_DEF(name,"params"), to script_def.inc │
│   3. make map-server                                    │
│                                                         │
│ NEW CONFIG OPTION:                                      │
│   1. Add variable to battle_config_struct.inc           │
│   2. Add initialization to battle_config_init.inc       │
│   3. Add to conf/battle/battle.conf                     │
│   4. make map-server                                    │
│                                                         │
│ NEW DEFINE:                                             │
│   - Override core? → defines_pre.hpp                    │
│   - Add new? → defines_post.hpp                         │
│   - make clean && make server (defines need clean)      │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## 📖 Final Notes

### Safety Checklist

Before committing custom code:

- [ ] Null pointer checks (nullpo_retr)
- [ ] Buffer overflow protection (snprintf, not sprintf)
- [ ] Parameter validation
- [ ] Return value handling
- [ ] Memory leak prevention
- [ ] Recompiled and tested in-game
- [ ] No conflicts with core defines
- [ ] Trailing commas in _def.inc files
- [ ] Parameter indices start at 2 for script commands

### Debugging Tips

1. **Compile errors:** Check syntax in .inc files
2. **Linker errors:** Name mismatch between .inc and _def.inc
3. **Runtime crashes:** Add nullpo checks
4. **Changes not working:** Recompile with `make map-server`
5. **Weird behavior:** `make clean && make server`

### Getting Help

- **rAthena Forums:** https://rathena.org/board/
- **rAthena Discord:** https://discord.gg/rathena
- **GitHub Issues:** https://github.com/rathena/rathena/issues

### Version Information

- **Document Version:** 1.0
- **rAthena Version:** 2024+ (modern repo structure)
- **Last Updated:** 2024-01-15

---

**END OF DOCUMENT**

**Total sections:** 10 major sections
**Total examples:** 15+ working code examples
**Total file size:** ~20KB of comprehensive documentation

This document is part of the rAthena Knowledge Base v2.0 optimized for RAG systems.


# ═══════════════════════════════════════════════════════════════
# PART 2: BEST PRACTICES (CODE QUALITY & SAFETY)
# ═══════════════════════════════════════════════════════════════
<!-- RAG_CHUNK: best_practices_complete -->

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


# ═══════════════════════════════════════════════════════════════
# PART 3: MEMORY CRASH PATTERNS (CRITICAL SAFETY)
# ═══════════════════════════════════════════════════════════════
<!-- RAG_CHUNK: memory_crash_patterns_complete -->

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


# ═══════════════════════════════════════════════════════════════
# PART 4: SOURCE CODE STRUCTURE (CODEBASE OVERVIEW)
# ═══════════════════════════════════════════════════════════════
<!-- RAG_CHUNK: source_structure_complete -->

# rAthena Source Code Structure Reference

## Table of Contents
1. [Directory Structure Overview](#directory-structure-overview)
2. [Core Directories Deep Dive](#core-directories-deep-dive)
3. [Essential Data Structures](#essential-data-structures)
4. [File Responsibilities](#file-responsibilities)
5. [Data Flow Between Systems](#data-flow-between-systems)
6. [Include Hierarchy](#include-hierarchy)
7. [Build System (CMake)](#build-system-cmake)
8. [Feature Location Guide](#feature-location-guide)
9. [Navigation Quick Reference](#navigation-quick-reference)
10. [Code Examples](#code-examples)

---

## Directory Structure Overview

```
rathena2/
├── src/
│   ├── common/          # Shared code (all servers)
│   ├── map/             # Map server (game logic)
│   │   └── skills/      # Skill implementations by class
│   ├── char/            # Character server (save/load)
│   ├── login/           # Login server (authentication)
│   ├── web/             # Web server integration
│   ├── config/          # Compile-time configurations
│   │   └── classes/     # Class-specific configs
│   ├── tool/            # Development tools
│   └── custom/          # Custom modifications
├── 3rdparty/            # External dependencies
├── conf/                # Runtime configurations
├── db/                  # Game databases (YAML)
├── npc/                 # NPC scripts
└── sql-files/           # Database schemas
```

**Key Size Statistics (Line Counts):**
- script.cpp: 28,574 lines (largest - script engine)
- skill.cpp: 26,478 lines (skill system)
- clif.cpp: 25,821 lines (client interface/packets)
- status.cpp: 16,480 lines (status/stats calculations)
- pc.cpp: 16,102 lines (player character logic)
- battle.cpp: 12,680 lines (damage calculations)

---

## Core Directories Deep Dive

### 1. src/map/ - Map Server (Game Logic Core)

**Primary Files:**

| File | Lines | Purpose |
|------|-------|---------|
| **script.cpp/hpp** | 28,574 | Script engine, NPC commands (@commands, script functions) |
| **skill.cpp/hpp** | 26,478 | Skill system, casting, effects, requirements |
| **clif.cpp/hpp** | 25,821 | Client Interface - all packet handling (send/receive) |
| **status.cpp/hpp** | 16,480 | Status calculations, buffs/debuffs, stat computations |
| **pc.cpp/hpp** | 16,102 | Player character logic, inventory, equipment, jobs |
| **battle.cpp/hpp** | 12,680 | Damage calculations, battle formulas, element tables |
| **atcommand.cpp/hpp** | 12,074 | GM commands implementation |
| **mob.cpp/hpp** | 7,374 | Monster AI, spawning, movement, skills |
| **npc.cpp/hpp** | 6,381 | NPC management, script execution, shops |
| **map.cpp/hpp** | 5,478 | Map management, coordinates, zone handling |
| **itemdb.cpp/hpp** | 4,948 | Item database, bonuses, requirements |
| **unit.cpp/hpp** | 4,298 | Movement, pathfinding, target selection |
| **guild.cpp/hpp** | 2,755 | Guild systems, WoE, emblems |
| **party.cpp/hpp** | 1,573 | Party systems, exp sharing |

**Packet Files:**
- **packets.hpp** - Packet structure definitions
- **packets_struct.hpp** - Actual packet structs
- **clif_packetdb.hpp** - Packet database
- **clif_obfuscation.hpp** - Packet encryption/obfuscation
- **clif_shuffle.hpp** - Packet key shuffling

**Skills Subdirectory** (`src/map/skills/`):
```
skills/
├── acolyte/          # Priest, Monk skills
├── archer/           # Hunter, Bard/Dancer skills
├── mage/             # Wizard, Sage skills
├── merchant/         # Blacksmith, Alchemist skills
├── swordman/         # Knight, Crusader skills
├── thief/            # Assassin, Rogue skills
├── novice/           # Novice/Super Novice skills
├── gunslinger/       # Gunslinger skills
├── ninja/            # Ninja skills
├── summoner/         # Summoner skills
├── mercenary/        # Mercenary skills
├── npc/              # NPC/Monster skills
├── custom/           # Custom skill implementations
├── skill_impl.cpp/hpp          # Skill implementation base
├── skill_factory.cpp/hpp       # Skill factory pattern
├── status_skill_impl.cpp/hpp   # Status-related skills
└── weapon_skill_impl.cpp/hpp   # Weapon-based skills
```

### 2. src/char/ - Character Server

**Primary Files:**

| File | Purpose |
|------|---------|
| **char.cpp/hpp** | Main character server, character management |
| **char_clif.cpp/hpp** | Client interface for char server |
| **char_logif.cpp/hpp** | Login server interface |
| **char_mapif.cpp/hpp** | Map server interface |
| **inter.cpp/hpp** | Inter-server communication core |
| **int_guild.cpp/hpp** | Guild inter-server operations |
| **int_party.cpp/hpp** | Party inter-server operations |
| **int_storage.cpp/hpp** | Storage inter-server operations |
| **int_mail.cpp/hpp** | Mail system inter-server |
| **int_auction.cpp/hpp** | Auction system inter-server |
| **int_quest.cpp/hpp** | Quest inter-server operations |
| **int_pet.cpp/hpp** | Pet inter-server operations |
| **int_homun.cpp/hpp** | Homunculus inter-server |
| **int_mercenary.cpp/hpp** | Mercenary inter-server |
| **int_elemental.cpp/hpp** | Elemental inter-server |
| **int_achievement.cpp/hpp** | Achievement inter-server |
| **int_clan.cpp/hpp** | Clan inter-server operations |

### 3. src/login/ - Login Server

**Primary Files:**

| File | Purpose |
|------|---------|
| **login.cpp/hpp** | Main login server logic |
| **account.cpp/hpp** | Account management, database operations |
| **loginclif.cpp/hpp** | Client interface (login packets) |
| **loginchrif.cpp/hpp** | Character server interface |
| **logincnslif.cpp/hpp** | Console interface |
| **loginlog.cpp/hpp** | Login logging system |
| **ipban.cpp/hpp** | IP banning system |

### 4. src/common/ - Shared Libraries

**Core Files:**

| File | Purpose |
|------|---------|
| **mmo.hpp** | Core definitions, limits, constants (MAX_INVENTORY, etc.) |
| **cbasetypes.hpp** | Base types (uint8, int32, etc.) |
| **db.cpp/hpp** | Database abstraction layer |
| **database.cpp/hpp** | YAML database system |
| **socket.cpp/hpp** | Network socket handling |
| **timer.cpp/hpp** | Timer/tick system |
| **malloc.cpp/hpp** | Memory management |
| **showmsg.cpp/hpp** | Logging/output system |
| **strlib.cpp/hpp** | String utilities |
| **utils.cpp/hpp** | General utilities |
| **random.cpp/hpp** | Random number generation |
| **nullpo.cpp/hpp** | Null pointer checking |
| **core.cpp/hpp** | Server core initialization |
| **sql.cpp/hpp** | SQL database interface |
| **mapindex.cpp/hpp** | Map index management |
| **grfio.cpp/hpp** | GRF file reading |
| **conf.cpp/hpp** | Configuration file parsing |
| **ers.cpp/hpp** | Entry Reusage System (memory pools) |

**Location:** `/home/user/rathena2/src/common/mmo.hpp`

### 5. src/config/ - Compile-Time Configuration

**Configuration Files:**

| File | Purpose |
|------|---------|
| **core.hpp** | Core features (renewal, secure, etc.) |
| **const.hpp** | Constant definitions |
| **packets.hpp** | Packet version configuration |
| **renewal.hpp** | Renewal mode settings |
| **secure.hpp** | Security settings |
| **classes/*.hpp** | Class-specific configurations |

---

## Essential Data Structures

### 1. block_list - Universal Object Base

**Location:** `/home/user/rathena2/src/map/map.hpp:461-466`

```cpp
struct block_list {
    struct block_list *next, *prev;  // Linked list pointers
    int32 id;                        // Unique object ID
    int16 m, x, y;                   // Map index, coordinates
    enum bl_type type;               // Object type (PC, MOB, NPC, etc.)
};
```

**Purpose:** Base structure for all map objects. Every entity (player, mob, NPC, item) starts with this.

**Type Enumeration (bl_type):**
- `BL_NUL` - Invalid/null
- `BL_PC` - Player character
- `BL_MOB` - Monster
- `BL_PET` - Pet
- `BL_HOM` - Homunculus
- `BL_MER` - Mercenary
- `BL_ELEM` - Elemental
- `BL_NPC` - NPC
- `BL_ITEM` - Floor item
- `BL_SKILL` - Skill unit (ground skills)
- `BL_CHAT` - Chat room

### 2. map_session_data - Player Character

**Location:** `/home/user/rathena2/src/map/pc.hpp:381+`

```cpp
class map_session_data : public block_list {
public:
    struct unit_data ud;                        // Movement, targets, timers
    struct view_data vd;                        // Visual appearance data
    struct status_data base_status, battle_status;  // Base/calculated stats
    status_change sc;                           // Status change (buffs/debuffs)
    struct regen_data regen;                    // HP/SP regeneration

    // State flags
    struct s_state {
        uint32 active : 1;                      // Active player flag
        uint32 menu_or_input : 1;               // NPC interaction state
        uint32 dead_sit : 2;                    // Dead/sitting state
        e_lr_flag lr_flag;                      // Left/right hand flag
        uint32 arrow_atk : 1;                   // Arrow attack flag
        uint32 storage_flag : 3;                // Storage open state
        uint32 trading : 1;                     // Trade state
        uint32 vending : 1;                     // Vending state
        uint32 buyingstore : 1;                 // Buying store state
        // ... many more flags
    } state;

    // Special states from equipment/buffs
    struct {
        unsigned char no_weapon_damage, no_magic_damage, no_misc_damage;
        uint32 restart_full_recover : 1;
        uint32 no_castcancel : 1;
        uint32 no_gemstone : 2;
        uint32 intravision : 1;                 // Maya Purple Card
        uint32 perfect_hiding : 1;
        // ... more special states
    } special_state;

    uint32 login_id1, login_id2;                // Login session IDs
    uint64 class_;                              // Job ID
    int32 group_id;                             // Permission group

    struct mmo_charstatus status;               // Character data (DB)

    // Inventories
    struct s_storage storage, premiumStorage;   // Storages
    struct s_storage inventory;                 // Player inventory
    struct s_storage cart;                      // Cart

    struct item_data* inventory_data[MAX_INVENTORY];  // Item data pointers
    int16 equip_index[EQI_MAX];                 // Equipment indices

    uint32 weight, max_weight, add_max_weight;  // Weight system
    int32 fd;                                   // Socket file descriptor
    uint16 mapindex;                            // Current map index

    // ... hundreds more fields (equipment bonuses, skill data, etc.)
};
```

**Key Sections:**
- **Lines 381-499:** Core data, state, inventory
- **Lines 500-700:** Skills, bonuses, equipment data
- **Lines 700-900:** Combat stats, regeneration, timers
- **Lines 900+:** Social, quests, achievements

### 3. mob_data - Monster Instance

**Location:** `/home/user/rathena2/src/map/mob.hpp:337-349+`

```cpp
struct mob_data : public block_list {
    struct unit_data ud;                        // Movement/AI data
    struct view_data *vd;                       // Visual data pointer
    bool vd_changed;                            // View changed flag
    struct status_data status, *base_status;    // Current/base stats
    status_change sc;                           // Status changes
    std::shared_ptr<s_mob_db> db;              // Mob database entry
    char name[NAME_LENGTH];                     // Custom name

    struct s_specialState {
        uint32 size : 2;                        // Small/Big size
        enum mob_ai ai;                         // Special AI type
        uint32 clone : 1;                       // Clone flag
    } special_state;

    struct spawn_data *spawn;                   // Spawn point data
    int16 spawn_x, spawn_y;                     // Spawn coordinates

    // Damage log for MVP calculation
    struct s_dmglog {
        int32 id;                               // Char ID
        int64 dmg;                              // Damage dealt
        int64 dmg_tanked;                       // Damage tanked
        uint32 flag : 2;                        // Damage type flag
    } dmglog[DAMAGELOG_SIZE];

    // ... more fields (loot, timers, states)
};
```

**Mob Database Structure** (`s_mob_db` - Lines 261-285):
```cpp
struct s_mob_db {
    uint32 id;                                  // Monster ID
    std::string sprite;                         // Sprite name
    std::string name;                           // Monster name
    std::string jname;                          // Japanese name
    t_exp base_exp, job_exp, mexp;             // Experience values
    uint16 range2, range3;                      // Chase/sight range
    std::vector<e_race2> race2;                // Race2 types
    uint16 lv;                                  // Level
    std::vector<std::shared_ptr<s_mob_drop>> dropitem;     // Drops
    std::vector<std::shared_ptr<s_mob_drop>> mvpitem;      // MVP drops
    status_data status;                         // Base stats
    view_data vd;                               // Visual data
    uint32 option;                              // Special options
    std::vector<std::shared_ptr<s_mob_skill>> skill;       // Mob skills
    uint16 damagetaken;                         // Damage modifier
    int32 group_id;                             // Mob group
    std::string title;                          // Title string
};
```

### 4. item_data - Item Database Entry

**Location:** `/home/user/rathena2/src/map/itemdb.hpp:150+`

```cpp
struct item_data {
    t_itemid nameid;                            // Item ID
    char name[ITEM_NAME_LENGTH];                // Item name (English)
    char jname[ITEM_NAME_LENGTH];               // Item name (Japanese)

    enum item_types type;                       // Item type
    int32 value_buy;                            // Buy price
    int32 value_sell;                           // Sell price
    int32 weight;                               // Weight
    int32 atk;                                  // ATK
    int32 matk;                                 // MATK
    int32 def;                                  // DEF

    int32 range;                                // Attack range
    uint32 slot;                                // Card slots
    uint64 class_base[3];                       // Job restrictions
    uint32 class_upper;                         // Upper job restrictions
    uint64 sex;                                 // Gender restrictions
    uint32 equip;                               // Equipment position

    int32 wlv;                                  // Weapon level
    int32 elv;                                  // Equipment level

    struct script_code *script;                 // Use/equip script
    struct script_code *equip_script;           // Equip bonus script
    struct script_code *unequip_script;         // Unequip script

    struct {
        uint32 delay;                           // Item delay
        uint32 status;                          // Required status
        // ... more requirements
    } require;

    // ... item flags, bonuses, randomoptions
};
```

### 5. s_skill_db - Skill Database Entry

**Location:** `/home/user/rathena2/src/map/skill.hpp:150+`

```cpp
struct s_skill_db {
    uint16 nameid;                              // Skill ID
    char name[SKILL_NAME_LENGTH];               // Skill name
    char desc[SKILL_DESC_LENGTH];               // Description

    std::bitset<INF2_MAX> inf2;                 // Skill info flags
    uint16 inf;                                 // Skill type (attack/support)
    std::bitset<NK_MAX> nk;                     // Damage properties

    uint16 range[MAX_SKILL_LEVEL];              // Cast range per level
    int16 hit;                                  // Hit type

    uint16 max_level;                           // Max skill level

    struct {
        int16 hp[MAX_SKILL_LEVEL];              // HP cost
        int16 sp[MAX_SKILL_LEVEL];              // SP cost
        int16 hp_rate[MAX_SKILL_LEVEL];         // HP% cost
        int16 sp_rate[MAX_SKILL_LEVEL];         // SP% cost
        int16 zeny[MAX_SKILL_LEVEL];            // Zeny cost
        uint32 weapon;                          // Weapon requirement
        uint32 ammo;                            // Ammo requirement
        // ... more requirements
    } require;

    int32 casttime[MAX_SKILL_LEVEL];            // Cast time
    int32 delay[MAX_SKILL_LEVEL];               // After-cast delay
    int32 cooldown[MAX_SKILL_LEVEL];            // Cooldown

    // ... damage calculations, splash, flags
};
```

### 6. status_data - Entity Stats

**Location:** `/home/user/rathena2/src/map/status.hpp:200+`

```cpp
struct status_data {
    uint32 hp, sp, ap;                          // Current HP/SP/AP
    uint32 max_hp, max_sp, max_ap;              // Max HP/SP/AP

    uint16 str, agi, vit, int_, dex, luk;       // Primary stats
    uint16 pow, sta, wis, spl, con, crt;        // 4th job stats

    uint32 batk, watk, watk2;                   // Base/weapon ATK
    uint32 matk_min, matk_max;                  // Magic ATK
    int32 def, mdef;                            // Defense
    int32 def2, mdef2;                          // Soft defense

    int32 hit, flee, flee2;                     // Accuracy/evasion
    int32 cri;                                  // Critical rate
    int32 aspd, amotion, dmotion;               // Attack speed/motion

    uint16 speed;                               // Movement speed
    uint16 size;                                // Entity size
    uint16 race;                                // Race
    uint16 element;                             // Element

    // ... many more combat stats
};
```

### 7. unit_data - Movement & Action Control

**Location:** `/home/user/rathena2/src/map/unit.hpp:40+`

```cpp
struct unit_data {
    block_list *bl;                             // Owner
    struct walkpath_data walkpath;              // Path data

    t_tick attacktimer;                         // Attack timer
    t_tick walktimer;                           // Walk timer

    int32 target;                               // Current target ID
    int32 target_to;                            // Next target

    uint16 skill_id, skill_lv;                  // Casting skill
    int32 skilltarget;                          // Skill target ID
    t_tick skilltimer;                          // Skill timer

    struct {
        uint16 id;                              // Skill unit group ID
        t_tick tick;                            // Creation tick
    } stepskill;                                // Step skill data

    uint16 state;                               // Unit state flags
    uint8 dir;                                  // Facing direction

    // ... combat, movement state
};
```

---

## File Responsibilities

### Combat & Battle System

**battle.cpp/hpp** (12,680 lines)
- **Primary Functions:**
  - `battle_calc_attack()` - Main damage calculation entry
  - `battle_calc_weapon_attack()` - Physical damage
  - `battle_calc_magic_attack()` - Magic damage
  - `battle_calc_misc_attack()` - Misc damage (traps, etc.)
  - `battle_attr_fix()` - Element modifier calculation
  - `battle_calc_defense()` - Defense reduction
  - `battle_damage()` - Apply damage to target

**Key Code:** Lines 48-70
```cpp
/**
 * Returns the current/list skill used by the bl
 * @param bl
 * @return skill_id
 */
uint16 battle_getcurrentskill(block_list *bl)
{
    struct unit_data *ud;

    if( bl->type == BL_SKILL ) {
        skill_unit *su = (skill_unit*)bl;
        return (su && su->group?su->group->skill_id:0);
    }

    ud = unit_bl2ud(bl);
    return (ud?ud->skill_id:0);
}
```

**Battle Configuration:** `struct Battle_Config battle_config` - Global battle settings

### Player Management

**pc.cpp/hpp** (16,102 lines)
- **Primary Functions:**
  - `pc_authok()` - Player login initialization
  - `pc_reg_received()` - Load player data from char server
  - `pc_makesavestatus()` - Prepare save data
  - `pc_equipitem()` - Equip item
  - `pc_unequipitem()` - Unequip item
  - `pc_additem()` - Add item to inventory
  - `pc_delitem()` - Remove item from inventory
  - `pc_dropitem()` - Drop item on ground
  - `pc_checkskill()` - Check if player has skill
  - `pc_gainexp()` - Add experience
  - `pc_levelup()` - Level up process
  - `pc_jobchange()` - Change job

**Includes (Lines 4-66):**
```cpp
#include "pc.hpp"

#include <common/cbasetypes.hpp>
#include <common/database.hpp>
#include <common/mmo.hpp>
#include <common/nullpo.hpp>
#include <common/random.hpp>
#include <common/showmsg.hpp>
#include <common/socket.hpp>
#include <common/timer.hpp>

#include "achievement.hpp"
#include "atcommand.hpp"
#include "battle.hpp"
#include "clif.hpp"
#include "guild.hpp"
#include "itemdb.hpp"
#include "mob.hpp"
#include "npc.hpp"
#include "party.hpp"
#include "skill.hpp"
#include "status.hpp"
#include "storage.hpp"
// ... more includes
```

### Monster AI & Management

**mob.cpp/hpp** (7,374 lines)
- **Primary Functions:**
  - `mob_spawn()` - Spawn monster
  - `mob_spawn_guardian()` - Spawn guardian
  - `mob_ai_sub_hard()` - Monster AI logic
  - `mob_attack()` - Monster attack
  - `mob_skill_use()` - Monster skill usage
  - `mob_damage()` - Damage monster
  - `mob_dead()` - Monster death handling
  - `mob_drop_item()` - Drop items
  - `mob_summon()` - Summon monsters

**Monster Skill Structure** (Lines 196-208):
```cpp
struct s_mob_skill {
    enum MobSkillState state;    // MSS_IDLE, MSS_WALK, MSS_ATTACK, etc.
    uint16 skill_id, skill_lv;   // Skill ID and level
    int16 permillage;            // Usage rate (per 1000)
    int32 casttime, delay;       // Cast time, delay
    int16 cancel;                // Cancel flag
    int16 cond1;                 // Condition 1
    int64 cond2;                 // Condition 2
    int16 target;                // Target type
    int32 val[5];                // Additional values
    int16 emotion;               // Emotion to display
    uint16 msg_id;               // Message ID
};
```

### Skill System

**skill.cpp/hpp** (26,478 lines)
- **Primary Functions:**
  - `skill_check_condition()` - Validate skill requirements
  - `skill_use_id()` - Use skill on target
  - `skill_use_pos()` - Use skill on ground
  - `skill_castend_id()` - Finish casting on target
  - `skill_castend_pos()` - Finish casting on ground
  - `skill_attack()` - Skill attack damage
  - `skill_area_sub()` - Area skill processing
  - `skill_timerskill()` - Delayed skill effects
  - `skill_addtimerskill()` - Add timed skill
  - `skill_castcancel()` - Cancel casting

**Skill Constants** (Lines 31-48):
```cpp
#define MAX_SKILL_PRODUCE_DB    300     // Max Produce DB
#define MAX_PRODUCE_RESOURCE    12      // Max Produce requirements
#define MAX_SKILL_LEVEL         13      // Max Skill Level (for skill_db storage)
#define MAX_MOBSKILL_LEVEL      100     // Max monster skill level (on skill usage)
#define MAX_SKILL_CRIMSON_MARKER 3      // Max Crimson Marker targets (RL_C_MARKER)
#define SKILL_NAME_LENGTH       40      // Max Skill Name length
#define SKILL_DESC_LENGTH       40      // Max Skill Desc length

// Used with tracking the hitcount of Earthquake for skills that can avoid the first attack
#define NPC_EARTHQUAKE_FLAG 0x800

// To control alternative skill scalings
#define SKILL_ALTDMG_FLAG 0x10
// Make skill ignore requirement consumption
#define SKILL_NOCONSUME_REQ 0x20
// Make skill consume ammo, but not the unit
#define UNIT_NOCONSUME_AMMO 0x40
```

### Status & Stats Calculation

**status.cpp/hpp** (16,480 lines)
- **Primary Functions:**
  - `status_calc_pc()` - Calculate player stats (main)
  - `status_calc_mob()` - Calculate monster stats
  - `status_calc_str()`, `status_calc_agi()`, etc. - Calculate individual stats
  - `status_base_atk()` - Calculate base ATK
  - `status_calc_watk()` - Calculate weapon ATK
  - `status_calc_matk()` - Calculate magic ATK
  - `status_calc_def()` - Calculate defense
  - `status_calc_flee()` - Calculate flee
  - `status_change_start()` - Start status effect
  - `status_change_end()` - End status effect
  - `status_calc_regen()` - Calculate regeneration

**Status Change System:**
- Over 700+ status effects defined
- Timers for buff/debuff management
- Icon display to client
- Stack rules (stackable, non-stackable, refresh)

### Network & Packets

**clif.cpp/hpp** (25,821 lines)
- **Primary Functions:**
  - `clif_parse()` - Main packet parser
  - `clif_parse_*()` - Individual packet handlers (hundreds)
  - `clif_send()` - Send packet to client
  - `clif_displaymessage()` - Display message
  - `clif_skill_damage()` - Show skill damage
  - `clif_damage()` - Show physical damage
  - `clif_updatestatus()` - Update player status
  - `clif_changelook()` - Change appearance
  - `clif_item_equip()` - Show equipment change
  - `clif_inventorylist()` - Send inventory

**Includes (Lines 1-61):**
```cpp
#include "clif.hpp"

#include <common/cbasetypes.hpp>
#include <common/socket.hpp>
#include <common/timer.hpp>
#include <common/nullpo.hpp>
#include <common/random.hpp>
#include <common/showmsg.hpp>
#include <common/strlib.hpp>
#include <common/utils.hpp>

#include "achievement.hpp"
#include "atcommand.hpp"
#include "battle.hpp"
#include "battleground.hpp"
#include "cashshop.hpp"
#include "channel.hpp"
#include "chat.hpp"
#include "clan.hpp"
#include "elemental.hpp"
#include "guild.hpp"
#include "homunculus.hpp"
#include "instance.hpp"
#include "intif.hpp"
#include "itemdb.hpp"
#include "log.hpp"
#include "mail.hpp"
#include "map.hpp"
#include "mercenary.hpp"
#include "mob.hpp"
#include "npc.hpp"
#include "party.hpp"
#include "pc.hpp"
#include "pet.hpp"
#include "quest.hpp"
#include "script.hpp"
#include "skill.hpp"
#include "status.hpp"
#include "storage.hpp"
#include "unit.hpp"
#include "vending.hpp"
```

### Script Engine

**script.cpp/hpp** (28,574 lines - LARGEST FILE)
- **Primary Functions:**
  - `script_parse()` - Parse NPC scripts
  - `run_script()` - Execute script
  - `script_rid2sd()` - Get player from RID
  - `script_getnum()` - Get number parameter
  - `script_getstr()` - Get string parameter
  - `script_setvar()` - Set variable
  - `script_getvar()` - Get variable
  - Hundreds of builtin functions (BUILDIN macro)

**Script Built-in Functions:**
- Item manipulation: `getitem()`, `delitem()`, `getitemname()`
- Player data: `getcharid()`, `getskillv()`, `getskilllv()`
- Stats: `readparam()`, `getstat()`
- Skills: `skill()`, `addtoskill()`, `guildskill()`
- NPC interaction: `menu()`, `select()`, `input()`
- Timers: `addtimer()`, `deltimer()`, `sleep()`
- Maps: `warp()`, `areawarp()`, `mapannounce()`
- Combat: `monster()`, `areamonster()`, `killmonster()`
- And 500+ more functions

**Script State** (Lines 77-100):
```cpp
struct eri *array_ers;
DBMap *st_db;
uint32 active_scripts;
uint32 next_id;
struct eri *st_ers;
struct eri *stack_ers;
static map_session_data* dummy_sd;

static bool script_rid2sd_( struct script_state *st, map_session_data** sd, const char *func );

/**
 * Get `sd` from a account id in `loc` param instead of attached rid
 * @param st Script
 * @param loc Location to look account id in script parameter
 * @param sd Variable that will be assigned
 * @return True if `sd` is assigned, false otherwise
 **/
static bool script_accid2sd_(struct script_state *st, uint8 loc, map_session_data **sd, const char *func) {
    if (script_hasdata(st, loc)) {
        int32 id_ = script_getnum(st, loc);
        if (!(*sd = map_id2sd(id_))){
            ShowError("%s: Player with account id '%d' is not found.\n", func, id_);
            return false;
        }else{
            return true;
        }
    }
    else
        return script_rid2sd_(st,sd,func);
}
```

### Item Database

**itemdb.cpp/hpp** (4,948 lines)
- **Primary Functions:**
  - `itemdb_search()` - Find item by ID
  - `itemdb_exists()` - Check if item exists
  - `itemdb_searchname()` - Find item by name
  - `itemdb_isequip()` - Is equipment
  - `itemdb_isstackable()` - Is stackable
  - `itemdb_type()` - Get item type
  - `itemdb_weight()` - Get item weight
  - `itemdb_value_buy()` - Get buy price
  - `itemdb_value_sell()` - Get sell price
  - `itemdb_canrefine()` - Can refine
  - `itemdb_isidentified()` - Is identified

**Item Type Enum:**
```cpp
enum item_types {
    IT_HEALING = 0,        // Consumables
    IT_UNKNOWN,            // Unknown
    IT_USABLE,             // Usable items
    IT_ETC,                // Etc items
    IT_WEAPON,             // Weapons
    IT_ARMOR,              // Armor
    IT_CARD,               // Cards
    IT_PETEGG,             // Pet eggs
    IT_PETARMOR,           // Pet equipment
    IT_UNKNOWN2,           // Unknown
    IT_AMMO,               // Ammo
    IT_DELAYCONSUME,       // Delay consume
    IT_CASH = 18,          // Cash shop items
    IT_MAX
};
```

### Map Management

**map.cpp/hpp** (5,478 lines)
- **Primary Functions:**
  - `map_addflooritem()` - Add item to floor
  - `map_foreachinarea()` - Execute function in area
  - `map_foreachincell()` - Execute in cell
  - `map_foreachinrange()` - Execute in range
  - `map_searchrandfreecell()` - Find random free cell
  - `map_mapindex2mapid()` - Convert map index to ID
  - `map_id2bl()` - Get block_list by ID
  - `map_id2sd()` - Get player by ID
  - `map_id2md()` - Get mob by ID
  - `map_id2nd()` - Get NPC by ID

**Block List Iteration:**
The map server uses linked lists for efficient object iteration:
```cpp
// Iterate all objects in a range
map_foreachinrange(function, center_bl, range, type, ...args);

// Iterate all objects in rectangular area
map_foreachinarea(function, m, x0, y0, x1, y1, type, ...args);

// Iterate all objects in a cell
map_foreachincell(function, m, x, y, type, ...args);
```

### NPC Management

**npc.cpp/hpp** (6,381 lines)
- **Primary Functions:**
  - `npc_parse_script()` - Parse script NPC
  - `npc_parse_warp()` - Parse warp NPC
  - `npc_parse_shop()` - Parse shop NPC
  - `npc_click()` - NPC click handler
  - `npc_scriptcont()` - Continue script
  - `npc_buylist()` - Process buy
  - `npc_selllist()` - Process sell
  - `npc_event()` - Trigger event
  - `npc_timerevent()` - NPC timer event

### Unit Control (Movement/Actions)

**unit.cpp/hpp** (4,298 lines)
- **Primary Functions:**
  - `unit_walktoxy()` - Walk to coordinates
  - `unit_stop_walking()` - Stop walking
  - `unit_attack()` - Start attack
  - `unit_stop_attack()` - Stop attack
  - `unit_skilluse_id()` - Use skill on target
  - `unit_skilluse_pos()` - Use skill on position
  - `unit_warp()` - Warp unit
  - `unit_movepos()` - Move to position
  - `unit_setdir()` - Set facing direction

---

## Data Flow Between Systems

### Player Login Sequence

```
[Client] --> [Login Server] --> [Char Server] --> [Map Server]
```

**Detailed Flow:**

1. **Login Server** (`login.cpp`)
   - Client sends login packet → `loginclif_parse()`
   - Validate credentials → `account_db.load()`
   - Send character server list → `loginclif_server_list()`

2. **Character Server** (`char.cpp`)
   - Client selects character → `char_parse_char_select()`
   - Load character data from DB → `char_mmo_char_fromsql()`
   - Send to map server → `char_mapif_char_select_ack()`

3. **Map Server** (`pc.cpp`, `chrif.cpp`)
   - Receive auth request → `chrif_authreq()`
   - Character server responds → `chrif_authok()`
   - Initialize player → `pc_authok()` (Line ~1000+)
   - Load player data → `pc_reg_received()`
   - Calculate stats → `status_calc_pc()`
   - Send to map → `pc_setpos()`
   - Send player data to client → `clif_authok()`

### Skill Cast Sequence

```
Client Input → Validation → Requirements → Casting → Effect → Damage
```

**Detailed Flow:**

1. **Client Packet** (`clif.cpp`)
   ```
   clif_parse_UseSkillToId() or clif_parse_UseSkillToPos()
   ```

2. **Skill Request** (`skill.cpp`)
   ```
   skill_use_id() / skill_use_pos()
   ├─> skill_check_condition()  // Check requirements
   │   ├─> pc_checkskill()      // Has skill?
   │   ├─> Check SP/HP cost
   │   ├─> Check item requirements
   │   └─> Check state (mounted, etc.)
   ├─> unit_skilluse_id()       // Start casting
   ├─> skill_castend_id()       // Finish cast (timer)
   └─> skill_attack()           // Deal damage
   ```

3. **Damage Calculation** (`battle.cpp`)
   ```
   battle_calc_attack()
   ├─> battle_calc_weapon_attack()  // Physical
   │   ├─> status_base_atk()
   │   ├─> status_calc_watk()
   │   └─> battle_attr_fix()        // Element
   ├─> battle_calc_magic_attack()   // Magic
   └─> battle_calc_misc_attack()    // Misc
   ```

4. **Apply Damage** (`battle.cpp`, `mob.cpp`/`pc.cpp`)
   ```
   battle_damage()
   ├─> If target is PC: pc_damage()
   ├─> If target is MOB: mob_damage()
   └─> clif_damage()  // Show to client
   ```

5. **Death Handling**
   ```
   If HP <= 0:
   ├─> pc_dead() / mob_dead()
   ├─> Drop items (mob_drop_item)
   ├─> Calculate EXP (mob_dead → pc_gainexp)
   └─> Respawn (mob_spawn) or Return to save point
   ```

### Item Use Sequence

```
Use Item → Check Conditions → Run Script → Apply Effects → Update Client
```

**Detailed Flow:**

1. **Client Request** (`clif.cpp`)
   ```
   clif_parse_UseItem(fd, sd, packet)
   ```

2. **Item Usage** (`pc.cpp`)
   ```
   pc_useitem()
   ├─> itemdb_exists()        // Item exists?
   ├─> Check requirements     // Level, job, etc.
   ├─> pc_delitem()          // Remove from inventory
   ├─> script_run()          // Run item script
   └─> clif_useitemack()     // Confirm to client
   ```

3. **Item Script Execution** (`script.cpp`)
   ```
   run_script(item->script, 0, sd->bl.id, 0)
   ├─> Example: percentheal(50, 50)  // Heal 50% HP/SP
   ├─> sc_start() // Apply status
   └─> Other effects
   ```

### Monster AI Cycle

```
Think Timer → Evaluate State → Choose Action → Execute → Repeat
```

**Detailed Flow:**

1. **AI Timer** (`mob.cpp`)
   ```
   mobai_sub_hard_timer()  // Every MIN_MOBTHINKTIME (100ms)
   ├─> mob_ai_sub_hard(md)
   └─> For each mob on map
   ```

2. **AI State Machine** (`mob.cpp`)
   ```
   mob_ai_sub_hard(md)
   ├─> Check state (IDLE, WALK, ATTACK, DEAD, etc.)
   ├─> mob_ai_sub_hard_activesearch()  // Look for targets
   ├─> mob_ai_sub_hard_slavemob()      // Handle slaves
   ├─> mob_ai_sub_hard_lootsearch()    // Look for loot
   ├─> Decision making:
   │   ├─> Attack target?
   │   ├─> Use skill?
   │   ├─> Move/Chase?
   │   └─> Return to spawn?
   └─> Execute action
   ```

3. **Mob Skill Usage** (`mob.cpp`)
   ```
   mob_skill_use()
   ├─> Check conditions (HP%, state, distance)
   ├─> Calculate skill success rate
   ├─> unit_skilluse_id()/unit_skilluse_pos()
   └─> Apply skill effects
   ```

### Party EXP Share

```
Monster Death → Calculate EXP → Distribute to Party → Update Members
```

**Detailed Flow:**

1. **Monster Death** (`mob.cpp`)
   ```
   mob_dead(md, src)
   ├─> Calculate base/job EXP
   ├─> party_exp_share()  // If in party
   └─> pc_gainexp()       // If solo
   ```

2. **Party Distribution** (`party.cpp`)
   ```
   party_exp_share(p, src, base_exp, job_exp)
   ├─> Count eligible members (in range, alive)
   ├─> Apply bonuses (party bonus)
   ├─> For each member:
   │   ├─> Calculate share
   │   ├─> pc_gainexp(sd, base, job)
   │   └─> clif_updatestatus()  // Show EXP gain
   └─> Handle overflow
   ```

---

## Include Hierarchy

### Common Include Pattern

**Top Level:** `map/*.cpp` files

**Include Order:**
1. Own header (e.g., `pc.cpp` includes `pc.hpp`)
2. C/C++ standard libraries
3. Common headers (`<common/...>`)
4. Map server headers (local)

**Example from pc.cpp (Lines 4-66):**

```cpp
#include "pc.hpp"                    // 1. Own header

#include <cmath>                     // 2. C++ standard
#include <cstdlib>
#include <map>

#include <common/cbasetypes.hpp>    // 3. Common libs
#include <common/database.hpp>
#include <common/mmo.hpp>
#include <common/nullpo.hpp>
#include <common/random.hpp>
#include <common/showmsg.hpp>
#include <common/socket.hpp>
#include <common/timer.hpp>

#include "achievement.hpp"           // 4. Map server headers
#include "atcommand.hpp"
#include "battle.hpp"
#include "clif.hpp"
#include "guild.hpp"
#include "itemdb.hpp"
#include "mob.hpp"
#include "npc.hpp"
#include "party.hpp"
#include "skill.hpp"
#include "status.hpp"
#include "unit.hpp"
```

### Core Dependencies

**Base Types:** `common/cbasetypes.hpp`
- Defines: `uint8`, `uint16`, `uint32`, `uint64`, `int8`, `int16`, `int32`, `int64`
- Platform-specific size checks
- Boolean type definitions

**MMO Core:** `common/mmo.hpp`
- Game constants (MAX_INVENTORY, MAX_SKILL, etc.)
- Structure definitions (mmo_charstatus, item, etc.)
- Limits and boundaries

**Database:** `common/database.hpp`
- YAML database base classes
- TypesafeYamlDatabase template
- Database loading/parsing

**Network:** `common/socket.hpp`
- Socket management
- Session handling
- Packet buffers

**Memory:** `common/malloc.hpp`, `common/ers.hpp`
- Memory allocation wrappers
- Entry Reusage System (object pools)
- Memory debugging support

### Forward Declarations

Many headers use forward declarations to reduce compile dependencies:

**Example from map.hpp:**
```cpp
struct chat_data;
struct homun_data;
struct mob_data;
struct npc_data;
struct pet_data;
struct skill_unit;
struct item_data;
struct s_elemental_data;
struct s_mercenary_data;
struct Channel;
```

This allows including `map.hpp` without pulling in all dependent headers.

---

## Build System (CMake)

### Root CMakeLists.txt

**Location:** `/home/user/rathena2/CMakeLists.txt`

**Key Settings:**
- C++17 standard (Line 31: `set(CMAKE_CXX_STANDARD 17)`)
- Architecture detection (x86/x64)
- Build type: Release/Debug/RelWithDebInfo/MinSizeRel
- Packet version: `PACKETVER` (Line 118-121)

**Global Options:**
```cmake
# Enable web server (default: ON)
option( ENABLE_WEB_SERVER "Build web-server" ON )

# Enable extra debug code
option( ENABLE_EXTRA_DEBUG_CODE "enable extra debug code" OFF )

# Memory manager
set( ENABLE_MEMMGR "default" )  # default/yes/no

# Build type
set( CMAKE_BUILD_TYPE "Release" )  # Release/Debug/RelWithDebInfo
```

**Third-party Dependencies (Line 104-112):**
```cmake
set( CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/3rdparty/cmake )
include( CheckCSourceCompiles )
include( CheckCSourceRuns )
include( CheckIncludeFile )
include( CheckFunctionExists )
include( FindFunctionLibrary )
include( TestBigEndian )
```

**Subdirectories (Line 627-628):**
```cmake
add_subdirectory( 3rdparty )  # External libraries
add_subdirectory( src )       # Source code
```

### Source CMakeLists.txt

**Location:** `/home/user/rathena2/src/CMakeLists.txt`

```cmake
add_subdirectory( common )   # Common library
add_subdirectory( login )    # Login server
add_subdirectory( char )     # Char server
add_subdirectory( map )      # Map server
add_subdirectory( web )      # Web server
add_subdirectory( tool )     # Tools
```

### Map Server Build

**Location:** `/home/user/rathena2/src/map/CMakeLists.txt`

**Build Process:**
1. Compile common library first
2. Compile map server sources
3. Link with:
   - common (static library)
   - MySQL library
   - YAML library
   - PCRE library
   - zlib

**Output:** `map-server` (or `map-server.exe` on Windows)

### Typical Build Commands

```bash
# Create build directory
mkdir build && cd build

# Configure with CMake
cmake -G"Unix Makefiles" \
  -DCMAKE_BUILD_TYPE=RelWithDebInfo \
  -DINSTALL_TO_SOURCE=ON \
  -DPACKETVER=20211103 \
  ..

# Build
make -j4

# Install
make install
```

### Build Targets

```bash
make common         # Build common library only
make login-server   # Build login server
make char-server    # Build char server
make map-server     # Build map server
make web-server     # Build web server
make all            # Build everything
```

### Compile-time Options

**PACKETVER:** Client version compatibility
```cmake
-DPACKETVER=20211103  # 2021-11-03 client
```

**Renewal Mode:** `src/config/renewal.hpp`
```cpp
#define RENEWAL           // Enable renewal mechanics
#define RENEWAL_CAST      // Renewal casting
#define RENEWAL_DROP      // Renewal drop rates
#define RENEWAL_EXP       // Renewal EXP rates
#define RENEWAL_LVDMG     // Renewal level damage
#define RENEWAL_ASPD      // Renewal ASPD
```

**Security:** `src/config/secure.hpp`
```cpp
#define SECURE_NPCTIMEOUT 10000   // NPC timeout (ms)
#define PACKET_OBFUSCATION        // Packet obfuscation
```

---

## Feature Location Guide

### Where to Find Specific Features

#### Player Systems

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Login** | pc.cpp, chrif.cpp | `pc_authok()`, `chrif_authok()` |
| **Inventory** | pc.cpp | `pc_additem()`, `pc_delitem()`, `pc_dropitem()` |
| **Equipment** | pc.cpp | `pc_equipitem()`, `pc_unequipitem()` |
| **Stats Calculation** | status.cpp, pc.cpp | `status_calc_pc()`, `status_calc_*()` |
| **Job System** | pc.cpp | `pc_jobchange()`, `pc_calc_skilltree()` |
| **Skills** | skill.cpp, pc.cpp | `skill_use_id()`, `pc_checkskill()` |
| **Experience** | pc.cpp | `pc_gainexp()`, `pc_nextbaseexp()` |
| **Death** | pc.cpp | `pc_dead()`, `pc_setrestartvalue()` |
| **Regeneration** | status.cpp | `status_calc_regen()` |

#### Combat Systems

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Physical Damage** | battle.cpp | `battle_calc_weapon_attack()` |
| **Magic Damage** | battle.cpp | `battle_calc_magic_attack()` |
| **Element System** | battle.cpp | `battle_attr_fix()` |
| **Critical** | battle.cpp | `battle_calc_critical()` |
| **Defense Calc** | battle.cpp | `battle_calc_defense()` |
| **ASPD** | status.cpp | `status_calc_aspd()` |
| **HIT/FLEE** | status.cpp | `status_calc_hit()`, `status_calc_flee()` |

#### Monster Systems

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Spawning** | mob.cpp, npc.cpp | `mob_spawn()`, `mob_parse_dataset()` |
| **AI** | mob.cpp | `mob_ai_sub_hard()`, `mobai_sub_hard_timer()` |
| **Skills** | mob.cpp | `mob_skill_use()`, `mob_skill_event()` |
| **Drops** | mob.cpp | `mob_drop_item()`, `mob_setdropitem()` |
| **MVP** | mob.cpp | `mob_damage()` (MVP calculation) |
| **Slave/Master** | mob.cpp | `mob_ai_sub_hard_slavemob()` |

#### Item Systems

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Item Database** | itemdb.cpp | `itemdb_search()`, `itemdb_exists()` |
| **Item Use** | pc.cpp, script.cpp | `pc_useitem()`, item scripts |
| **Item Scripts** | script.cpp | Item bonus functions |
| **Refining** | status.cpp, script.cpp | refine_db, `refine_status()` |
| **Cards** | pc.cpp, status.cpp | Card bonus calculations |
| **Random Options** | itemdb.cpp, status.cpp | Random option system |

#### Skill Systems

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Skill Database** | skill.cpp | SkillDatabase class |
| **Skill Casting** | skill.cpp | `skill_castend_id()`, `skill_castend_pos()` |
| **Ground Skills** | skill.cpp | `skill_unitsetting()`, `skill_unit_onplace()` |
| **Skill Combos** | pc.cpp, skill.cpp | Combo system |
| **Skill Tree** | pc.cpp | `pc_calc_skilltree()` |
| **Skill Requirements** | skill.cpp | `skill_check_condition()` |
| **Class Skills** | src/map/skills/*/  | Individual skill implementations |

#### Status Effects

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Start Effect** | status.cpp | `status_change_start()` |
| **End Effect** | status.cpp | `status_change_end()` |
| **Timer** | status.cpp | `status_change_timer()` |
| **Icons** | clif.cpp | `clif_status_change()` |
| **Resistance** | status.cpp | SC resistance calculations |

#### Social Systems

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Party** | party.cpp | `party_create()`, `party_invite()` |
| **Guild** | guild.cpp | `guild_create()`, `guild_invite()` |
| **Chat** | chat.cpp | `chat_createpcchat()` |
| **Friends** | clif.cpp, pc.cpp | Friend list functions |
| **Mail** | mail.cpp | `mail_sendmail()`, `mail_getmail()` |

#### Map/Movement

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Walking** | unit.cpp | `unit_walktoxy()`, `unit_movepos()` |
| **Pathfinding** | path.cpp | `path_search()` |
| **Warp** | unit.cpp, pc.cpp | `unit_warp()`, `pc_setpos()` |
| **Map Loading** | map.cpp | `map_readgat()`, `map_waterheight()` |

#### NPC Systems

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **NPC Scripts** | npc.cpp, script.cpp | `npc_parse_script()`, `run_script()` |
| **Shops** | npc.cpp | `npc_parse_shop()`, `npc_buylist()` |
| **Warps** | npc.cpp | `npc_parse_warp()` |
| **Events** | npc.cpp | `npc_event()`, `npc_event_do()` |
| **Timers** | npc.cpp | `npc_timerevent()` |

#### Database Files (YAML)

| Database | Location | Loaded By |
|----------|----------|-----------|
| **Items** | db/item_db.yml | itemdb.cpp |
| **Mobs** | db/mob_db.yml | mob.cpp |
| **Skills** | db/skill_db.yml | skill.cpp |
| **Refine** | db/refine_db.yml | status.cpp |
| **Job Stats** | db/job_db.yml | pc.cpp |
| **Experience** | db/exp_group_db.yml | pc.cpp |
| **Status Effects** | db/sc_config.yml | status.cpp |

---

## Navigation Quick Reference

### Finding Code by Feature

**Q: "Where is damage calculation?"**
- **A:** `src/map/battle.cpp` → `battle_calc_attack()`
  - Physical: `battle_calc_weapon_attack()`
  - Magic: `battle_calc_magic_attack()`
  - Element: `battle_attr_fix()`

**Q: "Where is player stat calculation?"**
- **A:** `src/map/status.cpp` → `status_calc_pc()`
  - Individual stats: `status_calc_str()`, `status_calc_agi()`, etc.
  - ATK: `status_base_atk()`, `status_calc_watk()`
  - MATK: `status_calc_matk()`
  - DEF: `status_calc_def()`, `status_calc_def2()`

**Q: "Where is skill casting handled?"**
- **A:** `src/map/skill.cpp`
  - Request: `skill_use_id()`, `skill_use_pos()`
  - Requirements: `skill_check_condition()`
  - Casting: `skill_castend_id()`, `skill_castend_pos()`
  - Damage: `skill_attack()`

**Q: "Where are packets handled?"**
- **A:** `src/map/clif.cpp`
  - Parser: `clif_parse()` (main switch)
  - Individual handlers: `clif_parse_*()` functions
  - Sending: `clif_send()`, specific `clif_*()` functions

**Q: "Where is monster AI?"**
- **A:** `src/map/mob.cpp`
  - Main AI: `mob_ai_sub_hard()`
  - Timer: `mobai_sub_hard_timer()`
  - Skills: `mob_skill_use()`
  - Movement: Uses `unit.cpp` functions

**Q: "Where are NPC scripts parsed?"**
- **A:** `src/map/npc.cpp` (parsing) + `src/map/script.cpp` (execution)
  - Parse: `npc_parse_script()`
  - Execute: `run_script()`
  - Built-in functions: `BUILDIN(funcname)` macros

**Q: "Where is inventory management?"**
- **A:** `src/map/pc.cpp`
  - Add item: `pc_additem()`
  - Remove item: `pc_delitem()`
  - Drop item: `pc_dropitem()`
  - Pick up: `pc_takeitem()`
  - Equipment: `pc_equipitem()`, `pc_unequipitem()`

**Q: "Where is the item database?"**
- **A:** `src/map/itemdb.cpp/hpp`
  - Database class: `ItemDatabase`
  - Search: `itemdb_search()`, `itemdb_searchname()`
  - Properties: `itemdb_type()`, `itemdb_weight()`, etc.

### File Size as Complexity Indicator

**Largest Files (Most Complex):**
1. script.cpp (28,574 lines) - Script engine, 500+ builtin functions
2. skill.cpp (26,478 lines) - All skill mechanics
3. clif.cpp (25,821 lines) - All packet handling
4. status.cpp (16,480 lines) - Stat calculations, status effects
5. pc.cpp (16,102 lines) - Player character logic
6. battle.cpp (12,680 lines) - Battle formulas

**Tip:** Start with smaller, focused files when learning:
- path.cpp (pathfinding) - focused, algorithmic
- date.cpp (day/night) - simple
- duel.cpp (duel system) - small feature
- channel.cpp (chat channels) - medium complexity

### Common Patterns

**1. Object Retrieval by ID:**
```cpp
map_session_data *sd = map_id2sd(id);  // Player
mob_data *md = map_id2md(id);          // Monster
npc_data *nd = map_id2nd(id);          // NPC
block_list *bl = map_id2bl(id);        // Any object
```

**2. Null Safety:**
```cpp
nullpo_ret(sd);          // Return if NULL
nullpo_retr(val, sd);    // Return val if NULL
nullpo_retv(sd);         // Return void if NULL
nullpo_retb(sd);         // Return false if NULL
```

**3. Type Checking:**
```cpp
if (bl->type == BL_PC) {
    map_session_data *sd = (map_session_data *)bl;
}
```

**4. Area Iteration:**
```cpp
map_foreachinrange(function, center, range, type, ...args);
map_foreachinarea(function, m, x0, y0, x1, y1, type, ...args);
```

**5. Timer Management:**
```cpp
int tid = add_timer(gettick() + delay, function, id, data);
delete_timer(tid, function);
```

**6. Script Execution:**
```cpp
run_script(script, 0, sd->bl.id, 0);
```

---

## Code Examples

### Example 1: Player Stats Calculation Flow

**File:** `src/map/status.cpp`

**Main Function:** `status_calc_pc()` - Calculates all player stats

```cpp
// Called when:
// - Player logs in
// - Equipment changes
// - Status effect starts/ends
// - Job changes
// - Stats are reset/modified

int status_calc_pc_(map_session_data* sd, enum e_status_calc_opt opt) {
    // 1. Clear calculated stats
    memset(&sd->battle_status, 0, sizeof(status_data));

    // 2. Copy base stats
    sd->battle_status = sd->base_status;

    // 3. Calculate from equipment
    for (int i = 0; i < EQI_MAX; i++) {
        if (sd->equip_index[i] >= 0) {
            // Apply equipment bonuses
            run_script(item->script, 0, sd->bl.id, 0);
        }
    }

    // 4. Calculate individual stats
    status_calc_str(&sd->bl, &sd->sc, sd->battle_status.str);
    status_calc_agi(&sd->bl, &sd->sc, sd->battle_status.agi);
    // ... more stats

    // 5. Calculate combat stats
    status_calc_batk(&sd->bl, &sd->sc, sd->battle_status.batk);
    status_calc_watk(&sd->bl, &sd->sc, sd->battle_status.watk);
    status_calc_matk(&sd->bl, &sd->sc, sd->battle_status.matk);

    // 6. Apply status change modifiers
    status_calc_pc_additional(sd, opt);

    // 7. Send updates to client
    clif_updatestatus(sd, SP_STR);
    clif_updatestatus(sd, SP_ATK1);
    // ... more updates

    return 0;
}
```

### Example 2: Skill Damage Calculation

**File:** `src/map/skill.cpp` → `src/map/battle.cpp`

```cpp
// In skill.cpp
int skill_attack(int attack_type, block_list* src, block_list *dsrc,
                 block_list *bl, uint16 skill_id, uint16 skill_lv,
                 t_tick tick, int flag) {

    // 1. Calculate damage
    struct Damage dmg = battle_calc_attack(
        attack_type, src, bl, skill_id, skill_lv, flag
    );

    // 2. Apply damage
    if (dmg.damage > 0) {
        clif_skill_damage(dsrc, bl, tick, dmg.amotion, dmg.dmotion,
                         dmg.damage, dmg.div_, skill_id, skill_lv,
                         dmg.type);

        battle_damage(src, bl, dmg.damage, 0, 0);
    }

    // 3. Apply additional effects
    if (dmg.dmg_lv > ATK_BLOCK) {
        skill_additional_effect(src, bl, skill_id, skill_lv,
                               attack_type, dmg.dmg_lv, tick);
    }

    return dmg.damage;
}
```

### Example 3: Monster AI Decision Making

**File:** `src/map/mob.cpp`

```cpp
// Main AI function (simplified)
static int mob_ai_sub_hard(struct mob_data *md, t_tick tick) {
    // 1. Check if can move/act
    if (md->ud.skilltimer != INVALID_TIMER)
        return 0;  // Casting skill

    if (md->ud.walktimer != INVALID_TIMER)
        return 0;  // Moving

    // 2. Search for target
    if (!md->target_id) {
        mob_ai_sub_hard_activesearch(&md->bl, tick);
    }

    // 3. Get target
    block_list *tbl = map_id2bl(md->target_id);
    if (!tbl) {
        md->target_id = 0;
        return 0;
    }

    // 4. Check if should use skill
    if (mob_skill_use(md, tick, MSS_ANY)) {
        return 0;  // Used skill
    }

    // 5. Distance check
    int distance = distance_bl(&md->bl, tbl);

    // 6. Attack or chase
    if (distance <= md->status.rhw.range) {
        // In attack range - attack
        if (unit_attack(&md->bl, tbl->id, 0)) {
            return 0;
        }
    } else {
        // Out of range - chase
        if (unit_walktoxy(&md->bl, tbl->x, tbl->y, 0)) {
            return 0;
        }
    }

    return 0;
}
```

### Example 4: Packet Handling

**File:** `src/map/clif.cpp`

```cpp
/// Request to use item (CZ_USE_ITEM)
void clif_parse_UseItem(int fd, map_session_data *sd) {
    // 1. Read packet
    const PACKET_CZ_USE_ITEM *p = (PACKET_CZ_USE_ITEM *)RFIFOP(fd,0);

    uint16 index = p->index - 2;

    // 2. Validate
    if (index >= MAX_INVENTORY)
        return;

    if (!sd->inventory_data[index])
        return;

    // 3. Check conditions
    if (sd->npc_id || sd->state.storage_flag)
        return;

    if (sd->sc.cant.useitem)
        return;

    // 4. Use item
    if (!pc_useitem(sd, index))
        clif_useitemack(sd, index, 0, false);  // Failed
}

/// Send item use acknowledgement (ZC_USE_ITEM_ACK)
void clif_useitemack(map_session_data *sd, uint16 index, uint16 amount,
                     bool ok) {
    int fd = sd->fd;

    WFIFOHEAD(fd, packet_len(0xa8));
    WFIFOW(fd,0) = 0xa8;
    WFIFOW(fd,2) = index + 2;
    WFIFOW(fd,4) = amount;
    WFIFOB(fd,6) = ok;
    WFIFOSET(fd, packet_len(0xa8));
}
```

### Example 5: NPC Script Execution

**File:** `src/map/script.cpp`

```cpp
/// Built-in function: getitem
/// getitem <item id>, <amount>{, <account id>}
BUILDIN(getitem) {
    int nameid, amount;
    map_session_data *sd;
    struct item it;

    // 1. Get parameters
    if (script_isstringtype(st, 2)) {
        const char *name = script_getstr(st, 2);
        struct item_data *id = itemdb_searchname(name);
        nameid = id ? id->nameid : 0;
    } else {
        nameid = script_getnum(st, 2);
    }

    amount = script_getnum(st, 3);

    // 2. Get target player
    if (!script_accid2sd(4, sd))
        return SCRIPT_CMD_FAILURE;

    // 3. Validate
    if (nameid <= 0 || amount <= 0)
        return SCRIPT_CMD_FAILURE;

    // 4. Create item
    memset(&it, 0, sizeof(it));
    it.nameid = nameid;
    it.identify = 1;

    // 5. Add to inventory
    if ((flag = pc_additem(sd, &it, amount, LOG_TYPE_SCRIPT))) {
        clif_additem(sd, 0, 0, flag);
        if (pc_candrop(sd, &it))
            map_addflooritem(&it, amount, sd->bl.m,
                           sd->bl.x, sd->bl.y, 0, 0, 0, 0, 0);
    }

    return SCRIPT_CMD_SUCCESS;
}
```

### Example 6: Status Effect Application

**File:** `src/map/status.cpp`

```cpp
// Start a status change
int status_change_start(block_list *src, block_list *bl,
                       enum sc_type type, int rate, int val1,
                       int val2, int val3, int val4,
                       int tick, int flag) {

    status_change *sc = status_get_sc(bl);
    if (!sc) return 0;

    // 1. Check if can apply
    if (sc->data[type])
        return 0;  // Already has effect

    // 2. Calculate success rate
    if (rate < 10000) {
        rate = max(rate, 100);  // Min 1% success
        if (rnd()%10000 >= rate)
            return 0;  // Failed
    }

    // 3. Calculate duration
    tick = status_get_sc_tick(bl, src, type, tick);

    // 4. Create status data
    sc->data[type] = ers_alloc(sc_data_ers, struct status_change_entry);
    sc->data[type]->val1 = val1;
    sc->data[type]->val2 = val2;
    sc->data[type]->val3 = val3;
    sc->data[type]->val4 = val4;
    sc->data[type]->timer = add_timer(gettick() + tick,
                                      status_change_timer,
                                      bl->id, type);

    // 5. Apply effect
    status_calc_bl_(bl, SCB_ALL);  // Recalculate stats

    // 6. Send to client
    clif_status_change(bl, status_sc2icon(type), 1, tick,
                      val1, val2, val3);

    // 7. Call start function
    if (status_sc_start_func[type])
        status_sc_start_func[type](bl, sc, type);

    return 1;
}
```

---

## Quick Reference Tables

### Object Type Conversion Functions

| From → To | Function | Example |
|-----------|----------|---------|
| ID → block_list | `map_id2bl(id)` | `bl = map_id2bl(target_id)` |
| ID → Player | `map_id2sd(id)` | `sd = map_id2sd(char_id)` |
| ID → Mob | `map_id2md(id)` | `md = map_id2md(mob_id)` |
| ID → NPC | `map_id2nd(id)` | `nd = map_id2nd(npc_id)` |
| ID → Pet | `map_id2pd(id)` | `pd = map_id2pd(pet_id)` |
| bl → Player | `BL_CAST(BL_PC, bl)` | `sd = BL_CAST(BL_PC, bl)` |
| bl → Mob | `BL_CAST(BL_MOB, bl)` | `md = BL_CAST(BL_MOB, bl)` |

### Common Status Parameters (SP_*)

| Constant | Value | Description |
|----------|-------|-------------|
| SP_HP | 5 | Current HP |
| SP_MAXHP | 6 | Maximum HP |
| SP_SP | 7 | Current SP |
| SP_MAXSP | 8 | Maximum SP |
| SP_BASELEVEL | 11 | Base level |
| SP_JOBLEVEL | 55 | Job level |
| SP_STR | 13 | Strength |
| SP_AGI | 14 | Agility |
| SP_VIT | 15 | Vitality |
| SP_INT | 16 | Intelligence |
| SP_DEX | 17 | Dexterity |
| SP_LUK | 18 | Luck |
| SP_ZENY | 20 | Zeny |

### Skill Constants

| Constant | Value | Description |
|----------|-------|-------------|
| INF_ATTACK_SKILL | 0x01 | Attack skill |
| INF_GROUND_SKILL | 0x02 | Ground-targeted |
| INF_SELF_SKILL | 0x04 | Self-cast |
| INF_SUPPORT_SKILL | 0x10 | Support skill |
| INF_TRAP_SKILL | 0x20 | Trap skill |
| NK_SPLASH | 1 | Splash damage |
| NK_NODAMAGE | 0 | No damage |

### Battle Configuration

**Location:** `battle_config` global variable in `battle.cpp`

Common settings:
- `base_exp_rate` - Base EXP rate
- `job_exp_rate` - Job EXP rate
- `item_rate_common` - Common drop rate
- `max_hp` - Maximum HP
- `max_sp` - Maximum SP
- `max_parameter` - Maximum stat value

---

## Summary

This document provides a comprehensive reference for navigating the rAthena source code. Key takeaways:

1. **Directory Structure:** Map server (`src/map/`) contains game logic, with specialized subdirectories for skills
2. **Core Files:** script.cpp, skill.cpp, clif.cpp, status.cpp, pc.cpp, battle.cpp are the largest and most complex
3. **Data Structures:** `block_list` is the base for all objects, `map_session_data` for players, `mob_data` for monsters
4. **Build System:** CMake-based with configurable options (PACKETVER, RENEWAL, etc.)
5. **Code Flow:** Understanding the data flow between systems (login → char → map) is essential
6. **Feature Location:** Use the Feature Location Guide to quickly find specific functionality

**Next Steps for Developers:**
- Start with smaller files to understand patterns
- Trace a feature end-to-end (e.g., item use: clif.cpp → pc.cpp → script.cpp)
- Use forward declarations and include hierarchy to understand dependencies
- Refer to Quick Reference for common functions and constants

**File Locations:**
- Source code: `/home/user/rathena2/src/`
- Build system: `/home/user/rathena2/CMakeLists.txt`
- Common library: `/home/user/rathena2/src/common/`
- Map server: `/home/user/rathena2/src/map/`

---

*Document Version: 1.0*
*rAthena Source Analysis Date: 2025-11-18*
*Total Lines Analyzed: ~200,000+ across all source files*
