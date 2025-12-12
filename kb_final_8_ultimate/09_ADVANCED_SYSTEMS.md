# rAthena Advanced Systems Reference v1.0

**Version:** 1.0 - Gap Fill Edition
**Coverage:** 4th Job Classes, Attendance System, Stylist System
**Last Updated:** 2025-12-12
**Source:** Extracted from official rAthena repository (github.com/rathena/rathena)

---

<!-- RAG_CHUNK: 09_overview -->
## Overview

This document fills the remaining knowledge gaps for a complete rAthena scripting KB:
- **Part 1:** 4th Job Classes - Complete skill trees, stats, and inheritance
- **Part 2:** Attendance System - Daily login rewards configuration
- **Part 3:** Stylist System - Character appearance customization

---

# ═══════════════════════════════════════════════════════════════
# PART 1: 4TH JOB CLASSES COMPLETE REFERENCE
# ═══════════════════════════════════════════════════════════════

<!-- RAG_CHUNK: 09_4th_jobs_overview -->
## 4th Job Classes Overview

4th Job Classes are the latest job advancement in rAthena, requiring 3rd job completion. They introduce new stats (Pow, Sta, Wis, Spl, Crt, Con) alongside traditional stats.

### Complete 4th Job List

| 4th Job | Evolution From | Base Tree | Key Skills |
|---------|----------------|-----------|------------|
| Dragon Knight | Rune Knight | Swordman 2-1 | DK_SERVANTWEAPON, DK_DRAGONIC_BREATH |
| Imperial Guard | Royal Guard | Swordman 2-2 | IG_GUARD_STANCE, IG_JUDGEMENT_CROSS |
| Meister | Mechanic | Merchant 2-1 (Blacksmith) | MT_ABR_M, MT_SUMMON_ABR_INFINITY |
| Biolo | Genetic | Merchant 2-2 (Alchemist) | BO_BIONIC_PHARMACY, BO_HELLTREE |
| Shadow Cross | Guillotine Cross | Thief 2-1 (Assassin) | SHC_SHADOW_EXCEED, SHC_FATAL_SHADOW_CROW |
| Abyss Chaser | Shadow Chaser | Thief 2-2 (Rogue) | ABC_ABYSS_SLAYER, ABC_ABYSS_STRIKE |
| Arch Mage | Warlock | Mage 2-1 (Wizard) | AG_ASTRAL_STRIKE, AG_CLIMAX |
| Elemental Master | Sorcerer | Mage 2-2 (Sage) | EM_ELEMENTAL_BUSTER, EM_PSYCHIC_STREAM |
| Cardinal | Arch Bishop | Acolyte 2-1 (Priest) | CD_PNEUMATICUS_PROCELLA, CD_EFFLIGO |
| Inquisitor | Sura | Acolyte 2-2 (Monk) | IQ_MASSIVE_F_BLASTER, IQ_BLAZING_FLAME_BLAST |
| Windhawk | Ranger | Archer 2-1 (Hunter) | WH_CALAMITYGALE, WH_GALESTORM |
| Troubadour | Minstrel | Archer 2-2 (Bard) | TR_MYSTIC_SYMPHONY, TR_KVASIR_SONATA |
| Trouvere | Wanderer | Archer 2-2 (Dancer) | TR_MYSTIC_SYMPHONY, TR_KVASIR_SONATA |
| Sky Emperor | Star Emperor | Taekwon (Star Gladiator) | SKE_ALL_IN_THE_SKY, SKE_SKY_SUN |
| Soul Ascetic | Soul Reaper | Taekwon (Soul Linker) | SOA_SOUL_OF_HEAVEN_AND_EARTH |
| Night Watch | Rebellion | Gunslinger | NW_MISSION_BOMBARD, NW_MIDNIGHT_FALLEN |
| Shinkiro | Kagerou | Ninja (Male) | SS_ANKOKURYUUAKUMU, SS_HITOUAKUMU |
| Shiranui | Oboro | Ninja (Female) | SS_ANKOKURYUUAKUMU, SS_HITOUAKUMU |
| Spirit Handler | Summoner | Doram | SH_COMMUNE_WITH_CHUL_HO |
| Hyper Novice | Super Novice E | Novice | HN_BREAKINGLIMIT, HN_RULEBREAK |

---

<!-- RAG_CHUNK: 09_4th_jobs_stats -->
## 4th Job Class Stats

### Dragon Knight
```yaml
Jobs: Dragon_Knight, Dragon_Knight2
MaxWeight: 45000
HpFactor: 68
HpIncrease: 5828
SpFactor: 7
SpIncrease: 14
# Inherits from: Novice -> Swordman -> Knight -> Lord_Knight -> Rune_Knight
# Focus: Pow, Str, Crt (Physical DPS)
```

### Imperial Guard
```yaml
Jobs: Imperial_Guard, Imperial_Guard2
MaxWeight: 45000
HpFactor: 94
HpIncrease: 2767
SpFactor: 3
SpIncrease: 504
# Inherits from: Novice -> Swordman -> Crusader -> Paladin -> Royal_Guard
# Focus: Sta, Wis, Pow (Tank/Support)
```

### Meister
```yaml
Jobs: Meister, Meister2
MaxWeight: 48000
HpFactor: 76
HpIncrease: 4073
SpFactor: 3
SpIncrease: 552
# Inherits from: Novice -> Merchant -> Blacksmith -> Whitesmith -> Mechanic
# Focus: Pow, Sta, Con (Physical/Machine)
```

### Biolo
```yaml
Jobs: Biolo
MaxWeight: 42000
HpFactor: 104
HpIncrease: 22
SpFactor: 0
SpIncrease: 890
# Inherits from: Novice -> Merchant -> Alchemist -> Creator -> Genetic
# Focus: Crt, Pow, Int (Hybrid DPS)
```

### Shadow Cross
```yaml
Jobs: Shadow_Cross
MaxWeight: 42000
HpFactor: 64
HpIncrease: 5398
SpFactor: 7
SpIncrease: 4
# Inherits from: Novice -> Thief -> Assassin -> Assassin_Cross -> Guillotine_Cross
# Focus: Pow, Crt, Con (Melee Assassin)
```

### Abyss Chaser
```yaml
Jobs: Abyss_Chaser
MaxWeight: 42000
HpFactor: 64
HpIncrease: 5503
SpFactor: 7
SpIncrease: 11
# Inherits from: Novice -> Thief -> Rogue -> Stalker -> Shadow_Chaser
# Focus: Pow, Spl, Crt (Hybrid)
```

### Arch Mage
```yaml
Jobs: Arch_Mage
MaxWeight: 40000
HpFactor: 91
HpIncrease: 1075
SpFactor: 6
SpIncrease: 438
# Inherits from: Novice -> Mage -> Wizard -> High_Wizard -> Warlock
# Focus: Spl, Int, Wis (Magic DPS)
```

### Elemental Master
```yaml
Jobs: Elemental_Master
MaxWeight: 40000
HpFactor: 104
HpIncrease: 40
SpFactor: 9
SpIncrease: 61
# Inherits from: Novice -> Mage -> Sage -> Professor -> Sorcerer
# Focus: Spl, Int (Elemental Summoner)
```

### Cardinal
```yaml
Jobs: Cardinal
MaxWeight: 40000
HpFactor: 94
HpIncrease: 1047
SpFactor: 5
SpIncrease: 530
# Inherits from: Novice -> Acolyte -> Priest -> High_Priest -> Arch_Bishop
# Focus: Spl, Wis (Support/Holy DPS)
```

### Inquisitor
```yaml
Jobs: Inquisitor
MaxWeight: 42000
HpFactor: 90
HpIncrease: 2633
SpFactor: 7
SpIncrease: 33
# Inherits from: Novice -> Acolyte -> Monk -> Champion -> Sura
# Focus: Pow, Sta, Wis (Melee/Holy)
```

### Windhawk
```yaml
Jobs: Windhawk, Windhawk2
MaxWeight: 42000
HpFactor: 93
HpIncrease: 1121
SpFactor: 6
SpIncrease: 112
# Inherits from: Novice -> Archer -> Hunter -> Sniper -> Ranger
# Focus: Pow, Con, Crt (Ranged DPS)
```

### Troubadour / Trouvere
```yaml
Jobs: Troubadour (Male), Trouvere (Female)
MaxWeight: 42000
HpFactor: 95
HpIncrease: 1119
SpFactor: 8
SpIncrease: 3
# Inherits from: Novice -> Archer -> Bard/Dancer -> Clown/Gypsy -> Minstrel/Wanderer
# Focus: Spl, Con (Support/Performance)
```

### Sky Emperor
```yaml
Jobs: Sky_Emperor, Sky_Emperor2
MaxWeight: 42000
HpFactor: 72
HpIncrease: 6050
SpFactor: 3
SpIncrease: 469
# Inherits from: Novice -> Taekwon -> Star_Gladiator -> Star_Emperor
# Focus: Pow, Crt, Sta (Melee Kicks)
```

### Soul Ascetic
```yaml
Jobs: Soul_Ascetic
MaxWeight: 42000
HpFactor: 94
HpIncrease: 1058
SpFactor: 6
SpIncrease: 400
# Inherits from: Novice -> Taekwon -> Soul_Linker -> Soul_Reaper
# Focus: Spl, Wis, Con (Soul Magic)
```

### Night Watch
```yaml
Jobs: Night_Watch
MaxWeight: 48000
HpFactor: 66
HpIncrease: 5603
SpFactor: 9
SpIncrease: 16
# Inherits from: Novice -> Gunslinger -> Rebellion
# Focus: Pow, Con, Crt (Guns/Grenades)
```

### Shinkiro / Shiranui
```yaml
Jobs: Shinkiro (Male), Shiranui (Female)
MaxWeight: 45000
HpFactor: 85
HpIncrease: 4496
SpFactor: 3
SpIncrease: 474
# Inherits from: Novice -> Ninja -> Kagerou/Oboro
# Focus: Pow (Shinkiro) / Spl (Shiranui)
```

### Spirit Handler
```yaml
Jobs: Spirit_Handler
MaxWeight: 42000
HpFactor: 16
HpIncrease: 11979
SpFactor: 7
SpIncrease: 84
# Inherits from: Summoner (Doram)
# Focus: Multiple creature companions
```

### Hyper Novice
```yaml
Jobs: Hyper_Novice
MaxWeight: 40000
HpFactor: 38
HpIncrease: 5584
SpFactor: 6
SpIncrease: 40
# Inherits from: Novice -> Supernovice -> Super_Novice_E
# Focus: Pow, Spl (Hybrid)
```

---

<!-- RAG_CHUNK: 09_dragon_knight_skills -->
## Dragon Knight Skill Tree

```yaml
Job: Dragon_Knight
Inherit: [Novice, Swordman, Knight, Lord_Knight, Rune_Knight, Rune_Knight_T]

Skills:
  # Servant Weapon Line
  - DK_SERVANTWEAPON: {MaxLevel: 5}
  - DK_SERVANT_W_SIGN: {MaxLevel: 5, Requires: DK_SERVANTWEAPON Lv3}
  - DK_SERVANT_W_PHANTOM: {MaxLevel: 5, Requires: [DK_SERVANTWEAPON Lv5, DK_SERVANT_W_SIGN Lv5]}
  - DK_SERVANT_W_DEMOL: {MaxLevel: 5, Requires: DK_SERVANT_W_PHANTOM Lv5}

  # Pierce Line
  - DK_CHARGINGPIERCE: {MaxLevel: 10, Requires: RK_HUNDREDSPEAR Lv5}

  # Two-Hand Defense Line
  - DK_TWOHANDDEF: {MaxLevel: 10}
  - DK_HACKANDSLASHER: {MaxLevel: 10, Requires: DK_TWOHANDDEF Lv5}
  - DK_STORMSLASH: {MaxLevel: 5, Requires: [DK_HACKANDSLASHER Lv5, DK_TWOHANDDEF Lv10]}

  # Dragon Line
  - DK_DRAGONIC_BREATH: {MaxLevel: 10, Requires: [RK_DRAGONBREATH Lv10, RK_DRAGONBREATH_WATER Lv10]}
  - DK_DRAGONIC_AURA: {MaxLevel: 10, Requires: [DK_CHARGINGPIERCE Lv10, RK_DRAGONBREATH Lv10, RK_DRAGONBREATH_WATER Lv10]}

  # Ultimate Skills
  - DK_MADNESS_CRUSHER: {MaxLevel: 5, Requires: [DK_CHARGINGPIERCE Lv5, DK_HACKANDSLASHER Lv10]}
  - DK_VIGOR: {MaxLevel: 10, Requires: [DK_SERVANT_W_DEMOL Lv3, DK_STORMSLASH Lv5]}
  - DK_DRAGONIC_PIERCE: {MaxLevel: 5, Requires: DK_HACKANDSLASHER Lv7}
```

---

<!-- RAG_CHUNK: 09_imperial_guard_skills -->
## Imperial Guard Skill Tree

```yaml
Job: Imperial_Guard
Inherit: [Novice, Swordman, Crusader, Paladin, Royal_Guard, Royal_Guard_T]

Skills:
  # Shield Mastery Line
  - IG_SHIELD_MASTERY: {MaxLevel: 10}
  - IG_GUARD_STANCE: {MaxLevel: 5, Requires: IG_SHIELD_MASTERY Lv3}
  - IG_GUARDIAN_SHIELD: {MaxLevel: 5, Requires: IG_GUARD_STANCE Lv2}
  - IG_REBOUND_SHIELD: {MaxLevel: 5, Requires: IG_GUARD_STANCE Lv4}
  - IG_ULTIMATE_SACRIFICE: {MaxLevel: 5, Requires: [IG_GUARDIAN_SHIELD Lv3, IG_REBOUND_SHIELD Lv3]}

  # Spear/Sword Line
  - IG_SPEAR_SWORD_M: {MaxLevel: 10}
  - IG_ATTACK_STANCE: {MaxLevel: 5, Requires: IG_SPEAR_SWORD_M Lv3}
  - IG_OVERSLASH: {MaxLevel: 10, Requires: IG_ATTACK_STANCE Lv3}
  - IG_GRAND_JUDGEMENT: {MaxLevel: 10, Requires: [IG_OVERSLASH Lv5, IG_SPEAR_SWORD_M Lv5]}
  - IG_IMPERIAL_CROSS: {MaxLevel: 5, Requires: IG_OVERSLASH Lv5}

  # Holy Line
  - IG_CROSS_RAIN: {MaxLevel: 10, Requires: IG_SHIELD_MASTERY Lv1}
  - IG_HOLY_SHIELD: {MaxLevel: 5, Requires: [IG_CROSS_RAIN Lv3, IG_SHIELD_MASTERY Lv5]}
  - IG_JUDGEMENT_CROSS: {MaxLevel: 10, Requires: [IG_CROSS_RAIN Lv5, IG_HOLY_SHIELD Lv3]}

  # Ranged
  - IG_SHIELD_SHOOTING: {MaxLevel: 5, Requires: [IG_ATTACK_STANCE Lv2, IG_SHIELD_MASTERY Lv5]}
  - IG_RADIANT_SPEAR: {MaxLevel: 10, Requires: [IG_OVERSLASH Lv3, IG_SHIELD_SHOOTING Lv3]}
  - IG_IMPERIAL_PRESSURE: {MaxLevel: 5, Requires: [IG_SPEAR_SWORD_M Lv7, IG_GUARD_STANCE Lv3]}
```

---

<!-- RAG_CHUNK: 09_arch_mage_skills -->
## Arch Mage Skill Tree

```yaml
Job: Arch_Mage
Inherit: [Novice, Mage, Wizard, High_Wizard, Warlock, Warlock_T]

Skills:
  # Staff Mastery
  - AG_TWOHANDSTAFF: {MaxLevel: 10}

  # Soul Line
  - AG_SOUL_VC_STRIKE: {MaxLevel: 5, Requires: [AG_TWOHANDSTAFF Lv3, WL_SOULEXPANSION Lv5]}
  - AG_MYSTERY_ILLUSION: {MaxLevel: 5, Requires: [AG_SOUL_VC_STRIKE Lv3, WL_HELLINFERNO Lv3]}
  - AG_DEADLY_PROJECTION: {MaxLevel: 5, Requires: AG_MYSTERY_ILLUSION Lv3}

  # Earth Line
  - AG_STRANTUM_TREMOR: {MaxLevel: 5, Requires: WL_SIENNAEXECRATE Lv3}
  - AG_VIOLENT_QUAKE: {MaxLevel: 5, Requires: AG_STRANTUM_TREMOR Lv3}
  - AG_ROCK_DOWN: {MaxLevel: 5, Requires: AG_STRANTUM_TREMOR Lv1}

  # Wind Line
  - AG_TORNADO_STORM: {MaxLevel: 5, Requires: WL_CHAINLIGHTNING Lv3}
  - AG_DESTRUCTIVE_HURRICANE: {MaxLevel: 5, Requires: AG_TORNADO_STORM Lv3}
  - AG_STORM_CANNON: {MaxLevel: 5, Requires: AG_TORNADO_STORM Lv1}

  # Fire Line
  - AG_FLORAL_FLARE_ROAD: {MaxLevel: 5, Requires: WL_CRIMSONROCK Lv3}
  - AG_ALL_BLOOM: {MaxLevel: 5, Requires: AG_FLORAL_FLARE_ROAD Lv3}
  - AG_CRIMSON_ARROW: {MaxLevel: 5, Requires: AG_FLORAL_FLARE_ROAD Lv1}

  # Ice Line
  - AG_RAIN_OF_CRYSTAL: {MaxLevel: 5, Requires: WL_FROSTMISTY Lv3}
  - AG_CRYSTAL_IMPACT: {MaxLevel: 5, Requires: AG_RAIN_OF_CRYSTAL Lv3}
  - AG_FROZEN_SLASH: {MaxLevel: 5, Requires: AG_RAIN_OF_CRYSTAL Lv1}

  # Ultimate
  - AG_ASTRAL_STRIKE: {MaxLevel: 10, Requires: [AG_DEADLY_PROJECTION Lv3, AG_MYSTERY_ILLUSION Lv3, WL_COMET Lv5]}
  - AG_CLIMAX: {MaxLevel: 5, Requires: [AG_TWOHANDSTAFF Lv3, WL_TETRAVORTEX Lv5]}
  - AG_ENERGY_CONVERSION: {MaxLevel: 5, Requires: [WL_RECOGNIZEDSPELL Lv2, AG_CLIMAX Lv1]}
```

---

<!-- RAG_CHUNK: 09_cardinal_skills -->
## Cardinal Skill Tree

```yaml
Job: Cardinal
Inherit: [Novice, Acolyte, Priest, High_Priest, Arch_Bishop, Arch_Bishop_T]

Skills:
  # Heal Line
  - CD_DILECTIO_HEAL: {MaxLevel: 5, Requires: [AB_CHEAL Lv3, AB_HIGHNESSHEAL Lv3]}
  - CD_MEDIALE_VOTUM: {MaxLevel: 5, Requires: CD_DILECTIO_HEAL Lv3}
  - CD_REPARATIO: {MaxLevel: 5, Requires: CD_MEDIALE_VOTUM Lv3}

  # Buff Line
  - CD_RELIGIO: {MaxLevel: 5, Requires: [AB_CLEMENTIA Lv3, CD_DILECTIO_HEAL Lv2]}
  - CD_BENEDICTUM: {MaxLevel: 5, Requires: [AB_CANTO Lv3, CD_DILECTIO_HEAL Lv2]}
  - CD_ARGUTUS_VITA: {MaxLevel: 5, Requires: [CD_MEDIALE_VOTUM Lv3, CD_REPARATIO Lv3]}
  - CD_ARGUTUS_TELUM: {MaxLevel: 5, Requires: [CD_MEDIALE_VOTUM Lv3, CD_REPARATIO Lv3]}
  - CD_PRESENS_ACIES: {MaxLevel: 5, Requires: [CD_MEDIALE_VOTUM Lv3, CD_REPARATIO Lv3]}
  - CD_COMPETENTIA: {MaxLevel: 5, Requires: [CD_ARGUTUS_TELUM Lv2, CD_ARGUTUS_VITA Lv2, CD_PRESENS_ACIES Lv2]}

  # Weapon Mastery
  - CD_MACE_BOOK_M: {MaxLevel: 10}
  - CD_FIDUS_ANIMUS: {MaxLevel: 10}

  # Holy Attack Line
  - CD_PETITIO: {MaxLevel: 10, Requires: [AB_DUPLELIGHT Lv10, CD_MACE_BOOK_M Lv5]}
  - CD_FRAMEN: {MaxLevel: 5, Requires: [AB_JUDEX Lv10, CD_FIDUS_ANIMUS Lv5]}
  - CD_ARBITRIUM: {MaxLevel: 10, Requires: [AB_ADORAMUS Lv5, CD_FRAMEN Lv3]}
  - CD_EFFLIGO: {MaxLevel: 10, Requires: [AB_ORATIO Lv5, CD_PETITIO Lv10]}
  - CD_PNEUMATICUS_PROCELLA: {MaxLevel: 10, Requires: [CD_ARBITRIUM Lv10, CD_FRAMEN Lv5]}
  - CD_DIVINUS_FLOS: {MaxLevel: 5}
```

---

<!-- RAG_CHUNK: 09_windhawk_skills -->
## Windhawk Skill Tree

```yaml
Job: Windhawk
Inherit: [Novice, Archer, Hunter, Sniper, Ranger, Ranger_T]

Skills:
  # Nature Line
  - WH_NATUREFRIENDLY: {MaxLevel: 5}
  - WH_WIND_SIGN: {MaxLevel: 5, Requires: WH_NATUREFRIENDLY Lv5}
  - WH_WILD_WALK: {MaxLevel: 5, Requires: [WH_NATUREFRIENDLY Lv3, WH_HAWKRUSH Lv3]}

  # Hawk Line
  - WH_HAWK_M: {MaxLevel: 1, Requires: HT_STEELCROW Lv1}
  - WH_HAWKRUSH: {MaxLevel: 5, Requires: WH_HAWK_M Lv1}
  - WH_HAWKBOOMERANG: {MaxLevel: 5, Requires: WH_HAWKRUSH Lv5}

  # Bolt Line
  - WH_CRESCIVE_BOLT: {MaxLevel: 10, Requires: RA_AIMEDBOLT Lv5}
  - WH_GALESTORM: {MaxLevel: 10, Requires: WH_CRESCIVE_BOLT Lv3}
  - WH_CALAMITYGALE: {MaxLevel: 1, Requires: [WH_GALESTORM Lv5, WH_WIND_SIGN Lv5]}

  # Trap Line
  - WH_ADVANCED_TRAP: {MaxLevel: 5, Requires: RA_RESEARCHTRAP Lv3}
  - WH_DEEPBLINDTRAP: {MaxLevel: 5, Requires: WH_ADVANCED_TRAP Lv3}
  - WH_SOLIDTRAP: {MaxLevel: 5, Requires: WH_ADVANCED_TRAP Lv3}
  - WH_SWIFTTRAP: {MaxLevel: 5, Requires: WH_DEEPBLINDTRAP Lv1}
  - WH_FLAMETRAP: {MaxLevel: 5, Requires: WH_SOLIDTRAP Lv1}
```

---

<!-- RAG_CHUNK: 09_shadow_cross_skills -->
## Shadow Cross Skill Tree

```yaml
Job: Shadow_Cross
Inherit: [Novice, Thief, Assassin, Assassin_Cross, Guillotine_Cross, Guillotine_Cross_T]

Skills:
  # Shadow Sense Base
  - SHC_SHADOW_SENSE: {MaxLevel: 10}

  # Knife Line
  - SHC_DANCING_KNIFE: {MaxLevel: 5, Requires: SHC_SHADOW_SENSE Lv3}
  - SHC_ETERNAL_SLASH: {MaxLevel: 5, Requires: [GC_WEAPONBLOCKING Lv3, SHC_DANCING_KNIFE Lv3, SHC_SHADOW_SENSE Lv5]}
  - SHC_SHADOW_STAB: {MaxLevel: 5, Requires: [GC_CLOAKINGEXCEED Lv5, SHC_DANCING_KNIFE Lv5, SHC_ETERNAL_SLASH Lv3, SHC_SHADOW_SENSE Lv5]}
  - SHC_CROSS_SLASH: {MaxLevel: 5, Requires: [GC_WEAPONBLOCKING Lv3, SHC_DANCING_KNIFE Lv3]}

  # Impact Line
  - SHC_SAVAGE_IMPACT: {MaxLevel: 10, Requires: [GC_CROSSIMPACT Lv5, SHC_SHADOW_SENSE Lv3]}
  - SHC_IMPACT_CRATER: {MaxLevel: 5, Requires: [GC_ROLLINGCUTTER Lv5, GC_WEAPONBLOCKING Lv3, SHC_SAVAGE_IMPACT Lv5, SHC_SHADOW_SENSE Lv5]}

  # Poison Line
  - SHC_ENCHANTING_SHADOW: {MaxLevel: 5, Requires: [GC_POISONINGWEAPON Lv5, SHC_SHADOW_SENSE Lv3]}
  - SHC_POTENT_VENOM: {MaxLevel: 10, Requires: [SHC_ENCHANTING_SHADOW Lv3, SHC_SHADOW_SENSE Lv5]}

  # Ultimate
  - SHC_SHADOW_EXCEED: {MaxLevel: 10, Requires: [SHC_ENCHANTING_SHADOW Lv5, SHC_POTENT_VENOM Lv3, SHC_SHADOW_SENSE Lv7]}
  - SHC_FATAL_SHADOW_CROW: {MaxLevel: 10, Requires: [SHC_IMPACT_CRATER Lv5, SHC_SHADOW_STAB Lv5]}
```

---

<!-- RAG_CHUNK: 09_meister_skills -->
## Meister Skill Tree

```yaml
Job: Meister
Inherit: [Novice, Merchant, Blacksmith, Whitesmith, Mechanic, Mechanic_T]

Skills:
  # Axe Line
  - MT_TWOAXEDEF: {MaxLevel: 10}
  - MT_AXE_STOMP: {MaxLevel: 5, Requires: MT_TWOAXEDEF Lv5}
  - MT_RUSH_QUAKE: {MaxLevel: 10, Requires: MT_AXE_STOMP Lv5}
  - MT_MIGHTY_SMASH: {MaxLevel: 10, Requires: MT_AXE_STOMP Lv3}
  - MT_RUSH_STRIKE: {MaxLevel: 5, Requires: MT_RUSH_QUAKE Lv5}
  - MT_POWERFUL_SWING: {MaxLevel: 5, Requires: MT_RUSH_STRIKE Lv3}

  # Machine Line
  - MT_M_MACHINE: {MaxLevel: 5}
  - MT_A_MACHINE: {MaxLevel: 5, Requires: [MT_AXE_STOMP Lv3, MT_M_MACHINE Lv3]}
  - MT_D_MACHINE: {MaxLevel: 5, Requires: MT_M_MACHINE Lv1}

  # ABR Summon Line
  - MT_ABR_M: {MaxLevel: 10, Requires: MT_M_MACHINE Lv1}
  - MT_SUMMON_ABR_BATTLE_WARIOR: {MaxLevel: 4, Requires: MT_ABR_M Lv1}
  - MT_SUMMON_ABR_DUAL_CANNON: {MaxLevel: 4, Requires: [MT_ABR_M Lv3, MT_SUMMON_ABR_BATTLE_WARIOR Lv2]}
  - MT_SUMMON_ABR_MOTHER_NET: {MaxLevel: 4, Requires: [MT_ABR_M Lv5, MT_SUMMON_ABR_BATTLE_WARIOR Lv3, MT_SUMMON_ABR_DUAL_CANNON Lv3]}
  - MT_SUMMON_ABR_INFINITY: {MaxLevel: 4, Requires: [MT_ABR_M Lv10, All other ABR summons Lv4]}

  # Laser Line
  - MT_SPARK_BLASTER: {MaxLevel: 10, Requires: MT_M_MACHINE Lv1}
  - MT_TRIPLE_LASER: {MaxLevel: 5, Requires: MT_SPARK_BLASTER Lv5}
  - MT_ENERGY_CANNONADE: {MaxLevel: 5, Requires: MT_TRIPLE_LASER Lv3}
```

---

<!-- RAG_CHUNK: 09_inquisitor_skills -->
## Inquisitor Skill Tree

```yaml
Job: Inquisitor
Inherit: [Novice, Acolyte, Monk, Champion, Sura, Sura_T]

Skills:
  # Faith Line
  - IQ_WILL_OF_FAITH: {MaxLevel: 10}
  - IQ_POWERFUL_FAITH: {MaxLevel: 5, Requires: IQ_WILL_OF_FAITH Lv1}
  - IQ_FIRM_FAITH: {MaxLevel: 5, Requires: IQ_WILL_OF_FAITH Lv1}
  - IQ_SINCERE_FAITH: {MaxLevel: 5, Requires: IQ_WILL_OF_FAITH Lv1}

  # Holy Oil Line
  - IQ_OLEUM_SANCTUM: {MaxLevel: 5, Requires: [AL_HOLYWATER Lv1, IQ_WILL_OF_FAITH Lv3]}
  - IQ_EXPOSION_BLASTER: {MaxLevel: 5, Requires: IQ_OLEUM_SANCTUM Lv1}
  - IQ_MASSIVE_F_BLASTER: {MaxLevel: 10, Requires: [IQ_EXPOSION_BLASTER Lv3, IQ_OLEUM_SANCTUM Lv3, IQ_WILL_OF_FAITH Lv5]}
  - IQ_BLAZING_FLAME_BLAST: {MaxLevel: 5, Requires: IQ_MASSIVE_F_BLASTER Lv7}

  # Brand/Judge Line
  - IQ_FIRST_BRAND: {MaxLevel: 5, Requires: IQ_WILL_OF_FAITH Lv2}
  - IQ_FIRST_FAITH_POWER: {MaxLevel: 5, Requires: [IQ_FIRST_BRAND Lv1, IQ_WILL_OF_FAITH Lv3]}
  - IQ_JUDGE: {MaxLevel: 5, Requires: IQ_FIRST_FAITH_POWER Lv1}
  - IQ_SECOND_FAITH: {MaxLevel: 5, Requires: IQ_FIRST_FAITH_POWER Lv1}
  - IQ_SECOND_JUDGEMENT: {MaxLevel: 5, Requires: IQ_JUDGE Lv1}
  - IQ_THIRD_PUNISH: {MaxLevel: 5, Requires: IQ_SECOND_FAITH Lv2}
  - IQ_THIRD_CONSECRATION: {MaxLevel: 5, Requires: IQ_SECOND_JUDGEMENT Lv2}

  # Flame Line
  - IQ_THIRD_EXOR_FLAME: {MaxLevel: 5, Requires: IQ_JUDGE Lv1}
  - IQ_SECOND_FLAME: {MaxLevel: 5, Requires: IQ_THIRD_EXOR_FLAME Lv1}
  - IQ_THIRD_FLAME_BOMB: {MaxLevel: 5, Requires: IQ_SECOND_FLAME Lv2}
```

---

<!-- RAG_CHUNK: 09_night_watch_skills -->
## Night Watch Skill Tree

```yaml
Job: Night_Watch
Inherit: [Novice, Gunslinger, Rebellion]

Skills:
  # Pistol/Fire Mastery
  - NW_P_F_I: {MaxLevel: 10}
  - NW_INTENSIVE_AIM: {MaxLevel: 1, Requires: NW_P_F_I Lv1}

  # Hidden Card Line
  - NW_HIDDEN_CARD: {MaxLevel: 10, Requires: [NW_P_F_I Lv5, NW_INTENSIVE_AIM Lv1]}

  # Shooting Line
  - NW_THE_VIGILANTE_AT_NIGHT: {MaxLevel: 5, Requires: [NW_P_F_I Lv3, NW_INTENSIVE_AIM Lv1]}
  - NW_ONLY_ONE_BULLET: {MaxLevel: 5, Requires: [NW_P_F_I Lv3, NW_INTENSIVE_AIM Lv1]}
  - NW_SPIRAL_SHOOTING: {MaxLevel: 5, Requires: [NW_P_F_I Lv3, NW_INTENSIVE_AIM Lv1]}
  - NW_MAGAZINE_FOR_ONE: {MaxLevel: 5, Requires: [NW_P_F_I Lv3, NW_INTENSIVE_AIM Lv1]}
  - NW_WILD_FIRE: {MaxLevel: 5, Requires: [NW_P_F_I Lv3, NW_INTENSIVE_AIM Lv1]}
  - NW_WILD_SHOT: {MaxLevel: 5, Requires: [NW_ONLY_ONE_BULLET Lv3, NW_SPIRAL_SHOOTING Lv3, NW_MAGAZINE_FOR_ONE Lv3]}
  - NW_MIDNIGHT_FALLEN: {MaxLevel: 5, Requires: [NW_THE_VIGILANTE_AT_NIGHT Lv3, NW_MAGAZINE_FOR_ONE Lv3, NW_WILD_FIRE Lv3]}

  # Grenade Line
  - NW_GRENADE_MASTERY: {MaxLevel: 10}
  - NW_BASIC_GRENADE: {MaxLevel: 5, Requires: NW_GRENADE_MASTERY Lv3}
  - NW_GRENADE_FRAGMENT: {MaxLevel: 7, Requires: NW_GRENADE_MASTERY Lv1}
  - NW_HASTY_FIRE_IN_THE_HOLE: {MaxLevel: 5, Requires: NW_BASIC_GRENADE Lv3}
  - NW_GRENADES_DROPPING: {MaxLevel: 5, Requires: NW_HASTY_FIRE_IN_THE_HOLE Lv3}
  - NW_AUTO_FIRING_LAUNCHER: {MaxLevel: 5, Requires: NW_GRENADES_DROPPING Lv3}
  - NW_MISSION_BOMBARD: {MaxLevel: 10, Requires: [NW_GRENADE_MASTERY Lv5, NW_GRENADES_DROPPING Lv3]}
```

---

<!-- RAG_CHUNK: 09_4th_jobs_scripting -->
## 4th Job Scripting Examples

### Check if Player is 4th Job
```c
// Using eaclass with EAJL_FOURTH mask
if (eaclass() & EAJL_FOURTH) {
    mes "You have ascended to the 4th job class!";
    mes "Your mastery of both old and new stats is impressive.";
}
```

### Job Change to 4th Job
```c
// Dragon Knight job change
if (BaseJob == Job_Rune_Knight || BaseJob == Job_Rune_Knight_T) {
    if (BaseLevel >= 200 && JobLevel >= 70) {
        jobchange Job_Dragon_Knight;
        getitem 6635,1; // Job change reward
    }
}
```

### Check New Stats (Pow, Sta, Wis, Spl, Crt, Con)
```c
// 4th jobs have access to Trait Stats
if (readparam(bPow) >= 100) {
    mes "Your Power stat is maxed!";
}
if (readparam(bSpl) >= 100) {
    mes "Your Spell stat is maxed!";
}
```

### 4th Job Skill Check
```c
// Check if Dragon Knight has specific skills
if (getskilllv(DK_SERVANTWEAPON) >= 5) {
    mes "You've mastered Servant Weapon!";
    if (getskilllv(DK_SERVANT_W_DEMOL) >= 1) {
        mes "And unlocked the ultimate Servant skill!";
    }
}
```

---

# ═══════════════════════════════════════════════════════════════
# PART 2: ATTENDANCE SYSTEM
# ═══════════════════════════════════════════════════════════════

<!-- RAG_CHUNK: 09_attendance_overview -->
## Attendance System Overview

The Attendance System provides daily login rewards. Players can claim rewards by logging in each day during an event period.

### Database Location
- **File:** `db/re/attendance.yml` (Renewal) or `db/pre-re/attendance.yml` (Pre-Renewal)
- **Type:** ATTENDANCE_DB

---

<!-- RAG_CHUNK: 09_attendance_schema -->
## Attendance YAML Schema

```yaml
# Attendance Database Schema
Header:
  Type: ATTENDANCE_DB
  Version: 1

Body:
  - Start: YYYYMMDD          # Event start date (e.g., 20180502)
    End: YYYYMMDD            # Event end date (e.g., 20180529)
    Rewards:                 # List of daily rewards
      - Day: <number>        # Day number (1-20 typically)
        ItemId: <item_id>    # Item ID to give (aegis name or number)
        Amount: <number>     # Quantity (optional, default: 1)
```

### Example Configuration
```yaml
Body:
  - Start: 20250101
    End: 20250131
    Rewards:
      - Day: 1
        ItemId: 22979        # First day reward
      - Day: 2
        ItemId: 6316         # Second day reward
      - Day: 3
        ItemId: 12265        # 5x item
        Amount: 5
      - Day: 4
        ItemId: 23047
        Amount: 5
      - Day: 5
        ItemId: 23038        # Special item
      - Day: 6
        ItemId: 23043
      - Day: 7
        ItemId: 23340        # Weekly reward (bigger)
        Amount: 3
      - Day: 8
        ItemId: 12516
        Amount: 5
      - Day: 9
        ItemId: 23307
        Amount: 5
      - Day: 10
        ItemId: 12610        # Milestone reward
      - Day: 11
        ItemId: 14533
        Amount: 2
      - Day: 12
        ItemId: 23012
        Amount: 3
      - Day: 13
        ItemId: 23048
        Amount: 5
      - Day: 14
        ItemId: 12264        # Two week reward
        Amount: 5
      - Day: 15
        ItemId: 23046
        Amount: 5
      - Day: 16
        ItemId: 12515
        Amount: 5
      - Day: 17
        ItemId: 12522
        Amount: 5
      - Day: 18
        ItemId: 12523
        Amount: 5
      - Day: 19
        ItemId: 6234
      - Day: 20
        ItemId: 22845        # Final reward
```

---

<!-- RAG_CHUNK: 09_attendance_implementation -->
## Attendance System Implementation

### Server Configuration
Enable attendance in `conf/battle/client.conf`:
```conf
// Enable attendance system
// 0 = disabled, 1 = enabled
feature.attendance: 1
```

### Client Requirement
The client must support the attendance UI (2018+ clients with PACKETVER >= 20180307).

### Script Commands
```c
// Check attendance count
.@count = getd("attendance_count");

// Check if claimed today
.@claimed = checkquest(60001,PLAYTIME); // Quest ID for attendance

// Manual attendance reward (custom NPC)
if (.@count < 20) {
    .@day = .@count + 1;
    // Give reward based on day
    switch(.@day) {
        case 1: getitem 22979,1; break;
        case 7: getitem 23340,3; break;
        case 20: getitem 22845,1; break;
    }
    setd("attendance_count", .@count + 1);
}
```

---

# ═══════════════════════════════════════════════════════════════
# PART 3: STYLIST SYSTEM
# ═══════════════════════════════════════════════════════════════

<!-- RAG_CHUNK: 09_stylist_overview -->
## Stylist System Overview

The Stylist system allows players to change their character's appearance (hair style, hair color, cloth color) through an in-game UI or NPC.

### Database Location
- **Main Config:** `db/stylist.yml`
- **Renewal Options:** `db/re/stylist.yml`
- **Import Override:** `db/import/stylist.yml`

---

<!-- RAG_CHUNK: 09_stylist_schema -->
## Stylist YAML Schema

```yaml
Header:
  Type: STYLIST_DB
  Version: 1

Body:
  - Look: <look_type>       # What to change (Hair_Color, Hair, Cloth_Color)
    Options:                # Available options
      - Index: <number>     # Client-side menu index (-1 for default/revert)
        Value: <number>     # Actual look value (can also be item name)
        CostsHuman:         # Cost for human players
          Price: <zeny>     # Zeny cost (default: 0)
          RequiredItem: <item_name>     # Required item (optional)
          RequiredItemBox: <item_name>  # Required item box (optional)
        CostsDoram:         # Cost for Doram players (same structure)
          Price: <zeny>
          RequiredItem: <item_name>
          RequiredItemBox: <item_name>

Footer:
  Imports:
    - Path: db/re/stylist.yml
      Mode: Renewal
    - Path: db/import/stylist.yml
```

### Look Types
```
Hair_Color    - Changes hair dye color (0-8 typically)
Hair          - Changes hairstyle (1-42+ depending on client)
Cloth_Color   - Changes outfit palette/cloth color
```

---

<!-- RAG_CHUNK: 09_stylist_example -->
## Stylist Configuration Examples

### Basic Hair Color Setup
```yaml
Body:
  - Look: Hair_Color
    Options:
      - Index: -1          # Revert to original
        Value: 0
        CostsHuman:
          Price: 0
        CostsDoram:
          Price: 0
      - Index: 1           # Brown
        Value: 1
        CostsHuman:
          Price: 100000
        CostsDoram:
          Price: 100000
      - Index: 2           # Red
        Value: 2
        CostsHuman:
          Price: 100000
      - Index: 3           # Green
        Value: 3
        CostsHuman:
          Price: 100000
```

### Hairstyle with Item Requirements
```yaml
  - Look: Hair
    Options:
      - Index: 1
        Value: 1
        CostsHuman:
          Price: 100000
        CostsDoram:
          Price: 100000
      # Premium styles requiring coupons
      - Index: 24
        Value: 24
        CostsHuman:
          RequiredItem: New_Style_Coupon
          RequiredItemBox: C_New_Style_Box
      - Index: 28
        Value: 28
        CostsHuman:
          RequiredItem: J_Shop_Coupon
          RequiredItemBox: J_Shop_Coupon_Box
      # Expensive premium styles
      - Index: 33
        Value: 33
        CostsHuman:
          Price: 3000000
```

### Doram-Specific Options
```yaml
      - Index: 7
        Value: 7
        CostsHuman:
          Price: 100000
        CostsDoram:
          RequiredItem: J_Shop_Coupon2
          RequiredItemBox: J_Shop_Coupon2
```

---

<!-- RAG_CHUNK: 09_stylist_npc -->
## Custom Stylist NPC Script

### Simple Stylist NPC
```c
prontera,170,180,1	script	Stylist#custom	122,{
    setarray .@Styles[1],
        getbattleflag("max_cloth_color"),
        getbattleflag("max_hair_style"),
        getbattleflag("max_hair_color");
    setarray .@Look[1],
        LOOK_CLOTHES_COLOR,
        LOOK_HAIR,
        LOOK_HAIR_COLOR;

    set .@s, select(" ~ Cloth color: ~ Hairstyle: ~ Hair color");
    set .@Revert, getlook(.@Look[.@s]);
    set .@Style, 1;

    while(1) {
        setlook .@Look[.@s], .@Style;
        message strcharinfo(0), "This is style #" + .@Style + ".";

        set .@menu$, " ~ Next (^0055FF" +
            ((.@Style != .@Styles[.@s]) ? .@Style + 1 : 1) + "^000000)" +
            ": ~ Previous (^0055FF" +
            ((.@Style != 1) ? .@Style - 1 : .@Styles[.@s]) + "^000000)" +
            ": ~ Jump to...: ~ Revert to original (^0055FF" + .@Revert + "^000000)";

        switch(select(.@menu$)) {
            case 1:
                set .@Style, ((.@Style != .@Styles[.@s]) ? .@Style + 1 : 1);
                break;
            case 2:
                set .@Style, ((.@Style != 1) ? .@Style - 1 : .@Styles[.@s]);
                break;
            case 3:
                message strcharinfo(0), "Choose a style between 1 - " + .@Styles[.@s] + ".";
                input .@Style, 0, .@Styles[.@s];
                if (!.@Style)
                    set .@Style, rand(1, .@Styles[.@s]);
                break;
            case 4:
                set .@Style, .@Revert;
                setlook .@Look[.@s], .@Revert;
                break;
        }
    }
}
```

### Premium Stylist with Costs
```c
prontera,172,180,1	script	Premium Stylist	122,{
    mes "[Premium Stylist]";
    mes "Welcome! Our services require payment.";
    next;

    switch(select("Hair Style (500,000z):Hair Color (100,000z):Cloth Color (200,000z):Cancel")) {
        case 1:
            if (Zeny < 500000) {
                mes "[Premium Stylist]";
                mes "You need 500,000 zeny.";
                close;
            }
            set .@look, LOOK_HAIR;
            set .@max, getbattleflag("max_hair_style");
            set .@cost, 500000;
            break;
        case 2:
            if (Zeny < 100000) {
                mes "[Premium Stylist]";
                mes "You need 100,000 zeny.";
                close;
            }
            set .@look, LOOK_HAIR_COLOR;
            set .@max, getbattleflag("max_hair_color");
            set .@cost, 100000;
            break;
        case 3:
            if (Zeny < 200000) {
                mes "[Premium Stylist]";
                mes "You need 200,000 zeny.";
                close;
            }
            set .@look, LOOK_CLOTHES_COLOR;
            set .@max, getbattleflag("max_cloth_color");
            set .@cost, 200000;
            break;
        case 4:
            close;
    }

    mes "[Premium Stylist]";
    mes "Choose a style (1-" + .@max + "):";
    input .@style, 1, .@max;

    mes "[Premium Stylist]";
    mes "Confirm style #" + .@style + " for " + .@cost + " zeny?";
    if (select("Yes:No") == 1) {
        Zeny -= .@cost;
        setlook .@look, .@style;
        mes "[Premium Stylist]";
        mes "Enjoy your new look!";
    }
    close;
}
```

---

<!-- RAG_CHUNK: 09_stylist_commands -->
## Stylist Script Commands

### setlook
```c
setlook <look_type>, <value>;

// Look types:
LOOK_HAIR          // Hairstyle
LOOK_HAIR_COLOR    // Hair color
LOOK_CLOTHES_COLOR // Cloth/outfit color
LOOK_HEAD_BOTTOM   // Lower headgear view
LOOK_HEAD_TOP      // Upper headgear view
LOOK_HEAD_MID      // Middle headgear view
LOOK_ROBE          // Robe view
LOOK_BODY2         // Body style (alternate)

// Example
setlook LOOK_HAIR, 15;        // Set hairstyle to 15
setlook LOOK_HAIR_COLOR, 3;   // Set hair color to 3
```

### getlook
```c
<value> = getlook(<look_type>);

// Example
.@current_hair = getlook(LOOK_HAIR);
.@current_color = getlook(LOOK_HAIR_COLOR);
```

### changelook
```c
changelook <look_type>, <value>;
// Same as setlook but for attached player only
```

### getbattleflag
```c
// Get maximum allowed styles from battle config
.@max_hair = getbattleflag("max_hair_style");
.@max_hair_color = getbattleflag("max_hair_color");
.@max_cloth_color = getbattleflag("max_cloth_color");
```

---

<!-- RAG_CHUNK: 09_stylist_config -->
## Stylist Server Configuration

### conf/battle/client.conf
```conf
// Maximum hair style ID (default: 23)
// Higher values require client-side sprites
max_hair_style: 42

// Maximum hair color ID (default: 8)
max_hair_color: 8

// Maximum cloth color ID (default: 4)
max_cloth_color: 4

// Minimum hair style (default: 1)
min_hair_style: 1

// Minimum hair color (default: 0)
min_hair_color: 0

// Minimum cloth color (default: 0)
min_cloth_color: 0
```

---

<!-- RAG_CHUNK: 09_cross_reference -->
## Cross-Reference with Existing KB

### Related Files
| Topic | KB File | Section |
|-------|---------|---------|
| Job IDs (EAJ_*) | 05_GAME_MECHANICS | Part 1-4 |
| Status Effects for 4th Jobs | 03_STATUS_EFFECTS | SC_* entries |
| Item Bonuses | 04_ITEM_BONUSES | All |
| NPC Scripting | 06_CONTENT_CREATION | Parts 1-6 |
| Script Commands | 02_SCRIPT_COMMANDS | All |

### Skill Prefix Reference
| Prefix | Job Class | Example |
|--------|-----------|---------|
| DK_ | Dragon Knight | DK_SERVANTWEAPON |
| IG_ | Imperial Guard | IG_GUARD_STANCE |
| MT_ | Meister | MT_ABR_M |
| BO_ | Biolo | BO_BIONIC_PHARMACY |
| SHC_ | Shadow Cross | SHC_SHADOW_EXCEED |
| ABC_ | Abyss Chaser | ABC_ABYSS_SLAYER |
| AG_ | Arch Mage | AG_ASTRAL_STRIKE |
| EM_ | Elemental Master | EM_ELEMENTAL_BUSTER |
| CD_ | Cardinal | CD_PNEUMATICUS_PROCELLA |
| IQ_ | Inquisitor | IQ_MASSIVE_F_BLASTER |
| WH_ | Windhawk | WH_CALAMITYGALE |
| TR_ | Troubadour/Trouvere | TR_MYSTIC_SYMPHONY |
| SKE_ | Sky Emperor | SKE_ALL_IN_THE_SKY |
| SOA_ | Soul Ascetic | SOA_SOUL_OF_HEAVEN_AND_EARTH |
| NW_ | Night Watch | NW_MISSION_BOMBARD |
| SS_ | Shinkiro/Shiranui | SS_ANKOKURYUUAKUMU |
| SH_ | Spirit Handler | SH_COMMUNE_WITH_CHUL_HO |
| HN_ | Hyper Novice | HN_BREAKINGLIMIT |

---

<!-- RAG_METADATA -->
<!-- VERSION: 1.0 -->
<!-- LINES: ~1200 -->
<!-- RAG_CHUNKS: 18 -->
<!-- VALIDATED: 2025-12-12 -->
<!-- SOURCE: github.com/rathena/rathena (official repo) -->
