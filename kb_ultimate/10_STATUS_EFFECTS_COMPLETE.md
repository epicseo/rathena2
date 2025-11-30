# rAthena Status Effects - Complete Reference
## All 1038 SC_* Constants with Documentation

---

<!-- RAG_CHUNK: status_overview_001 -->
## Status Effect Overview

### Using Status Effects
```c
// Apply status effect
sc_start <SC_TYPE>, <duration_ms>, <val1>{, <val2>, <val3>, <val4>};
sc_start SC_BLESSING, 300000, 10;  // Blessing Lv10 for 5 min

// Check status
if (getstatus(SC_POISON))
    mes "You are poisoned!";

// Remove status
sc_end SC_POISON;

// Remove all status
sc_end SC_ALL;

// Get status info
.@remaining = getstatus(SC_BLESSING, 5);  // Remaining time in ms
.@level = getstatus(SC_BLESSING, 1);      // val1 (usually level)
```

### Status Categories
- **Common/Ailments** (SC_STONE - SC_STONEWAIT): Basic debuffs
- **Skill Effects**: From active skills
- **Item Effects**: From consumables and equipment
- **Special**: Event, quest, and system status

---

<!-- RAG_CHUNK: common_ailments_001 -->
## Common Ailments (SC_COMMON)

| Constant | ID | Effect | Cured By |
|----------|-----|--------|----------|
| SC_STONE | 0 | Petrification (DEF+25%, MDEF+25%, cannot act) | Green Potion, Panacea |
| SC_FREEZE | 1 | Frozen (cannot act, water element) | Fire damage, Natural thaw |
| SC_STUN | 2 | Stunned (cannot act) | Wears off |
| SC_SLEEP | 3 | Sleep (cannot act, wake on damage) | Damage, Wears off |
| SC_POISON | 4 | Poison (HP drain, reduced HP recovery) | Panacea, Detoxify |
| SC_CURSE | 5 | Curse (LUK=0, -25% movement) | Holy Water, Blessing |
| SC_SILENCE | 6 | Silence (cannot cast skills) | Green Potion, Panacea |
| SC_CONFUSION | 7 | Confusion (reversed movement) | Wears off |
| SC_BLIND | 8 | Blind (-25% HIT, -25% FLEE) | Green Potion, Panacea |
| SC_BLEEDING | 9 | Bleeding (HP drain, stops regen) | Bandage, Cure |
| SC_DPOISON | 10 | Deadly Poison (severe HP drain) | Antidote, Panacea |
| SC_STONEWAIT | 11 | Petrifying (turning to stone) | Move, Cure |

**Example Usage:**
```c
// Apply poison for 60 seconds
sc_start SC_POISON, 60000, 1;

// Check if player has any ailment
if (getstatus(SC_POISON) || getstatus(SC_CURSE) || getstatus(SC_SILENCE))
    mes "You have a status ailment!";
```

---

<!-- RAG_CHUNK: buff_status_001 -->
## Buff Status Effects

### Stat Buffs
| Constant | Effect | Val1 |
|----------|--------|------|
| SC_INCREASEAGI | +AGI, +Speed | Skill level |
| SC_DECREASEAGI | -AGI, -Speed | Skill level |
| SC_BLESSING | +STR/INT/DEX | Skill level |
| SC_GLORIA | +30 LUK | - |
| SC_ANGELUS | +DEF% | Skill level |
| SC_KYRIE | Damage barrier | Skill level |
| SC_MAGNIFICAT | +SP recovery | Skill level |
| SC_IMPOSITIO | +ATK | Skill level |
| SC_SUFFRAGIUM | -Cast time | Skill level |
| SC_ASPERSIO | Holy element weapon | - |

### Combat Buffs
| Constant | Effect | Val1 |
|----------|--------|------|
| SC_PROVOKE | -DEF, +ATK | Skill level |
| SC_ENDURE | No flinch | Hit count |
| SC_CONCENTRATION | +ATK%, -DEF% | Skill level |
| SC_ADRENALINE | +ASPD (axes/maces) | Skill level |
| SC_WEAPONPERFECTION | Size penalty removal | - |
| SC_OVERTHRUST | +ATK% | Skill level |
| SC_MAXIMIZEPOWER | Max weapon damage | - |
| SC_TWOHANDQUICKEN | +ASPD (2H sword) | Skill level |
| SC_SPEARQUICKEN | +ASPD (spear), +FLEE, +CRIT | Skill level |
| SC_ONEHAND | +ASPD (1H sword) | Skill level |
| SC_AURABLADE | +ATK | Skill level |
| SC_PARRYING | Block physical attacks | Skill level |
| SC_BERSERK | +ATK%, +Speed, cannot use skills | - |

### Speed Buffs
| Constant | Effect | Note |
|----------|--------|------|
| SC_SPEEDUP0 | +25% movement | From item |
| SC_SPEEDUP1 | +50% movement | From skill |
| SC_ASPDPOTION0 | +ASPD | Concentration Pot |
| SC_ASPDPOTION1 | +ASPD | Awakening Pot |
| SC_ASPDPOTION2 | +ASPD | Berserk Pot |
| SC_ASPDPOTION3 | +ASPD | Box effect |
| SC_ATKPOTION | +ATK | From item |
| SC_MATKPOTION | +MATK | From item |

**Example:**
```c
// Apply typical buff set
sc_start SC_BLESSING, 300000, 10;
sc_start SC_INCREASEAGI, 300000, 10;
sc_start SC_ASPDPOTION2, 1800000, 0;  // Berserk pot 30min
```

---

<!-- RAG_CHUNK: offensive_status_001 -->
## Offensive/Debuff Status

### Strip Effects
| Constant | Effect |
|----------|--------|
| SC_STRIPWEAPON | Cannot use weapon |
| SC_STRIPSHIELD | Cannot use shield |
| SC_STRIPARMOR | Cannot use armor |
| SC_STRIPHELM | Cannot use headgear |
| SC_CP_WEAPON | Strip immunity (weapon) |
| SC_CP_SHIELD | Strip immunity (shield) |
| SC_CP_ARMOR | Strip immunity (armor) |
| SC_CP_HELM | Strip immunity (helm) |

### Damage Over Time
| Constant | Effect | Source |
|----------|--------|--------|
| SC_BURNING | Fire damage over time | Fire skills |
| SC_CRYSTALIZE | Ice damage, cannot move | Ice skills |
| SC_LEECHESEND | HP drain | Shadow Chaser |
| SC_VENOMBLEED | HP loss on movement | Guillotine Cross |
| SC_TOXIN | Periodic damage, SP drain | Guillotine Cross |
| SC_MAGICMUSHROOM | Random skill cast, SP loss | Guillotine Cross |
| SC_PYREXIA | Confusion + HP drain | Guillotine Cross |
| SC_DEATHHURT | No recovery | Guillotine Cross |

### Movement Restrictions
| Constant | Effect |
|----------|--------|
| SC_ANKLE | Cannot move (Ankle Snare) |
| SC_STOP | Movement stopped |
| SC_SPIDERWEB | Stuck in web |
| SC_CLOSECONFINE | Cannot move (both attacker and target) |
| SC_ELECTRICSHOCKER | Stuck, cannot attack |
| SC_THORNSTRAP | Stuck in thorns |

---

<!-- RAG_CHUNK: skill_status_001 -->
## Skill-Related Status

### Swordsman Classes
```c
SC_PROVOKE          // Provoke
SC_ENDURE           // Endure (no flinch)
SC_AUTOGUARD        // Auto Guard block chance
SC_REFLECTSHIELD    // Reflect Shield
SC_DEFENDER         // Defender mode
SC_SACRIFICE        // Sacrifice mode
SC_DEVOTION         // Devotion link
SC_PARRYING         // Parrying block
SC_CONCENTRATION    // Spear Dynamo/Concentration
SC_TENSIONRELAX     // HP recovery boost
SC_BERSERK          // Lord Knight Berserk
SC_DEATHBOUND       // Deathbound counter
SC_REFRESH          // Refresh debuff immunity
```

### Mage Classes
```c
SC_SIGHT            // Sight (reveal hidden)
SC_SAFETYWALL       // Safety Wall protection
SC_ENERGYCOAT       // Energy Coat SP shield
SC_VOLCANO          // Volcano ground effect
SC_DELUGE           // Deluge ground effect
SC_VIOLENTGALE      // Violent Gale ground effect
SC_LANDPROTECTOR    // Land Protector
SC_AUTOSPELL        // Auto Spell trigger
SC_MEMORIZE         // Reduce cast time
SC_RECOGNIZEDSPELL  // Recognito spell
SC_READING_SB       // Spell Book reading
```

### Archer Classes
```c
SC_CONCENTRATION    // True Sight/Concentration
SC_TRUESIGHT        // True Sight buff
SC_WINDWALK         // Wind Walk speed
SC_FEARBREEZE       // Fear Breeze multi-hit
SC_UNLIMITEDHUMMINGVOICE // Unlimited Voice
SC_SWING            // Swing dance
SC_SYMPHONY         // Symphony ensemble
```

### Acolyte Classes
```c
SC_BLESSING         // Blessing
SC_INCREASEAGI      // Increase AGI
SC_DECREASEAGI      // Decrease AGI
SC_ANGELUS          // Angelus DEF
SC_KYRIE            // Kyrie Eleison
SC_MAGNIFICAT       // Magnificat SP regen
SC_GLORIA           // Gloria LUK
SC_ASSUMPTIO        // Assumptio damage reduction
SC_BASILICA         // Basilica protection
SC_EPICLESIS        // Epiclesis ground
SC_LAUDAAGNUS       // Lauda Agnus
SC_LAUDARAMUS       // Lauda Ramus
SC_ADORAMUS         // Adoramus debuff
SC_RENOVATIO        // Renovatio heal over time
SC_EXPIATIO         // Expiatio defense pierce
SC_SECRAMENT        // Secrament cast reduction
SC_DUPLELIGHT       // Duple Light trigger
SC_ORATIO           // Oratio holy resist down
```

### Merchant Classes
```c
SC_CARTBOOST        // Cart Boost speed
SC_MELTDOWN         // Meltdown strip
SC_ADRENALINE       // Adrenaline Rush
SC_ADRENALINE2      // Full Adrenaline Rush
SC_WEAPONPERFECTION // Weapon Perfection
SC_OVERTHRUST       // Over Thrust
SC_MAXOVERTHRUST    // Maximum Over Thrust
SC_LOUDEXCLAIM      // Loud Exclamation
SC_OVERTHRUST       // Over Thrust
```

### Thief Classes
```c
SC_HIDING           // Hiding
SC_CLOAKING         // Cloaking
SC_CHASEWALK        // Chase Walk
SC_CHASEWALK2       // Chase Walk STR bonus
SC_ENCPOISON        // Enchant Poison
SC_POISONREACT      // Poison React
SC_EDP              // Enchant Deadly Poison
SC_CLOAKINGEXCEED   // Cloaking Exceed
SC__SHADOWFORM      // Shadow Form link
SC__INVISIBILITY    // Invisibility
SC_WEAPONBLOCKING   // Weapon Blocking
```

---

<!-- RAG_CHUNK: extended_status_001 -->
## Extended Job Status

### Taekwon/Star Gladiator
```c
SC_RUN              // Running/Spurt
SC_STORMKICK_ON     // Storm Kick stance
SC_DOWNKICK_ON      // Down Kick stance
SC_TURNKICK_ON      // Turn Kick stance
SC_COUNTERKICK_ON   // Counter Kick stance
SC_DODGE_ON         // Dodge stance
SC_STAR_COMFORT     // Comfort of Star
SC_MOON_COMFORT     // Comfort of Moon
SC_SUN_COMFORT      // Comfort of Sun
SC_FUSION           // Soul Link Union
```

### Soul Linker
```c
SC_SPIRIT           // Soul Link
SC_SMA              // Esma ready
SC_SKE              // Eske ATK boost
SC_SKA              // Eska FLEE boost
SC_KAAHI            // Kaahi heal on hit
SC_KAUPE            // Kaupe dodge
SC_KAITE            // Kaite reflect
```

### Ninja/Kagerou/Oboro
```c
SC_NEN              // Soul/Ninja Aura
SC_UTSUSEMI         // Utsusemi dodge
SC_BUNSINJYUTSU     // Bunshin mirror image
SC_SUITON           // Suiton water ground
SC_KAENSIN          // Fire Formation
SC_IZAYOI           // Izayoi
SC_ZENKAI           // Zenkai
SC_KAGEHUMI         // Kagehumi
SC_KYOMU            // Kyomu debuff
SC_KAGEMUSYA        // Kagemusha
```

### Gunslinger/Rebellion
```c
SC_GATLINGFEVER     // Gatling Fever
SC_MADNESSCANCEL    // Madness Canceler
SC_ADJUSTMENT       // Adjustment
SC_INCREASING       // Increasing Accuracy
SC_HEAT_BARREL      // Heat Barrel
SC_P_ALTER          // Platinum Alter
SC_E_CHAIN          // Eternal Chain
SC_C_MARKER         // Crimson Marker
```

### Doram/Summoner
```c
SC_GROOMING         // Grooming
SC_CHATTERING       // Chattering
SC_MELON_BOMB       // Melon Bomb debuff
SC_CATNIPPOWDER     // Catnip Powder
SC_SV_ROOTTWIST     // Root Twist bind
SC_ARCLOUSEDASH     // Arclouse Dash
SC_TUNAPARTY        // Tuna Party buff
SC_SHRIMP           // Shrimp buff
```

---

<!-- RAG_CHUNK: renewal_status_001 -->
## 3rd Class / Renewal Status

### Rune Knight
```c
SC_ENCHANTBLADE     // Enchant Blade
SC_DEATHBOUND       // Death Bound
SC_VITALITYACTIVATION // Vitality Activation
SC_FIGHTINGSPIRIT   // Fighting Spirit
SC_ABUNDANCE        // Abundance
SC_GIANTGROWTH      // Giant Growth
SC_STONEHARDSKIN    // Stone Hard Skin
SC_MILLENNIUMSHIELD // Millennium Shield
SC_REFRESH          // Refresh
SC_CRUSHSTRIKE      // Crush Strike
```

### Warlock
```c
SC_FREEZING         // Freezing status
SC_MARSHOFABYSS     // Marsh of Abyss
SC_RECOGNIZEDSPELL  // Recognized Spell
SC_READING_SB       // Reading Spell Book
SC_STASIS           // Stasis
SC_WHITEIMPRISON    // White Imprison
```

### Ranger
```c
SC_FEARBREEZE       // Fear Breeze
SC_ELECTRICSHOCKER  // Electric Shocker
SC_WUGDASH          // Wug Dash
SC_WUGBITE          // Wug Bite debuff
SC_CAMOUFLAGE       // Camouflage
SC_UNLIMITEDHUMMINGVOICE // Unlimited
```

### Archbishop
```c
SC_RENOVATIO        // Renovatio HoT
SC_EXPIATIO         // Expiatio pierce
SC_DUPLELIGHT       // Duple Light
SC_SECRAMENT        // Secrament
SC_EPICLESIS        // Epiclesis field
SC_OFFERTORIUM      // Offertorium
SC_LAUDAAGNUS       // Lauda Agnus
SC_LAUDARAMUS       // Lauda Ramus
SC_ADORAMUS         // Adoramus
SC_ORATIO           // Oratio
SC_ANCILLA          // Ancilla
```

### Mechanic
```c
SC_ACCELERATION     // Acceleration
SC_HOVERING         // Hovering
SC_SHAPESHIFT       // Shape Shift
SC_INFRAREDSCAN     // Infrared Scan
SC_MAGNETICFIELD    // Magnetic Field
SC_NEUTRALBARRIER   // Neutral Barrier
SC_STEALTHFIELD     // Stealth Field
SC_OVERHEAT         // Overheat debuff
SC_OVERHEAT_LIMITPOINT // Overheat limit
```

### Guillotine Cross
```c
SC_CLOAKINGEXCEED   // Cloaking Exceed
SC_WEAPONBLOCKING   // Weapon Blocking
SC_HALLUCINATIONWALK // Hallucination Walk
SC_ROLLINGCUTTER    // Rolling Cutter count
SC_VENOMIMPRESS     // Venom Impress
SC_POISONINGWEAPON  // Poisoning Weapon
SC_PYREXIA          // Pyrexia
SC_DEATHHURT        // Death Hurt
SC_VENOMBLEED       // Venom Bleed
SC_MAGICMUSHROOM    // Magic Mushroom
SC_TOXIN            // Toxin
SC_OBLIVIONCURSE    // Oblivion Curse
SC_LEECHESEND       // Leech End
```

### Royal Guard
```c
SC_SHIELDSPELL_ATK  // Shield Spell ATK
SC_SHIELDSPELL_HP   // Shield Spell HP
SC_SHIELDSPELL_SP   // Shield Spell SP
SC_FORCEOFVANGUARD  // Force of Vanguard
SC_BANDING          // Banding
SC_PRESTIGE         // Prestige
SC_INSPIRATION      // Inspiration
SC_KINGS_GRACE      // King's Grace
SC_MOON_COMFORT     // Moon Comfort (linked)
```

### Sorcerer
```c
SC_FIRE_INSIGNIA    // Fire Insignia
SC_WATER_INSIGNIA   // Water Insignia
SC_WIND_INSIGNIA    // Wind Insignia
SC_EARTH_INSIGNIA   // Earth Insignia
SC_SPELLFIST        // Spell Fist
SC_WARMER           // Warmer field
SC_VACUUM_EXTREME   // Vacuum Extreme
SC_STRIKING         // Striking
```

### Minstrel/Wanderer
```c
SC_MELOITHESIS      // Metalic Sound debuff
SC_WINKCHARM        // Wink of Charm
SC_DANCEWITHWUG     // Dance with Wug
SC_LERADSDEW        // Lerad's Dew
SC_MELODYOFSINK     // Melody of Sink
SC_BEYONDOFWARCRY   // Beyond of Warcry
SC_UNLIMITEDHUMMINGVOICE // Unlimited
SC_SIRCLEOFNATURE   // Circle of Nature
SC_GLOOMYDAY        // Gloomy Day
SC_SATURDAYNIGHTFEVER // Saturday Night Fever
SC_SONGOFMANA       // Song of Mana
SC_DANCEWITHWUG     // Dance with Wug
SC_RUSHWINDMILL     // Rush Windmill
SC_ECHOSONG         // Echo Song
SC_HARMONIZE        // Harmonize
SC_FRIGG_SONG       // Frigg's Song
```

### Sura
```c
SC_CURSEDCIRCLE_ATKER  // Cursed Circle (caster)
SC_CURSEDCIRCLE_TARGET // Cursed Circle (target)
SC_CRESCENTELBOW    // Crescent Elbow
SC_LIGHTNINGWALK    // Lightning Walk
SC_GT_ENERGYGAIN    // Energy Gain
SC_GT_CHANGE        // Change
SC_GT_REVITALIZE    // Revitalize
SC_GENTLETOUCH_ENERGYGAIN // Gentle Touch Energy
SC_GENTLETOUCH_CHANGE // Gentle Touch Change
SC_GENTLETOUCH_REVITALIZE // Gentle Touch Revitalize
```

### Genetic
```c
SC_MELON_BOMB       // Melon Bomb
SC_BANANA_BOMB      // Banana Bomb
SC_BANANA_BOMB_SITDOWN // Banana Bomb sit
SC_SAVAGE_STEAK     // Savage Steak buff
SC_COCKTAIL_WARG_BLOOD // Cocktail buff
SC_MINOR_BBQ        // BBQ buff
SC_SIROMA_ICE_TEA   // Ice Tea buff
SC_DROCERA_HERB_STEAMED // Herb buff
SC_PUTTI_TAILS_NOODLES // Noodles buff
SC_THORNSTRAP       // Thorn Trap
SC_BLOODSUCKER      // Blood Sucker
SC_MANDRAGORA       // Howling of Mandragora
SC_SMOKEPOWDER      // Smoke Powder
SC_TEARGAS          // Tear Gas
SC_GN_CARTBOOST     // Cart Boost
```

### Shadow Chaser
```c
SC__REPRODUCE       // Reproduce
SC__AUTOSHADOWSPELL // Auto Shadow Spell
SC__SHADOWFORM      // Shadow Form
SC__BODYPAINT       // Body Paint
SC__INVISIBILITY    // Invisibility
SC__STRIPACCESSORY  // Strip Accessory
SC__DEADLYINFECT    // Deadly Infect
SC__ENERVATION      // Enervation
SC__GROOMY          // Groomy
SC__IGNORANCE       // Ignorance
SC__LAZINESS        // Laziness
SC__UNLUCKY         // Unlucky
SC__WEAKNESS        // Weakness
SC__CHAOS           // Chaos
SC__BLOODYLUST      // Bloody Lust
SC__FEINTBOMB       // Feint Bomb
SC__MANHOLE         // Manhole
```

---

<!-- RAG_CHUNK: 4th_class_status_001 -->
## 4th Class Status

### Dragon Knight
```c
SC_CHARGINGPIERCE   // Charging Pierce
SC_DRAGONIC_AURA    // Dragonic Aura
SC_SERVANTWEAPON    // Servant Weapon
```

### Imperial Guard
```c
SC_GUARD_STANCE     // Guard Stance
SC_ATTACK_STANCE    // Attack Stance
SC_SHIELD_POWER     // Shield Power
SC_HOLY_S           // Holy Shield
```

### Arch Mage
```c
SC_CLIMAX           // Climax
SC_CLIMAX_CRYIMP    // Climax Cryimp
SC_CLIMAX_DES_HU    // Climax Des Hu
SC_CLIMAX_EARTH     // Climax Earth
SC_CLIMAX_BLOOM     // Climax Bloom
```

### Cardinal
```c
SC_MEDIALE          // Mediale
SC_COMPETENTIA      // Competentia
SC_RELIGIO          // Religio
SC_BENEDICTUM       // Benedictum
```

### Meister
```c
SC_A_MACHINE        // A Machine
SC_D_MACHINE        // D Machine
SC_BIONIC_WOODENWARRIOR // Wooden Warrior
SC_BIONIC_WOODEN_FAIRY  // Wooden Fairy
SC_BIONIC_CREEPER   // Creeper
SC_BIONIC_HELLTREE  // Hell Tree
```

### Shadow Cross
```c
SC_SHADOW_STRIP     // Shadow Strip
SC_SHADOW_EXCEED    // Shadow Exceed
SC_POTENT_VENOM     // Potent Venom
SC_SHADOW_SCAR      // Shadow Scar
```

### Troubadour/Trouvere
```c
SC_MYSTIC_SYMPHONY  // Mystic Symphony
SC_KVASIR_SONATA    // Kvasir Sonata
SC_AIN_RHAPSODY     // Ain Rhapsody
SC_MUSICAL_INTERLUDE // Musical Interlude
```

### Inquisitor
```c
SC_POWERFUL_FAITH   // Powerful Faith
SC_FIRM_FAITH       // Firm Faith
SC_SINCERE_FAITH    // Sincere Faith
SC_FIRST_BRAND      // First Brand
SC_SECOND_BRAND     // Second Brand
SC_FIRST_FAITH_POWER // First Faith Power
SC_SECOND_JUDGE     // Second Judge
```

### Biolo
```c
SC_PRE_ACIES        // Pre Acies
SC_TOXIN_OF_MANDARA // Toxin of Mandara
SC_RESEARCHREPORT   // Research Report
SC_DEADLY_DEFEASANCE // Deadly Defeasance
```

### Abyss Chaser
```c
SC_ABYSS_DAGGER     // Abyss Dagger
SC_ABYSS_SLAYER     // Abyss Slayer
SC_ABYSSFORCEWEAPON // Abyss Force Weapon
```

### Wind Hawk
```c
SC_CALAMITYGALE     // Calamity Gale
SC_HAWKEYES         // Hawk Eyes
SC_INTENSIVE_AIM    // Intensive Aim
```

### Night Watch
```c
SC_AUTO_FIRING_LAUNCHER // Auto Firing Launcher
SC_GRENADE_FRAGMENT_1-6 // Grenade Fragments
SC_MASSIVE_F_BLASTER // Massive F Blaster
```

### Spirit Handler
```c
SC_SOULATTACK       // Soul Attack
SC_SOULDIVISION     // Soul Division
SC_SOULENERGY       // Soul Energy
SC_SOULCURSE        // Soul Curse
SC_SOULUNITY        // Soul Unity
SC_SOULCOLLECT      // Soul Collect
SC_SOULSHADOW       // Soul Shadow
SC_SOULFAIRY        // Soul Fairy
SC_SOULFALCON       // Soul Falcon
SC_SOULGOLEM        // Soul Golem
```

---

<!-- RAG_CHUNK: special_status_001 -->
## Special/System Status

### Weight Penalty
```c
SC_WEIGHT50         // 50% weight (no regen)
SC_WEIGHT90         // 90% weight (no attack)
```

### Transformation
```c
SC_WEDDING          // Wedding dress
SC_XMAS             // Christmas costume
SC_SUMMER           // Summer costume
SC_HANBOK           // Hanbok costume
SC_OKTOBERFEST      // Oktoberfest costume
SC_DRESSUP          // Costume dress up
```

### System Status
```c
SC_NOCHAT           // Chat ban
SC_JAILED           // Jailed
SC_AUTOTRADE        // Autotrading
SC_PUSH_CART        // Pushcart equipped
SC_ALL_RIDING       // Any riding status
SC_MADOGEAR         // Mado Gear
```

### Item/Event
```c
SC_ITEMBOOST        // EXP boost item
SC_EXPBOOST         // Base EXP boost
SC_JEXPBOOST        // Job EXP boost
SC_LIFEINSURANCE    // Token of Siegfried effect
SC_BOSSMAPINFO      // Convex Mirror
SC_PROTECT          // Protection
```

---

#rathena #status #sc_start #sc_end #buff #debuff #ailment #skill #effects
