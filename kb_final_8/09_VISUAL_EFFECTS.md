# rAthena Visual Effects Reference (EF_* Constants)
<!-- RAG_CHUNK: VISUAL_EFFECTS_INDEX -->

> **Version**: 15.0 | **Effects**: 967 | **RAG Chunks**: 968

Complete reference for client-side visual and sound effects. Use with `specialeffect`, `specialeffect2`, or `@effect` command.

## Quick Usage

```c
// In NPC scripts
specialeffect EF_HEAL;           // Effect on NPC
specialeffect2 EF_BLESSING;      // Effect on player

// As @command
@effect 42                        // Show Blessing effect
```

---

## Effects by Category

### Basic Hit Effects (0-10)
<!-- RAG_CHUNK: EF_HIT_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 0 | EF_HIT1 | Regular Hit |
| 1 | EF_HIT2 | Bash |
| 2 | EF_HIT3 | Melee Skill Hit |
| 3 | EF_HIT4 | Melee Skill Hit |
| 4 | EF_HIT5 | Melee Skill Hit |
| 5 | EF_HIT6 | Melee Skill Hit |
| 6 | EF_ENTRY | Being Warped |
| 7 | EF_EXIT | Item Heal effect |
| 8 | EF_WARP | Yellow Ripple Effect |
| 9 | EF_ENHANCE | Different Type of Heal |
| 10 | EF_COIN | Mammonite |

### Buff/Support Effects (11-50)
<!-- RAG_CHUNK: EF_BUFF_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 11 | EF_ENDURE | Endure |
| 12 | EF_BEGINSPELL | Yellow cast aura |
| 13 | EF_GLASSWALL | Blue Box |
| 14 | EF_HEALSP | Blue restoring effect |
| 15 | EF_SOULSTRIKE | Soul Strike |
| 16 | EF_BASH | Hide |
| 17 | EF_MAGNUMBREAK | Magnum Break |
| 18 | EF_STEAL | Steal |
| 19 | EF_HIDING | (Invalid) |
| 20 | EF_PATTACK | Envenom/Poison |
| 21 | EF_DETOXICATION | Detoxify |
| 22 | EF_SIGHT | Sight |
| 23 | EF_STONECURSE | Stone Curse |
| 37 | EF_INCAGILITY | AGI Up |
| 38 | EF_DECAGILITY | AGI Down |
| 39 | EF_AQUA | Aqua Benedicta |
| 40 | EF_SIGNUM | Signum Crucis |
| 41 | EF_ANGELUS | Angelus |
| 42 | EF_BLESSING | Blessing |
| 43 | EF_INCAGIDEX | Dex + Agi Up |

### Mage/Wizard Effects (24-36, 89-97)
<!-- RAG_CHUNK: EF_MAGE_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 24 | EF_FIREBALL | Fire Ball |
| 25 | EF_FIREWALL | Fire Wall |
| 26 | EF_ICEARROW | A sound (a swipe?) |
| 27 | EF_FROSTDIVER | Frost Diver (Traveling) |
| 28 | EF_FROSTDIVER2 | Frost Diver (Hitting) |
| 29 | EF_LIGHTBOLT | Lightning Bolt |
| 30 | EF_THUNDERSTORM | Thunder Storm |
| 31 | EF_FIREARROW | Bubbles from feet |
| 32 | EF_NAPALMBEAT | Small clustered explosions |
| 33 | EF_RUWACH | Ruwach |
| 89 | EF_STORMGUST | Storm Gust |
| 90 | EF_LORD | Lord of Vermilion |
| 92 | EF_METEORSTORM | Meteor Storm |
| 93 | EF_YUFITEL | Jupitel Thunder (Ball) |
| 94 | EF_YUFITELHIT | Jupitel Thunder (Hit) |
| 95 | EF_QUAGMIRE | Quagmire |
| 96 | EF_FIREPILLAR | Fire Pillar |
| 97 | EF_FIREPILLARBOMB | Fire Pillar/Land Mine hit |

### Cast Auras (54-60)
<!-- RAG_CHUNK: EF_CAST_AURAS -->

| ID | Constant | Description |
|----|----------|-------------|
| 54 | EF_BEGINSPELL2 | Cast Aura (Water Element) |
| 55 | EF_BEGINSPELL3 | Cast Aura (Fire Element) |
| 56 | EF_BEGINSPELL4 | Cast Aura (Earth Element) |
| 57 | EF_BEGINSPELL5 | Cast Aura (Wind Element) |
| 58 | EF_BEGINSPELL6 | Cast Aura (Holy Element) |
| 59 | EF_BEGINSPELL7 | Cast Aura (Poison Element) |
| 60 | EF_LOCKON | Cast target circle |

### Priest/Acolyte Effects (75-91)
<!-- RAG_CHUNK: EF_PRIEST_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 75 | EF_GLORIA | Gloria |
| 76 | EF_MAGNIFICAT | Magnificat |
| 77 | EF_RESURRECTION | Resurrection |
| 78 | EF_RECOVERY | Status Recovery |
| 82 | EF_TURNUNDEAD | Turn Undead |
| 83 | EF_SANCTUARY | Sanctuary |
| 84 | EF_IMPOSITIO | Impositio Manus |
| 85 | EF_LEXAETERNA | Lex Aeterna |
| 86 | EF_ASPERSIO | Aspersio |
| 87 | EF_LEXDIVINA | Lex Divina |
| 88 | EF_SUFFRAGIUM | Suffragium |
| 91 | EF_BENEDICTIO | B. S. Sacramenti |
| 112 | EF_KYRIE | Kyrie Eleison |
| 113 | EF_MAGNUS | Magnus Exorcismus |

### Hunter/Traps (69, 99-111)
<!-- RAG_CHUNK: EF_TRAP_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 69 | EF_SKIDTRAP | Skid Trap |
| 99 | EF_FLASHER | Flasher Trap |
| 100 | EF_REMOVETRAP | Yellow ball fountain |
| 105 | EF_BLASTMINE | (nothing) |
| 106 | EF_BLASTMINEBOMB | Blast Mine Trap |
| 107 | EF_CLAYMORE | Claymore Trap |
| 108 | EF_FREEZING | Freezing Trap |
| 111 | EF_SPRINGTRAP | Spring Trap |
| 115 | EF_BLITZBEAT | Blitz Beat |
| 139 | EF_SANDMAN | Sandman Trap |
| 145 | EF_SHOCKWAVE | Shockwave Trap |
| 146 | EF_SHOCKWAVEHIT | Shockwave Trap Hit |

### Blacksmith Effects (98-104, 128)
<!-- RAG_CHUNK: EF_BLACKSMITH_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 98 | EF_HASTEUP | Adrenaline Rush |
| 101 | EF_REPAIRWEAPON | Weapon Repair |
| 102 | EF_CRASHEARTH | Hammerfall |
| 103 | EF_PERFECTION | Weapon Perfection |
| 104 | EF_MAXPOWER | Maximize Power |
| 128 | EF_OVERTHRUST | Over Thrust |
| 154 | EF_REFINEOK | Refine Success |
| 155 | EF_REFINEFAIL | Refine Fail |

### Assassin Effects (120-132)
<!-- RAG_CHUNK: EF_ASSASSIN_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 120 | EF_CLOAKING | Cloaking |
| 121 | EF_SONICBLOW | Sonic Blow (Part 1/2) |
| 122 | EF_SONICBLOWHIT | Multi hit effect |
| 123 | EF_GRIMTOOTH | Grimtooth Cast |
| 124 | EF_VENOMDUST | Venom Dust |
| 125 | EF_ENCHANTPOISON | Enchant Poison |
| 126 | EF_POISONREACT | Poison React |
| 129 | EF_SPLASHER | Venom Splasher Explosion |
| 130 | EF_TWOHANDQUICKEN | Two-Hand Quicken |
| 131 | EF_AUTOCOUNTER | Auto-Counter Hit |
| 132 | EF_GRIMTOOTHATK | Grimtooth Hit |
| 493 | EF_EDP | Enchant Deadly Poison |

### Knight/Crusader Effects (70-74, 141, 222-252)
<!-- RAG_CHUNK: EF_KNIGHT_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 70 | EF_BRANDISHSPEAR | Brandish Spear |
| 73 | EF_BOWLINGBASH | Blue/White Small Aura |
| 74 | EF_ICEWALL | Ice Wall |
| 79 | EF_EARTHSPIKE | Earth Spike |
| 80 | EF_SPEARBMR | Spear Boomerang |
| 141 | EF_PNEUMA | Pneuma |
| 142 | EF_HEAVENSDRIVE | Heaven's Drive |
| 213 | EF_DEFFENDER | Defender |
| 222 | EF_DEFENDER | Defender (Crusader) |
| 226 | EF_GRANDCROSS | Grand Cross Effect |
| 245 | EF_HOLYCROSS | Holy Cross |
| 246 | EF_SHIELDCHARGE | Shield Charge |
| 248 | EF_PROVIDENCE | Resistant Souls |
| 249 | EF_SHIELDBOOMERANG | Shield Boomerang |
| 250 | EF_SPEARQUICKEN | Spear Quicken |
| 251 | EF_DEVOTION | Devotion |
| 252 | EF_REFLECTSHIELD | Reflect Shield |

### Monk Effects (253-267, 328-330)
<!-- RAG_CHUNK: EF_MONK_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 253 | EF_ABSORBSPIRITS | Absorb Spirit Spheres |
| 254 | EF_STEELBODY | Mental Strength |
| 261 | EF_GUMGANG2 | Fury Cast Animation |
| 262 | EF_TEIHIT1 | Raging Quadruple Blow |
| 265 | EF_TANJI | Throw Spirit Sphere |
| 267 | EF_CHIMTO | Occult Impaction |
| 273 | EF_CHAINCOMBO | Raging Quadruple Blow 4 |
| 276 | EF_TEIHIT3 | Raging Thrust |
| 328 | EF_BEGINASURA | Monk Asura Strike |
| 329 | EF_TRIPLEATTACK | Triple Strike |
| 330 | EF_HITLINE | Combo Finish |
| 510 | EF_BEGINASURA11 | Champion Asura Strike |

### Bard/Dancer Effects (277-294)
<!-- RAG_CHUNK: EF_BARD_DANCER_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 277 | EF_BOTTOM_DISSONANCE | Dissonance Map Unit |
| 278 | EF_BOTTOM_LULLABY | Lullaby Map Unit |
| 279 | EF_BOTTOM_RICHMANKIM | Mr Kim a Rich Man Map Unit |
| 280 | EF_BOTTOM_ETERNALCHAOS | Eternal Chaos Map Unit |
| 281 | EF_BOTTOM_DRUMBATTLEFIELD | Drum on Battlefield Map Unit |
| 282 | EF_BOTTOM_RINGNIBELUNGEN | Ring Of Nibelungen Map Unit |
| 283 | EF_BOTTOM_ROKISWEIL | Loki's Veil Map Unit |
| 284 | EF_BOTTOM_INTOABYSS | Into the Abyss Map Unit |
| 285 | EF_BOTTOM_SIEGFRIED | Invunerable Siegfried Map Unit |
| 286 | EF_BOTTOM_WHISTLE | A Whistle Map Unit |
| 287 | EF_BOTTOM_ASSASSINCROSS | Assassin Cross of Sunset Map Unit |
| 288 | EF_BOTTOM_POEMBRAGI | Poem of Bragi Map Unit |
| 289 | EF_BOTTOM_APPLEIDUN | Apple Of Idun Map Unit |
| 290 | EF_BOTTOM_UGLYDANCE | Ugly Dance Map Unit |
| 291 | EF_BOTTOM_HUMMING | Humming Map Unit |
| 292 | EF_BOTTOM_DONTFORGETME | Please don't Forget Me Map Unit |
| 293 | EF_BOTTOM_FORTUNEKISS | Fortune's Kiss Map Unit |
| 294 | EF_BOTTOM_SERVICEFORYOU | Service For You Map Unit |

### Rogue Effects (268-275)
<!-- RAG_CHUNK: EF_ROGUE_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 268 | EF_STEALCOIN | Steal Coin |
| 269 | EF_STRIPWEAPON | Divest Weapon |
| 270 | EF_STRIPSHIELD | Divest Shield |
| 271 | EF_STRIPARMOR | Divest Armor |
| 272 | EF_STRIPHELM | Divest Helm |
| 274 | EF_RG_COIN | Steal Coin Animation |
| 275 | EF_BACKSTAP | Back Stab Animation |
| 495 | EF_RG_COIN2 | Full Strip Sound |

### Alchemist Effects (300-306)
<!-- RAG_CHUNK: EF_ALCHEMIST_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 300 | EF_CHEMICALPROTECTION | Chemical Protection |
| 302 | EF_DEMONSTRATION | Bomb |
| 305 | EF_PHARMACY_OK | Pharmacy Success |
| 306 | EF_PHARMACY_FAIL | Pharmacy Failed |
| 497 | EF_SLIM | Twilight Alchemy 1 |
| 498 | EF_SLIM2 | Twilight Alchemy 2 |
| 499 | EF_SLIM3 | Twilight Alchemy 3 |
| 537 | EF_ACIDDEMON | Acid Demonstration |

### Level/Job Effects (156-160, 200-202)
<!-- RAG_CHUNK: EF_LEVEL_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 156 | EF_JOBCHANGE | Job Change (str not found) |
| 157 | EF_LVUP | Level Up (str not found) |
| 158 | EF_JOBLVUP | Job Level Up |
| 159 | EF_TOPRANK | PvP circle |
| 160 | EF_PARTY | PvP Party Circle |
| 200 | EF_LEVEL99 | Normal level 99 Aura (Middle) |
| 201 | EF_LEVEL99_2 | Normal level 99 Aura (Bottom) |
| 202 | EF_LEVEL99_3 | Lv 99 Aura Bubble |
| 337 | EF_JOBLVUP50 | Class Change |
| 362 | EF_LEVEL99_4 | Transcendent Level 99 Aura 1 |
| 371 | EF_ANGEL | Level Up |
| 397 | EF_LEVEL99_5 | Transcended 99 Aura (Middle) |
| 398 | EF_LEVEL99_6 | Transcended 99 Aura (Bottom) |

### Potion Effects (204-221)
<!-- RAG_CHUNK: EF_POTION_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 204 | EF_POTION1 | Red Herb/Potion |
| 205 | EF_POTION2 | Orange Potion |
| 206 | EF_POTION3 | Yellow Herb/Potion |
| 207 | EF_POTION4 | White Herb/Potion |
| 208 | EF_POTION5 | Blue Herb/Potion |
| 209 | EF_POTION6 | Green Herb/Potion |
| 210 | EF_POTION7 | Yellow Circle Healing Effect |
| 211 | EF_POTION8 | Blue Circle Healing Effect |
| 218 | EF_POTION_CON | Concentration Potion |
| 219 | EF_POTION_ | Awakening Potion |
| 220 | EF_POTION_BERSERK | Berserk Potion |
| 221 | EF_POTIONPILLAR | Intense light beam |

### Weather/Map Effects (161-163, 224-225, 233)
<!-- RAG_CHUNK: EF_WEATHER_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 161 | EF_RAIN | (Nothing) |
| 162 | EF_SNOW | Snow |
| 163 | EF_SAKURA | White Sakura Leaves |
| 224 | EF_WIND | Wind (Map effect) |
| 225 | EF_VOLCANO | Volcano casting effect |
| 233 | EF_CLOUD3 | Fog |
| 333 | EF_MAPLE | Autumn Leaves |
| 515 | EF_CLOUD4 | Einbroch Fog |
| 516 | EF_CLOUD5 | Airship Cloud |

### Waterfall Effects (349-356)
<!-- RAG_CHUNK: EF_WATERFALL_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 349 | EF_WATERFALL | Waterfall (Horizontal) |
| 350 | EF_WATERFALL_90 | Waterfall (Vertical) |
| 351 | EF_WATERFALL_SMALL | Small Waterfall (Horizontal) |
| 352 | EF_WATERFALL_SMALL_90 | Small Waterfall (Vertical) |
| 353 | EF_WATERFALL_T2 | Dark Waterfall (Horizontal) |
| 354 | EF_WATERFALL_T2_90 | Dark Waterfall (Vertical) |
| 355 | EF_WATERFALL_SMALL_T2 | Dark Small Waterfall (Horizontal) |
| 356 | EF_WATERFALL_SMALL_T2_90 | Dark Small Waterfall (Vertical) |
| 557 | EF_BLUEFALL | Juperos Energy Waterfall (Horizontal) |
| 558 | EF_BLUEFALL_90 | Juperos Energy Waterfall (Vertical) |

### Transcendent Class Effects (361-400)
<!-- RAG_CHUNK: EF_TRANS_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 361 | EF_SOULBREAKER | Soul Destroyer |
| 365 | EF_PRESSURE | Gloria Domini |
| 366 | EF_BASH3D | Martyr's Reckoning |
| 367 | EF_AURABLADE | Aura Blade |
| 368 | EF_REDBODY | Berserk |
| 369 | EF_LKCONCENTRATION | Concentration |
| 370 | EF_BOTTOM_GOSPEL | Gospel Map Unit |
| 374 | EF_BOTTOM_BASILICA | Basilica |
| 375 | EF_ASSUMPTIO | Assumptio |
| 380 | EF_MAGICCRASHER | Magic Crasher |
| 386 | EF_TRUESIGHT | True Sight |
| 387 | EF_FALCONASSAULT | Falcon Assault |
| 390 | EF_MELTDOWN | Shattering Strike |
| 391 | EF_CARTBOOST | Cart Boost |
| 392 | EF_REJECTSWORD | Reject Sword |
| 393 | EF_TRIPLEATTACK3 | Arrow Vulcan |

### Taekwon/Star Gladiator Effects (411-489)
<!-- RAG_CHUNK: EF_TAEKWON_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 411 | EF_PEONG | Leap |
| 413 | EF_PRESSEDBODY | Axe Kick |
| 414 | EF_SPINEDBODY | Round Kick |
| 415 | EF_KICKEDBODY | Counter Kick |
| 417 | EF_HITBODY | Flash |
| 418 | EF_DOUBLEGUMGANG | Warmth Lightning |
| 432 | EF_ELECTRIC | Solar, Lunar and Stellar Perception |
| 433 | EF_ELECTRIC2 | Solar, Lunar and Stellar Opposition |
| 445 | EF_JUMPBODY | High Jump (Jump) |
| 446 | EF_LANDBODY | High Jump (Return Down) |
| 475-484 | EF_DEVIL1-10 | Demon of Sun Moon Stars (Level 1-10) |
| 487 | EF_BLACKDEVIL | Demon Ground Effect |

### Soul Linker Effects (419-427, 546-556)
<!-- RAG_CHUNK: EF_SOUL_LINKER_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 419 | EF_REFLECTBODY | Kaite (Visual Effect) |
| 420 | EF_BABYBODY | Eswoo (Small) |
| 422 | EF_GIANTBODY | Eswoo (Normal) |
| 424 | EF_ASURABODY | Spirit Link |
| 425 | EF_4WAYBODY | Esma Hit |
| 426 | EF_QUAKEBODY | Sprint Collision |
| 503 | EF_SOULLINK | Soul Link Word |
| 546 | EF_SMA_READY | Kaupe |
| 547 | EF_STIN | Estin |
| 553 | EF_STIN2 | Esma |
| 555 | EF_STIN3 | Estun |

### Ninja Effects (613-636)
<!-- RAG_CHUNK: EF_NINJA_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 613 | EF_THROWITEM7 | Throw Shuriken |
| 614 | EF_THROWITEM8 | Throw Kunai |
| 615 | EF_THROWITEM9 | Throw Fumma Shuriken |
| 616 | EF_THROWITEM10 | Throw Money |
| 617 | EF_BUNSINJYUTSU | Illusionary Shadow |
| 618 | EF_KOUENKA | Crimson Fire Blossom |
| 619 | EF_HYOUSENSOU | Lightning Spear Of Ice |
| 620 | EF_BOTTOM_SUITON | Water Escape Technique |
| 621 | EF_STIN4 | Wind Blade |
| 624 | EF_STIN5 | Kamaitachi |
| 630 | EF_KIRIKAGE | Shadow Slash |
| 631 | EF_TATAMI | Reverse Tatami Map Unit |
| 632 | EF_KASUMIKIRI | Mist Slash |
| 633 | EF_ISSEN | Final Strike |
| 634 | EF_KAEN | Crimson Fire Formation |
| 635 | EF_BAKU | Dragon Fire Formation |
| 636 | EF_HYOUSYOURAKU | Falling Ice Pillar |

### Gunslinger Effects (637-661)
<!-- RAG_CHUNK: EF_GUNSLINGER_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 625 | EF_MADNESS_BLUE | Madness Canceller |
| 626 | EF_MADNESS_RED | Adjustment |
| 628 | EF_BASH3D5 | Dust |
| 637 | EF_DESPERADO | Desperado |
| 638-642 | EF_LIGHTNING_S to EF_FLARE_S | Ground Drift Grenades |
| 643 | EF_RAPIDSHOWER | Rapid Shower |
| 644 | EF_MAGICALBULLET | Magic Bullet |
| 645 | EF_SPREADATTACK | Spread Attack |
| 646 | EF_TRACKCASTING | Tracking (Casting) |
| 647 | EF_TRACKING | Tracking |
| 648 | EF_TRIPLEACTION | Triple Action |
| 649 | EF_BULLSEYE | Bull's Eye |

### Food/Cooking Effects (593-621)
<!-- RAG_CHUNK: EF_FOOD_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 491 | EF_MOCHI | Element Potions |
| 492 | EF_LAMADAN | Cooking Foods |
| 593 | EF_FOOD01 | Food Effect (STR) |
| 594 | EF_FOOD02 | Food Effect (INT) |
| 595 | EF_FOOD03 | Food Effect (VIT) |
| 596 | EF_FOOD04 | Food Effect (AGI) |
| 597 | EF_FOOD05 | Food Effect (DEX) |
| 598 | EF_FOOD06 | Food Effect (LUK) |
| 608 | EF_COOKING_OK | Cooking Success |
| 609 | EF_COOKING_FAIL | Cooking Failed |

### Homunculus Effects (564-572)
<!-- RAG_CHUNK: EF_HOMUNCULUS_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 564 | EF_HOMUNCASTING | Wedding Cast |
| 565 | EF_HFLIMOON1 | Filir Moonlight Lvl 1 |
| 566 | EF_HFLIMOON2 | Filir Moonlight Lvl 2 |
| 567 | EF_HFLIMOON3 | Filir Moonlight Lvl 3 |
| 568 | EF_HO_UP | Homunculus Level Up |
| 569 | EF_HAMIDEFENCE | Amistr Bulwark |
| 570 | EF_HAMICASTLE | Amistr Castling |
| 571 | EF_HAMIBLOOD | Amistr Bloodlust |

### 3rd Class Effects (718-967)
<!-- RAG_CHUNK: EF_3RD_CLASS_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 718 | EF_FIREPILLARON2 | Judex |
| 719 | EF_FORESTLIGHT5 | Renovatio (light beam) |
| 721 | EF_ADO_STR | Adoramus (lightning bolt) |
| 722 | EF_IGN_STR | Ignition Break (explosion) |
| 727 | EF_CRIMSON_STR | Crimson Rock |
| 734 | EF_CHAINL_STR | Chain Lightning |
| 745 | EF_AIMED_STR | Aimed Bolt (crosshairs) |
| 746 | EF_ARROWSTORM_STR | Arrow Storm |
| 749 | EF_MILSHIELD_STR | Millennium Shield |
| 753 | EF_CLEARTIME | Clearance |
| 755 | EF_ORATIO | Oratio (spinning blue symbol) |
| 757 | EF_CIRCLEPOWER | Third Class Aura (Middle) |
| 758-767 | EF_ROLLING1-10 | Rolling Cutter Spin Count 1-10 |
| 769 | EF_STIN6 | Cross Ripper Slasher |
| 788 | EF_VENOMIMPRESS | Venom Impress (green skull) |
| 794 | EF_INFRAREDSCAN | Infrared Scan (red lasers) |
| 799 | EF_STASIS | Stasis (expanding blue mist) |
| 802 | EF_BOTTOM_BASILICA2 | White Imprison |
| 804 | EF_TETRA | Tetra Vortex |
| 811 | EF_STRETCH | Body Painting |
| 813-818 | EF_ENERVATION1-6 | Masquerade skills |
| 822 | EF_BOTTOM_MANHOLE | Dimension Door |
| 827 | EF_BOTTOM_ANI | Chaos Panic |
| 828 | EF_BOTTOM_MAELSTROM | Maelstrom |
| 829 | EF_BOTTOM_BLOODYLUST | Bloody Lust |
| 832 | EF_HEAL_N | Sonic Wave |
| 856 | EF_BOT_REVERB | Reverberation |
| 857 | EF_RAIN_PARTICLE | Severe Rainstorm |
| 883 | EF_GLASSWALL4 | Epiclesis (green tree) |
| 906 | EF_PRESSURE2 | Shield Press |
| 912 | EF_WALLOFTHORN | Wall of Thorns |
| 916 | EF_DEMONICFIRE | Demonic Fire |
| 919 | EF_HELLSPLANT | Hell's Plant |
| 921 | EF_VACUUM | Vacuum Extreme |
| 922 | EF_SPR_PLANT10 | Psychic Wave |
| 927 | EF_SPR_PLANT11 | Earth Grave |
| 930 | EF_PRESSURE3 | Varetyr Spear |

### Elemental Spirit Effects (947-959)
<!-- RAG_CHUNK: EF_ELEMENTAL_EFFECTS -->

| ID | Constant | Description |
|----|----------|-------------|
| 947 | EF_EL_GUST | Blue lightning sphere |
| 948 | EF_EL_BLAST | Two blue lightning spheres |
| 949 | EF_EL_AQUAPLAY | Flat, spinning diamond |
| 950 | EF_EL_UPHEAVAL | Circling planetlike spheres |
| 951 | EF_EL_WILD_STORM | Three lightning spheres |
| 952 | EF_EL_CHILLY_AIR | Spinning gem + lightning |
| 953 | EF_EL_CURSED_SOIL | Spinning planetlike spheres |
| 954 | EF_EL_COOLER | Two lightblue glowing spheres |
| 955 | EF_EL_TROPIC | Three spinning flame spheres |
| 956 | EF_EL_PYROTECHNIC | Flame |
| 957 | EF_EL_PETROLOGY | Spinning planetlike sphere |
| 958 | EF_EL_HEATER | Two flames |
| 959 | EF_POISON_MIST | Purple flame |

---

## Complete Effect List (All 967 Effects)
<!-- RAG_CHUNK: EF_COMPLETE_LIST -->

| ID | Constant | Description |
|----|----------|-------------|
| 0 | EF_HIT1 | Regular Hit |
| 1 | EF_HIT2 | Bash |
| 2 | EF_HIT3 | Melee Skill Hit |
| 3 | EF_HIT4 | Melee Skill Hit |
| 4 | EF_HIT5 | Melee Skill Hit |
| 5 | EF_HIT6 | Melee Skill Hit |
| 6 | EF_ENTRY | Being Warped |
| 7 | EF_EXIT | Item Heal effect |
| 8 | EF_WARP | Yellow Ripple Effect |
| 9 | EF_ENHANCE | Different Type of Heal |
| 10 | EF_COIN | Mammonite |
| 11 | EF_ENDURE | Endure |
| 12 | EF_BEGINSPELL | Yellow cast aura |
| 13 | EF_GLASSWALL | Blue Box |
| 14 | EF_HEALSP | Blue restoring effect |
| 15 | EF_SOULSTRIKE | Soul Strike |
| 16 | EF_BASH | Hide |
| 17 | EF_MAGNUMBREAK | Magnum Break |
| 18 | EF_STEAL | Steal |
| 19 | EF_HIDING | (Invalid) |
| 20 | EF_PATTACK | Envenom/Poison |
| 21 | EF_DETOXICATION | Detoxify |
| 22 | EF_SIGHT | Sight |
| 23 | EF_STONECURSE | Stone Curse |
| 24 | EF_FIREBALL | Fire Ball |
| 25 | EF_FIREWALL | Fire Wall |
| 26 | EF_ICEARROW | A sound (a swipe?) |
| 27 | EF_FROSTDIVER | Frost Diver (Traveling) |
| 28 | EF_FROSTDIVER2 | Frost Diver (Hitting) |
| 29 | EF_LIGHTBOLT | Lightning Bolt |
| 30 | EF_THUNDERSTORM | Thunder Storm |
| 31 | EF_FIREARROW | Bubbles from feet |
| 32 | EF_NAPALMBEAT | Small clustered explosions |
| 33 | EF_RUWACH | Ruwach |
| 34 | EF_TELEPORTATION | Old Map Exit (unused) |
| 35 | EF_READYPORTAL | Old Warp Portal (unused) |
| 36 | EF_PORTAL | Old Warp Portal (unused) |
| 37 | EF_INCAGILITY | AGI Up |
| 38 | EF_DECAGILITY | AGI Down |
| 39 | EF_AQUA | Aqua Benedicta |
| 40 | EF_SIGNUM | Signum Crucis |
| 41 | EF_ANGELUS | Angelus |
| 42 | EF_BLESSING | Blessing |
| 43 | EF_INCAGIDEX | Dex + Agi Up |
| 44 | EF_SMOKE | Little Fog Smoke |
| 45 | EF_FIREFLY | Faint Little Ball Things |
| 46 | EF_SANDWIND | Sand Wind |
| 47 | EF_TORCH | Torch |
| 48 | EF_SPRAYPOND | Small Piece of Glass |
| 49 | EF_FIREHIT | Firebolt/Wall Hits |
| 50 | EF_FIRESPLASHHIT | Spinning Fire Thing |
| 51 | EF_COLDHIT | Ice Elemental Hit |
| 52 | EF_WINDHIT | Wind Elemental Hit |
| 53 | EF_POISONHIT | Puff of Purple Smoke |
| 54 | EF_BEGINSPELL2 | Cast Aura (Water) |
| 55 | EF_BEGINSPELL3 | Cast Aura (Fire) |
| 56 | EF_BEGINSPELL4 | Cast Aura (Earth) |
| 57 | EF_BEGINSPELL5 | Cast Aura (Wind) |
| 58 | EF_BEGINSPELL6 | Cast Aura (Holy) |
| 59 | EF_BEGINSPELL7 | Cast Aura (Poison) |
| 60 | EF_LOCKON | Cast target circle |
| 61 | EF_WARPZONE | Old Warp Portal NPC (unused) |
| 62 | EF_SIGHTRASHER | Sight Trasher |
| 63 | EF_BARRIER | Moonlight Sphere |
| 64 | EF_ARROWSHOT | Purple/Yellow Light Bullet |
| 65 | EF_INVENOM | Absorb Power effect |
| 66 | EF_CURE | Cure |
| 67 | EF_PROVOKE | Provoke |
| 68 | EF_MVP | MVP Banner |
| 69 | EF_SKIDTRAP | Skid Trap |
| 70 | EF_BRANDISHSPEAR | Brandish Spear |
| 71 | EF_CONE | Spiral White balls |
| 72 | EF_SPHERE | Bigger Spiral White balls |
| 73 | EF_BOWLINGBASH | Blue/White Small Aura |
| 74 | EF_ICEWALL | Ice Wall |
| 75 | EF_GLORIA | Gloria |
| 76 | EF_MAGNIFICAT | Magnificat |
| 77 | EF_RESURRECTION | Resurrection |
| 78 | EF_RECOVERY | Status Recovery |
| 79 | EF_EARTHSPIKE | Earth Spike |
| 80 | EF_SPEARBMR | Spear Boomerang |
| 81 | EF_PIERCE | Skill hit |
| 82 | EF_TURNUNDEAD | Turn Undead |
| 83 | EF_SANCTUARY | Sanctuary |
| 84 | EF_IMPOSITIO | Impositio Manus |
| 85 | EF_LEXAETERNA | Lex Aeterna |
| 86 | EF_ASPERSIO | Aspersio |
| 87 | EF_LEXDIVINA | Lex Divina |
| 88 | EF_SUFFRAGIUM | Suffragium |
| 89 | EF_STORMGUST | Storm Gust |
| 90 | EF_LORD | Lord of Vermilion |
| 91 | EF_BENEDICTIO | B. S. Sacramenti |
| 92 | EF_METEORSTORM | Meteor Storm |
| 93 | EF_YUFITEL | Jupitel Thunder (Ball) |
| 94 | EF_YUFITELHIT | Jupitel Thunder (Hit) |
| 95 | EF_QUAGMIRE | Quagmire |
| 96 | EF_FIREPILLAR | Fire Pillar |
| 97 | EF_FIREPILLARBOMB | Fire Pillar/Land Mine hit |
| 98 | EF_HASTEUP | Adrenaline Rush |
| 99 | EF_FLASHER | Flasher Trap |
| 100 | EF_REMOVETRAP | Yellow ball fountain |
| 101 | EF_REPAIRWEAPON | Weapon Repair |
| 102 | EF_CRASHEARTH | Hammerfall |
| 103 | EF_PERFECTION | Weapon Perfection |
| 104 | EF_MAXPOWER | Maximize Power |
| 105 | EF_BLASTMINE | (nothing) |
| 106 | EF_BLASTMINEBOMB | Blast Mine Trap |
| 107 | EF_CLAYMORE | Claymore Trap |
| 108 | EF_FREEZING | Freezing Trap |
| 109 | EF_BUBBLE | Bailaban Blue bubble |
| 110 | EF_GASPUSH | Giearth Trap |
| 111 | EF_SPRINGTRAP | Spring Trap |
| 112 | EF_KYRIE | Kyrie Eleison |
| 113 | EF_MAGNUS | Magnus Exorcismus |
| 114 | EF_BOTTOM | Old Magnus Map Unit (unused) |
| 115 | EF_BLITZBEAT | Blitz Beat |
| 116 | EF_WATERBALL | Fling Watersphere |
| 117 | EF_WATERBALL2 | Waterball |
| 118 | EF_FIREIVY | Fling Firesphere |
| 119 | EF_DETECTING | Detect |
| 120 | EF_CLOAKING | Cloaking |
| 121 | EF_SONICBLOW | Sonic Blow (Part 1/2) |
| 122 | EF_SONICBLOWHIT | Multi hit effect |
| 123 | EF_GRIMTOOTH | Grimtooth Cast |
| 124 | EF_VENOMDUST | Venom Dust |
| 125 | EF_ENCHANTPOISON | Enchant Poison |
| 126 | EF_POISONREACT | Poison React |
| 127 | EF_POISONREACT2 | Small Poison React |
| 128 | EF_OVERTHRUST | Over Thrust |
| 129 | EF_SPLASHER | Venom Splasher Explosion |
| 130 | EF_TWOHANDQUICKEN | Two-Hand Quicken |
| 131 | EF_AUTOCOUNTER | Auto-Counter Hit |
| 132 | EF_GRIMTOOTHATK | Grimtooth Hit |
| 133 | EF_FREEZE | Ice Effect (NPCs) |
| 134 | EF_FREEZED | Ice Effect (NPCs) |
| 135 | EF_ICECRASH | Ice Effect (NPCs) |
| 136 | EF_SLOWPOISON | Slow Poison |
| 137 | EF_BOTTOM2 | Old Sanctuary Map Unit (unused) |
| 138 | EF_FIREPILLARON | Fire pillar |
| 139 | EF_SANDMAN | Sandman Trap |
| 140 | EF_REVIVE | Resurrection Aura |
| 141 | EF_PNEUMA | Pneuma |
| 142 | EF_HEAVENSDRIVE | Heaven's Drive |
| 143 | EF_SONICBLOW2 | Sonic Blow (Part 2/2) |
| 144 | EF_BRANDISH2 | Brandish Spear Pre-Hit |
| 145 | EF_SHOCKWAVE | Shockwave Trap |
| 146 | EF_SHOCKWAVEHIT | Shockwave Trap Hit |
| 147 | EF_EARTHHIT | Pierce Hit |
| 148 | EF_PIERCESELF | Pierce Cast Animation |
| 149 | EF_BOWLINGSELF | Bowling Bash |
| 150 | EF_SPEARSTABSELF | Pierce Cast Animation |
| 151 | EF_SPEARBMRSELF | Spear Boomerang Cast |
| 152 | EF_HOLYHIT | Turn Undead |
| 153 | EF_CONCENTRATION | Increase Concentration |
| 154 | EF_REFINEOK | Refine Success |
| 155 | EF_REFINEFAIL | Refine Fail |
| 156 | EF_JOBCHANGE | Job Change |
| 157 | EF_LVUP | Level Up |
| 158 | EF_JOBLVUP | Job Level Up |
| 159 | EF_TOPRANK | PvP circle |
| 160 | EF_PARTY | PvP Party Circle |
| 161 | EF_RAIN | (Nothing) |
| 162 | EF_SNOW | Snow |
| 163 | EF_SAKURA | White Sakura Leaves |
| 164 | EF_STATUS_STATE | (Nothing) |
| 165 | EF_BANJJAKII | Comodo Fireworks Ball |
| 166 | EF_MAKEBLUR | Energy Coat |
| 167 | EF_TAMINGSUCCESS | (Nothing) |
| 168 | EF_TAMINGFAILED | (Nothing) |
| 169 | EF_ENERGYCOAT | Energy Coat Animation |
| 170 | EF_CARTREVOLUTION | Cart Revolution |
| 171 | EF_VENOMDUST2 | Venom Dust Map Unit |
| 172-179 | EF_CHANGEDARK-CHANGEPOISON | Change Element effects |
| 180 | EF_HITDARK | Darkness Attack |
| 181 | EF_MENTALBREAK | Mental Breaker |
| 182 | EF_MAGICALATTHIT | Magical Hit |
| 183 | EF_SUI_EXPLOSION | Self Destruction |
| 186-190 | EF_COMBOATTACK1-5 | Combo Attacks 1-5 |
| 191 | EF_GUIDEDATTACK | Guided Attack |
| 192-198 | Status Attack Effects | Poison/Silence/Stun/Petrify/Curse/Sleep |
| 199 | EF_PONG | Small Popping Bubble |
| 200-202 | EF_LEVEL99-99_3 | Level 99 Auras |
| 203 | EF_GUMGANG | Fury |
| 204-211 | EF_POTION1-8 | Potion Effects |
| 212 | EF_DARKBREATH | Dark Breath |
| 213-223 | Various Knight/Crusader Effects |
| 224-242 | Weather and Map Effects |
| 243-260 | Sage and Elemental Effects |
| 261-276 | Monk Effects |
| 277-294 | Bard/Dancer Song Effects |
| 295-330 | Various Class Effects |
| 331-360 | Misc Effects |
| 361-410 | Transcendent Class Effects |
| 411-510 | Taekwon/Soul Linker Effects |
| 511-600 | Extended Class Effects |
| 601-700 | Homunculus and Misc Effects |
| 701-800 | 3rd Class Effects Part 1 |
| 801-900 | 3rd Class Effects Part 2 |
| 901-967 | 3rd Class Effects Part 3 |

---

## Usage Examples
<!-- RAG_CHUNK: EF_USAGE_EXAMPLES -->

### NPC with Visual Effect
```c
prontera,150,150,4	script	Healer	100,{
    mes "Let me heal you!";
    close2;
    specialeffect EF_HEAL;      // Effect on NPC
    specialeffect2 EF_BLESSING; // Effect on player
    percentheal 100,100;
    end;
}
```

### Item Script with Effect
```yaml
# In item_db.yml
Script: |
  specialeffect2 EF_LEVEL99;
  percentheal 100,100;
```

### Monster Spawn with Effect
```c
// Show MVP banner when boss spawns
OnMVPSpawn:
    specialeffect EF_MVP;
    end;
```

### Warp Portal Effect
```c
OnTouch:
    specialeffect2 EF_WARP;
    warp "destination",x,y;
    end;
```

---

## Notes
<!-- RAG_CHUNK: EF_NOTES -->

- Effects are client-side only - they don't affect gameplay
- Some effects may not work on all client versions
- Use `@effect <id>` to test effects in-game
- `specialeffect` shows on NPC/mob, `specialeffect2` shows on player
- Some IDs cause client errors or crashes - test before using
- Effect constants are defined in `src/map/script_constants.hpp`

---

*Generated for rAthena Knowledge Base v15.0*
