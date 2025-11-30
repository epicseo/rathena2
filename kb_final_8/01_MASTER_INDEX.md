# rAthena Knowledge Base v15.0 - Superior Edition

**Version:** 15.0 - Enhanced with Visual Effects, Monster Modes & GM Permissions
**Release Date:** 2025-11-30
**Total Files:** 9 RAG-optimized knowledge base files
**Total Lines:** 94,826 (CLEAN - no duplicates)
**Total Size:** 2.9 MB
**RAG Chunks:** 1,687

---

<!-- RAG_CHUNK: version_comparison -->
## VERSION COMPARISON

| Metric | kb_v9_final | v14 (clean) | **v15 (SUPERIOR)** |
|--------|-------------|-------------|-------------------|
| **Total Files** | 9 | 8 | **9** |
| **Total Lines** | 92,448 | 93,732 | **94,826** |
| **Total Size** | 2.8 MB | 2.8 MB | **2.9 MB** |
| **Duplicates** | None | None | **None** |
| **RAG Chunks** | 1,621 | 1,649 | **1,687** |
| **Visual Effects** | Partial | Partial | **967 EF_* Complete** |
| **Monster Modes** | Partial | Partial | **27 MD_* Complete** |
| **GM Permissions** | None | None | **31 PC_PERM_* Complete** |

### What's NEW in v15

| Addition | Lines | RAG Chunks | Value |
|----------|-------|------------|-------|
| **09_VISUAL_EFFECTS.md** | 786 | 30 | All 967 EF_* effects with categories |
| **Monster Modes (MD_*)** | +189 | +3 | All 27 mob mode flags with explanations |
| **GM Permissions (PC_PERM_*)** | +119 | +5 | All 31 permission constants |
| **TOTAL NEW** | **+1,094** | **+38** | **Unique content NOT in v9** |

---

<!-- RAG_CHUNK: file_reference -->
## Complete File Reference (9 Files)

| # | File | Lines | RAG Chunks | Content |
|---|------|-------|------------|---------|
| 01 | **01_MASTER_INDEX.md** | ~200 | 10 | Navigation hub, comparison |
| 02 | **02_SCRIPT_COMMANDS.md** | 16,070 | 24 | 767+ commands + BUILDIN_FUNC |
| 03 | **03_STATUS_EFFECTS.md** | 11,982 | 671 | ALL 1,038 SC_* + val1-val4 |
| 04 | **04_ITEM_BONUSES.md** | 5,262 | 270 | All 263 bonuses + constants |
| 05 | **05_GAME_MECHANICS.md** | 3,481 | 31 | EAJ_*, mf_*, elements, **MD_*** |
| 06 | **06_CONTENT_CREATION.md** | 5,107 | 55 | NPC patterns, items, quests |
| 07 | **07_SOURCE_DEVELOPMENT.md** | 50,607 | 567 | C++ dev + 420+ tutorials |
| 08 | **08_AT_COMMANDS.md** | 1,364 | 30 | 287 @commands + **PC_PERM_*** |
| 09 | **09_VISUAL_EFFECTS.md** | 786 | 30 | **ALL 967 EF_* effects** |
| **TOTAL** | **9 files** | **94,826** | **1,687** | **Superior Coverage** |

---

<!-- RAG_CHUNK: quick_lookup -->
## Quick Lookup Guide

| I need... | Load File |
|-----------|-----------|
| Script command syntax | 02_SCRIPT_COMMANDS |
| Create custom command (BUILDIN_FUNC) | 02_SCRIPT_COMMANDS Part 2 |
| Status effects (SC_*) | 03_STATUS_EFFECTS |
| Item bonuses (bonus/bonus2/etc) | 04_ITEM_BONUSES |
| Job masks (EAJ_*) | 05_GAME_MECHANICS |
| Mapflags (mf_*) | 05_GAME_MECHANICS |
| **Monster modes (MD_*)** | **05_GAME_MECHANICS** |
| Element damage table | 05_GAME_MECHANICS |
| NPC scripting patterns | 06_CONTENT_CREATION |
| C++ source development | 07_SOURCE_DEVELOPMENT |
| @commands reference | 08_AT_COMMANDS |
| **GM permissions (PC_PERM_*)** | **08_AT_COMMANDS** |
| **Visual effects (EF_*)** | **09_VISUAL_EFFECTS** |

---

<!-- RAG_CHUNK: loading_strategy -->
## Recommended Loading Strategy

### For NPC Scripters
```
Load: 02_SCRIPT_COMMANDS + 03_STATUS_EFFECTS + 04_ITEM_BONUSES + 09_VISUAL_EFFECTS
```

### For Content Creators
```
Load: 06_CONTENT_CREATION + 04_ITEM_BONUSES + 05_GAME_MECHANICS + 09_VISUAL_EFFECTS
```

### For C++ Developers
```
Load: 07_SOURCE_DEVELOPMENT (includes all tutorials)
```

### For Server Admins
```
Load: 05_GAME_MECHANICS + 08_AT_COMMANDS (includes GM permissions)
```

### For Monster Creation
```
Load: 05_GAME_MECHANICS (Monster Modes section) + 06_CONTENT_CREATION
```

---

<!-- RAG_CHUNK: validation_status -->
## Source Validation Status

| Content | Source File | Status |
|---------|-------------|--------|
| Script Commands | doc/script_commands.txt | ✅ 767 commands |
| Status Effects | src/map/status.hpp | ✅ 1,038 SC_* |
| Item Bonuses | doc/item_bonus.txt | ✅ 263 bonuses |
| AT Commands | doc/atcommands.txt | ✅ 287 commands |
| **Visual Effects** | **doc/effect_list.md** | ✅ **967 EF_*** |
| **Monster Modes** | **doc/mob_db_mode_list.txt** | ✅ **27 MD_*** |
| **GM Permissions** | **doc/permissions.txt** | ✅ **31 PC_PERM_*** |
| Battle Config | conf/battle/*.conf | ✅ 550+ settings |
| Element Table | db/re/attr_fix.yml | ✅ Values verified |

---

<!-- RAG_CHUNK: rag_optimization -->
## RAG Optimization Details

### Chunk Distribution
- **03_STATUS_EFFECTS.md**: 671 chunks (1 per status effect)
- **07_SOURCE_DEVELOPMENT.md**: 567 chunks (per section/tutorial)
- **04_ITEM_BONUSES.md**: 270 chunks (1 per bonus type)
- **06_CONTENT_CREATION.md**: 55 chunks (per pattern/guide)
- **05_GAME_MECHANICS.md**: 31 chunks (inc. monster modes)
- **08_AT_COMMANDS.md**: 30 chunks (inc. permissions)
- **09_VISUAL_EFFECTS.md**: 30 chunks (effects by category)
- **02_SCRIPT_COMMANDS.md**: 24 chunks (major sections)
- **Total**: 1,687 semantic chunks

### Why v15 is Superior

1. **Complete Visual Effects Reference**: All 967 EF_* constants with descriptions - essential for NPC scripters using `specialeffect`
2. **Monster Mode Documentation**: Full MD_* flag explanations for mob_db.yml creation
3. **GM Permissions Reference**: All PC_PERM_* constants for groups.conf configuration
4. **Zero Duplicates**: Only genuinely unique content added
5. **+38 RAG Chunks**: More precise semantic boundaries

---

<!-- RAG_CHUNK: new_content_summary -->
## New Content in v15

### Visual Effects (09_VISUAL_EFFECTS.md)
```c
// Use in NPC scripts
specialeffect EF_BLESSING;    // Effect on NPC
specialeffect2 EF_HEAL;       // Effect on player
@effect 42                    // Test in-game
```
Categories: Hit, Buff, Mage, Priest, Assassin, Knight, Monk, Bard, Ninja, Gunslinger, 3rd Class, Elemental

### Monster Modes (05_GAME_MECHANICS.md)
```yaml
Mode:
  CanMove: true       # MD_CANMOVE
  Aggressive: true    # MD_AGGRESSIVE
  Mvp: true          # MD_MVP
  Detector: true     # MD_DETECTOR
```

### GM Permissions (08_AT_COMMANDS.md)
```conf
permissions: {
    all_commands: true        # PC_PERM_USE_ALL_COMMANDS
    any_warp: true           # PC_PERM_WARP_ANYWHERE
    bypass_max_stat: true    # PC_PERM_BYPASS_MAX_STAT
}
```

---

<!-- RAG_METADATA -->
<!-- VERSION: 15.0 -->
<!-- FILES: 9 -->
<!-- TOTAL_LINES: 94826 -->
<!-- RAG_CHUNKS: 1687 -->
<!-- DUPLICATES: 0 -->
<!-- LAST_UPDATED: 2025-11-30 -->
