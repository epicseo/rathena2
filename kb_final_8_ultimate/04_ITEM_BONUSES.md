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

<!-- RAG_CHUNK: 04_bonus_constants -->

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

<!-- RAG_CHUNK: 04_1_basic_bonuses -->

<!-- RAG_CHUNK: 04_bStr -->
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

<!-- RAG_CHUNK: 04_bAgi -->
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

<!-- RAG_CHUNK: 04_bVit -->
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

<!-- RAG_CHUNK: 04_bInt -->
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

<!-- RAG_CHUNK: 04_bDex -->
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

<!-- RAG_CHUNK: 04_bLuk -->
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

<!-- RAG_CHUNK: 04_bAllStats -->
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

<!-- RAG_CHUNK: 04_bAgiVit -->
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

<!-- RAG_CHUNK: 04_bAgiDexStr -->
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

<!-- RAG_CHUNK: 04_bPow -->
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

<!-- RAG_CHUNK: 04_bSta -->
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

<!-- RAG_CHUNK: 04_bWis -->
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

<!-- RAG_CHUNK: 04_bSpl -->
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

<!-- RAG_CHUNK: 04_bCon -->
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

<!-- RAG_CHUNK: 04_bCrt -->
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

<!-- RAG_CHUNK: 04_bMaxHP -->
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

<!-- RAG_CHUNK: 04_bMaxHPrate -->
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

<!-- RAG_CHUNK: 04_bMaxSP -->
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

<!-- RAG_CHUNK: 04_bMaxSPrate -->
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

<!-- RAG_CHUNK: 04_bMaxAP -->
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

<!-- RAG_CHUNK: 04_bMaxAPrate -->
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

<!-- RAG_CHUNK: 04_bBaseAtk -->
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

<!-- RAG_CHUNK: 04_bAtk -->
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

<!-- RAG_CHUNK: 04_bAtk2 -->
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

<!-- RAG_CHUNK: 04_bAtkRate -->
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

<!-- RAG_CHUNK: 04_bMatk -->
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

<!-- RAG_CHUNK: 04_bMatk2 -->
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

<!-- RAG_CHUNK: 04_bMatkRate -->
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

<!-- RAG_CHUNK: 04_bDef -->
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

<!-- RAG_CHUNK: 04_bDefRate -->
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

<!-- RAG_CHUNK: 04_bDef2 -->
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

<!-- RAG_CHUNK: 04_bDef2Rate -->
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

<!-- RAG_CHUNK: 04_bMdef -->
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

<!-- RAG_CHUNK: 04_bMdefRate -->
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

<!-- RAG_CHUNK: 04_bMdef2 -->
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

<!-- RAG_CHUNK: 04_bMdef2Rate -->
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

<!-- RAG_CHUNK: 04_bHit -->
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

<!-- RAG_CHUNK: 04_bHitRate -->
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

<!-- RAG_CHUNK: 04_bCritical -->
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

<!-- RAG_CHUNK: 04_bCriticalLong -->
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

<!-- RAG_CHUNK: 04_bCriticalAddRace -->
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

<!-- RAG_CHUNK: 04_bCriticalRate -->
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

<!-- RAG_CHUNK: 04_bFlee -->
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

<!-- RAG_CHUNK: 04_bFleeRate -->
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

<!-- RAG_CHUNK: 04_bFlee2 -->
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

<!-- RAG_CHUNK: 04_bFlee2Rate -->
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

<!-- RAG_CHUNK: 04_bAspd -->
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

<!-- RAG_CHUNK: 04_bAspdRate -->
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

<!-- RAG_CHUNK: 04_bAtkRange -->
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

<!-- RAG_CHUNK: 04_bPAtk -->
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

<!-- RAG_CHUNK: 04_bPAtkRate -->
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

<!-- RAG_CHUNK: 04_bSMatk -->
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

<!-- RAG_CHUNK: 04_bSMatkRate -->
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

<!-- RAG_CHUNK: 04_bRes -->
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

<!-- RAG_CHUNK: 04_bResRate -->
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

<!-- RAG_CHUNK: 04_bMRes -->
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

<!-- RAG_CHUNK: 04_bMResRate -->
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

<!-- RAG_CHUNK: 04_bHPlus -->
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

<!-- RAG_CHUNK: 04_bHPlusRate -->
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

<!-- RAG_CHUNK: 04_bCRate -->
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

<!-- RAG_CHUNK: 04_bCRateRate -->
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

<!-- RAG_CHUNK: 04_bCriticalDef -->
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

<!-- RAG_CHUNK: 04_bAtkEle -->
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

<!-- RAG_CHUNK: 04_bDefEle -->
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

<!-- RAG_CHUNK: 04_bDefRatioAtkRace -->
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

<!-- RAG_CHUNK: 04_bDefRatioAtkEle -->
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

<!-- RAG_CHUNK: 04_bDefRatioAtkClass -->
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

<!-- RAG_CHUNK: 04_bResEff -->
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

<!-- RAG_CHUNK: 04_bStateNoRecoverRace -->
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

<!-- RAG_CHUNK: 04_bSplashRange -->
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

<!-- RAG_CHUNK: 04_bSplashAddRange -->
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

<!-- RAG_CHUNK: 04_bIntravision -->
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

<!-- RAG_CHUNK: 04_bRestartFullRecover -->
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

<!-- RAG_CHUNK: 04_2_extended_bonuses -->

<!-- RAG_CHUNK: 04_bHPrecovRate -->
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

<!-- RAG_CHUNK: 04_bSPrecovRate -->
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

<!-- RAG_CHUNK: 04_bHPRegenRate -->
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

<!-- RAG_CHUNK: 04_bHPLossRate -->
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

<!-- RAG_CHUNK: 04_bSPRegenRate -->
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

<!-- RAG_CHUNK: 04_bSPLossRate -->
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

<!-- RAG_CHUNK: 04_bUseSPrate -->
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

<!-- RAG_CHUNK: 04_bSkillUseSP -->
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

<!-- RAG_CHUNK: 04_bSkillUseSPrate -->
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

<!-- RAG_CHUNK: 04_bSkillAtk -->
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

<!-- RAG_CHUNK: 04_bShortAtkRate -->
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

<!-- RAG_CHUNK: 04_bLongAtkRate -->
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

<!-- RAG_CHUNK: 04_bCritAtkRate -->
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

<!-- RAG_CHUNK: 04_bHealPower -->
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

<!-- RAG_CHUNK: 04_bHealPower2 -->
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

<!-- RAG_CHUNK: 04_bAddItemHealRate -->
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

<!-- RAG_CHUNK: 04_bCastrate -->
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

<!-- RAG_CHUNK: 04_bFixedCastrate -->
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

<!-- RAG_CHUNK: 04_bVariableCastrate -->
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

<!-- RAG_CHUNK: 04_bFixedCast -->
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

<!-- RAG_CHUNK: 04_bVariableCast -->
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

<!-- RAG_CHUNK: 04_bNoCastCancel -->
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

<!-- RAG_CHUNK: 04_bNoCastCancel2 -->
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

<!-- RAG_CHUNK: 04_bDelayrate -->
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

<!-- RAG_CHUNK: 04_3_group-specific_bonuses -->

<!-- RAG_CHUNK: 04_bAddEle -->
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

<!-- RAG_CHUNK: 04_bMagicAddEle -->
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

<!-- RAG_CHUNK: 04_bSubEle -->
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

<!-- RAG_CHUNK: 04_bAddRace -->
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

<!-- RAG_CHUNK: 04_bMagicAddRace -->
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

<!-- RAG_CHUNK: 04_bSubRace -->
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

<!-- RAG_CHUNK: 04_bAddClass -->
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

<!-- RAG_CHUNK: 04_bSubClass -->
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

<!-- RAG_CHUNK: 04_bAddSize -->
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

<!-- RAG_CHUNK: 04_bSubSize -->
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

<!-- RAG_CHUNK: 04_bAddRace2 -->
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

<!-- RAG_CHUNK: 04_bSubRace2 -->
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

<!-- RAG_CHUNK: 04_bMagicAddRace2 -->
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

<!-- RAG_CHUNK: 04_bIgnoreDefEle -->
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

<!-- RAG_CHUNK: 04_bIgnoreDefRace -->
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

<!-- RAG_CHUNK: 04_bIgnoreDefClass -->
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

<!-- RAG_CHUNK: 04_bIgnoreDefRaceRate -->
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

<!-- RAG_CHUNK: 04_bIgnoreDefClassRate -->
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

<!-- RAG_CHUNK: 04_bExpAddRace -->
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

<!-- RAG_CHUNK: 04_bExpAddClass -->
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

<!-- RAG_CHUNK: 04_bAddClassDropItem -->
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

<!-- RAG_CHUNK: 04_bAddClassDropItemGroup -->
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

<!-- RAG_CHUNK: 04_4_status-related_bonuses -->

<!-- RAG_CHUNK: 04_bAddEff -->
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

<!-- RAG_CHUNK: 04_bAddEff2 -->
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

<!-- RAG_CHUNK: 04_bAddEffWhenHit -->
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

<!-- RAG_CHUNK: 04_bAddEffOnSkill -->
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

<!-- RAG_CHUNK: 04_bComaClass -->
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

<!-- RAG_CHUNK: 04_bComaRace -->
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

<!-- RAG_CHUNK: 04_bWeaponComaEle -->
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

<!-- RAG_CHUNK: 04_bWeaponComaClass -->
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

<!-- RAG_CHUNK: 04_bWeaponComaRace -->
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

<!-- RAG_CHUNK: 04_5_autospell_bonuses -->

<!-- RAG_CHUNK: 04_bAutoSpell -->
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

<!-- RAG_CHUNK: 04_bAutoSpellWhenHit -->
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

<!-- RAG_CHUNK: 04_bAutoSpellOnSkill -->
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

<!-- RAG_CHUNK: 04_6_misc_bonuses -->

<!-- RAG_CHUNK: 04_bAllTraitStats -->
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

<!-- RAG_CHUNK: 04_bWeaponAtkRate -->
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

<!-- RAG_CHUNK: 04_bWeaponMatkRate -->
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

<!-- RAG_CHUNK: 04_bPerfectHitRate -->
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

<!-- RAG_CHUNK: 04_bPerfectHitAddRate -->
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

<!-- RAG_CHUNK: 04_bSpeedRate -->
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

<!-- RAG_CHUNK: 04_bSpeedAddRate -->
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

<!-- RAG_CHUNK: 04_bAddMaxWeight -->
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

<!-- RAG_CHUNK: 04_bRegenPercentHP -->
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

<!-- RAG_CHUNK: 04_bRegenPercentSP -->
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

<!-- RAG_CHUNK: 04_bNoRegen -->
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

<!-- RAG_CHUNK: 04_bSkillRatio -->
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

<!-- RAG_CHUNK: 04_bCritDefRate -->
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

<!-- RAG_CHUNK: 04_bWeaponAtk -->
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

<!-- RAG_CHUNK: 04_bWeaponDamageRate -->
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

<!-- RAG_CHUNK: 04_bNearAtkDef -->
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

<!-- RAG_CHUNK: 04_bLongAtkDef -->
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

<!-- RAG_CHUNK: 04_bMagicAtkDef -->
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

<!-- RAG_CHUNK: 04_bMiscAtkDef -->
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

<!-- RAG_CHUNK: 04_bNoWeaponDamage -->
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

<!-- RAG_CHUNK: 04_bNoMagicDamage -->
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

<!-- RAG_CHUNK: 04_bNoMiscDamage -->
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

<!-- RAG_CHUNK: 04_bSkillHeal -->
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

<!-- RAG_CHUNK: 04_bSkillHeal2 -->
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

<!-- RAG_CHUNK: 04_bAddItemGroupHealRate -->
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

<!-- RAG_CHUNK: 04_bAddItemSPHealRate -->
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

<!-- RAG_CHUNK: 04_bAddItemGroupSPHealRate -->
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

<!-- RAG_CHUNK: 04_bSkillFixedCast -->
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

<!-- RAG_CHUNK: 04_bSkillVariableCast -->
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

<!-- RAG_CHUNK: 04_bSkillDelay -->
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

<!-- RAG_CHUNK: 04_bSkillCooldown -->
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

<!-- RAG_CHUNK: 04_bSubDefEle -->
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

<!-- RAG_CHUNK: 04_bMagicSubDefEle -->
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

<!-- RAG_CHUNK: 04_bMagicAddClass -->
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

<!-- RAG_CHUNK: 04_bMagicAddSize -->
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

<!-- RAG_CHUNK: 04_bWeaponSubSize -->
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

<!-- RAG_CHUNK: 04_bMagicSubSize -->
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

<!-- RAG_CHUNK: 04_bNoSizeFix -->
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

<!-- RAG_CHUNK: 04_bAddDamageClass -->
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

<!-- RAG_CHUNK: 04_bAddMagicDamageClass -->
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

<!-- RAG_CHUNK: 04_bAddDefMonster -->
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

<!-- RAG_CHUNK: 04_bAddMDefMonster -->
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

<!-- RAG_CHUNK: 04_bSubSkill -->
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

<!-- RAG_CHUNK: 04_bAbsorbDmgMaxHP -->
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

<!-- RAG_CHUNK: 04_bAbsorbDmgMaxHP2 -->
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

<!-- RAG_CHUNK: 04_bMagicAtkEle -->
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

<!-- RAG_CHUNK: 04_bSetDefRace -->
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

<!-- RAG_CHUNK: 04_bSetMDefRace -->
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

<!-- RAG_CHUNK: 04_bIgnoreMDefRace -->
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

<!-- RAG_CHUNK: 04_bIgnoreMdefRaceRate -->
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

<!-- RAG_CHUNK: 04_bIgnoreMdefRace2Rate -->
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

<!-- RAG_CHUNK: 04_bIgnoreMDefEle -->
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

<!-- RAG_CHUNK: 04_bIgnoreMdefClassRate -->
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

<!-- RAG_CHUNK: 04_bIgnoreResRaceRate -->
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

<!-- RAG_CHUNK: 04_bIgnoreMResRaceRate -->
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

<!-- RAG_CHUNK: 04_bHPDrainValue -->
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

<!-- RAG_CHUNK: 04_bHPDrainValueRace -->
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

<!-- RAG_CHUNK: 04_bHpDrainValueClass -->
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

<!-- RAG_CHUNK: 04_bSPDrainValue -->
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

<!-- RAG_CHUNK: 04_bSPDrainValueRace -->
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

<!-- RAG_CHUNK: 04_bSpDrainValueClass -->
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

<!-- RAG_CHUNK: 04_bHPDrainRate -->
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

<!-- RAG_CHUNK: 04_bSPDrainRate -->
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

<!-- RAG_CHUNK: 04_bHPVanishRate -->
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

<!-- RAG_CHUNK: 04_bHPVanishRaceRate -->
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

<!-- RAG_CHUNK: 04_bSPVanishRate -->
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

<!-- RAG_CHUNK: 04_bSPVanishRaceRate -->
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

<!-- RAG_CHUNK: 04_bHPGainValue -->
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

<!-- RAG_CHUNK: 04_bSPGainValue -->
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

<!-- RAG_CHUNK: 04_bSPGainRace -->
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

<!-- RAG_CHUNK: 04_bLongHPGainValue -->
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

<!-- RAG_CHUNK: 04_bLongSPGainValue -->
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

<!-- RAG_CHUNK: 04_bMagicHPGainValue -->
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

<!-- RAG_CHUNK: 04_bMagicSPGainValue -->
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

<!-- RAG_CHUNK: 04_bShortWeaponDamageReturn -->
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

<!-- RAG_CHUNK: 04_bLongWeaponDamageReturn -->
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

<!-- RAG_CHUNK: 04_bMagicDamageReturn -->
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

<!-- RAG_CHUNK: 04_bReduceDamageReturn -->
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

<!-- RAG_CHUNK: 04_bUnstripableWeapon -->
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

<!-- RAG_CHUNK: 04_bUnstripableArmor -->
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

<!-- RAG_CHUNK: 04_bUnstripableHelm -->
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

<!-- RAG_CHUNK: 04_bUnstripableShield -->
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

<!-- RAG_CHUNK: 04_bUnstripable -->
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

<!-- RAG_CHUNK: 04_bUnbreakableGarment -->
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

<!-- RAG_CHUNK: 04_bUnbreakableWeapon -->
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

<!-- RAG_CHUNK: 04_bUnbreakableArmor -->
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

<!-- RAG_CHUNK: 04_bUnbreakableHelm -->
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

<!-- RAG_CHUNK: 04_bUnbreakableShield -->
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

<!-- RAG_CHUNK: 04_bUnbreakableShoes -->
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

<!-- RAG_CHUNK: 04_bUnbreakable -->
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

<!-- RAG_CHUNK: 04_bBreakWeaponRate -->
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

<!-- RAG_CHUNK: 04_bBreakArmorRate -->
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

<!-- RAG_CHUNK: 04_bDropAddRace -->
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

<!-- RAG_CHUNK: 04_bDropAddClass -->
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

<!-- RAG_CHUNK: 04_bAddMonsterIdDropItem -->
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

<!-- RAG_CHUNK: 04_bAddMonsterDropItem -->
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

<!-- RAG_CHUNK: 04_bAddMonsterDropItemGroup -->
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

<!-- RAG_CHUNK: 04_bGetZenyNum -->
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

<!-- RAG_CHUNK: 04_bAddGetZenyNum -->
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

<!-- RAG_CHUNK: 04_bDoubleRate -->
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

<!-- RAG_CHUNK: 04_bDoubleAddRate -->
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

<!-- RAG_CHUNK: 04_bAddSkillBlow -->
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

<!-- RAG_CHUNK: 04_bNoKnockback -->
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

<!-- RAG_CHUNK: 04_bNoGemStone -->
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

<!-- RAG_CHUNK: 04_bPerfectHide -->
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

<!-- RAG_CHUNK: 04_bClassChange -->
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

<!-- RAG_CHUNK: 04_bAddStealRate -->
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

<!-- RAG_CHUNK: 04_bNoMadoFuel -->
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

<!-- RAG_CHUNK: 04_bNoWalkDelay -->
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

