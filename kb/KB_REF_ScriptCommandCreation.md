---
kb_id: KB_REF_032
title: "Script Command Creation - BUILDIN_FUNC Implementation Guide"
category: Source Code Internals
keywords: [script_commands, buildin_func, script_state, stack_management, parameter_retrieval, script_engine, custom_commands, script_api, memory_management, array_handling]
related_files: [
  "src/map/script.cpp",
  "src/map/script.hpp",
  "src/map/pc.cpp",
  "src/common/malloc.cpp"
]
cross_references: [
  "KB_REF_MemoryCrashPatterns.md",
  "KB_REF_ScriptTimerInternals.md"
]
difficulty: expert
use_case: "Creating custom script commands, extending script engine functionality, understanding script internals"
version: rAthena 2024
last_updated: 2024-01-15
---

# Script Command Creation - BUILDIN_FUNC Implementation Guide

## 🎯 Critical Understanding

**WHY THIS MATTERS:**
- Script commands are the bridge between NPC scripts and C++ server code
- Understanding the stack-based architecture prevents crashes and memory leaks
- Proper parameter handling ensures type safety and script stability
- 90% of custom command crashes are from improper memory management

**THE ARCHITECTURE:**
```
NPC Script → Bytecode → Stack → BUILDIN_FUNC → Server Logic
   ↓            ↓         ↓          ↓              ↓
  rand(1,10)  Compile   Push Args  Extract Params  Random #
```

---

## 📋 Table of Contents

1. [BUILDIN_FUNC Macro Explained](#buildin-func-macro)
2. [Script State Structure](#script-state-structure)
3. [Stack Management](#stack-management)
4. [Parameter Retrieval](#parameter-retrieval)
5. [Return Values](#return-values)
6. [Registration with BUILDIN_DEF](#registration)
7. [Memory Management](#memory-management)
8. [Variable References](#variable-references)
9. [Array Handling](#array-handling)
10. [Optional Parameters](#optional-parameters)
11. [Complete Working Examples](#examples)
12. [Common Mistakes & Crashes](#common-mistakes)
13. [Testing Your Commands](#testing)

---

## 🔧 BUILDIN_FUNC Macro Explained {#buildin-func-macro}

### The Macro Definition
```cpp
// src/map/script.cpp:4913
#define BUILDIN_FUNC(x) int32 buildin_ ## x (struct script_state* st)
```

### What It Does
Expands `BUILDIN_FUNC(mes)` to:
```cpp
int32 buildin_mes(struct script_state* st)
```

### Function Signature Rules
- **Return Type:** Always `int32`
- **Return Values:**
  - `SCRIPT_CMD_SUCCESS` (0) - Command executed successfully
  - `SCRIPT_CMD_FAILURE` (1) - Command failed, triggers error reporting
- **Parameter:** Single `struct script_state* st` pointer
- **Naming:** Must be `buildin_<commandname>` for registration to work

### Basic Template
```cpp
/// Command description
/// Usage: mycommand <param1>,<param2>{,<optional>};
BUILDIN_FUNC(mycommand)
{
    // 1. Get required player data (if needed)
    map_session_data* sd;
    if (!script_rid2sd(sd))
        return SCRIPT_CMD_SUCCESS;

    // 2. Extract parameters from stack
    int32 param1 = script_getnum(st, 2);
    const char* param2 = script_getstr(st, 3);

    // 3. Validate parameters
    if (param1 < 0) {
        ShowError("buildin_mycommand: Invalid param1 value %d\n", param1);
        return SCRIPT_CMD_FAILURE;
    }

    // 4. Execute logic
    // ... your code here ...

    // 5. Push return value (optional)
    script_pushint(st, result);

    return SCRIPT_CMD_SUCCESS;
}
```

---

## 📊 Script State Structure {#script-state-structure}

### Core Structure Definition
```cpp
// src/map/script.hpp:316-336
struct script_state {
    struct script_stack* stack;  // The execution stack
    int32 start, end;            // Stack frame boundaries
    int32 pos;                   // Current bytecode position
    enum e_script_state state;   // RUN, STOP, END, RERUNLINE, GOTO, RETFUNC, CLOSE
    int32 rid, oid;             // Attached player RID, NPC OID
    struct script_code *script;  // The compiled script bytecode
    struct sleep_data {
        int32 tick, timer, charid;
    } sleep;
    struct script_state *bk_st;  // Backup state for nested scripts
    int32 bk_npcid;             // Backup NPC ID
    unsigned freeloop : 1;       // Infinite loop protection disabled
    unsigned op2ref : 1;         // Operator reference flag
    unsigned npc_item_flag : 1;  // Item script flag
    unsigned mes_active : 1;     // NPC dialog active
    unsigned clear_cutin : 1;    // Clear cutin on close
    char* funcname;             // Current function name
    uint32 id;                  // Unique state ID
};
```

### Key Fields Explained

#### rid (Run ID)
```cpp
// The character ID (GID) that triggered the script
// 0 = no player attached
int32 rid;

// Usage:
if (st->rid == 0) {
    ShowError("This command requires an attached player!\n");
    return SCRIPT_CMD_FAILURE;
}
```

#### oid (Object ID)
```cpp
// The NPC ID that owns this script
int32 oid;

// Get the NPC:
npc_data* nd = map_id2nd(st->oid);
```

#### stack (Execution Stack)
```cpp
// Contains all script data (parameters, variables, return values)
struct script_stack* stack;

// Stack structure:
struct script_stack {
    int32 sp;                    // Stack pointer (current top)
    int32 sp_max;               // Stack capacity
    int32 defsp;                // Default SP for cleanup
    struct script_data *stack_data; // The actual stack array
    struct reg_db scope;        // Scope variables (local vars)
};
```

#### state (Execution State)
```cpp
enum e_script_state {
    RUN,        // Continue execution
    STOP,       // Stop and wait for player input (menu, input, next)
    END,        // Script finished
    RERUNLINE,  // Re-execute current line (used by input/menu)
    GOTO,       // Jump to label
    RETFUNC,    // Return from function
    CLOSE       // Close dialog and end
};

// Usage:
st->state = STOP;  // Pause script for player input
```

---

## 🗂️ Stack Management {#stack-management}

### How Parameters Are Stored

```
Script Call:  mycommand(123, "hello", @var);

Stack Layout:
  Index:  [0]        [1]     [2]      [3]       [4]
  Data:   [C_FUNC] | [ARG] | [C_INT] | [C_STR] | [C_NAME]
          mycommand   ---    123       "hello"   @var

  st->start = 1  (ARG marker)
  st->end = 5    (one past last parameter)

Parameter Indexing (1-based):
  script_getdata(st, 1) = special (function reference)
  script_getdata(st, 2) = 123
  script_getdata(st, 3) = "hello"
  script_getdata(st, 4) = @var
```

### Stack Access Macros
```cpp
// src/map/script.hpp:35-74

// Get parameter at index (1-based)
#define script_getdata(st,i) (&((st)->stack->stack_data[(st)->start + (i)]))

// Check if parameter exists at index
#define script_hasdata(st,i) ((st)->end > (st)->start + (i))

// Get index of last parameter
#define script_lastdata(st) ((st)->end - (st)->start - 1)

// Push return values onto stack
#define script_pushint(st,val) push_val((st)->stack, C_INT, (val))
#define script_pushstr(st,val) push_str((st)->stack, C_STR, (val))
#define script_pushconststr(st,val) push_str((st)->stack, C_CONSTSTR, const_cast<char *>(val))
```

### Stack Data Types
```cpp
// src/map/script.hpp:222-265
typedef enum c_op {
    C_NOP,       // Nil/no value
    C_INT,       // Integer (int64)
    C_STR,       // String (auto-freed)
    C_CONSTSTR,  // Constant string (never freed)
    C_NAME,      // Variable reference
    C_POS,       // Label position
    C_PARAM,     // Parameter variable
    // ... operators ...
} c_op;

struct script_data {
    enum c_op type;
    union script_data_val {
        int64 num;                   // For C_INT
        char *str;                   // For C_STR/C_CONSTSTR
        struct script_retinfo* ri;   // For C_RETINFO
    } u;
    struct reg_db *ref;  // Variable scope reference
};
```

---

## 📥 Parameter Retrieval {#parameter-retrieval}

### Basic Retrieval Functions

#### script_getnum - Get Integer
```cpp
// src/map/script.hpp:59
#define script_getnum(st,val) conv_num(st, script_getdata(st,val))

// Returns: int32 value
// Converts: Any type to int32 (strings parsed as numbers)

BUILDIN_FUNC(example) {
    int32 value = script_getnum(st, 2);
    ShowInfo("Got integer: %d\n", value);
    return SCRIPT_CMD_SUCCESS;
}
```

#### script_getnum64 - Get 64-bit Integer
```cpp
// src/map/script.hpp:60
#define script_getnum64(st,val) conv_num64(st, script_getdata(st,val))

// Returns: int64 value
// Use for: Large numbers, timestamps, experience values

BUILDIN_FUNC(rand) {  // Real example from script.cpp:5579
    int64 minimum = script_getnum64(st, 2);
    int64 maximum = script_getnum64(st, 3);

    if (minimum > maximum) {
        ShowWarning("buildin_rand: minimum (%" PRId64 ") > maximum (%" PRId64 ")\n",
                    minimum, maximum);
    }

    script_pushint64(st, rnd_value(minimum, maximum));
    return SCRIPT_CMD_SUCCESS;
}
```

#### script_getstr - Get String
```cpp
// src/map/script.hpp:61
#define script_getstr(st,val) conv_str(st, script_getdata(st,val))

// Returns: const char* (temporary - DO NOT FREE)
// Lifetime: Valid until stack cleanup
// Converts: Numbers to strings automatically

BUILDIN_FUNC(mes) {  // Real example from script.cpp:4923
    map_session_data* sd;
    if (!script_rid2sd(sd))
        return SCRIPT_CMD_SUCCESS;

    // Get string parameter
    const char* message = script_getstr(st, 2);

    // Send to client
    clif_scriptmes(*sd, st->oid, message);

    st->mes_active = 1;
    return SCRIPT_CMD_SUCCESS;
}
```

#### script_getdata - Get Raw Stack Data
```cpp
// For advanced usage (variables, references)
struct script_data* data = script_getdata(st, 2);

// Check data type:
if (data_isstring(data)) {
    // It's a string
} else if (data_isint(data)) {
    // It's an integer
} else if (data_isreference(data)) {
    // It's a variable reference (@var, $var, etc.)
}

// Real example from script.cpp:6149 (input command)
BUILDIN_FUNC(input) {
    struct script_data* data = script_getdata(st, 2);

    // Must be a variable reference
    if (!data_isreference(data)) {
        ShowError("script:input: not a variable\n");
        script_reportdata(data);
        st->state = END;
        return SCRIPT_CMD_FAILURE;
    }

    int64 uid = reference_getuid(data);
    const char* name = reference_getname(data);
    // ... handle input ...
}
```

### script_hasdata - Check Parameter Exists
```cpp
// src/map/script.hpp:38
#define script_hasdata(st,i) ((st)->end > (st)->start + (i))

// Returns: bool (true if parameter exists)
// Use for: Optional parameters

BUILDIN_FUNC(warp) {  // Real example from script.cpp:5628
    const char* map = script_getstr(st, 2);
    int32 x = script_getnum(st, 3);
    int32 y = script_getnum(st, 4);

    map_session_data* sd;
    // Optional parameter 5: character ID
    if (!script_charid2sd(5, sd))  // Checks script_hasdata internally
        return SCRIPT_CMD_SUCCESS;

    // ... warp logic ...
}
```

### Type Checking Macros
```cpp
// src/map/script.hpp:56-57
#define script_isstring(st,i) data_isstring(get_val(st, script_getdata(st,i)))
#define script_isint(st,i) data_isint(get_val(st, script_getdata(st,i)))

// Usage:
if (script_isstring(st, 2)) {
    const char* str = script_getstr(st, 2);
} else {
    int32 num = script_getnum(st, 2);
}
```

---

## 📤 Return Values {#return-values}

### Push Functions

#### script_pushint - Return Integer (32-bit)
```cpp
// src/map/script.hpp:42
#define script_pushint(st,val) push_val((st)->stack, C_INT, (val))

BUILDIN_FUNC(countitem) {  // Real example from script.cpp:7223
    int32 count = 0;
    // ... count items ...
    script_pushint(st, count);  // Return count to script
    return SCRIPT_CMD_SUCCESS;
}
```

#### script_pushint64 - Return Integer (64-bit)
```cpp
// src/map/script.hpp:44
#define script_pushint64(st, val) push_val2((st)->stack, C_INT, val, nullptr)

BUILDIN_FUNC(rand) {  // Real example from script.cpp:5620
    int64 result = rnd_value(minimum, maximum);
    script_pushint64(st, result);
    return SCRIPT_CMD_SUCCESS;
}
```

#### script_pushstr - Return Dynamic String
```cpp
// src/map/script.hpp:46
#define script_pushstr(st,val) push_str((st)->stack, C_STR, (val))

// CRITICAL: String will be freed automatically by script engine
// MUST allocate with aStrdup/aMalloc

BUILDIN_FUNC(getitemname) {
    int32 item_id = script_getnum(st, 2);

    struct item_data* item = itemdb_exists(item_id);
    if (!item) {
        script_pushconststr(st, "Unknown Item");
        return SCRIPT_CMD_SUCCESS;
    }

    // Allocate new string - script engine will free it
    char* name = aStrdup(item->jname);
    script_pushstr(st, name);

    return SCRIPT_CMD_SUCCESS;
}
```

#### script_pushstrcopy - Return String Copy
```cpp
// src/map/script.hpp:48
#define script_pushstrcopy(st,val) push_str((st)->stack, C_STR, aStrdup(val))

// Convenience macro - automatically duplicates the string

BUILDIN_FUNC(example) {
    const char* static_str = "Hello World";

    // This is safe - string is copied
    script_pushstrcopy(st, static_str);

    return SCRIPT_CMD_SUCCESS;
}
```

#### script_pushconststr - Return Constant String
```cpp
// src/map/script.hpp:50
#define script_pushconststr(st,val) push_str((st)->stack, C_CONSTSTR, const_cast<char *>(val))

// CRITICAL: String must NEVER be freed (literals, const char*)
// Use for: String literals, permanent buffers

BUILDIN_FUNC(jobname) {  // Real example from script.cpp:6123
    int32 class_ = script_getnum(st, 2);

    // job_name returns a const char* to static data
    script_pushconststr(st, (char*)job_name(class_));

    return SCRIPT_CMD_SUCCESS;
}
```

### No Return Value
```cpp
// If command doesn't return a value, just don't push anything

BUILDIN_FUNC(mes) {
    // ... display message ...
    // No push - command has no return value
    return SCRIPT_CMD_SUCCESS;
}
```

---

## 📝 Registration with BUILDIN_DEF {#registration}

### Registration Macros
```cpp
// src/map/script.cpp:4909-4912
#define BUILDIN_DEF(x,args) { buildin_ ## x , #x , args, nullptr }
#define BUILDIN_DEF2(x,x2,args) { buildin_ ## x , x2 , args, nullptr }
#define BUILDIN_DEF_DEPRECATED(x,args,deprecationdate) { buildin_ ## x , #x , args, deprecationdate }
#define BUILDIN_DEF2_DEPRECATED(x,x2,args,deprecationdate) { buildin_ ## x , x2 , args, deprecationdate }
```

### Argument Pattern Syntax
```cpp
// Location: src/map/script.cpp (around line 27847+)
extern script_function buildin_func[];

// Pattern Characters:
// ""  = no parameters
// "i" = integer
// "s" = string
// "r" = reference (variable)
// "l" = label
// "v" = integer or string
// "?" = optional parameter
// "*" = any number of parameters (must be last)

// Examples from real code:
BUILDIN_DEF(mes,"s*"),           // mes "<text>"{,"<text>",...};
BUILDIN_DEF(next,""),            // next;
BUILDIN_DEF(close,""),           // close;
BUILDIN_DEF(rand,"i?"),          // rand(<max>) or rand(<min>,<max>)
BUILDIN_DEF(warp,"sii?"),        // warp "<map>",<x>,<y>{,<char_id>};
BUILDIN_DEF(input,"r??"),        // input(<variable>{,<min>,<max>})
BUILDIN_DEF(setarray,"rv*"),     // setarray <array>,<val1>{,<val2>,...};
BUILDIN_DEF(getitem,"vi?"),      // getitem <item>,<amount>{,<account_id>};
BUILDIN_DEF(menu,"sl*"),         // menu "<text>",<label>{,"<text>",<label>,...};
```

### Registration Example
```cpp
// 1. Implement the function
BUILDIN_FUNC(mycommand) {
    int32 param1 = script_getnum(st, 2);
    const char* param2 = script_getstr(st, 3);
    int32 optional = script_hasdata(st, 4) ? script_getnum(st, 4) : 0;

    // ... logic ...

    script_pushint(st, result);
    return SCRIPT_CMD_SUCCESS;
}

// 2. Register in buildin_func array (src/map/script.cpp)
extern script_function buildin_func[] = {
    // ... existing commands ...
    BUILDIN_DEF(mycommand,"is?"),  // mycommand <int>,"<str>"{,<optional_int>};
    // ... more commands ...
    { nullptr, nullptr, nullptr, nullptr }  // Array terminator
};
```

### Alternative Names
```cpp
// Register same function with different name
BUILDIN_DEF2(close, "close3", ""),  // close3 calls buildin_close

// One implementation, multiple script names:
BUILDIN_FUNC(close) {
    const char* command = script_getfuncname(st);

    if (!strcmp(command, "close3")) {
        st->clear_cutin = true;  // Special behavior for close3
    }

    // ... rest of close logic ...
}
```

---

## 💾 Memory Management {#memory-management}

### Memory Allocation Rules

#### For Strings Returned to Script
```cpp
// Rule 1: script_pushstr() takes ownership - string WILL be freed
char* str = (char*)aMalloc(256);
sprintf(str, "Result: %d", value);
script_pushstr(st, str);  // Script engine will aFree(str) later

// Rule 2: Use aStrdup for copying
const char* source = "Hello";
script_pushstr(st, aStrdup(source));  // Safe - new allocation

// Rule 3: NEVER push stack/local strings with script_pushstr
char buffer[256];  // DANGER!
sprintf(buffer, "Test");
script_pushstr(st, buffer);  // CRASH - will try to free stack memory!

// Correct:
script_pushstr(st, aStrdup(buffer));  // Safe - heap allocation
// OR
script_pushconststr(st, buffer);  // Safe - won't be freed (but buffer must live!)
```

#### For Constant Strings
```cpp
// String literals - use script_pushconststr
script_pushconststr(st, "Error: Invalid parameter");  // Safe

// Permanent buffers - use script_pushconststr
static char permanent_buffer[256] = "Data";
script_pushconststr(st, permanent_buffer);  // Safe

// Function returns const char* - use script_pushconststr
script_pushconststr(st, (char*)job_name(class_));  // Safe
```

#### Memory Allocation Functions
```cpp
// src/common/malloc.hpp

// Allocate memory
void* aMalloc(size_t size);
void* aCalloc(size_t num, size_t size);  // Zero-initialized
void* aRealloc(void* ptr, size_t size);

// Free memory
void aFree(void* ptr);

// String duplication
char* aStrdup(const char* str);  // Allocates and copies

// Example:
char* buffer = (char*)aMalloc(1024);
sprintf(buffer, "Player: %s", sd->status.name);
script_pushstr(st, buffer);  // Ownership transferred
```

### Common Memory Patterns

#### Pattern 1: Building Dynamic Strings
```cpp
BUILDIN_FUNC(getiteminfo) {
    int32 item_id = script_getnum(st, 2);
    struct item_data* item = itemdb_exists(item_id);

    if (!item) {
        script_pushconststr(st, "");
        return SCRIPT_CMD_SUCCESS;
    }

    // Build string dynamically
    char* result = (char*)aMalloc(256);
    snprintf(result, 256, "%s [%d]", item->jname, item_id);

    script_pushstr(st, result);  // Script engine will aFree(result)
    return SCRIPT_CMD_SUCCESS;
}
```

#### Pattern 2: Temporary Parameter Storage
```cpp
BUILDIN_FUNC(announce) {
    // Get string parameter - it's temporary!
    const char* message = script_getstr(st, 2);

    // WRONG: Store pointer for later use
    // some_global_ptr = message;  // CRASH - string will be freed!

    // CORRECT: Duplicate if you need to store it
    char* stored = aStrdup(message);
    some_global_ptr = stored;  // Safe

    // Remember to free later:
    // aFree(some_global_ptr);
}
```

#### Pattern 3: No Allocation Needed
```cpp
BUILDIN_FUNC(heal) {
    int32 hp = script_getnum(st, 2);
    int32 sp = script_getnum(st, 3);

    map_session_data* sd;
    if (!script_rid2sd(sd))
        return SCRIPT_CMD_SUCCESS;

    // Direct use - no allocation
    pc_heal(sd, hp, sp, 0);

    // No return value - no memory management
    return SCRIPT_CMD_SUCCESS;
}
```

### Memory Leak Prevention
```cpp
BUILDIN_FUNC(risky_command) {
    char* buffer1 = (char*)aMalloc(1024);
    char* buffer2 = (char*)aMalloc(1024);

    // Validation
    if (script_getnum(st, 2) < 0) {
        // WRONG: Leaks buffer1 and buffer2
        return SCRIPT_CMD_FAILURE;

        // CORRECT: Free before returning
        aFree(buffer1);
        aFree(buffer2);
        return SCRIPT_CMD_FAILURE;
    }

    // Use buffers...
    sprintf(buffer1, "Data");

    // Only push one - must free the other
    script_pushstr(st, buffer1);  // Ownership transferred
    aFree(buffer2);  // We're not using this one

    return SCRIPT_CMD_SUCCESS;
}
```

**CRITICAL MEMORY RULES:**
1. ✅ `script_pushstr()` - String MUST be heap-allocated, engine frees it
2. ✅ `script_pushconststr()` - String MUST NEVER be freed
3. ✅ Always use `aStrdup()` to copy strings for storage
4. ✅ Free allocated memory on all error paths
5. ❌ Never push stack/local buffers with `script_pushstr()`
6. ❌ Never store `script_getstr()` results beyond function scope

**See Also:** KB_REF_MemoryCrashPatterns.md for detailed crash prevention

---

## 🔗 Variable References {#variable-references}

### Variable Prefix Types
```cpp
// Character variables (stored per player)
@var    // Temporary (cleared on logout)
@var$   // Temporary string

// Permanent character variables (saved to database)
#var    // Permanent integer
#var$   // Permanent string

// Account variables (shared across characters)
##var   // Account-wide integer
##var$  // Account-wide string

// Global server variables
$var    // Global integer (all players)
$var$   // Global string

// NPC/Instance variables
.var    // NPC-local variable
.var$   // NPC-local string

// Special
'var    // Instance variable
```

### Working with References

#### Checking if Parameter is a Reference
```cpp
BUILDIN_FUNC(set_or_input) {
    struct script_data* data = script_getdata(st, 2);

    if (!data_isreference(data)) {
        ShowError("buildin_set_or_input: Parameter must be a variable!\n");
        script_reportdata(data);  // Show what was passed
        st->state = END;
        return SCRIPT_CMD_FAILURE;
    }

    // It's a valid reference - proceed
    // ...
}
```

#### Getting Reference Information
```cpp
// Real example from script.cpp:6201 (setr command)
BUILDIN_FUNC(setr) {
    struct script_data* data = script_getdata(st, 2);

    if (!data_isreference(data)) {
        ShowError("script:set: not a variable\n");
        return SCRIPT_CMD_FAILURE;
    }

    // Get variable details
    int64 uid = reference_getuid(data);      // Unique ID (var ID + array index)
    const char* name = reference_getname(data);  // Variable name
    int32 id = reference_getid(data);         // Variable ID only
    uint32 index = reference_getindex(data);  // Array index (0 if not array)
    struct reg_db* ref = reference_getref(data);  // Scope reference

    // Get variable prefix
    char prefix = *name;  // First character

    // Check scope
    if (not_server_variable(prefix)) {
        // Need player for @, #, ## variables
        map_session_data* sd;
        if (!script_rid2sd(sd)) {
            ShowError("buildin_set: No player for variable '%s'\n", name);
            return SCRIPT_CMD_FAILURE;
        }
    }

    // Set the variable value
    if (is_string_variable(name)) {
        const char* value = script_getstr(st, 3);
        set_reg_str(st, sd, uid, name, value, ref);
    } else {
        int64 value = script_getnum64(st, 3);
        set_reg_num(st, sd, uid, name, value, ref);
    }

    return SCRIPT_CMD_SUCCESS;
}
```

#### Setting Variable Values
```cpp
// Set integer variable
bool set_reg_num(struct script_state* st, map_session_data* sd,
                 int64 uid, const char* name, int64 value, struct reg_db *ref);

// Set string variable
bool set_reg_str(struct script_state* st, map_session_data* sd,
                 int64 uid, const char* name, const char* value, struct reg_db* ref);

// Clear variable
bool clear_reg(struct script_state* st, map_session_data* sd,
               int64 uid, const char* name, struct reg_db *ref);

// Example:
BUILDIN_FUNC(setvar) {
    struct script_data* data = script_getdata(st, 2);
    map_session_data* sd = nullptr;

    if (!data_isreference(data))
        return SCRIPT_CMD_FAILURE;

    int64 uid = reference_getuid(data);
    const char* name = reference_getname(data);
    struct reg_db* ref = reference_getref(data);

    if (not_server_variable(*name) && !script_rid2sd(sd))
        return SCRIPT_CMD_FAILURE;

    int32 value = script_getnum(st, 3);
    set_reg_num(st, sd, uid, name, value, ref);

    return SCRIPT_CMD_SUCCESS;
}
```

---

## 📊 Array Handling {#array-handling}

### Array Reference Structure
```cpp
// Arrays store index in upper 32 bits of UID
// uid = (index << 32) | variable_id

// Get array information:
uint32 index = reference_getindex(data);  // Array index
int32 id = reference_getid(data);         // Variable ID (same for all elements)
```

### Working with Arrays

#### Example: setarray Command
```cpp
// Real implementation from script.cpp:6285
BUILDIN_FUNC(setarray) {
    struct script_data* data = script_getdata(st, 2);
    map_session_data* sd = nullptr;

    if (!data_isreference(data)) {
        ShowError("script:setarray: not a variable\n");
        return SCRIPT_CMD_FAILURE;
    }

    int32 id = reference_getid(data);
    uint32 start = reference_getindex(data);  // Starting index
    const char* name = reference_getname(data);

    if (not_server_variable(*name) && !script_rid2sd(sd))
        return SCRIPT_CMD_SUCCESS;

    // Calculate end index
    uint32 end = start + script_lastdata(st) - 2;
    if (end > SCRIPT_MAX_ARRAYSIZE)
        end = SCRIPT_MAX_ARRAYSIZE;

    // Set array elements
    if (is_string_variable(name)) {
        // String array
        for (int32 i = 3; start < end; ++start, ++i) {
            set_reg_str(st, sd, reference_uid(id, start), name,
                       script_getstr(st, i), reference_getref(data));
        }
    } else {
        // Integer array
        for (int32 i = 3; start < end; ++start, ++i) {
            set_reg_num(st, sd, reference_uid(id, start), name,
                       script_getnum64(st, i), reference_getref(data));
        }
    }

    return SCRIPT_CMD_SUCCESS;
}
```

#### Example: getarraysize Command
```cpp
// Real implementation from script.cpp:6482
BUILDIN_FUNC(getarraysize) {
    struct script_data* data = script_getdata(st, 2);
    map_session_data* sd = nullptr;

    if (!data_isreference(data)) {
        script_pushint(st, 0);
        return SCRIPT_CMD_SUCCESS;
    }

    const char* name = reference_getname(data);

    if (not_server_variable(*name) && !script_rid2sd(sd))
        return SCRIPT_CMD_SUCCESS;

    // Get highest array index
    uint32 size = script_array_highest_key(st, sd, name, reference_getref(data));

    script_pushint(st, size);
    return SCRIPT_CMD_SUCCESS;
}
```

#### Array Helper Functions
```cpp
// Get array size (number of elements)
uint32 script_array_size(struct script_state *st, map_session_data *sd,
                         const char *name, struct reg_db *ref);

// Get highest array index
uint32 script_array_highest_key(struct script_state *st, map_session_data *sd,
                                const char *name, struct reg_db *ref);

// Construct array element UID
int64 reference_uid(int32 id, uint32 index);

// Example:
int32 var_id = reference_getid(data);
for (uint32 i = 0; i < 10; i++) {
    int64 uid = reference_uid(var_id, i);
    set_reg_num(st, sd, uid, name, i * 100, ref);
}
```

### Array Bounds
```cpp
// Maximum array size
#define SCRIPT_MAX_ARRAYSIZE (UINT_MAX - 1)

// Always check bounds:
if (end > SCRIPT_MAX_ARRAYSIZE)
    end = SCRIPT_MAX_ARRAYSIZE;
```

---

## ⚙️ Optional Parameters {#optional-parameters}

### Checking for Optional Parameters
```cpp
// Use script_hasdata() to check if parameter exists

BUILDIN_FUNC(heal) {  // Real example from script.cpp:6007
    int32 hp = script_getnum(st, 2);
    int32 sp = script_getnum(st, 3);

    map_session_data* sd;

    // Parameter 4 is optional - character ID
    if (!script_charid2sd(4, sd))  // Helper checks script_hasdata internally
        return SCRIPT_CMD_SUCCESS;

    pc_heal(sd, hp, sp, 0);
    return SCRIPT_CMD_SUCCESS;
}
```

### Multiple Optional Parameters
```cpp
BUILDIN_FUNC(input) {  // Real example from script.cpp:6137
    struct script_data* data = script_getdata(st, 2);
    int32 min, max;

    // Optional parameter 3: minimum value
    min = script_hasdata(st, 3) ? script_getnum(st, 3) : script_config.input_min_value;

    // Optional parameter 4: maximum value
    max = script_hasdata(st, 4) ? script_getnum(st, 4) : script_config.input_max_value;

    // ... use min and max ...
}
```

### Variadic Parameters (*)
```cpp
// Pattern: "s*" means first param is string, then any number of additional params

BUILDIN_FUNC(mes) {  // Real example from script.cpp:4923
    map_session_data* sd;
    if (!script_rid2sd(sd))
        return SCRIPT_CMD_SUCCESS;

    if (!script_hasdata(st, 3)) {
        // Single parameter
        clif_scriptmes(*sd, st->oid, script_getstr(st, 2));
    } else {
        // Multiple parameters - loop through all
        for (int32 i = 2; script_hasdata(st, i); i++) {
            clif_scriptmes(*sd, st->oid, script_getstr(st, i));
        }
    }

    st->mes_active = 1;
    return SCRIPT_CMD_SUCCESS;
}
```

### Default Values Pattern
```cpp
BUILDIN_FUNC(mycommand) {
    // Required parameters
    int32 param1 = script_getnum(st, 2);

    // Optional with defaults
    int32 param2 = script_hasdata(st, 3) ? script_getnum(st, 3) : 100;
    const char* param3 = script_hasdata(st, 4) ? script_getstr(st, 4) : "default";
    bool param4 = script_hasdata(st, 5) ? (bool)script_getnum(st, 5) : true;

    ShowInfo("Params: %d, %d, %s, %d\n", param1, param2, param3, param4);
    return SCRIPT_CMD_SUCCESS;
}

// Registration:
BUILDIN_DEF(mycommand,"i???"),  // mycommand <int>{,<int>,<str>,<bool>}
```

---

## 💡 Complete Working Examples {#examples}

### Example 1: Simple Command (No Parameters)
```cpp
/// Displays server uptime
/// Usage: showuptime;
BUILDIN_FUNC(showuptime)
{
    map_session_data* sd;
    if (!script_rid2sd(sd))
        return SCRIPT_CMD_SUCCESS;

    time_t uptime = time(nullptr) - server_start_time;
    int32 days = uptime / 86400;
    int32 hours = (uptime % 86400) / 3600;
    int32 minutes = (uptime % 3600) / 60;

    char* message = (char*)aMalloc(256);
    snprintf(message, 256, "Server uptime: %d days, %d hours, %d minutes",
             days, hours, minutes);

    clif_displaymessage(sd->fd, message);
    aFree(message);

    return SCRIPT_CMD_SUCCESS;
}

// Registration:
BUILDIN_DEF(showuptime,""),
```

### Example 2: Parameter Validation
```cpp
/// Gives experience with validation
/// Usage: giveexp <base_exp>,<job_exp>;
BUILDIN_FUNC(giveexp)
{
    map_session_data* sd;
    if (!script_rid2sd(sd))
        return SCRIPT_CMD_SUCCESS;

    int64 base_exp = script_getnum64(st, 2);
    int64 job_exp = script_getnum64(st, 3);

    // Validation
    if (base_exp < 0 || job_exp < 0) {
        ShowError("buildin_giveexp: Experience values cannot be negative! (base:%" PRId64 ", job:%" PRId64 ")\n",
                  base_exp, job_exp);
        return SCRIPT_CMD_FAILURE;
    }

    if (base_exp > INT_MAX || job_exp > INT_MAX) {
        ShowWarning("buildin_giveexp: Experience values too large, capping to INT_MAX\n");
        base_exp = min(base_exp, (int64)INT_MAX);
        job_exp = min(job_exp, (int64)INT_MAX);
    }

    // Give experience
    pc_gainexp(sd, nullptr, base_exp, job_exp, 0);

    return SCRIPT_CMD_SUCCESS;
}

// Registration:
BUILDIN_DEF(giveexp,"ii"),
```

### Example 3: Optional Parameters with Return Value
```cpp
/// Counts items in inventory with optional account ID
/// Usage: .count = countitems(<item_id>{,<account_id>});
BUILDIN_FUNC(countitems)
{
    int32 item_id = script_getnum(st, 2);
    map_session_data* sd;

    // Optional parameter: account ID (defaults to attached player)
    if (!script_accid2sd(3, sd))
        return SCRIPT_CMD_SUCCESS;

    // Validate item exists
    struct item_data* item = itemdb_exists(item_id);
    if (!item) {
        ShowError("buildin_countitems: Invalid item ID %d\n", item_id);
        script_pushint(st, 0);
        return SCRIPT_CMD_FAILURE;
    }

    // Count items
    int32 count = 0;
    for (int32 i = 0; i < MAX_INVENTORY; i++) {
        if (sd->inventory.u.items_inventory[i].nameid == item_id)
            count += sd->inventory.u.items_inventory[i].amount;
    }

    script_pushint(st, count);
    return SCRIPT_CMD_SUCCESS;
}

// Registration:
BUILDIN_DEF(countitems,"i?"),
```

### Example 4: Variable Reference (Input/Output Parameter)
```cpp
/// Increments a variable by amount
/// Usage: increment <variable>,<amount>;
BUILDIN_FUNC(increment)
{
    struct script_data* data = script_getdata(st, 2);
    map_session_data* sd = nullptr;

    // Validate it's a reference
    if (!data_isreference(data)) {
        ShowError("buildin_increment: First parameter must be a variable!\n");
        script_reportdata(data);
        st->state = END;
        return SCRIPT_CMD_FAILURE;
    }

    // Validate it's an integer variable
    const char* name = reference_getname(data);
    if (is_string_variable(name)) {
        ShowError("buildin_increment: Variable '%s' is a string variable!\n", name);
        return SCRIPT_CMD_FAILURE;
    }

    // Get player if needed
    if (not_server_variable(*name) && !script_rid2sd(sd))
        return SCRIPT_CMD_SUCCESS;

    // Get current value
    int64 uid = reference_getuid(data);
    struct reg_db* ref = reference_getref(data);
    int64 current = get_val2_num(st, uid, ref);

    // Get increment amount
    int64 amount = script_getnum64(st, 3);

    // Set new value
    set_reg_num(st, sd, uid, name, current + amount, ref);

    return SCRIPT_CMD_SUCCESS;
}

// Registration:
BUILDIN_DEF(increment,"ri"),
```

### Example 5: Array Manipulation
```cpp
/// Fills an array with sequential values
/// Usage: fillarray <array>,<start>,<count>;
BUILDIN_FUNC(fillarray)
{
    struct script_data* data = script_getdata(st, 2);
    map_session_data* sd = nullptr;

    if (!data_isreference(data)) {
        ShowError("buildin_fillarray: Parameter must be an array!\n");
        return SCRIPT_CMD_FAILURE;
    }

    const char* name = reference_getname(data);

    if (is_string_variable(name)) {
        ShowError("buildin_fillarray: Array '%s' must be integer type!\n", name);
        return SCRIPT_CMD_FAILURE;
    }

    if (not_server_variable(*name) && !script_rid2sd(sd))
        return SCRIPT_CMD_SUCCESS;

    int32 id = reference_getid(data);
    uint32 start_index = reference_getindex(data);
    struct reg_db* ref = reference_getref(data);

    int64 start_value = script_getnum64(st, 3);
    uint32 count = script_getnum(st, 4);

    // Bounds check
    if (start_index + count > SCRIPT_MAX_ARRAYSIZE)
        count = SCRIPT_MAX_ARRAYSIZE - start_index;

    // Fill array
    for (uint32 i = 0; i < count; i++) {
        int64 uid = reference_uid(id, start_index + i);
        set_reg_num(st, sd, uid, name, start_value + i, ref);
    }

    return SCRIPT_CMD_SUCCESS;
}

// Registration:
BUILDIN_DEF(fillarray,"rii"),
```

### Example 6: Complex String Building with Memory Management
```cpp
/// Builds a formatted player info string
/// Usage: .info$ = getplayerinfo("<name>");
BUILDIN_FUNC(getplayerinfo)
{
    const char* player_name = script_getstr(st, 2);

    // Find player
    map_session_data* sd = map_nick2sd(player_name, false);
    if (!sd) {
        ShowError("buildin_getplayerinfo: Player '%s' not found\n", player_name);
        script_pushconststr(st, "Player not found");
        return SCRIPT_CMD_FAILURE;
    }

    // Build info string (allocate enough space)
    char* info = (char*)aMalloc(512);
    snprintf(info, 512,
             "Name: %s | Level: %d/%d | Job: %s | HP: %d/%d | Location: %s (%d,%d)",
             sd->status.name,
             sd->status.base_level,
             sd->status.job_level,
             job_name(sd->status.class_),
             sd->status.hp,
             sd->status.max_hp,
             mapindex_id2name(sd->mapindex),
             sd->bl.x,
             sd->bl.y);

    // Push to script - ownership transferred
    script_pushstr(st, info);

    return SCRIPT_CMD_SUCCESS;
}

// Registration:
BUILDIN_DEF(getplayerinfo,"s"),
```

### Example 7: Timer Integration (Advanced)
```cpp
/// Adds a delayed command execution
/// Usage: delaycmd <milliseconds>,"<command>";
BUILDIN_FUNC(delaycmd)
{
    map_session_data* sd;
    if (!script_rid2sd(sd))
        return SCRIPT_CMD_SUCCESS;

    int32 tick = script_getnum(st, 2);
    const char* command = script_getstr(st, 3);

    // Validate tick
    if (tick < 0) {
        ShowError("buildin_delaycmd: Delay cannot be negative (%d)\n", tick);
        return SCRIPT_CMD_FAILURE;
    }

    // Validate command
    if (strlen(command) == 0) {
        ShowError("buildin_delaycmd: Command cannot be empty\n");
        return SCRIPT_CMD_FAILURE;
    }

    // Create event name (must be allocated - timer system stores it)
    char* event = (char*)aMalloc(EVENT_NAME_LENGTH);
    snprintf(event, EVENT_NAME_LENGTH, "%s::OnDelayCmd_%d",
             ((npc_data*)map_id2bl(st->oid))->exname, sd->status.char_id);

    // Store command in temporary variable for event to execute
    char var_name[64];
    snprintf(var_name, sizeof(var_name), "$@delaycmd_%d$", sd->status.char_id);
    set_var_str(sd, var_name, command);

    // Add timer
    if (!pc_addeventtimer(sd, tick, event)) {
        ShowWarning("buildin_delaycmd: Failed to add timer\n");
        aFree(event);
        return SCRIPT_CMD_FAILURE;
    }

    return SCRIPT_CMD_SUCCESS;
}

// Registration:
BUILDIN_DEF(delaycmd,"is"),
```

---

## ⚠️ Common Mistakes & Crashes {#common-mistakes}

### Mistake 1: Pushing Stack Strings
```cpp
// ❌ WRONG - Will crash!
BUILDIN_FUNC(bad_example1) {
    char buffer[256];
    sprintf(buffer, "Result: %d", 123);
    script_pushstr(st, buffer);  // CRASH! Can't free stack memory
    return SCRIPT_CMD_SUCCESS;
}

// ✅ CORRECT
BUILDIN_FUNC(good_example1) {
    char buffer[256];
    sprintf(buffer, "Result: %d", 123);
    script_pushstr(st, aStrdup(buffer));  // Safe - heap allocation
    return SCRIPT_CMD_SUCCESS;
}

// ✅ ALSO CORRECT
BUILDIN_FUNC(good_example1_alt) {
    char* buffer = (char*)aMalloc(256);
    sprintf(buffer, "Result: %d", 123);
    script_pushstr(st, buffer);  // Safe - heap allocation
    return SCRIPT_CMD_SUCCESS;
}
```

### Mistake 2: Storing Temporary String Pointers
```cpp
// ❌ WRONG - Dangling pointer!
char* stored_string;

BUILDIN_FUNC(bad_example2) {
    const char* param = script_getstr(st, 2);
    stored_string = (char*)param;  // DANGER! Points to stack, will be freed
    return SCRIPT_CMD_SUCCESS;
}

// Later use:
void some_function() {
    ShowInfo("%s\n", stored_string);  // CRASH! Memory already freed
}

// ✅ CORRECT
char* stored_string = nullptr;

BUILDIN_FUNC(good_example2) {
    const char* param = script_getstr(st, 2);

    // Free old stored string if exists
    if (stored_string)
        aFree(stored_string);

    // Duplicate for storage
    stored_string = aStrdup(param);

    return SCRIPT_CMD_SUCCESS;
}
```

### Mistake 3: Memory Leaks on Error Paths
```cpp
// ❌ WRONG - Leaks memory!
BUILDIN_FUNC(bad_example3) {
    char* buffer = (char*)aMalloc(1024);

    int32 value = script_getnum(st, 2);
    if (value < 0) {
        ShowError("Invalid value!\n");
        return SCRIPT_CMD_FAILURE;  // LEAK! buffer not freed
    }

    sprintf(buffer, "Value: %d", value);
    script_pushstr(st, buffer);
    return SCRIPT_CMD_SUCCESS;
}

// ✅ CORRECT
BUILDIN_FUNC(good_example3) {
    int32 value = script_getnum(st, 2);

    // Validate BEFORE allocating
    if (value < 0) {
        ShowError("Invalid value!\n");
        return SCRIPT_CMD_FAILURE;
    }

    char* buffer = (char*)aMalloc(1024);
    sprintf(buffer, "Value: %d", value);
    script_pushstr(st, buffer);
    return SCRIPT_CMD_SUCCESS;
}

// ✅ ALSO CORRECT (if must allocate early)
BUILDIN_FUNC(good_example3_alt) {
    char* buffer = (char*)aMalloc(1024);

    int32 value = script_getnum(st, 2);
    if (value < 0) {
        ShowError("Invalid value!\n");
        aFree(buffer);  // Free before returning
        return SCRIPT_CMD_FAILURE;
    }

    sprintf(buffer, "Value: %d", value);
    script_pushstr(st, buffer);
    return SCRIPT_CMD_SUCCESS;
}
```

### Mistake 4: Not Validating References
```cpp
// ❌ WRONG - Will crash if passed non-reference!
BUILDIN_FUNC(bad_example4) {
    struct script_data* data = script_getdata(st, 2);
    const char* name = reference_getname(data);  // CRASH if not a reference!
    // ...
}

// ✅ CORRECT
BUILDIN_FUNC(good_example4) {
    struct script_data* data = script_getdata(st, 2);

    if (!data_isreference(data)) {
        ShowError("buildin_example4: Parameter must be a variable!\n");
        script_reportdata(data);
        st->state = END;
        return SCRIPT_CMD_FAILURE;
    }

    const char* name = reference_getname(data);
    // ... safe to use ...
}
```

### Mistake 5: Wrong Return String Type
```cpp
// ❌ WRONG - String will be freed!
BUILDIN_FUNC(bad_example5) {
    static const char* msg = "Hello World";  // Static/const
    script_pushstr(st, (char*)msg);  // CRASH! Will try to aFree() it
    return SCRIPT_CMD_SUCCESS;
}

// ✅ CORRECT
BUILDIN_FUNC(good_example5) {
    static const char* msg = "Hello World";
    script_pushconststr(st, (char*)msg);  // Safe - won't be freed
    return SCRIPT_CMD_SUCCESS;
}

// ✅ ALSO CORRECT
BUILDIN_FUNC(good_example5_alt) {
    const char* msg = "Hello World";
    script_pushstr(st, aStrdup(msg));  // Safe - new allocation
    return SCRIPT_CMD_SUCCESS;
}
```

### Mistake 6: Forgetting Player Attachment
```cpp
// ❌ WRONG - Crashes if no player attached!
BUILDIN_FUNC(bad_example6) {
    map_session_data* sd;
    script_rid2sd(sd);  // Returns false if no player, but we ignore it

    pc_heal(sd, 100, 0, 0);  // CRASH! sd might be nullptr
    return SCRIPT_CMD_SUCCESS;
}

// ✅ CORRECT
BUILDIN_FUNC(good_example6) {
    map_session_data* sd;
    if (!script_rid2sd(sd)) {
        ShowError("buildin_example6: No player attached!\n");
        return SCRIPT_CMD_FAILURE;
    }

    pc_heal(sd, 100, 0, 0);  // Safe - sd is valid
    return SCRIPT_CMD_SUCCESS;
}
```

### Mistake 7: Array Bounds Not Checked
```cpp
// ❌ WRONG - Can overflow!
BUILDIN_FUNC(bad_example7) {
    struct script_data* data = script_getdata(st, 2);
    uint32 count = script_getnum(st, 3);

    // No bounds check!
    for (uint32 i = 0; i < count; i++) {
        // Set array elements - might exceed SCRIPT_MAX_ARRAYSIZE
    }
}

// ✅ CORRECT
BUILDIN_FUNC(good_example7) {
    struct script_data* data = script_getdata(st, 2);
    uint32 start = reference_getindex(data);
    uint32 count = script_getnum(st, 3);

    // Check bounds
    if (start + count > SCRIPT_MAX_ARRAYSIZE)
        count = SCRIPT_MAX_ARRAYSIZE - start;

    for (uint32 i = 0; i < count; i++) {
        // Safe - within bounds
    }
}
```

**CRASH PREVENTION CHECKLIST:**
- ✅ Always validate references with `data_isreference()`
- ✅ Check player attachment with `script_rid2sd()` return value
- ✅ Use `script_pushstr()` only with heap-allocated strings
- ✅ Use `script_pushconststr()` for literals and const char*
- ✅ Free allocated memory on ALL return paths
- ✅ Never store `script_getstr()` results beyond function scope
- ✅ Always check array bounds against `SCRIPT_MAX_ARRAYSIZE`
- ✅ Validate parameter counts with `script_hasdata()`

---

## 🧪 Testing Your Commands {#testing}

### Basic Testing Script Template
```c
// test_mycommand.txt
prontera,150,150,4	script	TestMyCommand	100,{
    mes "Testing mycommand...";

    // Test 1: Basic functionality
    .result = mycommand(100, "test");
    mes "Test 1: Result = " + .result;

    // Test 2: Optional parameters
    .result = mycommand(100);
    mes "Test 2: With default = " + .result;

    // Test 3: Edge cases
    .result = mycommand(0, "");
    mes "Test 3: Edge case = " + .result;

    // Test 4: Invalid input (should show error)
    .result = mycommand(-1, "invalid");
    mes "Test 4: Invalid = " + .result;

    close;
}
```

### Testing Checklist
1. **Basic Functionality**
   - Command executes without crash
   - Returns expected values
   - Side effects work correctly

2. **Parameter Validation**
   - Missing required parameters
   - Wrong parameter types (if applicable)
   - Boundary values (0, -1, MAX_INT)
   - Empty strings

3. **Optional Parameters**
   - Command works without optional params
   - Default values are correct
   - Optional params override defaults

4. **Memory Management**
   - Run command 1000+ times (check for leaks)
   - Monitor memory usage
   - Use valgrind/address sanitizer if available

5. **Error Handling**
   - Invalid player attachment
   - Invalid variable references
   - Out of bounds array access
   - Null/invalid pointers

6. **Edge Cases**
   - Very long strings
   - Large numbers
   - Array size limits
   - Concurrent execution

### Debugging Tips
```cpp
// Add debug output during development
BUILDIN_FUNC(mycommand) {
    ShowDebug("mycommand: called with %d parameters\n", script_lastdata(st));

    for (int i = 2; script_hasdata(st, i); i++) {
        struct script_data* data = script_getdata(st, i);
        ShowDebug("  Param %d: type=%d\n", i, data->type);
    }

    // ... rest of function ...
}

// Use script_reportdata for parameter dumps
if (!data_isreference(data)) {
    ShowError("Expected reference!\n");
    script_reportdata(data);  // Shows detailed info about what was passed
    return SCRIPT_CMD_FAILURE;
}
```

### Memory Leak Detection
```bash
# Compile with address sanitizer
./configure --enable-debug
make clean
make

# Run server and execute commands
# Check output for memory leaks
```

---

## 📚 Cross-References

### Related Documentation
- **KB_REF_MemoryCrashPatterns.md** - Detailed memory management and crash prevention
- **KB_REF_ScriptTimerInternals.md** - Timer system integration for delayed commands

### Key Source Files
- **src/map/script.cpp** - All built-in command implementations
- **src/map/script.hpp** - Script engine structures and macros
- **src/common/malloc.cpp** - Memory allocation functions

### Important Functions
```cpp
// Player retrieval
bool script_rid2sd_(struct script_state *st, map_session_data** sd, const char *func);
bool script_accid2sd_(struct script_state *st, uint8 loc, map_session_data **sd, const char *func);
bool script_charid2sd_(struct script_state *st, uint8 loc, map_session_data **sd, const char *func);
bool script_nick2sd_(struct script_state *st, uint8 loc, map_session_data **sd, const char *func);

// Variable manipulation
bool set_reg_num(struct script_state* st, map_session_data* sd, int64 num,
                 const char* name, const int64 value, struct reg_db *ref);
bool set_reg_str(struct script_state* st, map_session_data* sd, int64 num,
                 const char* name, const char* value, struct reg_db* ref);

// Array helpers
uint32 script_array_size(struct script_state *st, map_session_data *sd,
                         const char *name, struct reg_db *ref);
uint32 script_array_highest_key(struct script_state *st, map_session_data *sd,
                                const char *name, struct reg_db *ref);

// Stack manipulation
void push_val(struct script_stack* stack, c_op type, int64 val);
void push_str(struct script_stack* stack, c_op type, char* str);
void pop_stack(struct script_state* st, int32 start, int32 end);
```

---

## 🎓 Summary

**Creating a script command requires:**
1. Implement `BUILDIN_FUNC(commandname)` function
2. Extract parameters with `script_getnum/script_getstr/script_getdata`
3. Validate all inputs (nullpo checks, bounds, types)
4. Execute server logic
5. Push return value with `script_pushint/script_pushstr/script_pushconststr`
6. Register with `BUILDIN_DEF(commandname, "argument_pattern")`
7. Test thoroughly (basic, edge cases, memory leaks)

**Memory Management Rules:**
- `script_pushstr()` - Takes ownership, must be heap-allocated
- `script_pushconststr()` - Does NOT take ownership, must never be freed
- Always use `aStrdup()` to copy strings for storage
- Free all allocations on error paths

**Common Patterns:**
```cpp
// Template for most commands:
BUILDIN_FUNC(mycommand) {
    // 1. Get player (if needed)
    map_session_data* sd;
    if (!script_rid2sd(sd))
        return SCRIPT_CMD_SUCCESS;

    // 2. Get parameters
    int32 param1 = script_getnum(st, 2);

    // 3. Validate
    if (param1 < 0)
        return SCRIPT_CMD_FAILURE;

    // 4. Execute
    // ... logic ...

    // 5. Return
    script_pushint(st, result);
    return SCRIPT_CMD_SUCCESS;
}
```

**For Advanced Use Cases:**
- Study existing commands in script.cpp
- Reference KB_REF_MemoryCrashPatterns.md for safety
- Reference KB_REF_ScriptTimerInternals.md for timers
- Use `#ifdef DEBUG` for development logging
- Test with valgrind/ASAN for memory safety

---

**Document Size:** ~18KB
**Last Updated:** 2024-01-15
**Maintainer:** rAthena Development Team
