# rAthena Database Systems in C++ - Complete Reference

**Version:** 2.0
**Last Updated:** 2025-11-18
**Scope:** YAML & SQL database operations, TypesafeCachedYamlDatabase pattern, parsing, validation, and real-world examples

---

## Table of Contents

1. [Overview](#overview)
2. [Database Class Hierarchy](#database-class-hierarchy)
3. [TypesafeCachedYamlDatabase Template Pattern](#typesafecachedyamldatabase-template-pattern)
4. [Accessing Databases](#accessing-databases)
5. [YAML Parsing Fundamentals](#yaml-parsing-fundamentals)
6. [Adding Custom Fields to Structs](#adding-custom-fields-to-structs)
7. [Validation and Error Handling](#validation-and-error-handling)
8. [Caching and Performance](#caching-and-performance)
9. [Iterating Databases](#iterating-databases)
10. [Reloading Databases](#reloading-databases)
11. [SQL Database Access](#sql-database-access)
12. [Real-World Examples](#real-world-examples)
13. [Common Patterns and Best Practices](#common-patterns-and-best-practices)

---

## Overview

rAthena uses two primary database systems:

1. **YAML Databases** - For game configuration (items, mobs, skills, etc.)
   - File-based, human-readable configuration
   - Hot-reloadable via @commands
   - Uses TypesafeCachedYamlDatabase template for type safety and performance

2. **SQL Databases** - For persistent game data (characters, guilds, storage, etc.)
   - MySQL/MariaDB backend
   - Character data, inventory, guild information
   - Uses prepared statements for security and performance

**Key Files:**
- `/home/user/rathena2/src/common/database.hpp` - Base database classes
- `/home/user/rathena2/src/common/database.cpp` - YAML parsing implementation
- `/home/user/rathena2/src/common/sql.hpp` - SQL wrapper classes
- `/home/user/rathena2/src/map/itemdb.hpp` - Item database (YAML example)
- `/home/user/rathena2/src/map/mob.hpp` - Mob database (YAML example)

---

## Database Class Hierarchy

### Class Structure

```
YamlDatabase (abstract base)
    ↓
TypesafeYamlDatabase<keytype, datatype> (template)
    ↓
TypesafeCachedYamlDatabase<keytype, datatype> (template with vector caching)
    ↓
ItemDatabase, MobDatabase, SkillDatabase, etc. (concrete implementations)
```

### YamlDatabase (Base Class)

**Location:** `/home/user/rathena2/src/common/database.hpp:19`

```cpp
class YamlDatabase {
private:
    std::string type;           // Database type identifier (e.g., "ITEM_DB")
    uint16 version;             // Current version supported
    uint16 minimumVersion;      // Minimum compatible version
    std::string currentFile;    // Currently loading file path
    ryml::Parser parser;        // YAML parser instance

protected:
    // Helper functions for parsing
    bool nodeExists(const ryml::NodeRef& node, const std::string& name);
    bool nodesExist(const ryml::NodeRef& node, std::initializer_list<const std::string> names);

    // Type conversion functions
    bool asBool(const ryml::NodeRef& node, const std::string& name, bool& out);
    bool asInt16(const ryml::NodeRef& node, const std::string& name, int16& out);
    bool asUInt16(const ryml::NodeRef& node, const std::string& name, uint16& out);
    bool asInt32(const ryml::NodeRef& node, const std::string& name, int32& out);
    bool asUInt32(const ryml::NodeRef& node, const std::string& name, uint32& out);
    bool asInt64(const ryml::NodeRef& node, const std::string& name, int64& out);
    bool asUInt64(const ryml::NodeRef& node, const std::string& name, uint64& out);
    bool asFloat(const ryml::NodeRef& node, const std::string& name, float& out);
    bool asDouble(const ryml::NodeRef& node, const std::string& name, double& out);
    bool asString(const ryml::NodeRef& node, const std::string& name, std::string& out);
    bool asUInt16Rate(const ryml::NodeRef& node, const std::string& name, uint16& out, uint16 maximum=10000);
    bool asUInt32Rate(const ryml::NodeRef& node, const std::string& name, uint32& out, uint32 maximum=10000);

    void invalidWarning(const ryml::NodeRef& node, const char* fmt, ...);
    virtual void loadingFinished();

public:
    YamlDatabase(const std::string& type_, uint16 version_, uint16 minimumVersion_);

    bool load();
    bool reload();

    // Must be implemented by derived classes
    virtual void clear() = 0;
    virtual const std::string getDefaultLocation() = 0;
    virtual uint64 parseBodyNode(const ryml::NodeRef& node) = 0;
};
```

### TypesafeYamlDatabase Template

**Location:** `/home/user/rathena2/src/common/database.hpp:84`

```cpp
template <typename keytype, typename datatype>
class TypesafeYamlDatabase : public YamlDatabase {
protected:
    std::unordered_map<keytype, std::shared_ptr<datatype>> data;

public:
    TypesafeYamlDatabase(const std::string& type_, uint16 version_, uint16 minimumVersion_);

    void clear() override {
        this->data.clear();
    }

    bool empty() {
        return this->data.empty();
    }

    // Check if entry exists
    bool exists(keytype key) {
        return this->find(key) != nullptr;
    }

    // Find entry by key (returns nullptr if not found)
    virtual std::shared_ptr<datatype> find(keytype key) {
        auto it = this->data.find(key);
        if (it != this->data.end()) {
            return it->second;
        }
        return nullptr;
    }

    // Add/update entry
    virtual void put(keytype key, std::shared_ptr<datatype> ptr) {
        this->data[key] = ptr;
    }

    // Iteration support
    typename std::unordered_map<keytype, std::shared_ptr<datatype>>::iterator begin();
    typename std::unordered_map<keytype, std::shared_ptr<datatype>>::iterator end();

    size_t size();
    std::shared_ptr<datatype> random();
    virtual void erase(keytype key);
};
```

### TypesafeCachedYamlDatabase Template

**Location:** `/home/user/rathena2/src/common/database.hpp:146`

**Purpose:** Optimizes lookups by maintaining a vector cache for fast O(1) access by numeric IDs.

```cpp
template <typename keytype, typename datatype>
class TypesafeCachedYamlDatabase : public TypesafeYamlDatabase<keytype, datatype> {
private:
    std::vector<std::shared_ptr<datatype>> cache;  // Fast lookup cache
    bool loaded;

public:
    TypesafeCachedYamlDatabase(const std::string& type_, uint16 version_, uint16 minimumVersion_);

    void clear() override {
        TypesafeYamlDatabase<keytype, datatype>::clear();
        cache.clear();
        cache.shrink_to_fit();
        this->loaded = false;
    }

    // Overridden find() - uses cache for fast lookup
    std::shared_ptr<datatype> find(keytype key) override {
        if (this->cache.empty() || key >= this->cache.size()) {
            return TypesafeYamlDatabase<keytype, datatype>::find(key);
        }
        return cache[this->calculateCacheKey(key)];
    }

    // Override to customize cache key calculation
    virtual size_t calculateCacheKey(keytype key) {
        return key;
    }

    // Called after database loading completes
    void loadingFinished() override;
};
```

**Caching Strategy:**
- After all entries are loaded, `loadingFinished()` builds a vector cache
- Vector is sized to fit the highest key value + 1
- Direct array access via `cache[key]` provides O(1) lookup
- Fallback to hash map for keys outside cache range

---

## TypesafeCachedYamlDatabase Template Pattern

### Database Implementations in rAthena

**Common Implementations:**

```cpp
// Item Database - Cached by item ID
class ItemDatabase : public TypesafeCachedYamlDatabase<t_itemid, item_data> {
public:
    ItemDatabase() : TypesafeCachedYamlDatabase("ITEM_DB", 3, 1) {}

    const std::string getDefaultLocation() override;
    uint64 parseBodyNode(const ryml::NodeRef& node) override;
    void loadingFinished() override;

    // Additional lookup methods
    std::shared_ptr<item_data> searchname(const char* name);
    std::shared_ptr<item_data> search_aegisname(const char* name);
};

extern ItemDatabase item_db;  // Global instance


// Mob Database - Cached by mob ID
class MobDatabase : public TypesafeCachedYamlDatabase<uint32, s_mob_db> {
public:
    MobDatabase() : TypesafeCachedYamlDatabase("MOB_DB", 5, 1) {}

    const std::string getDefaultLocation() override;
    uint64 parseBodyNode(const ryml::NodeRef& node) override;
    void loadingFinished() override;
};

extern MobDatabase mob_db;  // Global instance


// Skill Database - Cached by skill ID
class SkillDatabase : public TypesafeCachedYamlDatabase<uint16, s_skill_db> {
private:
    uint16 skilldb_id2idx[(UINT16_MAX + 1)];  // Additional index mapping
    uint16 skill_num;

public:
    SkillDatabase() : TypesafeCachedYamlDatabase("SKILL_DB", 4) {
        this->clear();
    }

    const std::string getDefaultLocation() override;
    uint64 parseBodyNode(const ryml::NodeRef& node) override;
    void clear() override;
    void loadingFinished() override;

    uint16 get_index(uint16 skill_id, bool silent, const char* func, const char* file, int32 line);
};

extern SkillDatabase skill_db;  // Global instance
```

### Other Database Types

**Non-Cached Databases (TypesafeYamlDatabase):**
- Used when caching isn't beneficial (string keys, sparse IDs, small datasets)

```cpp
// Achievement Database (no caching, uses uint32 key)
class AchievementDatabase : public TypesafeYamlDatabase<uint32, s_achievement_db> {
public:
    AchievementDatabase() : TypesafeYamlDatabase("ACHIEVEMENT_DB", 2) {}
    // ...
};

// Quest Database (string key)
class QuestDatabase : public TypesafeYamlDatabase<uint32, s_quest_db> {
public:
    QuestDatabase() : TypesafeYamlDatabase("QUEST_DB", 2) {}
    // ...
};

// Barter Database (string key)
class BarterDatabase : public TypesafeYamlDatabase<std::string, s_npc_barter> {
public:
    BarterDatabase() : TypesafeYamlDatabase("BARTER_DB", 1) {}
    // ...
};
```

---

## Accessing Databases

### Basic Access Pattern: find() Method

**Always use find() and check for nullptr!**

```cpp
// Item database lookup
std::shared_ptr<item_data> item = item_db.find(item_id);
if (item == nullptr) {
    ShowError("Item %d not found in database!\n", item_id);
    return false;
}

// Now safe to use item->
ShowInfo("Item: %s (ID: %d)\n", item->name.c_str(), item->nameid);
```

### Using exists() for Quick Checks

```cpp
// Check if item exists without retrieving data
if (!item_db.exists(item_id)) {
    clif_displaymessage(fd, "Item does not exist!");
    return -1;
}
```

### Real Examples from Codebase

**Example 1: Mob Database Lookup**
**Source:** `/home/user/rathena2/src/map/pet.cpp:563`

```cpp
// Relink pet to mob database entry
pd->db = mob_db.find(pet_db_ptr->class_);

// Later, check before using
if (pd->db == nullptr) {
    ShowError("Pet mob class %d not found in mob database!\n", pet_db_ptr->class_);
    return false;
}
```

**Example 2: Item Database with Validation**
**Source:** `/home/user/rathena2/src/map/pc.cpp:3305`

```cpp
if (nameid && !item_db.exists(nameid)) {
    ShowError("Invalid item ID %d specified!\n", nameid);
    return false;
}

std::shared_ptr<item_data> id = item_db.find(nameid);
```

**Example 3: Mob Database in Script Command**
**Source:** `/home/user/rathena2/src/map/script.cpp:11130`

```cpp
std::shared_ptr<s_mob_db> mdb = mob_db.find(pet->class_);

if (mdb == nullptr) {
    ShowError("script:makepet: Invalid mob class %d\n", pet->class_);
    return false;
}

intif_create_pet(sd->status.account_id, sd->status.char_id,
                 pet->class_, mdb->lv, pet->EggID, 0,
                 pet->intimate, 100, 0, 1, mdb->jname.c_str());
```

**Example 4: Skill Database Existence Check**
**Source:** `/home/user/rathena2/src/map/mob.cpp:6496`

```cpp
if (!skill_db.exists(skill_id)) {
    ShowWarning("Mob %d has invalid skill %d in skill tree\n", mob_id, skill_id);
    continue;
}
```

**Example 5: Conditional Lookup**
**Source:** `/home/user/rathena2/src/map/map.cpp:2045`

```cpp
if (!extend_protection && mob_id > 0) {
    // Boss and MVP drops both have prolonged loot protection
    if (auto mob = mob_db.find(mob_id); mob != nullptr && mob->get_bosstype() != BOSSTYPE_NONE)
        extend_protection = true;
}
```

### Common Access Patterns

```cpp
// Pattern 1: Simple lookup with nullptr check
std::shared_ptr<item_data> item = item_db.find(item_id);
if (item == nullptr)
    return false;

// Pattern 2: Early return on missing data
if (!mob_db.exists(mob_id))
    return;
std::shared_ptr<s_mob_db> mob = mob_db.find(mob_id);

// Pattern 3: C++17 if-init statement (modern, preferred)
if (auto item = item_db.find(item_id); item != nullptr) {
    // Use item here
    ShowInfo("Found: %s\n", item->name.c_str());
}

// Pattern 4: Optional chaining pattern
auto mob = mob_db.find(mob_id);
if (mob && mob->get_bosstype() == BOSSTYPE_MVP) {
    // Handle MVP
}
```

### Performance Considerations

**Cached databases (TypesafeCachedYamlDatabase):**
- `find()` is O(1) for IDs within cache range
- `exists()` calls `find()` internally (same performance)
- Cache is built once at startup/reload

**Non-cached databases (TypesafeYamlDatabase):**
- `find()` is O(1) hash map lookup
- `exists()` has same performance as `find()`

**Recommendation:** Always prefer `find()` + nullptr check over `exists()` + `find()` to avoid double lookup.

```cpp
// INEFFICIENT - Two lookups
if (item_db.exists(item_id)) {
    auto item = item_db.find(item_id);  // Second lookup!
    // use item
}

// EFFICIENT - One lookup
auto item = item_db.find(item_id);
if (item != nullptr) {
    // use item
}
```

---

## YAML Parsing Fundamentals

### parseBodyNode() - Core Parsing Method

Every database must implement `parseBodyNode()` to parse individual entries.

**Signature:**
```cpp
virtual uint64 parseBodyNode(const ryml::NodeRef& node) = 0;
```

**Return Value:**
- `1` on success (entry parsed)
- `0` on failure (entry skipped)

### Basic Parsing Structure

**Example from ItemDatabase:**
**Source:** `/home/user/rathena2/src/map/itemdb.cpp:49`

```cpp
uint64 ItemDatabase::parseBodyNode(const ryml::NodeRef& node) {
    t_itemid nameid;

    // 1. Parse primary key (required)
    if (!this->asUInt32(node, "Id", nameid))
        return 0;

    // 2. Check if entry already exists (for updates)
    std::shared_ptr<item_data> item = this->find(nameid);
    bool exists = item != nullptr;

    // 3. For new entries, validate required fields
    if (!exists) {
        if (!this->nodesExist(node, { "AegisName", "Name" }))
            return 0;

        // Create new entry
        item = std::make_shared<item_data>();
        item->nameid = nameid;
        item->flag.available = true;
    }

    // 4. Parse optional fields with nodeExists() checks
    if (this->nodeExists(node, "Type")) {
        std::string type;
        if (!this->asString(node, "Type", type))
            return 0;

        // Convert string to enum/constant
        std::string type_constant = "IT_" + type;
        int64 constant;
        if (!script_get_constant(type_constant.c_str(), &constant)) {
            this->invalidWarning(node["Type"], "Invalid item type %s, defaulting to IT_ETC.\n", type.c_str());
            constant = IT_ETC;
        }
        item->type = static_cast<item_types>(constant);
    } else {
        if (!exists)
            item->type = IT_ETC;  // Default value
    }

    if (this->nodeExists(node, "Buy")) {
        uint32 buy;
        if (!this->asUInt32(node, "Buy", buy))
            return 0;

        if (buy > MAX_ZENY) {
            this->invalidWarning(node["Buy"], "Buying price exceeds MAX_ZENY. Capping...\n");
            buy = MAX_ZENY;
        }
        item->value_buy = buy;
    } else {
        if (!exists)
            item->value_buy = 0;
    }

    // 5. Store entry in database
    if (!exists)
        this->put(nameid, item);

    return 1;
}
```

### YAML Helper Functions

**All helper functions are in YamlDatabase base class.**

#### Node Existence Checks

```cpp
// Check if a single node exists
bool nodeExists(const ryml::NodeRef& node, const std::string& name);

// Check if multiple nodes exist (all required)
bool nodesExist(const ryml::NodeRef& node, std::initializer_list<const std::string> names);
```

**Usage:**
```cpp
// Single check
if (this->nodeExists(node, "Weight")) {
    // Parse Weight field
}

// Multiple required fields
if (!this->nodesExist(node, { "AegisName", "Name", "Type" }))
    return 0;  // Missing required fields
```

#### Type Conversion Functions

**Integer Types:**
```cpp
bool asInt16(const ryml::NodeRef& node, const std::string& name, int16& out);
bool asUInt16(const ryml::NodeRef& node, const std::string& name, uint16& out);
bool asInt32(const ryml::NodeRef& node, const std::string& name, int32& out);
bool asUInt32(const ryml::NodeRef& node, const std::string& name, uint32& out);
bool asInt64(const ryml::NodeRef& node, const std::string& name, int64& out);
bool asUInt64(const ryml::NodeRef& node, const std::string& name, uint64& out);
```

**Example:**
```cpp
if (this->nodeExists(node, "Attack")) {
    uint32 atk;
    if (!this->asUInt32(node, "Attack", atk))
        return 0;
    item->atk = atk;
}
```

**Floating Point:**
```cpp
bool asFloat(const ryml::NodeRef& node, const std::string& name, float& out);
bool asDouble(const ryml::NodeRef& node, const std::string& name, double& out);
```

**String:**
```cpp
bool asString(const ryml::NodeRef& node, const std::string& name, std::string& out);
```

**Example:**
```cpp
if (this->nodeExists(node, "AegisName")) {
    std::string name;
    if (!this->asString(node, "AegisName", name))
        return 0;

    if (name.length() > ITEM_NAME_LENGTH) {
        this->invalidWarning(node["AegisName"],
            "AegisName \"%s\" exceeds maximum of %d characters, capping...\n",
            name.c_str(), ITEM_NAME_LENGTH - 1);
    }
    item->name = name;
}
```

**Boolean:**
```cpp
bool asBool(const ryml::NodeRef& node, const std::string& name, bool& out);
```

**Rate Values (percentages):**
```cpp
// Parses percentage values (e.g., "50%" → 5000 out of 10000)
bool asUInt16Rate(const ryml::NodeRef& node, const std::string& name, uint16& out, uint16 maximum=10000);
bool asUInt32Rate(const ryml::NodeRef& node, const std::string& name, uint32& out, uint32 maximum=10000);
```

### Error Reporting

```cpp
void invalidWarning(const ryml::NodeRef& node, const char* fmt, ...);

// Usage:
this->invalidWarning(node["Defense"],
    "Item defense %d exceeds DEFTYPE_MAX (%d), capping to DEFTYPE_MAX.\n",
    def, DEFTYPE_MAX);
```

### Parsing Sub-Nodes and Arrays

**Example: Parsing nested structures**

```cpp
if (this->nodeExists(node, "Drops")) {
    const auto& dropsNode = node["Drops"];

    for (const auto& dropNode : dropsNode) {
        t_itemid item_id;
        uint16 rate;

        if (!this->asUInt32(dropNode, "Item", item_id))
            continue;
        if (!this->asUInt16Rate(dropNode, "Rate", rate))
            continue;

        // Add drop to list
        std::shared_ptr<s_mob_drop> drop = std::make_shared<s_mob_drop>();
        drop->nameid = item_id;
        drop->rate = rate;
        mob->dropitem.push_back(drop);
    }
}
```

### Complete Real Example: Mob Stats Parsing

**Source:** `/home/user/rathena2/src/map/mob.cpp:5200`

```cpp
// Parse Dex stat
if (this->nodeExists(node, "Dex")) {
    uint16 stat;
    if (!this->asUInt16(node, "Dex", stat))
        return 0;
    mob->status.dex = max(0, stat);
}

// Parse Size enum
if (this->nodeExists(node, "Size")) {
    std::string size;
    if (!this->asString(node, "Size", size))
        return 0;

    std::string size_constant = "Size_" + size;
    int64 constant;

    if (!script_get_constant(size_constant.c_str(), &constant)) {
        this->invalidWarning(node["Size"], "Unknown monster size %s, defaulting to Small.\n", size.c_str());
        constant = SZ_SMALL;
    }

    if (constant < SZ_SMALL || constant > SZ_BIG) {
        this->invalidWarning(node["Size"], "Invalid monster size %s, defaulting to Small.\n", size.c_str());
        constant = SZ_SMALL;
    }

    mob->status.size = static_cast<e_size>(constant);
}

// Parse race groups (array)
if (this->nodeExists(node, "RaceGroups")) {
    const auto& raceNode = node["RaceGroups"];

    for (const auto& raceit : raceNode) {
        std::string raceName;
        c4::from_chars(raceit.key(), &raceName);
        std::string raceName_constant = "RC2_" + raceName;
        int64 constant;

        if (!script_get_constant(raceName_constant.c_str(), &constant)) {
            this->invalidWarning(raceNode[raceit.key()],
                "Unknown monster race group %s, skipping.\n", raceName.c_str());
            continue;
        }

        mob->race2 |= constant;
    }
}
```

---

## Adding Custom Fields to Structs

### Step-by-Step Process

**Scenario:** Adding a custom "bonus_exp" field to items

#### Step 1: Modify the Data Structure

**File:** `/home/user/rathena2/src/map/itemdb.hpp`

```cpp
struct item_data {
    t_itemid nameid;
    std::string name;
    std::string ename;
    item_types type;
    uint32 weight;
    uint32 value_buy;
    uint32 value_sell;
    uint32 atk;
    uint32 def;
    // ... existing fields ...

    // ADD YOUR CUSTOM FIELD HERE
    uint32 bonus_exp;  // Custom: Bonus EXP when consuming item

    // Constructor can initialize default
    item_data() : bonus_exp(0) {
        // ... other defaults ...
    }
};
```

#### Step 2: Add Parsing Logic

**File:** `/home/user/rathena2/src/map/itemdb.cpp` in `parseBodyNode()`

```cpp
uint64 ItemDatabase::parseBodyNode(const ryml::NodeRef& node) {
    // ... existing parsing code ...

    // ADD PARSING FOR YOUR CUSTOM FIELD
    if (this->nodeExists(node, "BonusExp")) {
        uint32 exp;

        if (!this->asUInt32(node, "BonusExp", exp))
            return 0;

        // Optional: Add validation
        if (exp > 1000000) {
            this->invalidWarning(node["BonusExp"],
                "BonusExp %d exceeds maximum, capping to 1000000.\n", exp);
            exp = 1000000;
        }

        item->bonus_exp = exp;
    } else {
        if (!exists)
            item->bonus_exp = 0;  // Default value for new items
    }

    // ... rest of parsing ...

    return 1;
}
```

#### Step 3: Use the Custom Field

**File:** `/home/user/rathena2/src/map/pc.cpp` or wherever items are consumed

```cpp
// When item is used/consumed
std::shared_ptr<item_data> item = item_db.find(item_id);
if (item == nullptr)
    return false;

// Access your custom field
if (item->bonus_exp > 0) {
    pc_gainexp(sd, NULL, item->bonus_exp, 0, 0);
    clif_displaymessage(sd->fd, "You gained bonus experience!");
}
```

#### Step 4: Update YAML Database File

**File:** `db/re/item_db.yml` or `db/pre-re/item_db.yml`

```yaml
Body:
  - Id: 12345
    AegisName: "Exp_Potion"
    Name: "Experience Potion"
    Type: "Usable"
    Buy: 5000
    Weight: 100
    BonusExp: 10000  # Your custom field
    Script: |
      // Item usage script
```

### Real Example: Adding Custom Drop Rates

**Mob Database Custom Field Example:**

```cpp
// In s_mob_db struct (mob.hpp)
struct s_mob_db {
    uint32 mob_id;
    std::string sprite;
    std::string name;
    std::string jname;
    uint16 lv;
    // ... existing fields ...

    // CUSTOM: Global drop rate multiplier
    uint16 drop_rate_multiplier;  // In basis points (10000 = 100%)
};

// In MobDatabase::parseBodyNode() (mob.cpp)
if (this->nodeExists(node, "DropRateMultiplier")) {
    uint16 multiplier;
    if (!this->asUInt16Rate(node, "DropRateMultiplier", multiplier))
        return 0;
    mob->drop_rate_multiplier = multiplier;
} else {
    if (!exists)
        mob->drop_rate_multiplier = 10000;  // 100% default
}

// Usage in drop calculation (mob.cpp)
int32 effective_rate = (base_rate * mob->drop_rate_multiplier) / 10000;
```

---

## Validation and Error Handling

### Common Validation Patterns

#### Range Validation

```cpp
// Validate value within range
if (this->nodeExists(node, "Defense")) {
    uint32 def;
    if (!this->asUInt32(node, "Defense", def))
        return 0;

    if (def > DEFTYPE_MAX) {
        this->invalidWarning(node["Defense"],
            "Item defense %d exceeds DEFTYPE_MAX (%d), capping to DEFTYPE_MAX.\n",
            def, DEFTYPE_MAX);
        def = DEFTYPE_MAX;
    }

    item->def = def;
}
```

#### Currency/Zeny Validation

```cpp
if (this->nodeExists(node, "Buy")) {
    uint32 buy;
    if (!this->asUInt32(node, "Buy", buy))
        return 0;

    if (buy > MAX_ZENY) {
        this->invalidWarning(node["Buy"], "Buying price exceeds MAX_ZENY. Capping...\n");
        buy = MAX_ZENY;
    }

    item->value_buy = buy;
}
```

#### String Length Validation

```cpp
if (this->nodeExists(node, "Name")) {
    std::string name;
    if (!this->asString(node, "Name", name))
        return 0;

    if (name.length() > ITEM_NAME_LENGTH) {
        this->invalidWarning(node["Name"],
            "Name \"%s\" exceeds maximum of %d characters, capping...\n",
            name.c_str(), ITEM_NAME_LENGTH - 1);
    }

    item->ename.resize(ITEM_NAME_LENGTH);
    item->ename = name.c_str();
}
```

#### Enum/Constant Validation

```cpp
if (this->nodeExists(node, "Type")) {
    std::string type;
    if (!this->asString(node, "Type", type))
        return 0;

    std::string type_constant = "IT_" + type;
    int64 constant;

    if (!script_get_constant(type_constant.c_str(), &constant) ||
        constant < IT_HEALING || constant >= IT_MAX) {
        this->invalidWarning(node["Type"],
            "Invalid item type %s, defaulting to IT_ETC.\n", type.c_str());
        constant = IT_ETC;
    }

    item->type = static_cast<item_types>(constant);
}
```

#### Cross-Reference Validation

```cpp
// Validate referenced item exists in database
if (this->nodeExists(node, "RequiredItem")) {
    t_itemid required_id;
    if (!this->asUInt32(node, "RequiredItem", required_id))
        return 0;

    if (!item_db.exists(required_id)) {
        this->invalidWarning(node["RequiredItem"],
            "Required item %d does not exist in item database, skipping.\n", required_id);
        return 0;
    }

    item->required_item = required_id;
}
```

#### Duplicate Prevention

**Example:** Prevent duplicate Aegis names

```cpp
if (this->nodeExists(node, "AegisName")) {
    std::string name;
    if (!this->asString(node, "AegisName", name))
        return 0;

    // Check for existing entry with same Aegis name
    std::shared_ptr<item_data> id = item_db.search_aegisname(name.c_str());

    if (id != nullptr && id->nameid != nameid) {
        this->invalidWarning(node["AegisName"],
            "Found duplicate item Aegis name for %s, skipping.\n", name.c_str());
        return 0;  // Reject duplicate
    }

    item->name = name;
}
```

### Runtime Validation (In Game Code)

```cpp
// Validate at point of use
bool validate_item_usage(map_session_data* sd, t_itemid item_id) {
    // Check item exists
    std::shared_ptr<item_data> item = item_db.find(item_id);
    if (item == nullptr) {
        ShowError("validate_item_usage: Item %d not found!\n", item_id);
        return false;
    }

    // Check item type
    if (item->type != IT_USABLE && item->type != IT_HEALING) {
        clif_displaymessage(sd->fd, "This item cannot be used.");
        return false;
    }

    // Check player has item
    int16 idx = pc_search_inventory(sd, item_id);
    if (idx < 0) {
        clif_displaymessage(sd->fd, "You don't have this item.");
        return false;
    }

    return true;
}
```

---

## Caching and Performance

### TypesafeCachedYamlDatabase Internals

#### Cache Building Process

**Source:** `/home/user/rathena2/src/common/database.hpp:183`

```cpp
void loadingFinished() override {
    size_t max_key = 0;

    // Cache all known values
    for (auto& pair : *this) {
        // Calculate the key that should be used
        size_t key = this->calculateCacheKey(pair.first);

        // Check if the key fits into the current cache size
        if (this->cache.capacity() <= key) {
            // Some keys compute to 0, so we allocate a minimum of 500 (250*2) entries
            const static size_t minimum = 250;
            // Double the current size, so we do not have to resize that often
            size_t new_size = std::max(key, minimum) * 2;

            // Very important => initialize everything to nullptr
            this->cache.resize(new_size, nullptr);
        }

        // Insert the value into the cache
        this->cache[key] = pair.second;

        // Keep track of highest known key for easy resize
        max_key = std::max(max_key, key);
    }

    // Resize to only fit all existing non-null entries
    this->cache.resize(max_key + 1);
    // Free the memory that was allocated too much
    this->cache.shrink_to_fit();
    this->loaded = true;
}
```

#### Cache Lookup

```cpp
std::shared_ptr<datatype> find(keytype key) override {
    // Fast path: Use cache if available
    if (this->cache.empty() || key >= this->cache.size()) {
        // Fallback to hash map for keys outside cache
        return TypesafeYamlDatabase<keytype, datatype>::find(key);
    }

    // O(1) direct vector access
    return cache[this->calculateCacheKey(key)];
}
```

### Performance Characteristics

| Operation | TypesafeYamlDatabase | TypesafeCachedYamlDatabase |
|-----------|---------------------|---------------------------|
| `find()` (in range) | O(1) hash map | O(1) vector access (faster) |
| `find()` (out of range) | O(1) hash map | O(1) hash map (fallback) |
| `exists()` | O(1) hash map | O(1) vector access |
| Iteration | O(n) | O(n) |
| Memory | ~24 bytes/entry | ~24 bytes/entry + vector |

**Vector vs Hash Map:**
- Vector: ~8 bytes overhead per entry (pointer)
- Hash Map: ~24 bytes overhead per entry (node, hash, pointers)
- Cache vector trades memory for speed on hot path lookups

### std::shared_ptr Usage

**Why shared_ptr?**
1. **Automatic memory management** - No manual delete needed
2. **Safe references** - Multiple systems can hold pointers safely
3. **Reference counting** - Memory freed when last reference goes away
4. **Const correctness** - Can return const shared_ptr<const T>

**Example:**
```cpp
// Database stores shared_ptr
std::unordered_map<t_itemid, std::shared_ptr<item_data>> data;

// Multiple places can reference same item safely
std::shared_ptr<item_data> item1 = item_db.find(501);  // Red Potion
std::shared_ptr<item_data> item2 = item_db.find(501);  // Same Red Potion

// Both point to same memory (reference counted)
assert(item1.get() == item2.get());

// Memory freed automatically when last reference destroyed
```

**Performance Notes:**
- Creating `shared_ptr`: ~20 CPU cycles
- Copying `shared_ptr`: ~5 CPU cycles (increment refcount)
- Raw pointer dereference: 1 CPU cycle
- Recommendation: Store `shared_ptr`, pass by reference where possible

```cpp
// GOOD: Pass by reference in functions
void process_item(const std::shared_ptr<item_data>& item) {
    // No refcount increment
}

// ACCEPTABLE: Pass by value when ownership transfer needed
std::shared_ptr<item_data> get_item(t_itemid id) {
    return item_db.find(id);  // Refcount incremented on return
}

// AVOID: Creating unnecessary copies in loops
for (auto item : item_db) {  // BAD: Copies shared_ptr every iteration
    // ...
}

for (auto& item : item_db) {  // GOOD: Reference, no copy
    // ...
}
```

---

## Iterating Databases

### Basic Iteration Pattern

```cpp
// Iterate all entries
for (auto& pair : item_db) {
    t_itemid id = pair.first;
    std::shared_ptr<item_data> item = pair.second;

    // Process item
    ShowInfo("Item: %s (ID: %d)\n", item->name.c_str(), id);
}
```

### Real Examples from Codebase

**Example 1: Search by Name**
**Source:** `/home/user/rathena2/src/map/mob.cpp:295`

```cpp
uint16 mobdb_searchname_(const char* const str, bool full_cmp) {
    for (auto const& mobdb_pair : mob_db) {
        const uint16 mob_id = mobdb_pair.first;
        if (mobdb_searchname_sub(mob_id, str, full_cmp))
            return mob_id;
    }
    return 0;
}
```

**Example 2: Search by Aegis Name**
**Source:** `/home/user/rathena2/src/map/mob.cpp:308`

```cpp
std::shared_ptr<s_mob_db> mobdb_search_aegisname(const char* str) {
    for (auto& mobdb_pair : mob_db) {
        if (strcmpi(str, mobdb_pair.second->sprite.c_str()) == 0) {
            return mobdb_pair.second;
        }
    }
    return nullptr;
}
```

**Example 3: Post-Load Processing**
**Source:** `/home/user/rathena2/src/map/itemdb.cpp:1118`

```cpp
void ItemDatabase::loadingFinished() {
    for (auto& tmp_item : item_db) {
        std::shared_ptr<item_data> item = tmp_item.second;

        // Items that are consumed only after target confirmation
        if (item->type == IT_DELAYCONSUME) {
            item->type = IT_USABLE;
            item->flag.delay_consume |= DELAYCONSUME_TEMP;
        } else {
            item->flag.delay_consume &= ~DELAYCONSUME_TEMP;
        }

        // Validate weapon levels
        if (item->type == IT_WEAPON) {
            if (item->weapon_level == 0) {
                ShowWarning("Item %s is a weapon, but does not have a weapon level. Consider adding it. Defaulting to 1.\n",
                    item->name.c_str());
                item->weapon_level = 1;
            }
        }
    }
}
```

**Example 4: Building Search Array**
**Source:** `/home/user/rathena2/src/map/itemdb.cpp:2904`

```cpp
uint16 itemdb_searchname_array(std::map<t_itemid, std::shared_ptr<item_data>>& data,
                                uint16 size, const char* str) {
    for (const auto& item : item_db) {
        std::shared_ptr<item_data> id = item.second;

        if (id == nullptr)
            continue;

        if (stristr(id->name.c_str(), str) != nullptr ||
            stristr(id->ename.c_str(), str) != nullptr ||
            strcmpi(id->ename.c_str(), str) == 0) {
            data[id->nameid] = id;
        }
    }

    if (data.size() > size)
        util::map_resize(data, size);

    return static_cast<uint16>(data.size());
}
```

### Performance Considerations

**⚠️ WARNING: Avoid iteration in hot paths!**

```cpp
// BAD: Iterating in hot path (called every tick)
void monster_ai_tick(mob_data* md) {
    for (auto& mob : mob_db) {  // DON'T DO THIS
        // This iterates ENTIRE database every AI tick!
    }
}

// GOOD: Direct lookup
void monster_ai_tick(mob_data* md) {
    std::shared_ptr<s_mob_db> mob = mob_db.find(md->mob_id);
    // O(1) lookup
}
```

**When Iteration is Acceptable:**
- ✅ Initialization/loading phase
- ✅ Admin commands (@listmobs, @searchitem)
- ✅ Database reload operations
- ✅ One-time searches
- ✅ Debug/diagnostic tools

**When to Avoid Iteration:**
- ❌ Combat calculations
- ❌ Packet processing
- ❌ AI routines
- ❌ Any per-tick operations
- ❌ Player movement handling

### Iteration with Filtering

```cpp
// Count items by type
std::unordered_map<item_types, uint32> item_counts;

for (auto& pair : item_db) {
    std::shared_ptr<item_data> item = pair.second;
    item_counts[item->type]++;
}

ShowInfo("Usable items: %d\n", item_counts[IT_USABLE]);
ShowInfo("Equipment: %d\n", item_counts[IT_ARMOR] + item_counts[IT_WEAPON]);
```

### Using size() and empty()

```cpp
// Check if database is loaded
if (item_db.empty()) {
    ShowError("Item database is empty!\n");
    return false;
}

ShowStatus("Loaded %zu items\n", item_db.size());
```

---

## Reloading Databases

### Reload Commands

**Available @commands:**
- `@reloaditemdb` - Reload item database
- `@reloadmobdb` - Reload mob database
- `@reloadskilldb` - Reload skill database
- `@reloadquestdb` - Reload quest database
- (and many others...)

### Implementing Reload Commands

**Source:** `/home/user/rathena2/src/map/atcommand.cpp:4327`

```cpp
ACMD_FUNC(reloaditemdb) {
    nullpo_retr(-1, sd);

    itemdb_reload();
    clif_displaymessage(fd, msg_txt(sd, 97)); // Item database has been reloaded.

    return 0;
}

ACMD_FUNC(reloadmobdb) {
    nullpo_retr(-1, sd);

    mob_reload();
    pet_db.reload();
    hom_reload();
    clif_displaymessage(fd, msg_txt(sd, 98)); // Monster database has been reloaded.

    return 0;
}
```

### Implementing Reload Functions

**Pattern:**
```cpp
void itemdb_reload() {
    // 1. Clear and reload main database
    item_db.reload();

    // 2. Reload dependent databases
    itemdb_group.reload();
    itemdb_combo.reload();

    // 3. Update live data structures
    // Re-link existing items to new database entries
    // Update player inventories, ground items, etc.
}
```

**Example: Mob Reload**
**Source:** Inferred from `/home/user/rathena2/src/map/mob.cpp:7225`

```cpp
void mob_reload() {
    // Reload mob database
    mob_db.reload();

    // Fix live mob data - relink to new database entries
    for (auto& pair : mob_db) {
        std::shared_ptr<s_mob_db> mob = pair.second;

        // Update any cached or calculated values
        // Validate drop references still exist
        for (auto it = mob->dropitem.begin(); it != mob->dropitem.end(); ) {
            if (!item_db.exists((*it)->nameid)) {
                ShowWarning("Mob %d has invalid drop item %d, removing.\n",
                    mob->mob_id, (*it)->nameid);
                it = mob->dropitem.erase(it);
            } else {
                ++it;
            }
        }
    }

    // Update all spawned mobs
    // (iterate map objects and relink md->db pointers)
}
```

### reload() Method

**Inherited from YamlDatabase:**
**Source:** `/home/user/rathena2/src/common/database.cpp:86`

```cpp
bool YamlDatabase::reload() {
    this->clear();      // Clear existing data
    return this->load(); // Load from disk again
}
```

**The reload process:**
1. Calls `clear()` - removes all entries, clears cache
2. Calls `load()` - re-reads YAML files
3. Calls `loadingFinished()` - rebuilds cache, validates

### Handling Live Data During Reload

**⚠️ CRITICAL: Live references become invalid after reload!**

```cpp
// BEFORE RELOAD
std::shared_ptr<item_data> item = item_db.find(501);
ShowInfo("Item: %s\n", item->name.c_str());  // "Red Potion"

// RELOAD HAPPENS
item_db.reload();

// AFTER RELOAD
// 'item' shared_ptr still valid (reference counting)
// but points to OLD data that may be outdated
ShowInfo("Item: %s\n", item->name.c_str());  // Still "Red Potion", but OLD version

// MUST re-fetch for new data
item = item_db.find(501);
ShowInfo("Item: %s\n", item->name.c_str());  // New version with any changes
```

**Best Practice: Re-link after reload**

```cpp
void update_mob_after_reload(mob_data* md) {
    // Mob is spawned in world with old database reference

    // Re-link to new database entry
    md->db = mob_db.find(md->mob_id);

    if (md->db == nullptr) {
        ShowError("Mob %d no longer exists after reload!\n", md->mob_id);
        // Despawn mob or handle error
        unit_free(&md->bl);
        return;
    }

    // Update any cached values from database
    status_calc_mob(md, SCO_NONE);
}
```

---

## SQL Database Access

### SQL vs YAML Databases

| Feature | YAML Databases | SQL Databases |
|---------|---------------|---------------|
| **Purpose** | Static game configuration | Dynamic player/guild data |
| **Examples** | Items, Mobs, Skills | Characters, Inventory, Guilds |
| **Reload** | @commands (hot-reload) | Server restart or migration |
| **Storage** | Text files (YAML) | MySQL/MariaDB tables |
| **Query** | find(), exists() | Sql_Query(), prepared statements |

### Basic SQL Operations

#### Simple Query

**Source:** `/home/user/rathena2/src/char/int_mercenary.cpp:131`

```cpp
if (SQL_ERROR == Sql_Query(sql_handle,
    "SELECT `class`, `hp`, `sp`, `kill_counter`, `life_time` FROM `%s` WHERE `mer_id` = '%d' AND `char_id` = '%d'",
    schema_config.mercenary_db, merc_id, char_id)) {
    Sql_ShowDebug(sql_handle);
    return false;
}

// Fetch results
if (SQL_SUCCESS != Sql_NextRow(sql_handle)) {
    Sql_FreeResult(sql_handle);
    return false;
}

// Get column data
char* data;
Sql_GetData(sql_handle, 0, &data, nullptr); int32 mob_class = atoi(data);
Sql_GetData(sql_handle, 1, &data, nullptr); merc->hp = atoi(data);
Sql_GetData(sql_handle, 2, &data, nullptr); merc->sp = atoi(data);
Sql_GetData(sql_handle, 3, &data, nullptr); merc->kill_count = atoi(data);
Sql_GetData(sql_handle, 4, &data, nullptr); merc->life_time = (uint32)atol(data);

Sql_FreeResult(sql_handle);
```

### Prepared Statements (Recommended)

**Why Prepared Statements?**
- ✅ **SQL injection protection** - Parameters are properly escaped
- ✅ **Better performance** - Query is compiled once, executed many times
- ✅ **Type safety** - Explicit parameter binding
- ✅ **Cleaner code** - Separates query structure from data

#### Creating Prepared Statement

```cpp
SqlStmt stmt{ *sql_handle };  // Constructor takes Sql& reference

// Prepare query with ? placeholders
if (SQL_ERROR == stmt.Prepare(
    "INSERT INTO `%s` (`mer_id`, `skill`, `tick`) VALUES (%d, ?, ?)",
    schema_config.skillcooldown_mercenary_db, merc->mercenary_id)) {
    SqlStmt_ShowDebug(stmt);
    return false;
}
```

#### Binding Parameters

**Source:** `/home/user/rathena2/src/char/int_mercenary.cpp:112`

```cpp
for (uint16 i = 0; i < MAX_SKILLCOOLDOWN; ++i) {
    if (merc->scd[i].skill_id == 0)
        continue;
    if (merc->scd[i].tick == 0)
        continue;

    // Bind parameters by index
    if (SQL_ERROR == stmt.BindParam(0, SQLDT_UINT16, &merc->scd[i].skill_id, 0)
        || SQL_ERROR == stmt.BindParam(1, SQLDT_LONGLONG, &merc->scd[i].tick, 0)
        || SQL_ERROR == stmt.Execute()) {
        SqlStmt_ShowDebug(stmt);
        return false;
    }
}
```

**Parameter Types (SqlDataType):**
```cpp
SQLDT_CHAR      // char
SQLDT_SHORT     // short
SQLDT_INT       // int
SQLDT_LONGLONG  // long long (int64)
SQLDT_UCHAR     // unsigned char
SQLDT_USHORT    // unsigned short (uint16)
SQLDT_UINT      // unsigned int (uint32)
SQLDT_ULONGLONG // unsigned long long (uint64)
SQLDT_STRING    // char* (null-terminated string)
SQLDT_ENUM      // enum (stored as string)

// Used in code:
SQLDT_INT8      // = SQLDT_CHAR
SQLDT_INT16     // = SQLDT_SHORT
SQLDT_INT32     // = SQLDT_INT
SQLDT_UINT16    // = SQLDT_USHORT
SQLDT_UINT32    // = SQLDT_UINT
SQLDT_UINT64    // = SQLDT_ULONGLONG
```

#### Binding Result Columns

**Source:** `/home/user/rathena2/src/char/char.cpp:596`

```cpp
SqlStmt stmt{ *sql_handle };

if (SQL_ERROR == stmt.Prepare("SELECT `id`, `nameid`, `amount`, `equip`, `identify`, `refine`, `attribute`, `expire_time`, `bound`, `unique_id`, `enchantgrade` FROM `%s` WHERE `char_id` = ?", schema_config.inventory_db))
{
    SqlStmt_ShowDebug(stmt);
    return false;
}

// Bind result columns to variables
struct item_data item = {};
stmt.BindColumn(0, SQLDT_INT32, &item.id);
stmt.BindColumn(1, SQLDT_UINT32, &item.nameid);
stmt.BindColumn(2, SQLDT_INT16, &item.amount);
stmt.BindColumn(3, SQLDT_UINT32, &item.equip);
stmt.BindColumn(4, SQLDT_CHAR, &item.identify);
stmt.BindColumn(5, SQLDT_CHAR, &item.refine);
stmt.BindColumn(6, SQLDT_CHAR, &item.attribute);
stmt.BindColumn(7, SQLDT_UINT32, &item.expire_time);
stmt.BindColumn(8, SQLDT_UINT32, &item.bound);
stmt.BindColumn(9, SQLDT_UINT64, &item.unique_id);
stmt.BindColumn(10, SQLDT_INT8, &item.enchantgrade);

// Bind parameter and execute
if (SQL_ERROR == stmt.BindParam(0, SQLDT_INT32, &char_id, 0)
    || SQL_ERROR == stmt.Execute()) {
    SqlStmt_ShowDebug(stmt);
    return false;
}

// Fetch rows (columns auto-filled by BindColumn)
while (SQL_SUCCESS == stmt.NextRow()) {
    // item.nameid, item.amount, etc. are automatically populated
    inventory.push_back(item);
}

stmt.FreeResult();
```

### Complete SQL Example: Save and Load

```cpp
// SAVE: Insert/Update
bool save_player_data(uint32 char_id, const player_data& pd) {
    SqlStmt stmt{ *sql_handle };

    // Prepare INSERT/UPDATE statement
    if (SQL_ERROR == stmt.Prepare(
        "INSERT INTO `player_custom_data` (`char_id`, `custom_value`, `last_update`) "
        "VALUES (?, ?, NOW()) "
        "ON DUPLICATE KEY UPDATE `custom_value` = ?, `last_update` = NOW()")) {
        SqlStmt_ShowDebug(stmt);
        return false;
    }

    // Bind parameters
    if (SQL_ERROR == stmt.BindParam(0, SQLDT_UINT32, &char_id, 0)
        || SQL_ERROR == stmt.BindParam(1, SQLDT_INT32, &pd.custom_value, 0)
        || SQL_ERROR == stmt.BindParam(2, SQLDT_INT32, &pd.custom_value, 0)
        || SQL_ERROR == stmt.Execute()) {
        SqlStmt_ShowDebug(stmt);
        return false;
    }

    return true;
}

// LOAD: Select
bool load_player_data(uint32 char_id, player_data& pd) {
    SqlStmt stmt{ *sql_handle };

    if (SQL_ERROR == stmt.Prepare(
        "SELECT `custom_value` FROM `player_custom_data` WHERE `char_id` = ?")) {
        SqlStmt_ShowDebug(stmt);
        return false;
    }

    // Bind result column
    stmt.BindColumn(0, SQLDT_INT32, &pd.custom_value);

    // Bind parameter and execute
    if (SQL_ERROR == stmt.BindParam(0, SQLDT_UINT32, &char_id, 0)
        || SQL_ERROR == stmt.Execute()) {
        SqlStmt_ShowDebug(stmt);
        return false;
    }

    // Fetch result
    if (SQL_SUCCESS != stmt.NextRow()) {
        stmt.FreeResult();
        return false;  // No data found
    }

    stmt.FreeResult();
    return true;
}
```

### SQL Best Practices

```cpp
// ✅ GOOD: Use prepared statements
SqlStmt stmt{ *sql_handle };
stmt.Prepare("SELECT * FROM table WHERE id = ?");
stmt.BindParam(0, SQLDT_INT32, &id, 0);
stmt.Execute();

// ❌ BAD: String concatenation (SQL injection risk!)
char query[256];
sprintf(query, "SELECT * FROM table WHERE name = '%s'", user_input);
Sql_QueryStr(sql_handle, query);  // VULNERABLE!

// ✅ GOOD: Always check return values
if (SQL_ERROR == stmt.Execute()) {
    SqlStmt_ShowDebug(stmt);
    return false;
}

// ❌ BAD: Ignoring errors
stmt.Execute();  // What if it fails?

// ✅ GOOD: Always free results
stmt.FreeResult();
Sql_FreeResult(sql_handle);

// ❌ BAD: Memory leak if not freed

// ✅ GOOD: Use transactions for multiple writes
Sql_QueryStr(sql_handle, "START TRANSACTION");
// ... multiple INSERT/UPDATE ...
Sql_QueryStr(sql_handle, "COMMIT");

// ✅ GOOD: Rollback on error
if (error) {
    Sql_QueryStr(sql_handle, "ROLLBACK");
}
```

---

## Real-World Examples

### Example 1: Complete Item Database Implementation

**Struct Definition:** `/home/user/rathena2/src/map/itemdb.hpp`

```cpp
struct item_data {
    t_itemid nameid;
    std::string name;         // AegisName
    std::string ename;        // Display Name
    item_types type;
    uint8 subtype;
    uint32 value_buy;
    uint32 value_sell;
    uint32 weight;
    uint32 atk;
    uint32 matk;
    uint32 def;
    uint16 range;
    uint16 slots;
    uint64 class_base[3];
    e_sex sex;
    uint16 weapon_level;
    uint16 armor_level;
    uint16 equip_level_min;
    uint16 equip_level_max;

    // ... many more fields ...

    struct s_item_flag {
        bool available : 1;
        bool delay_consume : 3;
        bool buyingstore : 1;
        // ... more flags ...
    } flag;
};
```

**Database Class:** `/home/user/rathena2/src/map/itemdb.hpp:3424`

```cpp
class ItemDatabase : public TypesafeCachedYamlDatabase<t_itemid, item_data> {
private:
    std::unordered_map<std::string, std::shared_ptr<item_data>> nameToItemDataMap;
    std::unordered_map<std::string, std::shared_ptr<item_data>> aegisNameToItemDataMap;

public:
    ItemDatabase() : TypesafeCachedYamlDatabase("ITEM_DB", 3, 1) {}

    const std::string getDefaultLocation() override {
        return std::string(db_path) + "/item_db.yml";
    }

    uint64 parseBodyNode(const ryml::NodeRef& node) override;
    void loadingFinished() override;
    void clear() override {
        TypesafeCachedYamlDatabase::clear();
        this->nameToItemDataMap.clear();
        this->aegisNameToItemDataMap.clear();
    }

    // Additional lookup methods
    std::shared_ptr<item_data> searchname(const char* name);
    std::shared_ptr<item_data> search_aegisname(const char* name);
};

extern ItemDatabase item_db;
```

**Parsing Implementation:** `/home/user/rathena2/src/map/itemdb.cpp:49`

```cpp
uint64 ItemDatabase::parseBodyNode(const ryml::NodeRef& node) {
    t_itemid nameid;

    // Required: Item ID
    if (!this->asUInt32(node, "Id", nameid))
        return 0;

    // Find existing or create new
    std::shared_ptr<item_data> item = this->find(nameid);
    bool exists = item != nullptr;

    if (!exists) {
        // New items must have AegisName and Name
        if (!this->nodesExist(node, { "AegisName", "Name" }))
            return 0;

        item = std::make_shared<item_data>();
        item->nameid = nameid;
        item->flag.available = true;
    }

    // Parse AegisName (script name)
    if (this->nodeExists(node, "AegisName")) {
        std::string name;
        if (!this->asString(node, "AegisName", name))
            return 0;

        // Validate length
        if (name.length() > ITEM_NAME_LENGTH) {
            this->invalidWarning(node["AegisName"],
                "AegisName \"%s\" exceeds maximum of %d characters, capping...\n",
                name.c_str(), ITEM_NAME_LENGTH - 1);
        }

        // Check for duplicates
        std::shared_ptr<item_data> id = item_db.search_aegisname(name.c_str());
        if (id != nullptr && id->nameid != nameid) {
            this->invalidWarning(node["AegisName"],
                "Found duplicate item Aegis name for %s, skipping.\n", name.c_str());
            return 0;
        }

        // Update name maps
        if (exists) {
            std::string aegisname = item->name;
            util::tolower(aegisname);
            this->aegisNameToItemDataMap.erase(aegisname);
        }

        item->name = name;
        std::string aegisname_lower = name;
        util::tolower(aegisname_lower);
        this->aegisNameToItemDataMap[aegisname_lower] = item;
    }

    // Parse Type (enum)
    if (this->nodeExists(node, "Type")) {
        std::string type;
        if (!this->asString(node, "Type", type))
            return 0;

        std::string type_constant = "IT_" + type;
        int64 constant;

        if (!script_get_constant(type_constant.c_str(), &constant) ||
            constant < IT_HEALING || constant >= IT_MAX) {
            this->invalidWarning(node["Type"],
                "Invalid item type %s, defaulting to IT_ETC.\n", type.c_str());
            constant = IT_ETC;
        }

        item->type = static_cast<item_types>(constant);
    } else {
        if (!exists)
            item->type = IT_ETC;
    }

    // Parse numeric fields
    if (this->nodeExists(node, "Weight")) {
        uint32 weight;
        if (!this->asUInt32(node, "Weight", weight))
            return 0;
        item->weight = weight;
    } else {
        if (!exists)
            item->weight = 0;
    }

    // ... many more fields ...

    // Store in database
    if (!exists)
        this->put(nameid, item);

    return 1;
}
```

**Post-Load Processing:** `/home/user/rathena2/src/map/itemdb.cpp:1117`

```cpp
void ItemDatabase::loadingFinished() {
    // Called after all entries loaded

    for (auto& tmp_item : item_db) {
        std::shared_ptr<item_data> item = tmp_item.second;

        // Convert delayed consume flag
        if (item->type == IT_DELAYCONSUME) {
            item->type = IT_USABLE;
            item->flag.delay_consume |= DELAYCONSUME_TEMP;
        } else {
            item->flag.delay_consume &= ~DELAYCONSUME_TEMP;
        }

        // Validate weapon level
        if (item->type == IT_WEAPON) {
            if (item->weapon_level == 0) {
                ShowWarning("Item %s is a weapon, but does not have a weapon level. Defaulting to 1.\n",
                    item->name.c_str());
                item->weapon_level = 1;
            }
        }
    }

    // Call parent to build cache
    TypesafeCachedYamlDatabase::loadingFinished();
}
```

### Example 2: Mob Database with Complex Drops

**Struct Definition:** `/home/user/rathena2/src/map/mob.hpp`

```cpp
struct s_mob_drop {
    t_itemid nameid;
    uint16 rate;      // Drop rate (10000 = 100%)
    uint16 steal_protected;
    uint16 randomopt_group;
};

struct s_mob_db {
    uint32 mob_id;
    std::string sprite;
    std::string name;
    std::string jname;
    uint16 lv;

    struct status_data status;  // HP, stats, etc.

    // Drop tables
    std::vector<std::shared_ptr<s_mob_drop>> dropitem;  // Normal drops
    std::vector<std::shared_ptr<s_mob_drop>> mvpitem;   // MVP drops

    uint32 exp, jexp;
    uint32 mexp, mexpper;

    // ... many more fields ...
};
```

**Parsing Drops:** `/home/user/rathena2/src/map/mob.cpp` (parseDropNode method)

```cpp
bool MobDatabase::parseDropNode(std::string nodeName, const ryml::NodeRef& node,
                                 uint8 max, std::vector<std::shared_ptr<s_mob_drop>>& drops) {
    if (!this->nodeExists(node, nodeName))
        return true;

    const auto& dropNode = node[nodeName];

    for (const auto& drop : dropNode) {
        t_itemid item_id;
        if (!this->asUInt32(drop, "Item", item_id))
            continue;

        // Validate item exists
        if (!item_db.exists(item_id)) {
            this->invalidWarning(drop["Item"],
                "Item %d does not exist in item database.\n", item_id);
            continue;
        }

        uint16 rate;
        if (!this->asUInt16Rate(drop, "Rate", rate))
            continue;

        // Create drop entry
        std::shared_ptr<s_mob_drop> drop_entry = std::make_shared<s_mob_drop>();
        drop_entry->nameid = item_id;
        drop_entry->rate = rate;

        // Optional: steal protection
        if (this->nodeExists(drop, "StealProtected")) {
            bool protected_drop;
            if (this->asBool(drop, "StealProtected", protected_drop))
                drop_entry->steal_protected = protected_drop ? 1 : 0;
        }

        drops.push_back(drop_entry);
    }

    return true;
}
```

### Example 3: Custom Database - Player Reputation System

**Complete Implementation Example:**

```cpp
// 1. Define data structure
struct s_reputation {
    int64 reputation_id;
    std::string name;
    std::string description;
    int32 min_value;
    int32 max_value;
    std::unordered_map<int32, std::string> rank_names;  // value -> rank name
};

// 2. Define database class
class ReputationDatabase : public TypesafeYamlDatabase<int64, s_reputation> {
public:
    ReputationDatabase() : TypesafeYamlDatabase("REPUTATION_DB", 1) {}

    const std::string getDefaultLocation() override {
        return std::string(db_path) + "/reputation_db.yml";
    }

    uint64 parseBodyNode(const ryml::NodeRef& node) override {
        int64 rep_id;

        if (!this->asInt64(node, "Id", rep_id))
            return 0;

        std::shared_ptr<s_reputation> rep = this->find(rep_id);
        bool exists = rep != nullptr;

        if (!exists) {
            if (!this->nodesExist(node, { "Name" }))
                return 0;

            rep = std::make_shared<s_reputation>();
            rep->reputation_id = rep_id;
        }

        // Parse name
        if (this->nodeExists(node, "Name")) {
            std::string name;
            if (!this->asString(node, "Name", name))
                return 0;
            rep->name = name;
        }

        // Parse description
        if (this->nodeExists(node, "Description")) {
            std::string desc;
            if (this->asString(node, "Description", desc))
                rep->description = desc;
        }

        // Parse min/max values
        if (this->nodeExists(node, "MinValue")) {
            int32 min_val;
            if (this->asInt32(node, "MinValue", min_val))
                rep->min_value = min_val;
        }

        if (this->nodeExists(node, "MaxValue")) {
            int32 max_val;
            if (this->asInt32(node, "MaxValue", max_val))
                rep->max_value = max_val;
        }

        // Parse ranks (sub-nodes)
        if (this->nodeExists(node, "Ranks")) {
            const auto& ranksNode = node["Ranks"];

            for (const auto& rankNode : ranksNode) {
                int32 value;
                std::string rank_name;

                if (!this->asInt32(rankNode, "Value", value))
                    continue;
                if (!this->asString(rankNode, "Name", rank_name))
                    continue;

                rep->rank_names[value] = rank_name;
            }
        }

        if (!exists)
            this->put(rep_id, rep);

        return 1;
    }
};

// 3. Declare global instance
extern ReputationDatabase reputation_db;

// 4. Define in .cpp file
ReputationDatabase reputation_db;

// 5. Load in initialization
void do_init_reputation() {
    reputation_db.load();
}

// 6. Use in game code
std::shared_ptr<s_reputation> rep = reputation_db.find(REP_CITY_PRONTERA);
if (rep != nullptr) {
    int32 player_rep_value = pc_get_reputation(sd, REP_CITY_PRONTERA);

    // Find rank name
    std::string rank = "Unknown";
    for (auto& pair : rep->rank_names) {
        if (player_rep_value >= pair.first) {
            rank = pair.second;
        }
    }

    clif_displaymessage(sd->fd,
        StringBuf_Printf("Your %s reputation: %d (%s)",
            rep->name.c_str(), player_rep_value, rank.c_str()));
}
```

---

## Common Patterns and Best Practices

### Pattern 1: Null Check Everything

```cpp
// ALWAYS check nullptr before using database entries
std::shared_ptr<item_data> item = item_db.find(item_id);
if (item == nullptr) {
    ShowError("Item %d not found!\n", item_id);
    return false;
}

// Now safe to use item->
```

### Pattern 2: Early Return on Error

```cpp
uint64 MyDatabase::parseBodyNode(const ryml::NodeRef& node) {
    uint32 id;
    if (!this->asUInt32(node, "Id", id))
        return 0;  // Early return

    std::string name;
    if (!this->asString(node, "Name", name))
        return 0;  // Early return

    // Continue parsing...
    return 1;
}
```

### Pattern 3: Default Values for Optional Fields

```cpp
if (this->nodeExists(node, "OptionalField")) {
    uint32 value;
    if (this->asUInt32(node, "OptionalField", value))
        item->optional_field = value;
} else {
    if (!exists)
        item->optional_field = 0;  // Default value for new items
    // For existing items, leave unchanged
}
```

### Pattern 4: Validation with Capping

```cpp
if (this->nodeExists(node, "Attack")) {
    uint32 atk;
    if (!this->asUInt32(node, "Attack", atk))
        return 0;

    if (atk > MAX_ATTACK) {
        this->invalidWarning(node["Attack"],
            "Attack %d exceeds maximum (%d), capping.\n", atk, MAX_ATTACK);
        atk = MAX_ATTACK;
    }

    item->atk = atk;
}
```

### Pattern 5: Cross-Reference Validation

```cpp
// Validate referenced entry exists in another database
if (this->nodeExists(node, "RequiredItem")) {
    t_itemid required_id;
    if (!this->asUInt32(node, "RequiredItem", required_id))
        return 0;

    if (!item_db.exists(required_id)) {
        this->invalidWarning(node["RequiredItem"],
            "Required item %d does not exist, skipping.\n", required_id);
        return 0;
    }

    entry->required_item = required_id;
}
```

### Pattern 6: Enum from String Constant

```cpp
// Convert YAML string to script constant
if (this->nodeExists(node, "Type")) {
    std::string type_str;
    if (!this->asString(node, "Type", type_str))
        return 0;

    std::string constant_name = "PREFIX_" + type_str;
    int64 constant;

    if (!script_get_constant(constant_name.c_str(), &constant)) {
        this->invalidWarning(node["Type"],
            "Unknown type %s, defaulting to DEFAULT.\n", type_str.c_str());
        constant = TYPE_DEFAULT;
    }

    entry->type = static_cast<my_enum_type>(constant);
}
```

### Pattern 7: Building Lookup Maps

```cpp
class MyDatabase : public TypesafeCachedYamlDatabase<uint32, my_data> {
private:
    std::unordered_map<std::string, std::shared_ptr<my_data>> nameToDataMap;

public:
    void clear() override {
        TypesafeCachedYamlDatabase::clear();
        this->nameToDataMap.clear();
    }

    uint64 parseBodyNode(const ryml::NodeRef& node) override {
        // ... parse entry ...

        // Build name lookup map
        std::string name_lower = entry->name;
        util::tolower(name_lower);
        this->nameToDataMap[name_lower] = entry;

        return 1;
    }

    // Additional lookup method
    std::shared_ptr<my_data> searchname(const char* name) {
        std::string name_lower = name;
        util::tolower(name_lower);

        auto it = this->nameToDataMap.find(name_lower);
        if (it != this->nameToDataMap.end())
            return it->second;

        return nullptr;
    }
};
```

### Pattern 8: Post-Load Validation

```cpp
void MyDatabase::loadingFinished() {
    // Validate cross-references after all databases loaded
    for (auto& pair : *this) {
        std::shared_ptr<my_data> entry = pair.second;

        // Check if referenced items exist
        for (auto& required_id : entry->requirements) {
            if (!item_db.exists(required_id)) {
                ShowWarning("Entry %d references non-existent item %d\n",
                    entry->id, required_id);
            }
        }
    }

    // Call parent to build cache
    TypesafeCachedYamlDatabase::loadingFinished();
}
```

### Common Mistakes to Avoid

```cpp
// ❌ DON'T: Use without nullptr check
auto item = item_db.find(item_id);
ShowInfo("%s\n", item->name.c_str());  // CRASH if nullptr!

// ✅ DO: Always check nullptr
auto item = item_db.find(item_id);
if (item != nullptr) {
    ShowInfo("%s\n", item->name.c_str());
}

// ❌ DON'T: Double lookup
if (item_db.exists(item_id)) {
    auto item = item_db.find(item_id);  // Second lookup!
}

// ✅ DO: Single lookup
auto item = item_db.find(item_id);
if (item != nullptr) {
    // use item
}

// ❌ DON'T: Iterate in hot paths
void on_every_attack() {
    for (auto& item : item_db) {  // Called hundreds of times per second!
        // ...
    }
}

// ✅ DO: Direct lookup
void on_every_attack() {
    auto item = item_db.find(item_id);  // O(1) lookup
}

// ❌ DON'T: Forget to free SQL results
Sql_Query(sql_handle, "SELECT ...");
while (Sql_NextRow(sql_handle) == SQL_SUCCESS) {
    // process
}
// Missing Sql_FreeResult()!  Memory leak!

// ✅ DO: Always free
Sql_Query(sql_handle, "SELECT ...");
while (Sql_NextRow(sql_handle) == SQL_SUCCESS) {
    // process
}
Sql_FreeResult(sql_handle);

// ❌ DON'T: Concatenate user input into SQL
char query[256];
sprintf(query, "SELECT * FROM users WHERE name='%s'", player_name);  // SQL INJECTION!
Sql_QueryStr(sql_handle, query);

// ✅ DO: Use prepared statements
SqlStmt stmt{ *sql_handle };
stmt.Prepare("SELECT * FROM users WHERE name = ?");
stmt.BindParam(0, SQLDT_STRING, player_name, strlen(player_name));
stmt.Execute();
```

---

## Quick Reference Cheat Sheet

### YAML Database Operations

```cpp
// Access
auto entry = db.find(id);           // Returns shared_ptr or nullptr
bool exists = db.exists(id);        // Check existence

// Iteration
for (auto& pair : db) {
    KeyType id = pair.first;
    std::shared_ptr<DataType> entry = pair.second;
}

// Size
size_t count = db.size();
bool empty = db.empty();

// Reload
db.reload();
```

### Parsing Functions

```cpp
// Node checks
bool nodeExists(node, "FieldName");
bool nodesExist(node, { "Field1", "Field2" });

// Type conversions
asInt16(node, "Field", out);
asUInt16(node, "Field", out);
asInt32(node, "Field", out);
asUInt32(node, "Field", out);
asInt64(node, "Field", out);
asUInt64(node, "Field", out);
asFloat(node, "Field", out);
asDouble(node, "Field", out);
asString(node, "Field", out);
asBool(node, "Field", out);
asUInt16Rate(node, "Field", out);  // Percentage

// Error reporting
invalidWarning(node["Field"], "Message %d\n", value);
```

### SQL Operations

```cpp
// Simple query
Sql_Query(sql_handle, "SELECT ...");
while (Sql_NextRow(sql_handle) == SQL_SUCCESS) {
    char* data;
    Sql_GetData(sql_handle, 0, &data, nullptr);
}
Sql_FreeResult(sql_handle);

// Prepared statement
SqlStmt stmt{ *sql_handle };
stmt.Prepare("SELECT ... WHERE id = ?");
stmt.BindParam(0, SQLDT_INT32, &id, 0);
stmt.Execute();
while (stmt.NextRow() == SQL_SUCCESS) {
    // ...
}
stmt.FreeResult();
```

---

## Summary

This document covers:
- ✅ Database class hierarchy (YamlDatabase → TypesafeYamlDatabase → TypesafeCachedYamlDatabase)
- ✅ Accessing databases with find() and null checks
- ✅ YAML parsing with parseBodyNode() and helper functions
- ✅ Adding custom fields to structs (struct → parsing → usage)
- ✅ Validation patterns (range, cross-reference, duplicates)
- ✅ Caching architecture and performance
- ✅ Iterating databases (when appropriate)
- ✅ Reloading databases (@commands)
- ✅ SQL database access (queries and prepared statements)
- ✅ Real-world examples from itemdb, mobdb, skilldb

**Next Steps:**
- For script integration: See `KB_REF_ScriptCommands.md`
- For combat system: See `KB_COMBAT_SYSTEM.md`
- For packet handling: See `KB_PACKETS.md`

---

**Document End**
