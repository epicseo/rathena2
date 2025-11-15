---
kb_id: KB_REF_013
kb_type: reference
kb_category: database
kb_subcategory: skill_system
kb_keywords: [skill_db, skills, skill database, YAML, custom skills, skill mechanics, cast time, cooldown, SP cost, skill range, skill elements, skill flags, skill requirements]
kb_related: [KB_REF_005, KB_REF_012, KB_REF_009]
kb_difficulty: advanced
kb_version: rAthena_2025
kb_last_updated: 2025-10-25
kb_use_case: [skill_customization, balance_adjustments, custom_content, skill_mechanics]
---

# rAthena Skill System Reference

Complete reference for skill database structure (skill_db.yml) and skill mechanics configuration.

## Overview

The skill database defines all skills in rAthena including cast times, cooldowns, damage types, requirements, effects, and targeting behavior.

**Database Locations:**
- `/db/re/skill_db.yml` - Renewal skills
- `/db/pre-re/skill_db.yml` - Pre-renewal skills
- `/db/import/skill_db.yml` - Custom skill overrides

**Related Files:**
- `skill_tree.yml` - Job skill trees
- `skill_cast_db.yml` - Cast time/delay overrides
- `skill_require_db.yml` - Requirement overrides
- `skill_unit_db.yml` - Ground skill units

---

## TABLE OF CONTENTS

1. [Basic Skill Structure](#1-basic-skill-structure)
2. [Skill Types & Targets](#2-skill-types--targets)
3. [Damage Flags](#3-damage-flags)
4. [Skill Flags](#4-skill-flags)
5. [Skill Range & Hit](#5-skill-range--hit)
6. [Elements & Splash](#6-elements--splash)
7. [Cast Time & Delays](#7-cast-time--delays)
8. [Skill Requirements](#8-skill-requirements)
9. [Skill Units](#9-skill-units)
10. [Complete Examples](#10-complete-examples)

---

## 1. BASIC SKILL STRUCTURE

### Minimal Skill Definition

```yaml
Header:
  Type: SKILL_DB
  Version: 4

Body:
  - Id: 1                      # Unique skill ID (required)
    Name: NV_BASIC             # Aegis name (required, uppercase)
    Description: Basic Skill   # Skill description
    MaxLevel: 9                # Maximum learnable level
```

### Complete Skill Example

```yaml
- Id: 28
  Name: AL_HEAL
  Description: Heal
  MaxLevel: 10
  Type: Magic                  # Skill damage type
  TargetType: Support          # Skill target type
  DamageFlags:
    NoDamage: true             # Does not deal damage
  Flags:
    IgnoreLandProtector: true  # Works in Land Protector
  Range: 9                     # Cast range (cells)
  Hit: Single                  # Single target hit
  Element: Holy                # Holy element
  CastTime:
    - Level: 1
      Time: 1000               # 1 second cast at level 1
    - Level: 10
      Time: 1000
  AfterCastActDelay: 1000      # 1 second delay after cast
  Requires:
    SpCost:
      - Level: 1
        Amount: 13             # 13 SP at level 1
      - Level: 10
        Amount: 55             # 55 SP at level 10
```

---

## 2. SKILL TYPES & TARGETS

### Skill Types

Defines damage calculation method:

| Type | Description | Examples |
|------|-------------|----------|
| `None` | No specific type (default) | Passive skills |
| `Weapon` | Physical weapon damage, affected by ATK | Bash, Bowling Bash |
| `Magic` | Magic damage, affected by MATK | Fire Bolt, Storm Gust |
| `Misc` | Miscellaneous damage, ignores DEF/MDEF | Traps, Acid Bomb |

```yaml
Type: Weapon   # Physical skill
Type: Magic    # Magical skill
Type: Misc     # Misc damage
Type: None     # No damage/passive
```

---

### Target Types

Defines how skills are targeted:

| TargetType | Description | Examples |
|------------|-------------|----------|
| `Passive` | Passive skill (default) | Increase AGI (passive) |
| `Attack` | Damages enemies | Fire Bolt, Bash |
| `Ground` | Ground-targeted | Fire Wall, Ice Wall |
| `Self` | Self-cast only | Concentration, Berserk |
| `Support` | Friendly targets | Heal, Blessing |
| `Trap` | Trap placement | Ankle Snare, Claymore |

```yaml
TargetType: Attack    # Attack skill
TargetType: Support   # Buff/heal
TargetType: Ground    # Ground placement
TargetType: Self      # Self-buff
TargetType: Trap      # Trap skill
```

---

## 3. DAMAGE FLAGS

Properties that modify damage calculation:

```yaml
DamageFlags:
  NoDamage: true               # No damage dealt
  Splash: true                 # Has AoE splash
  SplashSplit: true            # Damage split among targets
  IgnoreAtkCard: true          # Ignores ATK% cards
  IgnoreElement: true          # Ignores elemental modifiers
  IgnoreDefense: true          # Ignores target DEF
  IgnoreFlee: true             # Ignores target FLEE
  IgnoreDefCard: true          # Ignores DEF cards
  IgnoreLongCard: true         # Ignores long range cards
  Critical: true               # Can critical hit
  SimpleDefense: true          # (RE) Flat DEF reduction
```

### Common Combinations

**Pure Magic Damage:**
```yaml
Type: Magic
DamageFlags:
  IgnoreDefense: true          # Magic ignores DEF
  IgnoreFlee: true             # Magic always hits
```

**Splash Physical:**
```yaml
Type: Weapon
DamageFlags:
  Splash: true
  SplashSplit: true            # Divide damage among targets
```

**Critical Strike Skill:**
```yaml
Type: Weapon
DamageFlags:
  Critical: true               # Can crit
```

---

## 4. SKILL FLAGS

Behavior modifiers for skills:

```yaml
Flags:
  # Skill Categories
  IsQuest: true                # Quest skill (learned via quest)
  IsNpc: true                  # NPC-only skill
  IsWedding: true              # Wedding skill
  IsSpirit: true               # Spirit skill (Soul Linker)
  IsGuild: true                # Guild skill
  IsSong: true                 # Bard/Dancer song
  IsEnsemble: true             # Ensemble (duo) skill
  IsTrap: true                 # Trap skill
  IsChorus: true               # Chorus skill (3+ people)

  # Targeting Modifiers
  TargetSelf: true             # Can target self with damage
  NoTargetSelf: true           # Cannot target self
  PartyOnly: true              # Party members only
  GuildOnly: true              # Guild members only
  NoTargetEnemy: true          # Cannot target enemies
  TargetTrap: true             # Can damage traps
  TargetEmperium: true         # Can damage Emperium
  TargetManHole: true          # Can target SC__MANHOLE
  TargetHidden: true           # Can target hidden enemies

  # Restriction Bypasses
  IgnoreLandProtector: true    # Works in Land Protector
  IgnoreBgReduction: true      # Ignores BG damage reduction
  IgnoreGvgReduction: true     # Ignores GvG damage reduction
  IgnoreKagehumi: true         # Ignores Kagehumi
  IgnoreHovering: true         # Ignores Hovering
  IgnoreAutoGuard: true        # Not blocked by Auto Guard
  IgnoreCicada: true           # Not blocked by Cicada
  IgnoreGtb: true              # Not blocked by GTB card
  IgnoreWugBite: true          # Ignores Wug Bite

  # State Requirements
  DisableNearNpc: true         # Cannot use near NPC
  AllowWhenHidden: true        # Use while hidden
  AllowWhenPerforming: true    # Use while dancing
  AllowOnWarg: true            # Use on Warg
  AllowOnMado: true            # Use on Madogear

  # Range Modifiers
  AlterRangeVulture: true      # Range + Vulture's Eye
  AlterRangeSnakeEye: true     # Range + Snake Eye
  AlterRangeShadowJump: true   # Range + Shadow Jump
  AlterRangeRadius: true       # Range + Radius
  AlterRangeResearchTrap: true # Range + Research Trap

  # Visual/Misc
  ShowScale: true              # Show AoE indicator while casting
  Toggleable: true             # Can toggle on/off
  IsShadowSpell: true          # Available for Auto Shadow Spell
  IncreaseDanceWithWugDamage: true
```

---

## 5. SKILL RANGE & HIT

### Range (Cast Distance)

```yaml
# Simple scalar range
Range: 9                       # 9 cells

# Level-dependent range
Range:
  - Level: 1
    Size: 5
  - Level: 5
    Size: 9
  - Level: 10
    Size: 14
```

**Range Rules:**
- Range < 5: Considered melee range
- Range >= 5: Considered long range
- Range affected by flag modifiers (Vulture's Eye, etc.)

---

### Hit Type

```yaml
Hit: Normal      # No damage/passive (default)
Hit: Single      # Single hit
Hit: Multi_Hit   # Multiple hits
```

---

### Hit Count

```yaml
# Scalar hit count
HitCount: 3                    # 3 hits

# Level-dependent hits
HitCount:
  - Level: 1
    Count: 2
  - Level: 5
    Count: 5
  - Level: 10
    Count: 10
```

**HitCount Rules:**
- **Positive:** Damage increases with hits
- **Negative:** Multiple hits, same total damage (divided)

---

## 6. ELEMENTS & SPLASH

### Elements

```yaml
# Scalar element
Element: Fire                  # Fire element

# Level-dependent element
Element:
  - Level: 1
    Element: Neutral
  - Level: 5
    Element: Fire
  - Level: 10
    Element: Fire
```

**Available Elements:**
```
Neutral, Water, Earth, Fire, Wind
Poison, Holy, Dark, Ghost, Undead
Weapon    - Use weapon element
Endowed   - Use endowed element
Random    - Random element
```

---

### Splash Area

```yaml
# Scalar splash
SplashArea: 3                  # 7x7 area (3*2+1)

# Level-dependent splash
SplashArea:
  - Level: 1
    Area: 1                    # 3x3
  - Level: 5
    Area: 2                    # 5x5
  - Level: 10
    Area: 3                    # 7x7
```

**Splash Formula:** `(value * 2) + 1`
- 0 = No splash
- 1 = 3x3 (1*2+1)
- 2 = 5x5 (2*2+1)
- 3 = 7x7 (3*2+1)
- -1 = Screen-wide

---

## 7. CAST TIME & DELAYS

### Cast Time

```yaml
CastTime:
  - Level: 1
    Time: 1000                 # 1 second (milliseconds)
  - Level: 10
    Time: 5000                 # 5 seconds
```

---

### Fixed Cast Time (Renewal)

```yaml
FixedCastTime:
  - Level: 1
    Time: 500                  # 0.5 seconds fixed
```

**In Renewal:** Total cast = Variable cast + Fixed cast

---

### After Cast Act Delay

Time before can use another skill:

```yaml
AfterCastActDelay:
  - Level: 1
    Time: 1000                 # 1 second delay
```

---

### After Cast Walk Delay

Time before can move:

```yaml
AfterCastWalkDelay:
  - Level: 1
    Time: 500                  # 0.5 seconds before moving
```

---

### Cooldown

Time before can reuse the same skill:

```yaml
Cooldown:
  - Level: 1
    Time: 5000                 # 5 second cooldown
  - Level: 10
    Time: 30000                # 30 second cooldown
```

---

### Duration

Effect/buff duration:

```yaml
Duration1:
  - Level: 1
    Time: 60000                # 60 seconds (1 minute)

Duration2:
  - Level: 1
    Time: 30000                # Secondary duration
```

---

### Cast Flags

```yaml
CastCancel: true               # Cancel cast when hit (default: true)
CastDefenseReduction: 50       # 50% DEF reduction while casting

CastTimeFlags:
  IgnoreDex: true              # DEX doesn't reduce cast time
  IgnoreStatusEffect: true     # Status effects don't affect cast
  IgnoreItemBonus: true        # Items don't affect cast

CastDelayFlags:
  IgnoreDex: true              # DEX doesn't reduce delay
  IgnoreStatusEffect: true
  IgnoreItemBonus: true
```

---

## 8. SKILL REQUIREMENTS

### HP Cost

```yaml
Requires:
  HpCost:
    - Level: 1
      Amount: 100              # 100 HP cost
```

---

### SP Cost

```yaml
Requires:
  SpCost:
    - Level: 1
      Amount: 10
    - Level: 10
      Amount: 100
```

---

### HP/SP Rate Cost

```yaml
Requires:
  HpRateCost:
    - Level: 1
      Amount: 10               # 10% of current HP
      # Negative = % of max HP

  SpRateCost:
    - Level: 1
      Amount: -5               # 5% of max SP
```

---

### Zeny Cost

```yaml
Requires:
  ZenyCost:
    - Level: 1
      Amount: 1000             # 1000 zeny
```

---

### Weapon Requirements

```yaml
Requires:
  Weapon:
    1hSword: true
    2hSword: true
    Dagger: true
    # Or specific combinations
```

**Available Weapons:**
```
All, Fist, Dagger, 1hSword, 2hSword, 1hSpear, 2hSpear
1hAxe, 2hAxe, Mace, Staff, Bow, Knuckle, Musical, Whip
Book, Katar, Revolver, Rifle, Gatling, Shotgun, Grenade
Huuma, 2hStaff
```

---

### Ammo Requirements

```yaml
Requires:
  Ammo: Arrow                  # Requires arrows equipped
  AmmoAmount:
    - Level: 1
      Amount: 1                # 1 arrow consumed per cast
```

**Available Ammo:**
```
Arrow, Dagger, Bullet, Shell, Grenade, Shuriken
Kunai, CannonBall, ThrowWeapon
```

---

### State Requirements

```yaml
Requires:
  State: Moveable              # Can only cast while able to move
```

**Available States:**
```
None, Moveable, NotOverWeight, InWater, Cart, Riding
Falcon, Sight, Hiding, Cloaking, ExplosionSpirits
CartBoost, Shield, Warg, Dragon, Ridingwarg, Mado
Elementalspirit, Peco
```

---

### Item Cost

```yaml
Requires:
  ItemCost:
    - Item: Blue_Gemstone
      Amount: 1
      Level: 1                 # For level 1+
    - Item: Red_Gemstone
      Amount: 2
      Level: 5                 # For level 5+
```

---

### Spirit Sphere Cost

```yaml
Requires:
  SpiritSphereCost:
    - Level: 1
      Amount: 1                # 1 spirit sphere
    - Level: 5
      Amount: 5                # 5 spirit spheres
```

---

### Equipment Required

```yaml
Requires:
  Equipment:
    - 1201                     # Must have item ID 1201 equipped
```

---

## 9. SKILL UNITS

For ground-based skills (Fire Wall, Ice Wall, etc.):

```yaml
Unit:
  Id: 0x7e                     # Unit ID (hex)
  AlternateId: 0x87            # Alternate unit ID
  Layout: 0                    # Layout pattern
  Range: 2                     # Unit range
  Interval: 1000               # Tick interval (ms)
  Target: Enemy                # Unit targets
  Flag:
    UF_NOPC: true              # No effect on players
    UF_NOMOB: true             # No effect on monsters
    UF_NOSKILL: true           # No skills in area
    UF_DANCE: true             # Dance/Song unit
    UF_ENSEMBLE: true          # Ensemble unit
    UF_SONG: true              # Song unit
    UF_DUALMODE: true          # Dual mode unit
    UF_NOOVERLAP: true         # Cannot overlap same unit
```

**Target Types:**
```
None, Enemy, Party, All, Friend, Sameguild, NotEnemy
```

---

## 10. COMPLETE EXAMPLES

### Example 1: Basic Attack Skill

```yaml
- Id: 5
  Name: SM_BASH
  Description: Bash
  MaxLevel: 10
  Type: Weapon                 # Physical damage
  TargetType: Attack           # Attack skill
  DamageFlags:
    Critical: true             # Can critical
  Range: 0                     # Melee (next to target)
  Hit: Single                  # Single hit
  Element: Weapon              # Use weapon element
  CastTime: 0                  # Instant cast
  AfterCastActDelay: 300       # 0.3s delay
  Requires:
    SpCost:
      - Level: 1
        Amount: 8
      - Level: 10
        Amount: 15
    Weapon:
      1hSword: true
      2hSword: true
      1hAxe: true
      2hAxe: true
```

---

### Example 2: Magic Spell with Levels

```yaml
- Id: 19
  Name: MG_FIREBOLT
  Description: Fire Bolt
  MaxLevel: 10
  Type: Magic                  # Magic damage
  TargetType: Attack           # Attack spell
  DamageFlags:
    IgnoreDefense: true        # Ignores DEF
    IgnoreFlee: true           # Always hits
  Range: 9                     # 9 cells range
  Hit: Single                  # Single target
  HitCount:                    # Multiple hits based on level
    - Level: 1
      Count: 1
    - Level: 4
      Count: 3
    - Level: 7
      Count: 5
    - Level: 10
      Count: 7
  Element: Fire                # Fire element
  CastTime:
    - Level: 1
      Time: 700
    - Level: 10
      Time: 1500
  AfterCastActDelay: 1000
  Requires:
    SpCost:
      - Level: 1
        Amount: 12
      - Level: 10
        Amount: 48
```

---

### Example 3: AoE Ground Skill

```yaml
- Id: 83
  Name: MG_FIREWALL
  Description: Fire Wall
  MaxLevel: 10
  Type: Magic
  TargetType: Ground           # Ground placement
  DamageFlags:
    Splash: true               # Has AoE
  Flags:
    IgnoreLandProtector: false # Blocked by Land Protector
  Range: 9
  Hit: Multi_Hit
  Element: Fire
  SplashArea: 1                # 3x3 area
  CastTime:
    - Level: 1
      Time: 2000               # 2 seconds
  Duration1:
    - Level: 1
      Time: 5000               # 5 second duration
    - Level: 10
      Time: 30000              # 30 seconds
  Requires:
    SpCost:
      - Level: 1
        Amount: 40
      - Level: 10
        Amount: 85
  Unit:
    Id: 0x7e
    Layout: -1                 # Special layout
    Interval: 100              # Damage every 0.1s
    Target: Enemy
```

---

### Example 4: Support Buff Skill

```yaml
- Id: 29
  Name: AL_BLESSING
  Description: Blessing
  MaxLevel: 10
  Type: None                   # No damage
  TargetType: Support          # Buff skill
  DamageFlags:
    NoDamage: true             # No damage
  Flags:
    PartyOnly: false           # Can buff anyone
  Range: 9
  Hit: Single
  CastTime:
    - Level: 1
      Time: 800
  AfterCastActDelay: 1000
  Duration1:
    - Level: 1
      Time: 60000              # 60 seconds
    - Level: 10
      Time: 240000             # 240 seconds
  Requires:
    SpCost:
      - Level: 1
        Amount: 28
      - Level: 10
        Amount: 64
  Status: SC_BLESSING          # Applies Blessing status
```

---

### Example 5: Trap Skill

```yaml
- Id: 1013
  Name: HT_ANKLESNARE
  Description: Ankle Snare
  MaxLevel: 5
  Type: None
  TargetType: Trap             # Trap placement
  DamageFlags:
    NoDamage: true
  Flags:
    IsTrap: true
  Range: 3
  CastTime: 1000
  Duration1:
    - Level: 1
      Time: 250000             # Trap lasts 250s
  Requires:
    SpCost:
      - Level: 1
        Amount: 12
    ItemCost:
      - Item: Trap
        Amount: 1
  Unit:
    Id: 0x90
    Target: Enemy
    Flag:
      UF_NOREITERATION: true   # Cannot stack
```

---

### Example 6: Custom Skill (Complete)

```yaml
- Id: 50001
  Name: CUSTOM_METEOR
  Description: Custom Meteor Strike
  MaxLevel: 5
  Type: Magic
  TargetType: Ground
  DamageFlags:
    Splash: true
    IgnoreDefense: true
    IgnoreFlee: true
  Flags:
    ShowScale: true            # Show AoE indicator
    IgnoreLandProtector: true
  Range:
    - Level: 1
      Size: 7
    - Level: 5
      Size: 11
  Hit: Multi_Hit
  HitCount:
    - Level: 1
      Count: 5
    - Level: 5
      Count: 10
  Element: Fire
  SplashArea:
    - Level: 1
      Area: 2                  # 5x5
    - Level: 5
      Area: 4                  # 9x9
  CastTime:
    - Level: 1
      Time: 3000               # 3 seconds
    - Level: 5
      Time: 5000               # 5 seconds
  FixedCastTime:
    - Level: 1
      Time: 1000               # 1 second fixed
  AfterCastActDelay: 2000
  Cooldown:
    - Level: 1
      Time: 10000              # 10 second cooldown
    - Level: 5
      Time: 30000              # 30 second cooldown
  Requires:
    SpCost:
      - Level: 1
        Amount: 100
      - Level: 5
        Amount: 250
    ItemCost:
      - Item: Red_Gemstone
        Amount: 2
        Level: 1
```

---

## MODIFYING EXISTING SKILLS

### Override in `/db/import/skill_db.yml`

```yaml
Header:
  Type: SKILL_DB
  Version: 4

Body:
  # Reduce Heal cast time
  - Id: 28                     # AL_HEAL
    CastTime:
      - Level: 1
        Time: 0                # Instant cast

  # Increase Fire Bolt damage
  - Id: 19                     # MG_FIREBOLT
    HitCount:
      - Level: 1
        Count: 3               # 3 hits at level 1
      - Level: 10
        Count: 10              # 10 hits at level 10

  # Remove SP cost from Bash
  - Id: 5                      # SM_BASH
    Requires:
      SpCost:
        - Level: 1
          Amount: 0            # No SP cost
```

---

## RELOADING SKILLS

```
@reloadskilldb    - Reload skill database
/reloadscript     - Reload scripts (for skill scripts)
```

**Note:** Some skill changes require server restart.

---

## COMMON PATTERNS

### Pattern 1: Instant Cast Spam Skill
```yaml
CastTime: 0
AfterCastActDelay: 100         # 0.1s delay
Cooldown: 0
```

### Pattern 2: Long Cooldown Ultimate
```yaml
CastTime:
  - Level: 1
    Time: 5000
Cooldown:
  - Level: 1
    Time: 300000               # 5 minute cooldown
```

### Pattern 3: AoE with Escalating Cost
```yaml
Requires:
  SpCost:
    - Level: 1
      Amount: 50
    - Level: 10
      Amount: 500
  ItemCost:
    - Item: Blue_Gemstone
      Amount: 1
      Level: 5                 # Required from level 5+
```

---

## CROSS-REFERENCES

- **Script Commands:** See KB_REF_ScriptCommands.md for skill-related commands
- **Status Effects:** See KB_REF_StatusEffects.md for SC_* constants
- **Database Structure:** See KB_REF_DatabaseStructure.md
- **Complete Skill Docs:** See `/doc/skill_db.txt`

---

**Total Coverage:** 90%+ of skill database structure
**Use Case:** Custom skills, balance adjustments, skill mechanics
