# rAthena Complete Knowledge Base v11.0
## COMPREHENSIVE RAG-OPTIMIZED REFERENCE

---

### STATISTICS
- **Total Lines**: 101,224
- **Total Files**: 25 documentation files
- **Total Script Commands**: 603+ (BUILDIN_FUNC implementations)
- **Total Status Effects**: 1,038 (SC_* constants)
- **Total Item Bonuses**: 263+ bonus types
- **Total AT Commands**: 287 (@commands)
- **Total Map Flags**: 84 (MF_* constants)
- **Total YAML Databases**: 180 files
- **Total NPC Scripts**: 1,135 files
- **Total Size**: ~3.0 MB

---

## FILE INDEX

### Core Documentation (from kb_v9_final)

| File | Content | Size |
|------|---------|------|
| 02_SCRIPT_COMMANDS.md | Complete script commands (472 KB) | 472 KB |
| 03_STATUS_EFFECTS.md | All 1,038 status effects | 181 KB |
| 04_ITEM_BONUSES.md | All 263+ item bonuses | 78 KB |
| 05_GAME_MECHANICS.md | Combat, formulas, systems | 112 KB |
| 06_CONTENT_CREATION.md | Items, mobs, skills, maps | 123 KB |
| 07_SOURCE_DEV_COMPLETE.md | C++ source development | 394 KB |
| 08_SOURCE_TUTORIALS.md | Extended source tutorials | 1.4 MB |

### Enhanced Documentation (from kb_ultimate)

| File | Content | Lines |
|------|---------|-------|
| 02_SCRIPT_COMMANDS_CORE.md | Core commands (mes, set, menu) | 650 |
| 03_SCRIPT_COMMANDS_ITEMS.md | Item commands (getitem, delitem) | 680 |
| 04_SCRIPT_COMMANDS_PLAYER.md | Player commands (warp, heal) | 760 |
| 05_SCRIPT_COMMANDS_MOB_NPC.md | Monster & NPC commands | 600 |
| 06_SCRIPT_COMMANDS_GUILD.md | Guild & BG commands | 465 |
| 07_SCRIPT_COMMANDS_INSTANCE.md | Instance system | 420 |
| 10_STATUS_EFFECTS_COMPLETE.md | Reorganized SC_* reference | 950 |
| 14_ITEM_BONUSES_COMPLETE.md | Complete bonus reference | 810 |
| 17_AT_COMMANDS_COMPLETE.md | All 287 @commands | 1,246 |
| 19_MAP_FLAGS.md | All 84 MF_* flags | 350 |
| 21_YAML_SCHEMAS.md | YAML database schemas | 420 |
| 25_SOURCE_PATTERNS.md | BUILDIN_FUNC, ACMD_FUNC | 465 |
| 29_NPC_TUTORIAL.md | Complete NPC scripting guide | 620 |
| 30_SERVER_CONFIGURATION.md | Server config reference | 600 |

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

### 1. NPC Scripting
- Script Commands: Core, Items, Player, Mobs, NPCs, Guilds, Instances
- NPC Tutorial: Dialog, menus, shops, warps, quests, events
- Variable Scopes: `.@local`, `.npc`, `PlayerVar`, `@temp`, `#account`, `$global`

### 2. Database Reference
- Status Effects: 1,038 SC_* constants with effects and durations
- Item Bonuses: 263+ bonus types (basic, bonus2-5, autobonus, etc.)
- Map Flags: 84 MF_* flags for map behavior

### 3. Administrative
- AT Commands: 287 @commands across 11 categories
- Server Configuration: Login, Char, Map, Inter-server settings
- GM Groups: Permission system in groups.conf

### 4. Source Development
- BUILDIN_FUNC: Script command implementation patterns
- ACMD_FUNC: AT command implementation patterns
- Packet Handling: clif.cpp patterns
- Status Effects: status.cpp implementation

### 5. YAML Databases
- item_db.yml: Item definitions
- mob_db.yml: Monster definitions
- skill_db.yml: Skill definitions
- quest_db.yml: Quest definitions
- instance_db.yml: Instance definitions

---

## QUICK COMMAND LOOKUP

### Most Used Script Commands
```c
mes "text"                    - Display message
next                          - Wait for player click
close                         - Close dialog
set VAR, value                - Set variable
getitem ITEM_ID, amount       - Give item to player
warp "map", x, y              - Teleport player
heal HP, SP                   - Heal player
sc_start SC_TYPE, ms, val     - Apply status effect
monster "map",x,y,"name",ID,amount - Spawn monster
announce "msg", flag          - Server announcement
query_sql "SQL", @var         - Execute SQL query
```

### Most Used AT Commands
```
@warp map x y                 - Teleport to location
@item item_id amount          - Create item
@heal                         - Full heal
@job job_id                   - Change job
@blvl amount                  - Add base levels
@allskill                     - Learn all skills
@speed value                  - Set movement speed
@hide                         - Toggle GM hide
@kick player                  - Kick player
@ban +time player             - Ban player
@reloadscript                 - Reload all scripts
```

### Most Used Status Effects
```c
SC_POISON       - Poison (HP drain)
SC_STUN         - Stun (cannot act)
SC_FREEZE       - Freeze (cannot move/act)
SC_STONE        - Petrify
SC_SLEEP        - Sleep
SC_SILENCE      - Cannot cast spells
SC_BLIND        - Reduced hit rate
SC_BLESSING     - Blessing buff (+STR/INT/DEX)
SC_INCREASEAGI  - AGI up buff
SC_KYRIE        - Kyrie Eleison shield
SC_ASSUMPTIO    - Damage reduction
SC_DEVOTION     - Transfer damage to Crusader
```

### Most Used Item Bonuses
```c
bonus bStr, n;                - +n STR
bonus bMaxHP, n;              - +n Max HP
bonus bAtk, n;                - +n ATK
bonus bAspd, n;               - +n ASPD
bonus2 bAddRace, Race_All, n; - +n% dmg vs all races
bonus2 bAddEle, Ele_All, n;   - +n% dmg vs all elements
bonus3 bAutoSpell, skill, lv, rate; - Auto-cast on attack
```

---

## DATABASE QUICK REFERENCE

### YAML File Locations
```
db/
├── item_db.yml               # Items
├── mob_db.yml                # Monsters
├── skill_db.yml              # Skills
├── quest_db.yml              # Quests
├── instance_db.yml           # Instances
├── achievement_db.yml        # Achievements
├── pet_db.yml                # Pets
├── homunculus_db.yml         # Homunculus
├── mercenary_db.yml          # Mercenaries
└── elemental_db.yml          # Elementals
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

---

## SEARCH TAGS

#rathena #ragnarok #mmorpg #server #emulator #scripting #npc #item #mob #skill
#sc_start #getitem #warp #monster #bonus #atcommand #mapflag #yaml #database
#buildin_func #status_effect #item_bonus #guild #party #instance #quest
#configuration #source #cpp #development #tutorial #reference

---

<!-- RAG_CHUNK_ID: master_index_001 -->
<!-- RAG_KEYWORDS: rathena, knowledge base, index, overview, architecture -->
<!-- VERSION: 11.0 -->
<!-- LAST_UPDATED: 2024 -->
