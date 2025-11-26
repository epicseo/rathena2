# rAthena KB v6.1 - Development & Troubleshooting

**Version:** 6.1 Validated
**Source:** src/map/*.cpp, src/map/*.hpp

---

## Quick Navigation

### Source Development
- [Project Structure](#project-structure)
- [Key Source Files](#key-source-files)
- [Core Data Structures](#core-data-structures)
- [Adding Custom @Commands](#adding-custom-commands)
- [Modifying Battle Formulas](#modifying-battle-formulas)
- [Build System](#build-system)

### Troubleshooting
- [Script Errors](#script-errors)
- [Database Errors](#database-errors)
- [Build Errors](#build-errors)
- [Runtime Errors](#runtime-errors)
- [Common Mistakes](#common-mistakes)

---

# PART 1: SOURCE DEVELOPMENT

## Project Structure

<!-- RAG_CHUNK: src_project_structure -->

```
rathena/
├── src/
│   ├── char/           # Character server
│   ├── common/         # Shared utilities
│   ├── login/          # Login server
│   └── map/            # Map server (MAIN)
│       ├── atcommand.cpp   # @commands
│       ├── battle.cpp      # Damage calculation
│       ├── clif.cpp        # Client communication
│       ├── pc.cpp          # Player character
│       ├── script.cpp      # Script engine
│       ├── skill.cpp       # Skill system
│       └── status.cpp      # Status effects
├── conf/               # Configuration files
├── db/                 # Database files (YAML)
└── npc/                # NPC scripts
```

---

## Key Source Files

<!-- RAG_CHUNK: src_key_files -->

### pc.cpp - Player Functions
```cpp
int pc_additem(map_session_data *sd, item *item, int amount, e_log_pick_type log_type);
int pc_delitem(map_session_data *sd, int n, int amount, int type, short reason, e_log_pick_type log_type);
int pc_gainexp(map_session_data *sd, block_list *src, t_exp base_exp, t_exp job_exp, bool quest);
int pc_setpos(map_session_data *sd, unsigned short mapindex, int x, int y, clr_type clrtype);
```

### battle.cpp - Damage Calculation
```cpp
int64 battle_calc_damage(block_list *src, block_list *bl, int64 damage, uint16 skill_id, uint16 skill_lv);
struct Damage battle_calc_attack(int attack_type, block_list *src, block_list *target, uint16 skill_id, uint16 skill_lv, int count);
```

### status.cpp - Status Effects
```cpp
int status_change_start(block_list *src, block_list *bl, sc_type type, int rate, int val1, int val2, int val3, int val4, t_tick duration, unsigned char flag);
int status_change_end(block_list *bl, sc_type type, int tid);
```

---

## Core Data Structures

<!-- RAG_CHUNK: src_data_structures -->

### map_session_data (Player)
```cpp
struct map_session_data {
    struct block_list bl;
    struct status_data base_status;
    struct status_data battle_status;
    struct status_change sc;

    int char_id, account_id;
    char name[NAME_LENGTH];
    uint32 base_level, job_level;
    uint64 base_exp, job_exp;
    struct item inventory[MAX_INVENTORY];
    struct s_skill skill[MAX_SKILL];
};
```

### status_data
```cpp
struct status_data {
    unsigned int hp, sp, max_hp, max_sp;
    short str, agi, vit, int_, dex, luk;
    short batk, matk_min, matk_max;
    short def, def2, mdef, mdef2;
    short hit, flee, cri;
};
```

---

## Adding Custom @Commands

<!-- RAG_CHUNK: src_custom_atcommand -->

### Step 1: Declare (atcommand.hpp)
```cpp
ACMD_FUNC(mycommand);
```

### Step 2: Implement (atcommand.cpp)
```cpp
ACMD_FUNC(mycommand) {
    nullpo_retr(-1, sd);
    char arg1[100];
    int arg2 = 0;

    if (!message || !*message || sscanf(message, "%99s %d", arg1, &arg2) < 1) {
        clif_displaymessage(fd, "Usage: @mycommand <name> <number>");
        return -1;
    }

    char output[256];
    sprintf(output, "Command executed: %s %d", arg1, arg2);
    clif_displaymessage(fd, output);
    return 0;
}
```

### Step 3: Register
```cpp
// In atcommand_base[] array:
{ "mycommand", atcommand_mycommand },
```

### Step 4: Permissions (conf/groups.conf)
```
commands: {
    mycommand: true
}
```

---

## Modifying Battle Formulas

<!-- RAG_CHUNK: src_battle_formulas -->

### Physical Damage (battle.cpp)
```cpp
// In battle_calc_weapon_attack():
int64 atkmax = status->batk + status->rhw.atk;

// Add custom modifier
if (sd && sd->special_state.my_custom_bonus) {
    atkmax = atkmax * 120 / 100;  // +20% damage
}

// Element modifier
damage = battle_attr_fix(src, target, damage, s_ele, tstatus->def_ele, tstatus->ele_lv);
```

---

## Build System

<!-- RAG_CHUNK: src_build_system -->

### CMake Build
```bash
mkdir build && cd build
cmake -G "Unix Makefiles" ..
make -j$(nproc)
```

### Dependencies
- CMake 3.13+, GCC 7+/Clang 6+
- MySQL/MariaDB client, zlib
- Optional: OpenSSL, PCRE

---

# PART 2: TROUBLESHOOTING

## Script Errors

<!-- RAG_CHUNK: troubleshoot_script -->

### Common Errors
| Error | Cause | Fix |
|-------|-------|-----|
| Unknown command | Typo | Check spelling |
| Unexpected EOF | Missing } | Count brackets |
| Variable undefined | Used before set | Initialize first |

### Variable Persistence
| Prefix | Scope | Persistence |
|--------|-------|-------------|
| @ | Character | Until logout |
| $ | Server | Until restart |
| # | Account | Permanent (SQL) |
| . | NPC | Until restart |
| .@ | Local | Until script ends |

### Script Fixes
```c
// Missing semicolon
Wrong: mes "Hello"
Right: mes "Hello";

// Using = instead of ==
Wrong: if (x = 1)
Right: if (x == 1)

// Missing end
OnInit:
    mes "Hello";
    end;  // Required!
```

---

## Database Errors

<!-- RAG_CHUNK: troubleshoot_database -->

### YAML Parse Errors
```yaml
# Use spaces, NOT tabs!
Body:
  - Id: 501        # 2 spaces
    Name: "Item"   # 4 spaces

# Quote special characters
Wrong: Name: Item: Special
Right: Name: "Item: Special"

# Proper list format
Jobs:
  All: true
  Novice: true
```

### Database Checklist
1. File loaded in `conf/import/`?
2. Correct ID?
3. Reloaded? (`@reloaditemdb`)
4. Check console for YAML errors

---

## Build Errors

<!-- RAG_CHUNK: troubleshoot_build -->

### Missing Libraries
```bash
# MySQL
sudo apt-get install libmysqlclient-dev

# PCRE
sudo apt-get install libpcre3-dev

# Check GCC version (need 7+)
g++ --version
```

---

## Runtime Errors

<!-- RAG_CHUNK: troubleshoot_runtime -->

### Server Won't Start
1. Check MySQL: `systemctl status mysql`
2. Check config: `conf/inter_athena.conf`
3. Check ports: `netstat -tulpn | grep 6900`
4. Check logs: `log/map-server.log`

### Client Disconnects
```c
// In src/custom/defines_pre.hpp
#define PACKETVER 20200401  // Match your client
```

---

## Common Mistakes

<!-- RAG_CHUNK: troubleshoot_common_mistakes -->

### Script
```c
Wrong: if (x = 1)         // Assigns!
Right: if (x == 1)        // Compares

Wrong: mes Test message;
Right: mes "Test message";

Wrong: getitem "Red_Potion", 10;
Right: getitem 501, 10;
```

### YAML
```yaml
Wrong: Refineable: yes
Right: Refineable: true

Wrong: Head_Top           # Missing value
Right: Head_Top: true
```

---

## Debug Commands

```
@iteminfo <id>    Item info
@mobinfo <id>     Monster info
@skillinfo <id>   Skill info
@reloadscript     Reload scripts
@reloaditemdb     Reload items
@reloadmobdb      Reload mobs
```

---

*rAthena KB v6.1 - Development & Troubleshooting*
