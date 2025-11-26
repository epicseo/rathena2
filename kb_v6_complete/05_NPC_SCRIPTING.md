# rAthena KB v6.1 - NPC Scripting & Database Reference

**Version:** 6.1 Validated
**Source:** npc/*.txt, db/re/*.yml

---

# PART 1: NPC PATTERNS


## Quick Navigation

- [Basic NPC Structure](#basic-npc-structure)
- [Shop NPCs](#shop-npcs)
- [Warp NPCs](#warp-npcs)
- [Quest NPCs](#quest-npcs)
- [Event NPCs](#event-npcs)
- [Instance NPCs](#instance-npcs)
- [Daily Reward NPCs](#daily-reward-npcs)
- [State Machine Patterns](#state-machine-patterns)
- [Common Techniques](#common-techniques)

---

## Basic NPC Structure

<!-- RAG_CHUNK: npc_basic_structure -->

### NPC Definition Format
```c
// Format: <map>,<x>,<y>,<dir><TAB>script<TAB><NPC Name><TAB><sprite>,{
<map>,<x>,<y>,<dir>	script	<NPC Name>	<sprite>,{
    // Script content here
}

// Example:
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
| 4_M_JOB_BLACKSMITH | Male Blacksmith NPC |
| 1_M_JOBGUIDER | Job Guide NPC |
| 4_M_MANAGER | Manager NPC |
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
prontera,150,180,4	shop	Weapon Dealer	4_M_JOB_BLACKSMITH,1201:1000,1202:1500,1203:2000

// Format: itemID:price,itemID:price,...
// Use -1 for price to use item_db price
```

### Dynamic Shop (Script-controlled)
```c
prontera,152,180,4	script	Custom Shop	4_M_MERCHANT,{
    mes "[Merchant]";
    mes "Welcome! What would you like to buy?";
    next;
    
    // Create dynamic shop
    setarray .@items[0], 501, 502, 503, 504;  // Item IDs
    setarray .@prices[0], 50, 100, 200, 500;  // Prices
    
    callshop "dynamic_shop", 1;
    end;
    
OnSellItem:
    // Custom sell logic
    end;
}

-	shop	dynamic_shop	-1,501:50,502:100,503:200,504:500
```

### Cash Shop
```c
prontera,160,180,4	cashshop	Cash Shop	4_M_MANAGER,12103:500,12104:750,12105:1000
// Uses #CASHPOINTS currency
```

---

## Warp NPCs

<!-- RAG_CHUNK: npc_warp_patterns -->

### Basic Warp Portal
```c
prontera,150,180,0	warp	prt_warp1	2,2,geffen,120,100
// Format: <map>,<x>,<y>,<dir>	warp	<name>	<triggerX>,<triggerY>,<destMap>,<destX>,<destY>
```

### Conditional Warp (with requirements)
```c
prontera,155,185,4	script	Dungeon Gate	WARPNPC,{
    mes "[Gate Guard]";
    mes "This dungeon requires Base Level 50+";
    next;
    
    if (BaseLevel < 50) {
        mes "[Gate Guard]";
        mes "You're not strong enough yet.";
        close;
    }
    
    if (Zeny < 1000) {
        mes "[Gate Guard]";
        mes "Entry fee is 1,000 Zeny.";
        close;
    }
    
    mes "[Gate Guard]";
    mes "You may enter.";
    Zeny -= 1000;
    close2;
    warp "pay_dun00", 100, 100;
    end;
}
```

---

## Quest NPCs

<!-- RAG_CHUNK: npc_quest_patterns -->

### Simple Kill Quest
```c
prontera,160,190,4	script	Hunt Master	4_M_JOB_HUNTER,{
    // Check quest state
    switch(checkquest(1000)) {
        case -1:  // Quest not started
            mes "[Hunt Master]";
            mes "I need you to kill 50 Porings.";
            mes "Will you help?";
            next;
            if (select("Accept:Decline") == 1) {
                setquest 1000;
                mes "[Hunt Master]";
                mes "Great! Come back when done.";
            }
            close;
            
        case 0:  // In progress
        case 1:  // In progress (objectives met)
            mes "[Hunt Master]";
            mes "Still working on it?";
            // Check kill count
            if (checkquest(1000, HUNTING) == 2) {
                // Completed
                completequest 1000;
                getitem 501, 10;  // Reward
                getexp 1000, 500;
                mes "Well done! Here's your reward.";
            } else {
                mes "Keep hunting those Porings!";
            }
            close;
            
        case 2:  // Completed
            mes "[Hunt Master]";
            mes "Thanks for your help before!";
            close;
    }
}
```

### Collection Quest
```c
prontera,162,190,4	script	Collector	4_M_JOB_WIZARD,{
    if (COLLECT_QUEST == 0) {
        mes "[Collector]";
        mes "Bring me 20 Jellopy!";
        next;
        if (select("OK:No thanks") == 1) {
            COLLECT_QUEST = 1;
            mes "I'll be waiting!";
        }
        close;
    }
    
    if (COLLECT_QUEST == 1) {
        if (countitem(909) >= 20) {
            mes "[Collector]";
            mes "You have them! Thank you!";
            delitem 909, 20;
            getitem 501, 50;  // Reward
            COLLECT_QUEST = 2;
        } else {
            mes "[Collector]";
            mes "You need " + (20 - countitem(909)) + " more Jellopy.";
        }
        close;
    }
    
    mes "[Collector]";
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
    mes "[Daily Reward]";
    
    // Check if already claimed today
    if (DAILY_REWARD == gettimetick(2) / 86400) {
        mes "You already claimed today's reward!";
        mes "Come back tomorrow.";
        close;
    }
    
    mes "Here's your daily reward!";
    
    // Set claim date (days since epoch)
    DAILY_REWARD = gettimetick(2) / 86400;
    
    // Give rewards
    getitem 501, 10;  // 10 Red Potions
    getitem 502, 5;   // 5 Orange Potions
    
    mes "See you tomorrow!";
    close;
}
```

### Weekly Reward with Streak
```c
prontera,172,190,4	script	Weekly Bonus	4_M_MANAGER,{
    .@today = gettimetick(2) / 86400;
    .@week = gettimetick(2) / 604800;  // Week number
    
    mes "[Weekly Bonus]";
    
    // Check weekly claim
    if (WEEKLY_CLAIM == .@week) {
        mes "You've claimed this week's bonus!";
        close;
    }
    
    // Consecutive week bonus
    if (WEEKLY_CLAIM == .@week - 1) {
        WEEKLY_STREAK++;
    } else {
        WEEKLY_STREAK = 1;  // Reset streak
    }
    
    WEEKLY_CLAIM = .@week;
    
    // Rewards scale with streak
    .@bonus = min(WEEKLY_STREAK, 4);  // Cap at 4x
    getitem 607, 5 * .@bonus;  // Yggdrasil Berry
    
    mes "Week " + WEEKLY_STREAK + " streak!";
    mes "Bonus: " + (5 * .@bonus) + " Yggdrasil Berries";
    close;
}
```

---

## Instance NPCs

<!-- RAG_CHUNK: npc_instance_patterns -->

### Instance Creator
```c
prontera,180,190,4	script	Instance Guide	4_M_JOB_KNIGHT,{
    mes "[Instance Guide]";
    mes "Would you like to enter the dungeon?";
    next;
    
    switch(select("Create Instance:Enter Instance:Cancel")) {
        case 1:  // Create
            // Check if in party
            if (getcharid(1) == 0) {
                mes "You need a party to create an instance!";
                close;
            }
            
            // Check if party leader
            if (getcharid(0) != getpartyleader(getcharid(1), 2)) {
                mes "Only the party leader can create!";
                close;
            }
            
            // Create instance
            .@instance_id = instance_create("My_Instance", getcharid(1));
            if (.@instance_id < 0) {
                mes "Failed to create instance!";
                close;
            }
            
            mes "Instance created! You may enter.";
            close;
            
        case 2:  // Enter
            if (has_instance("My_Instance") == "") {
                mes "No instance found for your party!";
                close;
            }
            
            close2;
            warp "My_Instance", 50, 50;
            end;
            
        case 3:  // Cancel
            close;
    }
}
```

---

## State Machine Patterns

<!-- RAG_CHUNK: npc_state_machine -->

### Multi-stage Quest with States
```c
prontera,185,190,4	script	Epic Quest	4_M_JOB_KNIGHT,{
    switch(EPIC_QUEST_STATE) {
        case 0:  // Not started
            mes "[Knight]";
            mes "Begin the epic quest?";
            next;
            if (select("Yes:No") == 1) {
                EPIC_QUEST_STATE = 1;
                mes "Go find the Ancient Sword!";
            }
            close;
            
        case 1:  // Looking for sword
            if (countitem(1234) > 0) {  // Ancient Sword ID
                mes "[Knight]";
                mes "You found it! Now slay the Dragon.";
                delitem 1234, 1;
                EPIC_QUEST_STATE = 2;
                DRAGON_KILLED = 0;
            } else {
                mes "[Knight]";
                mes "Keep searching for the sword!";
            }
            close;
            
        case 2:  // Kill dragon
            if (DRAGON_KILLED) {
                mes "[Knight]";
                mes "The Dragon is slain! Here's your reward.";
                getitem 7227, 1;  // MVP item
                EPIC_QUEST_STATE = 3;
            } else {
                mes "[Knight]";
                mes "Slay the Dragon in the cave!";
            }
            close;
            
        case 3:  // Completed
            mes "[Knight]";
            mes "You are a true hero!";
            close;
    }
}

// Dragon kill trigger (in mob spawn script)
// OnNPCKillEvent:
//     if (killedrid == DRAGON_ID && EPIC_QUEST_STATE == 2)
//         DRAGON_KILLED = 1;
```

---

## Common Techniques

<!-- RAG_CHUNK: npc_common_techniques -->

### Menu with Variables
```c
// Dynamic menu generation
setarray .@menu$[0], "Option 1", "Option 2", "Option 3";
.@choice = select(implode(.@menu$, ":"));
mes "You chose: " + .@menu$[.@choice - 1];
```

### Input Validation
```c
// Number input with validation
input .@amount;
if (.@amount <= 0 || .@amount > 100) {
    mes "Please enter 1-100.";
    close;
}
```

### Item Check & Consume
```c
// Check multiple items
if (countitem(501) < 5 || countitem(502) < 3) {
    mes "You need 5 Red Potions and 3 Orange Potions.";
    close;
}
delitem 501, 5;
delitem 502, 3;
```

### Party Check
```c
// Check if player is in a party
if (getcharid(1) == 0) {
    mes "You need to be in a party!";
    close;
}

// Get party member count
.@count = getpartymember(getcharid(1), 0);
mes "Party has " + .@count + " members.";
```

### Timer Events
```c
// Set a timer to trigger event
addtimer 60000, strnpcinfo(3) + "::OnTimer";
end;

OnTimer:
    announce "Time's up!", bc_all;
    end;
```

### Global Announcements
```c
announce "[Event] Boss spawned at prontera 150,180!", bc_all;
announce "You found a treasure!", bc_self;
mapannounce "prontera", "Prontera event starting!", bc_map;
```

---

## Event System Hooks

<!-- RAG_CHUNK: npc_event_hooks -->

### Available Event Labels
| Event | Trigger |
|-------|---------|
| OnPCLoginEvent | Player logs in |
| OnPCLogoutEvent | Player logs out |
| OnPCLoadMapEvent | Player enters map (needs mapflag) |
| OnPCKillEvent | Player kills another player |
| OnNPCKillEvent | Player kills a monster |
| OnPCDieEvent | Player dies |
| OnPCStatCalcEvent | Stats recalculated |
| OnWhisperGlobal | GM whisper command |

### Example Event Handler
```c
-	script	EventHandler	FAKE_NPC,{
    end;

OnPCLoginEvent:
    announce "Welcome " + strcharinfo(0) + "!", bc_self;
    end;

OnPCDieEvent:
    // Revive at save point after 5 seconds
    addtimer 5000, strnpcinfo(3) + "::OnRevive";
    end;

OnRevive:
    atcommand "@alive";
    end;
}
```

---

*Generated as part of rAthena KB v6 Complete*

---

# PART 2: DATABASE SCHEMAS


## Quick Navigation

- [item_db.yml](#item_dbyml) - Item definitions
- [skill_db.yml](#skill_dbyml) - Skill definitions
- [mob_db.yml](#mob_dbyml) - Monster definitions
- [quest_db.yml](#quest_dbyml) - Quest definitions
- [item_group_db.yml](#item_group_dbyml) - Item groups

---

## item_db.yml

<!-- RAG_CHUNK: db_item -->

### Complete Schema
```yaml
Header:
  Type: ITEM_DB
  Version: 3

Body:
  - Id: 501                      # Required: Unique item ID
    AegisName: "Red_Potion"      # Required: Server-side name (unique)
    Name: "Red Potion"           # Required: Display name
    Type: Healing                # Item type
    SubType: None                # Weapon/Ammo subtype
    Buy: 50                      # NPC buy price
    Sell: 10                     # NPC sell price
    Weight: 70                   # Item weight (0.1 units)
    Attack: 0                    # Physical attack
    MagicAttack: 0               # Magic attack (weapons)
    Defense: 0                   # Defense value (armor)
    Range: 0                     # Attack range (weapons)
    Slots: 0                     # Card slots (0-4)
    
    Jobs:                        # Equippable jobs
      All: true
      Novice: true
      Swordman: true
      # ... etc
    
    Classes:                     # Equippable classes
      All: true
      Normal: true
      Upper: true
      Baby: true
      Third: true
      Third_Upper: true
      Third_Baby: true
      Fourth: true
    
    Gender: Both                 # Male/Female/Both
    
    Locations:                   # Equipment slots
      Head_Top: true
      Head_Mid: true
      Head_Low: true
      Armor: true
      Right_Hand: true
      Left_Hand: true
      Garment: true
      Shoes: true
      Right_Accessory: true
      Left_Accessory: true
      Both_Hand: true            # Two-handed
      Both_Accessory: true       # Both accessory slots
    
    WeaponLevel: 1               # Weapon level (1-5)
    ArmorLevel: 1                # Armor level (1-2)
    EquipLevelMin: 1             # Minimum equip base level
    EquipLevelMax: 0             # Maximum equip level (0=none)
    Refineable: true             # Can be refined
    Gradable: false              # Can be graded (4th job)
    View: 0                      # Client sprite ID
    
    Flags:
      BuyingStore: false         # Can list in buying store
      DeadBranch: false          # Is dead branch item
      Container: false           # Is container item
      UniqueId: true             # Has unique ID
      BindOnEquip: false         # Binds when equipped
      DropAnnounce: false        # Announces on drop
      NoConsume: false           # Not consumed on use
      DropEffect: None           # DROPEFFECT_*
    
    Delay:
      Duration: 0                # Use delay (ms)
      Status: None               # Status that blocks use
    
    Stack:
      Amount: 0                  # Max stack (0=no limit)
      Inventory: true
      Cart: true
      Storage: true
      GuildStorage: true
    
    NoUse:
      Override: 0                # GM level to override
      Sitting: false             # Block while sitting
    
    Trade:
      Override: 0                # GM level to override
      NoDrop: false
      NoTrade: false
      TradePartner: false
      NoSell: false
      NoCart: false
      NoStorage: false
      NoGuildStorage: false
      NoMail: false
      NoAuction: false
    
    Script: |                    # On-use/equip script
      itemheal 45,0;
    
    EquipScript: |               # On-equip script
      bonus bStr,1;
    
    UnEquipScript: |             # On-unequip script
      # code here
```

### Item Types
| Type | ID | Description |
|------|-----|-------------|
| Healing | 0 | Healing consumables |
| Usable | 2 | Usable items |
| Etc | 3 | Misc items |
| Armor | 4 | Equipment (non-weapon) |
| Weapon | 5 | Weapons |
| Card | 6 | Cards |
| PetEgg | 7 | Pet eggs |
| PetArmor | 8 | Pet equipment |
| Ammo | 10 | Ammunition |
| DelayConsume | 11 | Delayed consume |
| ShadowGear | 12 | Shadow equipment |
| Cash | 18 | Cash items |

### Weapon SubTypes
| SubType | Description |
|---------|-------------|
| Fist | Bare hands |
| Dagger | Daggers |
| 1hSword | One-handed swords |
| 2hSword | Two-handed swords |
| 1hSpear | One-handed spears |
| 2hSpear | Two-handed spears |
| 1hAxe | One-handed axes |
| 2hAxe | Two-handed axes |
| Mace | Maces |
| 2hMace | Two-handed maces |
| Staff | Staves |
| Bow | Bows |
| Knuckle | Knuckles |
| Musical | Instruments |
| Whip | Whips |
| Book | Books |
| Katar | Katars |
| Revolver | Revolvers |
| Rifle | Rifles |
| Gatling | Gatling guns |
| Shotgun | Shotguns |
| Grenade | Grenade launchers |
| Huuma | Huuma shurikens |
| 2hStaff | Two-handed staves |

---

## skill_db.yml

<!-- RAG_CHUNK: db_skill -->

### Complete Schema
```yaml
Header:
  Type: SKILL_DB
  Version: 3

Body:
  - Id: 1                        # Skill ID
    Name: "NV_BASIC"             # Skill constant
    Description: "Basic Skill"   # Display name
    MaxLevel: 9                  # Max skill level
    Type: None                   # None/Weapon/Magic/Misc
    TargetType: Self             # Passive/Attack/Ground/Self/Support/Trap
    
    DamageFlags:
      Splash: false
      SplashSplit: false
      IgnoreAtkCard: false
      IgnoreElement: false
      IgnoreDefense: false
      IgnoreFlee: false
      IgnoreDefCard: false
      Critical: false
      NoDamage: false
    
    Flags:
      IsQuest: false
      IsNpc: false
      IsWedding: false
      IsSpirit: false
      IsGuild: false
      IsSong: false
      IsEnsemble: false
      IsTrap: false
      TargetSelf: false
      NoTargetSelf: false
      PartyOnly: false
      GuildOnly: false
      NoEnemy: false
      IgnoreLandProtector: false
      AllowWhenHidden: false
    
    Range:
      - Level: 1
        Size: 0
    
    Hit: None                    # None/Single/Multi
    
    HitCount:
      - Level: 1
        Count: 0
    
    Element:
      - Level: 1
        Element: Neutral
    
    CastTime:
      - Level: 1
        Time: 0                  # milliseconds
    
    AfterCastActDelay:
      - Level: 1
        Time: 0
    
    Cooldown:
      - Level: 1
        Time: 0
    
    FixedCastTime:
      - Level: 1
        Time: 0
    
    Requires:
      HpCost:
        - Level: 1
          Amount: 0
      SpCost:
        - Level: 1
          Amount: 0
      Weapon:
        All: true
      State: None                # Required state
      ItemCost:
        - Item: Red_Gemstone
          Amount: 1
```

---

## mob_db.yml

<!-- RAG_CHUNK: db_mob -->

### Complete Schema
```yaml
Header:
  Type: MOB_DB
  Version: 3

Body:
  - Id: 1002                     # Monster ID
    AegisName: "PORING"          # Server-side name
    Name: "Poring"               # Display name
    Level: 1
    Hp: 50
    Sp: 0
    BaseExp: 2
    JobExp: 1
    MvpExp: 0                    # MVP bonus EXP
    Attack: 7                    # Min ATK
    Attack2: 10                  # Max ATK
    Defense: 0
    MagicDefense: 5
    Str: 1
    Agi: 1
    Vit: 1
    Int: 0
    Dex: 6
    Luk: 30
    AttackRange: 1
    SkillRange: 10
    ChaseRange: 12
    Size: Small                  # Small/Medium/Large
    Race: Plant                  # Monster race
    Element: Water               # Element
    ElementLevel: 1              # Element level (1-4)
    WalkSpeed: 400
    AttackDelay: 1872
    AttackMotion: 672
    DamageMotion: 480
    DamageTaken: 100             # Damage modifier %
    Ai: 02                       # AI type
    Class: Normal                # Normal/Boss/Guardian
    
    Modes:
      CanMove: true
      Looter: true
      Aggressive: false
      Assist: false
      Boss: false
      Plant: false
      CanAttack: true
      Detector: false
      StatusImmune: false
      SkillImmune: false
    
    MvpDrops:
      - Item: Old_Card_Album
        Rate: 5000               # 50.00%
        StealProtected: true
    
    Drops:
      - Item: Jellopy
        Rate: 7000               # 70.00%
      - Item: Knife_
        Rate: 100                # 1.00%
      - Item: Poring_Card
        Rate: 1                  # 0.01%
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
| 03 | Passive, looter, assist |
| 04 | Aggressive |
| 05 | Aggressive, looter |
| 06 | Aggressive, assist |
| 07 | Boss |
| 08 | Passive, immobile |
| 09 | Aggressive, immobile |
| 10 | Passive, cast sensor |
| 17 | Boss, looter |
| 21 | Boss, aggressive |

---

## quest_db.yml

<!-- RAG_CHUNK: db_quest -->

```yaml
Header:
  Type: QUEST_DB
  Version: 2

Body:
  - Id: 1000                     # Quest ID
    Title: "Hunt Porings"        # Quest title
    TimeLimit: 86400             # Time limit (seconds), 0=none
    
    Targets:                     # Hunt objectives
      - Mob: PORING
        Count: 10
        Id: 0                    # Sub-objective ID
        Race: All                # Race filter
        Size: All                # Size filter
        Element: All             # Element filter
        MinLevel: 0
        MaxLevel: 0
    
    Drops:                       # Collect objectives
      - Mob: PORING
        Item: Jellopy
        Count: 5
        Rate: 5000               # 50% drop rate from kills
```

---

*Generated as part of rAthena KB v6 Complete*
