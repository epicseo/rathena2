# 06_DEBUG.md
<!-- repo: rathena | branch: claude/github-to-kb-converter-0137h2Ti2PFSsGmn6Xrp3xko | commit: 721d46e | generated: 2025-11-28 -->
<!-- tags: debug, troubleshooting, errors, logging -->

## Contents
- [Common Errors](#common-errors)
- [Debug Tools](#debug-tools)
- [Logging System](#logging-system)
- [Console Commands](#console-commands)
- [Troubleshooting Guide](#troubleshooting-guide)

---

## Common Errors
<!-- chunk: 06-errors | keywords: error, exception, fix -->

### Connection Errors
<!-- chunk: 06-connection | keywords: connection, socket, network -->

#### MySQL Connection Failed
```
[Error]: Couldn't connect with uname='ragnarok',host='127.0.0.1',port='3306',database='ragnarok'
```
**Cause:** MySQL server not running or wrong credentials
**Fix:**
1. Verify MySQL is running: `systemctl status mysql`
2. Check credentials in `conf/inter_athena.conf`
3. Verify database exists: `mysql -u ragnarok -p -e "SHOW DATABASES;"`
4. Check MySQL socket: use `127.0.0.1` on Windows, `localhost` on Linux

#### Inter-Server Connection Failed
```
[Error]: Can't connect to login-server (ip: 127.0.0.1, port: 6900)
```
**Cause:** Login server not running or port blocked
**Fix:**
1. Start login-server first
2. Check `login_port` in `conf/login_athena.conf`
3. Verify firewall allows port 6900
4. Check `userid`/`passwd` match in all server configs

#### Client Connection Refused
```
Failed to connect to server
```
**Cause:** Server not reachable from client
**Fix:**
1. Set `char_ip` and `map_ip` in config to public IP
2. Forward ports: 6900, 6121, 5121
3. Check PACKETVER matches client
4. → See [[05_CONFIG#server-configuration-files]]

### Database Errors
<!-- chunk: 06-database | keywords: sql, database, query -->

#### Table Doesn't Exist
```
[SQL]: DB error - Table 'ragnarok.char' doesn't exist
```
**Cause:** Database not initialized
**Fix:**
1. Import main.sql: `mysql -u root -p ragnarok < sql-files/main.sql`
2. Import logs.sql: `mysql -u root -p ragnarok < sql-files/logs.sql`
3. For web server: `mysql -u root -p ragnarok < sql-files/web.sql`

#### Character Data Corruption
```
[Error]: mmo_char_fromsql: Loaded invalid character data
```
**Cause:** Database integrity issue
**Fix:**
1. Check character table for NULL values
2. Run: `UPDATE char SET last_map='prontera' WHERE last_map IS NULL;`
3. Verify save/load cycle with `char_checkdb: yes`

### Script Errors
<!-- chunk: 06-script | keywords: script, npc, parse -->

#### Script Parse Error
```
[Error]: parse_line: syntax error at >;<
script error on npc/custom/my_npc.txt line 15
```
**Cause:** Invalid script syntax
**Fix:**
1. Check line 15 for missing semicolons, quotes, or braces
2. Validate brackets match: `{` `}` `[` `]` `(` `)`
3. Check string escaping: use `\"` inside strings
4. → See [[02_CORE_API#script-commands]]

#### Undefined Label
```
[Error]: script:goto: unknown label 'L_MyLabel'
```
**Cause:** Label doesn't exist or typo
**Fix:**
1. Define label: `L_MyLabel:`
2. Check case sensitivity
3. Ensure label is in same script scope

#### Variable Type Mismatch
```
[Warning]: script: getd: variable name contains invalid characters
```
**Cause:** Wrong variable syntax
**Fix:**
1. String vars end with `$`: `@name$`
2. Array index in brackets: `@array[0]`
3. → See [[02_CORE_API#variable-scope-prefixes]]

### Authentication Errors
<!-- chunk: 06-auth | keywords: login, password, ban -->

#### Invalid Password
```
[Info]: Connection refused (account: test, pass: ****, state: 1)
```
**State Codes:**
- `0` = Account OK
- `1` = Invalid password
- `2` = Expired account
- `5` = IP banned
- `6` = Account banned

**Fix:**
1. Reset password in `login` table
2. Check `use_MD5_passwords` setting
3. Verify client uses same password format

#### IP Banned
```
[Info]: Connection refused (IP banned)
```
**Cause:** Too many failed login attempts
**Fix:**
1. Clear ban: `DELETE FROM ipbanlist WHERE list='x.x.x.x';`
2. Adjust `ipban_dynamic_pass_failure_ban_limit`
3. Check `ipbanlist` table for entries

---

## Debug Tools
<!-- chunk: 06-tools | keywords: debug, gdb, valgrind -->

### Compile-Time Debug

**Enable Debug Build:**
```bash
cmake -DCMAKE_BUILD_TYPE=Debug ..
make
```

**Debug Symbols:**
- Adds `-g` flag to compilation
- Enables `ShowDebug()` messages
- Keeps function names for stack traces

### Runtime Debug Commands

| Command | Description |
|---------|-------------|
| `@mapinfo` | Show current map info and flags |
| `@gat` | Display terrain cell data |
| `@displayskill <id>` | Test skill animation |
| `@displaystatus <type>` | Test status display |
| `@send <packet>` | Send raw packet (dangerous) |

### GDB Debugging

```bash
# Start with GDB
gdb ./map-server

# Common commands
run                    # Start execution
bt                     # Backtrace on crash
info locals           # Show local variables
print variable        # Print variable value
break function        # Set breakpoint
continue              # Continue execution
```

### Valgrind Memory Check

```bash
valgrind --leak-check=full ./map-server

# Common errors:
# - "Invalid read" = Reading freed/unallocated memory
# - "Invalid write" = Writing to freed memory
# - "Definitely lost" = Memory leak
```

---

## Logging System
<!-- chunk: 06-logging | keywords: log, console, file -->

### Console Message Types

| Function | Color | Use Case |
|----------|-------|----------|
| `ShowMessage` | White | General info |
| `ShowStatus` | Green | Status updates |
| `ShowInfo` | Cyan | Informational |
| `ShowNotice` | Yellow | Important notices |
| `ShowWarning` | Yellow/Bold | Warnings |
| `ShowError` | Red | Errors |
| `ShowFatalError` | Red/Bold | Fatal (exits) |
| `ShowDebug` | Cyan | Debug only |

### Console Logging Settings

**In server config files:**
```
// Message type flags (add values):
// 1=Warning, 2=Error/SQL, 4=Debug
console_msg_log: 7    // Log all types

// Console output path
console_log_filepath: ./log/map-msg_log.log

// Hide message types (add values):
// 1=Info, 2=Status, 4=Notice, 8=Warning, 16=Error, 32=Debug
console_silent: 0     // Show everything
```

### Database Logging (logs.sql)

**Log Tables:**

| Table | Content |
|-------|---------|
| `atcommandlog` | GM command usage |
| `branchlog` | Dead Branch usage |
| `chatlog` | Chat messages |
| `loginlog` | Login attempts |
| `mvplog` | MVP kills |
| `npclog` | NPC interactions |
| `picklog` | Item transactions |
| `zenylog` | Zeny transactions |

**Enabling Logs (log_athena.conf):**
```
// Enable logging
enable_logs: yes

// What to log (bitmask)
log_filter: 1     // Items only
log_filter: 63    // Everything

// Log destinations
log_chat: 1       // To database
log_chat: 2       // To file
```

### Log File Locations

| File | Content |
|------|---------|
| `log/login.log` | Login server events |
| `log/login-msg_log.log` | Login console |
| `log/char-msg_log.log` | Char console |
| `log/map-msg_log.log` | Map console |
| `log/inter.log` | Inter-server events |

---

## Console Commands
<!-- chunk: 06-console | keywords: console, terminal, server -->

### Server Console (when console: on)

| Command | Server | Description |
|---------|--------|-------------|
| `shutdown` | All | Graceful shutdown |
| `exit` | All | Immediate exit |
| `alive` | All | Check server status |
| `reloadscript` | Map | Reload NPC scripts |
| `reloadbattleconf` | Map | Reload battle config |
| `reloadatcommand` | Map | Reload @commands |
| `reloadmotd` | Map | Reload MOTD |
| `kick <name>` | Map | Kick player |
| `gm <name> <level>` | Login | Set GM level |

### Enabling Console

```
// In server config
console: on
```

**Note:** Enabling console prevents output redirection (`>& log.file`)

---

## Troubleshooting Guide
<!-- chunk: 06-troubleshoot | keywords: guide, problem, solution -->

### Server Won't Start

1. **Check ports are free:**
   ```bash
   netstat -an | grep -E "6900|6121|5121"
   ```

2. **Check MySQL connection:**
   ```bash
   mysql -u ragnarok -p ragnarok -e "SELECT 1"
   ```

3. **Verify config syntax:**
   - No spaces around `:`
   - Proper `//` comments
   - Check import paths exist

4. **Check file permissions:**
   ```bash
   chmod +x login-server char-server map-server
   ```

### Client Can't Connect

1. **Verify client version:**
   - Check PACKETVER in `src/config/packets.hpp`
   - Must match client exe date

2. **Check IP configuration:**
   ```
   // char_athena.conf
   char_ip: <your_public_ip>

   // map_athena.conf
   map_ip: <your_public_ip>
   ```

3. **Test local connection first:**
   - Use `127.0.0.1` in clientinfo.xml

4. **Port forwarding:**
   - Forward TCP 6900, 6121, 5121

### Characters Won't Save

1. **Check autosave settings:**
   ```
   autosave_time: 300
   save_settings: 4095
   ```

2. **Verify MySQL connection:**
   - Check `map_server_*` settings in `inter_athena.conf`

3. **Check for SQL errors:**
   - Enable `console_msg_log: 2`
   - Check `map-msg_log.log`

### Script Debugging

1. **Enable script debug:**
   - Add `debugmes "reached here";` statements

2. **Check variable values:**
   ```
   mes "Value: " + @variable;
   ```

3. **Test in isolation:**
   - Create minimal test script
   - Use `@loadnpc` / `@unloadnpc`

### Performance Issues

1. **Check player count:**
   - Use `@who` to see online count

2. **Monitor mob spawns:**
   - Excessive spawns slow server
   - Check monster spawn scripts

3. **Database optimization:**
   ```sql
   OPTIMIZE TABLE char;
   OPTIMIZE TABLE inventory;
   ```

4. **Review custom scripts:**
   - Infinite loops cause hangs
   - Heavy queries slow server

---

## Health Check Commands
<!-- chunk: 06-health | keywords: status, check, verify -->

### Server Status Commands

| Command | Description |
|---------|-------------|
| `@uptime` | Server runtime |
| `@version` | Server version |
| `@users` | Online player count |
| `@who` | List online players |
| `@rates` | Current server rates |
| `@servertime` | Server time |

### Debug Information Commands

| Command | Description |
|---------|-------------|
| `@mapinfo 0` | Map flags and info |
| `@mapinfo 1` | Players on map |
| `@mapinfo 2` | NPCs on map |
| `@mapinfo 3` | Chat rooms |
| `@mobinfo <mob>` | Monster statistics |
| `@iteminfo <item>` | Item information |

---

## Quick Links

- Architecture: → See [[01_ARCHITECTURE]]
- API Functions: → See [[02_CORE_API]]
- Configuration: → See [[05_CONFIG]]
- Examples: → See [[07_EXAMPLES]]
