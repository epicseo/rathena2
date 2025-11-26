# rAthena KB v6 - Item Bonuses Complete Reference

**Version:** 6.0 Complete  
**Generated:** 2025-11-26
**Source:** doc/item_bonus.txt
**Total Bonuses:** 263

---

## Quick Navigation

### By Category
- [Basic Stats](#basic-stats) - STR, AGI, VIT, INT, DEX, LUK
- [HP/SP](#hpsp-bonuses) - MaxHP, MaxSP, Regen
- [Attack/Defense](#attackdefense) - ATK, DEF, MATK, MDEF
- [Combat Stats](#combat-stats) - Hit, Flee, Critical, ASPD
- [Elemental](#elemental-bonuses) - Element damage/resist
- [Race Bonuses](#race-bonuses) - Race damage/resist
- [Status Effects](#status-effect-bonuses) - AddEff, ResEff
- [AutoSpell](#autospell-bonuses) - Auto-cast skills
- [Special](#special-bonuses) - Drain, Strip, Break

---

## Constants Reference

### Status Effect Constants (eff)
```
Eff_Stone, Eff_Freeze, Eff_Stun, Eff_Sleep, Eff_Poison,
Eff_Curse, Eff_Silence, Eff_Confusion, Eff_Blind, Eff_Bleeding,
Eff_DPoison, Eff_Fear, Eff_Burning, Eff_Freezing
```

### Race Constants (r)
```
RC_Formless, RC_Undead, RC_Brute, RC_Plant, RC_Insect,
RC_Fish, RC_Demon, RC_DemiHuman, RC_Angel, RC_Dragon,
RC_Player_Human, RC_Player_Doram, RC_All
```

### Element Constants (e)
```
Ele_Neutral, Ele_Water, Ele_Earth, Ele_Fire, Ele_Wind,
Ele_Poison, Ele_Holy, Ele_Dark, Ele_Ghost, Ele_Undead, Ele_All
```

### Size Constants (s)
```
Size_Small, Size_Medium, Size_Large, Size_All
```

### Class Constants (c)
```
Class_Normal, Class_Boss, Class_Guardian, Class_All
```

### Trigger Flags (bf)
```
BF_SHORT (melee), BF_LONG (ranged), BF_WEAPON, BF_MAGIC, BF_MISC
BF_NORMAL (normal attacks), BF_SKILL (skills)
```

---

## Complete Bonus Reference

## Basic Stats

<!-- RAG_CHUNK: bonus_basic_stats -->

### bStr

**Syntax:** `bonus bStr,n;`

**Effect:** STR + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bStr,n;
```

---

### bAgi

**Syntax:** `bonus bAgi,n;`

**Effect:** AGI + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bAgi,n;
```

---

### bVit

**Syntax:** `bonus bVit,n;`

**Effect:** VIT + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bVit,n;
```

---

### bInt

**Syntax:** `bonus bInt,n;`

**Effect:** INT + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bInt,n;
```

---

### bDex

**Syntax:** `bonus bDex,n;`

**Effect:** DEX + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bDex,n;
```

---

### bLuk

**Syntax:** `bonus bLuk,n;`

**Effect:** LUK + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bLuk,n;
```

---

### bAllStats

**Syntax:** `bonus bAllStats,n;`

**Effect:** STR + n, AGI + n, VIT + n, INT + n, DEX + n, LUK + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bAllStats,n;
```

---

### bAgiVit

**Syntax:** `bonus bAgiVit,n;`

**Effect:** AGI + n, VIT + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bAgiVit,n;
```

---

### bAgiDexStr

**Syntax:** `bonus bAgiDexStr,n;`

**Effect:** STR + n, AGI + n, DEX + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bAgiDexStr,n;
```

---

### bPow

**Syntax:** `bonus bPow,n;`

**Effect:** POW + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bPow,n;
```

---

### bSta

**Syntax:** `bonus bSta,n;`

**Effect:** STA + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bSta,n;
```

---

### bWis

**Syntax:** `bonus bWis,n;`

**Effect:** WIS + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bWis,n;
```

---

### bSpl

**Syntax:** `bonus bSpl,n;`

**Effect:** SPL + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bSpl,n;
```

---

### bCon

**Syntax:** `bonus bCon,n;`

**Effect:** CON + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bCon,n;
```

---

### bCrt

**Syntax:** `bonus bCrt,n;`

**Effect:** CRT + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bCrt,n;
```

---

### bStateNoRecoverRace

**Syntax:** `bonus3 bStateNoRecoverRace,r,x,t;`

**Effect:** Set a no recovery state of an enemy of race r at x/100% for t milliseconds with normal attack.

**Parameters:**
- `r`
- `x`
- `t`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus3 bStateNoRecoverRace,r,x,t;
```

---

### bSplashRange

**Syntax:** `bonus bSplashRange,n;`

**Effect:** Splash attack radius + n (only the highest among all is applied)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bSplashRange,n;
```

---

### bSplashAddRange

**Syntax:** `bonus bSplashAddRange,n;`

**Effect:** Splash attack radius + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bSplashAddRange,n;
```

---

### bIntravision

**Syntax:** `bonus bIntravision;`

**Effect:** Always see Hiding and Cloaking players/mobs

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bIntravision;
```

---

## HP/SP Bonuses

<!-- RAG_CHUNK: bonus_hpsp_bonuses -->

### bMaxHP

**Syntax:** `bonus bMaxHP,n;`

**Effect:** MaxHP + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bMaxHP,n;
```

---

### bMaxHPrate

**Syntax:** `bonus bMaxHPrate,n;`

**Effect:** MaxHP + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bMaxHPrate,n;
```

---

### bMaxSP

**Syntax:** `bonus bMaxSP,n;`

**Effect:** MaxSP + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bMaxSP,n;
```

---

### bMaxSPrate

**Syntax:** `bonus bMaxSPrate,n;`

**Effect:** MaxSP + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bMaxSPrate,n;
```

---

### bMaxAP

**Syntax:** `bonus bMaxAP,n;`

**Effect:** MaxAP + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bMaxAP,n;
```

---

### bMaxAPrate

**Syntax:** `bonus bMaxAPrate,n;`

**Effect:** MaxAP + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bMaxAPrate,n;
```

---

### bHPlus

**Syntax:** `bonus bHPlus,n;`

**Effect:** HPlus + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bHPlus,n;
```

---

### bHPlusRate

**Syntax:** `bonus bHPlusRate,n;`

**Effect:** HPlus + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bHPlusRate,n;
```

---

### bHPrecovRate

**Syntax:** `bonus bHPrecovRate,n;`

**Effect:** Natural HP recovery ratio + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bHPrecovRate,n;
```

---

### bSPrecovRate

**Syntax:** `bonus bSPrecovRate,n;`

**Effect:** Natural SP recovery ratio + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bSPrecovRate,n;
```

---

### bHPRegenRate

**Syntax:** `bonus2 bHPRegenRate,n,t;`

**Effect:** Gain n HP every t milliseconds

**Parameters:**
- `n`
- `t`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bHPRegenRate,n,t;
```

---

### bHPLossRate

**Syntax:** `bonus2 bHPLossRate,n,t;`

**Effect:** Lose n HP every t milliseconds

**Parameters:**
- `n`
- `t`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bHPLossRate,n,t;
```

---

### bSPRegenRate

**Syntax:** `bonus2 bSPRegenRate,n,t;`

**Effect:** Gain n SP every t milliseconds

**Parameters:**
- `n`
- `t`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bSPRegenRate,n,t;
```

---

### bSPLossRate

**Syntax:** `bonus2 bSPLossRate,n,t;`

**Effect:** Lose n SP every t milliseconds

**Parameters:**
- `n`
- `t`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bSPLossRate,n,t;
```

---

### bNoRegen

**Syntax:** `bonus bNoRegen,x;`

**Effect:** Stops HP or SP regeneration (x: 1=HP, 2=SP)

**Parameters:**
- `x`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bNoRegen,x;
```

---

### bUseSPrate

**Syntax:** `bonus bUseSPrate,n;`

**Effect:** SP consumption + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bUseSPrate,n;
```

---

### bHPDrainValue

**Syntax:** `bonus bHPDrainValue,n;`

**Effect:** Heals +n HP with a normal attack

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bHPDrainValue,n;
```

---

### bHPDrainValueRace

**Syntax:** `bonus2 bHPDrainValueRace,r,n;`

**Effect:** Heals +n HP when attacking a monster of race r with normal attack

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bHPDrainValueRace,r,n;
```

---

### bSPDrainValue

**Syntax:** `bonus bSPDrainValue,n;`

**Effect:** Heals +n SP with a normal attack

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bSPDrainValue,n;
```

---

### bSPDrainValueRace

**Syntax:** `bonus2 bSPDrainValueRace,r,n;`

**Effect:** Heals +n SP when attacking a monster of race r with normal attack

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bSPDrainValueRace,r,n;
```

---

### bHPDrainRate

**Syntax:** `bonus2 bHPDrainRate,x,n;`

**Effect:** Adds a x/10% chance to drain n% HP from inflicted damage when attacking

**Parameters:**
- `x`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bHPDrainRate,x,n;
```

---

### bSPDrainRate

**Syntax:** `bonus2 bSPDrainRate,x,n;`

**Effect:** Adds a x/10% chance to drain n% SP from inflicted damage when attacking

**Parameters:**
- `x`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bSPDrainRate,x,n;
```

---

### bHPVanishRate

**Syntax:** `bonus2 bHPVanishRate,x,n;`

**Effect:** Add a x/10% chance of decreasing enemy's HP amount by n% with a normal attack

**Parameters:**
- `x`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bHPVanishRate,x,n;
```

---

### bHPVanishRaceRate

**Syntax:** `bonus3 bHPVanishRaceRate,r,x,n;`

**Effect:** Add a x/10% chance of decreasing enemy's HP amount by n% when attacking, depends on enemy race r

**Parameters:**
- `r`
- `x`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus3 bHPVanishRaceRate,r,x,n;
```

---

### bHPVanishRate

**Syntax:** `bonus3 bHPVanishRate,x,n,bf;`

**Effect:** Add a x/10% chance of decreasing enemy's HP amount by n% when attacking with trigger criteria bf

**Parameters:**
- `x`
- `n`
- `bf`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus3 bHPVanishRate,x,n,bf;
```

---

### bSPVanishRate

**Syntax:** `bonus2 bSPVanishRate,x,n;`

**Effect:** Add a x/10% chance of decreasing enemy's SP amount by n% with a normal attack

**Parameters:**
- `x`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bSPVanishRate,x,n;
```

---

### bSPVanishRaceRate

**Syntax:** `bonus3 bSPVanishRaceRate,r,x,n;`

**Effect:** Add a x/10% chance of decreasing enemy's SP amount by n% when attacking, depends on enemy race r

**Parameters:**
- `r`
- `x`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus3 bSPVanishRaceRate,r,x,n;
```

---

### bSPVanishRate

**Syntax:** `bonus3 bSPVanishRate,x,n,bf;`

**Effect:** Add a x/10% chance of decreasing enemy's SP amount by n% when attacking with trigger criteria bf

**Parameters:**
- `x`
- `n`
- `bf`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus3 bSPVanishRate,x,n,bf;
```

---

### bHPGainValue

**Syntax:** `bonus bHPGainValue,n;`

**Effect:** Heals +n HP when killing an enemy with a melee-physical attack

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bHPGainValue,n;
```

---

### bSPGainValue

**Syntax:** `bonus bSPGainValue,n;`

**Effect:** Heals +n SP when killing an enemy with a melee-physical attack

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bSPGainValue,n;
```

---

### bSPGainRace

**Syntax:** `bonus2 bSPGainRace,r,n;`

**Effect:** Heals +n SP when killing an enemy of race r with a melee-physical attack

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bSPGainRace,r,n;
```

---

## Attack/Defense

<!-- RAG_CHUNK: bonus_attackdefense -->

### bBaseAtk

**Syntax:** `bonus bBaseAtk,n;`

**Effect:** Basic attack power + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bBaseAtk,n;
```

---

### bAtk

**Syntax:** `bonus bAtk,n;`

**Effect:** ATK + n (unofficial)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bAtk,n;
```

---

### bAtk2

**Syntax:** `bonus bAtk2,n;`

**Effect:** ATK2 + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bAtk2,n;
```

---

### bAtkRate

**Syntax:** `bonus bAtkRate,n;`

**Effect:** ATK + n% that won't interfere with Damage modifier and SC_EDP (renewal mode only)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bAtkRate,n;
```

---

### bWeaponAtkRate

**Syntax:** `bonus bWeaponAtkRate,n;`

**Effect:** Weapon ATK + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bWeaponAtkRate,n;
```

---

### bMatk

**Syntax:** `bonus bMatk,n;`

**Effect:** Magical attack power + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bMatk,n;
```

---

### bMatk2

**Syntax:** `bonus bMatk2,n;`

**Effect:** Magical attack power + n (not visible in status window)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bMatk2,n;
```

---

### bMatkRate

**Syntax:** `bonus bMatkRate,n;`

**Effect:** Magical attack power + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bMatkRate,n;
```

---

### bWeaponMatkRate

**Syntax:** `bonus bWeaponMatkRate,n;`

**Effect:** Weapon Magical ATK + n% (renewal mode only)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bWeaponMatkRate,n;
```

---

### bDef

**Syntax:** `bonus bDef,n;`

**Effect:** Equipment DEF + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bDef,n;
```

---

### bDefRate

**Syntax:** `bonus bDefRate,n;`

**Effect:** Equipment DEF + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bDefRate,n;
```

---

### bDef2

**Syntax:** `bonus bDef2,n;`

**Effect:** VIT based DEF + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bDef2,n;
```

---

### bDef2Rate

**Syntax:** `bonus bDef2Rate,n;`

**Effect:** VIT based DEF + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bDef2Rate,n;
```

---

### bMdef

**Syntax:** `bonus bMdef,n;`

**Effect:** Equipment MDEF + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bMdef,n;
```

---

### bMdefRate

**Syntax:** `bonus bMdefRate,n;`

**Effect:** Equipment MDEF + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bMdefRate,n;
```

---

### bMdef2

**Syntax:** `bonus bMdef2,n;`

**Effect:** INT based MDEF + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bMdef2,n;
```

---

### bMdef2Rate

**Syntax:** `bonus bMdef2Rate,n;`

**Effect:** INT based MDEF + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bMdef2Rate,n;
```

---

### bAtkRange

**Syntax:** `bonus bAtkRange,n;`

**Effect:** Attack range + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bAtkRange,n;
```

---

### bWeaponAtk

**Syntax:** `bonus2 bWeaponAtk,w,n;`

**Effect:** Adds n ATK when weapon of type w is equipped

**Parameters:**
- `w`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bWeaponAtk,w,n;
```

---

### bAtkEle

**Syntax:** `bonus bAtkEle,e;`

**Effect:** Gives the player's attacks element e

**Parameters:**
- `e`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bAtkEle,e;
```

---

### bDefEle

**Syntax:** `bonus bDefEle,e;`

**Effect:** Gives the player's defense element e

**Parameters:**
- `e`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bDefEle,e;
```

---

### bDefRatioAtkRace

**Syntax:** `bonus bDefRatioAtkRace,r;`

**Effect:** Deals more damage to enemies of race r with higher defense

**Parameters:**
- `r`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bDefRatioAtkRace,r;
```

---

### bDefRatioAtkEle

**Syntax:** `bonus bDefRatioAtkEle,e;`

**Effect:** Deals more damage to enemies of element e with higher defense

**Parameters:**
- `e`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bDefRatioAtkEle,e;
```

---

### bDefRatioAtkClass

**Syntax:** `bonus bDefRatioAtkClass,c;`

**Effect:** Deals more damage to enemies of class c with higher defense

**Parameters:**
- `c`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bDefRatioAtkClass,c;
```

---

## Combat Stats

<!-- RAG_CHUNK: bonus_combat_stats -->

### bHit

**Syntax:** `bonus bHit,n;`

**Effect:** Hit + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bHit,n;
```

---

### bHitRate

**Syntax:** `bonus bHitRate,n;`

**Effect:** Hit + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bHitRate,n;
```

---

### bCritical

**Syntax:** `bonus bCritical,n;`

**Effect:** Critical + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bCritical,n;
```

---

### bCriticalLong

**Syntax:** `bonus bCriticalLong,n;`

**Effect:** Critical + n for normal long ranged attack (won't be shown in status window)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bCriticalLong,n;
```

---

### bCriticalAddRace

**Syntax:** `bonus2 bCriticalAddRace,r,n;`

**Effect:** Critical + n against enemies of race r

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bCriticalAddRace,r,n;
```

---

### bCriticalRate

**Syntax:** `bonus bCriticalRate,n;`

**Effect:** Critical + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bCriticalRate,n;
```

---

### bFlee

**Syntax:** `bonus bFlee,n;`

**Effect:** Flee + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bFlee,n;
```

---

### bFleeRate

**Syntax:** `bonus bFleeRate,n;`

**Effect:** Flee + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bFleeRate,n;
```

---

### bFlee2

**Syntax:** `bonus bFlee2,n;`

**Effect:** Perfect Dodge + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bFlee2,n;
```

---

### bFlee2Rate

**Syntax:** `bonus bFlee2Rate,n;`

**Effect:** Perfect Dodge + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bFlee2Rate,n;
```

---

### bPerfectHitRate

**Syntax:** `bonus bPerfectHitRate,n;`

**Effect:** On-target impact attack probability n% (only the highest among all is applied)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bPerfectHitRate,n;
```

---

### bPerfectHitAddRate

**Syntax:** `bonus bPerfectHitAddRate,n;`

**Effect:** On-target impact attack probability + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bPerfectHitAddRate,n;
```

---

### bSpeedRate

**Syntax:** `bonus bSpeedRate,n;`

**Effect:** Movement speed + n% (only the highest among all is applied, won't be stacked with SC_SPEEDUP0, SC_SPEEDUP1)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bSpeedRate,n;
```

---

### bSpeedAddRate

**Syntax:** `bonus bSpeedAddRate,n;`

**Effect:** Movement speed + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bSpeedAddRate,n;
```

---

### bAspd

**Syntax:** `bonus bAspd,n;`

**Effect:** Attack speed + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bAspd,n;
```

---

### bAspdRate

**Syntax:** `bonus bAspdRate,n;`

**Effect:** Attack speed + n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bAspdRate,n;
```

---

### bAtkRange

**Syntax:** `bonus bAtkRange,n;`

**Effect:** Attack range + n

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bAtkRange,n;
```

---

### bCriticalDef

**Syntax:** `bonus bCriticalDef,n;`

**Effect:** Decreases the chance of being hit by critical hits by n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bCriticalDef,n;
```

---

## Elemental Bonuses

<!-- RAG_CHUNK: bonus_elemental_bonuses -->

### bAddEle

**Syntax:** `bonus2 bAddEle,e,x;`

**Effect:** +x% physical damage against element e

**Parameters:**
- `e`
- `x`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bAddEle,e,x;
```

---

### bAddEle

**Syntax:** `bonus3 bAddEle,e,x,bf;`

**Effect:** +x% physical damage against element e with trigger criteria bf

**Parameters:**
- `e`
- `x`
- `bf`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus3 bAddEle,e,x,bf;
```

---

### bMagicAddEle

**Syntax:** `bonus2 bMagicAddEle,e,x;`

**Effect:** +x% magical damage against element e

**Parameters:**
- `e`
- `x`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bMagicAddEle,e,x;
```

---

### bSubEle

**Syntax:** `bonus2 bSubEle,e,x;`

**Effect:** +x% damage reduction against attack element e

**Parameters:**
- `e`
- `x`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bSubEle,e,x;
```

---

### bSubEle

**Syntax:** `bonus3 bSubEle,e,x,bf;`

**Effect:** +x% damage reduction against attack element e with trigger criteria bf

**Parameters:**
- `e`
- `x`
- `bf`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus3 bSubEle,e,x,bf;
```

---

### bAtkEle

**Syntax:** `bonus bAtkEle,e;`

**Effect:** Gives the player's attacks element e

**Parameters:**
- `e`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bAtkEle,e;
```

---

### bDefEle

**Syntax:** `bonus bDefEle,e;`

**Effect:** Gives the player's defense element e

**Parameters:**
- `e`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bDefEle,e;
```

---

## Race Bonuses

<!-- RAG_CHUNK: bonus_race_bonuses -->

### bAddRace

**Syntax:** `bonus2 bAddRace,r,x;`

**Effect:** +x% physical damage against race r

**Parameters:**
- `r`
- `x`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bAddRace,r,x;
```

---

### bMagicAddRace

**Syntax:** `bonus2 bMagicAddRace,r,x;`

**Effect:** +x% magical damage against race r

**Parameters:**
- `r`
- `x`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bMagicAddRace,r,x;
```

---

### bSubRace

**Syntax:** `bonus2 bSubRace,r,x;`

**Effect:** +x% damage reduction against race r

**Parameters:**
- `r`
- `x`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bSubRace,r,x;
```

---

### bSubRace

**Syntax:** `bonus3 bSubRace,r,x,bf;`

**Effect:** +x% damage reduction against race r with trigger criteria bf

**Parameters:**
- `r`
- `x`
- `bf`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus3 bSubRace,r,x,bf;
```

---

### bAddRace2

**Syntax:** `bonus2 bAddRace2,mr,x;`

**Effect:** +x% damage against monster race mr

**Parameters:**
- `mr`
- `x`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bAddRace2,mr,x;
```

---

### bSubRace2

**Syntax:** `bonus2 bSubRace2,mr,x;`

**Effect:** +x% damage reduction against monster race mr

**Parameters:**
- `mr`
- `x`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bSubRace2,mr,x;
```

---

### bMagicAddRace2

**Syntax:** `bonus2 bMagicAddRace2,mr,x;`

**Effect:** +x% magic damage against monster race mr

**Parameters:**
- `mr`
- `x`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bMagicAddRace2,mr,x;
```

---

### bIgnoreDefRace

**Syntax:** `bonus bIgnoreDefRace,r;`

**Effect:** Disregard DEF against enemies of race r

**Parameters:**
- `r`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bIgnoreDefRace,r;
```

---

### bIgnoreDefRaceRate

**Syntax:** `bonus2 bIgnoreDefRaceRate,r,n;`

**Effect:** Disregard n% of the target's DEF if the target belongs to race r

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bIgnoreDefRaceRate,r,n;
```

---

### bExpAddRace

**Syntax:** `bonus2 bExpAddRace,r,x;`

**Effect:** Increase exp gained by x% against enemies of race r

**Parameters:**
- `r`
- `x`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bExpAddRace,r,x;
```

---

## Status Effect Bonuses

<!-- RAG_CHUNK: bonus_status_effect_bonuses -->

### bAddEff

**Syntax:** `bonus2 bAddEff,eff,n;`

**Effect:** Adds a n/100% chance to cause status eff on the target when attacking

**Parameters:**
- `eff`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bAddEff,eff,n;
```

---

### bAddEff2

**Syntax:** `bonus2 bAddEff2,eff,n;`

**Effect:** Adds a n/100% chance to cause status eff on self when attacking

**Parameters:**
- `eff`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bAddEff2,eff,n;
```

---

### bAddEffWhenHit

**Syntax:** `bonus2 bAddEffWhenHit,eff,n;`

**Effect:** Adds a n/100% chance to cause status eff on the enemy when being hit by physical damage

**Parameters:**
- `eff`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bAddEffWhenHit,eff,n;
```

---

### bResEff

**Syntax:** `bonus2 bResEff,eff,n;`

**Effect:** Adds a n/100% tolerance to status eff

**Parameters:**
- `eff`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bResEff,eff,n;
```

---

### bAddEff

**Syntax:** `bonus3 bAddEff,eff,n,atf;`

**Effect:** Adds a n/100% chance to cause status eff on the target when attacking

**Parameters:**
- `eff`
- `n`
- `atf`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus3 bAddEff,eff,n,atf;
```

---

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
# In item_db.yml
Script: |
  bonus4 bAddEff,eff,n,atf,t;
```

---

### bAddEffWhenHit

**Syntax:** `bonus3 bAddEffWhenHit,eff,n,atf;`

**Effect:** Adds a n/100% chance to cause status eff on the target when being hit by physical damage

**Parameters:**
- `eff`
- `n`
- `atf`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus3 bAddEffWhenHit,eff,n,atf;
```

---

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
# In item_db.yml
Script: |
  bonus4 bAddEffWhenHit,eff,n,atf,t;
```

---

### bAddEffOnSkill

**Syntax:** `bonus3 bAddEffOnSkill,sk,eff,n;`

**Effect:** Adds a n/100% chance to cause status eff on enemy when using skill sk

**Parameters:**
- `sk`
- `eff`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus3 bAddEffOnSkill,sk,eff,n;
```

---

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
# In item_db.yml
Script: |
  bonus4 bAddEffOnSkill,sk,eff,n,atf;
```

---

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
# In item_db.yml
Script: |
  bonus5 bAddEffOnSkill,sk,eff,n,atf,t;
```

---

### bComaClass

**Syntax:** `bonus2 bComaClass,c,n;`

**Effect:** Adds a n/100% chance to cause Coma when attacking a target of class c (regardless the type of attack)

**Parameters:**
- `c`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bComaClass,c,n;
```

---

### bComaRace

**Syntax:** `bonus2 bComaRace,r,n;`

**Effect:** Adds a n/100% chance to cause Coma when attacking a target of race r (regardless the type of attack)

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bComaRace,r,n;
```

---

### bWeaponComaEle

**Syntax:** `bonus2 bWeaponComaEle,e,n;`

**Effect:** Adds a n/100% chance to cause Coma when attacking a target of element e with a normal attack

**Parameters:**
- `e`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bWeaponComaEle,e,n;
```

---

### bWeaponComaClass

**Syntax:** `bonus2 bWeaponComaClass,c,n;`

**Effect:** Adds a n/100% chance to cause Coma when attacking a target of class c with a normal attack

**Parameters:**
- `c`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bWeaponComaClass,c,n;
```

---

### bWeaponComaRace

**Syntax:** `bonus2 bWeaponComaRace,r,n;`

**Effect:** Adds a n/100% chance to cause Coma when attacking a target of race r with a normal attack

**Parameters:**
- `r`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus2 bWeaponComaRace,r,n;
```

---

## AutoSpell Bonuses

<!-- RAG_CHUNK: bonus_autospell_bonuses -->

### bAutoSpell

**Syntax:** `bonus3 bAutoSpell,sk,y,n;`

**Effect:** Adds a n/10% chance to cast skill sk of level y when attacking

**Parameters:**
- `sk`
- `y`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus3 bAutoSpell,sk,y,n;
```

---

### bAutoSpellWhenHit

**Syntax:** `bonus3 bAutoSpellWhenHit,sk,y,n;`

**Effect:** Adds a n/10% chance to cast skill sk of level y when being hit by a direct attack

**Parameters:**
- `sk`
- `y`
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus3 bAutoSpellWhenHit,sk,y,n;
```

---

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
# In item_db.yml
Script: |
  bonus4 bAutoSpell,sk,y,n,i;
```

---

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
# In item_db.yml
Script: |
  bonus5 bAutoSpell,sk,y,n,bf,i;
```

---

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
# In item_db.yml
Script: |
  bonus4 bAutoSpellWhenHit,sk,y,n,i;
```

---

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
# In item_db.yml
Script: |
  bonus5 bAutoSpellWhenHit,sk,y,n,bf,i;
```

---

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
# In item_db.yml
Script: |
  bonus4 bAutoSpellOnSkill,sk,x,y,n;
```

---

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
# In item_db.yml
Script: |
  bonus5 bAutoSpellOnSkill,sk,x,y,n,i;
```

---

## Special Bonuses

<!-- RAG_CHUNK: bonus_special_bonuses -->

### bNoCastCancel

**Syntax:** `bonus bNoCastCancel;`

**Effect:** Prevents casting from being interrupted when hit (does not work in GvG)

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bNoCastCancel;
```

---

### bNoCastCancel2

**Syntax:** `bonus bNoCastCancel2;`

**Effect:** Prevents casting from being interrupted when hit (works even in GvG)

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bNoCastCancel2;
```

---

### bUnstripableWeapon

**Syntax:** `bonus bUnstripableWeapon;`

**Effect:** Weapon cannot be taken off via Strip skills

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bUnstripableWeapon;
```

---

### bUnstripableArmor

**Syntax:** `bonus bUnstripableArmor;`

**Effect:** Armor cannot be taken off via Strip skills

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bUnstripableArmor;
```

---

### bUnstripableHelm

**Syntax:** `bonus bUnstripableHelm;`

**Effect:** Helm cannot be taken off via Strip skills

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bUnstripableHelm;
```

---

### bUnstripableShield

**Syntax:** `bonus bUnstripableShield;`

**Effect:** Shield cannot be taken off via Strip skills

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bUnstripableShield;
```

---

### bUnstripable

**Syntax:** `bonus bUnstripable;`

**Effect:** All equipment cannot be taken off via strip skills

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bUnstripable;
```

---

### bUnbreakableGarment

**Syntax:** `bonus bUnbreakableGarment;`

**Effect:** Garment cannot be damaged/broken by any means

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bUnbreakableGarment;
```

---

### bUnbreakableWeapon

**Syntax:** `bonus bUnbreakableWeapon;`

**Effect:** Weapon cannot be damaged/broken by any means

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bUnbreakableWeapon;
```

---

### bUnbreakableArmor

**Syntax:** `bonus bUnbreakableArmor;`

**Effect:** Armor cannot be damaged/broken by any means

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bUnbreakableArmor;
```

---

### bUnbreakableHelm

**Syntax:** `bonus bUnbreakableHelm;`

**Effect:** Helm cannot be damaged/broken by any means

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bUnbreakableHelm;
```

---

### bUnbreakableShield

**Syntax:** `bonus bUnbreakableShield;`

**Effect:** Shield cannot be damaged/broken by any means

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bUnbreakableShield;
```

---

### bUnbreakableShoes

**Syntax:** `bonus bUnbreakableShoes;`

**Effect:** Shoes cannot be damaged/broken by any means

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bUnbreakableShoes;
```

---

### bUnbreakable

**Syntax:** `bonus bUnbreakable,n;`

**Effect:** Reduces the break chance of all equipped equipment by n%

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bUnbreakable,n;
```

---

### bBreakWeaponRate

**Syntax:** `bonus bBreakWeaponRate,n;`

**Effect:** Adds a n/100% chance to break enemy's weapon while attacking (stacks with other break chances)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bBreakWeaponRate,n;
```

---

### bDoubleRate

**Syntax:** `bonus bDoubleRate,n;`

**Effect:** Double Attack probability n% (works with all weapons | only the highest among all is applied)

**Parameters:**
- `n`

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bDoubleRate,n;
```

---

### bNoKnockback

**Syntax:** `bonus bNoKnockback;`

**Effect:** Character is no longer knocked back by enemy skills with such effect

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bNoKnockback;
```

---

### bIntravision

**Syntax:** `bonus bIntravision;`

**Effect:** Always see Hiding and Cloaking players/mobs

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bIntravision;
```

---

### bPerfectHide

**Syntax:** `bonus bPerfectHide;`

**Effect:** Hidden/cloaked character is no longer detected by monsters with 'detector' mode

**Example:**
```yml
# In item_db.yml
Script: |
  bonus bPerfectHide;
```

---

## Other Bonuses

<!-- RAG_CHUNK: bonus_other -->

### bAllTraitStats

**Syntax:** `bonus bAllTraitStats,n;`

**Effect:** POW + n, STA + n, WIS + n, SPL + n, CON + n, CRT + n

---

### bAddMaxWeight

**Syntax:** `bonus bAddMaxWeight,n;`

**Effect:** MaxWeight + n (in units of 0.1)

---

### bPAtk

**Syntax:** `bonus bPAtk,n;`

**Effect:** PAtk + n

---

### bPAtkRate

**Syntax:** `bonus bPAtkRate,n;`

**Effect:** PAtk + n%

---

### bSMatk

**Syntax:** `bonus bSMatk,n;`

**Effect:** SMatk + n

---

### bSMatkRate

**Syntax:** `bonus bSMatkRate,n;`

**Effect:** SMatk + n%

---

### bRes

**Syntax:** `bonus bRes,n;`

**Effect:** Res + n

---

### bResRate

**Syntax:** `bonus bResRate,n;`

**Effect:** Res + n%

---

### bMRes

**Syntax:** `bonus bMRes,n;`

**Effect:** MRes + n

---

### bMResRate

**Syntax:** `bonus bMResRate,n;`

**Effect:** MRes + n%

---

### bCRate

**Syntax:** `bonus bCRate,n;`

**Effect:** CRate + n

---

### bCRateRate

**Syntax:** `bonus bCRateRate,n;`

**Effect:** CRate + n%

---

### bRegenPercentHP

**Syntax:** `bonus2 bRegenPercentHP,n,t;`

**Effect:** Gain n% of max HP every t milliseconds

---

### bRegenPercentSP

**Syntax:** `bonus2 bRegenPercentSP,n,t;`

**Effect:** Gain n% of max SP every t milliseconds

---

### bSkillUseSP

**Syntax:** `bonus2 bSkillUseSP,sk,n;`

**Effect:** Decreases SP consumption of skill sk by n

---

### bSkillUseSPrate

**Syntax:** `bonus2 bSkillUseSPrate,sk,n;`

**Effect:** Decreases SP consumption of skill sk by n%

---

### bSkillAtk

**Syntax:** `bonus2 bSkillAtk,sk,n;`

**Effect:** Increases damage of skill sk by n%

---

### bSkillRatio

**Syntax:** `bonus bSkillRatio,n;`

**Effect:** Adds n to the skillratio of all attacks/skills that use it

---

### bShortAtkRate

**Syntax:** `bonus bShortAtkRate,n;`

**Effect:** Increases damage of short ranged attacks by n%

---

### bLongAtkRate

**Syntax:** `bonus bLongAtkRate,n;`

**Effect:** Increases damage of long ranged attacks by n%

---

### bCritAtkRate

**Syntax:** `bonus bCritAtkRate,n;`

**Effect:** Increases critical damage by +n%

---

### bCritDefRate

**Syntax:** `bonus bCritDefRate,n;`

**Effect:** Decreases critical damage received by n%

---

### bWeaponDamageRate

**Syntax:** `bonus2 bWeaponDamageRate,w,n;`

**Effect:** Adds n% damage to normal attacks when weapon of type w is equipped

---

### bNearAtkDef

**Syntax:** `bonus bNearAtkDef,n;`

**Effect:** Adds n% damage reduction against melee physical attacks

---

### bLongAtkDef

**Syntax:** `bonus bLongAtkDef,n;`

**Effect:** Adds n% damage reduction against ranged physical attacks

---

### bMagicAtkDef

**Syntax:** `bonus bMagicAtkDef,n;`

**Effect:** Adds n% damage reduction against magical attacks

---

### bMiscAtkDef

**Syntax:** `bonus bMiscAtkDef,n;`

**Effect:** Adds n% damage reduction against MISC attacks (traps, falcon, ...)

---

### bNoWeaponDamage

**Syntax:** `bonus bNoWeaponDamage,n;`

**Effect:** Adds n% reduction to received physical damage

---

### bNoMagicDamage

**Syntax:** `bonus bNoMagicDamage,n;`

**Effect:** Adds n% reduction to received magical effect (attack, healing, support spells are all blocked)

---

### bNoMiscDamage

**Syntax:** `bonus bNoMiscDamage,n;`

**Effect:** Adds n% reduction to received misc damage

---

### bHealPower

**Syntax:** `bonus bHealPower,n;`

**Effect:** Increases heal amount of all heal skills by n%

---

### bHealPower2

**Syntax:** `bonus bHealPower2,n;`

**Effect:** Increases heal amount if you are healed by any skills by n%

---

### bSkillHeal

**Syntax:** `bonus2 bSkillHeal,sk,n;`

**Effect:** Increases heal amount of skill sk by n%

---

### bSkillHeal2

**Syntax:** `bonus2 bSkillHeal2,sk,n;`

**Effect:** Increases heal amount if you are healed by skill sk by n%

---

### bAddItemHealRate

**Syntax:** `bonus bAddItemHealRate,n;`

**Effect:** Increases HP recovered by n% for healing items

---

### bAddItemHealRate

**Syntax:** `bonus2 bAddItemHealRate,iid,n;`

**Effect:** Increases HP recovered by n% for item iid

---

### bAddItemGroupHealRate

**Syntax:** `bonus2 bAddItemGroupHealRate,ig,n;`

**Effect:** Increases HP recovered by n% for items of item group ig

---

### bAddItemSPHealRate

**Syntax:** `bonus bAddItemSPHealRate,n;`

**Effect:** Increases SP recovered by n% for healing items

---

### bAddItemSPHealRate

**Syntax:** `bonus2 bAddItemSPHealRate,iid,n;`

**Effect:** Increases SP recovered by n% for item iid

---

### bAddItemGroupSPHealRate

**Syntax:** `bonus2 bAddItemGroupSPHealRate,ig,n;`

**Effect:** Increases SP recovered by n% for items of item group ig

---

### bCastrate

**Syntax:** `bonus bCastrate,n;`

**Effect:** Skill cast time rate + n%. (If RENEWAL_CAST is defined, this bonus is equal to bVariableCastrate)

---

### bCastrate

**Syntax:** `bonus2 bCastrate,sk,n;`

**Effect:** Adjust casting time of skill sk by n%.(If RENEWAL_CAST is defined, this bonus is equal to bVariableCastrate)

---

### bFixedCastrate

**Syntax:** `bonus bFixedCastrate,n;`

**Effect:** Increases fixed cast time of all skills by n% (has effect in RENEWAL_CAST only)

---

### bFixedCastrate

**Syntax:** `bonus2 bFixedCastrate,sk,n;`

**Effect:** Increases fixed cast time of skill sk by n% (has effect in RENEWAL_CAST only)

---

### bVariableCastrate

**Syntax:** `bonus bVariableCastrate,n;`

**Effect:** Increases variable cast time of all skills by n%. (If RENEWAL_CAST is NOT defined, this bonus is equal to bCastrate)

---

### bVariableCastrate

**Syntax:** `bonus2 bVariableCastrate,sk,n;`

**Effect:** Increases variable cast time of skill sk by n% (If RENEWAL_CAST is NOT defined, this bonus is equal to bCastrate)

---

### bFixedCast

**Syntax:** `bonus bFixedCast,t;`

**Effect:** Increases fixed cast time of all skills by t milliseconds (has effect in RENEWAL_CAST only)

---

### bSkillFixedCast

**Syntax:** `bonus2 bSkillFixedCast,sk,t;`

**Effect:** Increases fixed cast time of skill sk by t milliseconds (has effect in RENEWAL_CAST only)

---

### bVariableCast

**Syntax:** `bonus bVariableCast,t;`

**Effect:** Increases variable cast time of all skills by t milliseconds

---

### bSkillVariableCast

**Syntax:** `bonus2 bSkillVariableCast,sk,t;`

**Effect:** Increases variable cast time of skill sk by t milliseconds

---

### bDelayrate

**Syntax:** `bonus bDelayrate,n;`

**Effect:** Increases skill delay by n%

---

### bSkillDelay

**Syntax:** `bonus2 bSkillDelay,sk,t;`

**Effect:** Increases delay of skill sk by t milliseconds

---

### bSkillCooldown

**Syntax:** `bonus2 bSkillCooldown,sk,t;`

**Effect:** Increases cooldown of skill sk by t milliseconds

---

### bSubDefEle

**Syntax:** `bonus2 bSubDefEle,e,x;`

**Effect:** +x% physical damage reduction from enemy with defense element e

---

### bMagicSubDefEle

**Syntax:** `bonus2 bMagicSubDefEle,e,x;`

**Effect:** +x% magic damage reduction from enemy with defense element e

---

### bAddClass

**Syntax:** `bonus2 bAddClass,c,x;`

**Effect:** +x% physical damage against class c

---

### bMagicAddClass

**Syntax:** `bonus2 bMagicAddClass,c,x;`

**Effect:** +x% magical damage against class c

---

### bSubClass

**Syntax:** `bonus2 bSubClass,c,x;`

**Effect:** +x% damage reduction against class c

---

### bAddSize

**Syntax:** `bonus2 bAddSize,s,x;`

**Effect:** +x% physical damage against size s

---

### bMagicAddSize

**Syntax:** `bonus2 bMagicAddSize,s,x;`

**Effect:** +x% magical damage against size s

---

### bSubSize

**Syntax:** `bonus2 bSubSize,s,x;`

**Effect:** +x% damage reduction against size s

---

### bWeaponSubSize

**Syntax:** `bonus2 bWeaponSubSize,s,x;`

**Effect:** +x% physical damage reduction against size s

---

### bMagicSubSize

**Syntax:** `bonus2 bMagicSubSize,s,x;`

**Effect:** +x% magic damage reduction against size s

---

### bNoSizeFix

**Syntax:** `bonus bNoSizeFix;`

**Effect:** Ignores the size modifier when calculating damage

---

### bAddDamageClass

**Syntax:** `bonus2 bAddDamageClass,mid,x;`

**Effect:** +x% physical damage against monster mid

---

### bAddMagicDamageClass

**Syntax:** `bonus2 bAddMagicDamageClass,mid,x;`

**Effect:** +x% magical damage against monster mid

---

### bAddDefMonster

**Syntax:** `bonus2 bAddDefMonster,mid,x;`

**Effect:** +x% physical damage reduction against monster mid

---

### bAddMDefMonster

**Syntax:** `bonus2 bAddMDefMonster,mid,x;`

**Effect:** +x% magical damage reduction against monster mid

---

### bSubSkill

**Syntax:** `bonus2 bSubSkill,sk,n;`

**Effect:** Reduces n% damage received from skill sk

---

### bAbsorbDmgMaxHP

**Syntax:** `bonus bAbsorbDmgMaxHP,n;`

**Effect:** If the damage received is more than n% of Max HP, the damage received is [TotalDamage] - [n% of MaxHP] (Doesn't stack, will use the highest value) (Legacy rAthena behavior)

---

### bAbsorbDmgMaxHP2

**Syntax:** `bonus bAbsorbDmgMaxHP2,n;`

**Effect:** If the damage received is more than n% of Max HP, the damage received is reduced to n% of MaxHP (Doesn't stack, will use the highest value) (Official behavior)

---

### bMagicAtkEle

**Syntax:** `bonus2 bMagicAtkEle,e,x;`

**Effect:** Increases damage of e element magic by x%

---

### bSetDefRace

**Syntax:** `bonus4 bSetDefRace,r,n,t,y;`

**Effect:** Set DEF to y of an enemy of race r at n% for t milliseconds with normal attack

---

### bSetMDefRace

**Syntax:** `bonus4 bSetMDefRace,r,n,t,y;`

**Effect:** Set MDEF to y of an enemy of race r at n% for t milliseconds with normal attack

---

### bIgnoreDefEle

**Syntax:** `bonus bIgnoreDefEle,e;`

**Effect:** Disregard DEF against enemies of element e

---

### bIgnoreDefClass

**Syntax:** `bonus bIgnoreDefClass,c;`

**Effect:** Disregard DEF against enemies of class c

---

### bIgnoreMDefRace

**Syntax:** `bonus bIgnoreMDefRace,r;`

**Effect:** Disregard MDEF against enemies of race r

---

### bIgnoreMdefRaceRate

**Syntax:** `bonus2 bIgnoreMdefRaceRate,r,n;`

**Effect:** Disregard n% of the target's MDEF if the target belongs to race r

---

### bIgnoreMdefRace2Rate

**Syntax:** `bonus2 bIgnoreMdefRace2Rate,mr,n;`

**Effect:** Disregard n% of the target's MDEF if the target belongs to monster race mr

---

### bIgnoreMDefEle

**Syntax:** `bonus bIgnoreMDefEle,e;`

**Effect:** Disregard MDEF against enemies of element e

---

### bIgnoreDefClassRate

**Syntax:** `bonus2 bIgnoreDefClassRate,c,n;`

**Effect:** Disregard n% of the target's DEF if the target belongs to class c

---

### bIgnoreMdefClassRate

**Syntax:** `bonus2 bIgnoreMdefClassRate,c,n;`

**Effect:** Disregard n% of the target's MDEF if the target belongs to class c

---

### bIgnoreResRaceRate

**Syntax:** `bonus2 bIgnoreResRaceRate,r,n;`

**Effect:** Disregard n% of the target's Res if the target belongs to race r

---

### bIgnoreMResRaceRate

**Syntax:** `bonus2 bIgnoreMResRaceRate,r,n;`

**Effect:** Disregard n% of the target's MRes if the target belongs to race r

---

### bExpAddClass

**Syntax:** `bonus2 bExpAddClass,c,x;`

**Effect:** Increase exp gained by x% against enemies of class c

---

### bHpDrainValueClass

**Syntax:** `bonus2 bHpDrainValueClass,c,n;`

**Effect:** Heals +n HP when attacking a monster of class c with normal attack

---

### bSpDrainValueClass

**Syntax:** `bonus2 bSpDrainValueClass,c,n;`

**Effect:** Heals +n SP when attacking a monster of class c with normal attack

---

### bLongHPGainValue

**Syntax:** `bonus bLongHPGainValue,n;`

**Effect:** Heals +n HP when killing an enemy with a range-physical attack

---

### bLongSPGainValue

**Syntax:** `bonus bLongSPGainValue,n;`

**Effect:** Heals +n SP when killing an enemy with a range-physical attack

---

### bMagicHPGainValue

**Syntax:** `bonus bMagicHPGainValue,n;`

**Effect:** Heals +n HP when killing an enemy with a magical attack

---

### bMagicSPGainValue

**Syntax:** `bonus bMagicSPGainValue,n;`

**Effect:** Heals +n SP when killing an enemy with a magical attack

---

### bShortWeaponDamageReturn

**Syntax:** `bonus bShortWeaponDamageReturn,n;`

**Effect:** Reflects n% of received melee damage back to the enemy that caused it

---

### bLongWeaponDamageReturn

**Syntax:** `bonus bLongWeaponDamageReturn,n;`

**Effect:** Reflects n% of received ranged damage back to the enemy that caused it

---

### bMagicDamageReturn

**Syntax:** `bonus bMagicDamageReturn,n;`

**Effect:** Adds a n% chance to reflect targetted magic spells back to the enemy that caused it

---

### bReduceDamageReturn

**Syntax:** `bonus bReduceDamageReturn,n;`

**Effect:** Reduces reflected damage (melee/ranged/magic) by n%

---

### bBreakArmorRate

**Syntax:** `bonus bBreakArmorRate,n;`

**Effect:** Adds a n/100% chance to break enemy's armor while attacking (stacks with other break chances)

---

### bDropAddRace

**Syntax:** `bonus2 bDropAddRace,r,x;`

**Effect:** Adds x% to player's drop rate when killing a monster with race r.

---

### bDropAddClass

**Syntax:** `bonus2 bDropAddClass,c,x;`

**Effect:** Adds x% to player's drop rate when killing a monster with class c.

---

### bAddMonsterIdDropItem

**Syntax:** `bonus3 bAddMonsterIdDropItem,iid,mid,n;`

**Effect:** Adds a n/100% chance of dropping item iid when killing monster mid

---

### bAddMonsterDropItem

**Syntax:** `bonus2 bAddMonsterDropItem,iid,n;`

**Effect:** Adds a n/100% chance for item iid to be dropped when killing a monster

---

### bAddMonsterDropItem

**Syntax:** `bonus3 bAddMonsterDropItem,iid,r,n;`

**Effect:** Adds a n/100% chance for item iid to be dropped when killing a monster of race r

---

### bAddClassDropItem

**Syntax:** `bonus3 bAddClassDropItem,iid,c,n;`

**Effect:** Adds a n/100% chance for item iid to be dropped when killing a monster of class c

---

### bAddMonsterDropItemGroup

**Syntax:** `bonus2 bAddMonsterDropItemGroup,ig,n;`

**Effect:** Adds a n/100% chance to get an item of group type ig when killing a monster

---

### bAddMonsterDropItemGroup

**Syntax:** `bonus3 bAddMonsterDropItemGroup,ig,r,n;`

**Effect:** Adds a n/100% chance to get an item of group type ig when killing a monster of race r

---

### bAddClassDropItemGroup

**Syntax:** `bonus3 bAddClassDropItemGroup,ig,c,n;`

**Effect:** Adds a n/100% chance to get an item of group type ig when killing a monster of class c

---

### bGetZenyNum

**Syntax:** `bonus2 bGetZenyNum,x,n;`

**Effect:** Adds a n% chance of gaining 1~x zeny when killing a monster (only the highest among all is applied)

---

### bAddGetZenyNum

**Syntax:** `bonus2 bAddGetZenyNum,x,n;`

**Effect:** Adds a n% chance of gaining 1~x zeny when killing a monster

---

### bDoubleAddRate

**Syntax:** `bonus bDoubleAddRate,n;`

**Effect:** Double Attack probability + n% (works with all weapons)

---

### bAddSkillBlow

**Syntax:** `bonus2 bAddSkillBlow,sk,n;`

**Effect:** Knock back the target by n cells when using skill sk

---

### bNoGemStone

**Syntax:** `bonus bNoGemStone;`

**Effect:** Skills requiring Gemstones do not require them

---

### bRestartFullRecover

**Syntax:** `bonus bRestartFullRecover;`

**Effect:** When reviving, HP and SP are fully healed

---

### bClassChange

**Syntax:** `bonus bClassChange,n;`

**Effect:** Gives a n/100% chance to change the attacked monster's class with normal attack

---

### bAddStealRate

**Syntax:** `bonus bAddStealRate,n;`

**Effect:** Increases success rate of Steal skill by n/100%

---

### bNoMadoFuel

**Syntax:** `bonus bNoMadoFuel;`

**Effect:** Nullify Magic Gear Fuel requirement for skills.

---

### bNoWalkDelay

**Syntax:** `bonus bNoWalkDelay;`

**Effect:** Give infinite Endure.

---

