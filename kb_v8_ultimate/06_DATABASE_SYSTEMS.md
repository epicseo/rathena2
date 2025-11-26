# rAthena Database Systems Complete Reference v8.0 Ultimate

**Version:** 8.0 Ultimate
**Coverage:** Database C++, Packets, Compilation/Debugging
**Last Updated:** 2025-11-26

---

# ═══════════════════════════════════════════════════════════════
# PART 1: DATABASE C++ IMPLEMENTATION
# ═══════════════════════════════════════════════════════════════

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

# ═══════════════════════════════════════════════════════════════
# PART 2: PACKET STRUCTURE
# ═══════════════════════════════════════════════════════════════
# rAthena Packet Structure Reference

**Version:** 2.0
**Last Updated:** 2025
**Scope:** Client-Server Communication in rAthena

---

## Table of Contents

1. [Introduction to Packet System](#1-introduction-to-packet-system)
2. [Packet Naming Conventions](#2-packet-naming-conventions)
3. [CLIF Structure and Functions](#3-clif-structure-and-functions)
4. [Packet Structure Definition](#4-packet-structure-definition)
5. [PACKETVER System](#5-packetver-system)
6. [Packet Registration System](#6-packet-registration-system)
7. [WFIFO/RFIF Macros](#7-wfiforfif-macros)
8. [Creating Custom Packets](#8-creating-custom-packets)
9. [Common Packet Patterns](#9-common-packet-patterns)
10. [Security and Validation](#10-security-and-validation)
11. [Debugging Packets](#11-debugging-packets)
12. [Real-World Examples](#12-real-world-examples)

---

## 1. Introduction to Packet System

The packet system in rAthena handles all client-server communication. Every action in the game—from player movement to chatting, trading, and combat—is transmitted via packets.

### Core Concepts

- **Packets** are binary data structures sent between client and server
- **Packet IDs** (headers) identify the type of packet (e.g., `0x8e` for chat messages)
- **clif.cpp/hpp** contains the main packet handling code for the map server
- **Packet direction** is encoded in the packet name prefix (CZ, ZC, HC, CH)

### File Locations

```
src/map/clif.cpp              # Main packet implementation
src/map/clif.hpp              # Function declarations
src/map/packets.hpp           # Packet structure definitions
src/map/clif_packetdb.hpp     # Packet registration database
src/config/packets.hpp        # PACKETVER configuration
src/common/socket.hpp         # Socket and FIFO macros
```

---

## 2. Packet Naming Conventions

rAthena uses a standardized naming convention for packets based on their direction and purpose.

### Packet Direction Prefixes

| Prefix | Direction | Description |
|--------|-----------|-------------|
| **CZ_** | Client → Zone (Map) Server | Client requests/sends data to map server |
| **ZC_** | Zone (Map) Server → Client | Map server sends data to client |
| **CH_** | Client → Character Server | Client interacts with char server |
| **HC_** | Character Server → Client | Char server responds to client |
| **CA_** | Client → Account (Login) Server | Client authentication |
| **AC_** | Account (Login) Server → Client | Login server responses |
| **SC_** | Server → Client | Generic server-to-client packets |

### Naming Examples

```cpp
// Client sends message to server
struct PACKET_CZ_REQMAKINGITEM { ... };          // Client requests to craft item

// Server sends data to client
struct PACKET_ZC_ITEM_PICKUP_ACK { ... };        // Server confirms item pickup
struct PACKET_ZC_BROADCAST { ... };              // Server sends broadcast message

// Character server packets
struct PACKET_CH_ENTER { ... };                  // Client enters char server
struct PACKET_HC_ACCEPT_ENTER { ... };           // Char server accepts connection
```

### Common Packet Name Patterns

| Pattern | Meaning | Example |
|---------|---------|---------|
| **REQ_** | Request | `PACKET_CZ_REQ_MAKINGARROW` - Request to make arrows |
| **ACK_** | Acknowledgment | `PACKET_ZC_ACK_CASH_BARGAIN_SALE_ITEM_INFO` |
| **NOTIFY_** | Notification | `PACKET_ZC_NOTIFY_PLAYERMOVE` - Notify player movement |
| **ACCEPT_** | Accept/Confirm | `PACKET_ZC_ACCEPT_ENTER` - Accept map entry |
| **REFUSE_** | Refuse/Reject | `PACKET_ZC_REFUSE_ENTER` - Refuse map entry |

---

## 3. CLIF Structure and Functions

The `clif` (Client Interface) module handles all packet transmission and reception for the map server.

### Function Naming Convention

```cpp
// SEND functions (server → client)
void clif_*               // Functions that SEND packets to client
void clif_displaymessage  // Send message to client
void clif_additem         // Send item add notification
void clif_skillinfo       // Send skill information

// PARSE functions (client → server)
void clif_parse_*         // Functions that PARSE packets from client
void clif_parse_WalkToXY      // Parse walk request
void clif_parse_GlobalMessage // Parse chat message
void clif_parse_DropItem      // Parse drop item request
```

### CLIF Send Functions

**Purpose:** Send packets FROM server TO client

**Pattern:**
```cpp
void clif_<action>(map_session_data *sd, <parameters>)
{
    int32 fd = sd->fd;  // Get file descriptor

    // Allocate buffer space
    WFIFOHEAD(fd, <packet_size>);

    // Write packet data
    WFIFOW(fd, 0) = <packet_id>;
    WFIFOW(fd, 2) = <packet_length>;
    // ... write more fields

    // Send packet
    WFIFOSET(fd, <packet_size>);
}
```

**Example:**
```cpp
// From src/map/clif.cpp
void clif_displaymessage(const int32 fd, const char* mes)
{
    nullpo_retv(mes);

    if (session_isActive(fd)) {
        int16 len = strnlen(mes, CHAT_SIZE_MAX);

        if (len > 0) {
            WFIFOHEAD(fd, 5 + len);
            WFIFOW(fd, 0) = 0x8e;           // Packet ID
            WFIFOW(fd, 2) = 5 + len;        // Packet length
            safestrncpy(WFIFOCP(fd, 4), mes, len + 1);
            WFIFOSET(fd, 5 + len);
        }
    }
}
```

### CLIF Parse Functions

**Purpose:** Parse packets FROM client, process request

**Pattern:**
```cpp
void clif_parse_<Action>(int32 fd, map_session_data *sd)
{
    // Validate player state
    if (pc_isdead(sd)) return;
    if (pc_cant_act(sd)) return;

    // Read packet data
    uint16 field1 = RFIFOW(fd, <offset>);
    uint32 field2 = RFIFOL(fd, <offset>);

    // Process request
    // Call game logic functions

    // Send response (if needed)
    clif_<response>(sd, ...);
}
```

**Example:**
```cpp
// From src/map/clif.cpp
void clif_parse_WalkToXY(int32 fd, map_session_data *sd)
{
    int16 x, y;

    // Validate state
    if (pc_isdead(sd)) {
        clif_clearunit_area(*sd, CLR_DEAD);
        return;
    }

    if (pc_cant_act(sd))
        return;

    // Parse position from packet
    RFIFOPOS(fd, packet_db[RFIFOW(fd, 0)].pos[0], &x, &y, nullptr);

    // Process movement
    unit_walktoxy(&sd->bl, x, y, 4);
}
```

---

## 4. Packet Structure Definition

Packet structures in rAthena are defined using C structs with specific attributes to ensure proper memory layout.

### Basic Packet Structure

```cpp
struct PACKET_<NAME> {
    int16 packetType;      // Packet ID (always first field)
    // ... other fields
} __attribute__((packed));
DEFINE_PACKET_HEADER(<NAME>, <packet_id>)
```

### The `__attribute__((packed))` Attribute

**Critical:** This attribute prevents compiler padding, ensuring the struct matches the exact binary layout expected by the client.

```cpp
// WITHOUT __attribute__((packed)) - WRONG!
struct BAD_PACKET {
    int16 packetType;  // offset 0-1
    // PADDING bytes 2-3 (compiler adds this)
    int32 value;       // offset 4-7
};  // Total: 8 bytes

// WITH __attribute__((packed)) - CORRECT!
struct GOOD_PACKET {
    int16 packetType;  // offset 0-1
    int32 value;       // offset 2-5
} __attribute__((packed));  // Total: 6 bytes
```

### Fixed-Length Packets

```cpp
// Fixed-length packet example
struct PACKET_ZC_RESTART_ACK {
    int16 packetType;   // 2 bytes - packet ID
    uint8 type;         // 1 byte  - restart type
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_RESTART_ACK, 0xb3)
// Total size: 3 bytes
```

### Variable-Length Packets

```cpp
// Variable-length packet with dynamic data
struct PACKET_ZC_BROADCAST {
    int16 packetType;   // 2 bytes - packet ID
    int16 packetLength; // 2 bytes - total packet length
    char message[];     // Variable length message
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_BROADCAST, 0x9a)

// Usage:
// Total size = 4 + strlen(message) + 1
```

### Nested Structures (Sub-packets)

```cpp
// Sub-structure for repeated data
struct PACKET_ZC_FRIENDS_LIST_sub {
    uint32 AID;        // Account ID
    uint32 CID;        // Character ID
    char name[NAME_LENGTH];
} __attribute__((packed));

// Main packet using sub-structure
struct PACKET_ZC_FRIENDS_LIST {
    int16 packetType;
    int16 packetLength;
    struct PACKET_ZC_FRIENDS_LIST_sub friends[];  // Array of friends
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_FRIENDS_LIST, 0x201)
```

### PACKETVER-Conditional Fields

```cpp
// Different structure based on client version
struct PACKET_CZ_REQ_MAKINGARROW {
    int16 packetType;
#if PACKETVER_MAIN_NUM >= 20181121 || PACKETVER_RE_NUM >= 20180704 || PACKETVER_ZERO_NUM >= 20181114
    uint32 itemId;      // Newer clients: 4-byte item ID
#else
    uint16 itemId;      // Older clients: 2-byte item ID
#endif
} __attribute__((packed));
DEFINE_PACKET_HEADER(CZ_REQ_MAKINGARROW, 0x1ae)
```

### Complete Example: Banking Packet

```cpp
// Client requests bank deposit
struct PACKET_CZ_REQ_BANKING_DEPOSIT {
    int16 packetType;   // Offset 0-1: Packet ID
    uint32 AID;         // Offset 2-5: Account ID
    int32 zeny;         // Offset 6-9: Amount to deposit
} __attribute__((packed));
// Total size: 10 bytes
```

---

## 5. PACKETVER System

The PACKETVER system allows rAthena to support multiple client versions with different packet structures.

### PACKETVER Configuration

**File:** `src/config/packets.hpp`

```cpp
#ifndef PACKETVER
    // Default client version: 2021-11-03
    #define PACKETVER 20211103
#endif

// Automatic Renewal detection
#ifndef PACKETVER_RE
    #if (PACKETVER > 20151104 && PACKETVER < 20180704) ||
        (PACKETVER >= 20200902 && PACKETVER <= 20211118)
        #define PACKETVER_RE
    #endif
#endif
```

### Setting PACKETVER

**Windows:**
```cpp
// In src/custom/defines_pre.hpp
#define PACKETVER 20211103
```

**Linux:**
```bash
./configure --enable-packetver=20211103
make clean
make server
```

### PACKETVER Variants

```cpp
PACKETVER               // Base packet version (YYYYMMDD format)
PACKETVER_MAIN_NUM      // Main server packet version
PACKETVER_RE_NUM        // Renewal server packet version
PACKETVER_ZERO_NUM      // Zero server packet version
```

### Version-Specific Code

```cpp
// Different packet structures for different versions
#if PACKETVER < 20080102
struct PACKET_ZC_ACCEPT_ENTER {
    int16 packetType;
    uint32 startTime;
    uint8 posDir[3];
    uint8 xSize;
    uint8 ySize;
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_ACCEPT_ENTER, 0x73)

#elif PACKETVER < 20141022 || PACKETVER >= 20160330
struct PACKET_ZC_ACCEPT_ENTER {
    int16 packetType;
    uint32 startTime;
    uint8 posDir[3];
    uint8 xSize;
    uint8 ySize;
    uint16 font;        // Font field added
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_ACCEPT_ENTER, 0x2eb)

#else
struct PACKET_ZC_ACCEPT_ENTER {
    int16 packetType;
    uint32 startTime;
    uint8 posDir[3];
    uint8 xSize;
    uint8 ySize;
    uint16 font;
    uint8 sex;          // Sex field added
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_ACCEPT_ENTER, 0xa18)
#endif
```

### PACKETVER Feature Flags

```cpp
// Feature availability checks
#define PACKETVER_SUPPORTS_PINCODE (PACKETVER >= 20110309)
#define PACKETVER_SUPPORTS_SALES (PACKETVER >= 20131223)
#define WEB_SERVER_ENABLE (PACKETVER > 20200300)

// Usage:
#if PACKETVER_SUPPORTS_PINCODE
    // Pincode system code
#endif
```

### Common PACKETVER Checks

```cpp
// Item ID size changed
#if PACKETVER_MAIN_NUM >= 20181121 || PACKETVER_RE_NUM >= 20180704 || PACKETVER_ZERO_NUM >= 20181114
    uint32 itemId;  // 4 bytes
#else
    uint32 itemId;  // 2 bytes
#endif

// String termination changed
#if PACKETVER < 20151001
    // Message must be null-terminated
#else
    // No null termination
#endif
```

---

## 6. Packet Registration System

Packets are registered in `clif_packetdb.hpp` to link packet IDs to their handler functions.

### Packet Database Structure

**File:** `src/map/clif.hpp`

```cpp
struct s_packet_db {
    int16 len;                              // Packet length (-1 = variable)
    void (*func)(int32, map_session_data *); // Handler function
    int16 pos[MAX_PACKET_POS];              // Field positions for parsing
};

extern struct s_packet_db packet_db[MAX_PACKET_DB + 1];
```

### Registration Macros

**File:** `src/map/clif_packetdb.hpp`

```cpp
// Simple packet registration (no handler)
#define packet(cmd, length) \
    packetdb_addpacket(cmd, length, nullptr, 0)

// Parseable packet registration (with handler)
#define parseable_packet(cmd, length, func, ...) \
    packetdb_addpacket(cmd, length, func, __VA_ARGS__, 0)
```

### Registration Examples

```cpp
// Fixed-length packet without handler
packet(0x0064, 55);           // Length: 55 bytes, no handler

// Variable-length packet without handler
packet(0x0069, -1);           // Length: variable (-1)

// Fixed-length packet WITH handler and field positions
parseable_packet(0x0072, 19, clif_parse_WantToConnection, 2, 6, 10, 14, 18);
//                ^      ^   ^                              ^  ^  ^   ^   ^
//              ID     Len  Handler function              Field positions
```

### Field Position System

The position array tells the parser where to find specific fields in the packet:

```cpp
// Example: Walk packet
parseable_packet(0x0085, 5, clif_parse_WalkToXY, 2);
//                                                 ^
//                                                 Position data starts at byte 2

// In the handler:
void clif_parse_WalkToXY(int32 fd, map_session_data *sd) {
    int16 x, y;
    // Use position from packet_db
    RFIFOPOS(fd, packet_db[RFIFOW(fd, 0)].pos[0], &x, &y, nullptr);
    //                                      ^^^^
    //                                      pos[0] = 2
}
```

### Common Registration Patterns

```cpp
// Chat message: variable length, handler with positions
parseable_packet(0x008c, -1, clif_parse_GlobalMessage, 2, 4);
//                       ^^                             ^  ^
//                    Variable                    pos[0] pos[1]

// Item use: fixed length with positions
parseable_packet(0x00a7, 8, clif_parse_UseItem, 2, 4);
//                       ^                       ^  ^
//                    8 bytes              index  amount

// Skill use: positions for skill ID, target, level
parseable_packet(0x0113, 10, clif_parse_UseSkillToId, 2, 4, 6);
//                           ^                         ^  ^  ^
//                         Handler                  skill target level

// NPC click: using HEADER constant and sizeof
parseable_packet(HEADER_CZ_CONTACTNPC, sizeof(PACKET_CZ_CONTACTNPC),
                 clif_parse_NpcClicked, 0);
```

### Adding Packets to Database

**Function:** `packetdb_addpacket`

```cpp
void packetdb_addpacket(uint16 cmd, uint16 length,
                        void (*func)(int32, map_session_data *), ...)
{
    va_list argp;
    int32 i;

    if (cmd <= 0 || cmd > MAX_PACKET_DB)
        return;

    packet_db[cmd].len = length;
    packet_db[cmd].func = func;

    // Read field positions from variable arguments
    va_start(argp, func);
    for (i = 0; i < MAX_PACKET_POS; i++) {
        int32 offset = va_arg(argp, int32);
        if (offset == 0)
            break;
        packet_db[cmd].pos[i] = offset;
    }
    va_end(argp);
}
```

### Complete Registration Example

```cpp
// In clif_packetdb.hpp

// 1. Trade request packet
parseable_packet(0x00e4, 6, clif_parse_TradeRequest, 2);

// 2. Trade item addition
parseable_packet(HEADER_CZ_ADD_EXCHANGE_ITEM,
                 sizeof(PACKET_CZ_ADD_EXCHANGE_ITEM),
                 clif_parse_TradeAddItem, 0);

// 3. Party message (variable length)
parseable_packet(0x0108, -1, clif_parse_PartyMessage, 2, 4);
```

---

## 7. WFIFO/RFIF Macros

Socket I/O macros for reading from and writing to network buffers.

### Core FIFO Macros

**File:** `src/common/socket.hpp`

```cpp
// Write FIFO (Server → Client)
WFIFOHEAD(fd, size)      // Allocate buffer space
WFIFOP(fd, pos)          // Get pointer at position
WFIFOB(fd, pos)          // Read/Write uint8 (1 byte)
WFIFOW(fd, pos)          // Read/Write uint16 (2 bytes)
WFIFOL(fd, pos)          // Read/Write uint32 (4 bytes)
WFIFOQ(fd, pos)          // Read/Write uint64 (8 bytes)
WFIFOCP(fd, pos)         // Get char pointer at position
WFIFOSET(fd, len)        // Finalize and send packet

// Read FIFO (Client → Server)
RFIFOP(fd, pos)          // Get pointer at position
RFIFOB(fd, pos)          // Read uint8
RFIFOW(fd, pos)          // Read uint16
RFIFOL(fd, pos)          // Read uint32
RFIFOQ(fd, pos)          // Read uint64
RFIFOCP(fd, pos)         // Get char pointer
RFIFOREST(fd)            // Remaining bytes in buffer
RFIFOSKIP(fd, len)       // Skip bytes in buffer
```

### WFIFO Usage (Sending Packets)

```cpp
void clif_example_send(map_session_data *sd, const char *message)
{
    int32 fd = sd->fd;
    uint16 msg_len = strlen(message) + 1;
    uint16 packet_len = 4 + msg_len;

    // Step 1: Allocate buffer space
    WFIFOHEAD(fd, packet_len);

    // Step 2: Write packet header
    WFIFOW(fd, 0) = 0x8e;          // Packet ID (2 bytes)
    WFIFOW(fd, 2) = packet_len;    // Packet length (2 bytes)

    // Step 3: Write message data
    safestrncpy(WFIFOCP(fd, 4), message, msg_len);

    // Step 4: Send packet
    WFIFOSET(fd, packet_len);
}
```

### RFIF Usage (Receiving Packets)

```cpp
void clif_parse_example(int32 fd, map_session_data *sd)
{
    // Read packet fields
    uint16 packet_id = RFIFOW(fd, 0);     // Byte 0-1: Packet ID
    uint16 item_index = RFIFOW(fd, 2);    // Byte 2-3: Item index
    uint32 amount = RFIFOL(fd, 4);        // Byte 4-7: Amount

    // Read string data
    char message[256];
    safestrncpy(message, RFIFOCP(fd, 8), sizeof(message));

    // Process data
    // ...
}
```

### Buffer Macros (WBUF/RBUF)

For working with pre-allocated buffers instead of session buffers:

```cpp
// Buffer macros (for packet_buffer or custom buffers)
WBUFP(p, pos)           // Get pointer in buffer
WBUFB(p, pos)           // Write uint8
WBUFW(p, pos)           // Write uint16
WBUFL(p, pos)           // Write uint32
WBUFQ(p, pos)           // Write uint64

RBUFP(p, pos)           // Get pointer in buffer
RBUFB(p, pos)           // Read uint8
RBUFW(p, pos)           // Read uint16
RBUFL(p, pos)           // Read uint32
RBUFQ(p, pos)           // Read uint64
```

### Using Packet Buffer

```cpp
// Global packet buffer for reusable storage
extern int8 packet_buffer[UINT16_MAX];

void clif_example_with_buffer(map_session_data *sd)
{
    PACKET_ZC_BROADCAST *p = (PACKET_ZC_BROADCAST*)packet_buffer;

    // Build packet in buffer
    p->packetType = HEADER_ZC_BROADCAST;
    p->packetLength = sizeof(PACKET_ZC_BROADCAST) + 20;
    strcpy(p->message, "Hello World!");

    // Send from buffer
    clif_send(p, p->packetLength, &sd->bl, SELF);
}
```

### Position Encoding Macros

Special macros for encoding/decoding coordinate data:

```cpp
// Write position to buffer
WBUFPOS(p, pos, x, y, dir)      // Encode x, y, direction (3 bytes)
WBUFPOS2(p, pos, ...)           // Encode movement path (6 bytes)

// Write position to FIFO
WFIFOPOS(fd, pos, x, y, dir)

// Read position from buffer
RBUFPOS(p, pos, &x, &y, &dir)
RBUFPOS2(p, pos, ...)

// Read position from FIFO
RFIFOPOS(fd, pos, &x, &y, &dir)
```

### Position Encoding Example

```cpp
// From src/map/clif.cpp
static inline void WBUFPOS(uint8* p, uint16 pos, int16 x, int16 y, unsigned char dir)
{
    p += pos;
    p[0] = (uint8)(x >> 2);
    p[1] = (uint8)((x << 6) | ((y >> 4) & 0x3f));
    p[2] = (uint8)((y << 4) | (dir & 0xf));
}

// Usage in movement packet
void clif_send_move(map_session_data *sd, int16 x, int16 y, uint8 dir)
{
    int fd = sd->fd;
    WFIFOHEAD(fd, 10);
    WFIFOW(fd, 0) = 0x87;           // Movement packet
    WFIFOL(fd, 2) = gettick();      // Timestamp
    WFIFOPOS(fd, 6, x, y, dir);     // Encode position (3 bytes)
    WFIFOSET(fd, 10);
}
```

### Complete Send Example

```cpp
// Real example from clif_displaymessage
void clif_displaymessage(const int32 fd, const char* mes)
{
    int16 len = strnlen(mes, CHAT_SIZE_MAX);

    if (len > 0) {
        // 1. Allocate buffer
        WFIFOHEAD(fd, 5 + len);

        // 2. Write header
        WFIFOW(fd, 0) = 0x8e;        // Packet ID
        WFIFOW(fd, 2) = 5 + len;     // Total length

        // 3. Write string
        safestrncpy(WFIFOCP(fd, 4), mes, len + 1);

        // 4. Send
        WFIFOSET(fd, 5 + len);
    }
}
```

---

## 8. Creating Custom Packets

Step-by-step guide to creating new packets for custom features.

### Step 1: Choose Packet ID

**Rules:**
- Use packet IDs in the custom range: `0x0CFF` and above
- Check existing packets to avoid conflicts
- Document your packet ID choice

```cpp
// Good choices for custom packets:
0x0d00, 0x0d01, 0x0d02, ...
0x9000, 0x9001, 0x9002, ...
```

### Step 2: Define Packet Structure

**File:** `src/map/packets.hpp`

```cpp
// Example: Custom quest notification packet

// Client requests quest info
struct PACKET_CZ_CUSTOM_QUEST_INFO {
    int16 packetType;
    uint32 questId;
} __attribute__((packed));
DEFINE_PACKET_HEADER(CZ_CUSTOM_QUEST_INFO, 0x0d00)

// Server sends quest data
struct PACKET_ZC_CUSTOM_QUEST_DATA {
    int16 packetType;
    int16 packetLength;
    uint32 questId;
    uint32 mobId;
    uint16 killCount;
    uint16 killRequired;
    char questName[50];
    char description[200];
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_CUSTOM_QUEST_DATA, 0x0d01)
```

### Step 3: Register Packet

**File:** `src/map/clif_packetdb.hpp`

```cpp
// Add at the end of the file, before #endif

// Register client→server packet
parseable_packet(HEADER_CZ_CUSTOM_QUEST_INFO,
                 sizeof(PACKET_CZ_CUSTOM_QUEST_INFO),
                 clif_parse_custom_quest_info, 0);

// Server→client packets don't need registration (send only)
```

### Step 4: Implement Parser (Client → Server)

**File:** `src/map/clif.cpp`

```cpp
/// Request quest information
/// 0d00 <quest id>.L (CZ_CUSTOM_QUEST_INFO)
void clif_parse_custom_quest_info(int32 fd, map_session_data *sd)
{
    // Validate player state
    if (!sd || !sd->bl.prev)
        return;

    // Read packet data
    const PACKET_CZ_CUSTOM_QUEST_INFO *p =
        (PACKET_CZ_CUSTOM_QUEST_INFO*)RFIFOP(fd, 0);

    uint32 quest_id = p->questId;

    // Validate quest ID
    if (quest_id == 0 || quest_id > MAX_QUEST_DB) {
        ShowWarning("clif_parse_custom_quest_info: Invalid quest ID %u from player %s\n",
                    quest_id, sd->status.name);
        return;
    }

    // Process quest request
    // ... your logic here ...

    // Send response
    clif_custom_quest_data(sd, quest_id);
}
```

### Step 5: Implement Sender (Server → Client)

**File:** `src/map/clif.cpp`

```cpp
/// Send quest information to client
/// 0d01 <packet len>.W <quest id>.L <mob id>.L <kill count>.W <required>.W
///      <name>.50B <description>.200B (ZC_CUSTOM_QUEST_DATA)
void clif_custom_quest_data(map_session_data *sd, uint32 quest_id)
{
    nullpo_retv(sd);

    int32 fd = sd->fd;
    if (!session_isActive(fd))
        return;

    // Get quest data from database
    struct quest_db *quest = quest_search(quest_id);
    if (!quest)
        return;

    // Build packet
    PACKET_ZC_CUSTOM_QUEST_DATA p = {};

    p.packetType = HEADER_ZC_CUSTOM_QUEST_DATA;
    p.packetLength = sizeof(PACKET_ZC_CUSTOM_QUEST_DATA);
    p.questId = quest_id;
    p.mobId = quest->mob_id;
    p.killCount = quest->count;
    p.killRequired = quest->required;
    safestrncpy(p.questName, quest->name, sizeof(p.questName));
    safestrncpy(p.description, quest->desc, sizeof(p.description));

    // Send packet
    WFIFOHEAD(fd, p.packetLength);
    memcpy(WFIFOP(fd, 0), &p, p.packetLength);
    WFIFOSET(fd, p.packetLength);
}
```

### Step 6: Add Function Declaration

**File:** `src/map/clif.hpp`

```cpp
// Add near other clif_parse_* declarations
void clif_parse_custom_quest_info(int32 fd, map_session_data *sd);

// Add near other clif_* declarations
void clif_custom_quest_data(map_session_data *sd, uint32 quest_id);
```

### Step 7: Usage in Game Code

```cpp
// In your quest system code
void quest_show_info(map_session_data *sd, uint32 quest_id)
{
    // Send quest data to player
    clif_custom_quest_data(sd, quest_id);
}

// Triggered by script command
BUILDIN_FUNC(showquestinfo)
{
    map_session_data *sd = script_rid2sd(st);
    uint32 quest_id = script_getnum(st, 2);

    if (sd)
        clif_custom_quest_data(sd, quest_id);

    return SCRIPT_CMD_SUCCESS;
}
```

### Variable-Length Custom Packet Example

```cpp
// Packet with variable-length array
struct PACKET_ZC_CUSTOM_ITEM_LIST_sub {
    uint32 itemId;
    uint16 amount;
} __attribute__((packed));

struct PACKET_ZC_CUSTOM_ITEM_LIST {
    int16 packetType;
    int16 packetLength;
    uint16 itemCount;
    struct PACKET_ZC_CUSTOM_ITEM_LIST_sub items[];
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_CUSTOM_ITEM_LIST, 0x0d02)

// Sender implementation
void clif_custom_item_list(map_session_data *sd, uint32 *item_ids, uint16 count)
{
    int32 fd = sd->fd;
    int i;

    // Calculate total packet size
    int packet_len = sizeof(PACKET_ZC_CUSTOM_ITEM_LIST) +
                     (count * sizeof(PACKET_ZC_CUSTOM_ITEM_LIST_sub));

    // Allocate and build packet
    WFIFOHEAD(fd, packet_len);
    WFIFOW(fd, 0) = HEADER_ZC_CUSTOM_ITEM_LIST;
    WFIFOW(fd, 2) = packet_len;
    WFIFOW(fd, 4) = count;

    // Fill item array
    for (i = 0; i < count; i++) {
        int offset = 6 + (i * sizeof(PACKET_ZC_CUSTOM_ITEM_LIST_sub));
        WFIFOL(fd, offset + 0) = item_ids[i];
        WFIFOW(fd, offset + 4) = 1;  // amount
    }

    WFIFOSET(fd, packet_len);
}
```

---

## 9. Common Packet Patterns

### Player Data Packets

```cpp
/// Send player stat update
/// 00b0 <var id>.W <value>.L (ZC_PAR_CHANGE)
void clif_updatestatus(map_session_data *sd, int32 type)
{
    int32 fd = sd->fd;
    int32 len = packet_len(0xb0);

    WFIFOHEAD(fd, len);
    WFIFOW(fd, 0) = 0xb0;
    WFIFOW(fd, 2) = type;   // Status type (SP_*, e.g., SP_HP)

    switch (type) {
        case SP_HP:
            WFIFOL(fd, 4) = sd->battle_status.hp;
            break;
        case SP_MAXHP:
            WFIFOL(fd, 4) = sd->battle_status.max_hp;
            break;
        case SP_SP:
            WFIFOL(fd, 4) = sd->battle_status.sp;
            break;
        // ... more cases
    }

    WFIFOSET(fd, len);
}
```

### Inventory Packets

```cpp
/// Item pickup acknowledgment
void clif_additem(map_session_data *sd, int32 n, int32 amount, unsigned char fail)
{
    int32 fd = sd->fd;

    PACKET_ZC_ITEM_PICKUP_ACK p = {};

    if (fail) {
        // Failed to pickup
        p.result = fail;
    } else {
        // Successful pickup - fill item data
        p.index = client_index(n);
        p.count = amount;
        p.nameid = client_nameid(sd->inventory.u.items_inventory[n].nameid);
        p.IsIdentified = sd->inventory.u.items_inventory[n].identify;
        p.IsDamaged = sd->inventory.u.items_inventory[n].attribute;
        p.refiningLevel = sd->inventory.u.items_inventory[n].refine;
        // ... fill more fields
        p.result = 0;  // Success
    }

    p.packetType = HEADER_ZC_ITEM_PICKUP_ACK;

    WFIFOHEAD(fd, sizeof(p));
    memcpy(WFIFOP(fd, 0), &p, sizeof(p));
    WFIFOSET(fd, sizeof(p));
}
```

### Skill Packets

```cpp
/// Update single skill information
void clif_skillinfo(map_session_data& sd, uint16 skill_id, int32 inf)
{
    uint16 idx = skill_get_index(skill_id);
    if (idx == 0)
        return;

    PACKET_ZC_SKILLINFO_UPDATE2 p = {};

    p.packetType = HEADER_ZC_SKILLINFO_UPDATE2;
    p.id = skill_id;
    p.level = sd.status.skill[idx].lv;
    p.sp = skill_get_sp(skill_id, sd.status.skill[idx].lv);
    p.range = skill_get_range2(&sd.bl, skill_id, sd.status.skill[idx].lv, false);
    p.upgradable = (sd.status.skill[idx].lv < skill_tree_get_max(skill_id, sd.status.class_));

    clif_send(&p, sizeof(p), &sd.bl, SELF);
}
```

### Chat Packets

```cpp
/// Broadcast message to all players
void clif_broadcast(block_list* bl, const char* mes, int32 len, int32 type, enum send_target target)
{
    PACKET_ZC_BROADCAST *packet = (PACKET_ZC_BROADCAST*)packet_buffer;

    packet->packetType = HEADER_ZC_BROADCAST;
    packet->packetLength = sizeof(PACKET_ZC_BROADCAST) + len;
    safestrncpy(packet->message, mes, len);

    clif_send(packet, packet->packetLength, bl, target);
}

/// Parse global chat message from client
void clif_parse_GlobalMessage(int32 fd, map_session_data* sd)
{
    char name[NAME_LENGTH], message[CHAT_SIZE_MAX];
    char output[CHAT_SIZE_MAX + NAME_LENGTH * 2];
    size_t length;

    // Validate and extract message
    if (!clif_process_message(sd, false, name, message, output))
        return;

    // Send to other players
    clif_GlobalMessage(*sd, output, sd->chatID ? CHAT_WOS : AREA_CHAT_WOC);

    // Echo back to sender
    length = strlen(output) + 1;
    WFIFOHEAD(fd, 4 + length);
    WFIFOW(fd, 0) = 0x8e;
    WFIFOW(fd, 2) = 4 + length;
    safestrncpy(WFIFOCP(fd, 4), output, length);
    WFIFOSET(fd, 4 + length);
}
```

### Trade Packets

```cpp
/// Send trade request
void clif_traderequest(map_session_data* sd, const char* name)
{
    int32 fd = sd->fd;

    WFIFOHEAD(fd, 30);
    WFIFOW(fd, 0) = 0xe5;
    safestrncpy(WFIFOCP(fd, 2), name, NAME_LENGTH);
    WFIFOSET(fd, 30);
}

/// Parse trade acknowledgment
void clif_parse_TradeAck(int32 fd, map_session_data *sd)
{
    uint8 response = RFIFOB(fd, packet_db[RFIFOW(fd, 0)].pos[0]);

    trade_tradeack(sd, response);
}
```

### Movement Packets

```cpp
/// Notify player of their own movement
void clif_walkok(map_session_data *sd)
{
    int32 fd = sd->fd;

    WFIFOHEAD(fd, 6);
    WFIFOW(fd, 0) = 0x87;
    WFIFOL(fd, 2) = (uint32)gettick();
    WFIFOSET(fd, 6);
}

/// Parse walk request from client
void clif_parse_WalkToXY(int32 fd, map_session_data *sd)
{
    int16 x, y;

    // Validate state
    if (pc_isdead(sd)) {
        clif_clearunit_area(*sd, CLR_DEAD);
        return;
    }

    if (pc_cant_act(sd))
        return;

    // Parse position
    RFIFOPOS(fd, packet_db[RFIFOW(fd, 0)].pos[0], &x, &y, nullptr);

    // Execute movement
    unit_walktoxy(&sd->bl, x, y, 4);
}
```

---

## 10. Security and Validation

Critical security practices for packet handling to prevent exploits and crashes.

### Input Validation Rules

**Always validate:**
1. Player state (alive, not in action, session active)
2. Packet length (for variable-length packets)
3. Array indices (inventory, skills, etc.)
4. String termination
5. Value ranges (amounts, IDs, etc.)

### Player State Validation

```cpp
void clif_parse_example(int32 fd, map_session_data *sd)
{
    // Check if player exists
    if (!sd)
        return;

    // Check if session is active
    if (!session_isActive(fd))
        return;

    // Check if player is in valid state
    if (!sd->bl.prev)  // Not on map
        return;

    // Check if player is dead
    if (pc_isdead(sd)) {
        clif_clearunit_area(*sd, CLR_DEAD);
        return;
    }

    // Check if player can act
    if (pc_cant_act(sd))
        return;

    // Process packet...
}
```

### Packet Length Validation

```cpp
void clif_parse_variable_packet(int32 fd, map_session_data *sd)
{
    uint16 packet_len = RFIFOW(fd, 2);  // Declared length
    uint16 expected_len;

    // Validate minimum length
    if (packet_len < 4) {
        ShowWarning("Invalid packet length: %u from %s\n",
                    packet_len, sd->status.name);
        return;
    }

    // Validate maximum length
    if (packet_len > 32768) {
        ShowWarning("Packet too large: %u from %s\n",
                    packet_len, sd->status.name);
        return;
    }

    // Check if full packet received
    if (RFIFOREST(fd) < packet_len) {
        return;  // Wait for more data
    }

    // Calculate expected length based on count
    uint16 count = RFIFOW(fd, 4);
    expected_len = 6 + (count * sizeof(struct item_data));

    if (packet_len != expected_len) {
        ShowWarning("Packet length mismatch: got %u, expected %u from %s\n",
                    packet_len, expected_len, sd->status.name);
        return;
    }

    // Process packet...
}
```

### Index Bounds Checking

```cpp
void clif_parse_UseItem(int32 fd, map_session_data *sd)
{
    struct s_packet_db* info = &packet_db[RFIFOW(fd, 0)];
    int32 index = RFIFOW(fd, info->pos[0]) - 2;  // Client index to server index

    // Validate index range
    if (index < 0 || index >= MAX_INVENTORY) {
        clif_useitemack(sd, 0, 0, 0);
        ShowWarning("clif_parse_UseItem: Invalid item index %d from %s\n",
                    index, sd->status.name);
        return;
    }

    // Validate item exists
    if (sd->inventory.u.items_inventory[index].nameid == 0) {
        clif_useitemack(sd, 0, 0, 0);
        return;
    }

    // Process item use
    pc_useitem(sd, index);
}
```

### String Validation

```cpp
bool clif_process_message(map_session_data *sd, bool whisperFormat,
                          char *out_name, char *out_message, char *out_output)
{
    char *input = (char*)RFIFOP(fd, 4);
    size_t inputLength = RFIFOW(fd, 2) - 4;
    size_t nameLength, messageLength;

    // Validate input length
    if (inputLength < 1) {
        ShowWarning("clif_process_message: Empty message from %s\n",
                    sd->status.name);
        return false;
    }

    if (whisperFormat) {
        // Name has fixed width
        if (inputLength < NAME_LENGTH + 1) {
            ShowWarning("clif_process_message: Malformed packet from %s\n",
                        sd->status.name);
            return false;
        }

        // Validate name is null-terminated
        nameLength = strnlen(input, NAME_LENGTH - 1);
        if (input[nameLength] != '\0') {
            ShowWarning("clif_process_message: Unterminated name from %s\n",
                        sd->status.name);
            return false;
        }

        safestrncpy(out_name, input, NAME_LENGTH);
        input += NAME_LENGTH;
    }

    // Validate message length
    messageLength = inputLength - (whisperFormat ? NAME_LENGTH : 0);
    if (messageLength > CHAT_SIZE_MAX - 1) {
        ShowWarning("clif_process_message: Message too long from %s\n",
                    sd->status.name);
        return false;
    }

#if PACKETVER < 20151001
    // Validate null termination
    if (input[messageLength - 1] != '\0') {
        ShowWarning("clif_process_message: Unterminated message from %s\n",
                    sd->status.name);
        return false;
    }
#endif

    safestrncpy(out_message, input, messageLength);
    return true;
}
```

### Value Range Validation

```cpp
void clif_parse_StatusUp(int32 fd, map_session_data *sd)
{
    uint16 status_type = RFIFOW(fd, 2);
    uint8 increase_amount = RFIFOB(fd, 4);

    // Validate status type
    if (status_type < SP_STR || status_type > SP_LUK) {
        ShowWarning("clif_parse_StatusUp: Invalid status type %u from %s\n",
                    status_type, sd->status.name);
        return;
    }

    // Validate increase amount
    if (increase_amount < 1 || increase_amount > 100) {
        ShowWarning("clif_parse_StatusUp: Invalid amount %u from %s\n",
                    increase_amount, sd->status.name);
        return;
    }

    // Process status increase
    pc_statusup(sd, status_type, increase_amount);
}
```

### Duplicate Action Prevention

```cpp
void clif_parse_TradeRequest(int32 fd, map_session_data *sd)
{
    map_session_data *target_sd;
    uint32 target_id = RFIFOL(fd, 2);

    // Check if already in trade
    if (sd->state.trading) {
        clif_tradestart(sd, 2);  // Already in trade
        return;
    }

    // Check if in other activities
    if (sd->npc_id || sd->state.vending || sd->state.buyingstore) {
        clif_tradestart(sd, 2);
        return;
    }

    // Validate target
    target_sd = map_id2sd(target_id);
    if (!target_sd || !target_sd->bl.prev) {
        clif_tradestart(sd, 1);  // Target not found
        return;
    }

    // Process trade request
    trade_traderequest(sd, target_sd);
}
```

### Session Validation

```cpp
void clif_example_send(map_session_data *sd)
{
    nullpo_retv(sd);

    int32 fd = sd->fd;

    // Always check session is active before sending
    if (!session_isActive(fd))
        return;

    // Check func_parse to ensure it's a player connection
    if (session[fd]->func_parse != clif_parse) {
        ShowError("clif_example_send: Invalid session type\n");
        return;
    }

    // Safe to send packet
    WFIFOHEAD(fd, packet_len);
    // ...
    WFIFOSET(fd, packet_len);
}
```

---

## 11. Debugging Packets

### Enable Packet Logging

**File:** `src/config/packets.hpp`

```cpp
// Uncomment to enable packet dumping
#define DUMP_UNKNOWN_PACKET     // Log unknown packets
#define DUMP_INVALID_PACKET     // Log invalid/malformed packets
```

### ShowDebug Packet Information

```cpp
void clif_parse_example(int32 fd, map_session_data *sd)
{
    // Log packet reception
    ShowDebug("clif_parse_example: Received from %s (AID:%d CID:%d)\n",
              sd->status.name, sd->status.account_id, sd->status.char_id);

    // Dump packet data
    uint16 packet_id = RFIFOW(fd, 0);
    uint16 packet_len = packet_db[packet_id].len;

    if (packet_len == -1)
        packet_len = RFIFOW(fd, 2);

    ShowDebug("Packet 0x%04x, Length: %u\n", packet_id, packet_len);

    // Hex dump
    int i;
    for (i = 0; i < packet_len; i++) {
        ShowDebug("%02X ", RFIFOB(fd, i));
        if ((i + 1) % 16 == 0)
            ShowDebug("\n");
    }
    ShowDebug("\n");
}
```

### Packet Viewer Function

```cpp
void clif_dump_packet(const unsigned char *packet, int32 length, const char *label)
{
    int i;

    ShowInfo("=== Packet Dump: %s ===\n", label);
    ShowInfo("Packet ID: 0x%04x\n", RBUFW(packet, 0));
    ShowInfo("Length: %d bytes\n", length);
    ShowInfo("Raw Data:\n");

    for (i = 0; i < length; i++) {
        printf("%02X ", packet[i]);
        if ((i + 1) % 16 == 0)
            printf("\n");
    }

    if (length % 16 != 0)
        printf("\n");

    ShowInfo("========================\n");
}

// Usage:
void clif_parse_custom(int32 fd, map_session_data *sd)
{
    clif_dump_packet(RFIFOP(fd, 0), packet_db[RFIFOW(fd, 0)].len, "Custom Packet");
    // Process packet...
}
```

### Wireshark Packet Capture

**Setup Wireshark Filter:**
```
tcp.port == 6900
```

**Ragnarok-Specific Dissector:**
1. Save Ragnarok packet definitions
2. Load as Wireshark dissector
3. View packets in human-readable format

**Common Filters:**
```
# Filter by packet ID
tcp.port == 6900 && data[0:2] == 8e:00   # 0x8e (chat)

# Filter by IP
ip.addr == 127.0.0.1 && tcp.port == 6900
```

### Debug Commands

```cpp
// In clif.cpp - add debug command
ACMD_FUNC(debugpacket)
{
    if (!message || !*message) {
        clif_displaymessage(fd, "Usage: @debugpacket <on|off>");
        return COMMAND_FAILURE;
    }

    if (strcmpi(message, "on") == 0) {
        sd->debug_packet = 1;
        clif_displaymessage(fd, "Packet debugging enabled.");
    } else {
        sd->debug_packet = 0;
        clif_displaymessage(fd, "Packet debugging disabled.");
    }

    return COMMAND_SUCCESS;
}

// In packet handlers
void clif_parse_example(int32 fd, map_session_data *sd)
{
    if (sd->debug_packet) {
        clif_dump_packet(RFIFOP(fd, 0), packet_db[RFIFOW(fd, 0)].len,
                        "clif_parse_example");
    }
    // Process packet...
}
```

### Logging Packet Flow

```cpp
// Add to src/map/log.cpp
void log_packet(map_session_data *sd, uint16 packet_id, bool incoming,
                const void *data, size_t len)
{
    if (!log_config.enable_packet_log)
        return;

    FILE *fp = fopen("log/packets.log", "a");
    if (!fp)
        return;

    time_t now = time(nullptr);
    struct tm *t = localtime(&now);

    fprintf(fp, "[%04d-%02d-%02d %02d:%02d:%02d] %s Packet 0x%04x (%u bytes) - %s (AID:%d)\n",
            t->tm_year + 1900, t->tm_mon + 1, t->tm_mday,
            t->tm_hour, t->tm_min, t->tm_sec,
            incoming ? "IN " : "OUT",
            packet_id, (uint32)len,
            sd->status.name, sd->status.account_id);

    fclose(fp);
}
```

### Runtime Packet Testing

```cpp
// Test packet sending in-game
ACMD_FUNC(testpacket)
{
    uint16 packet_id;

    if (!message || !*message || sscanf(message, "%hx", &packet_id) != 1) {
        clif_displaymessage(fd, "Usage: @testpacket <packet_id in hex>");
        return COMMAND_FAILURE;
    }

    // Example: send test packet
    WFIFOHEAD(fd, 10);
    WFIFOW(fd, 0) = packet_id;
    WFIFOW(fd, 2) = 10;
    WFIFOL(fd, 4) = 12345;
    WFIFOW(fd, 8) = 999;
    WFIFOSET(fd, 10);

    safesnprintf(atcmd_output, sizeof(atcmd_output),
                 "Sent test packet 0x%04x", packet_id);
    clif_displaymessage(fd, atcmd_output);

    return COMMAND_SUCCESS;
}
```

---

## 12. Real-World Examples

### Example 1: Item Drop System

```cpp
// From src/map/clif.cpp

/// Drop item acknowledgment
/// 00af <index>.W <amount>.W (ZC_ITEM_THROW_ACK)
void clif_dropitem(map_session_data *sd, int32 n, int32 amount)
{
    nullpo_retv(sd);

    int32 fd = sd->fd;

    if (!session_isActive(fd))
        return;

    WFIFOHEAD(fd, 6);
    WFIFOW(fd, 0) = 0xaf;
    WFIFOW(fd, 2) = client_index(n);
    WFIFOW(fd, 4) = (uint16)amount;
    WFIFOSET(fd, 6);
}

/// Request to drop an item
/// 00a2 <index>.W <amount>.W (CZ_ITEM_THROW)
void clif_parse_DropItem(int32 fd, map_session_data *sd)
{
    struct s_packet_db* info = &packet_db[RFIFOW(fd, 0)];
    int32 item_index = RFIFOW(fd, info->pos[0]) - 2;
    int32 item_amount = RFIFOW(fd, info->pos[1]);

    // Validate state
    if (pc_isdead(sd))
        return;

    if (pc_cant_act2(sd) || sd->npc_id)
        return;

    if (sd->state.storage_flag || sd->state.vending || sd->state.buyingstore)
        return;

    // Validate index
    if (item_index < 0 || item_index >= MAX_INVENTORY) {
        clif_dropitem(sd, 0, 0);
        return;
    }

    // Validate amount
    if (item_amount <= 0 || item_amount > sd->inventory.u.items_inventory[item_index].amount) {
        clif_dropitem(sd, 0, 0);
        return;
    }

    // Check if item can be dropped
    if (!pc_candrop(sd, &sd->inventory.u.items_inventory[item_index])) {
        clif_displaymessage(fd, msg_txt(sd, 263)); // This item cannot be dropped.
        return;
    }

    // Drop item
    pc_dropitem(sd, item_index, item_amount);
}
```

### Example 2: Skill System

```cpp
// From src/map/clif.cpp

/// Use skill on target
/// 0113 <level>.W <skill id>.W <target id>.L (CZ_USE_SKILL)
void clif_parse_UseSkillToId(int32 fd, map_session_data *sd)
{
    struct s_packet_db *info = &packet_db[RFIFOW(fd, 0)];
    uint16 skill_lv = RFIFOW(fd, info->pos[0]);
    uint16 skill_id = RFIFOW(fd, info->pos[1]);
    uint32 target_id = RFIFOL(fd, info->pos[2]);

    // Validate state
    if (pc_isdead(sd))
        return;

    if (pc_cant_act2(sd))
        return;

    // Validate skill
    if (skill_lv < 1)
        skill_lv = 1;

    uint16 skill_idx = skill_get_index(skill_id);
    if (skill_idx == 0 || skill_id >= GD_SKILLBASE)
        return;

    // Check if player has skill
    if (skill_lv > sd->status.skill[skill_idx].lv) {
        clif_skill_fail(sd, skill_id, USESKILL_FAIL_LEVEL, 0);
        return;
    }

    // Use skill
    unit_skilluse_id(&sd->bl, target_id, skill_id, skill_lv);
}

/// Skill use acknowledgment
/// 0110 <skill id>.W <btype>.L <damage>.W <target id>.L <result>.B (ZC_NOTIFY_SKILL)
void clif_skill_damage(block_list *src, block_list *dst, t_tick tick,
                       int32 sdelay, int32 ddelay, int64 damage, int32 div,
                       uint16 skill_id, uint16 skill_lv, int32 type)
{
    unsigned char buf[64];
    status_change *sc;

    // Build packet
    WBUFW(buf, 0) = 0x1de;
    WBUFW(buf, 2) = skill_id;
    WBUFL(buf, 4) = src->id;
    WBUFL(buf, 8) = dst->id;
    WBUFL(buf, 12) = (uint32)tick;
    WBUFL(buf, 16) = sdelay;
    WBUFL(buf, 20) = ddelay;

    // Clamp damage for client display
    if (damage > INT_MAX)
        damage = INT_MAX;
    else if (damage < INT_MIN)
        damage = INT_MIN;

    WBUFL(buf, 24) = (int32)damage;
    WBUFW(buf, 28) = skill_lv;
    WBUFW(buf, 30) = div;
    WBUFB(buf, 32) = (type > 0) ? type : skill_get_hit(skill_id);

    // Send to area
    clif_send(buf, 33, dst, AREA);
}
```

### Example 3: Chat System

```cpp
// From src/map/clif.cpp

/// Global message (Chat)
/// 008e <packet len>.W <message>.?B (ZC_NOTIFY_CHAT)
void clif_GlobalMessage(map_session_data& sd, const char *message, send_target target)
{
    size_t len = strlen(message) + 1;

    // Validate length
    if (len > CHAT_SIZE_MAX)
        len = CHAT_SIZE_MAX;

    // Build packet
    WFIFOHEAD(sd.fd, 4 + len);
    WFIFOW(sd.fd, 0) = 0x8e;
    WFIFOW(sd.fd, 2) = 4 + len;
    safestrncpy(WFIFOCP(sd.fd, 4), message, len);

    // Send based on target type
    if (target == SELF)
        WFIFOSET(sd.fd, 4 + len);
    else
        clif_send(WFIFOP(sd.fd, 0), 4 + len, &sd.bl, target);
}

/// Parse global message from client
/// 008c <packet len>.W <message>.?B (CZ_REQUEST_CHAT)
void clif_parse_GlobalMessage(int32 fd, map_session_data* sd)
{
    char name[NAME_LENGTH];
    char message[CHAT_SIZE_MAX];
    char output[CHAT_SIZE_MAX + NAME_LENGTH * 2];
    size_t length;

    // Validate and process message
    if (!clif_process_message(sd, false, name, message, output))
        return;

    // Check if in channel
    if (sd->gcbind && ((sd->gcbind->opt & CHAN_OPT_CAN_CHAT) ||
                       pc_has_permission(sd, PC_PERM_CHANNEL_ADMIN))) {
        channel_send(sd->gcbind, sd, message);
        return;
    }

    // Send to area
    clif_GlobalMessage(*sd, output, sd->chatID ? CHAT_WOS : AREA_CHAT_WOC);

    // Echo back to sender
    length = strlen(output) + 1;
    WFIFOHEAD(fd, 4 + length);
    WFIFOW(fd, 0) = 0x8e;
    WFIFOW(fd, 2) = 4 + length;
    safestrncpy(WFIFOCP(fd, 4), output, length);
    WFIFOSET(fd, 4 + length);

#ifdef PCRE_SUPPORT
    // Trigger NPC chat listeners
    map_foreachinallrange(npc_chat_sub, sd, AREA_SIZE, BL_NPC,
                          output, strlen(output), sd);
#endif
}
```

### Example 4: Banking System

```cpp
// From src/map/clif.cpp

/// Bank deposit request
/// 09a7 <account id>.L <money>.L (CZ_REQ_BANKING_DEPOSIT)
void clif_parse_BankDeposit(int32 fd, map_session_data* sd)
{
    const PACKET_CZ_REQ_BANKING_DEPOSIT *p =
        (PACKET_CZ_REQ_BANKING_DEPOSIT*)RFIFOP(fd, 0);

    int32 money = p->zeny;

    // Validate amount
    if (money <= 0 || money > sd->status.zeny) {
        clif_bank_deposit(sd, BDA_NO_MONEY);
        return;
    }

    // Check for overflow
    if (sd->status.bank_vault + money > MAX_BANK_ZENY) {
        clif_bank_deposit(sd, BDA_OVERFLOW);
        return;
    }

    // Process deposit
    if (pc_payzeny(sd, money, LOG_TYPE_BANK, nullptr) == 0) {
        sd->status.bank_vault += money;
        clif_bank_deposit(sd, BDA_SUCCESS);
    } else {
        clif_bank_deposit(sd, BDA_ERROR);
    }
}

/// Bank deposit result
/// 09a8 <reason>.W <money>.Q <balance>.L (ZC_ACK_BANKING_DEPOSIT)
void clif_bank_deposit(map_session_data *sd, enum e_BANKING_DEPOSIT_ACK reason)
{
    nullpo_retv(sd);

    int32 fd = sd->fd;

    WFIFOHEAD(fd, 16);
    WFIFOW(fd, 0) = 0x9a8;
    WFIFOW(fd, 2) = (uint16)reason;
    WFIFOQ(fd, 4) = sd->status.bank_vault;
    WFIFOL(fd, 12) = sd->status.zeny;
    WFIFOSET(fd, 16);
}
```

### Example 5: Variable-Length Inventory List

```cpp
// From src/map/clif.cpp

/// Send inventory list to client
void clif_inventorylist(map_session_data *sd)
{
    int i, n, ne, fd = sd->fd;
    PACKET_ZC_INVENTORY_ITEMLIST_NORMAL *normal = nullptr;

    // Count items
    for (i = 0, n = 0; i < MAX_INVENTORY; i++) {
        if (sd->inventory.u.items_inventory[i].nameid > 0 &&
            sd->inventory_data[i] &&
            !itemdb_isstackable2(sd->inventory_data[i]))
            n++;
    }

    // Calculate packet size
    int cmd = inventorylistnormalType;
    int packet_len = sizeof(PACKET_ZC_INVENTORY_ITEMLIST_NORMAL) +
                     (n * sizeof(struct NORMALITEM_INFO));

    // Allocate packet
    normal = (PACKET_ZC_INVENTORY_ITEMLIST_NORMAL*)aMalloc(packet_len);
    normal->packetType = cmd;
    normal->packetLength = packet_len;

    // Fill item data
    for (i = 0, n = 0; i < MAX_INVENTORY; i++) {
        if (sd->inventory.u.items_inventory[i].nameid <= 0 ||
            !sd->inventory_data[i] ||
            itemdb_isstackable2(sd->inventory_data[i]))
            continue;

        normal->items[n].index = client_index(i);
        normal->items[n].nameid = client_nameid(sd->inventory.u.items_inventory[i].nameid);
        normal->items[n].type = itemtype(sd->inventory.u.items_inventory[i].nameid);
        normal->items[n].amount = sd->inventory.u.items_inventory[i].amount;
        normal->items[n].location = pc_equippoint(sd, i);
        // ... fill more fields
        n++;
    }

    // Send packet
    clif_send(normal, packet_len, &sd->bl, SELF);
    aFree(normal);
}
```

---

## Summary

This reference covers the complete packet system in rAthena:

1. **Naming conventions** - Understand CZ_*/ZC_* prefixes for packet direction
2. **CLIF structure** - `clif_*` for sending, `clif_parse_*` for receiving
3. **Packet definitions** - Use `__attribute__((packed))` and proper structure
4. **PACKETVER** - Support multiple client versions with conditional compilation
5. **Registration** - Register packets in `clif_packetdb.hpp` with handlers
6. **WFIFO/RFIF macros** - Read and write binary packet data
7. **Custom packets** - Follow 8-step process for new features
8. **Common patterns** - Player data, inventory, skills, chat, movement
9. **Security** - Always validate input, indices, lengths, and state
10. **Debugging** - Use packet logging, Wireshark, and debug commands
11. **Real examples** - Study working code from clif.cpp

**Key Files:**
- `src/map/clif.cpp` - Implementation
- `src/map/clif.hpp` - Declarations
- `src/map/packets.hpp` - Packet structures
- `src/map/clif_packetdb.hpp` - Packet registration
- `src/config/packets.hpp` - PACKETVER settings
- `src/common/socket.hpp` - FIFO macros

**Best Practices:**
- Always use `__attribute__((packed))` on packet structures
- Validate all input from clients
- Check session state before sending
- Use proper WFIFOHEAD before writing
- Test with different PACKETVERs
- Log suspicious activity
- Follow existing patterns

**Next Steps:**
- Study real packets in clif.cpp
- Review packet structures in packets.hpp
- Test custom packets with different clients
- Monitor packet flow with debugging tools
- Contribute documentation for custom features

---

**Document Size:** ~22KB
**Last Updated:** 2025
**Maintained By:** rAthena Community

# ═══════════════════════════════════════════════════════════════
# PART 3: COMPILATION & DEBUGGING
# ═══════════════════════════════════════════════════════════════
# rAthena Compilation & Debugging Reference

## Table of Contents
1. [Build Systems](#build-systems)
2. [Dependencies](#dependencies)
3. [Build Options & Configuration](#build-options--configuration)
4. [Compilation Commands](#compilation-commands)
5. [GDB Debugging](#gdb-debugging)
6. [Visual Studio Debugging](#visual-studio-debugging)
7. [Memory Leak Detection](#memory-leak-detection)
8. [Profiling & Performance Analysis](#profiling--performance-analysis)
9. [Common Errors & Fixes](#common-errors--fixes)
10. [Continuous Integration Setup](#continuous-integration-setup)
11. [Optimization Flags](#optimization-flags)
12. [Real Debugging Scenarios](#real-debugging-scenarios)

---

## Build Systems

### CMake (Recommended - Cross-Platform)

**Directory Structure:**
```
rathena/
├── CMakeLists.txt           # Root CMake configuration
├── 3rdparty/
│   └── CMakeLists.txt       # Third-party dependencies
├── src/
│   ├── CMakeLists.txt       # Main source configuration
│   ├── common/CMakeLists.txt
│   ├── map/CMakeLists.txt
│   ├── char/CMakeLists.txt
│   └── login/CMakeLists.txt
└── build/                   # Build output directory
```

**Basic CMake Build Process:**
```bash
# Create build directory
mkdir build && cd build

# Configure (generate build files)
cmake ..

# Build
cmake --build . --parallel 4

# Install (optional)
cmake --install .
```

**Advanced CMake Configuration:**
```bash
# Debug build with all debug symbols
cmake -DCMAKE_BUILD_TYPE=Debug ..

# Release build with optimizations
cmake -DCMAKE_BUILD_TYPE=Release ..

# RelWithDebInfo (optimized with debug symbols)
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo ..

# MinSizeRel (optimized for size)
cmake -DCMAKE_BUILD_TYPE=MinSizeRel ..

# Custom install prefix
cmake -DCMAKE_INSTALL_PREFIX=/opt/rathena ..

# Enable Renewal mode
cmake -DRENEWAL=ON ..

# Set packet version
cmake -DPACKETVER=20211103 ..

# Set maximum level
cmake -DMAX_LEVEL=175 ..

# Enable PCRE support
cmake -DWITH_PCRE=ON ..

# Custom MySQL location
cmake -DMYSQL_INCLUDE_DIR=/usr/include/mysql \
      -DMYSQL_LIBRARY=/usr/lib/x86_64-linux-gnu/libmysqlclient.so ..

# Ninja generator (faster builds)
cmake -G Ninja ..
```

**CMake Cache Variables:**
```bash
# View all cache variables
cmake -LAH

# Clear cache
rm CMakeCache.txt

# Reconfigure from scratch
rm -rf CMakeFiles CMakeCache.txt
cmake ..
```

**Key CMakeLists.txt Sections:**
```cmake
# Minimum version
cmake_minimum_required(VERSION 3.10)

# Project definition
project(rAthena LANGUAGES C CXX)

# C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Build options
option(RENEWAL "Enable Renewal mode" ON)
option(WITH_PCRE "Enable PCRE support" ON)
option(BUILD_SERVERS "Build server executables" ON)
option(BUILD_TOOLS "Build tool executables" ON)

# Add subdirectories
add_subdirectory(3rdparty)
add_subdirectory(src/common)
add_subdirectory(src/map)
add_subdirectory(src/char)
add_subdirectory(src/login)

# Executable target
add_executable(map-server ${MAP_SOURCES})
target_link_libraries(map-server common ${MYSQL_LIBRARY} ${PCRE_LIBRARY})
```

### Configure Script (Legacy - Linux/Unix)

**Basic Usage:**
```bash
# Generate configure script (if from Git)
./autogen.sh

# Configure
./configure

# Build
make clean
make -j4

# Install
make install
```

**Configure Options:**
```bash
# Enable debug mode
./configure --enable-debug

# Enable Renewal
./configure --enable-renewal

# Custom packet version
./configure --enable-packetver=20211103

# Custom max level
./configure --enable-maxlevel=175

# Disable PCRE
./configure --without-pcre

# Custom MySQL path
./configure --with-mysql=/usr/local/mysql

# Install prefix
./configure --prefix=/opt/rathena

# All options
./configure --help
```

**Key Files:**
- `configure.ac` - Autoconf configuration
- `Makefile.in` - Makefile template
- `config.log` - Configuration log (check for errors)
- `config.status` - Configuration state

### Visual Studio (Windows)

**Project Structure:**
```
rathena.sln                  # Solution file
├── char-server.vcxproj      # Character server project
├── login-server.vcxproj     # Login server project
├── map-server.vcxproj       # Map server project
├── common.vcxproj           # Common library
└── 3rdparty/                # Dependencies
    ├── mysql/
    ├── pcre/
    └── zlib/
```

**Build Configurations:**
- **Debug**: No optimizations, full debug info, runtime checks
- **Release**: Full optimizations, no debug info
- **RelWithDebInfo**: Optimizations + debug symbols
- **MinSizeRel**: Optimize for size

**Project Properties:**
```
Configuration Properties
├── General
│   ├── Output Directory: $(SolutionDir)bin\$(Configuration)\
│   ├── Intermediate Directory: $(SolutionDir)obj\$(Configuration)\$(ProjectName)\
│   └── Configuration Type: Application (.exe)
├── C/C++
│   ├── General
│   │   └── Additional Include Directories
│   ├── Preprocessor
│   │   └── Preprocessor Definitions (PACKETVER, RENEWAL, etc.)
│   ├── Code Generation
│   │   └── Runtime Library: /MD or /MDd
│   └── Optimization
│       └── Optimization: /O2 (Release), /Od (Debug)
└── Linker
    ├── General
    │   └── Additional Library Directories
    └── Input
        └── Additional Dependencies (libmysql.lib, pcre.lib, etc.)
```

**Batch Building:**
```batch
REM Build all configurations
MSBuild rathena.sln /p:Configuration=Debug /m
MSBuild rathena.sln /p:Configuration=Release /m

REM Build specific project
MSBuild map-server.vcxproj /p:Configuration=Debug

REM Clean and rebuild
MSBuild rathena.sln /t:Clean,Build /p:Configuration=Release /m
```

---

## Dependencies

### MySQL/MariaDB

**Installation:**
```bash
# Ubuntu/Debian
sudo apt-get install libmariadb-dev libmariadb-dev-compat

# CentOS/RHEL
sudo yum install mysql-devel

# macOS
brew install mysql

# Windows
# Download MySQL Connector/C from mysql.com
# Extract to 3rdparty/mysql/
```

**Version Requirements:**
- MySQL 5.7+ or MariaDB 10.2+
- Connector/C or client library

**CMake Detection:**
```cmake
find_package(MySQL REQUIRED)
if(MYSQL_FOUND)
    include_directories(${MYSQL_INCLUDE_DIR})
    target_link_libraries(map-server ${MYSQL_LIBRARY})
endif()
```

**Common Issues:**
```bash
# MySQL not found
CMake Error: Could not find MySQL

# Fix: Set MySQL path manually
cmake -DMYSQL_INCLUDE_DIR=/usr/include/mysql \
      -DMYSQL_LIBRARY=/usr/lib/libmysqlclient.so ..

# Wrong MySQL library
# Fix: Ensure libmysqlclient, not libmysqld (embedded)
```

### PCRE (Perl Compatible Regular Expressions)

**Installation:**
```bash
# Ubuntu/Debian
sudo apt-get install libpcre3-dev

# CentOS/RHEL
sudo yum install pcre-devel

# macOS
brew install pcre

# Windows
# Download from https://www.pcre.org/
# Place in 3rdparty/pcre/
```

**Usage in Code:**
```cpp
// Script engine uses PCRE for pattern matching
#ifdef PCRE_SUPPORT
    pcre *re = pcre_compile(pattern, 0, &error, &erroffset, NULL);
    if (re && pcre_exec(re, NULL, str, strlen(str), 0, 0, ovector, 30) > 0) {
        // Match found
    }
#endif
```

**Build Without PCRE:**
```bash
cmake -DWITH_PCRE=OFF ..
# or
./configure --without-pcre
```

### zlib (Compression)

**Installation:**
```bash
# Ubuntu/Debian
sudo apt-get install zlib1g-dev

# CentOS/RHEL
sudo yum install zlib-devel

# macOS (usually pre-installed)
brew install zlib

# Windows
# Included in 3rdparty/zlib/
```

**Usage:**
- Packet compression
- Database compression
- Log file compression

### OpenSSL (Optional - For Encryption)

**Installation:**
```bash
# Ubuntu/Debian
sudo apt-get install libssl-dev

# CentOS/RHEL
sudo yum install openssl-devel

# macOS
brew install openssl
```

**Enable in Build:**
```bash
cmake -DWITH_OPENSSL=ON \
      -DOPENSSL_ROOT_DIR=/usr/local/opt/openssl ..
```

**Usage:**
- Login server password encryption
- Secure inter-server communication
- Web server integration

### Complete Dependency Install Scripts

**Ubuntu/Debian:**
```bash
#!/bin/bash
sudo apt-get update
sudo apt-get install -y \
    git \
    make \
    cmake \
    gcc \
    g++ \
    libmariadb-dev \
    libmariadb-dev-compat \
    libpcre3-dev \
    zlib1g-dev \
    libssl-dev
```

**CentOS/RHEL:**
```bash
#!/bin/bash
sudo yum install -y \
    git \
    make \
    cmake \
    gcc \
    gcc-c++ \
    mysql-devel \
    pcre-devel \
    zlib-devel \
    openssl-devel
```

---

## Build Options & Configuration

### PACKETVER (Client Version)

**What It Controls:**
- Client packet structures
- Available features per client version
- Packet encryption keys
- UI elements and display

**Setting PACKETVER:**
```cpp
// src/config/core.hpp
#define PACKETVER 20211103  // YYYYMMDD format

// CMake
cmake -DPACKETVER=20211103 ..

// Configure
./configure --enable-packetver=20211103
```

**Common Versions:**
```cpp
20211103  // 2021-11-03 (latest renewal)
20180620  // 2018-06-20 (popular stable)
20151104  // 2015-11-04 (pre-renewal compatible)
20120410  // 2012-04-10 (older stable)
```

**Version-Specific Code:**
```cpp
#if PACKETVER >= 20211103
    // New packet structure
    struct PACKET_ZC_NEW_ITEM {
        int16 packetType;
        uint32 itemId;
        // New fields...
    };
#else
    // Old packet structure
    struct PACKET_ZC_NEW_ITEM {
        int16 packetType;
        uint16 itemId;
        // Old fields...
    };
#endif
```

### RENEWAL Mode

**What It Changes:**
- Damage formulas
- Status point distribution
- Aspd calculations
- Monster stats and behavior
- Skill mechanics
- Experience tables

**Enabling RENEWAL:**
```cpp
// src/config/renewal.hpp
#define RENEWAL           // Enable all renewal features
#define RENEWAL_CAST      // Renewal cast system
#define RENEWAL_DROP      // Renewal drop rates
#define RENEWAL_EXP       // Renewal experience tables
#define RENEWAL_LVDMG     // Renewal level damage modifiers
#define RENEWAL_ASPD      // Renewal ASPD formula

// CMake
cmake -DRENEWAL=ON ..

// Configure
./configure --enable-renewal
```

**Conditional Compilation:**
```cpp
int battle_calc_damage(struct block_list *src, struct block_list *target) {
#ifdef RENEWAL
    // Renewal damage formula
    damage = (status_get_batk(src) + status_get_watk(src)) * skill_ratio / 100;
#else
    // Pre-renewal damage formula
    damage = status_get_batk(src) * skill_ratio / 100;
#endif
    return damage;
}
```

### MAX_LEVEL

**Configuration:**
```cpp
// src/config/core.hpp
#define MAX_LEVEL 99          // Base level cap
#define MAX_LEVEL_THIRD 175   // Third class level cap (Renewal)

// CMake
cmake -DMAX_LEVEL=175 ..

// Configure
./configure --enable-maxlevel=175
```

**Impact:**
```cpp
// Experience tables must match
// db/[pre-]re/exp_base.yml
// db/[pre-]re/exp_job.yml

// Status arrays sized accordingly
int status_point_table[MAX_LEVEL];
uint64 exp_table[MAX_LEVEL];
```

### Other Important Defines

**src/config/core.hpp:**
```cpp
// Inventory sizes
#define MAX_INVENTORY 100
#define MAX_STORAGE 600
#define MAX_CART 100

// Party/Guild
#define MAX_PARTY 12
#define MAX_GUILD 16+10*6  // 16 + 6 extension levels

// Skill limits
#define MAX_SKILL 5000
#define MAX_SKILL_LEVEL 20

// Chat/message
#define CHAT_SIZE_MAX 255
#define GLOBAL_REG_NUM 256

// Network
#define FIFOSIZE_SERVERLINK 512*1024
#define MAX_MAP_PER_SERVER 1500

// Security
#define MAX_ITEM_ID 65535
#define SECURE_NPCTIMEOUT
#define AUTOTRADE_PERSISTENCY

// Features
#define CELL_NOSTACK_LIMIT 1
#define OFFICIAL_WALKPATH
#define NEW_CARTS
#define SCRIPT_CALLFUNC_CHECK
```

**Feature Flags:**
```cpp
// Enable VIP system
#define VIP_ENABLE

// Enable bound item system
#define BOUND_ITEMS

// Enable banking system
#define BANK_VAULT

// Enable attendance system
#define ATTENDANCE_SYSTEM

// Enable item options (random options)
#define ITEM_OPTIONS

// Enable achievement system
#define ACHIEVEMENT_SYSTEM
```

---

## Compilation Commands

### Linux/Unix Full Build

**First-Time Build:**
```bash
#!/bin/bash
# Clone repository
git clone https://github.com/rathena/rathena.git
cd rathena

# Install dependencies (Ubuntu/Debian)
sudo apt-get update
sudo apt-get install -y git make cmake gcc g++ \
    libmariadb-dev libmariadb-dev-compat libpcre3-dev zlib1g-dev

# Create build directory
mkdir build && cd build

# Configure with CMake
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo \
      -DRENEWAL=ON \
      -DPACKETVER=20211103 \
      -DMAX_LEVEL=175 \
      ..

# Build (using all CPU cores)
cmake --build . --parallel $(nproc)

# Verify binaries
ls -lh map-server* char-server* login-server*
```

**Incremental Build:**
```bash
cd build

# Rebuild only changed files
cmake --build . --parallel $(nproc)

# Rebuild specific target
cmake --build . --target map-server

# Clean and rebuild
cmake --build . --target clean
cmake --build . --parallel $(nproc)
```

**Debug Build:**
```bash
# Configure for debugging
cmake -DCMAKE_BUILD_TYPE=Debug \
      -DCMAKE_C_FLAGS="-g3 -O0 -DDEBUG" \
      -DCMAKE_CXX_FLAGS="-g3 -O0 -DDEBUG" \
      ..

# Build with verbose output
cmake --build . --verbose

# Or with make
make VERBOSE=1 -j$(nproc)
```

### Windows Visual Studio Build

**Command Line (Developer Command Prompt):**
```batch
REM Open "Developer Command Prompt for VS 2019/2022"

REM Navigate to rAthena directory
cd C:\rathena

REM Build Debug configuration
MSBuild rathena.sln /p:Configuration=Debug /p:Platform=x64 /m

REM Build Release configuration
MSBuild rathena.sln /p:Configuration=Release /p:Platform=x64 /m

REM Build specific project
MSBuild map-server.vcxproj /p:Configuration=Debug /p:Platform=x64

REM Clean
MSBuild rathena.sln /t:Clean /p:Configuration=Debug /p:Platform=x64

REM Rebuild all
MSBuild rathena.sln /t:Rebuild /p:Configuration=Release /p:Platform=x64 /m
```

**IDE Build:**
1. Open `rathena.sln` in Visual Studio
2. Select configuration (Debug/Release) from toolbar
3. Select platform (x64/x86)
4. Build → Build Solution (Ctrl+Shift+B)
5. Build → Rebuild Solution (full rebuild)
6. Build → Build [specific project]

**Batch Script (build.bat):**
```batch
@echo off
setlocal

set VS_PATH="C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Current\Bin"
set SOLUTION=rathena.sln

echo Building Debug configuration...
%VS_PATH%\MSBuild.exe %SOLUTION% /p:Configuration=Debug /p:Platform=x64 /m /v:minimal
if errorlevel 1 (
    echo Debug build failed!
    exit /b 1
)

echo Building Release configuration...
%VS_PATH%\MSBuild.exe %SOLUTION% /p:Configuration=Release /p:Platform=x64 /m /v:minimal
if errorlevel 1 (
    echo Release build failed!
    exit /b 1
)

echo Build completed successfully!
```

### Build Verification

**Check Binary:**
```bash
# Verify executable
file map-server
# Output: map-server: ELF 64-bit LSB executable, x86-64, dynamically linked

# Check dependencies
ldd map-server
# Output shows linked libraries (mysql, pcre, etc.)

# Run with version flag
./map-server --version

# Check symbols (debug build)
nm map-server | grep -i "script_run"
```

**Test Run:**
```bash
# Quick syntax check
./map-server --help

# Test configuration loading
./map-server --load-plugin test
```

---

## GDB Debugging

### Setup & Basics

**Installing GDB:**
```bash
# Ubuntu/Debian
sudo apt-get install gdb

# CentOS/RHEL
sudo yum install gdb

# macOS (use LLDB instead)
# GDB available via brew but LLDB recommended
```

**Compile with Debug Symbols:**
```bash
cmake -DCMAKE_BUILD_TYPE=Debug \
      -DCMAKE_C_FLAGS="-g3 -O0" \
      -DCMAKE_CXX_FLAGS="-g3 -O0" \
      ..
cmake --build .
```

**Starting GDB:**
```bash
# Direct launch
gdb ./map-server

# Attach to running process
gdb -p $(pidof map-server)

# With arguments
gdb --args ./map-server --run-once

# With core dump
gdb ./map-server core.12345
```

### Essential GDB Commands

**Breakpoints:**
```gdb
# Set breakpoint at function
(gdb) break script_run
(gdb) b script_run

# Set breakpoint at file:line
(gdb) break script.cpp:1234
(gdb) b script.cpp:1234

# Conditional breakpoint
(gdb) break script_run if sd->status.account_id == 150000

# Breakpoint at address
(gdb) break *0x555555555234

# List breakpoints
(gdb) info breakpoints
(gdb) info b

# Enable/disable breakpoint
(gdb) disable 1
(gdb) enable 1

# Delete breakpoint
(gdb) delete 1
(gdb) clear script_run
```

**Execution Control:**
```gdb
# Run program
(gdb) run
(gdb) r

# Continue execution
(gdb) continue
(gdb) c

# Step (into functions)
(gdb) step
(gdb) s

# Next (over functions)
(gdb) next
(gdb) n

# Step instruction (assembly)
(gdb) stepi
(gdb) si

# Next instruction
(gdb) nexti
(gdb) ni

# Finish current function
(gdb) finish

# Until (run until line)
(gdb) until 1500
```

**Examining Variables:**
```gdb
# Print variable
(gdb) print sd
(gdb) p sd

# Print with type info
(gdb) ptype sd
# Output: type = struct map_session_data * {
#   ...
# }

# Print structure members
(gdb) p sd->status.name
(gdb) p sd->status.base_level

# Print array
(gdb) p sd->status.inventory[0]@10  # First 10 items

# Print in different formats
(gdb) p/x sd->status.account_id     # Hexadecimal
(gdb) p/d sd->status.account_id     # Decimal
(gdb) p/t sd->status.account_id     # Binary
(gdb) p/c variable                   # Character

# Print pointer dereferencing
(gdb) p *sd
(gdb) p sd->status

# Pretty printing
(gdb) set print pretty on
(gdb) p sd->status
```

**Watchpoints (Data Breakpoints):**
```gdb
# Watch for write
(gdb) watch sd->status.hp
# Hardware watchpoint 1: sd->status.hp

# Watch for read
(gdb) rwatch sd->status.hp

# Watch for read/write
(gdb) awatch sd->status.hp

# Conditional watchpoint
(gdb) watch sd->status.hp if sd->status.hp < 100
```

**Backtrace:**
```gdb
# Show call stack
(gdb) backtrace
(gdb) bt

# Full backtrace with locals
(gdb) bt full

# Show N frames
(gdb) bt 10

# Select frame
(gdb) frame 3
(gdb) f 3

# Move up/down frames
(gdb) up
(gdb) down

# Frame info
(gdb) info frame
(gdb) info locals
(gdb) info args
```

**Thread Debugging:**
```gdb
# List threads
(gdb) info threads

# Switch to thread
(gdb) thread 2

# Apply command to all threads
(gdb) thread apply all bt

# Break on thread
(gdb) break script.cpp:100 thread 3
```

**Memory Examination:**
```gdb
# Examine memory
(gdb) x/10x $sp           # 10 hex words at stack pointer
(gdb) x/10i $pc           # 10 instructions at program counter
(gdb) x/s 0x555556789     # String at address
(gdb) x/10wx sd           # 10 words in hex from sd

# Format: x/[count][format][size] address
# format: x(hex) d(decimal) u(unsigned) o(octal) t(binary)
#         a(address) c(char) s(string) i(instruction)
# size: b(byte) h(halfword) w(word) g(giant-8bytes)
```

### Advanced GDB Techniques

**GDB Script (.gdbinit):**
```gdb
# ~/.gdbinit or project .gdbinit
set print pretty on
set print array on
set print array-indexes on
set pagination off
set confirm off

# Custom commands
define print_player
    if $argc != 1
        help print_player
    else
        set $sd = (struct map_session_data *)$arg0
        printf "Player: %s\n", $sd->status.name
        printf "Level: %d/%d\n", $sd->status.base_level, $sd->status.job_level
        printf "HP: %d/%d\n", $sd->status.hp, $sd->status.max_hp
        printf "SP: %d/%d\n", $sd->status.sp, $sd->status.max_sp
    end
end

# Auto breakpoints
break main
break script_run
```

**Logging:**
```gdb
# Enable logging
(gdb) set logging on
(gdb) set logging file gdb.log
(gdb) set logging overwrite on

# Run commands
(gdb) bt full
(gdb) info registers

# Disable logging
(gdb) set logging off
```

**Reverse Debugging:**
```gdb
# Enable recording
(gdb) target record-full

# Reverse execution
(gdb) reverse-continue
(gdb) reverse-step
(gdb) reverse-next
(gdb) reverse-finish
```

**Core Dump Analysis:**
```bash
# Enable core dumps
ulimit -c unlimited

# Generate core dump from running process
gcore $(pidof map-server)

# Analyze core dump
gdb ./map-server core.12345

# Automatic backtrace
(gdb) bt full
(gdb) thread apply all bt full
```

---

## Visual Studio Debugging

### Basic Debugging Operations

**Starting Debug Session:**
- **F5** - Start Debugging
- **Ctrl+F5** - Start Without Debugging
- **F10** - Step Over (next line, don't enter functions)
- **F11** - Step Into (enter functions)
- **Shift+F11** - Step Out (exit current function)
- **Ctrl+Shift+F5** - Restart
- **Shift+F5** - Stop Debugging
- **Ctrl+Alt+Break** - Break All

**Breakpoints:**
- **F9** - Toggle breakpoint on current line
- **Ctrl+F9** - Enable/disable breakpoint
- **Ctrl+Shift+F9** - Delete all breakpoints

**Managing Breakpoints:**
```
Debug → Windows → Breakpoints (Ctrl+Alt+B)
```

**Breakpoint Actions:**
1. **Condition**: Break only when expression is true
   ```cpp
   sd->status.account_id == 150000
   ```

2. **Hit Count**: Break after N hits
   - Break always
   - Break when hit count equals N
   - Break when hit count is multiple of N
   - Break when hit count >= N

3. **Actions (Tracepoint)**: Print message without breaking
   ```
   Account ID: {sd->status.account_id}, Name: {sd->status.name}
   ```

4. **Filter**: Break only for specific process/thread

**Example Breakpoint Setup:**
```
Location: script.cpp, line 1523
Condition: strcmp(script->str_data[script->str_num].name, "OnPCDieEvent") == 0
Action: Script event triggered: {script->str_data[script->str_num].name}
```

### Watch Window & Data Inspection

**Watch Windows:**
- **Locals** (Alt+4): Variables in current scope
- **Autos** (Ctrl+Alt+V, A): Variables in current and previous statement
- **Watch 1-4** (Ctrl+Alt+W, 1-4): Custom watch expressions
- **Quick Watch** (Shift+F9): Evaluate expression

**Watch Expressions:**
```cpp
// Simple variable
sd->status.name

// Array range
sd->status.inventory[0], 10

// Complex expression
sd->status.hp * 100 / sd->status.max_hp

// Function call (may have side effects!)
strlen(sd->status.name)

// Type cast
(map_session_data*)bl

// Conditional
sd->status.hp > 0 ? "Alive" : "Dead"
```

**Format Specifiers:**
```cpp
sd->status.account_id, d      // Decimal
sd->status.account_id, x      // Hexadecimal
sd->status.account_id, b      // Binary
sd->status.name, s            // String
sd->status.name, s8           // UTF-8 string
sd, !                         // Type info
```

**Memory Window:**
```
Debug → Windows → Memory → Memory 1-4
```
- View raw memory at address
- Edit memory values
- Search for byte patterns

**Disassembly Window:**
```
Debug → Windows → Disassembly (Alt+8)
```
- View assembly code
- Step through assembly instructions
- Show source annotations

### Call Stack & Threads

**Call Stack Window:**
```
Debug → Windows → Call Stack (Ctrl+Alt+C)
```

**Features:**
- Double-click frame to navigate
- Right-click → "Show External Code" to see system calls
- Right-click → "Show Module Names" for DLL info
- Right-click → "Load Symbols" for missing symbols

**Threads Window:**
```
Debug → Windows → Threads (Ctrl+Alt+H)
```

**Thread Operations:**
- Double-click to switch to thread
- Right-click → Freeze to pause thread
- Right-click → Thaw to resume thread
- Flag important threads for tracking

### Advanced Visual Studio Debugging

**Data Breakpoints:**
```
Debug → New Breakpoint → Data Breakpoint
```
- Break when memory location changes
- Useful for tracking corruption
- Example: `&sd->status.hp` breaks when HP changes

**Function Breakpoints:**
```
Debug → New Breakpoint → Function Breakpoint
```
- Break on function name
- Example: `script_run`
- Supports wildcards: `script_*`

**Conditional Breakpoints for Performance:**
```cpp
// Only break for specific account
sd != nullptr && sd->status.account_id == 150000

// Only break when HP critical
sd != nullptr && sd->status.hp < (sd->status.max_hp / 10)

// Only break on error
return_value < 0
```

**Immediate Window:**
```
Debug → Windows → Immediate (Ctrl+Alt+I)
```

Execute commands during debugging:
```cpp
// Evaluate expression
? sd->status.name

// Call function
? strlen(sd->status.name)

// Modify variable
sd->status.hp = 5000

// Complex operations
? clif_displaymessage(sd->fd, "Debug message")
```

**Parallel Stacks & Tasks:**
```
Debug → Windows → Parallel Stacks
Debug → Windows → Parallel Tasks
```
- Visualize multi-threaded execution
- See all thread call stacks simultaneously
- Identify deadlocks

**Debugging Multi-Process (Multiple Servers):**
1. Debug → Attach to Process (Ctrl+Alt+P)
2. Select map-server, char-server, login-server
3. Click "Attach"
4. All servers now in same debug session

**IntelliTrace (Enterprise Edition):**
- Records execution history
- Step backwards through code
- See variable values at any point
- Save debug sessions for later analysis

---

## Memory Leak Detection

### Valgrind (Linux)

**Installation:**
```bash
# Ubuntu/Debian
sudo apt-get install valgrind

# CentOS/RHEL
sudo yum install valgrind
```

**Basic Leak Check:**
```bash
valgrind --leak-check=full \
         --show-leak-kinds=all \
         --track-origins=yes \
         --verbose \
         --log-file=valgrind.log \
         ./map-server
```

**Valgrind Options:**
```bash
--leak-check=full           # Detailed leak information
--show-leak-kinds=all       # Show all leak types
--track-origins=yes         # Track origin of uninitialized values
--verbose                   # Verbose output
--log-file=valgrind.log     # Log to file
--num-callers=30            # Stack trace depth
--suppressions=supp.txt     # Suppression file
--gen-suppressions=all      # Generate suppressions
```

**Leak Types:**
- **Definitely lost**: Memory leaked, no references
- **Indirectly lost**: Memory pointed to by leaked blocks
- **Possibly lost**: Pointers to middle of blocks
- **Still reachable**: Memory still referenced but not freed

**Example Output:**
```
==12345== HEAP SUMMARY:
==12345==     in use at exit: 1,024 bytes in 1 blocks
==12345==   total heap usage: 500 allocs, 499 frees, 102,400 bytes allocated
==12345==
==12345== 1,024 bytes in 1 blocks are definitely lost in loss record 1 of 1
==12345==    at 0x4C2FB0F: malloc (in /usr/lib/valgrind/vgpreload_memcheck-amd64-linux.so)
==12345==    by 0x123456: script_run (script.cpp:1234)
==12345==    by 0x234567: npc_scriptcont (npc.cpp:2345)
==12345==    by 0x345678: main (map.cpp:3456)
```

**Suppression File (valgrind.supp):**
```
{
   MySQL_Library_Leak
   Memcheck:Leak
   ...
   obj:*/libmysqlclient.so.*
}

{
   PCRE_JIT_Leak
   Memcheck:Leak
   ...
   fun:pcre_compile
}
```

**Usage with Suppression:**
```bash
valgrind --leak-check=full \
         --suppressions=valgrind.supp \
         ./map-server
```

### AddressSanitizer (ASan)

**Compile with ASan:**
```bash
cmake -DCMAKE_BUILD_TYPE=Debug \
      -DCMAKE_C_FLAGS="-fsanitize=address -fno-omit-frame-pointer -g" \
      -DCMAKE_CXX_FLAGS="-fsanitize=address -fno-omit-frame-pointer -g" \
      -DCMAKE_EXE_LINKER_FLAGS="-fsanitize=address" \
      ..
cmake --build .
```

**Run with ASan:**
```bash
# Direct run
./map-server

# With options
ASAN_OPTIONS=detect_leaks=1:log_path=asan.log ./map-server
```

**ASan Environment Variables:**
```bash
export ASAN_OPTIONS="\
detect_leaks=1:\
check_initialization_order=1:\
detect_stack_use_after_return=1:\
strict_init_order=1:\
log_path=asan.log:\
symbolize=1:\
halt_on_error=0"
```

**ASan Detects:**
- Heap buffer overflow
- Stack buffer overflow
- Use after free
- Use after return
- Use after scope
- Double free
- Memory leaks

**Example ASan Output:**
```
=================================================================
==12345==ERROR: AddressSanitizer: heap-use-after-free on address 0x60300000eff0
READ of size 8 at 0x60300000eff0 thread T0
    #0 0x555555558234 in script_run src/map/script.cpp:1234
    #1 0x555555559345 in npc_scriptcont src/map/npc.cpp:2345
    #2 0x55555555a456 in main src/map/map.cpp:3456

0x60300000eff0 is located 0 bytes inside of 1024-byte region [0x60300000eff0,0x60300000f3f0)
freed by thread T0 here:
    #0 0x7ffff7a12345 in free (/lib/x86_64-linux-gnu/libasan.so.5+0x12345)
    #1 0x555555557123 in script_free_code src/map/script.cpp:789

previously allocated by thread T0 here:
    #0 0x7ffff7a23456 in malloc (/lib/x86_64-linux-gnu/libasan.so.5+0x23456)
    #1 0x555555556012 in script_alloc_code src/map/script.cpp:456
```

### LeakSanitizer (LSan)

**Enable LSan (part of ASan):**
```bash
ASAN_OPTIONS=detect_leaks=1 ./map-server
```

**Standalone LSan:**
```bash
cmake -DCMAKE_C_FLAGS="-fsanitize=leak" \
      -DCMAKE_CXX_FLAGS="-fsanitize=leak" \
      ..
```

**LSan Suppressions (lsan.supp):**
```
leak:mysql_init
leak:pcre_compile
leak:ssl_init
```

**Run with Suppression:**
```bash
LSAN_OPTIONS=suppressions=lsan.supp ./map-server
```

### Visual Studio Memory Diagnostics

**Diagnostic Tools Window:**
```
Debug → Windows → Show Diagnostic Tools (Ctrl+Alt+F2)
```

**Features:**
- Memory usage graph
- CPU usage graph
- Events timeline
- Take memory snapshots

**Memory Snapshot:**
1. Start debugging (F5)
2. Click "Take Snapshot" in Diagnostic Tools
3. Perform operations
4. Take another snapshot
5. Compare snapshots to see leaks

**CRT Debug Heap:**
```cpp
// Enable CRT memory leak detection
#define _CRTDBG_MAP_ALLOC
#include <stdlib.h>
#include <crtdbg.h>

int main() {
    // Enable leak detection at exit
    _CrtSetDbgFlag(_CRTDBG_ALLOC_MEM_DF | _CRTDBG_LEAK_CHECK_DF);

    // Set breakpoint on specific allocation
    _CrtSetBreakAlloc(1234);  // Break on allocation #1234

    // Your code...

    // Dump leaks
    _CrtDumpMemoryLeaks();

    return 0;
}
```

---

## Profiling & Performance Analysis

### gprof (GNU Profiler)

**Compile with Profiling:**
```bash
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo \
      -DCMAKE_C_FLAGS="-pg" \
      -DCMAKE_CXX_FLAGS="-pg" \
      -DCMAKE_EXE_LINKER_FLAGS="-pg" \
      ..
cmake --build .
```

**Run and Generate Profile:**
```bash
# Run program (generates gmon.out)
./map-server

# Generate report
gprof ./map-server gmon.out > profile.txt

# View report
less profile.txt
```

**gprof Output Sections:**

1. **Flat Profile**:
```
  %   cumulative   self              self     total
 time   seconds   seconds    calls  ms/call  ms/call  name
 33.33      0.10     0.10    50000     0.00     0.00  battle_calc_damage
 16.67      0.15     0.05   100000     0.00     0.00  status_calc_misc
 11.11      0.18     0.03    75000     0.00     0.00  skill_castend_nodamage_id
```

2. **Call Graph**:
```
index % time    self  children    called     name
                0.10    0.05   50000/50000       battle_calc_attack [2]
[1]     50.0    0.10    0.05   50000         battle_calc_damage [1]
                0.03    0.00   50000/100000      status_calc_misc [3]
                0.02    0.00   50000/50000       battle_calc_defense [4]
```

### perf (Linux Performance Counter)

**Installation:**
```bash
# Ubuntu/Debian
sudo apt-get install linux-tools-common linux-tools-generic linux-tools-`uname -r`
```

**Basic Profiling:**
```bash
# Record performance data
sudo perf record -g ./map-server

# View report
sudo perf report

# Record with call graphs
sudo perf record -g --call-graph dwarf ./map-server

# Record specific events
sudo perf record -e cpu-clock,cache-misses ./map-server
```

**Real-time Monitoring:**
```bash
# Top-like interface
sudo perf top

# Monitor specific process
sudo perf top -p $(pidof map-server)

# Show call graphs
sudo perf top -g
```

**Advanced perf Commands:**
```bash
# CPU sampling
sudo perf stat -e cycles,instructions,cache-references,cache-misses ./map-server

# Annotate source code
sudo perf annotate

# Trace system calls
sudo perf trace -p $(pidof map-server)

# Memory access profiling
sudo perf mem record ./map-server
sudo perf mem report
```

**perf Output Example:**
```
Samples: 10K of event 'cpu-clock', Event count (approx.): 2500000000
Overhead  Command      Shared Object      Symbol
  33.45%  map-server   map-server         [.] battle_calc_damage
  18.23%  map-server   libc-2.31.so       [.] malloc
  12.67%  map-server   map-server         [.] script_run
   8.92%  map-server   map-server         [.] status_calc_misc
```

### Visual Studio Performance Profiler

**Start Profiling:**
```
Debug → Performance Profiler (Alt+F2)
```

**Profiling Tools:**
1. **CPU Usage**: Function-level CPU profiling
2. **Memory Usage**: Heap allocations and object lifetimes
3. **GPU Usage**: DirectX/graphics profiling
4. **Application Timeline**: UI responsiveness
5. **.NET Object Allocation**: .NET specific

**CPU Usage Profiling:**
1. Select "CPU Usage"
2. Click "Start"
3. Perform operations
4. Click "Stop Collection"
5. Analyze results

**Hot Path Analysis:**
- Shows most expensive call paths
- Flame graph visualization
- Filter by module, function
- Export to CSV

**Instrumentation:**
```cpp
#include <profileapi.h>

// Mark region
QueryPerformanceCounter(&start);
// ... code to profile ...
QueryPerformanceCounter(&end);

double elapsed = (double)(end.QuadPart - start.QuadPart) / frequency.QuadPart;
```

### Custom Profiling

**Simple Timer:**
```cpp
// Simple microsecond timer
class ProfileTimer {
    std::chrono::high_resolution_clock::time_point start_time;
    const char* name;
public:
    ProfileTimer(const char* n) : name(n) {
        start_time = std::chrono::high_resolution_clock::now();
    }

    ~ProfileTimer() {
        auto end_time = std::chrono::high_resolution_clock::now();
        auto duration = std::chrono::duration_cast<std::chrono::microseconds>(
            end_time - start_time
        ).count();
        ShowInfo("%s took %lld μs\n", name, duration);
    }
};

// Usage
void some_function() {
    ProfileTimer timer("some_function");
    // ... function code ...
}  // Automatically prints duration on exit
```

**Scoped Profiler with Accumulation:**
```cpp
struct ProfileStats {
    uint64 call_count;
    uint64 total_time_us;
    uint64 min_time_us;
    uint64 max_time_us;
};

std::unordered_map<std::string, ProfileStats> g_profile_stats;

class ScopedProfiler {
    std::string name;
    std::chrono::high_resolution_clock::time_point start;
public:
    ScopedProfiler(const char* n) : name(n) {
        start = std::chrono::high_resolution_clock::now();
    }

    ~ScopedProfiler() {
        auto end = std::chrono::high_resolution_clock::now();
        auto duration = std::chrono::duration_cast<std::chrono::microseconds>(
            end - start
        ).count();

        auto& stats = g_profile_stats[name];
        stats.call_count++;
        stats.total_time_us += duration;
        stats.min_time_us = (stats.call_count == 1) ? duration :
                             std::min(stats.min_time_us, (uint64)duration);
        stats.max_time_us = std::max(stats.max_time_us, (uint64)duration);
    }
};

// Print stats
void print_profile_stats() {
    ShowInfo("=== Profile Stats ===\n");
    for (const auto& [name, stats] : g_profile_stats) {
        ShowInfo("%s: calls=%llu avg=%llu min=%llu max=%llu total=%llu\n",
                 name.c_str(), stats.call_count,
                 stats.total_time_us / stats.call_count,
                 stats.min_time_us, stats.max_time_us, stats.total_time_us);
    }
}
```

---

## Common Errors & Fixes

### MySQL Not Found

**Error:**
```
CMake Error: Could not find MySQL
-- Could NOT find MySQL (missing: MYSQL_LIBRARY MYSQL_INCLUDE_DIR)
```

**Fix 1: Specify MySQL Path**
```bash
cmake -DMYSQL_INCLUDE_DIR=/usr/include/mysql \
      -DMYSQL_LIBRARY=/usr/lib/x86_64-linux-gnu/libmysqlclient.so \
      ..
```

**Fix 2: Install Development Package**
```bash
# Ubuntu/Debian
sudo apt-get install libmariadb-dev libmariadb-dev-compat

# CentOS/RHEL
sudo yum install mysql-devel

# Find MySQL manually
sudo find / -name "mysql.h" 2>/dev/null
sudo find / -name "libmysqlclient.so" 2>/dev/null
```

**Fix 3: Use pkg-config**
```bash
pkg-config --cflags --libs mysqlclient
# Use output in cmake command
```

### PCRE Missing

**Error:**
```
fatal error: pcre.h: No such file or directory
 #include <pcre.h>
```

**Fix 1: Install PCRE**
```bash
# Ubuntu/Debian
sudo apt-get install libpcre3-dev

# CentOS/RHEL
sudo yum install pcre-devel
```

**Fix 2: Disable PCRE**
```bash
cmake -DWITH_PCRE=OFF ..
```

**Fix 3: Specify PCRE Path**
```bash
cmake -DPCRE_INCLUDE_DIR=/usr/include \
      -DPCRE_LIBRARY=/usr/lib/libpcre.so \
      ..
```

### Linker Errors

**Error: Undefined Reference**
```
undefined reference to `mysql_init'
undefined reference to `pcre_compile'
```

**Fix: Check Link Order**
```cmake
# Ensure libraries linked correctly
target_link_libraries(map-server
    common
    ${MYSQL_LIBRARY}
    ${PCRE_LIBRARY}
    ${ZLIB_LIBRARY}
)
```

**Error: Multiple Definitions**
```
multiple definition of `status_calc_pc'
```

**Fix: Check Header Guards**
```cpp
// status.hpp
#ifndef STATUS_HPP
#define STATUS_HPP

// Declarations only (extern)
extern void status_calc_pc(struct map_session_data* sd);

#endif // STATUS_HPP
```

**Error: Cannot Find -lmysqlclient**
```
/usr/bin/ld: cannot find -lmysqlclient
```

**Fix:**
```bash
# Find library
sudo find / -name "libmysqlclient*" 2>/dev/null

# Create symlink if needed
sudo ln -s /usr/lib/x86_64-linux-gnu/libmariadb.so /usr/lib/x86_64-linux-gnu/libmysqlclient.so

# Or specify exact library
cmake -DMYSQL_LIBRARY=/usr/lib/x86_64-linux-gnu/libmariadb.so ..
```

### Runtime Errors

**Error: Segmentation Fault on Startup**
```
Segmentation fault (core dumped)
```

**Debug Steps:**
```bash
# Run with gdb
gdb ./map-server
(gdb) run
# When it crashes:
(gdb) bt full

# Check dependencies
ldd ./map-server
# Look for "not found"

# Run with valgrind
valgrind ./map-server
```

**Error: MySQL Connection Failed**
```
[Error]: Can't connect to MySQL server
```

**Fix:**
```bash
# Check MySQL running
sudo systemctl status mysql

# Test connection manually
mysql -h 127.0.0.1 -u ragnarok -p

# Check conf/import/inter_conf.txt
sql.db_hostname: 127.0.0.1
sql.db_port: 3306
sql.db_username: ragnarok
sql.db_password: password
sql.db_database: ragnarok

# Check firewall
sudo ufw allow 3306/tcp
```

**Error: Packet Version Mismatch**
```
[Warning]: Invalid packet version
[Warning]: Client disconnected
```

**Fix:**
```bash
# Verify PACKETVER matches client
grep "PACKETVER" src/config/core.hpp

# Rebuild with correct version
cmake -DPACKETVER=20211103 ..
cmake --build .
```

---

## Continuous Integration Setup

### GitHub Actions

**.github/workflows/build.yml:**
```yaml
name: Build rAthena

on:
  push:
    branches: [ master, develop ]
  pull_request:
    branches: [ master ]

jobs:
  build-linux:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        compiler: [gcc, clang]
        mode: [pre-renewal, renewal]

    steps:
    - uses: actions/checkout@v3

    - name: Install Dependencies
      run: |
        sudo apt-get update
        sudo apt-get install -y \
          cmake \
          ${{ matrix.compiler }} \
          libmariadb-dev \
          libmariadb-dev-compat \
          libpcre3-dev \
          zlib1g-dev

    - name: Configure
      run: |
        mkdir build && cd build
        cmake \
          -DCMAKE_BUILD_TYPE=RelWithDebInfo \
          -DCMAKE_C_COMPILER=${{ matrix.compiler == 'gcc' && 'gcc' || 'clang' }} \
          -DCMAKE_CXX_COMPILER=${{ matrix.compiler == 'gcc' && 'g++' || 'clang++' }} \
          -DRENEWAL=${{ matrix.mode == 'renewal' && 'ON' || 'OFF' }} \
          ..

    - name: Build
      run: |
        cd build
        cmake --build . --parallel $(nproc)

    - name: Test
      run: |
        cd build
        ctest --output-on-failure

    - name: Upload Artifacts
      uses: actions/upload-artifact@v3
      with:
        name: rathena-${{ matrix.compiler }}-${{ matrix.mode }}
        path: |
          build/map-server*
          build/char-server*
          build/login-server*

  build-windows:
    runs-on: windows-latest

    steps:
    - uses: actions/checkout@v3

    - name: Setup MSBuild
      uses: microsoft/setup-msbuild@v1

    - name: Build
      run: |
        MSBuild rathena.sln /p:Configuration=Release /p:Platform=x64 /m

    - name: Upload Artifacts
      uses: actions/upload-artifact@v3
      with:
        name: rathena-windows-x64
        path: |
          Release/*.exe
```

### Travis CI

**.travis.yml:**
```yaml
language: cpp

os:
  - linux
  - osx

compiler:
  - gcc
  - clang

env:
  - MODE=renewal PACKETVER=20211103
  - MODE=pre-renewal PACKETVER=20151104

addons:
  apt:
    packages:
      - cmake
      - libmariadb-dev
      - libmariadb-dev-compat
      - libpcre3-dev
      - zlib1g-dev

before_script:
  - mkdir build && cd build
  - cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo -DRENEWAL=${MODE == 'renewal'} -DPACKETVER=${PACKETVER} ..

script:
  - cmake --build . --parallel $(nproc)
  - ctest --output-on-failure

notifications:
  email:
    on_success: change
    on_failure: always
```

### Docker Build

**Dockerfile:**
```dockerfile
FROM ubuntu:22.04

# Install dependencies
RUN apt-get update && apt-get install -y \
    git \
    cmake \
    gcc \
    g++ \
    libmariadb-dev \
    libmariadb-dev-compat \
    libpcre3-dev \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /rathena

# Copy source
COPY . .

# Build
RUN mkdir build && cd build && \
    cmake -DCMAKE_BUILD_TYPE=Release -DRENEWAL=ON .. && \
    cmake --build . --parallel $(nproc)

# Runtime stage
FROM ubuntu:22.04

RUN apt-get update && apt-get install -y \
    libmariadb3 \
    libpcre3 \
    zlib1g \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /rathena

# Copy built binaries
COPY --from=0 /rathena/build/map-server* ./
COPY --from=0 /rathena/build/char-server* ./
COPY --from=0 /rathena/build/login-server* ./
COPY conf ./conf/
COPY db ./db/
COPY npc ./npc/

EXPOSE 6121 6900 5121

CMD ["./map-server"]
```

**docker-compose.yml:**
```yaml
version: '3.8'

services:
  mysql:
    image: mariadb:10.6
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: ragnarok
      MYSQL_USER: ragnarok
      MYSQL_PASSWORD: ragnarok
    volumes:
      - ./sql-files:/docker-entrypoint-initdb.d
      - mysql_data:/var/lib/mysql
    ports:
      - "3306:3306"

  login-server:
    build: .
    command: ./login-server
    depends_on:
      - mysql
    ports:
      - "6900:6900"
    volumes:
      - ./conf:/rathena/conf

  char-server:
    build: .
    command: ./char-server
    depends_on:
      - mysql
      - login-server
    ports:
      - "6121:6121"
    volumes:
      - ./conf:/rathena/conf

  map-server:
    build: .
    command: ./map-server
    depends_on:
      - mysql
      - char-server
    ports:
      - "5121:5121"
    volumes:
      - ./conf:/rathena/conf
      - ./db:/rathena/db
      - ./npc:/rathena/npc

volumes:
  mysql_data:
```

---

## Optimization Flags

### GCC/Clang Optimization Levels

**-O0 (No Optimization)**
```bash
# For debugging only
cmake -DCMAKE_BUILD_TYPE=Debug \
      -DCMAKE_C_FLAGS="-O0 -g3" \
      -DCMAKE_CXX_FLAGS="-O0 -g3" \
      ..
```
- No optimizations
- Fastest compile time
- Largest binary size
- Slowest execution
- Best for debugging (variables not optimized away)

**-O1 (Basic Optimization)**
```bash
cmake -DCMAKE_C_FLAGS="-O1" \
      -DCMAKE_CXX_FLAGS="-O1" \
      ..
```
- Basic optimizations
- Reasonable compile time
- Better performance than -O0
- Variables may be optimized away

**-O2 (Recommended for Release)**
```bash
cmake -DCMAKE_BUILD_TYPE=Release \
      -DCMAKE_C_FLAGS="-O2" \
      -DCMAKE_CXX_FLAGS="-O2" \
      ..
```
- Most optimizations enabled
- Good balance of speed and size
- **Default for Release builds**
- May inline functions
- Loop optimizations
- Dead code elimination

**-O3 (Maximum Optimization)**
```bash
cmake -DCMAKE_C_FLAGS="-O3" \
      -DCMAKE_CXX_FLAGS="-O3" \
      ..
```
- All -O2 optimizations plus:
- Aggressive inlining
- Vectorization
- Loop unrolling
- May increase binary size
- Longer compile time
- May not always be faster than -O2

**-Os (Optimize for Size)**
```bash
cmake -DCMAKE_BUILD_TYPE=MinSizeRel \
      -DCMAKE_C_FLAGS="-Os" \
      -DCMAKE_CXX_FLAGS="-Os" \
      ..
```
- -O2 optimizations but favoring size
- Smaller binaries
- Good for embedded systems
- May reduce cache misses

**-Ofast (Fastest, Non-Standard)**
```bash
cmake -DCMAKE_C_FLAGS="-Ofast" \
      -DCMAKE_CXX_FLAGS="-Ofast" \
      ..
```
- -O3 plus non-standard optimizations
- Breaks strict standards compliance
- -ffast-math included (may affect precision)
- Use with caution

### Debug Symbols

**-g (Basic Debug Info)**
```bash
cmake -DCMAKE_C_FLAGS="-g" \
      -DCMAKE_CXX_FLAGS="-g" \
      ..
```
- Minimal debug information
- Line numbers, function names

**-g3 (Maximum Debug Info)**
```bash
cmake -DCMAKE_C_FLAGS="-g3" \
      -DCMAKE_CXX_FLAGS="-g3" \
      ..
```
- Includes macro definitions
- More detailed debug info
- Larger binary size

**-ggdb (GDB-Specific)**
```bash
cmake -DCMAKE_C_FLAGS="-ggdb3" \
      -DCMAKE_CXX_FLAGS="-ggdb3" \
      ..
```
- GDB-optimized debug info
- Most detailed for GDB

**RelWithDebInfo (Optimized + Debug)**
```bash
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo ..
```
- Equivalent to: -O2 -g -DNDEBUG
- **Recommended for production debugging**
- Good performance with stack traces

### Architecture-Specific Optimizations

**-march=native (CPU-Specific)**
```bash
cmake -DCMAKE_C_FLAGS="-O3 -march=native" \
      -DCMAKE_CXX_FLAGS="-O3 -march=native" \
      ..
```
- Optimizes for build machine's CPU
- May not work on different CPUs
- Enables AVX, SSE, etc. if available

**-mtune=native**
```bash
cmake -DCMAKE_C_FLAGS="-O3 -mtune=native" \
      -DCMAKE_CXX_FLAGS="-O3 -mtune=native" \
      ..
```
- Tunes for CPU but maintains compatibility
- Safer than -march=native

### Link-Time Optimization (LTO)

**Enable LTO:**
```bash
cmake -DCMAKE_BUILD_TYPE=Release \
      -DCMAKE_C_FLAGS="-O3 -flto" \
      -DCMAKE_CXX_FLAGS="-O3 -flto" \
      -DCMAKE_EXE_LINKER_FLAGS="-flto" \
      ..
```
- Optimizes across translation units
- Significantly improved performance (10-20%)
- Much longer compile/link time
- Requires AR/RANLIB with LTO support

**CMake LTO Support:**
```cmake
set(CMAKE_INTERPROCEDURAL_OPTIMIZATION TRUE)
```

### Recommended Configurations

**Development (Debug):**
```bash
cmake -DCMAKE_BUILD_TYPE=Debug \
      -DCMAKE_C_FLAGS="-O0 -g3 -Wall -Wextra" \
      -DCMAKE_CXX_FLAGS="-O0 -g3 -Wall -Wextra" \
      ..
```

**Testing (With Debug Info):**
```bash
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo \
      -DCMAKE_C_FLAGS="-O2 -g" \
      -DCMAKE_CXX_FLAGS="-O2 -g" \
      ..
```

**Production (Maximum Performance):**
```bash
cmake -DCMAKE_BUILD_TYPE=Release \
      -DCMAKE_C_FLAGS="-O3 -march=native -flto" \
      -DCMAKE_CXX_FLAGS="-O3 -march=native -flto" \
      -DCMAKE_EXE_LINKER_FLAGS="-flto" \
      -DCMAKE_INTERPROCEDURAL_OPTIMIZATION=TRUE \
      ..
```

**Production (Portable):**
```bash
cmake -DCMAKE_BUILD_TYPE=Release \
      -DCMAKE_C_FLAGS="-O2" \
      -DCMAKE_CXX_FLAGS="-O2" \
      ..
```

---

## Real Debugging Scenarios

### Scenario 1: Server Crash on Player Login

**Symptoms:**
- Map server crashes when specific player logs in
- Other players can log in normally
- No error message, just segfault

**Investigation:**
```bash
# Step 1: Get core dump
ulimit -c unlimited
./map-server
# ... crash occurs ...

# Step 2: Analyze with GDB
gdb ./map-server core.12345

(gdb) bt full
#0  0x0000555555567890 in pc_authok (sd=0x7ffff0001234, ...) at pc.cpp:1234
#1  0x0000555555568901 in chrif_authok (fd=5) at chrif.cpp:567
...

(gdb) frame 0
(gdb) print sd
$1 = (struct map_session_data *) 0x7ffff0001234

(gdb) print *sd
$2 = {
  bl = {...},
  status = {
    account_id = 150000,
    char_id = 200000,
    name = "Player\000\000...",
    inventory = 0x0  # <-- NULL pointer!
  }
}

# Step 3: Find why inventory is NULL
(gdb) break pc.cpp:1200
(gdb) run
# When breakpoint hits:
(gdb) print sd->status.inventory
$3 = (struct item *) 0x0

# Step 4: Backtrace to see where it should be allocated
(gdb) bt
# Shows inventory allocation was skipped due to database error
```

**Root Cause:**
- Database query for inventory failed
- Code didn't check for NULL before dereferencing

**Fix:**
```cpp
// pc.cpp
int pc_authok(struct map_session_data *sd, ...) {
    // Load inventory
    if (!pc_load_inventory(sd)) {
        ShowError("pc_authok: Failed to load inventory for AID:%d\n", sd->status.account_id);
        clif_authfail_fd(sd->fd, 0);
        return 0;
    }

    // Add NULL check before use
    if (sd->status.inventory == NULL) {
        ShowError("pc_authok: Inventory is NULL for AID:%d\n", sd->status.account_id);
        return 0;
    }

    // ... rest of function ...
}
```

### Scenario 2: Memory Leak in Script Engine

**Symptoms:**
- Memory usage grows over time
- Server becomes slower after running for days
- Eventually crashes with out-of-memory

**Investigation with Valgrind:**
```bash
# Run with leak detection
valgrind --leak-check=full \
         --show-leak-kinds=all \
         --track-origins=yes \
         --log-file=valgrind.log \
         ./map-server

# After running for a while (or trigger with @reloadscript)
# Check valgrind.log

==12345== 10,485,760 bytes in 10,240 blocks are definitely lost
==12345==    at 0x4C2FB0F: malloc
==12345==    by 0x555555560123: script_alloc_state (script.cpp:2345)
==12345==    by 0x555555561234: run_script (script.cpp:3456)
==12345==    by 0x555555562345: npc_event (npc.cpp:4567)
```

**Investigation with GDB:**
```gdb
# Set breakpoint on allocation
(gdb) break script_alloc_state

# Run and trigger leak (e.g., @reloadscript)
(gdb) run

# Breakpoint hit, get address
(gdb) print $rax
$1 = 0x7ffff0123456

# Set watchpoint on this memory
(gdb) watch *(void**)0x7ffff0123456

# Continue - see if it's ever freed
(gdb) continue
# ... runs indefinitely, never freed!
```

**Finding the Leak:**
```gdb
# Search for where script states are stored
(gdb) grep -r "script_state" src/map/

# Found: Script states added to list but never removed on certain error paths
```

**Root Cause:**
```cpp
// script.cpp - Original code
struct script_state* run_script(const char* script, ...) {
    struct script_state* st = script_alloc_state();

    if (!script || !script[0]) {
        // ERROR: Early return without freeing st!
        return NULL;
    }

    // ... normal execution ...
    return st;
}
```

**Fix:**
```cpp
// script.cpp - Fixed code
struct script_state* run_script(const char* script, ...) {
    if (!script || !script[0]) {
        return NULL;  // Check BEFORE allocation
    }

    struct script_state* st = script_alloc_state();

    // ... normal execution ...
    return st;
}

// Also add cleanup in error paths
struct script_state* run_script(const char* script, ...) {
    struct script_state* st = script_alloc_state();

    if (some_error) {
        script_free_state(st);  // Clean up on error
        return NULL;
    }

    // ... normal execution ...
    return st;
}
```

### Scenario 3: Performance Problem - Slow Skill Casting

**Symptoms:**
- Players report laggy skill casting
- Skills sometimes take seconds to execute
- CPU usage spikes during mass skill usage

**Investigation with perf:**
```bash
# Record performance data during lag
sudo perf record -g -p $(pidof map-server)
# ... let it record during lag event ...
# Ctrl+C to stop

# Analyze
sudo perf report

# Output shows:
Overhead  Symbol
  45.67%  status_calc_pc
  23.45%  battle_calc_damage
  15.23%  map_foreachinrange
```

**Deep Dive with perf:**
```bash
# Annotate hot function
sudo perf annotate status_calc_pc

# Shows most time spent in:
  15.67%  for (i = 0; i < MAX_INVENTORY; i++) {
  12.34%      if (sd->status.inventory[i].card[0] == CARD0_CREATE) {
   8.90%          // Card bonus calculation
```

**Investigation with GDB:**
```gdb
# Break at slow function
(gdb) break status_calc_pc

# Run until break
(gdb) run

# Count loop iterations
(gdb) set pagination off
(gdb) set $count = 0
(gdb) break script.cpp:1234 if (++$count >= 100)
(gdb) commands
    silent
    printf "Iterations: %d\n", $count
    continue
end
(gdb) continue
```

**Profile with Custom Timer:**
```cpp
// Add to status.cpp
void status_calc_pc(struct map_session_data* sd, bool first) {
    auto start = std::chrono::high_resolution_clock::now();

    // ... existing code ...

    auto end = std::chrono::high_resolution_clock::now();
    auto duration = std::chrono::duration_cast<std::chrono::microseconds>(end - start).count();

    if (duration > 1000) {  // Log if > 1ms
        ShowWarning("status_calc_pc took %lld μs for AID:%d\n", duration, sd->status.account_id);
    }
}
```

**Root Cause:**
- `status_calc_pc` called every time any stat changes
- Recalculates ALL equipment bonuses every time
- Called hundreds of times during skill casting

**Fix - Add Caching:**
```cpp
// status.hpp
struct map_session_data {
    // ...
    struct {
        uint32 calc_flag;  // Dirty flags for what needs recalc
        tick_t last_calc;  // Last calculation time
    } status_cache;
};

// status.cpp
void status_calc_pc(struct map_session_data* sd, enum e_status_calc_flag flag) {
    // Check if recently calculated
    if (gettick() - sd->status_cache.last_calc < 100 &&
        !(sd->status_cache.calc_flag & flag)) {
        return;  // Use cached values
    }

    // Only recalculate what changed
    if (flag & SCF_EQUIP) {
        status_calc_pc_equipment(sd);
    }
    if (flag & SCF_BASE) {
        status_calc_pc_base(sd);
    }

    sd->status_cache.last_calc = gettick();
    sd->status_cache.calc_flag = 0;
}
```

**Result:**
- 90% reduction in `status_calc_pc` calls
- Skill casting lag eliminated
- CPU usage during mass skills reduced by 60%

### Scenario 4: Data Corruption - Items Duplicating

**Symptoms:**
- Players report items duplicating randomly
- Database shows duplicate inventory entries
- No obvious pattern

**Investigation:**
```bash
# Enable MySQL query logging
# In MySQL:
SET GLOBAL general_log = 'ON';
SET GLOBAL log_output = 'TABLE';

# Watch queries in real-time
mysql> SELECT * FROM mysql.general_log
       WHERE command_type = 'Query'
       AND argument LIKE '%inventory%'
       ORDER BY event_time DESC
       LIMIT 50;
```

**Add Debug Logging:**
```cpp
// pc.cpp - Add extensive logging
int pc_additem(struct map_session_data *sd, struct item *item_data, int amount, e_log_pick_type log_type) {
    ShowDebug("pc_additem: AID:%d adding item %d (amount:%d)\n",
              sd->status.account_id, item_data->nameid, amount);

    // ... existing code ...

    // Log inventory state
    for (int i = 0; i < MAX_INVENTORY; i++) {
        if (sd->status.inventory[i].nameid == item_data->nameid) {
            ShowDebug("  Slot %d: ID:%d Amount:%d\n",
                      i, sd->status.inventory[i].nameid, sd->status.inventory[i].amount);
        }
    }

    return 0;
}
```

**Found Race Condition:**
```cpp
// Original code - NOT thread-safe
int pc_additem(...) {
    // Find existing stack
    for (i = 0; i < MAX_INVENTORY; i++) {
        if (sd->status.inventory[i].nameid == item_data->nameid) {
            // Add to existing stack
            sd->status.inventory[i].amount += amount;
            intif_saveitem(&sd->status.inventory[i]);  // <-- ASYNC!
            return 0;
        }
    }

    // Add new item
    for (i = 0; i < MAX_INVENTORY; i++) {
        if (sd->status.inventory[i].nameid == 0) {
            memcpy(&sd->status.inventory[i], item_data, sizeof(struct item));
            sd->status.inventory[i].amount = amount;
            intif_saveitem(&sd->status.inventory[i]);  // <-- ASYNC!
            return 0;
        }
    }
}
```

**Problem:**
- Two calls to `pc_additem` in quick succession
- First call finds empty slot, starts async save
- Second call runs before first save completes
- Second call finds SAME empty slot (not yet marked as used)
- Both save to database with same slot number
- Result: Duplication

**Fix - Add Locking:**
```cpp
// pc.hpp
struct map_session_data {
    // ...
    std::mutex inventory_mutex;
    std::atomic<bool> inventory_saving;
};

// pc.cpp - Fixed code
int pc_additem(struct map_session_data *sd, struct item *item_data, int amount, e_log_pick_type log_type) {
    std::lock_guard<std::mutex> lock(sd->inventory_mutex);

    // Wait for any pending saves
    while (sd->inventory_saving.load()) {
        std::this_thread::sleep_for(std::chrono::milliseconds(1));
    }

    // Find existing stack
    for (i = 0; i < MAX_INVENTORY; i++) {
        if (sd->status.inventory[i].nameid == item_data->nameid) {
            sd->status.inventory[i].amount += amount;
            sd->inventory_saving.store(true);
            intif_saveitem(&sd->status.inventory[i], [sd]() {
                sd->inventory_saving.store(false);
            });
            return 0;
        }
    }

    // Add new item...
}
```

---

**Document Size: ~18KB**

This reference covers all essential compilation and debugging workflows for rAthena development, from basic builds to advanced debugging scenarios with real-world examples.
