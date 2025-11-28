# 04_PATTERNS.md
<!-- repo: rathena | branch: claude/github-to-kb-converter-0137h2Ti2PFSsGmn6Xrp3xko | commit: 721d46e | generated: 2025-11-28 -->
<!-- tags: patterns, conventions, coding, style, architecture -->

## Contents
- [Naming Conventions](#naming-conventions)
- [Code Style](#code-style)
- [Design Patterns](#design-patterns)
- [Error Handling](#error-handling)
- [Memory Management](#memory-management)
- [File Organization](#file-organization)

---

## Naming Conventions
<!-- chunk: 04-naming | keywords: naming, prefix, suffix, convention -->

### Function Naming

| Type | Prefix | Example | Location |
|------|--------|---------|----------|
| Module function | `module_` | `pc_addspiritball()` | pc.cpp |
| Client interface | `clif_` | `clif_displaymessage()` | clif.cpp |
| Char-server interface | `chrif_` | `chrif_save()` | chrif.cpp |
| Inter-server | `intif_` | `intif_guild_request()` | intif.cpp |
| Battle function | `battle_` | `battle_calc_attack()` | battle.cpp |
| Status function | `status_` | `status_change_start()` | status.cpp |
| Skill function | `skill_` | `skill_castend_damage_id()` | skill.cpp |
| Map function | `map_` | `map_foreachinrange()` | map.cpp |
| NPC function | `npc_` | `npc_parse_script()` | npc.cpp |
| Script buildin | `buildin_` | `buildin_mes()` | script.cpp |

### Structure Naming

| Type | Prefix | Example |
|------|--------|---------|
| Structure | `s_` | `s_quest_db` |
| Session data | `*_session_data` | `map_session_data` |
| Database entry | `*_db` | `item_db` |

### Constant Naming

| Type | Prefix | Example |
|------|--------|---------|
| Status change | `SC_` | `SC_BLESSING` |
| Skill ID | `<class>_` | `AL_HEAL`, `MG_FIREBOLT` |
| Bonus type | `SP_` or `b` | `SP_ATK_RATE`, `bStr` |
| Enumeration | `e_` | `e_race`, `e_size` |
| Battle flag | `BF_` | `BF_WEAPON`, `BF_MAGIC` |
| Element | `ELE_` | `ELE_FIRE`, `ELE_WATER` |
| Race | `RC_` | `RC_DEMON`, `RC_UNDEAD` |

### Variable Naming

| Variable | Full Name | Description |
|----------|-----------|-------------|
| `sd` | session data | Player session |
| `tsd` | target sd | Target player |
| `md` | mob data | Monster data |
| `nd` | NPC data | NPC data |
| `pd` | pet data | Pet data |
| `hd` | homunculus data | Homunculus data |
| `ed` | elemental data | Elemental data |
| `bl` | block list | Generic unit |
| `tbl` | target bl | Target unit |
| `sc` | status change | Status container |
| `sce` | status change entry | Single status |
| `st` | script stack | Script state |
| `fd` | file descriptor | Socket descriptor |
| `aid` | account ID | Account identifier |
| `cid` | character ID | Character identifier |
| `gid` | game ID | Generic unit ID |

---

## Code Style
<!-- chunk: 04-style | keywords: style, formatting, indentation -->

### General Rules

- **Indentation:** Tabs (displayed as 4 spaces)
- **Line Length:** No hard limit, prefer ~120 characters
- **Braces:** Opening brace on same line (K&R style)
- **Comments:** `//` for single line, `/* */` for blocks

### Function Definition Style

```cpp
/**
 * Brief description of function.
 * @param param1: Description of first parameter
 * @param param2: Description of second parameter
 * @return Description of return value
 */
int module_function(int param1, const char* param2)
{
    if (param1 < 0) {
        ShowError("module_function: Invalid param1 %d\n", param1);
        return -1;
    }

    // Function body
    return 0;
}
```

### Conditional Style

```cpp
// Single statement - braces optional but recommended
if (condition)
    single_statement();

// Multiple statements - always use braces
if (condition) {
    statement1();
    statement2();
}

// Switch statements
switch (value) {
    case 1:
        action1();
        break;
    case 2:
        action2();
        // fallthrough
    case 3:
        action3();
        break;
    default:
        default_action();
        break;
}
```

### Macro Definitions

```cpp
// Simple macros - uppercase with underscores
#define MAX_INVENTORY 100
#define STATUS_CHANGE_TICK_RATE 200

// Function-like macros - parenthesize parameters
#define MIN(a, b) ((a) < (b) ? (a) : (b))
#define RFIFOB(fd, pos) (*(uint8*)RFIFOP((fd), (pos)))
```

---

## Design Patterns
<!-- chunk: 04-patterns | keywords: singleton, observer, factory -->

### Event Loop Pattern
<!-- chunk: 04-eventloop | keywords: timer, tick, scheduling -->

All servers use a single-threaded event loop with 50ms tick granularity:

```cpp
// src/common/core.cpp
int main(int argc, char** argv)
{
    // Initialization
    core_init(server_type);

    // Main event loop
    while (runflag) {
        t_tick next = do_timer(gettick_nocache());
        do_sockets(next);
    }

    // Cleanup
    core_final();
    return 0;
}
```

### Database Pattern
<!-- chunk: 04-database | keywords: db, hashtable, lookup -->

In-memory databases use hash tables or binary trees:

```cpp
// Creating a database
DBMap* item_db = idb_alloc(DB_OPT_BASE);

// Adding entries
idb_put(item_db, item_id, item_data);

// Retrieving entries
struct item_data* id = (struct item_data*)idb_get(item_db, item_id);

// Iterating
int count = 0;
dbi_foreach(item_db, [](DBKey key, DBData* data, va_list ap) -> int {
    struct item_data* id = (struct item_data*)db_data2ptr(data);
    // Process item
    return 0;
});
```

### Packet Handler Pattern
<!-- chunk: 04-packets | keywords: packet, handler, clif -->

Client packets are handled via function pointer tables:

```cpp
// Packet definition (src/map/clif.cpp)
struct s_packet_db {
    short len;
    void (*func)(int fd, map_session_data* sd);
    short pos[20];
};

// Packet handler registration
packet_db[HEADER_CZ_ENTER] = { 19, clif_parse_WantToConnect, ... };

// Handler implementation
void clif_parse_WantToConnect(int fd, map_session_data* sd)
{
    int account_id = RFIFOL(fd, 2);
    int char_id = RFIFOL(fd, 6);
    // Process login request
}
```

### Script Command Pattern
<!-- chunk: 04-script | keywords: buildin, script, command -->

Script commands use a registration pattern:

```cpp
// Definition macro (src/map/script.cpp)
BUILDIN_FUNC(mes)
{
    TBL_PC* sd = script_rid2sd(st);
    if (sd == NULL)
        return SCRIPT_CMD_SUCCESS;

    const char* mes = script_getstr(st, 2);
    clif_scriptmes(sd, st->oid, mes);
    return SCRIPT_CMD_SUCCESS;
}

// Registration
BUILDIN_DEF(mes, "s"),  // "s" = string argument
```

### AT Command Pattern
<!-- chunk: 04-atcmd | keywords: atcommand, gm, admin -->

AT commands follow similar registration:

```cpp
// Definition macro (src/map/atcommand.cpp)
ACMD_FUNC(item)
{
    int item_id = 0, amount = 1;

    if (!message || !*message) {
        clif_displaymessage(fd, "Usage: @item <item_id> {<amount>}");
        return -1;
    }

    // Parse arguments and create item
    return 0;
}

// Registration
ACMD_DEF(item),
```

---

## Error Handling
<!-- chunk: 04-errors | keywords: error, showmsg, nullpo -->

### Message Display Functions

```cpp
// Console output (src/common/showmsg.cpp)
ShowMessage("Normal message\n");
ShowStatus("Status: %s\n", status);
ShowInfo("Info: Connected to database\n");
ShowNotice("Notice: Player %s logged in\n", name);
ShowWarning("Warning: Invalid value %d\n", value);
ShowError("Error: Failed to load %s\n", filename);
ShowFatalError("Fatal: Cannot continue\n");
ShowDebug("Debug: var=%d\n", var);
```

### Null Pointer Checks

```cpp
// Null pointer validation macro (src/common/nullpo.hpp)
#define nullpo_ret(t) { if (nullpo_chk(t)) return 0; }
#define nullpo_retv(t) { if (nullpo_chk(t)) return; }
#define nullpo_retr(ret, t) { if (nullpo_chk(t)) return (ret); }

// Usage
int function(map_session_data* sd)
{
    nullpo_ret(sd);  // Returns 0 if sd is NULL
    // Continue processing
}
```

### Return Codes

```cpp
// Common return patterns
enum e_result {
    SUCCESS = 0,
    FAILURE = 1,
    INVALID_PARAM = -1,
    NOT_FOUND = -2,
};

// Boolean returns
// 0 = failure, 1 = success (C-style)
// false = failure, true = success (C++-style)
```

---

## Memory Management
<!-- chunk: 04-memory | keywords: malloc, free, ers -->

### Custom Allocators

```cpp
// Memory allocation (src/common/malloc.hpp)
#define aMalloc(n) malloc_((n), __FILE__, __LINE__, __func__)
#define aCalloc(m, n) calloc_((m), (n), __FILE__, __LINE__, __func__)
#define aRealloc(p, n) realloc_((p), (n), __FILE__, __LINE__, __func__)
#define aFree(p) free_((p), __FILE__, __LINE__, __func__)

// Safe string allocation
#define aStrdup(s) strdup_((s), __FILE__, __LINE__, __func__)
```

### Entry Reusage System (ERS)

```cpp
// Pool allocation for frequently allocated objects
// src/common/ers.hpp

// Create pool
ERS* ers = ers_new(sizeof(struct block_list), "block_list_ers");

// Allocate from pool
struct block_list* bl = (struct block_list*)ers_alloc(ers);

// Return to pool
ers_free(ers, bl);

// Destroy pool
ers_destroy(ers);
```

### String Buffer Management

```cpp
// Dynamic string buffers
struct StringBuf {
    char* ptr;
    int len;
    int max;
};

StringBuf_Init(&buf);
StringBuf_Printf(&buf, "Value: %d", value);
const char* result = StringBuf_Value(&buf);
StringBuf_Destroy(&buf);
```

---

## File Organization
<!-- chunk: 04-files | keywords: files, modules, organization -->

### Source File Structure

```cpp
// Standard file layout
// ============================================================
// file.cpp - Brief description
// ============================================================

// Includes - system first, then project
#include <stdlib.h>
#include <string.h>

#include "../common/cbasetypes.hpp"
#include "../common/timer.hpp"
#include "module.hpp"

// Static/private declarations
static int private_variable;
static void private_function(void);

// Public function implementations
int module_init(void)
{
    // Implementation
}

void module_final(void)
{
    // Cleanup
}

// Private function implementations
static void private_function(void)
{
    // Implementation
}
```

### Header File Structure

```cpp
// Standard header layout
#ifndef MODULE_HPP
#define MODULE_HPP

// Required includes
#include "../common/cbasetypes.hpp"

// Forward declarations
struct map_session_data;

// Type definitions
struct s_module_data {
    int field1;
    char field2[32];
};

// Constants
#define MODULE_MAX_ENTRIES 100

// Enumerations
enum e_module_type {
    MODULE_TYPE_A = 0,
    MODULE_TYPE_B = 1,
};

// Function declarations
int module_init(void);
void module_final(void);
int module_process(struct s_module_data* data);

#endif /* MODULE_HPP */
```

### Git Workflow

- **Main branch:** `master`
- **Feature branches:** `feature/description`
- **Bugfix branches:** `bugfix/issue-number`
- **Commit format:** Descriptive subject line, optional body

---

## Quick Links

- Architecture: → See [[01_ARCHITECTURE]]
- API Functions: → See [[02_CORE_API]]
- Configuration: → See [[05_CONFIG]]
- Debugging: → See [[06_DEBUG]]
