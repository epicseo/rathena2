# rAthena KB v5 - Database Systems Reference

**Version:** 5.0 Enhanced
**Generated:** 2025-11-26
**Coverage:** item_db.yml, skill_db.yml, mob_db.yml, quest_db.yml

---

## Quick Navigation

- [item_db.yml Schema](#item_dbyml-schema)
- [skill_db.yml Schema](#skill_dbyml-schema)  
- [mob_db.yml Schema](#mob_dbyml-schema)
- [quest_db.yml Schema](#quest_dbyml-schema)
- [item_group_db.yml Schema](#item_group_dbyml-schema)

---

## item_db.yml Schema

<!-- RAG_CHUNK: item_db_schema -->

### Complete Field Reference

```yaml
Header:
  Type: ITEM_DB
  Version: 3

Body:
  - Id: 501                    # Item ID (required)
    AegisName: "Red_Potion"    # Server-side name (required, unique)
    Name: "Red Potion"         # Display name (required)
    Type: Healing              # Item type (see types below)
    SubType: None              # Weapon/Ammo subtype
    Buy: 50                    # Buy price (NPC)
    Sell: 10                   # Sell price (to NPC)
    Weight: 70                 # Weight (1 = 0.1)
    Attack: 0                  # Weapon ATK
    MagicAttack: 0             # Weapon MATK
    Defense: 0                 # Armor DEF
    Range: 0                   # Weapon range
    Slots: 0                   # Card slots
    Jobs:                      # Equippable jobs
      All: true
      Novice: false
    Classes:                   # Equippable classes
      All: true
    Gender: Both               # Male/Female/Both
    Locations:                 # Equipment location
      Right_Hand: true
    WeaponLevel: 1             # Weapon level 1-5
    ArmorLevel: 1              # Armor level 1-2
    EquipLevelMin: 1           # Min equip level
    EquipLevelMax: 0           # Max equip level (0=no max)
    Refineable: true           # Can be refined
    Gradable: false            # Can be graded
    View: 0                    # Sprite view ID
    AliasName: "Red_Potion"    # Alias for client
    Flags:                     # Special flags
      BuyingStore: true
      DeadBranch: false
      Container: false
      UniqueId: false
      BindOnEquip: false
      DropAnnounce: false
      NoConsume: false
      DropEffect: None
    Delay:                     # Use delay
      Duration: 0
      Status: None
    Stack:                     # Stack settings
      Amount: 0
      Inventory: true
      Cart: true
      Storage: true
      GuildStorage: true
    NoUse:                     # Use restrictions
      Override: 0
      Sitting: false
    Trade:                     # Trade restrictions
      Override: 0
      NoDrop: false
      NoTrade: false
      TradePartner: false
      NoSell: false
      NoCart: false
      NoStorage: false
      NoGuildStorage: false
      NoMail: false
      NoAuction: false
    Script: |                  # On-use/equip script
      itemheal 45,0;
    EquipScript: |             # On-equip script
      bonus bStr,1;
    UnEquipScript: |           # On-unequip script
      # script here
```

### Item Types
| Type | Description |
|------|-------------|
| Healing | Consumable healing items |
| Usable | Usable items (non-healing) |
| Etc | Misc items, materials |
| Armor | All equipment except weapons |
| Weapon | Weapons |
| Card | Cards |
| PetEgg | Pet eggs |
| PetArmor | Pet equipment |
| Ammo | Ammunition |
| DelayConsume | Delayed consumption items |
| ShadowGear | Shadow equipment |
| Cash | Cash shop items |

### Weapon SubTypes
| SubType | Description |
|---------|-------------|
| Fist | Bare hands |
| Dagger | Daggers |
| 1hSword | One-handed swords |
| 2hSword | Two-handed swords |
| 1hSpear | One-handed spears |
| 2hSpear | Two-handed spears |
| 1hAxe | One-handed axes |
| 2hAxe | Two-handed axes |
| Mace | Maces |
| 2hMace | Two-handed maces |
| Staff | Staves |
| Bow | Bows |
| Knuckle | Knuckles |
| Musical | Musical instruments |
| Whip | Whips |
| Book | Books |
| Katar | Katars |
| Revolver | Revolvers |
| Rifle | Rifles |
| Gatling | Gatling guns |
| Shotgun | Shotguns |
| Grenade | Grenade launchers |
| Huuma | Huuma shurikens |
| 2hStaff | Two-handed staves |

### Equipment Locations
| Location | Slot |
|----------|------|
| Head_Top | Upper headgear |
| Head_Mid | Middle headgear |
| Head_Low | Lower headgear |
| Armor | Body armor |
| Right_Hand | Weapon (right) |
| Left_Hand | Shield (left) |
| Garment | Garment/Cape |
| Shoes | Footgear |
| Right_Accessory | Accessory 1 |
| Left_Accessory | Accessory 2 |
| Both_Hand | Two-handed weapon |
| Both_Accessory | Both accessories |

---

## skill_db.yml Schema

<!-- RAG_CHUNK: skill_db_schema -->

### Complete Field Reference

```yaml
Header:
  Type: SKILL_DB
  Version: 3

Body:
  - Id: 1                      # Skill ID (required)
    Name: "NV_BASIC"           # Skill constant name (required)
    Description: "Basic Skill" # Display name
    MaxLevel: 9                # Maximum skill level
    Type: None                 # Skill type (see below)
    TargetType: Self           # Target type (see below)
    DamageFlags:               # Damage properties
      Splash: false
      SplashSplit: false
      IgnoreAtkCard: false
      IgnoreElement: false
      IgnoreDefense: false
      IgnoreFlee: false
      IgnoreDefCard: false
      Critical: false
      NoDamage: false
    Flags:                     # Skill flags
      IsQuest: false
      IsNpc: false
      IsWedding: false
      IsSpirit: false
      IsGuild: false
      IsSong: false
      IsEnsemble: false
      IsTrap: false
      TargetSelf: false
      NoTargetSelf: false
      PartyOnly: false
      GuildOnly: false
      NoEnemy: false
      IsAutoShadowSpell: false
      IsChorus: false
      IgnoreBgReduction: false
      IgnoreGvgReduction: false
      DisableNearNpc: false
      TargetTrap: false
      IgnoreLandProtector: false
      AllowWhenHidden: false
      AllowWhenPerforming: false
      TargetEmperium: false
      IgnoreStasis: false
      IgnoreKagehumi: false
      AlterRangeVulture: false
      AlterRangeSnakeEye: false
      AlterRangeShadowJump: false
      AlterRangeRadius: false
      AlterRangeResearchTrap: false
      IgnoreHovering: false
      AllowOnWarg: false
      AllowOnMado: false
      TargetManHole: false
      TargetHidden: false
      IncreaseGloomyDayDamage: false
      IncreaseHallucinationDamage: false
      EnableMagicDamage: false
      IgnoreGtb: false
      IgnoreWallOfFog: false
    Range:                     # Skill range per level
      - Level: 1
        Size: 0
    Hit: None                  # Hit type
    HitCount:                  # Number of hits
      - Level: 1
        Count: 0
    Element:                   # Element per level
      - Level: 1
        Element: Neutral
    SplashArea:                # Splash area
      - Level: 1
        Area: 0
    ActiveInstance:            # Active instances
      - Level: 1
        Max: 0
    Knockback:                 # Knockback cells
      - Level: 1
        Amount: 0
    GiveAp:                    # AP gained
      - Level: 1
        Amount: 0
    CopyFlags:                 # Plagiarism settings
      Skill:
        Plagiarism: false
        Reproduce: false
      RemoveRequirement:
        HpCost: false
        SpCost: false
        HpRateCost: false
        SpRateCost: false
        ApCost: false
        MaxHpTrigger: false
        ZenyCost: false
        Weapon: false
        Ammo: false
        State: false
        Status: false
        SpiritSphereCost: false
        ItemCost: false
        Equipment: false
    NoNearNpc:                 # NPC proximity restrictions
      Type: None
      AdditionalRange: 0
    CastCancel: false          # Cast can be cancelled
    CastDefenseReduction: 0    # DEF reduction during cast
    CastTime:                  # Cast time per level (ms)
      - Level: 1
        Time: 0
    AfterCastActDelay:         # After-cast delay
      - Level: 1
        Time: 0
    AfterCastWalkDelay:        # Walk delay after cast
      - Level: 1
        Time: 0
    Duration1:                 # Duration 1
      - Level: 1
        Time: 0
    Duration2:                 # Duration 2
      - Level: 1
        Time: 0
    Cooldown:                  # Cooldown per level
      - Level: 1
        Time: 0
    FixedCastTime:             # Fixed cast time
      - Level: 1
        Time: 0
    CastTimeFlags:             # Cast time modifiers
      IgnoreDex: false
      IgnoreStatus: false
      IgnoreItemBonus: false
    CastDelayFlags:            # Delay modifiers
      IgnoreDex: false
      IgnoreStatus: false
      IgnoreItemBonus: false
    Requires:                  # Skill requirements
      HpCost:                  # HP cost per level
        - Level: 1
          Amount: 0
      SpCost:                  # SP cost per level
        - Level: 1
          Amount: 0
      ApCost:                  # AP cost
        - Level: 1
          Amount: 0
      HpRateCost:              # HP % cost
        - Level: 1
          Amount: 0
      SpRateCost:              # SP % cost
        - Level: 1
          Amount: 0
      MaxHpTrigger:            # Max HP trigger
        - Level: 1
          Amount: 0
      ZenyCost:                # Zeny cost
        - Level: 1
          Amount: 0
      Weapon:                  # Required weapon
        All: true
      Ammo:                    # Required ammo
        None: true
      AmmoAmount:              # Ammo amount
        - Level: 1
          Amount: 0
      State: None              # Required state
      Status:                  # Required status
        None: true
      SpiritSphereCost:        # Spirit sphere cost
        - Level: 1
          Amount: 0
      ItemCost:                # Item cost
        - Item: Red_Gemstone
          Amount: 1
      Equipment:               # Required equipment
        None: true
    Unit:                      # Ground unit settings
      Id: None
      AlternateId: None
      Layout:
        - Level: 1
          Size: 0
      Range:
        - Level: 1
          Size: 0
      Interval: 0
      Target: All
      Flag:
        UF_DEFNOTENEMY: false
        UF_NOREITERATION: false
        UF_NOFOOTSET: false
        UF_NOOVERLAP: false
        UF_PATHCHECK: false
        UF_NOPC: false
        UF_NOMOB: false
        UF_SKILL: false
        UF_DANCE: false
        UF_ENSEMBLE: false
        UF_SONG: false
        UF_DUALMODE: false
        UF_RANGEDSINGLEUNIT: false
```

### Skill Types
| Type | Description |
|------|-------------|
| None | No type (passive) |
| Weapon | Physical attack |
| Magic | Magic attack |
| Misc | Misc damage |

### Target Types
| TargetType | Description |
|------------|-------------|
| Passive | Passive skill |
| Attack | Offensive targetable |
| Ground | Ground target |
| Self | Self only |
| Support | Support (party/ally) |
| Trap | Trap placement |

---

## mob_db.yml Schema

<!-- RAG_CHUNK: mob_db_schema -->

### Complete Field Reference

```yaml
Header:
  Type: MOB_DB
  Version: 3

Body:
  - Id: 1002                   # Monster ID (required)
    AegisName: "PORING"        # Server-side name (required)
    Name: "Poring"             # Display name
    JapaneseName: "Poring"     # Original name
    Level: 1                   # Monster level
    Hp: 50                     # HP
    Sp: 0                      # SP
    BaseExp: 2                 # Base EXP
    JobExp: 1                  # Job EXP
    MvpExp: 0                  # MVP EXP (bosses only)
    Attack: 7                  # Minimum ATK
    Attack2: 10                # Maximum ATK
    Defense: 0                 # DEF
    MagicDefense: 5            # MDEF
    Str: 1                     # STR stat
    Agi: 1                     # AGI stat
    Vit: 1                     # VIT stat
    Int: 0                     # INT stat
    Dex: 6                     # DEX stat
    Luk: 30                    # LUK stat
    AttackRange: 1             # Attack range
    SkillRange: 10             # Skill range
    ChaseRange: 12             # Chase range
    Size: Small                # Small/Medium/Large
    Race: Plant                # Race type
    RaceGroups:                # Race group flags
      Goblin: false
      Kobold: false
    Element: Water             # Element type
    ElementLevel: 1            # Element level (1-4)
    WalkSpeed: 400             # Walk speed
    AttackDelay: 1872          # Attack delay (ms)
    AttackMotion: 672          # Attack motion
    DamageMotion: 480          # Damage motion
    DamageTaken: 100           # Damage modifier %
    Ai: 02                     # AI type
    Class: Normal              # Normal/Boss/Guardian
    Modes:                     # Behavior modes
      CanMove: true
      Looter: true
      Aggressive: false
      Assist: false
      CastSensorIdle: false
      Boss: false
      Plant: false
      CanAttack: true
      Detector: false
      CastSensorChase: false
      ChangeChase: false
      Angry: false
      ChangeTargetMelee: false
      ChangeTargetChase: false
      TargetWeak: false
      NoKnockback: false
      TeleportBlock: false
      FixedItemDrop: false
      Detector: false
      StatusImmune: false
      SkillImmune: false
    MvpDrops:                  # MVP drops
      - Item: Old_Card_Album
        Rate: 5000
        StealProtected: true
    Drops:                     # Normal drops
      - Item: Jellopy
        Rate: 7000
        StealProtected: false
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

### Monster Races
| Race | Description |
|------|-------------|
| Formless | Formless monsters |
| Undead | Undead monsters |
| Brute | Brute/Animal |
| Plant | Plant monsters |
| Insect | Insect monsters |
| Fish | Fish/Sea creatures |
| Demon | Demon monsters |
| DemiHuman | Humanoid monsters |
| Angel | Angel monsters |
| Dragon | Dragon monsters |

### Monster Sizes
| Size | Description |
|------|-------------|
| Small | Small monsters |
| Medium | Medium monsters |
| Large | Large monsters |

### AI Types
| AI | Behavior |
|----|----------|
| 01 | Passive |
| 02 | Passive, looter |
| 03 | Passive, looter, helper |
| 04 | Aggressive |
| 05 | Aggressive, looter |
| 06 | Aggressive, looter, helper |
| 07 | Boss |

---

## quest_db.yml Schema

<!-- RAG_CHUNK: quest_db_schema -->

```yaml
Header:
  Type: QUEST_DB
  Version: 2

Body:
  - Id: 1000                   # Quest ID
    Title: "Sample Quest"      # Quest title
    TimeLimit: 86400           # Time limit in seconds (0=none)
    Targets:                   # Hunt objectives
      - Mob: PORING
        Count: 10
        Id: 0
        Race: All
        Size: All
        Element: All
        MinLevel: 0
        MaxLevel: 0
    Drops:                     # Collect objectives
      - Mob: PORING
        Item: Jellopy
        Count: 5
        Rate: 5000
```

---

## item_group_db.yml Schema

<!-- RAG_CHUNK: item_group_schema -->

```yaml
Header:
  Type: ITEM_GROUP_DB
  Version: 1

Body:
  - Group: IG_BLUEBOX          # Group constant
    SubGroups:
      - SubGroup: 0
        List:
          - Index: 0
            Item: Jellopy
            Rate: 1000
            Amount: 1
            Random: 0
            IsAnnounced: false
            Duration: 0
            GUID: ""
            IsNamed: false
            IsBound: 0
```

### Common Item Groups
| Group | Description |
|-------|-------------|
| IG_BLUEBOX | Old Blue Box |
| IG_VIOLETBOX | Old Purple Box |
| IG_CARDALBUM | Card Album |
| IG_GIFTBOX | Gift Box |
| IG_SCROLLBOX | Scroll Box |

---

*Generated as part of rAthena KB v5 Enhanced Package*
