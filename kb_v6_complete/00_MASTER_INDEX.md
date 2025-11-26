# rAthena KB v6 Complete - Master Index

**Version:** 6.0 Complete - The Ultimate rAthena AI Brain
**Generated:** 2025-11-26
**Total Files:** 10
**Total Lines:** 27,900
**Total Size:** 546.7 KB

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        00_MASTER_INDEX.md (this file)                       │
│                     Navigation Hub & Query Router                           │
└───────────────────────────────────┬─────────────────────────────────────────┘
                                    │
    ┌───────────────────────────────┼───────────────────────────────┐
    │                               │                               │
    ▼                               ▼                               ▼
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│ 01_SCRIPT_      │     │ 02_STATUS_      │     │ 03_ITEM_        │
│ COMMANDS        │     │ EFFECTS         │     │ BONUSES         │
│ (768 commands)  │     │ (670 SC_*)      │     │ (263 bonuses)   │
└─────────────────┘     └─────────────────┘     └─────────────────┘
    │                               │                               │
    ▼                               ▼                               ▼
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│ 04_ATCOMMANDS   │     │ 05_NPC_PATTERNS │     │ 06_DATABASE_    │
│ (@commands)     │     │ (templates)     │     │ SCHEMAS         │
└─────────────────┘     └─────────────────┘     └─────────────────┘
    │                               │                               │
    ▼                               ▼                               ▼
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│ 07_GAME_        │     │ 08_SOURCE_      │     │ 09_TROUBLE-     │
│ MECHANICS       │     │ DEVELOPMENT     │     │ SHOOTING        │
└─────────────────┘     └─────────────────┘     └─────────────────┘
                                    │
                                    ▼
                        ┌─────────────────┐
                        │ 10_CONFIG-      │
                        │ URATION         │
                        │ (566 settings)  │
                        └─────────────────┘
```

---

## Query Routing Table

<!-- RAG_CHUNK: query_routing -->

### "I want to..." → Primary KB File

| User Intent | Go To | Secondary |
|-------------|-------|-----------|
| **Write NPC scripts** | 01_SCRIPT_COMMANDS | 05_NPC_PATTERNS |
| **Use script commands** | 01_SCRIPT_COMMANDS | - |
| **Add status effect** | 02_STATUS_EFFECTS | 01_SCRIPT_COMMANDS |
| **Create custom item** | 03_ITEM_BONUSES | 06_DATABASE_SCHEMAS |
| **Use @commands** | 04_ATCOMMANDS | - |
| **Make shop/warp/quest NPC** | 05_NPC_PATTERNS | 01_SCRIPT_COMMANDS |
| **Edit item_db.yml** | 06_DATABASE_SCHEMAS | 03_ITEM_BONUSES |
| **Understand damage formula** | 07_GAME_MECHANICS | - |
| **Modify source code** | 08_SOURCE_DEVELOPMENT | - |
| **Fix script errors** | 09_TROUBLESHOOTING | 01_SCRIPT_COMMANDS |
| **Configure server** | 10_CONFIGURATION | - |

### By Keyword

| Keyword | Primary KB |
|---------|------------|
| mes, getitem, delitem, warp | 01_SCRIPT_COMMANDS |
| SC_*, status, buff, debuff | 02_STATUS_EFFECTS |
| bonus, bStr, bAtk | 03_ITEM_BONUSES |
| @item, @warp, @who | 04_ATCOMMANDS |
| shop, quest, daily, instance | 05_NPC_PATTERNS |
| item_db, skill_db, mob_db, YAML | 06_DATABASE_SCHEMAS |
| damage, formula, element, size | 07_GAME_MECHANICS |
| C++, atcommand, source, build | 08_SOURCE_DEVELOPMENT |
| error, bug, fix, debug | 09_TROUBLESHOOTING |
| conf, battle.conf, setting | 10_CONFIGURATION |

---

## File Index

| File | Description | Size |
|------|-------------|------|
| 01_SCRIPT_COMMANDS.md | 768 script commands reference | 272.7KB |
| 02_STATUS_EFFECTS.md | 670 status effects with val1-4 | 135.5KB |
| 03_ITEM_BONUSES.md | 263 item bonuses with examples | 49.9KB |
| 04_ATCOMMANDS.md | @commands for GM/players | 5.1KB |
| 05_NPC_PATTERNS.md | NPC script templates & patterns | 11.3KB |
| 06_DATABASE_SCHEMAS.md | YAML database schemas | 9.5KB |
| 07_GAME_MECHANICS.md | Damage formulas & tables | 4.6KB |
| 08_SOURCE_DEVELOPMENT.md | C++ development guide | 8.7KB |
| 09_TROUBLESHOOTING.md | Common errors & fixes | 6.3KB |
| 10_CONFIGURATION.md | 566 server settings | 43.1KB |

---

## Coverage Statistics

<!-- RAG_CHUNK: coverage_stats -->

| Category | Documented | Source Count | Coverage |
|----------|-----------|--------------|----------|
| Script Commands | 768 | ~750 | **102%** |
| Status Effects (SC_*) | 670 | ~700 | **96%** |
| Item Bonuses | 263 | 263 | **100%** |
| @Commands | 200+ | ~300 | **67%** |
| Battle Config | 566 | ~600 | **94%** |
| NPC Patterns | 15+ | N/A | - |
| Database Schemas | 5 | 5 | **100%** |

---

## How to Use This KB

### For AI/RAG Systems

1. **Always load 00_MASTER_INDEX.md first** for query routing
2. **Match keywords** to identify relevant KB files
3. **Load specific files** based on user query
4. **Use RAG_CHUNK markers** for targeted retrieval

### Example Query Flow

```
User: "How do I give a player 10 Red Potions?"

1. Keyword match: "give" + "player" + "potion" → 01_SCRIPT_COMMANDS
2. Load 01_SCRIPT_COMMANDS.md
3. Search for "getitem" command
4. Return: getitem 501, 10; or getitem Red_Potion, 10;
```

---

## Quick Reference Card

<!-- RAG_CHUNK: quick_reference -->

### Most Common Script Commands
```c
mes "text";              // Display message
next;                    // Wait for player to click
close;                   // End dialog
menu "opt1",L1,"opt2",L2; // Show menu
getitem <id>,<amount>;   // Give item
delitem <id>,<amount>;   // Remove item
Zeny += 1000;            // Give zeny
warp "<map>",<x>,<y>;    // Teleport player
sc_start <SC>,<ms>,<val>; // Apply status
```

### Most Common Bonuses
```c
bonus bStr,5;            // +5 STR
bonus bAllStats,10;      // +10 all stats
bonus bMaxHP,1000;       // +1000 Max HP
bonus bAtk,50;           // +50 ATK
bonus2 bAddRace,RC_Undead,20; // +20% vs Undead
bonus2 bAddEff,Eff_Stun,500;  // 5% stun chance
bonus3 bAutoSpell,"MG_FIREBOLT",5,100; // 10% autocast
```

### Most Common Status Effects
```c
SC_BLESSING    // +STR/DEX/INT
SC_INCREASEAGI // +AGI/Speed
SC_POISON      // DoT damage
SC_STUN        // Cannot act
SC_FREEZE      // Frozen
SC_STONE       // Petrified
```

---

## System Prompt Template

For AI systems using this KB, include in system prompt:

```
You are an rAthena expert assistant with access to comprehensive knowledge bases:
- 768 script commands with full syntax and examples
- 670 status effects with val1-val4 parameters
- 263 item bonuses with usage patterns
- Complete YAML database schemas
- NPC scripting patterns and templates
- Server configuration reference
- Source code modification guide

When answering questions:
1. Reference specific commands/functions by name
2. Provide working code examples
3. Explain parameter meanings
4. Mention related commands when relevant
```

---

*rAthena KB v6 Complete - Generated 2025-11-26*
*The definitive AI brain for rAthena development*
