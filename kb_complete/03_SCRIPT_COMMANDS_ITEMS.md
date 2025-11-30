# rAthena Script Commands - Item Reference
## Complete Item Management Commands

---

<!-- RAG_CHUNK: getitem_001 -->
## Give Items

### getitem
**Syntax:** `getitem <item id>,<amount>{,<account id>};`
**Syntax:** `getitem "<item name>",<amount>{,<account id>};`

Give items to player's inventory.

**Examples:**
```c
getitem 501, 10;           // 10 Red Potions
getitem "Red_Potion", 10;  // Same using name
getitem 501, 10, .@aid;    // Give to specific account
```

---

### getitem2
**Syntax:** `getitem2 <id>,<amount>,<identify>,<refine>,<attribute>,<c1>,<c2>,<c3>,<c4>{,<account id>};`

Give item with specific properties.

**Parameters:**
- `identify` - 1=identified, 0=unidentified
- `refine` - Refine level (0-20)
- `attribute` - 1=broken, 0=normal
- `c1-c4` - Card slots (card IDs or special values)

**Card Slot Special Values:**
- `254` in c1 = Named non-equipment item
- `255` in c1 = Named equipment
- c3/c4 = Character ID split for naming

**Examples:**
```c
// +10 Knife with 4 Drops cards
getitem2 1201, 1, 1, 10, 0, 4001, 4001, 4001, 4001;

// Named Apple
.@charid = getcharid(0);
.@c3 = .@charid & 65535;
.@c4 = .@charid >> 16;
getitem2 512, 1, 1, 0, 0, 254, 0, .@c3, .@c4;
```

---

### getitem3
**Syntax:** `getitem3 <id>,<amount>,<identify>,<refine>,<attribute>,<c1>,<c2>,<c3>,<c4>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account id>};`

Give item with random options.

**Example:**
```c
setarray .@OptID[0], RDMOPT_VAR_MAXHPAMOUNT;
setarray .@OptVal[0], 500;
setarray .@OptParam[0], 0;
getitem3 28705, 1, 1, 9, 0, 0, 0, 0, 0, .@OptID, .@OptVal, .@OptParam;
```

---

### getitem4
**Syntax:** `getitem4 <id>,<amount>,<identify>,<refine>,<attribute>,<c1>,<c2>,<c3>,<c4>,<grade>,<RandomIDArray>,<RandomValueArray>,<RandomParamArray>{,<account id>};`

Give item with grade and random options.

**Grades:**
- `ENCHANTGRADE_NONE` (0)
- `ENCHANTGRADE_D` (1)
- `ENCHANTGRADE_C` (2)
- `ENCHANTGRADE_B` (3)
- `ENCHANTGRADE_A` (4)

---

<!-- RAG_CHUNK: getitembound_001 -->
## Bound Items

### getitembound
**Syntax:** `getitembound <id>,<amount>,<bound type>{,<account id>};`

Give bound item (cannot be traded/dropped).

**Bound Types:**
- `Bound_Account` - Account bound
- `Bound_Guild` - Guild bound
- `Bound_Party` - Party bound
- `Bound_Char` - Character bound

**Example:**
```c
getitembound 2301, 1, Bound_Char;  // Character-bound Cotton Shirt
```

---

### getitembound2 / getitembound3 / getitembound4
Extended versions with cards, random options, and grades.

```c
getitembound2 1201, 1, 1, 10, 0, 4001, 0, 0, 0, Bound_Account;
```

---

<!-- RAG_CHUNK: rental_items_001 -->
## Rental Items

### rentitem
**Syntax:** `rentitem <id>,<seconds>{,<account id>};`

Give temporary item that auto-deletes after time expires.

**Example:**
```c
rentitem 2301, 86400;  // Cotton Shirt for 24 hours (86400 seconds)
```

---

### rentitem2 / rentitem3 / rentitem4
Extended versions with cards, random options, and grades.

```c
rentitem2 2301, 3600, 1, 5, 0, 0, 0, 0, 0;  // +5 for 1 hour
```

---

### rentalcountitem
**Syntax:** `rentalcountitem(<id>{,<account id>})`

Count rental items (regular countitem doesn't count rentals).

---

<!-- RAG_CHUNK: delitem_001 -->
## Delete Items

### delitem
**Syntax:** `delitem <id>,<amount>{,<account id>};`

Remove items from inventory.

**Example:**
```c
if (countitem(501) >= 10) {
    delitem 501, 10;
    mes "Removed 10 Red Potions.";
}
```

---

### delitem2 / delitem3 / delitem4
Delete items matching specific properties.

```c
// Delete specific +10 Knife with Drops cards
delitem2 1201, 1, 1, 10, 0, 4001, 4001, 4001, 4001;
```

---

### delitemidx
**Syntax:** `delitemidx <index>{,<amount>{,<char id>}};`

Delete item at specific inventory index (from getinventorylist).

**Example:**
```c
getinventorylist;
for (.@i = 0; .@i < @inventorylist_count; .@i++) {
    if (@inventorylist_id[.@i] == 501)
        delitemidx @inventorylist_idx[.@i];
}
```

---

<!-- RAG_CHUNK: countitem_001 -->
## Count Items

### countitem
**Syntax:** `countitem(<id>{,<account id>})`

Count items in inventory.

**Example:**
```c
.@apples = countitem(512);
mes "You have " + .@apples + " apples.";
```

---

### countitem2 / countitem3 / countitem4
Count items matching specific properties.

```c
// Count +10 Knives
.@count = countitem2(1201, 1, 10, 0, 0, 0, 0, 0);
```

---

### countbound
**Syntax:** `countbound({<bound type>{,<char id>}})`

Count bound items. Returns total or filtered by type.

---

<!-- RAG_CHUNK: cart_storage_001 -->
## Cart/Storage Commands

### Cart Commands
```c
cartcountitem(<id>)
cartcountitem2(<id>,<identify>,<refine>,<attr>,<c1>,<c2>,<c3>,<c4>)
cartdelitem <id>,<amount>
cartdelitem2 <id>,<amount>,<identify>,<refine>,<attr>,<c1>,<c2>,<c3>,<c4>
```

### Storage Commands
```c
storagecountitem(<id>)
storagecountitem2(...)
storagedelitem <id>,<amount>
storagedelitem2 ...
openstorage;              // Open personal storage
openstorage2 <mode>,<acc>; // mode: 0=view, 1=add, 2=get, 3=all
```

### Guild Storage Commands
```c
guildstoragecountitem(<id>)
guildstoragecountitem2(...)
guildstoragedelitem <id>,<amount>
guildstoragedelitem2 ...
guildopenstorage()        // Returns status code
```

**guildopenstorage Return Values:**
- `GSTORAGE_OPEN` - Success
- `GSTORAGE_STORAGE_ALREADY_OPEN` - Player storage open
- `GSTORAGE_ALREADY_OPEN` - Guild storage open
- `GSTORAGE_NO_GUILD` - Not in guild
- `GSTORAGE_NO_PERMISSION` - No permission

---

<!-- RAG_CHUNK: makeitem_001 -->
## Drop Items on Map

### makeitem
**Syntax:** `makeitem <id>,<amount>,"<map>",<x>,<y>{,<canShowEffect>};`

Create item on ground (will disappear after time).

**Example:**
```c
makeitem 512, 5, "prontera", 150, 150;  // Drop 5 Apples
makeitem 512, 1, "this", 0, 0;          // Drop near player randomly
```

---

### makeitem2 / makeitem3 / makeitem4
Drop items with properties, random options, grades.

---

### cleanarea / cleanmap
**Syntax:**
```c
cleanarea "<map>",<x1>,<y1>,<x2>,<y2>;  // Clear items in area
cleanmap "<map>";                         // Clear all items on map
```

---

<!-- RAG_CHUNK: item_info_001 -->
## Item Information

### getitemname
**Syntax:** `getitemname(<id>)`

Get item's display name.

```c
mes "Item: " + getitemname(501);  // "Red Potion"
```

---

### getitemslots
**Syntax:** `getitemslots(<id>)`

Get number of card slots.

---

### getiteminfo
**Syntax:** `getiteminfo(<id>,<type>)`

Get item database information.

**Types:**
| Constant | Value | Description |
|----------|-------|-------------|
| ITEMINFO_BUY | 0 | Buy price |
| ITEMINFO_SELL | 1 | Sell price |
| ITEMINFO_TYPE | 2 | Item type |
| ITEMINFO_MAXCHANCE | 3 | Max drop chance |
| ITEMINFO_GENDER | 4 | Gender restriction |
| ITEMINFO_LOCATIONS | 5 | Equip locations |
| ITEMINFO_WEIGHT | 6 | Weight (*10) |
| ITEMINFO_ATTACK | 7 | ATK |
| ITEMINFO_DEFENSE | 8 | DEF |
| ITEMINFO_RANGE | 9 | Attack range |
| ITEMINFO_SLOT | 10 | Card slots |
| ITEMINFO_VIEW | 11 | View/Look |
| ITEMINFO_EQUIPLEVELMIN | 12 | Min equip level |
| ITEMINFO_WEAPONLEVEL | 13 | Weapon level |
| ITEMINFO_ALIASNAME | 14 | Alias name ID |
| ITEMINFO_EQUIPLEVELMAX | 15 | Max equip level |
| ITEMINFO_MAGICATTACK | 16 | MATK (Renewal) |
| ITEMINFO_ARMORLEVEL | 19 | Armor level |

**Example:**
```c
.@price = getiteminfo(501, ITEMINFO_BUY);
.@weight = getiteminfo(501, ITEMINFO_WEIGHT) / 10;
```

---

### setiteminfo
**Syntax:** `setiteminfo(<id>,<type>,<value>)`

Modify item database value (temporary, resets on reload).

---

### setitemscript
**Syntax:** `setitemscript(<id>,"<script>"{,<type>});`

Set item's script (temporary).

**Types:**
- 0 = Script (use script)
- 1 = EquipScript
- 2 = UnEquipScript

**Example:**
```c
setitemscript 501, "{ heal 500,0; }";  // Red Potion heals 500 HP
setitemscript 501, "";                  // Remove script
```

---

### searchitem
**Syntax:** `searchitem(<array>,"<name>")`

Search items by name. Returns count (max 10 results).

**Example:**
```c
.@count = searchitem(.@results, "Potion");
for (.@i = 0; .@i < .@count; .@i++)
    mes getitemname(.@results[.@i]);
```

---

<!-- RAG_CHUNK: nameditem_001 -->
## Named Items

### getnameditem
**Syntax:** `getnameditem(<id>,"<char name>");`
**Syntax:** `getnameditem(<id>,<char id>);`

Create item signed with character's name. Returns 1 on success.

**Example:**
```c
if (getnameditem(512, strcharinfo(0)))
    mes "Here's your signed Apple!";
```

---

<!-- RAG_CHUNK: equipment_001 -->
## Equipment Commands

### equip
**Syntax:** `equip <id>{,<char id>};`

Equip item from inventory.

---

### unequip
**Syntax:** `unequip <slot>{,<char id>};`

Unequip item from slot.

**Equipment Slots:**
| Constant | Value | Location |
|----------|-------|----------|
| EQI_ACC_L | 0 | Accessory Left |
| EQI_ACC_R | 1 | Accessory Right |
| EQI_SHOES | 2 | Shoes |
| EQI_GARMENT | 3 | Garment |
| EQI_HEAD_LOW | 4 | Lower Headgear |
| EQI_HEAD_MID | 5 | Middle Headgear |
| EQI_HEAD_TOP | 6 | Upper Headgear |
| EQI_ARMOR | 7 | Armor |
| EQI_HAND_L | 8 | Left Hand |
| EQI_HAND_R | 9 | Right Hand |
| EQI_COSTUME_HEAD_TOP | 10 | Costume Top |
| EQI_COSTUME_HEAD_MID | 11 | Costume Mid |
| EQI_COSTUME_HEAD_LOW | 12 | Costume Low |
| EQI_COSTUME_GARMENT | 13 | Costume Garment |
| EQI_AMMO | 14 | Ammo |
| EQI_SHADOW_ARMOR | 15 | Shadow Armor |
| EQI_SHADOW_WEAPON | 16 | Shadow Weapon |
| EQI_SHADOW_SHIELD | 17 | Shadow Shield |
| EQI_SHADOW_SHOES | 18 | Shadow Shoes |
| EQI_SHADOW_ACC_R | 19 | Shadow Acc R |
| EQI_SHADOW_ACC_L | 20 | Shadow Acc L |

---

### getequipid
**Syntax:** `getequipid(<slot>{,<char id>})`

Get item ID equipped at slot. Returns -1 if empty.

**Example:**
```c
.@weapon = getequipid(EQI_HAND_R);
if (.@weapon > 0)
    mes "You have " + getitemname(.@weapon) + " equipped.";
```

---

### getequipname
**Syntax:** `getequipname(<slot>{,<char id>})`

Get equipped item's name including cards.

---

### getequiprefinerycnt
**Syntax:** `getequiprefinerycnt(<slot>{,<char id>})`

Get refine level of equipped item.

---

### getequipisenableref
**Syntax:** `getequipisenableref(<slot>{,<char id>})`

Check if equipped item can be refined.

---

### getequipweaponlv
**Syntax:** `getequipweaponlv(<slot>{,<char id>})`

Get weapon level (1-5) of equipped weapon.

---

### getequiparmorlv
**Syntax:** `getequiparmorlv(<slot>{,<char id>})`

Get armor level of equipped armor.

---

### getequipcardcnt
**Syntax:** `getequipcardcnt(<slot>{,<char id>})`

Count cards in equipped item.

---

### getequipcardid
**Syntax:** `getequipcardid(<slot>,<card slot>{,<char id>})`

Get card ID in specific card slot.

---

### getequipuniqueid
**Syntax:** `getequipuniqueid(<slot>{,<char id>})`

Get unique ID of equipped item.

---

<!-- RAG_CHUNK: refine_001 -->
## Refining

### successrefitem
**Syntax:** `successrefitem(<slot>{,<count>{,<char id>}});`

Increase refine level (with animation).

**Example:**
```c
successrefitem(EQI_HAND_R);  // +1 refine to weapon
successrefitem(EQI_ARMOR, 3); // +3 refine to armor
```

---

### failedrefitem
**Syntax:** `failedrefitem(<slot>{,<char id>});`

Break/downgrade equipped item based on settings.

---

### downrefitem
**Syntax:** `downrefitem(<slot>{,<count>{,<char id>}});`

Decrease refine level.

---

### getequippercentrefinery
**Syntax:** `getequippercentrefinery(<slot>{,<enriched>{,<char id>}})`

Get refine success chance percentage.

---

### getequiprefinecost
**Syntax:** `getequiprefinecost(<slot>,<type>,<info>{,<char id>})`

Get refine cost information.

---

### refineui
**Syntax:** `refineui({<char id>});`

Open refine UI window.

---

<!-- RAG_CHUNK: inventory_list_001 -->
## Inventory List

### getinventorylist
**Syntax:** `getinventorylist({<char id>});`

Populate arrays with inventory data.

**Arrays Set:**
```c
@inventorylist_id[]       - Item IDs
@inventorylist_amount[]   - Amounts
@inventorylist_equip[]    - Equip location
@inventorylist_refine[]   - Refine levels
@inventorylist_identify[] - Identified flag
@inventorylist_attribute[] - Broken flag
@inventorylist_card1[]    - Card slot 1
@inventorylist_card2[]    - Card slot 2
@inventorylist_card3[]    - Card slot 3
@inventorylist_card4[]    - Card slot 4
@inventorylist_expire[]   - Expiration time
@inventorylist_bound[]    - Bound type
@inventorylist_idx[]      - Inventory index
@inventorylist_count      - Total count
```

**Example:**
```c
getinventorylist;
for (.@i = 0; .@i < @inventorylist_count; .@i++) {
    mes getitemname(@inventorylist_id[.@i]) + " x" + @inventorylist_amount[.@i];
}
```

---

<!-- RAG_CHUNK: check_commands_001 -->
## Check Commands

### checkweight
**Syntax:** `checkweight(<id>,<amount>{,...})`

Check if player can hold items (weight + inventory space).

**Example:**
```c
if (checkweight(501, 100)) {
    getitem 501, 100;
} else {
    mes "You can't carry this!";
}
```

---

### checkweight2
**Syntax:** `checkweight2(<id array>,<amount array>)`

Check multiple items at once.

**Example:**
```c
setarray .@items[0], 501, 502, 503;
setarray .@amounts[0], 10, 10, 10;
if (checkweight2(.@items, .@amounts)) {
    // Can carry all items
}
```

---

### isequipped
**Syntax:** `isequipped(<id>{,<id>,...})`

Check if ALL specified items/cards are equipped.

**Example:**
```c
if (isequipped(4001, 4001, 4001, 4001))
    mes "Full Poring card set!";
```

---

### isequippedcnt
**Syntax:** `isequippedcnt(<id>{,<id>,...})`

Count how many of specified items/cards are equipped.

---

### checkequipedcard
**Syntax:** `checkequipedcard(<card id>)`

Check if card is in any equipment (equipped or not).

---

#rathena #script #items #getitem #delitem #countitem #equipment #refine #inventory #cards
