# rAthena KB v6 - Source Development Guide

**Version:** 6.0 Complete
**Generated:** 2025-11-26
**Language:** C++17

---

## Quick Navigation

- [Project Structure](#project-structure)
- [Key Source Files](#key-source-files)
- [Core Data Structures](#core-data-structures)
- [Adding Custom @Commands](#adding-custom-commands)
- [Modifying Battle Formulas](#modifying-battle-formulas)
- [Adding Custom Skills](#adding-custom-skills)
- [Build System](#build-system)

---

## Project Structure

<!-- RAG_CHUNK: src_project_structure -->

```
rathena/
├── src/
│   ├── char/           # Character server
│   │   ├── char.cpp    # Main char server
│   │   ├── int_*.cpp   # Inter-server communication
│   │   └── char.hpp    # Header definitions
│   │
│   ├── common/         # Shared utilities
│   │   ├── database.hpp    # YAML database base
│   │   ├── mmo.hpp         # Core MMO definitions
│   │   ├── socket.cpp      # Network handling
│   │   ├── timer.cpp       # Timer system
│   │   └── utils.cpp       # Utility functions
│   │
│   ├── login/          # Login server
│   │   ├── login.cpp   # Authentication
│   │   └── account.cpp # Account management
│   │
│   └── map/            # Map server (MAIN)
│       ├── atcommand.cpp   # @commands
│       ├── battle.cpp      # Damage calculation
│       ├── clif.cpp        # Client communication
│       ├── itemdb.cpp      # Item database
│       ├── map.cpp         # Map management
│       ├── mob.cpp         # Monster AI
│       ├── npc.cpp         # NPC handling
│       ├── party.cpp       # Party system
│       ├── pc.cpp          # Player character
│       ├── script.cpp      # Script engine
│       ├── skill.cpp       # Skill system
│       ├── status.cpp      # Status effects
│       └── unit.cpp        # Unit management
│
├── conf/               # Configuration files
├── db/                 # Database files (YAML)
├── doc/                # Documentation
├── npc/                # NPC scripts
└── tools/              # Utility tools
```

---

## Key Source Files

<!-- RAG_CHUNK: src_key_files -->

### Player Data: `src/map/pc.cpp` & `pc.hpp`
```cpp
// Key functions:
int pc_additem(map_session_data *sd, item *item, int amount, e_log_pick_type log_type);
int pc_delitem(map_session_data *sd, int n, int amount, int type, short reason, e_log_pick_type log_type);
int pc_gainexp(map_session_data *sd, block_list *src, t_exp base_exp, t_exp job_exp, bool quest);
int pc_setpos(map_session_data *sd, unsigned short mapindex, int x, int y, clr_type clrtype);
```

### Battle System: `src/map/battle.cpp` & `battle.hpp`
```cpp
// Damage calculation:
int64 battle_calc_damage(block_list *src, block_list *bl, int64 damage, uint16 skill_id, uint16 skill_lv);
struct Damage battle_calc_attack(int attack_type, block_list *src, block_list *target, uint16 skill_id, uint16 skill_lv, int count);

// Configuration:
struct Battle_Config battle_config;
```

### Status Effects: `src/map/status.cpp` & `status.hpp`
```cpp
// Apply/remove status:
int status_change_start(block_list *src, block_list *bl, sc_type type, int rate, int val1, int val2, int val3, int val4, t_tick duration, unsigned char flag);
int status_change_end(block_list *bl, sc_type type, int tid);

// Status enumeration:
enum sc_type {
    SC_STONE, SC_FREEZE, SC_STUN, SC_SLEEP, SC_POISON, ...
};
```

### Script Engine: `src/map/script.cpp`
```cpp
// Add new script command:
BUILDIN_FUNC(commandname) {
    // Your code here
    return SCRIPT_CMD_SUCCESS;
}

// Register command in script.cpp:
BUILDIN_DEF(commandname, "argument_types"),
// Argument types: i=int, s=string, v=variable, ?=optional, *=rest
```

---

## Core Data Structures

<!-- RAG_CHUNK: src_data_structures -->

### map_session_data (Player)
```cpp
struct map_session_data {
    struct block_list bl;           // Base unit data
    struct unit_data ud;            // Unit data (movement, etc.)
    struct status_data base_status; // Base stats
    struct status_data battle_status; // Current stats
    struct status_change sc;        // Active status effects
    
    // Character info
    int char_id;
    int account_id;
    char name[NAME_LENGTH];
    
    // Stats
    uint32 base_level, job_level;
    uint64 base_exp, job_exp;
    int status_point, skill_point;
    
    // Inventory
    struct item inventory[MAX_INVENTORY];
    struct s_storage storage;
    
    // Skills
    struct s_skill skill[MAX_SKILL];
    
    // Equipment
    struct {
        short index, id, card[4];
    } equip_index[EQI_MAX];
};
```

### block_list (Base Unit)
```cpp
struct block_list {
    int id;               // Unique ID
    int16 m;              // Map index
    int16 x, y;           // Coordinates
    enum bl_type type;    // BL_PC, BL_MOB, BL_NPC, etc.
    struct block_list *next, *prev;
};
```

### status_data
```cpp
struct status_data {
    unsigned int hp, sp;
    unsigned int max_hp, max_sp;
    short str, agi, vit, int_, dex, luk;
    short batk, matk_min, matk_max;
    short def, def2, mdef, mdef2;
    short hit, flee, flee2, cri;
    short aspd_rate;
    unsigned char def_ele, ele_lv;
    unsigned char size, race;
    short mode;
};
```

---

## Adding Custom @Commands

<!-- RAG_CHUNK: src_custom_atcommand -->

### Step 1: Declare in atcommand.hpp
```cpp
// In src/map/atcommand.hpp, add declaration:
ACMD_FUNC(mycommand);
```

### Step 2: Implement in atcommand.cpp
```cpp
// In src/map/atcommand.cpp, add implementation:
ACMD_FUNC(mycommand) {
    nullpo_retr(-1, sd);  // Null pointer check
    
    // Parse arguments
    char arg1[100];
    int arg2 = 0;
    
    if (!message || !*message || sscanf(message, "%99s %d", arg1, &arg2) < 1) {
        clif_displaymessage(fd, "Usage: @mycommand <name> <number>");
        return -1;
    }
    
    // Your logic here
    char output[256];
    sprintf(output, "Command executed: %s %d", arg1, arg2);
    clif_displaymessage(fd, output);
    
    return 0; // Success
}
```

### Step 3: Register the command
```cpp
// In atcommand.cpp, find atcommand_base[] array and add:
{ "mycommand", atcommand_mycommand },
```

### Step 4: Set permissions in conf/groups.conf
```
{
    id: 0       // Player group
    commands: {
        mycommand: true
    }
}
```

---

## Modifying Battle Formulas

<!-- RAG_CHUNK: src_battle_formulas -->

### Physical Damage: `battle.cpp`
```cpp
// In battle_calc_weapon_attack():

// Base ATK calculation
int64 atkmax = status->batk + status->rhw.atk;
int64 atkmin = status->batk + status->rhw.atk2;

// Add your modifier here
if (sd && sd->special_state.my_custom_bonus) {
    atkmax = atkmax * 120 / 100;  // +20% damage
    atkmin = atkmin * 120 / 100;
}

// Element modifier
int64 damage = battle_attr_fix(src, target, damage, s_ele, tstatus->def_ele, tstatus->ele_lv);

// Size modifier
damage = damage * (100 + pc_checkwatk(sd, weapon, weapon_perfection)) / 100;
```

### Magic Damage: `battle.cpp`
```cpp
// In battle_calc_magic_attack():

// MATK calculation
int64 matk = status_get_matk(src, 2);

// Skill-specific modifiers
switch (skill_id) {
    case MG_FIREBOLT:
        skillratio += 100 * skill_lv;
        break;
    // Add your skill modifiers
}

// Element modifier
damage = battle_attr_fix(src, target, damage, element, tstatus->def_ele, tstatus->ele_lv);
```

---

## Adding Custom Skills

<!-- RAG_CHUNK: src_custom_skills -->

### Step 1: Add skill constant in `skill.hpp`
```cpp
enum e_skill {
    // ... existing skills ...
    
    // Custom skills (use IDs 30000+)
    CUSTOM_SKILL1 = 30001,
    CUSTOM_SKILL2 = 30002,
};
```

### Step 2: Add to skill_db.yml
```yaml
- Id: 30001
  Name: "CUSTOM_SKILL1"
  Description: "My Custom Skill"
  MaxLevel: 10
  Type: Weapon
  TargetType: Attack
  Range:
    - Level: 1
      Size: 3
  SpCost:
    - Level: 1
      Amount: 20
```

### Step 3: Implement skill effect in `skill.cpp`
```cpp
// In skill_castend_damage_id() or skill_castend_nodamage_id():
case CUSTOM_SKILL1: {
    // Calculate damage
    int64 damage = 500 * skill_lv;
    damage = damage * status_get_matk(src, 2) / 100;
    
    // Deal damage
    battle_damage(src, target, damage, 0, skill_get_walkdelay(skill_id, skill_lv), !flag);
    clif_skill_damage(src, target, tick, status_get_amotion(src), 0, damage, 1, skill_id, skill_lv, DMG_SINGLE);
    break;
}
```

---

## Build System

<!-- RAG_CHUNK: src_build_system -->

### CMake Build (Recommended)
```bash
# Create build directory
mkdir build && cd build

# Configure
cmake -G "Unix Makefiles" ..

# Build
make -j$(nproc)

# Or for specific target
make map-server
make char-server  
make login-server
```

### Required Dependencies
- CMake 3.13+
- GCC 7+ or Clang 6+
- MySQL/MariaDB client libraries
- zlib
- OpenSSL (optional, for secure connections)
- PCRE (optional, for regex support)

### Build Options
```cmake
cmake -DWITH_MYSQL=ON -DWITH_PCRE=ON -DWITH_SSL=ON ..
```

---

*Generated as part of rAthena KB v6 Complete*
