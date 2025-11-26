# rAthena KB v6.1 - Game Reference (@Commands & Mechanics)

**Version:** 6.1 Validated
**Source:** doc/atcommands.txt, db/re/attr_fix.yml

---

## Quick Navigation

### @Commands
- [Permission Levels](#permission-levels)
- [Player Commands](#player-commands)
- [Item Commands](#item-commands)
- [Admin Commands](#admin-commands)
- [Reload Commands](#reload-commands)

### Game Mechanics
- [Damage Formulas](#damage-formulas)
- [Element Table](#element-table)
- [Size Modifiers](#size-modifiers)
- [Stat Formulas](#stat-formulas)
- [Battle Mechanics](#battle-mechanics)

---

# PART 1: @COMMANDS

## Permission Levels

<!-- RAG_CHUNK: atcmd_permissions -->

| Level | Description |
|-------|-------------|
| 0 | Players |
| 1-59 | Support GM |
| 60-79 | Moderator |
| 80-99 | High GM |
| 99 | Admin |

Configuration: `conf/groups.conf`

---

## Player Commands

<!-- RAG_CHUNK: atcmd_player -->

| Command | Description |
|---------|-------------|
| @commands | List available commands |
| @rates | Show server rates |
| @time | Show server time |
| @exp | Show experience |
| @stats | Show character stats |
| @storage | Open storage |
| @guildstorage | Open guild storage |
| @autotrade | Vend while offline |
| @showexp | Toggle exp display |
| @showzeny | Toggle zeny display |
| @noask | Block trade/party requests |
| @noks | Anti kill-steal mode |

---

## Item Commands

<!-- RAG_CHUNK: atcmd_item -->

| Command | Syntax |
|---------|--------|
| @item | @item <id/name> {amount} |
| @item2 | @item2 <id> <qty> <identify> <refine> <attr> <c1> <c2> <c3> <c4> |
| @itembound | @itembound <id> <amount> <bound_type> |
| @delitem | @delitem <id> <amount> |
| @storeall | Move all to storage |
| @itemreset | Delete all inventory |
| @clearstorage | Clear storage |
| @clearcart | Clear cart |
| @repairall | Repair all items |
| @identify | Identify items |
| @identifyall | Identify all items |

---

## Admin Commands

<!-- RAG_CHUNK: atcmd_admin -->

| Command | Description |
|---------|-------------|
| @kick <name> | Kick player |
| @ban <time> <name> | Ban player |
| @unban <name> | Unban player |
| @mute <time> <name> | Mute player |
| @jail <name> | Jail player |
| @unjail <name> | Unjail player |
| @kill <name> | Kill player |
| @alive | Resurrect self |
| @raise | Resurrect all on map |
| @raisemap | Resurrect all on server |
| @hide | GM invisibility |
| @disguise <id> | Disguise as monster |
| @undisguise | Remove disguise |

### Monster Commands
| Command | Description |
|---------|-------------|
| @monster <name> {amount} | Spawn monster |
| @killmonster | Kill all monsters on map |
| @killmonster2 | Kill without drops |
| @summon <name> {duration} | Summon monster as slave |

### Map Commands
| Command | Description |
|---------|-------------|
| @pvpon / @pvpoff | Toggle PVP |
| @gvgon / @gvgoff | Toggle GVG |
| @skillon / @skilloff | Toggle skills |
| @day / @night | Change time |
| @snow / @fog / @sakura | Weather effects |
| @clearweather | Clear weather |

---

## Reload Commands

<!-- RAG_CHUNK: atcmd_reload -->

| Command | Reloads |
|---------|---------|
| @reloadscript | All NPC scripts |
| @reloaditemdb | item_db.yml |
| @reloadmobdb | mob_db.yml |
| @reloadskilldb | skill_db.yml |
| @reloadquestdb | quest_db.yml |
| @reloadbattleconf | battle/*.conf |
| @reloadatcommand | atcommand.conf |
| @reloadstatusdb | status_db.yml |
| @reloadpcdb | job_db.yml |
| @reloadinstancedb | instance_db.yml |
| @reloadachievementdb | achievement_db.yml |
| @reloadmotd | motd.txt |

---

# PART 2: GAME MECHANICS

## Damage Formulas

<!-- RAG_CHUNK: mech_damage_formulas -->

### Physical Damage (Renewal)
```
Final Damage = (StatusATK + WeaponATK + EquipATK + Mastery)
               × SkillModifier × SizeModifier × ElementModifier
               × RaceModifier × ClassModifier
               / (DEF_Reduction)
```

### Status ATK
```
Melee:  floor(BaseLevel/4) + STR + floor(STR²/100) + floor(DEX/5)
Ranged: floor(BaseLevel/4) + DEX + floor(DEX²/100) + floor(STR/5)
```

### Weapon ATK
```
WeaponATK = WeaponBaseATK + RefineBonus + CardBonus
RefineBonus = Refine × (WeaponLevel × 3 + LevelBonus)
```

### Magic Damage (Renewal)
```
MATK = StatusMATK + WeaponMATK + EquipMATK
Final = MATK × SkillModifier × ElementModifier / (MDEF_Reduction)
StatusMATK = floor(BaseLevel/4) + INT + floor(INT²/2/100)
```

### Critical Hits
```
CritRate = (LUK × 0.3) + CritBonus - TargetLUK/5
CritDamage = NormalDamage × 1.4 + CritDamageBonus
```

---

## Element Table

<!-- RAG_CHUNK: mech_element_table -->

### Damage Multipliers (%) - Level 1

*Source: db/re/attr_fix.yml*

| Attack \ Defense | Neu | Wat | Ear | Fir | Win | Poi | Hol | Drk | Gho | Und |
|------------------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| **Neutral** | 100 | 100 | 100 | 100 | 100 | 100 | 100 | 100 | 90 | 100 |
| **Water** | 100 | 25 | 100 | 150 | 90 | 150 | 100 | 100 | 100 | 100 |
| **Earth** | 100 | 100 | 25 | 90 | 150 | 150 | 100 | 100 | 100 | 100 |
| **Fire** | 100 | 90 | 150 | 25 | 100 | 150 | 100 | 100 | 100 | 125 |
| **Wind** | 100 | 150 | 90 | 100 | 25 | 150 | 100 | 100 | 100 | 100 |
| **Poison** | 100 | 150 | 150 | 150 | 150 | 0 | 75 | 75 | 75 | 75 |
| **Holy** | 100 | 100 | 100 | 100 | 100 | 75 | 0 | 125 | 100 | 125 |
| **Dark** | 100 | 100 | 100 | 100 | 100 | 75 | 125 | 0 | 100 | 0 |
| **Ghost** | 90 | 100 | 100 | 100 | 100 | 75 | 90 | 90 | 125 | 100 |
| **Undead** | 100 | 100 | 100 | 90 | 100 | 75 | 125 | 0 | 100 | 0 |

*0 = immune, <100 = resistant, >100 = weak*

---

## Size Modifiers

<!-- RAG_CHUNK: mech_size_modifiers -->

### Weapon Size Penalty (%)

| Weapon | Small | Medium | Large |
|--------|-------|--------|-------|
| Fist | 100 | 100 | 100 |
| Dagger | 100 | 75 | 50 |
| 1H Sword | 75 | 100 | 75 |
| 2H Sword | 75 | 75 | 100 |
| 1H Spear | 75 | 75 | 100 |
| 2H Spear | 75 | 75 | 100 |
| 1H Axe | 50 | 75 | 100 |
| 2H Axe | 50 | 75 | 100 |
| Mace | 75 | 100 | 100 |
| Staff | 100 | 100 | 100 |
| Bow | 100 | 100 | 75 |
| Knuckle | 100 | 75 | 50 |
| Katar | 75 | 100 | 75 |
| Gun | 100 | 100 | 100 |

---

## Stat Formulas

<!-- RAG_CHUNK: mech_stat_formulas -->

### Status Points per Level
```
Points = floor((BaseLevel - 1) / 5) + 3
Total at Lv99 = 1225 points
Total at Lv175 = 2695 points (Renewal)
```

### HP/SP Calculation
```
MaxHP = BaseHP + (HPGainPerLevel × Level) + floor(VIT/5) × floor(BaseLv/4)
MaxSP = BaseSP + (SPGainPerLevel × Level) + floor(INT/6) × floor(BaseLv/4)
```

### Flee Calculation
```
Flee = BaseLevel + AGI + FleeBonus
HitChance = (Hit - Flee + 80)%  // Capped 5%-100%
```

### ASPD Calculation (Renewal)
```
ASPD = 195 - floor((BaseASPD - ASPDAGI - ASPDBonus) / 10)
ASPDAGI = sqrt((AGI×AGI/2 + DEX×DEX/5) / 4)
```

---

## Battle Mechanics

<!-- RAG_CHUNK: mech_battle -->

### Hit/Miss Calculation
```
HitRate = 80 + Hit - TargetFlee
HitRate is capped at 5% minimum, 100% maximum
Perfect Dodge = LUK / 10 (separate check)
```

### Skill Cast Time (Renewal)
```
TotalCast = VariableCast + FixedCast
VariableCast = BaseCast × (1 - DEX/530 - CastReduction)
FixedCast = BaseFixed × (1 - FixedReduction)
```

### Cooldown & Delay
```
AfterCastDelay = BaseDelay × (1 - DelayReduction)
Cooldown is not affected by reductions
Global delay = 0.3 seconds between most skills
```

---

*rAthena KB v6.1 - Game Reference*
