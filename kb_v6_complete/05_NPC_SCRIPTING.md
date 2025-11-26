# rAthena KB v6.1 - NPC Scripting & Database Reference

**Version:** 6.1 Validated
**Source:** npc/*.txt, db/re/*.yml

---

## Quick Navigation

### NPC Patterns
- [Basic NPC Structure](#basic-npc-structure)
- [Shop NPCs](#shop-npcs)
- [Warp NPCs](#warp-npcs)
- [Quest NPCs](#quest-npcs)
- [Daily Reward NPCs](#daily-reward-npcs)
- [Instance NPCs](#instance-npcs)
- [State Machine Patterns](#state-machine-patterns)
- [Event System Hooks](#event-system-hooks)

### Database Schemas
- [item_db.yml](#item_dbyml)
- [skill_db.yml](#skill_dbyml)
- [mob_db.yml](#mob_dbyml)
- [quest_db.yml](#quest_dbyml)

---

# PART 1: NPC PATTERNS

## Basic NPC Structure

<!-- RAG_CHUNK: npc_basic_structure -->

### NPC Definition Format
```c
// Format: <map>,<x>,<y>,<dir>	script	<NPC Name>	<sprite>,{
prontera,155,183,4	script	Guide	4_M_JOB_KNIGHT,{
    mes "[Guide]";
    mes "Welcome to Prontera!";
    close;
}
```

### NPC Sprites
| Sprite ID | Description |
|-----------|-------------|
| 4_M_JOB_KNIGHT | Male Knight NPC |
| 4_F_JOB_PRIEST | Female Priest NPC |
| 1_M_JOBGUIDER | Job Guide NPC |
| HIDDEN_NPC | Invisible NPC |

### Directions
| Dir | Direction |
|-----|-----------|
| 0 | South |
| 2 | West |
| 4 | North |
| 6 | East |

---

## Shop NPCs

<!-- RAG_CHUNK: npc_shop_patterns -->

### Basic Item Shop
```c
prontera,150,180,4	shop	Weapon Dealer	4_M_JOB_BLACKSMITH,1201:1000,1202:1500
// Format: itemID:price,itemID:price,...
// Use -1 for item_db price
```

### Dynamic Shop
```c
prontera,152,180,4	script	Custom Shop	4_M_MERCHANT,{
    mes "[Merchant]";
    mes "Welcome!";
    next;
    callshop "dynamic_shop", 1;
    end;
}
-	shop	dynamic_shop	-1,501:50,502:100
```

### Cash Shop
```c
prontera,160,180,4	cashshop	Cash Shop	4_M_MANAGER,12103:500,12104:750
// Uses #CASHPOINTS currency
```

---

## Warp NPCs

<!-- RAG_CHUNK: npc_warp_patterns -->

### Basic Warp
```c
prontera,150,180,0	warp	prt_warp1	2,2,geffen,120,100
```

### Conditional Warp
```c
prontera,155,185,4	script	Dungeon Gate	WARPNPC,{
    if (BaseLevel < 50) {
        mes "You need Base Level 50+";
        close;
    }
    if (Zeny < 1000) {
        mes "Entry fee: 1,000 Zeny";
        close;
    }
    Zeny -= 1000;
    close2;
    warp "pay_dun00", 100, 100;
    end;
}
```

---

## Quest NPCs

<!-- RAG_CHUNK: npc_quest_patterns -->

### Kill Quest
```c
prontera,160,190,4	script	Hunt Master	4_M_JOB_HUNTER,{
    switch(checkquest(1000)) {
        case -1:  // Not started
            mes "Kill 50 Porings. Accept?";
            next;
            if (select("Accept:Decline") == 1) {
                setquest 1000;
                mes "Come back when done.";
            }
            close;
        case 0:
        case 1:  // In progress
            if (checkquest(1000, HUNTING) == 2) {
                completequest 1000;
                getitem 501, 10;
                getexp 1000, 500;
                mes "Well done!";
            } else {
                mes "Keep hunting!";
            }
            close;
        case 2:  // Completed
            mes "Thanks for your help!";
            close;
    }
}
```

### Collection Quest
```c
prontera,162,190,4	script	Collector	4_M_JOB_WIZARD,{
    if (COLLECT_QUEST == 0) {
        mes "Bring me 20 Jellopy!";
        next;
        if (select("OK:No") == 1) COLLECT_QUEST = 1;
        close;
    }
    if (COLLECT_QUEST == 1) {
        if (countitem(909) >= 20) {
            delitem 909, 20;
            getitem 501, 50;
            COLLECT_QUEST = 2;
            mes "Thank you!";
        } else {
            mes "Need " + (20 - countitem(909)) + " more.";
        }
        close;
    }
    mes "Thanks for the help!";
    close;
}
```

---

## Daily Reward NPCs

<!-- RAG_CHUNK: npc_daily_patterns -->

### Daily Login Reward
```c
prontera,170,190,4	script	Daily NPC	4_F_JOB_PRIEST,{
    if (DAILY_REWARD == gettimetick(2) / 86400) {
        mes "Already claimed today!";
        close;
    }
    DAILY_REWARD = gettimetick(2) / 86400;
    getitem 501, 10;
    mes "Here's your daily reward!";
    close;
}
```

### Weekly Streak Bonus
```c
prontera,172,190,4	script	Weekly Bonus	4_M_MANAGER,{
    .@week = gettimetick(2) / 604800;
    if (WEEKLY_CLAIM == .@week) {
        mes "Already claimed this week!";
        close;
    }
    if (WEEKLY_CLAIM == .@week - 1)
        WEEKLY_STREAK++;
    else
        WEEKLY_STREAK = 1;
    WEEKLY_CLAIM = .@week;
    .@bonus = min(WEEKLY_STREAK, 4);
    getitem 607, 5 * .@bonus;
    mes "Week " + WEEKLY_STREAK + " streak!";
    close;
}
```

---

## Instance NPCs

<!-- RAG_CHUNK: npc_instance_patterns -->

```c
prontera,180,190,4	script	Instance Guide	4_M_JOB_KNIGHT,{
    switch(select("Create:Enter:Cancel")) {
        case 1:
            if (getcharid(1) == 0) {
                mes "Need a party!";
                close;
            }
            if (getcharid(0) != getpartyleader(getcharid(1), 2)) {
                mes "Party leader only!";
                close;
            }
            if (instance_create("My_Instance", getcharid(1)) < 0) {
                mes "Creation failed!";
                close;
            }
            mes "Instance created!";
            close;
        case 2:
            if (has_instance("My_Instance") == "") {
                mes "No instance found!";
                close;
            }
            close2;
            warp "My_Instance", 50, 50;
            end;
    }
    close;
}
```

---

## State Machine Patterns

<!-- RAG_CHUNK: npc_state_machine -->

```c
prontera,185,190,4	script	Epic Quest	4_M_JOB_KNIGHT,{
    switch(EPIC_QUEST_STATE) {
        case 0:  // Not started
            mes "Begin the epic quest?";
            if (select("Yes:No") == 1) {
                EPIC_QUEST_STATE = 1;
                mes "Find the Ancient Sword!";
            }
            close;
        case 1:  // Find item
            if (countitem(1234) > 0) {
                delitem 1234, 1;
                EPIC_QUEST_STATE = 2;
                mes "Now slay the Dragon!";
            } else {
                mes "Keep searching!";
            }
            close;
        case 2:  // Kill boss
            if (DRAGON_KILLED) {
                getitem 7227, 1;
                EPIC_QUEST_STATE = 3;
                mes "You are a hero!";
            } else {
                mes "Slay the Dragon!";
            }
            close;
        case 3:  // Done
            mes "Thanks, hero!";
            close;
    }
}
```

---

## Event System Hooks

<!-- RAG_CHUNK: npc_event_hooks -->

| Event | Trigger |
|-------|---------|
| OnPCLoginEvent | Player logs in |
| OnPCLogoutEvent | Player logs out |
| OnPCLoadMapEvent | Player enters map |
| OnPCKillEvent | Player kills player |
| OnNPCKillEvent | Player kills monster |
| OnPCDieEvent | Player dies |

### Example
```c
-	script	EventHandler	FAKE_NPC,{
    end;
OnPCLoginEvent:
    announce "Welcome " + strcharinfo(0) + "!", bc_self;
    end;
OnNPCKillEvent:
    if (killedrid == 1002) // Poring
        PORING_KILLS++;
    end;
}
```

---

# PART 2: DATABASE SCHEMAS

## item_db.yml

<!-- RAG_CHUNK: db_item -->

*Source: db/re/item_db.yml*

```yaml
Header:
  Type: ITEM_DB
  Version: 3

Body:
  - Id: 501
    AegisName: "Red_Potion"
    Name: "Red Potion"
    Type: Healing
    Buy: 50
    Sell: 10
    Weight: 70

    Jobs:
      All: true

    Classes:
      All: true

    Locations:
      Head_Top: true
      Armor: true
      Right_Hand: true
      Garment: true
      Shoes: true
      Right_Accessory: true
      Left_Accessory: true

    WeaponLevel: 1
    EquipLevelMin: 1
    Refineable: true

    Flags:
      BuyingStore: false
      UniqueId: true
      BindOnEquip: false

    Trade:
      NoDrop: false
      NoTrade: false
      NoSell: false

    Script: |
      itemheal 45,0;

    EquipScript: |
      bonus bStr,1;
```

### Item Types
| Type | Description |
|------|-------------|
| Healing | Consumables |
| Usable | Usable items |
| Etc | Misc items |
| Armor | Equipment |
| Weapon | Weapons |
| Card | Cards |
| Ammo | Ammunition |

### Weapon SubTypes
| SubType | Description |
|---------|-------------|
| Dagger | Daggers |
| 1hSword | One-handed swords |
| 2hSword | Two-handed swords |
| 1hSpear | One-handed spears |
| 2hSpear | Two-handed spears |
| 1hAxe | One-handed axes |
| 2hAxe | Two-handed axes |
| Mace | Maces |
| Staff | Staves |
| Bow | Bows |
| Knuckle | Knuckles |
| Katar | Katars |

---

## skill_db.yml

<!-- RAG_CHUNK: db_skill -->

*Source: db/re/skill_db.yml*

```yaml
Header:
  Type: SKILL_DB
  Version: 3

Body:
  - Id: 1
    Name: "NV_BASIC"
    Description: "Basic Skill"
    MaxLevel: 9
    Type: None
    TargetType: Self

    DamageFlags:
      Splash: false
      IgnoreDefense: false
      Critical: false

    Range:
      - Level: 1
        Size: 0

    CastTime:
      - Level: 1
        Time: 0

    Cooldown:
      - Level: 1
        Time: 0

    Requires:
      SpCost:
        - Level: 1
          Amount: 0
      ItemCost:
        - Item: Red_Gemstone
          Amount: 1
```

---

## mob_db.yml

<!-- RAG_CHUNK: db_mob -->

*Source: db/re/mob_db.yml*

```yaml
Header:
  Type: MOB_DB
  Version: 3

Body:
  - Id: 1002
    AegisName: "PORING"
    Name: "Poring"
    Level: 1
    Hp: 50
    BaseExp: 2
    JobExp: 1
    Attack: 7
    Attack2: 10
    Defense: 0
    Size: Small
    Race: Plant
    Element: Water
    ElementLevel: 1
    Ai: 02
    Class: Normal

    Modes:
      CanMove: true
      Looter: true
      Aggressive: false

    Drops:
      - Item: Jellopy
        Rate: 7000
      - Item: Poring_Card
        Rate: 1
```

### Monster Races
| Race | ID |
|------|-----|
| Formless | 0 |
| Undead | 1 |
| Brute | 2 |
| Plant | 3 |
| Insect | 4 |
| Fish | 5 |
| Demon | 6 |
| DemiHuman | 7 |
| Angel | 8 |
| Dragon | 9 |

### AI Types
| AI | Behavior |
|----|----------|
| 01 | Passive |
| 02 | Passive, looter |
| 04 | Aggressive |
| 07 | Boss |
| 21 | Boss, aggressive |

---

## quest_db.yml

<!-- RAG_CHUNK: db_quest -->

*Source: db/re/quest_db.yml*

```yaml
Header:
  Type: QUEST_DB
  Version: 2

Body:
  - Id: 1000
    Title: "Hunt Porings"
    TimeLimit: 86400

    Targets:
      - Mob: PORING
        Count: 10

    Drops:
      - Mob: PORING
        Item: Jellopy
        Count: 5
        Rate: 5000
```

---

*rAthena KB v6.1 - NPC Scripting & Database Reference*
