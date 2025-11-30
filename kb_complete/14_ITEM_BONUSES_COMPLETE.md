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
