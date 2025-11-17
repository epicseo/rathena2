---
kb_id: KB_REF_025
title: "Working with Databases in C++ (itemdb, mobdb, skilldb)"
category: Source Code
keywords: [database, itemdb, mobdb, skilldb, YAML, item_data, mob_data, TypesafeCachedYamlDatabase, custom_fields, database_modification, db_cpp]
related_files: [
  "src/map/itemdb.cpp",
  "src/map/itemdb.hpp",
  "src/map/mob.cpp",
  "src/map/mob.hpp",
  "src/map/skill.cpp",
  "src/map/skill.hpp",
  "db/re/item_db.yml",
  "db/re/mob_db.yml",
  "db/re/skill_db.yml"
]
difficulty: expert
use_case: "Interacting with game databases in C++ code and adding custom fields"
version: rAthena 2024
last_updated: 2024-01-15
---

# Working with Databases in C++ (itemdb, mobdb, skilldb)

## Quick Reference

### **Access Item Database**
```cpp
// Get item by ID
std::shared_ptr<item_data> item = item_db.find(501);  // Red Potion
if (item) {
    ShowInfo("Item: %s, Price: %d\n", item->name.c_str(), item->value_buy);
}

// Search by name
std::shared_ptr<item_data> item2 = item_db.searchname("Red_Potion");

// Legacy method (deprecated)
struct item_data* item3 = itemdb_search(501);
```

### **Access Mob Database**
```cpp
// Get mob by ID
std::shared_ptr<s_mob_db> mob = mob_db.find(1002);  // Poring
if (mob) {
    ShowInfo("Mob: %s, Level: %d\n", mob->name.c_str(), mob->lv);
}

// Legacy method
struct mob_db* mob2 = mob_get_db(1002);
```

### **Access Skill Database**
```cpp
// Get skill by ID
std::shared_ptr<s_skill_db> skill = skill_db.find(AL_HEAL);  // Heal
if (skill) {
    ShowInfo("Skill: %s, Max Level: %d\n", skill->name, skill->max);
}

// Legacy method
struct s_skill_db* skill2 = skill_db.get(AL_HEAL);
```

---

## Table of Contents
1. [Database System Overview](#database-system-overview)
2. [Item Database (itemdb)](#item-database-itemdb)
3. [Mob Database (mobdb)](#mob-database-mobdb)
4. [Skill Database (skilldb)](#skill-database-skilldb)
5. [Database Access Patterns](#database-access-patterns)
6. [Adding Custom Fields](#adding-custom-fields)
7. [Modifying Database Loading](#modifying-database-loading)
8. [Complete Examples](#complete-examples)
9. [Performance Tips](#performance-tips)
10. [Common Pitfalls](#common-pitfalls)

---

## Database System Overview

### **YAML-Based Database**

rAthena uses **YAML files** for databases (since 2020+):
- **Location**: `db/re/` (Renewal) or `db/pre-re/` (Pre-Renewal)
- **Format**: YAML (Yet Another Markup Language)
- **Parsing**: `TypesafeCachedYamlDatabase` template class
- **Caching**: Databases are loaded once at startup and cached in memory

### **Key Database Files**

| Database File | Purpose | Struct | C++ File |
|--------------|---------|--------|----------|
| `item_db.yml` | Items (weapons, armor, consumables) | `item_data` | `itemdb.cpp/hpp` |
| `mob_db.yml` | Monsters | `s_mob_db` | `mob.cpp/hpp` |
| `skill_db.yml` | Skills | `s_skill_db` | `skill.cpp/hpp` |
| `item_group.yml` | Item groups (random boxes) | `s_item_group_db` | `itemdb.cpp/hpp` |
| `mob_skill_db.yml` | Monster skills | `s_mob_skill` | `mob.cpp/hpp` |
| `produce_db.yml` | Crafting recipes | `s_produce_db` | `skill.cpp/hpp` |

### **Database Class Hierarchy**

```cpp
// Base class for all YAML databases
template <typename K, typename V>
class TypesafeCachedYamlDatabase {
    std::unordered_map<K, std::shared_ptr<V>> cache;

    virtual uint64 parseBodyNode(const ryml::NodeRef& node) = 0;
    virtual const std::string getDefaultLocation() = 0;
};

// Item database implementation
class ItemDatabase : public TypesafeCachedYamlDatabase<t_itemid, item_data> {
    std::unordered_map<std::string, std::shared_ptr<item_data>> nameToItemDataMap;
    std::unordered_map<std::string, std::shared_ptr<item_data>> aegisNameToItemDataMap;
};
```

---

## Item Database (itemdb)

### **struct item_data** (itemdb.hpp:3330-3422)

```cpp
struct item_data
{
    t_itemid nameid;                    // Item ID (e.g., 501)
    std::string name, ename;            // Japanese name, English name

    uint32 value_buy;                   // Buy price
    uint32 value_sell;                  // Sell price
    item_types type;                    // IT_HEALING, IT_WEAPON, IT_ARMOR, etc.
    uint8 subtype;                      // Weapon subtype, ammo type, etc.
    int32 maxchance;                    // Max drop chance (for logs)
    uint8 sex;                          // 0=Female, 1=Male, 2=Both
    uint32 equip;                       // Equipment location (EQP_HEAD_TOP, etc.)
    uint32 weight;                      // Weight (in 0.1 units)
    uint32 atk;                         // Attack power
    uint32 def;                         // Defense
    uint16 range;                       // Attack range
    uint16 slots;                       // Card slots
    uint32 look;                        // Visual appearance ID
    uint16 elv;                         // Minimum level requirement
    uint16 weapon_level;                // Weapon level (1-4)
    uint16 armor_level;                 // Armor level
    t_itemid view_id;                   // Visual override (for costumes)
    uint16 elvmax;                      // Maximum level requirement
#ifdef RENEWAL
    uint32 matk;                        // Magic attack
#endif

    uint64 class_base[3];               // Job restrictions (1-1, 2-1, 2-2)
    uint16 class_upper;                 // Job tier (Normal, Upper, Baby, etc.)

    struct {
        int32 chance;
        int32 id;
    } mob[MAX_SEARCH];                  // Top 10 mobs that drop this item

    struct script_code *script;         // Use script
    struct script_code *equip_script;   // Equip script
    struct script_code *unequip_script; // Unequip script

    struct {
        unsigned available : 1;
        uint32 no_equip;                // Map restrictions
        unsigned no_refine : 1;
        unsigned delay_consume;
        struct {
            bool drop, trade, trade_partner, sell, cart, storage,
                 guild_storage, mail, auction;
        } trade_restriction;
        unsigned autoequip: 1;
        bool buyingstore;
        bool dead_branch;
        bool group;
        unsigned guid : 1;
    } flag;
};
```

### **ItemDatabase Class** (itemdb.hpp:3424-3462)

```cpp
class ItemDatabase : public TypesafeCachedYamlDatabase<t_itemid, item_data> {
private:
    std::unordered_map<std::string, std::shared_ptr<item_data>> nameToItemDataMap;
    std::unordered_map<std::string, std::shared_ptr<item_data>> aegisNameToItemDataMap;

public:
    // Access methods
    std::shared_ptr<item_data> find(t_itemid id);                    // Get by ID
    std::shared_ptr<item_data> searchname(const char* name);         // Search by name
    std::shared_ptr<item_data> search_aegisname(const char *name);   // Search by aegis name

    // Utility
    std::string create_item_link(struct item& item);
};

extern ItemDatabase item_db;  // Global instance
```

### **Accessing Item Database**

```cpp
// Method 1: Modern C++ (recommended)
std::shared_ptr<item_data> item = item_db.find(501);
if (item) {
    ShowInfo("Item: %s, Buy: %d, Sell: %d\n",
             item->name.c_str(),
             item->value_buy,
             item->value_sell);
}

// Method 2: Search by name
std::shared_ptr<item_data> item2 = item_db.searchname("Red_Potion");
if (!item2) {
    ShowError("Item not found!\n");
}

// Method 3: Search by aegis name
std::shared_ptr<item_data> item3 = item_db.search_aegisname("Red_Potion");

// Method 4: Legacy (deprecated but still works)
struct item_data* item4 = itemdb_search(501);
// Note: This method always returns a valid pointer (defaults to UNKNOWN_ITEM_ID if not found)
```

### **Common Item Database Operations**

```cpp
// Check if item exists
if (item_db.exists(60000)) {
    ShowInfo("Item 60000 exists!\n");
}

// Get item type
std::shared_ptr<item_data> item = item_db.find(501);
if (item) {
    switch(item->type) {
        case IT_HEALING:  ShowInfo("Healing item\n"); break;
        case IT_USABLE:   ShowInfo("Usable item\n"); break;
        case IT_WEAPON:   ShowInfo("Weapon\n"); break;
        case IT_ARMOR:    ShowInfo("Armor\n"); break;
        case IT_CARD:     ShowInfo("Card\n"); break;
    }
}

// Check equipment location
if (item && (item->equip & EQP_HEAD_TOP)) {
    ShowInfo("This item equips on head top slot\n");
}

// Check job restrictions
if (item && (item->class_base[0] & (1ULL << MAPID_SWORDMAN))) {
    ShowInfo("Swordman can use this item\n");
}

// Check trade restrictions
if (item && item->flag.trade_restriction.drop) {
    ShowInfo("This item cannot be dropped\n");
}

// Execute item script
if (item && item->script) {
    run_script(item->script, 0, sd->bl.id, 0);
}
```

---

## Mob Database (mobdb)

### **struct s_mob_db** (mob.hpp)

```cpp
struct s_mob_db {
    t_mobid id;                         // Mob ID
    std::string name;                   // Mob name
    std::string jname;                  // Japanese name
    uint16 lv;                          // Level
    uint32 max_hp, max_sp;              // Max HP/SP
    uint32 base_exp, job_exp;           // Base/Job EXP
    uint16 range, range2, range3;       // Attack ranges
    uint32 atk1, atk2;                  // Min/Max attack
    uint32 def, mdef;                   // Defense, Magic Defense
    int16 str, agi, vit, int_, dex, luk; // Stats
    uint16 attack_motion, delay_motion; // Animation delays
    uint16 damage_taken_rate;           // Damage multiplier

    e_race race;                        // RC_FORMLESS, RC_UNDEAD, etc.
    e_race2 race2;                      // Secondary race
    e_element element;                  // Element (Fire, Water, etc.)
    e_size size;                        // SZ_SMALL, SZ_MEDIUM, SZ_BIG
    e_mode mode;                        // Behavior mode (MD_CANMOVE, MD_AGGRESSIVE, etc.)

    uint8 ai;                           // AI type (01-27)
    uint8 boss_type;                    // BOSSTYPE_NONE, BOSSTYPE_MINIBOSS, BOSSTYPE_MVP

    struct {
        t_itemid nameid;
        uint16 rate;
        bool steal_protected;
    } dropitem[MAX_MOB_DROP];           // Regular drops (up to 10)

    struct {
        t_itemid nameid;
        uint16 rate;
    } mvpitem[MAX_MVP_DROP];            // MVP drops (up to 3)

    // ... more fields
};
```

### **Accessing Mob Database**

```cpp
// Get mob by ID
std::shared_ptr<s_mob_db> mob = mob_db.find(1002);  // Poring
if (mob) {
    ShowInfo("Mob: %s, Level: %d, HP: %d\n",
             mob->name.c_str(),
             mob->lv,
             mob->max_hp);
}

// Check mob properties
if (mob) {
    // Check race
    if (mob->race == RC_BRUTE) {
        ShowInfo("This is a brute monster\n");
    }

    // Check element
    if (mob->element == ELE_FIRE) {
        ShowInfo("Fire element monster\n");
    }

    // Check mode flags
    if (mob->mode & MD_AGGRESSIVE) {
        ShowInfo("Aggressive monster\n");
    }

    if (mob->mode & MD_BOSS) {
        ShowInfo("Boss monster\n");
    }

    // Check drops
    for (int i = 0; i < MAX_MOB_DROP; i++) {
        if (mob->dropitem[i].nameid > 0) {
            ShowInfo("Drop: ItemID %d, Rate: %d\n",
                     mob->dropitem[i].nameid,
                     mob->dropitem[i].rate);
        }
    }
}

// Legacy method (still used in many places)
struct mob_db* mob2 = mob_get_db(1002);
if (mob2) {
    // Use mob2...
}
```

### **Working with Mob Data in Runtime**

```cpp
// Get mob data from a mob instance
struct mob_data *md;  // From somewhere (map, battle, etc.)

// Access database entry
std::shared_ptr<s_mob_db> db = mob_db.find(md->mob_id);

// Or use the db pointer directly (legacy)
struct mob_db *db2 = md->db;

// Get mob name
const char *name = md->db->name.c_str();

// Check mob AI
if (md->db->ai == 25) {  // AI 25 = Aggressive
    ShowInfo("This mob has aggressive AI\n");
}

// Modify mob stats (runtime only, doesn't change database)
md->status.max_hp = md->db->max_hp * 2;  // Double HP
status_calc_mob(md, SCO_NONE);
```

---

## Skill Database (skilldb)

### **struct s_skill_db** (skill.hpp)

```cpp
struct s_skill_db {
    uint16 nameid;                      // Skill ID
    char name[SKILL_NAME_LENGTH];       // Skill name
    char desc[SKILL_DESC_LENGTH];       // Description
    uint16 max;                         // Max level

    e_skill_inf inf;                    // Skill info flags
    e_skill_inf2 inf2;                  // Extended skill flags

    uint16 range[MAX_SKILL_LEVEL];      // Range per level
    uint16 hit;                         // Hit type
    e_skill_element element;            // Element
    uint16 splash[MAX_SKILL_LEVEL];     // Splash range per level

    uint16 max_count;                   // Max instances
    e_skill_type skill_type;            // Passive, offensive, etc.

    uint32 cast[MAX_SKILL_LEVEL];       // Cast time per level
    uint32 delay[MAX_SKILL_LEVEL];      // Delay per level
    uint32 cooldown[MAX_SKILL_LEVEL];   // Cooldown per level

    // Requirements
    struct {
        uint16 hp[MAX_SKILL_LEVEL];
        uint16 sp[MAX_SKILL_LEVEL];
        uint16 hp_rate[MAX_SKILL_LEVEL];
        uint16 sp_rate[MAX_SKILL_LEVEL];
        uint16 zeny[MAX_SKILL_LEVEL];

        struct {
            t_itemid id;
            uint16 amount;
        } itemid[MAX_SKILL_ITEM_REQUIRE];

        e_skill_state state;
        e_skill_unit_flag unit_flag;
    } require;

    // ... more fields
};
```

### **Accessing Skill Database**

```cpp
// Get skill by ID
std::shared_ptr<s_skill_db> skill = skill_db.find(AL_HEAL);
if (skill) {
    ShowInfo("Skill: %s, Max Level: %d\n", skill->name, skill->max);

    // Get cast time at level 10
    if (skill->max >= 10) {
        ShowInfo("Cast time lv10: %d ms\n", skill->cast[9]);  // Level 10 = index 9
    }

    // Check SP cost at level 5
    ShowInfo("SP cost lv5: %d\n", skill->require.sp[4]);

    // Check skill type
    if (skill->skill_type == BF_MAGIC) {
        ShowInfo("This is a magic skill\n");
    }
}

// Legacy method
struct s_skill_db* skill2 = skill_db.get(AL_HEAL);
```

### **Working with Skills in Runtime**

```cpp
// In skill casting functions (skill.cpp)
uint16 skill_id = AL_HEAL;
uint16 skill_lv = 10;

std::shared_ptr<s_skill_db> skill = skill_db.find(skill_id);
if (!skill) {
    ShowError("Skill %d not found in database!\n", skill_id);
    return 0;
}

// Get cast time for this skill level
int cast_time = skill->cast[skill_lv - 1];

// Apply cast time modifiers
cast_time = cast_time * (100 + sd->castrate) / 100;

// Get SP cost
int sp_cost = skill->require.sp[skill_lv - 1];

// Check if player has enough SP
if (sd->status.sp < sp_cost) {
    clif_skill_fail(sd, skill_id, USESKILL_FAIL_SP_INSUFFICIENT, 0);
    return 0;
}

// Consume SP
pc_payzeny(sd, -sp_cost, LOG_TYPE_CONSUME, NULL);
```

---

## Database Access Patterns

### **Pattern 1: Safe Access with Null Check**

```cpp
// Always check if the entry exists
std::shared_ptr<item_data> item = item_db.find(item_id);
if (!item) {
    ShowError("Item %d not found in database!\n", item_id);
    return 0;
}

// Use item safely
ShowInfo("Item: %s\n", item->name.c_str());
```

### **Pattern 2: Exists Check**

```cpp
// Check existence before detailed operations
if (!item_db.exists(custom_item_id)) {
    ShowWarning("Custom item %d not loaded!\n", custom_item_id);
    return;
}

std::shared_ptr<item_data> item = item_db.find(custom_item_id);
// Now guaranteed to exist
```

### **Pattern 3: Iterate All Entries**

```cpp
// Iterate all items (rarely needed, expensive)
for (auto &pair : item_db) {
    t_itemid item_id = pair.first;
    std::shared_ptr<item_data> item = pair.second;

    if (item->value_buy > 1000000) {
        ShowInfo("Expensive item: %s (%d zeny)\n",
                 item->name.c_str(),
                 item->value_buy);
    }
}
```

### **Pattern 4: Legacy Compatibility**

```cpp
// Many legacy functions still use raw pointers
struct item_data* item = itemdb_search(item_id);
// Always returns non-null (defaults to UNKNOWN_ITEM_ID if not found)

// Check if it's the unknown item
if (item->nameid == UNKNOWN_ITEM_ID) {
    ShowError("Invalid item!\n");
}
```

---

## Adding Custom Fields

### **Step 1: Modify Structure**

**Example**: Add custom field to `struct item_data`

**In src/map/itemdb.hpp**:
```cpp
struct item_data
{
    t_itemid nameid;
    std::string name, ename;
    // ... existing fields ...

    // *** CUSTOM FIELDS - Add at the end ***
    int custom_bonus;           // Custom stat bonus
    std::string custom_effect;  // Custom effect name
    bool custom_flag;           // Custom boolean flag
};
```

**Best Practice**: Add custom fields at the **end** of the struct to avoid breaking existing code.

---

### **Step 2: Initialize Custom Fields**

**In src/map/itemdb.cpp** (in `ItemDatabase::parseBodyNode`):

```cpp
uint64 ItemDatabase::parseBodyNode(const ryml::NodeRef& node) {
    t_itemid nameid;

    // Parse standard fields...

    // *** Initialize custom fields ***
    item->custom_bonus = 0;
    item->custom_effect = "";
    item->custom_flag = false;

    // Parse YAML nodes...

    // *** Parse custom YAML fields ***
    if (this->nodeExists(node, "CustomBonus")) {
        item->custom_bonus = this->asInt32(node, "CustomBonus");
    }

    if (this->nodeExists(node, "CustomEffect")) {
        item->custom_effect = this->asString(node, "CustomEffect");
    }

    if (this->nodeExists(node, "CustomFlag")) {
        item->custom_flag = this->asBool(node, "CustomFlag");
    }

    return 1;
}
```

---

### **Step 3: Add to YAML Database**

**In db/re/item_db.yml** (or db/import/item_db.yml for custom items):

```yaml
- Id: 60000
  AegisName: CustomSword
  Name: "Custom Legendary Sword"
  Type: Weapon
  SubType: 1hSword
  Buy: 1000000
  Sell: 500000
  Weight: 1500
  Attack: 250
  Range: 1
  Slots: 2
  Jobs:
    All: true
  Locations:
    Right_Hand: true
  WeaponLevel: 4
  EquipLevelMin: 99
  # *** Custom fields ***
  CustomBonus: 50
  CustomEffect: "flame_burst"
  CustomFlag: true
  Script: |
    bonus bAtk,50;
    bonus bCritical,10;
```

---

### **Step 4: Use Custom Fields in Code**

```cpp
// Anywhere in your code
std::shared_ptr<item_data> item = item_db.find(60000);
if (item) {
    // Use custom fields
    ShowInfo("Custom Bonus: %d\n", item->custom_bonus);
    ShowInfo("Custom Effect: %s\n", item->custom_effect.c_str());

    if (item->custom_flag) {
        // Apply special behavior
        clif_specialeffect(&sd->bl, EF_MAPPILLAR2, AREA);
    }
}

// In equipment bonus calculation (pc.cpp)
if (item && item->custom_bonus > 0) {
    sd->bonus.atk_rate += item->custom_bonus;
}
```

---

## Modifying Database Loading

### **Override parseBodyNode Method**

**Use Case**: Add custom validation or processing during database load

**In src/map/itemdb.cpp**:

```cpp
uint64 ItemDatabase::parseBodyNode(const ryml::NodeRef& node) {
    // Standard parsing...

    // *** Custom validation ***
    if (item->custom_bonus > 100) {
        ShowWarning("Item %d has excessive custom bonus (%d), capping to 100\n",
                    item->nameid, item->custom_bonus);
        item->custom_bonus = 100;
    }

    // *** Custom processing ***
    if (item->custom_effect == "auto_buff") {
        // Auto-add buff script
        item->flag.autoequip = 1;
    }

    // *** Logging ***
    if (item->custom_flag) {
        ShowInfo("Loaded custom item: %s (ID: %d)\n",
                 item->name.c_str(), item->nameid);
    }

    return 1;
}
```

---

### **Override loadingFinished Method**

**Use Case**: Post-processing after all database entries are loaded

**In src/map/itemdb.cpp**:

```cpp
void ItemDatabase::loadingFinished() {
    // Call parent implementation
    TypesafeCachedYamlDatabase::loadingFinished();

    // *** Custom post-processing ***
    int custom_count = 0;

    for (auto &pair : this->cache) {
        std::shared_ptr<item_data> item = pair.second;

        if (item->custom_flag) {
            custom_count++;

            // Auto-generate item links for custom items
            this->create_item_link_for_mes(item, true, item->name.c_str());
        }
    }

    ShowStatus("Loaded %d custom items with special flags.\n", custom_count);
}
```

---

## Complete Examples

### **Example 1: Custom Item Bonus System**

**Goal**: Items with `CustomBonus` field give extra stats when equipped

**1. Add field to item_data** (itemdb.hpp):
```cpp
struct item_data {
    // ... existing fields ...
    int custom_stat_bonus;  // 0-100
};
```

**2. Parse YAML field** (itemdb.cpp):
```cpp
if (this->nodeExists(node, "CustomStatBonus")) {
    item->custom_stat_bonus = this->asInt32(node, "CustomStatBonus");
} else {
    item->custom_stat_bonus = 0;
}
```

**3. Add to YAML** (item_db.yml):
```yaml
- Id: 60001
  AegisName: PowerRing
  Name: "Ring of Power"
  Type: Armor
  Locations:
    Right_Accessory: true
  CustomStatBonus: 25
```

**4. Apply bonus in pc.cpp** (in `pc_bonus` or `status_calc_pc`):
```cpp
// In status_calc_pc() after equipment calculation
for (int i = 0; i < EQI_MAX; i++) {
    int index = sd->equip_index[i];
    if (index < 0) continue;

    struct item_data *item = itemdb_search(sd->inventory.u.items_inventory[index].nameid);
    if (item && item->custom_stat_bonus > 0) {
        // Apply bonus
        sd->bonus.str += item->custom_stat_bonus;
        sd->bonus.agi += item->custom_stat_bonus;
        sd->bonus.vit += item->custom_stat_bonus;
        sd->bonus.int_ += item->custom_stat_bonus;
        sd->bonus.dex += item->custom_stat_bonus;
        sd->bonus.luk += item->custom_stat_bonus;

        ShowInfo("Applied custom stat bonus +%d from item %s\n",
                 item->custom_stat_bonus, item->name.c_str());
    }
}
```

---

### **Example 2: Custom Mob Behavior Flag**

**Goal**: Mobs with `CustomAggressive` flag always attack players on sight

**1. Add field to s_mob_db** (mob.hpp):
```cpp
struct s_mob_db {
    // ... existing fields ...
    bool custom_aggressive;
};
```

**2. Parse YAML field** (mob.cpp in `MobDatabase::parseBodyNode`):
```cpp
if (this->nodeExists(node, "CustomAggressive")) {
    mob->custom_aggressive = this->asBool(node, "CustomAggressive");
} else {
    mob->custom_aggressive = false;
}
```

**3. Add to YAML** (mob_db.yml):
```yaml
- Id: 20000
  AegisName: CUSTOM_DEMON
  Name: "Custom Demon"
  Level: 99
  Hp: 500000
  BaseExp: 100000
  JobExp: 50000
  CustomAggressive: true
```

**4. Check flag in mob AI** (mob.cpp in `mob_ai_sub_hard`):
```cpp
// In mob AI processing
if (md->db->custom_aggressive) {
    // Force aggressive behavior
    if (target_sd) {
        md->target_id = target_sd->bl.id;
        md->state.aggressive = 1;
        mob_attack(md, target_sd->bl.id, 0);
    }
}
```

---

### **Example 3: Custom Skill Requirement**

**Goal**: Skills with `CustomItemReq` require a custom currency item

**1. Add field to s_skill_db** (skill.hpp):
```cpp
struct s_skill_db {
    // ... existing fields ...
    struct {
        t_itemid custom_currency;
        uint16 custom_amount[MAX_SKILL_LEVEL];
    } custom_require;
};
```

**2. Parse YAML** (skill.cpp):
```cpp
if (this->nodeExists(node, "CustomRequire")) {
    auto custom_node = node["CustomRequire"];

    if (this->nodeExists(custom_node, "CurrencyItem")) {
        skill->custom_require.custom_currency = this->asUInt32(custom_node, "CurrencyItem");
    }

    if (this->nodeExists(custom_node, "Amount")) {
        for (int i = 0; i < MAX_SKILL_LEVEL; i++) {
            skill->custom_require.custom_amount[i] = this->asUInt16(custom_node["Amount"], i);
        }
    }
}
```

**3. Add to YAML** (skill_db.yml):
```yaml
- Id: 9000
  Name: "CUSTOM_ULTIMATE_SKILL"
  Description: "Ultimate Custom Skill"
  MaxLevel: 10
  CustomRequire:
    CurrencyItem: 60000  # Custom currency item
    Amount: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

**4. Check requirement** (skill.cpp in `skill_check_require`):
```cpp
std::shared_ptr<s_skill_db> skill = skill_db.find(skill_id);

if (skill && skill->custom_require.custom_currency > 0) {
    int required_amount = skill->custom_require.custom_amount[skill_lv - 1];

    int index = pc_search_inventory(sd, skill->custom_require.custom_currency);
    if (index < 0 || sd->inventory.u.items_inventory[index].amount < required_amount) {
        clif_skill_fail(sd, skill_id, USESKILL_FAIL_NEED_ITEM, required_amount);
        return 0;
    }

    // Consume custom currency
    pc_delitem(sd, index, required_amount, 0, 0, LOG_TYPE_CONSUME);
}
```

---

## Performance Tips

### **1. Cache Database Lookups**

```cpp
// ❌ BAD - Repeated database lookups
for (int i = 0; i < 1000; i++) {
    std::shared_ptr<item_data> item = item_db.find(501);
    // Process item...
}

// ✅ GOOD - Cache the result
std::shared_ptr<item_data> item = item_db.find(501);
if (item) {
    for (int i = 0; i < 1000; i++) {
        // Process item...
    }
}
```

### **2. Use Exists Check Before Heavy Operations**

```cpp
// ✅ GOOD - Fast existence check first
if (!item_db.exists(custom_id)) {
    return;
}

// Now do expensive operations
std::shared_ptr<item_data> item = item_db.find(custom_id);
// ... heavy processing ...
```

### **3. Avoid Iterating Entire Database**

```cpp
// ❌ BAD - Iterates all items every frame
for (auto &pair : item_db) {
    if (pair.second->type == IT_WEAPON) {
        // Do something
    }
}

// ✅ GOOD - Pre-cache weapon list at startup
std::vector<std::shared_ptr<item_data>> weapon_cache;

void cache_weapons() {
    for (auto &pair : item_db) {
        if (pair.second->type == IT_WEAPON) {
            weapon_cache.push_back(pair.second);
        }
    }
}

// Use cached list
for (auto &weapon : weapon_cache) {
    // Fast access
}
```

---

## Common Pitfalls

### **1. Not Checking Null Pointers**

```cpp
// ❌ WRONG - Crashes if item doesn't exist
std::shared_ptr<item_data> item = item_db.find(999999);
ShowInfo("Item: %s\n", item->name.c_str());  // CRASH!

// ✅ CORRECT - Always check
std::shared_ptr<item_data> item = item_db.find(999999);
if (item) {
    ShowInfo("Item: %s\n", item->name.c_str());
} else {
    ShowError("Item not found!\n");
}
```

### **2. Off-by-One Errors with Skill Levels**

```cpp
// ❌ WRONG - Skill levels are 1-indexed, arrays are 0-indexed
uint16 skill_lv = 10;
int cast_time = skill->cast[skill_lv];  // Out of bounds!

// ✅ CORRECT - Subtract 1 for array index
uint16 skill_lv = 10;
int cast_time = skill->cast[skill_lv - 1];
```

### **3. Modifying Database Structs (Unsafe)**

```cpp
// ❌ WRONG - Modifying shared database entry affects ALL instances
std::shared_ptr<item_data> item = item_db.find(501);
item->value_buy = 999999;  // Now ALL Red Potions cost 999999!

// ✅ CORRECT - Copy if you need to modify
std::shared_ptr<item_data> item = item_db.find(501);
item_data temp_item = *item;  // Copy
temp_item.value_buy = 999999;  // Modify copy
// Use temp_item...
```

### **4. Forgetting to Initialize Custom Fields**

```cpp
// ❌ WRONG - Custom field contains garbage data
struct item_data {
    int custom_bonus;  // Uninitialized!
};

// ✅ CORRECT - Always initialize in parseBodyNode
item->custom_bonus = 0;
if (this->nodeExists(node, "CustomBonus")) {
    item->custom_bonus = this->asInt32(node, "CustomBonus");
}
```

### **5. Using Legacy Methods Incorrectly**

```cpp
// ⚠️ LEGACY - Always returns non-null (defaults to UNKNOWN_ITEM_ID)
struct item_data* item = itemdb_search(999999);
if (!item) {  // This will NEVER be true!
    ShowError("Item not found!\n");
}

// ✅ CORRECT - Check against UNKNOWN_ITEM_ID
struct item_data* item = itemdb_search(999999);
if (item->nameid == UNKNOWN_ITEM_ID) {
    ShowError("Item not found!\n");
}

// OR use modern method
std::shared_ptr<item_data> item = item_db.find(999999);
if (!item) {
    ShowError("Item not found!\n");
}
```

---

## Related References

- **Source Code Structure**: [KB_REF_SourceCodeStructure.md]
- **Script Command Creation**: [KB_REF_ScriptCommandCreation.md]
- **Customization System**: [KB_REF_PluginSystem.md]
- **Best Practices**: [KB_REF_SourceCodeBestPractices.md]

---

**End of KB_REF_025 - Working with Databases in C++**
