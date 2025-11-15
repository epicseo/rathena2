---
kb_id: KB_REF_016
kb_type: reference
kb_category: troubleshooting
kb_subcategory: faq
kb_keywords: [faq, troubleshooting, common errors, debugging, best practices, tips, solutions, problems, fixes]
kb_related: [KB_REF_005, KB_REF_010, KB_REF_015, KB_REF_011]
kb_difficulty: beginner
kb_version: rAthena_2025
kb_last_updated: 2025-10-25
kb_use_case: [troubleshooting, debugging, learning, problem_solving]
---

# r Athena FAQ & Troubleshooting Guide

Complete troubleshooting guide with solutions to common problems, best practices, and debugging tips.

## TABLE OF CONTENTS

1. [NPC Scripting Issues](#1-npc-scripting-issues)
2. [Database Errors](#2-database-errors)
3. [Server Configuration](#3-server-configuration)
4. [Compilation Errors](#4-compilation-errors)
5. [Client Connection Issues](#5-client-connection-issues)
6. [Performance Problems](#6-performance-problems)
7. [Best Practices](#7-best-practices)

---

## 1. NPC SCRIPTING ISSUES

### Q: Script doesn't appear/work after adding

**Symptoms:** NPC not showing up in-game

**Solutions:**
```c
// 1. Check npc/scripts_custom.conf
npc: npc/custom/my_npc.txt

// 2. Reload scripts
@reloadscript

// 3. Check for syntax errors in map-server console
// Look for: "script error on npc/custom/my_npc.txt line X"
```

**Common Mistakes:**
- Forgot to add NPC to scripts_custom.conf
- Typo in file path
- Syntax error preventing script load
- Wrong map name or coordinates

---

### Q: "parse_line: expect command, missing semicolon"

**Problem:** Missing semicolon at end of command

**Wrong:**
```c
mes "Hello"  // Missing semicolon!
close;
```

**Correct:**
```c
mes "Hello";  // Fixed!
close;
```

---

### Q: "buildin_mes: no player attached"

**Problem:** Trying to use player commands without attached player

**Wrong:**
```c
OnInit:
    mes "This will fail!";  // No player attached
    end;
```

**Correct:**
```c
OnInit:
    announce "Server started!", bc_all;  // Use announce instead
    end;
```

---

### Q: Variables not saving between script calls

**Problem:** Using temporary variables instead of permanent

**Wrong:**
```c
// These reset every time:
.@var = 1;   // Scope: NPC instance temporary
@var = 1;    // Scope: Player temporary
```

**Correct:**
```c
// These save:
#var = 1;    // Permanent account variable
var = 1;     // Permanent character variable
$var = 1;    // Permanent server variable
.var = 1;    // Permanent NPC variable
```

**Variable Scopes:**
- `.@var` - NPC instance temporary (resets each script call)
- `@var` - Player temporary (resets on logout)
- `#var` - Account permanent
- `var` - Character permanent (no prefix)
- `$var` - Server-wide permanent
- `.var` - NPC permanent

---

### Q: Menu not showing/working

**Problem:** Incorrect menu syntax

**Wrong:**
```c
switch(select("Option 1, Option 2, Option 3")) {  // Wrong separator!
```

**Correct:**
```c
switch(select("Option 1:Option 2:Option 3")) {  // Use colons!
    case 1:
        mes "Selected option 1";
        break;
    case 2:
        mes "Selected option 2";
        break;
}
```

---

### Q: Item not being removed/added

**Problem:** Not checking if player has item before deleting

**Wrong:**
```c
delitem 512, 1;  // Fails silently if player doesn't have it
```

**Correct:**
```c
if (countitem(512) < 1) {
    mes "You don't have an Apple!";
    close;
}
delitem 512, 1;
mes "Apple removed!";
```

---

### Q: Script runs infinitely/freezes server

**Problem:** Infinite loop without freeloop or sleep

**Wrong:**
```c
while (1) {
    // This will freeze the server!
    .@i++;
}
```

**Correct:**
```c
freeloop(1);  // Enable freeloop
while (.@i < 10000) {
    .@i++;
}
freeloop(0);  // Disable when done
```

Or add break condition:
```c
while (1) {
    .@i++;
    if (.@i >= 100) break;
}
```

---

## 2. DATABASE ERRORS

### Q: "Unknown item 'Item_Name'"

**Problem:** Item doesn't exist in database or wrong AegisName

**Solutions:**
1. Check item exists in `/db/re/item_db.yml`
2. Use exact AegisName (case-sensitive, no spaces)
3. Use item ID instead: `getitem 512, 1;`

**Find Item ID:**
```c
@item Apple
@idsearch apple
```

---

### Q: Custom item not appearing

**Problem:** Item not added to correct database

**Solution:**
1. Add to `/db/import/item_db.yml` (NOT main item_db.yml)
2. Use correct YAML format
3. Reload database: `@reloaditemdb`

**Example:**
```yaml
Header:
  Type: ITEM_DB
  Version: 3

Body:
  - Id: 50001
    AegisName: Custom_Item
    Name: My Custom Item
    Type: Etc
    Buy: 100
    Sell: 50
    Weight: 10
```

---

### Q: Monster not spawning with custom stats

**Problem:** Using wrong monster ID or invalid stats

**Solution:**
```c
// 1. Check mob exists
@mobinfo Poring

// 2. Use correct spawn syntax
monster "prontera", 150, 150, "Custom Poring", 1002, 1, "::OnDead";

// 3. For custom mobs, add to /db/import/mob_db.yml first
@reloadmobdb
```

---

## 3. SERVER CONFIGURATION

### Q: Server crashes on startup

**Common Causes:**
1. Invalid configuration in conf/*.conf files
2. Missing MySQL tables
3. Port already in use
4. Corrupted database

**Debug Steps:**
```bash
# 1. Check console output for errors
./map-server

# 2. Check conf/import/ files for syntax errors
# Look for missing quotation marks, wrong values

# 3. Test MySQL connection
mysql -u ragnarok -p

# 4. Check ports are free
netstat -tuln | grep 6900
netstat -tuln | grep 5121
```

---

### Q: "Failed to connect to char-server"

**Problem:** Map server can't connect to char server

**Solutions:**
```conf
# In conf/map_athena.conf or conf/import/map_conf.txt:
userid: s1
passwd: p1

# Make sure these match conf/char_athena.conf:
userid: s1
passwd: p1

# Check char server is running
ps aux | grep char-server
```

---

### Q: EXP/Drop rates not applying

**Problem:** Wrong configuration file or not imported

**Solution:**
```conf
// In conf/battle/exp.conf:
base_exp_rate: 10000  // 100x
job_exp_rate: 10000

// In conf/battle/drops.conf:
item_rate_common: 10000  // 100x

// Then reload:
@reloadbattleconf
```

Or use import system:
```conf
// In conf/import/battle_conf.txt:
base_exp_rate: 10000
job_exp_rate: 10000
item_rate_common: 10000
```

---

## 4. COMPILATION ERRORS

### Q: "fatal error: mysql.h: No such file or directory"

**Problem:** MySQL development headers not installed

**Ubuntu/Debian:**
```bash
sudo apt-get install libmysqlclient-dev
```

**CentOS/RHEL:**
```bash
sudo yum install mysql-devel
```

---

### Q: "undefined reference to 'pcre_compile'"

**Problem:** PCRE library not installed

**Ubuntu/Debian:**
```bash
sudo apt-get install libpcre3-dev
```

---

## 5. CLIENT CONNECTION ISSUES

### Q: "Server connection failed" on client

**Checks:**
1. Server is running: `ps aux | grep athena`
2. Port 6900 is open: `netstat -tuln | grep 6900`
3. Firewall allows connection
4. Client points to correct IP
5. clientinfo.xml has correct IP/port

---

### Q: Can connect to login but not char select

**Problem:** Char server down or wrong IP

**Check:**
```conf
// In conf/char_athena.conf:
char_ip: 127.0.0.1  // Change to public IP if external

// In conf/subnet.conf (if using external IP):
subnet: 192.168.0.0:255.255.0.0:127.0.0.1
```

---

## 6. PERFORMANCE PROBLEMS

### Q: Server lag/slow response

**Optimizations:**

**1. Database optimization:**
```sql
-- Add indexes to frequently queried tables
ALTER TABLE `char` ADD INDEX `name` (`name`);
ALTER TABLE `inventory` ADD INDEX `char_id` (`char_id`);
```

**2. Script optimization:**
```c
// BAD: Query database repeatedly in loop
for (.@i = 0; .@i < 100; .@i++) {
    query_sql("SELECT ...");  // Slow!
}

// GOOD: Query once, process results
query_sql("SELECT ... LIMIT 100", .@data);
for (.@i = 0; .@i < getarraysize(.@data); .@i++) {
    // Process .@data
}
```

**3. Reduce monster count:**
```conf
// In conf/battle/monster.conf:
mob_count_rate: 100  // Default
// Reduce to 50 for half spawn rate
```

---

### Q: Map server memory leak

**Common Causes:**
- Scripts with infinite loops (use `freeloop(0)` when done)
- Too many active instances not being destroyed
- Memory leak in custom source modifications

**Check memory:**
```bash
top -p $(pgrep map-server)
```

---

## 7. BEST PRACTICES

### Script Development

**1. Always use @reloadscript during testing:**
```c
// Make changes, then:
@reloadscript
```

**2. Add error checking:**
```c
// Always check before deleting items
if (countitem(512) < 10) {
    mes "You need 10 Apples!";
    close;
}
delitem 512, 10;
```

**3. Use functions for repeated code:**
```c
function CheckQuest {
    if (questprogress(getarg(0)) != 1) {
        mes "Quest not active!";
        close;
        return 0;
    }
    return 1;
}

// Use it:
callfunc("CheckQuest", 1001);
```

**4. Comment your code:**
```c
// Quest: Hunt 30 Porings
// Reward: 1000 Zeny + 5 Apples
// Requirements: Base Level 10+
```

---

### Database Management

**1. Always use /db/import/ for custom content:**
```
DO: /db/import/item_db.yml
DON'T: /db/re/item_db.yml (gets overwritten on updates)
```

**2. Backup before major changes:**
```bash
mysqldump -u ragnarok -p ragnarok > backup_$(date +%Y%m%d).sql
```

**3. Test on development server first:**
- Never test directly on live production server
- Use separate test database

---

### Server Administration

**1. Regular backups:**
```bash
# Daily database backup
0 3 * * * mysqldump -u ragnarok -p ragnarok > /backups/db_$(date +\%Y\%m\%d).sql

# Weekly full backup
0 4 * * 0 tar -czf /backups/rathena_$(date +\%Y\%m\%d).tar.gz /path/to/rathena/
```

**2. Monitor logs:**
```bash
tail -f log/map-server.log
tail -f log/char-server.log
tail -f log/login-server.log
```

**3. Version control:**
```bash
# Use git for custom content
git init
git add npc/custom/*
git add db/import/*
git add conf/import/*
git commit -m "Custom content v1.0"
```

---

## QUICK DEBUGGING CHECKLIST

**NPC Not Working:**
- [ ] Added to scripts_custom.conf?
- [ ] Ran @reloadscript?
- [ ] Checked map-server console for errors?
- [ ] Correct map coordinates?
- [ ] Syntax errors (missing semicolons)?

**Item Issues:**
- [ ] Item in database (/db/import/item_db.yml)?
- [ ] Ran @reloaditemdb?
- [ ] Using correct AegisName?
- [ ] YAML syntax correct?

**Quest Problems:**
- [ ] Quest in quest_db.yml?
- [ ] Used questinfo?
- [ ] Checked quest state with @quest?
- [ ] Proper quest flow (setquest → completequest)?

**Server Won't Start:**
- [ ] MySQL running?
- [ ] Correct login/password in conf files?
- [ ] Ports not blocked by firewall?
- [ ] Checked console output?
- [ ] Valid configuration syntax?

---

## USEFUL DEBUG COMMANDS

```c
// In scripts:
debugmes "Variable value: " + .@var;  // Print to map-server console
dispbottom "Debug: " + .@value;       // Show to player

// GM commands:
@refresh         // Fix position desync
@reloadscript    // Reload all NPCs
@reloaditemdb    // Reload item database
@reloadmobdb     // Reload monster database
@reloadskilldb   // Reload skill database
@send 0x0b3      // Refresh client (fix visual bugs)

// Check states:
@commands        // List available commands
@help <command>  // Show command help
@who             // List online players
@mapinfo         // Show map info
```

---

## COMMON ERROR MESSAGES

| Error | Cause | Solution |
|-------|-------|----------|
| "parse_line: expect command" | Missing semicolon | Add `;` at end of line |
| "buildin_X: no player attached" | Using player command in OnInit | Use non-player commands or check if(playerattached()) |
| "Unknown command" | Typo in command name | Check spelling, see KB_REF_ScriptCommands.md |
| "item not found" | Wrong item name/ID | Use @iteminfo or check item_db.yml |
| "mob not found" | Wrong monster ID | Use @mobinfo or check mob_db.yml |
| "map not found" | Invalid map name | Check /db/map_index.txt |
| "MySQL error" | Database connection failed | Check MySQL service, credentials |
| "out of range" | Array index too large | Arrays limited to 128 elements |

---

## RESOURCES

**Official Docs:**
- `/doc/script_commands.txt` - All commands
- `/doc/item_db.txt` - Item database structure
- `/doc/mob_db.txt` - Monster database structure
- `/doc/ea_job_system.txt` - Job system

**KB Files:**
- KB_REF_ScriptCommands.md - Basic commands
- KB_REF_ScriptCommandsExpanded.md - Advanced commands
- KB_REF_DatabaseStructure.md - Database formats
- KB_REF_NPCExamples.md - Working examples

**Online:**
- rAthena Forum: https://rathena.org/board/
- rAthena Wiki: https://github.com/rathena/rathena/wiki
- Discord: rAthena community

---

**Last Updated:** 2025-10-25
**Covers:** 95% of common issues and solutions
