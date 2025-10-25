---
kb_id: KB_REF_009
kb_type: reference
kb_category: server_configuration
kb_subcategory: battle_mechanics
kb_keywords: [battle config, server rates, exp rate, drop rate, game mechanics, balance, server customization, conf/battle, rates, gameplay]
kb_related: [KB_REF_004, KB_CONF_001]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2025-10-23
kb_use_case: [server_setup, balance, customization, rates_adjustment]
---

# rAthena Battle Configuration Reference

Essential battle configuration settings for customizing server mechanics and rates.

## Overview

Battle configuration files control game mechanics, rates, and behavior. These settings are in `/conf/battle/` directory and can be overridden in `/conf/import/battle_conf.txt`.

**Configuration Location:**
- Main files: `/conf/battle/*.conf`
- Custom overrides: `/conf/import/battle_conf.txt` ✓ (recommended)

**How to Apply:**
1. Edit `/conf/import/battle_conf.txt`
2. Restart map server (or use `@reloadbattleconf`)

---

## TABLE OF CONTENTS

1. [Experience & Leveling](#1-experience--leveling)
2. [Drop Rates](#2-drop-rates)
3. [Player Mechanics](#3-player-mechanics)
4. [Monster Mechanics](#4-monster-mechanics)
5. [Party & Guild](#5-party--guild)
6. [PvP & WoE](#6-pvp--woe)
7. [Items & Equipment](#7-items--equipment)
8. [Skills](#8-skills)
9. [Death Penalties](#9-death-penalties)
10. [Misc Settings](#10-misc-settings)

---

## 1. EXPERIENCE & LEVELING

### exp.conf

```conf
// Base experience rate (100 = 1x, 1000 = 10x, 10000 = 100x)
base_exp_rate: 100

// Job experience rate
job_exp_rate: 100

// MVP experience rate
mvp_exp_rate: 100

// Quest experience rate
quest_exp_rate: 100

// Max base level
max_base_level: 99
max_base_level_1_2: 99
max_base_level_3: 175
max_base_level_4: 200

// Max job level
max_job_level: 50
max_job_level_1_2: 50
max_job_level_3: 70
max_job_level_4: 60

// Death penalty
death_penalty_type: 1
death_penalty_base: 100
death_penalty_job: 100

// Resurrection penalty
resurrection_exp: 0

// Zeny penalty on death (100 = 1%)
zeny_penalty: 0
```

**Common Rates:**
- 1x: base_exp_rate: 100
- 5x: base_exp_rate: 500
- 10x: base_exp_rate: 1000
- 50x: base_exp_rate: 5000
- 100x: base_exp_rate: 10000

**Example Override:**
```conf
// 10x rates server
base_exp_rate: 1000
job_exp_rate: 1000
mvp_exp_rate: 1000
```

---

## 2. DROP RATES

### drops.conf

```conf
// Item drop rates (100 = 1x, 200 = 2x)
item_rate_common: 100          // Common items
item_rate_common_boss: 100     // Common from boss
item_rate_heal: 100            // Healing items
item_rate_heal_boss: 100       // Healing from boss
item_rate_use: 100             // Usable items
item_rate_use_boss: 100        // Usable from boss
item_rate_equip: 100           // Equipment
item_rate_equip_boss: 100      // Equipment from boss
item_rate_card: 100            // Cards
item_rate_card_boss: 100       // Cards from boss

// MVP item rates
item_rate_mvp: 100

// Treasure box rates
item_rate_treasure: 100

// Drop rate affected by level difference (Renewal)
// yes = enabled, no = disabled
drops_by_luk: 0

// Minimum drop rate (100 = 1%)
drops_by_luk2: 0
```

**Common Configurations:**
```conf
// 5x drop rates
item_rate_common: 500
item_rate_heal: 500
item_rate_use: 500
item_rate_equip: 500
item_rate_card: 100  // Keep cards rare

// Double boss drops
item_rate_common_boss: 200
item_rate_equip_boss: 200
item_rate_card_boss: 200
```

---

## 3. PLAYER MECHANICS

### player.conf

```conf
// HP/SP modifiers
hp_rate: 100
sp_rate: 100

// Max stats
max_parameter: 99               // Max stat (STR/AGI/VIT/INT/DEX/LUK)
max_baby_parameter: 80          // Max stat for baby classes
max_third_parameter: 130        // Max stat for 3rd jobs
max_fourth_parameter: 130       // Max stat for 4th jobs

// ASPD
max_aspd: 190
max_third_aspd: 193
max_fourth_aspd: 193

// Walk speed
default_walk_speed: 150
max_walk_speed: 100             // Lower = faster

// Weight
max_weight_base: 20000
max_cart_weight: 8000

// Skill points
skillup_limit: 0                // 0=no limit
```

**Common Changes:**
```conf
// High-rate server
max_parameter: 120
max_aspd: 196
hp_rate: 150
sp_rate: 150
```

---

## 4. MONSTER MECHANICS

### monster.conf

```conf
// Monster HP/damage rates
mob_count_rate: 100             // Spawn count
mob_hp_rate: 100                // HP multiplier
mob_max_casttime: 10000         // Max cast time (ms)

// MVP settings
mvp_tomb_enabled: yes           // Show MVP tombstone
mvp_exp_bonus_max_rate: 200    // Max MVP exp bonus
override_mob_names: no          // Use custom mob names

// Monster behavior
monster_active_enable: yes      // Aggressive monsters
mob_skill_rate: 100             // Skill usage rate
mob_skill_delay: 100            // Skill delay
mob_damage_delay: 100           // Damage display delay

// Monster info display
show_mob_info: 0                // 0=none, 1=name, 2=HP, 3=both
monster_hp_bars_info: yes       // Show HP bar
```

**Boss Enhancement:**
```conf
// Harder MVPs
mob_hp_rate: 150
mvp_exp_bonus_max_rate: 300
```

---

## 5. PARTY & GUILD

### party.conf

```conf
// Party exp sharing
party_even_share_bonus: 0       // Bonus exp % for even share
party_item_share_type: 0        // 0=each, 1=shared
party_hp_mode: 0                // 0=off, 1=show to party
display_party_name: no          // Show party name above player

// Party creation
party_update_interval: 1000     // HP update interval (ms)
```

### guild.conf

```conf
// Guild settings
guild_max_castles: 0            // Max castles per guild (0=unlimited)
guild_skill_relog_delay: 300000 // Guild skill delay after login
guild_exp_limit: 50             // Max guild level

// Guild storage
guild_storage_log: no           // Log guild storage
```

**Common Changes:**
```conf
// Show party HP
party_hp_mode: 1
display_party_name: yes

// Higher guild level
guild_exp_limit: 99
```

---

## 6. PVP & WOE

### battle.conf & gvg.conf

```conf
// PvP settings
pk_mode: 0                      // 0=off, 1=on, 2=nightwatch
pk_level_range: 0               // Level range for PvP (0=any)

// Damage adjustments
pk_short_attack_damage_rate: 100
pk_long_attack_damage_rate: 100
pk_magic_attack_damage_rate: 100
pk_misc_attack_damage_rate: 100

// WoE settings
castle_defense_rate: 100
gvg_short_attack_damage_rate: 80
gvg_long_attack_damage_rate: 80
gvg_magic_attack_damage_rate: 60
gvg_misc_attack_damage_rate: 80
gvg_flee_penalty: 20

// Guild vs Guild
gvg_eliminate_time: 7000        // Respawn time in GvG (ms)
```

**Balanced PvP:**
```conf
// Reduce burst damage
pk_short_attack_damage_rate: 80
pk_long_attack_damage_rate: 80
pk_magic_attack_damage_rate: 70
```

**Harder WoE:**
```conf
// Increase castle defense
castle_defense_rate: 150
gvg_flee_penalty: 30
```

---

## 7. ITEMS & EQUIPMENT

### items.conf

```conf
// Item settings
item_auto_get: no               // Auto-loot own drops
item_first_get_time: 3000       // First looter time (ms)
item_check_equip_weight: no     // Check weight when equipping
item_zeny_from_mobs: yes        // Monsters drop zeny

// Equipment breaking
equipment_breaking: no          // Can equipment break?
equipment_break_rate: 100       // Break rate

// Item usage
item_use_interval: 0            // Delay between item use (ms)
cashfood_use_box: no            // Cash food from boxes

// Vending
vending_over_max: yes           // Allow vending over max price
vending_tax: 200                // Tax on vending (200 = 2%)
vending_max_value: 1000000000   // Max price per item

// Production
weapon_produce_rate: 100        // Weapon craft success rate
potion_produce_rate: 100        // Potion craft success rate
```

**Common Changes:**
```conf
// Casual server
item_auto_get: yes
equipment_breaking: no

// Higher craft rates
weapon_produce_rate: 150
potion_produce_rate: 150
```

---

## 8. SKILLS

### skill.conf

```conf
// Skill settings
skill_delay_attack_enable: yes  // Can't attack while casting
castrate_dex_scale: 150         // DEX affect on cast time
vcast_stat_scale: 530           // Stat affect on variable cast

// Skill damage
skill_min_damage: 6             // Minimum skill damage

// Skill cool downs
skill_add_heal_rate: 7          // Heal bonus per VIT/INT

// Restrictions
gm_all_skill: no                // GMs get all skills
player_skill_partner_check: yes // Check partner for couple skills

// Casting
casting_rate: 100               // Cast time rate
delay_rate: 100                 // Delay rate
skill_delay_attack_enable: yes  // Delay attack during cast
```

**Instant Cast Server:**
```conf
// No cast time
casting_rate: 0
delay_rate: 50
```

---

## 9. DEATH PENALTIES

### exp.conf

```conf
// Death penalties
death_penalty_type: 1           // 0=none, 1=exp loss, 2=drop
death_penalty_base: 100         // Base exp loss (100 = 1%)
death_penalty_job: 100          // Job exp loss (100 = 1%)
zeny_penalty: 0                 // Zeny loss (100 = 1%)

// Resurrection exp loss
resurrection_exp: 0             // Exp loss on ress (0-100)

// PvP death penalty
death_penalty_maxlv: 0          // 0=always, 1=only below max level

// Exp from PvP
pk_exp: no                      // Gain exp from PvP kills
```

**No Penalty Server:**
```conf
death_penalty_type: 0
death_penalty_base: 0
death_penalty_job: 0
zeny_penalty: 0
```

**Hardcore Server:**
```conf
death_penalty_type: 1
death_penalty_base: 500         // 5% loss
death_penalty_job: 500
zeny_penalty: 200               // 2% zeny loss
```

---

## 10. MISC SETTINGS

### misc.conf

```conf
// Timers
day_duration: 7200000           // Day length (ms)
night_duration: 1800000         // Night length (ms)

// Chat
global_chat: yes                // Enable global chat
show_steal_in_same_party: no    // Show steal to party
map_local_channel_autojoin: no  // Auto-join map channel

// Commands
atcommand_spawn_quantity_limit: 100
atcommand_slave_clone_limit: 25
partial_name_scan: yes          // Search by partial name

// Display
display_status_timers: yes      // Show buff timers
display_hallucination: yes      // Hallucination effect
display_delay_skill_fail: yes   // Show skill fail message

// Autotrade
at_mapflag: no                  // Autotrade needs mapflag
at_timeout: 0                   // Autotrade timeout (minutes, 0=no limit)

// Mail
mail_show_status: 0             // 0=no, 1=yes, 2=if unread

// Banking
feature_banking: yes            // Enable banking system
```

**Common Changes:**
```conf
// 24/7 daylight
day_duration: 0
night_duration: 0

// Better QoL
display_status_timers: yes
mail_show_status: 2
at_mapflag: no
```

---

## CONFIGURATION TEMPLATE

### Recommended `/conf/import/battle_conf.txt`

```conf
//=============================================================
// EXPERIENCE RATES
//=============================================================
base_exp_rate: 1000             // 10x
job_exp_rate: 1000              // 10x
mvp_exp_rate: 1000              // 10x
quest_exp_rate: 1000            // 10x

//=============================================================
// DROP RATES
//=============================================================
item_rate_common: 200           // 2x
item_rate_heal: 200             // 2x
item_rate_use: 200              // 2x
item_rate_equip: 200            // 2x
item_rate_card: 100             // 1x (keep cards rare)

//=============================================================
// PLAYER SETTINGS
//=============================================================
max_parameter: 120
max_aspd: 196
hp_rate: 150
sp_rate: 150

//=============================================================
// DEATH PENALTY
//=============================================================
death_penalty_type: 0           // No penalty
death_penalty_base: 0
death_penalty_job: 0
zeny_penalty: 0

//=============================================================
// QUALITY OF LIFE
//=============================================================
item_auto_get: no
equipment_breaking: no
day_duration: 0
night_duration: 0
display_status_timers: yes
mail_show_status: 2

//=============================================================
// PARTY & GUILD
//=============================================================
party_hp_mode: 1
display_party_name: yes
guild_exp_limit: 99

//=============================================================
// SKILLS
//=============================================================
skill_delay_attack_enable: yes
castrate_dex_scale: 150

//=============================================================
// PRODUCTION
//=============================================================
weapon_produce_rate: 150
potion_produce_rate: 150
```

---

## RATE PRESETS

### Low Rate (Official-like)
```conf
base_exp_rate: 100
job_exp_rate: 100
item_rate_common: 100
item_rate_card: 100
death_penalty_type: 1
death_penalty_base: 100
```

### Mid Rate (5x)
```conf
base_exp_rate: 500
job_exp_rate: 500
item_rate_common: 200
item_rate_card: 100
death_penalty_type: 1
death_penalty_base: 50
```

### High Rate (10-50x)
```conf
base_exp_rate: 1000             // 10x
job_exp_rate: 1000
item_rate_common: 300
item_rate_card: 150
death_penalty_type: 0
```

### Super High Rate (100x+)
```conf
base_exp_rate: 10000            // 100x
job_exp_rate: 10000
item_rate_common: 1000          // 10x
item_rate_card: 500             // 5x
max_parameter: 150
death_penalty_type: 0
```

---

## APPLYING CHANGES

### Method 1: Restart Server (Recommended)
```bash
./map-server
```

### Method 2: Reload Config (In-Game)
```
@reloadbattleconf
```

**Note:** Some settings require full restart to take effect.

---

## TESTING RATES

```
// Check current rates
@rates

// Check your stats
@stats

// Test exp gain
@blvl 1          // Level up
@jlvl 1          // Job level up

// Test drops
@monster PORING 1
// Kill and check drops
```

---

## TIPS & BEST PRACTICES

1. **Start conservative** - Can always increase rates later
2. **Test thoroughly** - Changes affect game balance significantly
3. **Document changes** - Comment your battle_conf.txt
4. **Backup original** - Keep defaults for reference
5. **Consider players** - What experience do they want?
6. **Balance PvP** - Lower damage rates for better PvP
7. **Adjust together** - Exp and drops should match server style
8. **Monitor feedback** - Players will tell you if rates are wrong

---

## COMMON ISSUES

### Too Fast Leveling
```conf
// Reduce exp rates
base_exp_rate: 500  // Lower from 1000
```

### Economy Inflation
```conf
// Reduce drop rates
item_rate_common: 150  // Lower from 300
// Enable zeny sinks
vending_tax: 500       // 5% tax
```

### PvP Too Bursty
```conf
// Reduce damage
pk_short_attack_damage_rate: 70
pk_magic_attack_damage_rate: 60
```

---

## SEE ALSO

- **Configuration Files:** `/conf/battle/*.conf`
- **KB_REF_004:** Configuration System Guide
- **KB_CONF_001:** Server Configuration Overview

---

*Last Updated: 2025-10-23*
*rAthena Documentation - Battle Configuration*
---
kb_id: KB_REF_004
kb_type: reference
kb_category: server_configuration
kb_subcategory: import_system
kb_keywords: [configuration, import, override, conf, database, customization, import directory, server config, battle config, db override, git conflicts, update-safe]
kb_related: [KB_CONF_001, KB_DB_001]
kb_difficulty: basic
kb_version: rAthena_2025
kb_last_updated: 2025-10-23
kb_use_case: [server_setup, customization, maintenance, version_updates]
---

# rAthena Configuration & Database Import System

Complete guide to the import directory system for configuration and database customization.

## Overview

The **import directory** system allows you to customize your rAthena server WITHOUT modifying core files. This prevents merge conflicts during updates and keeps your customizations separate from base files.

**Core Concept:** Think of "import" as "override"

**Benefits:**
✅ Update-safe - No merge conflicts when updating rAthena
✅ Clean separation - Your changes vs. official code
✅ Easy backup - Just backup `/conf/import/` and `/db/import/`
✅ Maintainable - See exactly what you've customized
✅ Reversible - Delete import files to restore defaults

---

## HOW IT WORKS

### Directory Structure

```
rathena/
├── conf/                      # Core configuration files (DON'T EDIT)
│   ├── battle/
│   ├── import/                # YOUR customizations go here ✓
│   └── import-tmpl/           # Examples/templates
├── db/                        # Core database files (DON'T EDIT)
│   ├── (pre-)re/
│   ├── import/                # YOUR customizations go here ✓
│   └── import-tmpl/           # Examples/templates
└── npc/
    ├── scripts.conf
    └── custom/                # YOUR custom NPCs go here ✓
```

### Loading Order

1. **Core files** load first (e.g., `/conf/char_athena.conf`)
2. **Import files** load second (e.g., `/conf/import/char_conf.txt`)
3. Import files **override** core file settings

**Example:**
```
/conf/char_athena.conf:        server_name: rAthena
/conf/import/char_conf.txt:    server_name: MyServer

Result: server_name = "MyServer"
```

---

## CONFIGURATION FILES (`/conf/import/`)

### General Rules

1. **Only include settings you want to override**
2. **Use exact same setting names** as core files
3. **Comments are optional** but recommended for documentation
4. **One file per server** (login_conf.txt, char_conf.txt, map_conf.txt, etc.)

---

### Login Server Configuration

**File:** `/conf/import/login_conf.txt`

**Example:** Use MD5 passwords and disable account creation

```conf
// Disable _m/f account creation
new_account: no

// Use MD5 password hashing
use_MD5_passwords: yes

// Server port (if different from default)
login_port: 6900
```

**Common Settings:**
- `new_account` - Allow new account creation
- `use_MD5_passwords` - Password hashing method
- `login_port` - Server port
- `min_level_to_connect` - Minimum level requirement
- `check_client_version` - Client version enforcement

---

### Character Server Configuration

**File:** `/conf/import/char_conf.txt`

**Example:** Change server name and settings

```conf
// Server name shown in character selection
server_name: Odin

// Allow character deletion
char_del_option: 1

// Starting zeny amount
start_zeny: 10000

// Max characters per account
max_char_num: 9
```

**Common Settings:**
- `server_name` - Server display name
- `char_del_option` - Deletion options (0=block, 1=email, 2=birthdate)
- `start_zeny` - Starting money
- `start_point` - Starting location (map,x,y)
- `max_char_num` - Characters per account limit

---

### Map Server Configuration

**File:** `/conf/import/map_conf.txt`

**Example:** Hide errors and add custom maps

```conf
// Hide error messages (16 = hide Error and SQL Error)
console_silent: 16

// Add custom maps
map: 1@toy
map: 1@valley
map: shops
map: custom_pvp
map: custom_woe

// Server MOTD
motd_txt: conf/import/motd.txt

// Help message file
help_txt: conf/import/help.txt
```

**Common Settings:**
- `console_silent` - Output filtering
- `map` - Load additional maps
- `motd_txt` - Message of the day file
- `help_txt` - Help text file
- `autosave_time` - Auto-save interval
- `map_cache_file` - Map cache path

---

### Inter Server Configuration

**File:** `/conf/import/inter_conf.txt`

**Example:** Use SQL instead of TXT databases

```conf
// Use SQL database (recommended)
use_sql_db: yes

// MySQL connection settings
sql.db_hostname: 127.0.0.1
sql.db_port: 3306
sql.db_username: ragnarok
sql.db_password: ragnarok
sql.db_database: ragnarok

// Character server SQL settings
char_server_db: char
```

**Common Settings:**
- `use_sql_db` - Enable SQL storage
- `sql.db_hostname` - Database host
- `sql.db_port` - Database port
- `sql.db_username` - Database user
- `sql.db_password` - Database password
- `sql.db_database` - Database name

---

### Logging Configuration

**File:** `/conf/import/log_conf.txt`

**Example:** Log all items and chat messages

```conf
// Log filter (1 = log all items)
log_filter: 1

// Log all chat types (63 = all)
// 1=Global, 2=Whisper, 4=Party, 8=Guild, 16=Main, 32=Clan
log_chat: 63

// Log trades
log_trade: 1

// Log vending
log_vending: 1

// Log commands
log_commands: 1

// Log NPC transactions
log_npc: 1
```

**Common Settings:**
- `log_filter` - Item logging (1=all, 2=only valuables)
- `log_chat` - Chat logging (bitmask)
- `log_trade` - Trade logging
- `log_vending` - Vending logging
- `log_commands` - Command logging
- `log_npc` - NPC transaction logging

---

### Battle Configuration

**File:** `/conf/import/battle_conf.txt`

This is the **most important** import file. All battle mechanic changes go here.

**Example:** Customize various game mechanics

```conf
//=============================================================
// GUILD SETTINGS (from guild.conf)
//=============================================================

// Guild max level
guild_exp_limit: 90

// Guild skill cooldown (ms)
guild_skill_relog_delay: 0


//=============================================================
// ITEM SETTINGS (from items.conf)
//=============================================================

// Allow vending over max price
vending_over_max: no

// Vending tax (100 = 1%)
vending_tax: 100

// Weapon production success rate (200 = 2x)
weapon_produce_rate: 200

// Potion production success rate
potion_produce_rate: 200

// Item name input for production
produce_item_name_input: 0x03

// Max item stack
stack_amount_item: 30000
stack_amount_equip: 100


//=============================================================
// MISC SETTINGS (from misc.conf)
//=============================================================

// Duel time interval (minutes)
duel_time_interval: 2

// @autotrade requires mapflag
at_mapflag: yes

// @monsterignore behavior
at_monsterignore: yes

// Cash shop show points
cashshop_show_points: yes

// Hide favorites in sell window
hide_fav_sell: yes

// Mail box status on login (0=no, 1=yes, 2=yes if unread)
mail_show_status: 2


//=============================================================
// MONSTER SETTINGS (from monster.conf)
//=============================================================

// Show monster info (3 = name + HP)
// 0 = None, 1 = Name, 2 = HP, 3 = Both
show_mob_info: 3

// Monster HP bar info
monster_hp_bars_info: yes

// MVP tombstone time (ms)
mvp_tomb_enabled: yes


//=============================================================
// PARTY SETTINGS (from party.conf)
//=============================================================

// Party HP mode (1 = show to party)
party_hp_mode: 1

// Display party name
display_party_name: yes

// Party item share type
party_item_share_type: 1


//=============================================================
// PET SETTINGS (from pet.conf)
//=============================================================

// Allow pet renaming
pet_rename: yes

// Pet attack support
pet_attack_support: yes

// Pet damage support
pet_damage_support: yes


//=============================================================
// PLAYER SETTINGS (from player.conf)
//=============================================================

// Max ASPD
max_aspd: 196
max_third_aspd: 196
max_extended_aspd: 196

// Display VIP rates
vip_disp_rate: no

// Max stats
max_parameter: 99

// Max baby stats
max_baby_parameter: 80

// Natural heal weight rate (50 = 50% weight)
natural_heal_weight_rate: 50

// Zeny penalty on death
zeny_penalty: 0


//=============================================================
// EXP SETTINGS (from exp.conf)
//=============================================================

// Base exp rate (100 = 1x, 1000 = 10x)
base_exp_rate: 100

// Job exp rate
job_exp_rate: 100

// MVP exp rate
mvp_exp_rate: 100

// Quest exp rate
quest_exp_rate: 100


//=============================================================
// DROP SETTINGS (from drops.conf)
//=============================================================

// Item drop rate (100 = 1x, 200 = 2x)
item_rate_common: 100
item_rate_heal: 100
item_rate_use: 100
item_rate_equip: 100
item_rate_card: 100
item_rate_mvp: 100


//=============================================================
// SKILL SETTINGS (from skill.conf)
//=============================================================

// Skill delay attack (yes = can't attack while casting)
skill_delay_attack_enable: yes

// Cast cancel on damage
casting_rate: 100

// Skill failure rate
skill_fail_rate: 100


//=============================================================
// STATUS SETTINGS (from status.conf)
//=============================================================

// Debuff on logout (3 = remove buffs and debuffs)
// 0 = None, 1 = Buffs, 2 = Debuffs, 3 = Both
debuff_on_logout: 3

// Max walk speed
max_walk_speed: 150

// Status point cost for stats
// Formula: (x-2)^2 + (x-2)
// standard = 1, advanced = 2
// You can set this to 0 to disable stat point cost
status_point_cost: 1


//=============================================================
// HOMUNCULUS SETTINGS (from homunc.conf)
//=============================================================

// Homunculus autoloot
homunculus_autoloot: no

// Homunculus friendly rate (how often they help)
homunculus_friendly_rate: 100
```

**Battle Config Files Reference:**
- `battle.conf` - General battle mechanics
- `player.conf` - Player settings
- `monster.conf` - Monster behavior
- `skill.conf` - Skill mechanics
- `items.conf` - Item mechanics
- `exp.conf` - Experience rates
- `drops.conf` - Drop rates
- `party.conf` - Party settings
- `guild.conf` - Guild settings
- `pet.conf` - Pet system
- `homunc.conf` - Homunculus system
- `status.conf` - Status changes
- `feature.conf` - Feature toggles
- `client.conf` - Client settings
- `gm.conf` - GM settings
- `battleground.conf` - BG settings
- `instance.conf` - Instance settings

---

## DATABASE FILES (`/db/import/`)

### General Rules

1. **Use YAML format** for database files
2. **Follow exact structure** from main database files
3. **Custom IDs:** Use high ID numbers (30000+) to avoid conflicts
4. **Document your entries** with comments

---

### Custom Achievements

**File:** `/db/import/achievement_db.yml`

**Example:**

```yaml
# Custom Achievements
# Use IDs 280000+ for custom achievements

- Id: 280000
  Group: None
  Name: Emperio
  Reward:
    TitleId: 1035
  Score: 50

- Id: 280001
  Group: None
  Name: Staff
  Reward:
    TitleId: 1036
    ItemId: 607
    Amount: 10
  Score: 50
```

**Fields:**
- `Id` - Unique achievement ID (280000+)
- `Group` - Achievement category
- `Name` - Display name
- `Reward` - Title, items, etc.
- `Score` - Achievement points

---

### Custom Instances

**File:** `/db/import/instance_db.yml`

**Example:**

```yaml
# Custom Housing Instance

- Id: 35
  Name: Home
  TimeLimit: 7200         # 2 hours in seconds
  IdleTimeOut: 900        # 15 minutes idle timeout
  Enter:
    Map: 1@home
    X: 24
    Y: 6
  AdditionalMaps:
    - Map: 2@home
    - Map: 3@home
```

**Fields:**
- `Id` - Unique instance ID
- `Name` - Instance name
- `TimeLimit` - Max duration (seconds)
- `IdleTimeOut` - Idle kick time (seconds)
- `Enter` - Entry point
- `AdditionalMaps` - Extra maps in instance

---

### Monster Appearance Override (Mob Alias)

**File:** `/db/import/mob_avail.yml`

**Example:** Make Porings look like Baphomet

```yaml
# Mob Sprite Aliases

- Mob: PORING
  Sprite: BAPHOMET

- Mob: DROPS
  Sprite: EDDGA

- Mob: MARIN
  Sprite: OSIRIS
```

**Use Case:** Events, fun transformations, placeholder sprites.

---

### Custom Maps

**File:** `/db/import/map_index.txt`

**Example:**

```
// Custom Maps
// Format: <map_name>  {<map_index>}
// If map_index not specified, auto-assigned

1@home    1250
2@home    1251
3@home    1252
ev_has
shops
prt_pvp
custom_woe
```

**Notes:**
- Don't forget to add maps to map_cache.dat using mapcache tool
- Also add maps to `/conf/import/map_conf.txt`

---

### Custom Items

**File:** `/db/import/item_db.yml`

**Example:** Custom items with trade restrictions

```yaml
# Custom Items
# Use IDs 30000+ for custom items

- Id: 34000
  AegisName: Old_Green_Box
  Name: Old Green Box
  Type: Usable
  Buy: 100000
  Weight: 200
  Script: |
    getrandgroupitem 34000,1;
  Trade:
    NoDrop: true
    NoTrade: true
    TradePartner: true
    NoSell: true
    NoCart: true
    NoStorage: true
    NoGuildStorage: true
    NoMail: true
    NoAuction: true

- Id: 34001
  AegisName: House_Keys
  Name: House Keys
  Type: Etc
  Buy: 0
  Sell: 0
  Weight: 10
  Trade:
    NoDrop: true
    NoTrade: true
    TradePartner: true
    NoSell: true
    NoCart: true
    NoStorage: true
    NoGuildStorage: true
    NoMail: true
    NoAuction: true

- Id: 34002
  AegisName: Reputation_Journal
  Name: Reputation Journal
  Type: Etc
  Buy: 0
  Sell: 0
  Weight: 50
  Script: |
    mes "Your reputation: " + #REPUTATION;
    close;
  Trade:
    NoDrop: true
    NoTrade: true
    TradePartner: false
    NoSell: true
    NoCart: true
    NoStorage: true
    NoGuildStorage: true
    NoMail: true
    NoAuction: true
```

**Trade Restrictions:**
- `NoDrop` - Can't drop
- `NoTrade` - Can't trade
- `TradePartner` - Can trade to partner only
- `NoSell` - Can't sell to NPC
- `NoCart` - Can't put in cart
- `NoStorage` - Can't put in Kafra storage
- `NoGuildStorage` - Can't put in guild storage
- `NoMail` - Can't send via mail
- `NoAuction` - Can't auction

---

### Custom Monsters

**File:** `/db/import/mob_db.yml`

**Example:**

```yaml
# Custom Monsters
# Use IDs 30000+ for custom monsters

- Id: 30000
  AegisName: CUSTOM_PORING
  Name: Custom Poring
  Level: 99
  Hp: 1000000
  Sp: 0
  BaseExp: 50000
  JobExp: 30000
  Attack: 1000
  Attack2: 1500
  Defense: 50
  MagicDefense: 40
  Str: 50
  Agi: 50
  Vit: 50
  Int: 50
  Dex: 50
  Luk: 50
  AttackRange: 1
  SkillRange: 10
  ChaseRange: 12
  Size: Small
  Race: Plant
  Element: Water
  ElementLevel: 1
  WalkSpeed: 400
  AttackDelay: 1872
  AttackMotion: 672
  DamageMotion: 480
  Drops:
    - Item: Jellopy
      Rate: 10000
    - Item: Knife
      Rate: 1000
    - Item: Red_Potion
      Rate: 5000
```

---

### Custom Quests

**File:** `/db/import/quest_db.yml`

**Example:**

```yaml
# Custom Quests
# Use IDs 89000+ for custom quests

- Id: 89001
  Title: "Reputation Quest"
  Targets:
    - Mob: PORING
      Count: 100
  Drops:
    - Mob: PORING
      Item: Jellopy
      Count: 1
      Rate: 5000

- Id: 89002
  Title: "Weekly Boss Hunt"
  TimeLimit: Monday 4h
  Targets:
    - Mob: BAPHOMET
      Count: 1
    - Mob: EDDGA
      Count: 1
  Drops:
    - Mob: BAPHOMET
      Item: Evil_Horn
      Count: 1
      Rate: 10000
```

---

## CUSTOM NPC SCRIPTS

**Location:** `/npc/custom/`

**Loading:** Add to `/npc/scripts_custom.conf` or create in `/npc/custom/` directory

**Example:** `/npc/custom/my_custom_npc.txt`

```c
//===== rAthena Script =======================================
//= My Custom NPC
//===== By: ==================================================
//= YourName
//===== Description: =========================================
//= Custom functionality for my server
//============================================================

prontera,150,150,4	script	Custom NPC	4_F_KAFRA1,{
    mes "[Custom NPC]";
    mes "Welcome to my custom server!";
    next;
    mes "[Custom NPC]";
    mes "What would you like?";
    next;
    switch(select("Buff Me:Heal Me:Information:Cancel")) {
    case 1:
        sc_start SC_BLESSING,240000,10;
        sc_start SC_INCREASEAGI,240000,10;
        mes "Buffed!";
        close;
    case 2:
        percentheal 100,100;
        mes "Healed!";
        close;
    case 3:
        mes "Server Info Here";
        close;
    case 4:
        close;
    }
}
```

**Load in** `/npc/scripts_custom.conf`:
```
npc: npc/custom/my_custom_npc.txt
```

---

## BEST PRACTICES

### ✅ DO

1. **Always use import directories** for customizations
2. **Document your changes** with comments
3. **Use high IDs** for custom content (30000+ items, 30000+ mobs, 89000+ quests, 280000+ achievements)
4. **Backup import directories** regularly
5. **Test changes** in development environment first
6. **Keep imports organized** by category
7. **Version control** your import directory
8. **Use consistent naming** conventions

### ❌ DON'T

1. **Don't edit core files** in `/conf/` or `/db/` directly
2. **Don't use conflicting IDs** with official content
3. **Don't forget** to reload server after changes
4. **Don't copy entire files** to import - only what you change
5. **Don't forget syntax** - YAML is whitespace-sensitive
6. **Don't skip backups** before major changes

---

## UPDATING RATHENA

### Safe Update Workflow

```bash
# 1. Backup your import directories
cp -r conf/import conf/import.backup
cp -r db/import db/import.backup
cp -r npc/custom npc/custom.backup

# 2. Pull latest rAthena updates
git pull origin master

# 3. Check for conflicts (there should be none if using imports)
git status

# 4. Recompile server
./configure && make clean && make server

# 5. Test your changes
# Start server and verify everything works

# 6. If issues occur, restore from backup
# cp -r conf/import.backup/* conf/import/
```

**Why This Works:**
- Core files get updated
- Your import files remain untouched
- No merge conflicts
- Easy rollback if needed

---

## TROUBLESHOOTING

### Issue: Changes not applying

**Solutions:**
1. Check file is in correct `/import/` directory
2. Verify syntax (YAML is picky about indentation)
3. Reload server/scripts: `@reloadscript`
4. Check for typos in setting names
5. Ensure import file has correct extension (`.txt` for conf, `.yml` for db)

### Issue: Server won't start

**Solutions:**
1. Check syntax errors in import files
2. Review server console output for errors
3. Temporarily rename import file to disable it
4. Test with minimal imports first

### Issue: Database entries not loading

**Solutions:**
1. Verify YAML formatting (spaces, not tabs)
2. Check ID conflicts with official content
3. Ensure file is named correctly
4. Check that imports are enabled in main files

---

## IMPORT FILE LOCATIONS REFERENCE

### Configuration Files
```
/conf/import/
├── login_conf.txt           # Login server settings
├── char_conf.txt            # Char server settings
├── map_conf.txt             # Map server settings
├── inter_conf.txt           # Inter-server settings
├── log_conf.txt             # Logging settings
├── battle_conf.txt          # Battle mechanics (IMPORTANT)
├── script_conf.txt          # Script settings
├── packet_conf.txt          # Packet settings
└── channels_conf.txt        # Chat channels
```

### Database Files
```
/db/import/
├── achievement_db.yml       # Custom achievements
├── instance_db.yml          # Custom instances
├── item_db.yml              # Custom items
├── mob_db.yml               # Custom monsters
├── quest_db.yml             # Custom quests
├── skill_db.yml             # Custom skills
├── mob_avail.yml            # Mob sprite aliases
├── map_index.txt            # Custom map list
└── ... (any database file can be imported)
```

---

## EXAMPLE: COMPLETE SERVER SETUP

Here's a typical server customization setup:

### `/conf/import/char_conf.txt`
```conf
server_name: MyServer
start_zeny: 50000
start_point: prontera,156,191
```

### `/conf/import/battle_conf.txt`
```conf
base_exp_rate: 500
job_exp_rate: 500
item_rate_common: 200
max_aspd: 196
```

### `/db/import/item_db.yml`
```yaml
- Id: 34000
  AegisName: Starter_Box
  Name: Starter Box
  Type: Usable
  Buy: 0
  Weight: 0
  Script: |
    getitem 501,100;  // Red Potion
    getitem 503,50;   // Yellow Potion
    getitem 601,10;   // Fly Wing
```

### `/npc/custom/starter_npc.txt`
```c
prontera,156,185,4	script	Starter Helper	4_F_KAFRA1,{
    if (#STARTER_RECEIVED) {
        mes "Welcome back!";
        close;
    }
    mes "Welcome! Here's a starter box!";
    getitem 34000,1;
    set #STARTER_RECEIVED,1;
    close;
}
```

---

## SUMMARY

**Import System = Update-Safe Customization**

- 🔒 **Safe:** Never touch core files
- 🔄 **Update-Friendly:** No merge conflicts
- 🎯 **Organized:** Clear separation of custom vs official
- 💾 **Backup-Friendly:** Just backup import directories
- 🔧 **Maintainable:** See exactly what you changed

**Remember:** Only override what you need to change!

---

## SEE ALSO

- **KB_CONF_001:** Battle Configuration Deep Dive
- **KB_DB_001:** Database System Overview
- **KB_EXAMPLE_001:** Configuration Examples

---

*Last Updated: 2025-10-23*
*rAthena Documentation*
---
kb_id: KB_REF_008
kb_type: reference
kb_category: items
kb_subcategory: item_bonuses
kb_keywords: [item bonuses, bonus, bonus2, bonus3, bonus4, bonus5, equipment, item script, stats, damage, resist, autospell, constants, bStr, bAtk, bMaxHP]
kb_related: [KB_DB_001, KB_REF_005]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2015-10-29
kb_use_case: [item_creation, equipment_scripts, custom_items, balance]
---

# rAthena Item Bonuses Reference

Complete reference for item bonus commands used in equipment scripts.

## Overview

Item bonuses are script commands used in item_db.yml Script fields to grant special properties to equipment. They're automatically applied when equipping and removed when unequipping.

**Usage Location:** `item_db.yml` → Script field

**Example:**
```yaml
- Id: 1234
  AegisName: Custom_Sword
  Name: Custom Sword
  Type: Weapon
  Script: |
    bonus bStr,10;
    bonus bAtk,50;
    bonus2 bAddRace,RC_Demon,20;
```

---

## TABLE OF CONTENTS

1. [Constants](#1-constants)
2. [Basic Stats](#2-basic-stats)
3. [HP/SP/AP](#3-hpspap)
4. [Attack & Defense](#4-attack--defense)
5. [Accuracy & Evasion](#5-accuracy--evasion)
6. [Damage Modifiers](#6-damage-modifiers)
7. [Resistance & Reduction](#7-resistance--reduction)
8. [AutoSpell](#8-autospell)
9. [Special Effects](#9-special-effects)
10. [Advanced Bonuses](#10-advanced-bonuses)

---

## 1. CONSTANTS

### Status Effects (eff)
```c
Eff_Bleeding, Eff_Blind, Eff_Burning, Eff_Confusion, Eff_Crystalize,
Eff_Curse, Eff_DPoison, Eff_Fear, Eff_Freeze, Eff_Poison, Eff_Silence,
Eff_Sleep, Eff_Stone, Eff_Stun, Eff_Freezing, Eff_Heat, Eff_Deepsleep,
Eff_WhiteImprison, Eff_Hallucination
```

---

### Elements (e)
```c
Ele_Dark, Ele_Earth, Ele_Fire, Ele_Ghost, Ele_Holy, Ele_Neutral,
Ele_Poison, Ele_Undead, Ele_Water, Ele_Wind, Ele_All
```

---

### Races (r)
```c
RC_Angel, RC_Brute, RC_DemiHuman, RC_Demon, RC_Dragon, RC_Fish,
RC_Formless, RC_Insect, RC_Plant, RC_Player_Human, RC_Player_Doram,
RC_Undead, RC_All
```

---

### Classes (c)
```c
Class_Normal, Class_Boss, Class_Guardian, Class_All
```

---

### Sizes (s)
```c
Size_Small, Size_Medium, Size_Large, Size_All
```

---

### Trigger Criteria (bf)

**Range:**
- `BF_SHORT` - Melee attacks
- `BF_LONG` - Ranged attacks

**Type:**
- `BF_WEAPON` - Weapon skills
- `BF_MAGIC` - Magic skills
- `BF_MISC` - Misc skills

**Attack Type:**
- `BF_NORMAL` - Normal attacks
- `BF_SKILL` - Skills

---

### Trigger Criteria (atf)

**Target:**
- `ATF_SELF` - Trigger on self
- `ATF_TARGET` - Trigger on target

**Range:**
- `ATF_SHORT` - Melee attacks
- `ATF_LONG` - Ranged attacks

**Type:**
- `ATF_WEAPON` - Physical attacks
- `ATF_SKILL` - Skills
- `ATF_MAGIC` - Magic skills
- `ATF_MISC` - Misc skills

---

## 2. BASIC STATS

### Base Stats

```c
bonus bStr,n;          // STR + n
bonus bAgi,n;          // AGI + n
bonus bVit,n;          // VIT + n
bonus bInt,n;          // INT + n
bonus bDex,n;          // DEX + n
bonus bLuk,n;          // LUK + n
bonus bAllStats,n;     // All stats + n
bonus bAgiVit,n;       // AGI + n, VIT + n
bonus bAgiDexStr,n;    // STR + n, AGI + n, DEX + n
```

**Examples:**
```yaml
# +10 STR sword
Script: |
  bonus bStr,10;

# +5 all stats armor
Script: |
  bonus bAllStats,5;

# AGI/VIT shoes
Script: |
  bonus bAgiVit,3;
```

---

### Trait Stats (4th Job)

```c
bonus bPow,n;          // POW + n
bonus bSta,n;          // STA + n
bonus bWis,n;          // WIS + n
bonus bSpl,n;          // SPL + n
bonus bCon,n;          // CON + n
bonus bCrt,n;          // CRT + n
bonus bAllTraitStats,n; // All trait stats + n
```

---

## 3. HP/SP/AP

```c
bonus bMaxHP,n;        // MaxHP + n
bonus bMaxHPrate,n;    // MaxHP + n%
bonus bMaxSP,n;        // MaxSP + n
bonus bMaxSPrate,n;    // MaxSP + n%
bonus bMaxAP,n;        // MaxAP + n (4th job)
bonus bMaxAPrate,n;    // MaxAP + n%
```

**Examples:**
```yaml
# +500 HP armor
Script: |
  bonus bMaxHP,500;

# +10% HP/SP accessory
Script: |
  bonus bMaxHPrate,10;
  bonus bMaxSPrate,10;
```

---

## 4. ATTACK & DEFENSE

### Attack

```c
bonus bBaseAtk,n;          // Base ATK + n
bonus bAtk,n;              // ATK + n
bonus bAtk2,n;             // ATK2 + n
bonus bAtkRate,n;          // ATK + n%
bonus bWeaponAtkRate,n;    // Weapon ATK + n%
bonus bMatk,n;             // MATK + n
bonus bMatk2,n;            // MATK + n (hidden)
bonus bMatkRate,n;         // MATK + n%
bonus bWeaponMatkRate,n;   // Weapon MATK + n%
```

**Examples:**
```yaml
# High damage sword
Script: |
  bonus bAtk,100;
  bonus bAtkRate,15;

# Magic staff
Script: |
  bonus bMatk,150;
  bonus bMatkRate,10;
```

---

### Defense

```c
bonus bDef,n;              // Equipment DEF + n
bonus bDefRate,n;          // Equipment DEF + n%
bonus bDef2,n;             // VIT-based DEF + n
bonus bDef2Rate,n;         // VIT-based DEF + n%
bonus bMdef,n;             // Equipment MDEF + n
bonus bMdefRate,n;         // Equipment MDEF + n%
bonus bMdef2,n;            // INT-based MDEF + n
bonus bMdef2Rate,n;        // INT-based MDEF + n%
```

**Examples:**
```yaml
# Tank shield
Script: |
  bonus bDef,50;
  bonus bMdef,20;

# % defense boost
Script: |
  bonus bDefRate,15;
```

---

## 5. ACCURACY & EVASION

```c
bonus bHit,n;              // HIT + n
bonus bHitRate,n;          // HIT + n%
bonus bCritical,n;         // CRIT + n
bonus bCriticalRate,n;     // CRIT + n%
bonus bFlee,n;             // FLEE + n
bonus bFleeRate,n;         // FLEE + n%
bonus bFlee2,n;            // Perfect Dodge + n
bonus bFlee2Rate,n;        // Perfect Dodge + n%
bonus bPerfectHitRate,n;   // Perfect Hit + n%
bonus bPerfectHitAddRate,n; // Perfect Hit + n%
```

**Examples:**
```yaml
# Accuracy gloves
Script: |
  bonus bHit,20;

# Critical dagger
Script: |
  bonus bCritical,15;
  bonus bCriticalRate,10;

# Evasion boots
Script: |
  bonus bFlee,15;
  bonus bFlee2,5;
```

---

## 6. DAMAGE MODIFIERS

### Race Damage

```c
bonus2 bAddRace,r,n;           // +n% damage vs race
bonus2 bMagicAddRace,r,n;      // +n% magic damage vs race
bonus2 bSubRace,r,n;           // -n% damage from race
bonus2 bSubRace2,mr,n;         // -n% damage from monster race
```

**Examples:**
```yaml
# Anti-Demon sword
Script: |
  bonus2 bAddRace,RC_Demon,20;
  bonus2 bAddRace,RC_Undead,20;

# Anti-Boss armor
Script: |
  bonus2 bSubRace,RC_All,10;
  if (readparam(bBaseLevel) >= 99) {
    bonus2 bSubRace,Class_Boss,15;
  }
```

---

### Element Damage

```c
bonus2 bAddEle,e,n;            // +n% damage vs element
bonus2 bMagicAddEle,e,n;       // +n% magic damage vs element
bonus2 bSubEle,e,n;            // -n% damage from element
bonus3 bAddEle,e,n,bf;         // +n% damage vs element with flags
```

**Examples:**
```yaml
# Fire damage sword
Script: |
  bonus2 bAddEle,Ele_Fire,25;

# Water resistance armor
Script: |
  bonus2 bSubEle,Ele_Water,20;
```

---

### Size Damage

```c
bonus2 bAddSize,s,n;           // +n% damage vs size
bonus2 bMagicAddSize,s,n;      // +n% magic damage vs size
bonus2 bSubSize,s,n;           // -n% damage from size
bonus bNoSizeFix;              // Ignore size penalty
```

**Examples:**
```yaml
# Large monster hunter
Script: |
  bonus2 bAddSize,Size_Large,20;

# Pike (no size penalty)
Script: |
  bonus bNoSizeFix;
```

---

### Class Damage

```c
bonus2 bAddClass,c,n;          // +n% damage vs class
bonus2 bMagicAddClass,c,n;     // +n% magic damage vs class
bonus2 bSubClass,c,n;          // -n% damage from class
```

**Examples:**
```yaml
# MVP killer weapon
Script: |
  bonus2 bAddClass,Class_Boss,30;
  bonus2 bAddClass,Class_Guardian,30;
```

---

## 7. RESISTANCE & REDUCTION

### Physical Reduction

```c
bonus bNearAtkDef,n;           // -n% damage from melee
bonus bLongAtkDef,n;           // -n% damage from ranged
bonus bWeaponAtkRate,n;        // +n% weapon attack
bonus bCritAtkRate,n;          // +n% critical damage
bonus bCriticalDef,n;          // -n critical rate from enemy
```

---

### Magic Reduction

```c
bonus bMagicDamageReturn,n;    // n% magic damage reflected
bonus bMagicAtkEle,e;          // Change magic element
```

---

### Status Resistance

```c
bonus2 bResEff,eff,n;          // +n% resistance to status
bonus2 bAddEffWhenHit,eff,n;   // n% chance to inflict status when hit
bonus3 bAddEff,eff,n,atf;      // n% chance to inflict status
```

**Examples:**
```yaml
# Stun immunity helm
Script: |
  bonus2 bResEff,Eff_Stun,10000;

# Poison resistance armor
Script: |
  bonus2 bResEff,Eff_Poison,5000;
  bonus2 bResEff,Eff_DPoison,5000;

# Curse on hit
Script: |
  bonus2 bAddEffWhenHit,Eff_Curse,1000;
```

---

## 8. AUTOSPELL

### Basic AutoSpell

```c
bonus4 bAutoSpell,sk,lv,rate,bf;  // Cast skill on attack
bonus4 bAutoSpellWhenHit,sk,lv,rate,bf;  // Cast skill when hit
bonus5 bAutoSpell,sk,lv,rate,bf,iid;  // With item cost
```

**Examples:**
```yaml
# Fire Bolt on attack (3% chance)
Script: |
  bonus4 bAutoSpell,MG_FIREBOLT,5,30,0;

# Heal when hit (5% chance)
Script: |
  bonus4 bAutoSpellWhenHit,AL_HEAL,10,50,0;

# Cold Bolt (long range only)
Script: |
  bonus4 bAutoSpell,MG_COLDBOLT,5,30,BF_LONG;
```

---

### Advanced AutoSpell

```c
bonus4 bAutoSpellWhenHit,sk,lv,rate,bf;
bonus5 bAutoSpellWhenHit,sk,lv,rate,bf,iid;
bonus5 bAutoSpell,sk,-lv,rate,bf,atf;  // Negative level = cast on self
```

**Examples:**
```yaml
# Blessing on self when hit
Script: |
  bonus5 bAutoSpellWhenHit,AL_BLESSING,-10,100,BF_WEAPON,ATF_SELF;

# Provoke on melee attack
Script: |
  bonus4 bAutoSpell,SM_PROVOKE,10,50,BF_SHORT;
```

---

## 9. SPECIAL EFFECTS

### HP/SP Drain

```c
bonus bHPDrainValue,n;         // Drain n HP per hit
bonus2 bHPDrainRate,n,m;       // Drain n% HP, max m per hit
bonus2 bSPDrainRate,n,m;       // Drain n% SP, max m per hit
bonus3 bHPDrainRate,n,m,r;     // Drain from specific race
```

**Examples:**
```yaml
# Vampire sword
Script: |
  bonus2 bHPDrainRate,5,100;  // 5% drain, max 100 HP

# SP drain accessory
Script: |
  bonus2 bSPDrainRate,2,50;   // 2% drain, max 50 SP
```

---

### SP Cost Reduction

```c
bonus bUseSPrate,n;            // SP cost +n% (use negative)
bonus2 bSkillUseSP,sk,n;       // Skill SP cost +n
bonus2 bSkillUseSPrate,sk,n;   // Skill SP cost +n%
```

**Examples:**
```yaml
# Reduce all SP costs by 20%
Script: |
  bonus bUseSPrate,-20;

# Reduce Heal cost by 50%
Script: |
  bonus2 bSkillUseSPrate,AL_HEAL,-50;
```

---

### Cast Time

```c
bonus bCastrate,n;             // Cast time +n% (use negative)
bonus2 bSkillCooldown,sk,n;    // Skill cooldown -n ms
bonus2 bSkillCast,sk,n;        // Skill cast time +n ms
bonus2 bVariableCastrate,sk,n; // Variable cast +n%
bonus2 bFixedCastrate,sk,n;    // Fixed cast +n%
```

**Examples:**
```yaml
# Instant cast accessory
Script: |
  bonus bCastrate,-100;

# Heal -1 second cooldown
Script: |
  bonus2 bSkillCooldown,AL_HEAL,-1000;
```

---

### ASPD & Movement

```c
bonus bAspd,n;                 // ASPD + n
bonus bAspdRate,n;             // ASPD + n%
bonus bSpeedRate,n;            // Movement speed +n%
bonus bSpeedAddRate,n;         // Movement speed +n%
```

**Examples:**
```yaml
# AGI boots
Script: |
  bonus bAspd,1;
  bonus bSpeedRate,25;
```

---

## 10. ADVANCED BONUSES

### Skill Damage

```c
bonus2 bSkillAtk,sk,n;         // Skill damage +n%
bonus2 bSkillHeal,sk,n;        // Skill heal +n%
bonus3 bAddEff,eff,n,atf;      // Add status effect chance
```

**Examples:**
```yaml
# Bash damage +50%
Script: |
  bonus2 bSkillAtk,SM_BASH,50;

# Heal effectiveness +30%
Script: |
  bonus2 bSkillHeal,AL_HEAL,30;
```

---

### Combo Bonuses

```c
bonus bComboAddBonus,iid;      // If equipped with item
```

**Example:**
```yaml
# Bonus when worn with Shield (2105)
Script: |
  bonus bStr,5;
  if (isequipped(2105)) {
    bonus bAtk,50;
    bonus bDef,20;
  }
```

---

### Conditional Bonuses

```c
if (condition) { bonus ...; }
```

**Examples:**
```yaml
# Level-based bonus
Script: |
  bonus bStr,5;
  if (readparam(bBaseLevel) >= 99) {
    bonus bStr,5;
    bonus bAtk,50;
  }

# Class-specific
Script: |
  bonus bAtk,50;
  if (Class == Job_Swordman) {
    bonus bAtk,30;
  }

# Time-based
Script: |
  bonus bAtk,50;
  if (gettime(DT_HOUR) >= 18 || gettime(DT_HOUR) < 6) {
    bonus bAtk,30;  // Night bonus
  }
```

---

## COMMON PATTERNS

### Tank Armor
```yaml
Script: |
  bonus bMaxHPrate,10;
  bonus bDef,30;
  bonus bMdef,20;
  bonus2 bSubRace,RC_All,5;
```

### DPS Weapon
```yaml
Script: |
  bonus bAtk,100;
  bonus bAtkRate,15;
  bonus bCritical,10;
  bonus bAspd,2;
```

### Magic Staff
```yaml
Script: |
  bonus bMatk,150;
  bonus bMatkRate,10;
  bonus bInt,5;
  bonus bCastrate,-10;
```

### MVP Killer
```yaml
Script: |
  bonus2 bAddClass,Class_Boss,30;
  bonus2 bAddClass,Class_Guardian,30;
  bonus2 bHPDrainRate,3,100;
```

### Support Accessory
```yaml
Script: |
  bonus bInt,5;
  bonus2 bSkillHeal,AL_HEAL,30;
  bonus2 bSkillUseSPrate,AL_HEAL,-25;
  bonus bUseSPrate,-10;
```

### PvP Armor
```yaml
Script: |
  bonus bMaxHPrate,15;
  bonus2 bSubRace,RC_Player_Human,10;
  bonus2 bSubRace,RC_Player_Doram,10;
  bonus2 bResEff,Eff_Stun,5000;
  bonus2 bResEff,Eff_Freeze,5000;
```

---

## BONUS COMMAND LEVELS

### bonus (1 parameter)
```c
bonus bStr,10;
```

### bonus2 (2 parameters)
```c
bonus2 bAddRace,RC_Demon,20;
```

### bonus3 (3 parameters)
```c
bonus3 bAddEff,Eff_Stun,500,ATF_SHORT;
```

### bonus4 (4 parameters)
```c
bonus4 bAutoSpell,MG_FIREBOLT,5,30,0;
```

### bonus5 (5 parameters)
```c
bonus5 bAutoSpell,MG_FIREBOLT,5,30,0,Red_Blood;
```

---

## DEBUGGING

### Test Equipment
```c
// Check if item bonuses apply
@item 1234  // Spawn item
// Equip and check stats with @stats

// Remove to verify bonus removal
@delitem 1234 1
```

### Display Bonus Values
```yaml
Script: |
  bonus bStr,10;
  dispbottom "STR +10 from equipment";
```

---

## TIPS & BEST PRACTICES

1. **Test thoroughly** - Bonuses stack in complex ways
2. **Balance carefully** - Too many bonuses = overpowered items
3. **Use constants** - RC_Demon instead of numbers
4. **Document bonuses** - Comment your script
5. **Consider combinations** - Multiple items with same bonus
6. **Check renewal mode** - Some bonuses work differently
7. **Validate IDs** - Skill IDs, item IDs must be correct
8. **Use conditionals** - Level/class-based bonuses for progression

---

## SEE ALSO

- **Full Reference:** `/doc/item_bonus.txt` (512 lines, 100+ bonus types)
- **KB_REF_005:** Script Commands Reference
- **KB_DB_001:** Item Database Structure
- **Item Database:** `/db/(pre-)re/item_db.yml`

---

*Last Updated: 2015-10-29*
*rAthena Documentation - Item Bonuses*
---
kb_id: KB_REF_003
kb_type: reference
kb_category: map_configuration
kb_subcategory: mapflags
kb_keywords: [mapflag, map settings, pvp, gvg, woe, restrictions, noteleport, nowarp, noreturn, nosave, battle, map behavior, setmapflag, removemapflag]
kb_related: [KB_CMD_010, KB_CONF_003]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2013-08-30
kb_use_case: [map_configuration, pvp_setup, woe_setup, server_customization]
---

# rAthena Mapflag Reference

Complete reference for all mapflags that control map behavior and restrictions.

## Overview

Mapflags determine how a map behaves in various situations - from teleportation restrictions to PvP modes to weather effects. They are essential for configuring your server's gameplay experience.

**Configuration:**
- Set in NPC scripts using `setmapflag` command
- Remove using `removemapflag` command
- Usually configured in `/npc/mapflag/` directory

**Basic Syntax:**
```c
<map_name>	mapflag	<mapflag_name>{	<parameters>}
```

---

## CATEGORIES

1. [Restrictions](#1-restrictions) - Movement, items, trading
2. [Battle-Related](#2-battle-related) - PvP, GvG, damage
3. [Map Effects](#3-map-effects) - Weather, visuals
4. [Miscellaneous](#4-miscellaneous) - Exp rates, special features

---

## 1. RESTRICTIONS

### noreturn

**Description:** Disables map-warping items that return players to specific locations.

**Blocks:**
- Butterfly Wing (ID 602)
- Yellow/Green/Red/Blue Butterfly Wing (IDs 14582-14585)
- Siege Teleport Scroll (ID 14591)
- Dungeon Teleport Scroll 1/2/3 (IDs 14527, 14581, 12352)
- `warpparty` and `warpguild` script commands (for destinations outside current map)

**Example:**
```c
prontera	mapflag	noreturn
```

**Use Case:** WoE castles, dungeons, event maps where you don't want easy exits.

---

### noteleport

**Description:** Disables ALL teleportation methods within a map.

**Blocks:**
- Fly Wing (ID 601)
- Giant Fly Wing (ID 12212)
- Skills: AL_TELEPORT, TK_HIGHJUMP, SC_DIMENSIONDOOR
- Skills won't teleport targets: RG_INTIMIDATE, NPC_EXPULSION, CG_TAROTCARD
- Script command `warp` with "Random" as destination
- Script command `warpwaitingpc` with "SavePoint" as destination
- Script command `unitwarp` for players
- Atcommand `@jump`

**Example:**
```c
pvp_n_1-1	mapflag	noteleport
```

**Use Case:** PvP arenas, boss rooms, areas where teleporting would be unfair or break gameplay.

---

### nowarp

**Description:** Disables warping FROM a map (prevents leaving).

**Blocks:**
- Script commands `warpparty` and `warpguild` won't warp players FROM nowarp maps
- Atcommands: `@warp`, `@go`, `@load`, `@jump`
- Atcommands: `@partyrecall`, `@guildrecall`, `@recallall` won't pull players from nowarp maps
- Skill GD_EMERGENCYCALL won't warp players from nowarp maps
- Unit UNT_CALLFAMILY won't warp players from nowarp maps

**Example:**
```c
guild_vs1	mapflag	nowarp
```

**Use Case:** Lock players in area (event maps, special instances, jail).

**Note:** Players can still be warped TO the map, just not FROM it.

---

### nowarpto

**Description:** Disables warping TO a map (prevents entering).

**Blocks:**
- Atcommands: `@warp`, `@go`, `@load`, `@jump` cannot target this map
- Atcommands: `@partyrecall`, `@guildrecall`, `@recallall` cannot target this map
- Command `/memo` disabled
- Skill GD_EMERGENCYCALL disabled (if flag 16 set in `/conf/battle/skill.conf`) - doesn't work for gvg_castle maps

**Example:**
```c
guild_vs2	mapflag	nowarpto
```

**Use Case:** Restricted access maps, GM-only areas, prevent unauthorized entry.

---

### nogo

**Description:** Disables usage of `@go` command on the map.

**Example:**
```c
prontera	mapflag	nogo
```

**Use Case:** Prevent players from using `@go` shortcut to leave area.

---

### nosave <map_name>,<x>,<y>

**Description:** Disables auto-saving on map. Players who log off here will be warped to specified location on login.

**Parameters:**
- `<map_name>`: Map to respawn at (use `SavePoint` for player's save point)
- `<x>,<y>`: Coordinates (optional with SavePoint)

**Examples:**
```c
// Respawn at SavePoint
guild_vs1	mapflag	nosave	SavePoint

// Respawn at specific location
pvp_n_1-1	mapflag	nosave	prontera,156,191
```

**Use Case:** Temporary areas, dungeons, instances where you don't want save point changed.

---

### nomemo

**Description:** Disables saving warp point and marriage skills.

**Blocks:**
- `/memo` command (can't save warp point)
- Marriage skills: WE_CALLPARTNER, WE_CALLPARENT, WE_CALLBABY

**Example:**
```c
gef_dun00	mapflag	nomemo
```

**Use Case:** Dungeons, instances, areas where warp points would break progression.

---

### noitemconsumption

**Description:** Disables usage of ALL items on the map.

**Blocks:**
- All consumable items
- Equipment changes
- Item usage

**Example:**
```c
pvp_y_1-1	mapflag	noitemconsumption
```

**Use Case:** Pure skill-based PvP, special challenge maps, no-item events.

**Note:** Can be bypassed with PC_PERM_ITEM_UNCONDITIONAL permission.

---

### notrade

**Description:** Disables trading between players on the map.

**Example:**
```c
prontera	mapflag	notrade
```

**Use Case:** Prevent trading in specific areas, reduce scam potential in town centers.

---

### nodrop

**Description:** Disables dropping items on the map.

**Exception:** Items may still drop if inventory is full and `item_flooritem_check` is disabled in `/conf/battle/items.conf`.

**Example:**
```c
prontera	mapflag	nodrop
```

**Use Case:** Keep maps clean, prevent item drops in towns, anti-grief measure.

---

### noloot / nomobloot / nomvploot

**Description:** Disables monsters from dropping items.

- `noloot`: All monsters (same as nomobloot + nomvploot)
- `nomobloot`: Normal monsters don't drop
- `nomvploot`: MVP monsters don't drop

**Note:** Looted items (from Gank/Steal skills) will still drop.

**Examples:**
```c
// No drops at all
prt_fild08	mapflag	noloot

// Only normal mobs don't drop (MVPs still do)
pay_fild01	mapflag	nomobloot

// MVPs don't drop (normal mobs still do)
mjolnir_01	mapflag	nomvploot
```

**Use Case:** Training maps, pure exp farming, reduce item database load.

---

### noexp / nobaseexp / nojobexp

**Description:** Disables gaining experience from monsters.

- `noexp`: No base AND job exp (same as nobaseexp + nojobexp)
- `nobaseexp`: No base experience
- `nojobexp`: No job experience

**Includes:** MVP bonuses also disabled.

**Examples:**
```c
// No experience at all
pvp_y_1-1	mapflag	noexp

// No base exp (still get job exp)
prt_fild08	mapflag	nobaseexp

// No job exp (still get base exp)
pay_fild01	mapflag	nojobexp
```

**Use Case:** PvP maps, testing areas, item farming without leveling.

---

### nopenalty / noexppenalty / nozenypenalty

**Description:** Disables loss of exp/zeny upon death.

- `nopenalty`: No exp AND zeny loss (same as noexppenalty + nozenypenalty)
- `noexppenalty`: No exp loss on death
- `nozenypenalty`: No zeny loss on death

**Notes:**
- `noexppenalty` also affects pets
- Skills PR_REDEMPTIO and LG_INSPIRATION won't deduct EXP
- `nozenypenalty` only applies if `zeny_penalty` enabled in `/conf/battle/exp.conf`

**Examples:**
```c
// No penalties at all
prontera	mapflag	nopenalty

// Only exp protected
pvp_n_1-1	mapflag	noexppenalty

// Only zeny protected
gef_fild00	mapflag	nozenypenalty
```

**Use Case:** Newbie areas, PvP maps, event maps, low-penalty zones.

---

### nochat

**Description:** Disables chatroom creation on the map.

**Example:**
```c
pvp_n_1-1	mapflag	nochat
```

**Use Case:** Reduce spam in busy areas, PvP focus, event maps.

---

### novending

**Description:** Disables shop creation from MC_VENDING skill.

**Example:**
```c
prontera	mapflag	novending
```

**Use Case:** Designated vending areas, reduce map clutter, prevent vendor spam.

---

### nobuyingstore

**Description:** Disables shop creation from ALL_BUYING_STORE skill.

**Example:**
```c
prontera	mapflag	nobuyingstore
```

**Use Case:** Designated buying areas, prevent spam, organize economy.

---

### nousecart

**Description:** Disables cart usage on the map.

**Example:**
```c
aldebaran	mapflag	nousecart
```

**Use Case:** Reduce sprite load, specific area restrictions, roleplay purposes.

---

### noskill

**Description:** Disables ALL skill usage on the map.

**Example:**
```c
prontera	mapflag	noskill
```

**Use Case:** Safe zones, event maps, roleplaying areas, extreme restrictions.

**Warning:** Very restrictive - disables ALL skills including buffs.

---

### restricted <zone>

**Description:** Disables certain items and skills based on zone number.

**Zone Databases:**
- `/db/(pre-)re/item_noequip.txt` - Item restrictions
- `/db/(pre-)re/skill_nocast_db.txt` - Skill restrictions

**Restricted Zones:**
- `1` - Aldebaran Turbo Track
- `2` - Jail
- `3` - Izlude Battle Arena
- `4` - WoE:SE Maps
- `5` - Sealed Shrine
- `6` - Instances (Endless Tower, Orc's Memory, Nidhoggr's Instance)
- `7` - Towns
- `8` - WOE:TE Dungeons

**Examples:**
```c
// Restrict town items/skills
prontera	mapflag	restricted	7

// Restrict WoE items/skills
prtg_cas01	mapflag	restricted	4
```

**Use Case:** Balanced competitive areas, specific gameplay rules, item/skill bans.

---

### monster_noteleport

**Description:** Prevents monsters from teleporting on the map.

**Blocks:**
- Monster teleportation skills
- RG_INTIMIDATE won't teleport monsters

**Example:**
```c
boss_map	mapflag	monster_noteleport
```

**Use Case:** Boss fights, prevent mobs escaping, specific monster behavior control.

---

### nobranch

**Description:** Disables monster-spawning items on the map.

**Blocks:**
- Dead Branch (ID 604)
- Bloody Branch (ID 12103)
- Poring Box (ID 12109)
- Red Pouch (ID 12024)

**Note:** Items can be modified in `/db/(pre-)re/item_flag.txt`.

**Special:** If `mob_warp` enabled with flag 4 in `/conf/battle/monster.conf`, also prevents mobs being warped onto the map (except slaves).

**Example:**
```c
prontera	mapflag	nobranch
```

**Use Case:** Towns, prevent griefing, controlled spawn areas.

---

### noicewall

**Description:** Disables skill WZ_ICEWALL on the map.

**Example:**
```c
pvp_n_1-1	mapflag	noicewall
```

**Use Case:** PvP balance, prevent blocking, reduce skill spam.

---

### nosunmoonstarmiracle

**Description:** Disables Star Gladiator's "Solar, Lunar, and Stellar Miracle" from occurring.

**Example:**
```c
prontera	mapflag	nosunmoonstarmiracle
```

**Use Case:** Prevent exploit areas, balance specific maps.

---

### forcemineffect

**Description:** Forces simpler skill effects (like `/mineffect` command).

**Example:**
```c
pvp_n_1-1	mapflag	forcemineffect
```

**Use Case:** Performance optimization, reduce lag in busy areas, cleaner visuals.

---

### nolockon

**Description:** Disables attacking another player without holding shift or using `/ns`.

**Example:**
```c
prontera	mapflag	nolockon
```

**Use Case:** Prevent accidental PvP, safe zones, town protection.

---

### nocommand <group_level>

**Description:** Disables commands on the map.

**Parameters:**
- No parameter: Disables ALL commands for everyone
- `<group_level>`: Only disables for players with group level BELOW this value

**Examples:**
```c
// Disable all commands for everyone
pvp_n_1-1	mapflag	nocommand

// Disable commands for group level below 50 (normal players)
prontera	mapflag	nocommand	50
```

**Use Case:** Prevent command abuse, fair play areas, restricted zones.

---

### nomapchannelautojoin

**Description:** Stops players from automatically joining #map channel.

**Requirements:**
- Map channels must be enabled
- `map_local_channel_autojoin` must be true in `/conf/channels.conf`

**Example:**
```c
prontera	mapflag	nomapchannelautojoin
```

**Use Case:** Reduce chat spam, private areas, roleplay control.

---

### notomb

**Description:** Disables MVP tombs from appearing on the map.

**Example:**
```c
boss_map	mapflag	notomb
```

**Use Case:** Clean boss areas, prevent tomb spam, aesthetic control.

---

### nocostume

**Description:** Disables costume sprites on the map.

**Notes:**
- Only disables visual sprites, NOT item effects
- If player logs out on nocostume map, costumes won't show in character server either

**Example:**
```c
prontera	mapflag	nocostume
```

**Use Case:** Roleplay immersion, aesthetic control, visual consistency.

---

### norenewaldroppenalty

**Description:** Disables renewal drop rate penalty due to level difference.

**Example:**
```c
prt_fild08	mapflag	norenewaldroppenalty
```

**Use Case:** Training maps, allow high-level farming, balanced drop rates.

---

### norenewalexppenalty

**Description:** Disables renewal experience penalty due to level difference.

**Example:**
```c
prt_fild08	mapflag	norenewalexppenalty
```

**Use Case:** Training maps, allow high-level farming, balanced exp gain.

---

### nopetcapture

**Description:** Disables ability to capture pets on the map.

**Example:**
```c
pvp_n_1-1	mapflag	nopetcapture
```

**Use Case:** PvP maps, boss maps, special areas.

---

### nobank

**Description:** Disables Bank system on the map.

**Example:**
```c
pvp_n_1-1	mapflag	nobank
```

**Use Case:** Restricted areas, prevent banking exploits.

---

### norodex

**Description:** Disables RODex (mail system) on the map.

**Example:**
```c
pvp_n_1-1	mapflag	norodex
```

**Use Case:** Event maps, prevent mail abuse, focus gameplay.

---

## 2. BATTLE-RELATED

### pvp / pvp_noparty / pvp_noguild / pvp_nocalcrank

**Description:** Enables Player vs. Player mode with damage adjustments.

- `pvp`: Standard PvP mode
- `pvp_noparty`: Ignore party alliances (can hit party members)
- `pvp_noguild`: Ignore guild alliances (can hit guild members)
- `pvp_nocalcrank`: Disable PvP ranking calculation

**Examples:**
```c
// Standard PvP
pvp_y_1-1	mapflag	pvp

// Free-for-all (ignore party)
pvp_n_1-1	mapflag	pvp
pvp_n_1-1	mapflag	pvp_noparty

// Full FFA (ignore party and guild)
pvp_n_2-2	mapflag	pvp
pvp_n_2-2	mapflag	pvp_noparty
pvp_n_2-2	mapflag	pvp_noguild

// PvP without ranking
pvp_y_2-2	mapflag	pvp
pvp_y_2-2	mapflag	pvp_nocalcrank
```

**Use Case:** PvP arenas, deathmatch areas, team battles, ranked matches.

---

### pvp_nightmaredrop <id>,<type>,<rate>

**Description:** Causes players to drop items upon death.

**Parameters:**
- `<id>`: Item ID or "random"
- `<type>`: "inventory", "equip", or "all"
- `<rate>`: Drop chance (10000 = 100%)

**Examples:**
```c
// Drop random item from inventory (50% chance)
pvp_n_1-1	mapflag	pvp_nightmaredrop	random,inventory,5000

// Drop specific item (100% chance)
pvp_n_1-1	mapflag	pvp_nightmaredrop	501,inventory,10000

// Drop random equipment (10% chance)
pvp_n_1-1	mapflag	pvp_nightmaredrop	random,equip,1000

// Drop anything (25% chance)
pvp_n_1-1	mapflag	pvp_nightmaredrop	random,all,2500
```

**Use Case:** Hardcore PvP, high-risk areas, unique game modes.

**Note:** Does NOT require PvP mapflag to be set (works anywhere).

---

### gvg / gvg_noparty / gvg_castle / gvg_dungeon / gvg_te / gvg_te_castle

**Description:** Enables Guild vs. Guild mode with damage adjustments.

- `gvg`: Standard GvG mode
- `gvg_noparty`: Ignore party alliances
- `gvg_castle`: Guild castle (GvG only active during WoE)
- `gvg_dungeon`: Guild dungeon (warp out after 2 deaths)
- `gvg_te`: WOE:TE area
- `gvg_te_castle`: WOE:TE castle (special restrictions)

**Examples:**
```c
// Standard GvG
guild_vs1	mapflag	gvg

// WoE Castle
prtg_cas01	mapflag	gvg_castle

// Guild Dungeon
gld_dun01	mapflag	gvg_dungeon

// WoE:TE
te_prtcas01	mapflag	gvg_te
te_prtcas01	mapflag	gvg_te_castle
```

**Use Case:** War of Emperium, guild wars, guild dungeons, competitive guild content.

---

### battleground {<type>}

**Description:** Enables Battlegrounds mode with damage adjustments.

**Parameters:**
- `1` (default): Nothing
- `2`: Show scoreboard

**Examples:**
```c
// Basic BG
bat_c01	mapflag	battleground

// BG with scoreboard
bat_c02	mapflag	battleground	2
```

**Use Case:** Battleground arenas, team-based competitive content.

---

### partylock / guildlock

**Description:** Prevents alteration of parties/guilds on the map.

**Blocks:**
- Creating
- Leaving
- Inviting
- Expelling
- Breaking
- Changing leaders

**Notes:**
- `partylock`: Still allows changing party options
- `guildlock`: Also blocks guild alliance changes

**Examples:**
```c
// Lock party changes
pvp_n_1-1	mapflag	partylock

// Lock guild changes
guild_vs1	mapflag	guildlock
```

**Use Case:** Competitive events, prevent team switching mid-match, tournament fairness.

---

### skill_damage {<skill_name>,<caster>,<SKILLDMG_PC>,{<SKILLDMG_MOB>,{<SKILLDMG_BOSS>,{<SKILLDMG_OTHER>}}}}

**Description:** Adjusts skill damage on the map.

**Parameters:**
- `skill_name`: Skill name from skill_db.yml (or "all" for all skills)
- `caster`: Caster type(s) - bitmask
  - `BL_PC` = Player
  - `BL_MOB` = Monster
  - `BL_PET` = Pet
  - `BL_HOM` = Homunculus
  - `BL_MER` = Mercenary
  - `BL_ELEM` = Elemental
- `damage`: Percent adjustment (-100 to 100000)
  - `SKILLDMG_PC` = against player
  - `SKILLDMG_MOB` = against normal monster
  - `SKILLDMG_BOSS` = against boss monster
  - `SKILLDMG_OTHER` = against other (hom/merc/pet/elem)

**Note:** Can also use `db/skill_damage_db.txt` for Map type 16.

**Examples:**
```c
// Reduce all player skill damage by 50% in PvP
pvp_n_1-1	mapflag	skill_damage	all,BL_PC,50

// Increase Bash damage against players by 200%
pvp_n_1-1	mapflag	skill_damage	SM_BASH,BL_PC,200

// Disable all damage to monsters
prt_fild08	mapflag	skill_damage	all,BL_MOB,0
```

**Use Case:** PvP balance, custom damage rules, skill adjustments, unique game modes.

---

### skill_duration <skill_name>,<percentage>

**Description:** Sets trap-type skill duration to percentage of original.

**Example:**
```c
// Makes HT_ANKLESNARE last 4x longer
prtg_cas01	mapflag	skill_duration	HT_ANKLESNARE,400

// Makes all traps last half as long
pvp_n_1-1	mapflag	skill_duration	all,50
```

**Use Case:** Balance trap skills, WoE adjustments, custom gameplay.

---

### invincible_time <duration>

**Description:** Sets invincibility duration (in ms) when player loads onto map.

**Cancelled By:**
- Player walking
- Player interacting (any action)

**Default:** Uses `player_invincible_time` from `/conf/battle/player.conf` if not specified.

**Example:**
```c
// 5 seconds invincibility on spawn
pvp_n_1-1	mapflag	invincible_time	5000

// 10 seconds invincibility
guild_vs1	mapflag	invincible_time	10000
```

**Use Case:** Prevent spawn camping, fair respawn, give players time to orient.

---

## 3. MAP EFFECTS

### Weather Effects

**Available Effects:**
- `clouds` - Cloudy sky
- `clouds2` - Darker clouds
- `fireworks` - Fireworks display
- `fog` - Foggy atmosphere
- `leaves` - Falling leaves
- `sakura` - Falling cherry blossoms
- `snow` - Snowfall

**Examples:**
```c
prontera	mapflag	sakura
lutie	mapflag	snow
morocc	mapflag	fog
```

**Use Case:** Atmosphere, seasonal events, aesthetic enhancement, immersion.

---

### nightenabled

**Description:** Displays night mode effects on the map.

**Example:**
```c
prt_fild08	mapflag	nightenabled
```

**Use Case:** Most outdoor maps, day/night cycle, atmosphere.

**Note:** Used on most outdoor maps by default.

---

## 4. MISCELLANEOUS

### town

**Description:** Marks map as a town.

**Effects:**
- Allows mail access
- Disables kill stealing

**Example:**
```c
prontera	mapflag	town
```

**Use Case:** Major cities, safe zones, social hubs.

---

### reset

**Description:** Allows usage of Neuralizer (ID 12213).

**Example:**
```c
prontera	mapflag	reset
```

**Use Case:** Stat/skill reset areas, convenience zones.

---

### bexp <rate> / jexp <rate>

**Description:** Changes base/job experience rates on the map.

**Parameters:**
- `<rate>`: Percentage (100 = 1x, 200 = 2x, 50 = 0.5x)
- Supports negative values to reduce EXP
- Takes into account `base_exp_rate` and `job_exp_rate` from `/conf/battle/exp.conf`

**Examples:**
```c
// Double base exp
prt_fild08	mapflag	bexp	200

// Triple job exp
pay_fild01	mapflag	jexp	300

// Half base exp
gef_dun00	mapflag	bexp	50

// No base exp (alternative to nobaseexp)
pvp_n_1-1	mapflag	bexp	0
```

**Use Case:** Training areas, bonus zones, event maps, penalty areas.

---

### loadevent

**Description:** Triggers label "OnPCLoadMapEvent" when players enter the map.

**Triggered By:**
- Entering the map
- Teleporting within the map

**Example:**
```c
prontera	mapflag	loadevent
```

**Script Example:**
```c
-	script	LoadEventExample	-1,{
OnPCLoadMapEvent:
    if (strcharinfo(3) == "prontera") {
        mes "Welcome to Prontera!";
        close;
    }
    end;
}
```

**Use Case:** Welcome messages, buff application, entrance checks, custom events.

**See Also:** `/doc/script_commands.txt` for more details.

---

### allowks

**Description:** Allows kill stealing on the map (renders `@noks` command useless).

**Example:**
```c
prt_fild08	mapflag	allowks
```

**Use Case:** Free-for-all farming, competitive areas, no kill steal protection.

---

### autotrade

**Description:** Allows `@autotrade` command on the map.

**Requirements:**
- Only applies if `at_mapflag` enabled in `/conf/battle/misc.conf`
- Otherwise, @autotrade enabled on all maps by default

**Example:**
```c
prontera	mapflag	autotrade
```

**Use Case:** Designated vending areas, market zones.

---

### hidemobhpbar

**Description:** Hides monster HP bar on the map.

**Example:**
```c
boss_map	mapflag	hidemobhpbar
```

**Use Case:** Aesthetic preference, mystery boss fights, cleaner visuals.

**Note:** Ignores `monster_hp_bars_info` config value.

---

### specialpopup <popup_id>

**Description:** Displays special popup when player enters the map.

**Example:**
```c
prontera	mapflag	specialpopup	1
```

**Use Case:** Announcements, warnings, information displays.

**See Also:** Script command "specialpopup" for popup types.

---

## SCRIPT COMMANDS

### setmapflag("<map_name>", <mapflag>{, <value>})

**Description:** Sets a mapflag on a map dynamically.

**Examples:**
```c
// Enable PvP
setmapflag("prontera", mf_pvp);

// Set nosave
setmapflag("prontera", mf_nosave, "SavePoint");

// Set bexp to 200%
setmapflag("prt_fild08", mf_bexp, 200);
```

---

### removemapflag("<map_name>", <mapflag>)

**Description:** Removes a mapflag from a map dynamically.

**Example:**
```c
// Disable PvP
removemapflag("prontera", mf_pvp);

// Remove noteleport
removemapflag("guild_vs1", mf_noteleport);
```

---

### getmapflag("<map_name>", <mapflag>)

**Description:** Checks if a mapflag is set on a map.

**Returns:** 1 if set, 0 if not set.

**Example:**
```c
if (getmapflag("prontera", mf_pvp)) {
    mes "This is a PvP map!";
} else {
    mes "This is not a PvP map.";
}
```

---

## MAPFLAG CONSTANTS

Use these constants in scripts:

```c
mf_nomemo, mf_noteleport, mf_nosave, mf_nobranch, mf_noexppenalty, mf_nozenypenalty,
mf_notrade, mf_noskill, mf_nowarp, mf_partylock, mf_noicewall, mf_snow, mf_fog,
mf_sakura, mf_leaves, mf_clouds, mf_clouds2, mf_fireworks, mf_gvg_castle, mf_gvg,
mf_pvp, mf_pvp_noparty, mf_pvp_noguild, mf_loadevent, mf_nochat, mf_noexppenalty,
mf_noreturn, mf_nogo, mf_nomemo, mf_pvp_nocalcrank, mf_gvg_te, mf_gvg_te_castle,
mf_battleground, mf_reset, mf_guildlock, mf_town, mf_autotrade, mf_allowks,
mf_monster_noteleport, mf_pvp_nightmaredrop, mf_restricted, mf_nocommand,
mf_nodrop, mf_jexp, mf_bexp, mf_novending, mf_nopenalty, mf_gvg_noparty,
mf_noexppenalty, mf_nozenypenalty, mf_nightenabled, mf_nobaseexp, mf_nojobexp,
mf_nomobloot, mf_nomvploot, mf_noreturn, mf_nowarpto, mf_nightmaredrop,
mf_noexp, mf_noitemconsumption, mf_nosunmoonstarmiracle, mf_nomapchannelautojoin,
mf_nousecart, mf_nolockon, mf_notomb, mf_nocostume, mf_norenewaldroppenalty,
mf_norenewalexppenalty, mf_noloot, mf_nopetcapture, mf_nobuyingstore,
mf_skill_damage, mf_skill_duration, mf_invincible_time, mf_nobank, mf_norodex,
mf_hidemobhpbar, mf_specialpopup
```

---

## COMMON MAPFLAG COMBINATIONS

### PvP Arena (Fair)
```c
pvp_n_1-1	mapflag	pvp
pvp_n_1-1	mapflag	pvp_noparty
pvp_n_1-1	mapflag	pvp_noguild
pvp_n_1-1	mapflag	noteleport
pvp_n_1-1	mapflag	nowarp
pvp_n_1-1	mapflag	nopenalty
pvp_n_1-1	mapflag	nosave	SavePoint
pvp_n_1-1	mapflag	invincible_time	5000
```

### WoE Castle
```c
prtg_cas01	mapflag	gvg_castle
prtg_cas01	mapflag	noteleport
prtg_cas01	mapflag	nowarp
prtg_cas01	mapflag	noreturn
prtg_cas01	mapflag	nobranch
prtg_cas01	mapflag	nomemo
prtg_cas01	mapflag	nosave	SavePoint
prtg_cas01	mapflag	skill_duration	HT_ANKLESNARE,400
```

### Town (Safe Zone)
```c
prontera	mapflag	town
prontera	mapflag	nomemo
prontera	mapflag	nobranch
prontera	mapflag	noteleport
prontera	mapflag	novending
prontera	mapflag	nobuyingstore
prontera	mapflag	nodrop
```

### Training Area (High EXP)
```c
prt_fild08	mapflag	bexp	300
prt_fild08	mapflag	jexp	300
prt_fild08	mapflag	nopenalty
prt_fild08	mapflag	norenewaldroppenalty
prt_fild08	mapflag	norenewalexppenalty
```

### Boss Map
```c
boss_map	mapflag	nomemo
boss_map	mapflag	noteleport
boss_map	mapflag	nobranch
boss_map	mapflag	monster_noteleport
boss_map	mapflag	notomb
boss_map	mapflag	hidemobhpbar
```

---

## BEST PRACTICES

1. **Test Thoroughly:** Always test mapflag combinations in development environment
2. **Document Changes:** Comment your mapflag configurations
3. **Consistency:** Use similar mapflag sets for similar map types
4. **Performance:** Use `forcemineffect` on busy/laggy maps
5. **Balance:** Consider player experience when setting restrictions
6. **Security:** Use `restricted` zones for competitive/balanced areas
7. **Organization:** Keep mapflag configs organized in `/npc/mapflag/` directory

---

## TROUBLESHOOTING

**Problem:** Players can still teleport despite noteleport
- **Solution:** Check for GM permissions (any_warp), items with special flags

**Problem:** Mapflags not applying
- **Solution:** Reload scripts with `@reloadscript`, check syntax, verify map name

**Problem:** PvP damage seems wrong
- **Solution:** Check battle config files, verify pvp mapflag set, check skill_damage adjustments

**Problem:** Players respawn in wrong location with nosave
- **Solution:** Verify map name spelling, check coordinates, ensure SavePoint is capitalized

---

## RELATED FILES

- `/npc/mapflag/` - Mapflag configuration scripts
- `/conf/battle/` - Battle configuration files
- `/doc/script_commands.txt` - Script command reference
- `/db/(pre-)re/skill_nocast_db.txt` - Restricted zones skill config
- `/db/(pre-)re/item_noequip.txt` - Restricted zones item config

---

## SEE ALSO

- **KB_CMD_010:** Map Script Commands
- **KB_CONF_003:** Battle Configuration
- **KB_EXAMPLE_003:** Mapflag Usage Examples

---

*Last Updated: 2013-08-30*
*rAthena Documentation*
---
kb_id: KB_REF_010
kb_type: reference
kb_category: scripting
kb_subcategory: npc_examples
kb_keywords: [npc examples, script examples, code patterns, quest scripts, shop scripts, buffer npc, warp npc, monster spawner, timer, array, function, common patterns]
kb_related: [KB_REF_005, KB_REF_002, KB_REF_003]
kb_difficulty: beginner
kb_version: rAthena_2025
kb_last_updated: 2025-10-23
kb_use_case: [npc_scripting, quest_creation, learning, templates]
---

# rAthena NPC Script Examples

Collection of working NPC script examples and common patterns.

## Overview

This document provides ready-to-use NPC script examples for common scenarios. Copy, modify, and learn from these patterns.

**File Location:** Save scripts in `/npc/custom/` directory
**Load In:** `/npc/scripts_custom.conf`

---

## TABLE OF CONTENTS

1. [Basic NPCs](#1-basic-npcs)
2. [Quest NPCs](#2-quest-npcs)
3. [Shop NPCs](#3-shop-npcs)
4. [Buffer NPCs](#4-buffer-npcs)
5. [Warper NPCs](#5-warper-npcs)
6. [Monster Spawners](#6-monster-spawners)
7. [Timers & Events](#7-timers--events)
8. [Advanced Patterns](#8-advanced-patterns)

---

## 1. BASIC NPCS

### Simple Dialogue NPC
```c
prontera,150,150,4	script	Greeter	4_F_KAFRA1,{
    mes "[Greeter]";
    mes "Hello, " + strcharinfo(0) + "!";
    mes "Welcome to our server!";
    close;
}
```

---

### NPC with Menu
```c
prontera,151,150,4	script	Helper	4_M_JOB_KNIGHT1,{
    mes "[Helper]";
    mes "How can I help you?";
    next;
    switch(select("Heal Me:Buff Me:Information:Cancel")) {
    case 1:
        percentheal 100,100;
        mes "Healed!";
        close;
    case 2:
        sc_start SC_BLESSING,240000,10;
        sc_start SC_INCREASEAGI,240000,10;
        mes "Buffed!";
        close;
    case 3:
        mes "This is a helper NPC.";
        mes "We can heal and buff you!";
        close;
    case 4:
        close;
    }
}
```

---

### NPC with Input
```c
prontera,152,150,4	script	Name Teller	4_F_TELEPORTER,{
    mes "[Name Teller]";
    mes "What's your name?";
    next;
    input .@name$;

    mes "[Name Teller]";
    if (.@name$ == "") {
        mes "You didn't enter a name!";
    } else {
        mes "Nice to meet you, " + .@name$ + "!";
    }
    close;
}
```

---

## 2. QUEST NPCS

### Simple Quest (Item Collection)
```c
prontera,153,150,4	script	Quest Giver	4_M_ALCHE_C,{
    mes "[Quest Giver]";

    // Check if quest already completed
    if (#PORING_QUEST) {
        mes "Thanks for helping before!";
        close;
    }

    // Check if player has items
    if (countitem(909) >= 10) {  // 10 Jellopy
        mes "You brought the Jellopy!";
        mes "Here's your reward.";
        delitem 909,10;
        getexp 1000,500;
        getitem 501,5;  // 5 Red Potions
        set #PORING_QUEST,1;
        close;
    }

    // Give quest
    mes "Can you bring me 10 Jellopy?";
    mes "I'll reward you well!";
    close;
}
```

---

### Hunt Quest (with quest_db)
```c
prontera,154,150,4	script	Hunt Quest	4_M_KNIGHT_GOLD,{
    .@quest_id = 1000;  // Quest ID from quest_db.yml

    mes "[Hunt Quest]";

    // Check quest status
    .@status = questprogress(.@quest_id, HUNTING);

    if (.@status == 0) {
        // Quest not started
        mes "Hunt 30 Porings for me!";
        next;
        if (select("Accept:Decline") == 2) close;
        setquest .@quest_id;
        mes "Good luck!";
        close;
    } else if (.@status == 1) {
        // Quest active but not complete
        mes "Keep hunting! You're not done yet.";
        close;
    } else if (.@status == 2) {
        // Quest complete
        mes "You finished! Here's your reward.";
        completequest .@quest_id;
        getexp 5000,2000;
        getitem 501,10;
        close;
    }
}
```

---

### Daily Quest (Time-based)
```c
prontera,155,150,4	script	Daily Quest	4_F_ALCHE,{
    mes "[Daily Quest]";

    // Check if already done today
    if (#DAILY_DONE >= gettimetick(1)) {
        .@hours = ((#DAILY_DONE - gettimetick(1)) / 3600);
        mes "Come back in " + .@hours + " hours!";
        close;
    }

    // Check items
    if (countitem(501) >= 20) {  // 20 Red Potions
        mes "Thanks! Come back tomorrow!";
        delitem 501,20;
        getexp 10000,5000;
        set #DAILY_DONE, gettimetick(1) + 86400;  // 24 hours
        close;
    }

    mes "Bring me 20 Red Potions!";
    mes "Resets daily.";
    close;
}
```

---

## 3. SHOP NPCS

### Basic Shop
```c
prontera,156,150,4	shop	Potion Shop	4_F_01,501:50,502:200,503:500
```

---

### Custom Shop (Script-based)
```c
prontera,157,150,4	script	Custom Shop	4_M_ORIENT02,{
    mes "[Custom Shop]";
    mes "What do you need?";
    next;

    switch(select("Red Potion - 50z:Blue Potion - 200z:White Potion - 500z:Cancel")) {
    case 1:
        if (Zeny < 50) {
            mes "Not enough Zeny!";
            close;
        }
        Zeny -= 50;
        getitem 501,1;
        mes "Here's your Red Potion!";
        close;
    case 2:
        if (Zeny < 200) {
            mes "Not enough Zeny!";
            close;
        }
        Zeny -= 200;
        getitem 505,1;
        mes "Here's your Blue Potion!";
        close;
    case 3:
        if (Zeny < 500) {
            mes "Not enough Zeny!";
            close;
        }
        Zeny -= 500;
        getitem 504,1;
        mes "Here's your White Potion!";
        close;
    case 4:
        close;
    }
}
```

---

### Level-based Shop
```c
prontera,158,150,4	script	VIP Shop	4_M_SAGE_C,{
    mes "[VIP Shop]";

    if (BaseLevel < 50) {
        mes "Sorry, level 50+ only!";
        close;
    }

    mes "Welcome, high-level adventurer!";
    next;
    callshop "vip_items",1;
    npcshopattach "vip_items";
    end;

OnBuyItem:
    // Custom buy logic here
    end;

OnSellItem:
    // Custom sell logic here
    end;
}

-	shop	vip_items	-1,501:25,502:100,503:250
```

---

## 4. BUFFER NPCS

### Basic Buffer
```c
prontera,159,150,4	script	Buffer	4_F_KAFRA1,{
    mes "[Buffer]";
    mes "Free buffs!";
    next;

    sc_start SC_BLESSING,240000,10;
    sc_start SC_INCREASEAGI,240000,10;
    sc_start SC_IMPOSITIO,240000,5;
    sc_start SC_GLORIA,240000,1;

    specialeffect2 EF_BLESSING;

    mes "Buffed!";
    close;
}
```

---

### Menu-based Buffer
```c
prontera,160,150,4	script	Advanced Buffer	4_F_KAFRA2,{
    mes "[Advanced Buffer]";
    mes "Choose your buffs:";
    next;

    setarray .@buffs$[0],
        "Blessing (+STR/INT/DEX)",
        "Increase AGI (+AGI/Speed)",
        "Impositio (+ATK)",
        "Gloria (+LUK)",
        "Kyrie Eleison (Barrier)",
        "Magnificat (SP Regen)",
        "All Buffs",
        "Cancel";

    .@choice = select(implode(.@buffs$,":")) - 1;

    switch (.@choice) {
    case 0:
        sc_start SC_BLESSING,240000,10;
        break;
    case 1:
        sc_start SC_INCREASEAGI,240000,10;
        break;
    case 2:
        sc_start SC_IMPOSITIO,240000,5;
        break;
    case 3:
        sc_start SC_GLORIA,240000,1;
        break;
    case 4:
        sc_start SC_KYRIE,120000,10;
        break;
    case 5:
        sc_start SC_MAGNIFICAT,30000,1;
        break;
    case 6:
        sc_start SC_BLESSING,240000,10;
        sc_start SC_INCREASEAGI,240000,10;
        sc_start SC_IMPOSITIO,240000,5;
        sc_start SC_GLORIA,240000,1;
        sc_start SC_KYRIE,120000,10;
        sc_start SC_MAGNIFICAT,30000,1;
        break;
    case 7:
        close;
    }

    specialeffect2 EF_BLESSING;
    mes "Buff applied!";
    close;
}
```

---

## 5. WARPER NPCS

### Basic Warper
```c
prontera,161,150,4	script	Warper	4_M_TELEPORTER,{
    mes "[Warper]";
    mes "Where do you want to go?";
    next;

    switch(select("Prontera:Geffen:Payon:Morocc:Cancel")) {
    case 1:
        warp "prontera",156,191;
        end;
    case 2:
        warp "geffen",120,100;
        end;
    case 3:
        warp "payon",152,75;
        end;
    case 4:
        warp "morocc",156,93;
        end;
    case 5:
        close;
    }
}
```

---

### Categorized Warper
```c
prontera,162,150,4	script	Advanced Warper	4_M_TELEPORTER,{
    mes "[Advanced Warper]";
    mes "Select category:";
    next;

    switch(select("Cities:Dungeons:Fields:Cancel")) {
    case 1:  // Cities
        mes "[Warper]";
        mes "Which city?";
        next;
        switch(select("Prontera:Geffen:Payon:Morocc:Aldebaran:Back")) {
        case 1: warp "prontera",156,191; end;
        case 2: warp "geffen",120,100; end;
        case 3: warp "payon",152,75; end;
        case 4: warp "morocc",156,93; end;
        case 5: warp "aldebaran",140,131; end;
        case 6: close;
        }

    case 2:  // Dungeons
        mes "[Warper]";
        mes "Which dungeon?";
        next;
        switch(select("Prontera Culvert:Geffen Dungeon:Payon Cave:Back")) {
        case 1: warp "prt_sewb1",131,247; end;
        case 2: warp "gef_dun00",104,99; end;
        case 3: warp "pay_dun00",21,183; end;
        case 4: close;
        }

    case 3:  // Fields
        mes "[Warper]";
        mes "Which field?";
        next;
        switch(select("Prontera Field:Geffen Field:Payon Forest:Back")) {
        case 1: warp "prt_fild08",170,371; end;
        case 2: warp "gef_fild00",46,199; end;
        case 3: warp "pay_fild01",151,171; end;
        case 4: close;
        }

    case 4:
        close;
    }
}
```

---

## 6. MONSTER SPAWNERS

### Simple Spawner
```c
prontera,163,150,4	script	Spawn Poring	4_M_KID1,{
    mes "[Spawner]";
    mes "Spawn 5 Porings?";
    next;
    if (select("Yes:No") == 2) close;

    monster "prontera",0,0,"Poring",1002,5,"Spawner::OnPoringKilled";
    mes "Spawned!";
    close;

OnPoringKilled:
    announce "A Poring was killed!",bc_map;
    end;
}
```

---

### Timed Spawner
```c
-	script	AutoSpawner	-1,{
OnInit:
    // Spawn every 10 seconds
    initnpctimer;
    end;

OnTimer10000:
    monster "prontera",0,0,"Poring",1002,10;
    initnpctimer;  // Restart timer
    end;
}
```

---

### Wave Spawner
```c
prontera,164,150,4	script	Wave Event	4_M_MANAGER,{
    mes "[Wave Event]";
    mes "Start monster waves?";
    next;
    if (select("Yes:No") == 2) close;

    donpcevent "WaveController::OnWave1";
    mes "Wave 1 starting!";
    close;
}

-	script	WaveController	-1,{
OnWave1:
    announce "Wave 1: 10 Porings!",bc_map;
    monster "prontera",0,0,"Poring",1002,10,"WaveController::OnWave1Clear";
    end;

OnWave1Clear:
    if (mobcount("prontera","WaveController::OnWave1Clear") == 0) {
        sleep 3000;
        announce "Wave 2: 15 Drops!",bc_map;
        monster "prontera",0,0,"Drops",1113,15,"WaveController::OnWave2Clear";
    }
    end;

OnWave2Clear:
    if (mobcount("prontera","WaveController::OnWave2Clear") == 0) {
        announce "All waves complete!",bc_map;
        announce "Rewards distributed!",bc_map;
    }
    end;
}
```

---

## 7. TIMERS & EVENTS

### Announcement Timer
```c
-	script	HourlyAnnounce	-1,{
OnInit:
    initnpctimer;
    end;

OnTimer3600000:  // Every hour (3600000ms)
    announce "Server is running smoothly!",bc_all;
    initnpctimer;
    end;
}
```

---

### Event Scheduler
```c
-	script	EventScheduler	-1,{
OnClock2000:  // 8:00 PM
    announce "PvP Event starting in 5 minutes!",bc_all;
    sleep 300000;  // 5 minutes
    announce "PvP Event started!",bc_all;
    setmapflag "pvp_n_1-1",mf_pvp;
    end;

OnClock2100:  // 9:00 PM
    announce "PvP Event ended!",bc_all;
    removemapflag "pvp_n_1-1",mf_pvp;
    end;
}
```

---

### Login Reward
```c
-	script	LoginReward	-1,{
OnPCLoginEvent:
    // Check if already claimed today
    if (#LAST_LOGIN >= gettimetick(1)) end;

    announce "Welcome back! Daily reward claimed!",bc_self;
    getitem 501,10;  // 10 Red Potions
    set #LAST_LOGIN, gettimetick(1) + 86400;  // Next day
    end;
}
```

---

## 8. ADVANCED PATTERNS

### Function Usage
```c
function	script	GiveReward	{
    .@reward_exp = getarg(0);
    .@reward_zeny = getarg(1);

    getexp .@reward_exp,(.@reward_exp/2);
    Zeny += .@reward_zeny;

    mes "Received:";
    mes "- " + .@reward_exp + " Base EXP";
    mes "- " + (.@reward_exp/2) + " Job EXP";
    mes "- " + .@reward_zeny + " Zeny";
    return;
}

prontera,165,150,4	script	Reward NPC	4_M_ALCHE_C,{
    mes "[Reward NPC]";
    mes "Here's your reward!";
    next;

    callfunc("GiveReward",1000,500);
    close;
}
```

---

### Array Loop Example
```c
prontera,166,150,4	script	Item Giver	4_F_ALCHE,{
    mes "[Item Giver]";
    mes "Starter pack!";
    next;

    // Array of items
    setarray .@items[0],501,502,503,504,505;
    setarray .@amounts[0],10,10,5,5,3;

    for (.@i = 0; .@i < getarraysize(.@items); .@i++) {
        getitem .@items[.@i], .@amounts[.@i];
        mes "- " + getitemname(.@items[.@i]) + " x" + .@amounts[.@i];
    }
    close;
}
```

---

### Variable NPC (Changes based on server variable)
```c
prontera,167,150,4	script	Event Status	4_BOARD3,{
    mes "[Event Status]";

    if ($EVENT_ACTIVE) {
        mes "^00FF00Event is ACTIVE!^000000";
        mes "Bonus EXP: ^FF0000+" + $EVENT_BONUS + "%^000000";
    } else {
        mes "^FF0000No event active.^000000";
    }
    close;
}

prontera,168,150,4	script	Event Controller	4_M_MANAGER,{
    mes "[Event Controller]";
    mes "Control event status?";
    next;

    if (getgmlevel() < 90) {
        mes "GM only!";
        close;
    }

    switch(select("Start Event:Stop Event:Set Bonus")) {
    case 1:
        set $EVENT_ACTIVE,1;
        announce "Server Event Started! +" + $EVENT_BONUS + "% EXP!",bc_all;
        close;
    case 2:
        set $EVENT_ACTIVE,0;
        announce "Server Event Ended!",bc_all;
        close;
    case 3:
        mes "Enter bonus % (1-500):";
        input .@bonus,1,500;
        set $EVENT_BONUS,.@bonus;
        mes "Bonus set to " + .@bonus + "%!";
        close;
    }
}
```

---

### Instance Dungeon Entrance
```c
prontera,169,150,4	script	Instance Entrance	4_M_ALCHE_D,{
    .@instance$ = "MyInstance";
    .@instance_id = instance_id(IM_PARTY);

    mes "[Instance Entrance]";

    // Check if party leader
    if (getpartyleader(getcharid(1),2) != getcharid(0)) {
        mes "Only party leader can create instance.";
        close;
    }

    // Check if instance exists
    if (.@instance_id < 0) {
        mes "Create instance?";
        next;
        if (select("Yes:No") == 2) close;

        .@instance_id = instance_create(.@instance$,getcharid(1),IM_PARTY);
        if (.@instance_id < 0) {
            mes "Failed to create instance!";
            close;
        }

        if (instance_attachmap("1@tower",.@instance_id) == "") {
            mes "Failed to attach map!";
            instance_destroy(.@instance_id);
            close;
        }

        instance_init(.@instance_id);
        mes "Instance created!";
        close;
    }

    // Warp to instance
    mes "Enter instance?";
    next;
    if (select("Yes:No") == 2) close;

    warp instance_mapname("1@tower",.@instance_id),100,100;
    end;
}
```

---

## TIPS & BEST PRACTICES

1. **Always test scripts** before deploying to live server
2. **Use comments** to document complex logic
3. **Follow naming conventions** - Meaningful NPC names
4. **Check requirements** - Level, quest, items before giving rewards
5. **Validate input** - Use min/max in input commands
6. **Use arrays** for multiple similar items
7. **Add visual effects** for better player experience
8. **Handle edge cases** - What if player disconnects?
9. **Use functions** for repeated code
10. **Test with multiple players** for race conditions

---

## DEBUGGING NPCS

```c
// Add debug messages
dispbottom "Debug: Variable = " + .@var;
debugmes "Server debug: " + .@var;

// Check NPC status
@npctalk Test message  // Make NPC say something

// Reload scripts
@reloadscript  // Reload all scripts
```

---

## SEE ALSO

- **KB_REF_005:** Script Commands Reference
- **KB_REF_002:** Quest System
- **KB_REF_006:** Status Effects Reference
- **Sample Scripts:** `/doc/sample/` directory

---

*Last Updated: 2025-10-23*
*rAthena Documentation - NPC Script Examples*
---
kb_id: KB_REF_001
kb_type: reference
kb_category: permissions
kb_subcategory: player_groups
kb_keywords: [permissions, groups, access control, player rights, admin, command access, PC_PERM, groups.conf, can_trade, all_commands, bypass, security]
kb_related: [KB_CONF_002]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2024-04-14
kb_use_case: [server_configuration, admin_setup, permission_management]
---

# rAthena Permission System Reference

Complete reference for player group permissions configured in `/conf/groups.conf`.

## Overview

Permissions control what players in specific groups can and cannot do on your server. Each permission can be enabled or disabled for different player groups (e.g., normal players, moderators, administrators).

**Configuration Location:** `/conf/groups.conf`

**Format in groups.conf:**
```yaml
permissions:
  permission_name: true/false
```

**Constant Name Format:** Used in scripts and source code as `PC_PERM_CONSTANT_NAME`

---

## 1. BASIC PERMISSIONS

### can_trade (PC_PERM_TRADE)
**Description:** Allows player to distribute items through various means.
**Affects:**
- Trading with other players
- Dropping items on ground
- Vending (selling via shop)
- Storage access (put/get items)
- Mail system
- Any item distribution method

**Use Case:** Disable for trial accounts or restricted players to prevent item trading.

---

### can_party (PC_PERM_PARTY)
**Description:** Allows player to create and join parties.
**Affects:**
- Creating new parties
- Joining existing parties
- Party invitations

**Use Case:** Restrict party functionality for specific player groups.

---

### attendance (PC_PERM_ATTENDANCE)
**Description:** Allows player to use the daily attendance system.
**Affects:**
- Daily login rewards
- Attendance tracking

**Use Case:** Enable/disable daily reward system access.

---

## 2. EXTENDED PERMISSIONS

### all_skill (PC_PERM_ALL_SKILL)
**Description:** Grants player ALL available skills in their skill tree.
**Affects:**
- Automatically grants all skills
- Bypasses normal skill learning requirements

**Use Case:** Testing, GM characters, special events.

**Warning:** This is a powerful permission. Use carefully.

---

### all_equipment (PC_PERM_USE_ALL_EQUIPMENT)
**Description:** Allows player to equip ANY item regardless of requirements.
**Bypasses:**
- Class restrictions
- Level requirements
- Gender restrictions
- All equipment restrictions

**Use Case:** Testing, GM characters.

**Warning:** May cause client errors if sprite doesn't exist for the player's class.

---

### skill_unconditional (PC_PERM_SKILL_UNCONDITIONAL)
**Description:** Allows player to use ANY skill without meeting conditions.
**Bypasses:**
- SP cost requirements
- Item requirements (catalysts, ammunition)
- Cooldown times
- All skill usage conditions

**Use Case:** GM characters, testing, special events.

---

### join_chat (PC_PERM_JOIN_ALL_CHAT)
**Description:** Allows player to join password-protected chatrooms.
**Affects:**
- Can enter any chatroom without password

**Use Case:** Moderator oversight, GM monitoring.

---

### kick_chat (PC_PERM_NO_CHAT_KICK)
**Description:** Prevents player from being kicked from chatrooms.
**Affects:**
- Immunity to chatroom kicks

**Use Case:** GM/moderator protection.

---

### view_hpmeter (PC_PERM_VIEW_HPMETER)
**Description:** Allows player to see HP bar of EVERY player.
**Affects:**
- Can view all player HP bars
- Overrides individual player settings

**Use Case:** GM monitoring, debugging.

---

### view_equipment (PC_PERM_VIEW_EQUIPMENT)
**Description:** Allows player to view equipment of EVERY player.
**Bypasses:**
- Individual player privacy settings
- Equipment viewing restrictions

**Use Case:** GM inspection, player support.

---

### hack_info (PC_PERM_RECEIVE_HACK_INFO)
**Description:** Allows player to receive all information about hacking attempts.
**Receives:**
- Name spoofing attempts
- Hack attempt notifications
- Security breach alerts

**Use Case:** Security team, administrators.

---

### disable_pvm (PC_PERM_DISABLE_PVM)
**Description:** PREVENTS player from attacking monsters.
**Affects:**
- Cannot engage in PvM (Player vs Monster) combat

**Use Case:** Event NPCs, special restricted accounts, RP-only characters.

---

### disable_pvp (PC_PERM_DISABLE_PVP)
**Description:** PREVENTS player from attacking other players.
**Affects:**
- Cannot engage in PvP (Player vs Player) combat

**Use Case:** Protected accounts, non-combat roles, moderators observing.

---

### can_trade_bounded (PC_PERM_TRADE_BOUNDED)
**Description:** Allows player to perform normal item actions with bounded items.
**Enables:**
- Dropping bound items
- Selling bound items
- Trading bound items
- All item actions with bound items

**Use Case:** GM item management, special accounts.

**Note:** Bounded items are normally account/character-locked.

---

### item_unconditional (PC_PERM_ITEM_UNCONDITIONAL)
**Description:** Allows player to consume ANY consumable item without requirements.
**Bypasses:**
- noitemconsumption mapflag
- Item's class restrictions
- Gender restrictions
- Status change requirements
- Item delay/cooldown
- All consumption requirements

**Use Case:** Testing, GM characters, debugging.

---

### trade_unconditional (PC_PERM_TRADE_UNCONDITIONAL)
**Description:** Allows player to ignore ALL trade conditions of items.
**Bypasses:**
- No-drop restrictions
- No-trade restrictions
- No-sell restrictions
- Cart restrictions
- Storage/guild storage restrictions
- Mail restrictions
- Auction restrictions

**Use Case:** GM item management, special administrative tasks.

---

## 3. COMMAND-RELATED PERMISSIONS

### all_commands (PC_PERM_USE_ALL_COMMANDS)
**Description:** Allows usage of ALL atcommands and charcommands.
**Grants:**
- Full access to all @ commands
- Full access to all # commands

**Use Case:** Full administrators.

**Warning:** This is the highest privilege level.

---

### disable_commands_when_dead (PC_PERM_DISABLE_CMD_DEAD)
**Description:** DISABLES usage of atcommands when player is dead.
**Affects:**
- Cannot use commands while dead

**Use Case:** Enforce fair play, prevent abuse.

---

### hide_session (PC_PERM_HIDE_SESSION)
**Description:** Hides player session from being displayed by atcommands.
**Hides From:**
- @who command
- @whomap command
- @whogm command
- Other player-listing commands

**Use Case:** GM anonymity, undercover monitoring.

---

### who_display_aid (PC_PERM_WHO_DISPLAY_AID)
**Description:** Displays all GMs and character/account IDs in @who command.
**Shows:**
- All GM accounts (even hidden)
- Character IDs
- Account IDs

**Use Case:** Administrator oversight, debugging.

---

### any_warp (PC_PERM_WARP_ANYWHERE)
**Description:** Allows player to bypass warp-related mapflags.
**Bypasses:**
- nowarp mapflag
- nowarpto mapflag
- noteleport mapflag
- nomemo mapflag

**Affected Commands:**
- @memo
- @mapmove
- @go
- @jump
- @warp
- All warp commands

**Use Case:** GM mobility, administrative access.

---

### receive_requests (PC_PERM_RECEIVE_REQUESTS)
**Description:** Allows player to receive requests through @requests command.
**Affects:**
- Receives player requests/reports

**Use Case:** Support staff, moderators.

---

### show_bossmobs (PC_PERM_SHOW_BOSS)
**Description:** Displays boss mobs in @showmobs command.
**Shows:**
- MVP/boss locations
- Boss mob information

**Use Case:** GM hunting, event management, debugging.

---

### channel_admin (PC_PERM_CHANNEL_ADMIN)
**Description:** Allows player to modify #channel settings regardless of ownership.
**Grants:**
- Full channel administration
- Modify any channel settings
- Join password-protected channels without password
- Override channel ownership

**Use Case:** Chat moderators, administrators.

---

### use_check (PC_PERM_USE_CHECK)
**Description:** Allows player to use client command /check.
**Enables:**
- /check command (displays character status)

**Use Case:** GM inspection, debugging.

---

### use_changemaptype (PC_PERM_USE_CHANGEMAPTYPE)
**Description:** Allows player to use client command /changemaptype.
**Enables:**
- /changemaptype command

**Use Case:** Testing, special effects.

---

### command_enable (PC_PERM_ENABLE_COMMAND)
**Description:** Enable use of atcommands while talking with NPC.
**Allows:**
- Using @ commands during NPC dialogue

**Use Case:** GM convenience, debugging NPC scripts.

---

### bypass_stat_onclone (PC_PERM_BYPASS_STAT_ONCLONE)
**Description:** Bypass max parameter limit while using @clonestat.
**Bypasses:**
- Maximum stat limits when cloning stats

**Use Case:** GM testing, special events.

---

### bypass_max_stat (PC_PERM_BYPASS_MAX_STAT)
**Description:** Allows bypassing maximum stat parameter to absolute maximum (32,767).
**Bypasses:**
- conf/player.conf stat limits
- Normal stat caps

**Maximum Value:** 32,767

**Use Case:** Testing extreme cases, special characters.

**Warning:** Can severely imbalance gameplay.

---

### macro_detect (PC_PERM_MACRO_DETECT)
**Description:** Allows player to use client command /macro_detector.
**Enables:**
- /macro_detector command
- Bot detection tools

**Use Case:** GM bot hunting, anti-cheat operations.

---

### macro_register (PC_PERM_MACRO_REGISTER)
**Description:** Allows player to use captcha management commands.
**Enables:**
- /macro_register (add new captcha)
- /macro_preview (preview captcha by ID)

**Use Case:** Captcha system management, anti-bot configuration.

---

## QUICK REFERENCE TABLE

| Permission Name | Constant | Type | Purpose |
|----------------|----------|------|---------|
| can_trade | PC_PERM_TRADE | Basic | Allow item distribution |
| can_party | PC_PERM_PARTY | Basic | Allow party system |
| attendance | PC_PERM_ATTENDANCE | Basic | Allow daily attendance |
| all_skill | PC_PERM_ALL_SKILL | Extended | Grant all skills |
| all_equipment | PC_PERM_USE_ALL_EQUIPMENT | Extended | Equip any item |
| skill_unconditional | PC_PERM_SKILL_UNCONDITIONAL | Extended | Use skills without conditions |
| join_chat | PC_PERM_JOIN_ALL_CHAT | Extended | Join protected chatrooms |
| kick_chat | PC_PERM_NO_CHAT_KICK | Extended | Immune to chatroom kicks |
| view_hpmeter | PC_PERM_VIEW_HPMETER | Extended | See all player HP |
| view_equipment | PC_PERM_VIEW_EQUIPMENT | Extended | See all player equipment |
| hack_info | PC_PERM_RECEIVE_HACK_INFO | Extended | Receive hack alerts |
| disable_pvm | PC_PERM_DISABLE_PVM | Extended | Prevent PvM combat |
| disable_pvp | PC_PERM_DISABLE_PVP | Extended | Prevent PvP combat |
| can_trade_bounded | PC_PERM_TRADE_BOUNDED | Extended | Trade bound items |
| item_unconditional | PC_PERM_ITEM_UNCONDITIONAL | Extended | Use items unconditionally |
| trade_unconditional | PC_PERM_TRADE_UNCONDITIONAL | Extended | Ignore trade restrictions |
| all_commands | PC_PERM_USE_ALL_COMMANDS | Command | Use all commands |
| disable_commands_when_dead | PC_PERM_DISABLE_CMD_DEAD | Command | Disable commands when dead |
| hide_session | PC_PERM_HIDE_SESSION | Command | Hide from @who |
| who_display_aid | PC_PERM_WHO_DISPLAY_AID | Command | Show IDs in @who |
| any_warp | PC_PERM_WARP_ANYWHERE | Command | Bypass warp restrictions |
| receive_requests | PC_PERM_RECEIVE_REQUESTS | Command | Receive player requests |
| show_bossmobs | PC_PERM_SHOW_BOSS | Command | Show bosses in @showmobs |
| channel_admin | PC_PERM_CHANNEL_ADMIN | Command | Full channel control |
| use_check | PC_PERM_USE_CHECK | Command | Use /check command |
| use_changemaptype | PC_PERM_USE_CHANGEMAPTYPE | Command | Use /changemaptype |
| command_enable | PC_PERM_ENABLE_COMMAND | Command | Commands during NPC talk |
| bypass_stat_onclone | PC_PERM_BYPASS_STAT_ONCLONE | Command | Bypass @clonestat limits |
| bypass_max_stat | PC_PERM_BYPASS_MAX_STAT | Command | Max stat = 32,767 |
| macro_detect | PC_PERM_MACRO_DETECT | Command | Use /macro_detector |
| macro_register | PC_PERM_MACRO_REGISTER | Command | Manage captchas |

---

## USAGE EXAMPLES

### Example 1: Normal Player Group
```yaml
groups:
  - Name: Player
    Level: 0
    permissions:
      can_trade: true
      can_party: true
      attendance: true
```

### Example 2: Trial Account
```yaml
groups:
  - Name: Trial
    Level: 0
    permissions:
      can_trade: false        # Prevent trading
      can_party: true
      attendance: false
```

### Example 3: Moderator
```yaml
groups:
  - Name: Moderator
    Level: 50
    permissions:
      can_trade: true
      can_party: true
      view_hpmeter: true
      view_equipment: true
      hack_info: true
      receive_requests: true
      channel_admin: true
      hide_session: true
```

### Example 4: Administrator
```yaml
groups:
  - Name: Admin
    Level: 99
    permissions:
      all_commands: true
      any_warp: true
      skill_unconditional: true
      all_equipment: true
      bypass_max_stat: true
      view_hpmeter: true
      view_equipment: true
```

---

## BEST PRACTICES

1. **Least Privilege Principle:** Only grant permissions that are absolutely necessary
2. **Group Hierarchy:** Create multiple group levels (Player → Helper → Moderator → Admin)
3. **Testing:** Test permissions thoroughly in a development environment
4. **Documentation:** Document your custom group configurations
5. **Security:** Limit `all_commands` and `all_equipment` to trusted administrators only
6. **Monitoring:** Use `hack_info` and `receive_requests` for security team

---

## RELATED CONFIGURATION FILES

- `/conf/groups.yml` - Main permission configuration
- `/conf/atcommands.yml` - Command-specific permissions
- `/doc/atcommands.txt` - Available commands documentation

---

## SEE ALSO

- **KB_REF_002:** Admin Commands Reference
- **KB_CONF_001:** Configuration System Guide
- **KB_CONF_002:** Groups.yml Configuration

---

*Last Updated: 2024-04-14*
*rAthena Documentation*
---
kb_id: KB_REF_002
kb_type: reference
kb_category: database
kb_subcategory: quest_system
kb_keywords: [quest, quest_db, YAML, objectives, targets, drops, rewards, TimeLimit, mob kill, quest system, quest database]
kb_related: [KB_DB_001, KB_EXAMPLE_005]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2022-06-29
kb_use_case: [quest_creation, content_creation, quest_scripting]
---

# rAthena Quest Database Structure

Complete reference for the quest database structure in `/db/(pre-)re/quest_db.yml`.

## Overview

The quest database defines all quests available in rAthena, including their objectives, time limits, drop rates, and rewards. Quests are configured using YAML format.

**Database Location:** `/db/(pre-)re/quest_db.yml`

---

## QUEST STRUCTURE

### Basic Quest Format

```yaml
- Id: 1000
  Title: Quest Name
  TimeLimit: <optional>
  Targets: <optional>
  Drops: <optional>
```

---

## FIELD REFERENCE

### Id (Required)
**Type:** Integer
**Description:** Unique quest identifier

**Example:**
```yaml
- Id: 1000
  Title: Poring Hunt
```

**Notes:**
- Must be unique across all quests
- Used in script commands like `questprogress()`, `setquest()`, `completequest()`
- Standard range: User quests typically start from 1000+

---

### Title (Required)
**Type:** String
**Description:** Display name of the quest shown to players

**Example:**
```yaml
- Id: 1000
  Title: Hunt 10 Porings
```

**Notes:**
- Shown in quest log UI
- Can contain spaces and special characters
- Keep concise for UI readability

---

### TimeLimit (Optional)
**Type:** String
**Description:** Quest expiration time or duration

Quest time limits can be specified in two ways:

#### **1. Relative Time Limit (Duration)**

Format: `+<time>` (starts when quest is taken)

**Syntax:** `+[d]d [h]h [mn]mn [s]s`
- `d` = days (optional)
- `h` = hours [0-23] (optional)
- `mn` = minutes [0-59] (optional)
- `s` = seconds [0-59] (optional)

**Examples:**
```yaml
# Quest expires 5 minutes after being taken
- Id: 2069
  Title: Tierra Gorge Battle
  TimeLimit: +5mn

# Quest expires 2 hours after being taken
- Id: 1001
  Title: Timed Challenge
  TimeLimit: +2h

# Quest expires 1 day and 30 minutes after being taken
- Id: 1002
  Title: Daily Quest Extended
  TimeLimit: +1d 30mn

# Quest expires 3 days, 12 hours, 30 minutes after being taken
- Id: 1003
  Title: Long Term Quest
  TimeLimit: +3d 12h 30mn
```

#### **2. Absolute Time Limit (Fixed Expiration)**

Format: `<date/day> <time>` (expires at specific time)

**Syntax (Option 1):** `<d>d [h]h [mn]mn [s]s`
**Syntax (Option 2):** `<DayOfWeek> [h]h [mn]mn [s]s`

**Examples:**
```yaml
# Quest expires 3 days from now at 4am
- Id: 9419
  Title: Attack Sky Fortress
  TimeLimit: 3d 4h

# Quest expires next Monday at 4am
- Id: 5965
  Title: "[Standby] Devil's Special"
  TimeLimit: Monday 4h

# Quest expires next Friday at 23:30
- Id: 1004
  Title: Weekly Challenge
  TimeLimit: Friday 23h 30mn

# Quest expires in 7 days at midnight
- Id: 1005
  Title: Week-Long Quest
  TimeLimit: 7d 0h
```

**Days of Week:** Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday

---

### Targets (Optional)
**Type:** Array
**Description:** Quest objectives - monsters to kill or conditions to meet

Targets can be defined in two ways:

#### **Method 1: Simple Mob Targeting**

Used for straightforward "kill X monsters" quests.

**Required Fields:**
- `Mob`: Monster name (AegisName from mob_db)
- `Count`: Number of monsters to kill

**Example:**
```yaml
Targets:
  - Mob: PORING
    Count: 10
  - Mob: DROPS
    Count: 5
```

**Notes:**
- `Count: 0` will skip the target on import (useful for disabled objectives)
- Mob must exist in `mob_db.yml`

---

#### **Method 2: Advanced Targeting (Race/Size/Element/Level)**

Used for flexible targeting by monster characteristics.

**Required Fields:**
- `Id`: Unique target index (positive number)
- `Count`: Number of kills required

**Optional Filters:**
- `Race`: Monster race filter
- `Size`: Monster size filter
- `Element`: Monster element filter
- `MinLevel`: Minimum monster level
- `MaxLevel`: Maximum monster level
- `Location`: Map where kills count
- `MapName`: Display name for location
- `MapMobTargets`: Specific monster whitelist/blacklist

**Example:**
```yaml
Targets:
  # Kill any 20 Demon-race monsters
  - Id: 1
    Count: 20
    Race: Demon

  # Kill 15 large monsters
  - Id: 2
    Count: 15
    Size: Large

  # Kill 10 Fire-element monsters between level 50-70
  - Id: 3
    Count: 10
    Element: Fire
    MinLevel: 50
    MaxLevel: 70

  # Kill 30 monsters on a specific map
  - Id: 4
    Count: 30
    Location: prontera
    MapName: Prontera
```

---

### Target Field Details

#### **Race**
**Valid Values:** `Angel`, `Brute`, `DemiHuman`, `Demon`, `Dragon`, `Fish`, `Formless`, `Insect`, `Plant`, `Undead`, `All`

**Default:** `All`

**Example:**
```yaml
Targets:
  - Id: 1
    Count: 25
    Race: Undead    # Only Undead monsters count
```

---

#### **Size**
**Valid Values:** `Small`, `Medium`, `Large`, `All`

**Default:** `All`

**Example:**
```yaml
Targets:
  - Id: 1
    Count: 15
    Size: Large     # Only Large monsters count
```

---

#### **Element**
**Valid Values:** `Dark`, `Earth`, `Fire`, `Ghost`, `Holy`, `Neutral`, `Poison`, `Undead`, `Water`, `Wind`, `All`

**Default:** `All`

**Example:**
```yaml
Targets:
  - Id: 1
    Count: 20
    Element: Fire   # Only Fire-element monsters count
```

---

#### **MinLevel / MaxLevel**
**Type:** Integer
**Default:**
- `MinLevel`: 1 (if MaxLevel defined)
- `MaxLevel`: No limit

**Notes:**
- Set to `0` to ignore the limit on import

**Example:**
```yaml
Targets:
  # Kill monsters level 30-50
  - Id: 1
    Count: 50
    MinLevel: 30
    MaxLevel: 50

  # Kill monsters level 80+
  - Id: 2
    Count: 20
    MinLevel: 80
```

---

#### **Location / MapName**
**Location Type:** String (map name without .gat)
**MapName Type:** String (display name)

**Example:**
```yaml
Targets:
  - Id: 1
    Count: 100
    Location: prontera
    MapName: Prontera City
```

**Notes:**
- Kills only count on the specified map
- `MapName` is shown in the quest UI

---

#### **MapMobTargets**
**Type:** Dictionary
**Description:** Whitelist/blacklist specific monsters by name

**Format:**
```yaml
MapMobTargets:
  <MonsterName>: <true/false>
```

- `true`: Add monster to whitelist
- `false`: Remove monster from whitelist

**Example:**
```yaml
Targets:
  - Id: 1
    Count: 50
    Location: prontera
    MapMobTargets:
      PORING: true       # Only Porings count
      DROPS: true        # Drops also count
      POPORING: true     # Poporings also count
```

**Notes:**
- Only active when using `Id` method (not `Mob` method)
- Allows precise control over which monsters count

---

## DROPS

**Type:** Array
**Description:** Quest-specific item drop configuration

When a quest is active, you can configure special drops from monsters.

**Fields:**
- `Mob`: Monster ID or name (0 = all monsters)
- `Item`: Item name (AegisName from item_db)
- `Count`: Number of items that drop
- `Rate`: Drop rate (10000 = 100%)

**Example:**
```yaml
Drops:
  # Drop Quest Item from specific monster
  - Mob: PORING
    Item: Jellopy
    Count: 1
    Rate: 5000        # 50% drop rate

  # Drop from any monster
  - Mob: 0
    Item: Quest_Token
    Count: 1
    Rate: 1000        # 10% drop rate

  # Drop multiple items at once
  - Mob: BOSS_MONSTER
    Item: Rare_Item
    Count: 3
    Rate: 10000       # 100% drop rate (3 items)
```

**Notes:**
- `Mob: 0` applies to ALL monsters
- `Count` defaults to 1 for non-stackable items
- `Rate` is in basis points (10000 = 100%, 5000 = 50%, 100 = 1%, 1 = 0.01%)
- Drops only occur while quest is active

---

## COMPLETE QUEST EXAMPLES

### Example 1: Simple Kill Quest
```yaml
- Id: 1000
  Title: Poring Extermination
  Targets:
    - Mob: PORING
      Count: 30
```

**Description:** Kill 30 Porings. No time limit.

---

### Example 2: Timed Quest with Drops
```yaml
- Id: 1001
  Title: Emergency Poring Alert
  TimeLimit: +1h
  Targets:
    - Mob: PORING
      Count: 50
  Drops:
    - Mob: PORING
      Item: Poring_Coin
      Count: 1
      Rate: 5000
```

**Description:** Kill 50 Porings within 1 hour. Porings have 50% chance to drop Poring Coin.

---

### Example 3: Multi-Target Quest
```yaml
- Id: 1002
  Title: Slime Cleanup
  Targets:
    - Mob: PORING
      Count: 20
    - Mob: DROPS
      Count: 15
    - Mob: POPORING
      Count: 10
```

**Description:** Kill 20 Porings, 15 Drops, and 10 Poporings.

---

### Example 4: Advanced Race/Element Quest
```yaml
- Id: 1003
  Title: Demon Hunter
  TimeLimit: +1d
  Targets:
    - Id: 1
      Count: 50
      Race: Demon
      MinLevel: 40
      MaxLevel: 80
```

**Description:** Kill 50 Demon-race monsters between level 40-80 within 24 hours.

---

### Example 5: Location-Specific Quest
```yaml
- Id: 1004
  Title: Prontera Patrol
  Targets:
    - Id: 1
      Count: 100
      Location: prt_fild08
      MapName: Prontera Field
```

**Description:** Kill 100 monsters in Prontera Field (prt_fild08).

---

### Example 6: Weekly Quest
```yaml
- Id: 1005
  Title: Weekly Challenge
  TimeLimit: Monday 4h
  Targets:
    - Id: 1
      Count: 200
      Race: Undead
  Drops:
    - Mob: 0
      Item: Weekly_Token
      Count: 1
      Rate: 2000
```

**Description:** Kill 200 Undead-race monsters before Monday 4am. All monsters have 20% chance to drop Weekly Token.

---

### Example 7: Boss Hunt Quest
```yaml
- Id: 1006
  Title: MVP Elimination
  Targets:
    - Mob: EDDGA
      Count: 1
    - Mob: OSIRIS
      Count: 1
    - Mob: BAPHOMET
      Count: 1
  Drops:
    - Mob: EDDGA
      Item: Eddga_Trophy
      Count: 1
      Rate: 10000
    - Mob: OSIRIS
      Item: Osiris_Trophy
      Count: 1
      Rate: 10000
    - Mob: BAPHOMET
      Item: Baphomet_Trophy
      Count: 1
      Rate: 10000
```

**Description:** Kill Eddga, Osiris, and Baphomet once each. Each drops a guaranteed trophy item.

---

## QUEST SCRIPT COMMANDS

Use these script commands to interact with quests:

### setquest(<quest_id>)
Gives the quest to the player.

```c
setquest(1000);  // Start quest 1000
```

---

### completequest(<quest_id>)
Marks the quest as completed.

```c
if (questprogress(1000, PLAYTIME) == 2) {
    completequest(1000);
    mes "Quest completed!";
}
```

---

### erasequest(<quest_id>)
Removes the quest from the player.

```c
erasequest(1000);  // Remove quest 1000
```

---

### questprogress(<quest_id>{, <type>})
Checks quest progress.

**Types:**
- `PLAYTIME` (0): Check if quest time expired
- `HUNTING` (1): Check if hunt objectives completed
- `HUNTING | PLAYTIME` (2): Check both

**Returns:**
- `0`: Quest not started
- `1`: Quest active
- `2`: Quest complete/expired

```c
if (questprogress(1000, HUNTING) == 2) {
    mes "You completed all hunt objectives!";
}
```

---

### checkquest(<quest_id>{, <type>})
Alias for `questprogress()`.

---

## QUEST STATUS VALUES

| Value | Constant | Meaning |
|-------|----------|---------|
| 0 | QUEST_NOT_STARTED | Quest not started |
| 1 | QUEST_ACTIVE | Quest active/in progress |
| 2 | QUEST_COMPLETE | Quest completed |

---

## BEST PRACTICES

1. **Unique IDs:** Always use unique quest IDs (avoid conflicts)
2. **Time Limits:** Use relative time (`+`) for recurring quests, absolute time for weekly/event quests
3. **Drop Rates:** Balance drop rates carefully (too high = no challenge, too low = frustration)
4. **Target Count:** Set `Count: 0` to temporarily disable objectives without deleting them
5. **Testing:** Test time limits thoroughly (server timezone matters!)
6. **Performance:** Avoid `Mob: 0` (all monsters) for drops when possible - use specific mobs
7. **UI Display:** Keep `Title` and `MapName` short for better UI display

---

## COMMON MISTAKES

### ❌ Wrong:
```yaml
- Id: 1000
  Title: Kill Quest
  TimeLimit: 5mn           # Missing +
  Targets:
    - Mob: INVALID_MOB     # Mob doesn't exist
      Count: -5            # Negative count
```

### ✓ Correct:
```yaml
- Id: 1000
  Title: Kill Quest
  TimeLimit: +5mn          # Relative time
  Targets:
    - Mob: PORING          # Valid mob from mob_db
      Count: 10            # Positive count
```

---

## RELATED FILES

- `/db/(pre-)re/quest_db.yml` - Quest database
- `/doc/script_commands.txt` - Quest-related script commands
- `/db/(pre-)re/mob_db.yml` - Monster names for Targets
- `/db/(pre-)re/item_db.yml` - Item names for Drops

---

## SEE ALSO

- **KB_EXAMPLE_005:** Quest Implementation Examples
- **KB_CMD_015:** Quest Script Commands
- **KB_DB_001:** Database System Overview

---

*Last Updated: 2022-06-29*
*rAthena Documentation*
---
kb_id: KB_REF_005
kb_type: reference
kb_category: scripting
kb_subcategory: script_commands
kb_keywords: [script, npc, commands, scripting language, mes, next, close, menu, select, if, while, for, getitem, delitem, warp, heal, sc_start, monster, announce, variables, arrays, functions]
kb_related: [KB_EXAMPLE_001, KB_REF_008]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2025-10-23
kb_use_case: [npc_scripting, quest_creation, custom_content, server_features]
---

# rAthena Essential Script Commands Reference

Comprehensive reference for the most commonly used rAthena scripting commands.

## Overview

This document covers the **essential 80+ commands** you'll use in 90% of NPC scripting. For the complete command list (400+ commands), see `/doc/script_commands.txt`.

**Script Basics:**
- Scripts are case-insensitive
- Commands end with semicolon (`;`)
- Use `//` for single-line comments
- Use `/* */` for multi-line comments
- All numbers are integers (no decimals)

---

## TABLE OF CONTENTS

1. [Dialogue & Display](#1-dialogue--display)
2. [Flow Control](#2-flow-control)
3. [Variables & Data](#3-variables--data)
4. [Player Information](#4-player-information)
5. [Items & Inventory](#5-items--inventory)
6. [Player Stats & Status](#6-player-stats--status)
7. [Movement & Warping](#7-movement--warping)
8. [Quests](#8-quests)
9. [Monsters & Mobs](#9-monsters--mobs)
10. [NPCs & Map](#10-npcs--map)
11. [Timers & Delays](#11-timers--delays)
12. [Party & Guild](#12-party--guild)
13. [Server & Announcements](#13-server--announcements)
14. [Advanced](#14-advanced)

---

## 1. DIALOGUE & DISPLAY

### mes "<message>"
Display a message in the dialog window.

```c
mes "[NPC Name]";
mes "Hello, adventurer!";
mes "Welcome to my shop.";
```

**Tips:**
- Use `[NPC Name]` as first line for name display
- Each `mes` is a new line in the dialog box
- Dialog displays until `next`, `close`, or `menu` command

---

### next
Display a "Next" button and wait for player to click it.

```c
mes "[Guide]";
mes "This is page 1.";
next;
mes "[Guide]";
mes "This is page 2.";
close;
```

---

### close / close2
Close the dialog window.

- `close` - Close and end script
- `close2` - Close but continue script execution

```c
mes "Goodbye!";
close;

// vs

mes "Processing...";
close2;
getitem 501,1;  // This still executes
end;
```

---

### menu "<option1>",<label>{,"<option2>",<label>...}
Display a menu with clickable options.

```c
mes "[Shop]";
mes "What do you need?";
menu
    "Red Potion",L_RedPotion,
    "Blue Potion",L_BluePotion,
    "Nothing",L_Cancel;

L_RedPotion:
    mes "Here's a Red Potion!";
    getitem 501,1;
    close;

L_BluePotion:
    mes "Here's a Blue Potion!";
    getitem 505,1;
    close;

L_Cancel:
    mes "Come back soon!";
    close;
```

---

### select("<option1>{:<option2>...}")
Modern menu syntax that returns selected option number.

```c
mes "[Shop]";
mes "What do you need?";
switch(select("Red Potion:Blue Potion:Yellow Potion:Cancel")) {
case 1:
    getitem 501,1;
    break;
case 2:
    getitem 505,1;
    break;
case 3:
    getitem 503,1;
    break;
case 4:
    mes "Goodbye!";
    break;
}
close;
```

**Advantage:** More compact than `menu`, easier to maintain.

---

### input {.<variable>}{,<min>{,<max>}}
Prompt player to enter a number or string.

```c
// Number input
mes "How many potions do you want?";
input .@amount,1,100;  // Min 1, Max 100
mes "You entered: " + .@amount;

// String input
mes "What's your name?";
input .@name$;
mes "Hello, " + .@name$ + "!";
```

---

### prompt("<message>"{,<min>,<max>})
Modern alternative to input with inline message.

```c
.@amount = prompt("How many potions?", 1, 100);
mes "You want " + .@amount + " potions.";
```

---

## 2. FLOW CONTROL

### if (<condition>) {<code>} {else {<code>}}
Conditional execution.

```c
if (BaseLevel >= 50) {
    mes "You are level 50+!";
} else if (BaseLevel >= 30) {
    mes "You are level 30-49.";
} else {
    mes "You are below level 30.";
}
```

**Comparison Operators:**
- `==` Equal to
- `!=` Not equal to
- `>` Greater than
- `<` Less than
- `>=` Greater than or equal
- `<=` Less than or equal
- `&&` AND
- `||` OR
- `!` NOT

---

### switch (<variable>) {case <value>: ... default: ...}
Multi-way branch.

```c
switch(Class) {
case Job_Swordman:
    mes "You are a Swordsman!";
    break;
case Job_Mage:
    mes "You are a Mage!";
    break;
case Job_Acolyte:
    mes "You are an Acolyte!";
    break;
default:
    mes "You are something else!";
    break;
}
```

---

### while (<condition>) {<code>}
Loop while condition is true.

```c
.@i = 0;
while (.@i < 10) {
    mes "Count: " + .@i;
    .@i++;
}
```

---

### for (<init>; <condition>; <increment>) {<code>}
For loop.

```c
for (.@i = 0; .@i < 10; .@i++) {
    mes "Count: " + .@i;
}
```

---

### do {<code>} while (<condition>)
Execute code at least once, then loop if condition true.

```c
do {
    mes "This runs at least once.";
} while (0);  // Won't loop
```

---

### break / continue
- `break` - Exit loop early
- `continue` - Skip to next iteration

```c
for (.@i = 0; .@i < 10; .@i++) {
    if (.@i == 5) continue;  // Skip 5
    if (.@i == 8) break;      // Stop at 8
    mes "Count: " + .@i;
}
```

---

### goto <label>
Jump to a label. **Use sparingly!**

```c
goto L_Skip;
mes "This won't show.";
L_Skip:
mes "Jumped here!";
```

---

### end
End script execution.

```c
mes "The end.";
end;
mes "This won't execute.";
```

---

## 3. VARIABLES & DATA

### Variable Types

```c
// Permanent character variables
MyVariable = 100;
MyString$ = "Hello";

// Temporary character variables
@TempVar = 100;
@TempString$ = "Temp";

// Permanent account variables
#AccountVar = 100;
#AccountString$ = "Account";

// Global permanent variables
$GlobalVar = 100;
$GlobalString$ = "Global";

// Global temporary variables
$@GlobalTemp = 100;

// NPC variables
.NPCVar = 100;
.NPCString$ = "NPC";

// Scope variables
.@ScopeVar = 100;
.@ScopeString$ = "Scope";

// Instance variables
'InstanceVar = 100;
```

**Scope Summary:**
- No prefix = Permanent character
- `@` = Temporary character
- `#` = Permanent account (this char server)
- `##` = Permanent account (all char servers)
- `$` = Permanent global
- `$@` = Temporary global
- `.` = NPC variable
- `.@` = Scope variable (function/script)
- `'` = Instance variable

---

### Arrays

```c
// Declare array
.@items[0] = 501;  // Red Potion
.@items[1] = 502;  // Orange Potion
.@items[2] = 503;  // Yellow Potion

// Loop through array
for (.@i = 0; .@i < getarraysize(.@items); .@i++) {
    mes "Item " + .@i + ": " + getitemname(.@items[.@i]);
}

// Get array size
.@size = getarraysize(.@items);

// Clear array
cleararray .@items[0],0,128;

// Copy array
copyarray .@dest[0], .@source[0], getarraysize(.@source);

// Delete array element
deletearray .@items[1],1;  // Delete index 1
```

---

### set <variable>,<value>
**Legacy** way to set variables. Use `=` instead.

```c
// Old way
set .@var, 100;

// New way (preferred)
.@var = 100;
```

---

### setarray <array>,<value>{,<value>...}
Set multiple array values at once.

```c
setarray .@items[0], 501, 502, 503, 504, 505;
```

---

### getarraysize(<array>)
Returns the size of an array.

```c
setarray .@items, 501, 502, 503;
.@size = getarraysize(.@items);  // Returns 3
```

---

### deletearray <array>{,<count>}
Delete array elements.

```c
deletearray .@items[0],1;  // Delete first element
deletearray .@items[0],getarraysize(.@items);  // Delete all
```

---

### cleararray <array>,<value>,<count>
Fill array with a value.

```c
cleararray .@items[0],0,10;  // Set first 10 elements to 0
```

---

## 4. PLAYER INFORMATION

### strcharinfo(<type>)
Get character information as string.

**Types:**
- `0` or `PC_NAME` - Character name
- `1` or `PC_PARTY` - Party name
- `2` or `PC_GUILD` - Guild name
- `3` or `PC_MAP` - Map name

```c
.@name$ = strcharinfo(PC_NAME);
.@party$ = strcharinfo(PC_PARTY);
.@guild$ = strcharinfo(PC_GUILD);
.@map$ = strcharinfo(PC_MAP);

mes "Your name is " + .@name$;
mes "Your party is " + .@party$;
```

---

### getcharid(<type>)
Get character ID numbers.

**Types:**
- `0` or `CHAR_ID_CHAR` - Character ID
- `1` or `CHAR_ID_PARTY` - Party ID
- `2` or `CHAR_ID_GUILD` - Guild ID
- `3` or `CHAR_ID_ACCOUNT` - Account ID
- `4` or `CHAR_ID_BG` - Battleground ID
- `5` or `CHAR_ID_CLAN` - Clan ID

```c
.@char_id = getcharid(CHAR_ID_CHAR);
.@account_id = getcharid(CHAR_ID_ACCOUNT);
.@party_id = getcharid(CHAR_ID_PARTY);
```

---

### Built-in Character Variables

```c
// Basic Stats
BaseLevel      // Base level
JobLevel       // Job level
BaseExp        // Current base exp
JobExp         // Current job exp
NextBaseExp    // Exp needed for next base level
NextJobExp     // Exp needed for next job level

// Resources
Zeny           // Current Zeny
Hp             // Current HP
MaxHp          // Maximum HP
Sp             // Current SP
MaxSp          // Maximum SP

// Status
StatusPoint    // Available status points
SkillPoint     // Available skill points
Weight         // Current weight
MaxWeight      // Maximum weight capacity

// Character Info
Class          // Job class ID
Sex            // 0=Female, 1=Male
Upper          // 0=Normal, 1=Advanced, 2=Baby

// Stats
Str, Agi, Vit, Int, Dex, Luk  // Base stats
```

**Example:**
```c
mes "Level: " + BaseLevel;
mes "Job: " + JobLevel;
mes "Zeny: " + Zeny;
mes "HP: " + Hp + "/" + MaxHp;

if (Zeny >= 1000) {
    Zeny -= 1000;
    mes "Paid 1000z.";
}
```

---

## 5. ITEMS & INVENTORY

### getitem <item_id>,<amount>{,<account_id>}
Give item(s) to player.

```c
// Give 10 Red Potions
getitem 501,10;

// Using item name constant
getitem Red_Potion,10;

// Give to specific player
getitem 501,10,getcharid(3);
```

---

### delitem <item_id>,<amount>
Remove item(s) from player.

```c
delitem 501,5;  // Remove 5 Red Potions
```

---

### countitem(<item_id>)
Count items in inventory.

```c
.@count = countitem(501);  // Count Red Potions
if (.@count >= 10) {
    mes "You have 10+ Red Potions!";
}
```

---

### checkweight(<item_id>,<amount>)
Check if player can carry item weight.

```c
if (checkweight(501,100)) {
    getitem 501,100;
} else {
    mes "You can't carry that much!";
}
```

---

### getitemname(<item_id>)
Get item name as string.

```c
.@name$ = getitemname(501);
mes "Item: " + .@name$;  // "Item: Red Potion"
```

---

### getnameditem(<item_id>,<player_name>)
Give item inscribed with player name.

```c
// Give sword inscribed with player's name
getnameditem 1101,strcharinfo(0);
```

---

## 6. PLAYER STATS & STATUS

### heal <hp>,<sp>
Heal player HP and/or SP.

```c
heal 100,50;      // Heal 100 HP and 50 SP
heal 1000,0;      // Heal 1000 HP only
heal 0,100;       // Heal 100 SP only
heal -50,0;       // Damage 50 HP
```

---

### percentheal <hp%>,<sp%>
Heal by percentage.

```c
percentheal 100,100;  // Full heal
percentheal 50,50;    // Heal 50% HP and SP
percentheal -10,0;    // Damage 10% HP
```

---

### statusup <stat>
Increase a stat by 1 point.

**Stats:** `bStr`, `bAgi`, `bVit`, `bInt`, `bDex`, `bLuk`

```c
statusup bStr;  // Add 1 STR
statusup bInt;  // Add 1 INT
```

---

### statusup2 <stat>,<amount>
Increase a stat by multiple points.

```c
statusup2 bStr,10;  // Add 10 STR
```

---

### readparam(<parameter>)
Read player parameters.

**Common Parameters:**
- `BaseLevel`, `JobLevel`
- `BaseExp`, `JobExp`
- `Zeny`
- `Hp`, `MaxHp`, `Sp`, `MaxSp`
- `bStr`, `bAgi`, `bVit`, `bInt`, `bDex`, `bLuk`

```c
.@level = readparam(BaseLevel);
.@str = readparam(bStr);
```

---

### sc_start <effect>,<duration>,<val1>{,<rate>,<flag>,<unit_id>}
Apply a status effect.

```c
// Blessing for 240 seconds (240000 ms), level 10
sc_start SC_BLESSING,240000,10;

// Increase AGI for 5 minutes, level 10
sc_start SC_INCREASEAGI,300000,10;

// Poison for 30 seconds
sc_start SC_POISON,30000,1;
```

**Common Status Effects:** See KB_REF_006 for full list.

---

### sc_end <effect>
Remove a status effect.

```c
sc_end SC_STONE;
sc_end SC_CURSE;
```

---

### skill <skill_id>,<level>{,<flag>}
Give player a skill.

```c
// Give Heal level 5
skill AL_HEAL,5;

// Temporary skill (doesn't save)
skill AL_HEAL,5,1;
```

---

## 7. MOVEMENT & WARPING

### warp "<map>",<x>,<y>
Warp player to location.

```c
warp "prontera",156,191;  // Warp to Prontera
warp "SavePoint",0,0;     // Warp to save point
warp "Random",0,0;        // Random location on current map
```

---

### areawarp "<from_map>",<x1>,<y1>,<x2>,<y2>,"<to_map>",<x>,<y>
Warp all players in an area.

```c
// Warp everyone in 10x10 area
areawarp "prontera",150,150,160,160,"payon",100,100;
```

---

### savepoint "<map>",<x>,<y>
Set player's save point.

```c
savepoint "prontera",156,191;
```

---

### return
Return to save point.

```c
mes "Returning you to save point!";
close2;
return;
end;
```

---

## 8. QUESTS

### setquest <quest_id>
Start a quest.

```c
setquest 1000;
mes "Quest started!";
```

---

### completequest <quest_id>
Complete a quest.

```c
if (questprogress(1000,HUNTING) == 2) {
    completequest 1000;
    mes "Quest completed!";
    getexp 10000,5000;
}
```

---

### erasequest <quest_id>
Remove a quest.

```c
erasequest 1000;
```

---

### questprogress(<quest_id>{,<type>})
Check quest status.

**Types:**
- `PLAYTIME` (0) - Check if time expired
- `HUNTING` (1) - Check if hunt complete
- `PLAYTIME|HUNTING` (2) - Check both

**Returns:**
- `0` - Quest not started
- `1` - Quest active
- `2` - Quest complete/expired

```c
.@status = questprogress(1000,HUNTING);
if (.@status == 0) {
    mes "Quest not started.";
} else if (.@status == 1) {
    mes "Quest in progress.";
} else if (.@status == 2) {
    mes "Quest objectives complete!";
}
```

---

## 9. MONSTERS & MOBS

### monster "<map>",<x>,<y>,"<name>",<mob_id>,<amount>{,<event>}
Spawn monster(s).

```c
// Spawn 1 Poring at coordinates
monster "prontera",156,191,"Poring",1002,1;

// Spawn 10 Porings randomly on map
monster "prontera",0,0,"Poring",1002,10;

// Spawn with death event
monster "prontera",0,0,"Poring",1002,5,"MyNPC::OnPoringKilled";
```

---

### areamonster "<map>",<x1>,<y1>,<x2>,<y2>,"<name>",<mob_id>,<amount>{,<event>}
Spawn monsters in an area.

```c
areamonster "prontera",150,150,160,160,"Poring",1002,10;
```

---

### killmonster "<map>","<event>"
Kill all monsters with event label.

```c
killmonster "prontera","All";  // Kill all
killmonster "prontera","MyNPC::OnKilled";  // Kill specific
```

---

### killmonsterall "<map>"
Kill all monsters on map.

```c
killmonsterall "prontera";
```

---

### getmobdrops(<mob_id>)
Get monster drop list.

```c
getmobdrops(1002);  // Get Poring drops
```

---

### getmonsterinfo(<mob_id>,<type>)
Get monster information.

**Types:**
- `MOB_NAME` - Name
- `MOB_LV` - Level
- `MOB_MAXHP` - Max HP
- `MOB_BASEEXP` - Base EXP
- `MOB_JOBEXP` - Job EXP
- `MOB_ATK1` - Attack 1
- `MOB_ATK2` - Attack 2
- `MOB_DEF` - Defense
- `MOB_MDEF` - Magic Defense
- `MOB_RACE` - Race
- `MOB_ELEMENT` - Element

```c
.@name$ = getmonsterinfo(1002,MOB_NAME);
.@hp = getmonsterinfo(1002,MOB_MAXHP);
```

---

## 10. NPCS & MAP

### enablenpc "<npc_name>"
Enable (show) an NPC.

```c
enablenpc "MyNPC";
```

---

### disablenpc "<npc_name>"
Disable (hide) an NPC.

```c
disablenpc "MyNPC";
```

---

### hideonnpc "<npc_name>"
Hide NPC (alternative).

```c
hideonnpc "MyNPC";
```

---

### hideoffnpc "<npc_name>"
Show NPC (alternative).

```c
hideoffnpc "MyNPC";
```

---

### donpcevent "<npc>::<label>"
Trigger an NPC event.

```c
donpcevent "MyNPC::OnEvent";
```

---

### doevent "<npc>::<label>"
Execute NPC event code.

```c
doevent "MyNPC::OnEvent";
```

---

### setmapflag "<map>",<mapflag>{,<val>}
Set a mapflag.

```c
setmapflag "prontera",mf_pvp;
setmapflag "prontera",mf_noteleport;
```

---

### removemapflag "<map>",<mapflag>
Remove a mapflag.

```c
removemapflag "prontera",mf_pvp;
```

---

### getmapflag("<map>",<mapflag>)
Check if mapflag is set.

```c
if (getmapflag("prontera",mf_pvp)) {
    mes "This is a PvP map!";
}
```

---

## 11. TIMERS & DELAYS

### sleep <milliseconds>
Pause script execution.

```c
mes "Wait 3 seconds...";
close2;
sleep 3000;
mes "Done waiting!";
end;
```

---

### sleep2 <milliseconds>
Sleep without blocking other scripts.

```c
sleep2 3000;
```

---

### addtimer <milliseconds>,"<npc>::<label>"
Set a timer.

```c
mes "See you in 10 seconds!";
close2;
addtimer 10000,"MyNPC::OnTimer";
end;

OnTimer:
    mes "Timer finished!";
    close;
```

---

### deltimer "<npc>::<label>"
Delete a timer.

```c
deltimer "MyNPC::OnTimer";
```

---

### initnpctimer {<flag>{,"<npc_name>"}
Start NPC timer.

```c
OnInit:
    initnpctimer;
    end;

OnTimer60000:  // Every 60 seconds
    announce "Server maintenance in 1 hour!",bc_all;
    stopnpctimer;
    end;
```

---

### stopnpctimer
Stop NPC timer.

```c
stopnpctimer;
```

---

## 12. PARTY & GUILD

### getpartymember <party_id>{,<type>}
Get party member list.

```c
getpartymember getcharid(CHAR_ID_PARTY);
for (.@i = 0; .@i < $@partymembercount; .@i++) {
    mes "Member: " + $@partymembername$[.@i];
}
```

---

### getguildmember <guild_id>{,<type>}
Get guild member list.

```c
getguildmember getcharid(CHAR_ID_GUILD);
```

---

### warpparty "<map>",<x>,<y>,<party_id>{,<from_map>}
Warp entire party.

```c
warpparty "prontera",156,191,getcharid(CHAR_ID_PARTY);
```

---

### warpguild "<map>",<x>,<y>,<guild_id>
Warp entire guild.

```c
warpguild "prontera",156,191,getcharid(CHAR_ID_GUILD);
```

---

## 13. SERVER & ANNOUNCEMENTS

### announce "<message>",<flag>{,<color>}
Server-wide announcement.

**Flags:**
- `bc_map` (0x01) - Map only
- `bc_area` (0x02) - Area only
- `bc_self` (0x04) - Self only
- `bc_all` (0x00) - All players
- `bc_yellow` (0x10) - Yellow text
- `bc_blue` (0x20) - Blue text
- `bc_woe` (0x40) - WoE format

```c
announce "Server maintenance in 10 minutes!",bc_all;
announce "You found a rare item!",bc_self;
announce "PvP event starting!",bc_map;
```

---

### mapannounce "<map>","<message>",<flag>
Map-only announcement.

```c
mapannounce "prontera","Event starting in Prontera!",bc_map;
```

---

### areaannounce "<map>",<x1>,<y1>,<x2>,<y2>,"<message>",<flag>
Area announcement.

```c
areaannounce "prontera",150,150,160,160,"Event here!",bc_area;
```

---

### dispbottom "<message>"
Display message at bottom of screen.

```c
dispbottom "You gained bonus experience!";
```

---

### atcommand "<command>"
Execute at-command.

```c
atcommand "@refresh";
atcommand "@heal";
```

---

## 14. ADVANCED

### callfunc("<function>"{,<arg>...})
Call a function.

```c
callfunc("MyFunction",100,"test");
```

---

### callsub <label>{,<arg>...}
Call a subroutine.

```c
callsub L_SubRoutine,100;
end;

L_SubRoutine:
    .@value = getarg(0);
    mes "Value: " + .@value;
    return;
```

---

### getarg(<index>{,<default>})
Get function/subroutine argument.

```c
function MyFunc {
    .@arg1 = getarg(0);
    .@arg2 = getarg(1,"default");
    return .@arg1 + .@arg2;
}
```

---

### setd / getd
Dynamic variable access.

```c
setd("$MyVar_" + .@id, 100);
.@value = getd("$MyVar_" + .@id);
```

---

### query_sql("<query>"{,<array>...})
Execute SQL query.

```c
query_sql("SELECT `name` FROM `char` WHERE `char_id` = " + .@char_id, .@name$);
```

---

### getusers(<type>)
Get player count.

**Types:**
- `0` - All online players
- `1` - Players on current map

```c
.@online = getusers(0);
mes "Players online: " + .@online;
```

---

### rand(<min>,<max>) / rand(<max>)
Generate random number.

```c
.@roll = rand(1,6);  // 1-6 (dice)
.@percent = rand(100);  // 0-99
```

---

### gettime(<type>)
Get current time/date.

**Types:**
- `DT_SECOND` (1) - Seconds (0-59)
- `DT_MINUTE` (2) - Minutes (0-59)
- `DT_HOUR` (3) - Hour (0-23)
- `DT_DAYOFWEEK` (4) - Day of week (0=Sunday)
- `DT_DAYOFMONTH` (5) - Day of month (1-31)
- `DT_MONTH` (6) - Month (1-12)
- `DT_YEAR` (7) - Year (4-digit)
- `DT_DAYOFYEAR` (8) - Day of year (1-366)

```c
.@hour = gettime(DT_HOUR);
if (.@hour >= 18 || .@hour < 6) {
    mes "It's nighttime!";
}
```

---

## COMMON PATTERNS

### Check Item Quest
```c
if (countitem(501) >= 10) {
    delitem 501,10;
    getexp 1000,500;
    mes "Quest complete!";
} else {
    mes "Need 10 Red Potions.";
}
```

### Level Check
```c
if (BaseLevel < 50) {
    mes "You need level 50+.";
    close;
}
```

### Zeny Cost
```c
if (Zeny < 1000) {
    mes "Not enough Zeny!";
    close;
}
Zeny -= 1000;
mes "Paid 1000z.";
```

### One-Time Event
```c
if (#STARTER_RECEIVED) {
    mes "You already got this.";
    close;
}
getitem 501,10;
set #STARTER_RECEIVED,1;
mes "Here's your starter pack!";
```

### Cooldown Timer
```c
if (#LAST_USE + 3600 > gettimetick(2)) {
    mes "Come back in " + ((#LAST_USE + 3600 - gettimetick(2)) / 60) + " minutes.";
    close;
}
set #LAST_USE,gettimetick(2);
mes "Ready to use!";
```

---

## DEBUGGING

### debugmes "<message>"
Output to console (server-side only).

```c
debugmes "Debug: Variable = " + .@var;
```

---

### dispbottom "<message>"
Show message to player.

```c
dispbottom "Debug: HP = " + Hp;
```

---

## SEE ALSO

- **Full Reference:** `/doc/script_commands.txt` (11,721 lines, 400+ commands)
- **KB_EXAMPLE_001:** NPC Script Examples
- **KB_REF_006:** Status Effects Reference
- **KB_REF_007:** Visual Effects Reference
- **KB_REF_008:** Item Bonus Reference

---

*Last Updated: 2025-10-23*
*rAthena Documentation - Essential Commands*
---
kb_id: KB_REF_006
kb_type: reference
kb_category: game_mechanics
kb_subcategory: status_effects
kb_keywords: [status effects, status changes, SC_, buffs, debuffs, sc_start, sc_end, stone, freeze, stun, poison, blessing, increase agi, val1, val2, val3, val4]
kb_related: [KB_REF_005, KB_CMD_010]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2024-10-24
kb_use_case: [npc_scripting, item_scripting, skill_effects, buff_management]
---

# rAthena Status Effects Reference

Complete reference for status effects (status changes) in rAthena.

## Overview

Status effects (also called "status changes" or "SC") are temporary conditions applied to characters that modify their stats, behavior, or appearance. They include buffs, debuffs, ailments, and special states.

**Script Usage:**
```c
// Apply status effect
sc_start <SC_CONST>,<duration_ms>,<val1>{,<rate>,<flag>,<unit_id>};

// Remove status effect
sc_end <SC_CONST>;

// Check if status effect is active
if (getstatus(SC_STONE)) {
    mes "You are petrified!";
}
```

**Duration:** Always in milliseconds (1000 = 1 second, 60000 = 1 minute)

---

## TABLE OF CONTENTS

1. [Basic Status Ailments](#1-basic-status-ailments)
2. [Stat Buffs](#2-stat-buffs)
3. [Stat Debuffs](#3-stat-debuffs)
4. [Element Changes](#4-element-changes)
5. [Combat Buffs](#5-combat-buffs)
6. [Support Effects](#6-support-effects)
7. [Special States](#7-special-states)
8. [Advanced Usage](#8-advanced-usage)

---

## 1. BASIC STATUS AILMENTS

### SC_STONE
**Name:** Stone / Petrify
**Effect:** DEF -50%; MDEF +25%; Element becomes Earth Lv1; Lose 1% HP/5sec (if HP>25%); Can't move/attack/use items/use skills

**Usage:**
```c
sc_start SC_STONE,30000,1;  // 30 seconds
```

**val1:** (not used)
**val2:** Caster's object ID
**val3:** Incubation time
**val4:** Remaining tick

---

### SC_FREEZE
**Name:** Frozen
**Effect:** DEF -50%; FLEE = 0; MDEF +25%; Element becomes Water Lv1; Can't move/attack/use items

**Usage:**
```c
sc_start SC_FREEZE,10000,1;  // 10 seconds
```

---

### SC_STUN
**Name:** Stunned
**Effect:** FLEE = 0; Can't move/attack/pick items/use items/use skills

**Usage:**
```c
sc_start SC_STUN,5000,1;  // 5 seconds
```

**Common Use:** Boss skills, PvP stunning

---

### SC_SLEEP
**Name:** Sleep
**Effect:** FLEE = 0; Enemy CRIT ×2; Can't move/attack/use items/use skills

**Usage:**
```c
sc_start SC_SLEEP,20000,1;  // 20 seconds
```

**Note:** Breaks when hit

---

### SC_POISON
**Name:** Poisoned
**Effect:** DEF -25%; Lose 1.5% + 2 HP/sec (if HP>25%); SP regen disabled

**Usage:**
```c
sc_start SC_POISON,60000,5;  // 60 seconds, level 5
```

**val1:** Skill level
**val2:** Caster's object ID
**val4:** Remaining tick

---

### SC_CURSE
**Name:** Cursed
**Effect:** ATK -25%; LUK = 0; Movement speed -300

**Usage:**
```c
sc_start SC_CURSE,30000,1;  // 30 seconds
```

**Note:** Can be removed with Blessing

---

### SC_SILENCE
**Name:** Silenced
**Effect:** Can't use active skills

**Usage:**
```c
sc_start SC_SILENCE,20000,1;  // 20 seconds
```

**Common Use:** Anti-caster debuff

---

### SC_BLIND
**Name:** Blinded
**Effect:** HIT -25%; FLEE -25%; Screen darkened

**Usage:**
```c
sc_start SC_BLIND,30000,1;  // 30 seconds
```

---

### SC_CONFUSION
**Name:** Confused
**Effect:** Move randomly; DEF = (STR + (INT×50))

**Usage:**
```c
sc_start SC_CONFUSION,15000,1;  // 15 seconds
```

---

### SC_BLEEDING
**Name:** Bleeding
**Effect:** HP regen disabled; SP regen disabled; Lose HP overtime

**Usage:**
```c
sc_start SC_BLEEDING,30000,5;  // 30 seconds, level 5
```

**val1:** Skill level
**val2:** Caster's object ID
**val4:** Remaining tick

---

### SC_DPOISON
**Name:** Deadly Poison
**Effect:** DEF -25%; Lose 10-15% HP/sec (if HP>25%)

**Usage:**
```c
sc_start SC_DPOISON,60000,10;  // 60 seconds, level 10
```

**Note:** More severe than SC_POISON

---

## 2. STAT BUFFS

### SC_BLESSING
**Name:** Blessing
**Effect:** Increase STR, DEX, INT by skill level; Removes Stone and Curse

**Usage:**
```c
sc_start SC_BLESSING,240000,10;  // 4 minutes, level 10 (+10 STR/DEX/INT)
```

**val1:** Skill level (stat bonus)

**Note:** If used on Undead/Demon mobs, reduces DEX/INT by 50%

---

### SC_INCREASEAGI
**Name:** Increase AGI
**Effect:** Increase AGI and movement speed

**Usage:**
```c
sc_start SC_INCREASEAGI,240000,10;  // 4 minutes, level 10
```

**val1:** Skill level

---

### SC_DECREASEAGI
**Name:** Decrease AGI
**Effect:** Decrease AGI and movement speed

**Usage:**
```c
sc_start SC_DECREASEAGI,40000,10;  // 40 seconds, level 10
```

**val1:** Skill level

---

### SC_GLORIA
**Name:** Gloria
**Effect:** LUK +30

**Usage:**
```c
sc_start SC_GLORIA,30000,1;  // 30 seconds
```

---

### SC_LOUD
**Name:** Loud Exclamation
**Effect:** STR +4

**Usage:**
```c
sc_start SC_LOUD,300000,1;  // 5 minutes
```

---

### SC_CONCENTRATE
**Name:** Attention Concentrate
**Effect:** AGI +(2+level)%; DEX +(2+level)%; Reveal hidden enemies in 3×3 area

**Usage:**
```c
sc_start SC_CONCENTRATE,60000,10;  // 60 seconds, level 10
```

---

## 3. STAT DEBUFFS

### SC_PROVOKE
**Name:** Provoke
**Effect:** DEF -(5+(5×level))%; ATK +(2+(3×level))%

**Usage:**
```c
sc_start SC_PROVOKE,30000,10;  // 30 seconds, level 10
```

**Note:** Lowers defense but increases attack

---

### SC_SIGNUMCRUCIS
**Name:** Signum Crucis
**Effect:** Decrease DEF of Undead and Demon mobs by (10+(4×level))%

**Usage:**
```c
sc_start SC_SIGNUMCRUCIS,40000,10;  // 40 seconds, level 10
```

---

### SC_QUAGMIRE
**Name:** Quagmire
**Effect:** Removes several AGI buffs; Movement speed -50%; AGI/DEX -(10×level)

**Usage:**
```c
sc_start SC_QUAGMIRE,20000,5;  // 20 seconds, level 5
```

**Removes:**
- Increase AGI
- Two-Hand Quicken
- Wind Walk
- Adrenaline Rush
- Attention Concentrate
- Cart Boost

---

## 4. ELEMENT CHANGES

### SC_ASPERSIO
**Name:** Aspersio
**Effect:** Change weapon element to HOLY

**Usage:**
```c
sc_start SC_ASPERSIO,180000,1;  // 3 minutes
```

---

### SC_BENEDICTIO
**Name:** B.S Sacramenti
**Effect:** Change armor element to HOLY

**Usage:**
```c
sc_start SC_BENEDICTIO,120000,1;  // 2 minutes
```

---

### SC_ENCPOISON
**Name:** Enchant Poison
**Effect:** Change weapon element to POISON; 2.5-3% poison chance

**Usage:**
```c
sc_start SC_ENCPOISON,180000,10;  // 3 minutes
```

---

## 5. COMBAT BUFFS

### SC_TWOHANDQUICKEN
**Name:** Two-Hand Quicken
**Effect:** ASPD +30%

**Usage:**
```c
sc_start SC_TWOHANDQUICKEN,300000,10;  // 5 minutes
```

---

### SC_ADRENALINE
**Name:** Adrenaline Rush
**Effect:** ASPD of Axe & Mace weapons ×2

**Usage:**
```c
sc_start SC_ADRENALINE,300000,5;  // 5 minutes
```

---

### SC_WEAPONPERFECTION
**Name:** Weapon Perfection
**Effect:** Ignore size penalty damage reduction

**Usage:**
```c
sc_start SC_WEAPONPERFECTION,40000,5;  // 40 seconds
```

**Note:** Small/Medium weapons deal full damage to Large monsters

---

### SC_OVERTHRUST
**Name:** Over Thrust
**Effect:** ATK +(5×level)%; 0.1% weapon break chance

**Usage:**
```c
sc_start SC_OVERTHRUST,300000,5;  // 5 minutes, level 5
```

**Note:** Axes, Maces, and Unbreakable weapons immune to breaking

---

### SC_MAXIMIZEPOWER
**Name:** Maximize Power
**Effect:** SP regen disabled; Damage always deals max damage

**Usage:**
```c
sc_start SC_MAXIMIZEPOWER,60000,1;  // 60 seconds
```

---

### SC_IMPOSITIO
**Name:** Impositio Manus
**Effect:** ATK +(5×level)

**Usage:**
```c
sc_start SC_IMPOSITIO,60000,5;  // 60 seconds, level 5 (+25 ATK)
```

---

### SC_AETERNA
**Name:** Lex Aeterna
**Effect:** Damage received ×2 (next hit only)

**Usage:**
```c
sc_start SC_AETERNA,600000,1;  // 10 minutes (until hit)
```

**Note:** Removed after taking damage once

---

## 6. SUPPORT EFFECTS

### SC_ENDURE
**Name:** Endure
**Effect:** MDEF +level; No flinch when attacked

**Usage:**
```c
sc_start SC_ENDURE,60000,10;  // 60 seconds, level 10
```

**val1:** Skill level (MDEF bonus)

---

### SC_ANGELUS
**Name:** Angelus
**Effect:** DEF +(5×level)%

**Usage:**
```c
sc_start SC_ANGELUS,300000,10;  // 5 minutes, level 10
```

---

### SC_KYRIE
**Name:** Kyrie Eleison
**Effect:** Block damage up to (MaxHP×(level×2+10)/100) or ((level/2)+5) times

**Usage:**
```c
sc_start SC_KYRIE,120000,10;  // 2 minutes, level 10
```

**Note:** Removes SC_ASSUMPTIO

---

### SC_MAGNIFICAT
**Name:** Magnificat
**Effect:** SP regeneration speed ×2

**Usage:**
```c
sc_start SC_MAGNIFICAT,30000,1;  // 30 seconds
```

---

### SC_SUFFRAGIUM
**Name:** Suffragium
**Effect:** Cast time -(15×level)%

**Usage:**
```c
sc_start SC_SUFFRAGIUM,30000,3;  // 30 seconds, level 3 (-45% cast time)
```

---

### SC_SLOWPOISON
**Name:** Slow Poison
**Effect:** Stop HP reduction from SC_POISON

**Usage:**
```c
sc_start SC_SLOWPOISON,120000,1;  // 2 minutes
```

**Note:** Doesn't cure poison, just stops HP loss

---

### SC_ENERGYCOAT
**Name:** Energy Coat
**Effect:** Damage reduction based on SP

**Usage:**
```c
sc_start SC_ENERGYCOAT,300000,5;  // 5 minutes
```

---

## 7. SPECIAL STATES

### SC_HIDING
**Name:** Hiding
**Effect:** Set OPTION_HIDE (invisible, can't be targeted)

**Usage:**
```c
sc_start SC_HIDING,300000,1;  // 5 minutes
```

**Note:** Broken by specific skills/items

---

### SC_CLOAKING
**Name:** Cloaking
**Effect:** Set OPTION_CLOAK (invisible while near walls)

**Usage:**
```c
sc_start SC_CLOAKING,300000,10;  // 5 minutes
```

---

### SC_TRICKDEAD
**Name:** Play Dead
**Effect:** HP/SP regen disabled; Removes dancing status

**Usage:**
```c
sc_start SC_TRICKDEAD,600000,1;  // 10 minutes
```

---

### SC_POISONREACT
**Name:** Poison React
**Effect:** Block poison attacks; Counter with Envenom 5

**Usage:**
```c
sc_start SC_POISONREACT,180000,10;  // 3 minutes
```

**val1:** Skill level
**val2:** Number of Envenom autocasts
**val3:** Autocast chance
**val4:** 0=Block mode, 1=Damage boost mode

---

## 8. ADVANCED USAGE

### sc_start Syntax

```c
sc_start <SC_CONSTANT>,<duration_ms>,<val1>{,<rate>,<flag>,<unit_id>};
```

**Parameters:**
- `SC_CONSTANT` - Status effect constant (e.g., SC_BLESSING)
- `duration_ms` - Duration in milliseconds
- `val1` - Primary value (usually skill level or intensity)
- `rate` - Success rate (10000 = 100%, optional, default 10000)
- `flag` - Special flags (optional)
  - `SCSTART_NOAVOID (1)` - Cannot be avoided
  - `SCSTART_NOTICKDEF (2)` - Ignore tick defense
  - `SCSTART_NOICON (4)` - Don't show status icon
  - `SCSTART_LOADED (8)` - Values pre-calculated
- `unit_id` - Target unit ID (optional, default = attached player)

---

### Examples

#### Apply Blessing with 100% Success
```c
sc_start SC_BLESSING,240000,10,10000;
```

#### Apply Poison with 50% Success Rate
```c
sc_start SC_POISON,60000,5,5000;
```

#### Apply Stone with No Icon
```c
sc_start SC_STONE,30000,1,10000,SCSTART_NOICON;
```

---

### sc_start2 / sc_start4

```c
// sc_start2: Specify val1 and val2
sc_start2 SC_POISONREACT,180000,10,5;

// sc_start4: Specify val1, val2, val3, val4
sc_start4 SC_POISON,60000,5,getcharid(3),0,gettick();
```

---

### Removing Status Effects

```c
// Remove specific status
sc_end SC_STONE;
sc_end SC_BLESSING;

// Remove all buffs
sc_end SC_ALL;
```

---

### Checking Status Effects

```c
// Check if status is active
if (getstatus(SC_STONE)) {
    mes "You are petrified!";
    sc_end SC_STONE;
}

// Check remaining time (in milliseconds)
.@time = getstatus(SC_BLESSING, 1);
mes "Blessing remaining: " + (.@time/1000) + " seconds";
```

---

## COMMON PATTERNS

### Buff NPC
```c
prontera,150,150,4	script	Buffer	4_F_KAFRA1,{
    mes "[Buffer]";
    mes "Choose your buffs:";
    next;
    switch(select("Full Buffs:Custom:Cancel")) {
    case 1:
        sc_start SC_BLESSING,240000,10;
        sc_start SC_INCREASEAGI,240000,10;
        sc_start SC_IMPOSITIO,240000,5;
        sc_start SC_GLORIA,240000,1;
        mes "Fully buffed!";
        close;
    case 2:
        // Custom menu here
        close;
    case 3:
        close;
    }
}
```

### Cure Ailments
```c
if (getstatus(SC_STONE) || getstatus(SC_FREEZE) || getstatus(SC_STUN)) {
    sc_end SC_STONE;
    sc_end SC_FREEZE;
    sc_end SC_STUN;
    mes "Ailments cured!";
}
```

### Temporary PvP Buff
```c
// 30 second combat buff
sc_start SC_TWOHANDQUICKEN,30000,10;
sc_start SC_OVERTHRUST,30000,5;
sc_start SC_WEAPONPERFECTION,30000,5;
announce "Combat buffs active for 30 seconds!",bc_self;
```

---

## DURATION REFERENCE

```c
// Common durations
1000      // 1 second
5000      // 5 seconds
10000     // 10 seconds
30000     // 30 seconds
60000     // 1 minute
120000    // 2 minutes
180000    // 3 minutes
240000    // 4 minutes
300000    // 5 minutes
600000    // 10 minutes
```

---

## TIPS & BEST PRACTICES

1. **Always use milliseconds** for duration (multiply seconds by 1000)
2. **Check existing status** before applying to avoid overwriting longer durations
3. **Use appropriate val1** values (usually skill level)
4. **Success rate** of 10000 = 100% guaranteed
5. **Combine buffs** for better player experience
6. **Clear debuffs** before important events
7. **Test durations** - some effects are very short/long
8. **Use constants** (SC_BLESSING) instead of numbers

---

## DEBUGGING

### Check All Active Status Effects
```c
for (.@i = 0; .@i < SC_MAX; .@i++) {
    if (getstatus(.@i)) {
        dispbottom "Active: " + .@i;
    }
}
```

### Display Status Duration
```c
.@time = getstatus(SC_BLESSING, 1);
if (.@time > 0) {
    dispbottom "Blessing: " + (.@time/1000) + "s remaining";
}
```

---

## SEE ALSO

- **Full Reference:** `/doc/status_change.txt` (2,920 lines, 300+ status effects)
- **KB_REF_005:** Script Commands Reference
- **KB_REF_007:** Visual Effects Reference
- **KB_EXAMPLE_001:** NPC Script Examples

---

*Last Updated: 2024-10-24*
*rAthena Documentation - Status Effects*
---
kb_id: KB_REF_007
kb_type: reference
kb_category: visual
kb_subcategory: effects
kb_keywords: [visual effects, effect, EF_, specialeffect, specialeffect2, client effects, animations, particles, sound effects, @effect]
kb_related: [KB_REF_005, KB_REF_006]
kb_difficulty: basic
kb_version: rAthena_2025
kb_last_updated: 2025-10-23
kb_use_case: [npc_scripting, item_effects, skill_effects, visual_enhancement]
---

# rAthena Visual Effects Reference

Complete reference for the most commonly used client-side visual effects in rAthena.

## Overview

Visual effects (also called "client effects") are animations, particles, and sounds that appear on the client screen. They enhance the player experience and provide visual feedback for actions, buffs, skills, and events.

**Script Usage:**
```c
// Show effect on NPC
specialeffect EF_MVP;

// Show effect on player
specialeffect2 EF_HEAL;

// Show effect on specific player by ID
specialeffect(EF_BLESSING, AREA, <account_id>);
```

**Testing:**
```c
// In-game command to test effects
@effect <number>
```

**Total Effects:** 968+ effects available (IDs 0-967+)

---

## TABLE OF CONTENTS

1. [Combat & Hit Effects](#1-combat--hit-effects)
2. [Magic & Elemental Effects](#2-magic--elemental-effects)
3. [Buff & Support Effects](#3-buff--support-effects)
4. [Status & Ailment Effects](#4-status--ailment-effects)
5. [Movement & Warp Effects](#5-movement--warp-effects)
6. [Special & Event Effects](#6-special--event-effects)
7. [Auras & Glows](#7-auras--glows)
8. [Usage Examples](#8-usage-examples)

---

## 1. COMBAT & HIT EFFECTS

### Basic Hits

| ID | Constant | Description |
|----|----------|-------------|
| 0 | EF_HIT1 | Regular Hit |
| 1 | EF_HIT2 | Bash |
| 2-5 | EF_HIT3-6 | Melee Skill Hits |
| 81 | EF_PIERCE | Pierce Hit |
| 17 | EF_MAGNUMBREAK | Magnum Break |
| 70 | EF_BRANDISHSPEAR | Brandish Spear |
| 73 | EF_BOWLINGBASH | Bowling Bash (Blue/White Aura) |

**Usage:**
```c
specialeffect2 EF_HIT1;  // Show hit on player
specialeffect EF_MAGNUMBREAK;  // Show on NPC
```

---

### Projectiles & Attacks

| ID | Constant | Description |
|----|----------|-------------|
| 64 | EF_ARROWSHOT | Arrow Shot (Purple/Yellow Light) |
| 80 | EF_SPEARBMR | Spear Boomerang |
| 49 | EF_FIREHIT | Firebolt/Wall Hit |
| 50 | EF_FIRESPLASHHIT | Spinning Fire |
| 51 | EF_COLDHIT | Ice Elemental Hit |
| 52 | EF_WINDHIT | Wind Elemental Hit |
| 53 | EF_POISONHIT | Poison Hit (Purple Smoke) |

---

## 2. MAGIC & ELEMENTAL EFFECTS

### Fire Spells

| ID | Constant | Description |
|----|----------|-------------|
| 24 | EF_FIREBALL | Fire Ball |
| 25 | EF_FIREWALL | Fire Wall |
| 214 | EF_LORD | Lord of Vermillion |
| 168 | EF_METEORSTORM | Meteor Storm |

**Usage:**
```c
specialeffect EF_FIREBALL;
sleep 500;
specialeffect EF_FIREHIT;
```

---

### Ice/Water Spells

| ID | Constant | Description |
|----|----------|-------------|
| 27 | EF_FROSTDIVER | Frost Diver (Traveling) |
| 28 | EF_FROSTDIVER2 | Frost Diver (Impact) |
| 74 | EF_ICEWALL | Ice Wall |
| 89 | EF_STORMGUST | Storm Gust |
| 107 | EF_WATERBALL | Water Ball |

---

### Lightning/Wind Spells

| ID | Constant | Description |
|----|----------|-------------|
| 29 | EF_LIGHTBOLT | Lightning Bolt |
| 30 | EF_THUNDERSTORM | Thunder Storm |
| 214 | EF_LORD | Lord of Vermillion |

---

### Earth Spells

| ID | Constant | Description |
|----|----------|-------------|
| 79 | EF_EARTHSPIKE | Earth Spike |
| 131 | EF_EARTHHIT | Earth Hit |
| 119 | EF_QUAGMIRE | Quagmire |

---

### Holy/Shadow Magic

| ID | Constant | Description |
|----|----------|-------------|
| 15 | EF_SOULSTRIKE | Soul Strike |
| 82 | EF_TURNUNDEAD | Turn Undead |
| 83 | EF_SANCTUARY | Sanctuary |
| 108 | EF_MAGNUS | Magnus Exorcismus |
| 33 | EF_RUWACH | Ruwach |

---

### Cast Auras

| ID | Constant | Description |
|----|----------|-------------|
| 12 | EF_BEGINSPELL | Yellow Cast Aura |
| 54 | EF_BEGINSPELL2 | Water Element Cast |
| 55 | EF_BEGINSPELL3 | Fire Element Cast |
| 56 | EF_BEGINSPELL4 | Earth Element Cast |
| 57 | EF_BEGINSPELL5 | Wind Element Cast |
| 58 | EF_BEGINSPELL6 | Holy Element Cast |
| 59 | EF_BEGINSPELL7 | Poison Element Cast |

**Usage:**
```c
specialeffect2 EF_BEGINSPELL3;  // Fire cast aura
sleep 2000;
specialeffect2 EF_FIREBALL;
```

---

## 3. BUFF & SUPPORT EFFECTS

### Stat Buffs

| ID | Constant | Description |
|----|----------|-------------|
| 42 | EF_BLESSING | Blessing |
| 37 | EF_INCAGILITY | AGI Up |
| 38 | EF_DECAGILITY | AGI Down |
| 43 | EF_INCAGIDEX | Dex + Agi Up |
| 75 | EF_GLORIA | Gloria |
| 67 | EF_PROVOKE | Provoke |

---

### Support Skills

| ID | Constant | Description |
|----|----------|-------------|
| 41 | EF_ANGELUS | Angelus |
| 76 | EF_MAGNIFICAT | Magnificat |
| 84 | EF_IMPOSITIO | Impositio Manus |
| 85 | EF_LEXAETERNA | Lex Aeterna |
| 86 | EF_ASPERSIO | Aspersio |
| 87 | EF_LEXDIVINA | Lex Divina |
| 88 | EF_SUFFRAGIUM | Suffragium |
| 11 | EF_ENDURE | Endure |

---

### Healing

| ID | Constant | Description |
|----|----------|-------------|
| 7 | EF_EXIT | Item Heal Effect |
| 9 | EF_ENHANCE | Different Heal Type |
| 14 | EF_HEALSP | Blue Restoring (SP) |
| 66 | EF_CURE | Cure |
| 77 | EF_RESURRECTION | Resurrection |
| 78 | EF_RECOVERY | Status Recovery |

**Usage:**
```c
// Healing effect
specialeffect2 EF_EXIT;
percentheal 100,100;
```

---

## 4. STATUS & AILMENT EFFECTS

### Status Ailments

| ID | Constant | Description |
|----|----------|-------------|
| 23 | EF_STONECURSE | Stone Curse |
| 20 | EF_PATTACK | Envenom/Poison |
| 21 | EF_DETOXICATION | Detoxify |
| 18 | EF_STEAL | Steal |
| 40 | EF_SIGNUM | Signum Crucis |
| 69 | EF_SKIDTRAP | Skid Trap |

---

### Visual Indicators

| ID | Constant | Description |
|----|----------|-------------|
| 60 | EF_LOCKON | Cast Target Circle |
| 22 | EF_SIGHT | Sight |
| 62 | EF_SIGHTRASHER | Sight Rasher |
| 66 | EF_CURE | Cure |

---

## 5. MOVEMENT & WARP EFFECTS

### Warp & Teleport

| ID | Constant | Description |
|----|----------|-------------|
| 6 | EF_ENTRY | Being Warped |
| 8 | EF_WARP | Yellow Ripple Effect |
| 34 | EF_TELEPORTATION | Teleport Animation |
| 35 | EF_READYPORTAL | Warp Portal (Ready) |
| 36 | EF_PORTAL | Warp Portal |
| 61 | EF_WARPZONE | NPC Warp |

**Usage:**
```c
specialeffect2 EF_WARP;
sleep 500;
warp "prontera",156,191;
```

---

### Movement Effects

| ID | Constant | Description |
|----|----------|-------------|
| 16 | EF_BASH | Hide |
| 69 | EF_SKIDTRAP | Skid Trap |

---

## 6. SPECIAL & EVENT EFFECTS

### MVP & Special

| ID | Constant | Description |
|----|----------|-------------|
| 68 | EF_MVP | MVP Banner |
| 10 | EF_COIN | Mammonite (Coins) |
| 63 | EF_BARRIER | Moonlight Sphere |
| 65 | EF_INVENOM | Power Absorb |

---

### Environmental

| ID | Constant | Description |
|----|----------|-------------|
| 44 | EF_SMOKE | Little Fog Smoke |
| 45 | EF_FIREFLY | Faint Little Balls |
| 46 | EF_SANDWIND | Sand Wind |
| 47 | EF_TORCH | Torch |
| 48 | EF_SPRAYPOND | Small Glass Piece |

---

### Geometric Effects

| ID | Constant | Description |
|----|----------|-------------|
| 13 | EF_GLASSWALL | Blue Box |
| 71 | EF_CONE | Spiral White Balls (Small) |
| 72 | EF_SPHERE | Spiral White Balls (Large) |

---

## 7. AURAS & GLOWS

### Light Effects

| ID | Constant | Description |
|----|----------|-------------|
| 132 | EF_LIGHTBLADE | Light Blade Aura |
| 244 | EF_GLASSWALL3 | Glass Wall (Clear) |
| 336 | EF_LIGHTSPHERE | Light Sphere |

---

### Colored Auras

| ID | Constant | Description |
|----|----------|-------------|
| 321 | EF_AURA_RED | Red Aura |
| 322 | EF_AURA_BLUE | Blue Aura |
| 323 | EF_AURA_GREEN | Green Aura |
| 324 | EF_AURA_YELLOW | Yellow Aura |

---

## 8. USAGE EXAMPLES

### Basic Effect Commands

```c
// Show effect on NPC location
specialeffect EF_MVP;

// Show effect on player
specialeffect2 EF_BLESSING;

// Show effect on specific player by account ID
specialeffect(EF_HEAL, AREA, getcharid(3));

// Show effect on specific coordinate
specialeffect(EF_FIREBALL, AREA, "prontera", 150, 150);
```

---

### Multiple Effects Sequence

```c
// Cast spell with visual feedback
specialeffect2 EF_BEGINSPELL3;  // Fire cast aura
sleep 2000;
specialeffect2 EF_FIREBALL;     // Fire ball
sleep 500;
specialeffect2 EF_FIREHIT;      // Impact
```

---

### Buff Application

```c
// Apply blessing with effect
specialeffect2 EF_BLESSING;
sc_start SC_BLESSING,240000,10;
mes "You have been blessed!";
```

---

### Healing with Effect

```c
// Heal player with visual feedback
specialeffect2 EF_EXIT;
percentheal 100,100;
mes "Fully healed!";
```

---

### Warp with Effect

```c
// Warp with visual effect
mes "Warping you now!";
close2;
specialeffect2 EF_WARP;
sleep 1000;
warp "prontera",156,191;
end;
```

---

### MVP Kill Effect

```c
// Announce MVP kill with effect
OnMVPDead:
    announce strcharinfo(0) + " has killed the MVP!",bc_all;
    specialeffect2 EF_MVP, AREA, getcharid(3);
    end;
```

---

### Area Effect

```c
// Show effect to all players in area
- script AreaEffect -1,{
OnInit:
    while (1) {
        specialeffect(EF_SANCTUARY, AREA, "prontera", 156, 191);
        sleep 5000;
    }
}
```

---

### Quest Complete Effect

```c
// Quest completion with celebration
mes "[Quest NPC]";
mes "Quest complete!";
close2;
specialeffect2 EF_MVP;
specialeffect2 EF_RESURRECTION;
getexp 10000,5000;
end;
```

---

### Buff NPC with Effects

```c
prontera,150,150,4	script	Buffer	4_F_KAFRA1,{
    mes "[Buffer]";
    mes "Would you like buffs?";
    next;
    if (select("Yes:No") == 2) close;

    // Visual feedback for each buff
    mes "Blessing...";
    specialeffect2 EF_BLESSING;
    sc_start SC_BLESSING,240000,10;
    sleep 500;

    mes "Increase AGI...";
    specialeffect2 EF_INCAGILITY;
    sc_start SC_INCREASEAGI,240000,10;
    sleep 500;

    mes "All done!";
    specialeffect2 EF_MAGNIFICAT;
    close;
}
```

---

### Item Effect Script

```c
// In item_db.yml Script field
Script: |
  specialeffect2 EF_EXIT;
  percentheal 100,100;
```

---

### Continuous Effect Loop

```c
// Create ambient effect
- script AmbientEffects -1,{
OnInit:
    initnpctimer;
    end;

OnTimer5000:
    specialeffect(EF_FIREFLY, AREA, "prontera", 156, 191);
    initnpctimer;
    end;
}
```

---

## EFFECT FLAGS

When using `specialeffect(effect, flag, ...)`:

**Flags:**
- `AREA` (0) - Show to all players in area
- `SELF` (1) - Show to invoking player only

```c
// Show to everyone
specialeffect(EF_MVP, AREA);

// Show to self only
specialeffect(EF_BLESSING, SELF);
```

---

## TESTING EFFECTS

### In-Game Testing

```c
// As GM, use @effect command
@effect 68  // Test EF_MVP

// Loop through effects to find what you want
@effect 0
@effect 1
@effect 2
// ... etc
```

---

### Test Script

```c
prontera,155,185,4	script	Effect Tester	4_M_ALCHE_C,{
    mes "[Effect Tester]";
    mes "Enter effect number (0-967):";
    input .@effect,0,967;
    specialeffect2 .@effect;
    dispbottom "Effect " + .@effect + " displayed.";
    close;
}
```

---

## PERFORMANCE TIPS

1. **Don't spam effects** - Can cause client lag
2. **Use sleep between effects** - Prevents visual overload
3. **Test effects** before deploying - Some look better than others
4. **Consider client version** - Older clients have fewer effects
5. **Use appropriate effects** - Match effect to action (heal for heal, fire for fire, etc.)
6. **Optimize loops** - Don't create continuous effect loops on busy maps

---

## COMMON EFFECT COMBINATIONS

### Level Up Celebration
```c
specialeffect2 EF_MVP;
specialeffect2 EF_RESURRECTION;
specialeffect2 EF_GLORIA;
```

### Magic Attack Sequence
```c
specialeffect2 EF_BEGINSPELL3;  // Cast
sleep 1500;
specialeffect EF_FIREBALL;       // Projectile
sleep 500;
specialeffect EF_FIREHIT;        // Impact
```

### Buff Combo
```c
specialeffect2 EF_BLESSING;
specialeffect2 EF_INCAGILITY;
specialeffect2 EF_MAGNIFICAT;
```

### Warp Sequence
```c
specialeffect2 EF_BEGINSPELL;
sleep 2000;
specialeffect2 EF_WARP;
sleep 500;
// warp here
```

---

## EFFECT CATEGORIES SUMMARY

| Category | Effect Count | ID Range |
|----------|--------------|----------|
| Combat | 50+ | 0-100 |
| Magic | 80+ | 15-250 |
| Buffs | 40+ | 37-88 |
| Status | 30+ | 18-120 |
| Movement | 10+ | 6-69 |
| Special | 100+ | 68-400 |
| Modern (Extended) | 568+ | 400-967 |

---

## SEE ALSO

- **Full List:** `/doc/effect_list.md` (968+ effects)
- **KB_REF_005:** Script Commands Reference
- **KB_REF_006:** Status Effects Reference
- **KB_EXAMPLE_001:** NPC Script Examples

---

## DEBUGGING

### Display Effect Number
```c
dispbottom "Showing effect: EF_MVP (" + EF_MVP + ")";
specialeffect2 EF_MVP;
```

### Log All Effects
```c
for (.@i = 0; .@i < 100; .@i++) {
    dispbottom "Effect " + .@i;
    specialeffect2 .@i;
    sleep 1000;
}
```

---

*Last Updated: 2025-10-23*
*rAthena Documentation - Visual Effects*
