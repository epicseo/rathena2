# rAthena KB v4 Cross-Reference Index

**Version:** Enhancement v1.0
**Purpose:** Query routing and cross-file navigation
**Last Updated:** 2025-11-26

---

## Query Routing Guide

### By Topic Category

| User Query Contains | Primary KB | Secondary KB |
|---------------------|------------|--------------|
| script command, mes, getitem | 02_SCRIPTING_COMPLETE | - |
| SC_*, status effect, buff, debuff | 03_GAME_MECHANICS + **01_STATUS_EFFECTS_COMPLETE** | 02_SCRIPTING |
| bonus, bStr, bAtk, item effect | 03_GAME_MECHANICS + **02_ITEM_BONUSES_COMPLETE** | - |
| mapflag, mf_, map setting | 03_GAME_MECHANICS | - |
| quest, quest_db, TimeLimit | 04_CONTENT_CREATION | 02_SCRIPTING |
| gacha, item_group, random box | 04_CONTENT_CREATION | - |
| NPC pattern, state machine | 04_CONTENT_CREATION | 02_SCRIPTING |
| struct, map_session_data, source | 05_SOURCE_DEVELOPMENT | 06_DATABASE |
| atcommand, custom @command | 05_SOURCE_DEVELOPMENT | - |
| item_db, skill_db, mob_db, YAML | 06_DATABASE_SYSTEMS | - |
| PACKETVER, packet, client | 06_DATABASE_SYSTEMS | - |
| compile, build, cmake | 06_DATABASE_SYSTEMS | - |
| battle formula, damage calc | 07_INTERNALS_REFERENCE | - |
| script internals, timer | 07_INTERNALS_REFERENCE | - |
| tutorial, guide, how to | 08_SOURCE_REFERENCE | varies |

---

## Enhancement Files Index

### 01_STATUS_EFFECTS_COMPLETE.md
**Fills Gap:** SC_* documentation (was 4.6% coverage, now ~50%)
**Content:**
- 200+ documented status effects
- val1-val4 parameters for each
- EFST/OPT mappings
- Script examples

**Load When:**
- User asks about any SC_* constant
- User asks about status effect mechanics
- User asks about sc_start/sc_end usage
- User asks about status duration/parameters

### 02_ITEM_BONUSES_COMPLETE.md
**Fills Gap:** Item bonus documentation (was 36% coverage, now ~90%)
**Content:**
- 263 bonuses documented
- All bonus variants (bonus, bonus2, bonus3, bonus4, bonus5)
- Constant references (eff, r, e, c, s, bf, atf)
- Examples for each category

**Load When:**
- User asks about any bXxx bonus
- User asks about item script effects
- User asks about equipment customization
- User asks about damage/defense modifiers

---

## File Relationship Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                    01_MASTER_INDEX.md                           │
│                    (Navigation Hub)                             │
└────────────────────────────┬────────────────────────────────────┘
                             │
      ┌──────────────────────┼──────────────────────┐
      │                      │                      │
      ▼                      ▼                      ▼
┌─────────────┐       ┌─────────────┐       ┌─────────────┐
│ SCRIPTING   │       │ MECHANICS   │       │ CONTENT     │
│ 02_SCRIPT   │◄─────►│ 03_MECH     │◄─────►│ 04_CONTENT  │
│ COMPLETE    │       │             │       │ CREATION    │
└─────────────┘       └──────┬──────┘       └─────────────┘
      │                      │                      │
      │               ┌──────┴──────┐               │
      │               │ ENHANCEMENTS│               │
      │               │ 01_SC_*     │               │
      │               │ 02_BONUS    │               │
      │               └─────────────┘               │
      │                                             │
      ▼                      ▼                      ▼
┌─────────────┐       ┌─────────────┐       ┌─────────────┐
│ SOURCE DEV  │       │ DATABASE    │       │ INTERNALS   │
│ 05_SOURCE   │◄─────►│ 06_DATABASE │◄─────►│ 07_INTERNAL │
│ DEVELOPMENT │       │ SYSTEMS     │       │ REFERENCE   │
└─────────────┘       └─────────────┘       └─────────────┘
                             │
                             ▼
                      ┌─────────────┐
                      │ EXPERT REF  │
                      │ 08_SOURCE   │
                      │ REFERENCE   │
                      └─────────────┘
```

---

## Common Multi-File Queries

### Query: "Create custom item with special effects"
**Load:**
1. 06_DATABASE_SYSTEMS (item_db.yml structure)
2. **02_ITEM_BONUSES_COMPLETE** (bonus syntax)
3. 02_SCRIPTING_COMPLETE (script command syntax)

### Query: "Add status effect that reduces damage"
**Load:**
1. **01_STATUS_EFFECTS_COMPLETE** (SC_* reference)
2. 03_GAME_MECHANICS (status interaction)
3. 05_SOURCE_DEVELOPMENT (if modifying source)

### Query: "Create gacha box with rare announce"
**Load:**
1. 04_CONTENT_CREATION (item_group_db)
2. 02_SCRIPTING_COMPLETE (getgroupitem)

### Query: "Modify battle formula for skill"
**Load:**
1. 07_INTERNALS_REFERENCE (battle formulas)
2. 05_SOURCE_DEVELOPMENT (source modification)

### Query: "Create quest with timed objectives"
**Load:**
1. 04_CONTENT_CREATION (quest_db.yml)
2. 02_SCRIPTING_COMPLETE (setquest, checkquest)

---

## Enhancement Integration Notes

### For AI/RAG Systems

When loading 03_GAME_MECHANICS.md for SC_* or bonus queries:
- **ALWAYS** also load the corresponding enhancement file
- Enhancement files contain 10x more detail
- Base KB provides context, enhancement provides specifics

### Priority Loading Order

1. Base KB file for topic overview
2. Enhancement file for detailed reference
3. Related KB files for cross-references

### Example RAG Context Building

```python
# Pseudo-code for query routing
if "SC_" in query or "status" in query:
    context = load("03_GAME_MECHANICS.md")
    context += load("01_STATUS_EFFECTS_COMPLETE.md")  # Enhancement
    if "script" in query:
        context += load("02_SCRIPTING_COMPLETE.md")

if "bonus" in query or "bStr" in query or "item effect" in query:
    context = load("03_GAME_MECHANICS.md")
    context += load("02_ITEM_BONUSES_COMPLETE.md")  # Enhancement
```

---

## Version Compatibility

| Enhancement File | Compatible With | Notes |
|-----------------|-----------------|-------|
| 01_STATUS_EFFECTS | KB v4.0+ | Supplements 03_GAME_MECHANICS |
| 02_ITEM_BONUSES | KB v4.0+ | Supplements 03_GAME_MECHANICS |
| 03_CROSS_REFERENCE | KB v4.0+ | Navigation aid |

---

*Generated as part of KB v4.0.1 Enhancement Package*
