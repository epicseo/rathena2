# Instance Event Handler Issue - OnPCLogoutEvent Duplicates

## ❌ Problem

**Issue**: OnPCLogoutEvent (and other OnPC* events) inside instance NPCs register **globally** for every instance copy, causing duplicate warnings/triggers.

**Why**: OnPC* events are **global server events**, not instance-specific. When an instance is created, the NPC is duplicated, but the event label is registered globally again.

**Symptoms**:
- Multiple "duplicate event" warnings in console
- Event triggers multiple times (once per instance copy)
- Performance degradation with many instances

---

## ✅ Solutions

### **Solution 1: Use Single Global Event Handler (Recommended)**

Create ONE global NPC that handles the event, then checks if player is in an instance.

```c
// ❌ BAD - Inside instance NPC (registers multiple times)
1@tower,50,50,0	script	Instance Controller	-1,{
OnInstanceInit:
	// Instance setup
	end;

OnPCLogoutEvent:  // ❌ This registers globally for EACH instance!
	// Handle logout
	end;
}

// ✅ GOOD - Separate global NPC
-	script	Global_Logout_Handler	-1,{
OnPCLogoutEvent:
	// Check if player is in an instance
	.@map$ = strcharinfo(3);

	// Check if map is an instance map
	if (preg_match("^[0-9]+@", .@map$)) {
		// Player is in instance, handle logout
		.@instance_id = instance_id(IM_PARTY);
		if (.@instance_id >= 0) {
			// Save instance progress or cleanup
			setd("$InstanceProgress_" + getcharid(0), getinstancevar('progress, .@instance_id));
		}
	}
	end;
}
```

---

### **Solution 2: Use Map-Specific Check**

Handle the event globally, but filter by specific instance map.

```c
-	script	Instance_Logout_Handler	-1,{
OnPCLogoutEvent:
	// Only handle if player is on specific instance map
	if (strcharinfo(3) == instance_mapname("1@tower")) {
		// Player is in Endless Tower instance
		.@instance_id = instance_id(IM_PARTY);

		// Save progress
		.@floor = getinstancevar('current_floor, .@instance_id);
		#tower_saved_floor = .@floor;

		dispbottom "Progress saved: Floor " + .@floor;
	}
	end;
}
```

---

### **Solution 3: Use getinstancevar() from Global Handler**

Access instance variables from the global event handler.

```c
-	script	Multi_Instance_Handler	-1,{
OnPCLogoutEvent:
	.@char_id = getcharid(0);
	.@map$ = strcharinfo(3);

	// Check various instance types
	if (preg_match("^[0-9]+@tower$", .@map$)) {
		// Endless Tower
		.@instance_id = instance_id(IM_PARTY);
		if (.@instance_id >= 0) {
			setd("#ET_Floor_" + .@char_id, getinstancevar('floor, .@instance_id));
			setd("#ET_Time_" + .@char_id, getinstancevar('start_time, .@instance_id));
		}
	}
	else if (preg_match("^[0-9]+@nyd$", .@map$)) {
		// Nidhoggr's Nest
		.@instance_id = instance_id(IM_PARTY);
		if (.@instance_id >= 0) {
			setd("#Nyd_Progress_" + .@char_id, getinstancevar('progress, .@instance_id));
		}
	}
	// Add more instances as needed
	end;
}
```

---

### **Solution 4: Conditional Event Registration**

Register the event only for the first instance (not recommended, but possible).

```c
1@tower,50,50,0	script	Instance Controller	-1,{
OnInstanceInit:
	// Only register event if not already registered
	if ($@logout_handler_registered == 0) {
		$@logout_handler_registered = 1;
		// Event will only trigger once globally
	}
	end;

OnPCLogoutEvent:
	// This still triggers globally, but flag prevents re-registration warnings
	if (strcharinfo(3) == instance_mapname("1@tower")) {
		// Handle logout
	}
	end;
}
```

---

## 🎯 Best Practice Pattern

**Recommended structure for instance + global events:**

```c
//===============================================
// Instance NPC (NO global events here!)
//===============================================
1@mydungeon,50,50,0	script	Instance_Controller	-1,{
OnInstanceInit:
	// Instance initialization
	'start_time = gettimetick(2);
	'progress = 0;
	'party_id = getcharid(1);
	end;

OnInstanceDestroy:
	// Cleanup before destruction
	stopnpctimer;
	end;

// Instance-specific labels only
OnBossDead:
	'progress = 100;
	instance_announce(0, "Boss defeated!", bc_map);
	end;
}

//===============================================
// Global Event Handler (separate NPC)
//===============================================
-	script	Instance_Event_Handler	-1,{
OnPCLogoutEvent:
	.@map$ = strcharinfo(3);

	// Check if in instance
	if (preg_match("^[0-9]+@mydungeon$", .@map$)) {
		.@instance_id = instance_id(IM_PARTY);

		if (.@instance_id >= 0) {
			// Save progress
			.@progress = getinstancevar('progress, .@instance_id);
			.@time = getinstancevar('start_time, .@instance_id);

			#mydungeon_progress = .@progress;
			#mydungeon_time = .@time;

			dispbottom "Instance progress saved.";
		}
	}
	end;

OnPCLoginEvent:
	// Restore progress on login
	if (#mydungeon_progress > 0) {
		dispbottom "You have saved progress in My Dungeon.";
		dispbottom "Progress: " + #mydungeon_progress + "%";
	}
	end;
}
```

---

## ⚠️ Events That Trigger Globally (NOT Instance-Specific)

These events are **GLOBAL** and will register for every instance copy:

- `OnPCLoginEvent` - Player login
- `OnPCLogoutEvent` - Player logout
- `OnPCBaseLvUpEvent` - Base level up
- `OnPCJobLvUpEvent` - Job level up
- `OnPCDieEvent` - Player death
- `OnPCKillEvent` - Player kills player
- `OnNPCKillEvent` - Player kills monster
- `OnClock****` - Time events (OnClock0000, etc.)
- `OnTimer****` - Global timers
- `OnInit` - Server start
- `OnInterIfInit` - Inter-server connection
- `OnAgitStart` / `OnAgitEnd` - WoE events

**Rule**: Never put these in instance NPCs. Always use separate global handlers.

---

## ✅ Events Safe for Instance NPCs

These are **instance-specific** and safe to use:

- `OnInstanceInit` - Instance creation
- `OnInstanceDestroy` - Instance destruction
- `OnTouch` - Player touches NPC
- `OnTouch_` - Single trigger version
- `OnTouchNPC` - Monster touches NPC
- Custom labels (OnBossDead, OnWaveComplete, etc.)
- `OnTimer****` called via `initnpctimer` (instance-scoped)

---

## 🔍 Debugging Tips

### Check for Duplicate Registrations

```bash
# In server console, look for:
[Warning]: npc_parse_script: duplicate event OnPCLogoutEvent in script '1@tower#101::Instance Controller'
```

### Test Event Triggers

```c
// Add debug messages
OnPCLogoutEvent:
	debugmes "OnPCLogoutEvent triggered for " + strcharinfo(0) + " on map " + strcharinfo(3);
	// If you see this multiple times per logout = duplicate registration
	end;
```

### Count Active Handlers

```c
// In a test NPC
prontera,150,150,4	script	Event Counter	123,{
	mes "Triggering logout test...";
	donpcevent "All::OnPCLogoutEvent";  // Triggers ALL registered handlers
	mes "Check console for duplicate messages.";
	close;
}
```

---

## 📊 Performance Impact

**Multiple instance copies with global events:**

| Instances | Event Handlers | Triggers per Logout | Performance |
|-----------|----------------|---------------------|-------------|
| 1 | 1 | 1x | ✅ Normal |
| 10 | 10 | 10x | ⚠️ Slow |
| 50 | 50 | 50x | ❌ Laggy |
| 100 | 100 | 100x | ❌ Server freeze |

**With proper global handler:**

| Instances | Event Handlers | Triggers per Logout | Performance |
|-----------|----------------|---------------------|-------------|
| 1-1000 | 1 | 1x | ✅ Normal |

---

## 🚀 Migration Guide

**If you already have instances with OnPCLogoutEvent:**

### Step 1: Create Global Handler
```c
-	script	Fix_Global_Events	-1,{
OnPCLogoutEvent:
	.@map$ = strcharinfo(3);

	// Add all your instance maps
	if (preg_match("^[0-9]+@", .@map$)) {
		.@instance_id = instance_id(IM_PARTY);

		if (.@instance_id >= 0) {
			// Generic progress save
			.@progress = getinstancevar('progress, .@instance_id);
			if (.@progress > 0) {
				setd("#Instance_" + .@map$ + "_Progress", .@progress);
			}
		}
	}
	end;
}
```

### Step 2: Remove from Instance NPCs
```c
// Delete these from your instance NPCs:
// OnPCLogoutEvent:
//     ...
// end;
```

### Step 3: Test
1. Create multiple instances
2. Check console for duplicate warnings (should be gone)
3. Test logout/login (progress should still save)

---

## 📚 Related Issues

- **Issue**: OnTimer labels in instances trigger for all copies
  **Fix**: Use `initnpctimer` within instance (creates instance-scoped timer)

- **Issue**: OnClock events trigger globally
  **Fix**: Use global handler with instance check

- **Issue**: Multiple OnInit labels
  **Fix**: This is normal - OnInit runs once per NPC copy

---

## ✅ Summary

**DO**:
- ✅ Use separate global NPC for OnPC* events
- ✅ Check if player is in instance using `strcharinfo(3)` or `instance_id()`
- ✅ Use `getinstancevar()` to access instance data from global handler
- ✅ Use instance-specific labels (OnInstanceInit, OnInstanceDestroy, custom labels)

**DON'T**:
- ❌ Put OnPC* events inside instance NPCs
- ❌ Assume OnPC* events are instance-specific
- ❌ Ignore duplicate event warnings
- ❌ Use global timers inside instances (use initnpctimer instead)

---

**This is a CRITICAL gap in the current KB!** Adding this to KB_REF_InstanceSystem.md...
