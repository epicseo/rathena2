# rAthena Content Creation Complete Guide v4.0

**Version:** 4.0 - RAG-Optimized Complete Edition
**File Size:** ~5K lines (merged from 3 files)
**Coverage:** 100% content designer workflow
**Last Updated:** 2025-11-19

---

<!-- RAG_CHUNK: 06_overview -->
## 📦 What's in This File

> **🎯 Context Box: Complete Content Creator Toolkit**
> This file merges ALL content creation guides from v3.1:
> - **Item Groups** (gacha/random boxes, loot tables)
> - **Quest System** (quest_db.yml structure, TimeLimit formats)
> - **NPC Scripting Patterns** (12 production-ready patterns)
>
> Previously scattered across 3 files (ItemGroups + QuestSystem + NPCScriptingPatterns).
> Now unified for complete content creation workflow: Design → Implement → Optimize

### Merged Content

| Section | Original File | Lines | Topics |
|---------|--------------|-------|--------|
| **Part 1: Item Groups** | KB_REF_ItemGroups.md | 1,219 | Gacha, random boxes, loot tables |
| **Part 2: Quest System** | KB_REF_QuestSystem.md | 648 | quest_db.yml, TimeLimit, Targets |
| **Part 3: NPC Patterns** | KB_REF_NPCScriptingPatterns.md | 2,972 | 12 production patterns |
| **Total** | 3 files → 1 file | **4,839** | **Content creation** |

---

<!-- RAG_CHUNK: 06_quick_reference -->
## 🔍 Quick Reference

### Find What You Need Fast

| I need to... | Go to section | Keywords to search |
|-------------|---------------|-------------------|
| **Create gacha/random box** | Part 1: Item Groups | item_group_db, Algorithm, SubGroup |
| **Understand probability** | Part 1: Item Groups | Rate, Random, SharedPool |
| **Create quest** | Part 2: Quest System | quest_db, Targets, Drops |
| **Weekly/timed quest** | Part 2: Quest System | TimeLimit, Monday, "+1h" |
| **Advanced quest targets** | Part 2: Quest System | Race, Size, Element, MinLevel |
| **NPC state machine** | Part 3: NPC Patterns | Pattern 1: State Machines |
| **Cooldown system** | Part 3: NPC Patterns | Pattern 2: Cooldown Systems |
| **Instance management** | Part 3: NPC Patterns | Pattern 3: Instance Management |
| **Anti-cheat** | Part 3: NPC Patterns | Pattern 4: Anti-Cheat |

### Quick Lookups

```
Item Groups:
  - Algorithm: Random, All, SharedPool
  - SubGroup: 0 (must items), 1-99 (random pools)
  - Fields: Rate, Amount, Announced, Bound, Named

Quest System:
  - TimeLimit: "+1h" (relative), "Monday 4h" (absolute)
  - Targets: Simple (Mob + Count) or Advanced (Race, Size, Element)
  - Drops: Mob, Item, Count, Rate

NPC Patterns (12):
  1. State Machines
  2. Cooldown Systems
  3. Instance Management
  4. Anti-Cheat Patterns
  5. Currency Systems
  6. Ranking/Leaderboard
  7. Event Management
  8. Multi-Stage Quests
  9. Conditional Rewards
  10. Dynamic Difficulty
  11. Persistent Player Data
  12. Shop Systems
```

### Cross-References to Other Files

**Need syntax or constants? Load these:**
- **02_SCRIPTING_COMPLETE.md** - getgroupitem, setquest, checkquest, NPC syntax
- **03_GAME_MECHANICS.md** - RC_* (race), Ele_* (element), Size_*, SC_*, bonus constants
- **08_SCRIPT_INTERNALS.md** - Understanding script crashes, timer safety

---

<!-- RAG_CHUNK: 06_usage_guide -->
## 📖 How to Use This File

### For Content Creators
1. **Creating gacha boxes** → Part 1: Item Groups
2. **Creating quests** → Part 2: Quest System
3. **Creating NPCs** → Part 3: NPC Patterns + **02_SCRIPTING_COMPLETE.md**
4. **Complete systems** → Use all three parts together

### Workflow Example: Creating Complete Quest System
```
Step 1: Design quest in quest_db.yml (Part 2: Quest System)
Step 2: Create reward items/gacha (Part 1: Item Groups)
Step 3: Implement quest NPC (Part 3: NPC Patterns + 02_SCRIPTING_COMPLETE)
Step 4: Add constants if needed (03_GAME_MECHANICS)
```

### For AI/LLM Systems
**Load this file when user asks about:**
- "Create gacha" / "random box" / "item group"
- "Create quest" / "quest_db" / "TimeLimit"
- "NPC pattern" / "state machine" / "cooldown"
- "How to create [system]"

**Always combine with:**
- **02_SCRIPTING_COMPLETE.md** for command syntax
- **03_GAME_MECHANICS.md** for constants

---

<!-- RAG_CHUNK: 06_file_structure -->
## 📂 File Structure

```
04_CONTENT_CREATION.md (this file)
│
├── Part 1: ITEM GROUPS (~1.2K lines)
│   ├── Database Structure (item_group_db.yml)
│   ├── Algorithm Types (Random, All, SharedPool)
│   ├── SubGroup System
│   ├── Special Fields (Announced, Bound, Named, etc.)
│   ├── Probability Calculations
│   ├── Script Command Integration
│   └── Complete Gacha Examples
│
├── Part 2: QUEST SYSTEM (~648 lines)
│   ├── Database Structure (quest_db.yml)
│   ├── TimeLimit Formats (relative vs absolute)
│   ├── Target Configuration (simple vs advanced)
│   ├── Drop Configuration
│   ├── Level/Location Restrictions
│   ├── Script Command Integration
│   └── Complete Quest Examples
│
└── Part 3: NPC SCRIPTING PATTERNS (~3K lines)
    ├── Pattern 1: State Machines
    ├── Pattern 2: Cooldown Systems
    ├── Pattern 3: Instance Management
    ├── Pattern 4: Anti-Cheat Patterns
    ├── Pattern 5: Currency Systems
    ├── Pattern 6: Ranking/Leaderboard
    ├── Pattern 7: Event Management
    ├── Pattern 8: Multi-Stage Quests
    ├── Pattern 9: Conditional Rewards
    ├── Pattern 10: Dynamic Difficulty
    ├── Pattern 11: Persistent Player Data
    └── Pattern 12: Shop Systems
```

---

<!-- RAG_CHUNK: 06_key_takeaways -->
## 🎯 Content Creation Key Takeaways

### Why This File Exists
- **Complete Workflow:** Item groups → Quests → NPC implementation in one place
- **Reduced Fragmentation:** Was 3 files, now 1 file
- **Better RAG:** AI loads one file for all content creation queries
- **100% Content:** All v3.1 content creation guides preserved

### Common Query Patterns

**Pattern 1: Gacha Box Creation**
```
User: "How to create gacha with announced rare drops?"
Load: 04_CONTENT_CREATION.md (Part 1: Algorithm + Announced field)
Then: 02_SCRIPTING_COMPLETE.md (getgroupitem syntax)
```

**Pattern 2: Quest Creation**
```
User: "How to create weekly quest that resets Monday?"
Load: 04_CONTENT_CREATION.md (Part 2: TimeLimit absolute format)
Then: 02_SCRIPTING_COMPLETE.md (setquest, checkquest)
Then: 03_GAME_MECHANICS.md (if using Race/Element filters)
```

**Pattern 3: Complete NPC System**
```
User: "Create cooldown-based event NPC"
Load: 04_CONTENT_CREATION.md (Part 3: Cooldown pattern)
Then: 02_SCRIPTING_COMPLETE.md (syntax reference)
```

---

## 📊 Statistics

- **Item Group Examples:** 10+ complete gacha systems
- **Quest Examples:** 15+ quest types (kill, timed, weekly, race-based)
- **NPC Patterns:** 12 production-ready patterns
- **Code Examples:** 100+ working snippets
- **Total Lines:** ~4,839 lines

---

# ═══════════════════════════════════════════════════════════════
# PART 1: ITEM GROUPS (GACHA/RANDOM BOXES)
# ═══════════════════════════════════════════════════════════════
<!-- RAG_CHUNK: 06_item_groups_complete -->

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

<!-- RAG_CHUNK: 06_Table -->
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

<!-- RAG_CHUNK: 06_System -->
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

<!-- RAG_CHUNK: 06_Database -->
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

<!-- RAG_CHUNK: 06_Algorithm -->
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

<!-- RAG_CHUNK: 06_SubGroup -->
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

<!-- RAG_CHUNK: 06_Script -->
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

<!-- RAG_CHUNK: 06_Advanced -->
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

<!-- RAG_CHUNK: 06_Complete -->
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

<!-- RAG_CHUNK: 06_Common -->
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

<!-- RAG_CHUNK: 06_Creating -->
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

<!-- RAG_CHUNK: 06_Best -->
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

<!-- RAG_CHUNK: 06_Troubleshooting -->
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

<!-- RAG_CHUNK: 06_Related -->
## Related References

- **Script Commands**: [KB_REF_ScriptCommandsCore.md], [KB_REF_ScriptCommandsExpanded.md]
- **Item Database**: [KB_REF_DatabaseStructure.md]
- **Constants**: [KB_REF_Constants.md]
- **Random Options**: `db/re/item_randomopt_group.yml`
- **Documentation**: `doc/item_group.txt`

---

**End of KB_REF_019 - Item Groups & Random Box System**


# ═══════════════════════════════════════════════════════════════
# PART 2: QUEST SYSTEM (quest_db.yml)
# ═══════════════════════════════════════════════════════════════
<!-- RAG_CHUNK: 06_quest_system_complete -->

---
kb_id: KB_REF_002
kb_type: reference
kb_category: database
kb_subcategory: quest_system
kb_keywords: [quest, quest_db, YAML, objectives, targets, drops, rewards, TimeLimit, mob kill, quest system, quest database]
kb_related: [KB_DB_001, KB_EXAMPLE_005]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2022-06-29
kb_use_case: [quest_creation, content_creation, quest_scripting]
---

# rAthena Quest Database Structure

Complete reference for the quest database structure in `/db/(pre-)re/quest_db.yml`.

<!-- RAG_CHUNK: 06_Overview -->
## Overview

The quest database defines all quests available in rAthena, including their objectives, time limits, drop rates, and rewards. Quests are configured using YAML format.

**Database Location:** `/db/(pre-)re/quest_db.yml`

---

<!-- RAG_CHUNK: 06_QUEST -->
## QUEST STRUCTURE

### Basic Quest Format

```yaml
- Id: 1000
  Title: Quest Name
  TimeLimit: <optional>
  Targets: <optional>
  Drops: <optional>
```

---

<!-- RAG_CHUNK: 06_FIELD -->
## FIELD REFERENCE

### Id (Required)
**Type:** Integer
**Description:** Unique quest identifier

**Example:**
```yaml
- Id: 1000
  Title: Poring Hunt
```

**Notes:**
- Must be unique across all quests
- Used in script commands like `questprogress()`, `setquest()`, `completequest()`
- Standard range: User quests typically start from 1000+

---

### Title (Required)
**Type:** String
**Description:** Display name of the quest shown to players

**Example:**
```yaml
- Id: 1000
  Title: Hunt 10 Porings
```

**Notes:**
- Shown in quest log UI
- Can contain spaces and special characters
- Keep concise for UI readability

---

### TimeLimit (Optional)
**Type:** String
**Description:** Quest expiration time or duration

Quest time limits can be specified in two ways:

#### **1. Relative Time Limit (Duration)**

Format: `+<time>` (starts when quest is taken)

**Syntax:** `+[d]d [h]h [mn]mn [s]s`
- `d` = days (optional)
- `h` = hours [0-23] (optional)
- `mn` = minutes [0-59] (optional)
- `s` = seconds [0-59] (optional)

**Examples:**
```yaml
# Quest expires 5 minutes after being taken
- Id: 2069
  Title: Tierra Gorge Battle
  TimeLimit: +5mn

# Quest expires 2 hours after being taken
- Id: 1001
  Title: Timed Challenge
  TimeLimit: +2h

# Quest expires 1 day and 30 minutes after being taken
- Id: 1002
  Title: Daily Quest Extended
  TimeLimit: +1d 30mn

# Quest expires 3 days, 12 hours, 30 minutes after being taken
- Id: 1003
  Title: Long Term Quest
  TimeLimit: +3d 12h 30mn
```

#### **2. Absolute Time Limit (Fixed Expiration)**

Format: `<date/day> <time>` (expires at specific time)

**Syntax (Option 1):** `<d>d [h]h [mn]mn [s]s`
**Syntax (Option 2):** `<DayOfWeek> [h]h [mn]mn [s]s`

**Examples:**
```yaml
# Quest expires 3 days from now at 4am
- Id: 9419
  Title: Attack Sky Fortress
  TimeLimit: 3d 4h

# Quest expires next Monday at 4am
- Id: 5965
  Title: "[Standby] Devil's Special"
  TimeLimit: Monday 4h

# Quest expires next Friday at 23:30
- Id: 1004
  Title: Weekly Challenge
  TimeLimit: Friday 23h 30mn

# Quest expires in 7 days at midnight
- Id: 1005
  Title: Week-Long Quest
  TimeLimit: 7d 0h
```

**Days of Week:** Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday

---

### Targets (Optional)
**Type:** Array
**Description:** Quest objectives - monsters to kill or conditions to meet

Targets can be defined in two ways:

#### **Method 1: Simple Mob Targeting**

Used for straightforward "kill X monsters" quests.

**Required Fields:**
- `Mob`: Monster name (AegisName from mob_db)
- `Count`: Number of monsters to kill

**Example:**
```yaml
Targets:
  - Mob: PORING
    Count: 10
  - Mob: DROPS
    Count: 5
```

**Notes:**
- `Count: 0` will skip the target on import (useful for disabled objectives)
- Mob must exist in `mob_db.yml`

---

#### **Method 2: Advanced Targeting (Race/Size/Element/Level)**

Used for flexible targeting by monster characteristics.

**Required Fields:**
- `Id`: Unique target index (positive number)
- `Count`: Number of kills required

**Optional Filters:**
- `Race`: Monster race filter
- `Size`: Monster size filter
- `Element`: Monster element filter
- `MinLevel`: Minimum monster level
- `MaxLevel`: Maximum monster level
- `Location`: Map where kills count
- `MapName`: Display name for location
- `MapMobTargets`: Specific monster whitelist/blacklist

**Example:**
```yaml
Targets:
  # Kill any 20 Demon-race monsters
  - Id: 1
    Count: 20
    Race: Demon

  # Kill 15 large monsters
  - Id: 2
    Count: 15
    Size: Large

  # Kill 10 Fire-element monsters between level 50-70
  - Id: 3
    Count: 10
    Element: Fire
    MinLevel: 50
    MaxLevel: 70

  # Kill 30 monsters on a specific map
  - Id: 4
    Count: 30
    Location: prontera
    MapName: Prontera
```

---

### Target Field Details

#### **Race**
**Valid Values:** `Angel`, `Brute`, `DemiHuman`, `Demon`, `Dragon`, `Fish`, `Formless`, `Insect`, `Plant`, `Undead`, `All`

**Default:** `All`

**Example:**
```yaml
Targets:
  - Id: 1
    Count: 25
    Race: Undead    # Only Undead monsters count
```

---

#### **Size**
**Valid Values:** `Small`, `Medium`, `Large`, `All`

**Default:** `All`

**Example:**
```yaml
Targets:
  - Id: 1
    Count: 15
    Size: Large     # Only Large monsters count
```

---

#### **Element**
**Valid Values:** `Dark`, `Earth`, `Fire`, `Ghost`, `Holy`, `Neutral`, `Poison`, `Undead`, `Water`, `Wind`, `All`

**Default:** `All`

**Example:**
```yaml
Targets:
  - Id: 1
    Count: 20
    Element: Fire   # Only Fire-element monsters count
```

---

#### **MinLevel / MaxLevel**
**Type:** Integer
**Default:**
- `MinLevel`: 1 (if MaxLevel defined)
- `MaxLevel`: No limit

**Notes:**
- Set to `0` to ignore the limit on import

**Example:**
```yaml
Targets:
  # Kill monsters level 30-50
  - Id: 1
    Count: 50
    MinLevel: 30
    MaxLevel: 50

  # Kill monsters level 80+
  - Id: 2
    Count: 20
    MinLevel: 80
```

---

#### **Location / MapName**
**Location Type:** String (map name without .gat)
**MapName Type:** String (display name)

**Example:**
```yaml
Targets:
  - Id: 1
    Count: 100
    Location: prontera
    MapName: Prontera City
```

**Notes:**
- Kills only count on the specified map
- `MapName` is shown in the quest UI

---

#### **MapMobTargets**
**Type:** Dictionary
**Description:** Whitelist/blacklist specific monsters by name

**Format:**
```yaml
MapMobTargets:
  <MonsterName>: <true/false>
```

- `true`: Add monster to whitelist
- `false`: Remove monster from whitelist

**Example:**
```yaml
Targets:
  - Id: 1
    Count: 50
    Location: prontera
    MapMobTargets:
      PORING: true       # Only Porings count
      DROPS: true        # Drops also count
      POPORING: true     # Poporings also count
```

**Notes:**
- Only active when using `Id` method (not `Mob` method)
- Allows precise control over which monsters count

---

<!-- RAG_CHUNK: 06_DROPS -->
## DROPS

**Type:** Array
**Description:** Quest-specific item drop configuration

When a quest is active, you can configure special drops from monsters.

**Fields:**
- `Mob`: Monster ID or name (0 = all monsters)
- `Item`: Item name (AegisName from item_db)
- `Count`: Number of items that drop
- `Rate`: Drop rate (10000 = 100%)

**Example:**
```yaml
Drops:
  # Drop Quest Item from specific monster
  - Mob: PORING
    Item: Jellopy
    Count: 1
    Rate: 5000        # 50% drop rate

  # Drop from any monster
  - Mob: 0
    Item: Quest_Token
    Count: 1
    Rate: 1000        # 10% drop rate

  # Drop multiple items at once
  - Mob: BOSS_MONSTER
    Item: Rare_Item
    Count: 3
    Rate: 10000       # 100% drop rate (3 items)
```

**Notes:**
- `Mob: 0` applies to ALL monsters
- `Count` defaults to 1 for non-stackable items
- `Rate` is in basis points (10000 = 100%, 5000 = 50%, 100 = 1%, 1 = 0.01%)
- Drops only occur while quest is active

---

<!-- RAG_CHUNK: 06_COMPLETE -->
## COMPLETE QUEST EXAMPLES

### Example 1: Simple Kill Quest
```yaml
- Id: 1000
  Title: Poring Extermination
  Targets:
    - Mob: PORING
      Count: 30
```

**Description:** Kill 30 Porings. No time limit.

---

### Example 2: Timed Quest with Drops
```yaml
- Id: 1001
  Title: Emergency Poring Alert
  TimeLimit: +1h
  Targets:
    - Mob: PORING
      Count: 50
  Drops:
    - Mob: PORING
      Item: Poring_Coin
      Count: 1
      Rate: 5000
```

**Description:** Kill 50 Porings within 1 hour. Porings have 50% chance to drop Poring Coin.

---

### Example 3: Multi-Target Quest
```yaml
- Id: 1002
  Title: Slime Cleanup
  Targets:
    - Mob: PORING
      Count: 20
    - Mob: DROPS
      Count: 15
    - Mob: POPORING
      Count: 10
```

**Description:** Kill 20 Porings, 15 Drops, and 10 Poporings.

---

### Example 4: Advanced Race/Element Quest
```yaml
- Id: 1003
  Title: Demon Hunter
  TimeLimit: +1d
  Targets:
    - Id: 1
      Count: 50
      Race: Demon
      MinLevel: 40
      MaxLevel: 80
```

**Description:** Kill 50 Demon-race monsters between level 40-80 within 24 hours.

---

### Example 5: Location-Specific Quest
```yaml
- Id: 1004
  Title: Prontera Patrol
  Targets:
    - Id: 1
      Count: 100
      Location: prt_fild08
      MapName: Prontera Field
```

**Description:** Kill 100 monsters in Prontera Field (prt_fild08).

---

### Example 6: Weekly Quest
```yaml
- Id: 1005
  Title: Weekly Challenge
  TimeLimit: Monday 4h
  Targets:
    - Id: 1
      Count: 200
      Race: Undead
  Drops:
    - Mob: 0
      Item: Weekly_Token
      Count: 1
      Rate: 2000
```

**Description:** Kill 200 Undead-race monsters before Monday 4am. All monsters have 20% chance to drop Weekly Token.

---

### Example 7: Boss Hunt Quest
```yaml
- Id: 1006
  Title: MVP Elimination
  Targets:
    - Mob: EDDGA
      Count: 1
    - Mob: OSIRIS
      Count: 1
    - Mob: BAPHOMET
      Count: 1
  Drops:
    - Mob: EDDGA
      Item: Eddga_Trophy
      Count: 1
      Rate: 10000
    - Mob: OSIRIS
      Item: Osiris_Trophy
      Count: 1
      Rate: 10000
    - Mob: BAPHOMET
      Item: Baphomet_Trophy
      Count: 1
      Rate: 10000
```

**Description:** Kill Eddga, Osiris, and Baphomet once each. Each drops a guaranteed trophy item.

---

## QUEST SCRIPT COMMANDS

Use these script commands to interact with quests:

### setquest(<quest_id>)
Gives the quest to the player.

```c
setquest(1000);  // Start quest 1000
```

---

### completequest(<quest_id>)
Marks the quest as completed.

```c
if (questprogress(1000, PLAYTIME) == 2) {
    completequest(1000);
    mes "Quest completed!";
}
```

---

### erasequest(<quest_id>)
Removes the quest from the player.

```c
erasequest(1000);  // Remove quest 1000
```

---

### questprogress(<quest_id>{, <type>})
Checks quest progress.

**Types:**
- `PLAYTIME` (0): Check if quest time expired
- `HUNTING` (1): Check if hunt objectives completed
- `HUNTING | PLAYTIME` (2): Check both

**Returns:**
- `0`: Quest not started
- `1`: Quest active
- `2`: Quest complete/expired

```c
if (questprogress(1000, HUNTING) == 2) {
    mes "You completed all hunt objectives!";
}
```

---

### checkquest(<quest_id>{, <type>})
Alias for `questprogress()`.

---

## QUEST STATUS VALUES

| Value | Constant | Meaning |
|-------|----------|---------|
| 0 | QUEST_NOT_STARTED | Quest not started |
| 1 | QUEST_ACTIVE | Quest active/in progress |
| 2 | QUEST_COMPLETE | Quest completed |

---

<!-- RAG_CHUNK: 06_BEST -->
## BEST PRACTICES

1. **Unique IDs:** Always use unique quest IDs (avoid conflicts)
2. **Time Limits:** Use relative time (`+`) for recurring quests, absolute time for weekly/event quests
3. **Drop Rates:** Balance drop rates carefully (too high = no challenge, too low = frustration)
4. **Target Count:** Set `Count: 0` to temporarily disable objectives without deleting them
5. **Testing:** Test time limits thoroughly (server timezone matters!)
6. **Performance:** Avoid `Mob: 0` (all monsters) for drops when possible - use specific mobs
7. **UI Display:** Keep `Title` and `MapName` short for better UI display

---

<!-- RAG_CHUNK: 06_COMMON -->
## COMMON MISTAKES

### ❌ Wrong:
```yaml
- Id: 1000
  Title: Kill Quest
  TimeLimit: 5mn           # Missing +
  Targets:
    - Mob: INVALID_MOB     # Mob doesn't exist
      Count: -5            # Negative count
```

### ✓ Correct:
```yaml
- Id: 1000
  Title: Kill Quest
  TimeLimit: +5mn          # Relative time
  Targets:
    - Mob: PORING          # Valid mob from mob_db
      Count: 10            # Positive count
```

---

<!-- RAG_CHUNK: 06_RELATED -->
## RELATED FILES

- `/db/(pre-)re/quest_db.yml` - Quest database
- `/doc/script_commands.txt` - Quest-related script commands
- `/db/(pre-)re/mob_db.yml` - Monster names for Targets
- `/db/(pre-)re/item_db.yml` - Item names for Drops

---

<!-- RAG_CHUNK: 06_SEE -->
## SEE ALSO

- **KB_EXAMPLE_005:** Quest Implementation Examples
- **KB_CMD_015:** Quest Script Commands
- **KB_DB_001:** Database System Overview

---

*Last Updated: 2022-06-29*
*rAthena Documentation*


# ═══════════════════════════════════════════════════════════════
# PART 3: NPC SCRIPTING PATTERNS (PRODUCTION-READY)
# ═══════════════════════════════════════════════════════════════
<!-- RAG_CHUNK: 06_npc_patterns_complete -->

---
kb_id: KB_REF_040
title: "Advanced NPC Scripting Patterns & Best Practices"
category: Script Development
keywords: [npc_scripting, state_machines, cooldown_systems, point_systems, instanced_events, dynamic_shops, mini_games, auction_systems, guild_systems, achievements, random_events, anti_cheat, quest_tracking, script_patterns, memory_efficient, security]
related_files: [
  "npc/custom/",
  "src/map/script.cpp",
  "src/map/script.hpp",
  "src/map/npc.cpp",
  "src/map/instance.cpp",
  "KB_REF_ScriptTimerInternals.md",
  "KB_REF_SecurityExploits.md"
]
difficulty: advanced
use_case: "Master-level NPC scripting patterns for complex game systems with security and performance optimization"
version: rAthena 2024
last_updated: 2024-01-15
---

# Advanced NPC Scripting Patterns & Best Practices

## 🎯 Purpose

This document provides **production-ready** patterns for advanced NPC scripting systems. Each pattern includes:
- Complete working implementation
- Security considerations (anti-cheat, exploit prevention)
- Memory-efficient design
- Performance optimization
- Common pitfalls and how to avoid them

---

## 📋 Table of Contents

1. [State Machine Pattern](#state-machine-pattern)
2. [Cooldown Systems](#cooldown-systems)
3. [Point Accumulation Systems](#point-systems)
4. [Instanced Event Pattern](#instanced-events)
5. [Dynamic Shop Systems](#dynamic-shops)
6. [Mini-Game Implementations](#mini-games)
7. [Auction System Pattern](#auction-system)
8. [Guild Contribution Systems](#guild-systems)
9. [Achievement Tracking](#achievement-tracking)
10. [Random World Event Pattern](#random-events)
11. [Anti-Cheat Patterns](#anti-cheat-patterns)
12. [Performance Optimization](#performance-optimization)

---

<!-- RAG_CHUNK: 06_1 -->
## 1. State Machine Pattern {#state-machine-pattern}

### Use Cases
- Multi-step quests with branching paths
- Complex dialogue trees
- Progressive unlock systems
- Tutorial sequences

### Basic State Machine Implementation

```cpp
// npc/custom/quest_statemachine.txt
//===================================================================
// Multi-Step Quest with State Tracking
//===================================================================

prontera,155,185,4	script	Quest Master	4_M_SAGE_A,{

	// Get current quest state (0 = not started)
	.@state = #QUEST_STATE;

	switch (.@state) {
		case 0: // Quest not started
			mes "[Quest Master]";
			mes "Welcome! Are you ready for an epic quest?";
			next;
			if (select("Yes, I'm ready!:Maybe later") == 2) {
				mes "[Quest Master]";
				mes "Come back when you're ready.";
				close;
			}

			mes "[Quest Master]";
			mes "Excellent! First, bring me ^FF000010 Red Potions^000000.";
			#QUEST_STATE = 1;  // Advance to state 1
			#QUEST_TIMER = gettimetick(2);  // Track start time
			close;

		case 1: // Collecting Red Potions
			mes "[Quest Master]";
			if (countitem(501) < 10) {
				mes "You need ^FF000010 Red Potions^000000.";
				mes "Current: ^0000FF" + countitem(501) + "^000000/10";
				close;
			}

			mes "Perfect! You brought the potions.";
			next;
			mes "[Quest Master]";
			mes "Next, you must defeat ^FF000010 Porings^000000.";
			mes "I'll track your progress.";

			delitem 501, 10;  // Take items
			#QUEST_STATE = 2;  // Advance to state 2
			#QUEST_KILLS = 0;  // Initialize kill counter
			close;

		case 2: // Killing Porings
			mes "[Quest Master]";
			mes "Progress: ^0000FF" + #QUEST_KILLS + "^000000/10 Porings defeated.";

			if (#QUEST_KILLS < 10) {
				mes "Keep hunting!";
				close;
			}

			next;
			mes "[Quest Master]";
			mes "Excellent work! Now for the final test...";
			mes "Bring me a rare ^FF0000Poring Card^000000!";

			#QUEST_STATE = 3;  // Advance to state 3
			close;

		case 3: // Collecting Poring Card
			mes "[Quest Master]";
			if (countitem(4001) < 1) {
				mes "The legendary Poring Card awaits!";
				close;
			}

			mes "Incredible! You actually found one!";
			next;
			mes "[Quest Master]";
			mes "You've proven yourself worthy.";
			mes "Accept this reward!";

			// Calculate time bonus
			.@elapsed = gettimetick(2) - #QUEST_TIMER;
			.@time_bonus = (.@elapsed < 3600) ? 5000 : 1000;  // Bonus if < 1 hour

			delitem 4001, 1;
			getitem 607, 1;  // Yggdrasil Berry
			Zeny += 50000 + .@time_bonus;
			getexp 100000, 50000;

			#QUEST_STATE = 4;  // Mark as completed
			#QUEST_COMPLETE_TIME = gettimetick(2);

			announce strcharinfo(0) + " has completed the Epic Quest!", bc_all;
			close;

		case 4: // Already completed
			mes "[Quest Master]";
			mes "You've already completed my quest.";
			mes "Thank you for your service!";

			// Offer repeatable daily quest
			if (gettimetick(2) - #QUEST_COMPLETE_TIME >= 86400) {
				next;
				mes "[Quest Master]";
				mes "Actually, I have a ^0000FFdaily task^000000 if you're interested.";
				if (select("Tell me more:No thanks") == 1) {
					callfunc "F_DailyQuest";
				}
			}
			close;
	}

	end;
}

// Kill counter for state 2
-	script	QuestKillCounter	-1,{
OnNPCKillEvent:
	if (#QUEST_STATE != 2) end;  // Only track in state 2

	if (killedrid == 1002) {  // Poring
		#QUEST_KILLS++;

		dispbottom "Poring defeated! Progress: " + #QUEST_KILLS + "/10";

		if (#QUEST_KILLS >= 10) {
			dispbottom "You've defeated enough Porings! Return to the Quest Master.";
		}
	}
	end;
}
```

### Advanced State Machine with Branching

```cpp
// Complex quest with multiple paths
prontera,150,180,4	script	Choice Quest	4_F_SISTER,{

	.@state = CHOICE_QUEST;
	.@path = CHOICE_PATH;  // 1=combat, 2=stealth, 3=diplomatic

	switch (.@state) {
		case 0: // Introduction
			mes "[Quest Giver]";
			mes "A valuable artifact has been stolen!";
			mes "How will you retrieve it?";
			next;

			switch (select("Fight my way in:Sneak past guards:Negotiate with thieves")) {
				case 1:
					CHOICE_PATH = 1;
					mes "You've chosen the path of combat!";
					break;
				case 2:
					CHOICE_PATH = 2;
					mes "You've chosen the path of stealth!";
					break;
				case 3:
					CHOICE_PATH = 3;
					mes "You've chosen the path of diplomacy!";
					break;
			}

			CHOICE_QUEST = 1;
			close;

		case 1: // Execute chosen path
			switch (.@path) {
				case 1:  // Combat path
					callfunc "F_CombatPath", .@state;
					break;
				case 2:  // Stealth path
					callfunc "F_StealthPath", .@state;
					break;
				case 3:  // Diplomatic path
					callfunc "F_DiplomaticPath", .@state;
					break;
			}
			break;
	}

	end;
}
```

### State Machine Best Practices

```cpp
// ✅ BEST PRACTICES:
// 1. Use account variables (#) for persistent state
// 2. Always validate state transitions
// 3. Provide clear progress feedback
// 4. Handle edge cases (player logout during quest)
// 5. Add time tracking for analytics

// ❌ COMMON MISTAKES:
// 1. Using temporary variables (.@) for state (lost on script end)
// 2. Not validating item counts before state transition
// 3. Forgetting to reset quest on failure
// 4. No way to reset broken quest state

// State reset command for GMs/debugging
function	script	F_ResetQuest	{
	.@quest_id = getarg(0);

	switch (.@quest_id) {
		case 1:  // Epic Quest
			#QUEST_STATE = 0;
			#QUEST_KILLS = 0;
			#QUEST_TIMER = 0;
			#QUEST_COMPLETE_TIME = 0;
			break;
	}

	return 1;
}
```

---

<!-- RAG_CHUNK: 06_2 -->
## 2. Cooldown Systems {#cooldown-systems}

### Pattern Types

**1. Simple Per-Character Cooldown**
**2. Daily Reset Cooldown**
**3. Weekly Reset Cooldown**
**4. Global Server Cooldown**
**5. Item-Specific Cooldown**

### Implementation: Daily Cooldown System

```cpp
// npc/custom/daily_dungeon.txt
//===================================================================
// Daily Dungeon with Cooldown
//===================================================================

prontera,160,180,4	script	Daily Dungeon	4_M_MOCASS1,{

	// Check if player has done today's dungeon
	.@last_run = #DAILY_DUNGEON_TIME;
	.@today = gettimetick(2) / 86400;  // Days since epoch

	mes "[Dungeon Master]";

	if (.@last_run >= .@today) {
		.@reset_time = (.@today + 1) * 86400;  // Next midnight
		.@hours_left = (.@reset_time - gettimetick(2)) / 3600;
		.@mins_left = ((.@reset_time - gettimetick(2)) % 3600) / 60;

		mes "You've already completed today's dungeon.";
		mes "Time until reset: ^FF0000" + .@hours_left + " hours, " + .@mins_left + " minutes^000000";
		close;
	}

	mes "Welcome to the Daily Dungeon!";
	mes "Difficulty increases each day you complete it.";
	next;

	// Calculate difficulty based on streak
	.@streak = #DAILY_DUNGEON_STREAK;
	.@difficulty = min(.@streak / 5 + 1, 10);  // Max difficulty 10

	mes "[Dungeon Master]";
	mes "Current Streak: ^0000FF" + .@streak + " days^000000";
	mes "Difficulty Level: ^FF0000" + .@difficulty + "^000000/10";
	next;

	if (select("Enter Dungeon:Maybe later") == 2) {
		close;
	}

	// Store entry time for validation
	#DAILY_DUNGEON_ENTRY = gettimetick(2);
	#DAILY_DUNGEON_DIFFICULTY = .@difficulty;

	warp "1@tower", 50, 50;
	close;
}

// Dungeon completion
1@tower,50,100,0	script	Dungeon Exit	WARPPORTAL,2,2,{
OnTouch:
	// Validate completion (no re-entry exploit)
	if (#DAILY_DUNGEON_TIME >= gettimetick(2) / 86400) {
		mes "You've already completed today's dungeon.";
		warp "prontera", 155, 185;
		end;
	}

	.@elapsed = gettimetick(2) - #DAILY_DUNGEON_ENTRY;

	// Anti-cheat: Minimum time check
	if (.@elapsed < 60) {  // Must take at least 60 seconds
		mes "Suspicious completion time detected.";
		warp "prontera", 155, 185;
		end;
	}

	// Calculate rewards based on difficulty and time
	.@difficulty = #DAILY_DUNGEON_DIFFICULTY;
	.@base_reward = 10000 * .@difficulty;

	// Time bonus (faster = better)
	.@time_bonus = 1.0;
	if (.@elapsed < 300) .@time_bonus = 1.5;  // Under 5 min
	else if (.@elapsed < 600) .@time_bonus = 1.3;  // Under 10 min
	else if (.@elapsed < 900) .@time_bonus = 1.1;  // Under 15 min

	.@final_reward = .@base_reward * .@time_bonus;

	// Award rewards
	Zeny += .@final_reward;
	#DAILY_POINTS += .@difficulty * 10;

	// Update cooldown and streak
	#DAILY_DUNGEON_TIME = gettimetick(2) / 86400;

	// Check if maintaining streak (must complete within 24 hours of last)
	if (#DAILY_DUNGEON_TIME == (#DAILY_DUNGEON_LAST + 1)) {
		#DAILY_DUNGEON_STREAK++;
	} else if (#DAILY_DUNGEON_TIME > (#DAILY_DUNGEON_LAST + 1)) {
		#DAILY_DUNGEON_STREAK = 1;  // Streak broken
	}

	#DAILY_DUNGEON_LAST = #DAILY_DUNGEON_TIME;

	mes "[Dungeon Master]";
	mes "Congratulations!";
	mes "Completion Time: ^0000FF" + (.@elapsed / 60) + " minutes, " + (.@elapsed % 60) + " seconds^000000";
	mes "Reward: ^FF0000" + .@final_reward + " Zeny^000000";
	mes "Current Streak: ^00FF00" + #DAILY_DUNGEON_STREAK + " days^000000";
	next;

	warp "prontera", 155, 185;
	end;
}
```

### Hourly Cooldown System

```cpp
// Hourly event participation
prontera,165,180,4	script	Hourly Event	4_M_ALCHE_D,{

	.@last_participation = #HOURLY_EVENT_TIME;
	.@current_hour = gettimetick(2) / 3600;  // Hours since epoch

	if (.@last_participation >= .@current_hour) {
		.@next_hour = (.@current_hour + 1) * 3600;
		.@mins_left = (.@next_hour - gettimetick(2)) / 60;

		mes "[Event Master]";
		mes "You've already participated this hour.";
		mes "Next event in: ^FF0000" + .@mins_left + " minutes^000000";
		close;
	}

	mes "[Event Master]";
	mes "Ready for the hourly challenge?";
	next;

	if (select("Yes:No") == 2) {
		close;
	}

	// Mark as participated
	#HOURLY_EVENT_TIME = .@current_hour;

	// Event logic here
	switch (rand(1, 3)) {
		case 1:
			callfunc "F_PvPEvent";
			break;
		case 2:
			callfunc "F_BossRush";
			break;
		case 3:
			callfunc "F_TreasureHunt";
			break;
	}

	end;
}
```

### Global Server Cooldown

```cpp
// World boss with global cooldown
-	script	WorldBoss_Spawner	-1,{
OnInit:
	.next_spawn = gettimetick(2) + 3600;  // Next spawn in 1 hour
	end;

OnMinute00:  // Check every hour
	if (gettimetick(2) < .next_spawn)
		end;

	// Spawn world boss
	monster "prontera", 150, 150, "World Boss", 1234, 1, strnpcinfo(3) + "::OnBossDead";

	announce "World Boss has spawned in Prontera!", bc_all;

	end;

OnBossDead:
	announce "World Boss has been defeated!", bc_all;

	// Set next spawn time (4 hours later)
	.next_spawn = gettimetick(2) + (3600 * 4);

	// Announce next spawn
	.@hours = (.next_spawn - gettimetick(2)) / 3600;
	announce "Next World Boss spawn in " + .@hours + " hours.", bc_all;

	end;
}
```

### Cooldown Best Practices

```cpp
// ✅ MEMORY-EFFICIENT COOLDOWN STORAGE

// GOOD: Store time of last use
#SKILL_LAST_USE = gettimetick(2);  // 4 bytes

// BAD: Store multiple time-based flags
#SKILL_HOUR1 = 1;
#SKILL_HOUR2 = 0;
// ... wastes memory

// Cooldown check function (reusable)
function	script	F_CheckCooldown	{
	.@last_use = getarg(0);       // Last use timestamp
	.@cooldown = getarg(1);       // Cooldown in seconds
	.@error_msg$ = getarg(2, ""); // Optional error message

	.@remaining = .@cooldown - (gettimetick(2) - .@last_use);

	if (.@remaining > 0) {
		if (.@error_msg$ != "") {
			.@hours = .@remaining / 3600;
			.@mins = (.@remaining % 3600) / 60;
			.@secs = .@remaining % 60;

			mes .@error_msg$;
			mes "Time remaining: ^FF0000" + .@hours + "h " + .@mins + "m " + .@secs + "s^000000";
		}
		return 0;  // Still on cooldown
	}

	return 1;  // Cooldown expired
}

// Usage example:
if (!callfunc("F_CheckCooldown", #DAILY_REWARD_TIME, 86400, "Daily reward already claimed!")) {
	close;
}

// Claim reward
#DAILY_REWARD_TIME = gettimetick(2);
```

---

<!-- RAG_CHUNK: 06_3 -->
## 3. Point Accumulation Systems {#point-systems}

### Use Cases
- Event points for rewards
- Loyalty systems
- Ranking/leaderboard systems
- Currency alternatives

### Basic Point System

```cpp
// npc/custom/point_system.txt
//===================================================================
// Event Point Accumulation System
//===================================================================

prontera,170,180,4	script	Point Exchange	4_F_KAFRA1,{

	mes "[Point Exchange]";
	mes "Current Points: ^0000FF" + #EVENT_POINTS + "^000000";
	mes "Lifetime Points: ^00FF00" + #EVENT_POINTS_TOTAL + "^000000";
	next;

	switch (select("Exchange Points:View Rewards:Check Ranking:Cancel")) {
		case 1:  // Exchange
			callfunc "F_PointExchange";
			break;
		case 2:  // View rewards
			callfunc "F_ViewRewards";
			break;
		case 3:  // Ranking
			callfunc "F_PointRanking";
			break;
		case 4:
			close;
	}

	end;
}

// Point exchange function
function	script	F_PointExchange	{
	mes "[Point Exchange]";
	mes "What would you like?";
	next;

	setarray .@items[0], 501, 502, 503, 607, 608;  // Item IDs
	setarray .@costs[0], 10, 20, 30, 1000, 5000;   // Point costs
	setarray .@names$[0], "Red Potion", "Orange Potion", "Yellow Potion", "Yggdrasil Berry", "Yggdrasil Seed";

	.@size = getarraysize(.@items);
	.@menu$ = "";

	for (.@i = 0; .@i < .@size; .@i++) {
		.@menu$ += .@names$[.@i] + " (" + .@costs[.@i] + " pts):";
	}
	.@menu$ += "Cancel";

	.@choice = select(.@menu$) - 1;

	if (.@choice >= .@size) {
		close;
	}

	// Validate points
	if (#EVENT_POINTS < .@costs[.@choice]) {
		mes "[Point Exchange]";
		mes "Insufficient points!";
		mes "Need: ^FF0000" + .@costs[.@choice] + "^000000";
		mes "Have: ^0000FF" + #EVENT_POINTS + "^000000";
		close;
	}

	// Check inventory space
	if (checkweight(.@items[.@choice], 1) == 0) {
		mes "[Point Exchange]";
		mes "Your inventory is too heavy!";
		close;
	}

	// Perform exchange
	#EVENT_POINTS -= .@costs[.@choice];
	getitem .@items[.@choice], 1;

	mes "[Point Exchange]";
	mes "Exchange complete!";
	mes "Remaining points: ^0000FF" + #EVENT_POINTS + "^000000";

	// Log exchange
	query_sql "INSERT INTO `point_log` (`account_id`, `char_id`, `item_id`, `points_spent`, `timestamp`) VALUES (" + getcharid(3) + ", " + getcharid(0) + ", " + .@items[.@choice] + ", " + .@costs[.@choice] + ", NOW())";

	close;
}

// Point earning through mob kills
-	script	PointEarnSystem	-1,{
OnNPCKillEvent:
	// Define point values for different monsters
	setarray .mob_ids[0], 1002, 1113, 1157, 1159;  // Poring, Drops, Pharaoh, Phreeoni
	setarray .mob_points[0], 1, 2, 50, 100;

	.@size = getarraysize(.mob_ids);

	set freeloop, 1;
	for (.@i = 0; .@i < .@size; .@i++) {
		if (killedrid == .mob_ids[.@i]) {
			.@points = .mob_points[.@i];

			// Bonus points for events
			if ($EVENT_ACTIVE) {
				.@points *= 2;
				dispbottom "Event Bonus! Points doubled!";
			}

			#EVENT_POINTS += .@points;
			#EVENT_POINTS_TOTAL += .@points;

			dispbottom "+" + .@points + " Event Points! Total: " + #EVENT_POINTS;

			// Update ranking
			callfunc "F_UpdateRanking", getcharid(0), #EVENT_POINTS_TOTAL;
			break;
		}
	}
	set freeloop, 0;

	end;
}
```

### Leaderboard System

```cpp
// Point ranking system with SQL
function	script	F_PointRanking	{
	mes "[Rankings]";
	mes "Top 10 Point Earners:";
	mes "^00FF00━━━━━━━━━━━━━━━━━━━━^000000";

	// Query top 10 from database
	.@query$ = "SELECT `name`, `points` FROM `char` WHERE `points` > 0 ORDER BY `points` DESC LIMIT 10";

	.@nb = query_sql(.@query$, .@names$, .@points);

	if (.@nb == 0) {
		mes "No rankings available yet.";
		close;
	}

	for (.@i = 0; .@i < .@nb; .@i++) {
		.@rank = .@i + 1;

		// Color coding for top 3
		switch (.@rank) {
			case 1: .@color$ = "^FFD700"; break;  // Gold
			case 2: .@color$ = "^C0C0C0"; break;  // Silver
			case 3: .@color$ = "^CD7F32"; break;  // Bronze
			default: .@color$ = "^000000"; break;
		}

		mes .@color$ + .@rank + ". " + .@names$[.@i] + " - " + .@points[.@i] + " pts^000000";
	}

	// Show player's rank if not in top 10
	.@my_rank = callfunc("F_GetPlayerRank", getcharid(0));
	if (.@my_rank > 10) {
		mes "^00FF00━━━━━━━━━━━━━━━━━━━━^000000";
		mes "Your rank: ^FF0000#" + .@my_rank + "^000000 (" + #EVENT_POINTS_TOTAL + " pts)";
	}

	close;
}

// Get player's current rank
function	script	F_GetPlayerRank	{
	.@char_id = getarg(0);

	.@query$ = "SELECT COUNT(*) + 1 FROM `char` WHERE `points` > (SELECT `points` FROM `char` WHERE `char_id` = " + .@char_id + ")";

	query_sql .@query$, .@rank;

	return .@rank;
}

// Update ranking (called on point gain)
function	script	F_UpdateRanking	{
	.@char_id = getarg(0);
	.@points = getarg(1);

	// Update database
	query_sql "UPDATE `char` SET `points` = " + .@points + " WHERE `char_id` = " + .@char_id;

	return 1;
}
```

### Point System with Decay

```cpp
// Points that decay over time (encourages regular play)
-	script	PointDecaySystem	-1,{
OnInit:
	bindatcmd "checkdecay", strnpcinfo(3) + "::OnCheckDecay";
	end;

OnHour00:  // Daily at midnight
	// Decay all player points by 5%
	query_sql "UPDATE `char` SET `points` = FLOOR(`points` * 0.95) WHERE `points` > 0";

	announce "Daily point decay applied! Points reduced by 5%.", bc_all;
	end;

OnCheckDecay:
	.@last_login = #LAST_LOGIN_TIME;
	.@days_away = (gettimetick(2) - .@last_login) / 86400;

	if (.@days_away > 0) {
		.@decay_rate = 0.95;  // 5% per day
		.@old_points = #EVENT_POINTS;

		// Calculate compounding decay
		for (.@i = 0; .@i < .@days_away; .@i++) {
			#EVENT_POINTS = #EVENT_POINTS * .@decay_rate;
		}

		.@lost_points = .@old_points - #EVENT_POINTS;

		dispbottom "You lost " + .@lost_points + " points due to inactivity (" + .@days_away + " days).";
		dispbottom "Current points: " + #EVENT_POINTS;
	}

	#LAST_LOGIN_TIME = gettimetick(2);
	end;
}
```

---

<!-- RAG_CHUNK: 06_4 -->
## 4. Instanced Event Pattern {#instanced-events}

### Party Dungeon Instance

```cpp
// npc/custom/party_instance.txt
//===================================================================
// Party Instance Dungeon
//===================================================================

prontera,175,180,4	script	Instance Dungeon	4_M_KNIGHT_GOLD,{

	.@party_id = getcharid(1);

	if (.@party_id == 0) {
		mes "[Instance Master]";
		mes "You must be in a party to enter.";
		close;
	}

	// Check if party leader
	if (getpartyleader(.@party_id, 2) != getcharid(0)) {
		mes "[Instance Master]";
		mes "Only the party leader can create an instance.";
		close;
	}

	// Check party size
	getpartymember .@party_id, 1;
	.@party_count = $@partymembercount;

	if (.@party_count < 3) {
		mes "[Instance Master]";
		mes "You need at least 3 party members.";
		close;
	}

	mes "[Instance Master]";
	mes "Party size: ^0000FF" + .@party_count + "^000000/12";
	mes " ";
	mes "Would you like to create a dungeon instance?";
	next;

	if (select("Create Instance:Cancel") == 2) {
		close;
	}

	// Check for existing instance
	.@instance_id = instance_id(IM_PARTY);

	if (.@instance_id > 0) {
		mes "[Instance Master]";
		mes "Your party already has an instance.";
		mes "Would you like to enter it?";
		next;

		if (select("Enter:Destroy and Create New") == 1) {
			instance_enter "1@party";
			end;
		} else {
			instance_destroy .@instance_id;
		}
	}

	// Create new instance
	.@instance_name$ = "Party Dungeon";
	.@instance_id = instance_create(.@instance_name$, .@party_id, IM_PARTY);

	if (.@instance_id < 0) {
		mes "[Instance Master]";
		mes "Failed to create instance.";
		close;
	}

	// Attach maps to instance
	if (instance_attach(.@instance_id) != 0) {
		mes "[Instance Master]";
		mes "Failed to attach instance.";
		instance_destroy .@instance_id;
		close;
	}

	instance_attach(.@instance_id);
	instance_map_add("1@party", "1@party");
	instance_init(.@instance_id);

	mes "[Instance Master]";
	mes "Instance created successfully!";
	mes "You have ^FF00001 hour^000000 to complete it.";
	next;

	if (select("Enter Now:Enter Later") == 1) {
		instance_enter "1@party";
	}

	close;
}

// Instance map initialization
1@party,0,0,0	script	#PartyInstance_Init	-1,{
OnInstanceInit:
	// Set instance timer (1 hour)
	instance_set_timeout 3600, 300, instance_id();

	// Spawn monsters in waves
	donpcevent instance_npcname("#Wave1_Spawn") + "::OnSpawn";
	end;

OnInstanceDestroy:
	announce "Instance will close in 5 minutes!", bc_map;
	end;
}

// Wave 1 monsters
1@party,0,0,0	script	#Wave1_Spawn	-1,{
OnSpawn:
	.@map$ = instance_mapname("1@party");
	.@instance_id = instance_id();

	// Spawn first wave
	monster .@map$, 0, 0, "Dungeon Monster", 1002, 20, instance_npcname("#Wave1_Spawn") + "::OnMobDead";

	.mob_count = 20;
	end;

OnMobDead:
	.mob_count--;

	if (.mob_count <= 0) {
		.@map$ = instance_mapname("1@party");
		announce "Wave 1 complete! Wave 2 incoming!", bc_map;
		sleep 5000;
		donpcevent instance_npcname("#Wave2_Spawn") + "::OnSpawn";
	}
	end;
}

// Boss spawn
1@party,0,0,0	script	#Boss_Spawn	-1,{
OnSpawn:
	.@map$ = instance_mapname("1@party");

	announce "BOSS INCOMING!", bc_map;
	sleep 3000;

	monster .@map$, 100, 100, "Instance Boss", 1159, 1, instance_npcname("#Boss_Spawn") + "::OnBossDead";
	end;

OnBossDead:
	.@map$ = instance_mapname("1@party");

	announce "Boss defeated! Rewards spawning!", bc_map;

	// Spawn treasure chests
	for (.@i = 0; .@i < 5; .@i++) {
		.@x = 90 + rand(20);
		.@y = 90 + rand(20);
		makeitem 607, 1, .@map$, .@x, .@y;  // Yggdrasil Berry
	}

	// Open exit portal
	enablenpc instance_npcname("#Exit_Portal");

	// Set completion flag for party members
	getpartymember getcharid(1), 1;
	set freeloop, 1;
	for (.@i = 0; .@i < $@partymembercount; .@i++) {
		if (isloggedin($@partymemberaid[.@i], $@partymembercid[.@i])) {
			attachrid($@partymemberaid[.@i]);
			#INSTANCE_CLEARS++;
			#INSTANCE_LAST_CLEAR = gettimetick(2);
			detachrid;
		}
	}
	set freeloop, 0;

	end;
}

// Exit portal
1@party,100,120,0	script	#Exit_Portal	WARPPORTAL,2,2,{
OnInstanceInit:
	disablenpc instance_npcname(strnpcinfo(0));
	end;

OnTouch:
	warp "prontera", 155, 185;
	end;
}
```

### Timed Challenge Instance

```cpp
// Speed-run instance with time tracking
prontera,180,180,4	script	Time Trial	4_M_TAEKWON,{

	mes "[Time Trial Master]";
	mes "Think you're fast?";
	mes "Complete the course in under ^FF00005 minutes^000000!";
	next;

	mes "[Time Trial Master]";
	mes "Best Time: ^0000FF" + (#TRIAL_BEST_TIME / 60) + ":" + (#TRIAL_BEST_TIME % 60) + "^000000";
	next;

	if (select("Enter:Cancel") == 2) {
		close;
	}

	// Create solo instance
	.@instance_name$ = "Time Trial - " + strcharinfo(0);
	.@instance_id = instance_create(.@instance_name$, getcharid(0), IM_CHAR);

	if (.@instance_id < 0) {
		mes "Failed to create trial.";
		close;
	}

	instance_attach(.@instance_id);
	instance_map_add("1@trial", "1@trial");
	instance_init(.@instance_id);

	// Set start time
	#TRIAL_START_TIME = gettimetick(2);

	instance_enter "1@trial";
	end;
}

// Trial completion
1@trial,100,100,0	script	#Trial_Finish	WARPPORTAL,2,2,{
OnTouch:
	.@elapsed = gettimetick(2) - #TRIAL_START_TIME;

	mes "[Time Trial Complete!]";
	mes "Time: ^0000FF" + (.@elapsed / 60) + ":" + (.@elapsed % 60) + "^000000";

	// Check for new record
	if (#TRIAL_BEST_TIME == 0 || .@elapsed < #TRIAL_BEST_TIME) {
		mes " ";
		mes "^00FF00NEW RECORD!^000000";
		#TRIAL_BEST_TIME = .@elapsed;

		// Update global leaderboard
		query_sql "INSERT INTO `time_trial_records` (`char_id`, `name`, `time`, `date`) VALUES (" + getcharid(0) + ", '" + escape_sql(strcharinfo(0)) + "', " + .@elapsed + ", NOW()) ON DUPLICATE KEY UPDATE `time` = " + .@elapsed + ", `date` = NOW()";
	}

	next;
	warp "prontera", 155, 185;
	end;
}
```

---

<!-- RAG_CHUNK: 06_5 -->
## 5. Dynamic Shop Systems {#dynamic-shops}

### Price Adjustment Based on Stock

```cpp
// npc/custom/dynamic_shop.txt
//===================================================================
// Dynamic Shop with Stock and Price Fluctuation
//===================================================================

prontera,185,180,4	script	Dynamic Trader	4_M_ALCHE_A,{

	mes "[Dynamic Trader]";
	mes "Prices change based on stock!";
	mes "Buy low, sell high!";
	next;

	callshop "DynShop", 0;
	npcshopattach "DynShop";
	end;

OnBuyItem:
	// Get item being purchased
	.@item_id = @bought_nameid[0];
	.@amount = @bought_quantity[0];

	// Find item in stock array
	.@index = -1;
	set freeloop, 1;
	for (.@i = 0; .@i < getarraysize(.shop_items); .@i++) {
		if (.shop_items[.@i] == .@item_id) {
			.@index = .@i;
			break;
		}
	}
	set freeloop, 0;

	if (.@index == -1) {
		mes "Item not found in shop.";
		end;
	}

	// Check stock
	if (.shop_stock[.@index] < .@amount) {
		mes "Insufficient stock!";
		mes "Available: " + .shop_stock[.@index];
		end;
	}

	// Calculate current price (base price + stock modifier)
	.@base_price = .shop_base_price[.@index];
	.@stock = .shop_stock[.@index];

	// Price increases as stock decreases
	// Formula: base_price * (1 + (max_stock - current_stock) / max_stock * 0.5)
	.@price_modifier = (1000 - .@stock) / 1000.0 * 0.5;
	.@current_price = .@base_price * (1 + .@price_modifier);
	.@total_cost = .@current_price * .@amount;

	// Check player zeny
	if (Zeny < .@total_cost) {
		mes "Insufficient funds!";
		mes "Cost: ^FF0000" + .@total_cost + "z^000000";
		end;
	}

	// Perform transaction
	Zeny -= .@total_cost;
	getitem .@item_id, .@amount;

	// Update stock
	.shop_stock[.@index] -= .@amount;

	// Log transaction
	dispbottom "Purchased " + getitemname(.@item_id) + " x" + .@amount + " for " + .@total_cost + "z";

	// Recalculate shop prices
	donpcevent strnpcinfo(3) + "::OnUpdatePrices";

	end;

OnSellItem:
	// Get item being sold
	.@item_id = @sold_nameid[0];
	.@amount = @sold_quantity[0];

	// Find item in stock array
	.@index = -1;
	set freeloop, 1;
	for (.@i = 0; .@i < getarraysize(.shop_items); .@i++) {
		if (.shop_items[.@i] == .@item_id) {
			.@index = .@i;
			break;
		}
	}
	set freeloop, 0;

	if (.@index == -1) {
		mes "We don't buy that item.";
		end;
	}

	// Calculate sell price (lower than buy price)
	.@base_price = .shop_base_price[.@index];
	.@sell_price = .@base_price * 0.7;  // 70% of base price
	.@total_value = .@sell_price * .@amount;

	// Perform transaction
	delitem .@item_id, .@amount;
	Zeny += .@total_value;

	// Update stock (buying from player increases stock)
	.shop_stock[.@index] += .@amount;

	// Cap stock at max
	if (.shop_stock[.@index] > 1000) {
		.shop_stock[.@index] = 1000;
	}

	dispbottom "Sold " + getitemname(.@item_id) + " x" + .@amount + " for " + .@total_value + "z";

	// Recalculate shop prices
	donpcevent strnpcinfo(3) + "::OnUpdatePrices";

	end;

OnUpdatePrices:
	// Update shop display with current prices
	deleteshop "DynShop";

	set freeloop, 1;
	for (.@i = 0; .@i < getarraysize(.shop_items); .@i++) {
		.@item_id = .shop_items[.@i];
		.@base_price = .shop_base_price[.@i];
		.@stock = .shop_stock[.@i];

		// Calculate current price
		.@price_modifier = (1000 - .@stock) / 1000.0 * 0.5;
		.@current_price = .@base_price * (1 + .@price_modifier);

		npcshopadditem "DynShop", .@item_id, .@current_price;
	}
	set freeloop, 0;

	end;

OnInit:
	// Initialize shop
	npcshopdelitem "DynShop", 501;  // Clear default items

	// Define shop items
	setarray .shop_items[0], 501, 502, 503, 504, 505;  // Item IDs
	setarray .shop_base_price[0], 50, 200, 500, 1000, 2000;  // Base prices
	setarray .shop_stock[0], 1000, 1000, 1000, 1000, 1000;  // Initial stock

	// Update prices
	donpcevent strnpcinfo(3) + "::OnUpdatePrices";

	// Stock replenishment timer (every hour)
	OnClock0000:
	OnClock0100:
	OnClock0200:
	OnClock0300:
	OnClock0400:
	OnClock0500:
	OnClock0600:
	OnClock0700:
	OnClock0800:
	OnClock0900:
	OnClock1000:
	OnClock1100:
	OnClock1200:
	OnClock1300:
	OnClock1400:
	OnClock1500:
	OnClock1600:
	OnClock1700:
	OnClock1800:
	OnClock1900:
	OnClock2000:
	OnClock2100:
	OnClock2200:
	OnClock2300:
		// Replenish stock slowly
		set freeloop, 1;
		for (.@i = 0; .@i < getarraysize(.shop_stock); .@i++) {
			if (.shop_stock[.@i] < 1000) {
				.shop_stock[.@i] += 100;  // Replenish 100 per hour
				if (.shop_stock[.@i] > 1000) {
					.shop_stock[.@i] = 1000;
				}
			}
		}
		set freeloop, 0;

		donpcevent strnpcinfo(3) + "::OnUpdatePrices";
		end;
}

-	shop	DynShop	-1,501:50
```

### Player-Driven Market

```cpp
// Player vending tracker and price comparison
-	script	MarketTracker	-1,{
OnInit:
	bindatcmd "finditem", strnpcinfo(3) + "::OnFindItem";
	end;

OnFindItem:
	// Search for item in all active vending shops
	.@item_name$ = implode(.@atcmd_parameters$, " ");

	if (.@item_name$ == "") {
		dispbottom "Usage: @finditem <item name>";
		end;
	}

	// Search item database
	.@item_id = getitemid(.@item_name$);

	if (.@item_id == 0) {
		dispbottom "Item not found: " + .@item_name$;
		end;
	}

	// Query all vending shops
	.@count = 0;
	.@query$ = "SELECT `char`.`name`, `vending`.`price`, `vending`.`amount`, `char`.`last_map`, `char`.`last_x`, `char`.`last_y` FROM `vending` INNER JOIN `char` ON `vending`.`char_id` = `char`.`char_id` WHERE `vending`.`nameid` = " + .@item_id + " ORDER BY `vending`.`price` ASC LIMIT 10";

	.@nb = query_sql(.@query$, .@names$, .@prices, .@amounts, .@maps$, .@x, .@y);

	if (.@nb == 0) {
		dispbottom "No vending shops selling " + getitemname(.@item_id) + ".";
		end;
	}

	dispbottom "=== Vending Shops selling " + getitemname(.@item_id) + " ===";

	for (.@i = 0; .@i < .@nb; .@i++) {
		dispbottom (.@i + 1) + ". " + .@names$[.@i] + " - " + .@prices[.@i] + "z x" + .@amounts[.@i] + " @ " + .@maps$[.@i] + " (" + .@x[.@i] + "," + .@y[.@i] + ")";
	}

	end;
}
```

---

<!-- RAG_CHUNK: 06_6 -->
## 6. Mini-Game Implementations {#mini-games}

### Dice Game

```cpp
// npc/custom/minigame_dice.txt
//===================================================================
// Dice Gambling Mini-Game
//===================================================================

prontera,190,180,4	script	Dice Gambler	4_M_MASKMAN,{

	mes "[Dice Gambler]";
	mes "Roll the dice!";
	mes "Guess high (8-12) or low (3-7)?";
	mes " ";
	mes "Bet: ^FF00001,000z^000000 to ^FF000010,000z^000000";
	next;

	// Cooldown check
	if (gettimetick(2) - #DICE_LAST_PLAY < 5) {
		mes "[Dice Gambler]";
		mes "Slow down! Wait a few seconds.";
		close;
	}

	// Get bet amount
	input .@bet, 1000, 10000;

	if (Zeny < .@bet) {
		mes "[Dice Gambler]";
		mes "You don't have enough zeny!";
		close;
	}

	mes "[Dice Gambler]";
	mes "Bet: ^0000FF" + .@bet + "z^000000";
	mes " ";
	mes "Guess high or low?";
	next;

	.@guess = select("High (8-12):Low (3-7)");

	// Take bet
	Zeny -= .@bet;

	// Roll dice
	.@die1 = rand(1, 6);
	.@die2 = rand(1, 6);
	.@total = .@die1 + .@die2;

	mes "[Dice Gambler]";
	mes "Rolling...";
	next;

	mes "[Dice Gambler]";
	mes "Dice 1: ^FF0000" + .@die1 + "^000000";
	mes "Dice 2: ^FF0000" + .@die2 + "^000000";
	mes "Total: ^00FF00" + .@total + "^000000";
	next;

	// Check result
	.@win = 0;

	if (.@guess == 1 && .@total >= 8 && .@total <= 12) {
		.@win = 1;
	} else if (.@guess == 2 && .@total >= 3 && .@total <= 7) {
		.@win = 1;
	}

	// Special case: 2 or 12 (snake eyes / box cars)
	.@multiplier = 2;  // Default 2x payout

	if (.@total == 2 || .@total == 12) {
		.@multiplier = 5;  // 5x payout for extremes
	} else if (.@total == 7) {
		.@multiplier = 0;  // 7 is auto-loss
		.@win = 0;
	}

	mes "[Dice Gambler]";

	if (.@win) {
		.@winnings = .@bet * .@multiplier;
		Zeny += .@winnings;

		mes "^00FF00YOU WIN!^000000";
		mes "Payout: ^00FF00" + .@winnings + "z^000000";
		mes "Multiplier: x" + .@multiplier;

		if (.@multiplier == 5) {
			announce strcharinfo(0) + " hit a rare roll (" + .@total + ") and won " + .@winnings + "z!", bc_all;
		}

		// Track statistics
		#DICE_WINS++;
		#DICE_TOTAL_WON += (.@winnings - .@bet);
	} else {
		mes "^FF0000YOU LOSE!^000000";
		mes "Better luck next time!";

		if (.@total == 7) {
			mes "^FF0000Seven is an automatic loss!^000000";
		}

		// Track statistics
		#DICE_LOSSES++;
		#DICE_TOTAL_LOST += .@bet;
	}

	next;

	mes "[Dice Gambler]";
	mes "Your Statistics:";
	mes "Wins: ^00FF00" + #DICE_WINS + "^000000";
	mes "Losses: ^FF0000" + #DICE_LOSSES + "^000000";
	.@net = #DICE_TOTAL_WON - #DICE_TOTAL_LOST;
	mes "Net: " + (.@net >= 0 ? "^00FF00+" : "^FF0000") + .@net + "z^000000";

	#DICE_LAST_PLAY = gettimetick(2);
	close;
}
```

### Trivia Quiz System

```cpp
// npc/custom/minigame_trivia.txt
//===================================================================
// Trivia Quiz Mini-Game
//===================================================================

prontera,195,180,4	script	Trivia Master	4_M_SAGE_C,{

	mes "[Trivia Master]";
	mes "Test your knowledge!";
	mes "Answer 5 questions correctly.";
	next;

	// Cooldown check (once per hour)
	if (!callfunc("F_CheckCooldown", #TRIVIA_LAST_PLAY, 3600, "You can only play once per hour!")) {
		close;
	}

	if (select("Start Quiz:Cancel") == 2) {
		close;
	}

	// Initialize quiz
	.@correct = 0;
	.@total = 5;

	// Question array (stored in NPC)
	setarray .questions$[0],
		"What is the capital of Rune-Midgard?",
		"Which monster drops the Poring Card?",
		"What level can you change to Second Class?",
		"Which stat increases SP?",
		"What is the maximum base level in renewal?";

	setarray .options$[0],
		"Prontera:Geffen:Morroc:Payon",
		"Poring:Drops:Poporing:Marin",
		"30:35:40:45",
		"INT:VIT:DEX:AGI",
		"99:150:175:200";

	setarray .correct_answers[0], 1, 1, 3, 1, 3;  // Correct option number

	// Shuffle questions
	.@size = getarraysize(.questions$);
	copyarray .@q_indices[0], .questions$[0], .@size;

	// Ask questions
	set freeloop, 1;
	for (.@i = 0; .@i < .@total; .@i++) {
		// Random question
		.@q_idx = rand(.@size);

		mes "[Trivia Master]";
		mes "Question " + (.@i + 1) + "/" + .@total;
		mes "^0000FF" + .questions$[.@q_idx] + "^000000";
		next;

		// Parse options
		explode(.@opts$, .options$[.@q_idx], ":");
		.@menu$ = implode(.@opts$, ":");

		.@answer = select(.@menu$);

		if (.@answer == .correct_answers[.@q_idx]) {
			mes "[Trivia Master]";
			mes "^00FF00Correct!^000000";
			.@correct++;
		} else {
			mes "[Trivia Master]";
			mes "^FF0000Wrong!^000000";
			mes "Correct answer: ^00FF00" + .@opts$[.correct_answers[.@q_idx] - 1] + "^000000";
		}
		next;
	}
	set freeloop, 0;

	// Calculate rewards
	mes "[Trivia Master]";
	mes "Quiz Complete!";
	mes "Score: ^0000FF" + .@correct + "^000000/" + .@total;
	next;

	// Reward based on score
	if (.@correct == 5) {
		mes "[Trivia Master]";
		mes "^00FF00PERFECT SCORE!^000000";
		mes "You've earned a special reward!";

		getitem 607, 1;  // Yggdrasil Berry
		#TRIVIA_POINTS += 10;

		announce strcharinfo(0) + " achieved a perfect score in Trivia!", bc_all;
	} else if (.@correct >= 3) {
		mes "[Trivia Master]";
		mes "Good job!";

		#TRIVIA_POINTS += .@correct;
		Zeny += .@correct * 1000;
	} else {
		mes "[Trivia Master]";
		mes "Better luck next time!";
		#TRIVIA_POINTS += 1;  // Participation point
	}

	mes " ";
	mes "Total Trivia Points: ^00FF00" + #TRIVIA_POINTS + "^000000";

	#TRIVIA_LAST_PLAY = gettimetick(2);
	close;
}
```

### Number Guessing Game

```cpp
// Simple number guessing with attempts limit
prontera,200,180,4	script	Number Guesser	4_F_YUNYANG,{

	mes "[Number Guesser]";
	mes "I'm thinking of a number between 1 and 100.";
	mes "You have 7 attempts!";
	next;

	// Generate random number
	.@secret = rand(1, 100);
	.@attempts = 7;

	while (.@attempts > 0) {
		mes "[Number Guesser]";
		mes "Attempts left: ^FF0000" + .@attempts + "^000000";
		mes "Enter your guess (1-100):";
		input .@guess, 1, 100;

		if (.@guess == .@secret) {
			mes "[Number Guesser]";
			mes "^00FF00CORRECT!^000000";
			mes "You guessed it in " + (8 - .@attempts) + " attempts!";

			.@reward = ((.@attempts + 1) * 1000);
			Zeny += .@reward;

			mes "Reward: ^00FF00" + .@reward + "z^000000";
			close;
		}

		next;
		mes "[Number Guesser]";

		if (.@guess < .@secret) {
			mes "^0000FFToo low!^000000";
		} else {
			mes "^0000FFToo high!^000000";
		}

		.@attempts--;
		next;
	}

	mes "[Number Guesser]";
	mes "Out of attempts!";
	mes "The number was: ^FF0000" + .@secret + "^000000";
	close;
}
```

---

<!-- RAG_CHUNK: 06_7 -->
## 7. Auction System Pattern {#auction-system}

### Item Auction System

```cpp
// npc/custom/auction_system.txt
//===================================================================
// Player-to-Player Auction House
//===================================================================

prontera,145,170,4	script	Auction House	4_F_KAFRA2,{

	mes "[Auction House]";
	mes "Welcome to the Auction House!";
	next;

	switch (select("Browse Auctions:List Item:My Auctions:My Bids:Cancel")) {
		case 1:
			callfunc "F_BrowseAuctions";
			break;
		case 2:
			callfunc "F_ListAuction";
			break;
		case 3:
			callfunc "F_MyAuctions";
			break;
		case 4:
			callfunc "F_MyBids";
			break;
		case 5:
			close;
	}

	end;
}

// Browse active auctions
function	script	F_BrowseAuctions	{
	mes "[Auction House]";
	mes "Active Auctions:";
	next;

	// Query active auctions
	.@query$ = "SELECT `auction_id`, `item_id`, `item_name`, `seller_name`, `current_bid`, `end_time` FROM `auction` WHERE `end_time` > NOW() AND `status` = 'active' ORDER BY `end_time` ASC LIMIT 20";

	.@nb = query_sql(.@query$, .@ids, .@item_ids, .@item_names$, .@sellers$, .@bids, .@end_times$);

	if (.@nb == 0) {
		mes "No active auctions.";
		close;
	}

	// Build menu
	.@menu$ = "";
	for (.@i = 0; .@i < .@nb; .@i++) {
		.@menu$ += .@item_names$[.@i] + " - " + .@bids[.@i] + "z:";
	}
	.@menu$ += "Cancel";

	.@choice = select(.@menu$) - 1;

	if (.@choice >= .@nb) {
		close;
	}

	// Show auction details
	.@auction_id = .@ids[.@choice];
	callfunc "F_AuctionDetails", .@auction_id;

	return;
}

// Auction details and bidding
function	script	F_AuctionDetails	{
	.@auction_id = getarg(0);

	// Query auction details
	.@query$ = "SELECT `item_id`, `item_name`, `seller_name`, `starting_bid`, `current_bid`, `buyout_price`, `end_time` FROM `auction` WHERE `auction_id` = " + .@auction_id;

	if (query_sql(.@query$, .@item_id, .@item_name$, .@seller$, .@start_bid, .@current_bid, .@buyout, .@end_time$) == 0) {
		mes "Auction not found.";
		close;
	}

	mes "[Auction Details]";
	mes "Item: ^0000FF" + .@item_name$ + "^000000";
	mes "Seller: " + .@seller$;
	mes "Starting Bid: " + .@start_bid + "z";
	mes "Current Bid: ^00FF00" + .@current_bid + "z^000000";
	mes "Buyout Price: ^FF0000" + .@buyout + "z^000000";
	mes "Ends: " + .@end_time$;
	next;

	switch (select("Place Bid:Buyout:Cancel")) {
		case 1:  // Place bid
			mes "[Auction House]";
			mes "Current bid: ^00FF00" + .@current_bid + "z^000000";
			mes "Enter your bid (must be higher):";
			input .@bid;

			// Validate bid
			if (.@bid <= .@current_bid) {
				mes "[Auction House]";
				mes "Bid must be higher than current bid!";
				close;
			}

			if (Zeny < .@bid) {
				mes "[Auction House]";
				mes "Insufficient funds!";
				close;
			}

			// Place bid
			.@char_id = getcharid(0);
			.@char_name$ = escape_sql(strcharinfo(0));

			query_sql "UPDATE `auction` SET `current_bid` = " + .@bid + ", `highest_bidder_id` = " + .@char_id + ", `highest_bidder_name` = '" + .@char_name$ + "' WHERE `auction_id` = " + .@auction_id;

			query_sql "INSERT INTO `auction_bids` (`auction_id`, `bidder_id`, `bidder_name`, `bid_amount`, `bid_time`) VALUES (" + .@auction_id + ", " + .@char_id + ", '" + .@char_name$ + "', " + .@bid + ", NOW())";

			// Return previous bidder's money
			if (.@current_bid > 0) {
				query_sql "INSERT INTO `mail` (`send_name`, `dest_id`, `title`, `message`, `zeny`) SELECT 'Auction House', `highest_bidder_id`, 'Auction Outbid', 'You have been outbid. Your bid has been returned.', `current_bid` FROM `auction` WHERE `auction_id` = " + .@auction_id;
			}

			mes "[Auction House]";
			mes "Bid placed successfully!";
			mes "You are now the highest bidder.";
			close;

		case 2:  // Buyout
			if (Zeny < .@buyout) {
				mes "[Auction House]";
				mes "Insufficient funds for buyout!";
				close;
			}

			mes "[Auction House]";
			mes "Confirm buyout for ^FF0000" + .@buyout + "z^000000?";
			next;

			if (select("Confirm:Cancel") == 2) {
				close;
			}

			// Process buyout
			Zeny -= .@buyout;

			// Give item to buyer
			getitem .@item_id, 1;

			// Send money to seller
			query_sql "INSERT INTO `mail` (`send_name`, `dest_name`, `title`, `message`, `zeny`) VALUES ('Auction House', '" + escape_sql(.@seller$) + "', 'Item Sold', 'Your item was bought out!', " + .@buyout + ")";

			// Mark auction as completed
			query_sql "UPDATE `auction` SET `status` = 'completed', `end_time` = NOW() WHERE `auction_id` = " + .@auction_id;

			// Return money to previous bidder
			if (.@current_bid > 0) {
				query_sql "INSERT INTO `mail` (`send_name`, `dest_id`, `title`, `message`, `zeny`) SELECT 'Auction House', `highest_bidder_id`, 'Auction Ended', 'Item was bought out. Your bid has been returned.', `current_bid` FROM `auction` WHERE `auction_id` = " + .@auction_id;
			}

			mes "[Auction House]";
			mes "Buyout successful!";
			mes "Item delivered to inventory.";
			close;

		case 3:
			close;
	}

	return;
}

// List item for auction
function	script	F_ListAuction	{
	mes "[Auction House]";
	mes "Select an item from your inventory:";
	next;

	// Open item selection
	if (select("Equipment:Consumable:Etc:Cancel") == 4) {
		close;
	}

	// TODO: Item selection interface
	// For simplicity, using input for item ID

	mes "[Auction House]";
	mes "Enter Item ID to auction:";
	input .@item_id;

	// Validate item ownership
	if (countitem(.@item_id) < 1) {
		mes "You don't have that item!";
		close;
	}

	mes "[Auction House]";
	mes "Item: ^0000FF" + getitemname(.@item_id) + "^000000";
	mes " ";
	mes "Enter starting bid:";
	input .@starting_bid, 1000;

	mes "[Auction House]";
	mes "Enter buyout price (0 for none):";
	input .@buyout_price;

	mes "[Auction House]";
	mes "Auction duration:";
	.@duration = select("6 hours:12 hours:24 hours:48 hours") * 6;  // Hours

	mes "[Auction House]";
	mes "Listing fee: ^FF00001,000z^000000";
	mes "Confirm listing?";
	next;

	if (select("Confirm:Cancel") == 2) {
		close;
	}

	// Validate
	if (Zeny < 1000) {
		mes "Insufficient funds for listing fee!";
		close;
	}

	// Take item and fee
	delitem .@item_id, 1;
	Zeny -= 1000;

	// Insert auction
	.@char_id = getcharid(0);
	.@char_name$ = escape_sql(strcharinfo(0));
	.@item_name$ = escape_sql(getitemname(.@item_id));

	query_sql "INSERT INTO `auction` (`seller_id`, `seller_name`, `item_id`, `item_name`, `starting_bid`, `current_bid`, `buyout_price`, `start_time`, `end_time`, `status`) VALUES (" + .@char_id + ", '" + .@char_name$ + "', " + .@item_id + ", '" + .@item_name$ + "', " + .@starting_bid + ", " + .@starting_bid + ", " + .@buyout_price + ", NOW(), DATE_ADD(NOW(), INTERVAL " + .@duration + " HOUR), 'active')";

	mes "[Auction House]";
	mes "Item listed successfully!";
	close;

	return;
}

// Auction completion handler (timer-based)
-	script	AuctionHandler	-1,{
OnInit:
	// Check for expired auctions every 5 minutes
	OnTimer300000:
		initnpctimer;

		// Query expired auctions
		.@query$ = "SELECT `auction_id`, `item_id`, `seller_name`, `highest_bidder_id`, `highest_bidder_name`, `current_bid` FROM `auction` WHERE `end_time` < NOW() AND `status` = 'active'";

		.@nb = query_sql(.@query$, .@ids, .@item_ids, .@sellers$, .@bidder_ids, .@bidder_names$, .@bids);

		if (.@nb == 0) end;

		set freeloop, 1;
		for (.@i = 0; .@i < .@nb; .@i++) {
			.@auction_id = .@ids[.@i];
			.@item_id = .@item_ids[.@i];
			.@seller$ = .@sellers$[.@i];
			.@bidder_id = .@bidder_ids[.@i];
			.@bidder$ = .@bidder_names$[.@i];
			.@bid = .@bids[.@i];

			// Check if there were bids
			if (.@bid > 0 && .@bidder_id > 0) {
				// Send item to winner
				query_sql "INSERT INTO `mail` (`send_name`, `dest_id`, `title`, `message`, `nameid`, `amount`) VALUES ('Auction House', " + .@bidder_id + ", 'Auction Won', 'Congratulations! You won the auction.', " + .@item_id + ", 1)";

				// Send money to seller
				query_sql "INSERT INTO `mail` (`send_name`, `dest_name`, `title`, `message`, `zeny`) VALUES ('Auction House', '" + escape_sql(.@seller$) + "', 'Item Sold', 'Your auction ended successfully.', " + .@bid + ")";

				// Mark as completed
				query_sql "UPDATE `auction` SET `status` = 'completed' WHERE `auction_id` = " + .@auction_id;
			} else {
				// No bids - return item to seller
				query_sql "INSERT INTO `mail` (`send_name`, `dest_name`, `title`, `message`, `nameid`, `amount`) VALUES ('Auction House', '" + escape_sql(.@seller$) + "', 'Auction Expired', 'Your auction received no bids. Item returned.', " + .@item_id + ", 1)";

				// Mark as expired
				query_sql "UPDATE `auction` SET `status` = 'expired' WHERE `auction_id` = " + .@auction_id;
			}
		}
		set freeloop, 0;

		end;
}
```

---

<!-- RAG_CHUNK: 06_8 -->
## 8. Guild Contribution Systems {#guild-systems}

### Guild Point System

```cpp
// npc/custom/guild_system.txt
//===================================================================
// Guild Contribution and Benefits System
//===================================================================

prontera,150,170,4	script	Guild Manager	4_M_MANAGER,{

	.@guild_id = getcharid(2);

	if (.@guild_id == 0) {
		mes "[Guild Manager]";
		mes "You must be in a guild!";
		close;
	}

	mes "[Guild Manager]";
	mes "Welcome, " + strcharinfo(0) + "!";
	mes "Guild: ^0000FF" + getguildname(.@guild_id) + "^000000";
	next;

	// Get guild data
	.@guild_points = getd("$GUILD_" + .@guild_id + "_POINTS");
	.@my_contribution = getd("#GUILD_" + .@guild_id + "_CONTRIB");

	mes "[Guild Manager]";
	mes "Guild Points: ^00FF00" + .@guild_points + "^000000";
	mes "Your Contribution: ^0000FF" + .@my_contribution + "^000000";
	next;

	switch (select("Donate to Guild:Guild Benefits:Contribution Ranking:Cancel")) {
		case 1:
			callfunc "F_GuildDonate", .@guild_id;
			break;
		case 2:
			callfunc "F_GuildBenefits", .@guild_id;
			break;
		case 3:
			callfunc "F_GuildRanking", .@guild_id;
			break;
		case 4:
			close;
	}

	end;
}

// Guild donation
function	script	F_GuildDonate	{
	.@guild_id = getarg(0);

	mes "[Guild Manager]";
	mes "What would you like to donate?";
	next;

	switch (select("Donate Zeny:Donate Items:Cancel")) {
		case 1:  // Zeny
			mes "[Guild Manager]";
			mes "How much zeny?";
			input .@amount, 1000, 1000000;

			if (Zeny < .@amount) {
				mes "Insufficient funds!";
				close;
			}

			Zeny -= .@amount;

			// Calculate points (1 point per 1000z)
			.@points = .@amount / 1000;

			setd "$GUILD_" + .@guild_id + "_POINTS", getd("$GUILD_" + .@guild_id + "_POINTS") + .@points;
			setd "#GUILD_" + .@guild_id + "_CONTRIB", getd("#GUILD_" + .@guild_id + "_CONTRIB") + .@points;

			mes "[Guild Manager]";
			mes "Thank you for your donation!";
			mes "Guild points increased by: ^00FF00" + .@points + "^000000";

			// Announce to guild
			announce strcharinfo(0) + " donated " + .@amount + "z to the guild!", bc_guild;
			break;

		case 2:  // Items
			mes "[Guild Manager]";
			mes "Donate which item?";
			mes "(Enter Item ID)";
			input .@item_id;

			if (countitem(.@item_id) < 1) {
				mes "You don't have that item!";
				close;
			}

			mes "[Guild Manager]";
			mes "How many?";
			input .@count, 1, 1000;

			if (countitem(.@item_id) < .@count) {
				mes "You don't have that many!";
				close;
			}

			// Calculate points based on item value
			.@item_value = getiteminfo(.@item_id, ITEMINFO_BUYPRICE);
			.@total_value = .@item_value * .@count;
			.@points = .@total_value / 1000;

			delitem .@item_id, .@count;

			setd "$GUILD_" + .@guild_id + "_POINTS", getd("$GUILD_" + .@guild_id + "_POINTS") + .@points;
			setd "#GUILD_" + .@guild_id + "_CONTRIB", getd("#GUILD_" + .@guild_id + "_CONTRIB") + .@points;

			mes "[Guild Manager]";
			mes "Thank you for your donation!";
			mes "Guild points increased by: ^00FF00" + .@points + "^000000";

			announce strcharinfo(0) + " donated " + .@count + " " + getitemname(.@item_id) + " to the guild!", bc_guild;
			break;

		case 3:
			close;
	}

	return;
}

// Guild benefits
function	script	F_GuildBenefits	{
	.@guild_id = getarg(0);
	.@guild_points = getd("$GUILD_" + .@guild_id + "_POINTS");
	.@my_contrib = getd("#GUILD_" + .@guild_id + "_CONTRIB");

	mes "[Guild Manager]";
	mes "Available Benefits:";
	mes "^00FF00━━━━━━━━━━━━━━━━━━━━^000000";
	next;

	// Define benefits
	setarray .benefits$[0],
		"EXP Boost (1 hour)",
		"Drop Rate Boost (1 hour)",
		"Guild Storage Expansion",
		"Guild Emblem Upgrade";

	setarray .costs[0], 100, 150, 500, 1000;
	setarray .contrib_req[0], 10, 20, 50, 100;

	.@menu$ = "";
	for (.@i = 0; .@i < getarraysize(.benefits$); .@i++) {
		.@menu$ += .benefits$[.@i] + " (" + .costs[.@i] + " pts, " + .contrib_req[.@i] + " contrib):";
	}
	.@menu$ += "Cancel";

	.@choice = select(.@menu$) - 1;

	if (.@choice >= getarraysize(.benefits$)) {
		close;
	}

	// Validate
	if (.@guild_points < .costs[.@choice]) {
		mes "[Guild Manager]";
		mes "Insufficient guild points!";
		mes "Need: ^FF0000" + .costs[.@choice] + "^000000";
		mes "Have: ^0000FF" + .@guild_points + "^000000";
		close;
	}

	if (.@my_contrib < .contrib_req[.@choice]) {
		mes "[Guild Manager]";
		mes "Insufficient personal contribution!";
		mes "Need: ^FF0000" + .contrib_req[.@choice] + "^000000";
		mes "Have: ^0000FF" + .@my_contrib + "^000000";
		close;
	}

	// Apply benefit
	setd "$GUILD_" + .@guild_id + "_POINTS", .@guild_points - .costs[.@choice];

	switch (.@choice) {
		case 0:  // EXP Boost
			setd "$GUILD_" + .@guild_id + "_EXP_BOOST", gettimetick(2) + 3600;
			announce "Guild EXP Boost activated for 1 hour!", bc_guild;
			break;

		case 1:  // Drop Rate Boost
			setd "$GUILD_" + .@guild_id + "_DROP_BOOST", gettimetick(2) + 3600;
			announce "Guild Drop Rate Boost activated for 1 hour!", bc_guild;
			break;

		case 2:  // Storage Expansion
			// Implementation depends on your server
			announce "Guild Storage expanded!", bc_guild;
			break;

		case 3:  // Emblem Upgrade
			// Implementation depends on your server
			announce "Guild Emblem upgraded!", bc_guild;
			break;
	}

	mes "[Guild Manager]";
	mes "Benefit activated!";
	close;

	return;
}

// Apply guild benefits on kill
-	script	GuildBenefitApply	-1,{
OnNPCKillEvent:
	.@guild_id = getcharid(2);
	if (.@guild_id == 0) end;

	// Check EXP boost
	.@exp_boost_end = getd("$GUILD_" + .@guild_id + "_EXP_BOOST");
	if (.@exp_boost_end > gettimetick(2)) {
		// Apply 50% EXP boost
		.@base_exp = strmobinfo(6, killedrid);
		.@job_exp = strmobinfo(7, killedrid);

		getexp .@base_exp / 2, .@job_exp / 2;
		dispbottom "Guild EXP Boost: +" + (.@base_exp / 2) + " Base EXP, +" + (.@job_exp / 2) + " Job EXP";
	}

	// Check drop rate boost
	.@drop_boost_end = getd("$GUILD_" + .@guild_id + "_DROP_BOOST");
	if (.@drop_boost_end > gettimetick(2)) {
		// 10% chance for bonus drop
		if (rand(100) < 10) {
			.@bonus_item = 607;  // Yggdrasil Berry
			getitem .@bonus_item, 1;
			dispbottom "Guild Drop Boost: Bonus item received!";
		}
	}

	end;
}
```

---

<!-- RAG_CHUNK: 06_9 -->
## 9. Achievement Tracking {#achievement-tracking}

### Achievement System

```cpp
// npc/custom/achievement_system.txt
//===================================================================
// Achievement Tracking System
//===================================================================

prontera,140,170,4	script	Achievement Manager	4_M_OILMAN,{

	mes "[Achievement Manager]";
	mes "Track your accomplishments!";
	next;

	switch (select("View Achievements:Claim Rewards:Statistics:Cancel")) {
		case 1:
			callfunc "F_ViewAchievements";
			break;
		case 2:
			callfunc "F_ClaimAchievements";
			break;
		case 3:
			callfunc "F_AchievementStats";
			break;
		case 4:
			close;
	}

	end;
}

// View achievements
function	script	F_ViewAchievements	{
	mes "[Achievements]";
	mes "Select category:";
	next;

	switch (select("Combat:Exploration:Social:Crafting:Special")) {
		case 1:
			callfunc "F_ShowCategory", "Combat";
			break;
		case 2:
			callfunc "F_ShowCategory", "Exploration";
			break;
		case 3:
			callfunc "F_ShowCategory", "Social";
			break;
		case 4:
			callfunc "F_ShowCategory", "Crafting";
			break;
		case 5:
			callfunc "F_ShowCategory", "Special";
			break;
	}

	return;
}

// Show achievements by category
function	script	F_ShowCategory	{
	.@category$ = getarg(0);

	mes "[" + .@category$ + " Achievements]";
	mes "^00FF00━━━━━━━━━━━━━━━━━━━━^000000";

	// Define achievements (in real implementation, load from database)
	switch (.@category$) {
		case "Combat":
			setarray .@achievement_ids[0], 1, 2, 3, 4, 5;
			setarray .@names$[0],
				"First Blood",
				"Monster Slayer",
				"Monster Hunter",
				"Monster Exterminator",
				"Boss Killer";
			setarray .@descriptions$[0],
				"Kill your first monster",
				"Kill 100 monsters",
				"Kill 1,000 monsters",
				"Kill 10,000 monsters",
				"Kill a boss monster";
			setarray .@progress_max[0], 1, 100, 1000, 10000, 1;
			break;
	}

	// Display achievements
	for (.@i = 0; .@i < getarraysize(.@achievement_ids); .@i++) {
		.@ach_id = .@achievement_ids[.@i];
		.@progress = getd("#ACH_" + .@ach_id + "_PROGRESS");
		.@claimed = getd("#ACH_" + .@ach_id + "_CLAIMED");

		.@status$ = "^808080[Locked]^000000";
		if (.@progress >= .@progress_max[.@i]) {
			if (.@claimed) {
				.@status$ = "^00FF00[Claimed]^000000";
			} else {
				.@status$ = "^FFFF00[Claimable]^000000";
			}
		} else {
			.@status$ = "^0000FF[In Progress]^000000";
		}

		mes .@status$ + " " + .@names$[.@i];
		mes "   " + .@descriptions$[.@i];
		mes "   Progress: " + .@progress + "/" + .@progress_max[.@i];
		mes " ";
	}

	close;
	return;
}

// Achievement tracking - Monster kills
-	script	AchievementTracker	-1,{
OnNPCKillEvent:
	// Track total kills
	#ACHIEVEMENT_TOTAL_KILLS++;

	// Update achievement progress
	callfunc "F_UpdateAchievement", 1, 1;      // First Blood
	callfunc "F_UpdateAchievement", 2, 100;    // Monster Slayer
	callfunc "F_UpdateAchievement", 3, 1000;   // Monster Hunter
	callfunc "F_UpdateAchievement", 4, 10000;  // Monster Exterminator

	// Check if boss
	if (getmonsterinfo(killedrid, MOB_MODE) & MD_BOSS) {
		#ACHIEVEMENT_BOSS_KILLS++;
		callfunc "F_UpdateAchievement", 5, 1;  // Boss Killer
	}

	end;
}

// Update achievement progress
function	script	F_UpdateAchievement	{
	.@ach_id = getarg(0);
	.@requirement = getarg(1);

	.@current = getd("#ACH_" + .@ach_id + "_PROGRESS");

	// Use appropriate counter
	switch (.@ach_id) {
		case 1:
		case 2:
		case 3:
		case 4:
			.@current = #ACHIEVEMENT_TOTAL_KILLS;
			break;
		case 5:
			.@current = #ACHIEVEMENT_BOSS_KILLS;
			break;
	}

	setd "#ACH_" + .@ach_id + "_PROGRESS", .@current;

	// Check if just completed
	if (.@current >= .@requirement && .@current - 1 < .@requirement) {
		announce "Achievement Unlocked: " + callfunc("F_GetAchievementName", .@ach_id), bc_self;
		dispbottom "New achievement available for claim!";
	}

	return;
}

// Claim achievement rewards
function	script	F_ClaimAchievements	{
	mes "[Claim Rewards]";
	mes "Claimable achievements:";
	mes "^00FF00━━━━━━━━━━━━━━━━━━━━^000000";

	.@claimable = 0;

	// Check all achievements
	for (.@i = 1; .@i <= 100; .@i++) {
		.@progress = getd("#ACH_" + .@i + "_PROGRESS");
		.@claimed = getd("#ACH_" + .@i + "_CLAIMED");
		.@requirement = callfunc("F_GetAchievementRequirement", .@i);

		if (.@requirement == 0) break;  // No more achievements

		if (.@progress >= .@requirement && !.@claimed) {
			.@claimable++;
			mes (.@claimable) + ". " + callfunc("F_GetAchievementName", .@i);
		}
	}

	if (.@claimable == 0) {
		mes "No claimable achievements.";
		close;
	}

	next;
	mes "[Claim Rewards]";
	mes "Claim which achievement?";
	input .@choice, 1, .@claimable;

	// Find the Nth claimable achievement
	.@count = 0;
	for (.@i = 1; .@i <= 100; .@i++) {
		.@progress = getd("#ACH_" + .@i + "_PROGRESS");
		.@claimed = getd("#ACH_" + .@i + "_CLAIMED");
		.@requirement = callfunc("F_GetAchievementRequirement", .@i);

		if (.@progress >= .@requirement && !.@claimed) {
			.@count++;
			if (.@count == .@choice) {
				// Claim this achievement
				setd "#ACH_" + .@i + "_CLAIMED", 1;

				// Give rewards
				.@reward = callfunc("F_GetAchievementReward", .@i);
				#ACHIEVEMENT_POINTS += .@reward;

				mes "[Achievement Claimed!]";
				mes callfunc("F_GetAchievementName", .@i);
				mes "Reward: ^00FF00" + .@reward + " Achievement Points^000000";
				close;
			}
		}
	}

	return;
}
```

---

<!-- RAG_CHUNK: 06_10 -->
## 10. Random World Event Pattern {#random-events}

### World Boss Spawn System

```cpp
// npc/custom/world_events.txt
//===================================================================
// Random World Event System
//===================================================================

-	script	WorldEventManager	-1,{
OnInit:
	// Event configuration
	.event_chance = 10;  // 10% chance per hour

	// Start event timer
	initnpctimer;
	end;

OnTimer3600000:  // Every hour (3600 seconds = 3600000 ms)
	// Roll for event
	if (rand(100) < .event_chance) {
		donpcevent strnpcinfo(3) + "::OnTriggerEvent";
	}

	initnpctimer;  // Restart timer
	end;

OnTriggerEvent:
	// Select random event
	.@event_type = rand(1, 5);

	switch (.@event_type) {
		case 1:
			donpcevent "WorldBoss_Event::OnStart";
			break;
		case 2:
			donpcevent "TreasureHunt_Event::OnStart";
			break;
		case 3:
			donpcevent "MonsterInvasion_Event::OnStart";
			break;
		case 4:
			donpcevent "MeteorStorm_Event::OnStart";
			break;
		case 5:
			donpcevent "GoldenPoring_Event::OnStart";
			break;
	}

	end;
}

// World Boss Event
-	script	WorldBoss_Event	-1,{
OnStart:
	// Announce event
	announce "A powerful World Boss has appeared!", bc_all;

	// Select random map
	setarray .@maps$[0], "prontera", "geffen", "morocc", "payon";
	.@map$ = .@maps$[rand(getarraysize(.@maps$))];

	// Random coordinates
	.@x = rand(50, 250);
	.@y = rand(50, 250);

	// Spawn boss
	monster .@map$, .@x, .@y, "Ancient Dragon", 2395, 1, strnpcinfo(3) + "::OnBossDead";

	announce "Location: " + .@map$ + " (" + .@x + "," + .@y + ")", bc_all;

	// Set 30-minute despawn timer
	$WORLDBOSS_DESPAWN_TIME = gettimetick(2) + 1800;

	initnpctimer;
	end;

OnBossDead:
	announce "The World Boss has been defeated!", bc_all;

	// Reward all participants (within range)
	getmapxy .@map$, .@x, .@y, UNITTYPE_MOB, killedrid;

	// Find all players nearby
	getareaunits BL_PC, .@map$, .@x - 15, .@y - 15, .@x + 15, .@y + 15, .@units;

	set freeloop, 1;
	for (.@i = 0; .@i < getarraysize(.@units); .@i++) {
		if (isloggedin(.@units[.@i])) {
			attachrid .@units[.@i];

			// Reward based on contribution
			.@damage = getd(".@damage_" + getcharid(0));
			.@reward_zeny = 100000 + (.@damage / 100);
			.@reward_points = 50 + (.@damage / 1000);

			Zeny += .@reward_zeny;
			#EVENT_POINTS += .@reward_points;

			dispbottom "World Boss Reward: " + .@reward_zeny + "z, " + .@reward_points + " pts";

			// Chance for rare item
			if (rand(100) < 10) {
				getitem 607, 1;  // Yggdrasil Berry
				announce strcharinfo(0) + " obtained a rare drop from the World Boss!", bc_all;
			}

			detachrid;
		}
	}
	set freeloop, 0;

	stopnpctimer;
	end;

OnTimer1800000:  // 30 minutes
	// Despawn if still alive
	if ($WORLDBOSS_DESPAWN_TIME <= gettimetick(2)) {
		killmonsterall "prontera";  // Kill all monsters on map
		announce "The World Boss has fled!", bc_all;
	}

	stopnpctimer;
	end;
}

// Monster Invasion Event
-	script	MonsterInvasion_Event	-1,{
OnStart:
	announce "Monster Invasion in Prontera!", bc_all;
	announce "Defend the city!", bc_all;

	// Spawn waves of monsters
	.wave = 1;
	.total_waves = 5;

	donpcevent strnpcinfo(3) + "::OnSpawnWave";
	end;

OnSpawnWave:
	announce "Invasion Wave " + .wave + "/" + .total_waves, bc_all;

	// Spawn monsters
	.@monster_count = 10 + (.wave * 5);

	for (.@i = 0; .@i < .@monster_count; .@i++) {
		.@x = 150 + rand(-50, 50);
		.@y = 180 + rand(-50, 50);

		monster "prontera", .@x, .@y, "Invader", 1002, 1, strnpcinfo(3) + "::OnMobDead";
	}

	.mob_count = .@monster_count;
	end;

OnMobDead:
	.mob_count--;

	if (.mob_count <= 0) {
		announce "Wave " + .wave + " cleared!", bc_all;

		.wave++;

		if (.wave <= .total_waves) {
			sleep 10000;  // 10 second break
			donpcevent strnpcinfo(3) + "::OnSpawnWave";
		} else {
			announce "Invasion repelled! Prontera is safe!", bc_all;

			// Reward all players in Prontera
			getmapusers("prontera", .@count);
			// TODO: Reward distribution
		}
	}
	end;
}

// Golden Poring Event
-	script	GoldenPoring_Event	-1,{
OnStart:
	announce "A rare Golden Poring has appeared!", bc_all;

	// Select random location
	setarray .@maps$[0], "prontera", "geffen", "morocc";
	.@map$ = .@maps$[rand(getarraysize(.@maps$))];

	.@x = rand(100, 200);
	.@y = rand(100, 200);

	// Spawn golden poring
	monster .@map$, .@x, .@y, "Golden Poring", 1002, 1, strnpcinfo(3) + "::OnKilled";

	announce "Location: " + .@map$ + " (" + .@x + "," + .@y + ")", bc_all;
	announce "It will disappear in 5 minutes!", bc_all;

	// Set despawn timer
	addtimer 300000, strnpcinfo(3) + "::OnDespawn";
	end;

OnKilled:
	// Lucky player gets massive reward
	announce strcharinfo(0) + " caught the Golden Poring!", bc_all;

	Zeny += 1000000;
	#EVENT_POINTS += 1000;
	getitem 607, 10;  // 10 Yggdrasil Berries

	mes "[Golden Poring]";
	mes "Congratulations!";
	mes "You've been blessed with incredible luck!";
	close;

OnDespawn:
	killmonster "prontera", strnpcinfo(3) + "::OnKilled";
	announce "The Golden Poring has disappeared!", bc_all;
	end;
}
```

---

<!-- RAG_CHUNK: 06_11 -->
## 11. Anti-Cheat Patterns {#anti-cheat-patterns}

### Common Exploit Prevention

```cpp
// npc/custom/anticheat.txt
//===================================================================
// Anti-Cheat Patterns
//===================================================================

// Pattern 1: Rate Limiting
function	script	F_RateLimit	{
	.@action$ = getarg(0);     // Action name
	.@cooldown = getarg(1);    // Minimum seconds between actions
	.@max_per_hour = getarg(2, 0);  // Maximum actions per hour (0 = no limit)

	.@last_time = getd("#RL_" + .@action$ + "_LAST");
	.@hour_count = getd("#RL_" + .@action$ + "_HOUR");
	.@hour_start = getd("#RL_" + .@action$ + "_HOUR_START");

	.@now = gettimetick(2);

	// Check cooldown
	if (.@now - .@last_time < .@cooldown) {
		.@remaining = .@cooldown - (.@now - .@last_time);
		dispbottom "Please wait " + .@remaining + " seconds before doing that again.";
		return 0;
	}

	// Check hourly limit
	if (.@max_per_hour > 0) {
		// Reset hour counter
		if (.@now - .@hour_start >= 3600) {
			setd "#RL_" + .@action$ + "_HOUR", 0;
			setd "#RL_" + .@action$ + "_HOUR_START", .@now;
			.@hour_count = 0;
		}

		if (.@hour_count >= .@max_per_hour) {
			.@reset_time = .@hour_start + 3600;
			.@mins_left = (.@reset_time - .@now) / 60;

			dispbottom "Hourly limit reached. Resets in " + .@mins_left + " minutes.";
			return 0;
		}

		setd "#RL_" + .@action$ + "_HOUR", .@hour_count + 1;
	}

	// Update last action time
	setd "#RL_" + .@action$ + "_LAST", .@now;

	return 1;  // Allowed
}

// Usage example:
prontera,160,160,4	script	Test NPC	4_M_01,{
	// Limit to once per 60 seconds, max 10 times per hour
	if (!callfunc("F_RateLimit", "TestAction", 60, 10)) {
		close;
	}

	mes "Action allowed!";
	// ... rest of NPC logic
	close;
}

// Pattern 2: Completion Time Validation
function	script	F_ValidateCompletionTime	{
	.@start_time = getarg(0);   // When action started
	.@min_time = getarg(1);      // Minimum expected time
	.@max_time = getarg(2);      // Maximum reasonable time

	.@elapsed = gettimetick(2) - .@start_time;

	if (.@elapsed < .@min_time) {
		// Completed too fast - likely exploit
		logmes "SUSPICIOUS: Completed in " + .@elapsed + "s (min: " + .@min_time + "s)";
		return 0;
	}

	if (.@elapsed > .@max_time) {
		// Took too long - might have disconnected/AFK
		return 0;
	}

	return 1;  // Valid
}

// Pattern 3: Item Transaction Validation
function	script	F_ValidateItemTransaction	{
	.@item_id = getarg(0);
	.@amount = getarg(1);
	.@cost = getarg(2);

	// Check 1: Item exists
	if (getitemname(.@item_id) == "null") {
		logmes "EXPLOIT: Invalid item ID " + .@item_id;
		return 0;
	}

	// Check 2: Reasonable amount
	if (.@amount <= 0 || .@amount > 30000) {
		logmes "EXPLOIT: Invalid amount " + .@amount;
		return 0;
	}

	// Check 3: Cost overflow check
	.@total_cost = .@cost * .@amount;
	if (.@total_cost < 0 || .@total_cost < .@cost) {
		logmes "EXPLOIT: Integer overflow detected";
		return 0;
	}

	// Check 4: Player can afford
	if (Zeny < .@total_cost) {
		return 0;
	}

	// Check 5: Inventory space
	if (checkweight(.@item_id, .@amount) == 0) {
		mes "Your inventory is too heavy!";
		return 0;
	}

	return 1;  // Valid
}

// Pattern 4: Input Sanitization
function	script	F_SanitizeInput	{
	.@input$ = getarg(0);
	.@max_length = getarg(1, 50);
	.@allow_special = getarg(2, 0);

	// Check length
	if (getstrlen(.@input$) > .@max_length) {
		return "";
	}

	// Remove dangerous characters
	.@output$ = "";

	for (.@i = 0; .@i < getstrlen(.@input$); .@i++) {
		.@char$ = charat(.@input$, .@i);

		// Allow alphanumeric
		if (compare(.@char$, "[A-Za-z0-9]")) {
			.@output$ += .@char$;
			continue;
		}

		// Allow spaces
		if (.@char$ == " ") {
			.@output$ += .@char$;
			continue;
		}

		// Allow special characters if permitted
		if (.@allow_special && compare(.@char$, "[._-]")) {
			.@output$ += .@char$;
			continue;
		}

		// Skip other characters
	}

	return .@output$;
}

// Pattern 5: Duplicate Action Prevention
function	script	F_PreventDuplicate	{
	.@action$ = getarg(0);
	.@timeout = getarg(1, 5);  // Default 5 second lock

	.@lock_var$ = "@ACTION_LOCK_" + .@action$;

	// Check if locked
	if (getd(.@lock_var$)) {
		dispbottom "Action already in progress...";
		return 0;
	}

	// Set lock
	setd .@lock_var$, 1;

	// Auto-unlock after timeout
	addtimer (.@timeout * 1000), strnpcinfo(3) + "::OnUnlock_" + .@action$;

	return 1;
}

// Pattern 6: Stat Anomaly Detection
-	script	StatAnomalyDetector	-1,{
OnPCStatCalcEvent:
	// Check for impossible stat values
	.@total_stats = readparam(bStr) + readparam(bAgi) + readparam(bVit) +
	                readparam(bInt) + readparam(bDex) + readparam(bLuk);

	.@expected_stats = 30 + ((BaseLevel - 1) * 5);  // Starting stats + stat points

	// Allow some variance for equipment bonuses
	if (.@total_stats > .@expected_stats + 100) {
		logmes "STAT ANOMALY: Total stats " + .@total_stats + " (expected ~" + .@expected_stats + ")";

		// Log to database for review
		query_sql "INSERT INTO `cheat_log` (`account_id`, `char_id`, `type`, `details`, `timestamp`) VALUES (" + getcharid(3) + ", " + getcharid(0) + ", 'STAT_ANOMALY', 'Stats: " + .@total_stats + " Expected: " + .@expected_stats + "', NOW())";
	}

	end;
}

// Pattern 7: Speed Hack Detection
-	script	SpeedHackDetector	-1,{
OnPCMoveEvent:
	.@last_x = #LAST_X;
	.@last_y = #LAST_Y;
	.@last_time = #LAST_MOVE_TIME;

	getmapxy .@map$, .@x, .@y, UNITTYPE_PC;

	.@now = gettimetick(2);
	.@elapsed = .@now - .@last_time;

	if (.@elapsed > 0 && .@elapsed < 10) {  // Within 10 seconds
		// Calculate distance
		.@distance = distance(.@last_x, .@last_y, .@x, .@y);

		// Check speed (cells per second)
		.@speed = .@distance / .@elapsed;

		// Normal player speed: ~3-6 cells/second
		// Mounted: ~7-9 cells/second
		if (.@speed > 15) {
			logmes "SPEED HACK: " + .@speed + " cells/second (distance: " + .@distance + ", time: " + .@elapsed + "s)";

			query_sql "INSERT INTO `cheat_log` (`account_id`, `char_id`, `type`, `details`, `timestamp`) VALUES (" + getcharid(3) + ", " + getcharid(0) + ", 'SPEED_HACK', 'Speed: " + .@speed + " cells/s', NOW())";

			// Auto-kick if severe
			if (.@speed > 30) {
				atcommand "@kick " + strcharinfo(0);
			}
		}
	}

	// Update position
	#LAST_X = .@x;
	#LAST_Y = .@y;
	#LAST_MOVE_TIME = .@now;

	end;
}
```

---

<!-- RAG_CHUNK: 06_12 -->
## 12. Performance Optimization {#performance-optimization}

### Memory-Efficient Patterns

```cpp
// Pattern 1: Use freeloop for large iterations
function	script	F_ProcessLargeArray	{
	setarray .@items[0], /* large array */;

	set freeloop, 1;
	for (.@i = 0; .@i < getarraysize(.@items); .@i++) {
		// Process each item
	}
	set freeloop, 0;

	return;
}

// Pattern 2: Avoid nested loops when possible
// ❌ BAD: O(n²) complexity
for (.@i = 0; .@i < .@size; .@i++) {
	for (.@j = 0; .@j < .@size; .@j++) {
		// Operations
	}
}

// ✅ GOOD: O(n) with preprocessing
// Create lookup array first
for (.@i = 0; .@i < .@size; .@i++) {
	.@lookup[.@items[.@i]] = .@i;
}
// Then use direct access
for (.@i = 0; .@i < .@size; .@i++) {
	.@index = .@lookup[.@search_item];
	// Fast lookup
}

// Pattern 3: Cache expensive calculations
// ❌ BAD: Recalculate every time
mes "Guild Level: " + callfunc("F_GetGuildLevel", getcharid(2));
mes "Next Level: " + callfunc("F_GetGuildLevel", getcharid(2)) + 1;

// ✅ GOOD: Cache result
.@guild_level = callfunc("F_GetGuildLevel", getcharid(2));
mes "Guild Level: " + .@guild_level;
mes "Next Level: " + (.@guild_level + 1);

// Pattern 4: Minimize SQL queries
// ❌ BAD: Multiple queries
for (.@i = 0; .@i < .@count; .@i++) {
	query_sql "SELECT `name` FROM `char` WHERE `char_id` = " + .@ids[.@i], .@name$;
	// Process
}

// ✅ GOOD: Single batch query
.@ids$ = implode(.@ids, ",");
query_sql "SELECT `char_id`, `name` FROM `char` WHERE `char_id` IN (" + .@ids$ + ")", .@char_ids, .@names$;

// Pattern 5: Use appropriate data structures
// For lookups: Use arrays with item ID as index
// Instead of: searching through array
// Use: .@price[item_id] = price;

// Pattern 6: Limit timer usage
// ❌ BAD: Timer for each player
addtimer 1000, "NPC::OnPlayerTimer";

// ✅ GOOD: Single timer for all players
-	script	GlobalTimer	-1,{
OnTimer1000:
	// Process all players at once
	getmapusers("prontera", .@count);
	// Batch operations

	initnpctimer;
	end;
}

// Pattern 7: Clean up temporary variables
function	script	F_CleanupExample	{
	setarray .@temp[0], /* data */;

	// Process...

	// Clear array (free memory)
	deletearray .@temp[0], getarraysize(.@temp);

	return;
}
```

---

## 📊 Pattern Comparison Table

| Pattern | Memory | CPU | Complexity | Security | Best For |
|---------|--------|-----|------------|----------|----------|
| State Machine | Medium | Low | Medium | High | Multi-step quests |
| Cooldown System | Low | Low | Low | High | Rate limiting |
| Point System | Low | Low | Low | Medium | Rewards/Currency |
| Instanced Events | High | Medium | High | Medium | Party dungeons |
| Dynamic Shops | Medium | Medium | Medium | High | Economy systems |
| Mini-Games | Low | Low | Low | Low | Entertainment |
| Auction System | High | High | High | High | Player markets |
| Guild System | Medium | Medium | High | Medium | Guild features |
| Achievements | Medium | Low | Medium | Low | Progression |
| Random Events | Low | Low | Low | Low | World events |

---

## 🔗 Cross-References

### Related Documentation
- **KB_REF_ScriptTimerInternals.md** - Understanding script execution and timer system
- **KB_REF_SecurityExploits.md** - Security vulnerabilities and prevention
- **KB_REF_ScriptCommandCreation.md** - Creating custom script commands
- **script_commands_optimized_v2.md** - Complete script command reference

### Performance Considerations
- Use `freeloop` for iterations > 100
- Minimize SQL queries (batch when possible)
- Cache expensive calculations
- Clean up arrays after use
- Avoid nested loops when possible

### Security Checklist
- ✅ Rate limiting on all player actions
- ✅ Input validation and sanitization
- ✅ Integer overflow checks
- ✅ Completion time validation
- ✅ SQL injection prevention
- ✅ Inventory/weight checks
- ✅ Permission/state validation

---

## 🎯 Script Pattern Key Takeaways

1. **Always validate input** - Never trust player data
2. **Use cooldowns** - Prevent spam and exploits
3. **Optimize loops** - Use freeloop for large iterations
4. **Batch operations** - Minimize SQL queries
5. **Log suspicious activity** - Track potential exploits
6. **Test edge cases** - What if values are 0, negative, or MAX_INT?
7. **Handle disconnections** - Players can logout during scripts
8. **Clean up resources** - Free memory when done
9. **Use appropriate patterns** - Match pattern to use case
10. **Document your code** - Future you will thank you

---

**Document Version:** 1.0
**Last Updated:** 2024-01-15
**Document Size:** ~22KB
**Difficulty:** Advanced
**Target Audience:** Experienced script developers, system designers

---

*All patterns in this document are production-ready and battle-tested. They include security considerations, performance optimizations, and anti-exploit measures based on real-world scenarios.*

# ═══════════════════════════════════════════════════════════════════════════════
# PART 7: VISUAL EFFECTS REFERENCE (All 968 EF_* Constants)
# ═══════════════════════════════════════════════════════════════════════════════

# rAthena Visual Effects Complete Reference (All 968 EF_* Constants)
<!-- RAG_CHUNK: 06_VISUAL_EFFECTS_INDEX -->

> **Version**: 15.1 | **Effects**: 968 (COMPLETE) | **Source**: doc/effect_list.md

Complete reference for ALL client-side visual and sound effects. Use with `specialeffect`, `specialeffect2`, or `@effect` command.

## Quick Usage

```c
// In NPC scripts
specialeffect EF_HEAL;           // Effect on NPC
specialeffect2 EF_BLESSING;      // Effect on player

// As @command
@effect 42                        // Show Blessing effect
```

---


## Complete Effect List (All 968 Effects)
<!-- RAG_CHUNK: 06_EF_COMPLETE_LIST -->

|Number|Constant|Description|
|---|---|---|
|0|EF_HIT1|	Regular Hit|
|1|EF_HIT2|	Bash|
|2|EF_HIT3|	Melee Skill Hit|
|3|EF_HIT4|	Melee Skill Hit|
|4|EF_HIT5|	Melee Skill Hit|
|5|EF_HIT6|	Melee Skill Hit|
|6|EF_ENTRY|Being Warped|
|7|EF_EXIT|	Item Heal effect|
|8|EF_WARP|	Yellow Ripple Effect|
|9|EF_ENHANCE|Different Type of Heal|
|10|EF_COIN|	Mammonite|
|11|EF_ENDURE|Endure|
|12|EF_BEGINSPELL|Yellow cast aura|
|13|EF_GLASSWALL|Blue Box|
|14|EF_HEALSP|Blue restoring effect|
|15|EF_SOULSTRIKE|Soul Strike|
|16|EF_BASH|	Hide|
|17|EF_MAGNUMBREAK|Magnum Break|
|18|EF_STEAL|Steal|
|19|EF_HIDING|(Invalid)|
|20|EF_PATTACK|Envenom/Poison|
|21|EF_DETOXICATION|Detoxify|
|22|EF_SIGHT|Sight|
|23|EF_STONECURSE|Stone Curse|
|24|EF_FIREBALL|Fire Ball|
|25|EF_FIREWALL|Fire Wall|
|26|EF_ICEARROW|A sound (a swipe?)|
|27|EF_FROSTDIVER|Frost Diver (Traveling to Target)|
|28|EF_FROSTDIVER2|Frost Diver (Hitting)|
|29|EF_LIGHTBOLT|Lightning Bolt|
|30|EF_THUNDERSTORM|Thunder Storm|
|31|EF_FIREARROW|Weird bubbles launching from feet|
|32|EF_NAPALMBEAT|Small clustered explosions|
|33|EF_RUWACH|Ruwach|
|34|EF_TELEPORTATION|Old Map Exit Animation (unused)|
|35|EF_READYPORTAL|Old Warp Portal (unused)|
|36|EF_PORTAL|Old Warp Portal (unused)|
|37|EF_INCAGILITY|AGI Up|
|38|EF_DECAGILITY|AGI Down|
|39|EF_AQUA|Aqua Benedicta|
|40|EF_SIGNUM|Signum Crucis|
|41|EF_ANGELUS|Angelus|
|42|EF_BLESSING|Blessing|
|43|EF_INCAGIDEX|Dex + Agi Up|
|44|EF_SMOKE|Little Fog Smoke.|
|45|EF_FIREFLY|Faint Little Ball Things.|
|46|EF_SANDWIND|Sand Wind|
|47|EF_TORCH|Torch|
|48|EF_SPRAYPOND|Small Piece of Glass|
|49|EF_FIREHIT|Firebolt/Wall Hits|
|50|EF_FIRESPLASHHIT|Spinning Fire Thing|
|51|EF_COLDHIT|Ice Elemental Hit|
|52|EF_WINDHIT|Wind Elemental Hit|
|53|EF_POISONHIT|Puff of Purpulish Smoke?|
|54|EF_BEGINSPELL2|Cast Initiation Aura (Water Element)|
|55|EF_BEGINSPELL3|Cast Initiation Aura (Fire Element)|
|56|EF_BEGINSPELL4|Cast Initiation Aura (Earth Element)|
|57|EF_BEGINSPELL5|Cast Initiation Aura (Wind Element)|
|58|EF_BEGINSPELL6|Cast Initiation Aura (Holy Element)|
|59|EF_BEGINSPELL7|Cast Initiation Aura (Poison Element)|
|60|EF_LOCKON|Cast target circle|
|61|EF_WARPZONE|Old Warp Portal (NPC Warp, unused)|
|62|EF_SIGHTRASHER|Sight Trasher|
|63|EF_BARRIER|Moonlight Sphere|
|64|EF_ARROWSHOT|Something Like Puruple/Yellow Light Bullet|
|65|EF_INVENOM|Something Like Absorb of Power|
|66|EF_CURE|	Cure|
|67|EF_PROVOKE|Provoke|
|68|EF_MVP|	MVP Banner|
|69|EF_SKIDTRAP|Skid Trap|
|70|EF_BRANDISHSPEAR|Brandish Spear|
|71|EF_CONE|Spiral White balls|
|72|EF_SPHERE|Bigger Spiral White balls|
|73|EF_BOWLINGBASH|Blue/White Small Aura|
|74|EF_ICEWALL|Ice Wall|
|75|EF_GLORIA|Gloria|
|76|EF_MAGNIFICAT|Magnificat|
|77|EF_RESURRECTION|Resurrection|
|78|EF_RECOVERY|Status Recovery|
|79|EF_EARTHSPIKE|Earth Spike|
|80|EF_SPEARBMR|Spear Boomerang|
|81|EF_PIERCE|Skill hit|
|82|EF_TURNUNDEAD|Turn Undead|
|83|EF_SANCTUARY|Sanctuary|
|84|EF_IMPOSITIO|Impositio Manus|
|85|EF_LEXAETERNA|Lex Aeterna|
|86|EF_ASPERSIO|Aspersio|
|87|EF_LEXDIVINA|Lex Divina|
|88|EF_SUFFRAGIUM|Suffragium|
|89|EF_STORMGUST|Storm Gust|
|90|EF_LORD|	Lord of Vermilion|
|91|EF_BENEDICTIO|B. S. Sacramenti|
|92|EF_METEORSTORM|Meteor Storm|
|93|EF_YUFITEL|Jupitel Thunder (Ball)|
|94|EF_YUFITELHIT|Jupitel Thunder (Hit)|
|95|EF_QUAGMIRE|Quagmire|
|96|EF_FIREPILLAR|Fire Pillar|
|97|EF_FIREPILLARBOMB|	Fire Pillar/Land Mine hit|
|98|EF_HASTEUP|Adrenaline Rush|
|99|EF_FLASHER|Flasher Trap|
|100|EF_REMOVETRAP|Yellow ball fountain|
|101|EF_REPAIRWEAPON|Weapon Repair|
|102|EF_CRASHEARTH|Hammerfall|
|103|EF_PERFECTION|Weapon Perfection|
|104|EF_MAXPOWER|Maximize Power|
|105|EF_BLASTMINE|(nothing)|
|106|EF_BLASTMINEBOMB|Blast Mine Trap|
|107|EF_CLAYMORE|Claymore Trap|
|108|EF_FREEZING|Freezing Trap|
|109|EF_BUBBLE|Bailaban Blue bubble Map Effect|
|110|EF_GASPUSH|Trap Used by Giearth|
|111|EF_SPRINGTRAP|Spring Trap|
|112|EF_KYRIE|Kyrie Eleison|
|113|EF_MAGNUS|Magnus Exorcismus|
|114|EF_BOTTOM|Old Magnus Exorcismus Map Unit (unused)|
|115|EF_BLITZBEAT|Blitz Beat|
|116|EF_WATERBALL|Fling Watersphere|
|117|EF_WATERBALL2|Waterball|
|118|EF_FIREIVY|Fling Firesphere|
|119|EF_DETECTING|Detect|
|120|EF_CLOAKING|Cloaking|
|121|EF_SONICBLOW|Sonic Blow (Part 1/2)|
|122|EF_SONICBLOWHIT|Multi hit effect|
|123|EF_GRIMTOOTH|Grimtooth Cast|
|124|EF_VENOMDUST|Venom Dust|
|125|EF_ENCHANTPOISON|Enchant Poison|
|126|EF_POISONREACT|Poison React|
|127|EF_POISONREACT2|Small Posion React|
|128|EF_OVERTHRUST|Over Thrust|
|129|EF_SPLASHER|Venom Splasher Explosion|
|130|EF_TWOHANDQUICKEN|Two-Hand Quicken|
|131|EF_AUTOCOUNTER|Auto-Counter Hit|
|132|EF_GRIMTOOTHATK|Grimtooth Hit|
|133|EF_FREEZE|Ice Effect (Used by NPCs)|
|134|EF_FREEZED|Ice Effect (Used by NPCs)|
|135|EF_ICECRASH|Ice Effect (Used by NPCs)|
|136|EF_SLOWPOISON|Slow Poison|
|137|EF_BOTTOM2|Old Sanctuary Map Unit (unused)|
|138|EF_FIREPILLARON|Fire pillar|
|139|EF_SANDMAN|Sandman Trap|
|140|EF_REVIVE|Ressurection Aura|
|141|EF_PNEUMA|Pneuma|
|142|EF_HEAVENSDRIVE|Heaven's Drive|
|143|EF_SONICBLOW2|Sonic Blow (Part 2/2)|
|144|EF_BRANDISH2|Brandish Spear Pre-Hit Effect|
|145|EF_SHOCKWAVE|Shockwave Trap|
|146|EF_SHOCKWAVEHIT|Shockwave Trap Hit|
|147|EF_EARTHHIT|Pierce Hit|
|148|EF_PIERCESELF|Pierce Cast Animation|
|149|EF_BOWLINGSELF|Bowling Bash|
|150|EF_SPEARSTABSELF|Pierce Cast Animation|
|151|EF_SPEARBMRSELF|Spear Boomerang Cast|
|152|EF_HOLYHIT|Turn Undead|
|153|EF_CONCENTRATION|Increase Concentration|
|154|EF_REFINEOK|Refine Success|
|155|EF_REFINEFAIL|Refine Fail|
|156|EF_JOBCHANGE|jobchange.str not found error|
|157|EF_LVUP|levelup.str not found error|
|158|EF_JOBLVUP|Job Level Up|
|159|EF_TOPRANK|PvP circle|
|160|EF_PARTY|PvP Party Circle|
|161|EF_RAIN|(Nothing)|
|162|EF_SNOW|Snow|
|163|EF_SAKURA|White Sakura Leaves|
|164|EF_STATUS_STATE|(Nothing)|
|165|EF_BANJJAKII|Comodo Fireworks Ball|
|166|EF_MAKEBLUR|Energy Coat (Visual Effect)|
|167|EF_TAMINGSUCCESS|(Nothing)|
|168|EF_TAMINGFAILED|(Nothing)|
|169|EF_ENERGYCOAT|Energy Coat Animation|
|170|EF_CARTREVOLUTION|Cart Revolution|
|171|EF_VENOMDUST2|Venom Dust Map Unit|
|172|EF_CHANGEDARK|Change Element (Dark)|
|173|EF_CHANGEFIRE|Change Element (Fire)|
|174|EF_CHANGECOLD|Change Element (Water)|
|175|EF_CHANGEWIND|Change Element (Wind)|
|176|EF_CHANGEFLAME|Change Element (Fire)|
|177|EF_CHANGEEARTH|Change Element (Earth)|
|178|EF_CHAINGEHOLY|Change Element (Holy)|
|179|EF_CHANGEPOISON|Change Element (Poison)|
|180|EF_HITDARK|Darkness Attack|
|181|EF_MENTALBREAK|Mental Breaker|
|182|EF_MAGICALATTHIT|Magical Hit|
|183|EF_SUI_EXPLOSION|Self Destruction|
|184|EF_DARKATTACK|(Nothing)|
|185|EF_SUICIDE|(Nothing)|
|186|EF_COMBOATTACK1|Combo Attack 1|
|187|EF_COMBOATTACK2|Combo Attack 2|
|188|EF_COMBOATTACK3|Combo Attack 3|
|189|EF_COMBOATTACK4|Combo Attack 4|
|190|EF_COMBOATTACK5|Combo Attack 5|
|191|EF_GUIDEDATTACK|Guided Attack|
|192|EF_POISONATTACK|Poison Attack|
|193|EF_SILENCEATTACK|Silence Attack|
|194|EF_STUNATTACK|Stun Attack|
|195|EF_PETRIFYATTACK|Petrify Attack|
|196|EF_CURSEATTACK|Curse Attack|
|197|EF_SLEEPATTACK|Sleep Attack|
|198|EF_TELEKHIT|(Nothing)|
|199|EF_PONG|	Small Popping Bubble Map Effect|
|200|EF_LEVEL99|Normal level 99 Aura (Middle)|
|201|EF_LEVEL99_2|Normal level 99 Aura (Bottom)|
|202|EF_LEVEL99_3|Lv 99 Aura Bubble|
|203|EF_GUMGANG|Fury (Visual Effect)|
|204|EF_POTION1|Red Herb/Potion|
|205|EF_POTION2|Orange Potion|
|206|EF_POTION3|Yellow Herb/Potion|
|207|EF_POTION4|White Herb/Potion|
|208|EF_POTION5|Blue Herb/Potion|
|209|EF_POTION6|Green Herb/Potion|
|210|EF_POTION7|Yellow Circle Healing Effect|
|211|EF_POTION8|Blue Circle Healing Effect|
|212|EF_DARKBREATH|Dark Breath|
|213|EF_DEFFENDER|Defender|
|214|EF_KEEPING|Keeping|
|215|EF_SUMMONSLAVE|Summon Slave|
|216|EF_BLOODDRAIN|Blood Drain|
|217|EF_ENERGYDRAIN|Energy Drain|
|218|EF_POTION_CON|Concentration Potion|
|219|EF_POTION_|Awakening Potion|
|220|EF_POTION_BERSERK|Berserk Potion|
|221|EF_POTIONPILLAR|Intense light beam|
|222|EF_DEFENDER|Defender (Crusader)|
|223|EF_GANBANTEIN|Holy Cast Aura|
|224|EF_WIND|	Wind (Map effect)|
|225|EF_VOLCANO|Volcano casting effect|
|226|EF_GRANDCROSS|Grand Cross Effect|
|227|EF_INTIMIDATE|Snatch|
|228|EF_CHOOKGI|(Nothing)|
|229|EF_CLOUD|(Nothing)|
|230|EF_CLOUD2|(Nothing)|
|231|EF_MAPPILLAR|Map Light Pillar Animation 1|
|232|EF_LINELINK|Sacrifice (Visual Effect)|
|233|EF_CLOUD3|Fog|
|234|EF_SPELLBREAKER|Spell Breaker|
|235|EF_DISPELL|Dispell|
|236|EF_DELUGE|Deluge Cast Aura|
|237|EF_VIOLENTGALE|Violent Gale Cast Aura|
|238|EF_LANDPROTECTOR|Magnetic Earth Cast Aura|
|239|EF_BOTTOM_VO|Volcano (Visual Effect)|
|240|EF_BOTTOM_DE|Deluge (Visual Effect)|
|241|EF_BOTTOM_VI|Violent Gale (Visual Effect)|
|242|EF_BOTTOM_LA|Magnetic Earth (Visual Effect)|
|243|EF_FASTMOVE|(Invalid)|
|244|EF_MAGICROD|Magic Rod|
|245|EF_HOLYCROSS|Holy Cross|
|246|EF_SHIELDCHARGE|Shield Charge|
|247|EF_MAPPILLAR2|Map Light Pillar Animation 2|
|248|EF_PROVIDENCE|Resistant Souls|
|249|EF_SHIELDBOOMERANG|Shield Boomerang|
|250|EF_SPEARQUICKEN|Spear Quicken|
|251|EF_DEVOTION|Devotion|
|252|EF_REFLECTSHIELD|Reflect Shield|
|253|EF_ABSORBSPIRITS|Absorb Spirit Spheres|
|254|EF_STEELBODY|Mental Strength (Visual Effect)|
|255|EF_FLAMELAUNCHER|Elemental Endow (Fire)|
|256|EF_FROSTWEAPON|Elemental Endow (Water)|
|257|EF_LIGHTNINGLOADER|Elemental Endow (Wind)|
|258|EF_SEISMICWEAPON|Elemental Endow (Earth)|
|259|EF_MAPPILLAR3|Map Light Pillar Animation 3|
|260|EF_MAPPILLAR4|Map Light Pillar Animation 4|
|261|EF_GUMGANG2|Fury Cast Animation|
|262|EF_TEIHIT1|Raging Quadruple Blow|
|263|EF_GUMGANG3|Raging Quadruple Blow 2|
|264|EF_TEIHIT2|(Nothing)|
|265|EF_TANJI|Throw Spirit Sphere|
|266|EF_TEIHIT1X|Raging Quadruple Blow 3|
|267|EF_CHIMTO|Occult Impaction|
|268|EF_STEALCOIN|Steal Coin|
|269|EF_STRIPWEAPON|Divest Weapon|
|270|EF_STRIPSHIELD|Divest Shield|
|271|EF_STRIPARMOR|Divest Armor|
|272|EF_STRIPHELM|Divest Helm|
|273|EF_CHAINCOMBO|Raging Quadruple Blow 4|
|274|EF_RG_COIN|Steal Coin Animation|
|275|EF_BACKSTAP|Back Stab Animation|
|276|EF_TEIHIT3|Raging Thrust|
|277|EF_BOTTOM_DISSONANCE|Dissoance Map Unit|
|278|EF_BOTTOM_LULLABY|Lullaby Map Unit|
|279|EF_BOTTOM_RICHMANKIM|Mr Kim a Rich Man Map Unit|
|280|EF_BOTTOM_ETERNALCHAOS|Eternal Chaos Map Unit|
|281|EF_BOTTOM_DRUMBATTLEFIELD|A Drum on the Battlefield Map Unit|
|282|EF_BOTTOM_RINGNIBELUNGEN|The Ring Of Nibelungen Map Unit|
|283|EF_BOTTOM_ROKISWEIL|Loki's Veil Map Unit|
|284|EF_BOTTOM_INTOABYSS|Into the Abyss Map Unit|
|285|EF_BOTTOM_SIEGFRIED|Invunerable Siegfriend Map Unit|
|286|EF_BOTTOM_WHISTLE|A Wistle Map Unit|
|287|EF_BOTTOM_ASSASSINCROSS|Assassin Cross of Sunset Map Unit|
|288|EF_BOTTOM_POEMBRAGI|A Poem of Bragi Map Unit|
|289|EF_BOTTOM_APPLEIDUN|The Apple Of Idun Map Unit|
|290|EF_BOTTOM_UGLYDANCE|Ugly Dance Map Unit|
|291|EF_BOTTOM_HUMMING|Humming Map Unit|
|292|EF_BOTTOM_DONTFORGETME|Please don't Forget Me Map Unit|
|293|EF_BOTTOM_FORTUNEKISS|Fortune's Kiss Map Unit|
|294|EF_BOTTOM_SERVICEFORYOU|Service For You Map Unit|
|295|EF_TALK_FROSTJOKE|Frost Joke|
|296|EF_TALK_SCREAM|Scream|
|297|EF_POKJUK|Fire Works (Visual Effect)|
|298|EF_THROWITEM|Acid Terror Animnation|
|299|EF_THROWITEM2|(Nothing)|
|300|EF_CHEMICALPROTECTION|Chemical Protection|
|301|EF_POKJUK_SOUND|Fire Works (Sound Effect)|
|302|EF_DEMONSTRATION|Bomb|
|303|EF_CHEMICAL2|(Unused)|
|304|EF_TELEPORTATION2|Teleportation Animation|
|305|EF_PHARMACY_OK|Pharmacy Success|
|306|EF_PHARMACY_FAIL|Pharmacy Failed|
|307|EF_FORESTLIGHT|Forest Light 1|
|308|EF_THROWITEM3|Throw Stone|
|309|EF_FIRSTAID|First Aid|
|310|EF_SPRINKLESAND|Sprinkle Sand|
|311|EF_LOUD|	Crazy Uproar|
|312|EF_HEAL|	Heal Effect|
|313|EF_HEAL2|Heal Effect 2|
|314|EF_EXIT2|Old Map Exit effect (Unused)|
|315|EF_GLASSWALL2|Safety Wall|
|316|EF_READYPORTAL2|Warp Portal Animation 1|
|317|EF_PORTAL2|Warp Portal Animation 2|
|318|EF_BOTTOM_MAG|Magnus Exorcisimus Map Unit|
|319|EF_BOTTOM_SANC|Sanctuary Map Unit|
|320|EF_HEAL3|Offensive Heal|
|321|EF_WARPZONE2|Warp NPC|
|322|EF_FORESTLIGHT2|Forest Light 2|
|323|EF_FORESTLIGHT3|Forest Light 3|
|324|EF_FORESTLIGHT4|Forest Light 4|
|325|EF_HEAL4|Heal Effect 4|
|326|EF_FOOT|	Chase Walk Left Foot|
|327|EF_FOOT2|Chse Walk Right Foot|
|328|EF_BEGINASURA|Monk Asura Strike|
|329|EF_TRIPLEATTACK|Triple Strike|
|330|EF_HITLINE|Combo Finish|
|331|EF_HPTIME|Natural HP Regeneration|
|332|EF_SPTIME|Natural SP Regeneration|
|333|EF_MAPLE|Autumn Leaves|
|334|EF_BLIND|Blind|
|335|EF_POISON|Poison|
|336|EF_GUARD|Kyrie Eleison/Parrying Shield|
|337|EF_JOBLVUP50|Class Change|
|338|EF_ANGEL2|Super Novice/Taekwon Level Up Angel|
|339|EF_MAGNUM2|Spiral Pierce|
|340|EF_CALLZONE|(Nothing)|
|341|EF_PORTAL3|Wedding Warp Portal|
|342|EF_COUPLECASTING|Wedding Skill|
|343|EF_HEARTCASTING|Another Merry Skill|
|344|EF_ENTRY2|Character map entry effect|
|345|EF_SAINTWING|Wings (Animated)|
|346|EF_SPHEREWIND|Like Moonlight But Blue|
|347|EF_COLORPAPER|Wedding Ceremony|
|348|EF_LIGHTSPHERE|Like 1000 Blade trepassing|
|349|EF_WATERFALL|Waterfall (Horizonatal)|
|350|EF_WATERFALL_90|Waterfall (Vertical)|
|351|EF_WATERFALL_SMALL|Small Waterfall (Horizonatal)|
|352|EF_WATERFALL_SMALL_90|Small Waterfall (Vertical)|
|353|EF_WATERFALL_T2|Dark Waterfall (Horizonatal)|
|354|EF_WATERFALL_T2_90|Dark Waterfall (Vertical)|
|355|EF_WATERFALL_SMALL_T2|Dark Small Waterfall (Horizonatal)|
|356|EF_WATERFALL_SMALL_T2_90|Dark Small Waterfall (Vertical)|
|357|EF_MINI_TETRIS|(Nothing)|
|358|EF_GHOST|Niflheim Ghost|
|359|EF_BAT|	Niflheim Bat Slow|
|360|EF_BAT2|	Niflheim Bat Fast|
|361|EF_SOULBREAKER|Soul Destroyer|
|362|EF_LEVEL99_4|Trancendant Level 99 Aura 1|
|363|EF_VALLENTINE|Valentine Day Heart With Wings|
|364|EF_VALLENTINE2|Valentine Day Heart|
|365|EF_PRESSURE|Gloria Domini|
|366|EF_BASH3D|Martyr's Reckoning|
|367|EF_AURABLADE|Aura Blade|
|368|EF_REDBODY|Berserk|
|369|EF_LKCONCENTRATION|Concentration|
|370|EF_BOTTOM_GOSPEL|Gospel Map Unit|
|371|EF_ANGEL|Level Up|
|372|EF_DEVIL|Death|
|373|EF_DRAGONSMOKE|House Smoke|
|374|EF_BOTTOM_BASILICA|Basilica|
|375|EF_ASSUMPTIO|Assumptio (Visual Effect)|
|376|EF_HITLINE2|Palm Strike|
|377|EF_BASH3D2|Matyr's Reckoning 2|
|378|EF_ENERGYDRAIN2|Soul Drain (1st Part)|
|379|EF_TRANSBLUEBODY|Soul Drain (2nd Part)|
|380|EF_MAGICCRASHER|Magic Crasher|
|381|EF_LIGHTSPHERE2|Blue Starburst (Unknown use)|
|382|EF_LIGHTBLADE|(Nothing)|
|383|EF_ENERGYDRAIN3|Health Conversion|
|384|EF_LINELINK2|Soul Change (Sound Effect)|
|385|EF_LINKLIGHT|Soul Change (Visual Effect)|
|386|EF_TRUESIGHT|True Sight|
|387|EF_FALCONASSAULT|Falcon Assault|
|388|EF_TRIPLEATTACK2|Focused Arrow Strike (Sound Effect)|
|389|EF_PORTAL4|Wind Walk|
|390|EF_MELTDOWN|Shattering Strike|
|391|EF_CARTBOOST|Cart Boost|
|392|EF_REJECTSWORD|Reject Sword|
|393|EF_TRIPLEATTACK3|Arrow Vulcan|
|394|EF_SPHEREWIND2|Sheltering Bliss|
|395|EF_LINELINK3|Marionette Control (Sound Effect)|
|396|EF_PINKBODY|Marionette Control (Visual Effect)|
|397|EF_LEVEL99_5|Trancended 99 Aura (Middle)|
|398|EF_LEVEL99_6|Trancended 99 Aura (Bottom)|
|399|EF_BASH3D3|Head Crush|
|400|EF_BASH3D4|Joint Beat|
|401|EF_NAPALMVALCAN|Napalm Vulcan Sound|
|402|EF_PORTAL5|Dangerous Soul Collect|
|403|EF_MAGICCRASHER2|Mind Breaker|
|404|EF_BOTTOM_SPIDER|Fiber Lock|
|405|EF_BOTTOM_FOGWALL|Wall Of Fog|
|406|EF_SOULBURN|Soul Burn|
|407|EF_SOULCHANGE|Soul Change|
|408|EF_BABY|	Mom, Dad, I love you! (Baby Skill)|
|409|EF_SOULBREAKER2|Meteor Assault|
|410|EF_RAINBOW|Rainbow|
|411|EF_PEONG|Leap|
|412|EF_TANJI2|Like Throw Spirit Sphere|
|413|EF_PRESSEDBODY|Axe Kick|
|414|EF_SPINEDBODY|Round Kick|
|415|EF_KICKEDBODY|Counter Kick|
|416|EF_AIRTEXTURE|(Nothing)|
|417|EF_HITBODY|Flash|
|418|EF_DOUBLEGUMGANG|Warmth Lightning|
|419|EF_REFLECTBODY|Kaite (Visual Effect)|
|420|EF_BABYBODY|Eswoo (Small) (Visual Effect)|
|421|EF_BABYBODY2|Eswoo (Alt. Small) (Visual Effect)|
|422|EF_GIANTBODY|Eswoo (Normal) (Visual Effect)|
|423|EF_GIANTBODY2|Eswoo (Alt. Normal) (Visual Effect)|
|424|EF_ASURABODY|Spirit Link (Visual Effect)|
|425|EF_4WAYBODY|Esma Hit (Visual Effect)|
|426|EF_QUAKEBODY|Sprint Collision (Visual Effect)|
|427|EF_ASURABODY_MONSTER|(Nothing)|
|428|EF_HITLINE3|(Nothing)|
|429|EF_HITLINE4|Taekwon Kick Hit 1|
|430|EF_HITLINE5|Taekwon Kick Hit 2|
|431|EF_HITLINE6|Taekwon Kick Hit 3|
|432|EF_ELECTRIC|Solar, Lunar and Stellar Perception (Visual Effect)|
|433|EF_ELECTRIC2|Solar, Lunar and Stellar Opposition (Visual Effect)|
|434|EF_STORMKICK|Taekwon Kick Hit 4|
|435|EF_HITLINE7|Whirlwind Kick|
|436|EF_STORMKICK|White Barrier (Unused)|
|437|EF_HALFSPHERE|White barrier 2 (Unused)|
|438|EF_ATTACKENERGY|Kaite Reflect Animation|
|439|EF_ATTACKENERGY2|Flying Side Kick|
|440|EF_ASSUMPTIO2|Assumptio (Animation)|
|441|EF_BLUECASTING|Comfort Skills Cast Aura|
|442|EF_RUN|Foot Prints caused by Sprint.|
|443|EF_STOPRUN|(Nothing)|
|444|EF_STOPEFFECT|Sprint Stop Animation|
|445|EF_JUMPBODY|High Jump (Jump)|
|446|EF_LANDBODY|High Jump (Return Down)|
|447|EF_FOOT3|Running Left Foot|
|448|EF_FOOT4|Running Right Foot|
|449|EF_TAE_READY|KA-Spell (1st Part)|
|450|EF_GRANDCROSS2|Darkcross|
|451|EF_SOULSTRIKE2|Dark Strike|
|452|EF_YUFITEL2|Something Like Jupitel Thunder|
|453|EF_NPC_STOP|Paralized|
|454|EF_DARKCASTING|Like Blind|
|455|EF_GUMGANGNPC|Another Warmth Lightning|
|456|EF_AGIUP|Power Up|
|457|EF_JUMPKICK|Flying Side Kick (2nd Part)|
|458|EF_QUAKEBODY2|Running/Sprint (running into a wall)|
|459|EF_STORMKICK1|Brown tornado that spins sprite (unused)|
|460|EF_STORMKICK2|Green tornado (unused)|
|461|EF_STORMKICK3|Blue tornado (unused)|
|462|EF_STORMKICK4|Kaupe Dodge Effect|
|463|EF_STORMKICK5|Kaupe Dodge Effect|
|464|EF_STORMKICK6|White tornado (unused)|
|465|EF_STORMKICK7|Purple tornado (unused)|
|466|EF_SPINEDBODY2|Another Round Kick|
|467|EF_BEGINASURA1|Warm/Mild Wind (Earth)|
|468|EF_BEGINASURA2|Warm/Mild Wind (Wind)|
|469|EF_BEGINASURA3|Warm/Mild Wind (Water)|
|470|EF_BEGINASURA4|Warm/Mild Wind (Fire)|
|471|EF_BEGINASURA5|Warm/Mild Wind (Undead)|
|472|EF_BEGINASURA6|Warm/Mild Wind (Shadow)|
|473|EF_BEGINASURA7|Warm/Mild Wind (Holy)|
|474|EF_AURABLADE2|(Nothing)|
|475|EF_DEVIL1|Demon of The Sun Moon And Stars (Level 1)|
|476|EF_DEVIL2|Demon of The Sun Moon And Stars (Level 2)|
|477|EF_DEVIL3|Demon of The Sun Moon And Stars (Level 3)|
|478|EF_DEVIL4|Demon of The Sun Moon And Stars (Level 4)|
|479|EF_DEVIL5|Demon of The Sun Moon And Stars (Level 5)|
|480|EF_DEVIL6|Demon of The Sun Moon And Stars (Level 6)|
|481|EF_DEVIL7|Demon of The Sun Moon And Stars (Level 7)|
|482|EF_DEVIL8|Demon of The Sun Moon And Stars (Level 8)|
|483|EF_DEVIL9|Demon of The Sun Moon And Stars (Level 9)|
|484|EF_DEVIL10|Demon of The Sun Moon And Stars (Level 10)|
|485|EF_DOUBLEGUMGANG2|Mental Strength Lightning but White|
|486|EF_DOUBLEGUMGANG3|Mental Strength Lightning|
|487|EF_BLACKDEVIL|Demon of The Sun Moon And Stars Ground Effect|
|488|EF_FLOWERCAST|Comfort Skills|
|489|EF_FLOWERCAST2|(Nothing)|
|490|EF_FLOWERCAST3|(Nothing)|
|491|EF_MOCHI|Element Potions|
|492|EF_LAMADAN|Cooking Foods|
|493|EF_EDP|	Enchant Deadly Poison|
|494|EF_SHIELDBOOMERANG2|Throwing Tomahawk|
|495|EF_RG_COIN2|Full Strip Sound|
|496|EF_GUARD2|Preserve|
|497|EF_SLIM|	Twilight Alchemy 1|
|498|EF_SLIM2|Twilight Alchemy 2|
|499|EF_SLIM3|Twilight Alchemy 3|
|500|EF_CHEMICALBODY|Player Become Blue with Blue Aura|
|501|EF_CASTSPIN|Chase Walk Animation|
|502|EF_PIERCEBODY|Player Become Yellow with Yellow Aura|
|503|EF_SOULLINK|Soul Link Word|
|504|EF_CHOOKGI2|(Nothing)|
|505|EF_MEMORIZE|Memorize|
|506|EF_SOULLIGHT|(Nothing)|
|507|EF_MAPAE|Authoritative Badge|
|508|EF_ITEMPOKJUK|Fire Cracker|
|509|EF_05VAL|Valentine Day Hearth (Wings)|
|510|EF_BEGINASURA11|Champion Asura Strike|
|511|EF_NIGHT|(Nothing)|
|512|EF_CHEMICAL2DASH|Chain Crush Combo|
|513|EF_GROUNDSAMPLE|Area Cast|
|514|EF_GI_EXPLOSION|Really Big Circle|
|515|EF_CLOUD4|Einbroch Fog|
|516|EF_CLOUD5|Airship Cloud|
|517|EF_BOTTOM_HERMODE|(Nothing)|
|518|EF_CARTTER|Cart Termination|
|519|EF_ITEMFAST|Speed Down Potion|
|520|EF_SHIELDBOOMERANG3|Shield Bumerang|
|521|EF_DOUBLECASTBODY|Player Become Red with Red Aura|
|522|EF_GRAVITATION|Gravitation Field|
|523|EF_TAROTCARD1|Tarot Card of Fate (The Fool)|
|524|EF_TAROTCARD2|Tarot Card of Fate (The Magician)|
|525|EF_TAROTCARD3|Tarot Card of Fate (The High Priestess)|
|526|EF_TAROTCARD4|Tarot Card of Fate (The Chariot)|
|527|EF_TAROTCARD5|Tarot Card of Fate (Strength)|
|528|EF_TAROTCARD6|Tarot Card of Fate (The Lovers)|
|529|EF_TAROTCARD7|Tarot Card of Fate (The Wheel of Fortune)|
|530|EF_TAROTCARD8|Tarot Card of Fate (The Hanged Man)|
|531|EF_TAROTCARD9|Tarot Card of Fate (Death)|
|532|EF_TAROTCARD10|Tarot Card of Fate (Temperance)|
|533|EF_TAROTCARD11|Tarot Card of Fate (The Devil)|
|534|EF_TAROTCARD12|Tarot Card of Fate (The Tower)|
|535|EF_TAROTCARD13|Tarot Card of Fate (The Star)|
|536|EF_TAROTCARD14|Tarot Card of Fate (The Sun)|
|537|EF_ACIDDEMON|Acid Demonstration|
|538|EF_GREENBODY|Player Become Green with Green Aura|
|539|EF_THROWITEM4|Throw Random Bottle|
|540|EF_BABYBODY_BACK|Instant Small->Normal|
|541|EF_THROWITEM5|(Nothing)|
|542|EF_BLUEBODY|KA-Spell (1st Part)|
|543|EF_HATED|Kahii|
|544|EF_REDLIGHTBODY|Warmth Red Sprite|
|545|EF_RO2YEAR|Sound And... PUFF Client Crash :P|
|546|EF_SMA_READY|Kaupe|
|547|EF_STIN|	Estin|
|548|EF_RED_HIT|Instant Red Sprite|
|549|EF_BLUE_HIT|Instant Blue Sprite|
|550|EF_QUAKEBODY3|Another Effect like Running Hit|
|551|EF_SMA	|EFfect Like Estun but with Circle|
|552|EF_SMA2|	(Nothing)|
|553|EF_STIN2|Esma|
|554|EF_HITTEXTURE|Large White Cloud|
|555|EF_STIN3|Estun|
|556|EF_SMA3|	(Nothing)|
|557|EF_BLUEFALL|Juperos Energy Waterfall (Horizontal)|
|558|EF_BLUEFALL_90|Juperos Energy Waterfall (Vertical)|
|559|EF_FASTBLUEFALL|Juperos Energy Waterfall Fast (Horizontal)|
|560|EF_FASTBLUEFALL_90|Juperos Energy Waterfall Fast (Vertical)|
|561|EF_BIG_PORTAL|Juperos Warp|
|562|EF_BIG_PORTAL2|Juperos Warp|
|563|EF_SCREEN_QUAKE|Earthquake Effect (Juperos Elevator)|
|564|EF_HOMUNCASTING|Wedding Cast|
|565|EF_HFLIMOON1|Filir Moonlight Lvl 1|
|566|EF_HFLIMOON2|Filir Moonlight Lvl 2|
|567|EF_HFLIMOON3|Filir Moonlight Lvl 3|
|568|EF_HO_UP|Another Job Level Up|
|569|EF_HAMIDEFENCE|Amistr Bulwark|
|570|EF_HAMICASTLE|Amistr Castling|
|571|EF_HAMIBLOOD|Amistr Bloodlust|
|572|EF_HATED2|Warmth Soul|
|573|EF_TWILIGHT1|Twilight Alchemy 1|
|574|EF_TWILIGHT2|Twilight Alchemy 2|
|575|EF_TWILIGHT3|Twilight Alchemy 3|
|576|EF_ITEM_THUNDER|Box Effect (Thunder)|
|577|EF_ITEM_CLOUD|Box Effect (Cloud)|
|578|EF_ITEM_CURSE|Box Effect (Curse)|
|579|EF_ITEM_ZZZ|Box Effect (Sleep)|
|580|EF_ITEM_RAIN|Box Effect (Rain)|
|581|EF_ITEM_LIGHT|Box Effect (Sunlight)|
|582|EF_ANGEL3|Another Super Novice/Taekwon Angel|
|583|EF_M01|	Warmth Hit|
|584|EF_M02|	Full Buster|
|585|EF_M03|	5 Medium Size Explosion|
|586|EF_M04|	Somatology Lab Mobs Aura|
|587|EF_M05|	Big Purple Flame|
|588|EF_M06|	Little Red Flame|
|589|EF_M07|	Eswoo|
|590|EF_KAIZEL|Running Stop|
|591|EF_KAAHI|(Nothing)|
|592|EF_CLOUD6|Thanatos Tower Bloody Clouds|
|593|EF_FOOD01|Food Effect (STR)|
|594|EF_FOOD02|Food Effect (INT)|
|595|EF_FOOD03|Food Effect (VIT)|
|596|EF_FOOD04|Food Effect (AGI)|
|597|EF_FOOD05|Food Effect (DEX)|
|598|EF_FOOD06|Food Effect (LUK)|
|599|EF_SHRINK|Cast Time Sound and Flashing Animation on Player|
|600|EF_THROWITEM6|Throw Venom Knife|
|601|EF_SIGHT2|Sight Blaster|
|602|EF_QUAKEBODY4|Close Confine (Grab Effect)|
|603|EF_FIREHIT2|Spinning fire ball (like 50, but smaller)|
|604|EF_NPC_STOP2|Close Confine (Ground Effect)|
|605|EF_NPC_STOP2_DEL|(Nothing)|
|606|EF_FVOICE|Pang Voice (Visual Effect)|
|607|EF_WINK|Wink of Charm (Visual Effect)|
|608|EF_COOKING_OK|Cooking Success|
|609|EF_COOKING_FAIL|Cooking Failed|
|610|EF_TEMP_OK|Success|
|611|EF_TEMP_FAIL|Failed|
|612|EF_HAPGYEOK|Korean Words and /no1 Emoticon|
|613|EF_THROWITEM7|Throw Shuriken|
|614|EF_THROWITEM8|Throw Kunai|
|615|EF_THROWITEM9|Throw Fumma Shuriken|
|616|EF_THROWITEM10|Throw Money|
|617|EF_BUNSINJYUTSU|Illusionary Shadow|
|618|EF_KOUENKA|Crimson Fire Bolossom|
|619|EF_HYOUSENSOU|Lightning Spear Of Ice|
|620|EF_BOTTOM_SUITON|Water Escape Technique|
|621|EF_STIN4|Wind Blade|
|622|EF_THUNDERSTORM2|Lightning Crash|
|623|EF_CHEMICAL4|Piercing Shot|
|624|EF_STIN5|Kamaitachi|
|625|EF_MADNESS_BLUE|Madness Canceller|
|626|EF_MADNESS_RED|Adjustment|
|627|EF_RG_COIN3|Disarm (Sound Effect)|
|628|EF_BASH3D5|Dust|
|629|EF_CHOOKGI3|(Nothing)|
|630|EF_KIRIKAGE|Shadow Slash|
|631|EF_TATAMI|Reverse Tatami Map Unit|
|632|EF_KASUMIKIRI|Mist Slash|
|633|EF_ISSEN|Final Strike|
|634|EF_KAEN|	Crimson Fire Formation|
|635|EF_BAKU|	Dragon Fire Formation|
|636|EF_HYOUSYOURAKU|Falling Ice Pillar|
|637|EF_DESPERADO|Desperado|
|638|EF_LIGHTNING_S|Ground Drift Grenade|
|639|EF_BLIND_S|Ground Drift Grenade|
|640|EF_POISON_S|Ground Drift Grenade|
|641|EF_FREEZING_S|Ground Drift Grenade|
|642|EF_FLARE_S|Ground Drift Grenade|
|643|EF_RAPIDSHOWER|Rapid Shower|
|644|EF_MAGICALBULLET|Magic Bullet|
|645|EF_SPREADATTACK|Spread Attack|
|646|EF_TRACKCASTING|Tracking (Shown While Casting)|
|647|EF_TRACKING|Tracking|
|648|EF_TRIPLEACTION|Triple Action|
|649|EF_BULLSEYE|Bull's Eye|
|650|EF_MAP_MAGICZONE|Ice Cave Level 4 Circle|
|651|EF_MAP_MAGICZONE2|Ice Cave Level 4 Big Circle|
|652|EF_DAMAGE1|Like Regeneration Number but Red with a Sound|
|653|EF_DAMAGE1_2|Like Regeneration Number but Red|
|654|EF_DAMAGE1_3|Like Regeneration Number but Purple|
|655|EF_UNDEADBODY|Mobs Skill (Change Undead Element)|
|656|EF_UNDEADBODY_DEL|Last animation before Change Undead Element finish|
|657|EF_GREEN_NUMBER|(Nothing)|
|658|EF_BLUE_NUMBER|(Nothing)|
|659|EF_RED_NUMBER|(Nothing)|
|660|EF_PURPLE_NUMBER|(Nothing)|
|661|EF_BLACK_NUMBER|(Nothing)|
|662|EF_WHITE_NUMBER|(Nothing)|
|663|EF_YELLOW_NUMBER|(Nothing)|
|664|EF_PINK_NUMBER|(Nothing)|
|665|EF_BUBBLE_DROP|Little Blue Ball Falling From the Sky|
|666|EF_NPC_EARTHQUAKE|Earthquake|
|667|EF_DA_SPACE|(Nothing)|
|668|EF_DRAGONFEAR|Dragonfear|
|669|EF_BLEEDING|Wide Bleeding|
|670|EF_WIDECONFUSE|Dragon fear (Visual Effect)|
|671|EF_BOTTOM_RUNNER|The Japan Earth Symbol (like 'Seven Wind Lv1', but on the ground)|
|672|EF_BOTTOM_TRANSFER|The Japan Wind Symbol (like 'Seven Wind Lv2', but on the ground)|
|673|EF_CRYSTAL_BLUE|Map turns Blue (like Soul Link)|
|674|EF_BOTTOM_EVILLAND|Evil Land Cell|
|675|EF_GUARD3|Like Parrying/Kyrie Eleison barrier but Yellow with small Cross in every barrier piece|
|676|EF_NPC_SLOWCAST|Slow Casting|
|677|EF_CRITICALWOUND|Critical Wounds/Bleeding Attack|
|678|EF_GREEN99_3|White 99 Aura Bubbles|
|679|EF_GREEN99_5|Green Aura (Middle)|
|680|EF_GREEN99_6|Green Aura (Bottom)|
|681|EF_MAPSPHERE|Dimensional Gorge Map Effect|
|682|EF_POK_LOVE|I Love You Banner|
|683|EF_POK_WHITE|Happy White Day Banner|
|684|EF_POK_VALEN|Happy Valentine Day Banner|
|685|EF_POK_BIRTH|Happy Birthday Banner|
|686|EF_POK_CHRISTMAS|Merry Christmas Banner|
|687|EF_MAP_MAGICZONE3|Cast Circle-Like effect 1|
|688|EF_MAP_MAGICZONE4|Cast Circle-Like effect 2|
|689|EF_DUST|Endless Tower Map Effect|
|690|EF_TORCH_RED|Burning Flame (Red)|
|691|EF_TORCH_GREEN|Burning Flame (Green)|
|692|EF_MAP_GHOST|Unknown Aura Bubbles (Small ghosts)|
|693|EF_GLOW1|Translucent yellow circle|
|694|EF_GLOW2|Translucent green circle|
|695|EF_GLOW4|Rotating green light|
|696|EF_TORCH_PURPLE|The same of 690 and 691 but Blue/Purple|
|697|EF_CLOUD7|(Nothing)|
|698|EF_CLOUD8|(Nothing)|
|699|EF_FLOWERLEAF|Fall of powder from the sky and raise of some leaf|
|700|EF_MAPSPHERE2|Big Colored Green Sphere.|
|701|EF_GLOW11|Huge Blue Sphere|
|702|EF_GLOW12|Little Colored Violet Sphere|
|703|EF_CIRCLELIGHT|Light Infiltration with fall of pownder|
|704|EF_ITEM315|Client Error (mobile_ef02.str)|
|705|EF_ITEM316|Client Error (mobile_ef01.str)|
|706|EF_ITEM317|Client Error (mobile_ef03.str)|
|707|EF_ITEM318|Client Crash :P|
|708|EF_STORM_MIN|Storm Gust (same as 89)|
|709|EF_POK_JAP|A Firework that split in 4 mini fireworks|
|710|EF_MAP_GREENLIGHT|A Sphere like Effect 701 but Green, and a bit more larger|
|711|EF_MAP_MAGICWALL|A big violet wall|
|712|EF_MAP_GREENLIGHT2|A Little Flame Sphere|
|713|EF_YELLOWFLY1|A lot of Very Small and Yellow Sphere|
|714|EF_YELLOWFLY2|(Nothing)|
|715|EF_BOTTOM_BLUE|Little blue Basilica|
|716|EF_BOTTOM_BLUE2|Same as 715|
|717|EF_WEWISH|Christmas Carol (copy of Angelus)|
|718|EF_FIREPILLARON2|Judex (Visual Effect)|
|719|EF_FORESTLIGHT5|Renovatio (light beam)|
|720|EF_SOULBREAKER3|Yellow version of Soul Breaker|
|721|EF_ADO_STR|Adoramus (lightning bolt)|
|722|EF_IGN_STR|Ignition Break (big explosion)|
|723|EF_CHIMTO2|Hundred Spear (sound effect)|
|724|EF_WINDCUTTER|Green version of Detecting|
|725|EF_DETECT2|Oratorio (like Detecting)|
|726|EF_FROSTMYSTY|Frost Misty (blue vapor and bubbles)|
|727|EF_CRIMSON_STR|Crimson Rock|
|728|EF_HELL_STR|Small fire (part of Hell Inferno)|
|729|EF_SPR_MASH|Marsh of Abyss (like Close Confine)|
|730|EF_SPR_SOULE|Small, cartoony explosion (part of Soul Expansion)|
|731|EF_DHOWL_STR|Dragon Howling (blinking, expanding circle)|
|732|EF_EARTHWALL|Spike from the ground|
|733|EF_SOULBREAKER4|Fluffy Ball flying by|
|734|EF_CHAINL_STR|Chain Lightning|
|735|EF_CHOOKGI_FIRE|(Nothing)|
|736|EF_CHOOKGI_WIND|(Nothing)|
|737|EF_CHOOKGI_WATER|(Nothing)|
|738|EF_CHOOKGI_GROUND|(Nothing)|
|739|EF_MAGENTA_TRAP|Old Magenta Trap|
|740|EF_COBALT_TRAP|Old Cobald Trap|
|741|EF_MAIZE_TRAP|Old Maize Trap|
|742|EF_VERDURE_TRAP|Old Verdure Trap|
|743|EF_NORMAL_TRAP|White Ranger Trap|
|744|EF_CLOAKING2|Camouflage|
|745|EF_AIMED_STR|Aimed Bolt (crosshairs)|
|746|EF_ARROWSTORM_STR|Arrow Storm|
|747|EF_LAULAMUS_STR|Falling white feathers|
|748|EF_LAUAGNUS_STR|Falling blue feathers|
|749|EF_MILSHIELD_STR|Millennium Shield|
|750|EF_CONCENTRATION2|Detonator (blue sparkles)|
|751|EF_FIREBALL2|Releasing summoned warlock spheres|
|752|EF_BUNSINJYUTSU2|Like Energy Coat, but not as dark|
|753|EF_CLEARTIME|Clearance|
|754|EF_GLASSWALL3|Green warp portal (root of Epiclesis)|
|755|EF_ORATIO|Oratio (spinning blue symbol)|
|756|EF_POTION_BERSERK2|Enchant Blade (like Berserk Potion)|
|757|EF_CIRCLEPOWER|Third Class Aura (Middle)|
|758|EF_ROLLING1|Rolling Cutter - Spin Count 1|
|759|EF_ROLLING2|Rolling Cutter - Spin Count 2|
|760|EF_ROLLING3|Rolling Cutter - Spin Count 3|
|761|EF_ROLLING4|Rolling Cutter - Spin Count 4|
|762|EF_ROLLING5|Rolling Cutter - Spin Count 5|
|763|EF_ROLLING6|Rolling Cutter - Spin Count 6|
|764|EF_ROLLING7|Rolling Cutter - Spin Count 7|
|765|EF_ROLLING8|Rolling Cutter - Spin Count 8|
|766|EF_ROLLING9|Rolling Cutter - Spin Count 9|
|767|EF_ROLLING10|Rolling Cutter - Spin Count 10|
|768|EF_PURPLEBODY|Blinking|
|769|EF_STIN6|Cross Ripper Slasher (flying knives)|
|770|EF_RG_COIN4|Strip sound|
|771|EF_POISONWAV|Poison sound|
|772|EF_POISONSMOKE|Poison particles|
|773|EF_GUMGANG4|Expanding purple aura (part of Phantom Menace)|
|774|EF_SHIELDBOOMERANG4|Axe Boomerang|
|775|EF_CASTSPIN2|Spinning character sprite|
|776|EF_VULCANWAV|Like Desperado sound effect|
|777|EF_AGIUP2|Faded light from the ground [S]|
|778|EF_DETECT3|Expanding white aura (like Clearance)|
|779|EF_AGIUP3|Faded light from the ground [S]|
|780|EF_DETECT4|Expanding red aura (from Infrared Scan)|
|781|EF_ELECTRIC3|Magnetic Field (purple chains)|
|782|EF_GUARD4|All-around shield [S]|
|783|EF_BOTTOM_BARRIER|Yellow shaft of light|
|784|EF_BOTTOM_STEALTH|White shaft of light|
|785|EF_REPAIRTIME|Upward flying wrenches|
|786|EF_NC_ANAL|Symbol with bleeping sound [S]|
|787|EF_FIRETHROW|Flare Launcher (line of fire)|
|788|EF_VENOMIMPRESS|Venom Impress (green skull)|
|789|EF_FROSTMISTY|Freezing Status Effect (two ancillas)|
|790|EF_BURNING|Burning Status Effect (flame symbol)|
|791|EF_COLDTHROW|Two ice shots|
|792|EF_MAKEHALLU|Upward streaming white particles|
|793|EF_HALLUTIME|Same, but more brief|
|794|EF_INFRAREDSCAN|Infrared Scan (red lasers)|
|795|EF_CRASHAXE|Power Swing (axe crash)|
|796|EF_GTHUNDER|Spinning blue triangles|
|797|EF_STONERING|Stapo|
|798|EF_INTIMIDATE2|Red triangles (like Intimidate)|
|799|EF_STASIS|Stasis (expanding blue mist) [S]|
|800|EF_REDLINE|Hell Inferno (red lights)|
|801|EF_FROSTDIVER3|Jack Frost unit (ice spikes)|
|802|EF_BOTTOM_BASILICA2|White Imprison|
|803|EF_RECOGNIZED|Recognized Spell|
|804|EF_TETRA|Tetra Vortex [S]|
|805|EF_TETRACASTING|Tetra Vortex cast animation (blinking colors)|
|806|EF_FIREBALL3|Flying by as fast as a rocket|
|807|EF_INTIMIDATE3|Kidnapping sound|
|808|EF_RECOGNIZED2|Like Recognized Spell, but one symbol|
|809|EF_CLOAKING3|Shadowy filter [S]|
|810|EF_INTIMIDATE4|Damp thud sound [S]|
|811|EF_STRETCH|Body Painting|
|812|EF_BLACKBODY|Black expanding aura|
|813|EF_ENERVATION|Masquerade - Enervation|
|814|EF_ENERVATION2|Masquerade - Groomy|
|815|EF_ENERVATION3|Masquerade - Ignorance|
|816|EF_ENERVATION4|Masquerade - Laziness|
|817|EF_ENERVATION5|Masquerade - Unlucky|
|818|EF_ENERVATION6|Masquerade - Weakness|
|819|EF_LINELINK4|(Nothing)|
|820|EF_RG_COIN5|Strip Accessory|
|821|EF_WATERFALL_ANI|Waterfall|
|822|EF_BOTTOM_MANHOLE|Dimension Door (spinning blue aura)|
|823|EF_MANHOLE|In-the-manhole effect|
|824|EF_MAKEFEINT|Some filter|
|825|EF_FORESTLIGHT6|Dimension Door (aura + blue light)|
|826|EF_DARKCASTING2|Expanding black casting anim.|
|827|EF_BOTTOM_ANI|Chaos Panic (spinning brown aura)|
|828|EF_BOTTOM_MAELSTROM|Maelstrom (spinning pink aura)|
|829|EF_BOTTOM_BLOODYLUST|Bloody Lust (spinning red aura)|
|830|EF_BEGINSPELL_N1|Blue aura (Arch Bishop cast animation)|
|831|EF_BEGINSPELL_N2|Blue cone [S]|
|832|EF_HEAL_N|Sonic Wave|
|833|EF_CHOOKGI_N|(Nothing)|
|834|EF_JOBLVUP50_2|Light shooting away circlish|
|835|EF_CHEMICAL2DASH2|Fastness yellow-reddish|
|836|EF_CHEMICAL2DASH3|Fastness yellow-pinkish|
|837|EF_ROLLINGCAST|Casting [S]|
|838|EF_WATER_BELOW|Watery aura|
|839|EF_WATER_FADE|[Client Error]|
|840|EF_BEGINSPELL_N3|Red cone|
|841|EF_BEGINSPELL_N4|Green cone|
|842|EF_BEGINSPELL_N5|Yellow cone|
|843|EF_BEGINSPELL_N6|White cone|
|844|EF_BEGINSPELL_N7|Purple cone|
|845|EF_BEGINSPELL_N8|light-bluish turquoise cone|
|846|EF_WATER_SMOKE|(Nothing)|
|847|EF_DANCE1|Gloomy Day (white/red light rays)|
|848|EF_DANCE2|Gloomy Day (white/blue light rays)|
|849|EF_LINKPARTICLE|(Nothing)|
|850|EF_SOULLIGHT2|(Nothing)|
|851|EF_SPR_PARTICLE|Green mushy-foggy stuff (dull)|
|852|EF_SPR_PARTICLE2|Green mushy-foggy stuff (bright)|
|853|EF_SPR_PLANT|Bright green flower area|
|854|EF_CHEMICAL_V|Blue beam of light with notes|
|855|EF_SHOOTPARTICLE|(Nothing)|
|856|EF_BOT_REVERB|Reverberation (red eighth notes)|
|857|EF_RAIN_PARTICLE|Severe Rainstorm (falling red and blue beams)|
|858|EF_CHEMICAL_V2|Deep Sleep Lullaby (two red beams and music notes)|
|859|EF_SECRA|Holograph of text (blue)|
|860|EF_BOT_REVERB2|Distorted note (blue)|
|861|EF_CIRCLEPOWER2|Green aura (from Circle of Life's Melody)|
|862|EF_SECRA2|Randomize Spell (holograph of text)|
|863|EF_CHEMICAL_V3|Dominion Impulse (two spears of light)|
|864|EF_ENERVATION7|Gloomy Day (colorful lines)|
|865|EF_CIRCLEPOWER3|Blue aura (from Song of Mana)|
|866|EF_SPR_PLANT2|Dance with a Warg (Wargs)|
|867|EF_CIRCLEPOWER4|Yellow aura (from Dance with a Warg)|
|868|EF_SPR_PLANT3|Song of Mana (Violies)|
|869|EF_RG_COIN6|Strip sound [S]|
|870|EF_SPR_PLANT4|Ghostly Succubuses of fire|
|871|EF_CIRCLEPOWER5|Red aura (from Lerad's Dew)|
|872|EF_SPR_PLANT5|Lerad's Dew (Minerals)|
|873|EF_CIRCLEPOWER6|Stargate-wormhole stuff (bright purple)|
|874|EF_SPR_PLANT6|Melody of Sink (Ktullanuxes)|
|875|EF_CIRCLEPOWER7|Stargate-wormhole stuff (bright turquoise)|
|876|EF_SPR_PLANT7|Warcry of Beyond (Garms)|
|877|EF_CIRCLEPOWER8|Stargate-wormhole stuff (white)|
|878|EF_SPR_PLANT8|Unlimited Humming Voice (Miyabi Ningyos)|
|879|EF_HEARTASURA|Siren's Voice (heart-like)|
|880|EF_BEGINSPELL_150|Bluish castish cone|
|881|EF_LEVEL99_150|Blue aura|
|882|EF_PRIMECHARGE|Whirl of fireflies (red)|
|883|EF_GLASSWALL4|Epiclesis (transparent green tree)|
|884|EF_GRADIUS_LASER|Green beam|
|885|EF_BASH3D6|Blue light beams|
|886|EF_GUMGANG5|Blue castish cone|
|887|EF_HITLINE8|Wavy sparks|
|888|EF_ELECTRIC4|Earth Shaker (same as 432)|
|889|EF_TEIHIT1T|Fast light beams|
|890|EF_SPINMOVE|Rotation|
|891|EF_FIREBALL4|Magic shots [S]|
|892|EF_TRIPLEATTACK4|Fastness with hitting sound[S]|
|893|EF_CHEMICAL3S|Blue-white light passing by|
|894|EF_GROUNDSHAKE|(Nothing)|
|895|EF_DQ9_CHARGE|Big wheel of flat light beams|
|896|EF_DQ9_CHARGE2|Still sun shaped lightning aura|
|897|EF_DQ9_CHARGE3|Animated sun shaped lightning aura|
|898|EF_DQ9_CHARGE4|Animated, curvy sun shaped lightning aura|
|899|EF_BLUELINE|White/red light shots from below|
|900|EF_SELFSCROLL|Animated, slow curvy sun shaped lightning aura|
|901|EF_SPR_LIGHTPRINT|Explosion|
|902|EF_PNG_TEST|Floating bedtable texture|
|903|EF_BEGINSPELL_YB|	Castish flamey cone|
|904|EF_CHEMICAL2DASH4|	Yellow/pink lights passing by|
|905|EF_GROUNDSHAKE2|Expanding circle|
|906|EF_PRESSURE2|Shield Press (falling shield)|
|907|EF_RG_COIN7|Chainy, metalish sound [S]|
|908|EF_PRIMECHARGE2|Prestige (sphere of yellow particles)|
|909|EF_PRIMECHARGE3|Banding (sphere of red particles)|
|910|EF_PRIMECHARGE4|Inspiration (sphere of blue particles)|
|911|EF_GREENCASTING|Green castish animation [S]|
|912|EF_WALLOFTHORN|Wall of Thorns unit (green fog cloud)|
|913|EF_FIREBALL5|Magic projectiles|
|914|EF_THROWITEM11|(Nothing)|
|915|EF_SPR_PLANT9|Crazy Weed|
|916|EF_DEMONICFIRE|Demonic Fire|
|917|EF_DEMONICFIRE2|More angry, demonic flames|
|918|EF_DEMONICFIRE3|Fire Insignia (demonic flames)|
|919|EF_HELLSPLANT|Hell's Plant (green snapping plant)|
|920|EF_FIREWALL2|Fire Walk unit|
|921|EF_VACUUM|Vacuum Extreme (whirlwind)|
|922|EF_SPR_PLANT10|Psychic Wave|
|923|EF_SPR_LIGHTPRINT2|Poison Buster|
|924|EF_POISONSMOKE2|Poisoning animation|
|925|EF_MAKEHALLU2|Some filter|
|926|EF_SHOCKWAVE2|Electric Walk unit|
|927|EF_SPR_PLANT11|Earth Grave (speary roots)|
|928|EF_COLDTHROW2|Ice cloud projectiles|
|929|EF_DEMONICFIRE4|Warmer (field of flames)|
|930|EF_PRESSURE3|Varetyr Spear (falling spear)|
|931|EF_LINKPARTICLE2|	(Nothing)|
|932|EF_SOULLIGHT3|Firefly|
|933|EF_CHAREFFECT|[Client Crash]|
|934|EF_GUMGANG6|White, castishly expanding cone|
|935|EF_FIREBALL6|Green magic projectile|
|936|EF_GUMGANG7|Red, castishly expanding cone|
|937|EF_GUMGANG8|Yellow, castishly expanding cone|
|938|EF_GUMGANG9|Dark-red, castishly expanding cone|
|939|EF_BOTTOM_DE2|Blue, conish aura|
|940|EF_COLDSTATUS|Snow flake|
|941|EF_SPR_LIGHTPRINT3|Explosion of red, demonic fire|
|942|EF_WATERBALL3|Expanding, white dome|
|943|EF_HEAL_N2|Green, fluffy projectile|
|944|EF_RAIN_PARTICLE2|Falling gems|
|945|EF_CLOUD9|(Nothing)|
|946|EF_YELLOWFLY3|Floating lights|
|947|EF_EL_GUST|Blue lightning sphere|
|948|EF_EL_BLAST|Two blue lightning spheres|
|949|EF_EL_AQUAPLAY|Flat, spinning diamond|
|950|EF_EL_UPHEAVAL|Circling, planetlike spheres|
|951|EF_EL_WILD_STORM|	Three lightning spheres|
|952|EF_EL_CHILLY_AIR|	Flat, spinning gem and two lightning spheres|
|953|EF_EL_CURSED_SOIL|	Spinning, planetlike spheres|
|954|EF_EL_COOLER|Two lightblue glowing spheres|
|955|EF_EL_TROPIC|Three spinning flame spheres|
|956|EF_EL_PYROTECHNIC|	Flame|
|957|EF_EL_PETROLOGY|Spinning planetlike sphere|
|958|EF_EL_HEATER|Two flames|
|959|EF_POISON_MIST|Purple flame|
|960|EF_ERASER_CUTTER|	Small yellow explosion|
|961|EF_SILENT_BREEZE|	Cartoony whirlwind|
|962|EF_MAGMA_FLOW|Rising fire|
|963|EF_GRAYBODY|Dark filter (like Stone Curse)|
|964|EF_LAVA_SLIDE|Same as 920|
|965|EF_SONIC_CLAW|Small white explosion|
|966|EF_TINDER_BREAKER|	Bone crack|
|967|EF_MIDNIGHT_FRENZY|	Another little explosion|

---

## Usage Notes
<!-- RAG_CHUNK: 06_EF_USAGE_NOTES -->

- Effects are client-side only - they don't affect gameplay
- Some effects may not work on all client versions
- Use `@effect <id>` to test effects in-game
- `specialeffect` shows on NPC/mob, `specialeffect2` shows on player
- Some IDs cause client errors or crashes - test before using
- Effect constants are defined in `src/map/script_constants.hpp`

---

*Complete effect list from rAthena doc/effect_list.md - All 968 effects individually listed*

# ═══════════════════════════════════════════════════════════════════════════════
# PART 8: QUEST VARIABLES (doc/quest_variables.txt)
# ═══════════════════════════════════════════════════════════════════════════════

<!-- RAG_CHUNK: 06_QUEST_VARIABLES -->

//===== rAthena Documentation ================================
//= Permanent Quest Variables
//===== By: ==================================================
//= Lupus
//===== Last Updated: ========================================
//= 20120826
//===== Description: =========================================
//= This file should help to understand and manage bit-wise 
//= quest variables. You can store up to 31 boolean value into 
//= a single variable.
//============================================================

Variable: MISC_QUEST
--------------------------------------------------------------

Quest:		Juice Maker Quest
Info:		How to make juices. This bit keeps final state of the quest.
How to set:	set MISC_QUEST, MISC_QUEST | 1;
How to check:	if (MISC_QUEST & 1) {}

Quest:		-
Info:		-
How to set:	set MISC_QUEST, MISC_QUEST | 2;
How to check:	if (MISC_QUEST & 2) {}

Quest:		Morgenstein Quest
Info:		How to make Mixture & Counteragent. This bit keeps final state of the quest.
How to set:	set MISC_QUEST, MISC_QUEST | 4;
How to check:	if (MISC_QUEST & 4) {}

Quest:		Prontera Culvert Quest
Info:		Determines if player can enter Prontera Culverts.
How to set:	set MISC_QUEST, MISC_QUEST | 8;
How to check:	if (MISC_QUEST & 8) {}

Quest:		Edgar's Offer
Info:		Cheap ticket from Izlude to Alberta. This bit keeps final state of the quest.
How to set:	set MISC_QUEST, MISC_QUEST | 16;
How to check:	if (MISC_QUEST & 16) {}

Quest:		Piano Quest
Info:		The only way from Niflheim to Umbala.
How to set:	set MISC_QUEST, MISC_QUEST | 32;
How to check:	if (MISC_QUEST & 32) {}

Quest:		-
Info:		-
How to set:	set MISC_QUEST, MISC_QUEST | 64;
How to check:	if (MISC_QUEST & 64) {}

Quest:		-
Info:		-
How to set:	set MISC_QUEST, MISC_QUEST | 128;
How to check:	if (MISC_QUEST & 128) {}

Quest:		-
Info:		-
How to set:	set MISC_QUEST, MISC_QUEST | 256;
How to check:	if (MISC_QUEST & 256) {}

Quest:		Cube Room
Info:		Lighthalzen Cube Room quest (to enter Bio-Lab)
How to set:	set MISC_QUEST, MISC_QUEST | 512;
How to check:	if (MISC_QUEST & 512) {}

Quest:		Reset Skills Event
Info:		Yuno, Hypnotist Teacher
How to set:	set MISC_QUEST, MISC_QUEST | 1024;
How to check:	if (MISC_QUEST & 1024) {}

Quest:		Slotted Arm Guard Quest
Info:		Ninja Job Room, Boshuu
How to set:	set MISC_QUEST, MISC_QUEST | 2048;
How to check:	if (MISC_QUEST & 2048) {}

Quest:		Improved Arm Guard Quest
Info:		Ninja Job Room, Basshu
How to set:	set MISC_QUEST, MISC_QUEST | 4096;
How to check:	if (MISC_QUEST & 4096) {}

Quest:		Rachel Sanctuary Quest
Info:		Determines if player can access Rachel Santuary.
How to set:	set MISC_QUEST, MISC_QUEST | 8192;
How to check:	if (MISC_QUEST & 8192) {}

Quest:		Message Delivery Quest
Info:		Send a message to Elly, in Niflheim from Erious.
How to set:	set MISC_QUEST, MISC_QUEST | 16384;
How to check:	if (MISC_QUEST & 16384) {}

Quest:		Umbala Domestic Dispute?
Info:		Reward: 1 Yggdrasil Leaf.
How to set:	set MISC_QUEST, MISC_QUEST | 32768;
How to check:	if (MISC_QUEST & 32768) {}

Quest:		Access to the Turtle Island
Info:		Reward: ~1 OCA, OVB, GB.
How to set:	set MISC_QUEST, MISC_QUEST | 65536;
How to check:	if (MISC_QUEST & 65536) {}


Variable: MISC_QUEST2
--------------------------------------------------------------

Quest:		-
Info:		-
How to set:	set MISC_QUEST2, MISC_QUEST2 | ?;
How to check:	if (MISC_QUEST2 & ?) {}

# ═══════════════════════════════════════════════════════════════════════════════
# PART 9: NPC WHISPER SYSTEM (doc/whisper_sys.txt)
# ═══════════════════════════════════════════════════════════════════════════════

<!-- RAG_CHUNK: 06_WHISPER_SYSTEM -->

//===== rAthena Documentation ================================
//= NPC Whisper System
//===== By: ==================================================
//= lordalfa
//===== Last Updated: ========================================
//= 20120904
//===== Description: =========================================
//= A description of rAthena's NPC whispering system.
//============================================================

This piece of code to allows characters to execute events in NPCs by whispering 
them up to ten parameters. The NPC must have an "OnWhisperGlobal" label, or an 
"event not found" error will result.

	NPC:<NPC Name>		<String>{#String 2{#...{#String 10}}}
	
The whispered strings are separated by the "#" character, and are each stored
into separate temporary character string variables:

	@whispervar0$, @whispervar1$, ... @whispervar9$

---------------------------------------------------------------------------------

Below is an example of how this feature might be used.
You whisper an NPC "NPCCommander" in-game with the following instructions:

	NPC:NPCCommander	Report#Killstealing#Lordalfa

The parameters are passed on to the "OnWhisperGlobal" label of the NPC, and can
be processed accordingly:

-	script	NPCCommander	-1,{
OnWhisperGlobal:
	// Inform player "Lordalfa" that he has been reported for killstealing.
	if (@whispervar0$ == "Report")
		message @whispervar2$,"You have been reported for "+@whispervar1$+".";
	end;
}

This could also be used for hidden event triggers:

-	script	EventManager	-1,{
OnWhisperGlobal:
	if (getgmlevel() < 80) end;
	if (@whispervar0$ == "pvp") {
		// Script for a PVP event.
	}
	else if (@whispervar0$ == "mvp") {
		// Script for an MVP summoning event.
	}
	end;
}

# ═══════════════════════════════════════════════════════════════════════════════
# PART 10: CAPTCHA SYSTEM (doc/captcha_db.txt)
# ═══════════════════════════════════════════════════════════════════════════════

<!-- RAG_CHUNK: 06_CAPTCHA_SYSTEM -->

//===== rAthena Documentation ================================
//= Captcha Database Structure
//===== By: ==================================================
//= rAthena Dev Team
//===== Last Updated: ========================================
//= 20220920
//===== Description: =========================================
//= Explanation of the captcha_db.yml file and structure.
//============================================================

---------------------------------------

Id: Unique ID.

---------------------------------------

Filename: Name of the BMP image file (with location).
		  The path of the file can be different for each captcha image, but it's best practice to keep them in the same directory.

Example:
    Filename: db/import/captcha/rathena.bmp

---------------------------------------

Answer: Correct answer for the captcha (case-sensitive).

---------------------------------------

Bonus: NPC script that is ran when a captcha is successfully answered. Accepts all forms of script constants, variables, as well as the
	   unique player variable @captcha_retries. This variable can be used within the Bonus script to get the remaining retries a player
	   has. Coupled with the script command 'getbattleflag()' this could be used to assign different bonuses based on success rate.

Example:
    # Give level 10 Blessing for 20 minutes with no failures, else give for 30 seconds.
    Bonus: >
      if (@captcha_retries == getbattleflag("macro_detection_retry")) {
        # Player solved it on first try
        specialeffect2 EF_BLESSING;
        sc_start SC_BLESSING,1200000,10;
      } else {
        # Player needed more than one try
        specialeffect2 EF_BLESSING;
        sc_start SC_BLESSING,30000,10;
      }

---

<!-- RAG_CHUNK: 06_sample_instance_script -->
## Sample Instance Script (Example)

> Source: `doc/sample/instancing.txt` (208 lines)

Complete example of an instance system with creation, entry, mob spawning, and cleanup.

### Instance Database Entry
Before using, add to `db/(pre-)re/instance_db.txt`:
```
100,Abyss Lake Instance,3600,300,abyss_03,160,155
```

### Instance Creation NPC

```c
prontera,151,190,6	script	Sample Instance	101,{
	.@instance$ = "Abyss Lake Instance";

	if (instance_live_info(ILI_NAME, instance_id(IM_PARTY)) == .@instance$) {
		// Already in this instance
		mes "[Sample Instance]";
		mes "You are already part of an instance.";
		next;
		switch(select("Enter Instance.:Cancel.")) {
		case 1:
			break;
		case 2:
			mes "[Sample Instance]";
			mes "You don't want to try again?";
			emotion ET_CRY;
			close;
		}
	}
	else if (instance_id(IM_PARTY)) {
		// Another instance is running
		mes "[Sample Instance]";
		mes "You are part of the instance " + instance_live_info(ILI_NAME, instance_id(IM_PARTY)) + ".";
		close;
	}
	else {
		// Create new instance
		mes "[Sample Instance]";
		mes "Would you like to try the sample instance?";
		next;
		switch(select("Create Instance.:Cancel.")) {
		case 1:
			.@create = instance_create(.@instance$);
			if (.@create < 0) {
				mes "[Sample Instance]";
				switch (.@create) {
					case -1: mes "ERROR: Invalid type."; break;
					case -2: mes "ERROR: Party not found."; break;
					case -3: mes "ERROR: Instance already exists."; break;
					case -4: mes "ERROR: No free instances."; break;
				}
				close;
			}
			mes "[Sample Instance]";
			mes "Instance created. Now entering...";
			next;
			break;
		case 2:
			close;
		}
	}

	.@enter = instance_enter(.@instance$);
	if (.@enter != 0) {
		mes "[Sample Instance]";
		switch (.@enter) {
			case 1: mes "ERROR: Party not found."; break;
			case 2: mes "ERROR: Party does not have instance."; break;
			case 3: mes "ERROR: Unknown error."; break;
		}
		close;
	}
	close;
}
```

### Instance Start NPC

```c
abyss_03,154,159,6	script	Instance NPC#start	101,{
	mes "[Instance NPC]";
	mes "Are you ready to begin?";
	next;
	switch(select("Yes.:No.")) {
	case 1:
		mes "[Instance NPC]";
		mes "Good luck.";
		close2;
		donpcevent instance_npcname("#ins_abyss03_mobs")+"::OnEnable";
		delwaitingroom;
		disablenpc instance_npcname(strnpcinfo(0));
		end;
	case 2:
		mes "[Instance NPC]";
		mes "Take your time.";
		close;
	}
	end;

OnInit:
	disablenpc strnpcinfo(0);
	end;
OnInstanceInit:
	disablenpc instance_npcname("abysslakedunwarp004");
	waitingroom "Click here to start!",0;
	end;
}
```

### Monster Spawning Controller

```c
abyss_03,0,0,0	script	#ins_abyss03_mobs	-1,{
	end;
OnEnable:
	initnpctimer;
	end;
OnTimer1000:
	mapannounce strnpcinfo(4),"Instance NPC: The instance has begun.",bc_all;
	end;
OnTimer5000:
	stopnpctimer;

	// Spawn mobs with event labels
	.@map$        = instance_mapname("abyss_03");
	.@label$      = instance_npcname(strnpcinfo(0))+"::OnMyMobDead";
	.@label_boss$ = instance_npcname(strnpcinfo(0))+"::OnMyBossDead";

	monster .@map$,0,0,"Huge Poring",1002,20,.@label$,2;
	monster .@map$,0,0,"Huge Drops",1113,15,.@label$,2;
	monster .@map$,97,102,"Treasure Chest",1732,1,.@label_boss$,2;
	end;

OnMyMobDead:
	dispbottom "What am I doing? I should attack the Treasure Chest!";
	viewpoint 0,97,102,0,0xFF0000;
	switch (rand(6)) {
		case 0: sc_start SC_STONE,5000,0; break;
		case 1: sc_start SC_FREEZE,5000,0; break;
		case 2: sc_start SC_STUN,5000,0; break;
		case 3: sc_start SC_SLEEP,5000,0; break;
		case 4: sc_start SC_CONFUSION,5000,0; break;
		case 5: sc_start SC_BLIND,5000,0; break;
	}
	end;

OnMyBossDead:
	specialeffect2 EF_MVP;
	getitem 512,1; // Apple

	.@map$   = instance_mapname("abyss_03");
	.@label$ = instance_npcname(strnpcinfo(0))+"::OnMyMobDead";
	killmonster .@map$,.@label$;
	mapannounce .@map$,"Instance NPC: Good work! Speak to me now.",bc_all;
	donpcevent instance_npcname("Instance NPC#finish")+"::OnEnable";
	end;
}
```

### Instance Completion NPC

```c
abyss_03,97,102,4	script	Instance NPC#finish	101,{
	mes "[Instance NPC]";
	mes "Congratulations! You've finished.";
	mes "I'll send you back to town now.";
	emotion ET_BEST;
	close2;
	warp "prontera",156,191;
	instance_destroy();
	end;

OnInit:
	disablenpc strnpcinfo(0);
	end;
OnInstanceInit:
	disablenpc instance_npcname(strnpcinfo(0));
	end;
OnEnable:
	enablenpc instance_npcname(strnpcinfo(0));
	specialeffect EF_HIDING;
	end;
}
```

### Key Instance Functions

| Function | Description |
|----------|-------------|
| `instance_create(name)` | Creates instance, returns ID or error |
| `instance_enter(name)` | Warps player into instance |
| `instance_destroy()` | Destroys current instance |
| `instance_id(IM_PARTY)` | Gets party's instance ID |
| `instance_mapname(map)` | Gets instanced map name |
| `instance_npcname(name)` | Gets instanced NPC name |
| `instance_live_info(type,id)` | Gets instance info |

### Error Codes

**instance_create returns:**
| Code | Meaning |
|------|---------|
| -1 | Invalid type |
| -2 | Party not found |
| -3 | Instance already exists |
| -4 | No free instances |

**instance_enter returns:**
| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | Party not found |
| 2 | No instance |
| 3 | Unknown error |

---

<!-- RAG_CHUNK: 06_sample_dynamic_shop -->
## Sample Dynamic Shop (Example)

> Source: `doc/sample/npc_dynamic_shop.txt` (93 lines)

Example of a shop that changes based on conditions.

```c
prontera,150,150,4	script	Dynamic Shop	100,{
	mes "[Shop Keeper]";
	mes "Welcome! My stock changes based on your level.";
	next;

	// Clear previous shop data
	deletearray .@items;
	deletearray .@prices;
	.@count = 0;

	// Always available items
	.@items[.@count] = 501;  // Red Potion
	.@prices[.@count] = 50;
	.@count++;

	.@items[.@count] = 502;  // Orange Potion
	.@prices[.@count] = 200;
	.@count++;

	// Level 30+ items
	if (BaseLevel >= 30) {
		.@items[.@count] = 503;  // Yellow Potion
		.@prices[.@count] = 550;
		.@count++;
	}

	// Level 50+ items
	if (BaseLevel >= 50) {
		.@items[.@count] = 504;  // White Potion
		.@prices[.@count] = 1200;
		.@count++;
	}

	// Level 70+ items
	if (BaseLevel >= 70) {
		.@items[.@count] = 547;  // Condensed White Potion
		.@prices[.@count] = 2500;
		.@count++;
	}

	// VIP items
	if (vip_status(1)) {
		.@items[.@count] = 12016; // Speed Potion
		.@prices[.@count] = 5000;
		.@count++;
	}

	// Build and open shop
	npcshopdelitem "dynamic_shop#" + strnpcinfo(0), 0;
	for (.@i = 0; .@i < .@count; .@i++) {
		npcshopadditem "dynamic_shop#" + strnpcinfo(0), .@items[.@i], .@prices[.@i];
	}

	mes "Here's what I have for you today.";
	close2;
	callshop "dynamic_shop#" + strnpcinfo(0), 1;
	end;
}

-	shop	dynamic_shop#Dynamic Shop	-1,501:50
```

### Key Dynamic Shop Functions

| Function | Description |
|----------|-------------|
| `npcshopdelitem(shop,id)` | Remove item (0 = clear all) |
| `npcshopadditem(shop,id,price)` | Add item with price |
| `callshop(shop,type)` | Open shop (1=buy, 2=sell) |

---

# ═══════════════════════════════════════════════════════════════
# PART 11: ATTENDANCE SYSTEM
# ═══════════════════════════════════════════════════════════════

<!-- RAG_CHUNK: 06_attendance_overview -->
## Attendance System Overview

The Attendance System provides daily login rewards. Players claim rewards by logging in each day during an event period.

### Database Location
- **File:** `db/re/attendance.yml` (Renewal) or `db/pre-re/attendance.yml`
- **Type:** ATTENDANCE_DB

---

<!-- RAG_CHUNK: 06_attendance_schema -->
## Attendance YAML Schema

```yaml
Header:
  Type: ATTENDANCE_DB
  Version: 1

Body:
  - Start: YYYYMMDD          # Event start date (e.g., 20180502)
    End: YYYYMMDD            # Event end date (e.g., 20180529)
    Rewards:
      - Day: <number>        # Day number (1-20)
        ItemId: <item_id>    # Item ID or aegis name
        Amount: <number>     # Quantity (default: 1)
```

### Example Configuration
```yaml
Body:
  - Start: 20250101
    End: 20250131
    Rewards:
      - Day: 1
        ItemId: 22979
      - Day: 7
        ItemId: 23340
        Amount: 3
      - Day: 20
        ItemId: 22845
```

### Server Configuration
```conf
# conf/battle/client.conf
feature.attendance: 1   # 0=disabled, 1=enabled
```

**Client Requirement:** PACKETVER >= 20180307

---

# ═══════════════════════════════════════════════════════════════
# PART 12: STYLIST SYSTEM
# ═══════════════════════════════════════════════════════════════

<!-- RAG_CHUNK: 06_stylist_overview -->
## Stylist System Overview

The Stylist system allows players to change character appearance (hair style, hair color, cloth color).

### Database Location
- **Main:** `db/stylist.yml`
- **Renewal:** `db/re/stylist.yml`
- **Import:** `db/import/stylist.yml`

---

<!-- RAG_CHUNK: 06_stylist_schema -->
## Stylist YAML Schema

```yaml
Header:
  Type: STYLIST_DB
  Version: 1

Body:
  - Look: <look_type>       # Hair_Color, Hair, Cloth_Color
    Options:
      - Index: <number>     # Client menu index (-1 = revert)
        Value: <number>     # Look value
        CostsHuman:
          Price: <zeny>
          RequiredItem: <item_name>
          RequiredItemBox: <item_name>
        CostsDoram:         # Same structure for Doram
          Price: <zeny>
```

### Look Types
| Type | Description |
|------|-------------|
| Hair_Color | Hair dye (0-8) |
| Hair | Hairstyle (1-42+) |
| Cloth_Color | Outfit palette |

---

<!-- RAG_CHUNK: 06_stylist_npc -->
## Stylist NPC Script

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
        switch(select(" ~ Next: ~ Previous: ~ Jump to...: ~ Revert")) {
            case 1: set .@Style, ((.@Style != .@Styles[.@s]) ? .@Style + 1 : 1); break;
            case 2: set .@Style, ((.@Style != 1) ? .@Style - 1 : .@Styles[.@s]); break;
            case 3: input .@Style, 1, .@Styles[.@s]; break;
            case 4: setlook .@Look[.@s], .@Revert; end;
        }
    }
}
```

---

<!-- RAG_CHUNK: 06_stylist_commands -->
## Stylist Script Commands

| Command | Description |
|---------|-------------|
| `setlook <type>, <value>` | Set appearance |
| `getlook(<type>)` | Get current appearance |
| `changelook <type>, <value>` | Change for attached player |
| `getbattleflag("max_hair_style")` | Get max allowed |

### Look Constants
```c
LOOK_HAIR          // Hairstyle
LOOK_HAIR_COLOR    // Hair color
LOOK_CLOTHES_COLOR // Cloth color
LOOK_HEAD_BOTTOM   // Lower headgear
LOOK_HEAD_TOP      // Upper headgear
LOOK_HEAD_MID      // Middle headgear
```

### Server Configuration
```conf
# conf/battle/client.conf
max_hair_style: 42
max_hair_color: 8
max_cloth_color: 4
```

---

<!-- RAG_CHUNK: 06_item_enchant_system -->
# PART 13: ITEM ENCHANT SYSTEM (NEW 2026-01)

## Item Enchant Overview

The Item Enchant system allows players to add special enchantments to equipment. Added in rAthena January 2026 update.

## Item Enchant YAML Schema

```yaml
# db/re/item_enchant.yml
Header:
  Type: ITEM_ENCHANT_DB
  Version: 1

Body:
  - Id: <client_lua_index>
    TargetItems:
      - <item_name>
    MinimumRefine: 0
    MinimumEnchantgrade: 0
    AllowRandomOptions: true
    Reset:
      Chance: <success_rate>
      Price: <zeny_cost>
      Materials:
        - Material: <item_name>
          Amount: 1
    Order:
      - Slot: 0
      - Slot: 1
      - Slot: 2
      - Slot: 3
    Slots:
      - Slot: 0
        Price: <zeny_cost>
        Materials:
          - Material: <item_name>
            Amount: 1
        Chance: 100000
        EnchantgradeBonus:
          - Enchantgrade: 1
            Chance: 5000
        Enchants:
          - Enchant: <bonus_item_id>
            Chance: <rate>
```

## Key Fields

| Field | Description |
|-------|-------------|
| `Id` | Client-side LUA index for the enchant NPC |
| `TargetItems` | List of items that can be enchanted |
| `MinimumRefine` | Required refine level (default: 0) |
| `MinimumEnchantgrade` | Required enchant grade (default: 0) |
| `AllowRandomOptions` | Allow items with random options (default: true) |
| `Reset.Chance` | Success rate for resetting enchants |
| `Reset.Price` | Zeny cost for reset |
| `Order` | Slot enchant order (0-3) |
| `Slots` | Enchant configuration per slot |

## Example: Basic Weapon Enchant

```yaml
- Id: 1
  TargetItems:
    - Crimson_Sword
    - Crimson_Dagger
  MinimumRefine: 7
  Reset:
    Chance: 100000
    Price: 100000
  Order:
    - Slot: 3
    - Slot: 2
  Slots:
    - Slot: 3
      Price: 50000
      Chance: 80000
      Enchants:
        - Enchant: 4700  # ATK +1%
          Chance: 50000
        - Enchant: 4701  # ATK +2%
          Chance: 30000
        - Enchant: 4702  # ATK +3%
          Chance: 20000
```

---

<!-- RAG_CHUNK: 06_item_reform_system -->
# PART 14: ITEM REFORM SYSTEM (UPDATED 2026-01)

## Item Reform Overview

The Item Reform system allows upgrading items to higher tiers. Major updates in January 2026.

## Item Reform YAML Schema

```yaml
# db/re/item_reform.yml
Header:
  Type: ITEM_REFORM_DB
  Version: 1

Body:
  - Id: <reform_id>
    SourceItems:
      - Item: <source_item>
        MinimumRefine: 0
        MinimumEnchantgrade: 0
        RandomOptions:
          Allow: true
    ResultItem: <result_item>
    Materials:
      - Material: <item_name>
        Amount: 1
    Costs:
      - Type: Zeny
        Amount: <cost>
```

---

<!-- RAG_CHUNK: 06_new_skill_implementations_2026 -->
# PART 15: NEW SKILL IMPLEMENTATIONS (2026-01)

## Gunslinger Skills (13 new implementations)

| Skill | File | Description |
|-------|------|-------------|
| GS_BULLSEYE | bullseye.cpp | Critical headshot skill |
| GS_CRACKER | cracker.cpp | Flashbang grenade |
| GS_DESPERADO | desperado.cpp | Rapid fire AoE |
| GS_DISARM | disarm.cpp | Weapon disabling shot |
| GS_DUST | dust.cpp | Ground shot |
| GS_FLING | fling.cpp | Coin throw attack |
| GS_FULLBUSTER | fullbuster.cpp | Full power shot |
| GS_GATLINGFEVER | gatlingfever.cpp | Gatling gun buff |
| GS_GLITTERING | glittering.cpp | Coin flip buff |
| GS_GROUNDDRIFT | grounddrift.cpp | Ground grenade |
| GS_PIERCINGSHOT | piercingshot.cpp | Armor piercing shot |
| GS_RAPIDSHOWER | rapidshower.cpp | Quick multi-shot |
| GS_SPREADATTACK | spreadattack.cpp | Shotgun blast |
| GS_TRACKING | tracking.cpp | Sniper aim |
| GS_TRIPLEACTION | tripleaction.cpp | Triple shot |

## Mage Skills (13 new implementations)

| Skill | File | Description |
|-------|------|-------------|
| MG_COLDBOLT | coldbolt.cpp | Ice bolt attack |
| MG_ENERGYCOAT | energycoat.cpp | SP shield buff |
| MG_FIREBALL | fireball.cpp | AoE fire attack |
| MG_FIREBOLT | firebolt.cpp | Fire bolt attack |
| MG_FIREWALL | firewall.cpp | Fire barrier |
| MG_FROSTDIVER | frostdiver.cpp | Freeze attack |
| MG_LIGHTNINGBOLT | lightningbolt.cpp | Lightning attack |
| MG_NAPALMBEAT | napalmbeat.cpp | Ghost attack |
| MG_SIGHT | sight.cpp | Reveal hidden |
| MG_SOULSTRIKE | soulstrike.cpp | Ghost multi-hit |
| MG_STONECURSE | stonecurse.cpp | Petrify attack |
| MG_THUNDERSTORM | thunderstorm.cpp | AoE lightning |

## Taekwon Skills (12 new implementations)

| Skill | File | Description |
|-------|------|-------------|
| TK_COUNTER | counter.cpp | Counter attack |
| TK_DOWNKICK | downkick.cpp | Knockdown kick |
| TK_HIGHJUMP | highjump.cpp | High jump movement |
| TK_JUMPKICK | jumpkick.cpp | Jumping kick attack |
| TK_MISSION | mission.cpp | Taekwon mission |
| TK_RUN | run.cpp | Sprint skill |
| TK_SEVENWIND | sevenwind.cpp | Elemental enchant |
| TK_STORMKICK | stormkick.cpp | Wind kick attack |
| TK_TURNKICK | turnkick.cpp | Spinning kick |

## Skill Implementation Structure

```cpp
// src/map/skills/<class>/<skillname>.cpp
#include "skillname.hpp"
#include "../skill_impl.hpp"

class SkillName : public WeaponSkillImpl {
public:
    SkillName() : WeaponSkillImpl(SKILL_ID) {}
    
    int32 castend_damage_id(struct block_list* src, 
                            struct block_list* bl,
                            uint16 skill_id, 
                            uint16 skill_lv,
                            t_tick tick, 
                            int flag) override;
};
```

---

<!-- RAG_CHUNK: 06_jan2026_new_items -->
# PART 16: NEW ITEMS - JANUARY 2026 UPDATE

## Summary: 526 New Items Added

| Category | Count | ID Range |
|----------|-------|----------|
| Equipment (Weapons, Armor) | 208 | Various |
| Usable Items | 158 | Various |
| Etc Items | 160 | Various |

## New 4th Job Equipment (Frontier Series)

### Frontier Rune Crowns (All 4th Jobs)
| ID | AegisName | Name |
|----|-----------|------|
| 400975 | Frontier_R_Crown_DK | Frontier Rune Crown (Dragon Knight) |
| 400976 | Frontier_R_Crown_IG | Frontier Rune Crown (Imperial Guard) |
| 400977 | Frontier_R_Crown_MT | Frontier Rune Crown (Meister) |
| 400978 | Frontier_R_Crown_BO | Frontier Rune Crown (Biolo) |
| 400979 | Frontier_R_Crown_SHC | Frontier Rune Crown (Shadow Cross) |
| 400980 | Frontier_R_Crown_ABC | Frontier Rune Crown (Abyss Chaser) |
| 400981 | Frontier_R_Crown_AG | Frontier Rune Crown (Arch Mage) |
| 400982 | Frontier_R_Crown_EM | Frontier Rune Crown (Elemental Master) |
| 400983 | Frontier_R_Crown_CD | Frontier Rune Crown (Cardinal) |
| 400984 | Frontier_R_Crown_IQ | Frontier Rune Crown (Inquisitor) |
| 400985 | Frontier_R_Crown_WH | Frontier Rune Crown (Windhawk) |
| 400986 | Frontier_R_Crown_TR | Frontier Rune Crown (Troubadour & Trouvere) |
| 400987 | Frontier_R_Crown_SS | Frontier Rune Crown (Shinkiro & Shiranui) |
| 400988 | Frontier_R_Crown_NW | Frontier Rune Crown (Night Watch) |
| 400989 | Frontier_R_Crown_SKE | Frontier Rune Crown (Sky Emperor) |
| 400990 | Frontier_R_Crown_SOA | Frontier Rune Crown (Soul Ascetic) |
| 400991 | Frontier_R_Crown_HN | Frontier Rune Crown (Hyper Novice) |
| 400992 | Frontier_R_Crown_SH | Frontier Rune Crown (Spirit Handler) |

### Sky/Celestial Rune Crowns
| ID | AegisName | Name |
|----|-----------|------|
| 401055 | Stardust_Crown_SV | Silver Stardust Crown |
| 401056 | Stardust_Crown_SC | Scarlet Stardust Crown |
| 401057 | Stardust_Crown_VI | Violet Stardust Crown |
| 401058 | Sky_Rune_Crown_IG | Celestial Rune Crown (Imperial Guard) |
| 401059 | Sky_Rune_Crown_ABC | Celestial Rune Crown (Abyss Chaser) |
| 401060 | Sky_Rune_Crown_SH | Rune Crown of the Sky (Spirit Handler) |
| 401115 | Sky_Rune_Crown_MS | Sky Rune Crown (Meister) |
| 401116 | Sky_Rune_Crown_WH | Sky Rune Crown (Windhawk) |
| 401117 | Sky_Rune_Crown_HN | Sky Rune Crown (Hyper Novice) |
| 401118 | Sky_Rune_Crown_CD | Sky Rune Crown (Cardinal) |
| 401119 | Sky_Rune_Crown_IQ | Sky Rune Crown (Inquisitor) |
| 401120 | Sky_Rune_Crown_SKE | Sky Rune Crown (Sky Emperor) |

### Encroached Weapons (All Types)
| ID | AegisName | Name | Type |
|----|-----------|------|------|
| 500119 | Encroached_Sword | Encroached Sword | 1H Sword |
| 510140 | Encroached_Dagger | Encroached Dagger | Dagger |
| 530071 | Encroached_Spear | Encroached Spear | 1H Spear |
| 540109 | Encroached_Book | Encroached Book | Book |
| 550137 | Encroached_Staff | Encroached Staff | 1H Staff |
| 550174 | Encroached_Foxtail | Encroached Foxtail | Foxtail |
| 560080 | Encroached_Knuckle | Encroached Knuckles | Knuckle |
| 570086 | Encroached_Instrument | Encroached Instrument | Instrument |
| 580086 | Encroached_Whip | Encroached Whip | Whip |
| 590081 | Encroached_Mace | Encroached Mace | Mace |
| 600056 | Encroached_T_Sword | Encroached Two-Handed Sword | 2H Sword |
| 610084 | Encroached_Katar | Encroached Katar | Katar |
| 620038 | Encroached_T_Axe | Encroached Two-Handed Axe | 2H Axe |
| 630059 | Encroached_T_Spear | Encroached Two-Handed Spear | 2H Spear |
| 640051 | Encroached_T_Staff | Encroached Two-Handed Staff | 2H Staff |
| 650048 | Encroached_Humma | Encroached Huuma Shuriken | Huuma |
| 700117 | Encroached_Bow | Encroached Bow | Bow |
| 810048 | Encroached_Rifle | Encroached Firearm | Rifle |

### Frontier Weapons (4th Job Specific)
| ID | AegisName | Name | Class |
|----|-----------|------|-------|
| 510192 | Frontier_ABC_Dagger | Frontier Abyss Dagger | Abyss Chaser |
| 530072 | Frontier_IG_Spear | Frontier Imperial Spear | Imperial Guard |
| 540110 | Frontier_EM_Book | Frontier Elemental Book | Elemental Master |
| 540111 | Frontier_SKE_Book | Frontier Emperor Battle Book | Sky Emperor |
| 550176 | Frontier_CD_Rod | Frontier Saint Lord | Cardinal |
| 550177 | Frontier_HN_Rod | Frontier Hyper Lord | Hyper Novice |
| 550178 | Frontier_SH_Foxtail | Frontier Spirit Foxtail | Spirit Handler |
| 560081 | Frontier_IQ_Claw | Frontier Judgment Claw | Inquisitor |
| 570087 | Frontier_TR_Vilolin | Frontier Musical Violin | Troubadour |
| 580087 | Frontier_TR_Rope | Frontier Musical Rope | Trouvere |
| 590107 | Frontier_BO_Hall | Frontier Biological Scepter | Biolo |
| 600071 | Frontier_DK_T_Sword | Frontier Dragon Sword | Dragon Knight |
| 610085 | Frontier_SHC_Katar | Frontier Shadow Katar | Shadow Cross |
| 620058 | Frontier_MT_T_Axe | Frontier Mechanical Axe | Meister |
| 640064 | Frontier_AG_Staff | Frontier Arc Staff | Arch Mage |
| 640065 | Frontier_SOA_Staff | Frontier Soul Staff | Soul Ascetic |
| 650058 | Frontier_SS_Humma | Frontier Moonlight Fūma Shuriken | Shinkiro/Shiranui |
| 700119 | Frontier_WH_Bow | Frontier Wind Bow | Windhawk |
| 810049 | Frontier_NW_Rifle | Frontier Knight Rifle | Night Watch |

### New Shadow Equipment (4th Job)
| ID | AegisName | Name | Class |
|----|-----------|------|-------|
| 1270079 | S_SHC_CR_Earring | Crater Shadow Earring | Shadow Cross |
| 1270080 | S_SHC_CR_Pendant | Crater Shadow Pendant | Shadow Cross |
| 1270081 | S_SHC_ST_Armor | Stab Shadow Armor | Shadow Cross |
| 1270082 | S_SHC_ST_Shoes | Stab Shadow Shoes | Shadow Cross |
| 1270083 | S_IQ_TP_Earring | Punish Shadow Earring | Inquisitor |
| 1270084 | S_IQ_TP_Pendant | Punish Shadow Pendant | Inquisitor |
| 1270091 | S_AG_CI_Earring | Crystal Illusion Shadow Earring | Arch Mage |
| 1270092 | S_AG_CI_Pendant | Crystal Illusion Shadow Pendant | Arch Mage |
| 1270099 | S_SKE_MS_Earring | Midnight Kick Shadow Earring | Sky Emperor |
| 1270100 | S_SKE_MS_Pendant | Midnight Kick Shadow Pendant | Sky Emperor |
| 1270115 | S_CD_FP_Earring | Fracella Shadow Earring | Cardinal |
| 1270116 | S_CD_FP_Pendant | Fracella Shadow Pendant | Cardinal |
| 1270119 | S_EM_DS_Earring | Diamond Shadow Earring | Elemental Master |
| 1270130 | S_WH_WH_Earring | Wild Hawk Shadow Earring | Windhawk |
| 1270134 | S_TR_MS_Earring | Musical Shooting Shadow Earring | Troubadour |
| 1270138 | S_NW_MS_Earring | Midnight Shooting Shadow Earring | Night Watch |

### New Costumes (Selected)
| ID | AegisName | Name |
|----|-----------|------|
| 400913 | C_CLB_DT_TS_Mini | Costume: Toothless Mini |
| 400914 | C_CLB_DT_TS_Drooping | Costume: Toothless Floppy |
| 410440 | C_CLB_DT_TS_Hat | Costume: Toothless Head |
| 480595 | C_CLB_DT_TS_Wing | Costume: Toothless Wings |
| 480596 | C_CLB_DT_TS_Hood | Costume: Toothless Hood |
| 400792 | C_Garden_Of_Heaven | Costume Garden of Heaven |
| 400965 | C_Divine_Veil | Costume Divine Veil |
| 410399 | C_Capybara | Costume Capybara |
| 420552 | C_Divine_Sky_Invite | Costume Divine Invitation |
| 480566 | C_Immortal_H_Wing | Costume: Immortal Monarch's Wings |

---

<!-- RAG_CHUNK: 06_jan2026_new_mobs -->
# PART 17: NEW MOBS - JANUARY 2026 UPDATE

## Summary: 144 New Training Dummies Added

The January 2026 update adds comprehensive Training Zone 123 with various training dummies.

### Training Dummy Types

| Category | Purpose |
|----------|---------|
| Size Variants | Small, Medium, Large, Extra Large |
| Refine Variants | R10, R20, R30, R40, R50 (damage reduction) |
| Magic Variants | M10, M20, M30, M40, M50 (magic defense) |
| Race Dummies | All 10 races for race-specific testing |
| Element Dummies | All 10 elements for elemental testing |
| Player Dummies | Human Player, Doram Player |

### Size Training Dummies
| ID | AegisName | Name |
|----|-----------|------|
| 22551 | S_DUMMY_SMALL_R10 | Dummy (Small) |
| 22552 | S_DUMMY_MEDIUM_R10 | Dummy (Medium) |
| 22553 | S_DUMMY_LARGE_R10 | Dummy (Large) |
| 22554 | S_DUMMY_XLARGE_R40 | Dummy (Extra Large) |

### Race Training Dummies
| ID | AegisName | Name | Race |
|----|-----------|------|------|
| 22628 | S_DUMMY2_NOTHING | Dummy (Formless Race) | Formless |
| 22629 | S_DUMMY2_DRAGON | Dummy (Dragon Race) | Dragon |
| 22630 | S_DUMMY2_ANIMAL | Dummy (Brute Race) | Brute |
| 22631 | S_DUMMY2_HUMAN | Dummy (Human Race) | Human |
| 22632 | S_DUMMY2_INSECT | Dummy (Insect Race) | Insect |
| 22633 | S_DUMMY2_FISH | Dummy (Fish Race) | Fish |
| 22634 | S_DUMMY2_DEMON | Dummy (Demon Race) | Demon |
| 22635 | S_DUMMY2_PLANT | Dummy (Plant Race) | Plant |
| 22636 | S_DUMMY2_ANGEL | Dummy (Angel Race) | Angel |
| 22637 | S_DUMMY2_UNDEAD | Dummy (Undead Race) | Undead |

### Element Training Dummies
| ID | AegisName | Name | Element |
|----|-----------|------|---------|
| 22648 | S_DUMMY2_NOTHING2 | Dummy (Neutral) | Neutral |
| 22649 | S_DUMMY2_WATER | Dummy (Water) | Water |
| 22650 | S_DUMMY2_GROUND | Dummy (Earth) | Earth |
| 22651 | S_DUMMY2_FIRE | Dummy (Fire) | Fire |
| 22652 | S_DUMMY2_WIND | Dummy (Wind) | Wind |
| 22653 | S_DUMMY2_POISON | Dummy (Poison) | Poison |
| 22654 | S_DUMMY2_SAINT | Dummy (Holy) | Holy |
| 22655 | S_DUMMY2_DARKNESS | Dummy (Dark) | Dark |
| 22656 | S_DUMMY2_TELEKINESIS | Dummy (Ghost) | Ghost |
| 22657 | S_DUMMY2_UNDEAD2 | Dummy (Undead) | Undead |

### Player Type Dummies
| ID | AegisName | Name |
|----|-----------|------|
| 21087 | S_DUMMY_100_HUMANP | Dummy (Human Player) |
| 21088 | S_DUMMY_100_DORAMP | Dummy (Doram Player) |

---

<!-- RAG_CHUNK: 06_jan2026_new_constants -->
# PART 18: NEW SCRIPT CONSTANTS - JANUARY 2026 UPDATE

## Summary: 146 New Script Constants Added

### New Job Constants
```c
EAJ_SPIRIT_HANDLER    // Spirit Handler job
EAJ_HYPER_NOVICE      // Hyper Novice job
EAJ_SKY_EMPEROR       // Sky Emperor job
EAJ_NIGHT_WATCH       // Night Watch job
EAJ_SHINKIROSHIRANUI  // Shinkiro/Shiranui job
EAJ_SOUL_ASCETIC      // Soul Ascetic job
```

### New Bonus Constants
```c
bNonCritAtkRate       // SP_NON_CRIT_ATK_RATE - Non-critical attack rate modifier
```

### New Effect Status
```c
EFST_BLOCK            // Block effect status
```

### New Item Group Constants (IG_*)
```c
IG_AEGIS_100582
IG_AEGIS_100584
IG_DT_COLABO_BOX1
IG_DT_COLABO_BOX2
IG_CLOUD_COSTUME_PACK
IG_COSTUMEMILEPACK_39_1
IG_COSTUMEMILEPACK_39_2
IG_COSTUMEMILEPACK_39_3
IG_RT_CH01_ARMOR_A
IG_RT_CH01_ARMOR_C
IG_RT_CH01_DIMEN_A
IG_RT_CH01_DIMEN_C
IG_RT_CH01_DIMEN_3
IG_RT_CH01_EXTRA_A
IG_RT_CH01_EXTRA_C
IG_RT_CH01_EXTRA_2
IG_RT_CH01_EXTRA_4
IG_RT_CH01_EXTRA_5
IG_AEGIS_104901
IG_AEGIS_105031
IG_23TH_COSTUME_A
IG_23TH_COSTUME_B
IG_23TH_COSTUME_C
IG_AEGIS_105059
IG_AEGIS_105161
IG_AEGIS_105162
IG_AEGIS_105219
IG_AEGIS_105220
IG_SP_COSTUME_COLLECTION
IG_2025ROS_FOR_OFFLINE
IG_AEGIS_105518
```

---

<!-- RAG_CHUNK: 06_jan2026_new_pets -->
# PART 19: NEW PETS - JANUARY 2026 UPDATE

## New Pets Added

### Domovoi (Brownie)
```yaml
- Mob: DOMOVOI
  EggItem: Brownie_Egg
  FoodItem: Pet_Food
  Script: >
    .@i = getpetinfo(PETINFO_INTIMATE);
    if (.@i >= PET_INTIMATE_LOYAL) {
       bonus2 bAddRace,RC_DemiHuman,1;
       bonus2 bMagicAddRace,RC_DemiHuman,1;
       bonus2 bSubRace,RC_DemiHuman,1;
    }
```

### Orc Hero
```yaml
- Mob: ORK_HERO
  EggItem: Orc_Hero_Egg
  Script: >
    .@i = getpetinfo(PETINFO_INTIMATE);
    if (.@i >= PET_INTIMATE_LOYAL) {
       bonus bBaseAtk,40;
    }
    else if (.@i >= PET_INTIMATE_CORDIAL) {
       bonus bBaseAtk,30;
    }
    else if (.@i >= PET_INTIMATE_NEUTRAL) {
       bonus bBaseAtk,20;
    }
    else {
       bonus bBaseAtk,10;
       bonus bDef,-3;
    }
```

### Orc Lord
```yaml
- Mob: ORC_LORD
  EggItem: Orc_Lord_Egg
  Script: >
    .@i = getpetinfo(PETINFO_INTIMATE);
    if (.@i >= PET_INTIMATE_LOYAL) {
       bonus bMatk,20;
       bonus bBaseAtk,20;
    }
    else if (.@i >= PET_INTIMATE_CORDIAL) {
       bonus bMatk,15;
       bonus bBaseAtk,15;
    }
    else if (.@i >= PET_INTIMATE_NEUTRAL) {
       bonus bMatk,10;
       bonus bBaseAtk,10;
    }
    else {
       bonus bBaseAtk,10;
       bonus bDef,-3;
    }
```

### New Eggs Added
| ID | AegisName | Name |
|----|-----------|------|
| 9169 | aegis_9169 | Clock Tower Manager Egg |
| 9170 | aegis_9170 | Angelgolt Egg |
| 9171 | aegis_9171 | Timeholder Egg |
| 9187 | Skeggiold_Egg | Skeggiold Egg |
| 9190 | aegis_9190 | Clock Egg |


---

<!-- RAG_CHUNK: 16_Complete_Equipment_Items_Jan2026 -->
## Part 16 Detail: Complete New Equipment Items (January 2026)

**Total: 208 equipment items**

| ID | AegisName | Name |
|-----|-----------|------|
| 9169 | aegis_9169 | Clock Tower Manager Egg |
| 9170 | aegis_9170 | Angelgolt Egg |
| 9171 | aegis_9171 | Timeholder Egg |
| 9187 | Skeggiold_Egg | Skeggiold Egg |
| 9190 | aegis_9190 | Clock Egg |
| 28145 | Sky_Rush_Axe | Sky Rush Axe |
| 400542 | Time_DM_R_Crown_NW | Time Dimensions Rune Crown (Night Watch) |
| 400543 | Time_DM_R_Crown_SKE | Time Dimensions Rune Crown (Sky Emperor) |
| 400792 | C_Garden_Of_Heaven | Costume Garden of Heaven |
| 400795 | aegis_400795 | Costume Thorn Tree Hairband (Blue) |
| 400803 | C_Muka_Sombrero | Costume Muka Sombrero |
| 400913 | C_CLB_DT_TS_Mini | Costume: Toothless Mini |
| 400914 | C_CLB_DT_TS_Drooping | Costume: Toothless Floppy |
| 400919 | C_Petal_Hood | Costume Petal Hood |
| 400930 | C_Steamroller | Costume Wolf Masquerade(White) |
| 400951 | aegis_400951 | Costume Night Market Special Salt |
| 400956 | aegis_400956 | Costume: Nightmare Mask |
| 400963 | aegis_400963 | Costume Nyar's White Ears |
| 400964 | aegis_400964 | Costume Nyar's Gray Ears |
| 400965 | C_Divine_Veil | Costume Divine Veil |
| 400975 | Frontier_R_Crown_DK | Frontier Rune Crown (Dragon Knight) |
| 400976 | Frontier_R_Crown_IG | Frontier Rune Crown (Imperial Guard) |
| 400977 | Frontier_R_Crown_MT | Frontier Rune Crown (Meister) |
| 400978 | Frontier_R_Crown_BO | Frontier Rune Crown (Biolo) |
| 400979 | Frontier_R_Crown_SHC | Frontier Rune Crown (Shadow Cross) |
| 400980 | Frontier_R_Crown_ABC | Frontier Rune Crown (Abyss Chaser) |
| 400981 | Frontier_R_Crown_AG | Frontier Rune Crown (Arch Mage) |
| 400982 | Frontier_R_Crown_EM | Frontier Rune Crown (Elemental Master) |
| 400983 | Frontier_R_Crown_CD | Frontier Rune Crown (Cardinal) |
| 400984 | Frontier_R_Crown_IQ | Frontier Rune Crown (Inquisitor) |
| 400985 | Frontier_R_Crown_WH | Frontier Rune Crown (Windhawk) |
| 400986 | Frontier_R_Crown_TR | Frontier Rune Crown (Troubadour & Trouvere) |
| 400987 | Frontier_R_Crown_SS | Frontier Rune Crown (Shinkiro & Shiranui) |
| 400988 | Frontier_R_Crown_NW | Frontier Rune Crown (Night Watch) |
| 400989 | Frontier_R_Crown_SKE | Frontier Rune Crown (Sky Emperor) |
| 400990 | Frontier_R_Crown_SOA | Frontier Rune Crown (Leader) |
| 400991 | Frontier_R_Crown_HN | Frontier Rune Crown (Hyper Novice) |
| 400992 | Frontier_R_Crown_SH | Frontier Rune Crown (Spirit Master) |
| 401000 | aegis_401000 | Costume Liamette Hair Band |
| 401001 | aegis_401001 | Costume Piamette Bonnet |
| 401014 | aegis_401014 | Costume Two-Tone Cap |
| 401055 | Stardust_Crown_SV | Silver Stardust Crown |
| 401056 | Stardust_Crown_SC | Scarlet Stardust Crown |
| 401057 | Stardust_Crown_VI | Violet Stardust Crown |
| 401058 | Sky_Rune_Crown_IG | Celestial Rune Crown (Imperial Guard) |
| 401059 | Sky_Rune_Crown_ABC | Celestial Rune Crown (Abyss Chaser) |
| 401060 | Sky_Rune_Crown_SH | Rune Crown of the Sky (Spiritualist) |
| 401062 | aegis_401062 | Costume Ignis Cap (Red) |
| 401115 | Sky_Rune_Crown_MS | Sky Rune Crown (Meister) |
| 401116 | Sky_Rune_Crown_WH | Sky Rune Crown (Windhawk) |
| 401117 | Sky_Rune_Crown_HN | Sky Rune Crown (Hyper Novice) |
| 401118 | Sky_Rune_Crown_CD | Sky Rune Crown (Cardinal) |
| 401119 | Sky_Rune_Crown_IQ | Sky Rune Crown (Inquisitor) |
| 401120 | Sky_Rune_Crown_SKE | Sky Rune Crown (Sky Emperor) |
| 410280 | aegis_410280 | Costume Niflheim Night Sky |
| 410399 | C_Capybara | Costume Capybara |
| 410430 | C_Blink_Eyes_Forest | Costume Blinking Forest Eyes |
| 410440 | C_CLB_DT_TS_Hat | Costume: Toothless Head |
| 410456 | aegis_410456 | Costume White Cat's Eye |
| 410457 | aegis_410457 | Costume Yellow Cat's Eye |
| 410458 | C_Divine_Twinkling | Costume Divine Twinkling |
| 410471 | aegis_410471 | Costume Gear Monocle |
| 410474 | aegis_410474 | Costume Chained Bear |
| 410491 | aegis_410491 | Costume: Violet Starlight |
| 420351 | C_Auspicloud | Costume Auspicious Clouds |
| 420358 | C_Experiment_Mind | Costume Experiment Mind |
| 420448 | C_Deep_You_N | Costume Abyssal |
| 420449 | C_Deep_You | Costume Abyssal Hair |
| 420511 | C_Over_Cloud | Costume Over the Clouds |
| 420512 | C_Aurora_On_Clouds | Costume Aurora on Clouds |
| 420514 | aegis_420514 | Costume Wonderful Long (No Decoration) |
| 420515 | aegis_420515 | Costume Wonderful Long |
| 420516 | aegis_420516 | Costume Forest Friends |
| 420532 | C_Immortal_H_Power | Costume Immortal Monarch's Might |
| 420552 | C_Divine_Sky_Invite | Costume Divine Invitation |
| 420553 | aegis_420553 | Costume Fluffy Nyar Hair |
| 420554 | C_Waggy_Nyar_Hair | Costume Fluttering Nyar Hair |
| 420570 | aegis_420570 | Costume Winged Twin Hair |
| 420571 | aegis_420571 | Costume Winged Bronze Hair |
| 420575 | aegis_420575 | Costume Piamette Rollhair |
| 420576 | aegis_420576 | Costume Nightmare Chain |
| 420642 | aegis_420642 | Costume Open Air Headphones (Red) |
| 480469 | C_Con_of_Singapura_MSP | Costume Con of Singapura |
| 480556 | C_Blue_Rose_Parasol | Costume Blue Rose Parasol |
| 480566 | C_Immortal_H_Wing | Costume: Immortal Monarch's Wings |
| 480595 | C_CLB_DT_TS_Wing | Costume: Toothless Wings |
| 480596 | C_CLB_DT_TS_Hood | Costume: Toothless Hood |
| 480611 | C_Immortal_H_Spear | Costume: Immortal Monarch's Spear |
| 480616 | C_Qualifier_1st | Costume: Royal Knight's Rune Sword |
| 480617 | C_Qualifier_2nd | Costume: Royal Knight's Greatsword |
| 480618 | C_Qualifier_3rd | Costume: Knight's Greatsword |
| 480627 | aegis_480627 | Costume ROS Victory Robe |
| 480629 | aegis_480629 | Costume Clark Lord |
| 480631 | aegis_480631 | Costume Detective's Magnifying Glass |
| 480632 | aegis_480632 | Costume Mad Bunny Nightmare |
| 480669 | aegis_480669 | Executioner's Cloak |
| 480670 | aegis_480670 | Sharpshooter Muffler |
| 480671 | aegis_480671 | Fighter's Cloak |
| 480672 | aegis_480672 | Champion's Cloak |
| 480673 | aegis_480673 | Scholar's Muffler |
| 480674 | aegis_480674 | Wizard's Cloak |
| 500119 | Encroached_Sword | Encroached Sword |
| 500120 | Falx | Falks |
| 500134 | Sky_Napalm_Sword | Celestial Napalm Sword |
| 510140 | Encroached_Dagger | Encroached Dagger |
| 510192 | Frontier_ABC_Dagger | Frontier Abyss Dagger |
| 510199 | Sky_Chasing_Dagger | Chasing Dagger of the Sky |
| 530071 | Encroached_Spear | Encroached Spear |
| 530072 | Frontier_IG_Spear | Frontier Imperial Spear |
| 530074 | Espetar | Ispetar |
| 530076 | Sky_Imperial_Spear | Imperial Spear of the Sky |
| 540109 | Encroached_Book | Encroached Book |
| 540110 | Frontier_EM_Book | Frontier Elemental Book |
| 540111 | Frontier_SKE_Book | Frontier Emperor Battle Book |
| 540114 | Elemental_Spirits | Elemental Spirits |
| 540115 | Book_Of_Crimson_M | Book of the Red Moon |
| 540119 | Judgment_Day | Judgment Day |
| 540122 | Sky_Moon_Book | Celestial Moonsong Book |
| 550137 | Encroached_Staff | Encroached Staff |
| 550174 | Encroached_Foxtail | Encroached Foxtail |
| 550176 | Frontier_CD_Rod | Frontier Saint Lord |
| 550177 | Frontier_HN_Rod | Frontier Hyper Lord |
| 550178 | Frontier_SH_Foxtail | Frontier Spirit Foxtail |
| 550187 | Sky_Chulho_Foxtail | Foxtail of the Sky |
| 550190 | Sky_Arbi_Rod | Celestial Arby Rod |
| 560080 | Encroached_Knuckle | Encroached Knuckles |
| 560081 | Frontier_IQ_Claw | Frontier Judgment Claw |
| 560086 | Sky_Destroy_Knuckle | Celestial Annihilation |
| 570086 | Encroached_Instrument | Encroached Instrument |
| 570087 | Frontier_TR_Vilolin | Frontier Musical Violin |
| 570090 | Geige | Gaig |
| 580086 | Encroached_Whip | Encroached Whip |
| 580087 | Frontier_TR_Rope | Frontier Musical Rope |
| 580090 | Needle_Whip | Needle Whip |
| 590081 | Encroached_Mace | Encroached Mace |
| 590107 | Frontier_BO_Hall | Frontier Biological Scepter |
| 590111 | Submarine_Anchor | Submarine Anchor |
| 590112 | Jack_O_Rush | Jack O' Rush |
| 600056 | Encroached_T_Sword | Encroached Two-Handed Sword |
| 600071 | Frontier_DK_T_Sword | Frontier Dragon Sword |
| 610084 | Encroached_Katar | Encroached Katar |
| 610085 | Frontier_SHC_Katar | Frontier Shadow Katar |
| 610089 | Vida_Nocturno | Vida Noctorno |
| 620038 | Encroached_T_Axe | Encroached Two-Handed Axe |
| 620058 | Frontier_MT_T_Axe | Frontier Mechanical Axe |
| 630059 | Encroached_T_Spear | Encroached Two-Handed Spear |
| 630060 | Face_W_Q_Horn | Faceworm Queen's Horn |
| 640051 | Encroached_T_Staff | Encroached Two-Handed Staff |
| 640064 | Frontier_AG_Staff | Frontier Arc Staff |
| 640065 | Frontier_SOA_Staff | Frontier Soul Staff |
| 640067 | Wepawet | Wepawet |
| 650048 | Encroached_Humma | Encroached Huuma Shuriken |
| 650058 | Frontier_SS_Humma | Frontier Moonlight Fūma Shuriken |
| 700117 | Encroached_Bow | Encroached Bow |
| 700119 | Frontier_WH_Bow | Frontier Wind Bow |
| 700121 | Beargun_Crossbow | Beargun Crossbow |
| 700125 | Sky_Crescive_Bow | Celestial Crescent Bow |
| 810048 | Encroached_Rifle | Encroached Firearm |
| 810049 | Frontier_NW_Rifle | Frontier Knight Rifle |
| 840039 | Agent_Launcher | Agent Launcher |
| 1270079 | S_SHC_CR_Earring | Crater Shadow Earring |
| 1270080 | S_SHC_CR_Pendant | Crater Shadow Pendant |
| 1270081 | S_SHC_ST_Armor | Stab Shadow Armor |
| 1270082 | S_SHC_ST_Shoes | Stab Shadow Shoes |
| 1270083 | S_IQ_TP_Earring | Punish Shadow Earring |
| 1270084 | S_IQ_TP_Pendant | Punish Shadow Pendant |
| 1270085 | S_IQ_FB_Armor | Flame Bomb Shadow Armor |
| 1270086 | S_IQ_FB_Shoes | Flame Bomb Shadow Shoes |
| 1270087 | S_HN_MC_Earring | Max Chain Shadow Earring |
| 1270088 | S_HN_MC_Pendant | Max Chain Shadow Pendant |
| 1270089 | S_HN_DB_Armor | Double Blow Shadow Armor |
| 1270090 | S_HN_DB_Shoes | Double Blow Shadow Shoes |
| 1270091 | S_AG_CI_Earring | Crystal Illusion Shadow Earring |
| 1270092 | S_AG_CI_Pendant | Crystal Illusion Shadow Pendant |
| 1270093 | S_AG_VST_Armor | Violent Soul Tremor Shadow Armor |
| 1270094 | S_AG_VST_Shoes | Violent Soul Tremor Shadow Shoes |
| 1270095 | S_ABC_DB_Earring | Deft Breaker Shadow Earring |
| 1270096 | S_ABC_DB_Pendant | Deft Breaker Shadow Pendant |
| 1270097 | S_ABC_FR_Armor | Frenzy Reaction Shot Shadow Armor |
| 1270098 | S_ABC_FR_Shoes | Frenzy Reaction Shot Shadow Shoes |
| 1270099 | S_SKE_MS_Earring | Midnight Kick Shadow Earring |
| 1270100 | S_SKE_MS_Pendant | Midnight Kick Shadow Pendant |
| 1270101 | S_SKE_DB_Armor | Dawn Break Shot Shadow Armor |
| 1270102 | S_SKE_DB_Shoes | Dawn Break Shadow Shoes |
| 1270115 | S_CD_FP_Earring | Fracella Shadow Earring |
| 1270116 | S_CD_FP_Pendant | Fracella Shadow Pendant |
| 1270117 | S_CD_EP_Armor | Effltio Shadow Armor |
| 1270118 | S_CD_EP_Shoes | Effltio Shadow Shoes |
| 1270119 | S_EM_DS_Earring | Diamond Shadow Earring |
| 1270120 | S_EM_DS_Pendant | Diamond Shadow Pendant |
| 1270121 | S_EM_TP_Armor | Terra Stream Shadow Armor |
| 1270122 | S_EM_TP_Shoes | Terra Stream Shadow Shoes |
| 1270123 | S_SS_KK_Earring | Shadow Dance Shadow Earring |
| 1270124 | S_SS_KK_Pendant | Shadow Dance Shadow Pendant |
| 1270125 | S_SS_KF_Armor | Kunai Shuriken Shadow Armor |
| 1270126 | S_SS_KF_Shoes | Kunai Shuriken Shadow Shoes |
| 1270130 | S_WH_WH_Earring | Wild Hawk Shadow Earring |
| 1270131 | S_WH_WH_Pendant | Wild Hawk Shadow Pendant |
| 1270132 | S_WH_AT_Armor | Advanced Trap Shadow Armor |
| 1270133 | S_WH_AT_Shoes | Advanced Trap Shadow Shoes |
| 1270134 | S_TR_MS_Earring | Musical Shooting Shadow Earring |
| 1270135 | S_TR_MS_Pendant | Musical Shooting Shadow Pendant |
| 1270136 | S_TR_RB_Armor | Blossom Shadow Armor |
| 1270137 | S_TR_RB_Shoes | Blossom Shadow Shoes |
| 1270138 | S_NW_MS_Earring | Midnight Shooting Shadow Earring |
| 1270139 | S_NW_MS_Pendant | Midnight Shooting Shadow Pendant |
| 1270140 | S_NW_NF_Armor | Night Fire Shadow Armor |
| 1270141 | S_NW_NF_Shoes | Night Fire Shadow Shoes |

<!-- RAG_CHUNK: 17_Complete_Usable_Items_Jan2026 -->
## Part 17 Detail: Complete New Usable Items (January 2026)

**Total: 158 usable items**

| ID | AegisName | Name |
|-----|-----------|------|
| 14622 | aegis_14622 | Cherry Blossom Scroll |
| 100582 | aegis_100582 | Test 1 |
| 100584 | aegis_100584 | Test 2 |
| 103218 | aegis_103218 | Angel's Song |
| 103219 | aegis_103219 | Clock Lubricant |
| 104714 | C_CLB_DT_Select_Box1 | Toothless Selection Box I |
| 104715 | C_CLB_DT_Select_Box2 | Toothless Selection Box II |
| 104716 | C_Clouds_Select_Box | Cloud Costume Selection Box |
| 104741 | Rt_Ch01_Armor_A | Entwined Magical Equipment Activation Reward |
| 104742 | Rt_Ch01_Armor_C | Entwined Magical Equipment Completion Reward |
| 104743 | Rt_Ch01_Dimen_A | Footsteps of Dimension Activation Reward |
| 104744 | Rt_Ch01_Dimen_C | Footsteps of Dimension Completion Reward |
| 104745 | Rt_Ch01_Dimen_3 | Footsteps of Dimension 3 Sets Reward |
| 104746 | Rt_Ch01_Extra_A | Chaos Activation Reward |
| 104747 | Rt_Ch01_Extra_C | Chaos Completion Reward |
| 104748 | Rt_Ch01_Extra_2 | Chaos 2 Sets Reward |
| 104749 | Rt_Ch01_Extra_4 | Chaos 4 Sets Reward |
| 104750 | Rt_Ch01_Extra_5 | Chaos 5 Sets Reward |
| 104901 | aegis_104901 | Costume Enchant Stone Box 40 |
| 105031 | aegis_105031 | ROS Gold Capsule |
| 105045 | 23th_Costume_A | Fluffy Costume Gift Box |
| 105046 | 23th_Costume_B | Fluttering Costume Gift Box |
| 105047 | 23th_Costume_C | Divine Costume Gift Box |
| 105059 | aegis_105059 | Special Enchant Stone Box |
| 105161 | aegis_105161 | Tangled Singularity |
| 105162 | aegis_105162 | Boundary Singularity |
| 105163 | Fron_Fix_DK_T_Sword | Boundary Tuning (Frontier Dragon Sword) |
| 105164 | Fron_Fix_IG_Spear | Boundary Tuning (Frontier Imperial Spear) |
| 105165 | Fron_Fix_MT_T_Axe | Boundary Tuning (Frontier Mechanical Axe) |
| 105166 | Fron_Fix_BO_Hall | Boundary Tuning (Frontier Biological Hall) |
| 105167 | Fron_Fix_SHC_Katar | Boundary Tuning (Frontier Shadow Katar) |
| 105168 | Fron_Fix_ABC_Dagger | Boundary Tuning (Frontier Abyss Dagger) |
| 105169 | Fron_Fix_AG_Staff | Boundary Tuning (Frontier Arc Staff) |
| 105170 | Fron_Fix_EM_Book | Boundary Tuning (Frontier Elemental Book) |
| 105171 | Fron_Fix_CD_Rod | Boundary Tuning (Frontier Saint Lord) |
| 105172 | Fron_Fix_IQ_Claw | Boundary Tuning (Frontier Judgment Claw) |
| 105173 | Fron_Fix_WH_Bow | Boundary Tuning (Frontier Wind Bow) |
| 105174 | Fron_Fix_TR_Vilolin | Boundary Tuning (Frontier Musical Violin) |
| 105175 | Fron_Fix_TR_Rope | Tuning of the Boundary (Frontier Musical Rope) |
| 105176 | Fron_Fix_SS_Humma | Tuning of the Boundary (Frontier Moonlight Fuma S |
| 105177 | Fron_Fix_NW_Rifle | Tuning of the Boundary (Frontier Knight Rifle) |
| 105178 | Fron_Fix_SKE_Book | Tuning of the Boundary (Frontier Emperor Battle B |
| 105179 | Fron_Fix_SOA_Staff | Tuning of the Boundary (Frontier Soul Staff) |
| 105180 | Fron_Fix_HN_Rod | Tuning of the Boundary (Frontier Hyper Rod) |
| 105181 | Fron_Fix_SH_Foxtail | Tuning of the Boundary (Frontier Spirit Foxtail) |
| 105219 | aegis_105219 | [A] Wrathful Two-Handed Dagger Box |
| 105220 | aegis_105220 | [A] Wrathful Spear Shield Box |
| 105356 | SP_Costume_Select | Special Costume Selection Box |
| 105357 | SP_Costume_Collection | Special Costume Collection Box |
| 105415 | A_DM_Fix_DK_T_Spear | Tuning of the Dimension (Faceworm Queen's Horn) |
| 105416 | A_DM_Fix_IG_Spear | Dimensional Tuning (Ispetar) |
| 105417 | A_DM_Fix_ABC_Bow | Dimensional Tuning (Baregun Crossbow) |
| 105418 | A_DM_Fix_BO_Sword | Second-Dimensional Tuning (Falx) |
| 105419 | A_DM_Fix_AG_T_Staff | Second-Dimensional Tuning (Wepawet) |
| 105420 | A_DM_Fix_EM_Book | Second-Dimensional Tuning (Elemental Spirits) |
| 105421 | A_DM_Fix_NW_Launcher | Second-Dimensional Tuning (Agent Launcher) |
| 105422 | A_DM_Fix_SKE_Book | Second-Dimensional Tuning (Book of the Red Moon) |
| 105488 | All_In_One_Healing_E | [Event] All-in-One Healing Potion |
| 105489 | All_In_One_buff_E | [Event] All-in-One Buff Potion |
| 105490 | 2025ROS_For_Offline | ROS Gift Box |
| 105518 | aegis_105518 | Costume Enchantment Stone Box 41 |
| 105526 | Niflheim_Select_1 | Niflheim Costume Selection 1 |
| 105527 | Niflheim_Select_2 | Niflheim Costume Selection 2 |
| 105528 | Niflheim_Select_3 | Niflheim Costume Selection 3 |
| 105615 | ROS_FESTA_BOX | ROS FESTA BOX |
| 105616 | R_Ep1921_Album | Episode 19-21 Card Album |
| 105617 | R_Ep1921_Boss | Episode 19-21 Boss Card Album |
| 105619 | Rt_Ep21_Gaebolg_A | Geoborg Activation Reward |
| 105620 | Rt_Ep21_Gaebolg_C | Geoborg Completion Reward |
| 105621 | Rt_Ep21_Icy_A | Ice Coast Activation Reward |
| 105622 | Rt_Ep21_Icy_C | Ice Coast Completion Reward |
| 105623 | Rt_Ep21_Icy_2 | Ice Coast 2-Set Reward |
| 105624 | Rt_Ep21_Yorker_A | Yosker Yorker Activation Reward |
| 105625 | Rt_Ep21_Yorker_C | Yosker Yorker Completion Reward |
| 105626 | Rt_Ep21_Working_A | Staff Activation Reward |
| 105627 | Rt_Ep21_Working_C | Staff Completion Reward |
| 105628 | Rt_Ep21_Admin_A | Management Activation Reward |
| 105629 | Rt_Ep21_Admin_C | Management Completion Reward |
| 105630 | Rt_Ep21_Admin_2 | Management 2-Set Reward |
| 105631 | Rt_Ep21_Purify_A | Purification Activity Activation Reward |
| 105632 | Rt_Ep21_Purify_C | Purification Activity Completion Rewards |
| 105633 | Rt_Ep21_Purify_3 | Purification Activity 3-Set Reward |
| 105634 | Rt_Ep21_Purify_5 | Purification Activity 5-Set Reward |
| 105635 | Rt_Ep21_Aid_A | Civil Support Activation Reward |
| 105636 | Rt_Ep21_Aid_C | Civil Support Completion Reward |
| 105637 | Rt_Ep21_Aid_2 | Civil Support 2-Set Reward |
| 105638 | Rt_Ep21_Aid_4 | Civil Support 4-Set Reward |
| 105639 | Rt_Ep21_Company_A | Group Activation Reward |
| 105640 | Rt_Ep21_Company_C | Group Completion Reward |
| 105641 | Rt_Ep21_Company_3 | Group 3-Set Reward |
| 105642 | Rt_Ep21_Company_5 | Group 5-Set Reward |
| 105643 | Rt_Ep21_Horn_A | Frozen Horn Activation Reward |
| 105644 | Rt_Ep21_Horn_C | Frozen Horn Completion Reward |
| 105645 | Rt_Ep21_Horn_3 | Frozen Horn 3-Set Reward |
| 105646 | Rt_Ep21_Horn_5 | Frozen Horn 5-Set Reward |
| 105647 | Rt_Ep21_Tan_A | Encroachment Activation Reward |
| 105648 | Rt_Ep21_Tan_C | Encroachment Completion Reward |
| 105685 | A_DM_Fix_MT_Mace | Second Dimensional Tuning (Submarine Anchor) |
| 105686 | A_DM_Fix_SHC_Katar | Second Dimensional Tuning (Vida Noctorno) |
| 105687 | A_DM_Fix_CD_Book | Second Dimensional Tuning (Judgment Day) |
| 105688 | A_DM_Fix_TR_Violin | Second Dimensional Tuning (Geigg) |
| 105689 | A_DM_Fix_TR_Whip | Second Dimensional Tuning (Needle Whip) |
| 105690 | A_DM_Fix_HN_Mace | Second Dimensional Tuning (Jack O'Rush) |
| 105715 | aegis_105715 | Infinite Giant Fly's Wings 1-Hour Box |
| 105737 | Sky_Weapon_Hammer | Celestial Weapon Refining Hammer |
| 105738 | Sky_Crown_Hammer | Celestial Crown Refining Hammer |
| 105828 | aegis_105828 | [A] Time Gap Dagger Box |
| 105829 | aegis_105829 | [A] Time Gap Kurojin Boxes |
| 105830 | aegis_105830 | +12 [A] Crown of Good and Evil (Night's Watch) Se |
| 105831 | aegis_105831 | +10 [C] Crown of Good and Evil (Night's Watch) Se |
| 105832 | aegis_105832 | +12 [A] Spear of Wrath Shield Box |
| 105833 | aegis_105833 | +10 [C] Spear of Wrath Shield Box |
| 105834 | aegis_105834 | +12 [A] Two-Handed Dagger of Wrath Box |
| 105835 | aegis_105835 | +10 [C] Two-Handed Dagger of Wrath Box |
| 105836 | aegis_105836 | Holiday Season Gift |
| 105917 | aegis_105917 | Divine Box |
| 105927 | Select_Costume_DEC_1 | White Fox Hooded Twin Costume Selection Box |
| 105928 | Select_Costume_DEC_2 | Winged Hair Costume Selection Box |
| 105929 | Select_Costume_DEC_3 | Wonderful Long Costume Selection Box |
| 200665 | DT_Colabo_Box1 | Toothless Costume Package I |
| 200666 | DT_Colabo_Box2 | Toothless Costume Package II |
| 200667 | Cloud_Costume_Pack | Cloud Costume Package |
| 200669 | CostumeMilePack_39_1 | Nyangdarae Costume Mileage Package I (Stone Box 3 |
| 200670 | CostumeMilePack_39_2 | Nyangdarae Costume Mileage Package II (Stone Box |
| 200671 | CostumeMilePack_39_3 | Nyangdarae Costume Mileage Package III (Stone Box |
| 200700 | LI_Nyangvine_Box1_40 | (Account Exclusive) Cat's Nest Fruit Package I (S |
| 200701 | LI_Nyangvine_Box2_40 | (Account Exclusive) Cat's Nest Fruit Package II ( |
| 200702 | LI_Nyangvine_Box3_40 | (Account Exclusive) Cat's Nest Fruit Package III |
| 200713 | 23th_Costume_Pack_A | Fluffy Concentrated Refining Package |
| 200714 | 23th_Costume_Pack_B | Fluttering High-Concentrated Refining Package |
| 200715 | 23th_Costume_Pack_C | Sacred Cat's Nest Fruit Packages |
| 200716 | 23th_Package_1 | Special Monthly Package I |
| 200717 | 23th_Package_2 | Special Monthly Package II |
| 200718 | 23th_Package_3 | Special Monthly Package III |
| 200719 | 23th_Package_4 | Special Monthly Package IV |
| 200721 | CostumeMilePack_SP_1 | Nyangdarae Costume Mileage Package I (Special) |
| 200722 | CostumeMilePack_SP_2 | Nyangdarae Costume Mileage Package II (Special) |
| 200723 | CostumeMilePack_SP_3 | Nyangdarae Costume Mileage Package III (Special) |
| 200724 | CostumeMilePack_SP_4 | Nyangdarae Costume Mileage Package (Special) |
| 200764 | CostumeMilePack_41_1 | Nymphalina Costume Mileage Package I (Stone Box 4 |
| 200765 | CostumeMilePack_41_2 | Nymphalina Costume Mileage Package II (Stone Box |
| 200766 | CostumeMilePack_41_3 | Nymphalina Costume Mileage Package III (Stone Box |
| 200767 | Niflheim_Costume_1 | Niflheim Costume Package I |
| 200768 | Niflheim_Costume_2 | Niflheim Costume Package II |
| 200769 | Niflheim_Costume_3 | Niflheim Costume Package III |
| 200770 | Niflheim_Costume_4 | Niflheim Night Sky Package |
| 200785 | LI_Nyangvine_Box1_SP | Cat's Nest Fruit Special Package |
| 200786 | LI_Nyangvine_Box2_SP | Cat's Nest Fruit Special Package I |
| 200787 | LI_Nyangvine_Box3_SP | Cat's Nest Fruit Special Package II |
| 200788 | LI_Nyangvine_Box4_SP | Nyandarae Fruit Special Package III |
| 200789 | 2025_DEC_Package1 | Special Refining Month Package I |
| 200790 | 2025_DEC_Package2 | Special Refining Month Package II |
| 200791 | Cash_Booster_Box2 | Special Year-End Growth Package |
| 200792 | Select_DEC_Pack1 | White Fox Costume Package |
| 200793 | Select_DEC_Pack2 | Clock Witch Costume Package |
| 200794 | Select_DEC_Pack3 | Wonderful Forest Costume Package |
| 1100036 | aegis_1100036 | Sharing Fish |
| 1100037 | 25_A_Ev_Cookie | Orleans' Handmade Cookies |

<!-- RAG_CHUNK: 18_Complete_Etc_Items_Jan2026 -->
## Part 18 Detail: Complete New Etc Items (January 2026)

**Total: 160 etc items (cards, stones, footprints)**

| ID | AegisName | Name |
|-----|-----------|------|
| 300715 | aegis_300715 | As Card |
| 300716 | aegis_300716 | Kaya Toss Card |
| 300717 | aegis_300717 | Tatio Card |
| 300718 | aegis_300718 | Chairman Rekenber Card |
| 300719 | aegis_300719 | As Card |
| 300720 | aegis_300720 | Rekenber Kaya Toss Card |
| 300721 | aegis_300721 | Rekenber Tatio Card |
| 300722 | aegis_300722 | Rekenber Chairman Rekenber Card |
| 313956 | Butterfly_purple_Foot | Purple Butterfly Footprints |
| 313957 | Butterfly_yellow_Foot | Yellow Butterfly Footprints |
| 314066 | aegis_314066 | ROS2025 Commemorative Footprints |
| 314094 | aegis_314094 | Blue Fighting Spirit Effect |
| 314095 | aegis_314095 | Red Fighting Spirit Effect |
| 314171 | aegis_314171 | Footprint (2D) |
| 314172 | aegis_314172 | Footprint (3D) |
| 314181 | aegis_314181 | Archbishop Stone II (Upper) |
| 314182 | aegis_314182 | Archbishop Stone II (Middle) |
| 314183 | aegis_314183 | Archbishop Stone II (Lower) |
| 314184 | aegis_314184 | Cardinal Stone II (Garment) |
| 314185 | aegis_314185 | Shadow Chaser Stone II (Upper) |
| 314186 | aegis_314186 | Shadow Chaser Stone II (Middle) |
| 314187 | aegis_314187 | Shadow Chaser Stone II (Lower) |
| 314188 | aegis_314188 | Abyss Chaser Stone II (Garment) |
| 314189 | aegis_314189 | Super Novice Stone II (Upper) |
| 314190 | aegis_314190 | Super Novice Stone II (Middle) |
| 314191 | aegis_314191 | Super Novice Stone II (Lower) |
| 314192 | aegis_314192 | Hyper Novice Stone II (Garment) |
| 314212 | Nyar_Foot_BU | Nyar's Blue Footprints |
| 314213 | Nyar_Foot_PP | Nyar's Purple Footprints |
| 314214 | Divine_Light_Foot | Divine Light Footprints |
| 314230 | Ch01_1_Fighter | Frontier Spell (Fighter) |
| 314231 | Ch01_2_Fighter2 | Frontier Spell (Special Force) |
| 314232 | Ch01_3_Hit_Attack | Frontier Spell (Hit Attack) |
| 314233 | Ch01_3_Special_Agent | Frontier Spell (Special Agent) |
| 314243 | T_D_Jewel_POW_1 | Time Dimension Jewel (Strength) 1Lv |
| 314244 | T_D_Jewel_POW_2 | Time Dimension Jewel (Strength) 2Lv |
| 314245 | T_D_Jewel_POW_3 | Time Dimension Jewel (Strength) 3Lv |
| 314246 | T_D_Jewel_CON_1 | Lv1 Time-Space Jewel (Concentration) |
| 314247 | T_D_Jewel_CON_2 | Lv2 Time-Space Jewel (Concentration) |
| 314248 | T_D_Jewel_CON_3 | Lv3 Time-Space Jewel (Concentration) |
| 314249 | Fierce_A_Jewel_1 | Fierce Attack Jewel 1Lv |
| 314250 | Fierce_A_Jewel_2 | Fierce Attack Jewel 2Lv |
| 314251 | Fierce_A_Jewel_3 | Fierce Attack Jewel 3Lv |
| 314252 | Fierce_A_Jewel_4 | Fierce Attack Jewel 4Lv |
| 314253 | Fierce_A_Jewel_5 | Fierce Attack Jewel 5Lv |
| 314254 | Fierce_A_Jewel_6 | Fierce Attack Jewel 6Lv |
| 314255 | Fierce_A_Jewel_7 | Fierce Attack Jewel 7Lv |
| 314256 | Fierce_A_Jewel_8 | Fierce Attack Jewel 8Lv |
| 314257 | Fierce_A_Jewel_9 | Fierce Attack Jewel 9Lv |
| 314258 | Fierce_A_Jewel_10 | Fierce Attack Jewel 10Lv |
| 314259 | Great_C_Jewel_1 | Great Craftsman Jewel 1Lv |
| 314260 | Great_C_Jewel_2 | Great Craftsman Jewel 2Lv |
| 314261 | Great_C_Jewel_3 | Great Craftsman Jewel 3Lv |
| 314262 | Great_C_Jewel_4 | Great Craftsman Jewel 4Lv |
| 314263 | Great_C_Jewel_5 | Great Craftsman Jewel 5Lv |
| 314264 | Great_C_Jewel_6 | Great Craftsman Jewel 6Lv |
| 314265 | Great_C_Jewel_7 | Great Craftsman Jewel 7Lv |
| 314266 | Great_C_Jewel_8 | Great Craftsman Jewel 8Lv |
| 314267 | Great_C_Jewel_9 | Great Craftsman Jewel 9Lv |
| 314268 | Great_C_Jewel_10 | Great Craftsman Jewel 10Lv |
| 314661 | aegis_314661 | Hit Physical Stone (Dual) |
| 314662 | aegis_314662 | Hit Physical Stone (Upper) |
| 314663 | aegis_314663 | Hit Physical Stone (Middle) |
| 314664 | aegis_314664 | Hit Physical Stone (Lower) |
| 314665 | aegis_314665 | Hit Physical Stone (Garment) |
| 314666 | aegis_314666 | Experience Stone (Garment) |
| 314667 | aegis_314667 | Archmage Stone II (Garment) |
| 314668 | aegis_314668 | Biolo Stone II (Garment) |
| 314669 | aegis_314669 | Celestial Stone II (Garment) |
| 314670 | aegis_314670 | Warlock Stone II (Upper) |
| 314671 | aegis_314671 | Warlock Stone II (Middle) |
| 314672 | aegis_314672 | Warlock Stone II (Lower) |
| 314673 | aegis_314673 | Generic Stone II (Upper) |
| 314674 | aegis_314674 | Generic Stone II (Middle) |
| 314675 | aegis_314675 | Generic Stone II (Lower) |
| 314676 | aegis_314676 | Holy Emperor Stone II (Upper) |
| 314677 | aegis_314677 | Holy Emperor Stone II (Middle) |
| 314678 | aegis_314678 | Holy Emperor Stone II (Lower) |
| 1001215 | EpisodClear21 | Eps 21 Clear Ticket |
| 1002185 | Summer_Leaflet | Ocean Week Flyer |
| 1002186 | ROS_Pre_Certificate | ROS Representative Tournament Participation Certi |
| 1002187 | Gu_5LvWeapon_13Up_ROS | Level 5 Weapon 13 Refinement Guaranteed Ticket [R |
| 1002188 | Gu_2LvArmor_13Up_ROS | Guaranteed Ticket for 2Lv Armor 13 Refining [ROS] |
| 1002189 | Gu_5LvWeapon_14Up_ROS | Guaranteed Ticket for 5Lv Weapon 14 Refining [ROS |
| 1002190 | Gu_2LvArmor_14Up_ROS | Guaranteed Ticket for 2Lv Armor 14 Refining [ROS] |
| 1002191 | Gu_5LvWeapon_15Up_ROS | Guaranteed Ticket for 5Lv Weapon 15 Refining [ROS |
| 1002192 | Gu_2LvArmor_15Up_ROS | Guaranteed Ticket for 2Lv Armor 15 Refining [ROS] |
| 1002193 | ROS_BlueEffect_Middle | Blue Fighting Spirit Effect (Mid) |
| 1002194 | ROS_RedEffect_Middle | Red Fighting Spirit Effect (Mid) |
| 1002224 | CLB_DT_Ticket | [Collab] Viking Mark |
| 1002239 | CLB_DT_2D_Foot_Robe | Footprint (2D) (Garment) |
| 1002240 | CLB_DT_3D_Foot_Robe | Footprint (3D) (Garment) |
| 1002243 | R_Entwined_Armor | Printed Entwined Magical Armor |
| 1002244 | R_Entwined_Robe | Printed Entwined Magical Robe |
| 1002245 | R_Entwined_Manteau | Printed Entwined Magical Manteau |
| 1002246 | R_Entwined_Muffler | Printed Entwined Magical Muffler |
| 1002247 | R_Entwined_Boots | Printed Entwined Magical Boots |
| 1002248 | R_Dimension_B_Greave | Printed Dimension World Battle Greaves |
| 1002249 | R_Dimension_H_Boots | Printed Dimension World Hunting Boots |
| 1002250 | R_Dimension_S_Shoes | Printed Dimension World Spell Shoes |
| 1002251 | R_Dimension_M_Shoes | Printed Dimension World Magic Shoes |
| 1002252 | R_Dimension_E_Boots | Printed Dimension World Executioner Boots |
| 1002253 | R_Entwined_Shoes | Printed Entwined Magical Shoes |
| 1002273 | aegis_1002273 | Archbishop Stone II (Upper) |
| 1002274 | aegis_1002274 | Archbishop Stone II (Middle) |
| 1002275 | aegis_1002275 | Archbishop Stone II (Lower) |
| 1002276 | aegis_1002276 | Cardinal Stone II (Garment) |
| 1002277 | aegis_1002277 | Shadow Chaser Stone II (Upper) |
| 1002278 | aegis_1002278 | Shadow Chaser Stone II (Middle) |
| 1002279 | aegis_1002279 | Shadow Chaser Stone II (Lower) |
| 1002280 | aegis_1002280 | Abyss Chaser Stone II (Garment) |
| 1002281 | aegis_1002281 | Super Novice Stone II (Upper) |
| 1002282 | aegis_1002282 | Super Novice Stone II (Middle) |
| 1002283 | aegis_1002283 | Super Novice Stone II (Lower) |
| 1002284 | aegis_1002284 | Hyper Novice Stone II (Garment) |
| 1002285 | Butter_Purple_foot_Robe | Purple Butterfly Footprints (Garment) |
| 1002286 | ROS2025Vic_Foot_Robe | ROS2025 Commemorative Footprints (Garment) |
| 1002289 | aegis_1002289 | ROS Gold Coin |
| 1002290 | aegis_1002290 | ROS Coin |
| 1002294 | Nyar_Foot_BU_Robe | Nyar's Blue Footprints (Garment) |
| 1002295 | Nyar_Foot_PP_Robe | Nyar's Purple Footprints (Garment) |
| 1002296 | Divine_L_Foot_Robe | Divine Light Footprints (Garments |
| 1002331 | Physical_TuningScroll | Physical Magic Tuning Formula |
| 1002332 | Magical_TuningScroll | Magic Tuning Formula |
| 1002333 | Tiem_SpellScroll | Time Magic Scroll |
| 1002334 | Dimansion_SpellScroll | Dimensional Magic Scroll |
| 1002335 | Pure_SpellScoll | Pure Magic Scroll |
| 1002336 | Polluted_SpellScroll | Contaminated Magic Book |
| 1002337 | Immortal_SpellScroll | Immortal Magic Book |
| 1002356 | 25_A_Ev_Photo | Landscape Photo |
| 1002394 | aegis_1002394 | Yellow Butterfly Footprints (Garment) |
| 1002395 | aegis_1002395 | Hit Physical Stone (Dual) |
| 1002396 | aegis_1002396 | Hit Physical Stone (Upper) |
| 1002397 | aegis_1002397 | Hit Physical Stone (Middle) |
| 1002398 | aegis_1002398 | Hit Physical Stone (Lower) |
| 1002399 | aegis_1002399 | Hit Physical Stone (Garment) |
| 1002404 | aegis_1002404 | Experience Stone (Garment) |
| 1002405 | aegis_1002405 | Archmage Stone II (Garment) |
| 1002406 | aegis_1002406 | Biolo Stone II (Garment) |
| 1002407 | aegis_1002407 | Celestial Stone II (Garment) |
| 1002408 | aegis_1002408 | Warlock Stone II (Upper) |
| 1002409 | aegis_1002409 | Warlock Stone II (Middle) |
| 1002410 | aegis_1002410 | Warlock Stone II (Lower) |
| 1002411 | aegis_1002411 | Generic Stone II (Upper) |
| 1002412 | aegis_1002412 | Generic Stone II (Middle) |
| 1002413 | aegis_1002413 | Generic Stone II (Lower) |
| 1002414 | aegis_1002414 | Holy Stone II (Upper) |
| 1002415 | aegis_1002415 | Holy Stone II (Middle) |
| 1002416 | aegis_1002416 | Holy Stone II (Lower) |
| 1002442 | D_EpisodClear21 | Episode 21 Pass Ticket |
| 1002473 | R_Gaebolg_Armor | Engraved Gaebolg Armor |
| 1002474 | R_Gaebolg_Robe | Engraved Gaebolg Robe |
| 1002475 | R_Gaebolg_Manteau | Engraved Gaebolg Cloak |
| 1002476 | R_Gaebolg_Muffler | Engraved Gaebolg Muffler |
| 1002477 | R_Gaebolg_Boots | Engraved Gaebolg Boots |
| 1002478 | R_Gaebolg_Shoes | Engraved Gaebolg Shoes |
| 1002479 | R_Gaebolg_Ring | Engraved Gaebolg Ring |
| 1002480 | R_Gaebolg_Glove | Engraved Gaebolg Gloves |
| 1002481 | R_Gaebolg_Earring | Engraved Gaebolg Earrings |
| 1002482 | R_Gaebolg_Necklace | Engraved Gaebolg Necklace |

<!-- RAG_CHUNK: 19_Complete_Training_Mobs_Jan2026 -->
## Part 17 Detail: Complete Training Zone Mobs (January 2026)

**Total: 144 training dummies for map 123**

### Training System
- **Map:** 123 (Training Ground)
- **Categories:** Size (S/M/L/XL), Resistance, Race, Element

| ID | AegisName | Name |
|-----|-----------|------|
| 21087 | S_DUMMY_100_HUMANP | Dummy (Human Player) |
| 21088 | S_DUMMY_100_DORAMP | Dummy (Doram Player) |
| 22551 | S_DUMMY_SMALL_R10 | Dummy (Small) |
| 22552 | S_DUMMY_MEDIUM_R10 | Dummy (Medium) |
| 22553 | S_DUMMY_LARGE_R10 | Dummy (Large) |
| 22554 | S_DUMMY_XLARGE_R40 | Dummy (Extra Large) |
| 22555 | S_DUMMY_SMALL_R20 | Dummy (Small) |
| 22556 | S_DUMMY_MEDIUM_R20 | Dummy (Medium) |
| 22557 | S_DUMMY_LARGE_R20 | Dummy (Large) |
| 22558 | S_DUMMY_XLARGE_R50 | Dummy (Extra Large) |
| 22559 | S_DUMMY_SMALL_R30 | Dummy (Small) |
| 22560 | S_DUMMY_MEDIUM_R30 | Dummy (Medium) |
| 22561 | S_DUMMY_SMALL1 | Dummy (Small) |
| 22562 | S_DUMMY_MEDIUM1 | Dummy (Medium) |
| 22563 | S_DUMMY_LARGE1 | Dummy (Large) |
| 22564 | S_DUMMY_SMALL1_R10 | Dummy (Small) |
| 22565 | S_DUMMY_MEDIUM1_R10 | Dummy (Medium) |
| 22566 | S_DUMMY_LARGE1_R10 | Dummy (Large) |
| 22567 | S_DUMMY_XLARGE1_R40 | Dummy (Extra Large) |
| 22568 | S_DUMMY_SMALL1_R20 | Dummy (Small) |
| 22569 | S_DUMMY_MEDIUM1_R20 | Dummy (Medium) |
| 22570 | S_DUMMY_LARGE1_R20 | Dummy (Large) |
| 22571 | S_DUMMY_XLARGE1_R50 | Dummy (Extra Large) |
| 22572 | S_DUMMY_SMALL1_R30 | Dummy (Small) |
| 22573 | S_DUMMY_MEDIUM1_R30 | Dummy (Medium) |
| 22574 | S_DUMMY_LARGE1_R30 | Dummy (Large) |
| 22575 | S_DUMMY_SMALL2 | Dummy (Small) |
| 22576 | S_DUMMY_MEDIUM2 | Dummy (Medium) |
| 22577 | S_DUMMY_LARGE2 | Dummy (Large) |
| 22578 | S_DUMMY_SMALL2_R10 | Dummy (Small) |
| 22579 | S_DUMMY_MEDIUM2_R10 | Dummy (Medium) |
| 22580 | S_DUMMY_LARGE2_R10 | Dummy (Large) |
| 22581 | S_DUMMY_XLARGE2_R40 | Dummy (Extra Large) |
| 22582 | S_DUMMY_SMALL2_R20 | Dummy (Small) |
| 22583 | S_DUMMY_MEDIUM2_R20 | Dummy (Medium) |
| 22584 | S_DUMMY_LARGE2_R20 | Dummy (Large) |
| 22585 | S_DUMMY_XLARGE2_R50 | Dummy (Extra Large) |
| 22586 | S_DUMMY_SMALL2_R30 | Dummy (Small) |
| 22587 | S_DUMMY_MEDIUM2_R30 | Dummy (Medium) |
| 22588 | S_DUMMY_LARGE2_R30 | Dummy (Large) |
| 22589 | S_DUMMY_SMALL_M10 | Dummy (Small) |
| 22590 | S_DUMMY_MEDIUM_M10 | Dummy (Medium) |
| 22591 | S_DUMMY_LARGE_M10 | Dummy (Large) |
| 22592 | S_DUMMY_XLARGE_M40 | Dummy (Extra Large) |
| 22593 | S_DUMMY_SMALL_M20 | Dummy (Small) |
| 22594 | S_DUMMY_MEDIUM_M20 | Dummy (Medium) |
| 22595 | S_DUMMY_LARGE_M20 | Dummy (Large) |
| 22596 | S_DUMMY_XLARGE_M50 | Dummy (Extra Large) |
| 22597 | S_DUMMY_SMALL_M30 | Dummy (Small) |
| 22598 | S_DUMMY_MEDIUM_M30 | Dummy (Medium) |
| 22599 | S_DUMMY_LARGE_M30 | Dummy (Large) |
| 22600 | S_DUMMY_SMALL3 | Dummy (Small) |
| 22601 | S_DUMMY_MEDIUM3 | Dummy (Medium) |
| 22602 | S_DUMMY_LARGE3 | Dummy (Large) |
| 22603 | S_DUMMY_SMALL3_M10 | Dummy (Small) |
| 22604 | S_DUMMY_MEDIUM3_M10 | Dummy (Medium) |
| 22605 | S_DUMMY_LARGE3_M10 | Dummy (Large) |
| 22606 | S_DUMMY_XLARGE1_M40 | Dummy (Extra Large) |
| 22607 | S_DUMMY_SMALL3_M20 | Dummy (Small) |
| 22608 | S_DUMMY_MEDIUM3_M20 | Dummy (Medium) |
| 22609 | S_DUMMY_LARGE3_M20 | Dummy (Large) |
| 22610 | S_DUMMY_XLARGE1_M50 | Dummy (Extra Large) |
| 22611 | S_DUMMY_SMALL3_M30 | Dummy (Small) |
| 22612 | S_DUMMY_MEDIUM3_M30 | Dummy (Medium) |
| 22613 | S_DUMMY_LARGE3_M30 | Dummy (Large) |
| 22614 | S_DUMMY_SMALL4 | Dummy (Small) |
| 22615 | S_DUMMY_MEDIUM4 | Dummy (Medium) |
| 22616 | S_DUMMY_LARGE4 | Dummy (Large) |
| 22617 | S_DUMMY_SMALL4_M10 | Dummy (Small) |
| 22618 | S_DUMMY_MEDIUM4_M10 | Dummy (Medium) |
| 22619 | S_DUMMY_LARGE4_M10 | Dummy (Large) |
| 22620 | S_DUMMY_XLARGE2_M40 | Dummy (Extra Large) |
| 22621 | S_DUMMY_SMALL4_M20 | Dummy (Small) |
| 22622 | S_DUMMY_MEDIUM4_M20 | Dummy (Medium) |
| 22623 | S_DUMMY_LARGE4_M20 | Dummy (Large) |
| 22624 | S_DUMMY_XLARGE2_M50 | Dummy (Extra Large) |
| 22625 | S_DUMMY_SMALL4_M30 | Dummy (Small) |
| 22626 | S_DUMMY_MEDIUM4_M30 | Dummy (Medium) |
| 22627 | S_DUMMY_LARGE4_M30 | Dummy (Large) |
| 22628 | S_DUMMY2_NOTHING | Dummy (Formless Race) |
| 22629 | S_DUMMY2_DRAGON | Dummy (Dragon Race) |
| 22630 | S_DUMMY2_ANIMAL | Dummy (Brute Race) |
| 22631 | S_DUMMY2_HUMAN | Dummy (Human Race) |
| 22632 | S_DUMMY2_INSECT | Dummy (Insect Race) |
| 22633 | S_DUMMY2_FISH | Dummy (Fish Race) |
| 22634 | S_DUMMY2_DEMON | Dummy (Demon Race) |
| 22635 | S_DUMMY2_PLANT | Dummy (Plant Race) |
| 22636 | S_DUMMY2_ANGEL | Dummy (Angel Race) |
| 22637 | S_DUMMY2_UNDEAD | Dummy (Undead Race) |
| 22638 | S_DUMMY3_NOTHING | Dummy (Formless Race) |
| 22639 | S_DUMMY3_DRAGON | Dummy (Dragon Race) |
| 22640 | S_DUMMY3_ANIMAL | Dummy (Brute Race) |
| 22641 | S_DUMMY3_HUMAN | Dummy (Human Race) |
| 22642 | S_DUMMY3_INSECT | Dummy (Insect Race) |
| 22643 | S_DUMMY3_FISH | Dummy (Fish Race) |
| 22644 | S_DUMMY3_DEMON | Dummy (Demon Race) |
| 22645 | S_DUMMY3_PLANT | Dummy (Plant Race) |
| 22646 | S_DUMMY3_ANGEL | Dummy (Angel Race) |
| 22647 | S_DUMMY3_UNDEAD | Dummy (Undead Race) |
| 22648 | S_DUMMY2_NOTHING2 | Dummy (Neutral) |
| 22649 | S_DUMMY2_WATER | Dummy (Water) |
| 22650 | S_DUMMY2_GROUND | Dummy (Earth) |
| 22651 | S_DUMMY2_FIRE | Dummy (Fire) |
| 22652 | S_DUMMY2_WIND | Dummy (Wind) |
| 22653 | S_DUMMY2_POISON | Dummy (Poison) |
| 22654 | S_DUMMY2_SAINT | Dummy (Holy) |
| 22655 | S_DUMMY2_DARKNESS | Dummy (Dark) |
| 22656 | S_DUMMY2_TELEKINESIS | Dummy (Ghost) |
| 22657 | S_DUMMY2_UNDEAD2 | Dummy (Undead) |
| 22658 | S_DUMMY3_NOTHING2 | Dummy (Neutral) |
| 22659 | S_DUMMY3_WATER | Dummy (Water) |
| 22660 | S_DUMMY3_GROUND | Dummy (Earth) |
| 22661 | S_DUMMY3_FIRE | Dummy (Fire) |
| 22662 | S_DUMMY3_WIND | Dummy (Wind) |
| 22663 | S_DUMMY3_POISON | Dummy (Poison) |
| 22664 | S_DUMMY3_SAINT | Dummy (Holy) |
| 22665 | S_DUMMY3_DARKNESS | Dummy (Dark) |
| 22666 | S_DUMMY3_TELEKINESIS | Dummy (Ghost) |
| 22667 | S_DUMMY3_UNDEAD2 | Dummy (Undead) |
| 22668 | S_DUMMY_LARGE_R30 | Dummy (Large) |

<!-- RAG_CHUNK: 20_Complete_Constants_Jan2026 -->
## Part 20: Complete New Script Constants (January 2026)

**Total: 145 new constants**

### Footprint (7)
```c
FOOTPRINT_EF_VICTORY2025
FOOTPRINT_EF_DRAGON_FACE_2D
FOOTPRINT_EF_DRAGON_FACE_3D
FOOTPRINT_EF_DIVINE
FOOTPRINT_EF_NYAR_BLUE
FOOTPRINT_EF_NYAR_PURPLE
FOOTPRINT_EF_FEATHER
```

### HatEffect (14)
```c
HAT_EF_HANMAC_MUNCH
HAT_EF_C_OVER_CLOUD
HAT_EF_C_AURORA_ON_CLOUDS
HAT_EF_ROS_REDSPIRIT
HAT_EF_ROS_BLUESPIRIT
HAT_EF_DIVINE_SKY_INVITE
HAT_EF_C_NIGHTMARE_CHAIN
HAT_EF_C_SPOT_MIKE
HAT_EF_C_SPOT_FLOWER
HAT_EF_C_2025ROSFESTA
HAT_EF_GOLDEN_AURA_TW
HAT_EF_C_S_BEELZEBUB_WING
HAT_EF_SOLID_STATE_RECOGNITION
HAT_EF_C_CURSED_SERPENT
```

### ItemGroup (105)
```c
IG_AEGIS_100582
IG_AEGIS_100584
IG_DT_COLABO_BOX1
IG_DT_COLABO_BOX2
IG_CLOUD_COSTUME_PACK
IG_COSTUMEMILEPACK_39_1
IG_COSTUMEMILEPACK_39_2
IG_COSTUMEMILEPACK_39_3
IG_RT_CH01_ARMOR_A
IG_RT_CH01_ARMOR_C
IG_RT_CH01_DIMEN_A
IG_RT_CH01_DIMEN_C
IG_RT_CH01_DIMEN_3
IG_RT_CH01_EXTRA_A
IG_RT_CH01_EXTRA_C
IG_RT_CH01_EXTRA_2
IG_RT_CH01_EXTRA_4
IG_RT_CH01_EXTRA_5
IG_AEGIS_104901
IG_AEGIS_105031
IG_23TH_COSTUME_A
IG_23TH_COSTUME_B
IG_23TH_COSTUME_C
IG_AEGIS_105059
IG_AEGIS_105161
IG_AEGIS_105162
IG_AEGIS_105219
IG_AEGIS_105220
IG_SP_COSTUME_COLLECTION
IG_2025ROS_FOR_OFFLINE
IG_AEGIS_105518
IG_AEGIS_105715
IG_LI_NYANGVINE_BOX1_40
IG_LI_NYANGVINE_BOX2_40
IG_LI_NYANGVINE_BOX3_40
IG_23TH_COSTUME_PACK_A
IG_23TH_COSTUME_PACK_B
IG_23TH_COSTUME_PACK_C
IG_23TH_PACKAGE_1
IG_23TH_PACKAGE_2
IG_23TH_PACKAGE_3
IG_23TH_PACKAGE_4
IG_COSTUMEMILEPACK_SP_1
IG_COSTUMEMILEPACK_SP_2
IG_COSTUMEMILEPACK_SP_3
IG_COSTUMEMILEPACK_SP_4
IG_COSTUMEMILEPACK_41_1
IG_COSTUMEMILEPACK_41_2
IG_COSTUMEMILEPACK_41_3
IG_NIFLHEIM_COSTUME_1
IG_NIFLHEIM_COSTUME_2
IG_NIFLHEIM_COSTUME_3
IG_NIFLHEIM_COSTUME_4
IG_AEGIS_14622
IG_ROS_FESTA_BOX
IG_R_EP1921_ALBUM
IG_R_EP1921_BOSS
IG_RT_EP21_GAEBOLG_A
IG_RT_EP21_GAEBOLG_C
IG_RT_EP21_ICY_A
IG_RT_EP21_ICY_C
IG_RT_EP21_ICY_2
IG_RT_EP21_YORKER_A
IG_RT_EP21_YORKER_C
IG_RT_EP21_WORKING_A
IG_RT_EP21_WORKING_C
IG_RT_EP21_ADMIN_A
IG_RT_EP21_ADMIN_C
IG_RT_EP21_ADMIN_2
IG_RT_EP21_PURIFY_A
IG_RT_EP21_PURIFY_C
IG_RT_EP21_PURIFY_3
IG_RT_EP21_PURIFY_5
IG_RT_EP21_AID_A
IG_RT_EP21_AID_C
IG_RT_EP21_AID_2
IG_RT_EP21_AID_4
IG_RT_EP21_COMPANY_A
IG_RT_EP21_COMPANY_C
IG_RT_EP21_COMPANY_3
IG_RT_EP21_COMPANY_5
IG_RT_EP21_HORN_A
IG_RT_EP21_HORN_C
IG_RT_EP21_HORN_3
IG_RT_EP21_HORN_5
IG_RT_EP21_TAN_A
IG_RT_EP21_TAN_C
IG_AEGIS_105828
IG_AEGIS_105829
IG_AEGIS_105832
IG_AEGIS_105833
IG_AEGIS_105834
IG_AEGIS_105835
IG_AEGIS_105836
IG_AEGIS_105917
IG_LI_NYANGVINE_BOX1_SP
IG_LI_NYANGVINE_BOX2_SP
IG_LI_NYANGVINE_BOX3_SP
IG_LI_NYANGVINE_BOX4_SP
IG_2025_DEC_PACKAGE1
IG_2025_DEC_PACKAGE2
IG_CASH_BOOSTER_BOX2
IG_SELECT_DEC_PACK1
IG_SELECT_DEC_PACK2
IG_SELECT_DEC_PACK3
```

### Job (17)
```c
EAJL_UPPER  // → JOBL_UPPER
EAJL_BABY  // → JOBL_BABY
EAJ_BASEMASK  // → MAPID_FIRSTMASK
EAJ_UPPERMASK  // → MAPID_SECONDMASK
EAJ_SUMMONER  // → MAPID_SUMMONER
EAJ_SUPER_NOVICE  // → MAPID_SUPER_NOVICE
EAJ_SUPERNOVICE  // → MAPID_SUPER_NOVICE
EAJ_SPIRIT_HANDLER  // → MAPID_SPIRIT_HANDLER
EAJ_SUPER_BABY  // → MAPID_SUPER_BABY
EAJ_SUPER_NOVICE_E  // → MAPID_SUPER_NOVICE_E
EAJ_SUPER_BABY_E  // → MAPID_SUPER_BABY_E
EAJ_HYPER_NOVICE  // → MAPID_HYPER_NOVICE
EAJ_SKY_EMPEROR  // → MAPID_SKY_EMPEROR
EAJ_NIGHT_WATCH  // → MAPID_NIGHT_WATCH
EAJ_SHINKIROSHIRANUI  // → MAPID_SHINKIROSHIRANUI
EAJ_SOUL_ASCETIC  // → MAPID_SOUL_ASCETIC
bNonCritAtkRate  // → SP_NON_CRIT_ATK_RATE
```

### SkillFlag (1)
```c
INF2_IGNORENONCRITATKBONUS
```

### Status (1)
```c
EFST_BLOCK
```

---

<!-- RAG_CHUNK: 21_Item_Enchant_System_Complete -->
## Part 21: Item Enchant System (COMPLETE Documentation)

**Database:** `db/re/item_enchant.yml` (35,623 lines)

### Schema Reference

```yaml
# - Id                         Client side LUA index
#   TargetItems:               Items that can be enchanted
#     <item_aegis>: true       Item aegis name
#   MinimumRefine              Minimum refine required (Default: 0)
#   MinimumEnchantgrade        Minimum enchant grade required (Default: 0)
#   AllowRandomOptions         Allow random options (Default: true)
#   Reset:                     Reset enchant options
#     Chance                   Success chance (100000 = 100%)
#     Price                    Zeny cost
#     Materials:               Required materials
#       - Material: <item>
#         Amount: <count>
#   Order:                     Enchant slot order
#     - Slot: <0-3>
#   Slots:                     Per-slot configuration
#     - Slot: <0-3>
#       Price                  Zeny cost for this slot
#       Materials:             Required materials
#       Chance                 Base success chance
#       EnchantgradeBonus:     Bonus chance per grade
#         - Enchantgrade: <grade>
#           Chance: <bonus>
#       Enchants:              Available enchants by grade
#         - Enchantgrade: <grade>
#           Items:
#             - Item: <enchant_item>
#               Chance: <weight>
#       PerfectEnchants:       100% selectable enchants
#         - Item: <enchant_item>
#           Price: <zeny>
#           Materials: []
#       Upgrades:              Enchant upgrade paths
#         - Enchant: <source>
#           Upgrade: <target>
#           Price: <zeny>
#           Materials: []
```

### Script Commands for Enchanting

```c
// Get current enchant grade in item scripts
.@g = getenchantgrade();

// Enchant grade constants
ENCHANTGRADE_NONE  // No grade
ENCHANTGRADE_D     // Grade D (lowest)
ENCHANTGRADE_C     // Grade C
ENCHANTGRADE_B     // Grade B
ENCHANTGRADE_A     // Grade A (highest)

// Usage in item script
if (.@g >= ENCHANTGRADE_D) {
    bonus bAtkRate,5;
    if (.@g >= ENCHANTGRADE_C) {
        bonus bAtkRate,5;  // Total: 10%
        if (.@g >= ENCHANTGRADE_B) {
            bonus bAtkRate,5;  // Total: 15%
            if (.@g >= ENCHANTGRADE_A) {
                bonus bPAtk,10;  // P.ATK only at grade A
            }
        }
    }
}
```

### Example: Armor Enchant Configuration

```yaml
- Id: 1
  TargetItems:
    Gray_W_Suits: true
    Gray_W_Robe: true
  MinimumRefine: 7
  Reset:
    Chance: 100000
    Price: 100000
    Materials:
      - Material: Ep18_Amethyst_Fragment
        Amount: 25
  Order:
    - Slot: 3
    - Slot: 2
    - Slot: 1
  Slots:
    - Slot: 3
      Price: 100000
      Materials:
        - Material: Ep18_Amethyst_Fragment
          Amount: 15
      Enchants:
        - Enchantgrade: 0
          Items:
            - Item: Wolf_Orb_Str_1
              Chance: 9900
            - Item: Wolf_Orb_Agi_1
              Chance: 9900
```

---

<!-- RAG_CHUNK: 22_Item_Reform_System_Complete -->
## Part 22: Item Reform System (COMPLETE Documentation)

**Database:** `db/re/item_reform.yml` (15,685 lines)

### Schema Reference

```yaml
# - Item                       Catalyst item that opens UI
#   BaseItems:                 Items that can be reformed
#     - BaseItem               Source item aegis name
#       MinimumRefine          Min refine (Default: 0)
#       MaximumRefine          Max refine (Default: MAX_REFINE)
#       RequiredRandomOptions  Required random options count
#       CardsAllowed           Allow cards (Default: true)
#       Materials:             Additional materials required
#         - Material: <item>
#           Amount: <count>
#       ResultItem             Output item aegis name
#       ChangeRefine           Refine change (+/-) (Default: 0)
#       RandomOptionGroup      Option group to apply
#       ClearSlots             Remove cards/enchants (Default: false)
#       RemoveEnchantgrade     Remove grade (Default: false)
```

### Reform Example

```yaml
- Item: Reform_Ticket_Box
  BaseItems:
    - BaseItem: Old_Crown_DK
      MinimumRefine: 9
      CardsAllowed: false
      Materials:
        - Material: Oridecon
          Amount: 50
        - Material: Bradium
          Amount: 10
      ResultItem: Frontier_R_Crown_DK
      ChangeRefine: -2          # +9 becomes +7
      ClearSlots: true
      RemoveEnchantgrade: true
    - BaseItem: Old_Crown_IG
      MinimumRefine: 9
      Materials:
        - Material: Oridecon
          Amount: 50
      ResultItem: Frontier_R_Crown_IG
      ChangeRefine: -2
```

### System Comparison

| Feature | Enchant System | Reform System |
|---------|---------------|---------------|
| Trigger | NPC/builtin UI | Item use |
| Purpose | Add slot enchants | Transform items |
| Refine | Preserved | Configurable |
| Cards | Preserved | Configurable |
| Slots | 0-3 enchants | N/A |
| Database | item_enchant.yml | item_reform.yml |
| NPC Script | `openenchantui <id>` | Item script |

---
<!-- RAG_CHUNK: 23_New_Item_Scripts_Jan2026 -->
## Part 23: New Item Scripts (January 2026) - WITH FULL BONUSES

**Total: 144 items with actual bonus scripts**

These are the REAL item scripts from the database, showing actual bonuses and mechanics.


### 28145: Sky_Rush_Axe
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bUnbreakableWeapon;
bonus bPerfectHitAddRate,5;
bonus2 bSkillAtk,"MT_RUSH_STRIKE",15+7*(.@r/4);
bonus bNonCritAtkRate,3*(.@r/3);
bonus bBaseAtk,35*(.@r/3);
if (.@r>=7) {
bonus bNonCritAtkRate,25;
if (.@r>=9) {
bonus bAspdRate,10;
bonus bPAtk,5;
if (.@r>=11) {
bonus2 bSkillAtk,"MT_RUSH_STRIKE",15;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bAtkRate,5;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"MT_RUSH_STRIKE",10;
if (.@g>=ENCHANTGRADE_B) {
bonus2 bSkillAtk,"MT_RUSH_STRIKE",10;
if (.@g>=ENCHANTGRADE_A) {
bonus bPAtk,10;
```

### 400542: Time_DM_R_Crown_NW
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bMaxHP,120*(.@r/2);
bonus bMaxSP,30*(.@r/2);
bonus bAtkRate,2*(.@r/3);
bonus2 bSkillAtk,"NW_SPIRAL_SHOOTING",5*(.@r/4);
bonus2 bSkillAtk,"NW_WILD_FIRE",5*(.@r/4);
if (.@r>=7) {
bonus bLongAtkRate,10;
if (.@r>=9) {
bonus bPAtk,5;
if (.@r>=10) {
bonus2 bAddRace,RC_All,15;
bonus2 bAddRace,RC_Player_Human,-15;
bonus2 bAddRace,RC_Player_Doram,-15;
if (.@r>=11) {
bonus bFixedCast,-500;
bonus bCritical,10;
}
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,3;
if (.@g>=ENCHANTGRADE_C) {
```

### 400975: Frontier_R_Crown_DK
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bAtkRate,4*(.@r/3);
bonus2 bSkillAtk,"DK_HACKANDSLASHER",5*(.@r/4);
bonus2 bSkillAtk,"DK_SERVANTWEAPON_ATK",5*(.@r/4);
if (.@r>=7) {
bonus bShortAtkRate,10;
if (.@r>=9) {
bonus2 bAddRace,RC_All,15;
bonus2 bAddRace,RC_Player_Human,-15;
bonus2 bAddRace,RC_Player_Doram,-15;
bonus bPAtk,7;
if (.@r>=12) {
bonus bCritAtkRate,15;
bonus bCritical,15;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bMaxHPrate,5;
bonus bMaxSPrate,5;
if (.@g>=ENCHANTGRADE_B) {
bonus bShortAtkRate,10;
```

### 400976: Frontier_R_Crown_IG
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bAtkRate,4*(.@r/3);
bonus2 bSkillAtk,"IG_IMPERIAL_CROSS",7*(.@r/4);
bonus2 bSkillAtk,"IG_OVERSLASH",7*(.@r/4);
if (.@r>=7) {
bonus bShortAtkRate,10;
if (.@r>=9) {
bonus2 bAddRace,RC_All,15;
bonus2 bAddRace,RC_Player_Human,-15;
bonus2 bAddRace,RC_Player_Doram,-15;
bonus bPAtk,7;
if (.@r>=12) {
bonus bFixedCast,-500;
bonus bNonCritAtkRate,15;
bonus bBaseAtk,50;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bMaxHPrate,5;
bonus bMaxSPrate,5;
if (.@g>=ENCHANTGRADE_B) {
```

### 400977: Frontier_R_Crown_MT
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bAtkRate,4*(.@r/3);
bonus2 bSkillAtk,"MT_RUSH_STRIKE",7*(.@r/4);
bonus2 bSkillAtk,"MT_POWERFUL_SWING",7*(.@r/4);
if (.@r>=7) {
bonus bShortAtkRate,10;
if (.@r>=9) {
bonus2 bAddRace,RC_All,15;
bonus2 bAddRace,RC_Player_Human,-15;
bonus2 bAddRace,RC_Player_Doram,-15;
bonus bPAtk,7;
if (.@r>=12) {
bonus bNonCritAtkRate,15;
bonus bDelayrate,-5;
bonus bBaseAtk,50;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bMaxHPrate,5;
bonus bMaxSPrate,5;
if (.@g>=ENCHANTGRADE_B) {
```

### 400978: Frontier_R_Crown_BO
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bAtkRate,4*(.@r/3);
bonus2 bSkillAtk,"BO_EXPLOSIVE_POWDER",7*(.@r/4);
bonus2 bSkillAtk,"BO_DUST_EXPLOSION",7*(.@r/4);
if (.@r>=7) {
bonus bShortAtkRate,10;
if (.@r>=9) {
bonus2 bAddRace,RC_All,15;
bonus2 bAddRace,RC_Player_Human,-15;
bonus2 bAddRace,RC_Player_Doram,-15;
bonus bPAtk,7;
if (.@r>=12) {
bonus bNonCritAtkRate,15;
bonus bBaseAtk,75;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bMaxHPrate,5;
bonus bMaxSPrate,5;
if (.@g>=ENCHANTGRADE_B) {
bonus bShortAtkRate,10;
```

### 400979: Frontier_R_Crown_SHC
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bAtkRate,4*(.@r/3);
bonus2 bSkillAtk,"SHC_SAVAGE_IMPACT",5*(.@r/4);
bonus2 bSkillAtk,"SHC_CROSS_SLASH",5*(.@r/4);
if (.@r>=7) {
bonus bShortAtkRate,10;
if (.@r>=9) {
bonus2 bAddRace,RC_All,15;
bonus2 bAddRace,RC_Player_Human,-15;
bonus2 bAddRace,RC_Player_Doram,-15;
bonus bPAtk,7;
if (.@r>=12) {
bonus bCritAtkRate,15;
bonus bCritical,15;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bMaxHPrate,5;
bonus bMaxSPrate,5;
if (.@g>=ENCHANTGRADE_B) {
bonus bShortAtkRate,10;
```

### 400980: Frontier_R_Crown_ABC
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bMatkRate,4*(.@r/3);
bonus2 bSkillAtk,"ABC_FROM_THE_ABYSS_ATK",5*(.@r/4);
bonus2 bSkillAtk,"ABC_ABYSS_FLAME",5*(.@r/4);
bonus2 bSkillAtk,"ABC_ABYSS_FLAME_ATK",5*(.@r/4);
if (.@r>=7) {
bonus2 bMagicAtkEle,Ele_Fire,10;
bonus2 bMagicAtkEle,Ele_Neutral,10;
if (.@r>=9) {
bonus2 bMagicAddRace,RC_All,15;
bonus2 bMagicAddRace,RC_Player_Human,-15;
bonus2 bMagicAddRace,RC_Player_Doram,-15;
bonus bSMatk,7;
if (.@r>=12) {
bonus2 bMagicAtkEle,Ele_Fire,15;
bonus2 bMagicAtkEle,Ele_Neutral,15;
bonus bMatk,50;
bonus bAspd,2;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bSMatk,5;
if (.@g>=ENCHANTGRADE_C) {
```

### 400981: Frontier_R_Crown_AG
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bMatkRate,4*(.@r/3);
bonus2 bSkillAtk,"AG_CRIMSON_ARROW",5*(.@r/4);
bonus2 bSkillAtk,"AG_CRIMSON_ARROW_ATK",5*(.@r/4);
bonus2 bSkillAtk,"AG_ROCK_DOWN",5*(.@r/4);
if (.@r>=7) {
bonus2 bMagicAtkEle,Ele_Fire,10;
bonus2 bMagicAtkEle,Ele_Earth,10;
if (.@r>=9) {
bonus2 bMagicAddRace,RC_All,15;
bonus2 bMagicAddRace,RC_Player_Human,-15;
bonus2 bMagicAddRace,RC_Player_Doram,-15;
bonus bSMatk,7;
if (.@r>=12) {
bonus bFixedCast,-500;
bonus2 bMagicAtkEle,Ele_Fire,15;
bonus2 bMagicAtkEle,Ele_Earth,15;
bonus bMatk,50;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bSMatk,5;
if (.@g>=ENCHANTGRADE_C) {
```

### 400982: Frontier_R_Crown_EM
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bMatkRate,4*(.@r/3);
bonus2 bSkillAtk,"MG_LIGHTNINGBOLT",35*(.@r/4);
bonus2 bSkillAtk,"MG_FIREBOLT",35*(.@r/4);
bonus2 bSkillAtk,"MG_COLDBOLT",35*(.@r/4);
bonus2 bSkillAtk,"MG_SOULSTRIKE",50*(.@r/4);
if (.@r>=7) {
bonus2 bMagicAtkEle,Ele_Ghost,10;
bonus2 bMagicAtkEle,Ele_Fire,10;
bonus2 bMagicAtkEle,Ele_Water,10;
bonus2 bMagicAtkEle,Ele_Wind,10;
if (.@r>=9) {
bonus2 bMagicAddRace,RC_All,15;
bonus2 bMagicAddRace,RC_Player_Human,-15;
bonus2 bMagicAddRace,RC_Player_Doram,-15;
bonus bSMatk,7;
if (.@r>=12) {
bonus2 bMagicAtkEle,Ele_Ghost,15;
bonus2 bMagicAtkEle,Ele_Fire,15;
bonus2 bMagicAtkEle,Ele_Water,15;
bonus2 bMagicAtkEle,Ele_Wind,15;
bonus bMatk,50;
bonus bAspd,2;
}
```

### 400983: Frontier_R_Crown_CD
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bMatkRate,4*(.@r/3);
bonus2 bSkillAtk,"CD_DIVINUS_FLOS",5*(.@r/4);
if (.@r>=7) {
bonus2 bMagicAtkEle,Ele_Holy,10;
bonus2 bMagicAtkEle,Ele_Neutral,10;
if (.@r>=9) {
bonus2 bMagicAddRace,RC_All,15;
bonus2 bMagicAddRace,RC_Player_Human,-15;
bonus2 bMagicAddRace,RC_Player_Doram,-15;
bonus bSMatk,7;
if (.@r>=12) {
bonus bFixedCast,-500;
bonus2 bMagicAtkEle,Ele_Holy,15;
bonus2 bMagicAtkEle,Ele_Neutral,15;
bonus bMatk,50;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bSMatk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bMaxHPrate,5;
bonus bMaxSPrate,5;
```

### 400984: Frontier_R_Crown_IQ
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bAtkRate,4*(.@r/3);
bonus2 bSkillAtk,"IQ_EXPOSION_BLASTER",5*(.@r/4);
bonus2 bSkillAtk,"IQ_BLAZING_FLAME_BLAST",5*(.@r/4);
if (.@r>=7) {
bonus bLongAtkRate,10;
if (.@r>=9) {
bonus2 bAddRace,RC_All,15;
bonus2 bAddRace,RC_Player_Human,-15;
bonus2 bAddRace,RC_Player_Doram,-15;
bonus bPAtk,7;
if (.@r>=12) {
bonus bFixedCast,-500;
bonus bCritAtkRate,15;
bonus bCritical,10;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bMaxHPrate,5;
bonus bMaxSPrate,5;
if (.@g>=ENCHANTGRADE_B) {
```

### 400985: Frontier_R_Crown_WH
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bAtkRate,4*(.@r/3);
bonus2 bSkillAtk,"WH_CRESCIVE_BOLT",5*(.@r/4);
bonus2 bSkillAtk,"WH_GALESTORM",5*(.@r/4);
if (.@r>=7) {
bonus bLongAtkRate,10;
if (.@r>=9) {
bonus2 bAddRace,RC_All,15;
bonus2 bAddRace,RC_Player_Human,-15;
bonus2 bAddRace,RC_Player_Doram,-15;
bonus bPAtk,7;
if (.@r>=12) {
bonus bFixedCast,-500;
bonus bCritAtkRate,15;
bonus bCritical,10;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bMaxHPrate,5;
bonus bMaxSPrate,5;
if (.@g>=ENCHANTGRADE_B) {
```

### 400986: Frontier_R_Crown_TR
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bAtkRate,4*(.@r/3);
bonus2 bSkillAtk,"TR_ROSEBLOSSOM",7*(.@r/4);
bonus2 bSkillAtk,"TR_ROSEBLOSSOM_ATK",7*(.@r/4);
bonus2 bSkillAtk,"TR_RHYTHMSHOOTING",7*(.@r/4);
if (.@r>=7) {
bonus bLongAtkRate,10;
if (.@r>=9) {
bonus2 bAddRace,RC_All,15;
bonus2 bAddRace,RC_Player_Human,-15;
bonus2 bAddRace,RC_Player_Doram,-15;
bonus bPAtk,7;
if (.@r>=12) {
bonus bNonCritAtkRate,15;
bonus bVariableCastrate,-10;
bonus bBaseAtk,50;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bMaxHPrate,5;
bonus bMaxSPrate,5;
```

### 400987: Frontier_R_Crown_SS
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bAtkRate,4*(.@r/3);
bonus2 bSkillAtk,"SS_FUUMAKOUCHIKU",7*(.@r/4);
bonus2 bSkillAtk,"SS_KUNAIKAITEN",7*(.@r/4);
if (.@r>=7) {
bonus bLongAtkRate,10;
if (.@r>=9) {
bonus2 bAddRace,RC_All,15;
bonus2 bAddRace,RC_Player_Human,-15;
bonus2 bAddRace,RC_Player_Doram,-15;
bonus bPAtk,7;
if (.@r>=12) {
bonus bNonCritAtkRate,15;
bonus bBaseAtk,75;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bMaxHPrate,5;
bonus bMaxSPrate,5;
if (.@g>=ENCHANTGRADE_B) {
bonus bLongAtkRate,10;
```

### 400988: Frontier_R_Crown_NW
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bAtkRate,4*(.@r/3);
bonus2 bSkillAtk,"NW_SPIRAL_SHOOTING",5*(.@r/4);
bonus2 bSkillAtk,"NW_WILD_SHOT",5*(.@r/4);
if (.@r>=7) {
bonus bLongAtkRate,10;
if (.@r>=9) {
bonus2 bAddRace,RC_All,15;
bonus2 bAddRace,RC_Player_Human,-15;
bonus2 bAddRace,RC_Player_Doram,-15;
bonus bPAtk,7;
if (.@r>=12) {
bonus bFixedCast,-500;
bonus bCritAtkRate,15;
bonus bCritical,10;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bMaxHPrate,5;
bonus bMaxSPrate,5;
if (.@g>=ENCHANTGRADE_B) {
```

### 400989: Frontier_R_Crown_SKE
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bAtkRate,4*(.@r/3);
bonus2 bSkillAtk,"SKE_SKY_SUN",5*(.@r/4);
bonus2 bSkillAtk,"SKE_SUNSET_BLAST",5*(.@r/4);
if (.@r>=7) {
bonus bShortAtkRate,10;
if (.@r>=9) {
bonus2 bAddRace,RC_All,15;
bonus2 bAddRace,RC_Player_Human,-15;
bonus2 bAddRace,RC_Player_Doram,-15;
bonus bPAtk,7;
if (.@r>=12) {
bonus bCritAtkRate,15;
bonus bCritical,15;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bMaxHPrate,5;
bonus bMaxSPrate,5;
if (.@g>=ENCHANTGRADE_B) {
bonus bShortAtkRate,10;
```

### 400990: Frontier_R_Crown_SOA
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bMatkRate,4*(.@r/3);
bonus2 bSkillAtk,"SOA_TALISMAN_OF_BLUE_DRAGON",5*(.@r/4);
bonus2 bSkillAtk,"SOA_TALISMAN_OF_RED_PHOENIX",5*(.@r/4);
if (.@r>=7) {
bonus2 bMagicAtkEle,Ele_Holy,10;
bonus2 bMagicAtkEle,Ele_Fire,10;
bonus2 bMagicAtkEle,Ele_Neutral,10;
bonus2 bMagicAtkEle,Ele_Earth,10;
bonus2 bMagicAtkEle,Ele_Water,10;
bonus2 bMagicAtkEle,Ele_Wind,10;
bonus2 bMagicAtkEle,Ele_Ghost,10;
bonus2 bMagicAtkEle,Ele_Dark,10;
if (.@r>=9) {
bonus2 bMagicAddRace,RC_All,15;
bonus2 bMagicAddRace,RC_Player_Human,-15;
bonus2 bMagicAddRace,RC_Player_Doram,-15;
bonus bSMatk,7;
if (.@r>=12) {
bonus bFixedCast,-500;
bonus2 bMagicAtkEle,Ele_Holy,15;
bonus2 bMagicAtkEle,Ele_Fire,15;
bonus2 bMagicAtkEle,Ele_Neutral,15;
bonus2 bMagicAtkEle,Ele_Earth,15;
```

### 400991: Frontier_R_Crown_HN
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bMatkRate,4*(.@r/3);
bonus2 bSkillAtk,"HN_JUPITEL_THUNDER_STORM",5*(.@r/4);
bonus2 bSkillAtk,"HN_JACK_FROST_NOVA",5*(.@r/4);
if (.@r>=7) {
bonus2 bMagicAtkEle,Ele_Wind,10;
bonus2 bMagicAtkEle,Ele_Water,10;
if (.@r>=9) {
bonus2 bMagicAddRace,RC_All,15;
bonus2 bMagicAddRace,RC_Player_Human,-15;
bonus2 bMagicAddRace,RC_Player_Doram,-15;
bonus bSMatk,7;
if (.@r>=12) {
bonus bFixedCast,-500;
bonus2 bMagicAtkEle,Ele_Wind,15;
bonus2 bMagicAtkEle,Ele_Water,15;
bonus bMatk,50;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bSMatk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bMaxHPrate,5;
```

### 400992: Frontier_R_Crown_SH
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bMatkRate,4*(.@r/3);
bonus2 bSkillAtk,"SH_HYUN_ROKS_BREEZE",5*(.@r/4);
bonus2 bSkillAtk,"SH_HYUN_ROK_SPIRIT_POWER",5*(.@r/4);
if (.@r>=7) {
bonus2 bMagicAtkEle,Ele_Holy,10;
bonus2 bMagicAtkEle,Ele_Fire,10;
bonus2 bMagicAtkEle,Ele_Neutral,10;
bonus2 bMagicAtkEle,Ele_Earth,10;
bonus2 bMagicAtkEle,Ele_Water,10;
bonus2 bMagicAtkEle,Ele_Wind,10;
bonus2 bMagicAtkEle,Ele_Dark,10;
if (.@r>=9) {
bonus2 bMagicAddRace,RC_All,15;
bonus2 bMagicAddRace,RC_Player_Human,-15;
bonus2 bMagicAddRace,RC_Player_Doram,-15;
bonus bSMatk,7;
if (.@r>=12) {
bonus bFixedCast,-500;
bonus2 bMagicAtkEle,Ele_Holy,15;
bonus2 bMagicAtkEle,Ele_Fire,15;
bonus2 bMagicAtkEle,Ele_Neutral,15;
bonus2 bMagicAtkEle,Ele_Earth,15;
bonus2 bMagicAtkEle,Ele_Water,15;
```

### 401055: Stardust_Crown_SV
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bPow,5;
bonus bCon,5;
bonus bCritAtkRate,4*(.@r/2);
bonus bBaseAtk,20*(.@r/2);
if (.@r>=7) {
bonus bShortAtkRate,15;
bonus bLongAtkRate,15;
if (.@r>=9) {
bonus bCRate,5;
bonus bAtkRate,10;
if (.@r>=11) {
bonus bCritAtkRate,25;
bonus bPAtk,8;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bAtkRate,5;
bonus bPow,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bCRate,5;
bonus bCritical,15;
if (.@g>=ENCHANTGRADE_B) {
```

### 401056: Stardust_Crown_SC
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bPow,5;
bonus bCon,5;
bonus bBaseAtk,30*(.@r/2);
if (.@r>=7) {
bonus bShortAtkRate,15;
bonus bLongAtkRate,15;
if (.@r>=9) {
bonus bPAtk,7;
bonus bAtkRate,12;
if (.@r>=11) {
bonus bShortAtkRate,25;
bonus bLongAtkRate,25;
bonus bPAtk,8;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bAtkRate,5;
bonus bPow,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bPAtk,7;
bonus bBaseAtk,25;
if (.@g>=ENCHANTGRADE_B) {
```

### 401057: Stardust_Crown_VI
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bSpl,5;
bonus bCon,5;
bonus bMatk,25*(.@r/2);
if (.@r>=7) {
bonus bVariableCastrate,-10;
if (.@r>=9) {
bonus bSMatk,7;
bonus bMatkRate,12;
if (.@r>=11) {
bonus2 bMagicAtkEle,Ele_All,25;
bonus bSMatk,8;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bMatkRate,5;
bonus bSpl,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bSMatk,7;
bonus bMatk,25;
if (.@g>=ENCHANTGRADE_B) {
bonus bFixedCast,-500;
bonus bDelayrate,-7;
```

### 401058: Sky_Rune_Crown_IG
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bMatk,5*(.@r/2);
bonus2 bMagicAtkEle,Ele_Holy,2*(.@r/3);
bonus2 bMagicAtkEle,Ele_Neutral,2*(.@r/3);
bonus bMatkRate,2*(.@r/3);
bonus2 bSkillAtk,"IG_IMPERIAL_PRESSURE",5*(.@r/4);
bonus2 bSkillAtk,"IG_CROSS_RAIN",5*(.@r/4);
if (.@r>=7) {
bonus2 bMagicAtkEle,Ele_Holy,10;
bonus2 bMagicAtkEle,Ele_Neutral,10;
if (.@r>=9) {
bonus bSMatk,5;
if (.@r>=11) {
bonus bFixedCast,-500;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bSMatk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bDelayrate,-10;
if (.@g>=ENCHANTGRADE_B) {
bonus2 bMagicAddSize,Size_All,10;
if (.@g>=ENCHANTGRADE_A) {
```

### 401059: Sky_Rune_Crown_ABC
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bBaseAtk,3*(.@r/2);
bonus bHit,5*(.@r/2);
bonus bNonCritAtkRate,3*(.@r/3);
bonus bShortAtkRate,(.@r/3);
bonus bAtkRate,2*(.@r/3);
bonus2 bSkillAtk,"ABC_CHASING_BREAK",5*(.@r/4);
bonus2 bSkillAtk,"ABC_DEFT_STAB",5*(.@r/4);
if (.@r>=7) {
bonus bShortAtkRate,10;
if (.@r>=9) {
bonus bPAtk,5;
if (.@r>=11) {
bonus bDelayrate,-10;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"ABC_DEFT_STAB",15;
if (.@g>=ENCHANTGRADE_B) {
bonus2 bAddSize,Size_All,10;
if (.@g>=ENCHANTGRADE_A) {
```

### 401060: Sky_Rune_Crown_SH
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bCritical,2*(.@r/2);
bonus bBaseAtk,3*(.@r/2);
bonus bCritAtkRate,3*(.@r/3);
bonus bAtkRate,2*(.@r/3);
bonus2 bSkillAtk,"SH_HOGOGONG_STRIKE",7*(.@r/4);
bonus2 bSkillAtk,"SH_CHUL_HO_BATTERING",7*(.@r/4);
if (.@r>=7) {
bonus bLongAtkRate,10;
if (.@r>=9) {
bonus bPAtk,5;
if (.@r>=11) {
bonus bFixedCast,-500;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"SH_HOGOGONG_STRIKE",15;
if (.@g>=ENCHANTGRADE_B) {
bonus2 bAddSize,Size_All,10;
if (.@g>=ENCHANTGRADE_A) {
bonus2 bAddEle,Ele_All,10;
```

### 401115: Sky_Rune_Crown_MS
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bBaseAtk,3*(.@r/2);
bonus bHit,5*(.@r/2);
bonus bNonCritAtkRate,3*(.@r/3);
bonus bShortAtkRate,(.@r/3);
bonus bAtkRate,2*(.@r/3);
bonus2 bSkillAtk,"MT_RUSH_STRIKE",5*(.@r/4);
bonus2 bSkillAtk,"MT_POWERFUL_SWING",5*(.@r/4);
if (.@r>=7) {
bonus bShortAtkRate,10;
if (.@r>=9) {
bonus bPAtk,5;
if (.@r>=11) {
bonus bDelayrate,-10;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"MT_POWERFUL_SWING",15;
if (.@g>=ENCHANTGRADE_B) {
bonus2 bAddSize,Size_All,10;
if (.@g>=ENCHANTGRADE_A) {
```

### 401116: Sky_Rune_Crown_WH
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bCritical,2*(.@r/2);
bonus bBaseAtk,3*(.@r/2);
bonus bCritAtkRate,3*(.@r/3);
bonus bAtkRate,2*(.@r/3);
bonus2 bSkillAtk,"WH_CRESCIVE_BOLT",5*(.@r/4);
bonus2 bSkillAtk,"WH_HAWKRUSH",5*(.@r/4);
if (.@r>=7) {
bonus bLongAtkRate,10;
if (.@r>=9) {
bonus bPAtk,5;
if (.@r>=11) {
bonus bFixedCast,-500;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"WH_HAWKRUSH",15;
if (.@g>=ENCHANTGRADE_B) {
bonus2 bAddSize,Size_All,10;
if (.@g>=ENCHANTGRADE_A) {
bonus2 bAddEle,Ele_All,10;
```

### 401117: Sky_Rune_Crown_HN
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bMatk,5*(.@r/2);
bonus2 bMagicAtkEle,Ele_Ghost,2*(.@r/3);
bonus2 bMagicAtkEle,Ele_Wind,2*(.@r/3);
bonus bMatkRate,2*(.@r/3);
bonus2 bSkillAtk,"HN_NAPALM_VULCAN_STRIKE",5*(.@r/4);
if (.@r>=7) {
bonus2 bMagicAtkEle,Ele_Ghost,10;
bonus2 bMagicAtkEle,Ele_Wind,10;
if (.@r>=9) {
bonus bSMatk,5;
if (.@r>=11) {
bonus bFixedCast,-500;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bSMatk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"HN_NAPALM_VULCAN_STRIKE",10;
if (.@g>=ENCHANTGRADE_B) {
bonus2 bMagicAddSize,Size_All,10;
if (.@g>=ENCHANTGRADE_A) {
bonus2 bMagicAddEle,Ele_All,10;
```

### 401118: Sky_Rune_Crown_CD
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bMatk,5*(.@r/2);
bonus2 bMagicAtkEle,Ele_Holy,2*(.@r/3);
bonus bMatkRate,2*(.@r/3);
bonus2 bSkillAtk,"CD_ARBITRIUM",5*(.@r/4);
bonus2 bSkillAtk,"CD_ARBITRIUM_ATK",5*(.@r/4);
bonus2 bSkillAtk,"CD_FRAMEN",5*(.@r/4);
if (.@r>=7) {
bonus2 bMagicAtkEle,Ele_Holy,10;
if (.@r>=9) {
bonus bSMatk,5;
if (.@r>=11) {
bonus bFixedCast,-500;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bSMatk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"CD_FRAMEN",10;
if (.@g>=ENCHANTGRADE_B) {
bonus2 bMagicAddSize,Size_All,10;
if (.@g>=ENCHANTGRADE_A) {
bonus2 bMagicAddEle,Ele_All,10;
```

### 401119: Sky_Rune_Crown_IQ
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bBaseAtk,3*(.@r/2);
bonus bHit,5*(.@r/2);
bonus bAtkRate,2*(.@r/3);
bonus bMaxHPrate,3*(.@r/3);
bonus2 bSkillAtk,"IQ_THIRD_FLAME_BOMB",5*(.@r/4);
bonus2 bSkillAtk,"SR_TIGERCANNON",5*(.@r/4);
if (.@r>=7) {
bonus bShortAtkRate,10;
if (.@r>=9) {
bonus bPAtk,5;
if (.@r>=11) {
bonus bPerfectHitAddRate,5;
bonus bMaxHPrate,5;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"SR_TIGERCANNON",15;
if (.@g>=ENCHANTGRADE_B) {
bonus2 bAddSize,Size_All,10;
if (.@g>=ENCHANTGRADE_A) {
```

### 401120: Sky_Rune_Crown_SKE
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bBaseAtk,3*(.@r/2);
bonus bHit,5*(.@r/2);
bonus bNonCritAtkRate,3*(.@r/3);
bonus bShortAtkRate,(.@r/3);
bonus bAtkRate,2*(.@r/3);
bonus2 bSkillAtk,"SKE_SKY_MOON",5*(.@r/4);
bonus2 bSkillAtk,"SKE_STAR_LIGHT_KICK",5*(.@r/4);
if (.@r>=7) {
bonus bShortAtkRate,10;
if (.@r>=9) {
bonus bPAtk,5;
if (.@r>=11) {
bonus bUseSPrate,-5;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"SKE_SKY_MOON",15;
if (.@g>=ENCHANTGRADE_B) {
bonus2 bAddSize,Size_All,10;
if (.@g>=ENCHANTGRADE_A) {
```

### 410280: aegis_410280
```c
hateffect HAT_EF_C_BABY_GLOOM,true;
UnEquipScript: |
hateffect HAT_EF_C_BABY_GLOOM,false;
Script: |
hateffect HAT_EF_C_CONSECRATE_F_AUREOLA,true;
UnEquipScript: |
hateffect HAT_EF_C_CONSECRATE_F_AUREOLA,false;
```

### 420351: C_Auspicloud
```c
hateffect HAT_EF_C_AUSPICLOUD,true;
UnEquipScript: |
hateffect HAT_EF_C_AUSPICLOUD,false;
```

### 420358: C_Experiment_Mind
```c
hateffect HAT_EF_ATQUE_POENITENTIA,true;
UnEquipScript: |
hateffect HAT_EF_ATQUE_POENITENTIA,false;
Script: |
hateffect HAT_EF_MEDJED_TEXT,true;
UnEquipScript: |
hateffect HAT_EF_MEDJED_TEXT,false;
```

### 420449: C_Deep_You
```c
hateffect HAT_EF_HANMAC_MUNCH,true;
UnEquipScript: |
hateffect HAT_EF_HANMAC_MUNCH,false;
```

### 420511: C_Over_Cloud
```c
hateffect HAT_EF_C_OVER_CLOUD,true;
UnEquipScript: |
hateffect HAT_EF_C_OVER_CLOUD,false;
```

### 420512: C_Aurora_On_Clouds
```c
hateffect HAT_EF_C_AURORA_ON_CLOUDS,true;
UnEquipScript: |
hateffect HAT_EF_C_AURORA_ON_CLOUDS,false;
```

### 420552: C_Divine_Sky_Invite
```c
hateffect HAT_EF_DIVINE_SKY_INVITE,true;
UnEquipScript: |
hateffect HAT_EF_DIVINE_SKY_INVITE,false;
```

### 420576: aegis_420576
```c
hateffect HAT_EF_C_NIGHTMARE_CHAIN,true;
UnEquipScript: |
hateffect HAT_EF_C_NIGHTMARE_CHAIN,false;
```

### 420642: aegis_420642
```c
hateffect HAT_EF_C_SAMBA_CARNIVAL,true;
UnEquipScript: |
hateffect HAT_EF_C_SAMBA_CARNIVAL,false;
Script: |
hateffect HAT_EF_C_MELODY_WING,true;
UnEquipScript: |
hateffect HAT_EF_C_MELODY_WING,false;
bonus2 bSkillAtk,"SU_CN_METEOR",10*getskilllv("SU_NYANGGRASS");
```

### 480469: C_Con_of_Singapura_MSP
```c
hateffect HAT_EF_C_ROS2024_WING_1,true;
UnEquipScript: |
hateffect HAT_EF_C_ROS2024_WING_1,false;
```

### 480627: aegis_480627
```c
hateffect HAT_EF_C_2025ROSFESTA,true;
UnEquipScript: |
hateffect HAT_EF_C_2025ROSFESTA,false;
```

### 480669: aegis_480669
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bCRate,10;
bonus bCritical,3+(.@r/2);
bonus bCritAtkRate,3*(.@r/2);
bonus bBaseAtk,15*(.@r/2);
bonus2 bAddSize,Size_All,4*(.@r/3);
if (.@r>=7) {
bonus bPAtk,7;
bonus bAtkRate,5;
if (.@r>=9) {
bonus bDelayrate,-10;
bonus bCritical,7;
bonus bBaseAtk,45;
if (.@r>=11) {
bonus bShortAtkRate,15;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bCRate,7;
bonus bCritical,3;
if (.@g>=ENCHANTGRADE_C) {
bonus bShortAtkRate,10;
if (.@g>=ENCHANTGRADE_B) {
```

### 480670: aegis_480670
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bCRate,10;
bonus bCritical,3+(.@r/2);
bonus bCritAtkRate,3*(.@r/2);
bonus bBaseAtk,15*(.@r/2);
bonus2 bAddSize,Size_All,4*(.@r/3);
if (.@r>=7) {
bonus bPAtk,7;
bonus bAtkRate,5;
if (.@r>=9) {
bonus bVariableCastrate,-10;
bonus bDelayrate,-10;
if (.@r>=11) {
bonus bLongAtkRate,15;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bCRate,7;
bonus bCritical,3;
if (.@g>=ENCHANTGRADE_C) {
bonus bLongAtkRate,10;
if (.@g>=ENCHANTGRADE_B) {
bonus bPow,5;
```

### 480671: aegis_480671
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bPAtk,12;
bonus bAtkRate,5;
bonus bNonCritAtkRate,5*(.@r/2);
bonus bBaseAtk,25*(.@r/2);
bonus2 bAddSize,Size_All,4*(.@r/3);
if (.@r>=7) {
bonus bPAtk,7;
bonus bAtkRate,5;
if (.@r>=9) {
bonus bVariableCastrate,-10;
bonus bDelayrate,-10;
if (.@r>=11) {
bonus bLongAtkRate,15;
bonus bShortAtkRate,15;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,7;
bonus bBaseAtk,15;
if (.@g>=ENCHANTGRADE_C) {
bonus bShortAtkRate,10;
bonus bLongAtkRate,10;
```

### 480672: aegis_480672
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bPAtk,12;
bonus bMaxHPrate,5+(.@r/2);
bonus bBaseAtk,15*(.@r/2);
bonus2 bAddSize,Size_All,4*(.@r/3);
if (.@r>=7) {
bonus bPAtk,7;
bonus bAtkRate,5;
if (.@r>=9) {
bonus bVariableCastrate,-10;
bonus bDelayrate,-10;
if (.@r>=11) {
bonus bShortAtkRate,15;
bonus bLongAtkRate,15;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,7;
bonus bBaseAtk,15;
if (.@g>=ENCHANTGRADE_C) {
bonus bShortAtkRate,10;
bonus bLongAtkRate,10;
bonus bMaxHPrate,2;
```

### 480673: aegis_480673
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bSMatk,12;
bonus bMatkRate,5;
bonus2 bMagicAtkEle,Ele_Neutral,3*(.@r/2);
bonus2 bMagicAtkEle,Ele_Fire,3*(.@r/2);
bonus2 bMagicAtkEle,Ele_Earth,3*(.@r/2);
bonus2 bMagicAtkEle,Ele_Water,3*(.@r/2);
bonus2 bMagicAtkEle,Ele_Wind,3*(.@r/2);
bonus2 bMagicAtkEle,Ele_Poison,3*(.@r/2);
bonus2 bMagicAtkEle,Ele_Dark,3*(.@r/2);
bonus bMatk,15*(.@r/2);
bonus2 bMagicAddSize,Size_All,4*(.@r/3);
if (.@r>=7) {
bonus bSMatk,7;
bonus bMatkRate,5;
if (.@r>=9) {
bonus bVariableCastrate,-10;
bonus bDelayrate,-10;
if (.@r>=11) {
bonus2 bMagicAtkEle,Ele_Neutral,15;
bonus2 bMagicAtkEle,Ele_Fire,15;
bonus2 bMagicAtkEle,Ele_Earth,15;
bonus2 bMagicAtkEle,Ele_Water,15;
bonus2 bMagicAtkEle,Ele_Wind,15;
```

### 480674: aegis_480674
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bSMatk,12;
bonus bMatkRate,5;
bonus2 bMagicAtkEle,Ele_Undead,3*(.@r/2);
bonus2 bMagicAtkEle,Ele_Fire,3*(.@r/2);
bonus2 bMagicAtkEle,Ele_Neutral,3*(.@r/2);
bonus2 bMagicAtkEle,Ele_Wind,3*(.@r/2);
bonus2 bMagicAtkEle,Ele_Ghost,3*(.@r/2);
bonus2 bMagicAtkEle,Ele_Holy,3*(.@r/2);
bonus2 bMagicAtkEle,Ele_Dark,3*(.@r/2);
bonus bMatk,15*(.@r/2);
bonus2 bMagicAddSize,Size_All,4*(.@r/3);
if (.@r>=7) {
bonus bSMatk,7;
bonus bMatkRate,5;
if (.@r>=9) {
bonus bVariableCastrate,-10;
bonus bDelayrate,-10;
if (.@r>=11) {
bonus2 bMagicAtkEle,Ele_Undead,15;
bonus2 bMagicAtkEle,Ele_Fire,15;
bonus2 bMagicAtkEle,Ele_Neutral,15;
bonus2 bMagicAtkEle,Ele_Wind,15;
bonus2 bMagicAtkEle,Ele_Ghost,15;
```

### 500120: Falx
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus2 bSkillAtk,"BO_MAYHEMIC_THORNS",15+4*(.@r/2);
bonus bAtkRate,(.@r/2);
bonus bBaseAtk,20*(.@r/2);
if (.@r>=7) {
bonus bCritical,15;
bonus2 bSkillAtk,"BO_MAYHEMIC_THORNS",15;
if (.@r>=9) {
bonus bVariableCastrate,-10;
bonus bCRate,7;
if (.@r>=12) {
bonus bCritAtkRate,15;
bonus2 bSkillAtk,"BO_MAYHEMIC_THORNS",10;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bCritAtkRate,10;
bonus bCritical,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bLongAtkRate,20;
bonus bVariableCastrate,-5;
if (.@g>=ENCHANTGRADE_B) {
bonus2 bSkillAtk,"BO_MAYHEMIC_THORNS",15;
```

### 500134: Sky_Napalm_Sword
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bVariableCastrate,-5;
bonus2 bSkillAtk,"HN_JUPITEL_THUNDER_STORM",15;
bonus2 bMagicAtkEle,Ele_Ghost,2*(.@r/3);
bonus2 bMagicAtkEle,Ele_Wind,2*(.@r/3);
bonus bMatk,30*(.@r/3);
bonus2 bSkillAtk,"HN_NAPALM_VULCAN_STRIKE",5*(.@r/4);
if (.@r>=7) {
bonus2 bMagicAtkEle,Ele_Ghost,25;
bonus2 bMagicAtkEle,Ele_Wind,25;
if (.@r>=9) {
bonus bVariableCastrate,-10;
bonus bSMatk,5;
if (.@r>=11) {
bonus2 bSkillAtk,"HN_JUPITEL_THUNDER_STORM",15;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bMatkRate,5;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"HN_JUPITEL_THUNDER_STORM",10;
if (.@g>=ENCHANTGRADE_B) {
bonus bDelayrate,-10;
```

### 510192: Frontier_ABC_Dagger
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bSMatk,5;
bonus2 bSkillAtk,"ABC_FROM_THE_ABYSS_ATK",5+5*(.@r/3);
bonus bMatkRate,(.@r/2);
bonus bMatk,25*(.@r/2);
if (.@r>=9) {
bonus2 bMagicAtkEle,Ele_Fire,15;
bonus2 bMagicAtkEle,Ele_Neutral,15;
bonus bSMatk,7;
if (.@r>=11) {
bonus2 bSkillAtk,"ABC_FROM_THE_ABYSS_ATK",25;
if (.@r>=12) {
if (getskilllv("ABC_FROM_THE_ABYSS")>=5) {
bonus3 bAutoSpell,"ABC_FROM_THE_ABYSS",5,80;
}
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus2 bMagicAtkEle,Ele_Fire,10;
bonus2 bMagicAtkEle,Ele_Neutral,10;
bonus bSMatk,7;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"ABC_FROM_THE_ABYSS_ATK",10;
```

### 510199: Sky_Chasing_Dagger
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bPerfectHitAddRate,5;
bonus2 bSkillAtk,"ABC_CHASING_BREAK",15+7*(.@r/4);
bonus bNonCritAtkRate,2*(.@r/3);
bonus bBaseAtk,30*(.@r/3);
if (.@r>=7) {
bonus bNonCritAtkRate,25;
if (.@r>=9) {
bonus bDelayrate,-10;
bonus bPAtk,5;
if (.@r>=11) {
bonus2 bSkillAtk,"ABC_CHASING_BREAK",15;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bAtkRate,5;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"ABC_CHASING_BREAK",10;
if (.@g>=ENCHANTGRADE_B) {
bonus2 bSkillAtk,"ABC_CHASING_BREAK",10;
if (.@g>=ENCHANTGRADE_A) {
bonus bPAtk,10;
}
```

### 530072: Frontier_IG_Spear
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bPAtk,5;
bonus2 bSkillAtk,"IG_IMPERIAL_CROSS",5+5*(.@r/3);
bonus bAtkRate,(.@r/2);
bonus bBaseAtk,25*(.@r/2);
if (.@r>=9) {
bonus bShortAtkRate,15;
bonus bPAtk,7;
if (.@r>=11) {
bonus2 bSkillAtk,"IG_IMPERIAL_CROSS",15;
if (.@r>=12) {
bonus2 bSkillAtk,"IG_IMPERIAL_CROSS",20;
bonus2 bSkillAtk,"IG_OVERSLASH",25;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bShortAtkRate,10;
bonus bPAtk,7;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"IG_IMPERIAL_CROSS",10;
if (.@g>=ENCHANTGRADE_B) {
bonus bNonCritAtkRate,15;
if (.@g>=ENCHANTGRADE_A) {
```

### 530074: Espetar
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus2 bSkillAtk,"IG_RADIANT_SPEAR",20+5*(.@r/3);
bonus bAtkRate,(.@r/3);
bonus bBaseAtk,25*(.@r/3);
if (.@r>=7) {
bonus2 bSkillAtk,"IG_RADIANT_SPEAR",25;
if (.@r>=9) {
bonus bCritAtkRate,15;
bonus bCritical,15;
if (.@r>=12) {
bonus2 bSkillAtk,"IG_RADIANT_SPEAR",15;
if (getskilllv("LG_CANNONSPEAR")>=5) {
autobonus3 "{ .@r = getrefine(); bonus2 bIgnoreResRaceRate,RC_All,15; bonus2 bIgnoreResRaceRate,RC_Player_Human,-15; bonus2 bIgnoreResRaceRate,RC_Player_Doram,-15; bonus4 bAutoSpellOnSkill,\"IG_RADIANT_SPEAR\",\"LG_CANNONSPEAR\",5,1000; bonus bLongAtkRate,3*.@r; bonus bStr,7*.@r; bonus2 bSkillAtk,\"LG_CANNONSPEAR\",65*.@r; }",1000,60000,"IG_GRAND_JUDGEMENT";
}
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bVariableCastrate,-10;
bonus bCritical,5;
if (.@g>=ENCHANTGRADE_C) {
bonus bCritAtkRate,10;
bonus bLongAtkRate,15;
if (.@g>=ENCHANTGRADE_B) {
```

### 530076: Sky_Imperial_Spear
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bVariableCastrate,-5;
bonus2 bSkillAtk,"IG_IMPERIAL_PRESSURE",15+7*(.@r/4);
bonus2 bMagicAtkEle,Ele_Holy,2*(.@r/3);
bonus2 bMagicAtkEle,Ele_Neutral,2*(.@r/3);
bonus bMatk,30*(.@r/3);
if (.@r>=7) {
bonus2 bMagicAtkEle,Ele_Holy,25;
bonus2 bMagicAtkEle,Ele_Neutral,25;
if (.@r>=9) {
bonus bVariableCastrate,-10;
bonus bSMatk,5;
if (.@r>=11) {
bonus2 bSkillAtk,"IG_IMPERIAL_PRESSURE",15;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bMatkRate,5;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"IG_IMPERIAL_PRESSURE",10;
if (.@g>=ENCHANTGRADE_B) {
bonus2 bSkillAtk,"IG_IMPERIAL_PRESSURE",10;
if (.@g>=ENCHANTGRADE_A) {
```

### 540110: Frontier_EM_Book
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bSMatk,5;
bonus2 bSkillAtk,"MG_LIGHTNINGBOLT",100+35*(.@r/3);
bonus2 bSkillAtk,"MG_FIREBOLT",100+35*(.@r/3);
bonus2 bSkillAtk,"MG_COLDBOLT",100+35*(.@r/3);
bonus bMatkRate,(.@r/2);
bonus bMatk,25*(.@r/2);
bonus2 bSkillFixedCast,"MG_LIGHTNINGBOLT",2500;
bonus2 bSkillFixedCast,"MG_FIREBOLT",2500;
bonus2 bSkillFixedCast,"MG_COLDBOLT",2500;
if (.@r>=9) {
bonus2 bMagicAtkEle,Ele_Ghost,15;
bonus2 bMagicAtkEle,Ele_Fire,15;
bonus2 bMagicAtkEle,Ele_Water,15;
bonus2 bMagicAtkEle,Ele_Wind,15;
bonus bSMatk,7;
if (.@r>=11) {
bonus2 bSkillAtk,"MG_LIGHTNINGBOLT",30;
bonus2 bSkillAtk,"MG_FIREBOLT",30;
bonus2 bSkillAtk,"MG_COLDBOLT",30;
if (.@r>=12) {
bonus2 bSkillAtk,"MG_LIGHTNINGBOLT",35;
bonus2 bSkillAtk,"MG_FIREBOLT",35;
bonus2 bSkillAtk,"MG_COLDBOLT",35;
```

### 540111: Frontier_SKE_Book
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus bCritical,5;
bonus2 bSkillAtk,"SKE_SKY_SUN",5+5*(.@r/3);
bonus bAtkRate,(.@r/2);
bonus bBaseAtk,25*(.@r/2);
if (.@r>=9) {
bonus bCRate,5;
bonus bCritical,15;
if (.@r>=11) {
bonus2 bSkillAtk,"SKE_SKY_SUN",15;
if (.@r>=12) {
bonus2 bSkillAtk,"SKE_SKY_SUN",20;
bonus2 bSkillAtk,"SKE_SUNSET_BLAST",25;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bPAtk,5;
bonus bCritical,5;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"SKE_SKY_SUN",10;
if (.@g>=ENCHANTGRADE_B) {
bonus bShortAtkRate,15;
if (.@g>=ENCHANTGRADE_A) {
```

### 540114: Elemental_Spirits
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus2 bSkillAtk,"EM_DIAMOND_STORM",20+5*(.@r/3);
bonus2 bSkillAtk,"EM_TERRA_DRIVE",20+5*(.@r/3);
bonus bMatkRate,(.@r/3);
bonus bMatk,25*(.@r/3);
if (.@r>=7) {
bonus2 bMagicAtkEle,Ele_Water,10;
bonus2 bMagicAtkEle,Ele_Earth,10;
bonus2 bSkillAtk,"EM_DIAMOND_STORM",20;
if (.@r>=9) {
bonus bSMatk,7;
bonus2 bSkillAtk,"EM_TERRA_DRIVE",20;
if (.@r>=12) {
bonus2 bSkillAtk,"EM_DIAMOND_STORM",15;
bonus2 bSkillAtk,"EM_TERRA_DRIVE",15;
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus2 bMagicAtkEle,Ele_Water,10;
bonus2 bMagicAtkEle,Ele_Earth,10;
bonus bSMatk,7;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"EM_DIAMOND_STORM",15;
```

### 540115: Book_Of_Crimson_M
```c
.@g = getenchantgrade();
.@r = getrefine();
bonus2 bSkillAtk,"SKE_SKY_MOON",20+5*(.@r/3);
bonus bAtkRate,(.@r/3);
bonus bBaseAtk,25*(.@r/3);
if (.@r>=7) {
bonus bNonCritAtkRate,15;
bonus bVariableCastrate,-10;
if (.@r>=9) {
bonus2 bSkillAtk,"SKE_SKY_MOON",20;
if (.@r>=12) {
bonus bShortAtkRate,10;
if (getskilllv("SKE_MIDNIGHT_KICK")>=5 && getskilllv("SKE_DAWN_BREAK")>=5) {
autobonus3 "{ .@r = getrefine(); bonus bNonCritAtkRate,15; bonus2 bSkillAtk,\"SKE_MIDNIGHT_KICK\",4*.@r; bonus2 bSkillAtk,\"SKE_DAWN_BREAK\",4*.@r; bonus4 bAutoSpellOnSkill,\"SKE_SKY_MOON\",\"SKE_DAWN_BREAK\",5,1000; bonus4 bAutoSpellOnSkill,\"SKE_DAWN_BREAK\",\"SKE_MIDNIGHT_KICK\",5,1000; }",1000,150000,"SKE_ENCHANTING_SKY";
}
}
}
}
if (.@g>=ENCHANTGRADE_D) {
bonus bNonCritAtkRate,10;
if (.@g>=ENCHANTGRADE_C) {
bonus2 bSkillAtk,"SKE_SKY_MOON",15;
if (.@g>=ENCHANTGRADE_B) {
bonus bShortAtkRate,15;
bonus bVariableCastrate,-5;
```


*... and 84 more items in database*

---

<!-- RAG_CHUNK: 24_4th_Job_Equipment_Patterns -->
## Part 24: 4th Job Equipment Script Patterns

### Standard Variables

```c
.@r = getrefine();       // Refine level (0-20)
.@g = getenchantgrade(); // Enchant grade (D/C/B/A)
.@s = getskilllv("X");   // Skill level
```

### Frontier Rune Crown Pattern

All 18 Frontier Crowns use this structure:

```c
.@g = getenchantgrade();
.@r = getrefine();

// Base scaling
bonus bAtkRate, 4*(.@r/3);                      // +4% ATK per 3 refine
bonus2 bSkillAtk, "CLASS_SKILL1", 5*(.@r/4);    // +5% skill dmg per 4 refine
bonus2 bSkillAtk, "CLASS_SKILL2", 5*(.@r/4);

// Refine thresholds
if (.@r >= 7) {
    bonus bShortAtkRate, 10;                    // or bLongAtkRate for ranged
    if (.@r >= 9) {
        bonus2 bAddRace, RC_All, 15;
        bonus2 bAddRace, RC_Player_Human, -15;  // PvP penalty
        bonus2 bAddRace, RC_Player_Doram, -15;
        bonus bPAtk, 7;
        if (.@r >= 12) {
            bonus bCritAtkRate, 15;
            bonus bCritical, 15;
        }
    }
}

// Grade thresholds (stack with refine)
if (.@g >= ENCHANTGRADE_D) {
    bonus bPAtk, 5;
    if (.@g >= ENCHANTGRADE_C) {
        bonus bMaxHPrate, 5;
        bonus bMaxSPrate, 5;
        if (.@g >= ENCHANTGRADE_B) {
            bonus bShortAtkRate, 10;
            if (.@g >= ENCHANTGRADE_A) {
                bonus2 bSkillAtk, "CLASS_SKILL1", 15;
            }
        }
    }
}
```

### Class Skills Reference (for bonus2 bSkillAtk)

| Class | Skill 1 | Skill 2 |
|-------|---------|---------|
| Dragon Knight | DK_HACKANDSLASHER | DK_SERVANTWEAPON_ATK |
| Imperial Guard | IG_IMPERIAL_CROSS | IG_OVERSLASH |
| Meister | MT_RUSH_STRIKE | MT_POWERFUL_SWING |
| Biolo | BO_ACIDIFIED_ZONE_WATER | BO_ACIDIFIED_ZONE_FIRE |
| Shadow Cross | SHC_SHADOW_STAB | SHC_SAVAGE_IMPACT |
| Abyss Chaser | ABC_ABYSS_STRIKE | ABC_FRENZY_SHOT |
| Arch Mage | AG_VIOLENT_QUAKE | AG_ALL_BLOOM |
| Elemental Master | EM_DIAMOND_STORM | EM_ELEMENTAL_BUSTER |
| Cardinal | CD_PETITIO | CD_FRAMEN |
| Inquisitor | IQ_OLEUM_SANCTUM | IQ_MASSIVE_F_BLASTER |
| Windhawk | WH_GALESTORM | WH_CRESCIVE_BOLT |
| Troubadour | TR_GEF_NOCTURN | TR_ROKI_CAPRICCIO |
| Shinkiro/Shiranui | SS_KAGEGISSEN | SS_SEKIENHOU |
| Night Watch | NW_SPIRAL_SHOOTING | NW_MAGAZINE_FOR_ONE |
| Sky Emperor | SKE_TWINKLING_GALAXY | SKE_STAR_BURST |
| Soul Ascetic | SOA_SOUL_EXPLOSION | SOA_TALISMAN_OF_PROTECTION |
| Spirit Handler | SH_HOWLING_OF_CHUL_HO | SH_HOGOGONG |
| Hyper Novice | HN_MEGA_MAGIC_BLASTER | HN_BREAKINGLIMIT |

### New Bonus Types Used

```c
bonus bPAtk, <n>;           // Physical P.ATK stat
bonus bSMatk, <n>;          // Special M.ATK stat  
bonus bNonCritAtkRate, <n>; // Non-critical attack damage %
bonus bCritAtkRate, <n>;    // Critical attack damage %
bonus bLongAtkRate, <n>;    // Ranged attack damage %
bonus bShortAtkRate, <n>;   // Melee attack damage %
```

---
