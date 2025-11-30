# rAthena YAML Database Schemas
## Complete Database Structure Reference

---

<!-- RAG_CHUNK: yaml_overview_001 -->
## YAML Database Overview

### File Locations
```
db/
├── re/                 # Renewal databases
│   ├── item_db.yml
│   ├── item_db_equip.yml
│   ├── item_db_usable.yml
│   ├── item_db_etc.yml
│   ├── mob_db.yml
│   ├── skill_db.yml
│   └── ...
├── pre-re/             # Pre-Renewal databases
└── import/             # Custom overrides
```

### Import System
Files in `db/import/` override main database entries.

---

<!-- RAG_CHUNK: item_db_001 -->
## Item Database (item_db.yml)

### Basic Structure
```yaml
Body:
  - Id: 501                    # Unique item ID
    AegisName: Red_Potion      # Server-side name (no spaces)
    Name: Red Potion           # Display name
    Type: Healing              # Item type
    Buy: 50                    # Buy price (NPC)
    Sell: 10                   # Sell price
    Weight: 70                 # Weight * 10 (70 = 7.0)
    Script: |
      itemheal rand(45,65),0;
```

### Item Types
```yaml
Type: Healing      # Consumable HP/SP item
Type: Usable       # Usable item
Type: Etc          # Miscellaneous
Type: Weapon       # Weapon
Type: Armor        # Armor/Accessory
Type: Card         # Card
Type: PetEgg       # Pet egg
Type: PetArmor     # Pet equipment
Type: Ammo         # Ammunition
Type: DelayConsume # Delayed consumption
Type: ShadowGear   # Shadow equipment
Type: Cash         # Cash shop item
```

### Equipment Fields
```yaml
Body:
  - Id: 1101
    AegisName: Sword
    Name: Sword
    Type: Weapon
    SubType: 1hSword          # Weapon subtype
    Buy: 100
    Weight: 500
    Attack: 25                # Physical ATK
    MagicAttack: 0            # MATK (Renewal)
    Range: 1                  # Attack range
    Slots: 3                  # Card slots
    Jobs:                     # Equippable jobs
      Novice: true
      Swordman: true
      Knight: true
    Classes:                  # Equippable classes
      Normal: true
      Upper: true
      Baby: true
    Gender: Both              # Both/Male/Female
    Locations:
      Right_Hand: true        # Equipment location
    WeaponLevel: 1            # Weapon level 1-5
    EquipLevelMin: 2          # Minimum level to equip
    EquipLevelMax: 99         # Maximum level
    Refineable: true          # Can be refined
    View: 1                   # View/sprite ID
    Script: |
      bonus bStr,2;
    EquipScript: |
      sc_start SC_BLESSING,60000,5;
    UnEquipScript: |
      sc_end SC_BLESSING;
```

### Equipment Locations
```yaml
Locations:
  Head_Top: true
  Head_Mid: true
  Head_Low: true
  Armor: true
  Right_Hand: true
  Left_Hand: true
  Garment: true
  Shoes: true
  Right_Accessory: true
  Left_Accessory: true
  Both_Accessory: true
  Both_Hand: true
  Shadow_Armor: true
  Shadow_Weapon: true
  Shadow_Shield: true
  Shadow_Shoes: true
  Shadow_Right_Accessory: true
  Shadow_Left_Accessory: true
```

### Weapon SubTypes
```yaml
SubType: Fist / Dagger / 1hSword / 2hSword / 1hSpear / 2hSpear
SubType: 1hAxe / 2hAxe / Mace / 2hMace / Staff / Bow
SubType: Knuckle / Musical / Whip / Book / Katar
SubType: Revolver / Rifle / Gatling / Shotgun / Grenade
SubType: Huuma / 2hStaff
```

---

<!-- RAG_CHUNK: mob_db_001 -->
## Monster Database (mob_db.yml)

### Basic Structure
```yaml
Body:
  - Id: 1002
    AegisName: PORING
    Name: Poring
    JapaneseName: Poring
    Level: 1
    Hp: 50
    Sp: 0
    BaseExp: 2
    JobExp: 1
    MvpExp: 0
    Attack: 7
    Attack2: 10
    Defense: 0
    MagicDefense: 5
    Str: 1
    Agi: 1
    Vit: 1
    Int: 0
    Dex: 6
    Luk: 30
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
    DamageTaken: 100
```

### AI Modes
```yaml
Ai: 01   # Passive
Ai: 02   # Passive, looter
Ai: 03   # Aggressive, chase
Ai: 04   # Aggressive, chase, cast on player
Ai: 05   # Aggressive, chase, change target
Ai: 06   # Aggressive, chase, attack nearby
Ai: 07   # Aggressive, random walk
Ai: 09   # Aggressive, chase, KS, change target
Ai: 10   # Aggressive, immobile
Ai: 17   # Passive, random walk
Ai: 20   # Passive, immobile
Ai: 21   # Aggressive (boss type)
```

### Monster Modes
```yaml
Modes:
  CanMove: true
  Looter: true
  Aggressive: true
  Assist: true
  CastSensorIdle: true
  Boss: true
  Plant: true
  CanAttack: true
  Detector: true
  CastSensorChase: true
  ChangeChase: true
  Angry: true
  ChangeTargetMelee: true
  ChangeTargetChase: true
  TargetWeak: true
  NoKnockback: true
  RandomTarget: true
  IgnoreMagic: true
  IgnoreMelee: true
  IgnoreMisc: true
  IgnoreRanged: true
  Mvp: true
  StatusImmune: true
  SkillImmune: true
  FixedItemDrop: true
  Detector: true
  TeleportBlock: true
```

### Drops
```yaml
Drops:
  - Item: Apple
    Rate: 7000           # 70.00%
  - Item: Empty_Bottle
    Rate: 1000           # 10.00%
  - Item: Poring_Card
    Rate: 1              # 0.01%
    StealProtected: true # Cannot be stolen

MvpDrops:
  - Item: Yggdrasilberry
    Rate: 5500
```

### Monster Skills
```yaml
Skills:
  - Name: NPC_EMOTION
    Level: 1
    State: Idle
    Rate: 2000
    CastTime: 0
    Delay: 5000
    Cancelable: false
    Target: Self
    Condition: always
```

---

<!-- RAG_CHUNK: skill_db_001 -->
## Skill Database (skill_db.yml)

### Basic Structure
```yaml
Body:
  - Id: 1
    Name: NV_BASIC
    Description: Basic Skill
    MaxLevel: 9
    Type: None
    TargetType: Passive
```

### Skill Types
```yaml
Type: None         # No type
Type: Weapon       # Physical attack
Type: Magic        # Magical attack
Type: Misc         # Misc attack
```

### Target Types
```yaml
TargetType: Passive    # Passive skill
TargetType: Attack     # Offensive, target required
TargetType: Ground     # Ground-targeted
TargetType: Self       # Self-targeted
TargetType: Support    # Support, target ally
TargetType: Trap       # Trap skill
```

### Skill Flags
```yaml
Flags:
  AllowOnMado: true
  AllowOnWarg: true
  AllowWhenHidden: true
  CanTargetSelf: true
  IgnoreAutoGuard: true
  IgnoreCicada: true
  IgnoreLandProtector: true
  NoCastSelf: true
  NoEnemy: true
  NoFootSet: true
  NoTargetSelf: true
  Picky: true
  Song: true
  Ensemble: true
  Trap: true
  TargetEmperium: true
  TargetSelf: true
  IgnoreKagehumi: true
  IsCombo: true
  AllowReproduce: true
  ShowScale: true
```

### Cast/Cooldown
```yaml
CastTime:           # Variable cast time
  - Level: 1
    Time: 1000
  - Level: 5
    Time: 2500
FixedCastTime: 500  # Fixed cast time
AfterCastActDelay: 1000  # Global cooldown
Cooldown: 5000      # Skill-specific cooldown
```

### Requirements
```yaml
Requires:
  HpCost:
    - Level: 1
      Amount: 5
  SpCost:
    - Level: 1
      Amount: 10
  ItemCost:
    - Item: Red_Gemstone
      Amount: 1
  Weapon:
    Dagger: true
    1hSword: true
  State: Hiding
```

---

<!-- RAG_CHUNK: quest_db_001 -->
## Quest Database (quest_db.yml)

### Basic Structure
```yaml
Body:
  - Id: 1000
    Title: Newbie Quest
    TimeLimit: 86400    # Seconds (24 hours)
    Targets:
      - Mob: PORING
        Count: 10
    Drops:
      - Mob: PORING
        Item: Apple
        Count: 5
        Rate: 5000      # 50%
```

---

<!-- RAG_CHUNK: instance_db_001 -->
## Instance Database (instance_db.yml)

### Basic Structure
```yaml
Body:
  - Id: 1
    Name: Endless Tower
    TimeLimit: 14400          # 4 hours
    IdleTimeOut: 300          # 5 min idle timeout
    Enter:
      Map: 1@tower
      X: 50
      Y: 50
    AdditionalMaps:
      2@tower: true
      3@tower: true
```

---

<!-- RAG_CHUNK: achievement_db_001 -->
## Achievement Database

### Basic Structure
```yaml
Body:
  - Id: 100000
    Group: Adventure
    Name: First Steps
    Targets:
      - Id: 1
        Mob: PORING
        Count: 1
    Rewards:
      - Item: Apple
        Amount: 10
      TitleId: 1000
    Score: 10
```

---

<!-- RAG_CHUNK: status_db_001 -->
## Status Database (status_db.yml)

### Status Configuration
```yaml
Body:
  - Status: Poison
    Icon: EFST_POISON
    DurationLookup: NPC_POISON
    CalcFlags:
      Regen: true
    StateFlags:
      SendOption: true
    EndOnStart:
      Hiding: true
    Fail:
      Boss: true
```

---

#rathena #yaml #database #item #mob #skill #quest #instance #schema
