# 08_QUICK_REF.md
<!-- repo: rathena | branch: claude/github-to-kb-converter-0137h2Ti2PFSsGmn6Xrp3xko | commit: 721d46e | generated: 2025-11-28 -->
<!-- tags: reference, index, cheatsheet, lookup -->

## Contents
- [Command Cheatsheet](#command-cheatsheet)
- [Function Index](#function-index)
- [Configuration Index](#configuration-index)
- [File Purpose Index](#file-purpose-index)
- [Glossary](#glossary)

---

## Command Cheatsheet
<!-- chunk: 08-cheatsheet | keywords: commands, quick, reference -->

### Server Management

| Command | Description |
|---------|-------------|
| `./athena-start start` | Start all servers |
| `./athena-start stop` | Stop all servers |
| `./athena-start restart` | Restart all servers |
| `./athena-start status` | Check server status |

### Build Commands

| Command | Description |
|---------|-------------|
| `cmake ..` | Configure build |
| `make` | Compile all |
| `make install` | Install binaries |
| `make clean` | Clean build |

### Database Setup

| Command | Description |
|---------|-------------|
| `mysql -u root -p ragnarok < sql-files/main.sql` | Core tables |
| `mysql -u root -p ragnarok < sql-files/logs.sql` | Log tables |
| `mysql -u root -p ragnarok < sql-files/web.sql` | Web tables |

### Common AT Commands
→ Full reference: [[02_CORE_API#at-commands]]

| Command | Description |
|---------|-------------|
| `@go 0` | Warp to Prontera |
| `@warp <map> <x> <y>` | Warp to location |
| `@item <id> <qty>` | Create item |
| `@monster <name> <qty>` | Spawn monster |
| `@heal` | Full heal |
| `@job <id>` | Change job |
| `@lvup <n>` | Add base levels |
| `@allstats <n>` | Set all stats |
| `@kick <name>` | Kick player |
| `@ban <time> <name>` | Ban player |
| `@reloadscript` | Reload NPC scripts |
| `@rates` | Show server rates |

### Script Command Quick Reference
→ Full reference: [[02_CORE_API#script-commands]]

| Command | Usage |
|---------|-------|
| `mes` | `mes "text";` |
| `next` | `next;` |
| `close` | `close;` |
| `menu` | `menu "A",L_A,"B",L_B;` |
| `select` | `select("A","B","C")` |
| `warp` | `warp "map",x,y;` |
| `getitem` | `getitem id,qty;` |
| `delitem` | `delitem id,qty;` |
| `countitem` | `countitem(id)` |
| `set` | `set var,value;` |
| `if` | `if (cond) { }` |
| `for` | `for (.@i=0;.@i<10;.@i++)` |
| `monster` | `monster "map",x,y,"name",id,qty;` |

---

## Function Index
<!-- chunk: 08-functions | keywords: function, api, index -->

### Common Module
→ Details: [[02_CORE_API#common-module-functions]]

| Function | Module | Link |
|----------|--------|------|
| `add_timer` | timer | [[02_CORE_API#timer-functions]] |
| `add_timer_interval` | timer | [[02_CORE_API#timer-functions]] |
| `db_get` | db | [[02_CORE_API#database-functions]] |
| `db_put` | db | [[02_CORE_API#database-functions]] |
| `gettick` | timer | [[02_CORE_API#timer-functions]] |
| `make_connection` | socket | [[02_CORE_API#socket-functions]] |
| `Sql_Query` | sql | [[02_CORE_API#sql-functions]] |

### Map Server
→ Details: [[02_CORE_API#server-core-functions]]

| Function | Module | Link |
|----------|--------|------|
| `battle_calc_attack` | battle | [[02_CORE_API#battle-functions]] |
| `battle_damage` | battle | [[02_CORE_API#battle-functions]] |
| `map_foreachinrange` | map | [[02_CORE_API#map-server-core]] |
| `pc_additem` | pc | [[02_CORE_API#player-functions]] |
| `pc_delitem` | pc | [[02_CORE_API#player-functions]] |
| `pc_setpos` | pc | [[02_CORE_API#player-functions]] |
| `skill_castend_damage_id` | skill | [[02_CORE_API#skill-functions]] |
| `status_change_start` | status | [[02_CORE_API#status-functions]] |
| `status_change_end` | status | [[02_CORE_API#status-functions]] |

---

## Configuration Index
<!-- chunk: 08-config | keywords: config, settings, index -->

### Server Ports
→ Details: [[05_CONFIG#server-configuration-files]]

| Service | Port | Config File |
|---------|------|-------------|
| Login Server | 6900 | `login_athena.conf` |
| Char Server | 6121 | `char_athena.conf` |
| Map Server | 5121 | `map_athena.conf` |
| Web Server | 8888 | `web_athena.conf` |
| MySQL | 3306 | `inter_athena.conf` |

### Rate Settings
→ Details: [[05_CONFIG#experience-and-drops]]

| Setting | File | Link |
|---------|------|------|
| `base_exp_rate` | exp.conf | [[05_CONFIG#experience-settings]] |
| `job_exp_rate` | exp.conf | [[05_CONFIG#experience-settings]] |
| `item_rate_common` | drops.conf | [[05_CONFIG#drop-settings]] |
| `item_rate_card` | drops.conf | [[05_CONFIG#drop-settings]] |
| `death_penalty_base` | exp.conf | [[05_CONFIG#experience-settings]] |

### Key Battle Settings
→ Details: [[05_CONFIG#battle-configuration]]

| Setting | File | Link |
|---------|------|------|
| `enable_critical` | battle.conf | [[05_CONFIG#core-battle-settings]] |
| `agi_penalty_type` | battle.conf | [[05_CONFIG#core-battle-settings]] |
| `delay_battle_damage` | battle.conf | [[05_CONFIG#core-battle-settings]] |

---

## File Purpose Index
<!-- chunk: 08-files | keywords: files, directory, purpose -->

### Source Files (src/)
→ Details: [[01_ARCHITECTURE#directory-structure]]

| Path | Purpose |
|------|---------|
| `src/common/` | Shared libraries |
| `src/common/socket.cpp` | Network I/O |
| `src/common/timer.cpp` | Event scheduling |
| `src/common/db.cpp` | In-memory databases |
| `src/common/sql.cpp` | MySQL client |
| `src/login/login.cpp` | Login server main |
| `src/char/char.cpp` | Character server main |
| `src/map/map.cpp` | Map server main |
| `src/map/pc.cpp` | Player character logic |
| `src/map/mob.cpp` | Monster logic |
| `src/map/skill.cpp` | Skill system |
| `src/map/battle.cpp` | Combat calculation |
| `src/map/status.cpp` | Status effects |
| `src/map/script.cpp` | Script interpreter |
| `src/map/clif.cpp` | Client packets |
| `src/map/atcommand.cpp` | GM commands |

### Configuration Files (conf/)
→ Details: [[05_CONFIG]]

| Path | Purpose |
|------|---------|
| `conf/login_athena.conf` | Login server config |
| `conf/char_athena.conf` | Char server config |
| `conf/map_athena.conf` | Map server config |
| `conf/inter_athena.conf` | Database config |
| `conf/battle_athena.conf` | Battle config loader |
| `conf/battle/` | Battle sub-configs |
| `conf/groups.yml` | Player permissions |
| `conf/atcommands.yml` | AT command config |

### Database Files (db/)
→ Details: [[03_DATA_MODELS#yaml-data-format]]

| Path | Purpose |
|------|---------|
| `db/item_db.yml` | Item definitions |
| `db/mob_db.yml` | Monster definitions |
| `db/skill_db.yml` | Skill definitions |
| `db/re/` | Renewal mode data |
| `db/pre-re/` | Pre-renewal data |
| `db/import/` | Custom imports |

### SQL Files (sql-files/)
→ Details: [[03_DATA_MODELS#mysql-database-schema]]

| Path | Purpose |
|------|---------|
| `sql-files/main.sql` | Core tables |
| `sql-files/logs.sql` | Log tables |
| `sql-files/web.sql` | Web tables |
| `sql-files/upgrades/` | Migration scripts |

### NPC Scripts (npc/)
→ Details: [[01_ARCHITECTURE#directory-structure]]

| Path | Purpose |
|------|---------|
| `npc/scripts_athena.conf` | Main loader |
| `npc/scripts_custom.conf` | Custom scripts |
| `npc/re/` | Renewal content |
| `npc/pre-re/` | Pre-renewal content |
| `npc/custom/` | User scripts |

### Documentation (doc/)

| Path | Purpose |
|------|---------|
| `doc/script_commands.txt` | Script reference (433KB) |
| `doc/atcommands.txt` | AT command reference |
| `doc/item_bonus.txt` | Item bonus reference |
| `doc/source_doc.txt` | Source documentation |

---

## Glossary
<!-- chunk: 08-glossary | keywords: terms, definitions, glossary -->

### Server Terms

| Term | Definition |
|------|------------|
| **Login Server** | Handles authentication and account management |
| **Char Server** | Manages character data, guilds, parties |
| **Map Server** | Game world, combat, NPCs, skills |
| **Inter-Server** | Communication between servers |
| **PACKETVER** | Client version date (e.g., 20211103) |

### Game Terms

| Term | Definition |
|------|------------|
| **Renewal** | Modern game mechanics (2010+) |
| **Pre-Renewal** | Classic game mechanics |
| **WoE** | War of Emperium (guild siege) |
| **MVP** | Boss monster / Most Valuable Player |
| **Instance** | Private dungeon copy |
| **Battleground** | PvP arena mode |

### Data Terms
→ Details: [[03_DATA_MODELS#core-data-structures]]

| Term | Definition |
|------|------------|
| **block_list (bl)** | Base unit structure |
| **map_session_data (sd)** | Player session data |
| **status_change (sc)** | Status effect container |
| **status_change_entry (sce)** | Single status effect |
| **mob_data (md)** | Monster instance data |
| **npc_data (nd)** | NPC instance data |

### Script Terms
→ Details: [[02_CORE_API#variable-scope-prefixes]]

| Term | Definition |
|------|------------|
| **@var** | Player temporary variable |
| **$var** | Global permanent variable |
| **$@var** | Global temporary variable |
| **#var** | Account permanent variable |
| **.var** | NPC scope variable |
| **'var** | Instance variable |

### Configuration Terms

| Term | Definition |
|------|------------|
| **Note 1** | Boolean (on/off, yes/no, 1/0) |
| **Note 2** | Percentage (100 = 100%) |
| **Note 3** | Bitmask (add values) |

### Database Terms
→ Details: [[03_DATA_MODELS]]

| Term | Definition |
|------|------------|
| **account_id** | Account identifier |
| **char_id** | Character identifier |
| **nameid** | Item identifier |
| **mob_id** | Monster identifier |
| **skill_id** | Skill identifier |

---

## Error Code Reference
<!-- chunk: 08-errors | keywords: errors, codes, reference -->
→ Details: [[06_DEBUG#common-errors]]

### Login State Codes

| Code | Meaning |
|------|---------|
| 0 | OK |
| 1 | Invalid password |
| 2 | Expired |
| 5 | IP banned |
| 6 | Account banned |

### Script Return Codes

| Code | Meaning |
|------|---------|
| 0 | Success/False |
| 1 | Success/True |
| -1 | Failure/Error |

---

## Quick Navigation

| Topic | KB File |
|-------|---------|
| Architecture | [[01_ARCHITECTURE]] |
| API Reference | [[02_CORE_API]] |
| Data Models | [[03_DATA_MODELS]] |
| Code Patterns | [[04_PATTERNS]] |
| Configuration | [[05_CONFIG]] |
| Debugging | [[06_DEBUG]] |
| Examples | [[07_EXAMPLES]] |
| This Index | [[08_QUICK_REF]] |
