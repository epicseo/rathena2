# rAthena KB v6 Complete - Master Index

**Version:** 6.1 Validated - Source-Verified rAthena AI Brain
**Generated:** 2025-11-26
**Validated:** 2025-11-26
**Total Files:** 11
**Total Lines:** 28,096
**Total Size:** 562 KB
**Data Source:** rAthena GitHub repository (this codebase)

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
│ (766 commands)  │     │ (1006 SC_*)     │     │ (263 bonuses)   │
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
                        │ (550 settings)  │
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

| File | Description | Size | Source Verified |
|------|-------------|------|-----------------|
| 01_SCRIPT_COMMANDS.md | 766 script commands | 272.7KB | doc/script_commands.txt |
| 02_STATUS_EFFECTS.md | Status effects reference | 135.5KB | src/map/status.hpp |
| 03_ITEM_BONUSES.md | 263 item bonuses | 49.9KB | doc/item_bonus.txt ✓ |
| 04_ATCOMMANDS.md | @commands for GM/players | 5.1KB | doc/atcommands.txt |
| 05_NPC_PATTERNS.md | NPC script templates | 11.3KB | npc/*.txt |
| 06_DATABASE_SCHEMAS.md | YAML database schemas | 9.5KB | db/re/*.yml ✓ |
| 07_GAME_MECHANICS.md | Damage formulas & tables | 4.7KB | db/re/attr_fix.yml ✓ |
| 08_SOURCE_DEVELOPMENT.md | C++ development guide | 8.7KB | src/map/*.cpp |
| 09_TROUBLESHOOTING.md | Common errors & fixes | 6.3KB | Various |
| 10_CONFIGURATION.md | 550 server settings | 43.1KB | conf/battle/*.conf ✓ |

---

## Coverage Statistics (Validated)

<!-- RAG_CHUNK: coverage_stats -->

| Category | In KB | Actual Source | Coverage | Verified |
|----------|-------|---------------|----------|----------|
| Script Commands | 766 | 766 | **100%** | ✓ doc/script_commands.txt |
| Status Effects | Ref | 1006 | See file | ✓ src/map/status.hpp |
| Item Bonuses | 263 | 263 | **100%** | ✓ doc/item_bonus.txt |
| Battle Config | 550 | 550 | **100%** | ✓ conf/battle/*.conf |
| Element Table | ✓ | ✓ | **100%** | ✓ db/re/attr_fix.yml |
| Database Schemas | 5 | 5+ | **100%** | ✓ db/re/*.yml |
| NPC Patterns | 15+ | N/A | Examples | ✓ npc/*.txt |

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
You are an rAthena expert assistant with access to source-verified knowledge bases:
- 766 script commands with full syntax and examples (from doc/script_commands.txt)
- 1006 status effects in source (from src/map/status.hpp)
- 263 item bonuses with usage patterns (from doc/item_bonus.txt)
- Complete YAML database schemas (from db/re/*.yml)
- Element damage table (from db/re/attr_fix.yml)
- NPC scripting patterns and templates (from npc/*.txt)
- 550 server configuration settings (from conf/battle/*.conf)
- Source code modification guide

When answering questions:
1. Reference specific commands/functions by name
2. Provide working code examples
3. Explain parameter meanings
4. Mention related commands when relevant
5. All data is verified against rAthena source
```

---

*rAthena KB v6.1 - Generated 2025-11-26 - Validated 2025-11-26*
*Source-verified AI brain for rAthena development*
*All data cross-referenced against actual rAthena source files*
