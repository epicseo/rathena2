# KB Loading Guide for Expert Development

## 🎯 **For Scripting & Instance Development (Current KB)**

### **Essential KB Files to Load**

#### **Tier 1: ALWAYS Load (Critical)**
```markdown
1. KB_REF_Constants.md (14KB)
   - Required for ALL scripting tasks
   - EQP_*, RC_*, Ele_*, Size_*, Job_* constants
   - Without this: AI will invent wrong constant names

2. KB_REF_ScriptCommands.md (21KB)
   - 100+ core commands with exact syntax
   - Basic NPC structure, variables, operators
   - Without this: Incorrect command syntax
```

#### **Tier 2: Task-Specific (High Priority)**

**For NPC Scripting:**
```markdown
Load:
- KB_REF_ScriptCommands.md (21KB) - Core commands
- KB_REF_Constants.md (14KB) - Constants
- KB_REF_NPCExamples.md (16KB) - Working templates

Optional:
- KB_REF_FAQ.md (13KB) - Troubleshooting
```

**For Instance/Memorial Dungeons:**
```markdown
Load:
- KB_REF_InstanceSystem.md (32KB) - Complete instance mechanics
- KB_REF_ScriptCommandsExpanded.md (20KB) - Advanced commands
- KB_REF_Constants.md (14KB) - Constants

Optional:
- KB_REF_MobModesAI.md (15KB) - Boss mechanics
- INSTANCE_EVENT_FIX.md (12KB) - Avoid OnPC* event pitfalls
```

**For Advanced Scripting (SQL, Optimization, Dynamic Systems):**
```markdown
Load:
- KB_REF_AdvancedScripting.md (34KB) - Expert patterns
- KB_REF_ScriptCommandsExpanded.md (20KB) - Advanced commands
- KB_REF_InstanceSystem.md (32KB) - Complex systems

Optional:
- KB_REF_ItemGroups.md (27KB) - Reward systems
```

**For Database Work:**
```markdown
Load:
- KB_REF_DatabaseStructure.md (21KB) - YAML structures
- KB_REF_ItemBonuses.md (15KB) - Item bonuses
- KB_REF_MobModesAI.md (15KB) - Monster AI

Optional:
- KB_REF_SkillSystem.md (21KB) - Skills
- KB_REF_ItemGroups.md (27KB) - Item groups
```

#### **Tier 3: Reference Only (Load as Needed)**
```markdown
- KB_REF_StatusEffects.md (14KB) - Status effects reference
- KB_REF_VisualEffects.md (13KB) - Visual effects
- KB_REF_QuestSystem.md (13KB) - Quest database
- KB_REF_JobSystem.md (16KB) - Job mechanics
- KB_REF_MapFlags.md (27KB) - Map properties
- KB_REF_AtCommands.md (23KB) - GM commands
- KB_REF_BattleConfig.md (15KB) - Battle config
- KB_REF_ConfigSystem.md (22KB) - Server config
- KB_REF_Permissions.md (14KB) - GM permissions
```

---

## ❌ **For C++ Source Modifications (MISSING FROM KB!)**

### **Critical Gap: Source Code KB Files Don't Exist Yet**

**Current KB Coverage**: 0% for C++ source modifications

**What You Need (NOT in current KB):**

#### **CRITICAL Missing KB Files:**

1. **KB_REF_SourceCodeStructure.md** (25KB) - MISSING
   ```
   What it should cover:
   - Directory structure (src/map/, src/char/, src/login/)
   - Key files (pc.cpp, mob.cpp, skill.cpp, itemdb.cpp, etc.)
   - Class hierarchies
   - Common patterns
   - Build system (CMake, dependencies)
   ```

2. **KB_REF_PluginSystem.md** (20KB) - MISSING
   ```
   What it should cover:
   - Plugin vs direct modification
   - HPM (Hercules Plugin Manager) hooks
   - Plugin structure
   - Available hooks list
   - Sample plugins
   - When to use plugins vs core edits
   ```

3. **KB_REF_ScriptCommandCreation.md** (15KB) - MISSING
   ```
   What it should cover:
   - Adding custom script commands
   - BUILDIN() macro usage
   - Parameter handling (script_getnum, script_getstr)
   - Return values (script_pushint, script_pushstr)
   - Complete examples
   - Common pitfalls
   ```

4. **KB_REF_PacketStructure.md** (20KB) - MISSING
   ```
   What it should cover:
   - Client-server packet structure
   - packet_db.txt
   - Adding custom packets
   - Packet handlers
   - clif.cpp functions
   - Security considerations
   ```

5. **KB_REF_DatabaseCPP.md** (18KB) - MISSING
   ```
   What it should cover:
   - Reading from databases (itemdb, mobdb, skilldb)
   - Adding new database fields
   - itemdb.cpp, mob.cpp, skill.cpp structure
   - Memory management
   - Database reload
   ```

6. **KB_REF_CompilationDebugging.md** (15KB) - MISSING
   ```
   What it should cover:
   - Compilation errors (common fixes)
   - Debugging with GDB/LLDB
   - Logging (ShowInfo, ShowWarning, ShowError)
   - Memory leaks detection
   - Performance profiling
   ```

7. **KB_REF_CommonSrcModifications.md** (20KB) - MISSING
   ```
   What it should cover:
   - Custom item bonuses
   - Custom status effects
   - Skill modifications
   - Damage formula changes
   - Custom monster AI
   - Map server modifications
   ```

8. **KB_REF_SourceCodeBestPractices.md** (12KB) - MISSING
   ```
   What it should cover:
   - Code style guidelines
   - Error handling patterns
   - Memory safety
   - Thread safety
   - Testing modifications
   - Version control for source mods
   ```

---

## 📊 **Current KB vs Needed KB for Source Modifications**

### **Current KB (Scripting/Config):**
| Area | Coverage | Files |
|------|----------|-------|
| NPC Scripting | ✅ 95% | 6 files |
| Database (YAML) | ✅ 90% | 7 files |
| Configuration | ✅ 85% | 3 files |
| System Mechanics | ✅ 80% | 5 files |
| **Total** | **✅ 85%** | **21 files** |

### **Needed KB (Source Code):**
| Area | Coverage | Status |
|------|----------|--------|
| C++ Source Structure | ❌ 0% | MISSING |
| Plugin System | ❌ 0% | MISSING |
| Packet Modifications | ❌ 0% | MISSING |
| Custom Script Commands | ❌ 0% | MISSING |
| Database C++ Code | ❌ 0% | MISSING |
| Compilation/Debugging | ❌ 0% | MISSING |
| Common Modifications | ❌ 0% | MISSING |
| Best Practices | ❌ 0% | MISSING |
| **Total** | **❌ 0%** | **8 files needed** |

---

## 🚀 **Recommended Action Plan**

### **Phase 1: Create Critical Source Code KB Files (Priority)**

I can create these RIGHT NOW:

**High Priority (Create First):**
1. **KB_REF_SourceCodeStructure.md** (25KB)
   - Directory layout, key files, build system
   - Essential for understanding where to make changes

2. **KB_REF_ScriptCommandCreation.md** (15KB)
   - How to add custom script commands
   - Most common source modification

3. **KB_REF_PluginSystem.md** (20KB)
   - Plugins vs core modifications
   - Safer approach than direct edits

**Medium Priority (Create Next):**
4. **KB_REF_DatabaseCPP.md** (18KB)
   - Working with item_db, mob_db in C++
   - Adding custom fields

5. **KB_REF_CompilationDebugging.md** (15KB)
   - Fixing compilation errors
   - Debugging techniques

**Lower Priority (Create Later):**
6. **KB_REF_PacketStructure.md** (20KB)
7. **KB_REF_CommonSrcModifications.md** (20KB)
8. **KB_REF_SourceCodeBestPractices.md** (12KB)

**Total to add**: ~145KB of source code documentation

---

## 💡 **Immediate Recommendations**

### **For Current Development (Scripting/Instances):**

**Load these KB files in your system prompt:**
```markdown
ALWAYS LOAD:
- KB_REF_Constants.md (required for all scripting)
- KB_REF_ScriptCommands.md (core syntax)

TASK-SPECIFIC:
- Instance work: KB_REF_InstanceSystem.md + INSTANCE_EVENT_FIX.md
- Advanced scripting: KB_REF_AdvancedScripting.md
- Database: KB_REF_DatabaseStructure.md
- Items: KB_REF_ItemBonuses.md
- Monsters: KB_REF_MobModesAI.md

REFERENCE ONLY:
- KB_REF_FAQ.md (when errors occur)
- Other KB files as needed
```

**System Prompt Template:**
```markdown
You are an rAthena expert developer. STRICT RULES:

1. ONLY use commands documented in loaded KB files
2. NEVER invent syntax - reference KB exactly
3. For constants: Use ONLY from KB_REF_Constants.md
4. For instances: Follow INSTANCE_EVENT_FIX.md pattern (separate global events)
5. If uncertain: Say "This requires information not in loaded KB"

Loaded KB for this task:
- KB_REF_ScriptCommands.md (core commands)
- KB_REF_Constants.md (required constants)
- KB_REF_InstanceSystem.md (instance mechanics)
- INSTANCE_EVENT_FIX.md (global event patterns)
```

### **For Source Modifications (After New KB Created):**

**Will load these (once I create them):**
```markdown
CRITICAL:
- KB_REF_SourceCodeStructure.md (where files are, what they do)
- KB_REF_ScriptCommandCreation.md (custom commands)
- KB_REF_PluginSystem.md (safer than core edits)

ADVANCED:
- KB_REF_DatabaseCPP.md (working with databases in C++)
- KB_REF_CompilationDebugging.md (fixing errors)
- KB_REF_PacketStructure.md (client-server communication)
```

---

## ❓ **Questions for You**

To create the RIGHT source code KB files for you:

1. **What source modifications do you make most often?**
   - Custom script commands?
   - Custom item bonuses?
   - Packet modifications?
   - Database changes?
   - Skill modifications?

2. **What errors do you encounter most?**
   - Compilation errors?
   - Runtime crashes?
   - Memory leaks?
   - Packet issues?

3. **Your experience level with C++?**
   - Beginner (need basics)?
   - Intermediate (know C++, new to rAthena)?
   - Advanced (need advanced patterns)?

4. **Priority order for source KB creation?**
   Which would help you most right now:
   - A. Script command creation
   - B. Plugin system
   - C. Source code structure
   - D. Database C++ modifications
   - E. All of the above

---

## 🎯 **Summary**

### **Current KB Status:**
✅ **Scripting/Instances/Config**: 85% covered (21 files, 388KB)
❌ **Source Code Modifications**: 0% covered (MISSING!)

### **For Expert Scripting (Current KB is Good):**
Load: Constants + ScriptCommands + InstanceSystem + AdvancedScripting

### **For Expert Source Mods (Need New KB):**
**Required**: 8 new KB files (~145KB) covering:
- Source structure
- Plugin system
- Custom commands
- Database C++
- Packets
- Debugging
- Common modifications
- Best practices

### **Next Step:**
Tell me which source code KB files to create first, and I'll make them NOW to fill this critical gap! 🚀
