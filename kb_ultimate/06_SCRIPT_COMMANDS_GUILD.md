# rAthena Script Commands - Guild Reference
## Complete Guild & WoE Management Commands

---

<!-- RAG_CHUNK: guild_info_001 -->
## Guild Information

### getguildname
**Syntax:** `getguildname(<guild id>)`

Get guild name from ID.

**Example:**
```c
.@gid = getcharid(2);
if (.@gid)
    mes "Guild: " + getguildname(.@gid);
else
    mes "You are not in a guild.";
```

---

### getguildmaster
**Syntax:** `getguildmaster(<guild id>)`

Get guild master's name.

---

### getguildmasterid
**Syntax:** `getguildmasterid(<guild id>)`

Get guild master's character ID.

---

### is_guild_leader
**Syntax:** `is_guild_leader({<guild id>{,<char id>}})`

Check if player is guild master. Returns 1 or 0.

---

### getguildmember
**Syntax:** `getguildmember(<guild id>{,<type>{,<array>}});`

Get guild member data.

**Types:**
- 0 = Name array ($@guildmembername$[])
- 1 = Character ID array ($@guildmembercid[])
- 2 = Account ID array ($@guildmemberaid[])

**Also Sets:**
```c
$@guildmembercount
```

**Example:**
```c
.@gid = getcharid(2);
getguildmember .@gid, 0;
mes "Guild has " + $@guildmembercount + " members:";
for (.@i = 0; .@i < $@guildmembercount; .@i++)
    mes "- " + $@guildmembername$[.@i];
```

---

### getguildinfo
**Syntax:** `getguildinfo(<type>{,<guild id>{,<char id>}})`

Get detailed guild information.

**Types:**
```c
GUILDINFO_ID           // Guild ID
GUILDINFO_NAME         // Guild name
GUILDINFO_MASTER_NAME  // Master name
GUILDINFO_MASTER_CID   // Master character ID
GUILDINFO_ONLINE_MEMBERS // Online member count
GUILDINFO_AFK_MEMBERS  // AFK member count
GUILDINFO_MEMBERS      // Total members
GUILDINFO_MAX_MEMBERS  // Max member capacity
GUILDINFO_AVERAGE_LV   // Average level
GUILDINFO_EXP          // Guild EXP
GUILDINFO_NEXT_EXP     // EXP to next level
GUILDINFO_LV           // Guild level
GUILDINFO_SKILL_POINTS // Skill points
GUILDINFO_CASTLES      // Owned castles
```

---

### getguildalliance
**Syntax:** `getguildalliance(<guild id1>,<guild id2>)`

Get alliance status between guilds.

**Returns:**
- -1 = War
- 0 = No relation
- 1 = Alliance

---

### guild_has_permission
**Syntax:** `guild_has_permission(<permission>{,<char id>})`

Check player's guild permissions.

**Permissions:**
```c
GUILD_PERM_INVITE       // Can invite members
GUILD_PERM_EXPEL        // Can kick members
GUILD_PERM_STORAGE      // Can access guild storage
GUILD_PERM_ALL          // All permissions
```

---

<!-- RAG_CHUNK: guild_actions_001 -->
## Guild Actions

### guildchangegm
**Syntax:** `guildchangegm(<guild id>,"<new master name>")`

Transfer guild leadership.

**Example:**
```c
if (is_guild_leader()) {
    mes "Enter new master name:";
    input .@name$;
    if (guildchangegm(getcharid(2), .@name$))
        mes "Leadership transferred!";
    else
        mes "Transfer failed!";
}
```

---

### guildgetexp
**Syntax:** `guildgetexp(<exp>{,<char id>});`

Give EXP to player's guild.

---

### guildskill
**Syntax:** `guildskill(<skill id>,<level>{,<guild id>{,<char id>}});`

Add guild skill. Level must be sequential.

**Guild Skills:**
```c
GD_APPROVAL       // Guild Approval
GD_KAFRACONTRACT  // Kafra Contract
GD_GUARDRESEARCH  // Guardian Research
GD_GUARDUP        // Strengthen Guardian
GD_EXTENSION      // Guild Extension
GD_GLORYGUILD     // Glory of Guild
GD_LEADERSHIP     // Great Leadership
GD_GLORYWOUNDS    // Wounds of Glory
GD_SOULCOLD       // Soul of Cold
GD_HAWKEYES       // Sharp Eyes
GD_BATTLEORDER    // Battle Orders
GD_REGENERATION   // Regeneration
GD_RESTORE        // Restoration
GD_EMERGENCYCALL  // Emergency Call
GD_DEVELOPMENT    // Development
GD_ITEMEMERGENCYCALL // Item Emergency Call
```

---

### getgdskilllv
**Syntax:** `getgdskilllv(<guild id>,<skill id>)`

Get guild skill level.

---

<!-- RAG_CHUNK: guild_storage_001 -->
## Guild Storage

### guildopenstorage
**Syntax:** `guildopenstorage()`

Open guild storage. Returns status code.

**Return Values:**
```c
GSTORAGE_OPEN                    // Success
GSTORAGE_STORAGE_ALREADY_OPEN    // Storage already open
GSTORAGE_ALREADY_OPEN            // Guild storage in use
GSTORAGE_NO_GUILD                // Not in guild
GSTORAGE_NO_PERMISSION           // No access permission
```

**Example:**
```c
.@result = guildopenstorage();
if (.@result == GSTORAGE_OPEN) {
    // Storage opened
} else if (.@result == GSTORAGE_NO_PERMISSION) {
    mes "You don't have permission!";
}
```

---

### guildopenstorage_log
**Syntax:** `guildopenstorage_log(<guild id>{,<char id>})`

Get guild storage access log.

---

### guildstoragecountitem
**Syntax:** `guildstoragecountitem(<item id>)`

Count items in guild storage.

---

### guildstoragecountitem2
Count items with specific properties in guild storage.

---

<!-- RAG_CHUNK: woe_commands_001 -->
## War of Emperium (WoE)

### agitstart / agitend
**Syntax:** `agitstart;`
**Syntax:** `agitend;`

Start/end WoE FE.

---

### agitstart2 / agitend2
Start/end WoE SE.

---

### agitstart3 / agitend3
Start/end WoE TE.

---

### agitcheck / agitcheck2 / agitcheck3
**Syntax:** `agitcheck()`

Check if WoE is active. Returns 1 or 0.

---

### gvgon / gvgoff
**Syntax:** `gvgon "<map>";`
**Syntax:** `gvgoff "<map>";`

Enable/disable GvG on map.

---

### flagemblem
**Syntax:** `flagemblem(<guild id>);`

Display guild emblem on NPC (for castle flags).

---

<!-- RAG_CHUNK: castle_commands_001 -->
## Castle Commands

### setcastledata / getcastledata
**Syntax:** `setcastledata("<map>",<index>,<value>);`
**Syntax:** `getcastledata("<map>",<index>)`

Manage castle data.

**Indexes:**
```c
CD_GUILD_ID              // 1: Owning guild ID
CD_CURRENT_ECONOMY       // 2: Current economy
CD_CURRENT_DEFENSE       // 3: Current defense
CD_INVESTED_ECONOMY      // 4: Investment (economy)
CD_INVESTED_DEFENSE      // 5: Investment (defense)
CD_CREATE_GUARDIAN_TIME  // 6: Time to create guardian
CD_ENABLED_KAFRA         // 7: Kafra enabled
CD_ENABLED_GUARDIAN00    // 8-15: Guardian enabled
CD_GUARDIAN_HP           // Guardian HP values
```

**Example:**
```c
// Check castle owner
.@owner = getcastledata("prtg_cas01", CD_GUILD_ID);
if (.@owner)
    mes "Castle owned by: " + getguildname(.@owner);
else
    mes "Castle has no owner.";
```

---

### getcastlename
**Syntax:** `getcastlename("<map>")`

Get castle display name.

---

### guardian
**Syntax:** `guardian "<map>",<x>,<y>,"<name>",<mob id>,<amount>{,"<event>"{,<guardian index>}};`

Spawn castle guardian.

**Example:**
```c
guardian "prtg_cas01",100,100,"Guardian",1285,1,"",0;
```

---

### guardianinfo
**Syntax:** `guardianinfo("<map>",<index>,<type>)`

Get guardian information.

**Types:**
- 0 = Is alive? (1/0)
- 1 = Display name

---

### maprespawnguildid
**Syntax:** `maprespawnguildid "<map>",<guild id>,<flag>;`

Respawn monsters to specific guild.

**Flags:**
- 1 = All except guild
- 2 = Guild only
- 4 = All

---

<!-- RAG_CHUNK: battleground_001 -->
## Battleground

### waitingroom2bg / waitingroom2bg_single
**Syntax:** `waitingroom2bg("<map>",<x>,<y>,{"<event death>",{"<event quit>"{,"<npc name>"}}})`
**Syntax:** `waitingroom2bg_single(<team id>,{"<npc name>"{,<x>,<y>}})`

Create battleground team from waiting room.

**Example:**
```c
OnInit:
    waitingroom "Blue Team",5;
    end;

OnStart:
    .@bg = waitingroom2bg("bat_a01",50,50,"BG_NPC::OnDeath","BG_NPC::OnQuit");
    end;
```

---

### bg_create
**Syntax:** `bg_create("<map>",<x>,<y>{,"<event death>"{,"<event quit>"}})`

Create empty BG team. Returns team ID.

---

### bg_join
**Syntax:** `bg_join(<team id>{,<char id>})`

Add player to BG team.

---

### bg_team_setxy
**Syntax:** `bg_team_setxy(<team id>,<x>,<y>)`

Set team respawn point.

---

### bg_warp
**Syntax:** `bg_warp(<team id>,"<map>",<x>,<y>)`

Warp entire team.

---

### bg_monster
**Syntax:** `bg_monster(<team id>,"<map>",<x>,<y>,"<name>",<mob id>,<amount>{,"<event>"})`

Spawn BG monster.

---

### bg_monster_set_team
**Syntax:** `bg_monster_set_team(<gid>,<team id>)`

Assign monster to BG team.

---

### bg_leave
**Syntax:** `bg_leave({<char id>})`

Remove player from BG team.

---

### bg_destroy
**Syntax:** `bg_destroy(<team id>)`

Destroy BG team.

---

### bg_get_data
**Syntax:** `bg_get_data(<team id>,<type>)`

Get BG team data.

**Types:**
- 0 = Member count

---

### bg_getareausers
**Syntax:** `bg_getareausers(<team id>,"<map>",<x1>,<y1>,<x2>,<y2>)`

Count team members in area.

---

### bg_updatescore
**Syntax:** `bg_updatescore("<map>",<team1 score>,<team2 score>)`

Update BG scoreboard.

---

### bg_info
**Syntax:** `bg_info("<queue name>",<type>)`

Get BG queue info.

---

#rathena #script #guild #woe #castle #battleground #gvg #commands
