# rAthena KB v5 - Game Mechanics Reference

**Version:** 5.0 Enhanced
**Generated:** 2025-11-26
**Coverage:** Damage formulas, mapflags, battle config

---

## Quick Navigation

- [Damage Formulas](#damage-formulas)
- [Map Flags](#map-flags)
- [Battle Configuration](#battle-configuration)
- [Element Table](#element-table)
- [Size Modifiers](#size-modifiers)

---

## Damage Formulas

<!-- RAG_CHUNK: damage_formulas -->

### Physical Damage (Renewal)

```
Base Damage = (Status ATK + Weapon ATK + Weapon Refine Bonus + Equipment ATK)
Final Damage = Base Damage * Modifiers * Element Modifier * Size Modifier / Defense
```

**Key Components:**
- **Status ATK:** Based on STR/DEX (varies by weapon type)
- **Weapon ATK:** Weapon's base attack value
- **Refine Bonus:** +1 per refine (varies by weapon level)
- **Equipment ATK:** Bonuses from equipment scripts

### Status ATK Calculation
```
# For most melee weapons:
Status ATK = floor(BaseLevel/4 + STR + STR/10^2 + DEX/5)

# For ranged weapons (bow, gun):
Status ATK = floor(BaseLevel/4 + DEX + DEX/10^2 + STR/5)
```

### Magical Damage (Renewal)

```
MATK = Status MATK + Weapon MATK + Equipment MATK
Magic Damage = MATK * Skill Modifier * Element Modifier / MDEF
```

**Status MATK:**
```
Status MATK = floor(BaseLevel/4 + INT + INT/2^2)
```

### Critical Damage
```
Critical Damage = Normal Damage * 1.4 (base) + Critical Damage Bonuses
Critical Rate = (LUK * 0.3 + Critical bonuses) / Target_Cri_Resist
```

### Flee Calculation
```
Flee = BaseLevel + AGI + Flee bonuses
Perfect Dodge = LUK / 10
Hit Chance = (Hit - Flee + 80)%  // Capped at 5%-100%
```

---

## Map Flags

<!-- RAG_CHUNK: mapflags -->

### Common Map Flags

| Flag | Description | Usage |
|------|-------------|-------|
| `nomemo` | Disable /memo command | PvP maps |
| `noteleport` | Disable teleport skills | Dungeons |
| `nosave` | Respawn at save point | Dungeons |
| `nobranch` | Disable Dead Branch | Towns |
| `nowarpto` | Block @warp to this map | Private |
| `nowarp` | Block @warp from this map | Dungeons |
| `noicewall` | Block Ice Wall | PvP |
| `nopenalty` | No death penalty | Events |
| `nozenypenalty` | No zeny loss on death | Events |
| `pvp` | Enable PvP mode | PvP maps |
| `gvg` | Enable GvG mode | WoE maps |
| `gvg_castle` | WoE castle map | WoE |
| `gvg_dungeon` | WoE dungeon map | WoE |
| `pvp_nightmaredrop` | Drop items on death | Hardcore |
| `restricted <n>` | Item/skill restrictions | Special |
| `skill_damage` | Modify skill damage | Balance |
| `nousecart` | Disable cart | Dungeons |
| `nomobhp` | Hide mob HP bar | Special |
| `partylock` | Cannot change party | Instance |
| `guildlock` | Cannot change guild | Instance |
| `loadevent` | Trigger OnPCLoadMapEvent | Script |
| `nochat` | Disable chat | Jail |
| `noitemconsumption` | Items not consumed | Events |
| `summonstarmiracle` | Enable Star Miracle | SG maps |
| `noskill` | Disable all skills | Safe zone |
| `nocommand <lv>` | Disable @commands | Security |
| `monster_noteleport` | Monsters can't teleport | Dungeons |
| `reset` | Reset position on death | Instance |

### Map Flag Syntax in map_zone_db.yml
```yaml
Body:
  - Zone: Normal
    Mapflags:
      - Flag: restricted
        Value: 1
    DisabledSkills:
      - ALL_INCCARRY
    DisabledItems:
      - Apple: true
```

### Map Flag Script Usage
```c
// Set mapflag
setmapflag "<map>", mf_pvp;
setmapflag "<map>", mf_restricted, 1;

// Remove mapflag
removemapflag "<map>", mf_pvp;

// Check mapflag
if (getmapflag("<map>", mf_pvp)) {
    mes "This is a PvP map!";
}
```

---

## Battle Configuration

<!-- RAG_CHUNK: battle_config -->

### Key Battle Settings (conf/battle/)

**Damage Settings:**
| Setting | Default | Description |
|---------|---------|-------------|
| weapon_defense_type | 0 | 0=Subtract, 1=Rate |
| magic_defense_type | 0 | 0=Subtract, 1=Rate |
| attribute_recover | false | Heal with element advantage |
| natural_healhp_interval | 6000 | HP regen interval (ms) |
| natural_healsp_interval | 8000 | SP regen interval (ms) |

**PvP Settings:**
| Setting | Default | Description |
|---------|---------|-------------|
| pk_mode | 0 | Enable PK on all maps |
| pk_level_range | 0 | Level diff for PK |
| pvp_exp_penalty | true | Lose EXP on PvP death |
| pvp_noDamage_0_internal | false | 0-damage hits are misses |

**WoE Settings:**
| Setting | Default | Description |
|---------|---------|-------------|
| gvg_flee_penalty | 20 | Flee reduction in GvG |
| gvg_short_damage_rate | 80 | Short range dmg in GvG |
| gvg_long_damage_rate | 80 | Long range dmg in GvG |
| gvg_weapon_damage_rate | 60 | Weapon dmg in GvG |
| gvg_magic_damage_rate | 60 | Magic dmg in GvG |
| gvg_misc_damage_rate | 60 | Misc dmg in GvG |

---

## Element Table

<!-- RAG_CHUNK: element_table -->

### Element Damage Modifiers (%)

| Attack \ Def | Neutral | Water | Earth | Fire | Wind | Poison | Holy | Dark | Ghost | Undead |
|---------------|---------|-------|-------|------|------|--------|------|------|-------|--------|
| **Neutral**   | 100 | 100 | 100 | 100 | 100 | 100 | 100 | 100 | 25 | 100 |
| **Water**     | 100 | 25 | 100 | 150 | 90 | 100 | 100 | 100 | 100 | 100 |
| **Earth**     | 100 | 100 | 100 | 90 | 150 | 100 | 100 | 100 | 100 | 100 |
| **Fire**      | 100 | 90 | 150 | 25 | 100 | 100 | 100 | 100 | 100 | 125 |
| **Wind**      | 100 | 150 | 90 | 100 | 25 | 100 | 100 | 100 | 100 | 100 |
| **Poison**    | 100 | 100 | 100 | 100 | 100 | 0 | 100 | 50 | 100 | -25 |
| **Holy**      | 100 | 75 | 75 | 75 | 75 | 75 | 0 | 125 | 75 | 150 |
| **Dark**      | 100 | 100 | 100 | 100 | 100 | 50 | 125 | 0 | 75 | -25 |
| **Ghost**     | 25 | 100 | 100 | 100 | 100 | 100 | 100 | 100 | 125 | 100 |
| **Undead**    | 100 | 100 | 100 | 125 | 100 | -25 | 150 | -25 | 100 | 0 |

*Values below 100 = resistance, above 100 = weakness*
*Negative values = heal instead of damage*

### Element Levels
Monsters have element levels 1-4. Higher levels increase resistance/weakness effects.

---

## Size Modifiers

<!-- RAG_CHUNK: size_modifiers -->

### Weapon Size Damage (%)

| Weapon Type | Small | Medium | Large |
|-------------|-------|--------|-------|
| Fist | 100 | 100 | 100 |
| Dagger | 100 | 75 | 50 |
| 1H Sword | 75 | 100 | 75 |
| 2H Sword | 75 | 75 | 100 |
| 1H Spear | 75 | 75 | 100 |
| 2H Spear | 75 | 75 | 100 |
| 1H Axe | 50 | 75 | 100 |
| 2H Axe | 50 | 75 | 100 |
| Mace | 75 | 100 | 100 |
| 2H Mace | 75 | 100 | 100 |
| Staff | 100 | 100 | 100 |
| Bow | 100 | 100 | 75 |
| Knuckle | 100 | 75 | 50 |
| Musical | 75 | 100 | 75 |
| Whip | 75 | 100 | 50 |
| Book | 100 | 100 | 50 |
| Katar | 75 | 100 | 75 |
| Revolver | 100 | 100 | 100 |
| Rifle | 100 | 100 | 100 |
| Gatling | 100 | 100 | 100 |
| Shotgun | 100 | 100 | 100 |
| Grenade | 100 | 100 | 100 |
| Huuma | 75 | 100 | 100 |
| 2H Staff | 100 | 100 | 100 |

---

## Stat Formulas

<!-- RAG_CHUNK: stat_formulas -->

### Status Points Per Level
```
SP = floor((BaseLv - 1) / 5) + 3
Total SP at Level N = sum(SP for levels 1 to N)
```

### Max Stats
| Mode | Base Cap | After Bonus |
|------|----------|-------------|
| Pre-Renewal | 99 | 99 + Job bonus + Equipment |
| Renewal | 130 | 130 + Job bonus + Equipment |
| 4th Job | 130 | 130 + Trait stats |

### HP/SP Calculation
```
# Renewal HP
MaxHP = BaseHP + (HPGainPerLv * Level) + floor(VIT/5) * floor(BaseLv/4)

# Renewal SP  
MaxSP = BaseSP + (SPGainPerLv * Level) + floor(INT/6) * floor(BaseLv/4)
```

---

*Generated as part of rAthena KB v5 Enhanced Package*
