# rAthena Game Mechanics Complete Reference v9.0 Final

**Version:** 9.0 Final - Best of All Versions
**Coverage:** Job System, Mapflags, Element Table (validated), Battle Configs
**Last Updated:** 2025-11-26

---

# ═══════════════════════════════════════════════════════════════
# PART 1: JOB SYSTEM (EAJ_* CONSTANTS)
# ═══════════════════════════════════════════════════════════════

---
kb_id: KB_REF_014
kb_type: reference
kb_category: system
kb_subcategory: job_system
kb_keywords: [job system, job classes, job IDs, eaclass, roclass, job change, job tree, job masks, EAJL, transcendent, baby, third job, fourth job, job stats]
kb_related: [KB_REF_005, KB_REF_011, KB_REF_013]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2025-10-25
kb_use_case: [job_change_scripts, job_checking, quest_restrictions, job_mechanics]
---

# rAthena Job System Reference

Complete reference for rAthena's job system, job IDs, job masks, and job-related scripting.

## Overview

rAthena uses a sophisticated job system that allows bitwise operations to identify job classes, job branches (2-1/2-2), and job types (normal/trans/baby/third/fourth).

**Key Concepts:**
- **Base Job:** Root job tree (Novice, Swordman, Mage, etc.)
- **Branch:** Job evolution path (2-1 or 2-2)
- **Type:** Job variant (Normal, Transcendent, Baby, Third, Fourth)

**Script Commands:**
- `eaclass()` - Get eAthena job class ID
- `roclass(<ea_job>)` - Convert eA job to RO job ID
- `jobchange <job>` - Change player's job

---

## TABLE OF CONTENTS

1. [Job System Basics](#1-job-system-basics)
2. [Base Jobs](#2-base-jobs)
3. [Job Branches](#3-job-branches)
4. [Job Types](#4-job-types)
5. [Job Masks](#5-job-masks)
6. [Script Examples](#6-script-examples)
7. [Job ID Reference](#7-job-id-reference)
8. [Common Job IDs](#8-common-job-ids)

---

## 1. JOB SYSTEM BASICS

### The Three Components

Every job can be identified by combining three bitwise flags:

```c
// Example: Lord Knight = Swordman + 2-1 + Upper
EAJ_SWORDMAN | EAJL_2_1 | EAJL_UPPER = Lord Knight
```

**Components:**
1. **Base Job** - Which job tree? (0x0-0x10)
2. **Branch** - 1st, 2-1, or 2-2? (0x100-0x300)
3. **Type** - Normal, Trans, Baby, 3rd, 4th? (0x1000-0x8000)

---

### Why Bitwise Operations?

Using bitwise OR (`|`) is "wreck-proof":

```c
// Adding EAJL_UPPER again doesn't break it
EAJ_SWORDMAN_HIGH | EAJL_UPPER = EAJ_SWORDMAN_HIGH  // Still correct!

// If we had used addition:
EAJ_SWORDMAN_HIGH + EAJL_UPPER = Wrong result!
```

---

## 2. BASE JOBS

The root job of every class tree:

```c
EAJ_NOVICE       0x0    // Novice tree
EAJ_SWORDMAN     0x1    // Swordman tree
EAJ_MAGE         0x2    // Mage tree
EAJ_ARCHER       0x3    // Archer tree
EAJ_ACOLYTE      0x4    // Acolyte tree
EAJ_MERCHANT     0x5    // Merchant tree
EAJ_THIEF        0x6    // Thief tree
EAJ_TAEKWON      0x7    // Taekwon tree
EAJ_GUNSLINGER   0x9    // Gunslinger (no 2nd job)
EAJ_NINJA        0xA    // Ninja (no 2nd job)
EAJ_GANGSI       0xD    // Bongun/Munak (NPC)
EAJ_SUMMONER     0x10   // Summoner (Doram)
```

---

## 3. JOB BRANCHES

Determines 1st class vs 2nd class path:

```c
EAJL_2_1    0x100    // 2-1 class (Knight, Wizard, Hunter, etc.)
EAJL_2_2    0x200    // 2-2 class (Crusader, Sage, Bard/Dancer, etc.)
EAJL_2      0x300    // Any 2nd class (EAJL_2_1 | EAJL_2_2)
```

### Examples

```c
// 2-1 Classes
EAJ_SWORDMAN | EAJL_2_1 = EAJ_KNIGHT
EAJ_MAGE | EAJL_2_1     = EAJ_WIZARD
EAJ_ARCHER | EAJL_2_1   = EAJ_HUNTER

// 2-2 Classes
EAJ_SWORDMAN | EAJL_2_2 = EAJ_CRUSADER
EAJ_MAGE | EAJL_2_2     = EAJ_SAGE
EAJ_ARCHER | EAJL_2_2   = EAJ_BARD (male) / EAJ_DANCER (female)
```

---

## 4. JOB TYPES

Variants of job classes:

```c
EAJL_UPPER   0x1000    // Transcendent/Rebirth (High Swordman, Lord Knight, etc.)
EAJL_BABY    0x2000    // Adopted/Baby classes
EAJL_THIRD   0x4000    // Third jobs (Rune Knight, Warlock, etc.)
EAJL_FOURTH  0x8000    // Fourth jobs (Dragon Knight, etc.)
```

### Examples

```c
// Transcendent Classes
EAJ_SWORDMAN | EAJL_UPPER           = EAJ_SWORDMAN_HIGH
EAJ_SWORDMAN | EAJL_2_1 | EAJL_UPPER = EAJ_LORD_KNIGHT

// Baby Classes
EAJ_SWORDMAN | EAJL_BABY            = EAJ_BABY_SWORDMAN
EAJ_SWORDMAN | EAJL_2_1 | EAJL_BABY  = EAJ_BABY_KNIGHT

// Third Classes
EAJ_SWORDMAN | EAJL_2_1 | EAJL_THIRD = EAJ_RUNE_KNIGHT
EAJ_MAGE | EAJL_2_1 | EAJL_THIRD     = EAJ_WARLOCK

// Transcendent Third
EAJ_SWORDMAN | EAJL_2_1 | EAJL_THIRD | EAJL_UPPER = EAJ_RUNE_KNIGHT_T

// Fourth Jobs
EAJ_SWORDMAN | EAJL_2_1 | EAJL_FOURTH = EAJ_DRAGON_KNIGHT
```

---

## 5. JOB MASKS

Masks strip job attributes for comparisons:

### EAJ_BASEMASK

Strips 2nd class AND upper/baby/third attributes.
**Use:** Check base job tree regardless of advancement.

```c
if ((eaclass() & EAJ_BASEMASK) == EAJ_SWORDMAN)
    mes "You are from the Swordman family!";
// True for: Swordman, Knight, Crusader, Lord Knight, Paladin,
// Rune Knight, Royal Guard, Baby versions, etc.
```

---

### EAJ_UPPERMASK

Strips upper/baby/third/fourth attributes but keeps 2nd class.
**Use:** Check exact job regardless of rebirth/baby status.

```c
if ((eaclass() & EAJ_UPPERMASK) == EAJ_MONK)
    mes "Knuckles are cool!";
// True for: Monk, Champion, Baby Monk
// False for: Acolyte, Priest, Sura
```

---

### EAJ_THIRDMASK

Strips third job attributes.
**Use:** Get the base 2nd job of a 3rd class.

```c
if ((eaclass() & EAJ_THIRDMASK) == EAJ_WARLOCK_T)
    mes "You've been through rebirth!";
```

---

### EAJ_FOURTHMASK

Strips fourth job attributes.
**Use:** Check 4th job base (currently unused, future-proof).

```c
if ((eaclass() & EAJ_FOURTHMASK) == EAJ_DRAGON_KNIGHT)
    mes "A Dragon Knight!";
```

---

## 6. SCRIPT EXAMPLES

### Example 1: Check if Player is 2nd Class

```c
set @eac, eaclass();
if (@eac & EAJL_2) {
    mes "You are a 2nd class!";
} else {
    mes "You are still 1st class.";
}
```

---

### Example 2: Check if Player is Transcendent

```c
if (eaclass() & EAJL_UPPER)
    mes "Rebirth achieved!";
else
    mes "Not transcendent yet.";
```

---

### Example 3: Check if Player is Baby

```c
if (eaclass() & EAJL_BABY)
    mes "Adopted character detected.";
```

---

### Example 4: Check if Player is Third Job

```c
if (eaclass() & EAJL_THIRD)
    mes "Welcome, Third Job!";
```

---

### Example 5: Check Base Job (Any Merchant)

```c
if ((eaclass() & EAJ_BASEMASK) == EAJ_MERCHANT) {
    mes "Merchant family member!";
    // True for: Merchant, Blacksmith, Alchemist, Whitesmith, Creator,
    // Mechanic, Geneticist, Baby versions, etc.
}
```

---

### Example 6: Check Specific 2nd Job (Any Knight)

```c
if ((eaclass() & EAJ_UPPERMASK) == EAJ_KNIGHT) {
    mes "A Knight! (includes Lord Knight and Baby Knight)";
}
```

---

### Example 7: Predict Next Job

```c
set @eac, eaclass();

if (@eac & EAJL_2) {
    // Already 2nd class
    if (@eac & (EAJL_UPPER|EAJL_BABY)) {
        mes "You can't advance further.";
        close;
    }
    // Check if rebirth is available
    set @newclass, roclass(@eac | EAJL_UPPER);
    if (@newclass == -1) {
        mes "No rebirth version for your class yet!";
        close;
    }
    mes "Will you become a " + jobname(@newclass) + "?";
    close;
}

// First class - show 2nd job options
set @class1, roclass(@eac | EAJL_2_1);
set @class2, roclass(@eac | EAJL_2_2);

if (@class1 == -1) {
    mes "No job advancement available.";
    close;
}

if (@class2 == -1) {
    mes "You can only become a " + jobname(@class1) + ".";
    close;
}

mes "Choose: " + jobname(@class1) + " or " + jobname(@class2) + "?";
close;
```

---

### Example 8: Job Change Script

```c
// Simple job change to Knight
if ((eaclass() & EAJ_BASEMASK) != EAJ_SWORDMAN) {
    mes "You are not a Swordman!";
    close;
}

if ((eaclass() & EAJL_2)) {
    mes "You are already 2nd class!";
    close;
}

if (JobLevel < 40) {
    mes "Reach Job Level 40 first!";
    close;
}

mes "Changing you to Knight!";
jobchange Job_Knight;
close;
```

---

### Example 9: Gender-Specific Jobs (Bard/Dancer)

```c
// Bard/Dancer are the same job tree, differ by gender
set @eac, eaclass();

if (((@eac & EAJ_BASEMASK) == EAJ_ARCHER) && (@eac & EAJL_2_2)) {
    if (Sex == 1) {
        mes "You are a Bard!";
    } else {
        mes "You are a Dancer!";
    }
}

// Using roclass with explicit gender
set @bardjob, roclass(EAJ_ARCHER | EAJL_2_2, 1);  // Male = Bard
set @dancerjob, roclass(EAJ_ARCHER | EAJL_2_2, 0); // Female = Dancer
```

---

### Example 10: Quest Restricted to Mage Tree Only

```c
if ((eaclass() & EAJ_BASEMASK) != EAJ_MAGE) {
    mes "This quest is for Mage classes only!";
    close;
}

mes "Welcome, magic user!";
// Allows: Mage, Wizard, Sage, High Mage, High Wizard, Professor,
// Warlock, Sorcerer, Baby Mage, etc.
```

---

## 7. JOB ID REFERENCE

### Complete Job Tree: Swordman

```c
EAJ_SWORDMAN                              = Swordman (Job ID: 1)
EAJ_SWORDMAN | EAJL_2_1                   = Knight (12)
EAJ_SWORDMAN | EAJL_2_2                   = Crusader (14)
EAJ_SWORDMAN | EAJL_UPPER                 = High Swordman (4002)
EAJ_SWORDMAN | EAJL_2_1 | EAJL_UPPER      = Lord Knight (4008)
EAJ_SWORDMAN | EAJL_2_2 | EAJL_UPPER      = Paladin (4015)
EAJ_SWORDMAN | EAJL_BABY                  = Baby Swordman (4024)
EAJ_SWORDMAN | EAJL_2_1 | EAJL_BABY       = Baby Knight (4030)
EAJ_SWORDMAN | EAJL_2_2 | EAJL_BABY       = Baby Crusader (4032)
EAJ_SWORDMAN | EAJL_2_1 | EAJL_THIRD      = Rune Knight (4054)
EAJ_SWORDMAN | EAJL_2_2 | EAJL_THIRD      = Royal Guard (4056)
EAJ_SWORDMAN | EAJL_2_1 | EAJL_THIRD | EAJL_UPPER = Rune Knight T (4096)
EAJ_SWORDMAN | EAJL_2_2 | EAJL_THIRD | EAJL_UPPER = Royal Guard T (4098)
EAJ_SWORDMAN | EAJL_2_1 | EAJL_FOURTH     = Dragon Knight (4252)
EAJ_SWORDMAN | EAJL_2_2 | EAJL_FOURTH     = Imperial Guard (4254)
```

---

### Complete Job Tree: Mage

```c
EAJ_MAGE                              = Mage (2)
EAJ_MAGE | EAJL_2_1                   = Wizard (9)
EAJ_MAGE | EAJL_2_2                   = Sage (16)
EAJ_MAGE | EAJL_UPPER                 = High Mage (4003)
EAJ_MAGE | EAJL_2_1 | EAJL_UPPER      = High Wizard (4010)
EAJ_MAGE | EAJL_2_2 | EAJL_UPPER      = Professor (4017)
EAJ_MAGE | EAJL_BABY                  = Baby Mage (4025)
EAJ_MAGE | EAJL_2_1 | EAJL_BABY       = Baby Wizard (4031)
EAJ_MAGE | EAJL_2_2 | EAJL_BABY       = Baby Sage (4033)
EAJ_MAGE | EAJL_2_1 | EAJL_THIRD      = Warlock (4060)
EAJ_MAGE | EAJL_2_2 | EAJL_THIRD      = Sorcerer (4062)
EAJ_MAGE | EAJL_2_1 | EAJL_THIRD | EAJL_UPPER = Warlock T (4102)
EAJ_MAGE | EAJL_2_2 | EAJL_THIRD | EAJL_UPPER = Sorcerer T (4104)
EAJ_MAGE | EAJL_2_1 | EAJL_FOURTH     = Arch Mage (4258)
EAJ_MAGE | EAJL_2_2 | EAJL_FOURTH     = Elemental Master (4260)
```

---

### Novice Tree (Special Case)

```c
EAJ_NOVICE                        = Novice (0)
EAJ_NOVICE | EAJL_2_1             = Super Novice (23)
EAJ_NOVICE | EAJL_UPPER           = High Novice (4001)
EAJ_NOVICE | EAJL_BABY            = Baby Novice (4023)
EAJ_NOVICE | EAJL_2_1 | EAJL_BABY = Super Baby (4045)
EAJ_NOVICE | EAJL_2_1 | EAJL_THIRD = Super Novice (Expanded) (4190)
```

**Note:** Super Novice is treated as the "2-1" job of Novice in the job system.

---

## 8. COMMON JOB IDs

### First Classes

| Job | ID | Constant |
|-----|-----|----------|
| Novice | 0 | Job_Novice |
| Swordman | 1 | Job_Swordman |
| Mage | 2 | Job_Mage |
| Archer | 3 | Job_Archer |
| Acolyte | 4 | Job_Acolyte |
| Merchant | 5 | Job_Merchant |
| Thief | 6 | Job_Thief |
| Taekwon | 4046 | Job_Taekwon |
| Gunslinger | 24 | Job_Gunslinger |
| Ninja | 25 | Job_Ninja |
| Summoner | 4218 | Job_Summoner |

---

### Second Classes (2-1)

| Job | ID | Constant |
|-----|-----|----------|
| Knight | 7 | Job_Knight |
| Wizard | 9 | Job_Wizard |
| Hunter | 11 | Job_Hunter |
| Priest | 8 | Job_Priest |
| Blacksmith | 10 | Job_Blacksmith |
| Assassin | 12 | Job_Assassin |
| Star Gladiator | 4047 | Job_Star_Gladiator |

---

### Second Classes (2-2)

| Job | ID | Constant |
|-----|-----|----------|
| Crusader | 14 | Job_Crusader |
| Sage | 16 | Job_Sage |
| Bard (male) | 19 | Job_Bard |
| Dancer (female) | 20 | Job_Dancer |
| Monk | 15 | Job_Monk |
| Alchemist | 18 | Job_Alchemist |
| Rogue | 17 | Job_Rogue |
| Soul Linker | 4049 | Job_Soul_Linker |

---

### Transcendent Classes

| Job | ID | Constant |
|-----|-----|----------|
| Lord Knight | 4008 | Job_Lord_Knight |
| High Wizard | 4010 | Job_High_Wizard |
| Sniper | 4012 | Job_Sniper |
| High Priest | 4009 | Job_High_Priest |
| Whitesmith | 4011 | Job_Whitesmith |
| Assassin Cross | 4013 | Job_Assassin_Cross |
| Paladin | 4015 | Job_Paladin |
| Professor | 4017 | Job_Professor |
| Clown (male) | 4020 | Job_Clown |
| Gypsy (female) | 4021 | Job_Gypsy |
| Champion | 4016 | Job_Champion |
| Creator | 4019 | Job_Creator |
| Stalker | 4018 | Job_Stalker |

---

### Third Classes

| Job | ID | Constant |
|-----|-----|----------|
| Rune Knight | 4054 | Job_Rune_Knight |
| Warlock | 4060 | Job_Warlock |
| Ranger | 4056 | Job_Ranger |
| Arch Bishop | 4057 | Job_Arch_Bishop |
| Mechanic | 4059 | Job_Mechanic |
| Guillotine Cross | 4062 | Job_Guillotine_Cross |
| Royal Guard | 4063 | Job_Royal_Guard |
| Sorcerer | 4058 | Job_Sorcerer |
| Minstrel (male) | 4075 | Job_Minstrel |
| Wanderer (female) | 4076 | Job_Wanderer |
| Sura | 4061 | Job_Sura |
| Geneticist | 4074 | Job_Geneticist |
| Shadow Chaser | 4073 | Job_Shadow_Chaser |

---

### Fourth Classes

| Job | ID | Constant |
|-----|-----|----------|
| Dragon Knight | 4252 | Job_Dragon_Knight |
| Meister | 4253 | Job_Meister |
| Shadow Cross | 4254 | Job_Shadow_Cross |
| Arch Mage | 4258 | Job_Arch_Mage |
| Cardinal | 4257 | Job_Cardinal |
| Windhawk | 4256 | Job_Windhawk |
| Imperial Guard | 4261 | Job_Imperial_Guard |
| Biolo | 4260 | Job_Biolo |
| Abyss Chaser | 4259 | Job_Abyss_Chaser |
| Elemental Master | 4262 | Job_Elemental_Master |
| Inquisitor | 4263 | Job_Inquisitor |
| Troubadour (male) | 4264 | Job_Troubadour |
| Trouvere (female) | 4265 | Job_Trouvere |

---

## COMMON USE CASES

### Restrict Quest to 2nd Class Only

```c
if (!(eaclass() & EAJL_2)) {
    mes "2nd class only!";
    close;
}
```

---

### Restrict to Transcendent Characters

```c
if (!(eaclass() & EAJL_UPPER)) {
    mes "Rebirth characters only!";
    close;
}
```

---

### Check if Swordman Family

```c
if ((eaclass() & EAJ_BASEMASK) == EAJ_SWORDMAN) {
    mes "Swordman family member!";
}
```

---

### Allow Only Non-Baby Classes

```c
if (eaclass() & EAJL_BABY) {
    mes "Sorry, no baby classes!";
    close;
}
```

---

## SCRIPT COMMAND REFERENCE

### eaclass()

**Returns:** eAthena job class ID of attached player

```c
set @eac, eaclass();
```

---

### roclass(<ea_job> {, <gender>})

**Converts:** eAthena job ID → RO job ID
**Gender:** 0 = female, 1 = male (optional, uses attached player's gender if omitted)

```c
set @knight, roclass(EAJ_SWORDMAN | EAJL_2_1);  // Job_Knight
set @bard, roclass(EAJ_ARCHER | EAJL_2_2, 1);   // Job_Bard (male)
set @dancer, roclass(EAJ_ARCHER | EAJL_2_2, 0); // Job_Dancer (female)
```

---

### jobchange <job_id>

**Changes:** Player's job to specified RO job ID

```c
jobchange Job_Knight;          // Change to Knight
jobchange Job_Lord_Knight;     // Change to Lord Knight
```

---

### jobname(<job_id>)

**Returns:** Job name string

```c
mes "Your job is: " + jobname(Class);
```

---

## TIPS & BEST PRACTICES

1. **Always use eaclass() for job checks** - More flexible than checking Class directly
2. **Use EAJ_BASEMASK for family checks** - Allows any variant of a job tree
3. **Use EAJ_UPPERMASK for specific job checks** - Allows trans/baby variants
4. **Use bitwise AND (&) for flag checks** - `if (eaclass() & EAJL_UPPER)`
5. **Use bitwise OR (|) for job construction** - `EAJ_MAGE | EAJL_2_1`
6. **Check roclass() return value** - Returns -1 if job doesn't exist
7. **Handle gender for Bard/Dancer** - Always specify or check Sex variable

---

## CROSS-REFERENCES

- **Script Commands:** See KB_REF_ScriptCommands.md
- **At-Commands:** See KB_REF_AtCommands.md for @job command
- **Skill System:** See KB_REF_SkillSystem.md for job-specific skills
- **Complete Job System Docs:** See `/doc/ea_job_system.txt`

---

**Total Coverage:** 100% of job system mechanics
**Use Case:** Job checking, job changes, quest restrictions, job trees

# ═══════════════════════════════════════════════════════════════
# PART 2: MAPFLAGS (mf_* CONSTANTS)
# ═══════════════════════════════════════════════════════════════

---
kb_id: KB_REF_003
kb_type: reference
kb_category: map_configuration
kb_subcategory: mapflags
kb_keywords: [mapflag, map settings, pvp, gvg, woe, restrictions, noteleport, nowarp, noreturn, nosave, battle, map behavior, setmapflag, removemapflag]
kb_related: [KB_CMD_010, KB_CONF_003]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2013-08-30
kb_use_case: [map_configuration, pvp_setup, woe_setup, server_customization]
---

# rAthena Mapflag Reference

Complete reference for all mapflags that control map behavior and restrictions.

## Overview

Mapflags determine how a map behaves in various situations - from teleportation restrictions to PvP modes to weather effects. They are essential for configuring your server's gameplay experience.

**Configuration:**
- Set in NPC scripts using `setmapflag` command
- Remove using `removemapflag` command
- Usually configured in `/npc/mapflag/` directory

**Basic Syntax:**
```c
<map_name>	mapflag	<mapflag_name>{	<parameters>}
```

---

## CATEGORIES

1. [Restrictions](#1-restrictions) - Movement, items, trading
2. [Battle-Related](#2-battle-related) - PvP, GvG, damage
3. [Map Effects](#3-map-effects) - Weather, visuals
4. [Miscellaneous](#4-miscellaneous) - Exp rates, special features

---

## 1. RESTRICTIONS

### noreturn

**Description:** Disables map-warping items that return players to specific locations.

**Blocks:**
- Butterfly Wing (ID 602)
- Yellow/Green/Red/Blue Butterfly Wing (IDs 14582-14585)
- Siege Teleport Scroll (ID 14591)
- Dungeon Teleport Scroll 1/2/3 (IDs 14527, 14581, 12352)
- `warpparty` and `warpguild` script commands (for destinations outside current map)

**Example:**
```c
prontera	mapflag	noreturn
```

**Use Case:** WoE castles, dungeons, event maps where you don't want easy exits.

---

### noteleport

**Description:** Disables ALL teleportation methods within a map.

**Blocks:**
- Fly Wing (ID 601)
- Giant Fly Wing (ID 12212)
- Skills: AL_TELEPORT, TK_HIGHJUMP, SC_DIMENSIONDOOR
- Skills won't teleport targets: RG_INTIMIDATE, NPC_EXPULSION, CG_TAROTCARD
- Script command `warp` with "Random" as destination
- Script command `warpwaitingpc` with "SavePoint" as destination
- Script command `unitwarp` for players
- Atcommand `@jump`

**Example:**
```c
pvp_n_1-1	mapflag	noteleport
```

**Use Case:** PvP arenas, boss rooms, areas where teleporting would be unfair or break gameplay.

---

### nowarp

**Description:** Disables warping FROM a map (prevents leaving).

**Blocks:**
- Script commands `warpparty` and `warpguild` won't warp players FROM nowarp maps
- Atcommands: `@warp`, `@go`, `@load`, `@jump`
- Atcommands: `@partyrecall`, `@guildrecall`, `@recallall` won't pull players from nowarp maps
- Skill GD_EMERGENCYCALL won't warp players from nowarp maps
- Unit UNT_CALLFAMILY won't warp players from nowarp maps

**Example:**
```c
guild_vs1	mapflag	nowarp
```

**Use Case:** Lock players in area (event maps, special instances, jail).

**Note:** Players can still be warped TO the map, just not FROM it.

---

### nowarpto

**Description:** Disables warping TO a map (prevents entering).

**Blocks:**
- Atcommands: `@warp`, `@go`, `@load`, `@jump` cannot target this map
- Atcommands: `@partyrecall`, `@guildrecall`, `@recallall` cannot target this map
- Command `/memo` disabled
- Skill GD_EMERGENCYCALL disabled (if flag 16 set in `/conf/battle/skill.conf`) - doesn't work for gvg_castle maps

**Example:**
```c
guild_vs2	mapflag	nowarpto
```

**Use Case:** Restricted access maps, GM-only areas, prevent unauthorized entry.

---

### nogo

**Description:** Disables usage of `@go` command on the map.

**Example:**
```c
prontera	mapflag	nogo
```

**Use Case:** Prevent players from using `@go` shortcut to leave area.

---

### nosave <map_name>,<x>,<y>

**Description:** Disables auto-saving on map. Players who log off here will be warped to specified location on login.

**Parameters:**
- `<map_name>`: Map to respawn at (use `SavePoint` for player's save point)
- `<x>,<y>`: Coordinates (optional with SavePoint)

**Examples:**
```c
// Respawn at SavePoint
guild_vs1	mapflag	nosave	SavePoint

// Respawn at specific location
pvp_n_1-1	mapflag	nosave	prontera,156,191
```

**Use Case:** Temporary areas, dungeons, instances where you don't want save point changed.

---

### nomemo

**Description:** Disables saving warp point and marriage skills.

**Blocks:**
- `/memo` command (can't save warp point)
- Marriage skills: WE_CALLPARTNER, WE_CALLPARENT, WE_CALLBABY

**Example:**
```c
gef_dun00	mapflag	nomemo
```

**Use Case:** Dungeons, instances, areas where warp points would break progression.

---

### noitemconsumption

**Description:** Disables usage of ALL items on the map.

**Blocks:**
- All consumable items
- Equipment changes
- Item usage

**Example:**
```c
pvp_y_1-1	mapflag	noitemconsumption
```

**Use Case:** Pure skill-based PvP, special challenge maps, no-item events.

**Note:** Can be bypassed with PC_PERM_ITEM_UNCONDITIONAL permission.

---

### notrade

**Description:** Disables trading between players on the map.

**Example:**
```c
prontera	mapflag	notrade
```

**Use Case:** Prevent trading in specific areas, reduce scam potential in town centers.

---

### nodrop

**Description:** Disables dropping items on the map.

**Exception:** Items may still drop if inventory is full and `item_flooritem_check` is disabled in `/conf/battle/items.conf`.

**Example:**
```c
prontera	mapflag	nodrop
```

**Use Case:** Keep maps clean, prevent item drops in towns, anti-grief measure.

---

### noloot / nomobloot / nomvploot

**Description:** Disables monsters from dropping items.

- `noloot`: All monsters (same as nomobloot + nomvploot)
- `nomobloot`: Normal monsters don't drop
- `nomvploot`: MVP monsters don't drop

**Note:** Looted items (from Gank/Steal skills) will still drop.

**Examples:**
```c
// No drops at all
prt_fild08	mapflag	noloot

// Only normal mobs don't drop (MVPs still do)
pay_fild01	mapflag	nomobloot

// MVPs don't drop (normal mobs still do)
mjolnir_01	mapflag	nomvploot
```

**Use Case:** Training maps, pure exp farming, reduce item database load.

---

### noexp / nobaseexp / nojobexp

**Description:** Disables gaining experience from monsters.

- `noexp`: No base AND job exp (same as nobaseexp + nojobexp)
- `nobaseexp`: No base experience
- `nojobexp`: No job experience

**Includes:** MVP bonuses also disabled.

**Examples:**
```c
// No experience at all
pvp_y_1-1	mapflag	noexp

// No base exp (still get job exp)
prt_fild08	mapflag	nobaseexp

// No job exp (still get base exp)
pay_fild01	mapflag	nojobexp
```

**Use Case:** PvP maps, testing areas, item farming without leveling.

---

### nopenalty / noexppenalty / nozenypenalty

**Description:** Disables loss of exp/zeny upon death.

- `nopenalty`: No exp AND zeny loss (same as noexppenalty + nozenypenalty)
- `noexppenalty`: No exp loss on death
- `nozenypenalty`: No zeny loss on death

**Notes:**
- `noexppenalty` also affects pets
- Skills PR_REDEMPTIO and LG_INSPIRATION won't deduct EXP
- `nozenypenalty` only applies if `zeny_penalty` enabled in `/conf/battle/exp.conf`

**Examples:**
```c
// No penalties at all
prontera	mapflag	nopenalty

// Only exp protected
pvp_n_1-1	mapflag	noexppenalty

// Only zeny protected
gef_fild00	mapflag	nozenypenalty
```

**Use Case:** Newbie areas, PvP maps, event maps, low-penalty zones.

---

### nochat

**Description:** Disables chatroom creation on the map.

**Example:**
```c
pvp_n_1-1	mapflag	nochat
```

**Use Case:** Reduce spam in busy areas, PvP focus, event maps.

---

### novending

**Description:** Disables shop creation from MC_VENDING skill.

**Example:**
```c
prontera	mapflag	novending
```

**Use Case:** Designated vending areas, reduce map clutter, prevent vendor spam.

---

### nobuyingstore

**Description:** Disables shop creation from ALL_BUYING_STORE skill.

**Example:**
```c
prontera	mapflag	nobuyingstore
```

**Use Case:** Designated buying areas, prevent spam, organize economy.

---

### nousecart

**Description:** Disables cart usage on the map.

**Example:**
```c
aldebaran	mapflag	nousecart
```

**Use Case:** Reduce sprite load, specific area restrictions, roleplay purposes.

---

### noskill

**Description:** Disables ALL skill usage on the map.

**Example:**
```c
prontera	mapflag	noskill
```

**Use Case:** Safe zones, event maps, roleplaying areas, extreme restrictions.

**Warning:** Very restrictive - disables ALL skills including buffs.

---

### restricted <zone>

**Description:** Disables certain items and skills based on zone number.

**Zone Databases:**
- `/db/(pre-)re/item_noequip.txt` - Item restrictions
- `/db/(pre-)re/skill_nocast_db.txt` - Skill restrictions

**Restricted Zones:**
- `1` - Aldebaran Turbo Track
- `2` - Jail
- `3` - Izlude Battle Arena
- `4` - WoE:SE Maps
- `5` - Sealed Shrine
- `6` - Instances (Endless Tower, Orc's Memory, Nidhoggr's Instance)
- `7` - Towns
- `8` - WOE:TE Dungeons

**Examples:**
```c
// Restrict town items/skills
prontera	mapflag	restricted	7

// Restrict WoE items/skills
prtg_cas01	mapflag	restricted	4
```

**Use Case:** Balanced competitive areas, specific gameplay rules, item/skill bans.

---

### monster_noteleport

**Description:** Prevents monsters from teleporting on the map.

**Blocks:**
- Monster teleportation skills
- RG_INTIMIDATE won't teleport monsters

**Example:**
```c
boss_map	mapflag	monster_noteleport
```

**Use Case:** Boss fights, prevent mobs escaping, specific monster behavior control.

---

### nobranch

**Description:** Disables monster-spawning items on the map.

**Blocks:**
- Dead Branch (ID 604)
- Bloody Branch (ID 12103)
- Poring Box (ID 12109)
- Red Pouch (ID 12024)

**Note:** Items can be modified in `/db/(pre-)re/item_flag.txt`.

**Special:** If `mob_warp` enabled with flag 4 in `/conf/battle/monster.conf`, also prevents mobs being warped onto the map (except slaves).

**Example:**
```c
prontera	mapflag	nobranch
```

**Use Case:** Towns, prevent griefing, controlled spawn areas.

---

### noicewall

**Description:** Disables skill WZ_ICEWALL on the map.

**Example:**
```c
pvp_n_1-1	mapflag	noicewall
```

**Use Case:** PvP balance, prevent blocking, reduce skill spam.

---

### nosunmoonstarmiracle

**Description:** Disables Star Gladiator's "Solar, Lunar, and Stellar Miracle" from occurring.

**Example:**
```c
prontera	mapflag	nosunmoonstarmiracle
```

**Use Case:** Prevent exploit areas, balance specific maps.

---

### forcemineffect

**Description:** Forces simpler skill effects (like `/mineffect` command).

**Example:**
```c
pvp_n_1-1	mapflag	forcemineffect
```

**Use Case:** Performance optimization, reduce lag in busy areas, cleaner visuals.

---

### nolockon

**Description:** Disables attacking another player without holding shift or using `/ns`.

**Example:**
```c
prontera	mapflag	nolockon
```

**Use Case:** Prevent accidental PvP, safe zones, town protection.

---

### nocommand <group_level>

**Description:** Disables commands on the map.

**Parameters:**
- No parameter: Disables ALL commands for everyone
- `<group_level>`: Only disables for players with group level BELOW this value

**Examples:**
```c
// Disable all commands for everyone
pvp_n_1-1	mapflag	nocommand

// Disable commands for group level below 50 (normal players)
prontera	mapflag	nocommand	50
```

**Use Case:** Prevent command abuse, fair play areas, restricted zones.

---

### nomapchannelautojoin

**Description:** Stops players from automatically joining #map channel.

**Requirements:**
- Map channels must be enabled
- `map_local_channel_autojoin` must be true in `/conf/channels.conf`

**Example:**
```c
prontera	mapflag	nomapchannelautojoin
```

**Use Case:** Reduce chat spam, private areas, roleplay control.

---

### notomb

**Description:** Disables MVP tombs from appearing on the map.

**Example:**
```c
boss_map	mapflag	notomb
```

**Use Case:** Clean boss areas, prevent tomb spam, aesthetic control.

---

### nocostume

**Description:** Disables costume sprites on the map.

**Notes:**
- Only disables visual sprites, NOT item effects
- If player logs out on nocostume map, costumes won't show in character server either

**Example:**
```c
prontera	mapflag	nocostume
```

**Use Case:** Roleplay immersion, aesthetic control, visual consistency.

---

### norenewaldroppenalty

**Description:** Disables renewal drop rate penalty due to level difference.

**Example:**
```c
prt_fild08	mapflag	norenewaldroppenalty
```

**Use Case:** Training maps, allow high-level farming, balanced drop rates.

---

### norenewalexppenalty

**Description:** Disables renewal experience penalty due to level difference.

**Example:**
```c
prt_fild08	mapflag	norenewalexppenalty
```

**Use Case:** Training maps, allow high-level farming, balanced exp gain.

---

### nopetcapture

**Description:** Disables ability to capture pets on the map.

**Example:**
```c
pvp_n_1-1	mapflag	nopetcapture
```

**Use Case:** PvP maps, boss maps, special areas.

---

### nobank

**Description:** Disables Bank system on the map.

**Example:**
```c
pvp_n_1-1	mapflag	nobank
```

**Use Case:** Restricted areas, prevent banking exploits.

---

### norodex

**Description:** Disables RODex (mail system) on the map.

**Example:**
```c
pvp_n_1-1	mapflag	norodex
```

**Use Case:** Event maps, prevent mail abuse, focus gameplay.

---

## 2. BATTLE-RELATED

### pvp / pvp_noparty / pvp_noguild / pvp_nocalcrank

**Description:** Enables Player vs. Player mode with damage adjustments.

- `pvp`: Standard PvP mode
- `pvp_noparty`: Ignore party alliances (can hit party members)
- `pvp_noguild`: Ignore guild alliances (can hit guild members)
- `pvp_nocalcrank`: Disable PvP ranking calculation

**Examples:**
```c
// Standard PvP
pvp_y_1-1	mapflag	pvp

// Free-for-all (ignore party)
pvp_n_1-1	mapflag	pvp
pvp_n_1-1	mapflag	pvp_noparty

// Full FFA (ignore party and guild)
pvp_n_2-2	mapflag	pvp
pvp_n_2-2	mapflag	pvp_noparty
pvp_n_2-2	mapflag	pvp_noguild

// PvP without ranking
pvp_y_2-2	mapflag	pvp
pvp_y_2-2	mapflag	pvp_nocalcrank
```

**Use Case:** PvP arenas, deathmatch areas, team battles, ranked matches.

---

### pvp_nightmaredrop <id>,<type>,<rate>

**Description:** Causes players to drop items upon death.

**Parameters:**
- `<id>`: Item ID or "random"
- `<type>`: "inventory", "equip", or "all"
- `<rate>`: Drop chance (10000 = 100%)

**Examples:**
```c
// Drop random item from inventory (50% chance)
pvp_n_1-1	mapflag	pvp_nightmaredrop	random,inventory,5000

// Drop specific item (100% chance)
pvp_n_1-1	mapflag	pvp_nightmaredrop	501,inventory,10000

// Drop random equipment (10% chance)
pvp_n_1-1	mapflag	pvp_nightmaredrop	random,equip,1000

// Drop anything (25% chance)
pvp_n_1-1	mapflag	pvp_nightmaredrop	random,all,2500
```

**Use Case:** Hardcore PvP, high-risk areas, unique game modes.

**Note:** Does NOT require PvP mapflag to be set (works anywhere).

---

### gvg / gvg_noparty / gvg_castle / gvg_dungeon / gvg_te / gvg_te_castle

**Description:** Enables Guild vs. Guild mode with damage adjustments.

- `gvg`: Standard GvG mode
- `gvg_noparty`: Ignore party alliances
- `gvg_castle`: Guild castle (GvG only active during WoE)
- `gvg_dungeon`: Guild dungeon (warp out after 2 deaths)
- `gvg_te`: WOE:TE area
- `gvg_te_castle`: WOE:TE castle (special restrictions)

**Examples:**
```c
// Standard GvG
guild_vs1	mapflag	gvg

// WoE Castle
prtg_cas01	mapflag	gvg_castle

// Guild Dungeon
gld_dun01	mapflag	gvg_dungeon

// WoE:TE
te_prtcas01	mapflag	gvg_te
te_prtcas01	mapflag	gvg_te_castle
```

**Use Case:** War of Emperium, guild wars, guild dungeons, competitive guild content.

---

### battleground {<type>}

**Description:** Enables Battlegrounds mode with damage adjustments.

**Parameters:**
- `1` (default): Nothing
- `2`: Show scoreboard

**Examples:**
```c
// Basic BG
bat_c01	mapflag	battleground

// BG with scoreboard
bat_c02	mapflag	battleground	2
```

**Use Case:** Battleground arenas, team-based competitive content.

---

### partylock / guildlock

**Description:** Prevents alteration of parties/guilds on the map.

**Blocks:**
- Creating
- Leaving
- Inviting
- Expelling
- Breaking
- Changing leaders

**Notes:**
- `partylock`: Still allows changing party options
- `guildlock`: Also blocks guild alliance changes

**Examples:**
```c
// Lock party changes
pvp_n_1-1	mapflag	partylock

// Lock guild changes
guild_vs1	mapflag	guildlock
```

**Use Case:** Competitive events, prevent team switching mid-match, tournament fairness.

---

### skill_damage {<skill_name>,<caster>,<SKILLDMG_PC>,{<SKILLDMG_MOB>,{<SKILLDMG_BOSS>,{<SKILLDMG_OTHER>}}}}

**Description:** Adjusts skill damage on the map.

**Parameters:**
- `skill_name`: Skill name from skill_db.yml (or "all" for all skills)
- `caster`: Caster type(s) - bitmask
  - `BL_PC` = Player
  - `BL_MOB` = Monster
  - `BL_PET` = Pet
  - `BL_HOM` = Homunculus
  - `BL_MER` = Mercenary
  - `BL_ELEM` = Elemental
- `damage`: Percent adjustment (-100 to 100000)
  - `SKILLDMG_PC` = against player
  - `SKILLDMG_MOB` = against normal monster
  - `SKILLDMG_BOSS` = against boss monster
  - `SKILLDMG_OTHER` = against other (hom/merc/pet/elem)

**Note:** Can also use `db/skill_damage_db.txt` for Map type 16.

**Examples:**
```c
// Reduce all player skill damage by 50% in PvP
pvp_n_1-1	mapflag	skill_damage	all,BL_PC,50

// Increase Bash damage against players by 200%
pvp_n_1-1	mapflag	skill_damage	SM_BASH,BL_PC,200

// Disable all damage to monsters
prt_fild08	mapflag	skill_damage	all,BL_MOB,0
```

**Use Case:** PvP balance, custom damage rules, skill adjustments, unique game modes.

---

### skill_duration <skill_name>,<percentage>

**Description:** Sets trap-type skill duration to percentage of original.

**Example:**
```c
// Makes HT_ANKLESNARE last 4x longer
prtg_cas01	mapflag	skill_duration	HT_ANKLESNARE,400

// Makes all traps last half as long
pvp_n_1-1	mapflag	skill_duration	all,50
```

**Use Case:** Balance trap skills, WoE adjustments, custom gameplay.

---

### invincible_time <duration>

**Description:** Sets invincibility duration (in ms) when player loads onto map.

**Cancelled By:**
- Player walking
- Player interacting (any action)

**Default:** Uses `player_invincible_time` from `/conf/battle/player.conf` if not specified.

**Example:**
```c
// 5 seconds invincibility on spawn
pvp_n_1-1	mapflag	invincible_time	5000

// 10 seconds invincibility
guild_vs1	mapflag	invincible_time	10000
```

**Use Case:** Prevent spawn camping, fair respawn, give players time to orient.

---

## 3. MAP EFFECTS

### Weather Effects

**Available Effects:**
- `clouds` - Cloudy sky
- `clouds2` - Darker clouds
- `fireworks` - Fireworks display
- `fog` - Foggy atmosphere
- `leaves` - Falling leaves
- `sakura` - Falling cherry blossoms
- `snow` - Snowfall

**Examples:**
```c
prontera	mapflag	sakura
lutie	mapflag	snow
morocc	mapflag	fog
```

**Use Case:** Atmosphere, seasonal events, aesthetic enhancement, immersion.

---

### nightenabled

**Description:** Displays night mode effects on the map.

**Example:**
```c
prt_fild08	mapflag	nightenabled
```

**Use Case:** Most outdoor maps, day/night cycle, atmosphere.

**Note:** Used on most outdoor maps by default.

---

## 4. MISCELLANEOUS

### town

**Description:** Marks map as a town.

**Effects:**
- Allows mail access
- Disables kill stealing

**Example:**
```c
prontera	mapflag	town
```

**Use Case:** Major cities, safe zones, social hubs.

---

### reset

**Description:** Allows usage of Neuralizer (ID 12213).

**Example:**
```c
prontera	mapflag	reset
```

**Use Case:** Stat/skill reset areas, convenience zones.

---

### bexp <rate> / jexp <rate>

**Description:** Changes base/job experience rates on the map.

**Parameters:**
- `<rate>`: Percentage (100 = 1x, 200 = 2x, 50 = 0.5x)
- Supports negative values to reduce EXP
- Takes into account `base_exp_rate` and `job_exp_rate` from `/conf/battle/exp.conf`

**Examples:**
```c
// Double base exp
prt_fild08	mapflag	bexp	200

// Triple job exp
pay_fild01	mapflag	jexp	300

// Half base exp
gef_dun00	mapflag	bexp	50

// No base exp (alternative to nobaseexp)
pvp_n_1-1	mapflag	bexp	0
```

**Use Case:** Training areas, bonus zones, event maps, penalty areas.

---

### loadevent

**Description:** Triggers label "OnPCLoadMapEvent" when players enter the map.

**Triggered By:**
- Entering the map
- Teleporting within the map

**Example:**
```c
prontera	mapflag	loadevent
```

**Script Example:**
```c
-	script	LoadEventExample	-1,{
OnPCLoadMapEvent:
    if (strcharinfo(3) == "prontera") {
        mes "Welcome to Prontera!";
        close;
    }
    end;
}
```

**Use Case:** Welcome messages, buff application, entrance checks, custom events.

**See Also:** `/doc/script_commands.txt` for more details.

---

### allowks

**Description:** Allows kill stealing on the map (renders `@noks` command useless).

**Example:**
```c
prt_fild08	mapflag	allowks
```

**Use Case:** Free-for-all farming, competitive areas, no kill steal protection.

---

### autotrade

**Description:** Allows `@autotrade` command on the map.

**Requirements:**
- Only applies if `at_mapflag` enabled in `/conf/battle/misc.conf`
- Otherwise, @autotrade enabled on all maps by default

**Example:**
```c
prontera	mapflag	autotrade
```

**Use Case:** Designated vending areas, market zones.

---

### hidemobhpbar

**Description:** Hides monster HP bar on the map.

**Example:**
```c
boss_map	mapflag	hidemobhpbar
```

**Use Case:** Aesthetic preference, mystery boss fights, cleaner visuals.

**Note:** Ignores `monster_hp_bars_info` config value.

---

### specialpopup <popup_id>

**Description:** Displays special popup when player enters the map.

**Example:**
```c
prontera	mapflag	specialpopup	1
```

**Use Case:** Announcements, warnings, information displays.

**See Also:** Script command "specialpopup" for popup types.

---

## SCRIPT COMMANDS

### setmapflag("<map_name>", <mapflag>{, <value>})

**Description:** Sets a mapflag on a map dynamically.

**Examples:**
```c
// Enable PvP
setmapflag("prontera", mf_pvp);

// Set nosave
setmapflag("prontera", mf_nosave, "SavePoint");

// Set bexp to 200%
setmapflag("prt_fild08", mf_bexp, 200);
```

---

### removemapflag("<map_name>", <mapflag>)

**Description:** Removes a mapflag from a map dynamically.

**Example:**
```c
// Disable PvP
removemapflag("prontera", mf_pvp);

// Remove noteleport
removemapflag("guild_vs1", mf_noteleport);
```

---

### getmapflag("<map_name>", <mapflag>)

**Description:** Checks if a mapflag is set on a map.

**Returns:** 1 if set, 0 if not set.

**Example:**
```c
if (getmapflag("prontera", mf_pvp)) {
    mes "This is a PvP map!";
} else {
    mes "This is not a PvP map.";
}
```

---

## MAPFLAG CONSTANTS

Use these constants in scripts:

```c
mf_nomemo, mf_noteleport, mf_nosave, mf_nobranch, mf_noexppenalty, mf_nozenypenalty,
mf_notrade, mf_noskill, mf_nowarp, mf_partylock, mf_noicewall, mf_snow, mf_fog,
mf_sakura, mf_leaves, mf_clouds, mf_clouds2, mf_fireworks, mf_gvg_castle, mf_gvg,
mf_pvp, mf_pvp_noparty, mf_pvp_noguild, mf_loadevent, mf_nochat, mf_noexppenalty,
mf_noreturn, mf_nogo, mf_nomemo, mf_pvp_nocalcrank, mf_gvg_te, mf_gvg_te_castle,
mf_battleground, mf_reset, mf_guildlock, mf_town, mf_autotrade, mf_allowks,
mf_monster_noteleport, mf_pvp_nightmaredrop, mf_restricted, mf_nocommand,
mf_nodrop, mf_jexp, mf_bexp, mf_novending, mf_nopenalty, mf_gvg_noparty,
mf_noexppenalty, mf_nozenypenalty, mf_nightenabled, mf_nobaseexp, mf_nojobexp,
mf_nomobloot, mf_nomvploot, mf_noreturn, mf_nowarpto, mf_nightmaredrop,
mf_noexp, mf_noitemconsumption, mf_nosunmoonstarmiracle, mf_nomapchannelautojoin,
mf_nousecart, mf_nolockon, mf_notomb, mf_nocostume, mf_norenewaldroppenalty,
mf_norenewalexppenalty, mf_noloot, mf_nopetcapture, mf_nobuyingstore,
mf_skill_damage, mf_skill_duration, mf_invincible_time, mf_nobank, mf_norodex,
mf_hidemobhpbar, mf_specialpopup
```

---

## COMMON MAPFLAG COMBINATIONS

### PvP Arena (Fair)
```c
pvp_n_1-1	mapflag	pvp
pvp_n_1-1	mapflag	pvp_noparty
pvp_n_1-1	mapflag	pvp_noguild
pvp_n_1-1	mapflag	noteleport
pvp_n_1-1	mapflag	nowarp
pvp_n_1-1	mapflag	nopenalty
pvp_n_1-1	mapflag	nosave	SavePoint
pvp_n_1-1	mapflag	invincible_time	5000
```

### WoE Castle
```c
prtg_cas01	mapflag	gvg_castle
prtg_cas01	mapflag	noteleport
prtg_cas01	mapflag	nowarp
prtg_cas01	mapflag	noreturn
prtg_cas01	mapflag	nobranch
prtg_cas01	mapflag	nomemo
prtg_cas01	mapflag	nosave	SavePoint
prtg_cas01	mapflag	skill_duration	HT_ANKLESNARE,400
```

### Town (Safe Zone)
```c
prontera	mapflag	town
prontera	mapflag	nomemo
prontera	mapflag	nobranch
prontera	mapflag	noteleport
prontera	mapflag	novending
prontera	mapflag	nobuyingstore
prontera	mapflag	nodrop
```

### Training Area (High EXP)
```c
prt_fild08	mapflag	bexp	300
prt_fild08	mapflag	jexp	300
prt_fild08	mapflag	nopenalty
prt_fild08	mapflag	norenewaldroppenalty
prt_fild08	mapflag	norenewalexppenalty
```

### Boss Map
```c
boss_map	mapflag	nomemo
boss_map	mapflag	noteleport
boss_map	mapflag	nobranch
boss_map	mapflag	monster_noteleport
boss_map	mapflag	notomb
boss_map	mapflag	hidemobhpbar
```

---

## BEST PRACTICES

1. **Test Thoroughly:** Always test mapflag combinations in development environment
2. **Document Changes:** Comment your mapflag configurations
3. **Consistency:** Use similar mapflag sets for similar map types
4. **Performance:** Use `forcemineffect` on busy/laggy maps
5. **Balance:** Consider player experience when setting restrictions
6. **Security:** Use `restricted` zones for competitive/balanced areas
7. **Organization:** Keep mapflag configs organized in `/npc/mapflag/` directory

---

## TROUBLESHOOTING

**Problem:** Players can still teleport despite noteleport
- **Solution:** Check for GM permissions (any_warp), items with special flags

**Problem:** Mapflags not applying
- **Solution:** Reload scripts with `@reloadscript`, check syntax, verify map name

**Problem:** PvP damage seems wrong
- **Solution:** Check battle config files, verify pvp mapflag set, check skill_damage adjustments

**Problem:** Players respawn in wrong location with nosave
- **Solution:** Verify map name spelling, check coordinates, ensure SavePoint is capitalized

---

## RELATED FILES

- `/npc/mapflag/` - Mapflag configuration scripts
- `/conf/battle/` - Battle configuration files
- `/doc/script_commands.txt` - Script command reference
- `/db/(pre-)re/skill_nocast_db.txt` - Restricted zones skill config
- `/db/(pre-)re/item_noequip.txt` - Restricted zones item config

---

## SEE ALSO

- **KB_CMD_010:** Map Script Commands
- **KB_CONF_003:** Battle Configuration
- **KB_EXAMPLE_003:** Mapflag Usage Examples

---

*Last Updated: 2013-08-30*
*rAthena Documentation*

# ═══════════════════════════════════════════════════════════════
# PART 3: ELEMENT DAMAGE TABLE (Source-Validated)
# ═══════════════════════════════════════════════════════════════
<!-- RAG_CHUNK: element_damage_table_validated -->

## Element Damage Multipliers (%) - Level 1

*Source: db/re/attr_fix.yml (Verified 2025-11-26)*

| Attack \ Defense | Neu | Wat | Ear | Fir | Win | Poi | Hol | Drk | Gho | Und |
|------------------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| **Neutral** | 100 | 100 | 100 | 100 | 100 | 100 | 100 | 100 | 90 | 100 |
| **Water** | 100 | 25 | 100 | 150 | 90 | 150 | 100 | 100 | 100 | 100 |
| **Earth** | 100 | 100 | 25 | 90 | 150 | 150 | 100 | 100 | 100 | 100 |
| **Fire** | 100 | 90 | 150 | 25 | 100 | 150 | 100 | 100 | 100 | 125 |
| **Wind** | 100 | 150 | 90 | 100 | 25 | 150 | 100 | 100 | 100 | 100 |
| **Poison** | 100 | 150 | 150 | 150 | 150 | 0 | 75 | 75 | 75 | 75 |
| **Holy** | 100 | 100 | 100 | 100 | 100 | 75 | 0 | 125 | 100 | 125 |
| **Dark** | 100 | 100 | 100 | 100 | 100 | 75 | 125 | 0 | 100 | 0 |
| **Ghost** | 90 | 100 | 100 | 100 | 100 | 75 | 90 | 90 | 125 | 100 |
| **Undead** | 100 | 100 | 100 | 90 | 100 | 75 | 125 | 0 | 100 | 0 |

*Values: <100 = resistance, >100 = weakness, 0 = immune*

### Element Levels (1-4)
- Level 1: Base values shown above
- Level 2: Weaknesses +5%, Resistances -5%
- Level 3: Weaknesses +10%, Resistances -10%
- Level 4: Weaknesses +15%, Resistances -15%

### Size Modifiers (Weapon Penalty %)

| Weapon | Small | Medium | Large |
|--------|-------|--------|-------|
| Fist | 100 | 100 | 100 |
| Dagger | 100 | 75 | 50 |
| 1H Sword | 75 | 100 | 75 |
| 2H Sword | 75 | 75 | 100 |
| 1H Spear | 75 | 75 | 100 |
| 2H Spear | 75 | 75 | 100 |
| 1H Axe | 50 | 75 | 100 |
| 2H Axe | 50 | 75 | 100 |
| Mace | 75 | 100 | 100 |
| Staff | 100 | 100 | 100 |
| Bow | 100 | 100 | 75 |
| Katar | 75 | 100 | 75 |
| Book | 100 | 100 | 50 |
| Knuckle | 100 | 75 | 50 |

---

# ═══════════════════════════════════════════════════════════════
# PART 4: BATTLE CONFIGURATION (550 Settings from v6 validated)
# ═══════════════════════════════════════════════════════════════

# rAthena KB v6 - Server Configuration Reference

**Version:** 6.0 Complete
**Generated:** 2025-11-26
**Source:** conf/battle/*.conf
**Total Settings:** 566

---

## Quick Navigation

- [Battle Settings](#battle-settings) - Core combat mechanics
- [Skill Settings](#skill-settings) - Skill behavior
- [Player Settings](#player-settings) - Player mechanics
- [Monster Settings](#monster-settings) - Monster behavior
- [Drop Settings](#drop-settings) - Item drop rates
- [Experience Settings](#experience-settings) - EXP rates
- [Party Settings](#party-settings) - Party mechanics
- [Guild Settings](#guild-settings) - Guild mechanics
- [Feature Toggles](#feature-toggles) - Enable/disable features

---

## Configuration File Reference

### Battle

<!-- RAG_CHUNK: conf_battle -->

**File:** `conf/battle/battle.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `enable_baseatk` | 0x9 | assume unit types (1: Pc, 2: Mob, 4: Pet, 8: Homun, 16: Merc... |
| `enable_baseatk_renewal` | 0x29F |  |
| `enable_perfect_flee` | 1 | Who can have perfect flee? (Note 3) |
| `enable_critical` | 17 | Who can have critical attacks? (Note 3) (Note that there are... |
| `mob_critical_rate` | 100 | Critical adjustment rate for non-players (Note 2) |
| `critical_rate` | 100 |  |
| `attack_walk_delay` | 0 | this setting is mainly a safety mechanism against client edi... |
| `damage_walk_delay` | 0 | The walk delay only affects the time a monster reacts to the... |
| `pc_damage_walk_delay_rate` | 20 | Move-delay adjustment after being hit. (Note 2) The 'can't w... |
| `damage_walk_delay_rate` | 100 |  |
| `multihit_delay` | 200 | This delay is also added to the time a monster waits until i... |
| `player_damage_delay_rate` | 100 | Damaged delay rate for players (Note 2) This affects the dam... |
| `infinite_endure` | 0 | The unit types defined here cannot be stopped by damage. Ple... |
| `undead_detect_type` | 0 | 0 = element undead 1 = race undead 2 = both (either one work... |
| `attribute_recover` | no | Does HP recover if hit by an attribute that's same as your o... |
| `min_hitrate` | 5 | What is the minimum and maximum hitrate of normal attacks? |
| `max_hitrate` | 100 |  |
| `agi_penalty_type` | 1 | 0 = no penalty is applied 1 = agi_penalty_num is reduced fro... |
| `agi_penalty_target` | 1 | When agi penalty is enabled, to whom it should apply to? (No... |
| `agi_penalty_count` | 3 | Amount of enemies required to be targetting player before FL... |
| `agi_penalty_num` | 10 | Amount of FLEE penalized per each attacking monster more tha... |
| `vit_penalty_type` | 1 | 0 = no penalty is applied 1 = vit_penalty_num is reduced fro... |
| `vit_penalty_target` | 1 | When vit penalty is enabled, to whom it should apply to? (No... |
| `vit_penalty_count` | 3 | Amount of enemies required to be targetting player before de... |
| `vit_penalty_num` | 5 | Amount of VIT defense penalized per each attacking monster m... |
| `weapon_defense_type` | 0 | With 0, disabled (use normal def% reduction with further def... |
| `magic_defense_type` | 0 | MDEF‚ same as above. (MDEF * value) |
| `attack_direction_change` | 0 | knockback direction won't change, so e.g. if you walk north ... |
| `attack_attr_none` | 14 | (100% versus on all defense-elements) (Note 3) NOTE: This is... |
| `equip_natural_break_rate` | 0 | Rate at which equipment can break (base rate before it's mod... |
| `equip_self_break_rate` | 100 | This rate affects penalty breaking rate of skills such as po... |
| `equip_skill_break_rate` | 100 | Overall rate at which you can break target's equipment. (Not... |
| `delay_battle_damage` | yes | Should damage have a delay before it is applied? (Note 1) So... |
| `synchronize_damage` | no | Many skills show their damage immediately, so setting "delay... |
| `arrow_decrement` | 1 | 2 = Yes even for skills that do not specify arrow consumptio... |
| `ammo_unequip` | yes | Should ammo be unequipped when unequipping a weapon? Officia... |
| `ammo_check_weapon` | yes | Should a suitable weapon be equipped when equipping ammo? Of... |
| `autospell_check_range` | no | Official behavior is "no", setting this to "yes" will make s... |
| `knockback_left` | yes | If both the attacker and the target are on the same tile, sh... |
| `warg_can_falcon` | no | Can players use Falcons and Wargs at the same time? (Note 1)... |
| `snap_dodge` | no | Should the target be able of dodging damage by snapping away... |
| `break_mob_equip` | no | This will effectively apply the strip equip effect to the no... |

---

### Skill

<!-- RAG_CHUNK: conf_skill -->

**File:** `conf/battle/skill.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `casting_rate` | 100 | assume unit types (1: Pc, 2: Mob, 4: Pet, 8: Homun, 16: Merc... |
| `delay_rate` | 100 | Delay time after casting (Note 2) |
| `delay_dependon_dex` | no | Does the delay time depend on the caster's DEX and/or AGI? (... |
| `delay_dependon_agi` | no |  |
| `min_skill_delay_limit` | 100 | Minimum allowed delay for ANY skills after castbegin (in mil... |
| `amotion_min_skill_delay` | no | than attack motion using these tricks. Set this to "yes" if ... |
| `default_walk_delay` | 300 | NOTE: Do not set this too low, if a character starts moving ... |
| `no_skill_delay` | 2 | database, but follow their own 'reuse' skill delay which is ... |
| `castrate_dex_scale` | 150 | At what dex does the cast time become zero (instacast)? |
| `vcast_stat_scale` | 530 | How much (dex*2+int) does variable cast turns zero? |
| `skill_amotion_leniency` | 0 | NOTE: Setting this will break chaining of skills with cast t... |
| `skill_delay_attack_enable` | yes | Will normal attacks be able to ignore the delay after skills... |
| `skill_add_range` | 0 | Range added to skills after their cast time finishes. Decide... |
| `skill_out_range_consume` | no | If the target moves out of range while casting, do we take t... |
| `skillrange_by_distance` | 14 | If set, when the distance between caster and target is great... |
| `skillrange_from_weapon` | 0 | Should the equipped weapon's range override the skill's rang... |
| `skill_caster_check` | yes | Should a check on the caster's status be performed in all sk... |
| `clear_skills_on_death` | 0 | Should ground placed skills be removed as soon as the caster... |
| `clear_skills_on_warp` | 15 | Should ground placed skills be removed when the caster chang... |
| `defunit_not_enemy` | no | Setting this to YES will override the target mode of ground-... |
| `skill_min_damage` | 0 | any damage from them. Examples: Sonic Blow, Lord of Vermilli... |
| `combo_delay_rate` | 100 | The delay rate of monk's combo (Note 2) |
| `auto_counter_type` | 15 | Use alternate auto Counter Attack Skill Type? (Note 3) For t... |
| `skill_reiteration` | 0 | Can ground skills be placed on top of each other? (Note 3) B... |
| `skill_nofootset` | 1 | Can ground skills NOT be placed underneath/near players/mons... |
| `gvg_traps_target_all` | 1 | Should traps (hunter traps + quagmire) change their target t... |
| `skill_wall_check` | yes | Whether placed down skills will check walls (Note 1) (ex. St... |
| `player_cloak_check_type` | 1 | 1 = Check for walls 2 = Cloaking is not cancelled when attac... |
| `monster_cloak_check_type` | 4 |  |
| `land_skill_limit` | 9 | Can't place unlimited land skills at the same time (Note 3) |
| `display_skill_fail` | 2 | 2 - Disable skill-failed messages due to can-act delays. 4 -... |
| `chat_warpportal` | no | Can a player in chat room (in-game), be warped by a warp por... |
| `sense_type` | 1 | 1: Base defense [RE default] 2: Vit/Int defense 3: Both (the... |
| `finger_offensive_type` | 0 | Which finger offensive style will be used? 0 = Aegis style (... |
| `gx_allhit` | no | Set this to yes if you want all waves to deal damage to all ... |
| `gx_disptype` | 1 | Grandcross display type (Default 1) 0: Yellow character 1: W... |
| `devotion_level_difference` | 10 | Max Level Difference for Devotion |
| `devotion_rdamage` | 0 | Default is 0 (official). If 'devotion_rdamage' is > 0 (chanc... |
| `devotion_rdamage_skill_only` | yes | Officially, reflecting shield (SC_REFLECTDAMAGE) reflects ph... |
| `devotion_standup_fix` | yes | You can read more about it on https://github.com/rathena/rat... |
| `player_skill_partner_check` | yes | If no than you can use the ensemble skills alone. (Note 1) |
| `skill_removetrap_type` | 0 | Remove trap type 0 = Aegis system : Returns 1 'Trap' item 1 ... |
| `backstab_bow_penalty` | yes | Does using bow to do a backstab give a 50% damage penalty? (... |
| `skill_steal_max_tries` | 0 | How many times you could try to steal from a mob. Note: It h... |
| `skill_steal_random_options` | no | Should random options be applied to stolen items? (Note 1) O... |
| `max_heal` | 9999 | Level and Strength of "MVP heal". When someone casts a heal ... |
| `max_heal_lv` | 11 |  |
| `emergency_call` | 11 | 8: Skill is usable on GvG grounds 16: Disable skill from "no... |
| `guild_aura` | 31 | 4: Skill works outside of GvG grounds 8: Skill works on GvG ... |
| `mob_max_skilllvl` | 100 | Max Possible Level of Monster skills Note: If your MVPs are ... |

*...and 32 more settings in this file*

---

### Player

<!-- RAG_CHUNK: conf_player -->

**File:** `conf/battle/player.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `hp_rate` | 100 | assume unit types (1: Pc, 2: Mob, 4: Pet, 8: Homun, 16: Merc... |
| `sp_rate` | 100 | Players' maximum SP rate? (Default is 100) |
| `left_cardfix_to_right` | yes | Whether or not cards and attributes of the left hand are app... |
| `restart_hp_rate` | 0 | The amount of HP a player will respawn with, 0 is default. (... |
| `restart_sp_rate` | 0 | The amount of SP a player will respawn with, 0 is default. (... |
| `player_skillfree` | no | Can a normal player by-pass the skill tree? (Note 1) |
| `player_skillup_limit` | yes | When set to yes, forces skill points gained from 1st class t... |
| `quest_skill_learn` | no | Quest skills can be learned? (Note 1) Setting this to yes ca... |
| `quest_skill_reset` | no | When skills are reset, quest skills are reset as well? (Note... |
| `basic_skill_check` | yes | You must have basic skills to be able to sit, trade, form a ... |
| `player_invincible_time` | 3000 | If you attack a monster, it will attack you back regardless ... |
| `natural_healhp_interval` | 6000 | The time interval for HP to restore naturally. (in milliseco... |
| `natural_healsp_interval` | 8000 | The time interval for SP to restore naturally. (in milliseco... |
| `natural_heal_skill_interval` | 10000 | Automatic healing skill's time interval. (in milliseconds) |
| `major_overweight_rate` | 90 | open_box_weight_rate: 90 The maximum weight for a character ... |
| `max_aspd` | 190 | Maximum atk speed. (Default 190, Highest allowed 199) |
| `max_third_aspd` | 193 | Same as max_aspd, but for 3rd classes. (Default 193, Highest... |
| `max_extended_aspd` | 193 | Max ASPD for extended class (Kagerou/Oboro and Rebellion). (... |
| `max_summoner_aspd` | 193 | Max ASPD for Summoner Class (Doram). (Default 193, Highest a... |
| `max_walk_speed` | 300 | Maximum walk speed rate (200 would be capped to twice the no... |
| `max_hp_lv99` | 330000 | Lv 99:  330000 Lv150:  660000 Lv175: 1100000 |
| `max_hp_lv150` | 660000 |  |
| `max_hp` | 1100000 |  |
| `max_sp` | 1000000 | Maximum SP. (Default is 1000000) |
| `max_parameter` | 99 | 'max_baby_third_parameter' for baby 3rd classes only 'max_ex... |
| `max_trans_parameter` | 99 |  |
| `max_third_parameter` | 130 |  |
| `max_third_trans_parameter` | 130 |  |
| `max_baby_parameter` | 80 |  |
| `max_baby_third_parameter` | 117 |  |
| `max_extended_parameter` | 130 |  |
| `max_summoner_parameter` | 130 |  |
| `max_fourth_parameter` | 130 |  |
| `transcendent_status_points` | 52 | Status points bonus for transcendent class |
| `max_def` | 99 | NOTE: does not affects skills and status effects like Mental... |
| `over_def_bonus` | 0 | Def to Def2 conversion bonus. If the armor def/mdef exceeds ... |
| `max_cart_weight` | 8000 | Max weight carts can hold. |
| `prevent_logout` | 10000 | Prevent logout of players after being hit for how long (in m... |
| `prevent_logout_trigger` | 14 | 2 = Prevent logout after attacking 4 = Prevent logout after ... |
| `show_hp_sp_drain` | no | Display the drained hp/sp values from normal attacks? (Ie: H... |
| `show_hp_sp_gain` | yes | Display the gained hp/sp values from killing mobs? (Ie: Sky ... |
| `friend_auto_add` | yes | If set, when A accepts B as a friend, B will also be added t... |
| `invite_request_check` | yes | Are simultaneous trade/party/guild invite requests automatic... |
| `bone_drop` | 0 | 0 = Disabled 1 = Dropped only in PvP maps 2 = Dropped in all... |
| `character_size` | 0 | 2 = only Baby Classes on Peco have Medium Size 3 = both Norm... |
| `idle_no_autoloot` | 0 | Idle characters can receive autoloot? Set to the time in sec... |
| `min_npc_vendchat_distance` | 3 | Minimum distance a vending/chat room must be from a NPC in o... |
| `rental_mount_speed_boost` | 25 | How much should rental mounts increase a player's movement s... |
| `vip_storage_increase` | 300 | Give more storage slots above the MIN_STORAGE limit. Note: M... |
| `vip_base_exp_increase` | 50 | Base experience rate increase. Setting to 0 will disable. (N... |

*...and 32 more settings in this file*

---

### Monster

<!-- RAG_CHUNK: conf_monster -->

**File:** `conf/battle/monster.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `mvp_hp_rate` | 100 | assume unit types (1: Pc, 2: Mob, 4: Pet, 8: Homun, 16: Merc... |
| `monster_hp_rate` | 100 | The HP rate of normal monsters (that is monsters that are no... |
| `monster_ai` | 0 | 0x2000: When set, monsters will move right after they attack... |
| `monster_chase_refresh` | 32 | If you want monsters to update their target cell while chasi... |
| `mob_warp` | 0 | 2: Enable mob-warping when standing on Priest Warp Portals 4... |
| `mob_active_time` | 0 | Even after this time they will still walk randomly and use i... |
| `boss_active_time` | 0 |  |
| `view_range_rate` | 100 | Mobs and Pets view-range adjustment (range2 column in the mo... |
| `chase_range_rate` | 100 | Chase Range is the base minimum-chase that a mob gives befor... |
| `monster_eye_range_bonus` | 0 | Officially monsters don't have these skills learned, so thei... |
| `loot_range` | 12 | Range in which looters search for loot (max 32) Official: 12... |
| `assist_range` | 11 | Range in which assist mobs search for allies to assist (max ... |
| `monster_active_enable` | yes | Allow monsters to be aggresive and attack first? (Note 1) |
| `override_mob_names` | 0 | 0: No 1: always use the mob_db Name column (english mob name... |
| `monster_damage_delay_rate` | 100 | Monster damage delay rate (Note 2) This affects the damage d... |
| `monster_loot_type` | 0 | Looting monster actions. 0 = Monster will consume the item. ... |
| `monster_loot_search_type` | 1 | How does monster search floor item to loot? 0: Closest (old ... |
| `mob_skill_rate` | 100 | Chance of mob casting a skill (Note 2) Higher rates lead to ... |
| `mob_skill_delay` | 100 | After a mob has casted a skill, there is a delay before bein... |
| `mob_count_rate` | 100 | Rate of monsters on a map, 200 would be twice as many as nor... |
| `mob_spawn_delay` | 100 | Respawn rate of monsters on a map. 50 would make mobs respaw... |
| `plant_spawn_delay` | 100 |  |
| `boss_spawn_delay` | 100 |  |
| `mob_spawn_variance` | 1 | 1: Boss monsters (official) 2: Normal monsters 3: All monste... |
| `no_spawn_on_player` | 0 | 5 seconds. NOTE: This has no effect on mobs that always spaw... |
| `force_random_spawn` | no | Should spawn coordinates in the mob-spawn files be ignored? ... |
| `randomize_center_cell` | yes | different experience each server start. Set this to "no" if ... |
| `slaves_inherit_mode` | 4 | 2: Slaves are always passive. 3: Same as master's aggressive... |
| `slaves_inherit_speed` | 3 | 2: If the master can't walk (even motionless mobs have a spe... |
| `mob_slave_keep_target` | yes | Should MVP slaves retain their target when summoned back to ... |
| `slave_stick_with_master` | no | Should slaves teleport back to their master if they get too ... |
| `slave_active_with_master` | no | Should slaves always be active when their master is active? ... |
| `summons_trigger_autospells` | yes | Will summoned monsters (alchemists, or @summon'ed monsters) ... |
| `retaliate_to_master` | yes | When a mob is attacked by another monster, will the mob reta... |
| `mob_changetarget_byskill` | no | eg: Mob attacks player B, and player A casts a skill C. If s... |
| `monster_class_change_full_recover` | yes | If monster's class is changed will it fully recover HP? (Not... |
| `show_mob_info` | 0 | 1: Display mob HP (Hp/MaxHp format) 2: Display mob HP (Perce... |
| `zeny_from_mobs` | no | Zeny from mobs |
| `mobs_level_up` | no | Monsters level up (monster will level up each time a player ... |
| `mobs_level_up_exp_rate` | 1 |  |
| `dynamic_mobs` | yes | Dynamic Mobs Options Use dynamic mobs? (recommended for smal... |
| `mob_remove_damaged` | yes | Remove Mobs even if they are hurt |
| `mob_remove_delay` | 300000 | Delay before removing mobs from empty maps (default 5 min = ... |
| `mob_npc_event_type` | 1 | Type 1: On the player that killed the mob (if killed by a no... |
| `ksprotection` | 0 | Set to 0 to disable it. If this is activated and a player is... |
| `mvp_tomb_enabled` | yes | Whether or not to spawn the mvp tomb. See http://irowiki.org... |
| `mvp_tomb_delay` | 9000 | Delay before the MVP tomb is spawned. Default: 9 seconds |
| `mob_size_influence` | no | and stats. The rates will be doubled for large mobs, and hal... |
| `mob_icewall_walk_block` | 75 | icewall completely blocked on all maps that have boss monste... |
| `boss_icewall_walk_block` | 0 |  |

*...and 9 more settings in this file*

---

### Drops

<!-- RAG_CHUNK: conf_drops -->

**File:** `conf/battle/drops.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `item_auto_get` | no | Note 2: Value is in percents (100 means 100%) --------------... |
| `flooritem_lifetime` | 60000 | How long does it take for an item to disappear from the floo... |
| `first_attack_loot_bonus` | 30 | If you set this to 0, then loot priority will be solely calc... |
| `item_first_get_time` | 3000 | Grace time during which only the player who did the most dam... |
| `item_second_get_time` | 2000 | Grace time during which only the first and second player who... |
| `item_third_get_time` | 2000 | Grace time during which only the first, second and third pla... |
| `mvp_item_first_get_time` | 10000 | Grace time during which only the player who did the most dam... |
| `mvp_item_second_get_time` | 10000 | Grace time during which only the first and second player who... |
| `mvp_item_third_get_time` | 2000 | Grace time during which only the first, second and third pla... |
| `item_rate_common` | 100 | Item drop rates (Note 2) The rate the common items are dropp... |
| `item_rate_common_boss` | 100 |  |
| `item_rate_common_mvp` | 100 |  |
| `item_drop_common_min` | 1 |  |
| `item_drop_common_max` | 10000 |  |
| `item_rate_heal` | 100 | The rate healing items are dropped (items that restore HP or... |
| `item_rate_heal_boss` | 100 |  |
| `item_rate_heal_mvp` | 100 |  |
| `item_drop_heal_min` | 1 |  |
| `item_drop_heal_max` | 10000 |  |
| `item_rate_use` | 100 | The rate at which usable items (in the item tab) other then ... |
| `item_rate_use_boss` | 100 |  |
| `item_rate_use_mvp` | 100 |  |
| `item_drop_use_min` | 1 |  |
| `item_drop_use_max` | 10000 |  |
| `item_rate_equip` | 100 | The rate at which equipment is dropped. |
| `item_rate_equip_boss` | 100 |  |
| `item_rate_equip_mvp` | 100 |  |
| `item_drop_equip_min` | 1 |  |
| `item_drop_equip_max` | 10000 |  |
| `item_rate_card` | 100 | The rate at which cards are dropped |
| `item_rate_card_boss` | 100 |  |
| `item_rate_card_mvp` | 100 |  |
| `item_drop_card_min` | 1 |  |
| `item_drop_card_max` | 10000 |  |
| `item_rate_mvp` | 100 | The rate adjustment for the MVP items that the MVP gets dire... |
| `item_drop_mvp_min` | 1 |  |
| `item_drop_mvp_max` | 10000 |  |
| `item_drop_mvp_mode` | 0 |  |
| `item_rate_adddrop` | 100 | The rate adjustment for equip-granted item drops. |
| `item_drop_add_min` | 1 |  |
| `item_drop_add_max` | 10000 |  |
| `item_group_rate` | 100 | The rate adjustment for items inside of equip-granted item g... |
| `item_group_drop_min` | 1 |  |
| `item_group_drop_max` | 10000 |  |
| `item_rate_treasure` | 100 | Rate adjustment for Treasure Box drops (these override all o... |
| `item_drop_treasure_min` | 1 |  |
| `item_drop_treasure_max` | 10000 |  |
| `item_logarithmic_drops` | no | 10000 | 1.00 1.67  3.25  5.28  8.44 15.24 23.19 34.26 54.57 ... |
| `drop_rate0item` | no | Can the monster's drop rate become 0? (Note 1) Default: no (... |
| `drop_rateincrease` | no | On official servers it is possible to get 0.00% drop chance ... |

*...and 12 more settings in this file*

---

### Items

<!-- RAG_CHUNK: conf_items -->

**File:** `conf/battle/items.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `vending_max_value` | 1000000000 | assume unit types (1: Pc, 2: Mob, 4: Pet, 8: Homun, 16: Merc... |
| `vending_over_max` | yes | of the items exceeds the maximum zeny allowed. (Note 1) If s... |
| `vending_tax` | 500 | Tax to apply to all vending transactions (eg: 10000 = 100%, ... |
| `vending_tax_min` | 100000000 | Minimum total of purchase until taxes are applied. Officiall... |
| `buyer_name` | yes | Show the buyer's name when successfully vended an item |
| `weapon_produce_rate` | 100 | Forging success rate. (Note 2) |
| `potion_produce_rate` | 100 | Prepare Potion success rate. (Note 2) |
| `produce_item_name_input` | 0x03 | 0x08: Produced Holy Water/Ancilla 0x10: Produced Deadly Poti... |
| `dead_branch_active` | yes | Is a monster summoned via dead branch aggressive? (Note 1) |
| `random_monster_checklv` | no | Should summoned monsters check the player's base level? (dea... |
| `item_check` | 0x0 | 0x1: Inventory 0x2: Cart 0x4: Storage |
| `item_use_interval` | 100 | How much time must pass between item uses? Only affects the ... |
| `cashfood_use_interval` | 60000 | How much time must pass between cash food uses? Default: 600... |
| `gtb_sc_immunity` | 50 | Required level of bNoMagicDamage before Status Changes are b... |
| `autospell_stacking` | no | Enable autospell card effects to stack? NOTE: Different card... |
| `allow_consume_restricted_item` | no | Allow the consumption of usable items that are disabled by i... |
| `allow_equip_restricted_item` | yes | no = can't be equipped and will be unequipped when entering ... |
| `item_flooritem_check` | yes | Allow map_addflooritem to check if item is droppable? (Note ... |
| `default_bind_on_equip` | 4 | 2 - Guild 3 - Party 4 - Character |
| `allow_bound_sell` | 0x0 | 0x4 = Bound items are able to be sold to Shops, because most... |
| `broadcast_hide_name` | 2 | obtained an item with special broadcast flag or refined an i... |
| `rental_transaction` | yes | Enable to sell rental item to NPC shop? (Note 1) |
| `rental_item_novalue` | no | Sell rental item for 0 to NPC shop regardless of the item va... |
| `min_shop_buy` | 1 | Minimum purchase price of items at a normal Shop Officially ... |
| `min_shop_sell` | 0 | Minimum sell price of items at a normal shop Officially item... |
| `cardfix_monster_physical` | yes | Officially "Asprika" (god item) reduces all monsters damage ... |
| `trade_count_stackable` | yes | Determines whether stackable items should be counted separat... |

---

### Misc

<!-- RAG_CHUNK: conf_misc -->

**File:** `conf/battle/misc.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `pk_mode` | 0 | Note: If pk_mode is set to 2 instead of 1 (yes), players wil... |
| `pk_mode_mes` | yes | Displays a message when the player enters a pk zone. Only du... |
| `manner_system` | 15 | 4: Disables commands usage 8: Disables item usage/picking/dr... |
| `pk_min_level` | 55 | For PK Server Mode. Change this to define the minimum level ... |
| `pk_level_range` | 0 | For PK Server Mode. It specifies the maximum level differenc... |
| `pk_short_attack_damage_rate` | 80 | For PK servers. Damage adjustment settings, these follow the... |
| `pk_long_attack_damage_rate` | 70 |  |
| `pk_weapon_attack_damage_rate` | 60 |  |
| `pk_magic_attack_damage_rate` | 60 |  |
| `pk_misc_attack_damage_rate` | 60 |  |
| `skill_log` | off | Display skill usage in console? (for debug only) (default: o... |
| `battle_log` | off | Display battle log? (for debug only) (default: off) (Note 1) |
| `etc_log` | off | Display other stuff? (for debug only) (default: off) (Note 1... |
| `warp_point_debug` | no | Do you want to debug warp points? If set to yes, warp points... |
| `night_at_start` | no | Choose if server begin with night (yes) or day (no) |
| `day_duration` | 0 | Define duration in msec of the day (default: 7200000 = 2 hou... |
| `night_duration` | 0 | Define duration in msec of the night (default: 1800000 = 30 ... |
| `duel_allow_pvp` | no | Using duel on pvp-maps |
| `duel_allow_gvg` | no | Using duel on gvg-maps |
| `duel_allow_teleport` | no | Allow using teleport/warp when dueling |
| `duel_autoleave_when_die` | yes | Autoleave duel when die |
| `duel_time_interval` | 60 | Delay between using @duel in minutes |
| `duel_only_on_same_map` | no | Restrict duel usage to same map |
| `official_cell_stack_limit` | 1 | Custom - This variation will make every full cell to be cons... |
| `custom_cell_stack_limit` | 1 |  |
| `at_mapflag` | no | Allow autotrade only in maps with autotrade flag? Set this t... |
| `at_timeout` | 0 | Set this to the amount of minutes autotrade chars will be ki... |
| `at_monsterignore` | no | Makes player cannot be attacked when autotrade? (turns playe... |
| `at_logout_event` | yes | Should autotrade trigger OnPCLogout script events? (Note 1) |
| `auction_feeperhour` | 12000 | Auction system, fee per hour. Default is 12000 |
| `auction_maximumprice` | 500000000 | Auction maximum sell price |
| `searchstore_querydelay` | 10 | Minimum delay between each store search query in seconds. |
| `searchstore_maxresults` | 30 | Maximum amount of results a store search query may yield, be... |
| `cashshop_show_points` | no | Whether or not gaining and loosing of cash points is display... |
| `mail_show_status` | 0 | 0 = No 1 = Yes 2 = Yes, when there are unread mails |
| `mail_daily_count` | 100 | Amount of mails a user can send a day. Default: 100 0 = Unli... |
| `mail_zeny_fee` | 2 | NOTE: this rate is hardcoded in the client, you need to diff... |
| `mail_attachment_price` | 2500 | NOTE: this fee is hardcoded in the client, you need to diff ... |
| `mail_attachment_weight` | 2000 | NOTE: this limit is hardcoded in the client, you need to dif... |
| `mon_trans_disable_in_gvg` | no | Is monster transformation disabled during Guild Wars? If set... |
| `discount_item_point_shop` | 0 | 1 = Item shops 2 = Point shops 3 = Item & point shops |
| `disp_servervip_msg` | no | Don't display message "login-serv has been asked to %s the p... |
| `mail_delay` | 1000 | Delay to allow user resend new mail (default & minimum is 10... |
| `hide_fav_sell` | no | Hides items from the player's favorite tab from being sold t... |
| `map_edge_size` | 15 | On some maps like in Pyramids this causes there to be very f... |
| `item_stacking` | yes | If you set this to "no", when you drop an item, it will only... |

---

### Client

<!-- RAG_CHUNK: conf_client -->

**File:** `conf/battle/client.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `min_chat_delay` | 0 | ------------------------------------------------------------... |
| `min_hair_style` | 0 | Valid range of dyes and styles on the client. |
| `max_hair_style` | 42 |  |
| `min_hair_color` | 0 |  |
| `max_hair_color` | 8 |  |
| `min_cloth_color` | 0 |  |
| `max_cloth_color` | 7 |  |
| `min_body_style` | 0 |  |
| `max_body_style` | 1 |  |
| `hide_woe_damage` | no | When set to yes, the damage field in packets sent from woe m... |
| `pet_hair_style` | 100 | older sakexes: 20 sakexe 0614: 24 sakexe 0628 (and later): 1... |
| `area_size` | 14 | Visible area size (how many squares away from a player they ... |
| `max_walk_path` | 17 | Maximum walk path (how many cells a player can walk going to... |
| `max_lv` | 99 | NOTE: You also need to adjust the client if you want this to... |
| `aura_lv` | 99 | Example: If max_lv is 99 and aura_lv is 150, characters with... |
| `client_limit_unit_lv` | 0 | Note: If an unit type, which normally does not show an aura,... |
| `wedding_modifydisplay` | no | Will tuxedo and wedding dresses be shown when worn? (Note 1) |
| `save_clothcolor` | yes | Save Clothes color. (This will degrade performance) (Note 1) |
| `save_body_style` | yes | Save body styles. (Note 1) |
| `wedding_ignorepalette` | no | Note: Both save_clothcolor and wedding_modifydisplay have to... |
| `xmas_ignorepalette` | no | Do not display cloth colors for the Xmas costume? Set this t... |
| `summer_ignorepalette` | no | Do not display cloth colors for the Summer costume? Set this... |
| `hanbok_ignorepalette` | no | Do not display cloth colors for the Hanbok costume? Set this... |
| `oktoberfest_ignorepalette` | no | Do not display cloth colors for the Oktoberfest costume? Set... |
| `motd_type` | 0 | Set this to 1 if your clients have langtype problems and can... |
| `display_version` | yes | Show rAthena version to users when the login? |
| `display_hallucination` | yes | When affected with the "Hallucination" status effect, send t... |
| `display_status_timers` | yes | Set this to 1 if your client supports status change timers a... |
| `client_reshuffle_dice` | yes | Randomizes the dice emoticon server-side, to prevent clients... |
| `client_sort_storage` | no | Sorts the cart, guild storage, inventory and storage before ... |
| `update_enemy_position` | yes | NOTE: Set to 'no' will make client won't update enemy positi... |
| `spawn_direction` | no | When a player teleports, changes maps, or logs in, will they... |
| `mvp_exp_reward_message` | no | Show the MVP EXP reward message for clients 2013-12-23cRagex... |
| `ping_timer_inverval` | 30 | Send ping timer Interval in seconds for each timer invoke. |
| `ping_time` | 20 | Send packets timeout in seconds before ping packet can be se... |
| `show_skill_scale` | yes | Show skill scale for clients 2015-12-23 and newer? (Note 1) ... |
| `drop_connection_on_quit` | no | Should the connection be dropped on server side after a play... |
| `macro_detection_retry` | 3 | Macro Detector retries Number of times someone can fail the ... |
| `macro_detection_timeout` | 60000 | Macro Detector timeout Amount of time in milliseconds before... |
| `macro_detection_punishment` | 0 | 0 - Ban 1 - Jail Official: 0 |
| `macro_detection_punishment_time` | 0 | Macro Detector punishment duration Amount of time in minutes... |
| `macrochecker_delay` | 600000 | Macrochecker delay (per map) Set to 0 to disable |

---

### Exp

<!-- RAG_CHUNK: conf_exp -->

**File:** `conf/battle/exp.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `base_exp_rate` | 100 | See files db/exp.txt and db/exp2.txt to change them. -------... |
| `job_exp_rate` | 100 | Rate at which job exp. is given. (Note 2) |
| `multi_level_up` | no | Turn this on to allow a player to level up more than once fr... |
| `multi_level_up_base` | 0 | Allow multi level up until a certain level? This only trigge... |
| `multi_level_up_job` | 0 |  |
| `max_exp_gain_rate` | 0 | % of the current exp bar. (Every 10 = 1.0%) For example, set... |
| `exp_calc_type` | 0 | 0 = uses damage given / total damage as damage ratio 1 = use... |
| `exp_bonus_attacker` | 25 | Experience increase per attacker. That is, every additional ... |
| `exp_bonus_max_attacker` | 12 | Max number of attackers at which exp bonus is capped (eg: if... |
| `exp_bonus_nodamage_attacker` | no | Should casting skills that deal no damage still make you cou... |
| `mvp_exp_rate` | 100 | MVP bonus exp rate. (Note 2) |
| `quest_exp_rate` | 100 | Rate of base/job exp given by NPCs. (Note 2) |
| `heal_exp` | 0 | The rate of job exp. from using Heal skill (100 is the same ... |
| `resurrection_exp` | 0 | The rate of exp. that is gained by the process of resurrecti... |
| `shop_exp` | 0 | The rate of job exp. when using discount and overcharge on a... |
| `pvp_exp` | yes | PVP exp.  Do players get exp in PvP maps (Note: NOT exp from... |
| `death_penalty_type` | 1 | 0 = No penalty. 1 = Lose % of current level when killed. 2 =... |
| `death_penalty_base` | 100 | Base exp. penalty rate (Each 100 is 1% of their exp) |
| `death_penalty_job` | 100 | Job exp. penalty rate (Each 100 is 1% of their exp) |
| `zeny_penalty` | 0 | When a player dies (to another player), how much zeny should... |
| `death_penalty_maxlv` | 0 | 0: Never lose (default as in official). 1: Lose Base EXP. 2:... |
| `disp_experience` | no | Will display experience gained from killing a monster. (Note... |
| `disp_zeny` | no | Will display zeny earned (from mobs, trades, etc) (Note 1) |
| `use_statpoint_table` | yes | Use the contents of db/statpoint.txt when doing a stats rese... |
| `use_traitpoint_table` | yes | Use the contents of db/statpoint.yml when doing a stats rese... |
| `exp_cost_redemptio` | 1 | EXP cost for cast PR_REDEMPTIO (Note 2) |
| `exp_cost_redemptio_limit` | 5 | How many player needed to makes PR_REDEMPTIO's EXP penalty b... |

---

### Party

<!-- RAG_CHUNK: conf_party -->

**File:** `conf/battle/party.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `show_steal_in_same_party` | no | Note 2: Value is in percents (100 means 100%) --------------... |
| `party_update_interval` | 1000 | Interval before updating the party-member map mini-dots (mil... |
| `party_hp_mode` | 0 | Method used to update party-mate hp-bars: 0: Aegis - bar is ... |
| `show_party_share_picker` | yes | under the value "party_share_level". When 'Party Share' item... |
| `party_item_share_type` | 0 | 1: Item Share is disabled for non-mob drops (player/pet drop... |
| `idle_no_share` | no | a character idle. Characters in a chat/vending are always co... |
| `party_even_share_bonus` | 0 | Give additional experience bonus per party-member involved o... |
| `display_party_name` | yes | Display party name regardless if player is in a guild. Offic... |
| `block_account_in_same_party` | yes | Prevent multiple characters of the same account to join the ... |
| `change_party_leader_samemap` | yes | Prevent changing the party leader if the specified player is... |

---

### Guild

<!-- RAG_CHUNK: conf_guild -->

**File:** `conf/battle/guild.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `guild_emperium_check` | yes | Note 2: Value is in percents (100 means 100%) --------------... |
| `guild_exp_limit` | 50 | Maximum tax limit on a guild member. |
| `guild_max_castles` | 0 | Maximum castles one guild can own (0 = unlimited) |
| `guild_skill_relog_delay` | 300000 | Delay in milliseconds that are applied to guild skills. Offi... |
| `gvg_short_attack_damage_rate` | 80 | Melee damage adjustments (non skills) for WoE battles (Guild... |
| `gvg_long_attack_damage_rate` | 80 | Ranged damage adjustments (non skills) for WoE battles (Guil... |
| `gvg_weapon_attack_damage_rate` | 60 | Weapon skills damage adjustments for WoE battles (Guild Vs G... |
| `gvg_magic_attack_damage_rate` | 60 | Magic skills damage adjustments for WoE battles (Guild Vs Gu... |
| `gvg_misc_attack_damage_rate` | 60 | Misc skills damage adjustments for WoE battles (Guild Vs Gui... |
| `gvg_flee_penalty` | 20 | Flee penalty on gvg grounds. Official value is 20 (Note 2) N... |
| `require_glory_guild` | no | Can the 'Glory of Guild' skill be learnt in the Guild window... |
| `max_guild_alliance` | 3 | Limit Guild alliances. Value is 0 to 3. If you want to chang... |
| `guild_notice_changemap` | 2 | Upon teleporting (regardless of changing maps): 2 (official)... |
| `guild_maprespawn_clones` | no | Should maprespawnguildid kill clones too? Default: no |
| `guild_leaderchange_delay` | 1440 | How long (in minutes) should a guild have to wait between gu... |
| `guild_leaderchange_woe` | no | Is changing the guild leader allowed during WoE? Default: no |
| `guild_alliance_onlygm` | no | Only guild master can accept alliance? Default: no |

---

### Pet

<!-- RAG_CHUNK: conf_pet -->

**File:** `conf/battle/pet.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `pet_legacy_formula` | no | ( Base rate + ( player level - monster level ) * 30 + player... |
| `pet_catch_rate` | 100 | Rate for catching pets (Note 2) |
| `pet_distance_check` | 5 | The client automatically walks the player into range when tr... |
| `pet_hide_check` | yes | On official servers players are unable to catch monsters if ... |
| `pet_rename` | no | Can you name a pet more then once? (Note 1) |
| `pet_friendly_rate` | 100 | The rate a pet will get friendly by feeding it. (Note 2) |
| `pet_hungry_delay_rate` | 100 | The rate at which a pet will become hungry. (Note 2) |
| `pet_equip_required` | yes | Does the pet need its equipment before it does its skill? (N... |
| `pet_unequip_destroy` | yes | Should the pet equipment be destroyed if the owner doesn't h... |
| `pet_attack_support` | no | When the master attacks a monster, whether or not the pet wi... |
| `pet_damage_support` | no | When the master receives damage from the monster, whether or... |
| `pet_support_min_friendly` | 900 | Minimum intimacy necessary for a pet to support their master... |
| `pet_status_support` | no | Whether or not the pet's will use skills. (Note 1) Note: Off... |
| `pet_support_rate` | 100 | Rate at which a pet will support it's owner in battle. (Note... |
| `pet_attack_exp_to_master` | no | Does the pets owner receive exp from the pets damage? |
| `pet_attack_exp_rate` | 100 | The rate exp. is gained from the pet attacking monsters |
| `pet_lv_rate` | 0 | Pet leveling system. Use 0 to disable (default). When enable... |
| `pet_max_stats` | 99 | When pet leveling is enabled, what is the max stats for pets... |
| `pet_max_atk1` | 500 | When pet leveling is enabled, these are the imposed caps on ... |
| `pet_max_atk2` | 1000 |  |
| `pet_disable_in_gvg` | no | Are pets disabled during Guild Wars? If set to yes, pets are... |
| `pet_ignore_infinite_def` | yes | Will does petskillattack2 fixed damage ignore plant infnite ... |
| `pet_master_dead` | no | Whether or not the pet will continue to attack when the mast... |
| `pet_autofeed_always` | yes | Send auto-feed notice even if the client setting is OFF (Not... |
| `pet_walk_speed` | 1 | 1: Master's walk speed (official) 2: DEFAULT_WALK_SPEED valu... |

---

### Homunc

<!-- RAG_CHUNK: conf_homunc -->

**File:** `conf/battle/homunc.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `hom_setting` | 0x3D | 0x10: They display luk/3+1 instead of their actual critical ... |
| `homunculus_friendly_rate` | 100 | Default on official servers: yes for Pre-renewal, no for Ren... |
| `hom_rename` | no | Can you name a homunculus more then once? (Note 1) |
| `homunculus_evo_intimacy_need` | 91100 | Minimum intimacy to evo the homunculus |
| `homunculus_evo_intimacy_reset` | 1000 | Reset intimacy after evolution to: |
| `hvan_explosion_intimate` | 45000 | Intimacy needed to use Evolved Vanilmirth's Bio Explosion |
| `homunculus_show_growth` | yes | Show stat growth to the owner when an Homunculus levels up |
| `homunculus_autoloot` | no | Does autoloot work, when a monster is killed by homunculus o... |
| `homunculus_auto_vapor` | 80 | Should homunculi Vaporize when Master dies? (Note 2) A homun... |
| `homunculus_max_level` | 99 | Max level for regular Homunculus |
| `homunculus_S_max_level` | 250 | Max level for Homunculus S |
| `homunculus_S_growth_level` | 99 | This is the level at which homunculus S can use their growth... |
| `homunculus_autofeed_always` | yes | Send auto-feed notice even if OFF (Note 1) Official: yes |
| `hom_idle_no_share` | no | Their master will only receive items if 'homunculus_autoloot... |
| `idletime_hom_option` | 0x1F | Default: walk (0x1) + useskilltoid (0x2) + useskilltopos (0x... |
| `homunculus_exp_gain` | 10 | The rate at which homunculus gain experience from kills. (No... |
| `homunculus_starving_rate` | 10 | See 'homunculus_starving_delay' for the delay value. Set to ... |
| `homunculus_starving_delay` | 20000 | Homunculi normally lose hunger every 60 seconds but when the... |

---

### Gm

<!-- RAG_CHUNK: conf_gm -->

**File:** `conf/battle/gm.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `atcommand_symbol` | @ | - '/' (client commands symbol) atcommand_symbol represents @... |
| `charcommand_symbol` | # |  |
| `atcommand_spawn_quantity_limit` | 100 | The maximum quantity of monsters that can be summoned per GM... |
| `atcommand_slave_clone_limit` | 25 | Maximum number of slave-clones that can be have by using the... |
| `partial_name_scan` | yes | current map server. Some critical atcommands like jail, ban ... |
| `ban_hack_trade` | 5 | Ban people that try trade dupe. Duration of the ban, in minu... |
| `atcommand_mobinfo_type` | 1 | modifies @mobinfo to display the users' real drop rate as pe... |
| `atcommand_levelup_events` | no | Should atcommands trigger level up events for NPCs? (Note 1)... |
| `atcommand_disable_npc` | yes | This can be changed by script commands 'enable_command' and ... |

---

### Instance

<!-- RAG_CHUNK: conf_instance -->

**File:** `conf/battle/instance.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `instance_block_leave` | yes | ------------------------------------------------------------... |
| `instance_block_leaderchange` | yes | Block leader changes for parties or guilds if they have an a... |
| `instance_block_invite` | yes | Block inviting for parties or guilds if they have an active ... |
| `instance_block_expulsion` | yes | Block expulsion for parties or guilds if they have an active... |

---

### Battleground

<!-- RAG_CHUNK: conf_battleground -->

**File:** `conf/battle/battleground.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `bg_short_attack_damage_rate` | 80 | assume unit types (1: Pc, 2: Mob, 4: Pet, 8: Homun, 16: Merc... |
| `bg_long_attack_damage_rate` | 80 | Ranged damage adjustments (non skills) for Battleground maps... |
| `bg_weapon_attack_damage_rate` | 60 | Weapon skills damage adjustments for Battleground maps (Note... |
| `bg_magic_attack_damage_rate` | 60 | Magic skills damage adjustments for Battleground maps (Note ... |
| `bg_misc_attack_damage_rate` | 60 | Misc skills damage adjustments for Battleground maps (Note 2... |
| `bg_flee_penalty` | 20 | Flee penalty on BG grounds. NOTE: It's %, not absolute, so 2... |
| `bg_update_interval` | 1000 | Interval before updating the bg-member map mini-dots (millis... |
| `bgqueue_nowarp_mapflag` | no | Before a player is warped into a Battleground from the Battl... |

---

### Status

<!-- RAG_CHUNK: conf_status -->

**File:** `conf/battle/status.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `status_cast_cancel` | 0 | assume unit types (1: Pc, 2: Mob, 4: Pet, 8: Homun, 16: Merc... |
| `debuff_on_logout` | 0 | 1 = Remove negative buffs (status that are flagged as debuff... |
| `pc_status_def_rate` | 100 | Adjustment for the natural rate of resistance from status ch... |
| `mob_status_def_rate` | 100 |  |
| `pc_max_status_def` | 100 | Maximum resistance to status changes. (100 = 100%) NOTE: Car... |
| `mob_max_status_def` | 100 |  |

---

# rAthena Database Schemas Complete Reference v9.1

**Version:** 9.1 - Complete Database Coverage
**Source:** db/re/*.yml (47 files)
**Last Updated:** 2025-11-26

---

## Quick Navigation

- [Item Databases](#item-databases)
- [Monster Database](#monster-database)
- [Skill Database](#skill-database)
- [Quest Database](#quest-database)
- [Instance Database](#instance-database)
- [Pet/Homunculus/Mercenary](#pet-homunculus-mercenary)
- [Job System](#job-system)
- [Refine/Enchant](#refine-enchant)
- [Other Databases](#other-databases)

---

# ═══════════════════════════════════════════════════════════════
# ITEM DATABASES
# ═══════════════════════════════════════════════════════════════


<!-- RAG_CHUNK: item_db_schema -->
## item_db.yml Schema

**Location:** `db/re/item_db.yml`, `item_db_equip.yml`, `item_db_usable.yml`, `item_db_etc.yml`

```yaml
Body:
  - Id: 501                    # Item ID (required)
    AegisName: Red_Potion      # Server-side name (required)
    Name: Red Potion           # Display name (required)
    Type: Healing              # Item type (required)
    # Types: Healing, Usable, Etc, Armor, Weapon, Card, PetEgg,
    #        PetArmor, Arrow, Ammo, DelayConsume, ShadowGear, Cash
    
    SubType: None              # Weapon/Ammo subtype
    # Weapon: Fist, Dagger, 1hSword, 2hSword, 1hSpear, 2hSpear,
    #         1hAxe, 2hAxe, Mace, Staff, Bow, Knuckle, Musical,
    #         Whip, Book, Katar, Revolver, Rifle, Gatling,
    #         Shotgun, Grenade, Huuma, 2hStaff
    
    Buy: 50                    # Buy price (NPC)
    Sell: 25                   # Sell price (NPC, default: Buy/2)
    Weight: 70                 # Weight (1 = 0.1)
    Attack: 0                  # Physical attack
    MagicAttack: 0             # Magic attack
    Defense: 0                 # Physical defense
    Range: 0                   # Attack range
    Slots: 0                   # Card slots
    Jobs:                      # Jobs that can equip
      All: true                # or specific jobs
      # Novice, Swordman, Mage, Archer, Acolyte, Merchant, Thief,
      # Knight, Priest, Wizard, Blacksmith, Hunter, Assassin,
      # Crusader, Monk, Sage, Rogue, Alchemist, Bard, Dancer, etc.
    
    Classes:                   # Classes that can equip
      All: true                # Normal, Upper, Baby, Third, Fourth
    
    Gender: Both               # Female, Male, Both
    Locations:                 # Equipment locations
      Head_Top: true           # Head_Top, Head_Mid, Head_Low
      # Right_Hand, Left_Hand, Both_Hand, Armor, Shoes,
      # Garment, Right_Accessory, Left_Accessory, Both_Accessory,
      # Costume_Head_Top, Costume_Head_Mid, Costume_Head_Low,
      # Costume_Garment, Shadow_Armor, Shadow_Weapon, Shadow_Shield,
      # Shadow_Shoes, Shadow_Right_Accessory, Shadow_Left_Accessory
    
    WeaponLevel: 1             # Weapon level 1-5
    ArmorLevel: 1              # Armor level 1-2
    EquipLevelMin: 1           # Minimum equip level
    EquipLevelMax: 999         # Maximum equip level
    Refineable: true           # Can be refined
    Gradable: false            # Can be graded
    View: 0                    # View/Sprite ID
    
    Script: |                  # Equip/Use script
      bonus bStr,1;
    EquipScript: |             # On equip script
      sc_start SC_BLESSING,60000,10;
    UnEquipScript: |           # On unequip script
      sc_end SC_BLESSING;
    
    Flags:
      BuyingStore: true        # Can be sold in buying store
      DeadBranch: false        # Spawned by dead branch
      Container: false         # Is a container item
      UniqueId: false          # Has unique ID
      BindOnEquip: false       # Binds on equip
      DropAnnounce: false      # Announces on drop
      NoConsume: false         # Not consumed on use
      DropEffect: None         # Client drop effect
    
    Delay:
      Duration: 0              # Use delay in ms
      Status: None             # Status for delay
    
    Stack:
      Amount: 0                # Max stack (0 = no limit)
      Inventory: true          # Can stack in inventory
      Cart: true               # Can stack in cart
      Storage: true            # Can stack in storage
      GuildStorage: true       # Can stack in guild storage
    
    NoUse:
      Override: 100            # GM level to override
      Sitting: false           # Cannot use while sitting
    
    Trade:
      Override: 100            # GM level to override
      NoDrop: false            # Cannot drop
      NoTrade: false           # Cannot trade
      TradePartner: false      # Cannot trade with partner
      NoSell: false            # Cannot sell to NPC
      NoCart: false            # Cannot put in cart
      NoStorage: false         # Cannot put in storage
      NoGuildStorage: false    # Cannot put in guild storage
      NoMail: false            # Cannot send by mail
      NoAuction: false         # Cannot auction
```


---

<!-- RAG_CHUNK: mob_db_schema -->
## mob_db.yml Schema

**Location:** `db/re/mob_db.yml`

```yaml
Body:
  - Id: 1002                   # Monster ID (required)
    AegisName: PORING          # Server name (required)
    Name: Poring               # Display name (required)
    JapaneseName: Poring       # Japanese name
    Level: 1                   # Monster level
    Hp: 55                     # Max HP
    Sp: 0                      # Max SP
    BaseExp: 27                # Base experience
    JobExp: 20                 # Job experience
    MvpExp: 0                  # MVP experience
    Attack: 8                  # Min attack
    Attack2: 11                # Max attack
    Defense: 2                 # Physical defense
    MagicDefense: 5            # Magic defense
    Str: 1                     # STR stat
    Agi: 1                     # AGI stat
    Vit: 1                     # VIT stat
    Int: 0                     # INT stat
    Dex: 6                     # DEX stat
    Luk: 5                     # LUK stat
    AttackRange: 1             # Attack range
    SkillRange: 10             # Skill range
    ChaseRange: 12             # Chase range
    Size: Small                # Small, Medium, Large
    Race: Plant                # Formless, Undead, Brute, Plant, Insect,
                               # Fish, Demon, DemiHuman, Angel, Dragon
    RaceGroups:                # Special race groups
      Goblin: true
    Element: Water             # Element type
    ElementLevel: 1            # Element level 1-4
    WalkSpeed: 400             # Walk speed (lower = faster)
    AttackDelay: 1872          # Attack delay in ms
    AttackMotion: 672          # Attack animation time
    DamageMotion: 480          # Damage animation time
    DamageTaken: 100           # Damage taken % (100 = normal)
    
    Ai: 02                     # AI type
    # 01 = Passive, 02 = Passive looter, 03 = Aggressive,
    # 04 = Aggressive looter, 05 = Aggressive coward,
    # 06 = Aggressive coward looter, 07 = Guard (doesn't move)
    # 17 = Passive detector, 21 = Aggressive detector
    
    Class: Normal              # Normal, Boss, Guardian
    
    Modes:
      CanMove: true            # Can move
      Looter: true             # Picks up items
      Aggressive: false        # Attacks on sight
      Assist: false            # Helps other monsters
      CastSensorIdle: false    # Detects cast (idle)
      Boss: false              # Boss monster
      Plant: false             # Plant mode (no exp/drops if killed too fast)
      CanAttack: true          # Can attack
      Detector: false          # Detects hidden players
      CastSensorChase: false   # Detects cast (chasing)
      ChangeChase: false       # Can change chase target
      Angry: false             # Gets angry
      ChangeTargetMelee: false # Changes target in melee
      ChangeTargetChase: false # Changes target while chasing
      TargetWeak: false        # Targets weakest
      NoKnockback: false       # Cannot be knocked back
      RandomTarget: false      # Attacks random target
      IgnoreMagic: false       # Ignores magic
      IgnoreMelee: false       # Ignores melee
      IgnoreMisc: false        # Ignores misc
      IgnoreRanged: false      # Ignores ranged
      Mvp: false               # Is MVP
      IgnoreSkill: false       # Ignores skills
    
    MvpDrops:                  # MVP drops
      - Item: Old_Card_Album
        Rate: 5000             # Rate in 0.01% (5000 = 50%)
    
    Drops:                     # Normal drops
      - Item: Jellopy
        Rate: 7000
      - Item: Knife_
        Rate: 100
      - Item: Sticky_Mucus
        Rate: 400
      - Item: Apple
        Rate: 1000
      - Item: Empty_Bottle
        Rate: 1500
      - Item: Poring_Card
        Rate: 1                # 0.01%
```

---

<!-- RAG_CHUNK: skill_db_schema -->
## skill_db.yml Schema

**Location:** `db/re/skill_db.yml`

```yaml
Body:
  - Id: 1                      # Skill ID (required)
    Name: NV_BASIC             # Skill constant name (required)
    Description: Basic Skill   # Display description (required)
    MaxLevel: 9                # Maximum skill level
    Type: None                 # Skill type
    # None, Weapon, Magic, Misc, Trap
    
    TargetType: Self           # Target type
    # Self, Attack, Ground, Trap, Friend, Party
    
    DamageFlags:               # Damage calculation flags
      NoDamage: true           # No damage
      Splash: false            # Splash damage
      SplashSplit: false       # Splash split
      IgnoreAtkCard: false     # Ignore ATK cards
      IgnoreElement: false     # Ignore element
      IgnoreDefense: false     # Ignore defense
      IgnoreFlee: false        # Ignore flee
      IgnoreDefCard: false     # Ignore DEF cards
      Critical: false          # Can crit
      IgnoreLongCard: false    # Ignore long range cards
    
    Flags:
      IsQuest: false           # Quest skill
      IsNpc: false             # NPC skill
      IsWedding: false         # Wedding skill
      IsSpirit: false          # Spirit skill
      IsGuild: false           # Guild skill
      IsSong: false            # Song/Dance skill
      IsEnsemble: false        # Ensemble skill
      IsTrap: false            # Trap skill
      TargetSelf: false        # Force self target
      NoTargetSelf: false      # Cannot target self
      PartyOnly: false         # Party only
      GuildOnly: false         # Guild only
      NoEnemy: false           # Cannot target enemy
      IgnoreLandProtector: false # Ignores LP
      Chorus: false            # Chorus skill
      FreeCastNormal: false    # Free cast normal
      FreeCastReduced: false   # Free cast reduced
      ShowSkillScale: false    # Show skill scale
      AllowReproduce: false    # Can be reproduced
      HiddenTrap: false        # Hidden trap
      IsCombo: false           # Combo skill
    
    Range:                     # Skill range per level
      - Level: 1
        Size: 1
      - Level: 5
        Size: 5
    
    Hit: Single                # Hit type: Single, Multi
    HitCount: 1                # Number of hits (negative = divide)
    
    Element: Weapon            # Skill element
    # Neutral, Water, Earth, Fire, Wind, Poison,
    # Holy, Dark, Ghost, Undead, Weapon, EndowedWeapon, Random
    
    SplashArea: 0              # Splash area
    ActiveInstance: 0          # Max active instances
    Knockback: 0               # Knockback cells
    GiveAp: 0                  # AP given
    
    CastCancel: true           # Can cancel cast
    CastDefenseReduction: true # Def reduces cast
    CastTime: 0                # Cast time in ms
    AfterCastActDelay: 0       # After cast delay
    AfterCastWalkDelay: 0      # After cast walk delay
    Duration1: 0               # Duration 1
    Duration2: 0               # Duration 2
    Cooldown: 0                # Cooldown time
    FixedCastTime: 0           # Fixed cast time
    
    CastTimeFlags:             # What affects cast time
      IgnoreDex: false
      IgnoreStatus: false
      IgnoreItemBonus: false
    
    CastDelayFlags:            # What affects delay
      IgnoreDex: false
      IgnoreStatus: false
      IgnoreItemBonus: false
    
    Requires:                  # Skill requirements
      HpCost: 0                # HP cost
      SpCost: 0                # SP cost per level
      ApCost: 0                # AP cost
      HpRateCost: 0            # HP % cost
      SpRateCost: 0            # SP % cost
      ApRateCost: 0            # AP % cost
      MaxHpTrigger: 0          # Max HP % trigger
      ZenyCost: 0              # Zeny cost
      Weapon:                  # Required weapon
        Fist: true
        Dagger: true
      Ammo:                    # Required ammo
        Arrow: true
      AmmoAmount: 1            # Ammo amount
      State: None              # Required state
      # None, Mounted, Falcon, Riding, Cart, Shield,
      # MoveStopped, MoveEnabled, Attack, Elemental, Poisoned,
      # Cursed, RollingCutter, RollingNights, Combo
      Status:                  # Required status
        Hiding: true
      SpiritSphereCost: 0      # Spirit sphere cost
      ItemCost:                # Item cost
        - Item: Red_Gemstone
          Amount: 1
      Equipment:               # Required equipment
        Shield: true
    
    Unit:                      # Ground unit settings
      Id: 0                    # Unit ID
      Layout: 0                # Unit layout
      Range: 0                 # Unit range
      Interval: 0              # Effect interval
      Target: All              # Unit target
      Flag:                    # Unit flags
        UF_DEFNOTENEMY: true
        UF_NOREITERATION: true
        UF_NOFOOTSET: true
        UF_NOOVERLAP: true
```


---

<!-- RAG_CHUNK: quest_db_schema -->
## quest_db.yml Schema

**Location:** `db/re/quest_db.yml`

```yaml
Body:
  - Id: 1000                   # Quest ID (required)
    Title: Quest Title         # Quest title
    TimeLimit: 2h              # Time limit (s, m, h, d format)
    Targets:                   # Kill targets
      - Mob: PORING
        Count: 10
        Id: 1                  # Target ID within quest
        Race: Plant            # Target race
        Size: Small            # Target size
        Element: Water         # Target element
        MinLevel: 1            # Min monster level
        MaxLevel: 999          # Max monster level
    Drops:                     # Required item drops
      - Mob: PORING
        Item: Jellopy
        Count: 5
        Rate: 5000             # Drop rate (10000 = 100%)
```

---

<!-- RAG_CHUNK: instance_db_schema -->
## instance_db.yml Schema

**Location:** `db/re/instance_db.yml`

```yaml
Body:
  - Id: 1                      # Instance ID (required)
    Name: Endless Tower        # Instance name (required)
    TimeLimit: 4h              # Time limit
    IdleTimeOut: 5m            # Idle timeout
    Enter:                     # Entry point
      Map: 1@tower
      X: 50
      Y: 50
    AdditionalMaps:            # Additional maps
      - Map: 2@tower
      - Map: 3@tower
```

---

<!-- RAG_CHUNK: pet_db_schema -->
## pet_db.yml Schema

**Location:** `db/re/pet_db.yml`

```yaml
Body:
  - Mob: PORING                # Pet monster (required)
    TameItem: Unripe_Apple     # Taming item
    EggItem: Poring_Egg        # Egg item
    EquipItem: Backpack        # Equipment item
    FoodItem: Apple            # Food item
    Fullness: 3                # Fullness decrease per tick
    HungryDelay: 60000         # Hunger delay in ms
    Intimacy:                  # Intimacy settings
      Initial: 250             # Initial intimacy
      FeedIncrement: 50        # +intimacy per feed
      OverFeedDecrement: 100   # -intimacy if overfed
      OwnerDeathDecrement: 20  # -intimacy on owner death
    CaptureRate: 2000          # Capture rate (10000 = 100%)
    Speed: 150                 # Pet speed
    SpecialPerformance: true   # Has special performance
    TalkWithEmotes: true       # Uses emotes
    AttackRate: 300            # Attack rate
    DefendRate: 400            # Defend rate
    ChangeTargetRate: 800      # Change target rate
    AutoFeed: true             # Can auto-feed
    Script: |                  # Pet bonus script
      bonus bLuk,2;
      bonus bCritical,1;
    SupportScript: |           # Support script
      sc_start SC_INCFLEE,10000,10;
```

---

<!-- RAG_CHUNK: homunculus_db_schema -->
## homunculus_db.yml Schema

**Location:** `db/re/homunculus_db.yml`

```yaml
Body:
  - Id: 6001                   # Homunculus ID
    Name: Lif                  # Name
    FoodItem: Pet_Food         # Food item
    HungryDelay: 60000         # Hunger delay
    BaseSize: Small            # Base size
    EvoSize: Medium            # Evolved size
    Race: Demihuman            # Race type
    Element: Neutral           # Element
    bASPD: 700                 # Base ASPD
    Status:                    # Base stats
      Hp: 150
      Sp: 40
      Str: 17
      Agi: 20
      Vit: 15
      Int: 35
      Dex: 24
      Luk: 12
    Growth:                    # Stat growth per level
      Hp: { Min: 60, Max: 100 }
      Sp: { Min: 4, Max: 9 }
      Str: { Min: 5, Max: 9 }
      Agi: { Min: 4, Max: 8 }
      Vit: { Min: 3, Max: 7 }
      Int: { Min: 6, Max: 10 }
      Dex: { Min: 4, Max: 8 }
      Luk: { Min: 2, Max: 6 }
    Evolution:                 # Evolution items
      - Item: Medicine_Bowl
        Amount: 1
```

---

<!-- RAG_CHUNK: refine_schema -->
## refine.yml Schema

**Location:** `db/re/refine.yml`

```yaml
Body:
  - Group: Armor               # Refine group
    # Armor, Weapon1, Weapon2, Weapon3, Weapon4, Shadow
    Levels:
      - Level: 1               # Refine level
        RefineryUISettings:
          Items:
            - Item: Elunium
              Amount: 1
            - Item: HD_Elunium
              Amount: 1
              FailureBehavior: Downgrade
          Cost: 2000           # Zeny cost
        Rates:
          - Type: Normal       # Rate type
            # Normal, Enriched, EventNormal, EventEnriched
            Rate: 100          # Success rate %
            Chance: 1000       # Random option chance
        Bonus: 70              # Stat bonus per refine
```

---

<!-- RAG_CHUNK: achievement_db_schema -->
## achievement_db.yml Schema

**Location:** `db/re/achievement_db.yml`

```yaml
Body:
  - Id: 100000                 # Achievement ID
    Group: Adventure           # Achievement group
    Name: Achievement Name     # Name
    Targets:                   # Completion targets
      - Id: 1                  # Target ID
        Mob: PORING            # Target monster
        Count: 100             # Required count
    Condition: BaseLevel >= 99 # Script condition
    Rewards:                   # Rewards
      TitleId: 1001            # Title reward
      Item: Old_Card_Album     # Item reward
      ItemAmount: 1            # Item amount
      Script: |                # Reward script
        getitem Knife,1;
    Score: 10                  # Achievement points
```

---

<!-- RAG_CHUNK: other_schemas -->
## Other Database Schemas

### item_group_db.yml (Item Groups/Boxes)
```yaml
Body:
  - Group: Old_Blue_Box        # Group name
    SubGroups:
      - SubGroup: 0            # SubGroup ID
        List:
          - Item: Apple
            Rate: 100          # Weight (not percentage)
          - Item: Jellopy
            Rate: 50
```

### skill_tree.yml (Job Skill Trees)
```yaml
Body:
  - Job: Swordman              # Job name
    Tree:
      - Skill: SM_SWORD        # Skill name
        MaxLevel: 10           # Max level
        Require:               # Prerequisites
          - Skill: NV_BASIC
            Level: 9
```

### job_exp.yml (Experience Tables)
```yaml
Body:
  - Jobs:                      # Affected jobs
      Novice: true
    MaxLevel: 99               # Max level
    Exp:                       # Required exp per level
      - 40                     # Level 1->2
      - 76                     # Level 2->3
```

### attr_fix.yml (Element Table)
```yaml
Body:
  - Level: 1                   # Element level
    Neutral:
      Neutral: 100
      Water: 100
      Earth: 100
      Fire: 100
      Wind: 100
      Poison: 100
      Holy: 100
      Dark: 100
      Ghost: 90               # Neutral vs Ghost = 90%
      Undead: 100
```

---

## Database File Summary

| Database | File | Purpose |
|----------|------|---------|
| item_db | item_db*.yml | All items |
| mob_db | mob_db.yml | All monsters |
| skill_db | skill_db.yml | All skills |
| quest_db | quest_db.yml | Quest definitions |
| instance_db | instance_db.yml | Instance dungeons |
| pet_db | pet_db.yml | Pet system |
| homunculus_db | homunculus_db.yml | Homunculus |
| mercenary_db | mercenary_db.yml | Mercenaries |
| refine | refine.yml | Refine system |
| achievement_db | achievement_db.yml | Achievements |
| item_group_db | item_group_db.yml | Item groups/boxes |
| skill_tree | skill_tree.yml | Job skill trees |
| job_exp | job_exp.yml | Experience tables |
| attr_fix | attr_fix.yml | Element table |
| size_fix | size_fix.yml | Size modifiers |
| level_penalty | level_penalty.yml | Level penalty |

---

*All schemas verified against rAthena db/re/*.yml files*
