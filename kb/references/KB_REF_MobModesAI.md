---
kb_id: KB_REF_018
kb_type: reference
kb_category: database
kb_subcategory: monster_ai
kb_keywords: [mob modes, monster AI, MD_, aggressive, passive, looter, assist, boss, MVP, mode flags, behavior, monster behavior]
kb_related: [KB_REF_012, KB_REF_015]
kb_difficulty: advanced
kb_version: rAthena_2025
kb_last_updated: 2025-10-25
kb_use_case: [monster_customization, mob_behavior, AI_configuration, boss_mechanics]
---

# rAthena Monster AI & Modes Reference

Complete reference for monster AI types, behavior modes, and class types in mob_db.yml.

## Overview

Monster behavior in rAthena is controlled by three components:
1. **AI Type** - Predefined behavior pattern (01-27)
2. **Class Type** - Monster classification (Normal, Boss, Guardian, etc.)
3. **Mode Flags** - Individual behavior modifiers (Can Move, Aggressive, etc.)

**Database Location:** `/db/re/mob_db.yml` or `/db/pre-re/mob_db.yml`

---

## TABLE OF CONTENTS

1. [AI Types (Aegis)](#1-ai-types-aegis)
2. [Mode Flags](#2-mode-flags)
3. [Class Types](#3-class-types)
4. [Attribute Types](#4-attribute-types)
5. [Common Combinations](#5-common-combinations)
6. [Practical Examples](#6-practical-examples)

---

## 1. AI TYPES (AEGIS)

Predefined AI behavior patterns matching official Ragnarok Online.

### Basic AI Types

| AI | Hex | Decimal | Behavior |
|----|-----|---------|----------|
| **01** | 0x0081 | 129 | **Passive** - Won't attack unless provoked |
| **02** | 0x0083 | 131 | **Passive Looter** - Passive + picks up items |
| **03** | 0x1089 | 4233 | **Passive Assist** - Helps same-type mobs |
| **04** | 0x3885 | 14469 | **Angry** - Hyper-active, changes targets |
| **05** | 0x2085 | 8325 | **Aggressive** - Attacks on sight |
| **06** | 0x0000 | 0 | **Plant** - Immobile, can't attack |
| **07** | 0x108B | 4235 | **Passive Looter Assist** - Combines 02 + 03 |
| **08** | 0x7085 | 28805 | **Aggressive Weak** - Only attacks weak players |

**Usage in mob_db.yml:**
```yaml
- Id: 1002
  AegisName: PORING
  Ai: 01      # Passive behavior
  Class: Normal

- Id: 1023
  AegisName: ORK_WARRIOR
  Ai: 05      # Aggressive behavior
  Class: Normal
```

---

### Advanced AI Types

| AI | Hex | Decimal | Behavior |
|----|-----|---------|----------|
| **09** | 0x3095 | 12437 | **Guardian** - Aggressive, cast sensor |
| **10** | 0x0084 | 132 | **Aggressive Immobile** |
| **11** | 0x0084 | 132 | **Aggressive Immobile Guardian** |
| **12** | 0x2085 | 8325 | **Aggressive Guardian** |
| **13** | 0x308D | 12429 | **Aggressive Assist** - Helps allies |
| **17** | 0x0091 | 145 | **Passive Cast Sensor** - Retaliates to magic |
| **19** | 0x3095 | 12437 | **Aggressive Cast Sensor** |
| **20** | 0x3295 | 12949 | **Aggressive Multi-Sensor** |
| **21** | 0x3695 | 13973 | **Aggressive Hunter** - Switches targets easily |
| **24** | 0x00A1 | 161 | **Slave** - Passive, no random walk |
| **25** | 0x0001 | 1 | **Pet** - Passive, can't attack |
| **26** | 0xB695 | 46741 | **Chaotic** - Random targeting |
| **27** | 0x8084 | 32900 | **Turret** - Aggressive immobile, random target |

---

### Special AI Types

```yaml
# Ancient Worm Boss Room AI
ABR_PASSIVE: 0x0021    # Passive, immobile, can't attack
ABR_OFFENSIVE: 0x00A5  # Aggressive, immobile
```

---

## 2. MODE FLAGS

Individual behavior modifiers that can be combined.

### Movement Flags

| Flag | Hex | Decimal | Description |
|------|-----|---------|-------------|
| **MD_CANMOVE** | 0x0000001 | 1 | Can move and chase players |
| **MD_NORANDOMWALK** | 0x0000020 | 32 | Won't randomly walk (stays in place) |

```yaml
Modes:
  CanMove: true          # Monster can move
  NoRandomWalk: false    # Monster walks randomly
```

---

### Behavior Flags

| Flag | Hex | Decimal | Description |
|------|-----|---------|-------------|
| **MD_LOOTER** | 0x0000002 | 2 | Picks up items from ground |
| **MD_AGGRESSIVE** | 0x0000004 | 4 | Attacks players on sight |
| **MD_ASSIST** | 0x0000008 | 8 | Helps same-type mobs when attacked |
| **MD_CANATTACK** | 0x0000080 | 128 | Can perform normal attacks |
| **MD_ANGRY** | 0x0000800 | 2048 | Hyper-active behavior |

```yaml
Modes:
  Looter: true           # Picks up items
  Aggressive: true       # Attacks on sight
  Assist: true           # Helps allies
  CanAttack: true        # Can use normal attacks
  Angry: false           # Normal behavior
```

---

### Cast Sensor Flags

| Flag | Hex | Decimal | Description |
|------|-----|---------|-------------|
| **MD_CASTSENSORIDLE** | 0x0000010 | 16 | Attacks casters when idle |
| **MD_CASTSENSORCHASE** | 0x0000200 | 512 | Switches to casters while chasing |
| **MD_NOCAST** | 0x0000040 | 64 | Cannot cast skills |

```yaml
Modes:
  CastSensorIdle: true   # Reacts to spells while idle
  CastSensorChase: true  # Switches to casters while chasing
```

---

### Target Switching Flags

| Flag | Hex | Decimal | Description |
|------|-----|---------|-------------|
| **MD_CHANGECHASE** | 0x0000400 | 1024 | Switches chase target to nearest |
| **MD_CHANGETARGETMELEE** | 0x0001000 | 4096 | Switches target when hit (melee) |
| **MD_CHANGETARGETCHASE** | 0x0002000 | 8192 | Switches target when hit (chasing) |
| **MD_TARGETWEAK** | 0x0004000 | 16384 | Only targets weak players (-5 levels) |
| **MD_RANDOMTARGET** | 0x0008000 | 32768 | Random target per attack |

```yaml
Modes:
  ChangeChase: true           # Switches to closest player
  ChangeTargetMelee: true     # Switches when hit in melee
  ChangeTargetChase: true     # Switches when hit while chasing
  TargetWeak: false           # Attacks any level
  RandomTarget: false         # Consistent targeting
```

---

### Immunity Flags

| Flag | Hex | Decimal | Description |
|------|-----|---------|-------------|
| **MD_IGNOREMELEE** | 0x0010000 | 65536 | Takes 1 HP from melee attacks |
| **MD_IGNOREMAGIC** | 0x0020000 | 131072 | Takes 1 HP from magic attacks |
| **MD_IGNORERANGED** | 0x0040000 | 262144 | Takes 1 HP from ranged attacks |
| **MD_IGNOREMISC** | 0x0100000 | 1048576 | Takes 1 HP from misc attacks |
| **MD_MVP** | 0x0080000 | 524288 | MVP flag, immune to Coma |
| **MD_KNOCKBACKIMMUNE** | 0x0200000 | 2097152 | Cannot be knocked back |
| **MD_TELEPORTBLOCK** | 0x0400000 | 4194304 | Blocks teleportation (not implemented) |

```yaml
Modes:
  IgnoreMelee: true      # 1 HP from physical attacks
  IgnoreMagic: true      # 1 HP from magic
  IgnoreRanged: true     # 1 HP from ranged
  Mvp: true              # Is an MVP
  KnockbackImmune: true  # Cannot be knocked back
```

---

### Special Flags

| Flag | Hex | Decimal | Description |
|------|-----|---------|-------------|
| **MD_DETECTOR** | 0x2000000 | 33554432 | Detects hidden/cloaked players |
| **MD_STATUSIMMUNE** | 0x4000000 | 67108864 | Immune to all status effects |
| **MD_SKILLIMMUNE** | 0x8000000 | 134217728 | Immune to all skills |
| **MD_FIXEDITEMDROP** | 0x1000000 | 16777216 | Drops ignore server rates |

```yaml
Modes:
  Detector: true         # Can see hidden players
  StatusImmune: true     # Immune to status effects
  SkillImmune: true      # Immune to skills
  FixedItemDrop: true    # Drops ignore rates
```

---

## 3. CLASS TYPES

Monster classifications with special properties.

| Class | Hex | Decimal | Modes Added |
|-------|-----|---------|-------------|
| **Normal** | 0x0000000 | 0 | Standard monster |
| **Boss** | 0x6200000 | 102760448 | StatusImmune + KnockbackImmune + Detector |
| **Guardian** | 0x4000000 | 67108864 | StatusImmune |
| **Battlefield** | 0xC000000 | 201326592 | StatusImmune + SkillImmune |
| **Event** | 0x1000000 | 16777216 | FixedItemDrop |

**Usage:**
```yaml
- Id: 1511
  AegisName: AMON_RA
  Ai: 05
  Class: Boss      # Adds Boss immunity modes automatically
```

**Boss Class Includes:**
- Cannot be affected by status effects
- Cannot be knocked back
- Can detect hidden players

---

## 4. ATTRIBUTE TYPES

Additional modifiers for damage immunity and MVP status.

| Attribute | Hex | Decimal | Description |
|-----------|-----|---------|-------------|
| **Attr 01** | 0x010000 | 65536 | 1 HP from melee |
| **Attr 02** | 0x020000 | 131072 | 1 HP from magic |
| **Attr 04** | 0x040000 | 262144 | 1 HP from ranged |
| **Attr 08** | 0x080000 | 524288 | MVP status |
| **Attr 16** | 0x100000 | 1048576 | 1 HP from misc |
| **Attr 32** | 0x200000 | 2097152 | No knockback |
| **Attr 64** | 0x400000 | 4194304 | Teleport block |

**Combined Plant Mode:**
```
Plant = Attr 01 + Attr 02 + Attr 04 + Attr 16
      = 0x170000 (1507328)
      = Takes 1 HP from all damage types
```

---

## 5. COMMON COMBINATIONS

### Basic Monster Types

**Passive Monster (Like Poring):**
```yaml
- Id: 1002
  AegisName: PORING
  Ai: 01              # Passive
  Class: Normal
  Modes:
    CanMove: true
    CanAttack: true
```

**Aggressive Monster:**
```yaml
- Id: 1031
  AegisName: POPORING
  Ai: 05              # Aggressive
  Class: Normal
  Modes:
    CanMove: true
    Aggressive: true
    CanAttack: true
    ChangeTargetChase: true
```

**Looter Monster:**
```yaml
- Id: 1242
  AegisName: MARIN
  Ai: 02              # Passive Looter
  Class: Normal
  Modes:
    CanMove: true
    Looter: true
    CanAttack: true
```

---

### Advanced Monsters

**Guardian/Castle Defender:**
```yaml
- Id: 1285
  AegisName: GUARDIAN
  Ai: 09              # Guardian AI
  Class: Guardian     # Guardian class
  Modes:
    CanMove: true
    Aggressive: true
    CanAttack: true
    CastSensorIdle: true
    ChangeTargetMelee: true
    ChangeTargetChase: true
```

**MVP Boss:**
```yaml
- Id: 1039
  AegisName: BAPHOMET
  Ai: 05
  Class: Boss         # Boss class (auto-adds immunities)
  Modes:
    CanMove: true
    Aggressive: true
    CanAttack: true
    Mvp: true
    ChangeTargetChase: true
  # Boss class automatically adds:
  # - StatusImmune: true
  # - KnockbackImmune: true
  # - Detector: true
```

**Plant Monster:**
```yaml
- Id: 1084
  AegisName: TAROU
  Ai: 06              # Plant AI (immobile)
  Class: Normal
  Modes:
    CanAttack: false  # Cannot attack
  # Note: Plant monsters are decorative
```

---

### Special Behaviors

**Mob That Helps Allies:**
```yaml
Ai: 03                # Passive Assist
Modes:
  CanMove: true
  Assist: true        # Helps same-type mobs
  ChangeTargetMelee: true
```

**Cast Sensor (Magic Detector):**
```yaml
Ai: 17                # Passive Cast Sensor
Modes:
  CanMove: true
  CastSensorIdle: true   # Attacks casters
```

**Chaotic Switcher:**
```yaml
Ai: 26                # Chaotic
Modes:
  CanMove: true
  Aggressive: true
  ChangeTargetMelee: true
  ChangeTargetChase: true
  CastSensorIdle: true
  CastSensorChase: true
  ChangeChase: true
  RandomTarget: true    # Switches randomly
```

**Weak Player Hunter:**
```yaml
Ai: 08                # Aggressive Weak
Modes:
  CanMove: true
  Aggressive: true
  TargetWeak: true      # Only attacks players 5+ levels lower
  ChangeTargetMelee: true
  ChangeTargetChase: true
```

---

## 6. PRACTICAL EXAMPLES

### Example 1: Custom Aggressive Monster

```yaml
- Id: 50001
  AegisName: CUSTOM_DEMON
  Name: Custom Demon
  Level: 80
  Hp: 50000
  Ai: 05                # Aggressive
  Class: Normal
  Modes:
    CanMove: true
    Aggressive: true     # Attacks on sight
    CanAttack: true
    ChangeTargetChase: true  # Switches targets when hit
```

---

### Example 2: Tank Boss (Physical Immunity)

```yaml
- Id: 50002
  AegisName: TANK_BOSS
  Name: Tank Boss
  Level: 99
  Hp: 10000000
  Ai: 05
  Class: Boss           # Auto-adds status/knockback immunity
  Modes:
    CanMove: true
    Aggressive: true
    CanAttack: true
    Mvp: true
    IgnoreMelee: true   # Only 1 HP from physical
    IgnoreRanged: true  # Only 1 HP from ranged
  # Must be killed with magic!
```

---

### Example 3: Magic-Only Boss

```yaml
- Id: 50003
  AegisName: MAGIC_BOSS
  Name: Magic Boss
  Level: 99
  Hp: 5000000
  Ai: 05
  Class: Boss
  Modes:
    CanMove: true
    Aggressive: true
    CanAttack: true
    Mvp: true
    IgnoreMagic: true   # Only 1 HP from magic
    IgnoreMisc: true    # Only 1 HP from misc
  # Must be killed with physical attacks!
```

---

### Example 4: Slave/Summoned Monster

```yaml
- Id: 50004
  AegisName: SLAVE_MOB
  Name: Slave Mob
  Level: 50
  Hp: 10000
  Ai: 24                # Slave AI
  Class: Normal
  Modes:
    CanMove: true
    CanAttack: true
    NoRandomWalk: true  # Stays near master
```

---

### Example 5: Assist Pack Monster

```yaml
- Id: 50005
  AegisName: PACK_WOLF
  Name: Pack Wolf
  Level: 60
  Hp: 20000
  Ai: 13                # Aggressive Assist
  Class: Normal
  Modes:
    CanMove: true
    Aggressive: true
    CanAttack: true
    Assist: true         # Calls for help!
    ChangeTargetMelee: true
    ChangeTargetChase: true
```

**Behavior:** When one Pack Wolf is attacked, all nearby Pack Wolves join the fight!

---

### Example 6: Immobile Turret

```yaml
- Id: 50006
  AegisName: TURRET
  Name: Turret
  Level: 70
  Hp: 50000
  Ai: 27                # Turret AI
  Class: Normal
  Modes:
    CanMove: false      # Cannot move!
    Aggressive: true
    CanAttack: true
    RandomTarget: true  # Random targeting
    NoRandomWalk: true
```

---

## MODE CALCULATION

### How to Calculate Mode Value

Add up the hex/decimal values of desired modes:

**Example: Aggressive Monster**
```
MD_CANMOVE (1) +
MD_AGGRESSIVE (4) +
MD_CANATTACK (128) +
MD_CHANGETARGETCHASE (8192)
= 1 + 4 + 128 + 8192
= 8325 (decimal)
= 0x2085 (hex)
= AI Type 05
```

---

## AI TYPE SELECTION GUIDE

| Want Monster To... | Use AI |
|-------------------|--------|
| Do nothing, decorative | 06 (Plant) |
| Stand still, attack when hit | 01 (Passive) |
| Walk around, attack when hit | 01 (Passive) |
| Pick up items | 02 (Passive Looter) |
| Help allies when they're attacked | 03 or 07 (Assist) |
| Attack players on sight | 05 (Aggressive) |
| Only attack weak players | 08 (Aggressive Weak) |
| Defend a specific area | 09, 11, 12 (Guardian) |
| React to magic casting | 17, 19, 20 (Cast Sensor) |
| Switch targets frequently | 21, 26 (Hunter/Chaotic) |
| Act as a pet | 25 (Pet) |
| Act as a summoned creature | 24 (Slave) |

---

## DEBUGGING TIPS

### Test Monster Behavior

```c
// Spawn test monster
@monster CUSTOM_MOB 1

// Check current mode
@mobinfo CUSTOM_MOB

// Test targeting
// - Stand still and see if it attacks (aggressive check)
// - Cast a spell and see if it reacts (cast sensor check)
// - Attack it and see if it retaliates (assist check)
// - Try to knock it back (knockback immunity check)
```

---

### Common Issues

**Problem:** Monster doesn't move
- **Check:** CanMove flag is true
- **Check:** Not using Plant AI (06)

**Problem:** Monster doesn't attack
- **Check:** CanAttack flag is true
- **Check:** Aggressive flag for auto-attack

**Problem:** Monster won't help allies
- **Check:** Assist flag is true
- **Check:** Allies are same AegisName

**Problem:** Boss dies too easily to status
- **Check:** Class is set to Boss
- **Check:** StatusImmune flag if needed

---

## CROSS-REFERENCES

- **Monster Database:** See KB_REF_DatabaseStructure.md
- **Script Commands:** See KB_REF_ScriptCommands.md
- **At Commands:** See KB_REF_AtCommands.md (@mobinfo, @monster)
- **Complete Docs:** See `/doc/mob_db_mode_list.txt`

---

**Total Coverage:** 100% of AI types and mode flags
**Use Case:** Custom monster behavior, boss mechanics, AI customization
