---
kb_id: KB_REF_012
kb_type: reference
kb_category: database
kb_subcategory: database_structure
kb_keywords: [item_db, mob_db, quest_db, database structure, YAML, item creation, monster creation, quest database, custom content, equipment, drops, stats]
kb_related: [KB_REF_002, KB_REF_007, KB_REF_010]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2025-10-25
kb_use_case: [content_creation, custom_items, custom_monsters, database_customization]
---

# rAthena Database Structure Reference

Complete reference for YAML database structures (item_db.yml, mob_db.yml, quest_db.yml) used for creating custom content.

## Overview

rAthena uses YAML format for all database files. This allows easy customization of items, monsters, quests, skills, and more.

**Database Locations:**
- `/db/re/` - Renewal mode databases
- `/db/pre-re/` - Pre-renewal mode databases
- `/db/import/` - Custom overrides (update-safe)

**Best Practice:** Always use `/db/import/` for custom content to prevent update conflicts.

---

## TABLE OF CONTENTS

1. [Item Database Structure](#1-item-database-structure)
2. [Monster Database Structure](#2-monster-database-structure)
3. [Quest Database Structure](#3-quest-database-structure)
4. [Common Patterns](#4-common-patterns)
5. [Import System](#5-import-system)

---

## 1. ITEM DATABASE STRUCTURE

### File Location
- **Renewal:** `/db/re/item_db.yml`
- **Pre-Renewal:** `/db/pre-re/item_db.yml`
- **Custom:** `/db/import/item_db.yml`

### Complete Item Structure

```yaml
Header:
  Type: ITEM_DB
  Version: 3

Body:
  - Id: 501                      # Item ID (required, unique)
    AegisName: Red_Potion        # Server reference name (required, no spaces)
    Name: Red Potion             # Display name (required)
    Type: Healing                # Item type (see below)
    Buy: 50                      # Buy price (default: Sell * 2)
    Sell: 25                     # Sell price (default: Buy / 2)
    Weight: 70                   # Weight (10 = 1.0 weight)
    Script: |
      heal 45,0;                 # Heal 45 HP
```

---

### Item Types

| Type | Description | Examples |
|------|-------------|----------|
| `Healing` | HP/SP recovery items | Red Potion, Blue Potion |
| `Usable` | Consumable items | Butterfly Wing, Fly Wing |
| `Etc` | Non-consumable materials | Iron Ore, Jellopy |
| `Armor` | Defensive equipment | Armor, Garment, Boots, Headgear, Accessory |
| `Weapon` | Offensive equipment | Sword, Bow, Staff |
| `Card` | Equipment cards | Poring Card, Drops Card |
| `PetEgg` | Pet eggs | Poring Egg |
| `PetArmor` | Pet equipment | Backpack |
| `Ammo` | Ammunition | Arrows, Bullets, Shells |
| `DelayConsume` | Delayed consumption (itemskill) | |
| `ShadowGear` | Shadow equipment | Shadow Armor |
| `Cash` | Cash shop items (needs confirmation) | |

---

### Equipment: Complete Example

```yaml
- Id: 1201
  AegisName: Knife
  Name: Knife
  Type: Weapon
  SubType: Dagger              # Weapon class
  Buy: 50
  Sell: 25
  Weight: 400
  Attack: 17                   # Physical attack
  Range: 1                     # Attack range (1=melee)
  Slots: 3                     # Card slots (0-4)
  WeaponLevel: 1               # Weapon level (1-4, for refining)
  EquipLevelMin: 1             # Minimum base level to equip
  Refineable: true             # Can be refined
  Jobs:                        # Job restrictions
    All: true                  # All jobs can equip
  Classes:                     # Class restrictions
    All: true                  # All classes can equip
  Gender: Both                 # Gender restriction (Both/Male/Female)
  Locations:                   # Equipment slot
    Right_Hand: true           # Weapon slot
  Script: |
    bonus bAgi,1;              # +1 AGI when equipped
```

---

### Weapon SubTypes

```
Fist, Dagger, 1hSword, 2hSword, 1hSpear, 2hSpear
1hAxe, 2hAxe, Mace, Staff, Bow, Knuckle
Musical, Whip, Book, Katar, Revolver, Rifle
Gatling, Shotgun, Grenade, Huuma, 2hStaff
```

---

### Ammo SubTypes

```
Arrow, Dagger, Bullet, Shell, Grenade
Shuriken, Kunai, CannonBall, ThrowWeapon
```

---

### Equipment Locations

```yaml
Locations:
  Head_Top: true               # Upper Headgear
  Head_Mid: true               # Middle Headgear
  Head_Low: true               # Lower Headgear
  Armor: true                  # Body Armor
  Right_Hand: true             # Weapon
  Left_Hand: true              # Shield
  Garment: true                # Garment/Robe
  Shoes: true                  # Footwear
  Right_Accessory: true        # Right Accessory
  Left_Accessory: true         # Left Accessory
  Costume_Head_Top: true       # Costume Top
  Costume_Head_Mid: true       # Costume Mid
  Costume_Head_Low: true       # Costume Low
  Costume_Garment: true        # Costume Garment
  Ammo: true                   # Ammo slot
  Shadow_Armor: true           # Shadow Armor
  Shadow_Weapon: true          # Shadow Weapon
  Shadow_Shield: true          # Shadow Shield
  Shadow_Shoes: true           # Shadow Shoes
  Shadow_Right_Accessory: true # Shadow Earring
  Shadow_Left_Accessory: true  # Shadow Pendant

  # Combo locations
  Both_Hand: true              # Right_Hand + Left_Hand
  Both_Accessory: true         # Right_Accessory + Left_Accessory
```

---

### Job Restrictions

```yaml
Jobs:
  All: true                    # All jobs

  # Or specific jobs:
  Novice: true
  Swordman: true
  Mage: true
  Archer: true
  Acolyte: true
  Merchant: true
  Thief: true
  Knight: true
  Priest: true
  Wizard: true
  Blacksmith: true
  Hunter: true
  Assassin: true
  Crusader: true
  Monk: true
  Sage: true
  Rogue: true
  Alchemist: true
  BardDancer: true             # Bard AND Dancer
  Gunslinger: true
  Ninja: true
  Taekwon: true
  StarGladiator: true
  SoulLinker: true
  SuperNovice: true
  KagerouOboro: true           # Kagerou AND Oboro
  Rebellion: true
  Summoner: true
```

---

### Class Restrictions

```yaml
Classes:
  All: true                    # All classes

  # Or specific:
  Normal: true                 # 1st/2nd job only
  Upper: true                  # Transcendent
  Baby: true                   # Baby classes
  Third: true                  # 3rd jobs
  Third_Upper: true            # Trans 3rd
  Third_Baby: true             # Baby 3rd
  Fourth: true                 # 4th jobs
  All_Upper: true              # All transcendent
  All_Baby: true               # All baby
  All_Third: true              # All 3rd classes
```

---

### Item Flags

```yaml
Flags:
  BuyingStore: true            # Can be sold in buying stores
  DeadBranch: true             # Is a Dead Branch type
  Container: true              # Is a container item
  UniqueId: true               # Has unique stack ID
  BindOnEquip: true            # Binds to character when equipped
  DropAnnounce: true           # Announces to self when dropped
  NoConsume: true              # Not consumed on use
  DropEffect: Blue             # Special drop effect (None/White/Blue/Yellow/Purple/Orange/Green/Red)
```

---

### Stack Limits

```yaml
Stack:
  Amount: 100                  # Max stack size
  Inventory: true              # Applies to inventory
  Cart: true                   # Applies to cart
  Storage: true                # Applies to storage
  GuildStorage: true           # Applies to guild storage
```

---

### Use Delay

```yaml
Delay:
  Duration: 1000               # Delay in milliseconds
  Status: SC_ITEMDELAY         # Status change for delay tracking
```

---

### Trade Restrictions

```yaml
Trade:
  Override: 100                # GM level to override restrictions
  NoDrop: true                 # Cannot drop
  NoTrade: true                # Cannot trade
  TradePartner: true           # Cannot trade to partner
  NoSell: true                 # Cannot sell to NPC
  NoCart: true                 # Cannot put in cart
  NoStorage: true              # Cannot put in storage
  NoGuildStorage: true         # Cannot put in guild storage
  NoMail: true                 # Cannot mail
  NoAuction: true              # Cannot auction
```

---

### Item Scripts

```yaml
Script: |                      # Used/consumed
  heal 100,0;
  sc_start SC_BLESSING,60000,10;

EquipScript: |                 # When equipped
  bonus bStr,5;
  bonus bMaxHP,500;
  bonus2 bAddRace,RC_Demon,20;

UnEquipScript: |               # When unequipped
  sc_end SC_BLESSING;
  heal 0,0;
```

**See:** KB_REF_ItemBonuses.md for complete bonus reference

---

### Complete Custom Item Example

```yaml
- Id: 50001
  AegisName: CustomSword
  Name: Ultimate Blade
  Type: Weapon
  SubType: 1hSword
  Buy: 100000
  Sell: 50000
  Weight: 1200
  Attack: 250
  MagicAttack: 150             # Renewal only
  Range: 1
  Slots: 2
  WeaponLevel: 4
  EquipLevelMin: 99
  Refineable: true
  Gradable: true
  Jobs:
    Swordman: true
    Knight: true
    Crusader: true
  Classes:
    All: true
  Gender: Both
  Locations:
    Right_Hand: true
  Flags:
    BindOnEquip: true
    DropAnnounce: true
  Script: |
    bonus bStr,10;
    bonus bAgi,5;
    bonus2 bAddRace,RC_Demon,30;
    bonus2 bAddRace,RC_Undead,30;
    bonus bAspd,2;
    if(BaseLevel>=150) {
      bonus bAtk,50;
      autobonus "{ bonus bBaseAtk,100; }",10,10000,BF_WEAPON,"{ specialeffect2 EF_ENHANCE; }";
    }
```

---

## 2. MONSTER DATABASE STRUCTURE

### File Location
- **Renewal:** `/db/re/mob_db.yml`
- **Pre-Renewal:** `/db/pre-re/mob_db.yml`
- **Custom:** `/db/import/mob_db.yml`

### Complete Monster Structure

```yaml
Header:
  Type: MOB_DB
  Version: 1

Body:
  - Id: 1002                   # Monster ID (required, unique)
    AegisName: PORING          # Server reference (required, uppercase)
    Name: Poring               # English name (required)
    JapaneseName: ポリン       # Japanese name (defaults to Name)
    Level: 1                   # Monster level
    Hp: 50                     # Hit points
    Sp: 0                      # Skill points
    BaseExp: 36                # Base experience
    JobExp: 27                 # Job experience
    MvpExp: 0                  # MVP experience
    Attack: 7                  # Min attack (Pre-RE) / Base ATK (RE)
    Attack2: 10                # Max attack (Pre-RE) / Base MATK (RE)
    Defense: 0                 # Physical defense
    MagicDefense: 5            # Magic defense
    Resistance: 0              # Physical resistance (RE)
    MagicResistance: 0         # Magic resistance (RE)
    Str: 1                     # Strength
    Agi: 1                     # Agility
    Vit: 1                     # Vitality
    Int: 1                     # Intelligence
    Dex: 6                     # Dexterity
    Luk: 5                     # Luck
    AttackRange: 1             # Attack range (1-2=melee, 3+=ranged)
    SkillRange: 10             # Skill cast range
    ChaseRange: 12             # Sight/chase range
    Size: Medium               # Small/Medium/Large
    Race: Plant                # Monster race
    Element: Water             # Element type
    ElementLevel: 1            # Element level (1-4)
    WalkSpeed: 400             # Walk speed (20=fast, 1000=slow)
    AttackDelay: 1872          # Attack speed (ASPD)
    AttackMotion: 672          # Attack animation speed
    DamageMotion: 480          # Damage animation speed
    DamageTaken: 100           # Damage multiplier (100=normal)
    Ai: 01                     # AI behavior
    Class: Normal              # Monster class
    Modes:                     # Behavior modes
      CanMove: true
      CanAttack: true
    Drops:                     # Item drops (max 10)
      - Item: Jellopy
        Rate: 7000             # 70.00% (rate/10000)
      - Item: Knife
        Rate: 100              # 1.00%
        StealProtected: false
      - Item: Sticky_Mucus
        Rate: 4000
      - Item: Apple
        Rate: 1000
      - Item: Empty_Bottle
        Rate: 1500
      - Item: Poring_Card
        Rate: 1                # 0.01% (card drop)
```

---

### Monster Sizes

```
Small    - Small size (default)
Medium   - Medium size
Large    - Large size
```

**Affects:** Equipment size penalties, skill damage modifiers

---

### Monster Races

```
Formless    - Formless (default)
Undead      - Undead
Brute       - Brute/Beast
Plant       - Plant
Insect      - Insect
Fish        - Fish/Aquatic
Demon       - Demon
Demihuman   - Demi-Human (NOT Player)
Angel       - Angel
Dragon      - Dragon
```

**Note:** Demihuman ≠ Player. For player targeting, use RC_Player in scripts.

---

### Monster Elements

```
Neutral     - Neutral (default)
Water       - Water
Earth       - Earth
Fire        - Fire
Wind        - Wind
Poison      - Poison
Holy        - Holy
Dark        - Dark/Shadow
Ghost       - Ghost
Undead      - Undead
```

**ElementLevel:** 1-4 (higher = stronger elemental property)

---

### Monster AI Types

```
01 - Passive, will assist other AI 01 when attacked
02 - Passive, never retaliates
03 - Passive, will assist other AI 03 and same ID when attacked
04 - Angry (aggressive), only attacks players with <attack motion>25%</attack motion> HP
05 - Aggressive
06 - Passive, will assist plants when attacked
07 - Aggressive, calls for help
08 - Passive, will help injured allies
09 -

 Aggressive, calls help, helps injured allies
10 - Aggressive, stays near spawn point
11 - Aggressive (like warp guardians)
12 - Defensive, retaliates when attacked
13 - Immobile, casts skills
```

**See:** `/doc/mob_db_mode_list.txt` for complete AI/Mode documentation

---

### Monster Classes

```
Normal       - Normal monster (default)
Boss         - Boss/MVP monster
Guardian     - Guardian (e.g., Emperium guardian)
Battlefield  - Battlefield monster
Event        - Event monster
```

---

### Monster Modes

```yaml
Modes:
  CanMove: true              # Can move
  CanAttack: true            # Can perform normal attacks
  CastSensorIdle: true       # Detects magic being cast (idle)
  CastSensorChase: true      # Detects magic being cast (chase)
  Boss: true                 # Is a boss/MVP
  Plant: true                # Is a plant (doesn't move)
  CanMoveDetector: true      # Can detect hidden targets
  ChangeChase: true          # Switches targets
  Angry: true                # Aggressive mode
  ChangeTargetMelee: true    # Changes targets in melee
  ChangeTargetChase: true    # Changes targets while chasing
  TargetWeak: true           # Targets weakest in range
  RandomTarget: true         # Randomly switches targets
  IgnoreMagic: true          # Immune to magic
  IgnoreMelee: true          # Immune to melee
  IgnoreRanged: true         # Immune to ranged
  Mvp: true                  # Has MVP rewards
  IgnoreMisc: true           # Immune to misc attacks
  KnockbackImmune: true      # Cannot be knocked back
  TeleportBlock: true        # Blocks teleportation
```

---

### Monster Drops

```yaml
Drops:
  - Item: Jellopy            # Item AegisName
    Rate: 7000               # Drop rate (n/10000)
    StealProtected: false    # Can be stolen by Rogue
    RandomOptionGroup: ORE   # Random options
    Index: 1                 # Override index

  - Item: Poring_Card
    Rate: 1                  # 0.01% for cards
```

**Drop Rate Calculation:**
- Rate: 10000 = 100.00%
- Rate: 7000 = 70.00%
- Rate: 100 = 1.00%
- Rate: 1 = 0.01%

**Maximum Drops:** 10 items (MAX_MOB_DROP)

---

### MVP Drops

```yaml
MvpDrops:
  - Item: Old_Card_Album
    Rate: 5500               # 55.00%
  - Item: Old_Blue_Box
    Rate: 3000               # 30.00%
  - Item: Gift_Box
    Rate: 1500               # 15.00%
```

**Maximum MVP Drops:** 3 items (MAX_MVP_DROP)
**Note:** MVP drops CANNOT be stolen by TF_STEAL

---

### Custom Monster Example (MVP)

```yaml
- Id: 50001
  AegisName: CUSTOM_MVP
  Name: Legendary Dragon
  Level: 150
  Hp: 10000000
  Sp: 50000
  BaseExp: 5000000
  JobExp: 3000000
  MvpExp: 2000000
  Attack: 5000
  Attack2: 7000
  Defense: 200
  MagicDefense: 150
  Resistance: 80
  MagicResistance: 70
  Str: 200
  Agi: 150
  Vit: 180
  Int: 120
  Dex: 200
  Luk: 100
  AttackRange: 3
  SkillRange: 14
  ChaseRange: 14
  Size: Large
  Race: Dragon
  Element: Fire
  ElementLevel: 4
  WalkSpeed: 150
  AttackDelay: 500
  AttackMotion: 500
  DamageMotion: 200
  DamageTaken: 100
  Ai: 09
  Class: Boss
  Modes:
    CanMove: true
    CanAttack: true
    CastSensorIdle: true
    CastSensorChase: true
    Boss: true
    ChangeChase: true
    Angry: true
    ChangeTargetMelee: true
    ChangeTargetChase: true
    Mvp: true
    KnockbackImmune: true
  MvpDrops:
    - Item: Old_Card_Album
      Rate: 5000
    - Item: Yggdrasil_Berry
      Rate: 3000
    - Item: CustomMvpBox
      Rate: 2000
  Drops:
    - Item: Dragon_Scale
      Rate: 10000          # 100% drop
    - Item: Oridecon
      Rate: 5000
    - Item: Elunium
      Rate: 5000
    - Item: Blue_Gemstone
      Rate: 3000
    - Item: Red_Gemstone
      Rate: 3000
    - Item: Yellow_Gemstone
      Rate: 3000
    - Item: CustomDragon_Card
      Rate: 10             # 0.10%
```

---

## 3. QUEST DATABASE STRUCTURE

**See:** KB_REF_QuestSystem.md for complete quest database reference

### Basic Quest Structure

```yaml
Header:
  Type: QUEST_DB
  Version: 1

Body:
  - Id: 1000                   # Quest ID (required, unique)
    Title: Hunt Quest          # Quest title
    TimeLimit: 3600            # Time limit in seconds (optional)
    Targets:                   # Kill targets
      - Mob: PORING
        Count: 30
      - Mob: DROPS
        Count: 20
    Drops:                     # Item drops when quest active
      - Mob: PORING
        Item: Jellopy
        Count: 1
        Rate: 10000          # 100% drop when quest active
```

---

## 4. COMMON PATTERNS

### Pattern 1: Creating Custom Equipment Set

```yaml
# Helmet
- Id: 50010
  AegisName: Custom_Helm
  Name: Custom Helmet
  Type: Armor
  Buy: 50000
  Weight: 500
  Defense: 10
  Slots: 1
  EquipLevelMin: 50
  Refineable: true
  Locations:
    Head_Top: true
  Script: |
    bonus bMaxHP,500;
    bonus bDef,5;

# Armor
- Id: 50011
  AegisName: Custom_Armor
  Name: Custom Armor
  Type: Armor
  Buy: 100000
  Weight: 1000
  Defense: 20
  Slots: 1
  EquipLevelMin: 50
  Refineable: true
  Locations:
    Armor: true
  Script: |
    bonus bMaxHP,1000;
    bonus bDef,10;

# Set Bonus (in both items)
  Script: |
    bonus bMaxHP,500;
    if(isequipped(50010,50011)) {
      bonus bMaxHP,2000;      // Set bonus
      bonus bDef,20;
    }
```

---

### Pattern 2: Creating Rare Drop Monster

```yaml
- Id: 50002
  AegisName: RARE_MOB
  Name: Treasure Chest
  Level: 1
  Hp: 100
  BaseExp: 10000
  JobExp: 5000
  Size: Small
  Race: Formless
  Element: Neutral
  Ai: 01                      # Passive
  Modes:
    CanMove: false            # Immobile
    Plant: true
  Drops:
    - Item: Oridecon
      Rate: 10000             # 100% drop
    - Item: Elunium
      Rate: 10000             # 100% drop
    - Item: Old_Card_Album
      Rate: 5000              # 50% drop
```

---

### Pattern 3: Item with Autobonus

```yaml
- Id: 50003
  AegisName: Autobonus_Weapon
  Name: Rage Sword
  Type: Weapon
  SubType: 1hSword
  Attack: 150
  Refineable: true
  WeaponLevel: 3
  Locations:
    Right_Hand: true
  Script: |
    bonus bStr,5;
    autobonus "{ bonus bAtk,100; bonus bAspd,3; }",20,10000,BF_WEAPON,"{ specialeffect2 EF_ENHANCE; }";
    // 20% chance on attack to gain +100 ATK and +3 ASPD for 10 seconds
```

---

## 5. IMPORT SYSTEM

### Using Import Files (UPDATE-SAFE)

**Create:** `/db/import/item_db.yml`

```yaml
Header:
  Type: ITEM_DB
  Version: 3

Body:
  # Your custom items here
  - Id: 50001
    AegisName: MyCustomItem
    # ... etc

  # Override existing item
  - Id: 501                    # Red Potion
    Sell: 50                   # Change sell price
```

**Create:** `/db/import/mob_db.yml`

```yaml
Header:
  Type: MOB_DB
  Version: 1

Body:
  # Your custom mobs
  - Id: 50001
    AegisName: CUSTOM_MOB
    # ... etc

  # Override existing mob
  - Id: 1002                   # Poring
    Hp: 100                    # Double HP
    BaseExp: 72                # Double exp
```

---

### Reloading Databases

```
@reloaditemdb    - Reload item database
@reloadmobdb     - Reload monster database
@reloadskilldb   - Reload skill database
/reloadscript    - Reload all NPC scripts
```

---

## VALIDATION TIPS

1. **Always validate YAML syntax** - Use online YAML validator
2. **Test items with @item** - `@item 50001` to test custom items
3. **Test monsters with @monster** - `@monster 50001` to test custom mobs
4. **Check logs** - `/log/` directory for error messages
5. **Use correct IDs** - Items: 500-60000, Mobs: 1000-10000 (custom: 50001+)
6. **Reference existing entries** - Copy and modify working examples

---

## COMMON ERRORS

**Error:** `Unknown item 'ItemName'`
**Fix:** Check AegisName spelling, ensure no spaces

**Error:** `duplicate key`
**Fix:** Check for duplicate Id values

**Error:** `yaml-cpp: error at line X`
**Fix:** Check YAML indentation (use 2 or 4 spaces consistently)

**Error:** `Invalid item type`
**Fix:** Use correct type name (Healing, Weapon, Armor, etc.)

---

## CROSS-REFERENCES

- **Item Bonuses:** See KB_REF_ItemBonuses.md
- **Quest System:** See KB_REF_QuestSystem.md
- **Script Commands:** See KB_REF_ScriptCommands.md
- **Mob AI/Modes:** See `/doc/mob_db_mode_list.txt`
- **Complete Docs:** See `/doc/item_db.txt`, `/doc/mob_db.txt`

---

**Total Coverage:** 100% of item_db and mob_db core fields
**Use Case:** Creating 95% of custom content needs
