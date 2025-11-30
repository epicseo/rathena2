# rAthena Complete Knowledge Base v12.0
## 8-FILE COMPREHENSIVE RAG-OPTIMIZED REFERENCE

---

### STATISTICS
- **Total Lines**: 101,177
- **Total Size**: 2.9 MB
- **Total Files**: 8 documentation files
- **Script Commands**: 603+ BUILDIN_FUNC implementations
- **Status Effects**: 1,038 SC_* constants
- **Item Bonuses**: 263+ bonus types
- **AT Commands**: 287 @commands
- **Map Flags**: 84 MF_* constants
- **YAML Databases**: 180 files documented
- **Source Tutorials**: 420+ sections

---

## FILE INDEX

| # | File | Lines | Size | Content |
|---|------|-------|------|---------|
| 1 | 01_MASTER_INDEX.md | ~200 | 8K | Quick reference, architecture, overview |
| 2 | 02_SCRIPT_COMMANDS.md | 19,833 | 532K | ALL 603+ script commands A-Z |
| 3 | 03_STATUS_EFFECTS.md | 12,662 | 196K | ALL 1,038 SC_* status effects |
| 4 | 04_ITEM_BONUSES.md | 5,762 | 93K | ALL 263+ item bonuses |
| 5 | 05_GAME_MECHANICS.md | 4,317 | 137K | Job system, map flags, server config |
| 6 | 06_CONTENT_CREATION.md | 6,168 | 141K | Item groups, quests, NPC patterns, YAML |
| 7 | 07_SOURCE_DEVELOPMENT.md | 51,079 | 1.8M | C++ development, BUILDIN/ACMD patterns |
| 8 | 08_AT_COMMANDS.md | 1,250 | 26K | ALL 287 @commands |

---

## ARCHITECTURE OVERVIEW

```
rAthena Server Architecture
===========================

┌─────────────────────────────────────────────────────────────────┐
│                        CLIENT LAYER                              │
│                    (Ragnarok Online Client)                      │
└─────────────────────────────┬───────────────────────────────────┘
                              │ TCP/IP Packets
┌─────────────────────────────┴───────────────────────────────────┐
│                       SERVER LAYER                               │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────┐│
│  │ Login Server│  │ Char Server │  │ Map Server  │  │Web Server││
│  │   :6900     │  │   :6121     │  │   :5121     │  │  :8888  ││
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
│  └──────────────────┘  └──────────────────┘  └────────────────┘ │
└──────────────────────────────────────────────────────────────────┘
```

---

## CONTENT CATEGORIES

### 1. NPC Scripting (02_SCRIPT_COMMANDS.md)
- **603+ Script Commands** organized A-Z
- Dialog commands: mes, next, close, menu, select, input
- Item commands: getitem, delitem, countitem, getinventorylist
- Player commands: warp, heal, skill, statusup, jobchange
- Monster commands: monster, areamonster, killmonster, mobcount
- Instance commands: instance_create, instance_warp, instance_destroy
- Quest commands: setquest, completequest, checkquest
- Variable scopes: `.@local`, `.npc`, `@temp`, `#account`, `$global`

### 2. Status Effects (03_STATUS_EFFECTS.md)
- **1,038 SC_* Constants** with effects and parameters
- Common ailments: SC_STONE, SC_FREEZE, SC_STUN, SC_POISON
- Buffs: SC_BLESSING, SC_INCREASEAGI, SC_KYRIE, SC_ASSUMPTIO
- Food effects, equipment effects, GvG effects
- Script usage: sc_start, sc_start2, sc_start4, sc_end

### 3. Item Bonuses (04_ITEM_BONUSES.md)
- **263+ Bonus Types** for item scripts
- Basic bonuses: bStr, bAgi, bMaxHP, bAtk, bDef
- Extended bonuses: bonus2, bonus3, bonus4, bonus5
- AutoSpell bonuses, random options
- Constants: Ele_*, RC_*, Size_*, Class_*, BF_*

### 4. Game Mechanics (05_GAME_MECHANICS.md)
- **Job System**: EAJ_* constants, job masks, job trees
- **Map Flags**: 84 MF_* constants (MF_NOMEMO, MF_PVP, etc.)
- **Server Configuration**: login/char/map/inter settings
- **Element Table**: Damage multipliers
- **Battle Configuration**: exp rates, drop rates, player settings

### 5. Content Creation (06_CONTENT_CREATION.md)
- **Item Groups**: Gacha boxes, random boxes, IG_* constants
- **Quest System**: quest_db.yml structure, TimeLimit formats
- **NPC Patterns**: 12 production-ready patterns
- **YAML Schemas**: item_db, mob_db, skill_db, instance_db

### 6. Source Development (07_SOURCE_DEVELOPMENT.md)
- **Plugin System**: src/custom/ modular development
- **BUILDIN_FUNC**: Script command implementation
- **ACMD_FUNC**: AT command implementation
- **Memory Safety**: ERS, map_freeblock patterns
- **420+ Tutorials**: Beginner to expert level

### 7. AT Commands (08_AT_COMMANDS.md)
- **287 @Commands** across 11 categories
- Player commands, GM commands, Admin commands
- Syntax, usage, permission levels

---

## QUICK COMMAND REFERENCE

### Most Used Script Commands
```c
mes "text"                    - Display message
next                          - Wait for player click
close                         - Close dialog
set VAR, value                - Set variable
getitem ITEM_ID, amount       - Give item to player
delitem ITEM_ID, amount       - Remove item
warp "map", x, y              - Teleport player
heal HP, SP                   - Heal player
sc_start SC_TYPE, ms, val     - Apply status effect
sc_end SC_TYPE                - Remove status effect
monster "map",x,y,"name",ID,amt - Spawn monster
killmonster "map","event"     - Kill monsters
announce "msg", flag          - Server announcement
query_sql "SQL", @var         - Execute SQL query
addtimer ms,"NPC::OnLabel"    - Add timer event
```

### Most Used AT Commands
```
@warp map x y                 - Teleport to location
@item item_id amount          - Create item
@heal                         - Full heal
@job job_id                   - Change job
@blvl amount                  - Add base levels
@jlvl amount                  - Add job levels
@allskill                     - Learn all skills
@speed value                  - Set movement speed
@hide                         - Toggle GM hide
@kick player                  - Kick player
@ban +time player             - Ban player
@reloadscript                 - Reload all scripts
@reloadmobdb                  - Reload mob database
@reloaditemdb                 - Reload item database
```

### Most Used Status Effects
```c
// Debuffs
SC_POISON       - Poison (HP drain)
SC_STUN         - Stun (cannot act)
SC_FREEZE       - Freeze (cannot move/act)
SC_STONE        - Petrify (turn to stone)
SC_SLEEP        - Sleep (cannot act)
SC_SILENCE      - Cannot cast spells
SC_BLIND        - Reduced hit rate
SC_CURSE        - LUK=0, slow movement
SC_BLEEDING     - HP/SP regen disabled

// Buffs
SC_BLESSING     - +STR/INT/DEX
SC_INCREASEAGI  - +AGI, faster move
SC_KYRIE        - Kyrie Eleison shield
SC_ASSUMPTIO    - Damage reduction
SC_DEVOTION     - Transfer damage
SC_TWOHANDQUICKEN - +30% ASPD
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
bonus bMaxHP, n;              - +n Max HP
bonus bMaxSP, n;              - +n Max SP

// Combat
bonus bAtk, n;                - +n ATK
bonus bDef, n;                - +n DEF
bonus bAspd, n;               - +n ASPD
bonus bCritical, n;           - +n Critical

// Advanced
bonus2 bAddRace, Race_All, n; - +n% dmg vs all races
bonus2 bAddEle, Ele_All, n;   - +n% dmg vs all elements
bonus2 bAddSize, Size_All, n; - +n% dmg vs all sizes
bonus3 bAutoSpell, skill, lv, rate; - Auto-cast on attack
bonus3 bAutoSpellWhenHit, skill, lv, rate; - Auto-cast when hit
```

---

## DATABASE QUICK REFERENCE

### YAML File Locations
```
db/
├── item_db.yml               # Items (weapons, armor, usables)
├── mob_db.yml                # Monsters
├── skill_db.yml              # Skills
├── quest_db.yml              # Quests
├── instance_db.yml           # Instances
├── achievement_db.yml        # Achievements
├── pet_db.yml                # Pets
├── homunculus_db.yml         # Homunculus
├── mercenary_db.yml          # Mercenaries
├── elemental_db.yml          # Elementals
├── item_group_db.yml         # Item groups (gacha)
└── job_db.yml                # Job stats
```

### Configuration Files
```
conf/
├── login_athena.conf         # Login server
├── char_athena.conf          # Character server
├── map_athena.conf           # Map server
├── inter_athena.conf         # Inter-server
├── groups.conf               # GM permissions
├── channels.conf             # Chat channels
├── battle/                   # Gameplay settings
│   ├── exp.conf              # Experience rates
│   ├── drops.conf            # Drop rates
│   ├── player.conf           # Player settings
│   ├── skill.conf            # Skill settings
│   └── monster.conf          # Monster settings
└── import/                   # Override configs
```

### Source Code Structure
```
src/
├── login/                    # Login server
├── char/                     # Character server
├── map/                      # Map server (main logic)
│   ├── script.cpp            # NPC scripting engine
│   ├── atcommand.cpp         # @commands
│   ├── clif.cpp              # Client interface
│   ├── status.cpp            # Status effects
│   ├── battle.cpp            # Combat calculations
│   └── pc.cpp                # Player functions
├── common/                   # Shared utilities
├── custom/                   # Custom additions
│   ├── atcommand.inc         # Custom @commands
│   ├── script.inc            # Custom script commands
│   └── defines_pre.hpp       # Custom defines
└── config/                   # Compilation config
```

---

## NPC SCRIPT TEMPLATE

```c
// Basic NPC structure
prontera,155,180,5	script	MyNPC	4_F_KAFRA1,{
    mes "[NPC Name]";
    mes "Hello, what can I help you with?";
    next;
    switch(select("Option 1:Option 2:Cancel")) {
        case 1:
            mes "[NPC Name]";
            mes "You chose option 1!";
            break;
        case 2:
            mes "[NPC Name]";
            mes "You chose option 2!";
            break;
        case 3:
            mes "[NPC Name]";
            mes "Goodbye!";
            break;
    }
    close;

OnInit:
    // Runs when server starts
    end;
}
```

---

## VARIABLE SCOPES

| Prefix | Scope | Persistence | Example |
|--------|-------|-------------|---------|
| `.@` | Local | Script execution | `.@temp = 1;` |
| `@` | Player temp | Until logout | `@score = 100;` |
| (none) | Player perm | Saved to DB | `MyVar = 1;` |
| `#` | Account | Saved to DB | `#Points = 50;` |
| `##` | Account global | All chars | `##Donation = 10;` |
| `.` | NPC | Until reload | `.count = 0;` |
| `$` | Global | Until restart | `$EventActive = 1;` |
| `$@` | Global temp | Until restart | `$@mobid[0]` |

---

## SEARCH TAGS

#rathena #ragnarok #mmorpg #server #emulator #scripting #npc #item #mob #skill
#sc_start #getitem #warp #monster #bonus #atcommand #mapflag #yaml #database
#buildin_func #acmd_func #status_effect #item_bonus #guild #party #instance #quest
#configuration #source #cpp #development #tutorial #reference #knowledgebase

---

<!-- RAG_CHUNK_ID: master_index_v12 -->
<!-- RAG_KEYWORDS: rathena, knowledge base, index, overview, architecture, quick reference -->
<!-- VERSION: 12.0 -->
<!-- FILES: 8 -->
<!-- TOTAL_LINES: 101177 -->
<!-- LAST_UPDATED: 2025-11-30 -->
