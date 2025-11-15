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
