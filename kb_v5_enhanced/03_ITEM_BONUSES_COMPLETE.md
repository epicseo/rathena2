# rAthena KB v5 - Item Bonuses Complete Reference

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

