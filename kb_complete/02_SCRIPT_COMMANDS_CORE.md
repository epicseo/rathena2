# rAthena Script Commands - Core Reference
## Comprehensive Documentation for 603+ Script Commands

---

<!-- RAG_CHUNK: script_basics_001 -->
## Script Basics

### Script Structure
```
<map>,<x>,<y>,<dir>	script	<NPC Name>	<sprite>,{
    // Script code here
}

// Floating NPC (no location)
-	script	<NPC Name>	-1,{
    // Script code here
}

// Function definition
function	script	<function name>	{
    // Function code here
}
```

### Variable Types and Scopes

| Prefix | Scope | Extent | Example |
|--------|-------|--------|---------|
| (none) | Character | Permanent | `MyVar` |
| `@` | Character | Temporary | `@temp` |
| `$` | Global | Permanent | `$GlobalVar` |
| `$@` | Global | Temporary | `$@tempGlobal` |
| `.` | NPC | Temporary | `.npcVar` |
| `.@` | Scope | Temporary | `.@localVar` |
| `'` | Instance | Temporary | `'instanceVar` |
| `#` | Account (local) | Permanent | `#accountVar` |
| `##` | Account (global) | Permanent | `##globalAccVar` |

String variables end with `$`: `@name$`, `.@str$`, `$globalStr$`

### Built-in Character Variables
```
Zeny        - Current zeny amount
Hp          - Current HP
MaxHp       - Maximum HP
Sp          - Current SP
MaxSp       - Maximum SP
Ap          - Current AP (4th jobs)
MaxAp       - Maximum AP
BaseLevel   - Base level
JobLevel    - Job level
BaseExp     - Current base EXP
JobExp      - Current job EXP
NextBaseExp - EXP needed for next base level
NextJobExp  - EXP needed for next job level
Weight      - Current weight
MaxWeight   - Maximum weight capacity
StatusPoint - Available status points
SkillPoint  - Available skill points
Class       - Current job class ID
Sex         - 0=Female, 1=Male
Upper       - 0=Normal, 1=Advanced, 2=Baby
BaseClass   - Base 1-1 job class
BaseJob     - Normal job equivalent
Karma       - Karma points
Manner      - Manner rating
```

---

<!-- RAG_CHUNK: dialog_commands_001 -->
## Dialog Commands

### mes
**Syntax:** `mes "<string>"{,"<string>",...};`

Display message in NPC dialog window. Supports color codes and special formatting.

**Color Codes:**
```
^RRGGBB - Set text color (hex RGB)
^FF0000 - Red
^00FF00 - Green
^0000FF - Blue
^000000 - Black (reset)
```

**Special Tags (2011+ clients):**
```html
<NAVI>Text<INFO>map,x,y,0,000,flag</INFO></NAVI>  - Navigation link
<ITEM>Text<INFO>ItemID</INFO></ITEM>              - Item link
<URL>Text<INFO>http://url</INFO></URL>            - URL link
<QUEST>Text<INFO>QuestID</INFO></QUEST>           - Quest link
```

**Examples:**
```c
mes "[NPC Name]";
mes "Hello, " + strcharinfo(0) + "!";
mes "This is ^FF0000red^000000 text.";
mes "Line 1", "Line 2", "Line 3";  // Multiple lines
```

---

### next
**Syntax:** `next;`

Display 'Next' button, wait for click, then clear dialog for new content.

**Example:**
```c
mes "[Guide]";
mes "Welcome to Prontera!";
next;
mes "[Guide]";
mes "How can I help you?";
```

---

### close
**Syntax:** `close;`

Display 'Close' button and end script execution when clicked.

**Example:**
```c
mes "[NPC]";
mes "Goodbye!";
close;
// Code after close never executes
```

---

### close2
**Syntax:** `close2;`

Display 'Close' button but continue script execution. Must use `end;` to stop.

**Example:**
```c
mes "[Warper]";
mes "Teleporting you now...";
close2;
warp "prontera",155,180;
end;
```

---

### close3
**Syntax:** `close3;`

Like `close` but also clears any displayed cutin image.

---

### clear
**Syntax:** `clear;`

Clear dialog text without player interaction. Useful with `sleep2`.

**Example:**
```c
mes "Loading...";
sleep2 2000;
clear;
mes "Done!";
close;
```

---

<!-- RAG_CHUNK: menu_commands_001 -->
## Menu Commands

### menu
**Syntax:** `menu "<option>",<label>{,"<option>",<label>,...};`

Create selection menu. Sets `@menu` to selected option number (1-based).

**Special Features:**
- Use `:` to group options: `"Option A:Option B",L_Label`
- Use `-` as label to continue after menu
- Empty strings `""` hide options (for dynamic menus)

**Example:**
```c
menu "Option 1",L_Opt1,"Option 2",L_Opt2,"Cancel",-;
mes "You cancelled.";
close;

L_Opt1:
    mes "You chose option 1";
    close;

L_Opt2:
    mes "You chose option 2";
    close;
```

---

### select
**Syntax:** `select("<option>"{,"<option>",...})`

Returns selected option number (1-based). Also sets `@menu`.

**Example:**
```c
.@choice = select("Yes:No");
if (.@choice == 1) {
    mes "You said yes!";
} else {
    mes "You said no!";
}
close;
```

---

### prompt
**Syntax:** `prompt("<option>"{,"<option>",...})`

Like `select` but returns 255 if player clicks Cancel.

**Example:**
```c
.@choice = prompt("Accept:Decline");
if (.@choice == 255) {
    mes "You cancelled.";
    close;
}
```

---

<!-- RAG_CHUNK: input_commands_001 -->
## Input Commands

### input
**Syntax:** `input(<variable>{,<min>,<max>})`

Get player input. Variable type determines input type (number or string).

**Return Values:**
- `0` - Input within range
- `1` - Input above max
- `-1` - Input below min

**Examples:**
```c
// Number input
input .@amount;
mes "You entered: " + .@amount;

// String input
input .@name$;
mes "Hello, " + .@name$;

// Bounded input (1-100)
if (input(.@num, 1, 100) != 0) {
    mes "Please enter 1-100!";
    close;
}
```

---

<!-- RAG_CHUNK: variable_commands_001 -->
## Variable Commands

### set
**Syntax:** `set <variable>,<expression>{,<char_id>};`

Assign value to variable. Can also use direct assignment: `.@x = 100;`

**Examples:**
```c
set .@count, 10;
set .@name$, "Player";
set @points, @points + 100;

// Direct assignment (preferred)
.@count = 10;
.@name$ = "Player";
@points += 100;
```

---

### setd
**Syntax:** `setd "<variable name>",<value>{,<char_id>};`

Set variable by dynamic name string.

**Example:**
```c
setd ".@item" + .@i, 501;  // Sets .@item0, .@item1, etc.
```

---

### getd
**Syntax:** `getd("<variable name>")`

Get variable reference by dynamic name string.

**Example:**
```c
.@val = getd("$var" + .@suffix);
```

---

### getvariableofnpc
**Syntax:** `getvariableofnpc(<variable>,"<npc name>")`

Access NPC variable from another NPC.

**Example:**
```c
.@otherVar = getvariableofnpc(.counter, "OtherNPC");
set getvariableofnpc(.counter, "OtherNPC"), 100;
```

---

### getvar
**Syntax:** `getvar(<variable>,<char_id>);`

Get player variable from specific character.

---

<!-- RAG_CHUNK: array_commands_001 -->
## Array Commands

### setarray
**Syntax:** `setarray <array>[<index>],<value>{,<value>,...};`

Initialize array with values starting at index.

**Example:**
```c
setarray .@items[0], 501, 502, 503, 504, 505;
setarray .@names$[0], "Apple", "Banana", "Cherry";
```

---

### getarraysize
**Syntax:** `getarraysize(<array>)`

Returns highest index + 1 (not count of non-empty elements).

**Example:**
```c
setarray .@arr[0], 1, 2, 3;
.@size = getarraysize(.@arr);  // Returns 3
```

---

### cleararray
**Syntax:** `cleararray <array>[<index>],<value>,<count>;`

Set `count` elements to `value` starting at `index`.

**Example:**
```c
cleararray .@arr[0], 0, 10;  // Set first 10 elements to 0
```

---

### copyarray
**Syntax:** `copyarray <dest array>[<index>],<source array>[<index>],<count>;`

Copy array elements.

**Example:**
```c
copyarray .@dest[0], .@source[0], 10;
```

---

### deletearray
**Syntax:** `deletearray <array>[<index>]{,<count>};`

Delete array elements, shifting remaining elements down.

**Example:**
```c
deletearray .@arr[2], 1;  // Delete element at index 2
deletearray .@arr[0];     // Delete all elements
```

---

### inarray
**Syntax:** `inarray(<array>,<value>)`

Find value in array. Returns index or -1 if not found.

**Example:**
```c
setarray .@items[0], 501, 502, 503;
.@idx = inarray(.@items, 502);  // Returns 1
```

---

### countinarray
**Syntax:** `countinarray(<array1>,<array2>)`

Count matching elements between two arrays.

---

<!-- RAG_CHUNK: flow_control_001 -->
## Flow Control

### if / else
**Syntax:**
```c
if (<condition>) <statement>;
if (<condition>) { <statements> }
if (<condition>) { } else { }
if (<condition>) { } else if (<condition>) { }
```

**Examples:**
```c
if (BaseLevel >= 99)
    mes "Max level!";

if (Zeny >= 1000) {
    Zeny -= 1000;
    getitem 501, 10;
} else {
    mes "Not enough zeny!";
}
```

---

### switch / case
**Syntax:**
```c
switch (<expression>) {
    case <value>:
        <statements>
        break;
    default:
        <statements>
        break;
}
```

**Example:**
```c
switch (Class) {
    case Job_Novice:
        mes "You're a Novice!";
        break;
    case Job_Swordman:
    case Job_Knight:
        mes "Melee class!";
        break;
    default:
        mes "Other class.";
        break;
}
```

---

### for
**Syntax:** `for (<init>; <condition>; <iteration>) <statement>;`

**Example:**
```c
for (.@i = 0; .@i < 10; .@i++) {
    mes "Count: " + .@i;
}
```

---

### while
**Syntax:** `while (<condition>) <statement>;`

**Example:**
```c
.@i = 0;
while (.@i < 5) {
    mes "Loop " + .@i;
    .@i++;
}
```

---

### do...while
**Syntax:** `do { <statements> } while (<condition>);`

**Example:**
```c
.@i = 0;
do {
    mes "At least once!";
    .@i++;
} while (.@i < 3);
```

---

### goto
**Syntax:** `goto <label>;`

Jump to label. **Avoid when possible** - use functions instead.

**Example:**
```c
goto L_Skip;
mes "This won't show";
L_Skip:
mes "Jumped here";
```

---

### end
**Syntax:** `end;`

Stop script execution immediately.

---

<!-- RAG_CHUNK: function_commands_001 -->
## Function Commands

### callfunc
**Syntax:** `callfunc("<function>"{,<arg>,...});`

Call global function NPC. Returns value if function uses `return`.

**Example:**
```c
// Call with arguments
callfunc("MyFunc", 100, "test");

// Get return value
.@result = callfunc("Calculate", 5, 10);
```

---

### callsub
**Syntax:** `callsub(<label>{,<arg>,...});`

Call subroutine within same script.

**Example:**
```c
callsub(S_GiveReward, 501, 10);
close;

S_GiveReward:
    getitem getarg(0), getarg(1);
    return;
```

---

### getarg
**Syntax:** `getarg(<index>{,<default>})`

Get argument passed to function/subroutine.

**Example:**
```c
.@item = getarg(0);       // First argument
.@amount = getarg(1, 1);  // Second argument, default 1
```

---

### getargcount
**Syntax:** `getargcount()`

Returns number of arguments passed.

---

### return
**Syntax:** `return {<value>};`

Return from function/subroutine, optionally with value.

---

### function (local)
**Syntax:**
```c
function <name>;           // Declaration
function <name> { }        // Definition
<name>({<args>});          // Call
```

**Example:**
```c
function MyFunc;

mes MyFunc(5, 10);
close;

function MyFunc {
    return getarg(0) + getarg(1);
}
```

---

### is_function
**Syntax:** `is_function("<name>")`

Check if function exists. Returns 1 or 0.

---

<!-- RAG_CHUNK: label_events_001 -->
## Labels and Events

### Special Labels
```c
OnInit:              // Script load/reload
OnInterIfInit:       // Map-char server connect
OnInterIfInitOnce:   // First map-char connect only

// Time-based
OnClock<HHMM>:       // Specific time (OnClock1200:)
OnMinute<MM>:        // Every hour at minute
OnHour<HH>:          // Every day at hour
On<Day><HHMM>:       // Weekly (OnMon0900:)
OnDay<MMDD>:         // Yearly (OnDay0101:)

// Player events
OnPCLoginEvent:      // Player login
OnPCLogoutEvent:     // Player logout
OnPCBaseLvUpEvent:   // Base level up
OnPCJobLvUpEvent:    // Job level up
OnPCDieEvent:        // Player death (killerrid set)
OnPCKillEvent:       // Player kills player (killedrid set)
OnNPCKillEvent:      // Player kills monster (killedrid, killedgid set)
OnPCLoadMapEvent:    // Enter map with loadevent flag

// NPC trigger
OnTouch:             // Player enters trigger area
OnTouch_:            // Single instance OnTouch
OnTouchNPC:          // Monster enters trigger area

// WoE events
OnAgitStart:         // WoE FE start
OnAgitEnd:           // WoE FE end
OnAgitInit:          // WoE FE data loaded
OnAgitStart2:        // WoE SE start
OnAgitEnd2:          // WoE SE end
OnAgitStart3:        // WoE TE start
OnAgitEnd3:          // WoE TE end

// Instance events
OnInstanceInit:      // Instance created
OnInstanceDestroy:   // Instance destroyed

// Whisper
OnWhisperGlobal:     // Player whispers NPC (@whispervar0$-9$)
```

---

<!-- RAG_CHUNK: operators_001 -->
## Operators Reference

### Arithmetic
```c
+   Addition (also string concatenation)
-   Subtraction
*   Multiplication
/   Integer division
%   Modulo (remainder)
```

### Comparison
```c
==  Equal
!=  Not equal
>   Greater than
<   Less than
>=  Greater or equal
<=  Less or equal
```

### Logical
```c
&&  AND
||  OR
!   NOT
```

### Bitwise
```c
&   AND
|   OR
^   XOR
~   NOT (complement)
<<  Left shift
>>  Right shift
```

### Assignment
```c
=    Assign
+=   Add and assign
-=   Subtract and assign
*=   Multiply and assign
/=   Divide and assign
%=   Modulo and assign
&=   Bitwise AND assign
|=   Bitwise OR assign
^=   Bitwise XOR assign
<<=  Left shift assign
>>=  Right shift assign
```

### Ternary
```c
<condition> ? <true_value> : <false_value>
```

**Example:**
```c
mes "You are " + (Sex ? "male" : "female");
```

---

#rathena #script #commands #mes #menu #input #variables #arrays #functions #labels #operators
