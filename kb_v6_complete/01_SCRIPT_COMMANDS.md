# rAthena KB v6 - Script Commands Complete Reference

**Version:** 6.0 Complete
**Generated:** 2025-11-26
**Source:** doc/script_commands.txt
**Total Commands:** 768

---

## Quick Navigation

### By Category
- [Basic Output](#basic-output) - mes, next, close, clear
- [Menu & Input](#menu--input) - menu, select, input, prompt
- [Variables](#variables) - set, getarg, setarray
- [Player Data](#player-data) - getcharid, strcharinfo, readparam
- [Items](#items) - getitem, delitem, countitem
- [Math & Logic](#math--logic) - rand, min, max, pow
- [Control Flow](#control-flow) - if, for, while, switch
- [Timers](#timers) - addtimer, deltimer, sleep
- [Maps & Warps](#maps--warps) - warp, areawarp, mapannounce
- [Monsters](#monsters) - monster, killmonster, mobcount
- [NPCs](#npcs) - setnpcdisplay, donpcevent, enablenpc
- [Parties & Guilds](#parties--guilds) - getpartymember, getguildmember
- [Instances](#instances) - instance_create, instance_attach
- [Status Effects](#status-effects) - sc_start, sc_end, getstatus
- [Skills](#skills) - skill, addtoskill, skilleffect
- [Database Access](#database-access) - query_sql, escape_sql

### Alphabetical Index

**A:** [achievementadd](#achievementadd) | [achievementcomplete](#achievementcomplete) | [achievementexists](#achievementexists) | [achievementinfo](#achievementinfo) | [achievementremove](#achievementremove) | [achievementupdate](#achievementupdate) | [activatepset](#activatepset) | [active_transform](#active_transform) | [active_transform](#active_transform) | [add_reputation_points](#add_reputation_points) | [addfame](#addfame) | [addhomintimacy](#addhomintimacy) | [addmonsterdrop](#addmonsterdrop) | [addmonsterdrop](#addmonsterdrop) | [addrid](#addrid) | [addspiritball](#addspiritball) | [addtimer](#addtimer) | [addtimercount](#addtimercount) | [addtoskill](#addtoskill) | [addtoskill](#addtoskill) | [adopt](#adopt) | [adopt](#adopt) | [agitcheck](#agitcheck) | [agitcheck2](#agitcheck2) | [agitcheck3](#agitcheck3) | [agitend](#agitend) | [agitend2](#agitend2) | [agitend3](#agitend3) | [agitstart](#agitstart) | [agitstart2](#agitstart2) | [agitstart3](#agitstart3) | [announce](#announce) | [areaannounce](#areaannounce) | [areamobuseskill](#areamobuseskill) | [areamobuseskill](#areamobuseskill) | [areamobuseskill](#areamobuseskill) | [areamobuseskill](#areamobuseskill) | [areamonster](#areamonster) | [areamonster](#areamonster) | [areapercentheal](#areapercentheal) | [areawarp](#areawarp) | [atcommand](#atcommand) | [atoi](#atoi) | [attachnpctimer](#attachnpctimer) | [attachrid](#attachrid) | [autobonus](#autobonus) | [autobonus2](#autobonus2) | [autobonus3](#autobonus3) | [autobonus3](#autobonus3) | [autoequip](#autoequip) | [autoloot](#autoloot) | [awake](#awake) | [axtoi](#axtoi) | 
**B:** [basicskillcheck](#basicskillcheck) | [bg_create](#bg_create) | [bg_desert](#bg_desert) | [bg_destroy](#bg_destroy) | [bg_get_data](#bg_get_data) | [bg_getareausers](#bg_getareausers) | [bg_info](#bg_info) | [bg_join](#bg_join) | [bg_leave](#bg_leave) | [bg_monster](#bg_monster) | [bg_monster](#bg_monster) | [bg_monster_set_team](#bg_monster_set_team) | [bg_reserve](#bg_reserve) | [bg_team_setxy](#bg_team_setxy) | [bg_unbook](#bg_unbook) | [bg_updatescore](#bg_updatescore) | [bg_warp](#bg_warp) | [bindatcmd](#bindatcmd) | [birthpet](#birthpet) | [bonus](#bonus) | [bonus2](#bonus2) | [bonus3](#bonus3) | [bonus4](#bonus4) | [bonus5](#bonus5) | [bonus_script](#bonus_script) | [bonus_script_clear](#bonus_script_clear) | [bpet](#bpet) | [breakequip](#breakequip) | [buyingstore](#buyingstore) | 
**C:** [callfunc](#callfunc) | [callfunc](#callfunc) | [callshop](#callshop) | [callsub](#callsub) | [callsub](#callsub) | [camerainfo](#camerainfo) | [cap_value](#cap_value) | [cardscnt](#cardscnt) | [cartcountitem](#cartcountitem) | [cartcountitem](#cartcountitem) | [cartcountitem2](#cartcountitem2) | [cartcountitem2](#cartcountitem2) | [cartdelitem](#cartdelitem) | [cartdelitem](#cartdelitem) | [cartdelitem2](#cartdelitem2) | [cartdelitem2](#cartdelitem2) | [catchpet](#catchpet) | [ceil](#ceil) | [changebase](#changebase) | [changecharsex](#changecharsex) | [changelook](#changelook) | [changequest](#changequest) | [changesex](#changesex) | [channel_ban](#channel_ban) | [channel_chat](#channel_chat) | [channel_create](#channel_create) | [channel_delete](#channel_delete) | [channel_getopt](#channel_getopt) | [channel_join](#channel_join) | [channel_kick](#channel_kick) | [channel_kick](#channel_kick) | [channel_setcolor](#channel_setcolor) | [channel_setgroup](#channel_setgroup) | [channel_setgroup2](#channel_setgroup2) | [channel_setopt](#channel_setopt) | [channel_setpass](#channel_setpass) | [channel_unban](#channel_unban) | [charat](#charat) | [charcommand](#charcommand) | [charisalpha](#charisalpha) | [charislower](#charislower) | [charisupper](#charisupper) | [chatmes](#chatmes) | [checkcart](#checkcart) | [checkcell](#checkcell) | [checkchatting](#checkchatting) | [checkdragon](#checkdragon) | [checkequipedcard](#checkequipedcard) | [checkfalcon](#checkfalcon) | [checkhomcall](#checkhomcall) | [checkidle](#checkidle) | [checkidlehom](#checkidlehom) | [checkidlemer](#checkidlemer) | [checkmadogear](#checkmadogear) | [checkoption](#checkoption) | [checkoption1](#checkoption1) | [checkoption2](#checkoption2) | [checkquest](#checkquest) | [checkre](#checkre) | [checkriding](#checkriding) | [checkvending](#checkvending) | [checkwall](#checkwall) | [checkweight](#checkweight) | [checkweight](#checkweight) | [checkweight2](#checkweight2) | [checkwug](#checkwug) | [clan_join](#clan_join) | [clan_leave](#clan_leave) | [classchange](#classchange) | [cleanarea](#cleanarea) | [cleanmap](#cleanmap) | [clear](#clear) | [cleararray](#cleararray) | [clearitem](#clearitem) | [cloakoffnpc](#cloakoffnpc) | [cloakoffnpcself](#cloakoffnpcself) | [cloakonnpc](#cloakonnpc) | [cloakonnpcself](#cloakonnpcself) | [clone](#clone) | [close](#close) | [close2](#close2) | [close3](#close3) | [cmdothernpc](#cmdothernpc) | [compare](#compare) | [completequest](#completequest) | [consumeitem](#consumeitem) | [consumeitem](#consumeitem) | [convertpcinfo](#convertpcinfo) | [convertpcinfo](#convertpcinfo) | [convertpcinfo](#convertpcinfo) | [cooking](#cooking) | [copyarray](#copyarray) | [countbound](#countbound) | [countinarray](#countinarray) | [countitem](#countitem) | [countitem](#countitem) | [countitem2](#countitem2) | [countitem2](#countitem2) | [countitem3](#countitem3) | [countitem3](#countitem3) | [countitem4](#countitem4) | [countitem4](#countitem4) | [countspiritball](#countspiritball) | [countstr](#countstr) | [cutin](#cutin) | 
**D:** [day](#day) | [deactivatepset](#deactivatepset) | [debugmes](#debugmes) | [defpattern](#defpattern) | [delchar](#delchar) | [delequip](#delequip) | [deletearray](#deletearray) | [deletepset](#deletepset) | [delitem](#delitem) | [delitem](#delitem) | [delitem2](#delitem2) | [delitem2](#delitem2) | [delitem3](#delitem3) | [delitem3](#delitem3) | [delitem4](#delitem4) | [delitem4](#delitem4) | [delitemidx](#delitemidx) | [delmonsterdrop](#delmonsterdrop) | [delmonsterdrop](#delmonsterdrop) | [delspiritball](#delspiritball) | [deltimer](#deltimer) | [delwaitingroom](#delwaitingroom) | [delwall](#delwall) | [detachnpctimer](#detachnpctimer) | [detachrid](#detachrid) | [disable_command](#disable_command) | [disable_items](#disable_items) | [disablearena](#disablearena) | [disablenpc](#disablenpc) | [disablewaitingroomevent](#disablewaitingroomevent) | [disguise](#disguise) | [dispbottom](#dispbottom) | [distance](#distance) | [divorce](#divorce) | [do](#do) | [doevent](#doevent) | [donpcevent](#donpcevent) | [downrefitem](#downrefitem) | [duplicate](#duplicate) | [duplicate_dynamic](#duplicate_dynamic) | 
**E:** [eaclass](#eaclass) | [emotion](#emotion) | [enable_command](#enable_command) | [enable_items](#enable_items) | [enablearena](#enablearena) | [enablenpc](#enablenpc) | [enablewaitingroomevent](#enablewaitingroomevent) | [enchantgradeui](#enchantgradeui) | [end](#end) | [equip](#equip) | [erasequest](#erasequest) | [errormes](#errormes) | [escape_sql](#escape_sql) | [explode](#explode) | 
**F:** [failedrefitem](#failedrefitem) | [failedremovecards](#failedremovecards) | [flagemblem](#flagemblem) | [floor](#floor) | [for](#for) | [freeloop](#freeloop) | [function](#function) | [function](#function) | [function](#function) | 
**G:** [get_githash](#get_githash) | [get_reputation_points](#get_reputation_points) | [get_revision](#get_revision) | [getareadropitem](#getareadropitem) | [getareaunits](#getareaunits) | [getareausers](#getareausers) | [getarg](#getarg) | [getargcount](#getargcount) | [getarraysize](#getarraysize) | [getattachedrid](#getattachedrid) | [getbaseexp_ratio](#getbaseexp_ratio) | [getbattleflag](#getbattleflag) | [getbrokenid](#getbrokenid) | [getcastledata](#getcastledata) | [getcastlename](#getcastlename) | [getcharid](#getcharid) | [getcharip](#getcharip) | [getchildid](#getchildid) | [getd](#getd) | [getelementofarray](#getelementofarray) | [geteleminfo](#geteleminfo) | [getenchantgrade](#getenchantgrade) | [getequiparmorlv](#getequiparmorlv) | [getequipcardcnt](#getequipcardcnt) | [getequipcardid](#getequipcardid) | [getequipid](#getequipid) | [getequipisenableref](#getequipisenableref) | [getequipisequiped](#getequipisequiped) | [getequipname](#getequipname) | [getequippercentrefinery](#getequippercentrefinery) | [getequiprandomoption](#getequiprandomoption) | [getequiprefinecost](#getequiprefinecost) | [getequiprefinerycnt](#getequiprefinerycnt) | [getequiptradability](#getequiptradability) | [getequipuniqueid](#getequipuniqueid) | [getequipweaponlv](#getequipweaponlv) | [getexp](#getexp) | [getexp2](#getexp2) | [getfame](#getfame) | [getfamerank](#getfamerank) | [getfatherid](#getfatherid) | [getfreecell](#getfreecell) | [getgdskilllv](#getgdskilllv) | [getgdskilllv](#getgdskilllv) | [getgmlevel](#getgmlevel) | [getgroupid](#getgroupid) | [getgroupitem](#getgroupitem) | [getguildalliance](#getguildalliance) | [getguildinfo](#getguildinfo) | [getguildmaster](#getguildmaster) | [getguildmasterid](#getguildmasterid) | [getguildmember](#getguildmember) | [getguildname](#getguildname) | [gethominfo](#gethominfo) | [getinstancevar](#getinstancevar) | [getinventorylist](#getinventorylist) | [getitem](#getitem) | [getitem](#getitem) | [getitem2](#getitem2) | [getitem2](#getitem2) | [getitem3](#getitem3) | [getitem3](#getitem3) | [getitem4](#getitem4) | [getitem4](#getitem4) | [getitembound](#getitembound) | [getitembound](#getitembound) | [getitembound2](#getitembound2) | [getitembound2](#getitembound2) | [getitembound3](#getitembound3) | [getitembound3](#getitembound3) | [getitembound4](#getitembound4) | [getitembound4](#getitembound4) | [getiteminfo](#getiteminfo) | [getiteminfo](#getiteminfo) | [getiteminfo](#getiteminfo) | [getitemname](#getitemname) | [getitemname](#getitemname) | [getitempos](#getitempos) | [getitemslots](#getitemslots) | [getjobexp_ratio](#getjobexp_ratio) | [getlook](#getlook) | [getmapflag](#getmapflag) | [getmapguildusers](#getmapguildusers) | [getmapunits](#getmapunits) | [getmapusers](#getmapusers) | [getmapxy](#getmapxy) | [getmercinfo](#getmercinfo) | [getmobdrops](#getmobdrops) | [getmonsterinfo](#getmonsterinfo) | [getmonsterinfo](#getmonsterinfo) | [getmotherid](#getmotherid) | [getnameditem](#getnameditem) | [getnameditem](#getnameditem) | [getnameditem](#getnameditem) | [getnameditem](#getnameditem) | [getnpcid](#getnpcid) | [getnpctimer](#getnpctimer) | [getpartnerid](#getpartnerid) | [getpartyleader](#getpartyleader) | [getpartymember](#getpartymember) | [getpartyname](#getpartyname) | [getpcblock](#getpcblock) | [getpetinfo](#getpetinfo) | [getrandgroupitem](#getrandgroupitem) | [getrandmobid](#getrandmobid) | [getrandomoptinfo](#getrandomoptinfo) | [getrefine](#getrefine) | [getsavepoint](#getsavepoint) | [getscrate](#getscrate) | [getskilllist](#getskilllist) | [getskilllv](#getskilllv) | [getskilllv](#getskilllv) | [getstatus](#getstatus) | [getstrlen](#getstrlen) | [gettime](#gettime) | [gettimestr](#gettimestr) | [gettimetick](#gettimetick) | [getunitdata](#getunitdata) | [getunitname](#getunitname) | [getunits](#getunits) | [getunittitle](#getunittitle) | [getunittype](#getunittype) | [getusers](#getusers) | [getvar](#getvar) | [getvariableofnpc](#getvariableofnpc) | [getwaitingroomstate](#getwaitingroomstate) | [getwaitingroomusers](#getwaitingroomusers) | [globalmes](#globalmes) | [goto](#goto) | [groupranditem](#groupranditem) | [guardian](#guardian) | [guardianinfo](#guardianinfo) | [guild_has_permission](#guild_has_permission) | [guildchangegm](#guildchangegm) | [guildgetexp](#guildgetexp) | [guildopenstorage](#guildopenstorage) | [guildopenstorage_log](#guildopenstorage_log) | [guildskill](#guildskill) | [guildskill](#guildskill) | [guildstoragecountitem](#guildstoragecountitem) | [guildstoragecountitem](#guildstoragecountitem) | [guildstoragecountitem2](#guildstoragecountitem2) | [guildstoragecountitem2](#guildstoragecountitem2) | [guildstoragedelitem](#guildstoragedelitem) | [guildstoragedelitem](#guildstoragedelitem) | [guildstoragedelitem2](#guildstoragedelitem2) | [guildstoragedelitem2](#guildstoragedelitem2) | [gvgoff](#gvgoff) | [gvgoff3](#gvgoff3) | [gvgon](#gvgon) | [gvgon3](#gvgon3) | 
**H:** [has_autoloot](#has_autoloot) | [has_hateffect](#has_hateffect) | [hateffect](#hateffect) | [heal](#heal) | [healap](#healap) | [hideoffnpc](#hideoffnpc) | [hideonnpc](#hideonnpc) | [homevolution](#homevolution) | [hommutate](#hommutate) | [homshuffle](#homshuffle) | 
**I:** [identifyall](#identifyall) | [if](#if) | [ignoretimeout](#ignoretimeout) | [implode](#implode) | [inarray](#inarray) | [initnpctimer](#initnpctimer) | [input](#input) | [insertchar](#insertchar) | [instance_announce](#instance_announce) | [instance_check_clan](#instance_check_clan) | [instance_check_guild](#instance_check_guild) | [instance_check_party](#instance_check_party) | [instance_create](#instance_create) | [instance_destroy](#instance_destroy) | [instance_enter](#instance_enter) | [instance_id](#instance_id) | [instance_info](#instance_info) | [instance_list](#instance_list) | [instance_live_info](#instance_live_info) | [instance_mapname](#instance_mapname) | [instance_npcname](#instance_npcname) | [instance_warpall](#instance_warpall) | [is_function](#is_function) | [is_guild_leader](#is_guild_leader) | [is_party_leader](#is_party_leader) | [isbegin_quest](#isbegin_quest) | [isday](#isday) | [isdead](#isdead) | [isequipped](#isequipped) | [isequippedcnt](#isequippedcnt) | [isloggedin](#isloggedin) | [ismounting](#ismounting) | [isnight](#isnight) | [isnpccloaked](#isnpccloaked) | [ispartneron](#ispartneron) | [item_enchant](#item_enchant) | [item_reform](#item_reform) | [item_reform](#item_reform) | [itemheal](#itemheal) | [itemlink](#itemlink) | [itemskill](#itemskill) | [itemskill](#itemskill) | 
**J:** [jobcanentermap](#jobcanentermap) | [jobchange](#jobchange) | [jobname](#jobname) | [jump_zero](#jump_zero) | 
**K:** [kick](#kick) | [kickwaitingroomall](#kickwaitingroomall) | [killmonster](#killmonster) | [killmonsterall](#killmonsterall) | 
**L:** [laphine_synthesis](#laphine_synthesis) | [laphine_synthesis](#laphine_synthesis) | [laphine_upgrade](#laphine_upgrade) | [logmes](#logmes) | 
**M:** [macro_detector](#macro_detector) | [macro_detector](#macro_detector) | [mail](#mail) | [makeitem](#makeitem) | [makeitem](#makeitem) | [makeitem2](#makeitem2) | [makeitem2](#makeitem2) | [makeitem3](#makeitem3) | [makeitem3](#makeitem3) | [makeitem4](#makeitem4) | [makeitem4](#makeitem4) | [makepet](#makepet) | [makerune](#makerune) | [mapannounce](#mapannounce) | [mapid2name](#mapid2name) | [mapname2id](#mapname2id) | [maprespawnguildid](#maprespawnguildid) | [mapwarp](#mapwarp) | [marriage](#marriage) | [max](#max) | [maximum](#maximum) | [md5](#md5) | [menu](#menu) | [mercenary_create](#mercenary_create) | [mercenary_delete](#mercenary_delete) | [mercenary_get_calls](#mercenary_get_calls) | [mercenary_get_faith](#mercenary_get_faith) | [mercenary_heal](#mercenary_heal) | [mercenary_sc_start](#mercenary_sc_start) | [mercenary_set_calls](#mercenary_set_calls) | [mercenary_set_faith](#mercenary_set_faith) | [mergeitem](#mergeitem) | [mergeitem2](#mergeitem2) | [mergeitem2](#mergeitem2) | [mes](#mes) | [mesitemicon](#mesitemicon) | [mesitemicon](#mesitemicon) | [mesitemlink](#mesitemlink) | [mesitemlink](#mesitemlink) | [message](#message) | [min](#min) | [minimum](#minimum) | [misceffect](#misceffect) | [mob_setidleevent](#mob_setidleevent) | [mobcount](#mobcount) | [monster](#monster) | [monster](#monster) | [morphembryo](#morphembryo) | [movenpc](#movenpc) | 
**N:** [navigateto](#navigateto) | [navihide](#navihide) | [naviregisterwarp](#naviregisterwarp) | [needed_status_point](#needed_status_point) | [next](#next) | [night](#night) | [npcshopadditem](#npcshopadditem) | [npcshopadditem](#npcshopadditem) | [npcshopattach](#npcshopattach) | [npcshopdelitem](#npcshopdelitem) | [npcshopitem](#npcshopitem) | [npcshopitem](#npcshopitem) | [npcshopupdate](#npcshopupdate) | [npcskill](#npcskill) | [npcskill](#npcskill) | [npcskilleffect](#npcskilleffect) | [npcskilleffect](#npcskilleffect) | [npcspeed](#npcspeed) | [npcstop](#npcstop) | [npctalk](#npctalk) | [npcwalkto](#npcwalkto) | [nude](#nude) | 
**O:** [open_quest_ui](#open_quest_ui) | [open_roulette](#open_roulette) | [openauction](#openauction) | [openbank](#openbank) | [opendressroom](#opendressroom) | [openmail](#openmail) | [openstorage](#openstorage) | [openstorage2](#openstorage2) | [openstylist](#openstylist) | [opentips](#opentips) | 
**P:** [party_addmember](#party_addmember) | [party_changeleader](#party_changeleader) | [party_changeoption](#party_changeoption) | [party_create](#party_create) | [party_delmember](#party_delmember) | [party_destroy](#party_destroy) | [pcblockmove](#pcblockmove) | [pcblockskill](#pcblockskill) | [pcfollow](#pcfollow) | [pcstopfollow](#pcstopfollow) | [percentheal](#percentheal) | [permission_add](#permission_add) | [permission_check](#permission_check) | [permission_remove](#permission_remove) | [pet](#pet) | [petautobonus](#petautobonus) | [petautobonus2](#petautobonus2) | [petautobonus3](#petautobonus3) | [petautobonus3](#petautobonus3) | [petloot](#petloot) | [petrecovery](#petrecovery) | [petskillattack](#petskillattack) | [petskillattack](#petskillattack) | [petskillattack2](#petskillattack2) | [petskillattack2](#petskillattack2) | [petskillbonus](#petskillbonus) | [petskillsupport](#petskillsupport) | [petskillsupport](#petskillsupport) | [plagiarizeskill](#plagiarizeskill) | [plagiarizeskillreset](#plagiarizeskillreset) | [play](#play) | [play](#play) | [playerattached](#playerattached) | [pow](#pow) | [preg_match](#preg_match) | [produce](#produce) | [progressbar](#progressbar) | [progressbar_npc](#progressbar_npc) | [prompt](#prompt) | [pushpc](#pushpc) | [pvpoff](#pvpoff) | [pvpon](#pvpon) | 
**Q:** [query_logsql](#query_logsql) | [query_sql](#query_sql) | [questinfo](#questinfo) | [questinfo_refresh](#questinfo_refresh) | 
**R:** [rand](#rand) | [randomoptgroup](#randomoptgroup) | [readbook](#readbook) | [readparam](#readparam) | [readparam](#readparam) | [recalculatestat](#recalculatestat) | [recovery](#recovery) | [refineui](#refineui) | [removemapflag](#removemapflag) | [removespecialeffect](#removespecialeffect) | [removespecialeffect2](#removespecialeffect2) | [rentalcountitem](#rentalcountitem) | [rentalcountitem](#rentalcountitem) | [rentalcountitem2](#rentalcountitem2) | [rentalcountitem2](#rentalcountitem2) | [rentalcountitem3](#rentalcountitem3) | [rentalcountitem3](#rentalcountitem3) | [rentalcountitem4](#rentalcountitem4) | [rentalcountitem4](#rentalcountitem4) | [rentitem](#rentitem) | [rentitem](#rentitem) | [rentitem2](#rentitem2) | [rentitem2](#rentitem2) | [rentitem3](#rentitem3) | [rentitem3](#rentitem3) | [rentitem4](#rentitem4) | [rentitem4](#rentitem4) | [repair](#repair) | [repairall](#repairall) | [replacestr](#replacestr) | [requestguildinfo](#requestguildinfo) | [resetfeel](#resetfeel) | [resethate](#resethate) | [resetlvl](#resetlvl) | [resetskill](#resetskill) | [resetstatus](#resetstatus) | [return](#return) | [rid2name](#rid2name) | [roclass](#roclass) | [round](#round) | 
**S:** [save](#save) | [savepoint](#savepoint) | [sc_end](#sc_end) | [sc_end_class](#sc_end_class) | [sc_start](#sc_start) | [sc_start2](#sc_start2) | [sc_start4](#sc_start4) | [searchitem](#searchitem) | [searchstores](#searchstores) | [select](#select) | [set](#set) | [set](#set) | [set_reputation_points](#set_reputation_points) | [setarray](#setarray) | [setbattleflag](#setbattleflag) | [setcart](#setcart) | [setcastledata](#setcastledata) | [setcell](#setcell) | [setchar](#setchar) | [setd](#setd) | [setdialogalign](#setdialogalign) | [setdialogpos](#setdialogpos) | [setdialogpospercent](#setdialogpospercent) | [setdialogsize](#setdialogsize) | [setdragon](#setdragon) | [setfalcon](#setfalcon) | [setfont](#setfont) | [setinstancevar](#setinstancevar) | [setiteminfo](#setiteminfo) | [setiteminfo](#setiteminfo) | [setitemscript](#setitemscript) | [setlook](#setlook) | [setmadogear](#setmadogear) | [setmapflag](#setmapflag) | [setmapflagnosave](#setmapflagnosave) | [setmounting](#setmounting) | [setnpcdisplay](#setnpcdisplay) | [setnpcdisplay](#setnpcdisplay) | [setnpcdisplay](#setnpcdisplay) | [setnpcdisplay](#setnpcdisplay) | [setnpctimer](#setnpctimer) | [setoption](#setoption) | [setpcblock](#setpcblock) | [setquest](#setquest) | [setrandomoption](#setrandomoption) | [setriding](#setriding) | [setunitdata](#setunitdata) | [setunitdata](#setunitdata) | [setunitname](#setunitname) | [setunittitle](#setunittitle) | [setwall](#setwall) | [showdigit](#showdigit) | [showevent](#showevent) | [showscript](#showscript) | [sit](#sit) | [skill](#skill) | [skill](#skill) | [skilleffect](#skilleffect) | [skilleffect](#skilleffect) | [skillpointcount](#skillpointcount) | [sleep](#sleep) | [sleep2](#sleep2) | [soundeffect](#soundeffect) | [soundeffectall](#soundeffectall) | [specialeffect](#specialeffect) | [specialeffect2](#specialeffect2) | [specialpopup](#specialpopup) | [sprintf](#sprintf) | [sqrt](#sqrt) | [sscanf](#sscanf) | [stand](#stand) | [startnpctimer](#startnpctimer) | [statusup](#statusup) | [statusup2](#statusup2) | [stopnpctimer](#stopnpctimer) | [storagecountitem](#storagecountitem) | [storagecountitem](#storagecountitem) | [storagecountitem2](#storagecountitem2) | [storagecountitem2](#storagecountitem2) | [storagedelitem](#storagedelitem) | [storagedelitem](#storagedelitem) | [storagedelitem2](#storagedelitem2) | [storagedelitem2](#storagedelitem2) | [strcharinfo](#strcharinfo) | [strcmp](#strcmp) | [strnpcinfo](#strnpcinfo) | [strpos](#strpos) | [strtol](#strtol) | [strtolower](#strtolower) | [strtoupper](#strtoupper) | [substr](#substr) | [successrefitem](#successrefitem) | [successremovecards](#successremovecards) | [summon](#summon) | [switch](#switch) | 
**T:** [traitstatusup](#traitstatusup) | [traitstatusup2](#traitstatusup2) | [transform](#transform) | [transform](#transform) | 
**U:** [unbindatcmd](#unbindatcmd) | [undisguise](#undisguise) | [unequip](#unequip) | [unitattack](#unitattack) | [unitattack](#unitattack) | [unitblockmove](#unitblockmove) | [unitblockskill](#unitblockskill) | [unitexists](#unitexists) | [unitkill](#unitkill) | [unitskilluseid](#unitskilluseid) | [unitskilluseid](#unitskilluseid) | [unitskillusepos](#unitskillusepos) | [unitskillusepos](#unitskillusepos) | [unitstopattack](#unitstopattack) | [unitstopwalk](#unitstopwalk) | [unittalk](#unittalk) | [unitwalk](#unitwalk) | [unitwalkto](#unitwalkto) | [unitwarp](#unitwarp) | [unloadnpc](#unloadnpc) | [useatcmd](#useatcmd) | 
**V:** [viewpoint](#viewpoint) | [viewpointmap](#viewpointmap) | [vip_status](#vip_status) | [vip_time](#vip_time) | 
**W:** [waitingroom](#waitingroom) | [waitingroom2bg](#waitingroom2bg) | [waitingroom2bg_single](#waitingroom2bg_single) | [waitingroomkick](#waitingroomkick) | [warp](#warp) | [warpguild](#warpguild) | [warppartner](#warppartner) | [warpparty](#warpparty) | [warpportal](#warpportal) | [warpwaitingpc](#warpwaitingpc) | [wedding](#wedding) | [while](#while) | 

---

## Complete Command Reference

### mes

<!-- RAG_CHUNK: cmd_mes -->

**Signature:**
```c
*mes "<string>"{,"<string>"{,...}};
```

**Description:**
This command will display a box on the screen for the invoking character, if no such box is displayed already, and will print the string specified into that box. There is normally no 'close' or 'next' button on this box, unless you create one with 'close' or 'next', and while it's open the player can't do much else, so it's important to create a button later. If the string is empty, it will show up as an empty line.

**Example:**
```c
	mes "Text that will appear in the box";

```

---

### next

<!-- RAG_CHUNK: cmd_next -->

**Signature:**
```c
*next;
```

**Description:**
This command will display a 'next' button in the message window for the invoking character. Clicking on it will cause the window to clear and display a new one. Used to segment NPC-talking, next is often used in combination with 'mes' and 'close'.

---

### clear

<!-- RAG_CHUNK: cmd_clear -->

**Signature:**
```c
*clear;
```

**Description:**
This command will clear the dialog text and continue the script without player interaction.

**Example:**
```c
	mes "This is how the 'clear' script command works.";
	sleep2 3000;
	clear; // This will clear the dialog and continue to the next one.
	mes "I will show you again.";
	sleep2 3000;
	clear;
	mes "Bye!";
	close;

```

---

### close

<!-- RAG_CHUNK: cmd_close -->

**Signature:**
```c
*close;
```

**Description:**
This command will create a 'close' button in the message window for the invoking character. If no window is currently on screen, the script execution will end. This is one of the ways to end a speech from an NPC. Once the button is clicked, the NPC script execution will end, and the message box will disappear.

---

### close2

<!-- RAG_CHUNK: cmd_close2 -->

**Signature:**
```c
*close2;
```

**Description:**
This command will create a 'close' button in the message window for the invoking character. WARNING: If no window is currently on screen, the script execution will halt indefinitely! See 'close'. There is one important difference, though - even though the message box will have closed, the script execution will not stop, and commands after 'close2' will still run, meaning an 'end' has to be used to stop the script, unless you make it stop in some other manner.

---

### close3

<!-- RAG_CHUNK: cmd_close3 -->

**Signature:**
```c
*close3;
```

**Description:**
The command is similar to 'close' but the cutin (if any) is cleared after closing.

---

### end

<!-- RAG_CHUNK: cmd_end -->

**Signature:**
```c
*end;
```

**Description:**
This command will stop the execution for this particular script. The two versions are perfectly equivalent. It is the normal way to end a script which does not use 'mes'.

---

### set

<!-- RAG_CHUNK: cmd_set -->

**Signature:**
```c
*set <variable>,<expression>{,<char_id>};
```

---

### set

<!-- RAG_CHUNK: cmd_set -->

**Signature:**
```c
*set(<variable>,<expression>{,<char id>})
```

**Description:**
This command will set a variable to the value that the expression results in. Variables may either be set through this command or directly, much like any other programming language (refer to the "Assigning variables" section).

---

### setd

<!-- RAG_CHUNK: cmd_setd -->

**Signature:**
```c
*setd "<variable name>",<value>{,<char_id>};
```

**Description:**
Works almost identically as set, except the variable name is identified as a string and can thus be constructed dynamically.

**Example:**
```c
	set getd("variable name"),<value>;

```

---

### getd

<!-- RAG_CHUNK: cmd_getd -->

**Signature:**
```c
*getd("<variable name>")
```

**Description:**
Returns a reference to a variable, the name can be constructed dynamically. Refer to 'setd' for usage.

**Example:**
```c
	setarray getd(".array[0]"), 1, 2, 3, 4, 5;

```

---

### getvariableofnpc

<!-- RAG_CHUNK: cmd_getvariableofnpc -->

**Signature:**
```c
*getvariableofnpc(<variable>,"<npc name>")
```

**Description:**
Returns a reference to a NPC variable (. prefix) from the target NPC. This can only be used to get . variables.

**Example:**
```c
	getvariableofnpc(.var,"TargetNPC");

```

---

### getvar

<!-- RAG_CHUNK: cmd_getvar -->

**Signature:**
```c
*getvar <variable>,<char_id>;
```

**Description:**
Get variable value from the specified player. Only player/account variables are allowed to be used (temporary character variable "@", permanent character "", permanent local account "#", and permanent global account "##").

---

### goto

<!-- RAG_CHUNK: cmd_goto -->

**Signature:**
```c
*goto <label>;
```

**Description:**
This command will make the script jump to a label, usually used in conjunction with other command, such as "if", but often used on its own.

---

### menu

<!-- RAG_CHUNK: cmd_menu -->

**Signature:**
```c
*menu "<option_text>",<target_label>{,"<option_text>",<target_label>,...};
```

**Description:**
This command will create a selectable menu for the invoking character. Only one menu can be on screen at the same time.

**Example:**
```c
	menu "A:B",L_Wrong,"C",L_Right;

```

---

### select

<!-- RAG_CHUNK: cmd_select -->

**Signature:**
```c
*select("<option>"{,"<option>",...})
```

---

### prompt

<!-- RAG_CHUNK: cmd_prompt -->

**Signature:**
```c
*prompt("<option>"{,"<option>",...})
```

**Description:**
This function is a handy replacement for 'menu' for some specific cases where you don't want a complex label structure - like, for example, asking simple yes- no questions. It will return the number of menu option picked, starting with 1. Like 'menu', it will also set the variable @menu to contain the option the user picked.

**Example:**
```c
    if (select("Yes:No" ) == 1)
		mes "You said yes, I know.";

```

---

### input

<!-- RAG_CHUNK: cmd_input -->

**Signature:**
```c
*input(<variable>{,<min>{,<max>}})
```

**Description:**
This command will make an input box pop up on the client connected to the invoking character, to allow entering of a number or a string. This has many uses, one example would be a guessing game, also making use of the 'rand' function:

**Example:**
```c
	mes "[Woman]";
	mes "Try and guess the number I am thinking of.";
	mes "The number will be between 1 and 10.";
	next;
	.@number = rand(1,10);
	input .@guess;
	if (.@guess == .@number) {
		mes "[Woman]";
		mes "Well done, that was the number I was thinking of!";
		close;
	} else {
		mes "[Woman]";
		mes "Sorry, that wasn't the number I was thinking of.";
		close;
	}
```

---

### callfunc

<!-- RAG_CHUNK: cmd_callfunc -->

**Signature:**
```c
*callfunc "<function>"{,<argument>,...<argument>};
```

---

### callfunc

<!-- RAG_CHUNK: cmd_callfunc -->

**Signature:**
```c
*callfunc("<function>"{,<argument>,...<argument>})
```

**Description:**
This command lets you call up a function NPC. A function NPC can be called from any script on any map server. Using the 'return' command it will come back to the place that called it.

---

### callsub

<!-- RAG_CHUNK: cmd_callsub -->

**Signature:**
```c
*callsub <label>{,<argument>,...<argument>};
```

---

### callsub

<!-- RAG_CHUNK: cmd_callsub -->

**Signature:**
```c
*callsub(<label>{,<argument>,...<argument>})
```

**Description:**
This command will go to a specified label within the current script (do NOT use quotes around it) coming in as if it were a 'callfunc' call, and pass it arguments given, if any, which can be recovered there with 'getarg'. When done there, you should use the 'return' command to go back to the point from where this label was called. This is used when there is a specific thing the script will do over and over, this lets you use the same bit of code as many times as you like, to save space and time, without creating extra NPC objects which are needed with 'callfunc'. A label is not callable in this manner from another script.

**Example:**
```c
	callsub S_CheckFull, "guild_vs2",50;
	switch( rand(4) ) {
		case 0:	warp "guild_vs2",9,50;	end;
		case 1:	warp "guild_vs2",49,90;	end;
		case 2:	warp "guild_vs2",90,50;	end;
		case 3:	warp "guild_vs2",49,9;	end;
	}

```

---

### getarg

<!-- RAG_CHUNK: cmd_getarg -->

**Signature:**
```c
*getarg(<index>{,<default_value>})
```

**Description:**
This function is used when you use the 'callsub' or 'callfunc' commands. In the call you can specify variables that will make that call different from another one. This function will return an argument the function or subroutine was called with, and is the normal way to get them. This is another thing that can let you use the same code more than once.

**Example:**
```c
	place,50,50,6%TAB%script%TAB%Woman1%TAB%115,{
		mes "[Woman]";
		mes "Let's see if you win...";
		callfunc "funcNPC",2;
		mes "Well done, you have won!";
		close;
	}

	place,52,50,6%TAB%script%TAB%Woman2%TAB%115,{
		mes "[Woman]";
		mes "Let's see if you win...";
		callfunc "funcNPC",5;
		mes "Well done, you have won!";
		close;
	}
```

---

### getargcount

<!-- RAG_CHUNK: cmd_getargcount -->

**Signature:**
```c
*getargcount()
```

**Description:**
This function is used when you use the 'callsub' or 'callfunc' commands. In the call you can specify arguments. This function will return the number of arguments provided.

**Example:**
```c
	callfunc "funcNPC",5,4,3;
	...
	function%TAB%script%TAB%funcNPC%TAB%{
		.@count = getargcount(); // 3
		...
	}

```

---

### return

<!-- RAG_CHUNK: cmd_return -->

**Signature:**
```c
*return {<value>};
```

**Description:**
This command causes the script execution to leave previously called function with callfunc or script with callsub and return to the location, where the call originated from. Optionally a return value can be supplied, when the call was done using the function form.

---

### function

<!-- RAG_CHUNK: cmd_function -->

**Signature:**
```c
*function <function name>;
```

---

### function

<!-- RAG_CHUNK: cmd_function -->

**Signature:**
```c
*function <function name>;
```

---

### function

<!-- RAG_CHUNK: cmd_function -->

**Signature:**
```c
*function <function name> {
```

**Description:**
<code> }

**Example:**
```c
    1. Declare the function.
	function <function name>;
    2. Call the function anywhere within the script.
       It can also return a value when used with parentheses.
	<function name>;
    3. Define the function within the script.
	<function name> {<code>}

```

---

### is_function

<!-- RAG_CHUNK: cmd_is_function -->

**Signature:**
```c
*is_function("<function name>")
```

**Description:**
This command checks whether a function exists. It returns 1 if function is found, or 0 if it isn't.

**Example:**
```c
	function	script	try	{
		dothat;
	}

	-	script	test	-1,{
		.@try = is_function("try"); // 1
		.@not = is_function("not"); // 0
	}

```

---

### if

<!-- RAG_CHUNK: cmd_if -->

**Signature:**
```c
*if (<condition>) <statement>;
```

**Description:**
This is the basic conditional statement command, and just about the only one available in this scripting language.

**Example:**
```c
    if (1)  mes "This will always print.";
    if (0)  mes "And this will never print.";
    if (5)  mes "This will also always print.";
    if (-1) mes "Funny as it is, this will also print just fine.";

```

---

### jump_zero

<!-- RAG_CHUNK: cmd_jump_zero -->

**Signature:**
```c
*jump_zero (<condition>),<label>;
```

**Description:**
This command works kinda like an 'if'+'goto' combination in one go. (See 'if'). If the condition is false (equal to zero) this command will immediately jump to the specified label like in 'goto'. While 'if' is more generally useful, for some cases this could be an optimization.

---

### switch

<!-- RAG_CHUNK: cmd_switch -->

**Signature:**
```c
*switch (expression);
```

**Description:**
The switch statement is similar to a series of if statements on the same expression. In many occasions, you may want to compare the same variable (or expression) with many different values, and execute a different piece of code depending on which value it equals to. This is exactly what the switch statement is for.

**Example:**
```c
	switch(select("Yes:No")) {
		case 1:
			mes "You said yes!";
			break;
		case 2:
			mes "Aww, why?";
			break;
	}
	close;

```

---

### while

<!-- RAG_CHUNK: cmd_while -->

**Signature:**
```c
*while (<condition>) <statement>;
```

**Description:**
This is probably the simplest and most frequently used loop structure. The 'while' statement can be interpreted as "while <condition> is true, perform <statement>". It is a pretest loop, meaning the conditional expression is tested before any of the statements in the body of the loop are performed. If the condition evaluates to false, the statement(s) in the body of the loop is/are never executed. If the condition evaluates to true, the statement(s) are executed, then control transfers back to the conditional expression, which is reevaluated and the cycle continues.

**Example:**
```c
	while (switch(select("Yes:No") == 2 ))
		mes "You picked no.";
	close;

```

---

### for

<!-- RAG_CHUNK: cmd_for -->

**Signature:**
```c
*for (<variable initialization>; <condition>; <variable update>) <statement>;
```

**Description:**
Another pretest looping structure is the 'for' statement. It is considered a specialized form of the 'while' statement, and is usually associated with counter- controlled loops. Here are the steps of the 'for' statement: the initialize statement is executed first and only once. The condition test is performed. When the condition evaluates to false, the rest of the for statement is skipped. When the condition evaluates to true, the body of the loop is executed, then the update statement is executed (this usually involves incrementing a variable). Then the condition is reevaluated and the cycle continues.

**Example:**
```c
	for( .@i = 1; .@i <= 5; .@i++ )
		mes "This line will print 5 times.";

```

---

### do

<!-- RAG_CHUNK: cmd_do -->

**Signature:**
```c
*do { <statement>; } while (<condition>);
```

**Description:**
The 'do...while' is the only post-test loop structure available in this script language. With a post-test, the statements are executed once before the condition is tested. When the condition is true, the statement(s) are repeated. When the condition is false, control is transferred to the statement following the 'do...while' loop expression.

**Example:**
```c
	mes "This menu will keep appearing until you pick Cancel";
	do {
		.@menu = select("One:Two:Three:Cancel");
	} while (.@menu != 4);

```

---

### freeloop

<!-- RAG_CHUNK: cmd_freeloop -->

**Signature:**
```c
*freeloop({<toggle>})
```

**Description:**
Toggling this to enabled (1) allows the script instance to bypass the infinite loop protection, allowing your script to loop as much as it may need. Disabling (0) will warn you if an infinite loop is detected.

**Example:**
```c
	freeloop(1); // enable script to loop freely

	// be careful with what you do here
	for ( .@i = 0; .@i < .@bigloop; .@i++ ) {
		dothis;
		// will sleep the script for 1ms when detect an infinity loop to
		// let rAthena do what it needs to do (socket, timer, process, etc.)
	}

	freeloop(0); // disable freeloop

	for ( .@i = 0; .@i < .@bigloop; .@i++ ) {
		dothis;
		// throw an infinity loop error
	}
```

---

### setarray

<!-- RAG_CHUNK: cmd_setarray -->

**Signature:**
```c
*setarray <array name>[<first value>],<value>{,<value>...<value>};
```

**Description:**
This command will allow you to quickly fill up an array in one go. Check the Kafra scripts in the distribution to see this used a lot.

**Example:**
```c
    setarray .@array[0], 100, 200, 300, 400, 500, 600;

```

---

### cleararray

<!-- RAG_CHUNK: cmd_cleararray -->

**Signature:**
```c
*cleararray <array name>[<first value to alter>],<value>,<number of values to set>;
```

**Description:**
This command will change many array values at the same time to the same value.

**Example:**
```c
    setarray .@array[0], 100, 200, 300, 400, 500, 600;
    // This will make all 6 values 0
    cleararray .@array[0],0,6;
    // This will make array element 0 change to 245
    cleararray .@array[0],245,1;
    // This will make elements 1 and 2 change to 345
    cleararray .@array[1],345,2;

```

---

### copyarray

<!-- RAG_CHUNK: cmd_copyarray -->

**Signature:**
```c
*copyarray <destination array>[<first value>],<source array>[<first value>],<amount of data to copy>;
```

**Description:**
This command lets you quickly shuffle a lot of data between arrays, which is in some cases invaluable.

**Example:**
```c
    setarray .@array[0], 100, 200, 300, 400, 500, 600;
    // So we have made .@array[]
    copyarray .@array2[0],@array[2],2;

    // Now, .@array2[0] will be equal to .@array[2] (300) and
    // .@array2[1] will be equal to .@array[3].

```

---

### deletearray

<!-- RAG_CHUNK: cmd_deletearray -->

**Signature:**
```c
*deletearray <array name>[<first value>]{,<how much to delete>};
```

**Description:**
This command will delete a specified number of array elements totally from an array, shifting all the elements beyond this towards the beginning.

**Example:**
```c
    // This will delete array element 0, and move all the other array elements
    // up one place.
    deletearray .@array[0],1

```

---

### inarray

<!-- RAG_CHUNK: cmd_inarray -->

**Signature:**
```c
*inarray <array name>,<value>;
```

**Description:**
This command returns the index of the first matching value found in the array. It will return -1 if the value is not found.

---

### countinarray

<!-- RAG_CHUNK: cmd_countinarray -->

**Signature:**
```c
*countinarray <array name>{[<start index>]},<array name>{[<start index>]};
```

**Description:**
This command will check for matches between the array values and return the number of matches. While being optional, if [<start index>] is supplied, the search will begin from the given index value.

---

### strcharinfo

<!-- RAG_CHUNK: cmd_strcharinfo -->

**Signature:**
```c
*strcharinfo(<type>{,<char_id>})
```

**Description:**
This function will return either the name, party name or guild name for the invoking character. Whatever it returns is determined by type.

---

### convertpcinfo

<!-- RAG_CHUNK: cmd_convertpcinfo -->

**Signature:**
```c
*convertpcinfo(<char_id>,<type>)
```

---

### convertpcinfo

<!-- RAG_CHUNK: cmd_convertpcinfo -->

**Signature:**
```c
*convertpcinfo(<account_id>,<type>)
```

---

### convertpcinfo

<!-- RAG_CHUNK: cmd_convertpcinfo -->

**Signature:**
```c
*convertpcinfo(<player_name>,<type>)
```

**Description:**
This function will return the information <type> for the specified character. Whatever it returns is determined by type.

---

### strnpcinfo

<!-- RAG_CHUNK: cmd_strnpcinfo -->

**Signature:**
```c
*strnpcinfo(<type>{,<npc_id>})
```

**Description:**
This function will return the various parts of the name of the calling NPC, or, if an NPC id is specified, of that npc. Whatever it returns is determined by type.

---

### getarraysize

<!-- RAG_CHUNK: cmd_getarraysize -->

**Signature:**
```c
*getarraysize(<array name>)
```

**Description:**
This function returns highest index of the array that is filled. Notice that zeros and empty strings at the end of this array are not counted towards this number.

**Example:**
```c
    setarray .@array[0], 100, 200, 300, 400, 500, 600;
    set .@arraysize,getarraysize(.@array);

```

---

### getelementofarray

<!-- RAG_CHUNK: cmd_getelementofarray -->

**Signature:**
```c
*getelementofarray(<array name>,<index>)
```

**Description:**
This command retrieves the value of the element of given array at given index. This is equivalent to using:

**Example:**
```c
    <array name>[<index>]

```

---

### readparam

<!-- RAG_CHUNK: cmd_readparam -->

**Signature:**
```c
*readparam(<parameter number>{,"<character name>"})
```

---

### readparam

<!-- RAG_CHUNK: cmd_readparam -->

**Signature:**
```c
*readparam(<parameter number>{,<char_id>})
```

**Description:**
This function will return the specified stat of the invoking character, or, if a character name or character id is specified, of that player. The stat can either be a number or parameter name, defined in 'src/map/script_constants.hpp'.

**Example:**
```c
    // Returns how many status points you haven't spent yet.
    mes "Unused status points: " + readparam(9);

```

---

### getcharid

<!-- RAG_CHUNK: cmd_getcharid -->

**Signature:**
```c
*getcharid(<type>{,"<character name>"})
```

**Description:**
This function will return a unique ID number of the invoking character, or, if a character name is specified, of that player.

---

### getnpcid

<!-- RAG_CHUNK: cmd_getnpcid -->

**Signature:**
```c
*getnpcid(<type>{,"<npc name>"});
```

**Description:**
Retrieves IDs of the currently invoked NPC. If a unique npc name is given, IDs of that NPC are retrieved instead. Type specifies what ID to retrieve and can be one of the following:

**Example:**
```c
    0 - NPC Game ID

```

---

### getchildid

<!-- RAG_CHUNK: cmd_getchildid -->

**Signature:**
```c
*getchildid({<char_id>})
```

---

### getmotherid

<!-- RAG_CHUNK: cmd_getmotherid -->

**Signature:**
```c
*getmotherid({<char_id>})
```

---

### getfatherid

<!-- RAG_CHUNK: cmd_getfatherid -->

**Signature:**
```c
*getfatherid({<char_id>})
```

**Description:**
These functions return the character ID of the attached player's child, mother, mother, or father, respectively. It returns 0 if no ID is found.

**Example:**
```c
    if (getmotherid()) mes "Your mother's ID is: " + getmotherid();

```

---

### ispartneron

<!-- RAG_CHUNK: cmd_ispartneron -->

**Signature:**
```c
*ispartneron({<char_id>})
```

**Description:**
This function returns 1 if the invoking character's marriage partner is currently online and 0 if they are not or if the character has no partner.

---

### getpartnerid

<!-- RAG_CHUNK: cmd_getpartnerid -->

**Signature:**
```c
*getpartnerid({<char_id>})
```

**Description:**
This function returns the character ID of the invoking character's marriage partner, if any. If the invoking character is not married, it will return 0, which is a quick way to see if they are married:

**Example:**
```c
    if (getpartnerid()) mes "I'm not going to be your girlfriend!";
    if (getpartnerid()) mes "You're married already!";

```

---

### getlook

<!-- RAG_CHUNK: cmd_getlook -->

**Signature:**
```c
*getlook(<type>{,<char_id>})
```

**Description:**
This function will return the number for the current character look value specified by type. See 'setlook' for valid look types.

---

### getsavepoint

<!-- RAG_CHUNK: cmd_getsavepoint -->

**Signature:**
```c
*getsavepoint(<information type>{,<char_id>})
```

**Description:**
This function will return information about the invoking character's save point. You can use it to let a character swap between several recorded save points. Available information types are:

---

### getcharip

<!-- RAG_CHUNK: cmd_getcharip -->

**Signature:**
```c
*getcharip({"<character name>"|<account id>|<char id>})
```

**Description:**
This function will return the IP address of the invoking character, or, if a player is specified, of that character. A blank string is returned if no player is attached.

**Example:**
```c
	mes "Your IP: " + getcharip();

```

---

### vip_status

<!-- RAG_CHUNK: cmd_vip_status -->

**Signature:**
```c
*vip_status(<type>,{"<character name>"})
```

**Description:**
Returns various information about a player's VIP status.

---

### vip_time

<!-- RAG_CHUNK: cmd_vip_time -->

**Signature:**
```c
*vip_time <time>,{"<character name>"};
```

**Description:**
Changes a player's VIP time (in minutes). A positive value will increase time, and a negative value will decrease time.

---

### addspiritball

<!-- RAG_CHUNK: cmd_addspiritball -->

**Signature:**
```c
*addspiritball <count>,<duration>{,<char_id>};
```

**Description:**
Adds spirit ball to player for 'duration' in milisecond.

---

### delspiritball

<!-- RAG_CHUNK: cmd_delspiritball -->

**Signature:**
```c
*delspiritball <count>{,<char_id>};
```

**Description:**
Deletes the spirit ball(s) from player.

---

### countspiritball

<!-- RAG_CHUNK: cmd_countspiritball -->

**Signature:**
```c
*countspiritball {<char_id>};
```

**Description:**
Counts the spirit ball that player has.

---

### ignoretimeout

<!-- RAG_CHUNK: cmd_ignoretimeout -->

**Signature:**
```c
*ignoretimeout <flag>{,<char_id>};
```

**Description:**
Disables the SECURE_NPCTIMEOUT function on the character invoking the script, or by the given character ID/character name.

---

### getequipid

<!-- RAG_CHUNK: cmd_getequipid -->

**Signature:**
```c
*getequipid({<equipment slot>,<char_id>})
```

**Description:**
This function returns the item ID of the item slot that calls the script on the invoking character or the specified equipment slot. If nothing is equipped there, it returns -1. Valid equipment slots are:

**Example:**
```c
	if (getequipid(EQI_HEAD_TOP) == 2234)
		mes "What a lovely Tiara you have on";
	else
		mes "Come back when you have a Tiara on";
	close;

```

---

### getequipuniqueid

<!-- RAG_CHUNK: cmd_getequipuniqueid -->

**Signature:**
```c
*getequipuniqueid(<equipment slot>{,<char_id>})
```

**Description:**
This function returns the unique ID (as a string) of the item equipped in the equipment slot specified on the invoking character. If nothing is equipped there, it returns an empty string. See 'getequipid' for a full list of valid equipment slots.

---

### getequipname

<!-- RAG_CHUNK: cmd_getequipname -->

**Signature:**
```c
*getequipname(<equipment slot>{,<char_id>})
```

**Description:**
Returns the jname of the item equipped in the specified equipment slot on the invoking character, or an empty string if nothing is equipped in that position. Does the same thing as getitemname(getequipid()). Useful for an NPC to state what your are wearing, or maybe saving as a string variable. See 'getequipid' for a full list of valid equipment slots.

**Example:**
```c
        if ( getequipname(EQI_HEAD_TOP) != "" )
	        mes "So you are wearing a " + getequipname(EQI_HEAD_TOP) + " on your head";
	else
	        mes "You are not wearing any head gear";

```

---

### getitemname

<!-- RAG_CHUNK: cmd_getitemname -->

**Signature:**
```c
*getitemname(<item id>)
```

---

### getitemname

<!-- RAG_CHUNK: cmd_getitemname -->

**Signature:**
```c
*getitemname(<aegis item name>)
```

**Description:**
Given the database ID number of an item, this function will return the text stored in the 'Name' field in item_db_*.yml for text version or 'name_english' field for SQL version. The function returns "null" if the item doesn't exist.

---

### getbrokenid

<!-- RAG_CHUNK: cmd_getbrokenid -->

**Signature:**
```c
*getbrokenid(<number>{,<char_id>})
```

**Description:**
This function will search the invoking character's inventory for any broken items, and will return their item ID numbers. Since the character may have several broken items, 1 given as an argument will return the first one found, 2 will return the second one, etc. Will return 0 if no such item is found.

---

### getequipisequiped

<!-- RAG_CHUNK: cmd_getequipisequiped -->

**Signature:**
```c
*getequipisequiped(<equipment slot>{,<char_id>})
```

**Description:**
This functions will return 1 if there is an equipment placed on the specified equipment slot and 0 otherwise. For a list of equipment slots see 'getequipid'. Function originally used by the refining NPCs:

**Example:**
```c
    if (getequipisequiped(EQI_HEAD_TOP)) {
        mes "[Refiner]";
        mes "That's a fine hat you are wearing there...";
        close;
	} else {
		mes "[Refiner]";
		mes "Do you want me to refine your dumb head?";
		close;
	}

```

---

### getequipisenableref

<!-- RAG_CHUNK: cmd_getequipisenableref -->

**Signature:**
```c
*getequipisenableref(<equipment slot>{,<char_id>})
```

**Description:**
Will return 1 if the item equipped on the invoking character in the specified equipment slot is refinable, and 0 if it isn't. For a list of equipment slots see 'getequipid'.

---

### getequiprefinerycnt

<!-- RAG_CHUNK: cmd_getequiprefinerycnt -->

**Signature:**
```c
*getequiprefinerycnt(<equipment slot>{,<char_id>})
```

**Description:**
Returns the current number of pluses for the item in the specified equipment slot. For a list of equipment slots see 'getequipid'.

---

### getequipweaponlv

<!-- RAG_CHUNK: cmd_getequipweaponlv -->

**Signature:**
```c
*getequipweaponlv({<equipment slot>{,<char_id>}})
```

**Description:**
This function returns the weapon level for the weapon equipped in the specified equipment slot on the invoking character. For a list of equipment slots see 'getequipid'.

**Example:**
```c
    switch (getequipweaponlv(EQI_HAND_R)) {
      case 1: mes "You are holding a lvl 1 weapon."; break;
      case 2: mes "You are holding a lvl 2 weapon."; break;
      case 3: mes "You are holding a lvl 3 weapon."; break;
      case 4: mes "You are holding a lvl 4 weapon."; break;
      case 5: mes "You are holding a lvl 5 weapon."; break;
      case 6: mes "You are holding a lvl 6 weapon, hm, must be a custom design..."; break;
      default: mes "Seems you don't have a weapon on."; break;
    }

    if (getequipid(EQI_HAND_L) == 0) {
        mes "Seems you have nothing equipped here.";
        close;
    }
    switch (getequipweaponlv(EQI_HAND_L)) {
```

---

### getequiparmorlv

<!-- RAG_CHUNK: cmd_getequiparmorlv -->

**Signature:**
```c
*getequiparmorlv({<equipment slot>{,<char_id>}})
```

**Description:**
This function returns the armor level for the item equipped in the specified equipment slot on the invoking character. For a list of equipment slots see 'getequipid'.

**Example:**
```c
    if (getequipid(EQI_ARMOR) == 0) {
        mes "Seems you have nothing equipped here.";
        close;
    }
    switch (getequiparmorlv(EQI_ARMOR)) {
      case 1: mes "You are wearing a lvl 1 armor."; break;
      case 2: mes "You are wearing a lvl 2 armor."; break;
      case 3: mes "You are wearing a lvl 3 armor, hm, must be a custom design..."; break;
    }

```

---

### getequippercentrefinery

<!-- RAG_CHUNK: cmd_getequippercentrefinery -->

**Signature:**
```c
*getequippercentrefinery(<equipment slot>{,<enriched>,<char_id>})
```

**Description:**
This function calculates and returns the percent value chance to successfully refine the item found in the specified equipment slot of the invoking character by +1. There is no actual formula, the success rate for a given weapon level of a certain refine level is found in the db/(pre-)re/refine_db.yml file. For a list of equipment slots see 'getequipid'.

**Example:**
```c
    if (getequippercentrefinery(EQI_HAND_L)<=rand(100)) goto L_Fail;

```

---

### getequiprefinecost

<!-- RAG_CHUNK: cmd_getequiprefinecost -->

**Signature:**
```c
*getequiprefinecost(<equipment slot>,<type>,<information>{,<char id>})
```

**Description:**
This function returns refine cost for equipment in <equipment slot> based on passed arguments <type> and <information>.

---

### getareadropitem

<!-- RAG_CHUNK: cmd_getareadropitem -->

**Signature:**
```c
*getareadropitem("<map name>",<x1>,<y1>,<x2>,<y2>,<item>)
```

**Description:**
This function will count all the items with the specified ID number lying on the ground on the specified map within the x1/y1-x2/y2 square on it and return that number.

---

### getequipcardcnt

<!-- RAG_CHUNK: cmd_getequipcardcnt -->

**Signature:**
```c
*getequipcardcnt(<equipment slot>)
```

**Description:**
This function will return the number of cards that have been compounded onto a specific equipped item for the invoking character. See 'getequipid' for a list of possible equipment slots.

---

### getinventorylist

<!-- RAG_CHUNK: cmd_getinventorylist -->

**Signature:**
```c
*getinventorylist {<char_id>};
```

**Description:**
This command sets a bunch of arrays with a complete list of whatever the invoking character has in their inventory, including all the data needed to recreate these items perfectly if they are destroyed. Here's what you get:

**Example:**
```c
                                     It will contain 0 if the item is not equipped.
```

---

### cardscnt

<!-- RAG_CHUNK: cmd_cardscnt -->

**Signature:**
```c
*cardscnt()
```

**Description:**
This function will return the number of cards inserted into the equipment from which the function is called.

---

### getrefine

<!-- RAG_CHUNK: cmd_getrefine -->

**Signature:**
```c
*getrefine()
```

**Description:**
This function will return the refine count of the equipment from which the function is called.

---

### getnameditem

<!-- RAG_CHUNK: cmd_getnameditem -->

**Signature:**
```c
*getnameditem(<item id>,"<name to inscribe>"|<char id>);
```

---

### getnameditem

<!-- RAG_CHUNK: cmd_getnameditem -->

**Signature:**
```c
*getnameditem("<item name>","<name to inscribe>"|<char id>);
```

**Description:**
This function is equivalent to using 'getitem', however, it will not just give the character an item object, but will also inscribe it with a specified character's name. You may not inscribe items with arbitrary strings, only with names of characters that actually exist. While this isn't said anywhere specifically, apparently, named items may not have cards in them, slots or no - these data slots are taken by the character ID who's name is inscribed. Only one remains free and it's not quite clear if a card may be there.

---

### getitemslots

<!-- RAG_CHUNK: cmd_getitemslots -->

**Signature:**
```c
*getitemslots(<item ID>)
```

**Description:**
This function will look up the item with the specified ID number in the database and return the number of slots this kind of items has - 0 if they are not slotted. It will also be 0 for all non-equippable items, naturally, unless someone messed up the item database. It will return -1 if there is no such item.

**Example:**
```c
	.@slots = getitemslots(1205);

```

---

### getiteminfo

<!-- RAG_CHUNK: cmd_getiteminfo -->

**Signature:**
```c
*getiteminfo(<item ID>,<type>)
```

---

### getiteminfo

<!-- RAG_CHUNK: cmd_getiteminfo -->

**Signature:**
```c
*getiteminfo(<item name>,<type>)
```

---

### getiteminfo

<!-- RAG_CHUNK: cmd_getiteminfo -->

**Signature:**
```c
*getiteminfo(<aegis item name>,<type>)
```

**Description:**
This function will look up the item with the specified ID number in the database and return the info set by TYPE argument. It will return -1 if there is no such item or "" if the aegis item name is requested.

**Example:**
```c
	ITEMINFO_BUY              -  Buy Price
	ITEMINFO_SELL             -  Sell Price
	ITEMINFO_TYPE             -  Type
	ITEMINFO_MAXCHANCE        -  maxchance (max drop chance of this item, e.g. 1 = 0.01%)
		                         if = 0, then monsters don't drop it at all (rare or a quest item)
		                         if = 10000, then this item is sold in NPC shops only
	ITEMINFO_GENDER           -  Gender
	ITEMINFO_LOCATIONS        -  Location(s)
	ITEMINFO_WEIGHT           -  Weight
	ITEMINFO_ATTACK           -  ATK
	ITEMINFO_DEFENSE          -  DEF
	ITEMINFO_RANGE            -  Range
	ITEMINFO_SLOT             -  Slot
	ITEMINFO_VIEW             -  View
	ITEMINFO_EQUIPLEVELMIN    -  equipment LV
```

---

### getequipcardid

<!-- RAG_CHUNK: cmd_getequipcardid -->

**Signature:**
```c
*getequipcardid(<equipment slot>,<card slot>)
```

**Description:**
Returns value from equipped item slot in the indicated slot (0, 1, 2, or 3).

---

### mergeitem

<!-- RAG_CHUNK: cmd_mergeitem -->

**Signature:**
```c
*mergeitem({,<char_id>});
```

**Description:**
Open merge item window to merge available item can be merged.

**Example:**
```c
    mes "Let's check if any item can be merged.";
    close2;
    mergeitem;
    end;

```

---

### mergeitem2

<!-- RAG_CHUNK: cmd_mergeitem2 -->

**Signature:**
```c
*mergeitem2({<item_id>{,<char_id>}});
```

---

### mergeitem2

<!-- RAG_CHUNK: cmd_mergeitem2 -->

**Signature:**
```c
*mergeitem2({"<item name>"{,<char_id>}});
```

**Description:**
Merge all stackable items that separated by GUID flags (UniqueId in item_db or in item_group). If no item ID/name given, all possible items in player's inventory will be merged.

---

### getequiptradability

<!-- RAG_CHUNK: cmd_getequiptradability -->

**Signature:**
```c
*getequiptradability(<equipment slot>{,<char id>});
```

**Description:**
Returns true if the item in <equipment slot> is tradable. Returns false otherwise.

---

### identifyall

<!-- RAG_CHUNK: cmd_identifyall -->

**Signature:**
```c
*identifyall({<type>{,<account_id>}});
```

**Description:**
Returns the count of unidentified items in the player inventory. If <type> is true the command will identify all the unidentified items as well (default). If <type> is false the command only returns the count of unidentified items.

---

### getenchantgrade

<!-- RAG_CHUNK: cmd_getenchantgrade -->

**Signature:**
```c
*getenchantgrade({<equipment slot>,<char_id>})
```

**Description:**
This function will return the enchantgrade of the equipment from which the function is called or the specified equipment slot. If nothing is equipped there, it returns -1.

---

### getitempos

<!-- RAG_CHUNK: cmd_getitempos -->

**Signature:**
```c
*getitempos()
```

**Description:**
This function will return the equip position of the equipment from which the function is called. (see EQP_* constants)

---

### getmapxy

<!-- RAG_CHUNK: cmd_getmapxy -->

**Signature:**
```c
*getmapxy("<variable for map name>",<variable for x>,<variable for y>{,<type>,"<search value>"})
```

**Description:**
This function will locate a character object, NPC object or pet's coordinates and place their coordinates into the variables specified when calling it. It will return 0 if the search was successful, and -1 if the parameters given were not variables or the search was not successful.

**Example:**
```c
	BL_PC   - Character object (default)
	BL_NPC  - NPC object
	BL_PET  - Pet object
	BL_HOM  - Homunculus object
	BL_MER  - Mercenary object
	BL_ELEM - Elemental object

```

---

### mapid2name

<!-- RAG_CHUNK: cmd_mapid2name -->

**Signature:**
```c
*mapid2name(<map ID>)
```

**Description:**
Returns the map name of the given map ID. Returns an empty string if given map ID doesn't exist.

---

### mapname2id

<!-- RAG_CHUNK: cmd_mapname2id -->

**Signature:**
```c
*mapname2id(<"map name">)
```

**Description:**
Returns the map ID of the given map name or -1 if the given map name doesn't exist or is on another map-server.

---

### getgmlevel

<!-- RAG_CHUNK: cmd_getgmlevel -->

**Signature:**
```c
*getgmlevel({<char_id>})
```

**Description:**
This function will return the (GM) level associated with the player group to which the invoking character belongs. If this is somehow executed from a console command, 99 will be returned, and 0 will be returned if the account has no GM level.

---

### getgroupid

<!-- RAG_CHUNK: cmd_getgroupid -->

**Signature:**
```c
*getgroupid({<char_id>})
```

**Description:**
This function will return the group id to which the invoking player belongs.

---

### gettimetick

<!-- RAG_CHUNK: cmd_gettimetick -->

**Signature:**
```c
*gettimetick(<tick type>)
```

**Description:**
This function will return a tick depending on <tick type>:  0: The server's tick, a measurement in milliseconds used by the server's timer     system. This tick is an unsigned int which loops every ~50 days.  1: The time, in seconds, since the start of the current day.  2: The system time in UNIX epoch time, or the number of seconds elapsed since     January 1st, 1970. Useful for reliably measuring time intervals.

**Example:**
```c
    system. This tick is an unsigned int which loops every ~50 days.
```

---

### gettime

<!-- RAG_CHUNK: cmd_gettime -->

**Signature:**
```c
*gettime(<type>)
```

**Description:**
This function will return specified information about the current system time.

---

### gettimestr

<!-- RAG_CHUNK: cmd_gettimestr -->

**Signature:**
```c
*gettimestr(<"time format">,<max length>{,<time_tick>})
```

**Description:**
This function will return a string containing time data as specified by the time format.

---

### getusers

<!-- RAG_CHUNK: cmd_getusers -->

**Signature:**
```c
*getusers(<type>)
```

**Description:**
This function will return a number of users on a map or the whole server. What it returns is specified by Type.

**Example:**
```c
    0 - Count of all characters on the map of the invoking character.
    1 - Count of all characters in the entire server.
    8 - Count of all characters on the map of the NPC the script is
        running in.

```

---

### getmapusers

<!-- RAG_CHUNK: cmd_getmapusers -->

**Signature:**
```c
*getmapusers("<map name>")
```

**Description:**
This function will return the number of users currently located on the specified map.

---

### getareausers

<!-- RAG_CHUNK: cmd_getareausers -->

**Signature:**
```c
*getareausers("<map name>",<x1>,<y1>,<x2>,<y2>)
```

**Description:**
This function will return the count of connected characters which are located within the specified area - an x1/y1-x2/y2 square on the specified map.

---

### getunits

<!-- RAG_CHUNK: cmd_getunits -->

**Signature:**
```c
*getunits(<type>{,<array_variable>[<first value>]})
```

---

### getmapunits

<!-- RAG_CHUNK: cmd_getmapunits -->

**Signature:**
```c
*getmapunits(<type>,<"map name">{,<array_variable>[<first value>]})
```

---

### getareaunits

<!-- RAG_CHUNK: cmd_getareaunits -->

**Signature:**
```c
*getareaunits(<type>,<"map name">,<x1>,<y1>,<x2>,<y2>{,<array_variable>[<first value>]})
```

**Description:**
The 'getunits' command will return the number of <type> objects active on the server.

**Example:**
```c
	BL_PC   - Character objects
	BL_MOB  - Monster objects
	BL_PET  - Pet objects
	BL_HOM  - Homunculus objects
	BL_MER  - Mercenary objects
	BL_NPC  - NPC objects
	BL_ELEM - Elemental objects

```

---

### getguildname

<!-- RAG_CHUNK: cmd_getguildname -->

**Signature:**
```c
*getguildname(<guild id>)
```

**Description:**
This function returns a guild's name given an ID number. If there is no such guild, "null" will be returned.

**Example:**
```c
	mes "The guild " + getguildname(10007) + " are all nice people.";

```

---

### getguildmember

<!-- RAG_CHUNK: cmd_getguildmember -->

**Signature:**
```c
*getguildmember <guild id>{,<type>{,<array_variable>}};
```

**Description:**
This command will find all members of a specified guild and returns their names (or character id or account id depending on the value of "type") into an array of temporary global variables.

**Example:**
```c
                     names of these guild members.
                     (only set when type is 0 or not specified)

```

---

### getguildmaster

<!-- RAG_CHUNK: cmd_getguildmaster -->

**Signature:**
```c
*getguildmaster(<guild id>)
```

**Description:**
This function return the name of the master of the guild which has the specified ID number. If there is no such guild, "null" will be returned.

**Example:**
```c
	// Prints the guild master of guild 10007, whoever that might be.
	mes getguildmaster(10007) + " runs " + getguildname(10007);

```

---

### getguildmasterid

<!-- RAG_CHUNK: cmd_getguildmasterid -->

**Signature:**
```c
*getguildmasterid(<guild id>)
```

**Description:**
This function will return the character ID number of the guild master of the guild specified by the ID. 0 if the character is not a guild master of any guild.

---

### getguildinfo

<!-- RAG_CHUNK: cmd_getguildinfo -->

**Signature:**
```c
*getguildinfo(<guild ID>, <type>);
```

**Description:**
This function will look up and return the request type of guild information.

**Example:**
```c
	GUILDINFO_NAME              - Guild's Name
	GUILDINFO_LEVEL             - Guild's Level
	GUILDINFO_AVERAGELEVEL      - Guild's Average Level
	GUILDINFO_ONLINECOUNT       - Guild's Online Member Count
	GUILDINFO_MEMBERCOUNT       - Guild's Current Member Count
	GUILDINFO_MAXMEMBERCOUNT    - Guild's Max Member Count
	GUILDINFO_EXP               - Guild's Current EXP
	GUILDINFO_NEXTEXP           - Guild's Required EXP to Level
	GUILDINFO_MASTERID          - Guild Master Character ID
	GUILDINFO_MASTERNAME        - Guild Master Name

```

---

### is_guild_leader

<!-- RAG_CHUNK: cmd_is_guild_leader -->

**Signature:**
```c
*is_guild_leader({<guild ID>})
```

**Description:**
This command will return true if the player attached to the script is the leader of his/her guild, or, if a guild ID is specified, of that guild.

---

### getcastlename

<!-- RAG_CHUNK: cmd_getcastlename -->

**Signature:**
```c
*getcastlename("<map name>")
```

**Description:**
This function returns the name of the castle when given the map name for that castle. The data is read from 'db/castle_db.yml'.

---

### getcastledata

<!-- RAG_CHUNK: cmd_getcastledata -->

**Signature:**
```c
*getcastledata("<map name>",<type of data>)
```

---

### setcastledata

<!-- RAG_CHUNK: cmd_setcastledata -->

**Signature:**
```c
*setcastledata "<map name>",<type of data>,<value>;
```

**Description:**
This function returns the castle ownership information for the castle referred to by its map name. Castle information is stored in `guild_castle` SQL table.

---

### getgdskilllv

<!-- RAG_CHUNK: cmd_getgdskilllv -->

**Signature:**
```c
*getgdskilllv(<guild id>,<skill id>)
```

---

### getgdskilllv

<!-- RAG_CHUNK: cmd_getgdskilllv -->

**Signature:**
```c
*getgdskilllv(<guild id>,"<skill name>")
```

**Description:**
This function returns the level of the skill <skill id> of the guild <guild id>. If the guild does not have that skill, 0 is returned. If the guild does not exist, -1 is returned. Refer to 'db/(pre-)re/skill_db.yml' for the full list of skills. (GD_* are guild skills)

---

### requestguildinfo

<!-- RAG_CHUNK: cmd_requestguildinfo -->

**Signature:**
```c
*requestguildinfo <guild id>{,"<event label>"};
```

**Description:**
This command requests the guild data from the char server and merrily continues with the execution. Whenever the guild information becomes available (which happens instantly if the guild information is already in memory, or later, if it isn't and the map server has to wait for the char server to reply) it will run the specified event as in a 'donpcevent' call.

---

### getmapguildusers

<!-- RAG_CHUNK: cmd_getmapguildusers -->

**Signature:**
```c
*getmapguildusers("<map name>",<guild id>)
```

**Description:**
Returns the amount of characters from the specified guild on the given map.

---

### getskilllv

<!-- RAG_CHUNK: cmd_getskilllv -->

**Signature:**
```c
*getskilllv(<skill id>)
```

---

### getskilllv

<!-- RAG_CHUNK: cmd_getskilllv -->

**Signature:**
```c
*getskilllv("<skill name>")
```

**Description:**
This function returns the level of the specified skill that the invoking character has. If they don't have the skill, 0 will be returned. The full list of character skills is available in 'db/(pre-)re/skill_db.yml'.

**Example:**
```c
	if (getskilllv(152))
		mes "You have got the skill Throw Stone";
	else
		mes "You don't have Throw Stone";
	close;

```

---

### getskilllist

<!-- RAG_CHUNK: cmd_getskilllist -->

**Signature:**
```c
*getskilllist({<char_id>});
```

**Description:**
This command sets a bunch of arrays with a complete list of skills the invoking character has. Here's what you get:

---

### getrandmobid

<!-- RAG_CHUNK: cmd_getrandmobid -->

**Signature:**
```c
*getrandmobid(<type>{,<flag>{,<level>}})
```

**Description:**
This command returns a random monster ID from the random monster group. With <flag> you can apply certain restrictions which monsters of the group can be returned. Returns 0 if one of the parameters is invalid or no monster could be found with the given parameters.

**Example:**
```c
	MOBG_BRANCH_OF_DEAD_TREE
	MOBG_PORING_BOX
	MOBG_BLOODY_DEAD_BRANCH
	MOBG_RED_POUCH_OF_SURPRISE
	MOBG_CLASSCHANGE
	MOBG_TAEKWON_MISSION
	
```

---

### getmonsterinfo

<!-- RAG_CHUNK: cmd_getmonsterinfo -->

**Signature:**
```c
*getmonsterinfo(<mob ID>,<type>)
```

---

### getmonsterinfo

<!-- RAG_CHUNK: cmd_getmonsterinfo -->

**Signature:**
```c
*getmonsterinfo(<mob name>,<type>)
```

**Description:**
This function will look up the monster with the specified <mob ID> or <mob name> in the mob database and return the info set by <type> argument. It will return -1 if there is no such monster (or the type value is invalid), or "null" if you requested the monster's name.

**Example:**
```c
	MOB_NAME          - monster's japanese name
	MOB_LV            - monster's level
	MOB_MAXHP         - monster's maximum hp
	MOB_BASEEXP       - monster's base experience
	MOB_JOBEXP        - monster's job experience
	MOB_ATKMIN        - monster's minimum atk
	MOB_ATKMAX        - monster's maximum atk
	MOB_DEF           - monster's def
	MOB_MDEF          - monster's mdef
	MOB_RES           - monster's res
	MOB_MRES          - monster's mres
	MOB_STR           - monster's str
	MOB_AGI           - monster's agi
	MOB_VIT           - monster's vit
	MOB_INT           - monster's int
```

---

### getmobdrops

<!-- RAG_CHUNK: cmd_getmobdrops -->

**Signature:**
```c
*getmobdrops(<mob id>)
```

**Description:**
This command will find all drops of the specified mob and return the item IDs and drop percentages into arrays of temporary global variables. 'getmobdrops' returns 1 if successful and 0 if the mob ID doesn't exist.

**Example:**
```c
                 item IDs of the monster's drops.

```

---

### skillpointcount

<!-- RAG_CHUNK: cmd_skillpointcount -->

**Signature:**
```c
*skillpointcount({<char_id>})
```

**Description:**
Returns the total amount of skill points a character possesses (SkillPoint+SP's used in skills) This command can be used to check the currently attached characters total amount of skill points. This means the skill points used in skill are counted, and added to SkillPoints (number of skill points not used). This command does not count skills which are set as flag 4 (permament granted) (ALL_BUYING_STORE/ALL_INCCARRY)

**Example:**
```c
	.@skillPoints = skillpointcount();
	mes "You have " + .@skillPoints + " skill points in total!";

```

---

### getscrate

<!-- RAG_CHUNK: cmd_getscrate -->

**Signature:**
```c
*getscrate(<effect type>,<base rate>{,<GID>})
```

**Description:**
This function will return the chance of a status effect affecting the invoking character, in percent, modified by the their current defense against said status. The 'base rate' is the base chance of the status effect being inflicted, in percent.

**Example:**
```c
    if (rand(100) > getscrate(Eff_Blind, 50)) goto BlindHimNow;

```

---

### playerattached

<!-- RAG_CHUNK: cmd_playerattached -->

**Signature:**
```c
*playerattached()
```

**Description:**
Returns the ID of the player currently attached to the script. It will return 0 if no one is attached, or if the attached player no longer exists on the map server. It is wise to check for the attached player in script functions that deal with timers as there's no guarantee the player will still be logged on when the timer triggers. Note that the ID of a player is actually their account ID.

---

### getattachedrid

<!-- RAG_CHUNK: cmd_getattachedrid -->

**Signature:**
```c
*getattachedrid();
```

**Description:**
Returns RID from running script. Script may not be attached to any RID like a floating script or function and will return 0.

---

### isloggedin

<!-- RAG_CHUNK: cmd_isloggedin -->

**Signature:**
```c
*isloggedin(<account id>{,<char id>})
```

**Description:**
This function returns 1 if the specified account is logged in and 0 if they aren't. You can also pass the char id to check for both account and char id.

---

### checkweight

<!-- RAG_CHUNK: cmd_checkweight -->

**Signature:**
```c
*checkweight(<item id>,<amount>{,<item id>,<amount>,<item id>,<amount>,...});
```

---

### checkweight

<!-- RAG_CHUNK: cmd_checkweight -->

**Signature:**
```c
*checkweight("<item name>",<amount>{,"<item name>",<amount>,"<item name>",<amount>,...});
```

---

### checkweight2

<!-- RAG_CHUNK: cmd_checkweight2 -->

**Signature:**
```c
*checkweight2(<id_array>,<amount_array>);
```

**Description:**
These functions will compute and return 1 if the total weight of the specified number of specific items does not exceed the invoking character's carrying capacity, and 0 otherwise. It is important to see if a player can carry the items you expect to give them, failing to do that may open your script up to abuse or create some very unfair errors.

**Example:**
```c
	if (checkweight(512,10)) {
		getitem 512,10;
	} else {
		mes "Sorry, you cannot hold this amount of apples!";
	}

```

---

### basicskillcheck

<!-- RAG_CHUNK: cmd_basicskillcheck -->

**Signature:**
```c
*basicskillcheck()
```

**Description:**
This function will return the state of the configuration option 'basic_skill_check' in 'battle_athena.conf'. It returns 1 if the option is enabled and 0 if it isn't. If the 'basic_skill_check' option is enabled, which it is by default, characters must have a certain number of basic skill levels to sit, request a trade, use emotions, etc. Making your script behave differently depending on whether the characters must actually have the skill to do all these things might in some cases be required.

---

### checkoption

<!-- RAG_CHUNK: cmd_checkoption -->

**Signature:**
```c
*checkoption(<option number>{,<char_id>})
```

---

### checkoption1

<!-- RAG_CHUNK: cmd_checkoption1 -->

**Signature:**
```c
*checkoption1(<option number>{,<char_id>})
```

---

### checkoption2

<!-- RAG_CHUNK: cmd_checkoption2 -->

**Signature:**
```c
*checkoption2(<option number>{,<char_id>})
```

---

### setoption

<!-- RAG_CHUNK: cmd_setoption -->

**Signature:**
```c
*setoption <option number>{,<flag>{,<char_id>}};
```

**Description:**
The 'setoption' series of functions check for a so-called option that is set on the invoking character. 'Options' are used to store status conditions and a lot of other non-permanent character data of the yes-no kind. For most common cases, it is better to use 'checkcart','checkfalcon','checkriding' and other similar functions, but there are some options which you cannot get at this way. They return 1 if the option is set and 0 if the option is not set.

---

### setcart

<!-- RAG_CHUNK: cmd_setcart -->

**Signature:**
```c
*setcart {<type>{,<char_id>}};
```

---

### checkcart

<!-- RAG_CHUNK: cmd_checkcart -->

**Signature:**
```c
*checkcart({<char_id>});
```

**Description:**
If <type> is 0 this command will remove the cart from the character. Otherwise it gives the invoking character a cart. The cart given will be cart number <type> and will work regardless of whether the character is a merchant class or not. Note: the character needs to have the skill MC_PUSHCART to gain a cart

**Example:**
```c
    if (checkcart()) mes "But you already have a cart!";

```

---

### setfalcon

<!-- RAG_CHUNK: cmd_setfalcon -->

**Signature:**
```c
*setfalcon {<flag>{,<char_id>}};
```

---

### checkfalcon

<!-- RAG_CHUNK: cmd_checkfalcon -->

**Signature:**
```c
*checkfalcon({<char_id>});
```

**Description:**
If <flag> is 0 this command will remove the falcon from the character. Otherwise it gives the invoking character a falcon. The falcon will be there regardless of whether the character is a hunter or not. It will (probably) not have any useful effects for non-hunters though. Note: the character needs to have the skill HT_FALCON to gain a falcon

**Example:**
```c
    if (checkfalcon()) mes "But you already have a falcon!";

```

---

### setriding

<!-- RAG_CHUNK: cmd_setriding -->

**Signature:**
```c
*setriding {<flag>{,<char_id>}};
```

---

### checkriding

<!-- RAG_CHUNK: cmd_checkriding -->

**Signature:**
```c
*checkriding({<char_id>});
```

**Description:**
If <flag> is 0 this command will remove the mount from the character. Otherwise it gives the invoking character a PecoPeco (if they are a Knight series class), a GrandPeco (if they are a Crusader series class), or a Gryphon (if they are a Royal Guard). Unlike 'setfalcon' and 'setcart' this will not work at all if they aren't of a class which can ride. Note: the character needs to have the skill KN_RIDING to gain a mount

**Example:**
```c
    if (checkriding()) mes "PLEASE leave your bird outside! No riding birds on the floor here!";

```

---

### setdragon

<!-- RAG_CHUNK: cmd_setdragon -->

**Signature:**
```c
*setdragon {<color>{,<char_id>}};
```

---

### checkdragon

<!-- RAG_CHUNK: cmd_checkdragon -->

**Signature:**
```c
*checkdragon({<char_id>});
```

**Description:**
The 'setdragon' function toggles mounting a dragon for the invoking character. It will return 1 if successful, 0 otherwise.

---

### setmadogear

<!-- RAG_CHUNK: cmd_setmadogear -->

**Signature:**
```c
*setmadogear {<flag>{,<type>{,<char_id>}}};
```

---

### checkmadogear

<!-- RAG_CHUNK: cmd_checkmadogear -->

**Signature:**
```c
*checkmadogear({<char_id>});
```

**Description:**
If <flag> is false this command will remove the mount from the character. Otherwise it gives the invoking character a Mado (if they are a Mechanic and have the skill NC_MADOLICENCE).

---

### setmounting

<!-- RAG_CHUNK: cmd_setmounting -->

**Signature:**
```c
*setmounting {<char_id>};
```

---

### ismounting

<!-- RAG_CHUNK: cmd_ismounting -->

**Signature:**
```c
*ismounting({<char_id>});
```

**Description:**
The 'setmounting' function toggles cash mount for the invoking character. It will return 1 if successful, 0 otherwise.

---

### checkwug

<!-- RAG_CHUNK: cmd_checkwug -->

**Signature:**
```c
*checkwug({<char_id>});
```

**Description:**
This function will return 1 if the invoking character has a warg and 0 if they don't.

---

### checkvending

<!-- RAG_CHUNK: cmd_checkvending -->

**Signature:**
```c
*checkvending({"<Player Name>"})
```

**Description:**
Checks if the player is vending or has has a buyingstore. Additionally it gives you the information whether the player uses autotrade or not. Name is optional, and defaults to the attached player if omitted.

**Example:**
```c
	//This will check Aaron's state
	.@state = checkvending("Aaron");
	if (.@state&1)
		mes "Aaron is currently vending!";
	if (.@state&4)
		mes "Aaron has a buying store!";
	if (.@state&2)
		mes "Aaron is autotrading!";

```

---

### checkchatting

<!-- RAG_CHUNK: cmd_checkchatting -->

**Signature:**
```c
*checkchatting({"<Player Name>"})
```

**Description:**
Checks if the player is in a chatroom. Name is optional, and defaults to the attached player if omitted. Returns 1 if they are in a chat room, 0 if they are not.

**Example:**
```c
	//This will check if the attached player in a chat room or not.
	if (checkchatting())
		mes "You are currently in a chat room!";

```

---

### checkidle

<!-- RAG_CHUNK: cmd_checkidle -->

**Signature:**
```c
*checkidle({"<Player Name>"})
```

**Description:**
Returns the time, in seconds, that the specified player has been idle. Name is optional, and defaults to the attached player if omitted.

---

### checkidlehom

<!-- RAG_CHUNK: cmd_checkidlehom -->

**Signature:**
```c
*checkidlehom({"<Player Name>"})
```

**Description:**
Returns the time, in seconds, that the specified player has been idle for homunculus item/exp share. Name is optional, and defaults to the attached player if omitted. This will only work if 'hom_idle_no_share' and 'idletime_hom_option' are enabled (see '/conf/battle/homunc.conf').

---

### checkidlemer

<!-- RAG_CHUNK: cmd_checkidlemer -->

**Signature:**
```c
*checkidlemer({"<Player Name>"})
```

**Description:**
Returns the time, in seconds, that the specified player has been idle for mercenary item share. Name is optional, and defaults to the attached player if omitted. This will only work if 'mer_idle_no_share' and 'idletime_mer_option' are enabled (see '/conf/battle/drops.conf').

---

### agitcheck

<!-- RAG_CHUNK: cmd_agitcheck -->

**Signature:**
```c
*agitcheck()
```

---

### agitcheck2

<!-- RAG_CHUNK: cmd_agitcheck2 -->

**Signature:**
```c
*agitcheck2()
```

---

### agitcheck3

<!-- RAG_CHUNK: cmd_agitcheck3 -->

**Signature:**
```c
*agitcheck3()
```

**Description:**
These function will let you check whether the server is currently in WoE:FE mode (agitcheck()), WoE:SE mode (agitcheck2()), or WoE:TE mode (agitcheck3()) and will return true if War of Emperium is on and false if it isn't.

---

### isnight

<!-- RAG_CHUNK: cmd_isnight -->

**Signature:**
```c
*isnight()
```

---

### isday

<!-- RAG_CHUNK: cmd_isday -->

**Signature:**
```c
*isday()
```

**Description:**
These functions will return 1 or 0 depending on whether the server is in night mode or day mode. 'isnight' returns 1 if it's night and 0 if it isn't, 'isday' the other way around. They can be used interchangeably, pick the one you like more:

**Example:**
```c
    // These two are equivalent:
    if (isday()) mes "I only prowl in the night.";
    if (isnight() != 1) mes "I only prowl in the night.";

```

---

### checkre

<!-- RAG_CHUNK: cmd_checkre -->

**Signature:**
```c
*checkre(<type>)
```

**Description:**
Checks if a renewal feature is enabled or not in renewal.hpp, and returns 1 if enabled and 0 for disabled.

---

### isequipped

<!-- RAG_CHUNK: cmd_isequipped -->

**Signature:**
```c
*isequipped(<id>{,<id>{,..}})
```

**Description:**
This function will return 1 if the invoking character has all of the item IDs given equipped (if item/card IDs are passed, then it checks if the items/cards are inserted into slots in the equipment they are currently wearing). Theoretically there is no limit to the number of items that may be tested for at the same time. If even one of the items given is not equipped, 0 will be returned.

**Example:**
```c
    // (Poring,Santa Poring,Poporing,Marin)
    if (isequipped(4001,4005,4033,4196)) mes "Wow! You're wearing a full complement of possible poring cards!";
    // (Poring)
    if (isequipped(4001)) mes "A poring card is useful, don't you think?";

```

---

### isequippedcnt

<!-- RAG_CHUNK: cmd_isequippedcnt -->

**Signature:**
```c
*isequippedcnt(<id>{,<id>{,..}})
```

**Description:**
This function is similar to 'isequipped', but instead of 1 or 0, it will return the amount of item/card equipped that were found on the invoking character from the given list.

**Example:**
```c
    if (isequippedcnt(4001,4005,4033,4196) == 5)
		mes "Finally got 5 cards from poring monsters type?";

```

---

### checkequipedcard

<!-- RAG_CHUNK: cmd_checkequipedcard -->

**Signature:**
```c
*checkequipedcard(<item id>)
```

**Description:**
This function will return 1 if the item/card specified by its item ID number is inserted into any equipment they have in their inventory, currently equipped or not.

---

### attachrid

<!-- RAG_CHUNK: cmd_attachrid -->

**Signature:**
```c
*attachrid(<account ID>{,force})
```

---

### detachrid

<!-- RAG_CHUNK: cmd_detachrid -->

**Signature:**
```c
*detachrid;
```

**Description:**
These commands allow the manipulation of the script's currently attached player. While 'attachrid' allows attaching of a different player by using its account id for the parameter RID, 'detachrid' makes the following commands run as if the script was never invoked by a player.

---

### addrid

<!-- RAG_CHUNK: cmd_addrid -->

**Signature:**
```c
*addrid(<type>{,<flag>{,<parameters>}});
```

**Description:**
This command will attach other RIDs to the current script without detaching the invoking RID. It returns 1 if successful and 0 upon failure.

**Example:**
```c
    [ Parameters: <party id> ]
```

---

### rid2name

<!-- RAG_CHUNK: cmd_rid2name -->

**Signature:**
```c
*rid2name(<rid>)
```

**Description:**
Converts rid to name. Note: The player/monster/NPC must be online/enabled. Good for PCKillEvent where you can convert 'killedrid' to the name of the player.

**Example:**
```c
      It will return the current online character of the account only.

```

---

### message

<!-- RAG_CHUNK: cmd_message -->

**Signature:**
```c
*message "<character name>","<message>";
```

**Description:**
That command will send a message to the chat window of the character specified by name. The text will also appear above the head of that character. It will not be seen by anyone else.

---

### dispbottom

<!-- RAG_CHUNK: cmd_dispbottom -->

**Signature:**
```c
*dispbottom "<message>"{,<color>{,<char_id>}};
```

**Description:**
This command will send the given message with color into the invoking character's chat window. The color format is in RGB (0xRRGGBB). The color is by default green

---

### showscript

<!-- RAG_CHUNK: cmd_showscript -->

**Signature:**
```c
*showscript "<message>"{,<GID>, <flag>};
```

**Description:**
Makes attached player or GID says a message like shouting a skill name, the message will be seen to everyone around but not in chat window. flag: Specify target    AREA - Message is sent to players in the vicinity of the source (default).    SELF - Message is sent only to player attached.

---

### warp

<!-- RAG_CHUNK: cmd_warp -->

**Signature:**
```c
*warp "<map name>",<x>,<y>{,<char id>};
```

**Description:**
This command will take the invoking character or <char id>, if specified, to the specified map, and if wanted, specified coordinates too, but these can be random.

---

### areawarp

<!-- RAG_CHUNK: cmd_areawarp -->

**Signature:**
```c
*areawarp "<from map name>",<x1>,<y1>,<x2>,<y2>,"<to map name>",<x3>,<y3>{,<x4>,<y4>};
```

**Description:**
This command is similar to 'warp', however, it will not refer to the invoking character, but instead, all characters within a specified area, defined by the x1/y1-x2/y2 square, will be warped. Nobody outside the area will be affected, including the activating character, if they are outside the area.

---

### warpparty

<!-- RAG_CHUNK: cmd_warpparty -->

**Signature:**
```c
*warpparty "<to_mapname>",<x>,<y>,<party_id>,{"<from_mapname>",<range x>,<range y>};
```

**Description:**
Warps a party to specified map and coordinate given the party ID, which you can get with getcharid(1). You can also request another party id given a member's name with getcharid(1,<player_name>).

**Example:**
```c
              all used a fly wing)
```

---

### warpguild

<!-- RAG_CHUNK: cmd_warpguild -->

**Signature:**
```c
*warpguild "<map name>",<x>,<y>,<guild_id>;
```

**Description:**
Warps a guild to specified map and coordinate given the guild id, which you can get with getcharid(2). You can also request another guild id given the member's name with getcharid(2,<player_name>).

**Example:**
```c
              all used a fly wing)
```

---

### warppartner

<!-- RAG_CHUNK: cmd_warppartner -->

**Signature:**
```c
*warppartner("<map name>",<x>,<y>);
```

**Description:**
This function will find the invoking character's marriage partner, if any, and warp them to the map and coordinates given. It will return 1 upon success and 0 if the partner is not online, the character is not married, or if there's no invoking character (no RID). 0,0 will, as usual, normally translate to random coordinates.

---

### savepoint

<!-- RAG_CHUNK: cmd_savepoint -->

**Signature:**
```c
*savepoint "<map name>",<x>,<y>{,{<range x>,<range y>,}<char_id>};
```

---

### save

<!-- RAG_CHUNK: cmd_save -->

**Signature:**
```c
*save "<map name>",<x>,<y>{,{<range x>,<range y>,}<char_id>};
```

**Description:**
These commands save where the invoking character will return to upon clicking "Return to Save Point", after death and in some other cases. The two versions are equivalent. They ignore any and all mapflags, and can make a character respawn where no teleportation is otherwise possible.

---

### heal

<!-- RAG_CHUNK: cmd_heal -->

**Signature:**
```c
*heal <hp>,<sp>{,<char_id>};
```

**Description:**
This command will heal a set amount of HP and/or SP on the invoking character.

---

### healap

<!-- RAG_CHUNK: cmd_healap -->

**Signature:**
```c
*healap <ap>{,<char_id>};
```

**Description:**
This command will heal a set amount of AP on the invoking character.

---

### itemheal

<!-- RAG_CHUNK: cmd_itemheal -->

**Signature:**
```c
*itemheal <hp>,<sp>{,<char_id>};
```

**Description:**
This command heals relative amounts of HP and/or SP on the invoking character. Unlike heal, this command is intended for use in item scripts. It applies potion-related bonuses, such as alchemist ranking, cards, and status changes. When used inside an NPC script, certain bonuses are omitted.

**Example:**
```c
	heal = heal * [(100 + STATUS*2) / 100]

```

---

### percentheal

<!-- RAG_CHUNK: cmd_percentheal -->

**Signature:**
```c
*percentheal <hp>,<sp>{,<char_id>};
```

**Description:**
This command will heal the invoking character. It heals the character, but not by a set value - it adds percent of their maximum HP/SP.

---

### recovery

<!-- RAG_CHUNK: cmd_recovery -->

**Signature:**
```c
*recovery <type>{,<option>,<revive_flag>{,<map name>}};
```

**Description:**
This command will revive and fully restore the HP/SP of the selected characters. It returns 1 upon successful use.

**Example:**
```c
	// Only revive characters in invoking party on map "morocc"
	recovery 1,getcharid(1),4,"morocc";

	// Fully heal (don't revive) all members of invoking character's guild
	recovery 2,getcharid(2),2;

	// Revive and fully heal everyone in map "prontera"
	recovery 3,"prontera";

	// Only revive all dead characters on server
	recovery 4,4;

```

---

### jobchange

<!-- RAG_CHUNK: cmd_jobchange -->

**Signature:**
```c
*jobchange <job number>{,<upper flag>,<char_id>};
```

**Description:**
This command will change the job class of the invoking character.

**Example:**
```c
	jobchange 1; // This would change your player into a Swordman
	jobchange 4002; // This would change your player into a Swordman High

```

---

### jobname

<!-- RAG_CHUNK: cmd_jobname -->

**Signature:**
```c
*jobname(<job number>)
```

**Description:**
This command retrieves the name of the given job using the map_msg entries 550->655.

---

### eaclass

<!-- RAG_CHUNK: cmd_eaclass -->

**Signature:**
```c
*eaclass({<job number>,<char_id>})
```

**Description:**
This commands returns the "eA job-number" corresponding to the given class, and uses the invoking player's class if none is given. The eA job-number is also a class number system, but it's one that comes with constants which make it easy to convert among classes. The command will return -1 if you pass it a job number which doesn't have an eA job-number equivalent.

---

### roclass

<!-- RAG_CHUNK: cmd_roclass -->

**Signature:**
```c
*roclass(<job number>{,<gender>})
```

**Description:**
Does the opposite of eaclass. That is, given an eA job-number, it returns the corresponding RO class number. A gender is required because both Bard and Dancers share the same eA job-number (EAJ_BARDDANCER), and uses the invoking player's gender if none is given (if no player is attached, male will be used by default). The command will return -1 if there is no valid class to represent the specified job (for example, if you try to get the baby version of a Taekwon class).

**Example:**
```c
	.@eac = eaclass();
	//Check if class is already rebirth
	if (.@eac&EAJL_UPPER) {
		mes "You look strong.";
		close;
	}
	.@eac = roclass(.@eac|EAJL_UPPER);
	//Check if class has a rebirth version
	if (.@eac != -1) {
		mes "Bet you can't wait to become a " + jobname(.@eac) + "!";
		close;
	}

```

---

### changebase

<!-- RAG_CHUNK: cmd_changebase -->

**Signature:**
```c
*changebase <job ID number>{,<account ID>};
```

**Description:**
This command will change a character's appearance to that of the specified job class. Nothing but appearance will change.

---

### classchange

<!-- RAG_CHUNK: cmd_classchange -->

**Signature:**
```c
*classchange(<view id>{,"<NPC name>","<flag>"});
```

**Description:**
This command is very ancient, its origins are clouded in mystery. It will send a 'display id change' packet to everyone in the immediate area of the NPC object, which will supposedly make the NPC look like a different sprite, an NPC sprite ID, or a monster ID. This effect is not stored anywhere and will not persist (Which is odd, cause it would be relatively easy to make it do so) and most importantly, will not work at all since this command was broken with the introduction of advanced classes. The code is written with the assumption that the lowest sprite IDs are the job sprites and the anything beyond them is monster and NPC sprites, but since the advanced classes rolled in, they got the ID numbers on the other end of the number pool where monster sprites float.

---

### changesex

<!-- RAG_CHUNK: cmd_changesex -->

**Signature:**
```c
*changesex({<char_id>});
```

**Description:**
This command will change the gender for the attached character's account. If it was male, it will become female, if it was female, it will become male. The change will be written to the character server, the player will receive the message: "Need disconnection to perform change-sex request..." and the player will be immediately kicked to the login screen. When they log back in, they will be the opposite sex.

---

### changecharsex

<!-- RAG_CHUNK: cmd_changecharsex -->

**Signature:**
```c
*changecharsex({<char_id>});
```

**Description:**
This command will change the gender of the attached character. If it was male, it will become female, if it was female, it will become male. The change will be written to the character server, the player will receive the message: "Need disconnection to perform change-sex request..." and the player will be immediately kicked to the login screen. When they log back in, they will be the opposite sex.

---

### getexp

<!-- RAG_CHUNK: cmd_getexp -->

**Signature:**
```c
*getexp <base_exp>,<job_exp>{,<char_id>};
```

**Description:**
This command will give the invoking character a specified number of base and job experience points. Used for a quest reward. Negative values won't work.

---

### getexp2

<!-- RAG_CHUNK: cmd_getexp2 -->

**Signature:**
```c
*getexp2 <base_exp>,<job_exp>{,<char_id>};
```

**Description:**
This command is safety version of 'set' command for BaseExp and JobExp. If using 'set' while the BaseExp or JobExp value is more than 2,147,483,647 (INT_MAX) will causing overflow error.

---

### getbaseexp_ratio

<!-- RAG_CHUNK: cmd_getbaseexp_ratio -->

**Signature:**
```c
*getbaseexp_ratio(<percent>{,<base_level>{,char_id});
```

**Description:**
Returns the amount of base experience representing the given <percent> of the required base experience at <base_level>. If no base level is specified the base level of the attached character will be used.

---

### getjobexp_ratio

<!-- RAG_CHUNK: cmd_getjobexp_ratio -->

**Signature:**
```c
*getjobexp_ratio(<percent>{,<job_level>{,char_id});
```

**Description:**
Returns the amount of job experience representing the given <percent> of the required job experience at <job_level>. If no job level is specified the job level of the attached character will be used.

---

### setlook

<!-- RAG_CHUNK: cmd_setlook -->

**Signature:**
```c
*setlook <look type>,<look value>{,<char_id>};
```

---

### changelook

<!-- RAG_CHUNK: cmd_changelook -->

**Signature:**
```c
*changelook <look type>,<look value>{,<char_id>};
```

**Description:**
'setlook' will alter the look data for the invoking character. It is used mainly for changing the palette used on hair and clothes: you specify which look type you want to change, then the palette you want to use. Make sure you specify a palette number that exists/is usable by the client you use. 'changelook' works the same, but is only client side (it doesn't save the look value).

**Example:**
```c
	// This will change your hair color, so that it uses palette 8, what ever your
	// palette 8 is, your hair will use that color

	setlook LOOK_HAIR_COLOR,8;

	// This will change your clothes color, so they are using palette 1, whatever
	// your palette 1 is, your clothes will then use that set of colors.

	setlook LOOK_CLOTHES_COLOR,1;

```

---

### pushpc

<!-- RAG_CHUNK: cmd_pushpc -->

**Signature:**
```c
*pushpc <direction>,<cells>;
```

**Description:**
This command will push the currently attached player to given direction by given amount of square cells. Direction is the same as used when declaring NPCs, and can be specified by using one of the DIR_* constants (src/map/script_constants.hpp).

---

### kick

<!-- RAG_CHUNK: cmd_kick -->

**Signature:**
```c
*kick({<char_id>});
```

**Description:**
This command kicks the attached character (or character provided by <char_id>) from the map server, just like @kick.

---

### recalculatestat

<!-- RAG_CHUNK: cmd_recalculatestat -->

**Signature:**
```c
*recalculatestat;
```

**Description:**
This command will force a stat recalculation for the attached player.

---

### needed_status_point

<!-- RAG_CHUNK: cmd_needed_status_point -->

**Signature:**
```c
*needed_status_point(<type>,<val>{,<char id>});
```

**Description:**
Returns the number of stat points needed to change the specified stat <type> by <val>. If <val> is negative, returns the number of stat points that would be needed to raise the specified stat from (current value - <val>) to current value.

---

### jobcanentermap

<!-- RAG_CHUNK: cmd_jobcanentermap -->

**Signature:**
```c
*jobcanentermap("<mapname>"{,<JobID>});
```

**Description:**
Return true if player (decided by job) can enter the map, false otherwise.

---

### get_revision

<!-- RAG_CHUNK: cmd_get_revision -->

**Signature:**
```c
*get_revision()
```

**Description:**
This command will return the SVN revision number that the server is currently running on.

---

### get_githash

<!-- RAG_CHUNK: cmd_get_githash -->

**Signature:**
```c
*get_githash()
```

**Description:**
This command will return the Git Hash that the server is currently running on.

---

### getitem

<!-- RAG_CHUNK: cmd_getitem -->

**Signature:**
```c
*getitem <item id>,<amount>{,<account ID>};
```

---

### getitem

<!-- RAG_CHUNK: cmd_getitem -->

**Signature:**
```c
*getitem "<item name>",<amount>{,<account ID>};
```

**Description:**
This command will give an amount of specified items to the invoking character. If an optional account ID is specified, and the target character is currently online, items will be created in their inventory instead. If they are not online, nothing will happen.

**Example:**
```c
	getitem 502,10 // The person will receive 10 apples
	getitem 617,1  // The person will receive 1 Old Violet Box

```

---

### getitem2

<!-- RAG_CHUNK: cmd_getitem2 -->

**Signature:**
```c
*getitem2 <item id>,<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<account ID>};
```

---

### getitem2

<!-- RAG_CHUNK: cmd_getitem2 -->

**Signature:**
```c
*getitem2 "<item name>",<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<account ID>};
```

---

### getitem3

<!-- RAG_CHUNK: cmd_getitem3 -->

**Signature:**
```c
*getitem3 <item id>,<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account ID>};
```

---

### getitem3

<!-- RAG_CHUNK: cmd_getitem3 -->

**Signature:**
```c
*getitem3 "<item name>",<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account ID>};
```

---

### getitem4

<!-- RAG_CHUNK: cmd_getitem4 -->

**Signature:**
```c
*getitem4 <item id>,<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account ID>};
```

---

### getitem4

<!-- RAG_CHUNK: cmd_getitem4 -->

**Signature:**
```c
*getitem4 "<item name>",<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account ID>};
```

**Description:**
This command will give an amount of specified items to the invoking character. If an optional account ID is specified, and the target character is currently online, items will be created in their inventory instead. If they are not online, nothing will happen. It works essentially the same as 'getitem' but is a lot more flexible.

**Example:**
```c
              It will not let you refine an item higher than the max refine.
```

---

### getitembound

<!-- RAG_CHUNK: cmd_getitembound -->

**Signature:**
```c
*getitembound <item id>,<amount>,<bound type>{,<account ID>};
```

---

### getitembound

<!-- RAG_CHUNK: cmd_getitembound -->

**Signature:**
```c
*getitembound "<item name>",<amount>,<bound type>{,<account ID>};
```

**Description:**
This command behaves identically to 'getitem', but the items created will be bound to the target character as specified by the bound type. All items created in this manner cannot be dropped, sold, vended, auctioned, or mailed, and in some cases cannot be traded or stored.

---

### getitembound2

<!-- RAG_CHUNK: cmd_getitembound2 -->

**Signature:**
```c
*getitembound2 <item id>,<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<bound type>{,<account ID>};
```

---

### getitembound2

<!-- RAG_CHUNK: cmd_getitembound2 -->

**Signature:**
```c
*getitembound2 "<item name>",<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<bound type>{,<account ID>};
```

---

### getitembound3

<!-- RAG_CHUNK: cmd_getitembound3 -->

**Signature:**
```c
*getitembound3 <item id>,<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<bound type>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account ID>};
```

---

### getitembound3

<!-- RAG_CHUNK: cmd_getitembound3 -->

**Signature:**
```c
*getitembound3 "<item name>",<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<bound type>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account ID>};
```

---

### getitembound4

<!-- RAG_CHUNK: cmd_getitembound4 -->

**Signature:**
```c
*getitembound4 <item id>,<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<bound type>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account ID>};
```

---

### getitembound4

<!-- RAG_CHUNK: cmd_getitembound4 -->

**Signature:**
```c
*getitembound4 "<item name>",<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<bound type>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account ID>};
```

**Description:**
This command behaves identically to 'getitem2', but the items created will be bound to the target character as specified by the bound type. All items created in this manner cannot be dropped, sold, vended, auctioned, or mailed, and in some cases cannot be traded or stored.

**Example:**
```c
	ENCHANTGRADE_NONE		- No grade
	ENCHANTGRADE_D			- Grade D
	ENCHANTGRADE_C			- Grade C
	ENCHANTGRADE_B			- Grade B
	ENCHANTGRADE_A			- Grade A

```

---

### getnameditem

<!-- RAG_CHUNK: cmd_getnameditem -->

**Signature:**
```c
*getnameditem <item id>,<character name|character ID>;
```

---

### getnameditem

<!-- RAG_CHUNK: cmd_getnameditem -->

**Signature:**
```c
*getnameditem "<item name>",<character name|character ID>;
```

**Description:**
Create an item signed with the given character's name.

**Example:**
```c
	getnameditem "Apple","Aaron";

```

---

### rentitem

<!-- RAG_CHUNK: cmd_rentitem -->

**Signature:**
```c
*rentitem <item id>,<time>{,<account_id>};
```

---

### rentitem

<!-- RAG_CHUNK: cmd_rentitem -->

**Signature:**
```c
*rentitem "<item name>",<time>{,<account_id>};
```

**Description:**
Creates a rental item in the attached character's inventory. The item will expire in <time> seconds and be automatically deleted. When receiving a rental item, the character will receive a message in their chat window. The character will also receive warning messages in their chat window before the item disappears.

---

### rentitem2

<!-- RAG_CHUNK: cmd_rentitem2 -->

**Signature:**
```c
*rentitem2 <item id>,<time>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<account_id>};
```

---

### rentitem2

<!-- RAG_CHUNK: cmd_rentitem2 -->

**Signature:**
```c
*rentitem2 "<item name>",<time>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<account_id>};
```

---

### rentitem3

<!-- RAG_CHUNK: cmd_rentitem3 -->

**Signature:**
```c
*rentitem3 <item id>,<time>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account_id>};
```

---

### rentitem3

<!-- RAG_CHUNK: cmd_rentitem3 -->

**Signature:**
```c
*rentitem3 "<item name>",<time>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account_id>};
```

---

### rentitem4

<!-- RAG_CHUNK: cmd_rentitem4 -->

**Signature:**
```c
*rentitem4 <item id>,<time>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account_id>};
```

---

### rentitem4

<!-- RAG_CHUNK: cmd_rentitem4 -->

**Signature:**
```c
*rentitem4 "<item name>",<time>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account_id>};
```

**Description:**
Creates a rental item in the attached character's inventory. The item will expire in <time> seconds and be automatically deleted. See 'rentitem' for further details.

**Example:**
```c
	ENCHANTGRADE_NONE		- No grade
	ENCHANTGRADE_D			- Grade D
	ENCHANTGRADE_C			- Grade C
	ENCHANTGRADE_B			- Grade B
	ENCHANTGRADE_A			- Grade A

```

---

### makeitem

<!-- RAG_CHUNK: cmd_makeitem -->

**Signature:**
```c
*makeitem <item id>,<amount>,"<map name>",<X>,<Y>{,<canShowEffect>};
```

---

### makeitem

<!-- RAG_CHUNK: cmd_makeitem -->

**Signature:**
```c
*makeitem "<item name>",<amount>,"<map name>",<X>,<Y>{,<canShowEffect>};
```

**Description:**
This command will create an item on the specified cell of a map.

---

### makeitem2

<!-- RAG_CHUNK: cmd_makeitem2 -->

**Signature:**
```c
*makeitem2 <item id>,<amount>,"<map name>",<X>,<Y>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<canShowEffect>};
```

---

### makeitem2

<!-- RAG_CHUNK: cmd_makeitem2 -->

**Signature:**
```c
*makeitem2 "<item name>",<amount>,"<map name>",<X>,<Y>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<canShowEffect>};
```

---

### makeitem3

<!-- RAG_CHUNK: cmd_makeitem3 -->

**Signature:**
```c
*makeitem3 <item id>,<amount>,"<map name>",<X>,<Y>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<canShowEffect>};
```

---

### makeitem3

<!-- RAG_CHUNK: cmd_makeitem3 -->

**Signature:**
```c
*makeitem3 "<item name>",<amount>,"<map name>",<X>,<Y>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<canShowEffect>};
```

---

### makeitem4

<!-- RAG_CHUNK: cmd_makeitem4 -->

**Signature:**
```c
*makeitem4 <item id>,<amount>,"<map name>",<X>,<Y>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<canShowEffect>};
```

---

### makeitem4

<!-- RAG_CHUNK: cmd_makeitem4 -->

**Signature:**
```c
*makeitem4 "<item name>",<amount>,"<map name>",<X>,<Y>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<canShowEffect>};
```

**Description:**
This command will create an item on the specified cell of a map. See 'makeitem' for further details.

**Example:**
```c
	ENCHANTGRADE_NONE		- No grade
	ENCHANTGRADE_D			- Grade D
	ENCHANTGRADE_C			- Grade C
	ENCHANTGRADE_B			- Grade B
	ENCHANTGRADE_A			- Grade A

```

---

### cleanarea

<!-- RAG_CHUNK: cmd_cleanarea -->

**Signature:**
```c
*cleanarea "<map name>",<x1>,<y1>,<x2>,<y2>;
```

---

### cleanmap

<!-- RAG_CHUNK: cmd_cleanmap -->

**Signature:**
```c
*cleanmap "<map name>";
```

**Description:**
These commands will clear all items lying on the ground on the specified map, either within the x1/y1-x2/y2 rectangle or across the entire map.

---

### searchitem

<!-- RAG_CHUNK: cmd_searchitem -->

**Signature:**
```c
*searchitem <array name>,"<item name>";
```

**Description:**
This command will fill the given array with the ID of items whose name matches the given one. It returns the number of items found. For performance reasons, the results array is limited to 10 items.

---

### delitem

<!-- RAG_CHUNK: cmd_delitem -->

**Signature:**
```c
*delitem <item id>,<amount>{,<account ID>};
```

---

### delitem

<!-- RAG_CHUNK: cmd_delitem -->

**Signature:**
```c
*delitem "<item name>",<amount>{,<account ID>};
```

**Description:**
This command will remove a specified amount of items from the invoking/target character. Like all the item commands, it uses the item ID found inside 'db/item_db.yml'.

**Example:**
```c
    delitem 502,10; // The person will lose 10 apples
    delitem 617,1;  // The person will lose 1 Old Violet Box

```

---

### cartdelitem

<!-- RAG_CHUNK: cmd_cartdelitem -->

**Signature:**
```c
*cartdelitem <item id>,<amount>{,<account ID>};
```

---

### cartdelitem

<!-- RAG_CHUNK: cmd_cartdelitem -->

**Signature:**
```c
*cartdelitem "<item name>",<amount>{,<account ID>};
```

---

### storagedelitem

<!-- RAG_CHUNK: cmd_storagedelitem -->

**Signature:**
```c
*storagedelitem <item id>,<amount>{,<account ID>};
```

---

### storagedelitem

<!-- RAG_CHUNK: cmd_storagedelitem -->

**Signature:**
```c
*storagedelitem "<item name>",<amount>{,<account ID>};
```

---

### guildstoragedelitem

<!-- RAG_CHUNK: cmd_guildstoragedelitem -->

**Signature:**
```c
*guildstoragedelitem <item id>,<amount>{,<account ID>};
```

---

### guildstoragedelitem

<!-- RAG_CHUNK: cmd_guildstoragedelitem -->

**Signature:**
```c
*guildstoragedelitem "<item name>",<amount>{,<account ID>};
```

**Description:**
This command behaves identically to 'delitem', but deletes items from the player's cart, storage, or guild storage.

---

### delitem2

<!-- RAG_CHUNK: cmd_delitem2 -->

**Signature:**
```c
*delitem2 <item id>,<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<account ID>};
```

---

### delitem2

<!-- RAG_CHUNK: cmd_delitem2 -->

**Signature:**
```c
*delitem2 "<item name>",<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<account ID>};
```

---

### delitem3

<!-- RAG_CHUNK: cmd_delitem3 -->

**Signature:**
```c
*delitem3 <item id>,<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account ID>};
```

---

### delitem3

<!-- RAG_CHUNK: cmd_delitem3 -->

**Signature:**
```c
*delitem3 "<item name>",<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account ID>};
```

---

### delitem4

<!-- RAG_CHUNK: cmd_delitem4 -->

**Signature:**
```c
*delitem4 <item id>,<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account ID>};
```

---

### delitem4

<!-- RAG_CHUNK: cmd_delitem4 -->

**Signature:**
```c
*delitem4 "<item name>",<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account ID>};
```

**Description:**
This command will remove a specified amount of items from the invoking/target character. See 'getitem2' for an explanation of the expanded parameters.

---

### delitemidx

<!-- RAG_CHUNK: cmd_delitemidx -->

**Signature:**
```c
*delitemidx <index>{,<amount>{,<char id>}}
```

**Description:**
This command will remove an item at the given inventory index.

**Example:**
```c
	// This will remove all Red Potions from player's inventory
	getinventorylist();
	for (.@i = 0; .@i < @inventorylist_count; ++.@i)
		if (@inventorylist_id[.@i] == 501)
			delitemidx @inventorylist_idx[.@i];

```

---

### cartdelitem2

<!-- RAG_CHUNK: cmd_cartdelitem2 -->

**Signature:**
```c
*cartdelitem2 <item id>,<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<account ID>};
```

---

### cartdelitem2

<!-- RAG_CHUNK: cmd_cartdelitem2 -->

**Signature:**
```c
*cartdelitem2 "<item name>",<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<account ID>};
```

---

### storagedelitem2

<!-- RAG_CHUNK: cmd_storagedelitem2 -->

**Signature:**
```c
*storagedelitem2 <item id>,<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<account ID>};
```

---

### storagedelitem2

<!-- RAG_CHUNK: cmd_storagedelitem2 -->

**Signature:**
```c
*storagedelitem2 "<item name>",<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<account ID>};
```

---

### guildstoragedelitem2

<!-- RAG_CHUNK: cmd_guildstoragedelitem2 -->

**Signature:**
```c
*guildstoragedelitem2 <item id>,<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<account ID>};
```

---

### guildstoragedelitem2

<!-- RAG_CHUNK: cmd_guildstoragedelitem2 -->

**Signature:**
```c
*guildstoragedelitem2 "<item name>",<amount>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<account ID>};
```

**Description:**
This command behaves identically to 'delitem2', but deletes items from the player's cart, storage, or guild storage.

---

### countitem

<!-- RAG_CHUNK: cmd_countitem -->

**Signature:**
```c
*countitem(<item id>{,<accountID>})
```

---

### countitem

<!-- RAG_CHUNK: cmd_countitem -->

**Signature:**
```c
*countitem("<item name>"{,<accountID>})
```

**Description:**
This function will return the number of items for the specified item ID that the invoking character has in the inventory.

---

### cartcountitem

<!-- RAG_CHUNK: cmd_cartcountitem -->

**Signature:**
```c
*cartcountitem(<item id>{,<accountID>})
```

---

### cartcountitem

<!-- RAG_CHUNK: cmd_cartcountitem -->

**Signature:**
```c
*cartcountitem("<item name>"{,<accountID>})
```

---

### storagecountitem

<!-- RAG_CHUNK: cmd_storagecountitem -->

**Signature:**
```c
*storagecountitem(<item id>{,<accountID>})
```

---

### storagecountitem

<!-- RAG_CHUNK: cmd_storagecountitem -->

**Signature:**
```c
*storagecountitem("<item name>"{,<accountID>})
```

---

### guildstoragecountitem

<!-- RAG_CHUNK: cmd_guildstoragecountitem -->

**Signature:**
```c
*guildstoragecountitem(<nameID>{,<accountID>})
```

---

### guildstoragecountitem

<!-- RAG_CHUNK: cmd_guildstoragecountitem -->

**Signature:**
```c
*guildstoragecountitem("<item name>"{,<accountID>})
```

**Description:**
This command behaves identically to 'countitem', but counts items from the player's cart, storage, or guild storage.

---

### countitem2

<!-- RAG_CHUNK: cmd_countitem2 -->

**Signature:**
```c
*countitem2(<item id>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<accountID>})
```

---

### countitem2

<!-- RAG_CHUNK: cmd_countitem2 -->

**Signature:**
```c
*countitem2("<item name>",<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<accountID>})
```

---

### countitem3

<!-- RAG_CHUNK: cmd_countitem3 -->

**Signature:**
```c
*countitem3(<item id>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<accountID>})
```

---

### countitem3

<!-- RAG_CHUNK: cmd_countitem3 -->

**Signature:**
```c
*countitem3("<item name>",<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<accountID>})
```

---

### countitem4

<!-- RAG_CHUNK: cmd_countitem4 -->

**Signature:**
```c
*countitem4(<item id>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<accountID>})
```

---

### countitem4

<!-- RAG_CHUNK: cmd_countitem4 -->

**Signature:**
```c
*countitem4("<item name>",<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<accountID>})
```

**Description:**
Expanded version of 'countitem' function, used for created/carded/forged items.

---

### cartcountitem2

<!-- RAG_CHUNK: cmd_cartcountitem2 -->

**Signature:**
```c
*cartcountitem2(<item id>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<accountID>})
```

---

### cartcountitem2

<!-- RAG_CHUNK: cmd_cartcountitem2 -->

**Signature:**
```c
*cartcountitem2("<item name>",<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<accountID>})
```

---

### storagecountitem2

<!-- RAG_CHUNK: cmd_storagecountitem2 -->

**Signature:**
```c
*storagecountitem2(<item id>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<accountID>})
```

---

### storagecountitem2

<!-- RAG_CHUNK: cmd_storagecountitem2 -->

**Signature:**
```c
*storagecountitem2("<item name>",<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<accountID>})
```

---

### guildstoragecountitem2

<!-- RAG_CHUNK: cmd_guildstoragecountitem2 -->

**Signature:**
```c
*guildstoragecountitem2(<nameID>,<Identified>,<Refine>,<Attribute>,<Card0>,<Card1>,<Card2>,<Card3>{,<accountID>})
```

---

### guildstoragecountitem2

<!-- RAG_CHUNK: cmd_guildstoragecountitem2 -->

**Signature:**
```c
*guildstoragecountitem2("<item name>",<Identified>,<Refine>,<Attribute>,<Card0>,<Card1>,<Card2>,<Card3>{,<accountID>})
```

**Description:**
This command behaves identically to 'countitem2', but counts items from the player's cart, storage, or guild storage.

---

### rentalcountitem

<!-- RAG_CHUNK: cmd_rentalcountitem -->

**Signature:**
```c
*rentalcountitem(<item id>{,<accountID>})
```

---

### rentalcountitem

<!-- RAG_CHUNK: cmd_rentalcountitem -->

**Signature:**
```c
*rentalcountitem("<item name>"{,<accountID>})
```

**Description:**
This function will return the number of rental items for the specified item ID that the invoking character has in the inventory.

---

### rentalcountitem2

<!-- RAG_CHUNK: cmd_rentalcountitem2 -->

**Signature:**
```c
*rentalcountitem2(<item id>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<accountID>})
```

---

### rentalcountitem2

<!-- RAG_CHUNK: cmd_rentalcountitem2 -->

**Signature:**
```c
*rentalcountitem2("<item name>",<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>{,<accountID>})
```

---

### rentalcountitem3

<!-- RAG_CHUNK: cmd_rentalcountitem3 -->

**Signature:**
```c
*rentalcountitem3(<item id>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<accountID>})
```

---

### rentalcountitem3

<!-- RAG_CHUNK: cmd_rentalcountitem3 -->

**Signature:**
```c
*rentalcountitem3("<item name>",<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<accountID>})
```

---

### rentalcountitem4

<!-- RAG_CHUNK: cmd_rentalcountitem4 -->

**Signature:**
```c
*rentalcountitem4(<item id>,<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<accountID>})
```

---

### rentalcountitem4

<!-- RAG_CHUNK: cmd_rentalcountitem4 -->

**Signature:**
```c
*rentalcountitem4("<item name>",<identify>,<refine>,<attribute>,<card1>,<card2>,<card3>,<card4>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<accountID>})
```

**Description:**
Expanded version of 'rentalcountitem' function, used for created/carded/forged items.

---

### countbound

<!-- RAG_CHUNK: cmd_countbound -->

**Signature:**
```c
*countbound({<bound type>{,<char_id>}})
```

**Description:**
This function will return the number of different bounded items in the character's inventory, and sets the arrays @bound_items[] and @bound_amount[] containing all item IDs of the counted items and their respective amount. If a bound type is specified, only those items will be counted.

**Example:**
```c
	.@total_type = countbound();
	mes "You currently have " + .@total_type + " different type of bounded items.";
	next;
	mes "The list of bounded items include:";
	for(.@i = 0; .@i < .@total_type; .@i++)
		mes "x" + @bound_amount[.@i] + " " + getitemname(@bound_items[.@i]);
	close;

```

---

### groupranditem

<!-- RAG_CHUNK: cmd_groupranditem -->

**Signature:**
```c
*groupranditem <group id>{,<sub_group>};
```

**Description:**
Returns the item_id of a random item picked from the group specified. The different groups and their group number are specified in 'db/(pre-)re/item_group_db.yml'.

---

### getrandgroupitem

<!-- RAG_CHUNK: cmd_getrandgroupitem -->

**Signature:**
```c
*getrandgroupitem <group_id>{,<quantity>{,<sub_group>{,<identify>{,<char_id>}}}};
```

**Description:**
Similar to "groupranditem", this command allows players to obtain the specified quantity of a random item from the group "<group id>". The different groups and their group number are specified in db/(pre-)re/item_group_db.yml

---

### getgroupitem

<!-- RAG_CHUNK: cmd_getgroupitem -->

**Signature:**
```c
*getgroupitem <group_id>{,<identify>{,<char_id>}};
```

**Description:**
Gives item(s) to the attached player based on item group contents. This is not working like 'getrandgroupitem' which only give 1 item for specified item group & sub_group.

---

### enable_items

<!-- RAG_CHUNK: cmd_enable_items -->

**Signature:**
```c
*enable_items;
```

---

### disable_items

<!-- RAG_CHUNK: cmd_disable_items -->

**Signature:**
```c
*disable_items;
```

**Description:**
These commands toggle the ability to change equipment while interacting with an NPC. To avoid possible exploits, the commands affect the particular script instance only. Note that if a different script also calls enable_items, it will override the last call (so you may want to call this command at the start of your script without assuming it is still in effect).

---

### itemskill

<!-- RAG_CHUNK: cmd_itemskill -->

**Signature:**
```c
*itemskill <skill id>,<skill level>{,<keep requirement>};
```

---

### itemskill

<!-- RAG_CHUNK: cmd_itemskill -->

**Signature:**
```c
*itemskill "<skill name>",<skill level>{,<keep requirement>};
```

**Description:**
This command is meant for item scripts to replicate single-use skills in usable items. It will not work properly if there is a visible dialog window or menu or if the item is not type 'Delayconsume'. If the skill is self or auto-targeting, it will be used immediately; otherwise a target cursor is shown.

**Example:**
```c
    AegisName: Anodyne
    Name: Anodyne
    Type: Delayconsume
    Buy: 2000
    Weight: 100
    Flags:
      BuyingStore: true
    Script: |
      itemskill "SM_ENDURE",1;

```

---

### consumeitem

<!-- RAG_CHUNK: cmd_consumeitem -->

**Signature:**
```c
*consumeitem <item id>{,<char_id>};
```

---

### consumeitem

<!-- RAG_CHUNK: cmd_consumeitem -->

**Signature:**
```c
*consumeitem "<item name>"{,<char_id>};
```

**Description:**
This command will run the item script of the specified item on the invoking character. The character does not need to possess the item, and the item will not be deleted. While this command is intended for usable items, it will run for any item type.

---

### produce

<!-- RAG_CHUNK: cmd_produce -->

**Signature:**
```c
*produce <item level>;
```

**Description:**
This command will open a crafting window on the client connected to the invoking character. The 'item level' is a number which determines what kind of a crafting window will pop-up.

---

### cooking

<!-- RAG_CHUNK: cmd_cooking -->

**Signature:**
```c
*cooking <dish level>;
```

**Description:**
This command will open a produce window on the client connected to the invoking character. The 'dish level' is the number which determines what kind of dish level you can produce. You can see the full list of dishes that can be produced in 'db/produce_db.txt'.

---

### makerune

<!-- RAG_CHUNK: cmd_makerune -->

**Signature:**
```c
*makerune <% success bonus>{,<char_id>};
```

**Description:**
This command will open a rune crafting window on the client connected to the invoking character. Since this command is officially used in rune ores, a bonus success rate must be specified (which adds to the base formula).

---

### successremovecards

<!-- RAG_CHUNK: cmd_successremovecards -->

**Signature:**
```c
*successremovecards <equipment slot>;
```

**Description:**
This command will remove all cards of the cards slots defined in db/item_db.yml from the item found in the specified equipment slot of the invoking character, create new card items and give them to the character. If any cards were removed in this manner, it will also show a success effect.

---

### failedremovecards

<!-- RAG_CHUNK: cmd_failedremovecards -->

**Signature:**
```c
*failedremovecards <equipment slot>,<type>;
```

**Description:**
This command will remove all cards from the item found in the specified equipment slot of the invoking character. 'type' determines what happens to the item and the cards:

---

### repair

<!-- RAG_CHUNK: cmd_repair -->

**Signature:**
```c
*repair <broken item number>{,<char_id>};
```

**Description:**
This command repairs a broken piece of equipment, using the same list of broken items as available through 'getbrokenid'.

---

### repairall

<!-- RAG_CHUNK: cmd_repairall -->

**Signature:**
```c
*repairall {<char_id>};
```

**Description:**
This command repairs all broken equipment in the attached player's inventory. A repair effect will be shown if any items are repaired, else the command will end silently.

---

### successrefitem

<!-- RAG_CHUNK: cmd_successrefitem -->

**Signature:**
```c
*successrefitem <equipment slot>{,<count>{,<char_id>}};
```

**Description:**
This command will refine an item in the specified equipment slot of the invoking character by +1, or a count if given. For a list of equipment slots see 'getequipid'. This command will also display a 'refine success' effect on the character and put appropriate messages into their chat window. It will also give the character fame points if a weapon reached +10 this way, even though these will only take effect for blacksmith who will later forge a weapon.

---

### failedrefitem

<!-- RAG_CHUNK: cmd_failedrefitem -->

**Signature:**
```c
*failedrefitem <equipment slot>{,<char_id>};
```

**Description:**
This command will fail to refine an item in the specified equipment slot of the invoking character. The item will be destroyed. This will also display a 'refine failure' effect on the character and put appropriate messages into their chat window.

---

### downrefitem

<!-- RAG_CHUNK: cmd_downrefitem -->

**Signature:**
```c
*downrefitem <equipment slot>{,<count>{,<char_id>}};
```

**Description:**
This command will downgrade an item in the specified equipment slot of the invoking character by -1, or a count if given. For a list of equipment slots see 'getequipid'. This command will also display a 'refine failure' effect on the character and put appropriate messages into their chat window.

---

### unequip

<!-- RAG_CHUNK: cmd_unequip -->

**Signature:**
```c
*unequip <equipment slot>{,<char_id>};
```

**Description:**
This command will unequip whatever is currently equipped in the invoking character's specified equipment slot. For a full list of possible equipment slots see 'getequipid'.

---

### delequip

<!-- RAG_CHUNK: cmd_delequip -->

**Signature:**
```c
*delequip <equipment slot>{,<char_id>};
```

**Description:**
This command will destroy whatever is currently equipped in the invoking character's specified equipment slot. For a full list of possible equipment slots see 'getequipid'.

---

### breakequip

<!-- RAG_CHUNK: cmd_breakequip -->

**Signature:**
```c
*breakequip <equipment slot>{,<char_id>};
```

**Description:**
This command will break and unequip whatever is currently equipped in the invoking character's specified equipment slot. For a full list of possible equipment slots see 'getequipid'.

---

### clearitem

<!-- RAG_CHUNK: cmd_clearitem -->

**Signature:**
```c
*clearitem {<char_id>};
```

**Description:**
This command will destroy all items the invoking character has in their inventory (including equipped items). It will not affect anything else, like storage or cart.

---

### equip

<!-- RAG_CHUNK: cmd_equip -->

**Signature:**
```c
*equip <item id>{,<char_id>};
```

---

### autoequip

<!-- RAG_CHUNK: cmd_autoequip -->

**Signature:**
```c
*autoequip <item id>,<option>;
```

**Description:**
These commands are to equip a equipment on the attached character. The equip function will equip the item ID given when the player has this item in his/her inventory, while the autoequip function will equip the given item ID when this is looted. The option parameter of the autoequip is 1 or 0, 1 to turn it on, and 0 to turn it off.

**Example:**
```c
	equip 1104;

```

---

### buyingstore

<!-- RAG_CHUNK: cmd_buyingstore -->

**Signature:**
```c
*buyingstore <slots>;
```

**Description:**
Invokes buying store preparation window like the skill 'Open Buying Store', without the item requirement. Amount of slots is limited by the server to a maximum of 5 slots by default.

**Example:**
```c
	// Gives the player opportunity to buy 4 different kinds of items.
	buyingstore 4;

```

---

### searchstores

<!-- RAG_CHUNK: cmd_searchstores -->

**Signature:**
```c
*searchstores <uses>,<effect>{,"<map name>"};
```

**Description:**
Invokes the store search window, which allows to search for both vending and buying stores.

**Example:**
```c
	SEARCHSTORE_EFFECT_NORMAL : Shows the store's position on the mini-map and highlights the
								shop sign with yellow color, when the store is on same map
								as the invoking player.
	SEARCHSTORE_EFFECT_REMOTE : Directly opens the shop, regardless of distance.
	
```

---

### enable_command

<!-- RAG_CHUNK: cmd_enable_command -->

**Signature:**
```c
*enable_command;
```

---

### disable_command

<!-- RAG_CHUNK: cmd_disable_command -->

**Signature:**
```c
*disable_command;
```

**Description:**
These commands toggle the ability to use atcommand while interacting with an NPC.

---

### openstorage

<!-- RAG_CHUNK: cmd_openstorage -->

**Signature:**
```c
*openstorage;
```

**Description:**
This will open character's Kafra storage window on the client connected to the invoking character. It can be used from any kind of NPC or item script, not just limited to Kafra Staff.

**Example:**
```c
    mes "Close this window to open your storage.";
    close2;
    openstorage;
    end;

```

---

### openstorage2

<!-- RAG_CHUNK: cmd_openstorage2 -->

**Signature:**
```c
*openstorage2 <storage_id>{,<mode>{,<account_id>}};
```

**Description:**
Just like the 'openstorage' command, except this command can open additional storages by the specified <storage_id>. For <storage_id>, please read the conf/inter_server.yml for storage groups.

**Example:**
```c
	STOR_MODE_NONE : Player only can read the storage entries.
	STOR_MODE_GET  : Player can get items from the storage.
	STOR_MODE_PUT  : Player can put items in the storage.
	STOR_MODE_ALL  : Player can get and put items in the storage. (default)

```

---

### openmail

<!-- RAG_CHUNK: cmd_openmail -->

**Signature:**
```c
*openmail({<char_id>});
```

**Description:**
This will open a character's Mail window on the client connected to the invoking character.

---

### mail

<!-- RAG_CHUNK: cmd_mail -->

**Signature:**
```c
*mail <destination id>,"<sender name>","<title>","<body>"{,<zeny>{,<item id array>,<item amount array>{,refine{,bound{,<item card0 array>{,<item card1 array>{,<item card2 array>{,<item card3 array>
```

**Description:**
{,<random option id0 array>, <random option value0 array>, <random option paramter0 array>{,<random option id1 array>, <random option value1 array>, <random option paramter1 array> 		{,<random option id2 array>, <random option value2 array>, <random option paramter2 array>{,<random option id3 array>, <random option value3 array>, <random option paramter3 array> 		{,<random option id4 array>, <random option value4 array>, <random option paramter4 array>}}}}}}}}};

**Example:**
```c
		{,<random option id2 array>, <random option value2 array>, <random option paramter2 array>{,<random option id3 array>, <random option value3 array>, <random option paramter3 array>
		{,<random option id4 array>, <random option value4 array>, <random option paramter4 array>}}}}}}}}};

```

---

### openauction

<!-- RAG_CHUNK: cmd_openauction -->

**Signature:**
```c
*openauction({<char_id>});
```

**Description:**
This will open the Auction window on the client connected to the invoking character.

---

### guildopenstorage

<!-- RAG_CHUNK: cmd_guildopenstorage -->

**Signature:**
```c
*guildopenstorage()
```

**Description:**
This function works the same as 'openstorage' but will open a guild storage window instead for the guild storage of the guild the invoking character belongs to.

---

### guildopenstorage_log

<!-- RAG_CHUNK: cmd_guildopenstorage_log -->

**Signature:**
```c
*guildopenstorage_log({<char id>})
```

**Description:**
Opens the guild storage log window for the attached character or the given character id.

---

### guild_has_permission

<!-- RAG_CHUNK: cmd_guild_has_permission -->

**Signature:**
```c
*guild_has_permission(<permission>{,<char id>})
```

**Description:**
Checks if the attached player or the player with the given character id has the given permission(s). Permission can be a bitmask and allows to use multiple values at the same time. Returns true if the player has all of the given permissions or false if the player does at least miss one of the given permissions or is not in a guild at all.

---

### guildchangegm

<!-- RAG_CHUNK: cmd_guildchangegm -->

**Signature:**
```c
*guildchangegm(<guild id>,<new master's name>)
```

**Description:**
This function will change the Guild Master of a guild. The ID is the guild's id, and the new guild master's name must be passed.

---

### guildgetexp

<!-- RAG_CHUNK: cmd_guildgetexp -->

**Signature:**
```c
*guildgetexp <amount>;
```

**Description:**
This will give the specified amount of guild experience points to the guild the invoking character belongs to. It will silently fail if they do not belong to any guild.

---

### guildskill

<!-- RAG_CHUNK: cmd_guildskill -->

**Signature:**
```c
*guildskill <skill id>,<level>
```

---

### guildskill

<!-- RAG_CHUNK: cmd_guildskill -->

**Signature:**
```c
*guildskill "<skill name>",<level>
```

**Description:**
This command will bump up the specified guild skill by the specified number of levels. This refers to the invoking character and will only work if the invoking character is a member of a guild AND its guild master, otherwise no failure message will be given and no error will occur, but nothing will happen - same about the guild skill trying to exceed the possible maximum. The full list of guild skills is available in 'db/(pre-)re/skill_db.yml', these are all the GD_ skills at the end.

---

### resetlvl

<!-- RAG_CHUNK: cmd_resetlvl -->

**Signature:**
```c
*resetlvl <action type>{,<char_id>};
```

**Description:**
This is a character reset command, meant mostly for rebirth script supporting Advanced jobs, which will reset the invoking character's stats and level depending on the action type given. Valid action types are:

**Example:**
```c
     status effects (only the ones settable by 'setoption'), sets all stats to 1.
     If the new job is 'Novice High', give 100 status points, give First Aid and
     Play Dead skills.
```

---

### resetstatus

<!-- RAG_CHUNK: cmd_resetstatus -->

**Signature:**
```c
*resetstatus({<char_id>});
```

**Description:**
This is a character reset command, which will reset the stats on the invoking character and give back all the stat points used to raise them previously. Nothing will happen to any other numbers about the character.

---

### resetskill

<!-- RAG_CHUNK: cmd_resetskill -->

**Signature:**
```c
*resetskill({<char_id>});
```

**Description:**
This command takes off all the skill points on the invoking character, so they only have Basic Skill blanked out (lvl 0) left, and returns the points for them to spend again. Nothing else will change but the skills. Quest skills will also reset if 'quest_skill_reset' option is set to Yes in 'battle_athena.conf'. If the 'quest_skill_learn' option is set in there, the points in the quest skills will also count towards the total.

---

### resetfeel

<!-- RAG_CHUNK: cmd_resetfeel -->

**Signature:**
```c
*resetfeel({<char_id>});
```

**Description:**
This command will reset the Star Gladiator's designated maps on the invoking character. Only works on Star Gladiator and Star Emperor classes.

---

### resethate

<!-- RAG_CHUNK: cmd_resethate -->

**Signature:**
```c
*resethate({<char_id>});
```

**Description:**
This command will reset the Star Gladiator's designated monsters on the invoking character. Only works on Star Gladiator and Star Emperor classes.

---

### sc_start

<!-- RAG_CHUNK: cmd_sc_start -->

**Signature:**
```c
*sc_start <effect type>,<ticks>,<value 1>{,<rate>,<flag>{,<GID>}};
```

---

### sc_start2

<!-- RAG_CHUNK: cmd_sc_start2 -->

**Signature:**
```c
*sc_start2 <effect type>,<ticks>,<value 1>,<value 2>{,<rate>,<flag>{,<GID>}};
```

---

### sc_start4

<!-- RAG_CHUNK: cmd_sc_start4 -->

**Signature:**
```c
*sc_start4 <effect type>,<ticks>,<value 1>,<value 2>,<value 3>,<value 4>{,<rate>,<flag>{,<GID>}};
```

---

### sc_end

<!-- RAG_CHUNK: cmd_sc_end -->

**Signature:**
```c
*sc_end <effect type>{,<GID>};
```

---

### sc_end_class

<!-- RAG_CHUNK: cmd_sc_end_class -->

**Signature:**
```c
*sc_end_class {<char_id>{,<job_id>}};
```

**Description:**
These commands will bestow a status effect on a character.

**Example:**
```c
	// This will poison the invoking character for 10 minutes at 50% chance.
	sc_start SC_POISON,600000,0,5000;

	// This will bestow the effect of Level 10 Blessing.
	sc_start SC_BLESSING,240000,10;

	// Adjust element resistance by percentage. Sample with Resist_Fire item script:
	// val1: Water resistance
	// val2: Earth resistance
	// val3: Fire resistance
	// val4: Wind resistance
	sc_start4 SC_ARMOR_ELEMENT,1200000,-15,0,20,0;

	// This will end the Freezing status for the invoking character.
	sc_end SC_FREEZE;
```

---

### getstatus

<!-- RAG_CHUNK: cmd_getstatus -->

**Signature:**
```c
*getstatus(<effect type>{,<type>{,<char_id>}})
```

**Description:**
Retrieve information about a specific status effect when called. Depending on <type> specified the function will return different information.

---

### skilleffect

<!-- RAG_CHUNK: cmd_skilleffect -->

**Signature:**
```c
*skilleffect <skill id>,<number>{,<game ID>};
```

---

### skilleffect

<!-- RAG_CHUNK: cmd_skilleffect -->

**Signature:**
```c
*skilleffect "<skill name>",<number>{,<game ID>};
```

**Description:**
This command displays visual and aural effects of given skill on currently attached character or, when defined, on any unit with the given ID. The number parameter is for skill whose visual effect involves displaying of a number (healing or damaging). Note, that this command will not actually use the skill, it is intended for scripts, which simulate skill usage by the NPC, such as buffs, by setting appropriate status and displaying the skill's effect.

---

### npcskilleffect

<!-- RAG_CHUNK: cmd_npcskilleffect -->

**Signature:**
```c
*npcskilleffect <skill id>,<number>,<x>,<y>;
```

---

### npcskilleffect

<!-- RAG_CHUNK: cmd_npcskilleffect -->

**Signature:**
```c
*npcskilleffect "<skill name>",<number>,<x>,<y>;
```

**Description:**
This command behaves identically to 'skilleffect', however, ground type skill effects will be centered at the map coordinates given on the same map as the attached character and all other skill types will be centered on the attached character.

---

### specialeffect

<!-- RAG_CHUNK: cmd_specialeffect -->

**Signature:**
```c
*specialeffect <effect number>{,<send_target>{,"<NPC Name>"}};
```

**Description:**
This command will display special effect with the given number, centered on the specified NPCs coordinates, if any. For a full list of special effect numbers known see 'doc/effect_list.txt'. Some effect numbers are known not to work in some client releases. (Notably, rain is absent from any client executables released after April 2005.)

---

### specialeffect2

<!-- RAG_CHUNK: cmd_specialeffect2 -->

**Signature:**
```c
*specialeffect2 <effect number>{,<send_target>{,"<Player Name>"}};
```

**Description:**
This command behaves identically to 'specialeffect', but the effect will be centered on the invoking character's sprite.

---

### removespecialeffect

<!-- RAG_CHUNK: cmd_removespecialeffect -->

**Signature:**
```c
*removespecialeffect <effect number>{,<send_target>{,"<NPC Name>"}};
```

**Description:**
Work for 2018-10-02+ This command behaves parameter same as 'specialeffect', but use for remove effect with <effect number> from invoking NPC.

---

### removespecialeffect2

<!-- RAG_CHUNK: cmd_removespecialeffect2 -->

**Signature:**
```c
*removespecialeffect2 <effect number>{,<send_target>{,"<Player Name>"}};
```

**Description:**
Work for 2018-10-02+ This command behaves parameter same as 'specialeffect2', but use for remove effect with <effect number> from invoking character.

---

### statusup

<!-- RAG_CHUNK: cmd_statusup -->

**Signature:**
```c
*statusup <stat>{,<char_id>};
```

**Description:**
This command will change a specified stat of the invoking character up by one permanently. Stats are to be given as number, but you can use these constants to replace them:

---

### statusup2

<!-- RAG_CHUNK: cmd_statusup2 -->

**Signature:**
```c
*statusup2 <stat>,<amount>{,<char_id>};
```

**Description:**
This command will change a specified stat of the invoking character by the specified amount permanently. The amount can be negative. See 'statusup'.

---

### traitstatusup

<!-- RAG_CHUNK: cmd_traitstatusup -->

**Signature:**
```c
*traitstatusup <stat>{,<char_id>};
```

**Description:**
This command will change a specified trait stat of the invoking character up by one permanently. Trait stats are to be given as number, but you can use these constants to replace them:

---

### traitstatusup2

<!-- RAG_CHUNK: cmd_traitstatusup2 -->

**Signature:**
```c
*traitstatusup2 <stat>,<amount>{,<char_id>};
```

**Description:**
This command will change a specified trait stat of the invoking character by the specified amount permanently. The amount can be negative. See 'statusup'.

---

### bonus

<!-- RAG_CHUNK: cmd_bonus -->

**Signature:**
```c
*bonus <bonus type>,<val1>;
```

---

### bonus2

<!-- RAG_CHUNK: cmd_bonus2 -->

**Signature:**
```c
*bonus2 <bonus type>,<val1>,<val2>;
```

---

### bonus3

<!-- RAG_CHUNK: cmd_bonus3 -->

**Signature:**
```c
*bonus3 <bonus type>,<val1>,<val2>,<val3>;
```

---

### bonus4

<!-- RAG_CHUNK: cmd_bonus4 -->

**Signature:**
```c
*bonus4 <bonus type>,<val1>,<val2>,<val3>,<val4>;
```

---

### bonus5

<!-- RAG_CHUNK: cmd_bonus5 -->

**Signature:**
```c
*bonus5 <bonus type>,<val1>,<val2>,<val3>,<val4>,<val5>;
```

**Description:**
These commands are meant to be used in item scripts. They will probably work outside item scripts, but the bonus will not persist for long. They, as expected, refer only to an invoking character.

---

### autobonus

<!-- RAG_CHUNK: cmd_autobonus -->

**Signature:**
```c
*autobonus <bonus script>,<rate>,<duration>{,<flag>,{<other script>}};
```

---

### autobonus2

<!-- RAG_CHUNK: cmd_autobonus2 -->

**Signature:**
```c
*autobonus2 <bonus script>,<rate>,<duration>{,<flag>,{<other script>}};
```

---

### autobonus3

<!-- RAG_CHUNK: cmd_autobonus3 -->

**Signature:**
```c
*autobonus3 <bonus script>,<rate>,<duration>,<skill id>,{<other script>};
```

---

### autobonus3

<!-- RAG_CHUNK: cmd_autobonus3 -->

**Signature:**
```c
*autobonus3 <bonus script>,<rate>,<duration>,"<skill name>",{<other script>};
```

**Description:**
These commands are meant to be used in item scripts only! See 'petautobonus' for pet usage.

---

### bonus_script

<!-- RAG_CHUNK: cmd_bonus_script -->

**Signature:**
```c
*bonus_script "<script code>",<duration>{,<flag>{,<type>{,<status_icon>{,<char_id>}}}};
```

**Description:**
This command will attach a script to a player for a given duration, in seconds. After that time, the script will automatically expire. The same bonus cannot be stacked. By default, this bonus will be stored on `bonus_script` table when player logs out.

**Example:**
```c
	1   : Remove when dead.
	2   : Removable by Dispell.
	4   : Removable by Clearance.
	8   : Remove when player logs out.
	16  : Removeable by Banishing Buster.
	32  : Removable by Refresh.
	64  : Removable by Lux Anima.
	128 : Remove when Madogear is activated or deactivated.
	256 : Remove when receive damage.
	512 : Script is permanent, cannot be cleared by bonus_script_clear.
	1024: Force to replace duplicated script by expanding the duration.
	2048: Force to add duplicated script. This flag cannot be stacked with 1024,
	      if both are defined, 1024 will be checked first and ignore this flag.

```

---

### bonus_script_clear

<!-- RAG_CHUNK: cmd_bonus_script_clear -->

**Signature:**
```c
*bonus_script_clear {<flag>,{<char_id>}};
```

**Description:**
Removes attached bonus_script from player. If no 'char_id' given, it will removes from the invoker.

---

### plagiarizeskill

<!-- RAG_CHUNK: cmd_plagiarizeskill -->

**Signature:**
```c
*plagiarizeskill <skill_id>,<level>;
```

**Description:**
Enable the player to plagiarize specific skills that are copyable. Return 1 on success, 0 otherwise.

---

### plagiarizeskillreset

<!-- RAG_CHUNK: cmd_plagiarizeskillreset -->

**Signature:**
```c
*plagiarizeskillreset <flag>;
```

**Description:**
Remove a plagiarized skill from the player. Return 1 on success, 0 otherwise.

---

### skill

<!-- RAG_CHUNK: cmd_skill -->

**Signature:**
```c
*skill <skill id>,<level>{,<flag>};
```

---

### skill

<!-- RAG_CHUNK: cmd_skill -->

**Signature:**
```c
*skill "<skill name>",<level>{,<flag>};
```

---

### addtoskill

<!-- RAG_CHUNK: cmd_addtoskill -->

**Signature:**
```c
*addtoskill <skill id>,<level>{,<flag>};
```

---

### addtoskill

<!-- RAG_CHUNK: cmd_addtoskill -->

**Signature:**
```c
*addtoskill "<skill name>",<level>{,<flag>};
```

**Description:**
These commands will give the invoking character a specified skill. This is also used for item scripts.

**Example:**
```c
	0 - SKILL_PERM
	1 - SKILL_TEMP
	2 - SKILL_TEMPLEVEL
	3 - SKILL_PERM_GRANT

```

---

### nude

<!-- RAG_CHUNK: cmd_nude -->

**Signature:**
```c
*nude {<char_id>};
```

**Description:**
This command will unequip anything equipped on the invoking character.

---

### sit

<!-- RAG_CHUNK: cmd_sit -->

**Signature:**
```c
*sit {"<character name>"};
```

---

### stand

<!-- RAG_CHUNK: cmd_stand -->

**Signature:**
```c
*stand {"<character name>"};
```

**Description:**
These commands will make a character sit or stand. If no character is specified, the command will run for the invoking character.

---

### disguise

<!-- RAG_CHUNK: cmd_disguise -->

**Signature:**
```c
*disguise <Monster ID>{,<char_id>};
```

---

### undisguise

<!-- RAG_CHUNK: cmd_undisguise -->

**Signature:**
```c
*undisguise {<char_id>};
```

**Description:**
This command disguises the current player with a monster sprite. The disguise lasts until 'undisguise' is issued or the player logs out.

---

### transform

<!-- RAG_CHUNK: cmd_transform -->

**Signature:**
```c
*transform <monster ID>,<duration>{,<sc type>,<val1>,<val2>,<val3>,<val4>};
```

---

### transform

<!-- RAG_CHUNK: cmd_transform -->

**Signature:**
```c
*transform "<monster name>",<duration>{,<sc type>,<val1>,<val2>,<val3>,<val4>};
```

---

### active_transform

<!-- RAG_CHUNK: cmd_active_transform -->

**Signature:**
```c
*active_transform <monster ID>,<duration>{,<sc type>,<val1>,<val2>,<val3>,<val4>};
```

---

### active_transform

<!-- RAG_CHUNK: cmd_active_transform -->

**Signature:**
```c
*active_transform "<monster name>",<duration>{,<sc type>,<val1>,<val2>,<val3>,<val4>};
```

**Description:**
This command will turn a player into a monster for a given duration and can grant a SC attribute effect while transformed. Note that players cannot be transformed during War of Emperium or if already disguised. Can only be removed when you die or the duration ends.

---

### marriage

<!-- RAG_CHUNK: cmd_marriage -->

**Signature:**
```c
*marriage("<spouse name>");
```

**Description:**
This function will marry two characters, the invoking character and the one referred to by name given, together, setting them up as each other's marriage partner. No second function call has to be issued (in current SVN at least) to make sure the marriage works both ways. The function returns 1 upon success, or 0 if the marriage could not be completed, either because the other character wasn't found or because one of the two characters is already married.

---

### wedding

<!-- RAG_CHUNK: cmd_wedding -->

**Signature:**
```c
*wedding;
```

**Description:**
This command will call up wedding effects - the music and confetti - centered on the invoking character. Example can be found in the wedding script.

---

### divorce

<!-- RAG_CHUNK: cmd_divorce -->

**Signature:**
```c
*divorce({<char_id>})
```

**Description:**
This function will "un-marry" the invoking character from whoever they were married to. Both will no longer be each other's marriage partner, (at least in current SVN, which prevents the cases of multi-spouse problems). It will return 1 upon success or 0 if the character was not married at all.

---

### adopt

<!-- RAG_CHUNK: cmd_adopt -->

**Signature:**
```c
*adopt("<parent_name>","<baby_name>");
```

---

### adopt

<!-- RAG_CHUNK: cmd_adopt -->

**Signature:**
```c
*adopt(<parent_id>,<baby_id>);
```

**Description:**
This function will send the client adoption request to the specified baby character. The parent value can be either parent. Both parents and the baby need to be online in order for adoption to work.

---

### pcfollow

<!-- RAG_CHUNK: cmd_pcfollow -->

**Signature:**
```c
*pcfollow <id>,<target id>;
```

---

### pcstopfollow

<!-- RAG_CHUNK: cmd_pcstopfollow -->

**Signature:**
```c
*pcstopfollow <id>;
```

**Description:**
Makes a character follow or stop following someone. This command does the same as the @follow command. The main difference is that @follow can use character names, and this commands needs the account ID for the target.

**Example:**
```c
	// This will make Aaron follow Bullah, when both of these characters are online.
	pcfollow getCharID(3,"Aaron"),getCharID(3,"Bullah");

	// Makes Aaron stop following whoever he is following.
	pcstopfollow getCharID(3,"Aaron");

```

---

### pcblockmove

<!-- RAG_CHUNK: cmd_pcblockmove -->

**Signature:**
```c
*pcblockmove <id>,<option>;
```

---

### unitblockmove

<!-- RAG_CHUNK: cmd_unitblockmove -->

**Signature:**
```c
*unitblockmove <id>,<option>;
```

**Description:**
Prevents the given GID from moving when the option is 1, and enables the ID to move again when the option is 0. This command will run for the attached unit if the given GID is zero.

**Example:**
```c
	// Prevents the current char from moving away.
	pcblockmove getcharid(3),1;

	// Enables the current char to move again.
	pcblockmove getcharid(3),0;

```

---

### pcblockskill

<!-- RAG_CHUNK: cmd_pcblockskill -->

**Signature:**
```c
*pcblockskill <id>,<option>;
```

---

### unitblockskill

<!-- RAG_CHUNK: cmd_unitblockskill -->

**Signature:**
```c
*unitblockskill <id>,<option>;
```

**Description:**
Prevents the given GID from casting skills when the option is 1, and enables the ID to cast skills again when the option is 0. This command will run for the attached unit if the given GID is zero.

**Example:**
```c
	// Prevents the current char from casting skills.
	pcblockskill getcharid(3),1;

	// Enables the current char to cast skills again.
	pcblockskill getcharid(3),0;

```

---

### setpcblock

<!-- RAG_CHUNK: cmd_setpcblock -->

**Signature:**
```c
*setpcblock <type>,<state>{,<account ID>};
```

---

### getpcblock

<!-- RAG_CHUNK: cmd_getpcblock -->

**Signature:**
```c
*getpcblock {<account ID>};
```

**Description:**
'setpcblock' command prevents/allows the player from doing the given <type> of action according to the <state> during the player session (note: @reloadscript removes all <type> except PCBLOCK_IMMUNE). The <type> values are bit-masks, multiples of <type> can be added to change the player action.

**Example:**
```c
	PCBLOCK_MOVE				Prevent the player from moving.
	PCBLOCK_ATTACK				Prevent the player from attacking.
	PCBLOCK_SKILL				Prevent the player from using skills/itemskills.
	PCBLOCK_USEITEM				Prevent the player from using usable items.
	PCBLOCK_CHAT				Prevent the player from sending global/guild/party/whisper messages.
	PCBLOCK_IMMUNE				Prevent the player from being hit by monsters.
	PCBLOCK_SITSTAND			Prevent the player from sitting/standing.
	PCBLOCK_COMMANDS			Prevent the player from using atcommands/charcommands.
	PCBLOCK_NPCCLICK			Prevent the player from clicking/touching any NPC/shop/warp.
	PCBLOCK_EMOTION				Prevent the player from using emotions.
	PCBLOCK_EQUIP				Prevent the player from replacing equipment.
	PCBLOCK_NPC				Simulate NPC interaction. Useful for NPC with no mes window. Sum of PCBLOCK_MOVE|PCBLOCK_SKILL|PCBLOCK_USEITEM|PCBLOCK_COMMANDS|PCBLOCK_NPCCLICK|PCBLOCK_EQUIP.
	PCBLOCK_ALL				Sum of all the flags.

```

---

### macro_detector

<!-- RAG_CHUNK: cmd_macro_detector -->

**Signature:**
```c
*macro_detector({<account ID>});
```

---

### macro_detector

<!-- RAG_CHUNK: cmd_macro_detector -->

**Signature:**
```c
*macro_detector({"<character name>"});
```

**Description:**
This command will display the captcha UI challenge onto the invoking character or the given <account ID>/<character name>.

**Example:**
```c
	// Use 'getareaunits' to gather an area of players to test.
	// Build an int array of the account IDs.
	.@num = getareaunits(BL_PC, "prontera", 150, 150, 160, 160, .@array[0]);

	mes "The number of Players in Prontera in between 150x150 and 160x160 is " + .@num + " .";
	mes "Players to challenge:";
	freeloop(1); // If the list is too big
	for(.@i = 0; .@i < getarraysize(.@array); .@i++) {
		mes (.@i + 1) + " " + convertpcinfo(.@array[.@i], CPC_NAME);
		macro_detector .@array[.@i];
	}
	freeloop(0);
	end;

```

---

### permission_check

<!-- RAG_CHUNK: cmd_permission_check -->

**Signature:**
```c
*permission_check(<permission>{,<char_id>});
```

**Description:**
This command will return true if the attached character has the specified permission, false otherwise. If <char_id> is given, it will check the permission for that character instead.

**Example:**
```c
	if (permission_check(PC_PERM_TRADE)) {
		mes "You have permission to trade!";
	}
	else {
		mes "You do not have permission to trade!";
	}
	end;

```

---

### permission_add

<!-- RAG_CHUNK: cmd_permission_add -->

**Signature:**
```c
*permission_add(<permission>{,<char_id>});
```

---

### permission_remove

<!-- RAG_CHUNK: cmd_permission_remove -->

**Signature:**
```c
*permission_remove(<permission>{,<char_id>});
```

**Description:**
These commands will temporarily add or remove the specified permission to the attached character, or the given <char_id> until the player logs out.

**Example:**
```c
	// Adds the 'can_trade' permission to the attached character,
	// allowing them to trade, drop, sell, store and mail items.
	permission_add(PC_PERM_TRADE);

	// Removes the 'can_party' permission from the attached character,
	// preventing them from joining or creating parties.
	permission_remove(PC_PERM_PARTY);

```

---

### monster

<!-- RAG_CHUNK: cmd_monster -->

**Signature:**
```c
*monster     "<map name>",<x>,<y>,"<name to show>",<mob id>,<amount>{,"<event label>",<size>,<ai>};
```

---

### monster

<!-- RAG_CHUNK: cmd_monster -->

**Signature:**
```c
*monster     "<map name>",<x>,<y>,"<name to show>","<mob name>",<amount>{,"<event label>",<size>,<ai>};
```

---

### areamonster

<!-- RAG_CHUNK: cmd_areamonster -->

**Signature:**
```c
*areamonster "<map name>",<x1>,<y1>,<x2>,<y2>,"<name to show>",<mob id>,<amount>{,"<event label>",<size>,<ai>};
```

---

### areamonster

<!-- RAG_CHUNK: cmd_areamonster -->

**Signature:**
```c
*areamonster "<map name>",<x1>,<y1>,<x2>,<y2>,"<name to show>","<mob name>",<amount>{,"<event label>",<size>,<ai>};
```

**Description:**
This command will spawn <amount> monsters with <mob id> or <mob name> on the specified coordinates on the specified map. If the script is invoked by a character, a special <map name>, "this", will be recognized to mean the name of the map the invoking character is located at. This command works fine in item scripts.

**Example:**
```c
	Size_Small	(0)		(default)
	Size_Medium	(1)
	Size_Large	(2)

```

---

### areamobuseskill

<!-- RAG_CHUNK: cmd_areamobuseskill -->

**Signature:**
```c
*areamobuseskill "<map name>",<x>,<y>,<range>,<mob id>,<skill id>,<skill level>,<cast time>,<cancelable>,<emotion>,<target type>;
```

---

### areamobuseskill

<!-- RAG_CHUNK: cmd_areamobuseskill -->

**Signature:**
```c
*areamobuseskill "<map name>",<x>,<y>,<range>,<mob id>,"<skill name>",<skill level>,<cast time>,<cancelable>,<emotion>,<target type>;
```

---

### areamobuseskill

<!-- RAG_CHUNK: cmd_areamobuseskill -->

**Signature:**
```c
*areamobuseskill "<map name>",<x>,<y>,<range>,"<mob name>",<skill id>,<skill level>,<cast time>,<cancelable>,<emotion>,<target type>;
```

---

### areamobuseskill

<!-- RAG_CHUNK: cmd_areamobuseskill -->

**Signature:**
```c
*areamobuseskill "<map name>",<x>,<y>,<range>,"<mob name>","<skill name>",<skill level>,<cast time>,<cancelable>,<emotion>,<target type>;
```

**Description:**
This command will make all monsters of the specified <mob id> or <mob name> in the specified area use the specified skill. <map name>, <x>, and <y> define the center of the area, which extending <range> cells in each direction (ex: a range of 3 would create a 7x7 square). The skill can be specified by <skill id> or <skill name>. <cast time> is in milliseconds (1000 = 1 second), and the rest should be self-explanatory.

**Example:**
```c
	0 = self
	1 = the mob's current target
	2 = the mob's master
	3 = random target

```

---

### killmonster

<!-- RAG_CHUNK: cmd_killmonster -->

**Signature:**
```c
*killmonster "<map name>","<event label>"{,<type>};
```

**Description:**
This command will kill all monsters that were spawned with 'monster' or 'addmonster' and have a specified event label attached to them. Commonly used to get rid of remaining quest monsters once the quest is complete.

---

### killmonsterall

<!-- RAG_CHUNK: cmd_killmonsterall -->

**Signature:**
```c
*killmonsterall "<map name>"{,<type>};
```

**Description:**
This command will kill all monsters on a specified map name, regardless of how they were spawned or what they are. As of r12873, The behavior has changed slightly. In light of a label behavior fix for mob spawning commands that will now allow the label to trigger when there is no player, killmonsterall has also been modified to support this.

---

### mobcount

<!-- RAG_CHUNK: cmd_mobcount -->

**Signature:**
```c
*mobcount("<map name>","<event label>")
```

**Description:**
This function will count all the monsters on the specified map that have a given event label and return the number or 0 if it can't find any. Naturally, only monsters spawned with 'monster' and 'areamonster' script commands can have non-empty event label. If you pass this function an empty string for the event label, it will return the total count of monster without event label, including permanently spawning monsters. With the dynamic mobs system enabled, where mobs are not kept in memory for maps with no actual people playing on them, this will return a 0 for any such map. If the event label is given as "all", all monsters will be counted, regardless of having any event label attached.

---

### clone

<!-- RAG_CHUNK: cmd_clone -->

**Signature:**
```c
*clone "<map name>",<x>,<y>,"<event>",<char id>{,<master_id>{,<mode>{,<flag>,<duration>}}}
```

**Description:**
This command creates a monster which is a copy of another player. The first four arguments serve the same purpose as in the monster script command, The <char id> is the character id of the player to clone (player must be online). If <master id> is given, the clone will be a 'slave/minion' of it. Master_id must be a character id of another online player.

---

### summon

<!-- RAG_CHUNK: cmd_summon -->

**Signature:**
```c
*summon "monster name",<monster id>{,<Time Out>{,"event label"}};
```

**Description:**
This command will summon a monster. (see also 'monster') Unlike monsters spawned with other commands, this one will set up the monster to fight to protect the invoking character. Monster name and mob id obey the same rules as the one given at the beginning of this document for permanent monster spawns with the exceptions mentioned when describing 'monster' command.

---

### addmonsterdrop

<!-- RAG_CHUNK: cmd_addmonsterdrop -->

**Signature:**
```c
*addmonsterdrop <monster id>,<item id>,<rate>,{<steal protected>,{<random option group id>}};
```

---

### addmonsterdrop

<!-- RAG_CHUNK: cmd_addmonsterdrop -->

**Signature:**
```c
*addmonsterdrop "<monster name>",<item id>,<rate>,{<steal protected>,{<random option group id>}};
```

---

### delmonsterdrop

<!-- RAG_CHUNK: cmd_delmonsterdrop -->

**Signature:**
```c
*delmonsterdrop <monster id>,<item id>;
```

---

### delmonsterdrop

<!-- RAG_CHUNK: cmd_delmonsterdrop -->

**Signature:**
```c
*delmonsterdrop "<monster name>",<item id>;
```

**Description:**
These commands will temporarily add or delete a monster drop, which will be reset when the mob database reloads or the server shuts down. They return true upon success, false otherwise.

**Example:**
```c
	// Makes Owl Baron drop Honey at an 80% rate.
	addmonsterdrop 1295,518,8000;

	// Makes Owl Baron drop Knife_ at an 80% rate, protected from TF_STEAL and with random option group Id 5.
	addmonsterdrop 1295,1202,8000,true,5;

	// Deletes Executioner's Mitten from Rybio.
	delmonsterdrop 1201,7017;

```

---

### mob_setidleevent

<!-- RAG_CHUNK: cmd_mob_setidleevent -->

**Signature:**
```c
*mob_setidleevent <GID>,<event>;
```

**Description:**
This command will attach an event label to the monster with the given <GID> which will execute when the <GID> is idle.

**Example:**
```c
	monster "prontera",0,0,"Quest Poring",1002,1;
	mob_setidleevent $@mobid[0], "NPC NAME::OnIdle";
	end;

```

---

### disablenpc

<!-- RAG_CHUNK: cmd_disablenpc -->

**Signature:**
```c
*disablenpc {"<NPC object name>"};
```

---

### enablenpc

<!-- RAG_CHUNK: cmd_enablenpc -->

**Signature:**
```c
*enablenpc {"<NPC object name>"};
```

**Description:**
These two commands will disable and enable, respectively, an NPC object specified by name. The disabled NPC will disappear from sight and will no longer be triggerable in the normal way. It is not clear whether it will still be accessible through 'donpcevent' and other triggering commands, but it probably will be. You can disable even warp NPCs if you know their object names, which is an easy way to make a map only accessible through walking half the time. Then you 'enablenpc' them back.

---

### hideonnpc

<!-- RAG_CHUNK: cmd_hideonnpc -->

**Signature:**
```c
*hideonnpc {"<NPC object name>"};
```

---

### hideoffnpc

<!-- RAG_CHUNK: cmd_hideoffnpc -->

**Signature:**
```c
*hideoffnpc {"<NPC object name>"};
```

**Description:**
These commands will make the NPC object specified display as hidden/visible, even though not actually disabled per se. Hidden as in thief Hide skill, but unfortunately, not detectable by Ruwach or Sight.

---

### unloadnpc

<!-- RAG_CHUNK: cmd_unloadnpc -->

**Signature:**
```c
*unloadnpc "<NPC object name>";
```

**Description:**
This command will fully unload a NPC object and all of it's duplicates.

---

### duplicate

<!-- RAG_CHUNK: cmd_duplicate -->

**Signature:**
```c
*duplicate "<NPC name>","<map>",<x>,<y>{,"<Duplicate NPC name>"{,<sprite>{,<dir>{,<xs>{,<xy>}}}}};
```

**Description:**
This command will duplicate the NPC with the given <NPC name> on <map> at <x>/<y>. If <Duplicate NPC name>, <sprite>, <dir>, <xs> or <ys> is not provided the value of the original NPC will be used. The Unique name of the new duplicated NPC is returned on success. An empty string is returned on failure.

---

### duplicate_dynamic

<!-- RAG_CHUNK: cmd_duplicate_dynamic -->

**Signature:**
```c
*duplicate_dynamic("<NPC name>"{,<character ID>});
```

**Description:**
This command will duplicate the NPC with the given <NPC name> near the attached player or the player with the given <character ID>. The Unique name of the new duplicated NPC is returned on success. An empty string is returned on failure.

---

### cloakonnpc

<!-- RAG_CHUNK: cmd_cloakonnpc -->

**Signature:**
```c
*cloakonnpc {"<NPC object name>"{,<character ID>}};
```

---

### cloakoffnpc

<!-- RAG_CHUNK: cmd_cloakoffnpc -->

**Signature:**
```c
*cloakoffnpc {"<NPC object name>"{,<character ID>}};
```

**Description:**
These commands will make the NPC object specified display as cloaked/uncloaked, even though not actually disabled. The player can interact with a NPC cloaked (via NPC click, monster event..) but the NPC trigger area is disabled.

---

### cloakonnpcself

<!-- RAG_CHUNK: cmd_cloakonnpcself -->

**Signature:**
```c
*cloakonnpcself {"<NPC object name>"};
```

---

### cloakoffnpcself

<!-- RAG_CHUNK: cmd_cloakoffnpcself -->

**Signature:**
```c
*cloakoffnpcself {"<NPC object name>"};
```

**Description:**
Same command as above, but an attached player is required. The NPC will only display to the attached player.

---

### isnpccloaked

<!-- RAG_CHUNK: cmd_isnpccloaked -->

**Signature:**
```c
*isnpccloaked {"<NPC object name>"{,<character ID>}};
```

**Description:**
Returns true if the NPC has been cloaked to the attached player or given <character ID>, false otherwise. This works in association with cloakonnpc when it is targetting a specific character.

---

### doevent

<!-- RAG_CHUNK: cmd_doevent -->

**Signature:**
```c
*doevent "<NPC object name>::<event label>";
```

**Description:**
This command will start a new execution thread in a specified NPC object at the specified label. The execution of the script running this command will not stop, and the event called by the 'doevent' command will not run until the invoking script has terminated. No parameters may be passed with a doevent call.

---

### donpcevent

<!-- RAG_CHUNK: cmd_donpcevent -->

**Signature:**
```c
*donpcevent "<NPC object name>::<event label>";
```

**Description:**
This command invokes the event label code within an another NPC or NPCs. It starts a separate instance of execution, and the invoking NPC will resume execution its immediately.

---

### cmdothernpc

<!-- RAG_CHUNK: cmd_cmdothernpc -->

**Signature:**
```c
*cmdothernpc "<npc name>","<command>";
```

**Description:**
This is simply "donpcevent <npc name>::OnCommand<command>". It is an approximation of official server script language's 'cmdothernpc'.

---

### npctalk

<!-- RAG_CHUNK: cmd_npctalk -->

**Signature:**
```c
*npctalk "<message>"{,"<NPC name>",<flag>{,<color>}};
```

**Description:**
This command will display a message as if the NPC object running it was a player talking - that is, above their head and in the chat window. The display name of the NPC won't get appended in front of the message. If the <NPC name> option is given and not empty, then that NPC will display the message, else the attached NPC will display the message, the color format is in RGB (0xRRGGBB). The color is White by default.

---

### chatmes

<!-- RAG_CHUNK: cmd_chatmes -->

**Signature:**
```c
*chatmes "<message>"{,"<NPC name>"};
```

**Description:**
This command will display a message in the waitingroom (chat) of the NPC. If the <NPC name> option is given, then that NPC will display the message, else the attached NPC will display the message. If the NPC is not in a waitingroom, nothing happens.

---

### setnpcdisplay

<!-- RAG_CHUNK: cmd_setnpcdisplay -->

**Signature:**
```c
*setnpcdisplay("<npc name>", "<display name>", <class id>, <size>)
```

---

### setnpcdisplay

<!-- RAG_CHUNK: cmd_setnpcdisplay -->

**Signature:**
```c
*setnpcdisplay("<npc name>", "<display name>", <class id>)
```

---

### setnpcdisplay

<!-- RAG_CHUNK: cmd_setnpcdisplay -->

**Signature:**
```c
*setnpcdisplay("<npc name>", "<display name>")
```

---

### setnpcdisplay

<!-- RAG_CHUNK: cmd_setnpcdisplay -->

**Signature:**
```c
*setnpcdisplay("<npc name>", <class id>)
```

**Description:**
Changes the display name and/or display class of the target NPC. Returns 0 is successful, 1 if the NPC does not exist. Size is 0 = normal 1 = small 2 = big.

---

### addtimer

<!-- RAG_CHUNK: cmd_addtimer -->

**Signature:**
```c
*addtimer <ticks>,"NPC::OnLabel";
```

---

### deltimer

<!-- RAG_CHUNK: cmd_deltimer -->

**Signature:**
```c
*deltimer "NPC::OnLabel";
```

---

### addtimercount

<!-- RAG_CHUNK: cmd_addtimercount -->

**Signature:**
```c
*addtimercount <ticks>,"NPC::OnLabel";
```

**Description:**
These commands will create, destroy, and delay a countdown timer - 'addtimer' to create, 'deltimer' to destroy and 'addtimercount' to delay it by the specified number of ticks. For all three cases, the event label given is the identifier of that timer. The timer runs on the character object that is attached to the script, and can have multiple instances. When the label is run, it is run as if the player that the timer runs on has clicked the NPC.

**Example:**
```c
	dispbottom "Starting a 5 second timer...";
	addtimer 5000, strnpcinfo(3) + "::On5secs";
	end;
```

---

### initnpctimer

<!-- RAG_CHUNK: cmd_initnpctimer -->

**Signature:**
```c
*initnpctimer{ "<NPC name>" {, <Attach Flag>} } |
```

**Description:**
{ "<NPC name>" | <Attach Flag> };

---

### stopnpctimer

<!-- RAG_CHUNK: cmd_stopnpctimer -->

**Signature:**
```c
*stopnpctimer{ "<NPC name>" {, <Detach Flag>}  } |
```

**Description:**
{ "<NPC name>" | <Detach Flag> };

---

### startnpctimer

<!-- RAG_CHUNK: cmd_startnpctimer -->

**Signature:**
```c
*startnpctimer{ "<NPC name>" {, <Attach Flag>} } |
```

**Description:**
{ "<NPC name>" | <Attach Flag> };

---

### setnpctimer

<!-- RAG_CHUNK: cmd_setnpctimer -->

**Signature:**
```c
*setnpctimer <tick>{,"<NPC name>"};
```

---

### getnpctimer

<!-- RAG_CHUNK: cmd_getnpctimer -->

**Signature:**
```c
*getnpctimer(<type of information>{,"<NPC name>"})
```

---

### attachnpctimer

<!-- RAG_CHUNK: cmd_attachnpctimer -->

**Signature:**
```c
*attachnpctimer {"<character name>"};
```

---

### detachnpctimer

<!-- RAG_CHUNK: cmd_detachnpctimer -->

**Signature:**
```c
*detachnpctimer {"<NPC name>"};
```

**Description:**
This set of commands and functions will create and manage an NPC-based timer. The NPC name may be omitted, in which case the calling NPC is used as target.

**Example:**
```c
     specified NPC waiting for execution.
```

---

### sleep

<!-- RAG_CHUNK: cmd_sleep -->

**Signature:**
```c
*sleep {<milliseconds>};
```

---

### sleep2

<!-- RAG_CHUNK: cmd_sleep2 -->

**Signature:**
```c
*sleep2 {<milliseconds>};
```

---

### awake

<!-- RAG_CHUNK: cmd_awake -->

**Signature:**
```c
*awake "<NPC name>";
```

**Description:**
These commands are used to control the pause of a NPC. sleep and sleep2 will pause the script for the given amount of milliseconds. Awake is used to cancel a sleep. When awake is called on a NPC it will run as if the sleep timer ran out, and thus making the script continue. Sleep and sleep2 basically do the same, but the main difference is that sleep will not keep the rid, while sleep2 does. Also sleep2 will stop the script if there is no unit attached.

**Example:**
```c
	sleep 10000; //pause the script for 10 seconds and ditch the RID (so no player is attached anymore)
	sleep2 5000; //pause the script for 5 seconds, and continue with the RID attached.
	awake "NPC"; //Cancels any running sleep timers on the NPC 'NPC'.

```

---

### progressbar

<!-- RAG_CHUNK: cmd_progressbar -->

**Signature:**
```c
*progressbar "<color>",<seconds>;
```

**Description:**
This command works almost like sleep2, but displays a progress bar above the head of the currently attached character (like cast bar). Once the given amount of seconds passes, the script resumes. If the character moves while the progress bar progresses, it is aborted and the script ends. The color format is in RGB (RRGGBB). The color is currently ignored by the client and appears always green.

---

### progressbar_npc

<!-- RAG_CHUNK: cmd_progressbar_npc -->

**Signature:**
```c
*progressbar_npc "<color>",<seconds>{,<"NPC Name">};
```

**Description:**
This command works like progressbar, but displays a progress bar above the head of the currently attached (or given) NPC. Once the given amount of seconds passes, the script resumes. The color format is in RGB (RRGGBB). The color is currently ignored by the client and appears always green.

---

### announce

<!-- RAG_CHUNK: cmd_announce -->

**Signature:**
```c
*announce "<text>",<flag>{,<fontColor>{,<fontType>{,<fontSize>{,<fontAlign>{,<fontY>{,<char_id>}}}}}};
```

**Description:**
This command will broadcast a message to all or most players, similar to @kami/@kamib GM commands.

**Example:**
```c
	announce "This will be shown to everyone at all in yellow.",0;

```

---

### mapannounce

<!-- RAG_CHUNK: cmd_mapannounce -->

**Signature:**
```c
*mapannounce "<map name>","<text>",<flag>{,<fontColor>{,<fontType>{,<fontSize>{,<fontAlign>{,<fontY>}}}}}};
```

**Description:**
This command will work like 'announce' but will only broadcast to characters currently residing on the specified map. The flag and optional parameters parameters are the same as in 'announce', but target and source flags are ignored.

---

### areaannounce

<!-- RAG_CHUNK: cmd_areaannounce -->

**Signature:**
```c
*areaannounce "<map name>",<x1>,<y1>,<x2>,<y2>,"<text>",<flag>{,<fontColor>{,<fontType>{,<fontSize>{,<fontAlign>{,<fontY>}}}}}};
```

**Description:**
This command works like 'announce' but will only broadcast to characters residing in the specified x1/y1-x2/y2 rectangle on the map given. The flags and optional parameters are the same as in 'announce', but target and source flags are ignored.

---

### callshop

<!-- RAG_CHUNK: cmd_callshop -->

**Signature:**
```c
*callshop "<name>"{,<option>};
```

**Description:**
These are a series of commands used to create dynamic shops. The 'callshop' function calls an invisible shop (view -1) as if the player clicked on it.

**Example:**
```c
	0 = The normal window (buy, sell and cancel) (default)
	1 = The buy window
	2 = The sell window

```

---

### npcshopitem

<!-- RAG_CHUNK: cmd_npcshopitem -->

**Signature:**
```c
*npcshopitem "<name>",<item id>,<price>{,<item id>,<price>{,<item id>,<price>{,...}}};
```

---

### npcshopitem

<!-- RAG_CHUNK: cmd_npcshopitem -->

**Signature:**
```c
*npcshopitem "<name>",<item id>,<price>,<stock>{,<item id>,<price>,<stock>{,<item id>,<price>,<stock>{,...}}};
```

**Description:**
This command lets you override the contents of an existing NPC shop or cashshop. The current sell list will be wiped, and only the items specified with the price specified will be for sale.

---

### npcshopadditem

<!-- RAG_CHUNK: cmd_npcshopadditem -->

**Signature:**
```c
*npcshopadditem "<name>",<item id>,<price>{,<item id>,<price>{,<item id>,<price>{,...}}};
```

---

### npcshopadditem

<!-- RAG_CHUNK: cmd_npcshopadditem -->

**Signature:**
```c
*npcshopadditem "<name>",<item id>,<price>,<stock>{,<item id>,<price>,<stock>{,<item id>,<price>,<stock>{,...}}};
```

**Description:**
This command will add more items at the end of the selling list for the specified NPC shop or cashshop. If you specify an item already for sell, that item will appear twice on the sell list.

---

### npcshopdelitem

<!-- RAG_CHUNK: cmd_npcshopdelitem -->

**Signature:**
```c
*npcshopdelitem "<name>",<item id>{,<item id>{,<item id>{,...}}};
```

**Description:**
This command will remove items from the specified NPC shop or cashshop. If the item to remove exists more than once on the shop, all instances will be removed.

---

### npcshopattach

<!-- RAG_CHUNK: cmd_npcshopattach -->

**Signature:**
```c
*npcshopattach "<name>"{,<flag>};
```

**Description:**
This command will attach the current script to the given NPC shop. When a script is attached to a shop, the events "OnBuyItem" and "OnSellItem" of your script will be executed whenever a player buys/sells from the shop. Additionally, the arrays @bought_nameid[], @bought_quantity[] or @sold_nameid[] and @sold_quantity[] will be filled up with the items and quantities bought/sold.

---

### npcshopupdate

<!-- RAG_CHUNK: cmd_npcshopupdate -->

**Signature:**
```c
*npcshopupdate "<name>",<item_id>,<price>{,<stock>}
```

**Description:**
Update an entry from a shop. If the price is 0 it won't be changed. May also be used for marketshop to update the stock quantity. For unlimited stock, use -1. For other shop types, the stock value has no effect.

---

### waitingroom

<!-- RAG_CHUNK: cmd_waitingroom -->

**Signature:**
```c
*waitingroom "<chatroom name>",<limit>{,"<event label>"{,<trigger>{,<required zeny>{,<min lvl>{,<max lvl>}}}}};
```

**Description:**
This command will create a chat room, owned by the NPC object running this script and displayed above the NPC sprite. The maximum length of a chat room name is 60 letters.

**Example:**
```c
    waitingroom "Hello World",0;

```

---

### delwaitingroom

<!-- RAG_CHUNK: cmd_delwaitingroom -->

**Signature:**
```c
*delwaitingroom {"<NPC object name"};
```

**Description:**
This command will delete a waiting room. If no parameter is given, it will delete a waiting room attached to the NPC object running this command, if it is, it will delete a waiting room owned by another NPC object. This is the only way to get rid of a waiting room, nothing else will cause it to disappear.

---

### enablewaitingroomevent

<!-- RAG_CHUNK: cmd_enablewaitingroomevent -->

**Signature:**
```c
*enablewaitingroomevent {"<NPC object name>"};
```

---

### disablewaitingroomevent

<!-- RAG_CHUNK: cmd_disablewaitingroomevent -->

**Signature:**
```c
*disablewaitingroomevent {"<NPC object name>"};
```

---

### enablearena

<!-- RAG_CHUNK: cmd_enablearena -->

**Signature:**
```c
*enablearena;
```

---

### disablearena

<!-- RAG_CHUNK: cmd_disablearena -->

**Signature:**
```c
*disablearena;
```

**Description:**
This will enable and disable triggering the waiting room event (see 'waitingroom') respectively. Optionally giving an NPC object name will do that for a specified NPC object. The chat room will not disappear when triggering is disabled and enabled in this manner and players will not be kicked out of it. Enabling a chat room event will also cause it to immediately check whether the number of users in it exceeded the trigger amount and trigger the event accordingly.

---

### getwaitingroomstate

<!-- RAG_CHUNK: cmd_getwaitingroomstate -->

**Signature:**
```c
*getwaitingroomstate(<information type>{,"<NPC object name>"})
```

**Description:**
This function will return information about the waiting room state for the attached waiting room or for a waiting room attached to the specified NPC if any.

**Example:**
```c
      0 otherwise.
```

---

### warpwaitingpc

<!-- RAG_CHUNK: cmd_warpwaitingpc -->

**Signature:**
```c
*warpwaitingpc "<map name>",<x>,<y>{,<number of people>};
```

**Description:**
This command will warp the amount of characters equal to the trigger number of the waiting room chat attached to the NPC object running this command to the specified map and coordinates, kicking them out of the chat. Those waiting the longest will get warped first. It can also do a random warp on the same map ("Random" instead of map name) and warp to the save point ("SavePoint").

**Example:**
```c
                  characters who were just warped.
```

---

### waitingroomkick

<!-- RAG_CHUNK: cmd_waitingroomkick -->

**Signature:**
```c
*waitingroomkick "<NPC object name>" , "<character name>";
```

**Description:**
This command kicks the given character from the waiting room attached to the given NPC.

---

### getwaitingroomusers

<!-- RAG_CHUNK: cmd_getwaitingroomusers -->

**Signature:**
```c
*getwaitingroomusers "<NPC object name>";
```

**Description:**
This command get all the characters in the waiting room of the given NPC and stores their gids in the array .@waitingroom_users[]. Also, stores the number of characters in the variable .@waitingroom_usercount.

---

### kickwaitingroomall

<!-- RAG_CHUNK: cmd_kickwaitingroomall -->

**Signature:**
```c
*kickwaitingroomall {"<NPC object name>"};
```

**Description:**
This command kicks everybody out of a specified waiting room chat.

---

### setmapflagnosave

<!-- RAG_CHUNK: cmd_setmapflagnosave -->

**Signature:**
```c
*setmapflagnosave "<map name>","<alternate map name>",<x>,<y>;
```

**Description:**
This command sets the 'nosave' flag for the specified map and also gives an alternate respawn-upon-relogin point.

---

### setmapflag

<!-- RAG_CHUNK: cmd_setmapflag -->

**Signature:**
```c
*setmapflag "<map name>",<flag>{,<zone>{,<type>}};
```

**Description:**
This command marks a specified map with the given map flag, which will alter the behavior of the map. A full list of mapflags is located in 'src/map/script_constants.hpp' with the 'mf_' prefix, and documentation can be found in 'doc/mapflags.txt'.

---

### removemapflag

<!-- RAG_CHUNK: cmd_removemapflag -->

**Signature:**
```c
*removemapflag "<map name>",<flag>{,<zone>};
```

**Description:**
This command removes a mapflag from a specified map. See 'setmapflag' for a list of mapflags.

---

### getmapflag

<!-- RAG_CHUNK: cmd_getmapflag -->

**Signature:**
```c
*getmapflag("<map name>",<flag>{,<type>})
```

**Description:**
This command checks the status of a given mapflag and returns the mapflag's state. 0 means OFF, and 1 means ON. See 'setmapflag' for a list of mapflags.

---

### setbattleflag

<!-- RAG_CHUNK: cmd_setbattleflag -->

**Signature:**
```c
*setbattleflag "<battle flag>",<value>{,<reload>};
```

---

### getbattleflag

<!-- RAG_CHUNK: cmd_getbattleflag -->

**Signature:**
```c
*getbattleflag("<battle flag>")
```

**Description:**
Sets or gets the value of the given battle flag. Battle flags are the flags found in the battle / *.conf files and is also used in Lupus' variable rates script. If the reload value is given then the server will attempt to reload monster data to properly apply the new rates. This applies to EXP/Drop type configs. The server will only attempt to reload specific configs.

**Example:**
```c
	setBattleFlag "base_exp_rate",2000;

```

---

### warpportal

<!-- RAG_CHUNK: cmd_warpportal -->

**Signature:**
```c
*warpportal <source x>,<source y>,"<map name>",<target x>,<target y>;
```

**Description:**
Creates a warp portal identical to the Acolyte "Warp Portal" skill. The source coordinates specify the portal's location on the map of the invoking NPC. The target map and coordinates determine the destination of the portal.

**Example:**
```c
	warpportal 150,150,"prontera",150,180;

```

---

### mapwarp

<!-- RAG_CHUNK: cmd_mapwarp -->

**Signature:**
```c
*mapwarp "<from map>","<to map>",<x>,<y>{,<type>,<ID>};
```

**Description:**
This command will collect all characters located on the From map and warp them wholesale to the same point on the To map, or randomly distribute them there if the coordinates are zero. "Random" is understood as a special To map name and will mean randomly shuffling everyone on the same map.

**Example:**
```c
	mapwarp "prontera","alberta",150,150,1,63;

```

---

### maprespawnguildid

<!-- RAG_CHUNK: cmd_maprespawnguildid -->

**Signature:**
```c
*maprespawnguildid "<map name>",<guild id>,<flag>;
```

**Description:**
This command goes through the specified map and for each player and monster found there does stuff.

---

### agitstart

<!-- RAG_CHUNK: cmd_agitstart -->

**Signature:**
```c
*agitstart;
```

---

### agitend

<!-- RAG_CHUNK: cmd_agitend -->

**Signature:**
```c
*agitend;
```

---

### agitstart2

<!-- RAG_CHUNK: cmd_agitstart2 -->

**Signature:**
```c
*agitstart2;
```

---

### agitend2

<!-- RAG_CHUNK: cmd_agitend2 -->

**Signature:**
```c
*agitend2;
```

---

### agitstart3

<!-- RAG_CHUNK: cmd_agitstart3 -->

**Signature:**
```c
*agitstart3;
```

---

### agitend3

<!-- RAG_CHUNK: cmd_agitend3 -->

**Signature:**
```c
*agitend3;
```

**Description:**
These commands will start and end War of Emperium FE, War of Emperium SE, or War of Emperium TE.

---

### gvgon

<!-- RAG_CHUNK: cmd_gvgon -->

**Signature:**
```c
*gvgon "<map name>";
```

---

### gvgoff

<!-- RAG_CHUNK: cmd_gvgoff -->

**Signature:**
```c
*gvgoff "<map name>";
```

**Description:**
These commands will turn GVG mode for the specified maps on and off, setting up appropriate map flags. In GVG mode, maps behave as if during the time of WoE, even though WoE itself may or may not actually be in effect.

---

### gvgon3

<!-- RAG_CHUNK: cmd_gvgon3 -->

**Signature:**
```c
*gvgon3 "<map name>";
```

---

### gvgoff3

<!-- RAG_CHUNK: cmd_gvgoff3 -->

**Signature:**
```c
*gvgoff3 "<map name>";
```

**Description:**
Theses commands behave identically to gvgon/gvgoff, but apply GVG_TE mapflag.

---

### flagemblem

<!-- RAG_CHUNK: cmd_flagemblem -->

**Signature:**
```c
*flagemblem <guild id>;
```

**Description:**
This command only works when run by the NPC objects which have sprite id 722, which is a 3D guild flag sprite. If it isn't, the data will change, but nothing will be seen by anyone. If it is invoked in that manner, the emblem of the specified guild will appear on the flag, though, if any players are watching it at this moment, they will not see the emblem change until they move out of sight of the flag and return.

**Example:**
```c
    flagemblem GetCastleData("guildcastle",1);

```

---

### guardian

<!-- RAG_CHUNK: cmd_guardian -->

**Signature:**
```c
*guardian "<map name>",<x>,<y>,"<name to show>",<mob id>{,"<event label>"{,<guardian index>}};
```

**Description:**
This command is roughly equivalent to 'monster', but is meant to be used with castle guardian monsters and will only work with them. It will set the guardian characteristics up according to the castle's investment values and otherwise set the things up that only castle guardians need.

---

### guardianinfo

<!-- RAG_CHUNK: cmd_guardianinfo -->

**Signature:**
```c
*guardianinfo("<map name>", <guardian number>, <type>);
```

**Description:**
This function will return various info about the specified guardian, or -1 if it fails for some reason. It is primarily used in the castle manager NPC.

---

### getguildalliance

<!-- RAG_CHUNK: cmd_getguildalliance -->

**Signature:**
```c
*getguildalliance(<guild id1>, <guild id2>);
```

**Description:**
This command will return the relation between 2 guilds.

---

### npcspeed

<!-- RAG_CHUNK: cmd_npcspeed -->

**Signature:**
```c
*npcspeed( <speed value> {,"<npc name>"} );
```

---

### npcwalkto

<!-- RAG_CHUNK: cmd_npcwalkto -->

**Signature:**
```c
*npcwalkto( <x>,<y> {,"<npc name>"} } );
```

---

### npcstop

<!-- RAG_CHUNK: cmd_npcstop -->

**Signature:**
```c
*npcstop( {"<npc name>", {"<flag>"}});
```

**Description:**
These commands will make the NPC object in question move around the map.

---

### movenpc

<!-- RAG_CHUNK: cmd_movenpc -->

**Signature:**
```c
*movenpc "<NPC name>",<x>,<y>{,<dir>};
```

**Description:**
This command looks like the NPCWalkToxy function,but is a little different.

**Example:**
```c
	moveNPC "Bugga",100,20;

```

---

### debugmes

<!-- RAG_CHUNK: cmd_debugmes -->

**Signature:**
```c
*debugmes "<message>";
```

**Description:**
This command will send a debug message to the server console (map-server window). It will not be displayed anywhere else.

**Example:**
```c
    // Displays "NAME has clicked me!" in the map-server window.
    debugmes strcharinfo(0) + " has clicked me!";

```

---

### errormes

<!-- RAG_CHUNK: cmd_errormes -->

**Signature:**
```c
*errormes "<message>";
```

**Description:**
This command will send an error message to the server console (map-server window). It will not be displayed anywhere else.

**Example:**
```c
    // Displays "NAME has clicked me!" in the map-server window.
    errormes strcharinfo(0) + " has clicked me!";

```

---

### logmes

<!-- RAG_CHUNK: cmd_logmes -->

**Signature:**
```c
*logmes "<message>";
```

**Description:**
This command will write the message given to the map server NPC log file, as specified in 'conf/log_athena.conf'. In the TXT version of the server, the log file is 'log/npclog.log' by default. In the SQL version, if SQL logging is enabled, the message will go to the 'npclog' table, otherwise, it will go to the same log file.

---

### globalmes

<!-- RAG_CHUNK: cmd_globalmes -->

**Signature:**
```c
*globalmes "<message>"{,"<NPC name>"};
```

**Description:**
This command will send a message to the chat window of all currently connected characters.

---

### rand

<!-- RAG_CHUNK: cmd_rand -->

**Signature:**
```c
*rand(<number>{,<number>});
```

**Description:**
This function returns a number ... (if you specify one) ... randomly positioned between 0 and the number you specify -1. (if you specify two) ... randomly positioned between the two numbers you specify.

---

### viewpoint

<!-- RAG_CHUNK: cmd_viewpoint -->

**Signature:**
```c
*viewpoint <action>,<x>,<y>,<point number>,<color>{,<Char ID>};
```

**Description:**
This command will mark places on the mini map in the client connected to the invoking character. It uses the normal X and Y coordinates from the main map. The colors of the marks are defined using a hexadecimal number, same as the ones used to color text in 'mes' output, but are written as hexadecimal numbers in C. (They look like 0x<six numbers>.)

---

### viewpointmap

<!-- RAG_CHUNK: cmd_viewpointmap -->

**Signature:**
```c
*viewpointmap "<map name>",<action>,<x>,<y>,<point number>,<color>;
```

**Description:**
This command will mark places on the mini map in the client for all players currently on the defined map. It uses the normal X and Y coordinates from the main map. The colors of the marks are defined using a hexadecimal number, same as the ones used to color text in 'mes' output, but are written as hexadecimal numbers in C. (They look like 0x<six numbers>.)

---

### cutin

<!-- RAG_CHUNK: cmd_cutin -->

**Signature:**
```c
*cutin "<filename>",<position>;
```

**Description:**
This command will display a picture, usually an NPC illustration, also called cutin, for the currently attached client. The position parameter determines the placement of the illustration and takes following values:

---

### emotion

<!-- RAG_CHUNK: cmd_emotion -->

**Signature:**
```c
*emotion <emotion number>{,<target>};
```

**Description:**
This command makes an object display an emotion sprite above their own as if they were doing that emotion. For a full list of emotion numbers, see 'src/map/script_constants.hpp' under 'ET_'. The not so obvious ones are 'ET_QUESTION' (a question mark) and 'ET_SURPRISE' (the exclamation mark).

---

### misceffect

<!-- RAG_CHUNK: cmd_misceffect -->

**Signature:**
```c
*misceffect <effect number>;
```

**Description:**
This command, if run from an NPC object that has a sprite, will call up a specified effect number, centered on the NPC sprite. If the running code does not have an object ID (a 'floating' NPC) or is not running from an NPC object at all (an item script) the effect will be centered on the character who's RID got attached to the script, if any. For usable item scripts, this command will create an effect centered on the player using the item.

---

### soundeffect

<!-- RAG_CHUNK: cmd_soundeffect -->

**Signature:**
```c
*soundeffect "<effect filename>",<type>;
```

---

### soundeffectall

<!-- RAG_CHUNK: cmd_soundeffectall -->

**Signature:**
```c
*soundeffectall "<effect filename>",<type>{,"<map name>"}{,<x0>,<y0>,<x1>,<y1>};
```

**Description:**
These two commands will play a sound effect to either the invoking character only ('soundeffect') or multiple characters ('soundeffectall'). If the running code does not have an object ID (a 'floating' NPC) or is not running from an NPC object at all (an item script) the sound will be centered on the character who's RID got attached to the script, if any. If it does, it will be centered on that object. (an NPC sprite)

---

### play

<!-- RAG_CHUNK: cmd_play -->

**Signature:**
```c
*playBGM "<BGM filename>";
```

---

### play

<!-- RAG_CHUNK: cmd_play -->

**Signature:**
```c
*playBGMall "<BGM filename>"{,"<map name>"{,<x0>,<y0>,<x1>,<y1>}};
```

**Description:**
These two commands will play a Background Music to either the invoking character only ('playBGM') or multiple characters ('playBGMall').

---

### pvpon

<!-- RAG_CHUNK: cmd_pvpon -->

**Signature:**
```c
*pvpon "<map name>";
```

---

### pvpoff

<!-- RAG_CHUNK: cmd_pvpoff -->

**Signature:**
```c
*pvpoff "<map name>";
```

**Description:**
These commands will turn PVP mode for the specified maps on and off. Beside setting the flags referred to in 'setmapflag', 'pvpon' will also create a PVP timer and ranking as will @pvpon GM command do.

---

### atcommand

<!-- RAG_CHUNK: cmd_atcommand -->

**Signature:**
```c
*atcommand "<command>";
```

**Description:**
This command will run the given command line exactly as if it was typed in from the keyboard by the player connected to the invoking character, and that character belonged to an account which had GM level 99.

---

### charcommand

<!-- RAG_CHUNK: cmd_charcommand -->

**Signature:**
```c
*charcommand "<command>";
```

**Description:**
This command will run the given command line exactly as if it was typed in from the keyboard from a character that belonged to an account which had GM level 99.

---

### bindatcmd

<!-- RAG_CHUNK: cmd_bindatcmd -->

**Signature:**
```c
*bindatcmd "<command>","<NPC object name>::<event label>"{,<atcommand level>,<charcommand level>};
```

**Description:**
This command will bind a NPC event label to an atcommand. Upon execution of the atcommand, the user will invoke the NPC event label. Each atcommand is only allowed one binding. If you rebind, it will override the original binding. Note: The default level for atcommand is 0 while the default level for charcommand is 100.

**Example:**
```c
	.@atcmd_command$       =  The name of the @command used.
	.@atcmd_parameters$[]  =  Array containing the given parameters, starting from an index of 0.
	.@atcmd_numparameters  =  The number of parameters defined.

```

---

### unbindatcmd

<!-- RAG_CHUNK: cmd_unbindatcmd -->

**Signature:**
```c
*unbindatcmd "<command>";
```

**Description:**
This command will unbind a NPC event label from an atcommand.

---

### useatcmd

<!-- RAG_CHUNK: cmd_useatcmd -->

**Signature:**
```c
*useatcmd "<command>";
```

**Description:**
This command will execute a script-bound atcommand for the attached RID. If the supplied command is not bound to any script, this command will act like 'atcommand' and attempt to execute a source-defined command.

---

### camerainfo

<!-- RAG_CHUNK: cmd_camerainfo -->

**Signature:**
```c
*camerainfo <range>,<rotation>,<latitude>{,<char id>};
```

**Description:**
This command will update the client's camera information with the given values where the client can be the attached character or the player given by the char id parameter. Note: This requires 2016-05-25aRagexeRE or newer.

---

### refineui

<!-- RAG_CHUNK: cmd_refineui -->

**Signature:**
```c
*refineui({<char id>})
```

**Description:**
Opens the refine UI for the attached player or the given character id.

---

### openstylist

<!-- RAG_CHUNK: cmd_openstylist -->

**Signature:**
```c
*openstylist({<char id>})
```

**Description:**
Opens the stylist UI for the attached player or the given character id.

---

### laphine_synthesis

<!-- RAG_CHUNK: cmd_laphine_synthesis -->

**Signature:**
```c
*laphine_synthesis({<item id>})
```

---

### laphine_synthesis

<!-- RAG_CHUNK: cmd_laphine_synthesis -->

**Signature:**
```c
*laphine_synthesis({<"item name">})
```

**Description:**
Opens the laphine synthesis UI for <item ID> or <item name> for the attached player. If run from within an item script <item ID> or <item name> is optional.

---

### laphine_upgrade

<!-- RAG_CHUNK: cmd_laphine_upgrade -->

**Signature:**
```c
*laphine_upgrade()
```

**Description:**
Opens the laphine upgrade UI for the attached player.

---

### openbank

<!-- RAG_CHUNK: cmd_openbank -->

**Signature:**
```c
*openbank({<char id>})
```

**Description:**
Opens the Bank UI for the attached player or the given character ID.

---

### enchantgradeui

<!-- RAG_CHUNK: cmd_enchantgradeui -->

**Signature:**
```c
*enchantgradeui {<char id>};
```

**Description:**
Opens the enchantgrade UI for the attached character or the player given by the char ID parameter.

---

### set_reputation_points

<!-- RAG_CHUNK: cmd_set_reputation_points -->

**Signature:**
```c
*set_reputation_points(<type>,<points>{,<char id>})
```

**Description:**
Sets the reputation points via <points> for reputation group <type> for the attached player or the given character ID. <type> is the client side index as stored in the Id field of the reputation.yml database files.

---

### get_reputation_points

<!-- RAG_CHUNK: cmd_get_reputation_points -->

**Signature:**
```c
*get_reputation_points(<type>{,<char id>})
```

**Description:**
Gets the reputation points for reputation group <type> for the attached player or the given character ID. <type> is the client side index as stored in the Id field of the reputation.yml database files.

---

### add_reputation_points

<!-- RAG_CHUNK: cmd_add_reputation_points -->

**Signature:**
```c
*add_reputation_points(<type>,<points>{,<char id>})
```

**Description:**
Adds the reputation points via <points> for reputation group <type> for the attached player or the given character ID. <type> is the client side index as stored in the Id field of the reputation.yml database files.

---

### item_reform

<!-- RAG_CHUNK: cmd_item_reform -->

**Signature:**
```c
*item_reform({<item id>{,<char id>}})
```

---

### item_reform

<!-- RAG_CHUNK: cmd_item_reform -->

**Signature:**
```c
*item_reform({<"item name">{,<char id>}})
```

**Description:**
Opens the item reform UI for <item ID> or <item name> for the attached player or the given character ID. If run from within an item script <item ID> or <item name> is optional.

---

### item_enchant

<!-- RAG_CHUNK: cmd_item_enchant -->

**Signature:**
```c
*item_enchant(<client side LUA index>{,<char ID>});
```

**Description:**
Opens the enchant UI for the attached character or the player given by the <char ID> parameter. If the player exceeds 70% weight the client will not open the enchant UI and will trigger an error message instead.

---

### opentips

<!-- RAG_CHUNK: cmd_opentips -->

**Signature:**
```c
*opentips({<Tip ID>,{<char ID>}});
```

**Description:**
Opens the tip box UI for the attached player or the given character ID.

---

### specialpopup

<!-- RAG_CHUNK: cmd_specialpopup -->

**Signature:**
```c
*specialpopup(<popup ID>);
```

**Description:**
Open popup and/or show text by ID from list defined in the client spopup.lub file. Popup and text is only visible if the player warped from one map to another map.

---

### unitwalk

<!-- RAG_CHUNK: cmd_unitwalk -->

**Signature:**
```c
*unitwalk <GID>,<x>,<y>{,"<event label>"};
```

---

### unitwalkto

<!-- RAG_CHUNK: cmd_unitwalkto -->

**Signature:**
```c
*unitwalkto <GID>,<Target GID>{,"<event label>"};
```

**Description:**
This command will tell a <GID> to walk to a position, defined either as a set of coordinates or another object. The command returns a 1 for success and 0 upon failure.

**Example:**
```c
	unitwalk getcharid(3),150,150;

```

---

### unitattack

<!-- RAG_CHUNK: cmd_unitattack -->

**Signature:**
```c
*unitattack <GID>,<Target ID>{,<action type>};
```

---

### unitattack

<!-- RAG_CHUNK: cmd_unitattack -->

**Signature:**
```c
*unitattack <GID>,"<Target Name>"{,<action type>};
```

**Description:**
This command will make a <GID> attack the specified target. It returns true upon success and false for all failures.

---

### unitkill

<!-- RAG_CHUNK: cmd_unitkill -->

**Signature:**
```c
*unitkill <GID>;
```

**Description:**
This command will kill a <GID>.

---

### unitwarp

<!-- RAG_CHUNK: cmd_unitwarp -->

**Signature:**
```c
*unitwarp <GID>,"<map name>",<x>,<y>;
```

**Description:**
This command will warp a <GID> to the specified map and coordinates.

---

### unitstopattack

<!-- RAG_CHUNK: cmd_unitstopattack -->

**Signature:**
```c
*unitstopattack <GID>;
```

**Description:**
This command will make a <GID> stop attacking.

---

### unitstopwalk

<!-- RAG_CHUNK: cmd_unitstopwalk -->

**Signature:**
```c
*unitstopwalk <GID>{,<flag>};
```

**Description:**
This command will make a <GID> stop moving.

---

### unittalk

<!-- RAG_CHUNK: cmd_unittalk -->

**Signature:**
```c
*unittalk <GID>,"<text>"{,flag};
```

**Description:**
This command will make a <GID> say a message. The display name of the <GID> won't get appended in front of the message. flag: Specify target    bc_area - Message is sent to players in the vicinity of the source (default).    bc_self - Message is sent only to player attached.

---

### unitskilluseid

<!-- RAG_CHUNK: cmd_unitskilluseid -->

**Signature:**
```c
*unitskilluseid <GID>,<skill id>,<skill lvl>{,<target id>,<casttime>,<cancel>,<Line_ID>,<ignore_range>};
```

---

### unitskilluseid

<!-- RAG_CHUNK: cmd_unitskilluseid -->

**Signature:**
```c
*unitskilluseid <GID>,"<skill name>",<skill lvl>{,<target id>,<casttime>,<cancel>,<Line_ID>,<ignore_range>};
```

---

### unitskillusepos

<!-- RAG_CHUNK: cmd_unitskillusepos -->

**Signature:**
```c
*unitskillusepos <GID>,<skill id>,<skill lvl>,<x>,<y>{,<casttime>,<cancel>,<Line_ID>,<ignore_range>};
```

---

### unitskillusepos

<!-- RAG_CHUNK: cmd_unitskillusepos -->

**Signature:**
```c
*unitskillusepos <GID>,"<skill name>",<skill lvl>,<x>,<y>{,<casttime>,<cancel>,<Line_ID>,<ignore_range>};
```

**Description:**
This is the replacement of the older commands, these use the same values for GID as the other unit* commands (See 'GID').

---

### unitexists

<!-- RAG_CHUNK: cmd_unitexists -->

**Signature:**
```c
*unitexists <GID>;
```

**Description:**
Checks if the given Game ID exists. Returns false if the object doesn't exist, or true if it does.

---

### getunittype

<!-- RAG_CHUNK: cmd_getunittype -->

**Signature:**
```c
*getunittype <GID>;
```

**Description:**
Returns the type of object from the given Game ID. Returns -1 if the given GID does not exist.

---

### getunitname

<!-- RAG_CHUNK: cmd_getunitname -->

**Signature:**
```c
*getunitname <GID>;
```

**Description:**
Gets the name of the given unit. Supported types are monster, homunculus, pet, and NPC. Mercenary and Elemental don't support custom names.

---

### setunitname

<!-- RAG_CHUNK: cmd_setunitname -->

**Signature:**
```c
*setunitname <GID>,"<new name>";
```

**Description:**
Changes the name of the given unit to the new name given. Supported types are monster, homunculus, and pet. To change an NPC's name, see 'setnpcdisplay'. Mercenary and Elemental don't support custom names.

---

### setunittitle

<!-- RAG_CHUNK: cmd_setunittitle -->

**Signature:**
```c
*setunittitle <GID>,<title>;
```

**Description:**
Apply a <title> to the given <GID>.

---

### getunittitle

<!-- RAG_CHUNK: cmd_getunittitle -->

**Signature:**
```c
*getunittitle <GID>;
```

**Description:**
Returns the title of the given <GID>.

---

### getunitdata

<!-- RAG_CHUNK: cmd_getunitdata -->

**Signature:**
```c
*getunitdata <GID>,<arrayname>;
```

---

### setunitdata

<!-- RAG_CHUNK: cmd_setunitdata -->

**Signature:**
```c
*setunitdata <GID>,<parameter>,<new value>;
```

**Description:**
This is used to get and set special data related to the unit. With getunitdata, the array given will be filled with the current data. In setunitdata the indexes in the array would be used to set that data on the unit.

**Example:**
```c
      recalculated (HIT, FLEE, etc) automatically. Keep in mind that some stats don't
	  affect a unit's status and will have to directly be modified.

```

---

### setunitdata

<!-- RAG_CHUNK: cmd_setunitdata -->

**Signature:**
```c
*setunitdata <GID>,<parameter>,<new value>;
```

**Description:**
This is used to get and set special data related to the unit. With getunitdata, the array given will be filled with the current data. In setunitdata the indexes in the array would be used to set that data on the unit.

**Example:**
```c
      recalculated (HIT, FLEE, etc) automatically. Keep in mind that some stats don't
	  affect a unit's status and will have to directly be modified.

```

---

### geteleminfo

<!-- RAG_CHUNK: cmd_geteleminfo -->

**Signature:**
```c
*geteleminfo <type>{,<char_id>};
```

**Description:**
Get info of elemental of attached player or player by char_id. Other info can be obtained by 'getunitdata' command.

---

### npcskill

<!-- RAG_CHUNK: cmd_npcskill -->

**Signature:**
```c
*npcskill <skill id>,<skill lvl>,<stat point>,<NPC level>;
```

---

### npcskill

<!-- RAG_CHUNK: cmd_npcskill -->

**Signature:**
```c
*npcskill "<skill name>",<skill lvl>,<stat point>,<NPC level>;
```

**Description:**
This command causes the attached NPC object to cast a skill on the attached player. The skill will have no cast time or cooldown. The player must be within the default skill range or the command will fail silently.

**Example:**
```c
    // Casts Level 10 Heal on the attached player, calculated with
    // all stats 99 and base level 60.
    npcskill "AL_HEAL",10,99,60;

```

---

### day

<!-- RAG_CHUNK: cmd_day -->

**Signature:**
```c
*day;
```

---

### night

<!-- RAG_CHUNK: cmd_night -->

**Signature:**
```c
*night;
```

**Description:**
These two commands will switch the entire server between day and night mode respectively. If your server is set to cycle between day and night by configuration, it will eventually return to that cycle.

**Example:**
```c
	day;
	end;
```

---

### defpattern

<!-- RAG_CHUNK: cmd_defpattern -->

**Signature:**
```c
*defpattern <set number>,"<regular expression pattern>","<event label>";
```

---

### activatepset

<!-- RAG_CHUNK: cmd_activatepset -->

**Signature:**
```c
*activatepset <set number>;
```

---

### deactivatepset

<!-- RAG_CHUNK: cmd_deactivatepset -->

**Signature:**
```c
*deactivatepset <set number>;
```

---

### deletepset

<!-- RAG_CHUNK: cmd_deletepset -->

**Signature:**
```c
*deletepset <set number>;
```

**Description:**
This set of commands is only available if the server is compiled with regular expressions library enabled. Default compilation and most binary distributions aren't, which is probably bad, since these, while complex to use, are quite fascinating.

---

### pow

<!-- RAG_CHUNK: cmd_pow -->

**Signature:**
```c
*pow(<number>,<power>)
```

**Description:**
Returns the result of the calculation.

**Example:**
```c
	.@i = pow(2,3); // .@i will be 8

```

---

### sqrt

<!-- RAG_CHUNK: cmd_sqrt -->

**Signature:**
```c
*sqrt(<number>)
```

**Description:**
Returns the square-root of a number.

**Example:**
```c
	.@i = sqrt(25); // .@i will be 5

```

---

### distance

<!-- RAG_CHUNK: cmd_distance -->

**Signature:**
```c
*distance(<x0>,<y0>,<x1>,<y1>)
```

**Description:**
Returns distance between 2 points.

**Example:**
```c
	.@i = distance(100,200,101,202);

```

---

### min

<!-- RAG_CHUNK: cmd_min -->

**Signature:**
```c
*min(<number or array>{,<number or array>,...})
```

---

### minimum

<!-- RAG_CHUNK: cmd_minimum -->

**Signature:**
```c
*minimum(<number or array>{,<number or array>,...})
```

---

### max

<!-- RAG_CHUNK: cmd_max -->

**Signature:**
```c
*max(<number or array>{,<number or array>,...})
```

---

### maximum

<!-- RAG_CHUNK: cmd_maximum -->

**Signature:**
```c
*maximum(<number or array>{,<number or array>,...})
```

**Description:**
Returns the smallest (or biggest) from the set of given parameters. These parameters have to be either numbers or number arrays.

**Example:**
```c
	.@minimum = min( 1, -6, -2, 8, 2 ); // .@minimum will be equal to -6
	.@maximum = max( 0, 5, 10, 4 ); // .@maximum will be equal to 10
	.@level = min( BaseLevel, 70 ); // .@level will be the character's base level, capped to 70

	setarray .@testarray, 4, 5, 12, 6, 7, 3, 8, 9, 10;

	.@minimum = min( .@testarray ); // .@minimum will be equal to 3
	.@maximum = max( .@testarray ); // .@maximum will be equal to 12

	.@minimum = min( -6, 1, 2, 3, .@testarray ); // .@minimum will be equal to -6
	.@maximum = max( -6, 1, 2, 3, .@testarray ); // .@maximum will be equal to 12

```

---

### cap_value

<!-- RAG_CHUNK: cmd_cap_value -->

**Signature:**
```c
*cap_value(<number>, <min>, <max>)
```

**Description:**
Returns the number but capped between <min> and <max>.

**Example:**
```c
	// capped between 0 ~ 100
	.@value = cap_value(10, 0, 100);   // .@value will be equal to 10
	.@value = cap_value(1000, 0, 100); // .@value will be equal to 100
	.@value = cap_value(-10, 3, 100);  // .@value will be equal to 3

```

---

### round

<!-- RAG_CHUNK: cmd_round -->

**Signature:**
```c
*round(<number>,<precision>);
```

---

### ceil

<!-- RAG_CHUNK: cmd_ceil -->

**Signature:**
```c
*ceil(<number>,<precision>);
```

---

### floor

<!-- RAG_CHUNK: cmd_floor -->

**Signature:**
```c
*floor(<number>,<precision>);
```

**Description:**
Returns <number> rounded to multiple of <precision>.

---

### md5

<!-- RAG_CHUNK: cmd_md5 -->

**Signature:**
```c
*md5("<string>")
```

**Description:**
Returns the md5 checksum of a number or string.

**Example:**
```c
	mes md5(12345);
	mes md5("12345"); 	// Will both display 827ccb0eea8a706c4c34a16891f84e7b
	mes md5("qwerty"); 	// Will display d8578edf8458ce06fbc5bb76a58c5ca4

```

---

### query_sql

<!-- RAG_CHUNK: cmd_query_sql -->

**Signature:**
```c
*query_sql("your MySQL query"{, <array variable>{, <array variable>{, ...}}});
```

---

### query_logsql

<!-- RAG_CHUNK: cmd_query_logsql -->

**Signature:**
```c
*query_logsql("your MySQL query"{, <array variable>{, <array variable>{, ...}}});
```

**Description:**
Executes an SQL query. A 'select' query can fill array variables with up to 2 billion rows of values, and will return the number of rows (i.e. array size) or -1 on failure.

**Example:**
```c
	.@nb = query_sql("select name,fame from `char` ORDER BY fame DESC LIMIT 5", .@name$, .@fame);
	mes "Hall Of Fame: TOP5";
	mes "1." + .@name$[0] + "(" + .@fame[0] + ")"; // largest fame value.
	mes "2." + .@name$[1] + "(" + .@fame[1] + ")";
	mes "3." + .@name$[2] + "(" + .@fame[2] + ")";
	mes "4." + .@name$[3] + "(" + .@fame[3] + ")";
	mes "5." + .@name$[4] + "(" + .@fame[4] + ")";

```

---

### escape_sql

<!-- RAG_CHUNK: cmd_escape_sql -->

**Signature:**
```c
*escape_sql(<value>)
```

**Description:**
Converts the value to a string and escapes special characters so that it is safe to use in query_sql(). Returns the escaped form of the given value.

**Example:**
```c
	.@name$ = "John's Laptop";
	.@esc_str$ = escape_sql(.@name$); // Escaped string: John\'s Laptop

```

---

### setiteminfo

<!-- RAG_CHUNK: cmd_setiteminfo -->

**Signature:**
```c
*setiteminfo(<item id>,<type>,<value>)
```

---

### setiteminfo

<!-- RAG_CHUNK: cmd_setiteminfo -->

**Signature:**
```c
*setiteminfo(<aegis item name>,<type>,<value>)
```

**Description:**
This function will set some value of an item. Returns the new value on success, or -1 on fail (item_id not found or invalid type).

**Example:**
```c
	ITEMINFO_BUY             (0)   -  Buy Price
	ITEMINFO_SELL            (1)   -  Sell Price
	ITEMINFO_TYPE            (2)   -  Type
	ITEMINFO_MAXCHANCE       (3)   -  maxchance (max drop chance of this item, e.g. 1 = 0.01%)
	                                  if = 0, then monsters don't drop it at all (rare or a quest item)
	                                  if = 10000, then this item is sold in NPC shops only
	ITEMINFO_GENDER          (4)   -  Gender
	ITEMINFO_LOCATIONS       (5)   -  Location(s)
	ITEMINFO_WEIGHT          (6)   -  Weight
	ITEMINFO_ATTACK          (7)   -  ATK
	ITEMINFO_DEFENSE         (8)   -  DEF
	ITEMINFO_RANGE           (9)   -  Range
	ITEMINFO_SLOT           (10)   -  Slot
	ITEMINFO_VIEW           (11)   -  View
	ITEMINFO_EQUIPLEVELMIN  (12)   -  equipment LV
```

---

### setitemscript

<!-- RAG_CHUNK: cmd_setitemscript -->

**Signature:**
```c
*setitemscript(<item id>,<"{ new item script }">{,<type>});
```

**Description:**
Set a new script bonus to the Item. Very useful for game events. You can remove an item's itemscript by leaving the itemscript argument empty. Returns 1 on success, or 0 on fail (item_id not found or new item script is invalid). Type can optionally be used indicates which script to set (default is 0):  0 - Script  1 - EquipScript  2 - UnEquipScript

**Example:**
```c
	setitemscript 2637,"{ if (isequipped(2236) == 0)end; if (getskilllv(26)){skill 40,1;}else{skill 26,1+isequipped(2636);} }";
	setitemscript 2637,"";

```

---

### atoi

<!-- RAG_CHUNK: cmd_atoi -->

**Signature:**
```c
*atoi("<string>")
```

---

### axtoi

<!-- RAG_CHUNK: cmd_axtoi -->

**Signature:**
```c
*axtoi("<string>")
```

---

### strtol

<!-- RAG_CHUNK: cmd_strtol -->

**Signature:**
```c
*strtol("<string>", base)
```

**Description:**
These commands are used to convert strings to numbers. 'atoi' will interpret given string as a decimal number (base 10), while 'axtoi' interprets strings as hexadecimal numbers (base 16). 'strtol' lets the user specify a base (valid range is between 2 and 36 inclusive, or the special value0, which means auto-detection).

**Example:**
```c
	.@var = atoi("11");        // Sets .@var to 11
	.@var = axtoi("FF");       // Sets .@var to 255
	mes axtoi("11");           // Displays 17 (1 = 1, 10 = 16)
	.@var = strtol("11", 10);  // Sets .@var to 11 (11 base 10)
	.@var = strtol("11", 16);  // Sets .@var to 17 (11 base 16)
	.@var = strtol("11", 0);   // Sets .@var to 11 (11 base 10, auto-detected)
	.@var = strtol("0x11", 0); // Sets .@var to 17 (11 base 16, auto-detected because of the "0x" prefix)
	.@var = strtol("011", 0);  // Sets .@var to 9 (11 base 8, auto-detected because of the "0" prefix)
	.@var = strtol("11", 2);   // Sets .@var to 3 (binary 11)

```

---

### compare

<!-- RAG_CHUNK: cmd_compare -->

**Signature:**
```c
*compare("<string>","<substring>")
```

**Description:**
This command returns 1 or 0 when the substring is in the main string (1) or not (0). This command is not case sensitive.

**Example:**
```c
	//dothis; will be executed ('Bloody Murderer' contains 'Blood').
	if (compare("Bloody Murderer","Blood"))
		dothis;

	//dothat; will not be executed ('Blood butterfly' does not contain 'Bloody').
	if (compare("Blood Butterfly","Bloody"))
		dothat;

```

---

### strcmp

<!-- RAG_CHUNK: cmd_strcmp -->

**Signature:**
```c
*strcmp("<string>","<string>")
```

**Description:**
This command compares two strings are returns a value:    1: string 1 > string 2    0: strings are equal   -1: string 1 < string 2

---

### getstrlen

<!-- RAG_CHUNK: cmd_getstrlen -->

**Signature:**
```c
*getstrlen("<string>")
```

**Description:**
This function will return the length of the string given as an argument. It is useful to check if anything input by the player exceeds name length limits and other length limits and asking them to try to input something else.

---

### charisalpha

<!-- RAG_CHUNK: cmd_charisalpha -->

**Signature:**
```c
*charisalpha("<string>",<position>)
```

**Description:**
This function will return 1 if the character number Position in the given string is a letter, 0 if it isn't a letter but a digit or a space. The first letter is position 0.

---

### charat

<!-- RAG_CHUNK: cmd_charat -->

**Signature:**
```c
*charat(<string>,<index>)
```

**Description:**
Returns char at specified index. If index is out of range, returns empty string. The first letter of a string is index 0.

**Example:**
```c
	charat("This is a string", 10); //returns "s"

```

---

### setchar

<!-- RAG_CHUNK: cmd_setchar -->

**Signature:**
```c
*setchar(<string>,<char>,<index>)
```

**Description:**
Returns the original string with the char at the specified index set to the specified char. If index out of range, the original string will be returned. Only the 1st char in the <char> parameter will be used.

**Example:**
```c
	setchar("Cat", "B", 0); //returns "Bat"

```

---

### insertchar

<!-- RAG_CHUNK: cmd_insertchar -->

**Signature:**
```c
*insertchar(<string>,<char>,<index>)
```

**Description:**
Returns the original string with the specified char inserted at the specified index. If index is out of range, the char will be inserted on the end of the string that it is closest. Only the 1st char in the <char> parameter will be used.

**Example:**
```c
	insertchar("laughter", "s", 0); //returns "slaughter"

```

---

### delchar

<!-- RAG_CHUNK: cmd_delchar -->

**Signature:**
```c
*delchar(<string>,<index>)
```

**Description:**
Returns the original string with the char at the specified index removed. If index is out of range, original string will be returned.

**Example:**
```c
	delchar("Diet", 3); //returns "Die"

```

---

### strtoupper

<!-- RAG_CHUNK: cmd_strtoupper -->

**Signature:**
```c
*strtoupper(<string>)
```

---

### strtolower

<!-- RAG_CHUNK: cmd_strtolower -->

**Signature:**
```c
*strtolower(<string>)
```

**Description:**
Returns the specified string in its uppercase/lowercase form. All non-alpha characters will be preserved.

**Example:**
```c
	strtoupper("The duck is blue!!"); //returns "THE DUCK IS BLUE!!"

```

---

### charisupper

<!-- RAG_CHUNK: cmd_charisupper -->

**Signature:**
```c
*charisupper(<string>,<index>)
```

---

### charislower

<!-- RAG_CHUNK: cmd_charislower -->

**Signature:**
```c
*charislower(<string>,<index>)
```

**Description:**
Returns 1 if character at specified index of specified string is uppercase/lowercase. Otherwise, 0. Characters not of the alphabet will return 0.

**Example:**
```c
	charisupper("rAthena", 1); //returns 1

```

---

### substr

<!-- RAG_CHUNK: cmd_substr -->

**Signature:**
```c
*substr(<string>,<start_index>,<end_index>)
```

**Description:**
Returns the sub-string of the specified string inclusively between the set indexes. If indexes are out of range, or the start index is after the end index, an empty string will be returned.

**Example:**
```c
	substr("foobar", 3, 5); //returns "bar"

```

---

### explode

<!-- RAG_CHUNK: cmd_explode -->

**Signature:**
```c
*explode(<dest_array>,<string>,<delimiter>)
```

**Description:**
Breaks a string up into substrings based on the specified delimiter. Substrings will be stored within the specified string array. Only the 1st char of the delimiter parameter will be used. If an empty string is passed as a delimiter, the string will be placed in the array in its original form.

**Example:**
```c
	explode(.@my_array$, "Explode:Test:1965:red:PIE", ":");
	//.@my_array$ contents will be...
	//.@my_array$[0]: "Explode"
	//.@my_array$[1]: "Test"
	//.@my_array$[2]: "1965"
	//.@my_array$[3]: "red"
	//.@my_array$[4]: "PIE"

```

---

### implode

<!-- RAG_CHUNK: cmd_implode -->

**Signature:**
```c
*implode(<string_array>{,<glue>})
```

**Description:**
Combines all substrings within the specified string array into a single string. If the glue parameter is specified, it will be inserted inbetween each substring.

**Example:**
```c
	setarray .@my_array$[0], "This", "is", "a", "test";
	implode(.@my_array$, " "); //returns "This is a test"

```

---

### sprintf

<!-- RAG_CHUNK: cmd_sprintf -->

**Signature:**
```c
*sprintf(<format>[,param[,param[,...]]])
```

**Description:**
C style sprintf. The resulting string is returned same as in PHP. All C format specifiers are supported except %n. More info: sprintf @ www.cplusplus.com. The number of params is only limited by rA's script engine.

**Example:**
```c
	.@format$ = "The %s contains %d monkeys";
	dispbottom(sprintf(.@format$, "zoo", 5));        //prints "The zoo contains 5 monkeys"
	dispbottom(sprintf(.@format$, "barrel", 82));    //prints "The barrel contains 82 monkeys"

```

---

### sscanf

<!-- RAG_CHUNK: cmd_sscanf -->

**Signature:**
```c
*sscanf(<string>,<format>[,param[,param[,...]]])
```

**Description:**
C style sscanf. All C format specifiers are supported. More info: sscanf @ www.cplusplus.com. The number of params is only limited by rA's script engine.

**Example:**
```c
	sscanf("This is a test: 42 foobar", "This is a test: %d %s", .@num, .@str$);
	dispbottom(.@num + " " + .@str$); //prints "42 foobar"

```

---

### strpos

<!-- RAG_CHUNK: cmd_strpos -->

**Signature:**
```c
*strpos(<haystack>,<needle>{,<offset>})
```

**Description:**
PHP style strpos. Finds a substring (needle) within a string (haystack). The offset parameter indicates the index of the string to start searching. Returns index of substring on successful search, else -1. Comparison is case sensitive.

**Example:**
```c
	strpos("foobar", "bar", 0); //returns 3
	strpos("foobarfoo", "foo", 0); //returns 0
	strpos("foobarfoo", "foo", 1); //returns 6

```

---

### replacestr

<!-- RAG_CHUNK: cmd_replacestr -->

**Signature:**
```c
*replacestr(<input>, <search>, <replace>{, <usecase>{, <count>}})
```

**Description:**
Replaces all instances of a search string in the input with the specified replacement string. By default is case sensitive unless <usecase> is set to 0. If specified it will only replace as many instances as specified in the count parameter.

**Example:**
```c
	replacestr("testing tester", "test", "dash"); //returns "dashing dasher"
	replacestr("Donkey", "don", "mon", 0); //returns "monkey"
	replacestr("test test test test test", "test", "yay", 0, 3); //returns "yay yay yay test test"

```

---

### countstr

<!-- RAG_CHUNK: cmd_countstr -->

**Signature:**
```c
*countstr(<input>, <search>{, <usecase>})
```

**Description:**
Counts all instances of a search string in the input. By default is case sensitive unless <usecase> is set to 0.

**Example:**
```c
	countstr("test test test Test", "test"); //returns 3
	countstr("cake Cake", "Cake", 0); //returns 2

```

---

### preg_match

<!-- RAG_CHUNK: cmd_preg_match -->

**Signature:**
```c
*preg_match(<regular expression pattern>,<string>{,<offset>})
```

**Description:**
Searches a string for a match to the regular expression provided. The offset parameter indicates the index of the string to start searching. Returns offsets to captured substrings, or 0 if no match is found.

---

### setfont

<!-- RAG_CHUNK: cmd_setfont -->

**Signature:**
```c
*setfont <font>;
```

**Description:**
This command sets the current RO client interface font to one of the fonts stored in data\*.eot by using an ID of the font. When the ID of the currently used font is used, default interface font is used again.

---

### showdigit

<!-- RAG_CHUNK: cmd_showdigit -->

**Signature:**
```c
*showdigit <value>{,<type>};
```

**Description:**
Displays given numeric 'value' in large digital clock font on top of the screen. The optional parameter 'type' specifies visual aspects of the "clock" and can be one of the following values:

---

### setcell

<!-- RAG_CHUNK: cmd_setcell -->

**Signature:**
```c
*setcell "<map name>",<x1>,<y1>,<x2>,<y2>,<type>,<flag>;
```

**Description:**
Each map cell has several 'flags' that specify the properties of that cell. These include terrain properties (walkability, shootability, presence of water), skills (basilica, land protector, ...) and other (NPC nearby, no vending, ...). Each of these can be 'on' or 'off'. Together they define a cell's behavior.

**Example:**
```c
	setcell "arena",0,0,300,300,cell_basilica,1;
	setcell "arena",140,140,160,160,cell_basilica,0;
	setcell "arena",135,135,165,165,cell_walkable,0;
	setcell "arena",140,140,160,160,cell_walkable,1;

```

---

### checkcell

<!-- RAG_CHUNK: cmd_checkcell -->

**Signature:**
```c
*checkcell ("<map name>",<x>,<y>,<type>);
```

**Description:**
This command will return 1 or 0, depending on whether the specified cell has the 'type' flag set or not. There are various types to check, all mimicking the server's cell_chk enumeration. The types can be found in 'src/map/script_constants.hpp'.

**Example:**
```c
    these check directly for the 'terrain component' of the specified cell
```

---

### getfreecell

<!-- RAG_CHUNK: cmd_getfreecell -->

**Signature:**
```c
*getfreecell "<map name>",<rX>,<rY>{,<x>,<y>,<rangeX>,<rangeY>,<flag>};
```

**Description:**
Finds a free cell on the given map and stores the reference to the found cell in <rX> and <rY>. Passing <x> and <y> with <rangeX> and <rangeY> allows for searching within a specified area on the given map. The <flag> is a bitmask and has the following possible values:  - 1 = Random cell on the map or from <x>,<y> range. (default)  - 2 = The target should be able to walk to the target tile.  - 4 = There shouldn't be any players around the target tile (use the no_spawn_on_player setting).

**Example:**
```c
	getfreecell("prontera",.@x,.@y); // Find a random empty cell in Prontera and store it within .@x and .@y
	getfreecell("prontera",.@x,.@y,150,150,5,5); // Find a random empty cell on 150,150 (with a range of 5x5) in Prontera and store it within .@x and .@y

```

---

### setwall

<!-- RAG_CHUNK: cmd_setwall -->

**Signature:**
```c
*setwall "<map name>",<x>,<y>,<size>,<dir>,<shootable>,"<name>";
```

---

### delwall

<!-- RAG_CHUNK: cmd_delwall -->

**Signature:**
```c
*delwall "<name>";
```

**Description:**
Creates an invisible wall, an array of "setcell" starting from x,y and doing a line of the given size in the given direction. The difference with setcell is this one update client part too to avoid the glitch problem. Directions are the same as NPC sprite facing directions: 0=north, 1=northwest, 2=west, etc.

---

### checkwall

<!-- RAG_CHUNK: cmd_checkwall -->

**Signature:**
```c
*checkwall "<name>";
```

**Description:**
This command will return true if the wall with the given name exists, false otherwise.

---

### readbook

<!-- RAG_CHUNK: cmd_readbook -->

**Signature:**
```c
*readbook <book id>,<page>;
```

**Description:**
This command will open a book item at the specified page.

---

### open_roulette

<!-- RAG_CHUNK: cmd_open_roulette -->

**Signature:**
```c
*open_roulette( {char_id} )
```

**Description:**
Opens the roulette window for the currently attached character or the character with the given character id.

---

### naviregisterwarp

<!-- RAG_CHUNK: cmd_naviregisterwarp -->

**Signature:**
```c
*naviregisterwarp("<Name of Link>", "<dest_map>", <dest_x>, <dest_y>)
```

**Description:**
Only useful when using the map-server-generator. Registers an extra warp from this npc to the destination map/x/y for the generated client files.

---

### navihide

<!-- RAG_CHUNK: cmd_navihide -->

**Signature:**
```c
*navihide
```

**Description:**
Only useful when using the map-server-generator. Hides this npc and all links from this npc in the navigation generation.

---

### instance_create

<!-- RAG_CHUNK: cmd_instance_create -->

**Signature:**
```c
*instance_create("<instance name>"{,<instance mode>{,<owner id>}});
```

**Description:**
Creates an instance for the <owner id> of <mode>. The instance name, along with all other instance data, is read from 'db/(pre-)re/instance_db.yml'. Upon success, the command generates a unique instance ID, duplicates all listed maps and NPCs, sets the alive time, and triggers the "OnInstanceInit" label in all NPCs inside the instance.

---

### instance_destroy

<!-- RAG_CHUNK: cmd_instance_destroy -->

**Signature:**
```c
*instance_destroy {<instance id>};
```

**Description:**
Destroys instance with the ID <instance id>. If no ID is specified, the instance the script is attached to is used. If that fails, the script will come to a halt. This will also trigger the "OnInstanceDestroy" label in all NPCs inside the instance.

---

### instance_enter

<!-- RAG_CHUNK: cmd_instance_enter -->

**Signature:**
```c
*instance_enter("<instance name>",{<x>,<y>,<char_id>,<instance id>});
```

**Description:**
Warps the attached player to the specified <instance id>. If no ID is specified, the IM_PARTY instance the invoking player is attached to is used.

---

### instance_npcname

<!-- RAG_CHUNK: cmd_instance_npcname -->

**Signature:**
```c
*instance_npcname("<npc name>"{,<instance id>})
```

**Description:**
Returns the unique name of the instanced script. If no ID is specified, the instance the script is attached to is used. If that fails, the script will come to a halt.

---

### instance_mapname

<!-- RAG_CHUNK: cmd_instance_mapname -->

**Signature:**
```c
*instance_mapname("<map name>"{,<instance id>})
```

**Description:**
Returns the unique name of the instanced map. If no instance ID is specified, the instance the script is attached to is used. If that fails, the command returns an empty string instead.

---

### instance_id

<!-- RAG_CHUNK: cmd_instance_id -->

**Signature:**
```c
*instance_id({<instance mode>})
```

**Description:**
Returns the unique instance ID of the given mode.

**Example:**
```c
	// Example with an attached player :
	npctalk "The current instance ID (mode party) from the attached player is : " + instance_id(IM_PARTY);

	// Example with an attached NPC on an instance map :
	npctalk "The current instance ID from the attached NPC is : " + instance_id();

```

---

### instance_warpall

<!-- RAG_CHUNK: cmd_instance_warpall -->

**Signature:**
```c
*instance_warpall "<map name>",<x>,<y>{,<instance id>,{<flag>}};
```

**Description:**
Warps all players in the <instance id> to <map name> to the given coordinates. If no ID is specified, the IM_PARTY instance the invoking player is attached to is used. If that fails, the script will come to a halt.

---

### instance_announce

<!-- RAG_CHUNK: cmd_instance_announce -->

**Signature:**
```c
*instance_announce <instance id>,"<text>",<flag>{,<fontColor>{,<fontType>{,<fontSize>{,<fontAlign>{,<fontY>}}}}};
```

**Description:**
Broadcasts a message to all players in the <instance id> currently residing on an instance map. If 0 is specified for <instance id>, the instance the script is attached to is used.

---

### instance_check_party

<!-- RAG_CHUNK: cmd_instance_check_party -->

**Signature:**
```c
*instance_check_party(<party id>{,<amount>{,<min>{,<max>}}})
```

**Description:**
This function checks if a party meets certain requirements, returning 1 if all conditions are met and 0 otherwise. It will only check online characters. The command returns 0 is the party ID does not exist.

**Example:**
```c
	mes "Your party meets the Memorial Dungeon requirements.",
	mes "All online members are between levels 1-150 and at least two are online.";
	close;
```

---

### instance_check_guild

<!-- RAG_CHUNK: cmd_instance_check_guild -->

**Signature:**
```c
*instance_check_guild(<guild id>{,<amount>{,<min>{,<max>}}})
```

**Description:**
This function checks if a guild meets certain requirements, returning 1 if all conditions are met and 0 otherwise. It will only check online characters.

**Example:**
```c
	mes "Your guild meets the Memorial Dungeon requirements.",
	mes "All online members are between levels 1-150 and at least two are online.";
	close;
```

---

### instance_check_clan

<!-- RAG_CHUNK: cmd_instance_check_clan -->

**Signature:**
```c
*instance_check_clan(<clan id>{,<amount>{,<min>{,<max>}}})
```

**Description:**
This function checks if a clan meets certain requirements, returning 1 if all conditions are met and 0 otherwise. It will only check online characters.

**Example:**
```c
	mes "Your clan meets the Memorial Dungeon requirements.",
	mes "All online members are between levels 1-150 and at least two are online.";
	close;
```

---

### instance_info

<!-- RAG_CHUNK: cmd_instance_info -->

**Signature:**
```c
*instance_info("<instance name>",<info type>{,<instance_db map index>});
```

**Description:**
Returns the specified <info type> of the given <instance name> from the instance database. If the <instance name> is unknown or an invalid <info type> is supplied -1 will be returned.

**Example:**
```c
          If the index is invalid an empty string will be returned.

```

---

### instance_live_info

<!-- RAG_CHUNK: cmd_instance_live_info -->

**Signature:**
```c
*instance_live_info(<info type>{,<instance id>});
```

**Description:**
Returns the specified <info type> of instance attached to the npc or, if an instance ID is specified, of that instance.

**Example:**
```c
			  Return the name of the instance or "" if that fails.
```

---

### instance_list

<!-- RAG_CHUNK: cmd_instance_list -->

**Signature:**
```c
*instance_list(<"map name">{,<instance mode>});
```

**Description:**
Creates the array '.@instance_list' with possible instance IDs for the given <map name> and optional <mode>. Return '.@instance_list' array size.

**Example:**
```c
	// This example assumes that there are several instances on the map of Prontera.
	.@size = instance_list("prontera");
	for ( .@i = 0; .@i < .@size; ++.@i )
		mes instance_mapname("prontera", .@instance_list[.@i]);
	//the output would be a list of all prontera copies that are active in the server.

```

---

### getinstancevar

<!-- RAG_CHUNK: cmd_getinstancevar -->

**Signature:**
```c
*getinstancevar(<variable>,<instance id>);
```

**Description:**
Returns a reference to an instance variable (' prefix) of the specific instance ID. This can only be used to get ' variables.

**Example:**
```c
	// This will set the .@s variable to the value of 'var variable of the specific instance ID.
	set .@s, getinstancevar('var, instance_id(IM_PARTY));

	// This will set the 'var variable of the specific instance ID to 1.
	set getinstancevar('var, instance_id(IM_GUILD)), 1;

```

---

### setinstancevar

<!-- RAG_CHUNK: cmd_setinstancevar -->

**Signature:**
```c
*setinstancevar(<variable>,<value>,<instance id>);
```

**Description:**
This command will set an instance variable to the value that the expression results in. See 'set' command for more information.

**Example:**
```c
	// This will set the 'var variable of the specific instance ID to 9.
	setinstancevar('var, 9, instance_id(IM_GUILD));

```

---

### questinfo

<!-- RAG_CHUNK: cmd_questinfo -->

**Signature:**
```c
*questinfo <Icon>{,<Map Mark Color>{,"<condition>"}};
```

**Description:**
This command should only be used in OnInit/OnInstanceInit labels. Show an emotion on top of a NPC, and optionally, a colored mark in the mini-map like "viewpoint" or "viewpointmap". When a user is doing some action, each NPC is checked for questinfo that has been set on the map. If questinfo is present, it will check if the player fulfill the condition. If he/she does or no condition has been set, the bubble will appear.

**Example:**
```c
	mes "[Test]";
	mes "Hello World.";
	close;

```

---

### questinfo_refresh

<!-- RAG_CHUNK: cmd_questinfo_refresh -->

**Signature:**
```c
*questinfo_refresh {<char_id>};
```

**Description:**
This command refreshes each quest bubble that has been set on the map according to the questinfo condition for the attached/given player.

---

### setquest

<!-- RAG_CHUNK: cmd_setquest -->

**Signature:**
```c
*setquest <ID>{,<char_id>};
```

**Description:**
Place quest of <ID> in the users quest log, the state of which is "active".

---

### completequest

<!-- RAG_CHUNK: cmd_completequest -->

**Signature:**
```c
*completequest <ID>{,<char_id>};
```

**Description:**
Change the state for the given quest <ID> to "complete" and remove from the users quest log.

---

### erasequest

<!-- RAG_CHUNK: cmd_erasequest -->

**Signature:**
```c
*erasequest <ID>{,<char_id>};
```

**Description:**
Remove the quest of the given <ID> from the user's quest log.

---

### changequest

<!-- RAG_CHUNK: cmd_changequest -->

**Signature:**
```c
*changequest <ID>,<ID2>{,<char_id>};
```

**Description:**
Remove quest of the given <ID> from the user's quest log. Add quest <ID2> to the quest log, and the state is "active".

---

### checkquest

<!-- RAG_CHUNK: cmd_checkquest -->

**Signature:**
```c
*checkquest(<ID>{,PLAYTIME|HUNTING{,<char_id>}})
```

**Description:**
If no additional argument supplied, return the state of the quest: 	-1 = Quest not started (not in quest log) 	0  = Quest has been given, but the state is "inactive" 	1  = Quest has been given, and the state is "active" 	2  = Quest completed

---

### isbegin_quest

<!-- RAG_CHUNK: cmd_isbegin_quest -->

**Signature:**
```c
*isbegin_quest(<ID>{,<char_id>})
```

**Description:**
Return the state of the quest: 	0  = Quest not started (not in quest log) 	1  = Quest has been given (state is either "inactive" or "active") 	2  = Quest completed

---

### showevent

<!-- RAG_CHUNK: cmd_showevent -->

**Signature:**
```c
*showevent <icon>{,<mark color>{,<char_id>}}
```

**Description:**
Show an emotion on top of a NPC, and optionally, a colored mark in the mini-map like "viewpoint" or "viewpointmap". This is used to indicate that a NPC has a quest or an event to a certain player.

---

### open_quest_ui

<!-- RAG_CHUNK: cmd_open_quest_ui -->

**Signature:**
```c
*open_quest_ui {<quest ID>,{<char ID>}};
```

**Description:**
Opens the quest UI for the attached player or the given character ID. Use 0 as the quest ID to open the main quest UI. If the quest ID is not 0 then the quest UI is opened to the given quest. If the quest data is not populated in the client LUB then a message will be displayed saying the quest doesn't exist.

---

### waitingroom2bg_single

<!-- RAG_CHUNK: cmd_waitingroom2bg_single -->

**Signature:**
```c
*waitingroom2bg_single(<battle group>,{"<map name>",<x>,<y>{,"<npc name>"}});
```

**Description:**
Adds the first waiting player from the chat room of the given NPC to an existing battleground group. The player will also be warped to the default spawn point of the battle group or to the specified coordinates <x> and <y> on the given <map>. Note: The map need the mapflag MF_BATTLEGROUND otherwise the player is removed from the Battleground team.

---

### waitingroom2bg

<!-- RAG_CHUNK: cmd_waitingroom2bg -->

**Signature:**
```c
*waitingroom2bg("<map name>",<x>,<y>,{"<On Quit Event>","<On Death Event>"{,"<NPC Name>"}});
```

**Description:**
<map name>,<x>,<y> refer to where the "respawn" base is, where the player group will respawn when they die. <On Quit Event> refers to an NPC label that attaches to the character and is run when they relog. (Optional) <On Death Event> refers to an NPC label that attaches to the character and is run when they die. (Optional)

**Example:**
```c
	// Battle Group will be referred to as $@KvM01BG_id1, and when they die, respawn at bat_c01,52,129.
	set $@KvM01BG_id1, waitingroom2bg("bat_c01",52,129,"KvM01_BG::OnGuillaumeQuit","KvM01_BG::OnGuillaumeDie");
	end;

```

---

### bg_create

<!-- RAG_CHUNK: cmd_bg_create -->

**Signature:**
```c
*bg_create("<map name>",<x>,<y>{,"<On Quit Event>","<On Death Event>"});
```

**Description:**
Creates an instance of battleground battle group that can be used with other battleground commands.

---

### bg_join

<!-- RAG_CHUNK: cmd_bg_join -->

**Signature:**
```c
*bg_join(<battle group>,{"<map name>",{<x>,<y>{,<char id>}});
```

**Description:**
Adds an attached player or <char id> if specified to an existing battleground group. The player will also be warped to the default spawn point of the battle group or to the specified coordinates <x> and <y> on the given <map>. Note: The map need the mapflag MF_BATTLEGROUND otherwise the player is removed from the Battleground team.

---

### bg_team_setxy

<!-- RAG_CHUNK: cmd_bg_team_setxy -->

**Signature:**
```c
*bg_team_setxy <Battle Group ID>,<x>,<y>;
```

**Description:**
Updates the respawn point of the given Battle Group to x,y on the same map. <Battle Group ID> can be retrieved using getcharid(4).

**Example:**
```c
	bg_team_setxy getcharid(4),56,212;
	mapannounce "bat_a01", "Group [1] has taken the work shop, and will now respawn there.",bc_map,"0xFFCE00";
	end;

```

---

### bg_reserve

<!-- RAG_CHUNK: cmd_bg_reserve -->

**Signature:**
```c
*bg_reserve("<battleground_map_name>"{,<ended>});
```

**Description:**
Reserves a Battleground map for the Battleground UI System. When a map is booked it prevents another similar queue from being created and will allow players to join an active Battlegrounds event.

---

### bg_unbook

<!-- RAG_CHUNK: cmd_bg_unbook -->

**Signature:**
```c
*bg_unbook("<battleground_map_name>");
```

**Description:**
Removes a Battleground map for the Battleground UI System. When a map is unbooked it allows a queue to be created.

---

### bg_desert

<!-- RAG_CHUNK: cmd_bg_desert -->

**Signature:**
```c
*bg_desert({<char_id>});
```

**Description:**
Same as 'bg_leave' but slaps the player with a deserter status so they can't enter another queue for the time defined in battleground_db (10 minutes by default).

---

### bg_warp

<!-- RAG_CHUNK: cmd_bg_warp -->

**Signature:**
```c
*bg_warp <Battle Group>,"<map name>",<x>,<y>;
```

**Description:**
Similar to the 'warp' command. Places all members of <Battle Group> at the specified map and coordinates.

**Example:**
```c
	//place the battle group one for Tierra Gorge at starting position.
	bg_warp $@TierraBG1_id1,"bat_a01",352,342;
	end;

```

---

### bg_monster

<!-- RAG_CHUNK: cmd_bg_monster -->

**Signature:**
```c
*bg_monster <Battle Group>,"<map name>",<x>,<y>,"<name to show>",<mob id>,"<event label>";
```

---

### bg_monster

<!-- RAG_CHUNK: cmd_bg_monster -->

**Signature:**
```c
*bg_monster(<Battle Group>,"<map name>",<x>,<y>,"<name to show>",<mob id>,"<event label>");
```

**Description:**
Similar to the 'monster' command. Spawns a monster with allegiance to the given Battle Group. Does not allow for the summoning of multiple monsters. Monsters are similar to those in War of Emperium, in that the specified Battle Group is considered friendly.

**Example:**
```c
	// It can be used in two different ways.
	bg_monster $@TierraBG1_id2,"bat_a01",167,50,"Food Depot",1910,"Feed Depot#1::OnMyMobDead";
	end;

	// Alternatively, you can set an ID for the monster using "set".
	// This becomes useful when used with the command below.
	set $@Guardian_3, bg_monster($@TierraBG1_id2,"bat_a01",268,204,"Guardian",1949,"NPCNAME::OnMyMobDead");
	end;

```

---

### bg_monster_set_team

<!-- RAG_CHUNK: cmd_bg_monster_set_team -->

**Signature:**
```c
*bg_monster_set_team <GID>,<Battle Group>;
```

**Description:**
This command will change the allegiance if a monster in a battle ground. GID can be set when spawning the monster via the 'bg_monster' command.

**Example:**
```c
	end;

```

---

### bg_leave

<!-- RAG_CHUNK: cmd_bg_leave -->

**Signature:**
```c
*bg_leave {<char_id>};
```

**Description:**
Removes attached player from their Battle Group.

---

### bg_destroy

<!-- RAG_CHUNK: cmd_bg_destroy -->

**Signature:**
```c
*bg_destroy <Batte Group>;
```

**Description:**
Destroys the Battle Group created for that battle ground.

---

### areapercentheal

<!-- RAG_CHUNK: cmd_areapercentheal -->

**Signature:**
```c
*areapercentheal "<map name>",<x1>,<y1>,<x2>,<y2>,<hp>,<sp>;
```

**Description:**
Restores a percentage of the maximum HP/SP of players within a defined area. This is primarily used in battleground scripts, but is not limited to them.

**Example:**
```c
	areapercentheal "bat_a01",52,208,61,217,100,100;
	end;

```

---

### bg_get_data

<!-- RAG_CHUNK: cmd_bg_get_data -->

**Signature:**
```c
*bg_get_data(<Battle Group>,<type>);
```

**Description:**
Retrieves data related to given Battle Group. Type can be one of the following:

---

### bg_getareausers

<!-- RAG_CHUNK: cmd_bg_getareausers -->

**Signature:**
```c
*bg_getareausers(<Battle Group>,"<map name>",<x0>,<y0>,<x1>,<y1>);
```

**Description:**
Retrieves the amount of players belonging to the given Battle Group on the given map within the specified rectangular area.

---

### bg_updatescore

<!-- RAG_CHUNK: cmd_bg_updatescore -->

**Signature:**
```c
*bg_updatescore "<map name>",<Guillaume Score>,<Croix Score>;
```

**Description:**
This command will force the update of the displayed scoreboard. It is only usable when the map is defined as a Type 2 Battleground: mapflag	<map name>	battleground	2

---

### bg_info

<!-- RAG_CHUNK: cmd_bg_info -->

**Signature:**
```c
*bg_info("<battleground name>", <type>);
```

**Description:**
Retrieves data related to given <battleground name> from the database. Requires feature.bgqueue to be enabled. <Type> can be one of the following:

---

### bpet

<!-- RAG_CHUNK: cmd_bpet -->

**Signature:**
```c
*bpet;
```

---

### birthpet

<!-- RAG_CHUNK: cmd_birthpet -->

**Signature:**
```c
*birthpet;
```

**Description:**
This command opens up a pet hatching window on the client connected to the invoking character. It is used in item script for the pet incubators and will let the player hatch an owned egg. If the character has no eggs, it will just open up an empty incubator window. This is still usable outside item scripts.

---

### pet

<!-- RAG_CHUNK: cmd_pet -->

**Signature:**
```c
*pet {<item_id>{,flag}};
```

---

### catchpet

<!-- RAG_CHUNK: cmd_catchpet -->

**Signature:**
```c
*catchpet {<item_id>{,flag}};
```

**Description:**
This command is used in all the item scripts for taming items. Running this command will make the pet catching cursor appear on the client of the invoking character and the player can then attempt to catch a monster.

---

### makepet

<!-- RAG_CHUNK: cmd_makepet -->

**Signature:**
```c
*makepet <pet id>;
```

**Description:**
This command will create a pet egg and put it in the invoking character's inventory. The kind of pet is specified by pet ID numbers listed in 'db/(pre-)re/pet_db.yml'. The egg is created exactly as if the character just successfully caught a pet in the normal way.

---

### getpetinfo

<!-- RAG_CHUNK: cmd_getpetinfo -->

**Signature:**
```c
*getpetinfo(<type>{,<char_id>})
```

**Description:**
This function will return pet information for the pet the invoking character currently has active. Valid types are:

**Example:**
```c
	mes "[Vet]";
	mes "Your pet + " getpetinfo(PETINFO_NAME);
	if (getpetinfo(PETINFO_INTIMATE) < PET_INTIMATE_LOYAL)
		mes "has some growing to do on you!";
	else
		mes "seems to love you very much!";
	close;

```

---

### petskillbonus

<!-- RAG_CHUNK: cmd_petskillbonus -->

**Signature:**
```c
*petskillbonus <bonus type>,<value>,<duration>,<delay>;
```

**Description:**
This command will make the pet give a bonus to the owner's stat in certain duration in seconds and will be repeated for certain delay in seconds.

---

### petrecovery

<!-- RAG_CHUNK: cmd_petrecovery -->

**Signature:**
```c
*petrecovery <status type>,<delay>;
```

**Description:**
This command will make the pet cure a specified status condition. The curing actions will occur once every Delay seconds. For a full list of status conditions that can be cured, see the list of 'SC_' status condition constants in 'src/map/script_constants.hpp'.

---

### petloot

<!-- RAG_CHUNK: cmd_petloot -->

**Signature:**
```c
*petloot <max items>;
```

**Description:**
This command will turn on pet looting, with a maximum number of items to loot specified. Pet will store items and return them when the maximum is reached or when pet performance is activated.

---

### petskillsupport

<!-- RAG_CHUNK: cmd_petskillsupport -->

**Signature:**
```c
*petskillsupport <skill id>,<skill level>,<delay>,<percent hp>,<percent sp>;
```

---

### petskillsupport

<!-- RAG_CHUNK: cmd_petskillsupport -->

**Signature:**
```c
*petskillsupport "<skill name>",<skill level>,<delay>,<percent hp>,<percent sp>;
```

**Description:**
This will make the pet use a specified support skill on the owner whenever the HP and SP are below the given percent values, with a specified delay time between activations. The skill numbers are as per 'db/(pre-)re/skill_db.yml'.

---

### petskillattack

<!-- RAG_CHUNK: cmd_petskillattack -->

**Signature:**
```c
*petskillattack <skill id>,<skill level>,<rate>,<bonusrate>;
```

---

### petskillattack

<!-- RAG_CHUNK: cmd_petskillattack -->

**Signature:**
```c
*petskillattack "<skill name>",<skill level>,<rate>,<bonusrate>;
```

---

### petskillattack2

<!-- RAG_CHUNK: cmd_petskillattack2 -->

**Signature:**
```c
*petskillattack2 <skill id>,<damage>,<number of attacks>,<rate>,<bonusrate>;
```

---

### petskillattack2

<!-- RAG_CHUNK: cmd_petskillattack2 -->

**Signature:**
```c
*petskillattack2 "<skill name>",<damage>,<number of attacks>,<rate>,<bonusrate>;
```

**Description:**
These two commands will make the pet cast an attack skill on the enemy the pet's owner is currently fighting. Skill IDs and levels are as per 'petskillsupport'. 'petskillattack2' will make the pet cast the skill with a fixed amount of damage inflicted and the specified number of attacks.

---

### petautobonus

<!-- RAG_CHUNK: cmd_petautobonus -->

**Signature:**
```c
*petautobonus <bonus script>,<rate>,<duration>{,<flag>,{<other script>}};
```

---

### petautobonus2

<!-- RAG_CHUNK: cmd_petautobonus2 -->

**Signature:**
```c
*petautobonus2 <bonus script>,<rate>,<duration>{,<flag>,{<other script>}};
```

---

### petautobonus3

<!-- RAG_CHUNK: cmd_petautobonus3 -->

**Signature:**
```c
*petautobonus3 <bonus script>,<rate>,<duration>,<skill id>,{<other script>};
```

---

### petautobonus3

<!-- RAG_CHUNK: cmd_petautobonus3 -->

**Signature:**
```c
*petautobonus3 <bonus script>,<rate>,<duration>,"<skill name>",{<other script>};
```

**Description:**
See 'autobonus' for more details.

---

### homevolution

<!-- RAG_CHUNK: cmd_homevolution -->

**Signature:**
```c
*homevolution;
```

**Description:**
This command will try to evolve the current player's homunculus. If it doesn't work, the /swt emotion is shown.

---

### morphembryo

<!-- RAG_CHUNK: cmd_morphembryo -->

**Signature:**
```c
*morphembryo;
```

**Description:**
This command will try to put the invoking player's Homunculus in an uncallable state, required for mutation into a Homunculus S. The player will also receive a Strange Embryo (ID 6415) in their inventory if successful, which is deleted upon mutation.

---

### hommutate

<!-- RAG_CHUNK: cmd_hommutate -->

**Signature:**
```c
*hommutate {<ID>};
```

**Description:**
This command will try to mutate the invoking player's Homunculus into a Homunculus S. The Strange Embryo (ID 6415) is deleted upon success.

---

### checkhomcall

<!-- RAG_CHUNK: cmd_checkhomcall -->

**Signature:**
```c
*checkhomcall()
```

**Description:**
This function checks if the attached player's Homunculus is active, and will return the following values:  -1: The player has no Homunculus.   0: The player's Homunculus is active.   1: The player's Homunculus is vaporized.   2: The player's Homunculus is in morph state.

---

### gethominfo

<!-- RAG_CHUNK: cmd_gethominfo -->

**Signature:**
```c
*gethominfo(<type>{,<char_id>})
```

**Description:**
This function will return Homunculus information for the Homunculus of the invoking character, regardless of its vaporize state. It returns zero or "null" if the player does not own a Homunculus.

---

### homshuffle

<!-- RAG_CHUNK: cmd_homshuffle -->

**Signature:**
```c
*homshuffle;
```

**Description:**
This will recalculate the homunculus stats according to its level, of the current invoking character.

---

### addhomintimacy

<!-- RAG_CHUNK: cmd_addhomintimacy -->

**Signature:**
```c
*addhomintimacy <amount>{,<char_id>};
```

**Description:**
Increase or decrease a homunculus' intimacy value by the given <amount>. 100000 is full loyalty. Fails silently when no players are attached or if the player has no homunculus.

---

### mercenary_create

<!-- RAG_CHUNK: cmd_mercenary_create -->

**Signature:**
```c
*mercenary_create <class>,<contract time>;
```

**Description:**
This command summons a mercenary for a given time (in milliseconds). For a list of all available classes, see 'db/mercenary_db.txt'.

---

### mercenary_delete

<!-- RAG_CHUNK: cmd_mercenary_delete -->

**Signature:**
```c
*mercenary_delete {<char id>{,<reply>}};
```

**Description:**
This command removes the mercenary from a player. The parameter 'reply' can be one of the following values:

---

### mercenary_heal

<!-- RAG_CHUNK: cmd_mercenary_heal -->

**Signature:**
```c
*mercenary_heal <hp>,<sp>;
```

**Description:**
This command works like 'heal', but affects the mercenary of the currently attached character.

---

### mercenary_sc_start

<!-- RAG_CHUNK: cmd_mercenary_sc_start -->

**Signature:**
```c
*mercenary_sc_start <type>,<tick>,<val1>;
```

**Description:**
This command works like 'sc_start', but affects the mercenary of the currently attached character.

---

### mercenary_get_calls

<!-- RAG_CHUNK: cmd_mercenary_get_calls -->

**Signature:**
```c
*mercenary_get_calls(<guild>);
```

---

### mercenary_set_calls

<!-- RAG_CHUNK: cmd_mercenary_set_calls -->

**Signature:**
```c
*mercenary_set_calls <guild>,<value>;
```

**Description:**
Sets or gets the mercenary calls value for given guild for currently attached character. Guild can be one or the following constants:

---

### mercenary_get_faith

<!-- RAG_CHUNK: cmd_mercenary_get_faith -->

**Signature:**
```c
*mercenary_get_faith(<guild>);
```

---

### mercenary_set_faith

<!-- RAG_CHUNK: cmd_mercenary_set_faith -->

**Signature:**
```c
*mercenary_set_faith <guild>,<value>;
```

**Description:**
Sets or gets the mercenary faith value for given guild for currently attached character. Guild can be one or the following constants:

---

### getmercinfo

<!-- RAG_CHUNK: cmd_getmercinfo -->

**Signature:**
```c
*getmercinfo(<type>{,<char id>});
```

**Description:**
Retrieves information about mercenary of the currently attached character. If char id is given, the information of that character is retrieved instead. Type specifies what information to retrieve and can be one of the following:

---

### getpartyname

<!-- RAG_CHUNK: cmd_getpartyname -->

**Signature:**
```c
*getpartyname(<party id>)
```

**Description:**
This function will return the name of a party that has the specified ID number. If there is no such party ID, "null" will be returned.

---

### getpartymember

<!-- RAG_CHUNK: cmd_getpartymember -->

**Signature:**
```c
*getpartymember <party id>{,<type>{,<array_variable>}};
```

**Description:**
This command will find all members of a specified party and returns their names (or character id or account id depending on the value of "type") into an array of temporary global variables. There's actually quite a few commands like this which will fill a special variable with data upon execution and not do anything else.

**Example:**
```c
                     names of these party members
                     (only set when type is 0 or not specified)

```

---

### getpartyleader

<!-- RAG_CHUNK: cmd_getpartyleader -->

**Signature:**
```c
*getpartyleader(<party id>{,<type>})
```

**Description:**
This function returns some information about the given party-id's leader. When type is omitted, the default information retrieved is the leader's name. Possible types are:

---

### is_party_leader

<!-- RAG_CHUNK: cmd_is_party_leader -->

**Signature:**
```c
*is_party_leader({<party ID>})
```

**Description:**
This command will return true if the player attached to the script is the leader of his/her party, or, if a party ID is specified, of that party.

---

### party_create

<!-- RAG_CHUNK: cmd_party_create -->

**Signature:**
```c
*party_create("<party name>"{,<character id>{,<item share>,<item share type>}});
```

**Description:**
Organizes a party with the attached or specified character as leader. If successful, the command returns 1 and sets the global temporary variable "$@party_create_id" to the ID of the party created.

---

### party_destroy

<!-- RAG_CHUNK: cmd_party_destroy -->

**Signature:**
```c
*party_destroy(<party id>);
```

**Description:**
Disbands a party. The command returns 1 upon success and 0 upon failure.

---

### party_addmember

<!-- RAG_CHUNK: cmd_party_addmember -->

**Signature:**
```c
*party_addmember(<party id>,<character id>);
```

**Description:**
Adds a player to an existing party.

---

### party_delmember

<!-- RAG_CHUNK: cmd_party_delmember -->

**Signature:**
```c
*party_delmember({<character id>,<party id>});
```

**Description:**
Removes a player from his/her party. If no player is specified, the command will run for the invoking player. If that player is the only party member remaining, the party will be disbanded.

---

### party_changeleader

<!-- RAG_CHUNK: cmd_party_changeleader -->

**Signature:**
```c
*party_changeleader(<party id>,<character id>);
```

**Description:**
Transfers leadership of a party to the specified character.

---

### party_changeoption

<!-- RAG_CHUNK: cmd_party_changeoption -->

**Signature:**
```c
*party_changeoption(<party id>,<option>,<flag>);
```

**Description:**
Changes a party option.

---

### opendressroom

<!-- RAG_CHUNK: cmd_opendressroom -->

**Signature:**
```c
*opendressroom({<char_id>});
```

**Description:**
This will open the Dress Room window on the client connected to the invoking character.

---

### navigateto

<!-- RAG_CHUNK: cmd_navigateto -->

**Signature:**
```c
*navigateto("<map>"{,<x>,<y>,<flag>,<hide_window>,<monster_id>,<char_id>});
```

**Description:**
Generates a navigation for attached or specified character. Requires client 2011-10-10aRagEXE or newer.

---

### hateffect

<!-- RAG_CHUNK: cmd_hateffect -->

**Signature:**
```c
*hateffect(<hat effect id>,<state>{,<target id>});
```

**Description:**
Sets a Hat Effect onto the unit specified by <target id>. If no ID is specified, the attached unit will be used. <state> can be true to enable or false to disable.

**Example:**
```c
	hateffect HAT_EF_FLUTTER_BUTTERFLY, true; // Enables the hat effect on attached player

	hateffect HAT_EF_FLUTTER_BUTTERFLY, true, getcharid(3); // Enables the hat effect on attached player
	hateffect HAT_EF_FLUTTER_BUTTERFLY, true, getnpcid(0); // Enables the hat effect on invoking NPC

	monster "prontera",50,50,"--en--",1002,1;
	hateffect HAT_EF_FLUTTER_BUTTERFLY, true, $@mobid; // Enables the hat effect on a spawned mob

```

---

### has_hateffect

<!-- RAG_CHUNK: cmd_has_hateffect -->

**Signature:**
```c
*has_hateffect(<hat effect id>{,<GID>});
```

**Description:**
Returns true if the unit <GID> already has the hat effect enabled, and false otherwise. If no GID is specified, the attached unit will be used.

---

### getrandomoptinfo

<!-- RAG_CHUNK: cmd_getrandomoptinfo -->

**Signature:**
```c
*getrandomoptinfo(<type>);
```

**Description:**
Returns value of an attribute of current random option.

---

### getequiprandomoption

<!-- RAG_CHUNK: cmd_getequiprandomoption -->

**Signature:**
```c
*getequiprandomoption(<equipment index>,<index>,<type>{,<char id>});
```

**Description:**
Returns value of an attribute of a random option on an equipped item.

---

### setrandomoption

<!-- RAG_CHUNK: cmd_setrandomoption -->

**Signature:**
```c
*setrandomoption(<equipment slot>,<index>,<id>,<value>,<param>{,<char id>});
```

**Description:**
Sets <index+1>th random option for equipment equipped at <equipment slot> to <id>, <value> and <param>.

---

### randomoptgroup

<!-- RAG_CHUNK: cmd_randomoptgroup -->

**Signature:**
```c
*randomoptgroup <random option group ID>;
```

**Description:**
This command fills the following arrays with the results of a random option group. The random option group IDs are specified in 'db/(pre-)re/item_randomopt_group.yml'.

**Example:**
```c
	// Fill the arrays using the random option group ID 5 (group used for Crimson weapons).
	randomoptgroup(5);

	// Create a +9 Crimson Dagger [2] with the Group 5 applied
	getitem3 28705,1,1,9,0,0,0,0,0,.@opt_id,.@opt_value,.@opt_param;

```

---

### clan_join

<!-- RAG_CHUNK: cmd_clan_join -->

**Signature:**
```c
*clan_join(<clan id>{,<char id>});
```

**Description:**
The attached player joins the clan with the <clan id>. On a successful join, true is returned, else false if the join failed. If <char id> is specified, the specified player is used rather than the attached one.

---

### clan_leave

<!-- RAG_CHUNK: cmd_clan_leave -->

**Signature:**
```c
*clan_leave({<char id>});
```

**Description:**
The attached player will leave their clan. On a successful leave, true is returned, else false if the leave failed. If <char id> is specified, the specified player is used rather than the attached one.

---

### itemlink

<!-- RAG_CHUNK: cmd_itemlink -->

**Signature:**
```c
*itemlink(<item_id>{,<refine>{,<card0>{,<card1>{,<card2>{,<card3>,{<enchantgrade>{,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>}}}}}}});
```

**Description:**
Generates an item link string for an item that can be used for npctalk, message, dispbottom, and broadcast commands. The result is a clickable-item name just like SHIFT+Click from a player's inventory/cart/equipment window. This command can be used with mes but the item name will not be clickable. You should use script command "mesitemlink" for displaying item links in mes dialogues, if the client supports them. 

**Example:**
```c
	npctalk "Knife [3] : "+itemlink(1201)+"";
	npctalk "+16 Knife [3] : "+itemlink(1201,16)+"";
	npctalk "+13 BXB Bapho+VR+EA2+EA1 : "+itemlink(18110,13,4147,4407,4833,4832)+"";
	setarray .@opt_ids[0],RDMOPT_VAR_ATKPERCENT,RDMOPT_VAR_ATKPERCENT,RDMOPT_VAR_ATTMPOWER,0,0;
	setarray .@opt_values[0],3,5,20,0,0;
	setarray .@opt_params[0],0,0,0,0,0;
	npctalk "+13 BXB Bapho+VR+EA2+EA1 + 3 Options : "+itemlink(18110,13,4147,4407,4833,4832,0,.@opt_ids,.@opt_values,.@opt_params)+"";


```

---

### mesitemlink

<!-- RAG_CHUNK: cmd_mesitemlink -->

**Signature:**
```c
*mesitemlink(<item_id>{,<use_brackets>{,<display_name>});
```

---

### mesitemlink

<!-- RAG_CHUNK: cmd_mesitemlink -->

**Signature:**
```c
*mesitemlink(<"item_name">{,<use_brackets>{,<display_name>});
```

**Description:**
Generates an itemlink string for an item and can be used with NPC's mes command. The NPC message will show the item's name which will be clickable and opens the item description client side. By default <use_brackets> is true which surrounds the link with brackets. Send false to disable. By default the link will be created with the name of the item stored in the item database, but in some cases it might be necessary to overwrite the <display_name> with something else.

**Example:**
```c
	mes mesitemlink( 1201 ); // Will display "[Knife]" and will be clickable. If clicked it opens the description for Knife [3]
	mes mesitemlink( "Knife" ); // Will display "[Knife]" and will be clickable. If clicked it opens the description for Knife [3]
	mes "Bring me a " + mesitemlink( 1201 ) + "."; // Will display "Bring me a [Knife]." and "[Knife]" will be clickable.
	mes "Bring me a " + mesitemlink( 1201, false ) + "."; // Will display "Bring me a Knife." and "Knife" will be clickable.
	mes "Bring me a " + mesitemlink( 1201, true, "Super cutting knife" ) + "."; // Will display "Bring me a [Super cutting knife]." and "[Super cutting knife]" will be clickable.

```

---

### mesitemicon

<!-- RAG_CHUNK: cmd_mesitemicon -->

**Signature:**
```c
*mesitemicon(<item_id>{,<display_name>});
```

---

### mesitemicon

<!-- RAG_CHUNK: cmd_mesitemicon -->

**Signature:**
```c
*mesitemicon(<"item_name">{,<display_name>});
```

**Description:**
Generates an itemicon string for an item and can be used with NPC's mes command. The NPC message will show the item's icon which will be clickable and opens the item description client side.

**Example:**
```c
	mes mesitemicon( 1201 ); // Will display a Knife icon and will be clickable. If clicked it opens the description for Knife [3]
	mes mesitemicon( "Knife" ); // Will display a Knife icon and will be clickable. If clicked it opens the description for Knife [3]

```

---

### channel_create

<!-- RAG_CHUNK: cmd_channel_create -->

**Signature:**
```c
*channel_create "<chname>","<alias>"{,"<password>"{<option>{,<delay>{,<color>{,<char_id>}}}}};
```

**Description:**
Creates a public channel with <chname> as the channel name. To protect the channel, use <password> or write "null" to create it without a password. Channel name must start with '#' and cannot be the same as the map or ally channel names.

**Example:**
```c
	CHAN_OPT_BASE		    - Default option including CHAN_OPT_ANNOUNCE_SELF|CHAN_OPT_MSG_DELAY|CHAN_OPT_CAN_CHAT|CHAN_OPT_CAN_LEAVE
	CHAN_OPT_ANNOUNCE_SELF  - Show info for player itself if player has joined/leaves the channel
	CHAN_OPT_ANNOUNCE_JOIN  - Display message when player is joining the channel
	CHAN_OPT_ANNOUNCE_LEAVE - Display message when player is leaving the channel
	CHAN_OPT_MSG_DELAY	    - Enable chat delay for the channel
	CHAN_OPT_COLOR_OVERRIDE - Player's unique font color will override channel's color
	CHAN_OPT_CAN_CHAT	    - Player can chat in the channel
	CHAN_OPT_CAN_LEAVE	    - Player can leave the channel
	CHAN_OPT_AUTOJOIN	    - Players will auto join the channel at login

```

---

### channel_join

<!-- RAG_CHUNK: cmd_channel_join -->

**Signature:**
```c
*channel_join "<channel_name>"{, <char_id>};
```

**Description:**
Join an existing channel. The command returns 0 upon success, and these values upon failure:  -1 : Invalid channel or player  -2 : Player already in channel  -3 : Player banned  -4 : Reached max limit

---

### channel_setopt

<!-- RAG_CHUNK: cmd_channel_setopt -->

**Signature:**
```c
*channel_setopt "<chname>",<option>,<value>;
```

**Description:**
Set option for the channel. Use 1 in <value> to set it, or 0 to unset. The <option> values are the same as the 'channel_create' options.

**Example:**
```c
	// Example to set delay
	channel_setopt("#global",CHAN_OPT_MSG_DELAY,5000);

```

---

### channel_getopt

<!-- RAG_CHUNK: cmd_channel_getopt -->

**Signature:**
```c
*channel_getopt "<chname>",<option>;
```

**Description:**
Get option value for the channel. The <option> values are the same as the 'channel_create' options. Returns true or false except for CHAN_OPT_MSG_DELAY which returns an integer.

**Example:**
```c
	// Example to get the delay
	.delay = channel_getopt("#global",CHAN_OPT_MSG_DELAY);

```

---

### channel_setcolor

<!-- RAG_CHUNK: cmd_channel_setcolor -->

**Signature:**
```c
*channel_setcolor "<chname>",<color>;
```

**Description:**
To change channel color. <color> uses hex RGB values.

---

### channel_setpass

<!-- RAG_CHUNK: cmd_channel_setpass -->

**Signature:**
```c
*channel_setpass "<chname>","<password>";
```

**Description:**
To set, unset, or change password of a channel. Use "null" to remove the password.

---

### channel_setgroup

<!-- RAG_CHUNK: cmd_channel_setgroup -->

**Signature:**
```c
*channel_setgroup "<chname>",<group_id>{,...,<group_id>};
```

---

### channel_setgroup2

<!-- RAG_CHUNK: cmd_channel_setgroup2 -->

**Signature:**
```c
*channel_setgroup2 "<chname>",<array_of_groups>;
```

**Description:**
Set group restriction for a channel. Only player with matching <group_id> are allowed to to join the channel.

**Example:**
```c
	// Example 1: Remove groups
	channel_setgroup("#event",0);

	// Example 2: Multiple values
	channel_setgroup("#vip",2,5);

	// Example 3: Using array
	setarray .@staffs[0],2,3,4,10,99;
	channel_setgroup("#staff",.@staffs);

```

---

### channel_chat

<!-- RAG_CHUNK: cmd_channel_chat -->

**Signature:**
```c
*channel_chat "<chname>","<message>"{,<color>};
```

**Description:**
Sends message to the channel. Returns 1 on success.

**Example:**
```c
	// Example if channel doesn't have alias
	channel_chat(#rathena,"Hello World!"); // #rathena Hello World!

	// Example if channel has alias
	channel_chat(#rathena,"Hello World!"); // [rAthena] Hello World!

```

---

### channel_ban

<!-- RAG_CHUNK: cmd_channel_ban -->

**Signature:**
```c
*channel_ban "<chname>",<char_id>;
```

**Description:**
Ban player from a public or private channel. Channel's owner or group with PC_PERM_CHANNEL_ADMIN cannot be banned. Returns 1 on success.

---

### channel_unban

<!-- RAG_CHUNK: cmd_channel_unban -->

**Signature:**
```c
*channel_unban "<chname>",<char_id>;
```

**Description:**
Unban player from a public or private channel. Returns 1 on success.

---

### channel_kick

<!-- RAG_CHUNK: cmd_channel_kick -->

**Signature:**
```c
*channel_kick "<chname>",<char_id>;
```

---

### channel_kick

<!-- RAG_CHUNK: cmd_channel_kick -->

**Signature:**
```c
*channel_kick "<chname>","<char_name>";
```

**Description:**
Kick player from a public or private channel. Channel's owner or group with PC_PERM_CHANNEL_ADMIN cannot be kicked. Returns 1 on success.

---

### channel_delete

<!-- RAG_CHUNK: cmd_channel_delete -->

**Signature:**
```c
*channel_delete "<chname>";
```

**Description:**
Delete an existing public or private channel. Cannot delete ally or local map channel. Returns 0 on success.

---

### achievementadd

<!-- RAG_CHUNK: cmd_achievementadd -->

**Signature:**
```c
*achievementadd(<achievement id>{,<char id>})
```

**Description:**
This function will add an achievement to the player's log for the attached player or the supplied <char id>. The objective requirements are not ignored when using this function. Returns true on success and false on failure.

---

### achievementremove

<!-- RAG_CHUNK: cmd_achievementremove -->

**Signature:**
```c
*achievementremove(<achievement id>{,<char id>})
```

**Description:**
This function will remove an achievement from the player's log for the attached player or the supplied <char id>. Returns true on success and false on failure.

---

### achievementinfo

<!-- RAG_CHUNK: cmd_achievementinfo -->

**Signature:**
```c
*achievementinfo(<achievement id>,<type>{,<char id>})
```

**Description:**
This function will return the specified <type> value for an achievement of the attached player or the supplied <char id>. If the player doesn't have the achievement active (no progress has been made): if the achievement doesn't exist -1 will be returned, or -2 will be returned on any other error such as an invalid <type>.

---

### achievementcomplete

<!-- RAG_CHUNK: cmd_achievementcomplete -->

**Signature:**
```c
*achievementcomplete(<achievement id>{,<char id>})
```

**Description:**
This function will complete an achievement for the attached player or the supplied <char id>. The objective requirements are ignored when using this function. Returns true on success and false on failure.

---

### achievementexists

<!-- RAG_CHUNK: cmd_achievementexists -->

**Signature:**
```c
*achievementexists(<achievement id>{,<char id>});
```

**Description:**
This function will return if the achievement exists on the player or the supplied <char id> and is completed. Returns true on success and false on failure.

---

### achievementupdate

<!-- RAG_CHUNK: cmd_achievementupdate -->

**Signature:**
```c
*achievementupdate(<achievement id>,<type>,<value>{,<char id>})
```

**Description:**
This function will update an achievement's value for an achievement of the attached player or the supplied <char id>. If the player does not have the achievement active (no progress has been made) it will be added to the player's log first before updating the <type> value. Returns true on success and false on failure.

---

### addfame

<!-- RAG_CHUNK: cmd_addfame -->

**Signature:**
```c
*addfame(<amount>,{,<char id>})
```

**Description:**
Increases the fame of the attached player or the supplied <char id> by the <amount> given. Note: Only works with classes that use the ranking system.

---

### getfame

<!-- RAG_CHUNK: cmd_getfame -->

**Signature:**
```c
*getfame({<char id>})
```

**Description:**
Gets the fame points of the attached player or the supplied <char id>. Note: Only works with classes that use the ranking system.

---

### getfamerank

<!-- RAG_CHUNK: cmd_getfamerank -->

**Signature:**
```c
*getfamerank({<char id>})
```

**Description:**
Returns fame rank (start from 1 to MAX_FAME_LIST), else 0. Note: Only works with classes that use the ranking system.

---

### isdead

<!-- RAG_CHUNK: cmd_isdead -->

**Signature:**
```c
*isdead({<account id>})
```

**Description:**
Returns true if the player is dead else false.

---

### has_autoloot

<!-- RAG_CHUNK: cmd_has_autoloot -->

**Signature:**
```c
*has_autoloot({<char_id>});
```

**Description:**
This command checks whether a player configured autoloot. Returns current autoloot value on success.

---

### autoloot

<!-- RAG_CHUNK: cmd_autoloot -->

**Signature:**
```c
*autoloot({<rate>{, <char_id>}});
```

**Description:**
This command sets the rate of autoloot. If no rate is provided and the user has autoloot disabled it will default to 10000 = 100% (enabled) or if the user has autoloot enabled it will default to 0 = 0% (disabled). Returns true on success and false on failure.

**Example:**
```c
    autoloot();      // toggle on/off depend on existing autoloot
    autoloot(0);     //   0.00% or off
    autoloot(100);   //   1.00%
    autoloot(3333);  //  33.33%
    autoloot(10000); // 100.00%

```

---

### setdialogalign

<!-- RAG_CHUNK: cmd_setdialogalign -->

**Signature:**
```c
*setdialogalign(<align>);
```

**Description:**
Set vertical or horizontal align in NPC dialog. Valid aligns: - horizontal align:   DIALOG_ALIGN_LEFT   DIALOG_ALIGN_CENTER   DIALOG_ALIGN_RIGHT

---

### setdialogsize

<!-- RAG_CHUNK: cmd_setdialogsize -->

**Signature:**
```c
*setdialogsize(<width>, <height>)
```

**Description:**
Set size for NPC dialog in pixels.

---

### setdialogpos

<!-- RAG_CHUNK: cmd_setdialogpos -->

**Signature:**
```c
*setdialogpos(<x>, <y>)
```

**Description:**
Set position for NPC dialog in pixels.

---

### setdialogpospercent

<!-- RAG_CHUNK: cmd_setdialogpospercent -->

**Signature:**
```c
*setdialogpospercent(<x>, <y>)
```

**Description:**
Set position for NPC dialog in screen size percent.

---

