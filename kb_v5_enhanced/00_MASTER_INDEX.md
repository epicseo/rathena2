# rAthena KB v5 - Master Index & Navigation Hub

**Version:** 5.0 Enhanced
**Generated:** 2025-11-26
**Architecture:** RAG-Optimized for AI/LLM Systems

---

## KB v5 Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                     00_MASTER_INDEX.md (this file)                      │
│                        Navigation & Query Routing                       │
└───────────────────────────────────┬─────────────────────────────────────┘
                                    │
        ┌───────────────────────────┼───────────────────────────┐
        │                           │                           │
        ▼                           ▼                           ▼
┌───────────────────┐     ┌───────────────────┐     ┌───────────────────┐
│ 01_SCRIPT_        │     │ 02_STATUS_        │     │ 03_ITEM_          │
│ COMMANDS_COMPLETE │     │ EFFECTS_COMPLETE  │     │ BONUSES_COMPLETE  │
│ (598 commands)    │     │ (670 SC_*)        │     │ (263 bonuses)     │
└───────────────────┘     └───────────────────┘     └───────────────────┘
        │                           │                           │
        │                           │                           │
        ▼                           ▼                           ▼
┌───────────────────┐     ┌───────────────────┐     ┌───────────────────┐
│ 04_DATABASE_      │     │ 05_GAME_          │     │ 06_SOURCE_        │
│ SYSTEMS           │     │ MECHANICS         │     │ DEVELOPMENT       │
│ (YAML schemas)    │     │ (formulas/rules)  │     │ (C++ reference)   │
└───────────────────┘     └───────────────────┘     └───────────────────┘
```

---

## Query Routing Guide

<!-- RAG_CHUNK: query_routing -->

### "I want to..." → Go to KB File

| User Intent | Primary KB | Secondary KB |
|-------------|------------|--------------|
| Write NPC scripts | 01_SCRIPT_COMMANDS | - |
| Use script commands (mes, getitem, etc.) | 01_SCRIPT_COMMANDS | - |
| Add status effect to player | 02_STATUS_EFFECTS | 01_SCRIPT_COMMANDS |
| Understand SC_* constants | 02_STATUS_EFFECTS | - |
| Create custom item effects | 03_ITEM_BONUSES | 01_SCRIPT_COMMANDS |
| Use bonus/bonus2/bonus3 commands | 03_ITEM_BONUSES | - |
| Edit item_db.yml | 04_DATABASE_SYSTEMS | 03_ITEM_BONUSES |
| Edit skill_db.yml | 04_DATABASE_SYSTEMS | 02_STATUS_EFFECTS |
| Edit mob_db.yml | 04_DATABASE_SYSTEMS | - |
| Understand damage formulas | 05_GAME_MECHANICS | - |
| Modify source code | 06_SOURCE_DEVELOPMENT | - |
| Create custom atcommand | 06_SOURCE_DEVELOPMENT | - |

---

## File Contents Summary

### 01_SCRIPT_COMMANDS_COMPLETE.md
**Size:** ~367KB | **Lines:** ~13,000 | **Commands:** 598

Categories covered:
- Basic Commands (mes, close, next, menu)
- Item Management (getitem, delitem, countitem)
- Player Data (getcharid, readparam, strcharinfo)
- Variables & Arrays (set, setarray, getarraysize)
- Math & Logic Operations
- Events & Timers (addtimer, deltimer)
- Instance Management (instance_create, instance_attach)
- Guild & Party Functions
- Battle & Combat
- Database Access

### 02_STATUS_EFFECTS_COMPLETE.md
**Size:** ~165KB | **Lines:** ~11,000 | **Effects:** 670

Categories covered:
- Common Ailments (SC_STONE, SC_FREEZE, SC_STUN, SC_POISON, etc.)
- Buff Effects (SC_BLESSING, SC_INCREASEAGI, SC_GLORIA, etc.)
- Skill Effects (SC_EDP, SC_BERSERK, SC_AUTOGUARD, etc.)
- Food Effects (SC_STRFOOD, SC_AGIFOOD, etc.)
- 3rd Job Skills (SC_ENCHANTBLADE, SC_INSPIRATION, etc.)
- 4th Job Skills (SC_SERVANTWEAPON, SC_CLIMAX, etc.)

### 03_ITEM_BONUSES_COMPLETE.md
**Size:** ~69KB | **Lines:** ~5,000 | **Bonuses:** 263

Categories covered:
- Basic Stats (bStr, bAgi, bVit, bInt, bDex, bLuk)
- HP/SP Bonuses (bMaxHP, bMaxSP, bHPrecovRate)
- Attack/Defense (bAtk, bDef, bMatk, bMdef)
- Cast Time (bCastrate, bFixedCast, bVariableCast)
- Damage Modifiers (bAddRace, bAddEle, bSubRace)
- AutoSpell (bAutoSpell, bAutoSpellWhenHit)
- Status Effects (bAddEff, bResEff)

---

## Common Query Patterns

<!-- RAG_CHUNK: common_queries -->

### Script Commands
```
Q: "How do I give items to a player?"
A: Use `getitem` command - see 01_SCRIPT_COMMANDS

Q: "How do I check if player has an item?"
A: Use `countitem` command - see 01_SCRIPT_COMMANDS

Q: "How do I make NPC dialog?"
A: Use `mes`, `next`, `close` commands - see 01_SCRIPT_COMMANDS
```

### Status Effects
```
Q: "How do I apply poison to a player?"
A: Use `sc_start SC_POISON, duration, level;` - see 02_STATUS_EFFECTS

Q: "What does SC_BLESSING do?"
A: Increases STR/DEX/INT - see 02_STATUS_EFFECTS

Q: "How do I remove a status effect?"
A: Use `sc_end SC_NAME;` - see 02_STATUS_EFFECTS
```

### Item Bonuses
```
Q: "How do I add ATK to an item?"
A: Use `bonus bAtk,n;` in item script - see 03_ITEM_BONUSES

Q: "How do I make item give status effect?"
A: Use `bonus2 bAddEff,Eff_Poison,rate;` - see 03_ITEM_BONUSES

Q: "How do I add race damage bonus?"
A: Use `bonus2 bAddRace,RC_Undead,20;` - see 03_ITEM_BONUSES
```

---

## KB Statistics

| Metric | Value |
|--------|-------|
| Total KB Files | 6 |
| Total Lines | ~30,000+ |
| Total Size | ~600KB+ |
| Script Commands | 598 |
| Status Effects | 670 |
| Item Bonuses | 263 |
| Coverage vs rAthena Source | ~95% |

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 5.0 | 2025-11-26 | Complete rewrite with full source parsing |
| 4.0 | 2024-xx-xx | Previous architecture (8 files) |

---

## RAG System Integration Notes

### Chunk Markers
All KB files use `<!-- RAG_CHUNK: chunk_name -->` markers for AI systems to identify content sections.

### Recommended Loading Strategy
1. Always load 00_MASTER_INDEX.md first for query routing
2. Load specific KB file(s) based on query topic
3. For complex queries, load multiple related KBs

### Token Optimization
- Each KB file is structured for selective loading
- Section headers enable targeted retrieval
- Cross-references minimize duplication

---

*Generated as part of rAthena KB v5 Enhanced Package*
