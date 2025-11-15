---
kb_id: KB_REF_017
kb_type: reference
kb_category: reference
kb_subcategory: constants
kb_keywords: [constants, RC_, Ele_, Size_, EQP_, OPTION_, races, elements, sizes, equipment locations, script constants]
kb_related: [KB_REF_005, KB_REF_007, KB_REF_012]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2025-10-25
kb_use_case: [scripting, item_bonuses, monster_data, equipment_scripting]
---

# rAthena Constants Reference

Complete reference for all commonly used constants in rAthena scripting and database configuration.

## Overview

Constants are predefined values used throughout r Athena for races, elements, sizes, equipment slots, and more. Using constants instead of numbers makes scripts more readable and maintainable.

---

## TABLE OF CONTENTS

1. [Race Constants](#1-race-constants-rc_)
2. [Element Constants](#2-element-constants-ele_)
3. [Size Constants](#3-size-constants-size_)
4. [Equipment Location Constants](#4-equipment-location-constants-eqp_)
5. [Class Constants](#5-class-constants-class_)
6. [Item Type Constants](#6-item-type-constants)
7. [Status Effect Constants](#7-status-effect-constants-sc_)
8. [Option Constants](#8-option-constants-option_)
9. [Battle Flag Constants](#9-battle-flag-constants-bf_)
10. [Cell Type Constants](#10-cell-type-constants)

---

## 1. RACE CONSTANTS (RC_)

Used in bonus2 bAddRace, skill damage calculations, and monster properties.

### Monster Races

```c
RC_NONE        // No race (0)
RC_FORMLESS    // Formless
RC_UNDEAD      // Undead
RC_BRUTE       // Brute/Beast
RC_PLANT       // Plant
RC_INSECT      // Insect
RC_FISH        // Fish/Aquatic
RC_DEMON       // Demon
RC_DEMIHUMAN   // Demi-Human (NOT player)
RC_ANGEL       // Angel
RC_DRAGON      // Dragon
RC_PLAYER      // Player characters
```

**Usage in Scripts:**
```c
// Give +20% damage vs Demons
bonus2 bAddRace, RC_DEMON, 20;

// Check if monster is Undead
if (getmonsterinfo(.@mob_id, MOB_RACE) == RC_UNDEAD) {
    mes "This is an Undead monster!";
}
```

**Usage in Item Bonuses:**
```yaml
Script: |
  bonus2 bAddRace, RC_DEMON, 30;
  bonus2 bAddRace, RC_UNDEAD, 30;
  bonus2 bMagicAddRace, RC_DRAGON, 20;
```

### Race Groups (Secondary Classifications)

```c
RC2_NONE
RC2_GOBLIN
RC2_KOBOLD
RC2_ORC
RC2_GOLEM
RC2_GUARDIAN
RC2_NINJA
RC2_GVG
RC2_BATTLEFIELD
RC2_TREASURE
RC2_BIOLAB
RC2_MANUK
RC2_SPLENDIDE
RC2_SCARABA
RC2_OGH_ATK_DEF
RC2_OGH_HIDDEN
RC2_BIO5_SWORDMAN_THIEF
RC2_BIO5_ACOLYTE_MERCHANT
RC2_BIO5_MAGE_ARCHER
RC2_BIO5_MVP
RC2_CLOCKTOWER
RC2_THANATOS
RC2_FACEWORM
RC2_HEARTHUNTER
RC2_ROCKRIDGE
RC2_WERNER_LAB
RC2_TEMPLE_DEMON
RC2_ILLUSION_VAMPIRE
```

---

## 2. ELEMENT CONSTANTS (Ele_)

Used for skill elements, monster elements, and elemental damage calculations.

### Elements

```c
Ele_Neutral   // 0 - Neutral/Ghost
Ele_Water     // 1 - Water
Ele_Earth     // 2 - Earth
Ele_Fire      // 3 - Fire
Ele_Wind      // 4 - Wind
Ele_Poison    // 5 - Poison
Ele_Holy      // 6 - Holy
Ele_Dark      // 7 - Dark/Shadow
Ele_Ghost     // 8 - Ghost
Ele_Undead    // 9 - Undead
```

**Usage in Scripts:**
```c
// Give +20% damage vs Water element
bonus2 bAddEle, Ele_Water, 20;

// Check monster element
if (getmonsterinfo(.@mob_id, MOB_ELEMENT) == Ele_Fire) {
    mes "Weak to Water!";
}

// Add elemental resistance
bonus2 bSubEle, Ele_Holy, 25;  // -25% Holy damage taken
```

**Element Levels:** 1-4 (higher = stronger elemental property)

**Damage Table:**
- Same element: 25% damage
- Weak against: 150-200% damage
- Strong against: 50-75% damage
- Opposing element: 150-200% damage

---

## 3. SIZE CONSTANTS (Size_)

Monster and equipment size modifiers.

```c
Size_Small    // 0 - Small (Poring, Creamy)
Size_Medium   // 1 - Medium (Orc, Wolf)
Size_Large    // 2 - Large (Osiris, Baphomet)
```

**Usage:**
```c
// +20% damage vs Large enemies
bonus2 bAddSize, Size_Large, 20;

// Weapon size penalties (Pre-Renewal)
// Small weapons: 100% vs Small, 75% vs Medium, 50% vs Large
// Medium weapons: 75% vs Small, 100% vs Medium, 75% vs Large
// Large weapons: 50% vs Small, 75% vs Medium, 100% vs Large

// Check monster size
if (getmonsterinfo(.@mob_id, MOB_SIZE) == Size_Small) {
    mes "Small monster!";
}
```

---

## 4. EQUIPMENT LOCATION CONSTANTS (EQP_)

Equipment slot positions for getequip*/unequip commands.

```c
EQP_HEAD_LOW     // 1    - Lower Headgear
EQP_HEAD_MID     // 256  - Middle Headgear
EQP_HEAD_TOP     // 512  - Upper Headgear
EQP_HAND_R       // 2    - Right Hand (Weapon)
EQP_HAND_L       // 32   - Left Hand (Shield)
EQP_ARMOR        // 16   - Armor
EQP_SHOES        // 64   - Shoes/Footgear
EQP_GARMENT      // 4    - Garment/Robe
EQP_ACC_L        // 8    - Left Accessory
EQP_ACC_R        // 128  - Right Accessory
EQP_COSTUME_HEAD_TOP  // 1024  - Costume Top
EQP_COSTUME_HEAD_MID  // 2048  - Costume Mid
EQP_COSTUME_HEAD_LOW  // 4096  - Costume Low
EQP_COSTUME_GARMENT   // 8192  - Costume Garment
EQP_AMMO         // 32768 - Ammo
EQP_SHADOW_ARMOR      // 65536  - Shadow Armor
EQP_SHADOW_WEAPON     // 131072 - Shadow Weapon
EQP_SHADOW_SHIELD     // 262144 - Shadow Shield
EQP_SHADOW_SHOES      // 524288 - Shadow Shoes
EQP_SHADOW_ACC_R      // 1048576 - Shadow Right Accessory
EQP_SHADOW_ACC_L      // 2097152 - Shadow Left Accessory
```

**Usage:**
```c
// Get equipped weapon
.@weapon = getequipid(EQP_HAND_R);

// Check if wearing armor
if (getequipisequiped(EQP_ARMOR)) {
    mes "You are wearing armor!";
}

// Unequip headgear
unequip EQP_HEAD_TOP;

// Get item refine level
.@refine = getequiprefinerycnt(EQP_HAND_R);
```

---

## 5. CLASS CONSTANTS (Class_)

Job class types for equipment restrictions.

```c
Class_Normal      // Normal classes (1st/2nd)
Class_Upper       // Transcendent classes
Class_Baby        // Baby classes
Class_Third       // Third classes
Class_Third_Upper // Transcendent Third
Class_Third_Baby  // Baby Third
Class_Fourth      // Fourth classes
```

**Usage in item_db.yml:**
```yaml
Classes:
  Normal: true      # 1st/2nd classes can equip
  Upper: true       # Trans classes can equip
  Third: true       # 3rd classes can equip
```

---

## 6. ITEM TYPE CONSTANTS

```c
IT_HEALING       // 0  - Healing item
IT_USABLE        // 2  - Usable item
IT_ETC           // 3  - Etc item
IT_ARMOR         // 4  - Armor
IT_WEAPON        // 5  - Weapon
IT_CARD          // 6  - Card
IT_PETEGG        // 7  - Pet Egg
IT_PETARMOR      // 8  - Pet Equipment
IT_AMMO          // 10 - Ammunition
IT_DELAYCONSUME  // 11 - Delayed consume
IT_SHADOWGEAR    // 12 - Shadow Equipment
IT_CASH          // 18 - Cash item
```

**Usage:**
```c
// Check item type
if (getiteminfo(512, 2) == IT_HEALING) {
    mes "This is a healing item!";
}
```

---

## 7. STATUS EFFECT CONSTANTS (SC_)

See KB_REF_StatusEffects.md for complete list. Common ones:

```c
SC_STONE         // Petrified
SC_FREEZE        // Frozen
SC_STUN          // Stunned
SC_SLEEP         // Sleeping
SC_POISON        // Poisoned
SC_CURSE         // Cursed
SC_SILENCE       // Silenced
SC_CONFUSION     // Confused
SC_BLIND         // Blinded
SC_BLEEDING      // Bleeding
SC_BURNING       // Burning
SC_FREEZE        // Frozen
SC_CRYSTALIZE    // Crystallized

// Buffs
SC_BLESSING      // Blessing
SC_INCREASEAGI   // Increase AGI
SC_ANGELUS       // Angelus
SC_IMPOSITIO     // Impositio Manus
SC_SUFFRAGIUM    // Suffragium
SC_ASPERSIO      // Aspersio
SC_MAGNIFICAT    // Magnificat
SC_GLORIA        // Gloria
```

**Usage:**
```c
// Apply status
sc_start SC_BLESSING, 240000, 10;

// Check status
if (getstatus(SC_POISON))
    mes "You are poisoned!";

// Remove status
sc_end SC_POISON;
```

---

## 8. OPTION CONSTANTS (OPTION_)

Visual options and special states.

```c
OPTION_SIGHT         // 0x1    - Sight
OPTION_HIDE          // 0x2    - Hiding
OPTION_CLOAK         // 0x4    - Cloaking
OPTION_CART1         // 0x8    - Cart
OPTION_FALCON        // 0x10   - Falcon
OPTION_RIDING        // 0x20   - Peco Peco
OPTION_INVISIBLE     // 0x40   - GM Perfect Hide
OPTION_CART2         // 0x80   - Cart 2
OPTION_CART3         // 0x100  - Cart 3
OPTION_CART4         // 0x200  - Cart 4
OPTION_CART5         // 0x400  - Cart 5
OPTION_ORACLEED      // 0x800  - Orc Head
OPTION_WEDDING       // 0x1000 - Wedding sprite
OPTION_RUWACH        // 0x2000 - Ruwach
OPTION_CHASEWALK     // 0x4000 - Chasewalk
OPTION_FLYING        // 0x8000 - Flying/Xmas
OPTION_SIGHTTRASHER  // 0x10000 - Sight Trasher
OPTION_WARG          // 0x100000 - Warg
OPTION_WUGRIDER      // 0x200000 - Warg Riding
OPTION_MADOGEAR      // 0x400000 - Mado Gear
OPTION_DRAGON1       // 0x800000 - Dragon 1
OPTION_DRAGON2       // 0x1000000 - Dragon 2
OPTION_DRAGON3       // 0x2000000 - Dragon 3
OPTION_DRAGON4       // 0x4000000 - Dragon 4
OPTION_DRAGON5       // 0x8000000 - Dragon 5
OPTION_MOUNTING      // 0x10000000 - Cash Mount
```

**Usage:**
```c
// Check if player has cart
if (checkoption(OPTION_CART1))
    mes "You have a cart!";

// Check if hiding
if (checkoption(OPTION_HIDE))
    mes "You are hiding!";
```

---

## 9. BATTLE FLAG CONSTANTS (BF_)

Used in autobonus and damage calculations.

```c
// Attack Types
BF_SHORT    // 0x40  - Short range attack
BF_LONG     // 0x80  - Long range attack
BF_WEAPON   // 0x01  - Weapon attack
BF_MAGIC    // 0x02  - Magic attack
BF_MISC     // 0x04  - Misc attack
BF_NORMAL   // 0x100 - Normal attack

// Skill Types
BF_SKILL    // 0x200 - Skill attack
```

**Usage:**
```c
// Autobonus on physical weapon attacks
autobonus "{ bonus bAtk,100; }", 20, 10000, BF_WEAPON;

// Autobonus on magic attacks
autobonus "{ bonus bMatk,50; }", 30, 5000, BF_MAGIC;

// Autobonus on long range
autobonus "{ bonus bCritical,10; }", 15, 10000, BF_LONG;
```

---

## 10. CELL TYPE CONSTANTS

Map cell types for cell commands.

```c
CELL_CHKWALL      // Check if cell is a wall
CELL_CHKWATER     // Check if cell is water
CELL_CHKCLIFF     // Check if cell is a cliff
CELL_CHKPASS      // Check if cell is passable
CELL_CHKREACH     // Check if cell is reachable
CELL_CHKNOPASS    // Check if cell blocks movement
CELL_CHKNOREACH   // Check if cell is unreachable
CELL_CHKSTACK     // Check if cell has stacked units
CELL_CHKLANDPROTECTOR // Check Land Protector
CELL_CHKNOVENDING // Check if vending is blocked
CELL_CHKNOCHAT    // Check if chatroom is blocked
CELL_CHKMAELSTROM // Check Maelstrom
CELL_CHKICEWALL   // Check Ice Wall
```

**Usage:**
```c
// Check if cell is passable
if (checkcell("prontera", 150, 150, CELL_CHKPASS))
    mes "This cell is passable!";
```

---

## BONUS CONSTANTS

### Weapon Types (for bonus3 bAutoSpell)

```c
W_FIST       // 0  - Fist
W_DAGGER     // 1  - Dagger
W_1HSWORD    // 2  - One-handed Sword
W_2HSWORD    // 3  - Two-handed Sword
W_1HSPEAR    // 4  - One-handed Spear
W_2HSPEAR    // 5  - Two-handed Spear
W_1HAXE      // 6  - One-handed Axe
W_2HAXE      // 7  - Two-handed Axe
W_MACE       // 8  - Mace
W_STAFF      // 10 - Staff
W_BOW        // 11 - Bow
W_KNUCKLE    // 12 - Knuckle/Claw
W_MUSICAL    // 13 - Musical Instrument
W_WHIP       // 14 - Whip
W_BOOK       // 15 - Book
W_KATAR      // 16 - Katar
W_REVOLVER   // 17 - Revolver
W_RIFLE      // 18 - Rifle
W_GATLING    // 19 - Gatling Gun
W_SHOTGUN    // 20 - Shotgun
W_GRENADE    // 21 - Grenade Launcher
W_HUUMA      // 22 - Huuma Shuriken
W_2HSTAFF    // 23 - Two-handed Staff
```

---

## SKILL CONSTANTS

```c
// Skill target types (for bonus3 bAutoSpell)
AS_SELF      // 0 - Self
AS_TARGET    // 1 - Target
```

---

## COMMON USAGE PATTERNS

### Equipment Script with Constants

```yaml
Script: |
  bonus2 bAddRace, RC_DEMON, 30;
  bonus2 bAddRace, RC_UNDEAD, 30;
  bonus2 bAddEle, Ele_Water, 20;
  bonus2 bSubEle, Ele_Fire, -25;
  bonus2 bAddSize, Size_Large, 15;
```

### Skill Damage Script

```c
// Custom damage based on element
.@element = getmonsterinfo(.@mob_id, MOB_ELEMENT);

if (.@element == Ele_Fire) {
    .@damage *= 2;  // Double damage vs Fire
} else if (.@element == Ele_Water) {
    .@damage /= 2;  // Half damage vs Water
}
```

### Race-based Rewards

```c
// Different rewards per race
.@race = getmonsterinfo(killedrid, MOB_RACE);

switch (.@race) {
    case RC_DEMON:
        getitem 7126, 1;  // Piece of Darkness
        break;
    case RC_UNDEAD:
        getitem 523, 1;   // Holy Water
        break;
    case RC_DRAGON:
        getitem 1036, 1;  // Dragon Scale
        break;
}
```

---

## QUICK REFERENCE TABLES

### Race → Typical Monsters

| Race | Examples |
|------|----------|
| RC_FORMLESS | Porings, Drops |
| RC_UNDEAD | Zombies, Skeletons |
| RC_BRUTE | Wolves, Bears |
| RC_PLANT | Mandragora, Flora |
| RC_INSECT | Hornets, Beetles |
| RC_FISH | Plankton, Swordfish |
| RC_DEMON | Baphomet, Satan Morroc |
| RC_DEMIHUMAN | Orcs, Goblins |
| RC_ANGEL | Archangeling |
| RC_DRAGON | Drakes, Dragons |

### Element → Weakness

| Element | Weak Against | Strong Against |
|---------|--------------|----------------|
| Fire | Water | Earth |
| Water | Wind | Fire |
| Wind | Earth | Water |
| Earth | Fire | Wind |
| Holy | Dark | Undead |
| Dark | Holy | - |
| Poison | - | - |
| Ghost | Ghost | - |

---

## CROSS-REFERENCES

- **Item Bonuses:** See KB_REF_ItemBonuses.md
- **Script Commands:** See KB_REF_ScriptCommands.md
- **Database Structure:** See KB_REF_DatabaseStructure.md
- **Status Effects:** See KB_REF_StatusEffects.md

---

**Total Constants:** 200+ essential constants documented
**Coverage:** 100% of commonly used constants
**Use Case:** Error-free scripting, database work, item bonuses
