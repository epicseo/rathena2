# 05_CONFIG.md
<!-- repo: rathena | branch: claude/github-to-kb-converter-0137h2Ti2PFSsGmn6Xrp3xko | commit: 721d46e | generated: 2025-11-28 -->
<!-- tags: configuration, settings, environment, deployment -->

## Contents
- [Server Configuration Files](#server-configuration-files)
- [Database Configuration](#database-configuration)
- [Battle Configuration](#battle-configuration)
- [Experience and Drops](#experience-and-drops)
- [Build and Deployment](#build-and-deployment)

---

## Server Configuration Files
<!-- chunk: 05-servers | keywords: login, char, map, web, ports -->

### Configuration File Locations

| File | Server | Purpose |
|------|--------|---------|
| `conf/login_athena.conf` | Login | Authentication settings |
| `conf/char_athena.conf` | Character | Character management |
| `conf/map_athena.conf` | Map | Game world settings |
| `conf/web_athena.conf` | Web | REST API settings |
| `conf/inter_athena.conf` | All | Database connections |
| `conf/battle_athena.conf` | Map | Game balance (imports) |
| `conf/groups.yml` | All | Player permissions |

### Login Server (login_athena.conf)
<!-- chunk: 05-login | keywords: login, port, authentication -->

| Setting | Default | Description |
|---------|---------|-------------|
| `login_port` | 6900 | Login server port |
| `new_account` | no | Allow _M/_F account creation |
| `use_MD5_passwords` | no | Store passwords as MD5 |
| `ipban_enable` | yes | Enable IP banning |
| `ipban_dynamic_pass_failure_ban` | yes | Auto-ban failed logins |
| `ipban_dynamic_pass_failure_ban_interval` | 5 | Minutes to track failures |
| `ipban_dynamic_pass_failure_ban_limit` | 7 | Max failures before ban |
| `ipban_dynamic_pass_failure_ban_duration` | 5 | Ban duration (minutes) |
| `use_dnsbl` | no | Enable DNS blacklist |
| `client_hash_check` | off | Client MD5 verification |
| `use_web_auth_token` | yes | Enable web auth tokens |
| `chars_per_account` | 0 | Characters per account (0=MIN_CHARS) |
| `vip_char_increase` | -1 | Extra VIP character slots |

### Character Server (char_athena.conf)
<!-- chunk: 05-char | keywords: character, creation, deletion -->

| Setting | Default | Description |
|---------|---------|-------------|
| `userid` | s1 | Inter-server username |
| `passwd` | p1 | Inter-server password |
| `server_name` | rAthena | Server display name |
| `login_port` | 6900 | Login server port |
| `char_port` | 6121 | Character server port |
| `max_connect_user` | -1 | Max users (-1=unlimited) |
| `gm_allow_group` | 99 | Group ID to bypass limits |
| `autosave_time` | 60 | Guild save interval (sec) |
| `start_point` | iz_int,18,26 | New character spawn |
| `start_items` | 1201,1,2:2301,1,16 | Starting equipment |
| `start_zeny` | 0 | Starting money |
| `char_del_delay` | 86400 | Delete delay (sec, 24h) |
| `char_del_level` | 0 | Level delete restriction |
| `pincode_enabled` | yes | Require pincode |
| `char_move_enabled` | yes | Allow slot moves |

### Map Server (map_athena.conf)
<!-- chunk: 05-map | keywords: map, game, world -->

| Setting | Default | Description |
|---------|---------|-------------|
| `userid` | s1 | Inter-server username |
| `passwd` | p1 | Inter-server password |
| `char_port` | 6121 | Character server port |
| `map_port` | 5121 | Map server port |
| `db_path` | db | Database files path |
| `autosave_time` | 300 | Character save interval (sec) |
| `minsave_time` | 100 | Min save interval (ms) |
| `save_settings` | 4095 | Auto-save triggers |
| `motd_txt` | conf/motd.txt | Message of the day |
| `use_grf` | no | Read maps from GRF |
| `enable_spy` | no | Enable @guildspy/@partyspy |

**Save Settings Flags:**
- `1` = After trade
- `2` = After vending
- `4` = After storage
- `8` = After pet hatch/return
- `16` = After mail with attachment
- `32` = After auction
- `64` = After quest change
- `128` = After bank transaction
- `256` = After attendance reward
- `4095` = Always

### Web Server (web_athena.conf)
<!-- chunk: 05-web | keywords: web, api, http -->

| Setting | Default | Description |
|---------|---------|-------------|
| `web_port` | 8888 | HTTP server port |
| `web_ip` | 127.0.0.1 | Bind IP address |

---

## Database Configuration
<!-- chunk: 05-database | keywords: mysql, database, connection -->

### inter_athena.conf
<!-- chunk: 05-inter | keywords: inter, mysql, tables -->

**MySQL Connection Settings:**

| Setting | Default | Description |
|---------|---------|-------------|
| `login_server_ip` | 127.0.0.1 | Login DB host |
| `login_server_port` | 3306 | Login DB port |
| `login_server_id` | ragnarok | Login DB user |
| `login_server_pw` | ragnarok | Login DB password |
| `login_server_db` | ragnarok | Login DB name |
| `char_server_ip` | 127.0.0.1 | Char DB host |
| `char_server_port` | 3306 | Char DB port |
| `char_server_id` | ragnarok | Char DB user |
| `char_server_pw` | ragnarok | Char DB password |
| `char_server_db` | ragnarok | Char DB name |
| `map_server_ip` | 127.0.0.1 | Map DB host |
| `map_server_db` | ragnarok | Map DB name |
| `log_db_ip` | 127.0.0.1 | Log DB host |
| `log_db_db` | ragnarok | Log DB name |

**Table Name Configuration:**

| Setting | Default | Description |
|---------|---------|-------------|
| `char_db` | char | Character table |
| `login_server_account_db` | login | Account table |
| `guild_db` | guild | Guild table |
| `party_db` | party | Party table |
| `pet_db` | pet | Pet table |
| `item_table` | item_db | Item table (pre-re) |
| `renewal-item_table` | item_db_re | Item table (renewal) |
| `mob_table` | mob_db | Monster table (pre-re) |
| `renewal-mob_table` | mob_db_re | Monster table (renewal) |
| `use_sql_db` | no | Use SQL for game data |

**Other Settings:**

| Setting | Default | Description |
|---------|---------|-------------|
| `log_inter` | 1 | Log inter connections |
| `party_share_level` | 15 | Party share level range |
| `start_status_points` | 48 | New char stat points |
| `mysql_reconnect_type` | 2 | 1=limited retry, 2=infinite |

---

## Battle Configuration
<!-- chunk: 05-battle | keywords: battle, combat, balance -->

### Battle Configuration Files (conf/battle/)

| File | Description |
|------|-------------|
| `battle.conf` | Core combat settings |
| `exp.conf` | Experience rates |
| `drops.conf` | Drop rates |
| `skill.conf` | Skill behavior |
| `status.conf` | Status effects |
| `player.conf` | Player settings |
| `monster.conf` | Monster AI/behavior |
| `pet.conf` | Pet settings |
| `homunc.conf` | Homunculus settings |
| `guild.conf` | Guild/WoE settings |
| `party.conf` | Party settings |
| `items.conf` | Item behavior |
| `feature.conf` | Feature toggles |

### Core Battle Settings (battle.conf)
<!-- chunk: 05-battle-core | keywords: damage, attack, defense -->

| Setting | Default | Description |
|---------|---------|-------------|
| `enable_baseatk` | 0x9 | Units with base ATK |
| `enable_critical` | 17 | Units with criticals |
| `mob_critical_rate` | 100 | Monster crit rate % |
| `min_hitrate` | 5 | Minimum hit chance % |
| `max_hitrate` | 100 | Maximum hit chance % |
| `agi_penalty_type` | 1 | Flee penalty type |
| `agi_penalty_count` | 3 | Mobs before penalty |
| `agi_penalty_num` | 10 | Penalty per mob |
| `vit_penalty_type` | 1 | DEF penalty type |
| `vit_penalty_count` | 3 | Mobs before penalty |
| `weapon_defense_type` | 0 | DEF calculation type |
| `delay_battle_damage` | yes | Delay damage application |
| `arrow_decrement` | 1 | Consume ammo |

---

## Experience and Drops
<!-- chunk: 05-exp-drops | keywords: exp, experience, drops, rates -->

### Experience Settings (exp.conf)
<!-- chunk: 05-exp | keywords: exp, level, penalty -->

| Setting | Default | Description |
|---------|---------|-------------|
| `base_exp_rate` | 100 | Base EXP rate % |
| `job_exp_rate` | 100 | Job EXP rate % |
| `mvp_exp_rate` | 100 | MVP EXP rate % |
| `quest_exp_rate` | 100 | Quest EXP rate % |
| `multi_level_up` | no | Allow multi-level |
| `max_exp_gain_rate` | 0 | Max EXP per kill % |
| `death_penalty_type` | 1 | 0=none, 1=current%, 2=total% |
| `death_penalty_base` | 100 | Base EXP penalty (100=1%) |
| `death_penalty_job` | 100 | Job EXP penalty (100=1%) |
| `zeny_penalty` | 0 | Zeny loss on PvP death % |
| `disp_experience` | no | Show EXP gain messages |
| `disp_zeny` | no | Show zeny gain messages |

### Drop Settings (drops.conf)
<!-- chunk: 05-drops | keywords: drops, loot, items -->

| Setting | Default | Description |
|---------|---------|-------------|
| `item_rate_common` | 100 | Common item rate % |
| `item_rate_common_boss` | 100 | Boss common rate % |
| `item_rate_heal` | 100 | Healing item rate % |
| `item_rate_use` | 100 | Usable item rate % |
| `item_rate_equip` | 100 | Equipment rate % |
| `item_rate_card` | 100 | Card rate % |
| `item_rate_mvp` | 100 | MVP reward rate % |
| `item_drop_common_min` | 1 | Min common drop |
| `item_drop_common_max` | 10000 | Max common drop |
| `item_drop_card_min` | 1 | Min card drop |
| `item_drop_card_max` | 10000 | Max card drop |
| `item_auto_get` | no | Auto-loot drops |
| `flooritem_lifetime` | 60000 | Item despawn (ms) |
| `item_first_get_time` | 3000 | First loot grace (ms) |
| `rare_drop_announce` | 0 | Announce threshold |
| `autoloot_adjust` | 0 | Autoloot use bonuses |

### Loot Priority Times

| Setting | Default | Description |
|---------|---------|-------------|
| `item_first_get_time` | 3000 | 1st player grace (ms) |
| `item_second_get_time` | 2000 | 2nd player grace (ms) |
| `item_third_get_time` | 2000 | 3rd player grace (ms) |
| `mvp_item_first_get_time` | 10000 | MVP 1st grace (ms) |
| `mvp_item_second_get_time` | 10000 | MVP 2nd grace (ms) |

---

## Build and Deployment
<!-- chunk: 05-build | keywords: cmake, compile, docker -->

### CMake Build
<!-- chunk: 05-cmake | keywords: cmake, build, compile -->

**Basic Build:**
```bash
mkdir build && cd build
cmake ..
make
make install
```

**Build Options:**

| Option | Default | Description |
|--------|---------|-------------|
| `-DRENEW=ON` | ON | Enable Renewal mode |
| `-DWITH_MYSQL=ON` | ON | Enable MySQL support |
| `-DWITH_PCRE=ON` | ON | Enable PCRE support |
| `-DCMAKE_BUILD_TYPE=` | Release | Debug/Release/RelWithDebInfo |

### Server Startup
<!-- chunk: 05-startup | keywords: start, athena, server -->

**Linux (athena-start script):**
```bash
./athena-start start    # Start all servers
./athena-start stop     # Stop all servers
./athena-start restart  # Restart all servers
./athena-start status   # Check server status
```

**Manual Start:**
```bash
./login-server &
./char-server &
./map-server &
./web-server &
```

### Docker Deployment
<!-- chunk: 05-docker | keywords: docker, container, deployment -->

**Docker Compose (tools/docker/):**
```yaml
version: '3'
services:
  rathena:
    build: .
    ports:
      - "6900:6900"
      - "6121:6121"
      - "5121:5121"
      - "8888:8888"
    depends_on:
      - mysql
  mysql:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: ragnarok
      MYSQL_DATABASE: ragnarok
```

### Configuration Import System
<!-- chunk: 05-import | keywords: import, override, custom -->

All configuration files support importing custom overrides:

```
// At end of config file
import: conf/import/login_conf.txt
```

**Import Directory Structure:**
```
conf/import/
├── battle_conf.txt      # Battle overrides
├── char_conf.txt        # Char server overrides
├── inter_conf.txt       # Database overrides
├── login_conf.txt       # Login server overrides
├── map_conf.txt         # Map server overrides
└── groups.yml           # Permission overrides
```

---

## Player Groups (groups.yml)
<!-- chunk: 05-groups | keywords: groups, permissions, gm -->

### Group Structure

```yaml
Body:
  - Id: 0
    Name: Player
    Level: 0
    Commands:
      changedress: true
      resurrect: true
    Permissions:
      can_trade: true
      can_party: true
      attendance: true

  - Id: 99
    Name: Admin
    Level: 99
    Inherit:
      Support: true
      Law Enforcement: true
    LogCommands: true
    Permissions:
      all_commands: true
      can_trade_bounded: true
```

### Default Groups

| ID | Name | Level | Description |
|----|------|-------|-------------|
| 0 | Player | 0 | Default player |
| 1 | Super Player | 0 | Extended commands |
| 2 | Support | 1 | Helper GM |
| 3 | Script Manager | 1 | NPC management |
| 4 | Event Manager | 1 | Event hosting |
| 5 | VIP | 0 | Premium player |
| 10 | Law Enforcement | 2 | Moderator |
| 99 | Admin | 99 | Full access |

### Key Permissions

| Permission | Description |
|------------|-------------|
| `can_trade` | Allow trading |
| `can_party` | Allow party join |
| `all_commands` | Access all @commands |
| `any_warp` | Warp anywhere |
| `view_equipment` | Inspect players |
| `hack_info` | See hack alerts |
| `who_display_aid` | Show account IDs |
| `channel_admin` | Channel management |

---

## Quick Links

- Architecture: → See [[01_ARCHITECTURE]]
- API Functions: → See [[02_CORE_API]]
- Data Models: → See [[03_DATA_MODELS]]
- Debugging: → See [[06_DEBUG]]
