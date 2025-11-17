# CRITICAL: Missing Source Code KB Files

## ❌ **Current Gap: 0% Source Code Coverage**

The current KB (21 files, 85% coverage) focuses on **scripting, database, and configuration**.

**For C++ source modifications, you need 8 additional KB files that DON'T EXIST YET.**

---

## 🚀 **8 Essential Source Code KB Files (MISSING)**

### **Priority 1: CRITICAL (Create These First)**

#### 1. KB_REF_SourceCodeStructure.md (25KB)
```
PURPOSE: Understand rAthena C++ codebase layout
COVERS:
- Directory structure (src/map/, src/char/, src/login/, src/common/)
- Key files and their purposes:
  * pc.cpp/hpp - Player character functions
  * mob.cpp/hpp - Monster functions
  * skill.cpp/hpp - Skill mechanics
  * itemdb.cpp/hpp - Item database
  * battle.cpp/hpp - Combat calculations
  * script.cpp/hpp - Script engine
  * clif.cpp/hpp - Client-server packets
  * atcommand.cpp/hpp - GM commands
  * map.cpp/hpp - Map server core
- Class hierarchies (map_session_data, mob_data, etc.)
- Build system (CMake, Visual Studio)
- Dependencies and libraries

ERROR FREE: Prevents editing wrong files, understanding code flow
EXPERT LEVEL: Know exactly where to make changes
```

#### 2. KB_REF_ScriptCommandCreation.md (15KB)
```
PURPOSE: Create custom script commands (most common modification)
COVERS:
- BUILDIN() macro usage
- Function signature patterns
- Parameter handling:
  * script_hasdata() - Check if parameter exists
  * script_getnum() - Get integer parameter
  * script_getstr() - Get string parameter
  * script_getdata() - Get variable reference
  * script_rid2sd() - Get character data
- Return values:
  * script_pushint() - Return integer
  * script_pushstr() - Return string
  * script_pushconststr() - Return constant string
- Registration in script.cpp
- Complete working examples:
  * Custom getitem2 variant
  * Custom damage calculation
  * Custom status effect
- Common errors and fixes
- Thread safety considerations

ERROR FREE: Correct parameter handling, no crashes
EXPERT LEVEL: Create any custom command safely
```

#### 3. KB_REF_PluginSystem.md (20KB)
```
PURPOSE: Use plugins instead of core modifications (safer approach)
COVERS:
- HPM (Hercules Plugin Manager) system
- Plugin vs core modification (when to use which)
- Plugin structure and skeleton
- Available hooks (200+ hook points):
  * PC hooks (login, logout, levelup, death)
  * Combat hooks (pre-damage, post-damage)
  * Item hooks (use, equip, bonus)
  * Skill hooks (cast, use, damage)
  * Map hooks (map load, cell check)
  * NPC hooks (script execution)
- Hook usage patterns
- Plugin data storage
- Complete plugin examples:
  * Custom script commands plugin
  * Custom item bonus plugin
  * Event logging plugin
- Plugin compilation and loading
- Debugging plugins
- When plugins can't be used (core changes needed)

ERROR FREE: Isolate modifications, easier debugging
EXPERT LEVEL: Modify without touching core (update-safe)
```

---

### **Priority 2: HIGH (Create Next)**

#### 4. KB_REF_DatabaseCPP.md (18KB)
```
PURPOSE: Work with databases in C++ code
COVERS:
- itemdb.cpp structure:
  * item_data class
  * itemdb_exists()
  * itemdb_search()
  * itemdb_type()
  * Adding custom item fields
- mobdb.cpp structure:
  * mob_db class
  * mob_once_spawn()
  * mob_parse_dataset()
  * Adding custom monster fields
- skilldb.cpp structure:
  * skill_get_*() functions
  * Adding custom skill fields
- Database reload mechanisms
- Memory management (new/delete patterns)
- Reading YAML databases from C++
- Adding new databases
- Database caching and optimization

ERROR FREE: Proper memory handling, no leaks
EXPERT LEVEL: Extend database systems
```

#### 5. KB_REF_CompilationDebugging.md (15KB)
```
PURPOSE: Fix compilation errors and debug runtime issues
COVERS:
- Common compilation errors:
  * "undefined reference" - Linking errors
  * "undeclared identifier" - Missing includes
  * "no matching function" - Wrong parameters
  * Template errors
  * Platform-specific errors (Windows vs Linux)
- CMake configuration
- Dependency issues
- Debugging tools:
  * GDB (Linux) - Breakpoints, backtraces, watchpoints
  * Visual Studio Debugger (Windows)
  * LLDB (Mac)
- Logging:
  * ShowInfo(), ShowWarning(), ShowError(), ShowDebug()
  * ShowSQL(), ShowStatus()
  * Debug level configuration
- Memory debugging:
  * Valgrind (memory leaks)
  * AddressSanitizer
  * Memory profiling
- Performance profiling:
  * gprof, perf, VTune
- Crash dump analysis
- Common runtime errors and fixes

ERROR FREE: Quickly fix compilation/runtime errors
EXPERT LEVEL: Debug complex issues efficiently
```

---

### **Priority 3: MEDIUM (Create After)**

#### 6. KB_REF_PacketStructure.md (20KB)
```
PURPOSE: Modify client-server communication
COVERS:
- Packet structure basics
- packet_db.txt format
- clif.cpp functions:
  * clif->send() - Send packet to client
  * clif->parse*() - Parse client packets
  * WFIFOHEAD(), WFIFOW(), WFIFOL() - Write to buffer
  * RFIFOB(), RFIFOW(), RFIFOL() - Read from buffer
- Adding custom packets:
  * Packet ID selection
  * Packet structure definition
  * Handler registration
  * Client-side counterpart
- Security considerations:
  * Packet validation
  * Buffer overflow prevention
  * Packet encryption
- Common packet modifications:
  * Custom UI elements
  * Custom item display
  * Custom skill effects
- Debugging packets (Wireshark, packet logger)

ERROR FREE: Prevent crashes, security issues
EXPERT LEVEL: Create custom client features
```

#### 7. KB_REF_CommonSrcModifications.md (20KB)
```
PURPOSE: Step-by-step guides for common modifications
COVERS:
- Custom item bonuses:
  * Adding bonus enum
  * Parsing bonus in pc.cpp
  * Applying bonus effect
- Custom status effects:
  * Adding SC_ constant
  * Status icon
  * Effect logic in status.cpp
  * Cure/cleanse handling
- Skill modifications:
  * Skill damage formulas
  * Skill effects
  * Skill cast conditions
- Damage formula changes:
  * battle.cpp modifications
  * Custom damage types
  * Elemental modifiers
- Custom monster AI:
  * AI types in mob.cpp
  * Custom AI functions
  * Targeting logic
- Map server modifications:
  * Custom map properties
  * Map event triggers
  * Zone systems
- Character modifications:
  * Custom stats
  * Custom job mechanics
  * Character save/load

ERROR FREE: Step-by-step prevents mistakes
EXPERT LEVEL: Implement complex features
```

#### 8. KB_REF_SourceCodeBestPractices.md (12KB)
```
PURPOSE: Write clean, maintainable source modifications
COVERS:
- rAthena code style:
  * Naming conventions
  * Indentation and formatting
  * Comment standards
- Error handling patterns:
  * nullpo checks (nullpo_ret, nullpo_retr)
  * Return codes
  * Error messages
- Memory safety:
  * RAII patterns
  * Smart pointers vs raw pointers
  * Memory leak prevention
- Thread safety:
  * Mutex usage
  * Atomic operations
  * Thread-safe patterns
- Performance considerations:
  * Cache-friendly code
  * Loop optimization
  * Database query optimization
- Testing modifications:
  * Unit testing
  * Integration testing
  * Stress testing
- Version control:
  * Git branching for mods
  * Patch management
  * Merging upstream updates
- Documentation:
  * Code comments
  * Change logs
  * User documentation

ERROR FREE: Follow best practices, avoid pitfalls
EXPERT LEVEL: Professional-grade modifications
```

---

## 📊 **Impact of Creating Source KB Files**

### **Before (Current):**
```
Scripting: ✅ 85% coverage (21 files, 388KB)
Source Code: ❌ 0% coverage (0 files)

Can do: Scripts, configs, databases (YAML)
Can't do: C++ modifications (blind trial-and-error)
```

### **After (With 8 Source KB Files):**
```
Scripting: ✅ 85% coverage (21 files, 388KB)
Source Code: ✅ 90% coverage (8 files, 145KB)
TOTAL: ✅ 88% coverage (29 files, 533KB)

Can do: Everything from scripts to core C++ modifications
Expertise: Error-free, expert-level source modifications
```

---

## 🎯 **Quick Decision Matrix**

### **When to Use Current KB (Scripting):**
- ✅ Creating NPCs
- ✅ Writing quests
- ✅ Building instances/dungeons
- ✅ Configuring server
- ✅ Modifying databases (YAML)
- ✅ Item groups, monster AI (data only)

**Load**: KB_REF_ScriptCommands.md + KB_REF_Constants.md + task-specific KB

### **When You Need Source KB (C++):**
- ❌ Custom script commands (needs KB_REF_ScriptCommandCreation.md)
- ❌ Custom item bonuses (needs KB_REF_CommonSrcModifications.md)
- ❌ Custom status effects (needs KB_REF_CommonSrcModifications.md)
- ❌ Packet modifications (needs KB_REF_PacketStructure.md)
- ❌ Core damage formulas (needs KB_REF_DatabaseCPP.md)
- ❌ Plugins (needs KB_REF_PluginSystem.md)

**Load**: All 8 source KB files (once created)

---

## 💬 **Tell Me What to Create**

I can create these 8 KB files RIGHT NOW. Which priority level?

**Option A: All 8 files** (~145KB total, comprehensive coverage)
**Option B: Priority 1 only** (3 files, ~60KB, most critical)
**Option C: Priority 1 + 2** (5 files, ~93KB, covers 80% of needs)
**Option D: Custom selection** (tell me which specific files you need most)

**Also tell me:**
1. What source modifications do you make most?
2. What's your C++ experience level?
3. Any specific features you want to add?

Then I'll create exactly what you need! 🚀
