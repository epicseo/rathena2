# rAthena Map Flags - Complete Reference
## All 84 Map Flags with Documentation

---

<!-- RAG_CHUNK: mapflag_overview_001 -->
## Map Flag Overview

### Setting Map Flags

**In NPC Scripts:**
```c
<map>	mapflag	<flag>
<map>	mapflag	<flag>	<value>
```

**Via Script Command:**
```c
setmapflag("<map>", <flag>{, <value>});
removemapflag("<map>", <flag>);
getmapflag("<map>", <flag>);
```

**Via @command:**
```
@mapflag <flag> {<value>}
```

---

<!-- RAG_CHUNK: restriction_flags_001 -->
## Restriction Flags

### Movement Restrictions
| Flag | Effect |
|------|--------|
| MF_NOWARP | Cannot @warp to this map |
| MF_NOWARPTO | Cannot @warp others here |
| MF_NOTELEPORT | Cannot use teleport skills/items |
| MF_NOGO | Cannot @go to this map |
| MF_NORETURN | Cannot use Butterfly Wing / Return |
| MF_NOMEMO | Cannot set memo point |

### Action Restrictions
| Flag | Effect |
|------|--------|
| MF_NOBRANCH | Cannot use Dead Branch items |
| MF_NOSAVE | Cannot save here (set nosave point) |
| MF_NOSKILL | Cannot use skills |
| MF_NOICEWALL | Cannot use Ice Wall |
| MF_NOTRADE | Cannot trade |
| MF_NODROP | Cannot drop items |
| MF_NOLOOT | Cannot loot items |
| MF_NOCHAT | Cannot create chat rooms |
| MF_NOUSECART | Cannot use pushcart |
| MF_NOVENDING | Cannot vend |
| MF_NOBUYINGSTORE | Cannot open buying store |
| MF_NOCOMMAND | Disable @commands (value = min GM level) |
| MF_NOBANK | Cannot use bank |
| MF_NORODEX | Cannot use mail (RoDEX) |
| MF_NOCASHSHOP | Cannot use cash shop |
| MF_NOCOSTUME | Costumes not displayed |

### Item Restrictions
| Flag | Effect |
|------|--------|
| MF_NOITEMCONSUMPTION | Items cannot be consumed |

**Example:**
```c
// Disable teleport on custom map
prontera	mapflag	noteleport

// Allow warping but not @go
prt_maze01	mapflag	nogo
```

---

<!-- RAG_CHUNK: pvp_flags_001 -->
## PvP Flags

### PvP Mode
| Flag | Effect |
|------|--------|
| MF_PVP | Enable PvP mode |
| MF_PVP_NOPARTY | Party members can attack each other |
| MF_PVP_NOGUILD | Guild members can attack each other |
| MF_PVP_NOCALCRANK | Don't calculate PvP ranking |
| MF_PVP_NIGHTMAREDROP | Drop items on death |

### GvG Mode
| Flag | Effect |
|------|--------|
| MF_GVG | Enable Guild vs Guild mode |
| MF_GVG_CASTLE | WoE castle map |
| MF_GVG_DUNGEON | GvG dungeon map |
| MF_GVG_NOPARTY | Ignore party in GvG |
| MF_GVG_TE | WoE:TE mode |
| MF_GVG_TE_CASTLE | WoE:TE castle |

### Battleground
| Flag | Effect |
|------|--------|
| MF_BATTLEGROUND | Battleground map (value = type) |

**Example:**
```c
// PvP Arena
pvp_room	mapflag	pvp

// GvG Castle
prtg_cas01	mapflag	gvg_castle
prtg_cas01	mapflag	gvg
```

---

<!-- RAG_CHUNK: exp_drop_flags_001 -->
## EXP & Drop Flags

### Experience
| Flag | Effect |
|------|--------|
| MF_NOEXP | No EXP gain |
| MF_NOBASEEXP | No base EXP |
| MF_NOJOBEXP | No job EXP |
| MF_BEXP | Base EXP rate modifier (% of normal) |
| MF_JEXP | Job EXP rate modifier (% of normal) |

### Drop
| Flag | Effect |
|------|--------|
| MF_NOMOBLOOT | Monsters don't drop items |
| MF_NOMVPLOOT | MVP doesn't drop items |

### Penalty
| Flag | Effect |
|------|--------|
| MF_NOPENALTY | No EXP/item penalty on death |
| MF_NOEXPPENALTY | No EXP penalty on death |
| MF_NOZENYPENALTY | No zeny penalty on death |
| MF_NORENEWALDROPPENALTY | No Renewal drop penalty |
| MF_NORENEWALEXPPENALTY | No Renewal EXP penalty |

**Example:**
```c
// Training map with 200% EXP
training_ground	mapflag	bexp	200
training_ground	mapflag	jexp	200

// No death penalty
guild_room	mapflag	nopenalty
```

---

<!-- RAG_CHUNK: misc_flags_001 -->
## Miscellaneous Flags

### Visual/Weather
| Flag | Effect |
|------|--------|
| MF_CLOUDS | Display clouds effect |
| MF_CLOUDS2 | Display clouds effect (type 2) |
| MF_FOG | Display fog effect |
| MF_FIREWORKS | Display fireworks |
| MF_SAKURA | Display sakura petals |
| MF_LEAVES | Display falling leaves |
| MF_RAIN | Display rain |
| MF_SNOW | Display snow |
| MF_NIGHTENABLED | Enable day/night cycle |

### Monster Behavior
| Flag | Effect |
|------|--------|
| MF_MONSTER_NOTELEPORT | Monsters can't teleport |
| MF_HIDEMOBHPBAR | Hide monster HP bars |

### System
| Flag | Effect |
|------|--------|
| MF_LOADEVENT | Trigger OnPCLoadMapEvent |
| MF_TOWN | Town map (affects EXP gain) |
| MF_RESET | Reset stats on map entry |
| MF_NOTOMB | Don't spawn MVP tomb |
| MF_ALLOWKS | Allow kill stealing |
| MF_AUTOTRADE | Allow @autotrade |
| MF_NOMACROCHECKER | Disable macro check |
| MF_NOMAPCHANNELAUTOJOIN | Don't auto-join map channel |
| MF_SPECIALPOPUP | Enable special popup |
| MF_NOSUNMOONSTARMIRACLE | Disable TK miracle |
| MF_INVINCIBLE_TIME | Set invincibility time after warp |
| MF_FORCEMINEFFECT | Force minimal effects |
| MF_NODYNAMICNPC | Disable dynamic NPC spawning |

### Private Airship
| Flag | Effect |
|------|--------|
| MF_PRIVATEAIRSHIP_SOURCE | Airship can depart from here |
| MF_PRIVATEAIRSHIP_DESTINATION | Airship can land here |

### Lock
| Flag | Effect |
|------|--------|
| MF_GUILDLOCK | Cannot leave guild |
| MF_PARTYLOCK | Cannot leave party |

### Restricted
| Flag | Effect |
|------|--------|
| MF_RESTRICTED | Enable zone restrictions |

---

<!-- RAG_CHUNK: skill_flags_001 -->
## Skill Modification Flags

### Skill Damage
| Flag | Format | Effect |
|------|--------|--------|
| MF_SKILL_DAMAGE | `skill_damage,<skill>,<rate>` | Modify skill damage |

**Example:**
```c
// Reduce all skill damage by 50% on map
pvp_arena	mapflag	skill_damage	all	50
```

### Skill Duration
| Flag | Format | Effect |
|------|--------|--------|
| MF_SKILL_DURATION | `skill_duration,<skill>,<rate>` | Modify skill duration |

---

<!-- RAG_CHUNK: nosave_flag_001 -->
## NoSave Configuration

### Syntax
```c
<map>	mapflag	nosave	<save_map>,<x>,<y>
<map>	mapflag	nosave	SavePoint
```

**Examples:**
```c
// Respawn at Prontera when dying on this map
dangerous_map	mapflag	nosave	prontera,156,181

// Respawn at player's save point
instance_map	mapflag	nosave	SavePoint
```

---

<!-- RAG_CHUNK: mapflag_example_001 -->
## Complete Examples

### PvP Arena Setup
```c
// PvP settings
pvp_arena	mapflag	pvp
pvp_arena	mapflag	pvp_nocalcrank
pvp_arena	mapflag	nopenalty
pvp_arena	mapflag	noteleport
pvp_arena	mapflag	nowarp
pvp_arena	mapflag	nowarpto
pvp_arena	mapflag	nosave	prontera,156,181
```

### Training Ground
```c
// Training map settings
training	mapflag	bexp	200
training	mapflag	jexp	200
training	mapflag	nopenalty
training	mapflag	noteleport
training	mapflag	nobranch
training	mapflag	town
```

### Instance Map
```c
// Instance settings
instance_map	mapflag	nosave	SavePoint
instance_map	mapflag	noteleport
instance_map	mapflag	nowarp
instance_map	mapflag	nowarpto
instance_map	mapflag	noreturn
instance_map	mapflag	nomemo
```

### WoE Castle
```c
// Castle settings
prtg_cas01	mapflag	gvg_castle
prtg_cas01	mapflag	gvg
prtg_cas01	mapflag	nowarpto
prtg_cas01	mapflag	noteleport
prtg_cas01	mapflag	nosave	prontera,156,181
prtg_cas01	mapflag	nopenalty
```

---

#rathena #mapflag #pvp #gvg #restriction #exp #drop #weather
