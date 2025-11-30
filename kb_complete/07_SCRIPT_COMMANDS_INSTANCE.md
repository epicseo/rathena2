# rAthena Script Commands - Instance Reference
## Complete Instance System Commands

---

<!-- RAG_CHUNK: instance_overview_001 -->
## Instance System Overview

### How Instances Work
1. Define instance in `db/instance_db.yml`
2. Create instance with `instance_create`
3. Players enter with `instance_enter`
4. Instance runs until destroyed or timeout

### Instance Database (db/instance_db.yml)
```yaml
Body:
  - Id: 1
    Name: My Instance
    TimeLimit: 3600        # 1 hour
    IdleTimeOut: 300       # 5 min idle destroy
    Enter:
      Map: 1@myinstance
      X: 50
      Y: 50
    AdditionalMaps:
      2@myinstance: true
```

---

<!-- RAG_CHUNK: instance_create_001 -->
## Instance Creation

### instance_create
**Syntax:** `instance_create("<instance name>"{,<owner id>{,<owner type>{,<mode>}}})`

Create a new instance. Returns instance ID or failure.

**Owner Types:**
```c
IOT_NONE    // No owner (0)
IOT_CHAR    // Character (1)
IOT_PARTY   // Party (2)
IOT_GUILD   // Guild (3)
IOT_CLAN    // Clan (4)
```

**Modes:**
```c
IM_NONE     // No respawn (0)
IM_CHAR     // Respawn as character (1)
IM_PARTY    // Respawn for party (2)
IM_GUILD    // Respawn for guild (3)
IM_CLAN     // Respawn for clan (4)
```

**Return Values:**
```c
>= 0                      // Instance ID (success)
-1                        // Invalid instance name
-2                        // Cannot create instance
-3                        // Already have instance of type
-4                        // Invalid party/guild
```

**Examples:**
```c
// Party instance
.@party_id = getcharid(1);
.@inst = instance_create("Endless Tower", .@party_id, IOT_PARTY);
if (.@inst < 0) {
    mes "Failed to create instance!";
    close;
}

// Character instance
.@inst = instance_create("Solo Dungeon", getcharid(0), IOT_CHAR);

// Guild instance
.@inst = instance_create("Guild Dungeon", getcharid(2), IOT_GUILD);
```

---

### instance_destroy
**Syntax:** `instance_destroy({<instance id>});`

Destroy instance and warp out all players.

**Example:**
```c
OnInstanceComplete:
    announce "Instance complete! You have 60 seconds.",bc_map;
    sleep 60000;
    instance_destroy();
    end;
```

---

<!-- RAG_CHUNK: instance_enter_001 -->
## Instance Entry

### instance_enter
**Syntax:** `instance_enter("<instance name>"{,<x>,<y>{,<instance id>}});`

Enter instance.

**Returns:**
```c
IE_OK          // Success (0)
IE_NOMEMBER    // Party/guild not found (1)
IE_NOINSTANCE  // Instance not found (2)
IE_BUSY        // Instance in creation (3)
IE_OTHER       // Other error (4)
```

**Example:**
```c
// Check party instance and enter
if (instance_check_party(getcharid(1))) {
    .@result = instance_enter("Endless Tower");
    if (.@result != IE_OK) {
        mes "Cannot enter instance!";
        close;
    }
} else {
    mes "No instance found. Create one first.";
}
```

---

### instance_warpall
**Syntax:** `instance_warpall("<map>",<x>,<y>{,<instance id>});`

Warp all players in instance.

---

<!-- RAG_CHUNK: instance_check_001 -->
## Instance Checking

### instance_check_party
**Syntax:** `instance_check_party(<party id>{,<amount>{,<min level>{,<max level>}}})`

Check if party can enter/create instance.

**Parameters:**
- `amount` = Minimum party members required
- `min/max level` = Level restrictions

**Returns:**
```c
>= 0           // Instance ID if exists
-1             // Party not found
-2             // Not enough members
-3             // Members outside level range
```

**Example:**
```c
.@party_id = getcharid(1);
.@check = instance_check_party(.@party_id, 2, 50, 99);

if (.@check == -1) {
    mes "You are not in a party!";
} else if (.@check == -2) {
    mes "Need at least 2 party members!";
} else if (.@check == -3) {
    mes "All members must be Lv50-99!";
} else {
    // Party can enter
}
```

---

### instance_check_guild
**Syntax:** `instance_check_guild(<guild id>{,<amount>{,<min level>{,<max level>}}})`

Check guild instance requirements.

---

### instance_check_clan
**Syntax:** `instance_check_clan(<clan id>{,<amount>{,<min level>{,<max level>}}})`

Check clan instance requirements.

---

### instance_id
**Syntax:** `instance_id({<type>})`

Get instance ID.

**Types:**
```c
IM_NONE    // Current instance (0)
IM_CHAR    // Character instance (1)
IM_PARTY   // Party instance (2)
IM_GUILD   // Guild instance (3)
IM_CLAN    // Clan instance (4)
```

---

<!-- RAG_CHUNK: instance_info_001 -->
## Instance Information

### instance_info
**Syntax:** `instance_info("<instance name>",<type>{,<instance id>})`

Get instance database info.

**Types:**
```c
IIT_ID              // Instance ID (0)
IIT_TIME_LIMIT      // Time limit (1)
IIT_IDLE_TIMEOUT    // Idle timeout (2)
IIT_ENTER_MAP       // Entry map name (3)
IIT_ENTER_X         // Entry X coord (4)
IIT_ENTER_Y         // Entry Y coord (5)
IIT_MAPCOUNT        // Map count (6)
IIT_MAP             // Map by index (7)
```

---

### instance_live_info
**Syntax:** `instance_live_info("<instance name>",<type>{,<instance id>})`

Get live instance data.

**Types:**
```c
ILI_ID              // Instance ID (0)
ILI_OWNER           // Owner ID (1)
ILI_OWNER_TYPE      // Owner type (2)
ILI_CREATE_TIME     // Creation time (3)
ILI_ENTER_TIME      // Last enter time (4)
ILI_MEMBER_COUNT    // Player count (5)
```

---

### instance_list
**Syntax:** `instance_list("<instance name>"{,<type>})`

Get list of active instances.

**Returns array:** `$@instance_list[]`

---

<!-- RAG_CHUNK: instance_maps_001 -->
## Instance Maps

### instance_mapname
**Syntax:** `instance_mapname("<map>"{,<instance id>})`

Get instanced map name.

**Example:**
```c
.@map$ = instance_mapname("1@tower");  // Returns "1@tower001" etc.
```

---

### instance_npcname
**Syntax:** `instance_npcname("<npc name>"{,<instance id>})`

Get instanced NPC name.

---

### instance_announce
**Syntax:** `instance_announce(<instance id>,"<message>",<flag>{,<font color>{,<font type>{,<font size>{,<font align>{,<font y>}}}}})`

Announce to instance.

**Example:**
```c
instance_announce instance_id(), "Boss has spawned!", bc_map, 0xFF0000;
```

---

<!-- RAG_CHUNK: instance_variables_001 -->
## Instance Variables

### Instance Variable Prefix
Use `'` prefix for instance-scoped variables.

```c
'instance_var = 1;    // Integer
'instance_str$ = "text";  // String
```

### getinstancevar / setinstancevar
**Syntax:** `getinstancevar(<variable>,<instance id>)`
**Syntax:** `setinstancevar(<variable>,<value>,<instance id>)`

Access instance variables from outside.

---

<!-- RAG_CHUNK: instance_example_001 -->
## Complete Instance Example

```c
// Instance entry NPC
prontera,155,180,5	script	Instance Guide	4_F_KAFRA1,{
    mes "[Instance Guide]";
    mes "Welcome to the Instance System!";
    next;

    switch(select("Create Instance:Enter Instance:Info:Cancel")) {
        case 1:
            if (getcharid(1) == 0) {
                mes "[Instance Guide]";
                mes "You need to be in a party!";
                close;
            }

            .@check = instance_check_party(getcharid(1), 1, 50);
            if (.@check < 0) {
                if (.@check == -2)
                    mes "Need at least 1 party member!";
                else if (.@check == -3)
                    mes "All members must be Lv50+!";
                else
                    mes "Error checking party!";
                close;
            }

            if (.@check > 0) {
                mes "[Instance Guide]";
                mes "Instance already exists!";
                close;
            }

            .@inst = instance_create("My Instance", getcharid(1), IOT_PARTY);
            if (.@inst < 0) {
                mes "[Instance Guide]";
                mes "Failed to create instance!";
                close;
            }

            mes "[Instance Guide]";
            mes "Instance created!";
            mes "You can now enter.";
            close;

        case 2:
            .@result = instance_enter("My Instance");
            if (.@result != IE_OK) {
                mes "[Instance Guide]";
                mes "Cannot enter instance!";
                close;
            }
            end;

        case 3:
            mes "[Instance Guide]";
            mes "Time Limit: 1 hour";
            mes "Level Req: 50+";
            mes "Party Size: 1-12";
            close;

        case 4:
            close;
    }
}

// Instance NPCs (defined with instance map)
1@myinstance,50,55,5	script	Instance NPC	4_M_01,{
    mes "[Instance NPC]";
    mes "Defeat all monsters!";
    mes "Monsters remaining: " + 'mob_count;
    close;

OnInstanceInit:
    'mob_count = 20;
    monster instance_mapname("1@myinstance"),0,0,"Monster",1002,20,strnpcinfo(0)+"::OnMobDead";
    end;

OnMobDead:
    'mob_count--;
    instance_announce instance_id(), "Monsters remaining: " + 'mob_count, bc_map;

    if ('mob_count <= 0) {
        instance_announce instance_id(), "All monsters defeated! Boss spawning...", bc_map;
        monster instance_mapname("1@myinstance"),50,50,"Boss",1039,1,strnpcinfo(0)+"::OnBossDead";
    }
    end;

OnBossDead:
    instance_announce instance_id(), "Boss defeated! Congratulations!", bc_map;
    getitem 607, 5;  // Yggdrasil Berry

    sleep 5000;
    instance_announce instance_id(), "Warping out in 30 seconds...", bc_map;
    sleep 30000;
    instance_destroy();
    end;
}
```

---

#rathena #script #instance #dungeon #party #commands
