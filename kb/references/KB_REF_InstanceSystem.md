---
kb_id: KB_REF_020
title: "rAthena Instance System Deep-Dive"
category: System Mechanics
keywords: [instance, memorial_dungeon, instance_create, instance_destroy, instance_enter, instance_warpall, instance_announce, OnInstanceInit, OnInstanceDestroy, party_instance, guild_instance, getinstancevar, setinstancevar]
related_files: [
  "db/re/instance_db.yml",
  "db/pre-re/instance_db.yml",
  "doc/script_commands.txt",
  "npc/instances/EndlessTower.txt",
  "npc/instances/NydhoggsNest.txt"
]
difficulty: advanced
use_case: "Creating memorial dungeons, party instances, guild raids, solo challenges, dynamic dungeon systems, and event instances"
version: rAthena 2024
last_updated: 2024-01-15
---

# rAthena Instance System Deep-Dive

## Table of Contents
1. [System Overview](#system-overview)
2. [Database Structure](#database-structure)
3. [Instance Modes](#instance-modes)
4. [Core Commands](#core-commands)
5. [Instance Variables](#instance-variables)
6. [Advanced Functions](#advanced-functions)
7. [Instance Events](#instance-events)
8. [Complete Examples](#complete-examples)
9. [Advanced Patterns](#advanced-patterns)
10. [Best Practices](#best-practices)

---

## System Overview

The **Instance System** (Memorial Dungeons) creates isolated, temporary copies of maps for individual players, parties, guilds, or clans. Each instance is completely independent with its own:
- **Maps** - Duplicated from source maps
- **NPCs** - Copied with independent states
- **Monsters** - Separate spawn pools
- **Variables** - Instance-scoped storage (`'var`)
- **Timers** - Independent countdown systems

### Use Cases
- **Memorial Dungeons** - Endless Tower, Nidhoggr's Nest
- **Party Challenges** - Raid bosses, timed dungeons
- **Guild Sieges** - Guild-exclusive battlegrounds
- **Solo Trials** - Character-specific challenges
- **Event Systems** - Tournament brackets, PvP arenas
- **Quest Instances** - Story dungeons, instanced quests

### Key Benefits
1. **Isolation** - Players don't interfere with each other
2. **Scalability** - Multiple groups can run the same content simultaneously
3. **State Management** - Each instance has independent progression
4. **Time Control** - Configurable lifetimes and idle timeouts
5. **Flexibility** - Supports solo, party, guild, and clan modes

---

## Database Structure

### Database Files
```yaml
# Renewal Mode
db/re/instance_db.yml

# Pre-Renewal Mode
db/pre-re/instance_db.yml

# Import Override
db/import/instance_db.yml
```

### YAML Format

```yaml
Header:
  Type: INSTANCE_DB
  Version: 2

Body:
  - Id: 1                      # Unique numeric ID
    Name: Endless Tower        # Instance name (used in commands)
    TimeLimit: 14400           # Total lifetime (seconds, 0=infinite)
    IdleTimeOut: 300           # Idle timeout (seconds, 0=infinite)
    NoNpc: false               # Skip copying NPCs from source map
    NoMapFlag: false           # Skip copying mapflags from source map
    Destroyable: true          # Allow manual destruction via UI button
    Enter:                     # Entry point configuration
      Map: 1@tower             # Starting map name
      X: 50                    # X coordinate
      Y: 355                   # Y coordinate
    AdditionalMaps:            # Other maps in this instance (optional)
      2@tower: true
      3@tower: true
      4@tower: true
      5@tower: true
      6@tower: true
```

### Field Reference

| Field | Type | Description | Default |
|-------|------|-------------|---------|
| **Id** | int | Unique instance ID | Required |
| **Name** | string | Instance name (for commands) | Required |
| **TimeLimit** | int | Total lifetime in seconds (0=infinite) | 3600 |
| **IdleTimeOut** | int | Idle timeout in seconds (0=infinite) | 300 |
| **NoNpc** | bool | Don't copy NPCs from source map | false |
| **NoMapFlag** | bool | Don't copy mapflags from source map | false |
| **Destroyable** | bool | Allow manual destruction | true |
| **Enter.Map** | string | Starting map name | Required |
| **Enter.X** | int | Starting X coordinate | Required |
| **Enter.Y** | int | Starting Y coordinate | Required |
| **AdditionalMaps** | list | Other instance maps | Optional |

### Example Definitions

```yaml
Body:
  # Simple single-map instance
  - Id: 100
    Name: Solo Trial
    TimeLimit: 3600      # 1 hour
    IdleTimeOut: 600     # 10 minutes
    Enter:
      Map: 1@trial
      X: 100
      Y: 100

  # Multi-map complex instance
  - Id: 101
    Name: Guild Raid
    TimeLimit: 7200      # 2 hours
    IdleTimeOut: 0       # No idle timeout
    Enter:
      Map: 1@graid
      X: 50
      Y: 50
    AdditionalMaps:
      2@graid: true
      3@graid: true
      4@graid: true

  # Infinite instance (event)
  - Id: 102
    Name: PvP Arena
    TimeLimit: 0         # Infinite
    IdleTimeOut: 0       # No idle timeout
    Destroyable: false   # Cannot be destroyed manually
    Enter:
      Map: 1@pvp
      X: 150
      Y: 150
```

---

## Instance Modes

Instances can be attached to different owner types.

### Mode Constants

| Constant | Value | Owner Type | Description |
|----------|-------|------------|-------------|
| `IM_NONE` | 0 | None | Not attached to any entity |
| `IM_CHAR` | 1 | Character | Character-exclusive instance |
| `IM_PARTY` | 2 | Party | Party-shared instance (default) |
| `IM_GUILD` | 3 | Guild | Guild-shared instance |
| `IM_CLAN` | 4 | Clan | Clan-shared instance |

### Mode Usage

```c
// Create party instance (default)
.@instance_id = instance_create("Endless Tower");
.@instance_id = instance_create("Endless Tower", IM_PARTY);

// Create character instance (solo)
.@instance_id = instance_create("Solo Trial", IM_CHAR, getcharid(0));

// Create guild instance
.@instance_id = instance_create("Guild Raid", IM_GUILD, getcharid(2));

// Create clan instance
.@instance_id = instance_create("Clan Challenge", IM_CLAN, getcharid(5));
```

### Mode Behavior

**IM_NONE**:
- Not attached to any specific entity
- Requires manual management
- Used for special event systems

**IM_CHAR**:
- One instance per character
- Only that character can enter
- Automatically destroyed when character logs out (optional)
- Perfect for solo challenges

**IM_PARTY** (Default):
- One instance per party
- All party members can enter
- Shared progression
- Most common for memorial dungeons

**IM_GUILD**:
- One instance per guild
- All guild members can enter
- Guild-wide challenges

**IM_CLAN**:
- One instance per clan
- All clan members can enter
- Clan competitions

---

## Core Commands

### 1. instance_create()

**Syntax**: `instance_create("<instance name>"{,<instance mode>{,<owner id>}})`

**Returns**:
- `>0`: Instance ID (success)
- `-1`: Invalid type
- `-2`: Character/Party/Guild/Clan not found
- `-3`: Instance already exists
- `-4`: No free instances (MAX_INSTANCE exceeded)

```c
// Basic party instance
.@instance_id = instance_create("Endless Tower");
if (.@instance_id < 0) {
	mes "Failed to create instance!";
	switch (.@instance_id) {
		case -1: mes "Invalid instance type."; break;
		case -2: mes "Party not found."; break;
		case -3: mes "Instance already exists!"; break;
		case -4: mes "Server is full of instances."; break;
	}
	close;
}
mes "Instance created! ID: " + .@instance_id;

// Character instance with specific owner
.@char_id = getcharid(0);
.@instance_id = instance_create("Solo Trial", IM_CHAR, .@char_id);

// Guild instance
.@guild_id = getcharid(2);
.@instance_id = instance_create("Guild Raid", IM_GUILD, .@guild_id);
```

**Behavior**:
1. Validates instance name exists in instance_db.yml
2. Checks if owner already has an instance of this type
3. Duplicates all maps listed in instance definition
4. Copies NPCs and mapflags (unless NoNpc/NoMapFlag)
5. Triggers `OnInstanceInit` label in all NPCs
6. Returns unique instance ID

---

### 2. instance_destroy()

**Syntax**: `instance_destroy({<instance id>})`

**Returns**: Nothing (halts on failure)

```c
// Destroy current instance (from within instance NPC)
instance_destroy();

// Destroy specific instance by ID
.@instance_id = instance_id(IM_PARTY);
instance_destroy(.@instance_id);

// Safe destruction with validation
if (.@instance_id > 0) {
	instance_destroy(.@instance_id);
	mes "Instance destroyed!";
}
```

**Behavior**:
1. Triggers `OnInstanceDestroy` label in all NPCs
2. Warps all players out of instance maps
3. Deletes all instance maps and NPCs
4. Frees instance ID for reuse

**Important**: `OnInstanceDestroy` runs BEFORE actual destruction, so NPCs and maps still exist during execution.

---

### 3. instance_enter()

**Syntax**: `instance_enter("<instance name>"{,<x>,<y>,<char_id>,<instance id>})`

**Returns**:
- `IE_OK` (0): Success
- `IE_NOMEMBER` (1): Party/Guild/Clan not found
- `IE_NOINSTANCE` (2): No instance exists
- `IE_OTHER` (3): Other errors

```c
// Basic entrance (uses coordinates from instance_db)
.@result = instance_enter("Endless Tower");
if (.@result != IE_OK) {
	mes "Cannot enter instance!";
	switch (.@result) {
		case IE_NOMEMBER: mes "Party not found."; break;
		case IE_NOINSTANCE: mes "Instance doesn't exist."; break;
		case IE_OTHER: mes "Unknown error."; break;
	}
	close;
}

// Enter with custom coordinates
instance_enter("Endless Tower", 100, 200);

// Enter specific character into specific instance
.@instance_id = instance_id(IM_PARTY);
instance_enter("Endless Tower", -1, -1, getcharid(0), .@instance_id);

// Use -1 for default coordinates from database
instance_enter("Endless Tower", -1, -1);
```

---

### 4. instance_npcname()

**Syntax**: `instance_npcname("<npc name>"{,<instance id>})`

**Returns**: Unique instance NPC name (string)

```c
// Get instance NPC name from current instance
.@npc_name$ = instance_npcname("Boss Controller");
donpcevent .@npc_name$ + "::OnKill";

// Get from specific instance
.@instance_id = instance_id(IM_PARTY);
.@npc_name$ = instance_npcname("Reward NPC", .@instance_id);
enablenpc .@npc_name$;

// Practical example: Enable NPC in instance
.@npc$ = instance_npcname("#FloorWarp");
enablenpc .@npc$;
```

**Why Needed**: Each instance has unique NPC names (e.g., `"Boss#101"` instead of `"Boss"`). This command gets the correct instance-specific name.

---

### 5. instance_mapname()

**Syntax**: `instance_mapname("<map name>"{,<instance id>})`

**Returns**: Unique instance map name (string), or `""` on failure

```c
// Get instance map name
.@map$ = instance_mapname("1@tower");
mes "Instance map: " + .@map$;  // e.g., "1@tower#101"

// Warp to instance map
.@map$ = instance_mapname("2@tower");
warp .@map$, 100, 100;

// Check if player is in instance
if (strcharinfo(3) == instance_mapname("1@tower")) {
	mes "You're in the instance!";
}

// Spawn monsters in instance map
.@map$ = instance_mapname("1@boss");
monster .@map$, 0, 0, "Boss Monster", 1039, 1, instance_npcname("BossCtrl") + "::OnBossDead";
```

---

### 6. instance_id()

**Syntax**: `instance_id({<instance mode>})`

**Returns**: Instance ID, or `-1` if not found

```c
// Get instance ID from attached NPC (default)
.@instance_id = instance_id();

// Get party instance ID
.@instance_id = instance_id(IM_PARTY);

// Get character instance ID
.@instance_id = instance_id(IM_CHAR);

// Get guild instance ID
.@instance_id = instance_id(IM_GUILD);

// Practical check
.@instance_id = instance_id(IM_PARTY);
if (.@instance_id < 0) {
	mes "You don't have an active instance!";
	close;
}
```

---

## Instance Variables

Instance variables use the `'` prefix and are unique per instance.

### Syntax

```c
// Set instance variable
'progress = 5;
'boss_killed = 1;
'floor_number = 25;

// Read instance variable
if ('progress >= 10) {
	mes "You've made good progress!";
}

// String variables
'current_stage$ = "Boss Fight";
mes "Current stage: " + 'current_stage$;
```

### getinstancevar() / setinstancevar()

Access instance variables from outside the instance:

```c
// Get instance variable from specific instance
.@instance_id = instance_id(IM_PARTY);
.@progress = getinstancevar('progress, .@instance_id);
mes "Your party's progress: " + .@progress;

// Set instance variable from outside
setinstancevar('boss_killed, 1, .@instance_id);

// Practical example: Check progress from NPC outside instance
prontera,150,150,4	script	Instance Info	123,{
	.@instance_id = instance_id(IM_PARTY);
	if (.@instance_id < 0) {
		mes "You don't have an active instance.";
		close;
	}

	.@floor = getinstancevar('current_floor, .@instance_id);
	.@time = getinstancevar('start_time, .@instance_id);
	.@elapsed = gettimetick(2) - .@time;

	mes "Current Floor: " + .@floor;
	mes "Time Elapsed: " + .@elapsed + " seconds";
	close;
}
```

### Variable Scope Summary

```c
// Instance variables (unique per instance)
'var = 1;           // Accessible within instance or via getinstancevar

// NPC variables (shared across all instances of this NPC)
.var = 1;           // Permanent NPC variable
.@var = 1;          // Temporary NPC variable

// Player variables (attached player)
@var = 1;           // Temporary player variable
#var = 1;           // Permanent account variable
var = 1;            // Permanent character variable
```

---

## Advanced Functions

### instance_warpall()

Warps all players in an instance to a specific location.

**Syntax**: `instance_warpall("<map name>",<x>,<y>{,<instance id>{,<flag>}})`

```c
// Warp all to specific map/coords
instance_warpall("prontera", 150, 150);

// Warp within instance
.@map$ = instance_mapname("2@tower");
instance_warpall(.@map$, 100, 100);

// With flag: exclude dead players
instance_warpall("prontera", 150, 150, instance_id(), IWA_NOTDEAD);

// Practical: Warp all on boss death
OnBossDead:
	instance_announce(0, "Congratulations! Warping in 5 seconds...", bc_map, 0x00FF00);
	sleep 5000;
	instance_warpall("prontera", 156, 191);
	end;
```

**Flags**:
- `IWA_NONE` (0) - No restriction (default)
- `IWA_NOTDEAD` (1) - Don't warp dead players

---

### instance_announce()

Broadcasts a message to all players in an instance.

**Syntax**: `instance_announce(<instance id>,"<text>",<flag>{,<fontColor>{,<fontType>{,<fontSize>{,<fontAlign>{,<fontY>}}}}})`

```c
// Basic announcement (current instance)
instance_announce(0, "The boss has appeared!", bc_map);

// With color
instance_announce(0, "Warning: 5 minutes remaining!", bc_map, 0xFF0000);

// Specific instance
.@instance_id = instance_id(IM_PARTY);
instance_announce(.@instance_id, "Floor cleared!", bc_map, 0x00FF00);

// Advanced formatting
instance_announce(0, "BOSS BATTLE!", bc_map | bc_blue, 0x0000FF, FW_NORMAL, 20);
```

**Common Flags**:
- `bc_map` - All players on instance maps
- `bc_blue` - Blue chat color
- `bc_woe` - WoE font style

---

### instance_check_party()

Validates party requirements before allowing entry.

**Syntax**: `instance_check_party(<party id>{,<amount>{,<min>{,<max>}}})`

**Returns**: `1` if requirements met, `0` otherwise

```c
// Basic check: party exists and has 1+ online member
if (!instance_check_party(getcharid(1))) {
	mes "You need to be in a party!";
	close;
}

// At least 2 online members
if (!instance_check_party(getcharid(1), 2)) {
	mes "You need at least 2 online party members!";
	close;
}

// 2+ members, levels 100-150
if (!instance_check_party(getcharid(1), 2, 100, 150)) {
	mes "Requirements:";
	mes "- At least 2 online members";
	mes "- All members level 100-150";
	close;
}

// Complete entrance NPC
prontera,150,150,4	script	Instance Entrance	123,{
	.@party_id = getcharid(1);

	// Validate party requirements
	if (!instance_check_party(.@party_id, 2, 50, 150)) {
		mes "[Entrance Guardian]";
		mes "Your party doesn't meet requirements:";
		mes "- At least 2 online members";
		mes "- All members level 50-150";
		close;
	}

	// Check if party leader
	if (!is_party_leader()) {
		mes "Only the party leader can create an instance.";
		close;
	}

	// Create instance
	.@instance_id = instance_create("My Dungeon", IM_PARTY, .@party_id);
	if (.@instance_id < 0) {
		mes "Failed to create instance!";
		close;
	}

	mes "Instance created! Entering...";
	close2;
	instance_enter("My Dungeon");
	end;
}
```

---

### instance_check_guild() / instance_check_clan()

Same as `instance_check_party()` but for guilds/clans.

```c
// Guild check
if (!instance_check_guild(getcharid(2), 5, 100, 150)) {
	mes "Need 5+ online guild members, levels 100-150!";
	close;
}

// Clan check
if (!instance_check_clan(getcharid(5), 3, 80, 120)) {
	mes "Need 3+ online clan members, levels 80-120!";
	close;
}
```

---

### instance_info()

Get static information about an instance definition from the database.

**Syntax**: `instance_info("<instance name>",<info type>{,<instance_db map index>})`

**Info Types**:
- `IIT_ID` - Instance ID from database
- `IIT_TIME_LIMIT` - TimeLimit value (seconds)
- `IIT_IDLE_TIMEOUT` - IdleTimeOut value (seconds)
- `IIT_ENTER_MAP` - Enter map name
- `IIT_ENTER_X` - Enter X coordinate
- `IIT_ENTER_Y` - Enter Y coordinate
- `IIT_MAP` - Map name by index (requires map index parameter)

```c
// Get instance info
.@time_limit = instance_info("Endless Tower", IIT_TIME_LIMIT);
.@idle_timeout = instance_info("Endless Tower", IIT_IDLE_TIMEOUT);
.@enter_map$ = instance_info("Endless Tower", IIT_ENTER_MAP);

mes "Endless Tower Info:";
mes "Time Limit: " + .@time_limit + " seconds";
mes "Idle Timeout: " + .@idle_timeout + " seconds";
mes "Enter Map: " + .@enter_map$;

// Get additional map by index
.@map$ = instance_info("Endless Tower", IIT_MAP, 1);  // Get 2nd map (index 1)
```

---

### instance_live_info()

Get runtime information about a currently running instance.

**Syntax**: `instance_live_info(<info type>{,<instance id>})`

**Info Types**:
- `ILI_NAME` - Instance name
- `ILI_MODE` - Instance mode (IM_PARTY, etc.)
- `ILI_OWNER` - Owner ID
- `ILI_MAP` - Number of maps in instance
- `ILI_START_TIME` - Instance creation time (timestamp)
- `ILI_ALIVE_TIME` - Remaining time before destruction (seconds)
- `ILI_IDLE_TIMER` - Remaining idle time (seconds)

```c
// From within instance
.@name$ = instance_live_info(ILI_NAME);
.@mode = instance_live_info(ILI_MODE);
.@alive_time = instance_live_info(ILI_ALIVE_TIME);

mes "Instance: " + .@name$;
mes "Time Remaining: " + .@alive_time + " seconds";

// From outside instance
.@instance_id = instance_id(IM_PARTY);
.@start_time = instance_live_info(ILI_START_TIME, .@instance_id);
.@elapsed = gettimetick(2) - .@start_time;
mes "Elapsed time: " + .@elapsed + " seconds";

// Complete info display
prontera,155,155,4	script	Instance Status	123,{
	.@instance_id = instance_id(IM_PARTY);
	if (.@instance_id < 0) {
		mes "No active instance.";
		close;
	}

	.@name$ = instance_live_info(ILI_NAME, .@instance_id);
	.@alive = instance_live_info(ILI_ALIVE_TIME, .@instance_id);
	.@idle = instance_live_info(ILI_IDLE_TIMER, .@instance_id);

	mes "[Instance Status]";
	mes "Name: " + .@name$;
	mes "Time Remaining: " + (.@alive / 60) + " minutes";
	mes "Idle Timeout: " + (.@idle / 60) + " minutes";
	close;
}
```

---

### instance_list()

Lists all instance IDs for a specific map and mode.

**Syntax**: `instance_list("<map name>"{,<instance mode>})`

**Returns**: Array size of `.@instance_list[]`

```c
// List all instances on a map
.@count = instance_list("1@tower");
mes "Found " + .@count + " instances of Endless Tower";
for (.@i = 0; .@i < .@count; .@i++) {
	mes "Instance #" + .@instance_list[.@i];
}

// List party instances only
.@count = instance_list("1@tower", IM_PARTY);

// Admin tool: List and destroy all instances
-	script	AdminInstanceManager	-1,{
OnCommand:
	.@count = instance_list("1@tower");
	mes "Found " + .@count + " instances.";
	mes "Destroy all?";
	next;
	if (select("Yes:No") == 1) {
		for (.@i = 0; .@i < .@count; .@i++) {
			instance_destroy(.@instance_list[.@i]);
		}
		mes "All instances destroyed.";
	}
	close;
}
```

---

## Instance Events

### OnInstanceInit

Triggered when an instance is created or `@reloadscript` is used.

```c
// Inside instance NPC
1@tower,50,50,4	script	Instance Controller	111,{
	end;

OnInstanceInit:
	// Initialize instance state
	'current_floor = 1;
	'start_time = gettimetick(2);
	'boss_killed = 0;

	// Announce
	instance_announce(0, "Welcome to Endless Tower!", bc_map);

	// Spawn initial monsters
	.@map$ = instance_mapname("1@tower");
	monster .@map$, 0, 0, "Poring", 1002, 50;

	// Start timer
	initnpctimer;
	end;

OnTimer60000:  // Every 60 seconds
	.@floor = 'current_floor;
	instance_announce(0, "Current Floor: " + .@floor, bc_map);
	initnpctimer;
	end;
}
```

---

### OnInstanceDestroy

Triggered just before instance destruction.

```c
OnInstanceDestroy:
	// Save final data
	.@instance_id = instance_id();
	.@floor = 'current_floor;
	.@time = gettimetick(2) - 'start_time;

	// Log to database (if needed)
	query_sql("INSERT INTO instance_log VALUES ('" + getcharid(0) + "', " + .@floor + ", " + .@time + ")");

	// Final announcement
	instance_announce(0, "Instance will be destroyed in 10 seconds!", bc_map, 0xFF0000);
	sleep 10000;

	// Warp everyone out
	instance_warpall("prontera", 150, 150);

	// Cleanup
	stopnpctimer;
	end;
```

---

## Complete Examples

### Example 1: Simple Solo Instance

```yaml
# db/import/instance_db.yml
Body:
  - Id: 100
    Name: Training Ground
    TimeLimit: 1800      # 30 minutes
    IdleTimeOut: 300     # 5 minutes
    Enter:
      Map: 1@training
      X: 100
      Y: 100
```

```c
// Entrance NPC
prontera,150,150,4	script	Training Entrance	123,{
	mes "[Trainer]";
	mes "Welcome to the Training Ground!";
	mes "This is a solo challenge.";
	next;

	// Check if already has instance
	.@instance_id = instance_id(IM_CHAR);
	if (.@instance_id >= 0) {
		mes "You already have an active instance!";
		mes "Re-enter?";
		next;
		if (select("Yes:No") == 1) {
			instance_enter("Training Ground");
		}
		close;
	}

	// Create character instance
	.@char_id = getcharid(0);
	.@instance_id = instance_create("Training Ground", IM_CHAR, .@char_id);

	if (.@instance_id < 0) {
		mes "Failed to create instance!";
		close;
	}

	mes "Instance created! Good luck!";
	close2;
	instance_enter("Training Ground");
	end;
}

// Instance Controller
1@training,100,100,0	script	Training Controller	-1,{
OnInstanceInit:
	// Initialize
	'wave = 1;
	'monsters_killed = 0;
	instance_announce(0, "Training started! Defeat 3 waves!", bc_map);

	// Spawn wave 1
	donpcevent instance_npcname("Training Controller") + "::OnWave1";
	end;

OnWave1:
	.@map$ = instance_mapname("1@training");
	instance_announce(0, "Wave 1: Porings!", bc_map);
	monster .@map$, 0, 0, "Poring", 1002, 10, instance_npcname("Training Controller") + "::OnMonsterKilled";
	end;

OnMonsterKilled:
	'monsters_killed++;
	if ('monsters_killed >= 10 && 'wave == 1) {
		'wave = 2;
		'monsters_killed = 0;
		sleep 3000;
		donpcevent instance_npcname("Training Controller") + "::OnWave2";
	} else if ('monsters_killed >= 15 && 'wave == 2) {
		'wave = 3;
		'monsters_killed = 0;
		sleep 3000;
		donpcevent instance_npcname("Training Controller") + "::OnWave3";
	} else if ('monsters_killed >= 1 && 'wave == 3) {
		donpcevent instance_npcname("Training Controller") + "::OnComplete";
	}
	end;

OnWave2:
	.@map$ = instance_mapname("1@training");
	instance_announce(0, "Wave 2: Drops!", bc_map);
	monster .@map$, 0, 0, "Drops", 1113, 15, instance_npcname("Training Controller") + "::OnMonsterKilled";
	end;

OnWave3:
	.@map$ = instance_mapname("1@training");
	instance_announce(0, "Wave 3: BOSS!", bc_map);
	monster .@map$, 100, 100, "Training Boss", 1039, 1, instance_npcname("Training Controller") + "::OnMonsterKilled";
	end;

OnComplete:
	instance_announce(0, "Training complete! Congratulations!", bc_map, 0x00FF00);
	sleep 5000;
	instance_warpall("prontera", 150, 150);
	instance_destroy();
	end;
}
```

---

### Example 2: Party Memorial Dungeon

```yaml
# db/import/instance_db.yml
Body:
  - Id: 101
    Name: Ancient Ruins
    TimeLimit: 7200      # 2 hours
    IdleTimeOut: 600     # 10 minutes
    Enter:
      Map: 1@ruins
      X: 50
      Y: 50
    AdditionalMaps:
      2@ruins: true
      3@ruins: true
```

```c
// Entrance NPC
geffen,120,100,4	script	Ruins Entrance	123,{
	.@party_id = getcharid(1);

	// Validate party
	if (!instance_check_party(.@party_id, 2, 75)) {
		mes "[Guardian]";
		mes "Requirements:";
		mes "- At least 2 online party members";
		mes "- All members level 75+";
		close;
	}

	mes "[Guardian]";
	mes "Your party meets the requirements!";
	next;

	// Check for existing instance
	.@instance_id = instance_id(IM_PARTY);
	if (.@instance_id >= 0) {
		mes "Your party already has an instance.";
		if (select("Enter:Cancel") == 1) {
			instance_enter("Ancient Ruins");
		}
		close;
	}

	// Only leader can create
	if (!is_party_leader()) {
		mes "Only the party leader can create an instance.";
		close;
	}

	mes "Create instance?";
	next;
	if (select("Yes:No") == 2) close;

	// Create instance
	.@instance_id = instance_create("Ancient Ruins", IM_PARTY, .@party_id);
	if (.@instance_id < 0) {
		mes "Failed to create instance!";
		close;
	}

	mes "Instance created!";
	close2;
	instance_enter("Ancient Ruins");
	end;
}

// Floor 1 Controller
1@ruins,50,50,0	script	Floor1_Controller	-1,{
OnInstanceInit:
	// Initialize progress
	'floor = 1;
	'start_time = gettimetick(2);
	'boss1_dead = 0;

	instance_announce(0, "Ancient Ruins - Floor 1", bc_map);
	instance_announce(0, "Defeat the guardian to proceed!", bc_map);

	// Spawn boss
	.@map$ = instance_mapname("1@ruins");
	monster .@map$, 100, 100, "Floor Guardian", 1046, 1, instance_npcname("Floor1_Controller") + "::OnBossDead";

	// Lock exit warp
	disablenpc instance_npcname("Floor1Exit");
	end;

OnBossDead:
	'boss1_dead = 1;
	instance_announce(0, "Floor 1 cleared! Exit unlocked!", bc_map, 0x00FF00);

	// Unlock exit
	enablenpc instance_npcname("Floor1Exit");

	// Give rewards
	getitem 607, 5;  // Yggdrasil Berry
	end;
}

// Floor 1 Exit Warp
1@ruins,150,150,0	script	Floor1Exit	45,2,2,{
OnTouch:
	.@map$ = instance_mapname("2@ruins");
	warp .@map$, 50, 50;
	end;

OnInstanceInit:
	disablenpc instance_npcname("Floor1Exit");
	end;
}

// Floor 2 Controller
2@ruins,50,50,0	script	Floor2_Controller	-1,{
OnInstanceInit:
	'floor = 2;
	instance_announce(0, "Ancient Ruins - Floor 2", bc_map);
	instance_announce(0, "Final boss ahead!", bc_map);

	// Spawn final boss
	.@map$ = instance_mapname("2@ruins");
	monster .@map$, 100, 100, "Ancient King", 1039, 1, instance_npcname("Floor2_Controller") + "::OnFinalBossDead";

	disablenpc instance_npcname("ExitPortal");
	end;

OnFinalBossDead:
	'boss2_dead = 1;
	.@time_taken = gettimetick(2) - 'start_time;
	.@minutes = .@time_taken / 60;

	instance_announce(0, "CONGRATULATIONS!", bc_map, 0xFFFF00);
	instance_announce(0, "Time: " + .@minutes + " minutes", bc_map);

	// Give MVP rewards
	getitem 607, 10;  // Yggdrasil Berry
	getitem 617, 5;   // Old Purple Box

	enablenpc instance_npcname("ExitPortal");
	end;
}

// Exit Portal
2@ruins,100,120,0	script	ExitPortal	45,2,2,{
OnTouch:
	mes "Leave instance?";
	next;
	if (select("Yes:No") == 1) {
		warp "geffen", 120, 100;
	}
	close;

OnInstanceInit:
	disablenpc instance_npcname("ExitPortal");
	end;
}
```

---

## Advanced Patterns

### Pattern 1: Cooldown System

```c
prontera,150,150,4	script	CD Instance Entry	123,{
	.@party_id = getcharid(1);

	// Check cooldown (1 week)
	.@cooldown = checkquest(60200, PLAYTIME);
	if (.@cooldown == 0 || .@cooldown == 1) {
		mes "Your party is on cooldown!";
		mes "Time remaining: ";
		// Calculate remaining time
		close;
	} else if (.@cooldown == 2) {
		erasequest 60200;
	}

	// Create instance
	.@instance_id = instance_create("My Instance", IM_PARTY, .@party_id);
	if (.@instance_id >= 0) {
		// Set cooldown
		setquest 60200;
		instance_enter("My Instance");
	}
	end;
}
```

---

### Pattern 2: Progress Saving

```c
// Save progress when player leaves
1@tower,0,0,0	script	Progress Saver	-1,{
OnPCLogoutEvent:
	if (strcharinfo(3) == instance_mapname("1@tower")) {
		// Save current floor
		.@floor = 'current_floor;
		#tower_progress = .@floor;
	}
	end;
}

// Restore progress on re-entry
OnInstanceInit:
	if (#tower_progress > 0) {
		'current_floor = #tower_progress;
		instance_announce(0, "Restored to floor " + #tower_progress, bc_map);
	}
	end;
```

---

### Pattern 3: Time Trial Rankings

```c
OnFinalBossDead:
	.@time = gettimetick(2) - 'start_time;
	.@party_name$ = getpartyname(getcharid(1));

	// Save to database
	query_sql("INSERT INTO instance_rankings (party_name, clear_time) VALUES ('" + escape_sql(.@party_name$) + "', " + .@time + ")");

	// Get ranking
	query_sql("SELECT COUNT(*) FROM instance_rankings WHERE clear_time < " + .@time, .@rank);

	instance_announce(0, "Clear time: " + (.@time / 60) + " minutes", bc_map);
	instance_announce(0, "Rank: #" + (.@rank + 1), bc_map);
	end;
```

---

### Pattern 4: Buff Removal on Entry

```c
OnInstanceInit:
	// Remove all buffs from party members
	.@party_id = getcharid(1);
	getpartymember .@party_id;
	for (.@i = 0; .@i < $@partymembercount; .@i++) {
		if (isloggedin($@partymemberaid[.@i], $@partymembercid[.@i])) {
			atcommand "@recallparty " + getpartyname(.@party_id);
			sc_end SC_ALL;  // Remove all status effects
		}
	}
	end;
```

---

## Best Practices

### 1. Always Validate Instance Creation

```c
.@instance_id = instance_create("My Instance");
if (.@instance_id < 0) {
	switch (.@instance_id) {
		case -1: mes "Invalid type!"; break;
		case -2: mes "Party not found!"; break;
		case -3: mes "Instance already exists!"; break;
		case -4: mes "Server full!"; break;
	}
	close;
}
```

### 2. Use instance_npcname() for All NPC References

```c
// WRONG
enablenpc "BossWarp";
donpcevent "Controller::OnStart";

// CORRECT
enablenpc instance_npcname("BossWarp");
donpcevent instance_npcname("Controller") + "::OnStart";
```

### 3. Use instance_mapname() for All Map References

```c
// WRONG
warp "1@tower", 100, 100;
monster "1@tower", 0, 0, "Mob", 1002, 10;

// CORRECT
.@map$ = instance_mapname("1@tower");
warp .@map$, 100, 100;
monster .@map$, 0, 0, "Mob", 1002, 10;
```

### 4. Clean Up on Destruction

```c
OnInstanceDestroy:
	// Stop timers
	stopnpctimer;

	// Warp players out
	instance_warpall("prontera", 150, 150);

	// Clear variables
	'progress = 0;
	'boss_killed = 0;
	end;
```

### 5. Set Appropriate Timeouts

```yaml
# Short instance (quick run)
TimeLimit: 1800       # 30 minutes
IdleTimeOut: 300      # 5 minutes

# Long instance (raid)
TimeLimit: 10800      # 3 hours
IdleTimeOut: 900      # 15 minutes

# Event instance (no limit)
TimeLimit: 0          # Infinite
IdleTimeOut: 0        # No timeout
```

### 6. Use OnInstanceInit for Setup

```c
OnInstanceInit:
	// Initialize variables
	'floor = 1;
	'start_time = gettimetick(2);

	// Initial announcements
	instance_announce(0, "Instance created!", bc_map);

	// Spawn initial content
	.@map$ = instance_mapname("1@map");
	monster .@map$, 0, 0, "Mob", 1002, 50;

	// Disable locked areas
	disablenpc instance_npcname("LockedDoor");

	// Start timers
	initnpctimer;
	end;
```

### 7. Prevent Resource Leaks

```c
// Always clean up monsters on instance destroy
OnInstanceDestroy:
	.@map$ = instance_mapname("1@map");
	killmonsterall .@map$;
	stopnpctimer;
	end;
```

---

## Troubleshooting

### Issue: "Instance already exists"

**Cause**: Party/character already has an active instance.

**Solution**:
```c
.@instance_id = instance_id(IM_PARTY);
if (.@instance_id >= 0) {
	mes "Instance already exists! Enter?";
	if (select("Yes:No") == 1) {
		instance_enter("My Instance");
	}
	close;
}
```

---

### Issue: NPCs not responding in instance

**Cause**: Using NPC name instead of instance_npcname().

**Fix**:
```c
// WRONG
enablenpc "MyNPC";

// CORRECT
enablenpc instance_npcname("MyNPC");
```

---

### Issue: Variables not persisting

**Cause**: Using temporary variables instead of instance variables.

**Fix**:
```c
// WRONG (temporary NPC variable)
.@progress = 5;

// CORRECT (instance variable)
'progress = 5;
```

---

## Related References

- **Script Commands**: [KB_REF_ScriptCommandsCore.md], [KB_REF_ScriptCommandsExpanded.md]
- **Database Structure**: [KB_REF_DatabaseStructure.md]
- **NPC Scripting**: [KB_REF_NPCScripting.md]
- **Mob System**: [KB_REF_MobModesAI.md]
- **Documentation**: `doc/script_commands.txt`
- **Examples**: `npc/instances/EndlessTower.txt`, `npc/instances/NydhoggsNest.txt`

---

**End of KB_REF_020 - Instance System Deep-Dive**
