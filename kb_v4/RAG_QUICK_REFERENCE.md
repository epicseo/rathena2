# rAthena KB v4.0 - RAG Quick Reference Guide

**Purpose:** Fast reference for AI/LLM systems to determine which KB files to load
**Version:** 4.0
**Last Updated:** 2025-11-19

---

<!-- RAG_CHUNK: file_selection_matrix -->
## File Selection Matrix

### Query → File Mapping (Load Order)

| User Query Pattern | Primary File | Secondary Files | Query Examples |
|-------------------|--------------|-----------------|----------------|
| **Script command syntax** | 02_SCRIPTING | 03_GAME_MECHANICS (constants) | "How to use getitem?", "mes syntax", "sc_start parameters" |
| **Status effects (SC_*)** | 03_GAME_MECHANICS | 02_SCRIPTING (sc_start) | "What is SC_STONE?", "SC_BLESSING val1", "status effect duration" |
| **Item bonuses** | 03_GAME_MECHANICS | 02_SCRIPTING (bonus cmd) | "bAddRace", "bonus vs demons", "RC_Demon constant" |
| **Job system** | 03_GAME_MECHANICS | 02_SCRIPTING (jobchange) | "EAJ_SWORDMAN", "check 2nd class", "eaclass function" |
| **Mapflags** | 03_GAME_MECHANICS | 02_SCRIPTING (setmapflag) | "mf_pvp", "noteleport mapflag", "PvP map setup" |
| **Gacha/Item groups** | 04_CONTENT_CREATION | 02_SCRIPTING, 03_GAME_MECHANICS | "random box", "gacha system", "item_group_db" |
| **Quest system** | 04_CONTENT_CREATION | 02_SCRIPTING, 03_GAME_MECHANICS | "create quest", "quest_db", "weekly quest", "TimeLimit" |
| **NPC patterns** | 04_CONTENT_CREATION | 02_SCRIPTING | "state machine", "cooldown system", "NPC pattern" |
| **Custom @command** | 05_SOURCE_DEVELOPMENT | 09_SECURITY, 06_DATABASE | "ACMD_FUNC", "add @command", "custom command" |
| **Custom script cmd** | 05_SOURCE_DEVELOPMENT | 02_SCRIPTING (BUILDIN_FUNC) | "BUILDIN_FUNC", "create script command" |
| **Crash debugging** | 05_SOURCE_DEVELOPMENT | 08_SCRIPT_INTERNALS | "segfault", "crash", "bl->prev", "ERS", "nullpo" |
| **Source structure** | 05_SOURCE_DEVELOPMENT | 10_SOURCE_REFERENCE | "src/map/", "codebase structure", "core structs" |
| **Database ops** | 06_DATABASE_SYSTEMS | 05_SOURCE_DEVELOPMENT | "item_db.find()", "YAML parsing", "SQL queries" |
| **Packets** | 06_DATABASE_SYSTEMS | 05_SOURCE_DEVELOPMENT | "CZ_*", "ZC_*", "clif_", "WFIFO", "custom packet" |
| **Compilation** | 06_DATABASE_SYSTEMS | 05_SOURCE_DEVELOPMENT | "compile", "cmake", "build error", "GDB", "Valgrind" |
| **Battle calculations** | 07_BATTLE_STATUS | 03_GAME_MECHANICS | "damage calc", "ATK formula", "element table", "status_calc" |
| **Script internals** | 08_SCRIPT_INTERNALS | 02_SCRIPTING, 05_SOURCE | "script_state", "timer system", "freeloop", "DIFF_TICK" |
| **Security/exploits** | 09_SECURITY | 05_SOURCE_DEVELOPMENT | "exploit", "item dupe", "SQL injection", "security" |
| **Expert tutorials** | 10_SOURCE_REFERENCE | 05_SOURCE, 06_DATABASE | "tutorial", "advanced", "src/", "clif_", "pc_" |

---

<!-- RAG_CHUNK: complete_file_reference -->
## Complete File Reference

### 01_MASTER_INDEX.md (1,064 lines | 38KB)

**Load:** Always first for all queries

**Contains:**
- Navigation hub and KB overview
- Quick reference table (all 10 files)
- Navigation by role (Creator/Scripter/Developer/Debugger)
- Navigation by need (quick lookups, complex tasks)
- Complete file descriptions
- Learning paths (beginner → expert)
- RAG integration guide
- Version history

**Query Triggers:**
```
"what's in KB", "where to start", "learning path", "which file covers",
"KB overview", "how to use KB", "file organization"
```

**Use For:**
- Initial navigation
- Determining which files to load next
- Understanding KB structure
- Finding learning resources

---

### 02_SCRIPTING_COMPLETE.md (16,054 lines | 461KB)

**Merged From:** script_commands (12.6K) + ScriptCommandCreation (1.8K) + ScriptPerformance (1.6K)

**Contains:**
- **Part 1:** 767+ script commands A-Z (syntax, parameters, examples)
- **Part 2:** BUILDIN_FUNC guide (custom command creation, C++ integration)
- **Part 3:** Performance optimization (freeloop, database queries, benchmarks)

**Query Triggers:**
```
"mes", "getitem", "setquest", "sc_start", "bonus", "warp", "monster",
"script command", "NPC script", "how to script", "BUILDIN_FUNC",
"freeloop", "optimize script", "script performance"
```

**Topics Covered:**
- Dialog & Display (mes, next, close, menu, select, input)
- Item Management (getitem, delitem, countitem, getitemname)
- Quest System (setquest, completequest, checkquest, questinfo)
- Status Effects (sc_start, sc_end, checkoption)
- Equipment (getequipid, equip, unequip)
- Stats & Skills (readparam, statusup, skill, checkskill)
- Monsters (monster, areamonster, killmonster, summon)
- Movement (warp, areawarp, mapwarp)
- Timers (addtimer, deltimer, sleep, initnpctimer)
- Events (donpcevent, doevent, announce)
- Database (query_sql, escape_sql)
- Arrays (setarray, cleararray, copyarray, deletearray)
- Functions (callfunc, callsub, return, getarg)
- Variables (set, setd, getd, getvariableofnpc)
- Instance Commands (instance_create, instance_attachmap)
- Battleground Commands (bg_create, bg_join, bg_warp)

**Always Combine With:**
- 03_GAME_MECHANICS.md for constants (SC_*, bonus, EAJ_*, mf_*)
- 04_CONTENT_CREATION.md for complete NPC patterns
- 08_SCRIPT_INTERNALS.md for crash prevention

**Example Queries:**
```
Query: "How to use sc_start?"
Load: 02_SCRIPTING_COMPLETE.md (sc_start syntax)
Then: 03_GAME_MECHANICS.md (SC_* constants, val1-val4)

Query: "Optimize slow NPC script"
Load: 02_SCRIPTING_COMPLETE.md (Part 3: Performance)

Query: "Create custom script command"
Load: 02_SCRIPTING_COMPLETE.md (Part 2: BUILDIN_FUNC)
Then: 05_SOURCE_DEVELOPMENT.md (safety patterns)
```

---

### 03_GAME_MECHANICS.md (3,685 lines | 79KB)

**Merged From:** StatusEffects (768) + ItemBonuses (775) + JobSystem (669) + MapFlags (1,225)

**Contains:**
- **Part 1:** Status Effects - 50+ SC_* constants, val1-val4, durations, interactions
- **Part 2:** Item Bonuses - 100+ bonus types, RC_*, Ele_*, Size_*, BF_* constants
- **Part 3:** Job System - 150+ job constants, EAJ_* masks, job trees, eaclass/roclass
- **Part 4:** Mapflags - 100+ mf_* flags, parameters, configurations

**Query Triggers:**
```
"SC_STONE", "SC_BLESSING", "val1", "status effect",
"bAddRace", "bonus", "RC_Demon", "Ele_Fire", "Size_Large",
"EAJ_SWORDMAN", "job mask", "eaclass", "job tree",
"mf_pvp", "noteleport", "mapflag", "setmapflag"
```

**Topics Covered:**

**Status Effects:**
- Ailments: SC_STONE, SC_FREEZE, SC_STUN, SC_SLEEP, SC_POISON, SC_CURSE, SC_SILENCE, SC_BLIND
- Buffs: SC_BLESSING, SC_INC_AGI, SC_KYRIE, SC_ANGELUS, SC_IMPOSITIO, SC_SUFFRAGIUM
- Debuffs: SC_DEC_AGI, SC_SIGNUMCRUCIS, SC_AETERNA, SC_ORCISH
- Special: SC_HIDING, SC_CLOAKING, SC_CARTBOOST, SC_GLORIA, SC_MAGNIFICAT
- Flags: SCSTART_NOAVOID, SCSTART_NOTICKDEF, SCSTART_NORATEDEF

**Item Bonuses:**
- Stat Bonuses: bStr, bAgi, bVit, bInt, bDex, bLuk, bMaxHP, bMaxSP, bAtk, bMatk
- Damage Modifiers: bAddRace, bAddEle, bAddSize, bAddRace2, bCriticalAddRace
- Resistance: bSubRace, bSubEle, bSubSize, bResEff, bMagicDamageReturn
- Special Effects: bAutoSpell, bHPDrainRate, bSPDrainRate, bAddItemHealRate, bCastrate
- Constants: RC_Formless, RC_Undead, RC_Brute, RC_Plant, RC_Insect, RC_Fish, RC_Demon, RC_DemiHuman, RC_Angel, RC_Dragon
- Elements: Ele_Neutral, Ele_Water, Ele_Earth, Ele_Fire, Ele_Wind, Ele_Poison, Ele_Holy, Ele_Dark, Ele_Ghost, Ele_Undead
- Sizes: Size_Small, Size_Medium, Size_Large
- Battle Flags: BF_SHORT, BF_LONG, BF_MAGIC, BF_WEAPON

**Job System:**
- Base Jobs: EAJ_NOVICE, EAJ_SWORDMAN, EAJ_MAGE, EAJ_ARCHER, EAJ_ACOLYTE, EAJ_MERCHANT, EAJ_THIEF
- Extended: EAJ_TAEKWON, EAJ_GUNSLINGER, EAJ_NINJA, EAJ_SUMMONER
- Branches: EAJL_2_1 (first path), EAJL_2_2 (second path)
- Types: EAJL_UPPER (transcendent), EAJL_BABY, EAJL_THIRD, EAJL_FOURTH
- Masks: EAJ_BASEMASK, EAJ_UPPERMASK, EAJ_THIRDMASK, EAJ_FOURTHMASK
- Functions: eaclass(jobid), roclass(eajobid{, sex})

**Mapflags:**
- Restrictions: noteleport, nowarp, nowarpto, noreturn, nomemo, nosave, nobranch, nopenalty
- Battle: pvp, pvp_noparty, pvp_noguild, gvg, battleground, skill_damage, skill_duration
- Effects: nightenabled, clouds, clouds2, fog, fireworks, sakura, leaves, rain, snow
- Misc: bexp, jexp, town, loadevent, autotrade, allowks, monster_noteleport

**Always Combine With:**
- 02_SCRIPTING_COMPLETE.md for command syntax (sc_start, bonus, jobchange, setmapflag)
- 04_CONTENT_CREATION.md for practical applications
- 07_BATTLE_STATUS.md for how constants affect calculations

**Example Queries:**
```
Query: "What does SC_BLESSING do?"
Load: 03_GAME_MECHANICS.md (Part 1: SC_BLESSING section)
Result: val1 = skill level, +val1 STR/INT/DEX, duration formula

Query: "Create item +20% vs Demons"
Load: 03_GAME_MECHANICS.md (bAddRace + RC_Demon)
Then: 02_SCRIPTING_COMPLETE.md (bonus syntax)
Result: bonus bAddRace, RC_Demon, 20;

Query: "Check if 2nd class job"
Load: 03_GAME_MECHANICS.md (EAJL_2 mask + eaclass)
Result: if ((eaclass(Class) & EAJL_2) && !(eaclass(Class) & EAJL_UPPER))
```

---

### 04_CONTENT_CREATION.md (5,060 lines | 120KB)

**Merged From:** ItemGroups (1,219) + QuestSystem (648) + NPCScriptingPatterns (2,972)

**Contains:**
- **Part 1:** Item Groups - item_group_db.yml, Algorithm types, SubGroups, probability
- **Part 2:** Quest System - quest_db.yml, TimeLimit formats, Targets, Drops
- **Part 3:** NPC Patterns - 12 production-ready patterns (state machines, cooldowns, etc.)

**Query Triggers:**
```
"gacha", "random box", "item group", "IG_*", "getgroupitem",
"quest", "quest_db", "setquest", "TimeLimit", "weekly quest",
"NPC pattern", "state machine", "cooldown", "instance", "anti-cheat"
```

**Topics Covered:**

**Item Groups:**
- Database structure (item_group_db.yml YAML)
- Algorithm types: Random, All, SharedPool
- SubGroup system (0 = must items, 1-99 = random pools)
- Special fields: Rate, Amount, Announced, Bound, Named, Duration, Refine, RandomOptions
- Probability calculations
- Complete gacha examples (simple, advanced, multi-pool)

**Quest System:**
- Database structure (quest_db.yml YAML)
- Basic fields: Id, Title, MinLevel, MaxLevel, Location
- TimeLimit formats: Relative ("+1h", "+30m", "+1d") vs Absolute ("Monday 4h", "Tuesday 18h30m")
- Target methods: Simple (Mob + Count) vs Advanced (Race, Size, Element, MinLevel, MaxLevel)
- Drop configuration: Mob, Item, Count, Rate
- Complete quest examples (kill, timed, weekly, race-based, multi-target)

**NPC Patterns (12 Production-Ready):**
1. State Machines - Complex NPC conversation flows
2. Cooldown Systems - Time-based restrictions
3. Instance Management - Custom instance handling
4. Anti-Cheat Patterns - Exploit prevention
5. Currency Systems - Custom currency management
6. Ranking/Leaderboard - Competitive systems
7. Event Management - Timed events
8. Multi-Stage Quests - Complex quest chains
9. Conditional Rewards - Dynamic reward systems
10. Dynamic Difficulty - Scaling challenges
11. Persistent Player Data - Save/load systems
12. Shop Systems - Custom shops

**Always Combine With:**
- 02_SCRIPTING_COMPLETE.md for command syntax
- 03_GAME_MECHANICS.md for constants (if using Race, Element, status effects, bonuses)

**Example Queries:**
```
Query: "Create gacha with announced rare drops"
Load: 04_CONTENT_CREATION.md (Part 1: Algorithm + Announced)
Then: 02_SCRIPTING_COMPLETE.md (getgroupitem)

Query: "Weekly quest reset Monday"
Load: 04_CONTENT_CREATION.md (Part 2: TimeLimit absolute)
Then: 02_SCRIPTING_COMPLETE.md (setquest, checkquest)

Query: "NPC cooldown system"
Load: 04_CONTENT_CREATION.md (Part 3: Pattern 2)
Then: 02_SCRIPTING_COMPLETE.md (command reference)
```

---

### 05_SOURCE_DEVELOPMENT.md (6,054 lines | 162KB)

**Merged From:** PluginSystem (1,753) + BestPractices (1,631) + MemoryCrash (737) + SourceStructure (1,871)

**Contains:**
- **Part 1:** Plugin System - src/custom/, ACMD_FUNC, BUILDIN_FUNC, custom defines
- **Part 2:** Best Practices - Code quality, safety patterns, naming conventions
- **Part 3:** Memory Crash Patterns - ERS, map_freeblock, bl->prev, 25+ crash patterns
- **Part 4:** Source Code Structure - Directory layout, core structs, file responsibilities

**Query Triggers:**
```
"ACMD_FUNC", "custom @command", "@go", "src/custom",
"BUILDIN_FUNC", "custom script command",
"crash", "segfault", "nullpo", "bl->prev", "ERS", "map_freeblock",
"best practices", "code quality", "naming convention",
"src/map/", "src/char/", "directory structure", "core structs"
```

**Topics Covered:**

**Plugin System (src/custom/):**
- Directory structure: atcommand.inc, atcommand_def.inc, script.inc, script_def.inc
- ACMD_FUNC macro: Custom @command implementation
- BUILDIN_FUNC macro: Custom script command implementation
- Custom defines: defines_pre.hpp, defines_post.hpp
- Custom battle config: battle_config_init.inc, battle_config_struct.inc
- 50+ working examples
- 8 common mistakes documented

**Best Practices:**
- K&R braces, naming conventions
- Safety patterns: null checks (nullpo_ret, nullpo_retr), bounds checking
- Memory management: aMalloc/aFree, ERS usage
- Common mistakes: skill indexing, integer overflow, buffer overflow
- Code organization and modularity

**Memory Crash Patterns (80% of crashes):**
- ERS (Entry Reusage System): Object pooling, use-after-free prevention
- Map block system: Deferred deletion, map_freeblock_lock/unlock
- Critical bl->prev check: Prevents 80% of segfaults
- String ownership: script_pushstr vs script_pushconststr
- Timer data validation
- 25+ complete crash patterns with fixes

**Source Code Structure:**
- Directory layout: src/map/, src/char/, src/login/, src/common/
- Core structs: map_session_data, mob_data, item_data, skill_data, status_data
- File responsibilities: pc.cpp, mob.cpp, skill.cpp, battle.cpp, clif.cpp, script.cpp
- CMake build system

**Always Combine With:**
- 09_SECURITY_GUIDE.md for security checks
- 06_DATABASE_SYSTEMS.md for compilation/debugging
- 10_SOURCE_REFERENCE.md for expert tutorials

**Example Queries:**
```
Query: "Add custom @command safely"
Load: 05_SOURCE_DEVELOPMENT.md (Part 1: ACMD_FUNC)
Then: 09_SECURITY_GUIDE.md (security checks)

Query: "Fix segmentation fault"
Load: 05_SOURCE_DEVELOPMENT.md (Part 3: Memory patterns)
Focus: bl->prev check, ERS usage

Query: "Understanding codebase structure"
Load: 05_SOURCE_DEVELOPMENT.md (Part 4: Source structure)
Then: 10_SOURCE_REFERENCE.md (expert details)
```

---

### 06_DATABASE_SYSTEMS.md (7,104 lines | 172KB)

**Merged From:** DatabaseCPP (2,417) + PacketStructure (1,959) + CompilationDebugging (2,675)

**Contains:**
- **Part 1:** Database C++ - item_db.find(), mob_db.find(), YAML parsing, SQL
- **Part 2:** Packet Structure - CZ_*, ZC_*, clif.cpp, WFIFO/RFIF, custom packets
- **Part 3:** Compilation & Debugging - CMake, GDB, Valgrind, AddressSanitizer

**Query Triggers:**
```
"database", "item_db.find", "mob_db", "YAML parsing", "SQL query",
"packet", "CZ_", "ZC_", "clif_", "WFIFO", "RFIF", "custom packet",
"compile", "cmake", "build error", "GDB", "Valgrind", "debug"
```

**Topics Covered:**

**Database C++ Internals:**
- Database lookups: item_db.find(), mob_db.find(), skill_db.find()
- YAML parsing: parseBodyNode, loadingTable, defaulting
- Adding custom database fields
- SQL operations: Sql_Query, Sql_NextRow, Sql_GetData
- Prepared statements for security
- Database safety patterns

**Packet Structure:**
- Packet naming: CZ_* (client→zone), ZC_* (zone→client), HC_*, CH_*
- clif.cpp structure and organization
- WFIFO/RFIF macros: WFIFOW, WFIFOL, WFIFOB, RFIFOW, RFIFOL, RFIFOB
- Packet creation 7-step guide
- PACKETVER handling
- Custom packet examples

**Compilation & Debugging:**
- Build systems: CMake, configure, Visual Studio
- Compilation flags and options
- GDB debugging: bt (backtrace), break, watch, print, continue
- Valgrind memory checking
- AddressSanitizer usage
- Common compilation errors and fixes
- Performance profiling

**Always Combine With:**
- 05_SOURCE_DEVELOPMENT.md for safety patterns
- 10_SOURCE_REFERENCE.md for advanced usage

**Example Queries:**
```
Query: "How to use item_db.find()?"
Load: 06_DATABASE_SYSTEMS.md (Part 1: Database section)

Query: "Create custom packet"
Load: 06_DATABASE_SYSTEMS.md (Part 2: Packet structure)
Then: 05_SOURCE_DEVELOPMENT.md (safety patterns)

Query: "Fix compilation error"
Load: 06_DATABASE_SYSTEMS.md (Part 3: Compilation)
```

---

### 07_BATTLE_STATUS.md (877 lines | 23KB)

**Standalone File:** KB_REF_BattleStatusInternals.md (too complex to merge)

**Contains:**
- Status data structure (base vs final stats)
- Stat calculation pipeline (equipment → base → SC → final)
- Battle damage calculation flow (2000+ line flow explained)
- Element system and modifier tables
- Status change lifecycle
- ATK/MATK/HIT/FLEE/DEF formulas
- Race/Size/Element modifier stacking rules
- Base ATK vs Weapon ATK
- Hard DEF (%) vs Soft DEF (flat)
- Element level effects (1-4)

**Query Triggers:**
```
"damage calculation", "battle", "damage formula", "ATK", "MATK", "DEF",
"element table", "status_calc", "status_data", "battle_calc",
"why is damage", "how to calculate"
```

**Topics Covered:**
- struct status_data (all fields explained)
- status_calc_pc(), status_calc_mob() flow
- battle_calc_weapon_attack() 2000+ line breakdown
- Element modifier table (20x element grid)
- Size modifier table (weapon type vs monster size)
- Race/Element/Size modifier stacking order
- Critical damage calculations
- Skill damage formulas
- Defense reduction formulas

**Always Combine With:**
- 03_GAME_MECHANICS.md for constants (RC_*, Ele_*, Size_*)
- 10_SOURCE_REFERENCE.md for battle.cpp source reference

**Example Queries:**
```
Query: "How is ATK calculated?"
Load: 07_BATTLE_STATUS.md (ATK formula section)

Query: "Element modifier table"
Load: 07_BATTLE_STATUS.md (element system)

Query: "Why is my damage wrong?"
Load: 07_BATTLE_STATUS.md (damage calc flow)
Then: 03_GAME_MECHANICS.md (verify constants used)
```

---

### 08_SCRIPT_INTERNALS.md (844 lines | 20KB)

**Standalone File:** KB_REF_ScriptTimerInternals.md (critical internals)

**Contains:**
- Script execution engine (run_script_main internals)
- Stack management (parameter handling)
- Timer system (binary heap implementation)
- DIFF_TICK macro (wraparound handling)
- Sleep vs sleep2 (RID invalidation)
- Freeloop protection (when safe to disable)
- Script state lifecycle
- 15+ critical crash patterns with fixes

**Query Triggers:**
```
"script_state", "script engine", "timer", "binary heap",
"freeloop", "sleep", "sleep2", "RERUNLINE", "DIFF_TICK",
"script crash", "timer not working", "RID invalid"
```

**Topics Covered:**
- struct script_state (all fields explained)
- run_script_main() execution flow
- Stack operations: script_pushint, script_pushstr, script_getnum, script_getstr
- Binary heap timer implementation
- Timer wraparound handling (DIFF_TICK)
- RID validation after sleep/timer
- Freeloop safe usage patterns
- Script memory leaks
- 15+ crash patterns: Invalid RID, stack corruption, timer data validation, infinite loops

**Always Combine With:**
- 02_SCRIPTING_COMPLETE.md for script command context
- 05_SOURCE_DEVELOPMENT.md for C++ fixes

**Example Queries:**
```
Query: "Why does my script crash after sleep?"
Load: 08_SCRIPT_INTERNALS.md (RID invalidation pattern)

Query: "How does timer system work?"
Load: 08_SCRIPT_INTERNALS.md (binary heap section)

Query: "When is freeloop safe?"
Load: 08_SCRIPT_INTERNALS.md (freeloop protection)
```

---

### 09_SECURITY_GUIDE.md (1,811 lines | 46KB)

**Standalone File:** KB_REF_SecurityExploits.md (critical security)

**Contains:**
- 15 exploit types documented with prevention
- Prevention code for each exploit
- Input validation patterns
- Security audit checklist
- Real-world exploit examples

**Query Triggers:**
```
"security", "exploit", "hack", "vulnerability",
"item dupe", "stat manipulation", "packet injection", "SQL injection",
"prevent", "validation", "security check"
```

**Topics Covered:**

**15 Exploit Types:**
1. Item Duplication - Prevention patterns
2. Stat Manipulation - Validation checks
3. Packet Injection - Packet validation
4. SQL Injection - Prepared statements
5. Integer Overflow - Safe arithmetic
6. Race Conditions - Lock patterns
7. Command Injection - Input sanitization
8. XSS in Custom Pages - Output escaping
9. Directory Traversal - Path validation
10. Authentication Bypass - Session checks
11. Item ID Manipulation - Range validation
12. GM Command Abuse - Permission checks
13. Skill ID Manipulation - Skill validation
14. Map Server Exploits - Server-side validation
15. Client Modification Detection - Integrity checks

**Prevention Patterns:**
- Input validation (range, type, format)
- Prepared SQL statements
- Packet integrity checks
- Session validation
- Rate limiting
- Server-side authority
- Safe string handling
- Integer overflow checks

**Always Combine With:**
- 05_SOURCE_DEVELOPMENT.md for implementation
- 06_DATABASE_SYSTEMS.md for database security

**Example Queries:**
```
Query: "Prevent item duplication"
Load: 09_SECURITY_GUIDE.md (Exploit Type 1)

Query: "SQL injection prevention"
Load: 09_SECURITY_GUIDE.md (Exploit Type 4)
Then: 06_DATABASE_SYSTEMS.md (prepared statements)

Query: "Security checklist for custom @command"
Load: 09_SECURITY_GUIDE.md (checklist + relevant exploits)
Then: 05_SOURCE_DEVELOPMENT.md (ACMD_FUNC implementation)
```

---

### 10_SOURCE_REFERENCE.md (35,014 lines | 1.4MB)

**Complete Reference:** Rathena_Source_Data_v2.md with v4.0 header

**Contains:**
- 420+ tutorial sections (beginner to expert)
- Source modification guides (step-by-step with source code)
- Server setup (advanced configuration)
- Client integration (GRF, packets, PACKETVER)
- Database tutorials (advanced item_db, mob_db, skill_db)
- Custom content creation (maps, items, skills, monsters)
- 100+ advanced NPC script examples

**Query Triggers:**
```
"tutorial", "advanced", "src/map/", "src/char/", "clif_", "pc_",
"how to modify", "step by step", "advanced tutorial",
"expert", "source reference"
```

**Topics Covered:**

**Server Setup (15%):**
- Installation (Windows, Linux, FreeBSD)
- MySQL/MariaDB setup and optimization
- Configuration files: login_athena.conf, char_athena.conf, map_athena.conf
- GRF setup, clientinfo, data folder
- Network configuration
- Server optimization

**Source Modifications (20%):**
- Adding custom mapflags (complete guide)
- Creating @commands (step-by-step)
- Custom constants and defines
- Skill modifications
- Item script modifications
- Monster AI modifications

**Client Integration (10%):**
- GRF file structure and creation
- Packet version (PACKETVER) handling
- Client/server protocol
- Custom textures and sprites
- Custom UI elements

**Database Tutorials (15%):**
- item_db.yml structure (complete)
- mob_db.yml structure (complete)
- skill_db.yml structure (complete)
- Adding custom items/mobs/skills
- Database relationships

**Custom Content (15%):**
- Custom maps (mapcache, map_index)
- Custom items with scripts
- Custom skills with source code
- Custom monsters with AI
- Custom instances

**Script Examples (35%):**
- 100+ NPC script examples
- Event scripts (holiday, PvP, etc.)
- Instance examples (advanced)
- Battleground examples (advanced)
- Complex NPC systems

**Always Combine With:**
- 05_SOURCE_DEVELOPMENT.md for safety patterns
- 06_DATABASE_SYSTEMS.md for compilation
- 09_SECURITY_GUIDE.md for security

**Example Queries:**
```
Query: "Tutorial for adding custom mapflag"
Load: 10_SOURCE_REFERENCE.md (mapflag tutorial)
Then: 05_SOURCE_DEVELOPMENT.md (if using src/custom/)

Query: "Advanced instance example"
Load: 10_SOURCE_REFERENCE.md (instance section)
Then: 02_SCRIPTING_COMPLETE.md (command reference)

Query: "Complete guide to PACKETVER"
Load: 10_SOURCE_REFERENCE.md (client integration)
Then: 06_DATABASE_SYSTEMS.md (packet structure)
```

---

<!-- RAG_CHUNK: loading_strategies -->
## Loading Strategies by Query Type

### Single-File Queries (Load 1 file - 80% of queries)

```
Query: "What does mes command do?"
→ Load: 02_SCRIPTING_COMPLETE.md

Query: "What is SC_BLESSING?"
→ Load: 03_GAME_MECHANICS.md

Query: "How to use item_db.find()?"
→ Load: 06_DATABASE_SYSTEMS.md

Query: "Prevent SQL injection"
→ Load: 09_SECURITY_GUIDE.md
```

### Two-File Queries (Load 2 files - 15% of queries)

```
Query: "How to apply blessing status?"
→ Load: 02_SCRIPTING_COMPLETE.md (sc_start syntax)
→ Then: 03_GAME_MECHANICS.md (SC_BLESSING parameters)

Query: "Create item with bonus vs demons"
→ Load: 03_GAME_MECHANICS.md (bAddRace + RC_Demon)
→ Then: 02_SCRIPTING_COMPLETE.md (bonus syntax)

Query: "Add custom @command safely"
→ Load: 05_SOURCE_DEVELOPMENT.md (ACMD_FUNC)
→ Then: 09_SECURITY_GUIDE.md (security checks)
```

### Multi-File Queries (Load 3+ files - 5% of queries)

```
Query: "Complete quest system with rewards"
→ Load: 04_CONTENT_CREATION.md (quest_db structure)
→ Then: 02_SCRIPTING_COMPLETE.md (setquest, checkquest)
→ Then: 03_GAME_MECHANICS.md (if using Race/Element filters)

Query: "Debug script crash in timer"
→ Load: 08_SCRIPT_INTERNALS.md (timer internals)
→ Then: 05_SOURCE_DEVELOPMENT.md (crash patterns)
→ Then: 02_SCRIPTING_COMPLETE.md (command reference)
```

---

<!-- RAG_CHUNK: keyword_index -->
## Keyword Index (Fast Lookup)

### Commands & Functions
- **mes, next, close** → 02_SCRIPTING
- **getitem, delitem** → 02_SCRIPTING
- **setquest, checkquest** → 02_SCRIPTING + 04_CONTENT
- **sc_start, sc_end** → 02_SCRIPTING + 03_GAME_MECHANICS
- **bonus, bonus2** → 02_SCRIPTING + 03_GAME_MECHANICS
- **warp, areawarp** → 02_SCRIPTING
- **monster, areamonster** → 02_SCRIPTING
- **setmapflag, removemapflag** → 02_SCRIPTING + 03_GAME_MECHANICS
- **jobchange, eaclass** → 02_SCRIPTING + 03_GAME_MECHANICS
- **getgroupitem** → 02_SCRIPTING + 04_CONTENT

### Constants
- **SC_*** (status) → 03_GAME_MECHANICS (Part 1)
- **bonus types** (bStr, bAtk, etc.) → 03_GAME_MECHANICS (Part 2)
- **RC_*** (race) → 03_GAME_MECHANICS (Part 2)
- **Ele_*** (element) → 03_GAME_MECHANICS (Part 2)
- **Size_*** (size) → 03_GAME_MECHANICS (Part 2)
- **EAJ_***, **EAJL_*** (job) → 03_GAME_MECHANICS (Part 3)
- **mf_*** (mapflag) → 03_GAME_MECHANICS (Part 4)

### C++ Development
- **ACMD_FUNC** → 05_SOURCE + 02_SCRIPTING (Part 2)
- **BUILDIN_FUNC** → 05_SOURCE + 02_SCRIPTING (Part 2)
- **src/custom/** → 05_SOURCE
- **nullpo, bl->prev** → 05_SOURCE (Part 3)
- **ERS, map_freeblock** → 05_SOURCE (Part 3)
- **item_db.find()** → 06_DATABASE
- **clif_***, **WFIFO** → 06_DATABASE
- **cmake, GDB** → 06_DATABASE

### Systems & Internals
- **quest_db** → 04_CONTENT (Part 2)
- **item_group_db** → 04_CONTENT (Part 1)
- **status_calc, battle_calc** → 07_BATTLE_STATUS
- **script_state, timer** → 08_SCRIPT_INTERNALS
- **exploit, security** → 09_SECURITY

---

<!-- RAG_CHUNK: best_practices -->
## RAG Best Practices

### Always Start With
```
EVERY query: Load 01_MASTER_INDEX.md first
→ Provides context and determines next files
```

### Progressive Loading
```
Start with primary file
→ Check if complete
→ Load secondary files only if needed
→ Follow cross-references in files
```

### Context Window Optimization
```
Small query (1-2K context):
  → Load 1 file (relevant section)

Medium query (5-10K context):
  → Load 2 files (primary + secondary)

Large query (20K+ context):
  → Load 3+ files (complete topic coverage)
```

### File Combination Rules
```
Script commands + Constants:
  02_SCRIPTING + 03_GAME_MECHANICS

Content creation + Implementation:
  04_CONTENT + 02_SCRIPTING + 03_GAME_MECHANICS

Source development + Security:
  05_SOURCE + 09_SECURITY + 06_DATABASE

Debugging + Internals:
  05_SOURCE + 08_SCRIPT_INTERNALS + 02_SCRIPTING
```

### Cross-Reference Following
```
Files contain smart cross-references:
  "See 03_GAME_MECHANICS.md for SC_* constants"
  "See 05_SOURCE_DEVELOPMENT.md for safety patterns"

AI should:
  1. Parse cross-references
  2. Load referenced sections
  3. Provide complete answers
```

---

## File Size Reference (for context planning)

| File | Lines | Size | Load Time | Context Priority |
|------|-------|------|-----------|------------------|
| 01_MASTER_INDEX | 1,064 | 38KB | Fast | Always first |
| 02_SCRIPTING_COMPLETE | 16,054 | 461KB | Slow | High (50% queries) |
| 03_GAME_MECHANICS | 3,685 | 79KB | Medium | High (40% queries) |
| 04_CONTENT_CREATION | 5,060 | 120KB | Medium | Medium (20% queries) |
| 05_SOURCE_DEVELOPMENT | 6,054 | 162KB | Medium | Medium (15% queries) |
| 06_DATABASE_SYSTEMS | 7,104 | 172KB | Slow | Low (10% queries) |
| 07_BATTLE_STATUS | 877 | 23KB | Fast | Low (5% queries) |
| 08_SCRIPT_INTERNALS | 844 | 20KB | Fast | Low (5% queries) |
| 09_SECURITY | 1,811 | 46KB | Fast | Medium (15% queries) |
| 10_SOURCE_REFERENCE | 35,014 | 1.4MB | Very Slow | Low (10% queries) |

**Recommendation:** Prioritize loading smaller, high-frequency files first.

---

**End of RAG Quick Reference | v4.0 | 2025-11-19**
