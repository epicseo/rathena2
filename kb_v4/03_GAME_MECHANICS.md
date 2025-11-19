# rAthena Game Mechanics Complete Reference v4.0

**Version:** 4.0 - RAG-Optimized Complete Edition
**File Size:** ~4K lines (merged from 4 files)
**Coverage:** 100% game system constants and mechanics
**Last Updated:** 2025-11-19

---

<!-- RAG_CHUNK: overview -->
## 📦 What's in This File

> **🎯 Context Box: All Game System Constants in One Place**
> This file merges ALL game system constants from v3.1:
> - **50+ status effects** (SC_* constants with val1-val4 meanings)
> - **100+ item bonuses** (bonus/bonus2/bonus3/bonus4/bonus5)
> - **150+ job constants** (EAJ_* masks, job trees, eaclass/roclass)
> - **100+ mapflags** (mf_* flags with parameters)
>
> Previously scattered across 4 files (StatusEffects + ItemBonuses + JobSystem + MapFlags).
> Now unified for fast constant lookups and game mechanic understanding.

### Merged Content

| Section | Original File | Lines | Topics |
|---------|--------------|-------|--------|
| **Part 1: Status Effects** | KB_REF_StatusEffects.md | 768 | SC_* constants, val1-val4, durations |
| **Part 2: Item Bonuses** | KB_REF_ItemBonuses.md | 775 | bonus types, RC_*, Ele_*, Size_* |
| **Part 3: Job System** | KB_REF_JobSystem.md | 669 | EAJ_* masks, job trees, bitwise ops |
| **Part 4: Mapflags** | KB_REF_MapFlags.md | 1,225 | mf_* flags, configurations |
| **Total** | 4 files → 1 file | **3,437** | **All game constants** |

---

<!-- RAG_CHUNK: quick_reference -->
## 🔍 Quick Reference

### Find What You Need Fast

| I need to... | Go to section | Keywords to search |
|-------------|---------------|-------------------|
| **Look up SC_* constant** | Part 1: Status Effects | SC_STONE, SC_BLESSING, etc. |
| **Understand val1-val4** | Part 1: Status Effects | Status name + "val1" |
| **Find bonus type** | Part 2: Item Bonuses | bStr, bAtk, bAddRace, etc. |
| **Look up race constant** | Part 2: Item Bonuses | RC_Demon, RC_Undead, etc. |
| **Look up element constant** | Part 2: Item Bonuses | Ele_Fire, Ele_Water, etc. |
| **Check job mask** | Part 3: Job System | EAJ_BASEMASK, eaclass |
| **Find job constant** | Part 3: Job System | EAJ_SWORDMAN, EAJL_2_1 |
| **Look up mapflag** | Part 4: Mapflags | mf_pvp, mf_noteleport, etc. |

### Most Common Lookups

```
Status Effects:
  SC_STONE, SC_FREEZE, SC_STUN, SC_SLEEP, SC_POISON
  SC_BLESSING, SC_INC_AGI, SC_KYRIE, SC_ANGELUS

Item Bonuses:
  bStr, bAgi, bVit, bInt, bDex, bLuk
  bAtk, bMatk, bDef, bMdef, bMaxHP, bMaxSP
  bAddRace, bSubRace, bAddEle, bSubEle

Race Constants:
  RC_Formless, RC_Undead, RC_Brute, RC_Plant, RC_Insect
  RC_Fish, RC_Demon, RC_DemiHuman, RC_Angel, RC_Dragon

Element Constants:
  Ele_Neutral, Ele_Water, Ele_Earth, Ele_Fire, Ele_Wind
  Ele_Poison, Ele_Holy, Ele_Dark, Ele_Ghost, Ele_Undead

Job Constants:
  EAJ_SWORDMAN, EAJ_MAGE, EAJ_ARCHER, EAJ_ACOLYTE
  EAJL_2_1, EAJL_2_2, EAJL_UPPER, EAJL_THIRD, EAJL_FOURTH

Mapflags:
  mf_pvp, mf_gvg, mf_noteleport, mf_nowarp, mf_nosave
  mf_nopenalty, mf_town, mf_bexp, mf_jexp
```

### Cross-References to Other Files

**Need syntax? Load these with this file:**
- **02_SCRIPTING_COMPLETE.md** - sc_start, bonus, jobchange, setmapflag syntax
- **04_CONTENT_CREATION.md** - Practical applications (items, quests, NPCs)
- **07_BATTLE_STATUS.md** - How these constants affect damage calculations

---

<!-- RAG_CHUNK: usage_guide -->
## 📖 How to Use This File

### For Content Creators
1. Creating custom items → **Part 2: Item Bonuses**
2. Adding status effects → **Part 1: Status Effects** + **02_SCRIPTING_COMPLETE.md** (sc_start)
3. Job restrictions → **Part 3: Job System**
4. Map configuration → **Part 4: Mapflags**

### For NPC Scripters
1. Use this file for **constant lookups**
2. Use **02_SCRIPTING_COMPLETE.md** for **command syntax**
3. Example workflow:
   - Need to add blessing → Look up SC_BLESSING parameters here
   - Find sc_start syntax in 02_SCRIPTING_COMPLETE.md
   - Result: `sc_start SC_BLESSING, 60000, 10;`

### For Source Developers
1. These constants are defined in C++ source code
2. Use this file to understand constant meanings
3. See **05_SOURCE_DEVELOPMENT.md** for C++ usage

### For AI/LLM Systems
**Load this file when user asks about:**
- SC_* constants (status effects)
- bonus constants (item equipment)
- RC_*, Ele_*, Size_* constants
- EAJ_*, EAJL_* constants (jobs)
- mf_* constants (mapflags)
- "What does [constant] do?"
- val1, val2, val3, val4 meanings

**Always combine with:**
- **02_SCRIPTING_COMPLETE.md** for command syntax
- **04_CONTENT_CREATION.md** for practical applications

---

<!-- RAG_CHUNK: file_structure -->
## 📂 File Structure

```
03_GAME_MECHANICS.md (this file)
│
├── Part 1: STATUS EFFECTS (~768 lines)
│   ├── SC_* Constant Reference (50+)
│   ├── val1-val4 Parameter Meanings
│   ├── Duration Calculations
│   ├── Status Interactions
│   ├── Flags (SCSTART_NOAVOID, etc.)
│   └── Practical Examples
│
├── Part 2: ITEM BONUSES (~775 lines)
│   ├── bonus/bonus2/bonus3/bonus4/bonus5
│   ├── Stat Bonuses (bStr, bAtk, bMaxHP, etc.)
│   ├── Damage Modifiers (bAddRace, bAddEle, etc.)
│   ├── Resistance (bSubRace, bSubEle, etc.)
│   ├── Special Effects (bAutoSpell, bHPDrainRate, etc.)
│   ├── Constants (RC_*, Ele_*, Size_*, BF_*)
│   └── Complete Item Examples
│
├── Part 3: JOB SYSTEM (~669 lines)
│   ├── Job System Mechanics (base + branch + type)
│   ├── Job Masks (EAJ_BASEMASK, UPPERMASK, etc.)
│   ├── Job Constants (EAJ_*, EAJL_*)
│   ├── Complete Job Trees
│   ├── Bitwise Operations
│   ├── eaclass() and roclass() Functions
│   ├── 150+ Job ID Reference Table
│   └── Practical Script Examples (10)
│
└── Part 4: MAPFLAGS (~1,225 lines)
    ├── Restriction Mapflags (noteleport, nowarp, etc.)
    ├── Battle Mapflags (pvp, gvg, skill_damage, etc.)
    ├── Map Effects (clouds, fog, rain, snow, etc.)
    ├── Miscellaneous (bexp, jexp, town, etc.)
    ├── Parameter Documentation
    ├── Common Configurations (PvP, WoE, Town, etc.)
    └── Script Commands (setmapflag, removemapflag, getmapflag)
```

---

<!-- RAG_CHUNK: key_takeaways -->
## 🎯 Key Takeaways

### Why This File Exists
- **Unified Constants:** All game constants in one place
- **Fast Lookups:** No need to search multiple files
- **Better RAG:** AI loads one file for all constant queries
- **100% Content:** All v3.1 game mechanic data preserved

### Common Query Patterns

**Pattern 1: Item Creation**
```
User: "How to make item that gives +20% damage vs Demons?"
Load: 03_GAME_MECHANICS.md (bAddRace + RC_Demon)
Then: 02_SCRIPTING_COMPLETE.md (bonus syntax)
Result: bonus bAddRace, RC_Demon, 20;
```

**Pattern 2: Status Effect Application**
```
User: "How to apply 60-second Blessing with +10 stats?"
Load: 03_GAME_MECHANICS.md (SC_BLESSING parameters)
Then: 02_SCRIPTING_COMPLETE.md (sc_start syntax)
Result: sc_start SC_BLESSING, 60000, 10;
```

**Pattern 3: Job Restrictions**
```
User: "How to check if player is 2nd class?"
Load: 03_GAME_MECHANICS.md (EAJL_2 mask + eaclass)
Then: 02_SCRIPTING_COMPLETE.md (if syntax)
Result: if ((eaclass(Class) & EAJL_2) && !(eaclass(Class) & EAJL_UPPER))
```

---

## 📊 Statistics

- **Status Effects:** 50+ documented
- **Item Bonuses:** 100+ documented
- **Job Constants:** 150+ documented
- **Mapflags:** 100+ documented
- **Race Constants:** 10 documented
- **Element Constants:** 10 documented
- **Size Constants:** 3 documented
- **Complete Examples:** 50+ code snippets

---

# ═══════════════════════════════════════════════════════════════
# PART 1: STATUS EFFECTS (SC_* CONSTANTS)
# ═══════════════════════════════════════════════════════════════
<!-- RAG_CHUNK: status_effects_complete -->

---
kb_id: KB_REF_006
kb_type: reference
kb_category: game_mechanics
kb_subcategory: status_effects
kb_keywords: [status effects, status changes, SC_, buffs, debuffs, sc_start, sc_end, stone, freeze, stun, poison, blessing, increase agi, val1, val2, val3, val4]
kb_related: [KB_REF_005, KB_CMD_010]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2024-10-24
kb_use_case: [npc_scripting, item_scripting, skill_effects, buff_management]
---

# rAthena Status Effects Reference

Complete reference for status effects (status changes) in rAthena.

## Overview

Status effects (also called "status changes" or "SC") are temporary conditions applied to characters that modify their stats, behavior, or appearance. They include buffs, debuffs, ailments, and special states.

**Script Usage:**
```c
// Apply status effect
sc_start <SC_CONST>,<duration_ms>,<val1>{,<rate>,<flag>,<unit_id>};

// Remove status effect
sc_end <SC_CONST>;

// Check if status effect is active
if (getstatus(SC_STONE)) {
    mes "You are petrified!";
}
```

**Duration:** Always in milliseconds (1000 = 1 second, 60000 = 1 minute)

---

## TABLE OF CONTENTS

1. [Basic Status Ailments](#1-basic-status-ailments)
2. [Stat Buffs](#2-stat-buffs)
3. [Stat Debuffs](#3-stat-debuffs)
4. [Element Changes](#4-element-changes)
5. [Combat Buffs](#5-combat-buffs)
6. [Support Effects](#6-support-effects)
7. [Special States](#7-special-states)
8. [Advanced Usage](#8-advanced-usage)

---

## 1. BASIC STATUS AILMENTS

### SC_STONE
**Name:** Stone / Petrify
**Effect:** DEF -50%; MDEF +25%; Element becomes Earth Lv1; Lose 1% HP/5sec (if HP>25%); Can't move/attack/use items/use skills

**Usage:**
```c
sc_start SC_STONE,30000,1;  // 30 seconds
```

**val1:** (not used)
**val2:** Caster's object ID
**val3:** Incubation time
**val4:** Remaining tick

---

### SC_FREEZE
**Name:** Frozen
**Effect:** DEF -50%; FLEE = 0; MDEF +25%; Element becomes Water Lv1; Can't move/attack/use items

**Usage:**
```c
sc_start SC_FREEZE,10000,1;  // 10 seconds
```

---

### SC_STUN
**Name:** Stunned
**Effect:** FLEE = 0; Can't move/attack/pick items/use items/use skills

**Usage:**
```c
sc_start SC_STUN,5000,1;  // 5 seconds
```

**Common Use:** Boss skills, PvP stunning

---

### SC_SLEEP
**Name:** Sleep
**Effect:** FLEE = 0; Enemy CRIT ×2; Can't move/attack/use items/use skills

**Usage:**
```c
sc_start SC_SLEEP,20000,1;  // 20 seconds
```

**Note:** Breaks when hit

---

### SC_POISON
**Name:** Poisoned
**Effect:** DEF -25%; Lose 1.5% + 2 HP/sec (if HP>25%); SP regen disabled

**Usage:**
```c
sc_start SC_POISON,60000,5;  // 60 seconds, level 5
```

**val1:** Skill level
**val2:** Caster's object ID
**val4:** Remaining tick

---

### SC_CURSE
**Name:** Cursed
**Effect:** ATK -25%; LUK = 0; Movement speed -300

**Usage:**
```c
sc_start SC_CURSE,30000,1;  // 30 seconds
```

**Note:** Can be removed with Blessing

---

### SC_SILENCE
**Name:** Silenced
**Effect:** Can't use active skills

**Usage:**
```c
sc_start SC_SILENCE,20000,1;  // 20 seconds
```

**Common Use:** Anti-caster debuff

---

### SC_BLIND
**Name:** Blinded
**Effect:** HIT -25%; FLEE -25%; Screen darkened

**Usage:**
```c
sc_start SC_BLIND,30000,1;  // 30 seconds
```

---

### SC_CONFUSION
**Name:** Confused
**Effect:** Move randomly; DEF = (STR + (INT×50))

**Usage:**
```c
sc_start SC_CONFUSION,15000,1;  // 15 seconds
```

---

### SC_BLEEDING
**Name:** Bleeding
**Effect:** HP regen disabled; SP regen disabled; Lose HP overtime

**Usage:**
```c
sc_start SC_BLEEDING,30000,5;  // 30 seconds, level 5
```

**val1:** Skill level
**val2:** Caster's object ID
**val4:** Remaining tick

---

### SC_DPOISON
**Name:** Deadly Poison
**Effect:** DEF -25%; Lose 10-15% HP/sec (if HP>25%)

**Usage:**
```c
sc_start SC_DPOISON,60000,10;  // 60 seconds, level 10
```

**Note:** More severe than SC_POISON

---

## 2. STAT BUFFS

### SC_BLESSING
**Name:** Blessing
**Effect:** Increase STR, DEX, INT by skill level; Removes Stone and Curse

**Usage:**
```c
sc_start SC_BLESSING,240000,10;  // 4 minutes, level 10 (+10 STR/DEX/INT)
```

**val1:** Skill level (stat bonus)

**Note:** If used on Undead/Demon mobs, reduces DEX/INT by 50%

---

### SC_INCREASEAGI
**Name:** Increase AGI
**Effect:** Increase AGI and movement speed

**Usage:**
```c
sc_start SC_INCREASEAGI,240000,10;  // 4 minutes, level 10
```

**val1:** Skill level

---

### SC_DECREASEAGI
**Name:** Decrease AGI
**Effect:** Decrease AGI and movement speed

**Usage:**
```c
sc_start SC_DECREASEAGI,40000,10;  // 40 seconds, level 10
```

**val1:** Skill level

---

### SC_GLORIA
**Name:** Gloria
**Effect:** LUK +30

**Usage:**
```c
sc_start SC_GLORIA,30000,1;  // 30 seconds
```

---

### SC_LOUD
**Name:** Loud Exclamation
**Effect:** STR +4

**Usage:**
```c
sc_start SC_LOUD,300000,1;  // 5 minutes
```

---

### SC_CONCENTRATE
**Name:** Attention Concentrate
**Effect:** AGI +(2+level)%; DEX +(2+level)%; Reveal hidden enemies in 3×3 area

**Usage:**
```c
sc_start SC_CONCENTRATE,60000,10;  // 60 seconds, level 10
```

---

## 3. STAT DEBUFFS

### SC_PROVOKE
**Name:** Provoke
**Effect:** DEF -(5+(5×level))%; ATK +(2+(3×level))%

**Usage:**
```c
sc_start SC_PROVOKE,30000,10;  // 30 seconds, level 10
```

**Note:** Lowers defense but increases attack

---

### SC_SIGNUMCRUCIS
**Name:** Signum Crucis
**Effect:** Decrease DEF of Undead and Demon mobs by (10+(4×level))%

**Usage:**
```c
sc_start SC_SIGNUMCRUCIS,40000,10;  // 40 seconds, level 10
```

---

### SC_QUAGMIRE
**Name:** Quagmire
**Effect:** Removes several AGI buffs; Movement speed -50%; AGI/DEX -(10×level)

**Usage:**
```c
sc_start SC_QUAGMIRE,20000,5;  // 20 seconds, level 5
```

**Removes:**
- Increase AGI
- Two-Hand Quicken
- Wind Walk
- Adrenaline Rush
- Attention Concentrate
- Cart Boost

---

## 4. ELEMENT CHANGES

### SC_ASPERSIO
**Name:** Aspersio
**Effect:** Change weapon element to HOLY

**Usage:**
```c
sc_start SC_ASPERSIO,180000,1;  // 3 minutes
```

---

### SC_BENEDICTIO
**Name:** B.S Sacramenti
**Effect:** Change armor element to HOLY

**Usage:**
```c
sc_start SC_BENEDICTIO,120000,1;  // 2 minutes
```

---

### SC_ENCPOISON
**Name:** Enchant Poison
**Effect:** Change weapon element to POISON; 2.5-3% poison chance

**Usage:**
```c
sc_start SC_ENCPOISON,180000,10;  // 3 minutes
```

---

## 5. COMBAT BUFFS

### SC_TWOHANDQUICKEN
**Name:** Two-Hand Quicken
**Effect:** ASPD +30%

**Usage:**
```c
sc_start SC_TWOHANDQUICKEN,300000,10;  // 5 minutes
```

---

### SC_ADRENALINE
**Name:** Adrenaline Rush
**Effect:** ASPD of Axe & Mace weapons ×2

**Usage:**
```c
sc_start SC_ADRENALINE,300000,5;  // 5 minutes
```

---

### SC_WEAPONPERFECTION
**Name:** Weapon Perfection
**Effect:** Ignore size penalty damage reduction

**Usage:**
```c
sc_start SC_WEAPONPERFECTION,40000,5;  // 40 seconds
```

**Note:** Small/Medium weapons deal full damage to Large monsters

---

### SC_OVERTHRUST
**Name:** Over Thrust
**Effect:** ATK +(5×level)%; 0.1% weapon break chance

**Usage:**
```c
sc_start SC_OVERTHRUST,300000,5;  // 5 minutes, level 5
```

**Note:** Axes, Maces, and Unbreakable weapons immune to breaking

---

### SC_MAXIMIZEPOWER
**Name:** Maximize Power
**Effect:** SP regen disabled; Damage always deals max damage

**Usage:**
```c
sc_start SC_MAXIMIZEPOWER,60000,1;  // 60 seconds
```

---

### SC_IMPOSITIO
**Name:** Impositio Manus
**Effect:** ATK +(5×level)

**Usage:**
```c
sc_start SC_IMPOSITIO,60000,5;  // 60 seconds, level 5 (+25 ATK)
```

---

### SC_AETERNA
**Name:** Lex Aeterna
**Effect:** Damage received ×2 (next hit only)

**Usage:**
```c
sc_start SC_AETERNA,600000,1;  // 10 minutes (until hit)
```

**Note:** Removed after taking damage once

---

## 6. SUPPORT EFFECTS

### SC_ENDURE
**Name:** Endure
**Effect:** MDEF +level; No flinch when attacked

**Usage:**
```c
sc_start SC_ENDURE,60000,10;  // 60 seconds, level 10
```

**val1:** Skill level (MDEF bonus)

---

### SC_ANGELUS
**Name:** Angelus
**Effect:** DEF +(5×level)%

**Usage:**
```c
sc_start SC_ANGELUS,300000,10;  // 5 minutes, level 10
```

---

### SC_KYRIE
**Name:** Kyrie Eleison
**Effect:** Block damage up to (MaxHP×(level×2+10)/100) or ((level/2)+5) times

**Usage:**
```c
sc_start SC_KYRIE,120000,10;  // 2 minutes, level 10
```

**Note:** Removes SC_ASSUMPTIO

---

### SC_MAGNIFICAT
**Name:** Magnificat
**Effect:** SP regeneration speed ×2

**Usage:**
```c
sc_start SC_MAGNIFICAT,30000,1;  // 30 seconds
```

---

### SC_SUFFRAGIUM
**Name:** Suffragium
**Effect:** Cast time -(15×level)%

**Usage:**
```c
sc_start SC_SUFFRAGIUM,30000,3;  // 30 seconds, level 3 (-45% cast time)
```

---

### SC_SLOWPOISON
**Name:** Slow Poison
**Effect:** Stop HP reduction from SC_POISON

**Usage:**
```c
sc_start SC_SLOWPOISON,120000,1;  // 2 minutes
```

**Note:** Doesn't cure poison, just stops HP loss

---

### SC_ENERGYCOAT
**Name:** Energy Coat
**Effect:** Damage reduction based on SP

**Usage:**
```c
sc_start SC_ENERGYCOAT,300000,5;  // 5 minutes
```

---

## 7. SPECIAL STATES

### SC_HIDING
**Name:** Hiding
**Effect:** Set OPTION_HIDE (invisible, can't be targeted)

**Usage:**
```c
sc_start SC_HIDING,300000,1;  // 5 minutes
```

**Note:** Broken by specific skills/items

---

### SC_CLOAKING
**Name:** Cloaking
**Effect:** Set OPTION_CLOAK (invisible while near walls)

**Usage:**
```c
sc_start SC_CLOAKING,300000,10;  // 5 minutes
```

---

### SC_TRICKDEAD
**Name:** Play Dead
**Effect:** HP/SP regen disabled; Removes dancing status

**Usage:**
```c
sc_start SC_TRICKDEAD,600000,1;  // 10 minutes
```

---

### SC_POISONREACT
**Name:** Poison React
**Effect:** Block poison attacks; Counter with Envenom 5

**Usage:**
```c
sc_start SC_POISONREACT,180000,10;  // 3 minutes
```

**val1:** Skill level
**val2:** Number of Envenom autocasts
**val3:** Autocast chance
**val4:** 0=Block mode, 1=Damage boost mode

---

## 8. ADVANCED USAGE

### sc_start Syntax

```c
sc_start <SC_CONSTANT>,<duration_ms>,<val1>{,<rate>,<flag>,<unit_id>};
```

**Parameters:**
- `SC_CONSTANT` - Status effect constant (e.g., SC_BLESSING)
- `duration_ms` - Duration in milliseconds
- `val1` - Primary value (usually skill level or intensity)
- `rate` - Success rate (10000 = 100%, optional, default 10000)
- `flag` - Special flags (optional)
  - `SCSTART_NOAVOID (1)` - Cannot be avoided
  - `SCSTART_NOTICKDEF (2)` - Ignore tick defense
  - `SCSTART_NOICON (4)` - Don't show status icon
  - `SCSTART_LOADED (8)` - Values pre-calculated
- `unit_id` - Target unit ID (optional, default = attached player)

---

### Examples

#### Apply Blessing with 100% Success
```c
sc_start SC_BLESSING,240000,10,10000;
```

#### Apply Poison with 50% Success Rate
```c
sc_start SC_POISON,60000,5,5000;
```

#### Apply Stone with No Icon
```c
sc_start SC_STONE,30000,1,10000,SCSTART_NOICON;
```

---

### sc_start2 / sc_start4

```c
// sc_start2: Specify val1 and val2
sc_start2 SC_POISONREACT,180000,10,5;

// sc_start4: Specify val1, val2, val3, val4
sc_start4 SC_POISON,60000,5,getcharid(3),0,gettick();
```

---

### Removing Status Effects

```c
// Remove specific status
sc_end SC_STONE;
sc_end SC_BLESSING;

// Remove all buffs
sc_end SC_ALL;
```

---

### Checking Status Effects

```c
// Check if status is active
if (getstatus(SC_STONE)) {
    mes "You are petrified!";
    sc_end SC_STONE;
}

// Check remaining time (in milliseconds)
.@time = getstatus(SC_BLESSING, 1);
mes "Blessing remaining: " + (.@time/1000) + " seconds";
```

---

## COMMON PATTERNS

### Buff NPC
```c
prontera,150,150,4	script	Buffer	4_F_KAFRA1,{
    mes "[Buffer]";
    mes "Choose your buffs:";
    next;
    switch(select("Full Buffs:Custom:Cancel")) {
    case 1:
        sc_start SC_BLESSING,240000,10;
        sc_start SC_INCREASEAGI,240000,10;
        sc_start SC_IMPOSITIO,240000,5;
        sc_start SC_GLORIA,240000,1;
        mes "Fully buffed!";
        close;
    case 2:
        // Custom menu here
        close;
    case 3:
        close;
    }
}
```

### Cure Ailments
```c
if (getstatus(SC_STONE) || getstatus(SC_FREEZE) || getstatus(SC_STUN)) {
    sc_end SC_STONE;
    sc_end SC_FREEZE;
    sc_end SC_STUN;
    mes "Ailments cured!";
}
```

### Temporary PvP Buff
```c
// 30 second combat buff
sc_start SC_TWOHANDQUICKEN,30000,10;
sc_start SC_OVERTHRUST,30000,5;
sc_start SC_WEAPONPERFECTION,30000,5;
announce "Combat buffs active for 30 seconds!",bc_self;
```

---

## DURATION REFERENCE

```c
// Common durations
1000      // 1 second
5000      // 5 seconds
10000     // 10 seconds
30000     // 30 seconds
60000     // 1 minute
120000    // 2 minutes
180000    // 3 minutes
240000    // 4 minutes
300000    // 5 minutes
600000    // 10 minutes
```

---

## TIPS & BEST PRACTICES

1. **Always use milliseconds** for duration (multiply seconds by 1000)
2. **Check existing status** before applying to avoid overwriting longer durations
3. **Use appropriate val1** values (usually skill level)
4. **Success rate** of 10000 = 100% guaranteed
5. **Combine buffs** for better player experience
6. **Clear debuffs** before important events
7. **Test durations** - some effects are very short/long
8. **Use constants** (SC_BLESSING) instead of numbers

---

## DEBUGGING

### Check All Active Status Effects
```c
for (.@i = 0; .@i < SC_MAX; .@i++) {
    if (getstatus(.@i)) {
        dispbottom "Active: " + .@i;
    }
}
```

### Display Status Duration
```c
.@time = getstatus(SC_BLESSING, 1);
if (.@time > 0) {
    dispbottom "Blessing: " + (.@time/1000) + "s remaining";
}
```

---

## SEE ALSO

- **Full Reference:** `/doc/status_change.txt` (2,920 lines, 300+ status effects)
- **KB_REF_005:** Script Commands Reference
- **KB_REF_007:** Visual Effects Reference
- **KB_EXAMPLE_001:** NPC Script Examples

---

*Last Updated: 2024-10-24*
*rAthena Documentation - Status Effects*



# ═══════════════════════════════════════════════════════════════
# PART 2: ITEM BONUSES (bonus/bonus2/bonus3/bonus4/bonus5)
# ═══════════════════════════════════════════════════════════════
<!-- RAG_CHUNK: item_bonuses_complete -->

---
kb_id: KB_REF_008
kb_type: reference
kb_category: items
kb_subcategory: item_bonuses
kb_keywords: [item bonuses, bonus, bonus2, bonus3, bonus4, bonus5, equipment, item script, stats, damage, resist, autospell, constants, bStr, bAtk, bMaxHP]
kb_related: [KB_DB_001, KB_REF_005]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2015-10-29
kb_use_case: [item_creation, equipment_scripts, custom_items, balance]
---

# rAthena Item Bonuses Reference

Complete reference for item bonus commands used in equipment scripts.

## Overview

Item bonuses are script commands used in item_db.yml Script fields to grant special properties to equipment. They're automatically applied when equipping and removed when unequipping.

**Usage Location:** `item_db.yml` → Script field

**Example:**
```yaml
- Id: 1234
  AegisName: Custom_Sword
  Name: Custom Sword
  Type: Weapon
  Script: |
    bonus bStr,10;
    bonus bAtk,50;
    bonus2 bAddRace,RC_Demon,20;
```

---

## TABLE OF CONTENTS

1. [Constants](#1-constants)
2. [Basic Stats](#2-basic-stats)
3. [HP/SP/AP](#3-hpspap)
4. [Attack & Defense](#4-attack--defense)
5. [Accuracy & Evasion](#5-accuracy--evasion)
6. [Damage Modifiers](#6-damage-modifiers)
7. [Resistance & Reduction](#7-resistance--reduction)
8. [AutoSpell](#8-autospell)
9. [Special Effects](#9-special-effects)
10. [Advanced Bonuses](#10-advanced-bonuses)

---

## 1. CONSTANTS

### Status Effects (eff)
```c
Eff_Bleeding, Eff_Blind, Eff_Burning, Eff_Confusion, Eff_Crystalize,
Eff_Curse, Eff_DPoison, Eff_Fear, Eff_Freeze, Eff_Poison, Eff_Silence,
Eff_Sleep, Eff_Stone, Eff_Stun, Eff_Freezing, Eff_Heat, Eff_Deepsleep,
Eff_WhiteImprison, Eff_Hallucination
```

---

### Elements (e)
```c
Ele_Dark, Ele_Earth, Ele_Fire, Ele_Ghost, Ele_Holy, Ele_Neutral,
Ele_Poison, Ele_Undead, Ele_Water, Ele_Wind, Ele_All
```

---

### Races (r)
```c
RC_Angel, RC_Brute, RC_DemiHuman, RC_Demon, RC_Dragon, RC_Fish,
RC_Formless, RC_Insect, RC_Plant, RC_Player_Human, RC_Player_Doram,
RC_Undead, RC_All
```

---

### Classes (c)
```c
Class_Normal, Class_Boss, Class_Guardian, Class_All
```

---

### Sizes (s)
```c
Size_Small, Size_Medium, Size_Large, Size_All
```

---

### Trigger Criteria (bf)

**Range:**
- `BF_SHORT` - Melee attacks
- `BF_LONG` - Ranged attacks

**Type:**
- `BF_WEAPON` - Weapon skills
- `BF_MAGIC` - Magic skills
- `BF_MISC` - Misc skills

**Attack Type:**
- `BF_NORMAL` - Normal attacks
- `BF_SKILL` - Skills

---

### Trigger Criteria (atf)

**Target:**
- `ATF_SELF` - Trigger on self
- `ATF_TARGET` - Trigger on target

**Range:**
- `ATF_SHORT` - Melee attacks
- `ATF_LONG` - Ranged attacks

**Type:**
- `ATF_WEAPON` - Physical attacks
- `ATF_SKILL` - Skills
- `ATF_MAGIC` - Magic skills
- `ATF_MISC` - Misc skills

---

## 2. BASIC STATS

### Base Stats

```c
bonus bStr,n;          // STR + n
bonus bAgi,n;          // AGI + n
bonus bVit,n;          // VIT + n
bonus bInt,n;          // INT + n
bonus bDex,n;          // DEX + n
bonus bLuk,n;          // LUK + n
bonus bAllStats,n;     // All stats + n
bonus bAgiVit,n;       // AGI + n, VIT + n
bonus bAgiDexStr,n;    // STR + n, AGI + n, DEX + n
```

**Examples:**
```yaml
# +10 STR sword
Script: |
  bonus bStr,10;

# +5 all stats armor
Script: |
  bonus bAllStats,5;

# AGI/VIT shoes
Script: |
  bonus bAgiVit,3;
```

---

### Trait Stats (4th Job)

```c
bonus bPow,n;          // POW + n
bonus bSta,n;          // STA + n
bonus bWis,n;          // WIS + n
bonus bSpl,n;          // SPL + n
bonus bCon,n;          // CON + n
bonus bCrt,n;          // CRT + n
bonus bAllTraitStats,n; // All trait stats + n
```

---

## 3. HP/SP/AP

```c
bonus bMaxHP,n;        // MaxHP + n
bonus bMaxHPrate,n;    // MaxHP + n%
bonus bMaxSP,n;        // MaxSP + n
bonus bMaxSPrate,n;    // MaxSP + n%
bonus bMaxAP,n;        // MaxAP + n (4th job)
bonus bMaxAPrate,n;    // MaxAP + n%
```

**Examples:**
```yaml
# +500 HP armor
Script: |
  bonus bMaxHP,500;

# +10% HP/SP accessory
Script: |
  bonus bMaxHPrate,10;
  bonus bMaxSPrate,10;
```

---

## 4. ATTACK & DEFENSE

### Attack

```c
bonus bBaseAtk,n;          // Base ATK + n
bonus bAtk,n;              // ATK + n
bonus bAtk2,n;             // ATK2 + n
bonus bAtkRate,n;          // ATK + n%
bonus bWeaponAtkRate,n;    // Weapon ATK + n%
bonus bMatk,n;             // MATK + n
bonus bMatk2,n;            // MATK + n (hidden)
bonus bMatkRate,n;         // MATK + n%
bonus bWeaponMatkRate,n;   // Weapon MATK + n%
```

**Examples:**
```yaml
# High damage sword
Script: |
  bonus bAtk,100;
  bonus bAtkRate,15;

# Magic staff
Script: |
  bonus bMatk,150;
  bonus bMatkRate,10;
```

---

### Defense

```c
bonus bDef,n;              // Equipment DEF + n
bonus bDefRate,n;          // Equipment DEF + n%
bonus bDef2,n;             // VIT-based DEF + n
bonus bDef2Rate,n;         // VIT-based DEF + n%
bonus bMdef,n;             // Equipment MDEF + n
bonus bMdefRate,n;         // Equipment MDEF + n%
bonus bMdef2,n;            // INT-based MDEF + n
bonus bMdef2Rate,n;        // INT-based MDEF + n%
```

**Examples:**
```yaml
# Tank shield
Script: |
  bonus bDef,50;
  bonus bMdef,20;

# % defense boost
Script: |
  bonus bDefRate,15;
```

---

## 5. ACCURACY & EVASION

```c
bonus bHit,n;              // HIT + n
bonus bHitRate,n;          // HIT + n%
bonus bCritical,n;         // CRIT + n
bonus bCriticalRate,n;     // CRIT + n%
bonus bFlee,n;             // FLEE + n
bonus bFleeRate,n;         // FLEE + n%
bonus bFlee2,n;            // Perfect Dodge + n
bonus bFlee2Rate,n;        // Perfect Dodge + n%
bonus bPerfectHitRate,n;   // Perfect Hit + n%
bonus bPerfectHitAddRate,n; // Perfect Hit + n%
```

**Examples:**
```yaml
# Accuracy gloves
Script: |
  bonus bHit,20;

# Critical dagger
Script: |
  bonus bCritical,15;
  bonus bCriticalRate,10;

# Evasion boots
Script: |
  bonus bFlee,15;
  bonus bFlee2,5;
```

---

## 6. DAMAGE MODIFIERS

### Race Damage

```c
bonus2 bAddRace,r,n;           // +n% damage vs race
bonus2 bMagicAddRace,r,n;      // +n% magic damage vs race
bonus2 bSubRace,r,n;           // -n% damage from race
bonus2 bSubRace2,mr,n;         // -n% damage from monster race
```

**Examples:**
```yaml
# Anti-Demon sword
Script: |
  bonus2 bAddRace,RC_Demon,20;
  bonus2 bAddRace,RC_Undead,20;

# Anti-Boss armor
Script: |
  bonus2 bSubRace,RC_All,10;
  if (readparam(bBaseLevel) >= 99) {
    bonus2 bSubRace,Class_Boss,15;
  }
```

---

### Element Damage

```c
bonus2 bAddEle,e,n;            // +n% damage vs element
bonus2 bMagicAddEle,e,n;       // +n% magic damage vs element
bonus2 bSubEle,e,n;            // -n% damage from element
bonus3 bAddEle,e,n,bf;         // +n% damage vs element with flags
```

**Examples:**
```yaml
# Fire damage sword
Script: |
  bonus2 bAddEle,Ele_Fire,25;

# Water resistance armor
Script: |
  bonus2 bSubEle,Ele_Water,20;
```

---

### Size Damage

```c
bonus2 bAddSize,s,n;           // +n% damage vs size
bonus2 bMagicAddSize,s,n;      // +n% magic damage vs size
bonus2 bSubSize,s,n;           // -n% damage from size
bonus bNoSizeFix;              // Ignore size penalty
```

**Examples:**
```yaml
# Large monster hunter
Script: |
  bonus2 bAddSize,Size_Large,20;

# Pike (no size penalty)
Script: |
  bonus bNoSizeFix;
```

---

### Class Damage

```c
bonus2 bAddClass,c,n;          // +n% damage vs class
bonus2 bMagicAddClass,c,n;     // +n% magic damage vs class
bonus2 bSubClass,c,n;          // -n% damage from class
```

**Examples:**
```yaml
# MVP killer weapon
Script: |
  bonus2 bAddClass,Class_Boss,30;
  bonus2 bAddClass,Class_Guardian,30;
```

---

## 7. RESISTANCE & REDUCTION

### Physical Reduction

```c
bonus bNearAtkDef,n;           // -n% damage from melee
bonus bLongAtkDef,n;           // -n% damage from ranged
bonus bWeaponAtkRate,n;        // +n% weapon attack
bonus bCritAtkRate,n;          // +n% critical damage
bonus bCriticalDef,n;          // -n critical rate from enemy
```

---

### Magic Reduction

```c
bonus bMagicDamageReturn,n;    // n% magic damage reflected
bonus bMagicAtkEle,e;          // Change magic element
```

---

### Status Resistance

```c
bonus2 bResEff,eff,n;          // +n% resistance to status
bonus2 bAddEffWhenHit,eff,n;   // n% chance to inflict status when hit
bonus3 bAddEff,eff,n,atf;      // n% chance to inflict status
```

**Examples:**
```yaml
# Stun immunity helm
Script: |
  bonus2 bResEff,Eff_Stun,10000;

# Poison resistance armor
Script: |
  bonus2 bResEff,Eff_Poison,5000;
  bonus2 bResEff,Eff_DPoison,5000;

# Curse on hit
Script: |
  bonus2 bAddEffWhenHit,Eff_Curse,1000;
```

---

## 8. AUTOSPELL

### Basic AutoSpell

```c
bonus4 bAutoSpell,sk,lv,rate,bf;  // Cast skill on attack
bonus4 bAutoSpellWhenHit,sk,lv,rate,bf;  // Cast skill when hit
bonus5 bAutoSpell,sk,lv,rate,bf,iid;  // With item cost
```

**Examples:**
```yaml
# Fire Bolt on attack (3% chance)
Script: |
  bonus4 bAutoSpell,MG_FIREBOLT,5,30,0;

# Heal when hit (5% chance)
Script: |
  bonus4 bAutoSpellWhenHit,AL_HEAL,10,50,0;

# Cold Bolt (long range only)
Script: |
  bonus4 bAutoSpell,MG_COLDBOLT,5,30,BF_LONG;
```

---

### Advanced AutoSpell

```c
bonus4 bAutoSpellWhenHit,sk,lv,rate,bf;
bonus5 bAutoSpellWhenHit,sk,lv,rate,bf,iid;
bonus5 bAutoSpell,sk,-lv,rate,bf,atf;  // Negative level = cast on self
```

**Examples:**
```yaml
# Blessing on self when hit
Script: |
  bonus5 bAutoSpellWhenHit,AL_BLESSING,-10,100,BF_WEAPON,ATF_SELF;

# Provoke on melee attack
Script: |
  bonus4 bAutoSpell,SM_PROVOKE,10,50,BF_SHORT;
```

---

## 9. SPECIAL EFFECTS

### HP/SP Drain

```c
bonus bHPDrainValue,n;         // Drain n HP per hit
bonus2 bHPDrainRate,n,m;       // Drain n% HP, max m per hit
bonus2 bSPDrainRate,n,m;       // Drain n% SP, max m per hit
bonus3 bHPDrainRate,n,m,r;     // Drain from specific race
```

**Examples:**
```yaml
# Vampire sword
Script: |
  bonus2 bHPDrainRate,5,100;  // 5% drain, max 100 HP

# SP drain accessory
Script: |
  bonus2 bSPDrainRate,2,50;   // 2% drain, max 50 SP
```

---

### SP Cost Reduction

```c
bonus bUseSPrate,n;            // SP cost +n% (use negative)
bonus2 bSkillUseSP,sk,n;       // Skill SP cost +n
bonus2 bSkillUseSPrate,sk,n;   // Skill SP cost +n%
```

**Examples:**
```yaml
# Reduce all SP costs by 20%
Script: |
  bonus bUseSPrate,-20;

# Reduce Heal cost by 50%
Script: |
  bonus2 bSkillUseSPrate,AL_HEAL,-50;
```

---

### Cast Time

```c
bonus bCastrate,n;             // Cast time +n% (use negative)
bonus2 bSkillCooldown,sk,n;    // Skill cooldown -n ms
bonus2 bSkillCast,sk,n;        // Skill cast time +n ms
bonus2 bVariableCastrate,sk,n; // Variable cast +n%
bonus2 bFixedCastrate,sk,n;    // Fixed cast +n%
```

**Examples:**
```yaml
# Instant cast accessory
Script: |
  bonus bCastrate,-100;

# Heal -1 second cooldown
Script: |
  bonus2 bSkillCooldown,AL_HEAL,-1000;
```

---

### ASPD & Movement

```c
bonus bAspd,n;                 // ASPD + n
bonus bAspdRate,n;             // ASPD + n%
bonus bSpeedRate,n;            // Movement speed +n%
bonus bSpeedAddRate,n;         // Movement speed +n%
```

**Examples:**
```yaml
# AGI boots
Script: |
  bonus bAspd,1;
  bonus bSpeedRate,25;
```

---

## 10. ADVANCED BONUSES

### Skill Damage

```c
bonus2 bSkillAtk,sk,n;         // Skill damage +n%
bonus2 bSkillHeal,sk,n;        // Skill heal +n%
bonus3 bAddEff,eff,n,atf;      // Add status effect chance
```

**Examples:**
```yaml
# Bash damage +50%
Script: |
  bonus2 bSkillAtk,SM_BASH,50;

# Heal effectiveness +30%
Script: |
  bonus2 bSkillHeal,AL_HEAL,30;
```

---

### Combo Bonuses

```c
bonus bComboAddBonus,iid;      // If equipped with item
```

**Example:**
```yaml
# Bonus when worn with Shield (2105)
Script: |
  bonus bStr,5;
  if (isequipped(2105)) {
    bonus bAtk,50;
    bonus bDef,20;
  }
```

---

### Conditional Bonuses

```c
if (condition) { bonus ...; }
```

**Examples:**
```yaml
# Level-based bonus
Script: |
  bonus bStr,5;
  if (readparam(bBaseLevel) >= 99) {
    bonus bStr,5;
    bonus bAtk,50;
  }

# Class-specific
Script: |
  bonus bAtk,50;
  if (Class == Job_Swordman) {
    bonus bAtk,30;
  }

# Time-based
Script: |
  bonus bAtk,50;
  if (gettime(DT_HOUR) >= 18 || gettime(DT_HOUR) < 6) {
    bonus bAtk,30;  // Night bonus
  }
```

---

## COMMON PATTERNS

### Tank Armor
```yaml
Script: |
  bonus bMaxHPrate,10;
  bonus bDef,30;
  bonus bMdef,20;
  bonus2 bSubRace,RC_All,5;
```

### DPS Weapon
```yaml
Script: |
  bonus bAtk,100;
  bonus bAtkRate,15;
  bonus bCritical,10;
  bonus bAspd,2;
```

### Magic Staff
```yaml
Script: |
  bonus bMatk,150;
  bonus bMatkRate,10;
  bonus bInt,5;
  bonus bCastrate,-10;
```

### MVP Killer
```yaml
Script: |
  bonus2 bAddClass,Class_Boss,30;
  bonus2 bAddClass,Class_Guardian,30;
  bonus2 bHPDrainRate,3,100;
```

### Support Accessory
```yaml
Script: |
  bonus bInt,5;
  bonus2 bSkillHeal,AL_HEAL,30;
  bonus2 bSkillUseSPrate,AL_HEAL,-25;
  bonus bUseSPrate,-10;
```

### PvP Armor
```yaml
Script: |
  bonus bMaxHPrate,15;
  bonus2 bSubRace,RC_Player_Human,10;
  bonus2 bSubRace,RC_Player_Doram,10;
  bonus2 bResEff,Eff_Stun,5000;
  bonus2 bResEff,Eff_Freeze,5000;
```

---

## BONUS COMMAND LEVELS

### bonus (1 parameter)
```c
bonus bStr,10;
```

### bonus2 (2 parameters)
```c
bonus2 bAddRace,RC_Demon,20;
```

### bonus3 (3 parameters)
```c
bonus3 bAddEff,Eff_Stun,500,ATF_SHORT;
```

### bonus4 (4 parameters)
```c
bonus4 bAutoSpell,MG_FIREBOLT,5,30,0;
```

### bonus5 (5 parameters)
```c
bonus5 bAutoSpell,MG_FIREBOLT,5,30,0,Red_Blood;
```

---

## DEBUGGING

### Test Equipment
```c
// Check if item bonuses apply
@item 1234  // Spawn item
// Equip and check stats with @stats

// Remove to verify bonus removal
@delitem 1234 1
```

### Display Bonus Values
```yaml
Script: |
  bonus bStr,10;
  dispbottom "STR +10 from equipment";
```

---

## TIPS & BEST PRACTICES

1. **Test thoroughly** - Bonuses stack in complex ways
2. **Balance carefully** - Too many bonuses = overpowered items
3. **Use constants** - RC_Demon instead of numbers
4. **Document bonuses** - Comment your script
5. **Consider combinations** - Multiple items with same bonus
6. **Check renewal mode** - Some bonuses work differently
7. **Validate IDs** - Skill IDs, item IDs must be correct
8. **Use conditionals** - Level/class-based bonuses for progression

---

## SEE ALSO

- **Full Reference:** `/doc/item_bonus.txt` (512 lines, 100+ bonus types)
- **KB_REF_005:** Script Commands Reference
- **KB_DB_001:** Item Database Structure
- **Item Database:** `/db/(pre-)re/item_db.yml`

---

*Last Updated: 2015-10-29*
*rAthena Documentation - Item Bonuses*


# ═══════════════════════════════════════════════════════════════
# PART 3: JOB SYSTEM (EAJ_* MASKS AND JOB TREES)
# ═══════════════════════════════════════════════════════════════
<!-- RAG_CHUNK: job_system_complete -->

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
# PART 4: MAPFLAGS (mf_* CONSTANTS)
# ═══════════════════════════════════════════════════════════════
<!-- RAG_CHUNK: mapflags_complete -->

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
