# rAthena Game Data Complete Reference v9.1

**Version:** 9.1 Final - 5-File Edition
**Content:** Status Effects + Item Bonuses + Game Mechanics + Database Schemas
**Lines:** ~20,500 | **RAG Chunks:** ~970
**Last Updated:** 2025-11-26

---

<!-- RAG_CHUNK: game_data_overview -->
## What's in This File

This file contains ALL game data constants and schemas:

| Part | Content | Lines |
|------|---------|-------|
| **Part 1** | Status Effects (ALL 1038 SC_*) | ~12,000 |
| **Part 2** | Item Bonuses (263 bonuses) | ~5,300 |
| **Part 3** | Game Mechanics (EAJ_*, mf_*, element, configs, 47 DB schemas) | ~3,300 |

---

# ═══════════════════════════════════════════════════════════════
# PART 1: STATUS EFFECTS (ALL 1038 SC_*)
# ═══════════════════════════════════════════════════════════════


**Version:** 5.0 Enhanced
**Generated:** 2025-11-26
**Source:** doc/status_change.txt, src/map/status.hpp
**Total Status Effects:** 670

---

## Quick Navigation

- [Common Ailments](#common-ailments) - Stone, Freeze, Stun, Sleep, Poison
- [Character Buffs](#character-buffs) - Blessing, AGI Up, Gloria, etc.
- [Combat Skills](#combat-skills) - Damage modifiers, attack effects
- [Support Skills](#support-skills) - Healing, protection, utility
- [Food & Consumables](#food--consumables) - Stat foods, potions
- [Equipment Effects](#equipment-effects) - Item-triggered statuses
- [Guild War Effects](#guild-war-effects) - GvG-specific statuses
- [Job-Specific Effects](#job-specific-effects) - Class skill effects

---

## Using Status Effects in Scripts

### Basic Commands
```c
// Apply status effect for duration (milliseconds)
sc_start SC_BLESSING, 240000, 10;  // Blessing Lv10 for 4 minutes

// Apply with multiple values
sc_start4 SC_POISON, 30000, 5, getcharid(3), 0, 0;  // Poison with attacker ID

// Check if player has status
if (sc_is(SC_BLESSING)) {
    mes "You are blessed!";
}

// Remove specific status
sc_end SC_BLESSING;

// Remove all negative statuses
sc_end SC_STONE;
sc_end SC_FREEZE;
sc_end SC_STUN;
```

### Flag Constants (for sc_start)
| Flag | Value | Description |
|------|-------|-------------|
| SCSTART_NOAVOID | 1 | Cannot be avoided/resisted |
| SCSTART_NOTICKDEF | 2 | Duration not affected by VIT |
| SCSTART_LOADED | 4 | Use val1-val4 directly |
| SCSTART_NORATEDEF | 8 | Success rate not reduced |

---

## Complete Status Effect Reference

### SC_STONE

<!-- RAG_CHUNK: SC_STONE -->

**Effect:** DEF -50%; if HP>25% lose 1% HP/5 sec; MDEF +25%; change element to Earth Lv 1; ignore Steal & Lex Aeterna; can't move/attack/pick item/use item/use skill/sit/logout

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | Caster's object ID |
| val3 | Incubation time |
| val4 | Remaining tick |

**Script Example:**
```c
sc_start SC_STONE, 60000, 1;
```

---

### SC_FREEZE

<!-- RAG_CHUNK: SC_FREEZE -->

**Effect:** DEF -50%; FLEE = 0; MDEF +25%; ignore Steal, Lex Aeterna, Storm Gust, Falling Ice Pillar; change element to Water Lv 1; can't move/attack/pick item/use item/sit/logout

**Script Example:**
```c
sc_start SC_FREEZE, 60000, 1;
```

---

### SC_STUN

<!-- RAG_CHUNK: SC_STUN -->

**Effect:** FLEE = 0; can't move/attack/pick item/use item/use skill/sit/logout

**Script Example:**
```c
sc_start SC_STUN, 60000, 1;
```

---

### SC_SLEEP

<!-- RAG_CHUNK: SC_SLEEP -->

**Effect:** FLEE = 0; enemy CRIT x2; can't move/attack/pick item/use item/use skill/sit/logout

**Script Example:**
```c
sc_start SC_SLEEP, 60000, 1;
```

---

### SC_POISON

<!-- RAG_CHUNK: SC_POISON -->

**Effect:** DEF -25%; if HP>25% lose 1.5% + 2 HP/sec; SP Regeneration is disabled

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Level |
| val2 | Caster's object ID |
| val4 | Remaining tick |

**Script Example:**
```c
sc_start SC_POISON, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CURSE

<!-- RAG_CHUNK: SC_CURSE -->

**Effect:** ATK-25%; LUK = 0; Movement speed -300

**Script Example:**
```c
sc_start SC_CURSE, 60000, 1;
```

---

### SC_SILENCE

<!-- RAG_CHUNK: SC_SILENCE -->

**Effect:** Can't use active skills

**Script Example:**
```c
sc_start SC_SILENCE, 60000, 1;
```

---

### SC_CONFUSION

<!-- RAG_CHUNK: SC_CONFUSION -->

**Effect:** Move randomly; Set DEF to (STR+(INT*50))

**Script Example:**
```c
sc_start SC_CONFUSION, 60000, 1;
```

---

### SC_BLIND

<!-- RAG_CHUNK: SC_BLIND -->

**Effect:** HIT -25%; FLEE -25%; Black out the outter part of the screen

**Script Example:**
```c
sc_start SC_BLIND, 60000, 1;
```

---

### SC_BLEEDING

<!-- RAG_CHUNK: SC_BLEEDING -->

**Icon (EFST):** `EFST_BLOODING`

**Effect:** HP Regeneration is disabled; SP Regeneration is disabled; Lose HP overtime

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Level |
| val2 | Caster's object ID (for mob_log_damage) |
| val4 | Remaining tick |

**Script Example:**
```c
sc_start SC_BLEEDING, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_DPOISON

<!-- RAG_CHUNK: SC_DPOISON -->

**Effect:** DEF -25%; if HP>25% lose 10/15% HP/sec

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Level |
| val2 | Caster's object ID (for mob_log_damage) |
| val4 | Remaining tick |

**Script Example:**
```c
sc_start SC_DPOISON, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PROVOKE

<!-- RAG_CHUNK: SC_PROVOKE -->

**Icon (EFST):** `EFST_PROVOKE`

**Effect:** Decrease DEF by (5+(5*Skill Lv))%; Increase ATK by (2+(3*Skill lv))%

**Script Example:**
```c
sc_start SC_PROVOKE, 60000, 1;
```

---

### SC_ENDURE

<!-- RAG_CHUNK: SC_ENDURE -->

**Icon (EFST):** `EFST_ENDURE`

**Effect:** Increase MDEF by (Skill Lv); Doesn't get flinched when attacked

**Script Example:**
```c
sc_start SC_ENDURE, 60000, 1;
```

---

### SC_TWOHANDQUICKEN

<!-- RAG_CHUNK: SC_TWOHANDQUICKEN -->

**Icon (EFST):** `EFST_TWOHANDQUICKEN`

**Effect:** ASPD +30%

**Script Example:**
```c
sc_start SC_TWOHANDQUICKEN, 60000, 1;
```

---

### SC_CONCENTRATE

<!-- RAG_CHUNK: SC_CONCENTRATE -->

**Icon (EFST):** `EFST_CONCENTRATION`

**Effect:** Increase AGI by (2+Skill Lv)%; Increase DEX by (2+Skill Lv)%; Reveal hidden enemies in 3x3 area around caster

**Script Example:**
```c
sc_start SC_CONCENTRATE, 60000, 1;
```

---

### SC_HIDING

<!-- RAG_CHUNK: SC_HIDING -->

**Icon (EFST):** `EFST_HIDING`

**Effect:** Set OPTION_HIDE

**Script Example:**
```c
sc_start SC_HIDING, 60000, 1;
```

---

### SC_CLOAKING

<!-- RAG_CHUNK: SC_CLOAKING -->

**Icon (EFST):** `EFST_CLOAKING`

**Effect:** Set OPTION_CLOAK

**Script Example:**
```c
sc_start SC_CLOAKING, 60000, 1;
```

---

### SC_ENCPOISON

<!-- RAG_CHUNK: SC_ENCPOISON -->

**Icon (EFST):** `EFST_ENCHANTPOISON`

**Effect:** Change weapon element to ELE_POISON; Poisoning chance is (2.5+0.5%)

**Script Example:**
```c
sc_start SC_ENCPOISON, 60000, 1;
```

---

### SC_POISONREACT

<!-- RAG_CHUNK: SC_POISONREACT -->

**Icon (EFST):** `EFST_POISONREACT`

**Effect:** Blocks poison attacks; Increases damage by (30*Skill Lv)% after block; Counters non-poison attacks with Envenom 5 autocast

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill level |
| val2 | Number of Envenom autocasts |
| val3 | Chance to autocast Envenom on hit / Poison chance after block |
| val4 | 0=Poison Block Mode; 1=Damage Boost Mode |

**Script Example:**
```c
sc_start SC_POISONREACT, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_QUAGMIRE

<!-- RAG_CHUNK: SC_QUAGMIRE -->

**Icon (EFST):** `EFST_QUAGMIRE`

**Effect:** Removes Increase AGI, Twhohand Quicken, Wind Walk, Adrenaline Rush, Attention Concentrate, Cart Boost, True Sight, Magnetic Field & Onehand Quicken skill effect; Movement Speed -50; Decrease AGI & DEX by (10*Skill Lv) but can't below 75% for players and 50% for mobs

**Script Example:**
```c
sc_start SC_QUAGMIRE, 60000, 1;
```

---

### SC_ANGELUS

<!-- RAG_CHUNK: SC_ANGELUS -->

**Icon (EFST):** `EFST_ANGELUS`

**Effect:** Increase DEF by (5*Skill Lv)%

**Script Example:**
```c
sc_start SC_ANGELUS, 60000, 1;
```

---

### SC_BLESSING

<!-- RAG_CHUNK: SC_BLESSING -->

**Icon (EFST):** `EFST_BLESSING`

**Effect:** Increase STR, DEX & INT by (Skill Lv); Removes Stone and Curse status. If used on mobs will reduce their DEX and INT by 50%

**Script Example:**
```c
sc_start SC_BLESSING, 60000, 1;
```

---

### SC_SIGNUMCRUCIS

<!-- RAG_CHUNK: SC_SIGNUMCRUCIS -->

**Icon (EFST):** `EFST_CRUCIS`

**Effect:** Decrease DEF of Undead and Demon mobs by (10+(4*Skill Lv))% on screen

**Script Example:**
```c
sc_start SC_SIGNUMCRUCIS, 60000, 1;
```

---

### SC_INCREASEAGI

<!-- RAG_CHUNK: SC_INCREASEAGI -->

**Icon (EFST):** `EFST_INC_AGI`

**Effect:** Increase AGI and walkspeed, AL_INCAGI effect

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | (hardcoded) |

**Script Example:**
```c
sc_start SC_INCREASEAGI, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_DECREASEAGI

<!-- RAG_CHUNK: SC_DECREASEAGI -->

**Icon (EFST):** `EFST_DEC_AGI`

**Effect:** Decrease AGI and walkspeed, AL_DECAGI effect

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | (hardcoded) |

**Script Example:**
```c
sc_start SC_DECREASEAGI, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SLOWPOISON

<!-- RAG_CHUNK: SC_SLOWPOISON -->

**Icon (EFST):** `EFST_SLOWPOISON`

**Effect:** Stop the HP reduction of SC_POISON

**Script Example:**
```c
sc_start SC_SLOWPOISON, 60000, 1;
```

---

### SC_IMPOSITIO

<!-- RAG_CHUNK: SC_IMPOSITIO -->

**Icon (EFST):** `EFST_IMPOSITIO`

**Effect:** Increase ATK by (5*Skill Lv)

**Script Example:**
```c
sc_start SC_IMPOSITIO, 60000, 1;
```

---

### SC_SUFFRAGIUM

<!-- RAG_CHUNK: SC_SUFFRAGIUM -->

**Icon (EFST):** `EFST_SUFFRAGIUM`

**Effect:** Cast time decreased by (15*Skill Lv)%

**Script Example:**
```c
sc_start SC_SUFFRAGIUM, 60000, 1;
```

---

### SC_ASPERSIO

<!-- RAG_CHUNK: SC_ASPERSIO -->

**Icon (EFST):** `EFST_ASPERSIO`

**Effect:** Change weapon element to ELE_HOLY

**Script Example:**
```c
sc_start SC_ASPERSIO, 60000, 1;
```

---

### SC_BENEDICTIO

<!-- RAG_CHUNK: SC_BENEDICTIO -->

**Icon (EFST):** `EFST_BENEDICTIO`

**Effect:** Change armor element to ELE_HOLY

**Script Example:**
```c
sc_start SC_BENEDICTIO, 60000, 1;
```

---

### SC_KYRIE

<!-- RAG_CHUNK: SC_KYRIE -->

**Icon (EFST):** `EFST_KYRIE`

**Effect:** Remove SC_ASSUMPTIO skill effect; Block damage with a total of (MaxHP*(Skill Lv*2+10)/100) or ((Skill Lv/2)+5) times

**Script Example:**
```c
sc_start SC_KYRIE, 60000, 1;
```

---

### SC_MAGNIFICAT

<!-- RAG_CHUNK: SC_MAGNIFICAT -->

**Icon (EFST):** `EFST_MAGNIFICAT`

**Effect:** SP Regeneration speed x2

**Script Example:**
```c
sc_start SC_MAGNIFICAT, 60000, 1;
```

---

### SC_GLORIA

<!-- RAG_CHUNK: SC_GLORIA -->

**Icon (EFST):** `EFST_GLORIA`

**Effect:** LUK +30

**Script Example:**
```c
sc_start SC_GLORIA, 60000, 1;
```

---

### SC_AETERNA

<!-- RAG_CHUNK: SC_AETERNA -->

**Icon (EFST):** `EFST_LEXAETERNA`

**Effect:** Damaged received x2

**Script Example:**
```c
sc_start SC_AETERNA, 60000, 1;
```

---

### SC_ADRENALINE

<!-- RAG_CHUNK: SC_ADRENALINE -->

**Icon (EFST):** `EFST_ADRENALINE`

**Effect:** ASPD of Axe & Mace weapons x2

**Script Example:**
```c
sc_start SC_ADRENALINE, 60000, 1;
```

---

### SC_WEAPONPERFECTION

<!-- RAG_CHUNK: SC_WEAPONPERFECTION -->

**Icon (EFST):** `EFST_WEAPONPERFECT`

**Effect:** Ignore damage reduction to any monster size

**Script Example:**
```c
sc_start SC_WEAPONPERFECTION, 60000, 1;
```

---

### SC_OVERTHRUST

<!-- RAG_CHUNK: SC_OVERTHRUST -->

**Icon (EFST):** `EFST_OVERTHRUST`

**Effect:** Increase ATK by (5*Skill Lv)%; Add a 0.1% of breaking the equipped weapon [except Axes, Maces & Unbreakable weapons]

**Script Example:**
```c
sc_start SC_OVERTHRUST, 60000, 1;
```

---

### SC_MAXIMIZEPOWER

<!-- RAG_CHUNK: SC_MAXIMIZEPOWER -->

**Icon (EFST):** `EFST_MAXIMIZE`

**Effect:** SP Regeneration is disabled; Damage dealt is always the max damage

**Script Example:**
```c
sc_start SC_MAXIMIZEPOWER, 60000, 1;
```

---

### SC_TRICKDEAD

<!-- RAG_CHUNK: SC_TRICKDEAD -->

**Icon (EFST):** `EFST_TRICKDEAD`

**Effect:** HP & SP Regeneration is disabled; Remove SC_DANCING

**Script Example:**
```c
sc_start SC_TRICKDEAD, 60000, 1;
```

---

### SC_LOUD

<!-- RAG_CHUNK: SC_LOUD -->

**Icon (EFST):** `EFST_SHOUT`

**Effect:** STR +4

**Script Example:**
```c
sc_start SC_LOUD, 60000, 1;
```

---

### SC_ENERGYCOAT

<!-- RAG_CHUNK: SC_ENERGYCOAT -->

**Icon (EFST):** `EFST_ENERGYCOAT`

**Effect:** Reduce damage received according to current MaxSP %

**Script Example:**
```c
sc_start SC_ENERGYCOAT, 60000, 1;
```

---

### SC_BROKENARMOR

<!-- RAG_CHUNK: SC_BROKENARMOR -->

**Icon (EFST):** `EFST_BROKENARMOR`

**Effect:** Shows EFST_BROKENARMOR status icon if the armor is broken

**Script Example:**
```c
sc_start SC_BROKENARMOR, 60000, 1;
```

---

### SC_BROKENWEAPON

<!-- RAG_CHUNK: SC_BROKENWEAPON -->

**Icon (EFST):** `EFST_BROKENWEAPON`

**Effect:** Shows EFST_BROKENWEAPON status icon if the armor is broken

**Script Example:**
```c
sc_start SC_BROKENWEAPON, 60000, 1;
```

---

### SC_HALLUCINATION

<!-- RAG_CHUNK: SC_HALLUCINATION -->

**Icon (EFST):** `EFST_ILLUSION`

**Effect:** The screen goes wavy and you see crazy numbers for all damage that is processed around you, but they are all fake. Even other players see those numbers at you.

**Script Example:**
```c
sc_start SC_HALLUCINATION, 60000, 1;
```

---

### SC_WEIGHT50

<!-- RAG_CHUNK: SC_WEIGHT50 -->

**Icon (EFST):** `EFST_WEIGHTOVER50`

**Effect:** Shows EFST_WEIGHTOVER50 status icon if Weight >= 50%

**Script Example:**
```c
sc_start SC_WEIGHT50, 60000, 1;
```

---

### SC_WEIGHT90

<!-- RAG_CHUNK: SC_WEIGHT90 -->

**Icon (EFST):** `EFST_WEIGHTOVER90`

**Effect:** Shows EFST_WEIGHTOVER90 status icon if Weight >= 90%

**Script Example:**
```c
sc_start SC_WEIGHT90, 60000, 1;
```

---

### SC_ASPDPOTION0

<!-- RAG_CHUNK: SC_ASPDPOTION0 -->

**Icon (EFST):** `EFST_ATTHASTE_POTION1`

**Effect:** Increase ASPD, won't be stacked with SC_ASPDPOTION1, SC_ASPDPOTION2, SC_ASPDPOTION3

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +ASPD (Renewal) |
| val2 | +% ASPD (Pre-Renewal) |

**Script Example:**
```c
sc_start SC_ASPDPOTION0, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_ASPDPOTION1

<!-- RAG_CHUNK: SC_ASPDPOTION1 -->

**Icon (EFST):** `EFST_ATTHASTE_POTION2`

**Effect:** Increase ASPD, won't be stacked with SC_ASPDPOTION0, SC_ASPDPOTION2, SC_ASPDPOTION3

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +ASPD (Renewal) |
| val2 | +% ASPD (Pre-Renewal) |

**Script Example:**
```c
sc_start SC_ASPDPOTION1, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_ASPDPOTION2

<!-- RAG_CHUNK: SC_ASPDPOTION2 -->

**Icon (EFST):** `EFST_ATTHASTE_POTION3`

**Effect:** Increase ASPD, won't be stacked with SC_ASPDPOTION0, SC_ASPDPOTION1, SC_ASPDPOTION3

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +ASPD (Renewal) |
| val2 | +% ASPD (Pre-Renewal) |

**Script Example:**
```c
sc_start SC_ASPDPOTION2, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_ASPDPOTION3

<!-- RAG_CHUNK: SC_ASPDPOTION3 -->

**Icon (EFST):** `EFST_ATTHASTE_INFINITY`

**Effect:** Increase ASPD, won't be stacked with SC_ASPDPOTION0, SC_ASPDPOTION1, SC_ASPDPOTION2

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + ASPD (Renewal) |
| val2 | +% ASPD (Pre-Renewal) |

**Script Example:**
```c
sc_start SC_ASPDPOTION3, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SPEEDUP0

<!-- RAG_CHUNK: SC_SPEEDUP0 -->

**Icon (EFST):** `EFST_MOVHASTE_HORSE`

**Effect:** Increase/change walkspeed rate. This effect won't be stacked with bonus bSpeedRate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Walkspeed |

**Script Example:**
```c
sc_start SC_SPEEDUP0, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SPEEDUP1

<!-- RAG_CHUNK: SC_SPEEDUP1 -->

**Icon (EFST):** `EFST_MOVHASTE_POTION`

**Effect:** Increase/change walkspeed rate. This effect won't be stacked with bonus bSpeedRate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Walkspeed |

**Script Example:**
```c
sc_start SC_SPEEDUP1, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_ATKPOTION

<!-- RAG_CHUNK: SC_ATKPOTION -->

**Icon (EFST):** `EFST_PLUSATTACKPOWER`

**Effect:** Increase Atk

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +Atk |

**Script Example:**
```c
sc_start SC_ATKPOTION, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MATKPOTION

<!-- RAG_CHUNK: SC_MATKPOTION -->

**Icon (EFST):** `EFST_PLUSMAGICPOWER`

**Effect:** Increase MAtk

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +MAtk |

**Script Example:**
```c
sc_start SC_MATKPOTION, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_WEDDING

<!-- RAG_CHUNK: SC_WEDDING -->

**Effect:** Set Movement Speed to 100; Call clif_changelook; Set OPTION_WEDDING

**Script Example:**
```c
sc_start SC_WEDDING, 60000, 1;
```

---

### SC_SLOWDOWN

<!-- RAG_CHUNK: SC_SLOWDOWN -->

**Effect:** Reduce walkspeed rate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | -% Walkspeed |

**Script Example:**
```c
sc_start SC_SLOWDOWN, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_ANKLE

<!-- RAG_CHUNK: SC_ANKLE -->

**Icon (EFST):** `EFST_ANKLESNARE`

**Effect:** Set DEF to (AGI*50); Can't move

**Script Example:**
```c
sc_start SC_ANKLE, 60000, 1;
```

---

### SC_KEEPING

<!-- RAG_CHUNK: SC_KEEPING -->

**Effect:** Set DEF to 90

**Script Example:**
```c
sc_start SC_KEEPING, 60000, 1;
```

---

### SC_BARRIER

<!-- RAG_CHUNK: SC_BARRIER -->

**Icon (EFST):** `EFST_BARRIER`

**Effect:** Set DEF to 100

**Script Example:**
```c
sc_start SC_BARRIER, 60000, 1;
```

---

### SC_STRIPWEAPON

<!-- RAG_CHUNK: SC_STRIPWEAPON -->

**Icon (EFST):** `EFST_NOEQUIPWEAPON`

**Effect:** Unequip weapon; On mob ATK -25%

**Script Example:**
```c
sc_start SC_STRIPWEAPON, 60000, 1;
```

---

### SC_STRIPSHIELD

<!-- RAG_CHUNK: SC_STRIPSHIELD -->

**Icon (EFST):** `EFST_NOEQUIPSHIELD`

**Effect:** Unequip shield; On mob DEF -15%

**Script Example:**
```c
sc_start SC_STRIPSHIELD, 60000, 1;
```

---

### SC_STRIPARMOR

<!-- RAG_CHUNK: SC_STRIPARMOR -->

**Icon (EFST):** `EFST_NOEQUIPARMOR`

**Effect:** Unequip armor; On mob VIT -40%

**Script Example:**
```c
sc_start SC_STRIPARMOR, 60000, 1;
```

---

### SC_STRIPHELM

<!-- RAG_CHUNK: SC_STRIPHELM -->

**Icon (EFST):** `EFST_NOEQUIPHELM`

**Effect:** Unequip helm; On mob INT -40%

**Script Example:**
```c
sc_start SC_STRIPHELM, 60000, 1;
```

---

### SC_CP_WEAPON

<!-- RAG_CHUNK: SC_CP_WEAPON -->

**Icon (EFST):** `EFST_PROTECTWEAPON`

**Effect:** Protects equipped weapon from damage and strip skill

**Script Example:**
```c
sc_start SC_CP_WEAPON, 60000, 1;
```

---

### SC_CP_SHIELD

<!-- RAG_CHUNK: SC_CP_SHIELD -->

**Icon (EFST):** `EFST_PROTECTSHIELD`

**Effect:** Protects equipped shield from damage and strip skill

**Script Example:**
```c
sc_start SC_CP_SHIELD, 60000, 1;
```

---

### SC_CP_ARMOR

<!-- RAG_CHUNK: SC_CP_ARMOR -->

**Icon (EFST):** `EFST_PROTECTARMOR`

**Effect:** Protects equipped armor from damage and strip skill

**Script Example:**
```c
sc_start SC_CP_ARMOR, 60000, 1;
```

---

### SC_CP_HELM

<!-- RAG_CHUNK: SC_CP_HELM -->

**Icon (EFST):** `EFST_PROTECTHELM`

**Effect:** Protects equipped helm from damage and strip skill

**Script Example:**
```c
sc_start SC_CP_HELM, 60000, 1;
```

---

### SC_AUTOGUARD

<!-- RAG_CHUNK: SC_AUTOGUARD -->

**Icon (EFST):** `EFST_AUTOGUARD`

**Effect:** Blocks short and long range physical attacks at a certain chance, and stops the caster for 0.3 seconds if it's activated

**Script Example:**
```c
sc_start SC_AUTOGUARD, 60000, 1;
```

---

### SC_REFLECTSHIELD

<!-- RAG_CHUNK: SC_REFLECTSHIELD -->

**Icon (EFST):** `EFST_REFLECTSHIELD`

**Effect:** Reflects (10+(3*Skill Lv))% of short ranged physical attack back to the attacker

**Script Example:**
```c
sc_start SC_REFLECTSHIELD, 60000, 1;
```

---

### SC_SPLASHER

<!-- RAG_CHUNK: SC_SPLASHER -->

**Icon (EFST):** `EFST_SPLASHER`

**Effect:** This skill will only work once the target's HP is 1/3 or less of its Max HP. When struck by this skill, the target will explode and damage other enemies in it's vicinity

**Script Example:**
```c
sc_start SC_SPLASHER, 60000, 1;
```

---

### SC_PROVIDENCE

<!-- RAG_CHUNK: SC_PROVIDENCE -->

**Icon (EFST):** `EFST_PROVIDENCE`

**Effect:** Increase party members' resistance to RC_Demon and Ele_Holy monsters

**Script Example:**
```c
sc_start SC_PROVIDENCE, 60000, 1;
```

---

### SC_DEFENDER

<!-- RAG_CHUNK: SC_DEFENDER -->

**Icon (EFST):** `EFST_DEFENDER`

**Effect:** Decrease (5+(15*Skill Lv))% damage taken from long range attack; Decrease (25+(5*Skill Lv)) ASPD

**Script Example:**
```c
sc_start SC_DEFENDER, 60000, 1;
```

---

### SC_MAGICROD

<!-- RAG_CHUNK: SC_MAGICROD -->

**Icon (EFST):** `EFST_MAGICROD`

**Effect:** Gain (Skill Lv*20)% of SP consumed by the skill used from enemy; Damage received becomes 0; Drain 20% of enemy's Max SP

**Script Example:**
```c
sc_start SC_MAGICROD, 60000, 1;
```

---

### SC_SPELLBREAKER

<!-- RAG_CHUNK: SC_SPELLBREAKER -->

**Effect:** Gain SP used by enemy to cast the spell, and interrupt the magic cast. At lv 5, gain 1% from enemy max hp.

**Script Example:**
```c
sc_start SC_SPELLBREAKER, 60000, 1;
```

---

### SC_AUTOSPELL

<!-- RAG_CHUNK: SC_AUTOSPELL -->

**Icon (EFST):** `EFST_AUTOSPELL`

**Effect:** Auto cast several learned magic spells by using 2/3 of SP cost of the skill, but only when attacking with physical attacks.

**Script Example:**
```c
sc_start SC_AUTOSPELL, 60000, 1;
```

---

### SC_SIGHTTRASHER

<!-- RAG_CHUNK: SC_SIGHTTRASHER -->

**Effect:** (not exist)

**Script Example:**
```c
sc_start SC_SIGHTTRASHER, 60000, 1;
```

---

### SC_AUTOBERSERK

<!-- RAG_CHUNK: SC_AUTOBERSERK -->

**Icon (EFST):** `EFST_AUTOBERSERK`

**Effect:** If HP<25%, set SC_PROVOKE lv 10 on self

**Script Example:**
```c
sc_start SC_AUTOBERSERK, 60000, 1;
```

---

### SC_SPEARQUICKEN

<!-- RAG_CHUNK: SC_SPEARQUICKEN -->

**Icon (EFST):** `EFST_SPEARQUICKEN`

**Effect:** When using spear, +ASPD (20+(1*Skill Lv))%, +CRIT (3+(10*Skill Lv)), +FLEE (2*Skill Lv)

**Script Example:**
```c
sc_start SC_SPEARQUICKEN, 60000, 1;
```

---

### SC_AUTOCOUNTER

<!-- RAG_CHUNK: SC_AUTOCOUNTER -->

**Icon (EFST):** `EFST_AUTOCOUNTER`

**Effect:** Hitrate +20%; If attacked by close range, automatically retaliate with crit*2

**Script Example:**
```c
sc_start SC_AUTOCOUNTER, 60000, 1;
```

---

### SC_SIGHT

<!-- RAG_CHUNK: SC_SIGHT -->

**Effect:** Reveal hidden enemy on 3*3 range; Set OPTION_SIGHT

**Script Example:**
```c
sc_start SC_SIGHT, 60000, 1;
```

---

### SC_SAFETYWALL

<!-- RAG_CHUNK: SC_SAFETYWALL -->

**Effect:** Block short ranged attack; Set OPTION_RUWACH

**Script Example:**
```c
sc_start SC_SAFETYWALL, 60000, 1;
```

---

### SC_RUWACH

<!-- RAG_CHUNK: SC_RUWACH -->

**Effect:** Reveal hidden target and deal little damages if enemy is under SC_HIDING/SC_CLOAKING/SC_CAMOUFLAGE/SC_CLOAKINGEXCEED; Set OPTION_RUWACH

**Script Example:**
```c
sc_start SC_RUWACH, 60000, 1;
```

---

### SC_EXTREMITYFIST

<!-- RAG_CHUNK: SC_EXTREMITYFIST -->

**Icon (EFST):** `EFST_EXTREMITYFIST`

**Effect:** Stop SP Regeneration by setting RGN_SP

**Script Example:**
```c
sc_start SC_EXTREMITYFIST, 60000, 1;
```

---

### SC_EXPLOSIONSPIRITS

<!-- RAG_CHUNK: SC_EXPLOSIONSPIRITS -->

**Icon (EFST):** `EFST_EXPLOSIONSPIRITS`

**Effect:** Stop SP Regeneration by setting RGN_SP; +Crit

**Script Example:**
```c
sc_start SC_EXPLOSIONSPIRITS, 60000, 1;
```

---

### SC_COMBO

<!-- RAG_CHUNK: SC_COMBO -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_COMBO, 60000, 1;
```

---

### SC_BLADESTOP_WAIT

<!-- RAG_CHUNK: SC_BLADESTOP_WAIT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BLADESTOP_WAIT, 60000, 1;
```

---

### SC_BLADESTOP

<!-- RAG_CHUNK: SC_BLADESTOP -->

**Icon (EFST):** `EFST_BLADESTOP`

**Effect:** Stops player and target; Set OPT3_BLADESTOP

**Script Example:**
```c
sc_start SC_BLADESTOP, 60000, 1;
```

---

### SC_FIREWEAPON

<!-- RAG_CHUNK: SC_FIREWEAPON -->

**Icon (EFST):** `EFST_PROPERTYFIRE`

**Effect:** Change weapon element to Fire element

**Script Example:**
```c
sc_start SC_FIREWEAPON, 60000, 1;
```

---

### SC_WATERWEAPON

<!-- RAG_CHUNK: SC_WATERWEAPON -->

**Icon (EFST):** `EFST_PROPERTYWATER`

**Effect:** Change weapon element to Water element

**Script Example:**
```c
sc_start SC_WATERWEAPON, 60000, 1;
```

---

### SC_WINDWEAPON

<!-- RAG_CHUNK: SC_WINDWEAPON -->

**Icon (EFST):** `EFST_PROPERTYWIND`

**Effect:** Change weapon element to Wind element

**Script Example:**
```c
sc_start SC_WINDWEAPON, 60000, 1;
```

---

### SC_EARTHWEAPON

<!-- RAG_CHUNK: SC_EARTHWEAPON -->

**Icon (EFST):** `EFST_PROPERTYGROUND`

**Effect:** Change weapon element to Earth element

**Script Example:**
```c
sc_start SC_EARTHWEAPON, 60000, 1;
```

---

### SC_VOLCANO

<!-- RAG_CHUNK: SC_VOLCANO -->

**Icon (EFST):** `EFST_GROUNDMAGIC`

**Effect:** +watk of ELE_FIRE user

**Script Example:**
```c
sc_start SC_VOLCANO, 60000, 1;
```

---

### SC_DELUGE

<!-- RAG_CHUNK: SC_DELUGE -->

**Icon (EFST):** `EFST_GROUNDMAGIC`

**Effect:** +Max HP of ELE_WATER user

**Script Example:**
```c
sc_start SC_DELUGE, 60000, 1;
```

---

### SC_VIOLENTGALE

<!-- RAG_CHUNK: SC_VIOLENTGALE -->

**Icon (EFST):** `EFST_GROUNDMAGIC`

**Effect:** +FLEE of ELE_WIND user

**Script Example:**
```c
sc_start SC_VIOLENTGALE, 60000, 1;
```

---

### SC_WATK_ELEMENT

<!-- RAG_CHUNK: SC_WATK_ELEMENT -->

**Effect:** Adds a percent of damage as an element

**Script Example:**
```c
sc_start SC_WATK_ELEMENT, 60000, 1;
```

---

### SC_ARMOR

<!-- RAG_CHUNK: SC_ARMOR -->

**Effect:** Reduce damage received by 80 from long ranged weapon/misc attacks

**Script Example:**
```c
sc_start SC_ARMOR, 60000, 1;
```

---

### SC_ARMOR_ELEMENT

<!-- RAG_CHUNK: SC_ARMOR_ELEMENT -->

**Effect:** Adjust element resistance by percentage

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Water resistance |
| val2 | Earth resistance |
| val3 | Fire resistance |
| val4 | Wind resistance |

**Script Example:**
```c
sc_start SC_ARMOR_ELEMENT, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_NOCHAT

<!-- RAG_CHUNK: SC_NOCHAT -->

**Effect:** Can't chat, pick item, drop item

**Script Example:**
```c
sc_start SC_NOCHAT, 60000, 1;
```

---

### SC_BABY

<!-- RAG_CHUNK: SC_BABY -->

**Icon (EFST):** `EFST_PROTECTEXP`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BABY, 60000, 1;
```

---

### SC_AURABLADE

<!-- RAG_CHUNK: SC_AURABLADE -->

**Icon (EFST):** `EFST_AURABLADE`

**Effect:** Set OPT3_AURABLADE; Add damage by (20*Skill Lv) which ignore caster's accuracy rate/target's DEF

**Script Example:**
```c
sc_start SC_AURABLADE, 60000, 1;
```

---

### SC_PARRYING

<!-- RAG_CHUNK: SC_PARRYING -->

**Icon (EFST):** `EFST_PARRYING`

**Effect:** Block using a 2H-Sword with chance (20+(3*Skill Lv))%

**Script Example:**
```c
sc_start SC_PARRYING, 60000, 1;
```

---

### SC_CONCENTRATION

<!-- RAG_CHUNK: SC_CONCENTRATION -->

**Icon (EFST):** `EFST_LKCONCENTRATION`

**Effect:** Lv 1 Endurace effect; +WATK; +HIT; -DEF

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | 5*val1;		// Batk/Watk Increase |
| val3 | 10*val1;	// Hit Increase |
| val4 | 5*val1;		// Def reduction |

**Script Example:**
```c
sc_start SC_CONCENTRATION, 60000, 1;
```

---

### SC_TENSIONRELAX

<!-- RAG_CHUNK: SC_TENSIONRELAX -->

**Icon (EFST):** `EFST_TENSIONRELAX`

**Effect:** Increase HP regeneration rate while sitting

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | 12;		// SP cost |
| val3 | tick/val4; |
| val4 | 10000;	// Decrease at 10secs intervals. |

**Script Example:**
```c
sc_start SC_TENSIONRELAX, 60000, 1;
```

---

### SC_BERSERK

<!-- RAG_CHUNK: SC_BERSERK -->

**Icon (EFST):** `EFST_BERSERK`

**Effect:** Stop HP+SP Regen; Can't use skill; Can't chat; -FLEE; +Max HP; +Movement Speed; +ATK; Set OPT3_BERSERK; -5%HP per 10 second; Set DEF+MDEF to 0

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | HP Penalty (5% of Max HP) |
| val3 | Skill duration |
| val4 | Interval of HP Penalty |

**Script Example:**
```c
sc_start SC_BERSERK, 60000, 1;
```

---

### SC_FURY

<!-- RAG_CHUNK: SC_FURY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FURY, 60000, 1;
```

---

### SC_GOSPEL

<!-- RAG_CHUNK: SC_GOSPEL -->

**Icon (EFST):** `EFST_GOSPEL`

**Effect:** Can't move; Gives a random status to party member and also enemy.

**Script Example:**
```c
sc_start SC_GOSPEL, 60000, 1;
```

---

### SC_ASSUMPTIO

<!-- RAG_CHUNK: SC_ASSUMPTIO -->

**Icon (EFST):** `RE: EFST_ASSUMPTIO2. Pre-RE: EFST_ASSUMPTIO`

**Effect:** HP_ASSUMPTIO's effect

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Level // * 2 Bonus heal % (in RENEWAL) |

**Script Example:**
```c
sc_start SC_ASSUMPTIO, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_BASILICA

<!-- RAG_CHUNK: SC_BASILICA -->

**Effect:** Can't move; Can't use skill except the Basilica caster to cancel the basilica itself; Clear the skill area; Knockback enemy except Boss

**Script Example:**
```c
sc_start SC_BASILICA, 60000, 1;
```

---

### SC_GUILDAURA

<!-- RAG_CHUNK: SC_GUILDAURA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GUILDAURA, 60000, 1;
```

---

### SC_MAGICPOWER

<!-- RAG_CHUNK: SC_MAGICPOWER -->

**Icon (EFST):** `EFST_MAGICPOWER`

**Effect:** +MATK by (Skill Lv*5)% for the next magic skill that is cast

**Script Example:**
```c
sc_start SC_MAGICPOWER, 60000, 1;
```

---

### SC_EDP

<!-- RAG_CHUNK: SC_EDP -->

**Icon (EFST):** `EFST_EDP`

**Effect:** +WATK by (100+(Skill Lv*80))

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |
| val2 | Chance to Poison enemy (val1+2)% |
| val3 | Damage increased by (50*(val1+1)) |

**Script Example:**
```c
sc_start SC_EDP, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_TRUESIGHT

<!-- RAG_CHUNK: SC_TRUESIGHT -->

**Icon (EFST):** `EFST_TRUESIGHT`

**Effect:** All stat +5; Damage +(2*Skill Lv)%; Crit +(Skill Lv); Hit +(3*Skill Lv)%

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |
| val2 | Crit |
| val3 | Hit |

**Script Example:**
```c
sc_start SC_TRUESIGHT, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_WINDWALK

<!-- RAG_CHUNK: SC_WINDWALK -->

**Icon (EFST):** `EFST_WINDWALK`

**Effect:** +Flee; +Movement speed

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |
| val2 | Flee |

**Script Example:**
```c
sc_start SC_WINDWALK, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MELTDOWN

<!-- RAG_CHUNK: SC_MELTDOWN -->

**Icon (EFST):** `EFST_MELTDOWN`

**Effect:** Breaks target's weapon and armor at a certain chance

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |
| val2 | Chance to break weapon (100*Skill Lv) |
| val3 | Change to break armor (70*Skill Lv) |

**Script Example:**
```c
sc_start SC_MELTDOWN, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CARTBOOST

<!-- RAG_CHUNK: SC_CARTBOOST -->

**Icon (EFST):** `EFST_CARTBOOST`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CARTBOOST, 60000, 1;
```

---

### SC_CHASEWALK

<!-- RAG_CHUNK: SC_CHASEWALK -->

**Icon (EFST):** `EFST_CHASEWALK`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CHASEWALK, 60000, 1;
```

---

### SC_REJECTSWORD

<!-- RAG_CHUNK: SC_REJECTSWORD -->

**Icon (EFST):** `EFST_SWORDREJECT`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_REJECTSWORD, 60000, 1;
```

---

### SC_MARIONETTE

<!-- RAG_CHUNK: SC_MARIONETTE -->

**Icon (EFST):** `EFST_MARIONETTE_MASTER`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MARIONETTE, 60000, 1;
```

---

### SC_MARIONETTE2

<!-- RAG_CHUNK: SC_MARIONETTE2 -->

**Icon (EFST):** `EFST_MARIONETTE`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MARIONETTE2, 60000, 1;
```

---

### SC_CHANGEUNDEAD

<!-- RAG_CHUNK: SC_CHANGEUNDEAD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CHANGEUNDEAD, 60000, 1;
```

---

### SC_JOINTBEAT

<!-- RAG_CHUNK: SC_JOINTBEAT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_JOINTBEAT, 60000, 1;
```

---

### SC_MINDBREAKER

<!-- RAG_CHUNK: SC_MINDBREAKER -->

**Icon (EFST):** `EFST_MINDBREAKER`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MINDBREAKER, 60000, 1;
```

---

### SC_MEMORIZE

<!-- RAG_CHUNK: SC_MEMORIZE -->

**Icon (EFST):** `EFST_MEMORIZE`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MEMORIZE, 60000, 1;
```

---

### SC_FOGWALL

<!-- RAG_CHUNK: SC_FOGWALL -->

**Icon (EFST):** `EFST_FOGWALL`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FOGWALL, 60000, 1;
```

---

### SC_SPIDERWEB

<!-- RAG_CHUNK: SC_SPIDERWEB -->

**Icon (EFST):** `EFST_SPIDERWEB`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPIDERWEB, 60000, 1;
```

---

### SC_DEVOTION

<!-- RAG_CHUNK: SC_DEVOTION -->

**Icon (EFST):** `EFST_DEVOTION`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DEVOTION, 60000, 1;
```

---

### SC_SACRIFICE

<!-- RAG_CHUNK: SC_SACRIFICE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SACRIFICE, 60000, 1;
```

---

### SC_STEELBODY

<!-- RAG_CHUNK: SC_STEELBODY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STEELBODY, 60000, 1;
```

---

### SC_ORCISH

<!-- RAG_CHUNK: SC_ORCISH -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ORCISH, 60000, 1;
```

---

### SC_READYSTORM

<!-- RAG_CHUNK: SC_READYSTORM -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_READYSTORM, 60000, 1;
```

---

### SC_READYDOWN

<!-- RAG_CHUNK: SC_READYDOWN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_READYDOWN, 60000, 1;
```

---

### SC_READYTURN

<!-- RAG_CHUNK: SC_READYTURN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_READYTURN, 60000, 1;
```

---

### SC_READYCOUNTER

<!-- RAG_CHUNK: SC_READYCOUNTER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_READYCOUNTER, 60000, 1;
```

---

### SC_DODGE

<!-- RAG_CHUNK: SC_DODGE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DODGE, 60000, 1;
```

---

### SC_RUN

<!-- RAG_CHUNK: SC_RUN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_RUN, 60000, 1;
```

---

### SC_SHADOWWEAPON

<!-- RAG_CHUNK: SC_SHADOWWEAPON -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SHADOWWEAPON, 60000, 1;
```

---

### SC_ADRENALINE2

<!-- RAG_CHUNK: SC_ADRENALINE2 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ADRENALINE2, 60000, 1;
```

---

### SC_GHOSTWEAPON

<!-- RAG_CHUNK: SC_GHOSTWEAPON -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GHOSTWEAPON, 60000, 1;
```

---

### SC_KAIZEL

<!-- RAG_CHUNK: SC_KAIZEL -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KAIZEL, 60000, 1;
```

---

### SC_KAAHI

<!-- RAG_CHUNK: SC_KAAHI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KAAHI, 60000, 1;
```

---

### SC_KAUPE

<!-- RAG_CHUNK: SC_KAUPE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KAUPE, 60000, 1;
```

---

### SC_ONEHAND

<!-- RAG_CHUNK: SC_ONEHAND -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ONEHAND, 60000, 1;
```

---

### SC_PRESERVE

<!-- RAG_CHUNK: SC_PRESERVE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PRESERVE, 60000, 1;
```

---

### SC_BATTLEORDERS

<!-- RAG_CHUNK: SC_BATTLEORDERS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BATTLEORDERS, 60000, 1;
```

---

### SC_REGENERATION

<!-- RAG_CHUNK: SC_REGENERATION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_REGENERATION, 60000, 1;
```

---

### SC_DOUBLECAST

<!-- RAG_CHUNK: SC_DOUBLECAST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DOUBLECAST, 60000, 1;
```

---

### SC_GRAVITATION

<!-- RAG_CHUNK: SC_GRAVITATION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GRAVITATION, 60000, 1;
```

---

### SC_MAXOVERTHRUST

<!-- RAG_CHUNK: SC_MAXOVERTHRUST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MAXOVERTHRUST, 60000, 1;
```

---

### SC_LONGING

<!-- RAG_CHUNK: SC_LONGING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_LONGING, 60000, 1;
```

---

### SC_HERMODE

<!-- RAG_CHUNK: SC_HERMODE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HERMODE, 60000, 1;
```

---

### SC_SHRINK

<!-- RAG_CHUNK: SC_SHRINK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SHRINK, 60000, 1;
```

---

### SC_SIGHTBLASTER

<!-- RAG_CHUNK: SC_SIGHTBLASTER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SIGHTBLASTER, 60000, 1;
```

---

### SC_WINKCHARM

<!-- RAG_CHUNK: SC_WINKCHARM -->

**Icon (EFST):** `EFST_DC_WINKCHARM`

**Effect:** Can't cast spells. Can't attack the charmer. Only works on non-players.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill level |
| val2 | ID of the charmer |

**Script Example:**
```c
sc_start SC_WINKCHARM, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CLOSECONFINE

<!-- RAG_CHUNK: SC_CLOSECONFINE -->

**Icon (EFST):** `EFST_RG_CCONFINE_M`

**Effect:** Flee bonus and counter for confined enemies

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill level |
| val2 | Confined enemy count |
| val3 | +50 Flee |

**Script Example:**
```c
sc_start SC_CLOSECONFINE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CLOSECONFINE2

<!-- RAG_CHUNK: SC_CLOSECONFINE2 -->

**Icon (EFST):** `EFST_RG_CCONFINE_S`

**Effect:** Confines target in place

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill level |
| val2 | MapID of caster |

**Script Example:**
```c
sc_start SC_CLOSECONFINE2, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_DANCING

<!-- RAG_CHUNK: SC_DANCING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DANCING, 60000, 1;
```

---

### SC_ELEMENTALCHANGE

<!-- RAG_CHUNK: SC_ELEMENTALCHANGE -->

**Icon (EFST):** `EFST_ARMOR_PROPERTY`

**Effect:** Change armor element

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Element level |
| val2 | Element (see doc/item_bonus.txt) |

**Script Example:**
```c
sc_start SC_ELEMENTALCHANGE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_RICHMANKIM

<!-- RAG_CHUNK: SC_RICHMANKIM -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_RICHMANKIM, 60000, 1;
```

---

### SC_ETERNALCHAOS

<!-- RAG_CHUNK: SC_ETERNALCHAOS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ETERNALCHAOS, 60000, 1;
```

---

### SC_DRUMBATTLE

<!-- RAG_CHUNK: SC_DRUMBATTLE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DRUMBATTLE, 60000, 1;
```

---

### SC_NIBELUNGEN

<!-- RAG_CHUNK: SC_NIBELUNGEN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_NIBELUNGEN, 60000, 1;
```

---

### SC_ROKISWEIL

<!-- RAG_CHUNK: SC_ROKISWEIL -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ROKISWEIL, 60000, 1;
```

---

### SC_INTOABYSS

<!-- RAG_CHUNK: SC_INTOABYSS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INTOABYSS, 60000, 1;
```

---

### SC_SIEGFRIED

<!-- RAG_CHUNK: SC_SIEGFRIED -->

**Icon (EFST):** `EFST_SIEGFRIED`

**Effect:** Status change for BD_SIEGFRIED

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | BD_SIEGFRIED Skill level |
| val2 | Increase val2% damage reduction from non-Nuetral elemental attack |
| val3 | Increase status resistance value by val3% of player's current resistance. |

**Script Example:**
```c
sc_start SC_SIEGFRIED, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_WHISTLE

<!-- RAG_CHUNK: SC_WHISTLE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WHISTLE, 60000, 1;
```

---

### SC_ASSNCROS

<!-- RAG_CHUNK: SC_ASSNCROS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ASSNCROS, 60000, 1;
```

---

### SC_POEMBRAGI

<!-- RAG_CHUNK: SC_POEMBRAGI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_POEMBRAGI, 60000, 1;
```

---

### SC_APPLEIDUN

<!-- RAG_CHUNK: SC_APPLEIDUN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_APPLEIDUN, 60000, 1;
```

---

### SC_MODECHANGE

<!-- RAG_CHUNK: SC_MODECHANGE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MODECHANGE, 60000, 1;
```

---

### SC_HUMMING

<!-- RAG_CHUNK: SC_HUMMING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HUMMING, 60000, 1;
```

---

### SC_DONTFORGETME

<!-- RAG_CHUNK: SC_DONTFORGETME -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DONTFORGETME, 60000, 1;
```

---

### SC_FORTUNE

<!-- RAG_CHUNK: SC_FORTUNE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FORTUNE, 60000, 1;
```

---

### SC_SERVICE4U

<!-- RAG_CHUNK: SC_SERVICE4U -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SERVICE4U, 60000, 1;
```

---

### SC_STOP

<!-- RAG_CHUNK: SC_STOP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STOP, 60000, 1;
```

---

### SC_SPURT

<!-- RAG_CHUNK: SC_SPURT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPURT, 60000, 1;
```

---

### SC_SPIRIT

<!-- RAG_CHUNK: SC_SPIRIT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPIRIT, 60000, 1;
```

---

### SC_COMA

<!-- RAG_CHUNK: SC_COMA -->

**Effect:** Vanish HP to 1 and SP to 0

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Level |
| val2 | If 1 means do not remove SP |
| val3 | Caster's object ID (for mob_log_damage) |

**Script Example:**
```c
sc_start SC_COMA, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INTRAVISION

<!-- RAG_CHUNK: SC_INTRAVISION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INTRAVISION, 60000, 1;
```

---

### SC_INCALLSTATUS

<!-- RAG_CHUNK: SC_INCALLSTATUS -->

**Effect:** Increase all status

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +AllStats |

**Script Example:**
```c
sc_start SC_INCALLSTATUS, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCSTR

<!-- RAG_CHUNK: SC_INCSTR -->

**Effect:** Increase STR

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + STR |

**Script Example:**
```c
sc_start SC_INCSTR, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCAGI

<!-- RAG_CHUNK: SC_INCAGI -->

**Effect:** Increase AGI

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + AGI |

**Script Example:**
```c
sc_start SC_INCAGI, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCVIT

<!-- RAG_CHUNK: SC_INCVIT -->

**Effect:** Incrase VIT

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + VIT |

**Script Example:**
```c
sc_start SC_INCVIT, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCINT

<!-- RAG_CHUNK: SC_INCINT -->

**Effect:** Increase INT

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + INT |

**Script Example:**
```c
sc_start SC_INCINT, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCDEX

<!-- RAG_CHUNK: SC_INCDEX -->

**Effect:** Increase DEX

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + DEX |

**Script Example:**
```c
sc_start SC_INCDEX, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCLUK

<!-- RAG_CHUNK: SC_INCLUK -->

**Effect:** Increase LUK

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + Luk |

**Script Example:**
```c
sc_start SC_INCLUK, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCHIT

<!-- RAG_CHUNK: SC_INCHIT -->

**Effect:** Increase Hit

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + Hit |

**Script Example:**
```c
sc_start SC_INCHIT, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCHITRATE

<!-- RAG_CHUNK: SC_INCHITRATE -->

**Effect:** Incrase Hit

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Hit |

**Script Example:**
```c
sc_start SC_INCHITRATE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCFLEE

<!-- RAG_CHUNK: SC_INCFLEE -->

**Effect:** Increase Flee

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + Flee |

**Script Example:**
```c
sc_start SC_INCFLEE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCFLEERATE

<!-- RAG_CHUNK: SC_INCFLEERATE -->

**Effect:** Incrase Flee

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Flee |

**Script Example:**
```c
sc_start SC_INCFLEERATE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCMHPRATE

<!-- RAG_CHUNK: SC_INCMHPRATE -->

**Effect:** Increase MaxHP

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% MaxHP |

**Script Example:**
```c
sc_start SC_INCMHPRATE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCMSPRATE

<!-- RAG_CHUNK: SC_INCMSPRATE -->

**Effect:** Incrase Max SP

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% MaxSP |

**Script Example:**
```c
sc_start SC_INCMSPRATE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCATKRATE

<!-- RAG_CHUNK: SC_INCATKRATE -->

**Effect:** Increase Base Attack

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Atk |

**Script Example:**
```c
sc_start SC_INCATKRATE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCMATKRATE

<!-- RAG_CHUNK: SC_INCMATKRATE -->

**Effect:** Increase MATK

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Matk |

**Script Example:**
```c
sc_start SC_INCMATKRATE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCDEFRATE

<!-- RAG_CHUNK: SC_INCDEFRATE -->

**Effect:** Increase Defense

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Def |

**Script Example:**
```c
sc_start SC_INCDEFRATE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_STRFOOD

<!-- RAG_CHUNK: SC_STRFOOD -->

**Icon (EFST):** `EFST_FOOD_STR`

**Effect:** Increase STR (cannot be stacked with SC_FOOD_STR_CASH, ignored if value is lower)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +STR |

**Script Example:**
```c
sc_start SC_STRFOOD, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_AGIFOOD

<!-- RAG_CHUNK: SC_AGIFOOD -->

**Icon (EFST):** `EFST_FOOD_AGI`

**Effect:** Increase AGI (cannot be stacked with SC_FOOD_AGI_CASH, ignored if value is lower)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +AGI |

**Script Example:**
```c
sc_start SC_AGIFOOD, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_VITFOOD

<!-- RAG_CHUNK: SC_VITFOOD -->

**Icon (EFST):** `EFST_FOOD_VIT`

**Effect:** Increase VIT (cannot be stacked with SC_FOOD_VIT_CASH, ignored if value is lower)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +VIT |

**Script Example:**
```c
sc_start SC_VITFOOD, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INTFOOD

<!-- RAG_CHUNK: SC_INTFOOD -->

**Icon (EFST):** `EFST_FOOD_INT`

**Effect:** Increase INT (cannot be stacked with SC_FOOD_INT_CASH, ignored if value is lower)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +INT |

**Script Example:**
```c
sc_start SC_INTFOOD, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_DEXFOOD

<!-- RAG_CHUNK: SC_DEXFOOD -->

**Icon (EFST):** `EFST_FOOD_DEX`

**Effect:** Increase DEX (cannot be stacked with SC_FOOD_DEX_CASH, ignored if value is lower)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +DEX |

**Script Example:**
```c
sc_start SC_DEXFOOD, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_LUKFOOD

<!-- RAG_CHUNK: SC_LUKFOOD -->

**Icon (EFST):** `EFST_FOOD_LUK`

**Effect:** Increase LUK (cannot be stacked with SC_FOOD_LUK_CASH, ignored if value is lower)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +LUK |

**Script Example:**
```c
sc_start SC_LUKFOOD, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_HITFOOD

<!-- RAG_CHUNK: SC_HITFOOD -->

**Icon (EFST):** `EFST_FOOD_BASICHIT`

**Effect:** Increase HIT (food-type effect)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +Hit |

**Script Example:**
```c
sc_start SC_HITFOOD, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_FLEEFOOD

<!-- RAG_CHUNK: SC_FLEEFOOD -->

**Icon (EFST):** `EFST_FOOD_BASICAVOIDANCE`

**Effect:** Increase FLEE (food-type effect)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +Flee |

**Script Example:**
```c
sc_start SC_FLEEFOOD, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_BATKFOOD

<!-- RAG_CHUNK: SC_BATKFOOD -->

**Effect:** Increase Base Attack (food-type effect)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +BaseAttack |

**Script Example:**
```c
sc_start SC_BATKFOOD, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_WATKFOOD

<!-- RAG_CHUNK: SC_WATKFOOD -->

**Effect:** Increase Weapon Attack (food-type effect)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +WeaponAttack |

**Script Example:**
```c
sc_start SC_WATKFOOD, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MATKFOOD

<!-- RAG_CHUNK: SC_MATKFOOD -->

**Effect:** Increase Magic Attack (food-type effect)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +MagicAttack |

**Script Example:**
```c
sc_start SC_MATKFOOD, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SCRESIST

<!-- RAG_CHUNK: SC_SCRESIST -->

**Effect:** Status resistance from Gospel skill

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Increase status resistance value by n% of player's current resistance. |

**Script Example:**
```c
sc_start SC_SCRESIST, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_XMAS

<!-- RAG_CHUNK: SC_XMAS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_XMAS, 60000, 1;
```

---

### SC_WARM

<!-- RAG_CHUNK: SC_WARM -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WARM, 60000, 1;
```

---

### SC_SUN_COMFORT

<!-- RAG_CHUNK: SC_SUN_COMFORT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SUN_COMFORT, 60000, 1;
```

---

### SC_MOON_COMFORT

<!-- RAG_CHUNK: SC_MOON_COMFORT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MOON_COMFORT, 60000, 1;
```

---

### SC_STAR_COMFORT

<!-- RAG_CHUNK: SC_STAR_COMFORT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STAR_COMFORT, 60000, 1;
```

---

### SC_FUSION

<!-- RAG_CHUNK: SC_FUSION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FUSION, 60000, 1;
```

---

### SC_SKILLRATE_UP

<!-- RAG_CHUNK: SC_SKILLRATE_UP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SKILLRATE_UP, 60000, 1;
```

---

### SC_SKE

<!-- RAG_CHUNK: SC_SKE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SKE, 60000, 1;
```

---

### SC_KAITE

<!-- RAG_CHUNK: SC_KAITE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KAITE, 60000, 1;
```

---

### SC_SWOO

<!-- RAG_CHUNK: SC_SWOO -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SWOO, 60000, 1;
```

---

### SC_SKA

<!-- RAG_CHUNK: SC_SKA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SKA, 60000, 1;
```

---

### SC_EARTHSCROLL

<!-- RAG_CHUNK: SC_EARTHSCROLL -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_EARTHSCROLL, 60000, 1;
```

---

### SC_MIRACLE

<!-- RAG_CHUNK: SC_MIRACLE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MIRACLE, 60000, 1;
```

---

### SC_MADNESSCANCEL

<!-- RAG_CHUNK: SC_MADNESSCANCEL -->

**Icon (EFST):** `EFST_GS_MADNESSCANCEL`

**Effect:** Increases some statuses (Base ATK, ASPD)

**Script Example:**
```c
sc_start SC_MADNESSCANCEL, 60000, 1;
```

---

### SC_ADJUSTMENT

<!-- RAG_CHUNK: SC_ADJUSTMENT -->

**Icon (EFST):** `EFST_GS_ADJUSTMENT`

**Effect:** Increases some statuses (Hit, Flee)

**Script Example:**
```c
sc_start SC_ADJUSTMENT, 60000, 1;
```

---

### SC_INCREASING

<!-- RAG_CHUNK: SC_INCREASING -->

**Icon (EFST):** `EFST_GS_ACCURACY`

**Effect:** Increase some statuses (Hit, Dex, Agi), GS_INCREASING effect

**Script Example:**
```c
sc_start SC_INCREASING, 60000, 1;
```

---

### SC_MAGICALBULLET

<!-- RAG_CHUNK: SC_MAGICALBULLET -->

**Icon (EFST):** `EFST_GS_MAGICAL_BULLET`

**Effect:** Increases damage based on source's MATK and is reduced by target's MDEF

**Script Example:**
```c
sc_start SC_MAGICALBULLET, 60000, 1;
```

---

### SC_GATLINGFEVER

<!-- RAG_CHUNK: SC_GATLINGFEVER -->

**Icon (EFST):** `EFST_GS_GATLINGFEVER`

**Effect:** Increases some statuses (Base ATK, Flee, Movement Speed, ASPD)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | SkillLv |
| val2 | ASPD increase (20 * val1) |
| val3 | Base ATK (20 + 10 * val1) [pre-renewal] |
| val4 | Flee decrease (5 * val1) |

**Script Example:**
```c
sc_start SC_GATLINGFEVER, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_TATAMIGAESHI

<!-- RAG_CHUNK: SC_TATAMIGAESHI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_TATAMIGAESHI, 60000, 1;
```

---

### SC_UTSUSEMI

<!-- RAG_CHUNK: SC_UTSUSEMI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_UTSUSEMI, 60000, 1;
```

---

### SC_BUNSINJYUTSU

<!-- RAG_CHUNK: SC_BUNSINJYUTSU -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BUNSINJYUTSU, 60000, 1;
```

---

### SC_KAENSIN

<!-- RAG_CHUNK: SC_KAENSIN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KAENSIN, 60000, 1;
```

---

### SC_SUITON

<!-- RAG_CHUNK: SC_SUITON -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SUITON, 60000, 1;
```

---

### SC_NEN

<!-- RAG_CHUNK: SC_NEN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_NEN, 60000, 1;
```

---

### SC_KNOWLEDGE

<!-- RAG_CHUNK: SC_KNOWLEDGE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KNOWLEDGE, 60000, 1;
```

---

### SC_SMA

<!-- RAG_CHUNK: SC_SMA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SMA, 60000, 1;
```

---

### SC_FLING

<!-- RAG_CHUNK: SC_FLING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FLING, 60000, 1;
```

---

### SC_AVOID

<!-- RAG_CHUNK: SC_AVOID -->

**Icon (EFST):** `EFST_HLIF_AVOID`

**Effect:** Increase walkspeed for Players and Homunculus

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Level |
| val2 | Walkspeed increase (10 * val1 for Players, 40 * val1 for Homunculus) |

**Script Example:**
```c
sc_start SC_AVOID, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CHANGE

<!-- RAG_CHUNK: SC_CHANGE -->

**Icon (EFST):** `EFST_HLIF_CHANGE`

**Effect:** Increase some Homunculus' statuses (VIT, INT); Uses MATK for damage calculation; Sets Homunculus' HP and SP to 10 on expiration; On Pre-Renewal, sets Homunculus' HP and SP to 100% on cast

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Level |
| val2 | VIT increase (20 * val1) |
| val3 | INT increase (30 * val1) |

**Script Example:**
```c
sc_start SC_CHANGE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_BLOODLUST

<!-- RAG_CHUNK: SC_BLOODLUST -->

**Icon (EFST):** `EFST_HAMI_BLOODLUST`

**Effect:** Increase the homunculus ATK and has a chance to leech HP from the target

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Level |
| val2 | ATK increase (20 + (10 * val1)) |
| val3 | Chance to leech HP (9 * val1)% |
| val4 | Leeched HP percentage 20% |

**Script Example:**
```c
sc_start SC_BLOODLUST, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_FLEET

<!-- RAG_CHUNK: SC_FLEET -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FLEET, 60000, 1;
```

---

### SC_SPEED

<!-- RAG_CHUNK: SC_SPEED -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPEED, 60000, 1;
```

---

### SC_DEFENCE

<!-- RAG_CHUNK: SC_DEFENCE -->

**Icon (EFST):** `EFST_HAMI_DEFENCE`

**Effect:** Increase VIT and as result VIT-based DEF of the Player and plain VIT of the Homunculus

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Level |
| val2 | VIT increase for players, DEF increase for homunculus (5 + (5 * val1)) [Renewal], (2 * val1) [Pre-Renewal] |

**Script Example:**
```c
sc_start SC_DEFENCE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCASPDRATE

<!-- RAG_CHUNK: SC_INCASPDRATE -->

**Effect:** Increase ASPD

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% ASPD |

**Script Example:**
```c
sc_start SC_INCASPDRATE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCFLEE2

<!-- RAG_CHUNK: SC_INCFLEE2 -->

**Icon (EFST):** `EFST_PLUSAVOIDVALUE`

**Effect:** Increase perfect flee

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + Flee2 |

**Script Example:**
```c
sc_start SC_INCFLEE2, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_JAILED

<!-- RAG_CHUNK: SC_JAILED -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_JAILED, 60000, 1;
```

---

### SC_ENCHANTARMS

<!-- RAG_CHUNK: SC_ENCHANTARMS -->

**Icon (EFST):** `EFST_WEAPONPROPERTY`

**Effect:** Changes the element of a target's weapon.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Element value from skill_db |

**Script Example:**
```c
sc_start SC_ENCHANTARMS, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MAGICALATTACK

<!-- RAG_CHUNK: SC_MAGICALATTACK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MAGICALATTACK, 60000, 1;
```

---

### SC_ARMORCHANGE

<!-- RAG_CHUNK: SC_ARMORCHANGE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ARMORCHANGE, 60000, 1;
```

---

### SC_CRITICALWOUND

<!-- RAG_CHUNK: SC_CRITICALWOUND -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CRITICALWOUND, 60000, 1;
```

---

### SC_MAGICMIRROR

<!-- RAG_CHUNK: SC_MAGICMIRROR -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MAGICMIRROR, 60000, 1;
```

---

### SC_SLOWCAST

<!-- RAG_CHUNK: SC_SLOWCAST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SLOWCAST, 60000, 1;
```

---

### SC_SUMMER

<!-- RAG_CHUNK: SC_SUMMER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SUMMER, 60000, 1;
```

---

### SC_EXPBOOST

<!-- RAG_CHUNK: SC_EXPBOOST -->

**Icon (EFST):** `EFST_CASH_PLUSEXP`

**Effect:** Increase EXP rate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% EXP |

**Script Example:**
```c
sc_start SC_EXPBOOST, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_ITEMBOOST

<!-- RAG_CHUNK: SC_ITEMBOOST -->

**Icon (EFST):** `EFST_CASH_RECEIVEITEM`

**Effect:** Increase Drop rate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Drop |

**Script Example:**
```c
sc_start SC_ITEMBOOST, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_BOSSMAPINFO

<!-- RAG_CHUNK: SC_BOSSMAPINFO -->

**Icon (EFST):** `EFST_CASH_BOSS_ALARM`

**Effect:** Used to display Boss location on minimap

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Boss game ID |
| val2 | Used to keep timer message from spamming chat window |
| val4 | Remaining tick |

**Script Example:**
```c
sc_start SC_BOSSMAPINFO, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_LIFEINSURANCE

<!-- RAG_CHUNK: SC_LIFEINSURANCE -->

**Icon (EFST):** `EFST_CASH_DEATHPENALTY`

**Effect:** Remove death pleanlties

**Script Example:**
```c
sc_start SC_LIFEINSURANCE, 60000, 1;
```

---

### SC_INCCRI

<!-- RAG_CHUNK: SC_INCCRI -->

**Icon (EFST):** `EFST_FOOD_CRITICALSUCCESSVALUE`

**Effect:** Increase critical value

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + Critical (100% = 1000) |

**Script Example:**
```c
sc_start SC_INCCRI, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCDEF

<!-- RAG_CHUNK: SC_INCDEF -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INCDEF, 60000, 1;
```

---

### SC_INCBASEATK

<!-- RAG_CHUNK: SC_INCBASEATK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INCBASEATK, 60000, 1;
```

---

### SC_FASTCAST

<!-- RAG_CHUNK: SC_FASTCAST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FASTCAST, 60000, 1;
```

---

### SC_MDEF_RATE

<!-- RAG_CHUNK: SC_MDEF_RATE -->

**Icon (EFST):** `EFST_PROTECT_MDEF`

**Effect:** Increase MDef by %

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Mdef |

**Script Example:**
```c
sc_start SC_MDEF_RATE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_HPREGEN

<!-- RAG_CHUNK: SC_HPREGEN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HPREGEN, 60000, 1;
```

---

### SC_INCHEALRATE

<!-- RAG_CHUNK: SC_INCHEALRATE -->

**Icon (EFST):** `EFST_HEALPLUS`

**Effect:** Increase Heal power

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Heal |

**Script Example:**
```c
sc_start SC_INCHEALRATE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PNEUMA

<!-- RAG_CHUNK: SC_PNEUMA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PNEUMA, 60000, 1;
```

---

### SC_AUTOTRADE

<!-- RAG_CHUNK: SC_AUTOTRADE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_AUTOTRADE, 60000, 1;
```

---

### SC_KSPROTECTED

<!-- RAG_CHUNK: SC_KSPROTECTED -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KSPROTECTED, 60000, 1;
```

---

### SC_ARMOR_RESIST

<!-- RAG_CHUNK: SC_ARMOR_RESIST -->

**Effect:** Adjust element resistance by percentage

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Water resistance |
| val2 | Earth resistance |
| val3 | Fire resistance |
| val4 | Wind resistance |

**Script Example:**
```c
sc_start SC_ARMOR_RESIST, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SPCOST_RATE

<!-- RAG_CHUNK: SC_SPCOST_RATE -->

**Icon (EFST):** `EFST_ATKER_BLOOD`

**Effect:** Reduce SP cost

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Rate |

**Script Example:**
```c
sc_start SC_SPCOST_RATE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_COMMONSC_RESIST

<!-- RAG_CHUNK: SC_COMMONSC_RESIST -->

**Icon (EFST):** `EFST_TARGET_BLOOD`

**Effect:** Increase resistance of status changes, only againts SC_STONE, SC_FREEZE, SC_STUN, SC_SLEEP, SC_POISON, SC_CURSE, SC_SILENCE, SC_CONFUSION, SC_BLIND, SC_BLEEDING, and SC_DPOISON

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Resistance |

**Script Example:**
```c
sc_start SC_COMMONSC_RESIST, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SEVENWIND

<!-- RAG_CHUNK: SC_SEVENWIND -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SEVENWIND, 60000, 1;
```

---

### SC_DEF_RATE

<!-- RAG_CHUNK: SC_DEF_RATE -->

**Icon (EFST):** `EFST_PROTECT_DEF`

**Effect:** Increase Def by %

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Def |

**Script Example:**
```c
sc_start SC_DEF_RATE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SPREGEN

<!-- RAG_CHUNK: SC_SPREGEN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPREGEN, 60000, 1;
```

---

### SC_WALKSPEED

<!-- RAG_CHUNK: SC_WALKSPEED -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WALKSPEED, 60000, 1;
```

---

### SC_MERC_FLEEUP

<!-- RAG_CHUNK: SC_MERC_FLEEUP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MERC_FLEEUP, 60000, 1;
```

---

### SC_MERC_ATKUP

<!-- RAG_CHUNK: SC_MERC_ATKUP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MERC_ATKUP, 60000, 1;
```

---

### SC_MERC_HPUP

<!-- RAG_CHUNK: SC_MERC_HPUP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MERC_HPUP, 60000, 1;
```

---

### SC_MERC_SPUP

<!-- RAG_CHUNK: SC_MERC_SPUP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MERC_SPUP, 60000, 1;
```

---

### SC_MERC_HITUP

<!-- RAG_CHUNK: SC_MERC_HITUP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MERC_HITUP, 60000, 1;
```

---

### SC_MERC_QUICKEN

<!-- RAG_CHUNK: SC_MERC_QUICKEN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MERC_QUICKEN, 60000, 1;
```

---

### SC_REBIRTH

<!-- RAG_CHUNK: SC_REBIRTH -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_REBIRTH, 60000, 1;
```

---

### SC_SKILLCASTRATE

<!-- RAG_CHUNK: SC_SKILLCASTRATE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SKILLCASTRATE, 60000, 1;
```

---

### SC_DEFRATIOATK

<!-- RAG_CHUNK: SC_DEFRATIOATK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DEFRATIOATK, 60000, 1;
```

---

### SC_HPDRAIN

<!-- RAG_CHUNK: SC_HPDRAIN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HPDRAIN, 60000, 1;
```

---

### SC_SKILLATKBONUS

<!-- RAG_CHUNK: SC_SKILLATKBONUS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SKILLATKBONUS, 60000, 1;
```

---

### SC_ITEMSCRIPT

<!-- RAG_CHUNK: SC_ITEMSCRIPT -->

**Effect:** Timer script from other item script

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Item ID |
| val2 | Status Icon |

**Script Example:**
```c
sc_start SC_ITEMSCRIPT, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_S_LIFEPOTION

<!-- RAG_CHUNK: SC_S_LIFEPOTION -->

**Icon (EFST):** `EFST_S_LIFEPOTION`

**Effect:** Increase HP each interval

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | if < 0 will be percentage. If > 0 is fixed HP heal value |
| val2 | Interval per seconds |

**Script Example:**
```c
sc_start SC_S_LIFEPOTION, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_L_LIFEPOTION

<!-- RAG_CHUNK: SC_L_LIFEPOTION -->

**Icon (EFST):** `EFST_L_LIFEPOTION`

**Effect:** Increase HP each interval

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | if < 0 will be percentage. If > 0 is fixed HP heal value |
| val2 | Interval per seconds |

**Script Example:**
```c
sc_start SC_L_LIFEPOTION, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_JEXPBOOST

<!-- RAG_CHUNK: SC_JEXPBOOST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_JEXPBOOST, 60000, 1;
```

---

### SC_IGNOREDEF

<!-- RAG_CHUNK: SC_IGNOREDEF -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_IGNOREDEF, 60000, 1;
```

---

### SC_HELLPOWER

<!-- RAG_CHUNK: SC_HELLPOWER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HELLPOWER, 60000, 1;
```

---

### SC_INVINCIBLE

<!-- RAG_CHUNK: SC_INVINCIBLE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INVINCIBLE, 60000, 1;
```

---

### SC_INVINCIBLEOFF

<!-- RAG_CHUNK: SC_INVINCIBLEOFF -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INVINCIBLEOFF, 60000, 1;
```

---

### SC_MANU_ATK

<!-- RAG_CHUNK: SC_MANU_ATK -->

**Icon (EFST):** `EFST_MANU_ATK`

**Effect:** Increase Weapon Damage rate to Manuk monsters

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Damage |
| val2 | (hardcoded to 1 mark as Manuk group bonus) |

**Script Example:**
```c
sc_start SC_MANU_ATK, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MANU_DEF

<!-- RAG_CHUNK: SC_MANU_DEF -->

**Icon (EFST):** `EFST_MANU_DEF`

**Effect:** Increase Defense rate against Manuk monsters

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Defense |
| val2 | (hardcoded to 1 mark as Manuk group bonus) |

**Script Example:**
```c
sc_start SC_MANU_DEF, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SPL_ATK

<!-- RAG_CHUNK: SC_SPL_ATK -->

**Icon (EFST):** `EFST_SPL_ATK`

**Effect:** Increase Weapon Damage rate to Splendide Monster

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Damage |
| val2 | (hardcoded to 1 mark as Splendide group bonus) |

**Script Example:**
```c
sc_start SC_SPL_ATK, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SPL_DEF

<!-- RAG_CHUNK: SC_SPL_DEF -->

**Icon (EFST):** `EFST_SPL_DEF`

**Effect:** Increase Defense rate against Splendide Monster

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Defense |
| val2 | (hardcoded to 1 mark as Splendide group bonus) |

**Script Example:**
```c
sc_start SC_SPL_DEF, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MANU_MATK

<!-- RAG_CHUNK: SC_MANU_MATK -->

**Icon (EFST):** `EFST_MANU_MATK`

**Effect:** Increase Magic Damage rate to Manuk monsters

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Magic damage |
| val2 | (hardcoded to 1 mark as Manuk group bonus) |

**Script Example:**
```c
sc_start SC_MANU_MATK, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SPL_MATK

<!-- RAG_CHUNK: SC_SPL_MATK -->

**Icon (EFST):** `EFST_SPL_MATK`

**Effect:** Increase Magic Damage to Splendide Monster

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Damage |
| val2 | (hardcoded to 1 mark as Splendide group bonus) |

**Script Example:**
```c
sc_start SC_SPL_MATK, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_FOOD_STR_CASH

<!-- RAG_CHUNK: SC_FOOD_STR_CASH -->

**Icon (EFST):** `EFST_FOOD_STR_CASH`

**Effect:** Increase STR (cannot be stacked with SC_STRFOOD, ignored if value is lower)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +STR |

**Script Example:**
```c
sc_start SC_FOOD_STR_CASH, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_FOOD_AGI_CASH

<!-- RAG_CHUNK: SC_FOOD_AGI_CASH -->

**Icon (EFST):** `EFST_FOOD_AGI_CASH`

**Effect:** Increase AGI (cannot be stacked with SC_AGIFOOD, ignored if value is lower)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +AGI |

**Script Example:**
```c
sc_start SC_FOOD_AGI_CASH, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_FOOD_VIT_CASH

<!-- RAG_CHUNK: SC_FOOD_VIT_CASH -->

**Icon (EFST):** `EFST_FOOD_VIT_CASH`

**Effect:** Increase VIT (cannot be stacked with SC_VITFOOD, ignored if value is lower)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +VIT |

**Script Example:**
```c
sc_start SC_FOOD_VIT_CASH, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_FOOD_DEX_CASH

<!-- RAG_CHUNK: SC_FOOD_DEX_CASH -->

**Icon (EFST):** `EFST_FOOD_DEX_CASH`

**Effect:** Increase DEX (cannot be stacked with SC_DEXFOOD, ignored if value is lower)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +DEX |

**Script Example:**
```c
sc_start SC_FOOD_DEX_CASH, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_FOOD_INT_CASH

<!-- RAG_CHUNK: SC_FOOD_INT_CASH -->

**Icon (EFST):** `EFST_FOOD_INT_CASH`

**Effect:** Increase INT (cannot be stacked with SC_INTFOOD, ignored if value is lower)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +INT |

**Script Example:**
```c
sc_start SC_FOOD_INT_CASH, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_FOOD_LUK_CASH

<!-- RAG_CHUNK: SC_FOOD_LUK_CASH -->

**Icon (EFST):** `EFST_FOOD_LUK_CASH`

**Effect:** Increase LUK (cannot be stacked with SC_LUKFOOD, ignored if value is lower)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +LUK |

**Script Example:**
```c
sc_start SC_FOOD_LUK_CASH, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_FEAR

<!-- RAG_CHUNK: SC_FEAR -->

**Effect:** Cause SC_ANKLE for 2 seconds, Hit/Flee -20%, remove blind, immune to blind

**Script Example:**
```c
sc_start SC_FEAR, 60000, 1;
```

---

### SC_BURNING

<!-- RAG_CHUNK: SC_BURNING -->

**Icon (EFST):** `EFST_BURNT`

**Effect:** MDEF -25%; Deals fixed (1000 + 3%*MaxHP) damage every 3 seconds; Damage can not be reduced

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Level |
| val2 | 1000 |
| val3 | Caster's object ID (for mob_log_damage) |
| val4 | Remaining tick |

**Script Example:**
```c
sc_start SC_BURNING, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_FREEZING

<!-- RAG_CHUNK: SC_FREEZING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FREEZING, 60000, 1;
```

---

### SC_ENCHANTBLADE

<!-- RAG_CHUNK: SC_ENCHANTBLADE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ENCHANTBLADE, 60000, 1;
```

---

### SC_DEATHBOUND

<!-- RAG_CHUNK: SC_DEATHBOUND -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DEATHBOUND, 60000, 1;
```

---

### SC_MILLENNIUMSHIELD

<!-- RAG_CHUNK: SC_MILLENNIUMSHIELD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MILLENNIUMSHIELD, 60000, 1;
```

---

### SC_CRUSHSTRIKE

<!-- RAG_CHUNK: SC_CRUSHSTRIKE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CRUSHSTRIKE, 60000, 1;
```

---

### SC_REFRESH

<!-- RAG_CHUNK: SC_REFRESH -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_REFRESH, 60000, 1;
```

---

### SC_REUSE_REFRESH

<!-- RAG_CHUNK: SC_REUSE_REFRESH -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_REUSE_REFRESH, 60000, 1;
```

---

### SC_GIANTGROWTH

<!-- RAG_CHUNK: SC_GIANTGROWTH -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GIANTGROWTH, 60000, 1;
```

---

### SC_STONEHARDSKIN

<!-- RAG_CHUNK: SC_STONEHARDSKIN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STONEHARDSKIN, 60000, 1;
```

---

### SC_VITALITYACTIVATION

<!-- RAG_CHUNK: SC_VITALITYACTIVATION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_VITALITYACTIVATION, 60000, 1;
```

---

### SC_STORMBLAST

<!-- RAG_CHUNK: SC_STORMBLAST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STORMBLAST, 60000, 1;
```

---

### SC_FIGHTINGSPIRIT

<!-- RAG_CHUNK: SC_FIGHTINGSPIRIT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FIGHTINGSPIRIT, 60000, 1;
```

---

### SC_ABUNDANCE

<!-- RAG_CHUNK: SC_ABUNDANCE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ABUNDANCE, 60000, 1;
```

---

### SC_ADORAMUS

<!-- RAG_CHUNK: SC_ADORAMUS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ADORAMUS, 60000, 1;
```

---

### SC_EPICLESIS

<!-- RAG_CHUNK: SC_EPICLESIS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_EPICLESIS, 60000, 1;
```

---

### SC_ORATIO

<!-- RAG_CHUNK: SC_ORATIO -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ORATIO, 60000, 1;
```

---

### SC_LAUDAAGNUS

<!-- RAG_CHUNK: SC_LAUDAAGNUS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_LAUDAAGNUS, 60000, 1;
```

---

### SC_LAUDARAMUS

<!-- RAG_CHUNK: SC_LAUDARAMUS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_LAUDARAMUS, 60000, 1;
```

---

### SC_RENOVATIO

<!-- RAG_CHUNK: SC_RENOVATIO -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_RENOVATIO, 60000, 1;
```

---

### SC_EXPIATIO

<!-- RAG_CHUNK: SC_EXPIATIO -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_EXPIATIO, 60000, 1;
```

---

### SC_DUPLELIGHT

<!-- RAG_CHUNK: SC_DUPLELIGHT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DUPLELIGHT, 60000, 1;
```

---

### SC_SECRAMENT

<!-- RAG_CHUNK: SC_SECRAMENT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SECRAMENT, 60000, 1;
```

---

### SC_WHITEIMPRISON

<!-- RAG_CHUNK: SC_WHITEIMPRISON -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WHITEIMPRISON, 60000, 1;
```

---

### SC_MARSHOFABYSS

<!-- RAG_CHUNK: SC_MARSHOFABYSS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MARSHOFABYSS, 60000, 1;
```

---

### SC_RECOGNIZEDSPELL

<!-- RAG_CHUNK: SC_RECOGNIZEDSPELL -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_RECOGNIZEDSPELL, 60000, 1;
```

---

### SC_STASIS

<!-- RAG_CHUNK: SC_STASIS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STASIS, 60000, 1;
```

---

### SC_SPHERE_1

<!-- RAG_CHUNK: SC_SPHERE_1 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPHERE_1, 60000, 1;
```

---

### SC_SPHERE_2

<!-- RAG_CHUNK: SC_SPHERE_2 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPHERE_2, 60000, 1;
```

---

### SC_SPHERE_3

<!-- RAG_CHUNK: SC_SPHERE_3 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPHERE_3, 60000, 1;
```

---

### SC_SPHERE_4

<!-- RAG_CHUNK: SC_SPHERE_4 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPHERE_4, 60000, 1;
```

---

### SC_SPHERE_5

<!-- RAG_CHUNK: SC_SPHERE_5 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPHERE_5, 60000, 1;
```

---

### SC_READING_SB

<!-- RAG_CHUNK: SC_READING_SB -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_READING_SB, 60000, 1;
```

---

### SC_FREEZE_SP

<!-- RAG_CHUNK: SC_FREEZE_SP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FREEZE_SP, 60000, 1;
```

---

### SC_FEARBREEZE

<!-- RAG_CHUNK: SC_FEARBREEZE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FEARBREEZE, 60000, 1;
```

---

### SC_ELECTRICSHOCKER

<!-- RAG_CHUNK: SC_ELECTRICSHOCKER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ELECTRICSHOCKER, 60000, 1;
```

---

### SC_WUGDASH

<!-- RAG_CHUNK: SC_WUGDASH -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WUGDASH, 60000, 1;
```

---

### SC_BITE

<!-- RAG_CHUNK: SC_BITE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BITE, 60000, 1;
```

---

### SC_CAMOUFLAGE

<!-- RAG_CHUNK: SC_CAMOUFLAGE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CAMOUFLAGE, 60000, 1;
```

---

### SC_ACCELERATION

<!-- RAG_CHUNK: SC_ACCELERATION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ACCELERATION, 60000, 1;
```

---

### SC_HOVERING

<!-- RAG_CHUNK: SC_HOVERING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HOVERING, 60000, 1;
```

---

### SC_SHAPESHIFT

<!-- RAG_CHUNK: SC_SHAPESHIFT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SHAPESHIFT, 60000, 1;
```

---

### SC_INFRAREDSCAN

<!-- RAG_CHUNK: SC_INFRAREDSCAN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INFRAREDSCAN, 60000, 1;
```

---

### SC_ANALYZE

<!-- RAG_CHUNK: SC_ANALYZE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ANALYZE, 60000, 1;
```

---

### SC_MAGNETICFIELD

<!-- RAG_CHUNK: SC_MAGNETICFIELD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MAGNETICFIELD, 60000, 1;
```

---

### SC_NEUTRALBARRIER

<!-- RAG_CHUNK: SC_NEUTRALBARRIER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_NEUTRALBARRIER, 60000, 1;
```

---

### SC_NEUTRALBARRIER_MASTER

<!-- RAG_CHUNK: SC_NEUTRALBARRIER_MASTER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_NEUTRALBARRIER_MASTER, 60000, 1;
```

---

### SC_STEALTHFIELD

<!-- RAG_CHUNK: SC_STEALTHFIELD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STEALTHFIELD, 60000, 1;
```

---

### SC_STEALTHFIELD_MASTER

<!-- RAG_CHUNK: SC_STEALTHFIELD_MASTER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STEALTHFIELD_MASTER, 60000, 1;
```

---

### SC_OVERHEAT

<!-- RAG_CHUNK: SC_OVERHEAT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_OVERHEAT, 60000, 1;
```

---

### SC_OVERHEAT_LIMITPOINT

<!-- RAG_CHUNK: SC_OVERHEAT_LIMITPOINT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_OVERHEAT_LIMITPOINT, 60000, 1;
```

---

### SC_VENOMIMPRESS

<!-- RAG_CHUNK: SC_VENOMIMPRESS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_VENOMIMPRESS, 60000, 1;
```

---

### SC_POISONINGWEAPON

<!-- RAG_CHUNK: SC_POISONINGWEAPON -->

**Icon (EFST):** `EFST_POISONINGWEAPON`

**Effect:** Coat the user's equipped weapon with a new poison temporarily, which grants a chance of leaving the target infected with the current poison while physically attacking.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val2 | Poison Type |
| val3 | Success Rate |
| val4 | Caster's object ID (for mob_log_damage) |

**Script Example:**
```c
sc_start SC_POISONINGWEAPON, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_WEAPONBLOCKING

<!-- RAG_CHUNK: SC_WEAPONBLOCKING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WEAPONBLOCKING, 60000, 1;
```

---

### SC_CLOAKINGEXCEED

<!-- RAG_CHUNK: SC_CLOAKINGEXCEED -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CLOAKINGEXCEED, 60000, 1;
```

---

### SC_HALLUCINATIONWALK

<!-- RAG_CHUNK: SC_HALLUCINATIONWALK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HALLUCINATIONWALK, 60000, 1;
```

---

### SC_HALLUCINATIONWALK_POSTDELAY

<!-- RAG_CHUNK: SC_HALLUCINATIONWALK_POSTDELAY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HALLUCINATIONWALK_POSTDELAY, 60000, 1;
```

---

### SC_ROLLINGCUTTER

<!-- RAG_CHUNK: SC_ROLLINGCUTTER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ROLLINGCUTTER, 60000, 1;
```

---

### SC_TOXIN

<!-- RAG_CHUNK: SC_TOXIN -->

**Icon (EFST):** `EFST_TOXIN`

**Effect:** Inflict damage, which causes the affected entity to flinch every 10 seconds; This will interrupt the skill casting, even if protected against it

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val2 | Caster's object ID |
| val4 | Remaining tick |

**Script Example:**
```c
sc_start SC_TOXIN, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PARALYSE

<!-- RAG_CHUNK: SC_PARALYSE -->

**Icon (EFST):** `EFST_PARALYSE`

**Effect:** Decrease both ASPD and Flee Rate by 10% and halve Movement Speed, which does not stack with Decrease AGI, Quagmire, Marsh Of Abyss or Freezing status

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val4 | Tick |

**Script Example:**
```c
sc_start SC_PARALYSE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_VENOMBLEED

<!-- RAG_CHUNK: SC_VENOMBLEED -->

**Icon (EFST):** `EFST_VENOMBLEED`

**Effect:** Decrease Max HP by 15%

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val4 | Tick |

**Script Example:**
```c
sc_start SC_VENOMBLEED, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MAGICMUSHROOM

<!-- RAG_CHUNK: SC_MAGICMUSHROOM -->

**Icon (EFST):** `EFST_MAGICMUSHROOM`

**Effect:** Force the affected entity to use /heh emote, to randomly use skills and drain 3% of Max HP every 4 seconds

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val2 | Caster's object ID |
| val4 | Remaining tick |

**Script Example:**
```c
sc_start SC_MAGICMUSHROOM, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_DEATHHURT

<!-- RAG_CHUNK: SC_DEATHHURT -->

**Icon (EFST):** `EFST_DEATHHURT`

**Effect:** Drop the healing effectiveness by 20%; This effect stacks with Critical Wounds

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val4 | Tick |

**Script Example:**
```c
sc_start SC_DEATHHURT, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PYREXIA

<!-- RAG_CHUNK: SC_PYREXIA -->

**Icon (EFST):** `EFST_PYREXIA`

**Effect:** Cause Blind and Hallucination statuses; If the affected entity takes damage while under the effects of this poison, it will remain in flinching motion, which will interrupt the skill casting

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val4 | Remaining tick |

**Script Example:**
```c
sc_start SC_PYREXIA, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_OBLIVIONCURSE

<!-- RAG_CHUNK: SC_OBLIVIONCURSE -->

**Icon (EFST):** `EFST_OBLIVIONCURSE`

**Effect:** Force the affected entity to use /? emote, block SP Recovery and cause Oblivion status; There is a chance (100% - (Target INT * 0.8)%) of being inflicted, with a minimum of 5%

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val4 | Tick |

**Script Example:**
```c
sc_start SC_OBLIVIONCURSE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_LEECHESEND

<!-- RAG_CHUNK: SC_LEECHESEND -->

**Icon (EFST):** `EFST_LEECHESEND`

**Effect:** Drain (Target VIT * (SkillLv - 3)) + (Target HP / 100) HP each second

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val2 | Caster's object ID |
| val4 | Remaining tick |

**Script Example:**
```c
sc_start SC_LEECHESEND, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_REFLECTDAMAGE

<!-- RAG_CHUNK: SC_REFLECTDAMAGE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_REFLECTDAMAGE, 60000, 1;
```

---

### SC_FORCEOFVANGUARD

<!-- RAG_CHUNK: SC_FORCEOFVANGUARD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FORCEOFVANGUARD, 60000, 1;
```

---

### SC_SHIELDSPELL_DEF

<!-- RAG_CHUNK: SC_SHIELDSPELL_DEF -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SHIELDSPELL_DEF, 60000, 1;
```

---

### SC_SHIELDSPELL_MDEF

<!-- RAG_CHUNK: SC_SHIELDSPELL_MDEF -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SHIELDSPELL_MDEF, 60000, 1;
```

---

### SC_SHIELDSPELL_REF

<!-- RAG_CHUNK: SC_SHIELDSPELL_REF -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SHIELDSPELL_REF, 60000, 1;
```

---

### SC_EXEEDBREAK

<!-- RAG_CHUNK: SC_EXEEDBREAK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_EXEEDBREAK, 60000, 1;
```

---

### SC_PRESTIGE

<!-- RAG_CHUNK: SC_PRESTIGE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PRESTIGE, 60000, 1;
```

---

### SC_BANDING

<!-- RAG_CHUNK: SC_BANDING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BANDING, 60000, 1;
```

---

### SC_BANDING_DEFENCE

<!-- RAG_CHUNK: SC_BANDING_DEFENCE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BANDING_DEFENCE, 60000, 1;
```

---

### SC_EARTHDRIVE

<!-- RAG_CHUNK: SC_EARTHDRIVE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_EARTHDRIVE, 60000, 1;
```

---

### SC_INSPIRATION

<!-- RAG_CHUNK: SC_INSPIRATION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INSPIRATION, 60000, 1;
```

---

### SC_SPELLFIST

<!-- RAG_CHUNK: SC_SPELLFIST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPELLFIST, 60000, 1;
```

---

### SC_CRYSTALIZE

<!-- RAG_CHUNK: SC_CRYSTALIZE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CRYSTALIZE, 60000, 1;
```

---

### SC_STRIKING

<!-- RAG_CHUNK: SC_STRIKING -->

**Icon (EFST):** `EFST_STRIKING`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | SO_STRIKING Skill Level |
| val2 | Increased ATK |
| val3 | SP Drain / Sec |
| val4 | Tick Left (in sec) |

**Script Example:**
```c
sc_start SC_STRIKING, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_WARMER

<!-- RAG_CHUNK: SC_WARMER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WARMER, 60000, 1;
```

---

### SC_VACUUM_EXTREME

<!-- RAG_CHUNK: SC_VACUUM_EXTREME -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_VACUUM_EXTREME, 60000, 1;
```

---

### SC_PROPERTYWALK

<!-- RAG_CHUNK: SC_PROPERTYWALK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PROPERTYWALK, 60000, 1;
```

---

### SC_SWINGDANCE

<!-- RAG_CHUNK: SC_SWINGDANCE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SWINGDANCE, 60000, 1;
```

---

### SC_SYMPHONYOFLOVER

<!-- RAG_CHUNK: SC_SYMPHONYOFLOVER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SYMPHONYOFLOVER, 60000, 1;
```

---

### SC_MOONLITSERENADE

<!-- RAG_CHUNK: SC_MOONLITSERENADE -->

**Icon (EFST):** `EFST_MOONLIT_SERENADE`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | WA_MOONLIT_SERENADE Skill Level |
| val2 | WM_LESSON Level |
| val3 | Increased MATK |

**Script Example:**
```c
sc_start SC_MOONLITSERENADE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_RUSHWINDMILL

<!-- RAG_CHUNK: SC_RUSHWINDMILL -->

**Icon (EFST):** `EFST_RUSH_WINDMILL`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | MI_RUSH_WINDMILL Skill Level |
| val2 | WM_LESSON Level |
| val3 | Increased ATK |

**Script Example:**
```c
sc_start SC_RUSHWINDMILL, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_ECHOSONG

<!-- RAG_CHUNK: SC_ECHOSONG -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ECHOSONG, 60000, 1;
```

---

### SC_HARMONIZE

<!-- RAG_CHUNK: SC_HARMONIZE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HARMONIZE, 60000, 1;
```

---

### SC_VOICEOFSIREN

<!-- RAG_CHUNK: SC_VOICEOFSIREN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_VOICEOFSIREN, 60000, 1;
```

---

### SC_DEEPSLEEP

<!-- RAG_CHUNK: SC_DEEPSLEEP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DEEPSLEEP, 60000, 1;
```

---

### SC_SIRCLEOFNATURE

<!-- RAG_CHUNK: SC_SIRCLEOFNATURE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SIRCLEOFNATURE, 60000, 1;
```

---

### SC_GLOOMYDAY

<!-- RAG_CHUNK: SC_GLOOMYDAY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GLOOMYDAY, 60000, 1;
```

---

### SC_GLOOMYDAY_SK

<!-- RAG_CHUNK: SC_GLOOMYDAY_SK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GLOOMYDAY_SK, 60000, 1;
```

---

### SC_SONGOFMANA

<!-- RAG_CHUNK: SC_SONGOFMANA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SONGOFMANA, 60000, 1;
```

---

### SC_DANCEWITHWUG

<!-- RAG_CHUNK: SC_DANCEWITHWUG -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DANCEWITHWUG, 60000, 1;
```

---

### SC_SATURDAYNIGHTFEVER

<!-- RAG_CHUNK: SC_SATURDAYNIGHTFEVER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SATURDAYNIGHTFEVER, 60000, 1;
```

---

### SC_LERADSDEW

<!-- RAG_CHUNK: SC_LERADSDEW -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_LERADSDEW, 60000, 1;
```

---

### SC_MELODYOFSINK

<!-- RAG_CHUNK: SC_MELODYOFSINK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MELODYOFSINK, 60000, 1;
```

---

### SC_BEYONDOFWARCRY

<!-- RAG_CHUNK: SC_BEYONDOFWARCRY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BEYONDOFWARCRY, 60000, 1;
```

---

### SC_UNLIMITEDHUMMINGVOICE

<!-- RAG_CHUNK: SC_UNLIMITEDHUMMINGVOICE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_UNLIMITEDHUMMINGVOICE, 60000, 1;
```

---

### SC_SITDOWN_FORCE

<!-- RAG_CHUNK: SC_SITDOWN_FORCE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SITDOWN_FORCE, 60000, 1;
```

---

### SC_NETHERWORLD

<!-- RAG_CHUNK: SC_NETHERWORLD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_NETHERWORLD, 60000, 1;
```

---

### SC_CRESCENTELBOW

<!-- RAG_CHUNK: SC_CRESCENTELBOW -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CRESCENTELBOW, 60000, 1;
```

---

### SC_CURSEDCIRCLE_ATKER

<!-- RAG_CHUNK: SC_CURSEDCIRCLE_ATKER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CURSEDCIRCLE_ATKER, 60000, 1;
```

---

### SC_CURSEDCIRCLE_TARGET

<!-- RAG_CHUNK: SC_CURSEDCIRCLE_TARGET -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CURSEDCIRCLE_TARGET, 60000, 1;
```

---

### SC_LIGHTNINGWALK

<!-- RAG_CHUNK: SC_LIGHTNINGWALK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_LIGHTNINGWALK, 60000, 1;
```

---

### SC_RAISINGDRAGON

<!-- RAG_CHUNK: SC_RAISINGDRAGON -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_RAISINGDRAGON, 60000, 1;
```

---

### SC_GT_ENERGYGAIN

<!-- RAG_CHUNK: SC_GT_ENERGYGAIN -->

**Icon (EFST):** `EFST_GENTLETOUCH_ENERGYGAIN`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | SR_GENTLETOUCH_ENERGYGAIN Skill Level |
| val2 | Sphere Gain Chance |

**Script Example:**
```c
sc_start SC_GT_ENERGYGAIN, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_GT_CHANGE

<!-- RAG_CHUNK: SC_GT_CHANGE -->

**Icon (EFST):** `EFST_GENTLETOUCH_CHANGE`

**Effect:** ATK increase: ATK [{(Caster DEX / 4) + (Caster STR / 2)} x Skill Level / 5]; ASPD increase: [(Target AGI x Skill Level) / 60] %; MDEF decrease: MDEF [(200 / Caster INT) x Skill Level]; Max HP decrease: [Skill Level x 4] %

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | SR_GENTLETOUCH_CHANGE Skill Level |
| val2 | Increased ATK |
| val3 | Increased ASPD Rate |
| val4 | Decreased MDEF |

**Script Example:**
```c
sc_start SC_GT_CHANGE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_GT_REVITALIZE

<!-- RAG_CHUNK: SC_GT_REVITALIZE -->

**Icon (EFST):** `EFST_GENTLETOUCH_REVITALIZE`

**Effect:** MaxHP: [(Skill Level * 2)]%; Natural HP recovery increase: [(Skill Level x 30) + 50] %; STAT DEF increase: [(Caster VIT / 4) x Skill Level] (The stat def is not shown in the status window and it is processed differently)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | SR_GENTLETOUCH_REVITALIZE Skill Level |
| val2 | Max HP Rate bonus |
| val3 | HP Regen Rage Value |
| val4 | Increased DEF |

**Script Example:**
```c
sc_start SC_GT_REVITALIZE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_GN_CARTBOOST

<!-- RAG_CHUNK: SC_GN_CARTBOOST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GN_CARTBOOST, 60000, 1;
```

---

### SC_THORNSTRAP

<!-- RAG_CHUNK: SC_THORNSTRAP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_THORNSTRAP, 60000, 1;
```

---

### SC_BLOODSUCKER

<!-- RAG_CHUNK: SC_BLOODSUCKER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BLOODSUCKER, 60000, 1;
```

---

### SC_SMOKEPOWDER

<!-- RAG_CHUNK: SC_SMOKEPOWDER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SMOKEPOWDER, 60000, 1;
```

---

### SC_TEARGAS

<!-- RAG_CHUNK: SC_TEARGAS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_TEARGAS, 60000, 1;
```

---

### SC_MANDRAGORA

<!-- RAG_CHUNK: SC_MANDRAGORA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MANDRAGORA, 60000, 1;
```

---

### SC_STOMACHACHE

<!-- RAG_CHUNK: SC_STOMACHACHE -->

**Icon (EFST):** `EFST_STOMACHACHE`

**Effect:** Reduce all stats

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | -AllStats |

**Script Example:**
```c
sc_start SC_STOMACHACHE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MYSTERIOUS_POWDER

<!-- RAG_CHUNK: SC_MYSTERIOUS_POWDER -->

**Icon (EFST):** `EFST_MYSTERIOUS_POWDER`

**Effect:** Reduce Max HP rate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | ReduceValue (don't use - sign to reduce) |

**Script Example:**
```c
sc_start SC_MYSTERIOUS_POWDER, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MELON_BOMB

<!-- RAG_CHUNK: SC_MELON_BOMB -->

**Icon (EFST):** `EFST_MELON_BOMB`

**Effect:** Reduce ASPD and move speed

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | ReduceValue (don't use - sign to reduce) |

**Script Example:**
```c
sc_start SC_MELON_BOMB, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_BANANA_BOMB

<!-- RAG_CHUNK: SC_BANANA_BOMB -->

**Icon (EFST):** `EFST_BANANA_BOMB`

**Effect:** Reduce LUK rate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | ReduceValue (don't use - sign to reduce) |

**Script Example:**
```c
sc_start SC_BANANA_BOMB, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_BANANA_BOMB_SITDOWN

<!-- RAG_CHUNK: SC_BANANA_BOMB_SITDOWN -->

**Icon (EFST):** `EFST_BANANA_BOMB_SITDOWN_POSTDELAY`

**Effect:** Force player to sit

**Script Example:**
```c
sc_start SC_BANANA_BOMB_SITDOWN, 60000, 1;
```

---

### SC_SAVAGE_STEAK

<!-- RAG_CHUNK: SC_SAVAGE_STEAK -->

**Icon (EFST):** `EFST_SAVAGE_STEAK`

**Effect:** Increase STR

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +STR |

**Script Example:**
```c
sc_start SC_SAVAGE_STEAK, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_COCKTAIL_WARG_BLOOD

<!-- RAG_CHUNK: SC_COCKTAIL_WARG_BLOOD -->

**Icon (EFST):** `EFST_COCKTAIL_WARG_BLOOD`

**Effect:** Increase INT

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +INT |

**Script Example:**
```c
sc_start SC_COCKTAIL_WARG_BLOOD, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MINOR_BBQ

<!-- RAG_CHUNK: SC_MINOR_BBQ -->

**Icon (EFST):** `EFST_MINOR_BBQ`

**Effect:** Increase VIT

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +VIT |

**Script Example:**
```c
sc_start SC_MINOR_BBQ, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SIROMA_ICE_TEA

<!-- RAG_CHUNK: SC_SIROMA_ICE_TEA -->

**Icon (EFST):** `EFST_SIROMA_ICE_TEA`

**Effect:** Increase DEX

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +DEX |

**Script Example:**
```c
sc_start SC_SIROMA_ICE_TEA, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_DROCERA_HERB_STEAMED

<!-- RAG_CHUNK: SC_DROCERA_HERB_STEAMED -->

**Icon (EFST):** `EFST_DROCERA_HERB_STEAMED`

**Effect:** Increase AGI

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +AGI |

**Script Example:**
```c
sc_start SC_DROCERA_HERB_STEAMED, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PUTTI_TAILS_NOODLES

<!-- RAG_CHUNK: SC_PUTTI_TAILS_NOODLES -->

**Icon (EFST):** `EFST_PUTTI_TAILS_NOODLES`

**Effect:** Increase LUK

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +LUK |

**Script Example:**
```c
sc_start SC_PUTTI_TAILS_NOODLES, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_BOOST500

<!-- RAG_CHUNK: SC_BOOST500 -->

**Icon (EFST):** `EFST_BOOST500`

**Effect:** Increase ASPD rate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Aspd |

**Script Example:**
```c
sc_start SC_BOOST500, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_FULL_SWING_K

<!-- RAG_CHUNK: SC_FULL_SWING_K -->

**Icon (EFST):** `EFST_FULL_SWING_K`

**Effect:** Increase Base Atk

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +BaseAtk |

**Script Example:**
```c
sc_start SC_FULL_SWING_K, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MANA_PLUS

<!-- RAG_CHUNK: SC_MANA_PLUS -->

**Icon (EFST):** `EFST_MANA_PLUS`

**Effect:** Increase MAtk

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +Matk |

**Script Example:**
```c
sc_start SC_MANA_PLUS, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MUSTLE_M

<!-- RAG_CHUNK: SC_MUSTLE_M -->

**Icon (EFST):** `EFST_MUSTLE_M`

**Effect:** Increase Max HP rate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% MaxHP |

**Script Example:**
```c
sc_start SC_MUSTLE_M, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_LIFE_FORCE_F

<!-- RAG_CHUNK: SC_LIFE_FORCE_F -->

**Icon (EFST):** `EFST_LIFE_FORCE_F`

**Effect:** Increase Max SP rate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% MaxSP |

**Script Example:**
```c
sc_start SC_LIFE_FORCE_F, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_EXTRACT_WHITE_POTION_Z

<!-- RAG_CHUNK: SC_EXTRACT_WHITE_POTION_Z -->

**Icon (EFST):** `EFST_EXTRACT_WHITE_POTION_Z`

**Effect:** Increase HP regen rate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% HP regen |

**Script Example:**
```c
sc_start SC_EXTRACT_WHITE_POTION_Z, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_VITATA_500

<!-- RAG_CHUNK: SC_VITATA_500 -->

**Icon (EFST):** `EFST_VITATA_500`

**Effect:** Increase SP Regen rate & Max SP rate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% SP regen |
| val2 | +% MaxSP |

**Script Example:**
```c
sc_start SC_VITATA_500, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_EXTRACT_SALAMINE_JUICE

<!-- RAG_CHUNK: SC_EXTRACT_SALAMINE_JUICE -->

**Icon (EFST):** `EFST_EXTRACT_SALAMINE_JUICE`

**Effect:** Increase ASP rate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% ASPD |

**Script Example:**
```c
sc_start SC_EXTRACT_SALAMINE_JUICE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC__REPRODUCE

<!-- RAG_CHUNK: SC__REPRODUCE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__REPRODUCE, 60000, 1;
```

---

### SC__AUTOSHADOWSPELL

<!-- RAG_CHUNK: SC__AUTOSHADOWSPELL -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__AUTOSHADOWSPELL, 60000, 1;
```

---

### SC__SHADOWFORM

<!-- RAG_CHUNK: SC__SHADOWFORM -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__SHADOWFORM, 60000, 1;
```

---

### SC__BODYPAINT

<!-- RAG_CHUNK: SC__BODYPAINT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__BODYPAINT, 60000, 1;
```

---

### SC__INVISIBILITY

<!-- RAG_CHUNK: SC__INVISIBILITY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__INVISIBILITY, 60000, 1;
```

---

### SC__DEADLYINFECT

<!-- RAG_CHUNK: SC__DEADLYINFECT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__DEADLYINFECT, 60000, 1;
```

---

### SC__ENERVATION

<!-- RAG_CHUNK: SC__ENERVATION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__ENERVATION, 60000, 1;
```

---

### SC__GROOMY

<!-- RAG_CHUNK: SC__GROOMY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__GROOMY, 60000, 1;
```

---

### SC__IGNORANCE

<!-- RAG_CHUNK: SC__IGNORANCE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__IGNORANCE, 60000, 1;
```

---

### SC__LAZINESS

<!-- RAG_CHUNK: SC__LAZINESS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__LAZINESS, 60000, 1;
```

---

### SC__UNLUCKY

<!-- RAG_CHUNK: SC__UNLUCKY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__UNLUCKY, 60000, 1;
```

---

### SC__WEAKNESS

<!-- RAG_CHUNK: SC__WEAKNESS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__WEAKNESS, 60000, 1;
```

---

### SC__STRIPACCESSORY

<!-- RAG_CHUNK: SC__STRIPACCESSORY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__STRIPACCESSORY, 60000, 1;
```

---

### SC__MANHOLE

<!-- RAG_CHUNK: SC__MANHOLE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__MANHOLE, 60000, 1;
```

---

### SC__BLOODYLUST

<!-- RAG_CHUNK: SC__BLOODYLUST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__BLOODYLUST, 60000, 1;
```

---

### SC_CIRCLE_OF_FIRE

<!-- RAG_CHUNK: SC_CIRCLE_OF_FIRE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CIRCLE_OF_FIRE, 60000, 1;
```

---

### SC_CIRCLE_OF_FIRE_OPTION

<!-- RAG_CHUNK: SC_CIRCLE_OF_FIRE_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CIRCLE_OF_FIRE_OPTION, 60000, 1;
```

---

### SC_FIRE_CLOAK

<!-- RAG_CHUNK: SC_FIRE_CLOAK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FIRE_CLOAK, 60000, 1;
```

---

### SC_FIRE_CLOAK_OPTION

<!-- RAG_CHUNK: SC_FIRE_CLOAK_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FIRE_CLOAK_OPTION, 60000, 1;
```

---

### SC_WATER_SCREEN

<!-- RAG_CHUNK: SC_WATER_SCREEN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WATER_SCREEN, 60000, 1;
```

---

### SC_WATER_SCREEN_OPTION

<!-- RAG_CHUNK: SC_WATER_SCREEN_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WATER_SCREEN_OPTION, 60000, 1;
```

---

### SC_WATER_DROP

<!-- RAG_CHUNK: SC_WATER_DROP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WATER_DROP, 60000, 1;
```

---

### SC_WATER_DROP_OPTION

<!-- RAG_CHUNK: SC_WATER_DROP_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WATER_DROP_OPTION, 60000, 1;
```

---

### SC_WATER_BARRIER

<!-- RAG_CHUNK: SC_WATER_BARRIER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WATER_BARRIER, 60000, 1;
```

---

### SC_WIND_STEP

<!-- RAG_CHUNK: SC_WIND_STEP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WIND_STEP, 60000, 1;
```

---

### SC_WIND_STEP_OPTION

<!-- RAG_CHUNK: SC_WIND_STEP_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WIND_STEP_OPTION, 60000, 1;
```

---

### SC_WIND_CURTAIN

<!-- RAG_CHUNK: SC_WIND_CURTAIN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WIND_CURTAIN, 60000, 1;
```

---

### SC_WIND_CURTAIN_OPTION

<!-- RAG_CHUNK: SC_WIND_CURTAIN_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WIND_CURTAIN_OPTION, 60000, 1;
```

---

### SC_ZEPHYR

<!-- RAG_CHUNK: SC_ZEPHYR -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ZEPHYR, 60000, 1;
```

---

### SC_SOLID_SKIN

<!-- RAG_CHUNK: SC_SOLID_SKIN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SOLID_SKIN, 60000, 1;
```

---

### SC_SOLID_SKIN_OPTION

<!-- RAG_CHUNK: SC_SOLID_SKIN_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SOLID_SKIN_OPTION, 60000, 1;
```

---

### SC_STONE_SHIELD

<!-- RAG_CHUNK: SC_STONE_SHIELD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STONE_SHIELD, 60000, 1;
```

---

### SC_STONE_SHIELD_OPTION

<!-- RAG_CHUNK: SC_STONE_SHIELD_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STONE_SHIELD_OPTION, 60000, 1;
```

---

### SC_POWER_OF_GAIA

<!-- RAG_CHUNK: SC_POWER_OF_GAIA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_POWER_OF_GAIA, 60000, 1;
```

---

### SC_PYROTECHNIC

<!-- RAG_CHUNK: SC_PYROTECHNIC -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PYROTECHNIC, 60000, 1;
```

---

### SC_PYROTECHNIC_OPTION

<!-- RAG_CHUNK: SC_PYROTECHNIC_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PYROTECHNIC_OPTION, 60000, 1;
```

---

### SC_HEATER

<!-- RAG_CHUNK: SC_HEATER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HEATER, 60000, 1;
```

---

### SC_HEATER_OPTION

<!-- RAG_CHUNK: SC_HEATER_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HEATER_OPTION, 60000, 1;
```

---

### SC_TROPIC

<!-- RAG_CHUNK: SC_TROPIC -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_TROPIC, 60000, 1;
```

---

### SC_TROPIC_OPTION

<!-- RAG_CHUNK: SC_TROPIC_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_TROPIC_OPTION, 60000, 1;
```

---

### SC_AQUAPLAY

<!-- RAG_CHUNK: SC_AQUAPLAY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_AQUAPLAY, 60000, 1;
```

---

### SC_AQUAPLAY_OPTION

<!-- RAG_CHUNK: SC_AQUAPLAY_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_AQUAPLAY_OPTION, 60000, 1;
```

---

### SC_COOLER

<!-- RAG_CHUNK: SC_COOLER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_COOLER, 60000, 1;
```

---

### SC_COOLER_OPTION

<!-- RAG_CHUNK: SC_COOLER_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_COOLER_OPTION, 60000, 1;
```

---

### SC_CHILLY_AIR

<!-- RAG_CHUNK: SC_CHILLY_AIR -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CHILLY_AIR, 60000, 1;
```

---

### SC_CHILLY_AIR_OPTION

<!-- RAG_CHUNK: SC_CHILLY_AIR_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CHILLY_AIR_OPTION, 60000, 1;
```

---

### SC_GUST

<!-- RAG_CHUNK: SC_GUST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GUST, 60000, 1;
```

---

### SC_GUST_OPTION

<!-- RAG_CHUNK: SC_GUST_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GUST_OPTION, 60000, 1;
```

---

### SC_BLAST

<!-- RAG_CHUNK: SC_BLAST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BLAST, 60000, 1;
```

---

### SC_BLAST_OPTION

<!-- RAG_CHUNK: SC_BLAST_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BLAST_OPTION, 60000, 1;
```

---

### SC_WILD_STORM

<!-- RAG_CHUNK: SC_WILD_STORM -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WILD_STORM, 60000, 1;
```

---

### SC_WILD_STORM_OPTION

<!-- RAG_CHUNK: SC_WILD_STORM_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WILD_STORM_OPTION, 60000, 1;
```

---

### SC_PETROLOGY

<!-- RAG_CHUNK: SC_PETROLOGY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PETROLOGY, 60000, 1;
```

---

### SC_PETROLOGY_OPTION

<!-- RAG_CHUNK: SC_PETROLOGY_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PETROLOGY_OPTION, 60000, 1;
```

---

### SC_CURSED_SOIL

<!-- RAG_CHUNK: SC_CURSED_SOIL -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CURSED_SOIL, 60000, 1;
```

---

### SC_CURSED_SOIL_OPTION

<!-- RAG_CHUNK: SC_CURSED_SOIL_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CURSED_SOIL_OPTION, 60000, 1;
```

---

### SC_UPHEAVAL

<!-- RAG_CHUNK: SC_UPHEAVAL -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_UPHEAVAL, 60000, 1;
```

---

### SC_UPHEAVAL_OPTION

<!-- RAG_CHUNK: SC_UPHEAVAL_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_UPHEAVAL_OPTION, 60000, 1;
```

---

### SC_TIDAL_WEAPON

<!-- RAG_CHUNK: SC_TIDAL_WEAPON -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_TIDAL_WEAPON, 60000, 1;
```

---

### SC_TIDAL_WEAPON_OPTION

<!-- RAG_CHUNK: SC_TIDAL_WEAPON_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_TIDAL_WEAPON_OPTION, 60000, 1;
```

---

### SC_ROCK_CRUSHER

<!-- RAG_CHUNK: SC_ROCK_CRUSHER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ROCK_CRUSHER, 60000, 1;
```

---

### SC_ROCK_CRUSHER_ATK

<!-- RAG_CHUNK: SC_ROCK_CRUSHER_ATK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ROCK_CRUSHER_ATK, 60000, 1;
```

---

### SC_LEADERSHIP

<!-- RAG_CHUNK: SC_LEADERSHIP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_LEADERSHIP, 60000, 1;
```

---

### SC_GLORYWOUNDS

<!-- RAG_CHUNK: SC_GLORYWOUNDS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GLORYWOUNDS, 60000, 1;
```

---

### SC_SOULCOLD

<!-- RAG_CHUNK: SC_SOULCOLD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SOULCOLD, 60000, 1;
```

---

### SC_HAWKEYES

<!-- RAG_CHUNK: SC_HAWKEYES -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HAWKEYES, 60000, 1;
```

---

### SC_ODINS_POWER

<!-- RAG_CHUNK: SC_ODINS_POWER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ODINS_POWER, 60000, 1;
```

---

### SC_RAID

<!-- RAG_CHUNK: SC_RAID -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_RAID, 60000, 1;
```

---

### SC_FIRE_INSIGNIA

<!-- RAG_CHUNK: SC_FIRE_INSIGNIA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FIRE_INSIGNIA, 60000, 1;
```

---

### SC_WATER_INSIGNIA

<!-- RAG_CHUNK: SC_WATER_INSIGNIA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WATER_INSIGNIA, 60000, 1;
```

---

### SC_WIND_INSIGNIA

<!-- RAG_CHUNK: SC_WIND_INSIGNIA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WIND_INSIGNIA, 60000, 1;
```

---

### SC_EARTH_INSIGNIA

<!-- RAG_CHUNK: SC_EARTH_INSIGNIA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_EARTH_INSIGNIA, 60000, 1;
```

---

### SC_PUSH_CART

<!-- RAG_CHUNK: SC_PUSH_CART -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PUSH_CART, 60000, 1;
```

---

### SC_SPELLBOOK1

<!-- RAG_CHUNK: SC_SPELLBOOK1 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPELLBOOK1, 60000, 1;
```

---

### SC_SPELLBOOK2

<!-- RAG_CHUNK: SC_SPELLBOOK2 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPELLBOOK2, 60000, 1;
```

---

### SC_SPELLBOOK3

<!-- RAG_CHUNK: SC_SPELLBOOK3 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPELLBOOK3, 60000, 1;
```

---

### SC_SPELLBOOK4

<!-- RAG_CHUNK: SC_SPELLBOOK4 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPELLBOOK4, 60000, 1;
```

---

### SC_SPELLBOOK5

<!-- RAG_CHUNK: SC_SPELLBOOK5 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPELLBOOK5, 60000, 1;
```

---

### SC_SPELLBOOK6

<!-- RAG_CHUNK: SC_SPELLBOOK6 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPELLBOOK6, 60000, 1;
```

---

### SC_MAXSPELLBOOK

<!-- RAG_CHUNK: SC_MAXSPELLBOOK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MAXSPELLBOOK, 60000, 1;
```

---

### SC_INCMHP

<!-- RAG_CHUNK: SC_INCMHP -->

**Effect:** Increase Max HP

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + Max HP |

**Script Example:**
```c
sc_start SC_INCMHP, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCMSP

<!-- RAG_CHUNK: SC_INCMSP -->

**Effect:** Incrase Max SP

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + MaxSP |

**Script Example:**
```c
sc_start SC_INCMSP, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PARTYFLEE

<!-- RAG_CHUNK: SC_PARTYFLEE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PARTYFLEE, 60000, 1;
```

---

### SC_MEIKYOUSISUI

<!-- RAG_CHUNK: SC_MEIKYOUSISUI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MEIKYOUSISUI, 60000, 1;
```

---

### SC_JYUMONJIKIRI

<!-- RAG_CHUNK: SC_JYUMONJIKIRI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_JYUMONJIKIRI, 60000, 1;
```

---

### SC_KYOUGAKU

<!-- RAG_CHUNK: SC_KYOUGAKU -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KYOUGAKU, 60000, 1;
```

---

### SC_IZAYOI

<!-- RAG_CHUNK: SC_IZAYOI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_IZAYOI, 60000, 1;
```

---

### SC_ZENKAI

<!-- RAG_CHUNK: SC_ZENKAI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ZENKAI, 60000, 1;
```

---

### SC_KAGEHUMI

<!-- RAG_CHUNK: SC_KAGEHUMI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KAGEHUMI, 60000, 1;
```

---

### SC_KYOMU

<!-- RAG_CHUNK: SC_KYOMU -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KYOMU, 60000, 1;
```

---

### SC_KAGEMUSYA

<!-- RAG_CHUNK: SC_KAGEMUSYA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KAGEMUSYA, 60000, 1;
```

---

### SC_ZANGETSU

<!-- RAG_CHUNK: SC_ZANGETSU -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ZANGETSU, 60000, 1;
```

---

### SC_GENSOU

<!-- RAG_CHUNK: SC_GENSOU -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GENSOU, 60000, 1;
```

---

### SC_AKAITSUKI

<!-- RAG_CHUNK: SC_AKAITSUKI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_AKAITSUKI, 60000, 1;
```

---

### SC_STYLE_CHANGE

<!-- RAG_CHUNK: SC_STYLE_CHANGE -->

**Effect:** Eleanor's mode

**Script Example:**
```c
sc_start SC_STYLE_CHANGE, 60000, 1;
```

---

### SC_TINDER_BREAKER

<!-- RAG_CHUNK: SC_TINDER_BREAKER -->

**Icon (EFST):** `EFST_TINDER_BREAKER_POSTDELAY`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_TINDER_BREAKER, 60000, 1;
```

---

### SC_TINDER_BREAKER2

<!-- RAG_CHUNK: SC_TINDER_BREAKER2 -->

**Icon (EFST):** `EFST_TINDER_BREAKER`

**Effect:** Tinder Breaker after-effect, just like Close Confine

**Script Example:**
```c
sc_start SC_TINDER_BREAKER2, 60000, 1;
```

---

### SC_CBC

<!-- RAG_CHUNK: SC_CBC -->

**Icon (EFST):** `EFST_CBC`

**Effect:** Drain HP & SP each iteration (default is each 1 sec)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val3 | %SP drain |

**Script Example:**
```c
sc_start SC_CBC, 60000, 1;
```

---

### SC_EQC

<!-- RAG_CHUNK: SC_EQC -->

**Icon (EFST):** `EFST_EQC`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | -% Def |
| val3 | -%MaxHP |

**Script Example:**
```c
sc_start SC_EQC, 60000, 1;
```

---

### SC_GOLDENE_FERSE

<!-- RAG_CHUNK: SC_GOLDENE_FERSE -->

**Icon (EFST):** `EFST_GOLDENE_FERSE`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | +% Flee |
| val3 | +% ASPD |
| val4 | % Chance to convert attack as Holy element |

**Script Example:**
```c
sc_start SC_GOLDENE_FERSE, 60000, 1;
```

---

### SC_ANGRIFFS_MODUS

<!-- RAG_CHUNK: SC_ANGRIFFS_MODUS -->

**Icon (EFST):** `EFST_ANGRIFFS_MODUS`

**Effect:** Drain 100 HP & 20 SP each iteration (default is each 1 sec)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Level. Usage for +MaxHP rate (5 * level) |
| val2 | +ATK |
| val3 | -Flee |

**Script Example:**
```c
sc_start SC_ANGRIFFS_MODUS, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_OVERED_BOOST

<!-- RAG_CHUNK: SC_OVERED_BOOST -->

**Icon (EFST):** `EFST_OVERED_BOOST`

**Effect:** When status ended, reduce 50% HP for player and increase 50 the Homunculus's hunger

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | Fixed Flee value |
| val3 | Fixed ASPD value |
| val4 | -% Def |

**Script Example:**
```c
sc_start SC_OVERED_BOOST, 60000, 1;
```

---

### SC_LIGHT_OF_REGENE

<!-- RAG_CHUNK: SC_LIGHT_OF_REGENE -->

**Icon (EFST):** `EFST_LIGHT_OF_REGENE`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | % of HP recovery on death |

**Script Example:**
```c
sc_start SC_LIGHT_OF_REGENE, 60000, 1;
```

---

### SC_ASH

<!-- RAG_CHUNK: SC_ASH -->

**Icon (EFST):** `EFST_VOLCANIC_ASH`

**Effect:** Increase damage to Fire element enemy (ratio +150%), reduce Hit, Def, Atk & Flee.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | -% Hit |
| val2 | -% Def |
| val4 | -Atk & Flee |

**Script Example:**
```c
sc_start SC_ASH, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_GRANITIC_ARMOR

<!-- RAG_CHUNK: SC_GRANITIC_ARMOR -->

**Icon (EFST):** `EFST_GRANITIC_ARMOR`

**Effect:** Reduce the inflicted damage, when status ended deals another damage to self

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | -%Damage |
| val3 | Damage taken on status end |

**Script Example:**
```c
sc_start SC_GRANITIC_ARMOR, 60000, 1;
```

---

### SC_MAGMA_FLOW

<!-- RAG_CHUNK: SC_MAGMA_FLOW -->

**Icon (EFST):** `EFST_MAGMA_FLOW`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | Rate to cast Magma Flow (deals damage) to target while attacking |

**Script Example:**
```c
sc_start SC_MAGMA_FLOW, 60000, 1;
```

---

### SC_PYROCLASTIC

<!-- RAG_CHUNK: SC_PYROCLASTIC -->

**Icon (EFST):** `EFST_PYROCLASTIC`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | +ATK |
| val3 | % Rate to cast Hammer Fall |

**Script Example:**
```c
sc_start SC_PYROCLASTIC, 60000, 1;
```

---

### SC_PARALYSIS

<!-- RAG_CHUNK: SC_PARALYSIS -->

**Icon (EFST):** `EFST_NEEDLE_OF_PARALYZE`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | -Def |
| val3 | +% CastTime |

**Script Example:**
```c
sc_start SC_PARALYSIS, 60000, 1;
```

---

### SC_PAIN_KILLER

<!-- RAG_CHUNK: SC_PAIN_KILLER -->

**Icon (EFST):** `EFST_PAIN_KILLER`

**Effect:** Reduce damage for certain value, reduce ASPD rate, inflict Endure if has active SC_PARALYSIS

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | -% ASPD |
| val3 | -Damage |

**Script Example:**
```c
sc_start SC_PAIN_KILLER, 60000, 1;
```

---

### SC_HANBOK

<!-- RAG_CHUNK: SC_HANBOK -->

**Effect:** Visual effect. Hanbok costume!

**Script Example:**
```c
sc_start SC_HANBOK, 60000, 1;
```

---

### SC_DEFSET

<!-- RAG_CHUNK: SC_DEFSET -->

**Effect:** Vellum Weapon bonus. Set Def value

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Def fixed value |

**Script Example:**
```c
sc_start SC_DEFSET, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MDEFSET

<!-- RAG_CHUNK: SC_MDEFSET -->

**Effect:** Vellum Weapon bonus. Set MDef value

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | MDef fixed value |

**Script Example:**
```c
sc_start SC_MDEFSET, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_DARKCROW

<!-- RAG_CHUNK: SC_DARKCROW -->

**Icon (EFST):** `EFST_DARKCROW`

**Effect:** Increase short/melee damage rate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | +% Damage |

**Script Example:**
```c
sc_start SC_DARKCROW, 60000, 1;
```

---

### SC_FULL_THROTTLE

<!-- RAG_CHUNK: SC_FULL_THROTTLE -->

**Icon (EFST):** `EFST_FULL_THROTTLE`

**Effect:** Increase walk speed, increase allstats, full HP once activated

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Level, also used as Rebound level when this sc ended |
| val2 | -SP each iteration |
| val3 | +% Allstats |

**Script Example:**
```c
sc_start SC_FULL_THROTTLE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_REBOUND

<!-- RAG_CHUNK: SC_REBOUND -->

**Icon (EFST):** `EFST_REBOUND`

**Effect:** Full Throttle  after-effect. Reduce walk speed

**Script Example:**
```c
sc_start SC_REBOUND, 60000, 1;
```

---

### SC_UNLIMIT

<!-- RAG_CHUNK: SC_UNLIMIT -->

**Icon (EFST):** `EFST_UNLIMIT`

**Effect:** Increase attak rate & set Def/MDef to 1,

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | +% Attack |

**Script Example:**
```c
sc_start SC_UNLIMIT, 60000, 1;
```

---

### SC_KINGS_GRACE

<!-- RAG_CHUNK: SC_KINGS_GRACE -->

**Icon (EFST):** `EFST_KINGS_GRACE`

**Effect:** Add Max HP & heal each iteration (default 1 seconds)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | +HP heal |

**Script Example:**
```c
sc_start SC_KINGS_GRACE, 60000, 1;
```

---

### SC_TELEKINESIS_INTENSE

<!-- RAG_CHUNK: SC_TELEKINESIS_INTENSE -->

**Effect:** Increase SP cost & damage of Ghost skill, reduce casttime

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | +% SP Cost |
| val3 | +Damage ratio |
| val4 | -CastTime |

**Script Example:**
```c
sc_start SC_TELEKINESIS_INTENSE, 60000, 1;
```

---

### SC_OFFERTORIUM

<!-- RAG_CHUNK: SC_OFFERTORIUM -->

**Icon (EFST):** `EFST_OFFERTORIUM`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | +Heal Power |
| val3 | +SP Cost |

**Script Example:**
```c
sc_start SC_OFFERTORIUM, 60000, 1;
```

---

### SC_FRIGG_SONG

<!-- RAG_CHUNK: SC_FRIGG_SONG -->

**Icon (EFST):** `EFST_FRIGG_SONG`

**Effect:** Add Max HP & heal each iteration (default 1 seconds)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Level |
| val2 | +% MaxHP |
| val3 | +HP heal |

**Script Example:**
```c
sc_start SC_FRIGG_SONG, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MONSTER_TRANSFORM

<!-- RAG_CHUNK: SC_MONSTER_TRANSFORM -->

**Effect:** Monster Transformation. (DO NOT USE THIS DIRECTLY, use script 'transform')

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Monster ID |

**Script Example:**
```c
sc_start SC_MONSTER_TRANSFORM, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_ANGEL_PROTECT

<!-- RAG_CHUNK: SC_ANGEL_PROTECT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ANGEL_PROTECT, 60000, 1;
```

---

### SC_ILLUSIONDOPING

<!-- RAG_CHUNK: SC_ILLUSIONDOPING -->

**Icon (EFST):** `EFST_ILLUSIONDOPING`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | -Hit |

**Script Example:**
```c
sc_start SC_ILLUSIONDOPING, 60000, 1;
```

---

### SC_FLASHCOMBO

<!-- RAG_CHUNK: SC_FLASHCOMBO -->

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | +ATK (isn't shown in status window) |

**Script Example:**
```c
sc_start SC_FLASHCOMBO, 60000, 1;
```

---

### SC_MOONSTAR

<!-- RAG_CHUNK: SC_MOONSTAR -->

**Icon (EFST):** `EFST_MOONSTAR`

**Effect:** Visual effect

**Script Example:**
```c
sc_start SC_MOONSTAR, 60000, 1;
```

---

### SC_SUPER_STAR

<!-- RAG_CHUNK: SC_SUPER_STAR -->

**Icon (EFST):** `EFST_SUPER_STAR`

**Effect:** Visual effect

**Script Example:**
```c
sc_start SC_SUPER_STAR, 60000, 1;
```

---

### SC_HEAT_BARREL

<!-- RAG_CHUNK: SC_HEAT_BARREL -->

**Icon (EFST):** `EFST_HEAT_BARREL`

**Effect:** (Rebellion) Reduce fixed cast time, add ASPD rate, and reduce FLEE

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | SkillLv |
| val2 | -Fixed Casttime (5 * val1) |
| val3 | +% ASPD (6 + val1 * 2) |
| val4 | -FLEE (25 + val1 * 5) |

**Script Example:**
```c
sc_start SC_HEAT_BARREL, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_P_ALTER

<!-- RAG_CHUNK: SC_P_ALTER -->

**Icon (EFST):** `EFST_P_ALTER`

**Effect:** Increase attack ratio and creates a barrier like Kyrie

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | SkillLv |
| val2 | +ATK ratio (10 * Coin Count) |
| val3 | Barrier HP (Max HP * (val1 * 5) / 100) |

**Script Example:**
```c
sc_start SC_P_ALTER, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_E_CHAIN

<!-- RAG_CHUNK: SC_E_CHAIN -->

**Icon (EFST):** `EFST_E_CHAIN`

**Effect:** (Rebellion) Has chance to trigger Chain Action for any weapon

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | SkillLv |
| val2 | Coins used for success rate. (5 * val) |

**Script Example:**
```c
sc_start SC_E_CHAIN, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_C_MARKER

<!-- RAG_CHUNK: SC_C_MARKER -->

**Icon (EFST):** `EFST_C_MARKER`

**Effect:** (Rebellion) Crimson Marker effect, also sends the target location to the caster

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | SkillLv |
| val3 | -FLEE (10) |

**Script Example:**
```c
sc_start SC_C_MARKER, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_ANTI_M_BLAST

<!-- RAG_CHUNK: SC_ANTI_M_BLAST -->

**Icon (EFST):** `EFST_ANTI_M_BLAST`

**Effect:** (Rebellion) Anti-Material effect, reduce resistance of Neutral attack

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | SkillLv |
| val2 | Reduction ratio (10 * val1) |

**Script Example:**
```c
sc_start SC_ANTI_M_BLAST, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_B_TRAP

<!-- RAG_CHUNK: SC_B_TRAP -->

**Icon (EFST):** `EFST_B_TRAP`

**Effect:** (Rebellion) Bind Trap effect, waiting for Flicker to be used

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | SkillLv |
| val3 | -Walk Speed (Unstackable penalty) (25 * val1) |

**Script Example:**
```c
sc_start SC_B_TRAP, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_H_MINE

<!-- RAG_CHUNK: SC_H_MINE -->

**Icon (EFST):** `EFST_H_MINE`

**Effect:** (Rebellion) Howling Mine effect, waiting for Flicker to be used

**Script Example:**
```c
sc_start SC_H_MINE, 60000, 1;
```

---

### SC_QD_SHOT_READY

<!-- RAG_CHUNK: SC_QD_SHOT_READY -->

**Icon (EFST):** `EFST_E_QD_SHOT_READY`

**Effect:** (Rebellion) Combo stance to cast Quick Draw Shot

**Script Example:**
```c
sc_start SC_QD_SHOT_READY, 60000, 1;
```

---

### SC_MTF_ASPD

<!-- RAG_CHUNK: SC_MTF_ASPD -->

**Icon (EFST):** `EFST_MTF_ASPD`

**Effect:** Increase ASP and Hit

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +ASPD |
| val2 | +Hit |

**Script Example:**
```c
sc_start SC_MTF_ASPD, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MTF_ASPD2

<!-- RAG_CHUNK: SC_MTF_ASPD2 -->

**Icon (EFST):** `EFST_MTF_ASPD2`

**Effect:** Increase ASP and Hit

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +ASPD |
| val2 | +Hit |

**Script Example:**
```c
sc_start SC_MTF_ASPD2, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MTF_RANGEATK

<!-- RAG_CHUNK: SC_MTF_RANGEATK -->

**Icon (EFST):** `EFST_MTF_RANGEATK`

**Effect:** Increase Long-ranged damage while attacking

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Damage (not be shown in status window) |

**Script Example:**
```c
sc_start SC_MTF_RANGEATK, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MTF_RANGEATK2

<!-- RAG_CHUNK: SC_MTF_RANGEATK2 -->

**Icon (EFST):** `EFST_MTF_RANGEATK2`

**Effect:** Increase Long-ranged damage while attacking

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Damage (not be shown in status window) |

**Script Example:**
```c
sc_start SC_MTF_RANGEATK2, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MTF_MATK

<!-- RAG_CHUNK: SC_MTF_MATK -->

**Icon (EFST):** `EFST_MTF_MATK`

**Effect:** Increase MATK damage while attacking

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% MATK |

**Script Example:**
```c
sc_start SC_MTF_MATK, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MTF_MATK2

<!-- RAG_CHUNK: SC_MTF_MATK2 -->

**Icon (EFST):** `EFST_MTF_MATK2`

**Effect:** Increase MATK damage while attacking

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + MATK |

**Script Example:**
```c
sc_start SC_MTF_MATK2, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MTF_MLEATKED

<!-- RAG_CHUNK: SC_MTF_MLEATKED -->

**Icon (EFST):** `EFST_MTF_MLEATKED`

**Effect:** Has chance to cast Endure to self while attacked

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Endure Level |
| val2 | Rate to cast |
| val3 | Neutral element resistance |

**Script Example:**
```c
sc_start SC_MTF_MLEATKED, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_MTF_CRIDAMAGE

<!-- RAG_CHUNK: SC_MTF_CRIDAMAGE -->

**Icon (EFST):** `EFST_MTF_CRIDAMAGE`

**Effect:** Bonus critical rate of monster transformation

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Critical |

**Script Example:**
```c
sc_start SC_MTF_CRIDAMAGE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_OKTOBERFEST

<!-- RAG_CHUNK: SC_OKTOBERFEST -->

**Effect:** Costume

**Script Example:**
```c
sc_start SC_OKTOBERFEST, 60000, 1;
```

---

### SC_STRANGELIGHTS

<!-- RAG_CHUNK: SC_STRANGELIGHTS -->

**Icon (EFST):** `EFST_STRANGELIGHTS`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STRANGELIGHTS, 60000, 1;
```

---

### SC_DECORATION_OF_MUSIC

<!-- RAG_CHUNK: SC_DECORATION_OF_MUSIC -->

**Icon (EFST):** `EFST_DECORATION_OF_MUSIC`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DECORATION_OF_MUSIC, 60000, 1;
```

---

### SC_QUEST_BUFF1

<!-- RAG_CHUNK: SC_QUEST_BUFF1 -->

**Icon (EFST):** `EFST_QUEST_BUFF1`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +ATK & +MATK |

**Script Example:**
```c
sc_start SC_QUEST_BUFF1, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_QUEST_BUFF2

<!-- RAG_CHUNK: SC_QUEST_BUFF2 -->

**Icon (EFST):** `EFST_QUEST_BUFF2`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +ATK & +MATK |

**Script Example:**
```c
sc_start SC_QUEST_BUFF2, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_QUEST_BUFF3

<!-- RAG_CHUNK: SC_QUEST_BUFF3 -->

**Icon (EFST):** `EFST_QUEST_BUFF3`

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +ATK & +MATK |

**Script Example:**
```c
sc_start SC_QUEST_BUFF3, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_ALL_RIDING

<!-- RAG_CHUNK: SC_ALL_RIDING -->

**Icon (EFST):** `EFST_ALL_RIDING`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ALL_RIDING, 60000, 1;
```

---

### SC_TEARGAS_SOB

<!-- RAG_CHUNK: SC_TEARGAS_SOB -->

**Effect:** 2nd Teargas effect, do /sob expression each 3 seconds

**Script Example:**
```c
sc_start SC_TEARGAS_SOB, 60000, 1;
```

---

### SC__FEINTBOMB

<!-- RAG_CHUNK: SC__FEINTBOMB -->

**Effect:** (See source code for details)

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | -1 SP each second |

**Script Example:**
```c
sc_start SC__FEINTBOMB, 60000, 1;
```

---

### SC__CHAOS

<!-- RAG_CHUNK: SC__CHAOS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__CHAOS, 60000, 1;
```

---

### SC_ELEMENTAL_SHIELD

<!-- RAG_CHUNK: SC_ELEMENTAL_SHIELD -->

**Effect:** Block magic attack

**Script Example:**
```c
sc_start SC_ELEMENTAL_SHIELD, 60000, 1;
```

---

### SC_CHASEWALK2

<!-- RAG_CHUNK: SC_CHASEWALK2 -->

**Icon (EFST):** `EFST_CHASEWALK2`

**Effect:** 2nd effect of Chasewalk

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +STR |

**Script Example:**
```c
sc_start SC_CHASEWALK2, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SUHIDE

<!-- RAG_CHUNK: SC_SUHIDE -->

**Icon (EFST):** `EFST_SUHIDE`

**Effect:** Hide caster. Can be seen by insect, demon, and boss. Cannot move or pickup items.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |

**Script Example:**
```c
sc_start SC_SUHIDE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SU_STOOP

<!-- RAG_CHUNK: SC_SU_STOOP -->

**Icon (EFST):** `EFST_SU_STOOP`

**Effect:** Places a temporary buff on the user that decreases all damage taken by 90%.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |

**Script Example:**
```c
sc_start SC_SU_STOOP, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SPRITEMABLE

<!-- RAG_CHUNK: SC_SPRITEMABLE -->

**Icon (EFST):** `EFST_SPRITEMABLE`

**Effect:** Increase 1000 HP and 100 SP.

**Script Example:**
```c
sc_start SC_SPRITEMABLE, 60000, 1;
```

---

### SC_CATNIPPOWDER

<!-- RAG_CHUNK: SC_CATNIPPOWDER -->

**Icon (EFST):** `EFST_CATNIPPOWDER`

**Effect:** Reduces ATK and MATK by 50% to targets in a 3x3~7x7 area. HP and SP recovery rate increase.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |
| val2 | WATK% / MATK% |
| val3 | Movement speed reduction |

**Script Example:**
```c
sc_start SC_CATNIPPOWDER, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SV_ROOTTWIST

<!-- RAG_CHUNK: SC_SV_ROOTTWIST -->

**Icon (EFST):** `EFST_SV_ROOTTWIST`

**Effect:** Prevents the target from moving and receives 100 Poison damage every second. Cannot be used on Boss monsters.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |

**Script Example:**
```c
sc_start SC_SV_ROOTTWIST, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_BITESCAR

<!-- RAG_CHUNK: SC_BITESCAR -->

**Icon (EFST):** `EFST_BITESCAR`

**Effect:** Drains a portion of the target's Max HP each second.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |
| val2 | Max HP% damage |
| val4 | Tick |

**Script Example:**
```c
sc_start SC_BITESCAR, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_ARCLOUSEDASH

<!-- RAG_CHUNK: SC_ARCLOUSEDASH -->

**Icon (EFST):** `EFST_ARCLOUSEDASH`

**Effect:** Increases Agi and movement speed.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | AGI |
| val2 | Movement speed increase |
| val4 | Ranged ATK increase for Doram |

**Script Example:**
```c
sc_start SC_ARCLOUSEDASH, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_TUNAPARTY

<!-- RAG_CHUNK: SC_TUNAPARTY -->

**Icon (EFST):** `EFST_TUNAPARTY`

**Effect:** Protects from damage, the amount is based on Max HP.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Max HP% to absorb |
| val2 | Double the shield life with Spirit of Sea |

**Script Example:**
```c
sc_start SC_TUNAPARTY, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SHRIMP

<!-- RAG_CHUNK: SC_SHRIMP -->

**Icon (EFST):** `EFST_SHRIMP`

**Effect:** Gives all party members on screen +10% ATK and MATK.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | BATK% / MATK% |

**Script Example:**
```c
sc_start SC_SHRIMP, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_FRESHSHRIMP

<!-- RAG_CHUNK: SC_FRESHSHRIMP -->

**Icon (EFST):** `EFST_FRESHSHRIMP`

**Effect:** Recovers a small amount of HP. Each level reduces the time between each HP recovery tick.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |
| val2 | Heal amount |
| val4 | Tick |

**Script Example:**
```c
sc_start SC_FRESHSHRIMP, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_HISS

<!-- RAG_CHUNK: SC_HISS -->

**Icon (EFST):** `EFST_HISS`

**Effect:** Increases movement speed and perfect dodge of the user and his party.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |
| val2 | Perfect Dodge |

**Script Example:**
```c
sc_start SC_HISS, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_NYANGGRASS

<!-- RAG_CHUNK: SC_NYANGGRASS -->

**Icon (EFST):** `EFST_NYANGGRASS`

**Effect:** Reduces monster's DEF and MDEF by 50%. Reduces other player's equipment DEF and MDEF to 0.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |

**Script Example:**
```c
sc_start SC_NYANGGRASS, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_GROOMING

<!-- RAG_CHUNK: SC_GROOMING -->

**Icon (EFST):** `EFST_GROOMING`

**Effect:** FLEE + 100. Cures Poison, Frozen, Stun, Sleep, Bleeding, Silence, Crystallization, Deep Sleep, Fear, and Mandragora Howling.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |
| val2 | FLEE |

**Script Example:**
```c
sc_start SC_GROOMING, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_SHRIMPBLESSING

<!-- RAG_CHUNK: SC_SHRIMPBLESSING -->

**Icon (EFST):** `EFST_PROTECTIONOFSHRIMP`

**Effect:** Increases caster's SP recovery by 150%.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |

**Script Example:**
```c
sc_start SC_SHRIMPBLESSING, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CHATTERING

<!-- RAG_CHUNK: SC_CHATTERING -->

**Icon (EFST):** `EFST_CHATTERING`

**Effect:** Increases the player's ATK and MATK by 100. Increases the player's movespeed.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Skill Lv |
| val2 | ATK / MATK |

**Script Example:**
```c
sc_start SC_CHATTERING, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_DORAM_WALKSPEED

<!-- RAG_CHUNK: SC_DORAM_WALKSPEED -->

**Effect:** Adjusts player's walk speed.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Movement speed adjustment |

**Script Example:**
```c
sc_start SC_DORAM_WALKSPEED, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_DORAM_MATK

<!-- RAG_CHUNK: SC_DORAM_MATK -->

**Effect:** Statically increases MATK for Spirit of Land.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | MATK |

**Script Example:**
```c
sc_start SC_DORAM_MATK, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_DORAM_FLEE2

<!-- RAG_CHUNK: SC_DORAM_FLEE2 -->

**Effect:** Statically increase FLEE2 for Spirit of Land.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | FLEE2 |

**Script Example:**
```c
sc_start SC_DORAM_FLEE2, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_DORAM_SVSP

<!-- RAG_CHUNK: SC_DORAM_SVSP -->

**Effect:** Casts Silvervine Stem Spear when receiving Magic or Ranged damage after using Catnip Meteor for Spirit of Land.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Value to know it's active |

**Script Example:**
```c
sc_start SC_DORAM_SVSP, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_GVG_GIANT

<!-- RAG_CHUNK: SC_GVG_GIANT -->

**Icon (EFST):** `EFST_GVG_GIANT`

**Effect:** Instantly consumes HP/SP, increases Physical/Magic damage on player enemies by n%.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |
| val3 | Increases % Physical damage |
| val4 | Increases % Magical damage |

**Script Example:**
```c
sc_start SC_GVG_GIANT, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_GVG_GOLEM

<!-- RAG_CHUNK: SC_GVG_GOLEM -->

**Icon (EFST):** `EFST_GVG_GOLEM`

**Effect:** Instantly consumes HP/SP, decreases n% damage received from other adventurers.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |
| val3 | Decreases % damage received of physical attack |
| val4 | Decreases % damage received of magical attack |

**Script Example:**
```c
sc_start SC_GVG_GOLEM, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_GVG_STUN

<!-- RAG_CHUNK: SC_GVG_STUN -->

**Icon (EFST):** `EFST_GVG_STUN`

**Effect:** Instantly consumes HP/SP, immunizes you against Stun.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |

**Script Example:**
```c
sc_start SC_GVG_STUN, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_GVG_STONE

<!-- RAG_CHUNK: SC_GVG_STONE -->

**Icon (EFST):** `EFST_GVG_STONE`

**Effect:** Instantly consumes HP/SP, immunizes you against Petrification.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |

**Script Example:**
```c
sc_start SC_GVG_STONE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_GVG_FREEZ

<!-- RAG_CHUNK: SC_GVG_FREEZ -->

**Icon (EFST):** `EFST_GVG_FREEZ`

**Effect:** Instantly consumes HP/SP, immunizes you against Frost.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |

**Script Example:**
```c
sc_start SC_GVG_FREEZ, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_GVG_SLEEP

<!-- RAG_CHUNK: SC_GVG_SLEEP -->

**Icon (EFST):** `EFST_GVG_SLEEP`

**Effect:** Instantly consumes HP/SP, immunizes you against Sleep.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |

**Script Example:**
```c
sc_start SC_GVG_SLEEP, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_GVG_CURSE

<!-- RAG_CHUNK: SC_GVG_CURSE -->

**Icon (EFST):** `EFST_GVG_CURSE`

**Effect:** Instantly consumes HP/SP, immunizes you against Curse.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |

**Script Example:**
```c
sc_start SC_GVG_CURSE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_GVG_SILENCE

<!-- RAG_CHUNK: SC_GVG_SILENCE -->

**Icon (EFST):** `EFST_GVG_SILENCE`

**Effect:** Instantly consumes HP/SP, immunizes you against Silence.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |

**Script Example:**
```c
sc_start SC_GVG_SILENCE, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_GVG_BLIND

<!-- RAG_CHUNK: SC_GVG_BLIND -->

**Icon (EFST):** `EFST_GVG_BLIND`

**Effect:** Instantly consumes HP/SP, immunizes you against Blind.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |

**Script Example:**
```c
sc_start SC_GVG_BLIND, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_EXTREMITYFIST2

<!-- RAG_CHUNK: SC_EXTREMITYFIST2 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_EXTREMITYFIST2, 60000, 1;
```

---

### SC_LHZ_DUN_N1

<!-- RAG_CHUNK: SC_LHZ_DUN_N1 -->

**Icon (EFST):** `EFST_LHZ_DUN_N1`

**Effect:** Increases damage against Swordman, Thief and reduces damage taken from Acolyte, Merchant monsters of Biolab 5 (except MVPs).

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Damage |
| val2 | +% Defense |

**Script Example:**
```c
sc_start SC_LHZ_DUN_N1, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_LHZ_DUN_N2

<!-- RAG_CHUNK: SC_LHZ_DUN_N2 -->

**Icon (EFST):** `EFST_LHZ_DUN_N2`

**Effect:** Increases damage against Acolyte, Merchant and reduces damage taken from Mage, Archer monsters of Biolab 5 (except MVPs).

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Damage |
| val2 | +% Defense |

**Script Example:**
```c
sc_start SC_LHZ_DUN_N2, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_LHZ_DUN_N3

<!-- RAG_CHUNK: SC_LHZ_DUN_N3 -->

**Icon (EFST):** `EFST_LHZ_DUN_N3`

**Effect:** Increases damage against Mage, Archer and reduces damage taken from Swordman, Thief monsters of Biolab 5 (except MVPs).

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Damage |
| val2 | +% Defense |

**Script Example:**
```c
sc_start SC_LHZ_DUN_N3, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_LHZ_DUN_N4

<!-- RAG_CHUNK: SC_LHZ_DUN_N4 -->

**Icon (EFST):** `EFST_LHZ_DUN_N4`

**Effect:** Increases and reduces damage against MVPs of Biolab 5.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Damage |
| val2 | +% Defense |

**Script Example:**
```c
sc_start SC_LHZ_DUN_N4, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_DORAM_BUF_01

<!-- RAG_CHUNK: SC_DORAM_BUF_01 -->

**Effect:** Recovers 10 HP every 10 seconds.

**Script Example:**
```c
sc_start SC_DORAM_BUF_01, 60000, 1;
```

---

### SC_DORAM_BUF_02

<!-- RAG_CHUNK: SC_DORAM_BUF_02 -->

**Effect:** Recovers 5 SP every 10 seconds.

**Script Example:**
```c
sc_start SC_DORAM_BUF_02, 60000, 1;
```

---

### SC_INCREASE_MAXHP

<!-- RAG_CHUNK: SC_INCREASE_MAXHP -->

**Icon (EFST):** `EFST_ATKER_ASPD`

**Effect:** Increases MaxHP. Increases natural HP regeneration.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + HP |
| val2 | +% HP regeneration |

**Script Example:**
```c
sc_start SC_INCREASE_MAXHP, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INCREASE_MAXSP

<!-- RAG_CHUNK: SC_INCREASE_MAXSP -->

**Icon (EFST):** `EFST_ATKER_MOVESPEED`

**Effect:** Increases MaxSP. Increases natural SP regeneration.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + SP |
| val2 | +% SP regeneration |

**Script Example:**
```c
sc_start SC_INCREASE_MAXSP, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_REF_T_POTION

<!-- RAG_CHUNK: SC_REF_T_POTION -->

**Icon (EFST):** `EFST_REF_T_POTION`

**Effect:** Decreases reflected damage by 100%.

**Script Example:**
```c
sc_start SC_REF_T_POTION, 60000, 1;
```

---

### SC_ADD_ATK_DAMAGE

<!-- RAG_CHUNK: SC_ADD_ATK_DAMAGE -->

**Icon (EFST):** `EFST_ADD_ATK_DAMAGE`

**Effect:** Increases melee physical damage by 15%. Increases ranged physical damage by 15%.

**Script Example:**
```c
sc_start SC_ADD_ATK_DAMAGE, 60000, 1;
```

---

### SC_ADD_MATK_DAMAGE

<!-- RAG_CHUNK: SC_ADD_MATK_DAMAGE -->

**Icon (EFST):** `EFST_ADD_MATK_DAMAGE`

**Effect:** Increases all elemental magical damage by 15%.

**Script Example:**
```c
sc_start SC_ADD_MATK_DAMAGE, 60000, 1;
```

---

### SC_HELPANGEL

<!-- RAG_CHUNK: SC_HELPANGEL -->

**Icon (EFST):** `EFST_HELPANGEL`

**Effect:** Recover 1000 HP every second. Recover 350 SP every second.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val4 | Tick time (milliseconds) |

**Script Example:**
```c
sc_start SC_HELPANGEL, 60000, 1;
```

---

### SC_SOUNDOFDESTRUCTION

<!-- RAG_CHUNK: SC_SOUNDOFDESTRUCTION -->

**Icon (EFST):** `EFST_SOUND_OF_DESTRUCTION`

**Effect:** Doubles incoming damage for 10 seconds.

**Script Example:**
```c
sc_start SC_SOUNDOFDESTRUCTION, 60000, 1;
```

---

### SC_LUXANIMA

<!-- RAG_CHUNK: SC_LUXANIMA -->

**Icon (EFST):** `EFST_LUXANIMA`

**Effect:** Physical attacks has the chance to activate Storm Blast Level 1. Increases physical damage against all sizes.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | Storm Blast success 15% (hardcoded) |
| val3 | Damage/HP/SP 30% increase (hardcoded) |

**Script Example:**
```c
sc_start SC_LUXANIMA, 60000, 1;
```

---

### SC_REUSE_LIMIT_LUXANIMA

<!-- RAG_CHUNK: SC_REUSE_LIMIT_LUXANIMA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_REUSE_LIMIT_LUXANIMA, 60000, 1;
```

---

### SC_ENSEMBLEFATIGUE

<!-- RAG_CHUNK: SC_ENSEMBLEFATIGUE -->

**Icon (EFST):** `EFST_ENSEMBLEFATIGUE`

**Effect:** Disables skill use. Movement and attack speed reduced by 30%.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | + 30 Speed and ASPD rates penalty (hardcoded) |

**Script Example:**
```c
sc_start SC_ENSEMBLEFATIGUE, 60000, 1;
```

---

### SC_MISTY_FROST

<!-- RAG_CHUNK: SC_MISTY_FROST -->

**Icon (EFST):** `EFST_MISTY_FROST`

**Effect:** Freezing.

**Script Example:**
```c
sc_start SC_MISTY_FROST, 60000, 1;
```

---

### SC_MAGIC_POISON

<!-- RAG_CHUNK: SC_MAGIC_POISON -->

**Icon (EFST):** `EFST_MAGIC_POISON`

**Effect:** Decreases resistance against all elemental attacks by 50%.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | Attribute Reduction (50, hardcoded). |

**Script Example:**
```c
sc_start SC_MAGIC_POISON, 60000, 1;
```

---

### SC_EP16_2_BUFF_SS

<!-- RAG_CHUNK: SC_EP16_2_BUFF_SS -->

**Icon (EFST):** `EFST_EP16_2_BUFF_SS`

**Effect:** ASPD +10.

**Script Example:**
```c
sc_start SC_EP16_2_BUFF_SS, 60000, 1;
```

---

### SC_EP16_2_BUFF_SC

<!-- RAG_CHUNK: SC_EP16_2_BUFF_SC -->

**Icon (EFST):** `EFST_EP16_2_BUFF_SC`

**Effect:** CRIT +30.

**Script Example:**
```c
sc_start SC_EP16_2_BUFF_SC, 60000, 1;
```

---

### SC_EP16_2_BUFF_AC

<!-- RAG_CHUNK: SC_EP16_2_BUFF_AC -->

**Icon (EFST):** `EFST_EP16_2_BUFF_AC`

**Effect:** Reduce variable cast time by 80%.

**Script Example:**
```c
sc_start SC_EP16_2_BUFF_AC, 60000, 1;
```

---

### SC_EMERGENCY_MOVE

<!-- RAG_CHUNK: SC_EMERGENCY_MOVE -->

**Icon (EFST):** `EFST_INC_AGI`

**Effect:** Increase AGI and walkspeed, AL_INCAGI effect.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val2 | Movement speed +25 (hardcoded) |

**Script Example:**
```c
sc_start SC_EMERGENCY_MOVE, 60000, 1;
```

---

### SC_PACKING_ENVELOPE1

<!-- RAG_CHUNK: SC_PACKING_ENVELOPE1 -->

**Icon (EFST):** `EFST_PACKING_ENVELOPE1`

**Effect:** Increases ATK

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + watk |

**Script Example:**
```c
sc_start SC_PACKING_ENVELOPE1, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PACKING_ENVELOPE2

<!-- RAG_CHUNK: SC_PACKING_ENVELOPE2 -->

**Icon (EFST):** `EFST_PACKING_ENVELOPE2`

**Effect:** Increases MATK

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + ematk |

**Script Example:**
```c
sc_start SC_PACKING_ENVELOPE2, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PACKING_ENVELOPE3

<!-- RAG_CHUNK: SC_PACKING_ENVELOPE3 -->

**Icon (EFST):** `EFST_PACKING_ENVELOPE3`

**Effect:** Increases MaxHP

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% MaxHP |

**Script Example:**
```c
sc_start SC_PACKING_ENVELOPE3, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PACKING_ENVELOPE4

<!-- RAG_CHUNK: SC_PACKING_ENVELOPE4 -->

**Icon (EFST):** `EFST_PACKING_ENVELOPE4`

**Effect:** Increases MaxSP

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% MaxSP |

**Script Example:**
```c
sc_start SC_PACKING_ENVELOPE4, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PACKING_ENVELOPE5

<!-- RAG_CHUNK: SC_PACKING_ENVELOPE5 -->

**Icon (EFST):** `EFST_PACKING_ENVELOPE5`

**Effect:** Increases FLEE

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + Flee |

**Script Example:**
```c
sc_start SC_PACKING_ENVELOPE5, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PACKING_ENVELOPE6

<!-- RAG_CHUNK: SC_PACKING_ENVELOPE6 -->

**Icon (EFST):** `EFST_PACKING_ENVELOPE6`

**Effect:** Increases ASPD

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + ASPD |

**Script Example:**
```c
sc_start SC_PACKING_ENVELOPE6, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PACKING_ENVELOPE7

<!-- RAG_CHUNK: SC_PACKING_ENVELOPE7 -->

**Icon (EFST):** `EFST_PACKING_ENVELOPE7`

**Effect:** Increases DEF

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + DEF |

**Script Example:**
```c
sc_start SC_PACKING_ENVELOPE7, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PACKING_ENVELOPE8

<!-- RAG_CHUNK: SC_PACKING_ENVELOPE8 -->

**Icon (EFST):** `EFST_PACKING_ENVELOPE8`

**Effect:** Increases MDEF

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + MDEF |

**Script Example:**
```c
sc_start SC_PACKING_ENVELOPE8, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PACKING_ENVELOPE9

<!-- RAG_CHUNK: SC_PACKING_ENVELOPE9 -->

**Icon (EFST):** `EFST_PACKING_ENVELOPE9`

**Effect:** Increases Critical rate

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + Critical rate |

**Script Example:**
```c
sc_start SC_PACKING_ENVELOPE9, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_PACKING_ENVELOPE10

<!-- RAG_CHUNK: SC_PACKING_ENVELOPE10 -->

**Icon (EFST):** `EFST_PACKING_ENVELOPE10`

**Effect:** Increase Speed and Flee.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% Walkspeed |
| val2 | +% Flee |

**Script Example:**
```c
sc_start SC_PACKING_ENVELOPE10, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_BATH_FOAM_A

<!-- RAG_CHUNK: SC_BATH_FOAM_A -->

**Icon (EFST):** `EFST_BATH_FOAM_A`

**Effect:** Increases physical and magical damage against Meditathio Dungeon Monsters.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% damage |

**Script Example:**
```c
sc_start SC_BATH_FOAM_A, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_BATH_FOAM_B

<!-- RAG_CHUNK: SC_BATH_FOAM_B -->

**Icon (EFST):** `EFST_BATH_FOAM_B`

**Effect:** Increases physical and magical damage against Meditathio Dungeon Monsters.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% damage |

**Script Example:**
```c
sc_start SC_BATH_FOAM_B, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_BATH_FOAM_C

<!-- RAG_CHUNK: SC_BATH_FOAM_C -->

**Icon (EFST):** `EFST_BATH_FOAM_C`

**Effect:** Increases physical and magical damage against Meditathio Dungeon Monsters.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% damage |

**Script Example:**
```c
sc_start SC_BATH_FOAM_C, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_BUCHEDENOEL

<!-- RAG_CHUNK: SC_BUCHEDENOEL -->

**Icon (EFST):** `EFST_BUCHEDENOEL`

**Effect:** Increases HP & SP restoration by 3%, Hit +3, and Critical +7.

**Script Example:**
```c
sc_start SC_BUCHEDENOEL, 60000, 1;
```

---

### SC_EP16_DEF

<!-- RAG_CHUNK: SC_EP16_DEF -->

**Icon (EFST):** `EFST_EP16_DEF`

**Effect:** Decrease physical and magical damage against monsters in the Room of Consciousness and Prontera Invasion Dungeon. Restores 1000 HP. Cures Curse, Poison and Silence.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% reduction |

**Script Example:**
```c
sc_start SC_EP16_DEF, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_STR_SCROLL

<!-- RAG_CHUNK: SC_STR_SCROLL -->

**Icon (EFST):** `EFST_STR_SCROLL`

**Effect:** Increases STR.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + STR |

**Script Example:**
```c
sc_start SC_STR_SCROLL, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_INT_SCROLL

<!-- RAG_CHUNK: SC_INT_SCROLL -->

**Icon (EFST):** `EFST_INT_SCROLL`

**Effect:** Increases INT.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | + INT |

**Script Example:**
```c
sc_start SC_INT_SCROLL, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CONTENTS_1

<!-- RAG_CHUNK: SC_CONTENTS_1 -->

**Icon (EFST):** `EFST_CONTENTS_1`

**Effect:** Increase physical and magical damage to all element enemies

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% damage |

**Script Example:**
```c
sc_start SC_CONTENTS_1, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CONTENTS_2

<!-- RAG_CHUNK: SC_CONTENTS_2 -->

**Icon (EFST):** `EFST_CONTENTS_2`

**Effect:** Increase melee physical damage, range physical damage, and all elemental magic damage.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% damage |

**Script Example:**
```c
sc_start SC_CONTENTS_2, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CONTENTS_3

<!-- RAG_CHUNK: SC_CONTENTS_3 -->

**Icon (EFST):** `EFST_CONTENTS_3`

**Effect:** Increase ATK and MATK

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% damage |

**Script Example:**
```c
sc_start SC_CONTENTS_3, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CONTENTS_4

<!-- RAG_CHUNK: SC_CONTENTS_4 -->

**Icon (EFST):** `EFST_CONTENTS_4`

**Effect:** Increase ATK and MATK

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% damage |

**Script Example:**
```c
sc_start SC_CONTENTS_4, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CONTENTS_5

<!-- RAG_CHUNK: SC_CONTENTS_5 -->

**Icon (EFST):** `EFST_CONTENTS_5`

**Effect:** Increase ASPD and reduce variable casttime

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% increase ASPD, -% reduce variable casttime |

**Script Example:**
```c
sc_start SC_CONTENTS_5, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CONTENTS_6

<!-- RAG_CHUNK: SC_CONTENTS_6 -->

**Icon (EFST):** `EFST_CONTENTS_6`

**Effect:** Increase physical and magical damage to Dragon and Plant race.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% damage |

**Script Example:**
```c
sc_start SC_CONTENTS_6, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CONTENTS_7

<!-- RAG_CHUNK: SC_CONTENTS_7 -->

**Icon (EFST):** `EFST_CONTENTS_7`

**Effect:** Increase physical and magical damage to Demon and Undead race.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% damage |

**Script Example:**
```c
sc_start SC_CONTENTS_7, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CONTENTS_8

<!-- RAG_CHUNK: SC_CONTENTS_8 -->

**Icon (EFST):** `EFST_CONTENTS_8`

**Effect:** Increase physical and magical damage to Formless and Fish race.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% damage |

**Script Example:**
```c
sc_start SC_CONTENTS_8, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CONTENTS_9

<!-- RAG_CHUNK: SC_CONTENTS_9 -->

**Icon (EFST):** `EFST_CONTENTS_9`

**Effect:** Increase physical and magical damage to Angel and Brute race.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% damage |

**Script Example:**
```c
sc_start SC_CONTENTS_9, 60000, 10;  // Duration 60s, val1=10
```

---

### SC_CONTENTS_10

<!-- RAG_CHUNK: SC_CONTENTS_10 -->

**Icon (EFST):** `EFST_CONTENTS10`

**Effect:** Increase physical and magical damage to Insect and Demihuman race.

**Parameters:**

| Parameter | Usage |
|-----------|-------|
| val1 | +% damage |

**Script Example:**
```c
sc_start SC_CONTENTS_10, 60000, 10;  // Duration 60s, val1=10
```

---


# ═══════════════════════════════════════════════════════════════
# COMPLETE SC_* CONSTANT LIST (1038 entries from source)
# ═══════════════════════════════════════════════════════════════
<!-- RAG_CHUNK: complete_sc_list -->

## All SC_* Constants (Source: src/map/status.hpp)

```
SC_2011RWC_SCROLL
SC_ABR_BATTLE_WARIOR
SC_ABR_DUAL_CANNON
SC_ABR_INFINITY
SC_ABR_MOTHER_NET
SC_ABUNDANCE
SC_ABYSSFORCEWEAPON
SC_ABYSS_DAGGER
SC_ABYSS_SLAYER
SC_ACARAJE
SC_ACCELERATION
SC_ACTIVE_MONSTER_TRANSFORM
SC_ADAPTATION
SC_ADD_ATK_DAMAGE
SC_ADD_MATK_DAMAGE
SC_ADJUSTMENT
SC_ADORAMUS
SC_ADRENALINE
SC_ADRENALINE2
SC_AETERNA
SC_AGIFOOD
SC_AGIUP
SC_AIN_RHAPSODY
SC_AKAITSUKI
SC_ALL
SC_ALL_GLASTHEIM_RECALL
SC_ALL_LIGHTHALZEN_RECALL
SC_ALL_NIFLHEIM_RECALL
SC_ALL_PRONTERA_RECALL
SC_ALL_RIDING
SC_ALL_RIDING_REUSE_LIMIT
SC_ALL_STAT_DOWN
SC_ALL_THANATOS_RECALL
SC_ALMIGHTY
SC_ANALYZE
SC_ANCILLA
SC_ANGELUS
SC_ANGEL_PROTECT
SC_ANGRIFFS_MODUS
SC_ANKLE
SC_ANTI_M_BLAST
SC_APPLEIDUN
SC_AQUAPLAY
SC_AQUAPLAY_OPTION
SC_ARCLOUSEDASH
SC_ARCWANDCLAN
SC_ARMOR
SC_ARMORCHANGE
SC_ARMOR_ELEMENT_EARTH
SC_ARMOR_ELEMENT_FIRE
SC_ARMOR_ELEMENT_WATER
SC_ARMOR_ELEMENT_WIND
SC_ARMOR_RESIST
SC_ASH
SC_ASPDPOTION0
SC_ASPDPOTION1
SC_ASPDPOTION2
SC_ASPDPOTION3
SC_ASPERSIO
SC_ASSNCROS
SC_ASSUMPTIO
SC_ATKPOTION
SC_ATTACK_STANCE
SC_ATTHASTE_CASH
SC_AURABLADE
SC_AUTOBERSERK
SC_AUTOCOUNTER
SC_AUTOGUARD
SC_AUTOSPELL
SC_AUTOTRADE
SC_AUTO_FIRING_LAUNCHER
SC_AVOID
SC_AXE_STOMP
SC_A_MACHINE
SC_A_TELUM
SC_A_VITA
SC_BANANA_BOMB
SC_BANANA_BOMB_SITDOWN
SC_BANDING
SC_BANDING_DEFENCE
SC_BARRIER
SC_BASILICA
SC_BASILICA_CELL
SC_BATH_FOAM_A
SC_BATH_FOAM_B
SC_BATH_FOAM_C
SC_BATKFOOD
SC_BATTLEORDERS
SC_BEEF_RIB_STEW
SC_BENEDICTIO
SC_BENEDICTUM
SC_BERSERK
SC_BEYONDOFWARCRY
SC_BIONIC_CREEPER
SC_BIONIC_HELLTREE
SC_BIONIC_WOODENWARRIOR
SC_BIONIC_WOODEN_FAIRY
SC_BITE
SC_BITESCAR
SC_BLADESTOP
SC_BLADESTOP_WAIT
SC_BLAST
SC_BLAST_OPTION
SC_BLEEDING
SC_BLESSING
SC_BLESSING_OF_M_CREATURES
SC_BLESSING_OF_M_C_DEBUFF
SC_BLIND
SC_BLOODLUST
SC_BLOODSUCKER
SC_BOOST500
SC_BOSSMAPINFO
SC_BO_HELL_DUSTY
SC_BREAKINGLIMIT
SC_BROKENARMOR
SC_BROKENWEAPON
SC_BUCHEDENOEL
SC_BUNSINJYUTSU
SC_BURNING
SC_BURNT
SC_B_TRAP
SC_CALAMITYGALE
SC_CAMOUFLAGE
SC_CARTBOOST
SC_CATNIPPOWDER
SC_CBC
SC_CHANGE
SC_CHANGEUNDEAD
SC_CHARGINGPIERCE
SC_CHARGINGPIERCE_COUNT
SC_CHASEWALK
SC_CHASEWALK2
SC_CHASING
SC_CHATTERING
SC_CHEERUP
SC_CHILL
SC_CHILLY_AIR
SC_CHILLY_AIR_OPTION
SC_CIRCLE_OF_FIRE
SC_CIRCLE_OF_FIRE_OPTION
SC_CLAN_INFO
SC_CLIMAX
SC_CLIMAX_BLOOM
SC_CLIMAX_CRYIMP
SC_CLIMAX_DES_HU
SC_CLIMAX_EARTH
SC_CLOAKING
SC_CLOAKINGEXCEED
SC_CLOSECONFINE
SC_CLOSECONFINE2
SC_CLOUD_KILL
SC_CLOUD_POISON
SC_COCKTAIL_WARG_BLOOD
SC_COLD_FORCE
SC_COLD_FORCE_OPTION
SC_COLORS_OF_HYUN_ROK_1
SC_COLORS_OF_HYUN_ROK_2
SC_COLORS_OF_HYUN_ROK_3
SC_COLORS_OF_HYUN_ROK_4
SC_COLORS_OF_HYUN_ROK_5
SC_COLORS_OF_HYUN_ROK_6
SC_COLORS_OF_HYUN_ROK_BUFF
SC_COMA
SC_COMBAT_PILL
SC_COMBAT_PILL2
SC_COMBO
SC_COMMONSC_RESIST
SC_COMMON_MAX
SC_COMMON_MIN
SC_COMPETENTIA
SC_CONCENTRATE
SC_CONCENTRATION
SC_CONFUSION
SC_CONTENTS_1
SC_CONTENTS_10
SC_CONTENTS_15
SC_CONTENTS_16
SC_CONTENTS_17
SC_CONTENTS_18
SC_CONTENTS_19
SC_CONTENTS_2
SC_CONTENTS_20
SC_CONTENTS_26
SC_CONTENTS_27
SC_CONTENTS_28
SC_CONTENTS_29
SC_CONTENTS_3
SC_CONTENTS_31
SC_CONTENTS_32
SC_CONTENTS_33
SC_CONTENTS_34
SC_CONTENTS_35
SC_CONTENTS_4
SC_CONTENTS_5
SC_CONTENTS_6
SC_CONTENTS_7
SC_CONTENTS_8
SC_CONTENTS_9
SC_COOLER
SC_COOLER_OPTION
SC_CP_ARMOR
SC_CP_HELM
SC_CP_SHIELD
SC_CP_WEAPON
SC_CREATINGSTAR
SC_CRESCENTELBOW
SC_CRESCIVEBOLT
SC_CRIFOOD
SC_CRITICALWOUND
SC_CROSSBOWCLAN
SC_CRUSHSTRIKE
SC_CRYSTALIZE
SC_CRYSTAL_ARMOR
SC_CRYSTAL_ARMOR_OPTION
SC_CUP_OF_BOZA
SC_CURSE
SC_CURSEDCIRCLE_ATKER
SC_CURSEDCIRCLE_TARGET
SC_CURSED_SOIL
SC_CURSED_SOIL_OPTION
SC_C_BUFF_3
SC_C_BUFF_4
SC_C_BUFF_5
SC_C_BUFF_6
SC_C_MARKER
SC_DAILYSENDMAILCNT
SC_DAMAGE_HEAL
SC_DANCEWITHWUG
SC_DANCING
SC_DANCING_KNIFE
SC_DARKCROW
SC_DAWN_MOON
SC_DEADLY_DEFEASANCE
SC_DEATHBOUND
SC_DEATHHURT
SC_DECORATION_OF_MUSIC
SC_DECREASEAGI
SC_DEEPSLEEP
SC_DEEP_POISONING
SC_DEEP_POISONING_OPTION
SC_DEFENCE
SC_DEFENDER
SC_DEFRATIOATK
SC_DEFSET
SC_DEF_RATE
SC_DELUGE
SC_DEVOTION
SC_DEXFOOD
SC_DIMENSION
SC_DIMENSION1
SC_DIMENSION2
SC_DODGE
SC_DONTFORGETME
SC_DORAM_BUF_01
SC_DORAM_BUF_02
SC_DORAM_FLEE2
SC_DORAM_MATK
SC_DORAM_SVSP
SC_DORAM_WALKSPEED
SC_DOUBLECAST
SC_DPOISON
SC_DRAGONIC_AURA
SC_DRESSUP
SC_DROCERA_HERB_STEAMED
SC_DRUMBATTLE
SC_DUPLELIGHT
SC_D_MACHINE
SC_EARTHDRIVE
SC_EARTHSCROLL
SC_EARTHSHAKER
SC_EARTHWEAPON
SC_EARTH_CARE
SC_EARTH_CARE_OPTION
SC_EARTH_INSIGNIA
SC_ECHOSONG
SC_ECLAGE_RECALL
SC_EDP
SC_ELECTRICSHOCKER
SC_ELEMENTALCHANGE
SC_ELEMENTAL_VEIL
SC_EMERGENCY_MOVE
SC_ENCHANTARMS
SC_ENCHANTBLADE
SC_ENCPOISON
SC_ENDURE
SC_ENERGYCOAT
SC_ENERGY_DRINK_RESERCH
SC_ENSEMBLEFATIGUE
SC_ENTRY_QUEUE_APPLY_DELAY
SC_ENTRY_QUEUE_NOTIFY_ADMISSION_TIME_OUT
SC_EP16_2_BUFF_AC
SC_EP16_2_BUFF_SC
SC_EP16_2_BUFF_SS
SC_EP16_DEF
SC_EPICLESIS
SC_EQC
SC_ETERNALCHAOS
SC_EXEEDBREAK
SC_EXPBOOST
SC_EXPIATIO
SC_EXPLOSIONSPIRITS
SC_EXTRACT_SALAMINE_JUICE
SC_EXTRACT_WHITE_POTION_Z
SC_EXTREMITYFIST
SC_EXTREMITYFIST2
SC_EYES_OF_STORM
SC_EYES_OF_STORM_OPTION
SC_E_CHAIN
SC_E_SLASH_COUNT
SC_FALLEN_ANGEL
SC_FALLINGSTAR
SC_FASTCAST
SC_FEAR
SC_FEARBREEZE
SC_FIGHTINGSPIRIT
SC_FIREWEAPON
SC_FIRE_CLOAK
SC_FIRE_CLOAK_OPTION
SC_FIRE_INSIGNIA
SC_FIRM_FAITH
SC_FIRST_BRAND
SC_FIRST_FAITH_POWER
SC_FLAMEARMOR
SC_FLAMEARMOR_OPTION
SC_FLAMETECHNIC
SC_FLAMETECHNIC_OPTION
SC_FLASHCOMBO
SC_FLASHKICK
SC_FLEEFOOD
SC_FLEET
SC_FLING
SC_FLOWERSMOKE
SC_FOGWALL
SC_FOOD_AGI_CASH
SC_FOOD_DEX_CASH
SC_FOOD_INT_CASH
SC_FOOD_LUK_CASH
SC_FOOD_STR_CASH
SC_FOOD_VIT_CASH
SC_FORCEOFVANGUARD
SC_FORTUNE
SC_FREEZE
SC_FREEZE_SP
SC_FREEZING
SC_FRESHSHRIMP
SC_FRIGG_SONG
SC_FSTONE
SC_FULL_SWING_K
SC_FULL_THROTTLE
SC_FURY
SC_FUSION
SC_GATLINGFEVER
SC_GEFFEN_MAGIC1
SC_GEFFEN_MAGIC2
SC_GEFFEN_MAGIC3
SC_GEF_NOCTURN
SC_GENSOU
SC_GHOSTWEAPON
SC_GIANTGROWTH
SC_GLASTHEIM_ATK
SC_GLASTHEIM_DEF
SC_GLASTHEIM_HEAL
SC_GLASTHEIM_HIDDEN
SC_GLASTHEIM_HPSP
SC_GLASTHEIM_ITEMDEF
SC_GLASTHEIM_STATE
SC_GLOOMYDAY
SC_GLOOMYDAY_SK
SC_GLORIA
SC_GLORYWOUNDS
SC_GN_CARTBOOST
SC_GOLDENE_FERSE
SC_GOLDENE_TONE
SC_GOLDENMACECLAN
SC_GOSPEL
SC_GRACE_BREEZE
SC_GRACE_BREEZE_OPTION
SC_GRADUAL_GRAVITY
SC_GRANITIC_ARMOR
SC_GRAVITATION
SC_GRAVITYCONTROL
SC_GRENADE_FRAGMENT_1
SC_GRENADE_FRAGMENT_2
SC_GRENADE_FRAGMENT_3
SC_GRENADE_FRAGMENT_4
SC_GRENADE_FRAGMENT_5
SC_GRENADE_FRAGMENT_6
SC_GROOMING
SC_GROUNDGRAVITY
SC_GT_CHANGE
SC_GT_ENERGYGAIN
SC_GT_REVITALIZE
SC_GUARDIAN_RECALL
SC_GUARDIAN_S
SC_GUARD_STANCE
SC_GUILDAURA
SC_GUST
SC_GUST_OPTION
SC_GVG_BLIND
SC_GVG_CURSE
SC_GVG_FREEZ
SC_GVG_GIANT
SC_GVG_GOLEM
SC_GVG_SILENCE
SC_GVG_SLEEP
SC_GVG_STONE
SC_GVG_STUN
SC_G_LIFEPOTION
SC_HALLUCINATION
SC_HALLUCINATIONWALK
SC_HALLUCINATIONWALK_POSTDELAY
SC_HANBOK
SC_HANDICAPSTATE_CONFLAGRATION
SC_HANDICAPSTATE_CRYSTALLIZATION
SC_HANDICAPSTATE_DEADLYPOISON
SC_HANDICAPSTATE_DEEPBLIND
SC_HANDICAPSTATE_DEEPSILENCE
SC_HANDICAPSTATE_DEPRESSION
SC_HANDICAPSTATE_FROSTBITE
SC_HANDICAPSTATE_HOLYFLAME
SC_HANDICAPSTATE_LASSITUDE
SC_HANDICAPSTATE_LIGHTNINGSTRIKE
SC_HANDICAPSTATE_MISFORTUNE
SC_HANDICAPSTATE_SWOONING
SC_HAPPINESS_STAR
SC_HARMONIZE
SC_HAT_EFFECT
SC_HAWKEYES
SC_HEATER
SC_HEATER_OPTION
SC_HEAT_BARREL
SC_HEAVEN_AND_EARTH
SC_HELLPOWER
SC_HELLS_PLANT
SC_HELPANGEL
SC_HERMODE
SC_HIDDEN_CARD
SC_HIDING
SC_HISS
SC_HITFOOD
SC_HNNOWEAPON
SC_HOGOGONG
SC_HOLY_OIL
SC_HOLY_S
SC_HOMUN_TIME
SC_HOVERING
SC_HPDRAIN
SC_HPREGEN
SC_HUMMING
SC_H_MINE
SC_IGNOREDEF
SC_ILLUSIONDOPING
SC_IMMUNE_PROPERTY_DARKNESS
SC_IMMUNE_PROPERTY_FIRE
SC_IMMUNE_PROPERTY_GROUND
SC_IMMUNE_PROPERTY_NOTHING
SC_IMMUNE_PROPERTY_POISON
SC_IMMUNE_PROPERTY_SAINT
SC_IMMUNE_PROPERTY_TELEKINESIS
SC_IMMUNE_PROPERTY_UNDEAD
SC_IMMUNE_PROPERTY_WATER
SC_IMMUNE_PROPERTY_WIND
SC_IMPOSITIO
SC_INCAGI
SC_INCALLSTATUS
SC_INCASPDRATE
SC_INCATKRATE
SC_INCBASEATK
SC_INCCRI
SC_INCDEF
SC_INCDEFRATE
SC_INCDEX
SC_INCFLEE
SC_INCFLEE2
SC_INCFLEERATE
SC_INCHEALRATE
SC_INCHIT
SC_INCHITRATE
SC_INCINT
SC_INCLUK
SC_INCMATKRATE
SC_INCMHP
SC_INCMHPRATE
SC_INCMSP
SC_INCMSPRATE
SC_INCREASEAGI
SC_INCREASE_MAXHP
SC_INCREASE_MAXSP
SC_INCREASING
SC_INCSTR
SC_INCVIT
SC_INFINITY_DRINK
SC_INFRAREDSCAN
SC_INSPIRATION
SC_INTENSIVE_AIM
SC_INTENSIVE_AIM_COUNT
SC_INTFOOD
SC_INTOABYSS
SC_INTRAVISION
SC_INT_SCROLL
SC_INVINCIBLE
SC_INVINCIBLEOFF
SC_ITEMBOOST
SC_ITEMSCRIPT
SC_IZAYOI
SC_JAILED
SC_JAWAII_SERENADE
SC_JEXPBOOST
SC_JOINTBEAT
SC_JP_EVENT04
SC_JUMPINGCLAN
SC_JYUMONJIKIRI
SC_KAAHI
SC_KAENSIN
SC_KAGEHUMI
SC_KAGEMUSYA
SC_KAITE
SC_KAIZEL
SC_KAUPE
SC_KEEPING
SC_KILLING_AURA
SC_KINGS_GRACE
SC_KI_SUL_RAMPAGE
SC_KNOWLEDGE
SC_KSPROTECTED
SC_KVASIR_SONATA
SC_KYOMU
SC_KYOUGAKU
SC_KYRIE
SC_LAUDAAGNUS
SC_LAUDARAMUS
SC_LEADERSHIP
SC_LEECHESEND
SC_LERADSDEW
SC_LHZ_DUN_N1
SC_LHZ_DUN_N2
SC_LHZ_DUN_N3
SC_LHZ_DUN_N4
SC_LIFEINSURANCE
SC_LIFE_FORCE_F
SC_LIGHTNINGWALK
SC_LIGHTOFMOON
SC_LIGHTOFSTAR
SC_LIGHTOFSUN
SC_LIGHT_OF_REGENE
SC_LIMIT_POWER_BOOSTER
SC_LJOSALFAR
SC_LONGING
SC_LOUD
SC_LUKFOOD
SC_LUNARSTANCE
SC_LUXANIMA
SC_L_LIFEPOTION
SC_MADNESSCANCEL
SC_MADOGEAR
SC_MAGICALATTACK
SC_MAGICALBULLET
SC_MAGICAL_FEATHER
SC_MAGICCANDY
SC_MAGICMIRROR
SC_MAGICMUSHROOM
SC_MAGICPOWER
SC_MAGICROD
SC_MAGIC_POISON
SC_MAGMA_FLOW
SC_MAGNETICFIELD
SC_MAGNIFICAT
SC_MANA_PLUS
SC_MANDRAGORA
SC_MANU_ATK
SC_MANU_DEF
SC_MANU_MATK
SC_MAPLE_FALLS
SC_MARINE_FESTIVAL
SC_MARIONETTE
SC_MARIONETTE2
SC_MARSHOFABYSS
SC_MASSIVE_F_BLASTER
SC_MATKFOOD
SC_MATKPOTION
SC_MAX
SC_MAXIMIZEPOWER
SC_MAXOVERTHRUST
SC_MAXPAIN
SC_MAXSPELLBOOK
SC_MDEFSET
SC_MDEF_RATE
SC_MEDIALE
SC_MEIKYOUSISUI
SC_MELODYOFSINK
SC_MELON_BOMB
SC_MELTDOWN
SC_MEMORIZE
SC_MENTAL_POTION
SC_MERC_ATKUP
SC_MERC_FLEEUP
SC_MERC_HITUP
SC_MERC_HPUP
SC_MERC_QUICKEN
SC_MERC_SPUP
SC_MERMAID_LONGING
SC_MIDNIGHT_MOON
SC_MILLENNIUMSHIELD
SC_MINDBREAKER
SC_MINOR_BBQ
SC_MIRACLE
SC_MISTYFROST
SC_MISTY_FROST
SC_MODECHANGE
SC_MONSTER_TRANSFORM
SC_MOONLITSERENADE
SC_MOONSTAR
SC_MOON_COMFORT
SC_MTF_ASPD
SC_MTF_ASPD2
SC_MTF_CRIDAMAGE
SC_MTF_HITFLEE
SC_MTF_MATK
SC_MTF_MATK2
SC_MTF_MHP
SC_MTF_MLEATKED
SC_MTF_MSP
SC_MTF_PUMPKIN
SC_MTF_RANGEATK
SC_MTF_RANGEATK2
SC_MUSICAL_INTERLUDE
SC_MUSTLE_M
SC_MYSTERIOUS_POWDER
SC_MYSTERY_POWDER
SC_MYSTICPOWDER
SC_MYSTIC_SYMPHONY
SC_M_DEFSCROLL
SC_M_LIFEPOTION
SC_NEN
SC_NETHERWORLD
SC_NEUTRALBARRIER
SC_NEUTRALBARRIER_MASTER
SC_NEWMOON
SC_NIBELUNGEN
SC_NIGHTMARE
SC_NOACTION
SC_NOCHAT
SC_NONE
SC_NOON_SUN
SC_NORECOVER_STATE
SC_NOVAEXPLOSING
SC_NPC_HALLUCINATIONWALK
SC_NYANGGRASS
SC_OBLIVIONCURSE
SC_ODINS_POWER
SC_OFFERTORIUM
SC_OKTOBERFEST
SC_ONEHAND
SC_ORATIO
SC_ORCISH
SC_OVERBRANDREADY
SC_OVERCOMING_CRISIS
SC_OVERED_BOOST
SC_OVERHEAT
SC_OVERHEAT_LIMITPOINT
SC_OVERTHRUST
SC_PACKING_ENVELOPE1
SC_PACKING_ENVELOPE10
SC_PACKING_ENVELOPE2
SC_PACKING_ENVELOPE3
SC_PACKING_ENVELOPE4
SC_PACKING_ENVELOPE5
SC_PACKING_ENVELOPE6
SC_PACKING_ENVELOPE7
SC_PACKING_ENVELOPE8
SC_PACKING_ENVELOPE9
SC_PAIN_KILLER
SC_PARALYSE
SC_PARALYSIS
SC_PARRYING
SC_PARTYFLEE
SC_PERIOD_PLUSEXP_2ND
SC_PERIOD_RECEIVEITEM_2ND
SC_PETROLOGY
SC_PETROLOGY_OPTION
SC_PNEUMA
SC_POEMBRAGI
SC_POISON
SC_POISONINGWEAPON
SC_POISONREACT
SC_POISON_MIST
SC_POISON_SHIELD
SC_POISON_SHIELD_OPTION
SC_POPECOOKIE
SC_PORK_RIB_STEW
SC_POTENT_VENOM
SC_POWERFUL_FAITH
SC_POWERUP
SC_POWER_OF_GAIA
SC_PRESERVE
SC_PRESTIGE
SC_PRE_ACIES
SC_PROMOTE_HEALTH_RESERCH
SC_PRON_MARCH
SC_PROPERTYWALK
SC_PROTECTEXP
SC_PROTECTION
SC_PROTECTSHADOWEQUIP
SC_PROVIDENCE
SC_PROVOKE
SC_PUSH_CART
SC_PUTTI_TAILS_NOODLES
SC_PYREXIA
SC_PYROCLASTIC
SC_PYROTECHNIC
SC_PYROTECHNIC_OPTION
SC_P_ALTER
SC_QD_SHOT_READY
SC_QUAGMIRE
SC_QUEST_BUFF1
SC_QUEST_BUFF2
SC_QUEST_BUFF3
SC_RAID
SC_RAISINGDRAGON
SC_READING_SB
SC_READYCOUNTER
SC_READYDOWN
SC_READYSTORM
SC_READYTURN
SC_REBIRTH
SC_REBOUND
SC_REBOUND_S
SC_RECOGNIZEDSPELL
SC_REFLECTDAMAGE
SC_REFLECTSHIELD
SC_REFRESH
SC_REF_T_POTION
SC_REGENERATION
SC_REJECTSWORD
SC_RELIEVE_OFF
SC_RELIEVE_ON
SC_RELIGIO
SC_RENOVATIO
SC_RESEARCHREPORT
SC_RETURN_TO_ELDICASTES
SC_REUSE_CRUSHSTRIKE
SC_REUSE_LIMIT_A
SC_REUSE_LIMIT_ASPD_POTION
SC_REUSE_LIMIT_B
SC_REUSE_LIMIT_C
SC_REUSE_LIMIT_D
SC_REUSE_LIMIT_E
SC_REUSE_LIMIT_ECL
SC_REUSE_LIMIT_F
SC_REUSE_LIMIT_G
SC_REUSE_LIMIT_H
SC_REUSE_LIMIT_LUXANIMA
SC_REUSE_LIMIT_MTF
SC_REUSE_LIMIT_RECALL
SC_REUSE_MILLENNIUMSHIELD
SC_REUSE_REFRESH
SC_REUSE_STORMBLAST
SC_RICHMANKIM
SC_RISING_MOON
SC_RISING_SUN
SC_ROCK_CRUSHER
SC_ROCK_CRUSHER_ATK
SC_ROKISWEIL
SC_ROLLINGCUTTER
SC_ROSEBLOSSOM
SC_RULEBREAK
SC_RUN
SC_RUSHWINDMILL
SC_RUSH_QUAKE1
SC_RUSH_QUAKE2
SC_RUWACH
SC_SACRIFICE
SC_SAFETYWALL
SC_SANDY_FESTIVAL
SC_SATURDAYNIGHTFEVER
SC_SAVAGE_STEAK
SC_SBUNSHIN
SC_SCRESIST
SC_SECOND_BRAND
SC_SECOND_JUDGE
SC_SECRAMENT
SC_SERVANTWEAPON
SC_SERVANT_SIGN
SC_SERVICE4U
SC_SEVENWIND
SC_SHADOWWEAPON
SC_SHADOW_CLOCK
SC_SHADOW_EXCEED
SC_SHADOW_SCAR
SC_SHADOW_STRIP
SC_SHADOW_WEAPON
SC_SHAPESHIFT
SC_SHIELDCHAINRUSH
SC_SHIELDSPELL_ATK
SC_SHIELDSPELL_HP
SC_SHIELDSPELL_SP
SC_SHIELD_POWER
SC_SHINKIROU_CALL
SC_SHRIMP
SC_SHRIMPBLESSING
SC_SHRINK
SC_SIEGFRIED
SC_SIGHT
SC_SIGHTBLASTER
SC_SIGHTTRASHER
SC_SIGNUMCRUCIS
SC_SILENCE
SC_SINCERE_FAITH
SC_SIRCLEOFNATURE
SC_SIROMA_ICE_TEA
SC_SITDOWN_FORCE
SC_SKA
SC_SKE
SC_SKF_ASPD
SC_SKF_ATK
SC_SKF_CAST
SC_SKF_MATK
SC_SKILLATKBONUS
SC_SKILLCASTRATE
SC_SKILLRATE_UP
SC_SKY_ENCHANT
SC_SLEEP
SC_SLOWCAST
SC_SLOWDOWN
SC_SLOWPOISON
SC_SMA
SC_SMOKEPOWDER
SC_SOLID_SKIN
SC_SOLID_SKIN_OPTION
SC_SONGOFMANA
SC_SOULATTACK
SC_SOULCOLD
SC_SOULCOLLECT
SC_SOULCURSE
SC_SOULDIVISION
SC_SOULENERGY
SC_SOULFAIRY
SC_SOULFALCON
SC_SOULGOLEM
SC_SOULREAPER
SC_SOULSHADOW
SC_SOULUNITY
SC_SOUNDBLEND
SC_SOUNDOFDESTRUCTION
SC_SPARKCANDY
SC_SPCOST_RATE
SC_SPEARQUICKEN
SC_SPEAR_SCAR
SC_SPEED
SC_SPEEDUP0
SC_SPEEDUP1
SC_SPELLBOOK1
SC_SPELLBOOK2
SC_SPELLBOOK3
SC_SPELLBOOK4
SC_SPELLBOOK5
SC_SPELLBOOK6
SC_SPELLBOOK7
SC_SPELLBREAKER
SC_SPELLFIST
SC_SPELL_ENCHANTING
SC_SPHERE_1
SC_SPHERE_2
SC_SPHERE_3
SC_SPHERE_4
SC_SPHERE_5
SC_SPIDERWEB
SC_SPIRIT
SC_SPLASHER
SC_SPL_ATK
SC_SPL_DEF
SC_SPL_MATK
SC_SPORE_EXPLOSION
SC_SPREGEN
SC_SPRITEMABLE
SC_SPURT
SC_SP_SHA
SC_STARSTANCE
SC_STAR_BURST
SC_STAR_COMFORT
SC_STASIS
SC_STEALTHFIELD
SC_STEALTHFIELD_MASTER
SC_STEELBODY
SC_STOMACHACHE
SC_STONE
SC_STONEHARDSKIN
SC_STONEWAIT
SC_STONE_SHIELD
SC_STONE_SHIELD_OPTION
SC_STONE_WALL
SC_STOP
SC_STORMBLAST
SC_STRANGELIGHTS
SC_STRFOOD
SC_STRIKING
SC_STRIPARMOR
SC_STRIPHELM
SC_STRIPSHIELD
SC_STRIPWEAPON
SC_STRONG_PROTECTION
SC_STRONG_PROTECTION_OPTION
SC_STR_SCROLL
SC_STUN
SC_STYLE_CHANGE
SC_SUB_WEAPONPROPERTY
SC_SUFFRAGIUM
SC_SUHIDE
SC_SUITON
SC_SUMMER
SC_SUMMON_ELEMENTAL_ARDOR
SC_SUMMON_ELEMENTAL_DILUVIO
SC_SUMMON_ELEMENTAL_PROCELLA
SC_SUMMON_ELEMENTAL_SERPENS
SC_SUMMON_ELEMENTAL_TERREMOTUS
SC_SUNSET_SUN
SC_SUNSTANCE
SC_SUN_COMFORT
SC_SUPER_STAR
SC_SU_STOOP
SC_SV_ROOTTWIST
SC_SWINGDANCE
SC_SWOO
SC_SWORDCLAN
SC_SYMPHONYOFLOVER
SC_S_LIFEPOTION
SC_S_MANAPOTION
SC_TALISMAN_OF_FIVE_ELEMENTS
SC_TALISMAN_OF_MAGICIAN
SC_TALISMAN_OF_PROTECTION
SC_TALISMAN_OF_WARRIOR
SC_TAROTCARD
SC_TATAMIGAESHI
SC_TEARGAS
SC_TEARGAS_SOB
SC_TELEKINESIS_INTENSE
SC_TEMPERING
SC_TEMPORARY_COMMUNION
SC_TENSIONRELAX
SC_THIRD_EXOR_FLAME
SC_THORNSTRAP
SC_TIDAL_WEAPON
SC_TIDAL_WEAPON_OPTION
SC_TIME_ACCESSORY
SC_TINDER_BREAKER
SC_TINDER_BREAKER2
SC_TOTEM_OF_TUTELARY
SC_TOXIN
SC_TOXIN_OF_MANDARA
SC_TRICKDEAD
SC_TROPIC
SC_TROPIC_OPTION
SC_TRUESIGHT
SC_TUNAPARTY
SC_TWOHANDQUICKEN
SC_T_FIFTH_GOD
SC_T_FIRST_GOD
SC_T_FOURTH_GOD
SC_T_SECOND_GOD
SC_T_THIRD_GOD
SC_ULTIMATECOOK
SC_ULTIMATE_S
SC_UNIVERSESTANCE
SC_UNLIMIT
SC_UNLIMITEDHUMMINGVOICE
SC_UPHEAVAL
SC_UPHEAVAL_OPTION
SC_USE_SKILL_SP_SHA
SC_USE_SKILL_SP_SPA
SC_UTSUSEMI
SC_VACUUM_EXTREME
SC_VACUUM_EXTREME_POSTDELAY
SC_VENOMBLEED
SC_VENOMIMPRESS
SC_VIGOR
SC_VIOLENTGALE
SC_VITALITYACTIVATION
SC_VITALIZE_POTION
SC_VITATA_500
SC_VITFOOD
SC_VOICEOFSIREN
SC_VOLCANO
SC_WALKSPEED
SC_WARM
SC_WARMER
SC_WATERWEAPON
SC_WATER_BARRIER
SC_WATER_DROP
SC_WATER_DROP_OPTION
SC_WATER_INSIGNIA
SC_WATER_SCREEN
SC_WATER_SCREEN_OPTION
SC_WATKFOOD
SC_WATK_ELEMENT
SC_WEAPONBLOCKING
SC_WEAPONBLOCK_ON
SC_WEAPONBREAKER
SC_WEAPONPERFECTION
SC_WEDDING
SC_WEIGHT50
SC_WEIGHT90
SC_WHISTLE
SC_WHITEIMPRISON
SC_WIDEWEB
SC_WILD_STORM
SC_WILD_STORM_OPTION
SC_WILD_WALK
SC_WINDSIGN
SC_WINDWALK
SC_WINDWEAPON
SC_WIND_CURTAIN
SC_WIND_CURTAIN_OPTION
SC_WIND_INSIGNIA
SC_WIND_STEP
SC_WIND_STEP_OPTION
SC_WINKCHARM
SC_WUGDASH
SC_XMAS
SC_ZANGETSU
SC_ZENKAI
SC_ZEPHYR
SC__AUTOSHADOWSPELL
SC__BLOODYLUST
SC__BODYPAINT
SC__CHAOS
SC__DEADLYINFECT
SC__ENERVATION
SC__FEINTBOMB
SC__GROOMY
SC__IGNORANCE
SC__INVISIBILITY
SC__LAZINESS
SC__MANHOLE
SC__REPRODUCE
SC__SHADOWFORM
SC__STRIPACCESSORY
SC__UNLUCKY
SC__WEAKNESS
```

# ═══════════════════════════════════════════════════════════════
# PART 2: ITEM BONUSES (263 bonuses)
# ═══════════════════════════════════════════════════════════════


**Version:** 5.0 Enhanced
**Generated:** 2025-11-26
**Source:** doc/item_bonus.txt
**Total Bonuses:** 263

---

## Quick Navigation

- [Constants Reference](#constants-reference) - eff, e, r, c, s, bf, atf
- [Basic Bonuses](#1-basic-bonuses) - Stats, HP/SP, ATK/DEF
- [Extended Bonuses](#2-extended-bonuses) - Regen, Cast time
- [Group-Specific Bonuses](#3-group-specific-bonuses) - Race, Element, Size
- [Status-Related Bonuses](#4-status-related-bonuses) - AddEff, Coma
- [AutoSpell Bonuses](#5-autospell-bonuses) - Auto-cast skills
- [Misc Bonuses](#6-misc-bonuses) - Drain, drops, special

---

## Constants Reference

<!-- RAG_CHUNK: bonus_constants -->

### Status Effect Constants (eff)
Used with bAddEff, bResEff, etc.

| Constant | Effect |
|----------|--------|
| Eff_Bleeding | Bleeding status |
| Eff_Blind | Blind status |
| Eff_Burning | Burning status |
| Eff_Confusion | Confusion status |
| Eff_Crystalize | Crystalize/Frozen status |
| Eff_Curse | Curse status |
| Eff_DPoison | Deadly Poison status |
| Eff_Fear | Fear status |
| Eff_Freeze | Freeze status |
| Eff_Poison | Poison status |
| Eff_Silence | Silence status |
| Eff_Sleep | Sleep status |
| Eff_Stone | Stone/Petrify status |
| Eff_Stun | Stun status |

### Element Constants (e)
| Constant | Element |
|----------|---------|
| Ele_Neutral | Neutral |
| Ele_Water | Water |
| Ele_Earth | Earth |
| Ele_Fire | Fire |
| Ele_Wind | Wind |
| Ele_Poison | Poison |
| Ele_Holy | Holy |
| Ele_Dark | Dark/Shadow |
| Ele_Ghost | Ghost |
| Ele_Undead | Undead |
| Ele_All | All elements |

### Race Constants (r)
| Constant | Race |
|----------|------|
| RC_Formless | Formless |
| RC_Undead | Undead |
| RC_Brute | Brute |
| RC_Plant | Plant |
| RC_Insect | Insect |
| RC_Fish | Fish |
| RC_Demon | Demon |
| RC_DemiHuman | Demi-Human |
| RC_Angel | Angel |
| RC_Dragon | Dragon |
| RC_Player_Human | Human Player |
| RC_Player_Doram | Doram Player |
| RC_All | All races |

### Class Constants (c)
| Constant | Class |
|----------|-------|
| Class_Normal | Normal monsters |
| Class_Boss | Boss monsters |
| Class_Guardian | Guardian monsters |
| Class_All | All classes |

### Size Constants (s)
| Constant | Size |
|----------|------|
| Size_Small | Small |
| Size_Medium | Medium |
| Size_Large | Large |
| Size_All | All sizes |

### Trigger Criteria (bf)
| Flag | Description |
|------|-------------|
| BF_SHORT | Trigger on melee attacks |
| BF_LONG | Trigger on ranged attacks |
| BF_WEAPON | Trigger on weapon skills |
| BF_MAGIC | Trigger on magic skills |
| BF_MISC | Trigger on misc skills |
| BF_NORMAL | Trigger on normal attacks |
| BF_SKILL | Trigger on skills |

### Attack Target Flags (atf)
| Flag | Description |
|------|-------------|
| ATF_SELF | Trigger effect on self |
| ATF_TARGET | Trigger effect on target |
| ATF_SHORT | Trigger on melee attacks |
| ATF_LONG | Trigger on ranged attacks |

---

## Complete Bonus Reference


## 1. Basic Bonuses

<!-- RAG_CHUNK: 1_basic_bonuses -->

<!-- RAG_CHUNK: bStr -->
### bStr

**Syntax:** `bonus bStr,n;`

**Effect:** STR + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bStr,n;
```

---

<!-- RAG_CHUNK: bAgi -->
### bAgi

**Syntax:** `bonus bAgi,n;`

**Effect:** AGI + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAgi,n;
```

---

<!-- RAG_CHUNK: bVit -->
### bVit

**Syntax:** `bonus bVit,n;`

**Effect:** VIT + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bVit,n;
```

---

<!-- RAG_CHUNK: bInt -->
### bInt

**Syntax:** `bonus bInt,n;`

**Effect:** INT + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bInt,n;
```

---

<!-- RAG_CHUNK: bDex -->
### bDex

**Syntax:** `bonus bDex,n;`

**Effect:** DEX + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bDex,n;
```

---

<!-- RAG_CHUNK: bLuk -->
### bLuk

**Syntax:** `bonus bLuk,n;`

**Effect:** LUK + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bLuk,n;
```

---

<!-- RAG_CHUNK: bAllStats -->
### bAllStats

**Syntax:** `bonus bAllStats,n;`

**Effect:** STR + n, AGI + n, VIT + n, INT + n, DEX + n, LUK + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAllStats,n;
```

---

<!-- RAG_CHUNK: bAgiVit -->
### bAgiVit

**Syntax:** `bonus bAgiVit,n;`

**Effect:** AGI + n, VIT + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAgiVit,n;
```

---

<!-- RAG_CHUNK: bAgiDexStr -->
### bAgiDexStr

**Syntax:** `bonus bAgiDexStr,n;`

**Effect:** STR + n, AGI + n, DEX + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAgiDexStr,n;
```

---

<!-- RAG_CHUNK: bPow -->
### bPow

**Syntax:** `bonus bPow,n;`

**Effect:** POW + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bPow,n;
```

---

<!-- RAG_CHUNK: bSta -->
### bSta

**Syntax:** `bonus bSta,n;`

**Effect:** STA + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bSta,n;
```

---

<!-- RAG_CHUNK: bWis -->
### bWis

**Syntax:** `bonus bWis,n;`

**Effect:** WIS + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bWis,n;
```

---

<!-- RAG_CHUNK: bSpl -->
### bSpl

**Syntax:** `bonus bSpl,n;`

**Effect:** SPL + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bSpl,n;
```

---

<!-- RAG_CHUNK: bCon -->
### bCon

**Syntax:** `bonus bCon,n;`

**Effect:** CON + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bCon,n;
```

---

<!-- RAG_CHUNK: bCrt -->
### bCrt

**Syntax:** `bonus bCrt,n;`

**Effect:** CRT + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bCrt,n;
```

---

<!-- RAG_CHUNK: bMaxHP -->
### bMaxHP

**Syntax:** `bonus bMaxHP,n;`

**Effect:** MaxHP + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMaxHP,n;
```

---

<!-- RAG_CHUNK: bMaxHPrate -->
### bMaxHPrate

**Syntax:** `bonus bMaxHPrate,n;`

**Effect:** MaxHP + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMaxHPrate,n;
```

---

<!-- RAG_CHUNK: bMaxSP -->
### bMaxSP

**Syntax:** `bonus bMaxSP,n;`

**Effect:** MaxSP + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMaxSP,n;
```

---

<!-- RAG_CHUNK: bMaxSPrate -->
### bMaxSPrate

**Syntax:** `bonus bMaxSPrate,n;`

**Effect:** MaxSP + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMaxSPrate,n;
```

---

<!-- RAG_CHUNK: bMaxAP -->
### bMaxAP

**Syntax:** `bonus bMaxAP,n;`

**Effect:** MaxAP + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMaxAP,n;
```

---

<!-- RAG_CHUNK: bMaxAPrate -->
### bMaxAPrate

**Syntax:** `bonus bMaxAPrate,n;`

**Effect:** MaxAP + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMaxAPrate,n;
```

---

<!-- RAG_CHUNK: bBaseAtk -->
### bBaseAtk

**Syntax:** `bonus bBaseAtk,n;`

**Effect:** Basic attack power + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bBaseAtk,n;
```

---

<!-- RAG_CHUNK: bAtk -->
### bAtk

**Syntax:** `bonus bAtk,n;`

**Effect:** ATK + n (unofficial)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAtk,n;
```

---

<!-- RAG_CHUNK: bAtk2 -->
### bAtk2

**Syntax:** `bonus bAtk2,n;`

**Effect:** ATK2 + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAtk2,n;
```

---

<!-- RAG_CHUNK: bAtkRate -->
### bAtkRate

**Syntax:** `bonus bAtkRate,n;`

**Effect:** ATK + n% that won't interfere with Damage modifier and SC_EDP (renewal mode only)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAtkRate,n;
```

---

<!-- RAG_CHUNK: bMatk -->
### bMatk

**Syntax:** `bonus bMatk,n;`

**Effect:** Magical attack power + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMatk,n;
```

---

<!-- RAG_CHUNK: bMatk2 -->
### bMatk2

**Syntax:** `bonus bMatk2,n;`

**Effect:** Magical attack power + n (not visible in status window)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMatk2,n;
```

---

<!-- RAG_CHUNK: bMatkRate -->
### bMatkRate

**Syntax:** `bonus bMatkRate,n;`

**Effect:** Magical attack power + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMatkRate,n;
```

---

<!-- RAG_CHUNK: bDef -->
### bDef

**Syntax:** `bonus bDef,n;`

**Effect:** Equipment DEF + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bDef,n;
```

---

<!-- RAG_CHUNK: bDefRate -->
### bDefRate

**Syntax:** `bonus bDefRate,n;`

**Effect:** Equipment DEF + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bDefRate,n;
```

---

<!-- RAG_CHUNK: bDef2 -->
### bDef2

**Syntax:** `bonus bDef2,n;`

**Effect:** VIT based DEF + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bDef2,n;
```

---

<!-- RAG_CHUNK: bDef2Rate -->
### bDef2Rate

**Syntax:** `bonus bDef2Rate,n;`

**Effect:** VIT based DEF + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bDef2Rate,n;
```

---

<!-- RAG_CHUNK: bMdef -->
### bMdef

**Syntax:** `bonus bMdef,n;`

**Effect:** Equipment MDEF + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMdef,n;
```

---

<!-- RAG_CHUNK: bMdefRate -->
### bMdefRate

**Syntax:** `bonus bMdefRate,n;`

**Effect:** Equipment MDEF + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMdefRate,n;
```

---

<!-- RAG_CHUNK: bMdef2 -->
### bMdef2

**Syntax:** `bonus bMdef2,n;`

**Effect:** INT based MDEF + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMdef2,n;
```

---

<!-- RAG_CHUNK: bMdef2Rate -->
### bMdef2Rate

**Syntax:** `bonus bMdef2Rate,n;`

**Effect:** INT based MDEF + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMdef2Rate,n;
```

---

<!-- RAG_CHUNK: bHit -->
### bHit

**Syntax:** `bonus bHit,n;`

**Effect:** Hit + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bHit,n;
```

---

<!-- RAG_CHUNK: bHitRate -->
### bHitRate

**Syntax:** `bonus bHitRate,n;`

**Effect:** Hit + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bHitRate,n;
```

---

<!-- RAG_CHUNK: bCritical -->
### bCritical

**Syntax:** `bonus bCritical,n;`

**Effect:** Critical + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bCritical,n;
```

---

<!-- RAG_CHUNK: bCriticalLong -->
### bCriticalLong

**Syntax:** `bonus bCriticalLong,n;`

**Effect:** Critical + n for normal long ranged attack (won't be shown in status window)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bCriticalLong,n;
```

---

<!-- RAG_CHUNK: bCriticalAddRace -->
### bCriticalAddRace

**Syntax:** `bonus2 bCriticalAddRace,r,n;`

**Effect:** Critical + n against enemies of race r

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bCriticalAddRace,r,n;
```

---

<!-- RAG_CHUNK: bCriticalRate -->
### bCriticalRate

**Syntax:** `bonus bCriticalRate,n;`

**Effect:** Critical + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bCriticalRate,n;
```

---

<!-- RAG_CHUNK: bFlee -->
### bFlee

**Syntax:** `bonus bFlee,n;`

**Effect:** Flee + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bFlee,n;
```

---

<!-- RAG_CHUNK: bFleeRate -->
### bFleeRate

**Syntax:** `bonus bFleeRate,n;`

**Effect:** Flee + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bFleeRate,n;
```

---

<!-- RAG_CHUNK: bFlee2 -->
### bFlee2

**Syntax:** `bonus bFlee2,n;`

**Effect:** Perfect Dodge + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bFlee2,n;
```

---

<!-- RAG_CHUNK: bFlee2Rate -->
### bFlee2Rate

**Syntax:** `bonus bFlee2Rate,n;`

**Effect:** Perfect Dodge + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bFlee2Rate,n;
```

---

<!-- RAG_CHUNK: bAspd -->
### bAspd

**Syntax:** `bonus bAspd,n;`

**Effect:** Attack speed + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAspd,n;
```

---

<!-- RAG_CHUNK: bAspdRate -->
### bAspdRate

**Syntax:** `bonus bAspdRate,n;`

**Effect:** Attack speed + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAspdRate,n;
```

---

<!-- RAG_CHUNK: bAtkRange -->
### bAtkRange

**Syntax:** `bonus bAtkRange,n;`

**Effect:** Attack range + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAtkRange,n;
```

---

<!-- RAG_CHUNK: bPAtk -->
### bPAtk

**Syntax:** `bonus bPAtk,n;`

**Effect:** PAtk + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bPAtk,n;
```

---

<!-- RAG_CHUNK: bPAtkRate -->
### bPAtkRate

**Syntax:** `bonus bPAtkRate,n;`

**Effect:** PAtk + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bPAtkRate,n;
```

---

<!-- RAG_CHUNK: bSMatk -->
### bSMatk

**Syntax:** `bonus bSMatk,n;`

**Effect:** SMatk + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bSMatk,n;
```

---

<!-- RAG_CHUNK: bSMatkRate -->
### bSMatkRate

**Syntax:** `bonus bSMatkRate,n;`

**Effect:** SMatk + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bSMatkRate,n;
```

---

<!-- RAG_CHUNK: bRes -->
### bRes

**Syntax:** `bonus bRes,n;`

**Effect:** Res + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bRes,n;
```

---

<!-- RAG_CHUNK: bResRate -->
### bResRate

**Syntax:** `bonus bResRate,n;`

**Effect:** Res + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bResRate,n;
```

---

<!-- RAG_CHUNK: bMRes -->
### bMRes

**Syntax:** `bonus bMRes,n;`

**Effect:** MRes + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMRes,n;
```

---

<!-- RAG_CHUNK: bMResRate -->
### bMResRate

**Syntax:** `bonus bMResRate,n;`

**Effect:** MRes + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMResRate,n;
```

---

<!-- RAG_CHUNK: bHPlus -->
### bHPlus

**Syntax:** `bonus bHPlus,n;`

**Effect:** HPlus + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bHPlus,n;
```

---

<!-- RAG_CHUNK: bHPlusRate -->
### bHPlusRate

**Syntax:** `bonus bHPlusRate,n;`

**Effect:** HPlus + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bHPlusRate,n;
```

---

<!-- RAG_CHUNK: bCRate -->
### bCRate

**Syntax:** `bonus bCRate,n;`

**Effect:** CRate + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bCRate,n;
```

---

<!-- RAG_CHUNK: bCRateRate -->
### bCRateRate

**Syntax:** `bonus bCRateRate,n;`

**Effect:** CRate + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bCRateRate,n;
```

---

<!-- RAG_CHUNK: bCriticalDef -->
### bCriticalDef

**Syntax:** `bonus bCriticalDef,n;`

**Effect:** Decreases the chance of being hit by critical hits by n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bCriticalDef,n;
```

---

<!-- RAG_CHUNK: bAtkEle -->
### bAtkEle

**Syntax:** `bonus bAtkEle,e;`

**Effect:** Gives the player's attacks element e

**Parameters:**
- `e`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAtkEle,e;
```

---

<!-- RAG_CHUNK: bDefEle -->
### bDefEle

**Syntax:** `bonus bDefEle,e;`

**Effect:** Gives the player's defense element e

**Parameters:**
- `e`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bDefEle,e;
```

---

<!-- RAG_CHUNK: bDefRatioAtkRace -->
### bDefRatioAtkRace

**Syntax:** `bonus bDefRatioAtkRace,r;`

**Effect:** Deals more damage to enemies of race r with higher defense

**Parameters:**
- `r`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bDefRatioAtkRace,r;
```

---

<!-- RAG_CHUNK: bDefRatioAtkEle -->
### bDefRatioAtkEle

**Syntax:** `bonus bDefRatioAtkEle,e;`

**Effect:** Deals more damage to enemies of element e with higher defense

**Parameters:**
- `e`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bDefRatioAtkEle,e;
```

---

<!-- RAG_CHUNK: bDefRatioAtkClass -->
### bDefRatioAtkClass

**Syntax:** `bonus bDefRatioAtkClass,c;`

**Effect:** Deals more damage to enemies of class c with higher defense

**Parameters:**
- `c`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bDefRatioAtkClass,c;
```

---

<!-- RAG_CHUNK: bResEff -->
### bResEff

**Syntax:** `bonus2 bResEff,eff,n;`

**Effect:** Adds a n/100% tolerance to status eff

**Parameters:**
- `eff`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bResEff,eff,n;
```

---

<!-- RAG_CHUNK: bStateNoRecoverRace -->
### bStateNoRecoverRace

**Syntax:** `bonus3 bStateNoRecoverRace,r,x,t;`

**Effect:** Set a no recovery state of an enemy of race r at x/100% for t milliseconds with normal attack.

**Parameters:**
- `r`
- `x`
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bStateNoRecoverRace,r,x,t;
```

---

<!-- RAG_CHUNK: bSplashRange -->
### bSplashRange

**Syntax:** `bonus bSplashRange,n;`

**Effect:** Splash attack radius + n (only the highest among all is applied)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bSplashRange,n;
```

---

<!-- RAG_CHUNK: bSplashAddRange -->
### bSplashAddRange

**Syntax:** `bonus bSplashAddRange,n;`

**Effect:** Splash attack radius + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bSplashAddRange,n;
```

---

<!-- RAG_CHUNK: bIntravision -->
### bIntravision

**Syntax:** `bonus bIntravision,Always see Hiding and Cloaking players/mobs;`

**Parameters:**
- `Always see Hiding and Cloaking players/mobs`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bIntravision,Always see Hiding and Cloaking players/mobs;
```

---

<!-- RAG_CHUNK: bRestartFullRecover -->
### bRestartFullRecover

**Syntax:** `bonus bRestartFullRecover,When reviving, HP and SP are fully healed;`

**Parameters:**
- `When reviving`
- `HP and SP are fully healed`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bRestartFullRecover,When reviving, HP and SP are fully healed;
```

---


## 2. Extended Bonuses

<!-- RAG_CHUNK: 2_extended_bonuses -->

<!-- RAG_CHUNK: bHPrecovRate -->
### bHPrecovRate

**Syntax:** `bonus bHPrecovRate,n;`

**Effect:** Natural HP recovery ratio + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bHPrecovRate,n;
```

---

<!-- RAG_CHUNK: bSPrecovRate -->
### bSPrecovRate

**Syntax:** `bonus bSPrecovRate,n;`

**Effect:** Natural SP recovery ratio + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bSPrecovRate,n;
```

---

<!-- RAG_CHUNK: bHPRegenRate -->
### bHPRegenRate

**Syntax:** `bonus2 bHPRegenRate,n,t;`

**Effect:** Gain n HP every t milliseconds

**Parameters:**
- `n`
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bHPRegenRate,n,t;
```

---

<!-- RAG_CHUNK: bHPLossRate -->
### bHPLossRate

**Syntax:** `bonus2 bHPLossRate,n,t;`

**Effect:** Lose n HP every t milliseconds

**Parameters:**
- `n`
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bHPLossRate,n,t;
```

---

<!-- RAG_CHUNK: bSPRegenRate -->
### bSPRegenRate

**Syntax:** `bonus2 bSPRegenRate,n,t;`

**Effect:** Gain n SP every t milliseconds

**Parameters:**
- `n`
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSPRegenRate,n,t;
```

---

<!-- RAG_CHUNK: bSPLossRate -->
### bSPLossRate

**Syntax:** `bonus2 bSPLossRate,n,t;`

**Effect:** Lose n SP every t milliseconds

**Parameters:**
- `n`
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSPLossRate,n,t;
```

---

<!-- RAG_CHUNK: bUseSPrate -->
### bUseSPrate

**Syntax:** `bonus bUseSPrate,n;`

**Effect:** SP consumption + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bUseSPrate,n;
```

---

<!-- RAG_CHUNK: bSkillUseSP -->
### bSkillUseSP

**Syntax:** `bonus2 bSkillUseSP,sk,n;`

**Effect:** Decreases SP consumption of skill sk by n

**Parameters:**
- `sk`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSkillUseSP,sk,n;
```

---

<!-- RAG_CHUNK: bSkillUseSPrate -->
### bSkillUseSPrate

**Syntax:** `bonus2 bSkillUseSPrate,sk,n;`

**Effect:** Decreases SP consumption of skill sk by n%

**Parameters:**
- `sk`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSkillUseSPrate,sk,n;
```

---

<!-- RAG_CHUNK: bSkillAtk -->
### bSkillAtk

**Syntax:** `bonus2 bSkillAtk,sk,n;`

**Effect:** Increases damage of skill sk by n%

**Parameters:**
- `sk`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSkillAtk,sk,n;
```

---

<!-- RAG_CHUNK: bShortAtkRate -->
### bShortAtkRate

**Syntax:** `bonus bShortAtkRate,n;`

**Effect:** Increases damage of short ranged attacks by n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bShortAtkRate,n;
```

---

<!-- RAG_CHUNK: bLongAtkRate -->
### bLongAtkRate

**Syntax:** `bonus bLongAtkRate,n;`

**Effect:** Increases damage of long ranged attacks by n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bLongAtkRate,n;
```

---

<!-- RAG_CHUNK: bCritAtkRate -->
### bCritAtkRate

**Syntax:** `bonus bCritAtkRate,n;`

**Effect:** Increases critical damage by +n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bCritAtkRate,n;
```

---

<!-- RAG_CHUNK: bHealPower -->
### bHealPower

**Syntax:** `bonus bHealPower,n;`

**Effect:** Increases heal amount of all heal skills by n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bHealPower,n;
```

---

<!-- RAG_CHUNK: bHealPower2 -->
### bHealPower2

**Syntax:** `bonus bHealPower2,n;`

**Effect:** Increases heal amount if you are healed by any skills by n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bHealPower2,n;
```

---

<!-- RAG_CHUNK: bAddItemHealRate -->
### bAddItemHealRate

**Syntax:** `bonus bAddItemHealRate,n;`

**Effect:** Increases HP recovered by n% for healing items

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAddItemHealRate,n;
```

---

<!-- RAG_CHUNK: bAddItemHealRate -->
### bAddItemHealRate

**Syntax:** `bonus2 bAddItemHealRate,iid,n;`

**Effect:** Increases HP recovered by n% for item iid

**Parameters:**
- `iid`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddItemHealRate,iid,n;
```

---

<!-- RAG_CHUNK: bCastrate -->
### bCastrate

**Syntax:** `bonus bCastrate,n;`

**Effect:** Skill cast time rate + n%. (If RENEWAL_CAST is defined, this bonus is equal to bVariableCastrate)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bCastrate,n;
```

---

<!-- RAG_CHUNK: bCastrate -->
### bCastrate

**Syntax:** `bonus2 bCastrate,sk,n;`

**Effect:** Adjust casting time of skill sk by n%.(If RENEWAL_CAST is defined, this bonus is equal to bVariableCastrate)

**Parameters:**
- `sk`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bCastrate,sk,n;
```

---

<!-- RAG_CHUNK: bFixedCastrate -->
### bFixedCastrate

**Syntax:** `bonus bFixedCastrate,n;`

**Effect:** Increases fixed cast time of all skills by n% (has effect in RENEWAL_CAST only)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bFixedCastrate,n;
```

---

<!-- RAG_CHUNK: bFixedCastrate -->
### bFixedCastrate

**Syntax:** `bonus2 bFixedCastrate,sk,n;`

**Effect:** Increases fixed cast time of skill sk by n% (has effect in RENEWAL_CAST only)

**Parameters:**
- `sk`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bFixedCastrate,sk,n;
```

---

<!-- RAG_CHUNK: bVariableCastrate -->
### bVariableCastrate

**Syntax:** `bonus bVariableCastrate,n;`

**Effect:** Increases variable cast time of all skills by n%. (If RENEWAL_CAST is NOT defined, this bonus is equal to bCastrate)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bVariableCastrate,n;
```

---

<!-- RAG_CHUNK: bVariableCastrate -->
### bVariableCastrate

**Syntax:** `bonus2 bVariableCastrate,sk,n;`

**Effect:** Increases variable cast time of skill sk by n% (If RENEWAL_CAST is NOT defined, this bonus is equal to bCastrate)

**Parameters:**
- `sk`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bVariableCastrate,sk,n;
```

---

<!-- RAG_CHUNK: bFixedCast -->
### bFixedCast

**Syntax:** `bonus bFixedCast,t;`

**Effect:** Increases fixed cast time of all skills by t milliseconds (has effect in RENEWAL_CAST only)

**Parameters:**
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bFixedCast,t;
```

---

<!-- RAG_CHUNK: bVariableCast -->
### bVariableCast

**Syntax:** `bonus bVariableCast,t;`

**Effect:** Increases variable cast time of all skills by t milliseconds

**Parameters:**
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bVariableCast,t;
```

---

<!-- RAG_CHUNK: bNoCastCancel -->
### bNoCastCancel

**Syntax:** `bonus bNoCastCancel,Prevents casting from being interrupted when hit (does not work in GvG);`

**Parameters:**
- `Prevents casting from being interrupted when hit (does not work in GvG)`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bNoCastCancel,Prevents casting from being interrupted when hit (does not work in GvG);
```

---

<!-- RAG_CHUNK: bNoCastCancel2 -->
### bNoCastCancel2

**Syntax:** `bonus bNoCastCancel2,Prevents casting from being interrupted when hit (works even in GvG);`

**Parameters:**
- `Prevents casting from being interrupted when hit (works even in GvG)`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bNoCastCancel2,Prevents casting from being interrupted when hit (works even in GvG);
```

---

<!-- RAG_CHUNK: bDelayrate -->
### bDelayrate

**Syntax:** `bonus bDelayrate,n;`

**Effect:** Increases skill delay by n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bDelayrate,n;
```

---


## 3. Group-Specific Bonuses

<!-- RAG_CHUNK: 3_group-specific_bonuses -->

<!-- RAG_CHUNK: bAddEle -->
### bAddEle

**Syntax:** `bonus2 bAddEle,e,x;`

**Effect:** +x% physical damage against element e

**Parameters:**
- `e`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddEle,e,x;
```

---

<!-- RAG_CHUNK: bAddEle -->
### bAddEle

**Syntax:** `bonus3 bAddEle,e,x,bf;`

**Effect:** +x% physical damage against element e with trigger criteria bf

**Parameters:**
- `e`
- `x`
- `bf`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bAddEle,e,x,bf;
```

---

<!-- RAG_CHUNK: bMagicAddEle -->
### bMagicAddEle

**Syntax:** `bonus2 bMagicAddEle,e,x;`

**Effect:** +x% magical damage against element e

**Parameters:**
- `e`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bMagicAddEle,e,x;
```

---

<!-- RAG_CHUNK: bSubEle -->
### bSubEle

**Syntax:** `bonus2 bSubEle,e,x;`

**Effect:** +x% damage reduction against attack element e

**Parameters:**
- `e`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSubEle,e,x;
```

---

<!-- RAG_CHUNK: bSubEle -->
### bSubEle

**Syntax:** `bonus3 bSubEle,e,x,bf;`

**Effect:** +x% damage reduction against attack element e with trigger criteria bf

**Parameters:**
- `e`
- `x`
- `bf`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bSubEle,e,x,bf;
```

---

<!-- RAG_CHUNK: bAddRace -->
### bAddRace

**Syntax:** `bonus2 bAddRace,r,x;`

**Effect:** +x% physical damage against race r

**Parameters:**
- `r`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddRace,r,x;
```

---

<!-- RAG_CHUNK: bMagicAddRace -->
### bMagicAddRace

**Syntax:** `bonus2 bMagicAddRace,r,x;`

**Effect:** +x% magical damage against race r

**Parameters:**
- `r`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bMagicAddRace,r,x;
```

---

<!-- RAG_CHUNK: bSubRace -->
### bSubRace

**Syntax:** `bonus2 bSubRace,r,x;`

**Effect:** +x% damage reduction against race r

**Parameters:**
- `r`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSubRace,r,x;
```

---

<!-- RAG_CHUNK: bSubRace -->
### bSubRace

**Syntax:** `bonus3 bSubRace,r,x,bf;`

**Effect:** +x% damage reduction against race r with trigger criteria bf

**Parameters:**
- `r`
- `x`
- `bf`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bSubRace,r,x,bf;
```

---

<!-- RAG_CHUNK: bAddClass -->
### bAddClass

**Syntax:** `bonus2 bAddClass,c,x;`

**Effect:** +x% physical damage against class c

**Parameters:**
- `c`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddClass,c,x;
```

---

<!-- RAG_CHUNK: bSubClass -->
### bSubClass

**Syntax:** `bonus2 bSubClass,c,x;`

**Effect:** +x% damage reduction against class c

**Parameters:**
- `c`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSubClass,c,x;
```

---

<!-- RAG_CHUNK: bAddSize -->
### bAddSize

**Syntax:** `bonus2 bAddSize,s,x;`

**Effect:** +x% physical damage against size s

**Parameters:**
- `s`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddSize,s,x;
```

---

<!-- RAG_CHUNK: bSubSize -->
### bSubSize

**Syntax:** `bonus2 bSubSize,s,x;`

**Effect:** +x% damage reduction against size s

**Parameters:**
- `s`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSubSize,s,x;
```

---

<!-- RAG_CHUNK: bAddRace2 -->
### bAddRace2

**Syntax:** `bonus2 bAddRace2,mr,x;`

**Effect:** +x% damage against monster race mr

**Parameters:**
- `mr`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddRace2,mr,x;
```

---

<!-- RAG_CHUNK: bSubRace2 -->
### bSubRace2

**Syntax:** `bonus2 bSubRace2,mr,x;`

**Effect:** +x% damage reduction against monster race mr

**Parameters:**
- `mr`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSubRace2,mr,x;
```

---

<!-- RAG_CHUNK: bMagicAddRace2 -->
### bMagicAddRace2

**Syntax:** `bonus2 bMagicAddRace2,mr,x;`

**Effect:** +x% magic damage against monster race mr

**Parameters:**
- `mr`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bMagicAddRace2,mr,x;
```

---

<!-- RAG_CHUNK: bIgnoreDefEle -->
### bIgnoreDefEle

**Syntax:** `bonus bIgnoreDefEle,e;`

**Effect:** Disregard DEF against enemies of element e

**Parameters:**
- `e`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bIgnoreDefEle,e;
```

---

<!-- RAG_CHUNK: bIgnoreDefRace -->
### bIgnoreDefRace

**Syntax:** `bonus bIgnoreDefRace,r;`

**Effect:** Disregard DEF against enemies of race r

**Parameters:**
- `r`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bIgnoreDefRace,r;
```

---

<!-- RAG_CHUNK: bIgnoreDefClass -->
### bIgnoreDefClass

**Syntax:** `bonus bIgnoreDefClass,c;`

**Effect:** Disregard DEF against enemies of class c

**Parameters:**
- `c`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bIgnoreDefClass,c;
```

---

<!-- RAG_CHUNK: bIgnoreDefRaceRate -->
### bIgnoreDefRaceRate

**Syntax:** `bonus2 bIgnoreDefRaceRate,r,n;`

**Effect:** Disregard n% of the target's DEF if the target belongs to race r

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bIgnoreDefRaceRate,r,n;
```

---

<!-- RAG_CHUNK: bIgnoreDefClassRate -->
### bIgnoreDefClassRate

**Syntax:** `bonus2 bIgnoreDefClassRate,c,n;`

**Effect:** Disregard n% of the target's DEF if the target belongs to class c

**Parameters:**
- `c`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bIgnoreDefClassRate,c,n;
```

---

<!-- RAG_CHUNK: bExpAddRace -->
### bExpAddRace

**Syntax:** `bonus2 bExpAddRace,r,x;`

**Effect:** Increase exp gained by x% against enemies of race r

**Parameters:**
- `r`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bExpAddRace,r,x;
```

---

<!-- RAG_CHUNK: bExpAddClass -->
### bExpAddClass

**Syntax:** `bonus2 bExpAddClass,c,x;`

**Effect:** Increase exp gained by x% against enemies of class c

**Parameters:**
- `c`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bExpAddClass,c,x;
```

---

<!-- RAG_CHUNK: bAddClassDropItem -->
### bAddClassDropItem

**Syntax:** `bonus3 bAddClassDropItem,iid,c,n;`

**Effect:** Adds a n/100% chance for item iid to be dropped when killing a monster of class c

**Parameters:**
- `iid`
- `c`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bAddClassDropItem,iid,c,n;
```

---

<!-- RAG_CHUNK: bAddClassDropItemGroup -->
### bAddClassDropItemGroup

**Syntax:** `bonus3 bAddClassDropItemGroup,ig,c,n;`

**Effect:** Adds a n/100% chance to get an item of group type ig when killing a monster of class c

**Parameters:**
- `ig`
- `c`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bAddClassDropItemGroup,ig,c,n;
```

---


## 4. Status-Related Bonuses

<!-- RAG_CHUNK: 4_status-related_bonuses -->

<!-- RAG_CHUNK: bAddEff -->
### bAddEff

**Syntax:** `bonus2 bAddEff,eff,n;`

**Effect:** Adds a n/100% chance to cause status eff on the target when attacking

**Parameters:**
- `eff`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddEff,eff,n;
```

---

<!-- RAG_CHUNK: bAddEff2 -->
### bAddEff2

**Syntax:** `bonus2 bAddEff2,eff,n;`

**Effect:** Adds a n/100% chance to cause status eff on self when attacking

**Parameters:**
- `eff`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddEff2,eff,n;
```

---

<!-- RAG_CHUNK: bAddEffWhenHit -->
### bAddEffWhenHit

**Syntax:** `bonus2 bAddEffWhenHit,eff,n;`

**Effect:** Adds a n/100% chance to cause status eff on the enemy when being hit by physical damage

**Parameters:**
- `eff`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddEffWhenHit,eff,n;
```

---

<!-- RAG_CHUNK: bAddEff -->
### bAddEff

**Syntax:** `bonus3 bAddEff,eff,n,atf;`

**Effect:** Adds a n/100% chance to cause status eff on the target when attacking

**Parameters:**
- `eff`
- `n`
- `atf`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bAddEff,eff,n,atf;
```

---

<!-- RAG_CHUNK: bAddEff -->
### bAddEff

**Syntax:** `bonus4 bAddEff,eff,n,atf,t;`

**Effect:** Adds a n/100% chance to cause status eff for t milliseconds on the target when attacking

**Parameters:**
- `eff`
- `n`
- `atf`
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus4 bAddEff,eff,n,atf,t;
```

---

<!-- RAG_CHUNK: bAddEffWhenHit -->
### bAddEffWhenHit

**Syntax:** `bonus3 bAddEffWhenHit,eff,n,atf;`

**Effect:** Adds a n/100% chance to cause status eff on the target when being hit by physical damage

**Parameters:**
- `eff`
- `n`
- `atf`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bAddEffWhenHit,eff,n,atf;
```

---

<!-- RAG_CHUNK: bAddEffWhenHit -->
### bAddEffWhenHit

**Syntax:** `bonus4 bAddEffWhenHit,eff,n,atf,t;`

**Effect:** Adds a n/100% chance to cause status eff for t milliseconds on the target when being hit by physical damage

**Parameters:**
- `eff`
- `n`
- `atf`
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus4 bAddEffWhenHit,eff,n,atf,t;
```

---

<!-- RAG_CHUNK: bAddEffOnSkill -->
### bAddEffOnSkill

**Syntax:** `bonus3 bAddEffOnSkill,sk,eff,n;`

**Effect:** Adds a n/100% chance to cause status eff on enemy when using skill sk

**Parameters:**
- `sk`
- `eff`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bAddEffOnSkill,sk,eff,n;
```

---

<!-- RAG_CHUNK: bAddEffOnSkill -->
### bAddEffOnSkill

**Syntax:** `bonus4 bAddEffOnSkill,sk,eff,n,atf;`

**Effect:** Adds a n/100% chance to cause status eff on the target when using skill sk

**Parameters:**
- `sk`
- `eff`
- `n`
- `atf`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus4 bAddEffOnSkill,sk,eff,n,atf;
```

---

<!-- RAG_CHUNK: bAddEffOnSkill -->
### bAddEffOnSkill

**Syntax:** `bonus5 bAddEffOnSkill,sk,eff,n,atf,t;`

**Effect:** Adds a n/100% chance to cause status eff for t milliseconds on the target when using skill sk

**Parameters:**
- `sk`
- `eff`
- `n`
- `atf`
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus5 bAddEffOnSkill,sk,eff,n,atf,t;
```

---

<!-- RAG_CHUNK: bComaClass -->
### bComaClass

**Syntax:** `bonus2 bComaClass,c,n;`

**Effect:** Adds a n/100% chance to cause Coma when attacking a target of class c (regardless the type of attack)

**Parameters:**
- `c`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bComaClass,c,n;
```

---

<!-- RAG_CHUNK: bComaRace -->
### bComaRace

**Syntax:** `bonus2 bComaRace,r,n;`

**Effect:** Adds a n/100% chance to cause Coma when attacking a target of race r (regardless the type of attack)

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bComaRace,r,n;
```

---

<!-- RAG_CHUNK: bWeaponComaEle -->
### bWeaponComaEle

**Syntax:** `bonus2 bWeaponComaEle,e,n;`

**Effect:** Adds a n/100% chance to cause Coma when attacking a target of element e with a normal attack

**Parameters:**
- `e`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bWeaponComaEle,e,n;
```

---

<!-- RAG_CHUNK: bWeaponComaClass -->
### bWeaponComaClass

**Syntax:** `bonus2 bWeaponComaClass,c,n;`

**Effect:** Adds a n/100% chance to cause Coma when attacking a target of class c with a normal attack

**Parameters:**
- `c`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bWeaponComaClass,c,n;
```

---

<!-- RAG_CHUNK: bWeaponComaRace -->
### bWeaponComaRace

**Syntax:** `bonus2 bWeaponComaRace,r,n;`

**Effect:** Adds a n/100% chance to cause Coma when attacking a target of race r with a normal attack

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bWeaponComaRace,r,n;
```

---


## 5. AutoSpell Bonuses

<!-- RAG_CHUNK: 5_autospell_bonuses -->

<!-- RAG_CHUNK: bAutoSpell -->
### bAutoSpell

**Syntax:** `bonus3 bAutoSpell,sk,y,n;`

**Effect:** Adds a n/10% chance to cast skill sk of level y when attacking

**Parameters:**
- `sk`
- `y`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bAutoSpell,sk,y,n;
```

---

<!-- RAG_CHUNK: bAutoSpellWhenHit -->
### bAutoSpellWhenHit

**Syntax:** `bonus3 bAutoSpellWhenHit,sk,y,n;`

**Effect:** Adds a n/10% chance to cast skill sk of level y when being hit by a direct attack

**Parameters:**
- `sk`
- `y`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bAutoSpellWhenHit,sk,y,n;
```

---

<!-- RAG_CHUNK: bAutoSpell -->
### bAutoSpell

**Syntax:** `bonus4 bAutoSpell,sk,y,n,i;`

**Effect:** Adds a n/10% chance to cast skill sk of level y when attacking

**Parameters:**
- `sk`
- `y`
- `n`
- `i`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus4 bAutoSpell,sk,y,n,i;
```

---

<!-- RAG_CHUNK: bAutoSpell -->
### bAutoSpell

**Syntax:** `bonus5 bAutoSpell,sk,y,n,bf,i;`

**Effect:** Adds a n/10% chance to cast skill sk of level y when attacking with trigger criteria bf

**Parameters:**
- `sk`
- `y`
- `n`
- `bf`
- `i`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus5 bAutoSpell,sk,y,n,bf,i;
```

---

<!-- RAG_CHUNK: bAutoSpellWhenHit -->
### bAutoSpellWhenHit

**Syntax:** `bonus4 bAutoSpellWhenHit,sk,y,n,i;`

**Effect:** Adds a n/10% chance to cast skill sk of level y when being hit by a direct attack

**Parameters:**
- `sk`
- `y`
- `n`
- `i`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus4 bAutoSpellWhenHit,sk,y,n,i;
```

---

<!-- RAG_CHUNK: bAutoSpellWhenHit -->
### bAutoSpellWhenHit

**Syntax:** `bonus5 bAutoSpellWhenHit,sk,y,n,bf,i;`

**Effect:** Adds a n/10% chance to cast skill sk of level y when being hit by a direct attack with trigger criteria bf

**Parameters:**
- `sk`
- `y`
- `n`
- `bf`
- `i`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus5 bAutoSpellWhenHit,sk,y,n,bf,i;
```

---

<!-- RAG_CHUNK: bAutoSpellOnSkill -->
### bAutoSpellOnSkill

**Syntax:** `bonus4 bAutoSpellOnSkill,sk,x,y,n;`

**Effect:** Adds a n/10% chance to autospell skill x at level y when using skill sk

**Parameters:**
- `sk`
- `x`
- `y`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus4 bAutoSpellOnSkill,sk,x,y,n;
```

---

<!-- RAG_CHUNK: bAutoSpellOnSkill -->
### bAutoSpellOnSkill

**Syntax:** `bonus5 bAutoSpellOnSkill,sk,x,y,n,i;`

**Effect:** Adds a n/10% chance to autospell skill x at level y when using skill sk

**Parameters:**
- `sk`
- `x`
- `y`
- `n`
- `i`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus5 bAutoSpellOnSkill,sk,x,y,n,i;
```

---


## 6. Misc Bonuses

<!-- RAG_CHUNK: 6_misc_bonuses -->

<!-- RAG_CHUNK: bAllTraitStats -->
### bAllTraitStats

**Syntax:** `bonus bAllTraitStats,n;`

**Effect:** POW + n, STA + n, WIS + n, SPL + n, CON + n, CRT + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAllTraitStats,n;
```

---

<!-- RAG_CHUNK: bWeaponAtkRate -->
### bWeaponAtkRate

**Syntax:** `bonus bWeaponAtkRate,n;`

**Effect:** Weapon ATK + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bWeaponAtkRate,n;
```

---

<!-- RAG_CHUNK: bWeaponMatkRate -->
### bWeaponMatkRate

**Syntax:** `bonus bWeaponMatkRate,n;`

**Effect:** Weapon Magical ATK + n% (renewal mode only)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bWeaponMatkRate,n;
```

---

<!-- RAG_CHUNK: bPerfectHitRate -->
### bPerfectHitRate

**Syntax:** `bonus bPerfectHitRate,n;`

**Effect:** On-target impact attack probability n% (only the highest among all is applied)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bPerfectHitRate,n;
```

---

<!-- RAG_CHUNK: bPerfectHitAddRate -->
### bPerfectHitAddRate

**Syntax:** `bonus bPerfectHitAddRate,n;`

**Effect:** On-target impact attack probability + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bPerfectHitAddRate,n;
```

---

<!-- RAG_CHUNK: bSpeedRate -->
### bSpeedRate

**Syntax:** `bonus bSpeedRate,n;`

**Effect:** Movement speed + n% (only the highest among all is applied, won't be stacked with SC_SPEEDUP0, SC_SPEEDUP1)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bSpeedRate,n;
```

---

<!-- RAG_CHUNK: bSpeedAddRate -->
### bSpeedAddRate

**Syntax:** `bonus bSpeedAddRate,n;`

**Effect:** Movement speed + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bSpeedAddRate,n;
```

---

<!-- RAG_CHUNK: bAddMaxWeight -->
### bAddMaxWeight

**Syntax:** `bonus bAddMaxWeight,n;`

**Effect:** MaxWeight + n (in units of 0.1)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAddMaxWeight,n;
```

---

<!-- RAG_CHUNK: bRegenPercentHP -->
### bRegenPercentHP

**Syntax:** `bonus2 bRegenPercentHP,n,t;`

**Effect:** Gain n% of max HP every t milliseconds

**Parameters:**
- `n`
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bRegenPercentHP,n,t;
```

---

<!-- RAG_CHUNK: bRegenPercentSP -->
### bRegenPercentSP

**Syntax:** `bonus2 bRegenPercentSP,n,t;`

**Effect:** Gain n% of max SP every t milliseconds

**Parameters:**
- `n`
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bRegenPercentSP,n,t;
```

---

<!-- RAG_CHUNK: bNoRegen -->
### bNoRegen

**Syntax:** `bonus bNoRegen,x;`

**Effect:** Stops HP or SP regeneration (x: 1=HP, 2=SP)

**Parameters:**
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bNoRegen,x;
```

---

<!-- RAG_CHUNK: bSkillRatio -->
### bSkillRatio

**Syntax:** `bonus bSkillRatio,n;`

**Effect:** Adds n to the skillratio of all attacks/skills that use it

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bSkillRatio,n;
```

---

<!-- RAG_CHUNK: bCritDefRate -->
### bCritDefRate

**Syntax:** `bonus bCritDefRate,n;`

**Effect:** Decreases critical damage received by n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bCritDefRate,n;
```

---

<!-- RAG_CHUNK: bWeaponAtk -->
### bWeaponAtk

**Syntax:** `bonus2 bWeaponAtk,w,n;`

**Effect:** Adds n ATK when weapon of type w is equipped

**Parameters:**
- `w`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bWeaponAtk,w,n;
```

---

<!-- RAG_CHUNK: bWeaponDamageRate -->
### bWeaponDamageRate

**Syntax:** `bonus2 bWeaponDamageRate,w,n;`

**Effect:** Adds n% damage to normal attacks when weapon of type w is equipped

**Parameters:**
- `w`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bWeaponDamageRate,w,n;
```

---

<!-- RAG_CHUNK: bNearAtkDef -->
### bNearAtkDef

**Syntax:** `bonus bNearAtkDef,n;`

**Effect:** Adds n% damage reduction against melee physical attacks

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bNearAtkDef,n;
```

---

<!-- RAG_CHUNK: bLongAtkDef -->
### bLongAtkDef

**Syntax:** `bonus bLongAtkDef,n;`

**Effect:** Adds n% damage reduction against ranged physical attacks

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bLongAtkDef,n;
```

---

<!-- RAG_CHUNK: bMagicAtkDef -->
### bMagicAtkDef

**Syntax:** `bonus bMagicAtkDef,n;`

**Effect:** Adds n% damage reduction against magical attacks

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMagicAtkDef,n;
```

---

<!-- RAG_CHUNK: bMiscAtkDef -->
### bMiscAtkDef

**Syntax:** `bonus bMiscAtkDef,n;`

**Effect:** Adds n% damage reduction against MISC attacks (traps, falcon, ...)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMiscAtkDef,n;
```

---

<!-- RAG_CHUNK: bNoWeaponDamage -->
### bNoWeaponDamage

**Syntax:** `bonus bNoWeaponDamage,n;`

**Effect:** Adds n% reduction to received physical damage

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bNoWeaponDamage,n;
```

---

<!-- RAG_CHUNK: bNoMagicDamage -->
### bNoMagicDamage

**Syntax:** `bonus bNoMagicDamage,n;`

**Effect:** Adds n% reduction to received magical effect (attack, healing, support spells are all blocked)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bNoMagicDamage,n;
```

---

<!-- RAG_CHUNK: bNoMiscDamage -->
### bNoMiscDamage

**Syntax:** `bonus bNoMiscDamage,n;`

**Effect:** Adds n% reduction to received misc damage

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bNoMiscDamage,n;
```

---

<!-- RAG_CHUNK: bSkillHeal -->
### bSkillHeal

**Syntax:** `bonus2 bSkillHeal,sk,n;`

**Effect:** Increases heal amount of skill sk by n%

**Parameters:**
- `sk`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSkillHeal,sk,n;
```

---

<!-- RAG_CHUNK: bSkillHeal2 -->
### bSkillHeal2

**Syntax:** `bonus2 bSkillHeal2,sk,n;`

**Effect:** Increases heal amount if you are healed by skill sk by n%

**Parameters:**
- `sk`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSkillHeal2,sk,n;
```

---

<!-- RAG_CHUNK: bAddItemGroupHealRate -->
### bAddItemGroupHealRate

**Syntax:** `bonus2 bAddItemGroupHealRate,ig,n;`

**Effect:** Increases HP recovered by n% for items of item group ig

**Parameters:**
- `ig`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddItemGroupHealRate,ig,n;
```

---

<!-- RAG_CHUNK: bAddItemSPHealRate -->
### bAddItemSPHealRate

**Syntax:** `bonus bAddItemSPHealRate,n;`

**Effect:** Increases SP recovered by n% for healing items

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAddItemSPHealRate,n;
```

---

<!-- RAG_CHUNK: bAddItemSPHealRate -->
### bAddItemSPHealRate

**Syntax:** `bonus2 bAddItemSPHealRate,iid,n;`

**Effect:** Increases SP recovered by n% for item iid

**Parameters:**
- `iid`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddItemSPHealRate,iid,n;
```

---

<!-- RAG_CHUNK: bAddItemGroupSPHealRate -->
### bAddItemGroupSPHealRate

**Syntax:** `bonus2 bAddItemGroupSPHealRate,ig,n;`

**Effect:** Increases SP recovered by n% for items of item group ig

**Parameters:**
- `ig`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddItemGroupSPHealRate,ig,n;
```

---

<!-- RAG_CHUNK: bSkillFixedCast -->
### bSkillFixedCast

**Syntax:** `bonus2 bSkillFixedCast,sk,t;`

**Effect:** Increases fixed cast time of skill sk by t milliseconds (has effect in RENEWAL_CAST only)

**Parameters:**
- `sk`
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSkillFixedCast,sk,t;
```

---

<!-- RAG_CHUNK: bSkillVariableCast -->
### bSkillVariableCast

**Syntax:** `bonus2 bSkillVariableCast,sk,t;`

**Effect:** Increases variable cast time of skill sk by t milliseconds

**Parameters:**
- `sk`
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSkillVariableCast,sk,t;
```

---

<!-- RAG_CHUNK: bSkillDelay -->
### bSkillDelay

**Syntax:** `bonus2 bSkillDelay,sk,t;`

**Effect:** Increases delay of skill sk by t milliseconds

**Parameters:**
- `sk`
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSkillDelay,sk,t;
```

---

<!-- RAG_CHUNK: bSkillCooldown -->
### bSkillCooldown

**Syntax:** `bonus2 bSkillCooldown,sk,t;`

**Effect:** Increases cooldown of skill sk by t milliseconds

**Parameters:**
- `sk`
- `t`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSkillCooldown,sk,t;
```

---

<!-- RAG_CHUNK: bSubDefEle -->
### bSubDefEle

**Syntax:** `bonus2 bSubDefEle,e,x;`

**Effect:** +x% physical damage reduction from enemy with defense element e

**Parameters:**
- `e`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSubDefEle,e,x;
```

---

<!-- RAG_CHUNK: bMagicSubDefEle -->
### bMagicSubDefEle

**Syntax:** `bonus2 bMagicSubDefEle,e,x;`

**Effect:** +x% magic damage reduction from enemy with defense element e

**Parameters:**
- `e`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bMagicSubDefEle,e,x;
```

---

<!-- RAG_CHUNK: bMagicAddClass -->
### bMagicAddClass

**Syntax:** `bonus2 bMagicAddClass,c,x;`

**Effect:** +x% magical damage against class c

**Parameters:**
- `c`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bMagicAddClass,c,x;
```

---

<!-- RAG_CHUNK: bMagicAddSize -->
### bMagicAddSize

**Syntax:** `bonus2 bMagicAddSize,s,x;`

**Effect:** +x% magical damage against size s

**Parameters:**
- `s`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bMagicAddSize,s,x;
```

---

<!-- RAG_CHUNK: bWeaponSubSize -->
### bWeaponSubSize

**Syntax:** `bonus2 bWeaponSubSize,s,x;`

**Effect:** +x% physical damage reduction against size s

**Parameters:**
- `s`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bWeaponSubSize,s,x;
```

---

<!-- RAG_CHUNK: bMagicSubSize -->
### bMagicSubSize

**Syntax:** `bonus2 bMagicSubSize,s,x;`

**Effect:** +x% magic damage reduction against size s

**Parameters:**
- `s`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bMagicSubSize,s,x;
```

---

<!-- RAG_CHUNK: bNoSizeFix -->
### bNoSizeFix

**Syntax:** `bonus bNoSizeFix,Ignores the size modifier when calculating damage;`

**Parameters:**
- `Ignores the size modifier when calculating damage`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bNoSizeFix,Ignores the size modifier when calculating damage;
```

---

<!-- RAG_CHUNK: bAddDamageClass -->
### bAddDamageClass

**Syntax:** `bonus2 bAddDamageClass,mid,x;`

**Effect:** +x% physical damage against monster mid

**Parameters:**
- `mid`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddDamageClass,mid,x;
```

---

<!-- RAG_CHUNK: bAddMagicDamageClass -->
### bAddMagicDamageClass

**Syntax:** `bonus2 bAddMagicDamageClass,mid,x;`

**Effect:** +x% magical damage against monster mid

**Parameters:**
- `mid`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddMagicDamageClass,mid,x;
```

---

<!-- RAG_CHUNK: bAddDefMonster -->
### bAddDefMonster

**Syntax:** `bonus2 bAddDefMonster,mid,x;`

**Effect:** +x% physical damage reduction against monster mid

**Parameters:**
- `mid`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddDefMonster,mid,x;
```

---

<!-- RAG_CHUNK: bAddMDefMonster -->
### bAddMDefMonster

**Syntax:** `bonus2 bAddMDefMonster,mid,x;`

**Effect:** +x% magical damage reduction against monster mid

**Parameters:**
- `mid`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddMDefMonster,mid,x;
```

---

<!-- RAG_CHUNK: bSubSkill -->
### bSubSkill

**Syntax:** `bonus2 bSubSkill,sk,n;`

**Effect:** Reduces n% damage received from skill sk

**Parameters:**
- `sk`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSubSkill,sk,n;
```

---

<!-- RAG_CHUNK: bAbsorbDmgMaxHP -->
### bAbsorbDmgMaxHP

**Syntax:** `bonus bAbsorbDmgMaxHP,n;`

**Effect:** If the damage received is more than n% of Max HP, the damage received is [TotalDamage] - [n% of MaxHP] (Doesn't stack, will use the highest value) (Legacy rAthena behavior)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAbsorbDmgMaxHP,n;
```

---

<!-- RAG_CHUNK: bAbsorbDmgMaxHP2 -->
### bAbsorbDmgMaxHP2

**Syntax:** `bonus bAbsorbDmgMaxHP2,n;`

**Effect:** If the damage received is more than n% of Max HP, the damage received is reduced to n% of MaxHP (Doesn't stack, will use the highest value) (Official behavior)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAbsorbDmgMaxHP2,n;
```

---

<!-- RAG_CHUNK: bMagicAtkEle -->
### bMagicAtkEle

**Syntax:** `bonus2 bMagicAtkEle,e,x;`

**Effect:** Increases damage of e element magic by x%

**Parameters:**
- `e`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bMagicAtkEle,e,x;
```

---

<!-- RAG_CHUNK: bSetDefRace -->
### bSetDefRace

**Syntax:** `bonus4 bSetDefRace,r,n,t,y;`

**Effect:** Set DEF to y of an enemy of race r at n% for t milliseconds with normal attack

**Parameters:**
- `r`
- `n`
- `t`
- `y`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus4 bSetDefRace,r,n,t,y;
```

---

<!-- RAG_CHUNK: bSetMDefRace -->
### bSetMDefRace

**Syntax:** `bonus4 bSetMDefRace,r,n,t,y;`

**Effect:** Set MDEF to y of an enemy of race r at n% for t milliseconds with normal attack

**Parameters:**
- `r`
- `n`
- `t`
- `y`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus4 bSetMDefRace,r,n,t,y;
```

---

<!-- RAG_CHUNK: bIgnoreMDefRace -->
### bIgnoreMDefRace

**Syntax:** `bonus bIgnoreMDefRace,r;`

**Effect:** Disregard MDEF against enemies of race r

**Parameters:**
- `r`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bIgnoreMDefRace,r;
```

---

<!-- RAG_CHUNK: bIgnoreMdefRaceRate -->
### bIgnoreMdefRaceRate

**Syntax:** `bonus2 bIgnoreMdefRaceRate,r,n;`

**Effect:** Disregard n% of the target's MDEF if the target belongs to race r

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bIgnoreMdefRaceRate,r,n;
```

---

<!-- RAG_CHUNK: bIgnoreMdefRace2Rate -->
### bIgnoreMdefRace2Rate

**Syntax:** `bonus2 bIgnoreMdefRace2Rate,mr,n;`

**Effect:** Disregard n% of the target's MDEF if the target belongs to monster race mr

**Parameters:**
- `mr`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bIgnoreMdefRace2Rate,mr,n;
```

---

<!-- RAG_CHUNK: bIgnoreMDefEle -->
### bIgnoreMDefEle

**Syntax:** `bonus bIgnoreMDefEle,e;`

**Effect:** Disregard MDEF against enemies of element e

**Parameters:**
- `e`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bIgnoreMDefEle,e;
```

---

<!-- RAG_CHUNK: bIgnoreMdefClassRate -->
### bIgnoreMdefClassRate

**Syntax:** `bonus2 bIgnoreMdefClassRate,c,n;`

**Effect:** Disregard n% of the target's MDEF if the target belongs to class c

**Parameters:**
- `c`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bIgnoreMdefClassRate,c,n;
```

---

<!-- RAG_CHUNK: bIgnoreResRaceRate -->
### bIgnoreResRaceRate

**Syntax:** `bonus2 bIgnoreResRaceRate,r,n;`

**Effect:** Disregard n% of the target's Res if the target belongs to race r

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bIgnoreResRaceRate,r,n;
```

---

<!-- RAG_CHUNK: bIgnoreMResRaceRate -->
### bIgnoreMResRaceRate

**Syntax:** `bonus2 bIgnoreMResRaceRate,r,n;`

**Effect:** Disregard n% of the target's MRes if the target belongs to race r

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bIgnoreMResRaceRate,r,n;
```

---

<!-- RAG_CHUNK: bHPDrainValue -->
### bHPDrainValue

**Syntax:** `bonus bHPDrainValue,n;`

**Effect:** Heals +n HP with a normal attack

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bHPDrainValue,n;
```

---

<!-- RAG_CHUNK: bHPDrainValueRace -->
### bHPDrainValueRace

**Syntax:** `bonus2 bHPDrainValueRace,r,n;`

**Effect:** Heals +n HP when attacking a monster of race r with normal attack

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bHPDrainValueRace,r,n;
```

---

<!-- RAG_CHUNK: bHpDrainValueClass -->
### bHpDrainValueClass

**Syntax:** `bonus2 bHpDrainValueClass,c,n;`

**Effect:** Heals +n HP when attacking a monster of class c with normal attack

**Parameters:**
- `c`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bHpDrainValueClass,c,n;
```

---

<!-- RAG_CHUNK: bSPDrainValue -->
### bSPDrainValue

**Syntax:** `bonus bSPDrainValue,n;`

**Effect:** Heals +n SP with a normal attack

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bSPDrainValue,n;
```

---

<!-- RAG_CHUNK: bSPDrainValueRace -->
### bSPDrainValueRace

**Syntax:** `bonus2 bSPDrainValueRace,r,n;`

**Effect:** Heals +n SP when attacking a monster of race r with normal attack

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSPDrainValueRace,r,n;
```

---

<!-- RAG_CHUNK: bSpDrainValueClass -->
### bSpDrainValueClass

**Syntax:** `bonus2 bSpDrainValueClass,c,n;`

**Effect:** Heals +n SP when attacking a monster of class c with normal attack

**Parameters:**
- `c`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSpDrainValueClass,c,n;
```

---

<!-- RAG_CHUNK: bHPDrainRate -->
### bHPDrainRate

**Syntax:** `bonus2 bHPDrainRate,x,n;`

**Effect:** Adds a x/10% chance to drain n% HP from inflicted damage when attacking

**Parameters:**
- `x`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bHPDrainRate,x,n;
```

---

<!-- RAG_CHUNK: bSPDrainRate -->
### bSPDrainRate

**Syntax:** `bonus2 bSPDrainRate,x,n;`

**Effect:** Adds a x/10% chance to drain n% SP from inflicted damage when attacking

**Parameters:**
- `x`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSPDrainRate,x,n;
```

---

<!-- RAG_CHUNK: bHPVanishRate -->
### bHPVanishRate

**Syntax:** `bonus2 bHPVanishRate,x,n;`

**Effect:** Add a x/10% chance of decreasing enemy's HP amount by n% with a normal attack

**Parameters:**
- `x`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bHPVanishRate,x,n;
```

---

<!-- RAG_CHUNK: bHPVanishRaceRate -->
### bHPVanishRaceRate

**Syntax:** `bonus3 bHPVanishRaceRate,r,x,n;`

**Effect:** Add a x/10% chance of decreasing enemy's HP amount by n% when attacking, depends on enemy race r

**Parameters:**
- `r`
- `x`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bHPVanishRaceRate,r,x,n;
```

---

<!-- RAG_CHUNK: bHPVanishRate -->
### bHPVanishRate

**Syntax:** `bonus3 bHPVanishRate,x,n,bf;`

**Effect:** Add a x/10% chance of decreasing enemy's HP amount by n% when attacking with trigger criteria bf

**Parameters:**
- `x`
- `n`
- `bf`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bHPVanishRate,x,n,bf;
```

---

<!-- RAG_CHUNK: bSPVanishRate -->
### bSPVanishRate

**Syntax:** `bonus2 bSPVanishRate,x,n;`

**Effect:** Add a x/10% chance of decreasing enemy's SP amount by n% with a normal attack

**Parameters:**
- `x`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSPVanishRate,x,n;
```

---

<!-- RAG_CHUNK: bSPVanishRaceRate -->
### bSPVanishRaceRate

**Syntax:** `bonus3 bSPVanishRaceRate,r,x,n;`

**Effect:** Add a x/10% chance of decreasing enemy's SP amount by n% when attacking, depends on enemy race r

**Parameters:**
- `r`
- `x`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bSPVanishRaceRate,r,x,n;
```

---

<!-- RAG_CHUNK: bSPVanishRate -->
### bSPVanishRate

**Syntax:** `bonus3 bSPVanishRate,x,n,bf;`

**Effect:** Add a x/10% chance of decreasing enemy's SP amount by n% when attacking with trigger criteria bf

**Parameters:**
- `x`
- `n`
- `bf`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bSPVanishRate,x,n,bf;
```

---

<!-- RAG_CHUNK: bHPGainValue -->
### bHPGainValue

**Syntax:** `bonus bHPGainValue,n;`

**Effect:** Heals +n HP when killing an enemy with a melee-physical attack

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bHPGainValue,n;
```

---

<!-- RAG_CHUNK: bSPGainValue -->
### bSPGainValue

**Syntax:** `bonus bSPGainValue,n;`

**Effect:** Heals +n SP when killing an enemy with a melee-physical attack

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bSPGainValue,n;
```

---

<!-- RAG_CHUNK: bSPGainRace -->
### bSPGainRace

**Syntax:** `bonus2 bSPGainRace,r,n;`

**Effect:** Heals +n SP when killing an enemy of race r with a melee-physical attack

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bSPGainRace,r,n;
```

---

<!-- RAG_CHUNK: bLongHPGainValue -->
### bLongHPGainValue

**Syntax:** `bonus bLongHPGainValue,n;`

**Effect:** Heals +n HP when killing an enemy with a range-physical attack

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bLongHPGainValue,n;
```

---

<!-- RAG_CHUNK: bLongSPGainValue -->
### bLongSPGainValue

**Syntax:** `bonus bLongSPGainValue,n;`

**Effect:** Heals +n SP when killing an enemy with a range-physical attack

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bLongSPGainValue,n;
```

---

<!-- RAG_CHUNK: bMagicHPGainValue -->
### bMagicHPGainValue

**Syntax:** `bonus bMagicHPGainValue,n;`

**Effect:** Heals +n HP when killing an enemy with a magical attack

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMagicHPGainValue,n;
```

---

<!-- RAG_CHUNK: bMagicSPGainValue -->
### bMagicSPGainValue

**Syntax:** `bonus bMagicSPGainValue,n;`

**Effect:** Heals +n SP when killing an enemy with a magical attack

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMagicSPGainValue,n;
```

---

<!-- RAG_CHUNK: bShortWeaponDamageReturn -->
### bShortWeaponDamageReturn

**Syntax:** `bonus bShortWeaponDamageReturn,n;`

**Effect:** Reflects n% of received melee damage back to the enemy that caused it

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bShortWeaponDamageReturn,n;
```

---

<!-- RAG_CHUNK: bLongWeaponDamageReturn -->
### bLongWeaponDamageReturn

**Syntax:** `bonus bLongWeaponDamageReturn,n;`

**Effect:** Reflects n% of received ranged damage back to the enemy that caused it

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bLongWeaponDamageReturn,n;
```

---

<!-- RAG_CHUNK: bMagicDamageReturn -->
### bMagicDamageReturn

**Syntax:** `bonus bMagicDamageReturn,n;`

**Effect:** Adds a n% chance to reflect targetted magic spells back to the enemy that caused it

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bMagicDamageReturn,n;
```

---

<!-- RAG_CHUNK: bReduceDamageReturn -->
### bReduceDamageReturn

**Syntax:** `bonus bReduceDamageReturn,n;`

**Effect:** Reduces reflected damage (melee/ranged/magic) by n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bReduceDamageReturn,n;
```

---

<!-- RAG_CHUNK: bUnstripableWeapon -->
### bUnstripableWeapon

**Syntax:** `bonus bUnstripableWeapon,Weapon cannot be taken off via Strip skills;`

**Parameters:**
- `Weapon cannot be taken off via Strip skills`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bUnstripableWeapon,Weapon cannot be taken off via Strip skills;
```

---

<!-- RAG_CHUNK: bUnstripableArmor -->
### bUnstripableArmor

**Syntax:** `bonus bUnstripableArmor,Armor cannot be taken off via Strip skills;`

**Parameters:**
- `Armor cannot be taken off via Strip skills`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bUnstripableArmor,Armor cannot be taken off via Strip skills;
```

---

<!-- RAG_CHUNK: bUnstripableHelm -->
### bUnstripableHelm

**Syntax:** `bonus bUnstripableHelm,Helm cannot be taken off via Strip skills;`

**Parameters:**
- `Helm cannot be taken off via Strip skills`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bUnstripableHelm,Helm cannot be taken off via Strip skills;
```

---

<!-- RAG_CHUNK: bUnstripableShield -->
### bUnstripableShield

**Syntax:** `bonus bUnstripableShield,Shield cannot be taken off via Strip skills;`

**Parameters:**
- `Shield cannot be taken off via Strip skills`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bUnstripableShield,Shield cannot be taken off via Strip skills;
```

---

<!-- RAG_CHUNK: bUnstripable -->
### bUnstripable

**Syntax:** `bonus bUnstripable,All equipment cannot be taken off via strip skills;`

**Parameters:**
- `All equipment cannot be taken off via strip skills`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bUnstripable,All equipment cannot be taken off via strip skills;
```

---

<!-- RAG_CHUNK: bUnbreakableGarment -->
### bUnbreakableGarment

**Syntax:** `bonus bUnbreakableGarment,Garment cannot be damaged/broken by any means;`

**Parameters:**
- `Garment cannot be damaged/broken by any means`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bUnbreakableGarment,Garment cannot be damaged/broken by any means;
```

---

<!-- RAG_CHUNK: bUnbreakableWeapon -->
### bUnbreakableWeapon

**Syntax:** `bonus bUnbreakableWeapon,Weapon cannot be damaged/broken by any means;`

**Parameters:**
- `Weapon cannot be damaged/broken by any means`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bUnbreakableWeapon,Weapon cannot be damaged/broken by any means;
```

---

<!-- RAG_CHUNK: bUnbreakableArmor -->
### bUnbreakableArmor

**Syntax:** `bonus bUnbreakableArmor,Armor cannot be damaged/broken by any means;`

**Parameters:**
- `Armor cannot be damaged/broken by any means`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bUnbreakableArmor,Armor cannot be damaged/broken by any means;
```

---

<!-- RAG_CHUNK: bUnbreakableHelm -->
### bUnbreakableHelm

**Syntax:** `bonus bUnbreakableHelm,Helm cannot be damaged/broken by any means;`

**Parameters:**
- `Helm cannot be damaged/broken by any means`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bUnbreakableHelm,Helm cannot be damaged/broken by any means;
```

---

<!-- RAG_CHUNK: bUnbreakableShield -->
### bUnbreakableShield

**Syntax:** `bonus bUnbreakableShield,Shield cannot be damaged/broken by any means;`

**Parameters:**
- `Shield cannot be damaged/broken by any means`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bUnbreakableShield,Shield cannot be damaged/broken by any means;
```

---

<!-- RAG_CHUNK: bUnbreakableShoes -->
### bUnbreakableShoes

**Syntax:** `bonus bUnbreakableShoes,Shoes cannot be damaged/broken by any means;`

**Parameters:**
- `Shoes cannot be damaged/broken by any means`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bUnbreakableShoes,Shoes cannot be damaged/broken by any means;
```

---

<!-- RAG_CHUNK: bUnbreakable -->
### bUnbreakable

**Syntax:** `bonus bUnbreakable,n;`

**Effect:** Reduces the break chance of all equipped equipment by n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bUnbreakable,n;
```

---

<!-- RAG_CHUNK: bBreakWeaponRate -->
### bBreakWeaponRate

**Syntax:** `bonus bBreakWeaponRate,n;`

**Effect:** Adds a n/100% chance to break enemy's weapon while attacking (stacks with other break chances)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bBreakWeaponRate,n;
```

---

<!-- RAG_CHUNK: bBreakArmorRate -->
### bBreakArmorRate

**Syntax:** `bonus bBreakArmorRate,n;`

**Effect:** Adds a n/100% chance to break enemy's armor while attacking (stacks with other break chances)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bBreakArmorRate,n;
```

---

<!-- RAG_CHUNK: bDropAddRace -->
### bDropAddRace

**Syntax:** `bonus2 bDropAddRace,r,x;`

**Effect:** Adds x% to player's drop rate when killing a monster with race r.

**Parameters:**
- `r`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bDropAddRace,r,x;
```

---

<!-- RAG_CHUNK: bDropAddClass -->
### bDropAddClass

**Syntax:** `bonus2 bDropAddClass,c,x;`

**Effect:** Adds x% to player's drop rate when killing a monster with class c.

**Parameters:**
- `c`
- `x`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bDropAddClass,c,x;
```

---

<!-- RAG_CHUNK: bAddMonsterIdDropItem -->
### bAddMonsterIdDropItem

**Syntax:** `bonus3 bAddMonsterIdDropItem,iid,mid,n;`

**Effect:** Adds a n/100% chance of dropping item iid when killing monster mid

**Parameters:**
- `iid`
- `mid`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bAddMonsterIdDropItem,iid,mid,n;
```

---

<!-- RAG_CHUNK: bAddMonsterDropItem -->
### bAddMonsterDropItem

**Syntax:** `bonus2 bAddMonsterDropItem,iid,n;`

**Effect:** Adds a n/100% chance for item iid to be dropped when killing a monster

**Parameters:**
- `iid`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddMonsterDropItem,iid,n;
```

---

<!-- RAG_CHUNK: bAddMonsterDropItem -->
### bAddMonsterDropItem

**Syntax:** `bonus3 bAddMonsterDropItem,iid,r,n;`

**Effect:** Adds a n/100% chance for item iid to be dropped when killing a monster of race r

**Parameters:**
- `iid`
- `r`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bAddMonsterDropItem,iid,r,n;
```

---

<!-- RAG_CHUNK: bAddMonsterDropItemGroup -->
### bAddMonsterDropItemGroup

**Syntax:** `bonus2 bAddMonsterDropItemGroup,ig,n;`

**Effect:** Adds a n/100% chance to get an item of group type ig when killing a monster

**Parameters:**
- `ig`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddMonsterDropItemGroup,ig,n;
```

---

<!-- RAG_CHUNK: bAddMonsterDropItemGroup -->
### bAddMonsterDropItemGroup

**Syntax:** `bonus3 bAddMonsterDropItemGroup,ig,r,n;`

**Effect:** Adds a n/100% chance to get an item of group type ig when killing a monster of race r

**Parameters:**
- `ig`
- `r`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus3 bAddMonsterDropItemGroup,ig,r,n;
```

---

<!-- RAG_CHUNK: bGetZenyNum -->
### bGetZenyNum

**Syntax:** `bonus2 bGetZenyNum,x,n;`

**Effect:** Adds a n% chance of gaining 1~x zeny when killing a monster (only the highest among all is applied)

**Parameters:**
- `x`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bGetZenyNum,x,n;
```

---

<!-- RAG_CHUNK: bAddGetZenyNum -->
### bAddGetZenyNum

**Syntax:** `bonus2 bAddGetZenyNum,x,n;`

**Effect:** Adds a n% chance of gaining 1~x zeny when killing a monster

**Parameters:**
- `x`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddGetZenyNum,x,n;
```

---

<!-- RAG_CHUNK: bDoubleRate -->
### bDoubleRate

**Syntax:** `bonus bDoubleRate,n;`

**Effect:** Double Attack probability n% (works with all weapons | only the highest among all is applied)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bDoubleRate,n;
```

---

<!-- RAG_CHUNK: bDoubleAddRate -->
### bDoubleAddRate

**Syntax:** `bonus bDoubleAddRate,n;`

**Effect:** Double Attack probability + n% (works with all weapons)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bDoubleAddRate,n;
```

---

<!-- RAG_CHUNK: bAddSkillBlow -->
### bAddSkillBlow

**Syntax:** `bonus2 bAddSkillBlow,sk,n;`

**Effect:** Knock back the target by n cells when using skill sk

**Parameters:**
- `sk`
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus2 bAddSkillBlow,sk,n;
```

---

<!-- RAG_CHUNK: bNoKnockback -->
### bNoKnockback

**Syntax:** `bonus bNoKnockback,Character is no longer knocked back by enemy skills with such effect;`

**Parameters:**
- `Character is no longer knocked back by enemy skills with such effect`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bNoKnockback,Character is no longer knocked back by enemy skills with such effect;
```

---

<!-- RAG_CHUNK: bNoGemStone -->
### bNoGemStone

**Syntax:** `bonus bNoGemStone,Skills requiring Gemstones do not require them;`

**Parameters:**
- `Skills requiring Gemstones do not require them`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bNoGemStone,Skills requiring Gemstones do not require them;
```

---

<!-- RAG_CHUNK: bPerfectHide -->
### bPerfectHide

**Syntax:** `bonus bPerfectHide,Hidden/cloaked character is no longer detected by monsters with 'detector' mode;`

**Parameters:**
- `Hidden/cloaked character is no longer detected by monsters with 'detector' mode`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bPerfectHide,Hidden/cloaked character is no longer detected by monsters with 'detector' mode;
```

---

<!-- RAG_CHUNK: bClassChange -->
### bClassChange

**Syntax:** `bonus bClassChange,n;`

**Effect:** Gives a n/100% chance to change the attacked monster's class with normal attack

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bClassChange,n;
```

---

<!-- RAG_CHUNK: bAddStealRate -->
### bAddStealRate

**Syntax:** `bonus bAddStealRate,n;`

**Effect:** Increases success rate of Steal skill by n/100%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bAddStealRate,n;
```

---

<!-- RAG_CHUNK: bNoMadoFuel -->
### bNoMadoFuel

**Syntax:** `bonus bNoMadoFuel,Nullify Magic Gear Fuel requirement for skills.;`

**Parameters:**
- `Nullify Magic Gear Fuel requirement for skills.`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bNoMadoFuel,Nullify Magic Gear Fuel requirement for skills.;
```

---

<!-- RAG_CHUNK: bNoWalkDelay -->
### bNoWalkDelay

**Syntax:** `bonus bNoWalkDelay,Give infinite Endure.;`

**Parameters:**
- `Give infinite Endure.`

**Example:**
```yml
# In item_db.yml Script field
Script: |
  bonus bNoWalkDelay,Give infinite Endure.;
```

---


# ═══════════════════════════════════════════════════════════════
# PART 3: GAME MECHANICS + DATABASE SCHEMAS
# ═══════════════════════════════════════════════════════════════


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
