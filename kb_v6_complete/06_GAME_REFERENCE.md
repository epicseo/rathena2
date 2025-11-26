# rAthena KB v6.1 - Game Reference (@Commands & Mechanics)

**Version:** 6.1 Validated
**Source:** doc/atcommands.txt, db/re/attr_fix.yml

---

# PART 1: @COMMANDS

---

## Quick Navigation

### By Category
- [Player Commands](#player-commands) - @go, @warp, @memo
- [Item Commands](#item-commands) - @item, @storage, @storeall
- [Information](#information-commands) - @who, @where, @time
- [Guild Commands](#guild-commands) - @guild, @breakguild
- [Admin Commands](#admin-commands) - @kick, @ban, @mute
- [Monster Commands](#monster-commands) - @monster, @killmonster
- [Skill Commands](#skill-commands) - @allskill, @skillpoint
- [Stat Commands](#stat-commands) - @str, @agi, @statall

---

## Permission Levels

| Level | Description |
|-------|-------------|
| 0 | Players |
| 1-59 | Support GM |
| 60-79 | Moderator |
| 80-99 | High GM |
| 99 | Admin |

Permission configuration: `conf/groups.conf`

---

## Complete @Command Reference

### @version

@version

---

### @rates

@rates

---

### @time

@time

---

### @uptime

@uptime

---

### @refresh

@refresh

---

### @refreshall

@refreshall

---

### @showexp

@showexp

---

### @showzeny

@showzeny

---

### @showdelay

@showdelay

---

### @noask

@noask

---

### @noks

@noks

---

### @agitstart

@agitstart

---

### @agitend

@agitend

---

### @agitstart2

@agitstart2

---

### @agitend2

@agitend2

---

### @agitstart3

@agitstart3

---

### @agitend3

@agitend3

---

### @pvpon

@pvpon

---

### @pvpoff

@pvpoff

---

### @gvgon

@gvgon

---

### @gvgoff

@gvgoff

---

### @skillon

@skillon

---

### @skilloff

@skilloff

---

### @allowks

@allowks

---

### @day

@day

---

### @night

@night

---

### @snow

@snow

---

### @clouds

@clouds

---

### @clouds2

@clouds2

---

### @fog

@fog

---

### @fireworks

@fireworks

---

### @sakura

@sakura

---

### @leaves

@leaves

---

### @clearweather

@clearweather

---

### @gat

@gat

---

### @showrate

@showrate

---

### @whereis

@whereis

---

### @commands

@commands

---

### @charcommands

@charcommands

---

### @exp

@exp

---

### @stats

@stats

---

### @itemlist

@itemlist

---

### @users

@users

---

### @jailtime

@jailtime

---

### @storage

@storage

---

### @mail

@mail

---

### @auction

@auction

---

### @identify

@identify

---

### @identifyall

@identifyall

---

### @autotrade

@autotrade

---

### @item

@item <item name/ID>{:<item name/ID>:...} {<amount>}

---

### @itembound

@itembound <item name/ID>{:<item name/ID>:...} <amount> <bound type>

---

### @repairall

@repairall

---

### @storeall

@storeall

---

### @itemreset

@itemreset

---

### @clearstorage

@clearstorage

---

### @cleargstorage

@cleargstorage

---

### @clearcart

@clearcart

---

### @cleanarea

@cleanarea

---

### @cleanmap

@cleanmap

---

### @save

@save

---

### @load

@load

---

### @recallall

@recallall

---

### @killer

@killer

---

### @killable

@killable

---

### @allskill

@allskill

---

### @resetstat

@resetstat

---

### @resetskill

@resetskill

---

### @reset

@reset

---

### @feelreset

@feelreset

---

### @hatereset

@hatereset

---

### @mount2

@mount2

---

### @hairstyle

@hairstyle <default: 0-27>

---

### @haircolor

@haircolor <default: 0-8>

---

### @dye

@dye <default: 0-4>

---

### @bodystyle

@bodystyle <default: 0-1>

---

### @changedress

@changedress

---

### @accept

@accept

---

### @reject

@reject

---

### @leave

@leave

---

### @alive

@alive

---

### @raisemap

@raisemap

---

### @raise

@raise

---

### @undisguise

@undisguise

---

### @undisguiseall

@undisguiseall

---

### @monsterignore

@monsterignore

---

### @hide

@hide

---

### @limitedsale

@limitedsale

---

### @enchantgradeui

@enchantgradeui

---

### @resetcooltime

@resetcooltime

---

### @changesex

@changesex

---

### @changecharsex

@changecharsex

---

### @refineui

@refineui

---

### @stylist

@stylist

---

### @gmotd

@gmotd

---

### @killmonster

@killmonster

---

### @killmonster2

@killmonster2

---

### @kill

@kill

---

### @doommap

@doommap

---

### @doom

@doom

---

### @kickall

@kickall

---

### @mapexit

@mapexit

---

### @reloadatcommand

@reloadatcommand

---

### @reloadbattleconf

@reloadbattleconf

---

### @reloadinstancedb

@reloadinstancedb

---

### @reloaditemdb

@reloaditemdb

---

### @reloadmobdb

@reloadmobdb

---

### @reloadmotd

@reloadmotd

---

### @reloadmsgconf

@reloadmsgconf

---

### @reloadpcdb

@reloadpcdb

---

### @reloadquestdb

@reloadquestdb

---

### @reloadscript

@reloadscript

---

### @reloadskilldb

@reloadskilldb

---

### @reloadstatusdb

@reloadstatusdb

---

### @reloadachievementdb

@reloadachievementdb

---

### @reloadattendancedb

@reloadattendancedb

---

### @reloadbarterdb

@reloadbarterdb

---

### @partyoption

@partyoption <pickup share: yes/no> <item distribution: yes/no>

---

### @breakguild

@breakguild

---

### @guildstorage

@guildstorage

---

### @undisguiseguild

@undisguiseguild

---

### @hatch

@hatch

---

### @petrename

@petrename

---

### @homevolution

@homevolution

---

### @hominfo

@hominfo

---

### @homstats

@homstats

---

### @homshuffle

@homshuffle

---


---

# PART 2: GAME MECHANICS

## Quick Navigation

- [Damage Formulas](#damage-formulas)
- [Element Table](#element-table)
- [Size Modifiers](#size-modifiers)
- [Stat Formulas](#stat-formulas)
- [Battle Mechanics](#battle-mechanics)

---

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

### Defense Reduction
```
Physical: FinalDEF = EquipDEF × (1 - HardDEFRate) + SoftDEF
MDEF: Same formula with MDEF values
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

*Values below 100 = resistance, above 100 = weakness, 0 = immune*

### Element Levels
Monsters have element levels 1-4 that modify resistances:
- Level 1: Base values
- Level 2: +5% per weakness, -5% per resistance
- Level 3: +10% per weakness, -10% per resistance
- Level 4: +15% per weakness, -15% per resistance

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
| Musical | 75 | 100 | 75 |
| Whip | 75 | 100 | 50 |
| Book | 100 | 100 | 50 |
| Katar | 75 | 100 | 75 |
| Gun | 100 | 100 | 100 |
| Huuma | 75 | 100 | 100 |

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
BaseASPD depends on job and weapon type
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

### Knockback
```
Knockback ignores Boss protocol flag
NoKnockback bonus prevents knockback
Direction is from attacker to target
```

---

*Generated as part of rAthena KB v6 Complete*
