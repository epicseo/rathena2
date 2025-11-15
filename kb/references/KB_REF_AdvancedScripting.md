---
kb_id: KB_REF_021
title: "rAthena Advanced Scripting Patterns & Techniques"
category: Advanced Scripting
keywords: [advanced_scripting, optimization, arrays, dynamic_shops, sql, pcre, regex, performance, error_handling, best_practices, freeloop, query_sql, setd, getd, npcshopattach, npc_timers]
related_files: [
  "doc/sample/",
  "doc/script_commands.txt",
  "npc/re/merchants/",
  "npc/custom/"
]
difficulty: expert
use_case: "Advanced scripting patterns, optimization techniques, complex systems, dynamic content, SQL integration, and professional-grade NPC development"
version: rAthena 2024
last_updated: 2024-01-15
---

# rAthena Advanced Scripting Patterns & Techniques

## Table of Contents
1. [Advanced Array Techniques](#advanced-array-techniques)
2. [Dynamic Variable Management](#dynamic-variable-management)
3. [Dynamic Shop Systems](#dynamic-shop-systems)
4. [Regular Expressions (PCRE)](#regular-expressions-pcre)
5. [SQL Integration](#sql-integration)
6. [Performance Optimization](#performance-optimization)
7. [Advanced NPC Patterns](#advanced-npc-patterns)
8. [Error Handling & Validation](#error-handling--validation)
9. [Complex Event Systems](#complex-event-systems)
10. [Real-World Examples](#real-world-examples)

---

## Advanced Array Techniques

### Multi-Dimensional Arrays

While rAthena doesn't have true multi-dimensional arrays, you can simulate them:

```c
// Simulate 2D array using index calculation
// Formula: index = row * column_count + column

function	Set2D	{
	// Set2D(array, row, col, column_count, value)
	set getarg(0)[getarg(1) * getarg(3) + getarg(2)], getarg(4);
	return;
}

function	Get2D	{
	// Get2D(array, row, col, column_count)
	return getarg(0)[getarg(1) * getarg(3) + getarg(2)];
}

// Usage example: 3x3 grid
prontera,150,150,4	script	2D Array Test	123,{
	// Set values in 3x3 grid
	callfunc("Set2D", .@grid, 0, 0, 3, 100);  // [0,0] = 100
	callfunc("Set2D", .@grid, 0, 1, 3, 200);  // [0,1] = 200
	callfunc("Set2D", .@grid, 1, 2, 3, 300);  // [1,2] = 300

	// Read values
	.@val = callfunc("Get2D", .@grid, 0, 0, 3);
	mes "Grid[0,0] = " + .@val;  // 100

	.@val = callfunc("Get2D", .@grid, 1, 2, 3);
	mes "Grid[1,2] = " + .@val;  // 300
	close;
}
```

---

### Array Searching & Sorting

```c
// Linear search in array
function	ArraySearch	{
	// ArraySearch(array, value) - returns index or -1
	.@size = getarraysize(getarg(0));
	for (.@i = 0; .@i < .@size; .@i++) {
		if (getarg(0)[.@i] == getarg(1))
			return .@i;
	}
	return -1;
}

// Bubble sort (ascending)
function	ArraySort	{
	// ArraySort(array)
	.@size = getarraysize(getarg(0));
	for (.@i = 0; .@i < .@size - 1; .@i++) {
		for (.@j = 0; .@j < .@size - .@i - 1; .@j++) {
			if (getarg(0)[.@j] > getarg(0)[.@j + 1]) {
				.@temp = getarg(0)[.@j];
				set getarg(0)[.@j], getarg(0)[.@j + 1];
				set getarg(0)[.@j + 1], .@temp;
			}
		}
	}
	return;
}

// Usage
prontera,151,151,4	script	Array Utils	123,{
	setarray .@items[0], 502, 501, 503, 506, 505;

	// Search for item
	.@index = callfunc("ArraySearch", .@items, 503);
	mes "Item 503 is at index: " + .@index;

	// Sort array
	callfunc("ArraySort", .@items);
	mes "Sorted: " + .@items[0] + ", " + .@items[1] + ", " + .@items[2];
	close;
}
```

---

### Advanced Array Operations

```c
// Remove duplicates from array
function	ArrayUnique	{
	.@size = getarraysize(getarg(0));
	.@new_size = 0;

	for (.@i = 0; .@i < .@size; .@i++) {
		.@found = 0;
		for (.@j = 0; .@j < .@new_size; .@j++) {
			if (.@unique[.@j] == getarg(0)[.@i]) {
				.@found = 1;
				break;
			}
		}
		if (!.@found)
			.@unique[.@new_size++] = getarg(0)[.@i];
	}

	// Copy back to original array
	cleararray getarg(0)[0], 0, .@size;
	copyarray getarg(0)[0], .@unique[0], .@new_size;
	return .@new_size;
}

// Shuffle array (Fisher-Yates algorithm)
function	ArrayShuffle	{
	.@size = getarraysize(getarg(0));
	for (.@i = .@size - 1; .@i > 0; .@i--) {
		.@j = rand(.@i + 1);
		.@temp = getarg(0)[.@i];
		set getarg(0)[.@i], getarg(0)[.@j];
		set getarg(0)[.@j], .@temp;
	}
	return;
}

// Filter array by condition
function	ArrayFilter	{
	// ArrayFilter(source_array, dest_array, min_value, max_value)
	.@size = getarraysize(getarg(0));
	.@new_size = 0;

	for (.@i = 0; .@i < .@size; .@i++) {
		if (getarg(0)[.@i] >= getarg(2) && getarg(0)[.@i] <= getarg(3))
			set getarg(1)[.@new_size++], getarg(0)[.@i];
	}
	return .@new_size;
}

// Usage
prontera,152,152,4	script	Advanced Arrays	123,{
	// Unique example
	setarray .@nums[0], 1, 2, 3, 2, 4, 1, 5, 3;
	.@size = callfunc("ArrayUnique", .@nums);
	mes "Unique: " + implode(.@nums, ", ");

	// Shuffle example
	setarray .@cards[0], 4001, 4002, 4003, 4004, 4005;
	callfunc("ArrayShuffle", .@cards);
	mes "Shuffled: " + implode(.@cards, ", ");

	// Filter example
	setarray .@levels[0], 50, 75, 100, 125, 150, 25, 80;
	.@count = callfunc("ArrayFilter", .@levels, .@filtered, 70, 130);
	mes "Filtered (70-130): " + implode(.@filtered, ", ");
	close;
}
```

---

## Dynamic Variable Management

### setd() / getd() - Dynamic Variable Names

```c
// Basic usage
prontera,153,153,4	script	Dynamic Vars	123,{
	// Set variable with dynamic name
	.@var_name$ = "#Kill_" + 1002;  // "#Kill_1002"
	setd(.@var_name$, 100);
	mes "Killed Porings: " + getd("#Kill_1002");  // 100

	// Loop through dynamic variables
	for (.@i = 1002; .@i <= 1005; .@i++) {
		.@var$ = "#Kill_" + .@i;
		setd(.@var$, rand(50, 200));
	}

	// Display all
	mes "Monster Kill Counts:";
	for (.@i = 1002; .@i <= 1005; .@i++) {
		.@var$ = "#Kill_" + .@i;
		mes getmonsterinfo(.@i, MOB_NAME) + ": " + getd(.@var$);
	}
	close;
}
```

---

### Advanced setd/getd Patterns

```c
// Dynamic quest system
-	script	DynamicQuest	-1,{
OnInit:
	// Define quest data using dynamic variables
	for (.@i = 0; .@i < 10; .@i++) {
		setd("$Quest_" + .@i + "_Target", 1002 + .@i);  // Monster ID
		setd("$Quest_" + .@i + "_Count", 100);           // Required kills
		setd("$Quest_" + .@i + "_Reward", 1000000);      // Zeny reward
	}
	end;
}

prontera,154,154,4	script	Quest Board	123,{
	mes "[Quest Board]";
	mes "Available quests:";
	next;

	// Display all quests
	for (.@i = 0; .@i < 10; .@i++) {
		.@mob = getd("$Quest_" + .@i + "_Target");
		.@count = getd("$Quest_" + .@i + "_Count");
		.@reward = getd("$Quest_" + .@i + "_Reward");
		.@progress = getd("#Quest_" + .@i + "_Progress");

		.@mob_name$ = getmonsterinfo(.@mob, MOB_NAME);
		mes (.@i + 1) + ". Kill " + .@count + "x " + .@mob_name$;
		mes "   Progress: " + .@progress + "/" + .@count;
		mes "   Reward: " + .@reward + " Zeny";
	}

	next;
	mes "Select quest:";
	.@quest = select("Quest 1:Quest 2:Quest 3:Cancel") - 1;

	if (.@quest == 3) close;

	// Accept quest
	.@mob = getd("$Quest_" + .@quest + "_Target");
	.@count = getd("$Quest_" + .@quest + "_Count");

	mes "Quest accepted!";
	mes "Kill " + .@count + "x " + getmonsterinfo(.@mob, MOB_NAME);
	setd("#Quest_" + .@quest + "_Active", 1);
	close;
}
```

---

### Variable Reference Patterns

```c
// Access player variables dynamically
function	GetPlayerVar	{
	// GetPlayerVar("variable_name", char_id)
	.@var$ = getarg(0);
	.@char_id = getarg(1);

	attachrid(.@char_id);
	.@value = getd(.@var$);
	detachrid();

	return .@value;
}

function	SetPlayerVar	{
	// SetPlayerVar("variable_name", value, char_id)
	.@var$ = getarg(0);
	.@value = getarg(1);
	.@char_id = getarg(2);

	attachrid(.@char_id);
	setd(.@var$, .@value);
	detachrid();

	return;
}

// Usage
prontera,155,155,4	script	Admin Tools	123,{
	if (getgmlevel() < 99) {
		mes "Access denied.";
		close;
	}

	mes "[Admin Tools]";
	mes "Target player name:";
	input .@target$;

	.@char_id = getcharid(0, .@target$);
	if (.@char_id == 0) {
		mes "Player not found!";
		close;
	}

	// Get player's zeny
	.@zeny = callfunc("GetPlayerVar", "Zeny", .@char_id);
	mes .@target$ + "'s Zeny: " + .@zeny;

	mes "Modify?";
	next;
	if (select("Yes:No") == 1) {
		mes "New value:";
		input .@new_zeny;
		callfunc("SetPlayerVar", "Zeny", .@new_zeny, .@char_id);
		mes "Updated!";
	}
	close;
}
```

---

## Dynamic Shop Systems

### Basic Dynamic Shop

```c
// Dummy shop definition
-	shop	DynShop	-1,501:50

prontera,156,156,4	script	Dynamic Shop	123,{
	mes "[Dynamic Shop]";
	mes "Current stock:";
	mes "Red Potion: " + $@stock_501 + " left";
	mes "Orange Potion: " + $@stock_502 + " left";
	next;

	callshop "DynShop", 0;
	npcshopattach "DynShop";
	end;

OnBuyItem:
	// Process each bought item
	for (.@i = 0; .@i < getarraysize(@bought_nameid); .@i++) {
		.@item = @bought_nameid[.@i];
		.@qty = @bought_quantity[.@i];
		.@price = @bought_price[.@i];

		// Check stock
		.@stock_var$ = "$@stock_" + .@item;
		.@available = getd(.@stock_var$);

		if (.@qty > .@available) {
			mes "Not enough stock!";
			close;
		}

		// Check zeny
		if (Zeny < (.@price * .@qty)) {
			mes "Not enough zeny!";
			close;
		}

		// Process purchase
		Zeny -= (.@price * .@qty);
		getitem .@item, .@qty;
		setd(.@stock_var$, .@available - .@qty);
	}

	// Clear arrays
	deletearray @bought_nameid, getarraysize(@bought_nameid);
	deletearray @bought_quantity, getarraysize(@bought_quantity);
	deletearray @bought_price, getarraysize(@bought_price);

	mes "Purchase complete!";
	close;

OnSellItem:
	// Process sold items (restocking)
	for (.@i = 0; .@i < getarraysize(@sold_nameid); .@i++) {
		.@item = @sold_nameid[.@i];
		.@qty = @sold_quantity[.@i];

		// Validate player has items
		if (countitem(.@item) < .@qty) {
			mes "You don't have that many items!";
			close;
		}

		// Calculate sell price (50% of buy price)
		.@price = getiteminfo(.@item, ITEMINFO_BUY) / 2;

		// Process sale
		delitem .@item, .@qty;
		Zeny += (.@price * .@qty);

		// Restock
		.@stock_var$ = "$@stock_" + .@item;
		setd(.@stock_var$, getd(.@stock_var$) + .@qty);
	}

	// Clear arrays
	deletearray @sold_nameid, getarraysize(@sold_nameid);
	deletearray @sold_quantity, getarraysize(@sold_quantity);

	mes "Sold successfully!";
	close;

OnInit:
	// Initialize shop items and stock
	npcshopitem "DynShop", 501, 50, 502, 100;
	$@stock_501 = 100;
	$@stock_502 = 50;
	end;
}
```

---

### Advanced Time-Based Shop

```c
// Shop that changes inventory based on time
-	shop	TimeShop	-1,501:50

prontera,157,157,4	script	Time-Based Shop	123,{
	mes "[Time Shop]";
	mes "Current hour: " + gettime(3);
	mes "Shop changes every hour!";
	next;

	callshop "TimeShop", 0;
	npcshopattach "TimeShop";
	end;

OnClock0000:
OnClock0100:
OnClock0200:
OnClock0300:
OnClock0400:
OnClock0500:
OnClock0600:
OnClock0700:
OnClock0800:
OnClock0900:
OnClock1000:
OnClock1100:
OnClock1200:
OnClock1300:
OnClock1400:
OnClock1500:
OnClock1600:
OnClock1700:
OnClock1800:
OnClock1900:
OnClock2000:
OnClock2100:
OnClock2200:
OnClock2300:
	donpcevent strnpcinfo(3) + "::OnUpdateShop";
	end;

OnUpdateShop:
	.@hour = gettime(3);

	// Clear current shop
	npcshopdelitem "TimeShop", 501;
	npcshopdelitem "TimeShop", 502;
	npcshopdelitem "TimeShop", 503;

	// Add items based on hour
	if (.@hour >= 0 && .@hour < 6) {
		// Night items (00:00 - 05:59)
		npcshopadditem "TimeShop", 501, 40;   // Red Potion
		npcshopadditem "TimeShop", 502, 80;   // Orange Potion
	} else if (.@hour >= 6 && .@hour < 12) {
		// Morning items (06:00 - 11:59)
		npcshopadditem "TimeShop", 502, 80;
		npcshopadditem "TimeShop", 503, 150;  // Yellow Potion
	} else if (.@hour >= 12 && .@hour < 18) {
		// Afternoon items (12:00 - 17:59)
		npcshopadditem "TimeShop", 501, 40;
		npcshopadditem "TimeShop", 503, 150;
	} else {
		// Evening items (18:00 - 23:59)
		npcshopadditem "TimeShop", 501, 40;
		npcshopadditem "TimeShop", 502, 80;
		npcshopadditem "TimeShop", 503, 150;
	}

	announce "Time Shop inventory updated!", bc_all;
	end;

OnInit:
	donpcevent strnpcinfo(3) + "::OnUpdateShop";
	end;
}
```

---

### VIP Shop System

```c
-	shop	VIPShop	-1,501:50

prontera,158,158,4	script	VIP Shop	123,{
	// Check VIP status
	if (#VIP_Expire < gettimetick(2)) {
		mes "[VIP Shop]";
		mes "This shop is for VIP members only!";
		mes "Purchase VIP access?";
		mes "Cost: 10,000,000 Zeny (30 days)";
		next;
		if (select("Purchase:Cancel") == 2) close;

		if (Zeny < 10000000) {
			mes "Not enough zeny!";
			close;
		}

		Zeny -= 10000000;
		#VIP_Expire = gettimetick(2) + (30 * 24 * 60 * 60);
		mes "VIP access granted for 30 days!";
		close;
	}

	.@remaining = (#VIP_Expire - gettimetick(2)) / (24 * 60 * 60);
	mes "[VIP Shop]";
	mes "Welcome, VIP member!";
	mes "VIP expires in " + .@remaining + " days.";
	next;

	callshop "VIPShop", 0;
	npcshopattach "VIPShop";
	end;

OnBuyItem:
	// Apply VIP discount (20% off)
	for (.@i = 0; .@i < getarraysize(@bought_nameid); .@i++) {
		.@item = @bought_nameid[.@i];
		.@qty = @bought_quantity[.@i];
		.@price = @bought_price[.@i];

		// Calculate discounted price
		.@final_price = (.@price * 80) / 100;  // 20% off

		if (Zeny < (.@final_price * .@qty)) {
			mes "Not enough zeny!";
			close;
		}

		Zeny -= (.@final_price * .@qty);
		getitem .@item, .@qty;

		mes "Purchased " + .@qty + "x " + getitemname(.@item);
		mes "VIP Price: " + (.@final_price * .@qty) + " Zeny";
		mes "You saved: " + ((.@price - .@final_price) * .@qty) + " Zeny!";
	}

	deletearray @bought_nameid, getarraysize(@bought_nameid);
	deletearray @bought_quantity, getarraysize(@bought_quantity);
	deletearray @bought_price, getarraysize(@bought_price);
	close;

OnInit:
	// Add VIP-exclusive items
	npcshopitem "VIPShop", 501, 50, 502, 100, 503, 200, 607, 5000;
	end;
}
```

---

## Regular Expressions (PCRE)

### Basic Pattern Matching

```c
prontera,159,159,4	script	PCRE Test	123,{
	mes "[PCRE Test]";
	mes "Enter a string to test:";
	input .@input$;

	// Email validation
	if (preg_match("^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$", .@input$)) {
		mes "Valid email address!";
	} else {
		mes "Invalid email.";
	}
	next;

	// Username validation (alphanumeric, 3-16 chars)
	if (preg_match("^[a-zA-Z0-9_]{3,16}$", .@input$)) {
		mes "Valid username!";
	} else {
		mes "Invalid username.";
		mes "Must be 3-16 alphanumeric characters.";
	}
	next;

	// Extract numbers
	if (preg_match("\\d+", .@input$, .@matches$)) {
		mes "Found number: " + .@matches$[0];
	}
	close;
}
```

---

### Advanced PCRE Usage

```c
// Chat command parser
prontera,160,160,4	script	Command Parser	123,{
OnInit:
	bindatcmd("test", strnpcinfo(3) + "::OnCommand", 0, 100);
	end;

OnCommand:
	// Parse: @test <action> <target> <value>
	// Example: @test give PlayerName 1000000

	.@cmd$ = implode(.@atcmd_parameters$, " ");

	if (preg_match("^(give|take)\\s+(\\w+)\\s+(\\d+)$", .@cmd$, .@matches$)) {
		.@action$ = .@matches$[1];   // "give" or "take"
		.@target$ = .@matches$[2];   // player name
		.@amount = atoi(.@matches$[3]);  // amount

		.@target_id = getcharid(0, .@target$);
		if (.@target_id == 0) {
			dispbottom "Player not found: " + .@target$;
			end;
		}

		if (.@action$ == "give") {
			attachrid(.@target_id);
			Zeny += .@amount;
			detachrid();
			dispbottom "Gave " + .@amount + " Zeny to " + .@target$;
		} else if (.@action$ == "take") {
			attachrid(.@target_id);
			if (Zeny >= .@amount) {
				Zeny -= .@amount;
				detachrid();
				dispbottom "Took " + .@amount + " Zeny from " + .@target$;
			} else {
				detachrid();
				dispbottom "Player doesn't have enough zeny!";
			}
		}
	} else {
		dispbottom "Usage: @test <give|take> <player> <amount>";
	}
	end;
}
```

---

### String Replacement with PCRE

```c
prontera,161,161,4	script	PCRE Replace	123,{
	mes "[String Replacement]";

	.@text$ = "Hello World! This is a test.";
	mes "Original: " + .@text$;

	// Replace "World" with "rAthena"
	.@result$ = preg_replace("World", "rAthena", .@text$);
	mes "Replaced: " + .@result$;

	// Remove all numbers
	.@text2$ = "Item123Price456Zeny789";
	.@result$ = preg_replace("\\d+", "", .@text2$);
	mes "No numbers: " + .@result$;

	// Replace multiple spaces with single space
	.@text3$ = "Too    many     spaces";
	.@result$ = preg_replace("\\s+", " ", .@text3$);
	mes "Fixed: " + .@result$;

	close;
}
```

---

## SQL Integration

### Basic SQL Queries

```c
prontera,162,162,4	script	SQL Examples	123,{
	mes "[SQL Examples]";

	// SELECT query
	.@nb = query_sql("SELECT name, base_level FROM `char` WHERE account_id = " + getcharid(3) + " ORDER BY base_level DESC LIMIT 5", .@name$, .@level);

	mes "Your characters:";
	for (.@i = 0; .@i < .@nb; .@i++) {
		mes "- " + .@name$[.@i] + " (Lv. " + .@level[.@i] + ")";
	}
	next;

	// Count query
	.@count = query_sql("SELECT COUNT(*) FROM `char` WHERE online = 1", .@online);
	mes "Online players: " + .@online;
	next;

	// INSERT query
	query_sql("INSERT INTO custom_table (char_id, data, value) VALUES (" + getcharid(0) + ", 'test', 100)");
	mes "Data inserted!";

	close;
}
```

---

### Advanced SQL Patterns

```c
// Leaderboard system
prontera,163,163,4	script	Leaderboard	123,{
	mes "[Leaderboard]";
	mes "Top 10 Players by Base Level:";

	.@nb = query_sql("SELECT name, base_level, job_level FROM `char` ORDER BY base_level DESC, job_level DESC LIMIT 10", .@name$, .@blvl, .@jlvl);

	for (.@i = 0; .@i < .@nb; .@i++) {
		mes (.@i + 1) + ". " + .@name$[.@i] + " - Lv." + .@blvl[.@i] + "/" + .@jlvl[.@i];
	}
	next;

	// Custom achievement tracking
	mes "Your achievements:";
	.@count = query_sql("SELECT achievement_name, progress FROM custom_achievements WHERE char_id = " + getcharid(0), .@ach_name$, .@progress);

	if (.@count == 0) {
		mes "No achievements yet.";
	} else {
		for (.@i = 0; .@i < .@count; .@i++) {
			mes "- " + .@ach_name$[.@i] + ": " + .@progress[.@i] + "%";
		}
	}
	close;
}
```

---

### SQL Error Handling

```c
prontera,164,164,4	script	SQL Safety	123,{
	mes "[SQL Safety]";

	// Always escape user input!
	mes "Enter player name:";
	input .@search$;

	// BAD - SQL Injection vulnerable!
	// query_sql("SELECT * FROM `char` WHERE name = '" + .@search$ + "'");

	// GOOD - Use escape_sql()
	.@safe$ = escape_sql(.@search$);
	.@nb = query_sql("SELECT name, base_level FROM `char` WHERE name = '" + .@safe$ + "'", .@name$, .@level);

	if (.@nb == 0) {
		mes "Player not found.";
	} else {
		mes "Found: " + .@name$ + " (Lv." + .@level + ")";
	}
	close;
}
```

---

### Database Logging System

```c
// Activity logger
-	script	ActivityLogger	-1,{
OnPCLoginEvent:
	// Log player login
	query_sql("INSERT INTO activity_log (char_id, char_name, action, timestamp) VALUES (" +
		getcharid(0) + ", '" + escape_sql(strcharinfo(0)) + "', 'login', NOW())");
	end;

OnPCLogoutEvent:
	// Log player logout
	query_sql("INSERT INTO activity_log (char_id, char_name, action, timestamp) VALUES (" +
		getcharid(0) + ", '" + escape_sql(strcharinfo(0)) + "', 'logout', NOW())");
	end;

OnPCKillEvent:
	// Log player kills
	.@mob_id = killedrid;
	.@mob_name$ = getmonsterinfo(.@mob_id, MOB_NAME);

	query_sql("INSERT INTO kill_log (char_id, mob_id, mob_name, timestamp) VALUES (" +
		getcharid(0) + ", " + .@mob_id + ", '" + escape_sql(.@mob_name$) + "', NOW())");
	end;
}

// View logs
prontera,165,165,4	script	View Logs	123,{
	if (getgmlevel() < 99) {
		mes "Access denied.";
		close;
	}

	mes "[Activity Logs]";
	mes "Recent activity:";

	.@nb = query_sql("SELECT char_name, action, timestamp FROM activity_log ORDER BY timestamp DESC LIMIT 20", .@name$, .@action$, .@time$);

	for (.@i = 0; .@i < .@nb; .@i++) {
		mes .@time$[.@i] + " - " + .@name$[.@i] + " (" + .@action$[.@i] + ")";
	}
	close;
}
```

---

## Performance Optimization

### freeloop() - Critical for Large Loops

```c
prontera,166,166,4	script	Optimization	123,{
	mes "[Performance Test]";

	// WITHOUT freeloop (slow, causes lag)
	.@start = gettimetick(2);
	for (.@i = 0; .@i < 10000; .@i++) {
		.@dummy++;
	}
	.@time1 = gettimetick(2) - .@start;
	mes "Without freeloop: " + .@time1 + "ms";

	// WITH freeloop (fast, no lag)
	.@start = gettimetick(2);
	freeloop(1);
	for (.@i = 0; .@i < 10000; .@i++) {
		.@dummy++;
	}
	freeloop(0);
	.@time2 = gettimetick(2) - .@start;
	mes "With freeloop: " + .@time2 + "ms";

	close;
}
```

**Important**: ALWAYS disable freeloop after use!

---

### Batch Operations

```c
// BAD - Multiple database calls
for (.@i = 0; .@i < 100; .@i++) {
	query_sql("INSERT INTO log (id, value) VALUES (" + .@i + ", " + .@val[.@i] + ")");
}

// GOOD - Single batch insert
.@query$ = "INSERT INTO log (id, value) VALUES ";
for (.@i = 0; .@i < 100; .@i++) {
	.@query$ += "(" + .@i + ", " + .@val[.@i] + ")";
	if (.@i < 99) .@query$ += ", ";
}
query_sql(.@query$);
```

---

### Cache Frequently Accessed Data

```c
-	script	CacheSystem	-1,{
OnInit:
	// Cache item prices at server start
	freeloop(1);
	for (.@i = 501; .@i <= 1000; .@i++) {
		.@price = getiteminfo(.@i, ITEMINFO_BUY);
		if (.@price > 0) {
			setd("$ItemPrice_" + .@i, .@price);
		}
	}
	freeloop(0);
	debugmes "Cached " + (.@i - 501) + " item prices.";
	end;
}

// Access cached data (fast)
prontera,167,167,4	script	Price Checker	123,{
	mes "Item ID:";
	input .@item_id;

	// Fast lookup from cache
	.@price = getd("$ItemPrice_" + .@item_id);
	if (.@price == 0) {
		mes "Item not found.";
	} else {
		mes getitemname(.@item_id) + ": " + .@price + " Zeny";
	}
	close;
}
```

---

### Optimize String Operations

```c
// BAD - Repeated string concatenation
.@str$ = "";
for (.@i = 0; .@i < 100; .@i++) {
	.@str$ = .@str$ + "Item" + .@i + ",";  // Slow!
}

// BETTER - Use array + implode
for (.@i = 0; .@i < 100; .@i++) {
	.@parts$[.@i] = "Item" + .@i;
}
.@str$ = implode(.@parts$, ",");  // Fast!
```

---

## Advanced NPC Patterns

### NPC Timers - Advanced Usage

```c
prontera,168,168,4	script	Timer Master	123,{
	mes "[Timer System]";
	mes "Timer examples:";
	next;

	switch (select("Start Countdown:Stop Timer:Check Status:Multiple Timers")) {
	case 1:
		mes "Starting 60-second countdown...";
		'countdown = 60;
		initnpctimer;
		close;

	case 2:
		stopnpctimer;
		mes "Timer stopped.";
		close;

	case 3:
		.@time = getnpctimer(0);
		mes "Elapsed time: " + (.@time / 1000) + " seconds";
		mes "Countdown remaining: " + 'countdown;
		close;

	case 4:
		mes "Starting multiple timers...";
		donpcevent strnpcinfo(3) + "::OnTimer1";
		donpcevent strnpcinfo(3) + "::OnTimer2";
		close;
	}

OnTimer1000:
	if ('countdown > 0) {
		'countdown--;
		if ('countdown % 10 == 0) {
			announce "Countdown: " + 'countdown + " seconds remaining!", bc_all;
		}
		setnpctimer 0;
		startnpctimer;
	} else {
		announce "Countdown finished!", bc_all;
		stopnpctimer;
	}
	end;

OnTimer1:
	announce "Timer 1 triggered!", bc_self;
	end;

OnTimer2:
	sleep 5000;
	announce "Timer 2 triggered (5 seconds later)!", bc_self;
	end;
}
```

---

### NPC Duplication Patterns

```c
// Template NPC
-	script	WarperTemplate	-1,{
	mes "[Warper]";
	mes "Warp to " + .map_name$ + "?";
	next;
	if (select("Yes:No") == 1) {
		warp .map$, .x, .y;
	}
	close;
}

// Duplicate warpers
prontera,150,150,4	duplicate(WarperTemplate)	Warp to Geffen	123,{
OnInit:
	.map_name$ = "Geffen";
	.map$ = "geffen";
	.x = 120;
	.y = 100;
	end;
}

prontera,151,150,4	duplicate(WarperTemplate)	Warp to Payon	123,{
OnInit:
	.map_name$ = "Payon";
	.map$ = "payon";
	.x = 70;
	.y = 100;
	end;
}

prontera,152,150,4	duplicate(WarperTemplate)	Warp to Morocc	123,{
OnInit:
	.map_name$ = "Morocc";
	.map$ = "morocc";
	.x = 156;
	.y = 93;
	end;
}
```

---

### Function Libraries

```c
// Utility function library
function	script	F_Util	{
	// F_Util("command", params...)
	.@cmd$ = getarg(0);

	if (.@cmd$ == "comma") {
		// Add comma separators to number
		// F_Util("comma", 1234567) -> "1,234,567"
		.@num = getarg(1);
		.@str$ = "" + .@num;
		.@len = getstrlen(.@str$);

		for (.@i = .@len - 3; .@i > 0; .@i -= 3) {
			.@str$ = insertchar(.@str$, ",", .@i);
		}
		return .@str$;

	} else if (.@cmd$ == "time_format") {
		// Format seconds to HH:MM:SS
		// F_Util("time_format", 3661) -> "01:01:01"
		.@sec = getarg(1);
		.@h = .@sec / 3600;
		.@m = (.@sec % 3600) / 60;
		.@s = .@sec % 60;

		return sprintf("%02d:%02d:%02d", .@h, .@m, .@s);

	} else if (.@cmd$ == "percent") {
		// Calculate percentage
		// F_Util("percent", 75, 200) -> 37.5
		return (getarg(1) * 100.0) / getarg(2);

	} else if (.@cmd$ == "clamp") {
		// Clamp value between min and max
		// F_Util("clamp", 150, 0, 100) -> 100
		.@val = getarg(1);
		.@min = getarg(2);
		.@max = getarg(3);

		if (.@val < .@min) return .@min;
		if (.@val > .@max) return .@max;
		return .@val;
	}

	return 0;
}

// Usage
prontera,169,169,4	script	Utility Test	123,{
	.@val = 1234567;
	mes "Formatted: " + callfunc("F_Util", "comma", .@val);

	.@time = 3661;
	mes "Time: " + callfunc("F_Util", "time_format", .@time);

	.@pct = callfunc("F_Util", "percent", 75, 200);
	mes "Percentage: " + .@pct + "%";

	.@clamped = callfunc("F_Util", "clamp", 150, 0, 100);
	mes "Clamped: " + .@clamped;
	close;
}
```

---

## Error Handling & Validation

### Input Validation

```c
prontera,170,170,4	script	Input Validator	123,{
	mes "[Input Validator]";

	// Validate integer input
	mes "Enter a number (1-100):";
	input .@num;

	if (.@num < 1 || .@num > 100) {
		mes "Error: Number must be between 1 and 100!";
		close;
	}

	// Validate string input
	mes "Enter your character name:";
	input .@name$;

	if (getstrlen(.@name$) < 4 || getstrlen(.@name$) > 23) {
		mes "Error: Name must be 4-23 characters!";
		close;
	}

	if (!preg_match("^[a-zA-Z0-9_]+$", .@name$)) {
		mes "Error: Name can only contain letters, numbers, and underscores!";
		close;
	}

	// Validate item exists
	mes "Enter item ID:";
	input .@item_id;

	if (getiteminfo(.@item_id, ITEMINFO_ID) == -1) {
		mes "Error: Item doesn't exist!";
		close;
	}

	mes "All validations passed!";
	close;
}
```

---

### Safe Resource Access

```c
prontera,171,171,4	script	Safe Access	123,{
	// Safe equipment access
	.@equip_pos = EQP_WEAPON;
	if (!getequipisequiped(.@equip_pos)) {
		mes "No weapon equipped!";
		close;
	}

	.@item_id = getequipid(.@equip_pos);
	if (.@item_id < 0) {
		mes "Error reading equipment!";
		close;
	}

	mes "Weapon: " + getitemname(.@item_id);
	next;

	// Safe array access
	setarray .@items[0], 501, 502, 503;
	.@index = 10;  // Out of bounds!

	if (.@index >= 0 && .@index < getarraysize(.@items)) {
		mes "Item: " + .@items[.@index];
	} else {
		mes "Error: Array index out of bounds!";
	}
	close;
}
```

---

## Complex Event Systems

### Tournament Bracket System

```c
-	script	Tournament	-1,{
OnInit:
	setarray $@bracket_maps$[0], "guild_vs1", "guild_vs2", "guild_vs3", "guild_vs4";
	end;

OnRegister:
	// Register player for tournament
	if ($@tournament_status != 0) {
		dispbottom "Tournament registration is closed!";
		end;
	}

	if (#tournament_registered) {
		dispbottom "You're already registered!";
		end;
	}

	$@participants[$ @participant_count] = getcharid(0);
	$@participant_names$[$@participant_count] = strcharinfo(0);
	$@participant_count++;
	#tournament_registered = 1;

	announce strcharinfo(0) + " registered for the tournament! (" + $@participant_count + "/16)", bc_all;
	end;

OnStart:
	if ($@participant_count < 2) {
		announce "Not enough participants!", bc_all;
		end;
	}

	// Shuffle participants
	callfunc("ArrayShuffle", $@participants);

	$@tournament_status = 1;
	$@current_round = 1;
	$@matches_in_round = $@participant_count / 2;

	announce "Tournament starting! Round 1 begins!", bc_all;
	donpcevent strnpcinfo(3) + "::OnMatchStart";
	end;

OnMatchStart:
	for (.@i = 0; .@i < $@matches_in_round; .@i++) {
		.@p1 = $@participants[.@i * 2];
		.@p2 = $@participants[.@i * 2 + 1];

		// Warp to arena
		.@map$ = $@bracket_maps$[.@i];
		attachrid(.@p1);
		warp .@map$, 50, 50;
		detachrid();

		attachrid(.@p2);
		warp .@map$, 100, 100;
		detachrid();

		announce "Match " + (.@i + 1) + ": " + $@participant_names$[.@i * 2] + " vs " + $@participant_names$[.@i * 2 + 1], bc_all;
	}
	end;

OnPCDieEvent:
	// Handle tournament death
	if ($@tournament_status == 0) end;

	// Check if player is in tournament map
	.@map$ = strcharinfo(3);
	for (.@i = 0; .@i < getarraysize($@bracket_maps$); .@i++) {
		if (.@map$ == $@bracket_maps$[.@i]) {
			// Player lost, warp out
			sleep2 3000;
			warp "prontera", 150, 150;

			announce strcharinfo(0) + " has been eliminated!", bc_all;

			// Check if round is complete
			// (Implementation continues...)
			break;
		}
	}
	end;
}
```

---

## Real-World Examples

### Complete Daily Quest System

```c
// Daily quest system with SQL backend
-	script	DailyQuestSystem	-1,{
OnInit:
	// Create table if not exists
	query_sql("CREATE TABLE IF NOT EXISTS daily_quests (" +
		"id INT AUTO_INCREMENT PRIMARY KEY, " +
		"char_id INT NOT NULL, " +
		"quest_id INT NOT NULL, " +
		"progress INT DEFAULT 0, " +
		"completed BOOLEAN DEFAULT FALSE, " +
		"date_started DATE NOT NULL, " +
		"date_completed DATE, " +
		"INDEX(char_id), " +
		"INDEX(date_started)" +
	")");

	// Define quests
	setarray .quest_names$[0], "Poring Hunter", "Material Gatherer", "Zeny Maker";
	setarray .quest_targets[0], 1002, 1113, 1002;  // Monster IDs
	setarray .quest_counts[0], 100, 50, 200;        // Required kills
	setarray .quest_rewards[0], 1000000, 500000, 2000000;  // Zeny rewards
	end;
}

prontera,172,172,4	script	Daily Quests	123,{
	mes "[Daily Quests]";
	mes "Available daily quests:";
	next;

	// Check for completed quests today
	.@today$ = gettimestr("%Y-%m-%d", 21);
	.@count = query_sql("SELECT quest_id FROM daily_quests WHERE char_id = " + getcharid(0) + " AND date_started = '" + .@today$ + "' AND completed = TRUE", .@completed_ids);

	// Display quests
	for (.@i = 0; .@i < getarraysize(getvariableofnpc(.quest_names$, "DailyQuestSystem")); .@i++) {
		.@completed = 0;
		for (.@j = 0; .@j < .@count; .@j++) {
			if (.@completed_ids[.@j] == .@i) {
				.@completed = 1;
				break;
			}
		}

		.@name$ = getvariableofnpc(.quest_names$[.@i], "DailyQuestSystem");
		.@target = getvariableofnpc(.quest_targets[.@i], "DailyQuestSystem");
		.@required = getvariableofnpc(.quest_counts[.@i], "DailyQuestSystem");
		.@reward = getvariableofnpc(.quest_rewards[.@i], "DailyQuestSystem");

		mes (.@i + 1) + ". " + .@name$;
		mes "   Kill " + .@required + "x " + getmonsterinfo(.@target, MOB_NAME);
		mes "   Reward: " + .@reward + " Zeny";
		if (.@completed) {
			mes "   ^00FF00COMPLETED^000000";
		}
	}

	next;
	mes "Select quest:";
	.@quest = select("Quest 1:Quest 2:Quest 3:Cancel") - 1;

	if (.@quest == 3) close;

	// Check if already completed today
	.@completed = query_sql("SELECT id FROM daily_quests WHERE char_id = " + getcharid(0) + " AND quest_id = " + .@quest + " AND date_started = '" + .@today$ + "' AND completed = TRUE", .@dummy);

	if (.@completed > 0) {
		mes "You've already completed this quest today!";
		close;
	}

	// Get current progress
	.@progress = 0;
	query_sql("SELECT progress FROM daily_quests WHERE char_id = " + getcharid(0) + " AND quest_id = " + .@quest + " AND date_started = '" + .@today$ + "'", .@progress);

	.@required = getvariableofnpc(.quest_counts[.@quest], "DailyQuestSystem");

	mes "Progress: " + .@progress + "/" + .@required;

	if (.@progress >= .@required) {
		mes "Quest complete! Claim reward?";
		next;
		if (select("Yes:No") == 1) {
			.@reward = getvariableofnpc(.quest_rewards[.@quest], "DailyQuestSystem");
			Zeny += .@reward;

			query_sql("UPDATE daily_quests SET completed = TRUE, date_completed = NOW() WHERE char_id = " + getcharid(0) + " AND quest_id = " + .@quest + " AND date_started = '" + .@today$ + "'");

			mes "Received " + .@reward + " Zeny!";
		}
	}
	close;
}

// Monster kill tracking
-	script	QuestTracker	-1,{
OnNPCKillEvent:
	.@mob_id = killedrid;
	.@today$ = gettimestr("%Y-%m-%d", 21);

	// Check if player has active quests for this mob
	for (.@i = 0; .@i < getarraysize(getvariableofnpc(.quest_targets, "DailyQuestSystem")); .@i++) {
		.@target = getvariableofnpc(.quest_targets[.@i], "DailyQuestSystem");

		if (.@target == .@mob_id) {
			// Check if quest is active
			.@count = query_sql("SELECT id, progress FROM daily_quests WHERE char_id = " + getcharid(0) + " AND quest_id = " + .@i + " AND date_started = '" + .@today$ + "' AND completed = FALSE", .@id, .@progress);

			if (.@count > 0) {
				// Increment progress
				.@new_progress = .@progress + 1;
				query_sql("UPDATE daily_quests SET progress = " + .@new_progress + " WHERE id = " + .@id);

				.@required = getvariableofnpc(.quest_counts[.@i], "DailyQuestSystem");
				dispbottom "Quest progress: " + .@new_progress + "/" + .@required;

				if (.@new_progress >= .@required) {
					dispbottom "Quest completed! Visit the Daily Quest NPC to claim your reward.";
				}
			} else {
				// Start quest automatically
				query_sql("INSERT INTO daily_quests (char_id, quest_id, progress, date_started) VALUES (" + getcharid(0) + ", " + .@i + ", 1, '" + .@today$ + "')");
				dispbottom "Daily quest started! Check the Daily Quest NPC for details.";
			}
		}
	}
	end;
}
```

---

## Best Practices Summary

### 1. Always Use freeloop for Large Loops
```c
freeloop(1);
for (.@i = 0; .@i < 10000; .@i++) {
	// Heavy processing
}
freeloop(0);
```

### 2. Validate All Input
```c
input .@value;
if (.@value < min || .@value > max) {
	mes "Invalid input!";
	close;
}
```

### 3. Escape SQL Input
```c
.@safe$ = escape_sql(.@user_input$);
query_sql("... WHERE name = '" + .@safe$ + "'");
```

### 4. Use Constants, Not Magic Numbers
```c
// BAD
if (getequipid(2) > 0)

// GOOD
if (getequipid(EQP_HAND_R) > 0)
```

### 5. Comment Complex Logic
```c
// Calculate damage with element modifier
.@element_mod = 100 + ((.@attacker_element - .@target_element) * 25);
.@damage = (.@base_damage * .@element_mod) / 100;
```

### 6. Use Functions for Reusable Code
```c
function	CalculateDiscount	{
	.@vip_level = getarg(0);
	.@base_price = getarg(1);
	return (.@base_price * (100 - (.@vip_level * 5))) / 100;
}
```

---

## Related References

- **Core Commands**: [KB_REF_ScriptCommandsCore.md]
- **Instance System**: [KB_REF_InstanceSystem.md]
- **Item Groups**: [KB_REF_ItemGroups.md]
- **Constants**: [KB_REF_Constants.md]
- **Database**: [KB_REF_DatabaseStructure.md]
- **Sample Scripts**: `doc/sample/`

---

**End of KB_REF_021 - Advanced Scripting Patterns & Techniques**
