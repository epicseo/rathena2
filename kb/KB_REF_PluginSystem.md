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
