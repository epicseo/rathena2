# rAthena Content Creation Complete Guide v4.0

**Version:** 4.0 - RAG-Optimized Complete Edition
**File Size:** ~5K lines (merged from 3 files)
**Coverage:** 100% content designer workflow
**Last Updated:** 2025-11-19

---

<!-- RAG_CHUNK: overview -->
<!-- RAG_CHUNK:  -->
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

<!-- RAG_CHUNK: quick_reference -->
<!-- RAG_CHUNK:  -->
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

<!-- RAG_CHUNK: usage_guide -->
<!-- RAG_CHUNK:  -->
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

<!-- RAG_CHUNK: file_structure -->
<!-- RAG_CHUNK:  -->
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

<!-- RAG_CHUNK: key_takeaways -->
<!-- RAG_CHUNK:  -->
## 🎯 Key Takeaways

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

<!-- RAG_CHUNK:  -->
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
<!-- RAG_CHUNK: item_groups_complete -->

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

<!-- RAG_CHUNK: Table -->
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

<!-- RAG_CHUNK: System -->
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

<!-- RAG_CHUNK: Database -->
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

<!-- RAG_CHUNK: Algorithm -->
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

<!-- RAG_CHUNK: SubGroup -->
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

<!-- RAG_CHUNK: Script -->
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

<!-- RAG_CHUNK: Advanced -->
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

<!-- RAG_CHUNK: Complete -->
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

<!-- RAG_CHUNK: Common -->
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

<!-- RAG_CHUNK: Creating -->
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

<!-- RAG_CHUNK: Best -->
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

<!-- RAG_CHUNK: Troubleshooting -->
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

<!-- RAG_CHUNK: Related -->
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
<!-- RAG_CHUNK: quest_system_complete -->

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

<!-- RAG_CHUNK: Overview -->
## Overview

The quest database defines all quests available in rAthena, including their objectives, time limits, drop rates, and rewards. Quests are configured using YAML format.

**Database Location:** `/db/(pre-)re/quest_db.yml`

---

<!-- RAG_CHUNK: QUEST -->
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

<!-- RAG_CHUNK: FIELD -->
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

<!-- RAG_CHUNK: DROPS -->
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

<!-- RAG_CHUNK: COMPLETE -->
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

<!-- RAG_CHUNK: QUEST -->
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

<!-- RAG_CHUNK: QUEST -->
## QUEST STATUS VALUES

| Value | Constant | Meaning |
|-------|----------|---------|
| 0 | QUEST_NOT_STARTED | Quest not started |
| 1 | QUEST_ACTIVE | Quest active/in progress |
| 2 | QUEST_COMPLETE | Quest completed |

---

<!-- RAG_CHUNK: BEST -->
## BEST PRACTICES

1. **Unique IDs:** Always use unique quest IDs (avoid conflicts)
2. **Time Limits:** Use relative time (`+`) for recurring quests, absolute time for weekly/event quests
3. **Drop Rates:** Balance drop rates carefully (too high = no challenge, too low = frustration)
4. **Target Count:** Set `Count: 0` to temporarily disable objectives without deleting them
5. **Testing:** Test time limits thoroughly (server timezone matters!)
6. **Performance:** Avoid `Mob: 0` (all monsters) for drops when possible - use specific mobs
7. **UI Display:** Keep `Title` and `MapName` short for better UI display

---

<!-- RAG_CHUNK: COMMON -->
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

<!-- RAG_CHUNK: RELATED -->
## RELATED FILES

- `/db/(pre-)re/quest_db.yml` - Quest database
- `/doc/script_commands.txt` - Quest-related script commands
- `/db/(pre-)re/mob_db.yml` - Monster names for Targets
- `/db/(pre-)re/item_db.yml` - Item names for Drops

---

<!-- RAG_CHUNK: SEE -->
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
<!-- RAG_CHUNK: npc_patterns_complete -->

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

<!-- RAG_CHUNK:  -->
## 🎯 Purpose

This document provides **production-ready** patterns for advanced NPC scripting systems. Each pattern includes:
- Complete working implementation
- Security considerations (anti-cheat, exploit prevention)
- Memory-efficient design
- Performance optimization
- Common pitfalls and how to avoid them

---

<!-- RAG_CHUNK:  -->
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

<!-- RAG_CHUNK: 1 -->
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

<!-- RAG_CHUNK: 2 -->
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

<!-- RAG_CHUNK: 3 -->
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

<!-- RAG_CHUNK: 4 -->
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

<!-- RAG_CHUNK: 5 -->
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

<!-- RAG_CHUNK: 6 -->
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

<!-- RAG_CHUNK: 7 -->
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

<!-- RAG_CHUNK: 8 -->
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

<!-- RAG_CHUNK: 9 -->
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

<!-- RAG_CHUNK: 10 -->
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

<!-- RAG_CHUNK: 11 -->
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

<!-- RAG_CHUNK: 12 -->
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

<!-- RAG_CHUNK:  -->
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

<!-- RAG_CHUNK:  -->
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

<!-- RAG_CHUNK:  -->
## 🎯 Key Takeaways

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
<!-- RAG_CHUNK: VISUAL_EFFECTS_INDEX -->

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
<!-- RAG_CHUNK: EF_COMPLETE_LIST -->

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
<!-- RAG_CHUNK: EF_USAGE_NOTES -->

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

<!-- RAG_CHUNK: QUEST_VARIABLES -->

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

<!-- RAG_CHUNK: WHISPER_SYSTEM -->

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

<!-- RAG_CHUNK: CAPTCHA_SYSTEM -->

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
