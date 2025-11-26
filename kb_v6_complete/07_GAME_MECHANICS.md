# rAthena KB v6 - Game Mechanics Reference

**Version:** 6.0 Complete
**Generated:** 2025-11-26

---

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

### Damage Multipliers (%)

| Attack \ Defense | Neu | Wat | Ear | Fir | Win | Poi | Hol | Drk | Gho | Und |
|------------------|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| **Neutral** | 100 | 100 | 100 | 100 | 100 | 100 | 100 | 100 | 25 | 100 |
| **Water** | 100 | 25 | 100 | 150 | 90 | 100 | 100 | 100 | 100 | 100 |
| **Earth** | 100 | 100 | 100 | 90 | 150 | 100 | 100 | 100 | 100 | 100 |
| **Fire** | 100 | 90 | 150 | 25 | 100 | 100 | 100 | 100 | 100 | 125 |
| **Wind** | 100 | 150 | 90 | 100 | 25 | 100 | 100 | 100 | 100 | 100 |
| **Poison** | 100 | 100 | 100 | 100 | 100 | 0 | 100 | 50 | 100 | -25 |
| **Holy** | 100 | 75 | 75 | 75 | 75 | 75 | 0 | 125 | 75 | 150 |
| **Dark** | 100 | 100 | 100 | 100 | 100 | 50 | 125 | 0 | 75 | -25 |
| **Ghost** | 25 | 100 | 100 | 100 | 100 | 100 | 100 | 100 | 125 | 100 |
| **Undead** | 100 | 100 | 100 | 125 | 100 | -25 | 150 | -25 | 100 | 0 |

*Values below 100 = resistance, above 100 = weakness, negative = heal*

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
