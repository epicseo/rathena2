# rAthena KB v6 - Database Schemas Reference

**Version:** 6.0 Complete
**Generated:** 2025-11-26
**Format:** YAML (rAthena uses ryml parser)

---

## Quick Navigation

- [item_db.yml](#item_dbyml) - Item definitions
- [skill_db.yml](#skill_dbyml) - Skill definitions
- [mob_db.yml](#mob_dbyml) - Monster definitions
- [quest_db.yml](#quest_dbyml) - Quest definitions
- [item_group_db.yml](#item_group_dbyml) - Item groups

---

## item_db.yml

<!-- RAG_CHUNK: db_item -->

### Complete Schema
```yaml
Header:
  Type: ITEM_DB
  Version: 3

Body:
  - Id: 501                      # Required: Unique item ID
    AegisName: "Red_Potion"      # Required: Server-side name (unique)
    Name: "Red Potion"           # Required: Display name
    Type: Healing                # Item type
    SubType: None                # Weapon/Ammo subtype
    Buy: 50                      # NPC buy price
    Sell: 10                     # NPC sell price
    Weight: 70                   # Item weight (0.1 units)
    Attack: 0                    # Physical attack
    MagicAttack: 0               # Magic attack (weapons)
    Defense: 0                   # Defense value (armor)
    Range: 0                     # Attack range (weapons)
    Slots: 0                     # Card slots (0-4)
    
    Jobs:                        # Equippable jobs
      All: true
      Novice: true
      Swordman: true
      # ... etc
    
    Classes:                     # Equippable classes
      All: true
      Normal: true
      Upper: true
      Baby: true
      Third: true
      Third_Upper: true
      Third_Baby: true
      Fourth: true
    
    Gender: Both                 # Male/Female/Both
    
    Locations:                   # Equipment slots
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
      Both_Hand: true            # Two-handed
      Both_Accessory: true       # Both accessory slots
    
    WeaponLevel: 1               # Weapon level (1-5)
    ArmorLevel: 1                # Armor level (1-2)
    EquipLevelMin: 1             # Minimum equip base level
    EquipLevelMax: 0             # Maximum equip level (0=none)
    Refineable: true             # Can be refined
    Gradable: false              # Can be graded (4th job)
    View: 0                      # Client sprite ID
    
    Flags:
      BuyingStore: false         # Can list in buying store
      DeadBranch: false          # Is dead branch item
      Container: false           # Is container item
      UniqueId: true             # Has unique ID
      BindOnEquip: false         # Binds when equipped
      DropAnnounce: false        # Announces on drop
      NoConsume: false           # Not consumed on use
      DropEffect: None           # DROPEFFECT_*
    
    Delay:
      Duration: 0                # Use delay (ms)
      Status: None               # Status that blocks use
    
    Stack:
      Amount: 0                  # Max stack (0=no limit)
      Inventory: true
      Cart: true
      Storage: true
      GuildStorage: true
    
    NoUse:
      Override: 0                # GM level to override
      Sitting: false             # Block while sitting
    
    Trade:
      Override: 0                # GM level to override
      NoDrop: false
      NoTrade: false
      TradePartner: false
      NoSell: false
      NoCart: false
      NoStorage: false
      NoGuildStorage: false
      NoMail: false
      NoAuction: false
    
    Script: |                    # On-use/equip script
      itemheal 45,0;
    
    EquipScript: |               # On-equip script
      bonus bStr,1;
    
    UnEquipScript: |             # On-unequip script
      # code here
```

### Item Types
| Type | ID | Description |
|------|-----|-------------|
| Healing | 0 | Healing consumables |
| Usable | 2 | Usable items |
| Etc | 3 | Misc items |
| Armor | 4 | Equipment (non-weapon) |
| Weapon | 5 | Weapons |
| Card | 6 | Cards |
| PetEgg | 7 | Pet eggs |
| PetArmor | 8 | Pet equipment |
| Ammo | 10 | Ammunition |
| DelayConsume | 11 | Delayed consume |
| ShadowGear | 12 | Shadow equipment |
| Cash | 18 | Cash items |

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
| Musical | Instruments |
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

---

## skill_db.yml

<!-- RAG_CHUNK: db_skill -->

### Complete Schema
```yaml
Header:
  Type: SKILL_DB
  Version: 3

Body:
  - Id: 1                        # Skill ID
    Name: "NV_BASIC"             # Skill constant
    Description: "Basic Skill"   # Display name
    MaxLevel: 9                  # Max skill level
    Type: None                   # None/Weapon/Magic/Misc
    TargetType: Self             # Passive/Attack/Ground/Self/Support/Trap
    
    DamageFlags:
      Splash: false
      SplashSplit: false
      IgnoreAtkCard: false
      IgnoreElement: false
      IgnoreDefense: false
      IgnoreFlee: false
      IgnoreDefCard: false
      Critical: false
      NoDamage: false
    
    Flags:
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
      IgnoreLandProtector: false
      AllowWhenHidden: false
    
    Range:
      - Level: 1
        Size: 0
    
    Hit: None                    # None/Single/Multi
    
    HitCount:
      - Level: 1
        Count: 0
    
    Element:
      - Level: 1
        Element: Neutral
    
    CastTime:
      - Level: 1
        Time: 0                  # milliseconds
    
    AfterCastActDelay:
      - Level: 1
        Time: 0
    
    Cooldown:
      - Level: 1
        Time: 0
    
    FixedCastTime:
      - Level: 1
        Time: 0
    
    Requires:
      HpCost:
        - Level: 1
          Amount: 0
      SpCost:
        - Level: 1
          Amount: 0
      Weapon:
        All: true
      State: None                # Required state
      ItemCost:
        - Item: Red_Gemstone
          Amount: 1
```

---

## mob_db.yml

<!-- RAG_CHUNK: db_mob -->

### Complete Schema
```yaml
Header:
  Type: MOB_DB
  Version: 3

Body:
  - Id: 1002                     # Monster ID
    AegisName: "PORING"          # Server-side name
    Name: "Poring"               # Display name
    Level: 1
    Hp: 50
    Sp: 0
    BaseExp: 2
    JobExp: 1
    MvpExp: 0                    # MVP bonus EXP
    Attack: 7                    # Min ATK
    Attack2: 10                  # Max ATK
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
    Size: Small                  # Small/Medium/Large
    Race: Plant                  # Monster race
    Element: Water               # Element
    ElementLevel: 1              # Element level (1-4)
    WalkSpeed: 400
    AttackDelay: 1872
    AttackMotion: 672
    DamageMotion: 480
    DamageTaken: 100             # Damage modifier %
    Ai: 02                       # AI type
    Class: Normal                # Normal/Boss/Guardian
    
    Modes:
      CanMove: true
      Looter: true
      Aggressive: false
      Assist: false
      Boss: false
      Plant: false
      CanAttack: true
      Detector: false
      StatusImmune: false
      SkillImmune: false
    
    MvpDrops:
      - Item: Old_Card_Album
        Rate: 5000               # 50.00%
        StealProtected: true
    
    Drops:
      - Item: Jellopy
        Rate: 7000               # 70.00%
      - Item: Knife_
        Rate: 100                # 1.00%
      - Item: Poring_Card
        Rate: 1                  # 0.01%
```

### Monster Races
| Race | ID |
|------|-----|
| Formless | 0 |
| Undead | 1 |
| Brute | 2 |
| Plant | 3 |
| Insect | 4 |
| Fish | 5 |
| Demon | 6 |
| DemiHuman | 7 |
| Angel | 8 |
| Dragon | 9 |

### AI Types
| AI | Behavior |
|----|----------|
| 01 | Passive |
| 02 | Passive, looter |
| 03 | Passive, looter, assist |
| 04 | Aggressive |
| 05 | Aggressive, looter |
| 06 | Aggressive, assist |
| 07 | Boss |
| 08 | Passive, immobile |
| 09 | Aggressive, immobile |
| 10 | Passive, cast sensor |
| 17 | Boss, looter |
| 21 | Boss, aggressive |

---

## quest_db.yml

<!-- RAG_CHUNK: db_quest -->

```yaml
Header:
  Type: QUEST_DB
  Version: 2

Body:
  - Id: 1000                     # Quest ID
    Title: "Hunt Porings"        # Quest title
    TimeLimit: 86400             # Time limit (seconds), 0=none
    
    Targets:                     # Hunt objectives
      - Mob: PORING
        Count: 10
        Id: 0                    # Sub-objective ID
        Race: All                # Race filter
        Size: All                # Size filter
        Element: All             # Element filter
        MinLevel: 0
        MaxLevel: 0
    
    Drops:                       # Collect objectives
      - Mob: PORING
        Item: Jellopy
        Count: 5
        Rate: 5000               # 50% drop rate from kills
```

---

*Generated as part of rAthena KB v6 Complete*
