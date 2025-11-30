# rAthena Complete Knowledge Base v13.0
## 8-FILE COMPREHENSIVE RAG-OPTIMIZED REFERENCE

<!-- RAG_CHUNK_ID: master_index_v13 -->
<!-- RAG_KEYWORDS: rathena, knowledge base, index, overview, architecture, quick reference -->
<!-- VERSION: 13.0 MERGED EDITION -->
<!-- INCLUDES: kb_v9_final + kb_ultimate + kb_complete + script_commands_optimized + Rathena_Source_Data -->

---

## VERSION COMPARISON TABLE

| Metric | kb_v9_final | kb_final_8 v12 | kb_final_8 v13 (CURRENT) |
|--------|-------------|----------------|--------------------------|
| **Total Files** | 9 | 8 | 8 |
| **Total Lines** | 92,448 | 101,402 | **143,038** |
| **Total Size** | 2.8 MB | 2.9 MB | **4.6 MB** |
| **Script Commands** | 16,070 lines | 19,833 lines | **30,061 lines** |
| **Source Tutorials** | 35,436 lines | 51,079 lines | **82,487 lines** |
| **Status Effects** | 11,982 lines | 12,662 lines | 12,662 lines |
| **Item Bonuses** | 5,262 lines | 5,762 lines | 5,762 lines |
| **Game Mechanics** | 3,292 lines | 4,317 lines | 4,317 lines |
| **Content Creation** | 5,107 lines | 6,168 lines | 6,168 lines |
| **AT Commands** | N/A | 1,250 lines | 1,250 lines |
| **RAG Optimized** | Partial | Yes | **Full** |

### Source Files Merged
- ✅ kb_v9_final (9 files, 92K lines)
- ✅ kb_ultimate (14 files, 7.6K lines)
- ✅ kb_complete (24 files, 100K lines)
- ✅ script_commands_optimized.md (10,222 lines)
- ✅ Rathena_Source_Data.md (31,401 lines)

---

## STATISTICS

- **Total Lines**: 143,038
- **Total Size**: 4.6 MB
- **Total Files**: 8 documentation files
- **Script Commands**: 767+ BUILDIN_FUNC implementations
- **Status Effects**: 1,038 SC_* constants
- **Item Bonuses**: 263+ bonus types
- **AT Commands**: 287 @commands
- **Map Flags**: 84 MF_* constants
- **YAML Databases**: 180 files documented
- **Source Tutorials**: 420+ sections
- **Code Examples**: 500+ working snippets

---

## FILE INDEX

| # | File | Lines | Size | Content |
|---|------|-------|------|---------|
| 1 | 01_MASTER_INDEX.md | ~350 | 16K | Quick reference, architecture, comparison |
| 2 | 02_SCRIPT_COMMANDS.md | 30,061 | 864K | ALL 767+ script commands + compact ref |
| 3 | 03_STATUS_EFFECTS.md | 12,662 | 196K | ALL 1,038 SC_* status effects |
| 4 | 04_ITEM_BONUSES.md | 5,762 | 93K | ALL 263+ item bonuses |
| 5 | 05_GAME_MECHANICS.md | 4,317 | 137K | Job system, map flags, server config |
| 6 | 06_CONTENT_CREATION.md | 6,168 | 141K | Item groups, quests, NPC patterns, YAML |
| 7 | 07_SOURCE_DEVELOPMENT.md | 82,487 | 3.2M | C++ dev, tutorials, wiki reference |
| 8 | 08_AT_COMMANDS.md | 1,250 | 26K | ALL 287 @commands |

---

## RAG OPTIMIZATION FEATURES

<!-- RAG_CHUNK: rag_features -->

### Chunking Strategy
```
Each file uses semantic RAG chunks:
- <!-- RAG_CHUNK: chunk_name --> markers
- Semantic grouping by topic
- Cross-reference links between files
- Keyword tags for retrieval
```

### How to Use with RAG Systems
1. **Load relevant file(s)** based on query keywords
2. **Use chunk markers** to extract specific sections
3. **Follow cross-references** for related content
4. **Search by tags** at end of each file

### File Selection Guide
| Query Type | Primary File | Secondary |
|------------|--------------|-----------|
| Script command syntax | 02_SCRIPT_COMMANDS | 06_CONTENT_CREATION |
| Status effect info | 03_STATUS_EFFECTS | 02_SCRIPT_COMMANDS |
| Item bonus syntax | 04_ITEM_BONUSES | 06_CONTENT_CREATION |
| Job/class info | 05_GAME_MECHANICS | 02_SCRIPT_COMMANDS |
| NPC creation | 06_CONTENT_CREATION | 02_SCRIPT_COMMANDS |
| C++ development | 07_SOURCE_DEVELOPMENT | 05_GAME_MECHANICS |
| @command syntax | 08_AT_COMMANDS | 07_SOURCE_DEVELOPMENT |

---

## ARCHITECTURE OVERVIEW

<!-- RAG_CHUNK: architecture -->

```
rAthena Server Architecture
===========================

┌─────────────────────────────────────────────────────────────────┐
│                        CLIENT LAYER                              │
│                    (Ragnarok Online Client)                      │
│                    PACKETVER: 20180620+                          │
└─────────────────────────────┬───────────────────────────────────┘
                              │ TCP/IP Packets
┌─────────────────────────────┴───────────────────────────────────┐
│                       SERVER LAYER                               │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────┐│
│  │ Login Server│  │ Char Server │  │ Map Server  │  │Web Server││
│  │   :6900     │  │   :6121     │  │   :5121     │  │  :8888  ││
│  │   (auth)    │  │  (chars)    │  │  (gameplay) │  │  (API)  ││
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘  └────┬────┘│
│         │                │                │               │     │
│         └────────────────┴────────────────┴───────────────┘     │
│                              │                                   │
└──────────────────────────────┼───────────────────────────────────┘
                               │
┌──────────────────────────────┴───────────────────────────────────┐
│                       DATA LAYER                                  │
│  ┌──────────────────┐  ┌──────────────────┐  ┌────────────────┐ │
│  │  MySQL Database  │  │  YAML Databases  │  │  NPC Scripts   │ │
│  │  (Persistent)    │  │  (Static Data)   │  │  (Logic)       │ │
│  │  - Accounts      │  │  - item_db.yml   │  │  - *.txt       │ │
│  │  - Characters    │  │  - mob_db.yml    │  │  - Events      │ │
│  │  - Guilds        │  │  - skill_db.yml  │  │  - Quests      │ │
│  │  - Storage       │  │  - quest_db.yml  │  │  - Shops       │ │
│  └──────────────────┘  └──────────────────┘  └────────────────┘ │
└──────────────────────────────────────────────────────────────────┘
```

---

## CONTENT CATEGORIES

<!-- RAG_CHUNK: content_categories -->

### 1. NPC Scripting (02_SCRIPT_COMMANDS.md) - 30,061 lines
- **767+ Script Commands** organized A-Z with full syntax
- **Compact RAG reference** from script_commands_optimized.md
- Dialog: mes, next, close, menu, select, input, prompt
- Items: getitem, delitem, countitem, getinventorylist, rentitem
- Player: warp, heal, skill, statusup, jobchange, savepoint
- Monster: monster, areamonster, killmonster, mobcount, summon
- Instance: instance_create, instance_warp, instance_destroy
- Quest: setquest, completequest, checkquest, erasequest
- Variable scopes: `.@local`, `.npc`, `@temp`, `#account`, `$global`

### 2. Status Effects (03_STATUS_EFFECTS.md) - 12,662 lines
- **1,038 SC_* Constants** with effects and parameters
- Common ailments: SC_STONE, SC_FREEZE, SC_STUN, SC_POISON
- Buffs: SC_BLESSING, SC_INCREASEAGI, SC_KYRIE, SC_ASSUMPTIO
- Food/consumable effects, equipment effects, GvG effects
- Script usage: sc_start, sc_start2, sc_start4, sc_end, sc_is

### 3. Item Bonuses (04_ITEM_BONUSES.md) - 5,762 lines
- **263+ Bonus Types** for item scripts
- Basic: bStr, bAgi, bVit, bInt, bDex, bLuk, bAllStats
- HP/SP: bMaxHP, bMaxSP, bMaxHPrate, bMaxSPrate
- Combat: bAtk, bDef, bMdef, bAspd, bCritical, bHit, bFlee
- Advanced: bonus2, bonus3, bonus4, bonus5, autobonus
- Constants: Ele_*, RC_*, Size_*, Class_*, BF_*, ATF_*

### 4. Game Mechanics (05_GAME_MECHANICS.md) - 4,317 lines
- **Job System**: EAJ_* constants, EAJL_* masks, job trees
- **Map Flags**: 84 MF_* constants (MF_NOMEMO, MF_PVP, MF_GVG)
- **Server Configuration**: login/char/map/inter/web settings
- **Element Table**: 10x10 damage multiplier matrix
- **Battle Configuration**: exp rates, drop rates, player settings

### 5. Content Creation (06_CONTENT_CREATION.md) - 6,168 lines
- **Item Groups**: Gacha boxes, random boxes, IG_* constants
- **Quest System**: quest_db.yml structure, TimeLimit formats
- **NPC Patterns**: 12 production-ready patterns with code
- **YAML Schemas**: item_db, mob_db, skill_db, instance_db structure

### 6. Source Development (07_SOURCE_DEVELOPMENT.md) - 82,487 lines
- **Plugin System**: src/custom/ modular development
- **BUILDIN_FUNC**: Script command C++ implementation
- **ACMD_FUNC**: AT command C++ implementation
- **Memory Safety**: ERS, map_freeblock, crash prevention
- **420+ Tutorials**: Server setup to advanced modifications
- **Wiki Reference**: Complete Rathena_Source_Data content

### 7. AT Commands (08_AT_COMMANDS.md) - 1,250 lines
- **287 @Commands** across 11 categories
- Player, Information, GM, Admin, Developer commands
- Syntax, parameters, permission levels, examples

---

## QUICK COMMAND REFERENCE

<!-- RAG_CHUNK: quick_reference -->

### Most Used Script Commands
```c
// Dialog
mes "text";                   - Display message in NPC window
next;                         - Wait for player click, continue
close;                        - Close dialog, end script
menu "opt1",L1,"opt2",L2;     - Menu with jump labels
select("opt1:opt2:opt3");     - Menu returning selection number
input @var;                   - Get player text/number input

// Variables
set VAR, value;               - Set variable (deprecated, use =)
VAR = value;                  - Set variable (preferred)
.@local = 1;                  - Local variable (script only)
@temp = 1;                    - Temp variable (until logout)
PlayerVar = 1;                - Permanent variable (saved)
#AccountVar = 1;              - Account variable (all chars)
$GlobalVar = 1;               - Server variable (all players)

// Items
getitem ITEM_ID, amount;      - Give item to player
delitem ITEM_ID, amount;      - Remove item from player
countitem(ITEM_ID);           - Count items in inventory
getinventorylist;             - Load inventory into arrays

// Player
warp "map", x, y;             - Teleport player
heal HP, SP;                  - Heal player (negative = damage)
percentheal HP%, SP%;         - Heal by percentage
sc_start SC_TYPE, ms, val;    - Apply status effect
sc_end SC_TYPE;               - Remove status effect
skill SKILL_ID, level, flag;  - Give skill to player

// Monster
monster "map",x,y,"name",ID,amount,"event"; - Spawn monster
areamonster "map",x1,y1,x2,y2,"name",ID,amount,"event";
killmonster "map","event";    - Kill monsters with label
mobcount("map","event");      - Count monsters

// Events & Timers
announce "message", flag;     - Server announcement
addtimer ms,"NPC::OnLabel";   - Add timer event
initnpctimer;                 - Start NPC timer
donpcevent "NPC::OnLabel";    - Trigger NPC event
```

### Most Used AT Commands
```
@warp <map> <x> <y>           - Teleport to location
@jump <x> <y>                 - Jump to coordinates on current map
@go <number/name>             - Warp to preset location
@item <id> <amount>           - Create item
@item2 <id> <q> <i> <r> <a> <c1-4>  - Create item with options
@zeny <amount>                - Give/take zeny
@heal                         - Full heal HP/SP
@alive                        - Resurrect self
@job <id>                     - Change job class
@blvl <amount>                - Add base levels
@jlvl <amount>                - Add job levels
@allskill                     - Learn all skills
@stpoint <amount>             - Add stat points
@skpoint <amount>             - Add skill points
@str/agi/vit/int/dex/luk <n>  - Set stat value
@speed <value>                - Set movement speed (1-1000)
@hide                         - Toggle GM invisibility
@option <opt1> <opt2> <opt3>  - Set character options
@effect <id>                  - Play effect
@kick <name>                  - Kick player
@ban <+time> <name>           - Ban player
@unban <name>                 - Unban player
@reloadscript                 - Reload all NPC scripts
@reloadmobdb                  - Reload monster database
@reloaditemdb                 - Reload item database
@reloadskilldb                - Reload skill database
```

### Most Used Status Effects
```c
// Debuffs (Negative)
SC_POISON       - Poison: HP drain, no SP regen
SC_STUN         - Stun: Cannot act
SC_FREEZE       - Freeze: Cannot move/act, +MDEF
SC_STONE        - Petrify: Turn to stone, element change
SC_SLEEP        - Sleep: Cannot act, 2x crit received
SC_SILENCE      - Silence: Cannot cast spells
SC_BLIND        - Blind: -25% HIT/FLEE
SC_CURSE        - Curse: LUK=0, slow movement
SC_BLEEDING     - Bleeding: No HP/SP regen
SC_CONFUSION    - Confusion: Random movement

// Buffs (Positive)
SC_BLESSING     - Blessing: +STR/INT/DEX
SC_INCREASEAGI  - Increase AGI: +AGI, +speed
SC_KYRIE        - Kyrie Eleison: Block hits
SC_ASSUMPTIO    - Assumptio: Damage reduction
SC_DEVOTION     - Devotion: Transfer damage
SC_TWOHANDQUICKEN - Two-Hand Quicken: +30% ASPD
SC_ADRENALINE   - Adrenaline Rush: +ASPD
SC_CONCENTRATION - Concentration: +AGI/DEX
SC_GLORIA       - Gloria: +30 LUK
SC_ANGELUS      - Angelus: +DEF%
```

### Most Used Item Bonuses
```c
// Basic Stats
bonus bStr, n;                - +n STR
bonus bAgi, n;                - +n AGI
bonus bVit, n;                - +n VIT
bonus bInt, n;                - +n INT
bonus bDex, n;                - +n DEX
bonus bLuk, n;                - +n LUK
bonus bAllStats, n;           - +n All Stats

// HP/SP
bonus bMaxHP, n;              - +n Max HP
bonus bMaxSP, n;              - +n Max SP
bonus bMaxHPrate, n;          - +n% Max HP
bonus bMaxSPrate, n;          - +n% Max SP

// Combat
bonus bAtk, n;                - +n ATK
bonus bAtk2, n;               - +n ATK (stacks differently)
bonus bDef, n;                - +n DEF
bonus bDef2, n;               - +n VIT DEF
bonus bMdef, n;               - +n MDEF
bonus bAspd, n;               - +n ASPD
bonus bCritical, n;           - +n Critical rate
bonus bHit, n;                - +n HIT
bonus bFlee, n;               - +n FLEE
bonus bFlee2, n;              - +n Perfect Dodge

// Advanced (bonus2, bonus3)
bonus2 bAddRace, r, n;        - +n% damage vs race r
bonus2 bAddEle, e, n;         - +n% damage vs element e
bonus2 bAddSize, s, n;        - +n% damage vs size s
bonus2 bSubRace, r, n;        - -n% damage from race r
bonus2 bSubEle, e, n;         - -n% damage from element e
bonus3 bAutoSpell, sk, lv, n; - n/10% auto-cast skill on attack
bonus3 bAutoSpellWhenHit, sk, lv, n; - Auto-cast when hit
```

---

## DATABASE QUICK REFERENCE

<!-- RAG_CHUNK: database_reference -->

### YAML File Locations
```
db/
├── re/                       # Renewal databases
│   ├── item_db.yml           # Items
│   ├── mob_db.yml            # Monsters
│   └── skill_db.yml          # Skills
├── pre-re/                   # Pre-Renewal databases
├── item_db.yml               # Shared items
├── mob_db.yml                # Shared monsters
├── skill_db.yml              # Shared skills
├── quest_db.yml              # Quests
├── instance_db.yml           # Instances
├── achievement_db.yml        # Achievements
├── pet_db.yml                # Pets
├── homunculus_db.yml         # Homunculus
├── mercenary_db.yml          # Mercenaries
├── item_group_db.yml         # Item groups (gacha)
├── job_db.yml                # Job stats
└── import/                   # Override databases
```

### Configuration Files
```
conf/
├── login_athena.conf         # Login server config
├── char_athena.conf          # Character server config
├── map_athena.conf           # Map server config
├── inter_athena.conf         # Inter-server config
├── groups.conf               # GM permission groups
├── channels.conf             # Chat channels
├── battle/                   # Gameplay settings
│   ├── battle.conf           # Main battle settings
│   ├── exp.conf              # Experience rates
│   ├── drops.conf            # Drop rates
│   ├── player.conf           # Player settings
│   ├── skill.conf            # Skill settings
│   ├── monster.conf          # Monster settings
│   ├── gm.conf               # GM settings
│   └── misc.conf             # Miscellaneous
└── import/                   # Override configs
```

### Source Code Structure
```
src/
├── login/                    # Login server source
├── char/                     # Character server source
├── map/                      # Map server source (main)
│   ├── script.cpp            # NPC scripting engine (BUILDIN_FUNC)
│   ├── atcommand.cpp         # @commands (ACMD_FUNC)
│   ├── clif.cpp              # Client packet interface
│   ├── status.cpp            # Status effects (SC_*)
│   ├── battle.cpp            # Combat calculations
│   ├── pc.cpp                # Player functions
│   ├── mob.cpp               # Monster functions
│   ├── skill.cpp             # Skill functions
│   ├── itemdb.cpp            # Item database
│   ├── npc.cpp               # NPC functions
│   └── instance.cpp          # Instance dungeons
├── common/                   # Shared utilities
│   ├── mmo.hpp               # Core structures
│   ├── database.hpp          # Database base class
│   └── timer.hpp             # Timer functions
├── custom/                   # Custom additions (safe from updates)
│   ├── atcommand.inc         # Custom @commands
│   ├── atcommand_def.inc     # @command registration
│   ├── script.inc            # Custom script commands
│   ├── script_def.inc        # Script command registration
│   ├── defines_pre.hpp       # Pre-core defines
│   └── defines_post.hpp      # Post-core defines
└── config/                   # Compilation config
```

---

## NPC SCRIPT TEMPLATE

<!-- RAG_CHUNK: npc_template -->

```c
// =========================================
// NPC Script Template
// Location: npc/custom/my_npc.txt
// =========================================

// Basic NPC: Map,X,Y,Direction  script  Name  Sprite,{
prontera,155,180,5	script	MyNPC	4_F_KAFRA1,{
    // Dialog
    mes "[NPC Name]";
    mes "Hello, " + strcharinfo(0) + "!";
    mes "What can I help you with?";
    next;

    // Menu
    switch(select("Give Item:Check Quest:Warp Me:Cancel")) {
        case 1:
            mes "[NPC Name]";
            if (Zeny < 1000) {
                mes "You need 1000 Zeny!";
                close;
            }
            Zeny -= 1000;
            getitem Red_Potion, 10;
            mes "Here are your potions!";
            break;
        case 2:
            mes "[NPC Name]";
            if (checkquest(1000) == 2) {
                mes "Quest completed!";
            } else if (checkquest(1000) >= 0) {
                mes "Quest in progress...";
            } else {
                mes "Starting quest!";
                setquest 1000;
            }
            break;
        case 3:
            mes "[NPC Name]";
            mes "Warping you to Geffen!";
            close2;
            warp "geffen", 120, 60;
            end;
        case 4:
            mes "[NPC Name]";
            mes "Goodbye!";
            break;
    }
    close;

// NPC Events
OnInit:
    // Runs when server starts
    .npc_var = 100;
    end;

OnClock0000:
    // Runs at midnight
    announce "Server event starting!", bc_all;
    end;
}

// Floating NPC (invisible)
-	script	BackgroundProcess	-1,{
OnInit:
    initnpctimer;
    end;

OnTimer60000:
    // Runs every 60 seconds
    initnpctimer;
    end;
}
```

---

## VARIABLE SCOPES

<!-- RAG_CHUNK: variable_scopes -->

| Prefix | Scope | Persistence | Example | Use Case |
|--------|-------|-------------|---------|----------|
| `.@` | Local | Script execution only | `.@temp = 1;` | Temporary calculations |
| `@` | Player | Until logout | `@score = 100;` | Session data |
| (none) | Player | Saved to DB | `QuestProgress = 1;` | Quest progress |
| `#` | Account | Saved to DB | `#Points = 50;` | Account currency |
| `##` | Account Global | All chars, saved | `##Donation = 10;` | Donations, VIP |
| `.` | NPC | Until reload | `.count = 0;` | NPC state |
| `$` | Global | Until restart | `$EventActive = 1;` | Event flags |
| `$@` | Global Array | Until restart | `$@mobid[0]` | Temp arrays |
| `'` | Instance | Instance lifetime | `'boss_hp = 100;` | Instance vars |

---

## SEARCH TAGS

<!-- RAG_CHUNK: search_tags -->

#rathena #ragnarok #mmorpg #server #emulator #scripting #npc #item #mob #skill
#script_command #buildin_func #mes #getitem #warp #monster #heal #sc_start
#status_effect #sc_poison #sc_stun #sc_freeze #sc_blessing #buff #debuff
#item_bonus #bonus #bStr #bMaxHP #bAtk #autobonus #equipment
#atcommand #acmd_func #gm_command #admin #warp #item #heal #job
#mapflag #mf_pvp #mf_gvg #mf_nomemo #mf_noreturn
#yaml #database #item_db #mob_db #skill_db #quest_db #instance_db
#configuration #battle_conf #exp_rate #drop_rate #server_config
#source_code #cpp #development #tutorial #plugin #custom
#job_system #eaj #class #transcendent #third_job #fourth_job
#instance #dungeon #party #guild #woe #gvg #pvp #battleground
#quest #achievement #pet #homunculus #mercenary #elemental
#knowledgebase #reference #documentation #rag #ai #llm

---

<!-- RAG_METADATA -->
<!-- VERSION: 13.0 -->
<!-- FILES: 8 -->
<!-- TOTAL_LINES: 143038 -->
<!-- TOTAL_SIZE: 4.6MB -->
<!-- LAST_UPDATED: 2025-11-30 -->
<!-- SOURCES: kb_v9_final, kb_ultimate, kb_complete, script_commands_optimized, Rathena_Source_Data -->
