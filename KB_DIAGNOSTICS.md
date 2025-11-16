# KB Diagnostics Checklist

## Is the KB enough? Run this checklist:

### ✅ Coverage Check
- [ ] Does KB cover the specific feature you need?
- [ ] Is the information accurate for your rAthena version?
- [ ] Are there working examples for your use case?
- [ ] Do you have the right KB files loaded for your task?

### ✅ System Prompt Check
**Current issues might be due to:**

1. **Token Limit Exceeded**
   - Full KB = 388KB ≈ 100K tokens
   - Many AI models limit: 32K-200K tokens
   - Solution: Load only relevant KB files per task

2. **Improper KB Loading**
   - ❌ Bad: Load all 21 KB files every time
   - ✅ Good: Load 2-4 relevant KB files per task

3. **Missing Instructions**
   - AI needs explicit instructions on HOW to use KB
   - Need clear format: "Reference KB_REF_X for Y, use exact syntax"

4. **Hallucination Issues**
   - AI invents commands not in KB
   - Solution: Add "ONLY use commands from KB_REF_ScriptCommands.md"

### ✅ Common Missing Topics (Not in Current KB)

**Source Code Level:**
- C++ modifications
- Plugin development
- Custom packets
- Client modifications

**Advanced Systems:**
- Battlegrounds detailed mechanics
- WoE (War of Emperium) systems
- Custom database tables
- Multi-server architecture

**Integration:**
- Web panel integration
- Discord bot integration
- Payment gateways
- External APIs

**Optimization:**
- Advanced SQL optimization
- Memory management
- Server hardening
- DDoS protection

**Client Files:**
- .lub files (lua)
- .grf files
- .spr/.act files
- iteminfo.lua

---

## 🔧 Recommended Solutions

### **Solution 1: Improve System Prompt Structure**

**Current (probably):**
```
You are an rAthena developer.
[Loads all 21 KB files]
```

**Improved:**
```
You are an rAthena developer. Follow these rules STRICTLY:

1. ONLY use commands documented in the loaded KB files
2. For scripting: Reference KB_REF_ScriptCommands.md for syntax
3. For database: Follow EXACT YAML structure from KB_REF_DatabaseStructure.md
4. For constants: Use ONLY constants from KB_REF_Constants.md
5. If unsure, say "This requires information not in current KB"

Loaded KB for this task:
- KB_REF_ScriptCommands.md (core commands)
- KB_REF_Constants.md (required constants)
```

### **Solution 2: Task-Specific KB Loading**

Don't load all KB files at once. Use this pattern:

**For NPC Creation:**
```
Load ONLY:
- KB_REF_ScriptCommands.md
- KB_REF_Constants.md
- KB_REF_NPCExamples.md
```

**For Item Creation:**
```
Load ONLY:
- KB_REF_DatabaseStructure.md
- KB_REF_ItemBonuses.md
- KB_REF_Constants.md
```

### **Solution 3: Add Missing KB Files**

I can create these additional KB files:

**High Priority (10-15KB each):**
- KB_REF_DebuggingGuide.md - Error diagnosis, debugging techniques
- KB_REF_CommonPatterns.md - Proven design patterns, anti-patterns
- KB_REF_EventSystems.md - WoE, BG, custom events
- KB_REF_SQLAdvanced.md - Complex queries, optimization, transactions

**Medium Priority (15-20KB each):**
- KB_REF_SourceModifications.md - C++ basics, plugin system
- KB_REF_ClientFiles.md - lub files, client data
- KB_REF_SecurityGuide.md - Security hardening, protection
- KB_REF_VersionDifferences.md - RE vs Pre-RE specifics

**Low Priority (5-10KB each):**
- KB_REF_Troubleshooting.md - Common errors with solutions
- KB_REF_BestPractices.md - Do's and don'ts
- KB_REF_PerformanceTips.md - Optimization checklist

---

## 💬 What I Need From You

**To help fix your specific issues, please tell me:**

1. **What task fails most often?**
   - NPC scripting?
   - Database creation?
   - Configuration?
   - Something else?

2. **Example of a failure case?**
   - What did you ask AI to do?
   - What did it produce?
   - What went wrong?

3. **Your rAthena version?**
   - Latest (2024)?
   - Older version?
   - Renewal or Pre-Renewal?

4. **Your current system prompt?**
   - How are you loading KB files?
   - What instructions do you give AI?

5. **Missing topics?**
   - What features/topics do you need that aren't covered?

---

## 🚀 Immediate Action

**I can create right now:**

Option A: **5 critical missing KB files** (50-75KB total)
- Debugging guide
- Common patterns
- SQL advanced
- Event systems
- Troubleshooting

Option B: **Enhanced system prompt template**
- Optimized KB loading strategy
- Strict validation rules
- Task-specific examples

Option C: **KB usage guide**
- How to properly use KB in system prompts
- Token optimization
- Task-to-KB mapping

**Which would help you most?**
