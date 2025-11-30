# rAthena Item Bonuses Complete Reference v12.0
## ALL 263+ ITEM BONUSES (bonus, bonus2-5, autobonus)

---

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


---
# ENHANCED ITEM BONUSES REFERENCE
---

# rAthena Item Bonuses - Complete Reference
## All 263+ Item Bonus Types

---

<!-- RAG_CHUNK: bonus_overview_001 -->
## Item Bonus Overview

### Syntax Formats
```c
bonus <bonus type>,<value>;                    // Single value
bonus2 <bonus type>,<type>,<value>;            // Two parameters
bonus3 <bonus type>,<type>,<value>,<value2>;   // Three parameters
bonus4 <bonus type>,<type>,<val>,<val2>,<val3>; // Four parameters
bonus5 <bonus type>,<a>,<b>,<c>,<d>,<e>;       // Five parameters
```

### Usage Context
Item bonuses are used in:
- Item scripts in `item_db.yml`
- Equipment scripts
- Card scripts
- NPC scripts (temporary bonuses)

### Important Constants
```c
// Elements (e)
Ele_Neutral, Ele_Water, Ele_Earth, Ele_Fire, Ele_Wind,
Ele_Poison, Ele_Holy, Ele_Dark, Ele_Ghost, Ele_Undead, Ele_All

// Races (r)
RC_Formless, RC_Undead, RC_Brute, RC_Plant, RC_Insect,
RC_Fish, RC_Demon, RC_DemiHuman, RC_Angel, RC_Dragon,
RC_Player, RC_Boss, RC_NonBoss, RC_NonDemiHuman,
RC_NonPlayer, RC_DemiPlayer, RC_NonDemiPlayer, RC_All

// Classes (c)
Class_Normal, Class_Boss, Class_Guardian, Class_Battlefield, Class_All

// Sizes (s)
Size_Small, Size_Medium, Size_Large, Size_All

// Weapon Types (w)
W_FIST, W_DAGGER, W_1HSWORD, W_2HSWORD, W_1HSPEAR, W_2HSPEAR,
W_1HAXE, W_2HAXE, W_MACE, W_2HMACE, W_STAFF, W_BOW, W_KNUCKLE,
W_MUSICAL, W_WHIP, W_BOOK, W_KATAR, W_REVOLVER, W_RIFLE,
W_GATLING, W_SHOTGUN, W_GRENADE, W_HUUMA, W_2HSTAFF
```

---

<!-- RAG_CHUNK: basic_stats_001 -->
## Basic Stat Bonuses

### Primary Stats
| Bonus | Effect | Example |
|-------|--------|---------|
| bStr | +n STR | `bonus bStr,5;` |
| bAgi | +n AGI | `bonus bAgi,5;` |
| bVit | +n VIT | `bonus bVit,5;` |
| bInt | +n INT | `bonus bInt,5;` |
| bDex | +n DEX | `bonus bDex,5;` |
| bLuk | +n LUK | `bonus bLuk,5;` |
| bAllStats | +n to all stats | `bonus bAllStats,10;` |

### Trait Stats (4th Class)
| Bonus | Effect | Example |
|-------|--------|---------|
| bPow | +n POW | `bonus bPow,5;` |
| bSta | +n STA | `bonus bSta,5;` |
| bWis | +n WIS | `bonus bWis,5;` |
| bSpl | +n SPL | `bonus bSpl,5;` |
| bCon | +n CON | `bonus bCon,5;` |
| bCrt | +n CRT | `bonus bCrt,5;` |

---

<!-- RAG_CHUNK: hp_sp_bonuses_001 -->
## HP/SP Bonuses

### Flat Bonuses
| Bonus | Effect | Example |
|-------|--------|---------|
| bMaxHP | +n Max HP | `bonus bMaxHP,1000;` |
| bMaxSP | +n Max SP | `bonus bMaxSP,100;` |
| bMaxAP | +n Max AP | `bonus bMaxAP,50;` |

### Percentage Bonuses
| Bonus | Effect | Example |
|-------|--------|---------|
| bMaxHPrate | +n% Max HP | `bonus bMaxHPrate,10;` |
| bMaxSPrate | +n% Max SP | `bonus bMaxSPrate,10;` |

### Recovery
| Bonus | Effect | Example |
|-------|--------|---------|
| bHPrecovRate | +n% HP recovery rate | `bonus bHPrecovRate,50;` |
| bSPrecovRate | +n% SP recovery rate | `bonus bSPrecovRate,50;` |
| bHPRegenRate | +n HP/5sec | `bonus bHPRegenRate,100;` |
| bSPRegenRate | +n SP/5sec | `bonus bSPRegenRate,10;` |
| bNoRegen | Disable HP/SP regen | `bonus bNoRegen,1;` |
| bUseSPrate | +n% SP cost | `bonus bUseSPrate,-20;` |

---

<!-- RAG_CHUNK: combat_bonuses_001 -->
## Combat Bonuses

### Attack Power
| Bonus | Effect | Example |
|-------|--------|---------|
| bBaseAtk | +n base ATK | `bonus bBaseAtk,50;` |
| bAtk | +n total ATK | `bonus bAtk,50;` |
| bAtk2 | +n weapon ATK | `bonus bAtk2,50;` |
| bAtkRate | +n% ATK | `bonus bAtkRate,10;` |
| bWeaponAtkRate | +n% weapon ATK | `bonus bWeaponAtkRate,10;` |
| bMatk | +n MATK | `bonus bMatk,50;` |
| bMatkRate | +n% MATK | `bonus bMatkRate,10;` |

### Defense
| Bonus | Effect | Example |
|-------|--------|---------|
| bDef | +n DEF | `bonus bDef,50;` |
| bDefRate | +n% DEF | `bonus bDefRate,10;` |
| bDef2 | +n VIT DEF | `bonus bDef2,50;` |
| bDef2Rate | +n% VIT DEF | `bonus bDef2Rate,10;` |
| bMdef | +n MDEF | `bonus bMdef,50;` |
| bMdefRate | +n% MDEF | `bonus bMdefRate,10;` |
| bMdef2 | +n INT MDEF | `bonus bMdef2,50;` |
| bMdef2Rate | +n% INT MDEF | `bonus bMdef2Rate,10;` |

### Accuracy & Evasion
| Bonus | Effect | Example |
|-------|--------|---------|
| bHit | +n HIT | `bonus bHit,50;` |
| bHitRate | +n% HIT | `bonus bHitRate,10;` |
| bFlee | +n FLEE | `bonus bFlee,50;` |
| bFleeRate | +n% FLEE | `bonus bFleeRate,10;` |
| bFlee2 | +n Perfect Dodge | `bonus bFlee2,10;` |
| bFlee2Rate | +n% Perfect Dodge | `bonus bFlee2Rate,10;` |

### Critical
| Bonus | Effect | Example |
|-------|--------|---------|
| bCritical | +n CRIT | `bonus bCritical,20;` |
| bCriticalLong | +n% ranged CRIT rate | `bonus bCriticalLong,10;` |
| bCritAtkRate | +n% CRIT damage | `bonus bCritAtkRate,20;` |
| bCriticalDef | +n% CRIT resist | `bonus bCriticalDef,50;` |

### Attack Speed
| Bonus | Effect | Example |
|-------|--------|---------|
| bAspd | +n ASPD (raw) | `bonus bAspd,5;` |
| bAspdRate | +n% ASPD | `bonus bAspdRate,10;` |
| bAtkRange | +n attack range | `bonus bAtkRange,2;` |

---

<!-- RAG_CHUNK: damage_bonuses_001 -->
## Damage Modifiers

### Range-Based
| Bonus | Effect | Example |
|-------|--------|---------|
| bShortAtkRate | +n% melee damage | `bonus bShortAtkRate,10;` |
| bLongAtkRate | +n% ranged damage | `bonus bLongAtkRate,10;` |
| bLongAtkDef | +n% ranged damage reduction | `bonus bLongAtkDef,10;` |
| bNearAtkDef | +n% melee damage reduction | `bonus bNearAtkDef,10;` |

### Attack Type
| Bonus | Effect | Example |
|-------|--------|---------|
| bNoWeaponDamage | Immune to physical damage | `bonus bNoWeaponDamage,100;` |
| bNoMagicDamage | Immune to magical damage | `bonus bNoMagicDamage,100;` |
| bNoMiscDamage | Immune to misc damage | `bonus bNoMiscDamage,100;` |

---

<!-- RAG_CHUNK: element_bonuses_001 -->
## Element Bonuses

### Weapon Element
| Bonus | Effect | Example |
|-------|--------|---------|
| bAtkEle | Set weapon element | `bonus bAtkEle,Ele_Fire;` |
| bDefEle | Set armor element | `bonus bDefEle,Ele_Fire;` |

### Element Damage
| Bonus | Syntax | Effect |
|-------|--------|--------|
| bAddEle | `bonus2 bAddEle,e,x;` | +x% physical damage vs element |
| bMagicAddEle | `bonus2 bMagicAddEle,e,x;` | +x% magical damage vs element |
| bSubEle | `bonus2 bSubEle,e,x;` | +x% damage taken from element |
| bAddDefEle | `bonus2 bAddDefEle,e,x;` | +x% physical resist vs element |
| bMagicSubEle | `bonus2 bMagicSubEle,e,x;` | +x% magical resist vs element |

**Examples:**
```c
bonus2 bAddEle,Ele_Undead,20;     // +20% physical vs Undead element
bonus2 bSubEle,Ele_Fire,-30;       // -30% damage from Fire
bonus2 bMagicAddEle,Ele_Water,15; // +15% magical vs Water
```

---

<!-- RAG_CHUNK: race_bonuses_001 -->
## Race Bonuses

### Damage vs Race
| Bonus | Syntax | Effect |
|-------|--------|--------|
| bAddRace | `bonus2 bAddRace,r,x;` | +x% physical damage vs race |
| bMagicAddRace | `bonus2 bMagicAddRace,r,x;` | +x% magical damage vs race |
| bSubRace | `bonus2 bSubRace,r,x;` | +x% damage taken from race |
| bAddRace2 | `bonus2 bAddRace2,mr,x;` | +x% vs monster race |

**Examples:**
```c
bonus2 bAddRace,RC_DemiHuman,10;  // +10% vs Demi-Human
bonus2 bAddRace,RC_Boss,25;       // +25% vs Boss monsters
bonus2 bSubRace,RC_Demon,15;      // +15% resist vs Demon
```

### Monster Races (for bAddRace2)
```c
RC2_Goblin, RC2_Kobold, RC2_Orc, RC2_Golem, RC2_Guardian,
RC2_Ninja, RC2_Scaraba, RC2_Turtle, RC2_Dragon, RC2_Plant,
RC2_Bat, RC2_Clocktower, RC2_Thanatos, RC2_Bio5,
RC2_Faceworm, RC2_Hearthunter, RC2_Loli_Ruri, RC2_Illusion_Vampire
```

---

<!-- RAG_CHUNK: size_class_bonuses_001 -->
## Size & Class Bonuses

### Size Damage
| Bonus | Syntax | Effect |
|-------|--------|--------|
| bAddSize | `bonus2 bAddSize,s,x;` | +x% physical vs size |
| bMagicAddSize | `bonus2 bMagicAddSize,s,x;` | +x% magical vs size |
| bSubSize | `bonus2 bSubSize,s,x;` | +x% resist vs size |
| bNoSizeFix | Remove size penalty | `bonus bNoSizeFix,0;` |

### Class Damage
| Bonus | Syntax | Effect |
|-------|--------|--------|
| bAddClass | `bonus2 bAddClass,c,x;` | +x% vs class |
| bMagicAddClass | `bonus2 bMagicAddClass,c,x;` | +x% magical vs class |
| bSubClass | `bonus2 bSubClass,c,x;` | +x% resist vs class |

**Examples:**
```c
bonus2 bAddSize,Size_Large,15;    // +15% vs Large
bonus2 bSubSize,Size_Medium,10;   // +10% resist vs Medium
bonus2 bAddClass,Class_Boss,20;   // +20% vs Boss class
```

---

<!-- RAG_CHUNK: skill_bonuses_001 -->
## Skill Bonuses

### Skill Damage
| Bonus | Syntax | Effect |
|-------|--------|--------|
| bSkillAtk | `bonus2 bSkillAtk,sk,x;` | +x% damage of skill |
| bSkillHeal | `bonus2 bSkillHeal,sk,x;` | +x% healing of skill |
| bSkillHeal2 | `bonus2 bSkillHeal2,sk,x;` | +x% heal received from skill |

### Skill Cast
| Bonus | Syntax | Effect |
|-------|--------|--------|
| bVariableCastrate | +n% variable cast | `bonus bVariableCastrate,-10;` |
| bFixedCastrate | +n% fixed cast | `bonus bFixedCastrate,-10;` |
| bCastrate | +n% total cast | `bonus bCastrate,-10;` |
| bSkillVariableCast | `bonus2 bSkillVariableCast,sk,x;` | +x ms var cast for skill |
| bSkillFixedCast | `bonus2 bSkillFixedCast,sk,x;` | +x ms fixed cast for skill |
| bSkillCooldown | `bonus2 bSkillCooldown,sk,x;` | +x ms cooldown for skill |
| bSkillUseSPrate | `bonus2 bSkillUseSPrate,sk,x;` | +x% SP cost for skill |

**Examples:**
```c
bonus2 bSkillAtk,"MG_FIREBOLT",20;       // +20% Fire Bolt damage
bonus bVariableCastrate,-30;              // -30% variable cast time
bonus2 bSkillCooldown,"AS_SONICBLOW",-500; // -500ms Sonic Blow CD
```

---

<!-- RAG_CHUNK: status_bonuses_001 -->
## Status Effect Bonuses

### Inflict Status
| Bonus | Syntax | Effect |
|-------|--------|--------|
| bAddEff | `bonus2 bAddEff,sc,n;` | n/100% chance to inflict on attack |
| bAddEff2 | `bonus2 bAddEff2,sc,n;` | n/100% chance (self) |
| bAddEffWhenHit | `bonus2 bAddEffWhenHit,sc,n;` | n/100% on being hit |
| bAddEffOnSkill | `bonus3 bAddEffOnSkill,sk,sc,n;` | On skill use |

### Resist Status
| Bonus | Syntax | Effect |
|-------|--------|--------|
| bResEff | `bonus2 bResEff,sc,n;` | +n/100% resist |
| bAddEffOnSkill | Duration reduction | With ATF_SELF |

### Status Trigger Flags (ATF)
```c
ATF_SELF     = 1   // Affect self
ATF_TARGET   = 2   // Affect target
ATF_SHORT    = 4   // Melee attack
ATF_LONG     = 8   // Ranged attack
ATF_WEAPON   = 16  // Weapon attack
ATF_MAGIC    = 32  // Magic attack
ATF_MISC     = 64  // Misc attack
ATF_SKILL    = 128 // Skill use
```

**Examples:**
```c
bonus2 bAddEff,Eff_Stun,500;           // 5% stun on attack
bonus2 bAddEffWhenHit,Eff_Curse,100;   // 1% curse when hit
bonus2 bResEff,Eff_Freeze,5000;        // +50% freeze resist
bonus4 bAddEff,Eff_Poison,1000,ATF_WEAPON|ATF_SHORT,3000; // Complex
```

---

<!-- RAG_CHUNK: autospell_001 -->
## Auto Spell Bonuses

### On Attack
| Bonus | Syntax | Effect |
|-------|--------|--------|
| bAutoSpell | `bonus3 bAutoSpell,sk,lv,n;` | Cast skill on attack |
| bAutoSpellWhenHit | `bonus3 bAutoSpellWhenHit,sk,lv,n;` | Cast when hit |
| bAutoSpellOnSkill | `bonus4 bAutoSpellOnSkill,sk,sk2,lv,n;` | Cast on skill use |

### Parameters
- `sk` / `sk2` - Skill ID or name
- `lv` - Skill level
- `n` - Trigger rate (n/10 = %)

**Examples:**
```c
// 10% chance to cast Lv5 Fire Bolt on attack
bonus3 bAutoSpell,"MG_FIREBOLT",5,100;

// 5% chance to cast Lv1 Heal when hit
bonus3 bAutoSpellWhenHit,"AL_HEAL",1,50;

// When using Bash, 20% to cast Lv3 Magnum Break
bonus4 bAutoSpellOnSkill,"SM_BASH","MG_MAGNUMBREAK",3,200;
```

---

<!-- RAG_CHUNK: autobonus_001 -->
## Auto Bonus

### Syntax
```c
autobonus "<bonus script>",<rate>,<duration>{,<flag>{,"<other script>"}};
autobonus2 "<bonus script>",<rate>,<duration>{,<flag>{,"<other script>"}};
autobonus3 "<bonus script>",<rate>,<duration>,"<skill name>",{<flag>};
```

### Types
- `autobonus` - Triggers on attack
- `autobonus2` - Triggers when hit
- `autobonus3` - Triggers on skill use

### Parameters
- `rate` - Trigger chance (rate/10 = %)
- `duration` - Bonus duration (ms)
- `flag` - ATF flags
- `other script` - Script to run on trigger

**Examples:**
```c
// 5% on attack: +100 ATK for 10 seconds
autobonus "{ bonus bAtk,100; }",50,10000;

// 10% when hit: +50 DEF for 5 seconds
autobonus2 "{ bonus bDef,50; }",100,5000;

// On Bash use: +200 ATK for 3 seconds
autobonus3 "{ bonus bAtk,200; }",1000,3000,"SM_BASH";

// 3% on attack, ATK bonus + show effect
autobonus "{ bonus bAtk,150; }",30,10000,BF_WEAPON,"{ specialeffect2 EF_POTION_BERSERK; }";
```

---

<!-- RAG_CHUNK: drain_bonuses_001 -->
## HP/SP Drain

### Per Hit
| Bonus | Syntax | Effect |
|-------|--------|--------|
| bHPDrainValue | `bonus bHPDrainValue,n;` | Drain n HP per hit |
| bSPDrainValue | `bonus bSPDrainValue,n;` | Drain n SP per hit |
| bHPDrainRate | `bonus2 bHPDrainRate,x,n;` | x% chance to drain n% HP |
| bSPDrainRate | `bonus2 bSPDrainRate,x,n;` | x% chance to drain n% SP |

### On Damage
| Bonus | Syntax | Effect |
|-------|--------|--------|
| bHPDrainValueRace | `bonus2 bHPDrainValueRace,r,n;` | HP drain vs race |
| bSPDrainValueRace | `bonus2 bSPDrainValueRace,r,n;` | SP drain vs race |
| bHPVanishRate | `bonus2 bHPVanishRate,x,n;` | x% to remove n% target HP |
| bSPVanishRate | `bonus2 bSPVanishRate,x,n;` | x% to remove n% target SP |

**Examples:**
```c
bonus bHPDrainValue,10;              // +10 HP per hit
bonus2 bHPDrainRate,100,5;           // 100% to drain 5% HP
bonus2 bSPDrainValueRace,RC_Boss,5;  // +5 SP drain vs Boss
bonus2 bHPVanishRate,10,10;          // 10% to vanish 10% HP
```

---

<!-- RAG_CHUNK: special_bonuses_001 -->
## Special Bonuses

### Combat Mechanics
| Bonus | Effect | Example |
|-------|--------|---------|
| bDoubleRate | +n% double attack rate | `bonus bDoubleRate,15;` |
| bDoubleAddRate | +n% double attack rate | `bonus bDoubleAddRate,10;` |
| bSplashRange | +n splash range | `bonus bSplashRange,1;` |
| bSplashAddRange | +n splash range | `bonus bSplashAddRange,1;` |
| bPerfectHitRate | +n% perfect hit | `bonus bPerfectHitRate,50;` |
| bPerfectHitAddRate | +n% perfect hit (additive) | `bonus bPerfectHitAddRate,10;` |
| bIgnoreDefEle | Ignore DEF of element | `bonus bIgnoreDefEle,Ele_Ghost;` |
| bIgnoreDefRace | Ignore DEF of race | `bonus bIgnoreDefRace,RC_Boss;` |
| bIgnoreMDefEle | Ignore MDEF of element | `bonus bIgnoreMDefEle,Ele_Holy;` |
| bIgnoreMDefRace | Ignore MDEF of race | `bonus bIgnoreMDefRace,RC_Demon;` |
| bDefRatioAtkEle | DEF->ATK vs element | `bonus bDefRatioAtkEle,Ele_Undead;` |
| bDefRatioAtkRace | DEF->ATK vs race | `bonus bDefRatioAtkRace,RC_Plant;` |

### Restrictions
| Bonus | Effect | Example |
|-------|--------|---------|
| bUnbreakableWeapon | Weapon cannot break | `bonus bUnbreakableWeapon,0;` |
| bUnbreakableArmor | Armor cannot break | `bonus bUnbreakableArmor,0;` |
| bUnbreakableHelm | Helm cannot break | `bonus bUnbreakableHelm,0;` |
| bUnbreakableShield | Shield cannot break | `bonus bUnbreakableShield,0;` |
| bUnbreakableGarment | Garment cannot break | `bonus bUnbreakableGarment,0;` |
| bUnbreakableShoes | Shoes cannot break | `bonus bUnbreakableShoes,0;` |
| bNoGemStone | No catalyst required | `bonus bNoGemStone,0;` |
| bNoKnockback | Cannot be knocked back | `bonus bNoKnockback,0;` |
| bRestartFullRecover | Full HP/SP on respawn | `bonus bRestartFullRecover,0;` |

### Vision
| Bonus | Effect | Example |
|-------|--------|---------|
| bIntravision | See hidden targets | `bonus bIntravision,0;` |
| bPerfectHide | Hide from Sight/Ruwach | `bonus bPerfectHide,0;` |

---

<!-- RAG_CHUNK: reflect_counter_001 -->
## Reflect & Counter

### Reflect
| Bonus | Syntax | Effect |
|-------|--------|--------|
| bShortWeaponDamageReturn | `bonus bShortWeaponDamageReturn,n;` | Reflect n% melee physical |
| bLongWeaponDamageReturn | `bonus bLongWeaponDamageReturn,n;` | Reflect n% ranged physical |
| bMagicDamageReturn | `bonus bMagicDamageReturn,n;` | Reflect n% magic |

### Coma
| Bonus | Syntax | Effect |
|-------|--------|--------|
| bComaClass | `bonus2 bComaClass,c,n;` | n/100% coma vs class |
| bComaRace | `bonus2 bComaRace,r,n;` | n/100% coma vs race |

**Examples:**
```c
bonus bShortWeaponDamageReturn,10;   // 10% melee reflect
bonus2 bComaRace,RC_Brute,100;        // 1% coma vs Brute
```

---

#rathena #item #bonus #equipment #cards #stats #damage #skills #autospell #autobonus
