---
title: rAthena Configuration Reference
type: config_reference
category: rathena_admin
tags: [configuration, conf, battle, rates, settings, server]
version: 2.0
mode: DEV
chunk_strategy: BY_SETTING
---

# rAthena Configuration Reference

This KB covers server configuration settings from `conf/` directory.

**Location:** Configuration files are in `conf/` and `conf/battle/`.

**Note Types:**
- Note 1: Switch value (on/off, yes/no, 1/0)
- Note 2: Percentage value (100 = 100%)
- Note 3: Bit field value

---

# Experience Settings (exp.conf)

## EXP Rates

| Setting | Default | Description |
|---------|---------|-------------|
| base_exp_rate | 100 | Base EXP rate (100 = 1x) |
| job_exp_rate | 100 | Job EXP rate (100 = 1x) |
| mvp_exp_rate | 100 | MVP bonus EXP rate |
| quest_exp_rate | 100 | Quest EXP rate |

## Multi Level Up

| Setting | Default | Description |
|---------|---------|-------------|
| multi_level_up | no | Allow leveling multiple times from one kill |
| multi_level_up_base | 0 | Cap for multi base level up (0 = unlimited) |
| multi_level_up_job | 0 | Cap for multi job level up (0 = unlimited) |

## EXP Gain Limits

| Setting | Default | Description |
|---------|---------|-------------|
| max_exp_gain_rate | 0 | Max EXP per kill as % of bar (0 = no limit) |
| exp_calc_type | 0 | 0=damage ratio, 1=damage/maxhp, 2=first attacker x2 |
| exp_bonus_attacker | 25 | EXP bonus % per additional attacker |
| exp_bonus_max_attacker | 12 | Max attackers for bonus cap |

## Death Penalty

| Setting | Default | Description |
|---------|---------|-------------|
| death_penalty_type | 1 | 0=none, 1=% current level, 2=% total exp |
| death_penalty_base | 100 | Base EXP penalty (100 = 1%) |
| death_penalty_job | 100 | Job EXP penalty (100 = 1%) |
| zeny_penalty | 0 | Zeny loss on death (100 = 1%) |
| death_penalty_maxlv | 0 | Lose EXP at max level (0=no, 1=base, 2=job) |

## Misc EXP Settings

| Setting | Default | Description |
|---------|---------|-------------|
| pvp_exp | yes | Enable EXP gain in PvP maps |
| heal_exp | 0 | Job EXP from Heal skill |
| resurrection_exp | 0 | EXP from resurrection (0.01%) |
| shop_exp | 0 | Job EXP from Discount/Overcharge |
| disp_experience | no | Display EXP gained messages |

---

# Drop Settings (drops.conf)

## Drop Rates by Type

| Setting | Default | Description |
|---------|---------|-------------|
| item_rate_common | 100 | ETC items drop rate |
| item_rate_common_boss | 100 | ETC from bosses |
| item_rate_common_mvp | 100 | ETC from MVPs |
| item_rate_heal | 100 | Healing items drop rate |
| item_rate_use | 100 | Usable items drop rate |
| item_rate_equip | 100 | Equipment drop rate |
| item_rate_card | 100 | Card drop rate |
| item_rate_mvp | 100 | MVP reward items |

## Drop Rate Limits

| Setting | Default | Description |
|---------|---------|-------------|
| item_drop_common_min | 1 | Minimum drop rate |
| item_drop_common_max | 10000 | Maximum drop rate (10000 = 100%) |
| item_drop_equip_min | 1 | Min equipment drop |
| item_drop_equip_max | 10000 | Max equipment drop |
| item_drop_card_min | 1 | Min card drop |
| item_drop_card_max | 10000 | Max card drop |

## Loot Priority

| Setting | Default | Description |
|---------|---------|-------------|
| first_attack_loot_bonus | 30 | Loot priority bonus for first attacker |
| item_first_get_time | 3000 | First loot priority (ms) |
| item_second_get_time | 2000 | Second loot priority (ms) |
| item_third_get_time | 2000 | Third loot priority (ms) |
| mvp_item_first_get_time | 10000 | MVP loot first priority (ms) |

## Misc Drop Settings

| Setting | Default | Description |
|---------|---------|-------------|
| item_auto_get | no | Items go directly to inventory |
| flooritem_lifetime | 60000 | Floor item timeout (ms) |
| item_drop_mvp_mode | 0 | 0=official, 1=random, 2=all items |

---

# Battle Settings (battle.conf)

## Attack Calculations

| Setting | Default | Description |
|---------|---------|-------------|
| enable_baseatk | 0x9 | Who has base ATK (bit field) |
| enable_baseatk_renewal | 0x29F | Renewal base ATK |
| enable_perfect_flee | 1 | Who can perfect flee |
| enable_critical | 17 | Who can critical |
| mob_critical_rate | 100 | Mob critical rate modifier |
| critical_rate | 100 | Player critical rate modifier |

## Walk/Attack Delay

| Setting | Default | Description |
|---------|---------|-------------|
| attack_walk_delay | 0 | Walk delay after attack (bit field) |
| damage_walk_delay | 0 | Legacy walk delay when damaged |
| pc_damage_walk_delay_rate | 20 | Player walk delay % |
| damage_walk_delay_rate | 100 | Monster walk delay % |
| multihit_delay | 200 | Multi-hit walk delay (ms) |

## Damage Settings

| Setting | Default | Description |
|---------|---------|-------------|
| min_hitrate | 5 | Minimum hit rate % |
| max_hitrate | 100 | Maximum hit rate % |
| attribute_recover | no | Heal from same element attacks |
| undead_detect_type | 0 | 0=element, 1=race, 2=both |

## AGI/VIT Penalty

| Setting | Default | Description |
|---------|---------|-------------|
| agi_penalty_type | 1 | 0=none, 1=%, 2=flat |
| agi_penalty_target | 1 | Who gets penalty (bit field) |
| agi_penalty_count | 3 | Enemies before penalty |
| agi_penalty_num | 10 | Penalty per extra attacker |
| vit_penalty_type | 1 | DEF penalty type |
| vit_penalty_count | 3 | Enemies before DEF penalty |
| vit_penalty_num | 5 | DEF penalty per attacker |

---

# Skill Settings (skill.conf)

## Cast Settings

| Setting | Default | Description |
|---------|---------|-------------|
| cast_rate | 100 | Global cast time rate |
| delay_rate | 100 | Global skill delay rate |
| delay_dependon_dex | no | Delay affected by DEX |
| delay_dependon_agi | no | Delay affected by AGI |
| castrate_dex_scale | 150 | DEX for 0 variable cast |
| skill_amotion_leniency | 90 | Animation leniency (ms) |

## Skill Behavior

| Setting | Default | Description |
|---------|---------|-------------|
| skill_add_range | 0 | Extra skill range |
| skill_out_range_consume | no | Consume on out-of-range |
| combo_delay_rate | 100 | Combo delay rate |
| skill_trap_type | 0 | Trap behavior type |
| autospell_check_range | no | Range check for autospell |

## Skill Restrictions

| Setting | Default | Description |
|---------|---------|-------------|
| skill_nofootset | 1 | Can't set traps on cells with existing effects |
| gvg_traps_target_all | 1 | Traps hit all in GvG |
| restricted_def_rate | 50 | DEF reduction for restricted skills |
| song_timer_reset | 0 | Reset song duration on recast |

---

# Player Settings (player.conf)

## HP/SP

| Setting | Default | Description |
|---------|---------|-------------|
| hp_rate | 100 | Max HP rate |
| sp_rate | 100 | Max SP rate |
| natural_healhp_interval | 6000 | HP regen interval (ms) |
| natural_healsp_interval | 8000 | SP regen interval (ms) |
| natural_heal_skill_interval | 10000 | Sitting skill interval (ms) |
| natural_heal_weight_rate | 50 | Weight % to stop regen |
| natural_heal_weight_rate_renewal | 70 | Renewal weight % |

## Damage/Defense

| Setting | Default | Description |
|---------|---------|-------------|
| player_defense_type | 0 | DEF calculation type |
| defnotenemy | 0 | DEF vs non-enemies |
| magic_defense_type | 0 | MDEF calculation type |
| player_cloak_check_type | 1 | Cloak check type |

## Stats

| Setting | Default | Description |
|---------|---------|-------------|
| max_parameter | 99 | Max base stat |
| max_trans_parameter | 99 | Max trans stat |
| max_third_trans_parameter | 130 | Max 3rd trans stat |
| max_baby_parameter | 80 | Max baby stat |
| max_extended_parameter | 125 | Max extended stat |
| max_summoner_parameter | 120 | Max Doram stat |
| max_fourth_parameter | 130 | Max 4th job stat |

## ASPD

| Setting | Default | Description |
|---------|---------|-------------|
| max_aspd | 190 | Max ASPD |
| max_third_aspd | 193 | Max 3rd class ASPD |
| max_extended_aspd | 193 | Max extended ASPD |
| max_summoner_aspd | 193 | Max Doram ASPD |
| max_fourth_aspd | 193 | Max 4th job ASPD |

---

# Monster Settings (monster.conf)

## Spawn/Respawn

| Setting | Default | Description |
|---------|---------|-------------|
| mob_spawn_delay | 100 | Spawn delay % |
| plant_spawn_delay | 100 | Plant spawn delay % |
| boss_spawn_delay | 100 | Boss spawn delay % |
| no_spawn_on_player | 0 | Distance from players for spawn |

## AI Behavior

| Setting | Default | Description |
|---------|---------|-------------|
| monster_active_enable | yes | Enable aggressive monsters |
| mob_skill_rate | 100 | Skill use rate |
| mob_skill_delay | 100 | Skill delay rate |
| mob_count_rate | 100 | Monster count rate |
| no_spawn_on_player | 0 | Min distance from players |

## Damage/Defense

| Setting | Default | Description |
|---------|---------|-------------|
| monster_defense_type | 0 | Monster DEF type |
| mob_max_def | 100 | Max mob DEF |
| mob_max_mdef | 100 | Max mob MDEF |

## Movement

| Setting | Default | Description |
|---------|---------|-------------|
| monster_max_aspd | 199 | Max monster ASPD |
| mob_warp | 0 | Warp behavior flags |
| boss_active_time | 0 | Boss active time |

---

# Feature Settings (feature.conf)

## System Features

| Setting | Default | Description |
|---------|---------|-------------|
| buying_store | yes | Enable buying stores |
| search_stores | yes | Enable store search |
| banking | yes | Enable banking |
| auction | no | Enable auctions |
| mail | yes | Enable mail system |
| achievement | yes | Enable achievements |
| attendance | yes | Enable attendance |
| private_airship | yes | Enable private airship |

## Renewal Features

| Setting | Default | Description |
|---------|---------|-------------|
| renewal_cast | yes | Renewal cast system |
| renewal_drop | yes | Renewal drop rates |
| renewal_exp | yes | Renewal EXP |
| renewal_aspd | yes | Renewal ASPD |

## PvP/GvG Features

| Setting | Default | Description |
|---------|---------|-------------|
| pk_mode | 0 | PK mode (0=off, 1=on, 2=GvG) |
| pk_level_range | 0 | Level range for PK |
| pk_mode_mes | yes | Show PK messages |

---

# Misc Settings (misc.conf)

## Core Settings

| Setting | Default | Description |
|---------|---------|-------------|
| enable_logs | 1 | Enable logging |
| save_clothcolor | yes | Save cloth color |
| save_body_style | yes | Save body style |
| pet_catch_rate | 100 | Pet catch rate |
| vending_max_value | 1000000000 | Max vending price |
| vending_over_max | yes | Allow over-max price |
| vending_tax | 0 | Vending tax (0.01%) |
| buyer_name | yes | Show buyer name |

## Display Settings

| Setting | Default | Description |
|---------|---------|-------------|
| show_mob_info | 0 | Show mob info |
| monster_hp_bars_info | yes | Show HP bars |
| zeny_from_mobs | no | Monsters drop Zeny |
| mob_remove_damaged | yes | Remove damaged mobs |

---

# Server Architecture

## Login Server (login-server.conf)

| Setting | Default | Description |
|---------|---------|-------------|
| login_port | 6900 | Login server port |
| use_MD5_passwords | no | Use MD5 password hashing |
| client_hash_check | no | Check client hash |
| console | on | Enable console |

## Char Server (char-server.conf)

| Setting | Default | Description |
|---------|---------|-------------|
| char_port | 6121 | Char server port |
| max_connect_user | -1 | Max connections (-1 = unlimited) |
| start_zeny | 0 | Starting Zeny |
| start_items | 1201,1,0,5 | Starting items |
| save_log | yes | Enable save log |
| char_move_enabled | yes | Allow char move |
| char_rename | yes | Allow char rename |

## Map Server (map-server.conf)

| Setting | Default | Description |
|---------|---------|-------------|
| map_port | 5121 | Map server port |
| autosave_time | 300 | Auto-save interval (sec) |
| minsave_time | 100 | Minimum save interval |
| save_settings | 0x1FF | What to save (bit field) |
| log_chat | no | Log chat messages |

---

# Quick Reference: Common Tasks

## Double EXP Rates
```conf
base_exp_rate: 200
job_exp_rate: 200
quest_exp_rate: 200
```

## Double Drop Rates
```conf
item_rate_common: 200
item_rate_heal: 200
item_rate_use: 200
item_rate_equip: 200
item_rate_card: 200
```

## Disable Death Penalty
```conf
death_penalty_type: 0
zeny_penalty: 0
```

## Enable Pre-Renewal Mode
```conf
// In Makefile or configure
--disable-renewal
```

## Max Stats to 255
```conf
max_parameter: 255
max_trans_parameter: 255
max_third_trans_parameter: 255
```

## Disable PvP/GvG Damage
```conf
// In battle.conf
pk_mode: 0
```

---

*KB Version 2.0 | Mode: DEV | Source: conf/battle/*.conf*
