# 07_EXAMPLES.md
<!-- repo: rathena | branch: claude/github-to-kb-converter-0137h2Ti2PFSsGmn6Xrp3xko | commit: 721d46e | generated: 2025-11-28 -->
<!-- tags: examples, recipes, howto, scripts, code -->

## Contents
- [Quick Start](#quick-start)
- [NPC Script Examples](#npc-script-examples)
- [Item Script Examples](#item-script-examples)
- [Configuration Examples](#configuration-examples)
- [Common Recipes](#common-recipes)

---

## Quick Start
<!-- chunk: 07-quickstart | keywords: setup, install, first, start -->

### Minimal Server Setup

**1. Database Setup:**
```bash
mysql -u root -p
CREATE DATABASE ragnarok;
CREATE USER 'ragnarok'@'localhost' IDENTIFIED BY 'ragnarok';
GRANT ALL ON ragnarok.* TO 'ragnarok'@'localhost';
FLUSH PRIVILEGES;
exit;

mysql -u ragnarok -p ragnarok < sql-files/main.sql
mysql -u ragnarok -p ragnarok < sql-files/logs.sql
```

**2. Build Server:**
```bash
mkdir build && cd build
cmake ..
make -j$(nproc)
make install
cd ..
```

**3. Configure (minimal changes):**
```
// conf/char_athena.conf
server_name: MyServer

// conf/inter_athena.conf
login_server_pw: ragnarok
char_server_pw: ragnarok
map_server_pw: ragnarok
```

**4. Start Server:**
```bash
./athena-start start
```

**5. Create GM Account:**
```sql
INSERT INTO login (account_id, userid, user_pass, sex, group_id)
VALUES (2000000, 'admin', 'admin', 'M', 99);
```

---

## NPC Script Examples
<!-- chunk: 07-npc | keywords: npc, script, dialog -->

### Basic NPC Dialog
<!-- chunk: 07-npc-basic | keywords: mes, next, close -->

```c
// Location: npc/custom/my_npc.txt
// Format: map,x,y,direction<TAB>script<TAB>Display Name<TAB>sprite,{script}

prontera,150,180,4	script	Guide	4_M_NFDEADMAN,{
    mes "[Guide]";
    mes "Welcome to our server!";
    mes "How can I help you?";
    next;
    switch(select("Warp to Payon", "Heal me", "Nothing")) {
        case 1:
            warp "payon",150,150;
            break;
        case 2:
            percentheal 100,100;
            mes "[Guide]";
            mes "You have been healed!";
            break;
        case 3:
            mes "[Guide]";
            mes "Come back anytime!";
            break;
    }
    close;
}
```
→ API: [[02_CORE_API#player-commands]]

### Shop NPC
<!-- chunk: 07-npc-shop | keywords: shop, buy, sell -->

```c
// Simple shop
prontera,155,180,4	shop	Tool Dealer	4_M_ORIENT02,501:50,502:200,503:500

// Advanced shop with conditions
prontera,160,180,4	script	VIP Shop	4_F_KAFRA1,{
    if (getgroupid() < 5) {
        mes "This shop is for VIP members only.";
        close;
    }
    mes "Welcome VIP member!";
    next;
    callshop "vip_shop",1;
    end;
}
-	shop	vip_shop	-1,607:1000,608:2000,678:5000
```

### Quest NPC
<!-- chunk: 07-npc-quest | keywords: quest, items, reward -->

```c
prontera,145,180,4	script	Quest Master	4_M_HUGRANFA,{
    mes "[Quest Master]";
    if (countitem(909) >= 10) {  // Has 10 Jellopy
        mes "You collected the items!";
        delitem 909,10;
        getitem 501,5;  // 5 Red Potions
        getexp 100,50;  // 100 base, 50 job exp
        mes "Here's your reward!";
        close;
    }
    mes "Please bring me 10 Jellopy.";
    close;
}
```

### Warper NPC
<!-- chunk: 07-npc-warp | keywords: warp, teleport, menu -->

```c
prontera,150,175,4	script	Warper	4_F_TELEPORTER,{
    mes "[Warper]";
    mes "Where would you like to go?";
    next;
    switch(select("Towns:Dungeons:Cancel")) {
        case 1:
            mes "[Warper]";
            mes "Select a town:";
            next;
            switch(select("Prontera:Payon:Geffen:Alberta")) {
                case 1: warp "prontera",155,180; break;
                case 2: warp "payon",152,75; break;
                case 3: warp "geffen",120,68; break;
                case 4: warp "alberta",28,234; break;
            }
            break;
        case 2:
            mes "[Warper]";
            mes "Select a dungeon:";
            next;
            switch(select("Prontera Culvert:Payon Cave:Geffen Dungeon")) {
                case 1: warp "prt_sewb1",131,247; break;
                case 2: warp "pay_dun00",21,183; break;
                case 3: warp "gef_dun00",104,99; break;
            }
            break;
        case 3:
            close;
    }
    close;
}
```

### Monster Spawner
<!-- chunk: 07-npc-monster | keywords: monster, spawn, summon -->

```c
prontera,140,180,4	script	Arena Master	4_M_BARMUND,{
    mes "[Arena Master]";
    mes "Ready for a challenge?";
    next;
    if (select("Yes!:No thanks") == 2) close;

    // Warp to arena
    warp "guild_vs1",50,50;

    // Spawn monsters with event label
    monster "guild_vs1",0,0,"Poring",1002,5,"Arena Master::OnMobDead";
    initnpctimer;
    end;

OnMobDead:
    .@count = mobcount("guild_vs1","Arena Master::OnMobDead");
    if (.@count == 0) {
        announce "All monsters defeated!",bc_self;
        warp "prontera",150,180;
        getitem 607,1;  // Yggdrasil Berry reward
    }
    end;

OnTimer60000:  // 60 second timeout
    killmonster "guild_vs1","Arena Master::OnMobDead";
    announce "Time's up!",bc_self;
    warp "prontera",150,180;
    end;
}
```

### Instance Dungeon
<!-- chunk: 07-npc-instance | keywords: instance, dungeon, party -->

```c
prontera,135,180,4	script	Instance Guide	4_M_SAGE_A,{
    mes "[Instance Guide]";

    if (!getcharid(1)) {
        mes "You need a party to enter.";
        close;
    }

    if (!instance_check_party(getcharid(1), 1)) {
        mes "Your party needs at least 1 member here.";
        close;
    }

    mes "Enter the dungeon?";
    next;
    if (select("Enter:Cancel") == 2) close;

    // Create or enter instance
    if (instance_create("MyDungeon", getcharid(1)) < 0) {
        mes "Failed to create instance.";
        close;
    }

    instance_enter("1@mir");
    end;
}
```

---

## Item Script Examples
<!-- chunk: 07-items | keywords: item, bonus, script -->

### Weapon with Bonus
<!-- chunk: 07-item-weapon | keywords: weapon, atk, bonus -->

```yaml
# db/import/item_db.yml
Body:
  - Id: 30000
    AegisName: MY_SWORD
    Name: Custom Sword
    Type: Weapon
    SubType: 1hSword
    Buy: 10000
    Weight: 800
    Attack: 150
    Range: 1
    Slots: 2
    Jobs:
      Swordman: true
      Knight: true
    Locations:
      Right_Hand: true
    WeaponLevel: 3
    EquipLevelMin: 50
    Refineable: true
    Script: |
      bonus bStr,5;
      bonus bAtkRate,10;
      bonus2 bAddRace,RC_Undead,15;
```
→ API: [[02_CORE_API#item-bonuses]]

### Armor with Set Bonus
<!-- chunk: 07-item-armor | keywords: armor, set, combo -->

```yaml
# Custom armor with set effect
Body:
  - Id: 30001
    AegisName: MY_ARMOR
    Name: Dragon Armor
    Type: Armor
    Buy: 50000
    Weight: 2000
    Defense: 80
    Slots: 1
    Jobs:
      All: true
    Locations:
      Armor: true
    ArmorLevel: 1
    EquipLevelMin: 60
    Refineable: true
    Script: |
      bonus bMdef,10;
      bonus bMaxHPrate,5;
    EquipScript: |
      // Check for set pieces
      if (isequipped(30002)) {  // Dragon Shield
        bonus bAllStats,3;
        bonus bLongAtkDef,15;
      }
```

### Consumable with Effect
<!-- chunk: 07-item-consumable | keywords: consumable, heal, buff -->

```yaml
Body:
  - Id: 30010
    AegisName: SUPER_POTION
    Name: Super Potion
    Type: Healing
    Buy: 500
    Sell: 250
    Weight: 50
    Script: |
      itemheal rand(500,700),rand(50,70);
      sc_start SC_INCREASEAGI,60000,5;
    Delay:
      Duration: 3
      Status: ReusableDelay
```

### Card Effect
<!-- chunk: 07-item-card | keywords: card, bonus, slot -->

```yaml
Body:
  - Id: 30100
    AegisName: MY_CARD
    Name: Custom Card
    Type: Card
    Buy: 20
    Weight: 10
    Locations:
      Right_Hand: true
    Script: |
      bonus bCritical,10;
      bonus3 bAutoSpell,"MG_FIREBOLT",3,50;
```

---

## Configuration Examples
<!-- chunk: 07-config | keywords: config, settings, rates -->

### Custom Rates Server
<!-- chunk: 07-config-rates | keywords: rates, exp, drops -->

```
// conf/import/battle_conf.txt

// Experience rates (100 = 1x)
base_exp_rate: 500    // 5x base exp
job_exp_rate: 500     // 5x job exp
mvp_exp_rate: 500     // 5x MVP exp

// Drop rates (100 = 1x)
item_rate_common: 300       // 3x common drops
item_rate_heal: 300         // 3x heal items
item_rate_equip: 200        // 2x equipment
item_rate_card: 100         // 1x cards (keep rare)

// Quality of life
item_auto_get: yes          // Auto-loot
flooritem_lifetime: 120000  // 2 min item despawn
```

### PvP Server Settings
<!-- chunk: 07-config-pvp | keywords: pvp, battle, combat -->

```
// conf/import/battle_conf.txt

// PvP settings
pk_mode: 2                    // Enable PK on all maps
pk_level_range: 15            // Level difference for PK
pk_min_level: 55              // Min level for PK

// Balance for PvP
player_damage_delay_rate: 50  // Faster recovery
skill_min_damage: 1           // Skills always hit
weapon_defense_type: 1        // Linear defense
```

### Low-Rate Classic Settings
<!-- chunk: 07-config-classic | keywords: classic, pre-renewal, lowrate -->

```
// conf/import/battle_conf.txt

// 1x classic experience
base_exp_rate: 100
job_exp_rate: 100
death_penalty_base: 100       // 1% death penalty
death_penalty_job: 100

// Classic drops
item_rate_common: 100
item_rate_card: 100

// Disable modern features
feature.banking: off
feature.roulette: off
feature.achievement: off
```

---

## Common Recipes
<!-- chunk: 07-recipes | keywords: howto, recipe, guide -->

### Add Custom Monster
<!-- chunk: 07-recipe-mob | keywords: monster, custom, spawn -->

**1. Define monster (db/import/mob_db.yml):**
```yaml
Body:
  - Id: 90000
    AegisName: MY_BOSS
    Name: Custom Boss
    Level: 99
    Hp: 1000000
    BaseExp: 100000
    JobExp: 50000
    Attack: 2000
    Attack2: 3000
    Defense: 200
    MagicDefense: 100
    Size: Large
    Race: Demon
    Element: Dark
    ElementLevel: 4
    WalkSpeed: 150
    AttackDelay: 576
    AttackMotion: 576
    DamageMotion: 288
    Ai: 21
    Class: Boss
    Drops:
      - Item: Old_Card_Album
        Rate: 1000
      - Item: Yggdrasilberry
        Rate: 5000
```

**2. Create spawn script (npc/custom/my_boss.txt):**
```c
// Spawn every 4 hours at random location
prt_maze03,0,0,0	boss_monster	Custom Boss	90000,1,14400000,0,0
```

**3. Add to loader (npc/scripts_custom.conf):**
```
npc: npc/custom/my_boss.txt
```

### Add Custom Skill
<!-- chunk: 07-recipe-skill | keywords: skill, custom, ability -->

**Note:** Adding truly new skills requires C++ modifications. This shows buff-like effects via items/scripts.

```c
// Create skill-like effect via item
prontera,130,180,4	script	Skill Vendor	4_M_ALCHE_B,{
    mes "[Skill Master]";
    mes "I can grant you temporary power.";
    next;
    switch(select("Power Boost (1000z):Speed Boost (500z):Cancel")) {
        case 1:
            if (Zeny < 1000) { mes "Not enough zeny."; close; }
            Zeny -= 1000;
            // Custom "skill" effect
            sc_start SC_INCATKRATE,300000,20;  // +20% ATK for 5 min
            sc_start SC_BLESSING,300000,10;
            mes "Power activated!";
            break;
        case 2:
            if (Zeny < 500) { mes "Not enough zeny."; close; }
            Zeny -= 500;
            sc_start SC_INCREASEAGI,300000,10;
            sc_start SC_WINDWALK,300000,5;
            mes "Speed activated!";
            break;
        case 3:
            close;
    }
    close;
}
```

### Add Custom Quest
<!-- chunk: 07-recipe-quest | keywords: quest, objective, reward -->

**1. Define quest (db/import/quest_db.yml):**
```yaml
Body:
  - Id: 90000
    Title: Poring Extermination
    TimeLimitSeconds: 3600
    Targets:
      - Mob: PORING
        Count: 20
    Drops:
      - Mob: PORING
        Item: Jellopy
        Count: 10
        Rate: 3000
```

**2. Create quest giver (npc/custom/my_quest.txt):**
```c
prontera,125,180,4	script	Quest Giver	4_M_JOB_KNIGHT1,{
    mes "[Quest Giver]";

    if (checkquest(90000) == 2) {
        mes "You completed the quest!";
        completequest 90000;
        getitem 607,5;  // 5 Yggdrasil Berries
        getexp 10000,5000;
        close;
    }

    if (checkquest(90000) == 1) {
        mes "Kill 20 Porings and collect 10 Jellopy.";
        close;
    }

    if (checkquest(90000) == 0) {
        mes "No active quest.";
        mes "Want to hunt Porings?";
        next;
        if (select("Accept:Decline") == 1) {
            setquest 90000;
            mes "Good luck!";
        }
        close;
    }
    close;
}
```

### Create Daily Reward System
<!-- chunk: 07-recipe-daily | keywords: daily, reward, login -->

```c
prontera,120,180,4	script	Daily Rewards	4_F_KAFRA2,{
    mes "[Daily Rewards]";

    // Check if already claimed today
    if (#DAILY_LASTCLAIM >= gettimetick(2) - 86400) {
        mes "Come back tomorrow!";
        .@next = #DAILY_LASTCLAIM + 86400 - gettimetick(2);
        mes "Time remaining: " + (.@next/3600) + "h " + ((.@next%3600)/60) + "m";
        close;
    }

    // Calculate streak
    if (#DAILY_LASTCLAIM < gettimetick(2) - 172800) {
        #DAILY_STREAK = 0;  // Reset if missed a day
    }
    #DAILY_STREAK++;
    #DAILY_LASTCLAIM = gettimetick(2);

    mes "Day " + #DAILY_STREAK + " reward!";

    // Rewards based on streak
    switch(#DAILY_STREAK) {
        case 1: getitem 501,10; break;   // 10 Red Potions
        case 2: getitem 502,10; break;   // 10 Orange Potions
        case 3: getitem 503,5; break;    // 5 Yellow Potions
        case 4: getitem 504,5; break;    // 5 White Potions
        case 5: getitem 607,3; break;    // 3 Yggdrasil Berries
        case 6: getitem 608,1; break;    // 1 Yggdrasil Seed
        case 7:
            getitem 7227,1;              // 1 Treasure Box
            #DAILY_STREAK = 0;           // Reset after week
            break;
    }

    mes "Claimed successfully!";
    close;
}
```

---

## Quick Links

- Architecture: → See [[01_ARCHITECTURE]]
- API Functions: → See [[02_CORE_API]]
- Data Models: → See [[03_DATA_MODELS]]
- Configuration: → See [[05_CONFIG]]
