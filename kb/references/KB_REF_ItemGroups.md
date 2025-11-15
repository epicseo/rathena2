---
kb_id: KB_REF_019
title: "rAthena Item Groups & Random Box System"
category: Database & Content
keywords: [item_group, random_box, getgroupitem, getrandgroupitem, groupranditem, algorithm, subgroup, shared_pool, item_group_db, old_blue_box, gift_box, card_album]
related_files: [
  "db/re/item_group_db.yml",
  "db/pre-re/item_group_db.yml",
  "doc/item_group.txt",
  "src/map/itemdb.hpp",
  "src/map/script_constants.hpp"
]
difficulty: intermediate
use_case: "Creating random item boxes, gacha systems, reward pools, loot tables, mystery boxes, and complex item distribution systems"
version: rAthena 2024
last_updated: 2024-01-15
---

# rAthena Item Groups & Random Box System

## Table of Contents
1. [System Overview](#system-overview)
2. [Database Structure](#database-structure)
3. [Algorithm Types](#algorithm-types)
4. [SubGroup System](#subgroup-system)
5. [Script Commands](#script-commands)
6. [Advanced Features](#advanced-features)
7. [Complete Examples](#complete-examples)
8. [Common Item Boxes](#common-item-boxes)
9. [Creating Custom Groups](#creating-custom-groups)
10. [Best Practices](#best-practices)

---

## System Overview

The **Item Group System** allows you to create pools of items with configurable probabilities and behaviors. Used for:
- **Random Boxes** (Old Blue Box, Gift Box, etc.)
- **Card Albums** (Old Card Album, class-specific albums)
- **Gacha Systems** (event boxes, premium boxes)
- **Quest Rewards** (variable reward pools)
- **Event Prizes** (lottery systems, raffles)

### Database Files
```yaml
# Renewal Mode
db/re/item_group_db.yml

# Pre-Renewal Mode
db/pre-re/item_group_db.yml

# Import Override
db/import/item_group_db.yml
```

### IG_ Constants
Groups are referenced via `IG_` constants:
```c
// Example Constants (auto-generated from group names)
IG_BLUEBOX          // "BLUEBOX" group
IG_CARDALBUM        // "CARDALBUM" group
IG_CANDY            // "CANDY" group
IG_MyCustomGroup    // "MyCustomGroup" group

// Usage in scripts
getgroupitem(IG_BLUEBOX);
.@item_id = groupranditem(IG_CARDALBUM);
```

**Important**: The `IG_` prefix is automatically appended to the group name when reading the database.

---

## Database Structure

### Basic YAML Format

```yaml
Header:
  Type: ITEM_GROUP_DB
  Version: 4

Body:
  - Group: GroupName          # Name of item group (IG_ prefix auto-added)
    SubGroups:
      - SubGroup: 1           # SubGroup number (0 = "must" items, 1+ = random pools)
        Algorithm: Random     # How items are selected (Random/All/SharedPool)
        List:
          - Index: 0          # Unique identifier for this entry
            Item: ItemName    # AegisName from item_db
            Rate: 100         # Probability weight (not percentage!)
            Amount: 1         # Quantity to give (default: 1)
```

### Field Reference

| Field | Type | Description | Default |
|-------|------|-------------|---------|
| **Group** | string | Group name (IG_ prefix added automatically) | Required |
| **SubGroup** | int | SubGroup number (0 for "must" items, 1+ for random) | Required |
| **Algorithm** | enum | Selection method (Random/All/SharedPool) | SharedPool |
| **Index** | int | Unique number to allow duplicate items with different settings | Required |
| **Item** | string | AegisName of item from item_db | Required |
| **Rate** | int | Probability weight (NOT percentage!) | 0 |
| **Amount** | int | Quantity of item to give | 1 |
| **Announced** | bool | Broadcast to server when obtained | false |
| **Duration** | int | Rental duration in minutes (0 = permanent) | 0 |
| **UniqueId** | bool | Give item with unique ID | from item_db |
| **Stacked** | bool | Stack items if possible | true |
| **Named** | bool | Inscribe obtainer's name on item | false |
| **Bound** | enum | Bind type (None/Account/Guild/Party/Char) | None |
| **RandomOptionGroup** | string | Random option group to apply | None |
| **RefineMinimum** | int | Minimum refine level | 0 |
| **RefineMaximum** | int | Maximum refine level | 0 |

---

## Algorithm Types

### 1. Random Algorithm

**Behavior**: Pick ONE random item based on rate as probability weight. Rates remain constant.

```yaml
- Group: MyWeaponBox
  SubGroups:
    - SubGroup: 1
      Algorithm: Random
      List:
        - Index: 0
          Item: Stiletto
          Rate: 5          # 5/7 chance (71.4%)
        - Index: 1
          Item: Dagger
          Rate: 2          # 2/7 chance (28.6%)
```

**Probability Calculation**:
```
Total Rate = 5 + 2 = 7
Stiletto chance = 5/7 = 71.4%
Dagger chance = 2/7 = 28.6%
```

**Use Cases**:
- Standard random boxes
- Quest reward choices
- Monster drops simulation
- Constant probability gacha

---

### 2. All Algorithm

**Behavior**: Give ALL items in the sub group. When used with commands expecting one item, picks randomly with equal probability (ignores rate).

```yaml
- Group: StarterPackage
  SubGroups:
    - SubGroup: 0
      Algorithm: All
      List:
        - Index: 0
          Item: Novice_Potion
          Amount: 100
        - Index: 1
          Item: Butterfly_Wing
          Amount: 50
        - Index: 2
          Item: Beginners_Uniform
```

**Important**: When using `All` algorithm, rate MUST remain unspecified (0).

**Use Cases**:
- Starter packages (all items guaranteed)
- Daily login rewards
- Quest completion bundles
- Event participation prizes

---

### 3. SharedPool Algorithm (Default)

**Behavior**: Items are "consumed" from a pool. Each time an item is drawn, it's removed from the pool, changing future probabilities. Pool refills on server restart or when empty.

```yaml
- Group: LimitedGachaBox
  SubGroups:
    - SubGroup: 1
      Algorithm: SharedPool    # Optional (default)
      List:
        - Index: 0
          Item: Jackpot_Item
          Rate: 1              # 1 item in pool
        - Index: 1
          Item: Rare_Item
          Rate: 5              # 5 items in pool
        - Index: 2
          Item: Common_Item
          Rate: 94             # 94 items in pool
```

**Probability Evolution**:
```
1st draw: Jackpot=1/100, Rare=5/100, Common=94/100
(If Common drawn)
2nd draw: Jackpot=1/99, Rare=5/99, Common=93/99
(If Jackpot drawn)
3rd draw: Rare=5/98, Common=93/98  (Jackpot exhausted!)
...after 100 draws, pool refills
```

**Use Cases**:
- Limited gacha (guarantee jackpot within X draws)
- Event boxes with exhaustible prizes
- Fairness-guaranteed loot systems
- TCG pack simulation

---

## SubGroup System

### SubGroup Numbering

| SubGroup | Type | Usage |
|----------|------|-------|
| **0** | "Must" items | Always given with `getgroupitem()` |
| **1** | Default random | Used by `groupranditem()`/`getrandgroupitem()` without subgroup arg |
| **2+** | Additional pools | Explicit subgroup selection required |

### Multi-SubGroup Example

```yaml
- Group: ComplexRewardBox
  SubGroups:
    # SubGroup 0 - Guaranteed items (All algorithm)
    - SubGroup: 0
      Algorithm: All
      List:
        - Index: 0
          Item: Red_Potion
          Amount: 5
        - Index: 1
          Item: Blue_Potion
          Amount: 5

    # SubGroup 1 - Main random pool (Random algorithm)
    - SubGroup: 1
      Algorithm: Random
      List:
        - Index: 0
          Item: Rare_Weapon
          Rate: 1          # 1/100 = 1%
        - Index: 1
          Item: Uncommon_Armor
          Rate: 9          # 9/100 = 9%
        - Index: 2
          Item: Common_Material
          Rate: 90         # 90/100 = 90%

    # SubGroup 2 - Bonus pool (Random algorithm)
    - SubGroup: 2
      Algorithm: Random
      List:
        - Index: 0
          Item: Bonus_Card
          Rate: 10
        - Index: 1
          Item: Bonus_Accessory
          Rate: 40
        - Index: 2
          Item: Bonus_Consumable
          Rate: 50
```

**Script Usage**:
```c
// Get ALL items from SubGroup 0 + random from SubGroup 1
getgroupitem(IG_ComplexRewardBox);

// Get only from SubGroup 1 (main pool)
getrandgroupitem(IG_ComplexRewardBox, 0, 1);

// Get only from SubGroup 2 (bonus pool)
getrandgroupitem(IG_ComplexRewardBox, 0, 2);

// Get item ID from SubGroup 0 ("must" items)
.@item = groupranditem(IG_ComplexRewardBox, 0);
```

---

## Script Commands

### 1. groupranditem()

**Syntax**: `groupranditem(<group_id>{,<sub_group>})`

**Returns**: Item ID (integer)

**Behavior**:
- Returns ONLY the item ID number
- Does NOT give the item to player
- Must be combined with `getitem()`
- Uses rate as probability weight

```c
// Get random item ID from default SubGroup (1)
.@item_id = groupranditem(IG_BLUEBOX);
getitem .@item_id, 1;

// Get from specific SubGroup
.@item_id = groupranditem(IG_MyGroup, 2);
getitem .@item_id, 5;

// Practical example: Random pet lure
.@taming_item = groupranditem(IG_Taming);
getitem .@taming_item, 1;
```

**Field Access**:
| Field | Accessed? |
|-------|-----------|
| GroupID | ✓ |
| Item | ✓ |
| Rate | ✓ |
| Amount | ✗ (ignored) |
| SubGroup | ✓ (optional) |
| Announced | ✗ |
| Duration | ✗ |
| UniqueId | ✗ |
| Bound | ✗ |
| Named | ✗ |

---

### 2. getrandgroupitem()

**Syntax**: `getrandgroupitem(<group_id>{,<quantity>{,<sub_group>{,<identify>{,<char_id>}}}})`

**Returns**: Success (1) or failure (0)

**Behavior**:
- Gives item(s) directly to player
- Respects `Amount` field if quantity=0
- Can override amount with quantity parameter
- Equipment given unidentified unless identify=1

```c
// Basic usage (default SubGroup 1, use Amount from list)
getrandgroupitem(IG_BLUEBOX);

// Override amount (2 items, ignore Amount field)
getrandgroupitem(IG_CARDALBUM, 2);

// Specify SubGroup and amount
getrandgroupitem(IG_MyGroup, 3, 2);  // 3 items from SubGroup 2

// From "must" SubGroup (0)
getrandgroupitem(IG_MyGroup, 5, 0);  // 5 items from SubGroup 0

// Give identified equipment
getrandgroupitem(IG_WeaponBox, 1, 1, 1);

// Give to specific character
getrandgroupitem(IG_PrizeBox, 1, 1, 0, getcharid(0, "PlayerName"));
```

**Field Access**:
| Field | Accessed? |
|-------|-----------|
| GroupID | ✓ |
| Item | ✓ |
| Rate | ✓ |
| Amount | ✓ (optional override) |
| SubGroup | ✓ (optional) |
| Announced | ✗ |
| Duration | ✗ |
| UniqueId | ✗ |
| Bound | ✗ |
| Named | ✗ |

---

### 3. getgroupitem()

**Syntax**: `getgroupitem(<group_id>{,<identify>{,<char_id>}})`

**Returns**: Success (1) or failure (0)

**Behavior**:
- Gives items from ALL SubGroups based on their algorithm
- SubGroup 0 (All): All items given
- SubGroup 1+ (Random): One random item per SubGroup
- Accesses ALL fields (Announced, Bound, Named, etc.)

```c
// Basic usage (processes all SubGroups)
getgroupitem(IG_BLUEBOX);

// Give identified equipment
getgroupitem(IG_WeaponRewardBox, 1);

// Give to specific character
getgroupitem(IG_EventPrize, 0, getcharid(0, "PlayerName"));
```

**SubGroup Processing**:
```yaml
# Example Group
- Group: MultiRewardBox
  SubGroups:
    - SubGroup: 0      # Algorithm: All
      List:
        - Item: Red_Potion    # ALWAYS given
        - Item: Blue_Potion   # ALWAYS given
    - SubGroup: 1      # Algorithm: Random
      List:
        - Item: Weapon1  # ONE random from this pool
        - Item: Weapon2
    - SubGroup: 2      # Algorithm: Random
      List:
        - Item: Card1    # ONE random from this pool
        - Item: Card2
```

When calling `getgroupitem(IG_MultiRewardBox)`:
1. Player gets Red_Potion + Blue_Potion (SubGroup 0)
2. Player gets ONE random weapon (SubGroup 1)
3. Player gets ONE random card (SubGroup 2)

**Field Access**:
| Field | Accessed? |
|-------|-----------|
| GroupID | ✓ |
| Item | ✓ |
| Rate | ✓ |
| Amount | ✓ |
| SubGroup | ✓ (all) |
| Announced | ✓ |
| Duration | ✓ |
| UniqueId | ✓ |
| Bound | ✓ |
| Named | ✓ |

---

## Advanced Features

### 1. Announced Items

Broadcasts to entire server when item is obtained.

```yaml
- Group: JackpotBox
  SubGroups:
    - SubGroup: 1
      List:
        - Index: 0
          Item: Godly_Weapon
          Rate: 1
          Announced: true      # "[PlayerName] has won [Godly Weapon] from 'Box'"
        - Index: 1
          Item: Common_Item
          Rate: 999
          Announced: false     # Silent
```

**Broadcast Format**: `[PlayerName] has won [ItemName] from 'Box'`

---

### 2. Bound Items

Binds item to player/account/guild.

```yaml
- Group: SoulboundRewards
  SubGroups:
    - SubGroup: 1
      List:
        - Index: 0
          Item: Exclusive_Weapon
          Rate: 10
          Bound: Char          # Character-bound (cannot trade/drop)
        - Index: 1
          Item: Account_Item
          Rate: 20
          Bound: Account       # Account-bound
        - Index: 2
          Item: Guild_Prize
          Rate: 30
          Bound: Guild         # Guild-bound
```

**Bound Types**:
- `None` - No binding (default)
- `Account` - Bound to account
- `Guild` - Bound to guild
- `Party` - Bound to party
- `Char` - Bound to character

See `getitembound` in `doc/script_commands.txt` for details.

---

### 3. Named Items

Inscribes the obtainer's name on the item.

```yaml
- Group: CustomWeaponBox
  SubGroups:
    - SubGroup: 1
      List:
        - Index: 0
          Item: Legendary_Sword
          Rate: 1
          Named: true          # Item shows "[PlayerName]'s Legendary Sword"
```

---

### 4. UniqueId Items

Each item gets a unique identifier, preventing stacking with identical items.

```yaml
- Group: AppleBox
  SubGroups:
    - SubGroup: 1
      List:
        - Index: 0
          Item: Apple
          Amount: 3
          UniqueId: true       # Creates 3 separate stacks
```

**Result in Inventory**:
```
3x Apple (UniqueId #1001)
3x Apple (UniqueId #1002)
3x Apple (UniqueId #1003)
```

Each group of 3 apples won't stack with other groups, even from the same box.

---

### 5. Rental Items (Duration)

Items expire after specified minutes.

```yaml
- Group: TemporaryBuffBox
  SubGroups:
    - SubGroup: 1
      List:
        - Index: 0
          Item: Premium_Weapon
          Rate: 10
          Duration: 10080      # 7 days (7 * 24 * 60 minutes)
        - Index: 1
          Item: Trial_Armor
          Rate: 50
          Duration: 1440       # 1 day (24 * 60 minutes)
```

**Note**: Not intended for stackable items.

---

### 6. Refine Levels

Apply random refine levels to equipment.

```yaml
- Group: EnchantedWeaponBox
  SubGroups:
    - SubGroup: 1
      List:
        - Index: 0
          Item: Excalibur
          Rate: 1
          RefineMinimum: 7
          RefineMaximum: 10    # Random +7 to +10
        - Index: 1
          Item: Masamune
          Rate: 5
          RefineMinimum: 5
          RefineMaximum: 7     # Random +5 to +7
```

---

### 7. Random Options

Apply random option groups to equipment.

```yaml
- Group: EnchantedArmorBox
  SubGroups:
    - SubGroup: 1
      List:
        - Index: 0
          Item: Valkyrie_Armor
          Rate: 10
          RandomOptionGroup: RANDOM_OPT_GROUP_WEAPON
        - Index: 1
          Item: Valhalla_Helm
          Rate: 20
          RandomOptionGroup: RANDOM_OPT_GROUP_ARMOR
```

See `db/re/item_randomopt_group.yml` for random option groups.

---

## Complete Examples

### Example 1: Simple Random Box

```yaml
- Group: NewbieBox
  SubGroups:
    - SubGroup: 1
      Algorithm: Random
      List:
        - Index: 0
          Item: Knife
          Rate: 50
          Amount: 1
        - Index: 1
          Item: Cotton_Shirt
          Rate: 30
          Amount: 1
        - Index: 2
          Item: Red_Potion
          Rate: 20
          Amount: 10
```

**Script**:
```c
// In item_db, create the box item
prontera,150,150,4	script	NewbieBox	123,{
	if (countitem(NewbieBox_Item) < 1) {
		mes "You need a Newbie Box!";
		close;
	}
	delitem NewbieBox_Item, 1;
	getrandgroupitem(IG_NewbieBox);
	mes "You obtained an item from the Newbie Box!";
	close;
}
```

---

### Example 2: Multi-Tier Reward System

```yaml
- Group: QuestRewardBox
  SubGroups:
    # Guaranteed consumables
    - SubGroup: 0
      Algorithm: All
      List:
        - Index: 0
          Item: Red_Potion
          Amount: 50
        - Index: 1
          Item: Blue_Potion
          Amount: 30
        - Index: 2
          Item: Butterfly_Wing
          Amount: 10

    # Main equipment reward
    - SubGroup: 1
      Algorithm: Random
      List:
        - Index: 0
          Item: Legendary_Weapon
          Rate: 1
          Announced: true
          Bound: Char
          RefineMinimum: 7
          RefineMaximum: 10
        - Index: 1
          Item: Epic_Armor
          Rate: 9
          RefineMinimum: 5
          RefineMaximum: 7
        - Index: 2
          Item: Rare_Accessory
          Rate: 40
          RefineMinimum: 3
          RefineMaximum: 5
        - Index: 3
          Item: Common_Gear
          Rate: 950

    # Bonus card pool
    - SubGroup: 2
      Algorithm: Random
      List:
        - Index: 0
          Item: MVP_Card
          Rate: 1
          Announced: true
        - Index: 1
          Item: Rare_Card
          Rate: 19
        - Index: 2
          Item: Common_Card
          Rate: 80
```

**Script**:
```c
// Complete reward distribution
OnQuestComplete:
	mes "Quest completed!";
	mes "Here are your rewards...";

	// Give all SubGroup 0 + one from SubGroup 1 + one from SubGroup 2
	getgroupitem(IG_QuestRewardBox, 1);  // 1 = identified

	mes "Check your inventory!";
	close;
```

---

### Example 3: SharedPool Gacha (Limited Pool)

```yaml
- Group: LimitedEventGacha
  SubGroups:
    - SubGroup: 1
      Algorithm: SharedPool
      List:
        - Index: 0
          Item: Grand_Prize
          Rate: 1              # Only 1 in entire pool
          Announced: true
          Bound: Char
        - Index: 1
          Item: First_Prize
          Rate: 5              # 5 in pool
          Announced: true
        - Index: 2
          Item: Second_Prize
          Rate: 20             # 20 in pool
        - Index: 3
          Item: Third_Prize
          Rate: 74             # 74 in pool
```

**Explanation**:
- Total pool: 1 + 5 + 20 + 74 = 100 items
- After 100 draws, pool refills
- Grand Prize guaranteed within 100 draws
- Probability changes as items are drawn

**Script**:
```c
// Gacha machine NPC
prontera,155,185,4	script	Gacha Machine	844,{
	mes "[Gacha Machine]";
	mes "1 try = 100,000 zeny";
	mes "Pull the lever?";
	next;
	if (select("Yes:No") == 2) close;

	if (Zeny < 100000) {
		mes "Not enough zeny!";
		close;
	}

	Zeny -= 100000;
	getrandgroupitem(IG_LimitedEventGacha);
	mes "You got an item!";
	close;
}
```

---

### Example 4: Class-Specific Card Album

```yaml
- Group: CARDALBUM_WEAPON
  SubGroups:
    - SubGroup: 1
      Algorithm: Random
      List:
        - Index: 0
          Item: Poring_Card
          Rate: 800
        - Index: 1
          Item: Drops_Card
          Rate: 800
        - Index: 2
          Item: Andre_Card
          Rate: 600
        - Index: 3
          Item: Hydra_Card
          Rate: 200
        - Index: 4
          Item: Skeleton_Worker_Card
          Rate: 150
        - Index: 5
          Item: Drainliar_Card
          Rate: 100
        - Index: 6
          Item: Thara_Frog_Card
          Rate: 50
        - Index: 7
          Item: Ghostring_Card
          Rate: 10
          Announced: true
        - Index: 8
          Item: Angeling_Card
          Rate: 5
          Announced: true
```

---

## Common Item Boxes

### Old Blue Box (IG_BLUEBOX)

Classic random item box containing equipment, consumables, and rare items.

```c
// Usage
.@item = groupranditem(IG_BLUEBOX);
getitem .@item, 1;

// Or directly
getrandgroupitem(IG_BLUEBOX);
```

**Contents**: 1000+ items including weapons, armor, cards, rare equipment
**Type**: Algorithm Random (constant probabilities)

---

### Old Card Album (IG_CARDALBUM)

Contains random cards from all types.

**Sub-albums**:
- `IG_CARDALBUM` - All cards
- `IG_CARDALBUM_WEAPON` - Weapon cards only
- `IG_CARDALBUM_ARMOR` - Armor cards only
- `IG_CARDALBUM_HELM` - Headgear cards only
- `IG_CARDALBUM_SHIELD` - Shield cards only
- `IG_CARDALBUM_GARMENT` - Garment cards only
- `IG_CARDALBUM_SHOES` - Shoes cards only
- `IG_CARDALBUM_ACC` - Accessory cards only

```c
// General card
getrandgroupitem(IG_CARDALBUM);

// Specific slot card
getrandgroupitem(IG_CARDALBUM_WEAPON);
```

---

### Gift Box (IG_BLUEBOX or custom)

Event-specific gift boxes with holiday/seasonal items.

```c
// Usually custom implementations
getgroupitem(IG_ChristmasGiftBox);
getgroupitem(IG_ValentineBox);
```

---

## Creating Custom Groups

### Step 1: Design Your Group

```yaml
# db/import/item_group_db.yml

Header:
  Type: ITEM_GROUP_DB
  Version: 4

Body:
  - Group: MyDailyRewardBox
    SubGroups:
      # Guaranteed consumables
      - SubGroup: 0
        Algorithm: All
        List:
          - Index: 0
            Item: Red_Potion
            Amount: 10
          - Index: 1
            Item: Blue_Potion
            Amount: 10
          - Index: 2
            Item: Butterfly_Wing
            Amount: 5

      # Random equipment
      - SubGroup: 1
        Algorithm: Random
        List:
          - Index: 0
            Item: Premium_Weapon
            Rate: 5
            Bound: Char
            RefineMinimum: 5
            RefineMaximum: 7
          - Index: 1
            Item: Normal_Armor
            Rate: 25
          - Index: 2
            Item: Basic_Accessory
            Rate: 70
```

### Step 2: Reload Database

```bash
@reloaditemdb
# Or restart server
```

### Step 3: Use in Scripts

```c
// NPC that gives daily reward
prontera,150,150,4	script	Daily Reward	123,{
	// Check if already claimed today
	if (#LastDailyReward >= gettimestr("%Y%m%d", 8)) {
		mes "You already claimed your daily reward!";
		close;
	}

	mes "[Daily Reward]";
	mes "Here's your daily reward!";

	getgroupitem(IG_MyDailyRewardBox, 1);

	#LastDailyReward = atoi(gettimestr("%Y%m%d", 8));
	mes "Come back tomorrow!";
	close;
}
```

### Step 4: Create Box Item (Optional)

```yaml
# db/import/item_db.yml
  - Id: 50000
    AegisName: My_Daily_Box
    Name: Daily Reward Box
    Type: Usable
    Buy: 0
    Weight: 10
    Script: |
      getgroupitem(IG_MyDailyRewardBox);
```

---

## Best Practices

### 1. Rate Calculation

**Remember**: Rate is NOT percentage!

```yaml
# WRONG - Thinking rates are percentages
List:
  - Item: Rare_Item
    Rate: 1      # This is 1/101 = 0.99%, not 1%!
  - Item: Common_Item
    Rate: 100

# CORRECT - Rates as weights
List:
  - Item: Rare_Item
    Rate: 10     # 10/1000 = 1%
  - Item: Common_Item
    Rate: 990    # 990/1000 = 99%
```

### 2. Use Proper Algorithms

```yaml
# For guaranteed bundles - Use All
- SubGroup: 0
  Algorithm: All
  List:
    - Item: Reward1
    - Item: Reward2

# For constant probability - Use Random
- SubGroup: 1
  Algorithm: Random
  List:
    - Item: Prize1
      Rate: 10
    - Item: Prize2
      Rate: 90

# For limited pools - Use SharedPool
- SubGroup: 1
  Algorithm: SharedPool
  List:
    - Item: JackpotItem
      Rate: 1      # Only 1 exists until refill
```

### 3. SubGroup Organization

```yaml
# Clear organization pattern
- Group: MyBox
  SubGroups:
    - SubGroup: 0          # Always: Guaranteed items
      Algorithm: All
    - SubGroup: 1          # Main random pool (default for commands)
      Algorithm: Random
    - SubGroup: 2          # Bonus pool
      Algorithm: Random
    - SubGroup: 3          # Premium pool
      Algorithm: SharedPool
```

### 4. Use Announced for Rare Items

```yaml
List:
  - Index: 0
    Item: Ultra_Rare_MVP_Card
    Rate: 1
    Announced: true        # Let everyone know someone got it!
    Bound: Char
```

### 5. Bind Valuable Items

```yaml
List:
  - Index: 0
    Item: Exclusive_Weapon
    Rate: 10
    Bound: Char           # Prevent trading/selling
    Named: true           # Add player's name
```

### 6. Test Your Probabilities

```c
// Test script to verify rates
-	script	TestItemGroup	-1,{
OnInit:
	.@total = 10000;
	for (.@i = 0; .@i < .@total; .@i++) {
		.@item = groupranditem(IG_MyTestGroup);
		.@count[.@item]++;
	}

	// Display results
	debugmes "Results from " + .@total + " draws:";
	for (.@i = 0; .@i < getarraysize(.@count); .@i++) {
		if (.@count[.@i]) {
			.@name$ = getitemname(.@i);
			.@pct = .@count[.@i] * 100.0 / .@total;
			debugmes .@name$ + ": " + .@count[.@i] + " (" + .@pct + "%)";
		}
	}
	end;
}
```

### 7. Document Your Custom Groups

```yaml
# Add comments to your custom groups
Body:
  # ========================================
  # EVENT: Summer 2024 - Beach Treasure Box
  # Duration: June 1 - August 31
  # ========================================
  - Group: SummerBeachBox
    SubGroups:
      - SubGroup: 1
        Algorithm: Random
        List:
          # Common summer consumables (70%)
          - Index: 0
            Item: Ice_Cream
            Rate: 700
          # Rare summer equipment (29%)
          - Index: 1
            Item: Beach_Umbrella_Hat
            Rate: 290
          # Ultra rare summer mount (1%)
          - Index: 2
            Item: Surfboard_Mount
            Rate: 10
            Announced: true
```

### 8. Avoid Common Mistakes

```yaml
# WRONG - Using All algorithm with rates
- SubGroup: 0
  Algorithm: All
  List:
    - Item: Item1
      Rate: 50         # ❌ Rate ignored with All algorithm!

# CORRECT
- SubGroup: 0
  Algorithm: All
  List:
    - Item: Item1      # ✓ No rate needed

# WRONG - Forgetting Index for duplicate items
- SubGroup: 1
  List:
    - Item: Red_Potion
      Amount: 5
    - Item: Red_Potion   # ❌ Duplicate without different Index!
      Amount: 10

# CORRECT - Use Index to differentiate
- SubGroup: 1
  List:
    - Index: 0
      Item: Red_Potion
      Amount: 5
      Rate: 70
    - Index: 1
      Item: Red_Potion
      Amount: 10
      Rate: 30
```

---

## Troubleshooting

### Issue: Items not dropping

**Check**:
1. Group name matches constant (IG_GroupName)
2. Database reloaded (@reloaditemdb)
3. Rate values are non-zero (except for All algorithm)
4. Item exists in item_db

```c
// Debug script
mes "Testing group...";
.@result = getrandgroupitem(IG_MyGroup);
if (.@result)
	mes "Success!";
else
	mes "Failed! Check console for errors.";
```

### Issue: Wrong probabilities

**Check**:
1. Rate is weight, not percentage
2. Calculate: item_rate / sum_of_all_rates
3. Algorithm type (SharedPool changes over time)

```c
// Verify calculation
// If Item A: Rate 10, Item B: Rate 90
// Total = 100
// Item A chance = 10/100 = 10%
// Item B chance = 90/100 = 90%
```

### Issue: SharedPool not refilling

**Solution**: Server restart or wait until pool is completely empty.

### Issue: Equipment given identified

**Solution**: Use `identify` parameter:
```c
getgroupitem(IG_MyGroup, 0);   // 0 = unidentified
getgroupitem(IG_MyGroup, 1);   // 1 = identified
```

---

## Related References

- **Script Commands**: [KB_REF_ScriptCommandsCore.md], [KB_REF_ScriptCommandsExpanded.md]
- **Item Database**: [KB_REF_DatabaseStructure.md]
- **Constants**: [KB_REF_Constants.md]
- **Random Options**: `db/re/item_randomopt_group.yml`
- **Documentation**: `doc/item_group.txt`

---

**End of KB_REF_019 - Item Groups & Random Box System**
