# 03_DATA_MODELS.md
<!-- repo: rathena | branch: claude/github-to-kb-converter-0137h2Ti2PFSsGmn6Xrp3xko | commit: 721d46e | generated: 2025-11-28 -->
<!-- tags: database, schema, tables, yaml, data, models -->

## Contents
- [MySQL Database Schema](#mysql-database-schema)
- [YAML Data Format](#yaml-data-format)
- [Core Data Structures](#core-data-structures)
- [Enumerations](#enumerations)

---

## MySQL Database Schema
<!-- chunk: 03-mysql | keywords: sql, tables, schema -->

### Installation Files

| File | Size | Description |
|------|------|-------------|
| `main.sql` | 41 KB | Core character/guild/party tables |
| `logs.sql` | 7 KB | Event logging tables |
| `web.sql` | 1.3 KB | Web server tables |
| `item_db_re_equip.sql` | 3.1 MB | Renewal equipment items |
| `mob_db_re.sql` | 1.5 MB | Renewal monsters |
| `mob_skill_db_re.sql` | 1.9 MB | Monster skills |

### Account Tables (Login Server)
<!-- chunk: 03-login-tables | keywords: login, account, ipban -->

#### login
```sql
CREATE TABLE `login` (
  `account_id` int(11) unsigned NOT NULL auto_increment,
  `userid` varchar(23) NOT NULL default '',
  `user_pass` varchar(32) NOT NULL default '',
  `sex` enum('M','F','S') NOT NULL default 'M',
  `email` varchar(39) NOT NULL default '',
  `group_id` tinyint(3) NOT NULL default '0',
  `state` int(11) unsigned NOT NULL default '0',
  `unban_time` int(11) unsigned NOT NULL default '0',
  `expiration_time` int(11) unsigned NOT NULL default '0',
  `logincount` mediumint(9) unsigned NOT NULL default '0',
  `lastlogin` datetime DEFAULT NULL,
  `last_ip` varchar(100) NOT NULL default '',
  `birthdate` date DEFAULT NULL,
  `character_slots` tinyint(3) unsigned NOT NULL default '0',
  `pincode` varchar(4) NOT NULL default '',
  `pincode_change` int(11) unsigned NOT NULL default '0',
  `vip_time` int(11) unsigned NOT NULL default '0',
  `old_group` tinyint(3) NOT NULL default '0',
  `web_auth_token` varchar(17) DEFAULT NULL,
  `web_auth_token_enabled` tinyint(2) NOT NULL default '0',
  PRIMARY KEY (`account_id`),
  UNIQUE KEY `name` (`userid`)
) ENGINE=MyISAM;
```

#### ipbanlist
```sql
CREATE TABLE `ipbanlist` (
  `list` varchar(15) NOT NULL default '',
  `btime` datetime NOT NULL,
  `rtime` datetime NOT NULL,
  `reason` varchar(255) NOT NULL default '',
  PRIMARY KEY (`list`,`btime`)
) ENGINE=MyISAM;
```

### Character Tables (Char Server)
<!-- chunk: 03-char-tables | keywords: char, character, inventory, skill -->

#### char
```sql
CREATE TABLE `char` (
  `char_id` int(11) unsigned NOT NULL auto_increment,
  `account_id` int(11) unsigned NOT NULL default '0',
  `char_num` tinyint(1) NOT NULL default '0',
  `name` varchar(30) NOT NULL DEFAULT '',
  `class` smallint(6) unsigned NOT NULL default '0',
  `base_level` smallint(6) unsigned NOT NULL default '1',
  `job_level` smallint(6) unsigned NOT NULL default '1',
  `base_exp` bigint(20) unsigned NOT NULL default '0',
  `job_exp` bigint(20) unsigned NOT NULL default '0',
  `zeny` int(11) unsigned NOT NULL default '0',
  `str` smallint(4) unsigned NOT NULL default '0',
  `agi` smallint(4) unsigned NOT NULL default '0',
  `vit` smallint(4) unsigned NOT NULL default '0',
  `int` smallint(4) unsigned NOT NULL default '0',
  `dex` smallint(4) unsigned NOT NULL default '0',
  `luk` smallint(4) unsigned NOT NULL default '0',
  `max_hp` int(11) unsigned NOT NULL default '0',
  `hp` int(11) unsigned NOT NULL default '0',
  `max_sp` int(11) unsigned NOT NULL default '0',
  `sp` int(11) unsigned NOT NULL default '0',
  `status_point` int(11) unsigned NOT NULL default '0',
  `skill_point` int(11) unsigned NOT NULL default '0',
  `party_id` int(11) unsigned NOT NULL default '0',
  `guild_id` int(11) unsigned NOT NULL default '0',
  `pet_id` int(11) unsigned NOT NULL default '0',
  `homun_id` int(11) unsigned NOT NULL default '0',
  `hair` tinyint(4) unsigned NOT NULL default '0',
  `hair_color` smallint(5) unsigned NOT NULL default '0',
  `last_map` varchar(11) NOT NULL default '',
  `last_x` smallint(4) unsigned NOT NULL default '53',
  `last_y` smallint(4) unsigned NOT NULL default '111',
  `save_map` varchar(11) NOT NULL default '',
  `save_x` smallint(4) unsigned NOT NULL default '53',
  `save_y` smallint(4) unsigned NOT NULL default '111',
  `online` tinyint(2) NOT NULL default '0',
  `sex` ENUM('M','F') NOT NULL,
  `last_login` datetime DEFAULT NULL,
  PRIMARY KEY (`char_id`),
  UNIQUE KEY `name_key` (`name`),
  KEY `account_id` (`account_id`),
  KEY `guild_id` (`guild_id`),
  KEY `online` (`online`)
) ENGINE=MyISAM AUTO_INCREMENT=150000;
```

#### inventory
```sql
CREATE TABLE `inventory` (
  `id` int(11) NOT NULL auto_increment,
  `char_id` int(11) NOT NULL default '0',
  `nameid` int(10) unsigned NOT NULL default '0',
  `amount` int(11) NOT NULL default '0',
  `equip` int(11) unsigned NOT NULL default '0',
  `identify` smallint(6) NOT NULL default '0',
  `refine` tinyint(3) unsigned NOT NULL default '0',
  `attribute` tinyint(4) NOT NULL default '0',
  `card0` int(10) unsigned NOT NULL default '0',
  `card1` int(10) unsigned NOT NULL default '0',
  `card2` int(10) unsigned NOT NULL default '0',
  `card3` int(10) unsigned NOT NULL default '0',
  `expire_time` int(11) unsigned NOT NULL default '0',
  `bound` tinyint(3) unsigned NOT NULL default '0',
  `unique_id` bigint(20) unsigned NOT NULL default '0',
  PRIMARY KEY (`id`),
  KEY `char_id` (`char_id`)
) ENGINE=MyISAM;
```

#### skill
```sql
CREATE TABLE `skill` (
  `char_id` int(11) unsigned NOT NULL default '0',
  `id` smallint(11) unsigned NOT NULL default '0',
  `lv` tinyint(4) unsigned NOT NULL default '0',
  `flag` tinyint(1) unsigned NOT NULL default '0',
  PRIMARY KEY (`char_id`,`id`)
) ENGINE=MyISAM;
```

### Guild Tables
<!-- chunk: 03-guild-tables | keywords: guild, alliance, castle, storage -->

#### guild
```sql
CREATE TABLE `guild` (
  `guild_id` int(11) unsigned NOT NULL auto_increment,
  `name` varchar(24) NOT NULL default '',
  `char_id` int(11) unsigned NOT NULL default '0',
  `master` varchar(24) NOT NULL default '',
  `guild_lv` tinyint(6) unsigned NOT NULL default '0',
  `connect_member` tinyint(6) unsigned NOT NULL default '0',
  `max_member` tinyint(6) unsigned NOT NULL default '0',
  `average_lv` smallint(6) unsigned NOT NULL default '1',
  `exp` bigint(20) unsigned NOT NULL default '0',
  `next_exp` bigint(20) unsigned NOT NULL default '0',
  `skill_point` tinyint(11) unsigned NOT NULL default '0',
  `mes1` varchar(60) NOT NULL default '',
  `mes2` varchar(120) NOT NULL default '',
  `emblem_len` int(11) unsigned NOT NULL default '0',
  `emblem_id` int(11) unsigned NOT NULL default '0',
  `emblem_data` blob,
  PRIMARY KEY (`guild_id`,`char_id`),
  UNIQUE KEY `guild_id` (`guild_id`)
) ENGINE=MyISAM;
```

#### guild_castle
```sql
CREATE TABLE `guild_castle` (
  `castle_id` int(11) unsigned NOT NULL default '0',
  `guild_id` int(11) unsigned NOT NULL default '0',
  `economy` int(11) unsigned NOT NULL default '0',
  `defense` int(11) unsigned NOT NULL default '0',
  `triggerE` int(11) unsigned NOT NULL default '0',
  `triggerD` int(11) unsigned NOT NULL default '0',
  `nextTime` int(11) unsigned NOT NULL default '0',
  `payTime` int(11) unsigned NOT NULL default '0',
  `createTime` int(11) unsigned NOT NULL default '0',
  `visibleC` int(11) unsigned NOT NULL default '0',
  PRIMARY KEY (`castle_id`)
) ENGINE=MyISAM;
```

### Logging Tables
<!-- chunk: 03-log-tables | keywords: logs, picklog, zenylog, chatlog -->

#### picklog
```sql
CREATE TABLE `picklog` (
  `id` int(11) NOT NULL auto_increment,
  `time` datetime NOT NULL,
  `char_id` int(11) NOT NULL default '0',
  `type` enum('M','P','L','T','V','S','N','C','A','R','G','E','B','O','I','X','D','U','$','F','Y','Z','Q','H','J','W','0','1','2','3') NOT NULL default 'P',
  `nameid` int(10) unsigned NOT NULL default '0',
  `amount` int(11) NOT NULL default '1',
  `refine` tinyint(3) unsigned NOT NULL default '0',
  `card0` int(10) unsigned NOT NULL default '0',
  `card1` int(10) unsigned NOT NULL default '0',
  `card2` int(10) unsigned NOT NULL default '0',
  `card3` int(10) unsigned NOT NULL default '0',
  `map` varchar(11) NOT NULL default '',
  PRIMARY KEY (`id`),
  INDEX (`type`)
) ENGINE=MyISAM;
```

**Picklog Type Codes:**
- `M` = Monster Drop
- `P` = Player Drop/Take
- `L` = Loot Drop/Take
- `T` = Trade
- `V` = Vending
- `S` = Shop
- `N` = NPC
- `C` = Consumable
- `A` = Admin
- `R` = Storage
- `G` = Guild Storage

#### zenylog
```sql
CREATE TABLE `zenylog` (
  `id` int(11) NOT NULL auto_increment,
  `time` datetime NOT NULL,
  `char_id` int(11) NOT NULL default '0',
  `src_id` int(11) NOT NULL default '0',
  `type` enum('T','V','P','M','S','N','D','C','A','E','I','B','K','J','X','0','2') NOT NULL default 'S',
  `amount` int(11) NOT NULL default '0',
  `map` varchar(11) NOT NULL default '',
  PRIMARY KEY (`id`)
) ENGINE=MyISAM;
```

---

## YAML Data Format
<!-- chunk: 03-yaml | keywords: yaml, database, items, mobs -->

### Standard YAML Structure

```yaml
Header:
  Type: <DB_TYPE>
  Version: <version>

Body:
  - <entry1>
  - <entry2>

Footer:
  Imports:
  - Path: <import_path>
    Mode: <Renewal|Prerenewal>
```

### Item Database (db/item_db.yml)
<!-- chunk: 03-item-yaml | keywords: item, equipment, weapon, armor -->

```yaml
Header:
  Type: ITEM_DB
  Version: 3

Body:
  - Id: 501                    # Item ID
    AegisName: RED_POTION      # Server reference name
    Name: Red Potion           # Display name
    Type: Consumable           # Item type
    Buy: 50                    # Buy price
    Sell: 25                   # Sell price
    Weight: 70                 # Weight (10 = 1.0)
    Script: |
      itemheal rand(45,65),0;
```

**Item Types:** `Healing`, `Usable`, `Etc`, `Weapon`, `Armor`, `Card`, `PetEgg`, `PetEquip`, `Ammo`, `DelayConsume`, `ShadowEquip`, `Cash`

**Equipment Locations:**
- `Head_Top`, `Head_Mid`, `Head_Low`
- `Armor`, `Left_Hand`, `Right_Hand`, `Both_Hand`
- `Garment`, `Shoes`, `Right_Accessory`, `Left_Accessory`
- `Costume_Head_Top`, `Costume_Head_Mid`, `Costume_Head_Low`
- `Costume_Garment`, `Shadow_Armor`, `Shadow_Weapon`

### Monster Database (db/mob_db.yml)
<!-- chunk: 03-mob-yaml | keywords: monster, mob, boss, mvp -->

```yaml
Header:
  Type: MOB_DB
  Version: 3

Body:
  - Id: 1002
    AegisName: PORING
    Name: Poring
    JapaneseName: Poring
    Level: 1
    Hp: 60
    BaseExp: 27
    JobExp: 20
    Attack: 8
    Attack2: 9
    Defense: 2
    MagicDefense: 5
    Str: 6
    Agi: 1
    Vit: 1
    Int: 1
    Dex: 6
    Luk: 5
    AttackRange: 1
    SkillRange: 10
    ChaseRange: 12
    Size: Medium
    Race: Plant
    Element: Water
    ElementLevel: 1
    WalkSpeed: 400
    AttackDelay: 1872
    AttackMotion: 672
    DamageMotion: 480
    Ai: 02
    Drops:
      - Item: Jellopy
        Rate: 7000
      - Item: Knife
        Rate: 100
      - Item: Sticky_Mucus
        Rate: 400
      - Item: Poring_Card
        Rate: 1
    MvpDrops:
      - Item: Old_Blue_Box
        Rate: 5000
```

### Skill Database (db/skill_db.yml)
<!-- chunk: 03-skill-yaml | keywords: skill, cast, cooldown -->

```yaml
Header:
  Type: SKILL_DB
  Version: 2

Body:
  - Id: 1
    Name: NV_BASIC
    Description: Basic Skill
    MaxLevel: 9
    Type: None
    TargetType: Passive
```

---

## Core Data Structures
<!-- chunk: 03-structs | keywords: struct, mmo, character, item -->

### Character Structure (src/common/mmo.hpp)
<!-- chunk: 03-mmo-char | keywords: mmo_charstatus, character, stats -->

```cpp
struct mmo_charstatus {
    int char_id;
    int account_id;
    int partner_id;
    int father;
    int mother;
    int child;

    unsigned int base_exp, job_exp;
    int zeny;

    short class_;
    unsigned int status_point;
    unsigned int skill_point;
    int hp, max_hp;
    int sp, max_sp;
    unsigned int option;
    short manner;
    unsigned char karma;
    short hair, hair_color, clothes_color;
    int party_id;
    int guild_id;
    int pet_id;
    int homun_id;
    int ele_id;
    int weapon;
    int shield;
    int head_top, head_mid, head_bottom;
    int robe;

    char name[NAME_LENGTH];
    unsigned int base_level, job_level;
    short str, agi, vit, int_, dex, luk;
    unsigned char slot;
    unsigned char sex;

    char last_point[MAP_NAME_LENGTH];
    char save_point[MAP_NAME_LENGTH];
    short last_point_x, last_point_y;
    short save_point_x, save_point_y;
};
```

### Item Structure
<!-- chunk: 03-item-struct | keywords: item, inventory, equip -->

```cpp
struct item {
    int id;
    unsigned short nameid;
    short amount;
    unsigned int equip;
    char identify;
    char refine;
    char attribute;
    unsigned short card[MAX_SLOTS];
    unsigned int expire_time;
    char favorite;
    unsigned char bound;
    uint64 unique_id;
    struct s_item_randomoption option[MAX_ITEM_RDM_OPT];
    uint8 enchantgrade;
};
```

### Block List Structure (src/map/map.hpp)
<!-- chunk: 03-blocklist | keywords: block_list, unit, npc, mob -->

```cpp
struct block_list {
    int id;
    int16 m;       // Map index
    int16 x, y;    // Coordinates
    enum bl_type type;
    struct block_list *next, *prev;
};

enum bl_type {
    BL_NUL   = 0x000,
    BL_PC    = 0x001,  // Player
    BL_MOB   = 0x002,  // Monster
    BL_PET   = 0x004,  // Pet
    BL_HOM   = 0x008,  // Homunculus
    BL_MER   = 0x010,  // Mercenary
    BL_ITEM  = 0x020,  // Floor item
    BL_SKILL = 0x040,  // Skill unit
    BL_NPC   = 0x080,  // NPC
    BL_CHAT  = 0x100,  // Chat room
    BL_ELEM  = 0x200,  // Elemental
    BL_ALL   = 0xFFF
};
```

---

## Enumerations
<!-- chunk: 03-enums | keywords: enum, constants, types -->

### Job Classes (src/common/mmo.hpp)
<!-- chunk: 03-jobs | keywords: job, class, novice, knight -->

| ID | Class Name | Description |
|----|------------|-------------|
| 0 | JOB_NOVICE | Novice |
| 1 | JOB_SWORDMAN | Swordman |
| 2 | JOB_MAGE | Mage |
| 3 | JOB_ARCHER | Archer |
| 4 | JOB_ACOLYTE | Acolyte |
| 5 | JOB_MERCHANT | Merchant |
| 6 | JOB_THIEF | Thief |
| 7 | JOB_KNIGHT | Knight |
| 8 | JOB_PRIEST | Priest |
| 9 | JOB_WIZARD | Wizard |
| 10 | JOB_BLACKSMITH | Blacksmith |
| 11 | JOB_HUNTER | Hunter |
| 12 | JOB_ASSASSIN | Assassin |

### Status Effects (src/map/status.hpp)
<!-- chunk: 03-status-effects | keywords: sc, status, buff, debuff -->

| ID | Status | Description |
|----|--------|-------------|
| SC_PROVOKE | Provoke | Increased ATK, decreased DEF |
| SC_ENDURE | Endure | Cannot be interrupted |
| SC_TWOHANDQUICKEN | Two-Hand Quicken | Increased ASPD |
| SC_CONCENTRATE | Concentration | Increased AGI/DEX |
| SC_HIDING | Hiding | Hidden from view |
| SC_CLOAKING | Cloaking | Hidden, can move |
| SC_ENCPOISON | Poison Weapon | Weapon adds poison |
| SC_POISONREACT | Poison React | Counter poison |
| SC_QUAGMIRE | Quagmire | Slowed movement |
| SC_SIGHT | Sight | Reveal hidden units |
| SC_BLESSING | Blessing | Increased STR/INT/DEX |
| SC_INCREASEAGI | Increase AGI | Increased AGI/speed |

### Elements (src/map/battle.hpp)
<!-- chunk: 03-elements | keywords: element, fire, water, earth -->

| ID | Element | Description |
|----|---------|-------------|
| 0 | ELE_NEUTRAL | Neutral |
| 1 | ELE_WATER | Water |
| 2 | ELE_EARTH | Earth |
| 3 | ELE_FIRE | Fire |
| 4 | ELE_WIND | Wind |
| 5 | ELE_POISON | Poison |
| 6 | ELE_HOLY | Holy |
| 7 | ELE_DARK | Shadow |
| 8 | ELE_GHOST | Ghost |
| 9 | ELE_UNDEAD | Undead |

### Races (src/map/battle.hpp)
<!-- chunk: 03-races | keywords: race, monster, demihuman -->

| ID | Race | Description |
|----|------|-------------|
| 0 | RC_FORMLESS | Formless |
| 1 | RC_UNDEAD | Undead |
| 2 | RC_BRUTE | Brute |
| 3 | RC_PLANT | Plant |
| 4 | RC_INSECT | Insect |
| 5 | RC_FISH | Fish |
| 6 | RC_DEMON | Demon |
| 7 | RC_DEMIHUMAN | Demi-Human |
| 8 | RC_ANGEL | Angel |
| 9 | RC_DRAGON | Dragon |

---

## Quick Links

- Architecture: → See [[01_ARCHITECTURE]]
- API Functions: → See [[02_CORE_API]]
- Configuration: → See [[05_CONFIG]]
- Examples: → See [[07_EXAMPLES]]
