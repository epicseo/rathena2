# rAthena Ultimate Knowledge Base v10.0
## COMPREHENSIVE RAG-OPTIMIZED REFERENCE

---

### STATISTICS
- **Total Script Commands**: 603+ (BUILDIN_FUNC implementations)
- **Total Status Effects**: 1,038 (SC_* constants)
- **Total Item Bonuses**: 263+ bonus types
- **Total AT Commands**: 216+ (@commands)
- **Total Map Flags**: 84 (MF_* constants)
- **Total YAML Databases**: 180 files
- **Total NPC Scripts**: 1,135 files

---

## FILE INDEX

| File | Content | RAG Chunks |
|------|---------|------------|
| 02_SCRIPT_COMMANDS_CORE.md | Core script commands (mes, set, if, menu, etc.) | 200+ |
| 03_SCRIPT_COMMANDS_ITEMS.md | Item commands (getitem, delitem, countitem, etc.) | 150+ |
| 04_SCRIPT_COMMANDS_PLAYER.md | Player commands (warp, heal, status, etc.) | 180+ |
| 05_SCRIPT_COMMANDS_NPC.md | NPC commands (enablenpc, npctalk, etc.) | 100+ |
| 06_SCRIPT_COMMANDS_MOB.md | Monster commands (monster, killmonster, etc.) | 80+ |
| 07_SCRIPT_COMMANDS_GUILD.md | Guild commands (guildskill, guildinfo, etc.) | 60+ |
| 08_SCRIPT_COMMANDS_INSTANCE.md | Instance commands (instance_create, etc.) | 50+ |
| 09_SCRIPT_COMMANDS_MISC.md | Misc commands (query_sql, announce, etc.) | 100+ |
| 10_STATUS_EFFECTS_COMMON.md | Common status effects (SC_POISON, etc.) | 100+ |
| 11_STATUS_EFFECTS_SKILLS.md | Skill-based status effects | 400+ |
| 12_STATUS_EFFECTS_ITEMS.md | Item-based status effects | 200+ |
| 13_STATUS_EFFECTS_SPECIAL.md | Special status effects | 338+ |
| 14_ITEM_BONUSES_BASIC.md | Basic bonuses (bStr, bAgi, etc.) | 80+ |
| 15_ITEM_BONUSES_EXTENDED.md | Extended bonuses (bonus2, bonus3, etc.) | 120+ |
| 16_ITEM_BONUSES_SPECIAL.md | Special bonuses (autobonus, autospell, etc.) | 60+ |
| 17_AT_COMMANDS_GM.md | GM AT commands (@item, @warp, etc.) | 150+ |
| 18_AT_COMMANDS_PLAYER.md | Player AT commands (@autoloot, etc.) | 66+ |
| 19_MAP_FLAGS.md | All 84 map flags with documentation | 84 |
| 20_JOB_CLASSES.md | All job classes and constants | 200+ |
| 21_YAML_ITEM_DB.md | Item database schema | 50+ |
| 22_YAML_MOB_DB.md | Monster database schema | 50+ |
| 23_YAML_SKILL_DB.md | Skill database schema | 50+ |
| 24_YAML_MISC.md | Other YAML database schemas | 100+ |
| 25_SOURCE_SCRIPT_CPP.md | script.cpp BUILDIN_FUNC patterns | 200+ |
| 26_SOURCE_STATUS_CPP.md | status.cpp implementation patterns | 100+ |
| 27_SOURCE_ATCOMMAND_CPP.md | atcommand.cpp ACMD patterns | 100+ |
| 28_SOURCE_CLIF_CPP.md | clif.cpp packet handling | 100+ |
| 29_NPC_BASIC_TUTORIAL.md | Basic NPC scripting tutorial | 50+ |
| 30_NPC_ADVANCED_TUTORIAL.md | Advanced NPC patterns | 80+ |
| 31_NPC_SHOP_TUTORIAL.md | Shop NPC creation | 30+ |
| 32_NPC_WARP_TUTORIAL.md | Warp NPC creation | 20+ |
| 33_NPC_QUEST_TUTORIAL.md | Quest system tutorial | 60+ |
| 34_ITEM_CREATION.md | Creating custom items | 80+ |
| 35_MOB_CREATION.md | Creating custom monsters | 60+ |
| 36_SKILL_CREATION.md | Creating custom skills | 100+ |
| 37_MAP_CREATION.md | Adding custom maps | 40+ |
| 38_CONFIGURATION.md | Server configuration guide | 150+ |
| 39_DEBUGGING.md | Debugging and troubleshooting | 80+ |
| 40_ARCHITECTURE.md | System architecture overview | 100+ |
| 41_QUICK_REFERENCE.md | Quick lookup tables | 200+ |

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

## QUICK COMMAND LOOKUP

### Most Used Script Commands
```
mes "text"              - Display message
next                    - Wait for player click
close                   - Close dialog
set VAR, value          - Set variable
getitem ITEM_ID, amount - Give item to player
warp "map", x, y        - Teleport player
heal HP, SP             - Heal player
sc_start SC_TYPE, ms, val - Apply status effect
monster "map",x,y,"name",ID,amount - Spawn monster
```

### Most Used AT Commands
```
@warp map x y           - Teleport to location
@item item_id amount    - Create item
@heal                   - Full heal
@job job_id             - Change job
@lvup amount            - Increase base level
@allskill               - Learn all skills
@speed value            - Set movement speed
@hide                   - Toggle GM hide
@kick player            - Kick player
@ban duration player    - Ban player
```

### Most Used Status Effects
```
SC_POISON     - Poison (HP drain)
SC_STUN       - Stun (cannot act)
SC_FREEZE     - Freeze (cannot move/act)
SC_STONE      - Petrify
SC_SLEEP      - Sleep
SC_SILENCE    - Cannot cast spells
SC_BLIND      - Reduced hit rate
SC_BLEEDING   - Bleeding (HP drain)
SC_CURSE      - Curse (reduced LUK)
SC_BLESSING   - Blessing buff
SC_INCREASEAGI - AGI up buff
SC_KYRIE      - Kyrie Eleison shield
```

---

## SEARCH TAGS

#rathena #ragnarok #mmorpg #server #emulator #scripting #npc #item #mob #skill
#sc_start #getitem #warp #monster #bonus #atcommand #mapflag #yaml #database
#buildin_func #status_effect #item_bonus #guild #party #instance #quest

---

<!-- RAG_CHUNK_ID: master_index_001 -->
<!-- RAG_KEYWORDS: rathena, knowledge base, index, overview, architecture -->
