---
kb_id: KB_REF_028
title: "Common Source Code Modifications (Step-by-Step)"
category: Source Code
keywords: [source_modifications, custom_bonuses, custom_skills, damage_formulas, custom_status_effects, item_bonuses, drop_rate, exp_rate, stat_modifications]
related_files: [
  "src/map/pc.cpp",
  "src/map/battle.cpp",
  "src/map/skill.cpp",
  "src/map/status.cpp",
  "src/map/mob.cpp",
  "src/map/itemdb.cpp"
]
difficulty: expert
use_case: "Step-by-step guides for the most common source code modifications"
version: rAthena 2024
last_updated: 2024-01-15
---

# Common Source Code Modifications (Step-by-Step)

## Quick Reference

### **Add Custom Item Bonus**
```cpp
// In src/map/pc.cpp (pc_bonus function)
case SP_CUSTOM_ATK_BONUS:
    sd->bonus.atk_rate += val;
    break;

// In item script (item_db.yml):
bonus SP_CUSTOM_ATK_BONUS,20;  // +20% ATK
```

### **Modify Damage Formula**
```cpp
// In src/map/battle.cpp (battle_calc_weapon_attack)
damage = (wd->damage + wd->damage2) / 2;  // Original
damage = damage * 150 / 100;              // +50% damage boost
```

### **Add Custom Drop**
```cpp
// In src/map/mob.cpp (mob_dead)
if (md->mob_id == 1002) {  // Poring
    pc_giveitem(sd, 501, 1, LOG_TYPE_PICKDROP_PLAYER);  // Always drop Red Potion
}
```

---

## Table of Contents
1. [Custom Item Bonuses](#custom-item-bonuses)
2. [Custom Status Effects](#custom-status-effects)
3. [Damage Formula Modifications](#damage-formula-modifications)
4. [Custom Skills](#custom-skills)
5. [Drop Rate Modifications](#drop-rate-modifications)
6. [EXP Rate Modifications](#exp-rate-modifications)
7. [Custom Player Stats](#custom-player-stats)
8. [Custom Level Cap](#custom-level-cap)
9. [Custom Equipment Slots](#custom-equipment-slots)
10. [Testing Your Modifications](#testing-your-modifications)

---

## Custom Item Bonuses

### **Goal**: Add a new item bonus `bonus bCustomDamage,<value>;`

**Effect**: Increases all damage by a flat amount.

---

### **Step 1: Define Constant**

**In src/map/pc.hpp** (around line 100, in `enum _sp` enum):

```cpp
enum _sp {
    SP_SPEED = 0,
    SP_BASEEXP,
    SP_JOBEXP,
    // ... existing constants ...

    // *** Add custom constant ***
    SP_CUSTOM_DAMAGE = 10000,  // Use high number to avoid conflicts
};
```

---

### **Step 2: Add Struct Field**

**In src/map/pc.hpp** (in `struct map_session_data`, around line 500):

```cpp
struct map_session_data {
    // ... existing fields ...

    struct {
        int str, agi, vit, int_, dex, luk;
        int atk_rate, matk_rate;
        // ... more bonus fields ...

        // *** Add custom bonus field ***
        int custom_damage;
    } bonus;

    // ... more fields ...
};
```

---

### **Step 3: Initialize Field**

**In src/map/status.cpp** (in `status_calc_pc_`, around line 3000):

```cpp
int status_calc_pc_(struct map_session_data* sd, enum e_status_calc_opt opt) {
    // Clear bonus struct
    memset(&sd->bonus, 0, sizeof(sd->bonus));

    // *** Initialize custom field ***
    sd->bonus.custom_damage = 0;

    // ... rest of function ...
}
```

---

### **Step 4: Implement Bonus**

**In src/map/pc.cpp** (in `pc_bonus` function, around line 7000):

```cpp
int pc_bonus(struct map_session_data *sd, int type, int val) {
    nullpo_ret(sd);

    switch(type) {
        case SP_STR:
            sd->bonus.str += val;
            break;
        // ... hundreds of other cases ...

        // *** Add custom bonus case ***
        case SP_CUSTOM_DAMAGE:
            sd->bonus.custom_damage += val;
            break;

        default:
            ShowWarning("pc_bonus: unknown type %d %d!\n", type, val);
            break;
    }
    return 0;
}
```

---

### **Step 5: Apply Bonus to Damage**

**In src/map/battle.cpp** (in `battle_calc_weapon_attack`, around line 4000):

```cpp
static struct Damage battle_calc_weapon_attack(...) {
    // ... calculate base damage ...

    // Final damage calculation
    wd.damage = (wd.damage + wd.damage2) / 2;

    // *** Apply custom damage bonus ***
    if (sd) {
        wd.damage += sd->bonus.custom_damage;
    }

    return wd;
}
```

---

### **Step 6: Use in Items**

**In db/re/item_db.yml** (or db/import/item_db.yml):

```yaml
- Id: 60000
  AegisName: PowerSword
  Name: "Sword of Power"
  Type: Weapon
  SubType: 1hSword
  Attack: 150
  Script: |
    bonus bAtk,50;
    bonus bCustomDamage,100;  // *** +100 flat damage ***
```

---

### **Step 7: Compile and Test**

```bash
cd build
cmake ..
make -j$(nproc)
make install

cd ..
./map-server
```

**Test in-game**:
```
@item 60000 1  // Get PowerSword
@equip PowerSword
@mi 1002  // Attack Poring - observe increased damage
```

---

## Custom Status Effects

### **Goal**: Add a custom status effect `SC_CUSTOM_HASTE` that doubles movement speed.

---

### **Step 1: Define Status Constant**

**In src/map/status.hpp** (around line 300, in `enum sc_type`):

```cpp
enum sc_type {
    SC_NONE = 0,
    SC_STONE = 1,
    SC_FREEZE,
    // ... existing status effects ...
    SC_MAX,  // Last official status (around 700)

    // *** Add custom status ***
    SC_CUSTOM_HASTE = SC_MAX + 1,

    SC_MAX_EXTENDED
};
```

---

### **Step 2: Add Status Data**

**In src/map/status.cpp** (in `status_change_start` function):

```cpp
int status_change_start(...) {
    // ... existing status checks ...

    switch (type) {
        case SC_STONE:
        case SC_FREEZE:
        // ... hundreds of cases ...

        // *** Add custom status case ***
        case SC_CUSTOM_HASTE:
            val1 = 200;  // 200% movement speed
            break;
    }

    // ... rest of function ...
}
```

---

### **Step 3: Apply Status Effect**

**In src/map/status.cpp** (in `status_calc_speed` function, around line 6000):

```cpp
static unsigned short status_calc_speed(struct block_list *bl, struct status_change *sc, int speed) {
    // ... existing speed calculations ...

    // *** Apply custom haste ***
    if (sc->data[SC_CUSTOM_HASTE]) {
        speed = speed * 100 / sc->data[SC_CUSTOM_HASTE]->val1;  // val1 = 200 = 2x speed
    }

    return (unsigned short)cap_value(speed, MIN_WALK_SPEED, MAX_WALK_SPEED);
}
```

---

### **Step 4: Add Status Icon (Optional)**

**In src/map/clif.cpp** (status icon mapping):

```cpp
// Add status icon ID (from client)
const int SI_CUSTOM_HASTE = 1000;  // Use unused icon ID

// In clif_status_change function:
case SC_CUSTOM_HASTE:
    si = SI_CUSTOM_HASTE;
    break;
```

---

### **Step 5: Create Script Command**

**In src/custom/script.inc**:

```cpp
/**
 * customhaste(<duration>)
 * Apply custom haste status
 * @param duration: Duration in seconds
 */
BUILDIN_FUNC(customhaste)
{
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) return 1;

    int duration = script_getnum(st, 2) * 1000;  // Convert to ms

    sc_start(NULL, &sd->bl, SC_CUSTOM_HASTE, 100, 1, duration);

    script_pushint(st, 1);
    return 0;
}
```

**In src/custom/script_def.inc**:

```cpp
BUILDIN_DEF(customhaste, "i"),
```

---

### **Step 6: Use in Scripts**

```c
prontera,150,150,4	script	Speed Booster	123,{
    mes "[Speed Booster]";
    mes "Want to move faster?";
    if (select("Yes:No") == 2) close;

    customhaste(60);  // 60 seconds of haste
    mes "You feel incredibly fast!";
    close;
}
```

---

## Damage Formula Modifications

### **Goal**: Increase all physical damage by 50%

---

### **Method 1: Global Damage Increase**

**In src/map/battle.cpp** (in `battle_calc_weapon_attack`, around line 5000):

```cpp
static struct Damage battle_calc_weapon_attack(...) {
    // ... complex damage calculations ...

    // Final damage
    wd.damage = (wd.damage + wd.damage2) / 2;

    // *** GLOBAL DAMAGE BOOST ***
    wd.damage = wd.damage * 150 / 100;  // +50%

    return wd;
}
```

---

### **Method 2: Conditional Damage Increase**

**In src/map/battle.cpp**:

```cpp
static struct Damage battle_calc_weapon_attack(...) {
    // ... damage calculations ...

    // *** Increase damage for swordsman class ***
    if (sd && (sd->class_&MAPID_BASEMASK) == MAPID_SWORDMAN) {
        wd.damage = wd.damage * 120 / 100;  // +20% for swordsman
    }

    // *** Increase damage vs boss monsters ***
    if (tsd && status_get_class(target) == CLASS_BOSS) {
        wd.damage = wd.damage * 130 / 100;  // +30% vs bosses
    }

    return wd;
}
```

---

### **Method 3: Custom Damage Formula**

**Replace entire damage calculation**:

```cpp
static struct Damage battle_calc_weapon_attack(...) {
    // ... existing setup code ...

    // *** CUSTOM FORMULA: (ATK * 2) + (STR * 5) ***
    int custom_atk = status_get_atk(src);
    int custom_str = status_get_base_status(src)->str;

    wd.damage = (custom_atk * 2) + (custom_str * 5);

    // Apply target defense
    int target_def = status_get_def(target);
    wd.damage -= target_def;

    // Ensure minimum damage
    if (wd.damage < 1) wd.damage = 1;

    return wd;
}
```

---

### **Method 4: Modify Critical Damage**

**In src/map/battle.cpp**:

```cpp
static struct Damage battle_calc_weapon_attack(...) {
    // ... damage calculations ...

    // Critical hit detection
    if (is_critical) {
        wd.type = 0x0a;  // Critical

        // *** Original: 40% bonus ***
        // wd.damage = wd.damage * 140 / 100;

        // *** Modified: 100% bonus (double damage) ***
        wd.damage = wd.damage * 200 / 100;
    }

    return wd;
}
```

---

## Custom Skills

### **Goal**: Add a custom healing skill that heals based on player level.

---

### **Step 1: Define Skill ID**

**In src/map/skill.hpp** (around line 100):

```cpp
enum e_skill {
    NV_BASIC = 1,
    SM_SWORD,
    // ... existing skills ...
    ALL_FULL_THROTTLE = 5007,

    // *** Custom skills (use IDs > 10000 to avoid conflicts) ***
    CUSTOM_POWER_HEAL = 10001,
};
```

---

### **Step 2: Add Skill to Database**

**In db/re/skill_db.yml**:

```yaml
- Id: 10001
  Name: CUSTOM_POWER_HEAL
  Description: "Power Heal"
  MaxLevel: 10
  Type: Self
  TargetType: Self
  DamageFlags:
    NoDamage: true
  Range: 0
  Hit: BDT_SKILL
  SkillType: Magic
  Element: Holy
  Requirements:
    SPCost:
      - 10
      - 15
      - 20
      - 25
      - 30
      - 35
      - 40
      - 45
      - 50
      - 55
  CastTime:
    - 500
    - 500
    - 500
    - 500
    - 500
    - 500
    - 500
    - 500
    - 500
    - 500
  CoolDown:
    - 3000
    - 3000
    - 3000
    - 3000
    - 3000
    - 3000
    - 3000
    - 3000
    - 3000
    - 3000
```

---

### **Step 3: Implement Skill Logic**

**In src/map/skill.cpp** (in `skill_castend_nodamage_id` function, around line 8000):

```cpp
int skill_castend_nodamage_id(...) {
    // ... existing skill cases ...

    case CUSTOM_POWER_HEAL:
    {
        struct map_session_data *sd = BL_CAST(BL_PC, src);
        if (!sd) break;

        // Heal amount: Level * Skill_Level * 10
        int heal_amount = sd->status.base_level * skill_lv * 10;

        // Heal player
        int hp_healed = pc_heal(sd, heal_amount, 0, 1);

        // Show effect
        clif_skill_nodamage(src, bl, skill_id, skill_lv, 1);
        clif_specialeffect(src, EF_HEAL, AREA);

        // Send message
        char message[100];
        sprintf(message, "Healed %d HP!", hp_healed);
        clif_displaymessage(sd->fd, message);

        break;
    }

    // ... rest of function ...
}
```

---

### **Step 4: Add Skill to Skill Tree**

**In db/re/skill_tree.yml** (for testing, give to Novice):

```yaml
- Job: Novice
  Skills:
    # ... existing skills ...
    - Name: CUSTOM_POWER_HEAL
      MaxLevel: 10
```

---

### **Step 5: Compile and Test**

```bash
make -j$(nproc)
make install
./map-server
```

**Test**:
```
@job 0  # Become Novice
@allskill  # Get all skills
# Open skill window, find "Power Heal"
# Use skill
```

---

## Drop Rate Modifications

### **Goal**: Increase card drop rates by 10x

---

### **Method 1: Global Drop Rate**

**In src/map/mob.cpp** (in `mob_droprate` function, around line 5000):

```cpp
static int mob_droprate(struct mob_data *md, int nameid, int rate) {
    struct item_data *id = itemdb_search(nameid);

    // Apply battle config rates
    rate = rate * battle_config.item_rate_common / 100;

    // *** Increase card drop rates by 10x ***
    if (id && id->type == IT_CARD) {
        rate = rate * 1000 / 100;  // 10x for cards
    }

    return rate;
}
```

---

### **Method 2: Conditional Drop Boost**

**In src/map/mob.cpp**:

```cpp
static int mob_droprate(struct mob_data *md, int nameid, int rate) {
    struct item_data *id = itemdb_search(nameid);

    // *** 5x drops on weekends ***
    time_t now = time(NULL);
    struct tm *timeinfo = localtime(&now);
    int day_of_week = timeinfo->tm_wday;  // 0=Sunday, 6=Saturday

    if (day_of_week == 0 || day_of_week == 6) {
        rate = rate * 500 / 100;  // 5x
    }

    // *** 2x card drops for MVP monsters ***
    if (id && id->type == IT_CARD && md->db->boss_type == BOSSTYPE_MVP) {
        rate = rate * 200 / 100;  // 2x
    }

    return rate;
}
```

---

### **Method 3: Add Custom Drops**

**In src/map/mob.cpp** (in `mob_dead` function, around line 3000):

```cpp
int mob_dead(struct mob_data *md, struct block_list *src, int type) {
    // ... existing code ...

    // *** Custom drops for specific mobs ***
    if (md->mob_id == 1002) {  // Poring
        // Always drop 1x Red Potion
        pc_giveitem(sd, 501, 1, LOG_TYPE_PICKDROP_PLAYER);
    }

    if (md->mob_id == 1288) {  // Emperium
        // Always drop 1x Emperium + 100x TCG Card
        pc_giveitem(sd, 714, 1, LOG_TYPE_PICKDROP_PLAYER);  // Emperium
        pc_giveitem(sd, 7227, 100, LOG_TYPE_PICKDROP_PLAYER);  // TCG Card
    }

    // *** 10% chance to drop custom item from all monsters ***
    if (rnd() % 100 < 10) {
        pc_giveitem(sd, 60000, 1, LOG_TYPE_PICKDROP_PLAYER);  // Custom item
    }

    return 0;
}
```

---

## EXP Rate Modifications

### **Goal**: Modify EXP gain based on level difference

---

### **Method 1: Level-Based EXP**

**In src/map/pc.cpp** (in `pc_gainexp` function, around line 8000):

```cpp
int pc_gainexp(struct map_session_data *sd, struct block_list *src,
               uint64 base_exp, uint64 job_exp, bool is_quest) {
    // ... existing code ...

    // *** Low level boost: 5x EXP for levels 1-50 ***
    if (sd->status.base_level < 50) {
        base_exp = base_exp * 5;
        job_exp = job_exp * 5;
    }

    // *** High level penalty: 0.5x EXP for levels 90+ ***
    if (sd->status.base_level >= 90) {
        base_exp = base_exp * 50 / 100;
        job_exp = job_exp * 50 / 100;
    }

    // ... apply EXP ...
}
```

---

### **Method 2: Mob Level Difference Penalty**

**In src/map/mob.cpp** (in `mob_dead` function):

```cpp
int mob_dead(struct mob_data *md, struct block_list *src, int type) {
    // ... calculate base_exp, job_exp ...

    // *** Penalty for killing low-level mobs ***
    int level_diff = sd->status.base_level - md->level;

    if (level_diff > 10) {
        // 10% penalty per level difference over 10
        int penalty = (level_diff - 10) * 10;
        if (penalty > 90) penalty = 90;  // Max 90% penalty

        base_exp = base_exp * (100 - penalty) / 100;
        job_exp = job_exp * (100 - penalty) / 100;
    }

    // Give EXP
    pc_gainexp(sd, &md->bl, base_exp, job_exp, false);
}
```

---

## Custom Player Stats

### **Goal**: Add a custom stat that increases with level

---

### **Step 1: Add Stat Field**

**In src/map/pc.hpp** (in `struct map_session_data`):

```cpp
struct map_session_data {
    // ... existing fields ...

    struct {
        int hp, sp;
        int atk, matk;
        // ... existing stats ...

        // *** Custom stat ***
        int custom_power;  // Increases with level
    } status;
};
```

---

### **Step 2: Calculate Custom Stat**

**In src/map/status.cpp** (in `status_calc_pc_` function):

```cpp
int status_calc_pc_(struct map_session_data* sd, enum e_status_calc_opt opt) {
    // ... existing calculations ...

    // *** Calculate custom power stat ***
    sd->status.custom_power = sd->status.base_level * 10;

    // Add bonus from equipment
    sd->status.custom_power += sd->bonus.custom_damage;

    // ... rest of function ...
}
```

---

### **Step 3: Use Custom Stat**

**In src/map/battle.cpp** (damage calculation):

```cpp
static struct Damage battle_calc_weapon_attack(...) {
    // ... existing calculations ...

    // *** Add custom power to damage ***
    if (sd) {
        wd.damage += sd->status.custom_power;
    }

    return wd;
}
```

---

### **Step 4: Display Custom Stat (Script Command)**

**In src/custom/script.inc**:

```cpp
/**
 * getcustompower()
 * Get player's custom power stat
 */
BUILDIN_FUNC(getcustompower)
{
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) {
        script_pushint(st, 0);
        return 1;
    }

    script_pushint(st, sd->status.custom_power);
    return 0;
}
```

**Usage**:
```c
mes "Your Custom Power: " + getcustompower();
```

---

## Custom Level Cap

### **Goal**: Increase max level from 99 to 150

---

### **Step 1: Modify Constants**

**In src/config/core.hpp** (or defines_post.hpp):

```cpp
// *** Original ***
// #define MAX_LEVEL 99

// *** Modified ***
#define MAX_LEVEL 150
#define MAX_JOB_LEVEL 70  // Also increase job level
```

---

### **Step 2: Update EXP Tables**

**In db/re/exp_table.yml**:

```yaml
BaseExpTable:
  MaxLevel: 150
  Exp:
    - 0
    - 9
    - 16
    # ... continue up to level 150 ...
    - 999999999  # Level 149→150 (set appropriate exp)

JobExpTable:
  MaxLevel: 70
  Exp:
    - 0
    - 50
    # ... continue up to job level 70 ...
```

---

### **Step 3: Update Skill Points**

**In src/map/pc.cpp** (in `pc_levelup` function):

```cpp
int pc_levelup(struct map_session_data *sd) {
    // ... existing code ...

    // *** Grant skill points per level ***
    sd->status.skill_point += 1;  // 1 point per level (default)

    // OR custom progression:
    if (sd->status.base_level <= 50) {
        sd->status.skill_point += 1;  // 1 point for levels 1-50
    } else if (sd->status.base_level <= 100) {
        sd->status.skill_point += 2;  // 2 points for levels 51-100
    } else {
        sd->status.skill_point += 3;  // 3 points for levels 101-150
    }

    // ... rest of function ...
}
```

---

## Custom Equipment Slots

### **Goal**: Add a new equipment slot (e.g., "Talisman" slot)

---

### **Step 1: Define Slot Constant**

**In src/common/mmo.hpp** (in `enum equip_index`):

```cpp
enum equip_index {
    EQI_COMPOUND_ON = -1,
    EQI_ACC_L = 0,
    EQI_ACC_R,
    EQI_SHOES,
    EQI_GARMENT,
    EQI_HEAD_LOW,
    EQI_HEAD_MID,
    EQI_HEAD_TOP,
    EQI_ARMOR,
    EQI_HAND_L,
    EQI_HAND_R,
    EQI_COSTUME_TOP,
    EQI_COSTUME_MID,
    EQI_COSTUME_LOW,
    EQI_COSTUME_GARMENT,
    EQI_AMMO,
    EQI_SHADOW_ARMOR,
    EQI_SHADOW_WEAPON,
    EQI_SHADOW_SHIELD,
    EQI_SHADOW_SHOES,
    EQI_SHADOW_ACC_R,
    EQI_SHADOW_ACC_L,

    // *** Custom slot ***
    EQI_CUSTOM_TALISMAN,

    EQI_MAX
};
```

---

### **Step 2: Update Equip Positions**

**In src/common/mmo.hpp** (in `enum equip_pos`):

```cpp
enum equip_pos {
    EQP_HEAD_LOW       = 0x000001,
    EQP_HEAD_MID       = 0x000200,
    EQP_HEAD_TOP       = 0x000100,
    // ... existing positions ...

    // *** Custom talisman slot (use unused bit) ***
    EQP_CUSTOM_TALISMAN = 0x400000,
};
```

---

### **Step 3: Update Equipment Functions**

**In src/map/pc.cpp** (in equipment-related functions):

```cpp
// In pc_equipitem(), pc_unequipitem(), etc., add handling for new slot
```

---

### **Step 4: Create Items for Slot**

**In db/re/item_db.yml**:

```yaml
- Id: 60100
  AegisName: PowerTalisman
  Name: "Power Talisman"
  Type: Armor
  Locations:
    Custom_Talisman: true  # New location
  Script: |
    bonus bAtk,50;
    bonus bMatk,50;
```

**Note**: This requires client-side modifications to display the new slot!

---

## Testing Your Modifications

### **Step 1: Compile**

```bash
cd build
cmake .. -DCMAKE_BUILD_TYPE=Debug  # Use Debug for easier testing
make -j$(nproc)
make install
```

---

### **Step 2: Run Server**

```bash
cd ..
./map-server
```

---

### **Step 3: Test with GM Commands**

```
@job 0  # Change job
@blevel 99  # Set base level
@jlevel 50  # Set job level
@allskill  # Get all skills
@item 60000 1  # Get custom item
@equip 60000  # Equip item
@monster 1002 1  # Spawn Poring
@stats  # Check stats
@mi 1002  # Check monster info
```

---

### **Step 4: Test Specific Features**

**Damage Test**:
```
@blevel 99
@str 99
@monster 1002 1
# Attack Poring, observe damage
```

**Drop Test**:
```
@dropall  # Drop all items
@monster 1002 100  # Spawn 100 Porings
@killmonster2  # Kill all monsters
# Check dropped items
```

**EXP Test**:
```
@blevel 1
@monster 1002 1
# Kill Poring, check EXP gain
```

---

### **Step 5: Debug Issues**

**Check console output**:
```
[Debug]: pc_bonus: unknown type 10000 100
[Error]: skill 10001 not found in database
```

**Add debug logging**:
```cpp
ShowDebug("Custom damage bonus: %d\n", sd->bonus.custom_damage);
ShowInfo("Applying skill %d, level %d\n", skill_id, skill_lv);
```

**Use GDB** (if crashes):
```bash
gdb ./map-server
(gdb) run
# ... crash ...
(gdb) bt
```

---

## Related References

- **Source Code Structure**: [KB_REF_SourceCodeStructure.md]
- **Database Work**: [KB_REF_DatabaseCPP.md]
- **Compilation/Debugging**: [KB_REF_CompilationDebugging.md]
- **Best Practices**: [KB_REF_SourceCodeBestPractices.md]

---

**End of KB_REF_028 - Common Source Code Modifications**
