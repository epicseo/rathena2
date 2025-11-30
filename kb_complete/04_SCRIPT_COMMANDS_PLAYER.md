# rAthena Script Commands - Player Reference
## Complete Player Management Commands

---

<!-- RAG_CHUNK: warp_commands_001 -->
## Warp Commands

### warp
**Syntax:** `warp "<map>",<x>,<y>{,<char id>};`

Teleport player to location.

**Special Values:**
- Map `"Random"` - Random spot on current map
- Map `"Save"` or `"SavePoint"` - Return to save point
- Coords `0,0` - Random coordinates on map

**Examples:**
```c
warp "prontera", 155, 180;       // Warp to Prontera
warp "Random", 0, 0;             // Random on current map
warp "Save", 0, 0;               // To save point
warp "prt_in", 0, 0;             // Random in prt_in
```

---

### areawarp
**Syntax:** `areawarp "<from map>",<x1>,<y1>,<x2>,<y2>,"<to map>",<x>,<y>{,<x2>,<y2>};`

Warp all players in area.

**Example:**
```c
areawarp "prt_church", 0, 0, 100, 100, "prontera", 155, 180;
```

---

### warpparty
**Syntax:** `warpparty "<map>",<x>,<y>,<party id>{,"<from map>"{,<range x>,<range y>}};`

Warp entire party.

**Example:**
```c
warpparty "prontera", 155, 180, getcharid(1);
```

---

### warpguild
**Syntax:** `warpguild "<map>",<x>,<y>,<guild id>{,"<from map>"};`

Warp entire guild.

---

### warppartner
**Syntax:** `warppartner("<map>",<x>,<y>)`

Warp married partner to location.

---

### warpwaitingpc
**Syntax:** `warpwaitingpc "<map>",<x>,<y>{,<count>{,"<npc name>"}};`

Warp players from waiting room.

---

### warpportal
**Syntax:** `warpportal <x>,<y>,"<dest map>",<dest x>,<dest y>;`

Create temporary warp portal on current map.

---

### mapwarp
**Syntax:** `mapwarp "<from map>","<to map>",<x>,<y>{,<x1>,<y1>,<x2>,<y2>};`

Warp all players on map.

---

<!-- RAG_CHUNK: savepoint_001 -->
## Save Point

### savepoint / save
**Syntax:** `savepoint "<map>",<x>,<y>{,<range x>,<range y>};`
**Syntax:** `save "<map>",<x>,<y>;`

Set player's respawn point.

**Example:**
```c
savepoint "prontera", 155, 180;
```

---

### getsavepoint
**Syntax:** `getsavepoint(<type>{,<char id>})`

Get save point info.

| Type | Returns |
|------|---------|
| 0 | Map name (string) |
| 1 | X coordinate |
| 2 | Y coordinate |

**Example:**
```c
.@map$ = getsavepoint(0);
.@x = getsavepoint(1);
.@y = getsavepoint(2);
```

---

<!-- RAG_CHUNK: heal_commands_001 -->
## Heal Commands

### heal
**Syntax:** `heal <hp>,<sp>{,<char id>};`

Heal/damage player HP and SP. Negative values damage.

**Example:**
```c
heal 100, 50;      // Heal 100 HP, 50 SP
heal -500, 0;      // Damage 500 HP
percentheal 100, 100;  // Full heal
```

---

### healap
**Syntax:** `healap <ap>{,<char id>};`

Heal/damage AP (4th job classes).

---

### percentheal
**Syntax:** `percentheal <hp%>,<sp%>{,<char id>};`

Heal by percentage. Negative values damage.

**Example:**
```c
percentheal 50, 50;   // Heal 50% HP and SP
percentheal 100, 100; // Full heal
percentheal -10, 0;   // Damage 10% HP
```

---

### itemheal
**Syntax:** `itemheal <hp>,<sp>{,<char id>};`

Like heal but affected by VIT/INT modifiers (for item scripts).

---

### recovery
**Syntax:** `recovery <type>{,<option>,<revive pos>{,<map>,<x>,<y>}};`

Mass recovery command.

**Types:**
- 0 = HP recovery
- 1 = SP recovery
- 2 = HP+SP recovery

**Options:**
- 1 = All players online
- 2 = All guild members
- 3 = All party members
- 4 = All map players

---

<!-- RAG_CHUNK: status_points_001 -->
## Status Points

### statusup
**Syntax:** `statusup <type>{,<char id>};`

Increase stat using status points (like clicking +).

**Types:**
```c
bStr    bAgi    bVit    bInt    bDex    bLuk
bPow    bSta    bWis    bSpl    bCon    bCrt
```

---

### statusup2
**Syntax:** `statusup2 <type>,<amount>{,<char id>};`

Add stat points directly (bypass status points).

**Example:**
```c
statusup2 bStr, 10;  // +10 STR permanently
```

---

### traitstatusup / traitstatusup2
Same but for 4th job trait stats.

---

### needed_status_point
**Syntax:** `needed_status_point(<type>,<val>{,<char id>})`

Calculate status points needed to reach value.

---

### needed_trait_point
Calculate trait points needed.

---

### resetstatus / resetskill
**Syntax:** `resetstatus({<char id>});`
**Syntax:** `resetskill({<char id>});`

Reset stats or skills.

---

### resetlvl
**Syntax:** `resetlvl(<type>{,<char id>});`

Reset character level.

| Type | Effect |
|------|--------|
| 1 | Rebirth (to High Novice) |
| 2 | Baby job |
| 3 | To level 1 (keep job) |
| 4 | Reset stats only |

---

<!-- RAG_CHUNK: experience_001 -->
## Experience

### getexp
**Syntax:** `getexp <base>,<job>{,<char id>};`

Give experience (affected by rates).

**Example:**
```c
getexp 10000, 5000;  // 10000 base, 5000 job
```

---

### getexp2
**Syntax:** `getexp2 <base>,<job>{,<char id>};`

Give experience (ignores rates).

---

### getbaseexp_ratio / getjobexp_ratio
**Syntax:** `getbaseexp_ratio(<value>,<base mob id>{,<char id>})`

Calculate EXP ratio based on monster.

---

<!-- RAG_CHUNK: job_commands_001 -->
## Job Commands

### jobchange
**Syntax:** `jobchange <job id>{,<upper>{,<char id>}};`

Change player's job class.

**Upper Values:**
- 0 = Normal
- 1 = High/Trans
- 2 = Baby
- -1 = Auto-detect

**Common Job IDs:**
```c
Job_Novice          = 0
Job_Swordman        = 1
Job_Mage            = 2
Job_Archer          = 3
Job_Acolyte         = 4
Job_Merchant        = 5
Job_Thief           = 6
Job_Knight          = 7
Job_Priest          = 8
Job_Wizard          = 9
Job_Blacksmith      = 10
Job_Hunter          = 11
Job_Assassin        = 12
Job_Knight2         = 13 (Peco Knight)
Job_Crusader        = 14
Job_Monk            = 15
Job_Sage            = 16
Job_Rogue           = 17
Job_Alchemist       = 18
Job_Bard            = 19
Job_Dancer          = 20
Job_Crusader2       = 21 (Peco Crusader)
Job_Wedding         = 22
Job_Super_Novice    = 23
Job_Gunslinger      = 24
Job_Ninja           = 25
Job_Xmas            = 26
Job_Summer          = 27
Job_Novice_High     = 4001
// ... and many more (see db/const.txt)
```

**Example:**
```c
jobchange Job_Swordman;
jobchange Job_Knight, 1;   // High Knight
jobchange Job_Knight2;      // Peco Knight
```

---

### eaclass
**Syntax:** `eaclass({<job id>{,<char id>}})`

Convert job to EAJ class constant (bitmask).

---

### roclass
**Syntax:** `roclass(<class>{,<sex>})`

Convert EAJ class to job ID.

---

### jobname
**Syntax:** `jobname(<job id>)`

Get job name string.

**Example:**
```c
mes "You are a " + jobname(Class) + "!";
```

---

### jobcanentermap
**Syntax:** `jobcanentermap("<map>"{,<job id>{,<upper>{,<char id>}}})`

Check if job can enter map.

---

<!-- RAG_CHUNK: skill_commands_001 -->
## Skill Commands

### skill
**Syntax:** `skill <skill id>,<level>{,<flag>{,<char id>}};`

Give skill to player.

**Flags:**
- 0 = Permanent, saves level
- 1 = Temporary, saved, overwrite
- 2 = Temporary, not saved
- 4 = Permanent, add level

**Example:**
```c
skill SM_BASH, 10, 0;       // Permanent Bash Lv10
skill MG_FIREBOLT, 10, 2;   // Temporary Fire Bolt
```

---

### getskilllv
**Syntax:** `getskilllv(<skill id>{,<char id>})`

Get player's skill level.

**Example:**
```c
if (getskilllv(SM_BASH) >= 5)
    mes "You know Bash Lv5+!";
```

---

### getskilllist
**Syntax:** `getskilllist({<char id>});`

Populate skill arrays.

**Arrays:**
```c
@skilllist_id[]
@skilllist_lv[]
@skilllist_flag[]
@skilllist_count
```

---

### skillpointcount
**Syntax:** `skillpointcount({<char id>})`

Count total skill points used.

---

### plagiarizeskill
**Syntax:** `plagiarizeskill <skill id>,<level>{,<char id>};`

Set Plagiarism/Reproduce skill.

---

### plagiarizeskillreset
**Syntax:** `plagiarizeskillreset {<char id>};`

Clear plagiarized skills.

---

<!-- RAG_CHUNK: skill_effects_001 -->
## Skill Effects

### skilleffect
**Syntax:** `skilleffect <skill id>,<level>;`

Show skill effect on attached player.

**Example:**
```c
skilleffect AL_HEAL, 10;  // Show Heal effect
```

---

### npcskilleffect
**Syntax:** `npcskilleffect <skill id>,<level>,<x>,<y>;`

Show skill effect at coordinates.

---

### npcskill
**Syntax:** `npcskill <skill id>,<level>,<stat>,<npc level>;`

Make NPC cast skill on attached player.

**Example:**
```c
npcskill AL_HEAL, 10, 99, 60;  // NPC casts Heal Lv10
```

---

### itemskill
**Syntax:** `itemskill <skill id>,<level>{,<flag>{,<char id>}};`

Make player use skill (for item scripts).

**Flags:**
- 0 = Target select
- 1 = No target, self
- 2 = Immediate use

---

### unitskilluseid / unitskillusepos
**Syntax:** `unitskilluseid <gid>,<skill id>,<level>{,<target id>{,<cast time>}};`
**Syntax:** `unitskillusepos <gid>,<skill id>,<level>,<x>,<y>{,<cast time>};`

Make unit cast skill.

---

<!-- RAG_CHUNK: status_effect_commands_001 -->
## Status Effects

### sc_start
**Syntax:** `sc_start <type>,<duration>,<val1>{,<val2>,<val3>,<val4>,<target>{,<flag>{,<char id>}}};`

Apply status effect.

**Parameters:**
- `duration` - Milliseconds (1000 = 1 second)
- `val1-4` - Effect-specific values
- `target` - GID or SELF
- `flag` - SCFLAG_* values

**Common Status Effects:**
```c
SC_INCREASEAGI     // AGI UP
SC_BLESSING        // Blessing
SC_KYRIE           // Kyrie Eleison
SC_CONCENTRATION   // Concentration Potion
SC_ASPDPOTION0     // Awakening Potion
SC_ASPDPOTION1     // Concentration Potion
SC_ASPDPOTION2     // Awakening Potion
SC_ASPDPOTION3     // Berserk Potion
SC_POISON          // Poison
SC_STUN            // Stun
SC_FREEZE          // Freeze
SC_STONE           // Stone Curse
SC_SLEEP           // Sleep
SC_SILENCE         // Silence
SC_BLIND           // Blind
SC_CURSE           // Curse
SC_CONFUSION       // Confusion
SC_BLEEDING        // Bleeding
```

**Examples:**
```c
// Blessing for 5 minutes at level 10
sc_start SC_BLESSING, 300000, 10;

// AGI UP for 3 minutes at level 10
sc_start SC_INCREASEAGI, 180000, 10;

// Stun for 5 seconds
sc_start SC_STUN, 5000, 0;

// Aspd potion effect (Awakening) for 30 minutes
sc_start SC_ASPDPOTION2, 1800000, 0;
```

---

### sc_start2 / sc_start4
**Syntax:** `sc_start2 <type>,<duration>,<val1>,<val2>{,<target>{,<flag>{,<char id>}}};`
**Syntax:** `sc_start4 <type>,<duration>,<val1>,<val2>,<val3>,<val4>{,<target>{,<flag>{,<char id>}}};`

Apply status with additional values.

---

### sc_end
**Syntax:** `sc_end <type>{,<char id>};`

Remove status effect.

**Special Values:**
- `SC_ALL` - Remove all status effects

**Example:**
```c
sc_end SC_POISON;     // Cure poison
sc_end SC_ALL;        // Remove all effects
```

---

### sc_end_class
**Syntax:** `sc_end_class {<char id>};`

Remove all status from all skill classes.

---

### getstatus
**Syntax:** `getstatus(<type>{,<info>{,<char id>}})`

Check status effect.

**Info Types:**
- 0 = Is active? (1/0)
- 1 = val1
- 2 = val2
- 3 = val3
- 4 = val4
- 5 = Remaining time (ms)

**Example:**
```c
if (getstatus(SC_POISON))
    mes "You are poisoned!";

.@time = getstatus(SC_BLESSING, 5) / 1000;
mes "Blessing: " + .@time + " seconds left.";
```

---

### getscrate
**Syntax:** `getscrate(<type>,<base rate>{,<target>{,<char id>}})`

Calculate status chance after resistances.

---

<!-- RAG_CHUNK: appearance_001 -->
## Appearance

### changelook
**Syntax:** `changelook <type>,<value>{,<char id>};`

Change player appearance temporarily.

**Types:**
| Constant | Value | Description |
|----------|-------|-------------|
| LOOK_BASE | 0 | Base sprite |
| LOOK_HAIR | 1 | Hair style |
| LOOK_WEAPON | 2 | Weapon sprite |
| LOOK_HEAD_BOTTOM | 3 | Lower headgear |
| LOOK_HEAD_TOP | 4 | Upper headgear |
| LOOK_HEAD_MID | 5 | Middle headgear |
| LOOK_HAIR_COLOR | 6 | Hair color |
| LOOK_CLOTHES_COLOR | 7 | Clothes color |
| LOOK_SHIELD | 8 | Shield sprite |
| LOOK_SHOES | 9 | Shoes |
| LOOK_BODY2 | 10 | Body style |
| LOOK_ROBE | 11 | Robe/Costume |

**Example:**
```c
changelook LOOK_HAIR_COLOR, 1;  // Change hair to red
changelook LOOK_HAIR, 5;        // Change hairstyle
```

---

### getlook
**Syntax:** `getlook(<type>{,<char id>})`

Get current appearance value.

---

### setlook
**Syntax:** `setlook <type>,<value>{,<char id>};`

Permanently change appearance.

---

### changebase
**Syntax:** `changebase <job id>{,<char id>};`

Change player's base sprite.

---

<!-- RAG_CHUNK: option_commands_001 -->
## Options

### setoption
**Syntax:** `setoption <option>{,<flag>{,<char id>}};`

Set player option flags.

**Flag:** 0=toggle, 1=set, 2=remove

**Options:**
```c
Option_Sight        // Sight skill
Option_Hide         // Hide status
Option_Cloak        // Cloak status
Option_Falcon       // Falcon
Option_Riding       // Peco riding
Option_Invisible    // Perfect hide
Option_Wedding      // Wedding sprite
Option_Dragon1-5    // Dragon riding
Option_Wug          // Warg
Option_Wugrider     // Riding warg
Option_Madogear     // Madogear
```

**Example:**
```c
setoption Option_Riding, 1;  // Mount Peco
setoption Option_Riding, 2;  // Dismount
```

---

### checkoption
**Syntax:** `checkoption(<option>{,<char id>})`

Check if option is active.

---

### checkoption1 / checkoption2
Check opt1/opt2 (body state/effects).

---

### setfalcon / setcart / setriding / setdragon / setmadogear
**Syntax:** `setfalcon({<flag>{,<char id>}});`

Toggle specific options.

**Example:**
```c
setcart 1;      // Give pushcart
setfalcon 1;    // Give falcon
setdragon 1;    // Mount dragon (Rune Knight)
setmadogear 1;  // Mount Madogear (Mechanic)
```

---

### checkfalcon / checkcart / checkriding / checkdragon / checkmadogear / checkwug
Check if player has option.

---

<!-- RAG_CHUNK: disguise_001 -->
## Disguise

### disguise
**Syntax:** `disguise <monster id>{,<char id>};`

Transform player into monster.

---

### undisguise
**Syntax:** `undisguise({<char id>});`

Remove disguise.

---

### montransform
**Syntax:** `montransform <monster id>,<duration>{,<type>{,<val1>,<val2>{,<char id>}}};`

Transform with monster buff.

---

<!-- RAG_CHUNK: marriage_001 -->
## Marriage

### marriage
**Syntax:** `marriage("<partner name>")`

Marry two players. Returns 1 on success.

---

### wedding
**Syntax:** `wedding;`

Trigger wedding effect.

---

### divorce
**Syntax:** `divorce({<char id>})`

Divorce players.

---

### getpartnerid
**Syntax:** `getpartnerid({<char id>})`

Get spouse's character ID.

---

### ispartneron
**Syntax:** `ispartneron({<char id>})`

Check if partner is online.

---

<!-- RAG_CHUNK: adopt_001 -->
## Adoption

### adopt
**Syntax:** `adopt("<parent1>","<parent2>","<child>")`

Adopt character as baby.

---

### getchildid / getfatherid / getmotherid
Get family member character IDs.

---

<!-- RAG_CHUNK: party_commands_001 -->
## Party Info

### getpartyname
**Syntax:** `getpartyname(<party id>)`

Get party name.

---

### getpartyleader
**Syntax:** `getpartyleader(<party id>{,<type>})`

Get party leader info.

| Type | Returns |
|------|---------|
| 1 | Character ID |
| 2 | Account ID |
| 3 | Name |
| 4 | Map name |

---

### getpartymember
**Syntax:** `getpartymember(<party id>{,<type>{,<array>}});`

Get party member info.

**Type 0:** Sets `$@partymembername$[]` and `$@partymembercount`
**Type 1:** Sets `$@partymembercid[]`
**Type 2:** Sets `$@partymemberaid[]`

---

### is_party_leader
**Syntax:** `is_party_leader({<party id>{,<char id>}})`

Check if player is party leader.

---

#rathena #script #player #warp #heal #job #skill #status #appearance #party #marriage
