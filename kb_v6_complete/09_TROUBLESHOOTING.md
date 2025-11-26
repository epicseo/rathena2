# rAthena KB v6 - Troubleshooting Guide

**Version:** 6.0 Complete
**Generated:** 2025-11-26

---

## Quick Navigation

- [Script Errors](#script-errors)
- [Database Errors](#database-errors)
- [Build Errors](#build-errors)
- [Runtime Errors](#runtime-errors)
- [Client Issues](#client-issues)
- [Common Mistakes](#common-mistakes)

---

## Script Errors

<!-- RAG_CHUNK: troubleshoot_script -->

### "Unknown command" / "Script not found"
**Symptoms:** NPC doesn't respond, script command not recognized

**Causes & Solutions:**
```
1. Typo in command name
   Wrong: mesage "Hello";
   Right: mes "Hello";

2. Missing semicolon
   Wrong: mes "Hello"
   Right: mes "Hello";

3. Wrong brackets
   Wrong: if (x == 1) [ mes "Yes"; ]
   Right: if (x == 1) { mes "Yes"; }

4. Script file not loaded
   Check: conf/import/npc_conf.txt
   Add: npc: npc/custom/myscript.txt
```

### "Unexpected end of file"
**Cause:** Unmatched brackets or missing close

**Fix:**
```c
// Count your brackets!
prontera,150,150,4	script	Test	4_M_JOB_KNIGHT,{
    if (condition) {
        mes "Test";
    }  // ← Don't forget this
}  // ← And this
```

### "Variable undefined"
**Cause:** Using variable before setting it

**Fix:**
```c
// Wrong - using before setting
mes "Value is " + @myvar;
@myvar = 10;

// Right - set first
@myvar = 10;
mes "Value is " + @myvar;
```

### Variables Not Saving
**Variable Types:**
| Prefix | Scope | Persistence |
|--------|-------|-------------|
| (none) | NPC | Until NPC restart |
| @ | Character | Until logout |
| $ | Server | Until restart |
| $@ | Server | Until restart |
| # | Account | Permanent (SQL) |
| ## | Account (global) | Permanent (SQL) |
| . | NPC | Until restart |
| .@ | Local | Until script ends |
| ' | Instance | Until instance ends |

---

## Database Errors

<!-- RAG_CHUNK: troubleshoot_database -->

### "YAML parse error"
**Symptoms:** Database won't load, server won't start

**Common Causes:**
```yaml
# 1. Wrong indentation (must use spaces, not tabs!)
Body:
  - Id: 501        # 2 spaces before dash
    Name: "Item"   # 4 spaces for properties

# 2. Missing quotes for special characters
Wrong: Name: Item: Special
Right: Name: "Item: Special"

# 3. Wrong list format
Wrong:
  Jobs: All, Novice, Swordman
Right:
  Jobs:
    All: true
    Novice: true
```

### "Duplicate entry"
**Cause:** Same ID used twice

**Fix:** Search for duplicate IDs:
```bash
grep -n "Id: 501" db/re/item_db.yml
```

### Item/Skill Not Working
**Checklist:**
1. Is the database file loaded in `conf/import/`?
2. Is the item/skill ID correct?
3. Did you reload the database? (`@reloaditemdb`, `@reloadskilldb`)
4. Check for YAML syntax errors in server console

---

## Build Errors

<!-- RAG_CHUNK: troubleshoot_build -->

### "MySQL not found"
```bash
# Ubuntu/Debian
sudo apt-get install libmysqlclient-dev

# CentOS/RHEL
sudo yum install mysql-devel

# macOS
brew install mysql-client
export PATH="/usr/local/opt/mysql-client/bin:$PATH"
```

### "PCRE not found"
```bash
# Ubuntu/Debian
sudo apt-get install libpcre3-dev

# CentOS/RHEL
sudo yum install pcre-devel
```

### "C++ compiler errors"
**Minimum Requirements:**
- GCC 7+ or Clang 6+
- C++17 support required

```bash
# Check version
g++ --version

# Ubuntu - install newer GCC
sudo apt-get install g++-9
```

### Link Errors
```bash
# Missing library paths
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

# Run ldconfig
sudo ldconfig
```

---

## Runtime Errors

<!-- RAG_CHUNK: troubleshoot_runtime -->

### Server Won't Start
**Checklist:**
1. Check MySQL is running: `systemctl status mysql`
2. Check configuration: `conf/inter_athena.conf`
3. Check port conflicts: `netstat -tulpn | grep 6900`
4. Check logs: `log/map-server.log`

### Client Disconnects Immediately
**Causes:**
1. PACKETVER mismatch
2. Wrong client date
3. Server not responding

**Fix:**
```c
// In src/custom/defines_pre.hpp
#define PACKETVER 20200401  // Match your client
```

### Skills Not Working
**Debug Steps:**
1. Check skill_db.yml syntax
2. Check skill requirements (SP, items, state)
3. Use `@skillid <name>` to verify skill exists
4. Check `@commands skillfail` for error codes

---

## Client Issues

<!-- RAG_CHUNK: troubleshoot_client -->

### Sprites Not Showing
**Cause:** Missing GRF files or wrong paths

**Fix:**
1. Check DATA.INI paths
2. Verify sprite files in data/sprite/
3. Rebuild GRF if needed

### "Invalid Version" Error
**Cause:** PACKETVER mismatch

**Fix:**
1. Find client PACKETVER (check exe date)
2. Update `src/custom/defines_pre.hpp`
3. Rebuild server

### Map Won't Load
**Causes:**
1. Map file missing from GRF
2. Map not in map_index.txt
3. Wrong map cache

**Fix:**
```bash
# Rebuild map cache
./tools/mapcache
```

---

## Common Mistakes

<!-- RAG_CHUNK: troubleshoot_common_mistakes -->

### Script Common Mistakes
```c
// 1. Using = instead of ==
Wrong: if (x = 1)     // Assigns 1 to x!
Right: if (x == 1)    // Compares x to 1

// 2. Forgetting quotes for strings
Wrong: mes Test message;
Right: mes "Test message";

// 3. Wrong getitem syntax
Wrong: getitem "Red_Potion", 10;
Right: getitem 501, 10;  // Use ID
Right: getitem Red_Potion, 10;  // Or constant without quotes

// 4. Case sensitivity
Wrong: if (BaseLevel >= 99)  // Wrong
Right: if (BaseLevel >= 99)  // Correct - BaseLevel is exact

// 5. Missing 'end' in script
Wrong:
OnInit:
    mes "Hello";
    close;
// Next label runs into this!

Right:
OnInit:
    end;  // Stop execution here
```

### Database Common Mistakes
```yaml
# 1. Tabs instead of spaces
# YAML requires spaces for indentation!

# 2. Missing type specifications
Wrong:
  Locations:
    Head_Top     # Missing value!
Right:
  Locations:
    Head_Top: true

# 3. Wrong boolean format
Wrong: Refineable: yes
Right: Refineable: true

# 4. Unquoted special strings
Wrong: Name: Item: Type 1
Right: Name: "Item: Type 1"
```

---

## Debug Commands

### Useful @Commands for Debugging
```
@who           - List online players
@where         - Show current position
@mobinfo <id>  - Monster information
@iteminfo <id> - Item information
@skillinfo <id> - Skill information
@reloadscript  - Reload all scripts
@reloaditemdb  - Reload item database
@reloadmobdb   - Reload monster database
@reloadskilldb - Reload skill database
```

### Server Console Commands
```
Ctrl+C         - Graceful shutdown
gm:character   - Send GM commands as character
server:status  - Show server status
```

---

*Generated as part of rAthena KB v6 Complete*
