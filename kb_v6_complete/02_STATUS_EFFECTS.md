# rAthena KB v6 - Status Effects Complete Reference

**Version:** 6.0 Complete
**Generated:** 2025-11-26
**Source:** doc/status_change.txt, src/map/status.hpp
**Total Status Effects:** 670

---

## Quick Navigation

### By Type
- [Common Ailments](#common-ailments) - Stone, Freeze, Stun, Poison
- [Buff Effects](#buff-effects) - Blessing, AGI Up, Aspersio
- [Debuff Effects](#debuff-effects) - Curse, Silence, Blind
- [Skill Effects](#skill-effects) - Skill-triggered statuses
- [Item Effects](#item-effects) - Consumable buffs
- [Guild War Effects](#gvg-effects) - WoE-specific statuses

### Alphabetical Quick Find

[SC_ABUNDANCE](#sc_abundance) | [SC_ACCELERATION](#sc_acceleration) | [SC_ADD_ATK_DAMAGE](#sc_add_atk_damage) | [SC_ADD_MATK_DAMAGE](#sc_add_matk_damage) | [SC_ADJUSTMENT](#sc_adjustment) | [SC_ADORAMUS](#sc_adoramus) | [SC_ADRENALINE](#sc_adrenaline) | [SC_ADRENALINE2](#sc_adrenaline2) | [SC_AETERNA](#sc_aeterna) | [SC_AGIFOOD](#sc_agifood) | 
[SC_AKAITSUKI](#sc_akaitsuki) | [SC_ALL_RIDING](#sc_all_riding) | [SC_ANALYZE](#sc_analyze) | [SC_ANGELUS](#sc_angelus) | [SC_ANGEL_PROTECT](#sc_angel_protect) | [SC_ANGRIFFS_MODUS](#sc_angriffs_modus) | [SC_ANKLE](#sc_ankle) | [SC_ANTI_M_BLAST](#sc_anti_m_blast) | [SC_APPLEIDUN](#sc_appleidun) | [SC_AQUAPLAY](#sc_aquaplay) | 
[SC_AQUAPLAY_OPTION](#sc_aquaplay_option) | [SC_ARCLOUSEDASH](#sc_arclousedash) | [SC_ARMOR](#sc_armor) | [SC_ARMORCHANGE](#sc_armorchange) | [SC_ARMOR_ELEMENT](#sc_armor_element) | [SC_ARMOR_RESIST](#sc_armor_resist) | [SC_ASH](#sc_ash) | [SC_ASPDPOTION0](#sc_aspdpotion0) | [SC_ASPDPOTION1](#sc_aspdpotion1) | [SC_ASPDPOTION2](#sc_aspdpotion2) | 
[SC_ASPDPOTION3](#sc_aspdpotion3) | [SC_ASPERSIO](#sc_aspersio) | [SC_ASSNCROS](#sc_assncros) | [SC_ASSUMPTIO](#sc_assumptio) | [SC_ATKPOTION](#sc_atkpotion) | [SC_AURABLADE](#sc_aurablade) | [SC_AUTOBERSERK](#sc_autoberserk) | [SC_AUTOCOUNTER](#sc_autocounter) | [SC_AUTOGUARD](#sc_autoguard) | [SC_AUTOSPELL](#sc_autospell) | 
[SC_AUTOTRADE](#sc_autotrade) | [SC_AVOID](#sc_avoid) | [SC_BABY](#sc_baby) | [SC_BANANA_BOMB](#sc_banana_bomb) | [SC_BANANA_BOMB_SITDOWN](#sc_banana_bomb_sitdown) | [SC_BANDING](#sc_banding) | [SC_BANDING_DEFENCE](#sc_banding_defence) | [SC_BARRIER](#sc_barrier) | [SC_BASILICA](#sc_basilica) | [SC_BATH_FOAM_A](#sc_bath_foam_a) | 
[SC_BATH_FOAM_B](#sc_bath_foam_b) | [SC_BATH_FOAM_C](#sc_bath_foam_c) | [SC_BATKFOOD](#sc_batkfood) | [SC_BATTLEORDERS](#sc_battleorders) | [SC_BENEDICTIO](#sc_benedictio) | [SC_BERSERK](#sc_berserk) | [SC_BEYONDOFWARCRY](#sc_beyondofwarcry) | [SC_BITE](#sc_bite) | [SC_BITESCAR](#sc_bitescar) | [SC_BLADESTOP](#sc_bladestop) | 
[SC_BLADESTOP_WAIT](#sc_bladestop_wait) | [SC_BLAST](#sc_blast) | [SC_BLAST_OPTION](#sc_blast_option) | [SC_BLEEDING](#sc_bleeding) | [SC_BLESSING](#sc_blessing) | [SC_BLIND](#sc_blind) | [SC_BLOODLUST](#sc_bloodlust) | [SC_BLOODSUCKER](#sc_bloodsucker) | [SC_BOOST500](#sc_boost500) | [SC_BOSSMAPINFO](#sc_bossmapinfo) | 
[SC_BROKENARMOR](#sc_brokenarmor) | [SC_BROKENWEAPON](#sc_brokenweapon) | [SC_BUCHEDENOEL](#sc_buchedenoel) | [SC_BUNSINJYUTSU](#sc_bunsinjyutsu) | [SC_BURNING](#sc_burning) | [SC_B_TRAP](#sc_b_trap) | [SC_CAMOUFLAGE](#sc_camouflage) | [SC_CARTBOOST](#sc_cartboost) | [SC_CATNIPPOWDER](#sc_catnippowder) | [SC_CBC](#sc_cbc) | 
[SC_CHANGE](#sc_change) | [SC_CHANGEUNDEAD](#sc_changeundead) | [SC_CHASEWALK](#sc_chasewalk) | [SC_CHASEWALK2](#sc_chasewalk2) | [SC_CHATTERING](#sc_chattering) | [SC_CHILLY_AIR](#sc_chilly_air) | [SC_CHILLY_AIR_OPTION](#sc_chilly_air_option) | [SC_CIRCLE_OF_FIRE](#sc_circle_of_fire) | [SC_CIRCLE_OF_FIRE_OPTION](#sc_circle_of_fire_option) | [SC_CLOAKING](#sc_cloaking) | 
[SC_CLOAKINGEXCEED](#sc_cloakingexceed) | [SC_CLOSECONFINE](#sc_closeconfine) | [SC_CLOSECONFINE2](#sc_closeconfine2) | [SC_COCKTAIL_WARG_BLOOD](#sc_cocktail_warg_blood) | [SC_COMA](#sc_coma) | [SC_COMBO](#sc_combo) | [SC_COMMONSC_RESIST](#sc_commonsc_resist) | [SC_CONCENTRATE](#sc_concentrate) | [SC_CONCENTRATION](#sc_concentration) | [SC_CONFUSION](#sc_confusion) | 
[SC_CONTENTS_1](#sc_contents_1) | [SC_CONTENTS_10](#sc_contents_10) | [SC_CONTENTS_2](#sc_contents_2) | [SC_CONTENTS_3](#sc_contents_3) | [SC_CONTENTS_4](#sc_contents_4) | [SC_CONTENTS_5](#sc_contents_5) | [SC_CONTENTS_6](#sc_contents_6) | [SC_CONTENTS_7](#sc_contents_7) | [SC_CONTENTS_8](#sc_contents_8) | [SC_CONTENTS_9](#sc_contents_9) | 
[SC_COOLER](#sc_cooler) | [SC_COOLER_OPTION](#sc_cooler_option) | [SC_CP_ARMOR](#sc_cp_armor) | [SC_CP_HELM](#sc_cp_helm) | [SC_CP_SHIELD](#sc_cp_shield) | [SC_CP_WEAPON](#sc_cp_weapon) | [SC_CRESCENTELBOW](#sc_crescentelbow) | [SC_CRITICALWOUND](#sc_criticalwound) | [SC_CRUSHSTRIKE](#sc_crushstrike) | [SC_CRYSTALIZE](#sc_crystalize) | 
[SC_CURSE](#sc_curse) | [SC_CURSEDCIRCLE_ATKER](#sc_cursedcircle_atker) | [SC_CURSEDCIRCLE_TARGET](#sc_cursedcircle_target) | [SC_CURSED_SOIL](#sc_cursed_soil) | [SC_CURSED_SOIL_OPTION](#sc_cursed_soil_option) | [SC_C_MARKER](#sc_c_marker) | [SC_DANCEWITHWUG](#sc_dancewithwug) | [SC_DANCING](#sc_dancing) | [SC_DARKCROW](#sc_darkcrow) | [SC_DEATHBOUND](#sc_deathbound) | 
[SC_DEATHHURT](#sc_deathhurt) | [SC_DECORATION_OF_MUSIC](#sc_decoration_of_music) | [SC_DECREASEAGI](#sc_decreaseagi) | [SC_DEEPSLEEP](#sc_deepsleep) | [SC_DEFENCE](#sc_defence) | [SC_DEFENDER](#sc_defender) | [SC_DEFRATIOATK](#sc_defratioatk) | [SC_DEFSET](#sc_defset) | [SC_DEF_RATE](#sc_def_rate) | [SC_DELUGE](#sc_deluge) | 
[SC_DEVOTION](#sc_devotion) | [SC_DEXFOOD](#sc_dexfood) | [SC_DODGE](#sc_dodge) | [SC_DONTFORGETME](#sc_dontforgetme) | [SC_DORAM_BUF_01](#sc_doram_buf_01) | [SC_DORAM_BUF_02](#sc_doram_buf_02) | [SC_DORAM_FLEE2](#sc_doram_flee2) | [SC_DORAM_MATK](#sc_doram_matk) | [SC_DORAM_SVSP](#sc_doram_svsp) | [SC_DORAM_WALKSPEED](#sc_doram_walkspeed) | 
[SC_DOUBLECAST](#sc_doublecast) | [SC_DPOISON](#sc_dpoison) | [SC_DROCERA_HERB_STEAMED](#sc_drocera_herb_steamed) | [SC_DRUMBATTLE](#sc_drumbattle) | [SC_DUPLELIGHT](#sc_duplelight) | [SC_EARTHDRIVE](#sc_earthdrive) | [SC_EARTHSCROLL](#sc_earthscroll) | [SC_EARTHWEAPON](#sc_earthweapon) | [SC_EARTH_INSIGNIA](#sc_earth_insignia) | [SC_ECHOSONG](#sc_echosong) | 
[SC_EDP](#sc_edp) | [SC_ELECTRICSHOCKER](#sc_electricshocker) | [SC_ELEMENTALCHANGE](#sc_elementalchange) | [SC_ELEMENTAL_SHIELD](#sc_elemental_shield) | [SC_EMERGENCY_MOVE](#sc_emergency_move) | [SC_ENCHANTARMS](#sc_enchantarms) | [SC_ENCHANTBLADE](#sc_enchantblade) | [SC_ENCPOISON](#sc_encpoison) | [SC_ENDURE](#sc_endure) | [SC_ENERGYCOAT](#sc_energycoat) | 
[SC_ENSEMBLEFATIGUE](#sc_ensemblefatigue) | [SC_EP16_2_BUFF_AC](#sc_ep16_2_buff_ac) | [SC_EP16_2_BUFF_SC](#sc_ep16_2_buff_sc) | [SC_EP16_2_BUFF_SS](#sc_ep16_2_buff_ss) | [SC_EP16_DEF](#sc_ep16_def) | [SC_EPICLESIS](#sc_epiclesis) | [SC_EQC](#sc_eqc) | [SC_ETERNALCHAOS](#sc_eternalchaos) | [SC_EXEEDBREAK](#sc_exeedbreak) | [SC_EXPBOOST](#sc_expboost) | 
[SC_EXPIATIO](#sc_expiatio) | [SC_EXPLOSIONSPIRITS](#sc_explosionspirits) | [SC_EXTRACT_SALAMINE_JUICE](#sc_extract_salamine_juice) | [SC_EXTRACT_WHITE_POTION_Z](#sc_extract_white_potion_z) | [SC_EXTREMITYFIST](#sc_extremityfist) | [SC_EXTREMITYFIST2](#sc_extremityfist2) | [SC_E_CHAIN](#sc_e_chain) | [SC_FASTCAST](#sc_fastcast) | [SC_FEAR](#sc_fear) | [SC_FEARBREEZE](#sc_fearbreeze) | 
[SC_FIGHTINGSPIRIT](#sc_fightingspirit) | [SC_FIREWEAPON](#sc_fireweapon) | [SC_FIRE_CLOAK](#sc_fire_cloak) | [SC_FIRE_CLOAK_OPTION](#sc_fire_cloak_option) | [SC_FIRE_INSIGNIA](#sc_fire_insignia) | [SC_FLASHCOMBO](#sc_flashcombo) | [SC_FLEEFOOD](#sc_fleefood) | [SC_FLEET](#sc_fleet) | [SC_FLING](#sc_fling) | [SC_FOGWALL](#sc_fogwall) | 
[SC_FOOD_AGI_CASH](#sc_food_agi_cash) | [SC_FOOD_DEX_CASH](#sc_food_dex_cash) | [SC_FOOD_INT_CASH](#sc_food_int_cash) | [SC_FOOD_LUK_CASH](#sc_food_luk_cash) | [SC_FOOD_STR_CASH](#sc_food_str_cash) | [SC_FOOD_VIT_CASH](#sc_food_vit_cash) | [SC_FORCEOFVANGUARD](#sc_forceofvanguard) | [SC_FORTUNE](#sc_fortune) | [SC_FREEZE](#sc_freeze) | [SC_FREEZE_SP](#sc_freeze_sp) | 
[SC_FREEZING](#sc_freezing) | [SC_FRESHSHRIMP](#sc_freshshrimp) | [SC_FRIGG_SONG](#sc_frigg_song) | [SC_FULL_SWING_K](#sc_full_swing_k) | [SC_FULL_THROTTLE](#sc_full_throttle) | [SC_FURY](#sc_fury) | [SC_FUSION](#sc_fusion) | [SC_GATLINGFEVER](#sc_gatlingfever) | [SC_GENSOU](#sc_gensou) | [SC_GHOSTWEAPON](#sc_ghostweapon) | 
[SC_GIANTGROWTH](#sc_giantgrowth) | [SC_GLOOMYDAY](#sc_gloomyday) | [SC_GLOOMYDAY_SK](#sc_gloomyday_sk) | [SC_GLORIA](#sc_gloria) | [SC_GLORYWOUNDS](#sc_glorywounds) | [SC_GN_CARTBOOST](#sc_gn_cartboost) | [SC_GOLDENE_FERSE](#sc_goldene_ferse) | [SC_GOSPEL](#sc_gospel) | [SC_GRANITIC_ARMOR](#sc_granitic_armor) | [SC_GRAVITATION](#sc_gravitation) | 
[SC_GROOMING](#sc_grooming) | [SC_GT_CHANGE](#sc_gt_change) | [SC_GT_ENERGYGAIN](#sc_gt_energygain) | [SC_GT_REVITALIZE](#sc_gt_revitalize) | [SC_GUILDAURA](#sc_guildaura) | [SC_GUST](#sc_gust) | [SC_GUST_OPTION](#sc_gust_option) | [SC_GVG_BLIND](#sc_gvg_blind) | [SC_GVG_CURSE](#sc_gvg_curse) | [SC_GVG_FREEZ](#sc_gvg_freez) | 
[SC_GVG_GIANT](#sc_gvg_giant) | [SC_GVG_GOLEM](#sc_gvg_golem) | [SC_GVG_SILENCE](#sc_gvg_silence) | [SC_GVG_SLEEP](#sc_gvg_sleep) | [SC_GVG_STONE](#sc_gvg_stone) | [SC_GVG_STUN](#sc_gvg_stun) | [SC_HALLUCINATION](#sc_hallucination) | [SC_HALLUCINATIONWALK](#sc_hallucinationwalk) | [SC_HALLUCINATIONWALK_POSTDELAY](#sc_hallucinationwalk_postdelay) | [SC_HANBOK](#sc_hanbok) | 
[SC_HARMONIZE](#sc_harmonize) | [SC_HAWKEYES](#sc_hawkeyes) | [SC_HEATER](#sc_heater) | [SC_HEATER_OPTION](#sc_heater_option) | [SC_HEAT_BARREL](#sc_heat_barrel) | [SC_HELLPOWER](#sc_hellpower) | [SC_HELPANGEL](#sc_helpangel) | [SC_HERMODE](#sc_hermode) | [SC_HIDING](#sc_hiding) | [SC_HISS](#sc_hiss) | 
[SC_HITFOOD](#sc_hitfood) | [SC_HOVERING](#sc_hovering) | [SC_HPDRAIN](#sc_hpdrain) | [SC_HPREGEN](#sc_hpregen) | [SC_HUMMING](#sc_humming) | [SC_H_MINE](#sc_h_mine) | [SC_IGNOREDEF](#sc_ignoredef) | [SC_ILLUSIONDOPING](#sc_illusiondoping) | [SC_IMPOSITIO](#sc_impositio) | [SC_INCAGI](#sc_incagi) | 
[SC_INCALLSTATUS](#sc_incallstatus) | [SC_INCASPDRATE](#sc_incaspdrate) | [SC_INCATKRATE](#sc_incatkrate) | [SC_INCBASEATK](#sc_incbaseatk) | [SC_INCCRI](#sc_inccri) | [SC_INCDEF](#sc_incdef) | [SC_INCDEFRATE](#sc_incdefrate) | [SC_INCDEX](#sc_incdex) | [SC_INCFLEE](#sc_incflee) | [SC_INCFLEE2](#sc_incflee2) | 
[SC_INCFLEERATE](#sc_incfleerate) | [SC_INCHEALRATE](#sc_inchealrate) | [SC_INCHIT](#sc_inchit) | [SC_INCHITRATE](#sc_inchitrate) | [SC_INCINT](#sc_incint) | [SC_INCLUK](#sc_incluk) | [SC_INCMATKRATE](#sc_incmatkrate) | [SC_INCMHP](#sc_incmhp) | [SC_INCMHPRATE](#sc_incmhprate) | [SC_INCMSP](#sc_incmsp) | 
[SC_INCMSPRATE](#sc_incmsprate) | [SC_INCREASEAGI](#sc_increaseagi) | [SC_INCREASE_MAXHP](#sc_increase_maxhp) | [SC_INCREASE_MAXSP](#sc_increase_maxsp) | [SC_INCREASING](#sc_increasing) | [SC_INCSTR](#sc_incstr) | [SC_INCVIT](#sc_incvit) | [SC_INFRAREDSCAN](#sc_infraredscan) | [SC_INSPIRATION](#sc_inspiration) | [SC_INTFOOD](#sc_intfood) | 
[SC_INTOABYSS](#sc_intoabyss) | [SC_INTRAVISION](#sc_intravision) | [SC_INT_SCROLL](#sc_int_scroll) | [SC_INVINCIBLE](#sc_invincible) | [SC_INVINCIBLEOFF](#sc_invincibleoff) | [SC_ITEMBOOST](#sc_itemboost) | [SC_ITEMSCRIPT](#sc_itemscript) | [SC_IZAYOI](#sc_izayoi) | [SC_JAILED](#sc_jailed) | [SC_JEXPBOOST](#sc_jexpboost) | 
[SC_JOINTBEAT](#sc_jointbeat) | [SC_JYUMONJIKIRI](#sc_jyumonjikiri) | [SC_KAAHI](#sc_kaahi) | [SC_KAENSIN](#sc_kaensin) | [SC_KAGEHUMI](#sc_kagehumi) | [SC_KAGEMUSYA](#sc_kagemusya) | [SC_KAITE](#sc_kaite) | [SC_KAIZEL](#sc_kaizel) | [SC_KAUPE](#sc_kaupe) | [SC_KEEPING](#sc_keeping) | 
[SC_KINGS_GRACE](#sc_kings_grace) | [SC_KNOWLEDGE](#sc_knowledge) | [SC_KSPROTECTED](#sc_ksprotected) | [SC_KYOMU](#sc_kyomu) | [SC_KYOUGAKU](#sc_kyougaku) | [SC_KYRIE](#sc_kyrie) | [SC_LAUDAAGNUS](#sc_laudaagnus) | [SC_LAUDARAMUS](#sc_laudaramus) | [SC_LEADERSHIP](#sc_leadership) | [SC_LEECHESEND](#sc_leechesend) | 
[SC_LERADSDEW](#sc_leradsdew) | [SC_LHZ_DUN_N1](#sc_lhz_dun_n1) | [SC_LHZ_DUN_N2](#sc_lhz_dun_n2) | [SC_LHZ_DUN_N3](#sc_lhz_dun_n3) | [SC_LHZ_DUN_N4](#sc_lhz_dun_n4) | [SC_LIFEINSURANCE](#sc_lifeinsurance) | [SC_LIFE_FORCE_F](#sc_life_force_f) | [SC_LIGHTNINGWALK](#sc_lightningwalk) | [SC_LIGHT_OF_REGENE](#sc_light_of_regene) | [SC_LONGING](#sc_longing) | 
[SC_LOUD](#sc_loud) | [SC_LUKFOOD](#sc_lukfood) | [SC_LUXANIMA](#sc_luxanima) | [SC_L_LIFEPOTION](#sc_l_lifepotion) | [SC_MADNESSCANCEL](#sc_madnesscancel) | [SC_MAGICALATTACK](#sc_magicalattack) | [SC_MAGICALBULLET](#sc_magicalbullet) | [SC_MAGICMIRROR](#sc_magicmirror) | [SC_MAGICMUSHROOM](#sc_magicmushroom) | [SC_MAGICPOWER](#sc_magicpower) | 
[SC_MAGICROD](#sc_magicrod) | [SC_MAGIC_POISON](#sc_magic_poison) | [SC_MAGMA_FLOW](#sc_magma_flow) | [SC_MAGNETICFIELD](#sc_magneticfield) | [SC_MAGNIFICAT](#sc_magnificat) | [SC_MANA_PLUS](#sc_mana_plus) | [SC_MANDRAGORA](#sc_mandragora) | [SC_MANU_ATK](#sc_manu_atk) | [SC_MANU_DEF](#sc_manu_def) | [SC_MANU_MATK](#sc_manu_matk) | 
[SC_MARIONETTE](#sc_marionette) | [SC_MARIONETTE2](#sc_marionette2) | [SC_MARSHOFABYSS](#sc_marshofabyss) | [SC_MATKFOOD](#sc_matkfood) | [SC_MATKPOTION](#sc_matkpotion) | [SC_MAXIMIZEPOWER](#sc_maximizepower) | [SC_MAXOVERTHRUST](#sc_maxoverthrust) | [SC_MAXSPELLBOOK](#sc_maxspellbook) | [SC_MDEFSET](#sc_mdefset) | [SC_MDEF_RATE](#sc_mdef_rate) | 
[SC_MEIKYOUSISUI](#sc_meikyousisui) | [SC_MELODYOFSINK](#sc_melodyofsink) | [SC_MELON_BOMB](#sc_melon_bomb) | [SC_MELTDOWN](#sc_meltdown) | [SC_MEMORIZE](#sc_memorize) | [SC_MERC_ATKUP](#sc_merc_atkup) | [SC_MERC_FLEEUP](#sc_merc_fleeup) | [SC_MERC_HITUP](#sc_merc_hitup) | [SC_MERC_HPUP](#sc_merc_hpup) | [SC_MERC_QUICKEN](#sc_merc_quicken) | 
[SC_MERC_SPUP](#sc_merc_spup) | [SC_MILLENNIUMSHIELD](#sc_millenniumshield) | [SC_MINDBREAKER](#sc_mindbreaker) | [SC_MINOR_BBQ](#sc_minor_bbq) | [SC_MIRACLE](#sc_miracle) | [SC_MISTY_FROST](#sc_misty_frost) | [SC_MODECHANGE](#sc_modechange) | [SC_MONSTER_TRANSFORM](#sc_monster_transform) | [SC_MOONLITSERENADE](#sc_moonlitserenade) | [SC_MOONSTAR](#sc_moonstar) | 
[SC_MOON_COMFORT](#sc_moon_comfort) | [SC_MTF_ASPD](#sc_mtf_aspd) | [SC_MTF_ASPD2](#sc_mtf_aspd2) | [SC_MTF_CRIDAMAGE](#sc_mtf_cridamage) | [SC_MTF_MATK](#sc_mtf_matk) | [SC_MTF_MATK2](#sc_mtf_matk2) | [SC_MTF_MLEATKED](#sc_mtf_mleatked) | [SC_MTF_RANGEATK](#sc_mtf_rangeatk) | [SC_MTF_RANGEATK2](#sc_mtf_rangeatk2) | [SC_MUSTLE_M](#sc_mustle_m) | 
[SC_MYSTERIOUS_POWDER](#sc_mysterious_powder) | [SC_NEN](#sc_nen) | [SC_NETHERWORLD](#sc_netherworld) | [SC_NEUTRALBARRIER](#sc_neutralbarrier) | [SC_NEUTRALBARRIER_MASTER](#sc_neutralbarrier_master) | [SC_NIBELUNGEN](#sc_nibelungen) | [SC_NOCHAT](#sc_nochat) | [SC_NYANGGRASS](#sc_nyanggrass) | [SC_OBLIVIONCURSE](#sc_oblivioncurse) | [SC_ODINS_POWER](#sc_odins_power) | 
[SC_OFFERTORIUM](#sc_offertorium) | [SC_OKTOBERFEST](#sc_oktoberfest) | [SC_ONEHAND](#sc_onehand) | [SC_ORATIO](#sc_oratio) | [SC_ORCISH](#sc_orcish) | [SC_OVERED_BOOST](#sc_overed_boost) | [SC_OVERHEAT](#sc_overheat) | [SC_OVERHEAT_LIMITPOINT](#sc_overheat_limitpoint) | [SC_OVERTHRUST](#sc_overthrust) | [SC_PACKING_ENVELOPE1](#sc_packing_envelope1) | 
[SC_PACKING_ENVELOPE10](#sc_packing_envelope10) | [SC_PACKING_ENVELOPE2](#sc_packing_envelope2) | [SC_PACKING_ENVELOPE3](#sc_packing_envelope3) | [SC_PACKING_ENVELOPE4](#sc_packing_envelope4) | [SC_PACKING_ENVELOPE5](#sc_packing_envelope5) | [SC_PACKING_ENVELOPE6](#sc_packing_envelope6) | [SC_PACKING_ENVELOPE7](#sc_packing_envelope7) | [SC_PACKING_ENVELOPE8](#sc_packing_envelope8) | [SC_PACKING_ENVELOPE9](#sc_packing_envelope9) | [SC_PAIN_KILLER](#sc_pain_killer) | 
[SC_PARALYSE](#sc_paralyse) | [SC_PARALYSIS](#sc_paralysis) | [SC_PARRYING](#sc_parrying) | [SC_PARTYFLEE](#sc_partyflee) | [SC_PETROLOGY](#sc_petrology) | [SC_PETROLOGY_OPTION](#sc_petrology_option) | [SC_PNEUMA](#sc_pneuma) | [SC_POEMBRAGI](#sc_poembragi) | [SC_POISON](#sc_poison) | [SC_POISONINGWEAPON](#sc_poisoningweapon) | 
[SC_POISONREACT](#sc_poisonreact) | [SC_POWER_OF_GAIA](#sc_power_of_gaia) | [SC_PRESERVE](#sc_preserve) | [SC_PRESTIGE](#sc_prestige) | [SC_PROPERTYWALK](#sc_propertywalk) | [SC_PROVIDENCE](#sc_providence) | [SC_PROVOKE](#sc_provoke) | [SC_PUSH_CART](#sc_push_cart) | [SC_PUTTI_TAILS_NOODLES](#sc_putti_tails_noodles) | [SC_PYREXIA](#sc_pyrexia) | 
[SC_PYROCLASTIC](#sc_pyroclastic) | [SC_PYROTECHNIC](#sc_pyrotechnic) | [SC_PYROTECHNIC_OPTION](#sc_pyrotechnic_option) | [SC_P_ALTER](#sc_p_alter) | [SC_QD_SHOT_READY](#sc_qd_shot_ready) | [SC_QUAGMIRE](#sc_quagmire) | [SC_QUEST_BUFF1](#sc_quest_buff1) | [SC_QUEST_BUFF2](#sc_quest_buff2) | [SC_QUEST_BUFF3](#sc_quest_buff3) | [SC_RAID](#sc_raid) | 
[SC_RAISINGDRAGON](#sc_raisingdragon) | [SC_READING_SB](#sc_reading_sb) | [SC_READYCOUNTER](#sc_readycounter) | [SC_READYDOWN](#sc_readydown) | [SC_READYSTORM](#sc_readystorm) | [SC_READYTURN](#sc_readyturn) | [SC_REBIRTH](#sc_rebirth) | [SC_REBOUND](#sc_rebound) | [SC_RECOGNIZEDSPELL](#sc_recognizedspell) | [SC_REFLECTDAMAGE](#sc_reflectdamage) | 
[SC_REFLECTSHIELD](#sc_reflectshield) | [SC_REFRESH](#sc_refresh) | [SC_REF_T_POTION](#sc_ref_t_potion) | [SC_REGENERATION](#sc_regeneration) | [SC_REJECTSWORD](#sc_rejectsword) | [SC_RENOVATIO](#sc_renovatio) | [SC_REUSE_LIMIT_LUXANIMA](#sc_reuse_limit_luxanima) | [SC_REUSE_REFRESH](#sc_reuse_refresh) | [SC_RICHMANKIM](#sc_richmankim) | [SC_ROCK_CRUSHER](#sc_rock_crusher) | 
[SC_ROCK_CRUSHER_ATK](#sc_rock_crusher_atk) | [SC_ROKISWEIL](#sc_rokisweil) | [SC_ROLLINGCUTTER](#sc_rollingcutter) | [SC_RUN](#sc_run) | [SC_RUSHWINDMILL](#sc_rushwindmill) | [SC_RUWACH](#sc_ruwach) | [SC_SACRIFICE](#sc_sacrifice) | [SC_SAFETYWALL](#sc_safetywall) | [SC_SATURDAYNIGHTFEVER](#sc_saturdaynightfever) | [SC_SAVAGE_STEAK](#sc_savage_steak) | 
[SC_SCRESIST](#sc_scresist) | [SC_SECRAMENT](#sc_secrament) | [SC_SERVICE4U](#sc_service4u) | [SC_SEVENWIND](#sc_sevenwind) | [SC_SHADOWWEAPON](#sc_shadowweapon) | [SC_SHAPESHIFT](#sc_shapeshift) | [SC_SHIELDSPELL_DEF](#sc_shieldspell_def) | [SC_SHIELDSPELL_MDEF](#sc_shieldspell_mdef) | [SC_SHIELDSPELL_REF](#sc_shieldspell_ref) | [SC_SHRIMP](#sc_shrimp) | 
[SC_SHRIMPBLESSING](#sc_shrimpblessing) | [SC_SHRINK](#sc_shrink) | [SC_SIEGFRIED](#sc_siegfried) | [SC_SIGHT](#sc_sight) | [SC_SIGHTBLASTER](#sc_sightblaster) | [SC_SIGHTTRASHER](#sc_sighttrasher) | [SC_SIGNUMCRUCIS](#sc_signumcrucis) | [SC_SILENCE](#sc_silence) | [SC_SIRCLEOFNATURE](#sc_sircleofnature) | [SC_SIROMA_ICE_TEA](#sc_siroma_ice_tea) | 
[SC_SITDOWN_FORCE](#sc_sitdown_force) | [SC_SKA](#sc_ska) | [SC_SKE](#sc_ske) | [SC_SKILLATKBONUS](#sc_skillatkbonus) | [SC_SKILLCASTRATE](#sc_skillcastrate) | [SC_SKILLRATE_UP](#sc_skillrate_up) | [SC_SLEEP](#sc_sleep) | [SC_SLOWCAST](#sc_slowcast) | [SC_SLOWDOWN](#sc_slowdown) | [SC_SLOWPOISON](#sc_slowpoison) | 
[SC_SMA](#sc_sma) | [SC_SMOKEPOWDER](#sc_smokepowder) | [SC_SOLID_SKIN](#sc_solid_skin) | [SC_SOLID_SKIN_OPTION](#sc_solid_skin_option) | [SC_SONGOFMANA](#sc_songofmana) | [SC_SOULCOLD](#sc_soulcold) | [SC_SOUNDOFDESTRUCTION](#sc_soundofdestruction) | [SC_SPCOST_RATE](#sc_spcost_rate) | [SC_SPEARQUICKEN](#sc_spearquicken) | [SC_SPEED](#sc_speed) | 
[SC_SPEEDUP0](#sc_speedup0) | [SC_SPEEDUP1](#sc_speedup1) | [SC_SPELLBOOK1](#sc_spellbook1) | [SC_SPELLBOOK2](#sc_spellbook2) | [SC_SPELLBOOK3](#sc_spellbook3) | [SC_SPELLBOOK4](#sc_spellbook4) | [SC_SPELLBOOK5](#sc_spellbook5) | [SC_SPELLBOOK6](#sc_spellbook6) | [SC_SPELLBREAKER](#sc_spellbreaker) | [SC_SPELLFIST](#sc_spellfist) | 
[SC_SPHERE_1](#sc_sphere_1) | [SC_SPHERE_2](#sc_sphere_2) | [SC_SPHERE_3](#sc_sphere_3) | [SC_SPHERE_4](#sc_sphere_4) | [SC_SPHERE_5](#sc_sphere_5) | [SC_SPIDERWEB](#sc_spiderweb) | [SC_SPIRIT](#sc_spirit) | [SC_SPLASHER](#sc_splasher) | [SC_SPL_ATK](#sc_spl_atk) | [SC_SPL_DEF](#sc_spl_def) | 
[SC_SPL_MATK](#sc_spl_matk) | [SC_SPREGEN](#sc_spregen) | [SC_SPRITEMABLE](#sc_spritemable) | [SC_SPURT](#sc_spurt) | [SC_STAR_COMFORT](#sc_star_comfort) | [SC_STASIS](#sc_stasis) | [SC_STEALTHFIELD](#sc_stealthfield) | [SC_STEALTHFIELD_MASTER](#sc_stealthfield_master) | [SC_STEELBODY](#sc_steelbody) | [SC_STOMACHACHE](#sc_stomachache) | 
[SC_STONE](#sc_stone) | [SC_STONEHARDSKIN](#sc_stonehardskin) | [SC_STONE_SHIELD](#sc_stone_shield) | [SC_STONE_SHIELD_OPTION](#sc_stone_shield_option) | [SC_STOP](#sc_stop) | [SC_STORMBLAST](#sc_stormblast) | [SC_STRANGELIGHTS](#sc_strangelights) | [SC_STRFOOD](#sc_strfood) | [SC_STRIKING](#sc_striking) | [SC_STRIPARMOR](#sc_striparmor) | 
[SC_STRIPHELM](#sc_striphelm) | [SC_STRIPSHIELD](#sc_stripshield) | [SC_STRIPWEAPON](#sc_stripweapon) | [SC_STR_SCROLL](#sc_str_scroll) | [SC_STUN](#sc_stun) | [SC_STYLE_CHANGE](#sc_style_change) | [SC_SUFFRAGIUM](#sc_suffragium) | [SC_SUHIDE](#sc_suhide) | [SC_SUITON](#sc_suiton) | [SC_SUMMER](#sc_summer) | 
[SC_SUN_COMFORT](#sc_sun_comfort) | [SC_SUPER_STAR](#sc_super_star) | [SC_SU_STOOP](#sc_su_stoop) | [SC_SV_ROOTTWIST](#sc_sv_roottwist) | [SC_SWINGDANCE](#sc_swingdance) | [SC_SWOO](#sc_swoo) | [SC_SYMPHONYOFLOVER](#sc_symphonyoflover) | [SC_S_LIFEPOTION](#sc_s_lifepotion) | [SC_TATAMIGAESHI](#sc_tatamigaeshi) | [SC_TEARGAS](#sc_teargas) | 
[SC_TEARGAS_SOB](#sc_teargas_sob) | [SC_TELEKINESIS_INTENSE](#sc_telekinesis_intense) | [SC_TENSIONRELAX](#sc_tensionrelax) | [SC_THORNSTRAP](#sc_thornstrap) | [SC_TIDAL_WEAPON](#sc_tidal_weapon) | [SC_TIDAL_WEAPON_OPTION](#sc_tidal_weapon_option) | [SC_TINDER_BREAKER](#sc_tinder_breaker) | [SC_TINDER_BREAKER2](#sc_tinder_breaker2) | [SC_TOXIN](#sc_toxin) | [SC_TRICKDEAD](#sc_trickdead) | 
[SC_TROPIC](#sc_tropic) | [SC_TROPIC_OPTION](#sc_tropic_option) | [SC_TRUESIGHT](#sc_truesight) | [SC_TUNAPARTY](#sc_tunaparty) | [SC_TWOHANDQUICKEN](#sc_twohandquicken) | [SC_UNLIMIT](#sc_unlimit) | [SC_UNLIMITEDHUMMINGVOICE](#sc_unlimitedhummingvoice) | [SC_UPHEAVAL](#sc_upheaval) | [SC_UPHEAVAL_OPTION](#sc_upheaval_option) | [SC_UTSUSEMI](#sc_utsusemi) | 
[SC_VACUUM_EXTREME](#sc_vacuum_extreme) | [SC_VENOMBLEED](#sc_venombleed) | [SC_VENOMIMPRESS](#sc_venomimpress) | [SC_VIOLENTGALE](#sc_violentgale) | [SC_VITALITYACTIVATION](#sc_vitalityactivation) | [SC_VITATA_500](#sc_vitata_500) | [SC_VITFOOD](#sc_vitfood) | [SC_VOICEOFSIREN](#sc_voiceofsiren) | [SC_VOLCANO](#sc_volcano) | [SC_WALKSPEED](#sc_walkspeed) | 
[SC_WARM](#sc_warm) | [SC_WARMER](#sc_warmer) | [SC_WATERWEAPON](#sc_waterweapon) | [SC_WATER_BARRIER](#sc_water_barrier) | [SC_WATER_DROP](#sc_water_drop) | [SC_WATER_DROP_OPTION](#sc_water_drop_option) | [SC_WATER_INSIGNIA](#sc_water_insignia) | [SC_WATER_SCREEN](#sc_water_screen) | [SC_WATER_SCREEN_OPTION](#sc_water_screen_option) | [SC_WATKFOOD](#sc_watkfood) | 
[SC_WATK_ELEMENT](#sc_watk_element) | [SC_WEAPONBLOCKING](#sc_weaponblocking) | [SC_WEAPONPERFECTION](#sc_weaponperfection) | [SC_WEDDING](#sc_wedding) | [SC_WEIGHT50](#sc_weight50) | [SC_WEIGHT90](#sc_weight90) | [SC_WHISTLE](#sc_whistle) | [SC_WHITEIMPRISON](#sc_whiteimprison) | [SC_WILD_STORM](#sc_wild_storm) | [SC_WILD_STORM_OPTION](#sc_wild_storm_option) | 
[SC_WINDWALK](#sc_windwalk) | [SC_WINDWEAPON](#sc_windweapon) | [SC_WIND_CURTAIN](#sc_wind_curtain) | [SC_WIND_CURTAIN_OPTION](#sc_wind_curtain_option) | [SC_WIND_INSIGNIA](#sc_wind_insignia) | [SC_WIND_STEP](#sc_wind_step) | [SC_WIND_STEP_OPTION](#sc_wind_step_option) | [SC_WINKCHARM](#sc_winkcharm) | [SC_WUGDASH](#sc_wugdash) | [SC_XMAS](#sc_xmas) | 
[SC_ZANGETSU](#sc_zangetsu) | [SC_ZENKAI](#sc_zenkai) | [SC_ZEPHYR](#sc_zephyr) | [SC__AUTOSHADOWSPELL](#sc__autoshadowspell) | [SC__BLOODYLUST](#sc__bloodylust) | [SC__BODYPAINT](#sc__bodypaint) | [SC__CHAOS](#sc__chaos) | [SC__DEADLYINFECT](#sc__deadlyinfect) | [SC__ENERVATION](#sc__enervation) | [SC__FEINTBOMB](#sc__feintbomb) | 
[SC__GROOMY](#sc__groomy) | [SC__IGNORANCE](#sc__ignorance) | [SC__INVISIBILITY](#sc__invisibility) | [SC__LAZINESS](#sc__laziness) | [SC__MANHOLE](#sc__manhole) | [SC__REPRODUCE](#sc__reproduce) | [SC__SHADOWFORM](#sc__shadowform) | [SC__STRIPACCESSORY](#sc__stripaccessory) | [SC__UNLUCKY](#sc__unlucky) | [SC__WEAKNESS](#sc__weakness) | 

---

## Using Status Effects

### Script Commands
```c
// Apply status effect
sc_start <SC_NAME>, <duration_ms>, <val1>;
sc_start2 <SC_NAME>, <duration_ms>, <val1>, <val2>;
sc_start4 <SC_NAME>, <duration_ms>, <val1>, <val2>, <val3>, <val4>;

// Check status
if (getstatus(SC_BLESSING)) { mes "You are blessed!"; }

// Remove status
sc_end SC_BLESSING;
sc_end SC_ALL;  // Remove all statuses
```

### Flags for sc_start
| Flag | Value | Effect |
|------|-------|--------|
| SCSTART_NOAVOID | 1 | Cannot be resisted |
| SCSTART_NOTICKDEF | 2 | Duration ignores VIT |
| SCSTART_LOADED | 4 | Use val1-4 directly |
| SCSTART_NORATEDEF | 8 | Rate ignores LUK |

---

## Complete Status Effect Reference

## Common Ailments

<!-- RAG_CHUNK: sc_common_ailments -->

### SC_STONE

**Effect:** DEF -50%; if HP>25% lose 1% HP/5 sec; MDEF +25%; change element to Earth Lv 1; ignore Steal & Lex Aeterna; can't move/attack/pick item/use item/use skill/sit/logout

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | Caster's object ID |
| val3 | Incubation time |
| val4 | Remaining tick |

**Example:**
```c
sc_start SC_STONE, 60000, 1;
```

---

### SC_FREEZE

**Effect:** DEF -50%; FLEE = 0; MDEF +25%; ignore Steal, Lex Aeterna, Storm Gust, Falling Ice Pillar; change element to Water Lv 1; can't move/attack/pick item/use item/sit/logout

**Example:**
```c
sc_start SC_FREEZE, 60000, 1;
```

---

### SC_STUN

**Effect:** FLEE = 0; can't move/attack/pick item/use item/use skill/sit/logout

**Example:**
```c
sc_start SC_STUN, 60000, 1;
```

---

### SC_SLEEP

**Effect:** FLEE = 0; enemy CRIT x2; can't move/attack/pick item/use item/use skill/sit/logout

**Example:**
```c
sc_start SC_SLEEP, 60000, 1;
```

---

### SC_POISON

**Effect:** DEF -25%; if HP>25% lose 1.5% + 2 HP/sec; SP Regeneration is disabled

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Level |
| val2 | Caster's object ID |
| val4 | Remaining tick |

**Example:**
```c
sc_start SC_POISON, 60000, 10;  // 60 seconds
```

---

### SC_CURSE

**Effect:** ATK-25%; LUK = 0; Movement speed -300

**Example:**
```c
sc_start SC_CURSE, 60000, 1;
```

---

### SC_SILENCE

**Effect:** Can't use active skills

**Example:**
```c
sc_start SC_SILENCE, 60000, 1;
```

---

### SC_CONFUSION

**Effect:** Move randomly; Set DEF to (STR+(INT*50))

**Example:**
```c
sc_start SC_CONFUSION, 60000, 1;
```

---

### SC_BLIND

**Effect:** HIT -25%; FLEE -25%; Black out the outter part of the screen

**Example:**
```c
sc_start SC_BLIND, 60000, 1;
```

---

### SC_BLEEDING

**Icon:** `EFST_BLOODING`

**Effect:** HP Regeneration is disabled; SP Regeneration is disabled; Lose HP overtime

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Level |
| val2 | Caster's object ID (for mob_log_damage) |
| val4 | Remaining tick |

**Example:**
```c
sc_start SC_BLEEDING, 60000, 10;  // 60 seconds
```

---

### SC_DPOISON

**Effect:** DEF -25%; if HP>25% lose 10/15% HP/sec

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Level |
| val2 | Caster's object ID (for mob_log_damage) |
| val4 | Remaining tick |

**Example:**
```c
sc_start SC_DPOISON, 60000, 10;  // 60 seconds
```

---

### SC_ENCPOISON

**Icon:** `EFST_ENCHANTPOISON`

**Effect:** Change weapon element to ELE_POISON; Poisoning chance is (2.5+0.5%)

**Example:**
```c
sc_start SC_ENCPOISON, 60000, 1;
```

---

### SC_POISONREACT

**Icon:** `EFST_POISONREACT`

**Effect:** Blocks poison attacks; Increases damage by (30*Skill Lv)% after block; Counters non-poison attacks with Envenom 5 autocast

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill level |
| val2 | Number of Envenom autocasts |
| val3 | Chance to autocast Envenom on hit / Poison chance after block |
| val4 | 0=Poison Block Mode; 1=Damage Boost Mode |

**Example:**
```c
sc_start SC_POISONREACT, 60000, 10;  // 60 seconds
```

---

### SC_SLOWPOISON

**Icon:** `EFST_SLOWPOISON`

**Effect:** Stop the HP reduction of SC_POISON

**Example:**
```c
sc_start SC_SLOWPOISON, 60000, 1;
```

---

### SC_FEAR

**Effect:** Cause SC_ANKLE for 2 seconds, Hit/Flee -20%, remove blind, immune to blind

**Example:**
```c
sc_start SC_FEAR, 60000, 1;
```

---

### SC_BURNING

**Icon:** `EFST_BURNT`

**Effect:** MDEF -25%; Deals fixed (1000 + 3%*MaxHP) damage every 3 seconds; Damage can not be reduced

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Level |
| val2 | 1000 |
| val3 | Caster's object ID (for mob_log_damage) |
| val4 | Remaining tick |

**Example:**
```c
sc_start SC_BURNING, 60000, 10;  // 60 seconds
```

---

### SC_FREEZING

**Example:**
```c
sc_start SC_FREEZING, 60000, 1;
```

---

### SC_STONEHARDSKIN

**Example:**
```c
sc_start SC_STONEHARDSKIN, 60000, 1;
```

---

### SC_FREEZE_SP

**Example:**
```c
sc_start SC_FREEZE_SP, 60000, 1;
```

---

### SC_FEARBREEZE

**Example:**
```c
sc_start SC_FEARBREEZE, 60000, 1;
```

---

### SC_POISONINGWEAPON

**Icon:** `EFST_POISONINGWEAPON`

**Effect:** Coat the user's equipped weapon with a new poison temporarily, which grants a chance of leaving the target infected with the current poison while physically attacking.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val2 | Poison Type |
| val3 | Success Rate |
| val4 | Caster's object ID (for mob_log_damage) |

**Example:**
```c
sc_start SC_POISONINGWEAPON, 60000, 10;  // 60 seconds
```

---

### SC_OBLIVIONCURSE

**Icon:** `EFST_OBLIVIONCURSE`

**Effect:** Force the affected entity to use /? emote, block SP Recovery and cause Oblivion status; There is a chance (100% - (Target INT * 0.8)%) of being inflicted, with a minimum of 5%

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val4 | Tick |

**Example:**
```c
sc_start SC_OBLIVIONCURSE, 60000, 10;  // 60 seconds
```

---

### SC_DEEPSLEEP

**Example:**
```c
sc_start SC_DEEPSLEEP, 60000, 1;
```

---

### SC_CURSEDCIRCLE_ATKER

**Example:**
```c
sc_start SC_CURSEDCIRCLE_ATKER, 60000, 1;
```

---

### SC_CURSEDCIRCLE_TARGET

**Example:**
```c
sc_start SC_CURSEDCIRCLE_TARGET, 60000, 1;
```

---

### SC_STONE_SHIELD

**Example:**
```c
sc_start SC_STONE_SHIELD, 60000, 1;
```

---

### SC_STONE_SHIELD_OPTION

**Example:**
```c
sc_start SC_STONE_SHIELD_OPTION, 60000, 1;
```

---

### SC_CURSED_SOIL

**Example:**
```c
sc_start SC_CURSED_SOIL, 60000, 1;
```

---

### SC_CURSED_SOIL_OPTION

**Example:**
```c
sc_start SC_CURSED_SOIL_OPTION, 60000, 1;
```

---

### SC_GVG_STUN

**Icon:** `EFST_GVG_STUN`

**Effect:** Instantly consumes HP/SP, immunizes you against Stun.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |

**Example:**
```c
sc_start SC_GVG_STUN, 60000, 10;  // 60 seconds
```

---

### SC_GVG_STONE

**Icon:** `EFST_GVG_STONE`

**Effect:** Instantly consumes HP/SP, immunizes you against Petrification.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |

**Example:**
```c
sc_start SC_GVG_STONE, 60000, 10;  // 60 seconds
```

---

### SC_GVG_SLEEP

**Icon:** `EFST_GVG_SLEEP`

**Effect:** Instantly consumes HP/SP, immunizes you against Sleep.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |

**Example:**
```c
sc_start SC_GVG_SLEEP, 60000, 10;  // 60 seconds
```

---

### SC_GVG_CURSE

**Icon:** `EFST_GVG_CURSE`

**Effect:** Instantly consumes HP/SP, immunizes you against Curse.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |

**Example:**
```c
sc_start SC_GVG_CURSE, 60000, 10;  // 60 seconds
```

---

### SC_GVG_SILENCE

**Icon:** `EFST_GVG_SILENCE`

**Effect:** Instantly consumes HP/SP, immunizes you against Silence.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |

**Example:**
```c
sc_start SC_GVG_SILENCE, 60000, 10;  // 60 seconds
```

---

### SC_GVG_BLIND

**Icon:** `EFST_GVG_BLIND`

**Effect:** Instantly consumes HP/SP, immunizes you against Blind.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |

**Example:**
```c
sc_start SC_GVG_BLIND, 60000, 10;  // 60 seconds
```

---

### SC_MAGIC_POISON

**Icon:** `EFST_MAGIC_POISON`

**Effect:** Decreases resistance against all elemental attacks by 50%.

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | Attribute Reduction (50, hardcoded). |

**Example:**
```c
sc_start SC_MAGIC_POISON, 60000, 1;
```

---

## Buff Effects

<!-- RAG_CHUNK: sc_buff_effects -->

### SC_ENDURE

**Icon:** `EFST_ENDURE`

**Effect:** Increase MDEF by (Skill Lv); Doesn't get flinched when attacked

**Example:**
```c
sc_start SC_ENDURE, 60000, 1;
```

---

### SC_ANGELUS

**Icon:** `EFST_ANGELUS`

**Effect:** Increase DEF by (5*Skill Lv)%

**Example:**
```c
sc_start SC_ANGELUS, 60000, 1;
```

---

### SC_BLESSING

**Icon:** `EFST_BLESSING`

**Effect:** Increase STR, DEX & INT by (Skill Lv); Removes Stone and Curse status. If used on mobs will reduce their DEX and INT by 50%

**Example:**
```c
sc_start SC_BLESSING, 60000, 1;
```

---

### SC_INCREASEAGI

**Icon:** `EFST_INC_AGI`

**Effect:** Increase AGI and walkspeed, AL_INCAGI effect

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | (hardcoded) |

**Example:**
```c
sc_start SC_INCREASEAGI, 60000, 10;  // 60 seconds
```

---

### SC_IMPOSITIO

**Icon:** `EFST_IMPOSITIO`

**Effect:** Increase ATK by (5*Skill Lv)

**Example:**
```c
sc_start SC_IMPOSITIO, 60000, 1;
```

---

### SC_ASPERSIO

**Icon:** `EFST_ASPERSIO`

**Effect:** Change weapon element to ELE_HOLY

**Example:**
```c
sc_start SC_ASPERSIO, 60000, 1;
```

---

### SC_KYRIE

**Icon:** `EFST_KYRIE`

**Effect:** Remove SC_ASSUMPTIO skill effect; Block damage with a total of (MaxHP*(Skill Lv*2+10)/100) or ((Skill Lv/2)+5) times

**Example:**
```c
sc_start SC_KYRIE, 60000, 1;
```

---

### SC_MAGNIFICAT

**Icon:** `EFST_MAGNIFICAT`

**Effect:** SP Regeneration speed x2

**Example:**
```c
sc_start SC_MAGNIFICAT, 60000, 1;
```

---

### SC_GLORIA

**Icon:** `EFST_GLORIA`

**Effect:** LUK +30

**Example:**
```c
sc_start SC_GLORIA, 60000, 1;
```

---

### SC_AUTOGUARD

**Icon:** `EFST_AUTOGUARD`

**Effect:** Blocks short and long range physical attacks at a certain chance, and stops the caster for 0.3 seconds if it's activated

**Example:**
```c
sc_start SC_AUTOGUARD, 60000, 1;
```

---

### SC_CONCENTRATION

**Icon:** `EFST_LKCONCENTRATION`

**Effect:** Lv 1 Endurace effect; +WATK; +HIT; -DEF

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | 5*val1;		// Batk/Watk Increase |
| val3 | 10*val1;	// Hit Increase |
| val4 | 5*val1;		// Def reduction |

**Example:**
```c
sc_start SC_CONCENTRATION, 60000, 1;
```

---

### SC_SHRIMPBLESSING

**Icon:** `EFST_PROTECTIONOFSHRIMP`

**Effect:** Increases caster's SP recovery by 150%.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |

**Example:**
```c
sc_start SC_SHRIMPBLESSING, 60000, 10;  // 60 seconds
```

---

## Skill Effects

<!-- RAG_CHUNK: sc_skill_effects -->

### SC_PROVOKE

**Icon:** `EFST_PROVOKE`

**Effect:** Decrease DEF by (5+(5*Skill Lv))%; Increase ATK by (2+(3*Skill lv))%

**Example:**
```c
sc_start SC_PROVOKE, 60000, 1;
```

---

### SC_TWOHANDQUICKEN

**Icon:** `EFST_TWOHANDQUICKEN`

**Effect:** ASPD +30%

**Example:**
```c
sc_start SC_TWOHANDQUICKEN, 60000, 1;
```

---

### SC_CONCENTRATE

**Icon:** `EFST_CONCENTRATION`

**Effect:** Increase AGI by (2+Skill Lv)%; Increase DEX by (2+Skill Lv)%; Reveal hidden enemies in 3x3 area around caster

**Example:**
```c
sc_start SC_CONCENTRATE, 60000, 1;
```

---

### SC_HIDING

**Icon:** `EFST_HIDING`

**Effect:** Set OPTION_HIDE

**Example:**
```c
sc_start SC_HIDING, 60000, 1;
```

---

### SC_CLOAKING

**Icon:** `EFST_CLOAKING`

**Effect:** Set OPTION_CLOAK

**Example:**
```c
sc_start SC_CLOAKING, 60000, 1;
```

---

### SC_QUAGMIRE

**Icon:** `EFST_QUAGMIRE`

**Effect:** Removes Increase AGI, Twhohand Quicken, Wind Walk, Adrenaline Rush, Attention Concentrate, Cart Boost, True Sight, Magnetic Field & Onehand Quicken skill effect; Movement Speed -50; Decrease AGI & DEX by (10*Skill Lv) but can't below 75% for players and 50% for mobs

**Example:**
```c
sc_start SC_QUAGMIRE, 60000, 1;
```

---

### SC_SIGNUMCRUCIS

**Icon:** `EFST_CRUCIS`

**Effect:** Decrease DEF of Undead and Demon mobs by (10+(4*Skill Lv))% on screen

**Example:**
```c
sc_start SC_SIGNUMCRUCIS, 60000, 1;
```

---

### SC_DECREASEAGI

**Icon:** `EFST_DEC_AGI`

**Effect:** Decrease AGI and walkspeed, AL_DECAGI effect

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | (hardcoded) |

**Example:**
```c
sc_start SC_DECREASEAGI, 60000, 10;  // 60 seconds
```

---

### SC_SUFFRAGIUM

**Icon:** `EFST_SUFFRAGIUM`

**Effect:** Cast time decreased by (15*Skill Lv)%

**Example:**
```c
sc_start SC_SUFFRAGIUM, 60000, 1;
```

---

### SC_BENEDICTIO

**Icon:** `EFST_BENEDICTIO`

**Effect:** Change armor element to ELE_HOLY

**Example:**
```c
sc_start SC_BENEDICTIO, 60000, 1;
```

---

### SC_AETERNA

**Icon:** `EFST_LEXAETERNA`

**Effect:** Damaged received x2

**Example:**
```c
sc_start SC_AETERNA, 60000, 1;
```

---

### SC_ADRENALINE

**Icon:** `EFST_ADRENALINE`

**Effect:** ASPD of Axe & Mace weapons x2

**Example:**
```c
sc_start SC_ADRENALINE, 60000, 1;
```

---

### SC_WEAPONPERFECTION

**Icon:** `EFST_WEAPONPERFECT`

**Effect:** Ignore damage reduction to any monster size

**Example:**
```c
sc_start SC_WEAPONPERFECTION, 60000, 1;
```

---

### SC_OVERTHRUST

**Icon:** `EFST_OVERTHRUST`

**Effect:** Increase ATK by (5*Skill Lv)%; Add a 0.1% of breaking the equipped weapon [except Axes, Maces & Unbreakable weapons]

**Example:**
```c
sc_start SC_OVERTHRUST, 60000, 1;
```

---

### SC_MAXIMIZEPOWER

**Icon:** `EFST_MAXIMIZE`

**Effect:** SP Regeneration is disabled; Damage dealt is always the max damage

**Example:**
```c
sc_start SC_MAXIMIZEPOWER, 60000, 1;
```

---

### SC_TRICKDEAD

**Icon:** `EFST_TRICKDEAD`

**Effect:** HP & SP Regeneration is disabled; Remove SC_DANCING

**Example:**
```c
sc_start SC_TRICKDEAD, 60000, 1;
```

---

### SC_LOUD

**Icon:** `EFST_SHOUT`

**Effect:** STR +4

**Example:**
```c
sc_start SC_LOUD, 60000, 1;
```

---

### SC_ENERGYCOAT

**Icon:** `EFST_ENERGYCOAT`

**Effect:** Reduce damage received according to current MaxSP %

**Example:**
```c
sc_start SC_ENERGYCOAT, 60000, 1;
```

---

### SC_BROKENARMOR

**Icon:** `EFST_BROKENARMOR`

**Effect:** Shows EFST_BROKENARMOR status icon if the armor is broken

**Example:**
```c
sc_start SC_BROKENARMOR, 60000, 1;
```

---

### SC_BROKENWEAPON

**Icon:** `EFST_BROKENWEAPON`

**Effect:** Shows EFST_BROKENWEAPON status icon if the armor is broken

**Example:**
```c
sc_start SC_BROKENWEAPON, 60000, 1;
```

---

### SC_HALLUCINATION

**Icon:** `EFST_ILLUSION`

**Effect:** The screen goes wavy and you see crazy numbers for all damage that is processed around you, but they are all fake. Even other players see those numbers at you.

**Example:**
```c
sc_start SC_HALLUCINATION, 60000, 1;
```

---

### SC_WEIGHT50

**Icon:** `EFST_WEIGHTOVER50`

**Effect:** Shows EFST_WEIGHTOVER50 status icon if Weight >= 50%

**Example:**
```c
sc_start SC_WEIGHT50, 60000, 1;
```

---

### SC_WEIGHT90

**Icon:** `EFST_WEIGHTOVER90`

**Effect:** Shows EFST_WEIGHTOVER90 status icon if Weight >= 90%

**Example:**
```c
sc_start SC_WEIGHT90, 60000, 1;
```

---

### SC_SPEEDUP0

**Icon:** `EFST_MOVHASTE_HORSE`

**Effect:** Increase/change walkspeed rate. This effect won't be stacked with bonus bSpeedRate

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Walkspeed |

**Example:**
```c
sc_start SC_SPEEDUP0, 60000, 10;  // 60 seconds
```

---

### SC_SPEEDUP1

**Icon:** `EFST_MOVHASTE_POTION`

**Effect:** Increase/change walkspeed rate. This effect won't be stacked with bonus bSpeedRate

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Walkspeed |

**Example:**
```c
sc_start SC_SPEEDUP1, 60000, 10;  // 60 seconds
```

---

### SC_WEDDING

**Effect:** Set Movement Speed to 100; Call clif_changelook; Set OPTION_WEDDING

**Example:**
```c
sc_start SC_WEDDING, 60000, 1;
```

---

### SC_SLOWDOWN

**Effect:** Reduce walkspeed rate

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | -% Walkspeed |

**Example:**
```c
sc_start SC_SLOWDOWN, 60000, 10;  // 60 seconds
```

---

### SC_ANKLE

**Icon:** `EFST_ANKLESNARE`

**Effect:** Set DEF to (AGI*50); Can't move

**Example:**
```c
sc_start SC_ANKLE, 60000, 1;
```

---

### SC_KEEPING

**Effect:** Set DEF to 90

**Example:**
```c
sc_start SC_KEEPING, 60000, 1;
```

---

### SC_BARRIER

**Icon:** `EFST_BARRIER`

**Effect:** Set DEF to 100

**Example:**
```c
sc_start SC_BARRIER, 60000, 1;
```

---

### SC_STRIPWEAPON

**Icon:** `EFST_NOEQUIPWEAPON`

**Effect:** Unequip weapon; On mob ATK -25%

**Example:**
```c
sc_start SC_STRIPWEAPON, 60000, 1;
```

---

### SC_STRIPSHIELD

**Icon:** `EFST_NOEQUIPSHIELD`

**Effect:** Unequip shield; On mob DEF -15%

**Example:**
```c
sc_start SC_STRIPSHIELD, 60000, 1;
```

---

### SC_STRIPARMOR

**Icon:** `EFST_NOEQUIPARMOR`

**Effect:** Unequip armor; On mob VIT -40%

**Example:**
```c
sc_start SC_STRIPARMOR, 60000, 1;
```

---

### SC_STRIPHELM

**Icon:** `EFST_NOEQUIPHELM`

**Effect:** Unequip helm; On mob INT -40%

**Example:**
```c
sc_start SC_STRIPHELM, 60000, 1;
```

---

### SC_CP_WEAPON

**Icon:** `EFST_PROTECTWEAPON`

**Effect:** Protects equipped weapon from damage and strip skill

**Example:**
```c
sc_start SC_CP_WEAPON, 60000, 1;
```

---

### SC_CP_SHIELD

**Icon:** `EFST_PROTECTSHIELD`

**Effect:** Protects equipped shield from damage and strip skill

**Example:**
```c
sc_start SC_CP_SHIELD, 60000, 1;
```

---

### SC_CP_ARMOR

**Icon:** `EFST_PROTECTARMOR`

**Effect:** Protects equipped armor from damage and strip skill

**Example:**
```c
sc_start SC_CP_ARMOR, 60000, 1;
```

---

### SC_CP_HELM

**Icon:** `EFST_PROTECTHELM`

**Effect:** Protects equipped helm from damage and strip skill

**Example:**
```c
sc_start SC_CP_HELM, 60000, 1;
```

---

### SC_REFLECTSHIELD

**Icon:** `EFST_REFLECTSHIELD`

**Effect:** Reflects (10+(3*Skill Lv))% of short ranged physical attack back to the attacker

**Example:**
```c
sc_start SC_REFLECTSHIELD, 60000, 1;
```

---

### SC_SPLASHER

**Icon:** `EFST_SPLASHER`

**Effect:** This skill will only work once the target's HP is 1/3 or less of its Max HP. When struck by this skill, the target will explode and damage other enemies in it's vicinity

**Example:**
```c
sc_start SC_SPLASHER, 60000, 1;
```

---

### SC_PROVIDENCE

**Icon:** `EFST_PROVIDENCE`

**Effect:** Increase party members' resistance to RC_Demon and Ele_Holy monsters

**Example:**
```c
sc_start SC_PROVIDENCE, 60000, 1;
```

---

### SC_DEFENDER

**Icon:** `EFST_DEFENDER`

**Effect:** Decrease (5+(15*Skill Lv))% damage taken from long range attack; Decrease (25+(5*Skill Lv)) ASPD

**Example:**
```c
sc_start SC_DEFENDER, 60000, 1;
```

---

### SC_MAGICROD

**Icon:** `EFST_MAGICROD`

**Effect:** Gain (Skill Lv*20)% of SP consumed by the skill used from enemy; Damage received becomes 0; Drain 20% of enemy's Max SP

**Example:**
```c
sc_start SC_MAGICROD, 60000, 1;
```

---

### SC_SPELLBREAKER

**Effect:** Gain SP used by enemy to cast the spell, and interrupt the magic cast. At lv 5, gain 1% from enemy max hp.

**Example:**
```c
sc_start SC_SPELLBREAKER, 60000, 1;
```

---

### SC_AUTOSPELL

**Icon:** `EFST_AUTOSPELL`

**Effect:** Auto cast several learned magic spells by using 2/3 of SP cost of the skill, but only when attacking with physical attacks.

**Example:**
```c
sc_start SC_AUTOSPELL, 60000, 1;
```

---

### SC_SIGHTTRASHER

**Effect:** (not exist)

**Example:**
```c
sc_start SC_SIGHTTRASHER, 60000, 1;
```

---

### SC_AUTOBERSERK

**Icon:** `EFST_AUTOBERSERK`

**Effect:** If HP<25%, set SC_PROVOKE lv 10 on self

**Example:**
```c
sc_start SC_AUTOBERSERK, 60000, 1;
```

---

### SC_SPEARQUICKEN

**Icon:** `EFST_SPEARQUICKEN`

**Effect:** When using spear, +ASPD (20+(1*Skill Lv))%, +CRIT (3+(10*Skill Lv)), +FLEE (2*Skill Lv)

**Example:**
```c
sc_start SC_SPEARQUICKEN, 60000, 1;
```

---

### SC_AUTOCOUNTER

**Icon:** `EFST_AUTOCOUNTER`

**Effect:** Hitrate +20%; If attacked by close range, automatically retaliate with crit*2

**Example:**
```c
sc_start SC_AUTOCOUNTER, 60000, 1;
```

---

### SC_SIGHT

**Effect:** Reveal hidden enemy on 3*3 range; Set OPTION_SIGHT

**Example:**
```c
sc_start SC_SIGHT, 60000, 1;
```

---

### SC_SAFETYWALL

**Effect:** Block short ranged attack; Set OPTION_RUWACH

**Example:**
```c
sc_start SC_SAFETYWALL, 60000, 1;
```

---

### SC_RUWACH

**Effect:** Reveal hidden target and deal little damages if enemy is under SC_HIDING/SC_CLOAKING/SC_CAMOUFLAGE/SC_CLOAKINGEXCEED; Set OPTION_RUWACH

**Example:**
```c
sc_start SC_RUWACH, 60000, 1;
```

---

### SC_EXTREMITYFIST

**Icon:** `EFST_EXTREMITYFIST`

**Effect:** Stop SP Regeneration by setting RGN_SP

**Example:**
```c
sc_start SC_EXTREMITYFIST, 60000, 1;
```

---

### SC_EXPLOSIONSPIRITS

**Icon:** `EFST_EXPLOSIONSPIRITS`

**Effect:** Stop SP Regeneration by setting RGN_SP; +Crit

**Example:**
```c
sc_start SC_EXPLOSIONSPIRITS, 60000, 1;
```

---

### SC_COMBO

**Example:**
```c
sc_start SC_COMBO, 60000, 1;
```

---

### SC_BLADESTOP_WAIT

**Example:**
```c
sc_start SC_BLADESTOP_WAIT, 60000, 1;
```

---

### SC_BLADESTOP

**Icon:** `EFST_BLADESTOP`

**Effect:** Stops player and target; Set OPT3_BLADESTOP

**Example:**
```c
sc_start SC_BLADESTOP, 60000, 1;
```

---

### SC_FIREWEAPON

**Icon:** `EFST_PROPERTYFIRE`

**Effect:** Change weapon element to Fire element

**Example:**
```c
sc_start SC_FIREWEAPON, 60000, 1;
```

---

### SC_WATERWEAPON

**Icon:** `EFST_PROPERTYWATER`

**Effect:** Change weapon element to Water element

**Example:**
```c
sc_start SC_WATERWEAPON, 60000, 1;
```

---

### SC_WINDWEAPON

**Icon:** `EFST_PROPERTYWIND`

**Effect:** Change weapon element to Wind element

**Example:**
```c
sc_start SC_WINDWEAPON, 60000, 1;
```

---

### SC_EARTHWEAPON

**Icon:** `EFST_PROPERTYGROUND`

**Effect:** Change weapon element to Earth element

**Example:**
```c
sc_start SC_EARTHWEAPON, 60000, 1;
```

---

### SC_VOLCANO

**Icon:** `EFST_GROUNDMAGIC`

**Effect:** +watk of ELE_FIRE user

**Example:**
```c
sc_start SC_VOLCANO, 60000, 1;
```

---

### SC_DELUGE

**Icon:** `EFST_GROUNDMAGIC`

**Effect:** +Max HP of ELE_WATER user

**Example:**
```c
sc_start SC_DELUGE, 60000, 1;
```

---

### SC_VIOLENTGALE

**Icon:** `EFST_GROUNDMAGIC`

**Effect:** +FLEE of ELE_WIND user

**Example:**
```c
sc_start SC_VIOLENTGALE, 60000, 1;
```

---

### SC_WATK_ELEMENT

**Effect:** Adds a percent of damage as an element

**Example:**
```c
sc_start SC_WATK_ELEMENT, 60000, 1;
```

---

### SC_ARMOR

**Effect:** Reduce damage received by 80 from long ranged weapon/misc attacks

**Example:**
```c
sc_start SC_ARMOR, 60000, 1;
```

---

### SC_ARMOR_ELEMENT

**Effect:** Adjust element resistance by percentage

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Water resistance |
| val2 | Earth resistance |
| val3 | Fire resistance |
| val4 | Wind resistance |

**Example:**
```c
sc_start SC_ARMOR_ELEMENT, 60000, 10;  // 60 seconds
```

---

### SC_NOCHAT

**Effect:** Can't chat, pick item, drop item

**Example:**
```c
sc_start SC_NOCHAT, 60000, 1;
```

---

### SC_BABY

**Icon:** `EFST_PROTECTEXP`

**Example:**
```c
sc_start SC_BABY, 60000, 1;
```

---

### SC_AURABLADE

**Icon:** `EFST_AURABLADE`

**Effect:** Set OPT3_AURABLADE; Add damage by (20*Skill Lv) which ignore caster's accuracy rate/target's DEF

**Example:**
```c
sc_start SC_AURABLADE, 60000, 1;
```

---

### SC_PARRYING

**Icon:** `EFST_PARRYING`

**Effect:** Block using a 2H-Sword with chance (20+(3*Skill Lv))%

**Example:**
```c
sc_start SC_PARRYING, 60000, 1;
```

---

### SC_TENSIONRELAX

**Icon:** `EFST_TENSIONRELAX`

**Effect:** Increase HP regeneration rate while sitting

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | 12;		// SP cost |
| val3 | tick/val4; |
| val4 | 10000;	// Decrease at 10secs intervals. |

**Example:**
```c
sc_start SC_TENSIONRELAX, 60000, 1;
```

---

### SC_BERSERK

**Icon:** `EFST_BERSERK`

**Effect:** Stop HP+SP Regen; Can't use skill; Can't chat; -FLEE; +Max HP; +Movement Speed; +ATK; Set OPT3_BERSERK; -5%HP per 10 second; Set DEF+MDEF to 0

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | HP Penalty (5% of Max HP) |
| val3 | Skill duration |
| val4 | Interval of HP Penalty |

**Example:**
```c
sc_start SC_BERSERK, 60000, 1;
```

---

### SC_FURY

**Example:**
```c
sc_start SC_FURY, 60000, 1;
```

---

### SC_GOSPEL

**Icon:** `EFST_GOSPEL`

**Effect:** Can't move; Gives a random status to party member and also enemy.

**Example:**
```c
sc_start SC_GOSPEL, 60000, 1;
```

---

### SC_ASSUMPTIO

**Icon:** `RE: EFST_ASSUMPTIO2. Pre-RE: EFST_ASSUMPTIO`

**Effect:** HP_ASSUMPTIO's effect

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Level // * 2 Bonus heal % (in RENEWAL) |

**Example:**
```c
sc_start SC_ASSUMPTIO, 60000, 10;  // 60 seconds
```

---

### SC_BASILICA

**Effect:** Can't move; Can't use skill except the Basilica caster to cancel the basilica itself; Clear the skill area; Knockback enemy except Boss

**Example:**
```c
sc_start SC_BASILICA, 60000, 1;
```

---

### SC_GUILDAURA

**Example:**
```c
sc_start SC_GUILDAURA, 60000, 1;
```

---

### SC_MAGICPOWER

**Icon:** `EFST_MAGICPOWER`

**Effect:** +MATK by (Skill Lv*5)% for the next magic skill that is cast

**Example:**
```c
sc_start SC_MAGICPOWER, 60000, 1;
```

---

### SC_EDP

**Icon:** `EFST_EDP`

**Effect:** +WATK by (100+(Skill Lv*80))

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |
| val2 | Chance to Poison enemy (val1+2)% |
| val3 | Damage increased by (50*(val1+1)) |

**Example:**
```c
sc_start SC_EDP, 60000, 10;  // 60 seconds
```

---

### SC_TRUESIGHT

**Icon:** `EFST_TRUESIGHT`

**Effect:** All stat +5; Damage +(2*Skill Lv)%; Crit +(Skill Lv); Hit +(3*Skill Lv)%

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |
| val2 | Crit |
| val3 | Hit |

**Example:**
```c
sc_start SC_TRUESIGHT, 60000, 10;  // 60 seconds
```

---

### SC_WINDWALK

**Icon:** `EFST_WINDWALK`

**Effect:** +Flee; +Movement speed

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |
| val2 | Flee |

**Example:**
```c
sc_start SC_WINDWALK, 60000, 10;  // 60 seconds
```

---

### SC_MELTDOWN

**Icon:** `EFST_MELTDOWN`

**Effect:** Breaks target's weapon and armor at a certain chance

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |
| val2 | Chance to break weapon (100*Skill Lv) |
| val3 | Change to break armor (70*Skill Lv) |

**Example:**
```c
sc_start SC_MELTDOWN, 60000, 10;  // 60 seconds
```

---

### SC_CHASEWALK

**Icon:** `EFST_CHASEWALK`

**Example:**
```c
sc_start SC_CHASEWALK, 60000, 1;
```

---

### SC_REJECTSWORD

**Icon:** `EFST_SWORDREJECT`

**Example:**
```c
sc_start SC_REJECTSWORD, 60000, 1;
```

---

### SC_MARIONETTE

**Icon:** `EFST_MARIONETTE_MASTER`

**Example:**
```c
sc_start SC_MARIONETTE, 60000, 1;
```

---

### SC_MARIONETTE2

**Icon:** `EFST_MARIONETTE`

**Example:**
```c
sc_start SC_MARIONETTE2, 60000, 1;
```

---

### SC_CHANGEUNDEAD

**Example:**
```c
sc_start SC_CHANGEUNDEAD, 60000, 1;
```

---

### SC_JOINTBEAT

**Example:**
```c
sc_start SC_JOINTBEAT, 60000, 1;
```

---

### SC_MINDBREAKER

**Icon:** `EFST_MINDBREAKER`

**Example:**
```c
sc_start SC_MINDBREAKER, 60000, 1;
```

---

### SC_MEMORIZE

**Icon:** `EFST_MEMORIZE`

**Example:**
```c
sc_start SC_MEMORIZE, 60000, 1;
```

---

### SC_FOGWALL

**Icon:** `EFST_FOGWALL`

**Example:**
```c
sc_start SC_FOGWALL, 60000, 1;
```

---

### SC_SPIDERWEB

**Icon:** `EFST_SPIDERWEB`

**Example:**
```c
sc_start SC_SPIDERWEB, 60000, 1;
```

---

### SC_DEVOTION

**Icon:** `EFST_DEVOTION`

**Example:**
```c
sc_start SC_DEVOTION, 60000, 1;
```

---

### SC_SACRIFICE

**Example:**
```c
sc_start SC_SACRIFICE, 60000, 1;
```

---

### SC_STEELBODY

**Example:**
```c
sc_start SC_STEELBODY, 60000, 1;
```

---

### SC_ORCISH

**Example:**
```c
sc_start SC_ORCISH, 60000, 1;
```

---

### SC_READYSTORM

**Example:**
```c
sc_start SC_READYSTORM, 60000, 1;
```

---

### SC_READYDOWN

**Example:**
```c
sc_start SC_READYDOWN, 60000, 1;
```

---

### SC_READYTURN

**Example:**
```c
sc_start SC_READYTURN, 60000, 1;
```

---

### SC_READYCOUNTER

**Example:**
```c
sc_start SC_READYCOUNTER, 60000, 1;
```

---

### SC_DODGE

**Example:**
```c
sc_start SC_DODGE, 60000, 1;
```

---

### SC_RUN

**Example:**
```c
sc_start SC_RUN, 60000, 1;
```

---

### SC_SHADOWWEAPON

**Example:**
```c
sc_start SC_SHADOWWEAPON, 60000, 1;
```

---

### SC_ADRENALINE2

**Example:**
```c
sc_start SC_ADRENALINE2, 60000, 1;
```

---

### SC_GHOSTWEAPON

**Example:**
```c
sc_start SC_GHOSTWEAPON, 60000, 1;
```

---

### SC_KAIZEL

**Example:**
```c
sc_start SC_KAIZEL, 60000, 1;
```

---

### SC_KAAHI

**Example:**
```c
sc_start SC_KAAHI, 60000, 1;
```

---

### SC_KAUPE

**Example:**
```c
sc_start SC_KAUPE, 60000, 1;
```

---

### SC_ONEHAND

**Example:**
```c
sc_start SC_ONEHAND, 60000, 1;
```

---

### SC_PRESERVE

**Example:**
```c
sc_start SC_PRESERVE, 60000, 1;
```

---

### SC_BATTLEORDERS

**Example:**
```c
sc_start SC_BATTLEORDERS, 60000, 1;
```

---

### SC_REGENERATION

**Example:**
```c
sc_start SC_REGENERATION, 60000, 1;
```

---

### SC_DOUBLECAST

**Example:**
```c
sc_start SC_DOUBLECAST, 60000, 1;
```

---

### SC_GRAVITATION

**Example:**
```c
sc_start SC_GRAVITATION, 60000, 1;
```

---

### SC_MAXOVERTHRUST

**Example:**
```c
sc_start SC_MAXOVERTHRUST, 60000, 1;
```

---

### SC_LONGING

**Example:**
```c
sc_start SC_LONGING, 60000, 1;
```

---

### SC_HERMODE

**Example:**
```c
sc_start SC_HERMODE, 60000, 1;
```

---

### SC_SHRINK

**Example:**
```c
sc_start SC_SHRINK, 60000, 1;
```

---

### SC_SIGHTBLASTER

**Example:**
```c
sc_start SC_SIGHTBLASTER, 60000, 1;
```

---

### SC_WINKCHARM

**Icon:** `EFST_DC_WINKCHARM`

**Effect:** Can't cast spells. Can't attack the charmer. Only works on non-players.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill level |
| val2 | ID of the charmer |

**Example:**
```c
sc_start SC_WINKCHARM, 60000, 10;  // 60 seconds
```

---

### SC_CLOSECONFINE

**Icon:** `EFST_RG_CCONFINE_M`

**Effect:** Flee bonus and counter for confined enemies

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill level |
| val2 | Confined enemy count |
| val3 | +50 Flee |

**Example:**
```c
sc_start SC_CLOSECONFINE, 60000, 10;  // 60 seconds
```

---

### SC_CLOSECONFINE2

**Icon:** `EFST_RG_CCONFINE_S`

**Effect:** Confines target in place

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill level |
| val2 | MapID of caster |

**Example:**
```c
sc_start SC_CLOSECONFINE2, 60000, 10;  // 60 seconds
```

---

### SC_DANCING

**Example:**
```c
sc_start SC_DANCING, 60000, 1;
```

---

### SC_ELEMENTALCHANGE

**Icon:** `EFST_ARMOR_PROPERTY`

**Effect:** Change armor element

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Element level |
| val2 | Element (see doc/item_bonus.txt) |

**Example:**
```c
sc_start SC_ELEMENTALCHANGE, 60000, 10;  // 60 seconds
```

---

### SC_RICHMANKIM

**Example:**
```c
sc_start SC_RICHMANKIM, 60000, 1;
```

---

### SC_ETERNALCHAOS

**Example:**
```c
sc_start SC_ETERNALCHAOS, 60000, 1;
```

---

### SC_DRUMBATTLE

**Example:**
```c
sc_start SC_DRUMBATTLE, 60000, 1;
```

---

### SC_NIBELUNGEN

**Example:**
```c
sc_start SC_NIBELUNGEN, 60000, 1;
```

---

### SC_ROKISWEIL

**Example:**
```c
sc_start SC_ROKISWEIL, 60000, 1;
```

---

### SC_INTOABYSS

**Example:**
```c
sc_start SC_INTOABYSS, 60000, 1;
```

---

### SC_SIEGFRIED

**Icon:** `EFST_SIEGFRIED`

**Effect:** Status change for BD_SIEGFRIED

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | BD_SIEGFRIED Skill level |
| val2 | Increase val2% damage reduction from non-Nuetral elemental attack |
| val3 | Increase status resistance value by val3% of player's current resistance. |

**Example:**
```c
sc_start SC_SIEGFRIED, 60000, 10;  // 60 seconds
```

---

### SC_WHISTLE

**Example:**
```c
sc_start SC_WHISTLE, 60000, 1;
```

---

### SC_ASSNCROS

**Example:**
```c
sc_start SC_ASSNCROS, 60000, 1;
```

---

### SC_POEMBRAGI

**Example:**
```c
sc_start SC_POEMBRAGI, 60000, 1;
```

---

### SC_APPLEIDUN

**Example:**
```c
sc_start SC_APPLEIDUN, 60000, 1;
```

---

### SC_MODECHANGE

**Example:**
```c
sc_start SC_MODECHANGE, 60000, 1;
```

---

### SC_HUMMING

**Example:**
```c
sc_start SC_HUMMING, 60000, 1;
```

---

### SC_DONTFORGETME

**Example:**
```c
sc_start SC_DONTFORGETME, 60000, 1;
```

---

### SC_FORTUNE

**Example:**
```c
sc_start SC_FORTUNE, 60000, 1;
```

---

### SC_SERVICE4U

**Example:**
```c
sc_start SC_SERVICE4U, 60000, 1;
```

---

### SC_STOP

**Example:**
```c
sc_start SC_STOP, 60000, 1;
```

---

### SC_SPURT

**Example:**
```c
sc_start SC_SPURT, 60000, 1;
```

---

### SC_SPIRIT

**Example:**
```c
sc_start SC_SPIRIT, 60000, 1;
```

---

### SC_COMA

**Effect:** Vanish HP to 1 and SP to 0

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Level |
| val2 | If 1 means do not remove SP |
| val3 | Caster's object ID (for mob_log_damage) |

**Example:**
```c
sc_start SC_COMA, 60000, 10;  // 60 seconds
```

---

### SC_INTRAVISION

**Example:**
```c
sc_start SC_INTRAVISION, 60000, 1;
```

---

### SC_INCALLSTATUS

**Effect:** Increase all status

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +AllStats |

**Example:**
```c
sc_start SC_INCALLSTATUS, 60000, 10;  // 60 seconds
```

---

### SC_INCSTR

**Effect:** Increase STR

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + STR |

**Example:**
```c
sc_start SC_INCSTR, 60000, 10;  // 60 seconds
```

---

### SC_INCAGI

**Effect:** Increase AGI

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + AGI |

**Example:**
```c
sc_start SC_INCAGI, 60000, 10;  // 60 seconds
```

---

### SC_INCVIT

**Effect:** Incrase VIT

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + VIT |

**Example:**
```c
sc_start SC_INCVIT, 60000, 10;  // 60 seconds
```

---

### SC_INCINT

**Effect:** Increase INT

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + INT |

**Example:**
```c
sc_start SC_INCINT, 60000, 10;  // 60 seconds
```

---

### SC_INCDEX

**Effect:** Increase DEX

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + DEX |

**Example:**
```c
sc_start SC_INCDEX, 60000, 10;  // 60 seconds
```

---

### SC_INCLUK

**Effect:** Increase LUK

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + Luk |

**Example:**
```c
sc_start SC_INCLUK, 60000, 10;  // 60 seconds
```

---

### SC_INCHIT

**Effect:** Increase Hit

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + Hit |

**Example:**
```c
sc_start SC_INCHIT, 60000, 10;  // 60 seconds
```

---

### SC_INCHITRATE

**Effect:** Incrase Hit

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Hit |

**Example:**
```c
sc_start SC_INCHITRATE, 60000, 10;  // 60 seconds
```

---

### SC_INCFLEE

**Effect:** Increase Flee

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + Flee |

**Example:**
```c
sc_start SC_INCFLEE, 60000, 10;  // 60 seconds
```

---

### SC_INCFLEERATE

**Effect:** Incrase Flee

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Flee |

**Example:**
```c
sc_start SC_INCFLEERATE, 60000, 10;  // 60 seconds
```

---

### SC_INCMHPRATE

**Effect:** Increase MaxHP

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% MaxHP |

**Example:**
```c
sc_start SC_INCMHPRATE, 60000, 10;  // 60 seconds
```

---

### SC_INCMSPRATE

**Effect:** Incrase Max SP

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% MaxSP |

**Example:**
```c
sc_start SC_INCMSPRATE, 60000, 10;  // 60 seconds
```

---

### SC_INCATKRATE

**Effect:** Increase Base Attack

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Atk |

**Example:**
```c
sc_start SC_INCATKRATE, 60000, 10;  // 60 seconds
```

---

### SC_INCMATKRATE

**Effect:** Increase MATK

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Matk |

**Example:**
```c
sc_start SC_INCMATKRATE, 60000, 10;  // 60 seconds
```

---

### SC_INCDEFRATE

**Effect:** Increase Defense

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Def |

**Example:**
```c
sc_start SC_INCDEFRATE, 60000, 10;  // 60 seconds
```

---

### SC_SCRESIST

**Effect:** Status resistance from Gospel skill

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Increase status resistance value by n% of player's current resistance. |

**Example:**
```c
sc_start SC_SCRESIST, 60000, 10;  // 60 seconds
```

---

### SC_XMAS

**Example:**
```c
sc_start SC_XMAS, 60000, 1;
```

---

### SC_WARM

**Example:**
```c
sc_start SC_WARM, 60000, 1;
```

---

### SC_SUN_COMFORT

**Example:**
```c
sc_start SC_SUN_COMFORT, 60000, 1;
```

---

### SC_MOON_COMFORT

**Example:**
```c
sc_start SC_MOON_COMFORT, 60000, 1;
```

---

### SC_STAR_COMFORT

**Example:**
```c
sc_start SC_STAR_COMFORT, 60000, 1;
```

---

### SC_FUSION

**Example:**
```c
sc_start SC_FUSION, 60000, 1;
```

---

### SC_SKILLRATE_UP

**Example:**
```c
sc_start SC_SKILLRATE_UP, 60000, 1;
```

---

### SC_SKE

**Example:**
```c
sc_start SC_SKE, 60000, 1;
```

---

### SC_KAITE

**Example:**
```c
sc_start SC_KAITE, 60000, 1;
```

---

### SC_SWOO

**Example:**
```c
sc_start SC_SWOO, 60000, 1;
```

---

### SC_SKA

**Example:**
```c
sc_start SC_SKA, 60000, 1;
```

---

### SC_EARTHSCROLL

**Example:**
```c
sc_start SC_EARTHSCROLL, 60000, 1;
```

---

### SC_MIRACLE

**Example:**
```c
sc_start SC_MIRACLE, 60000, 1;
```

---

### SC_MADNESSCANCEL

**Icon:** `EFST_GS_MADNESSCANCEL`

**Effect:** Increases some statuses (Base ATK, ASPD)

**Example:**
```c
sc_start SC_MADNESSCANCEL, 60000, 1;
```

---

### SC_ADJUSTMENT

**Icon:** `EFST_GS_ADJUSTMENT`

**Effect:** Increases some statuses (Hit, Flee)

**Example:**
```c
sc_start SC_ADJUSTMENT, 60000, 1;
```

---

### SC_INCREASING

**Icon:** `EFST_GS_ACCURACY`

**Effect:** Increase some statuses (Hit, Dex, Agi), GS_INCREASING effect

**Example:**
```c
sc_start SC_INCREASING, 60000, 1;
```

---

### SC_MAGICALBULLET

**Icon:** `EFST_GS_MAGICAL_BULLET`

**Effect:** Increases damage based on source's MATK and is reduced by target's MDEF

**Example:**
```c
sc_start SC_MAGICALBULLET, 60000, 1;
```

---

### SC_GATLINGFEVER

**Icon:** `EFST_GS_GATLINGFEVER`

**Effect:** Increases some statuses (Base ATK, Flee, Movement Speed, ASPD)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | SkillLv |
| val2 | ASPD increase (20 * val1) |
| val3 | Base ATK (20 + 10 * val1) [pre-renewal] |
| val4 | Flee decrease (5 * val1) |

**Example:**
```c
sc_start SC_GATLINGFEVER, 60000, 10;  // 60 seconds
```

---

### SC_TATAMIGAESHI

**Example:**
```c
sc_start SC_TATAMIGAESHI, 60000, 1;
```

---

### SC_UTSUSEMI

**Example:**
```c
sc_start SC_UTSUSEMI, 60000, 1;
```

---

### SC_BUNSINJYUTSU

**Example:**
```c
sc_start SC_BUNSINJYUTSU, 60000, 1;
```

---

### SC_KAENSIN

**Example:**
```c
sc_start SC_KAENSIN, 60000, 1;
```

---

### SC_SUITON

**Example:**
```c
sc_start SC_SUITON, 60000, 1;
```

---

### SC_NEN

**Example:**
```c
sc_start SC_NEN, 60000, 1;
```

---

### SC_KNOWLEDGE

**Example:**
```c
sc_start SC_KNOWLEDGE, 60000, 1;
```

---

### SC_SMA

**Example:**
```c
sc_start SC_SMA, 60000, 1;
```

---

### SC_FLING

**Example:**
```c
sc_start SC_FLING, 60000, 1;
```

---

### SC_AVOID

**Icon:** `EFST_HLIF_AVOID`

**Effect:** Increase walkspeed for Players and Homunculus

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Level |
| val2 | Walkspeed increase (10 * val1 for Players, 40 * val1 for Homunculus) |

**Example:**
```c
sc_start SC_AVOID, 60000, 10;  // 60 seconds
```

---

### SC_CHANGE

**Icon:** `EFST_HLIF_CHANGE`

**Effect:** Increase some Homunculus' statuses (VIT, INT); Uses MATK for damage calculation; Sets Homunculus' HP and SP to 10 on expiration; On Pre-Renewal, sets Homunculus' HP and SP to 100% on cast

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Level |
| val2 | VIT increase (20 * val1) |
| val3 | INT increase (30 * val1) |

**Example:**
```c
sc_start SC_CHANGE, 60000, 10;  // 60 seconds
```

---

### SC_BLOODLUST

**Icon:** `EFST_HAMI_BLOODLUST`

**Effect:** Increase the homunculus ATK and has a chance to leech HP from the target

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Level |
| val2 | ATK increase (20 + (10 * val1)) |
| val3 | Chance to leech HP (9 * val1)% |
| val4 | Leeched HP percentage 20% |

**Example:**
```c
sc_start SC_BLOODLUST, 60000, 10;  // 60 seconds
```

---

### SC_FLEET

**Example:**
```c
sc_start SC_FLEET, 60000, 1;
```

---

### SC_SPEED

**Example:**
```c
sc_start SC_SPEED, 60000, 1;
```

---

### SC_DEFENCE

**Icon:** `EFST_HAMI_DEFENCE`

**Effect:** Increase VIT and as result VIT-based DEF of the Player and plain VIT of the Homunculus

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Level |
| val2 | VIT increase for players, DEF increase for homunculus (5 + (5 * val1)) [Renewal], (2 * val1) [Pre-Renewal] |

**Example:**
```c
sc_start SC_DEFENCE, 60000, 10;  // 60 seconds
```

---

### SC_INCASPDRATE

**Effect:** Increase ASPD

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% ASPD |

**Example:**
```c
sc_start SC_INCASPDRATE, 60000, 10;  // 60 seconds
```

---

### SC_INCFLEE2

**Icon:** `EFST_PLUSAVOIDVALUE`

**Effect:** Increase perfect flee

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + Flee2 |

**Example:**
```c
sc_start SC_INCFLEE2, 60000, 10;  // 60 seconds
```

---

### SC_JAILED

**Example:**
```c
sc_start SC_JAILED, 60000, 1;
```

---

### SC_ENCHANTARMS

**Icon:** `EFST_WEAPONPROPERTY`

**Effect:** Changes the element of a target's weapon.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Element value from skill_db |

**Example:**
```c
sc_start SC_ENCHANTARMS, 60000, 10;  // 60 seconds
```

---

### SC_MAGICALATTACK

**Example:**
```c
sc_start SC_MAGICALATTACK, 60000, 1;
```

---

### SC_ARMORCHANGE

**Example:**
```c
sc_start SC_ARMORCHANGE, 60000, 1;
```

---

### SC_CRITICALWOUND

**Example:**
```c
sc_start SC_CRITICALWOUND, 60000, 1;
```

---

### SC_MAGICMIRROR

**Example:**
```c
sc_start SC_MAGICMIRROR, 60000, 1;
```

---

### SC_SLOWCAST

**Example:**
```c
sc_start SC_SLOWCAST, 60000, 1;
```

---

### SC_SUMMER

**Example:**
```c
sc_start SC_SUMMER, 60000, 1;
```

---

### SC_BOSSMAPINFO

**Icon:** `EFST_CASH_BOSS_ALARM`

**Effect:** Used to display Boss location on minimap

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Boss game ID |
| val2 | Used to keep timer message from spamming chat window |
| val4 | Remaining tick |

**Example:**
```c
sc_start SC_BOSSMAPINFO, 60000, 10;  // 60 seconds
```

---

### SC_LIFEINSURANCE

**Icon:** `EFST_CASH_DEATHPENALTY`

**Effect:** Remove death pleanlties

**Example:**
```c
sc_start SC_LIFEINSURANCE, 60000, 1;
```

---

### SC_INCCRI

**Icon:** `EFST_FOOD_CRITICALSUCCESSVALUE`

**Effect:** Increase critical value

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + Critical (100% = 1000) |

**Example:**
```c
sc_start SC_INCCRI, 60000, 10;  // 60 seconds
```

---

### SC_INCDEF

**Example:**
```c
sc_start SC_INCDEF, 60000, 1;
```

---

### SC_INCBASEATK

**Example:**
```c
sc_start SC_INCBASEATK, 60000, 1;
```

---

### SC_FASTCAST

**Example:**
```c
sc_start SC_FASTCAST, 60000, 1;
```

---

### SC_MDEF_RATE

**Icon:** `EFST_PROTECT_MDEF`

**Effect:** Increase MDef by %

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Mdef |

**Example:**
```c
sc_start SC_MDEF_RATE, 60000, 10;  // 60 seconds
```

---

### SC_HPREGEN

**Example:**
```c
sc_start SC_HPREGEN, 60000, 1;
```

---

### SC_INCHEALRATE

**Icon:** `EFST_HEALPLUS`

**Effect:** Increase Heal power

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Heal |

**Example:**
```c
sc_start SC_INCHEALRATE, 60000, 10;  // 60 seconds
```

---

### SC_PNEUMA

**Example:**
```c
sc_start SC_PNEUMA, 60000, 1;
```

---

### SC_AUTOTRADE

**Example:**
```c
sc_start SC_AUTOTRADE, 60000, 1;
```

---

### SC_KSPROTECTED

**Example:**
```c
sc_start SC_KSPROTECTED, 60000, 1;
```

---

### SC_ARMOR_RESIST

**Effect:** Adjust element resistance by percentage

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Water resistance |
| val2 | Earth resistance |
| val3 | Fire resistance |
| val4 | Wind resistance |

**Example:**
```c
sc_start SC_ARMOR_RESIST, 60000, 10;  // 60 seconds
```

---

### SC_SPCOST_RATE

**Icon:** `EFST_ATKER_BLOOD`

**Effect:** Reduce SP cost

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Rate |

**Example:**
```c
sc_start SC_SPCOST_RATE, 60000, 10;  // 60 seconds
```

---

### SC_COMMONSC_RESIST

**Icon:** `EFST_TARGET_BLOOD`

**Effect:** Increase resistance of status changes, only againts SC_STONE, SC_FREEZE, SC_STUN, SC_SLEEP, SC_POISON, SC_CURSE, SC_SILENCE, SC_CONFUSION, SC_BLIND, SC_BLEEDING, and SC_DPOISON

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Resistance |

**Example:**
```c
sc_start SC_COMMONSC_RESIST, 60000, 10;  // 60 seconds
```

---

### SC_SEVENWIND

**Example:**
```c
sc_start SC_SEVENWIND, 60000, 1;
```

---

### SC_DEF_RATE

**Icon:** `EFST_PROTECT_DEF`

**Effect:** Increase Def by %

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Def |

**Example:**
```c
sc_start SC_DEF_RATE, 60000, 10;  // 60 seconds
```

---

### SC_SPREGEN

**Example:**
```c
sc_start SC_SPREGEN, 60000, 1;
```

---

### SC_WALKSPEED

**Example:**
```c
sc_start SC_WALKSPEED, 60000, 1;
```

---

### SC_MERC_FLEEUP

**Example:**
```c
sc_start SC_MERC_FLEEUP, 60000, 1;
```

---

### SC_MERC_ATKUP

**Example:**
```c
sc_start SC_MERC_ATKUP, 60000, 1;
```

---

### SC_MERC_HPUP

**Example:**
```c
sc_start SC_MERC_HPUP, 60000, 1;
```

---

### SC_MERC_SPUP

**Example:**
```c
sc_start SC_MERC_SPUP, 60000, 1;
```

---

### SC_MERC_HITUP

**Example:**
```c
sc_start SC_MERC_HITUP, 60000, 1;
```

---

### SC_MERC_QUICKEN

**Example:**
```c
sc_start SC_MERC_QUICKEN, 60000, 1;
```

---

### SC_REBIRTH

**Example:**
```c
sc_start SC_REBIRTH, 60000, 1;
```

---

### SC_SKILLCASTRATE

**Example:**
```c
sc_start SC_SKILLCASTRATE, 60000, 1;
```

---

### SC_DEFRATIOATK

**Example:**
```c
sc_start SC_DEFRATIOATK, 60000, 1;
```

---

### SC_HPDRAIN

**Example:**
```c
sc_start SC_HPDRAIN, 60000, 1;
```

---

### SC_SKILLATKBONUS

**Example:**
```c
sc_start SC_SKILLATKBONUS, 60000, 1;
```

---

### SC_ITEMSCRIPT

**Effect:** Timer script from other item script

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Item ID |
| val2 | Status Icon |

**Example:**
```c
sc_start SC_ITEMSCRIPT, 60000, 10;  // 60 seconds
```

---

### SC_IGNOREDEF

**Example:**
```c
sc_start SC_IGNOREDEF, 60000, 1;
```

---

### SC_HELLPOWER

**Example:**
```c
sc_start SC_HELLPOWER, 60000, 1;
```

---

### SC_INVINCIBLE

**Example:**
```c
sc_start SC_INVINCIBLE, 60000, 1;
```

---

### SC_INVINCIBLEOFF

**Example:**
```c
sc_start SC_INVINCIBLEOFF, 60000, 1;
```

---

### SC_MANU_ATK

**Icon:** `EFST_MANU_ATK`

**Effect:** Increase Weapon Damage rate to Manuk monsters

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Damage |
| val2 | (hardcoded to 1 mark as Manuk group bonus) |

**Example:**
```c
sc_start SC_MANU_ATK, 60000, 10;  // 60 seconds
```

---

### SC_MANU_DEF

**Icon:** `EFST_MANU_DEF`

**Effect:** Increase Defense rate against Manuk monsters

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Defense |
| val2 | (hardcoded to 1 mark as Manuk group bonus) |

**Example:**
```c
sc_start SC_MANU_DEF, 60000, 10;  // 60 seconds
```

---

### SC_SPL_ATK

**Icon:** `EFST_SPL_ATK`

**Effect:** Increase Weapon Damage rate to Splendide Monster

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Damage |
| val2 | (hardcoded to 1 mark as Splendide group bonus) |

**Example:**
```c
sc_start SC_SPL_ATK, 60000, 10;  // 60 seconds
```

---

### SC_SPL_DEF

**Icon:** `EFST_SPL_DEF`

**Effect:** Increase Defense rate against Splendide Monster

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Defense |
| val2 | (hardcoded to 1 mark as Splendide group bonus) |

**Example:**
```c
sc_start SC_SPL_DEF, 60000, 10;  // 60 seconds
```

---

### SC_MANU_MATK

**Icon:** `EFST_MANU_MATK`

**Effect:** Increase Magic Damage rate to Manuk monsters

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Magic damage |
| val2 | (hardcoded to 1 mark as Manuk group bonus) |

**Example:**
```c
sc_start SC_MANU_MATK, 60000, 10;  // 60 seconds
```

---

### SC_SPL_MATK

**Icon:** `EFST_SPL_MATK`

**Effect:** Increase Magic Damage to Splendide Monster

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Damage |
| val2 | (hardcoded to 1 mark as Splendide group bonus) |

**Example:**
```c
sc_start SC_SPL_MATK, 60000, 10;  // 60 seconds
```

---

### SC_ENCHANTBLADE

**Example:**
```c
sc_start SC_ENCHANTBLADE, 60000, 1;
```

---

### SC_DEATHBOUND

**Example:**
```c
sc_start SC_DEATHBOUND, 60000, 1;
```

---

### SC_MILLENNIUMSHIELD

**Example:**
```c
sc_start SC_MILLENNIUMSHIELD, 60000, 1;
```

---

### SC_CRUSHSTRIKE

**Example:**
```c
sc_start SC_CRUSHSTRIKE, 60000, 1;
```

---

### SC_REFRESH

**Example:**
```c
sc_start SC_REFRESH, 60000, 1;
```

---

### SC_REUSE_REFRESH

**Example:**
```c
sc_start SC_REUSE_REFRESH, 60000, 1;
```

---

### SC_GIANTGROWTH

**Example:**
```c
sc_start SC_GIANTGROWTH, 60000, 1;
```

---

### SC_VITALITYACTIVATION

**Example:**
```c
sc_start SC_VITALITYACTIVATION, 60000, 1;
```

---

### SC_STORMBLAST

**Example:**
```c
sc_start SC_STORMBLAST, 60000, 1;
```

---

### SC_FIGHTINGSPIRIT

**Example:**
```c
sc_start SC_FIGHTINGSPIRIT, 60000, 1;
```

---

### SC_ABUNDANCE

**Example:**
```c
sc_start SC_ABUNDANCE, 60000, 1;
```

---

### SC_ADORAMUS

**Example:**
```c
sc_start SC_ADORAMUS, 60000, 1;
```

---

### SC_EPICLESIS

**Example:**
```c
sc_start SC_EPICLESIS, 60000, 1;
```

---

### SC_ORATIO

**Example:**
```c
sc_start SC_ORATIO, 60000, 1;
```

---

### SC_LAUDAAGNUS

**Example:**
```c
sc_start SC_LAUDAAGNUS, 60000, 1;
```

---

### SC_LAUDARAMUS

**Example:**
```c
sc_start SC_LAUDARAMUS, 60000, 1;
```

---

### SC_RENOVATIO

**Example:**
```c
sc_start SC_RENOVATIO, 60000, 1;
```

---

### SC_EXPIATIO

**Example:**
```c
sc_start SC_EXPIATIO, 60000, 1;
```

---

### SC_DUPLELIGHT

**Example:**
```c
sc_start SC_DUPLELIGHT, 60000, 1;
```

---

### SC_SECRAMENT

**Example:**
```c
sc_start SC_SECRAMENT, 60000, 1;
```

---

### SC_WHITEIMPRISON

**Example:**
```c
sc_start SC_WHITEIMPRISON, 60000, 1;
```

---

### SC_MARSHOFABYSS

**Example:**
```c
sc_start SC_MARSHOFABYSS, 60000, 1;
```

---

### SC_RECOGNIZEDSPELL

**Example:**
```c
sc_start SC_RECOGNIZEDSPELL, 60000, 1;
```

---

### SC_STASIS

**Example:**
```c
sc_start SC_STASIS, 60000, 1;
```

---

### SC_SPHERE_1

**Example:**
```c
sc_start SC_SPHERE_1, 60000, 1;
```

---

### SC_SPHERE_2

**Example:**
```c
sc_start SC_SPHERE_2, 60000, 1;
```

---

### SC_SPHERE_3

**Example:**
```c
sc_start SC_SPHERE_3, 60000, 1;
```

---

### SC_SPHERE_4

**Example:**
```c
sc_start SC_SPHERE_4, 60000, 1;
```

---

### SC_SPHERE_5

**Example:**
```c
sc_start SC_SPHERE_5, 60000, 1;
```

---

### SC_READING_SB

**Example:**
```c
sc_start SC_READING_SB, 60000, 1;
```

---

### SC_ELECTRICSHOCKER

**Example:**
```c
sc_start SC_ELECTRICSHOCKER, 60000, 1;
```

---

### SC_WUGDASH

**Example:**
```c
sc_start SC_WUGDASH, 60000, 1;
```

---

### SC_BITE

**Example:**
```c
sc_start SC_BITE, 60000, 1;
```

---

### SC_CAMOUFLAGE

**Example:**
```c
sc_start SC_CAMOUFLAGE, 60000, 1;
```

---

### SC_ACCELERATION

**Example:**
```c
sc_start SC_ACCELERATION, 60000, 1;
```

---

### SC_HOVERING

**Example:**
```c
sc_start SC_HOVERING, 60000, 1;
```

---

### SC_SHAPESHIFT

**Example:**
```c
sc_start SC_SHAPESHIFT, 60000, 1;
```

---

### SC_INFRAREDSCAN

**Example:**
```c
sc_start SC_INFRAREDSCAN, 60000, 1;
```

---

### SC_ANALYZE

**Example:**
```c
sc_start SC_ANALYZE, 60000, 1;
```

---

### SC_MAGNETICFIELD

**Example:**
```c
sc_start SC_MAGNETICFIELD, 60000, 1;
```

---

### SC_NEUTRALBARRIER

**Example:**
```c
sc_start SC_NEUTRALBARRIER, 60000, 1;
```

---

### SC_NEUTRALBARRIER_MASTER

**Example:**
```c
sc_start SC_NEUTRALBARRIER_MASTER, 60000, 1;
```

---

### SC_OVERHEAT

**Example:**
```c
sc_start SC_OVERHEAT, 60000, 1;
```

---

### SC_OVERHEAT_LIMITPOINT

**Example:**
```c
sc_start SC_OVERHEAT_LIMITPOINT, 60000, 1;
```

---

### SC_VENOMIMPRESS

**Example:**
```c
sc_start SC_VENOMIMPRESS, 60000, 1;
```

---

### SC_WEAPONBLOCKING

**Example:**
```c
sc_start SC_WEAPONBLOCKING, 60000, 1;
```

---

### SC_CLOAKINGEXCEED

**Example:**
```c
sc_start SC_CLOAKINGEXCEED, 60000, 1;
```

---

### SC_HALLUCINATIONWALK

**Example:**
```c
sc_start SC_HALLUCINATIONWALK, 60000, 1;
```

---

### SC_HALLUCINATIONWALK_POSTDELAY

**Example:**
```c
sc_start SC_HALLUCINATIONWALK_POSTDELAY, 60000, 1;
```

---

### SC_ROLLINGCUTTER

**Example:**
```c
sc_start SC_ROLLINGCUTTER, 60000, 1;
```

---

### SC_TOXIN

**Icon:** `EFST_TOXIN`

**Effect:** Inflict damage, which causes the affected entity to flinch every 10 seconds; This will interrupt the skill casting, even if protected against it

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val2 | Caster's object ID |
| val4 | Remaining tick |

**Example:**
```c
sc_start SC_TOXIN, 60000, 10;  // 60 seconds
```

---

### SC_PARALYSE

**Icon:** `EFST_PARALYSE`

**Effect:** Decrease both ASPD and Flee Rate by 10% and halve Movement Speed, which does not stack with Decrease AGI, Quagmire, Marsh Of Abyss or Freezing status

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val4 | Tick |

**Example:**
```c
sc_start SC_PARALYSE, 60000, 10;  // 60 seconds
```

---

### SC_VENOMBLEED

**Icon:** `EFST_VENOMBLEED`

**Effect:** Decrease Max HP by 15%

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val4 | Tick |

**Example:**
```c
sc_start SC_VENOMBLEED, 60000, 10;  // 60 seconds
```

---

### SC_MAGICMUSHROOM

**Icon:** `EFST_MAGICMUSHROOM`

**Effect:** Force the affected entity to use /heh emote, to randomly use skills and drain 3% of Max HP every 4 seconds

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val2 | Caster's object ID |
| val4 | Remaining tick |

**Example:**
```c
sc_start SC_MAGICMUSHROOM, 60000, 10;  // 60 seconds
```

---

### SC_DEATHHURT

**Icon:** `EFST_DEATHHURT`

**Effect:** Drop the healing effectiveness by 20%; This effect stacks with Critical Wounds

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val4 | Tick |

**Example:**
```c
sc_start SC_DEATHHURT, 60000, 10;  // 60 seconds
```

---

### SC_PYREXIA

**Icon:** `EFST_PYREXIA`

**Effect:** Cause Blind and Hallucination statuses; If the affected entity takes damage while under the effects of this poison, it will remain in flinching motion, which will interrupt the skill casting

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val4 | Remaining tick |

**Example:**
```c
sc_start SC_PYREXIA, 60000, 10;  // 60 seconds
```

---

### SC_LEECHESEND

**Icon:** `EFST_LEECHESEND`

**Effect:** Drain (Target VIT * (SkillLv - 3)) + (Target HP / 100) HP each second

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | GC_WEAPONRESEARCH Skill Level |
| val2 | Caster's object ID |
| val4 | Remaining tick |

**Example:**
```c
sc_start SC_LEECHESEND, 60000, 10;  // 60 seconds
```

---

### SC_REFLECTDAMAGE

**Example:**
```c
sc_start SC_REFLECTDAMAGE, 60000, 1;
```

---

### SC_FORCEOFVANGUARD

**Example:**
```c
sc_start SC_FORCEOFVANGUARD, 60000, 1;
```

---

### SC_SHIELDSPELL_DEF

**Example:**
```c
sc_start SC_SHIELDSPELL_DEF, 60000, 1;
```

---

### SC_SHIELDSPELL_MDEF

**Example:**
```c
sc_start SC_SHIELDSPELL_MDEF, 60000, 1;
```

---

### SC_SHIELDSPELL_REF

**Example:**
```c
sc_start SC_SHIELDSPELL_REF, 60000, 1;
```

---

### SC_EXEEDBREAK

**Example:**
```c
sc_start SC_EXEEDBREAK, 60000, 1;
```

---

### SC_PRESTIGE

**Example:**
```c
sc_start SC_PRESTIGE, 60000, 1;
```

---

### SC_BANDING

**Example:**
```c
sc_start SC_BANDING, 60000, 1;
```

---

### SC_BANDING_DEFENCE

**Example:**
```c
sc_start SC_BANDING_DEFENCE, 60000, 1;
```

---

### SC_EARTHDRIVE

**Example:**
```c
sc_start SC_EARTHDRIVE, 60000, 1;
```

---

### SC_INSPIRATION

**Example:**
```c
sc_start SC_INSPIRATION, 60000, 1;
```

---

### SC_SPELLFIST

**Example:**
```c
sc_start SC_SPELLFIST, 60000, 1;
```

---

### SC_CRYSTALIZE

**Example:**
```c
sc_start SC_CRYSTALIZE, 60000, 1;
```

---

### SC_STRIKING

**Icon:** `EFST_STRIKING`

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | SO_STRIKING Skill Level |
| val2 | Increased ATK |
| val3 | SP Drain / Sec |
| val4 | Tick Left (in sec) |

**Example:**
```c
sc_start SC_STRIKING, 60000, 10;  // 60 seconds
```

---

### SC_WARMER

**Example:**
```c
sc_start SC_WARMER, 60000, 1;
```

---

### SC_VACUUM_EXTREME

**Example:**
```c
sc_start SC_VACUUM_EXTREME, 60000, 1;
```

---

### SC_PROPERTYWALK

**Example:**
```c
sc_start SC_PROPERTYWALK, 60000, 1;
```

---

### SC_SWINGDANCE

**Example:**
```c
sc_start SC_SWINGDANCE, 60000, 1;
```

---

### SC_SYMPHONYOFLOVER

**Example:**
```c
sc_start SC_SYMPHONYOFLOVER, 60000, 1;
```

---

### SC_MOONLITSERENADE

**Icon:** `EFST_MOONLIT_SERENADE`

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | WA_MOONLIT_SERENADE Skill Level |
| val2 | WM_LESSON Level |
| val3 | Increased MATK |

**Example:**
```c
sc_start SC_MOONLITSERENADE, 60000, 10;  // 60 seconds
```

---

### SC_RUSHWINDMILL

**Icon:** `EFST_RUSH_WINDMILL`

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | MI_RUSH_WINDMILL Skill Level |
| val2 | WM_LESSON Level |
| val3 | Increased ATK |

**Example:**
```c
sc_start SC_RUSHWINDMILL, 60000, 10;  // 60 seconds
```

---

### SC_ECHOSONG

**Example:**
```c
sc_start SC_ECHOSONG, 60000, 1;
```

---

### SC_HARMONIZE

**Example:**
```c
sc_start SC_HARMONIZE, 60000, 1;
```

---

### SC_VOICEOFSIREN

**Example:**
```c
sc_start SC_VOICEOFSIREN, 60000, 1;
```

---

### SC_SIRCLEOFNATURE

**Example:**
```c
sc_start SC_SIRCLEOFNATURE, 60000, 1;
```

---

### SC_GLOOMYDAY

**Example:**
```c
sc_start SC_GLOOMYDAY, 60000, 1;
```

---

### SC_GLOOMYDAY_SK

**Example:**
```c
sc_start SC_GLOOMYDAY_SK, 60000, 1;
```

---

### SC_SONGOFMANA

**Example:**
```c
sc_start SC_SONGOFMANA, 60000, 1;
```

---

### SC_DANCEWITHWUG

**Example:**
```c
sc_start SC_DANCEWITHWUG, 60000, 1;
```

---

### SC_SATURDAYNIGHTFEVER

**Example:**
```c
sc_start SC_SATURDAYNIGHTFEVER, 60000, 1;
```

---

### SC_LERADSDEW

**Example:**
```c
sc_start SC_LERADSDEW, 60000, 1;
```

---

### SC_MELODYOFSINK

**Example:**
```c
sc_start SC_MELODYOFSINK, 60000, 1;
```

---

### SC_BEYONDOFWARCRY

**Example:**
```c
sc_start SC_BEYONDOFWARCRY, 60000, 1;
```

---

### SC_UNLIMITEDHUMMINGVOICE

**Example:**
```c
sc_start SC_UNLIMITEDHUMMINGVOICE, 60000, 1;
```

---

### SC_SITDOWN_FORCE

**Example:**
```c
sc_start SC_SITDOWN_FORCE, 60000, 1;
```

---

### SC_NETHERWORLD

**Example:**
```c
sc_start SC_NETHERWORLD, 60000, 1;
```

---

### SC_CRESCENTELBOW

**Example:**
```c
sc_start SC_CRESCENTELBOW, 60000, 1;
```

---

### SC_LIGHTNINGWALK

**Example:**
```c
sc_start SC_LIGHTNINGWALK, 60000, 1;
```

---

### SC_RAISINGDRAGON

**Example:**
```c
sc_start SC_RAISINGDRAGON, 60000, 1;
```

---

### SC_GT_ENERGYGAIN

**Icon:** `EFST_GENTLETOUCH_ENERGYGAIN`

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | SR_GENTLETOUCH_ENERGYGAIN Skill Level |
| val2 | Sphere Gain Chance |

**Example:**
```c
sc_start SC_GT_ENERGYGAIN, 60000, 10;  // 60 seconds
```

---

### SC_GT_CHANGE

**Icon:** `EFST_GENTLETOUCH_CHANGE`

**Effect:** ATK increase: ATK [{(Caster DEX / 4) + (Caster STR / 2)} x Skill Level / 5]; ASPD increase: [(Target AGI x Skill Level) / 60] %; MDEF decrease: MDEF [(200 / Caster INT) x Skill Level]; Max HP decrease: [Skill Level x 4] %

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | SR_GENTLETOUCH_CHANGE Skill Level |
| val2 | Increased ATK |
| val3 | Increased ASPD Rate |
| val4 | Decreased MDEF |

**Example:**
```c
sc_start SC_GT_CHANGE, 60000, 10;  // 60 seconds
```

---

### SC_GT_REVITALIZE

**Icon:** `EFST_GENTLETOUCH_REVITALIZE`

**Effect:** MaxHP: [(Skill Level * 2)]%; Natural HP recovery increase: [(Skill Level x 30) + 50] %; STAT DEF increase: [(Caster VIT / 4) x Skill Level] (The stat def is not shown in the status window and it is processed differently)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | SR_GENTLETOUCH_REVITALIZE Skill Level |
| val2 | Max HP Rate bonus |
| val3 | HP Regen Rage Value |
| val4 | Increased DEF |

**Example:**
```c
sc_start SC_GT_REVITALIZE, 60000, 10;  // 60 seconds
```

---

### SC_THORNSTRAP

**Example:**
```c
sc_start SC_THORNSTRAP, 60000, 1;
```

---

### SC_BLOODSUCKER

**Example:**
```c
sc_start SC_BLOODSUCKER, 60000, 1;
```

---

### SC_SMOKEPOWDER

**Example:**
```c
sc_start SC_SMOKEPOWDER, 60000, 1;
```

---

### SC_MANDRAGORA

**Example:**
```c
sc_start SC_MANDRAGORA, 60000, 1;
```

---

### SC_STOMACHACHE

**Icon:** `EFST_STOMACHACHE`

**Effect:** Reduce all stats

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | -AllStats |

**Example:**
```c
sc_start SC_STOMACHACHE, 60000, 10;  // 60 seconds
```

---

### SC_MYSTERIOUS_POWDER

**Icon:** `EFST_MYSTERIOUS_POWDER`

**Effect:** Reduce Max HP rate

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | ReduceValue (don't use - sign to reduce) |

**Example:**
```c
sc_start SC_MYSTERIOUS_POWDER, 60000, 10;  // 60 seconds
```

---

### SC_MELON_BOMB

**Icon:** `EFST_MELON_BOMB`

**Effect:** Reduce ASPD and move speed

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | ReduceValue (don't use - sign to reduce) |

**Example:**
```c
sc_start SC_MELON_BOMB, 60000, 10;  // 60 seconds
```

---

### SC_BANANA_BOMB

**Icon:** `EFST_BANANA_BOMB`

**Effect:** Reduce LUK rate

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | ReduceValue (don't use - sign to reduce) |

**Example:**
```c
sc_start SC_BANANA_BOMB, 60000, 10;  // 60 seconds
```

---

### SC_BANANA_BOMB_SITDOWN

**Icon:** `EFST_BANANA_BOMB_SITDOWN_POSTDELAY`

**Effect:** Force player to sit

**Example:**
```c
sc_start SC_BANANA_BOMB_SITDOWN, 60000, 1;
```

---

### SC_COCKTAIL_WARG_BLOOD

**Icon:** `EFST_COCKTAIL_WARG_BLOOD`

**Effect:** Increase INT

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +INT |

**Example:**
```c
sc_start SC_COCKTAIL_WARG_BLOOD, 60000, 10;  // 60 seconds
```

---

### SC_PUTTI_TAILS_NOODLES

**Icon:** `EFST_PUTTI_TAILS_NOODLES`

**Effect:** Increase LUK

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +LUK |

**Example:**
```c
sc_start SC_PUTTI_TAILS_NOODLES, 60000, 10;  // 60 seconds
```

---

### SC_FULL_SWING_K

**Icon:** `EFST_FULL_SWING_K`

**Effect:** Increase Base Atk

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +BaseAtk |

**Example:**
```c
sc_start SC_FULL_SWING_K, 60000, 10;  // 60 seconds
```

---

### SC_MANA_PLUS

**Icon:** `EFST_MANA_PLUS`

**Effect:** Increase MAtk

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +Matk |

**Example:**
```c
sc_start SC_MANA_PLUS, 60000, 10;  // 60 seconds
```

---

### SC_MUSTLE_M

**Icon:** `EFST_MUSTLE_M`

**Effect:** Increase Max HP rate

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% MaxHP |

**Example:**
```c
sc_start SC_MUSTLE_M, 60000, 10;  // 60 seconds
```

---

### SC_LIFE_FORCE_F

**Icon:** `EFST_LIFE_FORCE_F`

**Effect:** Increase Max SP rate

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% MaxSP |

**Example:**
```c
sc_start SC_LIFE_FORCE_F, 60000, 10;  // 60 seconds
```

---

### SC_VITATA_500

**Icon:** `EFST_VITATA_500`

**Effect:** Increase SP Regen rate & Max SP rate

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% SP regen |
| val2 | +% MaxSP |

**Example:**
```c
sc_start SC_VITATA_500, 60000, 10;  // 60 seconds
```

---

### SC_EXTRACT_SALAMINE_JUICE

**Icon:** `EFST_EXTRACT_SALAMINE_JUICE`

**Effect:** Increase ASP rate

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% ASPD |

**Example:**
```c
sc_start SC_EXTRACT_SALAMINE_JUICE, 60000, 10;  // 60 seconds
```

---

### SC__REPRODUCE

**Example:**
```c
sc_start SC__REPRODUCE, 60000, 1;
```

---

### SC__AUTOSHADOWSPELL

**Example:**
```c
sc_start SC__AUTOSHADOWSPELL, 60000, 1;
```

---

### SC__SHADOWFORM

**Example:**
```c
sc_start SC__SHADOWFORM, 60000, 1;
```

---

### SC__BODYPAINT

**Example:**
```c
sc_start SC__BODYPAINT, 60000, 1;
```

---

### SC__INVISIBILITY

**Example:**
```c
sc_start SC__INVISIBILITY, 60000, 1;
```

---

### SC__DEADLYINFECT

**Example:**
```c
sc_start SC__DEADLYINFECT, 60000, 1;
```

---

### SC__ENERVATION

**Example:**
```c
sc_start SC__ENERVATION, 60000, 1;
```

---

### SC__GROOMY

**Example:**
```c
sc_start SC__GROOMY, 60000, 1;
```

---

### SC__IGNORANCE

**Example:**
```c
sc_start SC__IGNORANCE, 60000, 1;
```

---

### SC__LAZINESS

**Example:**
```c
sc_start SC__LAZINESS, 60000, 1;
```

---

### SC__UNLUCKY

**Example:**
```c
sc_start SC__UNLUCKY, 60000, 1;
```

---

### SC__WEAKNESS

**Example:**
```c
sc_start SC__WEAKNESS, 60000, 1;
```

---

### SC__STRIPACCESSORY

**Example:**
```c
sc_start SC__STRIPACCESSORY, 60000, 1;
```

---

### SC__MANHOLE

**Example:**
```c
sc_start SC__MANHOLE, 60000, 1;
```

---

### SC__BLOODYLUST

**Example:**
```c
sc_start SC__BLOODYLUST, 60000, 1;
```

---

### SC_CIRCLE_OF_FIRE

**Example:**
```c
sc_start SC_CIRCLE_OF_FIRE, 60000, 1;
```

---

### SC_CIRCLE_OF_FIRE_OPTION

**Example:**
```c
sc_start SC_CIRCLE_OF_FIRE_OPTION, 60000, 1;
```

---

### SC_FIRE_CLOAK

**Example:**
```c
sc_start SC_FIRE_CLOAK, 60000, 1;
```

---

### SC_FIRE_CLOAK_OPTION

**Example:**
```c
sc_start SC_FIRE_CLOAK_OPTION, 60000, 1;
```

---

### SC_WATER_SCREEN

**Example:**
```c
sc_start SC_WATER_SCREEN, 60000, 1;
```

---

### SC_WATER_SCREEN_OPTION

**Example:**
```c
sc_start SC_WATER_SCREEN_OPTION, 60000, 1;
```

---

### SC_WATER_DROP

**Example:**
```c
sc_start SC_WATER_DROP, 60000, 1;
```

---

### SC_WATER_DROP_OPTION

**Example:**
```c
sc_start SC_WATER_DROP_OPTION, 60000, 1;
```

---

### SC_WATER_BARRIER

**Example:**
```c
sc_start SC_WATER_BARRIER, 60000, 1;
```

---

### SC_WIND_STEP

**Example:**
```c
sc_start SC_WIND_STEP, 60000, 1;
```

---

### SC_WIND_STEP_OPTION

**Example:**
```c
sc_start SC_WIND_STEP_OPTION, 60000, 1;
```

---

### SC_WIND_CURTAIN

**Example:**
```c
sc_start SC_WIND_CURTAIN, 60000, 1;
```

---

### SC_WIND_CURTAIN_OPTION

**Example:**
```c
sc_start SC_WIND_CURTAIN_OPTION, 60000, 1;
```

---

### SC_ZEPHYR

**Example:**
```c
sc_start SC_ZEPHYR, 60000, 1;
```

---

### SC_SOLID_SKIN

**Example:**
```c
sc_start SC_SOLID_SKIN, 60000, 1;
```

---

### SC_SOLID_SKIN_OPTION

**Example:**
```c
sc_start SC_SOLID_SKIN_OPTION, 60000, 1;
```

---

### SC_POWER_OF_GAIA

**Example:**
```c
sc_start SC_POWER_OF_GAIA, 60000, 1;
```

---

### SC_PYROTECHNIC

**Example:**
```c
sc_start SC_PYROTECHNIC, 60000, 1;
```

---

### SC_PYROTECHNIC_OPTION

**Example:**
```c
sc_start SC_PYROTECHNIC_OPTION, 60000, 1;
```

---

### SC_HEATER

**Example:**
```c
sc_start SC_HEATER, 60000, 1;
```

---

### SC_HEATER_OPTION

**Example:**
```c
sc_start SC_HEATER_OPTION, 60000, 1;
```

---

### SC_TROPIC

**Example:**
```c
sc_start SC_TROPIC, 60000, 1;
```

---

### SC_TROPIC_OPTION

**Example:**
```c
sc_start SC_TROPIC_OPTION, 60000, 1;
```

---

### SC_AQUAPLAY

**Example:**
```c
sc_start SC_AQUAPLAY, 60000, 1;
```

---

### SC_AQUAPLAY_OPTION

**Example:**
```c
sc_start SC_AQUAPLAY_OPTION, 60000, 1;
```

---

### SC_COOLER

**Example:**
```c
sc_start SC_COOLER, 60000, 1;
```

---

### SC_COOLER_OPTION

**Example:**
```c
sc_start SC_COOLER_OPTION, 60000, 1;
```

---

### SC_CHILLY_AIR

**Example:**
```c
sc_start SC_CHILLY_AIR, 60000, 1;
```

---

### SC_CHILLY_AIR_OPTION

**Example:**
```c
sc_start SC_CHILLY_AIR_OPTION, 60000, 1;
```

---

### SC_GUST

**Example:**
```c
sc_start SC_GUST, 60000, 1;
```

---

### SC_GUST_OPTION

**Example:**
```c
sc_start SC_GUST_OPTION, 60000, 1;
```

---

### SC_BLAST

**Example:**
```c
sc_start SC_BLAST, 60000, 1;
```

---

### SC_BLAST_OPTION

**Example:**
```c
sc_start SC_BLAST_OPTION, 60000, 1;
```

---

### SC_WILD_STORM

**Example:**
```c
sc_start SC_WILD_STORM, 60000, 1;
```

---

### SC_WILD_STORM_OPTION

**Example:**
```c
sc_start SC_WILD_STORM_OPTION, 60000, 1;
```

---

### SC_PETROLOGY

**Example:**
```c
sc_start SC_PETROLOGY, 60000, 1;
```

---

### SC_PETROLOGY_OPTION

**Example:**
```c
sc_start SC_PETROLOGY_OPTION, 60000, 1;
```

---

### SC_UPHEAVAL

**Example:**
```c
sc_start SC_UPHEAVAL, 60000, 1;
```

---

### SC_UPHEAVAL_OPTION

**Example:**
```c
sc_start SC_UPHEAVAL_OPTION, 60000, 1;
```

---

### SC_TIDAL_WEAPON

**Example:**
```c
sc_start SC_TIDAL_WEAPON, 60000, 1;
```

---

### SC_TIDAL_WEAPON_OPTION

**Example:**
```c
sc_start SC_TIDAL_WEAPON_OPTION, 60000, 1;
```

---

### SC_ROCK_CRUSHER

**Example:**
```c
sc_start SC_ROCK_CRUSHER, 60000, 1;
```

---

### SC_ROCK_CRUSHER_ATK

**Example:**
```c
sc_start SC_ROCK_CRUSHER_ATK, 60000, 1;
```

---

### SC_LEADERSHIP

**Example:**
```c
sc_start SC_LEADERSHIP, 60000, 1;
```

---

### SC_GLORYWOUNDS

**Example:**
```c
sc_start SC_GLORYWOUNDS, 60000, 1;
```

---

### SC_SOULCOLD

**Example:**
```c
sc_start SC_SOULCOLD, 60000, 1;
```

---

### SC_HAWKEYES

**Example:**
```c
sc_start SC_HAWKEYES, 60000, 1;
```

---

### SC_ODINS_POWER

**Example:**
```c
sc_start SC_ODINS_POWER, 60000, 1;
```

---

### SC_RAID

**Example:**
```c
sc_start SC_RAID, 60000, 1;
```

---

### SC_FIRE_INSIGNIA

**Example:**
```c
sc_start SC_FIRE_INSIGNIA, 60000, 1;
```

---

### SC_WATER_INSIGNIA

**Example:**
```c
sc_start SC_WATER_INSIGNIA, 60000, 1;
```

---

### SC_WIND_INSIGNIA

**Example:**
```c
sc_start SC_WIND_INSIGNIA, 60000, 1;
```

---

### SC_EARTH_INSIGNIA

**Example:**
```c
sc_start SC_EARTH_INSIGNIA, 60000, 1;
```

---

### SC_PUSH_CART

**Example:**
```c
sc_start SC_PUSH_CART, 60000, 1;
```

---

### SC_SPELLBOOK1

**Example:**
```c
sc_start SC_SPELLBOOK1, 60000, 1;
```

---

### SC_SPELLBOOK2

**Example:**
```c
sc_start SC_SPELLBOOK2, 60000, 1;
```

---

### SC_SPELLBOOK3

**Example:**
```c
sc_start SC_SPELLBOOK3, 60000, 1;
```

---

### SC_SPELLBOOK4

**Example:**
```c
sc_start SC_SPELLBOOK4, 60000, 1;
```

---

### SC_SPELLBOOK5

**Example:**
```c
sc_start SC_SPELLBOOK5, 60000, 1;
```

---

### SC_SPELLBOOK6

**Example:**
```c
sc_start SC_SPELLBOOK6, 60000, 1;
```

---

### SC_MAXSPELLBOOK

**Example:**
```c
sc_start SC_MAXSPELLBOOK, 60000, 1;
```

---

### SC_INCMHP

**Effect:** Increase Max HP

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + Max HP |

**Example:**
```c
sc_start SC_INCMHP, 60000, 10;  // 60 seconds
```

---

### SC_INCMSP

**Effect:** Incrase Max SP

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + MaxSP |

**Example:**
```c
sc_start SC_INCMSP, 60000, 10;  // 60 seconds
```

---

### SC_PARTYFLEE

**Example:**
```c
sc_start SC_PARTYFLEE, 60000, 1;
```

---

### SC_MEIKYOUSISUI

**Example:**
```c
sc_start SC_MEIKYOUSISUI, 60000, 1;
```

---

### SC_JYUMONJIKIRI

**Example:**
```c
sc_start SC_JYUMONJIKIRI, 60000, 1;
```

---

### SC_KYOUGAKU

**Example:**
```c
sc_start SC_KYOUGAKU, 60000, 1;
```

---

### SC_IZAYOI

**Example:**
```c
sc_start SC_IZAYOI, 60000, 1;
```

---

### SC_ZENKAI

**Example:**
```c
sc_start SC_ZENKAI, 60000, 1;
```

---

### SC_KAGEHUMI

**Example:**
```c
sc_start SC_KAGEHUMI, 60000, 1;
```

---

### SC_KYOMU

**Example:**
```c
sc_start SC_KYOMU, 60000, 1;
```

---

### SC_KAGEMUSYA

**Example:**
```c
sc_start SC_KAGEMUSYA, 60000, 1;
```

---

### SC_ZANGETSU

**Example:**
```c
sc_start SC_ZANGETSU, 60000, 1;
```

---

### SC_GENSOU

**Example:**
```c
sc_start SC_GENSOU, 60000, 1;
```

---

### SC_AKAITSUKI

**Example:**
```c
sc_start SC_AKAITSUKI, 60000, 1;
```

---

### SC_STYLE_CHANGE

**Effect:** Eleanor's mode

**Example:**
```c
sc_start SC_STYLE_CHANGE, 60000, 1;
```

---

### SC_TINDER_BREAKER

**Icon:** `EFST_TINDER_BREAKER_POSTDELAY`

**Example:**
```c
sc_start SC_TINDER_BREAKER, 60000, 1;
```

---

### SC_TINDER_BREAKER2

**Icon:** `EFST_TINDER_BREAKER`

**Effect:** Tinder Breaker after-effect, just like Close Confine

**Example:**
```c
sc_start SC_TINDER_BREAKER2, 60000, 1;
```

---

### SC_CBC

**Icon:** `EFST_CBC`

**Effect:** Drain HP & SP each iteration (default is each 1 sec)

**Parameters:**

| Param | Usage |
|-------|-------|
| val3 | %SP drain |

**Example:**
```c
sc_start SC_CBC, 60000, 1;
```

---

### SC_EQC

**Icon:** `EFST_EQC`

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | -% Def |
| val3 | -%MaxHP |

**Example:**
```c
sc_start SC_EQC, 60000, 1;
```

---

### SC_GOLDENE_FERSE

**Icon:** `EFST_GOLDENE_FERSE`

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | +% Flee |
| val3 | +% ASPD |
| val4 | % Chance to convert attack as Holy element |

**Example:**
```c
sc_start SC_GOLDENE_FERSE, 60000, 1;
```

---

### SC_ANGRIFFS_MODUS

**Icon:** `EFST_ANGRIFFS_MODUS`

**Effect:** Drain 100 HP & 20 SP each iteration (default is each 1 sec)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Level. Usage for +MaxHP rate (5 * level) |
| val2 | +ATK |
| val3 | -Flee |

**Example:**
```c
sc_start SC_ANGRIFFS_MODUS, 60000, 10;  // 60 seconds
```

---

### SC_LIGHT_OF_REGENE

**Icon:** `EFST_LIGHT_OF_REGENE`

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | % of HP recovery on death |

**Example:**
```c
sc_start SC_LIGHT_OF_REGENE, 60000, 1;
```

---

### SC_ASH

**Icon:** `EFST_VOLCANIC_ASH`

**Effect:** Increase damage to Fire element enemy (ratio +150%), reduce Hit, Def, Atk & Flee.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | -% Hit |
| val2 | -% Def |
| val4 | -Atk & Flee |

**Example:**
```c
sc_start SC_ASH, 60000, 10;  // 60 seconds
```

---

### SC_GRANITIC_ARMOR

**Icon:** `EFST_GRANITIC_ARMOR`

**Effect:** Reduce the inflicted damage, when status ended deals another damage to self

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | -%Damage |
| val3 | Damage taken on status end |

**Example:**
```c
sc_start SC_GRANITIC_ARMOR, 60000, 1;
```

---

### SC_MAGMA_FLOW

**Icon:** `EFST_MAGMA_FLOW`

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | Rate to cast Magma Flow (deals damage) to target while attacking |

**Example:**
```c
sc_start SC_MAGMA_FLOW, 60000, 1;
```

---

### SC_PYROCLASTIC

**Icon:** `EFST_PYROCLASTIC`

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | +ATK |
| val3 | % Rate to cast Hammer Fall |

**Example:**
```c
sc_start SC_PYROCLASTIC, 60000, 1;
```

---

### SC_PARALYSIS

**Icon:** `EFST_NEEDLE_OF_PARALYZE`

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | -Def |
| val3 | +% CastTime |

**Example:**
```c
sc_start SC_PARALYSIS, 60000, 1;
```

---

### SC_PAIN_KILLER

**Icon:** `EFST_PAIN_KILLER`

**Effect:** Reduce damage for certain value, reduce ASPD rate, inflict Endure if has active SC_PARALYSIS

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | -% ASPD |
| val3 | -Damage |

**Example:**
```c
sc_start SC_PAIN_KILLER, 60000, 1;
```

---

### SC_HANBOK

**Effect:** Visual effect. Hanbok costume!

**Example:**
```c
sc_start SC_HANBOK, 60000, 1;
```

---

### SC_DEFSET

**Effect:** Vellum Weapon bonus. Set Def value

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Def fixed value |

**Example:**
```c
sc_start SC_DEFSET, 60000, 10;  // 60 seconds
```

---

### SC_MDEFSET

**Effect:** Vellum Weapon bonus. Set MDef value

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | MDef fixed value |

**Example:**
```c
sc_start SC_MDEFSET, 60000, 10;  // 60 seconds
```

---

### SC_DARKCROW

**Icon:** `EFST_DARKCROW`

**Effect:** Increase short/melee damage rate

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | +% Damage |

**Example:**
```c
sc_start SC_DARKCROW, 60000, 1;
```

---

### SC_FULL_THROTTLE

**Icon:** `EFST_FULL_THROTTLE`

**Effect:** Increase walk speed, increase allstats, full HP once activated

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Level, also used as Rebound level when this sc ended |
| val2 | -SP each iteration |
| val3 | +% Allstats |

**Example:**
```c
sc_start SC_FULL_THROTTLE, 60000, 10;  // 60 seconds
```

---

### SC_REBOUND

**Icon:** `EFST_REBOUND`

**Effect:** Full Throttle  after-effect. Reduce walk speed

**Example:**
```c
sc_start SC_REBOUND, 60000, 1;
```

---

### SC_UNLIMIT

**Icon:** `EFST_UNLIMIT`

**Effect:** Increase attak rate & set Def/MDef to 1,

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | +% Attack |

**Example:**
```c
sc_start SC_UNLIMIT, 60000, 1;
```

---

### SC_KINGS_GRACE

**Icon:** `EFST_KINGS_GRACE`

**Effect:** Add Max HP & heal each iteration (default 1 seconds)

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | +HP heal |

**Example:**
```c
sc_start SC_KINGS_GRACE, 60000, 1;
```

---

### SC_TELEKINESIS_INTENSE

**Effect:** Increase SP cost & damage of Ghost skill, reduce casttime

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | +% SP Cost |
| val3 | +Damage ratio |
| val4 | -CastTime |

**Example:**
```c
sc_start SC_TELEKINESIS_INTENSE, 60000, 1;
```

---

### SC_OFFERTORIUM

**Icon:** `EFST_OFFERTORIUM`

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | +Heal Power |
| val3 | +SP Cost |

**Example:**
```c
sc_start SC_OFFERTORIUM, 60000, 1;
```

---

### SC_FRIGG_SONG

**Icon:** `EFST_FRIGG_SONG`

**Effect:** Add Max HP & heal each iteration (default 1 seconds)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Level |
| val2 | +% MaxHP |
| val3 | +HP heal |

**Example:**
```c
sc_start SC_FRIGG_SONG, 60000, 10;  // 60 seconds
```

---

### SC_MONSTER_TRANSFORM

**Effect:** Monster Transformation. (DO NOT USE THIS DIRECTLY, use script 'transform')

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Monster ID |

**Example:**
```c
sc_start SC_MONSTER_TRANSFORM, 60000, 10;  // 60 seconds
```

---

### SC_ANGEL_PROTECT

**Example:**
```c
sc_start SC_ANGEL_PROTECT, 60000, 1;
```

---

### SC_ILLUSIONDOPING

**Icon:** `EFST_ILLUSIONDOPING`

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | -Hit |

**Example:**
```c
sc_start SC_ILLUSIONDOPING, 60000, 1;
```

---

### SC_FLASHCOMBO

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | +ATK (isn't shown in status window) |

**Example:**
```c
sc_start SC_FLASHCOMBO, 60000, 1;
```

---

### SC_MOONSTAR

**Icon:** `EFST_MOONSTAR`

**Effect:** Visual effect

**Example:**
```c
sc_start SC_MOONSTAR, 60000, 1;
```

---

### SC_SUPER_STAR

**Icon:** `EFST_SUPER_STAR`

**Effect:** Visual effect

**Example:**
```c
sc_start SC_SUPER_STAR, 60000, 1;
```

---

### SC_HEAT_BARREL

**Icon:** `EFST_HEAT_BARREL`

**Effect:** (Rebellion) Reduce fixed cast time, add ASPD rate, and reduce FLEE

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | SkillLv |
| val2 | -Fixed Casttime (5 * val1) |
| val3 | +% ASPD (6 + val1 * 2) |
| val4 | -FLEE (25 + val1 * 5) |

**Example:**
```c
sc_start SC_HEAT_BARREL, 60000, 10;  // 60 seconds
```

---

### SC_P_ALTER

**Icon:** `EFST_P_ALTER`

**Effect:** Increase attack ratio and creates a barrier like Kyrie

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | SkillLv |
| val2 | +ATK ratio (10 * Coin Count) |
| val3 | Barrier HP (Max HP * (val1 * 5) / 100) |

**Example:**
```c
sc_start SC_P_ALTER, 60000, 10;  // 60 seconds
```

---

### SC_E_CHAIN

**Icon:** `EFST_E_CHAIN`

**Effect:** (Rebellion) Has chance to trigger Chain Action for any weapon

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | SkillLv |
| val2 | Coins used for success rate. (5 * val) |

**Example:**
```c
sc_start SC_E_CHAIN, 60000, 10;  // 60 seconds
```

---

### SC_C_MARKER

**Icon:** `EFST_C_MARKER`

**Effect:** (Rebellion) Crimson Marker effect, also sends the target location to the caster

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | SkillLv |
| val3 | -FLEE (10) |

**Example:**
```c
sc_start SC_C_MARKER, 60000, 10;  // 60 seconds
```

---

### SC_ANTI_M_BLAST

**Icon:** `EFST_ANTI_M_BLAST`

**Effect:** (Rebellion) Anti-Material effect, reduce resistance of Neutral attack

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | SkillLv |
| val2 | Reduction ratio (10 * val1) |

**Example:**
```c
sc_start SC_ANTI_M_BLAST, 60000, 10;  // 60 seconds
```

---

### SC_B_TRAP

**Icon:** `EFST_B_TRAP`

**Effect:** (Rebellion) Bind Trap effect, waiting for Flicker to be used

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | SkillLv |
| val3 | -Walk Speed (Unstackable penalty) (25 * val1) |

**Example:**
```c
sc_start SC_B_TRAP, 60000, 10;  // 60 seconds
```

---

### SC_H_MINE

**Icon:** `EFST_H_MINE`

**Effect:** (Rebellion) Howling Mine effect, waiting for Flicker to be used

**Example:**
```c
sc_start SC_H_MINE, 60000, 1;
```

---

### SC_QD_SHOT_READY

**Icon:** `EFST_E_QD_SHOT_READY`

**Effect:** (Rebellion) Combo stance to cast Quick Draw Shot

**Example:**
```c
sc_start SC_QD_SHOT_READY, 60000, 1;
```

---

### SC_MTF_ASPD

**Icon:** `EFST_MTF_ASPD`

**Effect:** Increase ASP and Hit

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +ASPD |
| val2 | +Hit |

**Example:**
```c
sc_start SC_MTF_ASPD, 60000, 10;  // 60 seconds
```

---

### SC_MTF_ASPD2

**Icon:** `EFST_MTF_ASPD2`

**Effect:** Increase ASP and Hit

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +ASPD |
| val2 | +Hit |

**Example:**
```c
sc_start SC_MTF_ASPD2, 60000, 10;  // 60 seconds
```

---

### SC_MTF_RANGEATK

**Icon:** `EFST_MTF_RANGEATK`

**Effect:** Increase Long-ranged damage while attacking

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Damage (not be shown in status window) |

**Example:**
```c
sc_start SC_MTF_RANGEATK, 60000, 10;  // 60 seconds
```

---

### SC_MTF_RANGEATK2

**Icon:** `EFST_MTF_RANGEATK2`

**Effect:** Increase Long-ranged damage while attacking

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Damage (not be shown in status window) |

**Example:**
```c
sc_start SC_MTF_RANGEATK2, 60000, 10;  // 60 seconds
```

---

### SC_MTF_MATK

**Icon:** `EFST_MTF_MATK`

**Effect:** Increase MATK damage while attacking

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% MATK |

**Example:**
```c
sc_start SC_MTF_MATK, 60000, 10;  // 60 seconds
```

---

### SC_MTF_MATK2

**Icon:** `EFST_MTF_MATK2`

**Effect:** Increase MATK damage while attacking

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + MATK |

**Example:**
```c
sc_start SC_MTF_MATK2, 60000, 10;  // 60 seconds
```

---

### SC_MTF_MLEATKED

**Icon:** `EFST_MTF_MLEATKED`

**Effect:** Has chance to cast Endure to self while attacked

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Endure Level |
| val2 | Rate to cast |
| val3 | Neutral element resistance |

**Example:**
```c
sc_start SC_MTF_MLEATKED, 60000, 10;  // 60 seconds
```

---

### SC_MTF_CRIDAMAGE

**Icon:** `EFST_MTF_CRIDAMAGE`

**Effect:** Bonus critical rate of monster transformation

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Critical |

**Example:**
```c
sc_start SC_MTF_CRIDAMAGE, 60000, 10;  // 60 seconds
```

---

### SC_OKTOBERFEST

**Effect:** Costume

**Example:**
```c
sc_start SC_OKTOBERFEST, 60000, 1;
```

---

### SC_STRANGELIGHTS

**Icon:** `EFST_STRANGELIGHTS`

**Example:**
```c
sc_start SC_STRANGELIGHTS, 60000, 1;
```

---

### SC_DECORATION_OF_MUSIC

**Icon:** `EFST_DECORATION_OF_MUSIC`

**Example:**
```c
sc_start SC_DECORATION_OF_MUSIC, 60000, 1;
```

---

### SC_QUEST_BUFF1

**Icon:** `EFST_QUEST_BUFF1`

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +ATK & +MATK |

**Example:**
```c
sc_start SC_QUEST_BUFF1, 60000, 10;  // 60 seconds
```

---

### SC_QUEST_BUFF2

**Icon:** `EFST_QUEST_BUFF2`

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +ATK & +MATK |

**Example:**
```c
sc_start SC_QUEST_BUFF2, 60000, 10;  // 60 seconds
```

---

### SC_QUEST_BUFF3

**Icon:** `EFST_QUEST_BUFF3`

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +ATK & +MATK |

**Example:**
```c
sc_start SC_QUEST_BUFF3, 60000, 10;  // 60 seconds
```

---

### SC_ALL_RIDING

**Icon:** `EFST_ALL_RIDING`

**Example:**
```c
sc_start SC_ALL_RIDING, 60000, 1;
```

---

### SC__FEINTBOMB

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | -1 SP each second |

**Example:**
```c
sc_start SC__FEINTBOMB, 60000, 1;
```

---

### SC__CHAOS

**Example:**
```c
sc_start SC__CHAOS, 60000, 1;
```

---

### SC_ELEMENTAL_SHIELD

**Effect:** Block magic attack

**Example:**
```c
sc_start SC_ELEMENTAL_SHIELD, 60000, 1;
```

---

### SC_CHASEWALK2

**Icon:** `EFST_CHASEWALK2`

**Effect:** 2nd effect of Chasewalk

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +STR |

**Example:**
```c
sc_start SC_CHASEWALK2, 60000, 10;  // 60 seconds
```

---

### SC_SUHIDE

**Icon:** `EFST_SUHIDE`

**Effect:** Hide caster. Can be seen by insect, demon, and boss. Cannot move or pickup items.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |

**Example:**
```c
sc_start SC_SUHIDE, 60000, 10;  // 60 seconds
```

---

### SC_SU_STOOP

**Icon:** `EFST_SU_STOOP`

**Effect:** Places a temporary buff on the user that decreases all damage taken by 90%.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |

**Example:**
```c
sc_start SC_SU_STOOP, 60000, 10;  // 60 seconds
```

---

### SC_SPRITEMABLE

**Icon:** `EFST_SPRITEMABLE`

**Effect:** Increase 1000 HP and 100 SP.

**Example:**
```c
sc_start SC_SPRITEMABLE, 60000, 1;
```

---

### SC_CATNIPPOWDER

**Icon:** `EFST_CATNIPPOWDER`

**Effect:** Reduces ATK and MATK by 50% to targets in a 3x3~7x7 area. HP and SP recovery rate increase.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |
| val2 | WATK% / MATK% |
| val3 | Movement speed reduction |

**Example:**
```c
sc_start SC_CATNIPPOWDER, 60000, 10;  // 60 seconds
```

---

### SC_SV_ROOTTWIST

**Icon:** `EFST_SV_ROOTTWIST`

**Effect:** Prevents the target from moving and receives 100 Poison damage every second. Cannot be used on Boss monsters.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |

**Example:**
```c
sc_start SC_SV_ROOTTWIST, 60000, 10;  // 60 seconds
```

---

### SC_BITESCAR

**Icon:** `EFST_BITESCAR`

**Effect:** Drains a portion of the target's Max HP each second.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |
| val2 | Max HP% damage |
| val4 | Tick |

**Example:**
```c
sc_start SC_BITESCAR, 60000, 10;  // 60 seconds
```

---

### SC_ARCLOUSEDASH

**Icon:** `EFST_ARCLOUSEDASH`

**Effect:** Increases Agi and movement speed.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | AGI |
| val2 | Movement speed increase |
| val4 | Ranged ATK increase for Doram |

**Example:**
```c
sc_start SC_ARCLOUSEDASH, 60000, 10;  // 60 seconds
```

---

### SC_TUNAPARTY

**Icon:** `EFST_TUNAPARTY`

**Effect:** Protects from damage, the amount is based on Max HP.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Max HP% to absorb |
| val2 | Double the shield life with Spirit of Sea |

**Example:**
```c
sc_start SC_TUNAPARTY, 60000, 10;  // 60 seconds
```

---

### SC_SHRIMP

**Icon:** `EFST_SHRIMP`

**Effect:** Gives all party members on screen +10% ATK and MATK.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | BATK% / MATK% |

**Example:**
```c
sc_start SC_SHRIMP, 60000, 10;  // 60 seconds
```

---

### SC_FRESHSHRIMP

**Icon:** `EFST_FRESHSHRIMP`

**Effect:** Recovers a small amount of HP. Each level reduces the time between each HP recovery tick.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |
| val2 | Heal amount |
| val4 | Tick |

**Example:**
```c
sc_start SC_FRESHSHRIMP, 60000, 10;  // 60 seconds
```

---

### SC_HISS

**Icon:** `EFST_HISS`

**Effect:** Increases movement speed and perfect dodge of the user and his party.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |
| val2 | Perfect Dodge |

**Example:**
```c
sc_start SC_HISS, 60000, 10;  // 60 seconds
```

---

### SC_NYANGGRASS

**Icon:** `EFST_NYANGGRASS`

**Effect:** Reduces monster's DEF and MDEF by 50%. Reduces other player's equipment DEF and MDEF to 0.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |

**Example:**
```c
sc_start SC_NYANGGRASS, 60000, 10;  // 60 seconds
```

---

### SC_GROOMING

**Icon:** `EFST_GROOMING`

**Effect:** FLEE + 100. Cures Poison, Frozen, Stun, Sleep, Bleeding, Silence, Crystallization, Deep Sleep, Fear, and Mandragora Howling.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |
| val2 | FLEE |

**Example:**
```c
sc_start SC_GROOMING, 60000, 10;  // 60 seconds
```

---

### SC_CHATTERING

**Icon:** `EFST_CHATTERING`

**Effect:** Increases the player's ATK and MATK by 100. Increases the player's movespeed.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Skill Lv |
| val2 | ATK / MATK |

**Example:**
```c
sc_start SC_CHATTERING, 60000, 10;  // 60 seconds
```

---

### SC_DORAM_WALKSPEED

**Effect:** Adjusts player's walk speed.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Movement speed adjustment |

**Example:**
```c
sc_start SC_DORAM_WALKSPEED, 60000, 10;  // 60 seconds
```

---

### SC_DORAM_MATK

**Effect:** Statically increases MATK for Spirit of Land.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | MATK |

**Example:**
```c
sc_start SC_DORAM_MATK, 60000, 10;  // 60 seconds
```

---

### SC_DORAM_FLEE2

**Effect:** Statically increase FLEE2 for Spirit of Land.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | FLEE2 |

**Example:**
```c
sc_start SC_DORAM_FLEE2, 60000, 10;  // 60 seconds
```

---

### SC_DORAM_SVSP

**Effect:** Casts Silvervine Stem Spear when receiving Magic or Ranged damage after using Catnip Meteor for Spirit of Land.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Value to know it's active |

**Example:**
```c
sc_start SC_DORAM_SVSP, 60000, 10;  // 60 seconds
```

---

### SC_GVG_GIANT

**Icon:** `EFST_GVG_GIANT`

**Effect:** Instantly consumes HP/SP, increases Physical/Magic damage on player enemies by n%.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |
| val3 | Increases % Physical damage |
| val4 | Increases % Magical damage |

**Example:**
```c
sc_start SC_GVG_GIANT, 60000, 10;  // 60 seconds
```

---

### SC_GVG_GOLEM

**Icon:** `EFST_GVG_GOLEM`

**Effect:** Instantly consumes HP/SP, decreases n% damage received from other adventurers.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |
| val3 | Decreases % damage received of physical attack |
| val4 | Decreases % damage received of magical attack |

**Example:**
```c
sc_start SC_GVG_GOLEM, 60000, 10;  // 60 seconds
```

---

### SC_GVG_FREEZ

**Icon:** `EFST_GVG_FREEZ`

**Effect:** Instantly consumes HP/SP, immunizes you against Frost.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | Amount of HP that are instantly consumed |
| val2 | Amount of SP that are instantly consumed |

**Example:**
```c
sc_start SC_GVG_FREEZ, 60000, 10;  // 60 seconds
```

---

### SC_EXTREMITYFIST2

**Example:**
```c
sc_start SC_EXTREMITYFIST2, 60000, 1;
```

---

### SC_LHZ_DUN_N1

**Icon:** `EFST_LHZ_DUN_N1`

**Effect:** Increases damage against Swordman, Thief and reduces damage taken from Acolyte, Merchant monsters of Biolab 5 (except MVPs).

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Damage |
| val2 | +% Defense |

**Example:**
```c
sc_start SC_LHZ_DUN_N1, 60000, 10;  // 60 seconds
```

---

### SC_LHZ_DUN_N2

**Icon:** `EFST_LHZ_DUN_N2`

**Effect:** Increases damage against Acolyte, Merchant and reduces damage taken from Mage, Archer monsters of Biolab 5 (except MVPs).

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Damage |
| val2 | +% Defense |

**Example:**
```c
sc_start SC_LHZ_DUN_N2, 60000, 10;  // 60 seconds
```

---

### SC_LHZ_DUN_N3

**Icon:** `EFST_LHZ_DUN_N3`

**Effect:** Increases damage against Mage, Archer and reduces damage taken from Swordman, Thief monsters of Biolab 5 (except MVPs).

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Damage |
| val2 | +% Defense |

**Example:**
```c
sc_start SC_LHZ_DUN_N3, 60000, 10;  // 60 seconds
```

---

### SC_LHZ_DUN_N4

**Icon:** `EFST_LHZ_DUN_N4`

**Effect:** Increases and reduces damage against MVPs of Biolab 5.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Damage |
| val2 | +% Defense |

**Example:**
```c
sc_start SC_LHZ_DUN_N4, 60000, 10;  // 60 seconds
```

---

### SC_DORAM_BUF_01

**Effect:** Recovers 10 HP every 10 seconds.

**Example:**
```c
sc_start SC_DORAM_BUF_01, 60000, 1;
```

---

### SC_DORAM_BUF_02

**Effect:** Recovers 5 SP every 10 seconds.

**Example:**
```c
sc_start SC_DORAM_BUF_02, 60000, 1;
```

---

### SC_INCREASE_MAXHP

**Icon:** `EFST_ATKER_ASPD`

**Effect:** Increases MaxHP. Increases natural HP regeneration.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + HP |
| val2 | +% HP regeneration |

**Example:**
```c
sc_start SC_INCREASE_MAXHP, 60000, 10;  // 60 seconds
```

---

### SC_INCREASE_MAXSP

**Icon:** `EFST_ATKER_MOVESPEED`

**Effect:** Increases MaxSP. Increases natural SP regeneration.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + SP |
| val2 | +% SP regeneration |

**Example:**
```c
sc_start SC_INCREASE_MAXSP, 60000, 10;  // 60 seconds
```

---

### SC_ADD_ATK_DAMAGE

**Icon:** `EFST_ADD_ATK_DAMAGE`

**Effect:** Increases melee physical damage by 15%. Increases ranged physical damage by 15%.

**Example:**
```c
sc_start SC_ADD_ATK_DAMAGE, 60000, 1;
```

---

### SC_ADD_MATK_DAMAGE

**Icon:** `EFST_ADD_MATK_DAMAGE`

**Effect:** Increases all elemental magical damage by 15%.

**Example:**
```c
sc_start SC_ADD_MATK_DAMAGE, 60000, 1;
```

---

### SC_HELPANGEL

**Icon:** `EFST_HELPANGEL`

**Effect:** Recover 1000 HP every second. Recover 350 SP every second.

**Parameters:**

| Param | Usage |
|-------|-------|
| val4 | Tick time (milliseconds) |

**Example:**
```c
sc_start SC_HELPANGEL, 60000, 1;
```

---

### SC_SOUNDOFDESTRUCTION

**Icon:** `EFST_SOUND_OF_DESTRUCTION`

**Effect:** Doubles incoming damage for 10 seconds.

**Example:**
```c
sc_start SC_SOUNDOFDESTRUCTION, 60000, 1;
```

---

### SC_LUXANIMA

**Icon:** `EFST_LUXANIMA`

**Effect:** Physical attacks has the chance to activate Storm Blast Level 1. Increases physical damage against all sizes.

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | Storm Blast success 15% (hardcoded) |
| val3 | Damage/HP/SP 30% increase (hardcoded) |

**Example:**
```c
sc_start SC_LUXANIMA, 60000, 1;
```

---

### SC_REUSE_LIMIT_LUXANIMA

**Example:**
```c
sc_start SC_REUSE_LIMIT_LUXANIMA, 60000, 1;
```

---

### SC_ENSEMBLEFATIGUE

**Icon:** `EFST_ENSEMBLEFATIGUE`

**Effect:** Disables skill use. Movement and attack speed reduced by 30%.

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | + 30 Speed and ASPD rates penalty (hardcoded) |

**Example:**
```c
sc_start SC_ENSEMBLEFATIGUE, 60000, 1;
```

---

### SC_MISTY_FROST

**Icon:** `EFST_MISTY_FROST`

**Effect:** Freezing.

**Example:**
```c
sc_start SC_MISTY_FROST, 60000, 1;
```

---

### SC_EP16_2_BUFF_SS

**Icon:** `EFST_EP16_2_BUFF_SS`

**Effect:** ASPD +10.

**Example:**
```c
sc_start SC_EP16_2_BUFF_SS, 60000, 1;
```

---

### SC_EP16_2_BUFF_SC

**Icon:** `EFST_EP16_2_BUFF_SC`

**Effect:** CRIT +30.

**Example:**
```c
sc_start SC_EP16_2_BUFF_SC, 60000, 1;
```

---

### SC_EP16_2_BUFF_AC

**Icon:** `EFST_EP16_2_BUFF_AC`

**Effect:** Reduce variable cast time by 80%.

**Example:**
```c
sc_start SC_EP16_2_BUFF_AC, 60000, 1;
```

---

### SC_EMERGENCY_MOVE

**Icon:** `EFST_INC_AGI`

**Effect:** Increase AGI and walkspeed, AL_INCAGI effect.

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | Movement speed +25 (hardcoded) |

**Example:**
```c
sc_start SC_EMERGENCY_MOVE, 60000, 1;
```

---

### SC_PACKING_ENVELOPE1

**Icon:** `EFST_PACKING_ENVELOPE1`

**Effect:** Increases ATK

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + watk |

**Example:**
```c
sc_start SC_PACKING_ENVELOPE1, 60000, 10;  // 60 seconds
```

---

### SC_PACKING_ENVELOPE2

**Icon:** `EFST_PACKING_ENVELOPE2`

**Effect:** Increases MATK

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + ematk |

**Example:**
```c
sc_start SC_PACKING_ENVELOPE2, 60000, 10;  // 60 seconds
```

---

### SC_PACKING_ENVELOPE3

**Icon:** `EFST_PACKING_ENVELOPE3`

**Effect:** Increases MaxHP

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% MaxHP |

**Example:**
```c
sc_start SC_PACKING_ENVELOPE3, 60000, 10;  // 60 seconds
```

---

### SC_PACKING_ENVELOPE4

**Icon:** `EFST_PACKING_ENVELOPE4`

**Effect:** Increases MaxSP

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% MaxSP |

**Example:**
```c
sc_start SC_PACKING_ENVELOPE4, 60000, 10;  // 60 seconds
```

---

### SC_PACKING_ENVELOPE5

**Icon:** `EFST_PACKING_ENVELOPE5`

**Effect:** Increases FLEE

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + Flee |

**Example:**
```c
sc_start SC_PACKING_ENVELOPE5, 60000, 10;  // 60 seconds
```

---

### SC_PACKING_ENVELOPE6

**Icon:** `EFST_PACKING_ENVELOPE6`

**Effect:** Increases ASPD

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + ASPD |

**Example:**
```c
sc_start SC_PACKING_ENVELOPE6, 60000, 10;  // 60 seconds
```

---

### SC_PACKING_ENVELOPE7

**Icon:** `EFST_PACKING_ENVELOPE7`

**Effect:** Increases DEF

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + DEF |

**Example:**
```c
sc_start SC_PACKING_ENVELOPE7, 60000, 10;  // 60 seconds
```

---

### SC_PACKING_ENVELOPE8

**Icon:** `EFST_PACKING_ENVELOPE8`

**Effect:** Increases MDEF

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + MDEF |

**Example:**
```c
sc_start SC_PACKING_ENVELOPE8, 60000, 10;  // 60 seconds
```

---

### SC_PACKING_ENVELOPE9

**Icon:** `EFST_PACKING_ENVELOPE9`

**Effect:** Increases Critical rate

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + Critical rate |

**Example:**
```c
sc_start SC_PACKING_ENVELOPE9, 60000, 10;  // 60 seconds
```

---

### SC_PACKING_ENVELOPE10

**Icon:** `EFST_PACKING_ENVELOPE10`

**Effect:** Increase Speed and Flee.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Walkspeed |
| val2 | +% Flee |

**Example:**
```c
sc_start SC_PACKING_ENVELOPE10, 60000, 10;  // 60 seconds
```

---

### SC_BATH_FOAM_A

**Icon:** `EFST_BATH_FOAM_A`

**Effect:** Increases physical and magical damage against Meditathio Dungeon Monsters.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% damage |

**Example:**
```c
sc_start SC_BATH_FOAM_A, 60000, 10;  // 60 seconds
```

---

### SC_BATH_FOAM_B

**Icon:** `EFST_BATH_FOAM_B`

**Effect:** Increases physical and magical damage against Meditathio Dungeon Monsters.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% damage |

**Example:**
```c
sc_start SC_BATH_FOAM_B, 60000, 10;  // 60 seconds
```

---

### SC_BATH_FOAM_C

**Icon:** `EFST_BATH_FOAM_C`

**Effect:** Increases physical and magical damage against Meditathio Dungeon Monsters.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% damage |

**Example:**
```c
sc_start SC_BATH_FOAM_C, 60000, 10;  // 60 seconds
```

---

### SC_BUCHEDENOEL

**Icon:** `EFST_BUCHEDENOEL`

**Effect:** Increases HP & SP restoration by 3%, Hit +3, and Critical +7.

**Example:**
```c
sc_start SC_BUCHEDENOEL, 60000, 1;
```

---

### SC_EP16_DEF

**Icon:** `EFST_EP16_DEF`

**Effect:** Decrease physical and magical damage against monsters in the Room of Consciousness and Prontera Invasion Dungeon. Restores 1000 HP. Cures Curse, Poison and Silence.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% reduction |

**Example:**
```c
sc_start SC_EP16_DEF, 60000, 10;  // 60 seconds
```

---

### SC_STR_SCROLL

**Icon:** `EFST_STR_SCROLL`

**Effect:** Increases STR.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + STR |

**Example:**
```c
sc_start SC_STR_SCROLL, 60000, 10;  // 60 seconds
```

---

### SC_INT_SCROLL

**Icon:** `EFST_INT_SCROLL`

**Effect:** Increases INT.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + INT |

**Example:**
```c
sc_start SC_INT_SCROLL, 60000, 10;  // 60 seconds
```

---

### SC_CONTENTS_1

**Icon:** `EFST_CONTENTS_1`

**Effect:** Increase physical and magical damage to all element enemies

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% damage |

**Example:**
```c
sc_start SC_CONTENTS_1, 60000, 10;  // 60 seconds
```

---

### SC_CONTENTS_2

**Icon:** `EFST_CONTENTS_2`

**Effect:** Increase melee physical damage, range physical damage, and all elemental magic damage.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% damage |

**Example:**
```c
sc_start SC_CONTENTS_2, 60000, 10;  // 60 seconds
```

---

### SC_CONTENTS_3

**Icon:** `EFST_CONTENTS_3`

**Effect:** Increase ATK and MATK

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% damage |

**Example:**
```c
sc_start SC_CONTENTS_3, 60000, 10;  // 60 seconds
```

---

### SC_CONTENTS_4

**Icon:** `EFST_CONTENTS_4`

**Effect:** Increase ATK and MATK

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% damage |

**Example:**
```c
sc_start SC_CONTENTS_4, 60000, 10;  // 60 seconds
```

---

### SC_CONTENTS_5

**Icon:** `EFST_CONTENTS_5`

**Effect:** Increase ASPD and reduce variable casttime

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% increase ASPD, -% reduce variable casttime |

**Example:**
```c
sc_start SC_CONTENTS_5, 60000, 10;  // 60 seconds
```

---

### SC_CONTENTS_6

**Icon:** `EFST_CONTENTS_6`

**Effect:** Increase physical and magical damage to Dragon and Plant race.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% damage |

**Example:**
```c
sc_start SC_CONTENTS_6, 60000, 10;  // 60 seconds
```

---

### SC_CONTENTS_7

**Icon:** `EFST_CONTENTS_7`

**Effect:** Increase physical and magical damage to Demon and Undead race.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% damage |

**Example:**
```c
sc_start SC_CONTENTS_7, 60000, 10;  // 60 seconds
```

---

### SC_CONTENTS_8

**Icon:** `EFST_CONTENTS_8`

**Effect:** Increase physical and magical damage to Formless and Fish race.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% damage |

**Example:**
```c
sc_start SC_CONTENTS_8, 60000, 10;  // 60 seconds
```

---

### SC_CONTENTS_9

**Icon:** `EFST_CONTENTS_9`

**Effect:** Increase physical and magical damage to Angel and Brute race.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% damage |

**Example:**
```c
sc_start SC_CONTENTS_9, 60000, 10;  // 60 seconds
```

---

### SC_CONTENTS_10

**Icon:** `EFST_CONTENTS10`

**Effect:** Increase physical and magical damage to Insect and Demihuman race.

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% damage |

**Example:**
```c
sc_start SC_CONTENTS_10, 60000, 10;  // 60 seconds
```

---

## Food & Consumables

<!-- RAG_CHUNK: sc_food__consumables -->

### SC_ASPDPOTION0

**Icon:** `EFST_ATTHASTE_POTION1`

**Effect:** Increase ASPD, won't be stacked with SC_ASPDPOTION1, SC_ASPDPOTION2, SC_ASPDPOTION3

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +ASPD (Renewal) |
| val2 | +% ASPD (Pre-Renewal) |

**Example:**
```c
sc_start SC_ASPDPOTION0, 60000, 10;  // 60 seconds
```

---

### SC_ASPDPOTION1

**Icon:** `EFST_ATTHASTE_POTION2`

**Effect:** Increase ASPD, won't be stacked with SC_ASPDPOTION0, SC_ASPDPOTION2, SC_ASPDPOTION3

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +ASPD (Renewal) |
| val2 | +% ASPD (Pre-Renewal) |

**Example:**
```c
sc_start SC_ASPDPOTION1, 60000, 10;  // 60 seconds
```

---

### SC_ASPDPOTION2

**Icon:** `EFST_ATTHASTE_POTION3`

**Effect:** Increase ASPD, won't be stacked with SC_ASPDPOTION0, SC_ASPDPOTION1, SC_ASPDPOTION3

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +ASPD (Renewal) |
| val2 | +% ASPD (Pre-Renewal) |

**Example:**
```c
sc_start SC_ASPDPOTION2, 60000, 10;  // 60 seconds
```

---

### SC_ASPDPOTION3

**Icon:** `EFST_ATTHASTE_INFINITY`

**Effect:** Increase ASPD, won't be stacked with SC_ASPDPOTION0, SC_ASPDPOTION1, SC_ASPDPOTION2

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | + ASPD (Renewal) |
| val2 | +% ASPD (Pre-Renewal) |

**Example:**
```c
sc_start SC_ASPDPOTION3, 60000, 10;  // 60 seconds
```

---

### SC_ATKPOTION

**Icon:** `EFST_PLUSATTACKPOWER`

**Effect:** Increase Atk

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +Atk |

**Example:**
```c
sc_start SC_ATKPOTION, 60000, 10;  // 60 seconds
```

---

### SC_MATKPOTION

**Icon:** `EFST_PLUSMAGICPOWER`

**Effect:** Increase MAtk

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +MAtk |

**Example:**
```c
sc_start SC_MATKPOTION, 60000, 10;  // 60 seconds
```

---

### SC_CARTBOOST

**Icon:** `EFST_CARTBOOST`

**Example:**
```c
sc_start SC_CARTBOOST, 60000, 1;
```

---

### SC_STRFOOD

**Icon:** `EFST_FOOD_STR`

**Effect:** Increase STR (cannot be stacked with SC_FOOD_STR_CASH, ignored if value is lower)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +STR |

**Example:**
```c
sc_start SC_STRFOOD, 60000, 10;  // 60 seconds
```

---

### SC_AGIFOOD

**Icon:** `EFST_FOOD_AGI`

**Effect:** Increase AGI (cannot be stacked with SC_FOOD_AGI_CASH, ignored if value is lower)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +AGI |

**Example:**
```c
sc_start SC_AGIFOOD, 60000, 10;  // 60 seconds
```

---

### SC_VITFOOD

**Icon:** `EFST_FOOD_VIT`

**Effect:** Increase VIT (cannot be stacked with SC_FOOD_VIT_CASH, ignored if value is lower)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +VIT |

**Example:**
```c
sc_start SC_VITFOOD, 60000, 10;  // 60 seconds
```

---

### SC_INTFOOD

**Icon:** `EFST_FOOD_INT`

**Effect:** Increase INT (cannot be stacked with SC_FOOD_INT_CASH, ignored if value is lower)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +INT |

**Example:**
```c
sc_start SC_INTFOOD, 60000, 10;  // 60 seconds
```

---

### SC_DEXFOOD

**Icon:** `EFST_FOOD_DEX`

**Effect:** Increase DEX (cannot be stacked with SC_FOOD_DEX_CASH, ignored if value is lower)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +DEX |

**Example:**
```c
sc_start SC_DEXFOOD, 60000, 10;  // 60 seconds
```

---

### SC_LUKFOOD

**Icon:** `EFST_FOOD_LUK`

**Effect:** Increase LUK (cannot be stacked with SC_FOOD_LUK_CASH, ignored if value is lower)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +LUK |

**Example:**
```c
sc_start SC_LUKFOOD, 60000, 10;  // 60 seconds
```

---

### SC_HITFOOD

**Icon:** `EFST_FOOD_BASICHIT`

**Effect:** Increase HIT (food-type effect)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +Hit |

**Example:**
```c
sc_start SC_HITFOOD, 60000, 10;  // 60 seconds
```

---

### SC_FLEEFOOD

**Icon:** `EFST_FOOD_BASICAVOIDANCE`

**Effect:** Increase FLEE (food-type effect)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +Flee |

**Example:**
```c
sc_start SC_FLEEFOOD, 60000, 10;  // 60 seconds
```

---

### SC_BATKFOOD

**Effect:** Increase Base Attack (food-type effect)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +BaseAttack |

**Example:**
```c
sc_start SC_BATKFOOD, 60000, 10;  // 60 seconds
```

---

### SC_WATKFOOD

**Effect:** Increase Weapon Attack (food-type effect)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +WeaponAttack |

**Example:**
```c
sc_start SC_WATKFOOD, 60000, 10;  // 60 seconds
```

---

### SC_MATKFOOD

**Effect:** Increase Magic Attack (food-type effect)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +MagicAttack |

**Example:**
```c
sc_start SC_MATKFOOD, 60000, 10;  // 60 seconds
```

---

### SC_EXPBOOST

**Icon:** `EFST_CASH_PLUSEXP`

**Effect:** Increase EXP rate

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% EXP |

**Example:**
```c
sc_start SC_EXPBOOST, 60000, 10;  // 60 seconds
```

---

### SC_ITEMBOOST

**Icon:** `EFST_CASH_RECEIVEITEM`

**Effect:** Increase Drop rate

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Drop |

**Example:**
```c
sc_start SC_ITEMBOOST, 60000, 10;  // 60 seconds
```

---

### SC_S_LIFEPOTION

**Icon:** `EFST_S_LIFEPOTION`

**Effect:** Increase HP each interval

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | if < 0 will be percentage. If > 0 is fixed HP heal value |
| val2 | Interval per seconds |

**Example:**
```c
sc_start SC_S_LIFEPOTION, 60000, 10;  // 60 seconds
```

---

### SC_L_LIFEPOTION

**Icon:** `EFST_L_LIFEPOTION`

**Effect:** Increase HP each interval

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | if < 0 will be percentage. If > 0 is fixed HP heal value |
| val2 | Interval per seconds |

**Example:**
```c
sc_start SC_L_LIFEPOTION, 60000, 10;  // 60 seconds
```

---

### SC_JEXPBOOST

**Example:**
```c
sc_start SC_JEXPBOOST, 60000, 1;
```

---

### SC_FOOD_STR_CASH

**Icon:** `EFST_FOOD_STR_CASH`

**Effect:** Increase STR (cannot be stacked with SC_STRFOOD, ignored if value is lower)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +STR |

**Example:**
```c
sc_start SC_FOOD_STR_CASH, 60000, 10;  // 60 seconds
```

---

### SC_FOOD_AGI_CASH

**Icon:** `EFST_FOOD_AGI_CASH`

**Effect:** Increase AGI (cannot be stacked with SC_AGIFOOD, ignored if value is lower)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +AGI |

**Example:**
```c
sc_start SC_FOOD_AGI_CASH, 60000, 10;  // 60 seconds
```

---

### SC_FOOD_VIT_CASH

**Icon:** `EFST_FOOD_VIT_CASH`

**Effect:** Increase VIT (cannot be stacked with SC_VITFOOD, ignored if value is lower)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +VIT |

**Example:**
```c
sc_start SC_FOOD_VIT_CASH, 60000, 10;  // 60 seconds
```

---

### SC_FOOD_DEX_CASH

**Icon:** `EFST_FOOD_DEX_CASH`

**Effect:** Increase DEX (cannot be stacked with SC_DEXFOOD, ignored if value is lower)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +DEX |

**Example:**
```c
sc_start SC_FOOD_DEX_CASH, 60000, 10;  // 60 seconds
```

---

### SC_FOOD_INT_CASH

**Icon:** `EFST_FOOD_INT_CASH`

**Effect:** Increase INT (cannot be stacked with SC_INTFOOD, ignored if value is lower)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +INT |

**Example:**
```c
sc_start SC_FOOD_INT_CASH, 60000, 10;  // 60 seconds
```

---

### SC_FOOD_LUK_CASH

**Icon:** `EFST_FOOD_LUK_CASH`

**Effect:** Increase LUK (cannot be stacked with SC_LUKFOOD, ignored if value is lower)

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +LUK |

**Example:**
```c
sc_start SC_FOOD_LUK_CASH, 60000, 10;  // 60 seconds
```

---

### SC_STEALTHFIELD

**Example:**
```c
sc_start SC_STEALTHFIELD, 60000, 1;
```

---

### SC_STEALTHFIELD_MASTER

**Example:**
```c
sc_start SC_STEALTHFIELD_MASTER, 60000, 1;
```

---

### SC_GN_CARTBOOST

**Example:**
```c
sc_start SC_GN_CARTBOOST, 60000, 1;
```

---

### SC_TEARGAS

**Example:**
```c
sc_start SC_TEARGAS, 60000, 1;
```

---

### SC_SAVAGE_STEAK

**Icon:** `EFST_SAVAGE_STEAK`

**Effect:** Increase STR

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +STR |

**Example:**
```c
sc_start SC_SAVAGE_STEAK, 60000, 10;  // 60 seconds
```

---

### SC_MINOR_BBQ

**Icon:** `EFST_MINOR_BBQ`

**Effect:** Increase VIT

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +VIT |

**Example:**
```c
sc_start SC_MINOR_BBQ, 60000, 10;  // 60 seconds
```

---

### SC_SIROMA_ICE_TEA

**Icon:** `EFST_SIROMA_ICE_TEA`

**Effect:** Increase DEX

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +DEX |

**Example:**
```c
sc_start SC_SIROMA_ICE_TEA, 60000, 10;  // 60 seconds
```

---

### SC_DROCERA_HERB_STEAMED

**Icon:** `EFST_DROCERA_HERB_STEAMED`

**Effect:** Increase AGI

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +AGI |

**Example:**
```c
sc_start SC_DROCERA_HERB_STEAMED, 60000, 10;  // 60 seconds
```

---

### SC_BOOST500

**Icon:** `EFST_BOOST500`

**Effect:** Increase ASPD rate

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% Aspd |

**Example:**
```c
sc_start SC_BOOST500, 60000, 10;  // 60 seconds
```

---

### SC_EXTRACT_WHITE_POTION_Z

**Icon:** `EFST_EXTRACT_WHITE_POTION_Z`

**Effect:** Increase HP regen rate

**Parameters:**

| Param | Usage |
|-------|-------|
| val1 | +% HP regen |

**Example:**
```c
sc_start SC_EXTRACT_WHITE_POTION_Z, 60000, 10;  // 60 seconds
```

---

### SC_OVERED_BOOST

**Icon:** `EFST_OVERED_BOOST`

**Effect:** When status ended, reduce 50% HP for player and increase 50 the Homunculus's hunger

**Parameters:**

| Param | Usage |
|-------|-------|
| val2 | Fixed Flee value |
| val3 | Fixed ASPD value |
| val4 | -% Def |

**Example:**
```c
sc_start SC_OVERED_BOOST, 60000, 1;
```

---

### SC_TEARGAS_SOB

**Effect:** 2nd Teargas effect, do /sob expression each 3 seconds

**Example:**
```c
sc_start SC_TEARGAS_SOB, 60000, 1;
```

---

### SC_REF_T_POTION

**Icon:** `EFST_REF_T_POTION`

**Effect:** Decreases reflected damage by 100%.

**Example:**
```c
sc_start SC_REF_T_POTION, 60000, 1;
```

---

