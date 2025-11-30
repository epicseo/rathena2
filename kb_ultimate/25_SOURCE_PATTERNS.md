# rAthena Source Code Patterns
## C++ Development Reference for rAthena

---

<!-- RAG_CHUNK: source_overview_001 -->
## Source Code Structure

### Directory Layout
```
src/
├── char/           # Character server
├── common/         # Shared code
├── config/         # Configuration headers
├── login/          # Login server
├── map/            # Map server (main game logic)
│   ├── atcommand.cpp   # @commands
│   ├── battle.cpp      # Battle calculations
│   ├── clif.cpp        # Client interface (packets)
│   ├── mob.cpp         # Monster AI/behavior
│   ├── npc.cpp         # NPC handling
│   ├── pc.cpp          # Player character
│   ├── script.cpp      # Script engine (BUILDIN_FUNC)
│   ├── skill.cpp       # Skill handling
│   └── status.cpp      # Status effects
└── web/            # Web server
```

---

<!-- RAG_CHUNK: buildin_func_001 -->
## Script Commands (BUILDIN_FUNC)

### Basic Pattern
```cpp
// In src/map/script.cpp

BUILDIN_FUNC(mycommand)
{
    // Get script state
    struct script_state* st = script_state;

    // Get arguments
    int arg1 = script_getnum(st, 2);  // First arg
    const char* arg2 = script_getstr(st, 3);  // Second arg

    // Optional argument with default
    int arg3 = script_hasdata(st, 4) ? script_getnum(st, 4) : 0;

    // Get attached player
    struct map_session_data* sd;
    if (!script_rid2sd(sd)) {
        // No player attached
        script_pushint(st, 0);
        return SCRIPT_CMD_FAILURE;
    }

    // Do something...

    // Return value
    script_pushint(st, 1);  // or script_pushstr(st, "string")
    return SCRIPT_CMD_SUCCESS;
}
```

### Registration
```cpp
// In script.cpp def_buildin[] array
BUILDIN_DEF(mycommand, "is?"),  // i=int, s=string, ?=optional

// Type specifiers:
// i = integer
// s = string
// v = variable reference
// l = label
// r = reference
// ? = optional start
// * = varargs
```

### Complete Example
```cpp
/**
 * myfunc(<player_name>, <amount>{, <item_id>})
 * Give items to player by name
 */
BUILDIN_FUNC(myfunc)
{
    struct script_state* st = script_state;

    // Get required arguments
    const char* name = script_getstr(st, 2);
    int amount = script_getnum(st, 3);

    // Optional item_id, default to Red Potion
    t_itemid item_id = script_hasdata(st, 4) ? script_getnum(st, 4) : 501;

    // Find player by name
    struct map_session_data* sd = map_nick2sd(name, false);
    if (sd == nullptr) {
        ShowWarning("myfunc: player '%s' not found\n", name);
        script_pushint(st, 0);
        return SCRIPT_CMD_SUCCESS;
    }

    // Create item
    struct item item = {};
    item.nameid = item_id;
    item.identify = 1;
    item.amount = amount;

    // Add to player inventory
    if (pc_additem(sd, &item, amount, LOG_TYPE_SCRIPT) != ADDITEM_SUCCESS) {
        script_pushint(st, 0);
        return SCRIPT_CMD_SUCCESS;
    }

    script_pushint(st, 1);
    return SCRIPT_CMD_SUCCESS;
}

// Register: BUILDIN_DEF(myfunc, "si?"),
```

---

<!-- RAG_CHUNK: atcommand_001 -->
## AT Commands (ACMD_FUNC)

### Basic Pattern
```cpp
// In src/map/atcommand.cpp

ACMD_FUNC(myatcmd)
{
    // sd = invoking player
    // command = full command string
    // message = arguments after command

    nullpo_retr(-1, sd);

    // Parse arguments
    char name[NAME_LENGTH];
    int value;

    if (!message || !*message || sscanf(message, "%23s %d", name, &value) < 2) {
        clif_displaymessage(fd, "Usage: @myatcmd <name> <value>");
        return -1;
    }

    // Do something...

    clif_displaymessage(fd, "Success!");
    return 0;
}
```

### Registration
```cpp
// In atcommand.cpp atcommand_def[] array
ACMD_DEF(myatcmd),

// Or with alias:
ACMD_DEF2("alias", myatcmd),
```

### Permission Check
```cpp
ACMD_FUNC(protected_cmd)
{
    nullpo_retr(-1, sd);

    // Check group permission
    if (!pc_has_permission(sd, PC_PERM_MY_PERMISSION)) {
        clif_displaymessage(fd, "You don't have permission.");
        return -1;
    }

    // Continue...
    return 0;
}
```

---

<!-- RAG_CHUNK: status_effect_001 -->
## Status Effects (SC_*)

### Adding New Status

**1. Define constant in status.hpp:**
```cpp
enum sc_type : int16 {
    // ...existing entries...
    SC_MYEFFECT,
    // ...
    SC_MAX,
};
```

**2. Add to status_db.yml:**
```yaml
Body:
  - Status: MyEffect
    Icon: EFST_MYEFFECT      # Client effect icon
    DurationLookup: MYSKILL  # Skill for duration calc
    CalcFlags:
      Atk: true              # Triggers status_calc_atk
    Flags:
      NoSave: true           # Don't save on logout
      NoBoss: true           # Immune if boss
```

**3. Implement in status.cpp:**
```cpp
// In status_change_start_sub
case SC_MYEFFECT:
    val2 = val1 * 10;  // Calculate val2 based on val1
    if (val2 > 100)
        val2 = 100;
    break;

// In status_calc_xxx (for stat modifications)
case SC_MYEFFECT:
    batk += sc->data[SC_MYEFFECT]->val2;
    break;

// In status_change_end_sub (cleanup)
case SC_MYEFFECT:
    // Any cleanup code
    break;
```

---

<!-- RAG_CHUNK: packet_handling_001 -->
## Packet Handling (clif.cpp)

### Receiving Packets
```cpp
// In clif.cpp

void clif_parse_MyPacket(int fd, struct map_session_data *sd)
{
    // Validate
    if (sd == nullptr)
        return;

    // Read packet data
    int value = RFIFOL(fd, 2);  // Read long at offset 2
    const char* str = RFIFOCP(fd, 6);  // Read string at offset 6

    // Process...

    // Clear read buffer (automatically handled usually)
}
```

### Sending Packets
```cpp
void clif_mypacket(struct map_session_data* sd, int value)
{
    if (sd == nullptr)
        return;

    int fd = sd->fd;

    WFIFOHEAD(fd, 10);
    WFIFOW(fd, 0) = 0x1234;     // Packet ID
    WFIFOL(fd, 2) = sd->bl.id;  // Account ID
    WFIFOL(fd, 6) = value;      // Data
    WFIFOSET(fd, 10);
}
```

### Packet Registration
```cpp
// In clif_packetdb.hpp
packet(0x1234, 10, clif_parse_MyPacket, 2, 6);
// packet(ID, size, handler, offsets...)
```

---

<!-- RAG_CHUNK: skill_implementation_001 -->
## Skill Implementation

### Adding New Skill

**1. Define in skill.hpp:**
```cpp
enum e_skill {
    // ...
    MY_SKILL = 3000,
    // ...
};
```

**2. Add to skill_db.yml:**
```yaml
Body:
  - Id: 3000
    Name: MY_SKILL
    Description: My Custom Skill
    MaxLevel: 10
    Type: Weapon
    TargetType: Attack
    DamageFlags:
      Splash: true
    Range: 3
    Hit: Single
    HitCount: 1
    CastTime:
      - Level: 1
        Time: 500
      - Level: 10
        Time: 100
    Cooldown: 3000
    Requires:
      SpCost:
        - Level: 1
          Amount: 20
```

**3. Implement in skill.cpp:**
```cpp
// In skill_castend_damage_id or skill_castend_nodamage_id
case MY_SKILL:
{
    int damage = skill_get_num(skill_id, skill_lv) * 100;
    damage = damage * status_get_batk(src) / 100;

    clif_skill_nodamage(src, bl, skill_id, skill_lv, 1);
    battle_damage(src, bl, damage, 0);

    // Apply status effect
    sc_start(src, bl, SC_MYEFFECT, 100, skill_lv, 10000);
    break;
}
```

---

<!-- RAG_CHUNK: database_access_001 -->
## Database Access

### SQL Queries
```cpp
#include "common/sql.hpp"

// Simple query
if (SQL_ERROR == Sql_Query(sql_handle,
    "SELECT `name` FROM `char` WHERE `account_id` = %d",
    account_id))
{
    Sql_ShowDebug(sql_handle);
    return;
}

// Process results
while (SQL_SUCCESS == Sql_NextRow(sql_handle)) {
    char* name;
    Sql_GetData(sql_handle, 0, &name, nullptr);
    // Use name...
}
Sql_FreeResult(sql_handle);
```

### Escape Strings
```cpp
char escaped_name[NAME_LENGTH * 2 + 1];
Sql_EscapeStringLen(sql_handle, escaped_name, name, strlen(name));
```

---

<!-- RAG_CHUNK: timer_system_001 -->
## Timer System

### Add Timer
```cpp
// One-shot timer
add_timer(gettick() + 5000, my_timer_func, sd->bl.id, 0);

// Repeating timer
int timer_id = add_timer_interval(gettick() + 1000, my_timer_func, 0, 0, 1000);

// Timer callback
static TIMER_FUNC(my_timer_func)
{
    // id = timer ID
    // tick = current tick
    // data = custom data passed

    struct map_session_data* sd = map_id2sd(id);
    if (sd == nullptr)
        return 0;

    // Do something...

    return 0;
}
```

### Delete Timer
```cpp
delete_timer(timer_id, my_timer_func);
```

---

<!-- RAG_CHUNK: common_patterns_001 -->
## Common Patterns

### Null Pointer Check
```cpp
nullpo_ret(sd);      // Return if null
nullpo_retr(-1, sd); // Return -1 if null
nullpo_retv(sd);     // Return void if null
```

### Player Lookup
```cpp
// By account ID
struct map_session_data* sd = map_id2sd(account_id);

// By name
struct map_session_data* sd = map_nick2sd(name, false);

// By character ID
struct map_session_data* sd = map_charid2sd(char_id);
```

### Item Operations
```cpp
// Create item struct
struct item item = {};
item.nameid = item_id;
item.identify = 1;
item.amount = 1;

// Add to inventory
e_additem_result result = pc_additem(sd, &item, amount, LOG_TYPE_SCRIPT);

// Delete from inventory
pc_delitem(sd, index, amount, 0, DELITEM_NORMAL, LOG_TYPE_SCRIPT);
```

### Show Messages
```cpp
ShowStatus("Status message\n");
ShowInfo("Info message\n");
ShowNotice("Notice message\n");
ShowWarning("Warning message\n");
ShowError("Error message\n");
ShowFatalError("Fatal error\n");
ShowDebug("Debug message\n");  // Only in debug build
```

---

#rathena #source #cpp #buildin #atcommand #status #skill #packet #development
