---
kb_id: KB_REF_022
title: "rAthena Source Code Structure & Architecture"
category: Source Code
keywords: [source_code, cpp, directory_structure, architecture, pc.cpp, mob.cpp, skill.cpp, battle.cpp, itemdb.cpp, clif.cpp, map_session_data, cmake, compilation]
related_files: [
  "src/map/",
  "src/char/",
  "src/login/",
  "src/common/",
  "CMakeLists.txt"
]
difficulty: expert
use_case: "Understanding rAthena C++ codebase structure for source modifications, knowing where to make changes, key files and classes"
version: rAthena 2024
last_updated: 2024-01-15
---

# rAthena Source Code Structure & Architecture

## Table of Contents
1. [Directory Structure](#directory-structure)
2. [Key Source Files](#key-source-files)
3. [Core Data Structures](#core-data-structures)
4. [Server Architecture](#server-architecture)
5. [Build System](#build-system)
6. [Header Files Reference](#header-files-reference)
7. [Common Patterns](#common-patterns)
8. [Modification Guide](#modification-guide)

---

## Directory Structure

### **Root Layout**
```
rathena/
├── src/              # C++ source code
│   ├── char/         # Character server
│   ├── common/       # Shared code (all servers)
│   ├── config/       # Configuration headers
│   ├── custom/       # Custom modifications (safe to edit)
│   ├── login/        # Login server
│   ├── map/          # Map server (90% of modifications here)
│   ├── tool/         # Utility tools
│   └── web/          # Web server
├── db/               # Databases (YAML/TXT)
├── doc/              # Documentation
├── npc/              # NPC scripts
├── conf/             # Server configuration
├── 3rdparty/         # Third-party libraries
├── CMakeLists.txt    # CMake build configuration
└── vcproj-*/         # Visual Studio projects
```

---

## Key Source Files

### **src/map/ (Map Server - Primary Development)**

#### **Character/Player Related**

**pc.cpp / pc.hpp** (~15,000 lines)
```cpp
PURPOSE: Player character functions
KEY FUNCTIONS:
- pc_setpos() - Move player
- pc_calcstatus() - Recalculate player stats
- pc_bonus() - Apply item bonuses
- pc_damage() - Player takes damage
- pc_heal() - Heal player
- pc_checkskill() - Check skill level
- pc_jobchange() - Change job
- pc_levelup() - Level up player
- pc_makesavestatus() - Save player data

KEY STRUCTS:
- map_session_data - Player data structure
- s_autospell - Auto-spell data
- s_addeffect - Additional effects

COMMON MODIFICATIONS:
- Custom stats/formulas
- Custom job mechanics
- Stat calculation changes
- Bonus application
```

**clif.cpp / clif.hpp** (~18,000 lines)
```cpp
PURPOSE: Client-server communication (packets)
KEY FUNCTIONS:
- clif->send() - Send packet to client
- clif->parse*() - Parse client packets
- clif->displaymessage() - Chat message
- clif->showscript() - Script message box
- clif->skill_*() - Skill-related packets
- clif->item_*() - Item-related packets

PACKET MACROS:
- WFIFOHEAD(fd, size) - Prepare write buffer
- WFIFOB(fd, pos) - Write byte
- WFIFOW(fd, pos) - Write word (16-bit)
- WFIFOL(fd, pos) - Write long (32-bit)
- WFIFOSET(fd, size) - Send buffer
- RFIFOB(fd, pos) - Read byte
- RFIFOW(fd, pos) - Read word
- RFIFOL(fd, pos) - Read long

COMMON MODIFICATIONS:
- Custom packets
- UI modifications
- Custom displays
```

#### **Combat Related**

**battle.cpp / battle.hpp** (~8,000 lines)
```cpp
PURPOSE: Combat calculations and damage formulas
KEY FUNCTIONS:
- battle_calc_damage() - Calculate final damage
- battle_calc_attack() - Calculate attack
- battle_calc_weapon_attack() - Weapon damage
- battle_calc_magic_attack() - Magic damage
- battle_attr_fix() - Element modifier
- battle_calc_cardfix() - Card bonus calculation
- battle_calc_skillratio() - Skill damage ratio

KEY STRUCTS:
- Damage - Damage calculation result
- battle_config - Battle configuration

COMMON MODIFICATIONS:
- Damage formulas
- Critical damage
- Element tables
- Defense formulas
- Race/size/element modifiers
```

**skill.cpp / skill.hpp** (~12,000 lines)
```cpp
PURPOSE: Skill mechanics and effects
KEY FUNCTIONS:
- skill_castend_*() - Skill cast end
- skill_check_condition() - Check if can cast
- skill_consume_requirement() - Use SP/items
- skill_get_*() - Get skill data
- skill_attack() - Skill damage
- skill_area_*() - AoE skills

KEY DATA:
- skill_db - Skill database array
- skill_tree - Skill trees per job

COMMON MODIFICATIONS:
- Custom skills
- Skill damage
- Skill effects
- Cast conditions
```

**status.cpp / status.hpp** (~10,000 lines)
```cpp
PURPOSE: Status effects and stat calculations
KEY FUNCTIONS:
- status_change_start() - Apply status effect
- status_change_end() - Remove status effect
- status_calc_*() - Calculate stats
- status_heal() - HP/SP recovery
- status_percent_damage() - % damage
- status_fix_damage() - Modify damage

KEY STRUCTS:
- status_data - Entity status
- status_change - Active status effects
- s_status_change_entry - Single SC entry

COMMON MODIFICATIONS:
- Custom status effects
- Stat formulas
- Status effect mechanics
```

#### **Monster Related**

**mob.cpp / mob.hpp** (~8,000 lines)
```cpp
PURPOSE: Monster AI and behavior
KEY FUNCTIONS:
- mob_spawn_*() - Spawn monsters
- mob_ai_*() - AI routines
- mob_damage() - Monster takes damage
- mob_heal() - Heal monster
- mob_dead() - Monster death
- mob_unlocktarget() - Clear target
- mob_randomwalk() - Random movement

KEY STRUCTS:
- mob_data - Monster instance data
- mob_db_data - Monster database entry

COMMON MODIFICATIONS:
- Custom AI
- Monster behavior
- Spawn mechanics
- Drop rates
```

#### **Database Related**

**itemdb.cpp / itemdb.hpp** (~5,000 lines)
```cpp
PURPOSE: Item database management
KEY FUNCTIONS:
- itemdb_exists() - Check if item exists
- itemdb_search() - Get item data
- itemdb_type() - Get item type
- itemdb_reload() - Reload database
- itemdb_searchname() - Search by name

KEY STRUCTS:
- item_data - Item database entry
- s_item_delay - Item use delay

COMMON MODIFICATIONS:
- Custom item fields
- Item loading
- Item bonuses
```

**script.cpp / script.hpp** (~20,000 lines - LARGEST FILE)
```cpp
PURPOSE: Script engine and commands
KEY FUNCTIONS:
- BUILDIN(command_name) - Define script command
- script_getnum() - Get integer parameter
- script_getstr() - Get string parameter
- script_pushint() - Return integer
- script_pushstr() - Return string
- run_script() - Execute script

KEY MACROS:
- BUILDIN(func) - Script command definition
- script_getdata() - Get parameter
- script_hasdata() - Check parameter exists

COMMON MODIFICATIONS:
- Custom script commands
- Script engine features
```

#### **Map Related**

**map.cpp / map.hpp** (~6,000 lines)
```cpp
PURPOSE: Map management and pathfinding
KEY FUNCTIONS:
- map_foreachinarea() - Iterate area
- map_foreachinrange() - Iterate range
- map_getcell() - Get cell type
- map_setcell() - Set cell type
- path_search() - Pathfinding

COMMON MODIFICATIONS:
- Custom map properties
- Cell types
- Area effects
```

**atcommand.cpp / atcommand.hpp** (~9,000 lines)
```cpp
PURPOSE: GM commands
KEY FUNCTIONS:
- ACMD(command_name) - Define command
- atcommand_config_read() - Load config
- is_atcommand() - Check if @ command

KEY MACROS:
- ACMD(func) - AT command definition

COMMON MODIFICATIONS:
- Custom GM commands
```

**guild.cpp / guild.hpp**, **party.cpp / party.hpp**, **pet.cpp / pet.hpp**
```cpp
PURPOSE: Social systems
COMMON MODIFICATIONS:
- Guild mechanics
- Party bonuses
- Pet evolution
```

---

### **src/char/ (Character Server)**

**char.cpp / char.hpp** (~8,000 lines)
```cpp
PURPOSE: Character data management
KEY FUNCTIONS:
- char_mmo_char_tosql() - Save character
- char_mmo_char_fromsql() - Load character
- char_delete() - Delete character
- char_creation_*() - Character creation
```

**int_storage.cpp**, **int_guild.cpp**, **int_party.cpp**
```cpp
PURPOSE: Inter-server communication
```

---

### **src/login/ (Login Server)**

**login.cpp / login.hpp** (~4,000 lines)
```cpp
PURPOSE: Account authentication
KEY FUNCTIONS:
- login_auth() - Authenticate account
- login_fromchar_parse_auth() - Char server auth
```

---

### **src/common/ (Shared Code)**

**socket.cpp / socket.hpp**
```cpp
PURPOSE: Network socket handling
KEY FUNCTIONS:
- make_listen_bind() - Create server socket
- connect_client() - Connect to server
- do_sendrecv() - Send/receive data
```

**core.cpp / core.hpp**
```cpp
PURPOSE: Core server functions
KEY FUNCTIONS:
- sig_proc() - Signal handling
- usercheck() - Check running user
```

**malloc.cpp / malloc.hpp**
```cpp
PURPOSE: Memory management
KEY FUNCTIONS:
- aCalloc() - Allocate zeroed memory
- aRealloc() - Reallocate memory
- aFree() - Free memory
```

**showmsg.cpp / showmsg.hpp**
```cpp
PURPOSE: Console output and logging
KEY FUNCTIONS:
- ShowInfo() - Info message
- ShowWarning() - Warning message
- ShowError() - Error message
- ShowDebug() - Debug message
- ShowSQL() - SQL query logging
```

**timer.cpp / timer.hpp**
```cpp
PURPOSE: Timer system
KEY FUNCTIONS:
- add_timer() - Add timer
- add_timer_interval() - Repeating timer
- delete_timer() - Remove timer
```

**db.cpp / db.hpp**
```cpp
PURPOSE: Database abstraction layer
KEY TYPES:
- DBMap - Key-value database
- DBIterator - Iterator
```

**utils.cpp / utils.hpp**
```cpp
PURPOSE: Utility functions
KEY FUNCTIONS:
- cap_value() - Clamp value
- rnd() - Random number
```

---

## Core Data Structures

### **map_session_data** (Player Data)
```cpp
// Location: src/map/pc.hpp
struct map_session_data {
    struct block_list bl;           // Block list (position, id)
    struct unit_data ud;            // Unit data (movement, target)
    struct view_data vd;            // View data (appearance)
    struct status_data base_status; // Base stats
    struct status_data battle_status; // Battle stats (with bonuses)
    struct status_change sc;        // Active status changes

    // Basic info
    int char_id;                    // Character ID
    int account_id;                 // Account ID
    int class_;                     // Job class
    unsigned int status_point;      // Stat points
    unsigned int skill_point;       // Skill points

    // Stats
    int str, agi, vit, int_, dex, luk;  // Base stats

    // Position
    unsigned short mapindex;        // Map index
    short x, y;                     // Coordinates

    // Items
    struct s_storage storage;       // Storage
    struct item_data* inventory_data[MAX_INVENTORY];
    short equip_index[EQI_MAX];    // Equipment indices

    // Skills
    struct s_skill skill[MAX_SKILL];

    // State
    unsigned int state;             // Player state flags
    int fd;                         // Socket file descriptor

    // And 100+ more fields...
};
```

### **mob_data** (Monster Data)
```cpp
// Location: src/map/mob.hpp
struct mob_data {
    struct block_list bl;           // Block list
    struct unit_data ud;            // Unit data
    struct view_data *vd;           // View data
    struct status_data status;      // Status
    struct status_change sc;        // Status changes

    struct mob_db_data *db;         // Database reference

    int mob_id;                     // Monster ID
    short class_;                   // Class ID
    char name[NAME_LENGTH];         // Custom name

    struct {
        unsigned int size : 2;      // Size (small/medium/large)
        unsigned int ai : 4;        // AI type
        unsigned int clone : 1;     // Is clone
    } special_state;

    int target_id;                  // Current target
    int attacked_id;                // Last attacker

    // Timers
    int64 next_walktime;
    int64 attackabletime;

    // And more...
};
```

### **item_data** (Item Database)
```cpp
// Location: src/map/itemdb.hpp
struct item_data {
    uint16 nameid;                  // Item ID
    char name[ITEM_NAME_LENGTH];    // Aegis name
    char jname[ITEM_NAME_LENGTH];   // Display name

    enum item_types type;           // Item type
    int value_buy;                  // Buy price
    int value_sell;                 // Sell price
    int weight;                     // Weight
    int atk;                        // Attack
    int def;                        // Defense
    int range;                      // Range
    int slot;                       // Slots
    int look;                       // Sprite ID
    int elv;                        // Equip level
    int wlv;                        // Weapon level
    uint64 class_base[3];           // Usable by classes
    unsigned int sex;               // Gender
    uint16 equip;                   // Equipment position
    uint16 subtype;                 // Weapon/ammo subtype

    struct {
        unsigned int dead_branch : 1;
        unsigned int group_drop : 1;
        unsigned int guid : 1;
        // ... more flags
    } flag;

    struct script_code *script;     // Use script
    struct script_code *equip_script; // Equip script
    struct script_code *unequip_script; // Unequip script

    // And more...
};
```

### **skill_db** (Skill Database)
```cpp
// Location: src/map/skill.hpp
struct s_skill_db {
    uint16 nameid;                  // Skill ID
    char name[SKILL_NAME_LENGTH];   // Name
    char desc[SKILL_DESC_LENGTH];   // Description

    int range[MAX_SKILL_LEVEL];     // Range per level
    int hit[MAX_SKILL_LEVEL];       // Hit type
    int inf;                        // Target type
    int element[MAX_SKILL_LEVEL];   // Element
    int nk;                         // Damage properties
    int splash[MAX_SKILL_LEVEL];    // Splash range
    int max;                        // Max level
    int num[MAX_SKILL_LEVEL];       // Hits
    int cast[MAX_SKILL_LEVEL];      // Cast time
    int delay[MAX_SKILL_LEVEL];     // Delay
    int walkdelay[MAX_SKILL_LEVEL]; // Walk delay
    int upkeep_time[MAX_SKILL_LEVEL]; // Upkeep time
    int upkeep_time2[MAX_SKILL_LEVEL]; // Upkeep time 2
    int cooldown[MAX_SKILL_LEVEL];  // Cooldown
    int fixed_cast[MAX_SKILL_LEVEL]; // Fixed cast
    int cast_def_rate;              // Cast defense rate
    int inf2;                       // Additional flags
    int maxcount[MAX_SKILL_LEVEL];  // Max active instances
    int skill_type;                 // Skill type
    int blow_count[MAX_SKILL_LEVEL]; // Knockback

    // Requirements
    struct s_skill_require require;

    // And more...
};
```

---

## Server Architecture

### **Server Communication Flow**
```
[Client]
    ↕ TCP Packets
[Map Server] ←→ [Character Server] ←→ [Login Server]
    ↕                   ↕                     ↕
[MySQL Database]    [MySQL]              [MySQL]
```

### **Map Server Main Loop**
```cpp
// Simplified flow
int do_init(int argc, char *argv[]) {
    // 1. Load configuration
    // 2. Connect to char-server
    // 3. Load databases (item, mob, skill, etc.)
    // 4. Load scripts
    // 5. Create listening socket
    return 0;
}

void do_final() {
    // Cleanup on shutdown
}

int main(int argc, char *argv[]) {
    do_init(argc, argv);

    while (runflag) {
        // Main loop (every ~100ms)
        timer_do_tick();      // Process timers
        do_sendrecv();        // Process network
        flush_fifos();        // Send queued packets
        do_parsepacket();     // Parse received packets
    }

    do_final();
    return 0;
}
```

### **Packet Processing Flow**
```
Client sends packet
    ↓
do_sendrecv() receives data
    ↓
parse_func() (clif_parse)
    ↓
clif->parse_*() function
    ↓
Game logic (pc_*, mob_*, skill_*, etc.)
    ↓
clif->send*() sends response
    ↓
WFIFOSET() queues packet
    ↓
flush_fifos() sends to client
```

---

## Build System

### **CMake (Cross-Platform)**

**CMakeLists.txt** (Root)
```cmake
cmake_minimum_required(VERSION 3.10)
project(rAthena LANGUAGES C CXX)

# Options
option(BUILD_SERVERS "Build all servers" ON)
option(WITH_MYSQL "Build with MySQL support" ON)
option(WITH_PCRE "Build with PCRE support" ON)

# Subdirectories
add_subdirectory(3rdparty)
add_subdirectory(src)

# Find packages
find_package(MySQL REQUIRED)
find_package(PCRE REQUIRED)
find_package(ZLIB REQUIRED)
```

**Build Commands:**
```bash
# Linux/Mac
mkdir build
cd build
cmake ..
make -j$(nproc)

# Debug build
cmake -DCMAKE_BUILD_TYPE=Debug ..

# With custom MySQL
cmake -DMYSQL_INCLUDE_DIR=/path/to/include -DMYSQL_LIBRARY=/path/to/lib ..
```

### **Visual Studio (Windows)**

**Projects:**
- `rAthena.sln` - Solution file
- `map-server.vcxproj` - Map server
- `char-server.vcxproj` - Char server
- `login-server.vcxproj` - Login server

**Build Configurations:**
- Debug - With debug symbols
- Release - Optimized

---

## Header Files Reference

### **Common Include Pattern**
```cpp
#include "config/core.hpp"      // Core configuration
#include "common/cbasetypes.hpp" // Base types
#include "common/mmo.hpp"       // MMO structures
#include "common/timer.hpp"     // Timer functions
#include "common/nullpo.hpp"    // Null pointer checks
#include "common/malloc.hpp"    // Memory functions
#include "common/showmsg.hpp"   // Logging
#include "common/strlib.hpp"    // String functions
#include "map/map.hpp"          // Map functions
#include "map/pc.hpp"           // Player functions
```

### **Important Headers**

**cbasetypes.hpp** - Base type definitions
```cpp
typedef int8_t int8;
typedef int16_t int16;
typedef int32_t int32;
typedef int64_t int64;
typedef uint8_t uint8;
typedef uint16_t uint16;
typedef uint32_t uint32;
typedef uint64_t uint64;

#ifndef max
    #define max(a,b) (((a) > (b)) ? (a) : (b))
#endif
#ifndef min
    #define min(a,b) (((a) < (b)) ? (a) : (b))
#endif
```

**mmo.hpp** - MMO constants
```cpp
#define MAX_INVENTORY 100
#define MAX_STORAGE 600
#define MAX_SKILL 5020
#define MAX_PARTY 12
#define MAX_GUILD 16+10*6
#define MAX_GUILDSKILL 20
```

**nullpo.hpp** - Null pointer checks
```cpp
#define nullpo_ret(t) if (nullpo_chk(__FILE__, __LINE__, __func__, t)) return 0
#define nullpo_retr(ret, t) if (nullpo_chk(__FILE__, __LINE__, __func__, t)) return ret
#define nullpo_retv(t) if (nullpo_chk(__FILE__, __LINE__, __func__, t)) return
#define nullpo_retb(t) if (nullpo_chk(__FILE__, __LINE__, __func__, t)) break
```

---

## Common Patterns

### **Null Pointer Checking**
```cpp
int my_function(struct map_session_data *sd) {
    nullpo_ret(sd);  // Return 0 if sd is NULL

    // Safe to use sd here
    pc_heal(sd, 100, 0);
    return 1;
}
```

### **Iterating Players in Area**
```cpp
int my_callback(struct block_list *bl, va_list ap) {
    struct map_session_data *sd = (struct map_session_data *)bl;
    nullpo_ret(sd);

    // Do something with player
    clif->message(sd->fd, "Hello!");
    return 1;
}

// Call from somewhere
map_foreachinarea(my_callback, m, x0, y0, x1, y1, BL_PC);
```

### **Memory Allocation**
```cpp
// Allocate
struct my_data *data = (struct my_data *)aCalloc(1, sizeof(struct my_data));

// Use
data->value = 100;

// Free
aFree(data);
```

### **Timer Usage**
```cpp
int my_timer(int tid, int64 tick, int id, intptr_t data) {
    struct map_session_data *sd = map->id2sd(id);
    if (!sd) return 0;

    // Do something
    clif->message(sd->fd, "Timer triggered!");
    return 0;
}

// Add timer (5 seconds)
add_timer(gettick() + 5000, my_timer, sd->bl.id, 0);

// Add repeating timer (every 1 second)
add_timer_interval(gettick() + 1000, my_timer, sd->bl.id, 0, 1000);
```

---

## Modification Guide

### **Where to Make Changes**

**Custom Stats/Formulas:**
- `src/map/pc.cpp` - Player stat calculations
- `src/map/status.cpp` - Status calculations
- `src/map/battle.cpp` - Damage formulas

**Custom Items:**
- `src/map/itemdb.cpp` - Item loading/handling
- `src/map/pc.cpp` (pc_bonus*) - Item bonuses

**Custom Skills:**
- `src/map/skill.cpp` - Skill mechanics
- `src/map/battle.cpp` - Skill damage

**Custom Monsters:**
- `src/map/mob.cpp` - Monster AI/behavior
- `src/map/battle.cpp` - Monster damage

**Custom Packets:**
- `src/map/clif.cpp` - Packet handlers

**Custom Script Commands:**
- `src/map/script.cpp` - Add BUILDIN() functions

### **Safe Modification Locations**

**src/custom/** - Put all custom code here
```cpp
// src/custom/my_feature.cpp
#include "my_feature.hpp"

void my_custom_function() {
    ShowInfo("Custom function called!\n");
}
```

**Include in main files:**
```cpp
// In src/map/pc.cpp
#include "../custom/my_feature.hpp"

// Call your function
my_custom_function();
```

---

## Related References

- **Script Commands**: [KB_REF_ScriptCommandCreation.md]
- **Plugin System**: [KB_REF_PluginSystem.md]
- **Database C++**: [KB_REF_DatabaseCPP.md]
- **Packets**: [KB_REF_PacketStructure.md]
- **Common Mods**: [KB_REF_CommonSrcModifications.md]
- **Best Practices**: [KB_REF_SourceCodeBestPractices.md]

---

**End of KB_REF_022 - Source Code Structure & Architecture**
