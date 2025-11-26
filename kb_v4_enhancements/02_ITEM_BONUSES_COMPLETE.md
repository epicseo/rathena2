# rAthena Item Bonuses Complete Reference

**Version:** Enhancement v1.0 for KB v4
**Coverage:** 263 Item Bonuses
**RAG-Optimized:** Yes
**Last Updated:** 2025-11-26

---

<!-- RAG_CHUNK: overview -->
## Overview

This enhancement document provides comprehensive documentation for rAthena item bonuses used in item scripts. All bonuses are applied using the `bonus`, `bonus2`, `bonus3`, `bonus4`, and `bonus5` script commands.

### Quick Reference - Constants

```c
// Status effects (eff)
Eff_Bleeding, Eff_Blind, Eff_Burning, Eff_Confusion, Eff_Crystalize,
Eff_Curse, Eff_DPoison, Eff_Fear, Eff_Freeze, Eff_Poison, Eff_Silence,
Eff_Sleep, Eff_Stone, Eff_Stun, Eff_Freezing, Eff_Heat, Eff_Deepsleep,
Eff_WhiteImprison, Eff_Hallucination

// Element (e)
Ele_Dark, Ele_Earth, Ele_Fire, Ele_Ghost, Ele_Holy, Ele_Neutral,
Ele_Poison, Ele_Undead, Ele_Water, Ele_Wind, Ele_All

// Race (r)
RC_Angel, RC_Brute, RC_DemiHuman, RC_Demon, RC_Dragon, RC_Fish,
RC_Formless, RC_Insect, RC_Plant, RC_Player_Human, RC_Player_Doram,
RC_Undead, RC_All

// Monster Race (mr)
RC2_Goblin, RC2_Kobold, RC2_Orc, RC2_Golem, RC2_Guardian, RC2_Ninja,
RC2_GVG, RC2_Battlefield, RC2_Treasure, RC2_BioLab, RC2_Manuk,
RC2_Splendide, RC2_Scaraba, RC2_OGH_ATK_DEF, RC2_OGH_Hidden...

// Class (c)
Class_Normal, Class_Boss, Class_Guardian, Class_All

// Size (s)
Size_Small, Size_Medium, Size_Large, Size_All

// Trigger criteria (bf)
BF_SHORT, BF_LONG, BF_WEAPON, BF_MAGIC, BF_MISC, BF_NORMAL, BF_SKILL

// Attack target flags (atf)
ATF_SELF, ATF_TARGET, ATF_SHORT, ATF_LONG, ATF_SKILL, ATF_WEAPON,
ATF_MAGIC, ATF_MISC
```

---

<!-- RAG_CHUNK: basic_stat_bonuses -->
## 1. Basic Stat Bonuses

### Base Stats
```c
bonus bStr,n;           // STR + n
bonus bAgi,n;           // AGI + n
bonus bVit,n;           // VIT + n
bonus bInt,n;           // INT + n
bonus bDex,n;           // DEX + n
bonus bLuk,n;           // LUK + n
bonus bAllStats,n;      // All stats + n
bonus bAgiVit,n;        // AGI + n, VIT + n
bonus bAgiDexStr,n;     // STR + n, AGI + n, DEX + n
```

**Example:**
```c
// +5 to all stats
bonus bAllStats,5;

// +10 STR, +10 AGI, +10 DEX
bonus bAgiDexStr,10;
```

### Trait Stats (4th Job)
```c
bonus bPow,n;           // POW + n
bonus bSta,n;           // STA + n
bonus bWis,n;           // WIS + n
bonus bSpl,n;           // SPL + n
bonus bCon,n;           // CON + n
bonus bCrt,n;           // CRT + n
bonus bAllTraitStats,n; // All trait stats + n
```

### HP/SP/AP
```c
bonus bMaxHP,n;         // MaxHP + n
bonus bMaxHPrate,n;     // MaxHP + n%
bonus bMaxSP,n;         // MaxSP + n
bonus bMaxSPrate,n;     // MaxSP + n%
bonus bMaxAP,n;         // MaxAP + n
bonus bMaxAPrate,n;     // MaxAP + n%
```

**Example:**
```c
// +1000 HP
bonus bMaxHP,1000;

// +50% Max HP
bonus bMaxHPrate,50;
```

---

<!-- RAG_CHUNK: attack_defense_bonuses -->
## 2. Attack/Defense Bonuses

### Attack Bonuses
```c
bonus bBaseAtk,n;           // Basic attack power + n
bonus bAtk,n;               // ATK + n (unofficial)
bonus bAtk2,n;              // ATK2 + n
bonus bAtkRate,n;           // ATK + n% (RE mode, no interference with EDP)
bonus bWeaponAtkRate,n;     // Weapon ATK + n%
bonus bMatk,n;              // Magical attack power + n
bonus bMatk2,n;             // Magical ATK + n (not visible in status)
bonus bMatkRate,n;          // Magical ATK + n%
bonus bWeaponMatkRate,n;    // Weapon Magical ATK + n% (RE mode only)
```

**Example:**
```c
// +50 ATK
bonus bAtk,50;

// +20% ATK (Renewal)
bonus bAtkRate,20;

// +100 MATK
bonus bMatk,100;
```

### Defense Bonuses
```c
bonus bDef,n;               // Equipment DEF + n
bonus bDefRate,n;           // Equipment DEF + n%
bonus bDef2,n;              // VIT based DEF + n
bonus bDef2Rate,n;          // VIT based DEF + n%
bonus bMdef,n;              // Equipment MDEF + n
bonus bMdefRate,n;          // Equipment MDEF + n%
bonus bMdef2,n;             // INT based MDEF + n
bonus bMdef2Rate,n;         // INT based MDEF + n%
```

**Example:**
```c
// +100 DEF
bonus bDef,100;

// +30% MDEF
bonus bMdefRate,30;
```

---

<!-- RAG_CHUNK: additional_stat_bonuses -->
## 3. Additional Stat Bonuses

### Hit/Flee/Critical
```c
bonus bHit,n;               // Hit + n
bonus bHitRate,n;           // Hit + n%
bonus bCritical,n;          // Critical + n
bonus bCriticalLong,n;      // Critical + n for ranged (not shown in status)
bonus2 bCriticalAddRace,r,n;// Critical + n vs race r
bonus bCriticalRate,n;      // Critical + n%
bonus bFlee,n;              // Flee + n
bonus bFleeRate,n;          // Flee + n%
bonus bFlee2,n;             // Perfect Dodge + n
bonus bFlee2Rate,n;         // Perfect Dodge + n%
bonus bPerfectHitRate,n;    // On-target hit probability n% (highest applied)
bonus bPerfectHitAddRate,n; // On-target hit probability + n%
```

**Example:**
```c
// +30 HIT
bonus bHit,30;

// +10 CRIT vs Undead
bonus2 bCriticalAddRace,RC_Undead,10;

// 100% Perfect Hit
bonus bPerfectHitRate,100;
```

### Speed/ASPD/Range
```c
bonus bSpeedRate,n;         // Movement speed + n% (highest applied)
bonus bSpeedAddRate,n;      // Movement speed + n%
bonus bAspd,n;              // Attack speed + n
bonus bAspdRate,n;          // Attack speed + n%
bonus bAtkRange,n;          // Attack range + n
bonus bAddMaxWeight,n;      // MaxWeight + n (units of 0.1)
```

**Example:**
```c
// +25% movement speed (won't stack with SC_SPEEDUP)
bonus bSpeedRate,25;

// +10 ASPD
bonus bAspd,10;
```

### 4th Job Stats
```c
bonus bPAtk,n;              // PAtk + n
bonus bPAtkRate,n;          // PAtk + n%
bonus bSMatk,n;             // SMatk + n
bonus bSMatkRate,n;         // SMatk + n%
bonus bRes,n;               // Res + n
bonus bResRate,n;           // Res + n%
bonus bMRes,n;              // MRes + n
bonus bMResRate,n;          // MRes + n%
bonus bHPlus,n;             // HPlus + n
bonus bHPlusRate,n;         // HPlus + n%
bonus bCRate,n;             // CRate + n
bonus bCRateRate,n;         // CRate + n%
```

---

<!-- RAG_CHUNK: hp_sp_regen_bonuses -->
## 4. HP/SP Regeneration Bonuses

### Natural Recovery
```c
bonus bHPrecovRate,n;       // Natural HP recovery ratio + n%
bonus bSPrecovRate,n;       // Natural SP recovery ratio + n%
```

### Timed Regeneration
```c
bonus2 bHPRegenRate,n,t;    // Gain n HP every t milliseconds
bonus2 bHPLossRate,n,t;     // Lose n HP every t milliseconds
bonus2 bSPRegenRate,n,t;    // Gain n SP every t milliseconds
bonus2 bSPLossRate,n,t;     // Lose n SP every t milliseconds
bonus2 bRegenPercentHP,n,t; // Gain n% of max HP every t milliseconds
bonus2 bRegenPercentSP,n,t; // Gain n% of max SP every t milliseconds
bonus bNoRegen,x;           // Stops HP (1) or SP (2) regeneration
```

**Example:**
```c
// Recover 100 HP every 5 seconds
bonus2 bHPRegenRate,100,5000;

// Lose 50 SP every 3 seconds
bonus2 bSPLossRate,50,3000;

// Recover 1% of max HP every 10 seconds
bonus2 bRegenPercentHP,1,10000;

// Disable SP regeneration
bonus bNoRegen,2;
```

### SP Consumption
```c
bonus bUseSPrate,n;             // SP consumption + n%
bonus2 bSkillUseSP,sk,n;        // Decreases SP consumption of skill sk by n
bonus2 bSkillUseSPrate,sk,n;    // Decreases SP consumption of skill sk by n%
```

**Example:**
```c
// -20% SP consumption for all skills
bonus bUseSPrate,-20;

// Bolt skills cost 10 less SP
bonus2 bSkillUseSP,"MG_COLDBOLT",10;
bonus2 bSkillUseSP,"MG_FIREBOLT",10;
bonus2 bSkillUseSP,"MG_LIGHTNINGBOLT",10;
```

---

<!-- RAG_CHUNK: damage_modifier_bonuses -->
## 5. Damage Modifier Bonuses

### Skill Damage
```c
bonus2 bSkillAtk,sk,n;      // Increases damage of skill sk by n%
bonus bSkillRatio,n;        // Adds n to skillratio of all attacks
```

**Example:**
```c
// +20% Bash damage
bonus2 bSkillAtk,"SM_BASH",20;

// +10 to all skill ratios
bonus bSkillRatio,10;
```

### Range-Based Damage
```c
bonus bShortAtkRate,n;      // Melee damage + n%
bonus bLongAtkRate,n;       // Ranged damage + n%
bonus bCritAtkRate,n;       // Critical damage + n%
bonus bCritDefRate,n;       // Critical damage received - n%
bonus bCriticalDef,n;       // Chance of being crit - n%
```

**Example:**
```c
// +15% melee damage
bonus bShortAtkRate,15;

// +25% ranged damage
bonus bLongAtkRate,25;

// +50% critical damage
bonus bCritAtkRate,50;
```

### Weapon-Based Damage
```c
bonus2 bWeaponAtk,w,n;          // +n ATK when weapon type w equipped
bonus2 bWeaponDamageRate,w,n;   // +n% damage with weapon type w
```

**Example:**
```c
// +50 ATK with swords
bonus2 bWeaponAtk,W_1HSWORD,50;
bonus2 bWeaponAtk,W_2HSWORD,50;

// +10% damage with bows
bonus2 bWeaponDamageRate,W_BOW,10;
```

---

<!-- RAG_CHUNK: damage_reduction_bonuses -->
## 6. Damage Reduction Bonuses

### Physical/Magical/Misc Defense
```c
bonus bNearAtkDef,n;        // Melee physical damage - n%
bonus bLongAtkDef,n;        // Ranged physical damage - n%
bonus bMagicAtkDef,n;       // Magical damage - n%
bonus bMiscAtkDef,n;        // Misc damage (traps, falcon) - n%
```

### Total Damage Reduction
```c
bonus bNoWeaponDamage,n;    // Physical damage - n%
bonus bNoMagicDamage,n;     // Magical effect - n% (blocks attacks, heals, buffs)
bonus bNoMiscDamage,n;      // Misc damage - n%
```

**Example:**
```c
// 30% less melee damage
bonus bNearAtkDef,30;

// 50% less magic damage
bonus bMagicAtkDef,50;

// Immune to physical damage (100% reduction)
bonus bNoWeaponDamage,100;
```

### Max HP Damage Cap
```c
bonus bAbsorbDmgMaxHP,n;    // Damage > n% MaxHP reduced (legacy behavior)
bonus bAbsorbDmgMaxHP2,n;   // Damage > n% MaxHP capped to n% (official)
```

**Example:**
```c
// Cap damage at 10% of max HP
bonus bAbsorbDmgMaxHP2,10;
```

---

<!-- RAG_CHUNK: elemental_bonuses -->
## 7. Elemental Bonuses

### Element Attack/Defense
```c
bonus bAtkEle,e;            // Attack element becomes e
bonus bDefEle,e;            // Defense element becomes e
bonus2 bMagicAtkEle,e,x;    // Element e magic damage + x%
```

**Example:**
```c
// Fire element attacks
bonus bAtkEle,Ele_Fire;

// +30% fire magic damage
bonus2 bMagicAtkEle,Ele_Fire,30;
```

### Element Damage Modifiers
```c
bonus2 bAddEle,e,x;             // +x% physical damage vs element e
bonus3 bAddEle,e,x,bf;          // +x% with trigger bf
bonus2 bMagicAddEle,e,x;        // +x% magical damage vs element e
bonus2 bSubEle,e,x;             // +x% damage reduction vs element e
bonus3 bSubEle,e,x,bf;          // +x% reduction with trigger bf
bonus2 bSubDefEle,e,x;          // +x% physical reduction vs defense element e
bonus2 bMagicSubDefEle,e,x;     // +x% magic reduction vs defense element e
```

**Example:**
```c
// +25% damage vs Fire monsters
bonus2 bAddEle,Ele_Fire,25;

// +50% damage reduction vs Water attacks
bonus2 bSubEle,Ele_Water,50;

// +20% magic damage vs Undead
bonus2 bMagicAddEle,Ele_Undead,20;
```

---

<!-- RAG_CHUNK: race_bonuses -->
## 8. Race Bonuses

### Race Damage Modifiers
```c
bonus2 bAddRace,r,x;            // +x% physical damage vs race r
bonus2 bMagicAddRace,r,x;       // +x% magical damage vs race r
bonus2 bSubRace,r,x;            // +x% damage reduction vs race r
bonus3 bSubRace,r,x,bf;         // +x% reduction with trigger bf
```

**Example:**
```c
// +20% damage vs Demons
bonus2 bAddRace,RC_Demon,20;

// +30% damage reduction vs Undead
bonus2 bSubRace,RC_Undead,30;

// +25% magic damage vs Brutes
bonus2 bMagicAddRace,RC_Brute,25;
```

### Monster Race (RC2) Modifiers
```c
bonus2 bAddRace2,mr,x;          // +x% damage vs monster race mr
bonus2 bSubRace2,mr,x;          // +x% reduction vs monster race mr
bonus2 bMagicAddRace2,mr,x;     // +x% magic damage vs monster race mr
```

**Example:**
```c
// +30% damage vs Goblins
bonus2 bAddRace2,RC2_Goblin,30;

// +20% damage vs BioLab monsters
bonus2 bAddRace2,RC2_BioLab,20;
```

---

<!-- RAG_CHUNK: class_size_bonuses -->
## 9. Class & Size Bonuses

### Class Modifiers
```c
bonus2 bAddClass,c,x;           // +x% physical damage vs class c
bonus2 bMagicAddClass,c,x;      // +x% magical damage vs class c
bonus2 bSubClass,c,x;           // +x% damage reduction vs class c
```

**Example:**
```c
// +25% damage vs Boss monsters
bonus2 bAddClass,Class_Boss,25;

// +20% damage reduction vs Guardians
bonus2 bSubClass,Class_Guardian,20;
```

### Size Modifiers
```c
bonus2 bAddSize,s,x;            // +x% physical damage vs size s
bonus2 bMagicAddSize,s,x;       // +x% magical damage vs size s
bonus2 bSubSize,s,x;            // +x% damage reduction vs size s
bonus2 bWeaponSubSize,s,x;      // +x% physical reduction vs size s
bonus2 bMagicSubSize,s,x;       // +x% magic reduction vs size s
bonus bNoSizeFix;               // Ignore size modifier for damage
```

**Example:**
```c
// +15% damage vs Large monsters
bonus2 bAddSize,Size_Large,15;

// +20% reduction vs all sizes
bonus2 bSubSize,Size_All,20;

// Ignore size penalty
bonus bNoSizeFix;
```

---

<!-- RAG_CHUNK: ignore_defense_bonuses -->
## 10. Ignore Defense Bonuses

### Ignore DEF
```c
bonus bIgnoreDefEle,e;          // Ignore DEF vs element e
bonus bIgnoreDefRace,r;         // Ignore DEF vs race r
bonus bIgnoreDefClass,c;        // Ignore DEF vs class c
bonus2 bIgnoreDefRaceRate,r,n;  // Ignore n% DEF vs race r
bonus2 bIgnoreDefClassRate,c,n; // Ignore n% DEF vs class c
```

**Example:**
```c
// Ignore DEF vs Undead
bonus bIgnoreDefRace,RC_Undead;

// Ignore 50% DEF vs Boss
bonus2 bIgnoreDefClassRate,Class_Boss,50;
```

### Ignore MDEF
```c
bonus bIgnoreMDefRace,r;            // Ignore MDEF vs race r
bonus bIgnoreMDefEle,e;             // Ignore MDEF vs element e
bonus2 bIgnoreMdefRaceRate,r,n;     // Ignore n% MDEF vs race r
bonus2 bIgnoreMdefRace2Rate,mr,n;   // Ignore n% MDEF vs monster race mr
bonus2 bIgnoreMdefClassRate,c,n;    // Ignore n% MDEF vs class c
```

### Ignore Res/MRes (4th Job)
```c
bonus2 bIgnoreResRaceRate,r,n;      // Ignore n% Res vs race r
bonus2 bIgnoreMResRaceRate,r,n;     // Ignore n% MRes vs race r
```

---

<!-- RAG_CHUNK: healing_bonuses -->
## 11. Healing Bonuses

### Skill Healing
```c
bonus bHealPower,n;             // All heal skills + n%
bonus bHealPower2,n;            // Being healed + n%
bonus2 bSkillHeal,sk,n;         // Skill sk heal + n%
bonus2 bSkillHeal2,sk,n;        // Being healed by sk + n%
```

**Example:**
```c
// +20% healing from all skills
bonus bHealPower,20;

// +50% Heal effectiveness
bonus2 bSkillHeal,"AL_HEAL",50;
```

### Item Healing
```c
bonus bAddItemHealRate,n;           // HP recovered by items + n%
bonus2 bAddItemHealRate,iid,n;      // HP recovered by item iid + n%
bonus2 bAddItemGroupHealRate,ig,n;  // HP recovered by item group ig + n%
bonus bAddItemSPHealRate,n;         // SP recovered by items + n%
bonus2 bAddItemSPHealRate,iid,n;    // SP recovered by item iid + n%
bonus2 bAddItemGroupSPHealRate,ig,n;// SP recovered by item group ig + n%
```

**Example:**
```c
// All HP potions heal 30% more
bonus bAddItemHealRate,30;

// Red Potions heal 50% more
bonus2 bAddItemHealRate,501,50;  // 501 = Red_Potion
```

---

<!-- RAG_CHUNK: cast_time_bonuses -->
## 12. Cast Time & Delay Bonuses

### Cast Time Reduction
```c
bonus bCastrate,n;              // Cast time + n% (= bVariableCastrate in RE)
bonus2 bCastrate,sk,n;          // Skill sk cast time + n%
bonus bFixedCastrate,n;         // Fixed cast time + n% (RE only)
bonus2 bFixedCastrate,sk,n;     // Skill sk fixed cast + n%
bonus bVariableCastrate,n;      // Variable cast time + n%
bonus2 bVariableCastrate,sk,n;  // Skill sk variable cast + n%
```

**Example:**
```c
// -30% cast time for all skills
bonus bCastrate,-30;

// -50% cast time for Bolt spells
bonus2 bCastrate,"MG_COLDBOLT",-50;
bonus2 bCastrate,"MG_FIREBOLT",-50;
bonus2 bCastrate,"MG_LIGHTNINGBOLT",-50;

// -100% fixed cast (instant fixed cast in Renewal)
bonus bFixedCastrate,-100;
```

### Fixed Time Addition
```c
bonus bFixedCast,t;             // Fixed cast + t ms (RE only)
bonus2 bSkillFixedCast,sk,t;    // Skill sk fixed cast + t ms
bonus bVariableCast,t;          // Variable cast + t ms
bonus2 bSkillVariableCast,sk,t; // Skill sk variable cast + t ms
```

### Cast Interruption
```c
bonus bNoCastCancel;            // No cast interruption (not in GvG)
bonus bNoCastCancel2;           // No cast interruption (works in GvG)
```

### After-Cast Delay
```c
bonus bDelayrate,n;             // Skill delay + n%
bonus2 bSkillDelay,sk,t;        // Skill sk delay + t ms
bonus2 bSkillCooldown,sk,t;     // Skill sk cooldown + t ms
```

**Example:**
```c
// -20% after-cast delay
bonus bDelayrate,-20;

// -500ms delay on Bash
bonus2 bSkillDelay,"SM_BASH",-500;
```

---

<!-- RAG_CHUNK: status_effect_bonuses -->
## 13. Status Effect Bonuses

### Inflict Status
```c
bonus2 bAddEff,eff,n;               // n/100% chance to cause eff on target
bonus2 bAddEff2,eff,n;              // n/100% chance to cause eff on self
bonus2 bAddEffWhenHit,eff,n;        // n/100% chance to cause eff when hit
bonus2 bResEff,eff,n;               // n/100% tolerance to eff
bonus3 bAddEff,eff,n,atf;           // With trigger criteria atf
bonus4 bAddEff,eff,n,atf,t;         // For t milliseconds
bonus3 bAddEffWhenHit,eff,n,atf;    // When hit with criteria atf
bonus4 bAddEffWhenHit,eff,n,atf,t;  // For t milliseconds
```

**Example:**
```c
// 5% chance to stun on attack (5% = 500/100)
bonus2 bAddEff,Eff_Stun,500;

// 3% chance to poison enemy when hit
bonus2 bAddEffWhenHit,Eff_Poison,300;

// +50% resistance to Silence
bonus2 bResEff,Eff_Silence,5000;
```

### Skill-Triggered Status
```c
bonus3 bAddEffOnSkill,sk,eff,n;     // n/100% chance when using skill sk
bonus4 bAddEffOnSkill,sk,eff,n,atf; // With target criteria
bonus5 bAddEffOnSkill,sk,eff,n,atf,t; // For t milliseconds
```

### Coma Effect
```c
bonus2 bComaClass,c,n;          // n/100% coma vs class c
bonus2 bComaRace,r,n;           // n/100% coma vs race r
bonus2 bWeaponComaEle,e,n;      // n/100% coma with normal attack vs element e
bonus2 bWeaponComaClass,c,n;    // n/100% coma with normal attack vs class c
bonus2 bWeaponComaRace,r,n;     // n/100% coma with normal attack vs race r
```

**Example:**
```c
// 1% chance to coma Undead with normal attack
bonus2 bWeaponComaRace,RC_Undead,100;
```

---

<!-- RAG_CHUNK: autospell_bonuses -->
## 14. AutoSpell Bonuses

### Basic AutoSpell
```c
bonus3 bAutoSpell,sk,y,n;           // n/10% chance to cast sk lv y on attack
bonus3 bAutoSpellWhenHit,sk,y,n;    // n/10% chance when hit
```

### Advanced AutoSpell
```c
bonus4 bAutoSpell,sk,y,n,i;         // With target options i
bonus5 bAutoSpell,sk,y,n,bf,i;      // With trigger bf and target i
bonus4 bAutoSpellWhenHit,sk,y,n,i;
bonus5 bAutoSpellWhenHit,sk,y,n,bf,i;
// i options (bitfield):
//   &0 = cast on self
//   &1 = cast on enemy
//   &2 = random skill level [1..y]
//   &3 = 1+2 (random level on enemy)

bonus4 bAutoSpellOnSkill,sk,x,y,n;  // n/10% to cast x lv y when using sk
bonus5 bAutoSpellOnSkill,sk,x,y,n,i;
// i options:
//   &1 = force cast on self
//   &2 = random skill level
```

**Example:**
```c
// 10% chance to cast Fire Bolt lv 5 on attack
bonus3 bAutoSpell,"MG_FIREBOLT",5,100;

// 5% chance to cast Heal lv 10 on self when hit
bonus4 bAutoSpellWhenHit,"AL_HEAL",10,50,0;

// 20% chance to cast Storm Gust lv 1 when using Jupitel Thunder
bonus4 bAutoSpellOnSkill,"WZ_JUPITEL","WZ_STORMGUST",1,200;
```

---

<!-- RAG_CHUNK: drain_bonuses -->
## 15. HP/SP Drain Bonuses

### Value Drain
```c
bonus bHPDrainValue,n;          // Heal +n HP on attack
bonus2 bHPDrainValueRace,r,n;   // Heal +n HP vs race r
bonus2 bHpDrainValueClass,c,n;  // Heal +n HP vs class c
bonus bSPDrainValue,n;          // Heal +n SP on attack
bonus2 bSPDrainValueRace,r,n;   // Heal +n SP vs race r
bonus2 bSpDrainValueClass,c,n;  // Heal +n SP vs class c
```

### Rate Drain
```c
bonus2 bHPDrainRate,x,n;        // x/10% chance to drain n% HP from damage
bonus2 bSPDrainRate,x,n;        // x/10% chance to drain n% SP from damage
```

**Example:**
```c
// Drain 5 HP per hit
bonus bHPDrainValue,5;

// 10% chance to drain 5% of damage as HP
bonus2 bHPDrainRate,100,5;
```

### HP/SP Vanish (Enemy)
```c
bonus2 bHPVanishRate,x,n;           // x/10% chance to remove n% enemy HP
bonus3 bHPVanishRaceRate,r,x,n;     // vs race r
bonus3 bHPVanishRate,x,n,bf;        // with trigger bf
bonus2 bSPVanishRate,x,n;           // x/10% chance to remove n% enemy SP
bonus3 bSPVanishRaceRate,r,x,n;
bonus3 bSPVanishRate,x,n,bf;
```

### Kill Gain
```c
bonus bHPGainValue,n;           // +n HP on melee kill
bonus bSPGainValue,n;           // +n SP on melee kill
bonus2 bSPGainRace,r,n;         // +n SP on killing race r
bonus bLongHPGainValue,n;       // +n HP on ranged kill
bonus bLongSPGainValue,n;       // +n SP on ranged kill
bonus bMagicHPGainValue,n;      // +n HP on magic kill
bonus bMagicSPGainValue,n;      // +n SP on magic kill
```

---

<!-- RAG_CHUNK: reflect_bonuses -->
## 16. Damage Return Bonuses

```c
bonus bShortWeaponDamageReturn,n;   // Reflect n% melee damage
bonus bLongWeaponDamageReturn,n;    // Reflect n% ranged damage
bonus bMagicDamageReturn,n;         // n% chance to reflect magic
bonus bReduceDamageReturn,n;        // Reduce reflected damage by n%
```

**Example:**
```c
// Reflect 10% of melee damage
bonus bShortWeaponDamageReturn,10;

// 30% chance to reflect magic
bonus bMagicDamageReturn,30;
```

---

<!-- RAG_CHUNK: equipment_protection_bonuses -->
## 17. Equipment Protection Bonuses

### Unstripable
```c
bonus bUnstripableWeapon;       // Weapon immune to Strip
bonus bUnstripableArmor;        // Armor immune to Strip
bonus bUnstripableHelm;         // Helm immune to Strip
bonus bUnstripableShield;       // Shield immune to Strip
bonus bUnstripable;             // All equipment immune to Strip
```

### Unbreakable
```c
bonus bUnbreakableGarment;      // Garment cannot break
bonus bUnbreakableWeapon;       // Weapon cannot break
bonus bUnbreakableArmor;        // Armor cannot break
bonus bUnbreakableHelm;         // Helm cannot break
bonus bUnbreakableShield;       // Shield cannot break
bonus bUnbreakableShoes;        // Shoes cannot break
bonus bUnbreakable,n;           // Reduce break chance by n%
```

### Break Enemy Equipment
```c
bonus bBreakWeaponRate,n;       // n/100% chance to break enemy weapon
bonus bBreakArmorRate,n;        // n/100% chance to break enemy armor
```

**Example:**
```c
// All equipment immune to strip
bonus bUnstripable;

// 5% chance to break enemy weapon
bonus bBreakWeaponRate,500;
```

---

<!-- RAG_CHUNK: drop_bonuses -->
## 18. Monster Drop Bonuses

### Drop Rate Modifiers
```c
bonus2 bDropAddRace,r,x;        // +x% drop rate vs race r
bonus2 bDropAddClass,c,x;       // +x% drop rate vs class c
```

### Additional Drops
```c
bonus3 bAddMonsterIdDropItem,iid,mid,n; // n/100% chance to drop iid from monster mid
bonus2 bAddMonsterDropItem,iid,n;       // n/100% chance to drop iid
bonus3 bAddMonsterDropItem,iid,r,n;     // vs race r
bonus3 bAddClassDropItem,iid,c,n;       // vs class c
bonus2 bAddMonsterDropItemGroup,ig,n;   // n/100% chance for item from group ig
bonus3 bAddMonsterDropItemGroup,ig,r,n; // vs race r
bonus3 bAddClassDropItemGroup,ig,c,n;   // vs class c
```

**Example:**
```c
// +50% drop rate vs Undead
bonus2 bDropAddRace,RC_Undead,50;

// 10% chance to drop Old Blue Box from any monster
bonus2 bAddMonsterDropItem,603,1000;  // 603 = Old_Blue_Box

// 5% chance to drop Poring Card from Poring
bonus3 bAddMonsterIdDropItem,4001,1002,500;  // 4001=Poring_Card, 1002=Poring
```

### Zeny Gain
```c
bonus2 bGetZenyNum,x,n;         // n% chance to gain 1~x zeny (highest applied)
bonus2 bAddGetZenyNum,x,n;      // n% chance to gain 1~x zeny (stacks)
```

---

<!-- RAG_CHUNK: misc_bonuses -->
## 19. Miscellaneous Bonuses

### Double Attack/Splash
```c
bonus bDoubleRate,n;            // n% Double Attack (highest applied)
bonus bDoubleAddRate,n;         // +n% Double Attack
bonus bSplashRange,n;           // +n splash range (highest applied)
bonus bSplashAddRange,n;        // +n splash range (stacks)
```

### Special Effects
```c
bonus bRestartFullRecover;      // Full HP/SP on respawn
bonus bClassChange,n;           // n/100% chance to change monster class
bonus bAddStealRate,n;          // +n% Steal success rate
bonus bNoKnockback;             // Immune to knockback
bonus bNoGemStone;              // Skills don't consume gemstones
bonus bIntravision;             // See hidden enemies
bonus bPerfectHide;             // Hide from boss monsters
bonus bNoMadoFuel;              // Mado skills don't consume fuel
bonus bNoWalkDelay;             // No walk delay after being hit
```

### Skill-Related
```c
bonus2 bAddSkillBlow,sk,n;      // +n knockback cells for skill sk
bonus bNoInstantCast;           // Disable instant cast
bonus bDisableDEvade;           // Disable double evasion
```

### Counter/Reflect
```c
bonus bMagicCounter;            // Counter magic attacks
bonus bShortWeaponDamageReturn,n;
bonus bLongWeaponDamageReturn,n;
```

---

<!-- RAG_CHUNK: complete_bonus_list -->
## Complete Bonus Alphabetical Index

```
bAbsorbDmgMaxHP, bAbsorbDmgMaxHP2
bAddClass, bAddDamageClass, bAddDefMonster
bAddEff, bAddEff2, bAddEffOnSkill, bAddEffWhenHit
bAddEle, bAddGetZenyNum, bAddItemGroupHealRate
bAddItemGroupSPHealRate, bAddItemHealRate, bAddItemSPHealRate
bAddMaxWeight, bAddMDefMonster, bAddMagicDamageClass
bAddMonsterDropItem, bAddMonsterDropItemGroup
bAddMonsterIdDropItem, bAddRace, bAddRace2
bAddSize, bAddSkillBlow, bAddStealRate
bAgi, bAgiDexStr, bAgiVit, bAllStats, bAllTraitStats
bAspd, bAspdRate, bAtk, bAtk2, bAtkEle, bAtkRange, bAtkRate
bAutoSpell, bAutoSpellOnSkill, bAutoSpellWhenHit
bBaseAtk, bBreakArmorRate, bBreakWeaponRate
bCRate, bCRateRate, bCastrate, bClassChange
bCon, bComaClass, bComaRace, bCritAtkRate
bCritDefRate, bCritical, bCriticalAddRace
bCriticalDef, bCriticalLong, bCriticalRate, bCrt
bDef, bDef2, bDef2Rate, bDefEle, bDefRate
bDefRatioAtkClass, bDefRatioAtkEle, bDefRatioAtkRace
bDelayrate, bDex, bDisableDEvade
bDoubleAddRate, bDoubleRate, bDropAddClass, bDropAddRace
bExpAddClass, bExpAddRace
bFixedCast, bFixedCastrate, bFlee, bFlee2, bFlee2Rate, bFleeRate
bGetZenyNum
bHPDrainRate, bHPDrainValue, bHPDrainValueRace
bHPGainValue, bHPLossRate, bHPRegenRate, bHPVanishRate
bHPVanishRaceRate, bHPlus, bHPlusRate, bHPrecovRate
bHealPower, bHealPower2, bHit, bHitRate, bHpDrainValueClass
bIgnoreDefClass, bIgnoreDefClassRate, bIgnoreDefEle
bIgnoreDefRace, bIgnoreDefRaceRate
bIgnoreMDefEle, bIgnoreMDefRace
bIgnoreMdefClassRate, bIgnoreMdefRace2Rate, bIgnoreMdefRaceRate
bIgnoreMResRaceRate, bIgnoreResRaceRate
bInt, bIntravision
bLongAtkDef, bLongAtkRate, bLongHPGainValue, bLongSPGainValue
bLongWeaponDamageReturn, bLuk
bMRes, bMResRate, bMagicAddClass, bMagicAddEle
bMagicAddRace, bMagicAddRace2, bMagicAddSize
bMagicAtkDef, bMagicAtkEle, bMagicCounter
bMagicDamageReturn, bMagicHPGainValue, bMagicSPGainValue
bMagicSubDefEle, bMagicSubSize, bMatk, bMatk2, bMatkRate
bMaxAP, bMaxAPrate, bMaxHP, bMaxHPrate, bMaxSP, bMaxSPrate
bMdef, bMdef2, bMdef2Rate, bMdefRate, bMiscAtkDef
bNearAtkDef, bNoCastCancel, bNoCastCancel2
bNoGemStone, bNoInstantCast, bNoKnockback
bNoMadoFuel, bNoMagicDamage, bNoMiscDamage
bNoRegen, bNoSizeFix, bNoWalkDelay, bNoWeaponDamage
bPAtk, bPAtkRate, bPerfectHide, bPerfectHitAddRate, bPerfectHitRate
bPow, bReduceDamageReturn, bRegenPercentHP, bRegenPercentSP
bRes, bResEff, bResRate, bRestartFullRecover
bSMatk, bSMatkRate, bSPDrainRate, bSPDrainValue, bSPDrainValueRace
bSPGainRace, bSPGainValue, bSPLossRate, bSPRegenRate
bSPVanishRate, bSPVanishRaceRate, bSetDefRace, bSetMDefRace
bShortAtkRate, bShortWeaponDamageReturn
bSkillAtk, bSkillCooldown, bSkillDelay, bSkillFixedCast
bSkillHeal, bSkillHeal2, bSkillRatio, bSkillUseSP, bSkillUseSPrate
bSkillVariableCast, bSpDrainValueClass, bSpeedAddRate, bSpeedRate
bSpl, bSplashAddRange, bSplashRange, bSta, bStateNoRecoverRace
bStr, bSubClass, bSubDefEle, bSubEle, bSubRace, bSubRace2
bSubSize, bSubSkill
bUnbreakable, bUnbreakableArmor, bUnbreakableGarment
bUnbreakableHelm, bUnbreakableShield, bUnbreakableShoes
bUnbreakableWeapon, bUnstripable, bUnstripableArmor
bUnstripableHelm, bUnstripableShield, bUnstripableWeapon
bUseSPrate, bVariableCast, bVariableCastrate, bVit
bWeaponAtk, bWeaponAtkRate, bWeaponComaClass
bWeaponComaEle, bWeaponComaRace, bWeaponDamageRate
bWeaponMatkRate, bWeaponSubSize, bWis
```

---

*For complete syntax and constant definitions, see doc/item_bonus.txt*
