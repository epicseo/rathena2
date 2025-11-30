# rAthena Server Configuration Reference
## Complete Configuration Guide for All Server Components

---

<!-- RAG_CHUNK: server_architecture_001 -->
## Server Architecture Overview

### Server Components
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  Login Server   │────│  Char Server    │────│   Map Server    │
│   Port: 6900    │    │   Port: 6121    │    │   Port: 5121    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                      │                      │
         └──────────────────────┼──────────────────────┘
                                │
                        ┌───────────────┐
                        │   Database    │
                        │  (MySQL/MariaDB)│
                        └───────────────┘
                                │
                        ┌───────────────┐
                        │  Web Server   │
                        │  Port: 8888   │
                        └───────────────┘
```

### Configuration Directory Structure
```
conf/
├── login_athena.conf      # Login server settings
├── char_athena.conf       # Character server settings
├── map_athena.conf        # Map server settings
├── inter_athena.conf      # Inter-server communication
├── atcommand_athena.conf  # @command settings
├── groups.conf            # GM group permissions
├── channels.conf          # Chat channel settings
├── import/                # Override configurations
│   ├── login_conf.txt
│   ├── char_conf.txt
│   ├── map_conf.txt
│   └── inter_conf.txt
└── battle/                # Gameplay configuration
    ├── battle.conf        # Master battle config
    ├── client.conf        # Client settings
    ├── drops.conf         # Drop rates
    ├── exp.conf           # Experience rates
    ├── guild.conf         # Guild settings
    ├── monster.conf       # Monster behavior
    ├── party.conf         # Party settings
    ├── pet.conf           # Pet settings
    ├── player.conf        # Player settings
    ├── skill.conf         # Skill settings
    └── status.conf        # Status effect settings
```

---

<!-- RAG_CHUNK: login_server_config_001 -->
## Login Server Configuration (login_athena.conf)

### Basic Settings
```conf
// Login Server IP and Port
login_ip: 127.0.0.1
login_port: 6900

// Connection Settings
new_account: yes              // Allow account creation (yes/no)
new_acc_length_limit: yes     // Enforce 4-23 char limit
start_limited_time: -1        // Days until account expires (-1=unlimited)

// Password Settings
use_MD5_passwords: no         // Use MD5 hashed passwords
case_sensitive: yes           // Case-sensitive usernames

// Logging
log_login: yes                // Log login attempts
date_format: %Y-%m-%d %H:%M:%S
```

### Connection Limits
```conf
// IP-based restrictions
allowed_regs: 1               // Registrations per time unit
time_allowed: 10              // Time unit in seconds

// Concurrent connections
group_id_to_connect: -1       // Required group ID (-1=any)
min_group_id_to_connect: -1   // Minimum group ID

// DDOS Protection
use_dnsbl: no                 // Use DNS blacklist
dnsbl_servers: bl.blocklist.de
```

### Character Slot Settings
```conf
// Slots configuration
chars_per_account: 9          // Max characters per account
char_del_level: 0             // Max level for instant deletion
char_del_delay: 86400         // Delete delay in seconds
```

---

<!-- RAG_CHUNK: char_server_config_001 -->
## Character Server Configuration (char_athena.conf)

### Server Identity
```conf
// Server identification
userid: s1                    // Account for char server
passwd: p1                    // Password for char server
server_name: rAthena          // Server name shown to clients

// Network Settings
char_ip: 127.0.0.1
char_port: 6121
login_ip: 127.0.0.1
login_port: 6900
```

### Character Settings
```conf
// Starting location
start_point: iz_int,97,90     // Default: Izlude
start_point_pre: new_1-1,53,111  // Pre-renewal start
start_point_doram: lasa_fild01,48,297  // Doram start

// Starting items (itemid,amount,location,identify)
start_items: 1201,1,0,0:2301,1,0,0
// Sword, Cotton Shirt (unidentified, not equipped)

// Starting Zeny
start_zeny: 0
```

### Guild & Party Settings
```conf
// Guild limits
guild_exp_rate: 100           // Guild EXP rate (%)
max_guild_alliance: 3         // Max guild alliances

// Party share level range
party_share_level: 15         // Level difference for EXP share
```

### Character Restrictions
```conf
// Name restrictions
char_name_letters: abcdefghijklmnopqrstuvwxyz...
char_name_option: 1           // 0=letters, 1=unicode
unknown_char_name: Unknown    // Name for deleted chars

// Appearance limits
min_hair_style: 0
max_hair_style: 29
min_hair_color: 0
max_hair_color: 8
min_cloth_color: 0
max_cloth_color: 4
```

### Fame & Ranking
```conf
// Blacksmith/Alchemist rankings
fame_list_alchemist: 10       // Top X in fame list
fame_list_blacksmith: 10
fame_list_taekwon: 10
```

---

<!-- RAG_CHUNK: map_server_config_001 -->
## Map Server Configuration (map_athena.conf)

### Server Identity
```conf
// Server identification
userid: s1
passwd: p1

// Network Settings
map_ip: 127.0.0.1
map_port: 5121
char_ip: 127.0.0.1
char_port: 6121
```

### Map Loading
```conf
// Map configuration file
map_configuration: conf/map_athena.conf

// NPC script loading
npc: npc/scripts_main.conf    // Main NPC list
npc: npc/scripts_custom.conf  // Custom NPCs
```

### Console Settings
```conf
// Console commands
console: off                  // Enable console input
console_silent: 0             // 0=all, 1=info+, 2=notice+
console_msg_log: 0            // Log messages to file

// Auto-restart
autosave_time: 300            // Auto-save interval (seconds)
minsave_time: 100             // Minimum save interval
```

### SQL Settings
```conf
// Database logging
log_chat: yes                 // Log chat messages
log_mvpdrop: yes              // Log MVP drops
log_npc: yes                  // Log NPC transactions
```

---

<!-- RAG_CHUNK: inter_server_config_001 -->
## Inter-Server Configuration (inter_athena.conf)

### Database Connection
```conf
// MySQL/MariaDB Settings
sql.db_hostname: 127.0.0.1
sql.db_port: 3306
sql.db_username: ragnarok
sql.db_password: ragnarok
sql.db_database: ragnarok

// Connection pool
sql.db_pool_size: 10          // Connection pool size
sql.db_pool_growth: 10        // Pool growth increment
```

### Table Names
```conf
// Main tables
login_server_db: login
ipbanlist_db: ipbanlist
char_db: char
hotkey_db: hotkey
scdata_db: sc_data
cart_db: cart_inventory
inventory_db: inventory
charlog_db: charlog
skill_db: skill
interlog_db: interlog
memo_db: memo
guild_db: guild
guild_alliance_db: guild_alliance
guild_castle_db: guild_castle
guild_expulsion_db: guild_expulsion
guild_member_db: guild_member
guild_position_db: guild_position
guild_skill_db: guild_skill
guild_storage_db: guild_storage
party_db: party
pet_db: pet
friend_db: friends
mail_db: mail
auction_db: auction
quest_db: quest
homunculus_db: homunculus
skill_homunculus_db: skill_homunculus
mercenary_db: mercenary
mercenary_owner_db: mercenary_owner
elemental_db: elemental
ragsrvinfo_db: ragsrvinfo
skillcooldown_db: skillcooldown
bonus_script_db: bonus_script
acc_reg_num_db: acc_reg_num_db
acc_reg_str_db: acc_reg_str_db
char_reg_num_db: char_reg_num_db
char_reg_str_db: char_reg_str_db
global_acc_reg_num_db: global_acc_reg_num_db
global_acc_reg_str_db: global_acc_reg_str_db
```

### Web Interface
```conf
// Web server settings
web_server_ip: 127.0.0.1
web_server_port: 8888
```

---

<!-- RAG_CHUNK: battle_config_001 -->
## Battle Configuration (conf/battle/)

### Experience Rates (exp.conf)
```conf
// Base experience rates
base_exp_rate: 100            // Base EXP (100 = 1x)
job_exp_rate: 100             // Job EXP
quest_exp_rate: 100           // Quest EXP

// MVP experience
mvp_exp_rate: 100             // MVP EXP rate

// Special bonuses
multi_level_up: no            // Allow multiple level ups
max_exp_gain_rate: 0          // Max % of level per kill (0=off)
death_penalty_type: 1         // 0=exp, 1=exp+drop, 2=drop
death_penalty_base: 100       // Base EXP loss on death
death_penalty_job: 100        // Job EXP loss on death
```

### Drop Rates (drops.conf)
```conf
// Item drop rates (100 = 1x)
item_rate_common: 100         // Normal items
item_rate_common_boss: 100    // Boss normal items
item_rate_heal: 100           // Healing items
item_rate_heal_boss: 100      // Boss healing items
item_rate_use: 100            // Usable items
item_rate_use_boss: 100       // Boss usable items
item_rate_equip: 100          // Equipment
item_rate_equip_boss: 100     // Boss equipment
item_rate_card: 100           // Cards
item_rate_card_boss: 100      // Boss cards
item_rate_mvpitem: 100        // MVP items
item_rate_adddrop: 100        // Script drops
item_rate_treasure: 100       // Treasure box items

// Drop modifiers
drops_by_luk: 0               // Luck bonus to drops
drops_by_luk2: 0              // Additional luck bonus
item_drop_common_min: 1       // Minimum common drop rate
item_drop_common_max: 10000   // Maximum common drop rate (100%)
item_drop_equip_min: 1        // Minimum equip drop rate
item_drop_equip_max: 10000    // Maximum equip drop rate
item_drop_card_min: 1         // Minimum card drop rate
item_drop_card_max: 10000     // Maximum card drop rate
item_drop_mvp_min: 1          // Minimum MVP drop rate
item_drop_mvp_max: 10000      // Maximum MVP drop rate
```

### Player Settings (player.conf)
```conf
// Basic stats
max_lv: 175                   // Maximum base level
max_lv_job: 60                // Maximum job level (3rd class)
aura_lv: 99                   // Level for aura effect
max_hp: 1000000               // Maximum HP
max_sp: 32767                 // Maximum SP
max_cart_weight: 8000         // Maximum cart weight
max_parameter: 99             // Maximum stat (STR,AGI,etc)
max_third_parameter: 130      // Max stat for 3rd class
max_extended_parameter: 125   // Max stat for extended class
max_baby_parameter: 80        // Max stat for baby class

// Starting values
start_status_points: 48       // Status points at level 1
start_skill_points: 0         // Skill points at job 1

// Stat calculation
natural_healhp_interval: 6000 // HP regen interval (ms)
natural_healsp_interval: 8000 // SP regen interval (ms)
natural_heal_weight_rate: 50  // Regen rate when overweight
```

### Monster Settings (monster.conf)
```conf
// Monster behavior
mob_count_rate: 100           // Monster spawn rate
mob_spawn_delay: 100          // Spawn delay modifier
no_spawn_on_player: 0         // Don't spawn on player cells
boss_spawn_delay: 100         // Boss respawn delay modifier

// Monster stats
mob_hp_rate: 100              // Monster HP modifier
mob_max_aspd: 199             // Monster max ASPD

// Aggressive behavior
monster_active_enable: yes    // Monsters can be aggressive
mob_remove_damaged: yes       // Remove damaged mobs on spawn
mob_remove_delay: 300000      // Delay before removal (ms)

// Drop behavior
monster_drops_on_map: yes     // Drop items on ground
alchemist_summon_reward: 0    // Alchemist summon drop rate
mob_show_info: 0              // Show mob info on hover
```

### Skill Settings (skill.conf)
```conf
// Casting settings
casting_rate: 100             // Cast time modifier
delay_rate: 100               // After-cast delay modifier
castrate_dex_scale: 150       // DEX effect on cast time

// Skill ranges
skill_add_range: 0            // Additional skill range
skill_out_range_consume: yes  // Consume requirements on miss

// Area of Effect
area_size: 14                 // AoE detection range
skill_amotion_leniency: 90    // Animation delay leniency

// Safety settings
skill_caster_check: yes       // Check caster validity
skillrange_by_distance: yes   // Use distance for range check
skill_trap_type: 0            // 0=normal, 1=bypass protection
```

### Status Effects (status.conf)
```conf
// Potion settings
potion_hp_rate: 100           // Potion HP recovery rate
potion_sp_rate: 100           // Potion SP recovery rate

// Status durations
status_cast_cancel: no        // Cancel cast on status effect
display_status_timers: yes    // Show status timers
debuff_on_logout: 0           // Clear debuffs on logout
```

### Party Settings (party.conf)
```conf
// Party limits
party_hp_mode: 0              // HP bar display mode
party_show_share_picker: yes  // Show item picker
party_share_type: 0           // EXP share type

// Item sharing
party_item_share_type: 0      // Item share method
show_party_share_picker: yes  // Display share picker
```

### Guild Settings (guild.conf)
```conf
// Guild limits
guild_max_members: 16         // Base guild size
guild_skill_relog_delay: 300  // Skill cooldown on relog

// War of Emperium
woe_exp_rate: 100             // WoE EXP modifier
gvg_flee_penalty: 20          // Flee penalty in GvG
guild_emperium_check: yes     // Check Emperium ownership
```

### Pet Settings (pet.conf)
```conf
// Pet behavior
pet_catch_rate: 100           // Catch rate modifier
pet_rename: no                // Allow rename
pet_friendly_rate: 100        // Intimacy gain rate
pet_hungry_delay_rate: 100    // Hunger rate
pet_hungry_friendly_decrease: 5  // Intimacy loss on hunger
pet_status_support: no        // Pet stat bonuses
pet_attack_support: no        // Pet attacking
pet_damage_support: no        // Pet taking damage
```

### Client Settings (client.conf)
```conf
// Appearance limits
min_hair_style: 0
max_hair_style: 29
min_hair_color: 0
max_hair_color: 8
min_cloth_color: 0
max_cloth_color: 4
min_body_style: 0
max_body_style: 1
save_body_style: no           // Save body style on logout

// Display settings
save_clothcolor: yes          // Save cloth color
undead_detect_type: 0         // Undead detection method
```

---

<!-- RAG_CHUNK: groups_config_001 -->
## GM Groups Configuration (groups.conf)

### Group Structure
```conf
groups: (
{
    id: 0                     // Group ID
    name: "Player"            // Group name
    level: 0                  // Access level
    inherit: ( )              // Inherited groups
    commands: {               // Allowed commands
        // Command: true/false
        rates: true
        uptime: true
        showexp: true
    }
    permissions: {            // Special permissions
        can_trade: true
        can_party: true
    }
},
{
    id: 99
    name: "Admin"
    level: 99
    inherit: ( "Super Player" )
    commands: {
        // All commands allowed
        reloadscript: true
        kick: true
        ban: true
    }
    permissions: {
        all_skill: true
        all_equipment: true
        all_commands: true
    }
}
)
```

### Permission Types
```conf
permissions: {
    // Trading
    can_trade: true           // Can trade with players
    can_trade_bound: false    // Can trade bound items

    // Commands
    all_commands: true        // Access all commands
    receive_requests: true    // Receive @request messages

    // Bypass restrictions
    all_skill: true           // Use any skill
    all_equipment: true       // Equip any item
    skill_unconditional: true // No skill requirements
    join_chat: true           // Join any chat room
    kick_chat: true           // Kick from chat rooms

    // Administrative
    hide_session: true        // Hidden from @who
    bypass_stat_onclone: true // Clone without stat check
    bypass_max_stat: true     // Exceed stat limits

    // Security
    disable_pvm: false        // Cannot attack monsters
    disable_pvp: false        // Cannot attack players
}
```

---

<!-- RAG_CHUNK: channels_config_001 -->
## Channel Configuration (channels.conf)

### Channel Settings
```conf
chsys: {
    // Global settings
    ally_channel_enabled: true    // Enable ally channel
    local_channel_enabled: true   // Enable local channel
    irc_channel_enabled: false    // Enable IRC bridge

    // Channel limits
    local_channel_color: 0xFFFF00 // Local channel color (hex)
    ally_channel_color: 0x00FF00  // Ally channel color

    // User channels
    allow_user_channel_creation: true
    max_user_channels: 5          // Max channels per user

    // Default channels
    channels: (
    {
        name: "#main"             // Channel name
        color: 0xFFFFFF           // Text color
        options: {
            JoinAnnounce: false   // Announce joins
            MessageDelay: 0       // Message cooldown
            ColorOverride: true   // Allow user colors
            CanLeave: true        // Allow leaving
            AutoJoin: false       // Auto-join on login
        }
        groupid_range: [0, 99]    // Access range
    },
    {
        name: "#trade"
        color: 0x00FF00
        options: {
            MessageDelay: 10      // 10 second cooldown
            AutoJoin: true
        }
    },
    {
        name: "#support"
        color: 0xFF0000
        options: {
            AutoJoin: false
        }
        groupid_range: [1, 99]    // GM only
    }
    )
}
```

---

<!-- RAG_CHUNK: import_config_001 -->
## Import Configuration System

### Purpose
Import files override default configuration without modifying original files.
Located in `conf/import/`

### Usage
```conf
// In conf/import/map_conf.txt
map_ip: 192.168.1.100
map_port: 5121

// In conf/import/battle_conf.txt
base_exp_rate: 500
job_exp_rate: 500
item_rate_common: 300
```

### Load Order
1. Default configuration loaded
2. Import files override defaults
3. Changes persist across updates

### Import Files
```
conf/import/
├── battle_conf.txt     # Battle overrides
├── char_conf.txt       # Char server overrides
├── inter_conf.txt      # Inter-server overrides
├── login_conf.txt      # Login server overrides
├── map_conf.txt        # Map server overrides
├── msg_conf.txt        # Message overrides
└── packet_conf.txt     # Packet overrides
```

---

<!-- RAG_CHUNK: common_rate_examples_001 -->
## Common Configuration Examples

### Low Rate Server (1x/1x/1x)
```conf
// conf/import/battle_conf.txt
base_exp_rate: 100
job_exp_rate: 100
item_rate_common: 100
item_rate_equip: 100
item_rate_card: 100
```

### Mid Rate Server (10x/10x/5x)
```conf
base_exp_rate: 1000
job_exp_rate: 1000
item_rate_common: 500
item_rate_equip: 500
item_rate_card: 300
```

### High Rate Server (1000x/1000x/100x)
```conf
base_exp_rate: 100000
job_exp_rate: 100000
item_rate_common: 10000
item_rate_equip: 10000
item_rate_card: 5000
max_lv: 255
max_lv_job: 120
max_parameter: 255
```

### Super High Rate (99999x)
```conf
base_exp_rate: 9999900
job_exp_rate: 9999900
item_rate_common: 10000
item_rate_equip: 10000
item_rate_card: 10000
instant_cast_stat: 0
```

### Pre-Renewal Mode
```conf
// conf/map_athena.conf
renewal: no

// Different exp table used automatically
// Different formulas apply
```

---

#rathena #config #configuration #server #setup #rates #admin #reference
