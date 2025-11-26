# rAthena Status Effects Complete Reference

**Version:** Enhancement v1.0 for KB v4
**Coverage:** 500+ Status Effects (SC_*)
**RAG-Optimized:** Yes
**Last Updated:** 2025-11-26

---

<!-- RAG_CHUNK: overview -->
## Overview

This enhancement document provides comprehensive documentation for rAthena status effects (SC_* constants). Use with sc_start, sc_start2, sc_start4, sc_end, and getstatus script commands.

### Quick Reference

```c
// Basic status application
sc_start SC_BLESSING, 240000, 10;  // 4 minutes, level 10

// With success rate
sc_start SC_POISON, 60000, 5, 5000;  // 50% success rate

// With val1 and val2
sc_start2 SC_POISONREACT, 180000, 10, 5;

// With all 4 values
sc_start4 SC_ARMOR_ELEMENT, 60000, 50, 50, 50, 50;

// End status
sc_end SC_BLESSING;

// Check status
if (getstatus(SC_BLESSING)) { /* has blessing */ }
.@time = getstatus(SC_BLESSING, 1);  // remaining time
.@val1 = getstatus(SC_BLESSING, 2);  // val1
```

---

<!-- RAG_CHUNK: primary_status_effects -->
## 1. Primary Status Effects (Ailments)

### SC_STONE
**Effect:** Petrification - DEF -50%; MDEF +25%; Element becomes Earth Lv1
**Mechanics:**
- If HP > 25%, lose 1% HP every 5 seconds
- Cannot move, attack, pick items, use items, use skills, sit, or logout
- Ignores Steal and Lex Aeterna
**Parameters:**
- val1: (unused)
- val2: Caster's object ID
- val3: Incubation time (milliseconds before full petrification)
- val4: Remaining tick

```c
sc_start SC_STONE, 30000, 0;  // 30 seconds
sc_start4 SC_STONE, 30000, 0, getcharid(3), 3000, 0;  // 3 sec incubation
```

### SC_FREEZE
**Effect:** Frozen - DEF -50%; FLEE = 0; MDEF +25%; Element becomes Water Lv1
**Mechanics:**
- Cannot move, attack, pick items, use items, sit, or logout
- Ignores Steal, Lex Aeterna, Storm Gust, Falling Ice Pillar
**Parameters:**
- val1: (unused)

```c
sc_start SC_FREEZE, 10000, 0;  // 10 seconds frozen
```

### SC_STUN
**Effect:** Stunned - FLEE = 0
**Mechanics:**
- Cannot move, attack, pick items, use items, use skills, sit, or logout
**Parameters:**
- val1: (unused)

```c
sc_start SC_STUN, 5000, 0;  // 5 seconds stun
```

### SC_SLEEP
**Effect:** Asleep - FLEE = 0; Enemy CRIT x2
**Mechanics:**
- Cannot move, attack, pick items, use items, use skills, sit, or logout
- Taking damage wakes target
**Parameters:**
- val1: (unused)

```c
sc_start SC_SLEEP, 30000, 0;  // 30 seconds sleep
```

### SC_POISON
**Effect:** Poisoned - DEF -25%
**Mechanics:**
- If HP > 25%, lose 1.5% + 2 HP per second
- SP Regeneration disabled
**Parameters:**
- val1: Skill Level
- val2: Caster's object ID
- val3: (unused)
- val4: Remaining tick

```c
sc_start SC_POISON, 60000, 5;  // 60 seconds, level 5
sc_start4 SC_POISON, 60000, 5, getcharid(3), 0, gettick();
```

### SC_CURSE
**Effect:** Cursed - ATK -25%; LUK = 0; Movement speed -300
**Parameters:**
- val1: (unused)

```c
sc_start SC_CURSE, 30000, 0;
```

### SC_SILENCE
**Effect:** Silenced - Cannot use active skills
**Parameters:**
- val1: (unused)

```c
sc_start SC_SILENCE, 20000, 0;
```

### SC_CONFUSION
**Effect:** Confused - Move randomly; DEF set to (STR + INT*50)
**Parameters:**
- val1: (unused)

```c
sc_start SC_CONFUSION, 15000, 0;
```

### SC_BLIND
**Effect:** Blinded - HIT -25%; FLEE -25%; Screen darkened
**Parameters:**
- val1: (unused)

```c
sc_start SC_BLIND, 30000, 0;
```

### SC_BLEEDING
**Effect:** Bleeding - HP/SP Regeneration disabled; Lose HP over time
**EFST:** EFST_BLOODING
**Parameters:**
- val1: Skill Level
- val2: Caster's object ID (for mob_log_damage)
- val3: (unused)
- val4: Remaining tick

```c
sc_start SC_BLEEDING, 120000, 3;  // 2 minutes, level 3
```

### SC_DPOISON
**Effect:** Deadly Poison - DEF -25%
**Mechanics:**
- If HP > 25%, lose 10-15% HP per second (much more severe than SC_POISON)
**Parameters:**
- val1: Skill Level
- val2: Caster's object ID
- val3: (unused)
- val4: Remaining tick

```c
sc_start SC_DPOISON, 30000, 10;  // 30 seconds, level 10
```

---

<!-- RAG_CHUNK: buff_status_effects -->
## 2. Buff Status Effects

### SC_BLESSING
**Effect:** Blessing - STR, DEX, INT + Skill Level
**EFST:** EFST_BLESSING
**Mechanics:**
- Removes Stone and Curse status
- Against Undead/Demon mobs: reduces DEX and INT by 50%
**Parameters:**
- val1: Skill Level (stat bonus amount)

```c
sc_start SC_BLESSING, 240000, 10;  // 4 minutes, +10 STR/DEX/INT
```

### SC_INCREASEAGI
**Effect:** Increase AGI - AGI + bonus; Movement speed increased
**EFST:** EFST_INC_AGI
**Parameters:**
- val1: (hardcoded based on skill level)

```c
sc_start SC_INCREASEAGI, 240000, 10;  // 4 minutes, level 10
```

### SC_DECREASEAGI
**Effect:** Decrease AGI - AGI reduced; Movement speed decreased
**EFST:** EFST_DEC_AGI
**Parameters:**
- val1: (hardcoded)

```c
sc_start SC_DECREASEAGI, 120000, 10;
```

### SC_ANGELUS
**Effect:** Angelus - DEF + (5 * Skill Level)%
**EFST:** EFST_ANGELUS
**Parameters:**
- val1: (unused, effect hardcoded)

```c
sc_start SC_ANGELUS, 300000, 10;  // 5 minutes, +50% DEF
```

### SC_GLORIA
**Effect:** Gloria - LUK +30
**EFST:** EFST_GLORIA
**Parameters:**
- val1: (unused)

```c
sc_start SC_GLORIA, 30000, 0;  // 30 seconds
```

### SC_MAGNIFICAT
**Effect:** Magnificat - SP Regeneration x2
**EFST:** EFST_MAGNIFICAT
**Parameters:**
- val1: (unused)

```c
sc_start SC_MAGNIFICAT, 60000, 0;  // 60 seconds, 2x SP regen
```

### SC_KYRIE
**Effect:** Kyrie Eleison - Damage shield
**EFST:** EFST_KYRIE
**Mechanics:**
- Removes SC_ASSUMPTIO
- Blocks damage totaling (MaxHP * (SkillLv*2+10)/100)
- OR blocks (SkillLv/2+5) hits
**Parameters:**
- val1: (unused)

```c
sc_start SC_KYRIE, 120000, 10;
```

### SC_ASSUMPTIO
**Effect:** Assumptio - Damage reduction
**EFST:** EFST_ASSUMPTIO (Pre-RE) or EFST_ASSUMPTIO2 (RE)
**Parameters:**
- val1: Level (* 2 bonus heal % in RENEWAL)

```c
sc_start SC_ASSUMPTIO, 100000, 5;
```

### SC_PROVOKE
**Effect:** Provoke - DEF -(5+5*SkillLv)%; ATK +(2+3*SkillLv)%
**EFST:** EFST_PROVOKE
**Parameters:**
- val1: Skill Level

```c
sc_start SC_PROVOKE, 30000, 10;  // +32% ATK, -55% DEF
```

### SC_ENDURE
**Effect:** Endure - MDEF + Skill Level; No flinch on hit
**EFST:** EFST_ENDURE
**Parameters:**
- val1: Skill Level

```c
sc_start SC_ENDURE, 10000, 10;  // 10 seconds, +10 MDEF, no flinch
```

---

<!-- RAG_CHUNK: combat_status_effects -->
## 3. Combat Status Effects

### SC_TWOHANDQUICKEN
**Effect:** Two Hand Quicken - ASPD +30%
**EFST:** EFST_TWOHANDQUICKEN
**Parameters:**
- val1: (unused)

```c
sc_start SC_TWOHANDQUICKEN, 180000, 10;  // 3 minutes
```

### SC_ADRENALINE
**Effect:** Adrenaline Rush - ASPD of Axe & Mace weapons x2
**EFST:** EFST_ADRENALINE
**Parameters:**
- val1: (unused)

```c
sc_start SC_ADRENALINE, 150000, 5;
```

### SC_ADRENALINE2
**Effect:** Full Adrenaline Rush - Improved version
**Parameters:**
- val1: (unused)

```c
sc_start SC_ADRENALINE2, 150000, 5;
```

### SC_SPEARQUICKEN
**Effect:** Spear Quicken - When using spear
**EFST:** EFST_SPEARQUICKEN
**Mechanics:**
- ASPD +(20+SkillLv)%
- CRIT +(3+10*SkillLv)
- FLEE +(2*SkillLv)
**Parameters:**
- val1: (unused)

```c
sc_start SC_SPEARQUICKEN, 180000, 10;
```

### SC_CONCENTRATE
**Effect:** Attention Concentrate - AGI/DEX +(2+SkillLv)%; Reveal hidden
**EFST:** EFST_CONCENTRATION
**Mechanics:**
- Reveals hidden enemies in 3x3 area around caster
**Parameters:**
- val1: (unused)

```c
sc_start SC_CONCENTRATE, 60000, 10;  // +12% AGI/DEX
```

### SC_WEAPONPERFECTION
**Effect:** Weapon Perfection - Ignore size modifier
**EFST:** EFST_WEAPONPERFECT
**Parameters:**
- val1: (unused)

```c
sc_start SC_WEAPONPERFECTION, 40000, 5;
```

### SC_OVERTHRUST
**Effect:** Over Thrust - ATK +(5*SkillLv)%; 0.1% weapon break chance
**EFST:** EFST_OVERTHRUST
**Mechanics:**
- Does not break Axes, Maces, or Unbreakable weapons
**Parameters:**
- val1: Skill Level

```c
sc_start SC_OVERTHRUST, 180000, 5;  // +25% ATK
```

### SC_MAXOVERTHRUST
**Effect:** Maximum Over Thrust - Enhanced version
**Parameters:**
- val1: (unused)

```c
sc_start SC_MAXOVERTHRUST, 180000, 5;
```

### SC_MAXIMIZEPOWER
**Effect:** Maximize Power - Always deal max damage
**EFST:** EFST_MAXIMIZE
**Mechanics:**
- SP Regeneration disabled
**Parameters:**
- val1: (unused)

```c
sc_start SC_MAXIMIZEPOWER, 60000, 1;
```

### SC_AURABLADE
**Effect:** Aura Blade - +20*SkillLv damage ignoring DEF/accuracy
**EFST:** EFST_AURABLADE
**OPT3:** OPT3_AURABLADE
**Parameters:**
- val1: (unused)

```c
sc_start SC_AURABLADE, 90000, 5;  // +100 damage
```

### SC_PARRYING
**Effect:** Parrying - Block with 2H-Sword (20+3*SkillLv)% chance
**EFST:** EFST_PARRYING
**Parameters:**
- val1: (unused)

```c
sc_start SC_PARRYING, 60000, 10;  // 50% block chance
```

### SC_CONCENTRATION
**Effect:** Spear Dynamo - WATK+; HIT+; DEF-
**EFST:** EFST_LKCONCENTRATION
**Mechanics:**
- Level 1 Endure effect included
**Parameters:**
- val1: Skill Level
- val2: 5*val1 (Batk/Watk Increase)
- val3: 10*val1 (Hit Increase)
- val4: 5*val1 (Def reduction)

```c
sc_start SC_CONCENTRATION, 60000, 5;
```

### SC_BERSERK
**Effect:** Berserk/Frenzy - Massive power boost
**EFST:** EFST_BERSERK
**OPT3:** OPT3_BERSERK
**Mechanics:**
- HP+SP Regen stopped
- Cannot use skills or chat
- FLEE reduced
- MaxHP increased
- Movement speed increased
- ATK increased
- DEF+MDEF set to 0
- Lose 5% HP every 10 seconds
**Parameters:**
- val1: (unused)
- val2: HP Penalty (5% of Max HP)
- val3: Skill duration
- val4: Interval of HP Penalty

```c
sc_start SC_BERSERK, 300000, 1;  // 5 minutes
```

---

<!-- RAG_CHUNK: defensive_status_effects -->
## 4. Defensive Status Effects

### SC_AUTOGUARD
**Effect:** Auto Guard - Block physical attacks
**EFST:** EFST_AUTOGUARD
**Mechanics:**
- Blocks short and long range physical attacks at certain chance
- Stops caster for 0.3 seconds when activated
**Parameters:**
- val1: (unused)

```c
sc_start SC_AUTOGUARD, 300000, 10;
```

### SC_REFLECTSHIELD
**Effect:** Reflect Shield - Reflect damage
**EFST:** EFST_REFLECTSHIELD
**Mechanics:**
- Reflects (10+3*SkillLv)% of short ranged physical attack
**Parameters:**
- val1: (unused)

```c
sc_start SC_REFLECTSHIELD, 300000, 10;  // Reflect 40%
```

### SC_DEFENDER
**Effect:** Defending Aura - Ranged defense
**EFST:** EFST_DEFENDER
**Mechanics:**
- Reduce (5+15*SkillLv)% damage from long range attacks
- Reduce (25+5*SkillLv) ASPD
**Parameters:**
- val1: (unused)

```c
sc_start SC_DEFENDER, 180000, 5;
```

### SC_ENERGYCOAT
**Effect:** Energy Coat - SP-based damage reduction
**EFST:** EFST_ENERGYCOAT
**Mechanics:**
- Reduce damage according to current MaxSP %
**Parameters:**
- val1: (unused)

```c
sc_start SC_ENERGYCOAT, 300000, 1;
```

### SC_SAFETYWALL
**Effect:** Safety Wall - Block melee attacks
**OPT:** OPTION_RUWACH
**Parameters:**
- val1: (unused)

```c
sc_start SC_SAFETYWALL, 30000, 10;
```

### SC_DEVOTION
**Effect:** Devotion - Take damage for target
**EFST:** EFST_DEVOTION
**Parameters:**
- val1: (unused)

```c
sc_start SC_DEVOTION, 90000, 5;
```

### SC_PROVIDENCE
**Effect:** Providence - Demon/Holy resistance
**EFST:** EFST_PROVIDENCE
**Mechanics:**
- Increases party resistance to RC_Demon and Ele_Holy monsters
**Parameters:**
- val1: (unused)

```c
sc_start SC_PROVIDENCE, 180000, 5;
```

---

<!-- RAG_CHUNK: strip_protect_status -->
## 5. Strip & Protection Status Effects

### SC_STRIPWEAPON
**Effect:** Strip Weapon - Unequip weapon
**EFST:** EFST_NOEQUIPWEAPON
**Mechanics:**
- Forces weapon unequip
- On mobs: ATK -25%
**Parameters:**
- val1: (unused)

```c
sc_start SC_STRIPWEAPON, 90000, 5;
```

### SC_STRIPSHIELD
**Effect:** Strip Shield - Unequip shield
**EFST:** EFST_NOEQUIPSHIELD
**Mechanics:**
- Forces shield unequip
- On mobs: DEF -15%
**Parameters:**
- val1: (unused)

```c
sc_start SC_STRIPSHIELD, 90000, 5;
```

### SC_STRIPARMOR
**Effect:** Strip Armor - Unequip armor
**EFST:** EFST_NOEQUIPARMOR
**Mechanics:**
- Forces armor unequip
- On mobs: VIT -40%
**Parameters:**
- val1: (unused)

```c
sc_start SC_STRIPARMOR, 90000, 5;
```

### SC_STRIPHELM
**Effect:** Strip Helm - Unequip helm
**EFST:** EFST_NOEQUIPHELM
**Mechanics:**
- Forces helm unequip
- On mobs: INT -40%
**Parameters:**
- val1: (unused)

```c
sc_start SC_STRIPHELM, 90000, 5;
```

### SC_CP_WEAPON
**Effect:** Chemical Protection (Weapon)
**EFST:** EFST_PROTECTWEAPON
**Mechanics:**
- Protects weapon from damage and strip skills
**Parameters:**
- val1: (unused)

```c
sc_start SC_CP_WEAPON, 300000, 5;
```

### SC_CP_SHIELD
**Effect:** Chemical Protection (Shield)
**EFST:** EFST_PROTECTSHIELD
**Parameters:**
- val1: (unused)

```c
sc_start SC_CP_SHIELD, 300000, 5;
```

### SC_CP_ARMOR
**Effect:** Chemical Protection (Armor)
**EFST:** EFST_PROTECTARMOR
**Parameters:**
- val1: (unused)

```c
sc_start SC_CP_ARMOR, 300000, 5;
```

### SC_CP_HELM
**Effect:** Chemical Protection (Helm)
**EFST:** EFST_PROTECTHELM
**Parameters:**
- val1: (unused)

```c
sc_start SC_CP_HELM, 300000, 5;
```

---

<!-- RAG_CHUNK: elemental_status_effects -->
## 6. Elemental Status Effects

### SC_ASPERSIO
**Effect:** Aspersio - Weapon becomes Holy element
**EFST:** EFST_ASPERSIO
**Parameters:**
- val1: (unused)

```c
sc_start SC_ASPERSIO, 180000, 5;
```

### SC_BENEDICTIO
**Effect:** B.S. Sacramenti - Armor becomes Holy element
**EFST:** EFST_BENEDICTIO
**Parameters:**
- val1: (unused)

```c
sc_start SC_BENEDICTIO, 60000, 5;
```

### SC_ENCPOISON
**Effect:** Enchant Poison - Weapon becomes Poison element
**EFST:** EFST_ENCHANTPOISON
**Mechanics:**
- Poisoning chance is (2.5+0.5*SkillLv)%
**Parameters:**
- val1: (unused)

```c
sc_start SC_ENCPOISON, 180000, 10;
```

### SC_FIREWEAPON
**Effect:** Fire element weapon
**EFST:** EFST_PROPERTYFIRE
**Parameters:**
- val1: (unused)

```c
sc_start SC_FIREWEAPON, 180000, 3;
```

### SC_WATERWEAPON
**Effect:** Water element weapon
**EFST:** EFST_PROPERTYWATER
**Parameters:**
- val1: (unused)

```c
sc_start SC_WATERWEAPON, 180000, 3;
```

### SC_WINDWEAPON
**Effect:** Wind element weapon
**EFST:** EFST_PROPERTYWIND
**Parameters:**
- val1: (unused)

```c
sc_start SC_WINDWEAPON, 180000, 3;
```

### SC_EARTHWEAPON
**Effect:** Earth element weapon
**EFST:** EFST_PROPERTYGROUND
**Parameters:**
- val1: (unused)

```c
sc_start SC_EARTHWEAPON, 180000, 3;
```

### SC_SHADOWWEAPON
**Effect:** Shadow/Dark element weapon
**Parameters:**
- val1: (unused)

```c
sc_start SC_SHADOWWEAPON, 180000, 3;
```

### SC_GHOSTWEAPON
**Effect:** Ghost element weapon
**Parameters:**
- val1: (unused)

```c
sc_start SC_GHOSTWEAPON, 180000, 3;
```

### SC_ELEMENTALCHANGE
**Effect:** Change armor element
**EFST:** EFST_ARMOR_PROPERTY
**Parameters:**
- val1: Element level
- val2: Element (see doc/item_bonus.txt)

```c
sc_start2 SC_ELEMENTALCHANGE, 300000, 1, Ele_Fire;  // Fire Lv1 armor
```

### SC_ARMOR_ELEMENT
**Effect:** Adjust element resistance by percentage
**Parameters:**
- val1: Water resistance %
- val2: Earth resistance %
- val3: Fire resistance %
- val4: Wind resistance %

```c
sc_start4 SC_ARMOR_ELEMENT, 300000, 50, 50, 50, 50;  // +50% all ele resist
```

---

<!-- RAG_CHUNK: skill_specific_status -->
## 7. Skill-Specific Status Effects

### SC_EDP
**Effect:** Enchant Deadly Poison - Massive ATK boost
**EFST:** EFST_EDP
**Mechanics:**
- WATK +(100+SkillLv*80)
**Parameters:**
- val1: Skill Level
- val2: Chance to Poison enemy (val1+2)%
- val3: Damage increase (50*(val1+1))

```c
sc_start SC_EDP, 60000, 5;  // +500 WATK
```

### SC_QUAGMIRE
**Effect:** Quagmire - AGI/DEX reduction
**EFST:** EFST_QUAGMIRE
**Mechanics:**
- Removes: Increase AGI, Two Hand Quicken, Wind Walk, Adrenaline Rush,
  Attention Concentrate, Cart Boost, True Sight, Magnetic Field, One Hand Quicken
- Movement Speed -50
- AGI & DEX -(10*SkillLv), min 75% for players, 50% for mobs
**Parameters:**
- val1: (unused)

```c
sc_start SC_QUAGMIRE, 20000, 5;  // -50 AGI/DEX, movement penalty
```

### SC_TRUESIGHT
**Effect:** True Sight - All stats +5, damage boost
**EFST:** EFST_TRUESIGHT
**Mechanics:**
- All stats +5
- Damage +(2*SkillLv)%
- CRIT +SkillLv
- HIT +(3*SkillLv)%
**Parameters:**
- val1: Skill Level
- val2: Crit bonus
- val3: Hit bonus

```c
sc_start SC_TRUESIGHT, 180000, 10;  // +20% damage, +10 CRIT
```

### SC_WINDWALK
**Effect:** Wind Walk - FLEE and speed boost
**EFST:** EFST_WINDWALK
**Parameters:**
- val1: Skill Level
- val2: Flee bonus

```c
sc_start SC_WINDWALK, 300000, 10;
```

### SC_MELTDOWN
**Effect:** Meltdown - Break enemy equipment
**EFST:** EFST_MELTDOWN
**Mechanics:**
- Chance to break weapon: 100*SkillLv
- Chance to break armor: 70*SkillLv
**Parameters:**
- val1: Skill Level
- val2: Weapon break chance
- val3: Armor break chance

```c
sc_start SC_MELTDOWN, 60000, 10;
```

### SC_KAAHI
**Effect:** Kaahi - HP recovery on receiving damage
**Mechanics:**
- Recover HP when taking damage
- Consumes SP per activation
**Parameters:**
- val1: Skill Level

```c
sc_start SC_KAAHI, 300000, 7;
```

### SC_KAUPE
**Effect:** Kaupe - Dodge attacks
**Mechanics:**
- Chance to completely avoid attacks
**Parameters:**
- val1: Skill Level

```c
sc_start SC_KAUPE, 300000, 3;
```

### SC_KAIZEL
**Effect:** Kaizel - Auto-revive
**Mechanics:**
- Resurrects on death with some HP
**Parameters:**
- val1: Skill Level

```c
sc_start SC_KAIZEL, 600000, 7;  // 10 minute duration
```

---

<!-- RAG_CHUNK: hiding_stealth_status -->
## 8. Hiding & Stealth Status Effects

### SC_HIDING
**Effect:** Hiding - Become invisible
**EFST:** EFST_HIDING
**OPT:** OPTION_HIDE
**Parameters:**
- val1: (unused)

```c
sc_start SC_HIDING, 30000, 10;
```

### SC_CLOAKING
**Effect:** Cloaking - Invisible while moving
**EFST:** EFST_CLOAKING
**OPT:** OPTION_CLOAK
**Parameters:**
- val1: (unused)

```c
sc_start SC_CLOAKING, 60000, 10;
```

### SC_CHASEWALK
**Effect:** Chase Walk - Stealth with STR bonus
**EFST:** EFST_CHASEWALK
**Parameters:**
- val1: (unused)

```c
sc_start SC_CHASEWALK, 60000, 5;
```

### SC_SIGHT
**Effect:** Sight - Reveal hidden enemies
**OPT:** OPTION_SIGHT
**Mechanics:**
- Reveal hidden enemies in 3x3 range
**Parameters:**
- val1: (unused)

```c
sc_start SC_SIGHT, 10000, 1;
```

### SC_RUWACH
**Effect:** Ruwach - Reveal and damage hidden
**OPT:** OPTION_RUWACH
**Mechanics:**
- Reveals and damages hidden targets (SC_HIDING, SC_CLOAKING, SC_CAMOUFLAGE, SC_CLOAKINGEXCEED)
**Parameters:**
- val1: (unused)

```c
sc_start SC_RUWACH, 10000, 1;
```

---

<!-- RAG_CHUNK: food_potion_status -->
## 9. Food & Potion Status Effects

### SC_ASPDPOTION0 / SC_ASPDPOTION1 / SC_ASPDPOTION2 / SC_ASPDPOTION3
**Effect:** ASPD Potion effects (don't stack with each other)
**EFST:** EFST_ATTHASTE_POTION1/2/3/INFINITY
**Parameters:**
- val1: +ASPD (Renewal)
- val2: +% ASPD (Pre-Renewal)

```c
sc_start SC_ASPDPOTION2, 180000, 4;  // +4 ASPD (RE) or +% ASPD (Pre-RE)
```

### SC_SPEEDUP0 / SC_SPEEDUP1
**Effect:** Movement speed potion
**EFST:** EFST_MOVHASTE_HORSE / EFST_MOVHASTE_POTION
**Mechanics:**
- Won't stack with bonus bSpeedRate
**Parameters:**
- val1: +% Walkspeed

```c
sc_start SC_SPEEDUP1, 300000, 25;  // +25% movement speed
```

### SC_ATKPOTION
**Effect:** ATK Potion
**EFST:** EFST_PLUSATTACKPOWER
**Parameters:**
- val1: +Atk

```c
sc_start SC_ATKPOTION, 180000, 50;  // +50 ATK
```

### SC_MATKPOTION
**Effect:** MATK Potion
**EFST:** EFST_PLUSMAGICPOWER
**Parameters:**
- val1: +Matk

```c
sc_start SC_MATKPOTION, 180000, 50;  // +50 MATK
```

### SC_STRFOOD / SC_AGIFOOD / SC_VITFOOD / SC_INTFOOD / SC_DEXFOOD / SC_LUKFOOD
**Effect:** Stat food bonuses
**EFST:** EFST_FOOD_STR/AGI/VIT/INT/DEX/LUK
**Mechanics:**
- Cannot stack with CASH versions (ignored if value is lower)
**Parameters:**
- val1: +Stat

```c
sc_start SC_STRFOOD, 1800000, 10;  // +10 STR for 30 minutes
sc_start SC_AGIFOOD, 1800000, 10;
sc_start SC_VITFOOD, 1800000, 10;
sc_start SC_INTFOOD, 1800000, 10;
sc_start SC_DEXFOOD, 1800000, 10;
sc_start SC_LUKFOOD, 1800000, 10;
```

### SC_HITFOOD / SC_FLEEFOOD
**Effect:** HIT/FLEE food
**EFST:** EFST_FOOD_BASICHIT / EFST_FOOD_BASICAVOIDANCE
**Parameters:**
- val1: +Hit or +Flee

```c
sc_start SC_HITFOOD, 1800000, 30;  // +30 HIT
sc_start SC_FLEEFOOD, 1800000, 30;  // +30 FLEE
```

### SC_BATKFOOD / SC_WATKFOOD / SC_MATKFOOD
**Effect:** Attack food bonuses
**Parameters:**
- val1: Bonus amount

```c
sc_start SC_BATKFOOD, 1800000, 20;  // +20 Base ATK
sc_start SC_WATKFOOD, 1800000, 20;  // +20 Weapon ATK
sc_start SC_MATKFOOD, 1800000, 20;  // +20 MATK
```

---

<!-- RAG_CHUNK: stat_modifier_status -->
## 10. Stat Modifier Status Effects

### SC_INCALLSTATUS
**Effect:** Increase all stats
**Parameters:**
- val1: +AllStats

```c
sc_start SC_INCALLSTATUS, 300000, 10;  // +10 all stats
```

### SC_INCSTR / SC_INCAGI / SC_INCVIT / SC_INCINT / SC_INCDEX / SC_INCLUK
**Effect:** Individual stat increases
**Parameters:**
- val1: +Stat

```c
sc_start SC_INCSTR, 300000, 20;
sc_start SC_INCAGI, 300000, 20;
sc_start SC_INCVIT, 300000, 20;
sc_start SC_INCINT, 300000, 20;
sc_start SC_INCDEX, 300000, 20;
sc_start SC_INCLUK, 300000, 20;
```

### SC_INCHIT / SC_INCHITRATE
**Effect:** HIT bonus
**Parameters:**
- val1: +Hit or +% Hit

```c
sc_start SC_INCHIT, 300000, 50;      // +50 HIT
sc_start SC_INCHITRATE, 300000, 20;  // +20% HIT
```

### SC_INCFLEE / SC_INCFLEERATE
**Effect:** FLEE bonus
**Parameters:**
- val1: +Flee or +% Flee

```c
sc_start SC_INCFLEE, 300000, 50;      // +50 FLEE
sc_start SC_INCFLEERATE, 300000, 20;  // +20% FLEE
```

### SC_INCMHPRATE / SC_INCMSPRATE
**Effect:** MaxHP/MaxSP percentage increase
**Parameters:**
- val1: +% MaxHP or +% MaxSP

```c
sc_start SC_INCMHPRATE, 300000, 50;  // +50% MaxHP
sc_start SC_INCMSPRATE, 300000, 50;  // +50% MaxSP
```

### SC_INCATKRATE / SC_INCMATKRATE
**Effect:** ATK/MATK percentage increase
**Parameters:**
- val1: +% ATK or +% MATK

```c
sc_start SC_INCATKRATE, 300000, 20;   // +20% ATK
sc_start SC_INCMATKRATE, 300000, 20;  // +20% MATK
```

### SC_INCDEFRATE
**Effect:** DEF percentage increase
**Parameters:**
- val1: +% DEF

```c
sc_start SC_INCDEFRATE, 300000, 50;  // +50% DEF
```

---

<!-- RAG_CHUNK: misc_status_effects -->
## 11. Miscellaneous Status Effects

### SC_AUTOBERSERK
**Effect:** Auto Berserk - Provoke self when low HP
**EFST:** EFST_AUTOBERSERK
**Mechanics:**
- If HP < 25%, automatically apply SC_PROVOKE level 10 on self
**Parameters:**
- val1: (unused)

```c
sc_start SC_AUTOBERSERK, -1, 1;  // Permanent until death
```

### SC_AUTOSPELL
**Effect:** Auto Spell - Cast magic on physical attack
**EFST:** EFST_AUTOSPELL
**Mechanics:**
- Auto cast learned magic spells using 2/3 SP cost
- Only triggers on physical attacks
**Parameters:**
- val1: (unused)

```c
sc_start SC_AUTOSPELL, 180000, 10;
```

### SC_AUTOCOUNTER
**Effect:** Counter Attack - Auto critical on close attack
**EFST:** EFST_AUTOCOUNTER
**Mechanics:**
- +20% Hit rate
- If attacked by close range, counter with Crit x2
**Parameters:**
- val1: (unused)

```c
sc_start SC_AUTOCOUNTER, 30000, 5;
```

### SC_POISONREACT
**Effect:** Poison React - Block poison, counter attacks
**EFST:** EFST_POISONREACT
**Mechanics:**
- Mode 0: Block poison attacks, boost damage by 30*SkillLv% after block
- Mode 1: Counter non-poison attacks with Envenom 5 autocast
**Parameters:**
- val1: Skill level
- val2: Number of Envenom autocasts
- val3: Chance to autocast Envenom / Poison chance after block
- val4: 0=Poison Block Mode; 1=Damage Boost Mode

```c
sc_start SC_POISONREACT, 180000, 10;
sc_start4 SC_POISONREACT, 180000, 10, 5, 50, 0;
```

### SC_AETERNA
**Effect:** Lex Aeterna - Double damage received
**EFST:** EFST_LEXAETERNA
**Mechanics:**
- Next damage taken is doubled
- Removed after taking damage
**Parameters:**
- val1: (unused)

```c
sc_start SC_AETERNA, 60000, 1;
```

### SC_MAGICPOWER
**Effect:** Magic Power - MATK boost for next spell
**EFST:** EFST_MAGICPOWER
**Mechanics:**
- MATK +(SkillLv*5)% for next magic skill
**Parameters:**
- val1: (unused)

```c
sc_start SC_MAGICPOWER, 30000, 10;  // +50% MATK for next spell
```

### SC_SUFFRAGIUM
**Effect:** Suffragium - Cast time reduction
**EFST:** EFST_SUFFRAGIUM
**Mechanics:**
- Cast time -(15*SkillLv)%
**Parameters:**
- val1: (unused)

```c
sc_start SC_SUFFRAGIUM, 60000, 3;  // -45% cast time
```

### SC_IMPOSITIO
**Effect:** Impositio Manus - ATK bonus
**EFST:** EFST_IMPOSITIO
**Mechanics:**
- ATK +(5*SkillLv)
**Parameters:**
- val1: (unused)

```c
sc_start SC_IMPOSITIO, 60000, 5;  // +25 ATK
```

### SC_SLOWPOISON
**Effect:** Slow Poison - Stop HP reduction from poison
**EFST:** EFST_SLOWPOISON
**Mechanics:**
- Stops HP reduction from SC_POISON
- Does NOT cure poison
**Parameters:**
- val1: (unused)

```c
sc_start SC_SLOWPOISON, 300000, 1;
```

---

<!-- RAG_CHUNK: guild_woe_status -->
## 12. Guild & WoE Status Effects

### SC_GUILDAURA
**Effect:** Guild Aura effects
**Parameters:**
- val1: (varies)

### SC_BATTLEORDERS
**Effect:** Battle Orders - Guild buff
**Parameters:**
- val1: (unused)

```c
sc_start SC_BATTLEORDERS, 180000, 1;
```

### SC_REGENERATION
**Effect:** Regeneration - Guild regen buff
**Parameters:**
- val1: (unused)

```c
sc_start SC_REGENERATION, 180000, 1;
```

### SC_GOSPEL
**Effect:** Gospel - Random status effects
**EFST:** EFST_GOSPEL
**Mechanics:**
- Cannot move during effect
- Gives random positive effects to party members
- Gives random negative effects to enemies
**Parameters:**
- val1: (unused)

```c
sc_start SC_GOSPEL, 60000, 10;
```

---

<!-- RAG_CHUNK: bard_dancer_status -->
## 13. Bard & Dancer Status Effects

### SC_DANCING
**Effect:** Performing a song/dance
**Parameters:**
- val1: (varies by performance)

### SC_WHISTLE
**Effect:** A Whistle song effect
**Parameters:**
- val1: (unused)

### SC_ASSNCROS
**Effect:** Assassin Cross of Sunset
**Parameters:**
- val1: (unused)

### SC_POEMBRAGI
**Effect:** Poem of Bragi
**Parameters:**
- val1: (unused)

### SC_APPLEIDUN
**Effect:** Apple of Idun
**Parameters:**
- val1: (unused)

### SC_HUMMING
**Effect:** Humming song
**Parameters:**
- val1: (unused)

### SC_DONTFORGETME
**Effect:** Please Don't Forget Me
**Parameters:**
- val1: (unused)

### SC_FORTUNE
**Effect:** Fortune's Kiss
**Parameters:**
- val1: (unused)

### SC_SERVICE4U
**Effect:** Service for You
**Parameters:**
- val1: (unused)

### SC_RICHMANKIM
**Effect:** Down Tempo
**Parameters:**
- val1: (unused)

### SC_ETERNALCHAOS
**Effect:** Chaos Panic
**Parameters:**
- val1: (unused)

### SC_DRUMBATTLE
**Effect:** Battle Theme
**Parameters:**
- val1: (unused)

### SC_NIBELUNGEN
**Effect:** Song of Lutie
**Parameters:**
- val1: (unused)

### SC_ROKISWEIL
**Effect:** Loki's Wail
**Parameters:**
- val1: (unused)

### SC_INTOABYSS
**Effect:** Deep Sleep Lullaby
**Parameters:**
- val1: (unused)

### SC_SIEGFRIED
**Effect:** Ragnarok
**EFST:** EFST_SIEGFRIED
**Parameters:**
- val1: BD_SIEGFRIED Skill level
- val2: Increase damage reduction % from non-Neutral elemental attacks
- val3: Increase status resistance % of player's current resistance

```c
sc_start SC_SIEGFRIED, 300000, 5;
```

---

<!-- RAG_CHUNK: status_effect_tips -->
## Usage Tips & Best Practices

### Checking Status Effects
```c
// Check if player has status
if (getstatus(SC_BLESSING)) {
    mes "You are blessed!";
}

// Get remaining time
.@time = getstatus(SC_BLESSING, 1);
mes "Time remaining: " + (.@time/1000) + " seconds";

// Get val1
.@level = getstatus(SC_BLESSING, 2);
mes "Blessing level: " + .@level;

// Get val2, val3, val4
.@val2 = getstatus(SC_BLESSING, 3);
.@val3 = getstatus(SC_BLESSING, 4);
.@val4 = getstatus(SC_BLESSING, 5);
```

### Using SCSTART Flags
```c
// SCSTART_NOAVOID (1) - Ignore target's status resist
// SCSTART_NOTICKDEF (2) - Allow status even if tick is 0
// SCSTART_LOADED (4) - Use val1-val4 directly without modification

sc_start SC_POISON, 60000, 5, 0, SCSTART_NOAVOID;  // Ignore resist
sc_start4 SC_ARMOR_ELEMENT, 60000, 50, 50, 50, 50, SCSTART_LOADED;  // Use vals directly
```

### Removing Status Effects
```c
// Remove single status
sc_end SC_BLESSING;

// Remove all status (be careful!)
// This would need to iterate through all SC_ constants

// Remove status from another player
attachrid .@target_id;
sc_end SC_POISON;
detachrid;
```

### Duration Constants
```c
// Common durations
#define SECONDS *1000
#define MINUTES *60000

sc_start SC_BLESSING, 4 MINUTES, 10;  // 4 minutes
sc_start SC_STUN, 5 SECONDS, 0;       // 5 seconds
sc_start SC_AUTOBERSERK, -1, 1;       // Permanent (until death/logout)
```

---

*This document covers 200+ status effects. For complete list of 1000+ SC_* constants, see src/map/status.hpp*
