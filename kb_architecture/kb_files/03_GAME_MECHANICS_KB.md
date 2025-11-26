---
title: rAthena Game Mechanics Reference
type: mechanics_reference
category: rathena_admin
tags: [mapflag, atcommand, permissions, mob_mode, game_rules]
version: 2.0
mode: SCRIPTING
secondary_modes: [DEV]
chunk_strategy: BY_ENTRY
---

# rAthena Game Mechanics Reference

This KB covers mapflags, atcommands, permissions, and monster behavior modes.

**Search:** Use `*mapflag_name` for mapflags, `@command` for atcommands.

---

# Mapflags Reference

Mapflags determine map behavior. Set with: `<map>	mapflag	<flag>`

## 1. Restriction Mapflags

### *noreturn
Disables map-warping items:
- Butterfly Wing (602)
- Yellow/Green/Red/Blue Butterfly Wing (14582-14585)
- Siege Teleport Scroll (14591)
- Dungeon Teleport Scroll 1/2/3 (14527, 14581, 12352)

Also blocks `warpparty` and `warpguild` to other maps.

---

### *noteleport
Disables ALL teleportation within map:
- Fly Wing (601), Giant Fly Wing (12212) disabled
- Skills AL_TELEPORT, TK_HIGHJUMP, SC_DIMENSIONDOOR disabled
- RG_INTIMIDATE, NPC_EXPULSION won't teleport
- Script "Random" destination fails
- @jump disabled

---

### *nowarp
Disables warping FROM a map:
- `warpparty`, `warpguild` won't work
- @warp, @go, @load, @jump disabled
- @partyrecall, @guildrecall, @recallall blocked
- GD_EMERGENCYCALL won't warp players

---

### *nowarpto
Disables warping TO a map:
- @warp, @go, @load, @jump to this map disabled
- @partyrecall, @guildrecall, @recallall disabled
- /memo disabled
- GD_EMERGENCYCALL disabled (with config flag)

---

### *nogo
Disables @go command on a map.

---

### *nosave <map>
Disables auto-save. Players respawn at `<map>` or `SavePoint`.
```
prontera,150,150	mapflag	nosave	SavePoint
```

---

### *nomemo
Disables /memo and marriage skills (WE_CALLPARTNER, WE_CALLPARENT, WE_CALLBABY).

---

### *noitemconsumption
Disables all item usage on a map.

---

### *notrade
Disables trading on a map.

---

### *nodrop
Disables dropping items (may still drop if inventory full with config).

---

### *noloot / *nomobloot / *nomvploot
Disables monster drops. `noloot` = both mob and MVP.

---

### *noexp / *nobaseexp / *nojobexp
Disables EXP gain. `noexp` = both base and job.

---

### *nopenalty / *noexppenalty / *nozenypenalty
Disables death penalties. `nopenalty` = both EXP and Zeny.

---

### *nochat
Disables chatroom creation.

---

### *novending
Disables MC_VENDING shop creation.

---

### *nobuyingstore
Disables ALL_BUYING_STORE shop creation.

---

### *nousecart
Disables cart usage.

---

### *noskill
Disables all skill usage.

---

### *restricted <zone>
Disables items/skills based on zone. Zones defined in:
- `db/(pre-)re/item_noequip.txt`
- `db/(pre-)re/skill_nocast_db.txt`

**Zones:**
| Zone | Location |
|------|----------|
| 1 | Aldebaran Turbo Track |
| 2 | Jail |
| 3 | Izlude Battle Arena |
| 4 | WoE:SE Maps |
| 5 | Sealed Shrine |
| 6 | Instances (Endless Tower, Orc's Memory, Nidhoggr) |
| 7 | Towns |
| 8 | WoE:TE Dungeons |

---

### *monster_noteleport
Prevents monsters from teleporting (including RG_INTIMIDATE).

---

### *nobranch
Disables monster-spawning items:
- Dead Branch (604)
- Bloody Branch (12103)
- Poring Box (12109)
- Red Pouch (12024)

---

### *noicewall
Disables WZ_ICEWALL.

---

### *nocommand <group_level>
Disables commands for players below specified group level.

---

### *notomb
Disables MVP tombs.

---

### *nocostume
Hides costume sprites (effects still work).

---

## 2. Battle Mapflags

### *pvp / *pvp_noparty / *pvp_noguild / *pvp_nocalcrank
Enables PvP mode:
- `pvp_noparty` - ignore party alliance
- `pvp_noguild` - ignore guild alliance
- `pvp_nocalcrank` - disable ranking

---

### *pvp_nightmaredrop <id>,<type>,<rate>
Drop items on death:
- `id`: item ID or "random"
- `type`: "inventory", "equip", or "all"
- `rate`: drop chance (10000 = 100%)

---

### *gvg / *gvg_noparty / *gvg_castle / *gvg_dungeon / *gvg_te / *gvg_te_castle
Enables GvG mode:
- `gvg_noparty` - ignore party
- `gvg_castle` - guild castle (WoE only)
- `gvg_dungeon` - warp out after 2 deaths
- `gvg_te*` - WoE:TE maps

---

### *battleground {<type>}
Enables Battlegrounds. Type 2 shows scoreboard.

---

### *partylock / *guildlock
Prevents party/guild changes on map.

---

### *skill_damage {<skill>,<caster>,<dmg_pc>,<dmg_mob>,<dmg_boss>,<dmg_other>}
Adjusts skill damage on map:
```
prontera,150,150	mapflag	skill_damage	SM_BASH,BL_PC,50,100,100,100
```
- Caster: BL_PC, BL_MOB, BL_PET, BL_HOM, BL_MER, BL_ELEM
- Damage: -100 to 100000 percent

---

### *skill_duration <skill>,<percentage>
Adjusts trap duration:
```
prtg_cas01	mapflag	skill_duration	HT_ANKLESNARE,400
```

---

### *invincible_time <ms>
Sets invincibility duration on map load.

---

## 3. Map Effects

### Weather Effects
```
*clouds / *clouds2 / *fireworks / *fog / *leaves / *sakura / *snow
```

### *nightenabled
Displays night mode effects (outdoor maps).

---

## 4. Miscellaneous

### *town
Marks as town (enables mail, disables kill stealing).

### *reset
Allows Neuralizer (12213) usage.

### *bexp <rate> / *jexp <rate>
Changes EXP rates (100 = 1x):
```
prontera,150,150	mapflag	bexp	200
```

### *loadevent
Triggers `OnPCLoadMapEvent` label on map entry.

### *allowks
Allows kill stealing (@noks useless).

### *autotrade
Allows @autotrade (requires `at_mapflag` config).

### *hidemobhpbar
Hides monster HP bars.

### *specialpopup <id>
Shows popup on map entry.

---

# Monster Modes Reference

Monster AI behavior flags (set in mob_db.yml).

## Core Modes

| Mode | Value | Description |
|------|-------|-------------|
| MD_CANMOVE | 0x0001 | Can move |
| MD_LOOTER | 0x0002 | Picks up items |
| MD_AGGRESSIVE | 0x0004 | Attacks on sight |
| MD_ASSIST | 0x0008 | Helps attacked allies |
| MD_CASTSENSOR_IDLE | 0x0010 | Reacts to casting (idle) |
| MD_BOSS | 0x0020 | Boss type (MVP) |
| MD_PLANT | 0x0040 | Plant type (no damage numbers) |
| MD_CANATTACK | 0x0080 | Can attack |
| MD_DETECTOR | 0x0100 | Detects hidden players |
| MD_CASTSENSOR_CHASE | 0x0200 | Reacts to casting (chasing) |
| MD_CHANGECHASE | 0x0400 | Changes target while chasing |
| MD_ANGRY | 0x0800 | Attacks back when hit |
| MD_CHANGETARGET_MELEE | 0x1000 | Changes to melee attacker |
| MD_CHANGETARGET_CHASE | 0x2000 | Changes to closer target |
| MD_TARGETWEAK | 0x4000 | Targets weakest first |
| MD_NOKNOCKBACK | 0x8000 | Immune to knockback |

## Special Modes

| Mode | Value | Description |
|------|-------|-------------|
| MD_RANDOMTARGET | 0x10000 | Random target selection |
| MD_IGNOREMELEE | 0x20000 | Takes 1 damage from melee |
| MD_IGNOREMAGIC | 0x40000 | Takes 1 damage from magic |
| MD_IGNORERANGED | 0x80000 | Takes 1 damage from ranged |
| MD_MVP | 0x100000 | True MVP (death announcement) |
| MD_IGNOREMISC | 0x200000 | Takes 1 damage from misc |
| MD_KNOCKBACK_IMMUNE | 0x400000 | Full knockback immunity |
| MD_TELEPORT_BLOCK | 0x800000 | Blocks teleport when attacked |
| MD_FIXED_ITEMDROP | 0x1000000 | Fixed item drop (no modify) |
| MD_DETECTOR_INSIGHT | 0x2000000 | Detects hidden at range |
| MD_STATUS_IMMUNE | 0x4000000 | Immune to status effects |
| MD_SKILL_IMMUNE | 0x8000000 | Immune to skills |

---

# Permissions Reference

Group permission flags for `/conf/groups.conf`.

## Command Permissions

| Permission | Description |
|------------|-------------|
| can_trade | Can trade with others |
| can_party | Can create/join parties |
| can_shout | Can use global chat |
| all_skill | Access to all skills |
| all_equipment | Can equip any item |
| skill_unconditional | Use skills without requirements |
| join_chat | Can join chat rooms |
| kick_chat | Can kick from chat rooms |
| hide_session | Hidden from @who |
| who_display_aid | Show account ID in @who |
| hack_info | Receive hack attempt info |
| any_warp | Warp to any map |
| view_hpmeter | View party HP meter |
| view_equipment | View others' equipment |
| disable_pvm | Cannot attack monsters |
| disable_pvp | Cannot attack players |

## Administrative Permissions

| Permission | Description |
|------------|-------------|
| command_enable | Enable command usage |
| bypass_stat_onclone | Bypass @clone stats |
| bypass_max_stat | Bypass max stat limit |
| show_bossmobinfo | Boss spawn info |
| disable_pickup | Cannot pick up items |
| disable_store | Cannot use storage |
| can_trade_bounded | Trade bound items |
| item_unconditional | Use any item |
| receive_requests | Receive @request |
| show_bossmobinfo_2 | Extra boss info |

---

*KB Version 2.0 | Mode: SCRIPTING/DEV | Source: doc/mapflags.txt, doc/mob_db_mode_list.txt, doc/permissions.txt*
