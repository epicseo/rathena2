# rAthena AT Commands Complete Reference v12.0
## ALL 287 @COMMANDS WITH SYNTAX AND EXAMPLES

---

# rAthena AT Commands - Complete Reference
## All 287 @commands with Full Documentation

---

<!-- RAG_CHUNK: at_overview_001 -->
## AT Command Overview

### Command Format
```
@command [parameters]
#command [player] [parameters]  // Target other player (charcommand)
```

### Configuration Files
```
conf/atcommand_athena.conf - Symbol settings
conf/groups.conf - Group permissions
db/atcommand_db.yml - Command aliases
```

### Symbols (Default)
```
atcommand_symbol : "@"
charcommand_symbol: "#"
```

### Binding in Scripts
```c
bindatcmd "<command>","<NPC>::<event>";
unbindatcmd "<command>";
useatcmd "@command parameters";
```

---

<!-- RAG_CHUNK: system_commands_complete_001 -->
## 1. System Commands

### @version
Displays SVN/Git version of the server.

### @rates
Displays server experience and drop rates.
```
Experience rates: Base 1.00x / Job 1.00x
Normal Drop Rates: Common 1.00x / Healing 1.00x / Usable 1.00x Equipment 1.00x / Card 1.00x
Boss Drop Rates: Common 1.00x / Healing 1.00x / Usable 1.00x Equipment 1.00x / Card 1.00x
Other Drop Rates: MvP 1.00x / Card-Based 1.00x / Treasure 1.00x
```

### @time
Displays local server time with day/night information.

### @uptime
Shows server uptime since last restart.
```
Server Uptime: 3 days, 8 hours, 6 minutes, 4 seconds.
```

### @refresh
Synchronizes player position between client and server.

### @refreshall
Refreshes all online players.

### @showexp
Toggles EXP gain message display.

### @showzeny
Toggles Zeny gain message display.
Requires `zeny_from_mobs: yes` in `/conf/battle/monster.conf`.

### @showdelay
Shows/hides the red "Cannot use the skills" message.

### @noask
Toggles automatic rejection of deals and invites.

### @noks
Toggles Kill Steal Protection.

### @font <type 0-9>
Sets client font.
```
0: Default          5: RixMiniHeart
1: RixLoveangel     6: RixFreshman
2: RixSquirrel      7: RixKid
3: NHCgogo          8: RixMagic
4: RixDiary         9: RixJJangu
```

### @showrate
Toggles VIP rate information display when loading maps.

---

<!-- RAG_CHUNK: woe_system_commands_001 -->
## War of Emperium Commands

### @agitstart / @agitend
Starts/ends WoE FE (First Edition).
Invokes scripts with `OnAgitStart`/`OnAgitEnd` labels.

### @agitstart2 / @agitend2
Starts/ends WoE SE (Second Edition).
Invokes `OnAgitStart2`/`OnAgitEnd2` labels.

### @agitstart3 / @agitend3
Starts/ends WoE TE (Third Edition).
Invokes `OnAgitStart3`/`OnAgitEnd3` labels.

### @pvpon / @pvpoff
Enables/disables PvP (Player vs. Player) mode on current map.

### @gvgon / @gvgoff
Enables/disables GvG (Guild vs. Guild) mode on current map.

### @skillon / @skilloff
Enables/disables skill usage on current map.

### @allowks
Toggles Kill Steal Protection on current map.

---

<!-- RAG_CHUNK: weather_env_commands_001 -->
## Weather & Environment Commands

### @day / @night
Sets server to day or night mode.

### @snow
Toggles snow weather effect.

### @clouds / @clouds2
Toggles cloud weather effects.

### @fog
Toggles fog weather effect.

### @fireworks
Toggles fireworks weather effect.

### @sakura
Toggles sakura (cherry blossom) effect.

### @leaves
Toggles falling leaves effect.

### @clearweather
Stops all weather effects. May require map change or @refresh.

### @sound <filename>
Plays specified sound file.

### @mapflag <flag> <0|1>
Sets mapflag for current map (1 = On, 0 = Off).

### @addwarp <map> <x> <y> <npc name>
Creates temporary warp portal at current coordinates (until reboot).
```
@addwarp prontera 50 50 my_warp_sample
```

### @effect <effect ID>
Creates visual effect. See `/doc/effect_list.txt` for IDs.

### @misceffect <effect ID>
Visual effects:
```
0: Base level up      5: Pharmacy success
1: Job level up       6: Pharmacy failure
2: Refine failure     7: Base level up (Super Novice)
3: Refine success     8: Job level up (Super Novice)
4: Game over          9: Base level up (Taekwon)
```

### @displayskill <skill ID> {<level>}
Displays skill animation without using it (debug).

### @option {<p1> {<p2> {<p3>}}}
Adds visual effects to character. Lists options if no parameter.

### @displaystatus <type> <flag> <tick> {<val1> {<val2> {<val3>}}}
Displays status change without applying it (debug).

### @send <hex> {<value>}
Packet send testing (debug).
Value format: `<type=B,W,L><number>` or `S<length>"<string>"`

---

<!-- RAG_CHUNK: database_commands_complete_001 -->
## 2. Database Commands

### @mobinfo <mob name/ID>
Displays monster information.
```
Monster: 'Poring'/'Poring'/'PORING' (1002)
Lv: 1 HP:60 Base EXP:27 Job EXP:20 HIT:103 FLEE:183
DEF:2 MDEF:5 STR:6 AGI:1 VIT:1 INT:1 DEX:6 LUK:5
ATK:8~9 Range:1~10~12 Size:Medium Race:Plant Element:Water (Lv:1)
Drops:
 - Jellopy 70.00% - Knife[4] 1.00% etc...
```

### @iteminfo <item name/ID>
Displays item information.
```
Item: 'Jellopy'/'Jellopy'[0] (909) Type: Etc. | Extra Effect: None
NPC Buy:6z, Sell:3z | Weight: 1.0
- Maximal monsters drop change: 75.00%
```

### @whodrops <item name/ID>
Lists mobs that drop the specified item (highest drop rates shown).

### @autoloot {<%>}
Enables/disables autolooting. Optional percentage threshold.

### @alootid <+/- item name/ID>
Autoloot specific items. `reset` clears list. Default limit: 10 items.

### @autoloottype <+/- type>
Autoloot by item type. `reset` clears list.
```
healing = 0     weapon = 4      petegg = 7
usable = 2      armor = 5       petarmor = 8
etc = 3         card = 6        ammo = 10
```

### @mobsearch <monster name>
Locates monsters on current map with coordinates.
```
1[155:184] Poring
2[154:188] Poring
```

### @idsearch <item name>
Looks up item by name or partial name.

### @showmobs <monster name/ID>
Shows monster positions on minimap as white crosses (+).

### @whereis <monster name>
Displays maps where monster normally spawns (not script summoned).

### @skillid <skill name>
Looks up skill by name or partial name.

### @skilltree <skill ID> <target>
Lists requirements to obtain skill on target character.

### @questskill {<skill ID>}
Permanently adds quest skill. Lists available if no ID.

### @lostskill {<skill ID>}
Permanently removes quest skill.

### @useskill <skill ID> <level> <target>
Casts specified skill on target.
```
@useskill 28 5 Char2   // Level 5 Heal on Char2
```

---

<!-- RAG_CHUNK: player_info_commands_complete_001 -->
## 3. Player Information Commands

### @commands
Lists available @ commands for player.

### @charcommands
Lists available # commands for player.

### @help <command>
Displays help for specified command.

### @exp
Displays current level progress.
```
Base Level: 13 (3.323%) | Job Level: 10 (0.000%)
```

### @stats
Displays character stats in chat bar.

### @storagelist <player>
Shows Kafra storage contents of specified player.

### @cartlist <player>
Shows cart contents of specified player.

### @itemlist
Shows inventory contents of attached player.

### @who {<filter>}
Lists online characters with positions.

### @who2 {<filter>}
Lists online characters with job classes.

### @who3 {<filter>}
Lists online characters with parties/guilds.

### @whomap {<map>}
Lists characters on specific map with positions.

### @whomap2 {<map>}
Lists characters on specific map with job classes.

### @whomap3 {<map>}
Lists characters on specific map with parties/guilds.

### @whogm {<filter>}
Lists online GMs. Higher level GMs show name only.

### @users
Shows player distribution per map.
```
prontera: 1 (50%)
prt_fild01: 1 (50%)
all: 2
```

### @where <player>
Locates online player on map.

### @jailtime
Shows remaining jail time.

### @accinfo <player/account ID>
Detailed account information. Use `%` as wildcard.
```
@accinfo Test%
-- Account 2000001 --
User: user123 | GM Group: 0 | State: 0
Password: password123
Account e-mail: a@a.com
Last IP: 127.0.0.1 (Unknown)
-- Character Details --
[Slot/CID: 0/150001] Test1 | High Swordsman | Level: 99/50 | Off
```

### @mapinfo {<type 0-3>} {<map>}
Map information:
```
Type 0: General info + mapflags (default)
Type 1: Players
Type 2: NPCs
Type 3: Chatrooms
```

### @gat
Terrain/area debug information with cell types.

---

<!-- RAG_CHUNK: action_commands_complete_001 -->
## 4. Action Commands

### @me <message>
Displays as `*name message*` format.

### @storage
Opens Kafra storage.

### @mail
Opens mailbox.

### @auction
Opens auction window.

### @identify
Opens Identification window for unappraised items.

### @identifyall
Automatically identifies all unappraised items.

### @trade <player>
Opens trade window with specified player.

### @autotrade
Enables offline vending, then logs off.

---

<!-- RAG_CHUNK: monster_commands_complete_001 -->
## Monster Spawn Commands

### @monster <name/ID> {<amount>}
Spawns monsters at your location.

### @monstersmall <name/ID> {<amount>}
Spawns small-sized monsters.

### @monsterbig <name/ID> {<amount>}
Spawns large-sized monsters.

### @summon <name/ID> {<duration>}
Spawns monsters that follow you as master.

### @clone <player>
Spawns supportive player clone.

### @slaveclone <player>
Spawns supportive clone that follows you.

### @evilclone <player>
Spawns aggressive player clone.

---

<!-- RAG_CHUNK: item_commands_complete_001 -->
## Item Commands

### @item <name/ID>{:name:...} {<amount>}
Creates items. Use colon to create multiple different items.
```
@item 501:502:503 10    // 10 each of Red, Orange, Yellow Potions
```

### @item2 <name/ID> <qty> <identify> <refine> <attribute> <c1> <c2> <c3> <c4>
Creates item with parameters.
- `identify`: 0 = unidentified, 1 = identified
- `attribute`: 0 = normal, 1 = broken
- `c1-c4`: Card slots (any item ID)

### @itembound <name/ID>{:...} <amount> <bound type>
Creates bound items.
```
Bound Types:
1: Account      3: Party
2: Guild        4: Character
```

### @itembound2 <name/ID> <qty> <id> <ref> <attr> <c1> <c2> <c3> <c4> <bound>
Creates bound item with full parameters.

### @delitem <name/ID> <amount>
Deletes items from inventory.

### @produce <equip name/ID> <element> <# of Very's>
Creates elemental weapon.
```
@produce 1602 1 2   // "Very Very Strong Char's Ice Rod"
```

### @refine <position> <+/- amount>
Refines equipped item.
```
Position values:
0: All Equipment        64: Shoes
1: Lower Headgear       128: Right Accessory
2: Right Hand           256: Top Headgear
4: Garment              512: Mid Headgear
8: Left Accessory       65536: Shadow Armor
16: Body Armor          131072: Shadow Weapon
32: Left Hand           262144: Shadow Shield
                        524288: Shadow Shoes
                        1048576: Shadow Right Acc
                        2097152: Shadow Left Acc
```

### @grade <position> <+/- amount>
Enchantgrade equipped item (same positions as @refine).

### @repairall
Repairs all broken items in inventory.

### @dropall {<type>}
Drops all items by type.
```
-1: All (default)    4: Armors
0: Healing           5: Weapons
2: Useable           6: Cards
3: Etc               7: Pet Eggs
                     8: Pet Armors
                     10: Ammunition
```

### @stockall {<type>}
Transfers cart items to inventory (same types as @dropall).

### @storeall
Places all items in Kafra storage.

### @itemreset
Deletes all inventory items (not equipped).

### @clearstorage
Deletes all Kafra storage items.

### @cleargstorage
Deletes all guild storage items.

### @clearcart
Deletes all cart items.

### @cleanarea
Deletes floor items in sight range.

### @cleanmap
Deletes all floor items on map.

### @setcard <position> <slot> <card_id>
Adds card/enchant to equipment.
- `slot`: 0-3
- `card_id`: 0 to remove

---

<!-- RAG_CHUNK: warp_commands_complete_001 -->
## Warp & Movement Commands

### @save
Sets current position as save point.

### @memo {<0-2>}
Saves Warp Portal destination. Shows all if no position specified.

### @load
Warps to save point.

### @jump {<x> <y>}
Warps to coordinates on current map. Random if no coords.

### @go {<location/ID>}
Warps to predefined city locations.
Locations defined in `/src/map/atcommand.cpp`.

### @warp <map> {<x> <y>}
Warps to specified map and coordinates.

### @jumpto <player>
Warps to specified player.

### @follow <player>
Tracks player's movements until turned off.

### @recall <player>
Warps player to your position.

### @recallall
Warps all players on server to your position.

### @tonpc <npc name>
Warps to specified NPC.

---

<!-- RAG_CHUNK: combat_commands_complete_001 -->
## Combat Commands

### @killer
Allows attacking other players outside PvP.

### @killable
Allows being attacked by players outside PvP.

### @duel {<count>}
Creates duel room (2-65535 participants).

### @duel {<player>}
Invites player to duel.

### @invite <player>
Invites player to current duel.

### @accept
Accepts duel invitation.

### @reject
Rejects duel invitation.

### @leave
Leaves current duel.

### @heal {<hp> {<sp>}}
Heals HP and SP. Full heal if no parameters.

### @alive
Revives attached player.

### @raisemap
Revives all players on current map.

### @raise
Revives all players on server.

### @monsterignore
Makes you immune to attacks (untargetable).

### @hide
Toggles GM invisibility (invisible to players and monsters).

---

<!-- RAG_CHUNK: stat_commands_complete_001 -->
## Character Stat Commands

### @blvl <+/- amount>
Changes base level.

### @jlvl <+/- amount>
Changes job level.

### @str / @agi / @vit / @int / @dex / @luk <+/- amount>
Changes specific stat.

### @allstats {<+/- amount>}
Changes all stats. Sets to max (99) if no amount.

### @allskill
Gives all skills in current skill tree.

### @stpoint <+/- amount>
Changes unused status points.

### @skpoint <+/- amount>
Changes unused skill points.

### @resetstat
Resets all stats.

### @resetskill
Resets all skills.

### @reset
Resets both stats and skills.

### @feelreset
Resets Star Gladiator's marked maps.

### @hatereset
Resets Star Gladiator's marked monsters.

### @jobchange <job name/ID> {<upper>}
Changes job.
- `upper`: 0 = normal, 1 = advanced, 2 = baby
Note: Jobs 22 (Wedding), 26 (Summer), 27 (Christmas), 28 (Hanbok) not available.

### @speed <0-1000>
Sets movement/attack speed. Default: 150 (0 = fastest).

### @spiritball <0-100>
Summons spirit spheres.

### @soulball <0-20>
Summons soul spheres.

### @mount {<dragon color 1-5>}
Toggles dragon mount.

### @mount {<madogear type 0-2>}
Toggles Madogear.

### @mount2
Toggles cash mount.

### @zeny <+/- amount>
Changes Zeny.

### @cash <+/- amount>
Changes Cash Points.

### @points <+/- amount>
Changes Kafra Points.

---

<!-- RAG_CHUNK: appearance_commands_complete_001 -->
## Appearance Commands

### @model <hair style> <hair color> <cloth color>
Changes full appearance.

### @hairstyle <0-27>
Changes hair style (default range).

### @haircolor <0-8>
Changes hair color (default range).

### @dye <0-4>
Changes cloth color (default range).

### @bodystyle <0-1>
Changes body style.
Note: Requires `save_body_style` in `/conf/battle/client.conf`.

### @changelook {<position>} <view ID>
Changes appearance piece.
```
Positions:
1: Top Headgear      5: Shield
2: Middle Headgear   6: Shoes
3: Bottom Headgear   7: Robe
4: Weapon
```

### @costume {<name>}
Changes to costume. Removes if wearing one.
```
Available: Wedding, Xmas, Summer, Hanbok, Oktoberfest
```

### @changedress
Removes all costumes.

### @fakename {<name>}
Temporary name change until logout.

### @size <0-2>
Changes size (0=normal, 1=small, 2=large).

### @sizeall <0-2>
Changes size of all online players.

### @disguise <monster/npc ID>
Disguises as monster/NPC sprite.

### @undisguise
Removes disguise.

### @disguiseall <monster/npc ID>
Disguises all online players.

### @undisguiseall
Removes disguise from all players.

---

<!-- RAG_CHUNK: admin_commands_complete_001 -->
## 5. Administrative Commands

### @langtype <language>
Changes account language. Lists available if no parameter.

### @email <current> <new>
Changes account email.

### @changesex
Changes account gender.

### @changecharsex
Changes character gender.

### @marry <player1> <player2>
Marries two players.

### @divorce <player>
Divorces player.

### @adopt <player>
Adopts player (attached character as parent).

### @refineui
Opens refine UI (packet version 2016-10-12+).

### @stylist
Opens stylist UI (packet version 2015-11-04+).

### @enchantgradeui
Opens enchantgrade UI.

### @limitedsale
Opens limited sale window.

### @camerainfo {<range> <rotation> <latitude>}
Displays/sets camera position.

### @request <message>
Sends message to all connected GMs.

### @gmotd
Displays MOTD to all players.

### @broadcast <message>
Yellow announcement with name prefix (server-wide).

### @localbroadcast <message>
Yellow announcement with name prefix (map only).

### @kami <message>
Yellow announcement without name prefix.

### @kamib <message>
Blue announcement without name prefix.

### @kamic <color> <message>
Colored announcement (hexadecimal color).
```
@kamic FF0000 This message is red.
```

### @lkami <message>
Local announcement without name prefix.

### @killmonster
Kills all monsters on map.

### @killmonster2
Kills all monsters without drops (except looted).

### @kill
Kills attached player.

### @nuke <player>
Kills player with area splash damage.

### @doommap
Kills all players on map.

### @doom
Kills all players on server.

### @mute <time> <player>
Mutes player (prevents talking, skills, commands).

### @mutearea <time>
Mutes all players on screen.

### @unmute <player>
Unmutes player.

### @jail <player>
Jails player indefinitely.

### @jailfor <time> <player>
Jails player for specified time.
Time format: y/a (year), m (month), d/j (day), h (hour), mn (minute), s (second)

### @unjail <player>
Releases player from jail.

### @kick <player>
Disconnects player.

### @kickall
Disconnects all players.

### @ban <+/- time> <player>
Bans account for specified time.
```
@ban +2d Char2   // Bans for 2 days
```

### @unban <player>
Unbans account.

### @block <player>
Blocks account indefinitely.

### @unblock <player>
Unblocks account.

### @charban <+/- time> <player>
Bans specific character (not account).

### @charunban <player>
Unbans character.

### @mapexit
Graceful server shutdown (saves all data).

---

<!-- RAG_CHUNK: reload_commands_complete_001 -->
## Reload Commands

### @reload <type>
Reloads specified database or configuration.

**Database Reloads:**
| Command | Database |
|---------|----------|
| @reloadinstancedb | Instance Database |
| @reloaditemdb | Item Database |
| @reloadmobdb | Monster Database |
| @reloadquestdb | Quest Database |
| @reloadscript | NPC Scripts + Barter |
| @reloadskilldb | Skill Database |
| @reloadachievementdb | Achievement Database |
| @reloadattendancedb | Attendance Database |
| @reloadbarterdb | Barter Database |

**Configuration Reloads:**
| Command | Configuration |
|---------|---------------|
| @reloadatcommand | Atcommand Settings |
| @reloadbattleconf | Battle Settings |
| @reloadmotd | Message of the Day |
| @reloadmsgconf | Message Configuration |
| @reloadpcdb | Player Settings |
| @reloadstatusdb | Status Settings |

**Affected Files by Reload Type:**
```
atcommand: atcommands.yml, groups.conf
battleconf: battle_athena.conf, battle_conf.txt
instancedb: instance_db.yml
itemdb: item_db.yml, item_group_db.yml, item_noequip.txt,
        item_combos.yml, item_randomopt_db.yml, item_randomopt_group.yml
mobdb: mob_db.yml, mob_item_ratio.yml, mob_chat_db.yml, mob_avail.yml,
       mob_summon.yml, pet_db.yml, homunculus_db.txt, homun_skill_tree.txt,
       exp_homun.yml, mercenary_db.yml, elemental_db.yml
pcdb: statpoint.yml, job_exp.yml, skill_tree.yml, attr_fix.yml,
      job_stats.yml, job_basepoints.yml, level_penalty.yml
skilldb: skill_db.yml, skill_nocast_db.txt, skill_changematerial_db.txt,
         skill_damage_db.txt, abra_db.yml, create_arrow_db.yml,
         produce_db.txt, spellbook_db.yml, magicmushroom_db.yml
statusdb: attr_fix.yml, size_fix.yml, refine.yml
```

### @set <variable> {<value>}
Gets/sets player or account variable.

### @setbattleflag <flag> <value> {<reload>}
Changes battle_config without reboot.

### @adjgroup <group ID>
Temporary group change (until logout).

### @addperm {<permission>}
Temporarily adds permission (until logout).

### @rmvperm {<permission>}
Temporarily removes permission.

---

<!-- RAG_CHUNK: npc_commands_complete_001 -->
## NPC Commands

### @npcmove <x> <y> <npc name>
Moves NPC to coordinates on its map.

### @hidenpc <npc name>
Hides NPC sprite.

### @shownpc <npc name>
Shows NPC sprite.

### @loadnpc <path>
Loads NPC script file.
```
@loadnpc npc/custom/jobmaster.txt
```

### @unloadnpc <npc name>
Unloads single NPC.

### @unloadnpcfile <path>
Unloads all NPCs in file.

### @reloadnpcfile <path>
Unloads and reloads NPCs from file.

### @npctalk <npc name> <message>
Makes NPC say message.

### @vip <+/- time> <player>
Sets VIP mode for specified time.
```
@vip +2h mychar   // 2 hours VIP
```

### @fullstrip <player>
Unequips all items from player.

### @cart <0-9>
Gives/removes cart.
```
0: Remove cart
1-5: Normal carts
6-9: New carts (PACKETVER >= 20120201)
```

### @cloneequip <char_id/"name">
Clones equipment from another player.

### @clonestat <char_id/"name">
Clones stats from another player.

### @resetcooltime
Resets all skill cooldowns (player, homunculus, mercenary).

---

<!-- RAG_CHUNK: party_commands_complete_001 -->
## 6. Party Commands

### @party <party_name>
Creates new party with you as leader.

### @partyoption <pickup: yes/no> <item: yes/no>
Changes party sharing options.

### @changeleader <member>
Transfers party leadership (leader only).

### @partyrecall <party name>
Warps all online party members to you.

### @partyspy <party name>
Spy on party chat.
Requires `enable_spy: yes` in server config.

### @partysharelvl <value>
Adjusts party share level range (temporary).

---

<!-- RAG_CHUNK: guild_commands_complete_001 -->
## 7. Guild Commands

### @guild <guild name>
Creates new guild with you as guildmaster.

### @breakguild
Disbands your guild (guildmaster only).

### @changegm <member>
Transfers guild leadership (guildmaster only).

### @guildstorage
Opens guild storage.

### @glvl <+/- amount>
Changes guild level.

### @disguiseguild <monster/npc ID> <guild>
Disguises all online guild members.

### @undisguiseguild
Removes disguise from all guild members.

### @sizeguild <size> <guild>
Changes size of all online guild members.

### @guildrecall <guild name>
Warps all online guild members to you.

### @guildspy <guild name>
Spy on guild chat.
Requires `enable_spy: yes`.

---

<!-- RAG_CHUNK: pet_commands_complete_001 -->
## 8. Pet Commands

### @makeegg <egg ID>
Creates pet egg.

### @hatch
Opens hatch window (like Pet Incubator).

### @pettalk <message>
Makes pet say message.

### @petrename
Allows renaming pet again.

### @petfriendly <0-1000>
Sets pet intimacy (1000 = Loyal).

### @pethungry <0-100>
Sets pet hunger (100 = Stuffed).

---

<!-- RAG_CHUNK: homunculus_commands_complete_001 -->
## 9. Homunculus Commands

### @makehomun <ID>
Creates specified homunculus.

### @homevolution
Evolves homunculus if possible.

### @hommutate {<ID>}
Mutates homunculus. Random ID if not specified.

### @hominfo
Displays homunculus stats.
```
HP: 153/153 - SP: 54/54
ATK: 59 - MATK: 69~69
Hungry: 29 - Intimacy: 5
Stats: Str 24 / Agi 25 / Vit 18 / Int 40 / Dex 31 / Luk 14
```

### @homstats
Displays growth stats with ranges.
```
Homunculus growth stats (Lv 1 Lif):
Max HP: 153 (151~160)
Max SP: 54 (50~60)
Str: 20 (18~22)
...
```

### @homshuffle
Recalculates homunculus stats (as if re-leveled from 1).

### @homtalk <message>
Makes homunculus say message.

### @homlevel <+/- amount>
Changes homunculus level.

### @homfriendly <0-1000>
Sets homunculus intimacy (1000 = Loyal).

### @homhungry <0-100>
Sets homunculus hunger (100 = Stuffed).

---

<!-- RAG_CHUNK: channel_commands_complete_001 -->
## 10. Channel Commands

### @join <#channel> {<password>}
Joins specified channel.

### @channel join <#channel> {<password>}
Alternative join syntax.

### @channel leave <#channel>
Leaves channel.

### @channel create <#channel> <password>
Creates new channel.
Requires `allow_user_channel_creation` in `/conf/channels.conf`.

### @channel delete <#channel>
Destroys channel (owner or admin only).

### @channel list
Lists all public channels.

### @channel list mine
Lists channels you've joined.

### @channel list colors
Lists available colors.

### @fontcolor <color>
Sets your channel chat color. "Normal" resets.
Requires `ColorOverride` enabled.

### @channel setcolor <#channel> <color>
Changes channel text color (owner/admin only).

### @channel setopt <#channel> <option> <value>
Channel options:
```
JoinAnnounce <1|0>   - Announce when players join
MessageDelay <0-10>  - Message delay in seconds
ColorOverride <1|0>  - Allow @fontcolor
```

### @channel ban <#channel> <player>
Bans player from channel.

### @channel unban <#channel> <player>
Unbans player.

### @channel unbanall <#channel>
Clears all bans.

### @channel banlist <#channel>
Shows banned players.

### @channel bindto <#channel>
Binds global chat to channel.

### @channel unbind
Unbinds global chat from channel.

---

<!-- RAG_CHUNK: quest_commands_complete_001 -->
## Quest Commands

### @setquest <quest ID>
Starts/activates quest.

### @erasequest <quest ID>
Removes quest from log.

### @completequest <quest ID>
Completes quest.

### @checkquest <quest ID>
Checks quest status.

---

<!-- RAG_CHUNK: clan_commands_complete_001 -->
## 11. Clan Commands

### @clanspy <clan name>
Spy on clan chat.
Requires `enable_spy: yes`.

---

<!-- RAG_CHUNK: charcommand_syntax_001 -->
## Charcommand (#) Syntax

Character commands target other players:
```
#command <player> [parameters]
```

Most @ commands have # equivalents:
```
#item Player_Name 501 100    // Give items to player
#blvl Player_Name +10        // Add 10 base levels
#jobchange Player_Name 4001  // Change player's job
#warp Player_Name prontera 156 180
```

---

<!-- RAG_CHUNK: command_restrictions_001 -->
## Command Restrictions

Some commands cannot be used from console or scripts:
- @go
- @warp
- @blvl, @jlvl
- @jobchange
- @kick (restricted for autotraders)
- @reload, @reloadscript

Check `/src/map/atcommand.cpp` for full restriction list.

---

#rathena #atcommand #charcommand #gm #admin #commands #reference #complete
