# rAthena KB Architecture v2.0 - RAG-Optimized Design

## Executive Summary

| Metric | Value |
|--------|-------|
| **Total KBs** | 6 |
| **Total Source Lines** | ~45,000 |
| **Estimated KB Lines** | ~35,000 |
| **Mode Coverage** | SCRIPTING 40% / SRC 30% / DEV 30% |

---

## Subsystem Mental Model

### rAthena Execution Flow
```
┌─────────────────────────────────────────────────────────────────────────────┐
│ NPC TRIGGER (click/touch/event)                                              │
└─────────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│ SCRIPT PARSER (script.cpp)                                                   │
│ - Tokenizes script text                                                      │
│ - Builds bytecode                                                            │
│ - Manages script state (script_state)                                        │
└─────────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│ COMMAND EXECUTION (buildin_* functions in script.cpp)                        │
│ - ~600+ buildin functions                                                    │
│ - Each command has BUILDIN_FUNC() implementation                             │
│ - Commands call core source functions                                        │
└─────────────────────────────────────────────────────────────────────────────┘
                                    │
                    ┌───────────────┼───────────────┐
                    ▼               ▼               ▼
┌──────────────────────┐ ┌──────────────────────┐ ┌──────────────────────┐
│ PLAYER (pc.cpp)      │ │ ITEMS (itemdb.cpp)   │ │ STATUS (status.cpp)  │
│ - map_session_data   │ │ - item_data          │ │ - status_change      │
│ - inventory mgmt     │ │ - item_db loading    │ │ - bonus calculations │
└──────────────────────┘ └──────────────────────┘ └──────────────────────┘
                    │               │               │
                    └───────────────┼───────────────┘
                                    ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│ DATABASE LAYER (db/re/*.yml, db/pre-re/*.yml)                                │
│ - item_db_*.yml (263k lines equip, 99k etc, 86k usable)                     │
│ - skill_db.yml (50k lines)                                                   │
│ - mob_db.yml (118k lines)                                                    │
└─────────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│ CLIENT INTERFACE (clif.cpp - 25k lines)                                      │
│ - Packet construction                                                        │
│ - Client communication                                                       │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Knowledge Domain Boundaries

| Domain | Starts At | Ends At | Primary Users |
|--------|-----------|---------|---------------|
| **SCRIPTING** | NPC trigger | Command return | Server scripters |
| **SRC** | buildin_* function | Database read | C++ developers |
| **DEV** | Configuration files | Server startup | Server admins |

---

## Repository Analysis Summary

### High-Value Files Inventory

| Priority | File | Lines | Type | RAG Value | KB Target |
|----------|------|-------|------|-----------|-----------|
| 1 | doc/script_commands.txt | 11,721 | doc | HIGH | KB-1 (existing) |
| 2 | doc/item_bonus.txt | 512 | doc | HIGH | KB-2 |
| 3 | doc/status_change.txt | 2,920 | doc | HIGH | KB-2 |
| 4 | doc/mapflags.txt | 491 | doc | MEDIUM | KB-3 |
| 5 | doc/atcommands.txt | 1,931 | doc | MEDIUM | KB-3 |
| 6 | src/map/script.cpp | 28,574 | src | HIGH | KB-4 |
| 7 | src/map/pc.hpp | 2,200+ | src | HIGH | KB-4 |
| 8 | src/map/status.hpp | 1,500+ | src | MEDIUM | KB-4 |
| 9 | db/re/item_db_equip.yml | 263,846 | db | Schema only | KB-5 |
| 10 | db/re/skill_db.yml | 50,666 | db | Schema only | KB-5 |
| 11 | conf/battle/*.conf | ~2,000 | conf | HIGH | KB-6 |

### Existing KB Overlap Analysis

| Existing File | Lines | Coverage | Overlap Risk |
|---------------|-------|----------|--------------|
| script_commands_optimized.md | 10,222 | Script commands | AVOID duplication |
| Rathena_Source_Data.md | 31,401 | Tutorials/guides | Complements, no conflict |

---

## KB Architecture Specification

---

### KB-1: Script Commands Reference
**Status: EXISTING** (`script_commands_optimized.md`)

This KB already exists in the repository. No new creation needed.

---

### KB-2: Script Bonuses & Status Effects

```yaml
# ══════════════════════════════════════════════════════════════
# KB-2: SCRIPT BONUSES & STATUS EFFECTS
# ══════════════════════════════════════════════════════════════

KB_ID: 2
KB_FILENAME: "02_BONUSES_STATUS_KB.md"
PRIMARY_MODE: SCRIPTING
SECONDARY_MODES: [SRC]

# ─────────────────────────────────────────────────────────────
# PURPOSE & SCOPE
# ─────────────────────────────────────────────────────────────
PURPOSE: |
  Complete reference for item bonuses (bonus, bonus2, bonus3, etc.) and
  status changes (SC_*) used in rAthena scripting. This KB answers questions
  about equipment scripts, custom item effects, and status manipulation.

  Target users: Scripters creating custom items, equipment, and buff/debuff systems.

  Distinct from KB-1: KB-1 covers general script commands, this KB focuses
  exclusively on the bonus/status effect subsystem.

QUERY_TYPES_SERVED:
  - "What parameters does bAtkRate take?"
  - "How to add fire element to weapon?"
  - "SC_PROVOKE val1 val2 meaning"
  - "bonus2 vs bonus3 difference"
  - "autocast spell on attack"
  - "How to add HP drain to weapon?"
  - "SC_STONE incubation time"
  - "bAddRace parameters"

# ─────────────────────────────────────────────────────────────
# SOURCE FILES
# ─────────────────────────────────────────────────────────────
SOURCE_FILES:
  - path: "doc/item_bonus.txt"
    type: doc
    extraction: FULL
    lines: 512
    rationale: "Complete bonus reference - all bonus commands with parameters"

  - path: "doc/status_change.txt"
    type: doc
    extraction: FULL
    lines: 2920
    rationale: "Complete SC reference with val1-val4 documentation"

TOTAL_SOURCE_LINES: 3432
ESTIMATED_KB_LINES: 3400
ESTIMATED_CHARS: 204000

# ─────────────────────────────────────────────────────────────
# RAG OPTIMIZATION
# ─────────────────────────────────────────────────────────────
RAG_CONFIG:
  chunk_strategy: BY_ENTRY
  chunk_size_target: 1200
  chunk_overlap: 150

  delimiter_patterns:
    primary: "^(bonus[234]?\\s|SC_[A-Z]+)"
    secondary: "^-{3,}$"

  metadata_per_chunk:
    - field: "name"
      extraction: "First word after 'bonus' or 'SC_'"
    - field: "category"
      extraction: "Section header (1. Basic, 2. Extended, etc.)"
    - field: "parameters"
      extraction: "Text within parentheses or after comma"

  embedding_hints:
    prepend_context: "rAthena item bonus/status effect: "
    key_terms: ["bonus", "SC_", "status change", "item effect", "equipment script"]
    synonyms:
      - canonical: "bAtkRate"
        alternatives: ["attack rate", "atk percent", "damage bonus"]
      - canonical: "SC_POISON"
        alternatives: ["poison status", "poisoned", "poison effect"]

# ─────────────────────────────────────────────────────────────
# STRUCTURE & SECTIONS
# ─────────────────────────────────────────────────────────────
KB_STRUCTURE:
  - section: "Constants Reference"
    purpose: "Element, Race, Class, Size, Trigger criteria constants"
    estimated_lines: 80
    chunk_count: 3

  - section: "Basic Bonuses"
    purpose: "bStr, bAgi, bMaxHP, bAtk, bDef - simple stat modifiers"
    estimated_lines: 200
    chunk_count: 8

  - section: "Extended Bonuses"
    purpose: "HP/SP regen, skill bonuses, conditional effects"
    estimated_lines: 300
    chunk_count: 12

  - section: "AutoSpell Bonuses"
    purpose: "bonus3/4/5 autospell on attack/defense/skill"
    estimated_lines: 100
    chunk_count: 4

  - section: "Status Changes (SC_*)"
    purpose: "Complete SC list with val1-val4 documentation"
    estimated_lines: 2720
    chunk_count: 90

# ─────────────────────────────────────────────────────────────
# OVERLAP & ROUTING
# ─────────────────────────────────────────────────────────────
OVERLAP_ANALYSIS:
  - with_kb: "KB-1 (Script Commands)"
    overlap_percent: 5
    overlap_content: "sc_start mentioned in both"
    justification: "KB-1 has sc_start syntax, KB-2 has SC_* values"
    disambiguation: "Query 'sc_start parameters' → KB-1; Query 'SC_STONE values' → KB-2"

ROUTING_RULES:
  - query_pattern: "bonus.*parameter|bAdd|bAtk|bDef|bMax"
    confidence: HIGH
    fallback_kb: KB-1
  - query_pattern: "SC_.*|status change.*val|effect duration"
    confidence: HIGH
    fallback_kb: KB-4

# ─────────────────────────────────────────────────────────────
# VALIDATION
# ─────────────────────────────────────────────────────────────
VALIDATION_QUERIES:
  - query: "bonus bAtkRate effect"
    expected_chunk: "Basic Bonuses - Atk/Def"
    expected_answer_contains: ["ATK + n%", "renewal mode"]

  - query: "SC_PROVOKE val1 val2"
    expected_chunk: "SC_PROVOKE entry"
    expected_answer_contains: ["DEF", "ATK", "5*Skill Lv"]

  - query: "autocast skill on attack"
    expected_chunk: "AutoSpell Bonuses"
    expected_answer_contains: ["bonus3", "bAutoSpell"]

PRIORITY: 1
DEPENDENCIES: []
MAINTENANCE_FREQUENCY: QUARTERLY
```

---

### KB-3: Game Mechanics Reference

```yaml
# ══════════════════════════════════════════════════════════════
# KB-3: GAME MECHANICS REFERENCE
# ══════════════════════════════════════════════════════════════

KB_ID: 3
KB_FILENAME: "03_GAME_MECHANICS_KB.md"
PRIMARY_MODE: SCRIPTING
SECONDARY_MODES: [DEV]

# ─────────────────────────────────────────────────────────────
# PURPOSE & SCOPE
# ─────────────────────────────────────────────────────────────
PURPOSE: |
  Reference for game mechanics that scripters and admins need: mapflags,
  atcommands, permissions, and mob modes. This KB bridges scripting and
  server administration.

  Target users: Advanced scripters, GMs, server administrators.

  Distinct from KB-1: KB-1 covers script commands, this covers game rules
  and administrative controls.

QUERY_TYPES_SERVED:
  - "What does mapflag pvp do?"
  - "How to disable teleport on map?"
  - "atcommand permission levels"
  - "mob mode aggressive"
  - "mapflag nosave syntax"
  - "GM command to spawn monster"
  - "WoE mapflag settings"
  - "mob_db mode flags"

# ─────────────────────────────────────────────────────────────
# SOURCE FILES
# ─────────────────────────────────────────────────────────────
SOURCE_FILES:
  - path: "doc/mapflags.txt"
    type: doc
    extraction: FULL
    lines: 491
    rationale: "Complete mapflag reference with effects"

  - path: "doc/atcommands.txt"
    type: doc
    extraction: FULL
    lines: 1931
    rationale: "GM/player command reference"

  - path: "doc/permissions.txt"
    type: doc
    extraction: FULL
    lines: 238
    rationale: "Permission group definitions"

  - path: "doc/mob_db_mode_list.txt"
    type: doc
    extraction: FULL
    lines: 181
    rationale: "Monster AI behavior flags"

TOTAL_SOURCE_LINES: 2841
ESTIMATED_KB_LINES: 2800
ESTIMATED_CHARS: 168000

# ─────────────────────────────────────────────────────────────
# RAG OPTIMIZATION
# ─────────────────────────────────────────────────────────────
RAG_CONFIG:
  chunk_strategy: BY_ENTRY
  chunk_size_target: 1000
  chunk_overlap: 100

  delimiter_patterns:
    primary: "^\\*[a-z]|^@[a-z]"
    secondary: "^-{3,}$"

  metadata_per_chunk:
    - field: "name"
      extraction: "Text after * or @"
    - field: "category"
      extraction: "File source (mapflag/atcommand/permission)"
    - field: "gm_level"
      extraction: "Access level if specified"

  embedding_hints:
    prepend_context: "rAthena game mechanic: "
    key_terms: ["mapflag", "atcommand", "@", "permission", "mob mode"]
    synonyms:
      - canonical: "noteleport"
        alternatives: ["no teleport", "disable teleport", "block teleport"]
      - canonical: "@warp"
        alternatives: ["warp command", "teleport command", "move command"]

# ─────────────────────────────────────────────────────────────
# STRUCTURE & SECTIONS
# ─────────────────────────────────────────────────────────────
KB_STRUCTURE:
  - section: "Mapflags - Restrictions"
    purpose: "noteleport, nowarp, nodrop, notrade, etc."
    estimated_lines: 200
    chunk_count: 15

  - section: "Mapflags - Battle"
    purpose: "pvp, gvg, battleground settings"
    estimated_lines: 150
    chunk_count: 10

  - section: "Mapflags - Effects"
    purpose: "weather, skill restrictions, exp modifiers"
    estimated_lines: 140
    chunk_count: 10

  - section: "Atcommands - Player"
    purpose: "Commands available to regular players"
    estimated_lines: 400
    chunk_count: 25

  - section: "Atcommands - GM"
    purpose: "Administrative commands"
    estimated_lines: 1200
    chunk_count: 60

  - section: "Permissions"
    purpose: "Group permission flags"
    estimated_lines: 238
    chunk_count: 10

  - section: "Mob Modes"
    purpose: "Monster AI behavior flags"
    estimated_lines: 181
    chunk_count: 8

# ─────────────────────────────────────────────────────────────
# OVERLAP & ROUTING
# ─────────────────────────────────────────────────────────────
OVERLAP_ANALYSIS:
  - with_kb: "KB-1 (Script Commands)"
    overlap_percent: 10
    overlap_content: "setmapflag command"
    justification: "KB-1 has setmapflag syntax, KB-3 has mapflag effects"
    disambiguation: "Query 'setmapflag syntax' → KB-1; Query 'what does pvp mapflag do' → KB-3"

ROUTING_RULES:
  - query_pattern: "mapflag.*effect|what does.*mapflag"
    confidence: HIGH
    fallback_kb: KB-1
  - query_pattern: "@[a-z]+|atcommand|gm command"
    confidence: HIGH
    fallback_kb: KB-6

# ─────────────────────────────────────────────────────────────
# VALIDATION
# ─────────────────────────────────────────────────────────────
VALIDATION_QUERIES:
  - query: "mapflag noteleport effect"
    expected_chunk: "Mapflags - Restrictions"
    expected_answer_contains: ["Fly Wing", "AL_TELEPORT", "disabled"]

  - query: "@warp command syntax"
    expected_chunk: "Atcommands - GM"
    expected_answer_contains: ["map name", "coordinates"]

  - query: "mob mode aggressive"
    expected_chunk: "Mob Modes"
    expected_answer_contains: ["MD_AGGRESSIVE", "attack", "sight"]

PRIORITY: 2
DEPENDENCIES: []
MAINTENANCE_FREQUENCY: STABLE
```

---

### KB-4: Source Data Structures

```yaml
# ══════════════════════════════════════════════════════════════
# KB-4: SOURCE DATA STRUCTURES
# ══════════════════════════════════════════════════════════════

KB_ID: 4
KB_FILENAME: "04_SOURCE_STRUCTURES_KB.md"
PRIMARY_MODE: SRC
SECONDARY_MODES: []

# ─────────────────────────────────────────────────────────────
# PURPOSE & SCOPE
# ─────────────────────────────────────────────────────────────
PURPOSE: |
  Core C++ data structures and enums for source developers. Contains
  struct definitions, enum values, and key constants from header files.

  Target users: C++ developers modifying rAthena source code.

  Distinct from other KBs: Pure C++ reference, no script or config info.

QUERY_TYPES_SERVED:
  - "map_session_data structure fields"
  - "equip_index enum values"
  - "script_state structure"
  - "status_change enum"
  - "weapon_data struct"
  - "block_list types"
  - "item_data fields"
  - "c_op enum operators"

# ─────────────────────────────────────────────────────────────
# SOURCE FILES
# ─────────────────────────────────────────────────────────────
SOURCE_FILES:
  - path: "src/map/pc.hpp"
    type: src
    extraction: "LINES:1-500"
    lines: 500
    rationale: "Player structures, equip_index, bonuses"

  - path: "src/map/script.hpp"
    type: src
    extraction: "LINES:1-400"
    lines: 400
    rationale: "Script engine types, operators, macros"

  - path: "src/map/status.hpp"
    type: src
    extraction: "LINES:1-500"
    lines: 500
    rationale: "Status change enums, status_data"

  - path: "src/map/map.hpp"
    type: src
    extraction: "LINES:1-400"
    lines: 400
    rationale: "Core map structures, block_list"

  - path: "src/map/itemdb.hpp"
    type: src
    extraction: "LINES:1-300"
    lines: 300
    rationale: "Item structure definitions"

TOTAL_SOURCE_LINES: 2100
ESTIMATED_KB_LINES: 2000
ESTIMATED_CHARS: 120000

# ─────────────────────────────────────────────────────────────
# RAG OPTIMIZATION
# ─────────────────────────────────────────────────────────────
RAG_CONFIG:
  chunk_strategy: BY_DEFINITION
  chunk_size_target: 1500
  chunk_overlap: 200

  delimiter_patterns:
    primary: "^(struct|enum|class|#define)\\s"
    secondary: "^\\};"

  metadata_per_chunk:
    - field: "name"
      extraction: "Identifier after struct/enum/class"
    - field: "type"
      extraction: "struct|enum|class|define"
    - field: "file"
      extraction: "Source header file"

  embedding_hints:
    prepend_context: "rAthena C++ source: "
    key_terms: ["struct", "enum", "map_session_data", "script_state", "status_change"]
    synonyms:
      - canonical: "map_session_data"
        alternatives: ["player data", "sd", "session data"]
      - canonical: "equip_index"
        alternatives: ["equipment slot", "EQI_", "equip position"]

# ─────────────────────────────────────────────────────────────
# STRUCTURE & SECTIONS
# ─────────────────────────────────────────────────────────────
KB_STRUCTURE:
  - section: "Player Structures (pc.hpp)"
    purpose: "equip_index, weapon_data, s_autospell, player bonus structs"
    estimated_lines: 500
    chunk_count: 15

  - section: "Script Engine (script.hpp)"
    purpose: "c_op operators, script_data, script_state, macros"
    estimated_lines: 400
    chunk_count: 12

  - section: "Status System (status.hpp)"
    purpose: "sc_type enum, status_data, status_change_data"
    estimated_lines: 500
    chunk_count: 15

  - section: "Map Core (map.hpp)"
    purpose: "block_list, cell types, map_data"
    estimated_lines: 400
    chunk_count: 12

  - section: "Item System (itemdb.hpp)"
    purpose: "item_data, item_flags, item types"
    estimated_lines: 300
    chunk_count: 10

# ─────────────────────────────────────────────────────────────
# OVERLAP & ROUTING
# ─────────────────────────────────────────────────────────────
OVERLAP_ANALYSIS:
  - with_kb: "KB-2 (Bonuses/Status)"
    overlap_percent: 15
    overlap_content: "SC_* enum values appear in both"
    justification: "KB-2 has script usage, KB-4 has C++ definition"
    disambiguation: "Query 'sc_start SC_POISON' → KB-2; Query 'sc_type enum' → KB-4"

ROUTING_RULES:
  - query_pattern: "struct.*field|enum.*value|hpp definition"
    confidence: HIGH
    fallback_kb: KB-5
  - query_pattern: "map_session_data|script_state|block_list"
    confidence: HIGH
    fallback_kb: None

# ─────────────────────────────────────────────────────────────
# VALIDATION
# ─────────────────────────────────────────────────────────────
VALIDATION_QUERIES:
  - query: "equip_index enum values"
    expected_chunk: "Player Structures"
    expected_answer_contains: ["EQI_ACC_L", "EQI_HAND_R", "EQI_MAX"]

  - query: "c_op script operators"
    expected_chunk: "Script Engine"
    expected_answer_contains: ["C_INT", "C_STR", "C_ADD", "C_LOR"]

  - query: "weapon_data structure"
    expected_chunk: "Player Structures"
    expected_answer_contains: ["atkmods", "addele", "hp_drain"]

PRIORITY: 3
DEPENDENCIES: []
MAINTENANCE_FREQUENCY: QUARTERLY
```

---

### KB-5: Database Schema Reference

```yaml
# ══════════════════════════════════════════════════════════════
# KB-5: DATABASE SCHEMA REFERENCE
# ══════════════════════════════════════════════════════════════

KB_ID: 5
KB_FILENAME: "05_DATABASE_SCHEMA_KB.md"
PRIMARY_MODE: DEV
SECONDARY_MODES: [SCRIPTING]

# ─────────────────────────────────────────────────────────────
# PURPOSE & SCOPE
# ─────────────────────────────────────────────────────────────
PURPOSE: |
  YAML database schema documentation for all major databases: items,
  skills, mobs, quests. Contains field definitions, valid values, and
  examples for each database type.

  Target users: Content creators adding items/skills/mobs, server admins.

  Distinct from other KBs: Pure database structure, not runtime behavior.

QUERY_TYPES_SERVED:
  - "item_db.yml required fields"
  - "skill_db Duration1 format"
  - "mob_db AI field values"
  - "quest_db objectives format"
  - "item SubType values"
  - "skill CastTime per level"
  - "mob_db drop format"
  - "item_group_db structure"

# ─────────────────────────────────────────────────────────────
# SOURCE FILES
# ─────────────────────────────────────────────────────────────
SOURCE_FILES:
  - path: "db/re/item_db_equip.yml"
    type: db
    extraction: "LINES:1-90"
    lines: 90
    rationale: "Item schema header with all field definitions"

  - path: "db/re/skill_db.yml"
    type: db
    extraction: "LINES:1-140"
    lines: 140
    rationale: "Skill schema header with all field definitions"

  - path: "db/re/mob_db.yml"
    type: db
    extraction: "LINES:1-100"
    lines: 100
    rationale: "Monster schema header"

  - path: "doc/item_db.txt"
    type: doc
    extraction: FULL
    lines: 294
    rationale: "Extended item field documentation"

  - path: "doc/skill_db.txt"
    type: doc
    extraction: FULL
    lines: 933
    rationale: "Extended skill documentation"

  - path: "doc/mob_db.txt"
    type: doc
    extraction: FULL
    lines: 260
    rationale: "Monster database documentation"

  - path: "doc/quest_db.txt"
    type: doc
    extraction: FULL
    lines: 76
    rationale: "Quest database documentation"

TOTAL_SOURCE_LINES: 1893
ESTIMATED_KB_LINES: 1850
ESTIMATED_CHARS: 111000

# ─────────────────────────────────────────────────────────────
# RAG OPTIMIZATION
# ─────────────────────────────────────────────────────────────
RAG_CONFIG:
  chunk_strategy: BY_SECTION
  chunk_size_target: 1400
  chunk_overlap: 150

  delimiter_patterns:
    primary: "^# [A-Z]|^###"
    secondary: "^-{3,}$"

  metadata_per_chunk:
    - field: "database"
      extraction: "File name prefix (item_db, skill_db, etc.)"
    - field: "field_name"
      extraction: "YAML key being documented"
    - field: "data_type"
      extraction: "Integer, String, Boolean, Map, List"

  embedding_hints:
    prepend_context: "rAthena database schema: "
    key_terms: ["item_db", "skill_db", "mob_db", "quest_db", "yml", "yaml", "field"]
    synonyms:
      - canonical: "item_db"
        alternatives: ["item database", "items yml", "equipment database"]
      - canonical: "SubType"
        alternatives: ["weapon type", "item subtype", "equipment type"]

# ─────────────────────────────────────────────────────────────
# STRUCTURE & SECTIONS
# ─────────────────────────────────────────────────────────────
KB_STRUCTURE:
  - section: "Item Database Schema"
    purpose: "All item_db.yml fields with types and valid values"
    estimated_lines: 450
    chunk_count: 12

  - section: "Skill Database Schema"
    purpose: "skill_db.yml structure with level-based values"
    estimated_lines: 700
    chunk_count: 18

  - section: "Monster Database Schema"
    purpose: "mob_db.yml fields including drops and stats"
    estimated_lines: 350
    chunk_count: 10

  - section: "Quest Database Schema"
    purpose: "Quest objectives, rewards, conditions"
    estimated_lines: 150
    chunk_count: 5

  - section: "Item Groups Schema"
    purpose: "item_group_db.yml structure"
    estimated_lines: 150
    chunk_count: 5

# ─────────────────────────────────────────────────────────────
# OVERLAP & ROUTING
# ─────────────────────────────────────────────────────────────
OVERLAP_ANALYSIS:
  - with_kb: "KB-2 (Bonuses/Status)"
    overlap_percent: 5
    overlap_content: "Item Script field references bonuses"
    justification: "KB-5 explains Script field exists, KB-2 explains bonus syntax"
    disambiguation: "Query 'item_db Script field' → KB-5; Query 'bonus bAtk' → KB-2"

ROUTING_RULES:
  - query_pattern: "item_db.*field|skill_db.*format|mob_db.*schema"
    confidence: HIGH
    fallback_kb: KB-6
  - query_pattern: "yml.*structure|yaml.*format|database.*field"
    confidence: HIGH
    fallback_kb: None

# ─────────────────────────────────────────────────────────────
# VALIDATION
# ─────────────────────────────────────────────────────────────
VALIDATION_QUERIES:
  - query: "item_db.yml required fields"
    expected_chunk: "Item Database Schema"
    expected_answer_contains: ["Id", "AegisName", "Name", "Type"]

  - query: "skill_db CastTime format"
    expected_chunk: "Skill Database Schema"
    expected_answer_contains: ["Level", "Time", "milliseconds"]

  - query: "mob_db drop rate format"
    expected_chunk: "Monster Database Schema"
    expected_answer_contains: ["Item", "Rate", "10000"]

PRIORITY: 4
DEPENDENCIES: []
MAINTENANCE_FREQUENCY: STABLE
```

---

### KB-6: Configuration Reference

```yaml
# ══════════════════════════════════════════════════════════════
# KB-6: CONFIGURATION REFERENCE
# ══════════════════════════════════════════════════════════════

KB_ID: 6
KB_FILENAME: "06_CONFIGURATION_KB.md"
PRIMARY_MODE: DEV
SECONDARY_MODES: []

# ─────────────────────────────────────────────────────────────
# PURPOSE & SCOPE
# ─────────────────────────────────────────────────────────────
PURPOSE: |
  Server configuration documentation covering battle settings, rates,
  features, and server behavior. Extracted from conf/*.conf files with
  inline documentation.

  Target users: Server administrators configuring their server.

  Distinct from other KBs: Runtime configuration only, not code or scripts.

QUERY_TYPES_SERVED:
  - "How to change exp rate?"
  - "Enable pre-renewal mode"
  - "battle.conf settings"
  - "item drop rate configuration"
  - "skill delay settings"
  - "PvP damage modifier"
  - "monster spawn rate"
  - "How to disable god equipment?"

# ─────────────────────────────────────────────────────────────
# SOURCE FILES
# ─────────────────────────────────────────────────────────────
SOURCE_FILES:
  - path: "conf/battle/battle.conf"
    type: conf
    extraction: FULL
    lines: 200
    rationale: "Core battle calculations"

  - path: "conf/battle/exp.conf"
    type: conf
    extraction: FULL
    lines: 150
    rationale: "Experience rate settings"

  - path: "conf/battle/drops.conf"
    type: conf
    extraction: FULL
    lines: 150
    rationale: "Drop rate settings"

  - path: "conf/battle/skill.conf"
    type: conf
    extraction: FULL
    lines: 200
    rationale: "Skill behavior settings"

  - path: "conf/battle/player.conf"
    type: conf
    extraction: FULL
    lines: 150
    rationale: "Player behavior settings"

  - path: "conf/battle/monster.conf"
    type: conf
    extraction: FULL
    lines: 150
    rationale: "Monster behavior settings"

  - path: "conf/battle/items.conf"
    type: conf
    extraction: FULL
    lines: 100
    rationale: "Item behavior settings"

  - path: "conf/battle/feature.conf"
    type: conf
    extraction: FULL
    lines: 100
    rationale: "Feature toggles"

TOTAL_SOURCE_LINES: 1200
ESTIMATED_KB_LINES: 1200
ESTIMATED_CHARS: 72000

# ─────────────────────────────────────────────────────────────
# RAG OPTIMIZATION
# ─────────────────────────────────────────────────────────────
RAG_CONFIG:
  chunk_strategy: BY_SETTING
  chunk_size_target: 800
  chunk_overlap: 100

  delimiter_patterns:
    primary: "^[a-z_]+:"
    secondary: "^//"

  metadata_per_chunk:
    - field: "setting_name"
      extraction: "Text before colon"
    - field: "file"
      extraction: "Source conf file"
    - field: "default_value"
      extraction: "Value after colon"
    - field: "note_type"
      extraction: "Note 1/2/3 reference"

  embedding_hints:
    prepend_context: "rAthena server configuration: "
    key_terms: ["conf", "setting", "rate", "enable", "disable", "battle"]
    synonyms:
      - canonical: "base_exp_rate"
        alternatives: ["exp rate", "experience rate", "leveling rate"]
      - canonical: "item_rate_common"
        alternatives: ["drop rate", "loot rate", "item drop"]

# ─────────────────────────────────────────────────────────────
# STRUCTURE & SECTIONS
# ─────────────────────────────────────────────────────────────
KB_STRUCTURE:
  - section: "Battle Calculations"
    purpose: "Damage, defense, critical, flee settings"
    estimated_lines: 200
    chunk_count: 15

  - section: "Experience Settings"
    purpose: "EXP rates, death penalty, party share"
    estimated_lines: 150
    chunk_count: 10

  - section: "Drop Settings"
    purpose: "Item drop rates, MVP drops, card rates"
    estimated_lines: 150
    chunk_count: 10

  - section: "Skill Settings"
    purpose: "Skill delays, cast interruption, cooldowns"
    estimated_lines: 200
    chunk_count: 12

  - section: "Player Settings"
    purpose: "Player behavior, stats, limits"
    estimated_lines: 150
    chunk_count: 10

  - section: "Monster Settings"
    purpose: "Monster AI, spawn, aggro"
    estimated_lines: 150
    chunk_count: 10

  - section: "Feature Toggles"
    purpose: "Enable/disable game features"
    estimated_lines: 100
    chunk_count: 8

# ─────────────────────────────────────────────────────────────
# OVERLAP & ROUTING
# ─────────────────────────────────────────────────────────────
OVERLAP_ANALYSIS:
  - with_kb: "KB-3 (Game Mechanics)"
    overlap_percent: 10
    overlap_content: "Some mapflag effects reference conf settings"
    justification: "KB-3 has mapflag effects, KB-6 has global server settings"
    disambiguation: "Query 'pvp damage modifier' → KB-6; Query 'pvp mapflag' → KB-3"

ROUTING_RULES:
  - query_pattern: "conf.*setting|rate.*config|enable.*disable"
    confidence: HIGH
    fallback_kb: KB-3
  - query_pattern: "exp.*rate|drop.*rate|server.*setting"
    confidence: HIGH
    fallback_kb: None

# ─────────────────────────────────────────────────────────────
# VALIDATION
# ─────────────────────────────────────────────────────────────
VALIDATION_QUERIES:
  - query: "change experience rate"
    expected_chunk: "Experience Settings"
    expected_answer_contains: ["base_exp_rate", "job_exp_rate", "100"]

  - query: "item drop rate configuration"
    expected_chunk: "Drop Settings"
    expected_answer_contains: ["item_rate_common", "item_rate_equip", "10000"]

  - query: "skill cast interruption"
    expected_chunk: "Skill Settings"
    expected_answer_contains: ["cast_", "interrupt", "damage"]

PRIORITY: 5
DEPENDENCIES: []
MAINTENANCE_FREQUENCY: STABLE
```

---

## Cross-KB Architecture

### Mode-to-KB Routing Table

```yaml
MODE_ROUTING:
  SCRIPTING:
    primary_kbs: ["KB-1 (existing)", "KB-2"]
    secondary_kbs: ["KB-3"]
    query_patterns:
      - "how to use [command]"
      - "bonus [name] parameters"
      - "SC_* usage"
      - "script example"
      - "NPC dialogue"

  SRC:
    primary_kbs: ["KB-4"]
    secondary_kbs: ["KB-5"]
    query_patterns:
      - "struct [name] fields"
      - "enum [name] values"
      - "function signature"
      - "source implementation"
      - "hpp definition"

  DEV:
    primary_kbs: ["KB-5", "KB-6"]
    secondary_kbs: ["KB-3"]
    query_patterns:
      - "configure [setting]"
      - "database schema"
      - "yml format"
      - "server setup"
      - "rate settings"
```

### Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                          rAthena System Prompt                               │
│                        (MODE: SCRIPTING|SRC|DEV)                             │
└─────────────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                            RAG Query Router                                  │
│              (Routes based on mode + query pattern analysis)                 │
└─────────────────────────────────────────────────────────────────────────────┘
        │                           │                           │
        ▼                           ▼                           ▼
┌───────────────────┐   ┌───────────────────┐   ┌───────────────────┐
│    SCRIPTING      │   │       SRC         │   │       DEV         │
│      KBs          │   │       KBs         │   │       KBs         │
├───────────────────┤   ├───────────────────┤   ├───────────────────┤
│ KB-1: Commands    │   │ KB-4: Structures  │   │ KB-5: DB Schema   │
│      (existing)   │   │                   │   │                   │
│ KB-2: Bonuses/SC  │   │                   │   │ KB-6: Config      │
│ KB-3: Mechanics   │   │                   │   │                   │
└───────────────────┘   └───────────────────┘   └───────────────────┘
```

---

## Validation Query Coverage

### SCRIPTING Mode (20 queries)

| # | Query | Primary KB | Expected Coverage |
|---|-------|------------|-------------------|
| 1 | "getitem syntax and parameters" | KB-1 | ✓ |
| 2 | "how to check if player has item" | KB-1 | ✓ |
| 3 | "difference between set and setd" | KB-1 | ✓ |
| 4 | "bonus bAtkRate effect" | KB-2 | ✓ |
| 5 | "SC_PROVOKE val1 val2" | KB-2 | ✓ |
| 6 | "autocast skill on attack" | KB-2 | ✓ |
| 7 | "mapflag noteleport" | KB-3 | ✓ |
| 8 | "addtimer vs initnpctimer" | KB-1 | ✓ |
| 9 | "menu vs select command" | KB-1 | ✓ |
| 10 | "bonus2 bAddRace parameters" | KB-2 | ✓ |
| 11 | "SC_STONE incubation time" | KB-2 | ✓ |
| 12 | "getcharid types" | KB-1 | ✓ |
| 13 | "HP drain on weapon" | KB-2 | ✓ |
| 14 | "warp vs areawarp" | KB-1 | ✓ |
| 15 | "callsub vs callfunc" | KB-1 | ✓ |
| 16 | "OnPCLoginEvent timing" | KB-1 | ✓ |
| 17 | "bAllStats bonus" | KB-2 | ✓ |
| 18 | "announce color codes" | KB-1 | ✓ |
| 19 | "instance variable scope" | KB-1 | ✓ |
| 20 | "emotion command list" | KB-1 | ✓ |

### SRC Mode (15 queries)

| # | Query | Primary KB | Expected Coverage |
|---|-------|------------|-------------------|
| 1 | "map_session_data structure" | KB-4 | ✓ |
| 2 | "equip_index enum values" | KB-4 | ✓ |
| 3 | "c_op operators" | KB-4 | ✓ |
| 4 | "script_state fields" | KB-4 | ✓ |
| 5 | "weapon_data struct" | KB-4 | ✓ |
| 6 | "sc_type enum" | KB-4 | ✓ |
| 7 | "block_list types" | KB-4 | ✓ |
| 8 | "item_data structure" | KB-4 | ✓ |
| 9 | "s_autospell struct" | KB-4 | ✓ |
| 10 | "status_data fields" | KB-4 | ✓ |
| 11 | "SCRIPT_MAX_ARRAYSIZE" | KB-4 | ✓ |
| 12 | "e_additem_result enum" | KB-4 | ✓ |
| 13 | "Script_Config struct" | KB-4 | ✓ |
| 14 | "e_params enum" | KB-4 | ✓ |
| 15 | "drain_data struct" | KB-4 | ✓ |

### DEV Mode (10 queries)

| # | Query | Primary KB | Expected Coverage |
|---|-------|------------|-------------------|
| 1 | "change experience rate" | KB-6 | ✓ |
| 2 | "item_db.yml required fields" | KB-5 | ✓ |
| 3 | "skill_db CastTime format" | KB-5 | ✓ |
| 4 | "mob_db AI field values" | KB-5 | ✓ |
| 5 | "drop rate configuration" | KB-6 | ✓ |
| 6 | "battle.conf damage settings" | KB-6 | ✓ |
| 7 | "item SubType values" | KB-5 | ✓ |
| 8 | "enable god equipment" | KB-6 | ✓ |
| 9 | "quest_db objectives" | KB-5 | ✓ |
| 10 | "skill delay settings" | KB-6 | ✓ |

---

## Implementation Roadmap

| Priority | KB | Filename | Est. Lines | Dependencies | Build Effort |
|----------|-----|----------|------------|--------------|--------------|
| - | KB-1 | script_commands_optimized.md | 10,222 | EXISTING | N/A |
| 1 | KB-2 | 02_BONUSES_STATUS_KB.md | 3,400 | None | MEDIUM |
| 2 | KB-3 | 03_GAME_MECHANICS_KB.md | 2,800 | None | MEDIUM |
| 3 | KB-4 | 04_SOURCE_STRUCTURES_KB.md | 2,000 | None | LOW |
| 4 | KB-5 | 05_DATABASE_SCHEMA_KB.md | 1,850 | None | LOW |
| 5 | KB-6 | 06_CONFIGURATION_KB.md | 1,200 | None | LOW |

**Total New Lines**: ~11,250
**Total with Existing**: ~21,472

---

## Quality Gates Summary

| Gate | Check | Status |
|------|-------|--------|
| Chunk coherence | No chunk splits mid-entry | PENDING |
| Retrieval precision | ≥85% first-chunk relevance | PENDING |
| Size bounds | 1k-10k lines per KB | ✓ PASS |
| Overlap limits | <30% between KB pairs | ✓ PASS |
| Mode coverage | All 3 modes have primary KBs | ✓ PASS |
| Query coverage | 45+ queries documented | ✓ PASS |

---

*Document Version: 2.0*
*Generated: 2025-11-26*
*Target: RAG-optimized retrieval for rAthena development assistance*
