# rAthena Knowledge Base v14.0 - Clean Deduplicated Edition

**Version:** 14.0 - Properly Merged & Deduplicated
**Release Date:** 2025-11-30
**Total Files:** 8 RAG-optimized knowledge base files
**Total Lines:** 93,698 (CLEAN - no duplicates)
**Total Size:** 2.8 MB
**RAG Chunks:** 1,646

---

<!-- RAG_CHUNK: version_comparison -->
## VERSION COMPARISON

| Metric | kb_v9_final | v13 (bloated) | **v14 (CLEAN)** |
|--------|-------------|---------------|-----------------|
| **Total Files** | 9 | 8 | **8** |
| **Total Lines** | 92,448 | 143,038 | **93,698** |
| **Total Size** | 2.8 MB | 4.6 MB | **2.8 MB** |
| **Duplicates** | None | ~40% | **None** |
| **RAG Chunks** | 1,622 | ~50 | **1,646** |
| **Quality** | Excellent | Poor | **Excellent** |

### Why v14 is Better Than v13

| Issue | v13 Problem | v14 Solution |
|-------|-------------|--------------|
| script_commands_optimized.md | Added as duplicate (10K lines wasted) | Not added - v9 version is MORE comprehensive |
| Rathena_Source_Data.md | Added as duplicate (31K lines wasted) | Not added - already IN v9 source tutorials |
| RAG Markers | Only ~50 markers added to index | 1,646 markers preserved from v9 |
| @go tutorial | Appeared 4+ times | Appears 1 time |
| File bloat | 4.6 MB | 2.8 MB |

---

<!-- RAG_CHUNK: sources_merged -->
## Source Files Analysis

| File | Lines | In v9? | Action |
|------|-------|--------|--------|
| kb_v9_final | 92,448 | BASE | Used as gold standard |
| script_commands_optimized.md | 10,222 | YES (v9 has 16K superior version) | NOT added (subset) |
| Rathena_Source_Data.md | 31,401 | YES (in 08_SOURCE_TUTORIALS) | NOT added (already included) |
| 17_AT_COMMANDS_COMPLETE.md | 1,245 | NO | Added (unique content) |

---

<!-- RAG_CHUNK: file_reference -->
## Complete File Reference (8 Files)

| # | File | Lines | RAG Chunks | Content |
|---|------|-------|------------|---------|
| 01 | **01_MASTER_INDEX.md** | ~180 | 10 | Navigation hub, comparison |
| 02 | **02_SCRIPT_COMMANDS.md** | 16,070 | 24 | 767+ commands + creation + performance |
| 03 | **03_STATUS_EFFECTS.md** | 11,982 | 671 | ALL 1,038 SC_* + val1-val4 docs |
| 04 | **04_ITEM_BONUSES.md** | 5,262 | 270 | All 263 bonuses + constants |
| 05 | **05_GAME_MECHANICS.md** | 3,292 | 30 | EAJ_*, mf_*, element table, configs |
| 06 | **06_CONTENT_CREATION.md** | 5,107 | 55 | NPC patterns, items, quests |
| 07 | **07_SOURCE_DEVELOPMENT.md** | 50,607 | 567 | C++ dev + tutorials + wiki |
| 08 | **08_AT_COMMANDS.md** | 1,245 | 25 | ALL 287 @commands |
| **TOTAL** | **8 files** | **93,698** | **1,646** | **100% Complete** |

---

<!-- RAG_CHUNK: quick_lookup -->
## Quick Lookup Guide

| I need... | Load File |
|-----------|-----------|
| Script command syntax | 02_SCRIPT_COMMANDS |
| Create custom command (BUILDIN_FUNC) | 02_SCRIPT_COMMANDS Part 2 |
| Script performance optimization | 02_SCRIPT_COMMANDS Part 3 |
| Status effects (SC_*) | 03_STATUS_EFFECTS |
| SC_* val1-val4 parameters | 03_STATUS_EFFECTS |
| Item bonuses (bonus/bonus2/etc) | 04_ITEM_BONUSES |
| Race/Element/Size constants | 04_ITEM_BONUSES |
| Job masks (EAJ_*) | 05_GAME_MECHANICS |
| Mapflags (mf_*) | 05_GAME_MECHANICS |
| Element damage table | 05_GAME_MECHANICS |
| Battle config settings | 05_GAME_MECHANICS |
| NPC scripting patterns | 06_CONTENT_CREATION |
| Item groups/gacha | 06_CONTENT_CREATION |
| Quest system | 06_CONTENT_CREATION |
| C++ source code | 07_SOURCE_DEVELOPMENT |
| Plugin system | 07_SOURCE_DEVELOPMENT |
| Server setup tutorials | 07_SOURCE_DEVELOPMENT |
| @commands reference | 08_AT_COMMANDS |

---

<!-- RAG_CHUNK: loading_strategy -->
## Recommended Loading Strategy

### For NPC Scripters
```
Load: 02_SCRIPT_COMMANDS + 03_STATUS_EFFECTS + 04_ITEM_BONUSES
```

### For Content Creators
```
Load: 06_CONTENT_CREATION + 04_ITEM_BONUSES + 05_GAME_MECHANICS
```

### For C++ Developers
```
Load: 07_SOURCE_DEVELOPMENT (includes all tutorials)
```

### For Server Admins
```
Load: 05_GAME_MECHANICS (configs) + 08_AT_COMMANDS
```

### For Beginners
```
Load: 07_SOURCE_DEVELOPMENT (420+ tutorials section)
```

---

<!-- RAG_CHUNK: validation_status -->
## Source Validation Status

| Content | Source File | Status |
|---------|-------------|--------|
| Script Commands | doc/script_commands.txt | ✅ 767 commands |
| Status Effects | src/map/status.hpp | ✅ 1,038 SC_* verified |
| Item Bonuses | doc/item_bonus.txt | ✅ 263 bonuses |
| AT Commands | doc/atcommands.txt | ✅ 287 commands |
| Battle Config | conf/battle/*.conf | ✅ 550+ settings |
| Element Table | db/re/attr_fix.yml | ✅ Values verified |
| Job Constants | src/map/pc.hpp | ✅ EAJ_* verified |

---

<!-- RAG_CHUNK: rag_optimization -->
## RAG Optimization Details

### Chunk Distribution
- **03_STATUS_EFFECTS.md**: 671 chunks (1 per status effect)
- **04_ITEM_BONUSES.md**: 270 chunks (1 per bonus type)
- **07_SOURCE_DEVELOPMENT.md**: 567 chunks (per section/tutorial)
- **Total**: 1,646 semantic chunks

### Chunk Format
```html
<!-- RAG_CHUNK: SC_BLESSING -->
### SC_BLESSING
Effect: Increase STR, DEX & INT by (Skill Lv)
...
```

### Why This Works for RAG
1. Each chunk is semantically complete
2. Chunk names match search queries (SC_BLESSING, bStr, etc.)
3. No duplicate content = accurate retrieval
4. Consistent format = predictable parsing

---

<!-- RAG_METADATA -->
<!-- VERSION: 14.0 -->
<!-- FILES: 8 -->
<!-- TOTAL_LINES: 93698 -->
<!-- RAG_CHUNKS: 1646 -->
<!-- DUPLICATES: 0 -->
<!-- LAST_UPDATED: 2025-11-30 -->
