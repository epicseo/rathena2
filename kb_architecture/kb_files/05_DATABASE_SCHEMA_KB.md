---
title: rAthena Database Schema Reference
type: database_reference
category: rathena_admin
tags: [database, yml, yaml, schema, item_db, skill_db, mob_db]
version: 2.0
mode: DEV
secondary_modes: [SCRIPTING]
chunk_strategy: BY_SECTION
---

# rAthena Database Schema Reference

This KB provides YAML schema documentation for all major rAthena databases.

**Location:** Database files are in `db/re/` (Renewal) and `db/pre-re/` (Pre-Renewal).

---

# Item Database (item_db_*.yml)

## Header
```yaml
Header:
  Type: ITEM_DB
  Version: 3
```

## Required Fields
| Field | Type | Description |
|-------|------|-------------|
| Id | Integer | Unique item ID |
| AegisName | String | Server reference name (no spaces) |
| Name | String | Display name |

## Optional Fields

### Basic Properties
| Field | Type | Default | Description |
|-------|------|---------|-------------|
| Type | String | Etc | Item type (see below) |
| SubType | String | 0 | Weapon/Ammo/Card type |
| Buy | Integer | 2x Sell | Buying price |
| Sell | Integer | 0.5x Buy | Selling price |
| Weight | Integer | 0 | Weight (10 = 1.0) |
| Attack | Integer | 0 | Weapon attack |
| MagicAttack | Integer | 0 | Weapon magic attack |
| Defense | Integer | 0 | Armor defense |
| Range | Integer | 0 | Weapon range |
| Slots | Integer | 0 | Card slots |

### Type Values
```
Healing, Usable, Etc, Armor, Weapon, Card, PetEgg,
PetArmor, Ammo, DelayConsume, ShadowGear, Cash
```

### SubType Values (Weapons)
```
Fist, Dagger, 1hSword, 2hSword, 1hSpear, 2hSpear,
1hAxe, 2hAxe, Mace, 2hMace, Staff, Bow, Knuckle,
Musical, Whip, Book, Katar, Revolver, Rifle,
Gatling, Shotgun, Grenade, Huuma, 2hStaff
```

### Equip Properties
| Field | Type | Description |
|-------|------|-------------|
| Jobs | Map | Jobs that can equip |
| Classes | Map | Upper class types |
| Gender | String | Gender restriction (Male/Female/Both) |
| Locations | Map | Equipment placement |
| WeaponLevel | Integer | Weapon level (1-5) |
| ArmorLevel | Integer | Armor level (1-2) |
| EquipLevelMin | Integer | Minimum equip level |
| EquipLevelMax | Integer | Maximum equip level |
| Refineable | Boolean | Can be refined |
| Gradable | Boolean | Can be graded |
| View | Integer | View sprite ID |

### Locations Values
```yaml
Locations:
  Head_Top: true       # Upper headgear
  Head_Mid: true       # Middle headgear
  Head_Low: true       # Lower headgear
  Armor: true          # Body armor
  Right_Hand: true     # Weapon hand
  Left_Hand: true      # Shield hand
  Garment: true        # Garment slot
  Shoes: true          # Footgear
  Right_Accessory: true
  Left_Accessory: true
  Costume_Head_Top: true
  Costume_Head_Mid: true
  Costume_Head_Low: true
  Costume_Garment: true
  Ammo: true
  Shadow_Armor: true
  Shadow_Weapon: true
  Shadow_Shield: true
  Shadow_Shoes: true
  Shadow_Right_Accessory: true
  Shadow_Left_Accessory: true
```

### Flags
```yaml
Flags:
  BuyingStore: false    # Can be put in buying store
  DeadBranch: false     # Is a dead branch
  Container: false      # Part of container
  UniqueId: false       # Unique stack
  BindOnEquip: false    # Binds when equipped
  DropAnnounce: false   # Announce on drop
  NoConsume: false      # Not consumed on use
  DropEffect: None      # Ground effect (None/Client/White/Blue/Yellow/Purple/Orange/Green)
```

### Trade Restrictions
```yaml
Trade:
  Override: 100         # Group level to bypass
  NoDrop: false
  NoTrade: false
  TradePartner: false
  NoSell: false
  NoCart: false
  NoStorage: false
  NoGuildStorage: false
  NoMail: false
  NoAuction: false
```

### Stack Limits
```yaml
Stack:
  Amount: 100           # Max stack
  Inventory: true
  Cart: false
  Storage: false
  GuildStorage: false
```

### Scripts
```yaml
Script: |
  bonus bStr,5;
  bonus bAgi,3;

EquipScript: |
  sc_start SC_BLESSING,60000,10;

UnEquipScript: |
  sc_end SC_BLESSING;
```

## Example Entry
```yaml
  - Id: 1101
    AegisName: Sword
    Name: Sword
    Type: Weapon
    SubType: 1hSword
    Buy: 100
    Weight: 500
    Attack: 25
    Range: 1
    Slots: 3
    Jobs:
      Swordman: true
      Knight: true
      Crusader: true
    Locations:
      Right_Hand: true
    WeaponLevel: 1
    Refineable: true
```

---

# Skill Database (skill_db.yml)

## Header
```yaml
Header:
  Type: SKILL_DB
  Version: 4
```

## Required Fields
| Field | Type | Description |
|-------|------|-------------|
| Id | Integer | Unique skill ID |
| Name | String | Skill aegis name |
| Description | String | Skill description |
| MaxLevel | Integer | Maximum skill level |

## Skill Properties

### Basic Properties
| Field | Type | Description |
|-------|------|-------------|
| Type | String | Skill type (None/Weapon/Magic/Misc) |
| TargetType | String | Target type (Passive/Attack/Ground/Self/Support/Trap) |
| Hit | String | Hit type (Normal/Single/Multi) |

### Level-Based Values
```yaml
Range:
  - Level: 1
    Size: 2
  - Level: 5
    Size: 4

HitCount:
  - Level: 1
    Count: 1
  - Level: 5
    Count: 5

Element:
  - Level: 1
    Element: Fire
  - Level: 5
    Element: Fire
```

### Timing (in milliseconds)
```yaml
CastTime:
  - Level: 1
    Time: 1000
  - Level: 5
    Time: 3000

AfterCastActDelay:
  - Level: 1
    Time: 500

AfterCastWalkDelay:
  - Level: 1
    Time: 300

Duration1:
  - Level: 1
    Time: 10000

Duration2:
  - Level: 1
    Time: 5000

Cooldown:
  - Level: 1
    Time: 5000

FixedCastTime:
  - Level: 1
    Time: 500
```

### Requirements
```yaml
Requires:
  HpCost:
    - Level: 1
      Amount: 10
  SpCost:
    - Level: 1
      Amount: 20
  ApCost:
    - Level: 1
      Amount: 5
  ZenyCost:
    - Level: 1
      Amount: 100
  Weapon: Sword         # Required weapon type
  Ammo: Arrow           # Required ammo type
  AmmoAmount:
    - Level: 1
      Amount: 1
  State: Hiding         # Required state
  Status: SC_HIDING     # Required status
  SpiritSphereCost:
    - Level: 1
      Amount: 1
  ItemCost:
    - Item: Red_Gemstone
      Amount: 1
  Equipment:
    - Shield
```

### Skill Unit (Ground skills)
```yaml
Unit:
  Id: UNT_FIREWALL
  AlternateId: UNT_FIREWALL2
  Layout:
    - Level: 1
      Size: 1
  Range:
    - Level: 1
      Size: 1
  Interval: 200
  Target: Enemy          # All/Friend/Party/Guild/Ally/Enemy
  Flag:
    - NoEnemy
    - NoReiteration
```

### Damage Flags
```yaml
DamageFlags:
  NoDamage: true        # No damage dealt
  Splash: true          # Splash damage
  SplashSplit: true     # Split splash damage
  IgnoreAtkCard: true   # Ignore ATK cards
  IgnoreElement: true   # Ignore element
  IgnoreDefense: true   # Ignore defense
  IgnoreFlee: true      # Ignore flee
  IgnoreDefCard: true   # Ignore DEF cards
  Critical: true        # Can critical
```

### Flags
```yaml
Flags:
  IsQuest: true         # Quest skill
  IsNpc: true           # NPC skill only
  IsWedding: true       # Wedding skill
  IsSpirit: true        # Spirit skill
  IsGuild: true         # Guild skill
  IsSong: true          # Bard/Dancer song
  IsEnsemble: true      # Ensemble skill
  IsTrap: true          # Trap skill
  TargetSelf: true      # Always self-target
  NoTargetSelf: true    # Never self-target
  PartyOnly: true       # Party members only
  GuildOnly: true       # Guild members only
  NoEnemy: true         # Can't target enemy
  IgnoreLandProtector: true
  AllowWhenHidden: true
  AllowWhenPerforming: true
  TargetEmperium: true
  IgnoreStasis: true
  IgnoreKagehumi: true
  AlterRangeVulture: true
  AlterRangeSnakeEye: true
  AlterRangeShadowJump: true
  AlterRangeRadius: true
  AlterRangeResearchTrap: true
  IgnoreHovering: true
  AllowOnWarp: true
  AllowOnMado: true
  TargetManHole: true
  TargetHidden: true
  IncreaseDanceWithWugDamage: true
  IgnoreWugBite: true
  IgnoreAutoGuard: true
  IgnoreCicada: true
  ShowScale: true
```

## Example Entry
```yaml
  - Id: 5
    Name: SM_BASH
    Description: Bash
    MaxLevel: 10
    Type: Weapon
    TargetType: Attack
    Range: 1
    Hit: Single
    HitCount:
      - Level: 1
        Count: 1
    DamageFlags:
      Splash: false
    CastTime:
      - Level: 1
        Time: 0
    AfterCastActDelay:
      - Level: 1
        Time: 500
    Requires:
      SpCost:
        - Level: 1
          Amount: 8
        - Level: 5
          Amount: 14
        - Level: 10
          Amount: 15
```

---

# Monster Database (mob_db.yml)

## Header
```yaml
Header:
  Type: MOB_DB
  Version: 4
```

## Required Fields
| Field | Type | Description |
|-------|------|-------------|
| Id | Integer | Unique monster ID |
| AegisName | String | Server reference name |
| Name | String | Display name (kRO) |
| JapaneseName | String | Alternative name (jRO) |

## Stats
| Field | Type | Description |
|-------|------|-------------|
| Level | Integer | Monster level |
| Hp | Integer | Max HP |
| Sp | Integer | Max SP |
| BaseExp | Integer | Base EXP reward |
| JobExp | Integer | Job EXP reward |
| MvpExp | Integer | MVP EXP bonus |
| Attack | Integer | Minimum ATK |
| Attack2 | Integer | Maximum ATK |
| Defense | Integer | DEF |
| MagicDefense | Integer | MDEF |
| Resistance | Integer | RES |
| MagicResistance | Integer | MRES |
| Str | Integer | STR stat |
| Agi | Integer | AGI stat |
| Vit | Integer | VIT stat |
| Int | Integer | INT stat |
| Dex | Integer | DEX stat |
| Luk | Integer | LUK stat |

## Properties
| Field | Type | Description |
|-------|------|-------------|
| AttackRange | Integer | Attack range |
| SkillRange | Integer | Skill cast range |
| ChaseRange | Integer | Chase range |
| Size | String | Small/Medium/Large |
| Race | String | Monster race |
| RaceGroups | Map | Monster race groups |
| Element | String | Element type |
| ElementLevel | Integer | Element level (1-4) |
| WalkSpeed | Integer | Movement speed |
| AttackDelay | Integer | Attack animation time |
| AttackMotion | Integer | Attack motion |
| ClientAttackMotion | Integer | Client attack motion |
| DamageMotion | Integer | Damage motion |
| DamageTaken | Integer | Damage taken % (100 = normal) |

### AI Behavior
```yaml
Ai: 01                  # AI type (00-27)
Class: Normal           # Normal/Boss/Guardian
```

### Mode Flags
```yaml
Modes:
  CanMove: true
  Looter: false
  Aggressive: true
  Assist: true
  CastSensorIdle: false
  Boss: false
  Plant: false
  CanAttack: true
  Detector: false
  CastSensorChase: false
  ChangeChase: true
  Angry: true
  ChangeTargetMelee: true
  ChangeTargetChase: true
  TargetWeak: false
  NoKnockback: false
  RandomTarget: false
  IgnoreMelee: false
  IgnoreMagic: false
  IgnoreRanged: false
  Mvp: false
  IgnoreMisc: false
  KnockBackImmune: false
  TeleportBlock: false
  FixedItemDrop: false
  DetectorInsight: false
  StatusImmune: false
  SkillImmune: false
```

### Drops
```yaml
Drops:
  - Item: Red_Potion
    Rate: 5000           # 10000 = 100%
    StealProtected: false
    RandomOptionGroup: MyGroup
  - Item: Sword
    Rate: 100
    Index: 0             # Specific drop slot

MvpDrops:
  - Item: Old_Card_Album
    Rate: 5000
  - Item: Yggdrasilberry
    Rate: 2500
```

## Example Entry
```yaml
  - Id: 1002
    AegisName: PORING
    Name: Poring
    JapaneseName: Poring
    Level: 1
    Hp: 55
    BaseExp: 27
    JobExp: 20
    Attack: 8
    Attack2: 11
    Defense: 2
    Str: 1
    Agi: 1
    Vit: 1
    Int: 0
    Dex: 6
    Luk: 5
    AttackRange: 1
    SkillRange: 10
    ChaseRange: 12
    Size: Medium
    Race: Plant
    Element: Water
    ElementLevel: 1
    WalkSpeed: 400
    AttackDelay: 1872
    AttackMotion: 672
    DamageMotion: 480
    Ai: 01
    Drops:
      - Item: Jellopy
        Rate: 7000
      - Item: Knife_
        Rate: 100
      - Item: Sticky_Mucus
        Rate: 400
      - Item: Apple
        Rate: 1000
      - Item: Empty_Bottle
        Rate: 1500
      - Item: Poring_Card
        Rate: 1
```

---

# Quest Database (quest_db.yml)

## Header
```yaml
Header:
  Type: QUEST_DB
  Version: 2
```

## Fields
| Field | Type | Description |
|-------|------|-------------|
| Id | Integer | Quest ID |
| Title | String | Quest title |
| TimeLimit | String | Time limit (e.g., "2h", "1d") |

### Targets (Kill objectives)
```yaml
Targets:
  - Mob: PORING
    Count: 10
    MinLevel: 1
    MaxLevel: 99
    Location: prontera
    MapName: Prontera
```

### Drops (Item collection)
```yaml
Drops:
  - Mob: PORING
    Item: Jellopy
    Count: 5
    Rate: 5000           # 10000 = 100%
```

## Example Entry
```yaml
  - Id: 1000
    Title: Poring Hunt
    TimeLimit: 1d
    Targets:
      - Mob: PORING
        Count: 10
    Drops:
      - Mob: PORING
        Item: Jellopy
        Count: 5
        Rate: 10000
```

---

# Item Group Database (item_group_db.yml)

## Header
```yaml
Header:
  Type: ITEM_GROUP_DB
  Version: 1
```

## Fields
```yaml
  - Group: Blue_Box
    SubGroups:
      - SubGroup: 0       # Default group
        List:
          - Item: Sword
            Rate: 100     # Weight for random selection
            Amount: 1
            Random: 1     # Random amount 1 to Amount
            Announced: false
            Duration: 0   # Rental duration (minutes)
            GUID: false   # Unique ID
            Bound: None   # Bound type
            Named: false  # Character name prefix
```

### Bound Types
```
None, Account, Guild, Party, Character
```

## Example Entry
```yaml
  - Group: Blue_Box
    SubGroups:
      - SubGroup: 0
        List:
          - Item: Old_Card_Album
            Rate: 10
          - Item: Yggdrasilberry
            Rate: 50
            Amount: 3
          - Item: Elunium
            Rate: 100
            Amount: 5
```

---

# Instance Database (instance_db.yml)

## Header
```yaml
Header:
  Type: INSTANCE_DB
  Version: 1
```

## Fields
| Field | Type | Description |
|-------|------|-------------|
| Id | Integer | Instance ID |
| Name | String | Instance name |
| TimeLimit | Integer | Time limit (seconds) |
| IdleTimeOut | Integer | Idle timeout (seconds) |
| Enter | Map | Entry map info |
| AdditionalMaps | List | Extra map list |

## Example Entry
```yaml
  - Id: 1
    Name: Endless Tower
    TimeLimit: 14400
    IdleTimeOut: 300
    Enter:
      Map: 1@tower
      X: 50
      Y: 50
    AdditionalMaps:
      - Map: 2@tower
      - Map: 3@tower
```

---

*KB Version 2.0 | Mode: DEV | Source: db/re/*.yml headers, doc/*_db.txt*
