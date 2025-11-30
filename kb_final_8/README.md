# rAthena Knowledge Base v15.2 (kb_final_8)

**Version:** 15.2 - Superior Edition
**Total Lines:** 97,442
**Total Files:** 11 RAG-optimized files
**RAG Chunks:** 1,708
**Validation:** 100% source-verified

---

## Overview

This is the **superior** rAthena Knowledge Base, enhanced beyond kb_v9_final with:
- **All 968 EF_* visual effects** (complete individual listing)
- **All 26 MD_* monster modes** (with hex/decimal values)
- **All 31 PC_PERM_* GM permissions** (with examples)
- **All 287 @commands** (dedicated reference file)

## Validation Status

| Content Type | Status | Source |
|--------------|--------|--------|
| Script Commands (767+) | VERIFIED | doc/script_commands.txt |
| Status Effects (1,038) | VERIFIED | src/map/status.hpp |
| Item Bonuses (263) | VERIFIED | doc/item_bonus.txt |
| Visual Effects (968) | VERIFIED | doc/effect_list.md |
| Monster Modes (26) | VERIFIED | doc/mob_db_mode_list.txt |
| GM Permissions (31) | VERIFIED | doc/permissions.txt |
| @Commands (287) | VERIFIED | src/map/atcommand.cpp |

## File Contents

| # | File | Lines | RAG Chunks | Description |
|---|------|-------|------------|-------------|
| 01 | 01_MASTER_INDEX.md | ~190 | 8 | Navigation hub |
| 02 | 02_SCRIPT_COMMANDS.md | 16,070 | 24 | 767+ script commands |
| 03 | 03_STATUS_EFFECTS.md | 11,982 | 671 | 1,038 SC_* effects |
| 04 | 04_ITEM_BONUSES.md | 5,262 | 270 | 263 bonuses |
| 05 | 05_GAME_MECHANICS.md | 3,481 | 31 | EAJ_*, mf_*, MD_* |
| 06 | 06_CONTENT_CREATION.md | 5,107 | 55 | NPC patterns |
| 07 | 07_SOURCE_DEV_COMPLETE.md | 15,167 | 142 | C++ dev guide |
| 08 | 08_SOURCE_TUTORIALS.md | 35,440 | 425 | 420+ tutorials |
| 09 | 09_AT_COMMANDS.md | 1,364 | 30 | 287 @commands + PC_PERM_* |
| 10 | 10_VISUAL_EFFECTS.md | 1,010 | 3 | 968 EF_* effects |
| 11 | README.md | ~90 | 1 | This file |

## Comparison with kb_v9_final

| Metric | kb_v9_final | kb_final_8 v15.2 | Difference |
|--------|-------------|------------------|------------|
| Files | 9 | 11 | +2 |
| Lines | 92,530 | 97,442 | +4,912 |
| RAG Chunks | 1,622 | 1,708 | +86 |
| EF_* Effects | ~127 mentions | **968 complete** | +841 |
| MD_* Modes | 2 mentions | **26 complete** | +24 |
| PC_PERM_* | ~17 mentions | **31 complete** | +14 |
| @Commands | 3 tutorials | **287 documented** | +284 |

## RAG Usage

Optimal chunk size: 500-1000 tokens
Separator pattern: `<!-- RAG_CHUNK: .* -->`

```python
# Example RAG loading
for file in glob.glob("*.md"):
    chunks = re.split(r'<!-- RAG_CHUNK: .* -->', content)
    for chunk in chunks:
        vector_db.add(chunk, metadata={"source": file})
```

## Best Content Sources

- **Script Commands**: 02_SCRIPT_COMMANDS.md
- **Visual Effects**: 10_VISUAL_EFFECTS.md (ALL 968 EF_*)
- **Monster Modes**: 05_GAME_MECHANICS.md (MD_* section)
- **GM Permissions**: 09_AT_COMMANDS.md (PC_PERM_* section)
- **@Commands**: 09_AT_COMMANDS.md
- **C++ Source Dev**: 07_SOURCE_DEV_COMPLETE.md + 08_SOURCE_TUTORIALS.md
