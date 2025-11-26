# rAthena KB v6 - Server Configuration Reference

**Version:** 6.0 Complete
**Generated:** 2025-11-26
**Source:** conf/battle/*.conf
**Total Settings:** 566

---

## Quick Navigation

- [Battle Settings](#battle-settings) - Core combat mechanics
- [Skill Settings](#skill-settings) - Skill behavior
- [Player Settings](#player-settings) - Player mechanics
- [Monster Settings](#monster-settings) - Monster behavior
- [Drop Settings](#drop-settings) - Item drop rates
- [Experience Settings](#experience-settings) - EXP rates
- [Party Settings](#party-settings) - Party mechanics
- [Guild Settings](#guild-settings) - Guild mechanics
- [Feature Toggles](#feature-toggles) - Enable/disable features

---

## Configuration File Reference

### Battle

<!-- RAG_CHUNK: conf_battle -->

**File:** `conf/battle/battle.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `enable_baseatk` | 0x9 | assume unit types (1: Pc, 2: Mob, 4: Pet, 8: Homun, 16: Merc... |
| `enable_baseatk_renewal` | 0x29F |  |
| `enable_perfect_flee` | 1 | Who can have perfect flee? (Note 3) |
| `enable_critical` | 17 | Who can have critical attacks? (Note 3) (Note that there are... |
| `mob_critical_rate` | 100 | Critical adjustment rate for non-players (Note 2) |
| `critical_rate` | 100 |  |
| `attack_walk_delay` | 0 | this setting is mainly a safety mechanism against client edi... |
| `damage_walk_delay` | 0 | The walk delay only affects the time a monster reacts to the... |
| `pc_damage_walk_delay_rate` | 20 | Move-delay adjustment after being hit. (Note 2) The 'can't w... |
| `damage_walk_delay_rate` | 100 |  |
| `multihit_delay` | 200 | This delay is also added to the time a monster waits until i... |
| `player_damage_delay_rate` | 100 | Damaged delay rate for players (Note 2) This affects the dam... |
| `infinite_endure` | 0 | The unit types defined here cannot be stopped by damage. Ple... |
| `undead_detect_type` | 0 | 0 = element undead 1 = race undead 2 = both (either one work... |
| `attribute_recover` | no | Does HP recover if hit by an attribute that's same as your o... |
| `min_hitrate` | 5 | What is the minimum and maximum hitrate of normal attacks? |
| `max_hitrate` | 100 |  |
| `agi_penalty_type` | 1 | 0 = no penalty is applied 1 = agi_penalty_num is reduced fro... |
| `agi_penalty_target` | 1 | When agi penalty is enabled, to whom it should apply to? (No... |
| `agi_penalty_count` | 3 | Amount of enemies required to be targetting player before FL... |
| `agi_penalty_num` | 10 | Amount of FLEE penalized per each attacking monster more tha... |
| `vit_penalty_type` | 1 | 0 = no penalty is applied 1 = vit_penalty_num is reduced fro... |
| `vit_penalty_target` | 1 | When vit penalty is enabled, to whom it should apply to? (No... |
| `vit_penalty_count` | 3 | Amount of enemies required to be targetting player before de... |
| `vit_penalty_num` | 5 | Amount of VIT defense penalized per each attacking monster m... |
| `weapon_defense_type` | 0 | With 0, disabled (use normal def% reduction with further def... |
| `magic_defense_type` | 0 | MDEF‚ same as above. (MDEF * value) |
| `attack_direction_change` | 0 | knockback direction won't change, so e.g. if you walk north ... |
| `attack_attr_none` | 14 | (100% versus on all defense-elements) (Note 3) NOTE: This is... |
| `equip_natural_break_rate` | 0 | Rate at which equipment can break (base rate before it's mod... |
| `equip_self_break_rate` | 100 | This rate affects penalty breaking rate of skills such as po... |
| `equip_skill_break_rate` | 100 | Overall rate at which you can break target's equipment. (Not... |
| `delay_battle_damage` | yes | Should damage have a delay before it is applied? (Note 1) So... |
| `synchronize_damage` | no | Many skills show their damage immediately, so setting "delay... |
| `arrow_decrement` | 1 | 2 = Yes even for skills that do not specify arrow consumptio... |
| `ammo_unequip` | yes | Should ammo be unequipped when unequipping a weapon? Officia... |
| `ammo_check_weapon` | yes | Should a suitable weapon be equipped when equipping ammo? Of... |
| `autospell_check_range` | no | Official behavior is "no", setting this to "yes" will make s... |
| `knockback_left` | yes | If both the attacker and the target are on the same tile, sh... |
| `warg_can_falcon` | no | Can players use Falcons and Wargs at the same time? (Note 1)... |
| `snap_dodge` | no | Should the target be able of dodging damage by snapping away... |
| `break_mob_equip` | no | This will effectively apply the strip equip effect to the no... |

---

### Skill

<!-- RAG_CHUNK: conf_skill -->

**File:** `conf/battle/skill.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `casting_rate` | 100 | assume unit types (1: Pc, 2: Mob, 4: Pet, 8: Homun, 16: Merc... |
| `delay_rate` | 100 | Delay time after casting (Note 2) |
| `delay_dependon_dex` | no | Does the delay time depend on the caster's DEX and/or AGI? (... |
| `delay_dependon_agi` | no |  |
| `min_skill_delay_limit` | 100 | Minimum allowed delay for ANY skills after castbegin (in mil... |
| `amotion_min_skill_delay` | no | than attack motion using these tricks. Set this to "yes" if ... |
| `default_walk_delay` | 300 | NOTE: Do not set this too low, if a character starts moving ... |
| `no_skill_delay` | 2 | database, but follow their own 'reuse' skill delay which is ... |
| `castrate_dex_scale` | 150 | At what dex does the cast time become zero (instacast)? |
| `vcast_stat_scale` | 530 | How much (dex*2+int) does variable cast turns zero? |
| `skill_amotion_leniency` | 0 | NOTE: Setting this will break chaining of skills with cast t... |
| `skill_delay_attack_enable` | yes | Will normal attacks be able to ignore the delay after skills... |
| `skill_add_range` | 0 | Range added to skills after their cast time finishes. Decide... |
| `skill_out_range_consume` | no | If the target moves out of range while casting, do we take t... |
| `skillrange_by_distance` | 14 | If set, when the distance between caster and target is great... |
| `skillrange_from_weapon` | 0 | Should the equipped weapon's range override the skill's rang... |
| `skill_caster_check` | yes | Should a check on the caster's status be performed in all sk... |
| `clear_skills_on_death` | 0 | Should ground placed skills be removed as soon as the caster... |
| `clear_skills_on_warp` | 15 | Should ground placed skills be removed when the caster chang... |
| `defunit_not_enemy` | no | Setting this to YES will override the target mode of ground-... |
| `skill_min_damage` | 0 | any damage from them. Examples: Sonic Blow, Lord of Vermilli... |
| `combo_delay_rate` | 100 | The delay rate of monk's combo (Note 2) |
| `auto_counter_type` | 15 | Use alternate auto Counter Attack Skill Type? (Note 3) For t... |
| `skill_reiteration` | 0 | Can ground skills be placed on top of each other? (Note 3) B... |
| `skill_nofootset` | 1 | Can ground skills NOT be placed underneath/near players/mons... |
| `gvg_traps_target_all` | 1 | Should traps (hunter traps + quagmire) change their target t... |
| `skill_wall_check` | yes | Whether placed down skills will check walls (Note 1) (ex. St... |
| `player_cloak_check_type` | 1 | 1 = Check for walls 2 = Cloaking is not cancelled when attac... |
| `monster_cloak_check_type` | 4 |  |
| `land_skill_limit` | 9 | Can't place unlimited land skills at the same time (Note 3) |
| `display_skill_fail` | 2 | 2 - Disable skill-failed messages due to can-act delays. 4 -... |
| `chat_warpportal` | no | Can a player in chat room (in-game), be warped by a warp por... |
| `sense_type` | 1 | 1: Base defense [RE default] 2: Vit/Int defense 3: Both (the... |
| `finger_offensive_type` | 0 | Which finger offensive style will be used? 0 = Aegis style (... |
| `gx_allhit` | no | Set this to yes if you want all waves to deal damage to all ... |
| `gx_disptype` | 1 | Grandcross display type (Default 1) 0: Yellow character 1: W... |
| `devotion_level_difference` | 10 | Max Level Difference for Devotion |
| `devotion_rdamage` | 0 | Default is 0 (official). If 'devotion_rdamage' is > 0 (chanc... |
| `devotion_rdamage_skill_only` | yes | Officially, reflecting shield (SC_REFLECTDAMAGE) reflects ph... |
| `devotion_standup_fix` | yes | You can read more about it on https://github.com/rathena/rat... |
| `player_skill_partner_check` | yes | If no than you can use the ensemble skills alone. (Note 1) |
| `skill_removetrap_type` | 0 | Remove trap type 0 = Aegis system : Returns 1 'Trap' item 1 ... |
| `backstab_bow_penalty` | yes | Does using bow to do a backstab give a 50% damage penalty? (... |
| `skill_steal_max_tries` | 0 | How many times you could try to steal from a mob. Note: It h... |
| `skill_steal_random_options` | no | Should random options be applied to stolen items? (Note 1) O... |
| `max_heal` | 9999 | Level and Strength of "MVP heal". When someone casts a heal ... |
| `max_heal_lv` | 11 |  |
| `emergency_call` | 11 | 8: Skill is usable on GvG grounds 16: Disable skill from "no... |
| `guild_aura` | 31 | 4: Skill works outside of GvG grounds 8: Skill works on GvG ... |
| `mob_max_skilllvl` | 100 | Max Possible Level of Monster skills Note: If your MVPs are ... |

*...and 32 more settings in this file*

---

### Player

<!-- RAG_CHUNK: conf_player -->

**File:** `conf/battle/player.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `hp_rate` | 100 | assume unit types (1: Pc, 2: Mob, 4: Pet, 8: Homun, 16: Merc... |
| `sp_rate` | 100 | Players' maximum SP rate? (Default is 100) |
| `left_cardfix_to_right` | yes | Whether or not cards and attributes of the left hand are app... |
| `restart_hp_rate` | 0 | The amount of HP a player will respawn with, 0 is default. (... |
| `restart_sp_rate` | 0 | The amount of SP a player will respawn with, 0 is default. (... |
| `player_skillfree` | no | Can a normal player by-pass the skill tree? (Note 1) |
| `player_skillup_limit` | yes | When set to yes, forces skill points gained from 1st class t... |
| `quest_skill_learn` | no | Quest skills can be learned? (Note 1) Setting this to yes ca... |
| `quest_skill_reset` | no | When skills are reset, quest skills are reset as well? (Note... |
| `basic_skill_check` | yes | You must have basic skills to be able to sit, trade, form a ... |
| `player_invincible_time` | 3000 | If you attack a monster, it will attack you back regardless ... |
| `natural_healhp_interval` | 6000 | The time interval for HP to restore naturally. (in milliseco... |
| `natural_healsp_interval` | 8000 | The time interval for SP to restore naturally. (in milliseco... |
| `natural_heal_skill_interval` | 10000 | Automatic healing skill's time interval. (in milliseconds) |
| `major_overweight_rate` | 90 | open_box_weight_rate: 90 The maximum weight for a character ... |
| `max_aspd` | 190 | Maximum atk speed. (Default 190, Highest allowed 199) |
| `max_third_aspd` | 193 | Same as max_aspd, but for 3rd classes. (Default 193, Highest... |
| `max_extended_aspd` | 193 | Max ASPD for extended class (Kagerou/Oboro and Rebellion). (... |
| `max_summoner_aspd` | 193 | Max ASPD for Summoner Class (Doram). (Default 193, Highest a... |
| `max_walk_speed` | 300 | Maximum walk speed rate (200 would be capped to twice the no... |
| `max_hp_lv99` | 330000 | Lv 99:  330000 Lv150:  660000 Lv175: 1100000 |
| `max_hp_lv150` | 660000 |  |
| `max_hp` | 1100000 |  |
| `max_sp` | 1000000 | Maximum SP. (Default is 1000000) |
| `max_parameter` | 99 | 'max_baby_third_parameter' for baby 3rd classes only 'max_ex... |
| `max_trans_parameter` | 99 |  |
| `max_third_parameter` | 130 |  |
| `max_third_trans_parameter` | 130 |  |
| `max_baby_parameter` | 80 |  |
| `max_baby_third_parameter` | 117 |  |
| `max_extended_parameter` | 130 |  |
| `max_summoner_parameter` | 130 |  |
| `max_fourth_parameter` | 130 |  |
| `transcendent_status_points` | 52 | Status points bonus for transcendent class |
| `max_def` | 99 | NOTE: does not affects skills and status effects like Mental... |
| `over_def_bonus` | 0 | Def to Def2 conversion bonus. If the armor def/mdef exceeds ... |
| `max_cart_weight` | 8000 | Max weight carts can hold. |
| `prevent_logout` | 10000 | Prevent logout of players after being hit for how long (in m... |
| `prevent_logout_trigger` | 14 | 2 = Prevent logout after attacking 4 = Prevent logout after ... |
| `show_hp_sp_drain` | no | Display the drained hp/sp values from normal attacks? (Ie: H... |
| `show_hp_sp_gain` | yes | Display the gained hp/sp values from killing mobs? (Ie: Sky ... |
| `friend_auto_add` | yes | If set, when A accepts B as a friend, B will also be added t... |
| `invite_request_check` | yes | Are simultaneous trade/party/guild invite requests automatic... |
| `bone_drop` | 0 | 0 = Disabled 1 = Dropped only in PvP maps 2 = Dropped in all... |
| `character_size` | 0 | 2 = only Baby Classes on Peco have Medium Size 3 = both Norm... |
| `idle_no_autoloot` | 0 | Idle characters can receive autoloot? Set to the time in sec... |
| `min_npc_vendchat_distance` | 3 | Minimum distance a vending/chat room must be from a NPC in o... |
| `rental_mount_speed_boost` | 25 | How much should rental mounts increase a player's movement s... |
| `vip_storage_increase` | 300 | Give more storage slots above the MIN_STORAGE limit. Note: M... |
| `vip_base_exp_increase` | 50 | Base experience rate increase. Setting to 0 will disable. (N... |

*...and 32 more settings in this file*

---

### Monster

<!-- RAG_CHUNK: conf_monster -->

**File:** `conf/battle/monster.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `mvp_hp_rate` | 100 | assume unit types (1: Pc, 2: Mob, 4: Pet, 8: Homun, 16: Merc... |
| `monster_hp_rate` | 100 | The HP rate of normal monsters (that is monsters that are no... |
| `monster_ai` | 0 | 0x2000: When set, monsters will move right after they attack... |
| `monster_chase_refresh` | 32 | If you want monsters to update their target cell while chasi... |
| `mob_warp` | 0 | 2: Enable mob-warping when standing on Priest Warp Portals 4... |
| `mob_active_time` | 0 | Even after this time they will still walk randomly and use i... |
| `boss_active_time` | 0 |  |
| `view_range_rate` | 100 | Mobs and Pets view-range adjustment (range2 column in the mo... |
| `chase_range_rate` | 100 | Chase Range is the base minimum-chase that a mob gives befor... |
| `monster_eye_range_bonus` | 0 | Officially monsters don't have these skills learned, so thei... |
| `loot_range` | 12 | Range in which looters search for loot (max 32) Official: 12... |
| `assist_range` | 11 | Range in which assist mobs search for allies to assist (max ... |
| `monster_active_enable` | yes | Allow monsters to be aggresive and attack first? (Note 1) |
| `override_mob_names` | 0 | 0: No 1: always use the mob_db Name column (english mob name... |
| `monster_damage_delay_rate` | 100 | Monster damage delay rate (Note 2) This affects the damage d... |
| `monster_loot_type` | 0 | Looting monster actions. 0 = Monster will consume the item. ... |
| `monster_loot_search_type` | 1 | How does monster search floor item to loot? 0: Closest (old ... |
| `mob_skill_rate` | 100 | Chance of mob casting a skill (Note 2) Higher rates lead to ... |
| `mob_skill_delay` | 100 | After a mob has casted a skill, there is a delay before bein... |
| `mob_count_rate` | 100 | Rate of monsters on a map, 200 would be twice as many as nor... |
| `mob_spawn_delay` | 100 | Respawn rate of monsters on a map. 50 would make mobs respaw... |
| `plant_spawn_delay` | 100 |  |
| `boss_spawn_delay` | 100 |  |
| `mob_spawn_variance` | 1 | 1: Boss monsters (official) 2: Normal monsters 3: All monste... |
| `no_spawn_on_player` | 0 | 5 seconds. NOTE: This has no effect on mobs that always spaw... |
| `force_random_spawn` | no | Should spawn coordinates in the mob-spawn files be ignored? ... |
| `randomize_center_cell` | yes | different experience each server start. Set this to "no" if ... |
| `slaves_inherit_mode` | 4 | 2: Slaves are always passive. 3: Same as master's aggressive... |
| `slaves_inherit_speed` | 3 | 2: If the master can't walk (even motionless mobs have a spe... |
| `mob_slave_keep_target` | yes | Should MVP slaves retain their target when summoned back to ... |
| `slave_stick_with_master` | no | Should slaves teleport back to their master if they get too ... |
| `slave_active_with_master` | no | Should slaves always be active when their master is active? ... |
| `summons_trigger_autospells` | yes | Will summoned monsters (alchemists, or @summon'ed monsters) ... |
| `retaliate_to_master` | yes | When a mob is attacked by another monster, will the mob reta... |
| `mob_changetarget_byskill` | no | eg: Mob attacks player B, and player A casts a skill C. If s... |
| `monster_class_change_full_recover` | yes | If monster's class is changed will it fully recover HP? (Not... |
| `show_mob_info` | 0 | 1: Display mob HP (Hp/MaxHp format) 2: Display mob HP (Perce... |
| `zeny_from_mobs` | no | Zeny from mobs |
| `mobs_level_up` | no | Monsters level up (monster will level up each time a player ... |
| `mobs_level_up_exp_rate` | 1 |  |
| `dynamic_mobs` | yes | Dynamic Mobs Options Use dynamic mobs? (recommended for smal... |
| `mob_remove_damaged` | yes | Remove Mobs even if they are hurt |
| `mob_remove_delay` | 300000 | Delay before removing mobs from empty maps (default 5 min = ... |
| `mob_npc_event_type` | 1 | Type 1: On the player that killed the mob (if killed by a no... |
| `ksprotection` | 0 | Set to 0 to disable it. If this is activated and a player is... |
| `mvp_tomb_enabled` | yes | Whether or not to spawn the mvp tomb. See http://irowiki.org... |
| `mvp_tomb_delay` | 9000 | Delay before the MVP tomb is spawned. Default: 9 seconds |
| `mob_size_influence` | no | and stats. The rates will be doubled for large mobs, and hal... |
| `mob_icewall_walk_block` | 75 | icewall completely blocked on all maps that have boss monste... |
| `boss_icewall_walk_block` | 0 |  |

*...and 9 more settings in this file*

---

### Drops

<!-- RAG_CHUNK: conf_drops -->

**File:** `conf/battle/drops.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `item_auto_get` | no | Note 2: Value is in percents (100 means 100%) --------------... |
| `flooritem_lifetime` | 60000 | How long does it take for an item to disappear from the floo... |
| `first_attack_loot_bonus` | 30 | If you set this to 0, then loot priority will be solely calc... |
| `item_first_get_time` | 3000 | Grace time during which only the player who did the most dam... |
| `item_second_get_time` | 2000 | Grace time during which only the first and second player who... |
| `item_third_get_time` | 2000 | Grace time during which only the first, second and third pla... |
| `mvp_item_first_get_time` | 10000 | Grace time during which only the player who did the most dam... |
| `mvp_item_second_get_time` | 10000 | Grace time during which only the first and second player who... |
| `mvp_item_third_get_time` | 2000 | Grace time during which only the first, second and third pla... |
| `item_rate_common` | 100 | Item drop rates (Note 2) The rate the common items are dropp... |
| `item_rate_common_boss` | 100 |  |
| `item_rate_common_mvp` | 100 |  |
| `item_drop_common_min` | 1 |  |
| `item_drop_common_max` | 10000 |  |
| `item_rate_heal` | 100 | The rate healing items are dropped (items that restore HP or... |
| `item_rate_heal_boss` | 100 |  |
| `item_rate_heal_mvp` | 100 |  |
| `item_drop_heal_min` | 1 |  |
| `item_drop_heal_max` | 10000 |  |
| `item_rate_use` | 100 | The rate at which usable items (in the item tab) other then ... |
| `item_rate_use_boss` | 100 |  |
| `item_rate_use_mvp` | 100 |  |
| `item_drop_use_min` | 1 |  |
| `item_drop_use_max` | 10000 |  |
| `item_rate_equip` | 100 | The rate at which equipment is dropped. |
| `item_rate_equip_boss` | 100 |  |
| `item_rate_equip_mvp` | 100 |  |
| `item_drop_equip_min` | 1 |  |
| `item_drop_equip_max` | 10000 |  |
| `item_rate_card` | 100 | The rate at which cards are dropped |
| `item_rate_card_boss` | 100 |  |
| `item_rate_card_mvp` | 100 |  |
| `item_drop_card_min` | 1 |  |
| `item_drop_card_max` | 10000 |  |
| `item_rate_mvp` | 100 | The rate adjustment for the MVP items that the MVP gets dire... |
| `item_drop_mvp_min` | 1 |  |
| `item_drop_mvp_max` | 10000 |  |
| `item_drop_mvp_mode` | 0 |  |
| `item_rate_adddrop` | 100 | The rate adjustment for equip-granted item drops. |
| `item_drop_add_min` | 1 |  |
| `item_drop_add_max` | 10000 |  |
| `item_group_rate` | 100 | The rate adjustment for items inside of equip-granted item g... |
| `item_group_drop_min` | 1 |  |
| `item_group_drop_max` | 10000 |  |
| `item_rate_treasure` | 100 | Rate adjustment for Treasure Box drops (these override all o... |
| `item_drop_treasure_min` | 1 |  |
| `item_drop_treasure_max` | 10000 |  |
| `item_logarithmic_drops` | no | 10000 | 1.00 1.67  3.25  5.28  8.44 15.24 23.19 34.26 54.57 ... |
| `drop_rate0item` | no | Can the monster's drop rate become 0? (Note 1) Default: no (... |
| `drop_rateincrease` | no | On official servers it is possible to get 0.00% drop chance ... |

*...and 12 more settings in this file*

---

### Items

<!-- RAG_CHUNK: conf_items -->

**File:** `conf/battle/items.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `vending_max_value` | 1000000000 | assume unit types (1: Pc, 2: Mob, 4: Pet, 8: Homun, 16: Merc... |
| `vending_over_max` | yes | of the items exceeds the maximum zeny allowed. (Note 1) If s... |
| `vending_tax` | 500 | Tax to apply to all vending transactions (eg: 10000 = 100%, ... |
| `vending_tax_min` | 100000000 | Minimum total of purchase until taxes are applied. Officiall... |
| `buyer_name` | yes | Show the buyer's name when successfully vended an item |
| `weapon_produce_rate` | 100 | Forging success rate. (Note 2) |
| `potion_produce_rate` | 100 | Prepare Potion success rate. (Note 2) |
| `produce_item_name_input` | 0x03 | 0x08: Produced Holy Water/Ancilla 0x10: Produced Deadly Poti... |
| `dead_branch_active` | yes | Is a monster summoned via dead branch aggressive? (Note 1) |
| `random_monster_checklv` | no | Should summoned monsters check the player's base level? (dea... |
| `item_check` | 0x0 | 0x1: Inventory 0x2: Cart 0x4: Storage |
| `item_use_interval` | 100 | How much time must pass between item uses? Only affects the ... |
| `cashfood_use_interval` | 60000 | How much time must pass between cash food uses? Default: 600... |
| `gtb_sc_immunity` | 50 | Required level of bNoMagicDamage before Status Changes are b... |
| `autospell_stacking` | no | Enable autospell card effects to stack? NOTE: Different card... |
| `allow_consume_restricted_item` | no | Allow the consumption of usable items that are disabled by i... |
| `allow_equip_restricted_item` | yes | no = can't be equipped and will be unequipped when entering ... |
| `item_flooritem_check` | yes | Allow map_addflooritem to check if item is droppable? (Note ... |
| `default_bind_on_equip` | 4 | 2 - Guild 3 - Party 4 - Character |
| `allow_bound_sell` | 0x0 | 0x4 = Bound items are able to be sold to Shops, because most... |
| `broadcast_hide_name` | 2 | obtained an item with special broadcast flag or refined an i... |
| `rental_transaction` | yes | Enable to sell rental item to NPC shop? (Note 1) |
| `rental_item_novalue` | no | Sell rental item for 0 to NPC shop regardless of the item va... |
| `min_shop_buy` | 1 | Minimum purchase price of items at a normal Shop Officially ... |
| `min_shop_sell` | 0 | Minimum sell price of items at a normal shop Officially item... |
| `cardfix_monster_physical` | yes | Officially "Asprika" (god item) reduces all monsters damage ... |
| `trade_count_stackable` | yes | Determines whether stackable items should be counted separat... |

---

### Misc

<!-- RAG_CHUNK: conf_misc -->

**File:** `conf/battle/misc.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `pk_mode` | 0 | Note: If pk_mode is set to 2 instead of 1 (yes), players wil... |
| `pk_mode_mes` | yes | Displays a message when the player enters a pk zone. Only du... |
| `manner_system` | 15 | 4: Disables commands usage 8: Disables item usage/picking/dr... |
| `pk_min_level` | 55 | For PK Server Mode. Change this to define the minimum level ... |
| `pk_level_range` | 0 | For PK Server Mode. It specifies the maximum level differenc... |
| `pk_short_attack_damage_rate` | 80 | For PK servers. Damage adjustment settings, these follow the... |
| `pk_long_attack_damage_rate` | 70 |  |
| `pk_weapon_attack_damage_rate` | 60 |  |
| `pk_magic_attack_damage_rate` | 60 |  |
| `pk_misc_attack_damage_rate` | 60 |  |
| `skill_log` | off | Display skill usage in console? (for debug only) (default: o... |
| `battle_log` | off | Display battle log? (for debug only) (default: off) (Note 1) |
| `etc_log` | off | Display other stuff? (for debug only) (default: off) (Note 1... |
| `warp_point_debug` | no | Do you want to debug warp points? If set to yes, warp points... |
| `night_at_start` | no | Choose if server begin with night (yes) or day (no) |
| `day_duration` | 0 | Define duration in msec of the day (default: 7200000 = 2 hou... |
| `night_duration` | 0 | Define duration in msec of the night (default: 1800000 = 30 ... |
| `duel_allow_pvp` | no | Using duel on pvp-maps |
| `duel_allow_gvg` | no | Using duel on gvg-maps |
| `duel_allow_teleport` | no | Allow using teleport/warp when dueling |
| `duel_autoleave_when_die` | yes | Autoleave duel when die |
| `duel_time_interval` | 60 | Delay between using @duel in minutes |
| `duel_only_on_same_map` | no | Restrict duel usage to same map |
| `official_cell_stack_limit` | 1 | Custom - This variation will make every full cell to be cons... |
| `custom_cell_stack_limit` | 1 |  |
| `at_mapflag` | no | Allow autotrade only in maps with autotrade flag? Set this t... |
| `at_timeout` | 0 | Set this to the amount of minutes autotrade chars will be ki... |
| `at_monsterignore` | no | Makes player cannot be attacked when autotrade? (turns playe... |
| `at_logout_event` | yes | Should autotrade trigger OnPCLogout script events? (Note 1) |
| `auction_feeperhour` | 12000 | Auction system, fee per hour. Default is 12000 |
| `auction_maximumprice` | 500000000 | Auction maximum sell price |
| `searchstore_querydelay` | 10 | Minimum delay between each store search query in seconds. |
| `searchstore_maxresults` | 30 | Maximum amount of results a store search query may yield, be... |
| `cashshop_show_points` | no | Whether or not gaining and loosing of cash points is display... |
| `mail_show_status` | 0 | 0 = No 1 = Yes 2 = Yes, when there are unread mails |
| `mail_daily_count` | 100 | Amount of mails a user can send a day. Default: 100 0 = Unli... |
| `mail_zeny_fee` | 2 | NOTE: this rate is hardcoded in the client, you need to diff... |
| `mail_attachment_price` | 2500 | NOTE: this fee is hardcoded in the client, you need to diff ... |
| `mail_attachment_weight` | 2000 | NOTE: this limit is hardcoded in the client, you need to dif... |
| `mon_trans_disable_in_gvg` | no | Is monster transformation disabled during Guild Wars? If set... |
| `discount_item_point_shop` | 0 | 1 = Item shops 2 = Point shops 3 = Item & point shops |
| `disp_servervip_msg` | no | Don't display message "login-serv has been asked to %s the p... |
| `mail_delay` | 1000 | Delay to allow user resend new mail (default & minimum is 10... |
| `hide_fav_sell` | no | Hides items from the player's favorite tab from being sold t... |
| `map_edge_size` | 15 | On some maps like in Pyramids this causes there to be very f... |
| `item_stacking` | yes | If you set this to "no", when you drop an item, it will only... |

---

### Client

<!-- RAG_CHUNK: conf_client -->

**File:** `conf/battle/client.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `min_chat_delay` | 0 | ------------------------------------------------------------... |
| `min_hair_style` | 0 | Valid range of dyes and styles on the client. |
| `max_hair_style` | 42 |  |
| `min_hair_color` | 0 |  |
| `max_hair_color` | 8 |  |
| `min_cloth_color` | 0 |  |
| `max_cloth_color` | 7 |  |
| `min_body_style` | 0 |  |
| `max_body_style` | 1 |  |
| `hide_woe_damage` | no | When set to yes, the damage field in packets sent from woe m... |
| `pet_hair_style` | 100 | older sakexes: 20 sakexe 0614: 24 sakexe 0628 (and later): 1... |
| `area_size` | 14 | Visible area size (how many squares away from a player they ... |
| `max_walk_path` | 17 | Maximum walk path (how many cells a player can walk going to... |
| `max_lv` | 99 | NOTE: You also need to adjust the client if you want this to... |
| `aura_lv` | 99 | Example: If max_lv is 99 and aura_lv is 150, characters with... |
| `client_limit_unit_lv` | 0 | Note: If an unit type, which normally does not show an aura,... |
| `wedding_modifydisplay` | no | Will tuxedo and wedding dresses be shown when worn? (Note 1) |
| `save_clothcolor` | yes | Save Clothes color. (This will degrade performance) (Note 1) |
| `save_body_style` | yes | Save body styles. (Note 1) |
| `wedding_ignorepalette` | no | Note: Both save_clothcolor and wedding_modifydisplay have to... |
| `xmas_ignorepalette` | no | Do not display cloth colors for the Xmas costume? Set this t... |
| `summer_ignorepalette` | no | Do not display cloth colors for the Summer costume? Set this... |
| `hanbok_ignorepalette` | no | Do not display cloth colors for the Hanbok costume? Set this... |
| `oktoberfest_ignorepalette` | no | Do not display cloth colors for the Oktoberfest costume? Set... |
| `motd_type` | 0 | Set this to 1 if your clients have langtype problems and can... |
| `display_version` | yes | Show rAthena version to users when the login? |
| `display_hallucination` | yes | When affected with the "Hallucination" status effect, send t... |
| `display_status_timers` | yes | Set this to 1 if your client supports status change timers a... |
| `client_reshuffle_dice` | yes | Randomizes the dice emoticon server-side, to prevent clients... |
| `client_sort_storage` | no | Sorts the cart, guild storage, inventory and storage before ... |
| `update_enemy_position` | yes | NOTE: Set to 'no' will make client won't update enemy positi... |
| `spawn_direction` | no | When a player teleports, changes maps, or logs in, will they... |
| `mvp_exp_reward_message` | no | Show the MVP EXP reward message for clients 2013-12-23cRagex... |
| `ping_timer_inverval` | 30 | Send ping timer Interval in seconds for each timer invoke. |
| `ping_time` | 20 | Send packets timeout in seconds before ping packet can be se... |
| `show_skill_scale` | yes | Show skill scale for clients 2015-12-23 and newer? (Note 1) ... |
| `drop_connection_on_quit` | no | Should the connection be dropped on server side after a play... |
| `macro_detection_retry` | 3 | Macro Detector retries Number of times someone can fail the ... |
| `macro_detection_timeout` | 60000 | Macro Detector timeout Amount of time in milliseconds before... |
| `macro_detection_punishment` | 0 | 0 - Ban 1 - Jail Official: 0 |
| `macro_detection_punishment_time` | 0 | Macro Detector punishment duration Amount of time in minutes... |
| `macrochecker_delay` | 600000 | Macrochecker delay (per map) Set to 0 to disable |

---

### Exp

<!-- RAG_CHUNK: conf_exp -->

**File:** `conf/battle/exp.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `base_exp_rate` | 100 | See files db/exp.txt and db/exp2.txt to change them. -------... |
| `job_exp_rate` | 100 | Rate at which job exp. is given. (Note 2) |
| `multi_level_up` | no | Turn this on to allow a player to level up more than once fr... |
| `multi_level_up_base` | 0 | Allow multi level up until a certain level? This only trigge... |
| `multi_level_up_job` | 0 |  |
| `max_exp_gain_rate` | 0 | % of the current exp bar. (Every 10 = 1.0%) For example, set... |
| `exp_calc_type` | 0 | 0 = uses damage given / total damage as damage ratio 1 = use... |
| `exp_bonus_attacker` | 25 | Experience increase per attacker. That is, every additional ... |
| `exp_bonus_max_attacker` | 12 | Max number of attackers at which exp bonus is capped (eg: if... |
| `exp_bonus_nodamage_attacker` | no | Should casting skills that deal no damage still make you cou... |
| `mvp_exp_rate` | 100 | MVP bonus exp rate. (Note 2) |
| `quest_exp_rate` | 100 | Rate of base/job exp given by NPCs. (Note 2) |
| `heal_exp` | 0 | The rate of job exp. from using Heal skill (100 is the same ... |
| `resurrection_exp` | 0 | The rate of exp. that is gained by the process of resurrecti... |
| `shop_exp` | 0 | The rate of job exp. when using discount and overcharge on a... |
| `pvp_exp` | yes | PVP exp.  Do players get exp in PvP maps (Note: NOT exp from... |
| `death_penalty_type` | 1 | 0 = No penalty. 1 = Lose % of current level when killed. 2 =... |
| `death_penalty_base` | 100 | Base exp. penalty rate (Each 100 is 1% of their exp) |
| `death_penalty_job` | 100 | Job exp. penalty rate (Each 100 is 1% of their exp) |
| `zeny_penalty` | 0 | When a player dies (to another player), how much zeny should... |
| `death_penalty_maxlv` | 0 | 0: Never lose (default as in official). 1: Lose Base EXP. 2:... |
| `disp_experience` | no | Will display experience gained from killing a monster. (Note... |
| `disp_zeny` | no | Will display zeny earned (from mobs, trades, etc) (Note 1) |
| `use_statpoint_table` | yes | Use the contents of db/statpoint.txt when doing a stats rese... |
| `use_traitpoint_table` | yes | Use the contents of db/statpoint.yml when doing a stats rese... |
| `exp_cost_redemptio` | 1 | EXP cost for cast PR_REDEMPTIO (Note 2) |
| `exp_cost_redemptio_limit` | 5 | How many player needed to makes PR_REDEMPTIO's EXP penalty b... |

---

### Party

<!-- RAG_CHUNK: conf_party -->

**File:** `conf/battle/party.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `show_steal_in_same_party` | no | Note 2: Value is in percents (100 means 100%) --------------... |
| `party_update_interval` | 1000 | Interval before updating the party-member map mini-dots (mil... |
| `party_hp_mode` | 0 | Method used to update party-mate hp-bars: 0: Aegis - bar is ... |
| `show_party_share_picker` | yes | under the value "party_share_level". When 'Party Share' item... |
| `party_item_share_type` | 0 | 1: Item Share is disabled for non-mob drops (player/pet drop... |
| `idle_no_share` | no | a character idle. Characters in a chat/vending are always co... |
| `party_even_share_bonus` | 0 | Give additional experience bonus per party-member involved o... |
| `display_party_name` | yes | Display party name regardless if player is in a guild. Offic... |
| `block_account_in_same_party` | yes | Prevent multiple characters of the same account to join the ... |
| `change_party_leader_samemap` | yes | Prevent changing the party leader if the specified player is... |

---

### Guild

<!-- RAG_CHUNK: conf_guild -->

**File:** `conf/battle/guild.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `guild_emperium_check` | yes | Note 2: Value is in percents (100 means 100%) --------------... |
| `guild_exp_limit` | 50 | Maximum tax limit on a guild member. |
| `guild_max_castles` | 0 | Maximum castles one guild can own (0 = unlimited) |
| `guild_skill_relog_delay` | 300000 | Delay in milliseconds that are applied to guild skills. Offi... |
| `gvg_short_attack_damage_rate` | 80 | Melee damage adjustments (non skills) for WoE battles (Guild... |
| `gvg_long_attack_damage_rate` | 80 | Ranged damage adjustments (non skills) for WoE battles (Guil... |
| `gvg_weapon_attack_damage_rate` | 60 | Weapon skills damage adjustments for WoE battles (Guild Vs G... |
| `gvg_magic_attack_damage_rate` | 60 | Magic skills damage adjustments for WoE battles (Guild Vs Gu... |
| `gvg_misc_attack_damage_rate` | 60 | Misc skills damage adjustments for WoE battles (Guild Vs Gui... |
| `gvg_flee_penalty` | 20 | Flee penalty on gvg grounds. Official value is 20 (Note 2) N... |
| `require_glory_guild` | no | Can the 'Glory of Guild' skill be learnt in the Guild window... |
| `max_guild_alliance` | 3 | Limit Guild alliances. Value is 0 to 3. If you want to chang... |
| `guild_notice_changemap` | 2 | Upon teleporting (regardless of changing maps): 2 (official)... |
| `guild_maprespawn_clones` | no | Should maprespawnguildid kill clones too? Default: no |
| `guild_leaderchange_delay` | 1440 | How long (in minutes) should a guild have to wait between gu... |
| `guild_leaderchange_woe` | no | Is changing the guild leader allowed during WoE? Default: no |
| `guild_alliance_onlygm` | no | Only guild master can accept alliance? Default: no |

---

### Pet

<!-- RAG_CHUNK: conf_pet -->

**File:** `conf/battle/pet.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `pet_legacy_formula` | no | ( Base rate + ( player level - monster level ) * 30 + player... |
| `pet_catch_rate` | 100 | Rate for catching pets (Note 2) |
| `pet_distance_check` | 5 | The client automatically walks the player into range when tr... |
| `pet_hide_check` | yes | On official servers players are unable to catch monsters if ... |
| `pet_rename` | no | Can you name a pet more then once? (Note 1) |
| `pet_friendly_rate` | 100 | The rate a pet will get friendly by feeding it. (Note 2) |
| `pet_hungry_delay_rate` | 100 | The rate at which a pet will become hungry. (Note 2) |
| `pet_equip_required` | yes | Does the pet need its equipment before it does its skill? (N... |
| `pet_unequip_destroy` | yes | Should the pet equipment be destroyed if the owner doesn't h... |
| `pet_attack_support` | no | When the master attacks a monster, whether or not the pet wi... |
| `pet_damage_support` | no | When the master receives damage from the monster, whether or... |
| `pet_support_min_friendly` | 900 | Minimum intimacy necessary for a pet to support their master... |
| `pet_status_support` | no | Whether or not the pet's will use skills. (Note 1) Note: Off... |
| `pet_support_rate` | 100 | Rate at which a pet will support it's owner in battle. (Note... |
| `pet_attack_exp_to_master` | no | Does the pets owner receive exp from the pets damage? |
| `pet_attack_exp_rate` | 100 | The rate exp. is gained from the pet attacking monsters |
| `pet_lv_rate` | 0 | Pet leveling system. Use 0 to disable (default). When enable... |
| `pet_max_stats` | 99 | When pet leveling is enabled, what is the max stats for pets... |
| `pet_max_atk1` | 500 | When pet leveling is enabled, these are the imposed caps on ... |
| `pet_max_atk2` | 1000 |  |
| `pet_disable_in_gvg` | no | Are pets disabled during Guild Wars? If set to yes, pets are... |
| `pet_ignore_infinite_def` | yes | Will does petskillattack2 fixed damage ignore plant infnite ... |
| `pet_master_dead` | no | Whether or not the pet will continue to attack when the mast... |
| `pet_autofeed_always` | yes | Send auto-feed notice even if the client setting is OFF (Not... |
| `pet_walk_speed` | 1 | 1: Master's walk speed (official) 2: DEFAULT_WALK_SPEED valu... |

---

### Homunc

<!-- RAG_CHUNK: conf_homunc -->

**File:** `conf/battle/homunc.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `hom_setting` | 0x3D | 0x10: They display luk/3+1 instead of their actual critical ... |
| `homunculus_friendly_rate` | 100 | Default on official servers: yes for Pre-renewal, no for Ren... |
| `hom_rename` | no | Can you name a homunculus more then once? (Note 1) |
| `homunculus_evo_intimacy_need` | 91100 | Minimum intimacy to evo the homunculus |
| `homunculus_evo_intimacy_reset` | 1000 | Reset intimacy after evolution to: |
| `hvan_explosion_intimate` | 45000 | Intimacy needed to use Evolved Vanilmirth's Bio Explosion |
| `homunculus_show_growth` | yes | Show stat growth to the owner when an Homunculus levels up |
| `homunculus_autoloot` | no | Does autoloot work, when a monster is killed by homunculus o... |
| `homunculus_auto_vapor` | 80 | Should homunculi Vaporize when Master dies? (Note 2) A homun... |
| `homunculus_max_level` | 99 | Max level for regular Homunculus |
| `homunculus_S_max_level` | 250 | Max level for Homunculus S |
| `homunculus_S_growth_level` | 99 | This is the level at which homunculus S can use their growth... |
| `homunculus_autofeed_always` | yes | Send auto-feed notice even if OFF (Note 1) Official: yes |
| `hom_idle_no_share` | no | Their master will only receive items if 'homunculus_autoloot... |
| `idletime_hom_option` | 0x1F | Default: walk (0x1) + useskilltoid (0x2) + useskilltopos (0x... |
| `homunculus_exp_gain` | 10 | The rate at which homunculus gain experience from kills. (No... |
| `homunculus_starving_rate` | 10 | See 'homunculus_starving_delay' for the delay value. Set to ... |
| `homunculus_starving_delay` | 20000 | Homunculi normally lose hunger every 60 seconds but when the... |

---

### Gm

<!-- RAG_CHUNK: conf_gm -->

**File:** `conf/battle/gm.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `atcommand_symbol` | @ | - '/' (client commands symbol) atcommand_symbol represents @... |
| `charcommand_symbol` | # |  |
| `atcommand_spawn_quantity_limit` | 100 | The maximum quantity of monsters that can be summoned per GM... |
| `atcommand_slave_clone_limit` | 25 | Maximum number of slave-clones that can be have by using the... |
| `partial_name_scan` | yes | current map server. Some critical atcommands like jail, ban ... |
| `ban_hack_trade` | 5 | Ban people that try trade dupe. Duration of the ban, in minu... |
| `atcommand_mobinfo_type` | 1 | modifies @mobinfo to display the users' real drop rate as pe... |
| `atcommand_levelup_events` | no | Should atcommands trigger level up events for NPCs? (Note 1)... |
| `atcommand_disable_npc` | yes | This can be changed by script commands 'enable_command' and ... |

---

### Instance

<!-- RAG_CHUNK: conf_instance -->

**File:** `conf/battle/instance.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `instance_block_leave` | yes | ------------------------------------------------------------... |
| `instance_block_leaderchange` | yes | Block leader changes for parties or guilds if they have an a... |
| `instance_block_invite` | yes | Block inviting for parties or guilds if they have an active ... |
| `instance_block_expulsion` | yes | Block expulsion for parties or guilds if they have an active... |

---

### Battleground

<!-- RAG_CHUNK: conf_battleground -->

**File:** `conf/battle/battleground.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `bg_short_attack_damage_rate` | 80 | assume unit types (1: Pc, 2: Mob, 4: Pet, 8: Homun, 16: Merc... |
| `bg_long_attack_damage_rate` | 80 | Ranged damage adjustments (non skills) for Battleground maps... |
| `bg_weapon_attack_damage_rate` | 60 | Weapon skills damage adjustments for Battleground maps (Note... |
| `bg_magic_attack_damage_rate` | 60 | Magic skills damage adjustments for Battleground maps (Note ... |
| `bg_misc_attack_damage_rate` | 60 | Misc skills damage adjustments for Battleground maps (Note 2... |
| `bg_flee_penalty` | 20 | Flee penalty on BG grounds. NOTE: It's %, not absolute, so 2... |
| `bg_update_interval` | 1000 | Interval before updating the bg-member map mini-dots (millis... |
| `bgqueue_nowarp_mapflag` | no | Before a player is warped into a Battleground from the Battl... |

---

### Status

<!-- RAG_CHUNK: conf_status -->

**File:** `conf/battle/status.conf`

| Setting | Default | Description |
|---------|---------|-------------|
| `status_cast_cancel` | 0 | assume unit types (1: Pc, 2: Mob, 4: Pet, 8: Homun, 16: Merc... |
| `debuff_on_logout` | 0 | 1 = Remove negative buffs (status that are flagged as debuff... |
| `pc_status_def_rate` | 100 | Adjustment for the natural rate of resistance from status ch... |
| `mob_status_def_rate` | 100 |  |
| `pc_max_status_def` | 100 | Maximum resistance to status changes. (100 = 100%) NOTE: Car... |
| `mob_max_status_def` | 100 |  |

---

