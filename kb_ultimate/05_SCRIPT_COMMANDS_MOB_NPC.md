# rAthena Script Commands - Monster & NPC Reference
## Complete Monster and NPC Management Commands

---

<!-- RAG_CHUNK: monster_spawn_001 -->
## Monster Spawning

### monster
**Syntax:** `monster "<map>",<x>,<y>,"<name>",<mob id>,<amount>{,"<event>"{,<size>,<ai>}};`

Spawn monsters on map.

**Parameters:**
- `x,y` = 0,0 for random location
- `name` = "--en--" or "--ja--" for database names
- `event` = "NPCName::OnLabel" for kill event

**Size Constants:**
- `Size_Small` (0)
- `Size_Medium` (1)
- `Size_Large` (2)

**AI Constants:**
- `AI_NONE` (0) - Default
- `AI_ATTACK` (1) - Attack/friendly
- `AI_SPHERE` (2) - Marine Sphere
- `AI_FLORA` (3) - Flora
- `AI_ZANZOU` (4) - Kagerou/Oboro
- `AI_LEGION` (5) - Sera skill
- `AI_FAW` (6) - Mechanic skill
- `AI_WAVEMODE` (7) - Wave mode

**Examples:**
```c
// Spawn 10 Porings randomly
monster "prt_fild08",0,0,"Poring",1002,10;

// Spawn with kill event
monster "prontera",150,150,"Event Poring",1002,1,"MyNPC::OnPoringKilled";

// Spawn big Poring
monster "prontera",150,150,"Giant Poring",1002,1,"",Size_Large;
```

**After Spawning:**
```c
$@mobid[0]  // First spawned mob's GID
$@mobid[n]  // All spawned mob GIDs
```

---

### areamonster
**Syntax:** `areamonster "<map>",<x1>,<y1>,<x2>,<y2>,"<name>",<mob id>,<amount>{,"<event>"{,<size>,<ai>}};`

Spawn monsters in rectangular area.

**Example:**
```c
areamonster "prt_fild08",100,100,200,200,"Poring",1002,50;
```

---

### boss_monster
**Syntax:** Same as monster.

Spawns boss (detectable by Convex Mirror). Uses fixed spawn position.

---

### clone
**Syntax:** `clone "<map>",<x>,<y>,"<event>",<char id>{,<master id>{,<mode>{,<flag>{,<duration>}}}};`

Create clone of player.

**Flags:**
- 1 = Clone master's equipment
- 2 = Clone as enemy
- 4 = Clone with transformed look

**Example:**
```c
.@gid = clone("prontera",155,180,"",getcharid(0));
```

---

### summon
**Syntax:** `summon "<name>",<mob id>{,<timeout>{,"<event>"}};`

Summon monster that follows player.

**Example:**
```c
summon "My Pet",1002,300000;  // 5 minute duration
```

---

<!-- RAG_CHUNK: monster_control_001 -->
## Monster Control

### killmonster
**Syntax:** `killmonster "<map>","<event>"{,<type>};`

Kill monsters spawned with specific event.

**Types:**
- 0 = Kill and trigger death events (default)
- 1 = Kill silently (no drops/exp)

**Example:**
```c
// Kill monsters with our event label
killmonster "prt_fild08","MyNPC::OnPoringKilled";

// Kill all monsters on map
killmonster "prt_fild08","All";
```

---

### killmonsterall
**Syntax:** `killmonsterall "<map>"{,<type>};`

Kill all monsters on map.

---

### mobcount
**Syntax:** `mobcount("<map>","<event>")`

Count monsters with specific event.

**Example:**
```c
if (mobcount("prt_fild08","MyNPC::OnMobDead") == 0) {
    mes "All monsters cleared!";
}
```

---

### getmobdrops
**Syntax:** `getmobdrops(<mob id>)`

Get monster drop list. Returns count.

**Arrays Set:**
```c
$@MobDrop_item[]    - Item IDs
$@MobDrop_rate[]    - Drop rates
$@MobDrop_count     - Total drops
```

**Example:**
```c
.@count = getmobdrops(1002);
for (.@i = 0; .@i < .@count; .@i++) {
    mes getitemname($@MobDrop_item[.@i]) + ": " + ($@MobDrop_rate[.@i]/100) + "%";
}
```

---

### strmobinfo
**Syntax:** `strmobinfo(<type>,<mob id>)`

Get monster information.

| Type | Returns |
|------|---------|
| 0 | Name (aegis) |
| 1 | Name (japanese) |
| 2 | Level |
| 3 | HP |
| 4 | SP |
| 5 | Base EXP |
| 6 | Job EXP |

---

### getmonsterinfo
**Syntax:** `getmonsterinfo(<mob id>,<type>)`

Get detailed monster info.

**Types:**
```c
MOB_ID, MOB_AEGISNAME, MOB_NAME, MOB_LV, MOB_MAXHP, MOB_MAXSP,
MOB_BASEEXP, MOB_JOBEXP, MOB_ATK1, MOB_ATK2, MOB_DEF, MOB_MDEF,
MOB_STR, MOB_AGI, MOB_VIT, MOB_INT, MOB_DEX, MOB_LUK,
MOB_RANGE, MOB_RANGE2, MOB_RANGE3, MOB_SIZE, MOB_RACE, MOB_ELEMENT,
MOB_MODE, MOB_MVPEXP, MOB_ADELAY, MOB_AMOTION, MOB_DMOTION
```

---

### addmonsterdrop / delmonsterdrop
**Syntax:** `addmonsterdrop(<mob id>,<item id>,<rate>);`
**Syntax:** `delmonsterdrop(<mob id>,<item id>);`

Modify monster drops (temporary).

**Example:**
```c
// Add 50% drop of Apple to Poring
addmonsterdrop 1002, 512, 5000;
```

---

<!-- RAG_CHUNK: unit_control_001 -->
## Unit Control

### getunitdata
**Syntax:** `getunitdata(<gid>,<arrayname>)`

Get unit (mob/NPC/player) data into array.

**Mob Array Indexes (UMOB_*):**
```c
UMOB_SIZE, UMOB_LEVEL, UMOB_HP, UMOB_MAXHP, UMOB_MASTERAID,
UMOB_MAPID, UMOB_X, UMOB_Y, UMOB_SPEED, UMOB_MODE,
UMOB_AI, UMOB_SCOPTION, UMOB_SEX, UMOB_CLASS, UMOB_HAIRSTYLE,
UMOB_HAIRCOLOR, UMOB_HEADBOTTOM, UMOB_HEADMIDDLE, UMOB_HEADTOP,
UMOB_CLOTHCOLOR, UMOB_SHIELD, UMOB_WEAPON, UMOB_LOOKDIR,
UMOB_STR, UMOB_AGI, UMOB_VIT, UMOB_INT, UMOB_DEX, UMOB_LUK,
UMOB_SLAVECPYMSTRMD, UMOB_DMGIMMUNE, UMOB_ATKRANGE,
UMOB_ATKMIN, UMOB_ATKMAX, UMOB_MATKMIN, UMOB_MATKMAX,
UMOB_DEF, UMOB_MDEF, UMOB_HIT, UMOB_FLEE, UMOB_PDODGE,
UMOB_CRIT, UMOB_RACE, UMOB_ELETYPE, UMOB_ELELEVEL,
UMOB_AMOTION, UMOB_ADELAY, UMOB_DMOTION, UMOB_TARGETID
```

**Example:**
```c
monster "prontera",150,150,"Poring",1002,1;
.@gid = $@mobid[0];

getunitdata .@gid, .@data;
mes "HP: " + .@data[UMOB_HP] + "/" + .@data[UMOB_MAXHP];
```

---

### setunitdata
**Syntax:** `setunitdata <gid>,<type>,<value>;`

Set unit data.

**Example:**
```c
monster "prontera",150,150,"Super Poring",1002,1;
.@gid = $@mobid[0];

setunitdata .@gid, UMOB_MAXHP, 10000;
setunitdata .@gid, UMOB_HP, 10000;
setunitdata .@gid, UMOB_SIZE, Size_Large;
```

---

### unitwalk / unitwarp
**Syntax:** `unitwalk(<gid>,<x>,<y>{,"<event>"})`
**Syntax:** `unitwarp(<gid>,"<map>",<x>,<y>)`

Move unit.

---

### unitattack
**Syntax:** `unitattack(<gid>,<target id>{,<action>})`

Make unit attack target.

---

### unitkill
**Syntax:** `unitkill(<gid>)`

Kill unit instantly.

---

### unittalk
**Syntax:** `unittalk(<gid>,"<message>"{,<flag>})`

Make unit say message.

**Flags:**
- 1 = Message above unit
- 0 = Normal chat (default)

---

### unitexists
**Syntax:** `unitexists(<gid>)`

Check if unit exists. Returns 1 or 0.

---

### getunitname / setunitname
**Syntax:** `getunitname(<gid>)`
**Syntax:** `setunitname(<gid>,"<name>")`

Get/set unit name.

---

### getunittype
**Syntax:** `getunittype(<gid>)`

Get unit type.

**Types:**
```c
UNITTYPE_PC       = 0
UNITTYPE_NPC      = 1
UNITTYPE_PET      = 2
UNITTYPE_MOB      = 3
UNITTYPE_HOM      = 4
UNITTYPE_MER      = 5
UNITTYPE_ELEM     = 6
```

---

<!-- RAG_CHUNK: npc_control_001 -->
## NPC Control

### enablenpc / disablenpc
**Syntax:** `enablenpc "<npc name>";`
**Syntax:** `disablenpc "<npc name>";`

Enable/disable NPC (hides and makes unclickable).

**Example:**
```c
OnInit:
    disablenpc "EventNPC";
    end;

OnEnableEvent:
    enablenpc "EventNPC";
    end;
```

---

### hideonnpc / hideoffnpc
**Syntax:** `hideonnpc "<npc name>";`
**Syntax:** `hideoffnpc "<npc name>";`

Hide/show NPC sprite (still clickable).

---

### cloakonnpc / cloakoffnpc
**Syntax:** `cloakonnpc {<flag>,}"<npc name>";`
**Syntax:** `cloakoffnpc {<flag>,}"<npc name>";`

Cloak NPC (fade effect).

---

### setnpcdisplay
**Syntax:** `setnpcdisplay("<npc name>",<class id>{,<size>{,<color>}});`
**Syntax:** `setnpcdisplay("<npc name>","<display name>"{,<class id>{,<size>}});`

Change NPC appearance.

**Example:**
```c
setnpcdisplay "MyNPC", 1002;  // Change to Poring sprite
setnpcdisplay "MyNPC", "New Name", 4_F_KAFRA1;
```

---

### movenpc
**Syntax:** `movenpc "<npc name>",<x>,<y>{,<dir>};`

Relocate NPC.

---

### npctalk
**Syntax:** `npctalk "<message>"{,<flag>{,"<npc name>"}};`

Make NPC say message.

**Flags:**
- bc_area = Local message (default)
- bc_self = Only to attached player

---

### getnpcid
**Syntax:** `getnpcid(<type>{,"<npc name>"})`

Get NPC game ID.

**Types:**
- 0 = NPC itself or specified NPC

---

### strnpcinfo
**Syntax:** `strnpcinfo(<type>{,"<npc name>"})`

Get NPC information.

| Type | Returns |
|------|---------|
| 0 | Complete name (with #) |
| 1 | Visible name (before #) |
| 2 | Hidden part (after #) |
| 3 | Unique name (after ::) |
| 4 | Map name NPC is on |

---

### unloadnpc
**Syntax:** `unloadnpc "<npc name>";`

Completely remove NPC.

---

### duplicate
**Syntax:** `duplicate("<source npc>") <definition>;`

Create NPC duplicate dynamically.

---

### duplicate_dynamic
**Syntax:** `duplicate_dynamic("<source>",{"<new name>"},{<x>,<y>,<dir>})`

Dynamic duplicate creation.

---

### npcspeed / npcstop / npcwalkto
**Syntax:** `npcspeed(<speed>);`
**Syntax:** `npcstop;`
**Syntax:** `npcwalkto(<x>,<y>);`

Control NPC movement.

**Example:**
```c
OnTouch:
    npcspeed 150;
    npcwalkto 160, 180;
    end;
```

---

<!-- RAG_CHUNK: npc_timers_001 -->
## NPC Timers

### initnpctimer / startnpctimer
**Syntax:** `initnpctimer {<attach flag>{,"<npc name>"}};`
**Syntax:** `startnpctimer {<attach flag>{,"<npc name>"}};`

Start NPC timer. `initnpctimer` resets to 0.

**Attach Flags:**
- 0 = No player attached (default)
- 1 = Attach current player

---

### stopnpctimer
**Syntax:** `stopnpctimer {<flag>{,"<npc name>"}};`

Stop NPC timer.

**Flags:**
- 0 = Stop timer
- 1 = Detach player
- 2 = Stop and detach

---

### getnpctimer / setnpctimer
**Syntax:** `getnpctimer(<type>{,"<npc name>"})`
**Syntax:** `setnpctimer(<value>{,"<npc name>"})`

Get/set timer value.

**Types:**
- 0 = Current time (ms)
- 1 = Is running? (1/0)
- 2 = Has attached player? (1/0)

---

### attachnpctimer / detachnpctimer
**Syntax:** `attachnpctimer {"<npc name>"};`
**Syntax:** `detachnpctimer {"<npc name>"};`

Attach/detach player to NPC timer.

---

### Timer Label Format
```c
OnTimer<milliseconds>:
    // Code here
    end;

// Examples:
OnTimer1000:    // 1 second
OnTimer60000:   // 1 minute
OnTimer3600000: // 1 hour
```

**Example:**
```c
prontera,155,180,5	script	TimerNPC	4_F_KAFRA1,{
    mes "[Timer NPC]";
    mes "Starting countdown!";
    initnpctimer;
    close;

OnTimer1000:
    mapannounce "prontera","3...",bc_map;
    end;

OnTimer2000:
    mapannounce "prontera","2...",bc_map;
    end;

OnTimer3000:
    mapannounce "prontera","1...",bc_map;
    end;

OnTimer4000:
    mapannounce "prontera","GO!",bc_map;
    stopnpctimer;
    end;
}
```

---

<!-- RAG_CHUNK: waiting_room_001 -->
## Waiting Room / Chat Room

### waitingroom
**Syntax:** `waitingroom "<title>",<limit>{,"<event>"{,<trigger>{,<required zeny>{,<min level>{,<max level>}}}}};`

Create waiting room (chat room).

**Parameters:**
- `limit` = Max players
- `event` = Trigger when players join
- `trigger` = Number to trigger event (0 = when full)

**Example:**
```c
OnInit:
    waitingroom "PvP Arena - Waiting", 10, "MyNPC::OnRoomFull", 10;
    end;

OnRoomFull:
    warpwaitingpc "pvp_n_1-1", 50, 50;
    end;
```

---

### delwaitingroom
**Syntax:** `delwaitingroom {"<npc name>"};`

Delete waiting room.

---

### getwaitingroomusers / getwaitingroomstate
Get waiting room info.

---

### warpwaitingpc
**Syntax:** `warpwaitingpc "<map>",<x>,<y>{,<count>{,"<npc name>"}};`

Warp players from waiting room.

---

### waitingroomkick / waitingroomkickall
Kick players from waiting room.

---

#rathena #script #monster #spawn #npc #control #timer #unit #waitingroom
