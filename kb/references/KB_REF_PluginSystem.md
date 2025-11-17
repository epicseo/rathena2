---
kb_id: KB_REF_024
title: "rAthena Customization System (src/custom/)"
category: Source Code
keywords: [custom, customization, atcommand, script_commands, ACMD_FUNC, BUILDIN_FUNC, inc_files, modular_development, source_modifications]
related_files: [
  "src/custom/atcommand.inc",
  "src/custom/atcommand_def.inc",
  "src/custom/script.inc",
  "src/custom/script_def.inc",
  "src/custom/defines_pre.hpp",
  "src/custom/defines_post.hpp",
  "src/custom/battle_config_init.inc",
  "src/custom/battle_config_struct.inc"
]
difficulty: intermediate
use_case: "Adding custom features without modifying core source files"
version: rAthena 2024
last_updated: 2024-01-15
---

# rAthena Customization System (src/custom/)

## Quick Reference

### **Custom Atcommand Template**
```cpp
// In src/custom/atcommand.inc

ACMD_FUNC(mycommand)
{
    clif_displaymessage(fd, "Hello from custom command!");
    clif_specialeffect(&sd->bl, EF_HEARTCASTING, AREA);
    return 0;
}
```

### **Registration**
```cpp
// In src/custom/atcommand_def.inc
ACMD_DEF(mycommand),
```

### **Custom Script Command Template**
```cpp
// In src/custom/script.inc

BUILDIN_FUNC(customheal)
{
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) return 1;

    int amount = script_getnum(st, 2);
    pc_heal(sd, amount, 0, 0);

    script_pushint(st, 1);
    return 0;
}
```

### **Registration**
```cpp
// In src/custom/script_def.inc
BUILDIN_DEF(customheal, "i"),
```

---

## Table of Contents
1. [System Overview](#system-overview)
2. [Custom Directory Structure](#custom-directory-structure)
3. [Custom Atcommands](#custom-atcommands)
4. [Custom Script Commands](#custom-script-commands)
5. [Custom Defines](#custom-defines)
6. [Custom Battle Config](#custom-battle-config)
7. [Complete Examples](#complete-examples)
8. [Best Practices](#best-practices)
9. [Compilation](#compilation)
10. [Core Modifications vs Custom](#core-modifications-vs-custom)

---

## System Overview

### **What is src/custom/?**

rAthena's customization system allows you to add custom features **without modifying core source files**. All customizations go in `src/custom/` directory and are **included at compile time**.

**Benefits**:
- ✅ **Git-safe**: Custom code won't conflict with upstream updates
- ✅ **Modular**: Easy to enable/disable features
- ✅ **Organized**: All custom code in one location
- ✅ **Clean**: No need to hunt through core files for your changes

**When to use**:
- Adding new atcommands (@mycommand)
- Adding new script commands (customheal)
- Adding new constants/defines
- Adding new battle config options

**When NOT to use**:
- Modifying existing game mechanics (requires core edits)
- Changing damage formulas (edit battle.cpp directly)
- Altering existing skill behavior (edit skill.cpp directly)

---

## Custom Directory Structure

### **File Layout**
```
src/custom/
├── atcommand.inc              # Custom atcommand implementations
├── atcommand_def.inc          # Custom atcommand registrations
├── script.inc                 # Custom script command implementations
├── script_def.inc             # Custom script command registrations
├── defines_pre.hpp            # Custom defines (loaded BEFORE core)
├── defines_post.hpp           # Custom defines (loaded AFTER core)
├── battle_config_init.inc     # Custom battle config initialization
└── battle_config_struct.inc   # Custom battle config structure fields
```

### **Include Order**

**defines_pre.hpp** → **Core Headers** → **defines_post.hpp**

```cpp
// Compilation order:
1. src/custom/defines_pre.hpp       // Your defines loaded first
2. src/map/pc.hpp                   // Core headers
3. src/custom/defines_post.hpp      // Your defines override core
```

**Use Case**:
- `defines_pre.hpp`: Add new constants that core might need
- `defines_post.hpp`: Override existing constants (use carefully!)

---

## Custom Atcommands

### **Structure**

**Implementation** (atcommand.inc):
```cpp
ACMD_FUNC(command_name)
{
    // sd  = struct map_session_data* (player who used command)
    // fd  = file descriptor (for sending messages)

    // Your code here

    return 0;  // 0 = success, -1 = failure
}
```

**Registration** (atcommand_def.inc):
```cpp
// Basic
ACMD_DEF(command_name),

// With restriction
ACMD_DEFR(command_name, restriction),

// With alias
ACMD_DEF2("alias", command_name),
```

**Restrictions**:
- `1` - Restrict usage in console
- `2` - Restrict usage in script commands
- `3` - Restrict both

---

### **Example 1: Simple Atcommand**

**atcommand.inc**:
```cpp
/**
 * @heal - Fully heal HP/SP with special effect
 * Usage: @heal
 */
ACMD_FUNC(heal)
{
    // Heal player to full
    pc_heal(sd, sd->battle_status.max_hp, sd->battle_status.max_sp, 1);

    // Show effect
    clif_specialeffect(&sd->bl, EF_HEAL, AREA);

    // Send message
    clif_displaymessage(fd, "You have been fully healed!");

    return 0;
}
```

**atcommand_def.inc**:
```cpp
ACMD_DEF(heal),
```

**Usage in-game**:
```
@heal
```

---

### **Example 2: Atcommand with Parameters**

**atcommand.inc**:
```cpp
/**
 * @givezeny <amount>
 * Give zeny to yourself (for testing)
 * Usage: @givezeny 1000000
 */
ACMD_FUNC(givezeny)
{
    int amount;

    // Check if parameter provided
    if (!message || !*message) {
        clif_displaymessage(fd, "Usage: @givezeny <amount>");
        return -1;
    }

    // Parse amount
    amount = atoi(message);

    // Validate
    if (amount <= 0) {
        clif_displaymessage(fd, "Amount must be positive!");
        return -1;
    }

    if (amount > MAX_ZENY - sd->status.zeny) {
        clif_displaymessage(fd, "Amount too large! Zeny limit exceeded.");
        return -1;
    }

    // Give zeny
    pc_payzeny(sd, -amount, LOG_TYPE_COMMAND, NULL);

    // Feedback
    sprintf(atcmd_output, "Added %d Zeny. Current: %d", amount, sd->status.zeny);
    clif_displaymessage(fd, atcmd_output);

    return 0;
}
```

**atcommand_def.inc**:
```cpp
ACMD_DEF(givezeny),
```

---

### **Example 3: Atcommand Targeting Other Players**

**atcommand.inc**:
```cpp
/**
 * @buffplayer <player_name>
 * Give blessing to target player
 * Usage: @buffplayer PlayerName
 */
ACMD_FUNC(buffplayer)
{
    struct map_session_data *target_sd;
    char target_name[NAME_LENGTH];

    // Parse target name
    if (!message || !*message) {
        clif_displaymessage(fd, "Usage: @buffplayer <player_name>");
        return -1;
    }

    // Extract name
    if (sscanf(message, "%23s", target_name) < 1) {
        clif_displaymessage(fd, "Invalid player name!");
        return -1;
    }

    // Find target
    target_sd = map->nick2sd(target_name, false);
    if (!target_sd) {
        clif_displaymessage(fd, "Player not found!");
        return -1;
    }

    // Apply blessing (SC_BLESSING, 100% chance, level 10, 60 seconds)
    sc_start(NULL, &target_sd->bl, SC_BLESSING, 100, 10, 60000);

    // Feedback
    sprintf(atcmd_output, "Blessed player '%s'!", target_sd->status.name);
    clif_displaymessage(fd, atcmd_output);

    sprintf(atcmd_output, "You have been blessed by GM %s!", sd->status.name);
    clif_displaymessage(target_sd->fd, atcmd_output);

    return 0;
}
```

**atcommand_def.inc**:
```cpp
ACMD_DEF(buffplayer),
```

---

## Custom Script Commands

### **Structure**

**Implementation** (script.inc):
```cpp
BUILDIN_FUNC(command_name)
{
    // st = struct script_state* (script execution state)

    // Get parameters with script_getnum(st, index) or script_getstr(st, index)

    // Your code here

    // Return value (optional)
    script_pushint(st, return_value);

    return 0;  // 0 = success, 1 = failure
}
```

**Registration** (script_def.inc):
```cpp
// Basic
BUILDIN_DEF(command_name, "argument_types"),

// With alias
BUILDIN_DEF2(command_name, "alias", "argument_types"),
```

**Argument Types**:
- `i` - Integer
- `s` - String
- `v` - Variable
- `l` - Label
- `r` - Reference (variable reference)
- `?` - Optional parameter (one)
- `*` - Optional parameters (multiple)
- `""` - No arguments

---

### **Example 1: Simple Script Command**

**script.inc**:
```cpp
/**
 * serveruptime()
 * Returns server uptime in seconds
 * @return: Uptime in seconds
 */
BUILDIN_FUNC(serveruptime)
{
    int uptime = (int)(time(NULL) - map->start_time);
    script_pushint(st, uptime);
    return 0;
}
```

**script_def.inc**:
```cpp
BUILDIN_DEF(serveruptime, ""),
```

**Usage in NPC**:
```c
.@uptime = serveruptime();
.@hours = .@uptime / 3600;
mes "Server has been online for " + .@hours + " hours.";
```

---

### **Example 2: Script Command with Parameters**

**script.inc**:
```cpp
/**
 * customheal(<hp_amount>, <sp_amount>, <show_effect>)
 * Heal player with custom amounts
 * @param hp_amount: HP to heal
 * @param sp_amount: SP to heal
 * @param show_effect: 1=show effect, 0=silent
 * @return: 1=success, 0=fail
 */
BUILDIN_FUNC(customheal)
{
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) {
        script_pushint(st, 0);
        return 1;
    }

    int hp_amount = script_getnum(st, 2);
    int sp_amount = script_getnum(st, 3);
    int show_effect = script_getnum(st, 4);

    // Heal player
    pc_heal(sd, hp_amount, sp_amount, show_effect ? 1 : 0);

    script_pushint(st, 1);
    return 0;
}
```

**script_def.inc**:
```cpp
BUILDIN_DEF(customheal, "iii"),  // 3 integers
```

**Usage**:
```c
customheal(500, 100, 1);  // Heal 500 HP, 100 SP, with effect
```

---

### **Example 3: Script Command with Optional Parameters**

**script.inc**:
```cpp
/**
 * givebonus(<type>, <value>{, <duration>})
 * Give temporary stat bonus
 * @param type: 1=STR, 2=AGI, 3=VIT, 4=INT, 5=DEX, 6=LUK
 * @param value: Bonus amount
 * @param duration: Duration in seconds (default 60)
 * @return: 1=success, 0=fail
 */
BUILDIN_FUNC(givebonus)
{
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) {
        script_pushint(st, 0);
        return 1;
    }

    int type = script_getnum(st, 2);
    int value = script_getnum(st, 3);
    int duration = script_hasdata(st, 4) ? script_getnum(st, 4) : 60;

    // Map type to status change
    int sc_type;
    switch(type) {
        case 1: sc_type = SC_INCSTR; break;
        case 2: sc_type = SC_INCAGI; break;
        case 3: sc_type = SC_INCVIT; break;
        case 4: sc_type = SC_INCINT; break;
        case 5: sc_type = SC_INCDEX; break;
        case 6: sc_type = SC_INCLUK; break;
        default:
            script_pushint(st, 0);
            return 0;
    }

    // Apply bonus
    sc_start(NULL, &sd->bl, (sc_type)sc_type, 100, value, duration * 1000);

    script_pushint(st, 1);
    return 0;
}
```

**script_def.inc**:
```cpp
BUILDIN_DEF(givebonus, "ii?"),  // 2 int, 1 optional int
```

**Usage**:
```c
givebonus(1, 10);       // +10 STR for 60 seconds
givebonus(2, 20, 300);  // +20 AGI for 300 seconds
```

---

### **Example 4: Script Command with String Parameters**

**script.inc**:
```cpp
/**
 * customannounce(<message>, <color>)
 * Send colored announcement to player
 * @param message: Message text
 * @param color: Color code (e.g., "0xFF0000" for red)
 * @return: 1
 */
BUILDIN_FUNC(customannounce)
{
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) return 1;

    const char *message = script_getstr(st, 2);
    const char *color = script_getstr(st, 3);

    // Parse color (simplified - real implementation would convert hex)
    unsigned long color_code = strtoul(color, NULL, 16);

    // Send announcement
    char output[CHAT_SIZE_MAX];
    snprintf(output, sizeof(output), "%s", message);
    clif->broadcast2(&sd->bl, output, (int)strlen(output) + 1, color_code,
                     0x190, 12, 0, 0, SELF);

    script_pushint(st, 1);
    return 0;
}
```

**script_def.inc**:
```cpp
BUILDIN_DEF(customannounce, "ss"),  // 2 strings
```

**Usage**:
```c
customannounce("Event starting soon!", "0xFF0000");  // Red text
```

---

## Custom Defines

### **defines_pre.hpp** - Load BEFORE core

**Use Cases**:
- New constants that don't exist in core
- New item IDs, mob IDs, skill IDs (if not in database)

**Example**:
```cpp
#ifndef CONFIG_CUSTOM_DEFINES_PRE_HPP
#define CONFIG_CUSTOM_DEFINES_PRE_HPP

/**
 * Custom Item IDs for special items
 */
#define ITEMID_CUSTOM_TICKET    50000
#define ITEMID_CUSTOM_COIN      50001
#define ITEMID_CUSTOM_BOX       50002

/**
 * Custom constants
 */
#define MAX_CUSTOM_STORAGE      600  // Custom storage limit
#define CUSTOM_EXP_RATE         100  // Custom exp multiplier

#endif /* CONFIG_CUSTOM_DEFINES_PRE_HPP */
```

---

### **defines_post.hpp** - Load AFTER core

**Use Cases**:
- Override existing core constants (DANGEROUS!)
- Add constants that depend on core definitions

**Example**:
```cpp
#ifndef CONFIG_CUSTOM_DEFINES_POST_HPP
#define CONFIG_CUSTOM_DEFINES_POST_HPP

/**
 * Override max party size
 * WARNING: This may break things! Test thoroughly!
 */
#ifdef MAX_PARTY
    #undef MAX_PARTY
    #define MAX_PARTY 24  // Increase from 12 to 24
#endif

/**
 * Custom status change constants
 */
#define SC_CUSTOM_BUFF    (SC_MAX + 1)
#define SC_CUSTOM_DEBUFF  (SC_MAX + 2)

#endif /* CONFIG_CUSTOM_DEFINES_POST_HPP */
```

**WARNING**: Overriding core constants can cause:
- Crashes
- Database mismatches
- Client-server desync
- Unpredictable behavior

Only override if you **fully understand** the consequences!

---

## Custom Battle Config

### **battle_config_struct.inc** - Add new config fields

**Example**:
```cpp
/**
 * Custom battle config fields
 * These will be added to struct battle_config
 */

int custom_exp_modifier;        // Custom exp rate modifier
int custom_drop_rate;           // Custom drop rate
int enable_custom_feature;      // 1=enable, 0=disable
int max_custom_summons;         // Max number of custom summons
```

---

### **battle_config_init.inc** - Initialize config values

**Example**:
```cpp
/**
 * Initialize custom battle config values
 * These are the DEFAULT values
 */

{ "custom_exp_modifier",            &battle_config.custom_exp_modifier,             100,    0,      1000    },
{ "custom_drop_rate",                &battle_config.custom_drop_rate,                100,    0,      10000   },
{ "enable_custom_feature",           &battle_config.enable_custom_feature,           1,      0,      1       },
{ "max_custom_summons",              &battle_config.max_custom_summons,              5,      1,      20      },

// Format: { "config_name", &variable, default, min, max }
```

---

### **Using Custom Battle Config**

**In conf/battle/custom.conf**:
```ini
//--------------------------------------------------------------
// Custom Battle Configuration
//--------------------------------------------------------------

// Custom exp modifier (100 = 1x, 200 = 2x)
custom_exp_modifier: 150

// Custom drop rate (100 = normal)
custom_drop_rate: 200

// Enable custom feature
enable_custom_feature: 1

// Max custom summons per player
max_custom_summons: 10
```

**In your C++ code**:
```cpp
// Access your custom config
int exp_gain = base_exp * battle_config.custom_exp_modifier / 100;

if (battle_config.enable_custom_feature) {
    // Do custom feature logic
}

if (summon_count >= battle_config.max_custom_summons) {
    // Max summons reached
}
```

---

## Complete Examples

### **Example 1: Custom Currency System**

**1. defines_pre.hpp**:
```cpp
#define ITEMID_CUSTOM_CURRENCY  60000
#define MAX_CUSTOM_CURRENCY     1000000000
```

**2. script.inc**:
```cpp
/**
 * getcustomcurrency()
 * Get player's custom currency amount
 * @return: Currency amount
 */
BUILDIN_FUNC(getcustomcurrency)
{
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) {
        script_pushint(st, 0);
        return 1;
    }

    int amount = pc_search_inventory(sd, ITEMID_CUSTOM_CURRENCY);
    if (amount < 0) {
        script_pushint(st, 0);
    } else {
        script_pushint(st, sd->inventory.u.items_inventory[amount].amount);
    }

    return 0;
}

/**
 * addcustomcurrency(<amount>)
 * Add custom currency to player
 * @param amount: Amount to add
 * @return: 1=success, 0=fail
 */
BUILDIN_FUNC(addcustomcurrency)
{
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) {
        script_pushint(st, 0);
        return 1;
    }

    int amount = script_getnum(st, 2);

    if (amount <= 0 || amount > MAX_CUSTOM_CURRENCY) {
        script_pushint(st, 0);
        return 0;
    }

    struct item item_tmp;
    memset(&item_tmp, 0, sizeof(item_tmp));
    item_tmp.nameid = ITEMID_CUSTOM_CURRENCY;
    item_tmp.amount = amount;
    item_tmp.identify = 1;

    int result = pc_additem(sd, &item_tmp, amount, LOG_TYPE_SCRIPT);
    script_pushint(st, result == 0 ? 1 : 0);

    return 0;
}
```

**3. script_def.inc**:
```cpp
BUILDIN_DEF(getcustomcurrency, ""),
BUILDIN_DEF(addcustomcurrency, "i"),
```

**4. Usage in NPC**:
```c
prontera,150,150,4	script	Currency Exchanger	123,{
    mes "[Currency Exchanger]";
    mes "You have " + getcustomcurrency() + " custom currency.";
    mes "Would you like to exchange Zeny for currency?";
    next;

    if (select("Yes:No") == 2) close;

    mes "How much? (1,000 Zeny = 1 Currency)";
    input .@amount;

    if (.@amount <= 0 || Zeny < .@amount * 1000) {
        mes "Invalid amount or insufficient Zeny!";
        close;
    }

    Zeny -= .@amount * 1000;
    addcustomcurrency(.@amount);

    mes "Exchanged " + .@amount * 1000 + " Zeny for " + .@amount + " currency!";
    close;
}
```

---

### **Example 2: Custom Buff Command**

**atcommand.inc**:
```cpp
/**
 * @superbuff - Apply all stat buffs
 * Usage: @superbuff
 */
ACMD_FUNC(superbuff)
{
    const int duration = 600000;  // 10 minutes
    const int level = 10;

    // Apply all stat buffs
    sc_start(NULL, &sd->bl, SC_INCSTR, 100, level, duration);
    sc_start(NULL, &sd->bl, SC_INCAGI, 100, level, duration);
    sc_start(NULL, &sd->bl, SC_INCVIT, 100, level, duration);
    sc_start(NULL, &sd->bl, SC_INCINT, 100, level, duration);
    sc_start(NULL, &sd->bl, SC_INCDEX, 100, level, duration);
    sc_start(NULL, &sd->bl, SC_INCLUK, 100, level, duration);

    // Blessing, Agi Up, Increase Agi
    sc_start(NULL, &sd->bl, SC_BLESSING, 100, level, duration);
    sc_start(NULL, &sd->bl, SC_INCREASEAGI, 100, level, duration);

    // Visual effect
    clif_specialeffect(&sd->bl, EF_MAPPILLAR2, AREA);

    clif_displaymessage(fd, "Super buff applied for 10 minutes!");

    return 0;
}
```

**atcommand_def.inc**:
```cpp
ACMD_DEF(superbuff),
```

---

## Best Practices

### **1. Naming Conventions**

```cpp
// ✅ GOOD - Clear, descriptive names
ACMD_FUNC(resetcooldowns)
BUILDIN_FUNC(getpartyonlinecount)

// ❌ BAD - Vague, conflicts with core
ACMD_FUNC(reset)  // Too generic
BUILDIN_FUNC(get)  // What does it get?
```

---

### **2. Input Validation**

```cpp
// ✅ GOOD - Always validate
BUILDIN_FUNC(mycommand)
{
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) {
        script_pushint(st, 0);
        return 1;  // Failure
    }

    int amount = script_getnum(st, 2);
    if (amount <= 0 || amount > MAX_AMOUNT) {
        ShowError("mycommand: Invalid amount %d\n", amount);
        script_pushint(st, 0);
        return 0;
    }

    // Proceed...
}

// ❌ BAD - No validation
BUILDIN_FUNC(badcommand)
{
    struct map_session_data *sd = script_rid2sd(st);
    int amount = script_getnum(st, 2);
    // Crashes if sd is NULL or amount is invalid!
    pc_payzeny(sd, -amount, LOG_TYPE_SCRIPT, NULL);
}
```

---

### **3. Error Messages**

```cpp
// ✅ GOOD - Informative errors
if (!target_sd) {
    clif_displaymessage(fd, "Player not found. Please check the name.");
    return -1;
}

// ❌ BAD - Vague errors
if (!target_sd) {
    clif_displaymessage(fd, "Error!");
    return -1;
}
```

---

### **4. Documentation**

```cpp
// ✅ GOOD - Well documented
/**
 * customwarp(<map>, <x>, <y>, <save_location>)
 * Warp player to coordinates and optionally save as respawn point
 * @param map: Map name (string)
 * @param x: X coordinate
 * @param y: Y coordinate
 * @param save_location: 1=save as respawn, 0=don't save
 * @return: 1=success, 0=fail (invalid map, coords)
 */
BUILDIN_FUNC(customwarp) { /* ... */ }

// ❌ BAD - No documentation
BUILDIN_FUNC(warp2) { /* ... */ }
```

---

### **5. Memory Management**

```cpp
// ✅ GOOD - No memory leaks
BUILDIN_FUNC(getstring)
{
    const char *str = "Hello World";
    script_pushstr(st, aStrdup(str));  // Script engine will free this
    return 0;
}

// ❌ BAD - Memory leak
BUILDIN_FUNC(badgetstring)
{
    char *str = (char*)aMalloc(100);
    strcpy(str, "Hello");
    script_pushstr(st, str);  // Never freed if script doesn't use it!
    return 0;
}
```

---

## Compilation

### **Step 1: Add Your Code**

1. Edit `src/custom/atcommand.inc` or `src/custom/script.inc`
2. Add your implementation
3. Edit `src/custom/atcommand_def.inc` or `src/custom/script_def.inc`
4. Add your registration

### **Step 2: Compile**

**Linux (CMake)**:
```bash
cd /path/to/rathena
mkdir build && cd build
cmake ..
make -j$(nproc)
make install
```

**Linux (Configure)**:
```bash
cd /path/to/rathena
./configure
make clean
make -j$(nproc)
```

**Windows (Visual Studio)**:
1. Open `rathena-vs##.sln`
2. Build → Rebuild Solution
3. Copy executables from `build/bin/`

### **Step 3: Test**

1. **Start servers**:
```bash
./login-server &
./char-server &
./map-server
```

2. **Test atcommand**:
```
@mycommand
```

3. **Test script command** - Create test NPC:
```c
prontera,150,150,4	script	Test	123,{
    .@result = mycommand(100);
    mes "Result: " + .@result;
    close;
}
```

4. **Check console** for errors:
```
[Error]: script:mycommand: ...
[Error]: atcommand_mycommand: ...
```

---

## Core Modifications vs Custom

### **Use src/custom/ For**:

✅ **New atcommands** (@mycommand)
✅ **New script commands** (customheal)
✅ **New constants** (ITEMID_CUSTOM)
✅ **New battle config options**
✅ **Simple additions** that don't modify existing behavior

### **Edit Core Files For**:

⚠️ **Modifying existing commands** (change @heal behavior)
⚠️ **Changing game mechanics** (alter exp formula)
⚠️ **Modifying damage calculations** (battle.cpp)
⚠️ **Changing skill behavior** (skill.cpp)
⚠️ **Altering player stats** (pc.cpp)
⚠️ **Packet modifications** (clif.cpp)

### **Hybrid Approach Example**:

**Scenario**: Add custom damage bonus based on custom stat

**1. Add custom stat to defines_pre.hpp**:
```cpp
#define SP_CUSTOM_STAT  (SP_LAST_KNOWN + 1)
```

**2. Add script command in script.inc**:
```cpp
BUILDIN_FUNC(setcustomstat) {
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) return 1;

    int value = script_getnum(st, 2);
    sd->custom_stat = value;

    return 0;
}
```

**3. Modify core battle.cpp** (unavoidable):
```cpp
// In battle_calc_damage()
damage += sd->custom_stat * 10;  // +10 damage per custom stat point
```

This requires **both** custom code AND core modification.

---

## Troubleshooting

### **Common Errors**

**Error**: `undefined reference to 'buildin_mycommand'`
**Fix**: Add registration to `script_def.inc`

**Error**: `atcommand 'mycommand' not found`
**Fix**: Add registration to `atcommand_def.inc`

**Error**: `syntax error in atcommand.inc`
**Fix**: Check for missing semicolons, braces

**Error**: Server crashes when using command
**Fix**: Add null pointer checks, validate parameters

---

## Related References

- **Script Command Creation**: [KB_REF_ScriptCommandCreation.md]
- **Source Code Structure**: [KB_REF_SourceCodeStructure.md]
- **Best Practices**: [KB_REF_SourceCodeBestPractices.md]
- **Compilation**: [KB_REF_CompilationDebugging.md]

---

**End of KB_REF_024 - rAthena Customization System**
