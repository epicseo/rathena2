---
kb_id: KB_REF_023
title: "Creating Custom Script Commands in C++"
category: Source Code
keywords: [script_commands, BUILDIN, custom_commands, script_getnum, script_getstr, script_pushint, script_pushstr, script.cpp, parameter_handling]
related_files: [
  "src/map/script.cpp",
  "src/map/script.hpp"
]
difficulty: expert
use_case: "Adding custom script commands to rAthena for use in NPC scripts"
version: rAthena 2024
last_updated: 2024-01-15
---

# Creating Custom Script Commands in C++

## Quick Reference

### **Basic Template**
```cpp
// In src/map/script.cpp

/**
 * mycommand(<param1>, <param2>)
 * Description of what it does
 * @param param1: Description
 * @param param2: Description
 * @return: What it returns
 */
BUILDIN(mycommand) {
    // Get parameters
    int param1 = script_getnum(st, 2);
    const char *param2 = script_getstr(st, 3);
    
    // Your logic here
    
    // Return value
    script_pushint(st, 1);
    return true;
}
```

### **Registration**
```cpp
// In src/map/script.cpp, find BUILDIN_DEF() section
BUILDIN_DEF(mycommand, "is"),  // i=int, s=string
```

---

## Table of Contents
1. [BUILDIN Macro](#buildin-macro)
2. [Parameter Handling](#parameter-handling)
3. [Return Values](#return-values)
4. [Complete Examples](#complete-examples)
5. [Advanced Patterns](#advanced-patterns)
6. [Common Pitfalls](#common-pitfalls)

---

## BUILDIN Macro

### **Definition**
```cpp
#define BUILDIN(x) bool buildin_ ## x (struct script_state *st)
```

Expands to:
```cpp
BUILDIN(mycommand)
// Becomes:
bool buildin_mycommand(struct script_state *st)
```

### **Parameters**
```cpp
struct script_state *st  // Script execution state
```

Contains:
- `st->stack` - Parameter stack
- `st->script` - Current script
- `st->oid` - NPC object ID
- `st->rid` - Attached player RID

---

## Parameter Handling

### **Getting Parameters**

**script_getnum()** - Get integer
```cpp
int value = script_getnum(st, 2);  // 2 = first parameter
```

**script_getstr()** - Get string
```cpp
const char *text = script_getstr(st, 2);
```

**script_getdata()** - Get raw data
```cpp
struct script_data *data = script_getdata(st, 2);
```

**script_hasdata()** - Check if parameter exists
```cpp
if (script_hasdata(st, 3)) {
    // Optional third parameter exists
}
```

**script_rid2sd()** - Get attached player
```cpp
struct map_session_data *sd = script_rid2sd(st);
if (!sd) {
    ShowError("No player attached!\n");
    return false;
}
```

### **Parameter Types**

**Type Codes** (for BUILDIN_DEF):
- `i` - Integer (int32)
- `s` - String (const char*)
- `l` - Label (for goto/menu)
- `r` - Reference (variable reference)
- `*` - Optional parameters
- `?` - End of parameters

Examples:
```cpp
BUILDIN_DEF(mycommand, "i"),      // 1 int
BUILDIN_DEF(mycommand, "is"),     // int, string
BUILDIN_DEF(mycommand, "i*"),     // int + optional params
BUILDIN_DEF(mycommand, "is?"),    // int, optional string
```

---

## Return Values

**script_pushint()** - Return integer
```cpp
script_pushint(st, 100);
return true;
```

**script_pushstr()** - Return string (will be freed)
```cpp
char *str = aStrdup("Hello");
script_pushstr(st, str);
return true;
```

**script_pushconststr()** - Return constant string
```cpp
script_pushconststr(st, "Constant");
return true;
```

**No return value**
```cpp
return true;  // Command succeeds, no return
```

**Return 0 for variables**
```cpp
script_pushint(st, 0);  // For commands that set variables
return true;
```

---

## Complete Examples

### **Example 1: Simple Command (No Parameters)**
```cpp
/**
 * servertime()
 * Returns current server timestamp
 * @return: Unix timestamp
 */
BUILDIN(servertime) {
    time_t now = time(NULL);
    script_pushint(st, (int)now);
    return true;
}

// Registration
BUILDIN_DEF(servertime, ""),  // No parameters
```

**Usage in script:**
```c
.@time = servertime();
mes "Server time: " + .@time;
```

---

### **Example 2: With Required Parameters**
```cpp
/**
 * customheal(<amount>, <show_effect>)
 * Heal player with custom effect
 * @param amount: HP to heal
 * @param show_effect: 1=show effect, 0=silent
 * @return: 1=success, 0=fail
 */
BUILDIN(customheal) {
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) {
        script_pushint(st, 0);
        return false;
    }
    
    int amount = script_getnum(st, 2);
    int show_effect = script_getnum(st, 3);
    
    // Heal player
    pc_heal(sd, amount, 0, show_effect ? 1 : 0);
    
    script_pushint(st, 1);
    return true;
}

// Registration
BUILDIN_DEF(customheal, "ii"),  // 2 integers
```

**Usage:**
```c
customheal(500, 1);  // Heal 500 HP with effect
```

---

### **Example 3: With Optional Parameters**
```cpp
/**
 * givebonus(<type>, <value>{, <duration>})
 * Give temporary bonus to player
 * @param type: Bonus type (1=ATK, 2=MATK, etc.)
 * @param value: Bonus value
 * @param duration: Optional duration in seconds (default 60)
 * @return: 1=success, 0=fail
 */
BUILDIN(givebonus) {
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) {
        script_pushint(st, 0);
        return false;
    }
    
    int type = script_getnum(st, 2);
    int value = script_getnum(st, 3);
    int duration = script_hasdata(st, 4) ? script_getnum(st, 4) : 60;
    
    // Apply bonus (simplified)
    switch(type) {
        case 1:  // ATK bonus
            sc_start(NULL, &sd->bl, SC_BLESSING, 100, value, duration * 1000);
            break;
        case 2:  // MATK bonus
            sc_start(NULL, &sd->bl, SC_INCREASEAGI, 100, value, duration * 1000);
            break;
    }
    
    script_pushint(st, 1);
    return true;
}

// Registration
BUILDIN_DEF(givebonus, "ii?"),  // 2 int, 1 optional int
```

**Usage:**
```c
givebonus(1, 100);      // ATK +100 for 60 seconds (default)
givebonus(1, 100, 120); // ATK +100 for 120 seconds
```

---

### **Example 4: String Parameters**
```cpp
/**
 * announceto(<player_name>, <message>)
 * Send announcement to specific player
 * @param player_name: Character name
 * @param message: Message text
 * @return: 1=found, 0=not found
 */
BUILDIN(announceto) {
    const char *name = script_getstr(st, 2);
    const char *message = script_getstr(st, 3);
    
    struct map_session_data *target_sd = map->nick2sd(name, false);
    if (!target_sd) {
        script_pushint(st, 0);
        return true;
    }
    
    clif->broadcast(&target_sd->bl, message, strlen(message) + 1, 
                    BC_DEFAULT, SELF);
    
    script_pushint(st, 1);
    return true;
}

// Registration
BUILDIN_DEF(announceto, "ss"),  // 2 strings
```

**Usage:**
```c
.@result = announceto("PlayerName", "Hello!");
if (.@result == 0) {
    mes "Player not found";
}
```

---

### **Example 5: Variable Reference**
```cpp
/**
 * getplayerinfo(<char_id>, <.variable>)
 * Get player info and store in variable
 * @param char_id: Character ID
 * @param variable: Variable reference to store info
 */
BUILDIN(getplayerinfo) {
    int char_id = script_getnum(st, 2);
    struct script_data *data = script_getdata(st, 3);
    
    if (!data_isreference(data)) {
        ShowError("getplayerinfo: Second parameter must be a variable!\n");
        script_reportfunc(st);
        return false;
    }
    
    // Get player data (simplified)
    struct map_session_data *target_sd = map->charid2sd(char_id);
    if (!target_sd) {
        set_reg(st, NULL, reference_uid(reference_getid(data), reference_getindex(data)),
                reference_getname(data), (void *)0, reference_getref(data));
        return true;
    }
    
    // Store player level in variable
    set_reg(st, NULL, reference_uid(reference_getid(data), reference_getindex(data)),
            reference_getname(data), (void *)__64BPTRSIZE(target_sd->status.base_level), 
            reference_getref(data));
    
    return true;
}

// Registration
BUILDIN_DEF(getplayerinfo, "ir"),  // int, reference
```

**Usage:**
```c
getplayerinfo(150000, .@level);
mes "Player level: " + .@level;
```

---

## Advanced Patterns

### **Array Return**
```cpp
/**
 * getpartylevels()
 * Get all party member levels as array
 * Sets .@levels[] array
 */
BUILDIN(getpartylevels) {
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd || !sd->status.party_id) {
        script_pushint(st, 0);
        return true;
    }
    
    struct party_data *p = party->search(sd->status.party_id);
    if (!p) {
        script_pushint(st, 0);
        return true;
    }
    
    int count = 0;
    for (int i = 0; i < MAX_PARTY; i++) {
        if (p->party.member[i].account_id) {
            struct map_session_data *psd = map->charid2sd(p->party.member[i].char_id);
            if (psd) {
                // Set array element
                setd_sub_num(st, NULL, ".@levels", count, 
                             psd->status.base_level, NULL);
                count++;
            }
        }
    }
    
    script_pushint(st, count);
    return true;
}
```

---

### **SQL Query**
```cpp
/**
 * sqlcount(<query>)
 * Count rows from SQL query
 * @param query: SQL SELECT COUNT(*) query
 * @return: Row count
 */
BUILDIN(sqlcount) {
    const char *query = script_getstr(st, 2);
    
    if (SQL_ERROR == SQL->Query(map->mysql_handle, query)) {
        Sql_ShowDebug(map->mysql_handle);
        script_pushint(st, 0);
        return false;
    }
    
    int count = 0;
    if (SQL_SUCCESS == SQL->NextRow(map->mysql_handle)) {
        char *data;
        SQL->GetData(map->mysql_handle, 0, &data, NULL);
        count = atoi(data);
    }
    
    SQL->FreeResult(map->mysql_handle);
    script_pushint(st, count);
    return true;
}
```

---

### **Timer Callback**
```cpp
// Timer callback
int my_timer_func(int tid, int64 tick, int id, intptr_t data) {
    struct map_session_data *sd = map->id2sd(id);
    if (!sd) return 0;
    
    clif->message(sd->fd, "Timer expired!");
    return 0;
}

/**
 * settimer(<seconds>)
 * Set a timer for attached player
 */
BUILDIN(settimer) {
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) return false;
    
    int seconds = script_getnum(st, 2);
    add_timer(gettick() + (seconds * 1000), my_timer_func, sd->bl.id, 0);
    
    return true;
}
```

---

## Common Pitfalls

### **1. Memory Management**
```cpp
// ❌ WRONG - Memory leak
BUILDIN(badcommand) {
    char *str = (char *)aMalloc(100);
    strcpy(str, "Hello");
    script_pushstr(st, str);  // str will never be freed!
    return true;
}

// ✅ CORRECT - Use aStrdup for strings returned to script
BUILDIN(goodcommand) {
    script_pushstr(st, aStrdup("Hello"));  // Script engine will free this
    return true;
}
```

### **2. Null Pointer Check**
```cpp
// ❌ WRONG - Crash if no player attached
BUILDIN(badcommand) {
    struct map_session_data *sd = script_rid2sd(st);
    pc_heal(sd, 100, 0, 0);  // CRASH if sd is NULL!
    return true;
}

// ✅ CORRECT - Always check
BUILDIN(goodcommand) {
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) {
        ShowError("goodcommand: No player attached!\n");
        return false;
    }
    pc_heal(sd, 100, 0, 0);
    return true;
}
```

### **3. Parameter Count**
```cpp
// ❌ WRONG - Not checking optional params
BUILDIN(badcommand) {
    int param = script_getnum(st, 3);  // May not exist!
    return true;
}

// ✅ CORRECT - Check first
BUILDIN(goodcommand) {
    int param = script_hasdata(st, 3) ? script_getnum(st, 3) : 0;
    return true;
}
```

### **4. String Handling**
```cpp
// ❌ WRONG - Modifying const string
BUILDIN(badcommand) {
    const char *str = script_getstr(st, 2);
    str[0] = 'X';  // CRASH! String is const!
    return true;
}

// ✅ CORRECT - Copy if you need to modify
BUILDIN(goodcommand) {
    const char *str = script_getstr(st, 2);
    char *copy = aStrdup(str);
    copy[0] = 'X';
    // Use copy...
    aFree(copy);
    return true;
}
```

---

## Registration Location

**Find this section in src/map/script.cpp:**
```cpp
void script_parse_builtin(void) {
    struct script_function BUILDIN_DEF[] = {
        // Core commands
        BUILDIN_DEF(mes, "s*"),
        BUILDIN_DEF(next, ""),
        BUILDIN_DEF(close, ""),
        
        // ... hundreds of commands ...
        
        // Add your custom commands here
        BUILDIN_DEF(mycommand, "is"),
        BUILDIN_DEF(customheal, "ii"),
        
        {NULL, NULL, NULL},  // End marker
    };
    
    // Registration code...
}
```

---

## Testing

### **1. Compile**
```bash
make clean
make -j$(nproc)
```

### **2. Test Script**
```c
prontera,150,150,4	script	Test	123,{
	.@result = mycommand(100, "test");
	mes "Result: " + .@result;
	close;
}
```

### **3. Check Console**
Look for errors:
```
[Error]: script:mycommand: ...
```

---

## Related References

- **Source Structure**: [KB_REF_SourceCodeStructure.md]
- **Plugin System**: [KB_REF_PluginSystem.md]
- **Best Practices**: [KB_REF_SourceCodeBestPractices.md]

---

**End of KB_REF_023 - Creating Custom Script Commands**
