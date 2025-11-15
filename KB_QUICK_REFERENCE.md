# rAthena Knowledge Base - Quick Reference for System Prompts

**Version**: v3.0 | **Files**: 21 | **Total**: 388KB | **Coverage**: 85%

---

## 📋 Quick Lookup Snippets (All 21 KB Files)

### 🎯 **Database & Content** (7 files)

#### KB_REF_DatabaseStructure.md (21KB)
```
Complete database reference: item_db, mob_db, skill_db, quest_db, produce_db
YAML structures, all field types, validation rules, import system
Use for: Database creation, YAML editing, field reference
```

#### KB_REF_ItemBonuses.md (15KB)
```
200+ item bonus commands: bonus, bonus2, bonus3, bonus4, bonus5
Equipment bonuses, combat modifiers, special effects
Use for: Item scripting, equipment creation, bonus combinations
```

#### KB_REF_ItemGroups.md (27KB)
```
Item groups & random boxes: groupranditem, getrandgroupitem, getgroupitem
3 algorithms (Random/All/SharedPool), SubGroups, gacha systems
Use for: Loot boxes, rewards, Old Blue Box, Card Albums, random drops
```

#### KB_REF_MobModesAI.md (15KB)
```
Monster AI & behavior: 27 AI types (01-27), 30+ mode flags (MD_*)
5 class types (Normal/Boss/Guardian/Battlefield/Event), attributes
Use for: Monster creation, boss mechanics, AI behavior, immunity
```

#### KB_REF_SkillSystem.md (21KB)
```
Skill database: skill_db, skill requirements, cast times, cooldowns
Skill trees, job mastery, skill flags, skill_require_db
Use for: Custom skills, skill balancing, job-specific skills
```

#### KB_REF_StatusEffects.md (14KB)
```
400+ status effects: SC_* constants, effect IDs, durations
Status icons, buff/debuff mechanics, status immunity
Use for: Custom buffs, status scripting, effect reference
```

#### KB_REF_VisualEffects.md (13KB)
```
Visual effects & colors: effect(), specialeffect(), hex colors
Screen effects, animations, particle effects, color codes
Use for: NPC effects, skill visuals, event effects
```

---

### 💻 **Scripting** (6 files)

#### KB_REF_ScriptCommands.md (21KB)
```
100+ core script commands: mes, next, close, getitem, warp, set
Basic NPC structure, control flow, variables, operators
Use for: Basic NPC scripting, fundamental commands
```

#### KB_REF_ScriptCommandsExpanded.md (20KB)
```
120+ advanced commands: query_sql, instance_*, getd/setd, freeloop
Arrays, SQL, dynamic variables, timers, special mechanics
Use for: Advanced NPCs, SQL integration, optimization
```

#### KB_REF_AdvancedScripting.md (34KB)
```
Expert patterns: 2D arrays, dynamic shops, PCRE regex, SQL safety
Performance optimization (freeloop, caching), error handling
Use for: Complex systems, optimization, dynamic content, daily quests
```

#### KB_REF_Constants.md (14KB)
```
200+ essential constants: EQP_*, RC_*, Ele_*, Size_*, Job_*
Equipment locations, races, elements, sizes, job IDs
Use for: All scripting (always needed), constant reference
```

#### KB_REF_NPCExamples.md (16KB)
```
20+ working NPC examples: shops, warpers, buffers, quests
Complete code samples, best practices, common patterns
Use for: Learning scripting, copy-paste templates
```

#### KB_REF_FAQ.md (13KB)
```
50+ common issues & solutions: script errors, variable scope
Troubleshooting guide, common mistakes, debugging tips
Use for: Error fixing, learning pitfalls, quick answers
```

---

### ⚙️ **System Mechanics** (5 files)

#### KB_REF_InstanceSystem.md (32KB)
```
Memorial dungeons & instances: instance_create, instance_destroy
5 modes (CHAR/PARTY/GUILD/CLAN/NONE), instance variables ('var)
Use for: Dungeons, raids, solo trials, isolated maps
```

#### KB_REF_QuestSystem.md (13KB)
```
Quest database: quest_db, quest objectives, rewards
Quest scripting, checkquest, setquest, completequest
Use for: Quest creation, progression systems
```

#### KB_REF_JobSystem.md (16KB)
```
Job system: job IDs, job mastery, class changes
BaseJob, BaseClass, Upper, job trees, rebirth system
Use for: Job scripts, class restrictions, job checks
```

#### KB_REF_MapFlags.md (27KB)
```
100+ map flags: mapflag, setmapflag, nosave, pvp, gvg
Map properties, restrictions, special zones
Use for: Map configuration, zone mechanics
```

#### KB_REF_AtCommands.md (23KB)
```
100+ admin commands: @item, @warp, @stats, @monster
GM tools, testing commands, server management
Use for: Admin tools, debugging, GM NPCs
```

---

### 🔧 **Configuration** (3 files)

#### KB_REF_BattleConfig.md (15KB)
```
Battle mechanics config: battle/battle.conf, exp rates, damage
Monster AI, drop rates, penalties, game balance
Use for: Server balancing, rates configuration
```

#### KB_REF_ConfigSystem.md (22KB)
```
Server configuration: conf/import/, char-server, map-server
Import system, server settings, ports, SQL connection
Use for: Server setup, configuration management
```

#### KB_REF_Permissions.md (14KB)
```
Groups & permissions: conf/groups.yml, GM levels, commands
Access control, command restrictions, inheritance
Use for: GM hierarchy, command permissions
```

---

## 🎯 Usage Guide for System Prompts

### **Task-Based KB Loading**

#### For NPC Scripting:
```markdown
Load: KB_REF_ScriptCommands.md, KB_REF_Constants.md
Optional: KB_REF_NPCExamples.md (for templates)
```

#### For Item Creation:
```markdown
Load: KB_REF_DatabaseStructure.md, KB_REF_ItemBonuses.md
Optional: KB_REF_Constants.md (for EQP_*, bonus constants)
```

#### For Monster Creation:
```markdown
Load: KB_REF_DatabaseStructure.md, KB_REF_MobModesAI.md
Optional: KB_REF_StatusEffects.md (for immunities)
```

#### For Quest Development:
```markdown
Load: KB_REF_QuestSystem.md, KB_REF_ScriptCommands.md
Optional: KB_REF_ItemGroups.md (for rewards)
```

#### For Instance/Dungeon Creation:
```markdown
Load: KB_REF_InstanceSystem.md, KB_REF_ScriptCommandsExpanded.md
Optional: KB_REF_MobModesAI.md (for bosses)
```

#### For Advanced Scripting:
```markdown
Load: KB_REF_AdvancedScripting.md, KB_REF_ScriptCommandsExpanded.md
Optional: KB_REF_InstanceSystem.md, KB_REF_ItemGroups.md
```

#### For Server Configuration:
```markdown
Load: KB_REF_ConfigSystem.md, KB_REF_BattleConfig.md
Optional: KB_REF_Permissions.md (for GM setup)
```

#### For Troubleshooting:
```markdown
Load: KB_REF_FAQ.md
Optional: Relevant system KB based on error type
```

---

## 📊 KB File Priority Levels

### **Critical (Always Load These)**
- KB_REF_Constants.md - Required for all scripting
- KB_REF_ScriptCommands.md - Core command reference

### **High Priority (Load for Specific Tasks)**
- KB_REF_DatabaseStructure.md - Database work
- KB_REF_ItemBonuses.md - Item creation
- KB_REF_MobModesAI.md - Monster creation
- KB_REF_InstanceSystem.md - Instance dungeons
- KB_REF_AdvancedScripting.md - Complex systems

### **Medium Priority (Load as Needed)**
- KB_REF_ScriptCommandsExpanded.md - Advanced scripting
- KB_REF_ItemGroups.md - Random boxes/rewards
- KB_REF_QuestSystem.md - Quest development
- KB_REF_MapFlags.md - Map configuration
- KB_REF_JobSystem.md - Job-related work

### **Supporting (Reference Only)**
- KB_REF_NPCExamples.md - Learning/templates
- KB_REF_FAQ.md - Troubleshooting
- KB_REF_StatusEffects.md - Effect reference
- KB_REF_VisualEffects.md - Visual effects
- KB_REF_AtCommands.md - Admin tools
- KB_REF_BattleConfig.md - Server config
- KB_REF_ConfigSystem.md - Server setup
- KB_REF_Permissions.md - GM config

---

## 🔍 Quick Search Index

**Arrays**: KB_REF_ScriptCommandsExpanded.md, KB_REF_AdvancedScripting.md
**Bonuses**: KB_REF_ItemBonuses.md
**Boss Mechanics**: KB_REF_MobModesAI.md, KB_REF_InstanceSystem.md
**Constants**: KB_REF_Constants.md (all EQP_*, RC_*, Ele_*, etc.)
**Database**: KB_REF_DatabaseStructure.md (item_db, mob_db, skill_db)
**Drops/Loot**: KB_REF_ItemGroups.md, KB_REF_MobModesAI.md
**Errors/Debug**: KB_REF_FAQ.md
**GM Commands**: KB_REF_AtCommands.md, KB_REF_Permissions.md
**Instances**: KB_REF_InstanceSystem.md
**Items**: KB_REF_DatabaseStructure.md, KB_REF_ItemBonuses.md
**Jobs**: KB_REF_JobSystem.md
**Maps**: KB_REF_MapFlags.md
**Monsters**: KB_REF_DatabaseStructure.md, KB_REF_MobModesAI.md
**NPCs**: KB_REF_ScriptCommands.md, KB_REF_NPCExamples.md
**Optimization**: KB_REF_AdvancedScripting.md (freeloop, caching)
**Quests**: KB_REF_QuestSystem.md
**Random Boxes**: KB_REF_ItemGroups.md
**Skills**: KB_REF_SkillSystem.md
**SQL**: KB_REF_AdvancedScripting.md, KB_REF_ScriptCommandsExpanded.md
**Status Effects**: KB_REF_StatusEffects.md
**Variables**: KB_REF_ScriptCommands.md (basics), KB_REF_AdvancedScripting.md (advanced)
**Visuals**: KB_REF_VisualEffects.md

---

## 💡 System Prompt Templates

### **Template: General NPC Developer**
```
You are an rAthena NPC developer. Reference knowledge:
- KB_REF_ScriptCommands.md (core commands)
- KB_REF_Constants.md (constants)
- KB_REF_NPCExamples.md (patterns)

Always validate input, use proper constants, follow best practices.
```

### **Template: Database Specialist**
```
You are an rAthena database specialist. Reference knowledge:
- KB_REF_DatabaseStructure.md (YAML structures)
- KB_REF_ItemBonuses.md (item bonuses)
- KB_REF_MobModesAI.md (monster AI)

Follow YAML format strictly, validate all fields, use correct types.
```

### **Template: Advanced System Developer**
```
You are an rAthena advanced developer. Reference knowledge:
- KB_REF_AdvancedScripting.md (patterns, optimization)
- KB_REF_InstanceSystem.md (instances)
- KB_REF_ScriptCommandsExpanded.md (advanced commands)

Optimize performance, use SQL safely, implement complex systems.
```

---

## 📦 Download Locations

All files available at: `/home/user/rathena2/`

**Archives**:
- `rathena_kb_files_v4.zip` (132KB) - All 21 files
- `rathena_kb_files_v4.tar.gz` (123KB) - All 21 files
- `rathena_kb_complete_v4.md` (410KB) - Single merged file

**Individual Files**: `kb/references/KB_REF_*.md`
**Index**: `kb/KB_INDEX_v3.md` (complete navigation)

---

**End of Quick Reference**
