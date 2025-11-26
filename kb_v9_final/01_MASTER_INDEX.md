# rAthena Knowledge Base v9.0 Final - Master Index

**Version:** 9.0 Final - Best of ALL Versions Combined
**Release Date:** 2025-11-26
**Total Files:** 8 RAG-optimized knowledge base files
**Total Lines:** ~90,000 lines
**Total Size:** ~3.0 MB
**Source Validated:** All critical data verified against rAthena GitHub source

---

<!-- RAG_CHUNK: package_overview -->
## What's in KB v9.0 Final

This is the **ULTIMATE rAthena knowledge base** combining the BEST content from ALL versions:

| Content | Source Version | Lines | Why Best |
|---------|---------------|-------|----------|
| Script Commands | v4 | 16,054 | Includes command creation + performance |
| Status Effects | **v5** | 10,934 | Most comprehensive SC_* docs |
| Item Bonuses | **v5** | 4,999 | Complete 263 bonus documentation |
| Game Mechanics | v4 + v6 | 2,668 | Job system + validated element table |
| Content Creation | v4 | 5,060 | Complete NPC patterns |
| Source Development | v4 | 15,041 | Full C++ dev + database |
| Source Tutorials | v4 | 35,014 | 420+ tutorials, 100+ examples |

---

<!-- RAG_CHUNK: file_reference -->
## Complete File Reference (8 Files)

| # | File | Lines | Content |
|---|------|-------|---------|
| 01 | **01_MASTER_INDEX.md** | ~200 | Navigation hub |
| 02 | **02_SCRIPT_COMMANDS.md** | 16,054 | 767 commands + creation + performance |
| 03 | **03_STATUS_EFFECTS.md** | 10,934 | Complete SC_* with val1-val4 |
| 04 | **04_ITEM_BONUSES.md** | 4,999 | All 263 bonuses + constants |
| 05 | **05_GAME_MECHANICS.md** | 2,668 | EAJ_*, mf_*, element table, configs |
| 06 | **06_CONTENT_CREATION.md** | 5,060 | NPC patterns, items, quests |
| 07 | **07_SOURCE_DEV_COMPLETE.md** | 15,041 | C++ dev + database + packets |
| 08 | **08_SOURCE_TUTORIALS.md** | 35,014 | 420+ tutorials, 100+ NPC examples |
| **Total** | **8 files** | **~90K** | **Complete rAthena KB** |

---

<!-- RAG_CHUNK: version_comparison -->
## Why v9 is the Best

| Feature | v4 | v5 | v6 | v7 | v8 | **v9** |
|---------|-----|-----|-----|-----|-----|--------|
| Total Lines | 78K | 30K | 28K | 78K | 77K | **90K** |
| Script Commands | 16K | 13K | 12K | 16K | 13K | **16K** |
| Status Effects | 3.7K | **11K** | 9K | 3.7K | 0.8K | **11K** |
| Item Bonuses | (in GM) | **5K** | 4K | (in GM) | 0.8K | **5K** |
| Validated | ❌ | ❌ | ✅ | ✅ | ✅ | **✅** |
| Complete | ✅ | ❌ | ❌ | ✅ | ✅ | **✅** |

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
| C++ source code | 07_SOURCE_DEV_COMPLETE |
| Plugin system | 07_SOURCE_DEV_COMPLETE |
| Database C++ | 07_SOURCE_DEV_COMPLETE |
| Packet handling | 07_SOURCE_DEV_COMPLETE |
| Server setup tutorials | 08_SOURCE_TUTORIALS |
| NPC examples (100+) | 08_SOURCE_TUTORIALS |

---

<!-- RAG_CHUNK: validation_status -->
## Source Validation Status

| Content | Source File | Status |
|---------|-------------|--------|
| Script Commands | doc/script_commands.txt | ✅ 767 commands |
| Status Effects | src/map/status.hpp | ✅ SC_* verified |
| Item Bonuses | doc/item_bonus.txt | ✅ 263 bonuses |
| Battle Config | conf/battle/*.conf | ✅ 550 settings |
| Element Table | db/re/attr_fix.yml | ✅ Values verified |
| Job Constants | src/map/pc.hpp | ✅ EAJ_* verified |

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
Load: 07_SOURCE_DEV_COMPLETE
```

### For Server Admins
```
Load: 05_GAME_MECHANICS (configs) + 08_SOURCE_TUTORIALS
```

### For Beginners
```
Load: 08_SOURCE_TUTORIALS (420+ tutorials)
```

---

*KB v9.0 Final - The definitive rAthena knowledge base combining the best of all versions*
