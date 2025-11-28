# 02_CORE_API.md
<!-- repo: rathena | branch: claude/github-to-kb-converter-0137h2Ti2PFSsGmn6Xrp3xko | commit: 721d46e | generated: 2025-11-28 -->
<!-- tags: api, functions, commands, scripts, atcommands -->

## Contents
- [Common Module Functions](#common-module-functions)
- [Server Core Functions](#server-core-functions)
- [Script Commands](#script-commands)
- [AT Commands](#at-commands)
- [Item Bonuses](#item-bonuses)

---

## Common Module Functions
<!-- chunk: 02-common | keywords: socket, timer, database, sql -->

### Socket Functions (src/common/socket.cpp)
<!-- chunk: 02-socket | keywords: network, connection, packet -->

| Function | Signature | Description |
|----------|-----------|-------------|
| `make_listen_bind` | `int make_listen_bind(uint32 ip, uint16 port)` | Create listening socket |
| `make_connection` | `int make_connection(uint32 ip, uint16 port, ...)` | Connect to remote server |
| `session_isValid` | `bool session_isValid(int fd)` | Validate session descriptor |
| `session_isActive` | `bool session_isActive(int fd)` | Check if session is active |
| `do_close` | `void do_close(int fd)` | Close socket connection |
| `RFIFOHEAD` | `macro` | Read from input FIFO buffer |
| `WFIFOHEAD` | `macro` | Write to output FIFO buffer |
| `RFIFOP` | `macro(fd, pos)` | Get pointer to read buffer |
| `WFIFOP` | `macro(fd, pos)` | Get pointer to write buffer |

### Timer Functions (src/common/timer.cpp)
<!-- chunk: 02-timer | keywords: scheduling, events, milliseconds -->

| Function | Signature | Description |
|----------|-----------|-------------|
| `add_timer` | `int add_timer(t_tick tick, TimerFunc func, int id, intptr_t data)` | Schedule one-time timer |
| `add_timer_interval` | `int add_timer_interval(t_tick tick, TimerFunc func, int id, intptr_t data, int interval)` | Schedule repeating timer |
| `delete_timer` | `int delete_timer(int tid, TimerFunc func)` | Remove scheduled timer |
| `gettick` | `t_tick gettick(void)` | Get current tick (ms) |
| `gettick_nocache` | `t_tick gettick_nocache(void)` | Get tick without caching |

### Database Functions (src/common/db.cpp)
<!-- chunk: 02-db | keywords: hashtable, btree, storage -->

| Function | Signature | Description |
|----------|-----------|-------------|
| `idb_alloc` | `DBMap* idb_alloc(DBType type, DBOptions options, ...)` | Allocate integer-keyed DB |
| `strdb_alloc` | `DBMap* strdb_alloc(DBType type, DBOptions options, int maxlen)` | Allocate string-keyed DB |
| `db_get` | `DBData db_get(DBMap* self, DBKey key)` | Get value by key |
| `db_put` | `DBData db_put(DBMap* self, DBKey key, DBData data)` | Insert/update value |
| `db_remove` | `DBData db_remove(DBMap* self, DBKey key)` | Remove entry by key |
| `db_foreach` | `void db_foreach(DBMap* self, DBApply func, ...)` | Iterate all entries |
| `db_clear` | `int db_clear(DBMap* self, DBApply func, ...)` | Clear all entries |
| `db_destroy` | `void db_destroy(DBMap* self)` | Free database |

### SQL Functions (src/common/sql.cpp)
<!-- chunk: 02-sql | keywords: mysql, query, database -->

| Function | Signature | Description |
|----------|-----------|-------------|
| `Sql_Connect` | `int Sql_Connect(Sql* self, const char* user, const char* passwd, const char* host, uint16 port, const char* db)` | Connect to MySQL |
| `Sql_Query` | `int Sql_Query(Sql* self, const char* query, ...)` | Execute SQL query |
| `Sql_QueryStr` | `int Sql_QueryStr(Sql* self, const char* query)` | Execute query string |
| `Sql_NumRows` | `uint64 Sql_NumRows(Sql* self)` | Get result row count |
| `Sql_NextRow` | `int Sql_NextRow(Sql* self)` | Fetch next result row |
| `Sql_GetData` | `int Sql_GetData(Sql* self, size_t col, char** out_buf, size_t* out_len)` | Get column data |
| `Sql_FreeResult` | `void Sql_FreeResult(Sql* self)` | Free query result |
| `Sql_EscapeString` | `size_t Sql_EscapeString(Sql* self, char* out_to, const char* from)` | Escape string for SQL |

---

## Server Core Functions
<!-- chunk: 02-servercore | keywords: login, char, map, initialization -->

### Login Server (src/login/)
<!-- chunk: 02-login | keywords: authentication, account, session -->

| Function | Location | Description |
|----------|----------|-------------|
| `login_check_password` | login.cpp | Validate account credentials |
| `login_log` | loginlog.cpp | Log login attempts |
| `login_auth_ok` | login.cpp | Process successful authentication |
| `login_auth_failed` | login.cpp | Handle failed login |
| `ipban_check` | ipban.cpp | Check IP ban status |
| `ipban_log` | ipban.cpp | Log failed attempts for ban |

### Character Server (src/char/)
<!-- chunk: 02-char | keywords: character, guild, party, storage -->

| Function | Location | Description |
|----------|----------|-------------|
| `char_mmo_char_tosql` | char.cpp | Save character to database |
| `char_mmo_char_fromsql` | char.cpp | Load character from database |
| `char_make_new_char` | char.cpp | Create new character |
| `char_delete_char` | char.cpp | Delete character |
| `inter_guild_save` | int_guild.cpp | Save guild data |
| `inter_party_save` | int_party.cpp | Save party data |
| `inter_storage_save` | int_storage.cpp | Save storage data |

### Map Server Core (src/map/)
<!-- chunk: 02-map | keywords: game, world, npc, mob -->

| Function | Location | Description |
|----------|----------|-------------|
| `map_addblock` | map.cpp | Add unit to map block |
| `map_delblock` | map.cpp | Remove unit from map block |
| `map_foreachinarea` | map.cpp | Iterate units in area |
| `map_foreachinrange` | map.cpp | Iterate units in range |
| `map_moveblock` | map.cpp | Move unit between blocks |
| `map_search_freecell` | map.cpp | Find empty cell |
| `map_getcell` | map.cpp | Get cell properties |

### Player Functions (src/map/pc.cpp)
<!-- chunk: 02-pc | keywords: player, character, stats, inventory -->

| Function | Signature | Description |
|----------|-----------|-------------|
| `pc_authok` | `bool pc_authok(map_session_data* sd, ...)` | Process player authentication |
| `pc_setpos` | `int pc_setpos(map_session_data* sd, unsigned short mapindex, int x, int y, clr_type clrtype)` | Warp player to position |
| `pc_additem` | `enum e_additem_result pc_additem(map_session_data* sd, struct item* item, int amount, e_log_pick_type log_type)` | Add item to inventory |
| `pc_delitem` | `int pc_delitem(map_session_data* sd, int n, int amount, int type, short reason, e_log_pick_type log_type)` | Remove item from inventory |
| `pc_equipitem` | `int pc_equipitem(map_session_data* sd, int n, int req_pos)` | Equip item |
| `pc_unequipitem` | `int pc_unequipitem(map_session_data* sd, int n, int flag)` | Unequip item |
| `pc_calcstatus` | `int pc_calcstatus(map_session_data* sd, enum e_status_calc_opt opt)` | Recalculate player stats |
| `pc_gainexp` | `bool pc_gainexp(map_session_data* sd, block_list* src, t_exp base_exp, t_exp job_exp, bool is_quest)` | Award experience |
| `pc_heal` | `int pc_heal(map_session_data* sd, unsigned int hp, unsigned int sp, int type)` | Heal HP/SP |
| `pc_damage` | `int pc_damage(block_list* src, map_session_data* sd, unsigned int hp, unsigned int sp)` | Deal damage to player |

### Battle Functions (src/map/battle.cpp)
<!-- chunk: 02-battle | keywords: damage, combat, calculation -->

| Function | Signature | Description |
|----------|-----------|-------------|
| `battle_calc_attack` | `struct Damage battle_calc_attack(int attack_type, block_list* src, block_list* target, uint16 skill_id, uint16 skill_lv, int count)` | Calculate attack damage |
| `battle_calc_weapon_attack` | `struct Damage battle_calc_weapon_attack(...)` | Calculate weapon damage |
| `battle_calc_magic_attack` | `struct Damage battle_calc_magic_attack(...)` | Calculate magic damage |
| `battle_calc_misc_attack` | `struct Damage battle_calc_misc_attack(...)` | Calculate misc damage |
| `battle_damage` | `int64 battle_damage(block_list* src, block_list* target, int64 damage, t_tick delay, uint16 skill_lv, uint16 skill_id, enum damage_lv dmg_lv, unsigned short attack_type, bool additional_effects, t_tick tick, bool spdamage)` | Apply battle damage |
| `battle_attr_fix` | `int64 battle_attr_fix(...)` | Apply element modifier |

### Skill Functions (src/map/skill.cpp)
<!-- chunk: 02-skill | keywords: skills, casting, effects -->

| Function | Signature | Description |
|----------|-----------|-------------|
| `skill_castend_damage_id` | `int skill_castend_damage_id(...)` | Execute damage skill |
| `skill_castend_nodamage_id` | `int skill_castend_nodamage_id(...)` | Execute support skill |
| `skill_castend_pos2` | `int skill_castend_pos2(...)` | Execute ground-target skill |
| `skill_get_time` | `t_tick skill_get_time(uint16 skill_id, uint16 skill_lv)` | Get skill duration |
| `skill_get_cast` | `t_tick skill_get_cast(uint16 skill_id, uint16 skill_lv)` | Get cast time |
| `skill_check_condition_castbegin` | `bool skill_check_condition_castbegin(...)` | Check cast requirements |
| `skill_consume_requirement` | `int skill_consume_requirement(...)` | Consume skill costs |

### Status Functions (src/map/status.cpp)
<!-- chunk: 02-status | keywords: buffs, debuffs, effects -->

| Function | Signature | Description |
|----------|-----------|-------------|
| `status_change_start` | `int status_change_start(block_list* src, block_list* bl, enum sc_type type, int rate, int val1, int val2, int val3, int val4, t_tick tick, unsigned char flag)` | Apply status effect |
| `status_change_end` | `int status_change_end(block_list* bl, enum sc_type type, int tid)` | Remove status effect |
| `status_calc_pc` | `int status_calc_pc(map_session_data* sd, enum e_status_calc_opt opt)` | Recalculate player status |
| `status_get_class` | `int status_get_class(block_list* bl)` | Get unit class |
| `status_get_lv` | `int status_get_lv(block_list* bl)` | Get unit level |
| `status_get_hp` | `unsigned int status_get_hp(block_list* bl)` | Get current HP |
| `status_get_max_hp` | `unsigned int status_get_max_hp(block_list* bl)` | Get max HP |

---

## Script Commands
<!-- chunk: 02-scriptcmds | keywords: npc, scripting, commands -->

rAthena supports 850+ built-in script commands. Key categories:

### Player Commands
<!-- chunk: 02-script-player | keywords: mes, input, menu, warp -->

| Command | Syntax | Description |
|---------|--------|-------------|
| `mes` | `mes "<string>";` | Display NPC message |
| `next` | `next;` | Wait for player input |
| `close` | `close;` | Close dialog and end |
| `close2` | `close2;` | Close dialog, continue script |
| `menu` | `menu "<opt1>",<label1>{,...};` | Display selection menu |
| `select` | `select("<opt1>"{,...});` | Selection returning index |
| `prompt` | `prompt("<opt1>"{,...});` | Selection with cancel option |
| `input` | `input <variable>{,<min>,<max>};` | Get player input |
| `warp` | `warp "<map>",<x>,<y>;` | Warp attached player |
| `areawarp` | `areawarp "<from>",<x1>,<y1>,<x2>,<y2>,"<to>",<x>,<y>;` | Warp area |

### Item Commands
<!-- chunk: 02-script-items | keywords: getitem, delitem, countitem -->

| Command | Syntax | Description |
|---------|--------|-------------|
| `getitem` | `getitem <item_id>,<amount>{,<account_id>};` | Give item to player |
| `getitem2` | `getitem2 <item_id>,<amount>,<identified>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<account_id>};` | Give item with properties |
| `delitem` | `delitem <item_id>,<amount>{,<account_id>};` | Remove item from player |
| `countitem` | `countitem(<item_id>{,<account_id>});` | Count items in inventory |
| `checkweight` | `checkweight(<item_id>,<amount>{,...});` | Check if can carry |
| `getequipid` | `getequipid(<slot>);` | Get equipped item ID |
| `getequipname` | `getequipname(<slot>);` | Get equipped item name |
| `bonus` | `bonus <type>,<val>;` | Apply item bonus |
| `bonus2` | `bonus2 <type>,<type2>,<val>;` | Apply compound bonus |

### Monster Commands
<!-- chunk: 02-script-mobs | keywords: monster, mobcount, killmonster -->

| Command | Syntax | Description |
|---------|--------|-------------|
| `monster` | `monster "<map>",<x>,<y>,"<name>",<mob_id>,<amount>{,"<event>"};` | Spawn monster |
| `areamonster` | `areamonster "<map>",<x1>,<y1>,<x2>,<y2>,"<name>",<mob_id>,<amount>{,"<event>"};` | Spawn in area |
| `killmonster` | `killmonster "<map>","<event>"{,<type>};` | Kill monsters |
| `mobcount` | `mobcount("<map>","<event>");` | Count monsters |
| `summon` | `summon "<name>",<mob_id>{,<timeout>};` | Summon slave mob |

### Variable Commands
<!-- chunk: 02-script-vars | keywords: set, getarg, setarray -->

| Command | Syntax | Description |
|---------|--------|-------------|
| `set` | `set <variable>,<value>;` | Set variable value |
| `setarray` | `setarray <array>[<index>],<val1>{,<val2>,...};` | Set array values |
| `getarraysize` | `getarraysize(<array>);` | Get array length |
| `getelementofarray` | `getelementofarray(<array>,<index>);` | Get array element |
| `cleararray` | `cleararray <array>[<index>],<value>,<amount>;` | Clear array values |
| `copyarray` | `copyarray <dest>[<index>],<src>[<index>],<amount>;` | Copy array |

### Variable Scope Prefixes

| Prefix | Scope | Persistence | Example |
|--------|-------|-------------|---------|
| (none) | NPC | Until NPC ends | `.npcvar` |
| `@` | Player | Until logout | `@tempvar` |
| `$` | Global | Permanent (mapreg) | `$globalvar` |
| `$@` | Global | Until restart | `$@tempglobal` |
| `#` | Account | Permanent | `#CASHPOINTS` |
| `##` | Account Global | Permanent, all chars | `##KAFRAPOINTS` |

### Party/Guild Commands
<!-- chunk: 02-script-social | keywords: party, guild, getpartymember -->

| Command | Syntax | Description |
|---------|--------|-------------|
| `getpartymember` | `getpartymember <party_id>{,<type>};` | Get party member info |
| `getpartyleader` | `getpartyleader(<party_id>{,<type>});` | Get party leader |
| `party_create` | `party_create("<name>"{,<char_id>,<item>,<item2>});` | Create party |
| `getguildmember` | `getguildmember <guild_id>{,<type>};` | Get guild member info |
| `getguildmaster` | `getguildmaster(<guild_id>);` | Get guild master name |
| `guildchangegm` | `guildchangegm <guild_id>,"<new_master_name>";` | Change guild master |

### Instance Commands
<!-- chunk: 02-script-instance | keywords: instance, dungeon, create -->

| Command | Syntax | Description |
|---------|--------|-------------|
| `instance_create` | `instance_create("<name>"{,<party_id>,<mode>});` | Create instance |
| `instance_destroy` | `instance_destroy({<instance_id>});` | Destroy instance |
| `instance_enter` | `instance_enter("<map>"{,<x>,<y>,<char_id>,<instance_id>});` | Enter instance |
| `instance_warpall` | `instance_warpall "<map>",<x>,<y>{,<instance_id>};` | Warp all party |
| `instance_announce` | `instance_announce <instance_id>,"<text>",<flag>{,<font_color>,<font_type>,<font_size>,<font_align>,<font_y>};` | Instance announcement |

---

## AT Commands
<!-- chunk: 02-atcommands | keywords: gm, admin, commands -->

Full reference in `doc/atcommands.txt`. Key commands:

### System Commands
<!-- chunk: 02-at-system | keywords: version, rates, uptime -->

| Command | Syntax | Description |
|---------|--------|-------------|
| `@version` | `@version` | Display server version |
| `@rates` | `@rates` | Display server rates |
| `@time` | `@time` | Display server time |
| `@uptime` | `@uptime` | Show server uptime |
| `@refresh` | `@refresh` | Sync client position |
| `@refreshall` | `@refreshall` | Refresh all players |

### Database Commands
<!-- chunk: 02-at-database | keywords: mobinfo, iteminfo, whodrops -->

| Command | Syntax | Description |
|---------|--------|-------------|
| `@mobinfo` | `@mobinfo <mob_name/id>` | Show monster info |
| `@iteminfo` | `@iteminfo <item_name/id>` | Show item info |
| `@whodrops` | `@whodrops <item_name/id>` | Show drop sources |
| `@whereis` | `@whereis <mob_name/id>` | Show monster locations |
| `@autoloot` | `@autoloot {<%>}` | Toggle auto-looting |
| `@alootid` | `@alootid <+/- item>` | Autoloot specific item |

### Player Commands
<!-- chunk: 02-at-player | keywords: warp, job, stat -->

| Command | Syntax | Description |
|---------|--------|-------------|
| `@go` | `@go <number/city>` | Warp to city |
| `@warp` | `@warp <map> {<x> <y>}` | Warp to map |
| `@jump` | `@jump {<x> <y>}` | Jump to coordinates |
| `@where` | `@where {<player>}` | Show player location |
| `@job` | `@job <job_id/name>` | Change job class |
| `@lvup` | `@lvup <levels>` | Increase base level |
| `@jlvup` | `@jlvup <levels>` | Increase job level |
| `@stat` | `@str/agi/vit/int/dex/luk <value>` | Set stat value |
| `@allstats` | `@allstats <value>` | Set all stats |

### Admin Commands
<!-- chunk: 02-at-admin | keywords: item, monster, kick, ban -->

| Command | Syntax | Description |
|---------|--------|-------------|
| `@item` | `@item <item_id> {<amount>}` | Create item |
| `@item2` | `@item2 <id> <qty> <iden> <ref> <attr> <c1> <c2> <c3> <c4>` | Create item with props |
| `@monster` | `@monster <name> {<amount>}` | Spawn monster |
| `@killmonster` | `@killmonster {<map>}` | Kill all monsters |
| `@kick` | `@kick <player>` | Kick player |
| `@ban` | `@ban <time> <player>` | Ban player |
| `@jail` | `@jail <player>` | Jail player |
| `@broadcast` | `@broadcast <message>` | Server broadcast |
| `@localbroadcast` | `@localbroadcast <message>` | Map broadcast |

---

## Item Bonuses
<!-- chunk: 02-bonuses | keywords: bonus, equipment, effects -->

Full reference in `doc/item_bonus.txt`. Used in item scripts.

### Basic Stat Bonuses
<!-- chunk: 02-bonus-stats | keywords: str, agi, vit, int, dex, luk -->

| Bonus | Syntax | Effect |
|-------|--------|--------|
| `bStr` | `bonus bStr,n;` | STR + n |
| `bAgi` | `bonus bAgi,n;` | AGI + n |
| `bVit` | `bonus bVit,n;` | VIT + n |
| `bInt` | `bonus bInt,n;` | INT + n |
| `bDex` | `bonus bDex,n;` | DEX + n |
| `bLuk` | `bonus bLuk,n;` | LUK + n |
| `bAllStats` | `bonus bAllStats,n;` | All stats + n |
| `bMaxHP` | `bonus bMaxHP,n;` | Max HP + n |
| `bMaxHPrate` | `bonus bMaxHPrate,n;` | Max HP + n% |
| `bMaxSP` | `bonus bMaxSP,n;` | Max SP + n |
| `bMaxSPrate` | `bonus bMaxSPrate,n;` | Max SP + n% |

### Attack/Defense Bonuses
<!-- chunk: 02-bonus-combat | keywords: atk, def, matk, mdef -->

| Bonus | Syntax | Effect |
|-------|--------|--------|
| `bBaseAtk` | `bonus bBaseAtk,n;` | Base ATK + n |
| `bAtk` | `bonus bAtk,n;` | ATK + n |
| `bAtkRate` | `bonus bAtkRate,n;` | ATK + n% |
| `bMatk` | `bonus bMatk,n;` | MATK + n |
| `bMatkRate` | `bonus bMatkRate,n;` | MATK + n% |
| `bDef` | `bonus bDef,n;` | DEF + n |
| `bDefRate` | `bonus bDefRate,n;` | DEF + n% |
| `bMdef` | `bonus bMdef,n;` | MDEF + n |
| `bMdefRate` | `bonus bMdefRate,n;` | MDEF + n% |

### Combat Bonuses
<!-- chunk: 02-bonus-hit | keywords: hit, flee, critical, aspd -->

| Bonus | Syntax | Effect |
|-------|--------|--------|
| `bHit` | `bonus bHit,n;` | Hit + n |
| `bHitRate` | `bonus bHitRate,n;` | Hit + n% |
| `bCritical` | `bonus bCritical,n;` | Critical + n |
| `bCriticalRate` | `bonus bCriticalRate,n;` | Critical + n% |
| `bFlee` | `bonus bFlee,n;` | Flee + n |
| `bFleeRate` | `bonus bFleeRate,n;` | Flee + n% |
| `bFlee2` | `bonus bFlee2,n;` | Perfect Dodge + n |
| `bAspd` | `bonus bAspd,n;` | ASPD + n |
| `bAspdRate` | `bonus bAspdRate,n;` | ASPD + n% |

### Damage Modifiers
<!-- chunk: 02-bonus-damage | keywords: race, element, size -->

| Bonus | Syntax | Effect |
|-------|--------|--------|
| `bAddRace` | `bonus2 bAddRace,r,x;` | +x% damage vs race r |
| `bAddEle` | `bonus2 bAddEle,e,x;` | +x% damage vs element e |
| `bAddSize` | `bonus2 bAddSize,s,x;` | +x% damage vs size s |
| `bSubRace` | `bonus2 bSubRace,r,x;` | +x% reduction from race r |
| `bSubEle` | `bonus2 bSubEle,e,x;` | +x% reduction from element e |
| `bMagicAddRace` | `bonus2 bMagicAddRace,r,x;` | +x% magic vs race r |
| `bMagicAddEle` | `bonus2 bMagicAddEle,e,x;` | +x% magic vs element e |

### AutoSpell Bonuses
<!-- chunk: 02-bonus-autospell | keywords: autospell, trigger, chance -->

| Bonus | Syntax | Effect |
|-------|--------|--------|
| `bAutoSpell` | `bonus3 bAutoSpell,sk,y,n;` | n/10% chance to cast skill sk level y when attacking |
| `bAutoSpellWhenHit` | `bonus3 bAutoSpellWhenHit,sk,y,n;` | n/10% chance to cast when hit |
| `bAutoSpellOnSkill` | `bonus4 bAutoSpellOnSkill,sk,x,y,n;` | n/10% chance to cast x when using skill sk |

### Constant Values

**Elements (e):** `Ele_Neutral`, `Ele_Water`, `Ele_Earth`, `Ele_Fire`, `Ele_Wind`, `Ele_Poison`, `Ele_Holy`, `Ele_Dark`, `Ele_Ghost`, `Ele_Undead`

**Races (r):** `RC_Formless`, `RC_Undead`, `RC_Brute`, `RC_Plant`, `RC_Insect`, `RC_Fish`, `RC_Demon`, `RC_DemiHuman`, `RC_Angel`, `RC_Dragon`

**Sizes (s):** `Size_Small`, `Size_Medium`, `Size_Large`

**Classes (c):** `Class_Normal`, `Class_Boss`, `Class_Guardian`

---

## Quick Links

- Architecture Overview: → See [[01_ARCHITECTURE]]
- Data Models: → See [[03_DATA_MODELS]]
- Configuration: → See [[05_CONFIG]]
- Examples: → See [[07_EXAMPLES]]
