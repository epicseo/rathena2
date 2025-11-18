# rAthena Source Code Structure Reference

## Table of Contents
1. [Directory Structure Overview](#directory-structure-overview)
2. [Core Directories Deep Dive](#core-directories-deep-dive)
3. [Essential Data Structures](#essential-data-structures)
4. [File Responsibilities](#file-responsibilities)
5. [Data Flow Between Systems](#data-flow-between-systems)
6. [Include Hierarchy](#include-hierarchy)
7. [Build System (CMake)](#build-system-cmake)
8. [Feature Location Guide](#feature-location-guide)
9. [Navigation Quick Reference](#navigation-quick-reference)
10. [Code Examples](#code-examples)

---

## Directory Structure Overview

```
rathena2/
├── src/
│   ├── common/          # Shared code (all servers)
│   ├── map/             # Map server (game logic)
│   │   └── skills/      # Skill implementations by class
│   ├── char/            # Character server (save/load)
│   ├── login/           # Login server (authentication)
│   ├── web/             # Web server integration
│   ├── config/          # Compile-time configurations
│   │   └── classes/     # Class-specific configs
│   ├── tool/            # Development tools
│   └── custom/          # Custom modifications
├── 3rdparty/            # External dependencies
├── conf/                # Runtime configurations
├── db/                  # Game databases (YAML)
├── npc/                 # NPC scripts
└── sql-files/           # Database schemas
```

**Key Size Statistics (Line Counts):**
- script.cpp: 28,574 lines (largest - script engine)
- skill.cpp: 26,478 lines (skill system)
- clif.cpp: 25,821 lines (client interface/packets)
- status.cpp: 16,480 lines (status/stats calculations)
- pc.cpp: 16,102 lines (player character logic)
- battle.cpp: 12,680 lines (damage calculations)

---

## Core Directories Deep Dive

### 1. src/map/ - Map Server (Game Logic Core)

**Primary Files:**

| File | Lines | Purpose |
|------|-------|---------|
| **script.cpp/hpp** | 28,574 | Script engine, NPC commands (@commands, script functions) |
| **skill.cpp/hpp** | 26,478 | Skill system, casting, effects, requirements |
| **clif.cpp/hpp** | 25,821 | Client Interface - all packet handling (send/receive) |
| **status.cpp/hpp** | 16,480 | Status calculations, buffs/debuffs, stat computations |
| **pc.cpp/hpp** | 16,102 | Player character logic, inventory, equipment, jobs |
| **battle.cpp/hpp** | 12,680 | Damage calculations, battle formulas, element tables |
| **atcommand.cpp/hpp** | 12,074 | GM commands implementation |
| **mob.cpp/hpp** | 7,374 | Monster AI, spawning, movement, skills |
| **npc.cpp/hpp** | 6,381 | NPC management, script execution, shops |
| **map.cpp/hpp** | 5,478 | Map management, coordinates, zone handling |
| **itemdb.cpp/hpp** | 4,948 | Item database, bonuses, requirements |
| **unit.cpp/hpp** | 4,298 | Movement, pathfinding, target selection |
| **guild.cpp/hpp** | 2,755 | Guild systems, WoE, emblems |
| **party.cpp/hpp** | 1,573 | Party systems, exp sharing |

**Packet Files:**
- **packets.hpp** - Packet structure definitions
- **packets_struct.hpp** - Actual packet structs
- **clif_packetdb.hpp** - Packet database
- **clif_obfuscation.hpp** - Packet encryption/obfuscation
- **clif_shuffle.hpp** - Packet key shuffling

**Skills Subdirectory** (`src/map/skills/`):
```
skills/
├── acolyte/          # Priest, Monk skills
├── archer/           # Hunter, Bard/Dancer skills
├── mage/             # Wizard, Sage skills
├── merchant/         # Blacksmith, Alchemist skills
├── swordman/         # Knight, Crusader skills
├── thief/            # Assassin, Rogue skills
├── novice/           # Novice/Super Novice skills
├── gunslinger/       # Gunslinger skills
├── ninja/            # Ninja skills
├── summoner/         # Summoner skills
├── mercenary/        # Mercenary skills
├── npc/              # NPC/Monster skills
├── custom/           # Custom skill implementations
├── skill_impl.cpp/hpp          # Skill implementation base
├── skill_factory.cpp/hpp       # Skill factory pattern
├── status_skill_impl.cpp/hpp   # Status-related skills
└── weapon_skill_impl.cpp/hpp   # Weapon-based skills
```

### 2. src/char/ - Character Server

**Primary Files:**

| File | Purpose |
|------|---------|
| **char.cpp/hpp** | Main character server, character management |
| **char_clif.cpp/hpp** | Client interface for char server |
| **char_logif.cpp/hpp** | Login server interface |
| **char_mapif.cpp/hpp** | Map server interface |
| **inter.cpp/hpp** | Inter-server communication core |
| **int_guild.cpp/hpp** | Guild inter-server operations |
| **int_party.cpp/hpp** | Party inter-server operations |
| **int_storage.cpp/hpp** | Storage inter-server operations |
| **int_mail.cpp/hpp** | Mail system inter-server |
| **int_auction.cpp/hpp** | Auction system inter-server |
| **int_quest.cpp/hpp** | Quest inter-server operations |
| **int_pet.cpp/hpp** | Pet inter-server operations |
| **int_homun.cpp/hpp** | Homunculus inter-server |
| **int_mercenary.cpp/hpp** | Mercenary inter-server |
| **int_elemental.cpp/hpp** | Elemental inter-server |
| **int_achievement.cpp/hpp** | Achievement inter-server |
| **int_clan.cpp/hpp** | Clan inter-server operations |

### 3. src/login/ - Login Server

**Primary Files:**

| File | Purpose |
|------|---------|
| **login.cpp/hpp** | Main login server logic |
| **account.cpp/hpp** | Account management, database operations |
| **loginclif.cpp/hpp** | Client interface (login packets) |
| **loginchrif.cpp/hpp** | Character server interface |
| **logincnslif.cpp/hpp** | Console interface |
| **loginlog.cpp/hpp** | Login logging system |
| **ipban.cpp/hpp** | IP banning system |

### 4. src/common/ - Shared Libraries

**Core Files:**

| File | Purpose |
|------|---------|
| **mmo.hpp** | Core definitions, limits, constants (MAX_INVENTORY, etc.) |
| **cbasetypes.hpp** | Base types (uint8, int32, etc.) |
| **db.cpp/hpp** | Database abstraction layer |
| **database.cpp/hpp** | YAML database system |
| **socket.cpp/hpp** | Network socket handling |
| **timer.cpp/hpp** | Timer/tick system |
| **malloc.cpp/hpp** | Memory management |
| **showmsg.cpp/hpp** | Logging/output system |
| **strlib.cpp/hpp** | String utilities |
| **utils.cpp/hpp** | General utilities |
| **random.cpp/hpp** | Random number generation |
| **nullpo.cpp/hpp** | Null pointer checking |
| **core.cpp/hpp** | Server core initialization |
| **sql.cpp/hpp** | SQL database interface |
| **mapindex.cpp/hpp** | Map index management |
| **grfio.cpp/hpp** | GRF file reading |
| **conf.cpp/hpp** | Configuration file parsing |
| **ers.cpp/hpp** | Entry Reusage System (memory pools) |

**Location:** `/home/user/rathena2/src/common/mmo.hpp`

### 5. src/config/ - Compile-Time Configuration

**Configuration Files:**

| File | Purpose |
|------|---------|
| **core.hpp** | Core features (renewal, secure, etc.) |
| **const.hpp** | Constant definitions |
| **packets.hpp** | Packet version configuration |
| **renewal.hpp** | Renewal mode settings |
| **secure.hpp** | Security settings |
| **classes/*.hpp** | Class-specific configurations |

---

## Essential Data Structures

### 1. block_list - Universal Object Base

**Location:** `/home/user/rathena2/src/map/map.hpp:461-466`

```cpp
struct block_list {
    struct block_list *next, *prev;  // Linked list pointers
    int32 id;                        // Unique object ID
    int16 m, x, y;                   // Map index, coordinates
    enum bl_type type;               // Object type (PC, MOB, NPC, etc.)
};
```

**Purpose:** Base structure for all map objects. Every entity (player, mob, NPC, item) starts with this.

**Type Enumeration (bl_type):**
- `BL_NUL` - Invalid/null
- `BL_PC` - Player character
- `BL_MOB` - Monster
- `BL_PET` - Pet
- `BL_HOM` - Homunculus
- `BL_MER` - Mercenary
- `BL_ELEM` - Elemental
- `BL_NPC` - NPC
- `BL_ITEM` - Floor item
- `BL_SKILL` - Skill unit (ground skills)
- `BL_CHAT` - Chat room

### 2. map_session_data - Player Character

**Location:** `/home/user/rathena2/src/map/pc.hpp:381+`

```cpp
class map_session_data : public block_list {
public:
    struct unit_data ud;                        // Movement, targets, timers
    struct view_data vd;                        // Visual appearance data
    struct status_data base_status, battle_status;  // Base/calculated stats
    status_change sc;                           // Status change (buffs/debuffs)
    struct regen_data regen;                    // HP/SP regeneration

    // State flags
    struct s_state {
        uint32 active : 1;                      // Active player flag
        uint32 menu_or_input : 1;               // NPC interaction state
        uint32 dead_sit : 2;                    // Dead/sitting state
        e_lr_flag lr_flag;                      // Left/right hand flag
        uint32 arrow_atk : 1;                   // Arrow attack flag
        uint32 storage_flag : 3;                // Storage open state
        uint32 trading : 1;                     // Trade state
        uint32 vending : 1;                     // Vending state
        uint32 buyingstore : 1;                 // Buying store state
        // ... many more flags
    } state;

    // Special states from equipment/buffs
    struct {
        unsigned char no_weapon_damage, no_magic_damage, no_misc_damage;
        uint32 restart_full_recover : 1;
        uint32 no_castcancel : 1;
        uint32 no_gemstone : 2;
        uint32 intravision : 1;                 // Maya Purple Card
        uint32 perfect_hiding : 1;
        // ... more special states
    } special_state;

    uint32 login_id1, login_id2;                // Login session IDs
    uint64 class_;                              // Job ID
    int32 group_id;                             // Permission group

    struct mmo_charstatus status;               // Character data (DB)

    // Inventories
    struct s_storage storage, premiumStorage;   // Storages
    struct s_storage inventory;                 // Player inventory
    struct s_storage cart;                      // Cart

    struct item_data* inventory_data[MAX_INVENTORY];  // Item data pointers
    int16 equip_index[EQI_MAX];                 // Equipment indices

    uint32 weight, max_weight, add_max_weight;  // Weight system
    int32 fd;                                   // Socket file descriptor
    uint16 mapindex;                            // Current map index

    // ... hundreds more fields (equipment bonuses, skill data, etc.)
};
```

**Key Sections:**
- **Lines 381-499:** Core data, state, inventory
- **Lines 500-700:** Skills, bonuses, equipment data
- **Lines 700-900:** Combat stats, regeneration, timers
- **Lines 900+:** Social, quests, achievements

### 3. mob_data - Monster Instance

**Location:** `/home/user/rathena2/src/map/mob.hpp:337-349+`

```cpp
struct mob_data : public block_list {
    struct unit_data ud;                        // Movement/AI data
    struct view_data *vd;                       // Visual data pointer
    bool vd_changed;                            // View changed flag
    struct status_data status, *base_status;    // Current/base stats
    status_change sc;                           // Status changes
    std::shared_ptr<s_mob_db> db;              // Mob database entry
    char name[NAME_LENGTH];                     // Custom name

    struct s_specialState {
        uint32 size : 2;                        // Small/Big size
        enum mob_ai ai;                         // Special AI type
        uint32 clone : 1;                       // Clone flag
    } special_state;

    struct spawn_data *spawn;                   // Spawn point data
    int16 spawn_x, spawn_y;                     // Spawn coordinates

    // Damage log for MVP calculation
    struct s_dmglog {
        int32 id;                               // Char ID
        int64 dmg;                              // Damage dealt
        int64 dmg_tanked;                       // Damage tanked
        uint32 flag : 2;                        // Damage type flag
    } dmglog[DAMAGELOG_SIZE];

    // ... more fields (loot, timers, states)
};
```

**Mob Database Structure** (`s_mob_db` - Lines 261-285):
```cpp
struct s_mob_db {
    uint32 id;                                  // Monster ID
    std::string sprite;                         // Sprite name
    std::string name;                           // Monster name
    std::string jname;                          // Japanese name
    t_exp base_exp, job_exp, mexp;             // Experience values
    uint16 range2, range3;                      // Chase/sight range
    std::vector<e_race2> race2;                // Race2 types
    uint16 lv;                                  // Level
    std::vector<std::shared_ptr<s_mob_drop>> dropitem;     // Drops
    std::vector<std::shared_ptr<s_mob_drop>> mvpitem;      // MVP drops
    status_data status;                         // Base stats
    view_data vd;                               // Visual data
    uint32 option;                              // Special options
    std::vector<std::shared_ptr<s_mob_skill>> skill;       // Mob skills
    uint16 damagetaken;                         // Damage modifier
    int32 group_id;                             // Mob group
    std::string title;                          // Title string
};
```

### 4. item_data - Item Database Entry

**Location:** `/home/user/rathena2/src/map/itemdb.hpp:150+`

```cpp
struct item_data {
    t_itemid nameid;                            // Item ID
    char name[ITEM_NAME_LENGTH];                // Item name (English)
    char jname[ITEM_NAME_LENGTH];               // Item name (Japanese)

    enum item_types type;                       // Item type
    int32 value_buy;                            // Buy price
    int32 value_sell;                           // Sell price
    int32 weight;                               // Weight
    int32 atk;                                  // ATK
    int32 matk;                                 // MATK
    int32 def;                                  // DEF

    int32 range;                                // Attack range
    uint32 slot;                                // Card slots
    uint64 class_base[3];                       // Job restrictions
    uint32 class_upper;                         // Upper job restrictions
    uint64 sex;                                 // Gender restrictions
    uint32 equip;                               // Equipment position

    int32 wlv;                                  // Weapon level
    int32 elv;                                  // Equipment level

    struct script_code *script;                 // Use/equip script
    struct script_code *equip_script;           // Equip bonus script
    struct script_code *unequip_script;         // Unequip script

    struct {
        uint32 delay;                           // Item delay
        uint32 status;                          // Required status
        // ... more requirements
    } require;

    // ... item flags, bonuses, randomoptions
};
```

### 5. s_skill_db - Skill Database Entry

**Location:** `/home/user/rathena2/src/map/skill.hpp:150+`

```cpp
struct s_skill_db {
    uint16 nameid;                              // Skill ID
    char name[SKILL_NAME_LENGTH];               // Skill name
    char desc[SKILL_DESC_LENGTH];               // Description

    std::bitset<INF2_MAX> inf2;                 // Skill info flags
    uint16 inf;                                 // Skill type (attack/support)
    std::bitset<NK_MAX> nk;                     // Damage properties

    uint16 range[MAX_SKILL_LEVEL];              // Cast range per level
    int16 hit;                                  // Hit type

    uint16 max_level;                           // Max skill level

    struct {
        int16 hp[MAX_SKILL_LEVEL];              // HP cost
        int16 sp[MAX_SKILL_LEVEL];              // SP cost
        int16 hp_rate[MAX_SKILL_LEVEL];         // HP% cost
        int16 sp_rate[MAX_SKILL_LEVEL];         // SP% cost
        int16 zeny[MAX_SKILL_LEVEL];            // Zeny cost
        uint32 weapon;                          // Weapon requirement
        uint32 ammo;                            // Ammo requirement
        // ... more requirements
    } require;

    int32 casttime[MAX_SKILL_LEVEL];            // Cast time
    int32 delay[MAX_SKILL_LEVEL];               // After-cast delay
    int32 cooldown[MAX_SKILL_LEVEL];            // Cooldown

    // ... damage calculations, splash, flags
};
```

### 6. status_data - Entity Stats

**Location:** `/home/user/rathena2/src/map/status.hpp:200+`

```cpp
struct status_data {
    uint32 hp, sp, ap;                          // Current HP/SP/AP
    uint32 max_hp, max_sp, max_ap;              // Max HP/SP/AP

    uint16 str, agi, vit, int_, dex, luk;       // Primary stats
    uint16 pow, sta, wis, spl, con, crt;        // 4th job stats

    uint32 batk, watk, watk2;                   // Base/weapon ATK
    uint32 matk_min, matk_max;                  // Magic ATK
    int32 def, mdef;                            // Defense
    int32 def2, mdef2;                          // Soft defense

    int32 hit, flee, flee2;                     // Accuracy/evasion
    int32 cri;                                  // Critical rate
    int32 aspd, amotion, dmotion;               // Attack speed/motion

    uint16 speed;                               // Movement speed
    uint16 size;                                // Entity size
    uint16 race;                                // Race
    uint16 element;                             // Element

    // ... many more combat stats
};
```

### 7. unit_data - Movement & Action Control

**Location:** `/home/user/rathena2/src/map/unit.hpp:40+`

```cpp
struct unit_data {
    block_list *bl;                             // Owner
    struct walkpath_data walkpath;              // Path data

    t_tick attacktimer;                         // Attack timer
    t_tick walktimer;                           // Walk timer

    int32 target;                               // Current target ID
    int32 target_to;                            // Next target

    uint16 skill_id, skill_lv;                  // Casting skill
    int32 skilltarget;                          // Skill target ID
    t_tick skilltimer;                          // Skill timer

    struct {
        uint16 id;                              // Skill unit group ID
        t_tick tick;                            // Creation tick
    } stepskill;                                // Step skill data

    uint16 state;                               // Unit state flags
    uint8 dir;                                  // Facing direction

    // ... combat, movement state
};
```

---

## File Responsibilities

### Combat & Battle System

**battle.cpp/hpp** (12,680 lines)
- **Primary Functions:**
  - `battle_calc_attack()` - Main damage calculation entry
  - `battle_calc_weapon_attack()` - Physical damage
  - `battle_calc_magic_attack()` - Magic damage
  - `battle_calc_misc_attack()` - Misc damage (traps, etc.)
  - `battle_attr_fix()` - Element modifier calculation
  - `battle_calc_defense()` - Defense reduction
  - `battle_damage()` - Apply damage to target

**Key Code:** Lines 48-70
```cpp
/**
 * Returns the current/list skill used by the bl
 * @param bl
 * @return skill_id
 */
uint16 battle_getcurrentskill(block_list *bl)
{
    struct unit_data *ud;

    if( bl->type == BL_SKILL ) {
        skill_unit *su = (skill_unit*)bl;
        return (su && su->group?su->group->skill_id:0);
    }

    ud = unit_bl2ud(bl);
    return (ud?ud->skill_id:0);
}
```

**Battle Configuration:** `struct Battle_Config battle_config` - Global battle settings

### Player Management

**pc.cpp/hpp** (16,102 lines)
- **Primary Functions:**
  - `pc_authok()` - Player login initialization
  - `pc_reg_received()` - Load player data from char server
  - `pc_makesavestatus()` - Prepare save data
  - `pc_equipitem()` - Equip item
  - `pc_unequipitem()` - Unequip item
  - `pc_additem()` - Add item to inventory
  - `pc_delitem()` - Remove item from inventory
  - `pc_dropitem()` - Drop item on ground
  - `pc_checkskill()` - Check if player has skill
  - `pc_gainexp()` - Add experience
  - `pc_levelup()` - Level up process
  - `pc_jobchange()` - Change job

**Includes (Lines 4-66):**
```cpp
#include "pc.hpp"

#include <common/cbasetypes.hpp>
#include <common/database.hpp>
#include <common/mmo.hpp>
#include <common/nullpo.hpp>
#include <common/random.hpp>
#include <common/showmsg.hpp>
#include <common/socket.hpp>
#include <common/timer.hpp>

#include "achievement.hpp"
#include "atcommand.hpp"
#include "battle.hpp"
#include "clif.hpp"
#include "guild.hpp"
#include "itemdb.hpp"
#include "mob.hpp"
#include "npc.hpp"
#include "party.hpp"
#include "skill.hpp"
#include "status.hpp"
#include "storage.hpp"
// ... more includes
```

### Monster AI & Management

**mob.cpp/hpp** (7,374 lines)
- **Primary Functions:**
  - `mob_spawn()` - Spawn monster
  - `mob_spawn_guardian()` - Spawn guardian
  - `mob_ai_sub_hard()` - Monster AI logic
  - `mob_attack()` - Monster attack
  - `mob_skill_use()` - Monster skill usage
  - `mob_damage()` - Damage monster
  - `mob_dead()` - Monster death handling
  - `mob_drop_item()` - Drop items
  - `mob_summon()` - Summon monsters

**Monster Skill Structure** (Lines 196-208):
```cpp
struct s_mob_skill {
    enum MobSkillState state;    // MSS_IDLE, MSS_WALK, MSS_ATTACK, etc.
    uint16 skill_id, skill_lv;   // Skill ID and level
    int16 permillage;            // Usage rate (per 1000)
    int32 casttime, delay;       // Cast time, delay
    int16 cancel;                // Cancel flag
    int16 cond1;                 // Condition 1
    int64 cond2;                 // Condition 2
    int16 target;                // Target type
    int32 val[5];                // Additional values
    int16 emotion;               // Emotion to display
    uint16 msg_id;               // Message ID
};
```

### Skill System

**skill.cpp/hpp** (26,478 lines)
- **Primary Functions:**
  - `skill_check_condition()` - Validate skill requirements
  - `skill_use_id()` - Use skill on target
  - `skill_use_pos()` - Use skill on ground
  - `skill_castend_id()` - Finish casting on target
  - `skill_castend_pos()` - Finish casting on ground
  - `skill_attack()` - Skill attack damage
  - `skill_area_sub()` - Area skill processing
  - `skill_timerskill()` - Delayed skill effects
  - `skill_addtimerskill()` - Add timed skill
  - `skill_castcancel()` - Cancel casting

**Skill Constants** (Lines 31-48):
```cpp
#define MAX_SKILL_PRODUCE_DB    300     // Max Produce DB
#define MAX_PRODUCE_RESOURCE    12      // Max Produce requirements
#define MAX_SKILL_LEVEL         13      // Max Skill Level (for skill_db storage)
#define MAX_MOBSKILL_LEVEL      100     // Max monster skill level (on skill usage)
#define MAX_SKILL_CRIMSON_MARKER 3      // Max Crimson Marker targets (RL_C_MARKER)
#define SKILL_NAME_LENGTH       40      // Max Skill Name length
#define SKILL_DESC_LENGTH       40      // Max Skill Desc length

// Used with tracking the hitcount of Earthquake for skills that can avoid the first attack
#define NPC_EARTHQUAKE_FLAG 0x800

// To control alternative skill scalings
#define SKILL_ALTDMG_FLAG 0x10
// Make skill ignore requirement consumption
#define SKILL_NOCONSUME_REQ 0x20
// Make skill consume ammo, but not the unit
#define UNIT_NOCONSUME_AMMO 0x40
```

### Status & Stats Calculation

**status.cpp/hpp** (16,480 lines)
- **Primary Functions:**
  - `status_calc_pc()` - Calculate player stats (main)
  - `status_calc_mob()` - Calculate monster stats
  - `status_calc_str()`, `status_calc_agi()`, etc. - Calculate individual stats
  - `status_base_atk()` - Calculate base ATK
  - `status_calc_watk()` - Calculate weapon ATK
  - `status_calc_matk()` - Calculate magic ATK
  - `status_calc_def()` - Calculate defense
  - `status_calc_flee()` - Calculate flee
  - `status_change_start()` - Start status effect
  - `status_change_end()` - End status effect
  - `status_calc_regen()` - Calculate regeneration

**Status Change System:**
- Over 700+ status effects defined
- Timers for buff/debuff management
- Icon display to client
- Stack rules (stackable, non-stackable, refresh)

### Network & Packets

**clif.cpp/hpp** (25,821 lines)
- **Primary Functions:**
  - `clif_parse()` - Main packet parser
  - `clif_parse_*()` - Individual packet handlers (hundreds)
  - `clif_send()` - Send packet to client
  - `clif_displaymessage()` - Display message
  - `clif_skill_damage()` - Show skill damage
  - `clif_damage()` - Show physical damage
  - `clif_updatestatus()` - Update player status
  - `clif_changelook()` - Change appearance
  - `clif_item_equip()` - Show equipment change
  - `clif_inventorylist()` - Send inventory

**Includes (Lines 1-61):**
```cpp
#include "clif.hpp"

#include <common/cbasetypes.hpp>
#include <common/socket.hpp>
#include <common/timer.hpp>
#include <common/nullpo.hpp>
#include <common/random.hpp>
#include <common/showmsg.hpp>
#include <common/strlib.hpp>
#include <common/utils.hpp>

#include "achievement.hpp"
#include "atcommand.hpp"
#include "battle.hpp"
#include "battleground.hpp"
#include "cashshop.hpp"
#include "channel.hpp"
#include "chat.hpp"
#include "clan.hpp"
#include "elemental.hpp"
#include "guild.hpp"
#include "homunculus.hpp"
#include "instance.hpp"
#include "intif.hpp"
#include "itemdb.hpp"
#include "log.hpp"
#include "mail.hpp"
#include "map.hpp"
#include "mercenary.hpp"
#include "mob.hpp"
#include "npc.hpp"
#include "party.hpp"
#include "pc.hpp"
#include "pet.hpp"
#include "quest.hpp"
#include "script.hpp"
#include "skill.hpp"
#include "status.hpp"
#include "storage.hpp"
#include "unit.hpp"
#include "vending.hpp"
```

### Script Engine

**script.cpp/hpp** (28,574 lines - LARGEST FILE)
- **Primary Functions:**
  - `script_parse()` - Parse NPC scripts
  - `run_script()` - Execute script
  - `script_rid2sd()` - Get player from RID
  - `script_getnum()` - Get number parameter
  - `script_getstr()` - Get string parameter
  - `script_setvar()` - Set variable
  - `script_getvar()` - Get variable
  - Hundreds of builtin functions (BUILDIN macro)

**Script Built-in Functions:**
- Item manipulation: `getitem()`, `delitem()`, `getitemname()`
- Player data: `getcharid()`, `getskillv()`, `getskilllv()`
- Stats: `readparam()`, `getstat()`
- Skills: `skill()`, `addtoskill()`, `guildskill()`
- NPC interaction: `menu()`, `select()`, `input()`
- Timers: `addtimer()`, `deltimer()`, `sleep()`
- Maps: `warp()`, `areawarp()`, `mapannounce()`
- Combat: `monster()`, `areamonster()`, `killmonster()`
- And 500+ more functions

**Script State** (Lines 77-100):
```cpp
struct eri *array_ers;
DBMap *st_db;
uint32 active_scripts;
uint32 next_id;
struct eri *st_ers;
struct eri *stack_ers;
static map_session_data* dummy_sd;

static bool script_rid2sd_( struct script_state *st, map_session_data** sd, const char *func );

/**
 * Get `sd` from a account id in `loc` param instead of attached rid
 * @param st Script
 * @param loc Location to look account id in script parameter
 * @param sd Variable that will be assigned
 * @return True if `sd` is assigned, false otherwise
 **/
static bool script_accid2sd_(struct script_state *st, uint8 loc, map_session_data **sd, const char *func) {
    if (script_hasdata(st, loc)) {
        int32 id_ = script_getnum(st, loc);
        if (!(*sd = map_id2sd(id_))){
            ShowError("%s: Player with account id '%d' is not found.\n", func, id_);
            return false;
        }else{
            return true;
        }
    }
    else
        return script_rid2sd_(st,sd,func);
}
```

### Item Database

**itemdb.cpp/hpp** (4,948 lines)
- **Primary Functions:**
  - `itemdb_search()` - Find item by ID
  - `itemdb_exists()` - Check if item exists
  - `itemdb_searchname()` - Find item by name
  - `itemdb_isequip()` - Is equipment
  - `itemdb_isstackable()` - Is stackable
  - `itemdb_type()` - Get item type
  - `itemdb_weight()` - Get item weight
  - `itemdb_value_buy()` - Get buy price
  - `itemdb_value_sell()` - Get sell price
  - `itemdb_canrefine()` - Can refine
  - `itemdb_isidentified()` - Is identified

**Item Type Enum:**
```cpp
enum item_types {
    IT_HEALING = 0,        // Consumables
    IT_UNKNOWN,            // Unknown
    IT_USABLE,             // Usable items
    IT_ETC,                // Etc items
    IT_WEAPON,             // Weapons
    IT_ARMOR,              // Armor
    IT_CARD,               // Cards
    IT_PETEGG,             // Pet eggs
    IT_PETARMOR,           // Pet equipment
    IT_UNKNOWN2,           // Unknown
    IT_AMMO,               // Ammo
    IT_DELAYCONSUME,       // Delay consume
    IT_CASH = 18,          // Cash shop items
    IT_MAX
};
```

### Map Management

**map.cpp/hpp** (5,478 lines)
- **Primary Functions:**
  - `map_addflooritem()` - Add item to floor
  - `map_foreachinarea()` - Execute function in area
  - `map_foreachincell()` - Execute in cell
  - `map_foreachinrange()` - Execute in range
  - `map_searchrandfreecell()` - Find random free cell
  - `map_mapindex2mapid()` - Convert map index to ID
  - `map_id2bl()` - Get block_list by ID
  - `map_id2sd()` - Get player by ID
  - `map_id2md()` - Get mob by ID
  - `map_id2nd()` - Get NPC by ID

**Block List Iteration:**
The map server uses linked lists for efficient object iteration:
```cpp
// Iterate all objects in a range
map_foreachinrange(function, center_bl, range, type, ...args);

// Iterate all objects in rectangular area
map_foreachinarea(function, m, x0, y0, x1, y1, type, ...args);

// Iterate all objects in a cell
map_foreachincell(function, m, x, y, type, ...args);
```

### NPC Management

**npc.cpp/hpp** (6,381 lines)
- **Primary Functions:**
  - `npc_parse_script()` - Parse script NPC
  - `npc_parse_warp()` - Parse warp NPC
  - `npc_parse_shop()` - Parse shop NPC
  - `npc_click()` - NPC click handler
  - `npc_scriptcont()` - Continue script
  - `npc_buylist()` - Process buy
  - `npc_selllist()` - Process sell
  - `npc_event()` - Trigger event
  - `npc_timerevent()` - NPC timer event

### Unit Control (Movement/Actions)

**unit.cpp/hpp** (4,298 lines)
- **Primary Functions:**
  - `unit_walktoxy()` - Walk to coordinates
  - `unit_stop_walking()` - Stop walking
  - `unit_attack()` - Start attack
  - `unit_stop_attack()` - Stop attack
  - `unit_skilluse_id()` - Use skill on target
  - `unit_skilluse_pos()` - Use skill on position
  - `unit_warp()` - Warp unit
  - `unit_movepos()` - Move to position
  - `unit_setdir()` - Set facing direction

---

## Data Flow Between Systems

### Player Login Sequence

```
[Client] --> [Login Server] --> [Char Server] --> [Map Server]
```

**Detailed Flow:**

1. **Login Server** (`login.cpp`)
   - Client sends login packet → `loginclif_parse()`
   - Validate credentials → `account_db.load()`
   - Send character server list → `loginclif_server_list()`

2. **Character Server** (`char.cpp`)
   - Client selects character → `char_parse_char_select()`
   - Load character data from DB → `char_mmo_char_fromsql()`
   - Send to map server → `char_mapif_char_select_ack()`

3. **Map Server** (`pc.cpp`, `chrif.cpp`)
   - Receive auth request → `chrif_authreq()`
   - Character server responds → `chrif_authok()`
   - Initialize player → `pc_authok()` (Line ~1000+)
   - Load player data → `pc_reg_received()`
   - Calculate stats → `status_calc_pc()`
   - Send to map → `pc_setpos()`
   - Send player data to client → `clif_authok()`

### Skill Cast Sequence

```
Client Input → Validation → Requirements → Casting → Effect → Damage
```

**Detailed Flow:**

1. **Client Packet** (`clif.cpp`)
   ```
   clif_parse_UseSkillToId() or clif_parse_UseSkillToPos()
   ```

2. **Skill Request** (`skill.cpp`)
   ```
   skill_use_id() / skill_use_pos()
   ├─> skill_check_condition()  // Check requirements
   │   ├─> pc_checkskill()      // Has skill?
   │   ├─> Check SP/HP cost
   │   ├─> Check item requirements
   │   └─> Check state (mounted, etc.)
   ├─> unit_skilluse_id()       // Start casting
   ├─> skill_castend_id()       // Finish cast (timer)
   └─> skill_attack()           // Deal damage
   ```

3. **Damage Calculation** (`battle.cpp`)
   ```
   battle_calc_attack()
   ├─> battle_calc_weapon_attack()  // Physical
   │   ├─> status_base_atk()
   │   ├─> status_calc_watk()
   │   └─> battle_attr_fix()        // Element
   ├─> battle_calc_magic_attack()   // Magic
   └─> battle_calc_misc_attack()    // Misc
   ```

4. **Apply Damage** (`battle.cpp`, `mob.cpp`/`pc.cpp`)
   ```
   battle_damage()
   ├─> If target is PC: pc_damage()
   ├─> If target is MOB: mob_damage()
   └─> clif_damage()  // Show to client
   ```

5. **Death Handling**
   ```
   If HP <= 0:
   ├─> pc_dead() / mob_dead()
   ├─> Drop items (mob_drop_item)
   ├─> Calculate EXP (mob_dead → pc_gainexp)
   └─> Respawn (mob_spawn) or Return to save point
   ```

### Item Use Sequence

```
Use Item → Check Conditions → Run Script → Apply Effects → Update Client
```

**Detailed Flow:**

1. **Client Request** (`clif.cpp`)
   ```
   clif_parse_UseItem(fd, sd, packet)
   ```

2. **Item Usage** (`pc.cpp`)
   ```
   pc_useitem()
   ├─> itemdb_exists()        // Item exists?
   ├─> Check requirements     // Level, job, etc.
   ├─> pc_delitem()          // Remove from inventory
   ├─> script_run()          // Run item script
   └─> clif_useitemack()     // Confirm to client
   ```

3. **Item Script Execution** (`script.cpp`)
   ```
   run_script(item->script, 0, sd->bl.id, 0)
   ├─> Example: percentheal(50, 50)  // Heal 50% HP/SP
   ├─> sc_start() // Apply status
   └─> Other effects
   ```

### Monster AI Cycle

```
Think Timer → Evaluate State → Choose Action → Execute → Repeat
```

**Detailed Flow:**

1. **AI Timer** (`mob.cpp`)
   ```
   mobai_sub_hard_timer()  // Every MIN_MOBTHINKTIME (100ms)
   ├─> mob_ai_sub_hard(md)
   └─> For each mob on map
   ```

2. **AI State Machine** (`mob.cpp`)
   ```
   mob_ai_sub_hard(md)
   ├─> Check state (IDLE, WALK, ATTACK, DEAD, etc.)
   ├─> mob_ai_sub_hard_activesearch()  // Look for targets
   ├─> mob_ai_sub_hard_slavemob()      // Handle slaves
   ├─> mob_ai_sub_hard_lootsearch()    // Look for loot
   ├─> Decision making:
   │   ├─> Attack target?
   │   ├─> Use skill?
   │   ├─> Move/Chase?
   │   └─> Return to spawn?
   └─> Execute action
   ```

3. **Mob Skill Usage** (`mob.cpp`)
   ```
   mob_skill_use()
   ├─> Check conditions (HP%, state, distance)
   ├─> Calculate skill success rate
   ├─> unit_skilluse_id()/unit_skilluse_pos()
   └─> Apply skill effects
   ```

### Party EXP Share

```
Monster Death → Calculate EXP → Distribute to Party → Update Members
```

**Detailed Flow:**

1. **Monster Death** (`mob.cpp`)
   ```
   mob_dead(md, src)
   ├─> Calculate base/job EXP
   ├─> party_exp_share()  // If in party
   └─> pc_gainexp()       // If solo
   ```

2. **Party Distribution** (`party.cpp`)
   ```
   party_exp_share(p, src, base_exp, job_exp)
   ├─> Count eligible members (in range, alive)
   ├─> Apply bonuses (party bonus)
   ├─> For each member:
   │   ├─> Calculate share
   │   ├─> pc_gainexp(sd, base, job)
   │   └─> clif_updatestatus()  // Show EXP gain
   └─> Handle overflow
   ```

---

## Include Hierarchy

### Common Include Pattern

**Top Level:** `map/*.cpp` files

**Include Order:**
1. Own header (e.g., `pc.cpp` includes `pc.hpp`)
2. C/C++ standard libraries
3. Common headers (`<common/...>`)
4. Map server headers (local)

**Example from pc.cpp (Lines 4-66):**

```cpp
#include "pc.hpp"                    // 1. Own header

#include <cmath>                     // 2. C++ standard
#include <cstdlib>
#include <map>

#include <common/cbasetypes.hpp>    // 3. Common libs
#include <common/database.hpp>
#include <common/mmo.hpp>
#include <common/nullpo.hpp>
#include <common/random.hpp>
#include <common/showmsg.hpp>
#include <common/socket.hpp>
#include <common/timer.hpp>

#include "achievement.hpp"           // 4. Map server headers
#include "atcommand.hpp"
#include "battle.hpp"
#include "clif.hpp"
#include "guild.hpp"
#include "itemdb.hpp"
#include "mob.hpp"
#include "npc.hpp"
#include "party.hpp"
#include "skill.hpp"
#include "status.hpp"
#include "unit.hpp"
```

### Core Dependencies

**Base Types:** `common/cbasetypes.hpp`
- Defines: `uint8`, `uint16`, `uint32`, `uint64`, `int8`, `int16`, `int32`, `int64`
- Platform-specific size checks
- Boolean type definitions

**MMO Core:** `common/mmo.hpp`
- Game constants (MAX_INVENTORY, MAX_SKILL, etc.)
- Structure definitions (mmo_charstatus, item, etc.)
- Limits and boundaries

**Database:** `common/database.hpp`
- YAML database base classes
- TypesafeYamlDatabase template
- Database loading/parsing

**Network:** `common/socket.hpp`
- Socket management
- Session handling
- Packet buffers

**Memory:** `common/malloc.hpp`, `common/ers.hpp`
- Memory allocation wrappers
- Entry Reusage System (object pools)
- Memory debugging support

### Forward Declarations

Many headers use forward declarations to reduce compile dependencies:

**Example from map.hpp:**
```cpp
struct chat_data;
struct homun_data;
struct mob_data;
struct npc_data;
struct pet_data;
struct skill_unit;
struct item_data;
struct s_elemental_data;
struct s_mercenary_data;
struct Channel;
```

This allows including `map.hpp` without pulling in all dependent headers.

---

## Build System (CMake)

### Root CMakeLists.txt

**Location:** `/home/user/rathena2/CMakeLists.txt`

**Key Settings:**
- C++17 standard (Line 31: `set(CMAKE_CXX_STANDARD 17)`)
- Architecture detection (x86/x64)
- Build type: Release/Debug/RelWithDebInfo/MinSizeRel
- Packet version: `PACKETVER` (Line 118-121)

**Global Options:**
```cmake
# Enable web server (default: ON)
option( ENABLE_WEB_SERVER "Build web-server" ON )

# Enable extra debug code
option( ENABLE_EXTRA_DEBUG_CODE "enable extra debug code" OFF )

# Memory manager
set( ENABLE_MEMMGR "default" )  # default/yes/no

# Build type
set( CMAKE_BUILD_TYPE "Release" )  # Release/Debug/RelWithDebInfo
```

**Third-party Dependencies (Line 104-112):**
```cmake
set( CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/3rdparty/cmake )
include( CheckCSourceCompiles )
include( CheckCSourceRuns )
include( CheckIncludeFile )
include( CheckFunctionExists )
include( FindFunctionLibrary )
include( TestBigEndian )
```

**Subdirectories (Line 627-628):**
```cmake
add_subdirectory( 3rdparty )  # External libraries
add_subdirectory( src )       # Source code
```

### Source CMakeLists.txt

**Location:** `/home/user/rathena2/src/CMakeLists.txt`

```cmake
add_subdirectory( common )   # Common library
add_subdirectory( login )    # Login server
add_subdirectory( char )     # Char server
add_subdirectory( map )      # Map server
add_subdirectory( web )      # Web server
add_subdirectory( tool )     # Tools
```

### Map Server Build

**Location:** `/home/user/rathena2/src/map/CMakeLists.txt`

**Build Process:**
1. Compile common library first
2. Compile map server sources
3. Link with:
   - common (static library)
   - MySQL library
   - YAML library
   - PCRE library
   - zlib

**Output:** `map-server` (or `map-server.exe` on Windows)

### Typical Build Commands

```bash
# Create build directory
mkdir build && cd build

# Configure with CMake
cmake -G"Unix Makefiles" \
  -DCMAKE_BUILD_TYPE=RelWithDebInfo \
  -DINSTALL_TO_SOURCE=ON \
  -DPACKETVER=20211103 \
  ..

# Build
make -j4

# Install
make install
```

### Build Targets

```bash
make common         # Build common library only
make login-server   # Build login server
make char-server    # Build char server
make map-server     # Build map server
make web-server     # Build web server
make all            # Build everything
```

### Compile-time Options

**PACKETVER:** Client version compatibility
```cmake
-DPACKETVER=20211103  # 2021-11-03 client
```

**Renewal Mode:** `src/config/renewal.hpp`
```cpp
#define RENEWAL           // Enable renewal mechanics
#define RENEWAL_CAST      // Renewal casting
#define RENEWAL_DROP      // Renewal drop rates
#define RENEWAL_EXP       // Renewal EXP rates
#define RENEWAL_LVDMG     // Renewal level damage
#define RENEWAL_ASPD      // Renewal ASPD
```

**Security:** `src/config/secure.hpp`
```cpp
#define SECURE_NPCTIMEOUT 10000   // NPC timeout (ms)
#define PACKET_OBFUSCATION        // Packet obfuscation
```

---

## Feature Location Guide

### Where to Find Specific Features

#### Player Systems

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Login** | pc.cpp, chrif.cpp | `pc_authok()`, `chrif_authok()` |
| **Inventory** | pc.cpp | `pc_additem()`, `pc_delitem()`, `pc_dropitem()` |
| **Equipment** | pc.cpp | `pc_equipitem()`, `pc_unequipitem()` |
| **Stats Calculation** | status.cpp, pc.cpp | `status_calc_pc()`, `status_calc_*()` |
| **Job System** | pc.cpp | `pc_jobchange()`, `pc_calc_skilltree()` |
| **Skills** | skill.cpp, pc.cpp | `skill_use_id()`, `pc_checkskill()` |
| **Experience** | pc.cpp | `pc_gainexp()`, `pc_nextbaseexp()` |
| **Death** | pc.cpp | `pc_dead()`, `pc_setrestartvalue()` |
| **Regeneration** | status.cpp | `status_calc_regen()` |

#### Combat Systems

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Physical Damage** | battle.cpp | `battle_calc_weapon_attack()` |
| **Magic Damage** | battle.cpp | `battle_calc_magic_attack()` |
| **Element System** | battle.cpp | `battle_attr_fix()` |
| **Critical** | battle.cpp | `battle_calc_critical()` |
| **Defense Calc** | battle.cpp | `battle_calc_defense()` |
| **ASPD** | status.cpp | `status_calc_aspd()` |
| **HIT/FLEE** | status.cpp | `status_calc_hit()`, `status_calc_flee()` |

#### Monster Systems

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Spawning** | mob.cpp, npc.cpp | `mob_spawn()`, `mob_parse_dataset()` |
| **AI** | mob.cpp | `mob_ai_sub_hard()`, `mobai_sub_hard_timer()` |
| **Skills** | mob.cpp | `mob_skill_use()`, `mob_skill_event()` |
| **Drops** | mob.cpp | `mob_drop_item()`, `mob_setdropitem()` |
| **MVP** | mob.cpp | `mob_damage()` (MVP calculation) |
| **Slave/Master** | mob.cpp | `mob_ai_sub_hard_slavemob()` |

#### Item Systems

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Item Database** | itemdb.cpp | `itemdb_search()`, `itemdb_exists()` |
| **Item Use** | pc.cpp, script.cpp | `pc_useitem()`, item scripts |
| **Item Scripts** | script.cpp | Item bonus functions |
| **Refining** | status.cpp, script.cpp | refine_db, `refine_status()` |
| **Cards** | pc.cpp, status.cpp | Card bonus calculations |
| **Random Options** | itemdb.cpp, status.cpp | Random option system |

#### Skill Systems

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Skill Database** | skill.cpp | SkillDatabase class |
| **Skill Casting** | skill.cpp | `skill_castend_id()`, `skill_castend_pos()` |
| **Ground Skills** | skill.cpp | `skill_unitsetting()`, `skill_unit_onplace()` |
| **Skill Combos** | pc.cpp, skill.cpp | Combo system |
| **Skill Tree** | pc.cpp | `pc_calc_skilltree()` |
| **Skill Requirements** | skill.cpp | `skill_check_condition()` |
| **Class Skills** | src/map/skills/*/  | Individual skill implementations |

#### Status Effects

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Start Effect** | status.cpp | `status_change_start()` |
| **End Effect** | status.cpp | `status_change_end()` |
| **Timer** | status.cpp | `status_change_timer()` |
| **Icons** | clif.cpp | `clif_status_change()` |
| **Resistance** | status.cpp | SC resistance calculations |

#### Social Systems

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Party** | party.cpp | `party_create()`, `party_invite()` |
| **Guild** | guild.cpp | `guild_create()`, `guild_invite()` |
| **Chat** | chat.cpp | `chat_createpcchat()` |
| **Friends** | clif.cpp, pc.cpp | Friend list functions |
| **Mail** | mail.cpp | `mail_sendmail()`, `mail_getmail()` |

#### Map/Movement

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **Walking** | unit.cpp | `unit_walktoxy()`, `unit_movepos()` |
| **Pathfinding** | path.cpp | `path_search()` |
| **Warp** | unit.cpp, pc.cpp | `unit_warp()`, `pc_setpos()` |
| **Map Loading** | map.cpp | `map_readgat()`, `map_waterheight()` |

#### NPC Systems

| Feature | Primary File(s) | Key Functions |
|---------|----------------|---------------|
| **NPC Scripts** | npc.cpp, script.cpp | `npc_parse_script()`, `run_script()` |
| **Shops** | npc.cpp | `npc_parse_shop()`, `npc_buylist()` |
| **Warps** | npc.cpp | `npc_parse_warp()` |
| **Events** | npc.cpp | `npc_event()`, `npc_event_do()` |
| **Timers** | npc.cpp | `npc_timerevent()` |

#### Database Files (YAML)

| Database | Location | Loaded By |
|----------|----------|-----------|
| **Items** | db/item_db.yml | itemdb.cpp |
| **Mobs** | db/mob_db.yml | mob.cpp |
| **Skills** | db/skill_db.yml | skill.cpp |
| **Refine** | db/refine_db.yml | status.cpp |
| **Job Stats** | db/job_db.yml | pc.cpp |
| **Experience** | db/exp_group_db.yml | pc.cpp |
| **Status Effects** | db/sc_config.yml | status.cpp |

---

## Navigation Quick Reference

### Finding Code by Feature

**Q: "Where is damage calculation?"**
- **A:** `src/map/battle.cpp` → `battle_calc_attack()`
  - Physical: `battle_calc_weapon_attack()`
  - Magic: `battle_calc_magic_attack()`
  - Element: `battle_attr_fix()`

**Q: "Where is player stat calculation?"**
- **A:** `src/map/status.cpp` → `status_calc_pc()`
  - Individual stats: `status_calc_str()`, `status_calc_agi()`, etc.
  - ATK: `status_base_atk()`, `status_calc_watk()`
  - MATK: `status_calc_matk()`
  - DEF: `status_calc_def()`, `status_calc_def2()`

**Q: "Where is skill casting handled?"**
- **A:** `src/map/skill.cpp`
  - Request: `skill_use_id()`, `skill_use_pos()`
  - Requirements: `skill_check_condition()`
  - Casting: `skill_castend_id()`, `skill_castend_pos()`
  - Damage: `skill_attack()`

**Q: "Where are packets handled?"**
- **A:** `src/map/clif.cpp`
  - Parser: `clif_parse()` (main switch)
  - Individual handlers: `clif_parse_*()` functions
  - Sending: `clif_send()`, specific `clif_*()` functions

**Q: "Where is monster AI?"**
- **A:** `src/map/mob.cpp`
  - Main AI: `mob_ai_sub_hard()`
  - Timer: `mobai_sub_hard_timer()`
  - Skills: `mob_skill_use()`
  - Movement: Uses `unit.cpp` functions

**Q: "Where are NPC scripts parsed?"**
- **A:** `src/map/npc.cpp` (parsing) + `src/map/script.cpp` (execution)
  - Parse: `npc_parse_script()`
  - Execute: `run_script()`
  - Built-in functions: `BUILDIN(funcname)` macros

**Q: "Where is inventory management?"**
- **A:** `src/map/pc.cpp`
  - Add item: `pc_additem()`
  - Remove item: `pc_delitem()`
  - Drop item: `pc_dropitem()`
  - Pick up: `pc_takeitem()`
  - Equipment: `pc_equipitem()`, `pc_unequipitem()`

**Q: "Where is the item database?"**
- **A:** `src/map/itemdb.cpp/hpp`
  - Database class: `ItemDatabase`
  - Search: `itemdb_search()`, `itemdb_searchname()`
  - Properties: `itemdb_type()`, `itemdb_weight()`, etc.

### File Size as Complexity Indicator

**Largest Files (Most Complex):**
1. script.cpp (28,574 lines) - Script engine, 500+ builtin functions
2. skill.cpp (26,478 lines) - All skill mechanics
3. clif.cpp (25,821 lines) - All packet handling
4. status.cpp (16,480 lines) - Stat calculations, status effects
5. pc.cpp (16,102 lines) - Player character logic
6. battle.cpp (12,680 lines) - Battle formulas

**Tip:** Start with smaller, focused files when learning:
- path.cpp (pathfinding) - focused, algorithmic
- date.cpp (day/night) - simple
- duel.cpp (duel system) - small feature
- channel.cpp (chat channels) - medium complexity

### Common Patterns

**1. Object Retrieval by ID:**
```cpp
map_session_data *sd = map_id2sd(id);  // Player
mob_data *md = map_id2md(id);          // Monster
npc_data *nd = map_id2nd(id);          // NPC
block_list *bl = map_id2bl(id);        // Any object
```

**2. Null Safety:**
```cpp
nullpo_ret(sd);          // Return if NULL
nullpo_retr(val, sd);    // Return val if NULL
nullpo_retv(sd);         // Return void if NULL
nullpo_retb(sd);         // Return false if NULL
```

**3. Type Checking:**
```cpp
if (bl->type == BL_PC) {
    map_session_data *sd = (map_session_data *)bl;
}
```

**4. Area Iteration:**
```cpp
map_foreachinrange(function, center, range, type, ...args);
map_foreachinarea(function, m, x0, y0, x1, y1, type, ...args);
```

**5. Timer Management:**
```cpp
int tid = add_timer(gettick() + delay, function, id, data);
delete_timer(tid, function);
```

**6. Script Execution:**
```cpp
run_script(script, 0, sd->bl.id, 0);
```

---

## Code Examples

### Example 1: Player Stats Calculation Flow

**File:** `src/map/status.cpp`

**Main Function:** `status_calc_pc()` - Calculates all player stats

```cpp
// Called when:
// - Player logs in
// - Equipment changes
// - Status effect starts/ends
// - Job changes
// - Stats are reset/modified

int status_calc_pc_(map_session_data* sd, enum e_status_calc_opt opt) {
    // 1. Clear calculated stats
    memset(&sd->battle_status, 0, sizeof(status_data));

    // 2. Copy base stats
    sd->battle_status = sd->base_status;

    // 3. Calculate from equipment
    for (int i = 0; i < EQI_MAX; i++) {
        if (sd->equip_index[i] >= 0) {
            // Apply equipment bonuses
            run_script(item->script, 0, sd->bl.id, 0);
        }
    }

    // 4. Calculate individual stats
    status_calc_str(&sd->bl, &sd->sc, sd->battle_status.str);
    status_calc_agi(&sd->bl, &sd->sc, sd->battle_status.agi);
    // ... more stats

    // 5. Calculate combat stats
    status_calc_batk(&sd->bl, &sd->sc, sd->battle_status.batk);
    status_calc_watk(&sd->bl, &sd->sc, sd->battle_status.watk);
    status_calc_matk(&sd->bl, &sd->sc, sd->battle_status.matk);

    // 6. Apply status change modifiers
    status_calc_pc_additional(sd, opt);

    // 7. Send updates to client
    clif_updatestatus(sd, SP_STR);
    clif_updatestatus(sd, SP_ATK1);
    // ... more updates

    return 0;
}
```

### Example 2: Skill Damage Calculation

**File:** `src/map/skill.cpp` → `src/map/battle.cpp`

```cpp
// In skill.cpp
int skill_attack(int attack_type, block_list* src, block_list *dsrc,
                 block_list *bl, uint16 skill_id, uint16 skill_lv,
                 t_tick tick, int flag) {

    // 1. Calculate damage
    struct Damage dmg = battle_calc_attack(
        attack_type, src, bl, skill_id, skill_lv, flag
    );

    // 2. Apply damage
    if (dmg.damage > 0) {
        clif_skill_damage(dsrc, bl, tick, dmg.amotion, dmg.dmotion,
                         dmg.damage, dmg.div_, skill_id, skill_lv,
                         dmg.type);

        battle_damage(src, bl, dmg.damage, 0, 0);
    }

    // 3. Apply additional effects
    if (dmg.dmg_lv > ATK_BLOCK) {
        skill_additional_effect(src, bl, skill_id, skill_lv,
                               attack_type, dmg.dmg_lv, tick);
    }

    return dmg.damage;
}
```

### Example 3: Monster AI Decision Making

**File:** `src/map/mob.cpp`

```cpp
// Main AI function (simplified)
static int mob_ai_sub_hard(struct mob_data *md, t_tick tick) {
    // 1. Check if can move/act
    if (md->ud.skilltimer != INVALID_TIMER)
        return 0;  // Casting skill

    if (md->ud.walktimer != INVALID_TIMER)
        return 0;  // Moving

    // 2. Search for target
    if (!md->target_id) {
        mob_ai_sub_hard_activesearch(&md->bl, tick);
    }

    // 3. Get target
    block_list *tbl = map_id2bl(md->target_id);
    if (!tbl) {
        md->target_id = 0;
        return 0;
    }

    // 4. Check if should use skill
    if (mob_skill_use(md, tick, MSS_ANY)) {
        return 0;  // Used skill
    }

    // 5. Distance check
    int distance = distance_bl(&md->bl, tbl);

    // 6. Attack or chase
    if (distance <= md->status.rhw.range) {
        // In attack range - attack
        if (unit_attack(&md->bl, tbl->id, 0)) {
            return 0;
        }
    } else {
        // Out of range - chase
        if (unit_walktoxy(&md->bl, tbl->x, tbl->y, 0)) {
            return 0;
        }
    }

    return 0;
}
```

### Example 4: Packet Handling

**File:** `src/map/clif.cpp`

```cpp
/// Request to use item (CZ_USE_ITEM)
void clif_parse_UseItem(int fd, map_session_data *sd) {
    // 1. Read packet
    const PACKET_CZ_USE_ITEM *p = (PACKET_CZ_USE_ITEM *)RFIFOP(fd,0);

    uint16 index = p->index - 2;

    // 2. Validate
    if (index >= MAX_INVENTORY)
        return;

    if (!sd->inventory_data[index])
        return;

    // 3. Check conditions
    if (sd->npc_id || sd->state.storage_flag)
        return;

    if (sd->sc.cant.useitem)
        return;

    // 4. Use item
    if (!pc_useitem(sd, index))
        clif_useitemack(sd, index, 0, false);  // Failed
}

/// Send item use acknowledgement (ZC_USE_ITEM_ACK)
void clif_useitemack(map_session_data *sd, uint16 index, uint16 amount,
                     bool ok) {
    int fd = sd->fd;

    WFIFOHEAD(fd, packet_len(0xa8));
    WFIFOW(fd,0) = 0xa8;
    WFIFOW(fd,2) = index + 2;
    WFIFOW(fd,4) = amount;
    WFIFOB(fd,6) = ok;
    WFIFOSET(fd, packet_len(0xa8));
}
```

### Example 5: NPC Script Execution

**File:** `src/map/script.cpp`

```cpp
/// Built-in function: getitem
/// getitem <item id>, <amount>{, <account id>}
BUILDIN(getitem) {
    int nameid, amount;
    map_session_data *sd;
    struct item it;

    // 1. Get parameters
    if (script_isstringtype(st, 2)) {
        const char *name = script_getstr(st, 2);
        struct item_data *id = itemdb_searchname(name);
        nameid = id ? id->nameid : 0;
    } else {
        nameid = script_getnum(st, 2);
    }

    amount = script_getnum(st, 3);

    // 2. Get target player
    if (!script_accid2sd(4, sd))
        return SCRIPT_CMD_FAILURE;

    // 3. Validate
    if (nameid <= 0 || amount <= 0)
        return SCRIPT_CMD_FAILURE;

    // 4. Create item
    memset(&it, 0, sizeof(it));
    it.nameid = nameid;
    it.identify = 1;

    // 5. Add to inventory
    if ((flag = pc_additem(sd, &it, amount, LOG_TYPE_SCRIPT))) {
        clif_additem(sd, 0, 0, flag);
        if (pc_candrop(sd, &it))
            map_addflooritem(&it, amount, sd->bl.m,
                           sd->bl.x, sd->bl.y, 0, 0, 0, 0, 0);
    }

    return SCRIPT_CMD_SUCCESS;
}
```

### Example 6: Status Effect Application

**File:** `src/map/status.cpp`

```cpp
// Start a status change
int status_change_start(block_list *src, block_list *bl,
                       enum sc_type type, int rate, int val1,
                       int val2, int val3, int val4,
                       int tick, int flag) {

    status_change *sc = status_get_sc(bl);
    if (!sc) return 0;

    // 1. Check if can apply
    if (sc->data[type])
        return 0;  // Already has effect

    // 2. Calculate success rate
    if (rate < 10000) {
        rate = max(rate, 100);  // Min 1% success
        if (rnd()%10000 >= rate)
            return 0;  // Failed
    }

    // 3. Calculate duration
    tick = status_get_sc_tick(bl, src, type, tick);

    // 4. Create status data
    sc->data[type] = ers_alloc(sc_data_ers, struct status_change_entry);
    sc->data[type]->val1 = val1;
    sc->data[type]->val2 = val2;
    sc->data[type]->val3 = val3;
    sc->data[type]->val4 = val4;
    sc->data[type]->timer = add_timer(gettick() + tick,
                                      status_change_timer,
                                      bl->id, type);

    // 5. Apply effect
    status_calc_bl_(bl, SCB_ALL);  // Recalculate stats

    // 6. Send to client
    clif_status_change(bl, status_sc2icon(type), 1, tick,
                      val1, val2, val3);

    // 7. Call start function
    if (status_sc_start_func[type])
        status_sc_start_func[type](bl, sc, type);

    return 1;
}
```

---

## Quick Reference Tables

### Object Type Conversion Functions

| From → To | Function | Example |
|-----------|----------|---------|
| ID → block_list | `map_id2bl(id)` | `bl = map_id2bl(target_id)` |
| ID → Player | `map_id2sd(id)` | `sd = map_id2sd(char_id)` |
| ID → Mob | `map_id2md(id)` | `md = map_id2md(mob_id)` |
| ID → NPC | `map_id2nd(id)` | `nd = map_id2nd(npc_id)` |
| ID → Pet | `map_id2pd(id)` | `pd = map_id2pd(pet_id)` |
| bl → Player | `BL_CAST(BL_PC, bl)` | `sd = BL_CAST(BL_PC, bl)` |
| bl → Mob | `BL_CAST(BL_MOB, bl)` | `md = BL_CAST(BL_MOB, bl)` |

### Common Status Parameters (SP_*)

| Constant | Value | Description |
|----------|-------|-------------|
| SP_HP | 5 | Current HP |
| SP_MAXHP | 6 | Maximum HP |
| SP_SP | 7 | Current SP |
| SP_MAXSP | 8 | Maximum SP |
| SP_BASELEVEL | 11 | Base level |
| SP_JOBLEVEL | 55 | Job level |
| SP_STR | 13 | Strength |
| SP_AGI | 14 | Agility |
| SP_VIT | 15 | Vitality |
| SP_INT | 16 | Intelligence |
| SP_DEX | 17 | Dexterity |
| SP_LUK | 18 | Luck |
| SP_ZENY | 20 | Zeny |

### Skill Constants

| Constant | Value | Description |
|----------|-------|-------------|
| INF_ATTACK_SKILL | 0x01 | Attack skill |
| INF_GROUND_SKILL | 0x02 | Ground-targeted |
| INF_SELF_SKILL | 0x04 | Self-cast |
| INF_SUPPORT_SKILL | 0x10 | Support skill |
| INF_TRAP_SKILL | 0x20 | Trap skill |
| NK_SPLASH | 1 | Splash damage |
| NK_NODAMAGE | 0 | No damage |

### Battle Configuration

**Location:** `battle_config` global variable in `battle.cpp`

Common settings:
- `base_exp_rate` - Base EXP rate
- `job_exp_rate` - Job EXP rate
- `item_rate_common` - Common drop rate
- `max_hp` - Maximum HP
- `max_sp` - Maximum SP
- `max_parameter` - Maximum stat value

---

## Summary

This document provides a comprehensive reference for navigating the rAthena source code. Key takeaways:

1. **Directory Structure:** Map server (`src/map/`) contains game logic, with specialized subdirectories for skills
2. **Core Files:** script.cpp, skill.cpp, clif.cpp, status.cpp, pc.cpp, battle.cpp are the largest and most complex
3. **Data Structures:** `block_list` is the base for all objects, `map_session_data` for players, `mob_data` for monsters
4. **Build System:** CMake-based with configurable options (PACKETVER, RENEWAL, etc.)
5. **Code Flow:** Understanding the data flow between systems (login → char → map) is essential
6. **Feature Location:** Use the Feature Location Guide to quickly find specific functionality

**Next Steps for Developers:**
- Start with smaller files to understand patterns
- Trace a feature end-to-end (e.g., item use: clif.cpp → pc.cpp → script.cpp)
- Use forward declarations and include hierarchy to understand dependencies
- Refer to Quick Reference for common functions and constants

**File Locations:**
- Source code: `/home/user/rathena2/src/`
- Build system: `/home/user/rathena2/CMakeLists.txt`
- Common library: `/home/user/rathena2/src/common/`
- Map server: `/home/user/rathena2/src/map/`

---

*Document Version: 1.0*
*rAthena Source Analysis Date: 2025-11-18*
*Total Lines Analyzed: ~200,000+ across all source files*
