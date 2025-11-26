# rAthena Knowledge Base v7.0 Ultimate - Master Index

**Version:** 7.0 Ultimate - Source-Validated Edition
**Release Date:** 2025-11-26
**Total Files:** 8 RAG-optimized knowledge base files
**Total Content:** ~79K lines | ~2.6 MB
**Source Validated:** ✅ All data verified against rAthena GitHub source
**RAG-Optimized:** ✅ Semantic chunking, cross-references, quick lookups

---

<!-- RAG_CHUNK: package_overview -->
## 📦 What's in KB v7.0 Ultimate

> **🎯 Context Box: The Best of Both Worlds**
> KB v7.0 combines:
> - **KB v4's comprehensive content** (77K+ lines of tutorials, examples, guides)
> - **KB v6.1's source validation** (all data verified against actual rAthena source)
> - **Optimized structure** (8 files for efficient RAG loading)

### Key Features

| Feature | Description |
|---------|-------------|
| **Source Validated** | All counts, values, and examples verified against rAthena source |
| **767+ Script Commands** | Complete syntax + creation guide + performance optimization |
| **Game Constants** | SC_*, bonus, EAJ_*, mf_* with val1-val4 meanings |
| **Element Table** | Verified from db/re/attr_fix.yml (not fabricated) |
| **550 Battle Configs** | From conf/battle/*.conf with descriptions |
| **420+ Tutorials** | Server setup, source mods, NPC examples |
| **100+ NPC Examples** | Working scripts for common patterns |

---

<!-- RAG_CHUNK: file_reference -->
## 📊 Complete File Reference (8 Files)

| # | File | Lines | Size | Content |
|---|------|-------|------|---------|
| 01 | **01_MASTER_INDEX.md** | ~200 | 8KB | Navigation hub, query router |
| 02 | **02_SCRIPTING_COMPLETE.md** | 16,054 | 461KB | 767+ commands, creation guide, performance |
| 03 | **03_GAME_MECHANICS.md** | ~5,100 | 140KB | SC_*, bonus, EAJ_*, mf_*, element table, 550 configs |
| 04 | **04_CONTENT_CREATION.md** | 5,060 | 120KB | Items, quests, NPC patterns |
| 05 | **05_SOURCE_DEVELOPMENT_COMPLETE.md** | 7,932 | 215KB | C++ dev, security, custom @ commands |
| 06 | **06_DATABASE_SYSTEMS.md** | 7,104 | 172KB | YAML parsing, packets, compilation |
| 07 | **07_INTERNALS_REFERENCE.md** | 1,785 | 42KB | Battle + script internals |
| 08 | **08_SOURCE_REFERENCE.md** | 35,014 | 1.4MB | 420+ tutorials, expert reference |
| **Total** | **8 files** | **~79K** | **~2.6MB** | **Complete rAthena KB** |

---

<!-- RAG_CHUNK: quick_lookup -->
## 🔍 Quick Lookup Guide

### By Topic

| I need... | Load File | Section |
|-----------|-----------|---------|
| Script command syntax | 02_SCRIPTING_COMPLETE | Part 1: Commands A-Z |
| Create custom command | 02_SCRIPTING_COMPLETE | Part 2: BUILDIN_FUNC |
| Optimize slow script | 02_SCRIPTING_COMPLETE | Part 3: Performance |
| SC_* status effects | 03_GAME_MECHANICS | Part 1: Status Effects |
| Item bonus constants | 03_GAME_MECHANICS | Part 2: Item Bonuses |
| Job masks (EAJ_*) | 03_GAME_MECHANICS | Part 3: Job System |
| Mapflags (mf_*) | 03_GAME_MECHANICS | Part 4: Mapflags |
| Element damage table | 03_GAME_MECHANICS | Part 5: Element Table |
| Battle config settings | 03_GAME_MECHANICS | Part 6: Battle Config |
| Create custom items | 04_CONTENT_CREATION | Item Patterns |
| Create quests | 04_CONTENT_CREATION | Quest Patterns |
| Custom @ commands | 05_SOURCE_DEVELOPMENT | ACMD_FUNC Guide |
| Database C++ | 06_DATABASE_SYSTEMS | YAML Parsing |
| Packet handling | 06_DATABASE_SYSTEMS | Packet Reference |
| Damage formulas | 07_INTERNALS_REFERENCE | Battle Calculations |
| Server setup guides | 08_SOURCE_REFERENCE | Tutorials |
| NPC examples (100+) | 08_SOURCE_REFERENCE | Script Examples |

---

<!-- RAG_CHUNK: validation_status -->
## ✅ Source Validation Status

All data verified against rAthena GitHub source:

| Content | Source File | Status |
|---------|-------------|--------|
| Script Commands | doc/script_commands.txt | ✅ 766 commands verified |
| Status Effects | src/map/status.hpp | ✅ SC_* constants verified |
| Item Bonuses | doc/item_bonus.txt | ✅ 263 bonuses verified |
| Battle Config | conf/battle/*.conf | ✅ 550 settings verified |
| Element Table | db/re/attr_fix.yml | ✅ Values verified |
| Job Constants | src/map/pc.hpp | ✅ EAJ_* verified |
| Mapflags | doc/mapflags.txt | ✅ mf_* verified |

**No fabricated data. No unverified claims. 100% traceable to source.**

---

<!-- RAG_CHUNK: loading_strategy -->
## 📖 Recommended Loading Strategy

### For NPC Scripters
```
Load: 02_SCRIPTING_COMPLETE + 03_GAME_MECHANICS
```

### For Content Creators
```
Load: 04_CONTENT_CREATION + 03_GAME_MECHANICS
```

### For C++ Developers
```
Load: 05_SOURCE_DEVELOPMENT_COMPLETE + 06_DATABASE_SYSTEMS
```

### For Server Admins
```
Load: 03_GAME_MECHANICS (battle configs) + 08_SOURCE_REFERENCE (tutorials)
```

---

<!-- RAG_CHUNK: cross_references -->
## 🔗 Cross-Reference Index

### Script Commands → Constants
- `sc_start` uses SC_* from 03_GAME_MECHANICS Part 1
- `bonus` uses constants from 03_GAME_MECHANICS Part 2
- `jobchange` uses EAJ_* from 03_GAME_MECHANICS Part 3
- `setmapflag` uses mf_* from 03_GAME_MECHANICS Part 4

### Content → Scripts
- Item patterns in 04 use commands from 02
- Quest patterns in 04 use SC_* from 03

### Source → Internals
- ACMD_FUNC in 05 relates to commands in 02
- Battle calcs in 07 use formulas from 03

---

*KB v7.0 Ultimate - The definitive rAthena knowledge base for AI/LLM systems*
