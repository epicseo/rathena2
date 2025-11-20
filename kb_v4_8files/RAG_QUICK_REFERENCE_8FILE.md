# rAthena KB v4.0.1 - RAG Quick Reference (8-File Edition)

**Purpose:** Fast file selection for AI/LLM systems
**Version:** 4.0.1 (8-File Optimized)
**Last Updated:** 2025-11-19

---

## 📊 Quick File Selection Matrix

| Query Type | Load File(s) | Query Examples |
|------------|--------------|----------------|
| **Script syntax** | 02_SCRIPTING | "How to use getitem?", "mes syntax" |
| **Constants** | 03_GAME_MECHANICS | "What is SC_BLESSING?", "bAddRace", "RC_Demon" |
| **Content creation** | 04_CONTENT + 02 + 03 | "Create gacha", "Weekly quest" |
| **Source mods** | **05_SOURCE_DEV_COMPLETE** ⭐ | "Add @command", "BUILDIN_FUNC" |
| **Security** | **05_SOURCE_DEV_COMPLETE** ⭐ | "Prevent exploit", "Input validation" |
| **Crashes/Safety** | **05_SOURCE_DEV_COMPLETE** | "Fix segfault", "nullpo", "bl->prev" |
| **Database** | 06_DATABASE | "item_db.find()", "YAML parsing" |
| **Packets** | 06_DATABASE | "CZ_*", "WFIFO", "custom packet" |
| **Compilation** | 06_DATABASE | "cmake", "GDB", "build error" |
| **Battle internals** | **07_INTERNALS (Part 1)** ⭐ | "Damage calc", "ATK formula" |
| **Script internals** | **07_INTERNALS (Part 2)** ⭐ | "script_state", "timer", "freeloop" |
| **Expert tutorials** | 08_SOURCE_REFERENCE | "Advanced tutorial", "src/" |

⭐ = **Changed from v4.0 (10-file edition)**

---

## 📚 The 8 Files

### 01_MASTER_INDEX.md (1K lines)
**Same as v4.0**
- Navigation hub
- Quick reference
- Learning paths

### 02_SCRIPTING_COMPLETE.md (16K lines)
**Same as v4.0**
- All 767+ commands
- BUILDIN_FUNC creation
- Performance optimization

### 03_GAME_MECHANICS.md (4K lines)
**Same as v4.0**
- Status effects (SC_*)
- Item bonuses (bonus)
- Job system (EAJ_*)
- Mapflags (mf_*)

### 04_CONTENT_CREATION.md (5K lines)
**Same as v4.0**
- Item groups (gacha)
- Quest system
- NPC patterns (12)

### 05_SOURCE_DEVELOPMENT_COMPLETE.md (8K lines) ⭐ NEW
**Merged: v4.0 File 05 + File 09**

**Contains:**
- Part 1: Plugin System (ACMD_FUNC, BUILDIN_FUNC)
- Part 2: Best Practices (code quality)
- Part 3: Memory Crash Patterns (ERS, bl->prev)
- Part 4: Source Code Structure
- **Part 5: Security & Exploits** ⭐ NOW INTEGRATED

**Load when:**
- Source modifications
- Custom @commands
- Custom script commands
- Crash fixes
- **Security concerns** ⭐
- **Exploit prevention** ⭐

**Key benefit:** Security always included with source dev!

### 06_DATABASE_SYSTEMS.md (7K lines)
**Same as v4.0**
- Database C++ (item_db.find())
- Packet structure (CZ_*, ZC_*)
- Compilation & debugging

### 07_INTERNALS_REFERENCE.md (2K lines) ⭐ NEW
**Merged: v4.0 File 07 + File 08**

**Contains:**
- **Part 1: Battle & Status Internals** (damage calc, formulas)
- **Part 2: Script Engine Internals** (timer system, crashes)

**Load when:**
- Battle calculations → Part 1
- Damage formulas → Part 1
- Script crashes → Part 2
- Timer issues → Part 2
- Advanced debugging

**Key benefit:** All internals in one place!

### 08_SOURCE_REFERENCE.md (35K lines)
**Same as v4.0 File 10 (renumbered)**
- 420+ tutorials
- Expert examples
- Source modification guides

---

## 🎯 Query Pattern Changes from v4.0

### Security Queries
```
v4.0 (10-File):
  Load: 09_SECURITY_GUIDE.md

v4.0.1 (8-File):
  Load: 05_SOURCE_DEVELOPMENT_COMPLETE.md (Part 5) ⭐
```

### Crash/Safety Queries
```
v4.0 (10-File):
  Load: 05_SOURCE_DEVELOPMENT.md

v4.0.1 (8-File):
  Load: 05_SOURCE_DEVELOPMENT_COMPLETE.md (includes security) ⭐
```

### Battle Internals Queries
```
v4.0 (10-File):
  Load: 07_BATTLE_STATUS.md

v4.0.1 (8-File):
  Load: 07_INTERNALS_REFERENCE.md (Part 1) ⭐
```

### Script Internals Queries
```
v4.0 (10-File):
  Load: 08_SCRIPT_INTERNALS.md

v4.0.1 (8-File):
  Load: 07_INTERNALS_REFERENCE.md (Part 2) ⭐
```

---

## 🔍 Keyword Index

### Commands & Functions
- mes, getitem, setquest → **02_SCRIPTING**
- sc_start, bonus → **02_SCRIPTING** + **03_GAME_MECHANICS**

### Constants
- SC_*, status effects → **03_GAME_MECHANICS** (Part 1)
- bonus types, RC_*, Ele_* → **03_GAME_MECHANICS** (Part 2)
- EAJ_*, job masks → **03_GAME_MECHANICS** (Part 3)
- mf_*, mapflags → **03_GAME_MECHANICS** (Part 4)

### C++ Development
- ACMD_FUNC, BUILDIN_FUNC → **05_SOURCE_DEV_COMPLETE** ⭐
- nullpo, bl->prev → **05_SOURCE_DEV_COMPLETE** ⭐
- ERS, map_freeblock → **05_SOURCE_DEV_COMPLETE** ⭐

### Security (Now in File 05!)
- exploit, security → **05_SOURCE_DEV_COMPLETE (Part 5)** ⭐
- item dupe, SQL injection → **05_SOURCE_DEV_COMPLETE (Part 5)** ⭐
- input validation → **05_SOURCE_DEV_COMPLETE (Part 5)** ⭐

### Internals
- damage calc, battle → **07_INTERNALS (Part 1)** ⭐
- script_state, timer → **07_INTERNALS (Part 2)** ⭐

---

## 💡 Loading Strategy

### Single-File (85% of queries)
```
Script command → 02_SCRIPTING only
Constant lookup → 03_GAME_MECHANICS only
Security → 05_SOURCE_DEV_COMPLETE only ⭐ (was 09 in v4.0)
```

### Two-File (12% of queries)
```
Apply status → 02_SCRIPTING + 03_GAME_MECHANICS
Add @command → 05_SOURCE_DEV_COMPLETE + 06_DATABASE (if compile)
```

### Multi-File (3% of queries)
```
Complete quest system → 04_CONTENT + 02_SCRIPTING + 03_GAME_MECHANICS
```

---

## 📏 File Size Reference

| File | Lines | Load Priority | Frequency |
|------|-------|---------------|-----------|
| 01_MASTER_INDEX | 1,064 | Always first | 100% |
| 02_SCRIPTING_COMPLETE | 16,054 | High | 50% |
| 03_GAME_MECHANICS | 3,685 | High | 45% |
| 04_CONTENT_CREATION | 5,060 | Medium | 25% |
| 05_SOURCE_DEV_COMPLETE | 7,932 | Medium | 25% ⭐ |
| 06_DATABASE_SYSTEMS | 7,104 | Low | 12% |
| 07_INTERNALS_REFERENCE | 1,785 | Low | 8% ⭐ |
| 08_SOURCE_REFERENCE | 35,014 | Low | 10% |

---

## ⚡ Benefits vs v4.0 (10-File)

✅ **Fewer files** (10 → 8)
✅ **Security integrated** with source dev (File 05)
✅ **Internals grouped** (File 07)
✅ **Same efficiency** (1.2 files/query avg)
✅ **100% content** preserved

---

**Use this for quick file selection in your RAG system!**
