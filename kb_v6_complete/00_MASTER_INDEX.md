# rAthena KB v6.1 - Master Index (8-File Edition)

**Version:** 6.1 Validated
**Total Files:** 8
**Total Size:** 547 KB
**Source:** rAthena GitHub (this codebase)

---

## Architecture

```
┌───────────────────────────────────────────────────────┐
│              00_MASTER_INDEX.md (this file)           │
│                  Navigation & Query Router            │
└───────────────────────────┬───────────────────────────┘
                            │
    ┌───────────────────────┼───────────────────────────┐
    │                       │                           │
    ▼                       ▼                           ▼
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│ 01_SCRIPT_   │    │ 02_STATUS_   │    │ 03_ITEM_     │
│ COMMANDS     │    │ EFFECTS      │    │ BONUSES      │
│ (766 cmds)   │    │ (SC_*)       │    │ (263 bonus)  │
└──────────────┘    └──────────────┘    └──────────────┘
    │                       │                           │
    ▼                       ▼                           ▼
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│ 04_CONFIG-   │    │ 05_NPC_      │    │ 06_GAME_     │
│ URATION      │    │ SCRIPTING    │    │ REFERENCE    │
│ (550 conf)   │    │ + DB Schema  │    │ + @Commands  │
└──────────────┘    └──────────────┘    └──────────────┘
                            │
                            ▼
                    ┌──────────────┐
                    │ 07_DEVELOP-  │
                    │ MENT         │
                    │ + Debug      │
                    └──────────────┘
```

---

## Query Routing

<!-- RAG_CHUNK: query_routing -->

| User Intent | Go To |
|-------------|-------|
| Write NPC scripts | 01_SCRIPT_COMMANDS |
| Add status effect | 02_STATUS_EFFECTS |
| Create custom item | 03_ITEM_BONUSES |
| Configure server | 04_CONFIGURATION |
| Make shop/warp/quest NPC | 05_NPC_SCRIPTING |
| Edit item_db.yml | 05_NPC_SCRIPTING |
| Use @commands | 06_GAME_REFERENCE |
| Understand damage formula | 06_GAME_REFERENCE |
| Modify source code | 07_DEVELOPMENT |
| Fix script errors | 07_DEVELOPMENT |

### By Keyword

| Keyword | Primary KB |
|---------|------------|
| mes, getitem, warp, script | 01_SCRIPT_COMMANDS |
| SC_*, status, buff, debuff | 02_STATUS_EFFECTS |
| bonus, bStr, bAtk | 03_ITEM_BONUSES |
| conf, battle.conf, setting | 04_CONFIGURATION |
| shop, quest, instance, YAML | 05_NPC_SCRIPTING |
| @item, @warp, damage, element | 06_GAME_REFERENCE |
| C++, source, error, debug | 07_DEVELOPMENT |

---

## File Index

<!-- RAG_CHUNK: file_index -->

| # | File | Description | Size | Source |
|---|------|-------------|------|--------|
| 00 | MASTER_INDEX | Navigation | 9 KB | - |
| 01 | SCRIPT_COMMANDS | 766 commands | 273 KB | doc/script_commands.txt |
| 02 | STATUS_EFFECTS | SC_* reference | 136 KB | src/map/status.hpp |
| 03 | ITEM_BONUSES | 263 bonuses | 50 KB | doc/item_bonus.txt |
| 04 | CONFIGURATION | 550 settings | 43 KB | conf/battle/*.conf |
| 05 | NPC_SCRIPTING | Patterns + DB | 10 KB | npc/*.txt, db/re/*.yml |
| 06 | GAME_REFERENCE | @Cmds + Mech | 7 KB | doc/atcommands.txt |
| 07 | DEVELOPMENT | Source + Debug | 7 KB | src/map/*.cpp |

---

## Coverage (Validated)

| Category | Count | Source | Status |
|----------|-------|--------|--------|
| Script Commands | 766 | doc/script_commands.txt | ✓ |
| Status Effects | 1006 | src/map/status.hpp | ✓ |
| Item Bonuses | 263 | doc/item_bonus.txt | ✓ |
| Battle Config | 550 | conf/battle/*.conf | ✓ |
| Element Table | 100 | db/re/attr_fix.yml | ✓ |
| Database Schemas | 4 | db/re/*.yml | ✓ |

---

## Quick Reference

### Common Script Commands
```c
mes "text";              // Display message
next;                    // Wait for click
close;                   // End dialog
getitem <id>,<amount>;   // Give item
delitem <id>,<amount>;   // Remove item
warp "<map>",<x>,<y>;    // Teleport
sc_start <SC>,<ms>,<val>; // Apply status
```

### Common Bonuses
```c
bonus bStr,5;            // +5 STR
bonus bAllStats,10;      // +10 all stats
bonus bMaxHP,1000;       // +1000 Max HP
bonus2 bAddRace,RC_Undead,20; // +20% vs Undead
```

### Common Status Effects
```c
SC_BLESSING    // +STR/DEX/INT
SC_INCREASEAGI // +AGI/Speed
SC_POISON      // DoT damage
SC_STUN        // Cannot act
```

---

## System Prompt Template

```
You are an rAthena expert with source-verified knowledge:
- 766 script commands (doc/script_commands.txt)
- 1006 status effects (src/map/status.hpp)
- 263 item bonuses (doc/item_bonus.txt)
- 550 battle config settings (conf/battle/*.conf)
- Element table (db/re/attr_fix.yml)
- Database schemas (db/re/*.yml)
- NPC patterns (npc/*.txt)

All data verified against rAthena source.
```

---

*rAthena KB v6.1 - 8-File Edition*
*Source-verified, no fake data*
