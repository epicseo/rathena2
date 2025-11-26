---
title: rAthena Bonuses & Status Effects Reference
type: scripting_reference
category: rathena_scripting
tags: [bonus, status_change, item_effects, SC_, equipment]
version: 2.0
mode: SCRIPTING
chunk_strategy: BY_ENTRY
---

# rAthena Bonuses & Status Effects Reference

This KB provides complete documentation for item bonuses and status changes used in rAthena scripting.

**Search:** Use `bonus ` prefix for bonus commands, `SC_` prefix for status changes.

---

## Constants Reference

### Status Effect Constants (eff)
```
Eff_Bleeding, Eff_Blind, Eff_Burning, Eff_Confusion, Eff_Crystalize, Eff_Curse, Eff_DPoison,
Eff_Fear, Eff_Freeze, Eff_Poison, Eff_Silence, Eff_Sleep, Eff_Stone, Eff_Stun, Eff_Freezing,
Eff_Heat, Eff_Deepsleep, Eff_WhiteImprison, Eff_Hallucination
```

### Element Constants (e)
```
Ele_Dark, Ele_Earth, Ele_Fire, Ele_Ghost, Ele_Holy, Ele_Neutral, Ele_Poison,
Ele_Undead, Ele_Water, Ele_Wind, Ele_All
```

### Race Constants (r)
```
RC_Angel, RC_Brute, RC_DemiHuman, RC_Demon, RC_Dragon, RC_Fish, RC_Formless,
RC_Insect, RC_Plant, RC_Player_Human, RC_Player_Doram, RC_Undead, RC_All
```

### Monster Race Constants (mr)
```
RC2_Goblin, RC2_Kobold, RC2_Orc, RC2_Golem, RC2_Guardian, RC2_Ninja, RC2_GVG,
RC2_Battlefield, RC2_Treasure, RC2_BioLab, RC2_Manuk, RC2_Splendide, RC2_Scaraba
```

### Class Constants (c)
```
Class_Normal, Class_Boss, Class_Guardian, Class_All
```

### Size Constants (s)
```
Size_Small, Size_Medium, Size_Large, Size_All
```

### Trigger Criteria (bf)
| Flag | Effect |
|------|--------|
| BF_SHORT | Trigger on melee attacks |
| BF_LONG | Trigger on ranged attacks |
| BF_WEAPON | Trigger on weapon skills |
| BF_MAGIC | Trigger on magic skills |
| BF_MISC | Trigger on misc skills |
| BF_NORMAL | Trigger on normal attacks |
| BF_SKILL | Trigger on skills |

### AutoSpell Trigger (atf)
| Flag | Effect |
|------|--------|
| ATF_SELF | Trigger effect on self |
| ATF_TARGET | Trigger effect on target |
| ATF_SHORT | Trigger on melee attacks |
| ATF_LONG | Trigger on ranged attacks |
| ATF_WEAPON | Trigger on weapon/physical |
| ATF_MAGIC | Trigger on magic skills |
| ATF_MISC | Trigger on misc skills |

---

## 1. Basic Bonuses

### Base Stats
```
bonus bStr,n;           STR + n
bonus bAgi,n;           AGI + n
bonus bVit,n;           VIT + n
bonus bInt,n;           INT + n
bonus bDex,n;           DEX + n
bonus bLuk,n;           LUK + n
bonus bAllStats,n;      All stats + n
bonus bAgiVit,n;        AGI + n, VIT + n
bonus bAgiDexStr,n;     STR + n, AGI + n, DEX + n
```

### Trait Stats (4th Job)
```
bonus bPow,n;           POW + n
bonus bSta,n;           STA + n
bonus bWis,n;           WIS + n
bonus bSpl,n;           SPL + n
bonus bCon,n;           CON + n
bonus bCrt,n;           CRT + n
bonus bAllTraitStats,n; All trait stats + n
```

### HP/SP/AP
```
bonus bMaxHP,n;         MaxHP + n
bonus bMaxHPrate,n;     MaxHP + n%
bonus bMaxSP,n;         MaxSP + n
bonus bMaxSPrate,n;     MaxSP + n%
bonus bMaxAP,n;         MaxAP + n
bonus bMaxAPrate,n;     MaxAP + n%
```

### Attack/Defense
```
bonus bBaseAtk,n;       Basic attack power + n
bonus bAtk,n;           ATK + n (unofficial)
bonus bAtk2,n;          ATK2 + n
bonus bAtkRate,n;       ATK + n% (renewal only)
bonus bWeaponAtkRate,n; Weapon ATK + n%
bonus bMatk,n;          Magical attack power + n
bonus bMatkRate,n;      Magical attack power + n%
bonus bDef,n;           Equipment DEF + n
bonus bDefRate,n;       Equipment DEF + n%
bonus bMdef,n;          Equipment MDEF + n
bonus bMdefRate,n;      Equipment MDEF + n%
```

### Additional Stats
```
bonus bHit,n;           Hit + n
bonus bHitRate,n;       Hit + n%
bonus bCritical,n;      Critical + n
bonus bCriticalRate,n;  Critical + n%
bonus bFlee,n;          Flee + n
bonus bFleeRate,n;      Flee + n%
bonus bFlee2,n;         Perfect Dodge + n
bonus bAspd,n;          Attack speed + n
bonus bAspdRate,n;      Attack speed + n%
bonus bSpeedRate,n;     Movement speed + n% (highest only)
bonus bSpeedAddRate,n;  Movement speed + n% (stacks)
```

---

## 2. Extended Bonuses

### HP/SP Regeneration
```
bonus bHPrecovRate,n;           Natural HP recovery + n%
bonus bSPrecovRate,n;           Natural SP recovery + n%
bonus2 bHPRegenRate,n,t;        Gain n HP every t ms
bonus2 bHPLossRate,n,t;         Lose n HP every t ms
bonus2 bSPRegenRate,n,t;        Gain n SP every t ms
bonus2 bSPLossRate,n,t;         Lose n SP every t ms
bonus2 bRegenPercentHP,n,t;     Gain n% MaxHP every t ms
bonus2 bRegenPercentSP,n,t;     Gain n% MaxSP every t ms
bonus bNoRegen,x;               Stop regen (1=HP, 2=SP)
```

### SP Consumption
```
bonus bUseSPrate,n;             SP consumption + n%
bonus2 bSkillUseSP,sk,n;        Skill sk SP cost - n
bonus2 bSkillUseSPrate,sk,n;    Skill sk SP cost - n%
```

### Damage Modifiers
```
bonus2 bSkillAtk,sk,n;          Skill sk damage + n%
bonus bShortAtkRate,n;          Short range damage + n%
bonus bLongAtkRate,n;           Long range damage + n%
bonus bCritAtkRate,n;           Critical damage + n%
bonus bCritDefRate,n;           Critical damage received - n%
```

### Damage Reduction
```
bonus bNearAtkDef,n;            Melee physical reduction + n%
bonus bLongAtkDef,n;            Ranged physical reduction + n%
bonus bMagicAtkDef,n;           Magic damage reduction + n%
bonus bMiscAtkDef,n;            MISC damage reduction + n%
bonus bNoWeaponDamage,n;        Physical damage reduction + n%
bonus bNoMagicDamage,n;         Magic effect reduction + n%
```

### Healing
```
bonus bHealPower,n;             All heal skills + n%
bonus bHealPower2,n;            Heal received + n%
bonus2 bSkillHeal,sk,n;         Skill sk heal + n%
bonus bAddItemHealRate,n;       Item HP recovery + n%
bonus2 bAddItemHealRate,iid,n;  Item iid HP recovery + n%
```

### Cast Time
```
bonus bCastrate,n;              Cast time + n%
bonus2 bCastrate,sk,n;          Skill sk cast time + n%
bonus bFixedCastrate,n;         Fixed cast + n% (RENEWAL_CAST)
bonus bVariableCastrate,n;      Variable cast + n%
bonus bFixedCast,t;             Fixed cast + t ms
bonus bVariableCast,t;          Variable cast + t ms
bonus bNoCastCancel;            Prevent cast interrupt
bonus bNoCastCancel2;           Prevent cast interrupt (GvG too)
bonus bDelayrate,n;             Skill delay + n%
bonus2 bSkillCooldown,sk,t;     Skill sk cooldown + t ms
```

---

## 3. Group-Specific Bonuses

### Element Modifiers
```
bonus2 bAddEle,e,x;             +x% physical vs element e
bonus3 bAddEle,e,x,bf;          +x% physical vs element e (trigger bf)
bonus2 bMagicAddEle,e,x;        +x% magical vs element e
bonus2 bSubEle,e,x;             +x% reduction from element e
bonus3 bSubEle,e,x,bf;          +x% reduction from element e (trigger bf)
```

### Race Modifiers
```
bonus2 bAddRace,r,x;            +x% physical vs race r
bonus2 bMagicAddRace,r,x;       +x% magical vs race r
bonus2 bSubRace,r,x;            +x% reduction from race r
bonus2 bAddRace2,mr,x;          +x% vs monster race mr
bonus2 bSubRace2,mr,x;          +x% reduction from monster race mr
```

### Class/Size Modifiers
```
bonus2 bAddClass,c,x;           +x% physical vs class c
bonus2 bAddSize,s,x;            +x% physical vs size s
bonus2 bMagicAddSize,s,x;       +x% magical vs size s
bonus2 bSubSize,s,x;            +x% reduction from size s
bonus bNoSizeFix;               Ignore size modifier
```

### Ignore Defense
```
bonus bIgnoreDefEle,e;          Ignore DEF vs element e
bonus bIgnoreDefRace,r;         Ignore DEF vs race r
bonus bIgnoreDefClass,c;        Ignore DEF vs class c
bonus bIgnoreMDefRace,r;        Ignore MDEF vs race r
bonus2 bIgnoreDefRaceRate,r,n;  Ignore n% DEF vs race r
bonus2 bIgnoreMdefRaceRate,r,n; Ignore n% MDEF vs race r
```

---

## 4. Status-Related Bonuses

### Add Status Effect
```
bonus2 bAddEff,eff,n;           n/100% chance to inflict eff on attack
bonus2 bAddEff2,eff,n;          n/100% chance to inflict eff on self
bonus2 bAddEffWhenHit,eff,n;    n/100% chance to inflict eff when hit
bonus2 bResEff,eff,n;           n/100% resistance to eff

bonus3 bAddEff,eff,n,atf;       n/100% chance with trigger atf
bonus4 bAddEff,eff,n,atf,t;     n/100% for t ms with trigger atf
bonus3 bAddEffOnSkill,sk,eff,n; n/100% chance on skill sk
```

### Coma Effects
```
bonus2 bComaClass,c,n;          n/100% coma vs class c
bonus2 bComaRace,r,n;           n/100% coma vs race r
bonus2 bWeaponComaEle,e,n;      n/100% coma vs element e (normal attack)
bonus2 bWeaponComaRace,r,n;     n/100% coma vs race r (normal attack)
```

---

## 5. AutoSpell Bonuses

```
bonus3 bAutoSpell,sk,y,n;           n/10% cast skill sk lv y on attack
bonus3 bAutoSpellWhenHit,sk,y,n;    n/10% cast skill sk lv y when hit

bonus4 bAutoSpell,sk,y,n,i;         n/10% with options i
bonus5 bAutoSpell,sk,y,n,bf,i;      n/10% with trigger bf, options i
bonus4 bAutoSpellWhenHit,sk,y,n,i;  n/10% when hit with options i

bonus4 bAutoSpellOnSkill,sk,x,y,n;  n/10% cast x lv y when using skill sk
bonus5 bAutoSpellOnSkill,sk,x,y,n,i; n/10% with options i
```

**Options (i) bitfield:**
- &0 = cast on self
- &1 = cast on enemy
- &2 = random level [1..y]
- &3 = random level on enemy

---

## 6. Misc Bonuses

### HP/SP Drain
```
bonus bHPDrainValue,n;          Heal +n HP on attack
bonus bSPDrainValue,n;          Heal +n SP on attack
bonus2 bHPDrainRate,x,n;        x/10% chance to drain n% HP
bonus2 bSPDrainRate,x,n;        x/10% chance to drain n% SP
bonus2 bHPDrainValueRace,r,n;   Heal +n HP vs race r
bonus2 bSPDrainValueRace,r,n;   Heal +n SP vs race r
```

### HP/SP Vanish
```
bonus2 bHPVanishRate,x,n;       x/10% reduce enemy HP by n%
bonus2 bSPVanishRate,x,n;       x/10% reduce enemy SP by n%
bonus3 bHPVanishRaceRate,r,x,n; x/10% reduce race r HP by n%
```

### HP/SP Gain on Kill
```
bonus bHPGainValue,n;           +n HP on melee kill
bonus bSPGainValue,n;           +n SP on melee kill
bonus bLongHPGainValue,n;       +n HP on ranged kill
bonus bLongSPGainValue,n;       +n SP on ranged kill
bonus bMagicHPGainValue,n;      +n HP on magic kill
bonus bMagicSPGainValue,n;      +n SP on magic kill
```

### Damage Reflect
```
bonus bShortWeaponDamageReturn,n;   Reflect n% melee damage
bonus bLongWeaponDamageReturn,n;    Reflect n% ranged damage
bonus bMagicDamageReturn,n;         n% chance reflect magic
bonus bReduceDamageReturn,n;        Reduce reflected damage by n%
```

### Equipment Protection
```
bonus bUnstripableWeapon;       Weapon can't be stripped
bonus bUnstripableArmor;        Armor can't be stripped
bonus bUnstripableHelm;         Helm can't be stripped
bonus bUnstripableShield;       Shield can't be stripped
bonus bUnstripable;             All equipment can't be stripped

bonus bUnbreakableWeapon;       Weapon can't break
bonus bUnbreakableArmor;        Armor can't break
bonus bUnbreakable,n;           Reduce break chance by n%

bonus bBreakWeaponRate,n;       n/100% break enemy weapon
bonus bBreakArmorRate,n;        n/100% break enemy armor
```

### Monster Drops
```
bonus2 bDropAddRace,r,x;                +x% drop rate vs race r
bonus2 bDropAddClass,c,x;               +x% drop rate vs class c
bonus2 bAddMonsterDropItem,iid,n;       n/100% drop item iid
bonus3 bAddMonsterDropItem,iid,r,n;     n/100% drop iid vs race r
bonus2 bGetZenyNum,x,n;                 n% gain 1~x zeny on kill
```

### Misc Effects
```
bonus bDoubleRate,n;            n% double attack (all weapons)
bonus bDoubleAddRate,n;         +n% double attack
bonus bSplashRange,n;           Splash radius + n
bonus bSplashAddRange,n;        Splash radius + n (stacks)
bonus2 bAddSkillBlow,sk,n;      Knockback n cells on skill sk
bonus bNoKnockback;             Immune to knockback
bonus bNoGemStone;              No gemstone requirement
bonus bIntravision;             See hidden/cloaked units
bonus bPerfectHide;             Hide from detector monsters
bonus bRestartFullRecover;      Full HP/SP on revive
bonus bAddStealRate,n;          +n/100% steal rate
bonus bNoMadoFuel;              No Magic Gear fuel needed
bonus bNoWalkDelay;             Infinite Endure
```

---

# Status Changes Reference

## Usage Notes
- Use `sc_start` for basic status changes
- Use `sc_start2` when you need val1 and val2
- Use `sc_start4` when you need val1-val4
- Flag `SCSTART_LOADED(4)` skips internal calculations

---

## Negative Status Effects

### SC_STONE
**Effect:** DEF -50%; HP loss if HP>25%; MDEF +25%; Element→Earth; Can't move/attack/use skills
```
val2: Caster's object ID
val3: Incubation time
val4: Remaining tick
```

### SC_FREEZE
**Effect:** DEF -50%; FLEE=0; MDEF +25%; Element→Water; Can't move/attack

### SC_STUN
**Effect:** FLEE=0; Can't move/attack/use skills

### SC_SLEEP
**Effect:** FLEE=0; Enemy CRIT x2; Can't move/attack

### SC_POISON
**Effect:** DEF -25%; HP loss over time; No SP regen
```
val1: Skill Level
val2: Caster's object ID
val4: Remaining tick
```

### SC_CURSE
**Effect:** ATK -25%; LUK=0; Movement -300

### SC_SILENCE
**Effect:** Can't use active skills

### SC_CONFUSION
**Effect:** Random movement; DEF=(STR+(INT*50))

### SC_BLIND
**Effect:** HIT -25%; FLEE -25%; Screen darkened

### SC_BLEEDING
**Effect:** No HP/SP regen; HP loss over time
```
val1: Skill Level
val2: Caster's object ID
val4: Remaining tick
```

---

## Buff Status Effects

### SC_PROVOKE
**Effect:** DEF -(5+(5*Lv))%; ATK +(2+(3*Lv))%

### SC_ENDURE
**Effect:** MDEF +Lv; No flinch when attacked

### SC_TWOHANDQUICKEN
**Effect:** ASPD +30%

### SC_CONCENTRATE
**Effect:** AGI +(2+Lv)%; DEX +(2+Lv)%; Reveal hidden 3x3

### SC_BLESSING
**Effect:** STR/DEX/INT +Lv; Removes Stone/Curse

### SC_INCREASEAGI
**Effect:** AGI increase; Movement speed increase

### SC_ANGELUS
**Effect:** DEF +(5*Lv)%

### SC_KYRIE
**Effect:** Blocks damage up to (MaxHP*(Lv*2+10)/100)

### SC_MAGNIFICAT
**Effect:** SP Regen x2

### SC_GLORIA
**Effect:** LUK +30

### SC_IMPOSITIO
**Effect:** ATK +(5*Lv)

### SC_SUFFRAGIUM
**Effect:** Cast time -(15*Lv)%

### SC_ASPERSIO
**Effect:** Weapon element → Holy

---

## Combat Status Effects

### SC_AUTOGUARD
**Effect:** Chance to block attacks; 0.3s stop on activation

### SC_REFLECTSHIELD
**Effect:** Reflects (10+(3*Lv))% short range damage

### SC_DEFENDER
**Effect:** Long range damage -(5+(15*Lv))%; ASPD -(25+(5*Lv))

### SC_SPEARQUICKEN
**Effect:** With spear: ASPD +(20+Lv)%; CRIT +(3+(10*Lv)); FLEE +(2*Lv)

### SC_EDP
**Effect:** WATK +(100+(Lv*80))
```
val1: Skill Level
val2: Poison chance (val1+2)%
val3: Damage increase (50*(val1+1))
```

### SC_TRUESIGHT
**Effect:** All stats +5; Damage +(2*Lv)%; CRIT +Lv; HIT +(3*Lv)%
```
val1: Skill Level
val2: CRIT bonus
val3: HIT bonus
```

### SC_WINDWALK
**Effect:** FLEE increase; Movement speed increase
```
val1: Skill Level
val2: FLEE bonus
```

### SC_BERSERK
**Effect:** No regen; Can't use skills/chat; Max HP increase; ATK increase; DEF/MDEF=0
```
val1: Skill Level
val2: HP Penalty (5% MaxHP)
val3: Duration
val4: HP penalty interval
```

---

## Consumable Status Effects

### SC_ASPDPOTION0-3
**Effect:** ASPD increase (won't stack with other ASPD potions)
```
val1: +ASPD (Renewal)
val2: +% ASPD (Pre-Renewal)
```

### SC_SPEEDUP0/SC_SPEEDUP1
**Effect:** Movement speed increase (won't stack with bSpeedRate)
```
val1: +% Walkspeed
```

### SC_ATKPOTION
**Effect:** ATK increase
```
val1: +ATK
```

### SC_MATKPOTION
**Effect:** MATK increase
```
val1: +MATK
```

### SC_STRFOOD/AGIFOOD/VITFOOD/INTFOOD/DEXFOOD/LUKFOOD
**Effect:** Stat increase from food items
```
val1: +Stat value
```

---

## Equipment Status Effects

### SC_STRIPWEAPON
**Effect:** Unequip weapon; Mob ATK -25%

### SC_STRIPSHIELD
**Effect:** Unequip shield; Mob DEF -15%

### SC_STRIPARMOR
**Effect:** Unequip armor; Mob VIT -40%

### SC_STRIPHELM
**Effect:** Unequip helm; Mob INT -40%

### SC_CP_WEAPON/SHIELD/ARMOR/HELM
**Effect:** Protects equipment from damage and strip

---

## Special Status Effects

### SC_COMA
**Effect:** HP→1, SP→0
```
val1: Skill Level
val2: 1=keep SP
val3: Caster's object ID
```

### SC_ELEMENTALCHANGE
**Effect:** Change armor element
```
val1: Element level
val2: Element type
```

### SC_CLOSECONFINE
**Effect:** Confiner gets FLEE bonus
```
val1: Skill level
val2: Confined count
val3: +50 Flee
```

### SC_CLOSECONFINE2
**Effect:** Target is confined
```
val1: Skill level
val2: MapID of caster
```

---

*KB Version 2.0 | Mode: SCRIPTING | Source: doc/item_bonus.txt, doc/status_change.txt*
