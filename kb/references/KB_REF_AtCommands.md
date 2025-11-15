---
kb_id: KB_REF_011
kb_type: reference
kb_category: admin
kb_subcategory: atcommands
kb_keywords: [atcommands, gm commands, admin commands, @command, #command, server admin, testing, debugging, item spawning, player management, warp, level, stats, reload]
kb_related: [KB_REF_001, KB_REF_005, KB_REF_003]
kb_difficulty: intermediate
kb_version: rAthena_2025
kb_last_updated: 2025-10-25
kb_use_case: [server_administration, testing, debugging, player_support, event_management]
---

# rAthena At-Commands Reference

Complete reference for in-game admin/GM commands (atcommands) used for server management, testing, and player support.

## Overview

At-commands are special commands available to GMs and administrators for managing the server in-game. They are prefixed with `@` for self-targeting or `#` for targeting other players.

**Configuration:** `/conf/atcommand_athena.conf`
**Default Symbol:** `@` (atcommands) and `#` (charcommands)
**Permission Required:** Set in `/conf/groups.conf` per command

**Usage Pattern:**
```
@commandname <parameters>     // Affects yourself
#commandname <player> <params> // Affects another player
```

---

## TABLE OF CONTENTS

1. [System Commands](#1-system-commands) - Server info, rates, time
2. [Database Commands](#2-database-commands) - Search items, monsters, skills
3. [Player Information](#3-player-information) - Who's online, stats
4. [Item Commands](#4-item-commands) - Give/remove items, storage
5. [Player Modification](#5-player-modification) - Level, stats, skills
6. [Movement Commands](#6-movement-commands) - Warp, teleport, recall
7. [Monster Commands](#7-monster-commands) - Spawn mobs, kill
8. [Map Control](#8-map-control) - PvP, GvG, weather, mapflags
9. [Administrative](#9-administrative) - Kick, ban, reload
10. [Testing/Debug](#10-testingdebug) - Effects, packets, display

---

## 1. SYSTEM COMMANDS

### @version
**Description:** Displays SVN version of the server
**Syntax:** `@version`
**Permission:** Basic user
**Example:** `@version` → "rAthena vXXXX Revision XXXX"

---

### @rates
**Description:** Displays current server rates
**Syntax:** `@rates`
**Permission:** Basic user
**Output:**
```
Experience rates: Base 1.00x / Job 1.00x
Normal Drop Rates: Common 1.00x / Healing 1.00x / Usable 1.00x Equipment 1.00x / Card 1.00x
Boss Drop Rates: Common 1.00x / Healing 1.00x / Usable 1.00x Equipment 1.00x / Card 1.00x
Other Drop Rates: MvP 1.00x / Card-Based 1.00x / Treasure 1.00x
```

---

### @time
**Description:** Shows local server time and day/night status
**Syntax:** `@time`
**Permission:** Basic user

---

### @uptime
**Description:** Shows server uptime since last restart
**Syntax:** `@uptime`
**Example Output:** "Server Uptime: 3 days, 8 hours, 6 minutes, 4 seconds."

---

### @refresh
**Description:** Synchronizes player position (fixes desync issues)
**Syntax:** `@refresh`
**Permission:** Basic user
**Use Case:** Player stuck, invisible, or position desynced

---

### @refreshall
**Description:** Refreshes all online players
**Syntax:** `@refreshall`
**Permission:** Admin
**Use Case:** Server-wide desync fix

---

### @showexp / @showzeny / @showdelay
**Description:** Toggles display messages for exp gain, zeny gain, skill delays
**Syntax:** `@showexp` | `@showzeny` | `@showdelay`
**Permission:** Basic user

---

## 2. DATABASE COMMANDS

### @iteminfo <item ID/name>
**Description:** Displays detailed item information
**Syntax:** `@iteminfo <item ID or name>`
**Example:** `@iteminfo Red Potion` → Shows ID, type, buy/sell price, weight, etc.

---

### @mobinfo <monster ID/name>
**Description:** Displays detailed monster information
**Syntax:** `@mobinfo <monster ID or name>`
**Example:** `@mobinfo Poring` → Shows ID, HP, level, stats, drops, etc.

---

### @idsearch <item name>
**Description:** Searches for items by name (partial match)
**Syntax:** `@idsearch <partial name>`
**Example:** `@idsearch potion` → Lists all items with "potion" in name

---

### @whereis <monster name/ID>
**Description:** Shows maps where monster naturally spawns
**Syntax:** `@whereis <monster name or ID>`
**Example:** `@whereis Poring` → Lists maps with Poring spawns

---

### @showmobs <monster name/ID>
**Description:** Displays monster locations on mini-map (white crosses)
**Syntax:** `@showmobs <monster name or ID>`
**Use Case:** Finding rare spawns or MVPs

---

### @skillid <skill name>
**Description:** Looks up skill ID by name (partial match)
**Syntax:** `@skillid <partial skill name>`
**Example:** `@skillid heal` → Shows all healing skills with IDs

---

### @skilltree <skill ID> <target>
**Description:** Lists requirements to learn a skill
**Syntax:** `@skilltree <skill ID> <player name>`
**Example:** `@skilltree 28 PlayerName` → Shows Heal skill requirements

---

## 3. PLAYER INFORMATION

### @commands
**Description:** Lists all @ commands available to you
**Syntax:** `@commands`
**Permission:** Based on your group level

---

### @exp
**Description:** Shows current level and exp progress
**Syntax:** `@exp`
**Output:** "Base Level: 99 (75.323%) | Job Level: 70 (50.000%)"

---

### @stats
**Description:** Displays your character stats
**Syntax:** `@stats`
**Shows:** STR, AGI, VIT, INT, DEX, LUK, HP, SP

---

### @who {<filter>}
**Description:** Lists online players
**Syntax:** `@who [filter]` | `@who2` | `@who3`
**Variants:**
- `@who` - Shows names and positions
- `@who2` - Shows names and job classes
- `@who3` - Shows names, parties, and guilds
**Example:** `@who GM` → Lists all players with "GM" in name

---

### @whomap {<map>}
**Description:** Lists players on a specific map
**Syntax:** `@whomap [map name]`
**Example:** `@whomap prontera`

---

### @whogm {<filter>}
**Description:** Lists GMs online
**Syntax:** `@whogm [filter]`
**Note:** Shows full info for lower-level GMs, name only for higher-level

---

### @users
**Description:** Shows player distribution per map
**Syntax:** `@users`
**Output:** Percentage of players on each map

---

### @itemlist / @storagelist / @cartlist
**Description:** Lists items in inventory/storage/cart
**Syntax:** `@itemlist` | `@storagelist <player>` | `@cartlist <player>`
**Permission:** Admin (for viewing other players)

---

## 4. ITEM COMMANDS

### @item <item ID/name> {<amount>}
**Description:** Creates item(s) in your inventory
**Syntax:** `@item <item ID or name> [amount]`
**Example:**
```
@item 501              // 1x Red Potion
@item Red Potion 100   // 100x Red Potion
@item 1201             // 1x Knife
```
**Restriction:** Cannot be used from console

---

### @item2 <ID> <amount> <identify> <refine> <attribute> <card1> <card2> <card3> <card4>
**Description:** Creates item with specific properties
**Syntax:** `@item2 <item ID> <qty> <identified> <refine> <broken> <card1> <card2> <card3> <card4>`
**Example:**
```
@item2 1201 1 1 10 0 4001 0 0 0
// Creates +10 Knife with Poring Card
```
**Parameters:**
- `identify`: 0 = unidentified, 1 = identified
- `refine`: 0-20 (refine level, +0 to +20)
- `attribute`: 0 = normal, 1 = broken
- `card1-4`: Card item IDs (0 = no card)

---

### @delitem <item ID/name> {<amount>}
**Description:** Removes item(s) from inventory
**Syntax:** `@delitem <item ID or name> [amount]`
**Example:** `@delitem 501 50` → Removes 50 Red Potions

---

### @itemreset
**Description:** Deletes ALL items in inventory (not equipped)
**Syntax:** `@itemreset`
**Warning:** Irreversible! Items are permanently deleted.

---

### @clearstorage / @cleargstorage
**Description:** Deletes all items in storage or guild storage
**Syntax:** `@clearstorage` | `@cleargstorage`
**Warning:** Irreversible!

---

### @clearcart
**Description:** Deletes all items in cart
**Syntax:** `@clearcart`

---

### @storage / @gstorage
**Description:** Opens Kafra storage or guild storage
**Syntax:** `@storage` | `@gstorage`
**Use Case:** Access storage anywhere without Kafra NPC

---

### @storeall
**Description:** Moves all inventory/equipped items to storage
**Syntax:** `@storeall`

---

## 5. PLAYER MODIFICATION

### @blvl <+/- amount>
**Description:** Changes base level
**Syntax:** `@blvl <amount>` | `#blvl <player> <amount>`
**Example:**
```
@blvl +10     // Add 10 base levels
@blvl -5      // Remove 5 base levels
@blvl 99      // Set to level 99
```
**Restriction:** Cannot be used from console

---

### @jlvl <+/- amount>
**Description:** Changes job level
**Syntax:** `@jlvl <amount>` | `#jlvl <player> <amount>`
**Example:**
```
@jlvl +5      // Add 5 job levels
@jlvl 70      // Set to job level 70
```

---

### @str / @agi / @vit / @int / @dex / @luk
**Description:** Changes individual stat
**Syntax:** `@str <amount>` (also @agi, @vit, @int, @dex, @luk)
**Example:**
```
@str +10      // Add 10 STR
@dex 99       // Set DEX to 99
```

---

### @allstats {<amount>}
**Description:** Changes all stats
**Syntax:** `@allstats [amount]`
**Example:**
```
@allstats 99  // Set all stats to 99
@allstats     // Set all stats to max (default 99)
```

---

### @statall {<value>}
**Description:** Alternative to @allstats
**Syntax:** `@statall [value]`

---

### @job <job ID/name>
**Description:** Changes job class
**Syntax:** `@job <job ID or name>`
**Example:**
```
@job Knight
@job 7        // Job ID 7 = Knight
@job Assassin Cross
```
**Note:** See `/doc/ea_job_system.txt` for job IDs

---

### @jobchange <job ID>
**Description:** Alternative to @job
**Syntax:** `@jobchange <job ID>`

---

### @zeny <+/- amount>
**Description:** Changes zeny
**Syntax:** `@zeny <amount>` | `#zeny <player> <amount>`
**Example:**
```
@zeny +1000000    // Add 1 million zeny
@zeny -500        // Remove 500 zeny
```

---

### @refine <+/- amount> {<position>}
**Description:** Refines equipped item
**Syntax:** `@refine <amount> [equipment position]`
**Example:**
```
@refine +5 1  // Refine weapon to +5
@refine +10   // Refine all equipped to +10
```

---

### @produce <item ID> {<element> {<star crumb>}}
**Description:** Creates forged/crafted item
**Syntax:** `@produce <item ID> [element] [fame]`

---

### @heal {<HP> {<SP>}}
**Description:** Restores HP/SP
**Syntax:** `@heal [HP] [SP]`
**Example:**
```
@heal         // Full heal HP and SP
@heal 1000    // Heal 1000 HP
@heal 0 500   // Heal 500 SP
```

---

### @questskill <skill ID>
**Description:** Adds permanent quest skill
**Syntax:** `@questskill <skill ID>`
**Example:** `@questskill 142` → Learn Vending skill

---

### @lostskill <skill ID>
**Description:** Removes permanent quest skill
**Syntax:** `@lostskill <skill ID>`

---

### @useskill <skill ID> <level> <target>
**Description:** Casts skill on target
**Syntax:** `@useskill <skill ID> <level> <target name>`
**Example:** `@useskill 28 10 PlayerName` → Cast Lv10 Heal on player

---

### @skillall
**Description:** Learns all available skills for your class
**Syntax:** `@skillall`

---

### @allskill {<value>}
**Description:** Sets all skills to specified level
**Syntax:** `@allskill [level]`
**Example:** `@allskill 10` → All skills to level 10

---

### @skilltree <skill ID> <player>
**Description:** Shows skill requirements
**Syntax:** `@skilltree <skill ID> <player name>`

---

## 6. MOVEMENT COMMANDS

### @go {<location ID/name>}
**Description:** Warps to predefined major cities
**Syntax:** `@go [location]`
**Example:**
```
@go          // Show all available locations
@go prontera // Warp to Prontera
@go 0        // Warp to Prontera
```
**Common Locations:**
- 0: Prontera
- 1: Morocc
- 2: Geffen
- 3: Payon
- 4: Alberta
- 5: Izlude
- 6: Al De Baran
- 7: Lutie (Lutie/Xmas)
- 8: Comodo

**Restriction:** Cannot be used from console

---

### @warp <map> {<x> <y>}
**Aliases:** `/mm`, `/mapmove`
**Description:** Warps to specified map and coordinates
**Syntax:** `@warp <map name> [x] [y]`
**Example:**
```
@warp prontera          // Random position in Prontera
@warp prontera 150 150  // Prontera coordinates 150,150
```
**Restriction:** Cannot be used from console

---

### @jump {<x> <y>}
**Description:** Warps to coordinates on current map
**Syntax:** `@jump [x] [y]`
**Example:**
```
@jump         // Random position on current map
@jump 100 200 // Jump to 100,200 on current map
```

---

### @jumpto <player>
**Aliases:** `/shift`
**Description:** Warps to target player's location
**Syntax:** `@jumpto <player name>`
**Example:** `@jumpto PlayerName`

---

### @follow <player>
**Description:** Warps to player and follows their movement
**Syntax:** `@follow <player name>`
**Example:** `@follow PlayerName` → Follow until toggled off

---

### @recall <player>
**Aliases:** `/summon`
**Description:** Warps player to your location
**Syntax:** `@recall <player name>` | `#recall <player>`
**Example:** `@recall PlayerName`

---

### @recallall
**Description:** Recalls ALL online players to your location
**Syntax:** `@recallall`
**Warning:** Affects entire server!

---

### @tonpc <NPC name>
**Description:** Warps to NPC location
**Syntax:** `@tonpc <NPC name>`
**Example:** `@tonpc Kafra Employee`

---

### @save
**Description:** Sets current location as save point
**Syntax:** `@save`

---

### @load
**Description:** Warps to your save point
**Syntax:** `@load`

---

### @memo {<slot 0-2>}
**Description:** Saves warp portal location
**Syntax:** `@memo [slot number]`
**Example:**
```
@memo     // Show all saved locations
@memo 0   // Save to slot 0
```

---

## 7. MONSTER COMMANDS

### @monster <monster name> {<amount>}
**Aliases:** `@spawn`
**Description:** Spawns monster at your location
**Syntax:** `@monster <name or ID> [amount]`
**Example:**
```
@monster Poring      // Spawn 1 Poring
@monster 1002 10     // Spawn 10 Porings (ID 1002)
@monster Eddga       // Spawn MVP Eddga
```

---

### @monstersmall / @monsterbig
**Description:** Spawns small or large version of monster
**Syntax:** `@monstersmall <name> [amount]` | `@monsterbig <name> [amount]`

---

### @killmonster {<map>}
**Description:** Kills all monsters on map
**Syntax:** `@killmonster [map name]`
**Example:**
```
@killmonster         // Kill all monsters on current map
@killmonster prontera // Kill all in Prontera
```

---

### @killmonster2
**Description:** Kills all monsters including those spawned by scripts
**Syntax:** `@killmonster2`

---

### @summon <monster ID/name>
**Description:** Spawns monster that assists you
**Syntax:** `@summon <name or ID>`

---

## 8. MAP CONTROL

### @pvpon / @pvpoff
**Description:** Enables/disables PvP on current map
**Syntax:** `@pvpon` | `@pvpoff`

---

### @gvgon / @gvgoff
**Description:** Enables/disables GvG on current map
**Syntax:** `@gvgon` | `@gvgoff`

---

### @agitstart / @agitend
**Description:** Starts/ends War of Emperium [FE]
**Syntax:** `@agitstart` | `@agitend`
**Note:** Invokes OnAgitStart/OnAgitEnd script labels

---

### @agitstart2 / @agitend2
**Description:** Starts/ends War of Emperium [SE]
**Syntax:** `@agitstart2` | `@agitend2`

---

### @agitstart3 / @agitend3
**Description:** Starts/ends War of Emperium [TE]
**Syntax:** `@agitstart3` | `@agitend3`

---

### @skillon / @skilloff
**Description:** Enables/disables skill usage on map
**Syntax:** `@skillon` | `@skilloff`

---

### @mapflag <flag> <value>
**Description:** Sets mapflag for current map
**Syntax:** `@mapflag <flag name> <0 or 1>`
**Example:**
```
@mapflag pvp 1      // Enable PvP mapflag
@mapflag noteleport 1  // Disable teleport
```
**See:** KB_REF_MapFlags.md for all mapflag options

---

### @day / @night
**Description:** Changes server to day/night mode
**Syntax:** `@day` | `@night`

---

### @snow / @clouds / @fog / @fireworks / @sakura / @leaves
**Description:** Toggles weather effects on current map
**Syntax:** `@snow` | `@clouds` | `@fog` | etc.

---

### @clearweather
**Description:** Stops all weather effects
**Syntax:** `@clearweather`
**Note:** May require @refresh for client-side update

---

### @addwarp <map> <x> <y> <name>
**Description:** Creates temporary warp portal (until restart)
**Syntax:** `@addwarp <map> <x> <y> <warp name>`
**Example:** `@addwarp prontera 150 150 test_warp`

---

### @mapinfo {<type> {<map>}}
**Description:** Displays map information
**Syntax:** `@mapinfo [type] [map]`
**Types:**
- 0: General info and mapflags (default)
- 1: Players on map
- 2: NPCs on map
- 3: Chatrooms on map

---

## 9. ADMINISTRATIVE

### @reloadscript
**Description:** Reloads all NPC scripts
**Syntax:** `@reloadscript`
**Warning:** May cause issues with running scripts/instances

---

### @reloaditemdb / @reloadmobdb / @reloadskilldb
**Description:** Reloads database from YAML files
**Syntax:** `@reloaditemdb` | `@reloadmobdb` | `@reloadskilldb`

---

### @reloadatcommand
**Description:** Reloads atcommand configuration
**Syntax:** `@reloadatcommand`

---

### @reloadbattleconf
**Description:** Reloads battle configuration
**Syntax:** `@reloadbattleconf`

---

### @kick <player>
**Description:** Kicks player from server
**Syntax:** `@kick <player name>` | `#kick <player>`
**Example:** `@kick PlayerName`

---

### @kickall
**Description:** Kicks all players except GMs
**Syntax:** `@kickall`

---

### @ban <time> <player>
**Description:** Temporarily bans player
**Syntax:** `@ban <time> <player name>`
**Time Format:** `<value><unit>` (s=seconds, mn=minutes, h=hours, d=days, m=months, y=years)
**Example:**
```
@ban 1d PlayerName   // Ban for 1 day
@ban 12h PlayerName  // Ban for 12 hours
```

---

### @unban <player>
**Description:** Unbans player
**Syntax:** `@unban <player name>`

---

### @block <player>
**Description:** Permanently blocks account
**Syntax:** `@block <player name>`

---

### @unblock <player>
**Description:** Unblocks account
**Syntax:** `@unblock <player name>`

---

### @jail <player>
**Description:** Sends player to jail
**Syntax:** `@jail <player name>`

---

### @unjail <player>
**Description:** Releases player from jail
**Syntax:** `@unjail <player name>`

---

### @mute <time> <player>
**Description:** Prevents player from chatting
**Syntax:** `@mute <minutes> <player name>`
**Example:** `@mute 10 PlayerName` → Mute for 10 minutes

---

### @unmute <player>
**Description:** Unmutes player
**Syntax:** `@unmute <player name>`

---

### @announce <message>
**Description:** Server-wide announcement
**Syntax:** `@announce <message>`
**Example:** `@announce Server maintenance in 10 minutes!`

---

### @kami <message>
**Aliases:** `@kamib`
**Description:** God message (yellow text, server-wide)
**Syntax:** `@kami <message>`

---

### @localannounce <message>
**Description:** Announcement only on current map
**Syntax:** `@localannounce <message>`

---

### @broadcast <message>
**Description:** Broadcast message
**Syntax:** `@broadcast <message>`

---

## 10. TESTING/DEBUG

### @effect <effect ID>
**Description:** Displays visual effect on character
**Syntax:** `@effect <effect ID>`
**Example:** `@effect 7` → Displays effect #7
**See:** KB_REF_VisualEffects.md for effect IDs (EF_*)

---

### @misceffect <effect ID>
**Description:** Displays misc effect on character
**Syntax:** `@misceffect <ID>`
**Effects:**
- 0: Base level up
- 1: Job level up
- 2: Refine failure
- 3: Refine success
- 4: Game over
- 5: Pharmacy success
- 6: Pharmacy failure

---

### @displayskill <skill ID> {<level>}
**Description:** Displays skill animation without casting
**Syntax:** `@displayskill <skill ID> [level]`

---

### @option {<param1> {<param2> {<param3>}}}
**Description:** Adds visual status effects
**Syntax:** `@option [opt1] [opt2] [opt3]`
**Example:** `@option` → Shows list of available options

---

### @displaystatus <status> <flag> <tick> {<val1-3>}
**Description:** Displays status change without applying it
**Syntax:** `@displaystatus <type> <flag> <duration> [val1] [val2] [val3]`

---

### @size {<0-2>}
**Description:** Changes character size
**Syntax:** `@size [size]`
**Values:**
- 0: Normal
- 1: Small
- 2: Large

---

### @speed <0-1000>
**Description:** Changes movement speed
**Syntax:** `@speed <value>`
**Values:** 0 (instant) to 1000 (slowest)
**Default:** 150

---

### @hide
**Description:** Toggles invisibility (GM hide)
**Syntax:** `@hide`
**Note:** Hidden GMs cannot be seen or targeted

---

### @invisible
**Description:** Alternative to @hide
**Syntax:** `@invisible`

---

### @killable
**Description:** Allows other players to attack you outside PvP
**Syntax:** `@killable`

---

### @killer
**Description:** Allows you to attack players outside PvP
**Syntax:** `@killer`

---

### @send <packet hex> {<value>}
**Description:** Sends test packet to client (debug)
**Syntax:** `@send <hex> [value]`
**Value Format:** `<type=B,W,L><number>` or `S<length>"string"`

---

## COMMON WORKFLOWS

### Testing New Items
```
@item 501 100              // Get test items
@item2 1201 1 1 10 0 4001 0 0 0  // Get +10 weapon with card
@refine +10 1              // Refine weapon to +10
```

### Testing New NPCs
```
@reloadscript              // Reload after NPC changes
@tonpc NPC_Name            // Warp to NPC location
@jump 150 150              // Position test
```

### Event Management
```
@announce Event starting in 5 minutes!
@recallall                 // Gather all players
@warp event_map 150 150    // Move to event location
@monster MvP_Boss 1        // Spawn event boss
```

### Player Support
```
@jumpto PlayerName         // Go to player
@heal                      // Heal player
@item 501 100              // Give recovery items
@recall PlayerName         // Bring player to safe location
```

### Server Maintenance
```
@announce Server restarting in 10 minutes
@kickall                   // Kick all players
@reloadscript              // Reload scripts
@reloaditemdb              // Reload databases
```

---

## PERMISSION CONFIGURATION

Edit `/conf/groups.conf` to control command access:

```yaml
groups:
  - id: 99  # GM group
    name: "Game Master"
    level: 99
    commands:
      item: true
      warp: true
      recall: true
      # ... etc
    permissions:
      can_trade: true
      all_commands: true
```

---

## SECURITY NOTES

1. **Never give regular players admin commands** - Use group-based permissions
2. **@reloadscript can break running instances** - Use during low-traffic times
3. **@recallall affects entire server** - Use with caution
4. **@item/@zeny can crash economy** - Audit GM logs regularly
5. **Console restrictions** - Some commands blocked from console for safety

---

## CROSS-REFERENCES

- **Permissions:** See KB_REF_Permissions.md
- **Mapflags:** See KB_REF_MapFlags.md
- **Visual Effects:** See KB_REF_VisualEffects.md
- **Job IDs:** See `/doc/ea_job_system.txt`
- **Full Command List:** See `/doc/atcommands.txt` (1931 lines)

---

## TIPS

1. Use `@commands` to see what you have access to
2. Use `@help <command>` for command-specific help
3. Test with `@monster` before adding permanent spawns
4. Use `@refresh` when things look broken
5. Always use `@reloadscript` after NPC edits during testing
6. GM logs are stored - all command usage is tracked

---

**Total Commands Documented:** 100+ essential commands
**Coverage:** ~80% of daily admin/testing needs
**For Complete List:** See `/doc/atcommands.txt`
