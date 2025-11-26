---
title: rAthena Source Data Structures Reference
type: source_reference
category: rathena_development
tags: [struct, enum, source, cpp, hpp, data_structures]
version: 2.0
mode: SRC
chunk_strategy: BY_DEFINITION
---

# rAthena Source Data Structures Reference

This KB provides C++ struct and enum definitions from rAthena header files.

**Search:** Use struct/enum name directly (e.g., `map_session_data`, `equip_index`).

---

# Script Engine Structures (script.hpp)

## Script Macros

### Stack Access Macros
```cpp
// Get script_data at index
#define script_getdata(st,i) ( &((st)->stack->stack_data[(st)->start + (i)]) )

// Check if stack has data at index
#define script_hasdata(st,i) ( (st)->end > (st)->start + (i) )

// Get last data index
#define script_lastdata(st) ( (st)->end - (st)->start - 1 )

// Push values to stack
#define script_pushint(st,val) push_val((st)->stack, C_INT, (val))
#define script_pushint64(st,val) push_val2((st)->stack, C_INT, val, nullptr)
#define script_pushstr(st,val) push_str((st)->stack, C_STR, (val))
#define script_pushstrcopy(st,val) push_str((st)->stack, C_STR, aStrdup(val))
#define script_pushconststr(st,val) push_str((st)->stack, C_CONSTSTR, const_cast<char*>(val))
#define script_pushnil(st) push_val((st)->stack, C_NOP, 0)
```

### Type Check Macros
```cpp
#define script_isstring(st,i) data_isstring(get_val(st, script_getdata(st,i)))
#define script_isint(st,i) data_isint(get_val(st, script_getdata(st,i)))

#define script_getnum(st,val) conv_num(st, script_getdata(st,val))
#define script_getnum64(st,val) conv_num64(st, script_getdata(st,val))
#define script_getstr(st,val) conv_str(st, script_getdata(st,val))
```

### Reference Macros
```cpp
#define reference_getuid(data) ( (data)->u.num )
#define reference_getid(data) ( (int32)(int64)(reference_getuid(data) & 0xffffffff) )
#define reference_getindex(data) ( (uint32)(int64)((reference_getuid(data) >> 32) & 0xffffffff) )
#define reference_getname(data) ( str_buf + str_data[reference_getid(data)].str )
```

### Variable Macros
```cpp
#define not_server_variable(prefix) ( (prefix) != '$' && (prefix) != '.' && (prefix) != '\'')
#define is_string_variable(name) ( (name)[strlen(name) - 1] == '$' )
#define SCRIPT_MAX_ARRAYSIZE (UINT_MAX - 1)
```

---

## enum c_op (Script Operators)

```cpp
typedef enum c_op {
    C_NOP,          // end of script/no value (nil)
    C_POS,          // position/label
    C_INT,          // number
    C_PARAM,        // parameter variable (pc_readparam/pc_setparam)
    C_FUNC,         // buildin function call
    C_STR,          // string (freed automatically)
    C_CONSTSTR,     // string (not freed)
    C_ARG,          // start of argument list
    C_NAME,         // variable name
    C_EOL,          // end of line
    C_RETINFO,      // return info
    C_USERFUNC,     // internal script function
    C_USERFUNC_POS, // internal script function label
    C_REF,          // reference for c_op2

    // Operators
    C_OP3,          // a ? b : c (ternary)
    C_LOR,          // a || b
    C_LAND,         // a && b
    C_LE,           // a <= b
    C_LT,           // a < b
    C_GE,           // a >= b
    C_GT,           // a > b
    C_EQ,           // a == b
    C_NE,           // a != b
    C_XOR,          // a ^ b
    C_OR,           // a | b
    C_AND,          // a & b
    C_ADD,          // a + b
    C_SUB,          // a - b
    C_MUL,          // a * b
    C_DIV,          // a / b
    C_MOD,          // a % b
    C_NEG,          // -a
    C_LNOT,         // !a
    C_NOT,          // ~a
    C_R_SHIFT,      // a >> b
    C_L_SHIFT,      // a << b
    C_ADD_POST,     // a++
    C_SUB_POST,     // a--
    C_ADD_PRE,      // ++a
    C_SUB_PRE,      // --a
} c_op;
```

---

## enum script_cmd_result

```cpp
enum script_cmd_result {
    SCRIPT_CMD_SUCCESS = 0,  // buildin cmd completed successfully
    SCRIPT_CMD_FAILURE = 1,  // error in cmd, show_debug follows
};
```

---

## struct Script_Config

```cpp
struct Script_Config {
    unsigned warn_func_mismatch_argtypes : 1;
    unsigned warn_func_mismatch_paramnum : 1;
    int32 check_cmdcount;
    int32 check_gotocount;
    int32 input_min_value;
    int32 input_max_value;

    // PC events
    const char *die_event_name;           // OnPCDieEvent
    const char *kill_pc_event_name;       // OnPCKillEvent
    const char *kill_mob_event_name;      // OnNPCKillEvent
    const char *login_event_name;         // OnPCLoginEvent
    const char *logout_event_name;        // OnPCLogoutEvent
    const char *loadmap_event_name;       // OnPCLoadMapEvent
    const char *baselvup_event_name;      // OnPCBaseLvUpEvent
    const char *joblvup_event_name;       // OnPCJobLvUpEvent

    // NPC events
    const char *ontouch_event_name;       // OnTouch
    const char *ontouch2_event_name;      // OnTouch2
    const char *ontouchnpc_event_name;    // OnTouchNPC
    const char *onwhisper_event_name;     // OnWhisperGlobal
    const char *oncommand_event_name;     // OnCommand
    const char *onbuy_event_name;         // OnBuyItem
    const char *onsell_event_name;        // OnSellItem

    // Init events
    const char *init_event_name;          // OnInit
    const char *inter_init_event_name;    // OnInterIfInit
    const char *inter_init_once_event_name; // OnInterIfInitOnce

    // Timer events
    const char *timer_event_name;         // OnTimer
    const char *timer_quit_event_name;    // OnTimerQuit
    const char *timer_minute_event_name;  // OnMinute
    const char *timer_hour_event_name;    // OnHour
    const char *timer_clock_event_name;   // OnClock
    const char *timer_day_event_name;     // OnDay

    // Instance events
    const char *instance_init_event_name;
    const char *instance_destroy_event_name;
};
```

---

# Player Structures (pc.hpp)

## enum equip_index

```cpp
enum equip_index {
    EQI_COMPOUND_ON = -1,  // Compound on
    EQI_ACC_L = 0,         // Accessory Left
    EQI_ACC_R,             // Accessory Right
    EQI_SHOES,             // Shoes
    EQI_GARMENT,           // Garment
    EQI_HEAD_LOW,          // Lower Headgear
    EQI_HEAD_MID,          // Middle Headgear
    EQI_HEAD_TOP,          // Upper Headgear
    EQI_ARMOR,             // Armor
    EQI_HAND_L,            // Left Hand (Shield)
    EQI_HAND_R,            // Right Hand (Weapon)
    EQI_COSTUME_HEAD_TOP,  // Costume Upper
    EQI_COSTUME_HEAD_MID,  // Costume Middle
    EQI_COSTUME_HEAD_LOW,  // Costume Lower
    EQI_COSTUME_GARMENT,   // Costume Garment
    EQI_AMMO,              // Ammunition
    EQI_SHADOW_ARMOR,      // Shadow Armor
    EQI_SHADOW_WEAPON,     // Shadow Weapon
    EQI_SHADOW_SHIELD,     // Shadow Shield
    EQI_SHADOW_SHOES,      // Shadow Shoes
    EQI_SHADOW_ACC_R,      // Shadow Accessory Right
    EQI_SHADOW_ACC_L,      // Shadow Accessory Left
    EQI_MAX                // Total equip slots
};
```

---

## enum e_additem_result

```cpp
enum e_additem_result : uint8 {
    ADDITEM_SUCCESS,       // Item added successfully
    ADDITEM_INVALID,       // Invalid item
    ADDITEM_OVERWEIGHT,    // Would exceed weight limit
    ADDITEM_ITEM,          // Item not found
    ADDITEM_OVERITEM,      // Inventory full
    ADDITEM_OVERAMOUNT,    // Amount exceeds limit
    ADDITEM_REFUSED_TIME,  // Pickup delay
    ADDITEM_STACKLIMIT     // Stack limit reached
};
```

---

## enum e_chkitem_result

```cpp
enum e_chkitem_result : uint8 {
    CHKADDITEM_EXIST,      // Item can stack
    CHKADDITEM_NEW,        // New inventory slot needed
    CHKADDITEM_OVERAMOUNT  // Amount exceeds limit
};
```

---

## enum e_params (Stats)

```cpp
enum e_params {
    PARAM_STR = 0,
    PARAM_AGI,
    PARAM_VIT,
    PARAM_INT,
    PARAM_DEX,
    PARAM_LUK,
    // 4th Job Trait Stats
    PARAM_POW,
    PARAM_STA,
    PARAM_WIS,
    PARAM_SPL,
    PARAM_CON,
    PARAM_CRT,
    PARAM_MAX
};
```

---

## struct weapon_data

```cpp
struct weapon_data {
    int32 atkmods[SZ_ALL];           // Size modifiers
    int32 overrefine;                // Overrefine bonus
    int32 star;                      // Star crumb count
    int32 ignore_def_ele;            // Ignore element defense
    int32 ignore_def_race;           // Ignore race defense
    int32 ignore_def_class;          // Ignore class defense
    int32 def_ratio_atk_ele;         // DEF ratio by element
    int32 def_ratio_atk_race;        // DEF ratio by race
    int32 def_ratio_atk_class;       // DEF ratio by class
    int32 addele[ELE_MAX];           // Element damage bonus
    int32 addrace[RC_MAX];           // Race damage bonus
    int32 addclass[CLASS_MAX];       // Class damage bonus
    int32 addrace2[RC2_MAX];         // Monster race bonus
    int32 addsize[SZ_MAX];           // Size damage bonus
    int16 hp_drain_race[RC_MAX];     // HP drain by race
    int16 sp_drain_race[RC_MAX];     // SP drain by race
    int16 hp_drain_class[CLASS_MAX]; // HP drain by class
    int16 sp_drain_class[CLASS_MAX]; // SP drain by class

    struct drain_data {
        int16 rate;  // Success rate 10000 = 100%
        int16 per;   // Drain percent per attack
    } hp_drain_rate, sp_drain_rate;

    std::vector<s_item_bonus> add_dmg;
    std::vector<s_addele2> addele2;
    std::vector<s_addrace2> addrace3;
};
```

---

## struct s_autospell

```cpp
struct s_autospell {
    uint16 id;              // Autospell skill ID
    uint16 lv;              // Skill level
    uint16 trigger_skill;   // Triggering skill ID
    int16 rate;             // Trigger rate
    int16 battle_flag;      // Battle flags (BF_*)
    t_itemid card_id;       // Card that grants this
    uint8 flag;             // Autospell flags
};
```

---

## enum e_autospell_flags

```cpp
enum e_autospell_flags {
    AUTOSPELL_FORCE_SELF = 0x0,         // Cast on self
    AUTOSPELL_FORCE_TARGET = 0x1,       // Cast on target
    AUTOSPELL_FORCE_RANDOM_LEVEL = 0x2, // Random level
    AUTOSPELL_FORCE_ALL = 0x3           // Both target + random
};
```

---

# Status Structures (status.hpp)

## Refine Constants

```cpp
#ifdef RENEWAL
    #define MAX_REFINE 20
#else
    #define MAX_REFINE 10
#endif

#define MIN_ASPD 8000      // Minimum ASPD (max delay)
#define MAX_ASPD_NOPC 100  // Maximum monster ASPD

// Amotion calculations
#define AMOTION_DIVIDER_PC 2     // Player amotion = adelay/2
#define AMOTION_DIVIDER_NOPC 1   // Monster amotion = adelay
#define AMOTION_ZERO_ASPD 2000   // 0 ASPD value
#define AMOTION_INTERVAL 10      // ASPD reduction per point
```

---

## enum e_refine_type

```cpp
enum e_refine_type : uint16 {
    REFINE_TYPE_ARMOR = 0,
    REFINE_TYPE_WEAPON,
    REFINE_TYPE_SHADOW_ARMOR,
    REFINE_TYPE_SHADOW_WEAPON,
    REFINE_TYPE_MAX
};
```

---

## enum e_refine_cost_type

```cpp
enum e_refine_cost_type : uint16 {
    REFINE_COST_NORMAL = 0,
    REFINE_COST_HD,        // HD Ores
    REFINE_COST_ENRICHED,  // Enriched ores
    REFINE_COST_MAX
};
```

---

## struct s_refine_cost

```cpp
struct s_refine_cost {
    uint16 index;
    t_itemid nameid;        // Material item ID
    uint16 chance;          // Success chance
    uint32 zeny;            // Zeny cost
    uint16 breaking_rate;   // Break chance
    uint16 downgrade_amount;// Downgrade on fail
};
```

---

## struct s_sizefix_db

```cpp
struct s_sizefix_db {
    uint16 small;   // Damage vs small
    uint16 medium;  // Damage vs medium
    uint16 large;   // Damage vs large
};
```

---

# Map Structures (map.hpp)

## Block List Types

```cpp
enum bl_type : uint16 {
    BL_NUL   = 0x000,
    BL_PC    = 0x001,  // Player
    BL_MOB   = 0x002,  // Monster
    BL_PET   = 0x004,  // Pet
    BL_HOM   = 0x008,  // Homunculus
    BL_MER   = 0x010,  // Mercenary
    BL_ITEM  = 0x020,  // Ground item
    BL_SKILL = 0x040,  // Skill unit
    BL_NPC   = 0x080,  // NPC
    BL_CHAT  = 0x100,  // Chat room
    BL_ELEM  = 0x200,  // Elemental
    BL_ALL   = 0xFFF,  // All types
};
```

---

## Cell Types

```cpp
enum cell_type : uint8 {
    CELL_WALKABLE    = 0x00,  // Can walk
    CELL_SHOOTABLE   = 0x01,  // Can shoot through
    CELL_WATER       = 0x02,  // Water cell
    CELL_NPC         = 0x04,  // NPC on cell
    CELL_BASILICA    = 0x08,  // Basilica effect
    CELL_LANDPROTECTOR = 0x10, // Land Protector
    CELL_NOVENDING   = 0x20,  // No vending
    CELL_NOCHAT      = 0x40,  // No chatrooms
    CELL_ICEWALL     = 0x80,  // Ice Wall
};
```

---

# Item Structures (itemdb.hpp)

## Item Types

```cpp
enum item_types : uint8 {
    IT_HEALING = 0,    // Healing item
    IT_USABLE,         // Usable item
    IT_ETC,            // Etc item
    IT_ARMOR,          // Armor
    IT_WEAPON,         // Weapon
    IT_CARD,           // Card
    IT_PETEGG,         // Pet egg
    IT_PETARMOR,       // Pet equipment
    IT_AMMO,           // Ammunition
    IT_DELAYCONSUME,   // Delay consume
    IT_SHADOWGEAR,     // Shadow equipment
    IT_CASH = 18,      // Cash shop item
    IT_MAX
};
```

---

## Weapon Types

```cpp
enum weapon_type : uint8 {
    W_FIST,      // Bare fist
    W_DAGGER,    // Daggers
    W_1HSWORD,   // One-handed swords
    W_2HSWORD,   // Two-handed swords
    W_1HSPEAR,   // One-handed spears
    W_2HSPEAR,   // Two-handed spears
    W_1HAXE,     // One-handed axes
    W_2HAXE,     // Two-handed axes
    W_MACE,      // Maces
    W_2HMACE,    // Two-handed maces
    W_STAFF,     // Staves
    W_BOW,       // Bows
    W_KNUCKLE,   // Knuckles
    W_MUSICAL,   // Musical instruments
    W_WHIP,      // Whips
    W_BOOK,      // Books
    W_KATAR,     // Katars
    W_REVOLVER,  // Revolvers
    W_RIFLE,     // Rifles
    W_GATLING,   // Gatling guns
    W_SHOTGUN,   // Shotguns
    W_GRENADE,   // Grenade launchers
    W_HUUMA,     // Huuma shurikens
    W_2HSTAFF,   // Two-handed staves
    MAX_WEAPON_TYPE
};
```

---

## Ammo Types

```cpp
enum ammo_type : uint8 {
    AMMO_NONE = 0,
    AMMO_ARROW,        // Arrows
    AMMO_DAGGER,       // Throwing daggers
    AMMO_BULLET,       // Bullets
    AMMO_SHELL,        // Shells
    AMMO_GRENADE,      // Grenades
    AMMO_SHURIKEN,     // Shurikens
    AMMO_KUNAI,        // Kunai
    AMMO_CANNONBALL,   // Cannonballs
    AMMO_THROWWEAPON,  // Throwing weapons
    MAX_AMMO_TYPE
};
```

---

*KB Version 2.0 | Mode: SRC | Source: src/map/script.hpp, pc.hpp, status.hpp, map.hpp, itemdb.hpp*
