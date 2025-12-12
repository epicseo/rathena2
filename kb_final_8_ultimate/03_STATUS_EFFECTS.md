# rAthena KB v5 - Status Effects Complete Reference

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

<!-- RAG_CHUNK: 03_SC_STONE -->

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

<!-- RAG_CHUNK: 03_SC_FREEZE -->

**Effect:** DEF -50%; FLEE = 0; MDEF +25%; ignore Steal, Lex Aeterna, Storm Gust, Falling Ice Pillar; change element to Water Lv 1; can't move/attack/pick item/use item/sit/logout

**Script Example:**
```c
sc_start SC_FREEZE, 60000, 1;
```

---

### SC_STUN

<!-- RAG_CHUNK: 03_SC_STUN -->

**Effect:** FLEE = 0; can't move/attack/pick item/use item/use skill/sit/logout

**Script Example:**
```c
sc_start SC_STUN, 60000, 1;
```

---

### SC_SLEEP

<!-- RAG_CHUNK: 03_SC_SLEEP -->

**Effect:** FLEE = 0; enemy CRIT x2; can't move/attack/pick item/use item/use skill/sit/logout

**Script Example:**
```c
sc_start SC_SLEEP, 60000, 1;
```

---

### SC_POISON

<!-- RAG_CHUNK: 03_SC_POISON -->

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

<!-- RAG_CHUNK: 03_SC_CURSE -->

**Effect:** ATK-25%; LUK = 0; Movement speed -300

**Script Example:**
```c
sc_start SC_CURSE, 60000, 1;
```

---

### SC_SILENCE

<!-- RAG_CHUNK: 03_SC_SILENCE -->

**Effect:** Can't use active skills

**Script Example:**
```c
sc_start SC_SILENCE, 60000, 1;
```

---

### SC_CONFUSION

<!-- RAG_CHUNK: 03_SC_CONFUSION -->

**Effect:** Move randomly; Set DEF to (STR+(INT*50))

**Script Example:**
```c
sc_start SC_CONFUSION, 60000, 1;
```

---

### SC_BLIND

<!-- RAG_CHUNK: 03_SC_BLIND -->

**Effect:** HIT -25%; FLEE -25%; Black out the outter part of the screen

**Script Example:**
```c
sc_start SC_BLIND, 60000, 1;
```

---

### SC_BLEEDING

<!-- RAG_CHUNK: 03_SC_BLEEDING -->

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

<!-- RAG_CHUNK: 03_SC_DPOISON -->

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

<!-- RAG_CHUNK: 03_SC_PROVOKE -->

**Icon (EFST):** `EFST_PROVOKE`

**Effect:** Decrease DEF by (5+(5*Skill Lv))%; Increase ATK by (2+(3*Skill lv))%

**Script Example:**
```c
sc_start SC_PROVOKE, 60000, 1;
```

---

### SC_ENDURE

<!-- RAG_CHUNK: 03_SC_ENDURE -->

**Icon (EFST):** `EFST_ENDURE`

**Effect:** Increase MDEF by (Skill Lv); Doesn't get flinched when attacked

**Script Example:**
```c
sc_start SC_ENDURE, 60000, 1;
```

---

### SC_TWOHANDQUICKEN

<!-- RAG_CHUNK: 03_SC_TWOHANDQUICKEN -->

**Icon (EFST):** `EFST_TWOHANDQUICKEN`

**Effect:** ASPD +30%

**Script Example:**
```c
sc_start SC_TWOHANDQUICKEN, 60000, 1;
```

---

### SC_CONCENTRATE

<!-- RAG_CHUNK: 03_SC_CONCENTRATE -->

**Icon (EFST):** `EFST_CONCENTRATION`

**Effect:** Increase AGI by (2+Skill Lv)%; Increase DEX by (2+Skill Lv)%; Reveal hidden enemies in 3x3 area around caster

**Script Example:**
```c
sc_start SC_CONCENTRATE, 60000, 1;
```

---

### SC_HIDING

<!-- RAG_CHUNK: 03_SC_HIDING -->

**Icon (EFST):** `EFST_HIDING`

**Effect:** Set OPTION_HIDE

**Script Example:**
```c
sc_start SC_HIDING, 60000, 1;
```

---

### SC_CLOAKING

<!-- RAG_CHUNK: 03_SC_CLOAKING -->

**Icon (EFST):** `EFST_CLOAKING`

**Effect:** Set OPTION_CLOAK

**Script Example:**
```c
sc_start SC_CLOAKING, 60000, 1;
```

---

### SC_ENCPOISON

<!-- RAG_CHUNK: 03_SC_ENCPOISON -->

**Icon (EFST):** `EFST_ENCHANTPOISON`

**Effect:** Change weapon element to ELE_POISON; Poisoning chance is (2.5+0.5%)

**Script Example:**
```c
sc_start SC_ENCPOISON, 60000, 1;
```

---

### SC_POISONREACT

<!-- RAG_CHUNK: 03_SC_POISONREACT -->

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

<!-- RAG_CHUNK: 03_SC_QUAGMIRE -->

**Icon (EFST):** `EFST_QUAGMIRE`

**Effect:** Removes Increase AGI, Twhohand Quicken, Wind Walk, Adrenaline Rush, Attention Concentrate, Cart Boost, True Sight, Magnetic Field & Onehand Quicken skill effect; Movement Speed -50; Decrease AGI & DEX by (10*Skill Lv) but can't below 75% for players and 50% for mobs

**Script Example:**
```c
sc_start SC_QUAGMIRE, 60000, 1;
```

---

### SC_ANGELUS

<!-- RAG_CHUNK: 03_SC_ANGELUS -->

**Icon (EFST):** `EFST_ANGELUS`

**Effect:** Increase DEF by (5*Skill Lv)%

**Script Example:**
```c
sc_start SC_ANGELUS, 60000, 1;
```

---

### SC_BLESSING

<!-- RAG_CHUNK: 03_SC_BLESSING -->

**Icon (EFST):** `EFST_BLESSING`

**Effect:** Increase STR, DEX & INT by (Skill Lv); Removes Stone and Curse status. If used on mobs will reduce their DEX and INT by 50%

**Script Example:**
```c
sc_start SC_BLESSING, 60000, 1;
```

---

### SC_SIGNUMCRUCIS

<!-- RAG_CHUNK: 03_SC_SIGNUMCRUCIS -->

**Icon (EFST):** `EFST_CRUCIS`

**Effect:** Decrease DEF of Undead and Demon mobs by (10+(4*Skill Lv))% on screen

**Script Example:**
```c
sc_start SC_SIGNUMCRUCIS, 60000, 1;
```

---

### SC_INCREASEAGI

<!-- RAG_CHUNK: 03_SC_INCREASEAGI -->

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

<!-- RAG_CHUNK: 03_SC_DECREASEAGI -->

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

<!-- RAG_CHUNK: 03_SC_SLOWPOISON -->

**Icon (EFST):** `EFST_SLOWPOISON`

**Effect:** Stop the HP reduction of SC_POISON

**Script Example:**
```c
sc_start SC_SLOWPOISON, 60000, 1;
```

---

### SC_IMPOSITIO

<!-- RAG_CHUNK: 03_SC_IMPOSITIO -->

**Icon (EFST):** `EFST_IMPOSITIO`

**Effect:** Increase ATK by (5*Skill Lv)

**Script Example:**
```c
sc_start SC_IMPOSITIO, 60000, 1;
```

---

### SC_SUFFRAGIUM

<!-- RAG_CHUNK: 03_SC_SUFFRAGIUM -->

**Icon (EFST):** `EFST_SUFFRAGIUM`

**Effect:** Cast time decreased by (15*Skill Lv)%

**Script Example:**
```c
sc_start SC_SUFFRAGIUM, 60000, 1;
```

---

### SC_ASPERSIO

<!-- RAG_CHUNK: 03_SC_ASPERSIO -->

**Icon (EFST):** `EFST_ASPERSIO`

**Effect:** Change weapon element to ELE_HOLY

**Script Example:**
```c
sc_start SC_ASPERSIO, 60000, 1;
```

---

### SC_BENEDICTIO

<!-- RAG_CHUNK: 03_SC_BENEDICTIO -->

**Icon (EFST):** `EFST_BENEDICTIO`

**Effect:** Change armor element to ELE_HOLY

**Script Example:**
```c
sc_start SC_BENEDICTIO, 60000, 1;
```

---

### SC_KYRIE

<!-- RAG_CHUNK: 03_SC_KYRIE -->

**Icon (EFST):** `EFST_KYRIE`

**Effect:** Remove SC_ASSUMPTIO skill effect; Block damage with a total of (MaxHP*(Skill Lv*2+10)/100) or ((Skill Lv/2)+5) times

**Script Example:**
```c
sc_start SC_KYRIE, 60000, 1;
```

---

### SC_MAGNIFICAT

<!-- RAG_CHUNK: 03_SC_MAGNIFICAT -->

**Icon (EFST):** `EFST_MAGNIFICAT`

**Effect:** SP Regeneration speed x2

**Script Example:**
```c
sc_start SC_MAGNIFICAT, 60000, 1;
```

---

### SC_GLORIA

<!-- RAG_CHUNK: 03_SC_GLORIA -->

**Icon (EFST):** `EFST_GLORIA`

**Effect:** LUK +30

**Script Example:**
```c
sc_start SC_GLORIA, 60000, 1;
```

---

### SC_AETERNA

<!-- RAG_CHUNK: 03_SC_AETERNA -->

**Icon (EFST):** `EFST_LEXAETERNA`

**Effect:** Damaged received x2

**Script Example:**
```c
sc_start SC_AETERNA, 60000, 1;
```

---

### SC_ADRENALINE

<!-- RAG_CHUNK: 03_SC_ADRENALINE -->

**Icon (EFST):** `EFST_ADRENALINE`

**Effect:** ASPD of Axe & Mace weapons x2

**Script Example:**
```c
sc_start SC_ADRENALINE, 60000, 1;
```

---

### SC_WEAPONPERFECTION

<!-- RAG_CHUNK: 03_SC_WEAPONPERFECTION -->

**Icon (EFST):** `EFST_WEAPONPERFECT`

**Effect:** Ignore damage reduction to any monster size

**Script Example:**
```c
sc_start SC_WEAPONPERFECTION, 60000, 1;
```

---

### SC_OVERTHRUST

<!-- RAG_CHUNK: 03_SC_OVERTHRUST -->

**Icon (EFST):** `EFST_OVERTHRUST`

**Effect:** Increase ATK by (5*Skill Lv)%; Add a 0.1% of breaking the equipped weapon [except Axes, Maces & Unbreakable weapons]

**Script Example:**
```c
sc_start SC_OVERTHRUST, 60000, 1;
```

---

### SC_MAXIMIZEPOWER

<!-- RAG_CHUNK: 03_SC_MAXIMIZEPOWER -->

**Icon (EFST):** `EFST_MAXIMIZE`

**Effect:** SP Regeneration is disabled; Damage dealt is always the max damage

**Script Example:**
```c
sc_start SC_MAXIMIZEPOWER, 60000, 1;
```

---

### SC_TRICKDEAD

<!-- RAG_CHUNK: 03_SC_TRICKDEAD -->

**Icon (EFST):** `EFST_TRICKDEAD`

**Effect:** HP & SP Regeneration is disabled; Remove SC_DANCING

**Script Example:**
```c
sc_start SC_TRICKDEAD, 60000, 1;
```

---

### SC_LOUD

<!-- RAG_CHUNK: 03_SC_LOUD -->

**Icon (EFST):** `EFST_SHOUT`

**Effect:** STR +4

**Script Example:**
```c
sc_start SC_LOUD, 60000, 1;
```

---

### SC_ENERGYCOAT

<!-- RAG_CHUNK: 03_SC_ENERGYCOAT -->

**Icon (EFST):** `EFST_ENERGYCOAT`

**Effect:** Reduce damage received according to current MaxSP %

**Script Example:**
```c
sc_start SC_ENERGYCOAT, 60000, 1;
```

---

### SC_BROKENARMOR

<!-- RAG_CHUNK: 03_SC_BROKENARMOR -->

**Icon (EFST):** `EFST_BROKENARMOR`

**Effect:** Shows EFST_BROKENARMOR status icon if the armor is broken

**Script Example:**
```c
sc_start SC_BROKENARMOR, 60000, 1;
```

---

### SC_BROKENWEAPON

<!-- RAG_CHUNK: 03_SC_BROKENWEAPON -->

**Icon (EFST):** `EFST_BROKENWEAPON`

**Effect:** Shows EFST_BROKENWEAPON status icon if the armor is broken

**Script Example:**
```c
sc_start SC_BROKENWEAPON, 60000, 1;
```

---

### SC_HALLUCINATION

<!-- RAG_CHUNK: 03_SC_HALLUCINATION -->

**Icon (EFST):** `EFST_ILLUSION`

**Effect:** The screen goes wavy and you see crazy numbers for all damage that is processed around you, but they are all fake. Even other players see those numbers at you.

**Script Example:**
```c
sc_start SC_HALLUCINATION, 60000, 1;
```

---

### SC_WEIGHT50

<!-- RAG_CHUNK: 03_SC_WEIGHT50 -->

**Icon (EFST):** `EFST_WEIGHTOVER50`

**Effect:** Shows EFST_WEIGHTOVER50 status icon if Weight >= 50%

**Script Example:**
```c
sc_start SC_WEIGHT50, 60000, 1;
```

---

### SC_WEIGHT90

<!-- RAG_CHUNK: 03_SC_WEIGHT90 -->

**Icon (EFST):** `EFST_WEIGHTOVER90`

**Effect:** Shows EFST_WEIGHTOVER90 status icon if Weight >= 90%

**Script Example:**
```c
sc_start SC_WEIGHT90, 60000, 1;
```

---

### SC_ASPDPOTION0

<!-- RAG_CHUNK: 03_SC_ASPDPOTION0 -->

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

<!-- RAG_CHUNK: 03_SC_ASPDPOTION1 -->

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

<!-- RAG_CHUNK: 03_SC_ASPDPOTION2 -->

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

<!-- RAG_CHUNK: 03_SC_ASPDPOTION3 -->

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

<!-- RAG_CHUNK: 03_SC_SPEEDUP0 -->

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

<!-- RAG_CHUNK: 03_SC_SPEEDUP1 -->

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

<!-- RAG_CHUNK: 03_SC_ATKPOTION -->

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

<!-- RAG_CHUNK: 03_SC_MATKPOTION -->

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

<!-- RAG_CHUNK: 03_SC_WEDDING -->

**Effect:** Set Movement Speed to 100; Call clif_changelook; Set OPTION_WEDDING

**Script Example:**
```c
sc_start SC_WEDDING, 60000, 1;
```

---

### SC_SLOWDOWN

<!-- RAG_CHUNK: 03_SC_SLOWDOWN -->

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

<!-- RAG_CHUNK: 03_SC_ANKLE -->

**Icon (EFST):** `EFST_ANKLESNARE`

**Effect:** Set DEF to (AGI*50); Can't move

**Script Example:**
```c
sc_start SC_ANKLE, 60000, 1;
```

---

### SC_KEEPING

<!-- RAG_CHUNK: 03_SC_KEEPING -->

**Effect:** Set DEF to 90

**Script Example:**
```c
sc_start SC_KEEPING, 60000, 1;
```

---

### SC_BARRIER

<!-- RAG_CHUNK: 03_SC_BARRIER -->

**Icon (EFST):** `EFST_BARRIER`

**Effect:** Set DEF to 100

**Script Example:**
```c
sc_start SC_BARRIER, 60000, 1;
```

---

### SC_STRIPWEAPON

<!-- RAG_CHUNK: 03_SC_STRIPWEAPON -->

**Icon (EFST):** `EFST_NOEQUIPWEAPON`

**Effect:** Unequip weapon; On mob ATK -25%

**Script Example:**
```c
sc_start SC_STRIPWEAPON, 60000, 1;
```

---

### SC_STRIPSHIELD

<!-- RAG_CHUNK: 03_SC_STRIPSHIELD -->

**Icon (EFST):** `EFST_NOEQUIPSHIELD`

**Effect:** Unequip shield; On mob DEF -15%

**Script Example:**
```c
sc_start SC_STRIPSHIELD, 60000, 1;
```

---

### SC_STRIPARMOR

<!-- RAG_CHUNK: 03_SC_STRIPARMOR -->

**Icon (EFST):** `EFST_NOEQUIPARMOR`

**Effect:** Unequip armor; On mob VIT -40%

**Script Example:**
```c
sc_start SC_STRIPARMOR, 60000, 1;
```

---

### SC_STRIPHELM

<!-- RAG_CHUNK: 03_SC_STRIPHELM -->

**Icon (EFST):** `EFST_NOEQUIPHELM`

**Effect:** Unequip helm; On mob INT -40%

**Script Example:**
```c
sc_start SC_STRIPHELM, 60000, 1;
```

---

### SC_CP_WEAPON

<!-- RAG_CHUNK: 03_SC_CP_WEAPON -->

**Icon (EFST):** `EFST_PROTECTWEAPON`

**Effect:** Protects equipped weapon from damage and strip skill

**Script Example:**
```c
sc_start SC_CP_WEAPON, 60000, 1;
```

---

### SC_CP_SHIELD

<!-- RAG_CHUNK: 03_SC_CP_SHIELD -->

**Icon (EFST):** `EFST_PROTECTSHIELD`

**Effect:** Protects equipped shield from damage and strip skill

**Script Example:**
```c
sc_start SC_CP_SHIELD, 60000, 1;
```

---

### SC_CP_ARMOR

<!-- RAG_CHUNK: 03_SC_CP_ARMOR -->

**Icon (EFST):** `EFST_PROTECTARMOR`

**Effect:** Protects equipped armor from damage and strip skill

**Script Example:**
```c
sc_start SC_CP_ARMOR, 60000, 1;
```

---

### SC_CP_HELM

<!-- RAG_CHUNK: 03_SC_CP_HELM -->

**Icon (EFST):** `EFST_PROTECTHELM`

**Effect:** Protects equipped helm from damage and strip skill

**Script Example:**
```c
sc_start SC_CP_HELM, 60000, 1;
```

---

### SC_AUTOGUARD

<!-- RAG_CHUNK: 03_SC_AUTOGUARD -->

**Icon (EFST):** `EFST_AUTOGUARD`

**Effect:** Blocks short and long range physical attacks at a certain chance, and stops the caster for 0.3 seconds if it's activated

**Script Example:**
```c
sc_start SC_AUTOGUARD, 60000, 1;
```

---

### SC_REFLECTSHIELD

<!-- RAG_CHUNK: 03_SC_REFLECTSHIELD -->

**Icon (EFST):** `EFST_REFLECTSHIELD`

**Effect:** Reflects (10+(3*Skill Lv))% of short ranged physical attack back to the attacker

**Script Example:**
```c
sc_start SC_REFLECTSHIELD, 60000, 1;
```

---

### SC_SPLASHER

<!-- RAG_CHUNK: 03_SC_SPLASHER -->

**Icon (EFST):** `EFST_SPLASHER`

**Effect:** This skill will only work once the target's HP is 1/3 or less of its Max HP. When struck by this skill, the target will explode and damage other enemies in it's vicinity

**Script Example:**
```c
sc_start SC_SPLASHER, 60000, 1;
```

---

### SC_PROVIDENCE

<!-- RAG_CHUNK: 03_SC_PROVIDENCE -->

**Icon (EFST):** `EFST_PROVIDENCE`

**Effect:** Increase party members' resistance to RC_Demon and Ele_Holy monsters

**Script Example:**
```c
sc_start SC_PROVIDENCE, 60000, 1;
```

---

### SC_DEFENDER

<!-- RAG_CHUNK: 03_SC_DEFENDER -->

**Icon (EFST):** `EFST_DEFENDER`

**Effect:** Decrease (5+(15*Skill Lv))% damage taken from long range attack; Decrease (25+(5*Skill Lv)) ASPD

**Script Example:**
```c
sc_start SC_DEFENDER, 60000, 1;
```

---

### SC_MAGICROD

<!-- RAG_CHUNK: 03_SC_MAGICROD -->

**Icon (EFST):** `EFST_MAGICROD`

**Effect:** Gain (Skill Lv*20)% of SP consumed by the skill used from enemy; Damage received becomes 0; Drain 20% of enemy's Max SP

**Script Example:**
```c
sc_start SC_MAGICROD, 60000, 1;
```

---

### SC_SPELLBREAKER

<!-- RAG_CHUNK: 03_SC_SPELLBREAKER -->

**Effect:** Gain SP used by enemy to cast the spell, and interrupt the magic cast. At lv 5, gain 1% from enemy max hp.

**Script Example:**
```c
sc_start SC_SPELLBREAKER, 60000, 1;
```

---

### SC_AUTOSPELL

<!-- RAG_CHUNK: 03_SC_AUTOSPELL -->

**Icon (EFST):** `EFST_AUTOSPELL`

**Effect:** Auto cast several learned magic spells by using 2/3 of SP cost of the skill, but only when attacking with physical attacks.

**Script Example:**
```c
sc_start SC_AUTOSPELL, 60000, 1;
```

---

### SC_SIGHTTRASHER

<!-- RAG_CHUNK: 03_SC_SIGHTTRASHER -->

**Effect:** (not exist)

**Script Example:**
```c
sc_start SC_SIGHTTRASHER, 60000, 1;
```

---

### SC_AUTOBERSERK

<!-- RAG_CHUNK: 03_SC_AUTOBERSERK -->

**Icon (EFST):** `EFST_AUTOBERSERK`

**Effect:** If HP<25%, set SC_PROVOKE lv 10 on self

**Script Example:**
```c
sc_start SC_AUTOBERSERK, 60000, 1;
```

---

### SC_SPEARQUICKEN

<!-- RAG_CHUNK: 03_SC_SPEARQUICKEN -->

**Icon (EFST):** `EFST_SPEARQUICKEN`

**Effect:** When using spear, +ASPD (20+(1*Skill Lv))%, +CRIT (3+(10*Skill Lv)), +FLEE (2*Skill Lv)

**Script Example:**
```c
sc_start SC_SPEARQUICKEN, 60000, 1;
```

---

### SC_AUTOCOUNTER

<!-- RAG_CHUNK: 03_SC_AUTOCOUNTER -->

**Icon (EFST):** `EFST_AUTOCOUNTER`

**Effect:** Hitrate +20%; If attacked by close range, automatically retaliate with crit*2

**Script Example:**
```c
sc_start SC_AUTOCOUNTER, 60000, 1;
```

---

### SC_SIGHT

<!-- RAG_CHUNK: 03_SC_SIGHT -->

**Effect:** Reveal hidden enemy on 3*3 range; Set OPTION_SIGHT

**Script Example:**
```c
sc_start SC_SIGHT, 60000, 1;
```

---

### SC_SAFETYWALL

<!-- RAG_CHUNK: 03_SC_SAFETYWALL -->

**Effect:** Block short ranged attack; Set OPTION_RUWACH

**Script Example:**
```c
sc_start SC_SAFETYWALL, 60000, 1;
```

---

### SC_RUWACH

<!-- RAG_CHUNK: 03_SC_RUWACH -->

**Effect:** Reveal hidden target and deal little damages if enemy is under SC_HIDING/SC_CLOAKING/SC_CAMOUFLAGE/SC_CLOAKINGEXCEED; Set OPTION_RUWACH

**Script Example:**
```c
sc_start SC_RUWACH, 60000, 1;
```

---

### SC_EXTREMITYFIST

<!-- RAG_CHUNK: 03_SC_EXTREMITYFIST -->

**Icon (EFST):** `EFST_EXTREMITYFIST`

**Effect:** Stop SP Regeneration by setting RGN_SP

**Script Example:**
```c
sc_start SC_EXTREMITYFIST, 60000, 1;
```

---

### SC_EXPLOSIONSPIRITS

<!-- RAG_CHUNK: 03_SC_EXPLOSIONSPIRITS -->

**Icon (EFST):** `EFST_EXPLOSIONSPIRITS`

**Effect:** Stop SP Regeneration by setting RGN_SP; +Crit

**Script Example:**
```c
sc_start SC_EXPLOSIONSPIRITS, 60000, 1;
```

---

### SC_COMBO

<!-- RAG_CHUNK: 03_SC_COMBO -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_COMBO, 60000, 1;
```

---

### SC_BLADESTOP_WAIT

<!-- RAG_CHUNK: 03_SC_BLADESTOP_WAIT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BLADESTOP_WAIT, 60000, 1;
```

---

### SC_BLADESTOP

<!-- RAG_CHUNK: 03_SC_BLADESTOP -->

**Icon (EFST):** `EFST_BLADESTOP`

**Effect:** Stops player and target; Set OPT3_BLADESTOP

**Script Example:**
```c
sc_start SC_BLADESTOP, 60000, 1;
```

---

### SC_FIREWEAPON

<!-- RAG_CHUNK: 03_SC_FIREWEAPON -->

**Icon (EFST):** `EFST_PROPERTYFIRE`

**Effect:** Change weapon element to Fire element

**Script Example:**
```c
sc_start SC_FIREWEAPON, 60000, 1;
```

---

### SC_WATERWEAPON

<!-- RAG_CHUNK: 03_SC_WATERWEAPON -->

**Icon (EFST):** `EFST_PROPERTYWATER`

**Effect:** Change weapon element to Water element

**Script Example:**
```c
sc_start SC_WATERWEAPON, 60000, 1;
```

---

### SC_WINDWEAPON

<!-- RAG_CHUNK: 03_SC_WINDWEAPON -->

**Icon (EFST):** `EFST_PROPERTYWIND`

**Effect:** Change weapon element to Wind element

**Script Example:**
```c
sc_start SC_WINDWEAPON, 60000, 1;
```

---

### SC_EARTHWEAPON

<!-- RAG_CHUNK: 03_SC_EARTHWEAPON -->

**Icon (EFST):** `EFST_PROPERTYGROUND`

**Effect:** Change weapon element to Earth element

**Script Example:**
```c
sc_start SC_EARTHWEAPON, 60000, 1;
```

---

### SC_VOLCANO

<!-- RAG_CHUNK: 03_SC_VOLCANO -->

**Icon (EFST):** `EFST_GROUNDMAGIC`

**Effect:** +watk of ELE_FIRE user

**Script Example:**
```c
sc_start SC_VOLCANO, 60000, 1;
```

---

### SC_DELUGE

<!-- RAG_CHUNK: 03_SC_DELUGE -->

**Icon (EFST):** `EFST_GROUNDMAGIC`

**Effect:** +Max HP of ELE_WATER user

**Script Example:**
```c
sc_start SC_DELUGE, 60000, 1;
```

---

### SC_VIOLENTGALE

<!-- RAG_CHUNK: 03_SC_VIOLENTGALE -->

**Icon (EFST):** `EFST_GROUNDMAGIC`

**Effect:** +FLEE of ELE_WIND user

**Script Example:**
```c
sc_start SC_VIOLENTGALE, 60000, 1;
```

---

### SC_WATK_ELEMENT

<!-- RAG_CHUNK: 03_SC_WATK_ELEMENT -->

**Effect:** Adds a percent of damage as an element

**Script Example:**
```c
sc_start SC_WATK_ELEMENT, 60000, 1;
```

---

### SC_ARMOR

<!-- RAG_CHUNK: 03_SC_ARMOR -->

**Effect:** Reduce damage received by 80 from long ranged weapon/misc attacks

**Script Example:**
```c
sc_start SC_ARMOR, 60000, 1;
```

---

### SC_ARMOR_ELEMENT

<!-- RAG_CHUNK: 03_SC_ARMOR_ELEMENT -->

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

<!-- RAG_CHUNK: 03_SC_NOCHAT -->

**Effect:** Can't chat, pick item, drop item

**Script Example:**
```c
sc_start SC_NOCHAT, 60000, 1;
```

---

### SC_BABY

<!-- RAG_CHUNK: 03_SC_BABY -->

**Icon (EFST):** `EFST_PROTECTEXP`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BABY, 60000, 1;
```

---

### SC_AURABLADE

<!-- RAG_CHUNK: 03_SC_AURABLADE -->

**Icon (EFST):** `EFST_AURABLADE`

**Effect:** Set OPT3_AURABLADE; Add damage by (20*Skill Lv) which ignore caster's accuracy rate/target's DEF

**Script Example:**
```c
sc_start SC_AURABLADE, 60000, 1;
```

---

### SC_PARRYING

<!-- RAG_CHUNK: 03_SC_PARRYING -->

**Icon (EFST):** `EFST_PARRYING`

**Effect:** Block using a 2H-Sword with chance (20+(3*Skill Lv))%

**Script Example:**
```c
sc_start SC_PARRYING, 60000, 1;
```

---

### SC_CONCENTRATION

<!-- RAG_CHUNK: 03_SC_CONCENTRATION -->

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

<!-- RAG_CHUNK: 03_SC_TENSIONRELAX -->

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

<!-- RAG_CHUNK: 03_SC_BERSERK -->

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

<!-- RAG_CHUNK: 03_SC_FURY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FURY, 60000, 1;
```

---

### SC_GOSPEL

<!-- RAG_CHUNK: 03_SC_GOSPEL -->

**Icon (EFST):** `EFST_GOSPEL`

**Effect:** Can't move; Gives a random status to party member and also enemy.

**Script Example:**
```c
sc_start SC_GOSPEL, 60000, 1;
```

---

### SC_ASSUMPTIO

<!-- RAG_CHUNK: 03_SC_ASSUMPTIO -->

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

<!-- RAG_CHUNK: 03_SC_BASILICA -->

**Effect:** Can't move; Can't use skill except the Basilica caster to cancel the basilica itself; Clear the skill area; Knockback enemy except Boss

**Script Example:**
```c
sc_start SC_BASILICA, 60000, 1;
```

---

### SC_GUILDAURA

<!-- RAG_CHUNK: 03_SC_GUILDAURA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GUILDAURA, 60000, 1;
```

---

### SC_MAGICPOWER

<!-- RAG_CHUNK: 03_SC_MAGICPOWER -->

**Icon (EFST):** `EFST_MAGICPOWER`

**Effect:** +MATK by (Skill Lv*5)% for the next magic skill that is cast

**Script Example:**
```c
sc_start SC_MAGICPOWER, 60000, 1;
```

---

### SC_EDP

<!-- RAG_CHUNK: 03_SC_EDP -->

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

<!-- RAG_CHUNK: 03_SC_TRUESIGHT -->

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

<!-- RAG_CHUNK: 03_SC_WINDWALK -->

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

<!-- RAG_CHUNK: 03_SC_MELTDOWN -->

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

<!-- RAG_CHUNK: 03_SC_CARTBOOST -->

**Icon (EFST):** `EFST_CARTBOOST`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CARTBOOST, 60000, 1;
```

---

### SC_CHASEWALK

<!-- RAG_CHUNK: 03_SC_CHASEWALK -->

**Icon (EFST):** `EFST_CHASEWALK`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CHASEWALK, 60000, 1;
```

---

### SC_REJECTSWORD

<!-- RAG_CHUNK: 03_SC_REJECTSWORD -->

**Icon (EFST):** `EFST_SWORDREJECT`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_REJECTSWORD, 60000, 1;
```

---

### SC_MARIONETTE

<!-- RAG_CHUNK: 03_SC_MARIONETTE -->

**Icon (EFST):** `EFST_MARIONETTE_MASTER`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MARIONETTE, 60000, 1;
```

---

### SC_MARIONETTE2

<!-- RAG_CHUNK: 03_SC_MARIONETTE2 -->

**Icon (EFST):** `EFST_MARIONETTE`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MARIONETTE2, 60000, 1;
```

---

### SC_CHANGEUNDEAD

<!-- RAG_CHUNK: 03_SC_CHANGEUNDEAD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CHANGEUNDEAD, 60000, 1;
```

---

### SC_JOINTBEAT

<!-- RAG_CHUNK: 03_SC_JOINTBEAT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_JOINTBEAT, 60000, 1;
```

---

### SC_MINDBREAKER

<!-- RAG_CHUNK: 03_SC_MINDBREAKER -->

**Icon (EFST):** `EFST_MINDBREAKER`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MINDBREAKER, 60000, 1;
```

---

### SC_MEMORIZE

<!-- RAG_CHUNK: 03_SC_MEMORIZE -->

**Icon (EFST):** `EFST_MEMORIZE`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MEMORIZE, 60000, 1;
```

---

### SC_FOGWALL

<!-- RAG_CHUNK: 03_SC_FOGWALL -->

**Icon (EFST):** `EFST_FOGWALL`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FOGWALL, 60000, 1;
```

---

### SC_SPIDERWEB

<!-- RAG_CHUNK: 03_SC_SPIDERWEB -->

**Icon (EFST):** `EFST_SPIDERWEB`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPIDERWEB, 60000, 1;
```

---

### SC_DEVOTION

<!-- RAG_CHUNK: 03_SC_DEVOTION -->

**Icon (EFST):** `EFST_DEVOTION`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DEVOTION, 60000, 1;
```

---

### SC_SACRIFICE

<!-- RAG_CHUNK: 03_SC_SACRIFICE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SACRIFICE, 60000, 1;
```

---

### SC_STEELBODY

<!-- RAG_CHUNK: 03_SC_STEELBODY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STEELBODY, 60000, 1;
```

---

### SC_ORCISH

<!-- RAG_CHUNK: 03_SC_ORCISH -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ORCISH, 60000, 1;
```

---

### SC_READYSTORM

<!-- RAG_CHUNK: 03_SC_READYSTORM -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_READYSTORM, 60000, 1;
```

---

### SC_READYDOWN

<!-- RAG_CHUNK: 03_SC_READYDOWN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_READYDOWN, 60000, 1;
```

---

### SC_READYTURN

<!-- RAG_CHUNK: 03_SC_READYTURN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_READYTURN, 60000, 1;
```

---

### SC_READYCOUNTER

<!-- RAG_CHUNK: 03_SC_READYCOUNTER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_READYCOUNTER, 60000, 1;
```

---

### SC_DODGE

<!-- RAG_CHUNK: 03_SC_DODGE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DODGE, 60000, 1;
```

---

### SC_RUN

<!-- RAG_CHUNK: 03_SC_RUN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_RUN, 60000, 1;
```

---

### SC_SHADOWWEAPON

<!-- RAG_CHUNK: 03_SC_SHADOWWEAPON -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SHADOWWEAPON, 60000, 1;
```

---

### SC_ADRENALINE2

<!-- RAG_CHUNK: 03_SC_ADRENALINE2 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ADRENALINE2, 60000, 1;
```

---

### SC_GHOSTWEAPON

<!-- RAG_CHUNK: 03_SC_GHOSTWEAPON -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GHOSTWEAPON, 60000, 1;
```

---

### SC_KAIZEL

<!-- RAG_CHUNK: 03_SC_KAIZEL -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KAIZEL, 60000, 1;
```

---

### SC_KAAHI

<!-- RAG_CHUNK: 03_SC_KAAHI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KAAHI, 60000, 1;
```

---

### SC_KAUPE

<!-- RAG_CHUNK: 03_SC_KAUPE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KAUPE, 60000, 1;
```

---

### SC_ONEHAND

<!-- RAG_CHUNK: 03_SC_ONEHAND -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ONEHAND, 60000, 1;
```

---

### SC_PRESERVE

<!-- RAG_CHUNK: 03_SC_PRESERVE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PRESERVE, 60000, 1;
```

---

### SC_BATTLEORDERS

<!-- RAG_CHUNK: 03_SC_BATTLEORDERS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BATTLEORDERS, 60000, 1;
```

---

### SC_REGENERATION

<!-- RAG_CHUNK: 03_SC_REGENERATION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_REGENERATION, 60000, 1;
```

---

### SC_DOUBLECAST

<!-- RAG_CHUNK: 03_SC_DOUBLECAST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DOUBLECAST, 60000, 1;
```

---

### SC_GRAVITATION

<!-- RAG_CHUNK: 03_SC_GRAVITATION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GRAVITATION, 60000, 1;
```

---

### SC_MAXOVERTHRUST

<!-- RAG_CHUNK: 03_SC_MAXOVERTHRUST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MAXOVERTHRUST, 60000, 1;
```

---

### SC_LONGING

<!-- RAG_CHUNK: 03_SC_LONGING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_LONGING, 60000, 1;
```

---

### SC_HERMODE

<!-- RAG_CHUNK: 03_SC_HERMODE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HERMODE, 60000, 1;
```

---

### SC_SHRINK

<!-- RAG_CHUNK: 03_SC_SHRINK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SHRINK, 60000, 1;
```

---

### SC_SIGHTBLASTER

<!-- RAG_CHUNK: 03_SC_SIGHTBLASTER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SIGHTBLASTER, 60000, 1;
```

---

### SC_WINKCHARM

<!-- RAG_CHUNK: 03_SC_WINKCHARM -->

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

<!-- RAG_CHUNK: 03_SC_CLOSECONFINE -->

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

<!-- RAG_CHUNK: 03_SC_CLOSECONFINE2 -->

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

<!-- RAG_CHUNK: 03_SC_DANCING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DANCING, 60000, 1;
```

---

### SC_ELEMENTALCHANGE

<!-- RAG_CHUNK: 03_SC_ELEMENTALCHANGE -->

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

<!-- RAG_CHUNK: 03_SC_RICHMANKIM -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_RICHMANKIM, 60000, 1;
```

---

### SC_ETERNALCHAOS

<!-- RAG_CHUNK: 03_SC_ETERNALCHAOS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ETERNALCHAOS, 60000, 1;
```

---

### SC_DRUMBATTLE

<!-- RAG_CHUNK: 03_SC_DRUMBATTLE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DRUMBATTLE, 60000, 1;
```

---

### SC_NIBELUNGEN

<!-- RAG_CHUNK: 03_SC_NIBELUNGEN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_NIBELUNGEN, 60000, 1;
```

---

### SC_ROKISWEIL

<!-- RAG_CHUNK: 03_SC_ROKISWEIL -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ROKISWEIL, 60000, 1;
```

---

### SC_INTOABYSS

<!-- RAG_CHUNK: 03_SC_INTOABYSS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INTOABYSS, 60000, 1;
```

---

### SC_SIEGFRIED

<!-- RAG_CHUNK: 03_SC_SIEGFRIED -->

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

<!-- RAG_CHUNK: 03_SC_WHISTLE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WHISTLE, 60000, 1;
```

---

### SC_ASSNCROS

<!-- RAG_CHUNK: 03_SC_ASSNCROS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ASSNCROS, 60000, 1;
```

---

### SC_POEMBRAGI

<!-- RAG_CHUNK: 03_SC_POEMBRAGI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_POEMBRAGI, 60000, 1;
```

---

### SC_APPLEIDUN

<!-- RAG_CHUNK: 03_SC_APPLEIDUN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_APPLEIDUN, 60000, 1;
```

---

### SC_MODECHANGE

<!-- RAG_CHUNK: 03_SC_MODECHANGE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MODECHANGE, 60000, 1;
```

---

### SC_HUMMING

<!-- RAG_CHUNK: 03_SC_HUMMING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HUMMING, 60000, 1;
```

---

### SC_DONTFORGETME

<!-- RAG_CHUNK: 03_SC_DONTFORGETME -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DONTFORGETME, 60000, 1;
```

---

### SC_FORTUNE

<!-- RAG_CHUNK: 03_SC_FORTUNE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FORTUNE, 60000, 1;
```

---

### SC_SERVICE4U

<!-- RAG_CHUNK: 03_SC_SERVICE4U -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SERVICE4U, 60000, 1;
```

---

### SC_STOP

<!-- RAG_CHUNK: 03_SC_STOP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STOP, 60000, 1;
```

---

### SC_SPURT

<!-- RAG_CHUNK: 03_SC_SPURT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPURT, 60000, 1;
```

---

### SC_SPIRIT

<!-- RAG_CHUNK: 03_SC_SPIRIT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPIRIT, 60000, 1;
```

---

### SC_COMA

<!-- RAG_CHUNK: 03_SC_COMA -->

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

<!-- RAG_CHUNK: 03_SC_INTRAVISION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INTRAVISION, 60000, 1;
```

---

### SC_INCALLSTATUS

<!-- RAG_CHUNK: 03_SC_INCALLSTATUS -->

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

<!-- RAG_CHUNK: 03_SC_INCSTR -->

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

<!-- RAG_CHUNK: 03_SC_INCAGI -->

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

<!-- RAG_CHUNK: 03_SC_INCVIT -->

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

<!-- RAG_CHUNK: 03_SC_INCINT -->

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

<!-- RAG_CHUNK: 03_SC_INCDEX -->

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

<!-- RAG_CHUNK: 03_SC_INCLUK -->

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

<!-- RAG_CHUNK: 03_SC_INCHIT -->

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

<!-- RAG_CHUNK: 03_SC_INCHITRATE -->

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

<!-- RAG_CHUNK: 03_SC_INCFLEE -->

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

<!-- RAG_CHUNK: 03_SC_INCFLEERATE -->

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

<!-- RAG_CHUNK: 03_SC_INCMHPRATE -->

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

<!-- RAG_CHUNK: 03_SC_INCMSPRATE -->

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

<!-- RAG_CHUNK: 03_SC_INCATKRATE -->

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

<!-- RAG_CHUNK: 03_SC_INCMATKRATE -->

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

<!-- RAG_CHUNK: 03_SC_INCDEFRATE -->

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

<!-- RAG_CHUNK: 03_SC_STRFOOD -->

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

<!-- RAG_CHUNK: 03_SC_AGIFOOD -->

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

<!-- RAG_CHUNK: 03_SC_VITFOOD -->

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

<!-- RAG_CHUNK: 03_SC_INTFOOD -->

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

<!-- RAG_CHUNK: 03_SC_DEXFOOD -->

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

<!-- RAG_CHUNK: 03_SC_LUKFOOD -->

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

<!-- RAG_CHUNK: 03_SC_HITFOOD -->

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

<!-- RAG_CHUNK: 03_SC_FLEEFOOD -->

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

<!-- RAG_CHUNK: 03_SC_BATKFOOD -->

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

<!-- RAG_CHUNK: 03_SC_WATKFOOD -->

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

<!-- RAG_CHUNK: 03_SC_MATKFOOD -->

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

<!-- RAG_CHUNK: 03_SC_SCRESIST -->

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

<!-- RAG_CHUNK: 03_SC_XMAS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_XMAS, 60000, 1;
```

---

### SC_WARM

<!-- RAG_CHUNK: 03_SC_WARM -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WARM, 60000, 1;
```

---

### SC_SUN_COMFORT

<!-- RAG_CHUNK: 03_SC_SUN_COMFORT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SUN_COMFORT, 60000, 1;
```

---

### SC_MOON_COMFORT

<!-- RAG_CHUNK: 03_SC_MOON_COMFORT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MOON_COMFORT, 60000, 1;
```

---

### SC_STAR_COMFORT

<!-- RAG_CHUNK: 03_SC_STAR_COMFORT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STAR_COMFORT, 60000, 1;
```

---

### SC_FUSION

<!-- RAG_CHUNK: 03_SC_FUSION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FUSION, 60000, 1;
```

---

### SC_SKILLRATE_UP

<!-- RAG_CHUNK: 03_SC_SKILLRATE_UP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SKILLRATE_UP, 60000, 1;
```

---

### SC_SKE

<!-- RAG_CHUNK: 03_SC_SKE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SKE, 60000, 1;
```

---

### SC_KAITE

<!-- RAG_CHUNK: 03_SC_KAITE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KAITE, 60000, 1;
```

---

### SC_SWOO

<!-- RAG_CHUNK: 03_SC_SWOO -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SWOO, 60000, 1;
```

---

### SC_SKA

<!-- RAG_CHUNK: 03_SC_SKA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SKA, 60000, 1;
```

---

### SC_EARTHSCROLL

<!-- RAG_CHUNK: 03_SC_EARTHSCROLL -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_EARTHSCROLL, 60000, 1;
```

---

### SC_MIRACLE

<!-- RAG_CHUNK: 03_SC_MIRACLE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MIRACLE, 60000, 1;
```

---

### SC_MADNESSCANCEL

<!-- RAG_CHUNK: 03_SC_MADNESSCANCEL -->

**Icon (EFST):** `EFST_GS_MADNESSCANCEL`

**Effect:** Increases some statuses (Base ATK, ASPD)

**Script Example:**
```c
sc_start SC_MADNESSCANCEL, 60000, 1;
```

---

### SC_ADJUSTMENT

<!-- RAG_CHUNK: 03_SC_ADJUSTMENT -->

**Icon (EFST):** `EFST_GS_ADJUSTMENT`

**Effect:** Increases some statuses (Hit, Flee)

**Script Example:**
```c
sc_start SC_ADJUSTMENT, 60000, 1;
```

---

### SC_INCREASING

<!-- RAG_CHUNK: 03_SC_INCREASING -->

**Icon (EFST):** `EFST_GS_ACCURACY`

**Effect:** Increase some statuses (Hit, Dex, Agi), GS_INCREASING effect

**Script Example:**
```c
sc_start SC_INCREASING, 60000, 1;
```

---

### SC_MAGICALBULLET

<!-- RAG_CHUNK: 03_SC_MAGICALBULLET -->

**Icon (EFST):** `EFST_GS_MAGICAL_BULLET`

**Effect:** Increases damage based on source's MATK and is reduced by target's MDEF

**Script Example:**
```c
sc_start SC_MAGICALBULLET, 60000, 1;
```

---

### SC_GATLINGFEVER

<!-- RAG_CHUNK: 03_SC_GATLINGFEVER -->

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

<!-- RAG_CHUNK: 03_SC_TATAMIGAESHI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_TATAMIGAESHI, 60000, 1;
```

---

### SC_UTSUSEMI

<!-- RAG_CHUNK: 03_SC_UTSUSEMI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_UTSUSEMI, 60000, 1;
```

---

### SC_BUNSINJYUTSU

<!-- RAG_CHUNK: 03_SC_BUNSINJYUTSU -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BUNSINJYUTSU, 60000, 1;
```

---

### SC_KAENSIN

<!-- RAG_CHUNK: 03_SC_KAENSIN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KAENSIN, 60000, 1;
```

---

### SC_SUITON

<!-- RAG_CHUNK: 03_SC_SUITON -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SUITON, 60000, 1;
```

---

### SC_NEN

<!-- RAG_CHUNK: 03_SC_NEN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_NEN, 60000, 1;
```

---

### SC_KNOWLEDGE

<!-- RAG_CHUNK: 03_SC_KNOWLEDGE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KNOWLEDGE, 60000, 1;
```

---

### SC_SMA

<!-- RAG_CHUNK: 03_SC_SMA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SMA, 60000, 1;
```

---

### SC_FLING

<!-- RAG_CHUNK: 03_SC_FLING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FLING, 60000, 1;
```

---

### SC_AVOID

<!-- RAG_CHUNK: 03_SC_AVOID -->

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

<!-- RAG_CHUNK: 03_SC_CHANGE -->

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

<!-- RAG_CHUNK: 03_SC_BLOODLUST -->

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

<!-- RAG_CHUNK: 03_SC_FLEET -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FLEET, 60000, 1;
```

---

### SC_SPEED

<!-- RAG_CHUNK: 03_SC_SPEED -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPEED, 60000, 1;
```

---

### SC_DEFENCE

<!-- RAG_CHUNK: 03_SC_DEFENCE -->

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

<!-- RAG_CHUNK: 03_SC_INCASPDRATE -->

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

<!-- RAG_CHUNK: 03_SC_INCFLEE2 -->

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

<!-- RAG_CHUNK: 03_SC_JAILED -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_JAILED, 60000, 1;
```

---

### SC_ENCHANTARMS

<!-- RAG_CHUNK: 03_SC_ENCHANTARMS -->

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

<!-- RAG_CHUNK: 03_SC_MAGICALATTACK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MAGICALATTACK, 60000, 1;
```

---

### SC_ARMORCHANGE

<!-- RAG_CHUNK: 03_SC_ARMORCHANGE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ARMORCHANGE, 60000, 1;
```

---

### SC_CRITICALWOUND

<!-- RAG_CHUNK: 03_SC_CRITICALWOUND -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CRITICALWOUND, 60000, 1;
```

---

### SC_MAGICMIRROR

<!-- RAG_CHUNK: 03_SC_MAGICMIRROR -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MAGICMIRROR, 60000, 1;
```

---

### SC_SLOWCAST

<!-- RAG_CHUNK: 03_SC_SLOWCAST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SLOWCAST, 60000, 1;
```

---

### SC_SUMMER

<!-- RAG_CHUNK: 03_SC_SUMMER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SUMMER, 60000, 1;
```

---

### SC_EXPBOOST

<!-- RAG_CHUNK: 03_SC_EXPBOOST -->

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

<!-- RAG_CHUNK: 03_SC_ITEMBOOST -->

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

<!-- RAG_CHUNK: 03_SC_BOSSMAPINFO -->

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

<!-- RAG_CHUNK: 03_SC_LIFEINSURANCE -->

**Icon (EFST):** `EFST_CASH_DEATHPENALTY`

**Effect:** Remove death pleanlties

**Script Example:**
```c
sc_start SC_LIFEINSURANCE, 60000, 1;
```

---

### SC_INCCRI

<!-- RAG_CHUNK: 03_SC_INCCRI -->

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

<!-- RAG_CHUNK: 03_SC_INCDEF -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INCDEF, 60000, 1;
```

---

### SC_INCBASEATK

<!-- RAG_CHUNK: 03_SC_INCBASEATK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INCBASEATK, 60000, 1;
```

---

### SC_FASTCAST

<!-- RAG_CHUNK: 03_SC_FASTCAST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FASTCAST, 60000, 1;
```

---

### SC_MDEF_RATE

<!-- RAG_CHUNK: 03_SC_MDEF_RATE -->

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

<!-- RAG_CHUNK: 03_SC_HPREGEN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HPREGEN, 60000, 1;
```

---

### SC_INCHEALRATE

<!-- RAG_CHUNK: 03_SC_INCHEALRATE -->

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

<!-- RAG_CHUNK: 03_SC_PNEUMA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PNEUMA, 60000, 1;
```

---

### SC_AUTOTRADE

<!-- RAG_CHUNK: 03_SC_AUTOTRADE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_AUTOTRADE, 60000, 1;
```

---

### SC_KSPROTECTED

<!-- RAG_CHUNK: 03_SC_KSPROTECTED -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KSPROTECTED, 60000, 1;
```

---

### SC_ARMOR_RESIST

<!-- RAG_CHUNK: 03_SC_ARMOR_RESIST -->

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

<!-- RAG_CHUNK: 03_SC_SPCOST_RATE -->

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

<!-- RAG_CHUNK: 03_SC_COMMONSC_RESIST -->

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

<!-- RAG_CHUNK: 03_SC_SEVENWIND -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SEVENWIND, 60000, 1;
```

---

### SC_DEF_RATE

<!-- RAG_CHUNK: 03_SC_DEF_RATE -->

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

<!-- RAG_CHUNK: 03_SC_SPREGEN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPREGEN, 60000, 1;
```

---

### SC_WALKSPEED

<!-- RAG_CHUNK: 03_SC_WALKSPEED -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WALKSPEED, 60000, 1;
```

---

### SC_MERC_FLEEUP

<!-- RAG_CHUNK: 03_SC_MERC_FLEEUP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MERC_FLEEUP, 60000, 1;
```

---

### SC_MERC_ATKUP

<!-- RAG_CHUNK: 03_SC_MERC_ATKUP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MERC_ATKUP, 60000, 1;
```

---

### SC_MERC_HPUP

<!-- RAG_CHUNK: 03_SC_MERC_HPUP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MERC_HPUP, 60000, 1;
```

---

### SC_MERC_SPUP

<!-- RAG_CHUNK: 03_SC_MERC_SPUP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MERC_SPUP, 60000, 1;
```

---

### SC_MERC_HITUP

<!-- RAG_CHUNK: 03_SC_MERC_HITUP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MERC_HITUP, 60000, 1;
```

---

### SC_MERC_QUICKEN

<!-- RAG_CHUNK: 03_SC_MERC_QUICKEN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MERC_QUICKEN, 60000, 1;
```

---

### SC_REBIRTH

<!-- RAG_CHUNK: 03_SC_REBIRTH -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_REBIRTH, 60000, 1;
```

---

### SC_SKILLCASTRATE

<!-- RAG_CHUNK: 03_SC_SKILLCASTRATE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SKILLCASTRATE, 60000, 1;
```

---

### SC_DEFRATIOATK

<!-- RAG_CHUNK: 03_SC_DEFRATIOATK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DEFRATIOATK, 60000, 1;
```

---

### SC_HPDRAIN

<!-- RAG_CHUNK: 03_SC_HPDRAIN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HPDRAIN, 60000, 1;
```

---

### SC_SKILLATKBONUS

<!-- RAG_CHUNK: 03_SC_SKILLATKBONUS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SKILLATKBONUS, 60000, 1;
```

---

### SC_ITEMSCRIPT

<!-- RAG_CHUNK: 03_SC_ITEMSCRIPT -->

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

<!-- RAG_CHUNK: 03_SC_S_LIFEPOTION -->

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

<!-- RAG_CHUNK: 03_SC_L_LIFEPOTION -->

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

<!-- RAG_CHUNK: 03_SC_JEXPBOOST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_JEXPBOOST, 60000, 1;
```

---

### SC_IGNOREDEF

<!-- RAG_CHUNK: 03_SC_IGNOREDEF -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_IGNOREDEF, 60000, 1;
```

---

### SC_HELLPOWER

<!-- RAG_CHUNK: 03_SC_HELLPOWER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HELLPOWER, 60000, 1;
```

---

### SC_INVINCIBLE

<!-- RAG_CHUNK: 03_SC_INVINCIBLE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INVINCIBLE, 60000, 1;
```

---

### SC_INVINCIBLEOFF

<!-- RAG_CHUNK: 03_SC_INVINCIBLEOFF -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INVINCIBLEOFF, 60000, 1;
```

---

### SC_MANU_ATK

<!-- RAG_CHUNK: 03_SC_MANU_ATK -->

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

<!-- RAG_CHUNK: 03_SC_MANU_DEF -->

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

<!-- RAG_CHUNK: 03_SC_SPL_ATK -->

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

<!-- RAG_CHUNK: 03_SC_SPL_DEF -->

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

<!-- RAG_CHUNK: 03_SC_MANU_MATK -->

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

<!-- RAG_CHUNK: 03_SC_SPL_MATK -->

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

<!-- RAG_CHUNK: 03_SC_FOOD_STR_CASH -->

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

<!-- RAG_CHUNK: 03_SC_FOOD_AGI_CASH -->

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

<!-- RAG_CHUNK: 03_SC_FOOD_VIT_CASH -->

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

<!-- RAG_CHUNK: 03_SC_FOOD_DEX_CASH -->

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

<!-- RAG_CHUNK: 03_SC_FOOD_INT_CASH -->

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

<!-- RAG_CHUNK: 03_SC_FOOD_LUK_CASH -->

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

<!-- RAG_CHUNK: 03_SC_FEAR -->

**Effect:** Cause SC_ANKLE for 2 seconds, Hit/Flee -20%, remove blind, immune to blind

**Script Example:**
```c
sc_start SC_FEAR, 60000, 1;
```

---

### SC_BURNING

<!-- RAG_CHUNK: 03_SC_BURNING -->

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

<!-- RAG_CHUNK: 03_SC_FREEZING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FREEZING, 60000, 1;
```

---

### SC_ENCHANTBLADE

<!-- RAG_CHUNK: 03_SC_ENCHANTBLADE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ENCHANTBLADE, 60000, 1;
```

---

### SC_DEATHBOUND

<!-- RAG_CHUNK: 03_SC_DEATHBOUND -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DEATHBOUND, 60000, 1;
```

---

### SC_MILLENNIUMSHIELD

<!-- RAG_CHUNK: 03_SC_MILLENNIUMSHIELD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MILLENNIUMSHIELD, 60000, 1;
```

---

### SC_CRUSHSTRIKE

<!-- RAG_CHUNK: 03_SC_CRUSHSTRIKE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CRUSHSTRIKE, 60000, 1;
```

---

### SC_REFRESH

<!-- RAG_CHUNK: 03_SC_REFRESH -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_REFRESH, 60000, 1;
```

---

### SC_REUSE_REFRESH

<!-- RAG_CHUNK: 03_SC_REUSE_REFRESH -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_REUSE_REFRESH, 60000, 1;
```

---

### SC_GIANTGROWTH

<!-- RAG_CHUNK: 03_SC_GIANTGROWTH -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GIANTGROWTH, 60000, 1;
```

---

### SC_STONEHARDSKIN

<!-- RAG_CHUNK: 03_SC_STONEHARDSKIN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STONEHARDSKIN, 60000, 1;
```

---

### SC_VITALITYACTIVATION

<!-- RAG_CHUNK: 03_SC_VITALITYACTIVATION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_VITALITYACTIVATION, 60000, 1;
```

---

### SC_STORMBLAST

<!-- RAG_CHUNK: 03_SC_STORMBLAST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STORMBLAST, 60000, 1;
```

---

### SC_FIGHTINGSPIRIT

<!-- RAG_CHUNK: 03_SC_FIGHTINGSPIRIT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FIGHTINGSPIRIT, 60000, 1;
```

---

### SC_ABUNDANCE

<!-- RAG_CHUNK: 03_SC_ABUNDANCE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ABUNDANCE, 60000, 1;
```

---

### SC_ADORAMUS

<!-- RAG_CHUNK: 03_SC_ADORAMUS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ADORAMUS, 60000, 1;
```

---

### SC_EPICLESIS

<!-- RAG_CHUNK: 03_SC_EPICLESIS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_EPICLESIS, 60000, 1;
```

---

### SC_ORATIO

<!-- RAG_CHUNK: 03_SC_ORATIO -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ORATIO, 60000, 1;
```

---

### SC_LAUDAAGNUS

<!-- RAG_CHUNK: 03_SC_LAUDAAGNUS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_LAUDAAGNUS, 60000, 1;
```

---

### SC_LAUDARAMUS

<!-- RAG_CHUNK: 03_SC_LAUDARAMUS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_LAUDARAMUS, 60000, 1;
```

---

### SC_RENOVATIO

<!-- RAG_CHUNK: 03_SC_RENOVATIO -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_RENOVATIO, 60000, 1;
```

---

### SC_EXPIATIO

<!-- RAG_CHUNK: 03_SC_EXPIATIO -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_EXPIATIO, 60000, 1;
```

---

### SC_DUPLELIGHT

<!-- RAG_CHUNK: 03_SC_DUPLELIGHT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DUPLELIGHT, 60000, 1;
```

---

### SC_SECRAMENT

<!-- RAG_CHUNK: 03_SC_SECRAMENT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SECRAMENT, 60000, 1;
```

---

### SC_WHITEIMPRISON

<!-- RAG_CHUNK: 03_SC_WHITEIMPRISON -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WHITEIMPRISON, 60000, 1;
```

---

### SC_MARSHOFABYSS

<!-- RAG_CHUNK: 03_SC_MARSHOFABYSS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MARSHOFABYSS, 60000, 1;
```

---

### SC_RECOGNIZEDSPELL

<!-- RAG_CHUNK: 03_SC_RECOGNIZEDSPELL -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_RECOGNIZEDSPELL, 60000, 1;
```

---

### SC_STASIS

<!-- RAG_CHUNK: 03_SC_STASIS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STASIS, 60000, 1;
```

---

### SC_SPHERE_1

<!-- RAG_CHUNK: 03_SC_SPHERE_1 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPHERE_1, 60000, 1;
```

---

### SC_SPHERE_2

<!-- RAG_CHUNK: 03_SC_SPHERE_2 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPHERE_2, 60000, 1;
```

---

### SC_SPHERE_3

<!-- RAG_CHUNK: 03_SC_SPHERE_3 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPHERE_3, 60000, 1;
```

---

### SC_SPHERE_4

<!-- RAG_CHUNK: 03_SC_SPHERE_4 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPHERE_4, 60000, 1;
```

---

### SC_SPHERE_5

<!-- RAG_CHUNK: 03_SC_SPHERE_5 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPHERE_5, 60000, 1;
```

---

### SC_READING_SB

<!-- RAG_CHUNK: 03_SC_READING_SB -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_READING_SB, 60000, 1;
```

---

### SC_FREEZE_SP

<!-- RAG_CHUNK: 03_SC_FREEZE_SP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FREEZE_SP, 60000, 1;
```

---

### SC_FEARBREEZE

<!-- RAG_CHUNK: 03_SC_FEARBREEZE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FEARBREEZE, 60000, 1;
```

---

### SC_ELECTRICSHOCKER

<!-- RAG_CHUNK: 03_SC_ELECTRICSHOCKER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ELECTRICSHOCKER, 60000, 1;
```

---

### SC_WUGDASH

<!-- RAG_CHUNK: 03_SC_WUGDASH -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WUGDASH, 60000, 1;
```

---

### SC_BITE

<!-- RAG_CHUNK: 03_SC_BITE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BITE, 60000, 1;
```

---

### SC_CAMOUFLAGE

<!-- RAG_CHUNK: 03_SC_CAMOUFLAGE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CAMOUFLAGE, 60000, 1;
```

---

### SC_ACCELERATION

<!-- RAG_CHUNK: 03_SC_ACCELERATION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ACCELERATION, 60000, 1;
```

---

### SC_HOVERING

<!-- RAG_CHUNK: 03_SC_HOVERING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HOVERING, 60000, 1;
```

---

### SC_SHAPESHIFT

<!-- RAG_CHUNK: 03_SC_SHAPESHIFT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SHAPESHIFT, 60000, 1;
```

---

### SC_INFRAREDSCAN

<!-- RAG_CHUNK: 03_SC_INFRAREDSCAN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INFRAREDSCAN, 60000, 1;
```

---

### SC_ANALYZE

<!-- RAG_CHUNK: 03_SC_ANALYZE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ANALYZE, 60000, 1;
```

---

### SC_MAGNETICFIELD

<!-- RAG_CHUNK: 03_SC_MAGNETICFIELD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MAGNETICFIELD, 60000, 1;
```

---

### SC_NEUTRALBARRIER

<!-- RAG_CHUNK: 03_SC_NEUTRALBARRIER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_NEUTRALBARRIER, 60000, 1;
```

---

### SC_NEUTRALBARRIER_MASTER

<!-- RAG_CHUNK: 03_SC_NEUTRALBARRIER_MASTER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_NEUTRALBARRIER_MASTER, 60000, 1;
```

---

### SC_STEALTHFIELD

<!-- RAG_CHUNK: 03_SC_STEALTHFIELD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STEALTHFIELD, 60000, 1;
```

---

### SC_STEALTHFIELD_MASTER

<!-- RAG_CHUNK: 03_SC_STEALTHFIELD_MASTER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STEALTHFIELD_MASTER, 60000, 1;
```

---

### SC_OVERHEAT

<!-- RAG_CHUNK: 03_SC_OVERHEAT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_OVERHEAT, 60000, 1;
```

---

### SC_OVERHEAT_LIMITPOINT

<!-- RAG_CHUNK: 03_SC_OVERHEAT_LIMITPOINT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_OVERHEAT_LIMITPOINT, 60000, 1;
```

---

### SC_VENOMIMPRESS

<!-- RAG_CHUNK: 03_SC_VENOMIMPRESS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_VENOMIMPRESS, 60000, 1;
```

---

### SC_POISONINGWEAPON

<!-- RAG_CHUNK: 03_SC_POISONINGWEAPON -->

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

<!-- RAG_CHUNK: 03_SC_WEAPONBLOCKING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WEAPONBLOCKING, 60000, 1;
```

---

### SC_CLOAKINGEXCEED

<!-- RAG_CHUNK: 03_SC_CLOAKINGEXCEED -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CLOAKINGEXCEED, 60000, 1;
```

---

### SC_HALLUCINATIONWALK

<!-- RAG_CHUNK: 03_SC_HALLUCINATIONWALK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HALLUCINATIONWALK, 60000, 1;
```

---

### SC_HALLUCINATIONWALK_POSTDELAY

<!-- RAG_CHUNK: 03_SC_HALLUCINATIONWALK_POSTDELAY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HALLUCINATIONWALK_POSTDELAY, 60000, 1;
```

---

### SC_ROLLINGCUTTER

<!-- RAG_CHUNK: 03_SC_ROLLINGCUTTER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ROLLINGCUTTER, 60000, 1;
```

---

### SC_TOXIN

<!-- RAG_CHUNK: 03_SC_TOXIN -->

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

<!-- RAG_CHUNK: 03_SC_PARALYSE -->

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

<!-- RAG_CHUNK: 03_SC_VENOMBLEED -->

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

<!-- RAG_CHUNK: 03_SC_MAGICMUSHROOM -->

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

<!-- RAG_CHUNK: 03_SC_DEATHHURT -->

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

<!-- RAG_CHUNK: 03_SC_PYREXIA -->

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

<!-- RAG_CHUNK: 03_SC_OBLIVIONCURSE -->

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

<!-- RAG_CHUNK: 03_SC_LEECHESEND -->

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

<!-- RAG_CHUNK: 03_SC_REFLECTDAMAGE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_REFLECTDAMAGE, 60000, 1;
```

---

### SC_FORCEOFVANGUARD

<!-- RAG_CHUNK: 03_SC_FORCEOFVANGUARD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FORCEOFVANGUARD, 60000, 1;
```

---

### SC_SHIELDSPELL_DEF

<!-- RAG_CHUNK: 03_SC_SHIELDSPELL_DEF -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SHIELDSPELL_DEF, 60000, 1;
```

---

### SC_SHIELDSPELL_MDEF

<!-- RAG_CHUNK: 03_SC_SHIELDSPELL_MDEF -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SHIELDSPELL_MDEF, 60000, 1;
```

---

### SC_SHIELDSPELL_REF

<!-- RAG_CHUNK: 03_SC_SHIELDSPELL_REF -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SHIELDSPELL_REF, 60000, 1;
```

---

### SC_EXEEDBREAK

<!-- RAG_CHUNK: 03_SC_EXEEDBREAK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_EXEEDBREAK, 60000, 1;
```

---

### SC_PRESTIGE

<!-- RAG_CHUNK: 03_SC_PRESTIGE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PRESTIGE, 60000, 1;
```

---

### SC_BANDING

<!-- RAG_CHUNK: 03_SC_BANDING -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BANDING, 60000, 1;
```

---

### SC_BANDING_DEFENCE

<!-- RAG_CHUNK: 03_SC_BANDING_DEFENCE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BANDING_DEFENCE, 60000, 1;
```

---

### SC_EARTHDRIVE

<!-- RAG_CHUNK: 03_SC_EARTHDRIVE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_EARTHDRIVE, 60000, 1;
```

---

### SC_INSPIRATION

<!-- RAG_CHUNK: 03_SC_INSPIRATION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_INSPIRATION, 60000, 1;
```

---

### SC_SPELLFIST

<!-- RAG_CHUNK: 03_SC_SPELLFIST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPELLFIST, 60000, 1;
```

---

### SC_CRYSTALIZE

<!-- RAG_CHUNK: 03_SC_CRYSTALIZE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CRYSTALIZE, 60000, 1;
```

---

### SC_STRIKING

<!-- RAG_CHUNK: 03_SC_STRIKING -->

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

<!-- RAG_CHUNK: 03_SC_WARMER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WARMER, 60000, 1;
```

---

### SC_VACUUM_EXTREME

<!-- RAG_CHUNK: 03_SC_VACUUM_EXTREME -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_VACUUM_EXTREME, 60000, 1;
```

---

### SC_PROPERTYWALK

<!-- RAG_CHUNK: 03_SC_PROPERTYWALK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PROPERTYWALK, 60000, 1;
```

---

### SC_SWINGDANCE

<!-- RAG_CHUNK: 03_SC_SWINGDANCE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SWINGDANCE, 60000, 1;
```

---

### SC_SYMPHONYOFLOVER

<!-- RAG_CHUNK: 03_SC_SYMPHONYOFLOVER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SYMPHONYOFLOVER, 60000, 1;
```

---

### SC_MOONLITSERENADE

<!-- RAG_CHUNK: 03_SC_MOONLITSERENADE -->

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

<!-- RAG_CHUNK: 03_SC_RUSHWINDMILL -->

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

<!-- RAG_CHUNK: 03_SC_ECHOSONG -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ECHOSONG, 60000, 1;
```

---

### SC_HARMONIZE

<!-- RAG_CHUNK: 03_SC_HARMONIZE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HARMONIZE, 60000, 1;
```

---

### SC_VOICEOFSIREN

<!-- RAG_CHUNK: 03_SC_VOICEOFSIREN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_VOICEOFSIREN, 60000, 1;
```

---

### SC_DEEPSLEEP

<!-- RAG_CHUNK: 03_SC_DEEPSLEEP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DEEPSLEEP, 60000, 1;
```

---

### SC_SIRCLEOFNATURE

<!-- RAG_CHUNK: 03_SC_SIRCLEOFNATURE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SIRCLEOFNATURE, 60000, 1;
```

---

### SC_GLOOMYDAY

<!-- RAG_CHUNK: 03_SC_GLOOMYDAY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GLOOMYDAY, 60000, 1;
```

---

### SC_GLOOMYDAY_SK

<!-- RAG_CHUNK: 03_SC_GLOOMYDAY_SK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GLOOMYDAY_SK, 60000, 1;
```

---

### SC_SONGOFMANA

<!-- RAG_CHUNK: 03_SC_SONGOFMANA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SONGOFMANA, 60000, 1;
```

---

### SC_DANCEWITHWUG

<!-- RAG_CHUNK: 03_SC_DANCEWITHWUG -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DANCEWITHWUG, 60000, 1;
```

---

### SC_SATURDAYNIGHTFEVER

<!-- RAG_CHUNK: 03_SC_SATURDAYNIGHTFEVER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SATURDAYNIGHTFEVER, 60000, 1;
```

---

### SC_LERADSDEW

<!-- RAG_CHUNK: 03_SC_LERADSDEW -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_LERADSDEW, 60000, 1;
```

---

### SC_MELODYOFSINK

<!-- RAG_CHUNK: 03_SC_MELODYOFSINK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MELODYOFSINK, 60000, 1;
```

---

### SC_BEYONDOFWARCRY

<!-- RAG_CHUNK: 03_SC_BEYONDOFWARCRY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BEYONDOFWARCRY, 60000, 1;
```

---

### SC_UNLIMITEDHUMMINGVOICE

<!-- RAG_CHUNK: 03_SC_UNLIMITEDHUMMINGVOICE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_UNLIMITEDHUMMINGVOICE, 60000, 1;
```

---

### SC_SITDOWN_FORCE

<!-- RAG_CHUNK: 03_SC_SITDOWN_FORCE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SITDOWN_FORCE, 60000, 1;
```

---

### SC_NETHERWORLD

<!-- RAG_CHUNK: 03_SC_NETHERWORLD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_NETHERWORLD, 60000, 1;
```

---

### SC_CRESCENTELBOW

<!-- RAG_CHUNK: 03_SC_CRESCENTELBOW -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CRESCENTELBOW, 60000, 1;
```

---

### SC_CURSEDCIRCLE_ATKER

<!-- RAG_CHUNK: 03_SC_CURSEDCIRCLE_ATKER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CURSEDCIRCLE_ATKER, 60000, 1;
```

---

### SC_CURSEDCIRCLE_TARGET

<!-- RAG_CHUNK: 03_SC_CURSEDCIRCLE_TARGET -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CURSEDCIRCLE_TARGET, 60000, 1;
```

---

### SC_LIGHTNINGWALK

<!-- RAG_CHUNK: 03_SC_LIGHTNINGWALK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_LIGHTNINGWALK, 60000, 1;
```

---

### SC_RAISINGDRAGON

<!-- RAG_CHUNK: 03_SC_RAISINGDRAGON -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_RAISINGDRAGON, 60000, 1;
```

---

### SC_GT_ENERGYGAIN

<!-- RAG_CHUNK: 03_SC_GT_ENERGYGAIN -->

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

<!-- RAG_CHUNK: 03_SC_GT_CHANGE -->

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

<!-- RAG_CHUNK: 03_SC_GT_REVITALIZE -->

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

<!-- RAG_CHUNK: 03_SC_GN_CARTBOOST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GN_CARTBOOST, 60000, 1;
```

---

### SC_THORNSTRAP

<!-- RAG_CHUNK: 03_SC_THORNSTRAP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_THORNSTRAP, 60000, 1;
```

---

### SC_BLOODSUCKER

<!-- RAG_CHUNK: 03_SC_BLOODSUCKER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BLOODSUCKER, 60000, 1;
```

---

### SC_SMOKEPOWDER

<!-- RAG_CHUNK: 03_SC_SMOKEPOWDER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SMOKEPOWDER, 60000, 1;
```

---

### SC_TEARGAS

<!-- RAG_CHUNK: 03_SC_TEARGAS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_TEARGAS, 60000, 1;
```

---

### SC_MANDRAGORA

<!-- RAG_CHUNK: 03_SC_MANDRAGORA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MANDRAGORA, 60000, 1;
```

---

### SC_STOMACHACHE

<!-- RAG_CHUNK: 03_SC_STOMACHACHE -->

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

<!-- RAG_CHUNK: 03_SC_MYSTERIOUS_POWDER -->

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

<!-- RAG_CHUNK: 03_SC_MELON_BOMB -->

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

<!-- RAG_CHUNK: 03_SC_BANANA_BOMB -->

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

<!-- RAG_CHUNK: 03_SC_BANANA_BOMB_SITDOWN -->

**Icon (EFST):** `EFST_BANANA_BOMB_SITDOWN_POSTDELAY`

**Effect:** Force player to sit

**Script Example:**
```c
sc_start SC_BANANA_BOMB_SITDOWN, 60000, 1;
```

---

### SC_SAVAGE_STEAK

<!-- RAG_CHUNK: 03_SC_SAVAGE_STEAK -->

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

<!-- RAG_CHUNK: 03_SC_COCKTAIL_WARG_BLOOD -->

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

<!-- RAG_CHUNK: 03_SC_MINOR_BBQ -->

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

<!-- RAG_CHUNK: 03_SC_SIROMA_ICE_TEA -->

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

<!-- RAG_CHUNK: 03_SC_DROCERA_HERB_STEAMED -->

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

<!-- RAG_CHUNK: 03_SC_PUTTI_TAILS_NOODLES -->

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

<!-- RAG_CHUNK: 03_SC_BOOST500 -->

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

<!-- RAG_CHUNK: 03_SC_FULL_SWING_K -->

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

<!-- RAG_CHUNK: 03_SC_MANA_PLUS -->

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

<!-- RAG_CHUNK: 03_SC_MUSTLE_M -->

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

<!-- RAG_CHUNK: 03_SC_LIFE_FORCE_F -->

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

<!-- RAG_CHUNK: 03_SC_EXTRACT_WHITE_POTION_Z -->

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

<!-- RAG_CHUNK: 03_SC_VITATA_500 -->

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

<!-- RAG_CHUNK: 03_SC_EXTRACT_SALAMINE_JUICE -->

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

<!-- RAG_CHUNK: 03_SC__REPRODUCE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__REPRODUCE, 60000, 1;
```

---

### SC__AUTOSHADOWSPELL

<!-- RAG_CHUNK: 03_SC__AUTOSHADOWSPELL -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__AUTOSHADOWSPELL, 60000, 1;
```

---

### SC__SHADOWFORM

<!-- RAG_CHUNK: 03_SC__SHADOWFORM -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__SHADOWFORM, 60000, 1;
```

---

### SC__BODYPAINT

<!-- RAG_CHUNK: 03_SC__BODYPAINT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__BODYPAINT, 60000, 1;
```

---

### SC__INVISIBILITY

<!-- RAG_CHUNK: 03_SC__INVISIBILITY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__INVISIBILITY, 60000, 1;
```

---

### SC__DEADLYINFECT

<!-- RAG_CHUNK: 03_SC__DEADLYINFECT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__DEADLYINFECT, 60000, 1;
```

---

### SC__ENERVATION

<!-- RAG_CHUNK: 03_SC__ENERVATION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__ENERVATION, 60000, 1;
```

---

### SC__GROOMY

<!-- RAG_CHUNK: 03_SC__GROOMY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__GROOMY, 60000, 1;
```

---

### SC__IGNORANCE

<!-- RAG_CHUNK: 03_SC__IGNORANCE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__IGNORANCE, 60000, 1;
```

---

### SC__LAZINESS

<!-- RAG_CHUNK: 03_SC__LAZINESS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__LAZINESS, 60000, 1;
```

---

### SC__UNLUCKY

<!-- RAG_CHUNK: 03_SC__UNLUCKY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__UNLUCKY, 60000, 1;
```

---

### SC__WEAKNESS

<!-- RAG_CHUNK: 03_SC__WEAKNESS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__WEAKNESS, 60000, 1;
```

---

### SC__STRIPACCESSORY

<!-- RAG_CHUNK: 03_SC__STRIPACCESSORY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__STRIPACCESSORY, 60000, 1;
```

---

### SC__MANHOLE

<!-- RAG_CHUNK: 03_SC__MANHOLE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__MANHOLE, 60000, 1;
```

---

### SC__BLOODYLUST

<!-- RAG_CHUNK: 03_SC__BLOODYLUST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__BLOODYLUST, 60000, 1;
```

---

### SC_CIRCLE_OF_FIRE

<!-- RAG_CHUNK: 03_SC_CIRCLE_OF_FIRE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CIRCLE_OF_FIRE, 60000, 1;
```

---

### SC_CIRCLE_OF_FIRE_OPTION

<!-- RAG_CHUNK: 03_SC_CIRCLE_OF_FIRE_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CIRCLE_OF_FIRE_OPTION, 60000, 1;
```

---

### SC_FIRE_CLOAK

<!-- RAG_CHUNK: 03_SC_FIRE_CLOAK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FIRE_CLOAK, 60000, 1;
```

---

### SC_FIRE_CLOAK_OPTION

<!-- RAG_CHUNK: 03_SC_FIRE_CLOAK_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FIRE_CLOAK_OPTION, 60000, 1;
```

---

### SC_WATER_SCREEN

<!-- RAG_CHUNK: 03_SC_WATER_SCREEN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WATER_SCREEN, 60000, 1;
```

---

### SC_WATER_SCREEN_OPTION

<!-- RAG_CHUNK: 03_SC_WATER_SCREEN_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WATER_SCREEN_OPTION, 60000, 1;
```

---

### SC_WATER_DROP

<!-- RAG_CHUNK: 03_SC_WATER_DROP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WATER_DROP, 60000, 1;
```

---

### SC_WATER_DROP_OPTION

<!-- RAG_CHUNK: 03_SC_WATER_DROP_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WATER_DROP_OPTION, 60000, 1;
```

---

### SC_WATER_BARRIER

<!-- RAG_CHUNK: 03_SC_WATER_BARRIER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WATER_BARRIER, 60000, 1;
```

---

### SC_WIND_STEP

<!-- RAG_CHUNK: 03_SC_WIND_STEP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WIND_STEP, 60000, 1;
```

---

### SC_WIND_STEP_OPTION

<!-- RAG_CHUNK: 03_SC_WIND_STEP_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WIND_STEP_OPTION, 60000, 1;
```

---

### SC_WIND_CURTAIN

<!-- RAG_CHUNK: 03_SC_WIND_CURTAIN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WIND_CURTAIN, 60000, 1;
```

---

### SC_WIND_CURTAIN_OPTION

<!-- RAG_CHUNK: 03_SC_WIND_CURTAIN_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WIND_CURTAIN_OPTION, 60000, 1;
```

---

### SC_ZEPHYR

<!-- RAG_CHUNK: 03_SC_ZEPHYR -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ZEPHYR, 60000, 1;
```

---

### SC_SOLID_SKIN

<!-- RAG_CHUNK: 03_SC_SOLID_SKIN -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SOLID_SKIN, 60000, 1;
```

---

### SC_SOLID_SKIN_OPTION

<!-- RAG_CHUNK: 03_SC_SOLID_SKIN_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SOLID_SKIN_OPTION, 60000, 1;
```

---

### SC_STONE_SHIELD

<!-- RAG_CHUNK: 03_SC_STONE_SHIELD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STONE_SHIELD, 60000, 1;
```

---

### SC_STONE_SHIELD_OPTION

<!-- RAG_CHUNK: 03_SC_STONE_SHIELD_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STONE_SHIELD_OPTION, 60000, 1;
```

---

### SC_POWER_OF_GAIA

<!-- RAG_CHUNK: 03_SC_POWER_OF_GAIA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_POWER_OF_GAIA, 60000, 1;
```

---

### SC_PYROTECHNIC

<!-- RAG_CHUNK: 03_SC_PYROTECHNIC -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PYROTECHNIC, 60000, 1;
```

---

### SC_PYROTECHNIC_OPTION

<!-- RAG_CHUNK: 03_SC_PYROTECHNIC_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PYROTECHNIC_OPTION, 60000, 1;
```

---

### SC_HEATER

<!-- RAG_CHUNK: 03_SC_HEATER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HEATER, 60000, 1;
```

---

### SC_HEATER_OPTION

<!-- RAG_CHUNK: 03_SC_HEATER_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HEATER_OPTION, 60000, 1;
```

---

### SC_TROPIC

<!-- RAG_CHUNK: 03_SC_TROPIC -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_TROPIC, 60000, 1;
```

---

### SC_TROPIC_OPTION

<!-- RAG_CHUNK: 03_SC_TROPIC_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_TROPIC_OPTION, 60000, 1;
```

---

### SC_AQUAPLAY

<!-- RAG_CHUNK: 03_SC_AQUAPLAY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_AQUAPLAY, 60000, 1;
```

---

### SC_AQUAPLAY_OPTION

<!-- RAG_CHUNK: 03_SC_AQUAPLAY_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_AQUAPLAY_OPTION, 60000, 1;
```

---

### SC_COOLER

<!-- RAG_CHUNK: 03_SC_COOLER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_COOLER, 60000, 1;
```

---

### SC_COOLER_OPTION

<!-- RAG_CHUNK: 03_SC_COOLER_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_COOLER_OPTION, 60000, 1;
```

---

### SC_CHILLY_AIR

<!-- RAG_CHUNK: 03_SC_CHILLY_AIR -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CHILLY_AIR, 60000, 1;
```

---

### SC_CHILLY_AIR_OPTION

<!-- RAG_CHUNK: 03_SC_CHILLY_AIR_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CHILLY_AIR_OPTION, 60000, 1;
```

---

### SC_GUST

<!-- RAG_CHUNK: 03_SC_GUST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GUST, 60000, 1;
```

---

### SC_GUST_OPTION

<!-- RAG_CHUNK: 03_SC_GUST_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GUST_OPTION, 60000, 1;
```

---

### SC_BLAST

<!-- RAG_CHUNK: 03_SC_BLAST -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BLAST, 60000, 1;
```

---

### SC_BLAST_OPTION

<!-- RAG_CHUNK: 03_SC_BLAST_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_BLAST_OPTION, 60000, 1;
```

---

### SC_WILD_STORM

<!-- RAG_CHUNK: 03_SC_WILD_STORM -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WILD_STORM, 60000, 1;
```

---

### SC_WILD_STORM_OPTION

<!-- RAG_CHUNK: 03_SC_WILD_STORM_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WILD_STORM_OPTION, 60000, 1;
```

---

### SC_PETROLOGY

<!-- RAG_CHUNK: 03_SC_PETROLOGY -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PETROLOGY, 60000, 1;
```

---

### SC_PETROLOGY_OPTION

<!-- RAG_CHUNK: 03_SC_PETROLOGY_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PETROLOGY_OPTION, 60000, 1;
```

---

### SC_CURSED_SOIL

<!-- RAG_CHUNK: 03_SC_CURSED_SOIL -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CURSED_SOIL, 60000, 1;
```

---

### SC_CURSED_SOIL_OPTION

<!-- RAG_CHUNK: 03_SC_CURSED_SOIL_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_CURSED_SOIL_OPTION, 60000, 1;
```

---

### SC_UPHEAVAL

<!-- RAG_CHUNK: 03_SC_UPHEAVAL -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_UPHEAVAL, 60000, 1;
```

---

### SC_UPHEAVAL_OPTION

<!-- RAG_CHUNK: 03_SC_UPHEAVAL_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_UPHEAVAL_OPTION, 60000, 1;
```

---

### SC_TIDAL_WEAPON

<!-- RAG_CHUNK: 03_SC_TIDAL_WEAPON -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_TIDAL_WEAPON, 60000, 1;
```

---

### SC_TIDAL_WEAPON_OPTION

<!-- RAG_CHUNK: 03_SC_TIDAL_WEAPON_OPTION -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_TIDAL_WEAPON_OPTION, 60000, 1;
```

---

### SC_ROCK_CRUSHER

<!-- RAG_CHUNK: 03_SC_ROCK_CRUSHER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ROCK_CRUSHER, 60000, 1;
```

---

### SC_ROCK_CRUSHER_ATK

<!-- RAG_CHUNK: 03_SC_ROCK_CRUSHER_ATK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ROCK_CRUSHER_ATK, 60000, 1;
```

---

### SC_LEADERSHIP

<!-- RAG_CHUNK: 03_SC_LEADERSHIP -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_LEADERSHIP, 60000, 1;
```

---

### SC_GLORYWOUNDS

<!-- RAG_CHUNK: 03_SC_GLORYWOUNDS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GLORYWOUNDS, 60000, 1;
```

---

### SC_SOULCOLD

<!-- RAG_CHUNK: 03_SC_SOULCOLD -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SOULCOLD, 60000, 1;
```

---

### SC_HAWKEYES

<!-- RAG_CHUNK: 03_SC_HAWKEYES -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_HAWKEYES, 60000, 1;
```

---

### SC_ODINS_POWER

<!-- RAG_CHUNK: 03_SC_ODINS_POWER -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ODINS_POWER, 60000, 1;
```

---

### SC_RAID

<!-- RAG_CHUNK: 03_SC_RAID -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_RAID, 60000, 1;
```

---

### SC_FIRE_INSIGNIA

<!-- RAG_CHUNK: 03_SC_FIRE_INSIGNIA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_FIRE_INSIGNIA, 60000, 1;
```

---

### SC_WATER_INSIGNIA

<!-- RAG_CHUNK: 03_SC_WATER_INSIGNIA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WATER_INSIGNIA, 60000, 1;
```

---

### SC_WIND_INSIGNIA

<!-- RAG_CHUNK: 03_SC_WIND_INSIGNIA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_WIND_INSIGNIA, 60000, 1;
```

---

### SC_EARTH_INSIGNIA

<!-- RAG_CHUNK: 03_SC_EARTH_INSIGNIA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_EARTH_INSIGNIA, 60000, 1;
```

---

### SC_PUSH_CART

<!-- RAG_CHUNK: 03_SC_PUSH_CART -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PUSH_CART, 60000, 1;
```

---

### SC_SPELLBOOK1

<!-- RAG_CHUNK: 03_SC_SPELLBOOK1 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPELLBOOK1, 60000, 1;
```

---

### SC_SPELLBOOK2

<!-- RAG_CHUNK: 03_SC_SPELLBOOK2 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPELLBOOK2, 60000, 1;
```

---

### SC_SPELLBOOK3

<!-- RAG_CHUNK: 03_SC_SPELLBOOK3 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPELLBOOK3, 60000, 1;
```

---

### SC_SPELLBOOK4

<!-- RAG_CHUNK: 03_SC_SPELLBOOK4 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPELLBOOK4, 60000, 1;
```

---

### SC_SPELLBOOK5

<!-- RAG_CHUNK: 03_SC_SPELLBOOK5 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPELLBOOK5, 60000, 1;
```

---

### SC_SPELLBOOK6

<!-- RAG_CHUNK: 03_SC_SPELLBOOK6 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_SPELLBOOK6, 60000, 1;
```

---

### SC_MAXSPELLBOOK

<!-- RAG_CHUNK: 03_SC_MAXSPELLBOOK -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MAXSPELLBOOK, 60000, 1;
```

---

### SC_INCMHP

<!-- RAG_CHUNK: 03_SC_INCMHP -->

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

<!-- RAG_CHUNK: 03_SC_INCMSP -->

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

<!-- RAG_CHUNK: 03_SC_PARTYFLEE -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_PARTYFLEE, 60000, 1;
```

---

### SC_MEIKYOUSISUI

<!-- RAG_CHUNK: 03_SC_MEIKYOUSISUI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_MEIKYOUSISUI, 60000, 1;
```

---

### SC_JYUMONJIKIRI

<!-- RAG_CHUNK: 03_SC_JYUMONJIKIRI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_JYUMONJIKIRI, 60000, 1;
```

---

### SC_KYOUGAKU

<!-- RAG_CHUNK: 03_SC_KYOUGAKU -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KYOUGAKU, 60000, 1;
```

---

### SC_IZAYOI

<!-- RAG_CHUNK: 03_SC_IZAYOI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_IZAYOI, 60000, 1;
```

---

### SC_ZENKAI

<!-- RAG_CHUNK: 03_SC_ZENKAI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ZENKAI, 60000, 1;
```

---

### SC_KAGEHUMI

<!-- RAG_CHUNK: 03_SC_KAGEHUMI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KAGEHUMI, 60000, 1;
```

---

### SC_KYOMU

<!-- RAG_CHUNK: 03_SC_KYOMU -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KYOMU, 60000, 1;
```

---

### SC_KAGEMUSYA

<!-- RAG_CHUNK: 03_SC_KAGEMUSYA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_KAGEMUSYA, 60000, 1;
```

---

### SC_ZANGETSU

<!-- RAG_CHUNK: 03_SC_ZANGETSU -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ZANGETSU, 60000, 1;
```

---

### SC_GENSOU

<!-- RAG_CHUNK: 03_SC_GENSOU -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_GENSOU, 60000, 1;
```

---

### SC_AKAITSUKI

<!-- RAG_CHUNK: 03_SC_AKAITSUKI -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_AKAITSUKI, 60000, 1;
```

---

### SC_STYLE_CHANGE

<!-- RAG_CHUNK: 03_SC_STYLE_CHANGE -->

**Effect:** Eleanor's mode

**Script Example:**
```c
sc_start SC_STYLE_CHANGE, 60000, 1;
```

---

### SC_TINDER_BREAKER

<!-- RAG_CHUNK: 03_SC_TINDER_BREAKER -->

**Icon (EFST):** `EFST_TINDER_BREAKER_POSTDELAY`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_TINDER_BREAKER, 60000, 1;
```

---

### SC_TINDER_BREAKER2

<!-- RAG_CHUNK: 03_SC_TINDER_BREAKER2 -->

**Icon (EFST):** `EFST_TINDER_BREAKER`

**Effect:** Tinder Breaker after-effect, just like Close Confine

**Script Example:**
```c
sc_start SC_TINDER_BREAKER2, 60000, 1;
```

---

### SC_CBC

<!-- RAG_CHUNK: 03_SC_CBC -->

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

<!-- RAG_CHUNK: 03_SC_EQC -->

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

<!-- RAG_CHUNK: 03_SC_GOLDENE_FERSE -->

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

<!-- RAG_CHUNK: 03_SC_ANGRIFFS_MODUS -->

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

<!-- RAG_CHUNK: 03_SC_OVERED_BOOST -->

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

<!-- RAG_CHUNK: 03_SC_LIGHT_OF_REGENE -->

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

<!-- RAG_CHUNK: 03_SC_ASH -->

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

<!-- RAG_CHUNK: 03_SC_GRANITIC_ARMOR -->

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

<!-- RAG_CHUNK: 03_SC_MAGMA_FLOW -->

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

<!-- RAG_CHUNK: 03_SC_PYROCLASTIC -->

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

<!-- RAG_CHUNK: 03_SC_PARALYSIS -->

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

<!-- RAG_CHUNK: 03_SC_PAIN_KILLER -->

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

<!-- RAG_CHUNK: 03_SC_HANBOK -->

**Effect:** Visual effect. Hanbok costume!

**Script Example:**
```c
sc_start SC_HANBOK, 60000, 1;
```

---

### SC_DEFSET

<!-- RAG_CHUNK: 03_SC_DEFSET -->

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

<!-- RAG_CHUNK: 03_SC_MDEFSET -->

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

<!-- RAG_CHUNK: 03_SC_DARKCROW -->

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

<!-- RAG_CHUNK: 03_SC_FULL_THROTTLE -->

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

<!-- RAG_CHUNK: 03_SC_REBOUND -->

**Icon (EFST):** `EFST_REBOUND`

**Effect:** Full Throttle  after-effect. Reduce walk speed

**Script Example:**
```c
sc_start SC_REBOUND, 60000, 1;
```

---

### SC_UNLIMIT

<!-- RAG_CHUNK: 03_SC_UNLIMIT -->

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

<!-- RAG_CHUNK: 03_SC_KINGS_GRACE -->

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

<!-- RAG_CHUNK: 03_SC_TELEKINESIS_INTENSE -->

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

<!-- RAG_CHUNK: 03_SC_OFFERTORIUM -->

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

<!-- RAG_CHUNK: 03_SC_FRIGG_SONG -->

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

<!-- RAG_CHUNK: 03_SC_MONSTER_TRANSFORM -->

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

<!-- RAG_CHUNK: 03_SC_ANGEL_PROTECT -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ANGEL_PROTECT, 60000, 1;
```

---

### SC_ILLUSIONDOPING

<!-- RAG_CHUNK: 03_SC_ILLUSIONDOPING -->

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

<!-- RAG_CHUNK: 03_SC_FLASHCOMBO -->

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

<!-- RAG_CHUNK: 03_SC_MOONSTAR -->

**Icon (EFST):** `EFST_MOONSTAR`

**Effect:** Visual effect

**Script Example:**
```c
sc_start SC_MOONSTAR, 60000, 1;
```

---

### SC_SUPER_STAR

<!-- RAG_CHUNK: 03_SC_SUPER_STAR -->

**Icon (EFST):** `EFST_SUPER_STAR`

**Effect:** Visual effect

**Script Example:**
```c
sc_start SC_SUPER_STAR, 60000, 1;
```

---

### SC_HEAT_BARREL

<!-- RAG_CHUNK: 03_SC_HEAT_BARREL -->

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

<!-- RAG_CHUNK: 03_SC_P_ALTER -->

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

<!-- RAG_CHUNK: 03_SC_E_CHAIN -->

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

<!-- RAG_CHUNK: 03_SC_C_MARKER -->

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

<!-- RAG_CHUNK: 03_SC_ANTI_M_BLAST -->

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

<!-- RAG_CHUNK: 03_SC_B_TRAP -->

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

<!-- RAG_CHUNK: 03_SC_H_MINE -->

**Icon (EFST):** `EFST_H_MINE`

**Effect:** (Rebellion) Howling Mine effect, waiting for Flicker to be used

**Script Example:**
```c
sc_start SC_H_MINE, 60000, 1;
```

---

### SC_QD_SHOT_READY

<!-- RAG_CHUNK: 03_SC_QD_SHOT_READY -->

**Icon (EFST):** `EFST_E_QD_SHOT_READY`

**Effect:** (Rebellion) Combo stance to cast Quick Draw Shot

**Script Example:**
```c
sc_start SC_QD_SHOT_READY, 60000, 1;
```

---

### SC_MTF_ASPD

<!-- RAG_CHUNK: 03_SC_MTF_ASPD -->

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

<!-- RAG_CHUNK: 03_SC_MTF_ASPD2 -->

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

<!-- RAG_CHUNK: 03_SC_MTF_RANGEATK -->

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

<!-- RAG_CHUNK: 03_SC_MTF_RANGEATK2 -->

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

<!-- RAG_CHUNK: 03_SC_MTF_MATK -->

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

<!-- RAG_CHUNK: 03_SC_MTF_MATK2 -->

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

<!-- RAG_CHUNK: 03_SC_MTF_MLEATKED -->

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

<!-- RAG_CHUNK: 03_SC_MTF_CRIDAMAGE -->

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

<!-- RAG_CHUNK: 03_SC_OKTOBERFEST -->

**Effect:** Costume

**Script Example:**
```c
sc_start SC_OKTOBERFEST, 60000, 1;
```

---

### SC_STRANGELIGHTS

<!-- RAG_CHUNK: 03_SC_STRANGELIGHTS -->

**Icon (EFST):** `EFST_STRANGELIGHTS`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_STRANGELIGHTS, 60000, 1;
```

---

### SC_DECORATION_OF_MUSIC

<!-- RAG_CHUNK: 03_SC_DECORATION_OF_MUSIC -->

**Icon (EFST):** `EFST_DECORATION_OF_MUSIC`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_DECORATION_OF_MUSIC, 60000, 1;
```

---

### SC_QUEST_BUFF1

<!-- RAG_CHUNK: 03_SC_QUEST_BUFF1 -->

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

<!-- RAG_CHUNK: 03_SC_QUEST_BUFF2 -->

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

<!-- RAG_CHUNK: 03_SC_QUEST_BUFF3 -->

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

<!-- RAG_CHUNK: 03_SC_ALL_RIDING -->

**Icon (EFST):** `EFST_ALL_RIDING`

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_ALL_RIDING, 60000, 1;
```

---

### SC_TEARGAS_SOB

<!-- RAG_CHUNK: 03_SC_TEARGAS_SOB -->

**Effect:** 2nd Teargas effect, do /sob expression each 3 seconds

**Script Example:**
```c
sc_start SC_TEARGAS_SOB, 60000, 1;
```

---

### SC__FEINTBOMB

<!-- RAG_CHUNK: 03_SC__FEINTBOMB -->

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

<!-- RAG_CHUNK: 03_SC__CHAOS -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC__CHAOS, 60000, 1;
```

---

### SC_ELEMENTAL_SHIELD

<!-- RAG_CHUNK: 03_SC_ELEMENTAL_SHIELD -->

**Effect:** Block magic attack

**Script Example:**
```c
sc_start SC_ELEMENTAL_SHIELD, 60000, 1;
```

---

### SC_CHASEWALK2

<!-- RAG_CHUNK: 03_SC_CHASEWALK2 -->

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

<!-- RAG_CHUNK: 03_SC_SUHIDE -->

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

<!-- RAG_CHUNK: 03_SC_SU_STOOP -->

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

<!-- RAG_CHUNK: 03_SC_SPRITEMABLE -->

**Icon (EFST):** `EFST_SPRITEMABLE`

**Effect:** Increase 1000 HP and 100 SP.

**Script Example:**
```c
sc_start SC_SPRITEMABLE, 60000, 1;
```

---

### SC_CATNIPPOWDER

<!-- RAG_CHUNK: 03_SC_CATNIPPOWDER -->

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

<!-- RAG_CHUNK: 03_SC_SV_ROOTTWIST -->

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

<!-- RAG_CHUNK: 03_SC_BITESCAR -->

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

<!-- RAG_CHUNK: 03_SC_ARCLOUSEDASH -->

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

<!-- RAG_CHUNK: 03_SC_TUNAPARTY -->

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

<!-- RAG_CHUNK: 03_SC_SHRIMP -->

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

<!-- RAG_CHUNK: 03_SC_FRESHSHRIMP -->

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

<!-- RAG_CHUNK: 03_SC_HISS -->

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

<!-- RAG_CHUNK: 03_SC_NYANGGRASS -->

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

<!-- RAG_CHUNK: 03_SC_GROOMING -->

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

<!-- RAG_CHUNK: 03_SC_SHRIMPBLESSING -->

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

<!-- RAG_CHUNK: 03_SC_CHATTERING -->

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

<!-- RAG_CHUNK: 03_SC_DORAM_WALKSPEED -->

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

<!-- RAG_CHUNK: 03_SC_DORAM_MATK -->

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

<!-- RAG_CHUNK: 03_SC_DORAM_FLEE2 -->

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

<!-- RAG_CHUNK: 03_SC_DORAM_SVSP -->

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

<!-- RAG_CHUNK: 03_SC_GVG_GIANT -->

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

<!-- RAG_CHUNK: 03_SC_GVG_GOLEM -->

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

<!-- RAG_CHUNK: 03_SC_GVG_STUN -->

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

<!-- RAG_CHUNK: 03_SC_GVG_STONE -->

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

<!-- RAG_CHUNK: 03_SC_GVG_FREEZ -->

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

<!-- RAG_CHUNK: 03_SC_GVG_SLEEP -->

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

<!-- RAG_CHUNK: 03_SC_GVG_CURSE -->

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

<!-- RAG_CHUNK: 03_SC_GVG_SILENCE -->

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

<!-- RAG_CHUNK: 03_SC_GVG_BLIND -->

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

<!-- RAG_CHUNK: 03_SC_EXTREMITYFIST2 -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_EXTREMITYFIST2, 60000, 1;
```

---

### SC_LHZ_DUN_N1

<!-- RAG_CHUNK: 03_SC_LHZ_DUN_N1 -->

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

<!-- RAG_CHUNK: 03_SC_LHZ_DUN_N2 -->

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

<!-- RAG_CHUNK: 03_SC_LHZ_DUN_N3 -->

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

<!-- RAG_CHUNK: 03_SC_LHZ_DUN_N4 -->

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

<!-- RAG_CHUNK: 03_SC_DORAM_BUF_01 -->

**Effect:** Recovers 10 HP every 10 seconds.

**Script Example:**
```c
sc_start SC_DORAM_BUF_01, 60000, 1;
```

---

### SC_DORAM_BUF_02

<!-- RAG_CHUNK: 03_SC_DORAM_BUF_02 -->

**Effect:** Recovers 5 SP every 10 seconds.

**Script Example:**
```c
sc_start SC_DORAM_BUF_02, 60000, 1;
```

---

### SC_INCREASE_MAXHP

<!-- RAG_CHUNK: 03_SC_INCREASE_MAXHP -->

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

<!-- RAG_CHUNK: 03_SC_INCREASE_MAXSP -->

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

<!-- RAG_CHUNK: 03_SC_REF_T_POTION -->

**Icon (EFST):** `EFST_REF_T_POTION`

**Effect:** Decreases reflected damage by 100%.

**Script Example:**
```c
sc_start SC_REF_T_POTION, 60000, 1;
```

---

### SC_ADD_ATK_DAMAGE

<!-- RAG_CHUNK: 03_SC_ADD_ATK_DAMAGE -->

**Icon (EFST):** `EFST_ADD_ATK_DAMAGE`

**Effect:** Increases melee physical damage by 15%. Increases ranged physical damage by 15%.

**Script Example:**
```c
sc_start SC_ADD_ATK_DAMAGE, 60000, 1;
```

---

### SC_ADD_MATK_DAMAGE

<!-- RAG_CHUNK: 03_SC_ADD_MATK_DAMAGE -->

**Icon (EFST):** `EFST_ADD_MATK_DAMAGE`

**Effect:** Increases all elemental magical damage by 15%.

**Script Example:**
```c
sc_start SC_ADD_MATK_DAMAGE, 60000, 1;
```

---

### SC_HELPANGEL

<!-- RAG_CHUNK: 03_SC_HELPANGEL -->

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

<!-- RAG_CHUNK: 03_SC_SOUNDOFDESTRUCTION -->

**Icon (EFST):** `EFST_SOUND_OF_DESTRUCTION`

**Effect:** Doubles incoming damage for 10 seconds.

**Script Example:**
```c
sc_start SC_SOUNDOFDESTRUCTION, 60000, 1;
```

---

### SC_LUXANIMA

<!-- RAG_CHUNK: 03_SC_LUXANIMA -->

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

<!-- RAG_CHUNK: 03_SC_REUSE_LIMIT_LUXANIMA -->

**Effect:** (See source code for details)

**Script Example:**
```c
sc_start SC_REUSE_LIMIT_LUXANIMA, 60000, 1;
```

---

### SC_ENSEMBLEFATIGUE

<!-- RAG_CHUNK: 03_SC_ENSEMBLEFATIGUE -->

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

<!-- RAG_CHUNK: 03_SC_MISTY_FROST -->

**Icon (EFST):** `EFST_MISTY_FROST`

**Effect:** Freezing.

**Script Example:**
```c
sc_start SC_MISTY_FROST, 60000, 1;
```

---

### SC_MAGIC_POISON

<!-- RAG_CHUNK: 03_SC_MAGIC_POISON -->

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

<!-- RAG_CHUNK: 03_SC_EP16_2_BUFF_SS -->

**Icon (EFST):** `EFST_EP16_2_BUFF_SS`

**Effect:** ASPD +10.

**Script Example:**
```c
sc_start SC_EP16_2_BUFF_SS, 60000, 1;
```

---

### SC_EP16_2_BUFF_SC

<!-- RAG_CHUNK: 03_SC_EP16_2_BUFF_SC -->

**Icon (EFST):** `EFST_EP16_2_BUFF_SC`

**Effect:** CRIT +30.

**Script Example:**
```c
sc_start SC_EP16_2_BUFF_SC, 60000, 1;
```

---

### SC_EP16_2_BUFF_AC

<!-- RAG_CHUNK: 03_SC_EP16_2_BUFF_AC -->

**Icon (EFST):** `EFST_EP16_2_BUFF_AC`

**Effect:** Reduce variable cast time by 80%.

**Script Example:**
```c
sc_start SC_EP16_2_BUFF_AC, 60000, 1;
```

---

### SC_EMERGENCY_MOVE

<!-- RAG_CHUNK: 03_SC_EMERGENCY_MOVE -->

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

<!-- RAG_CHUNK: 03_SC_PACKING_ENVELOPE1 -->

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

<!-- RAG_CHUNK: 03_SC_PACKING_ENVELOPE2 -->

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

<!-- RAG_CHUNK: 03_SC_PACKING_ENVELOPE3 -->

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

<!-- RAG_CHUNK: 03_SC_PACKING_ENVELOPE4 -->

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

<!-- RAG_CHUNK: 03_SC_PACKING_ENVELOPE5 -->

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

<!-- RAG_CHUNK: 03_SC_PACKING_ENVELOPE6 -->

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

<!-- RAG_CHUNK: 03_SC_PACKING_ENVELOPE7 -->

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

<!-- RAG_CHUNK: 03_SC_PACKING_ENVELOPE8 -->

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

<!-- RAG_CHUNK: 03_SC_PACKING_ENVELOPE9 -->

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

<!-- RAG_CHUNK: 03_SC_PACKING_ENVELOPE10 -->

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

<!-- RAG_CHUNK: 03_SC_BATH_FOAM_A -->

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

<!-- RAG_CHUNK: 03_SC_BATH_FOAM_B -->

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

<!-- RAG_CHUNK: 03_SC_BATH_FOAM_C -->

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

<!-- RAG_CHUNK: 03_SC_BUCHEDENOEL -->

**Icon (EFST):** `EFST_BUCHEDENOEL`

**Effect:** Increases HP & SP restoration by 3%, Hit +3, and Critical +7.

**Script Example:**
```c
sc_start SC_BUCHEDENOEL, 60000, 1;
```

---

### SC_EP16_DEF

<!-- RAG_CHUNK: 03_SC_EP16_DEF -->

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

<!-- RAG_CHUNK: 03_SC_STR_SCROLL -->

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

<!-- RAG_CHUNK: 03_SC_INT_SCROLL -->

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

<!-- RAG_CHUNK: 03_SC_CONTENTS_1 -->

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

<!-- RAG_CHUNK: 03_SC_CONTENTS_2 -->

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

<!-- RAG_CHUNK: 03_SC_CONTENTS_3 -->

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

<!-- RAG_CHUNK: 03_SC_CONTENTS_4 -->

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

<!-- RAG_CHUNK: 03_SC_CONTENTS_5 -->

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

<!-- RAG_CHUNK: 03_SC_CONTENTS_6 -->

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

<!-- RAG_CHUNK: 03_SC_CONTENTS_7 -->

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

<!-- RAG_CHUNK: 03_SC_CONTENTS_8 -->

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

<!-- RAG_CHUNK: 03_SC_CONTENTS_9 -->

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

<!-- RAG_CHUNK: 03_SC_CONTENTS_10 -->

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
<!-- RAG_CHUNK: 03_complete_sc_list -->

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

---

<!-- RAG_CHUNK: 03_status_database_structure -->
## Part 3: Status Database Structure (status.yml)

> Source: `doc/status.txt` (321 lines)

This section explains the structure of `db/status.yml` and all available flags/options.

### Status Field Reference

#### Status
Status change name. See `src/map/script_constants.hpp` for SC_* constants.

#### Icon
Status change icon or client effect displayed client-side. See `src/map/script_constants.hpp` for EFST_* constants.

#### DurationLookup
Used for default duration lookup in `skill_db.yml`. The duration used is `Duration2` defined for the skill linked. If different durations are defined per level, level 7 is used.

### States

States given when the SC is active:

| State | Description |
|-------|-------------|
| None | No special state (Default) |
| NoMove | Cannot move |
| NoMoveCond | Condition check for SCS_NOMOVE |
| NoPickItem | Cannot pick item |
| NoPickItemCond | Condition check for SCS_NOPICKITEM |
| NoDropItem | Cannot drop item |
| NoDropItemCond | Condition check for SCS_NODROPITEM |
| NoCast | Cannot cast a skill |
| NoCastCond | Condition check for SCS_NOCAST |
| NoChat | Cannot chat and open chat room |
| NoChatCond | Condition check for SCS_NOCHATCOND |
| NoEquipItem | Cannot put on equipment |
| NoEquipItemCond | Condition check for SCS_NOEQUIPITEM |
| NoUnEquipItem | Cannot put off equipment |
| NoUnEquipItemCond | Condition check for SCS_NOUNEQUIPITEM |
| NoConsumeItem | Cannot consume item |
| NoConsumeItemCond | Condition check for SCS_NOCONSUMEITEM |
| NoAttack | Cannot attack |
| NoAttackCond | Condition check for SCS_NOATTACK |
| NoWarp | Cannot warp |
| NoWarpCond | Condition check for SCS_NOWARP |
| NoDeathPenalty | Cannot lose experience on death |
| NoDeathPenaltyCond | Condition check for SCS_NODEATHPENALTY |
| NoInteract | Cannot interact with client (sit/stand or talk with NPC) |
| NoInteractCond | Condition check for SCS_NOINTERACT |

> States with "Cond" suffix have hard coded conditions in `status.cpp::status_calc_state`

### CalcFlags

Flag indicating which status calculation is performed:

| Flag | Description |
|------|-------------|
| None | Calculates nothing (Default) |
| Base | Base status |
| MaxHp | Maximum HP |
| MaxSp | Maximum SP |
| Str | STR |
| Agi | AGI |
| Vit | VIT |
| Int | INT |
| Dex | DEX |
| Luk | LUK |
| Batk | Base Attack |
| Watk | Weapon Attack |
| Matk | Magic Attack |
| Hit | Hit/accuracy rate |
| Flee | Flee/dodge rate |
| Def | Equipment Defense |
| Def2 | Defense |
| Mdef | Equipment Magic Defense |
| Mdef2 | Magic Defense |
| Speed | Walk speed |
| Aspd | Attack speed |
| Dspd | Damage delay speed |
| Cri | Critical rate |
| Flee2 | Perfect dodge rate |
| Atk_Ele | Attack Element |
| Def_Ele | Defense Element |
| Mode | Mode |
| Size | Size |
| Race | Race |
| Range | Range |
| Regen | Regeneration |
| MaxAp | Maximum AP |
| Pow | POW |
| Sta | STA |
| Wis | WIS |
| Spl | SPL |
| Con | CON |
| Crt | CRT |
| Patk | Physical Power |
| Smatk | Spell Magic Attack |
| Res | Physical Resistance |
| Mres | Magic Resistance |
| Hplus | Heal Plus |
| Crate | Critical Rate |
| Dye | Dye |
| All | Calculates all CalcFlags |

### Opt1 (BODYSTATE)

Special effect when status is active. Not stackable:

| Option | Description |
|--------|-------------|
| None | No effect (Default) |
| Stone | Stone curse effect |
| StoneWait | Stone curse incubation effect |
| Freeze | Freeze effect |
| Stun | Stun effect |
| Sleep | Sleep effect |
| Burning | Burning effect |
| Imprison | Imprison effect |
| Crystalize | Crystalize effect |

### Opt2 (HEALTHSTATE)

Special client effect when status is active:

| Option | Description |
|--------|-------------|
| None | No effect (Default) |
| Poison | Poisoned effect |
| Curse | Cursed effect |
| Silence | Silenced effect |
| SignumCrucis | Signum Crucis effect |
| Blind | Blind effect |
| Angelus | Angelus effect |
| Bleeding | Bleeding effect |
| Dpoison | Heavy Poisoned effect |
| Fear | Fear effect |

### Opt3 (SHOW_EFST)

Special visual effect when status is active:

| Option | Description |
|--------|-------------|
| Normal | No effect (Default) |
| Quicken | Quicken effect |
| OverThrust | Overthrust effect |
| EnergyCoat | Energy Coat effect |
| ExplosionSpirits | Explosion Spirits effect |
| SteelBody | Steel Body effect |
| BladeStop | Blade Stop effect |
| AuraBlade | Aura Blade effect |
| Berserk | Berserk effect |
| LightBlade | Light Blade effect |
| Moonlit | Moonlit effect |
| Marionette | Marionette effect |
| Assumptio | Assumptio effect |
| Warm | Warm effect |
| Kaite | Kaite effect |
| Bunsin | Bunshin effect |
| SoulLink | Soul Link effect |
| Undead | Undead effect |
| Contract | Contract effect |

### Options (Visual States)

Special visual state when status is active:

| Option | Description |
|--------|-------------|
| Nothing | No effect (Default) |
| Sight | Sight effect |
| Hide | Hide effect |
| Cloak | Cloaking effect |
| Falcon | Falcon effect |
| Riding | Riding effect |
| Invisible | Invisible effect |
| Orcish | Orcish effect (the ugly face!) |
| Wedding | Wedding costume |
| Ruwach | Ruwach effect |
| ChaseWalk | Chasewalk effect |
| Flying | Flying effect (Star Gladiator Union) |
| Xmas | Christmas costume |
| Transform | Transformation |
| Summer | Summer costume |
| Dragon1-5 | Dragon mount variants |
| Wug | Wug |
| WugRider | Riding a Wug |
| Madogear | Madogear |
| Hanbok | Hanbok costume |
| Oktoberfest | Oktoberfest costume |

### Flags

Various status flags for specific events:

#### Display Flags
| Flag | Description |
|------|-------------|
| BlEffect | Status has BL_SCEFFECT as relevant effect |
| DisplayPc | Displays status effect when player logs in |
| DislpayNpc | Displays status effect on a NPC |
| Debuff | Status is considered a debuff |
| SetStand | Sets player to standing state |

#### Overlap/Mado Flags
| Flag | Description |
|------|-------------|
| OverlapIgnoreLevel | Status activates for any level if already active |
| FailedMado | Cannot be applied if Madogear is active |
| MadoCancel | Cancels when mounting Madogear |
| MadoEndCancel | Cancels when unmounting Madogear |

#### Removal Prevention Flags
| Flag | Description |
|------|-------------|
| NoClearbuff | Cannot be removed by status_change_clear_buffs() |
| NoForcedEnd | Cannot be removed by sc_end |
| NoRemoveOnDead | Cannot be removed when player dies |
| NoDispell | Cannot be removed by SA_DISPELL |
| NoClearance | Cannot be removed by AB_CLEARANCE |
| NoBanishingBuster | Cannot be removed by RL_BANISHING_BUSTER |
| NoSave | Won't be saved when player logs out |
| NoSaveInfinite | Infinite duration status won't be saved |

#### Removal Trigger Flags
| Flag | Description |
|------|-------------|
| RemoveOnDamaged | Removed when receiving damage |
| RemoveOnRefresh | Removed by RK_REFRESH |
| RemoveOnLuxAnima | Removed by RK_LUXANIMA |
| RemoveOnMapWarp | Removed when warping to another map |
| RemoveOnChangeMap | Removed when changing map-server |
| RemoveChemicalProtect | Removed by AM_CP_* skills |
| RemoveOnUnequip | Removed when unequipping any equipment |
| RemoveOnUnequipWeapon | Removed when unequipping weapon |
| RemoveOnUnequipArmor | Removed when unequipping armor |
| RemoveOnHermode | Removed by CG_HERMODE |

#### Action Stop Flags
| Flag | Description |
|------|-------------|
| StopAttacking | Makes unit stop attacking |
| StopCasting | Makes unit stop casting skills |
| StopWalking | Makes unit stop walking |

#### Boss Resistance Flags
| Flag | Description |
|------|-------------|
| BossResist | Cannot be applied to Boss Monster (MD_STATUS_IMMUNE) |
| MvpResist | Cannot be applied to MvP (MD_MVP) |

#### Notification Flags
| Flag | Description |
|------|-------------|
| SendOption | Sends STATE_CHANGE packet for Opt1/Opt2/Opt3 |
| SendLook | Sends STATE_CHANGE for body/look changes |
| SendVal1 | Notifies client of val1 |
| SendVal2 | Notifies client of val2 |
| SendVal3 | Notifies client of val3 |

#### Requirement Flags
| Flag | Description |
|------|-------------|
| RequireWeapon | Status requires weapon equipped |
| RequireNoWeapon | Status requires no weapon equipped |
| RequireShield | Status requires shield equipped |

### Additional Fields

| Field | Description |
|-------|-------------|
| MinDuration | Minimum duration (ms) after resistance reduction |
| MinRate | Minimum success rate (n/10000) after resistance reduction |
| Fail | List of status that causes activation to fail |
| EndOnStart | List of status that end when this status activates |
| EndReturn | List of status that end on activate and prevent effect |
| EndOnEnd | List of status that end when this status ends |
| Script | Script to execute when status starts |

### Important Notes

1. **Buff vs Debuff**: By default, statuses are 'Buff' unless given 'Debuff' flag
2. **NoClearbuff**: Prevents removal by `status_change_clear`, `status_change_clear_buffs`, `map_quit`
3. **Skill Interactions**:
   - CG_TAROTCARD, CG_HERMODE: Only remove buffs
   - PA_GOSPEL, LG_INSPIRATION: Remove buffs AND debuffs
   - RK_REFRESH, RK_LUXANIMA: Only remove with specific flags
4. **Opt1 Exclusivity**: SC_STONE, SC_FREEZE, SC_STUN, SC_SLEEP, SC_BURNING, SC_WHITEIMPRISON, SC_CRYSTALIZE cannot override each other
5. **Mado Immunity**: Madogear is immune to increase agi, wind walk, cart boost, etc.
6. **Berserk Types**: SC_BERSERK, SC_SATURDAYNIGHTFEVER, SC__BLOODYLUST do not overlap
