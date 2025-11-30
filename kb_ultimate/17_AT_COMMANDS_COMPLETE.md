# rAthena AT Commands - Complete Reference
## All 216+ @commands with Full Documentation

---

<!-- RAG_CHUNK: at_overview_001 -->
## AT Command Overview

### Command Format
```
@command [parameters]
#command [player] [parameters]  // Target other player
```

### Permission System
AT commands are controlled by:
- `conf/groups.conf` - Group permissions
- `db/atcommand_db.yml` - Command aliases
- `conf/atcommand_athena.conf` - Settings

### Binding in Scripts
```c
bindatcmd "<command>","<NPC>::<event>";
unbindatcmd "<command>";
useatcmd "@command parameters";
```

---

<!-- RAG_CHUNK: gm_items_001 -->
## Item Commands

### @item / @item2
**Syntax:** `@item <item id/name> {<amount>}`
**Syntax:** `@item2 <id> <amount> <identify> <refine> <attr> <c1> <c2> <c3> <c4>`

Create items. @item2 allows specifying properties.

**Examples:**
```
@item 501 100           // 100 Red Potions
@item Red_Potion 100    // Same using name
@item2 1201 1 1 10 0 4001 4001 0 0  // +10 Knife with 2 Drops cards
```

---

### @itembound / @itembound2
**Syntax:** `@itembound <id> <amount> <bound type>`

Create bound items (cannot trade/drop).

**Bound Types:**
- 1 = Account
- 2 = Guild
- 3 = Party
- 4 = Character

---

### @produce
**Syntax:** `@produce <equip id> <element> <star count>`

Create weapon with forging effects.

**Elements:** 0=None, 1=Ice, 2=Earth, 3=Fire, 4=Wind

---

### @refine
**Syntax:** `@refine <position> <+/- amount>`

Refine equipped item.

**Positions:**
- 0 = All equipment
- 1-2 = Accessories
- 4 = Shoes
- 8 = Garment
- 16 = Head (low)
- 32 = Head (mid)
- 64 = Head (top)
- 128 = Armor
- 256 = Left hand
- 512 = Right hand

**Example:** `@refine 512 10` - +10 to weapon

---

### @itemreset
Clear all inventory items.

### @clearstorage / @cleargstorage
Clear storage or guild storage.

### @storagelist / @guildstoragelist / @cartlist / @itemlist
Display item lists.

---

<!-- RAG_CHUNK: gm_player_001 -->
## Player Commands

### @heal
**Syntax:** `@heal {<hp> <sp>}`

Heal player. No arguments = full heal.

---

### @alive
Resurrect dead player.

---

### @job / @jobchange
**Syntax:** `@job <job id/name> {<upper>}`

Change job class.

**Upper:** 0=Normal, 1=High, 2=Baby

**Examples:**
```
@job 7           // Knight
@job Knight 1    // Lord Knight
@job 4001        // High Novice
```

---

### @lvup / @blvl
**Syntax:** `@lvup <amount>`

Increase base level.

---

### @joblvup / @jlvl
**Syntax:** `@joblvup <amount>`

Increase job level.

---

### @allskill
Learn all skills for current job.

---

### @skillpoint / @stpoint
**Syntax:** `@skillpoint <amount>`

Add skill/status points.

---

### @stat_all / @str / @agi / @vit / @int / @dex / @luk
**Syntax:** `@str <amount>`

Set or add to stats.

---

### @zeny
**Syntax:** `@zeny <amount>`

Add/remove zeny.

---

### @resetstate / @resetskill / @reset
Reset stats, skills, or both.

---

### @speed
**Syntax:** `@speed <value>`

Set movement speed. Range: 1-1000 (200 = normal)

---

### @spiritball
**Syntax:** `@spiritball <count>`

Set spirit spheres.

---

### @refresh
Refresh player state (clear visual bugs).

---

<!-- RAG_CHUNK: gm_warp_001 -->
## Warp Commands

### @warp / @rura / @go
**Syntax:** `@warp <map> {<x> <y>}`

Teleport to location.

### @go
**Syntax:** `@go <number/city>`

Quick teleport to cities.

| # | City | # | City |
|---|------|---|------|
| 0 | Prontera | 12 | Lighthalzen |
| 1 | Morroc | 13 | Einbroch |
| 2 | Geffen | 14 | Hugel |
| 3 | Payon | 15 | Rachel |
| 4 | Alberta | 16 | Veins |
| 5 | Izlude | 17 | Moscovia |
| 6 | Aldebaran | 18 | Midgard Camp |
| 7 | Lutie | 19 | Manuk |
| 8 | Comodo | 20 | Splendide |
| 9 | Yuno | 21 | Brasilis |
| 10 | Amatsu | 22 | El Dicastes |
| 11 | Kunlun | 23+ | More... |

---

### @jump
**Syntax:** `@jump {<x> <y>}`

Random teleport on current map, or to coordinates.

---

### @jumpto / @goto
**Syntax:** `@jumpto <player name>`

Teleport to player.

---

### @recall / @summon
**Syntax:** `@recall <player name>`

Summon player to your location.

---

### @load / @return
Return to save point.

---

### @save
**Syntax:** `@save {<map> <x> <y>}`

Set save point.

---

### @memo
**Syntax:** `@memo {<slot>}`

Set warp point for Warp Portal skill.

---

### @recallall / @guildrecall / @partyrecall
Mass recall commands.

---

<!-- RAG_CHUNK: gm_spawn_001 -->
## Monster Commands

### @monster / @spawn
**Syntax:** `@monster <mob id/name> {<amount> {"<display name>"}}`

Spawn monsters.

**Examples:**
```
@monster 1002 10         // 10 Porings
@monster Poring 5        // 5 Porings
@monster 1002 1 "Boss"   // Named Poring
```

---

### @monstersmall / @monsterbig
Spawn small/big version of monster.

---

### @summon
**Syntax:** `@summon <mob id/name> {<duration>}`

Summon monster that follows you.

---

### @killmonster / @killmonster2
**Syntax:** `@killmonster {<map>}`

Kill all monsters on map.
`@killmonster2` does not trigger drops/exp.

---

### @mobinfo / @mi
**Syntax:** `@mobinfo <mob id/name>`

Display monster information.

---

### @whereis / @mobsearch
**Syntax:** `@whereis <mob id/name>`

Find monster spawn locations.

---

### @showmobs
**Syntax:** `@showmobs <mob id/name>`

Highlight monsters on map.

---

<!-- RAG_CHUNK: gm_control_001 -->
## Player Control Commands

### @kick
**Syntax:** `@kick <player name>`

Kick player from server.

---

### @kickall
Kick all non-GM players.

---

### @ban / @unban
**Syntax:** `@ban <time> <player name>`

Ban player from server.

**Time Format:** `<number><unit>` (s=second, n=minute, h=hour, d=day, m=month, y=year)

**Examples:**
```
@ban 30m PlayerName    // 30 minute ban
@ban 7d PlayerName     // 7 day ban
@unban PlayerName      // Remove ban
```

---

### @jail / @jailfor / @unjail
**Syntax:** `@jail <player name>`
**Syntax:** `@jailfor <time> <player name>`

Imprison players.

---

### @mute / @mutearea
**Syntax:** `@mute <time> <player name>`

Mute player chat.

---

### @block / @unblock
Block/unblock player account.

---

### @nuke
**Syntax:** `@nuke <player name>`

Kill player with special effect.

---

### @doom / @doommap
Kill all non-GM players (current map or all maps).

---

### @raise / @raisemap
Resurrect all players.

---

<!-- RAG_CHUNK: gm_visual_001 -->
## Visual & Appearance

### @hide
Toggle GM invisibility.

---

### @disguise / @undisguise
**Syntax:** `@disguise <mob id>`

Transform into monster.

---

### @changelook
**Syntax:** `@changelook <type> <value>`

Change appearance.

| Type | Description |
|------|-------------|
| 1 | Hair style |
| 2 | Weapon |
| 3 | Head (bottom) |
| 4 | Head (top) |
| 5 | Head (mid) |
| 6 | Hair color |
| 7 | Cloth color |
| 8 | Shield |

---

### @dye / @ccolor
**Syntax:** `@dye <color>`

Change cloth color.

---

### @hairstyle / @hstyle
**Syntax:** `@hairstyle <style>`

Change hair style.

---

### @haircolor / @hcolor
**Syntax:** `@haircolor <color>`

Change hair color.

---

### @model
**Syntax:** `@model <hair style> <hair color> <cloth color>`

Change all appearance at once.

---

### @size
**Syntax:** `@size <0-2>`

Change character size. 0=small, 1=normal, 2=large

---

### @effect
**Syntax:** `@effect <effect id>`

Display visual effect.

---

<!-- RAG_CHUNK: gm_npc_001 -->
## NPC Commands

### @npcmove
**Syntax:** `@npcmove <x> <y> <npc name>`

Move NPC to coordinates.

---

### @hidenpc / @shownpc
**Syntax:** `@hidenpc <npc name>`

Toggle NPC visibility.

---

### @loadnpc / @unloadnpc
**Syntax:** `@loadnpc <file path>`
**Syntax:** `@unloadnpc <npc name>`

Load/unload NPC scripts.

---

### @tonpc
**Syntax:** `@tonpc <npc name>`

Teleport to NPC.

---

### @npctalk
**Syntax:** `@npctalk <npc name> <message>`

Make NPC say message.

---

<!-- RAG_CHUNK: gm_admin_001 -->
## Administration Commands

### @broadcast / @bc / @b
**Syntax:** `@broadcast <message>`

Send server-wide message.

---

### @localbroadcast / @lb
**Syntax:** `@localbroadcast <message>`

Send map-wide message.

---

### @kami / @kamib / @kamic / @lkami
GM announcements with colors.

---

### @reloadscript
Reload all NPC scripts.

---

### @reloaditemdb / @reloadmobdb / @reloadskilldb
Reload specific databases.

---

### @reloadbattleconf / @reloadatcommand
Reload configuration files.

---

### @mapflag
**Syntax:** `@mapflag <flag> {<value>}`

Set map flag.

---

### @mapexit
Shutdown map server.

---

### @gvgon / @gvgoff / @pvpon / @pvpoff
Toggle GvG/PvP mode on current map.

---

### @agitstart / @agitend
Start/end War of Emperium.

---

<!-- RAG_CHUNK: player_commands_001 -->
## Player Usable Commands

### @commands / @help
List available commands.

---

### @rates
Display server rates.

---

### @time / @servertime
Display server time.

---

### @uptime
Show server uptime.

---

### @showexp / @showzeny
Toggle EXP/Zeny gain display.

---

### @autoloot
**Syntax:** `@autoloot {<rate>}`

Auto-loot items. Rate in %.

---

### @autolootitem
**Syntax:** `@autolootitem <+/- item id/name>`

Add/remove specific items from autoloot.

---

### @autoloottype
**Syntax:** `@autoloottype <+/- type>`

Autoloot by item type.

**Types:** healing, usable, etc, weapon, armor, card, petegg, petarmor, ammo

---

### @autotrade / @at
Enable offline vending.

---

### @request
**Syntax:** `@request <message>`

Send message to online GMs.

---

### @noask
Block trade/party/guild requests.

---

### @noks / @ks
Enable/disable kill steal protection.

---

### @hominfo / @homstats
Display homunculus information.

---

### @pettalk / @homtalk / @mertalk
Make pet/homunculus/mercenary talk.

---

### @storage / @guildstorage
Open storage windows.

---

### @duel / @invite / @accept / @reject / @leave
Duel system commands.

---

<!-- RAG_CHUNK: utility_commands_001 -->
## Utility Commands

### @who / @who2 / @who3
**Syntax:** `@who {<map>}`

List online players.

---

### @users
Show player count by map.

---

### @whogm
List online GMs.

---

### @where
**Syntax:** `@where <player name>`

Find player location.

---

### @accinfo
**Syntax:** `@accinfo <account id / player name>`

Display account information.

---

### @charinfo / @charstats
Display character information.

---

### @showdelay
Toggle skill delay display.

---

### @font
**Syntax:** `@font <0-9>`

Change chat font.

---

### @langtype
**Syntax:** `@langtype <language>`

Change client language.

---

#rathena #atcommand #gm #admin #warp #item #monster #player #commands
