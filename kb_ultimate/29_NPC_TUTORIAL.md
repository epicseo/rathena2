# rAthena NPC Scripting Tutorial
## Complete Guide to Creating NPCs

---

<!-- RAG_CHUNK: npc_basics_001 -->
## NPC Basics

### NPC Types

**1. Standard NPC**
```c
prontera,155,180,5	script	Guide	4_F_KAFRA1,{
    mes "[Guide]";
    mes "Welcome to Prontera!";
    close;
}
```

**2. Floating NPC (No Location)**
```c
-	script	GlobalNPC	-1,{
OnInit:
    announce "Server loaded!",bc_all;
    end;
}
```

**3. Warp NPC**
```c
prontera,156,188,0	warp	prt_to_prtcas	2,2,prt_castle,102,129
```

**4. Shop NPC**
```c
prontera,147,180,4	shop	Tool Dealer	4_M_ORIENT01,501:50,502:60,503:200
```

**5. Duplicate NPC**
```c
alberta,100,100,4	duplicate(Guide)	Guide#alb	4_F_KAFRA1
```

### NPC Definition Format
```
<map>,<x>,<y>,<dir>	script	<Name>	<sprite>,{<script>}
<map>,<x>,<y>,<dir>	script	<Name>	<sprite>,<trigger_x>,<trigger_y>,{<script>}
```

- `<dir>` - Facing: 0=N, 1=NW, 2=W, 3=SW, 4=S, 5=SE, 6=E, 7=NE
- `<sprite>` - NPC sprite ID or constant (see db/const.txt)
- `-1` sprite = invisible NPC
- `111` sprite = invisible but clickable

---

<!-- RAG_CHUNK: npc_dialog_001 -->
## Dialog Patterns

### Basic Conversation
```c
prontera,155,180,5	script	Villager	4_M_01,{
    mes "[Villager]";
    mes "Hello there, " + strcharinfo(0) + "!";
    mes "How are you today?";
    next;
    mes "[Villager]";
    mes "I hope you're having a great adventure!";
    close;
}
```

### Menu Selection
```c
prontera,155,180,5	script	Guide	4_F_KAFRA1,{
    mes "[Guide]";
    mes "What would you like to know?";
    next;
    switch(select("About Prontera:Nearby Locations:Nothing")) {
        case 1:
            mes "[Guide]";
            mes "Prontera is the capital city!";
            break;
        case 2:
            mes "[Guide]";
            mes "You can visit Izlude to the south.";
            break;
        case 3:
            mes "[Guide]";
            mes "Okay, goodbye!";
            break;
    }
    close;
}
```

### Input Handling
```c
prontera,155,180,5	script	Quiz Master	4_M_SAGE_C,{
    mes "[Quiz Master]";
    mes "What is 2 + 2?";
    next;
    input .@answer;

    if (.@answer == 4) {
        mes "[Quiz Master]";
        mes "Correct! Here's your reward!";
        getitem 512, 5;  // 5 Apples
    } else {
        mes "[Quiz Master]";
        mes "Wrong! The answer is 4.";
    }
    close;
}
```

---

<!-- RAG_CHUNK: npc_shop_001 -->
## Shop NPCs

### Basic Shop
```c
// Format: itemID:price
prontera,147,180,4	shop	Potion Seller	4_M_ORIENT01,501:50,502:60,503:200,-1:999
```

Using `-1` as price uses item_db price.

### Cash Shop
```c
prontera,150,180,4	cashshop	Cash Shop	4_F_KAFRA3,12103:100,12104:150
```

### Point Shop
```c
prontera,152,180,4	pointshop	Event Shop	4_M_MERCAT1,#EVENTPOINTS,501:10,502:20
```

### Item Shop
```c
prontera,154,180,4	itemshop	Token Shop	4_M_MERCAT2,7227,501:1,502:2
```
Requires item 7227 (Token) as currency.

### Dynamic Shop (callshop)
```c
-	shop	DynamicShop	-1,501:100

prontera,156,180,4	script	Smart Seller	4_M_MERCAT1,{
    mes "[Seller]";
    mes "I have special items today!";
    next;

    // Modify shop contents
    npcshopdelitem "DynamicShop", 501;
    npcshopadditem "DynamicShop", 502, 150;

    callshop "DynamicShop", 1;  // 0=buy, 1=sell, 2=both
    end;
}
```

---

<!-- RAG_CHUNK: npc_warp_001 -->
## Warp NPCs

### Basic Warp
```c
// Walk-on warp
prontera,156,188,0	warp	prt_exit	2,2,prt_fild08,170,180
```

### Script-Based Warp
```c
prontera,155,180,5	script	Warper	4_F_KAFRA1,{
    mes "[Warper]";
    mes "Where would you like to go?";
    next;

    switch(select("Morroc:Geffen:Payon:Cancel")) {
        case 1:
            warp "morocc", 156, 93;
            break;
        case 2:
            warp "geffen", 120, 68;
            break;
        case 3:
            warp "payon", 152, 75;
            break;
        case 4:
            close;
    }
    end;
}
```

### Paid Warp
```c
prontera,155,180,5	script	Kafra	4_F_KAFRA1,{
    mes "[Kafra]";
    mes "Teleport service costs 1000z.";
    next;

    if (select("Yes:No") == 1) {
        if (Zeny < 1000) {
            mes "[Kafra]";
            mes "Not enough Zeny!";
            close;
        }
        Zeny -= 1000;
        warp "izlude", 128, 98;
        end;
    }
    close;
}
```

---

<!-- RAG_CHUNK: npc_quest_001 -->
## Quest NPCs

### Simple Collection Quest
```c
prontera,155,180,5	script	Collector	4_M_JOB_HUNTER,{
    mes "[Collector]";
    mes "I need 10 Jellopy. Can you help?";
    next;

    if (select("Yes:No") == 2) {
        mes "[Collector]";
        mes "Maybe next time.";
        close;
    }

    if (countitem(909) >= 10) {
        delitem 909, 10;
        mes "[Collector]";
        mes "Thank you! Here's your reward!";
        getitem 501, 20;
        getexp 1000, 500;
        close;
    }

    mes "[Collector]";
    mes "You don't have enough Jellopy.";
    mes "Current: " + countitem(909) + "/10";
    close;
}
```

### Monster Hunt Quest
```c
prontera,155,180,5	script	Hunter Guild	4_M_JOB_HUNTER,{
    if (#PORING_HUNT == 0) {
        mes "[Hunter]";
        mes "Kill 20 Porings for a reward!";
        next;

        if (select("Accept:Decline") == 1) {
            #PORING_HUNT = 1;
            #PORING_KILLED = 0;
            mes "[Hunter]";
            mes "Good luck!";
        }
        close;
    }

    if (#PORING_KILLED >= 20) {
        mes "[Hunter]";
        mes "Well done! Here's your reward!";
        getitem 607, 5;
        #PORING_HUNT = 0;
        #PORING_KILLED = 0;
        close;
    }

    mes "[Hunter]";
    mes "Progress: " + #PORING_KILLED + "/20 Porings";
    close;
}

// Kill tracking
prt_fild08,0,0,0	script	#PoringTracker	-1,{
OnNPCKillEvent:
    if (#PORING_HUNT && killedrid == 1002) {
        #PORING_KILLED++;
        dispbottom "Poring killed: " + #PORING_KILLED + "/20";
    }
    end;
}
```

### Quest Log Integration
```c
prontera,155,180,5	script	Quest Board	4_BOARD3,{
    if (checkquest(60001) == -1) {
        // Quest not started
        mes "[Quest Board]";
        mes "New Quest: Poring Hunt";
        mes "Kill 10 Porings";
        next;

        if (select("Accept:Cancel") == 1) {
            setquest 60001;
            mes "[Quest Board]";
            mes "Quest accepted!";
        }
        close;
    }

    if (checkquest(60001, PLAYTIME) == 2) {
        // Quest complete
        mes "[Quest Board]";
        mes "Quest Complete!";
        erasequest 60001;
        getitem 501, 50;
        close;
    }

    mes "[Quest Board]";
    mes "Quest in progress...";
    close;
}
```

---

<!-- RAG_CHUNK: npc_events_001 -->
## Event Labels

### Timer Events
```c
-	script	AutoAnnounce	-1,{
OnInit:
    // Run every hour
    initnpctimer;
    end;

OnTimer3600000:  // 1 hour in ms
    announce "Hourly reminder!",bc_all;
    initnpctimer;  // Restart timer
    end;
}
```

### Clock Events
```c
-	script	DailyReward	-1,{
OnClock1200:  // 12:00 PM
    announce "It's noon! Daily rewards available!",bc_all;
    end;

OnHour00:  // Every day at midnight
    // Reset daily counters
    query_sql("UPDATE `char_reg_num` SET `value`=0 WHERE `key`='#DAILY_DONE'");
    end;
}
```

### Player Events
```c
-	script	WelcomeSystem	-1,{
OnPCLoginEvent:
    if (#FIRST_LOGIN == 0) {
        #FIRST_LOGIN = 1;
        mes "[System]";
        mes "Welcome to our server!";
        mes "Here's a starter pack!";
        getitem 501, 50;
        getitem 502, 50;
        close;
    }
    end;

OnPCBaseLvUpEvent:
    if (BaseLevel == 99) {
        announce strcharinfo(0) + " has reached level 99!",bc_all;
    }
    end;

OnPCDieEvent:
    // killerrid contains killer's ID
    if (killerrid) {
        dispbottom "You were killed by " + rid2name(killerrid);
    }
    end;
}
```

### Touch/Trigger Events
```c
// NPC with trigger area (5x5)
prontera,155,180,5	script	Guard	4_M_JOB_KNIGHT1,5,5,{
    mes "[Guard]";
    mes "Welcome to the castle!";
    close;

OnTouch:
    mes "[Guard]";
    mes "Halt! State your business!";
    close;
}
```

---

<!-- RAG_CHUNK: npc_variables_001 -->
## Variables in NPCs

### Variable Scopes
```c
prontera,155,180,5	script	VarDemo	4_M_01,{
    // Scope variable (this execution only)
    .@local = 1;

    // NPC variable (persistent until reload)
    .npc_var++;

    // Character variable (permanent)
    PlayerVar++;

    // Temporary character variable
    @temp = 1;

    // Account variable (permanent)
    #account_var++;

    // Global variable (all players)
    $global++;

    // Global temporary variable
    $@temp = 1;

    mes "NPC accessed: " + .npc_var + " times";
    mes "Your visits: " + PlayerVar;
    close;
}
```

### Arrays
```c
prontera,155,180,5	script	ArrayDemo	4_M_01,{
    setarray .@items[0], 501, 502, 503, 504, 505;
    setarray .@names$[0], "Red Pot", "Orange Pot", "Yellow Pot", "White Pot", "Blue Pot";

    mes "Items:";
    for (.@i = 0; .@i < getarraysize(.@items); .@i++) {
        mes "- " + .@names$[.@i] + " (" + .@items[.@i] + ")";
    }
    close;
}
```

---

<!-- RAG_CHUNK: npc_functions_001 -->
## Functions and Subroutines

### Using callsub
```c
prontera,155,180,5	script	FuncDemo	4_M_01,{
    mes "[NPC]";
    mes "Choose an option:";
    next;

    switch(select("Get Items:Get Zeny:Heal")) {
        case 1:
            callsub S_GiveItems, 501, 10;
            break;
        case 2:
            callsub S_GiveZeny, 1000;
            break;
        case 3:
            callsub S_Heal;
            break;
    }
    close;

S_GiveItems:
    getitem getarg(0), getarg(1);
    mes "[NPC]";
    mes "Items given!";
    return;

S_GiveZeny:
    Zeny += getarg(0);
    mes "[NPC]";
    mes "Zeny given!";
    return;

S_Heal:
    percentheal 100, 100;
    mes "[NPC]";
    mes "Healed!";
    return;
}
```

### Using Local Functions
```c
prontera,155,180,5	script	LocalFunc	4_M_01,{
    function MyFunc;

    mes "Result: " + MyFunc(5, 10);
    close;

    function MyFunc {
        return getarg(0) + getarg(1);
    }
}
```

### Using Global Functions
```c
// Function NPC
function	script	F_GiveRandomItem	{
    .@items[0] = 501;
    .@items[1] = 502;
    .@items[2] = 503;

    .@rand = rand(getarraysize(.@items));
    getitem .@items[.@rand], getarg(0, 1);
    return .@items[.@rand];
}

// Using it
prontera,155,180,5	script	ItemGiver	4_M_01,{
    mes "[NPC]";
    .@item = callfunc("F_GiveRandomItem", 5);
    mes "You got 5x " + getitemname(.@item) + "!";
    close;
}
```

---

<!-- RAG_CHUNK: npc_advanced_001 -->
## Advanced Patterns

### Dynamic Menu
```c
prontera,155,180,5	script	DynMenu	4_M_01,{
    // Build menu based on conditions
    .@menu$ = "";

    if (BaseLevel >= 10)
        .@menu$ += "Option A:";
    if (BaseLevel >= 50)
        .@menu$ += "Option B:";
    if (BaseLevel >= 99)
        .@menu$ += "Option C:";

    .@menu$ += "Cancel";

    .@sel = select(.@menu$);
    // Handle selection...
    close;
}
```

### Cooldown System
```c
prontera,155,180,5	script	DailyNPC	4_M_01,{
    .@cooldown = 86400;  // 24 hours
    .@current = gettimetick(2);
    .@last = #DAILY_LAST;

    if (.@current - .@last < .@cooldown) {
        .@remain = .@cooldown - (.@current - .@last);
        .@hours = .@remain / 3600;
        .@mins = (.@remain % 3600) / 60;

        mes "[NPC]";
        mes "Come back in " + .@hours + "h " + .@mins + "m";
        close;
    }

    #DAILY_LAST = .@current;
    mes "[NPC]";
    mes "Here's your daily reward!";
    getitem 501, 10;
    close;
}
```

### Random Event NPC
```c
-	script	RandomEvent	-1,{
OnInit:
OnTimer7200000:  // Every 2 hours
    .@maps$[0] = "prontera";
    .@maps$[1] = "geffen";
    .@maps$[2] = "payon";

    .@map$ = .@maps$[rand(3)];

    announce "A treasure chest appeared in " + .@map$ + "!",bc_all;

    // Spawn event monster
    monster .@map$, 0, 0, "Treasure Chest", 1732, 1, strnpcinfo(0)+"::OnChestKilled";

    initnpctimer;
    end;

OnChestKilled:
    announce strcharinfo(0) + " found the treasure!",bc_all;
    getitem 607, 10;  // Yggdrasilberry
    end;
}
```

---

#rathena #npc #script #tutorial #dialog #shop #warp #quest #events #functions
