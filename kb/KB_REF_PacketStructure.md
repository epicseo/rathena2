# rAthena Packet Structure Reference

**Version:** 2.0
**Last Updated:** 2025
**Scope:** Client-Server Communication in rAthena

---

## Table of Contents

1. [Introduction to Packet System](#1-introduction-to-packet-system)
2. [Packet Naming Conventions](#2-packet-naming-conventions)
3. [CLIF Structure and Functions](#3-clif-structure-and-functions)
4. [Packet Structure Definition](#4-packet-structure-definition)
5. [PACKETVER System](#5-packetver-system)
6. [Packet Registration System](#6-packet-registration-system)
7. [WFIFO/RFIF Macros](#7-wfiforfif-macros)
8. [Creating Custom Packets](#8-creating-custom-packets)
9. [Common Packet Patterns](#9-common-packet-patterns)
10. [Security and Validation](#10-security-and-validation)
11. [Debugging Packets](#11-debugging-packets)
12. [Real-World Examples](#12-real-world-examples)

---

## 1. Introduction to Packet System

The packet system in rAthena handles all client-server communication. Every action in the game—from player movement to chatting, trading, and combat—is transmitted via packets.

### Core Concepts

- **Packets** are binary data structures sent between client and server
- **Packet IDs** (headers) identify the type of packet (e.g., `0x8e` for chat messages)
- **clif.cpp/hpp** contains the main packet handling code for the map server
- **Packet direction** is encoded in the packet name prefix (CZ, ZC, HC, CH)

### File Locations

```
src/map/clif.cpp              # Main packet implementation
src/map/clif.hpp              # Function declarations
src/map/packets.hpp           # Packet structure definitions
src/map/clif_packetdb.hpp     # Packet registration database
src/config/packets.hpp        # PACKETVER configuration
src/common/socket.hpp         # Socket and FIFO macros
```

---

## 2. Packet Naming Conventions

rAthena uses a standardized naming convention for packets based on their direction and purpose.

### Packet Direction Prefixes

| Prefix | Direction | Description |
|--------|-----------|-------------|
| **CZ_** | Client → Zone (Map) Server | Client requests/sends data to map server |
| **ZC_** | Zone (Map) Server → Client | Map server sends data to client |
| **CH_** | Client → Character Server | Client interacts with char server |
| **HC_** | Character Server → Client | Char server responds to client |
| **CA_** | Client → Account (Login) Server | Client authentication |
| **AC_** | Account (Login) Server → Client | Login server responses |
| **SC_** | Server → Client | Generic server-to-client packets |

### Naming Examples

```cpp
// Client sends message to server
struct PACKET_CZ_REQMAKINGITEM { ... };          // Client requests to craft item

// Server sends data to client
struct PACKET_ZC_ITEM_PICKUP_ACK { ... };        // Server confirms item pickup
struct PACKET_ZC_BROADCAST { ... };              // Server sends broadcast message

// Character server packets
struct PACKET_CH_ENTER { ... };                  // Client enters char server
struct PACKET_HC_ACCEPT_ENTER { ... };           // Char server accepts connection
```

### Common Packet Name Patterns

| Pattern | Meaning | Example |
|---------|---------|---------|
| **REQ_** | Request | `PACKET_CZ_REQ_MAKINGARROW` - Request to make arrows |
| **ACK_** | Acknowledgment | `PACKET_ZC_ACK_CASH_BARGAIN_SALE_ITEM_INFO` |
| **NOTIFY_** | Notification | `PACKET_ZC_NOTIFY_PLAYERMOVE` - Notify player movement |
| **ACCEPT_** | Accept/Confirm | `PACKET_ZC_ACCEPT_ENTER` - Accept map entry |
| **REFUSE_** | Refuse/Reject | `PACKET_ZC_REFUSE_ENTER` - Refuse map entry |

---

## 3. CLIF Structure and Functions

The `clif` (Client Interface) module handles all packet transmission and reception for the map server.

### Function Naming Convention

```cpp
// SEND functions (server → client)
void clif_*               // Functions that SEND packets to client
void clif_displaymessage  // Send message to client
void clif_additem         // Send item add notification
void clif_skillinfo       // Send skill information

// PARSE functions (client → server)
void clif_parse_*         // Functions that PARSE packets from client
void clif_parse_WalkToXY      // Parse walk request
void clif_parse_GlobalMessage // Parse chat message
void clif_parse_DropItem      // Parse drop item request
```

### CLIF Send Functions

**Purpose:** Send packets FROM server TO client

**Pattern:**
```cpp
void clif_<action>(map_session_data *sd, <parameters>)
{
    int32 fd = sd->fd;  // Get file descriptor

    // Allocate buffer space
    WFIFOHEAD(fd, <packet_size>);

    // Write packet data
    WFIFOW(fd, 0) = <packet_id>;
    WFIFOW(fd, 2) = <packet_length>;
    // ... write more fields

    // Send packet
    WFIFOSET(fd, <packet_size>);
}
```

**Example:**
```cpp
// From src/map/clif.cpp
void clif_displaymessage(const int32 fd, const char* mes)
{
    nullpo_retv(mes);

    if (session_isActive(fd)) {
        int16 len = strnlen(mes, CHAT_SIZE_MAX);

        if (len > 0) {
            WFIFOHEAD(fd, 5 + len);
            WFIFOW(fd, 0) = 0x8e;           // Packet ID
            WFIFOW(fd, 2) = 5 + len;        // Packet length
            safestrncpy(WFIFOCP(fd, 4), mes, len + 1);
            WFIFOSET(fd, 5 + len);
        }
    }
}
```

### CLIF Parse Functions

**Purpose:** Parse packets FROM client, process request

**Pattern:**
```cpp
void clif_parse_<Action>(int32 fd, map_session_data *sd)
{
    // Validate player state
    if (pc_isdead(sd)) return;
    if (pc_cant_act(sd)) return;

    // Read packet data
    uint16 field1 = RFIFOW(fd, <offset>);
    uint32 field2 = RFIFOL(fd, <offset>);

    // Process request
    // Call game logic functions

    // Send response (if needed)
    clif_<response>(sd, ...);
}
```

**Example:**
```cpp
// From src/map/clif.cpp
void clif_parse_WalkToXY(int32 fd, map_session_data *sd)
{
    int16 x, y;

    // Validate state
    if (pc_isdead(sd)) {
        clif_clearunit_area(*sd, CLR_DEAD);
        return;
    }

    if (pc_cant_act(sd))
        return;

    // Parse position from packet
    RFIFOPOS(fd, packet_db[RFIFOW(fd, 0)].pos[0], &x, &y, nullptr);

    // Process movement
    unit_walktoxy(&sd->bl, x, y, 4);
}
```

---

## 4. Packet Structure Definition

Packet structures in rAthena are defined using C structs with specific attributes to ensure proper memory layout.

### Basic Packet Structure

```cpp
struct PACKET_<NAME> {
    int16 packetType;      // Packet ID (always first field)
    // ... other fields
} __attribute__((packed));
DEFINE_PACKET_HEADER(<NAME>, <packet_id>)
```

### The `__attribute__((packed))` Attribute

**Critical:** This attribute prevents compiler padding, ensuring the struct matches the exact binary layout expected by the client.

```cpp
// WITHOUT __attribute__((packed)) - WRONG!
struct BAD_PACKET {
    int16 packetType;  // offset 0-1
    // PADDING bytes 2-3 (compiler adds this)
    int32 value;       // offset 4-7
};  // Total: 8 bytes

// WITH __attribute__((packed)) - CORRECT!
struct GOOD_PACKET {
    int16 packetType;  // offset 0-1
    int32 value;       // offset 2-5
} __attribute__((packed));  // Total: 6 bytes
```

### Fixed-Length Packets

```cpp
// Fixed-length packet example
struct PACKET_ZC_RESTART_ACK {
    int16 packetType;   // 2 bytes - packet ID
    uint8 type;         // 1 byte  - restart type
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_RESTART_ACK, 0xb3)
// Total size: 3 bytes
```

### Variable-Length Packets

```cpp
// Variable-length packet with dynamic data
struct PACKET_ZC_BROADCAST {
    int16 packetType;   // 2 bytes - packet ID
    int16 packetLength; // 2 bytes - total packet length
    char message[];     // Variable length message
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_BROADCAST, 0x9a)

// Usage:
// Total size = 4 + strlen(message) + 1
```

### Nested Structures (Sub-packets)

```cpp
// Sub-structure for repeated data
struct PACKET_ZC_FRIENDS_LIST_sub {
    uint32 AID;        // Account ID
    uint32 CID;        // Character ID
    char name[NAME_LENGTH];
} __attribute__((packed));

// Main packet using sub-structure
struct PACKET_ZC_FRIENDS_LIST {
    int16 packetType;
    int16 packetLength;
    struct PACKET_ZC_FRIENDS_LIST_sub friends[];  // Array of friends
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_FRIENDS_LIST, 0x201)
```

### PACKETVER-Conditional Fields

```cpp
// Different structure based on client version
struct PACKET_CZ_REQ_MAKINGARROW {
    int16 packetType;
#if PACKETVER_MAIN_NUM >= 20181121 || PACKETVER_RE_NUM >= 20180704 || PACKETVER_ZERO_NUM >= 20181114
    uint32 itemId;      // Newer clients: 4-byte item ID
#else
    uint16 itemId;      // Older clients: 2-byte item ID
#endif
} __attribute__((packed));
DEFINE_PACKET_HEADER(CZ_REQ_MAKINGARROW, 0x1ae)
```

### Complete Example: Banking Packet

```cpp
// Client requests bank deposit
struct PACKET_CZ_REQ_BANKING_DEPOSIT {
    int16 packetType;   // Offset 0-1: Packet ID
    uint32 AID;         // Offset 2-5: Account ID
    int32 zeny;         // Offset 6-9: Amount to deposit
} __attribute__((packed));
// Total size: 10 bytes
```

---

## 5. PACKETVER System

The PACKETVER system allows rAthena to support multiple client versions with different packet structures.

### PACKETVER Configuration

**File:** `src/config/packets.hpp`

```cpp
#ifndef PACKETVER
    // Default client version: 2021-11-03
    #define PACKETVER 20211103
#endif

// Automatic Renewal detection
#ifndef PACKETVER_RE
    #if (PACKETVER > 20151104 && PACKETVER < 20180704) ||
        (PACKETVER >= 20200902 && PACKETVER <= 20211118)
        #define PACKETVER_RE
    #endif
#endif
```

### Setting PACKETVER

**Windows:**
```cpp
// In src/custom/defines_pre.hpp
#define PACKETVER 20211103
```

**Linux:**
```bash
./configure --enable-packetver=20211103
make clean
make server
```

### PACKETVER Variants

```cpp
PACKETVER               // Base packet version (YYYYMMDD format)
PACKETVER_MAIN_NUM      // Main server packet version
PACKETVER_RE_NUM        // Renewal server packet version
PACKETVER_ZERO_NUM      // Zero server packet version
```

### Version-Specific Code

```cpp
// Different packet structures for different versions
#if PACKETVER < 20080102
struct PACKET_ZC_ACCEPT_ENTER {
    int16 packetType;
    uint32 startTime;
    uint8 posDir[3];
    uint8 xSize;
    uint8 ySize;
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_ACCEPT_ENTER, 0x73)

#elif PACKETVER < 20141022 || PACKETVER >= 20160330
struct PACKET_ZC_ACCEPT_ENTER {
    int16 packetType;
    uint32 startTime;
    uint8 posDir[3];
    uint8 xSize;
    uint8 ySize;
    uint16 font;        // Font field added
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_ACCEPT_ENTER, 0x2eb)

#else
struct PACKET_ZC_ACCEPT_ENTER {
    int16 packetType;
    uint32 startTime;
    uint8 posDir[3];
    uint8 xSize;
    uint8 ySize;
    uint16 font;
    uint8 sex;          // Sex field added
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_ACCEPT_ENTER, 0xa18)
#endif
```

### PACKETVER Feature Flags

```cpp
// Feature availability checks
#define PACKETVER_SUPPORTS_PINCODE (PACKETVER >= 20110309)
#define PACKETVER_SUPPORTS_SALES (PACKETVER >= 20131223)
#define WEB_SERVER_ENABLE (PACKETVER > 20200300)

// Usage:
#if PACKETVER_SUPPORTS_PINCODE
    // Pincode system code
#endif
```

### Common PACKETVER Checks

```cpp
// Item ID size changed
#if PACKETVER_MAIN_NUM >= 20181121 || PACKETVER_RE_NUM >= 20180704 || PACKETVER_ZERO_NUM >= 20181114
    uint32 itemId;  // 4 bytes
#else
    uint32 itemId;  // 2 bytes
#endif

// String termination changed
#if PACKETVER < 20151001
    // Message must be null-terminated
#else
    // No null termination
#endif
```

---

## 6. Packet Registration System

Packets are registered in `clif_packetdb.hpp` to link packet IDs to their handler functions.

### Packet Database Structure

**File:** `src/map/clif.hpp`

```cpp
struct s_packet_db {
    int16 len;                              // Packet length (-1 = variable)
    void (*func)(int32, map_session_data *); // Handler function
    int16 pos[MAX_PACKET_POS];              // Field positions for parsing
};

extern struct s_packet_db packet_db[MAX_PACKET_DB + 1];
```

### Registration Macros

**File:** `src/map/clif_packetdb.hpp`

```cpp
// Simple packet registration (no handler)
#define packet(cmd, length) \
    packetdb_addpacket(cmd, length, nullptr, 0)

// Parseable packet registration (with handler)
#define parseable_packet(cmd, length, func, ...) \
    packetdb_addpacket(cmd, length, func, __VA_ARGS__, 0)
```

### Registration Examples

```cpp
// Fixed-length packet without handler
packet(0x0064, 55);           // Length: 55 bytes, no handler

// Variable-length packet without handler
packet(0x0069, -1);           // Length: variable (-1)

// Fixed-length packet WITH handler and field positions
parseable_packet(0x0072, 19, clif_parse_WantToConnection, 2, 6, 10, 14, 18);
//                ^      ^   ^                              ^  ^  ^   ^   ^
//              ID     Len  Handler function              Field positions
```

### Field Position System

The position array tells the parser where to find specific fields in the packet:

```cpp
// Example: Walk packet
parseable_packet(0x0085, 5, clif_parse_WalkToXY, 2);
//                                                 ^
//                                                 Position data starts at byte 2

// In the handler:
void clif_parse_WalkToXY(int32 fd, map_session_data *sd) {
    int16 x, y;
    // Use position from packet_db
    RFIFOPOS(fd, packet_db[RFIFOW(fd, 0)].pos[0], &x, &y, nullptr);
    //                                      ^^^^
    //                                      pos[0] = 2
}
```

### Common Registration Patterns

```cpp
// Chat message: variable length, handler with positions
parseable_packet(0x008c, -1, clif_parse_GlobalMessage, 2, 4);
//                       ^^                             ^  ^
//                    Variable                    pos[0] pos[1]

// Item use: fixed length with positions
parseable_packet(0x00a7, 8, clif_parse_UseItem, 2, 4);
//                       ^                       ^  ^
//                    8 bytes              index  amount

// Skill use: positions for skill ID, target, level
parseable_packet(0x0113, 10, clif_parse_UseSkillToId, 2, 4, 6);
//                           ^                         ^  ^  ^
//                         Handler                  skill target level

// NPC click: using HEADER constant and sizeof
parseable_packet(HEADER_CZ_CONTACTNPC, sizeof(PACKET_CZ_CONTACTNPC),
                 clif_parse_NpcClicked, 0);
```

### Adding Packets to Database

**Function:** `packetdb_addpacket`

```cpp
void packetdb_addpacket(uint16 cmd, uint16 length,
                        void (*func)(int32, map_session_data *), ...)
{
    va_list argp;
    int32 i;

    if (cmd <= 0 || cmd > MAX_PACKET_DB)
        return;

    packet_db[cmd].len = length;
    packet_db[cmd].func = func;

    // Read field positions from variable arguments
    va_start(argp, func);
    for (i = 0; i < MAX_PACKET_POS; i++) {
        int32 offset = va_arg(argp, int32);
        if (offset == 0)
            break;
        packet_db[cmd].pos[i] = offset;
    }
    va_end(argp);
}
```

### Complete Registration Example

```cpp
// In clif_packetdb.hpp

// 1. Trade request packet
parseable_packet(0x00e4, 6, clif_parse_TradeRequest, 2);

// 2. Trade item addition
parseable_packet(HEADER_CZ_ADD_EXCHANGE_ITEM,
                 sizeof(PACKET_CZ_ADD_EXCHANGE_ITEM),
                 clif_parse_TradeAddItem, 0);

// 3. Party message (variable length)
parseable_packet(0x0108, -1, clif_parse_PartyMessage, 2, 4);
```

---

## 7. WFIFO/RFIF Macros

Socket I/O macros for reading from and writing to network buffers.

### Core FIFO Macros

**File:** `src/common/socket.hpp`

```cpp
// Write FIFO (Server → Client)
WFIFOHEAD(fd, size)      // Allocate buffer space
WFIFOP(fd, pos)          // Get pointer at position
WFIFOB(fd, pos)          // Read/Write uint8 (1 byte)
WFIFOW(fd, pos)          // Read/Write uint16 (2 bytes)
WFIFOL(fd, pos)          // Read/Write uint32 (4 bytes)
WFIFOQ(fd, pos)          // Read/Write uint64 (8 bytes)
WFIFOCP(fd, pos)         // Get char pointer at position
WFIFOSET(fd, len)        // Finalize and send packet

// Read FIFO (Client → Server)
RFIFOP(fd, pos)          // Get pointer at position
RFIFOB(fd, pos)          // Read uint8
RFIFOW(fd, pos)          // Read uint16
RFIFOL(fd, pos)          // Read uint32
RFIFOQ(fd, pos)          // Read uint64
RFIFOCP(fd, pos)         // Get char pointer
RFIFOREST(fd)            // Remaining bytes in buffer
RFIFOSKIP(fd, len)       // Skip bytes in buffer
```

### WFIFO Usage (Sending Packets)

```cpp
void clif_example_send(map_session_data *sd, const char *message)
{
    int32 fd = sd->fd;
    uint16 msg_len = strlen(message) + 1;
    uint16 packet_len = 4 + msg_len;

    // Step 1: Allocate buffer space
    WFIFOHEAD(fd, packet_len);

    // Step 2: Write packet header
    WFIFOW(fd, 0) = 0x8e;          // Packet ID (2 bytes)
    WFIFOW(fd, 2) = packet_len;    // Packet length (2 bytes)

    // Step 3: Write message data
    safestrncpy(WFIFOCP(fd, 4), message, msg_len);

    // Step 4: Send packet
    WFIFOSET(fd, packet_len);
}
```

### RFIF Usage (Receiving Packets)

```cpp
void clif_parse_example(int32 fd, map_session_data *sd)
{
    // Read packet fields
    uint16 packet_id = RFIFOW(fd, 0);     // Byte 0-1: Packet ID
    uint16 item_index = RFIFOW(fd, 2);    // Byte 2-3: Item index
    uint32 amount = RFIFOL(fd, 4);        // Byte 4-7: Amount

    // Read string data
    char message[256];
    safestrncpy(message, RFIFOCP(fd, 8), sizeof(message));

    // Process data
    // ...
}
```

### Buffer Macros (WBUF/RBUF)

For working with pre-allocated buffers instead of session buffers:

```cpp
// Buffer macros (for packet_buffer or custom buffers)
WBUFP(p, pos)           // Get pointer in buffer
WBUFB(p, pos)           // Write uint8
WBUFW(p, pos)           // Write uint16
WBUFL(p, pos)           // Write uint32
WBUFQ(p, pos)           // Write uint64

RBUFP(p, pos)           // Get pointer in buffer
RBUFB(p, pos)           // Read uint8
RBUFW(p, pos)           // Read uint16
RBUFL(p, pos)           // Read uint32
RBUFQ(p, pos)           // Read uint64
```

### Using Packet Buffer

```cpp
// Global packet buffer for reusable storage
extern int8 packet_buffer[UINT16_MAX];

void clif_example_with_buffer(map_session_data *sd)
{
    PACKET_ZC_BROADCAST *p = (PACKET_ZC_BROADCAST*)packet_buffer;

    // Build packet in buffer
    p->packetType = HEADER_ZC_BROADCAST;
    p->packetLength = sizeof(PACKET_ZC_BROADCAST) + 20;
    strcpy(p->message, "Hello World!");

    // Send from buffer
    clif_send(p, p->packetLength, &sd->bl, SELF);
}
```

### Position Encoding Macros

Special macros for encoding/decoding coordinate data:

```cpp
// Write position to buffer
WBUFPOS(p, pos, x, y, dir)      // Encode x, y, direction (3 bytes)
WBUFPOS2(p, pos, ...)           // Encode movement path (6 bytes)

// Write position to FIFO
WFIFOPOS(fd, pos, x, y, dir)

// Read position from buffer
RBUFPOS(p, pos, &x, &y, &dir)
RBUFPOS2(p, pos, ...)

// Read position from FIFO
RFIFOPOS(fd, pos, &x, &y, &dir)
```

### Position Encoding Example

```cpp
// From src/map/clif.cpp
static inline void WBUFPOS(uint8* p, uint16 pos, int16 x, int16 y, unsigned char dir)
{
    p += pos;
    p[0] = (uint8)(x >> 2);
    p[1] = (uint8)((x << 6) | ((y >> 4) & 0x3f));
    p[2] = (uint8)((y << 4) | (dir & 0xf));
}

// Usage in movement packet
void clif_send_move(map_session_data *sd, int16 x, int16 y, uint8 dir)
{
    int fd = sd->fd;
    WFIFOHEAD(fd, 10);
    WFIFOW(fd, 0) = 0x87;           // Movement packet
    WFIFOL(fd, 2) = gettick();      // Timestamp
    WFIFOPOS(fd, 6, x, y, dir);     // Encode position (3 bytes)
    WFIFOSET(fd, 10);
}
```

### Complete Send Example

```cpp
// Real example from clif_displaymessage
void clif_displaymessage(const int32 fd, const char* mes)
{
    int16 len = strnlen(mes, CHAT_SIZE_MAX);

    if (len > 0) {
        // 1. Allocate buffer
        WFIFOHEAD(fd, 5 + len);

        // 2. Write header
        WFIFOW(fd, 0) = 0x8e;        // Packet ID
        WFIFOW(fd, 2) = 5 + len;     // Total length

        // 3. Write string
        safestrncpy(WFIFOCP(fd, 4), mes, len + 1);

        // 4. Send
        WFIFOSET(fd, 5 + len);
    }
}
```

---

## 8. Creating Custom Packets

Step-by-step guide to creating new packets for custom features.

### Step 1: Choose Packet ID

**Rules:**
- Use packet IDs in the custom range: `0x0CFF` and above
- Check existing packets to avoid conflicts
- Document your packet ID choice

```cpp
// Good choices for custom packets:
0x0d00, 0x0d01, 0x0d02, ...
0x9000, 0x9001, 0x9002, ...
```

### Step 2: Define Packet Structure

**File:** `src/map/packets.hpp`

```cpp
// Example: Custom quest notification packet

// Client requests quest info
struct PACKET_CZ_CUSTOM_QUEST_INFO {
    int16 packetType;
    uint32 questId;
} __attribute__((packed));
DEFINE_PACKET_HEADER(CZ_CUSTOM_QUEST_INFO, 0x0d00)

// Server sends quest data
struct PACKET_ZC_CUSTOM_QUEST_DATA {
    int16 packetType;
    int16 packetLength;
    uint32 questId;
    uint32 mobId;
    uint16 killCount;
    uint16 killRequired;
    char questName[50];
    char description[200];
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_CUSTOM_QUEST_DATA, 0x0d01)
```

### Step 3: Register Packet

**File:** `src/map/clif_packetdb.hpp`

```cpp
// Add at the end of the file, before #endif

// Register client→server packet
parseable_packet(HEADER_CZ_CUSTOM_QUEST_INFO,
                 sizeof(PACKET_CZ_CUSTOM_QUEST_INFO),
                 clif_parse_custom_quest_info, 0);

// Server→client packets don't need registration (send only)
```

### Step 4: Implement Parser (Client → Server)

**File:** `src/map/clif.cpp`

```cpp
/// Request quest information
/// 0d00 <quest id>.L (CZ_CUSTOM_QUEST_INFO)
void clif_parse_custom_quest_info(int32 fd, map_session_data *sd)
{
    // Validate player state
    if (!sd || !sd->bl.prev)
        return;

    // Read packet data
    const PACKET_CZ_CUSTOM_QUEST_INFO *p =
        (PACKET_CZ_CUSTOM_QUEST_INFO*)RFIFOP(fd, 0);

    uint32 quest_id = p->questId;

    // Validate quest ID
    if (quest_id == 0 || quest_id > MAX_QUEST_DB) {
        ShowWarning("clif_parse_custom_quest_info: Invalid quest ID %u from player %s\n",
                    quest_id, sd->status.name);
        return;
    }

    // Process quest request
    // ... your logic here ...

    // Send response
    clif_custom_quest_data(sd, quest_id);
}
```

### Step 5: Implement Sender (Server → Client)

**File:** `src/map/clif.cpp`

```cpp
/// Send quest information to client
/// 0d01 <packet len>.W <quest id>.L <mob id>.L <kill count>.W <required>.W
///      <name>.50B <description>.200B (ZC_CUSTOM_QUEST_DATA)
void clif_custom_quest_data(map_session_data *sd, uint32 quest_id)
{
    nullpo_retv(sd);

    int32 fd = sd->fd;
    if (!session_isActive(fd))
        return;

    // Get quest data from database
    struct quest_db *quest = quest_search(quest_id);
    if (!quest)
        return;

    // Build packet
    PACKET_ZC_CUSTOM_QUEST_DATA p = {};

    p.packetType = HEADER_ZC_CUSTOM_QUEST_DATA;
    p.packetLength = sizeof(PACKET_ZC_CUSTOM_QUEST_DATA);
    p.questId = quest_id;
    p.mobId = quest->mob_id;
    p.killCount = quest->count;
    p.killRequired = quest->required;
    safestrncpy(p.questName, quest->name, sizeof(p.questName));
    safestrncpy(p.description, quest->desc, sizeof(p.description));

    // Send packet
    WFIFOHEAD(fd, p.packetLength);
    memcpy(WFIFOP(fd, 0), &p, p.packetLength);
    WFIFOSET(fd, p.packetLength);
}
```

### Step 6: Add Function Declaration

**File:** `src/map/clif.hpp`

```cpp
// Add near other clif_parse_* declarations
void clif_parse_custom_quest_info(int32 fd, map_session_data *sd);

// Add near other clif_* declarations
void clif_custom_quest_data(map_session_data *sd, uint32 quest_id);
```

### Step 7: Usage in Game Code

```cpp
// In your quest system code
void quest_show_info(map_session_data *sd, uint32 quest_id)
{
    // Send quest data to player
    clif_custom_quest_data(sd, quest_id);
}

// Triggered by script command
BUILDIN_FUNC(showquestinfo)
{
    map_session_data *sd = script_rid2sd(st);
    uint32 quest_id = script_getnum(st, 2);

    if (sd)
        clif_custom_quest_data(sd, quest_id);

    return SCRIPT_CMD_SUCCESS;
}
```

### Variable-Length Custom Packet Example

```cpp
// Packet with variable-length array
struct PACKET_ZC_CUSTOM_ITEM_LIST_sub {
    uint32 itemId;
    uint16 amount;
} __attribute__((packed));

struct PACKET_ZC_CUSTOM_ITEM_LIST {
    int16 packetType;
    int16 packetLength;
    uint16 itemCount;
    struct PACKET_ZC_CUSTOM_ITEM_LIST_sub items[];
} __attribute__((packed));
DEFINE_PACKET_HEADER(ZC_CUSTOM_ITEM_LIST, 0x0d02)

// Sender implementation
void clif_custom_item_list(map_session_data *sd, uint32 *item_ids, uint16 count)
{
    int32 fd = sd->fd;
    int i;

    // Calculate total packet size
    int packet_len = sizeof(PACKET_ZC_CUSTOM_ITEM_LIST) +
                     (count * sizeof(PACKET_ZC_CUSTOM_ITEM_LIST_sub));

    // Allocate and build packet
    WFIFOHEAD(fd, packet_len);
    WFIFOW(fd, 0) = HEADER_ZC_CUSTOM_ITEM_LIST;
    WFIFOW(fd, 2) = packet_len;
    WFIFOW(fd, 4) = count;

    // Fill item array
    for (i = 0; i < count; i++) {
        int offset = 6 + (i * sizeof(PACKET_ZC_CUSTOM_ITEM_LIST_sub));
        WFIFOL(fd, offset + 0) = item_ids[i];
        WFIFOW(fd, offset + 4) = 1;  // amount
    }

    WFIFOSET(fd, packet_len);
}
```

---

## 9. Common Packet Patterns

### Player Data Packets

```cpp
/// Send player stat update
/// 00b0 <var id>.W <value>.L (ZC_PAR_CHANGE)
void clif_updatestatus(map_session_data *sd, int32 type)
{
    int32 fd = sd->fd;
    int32 len = packet_len(0xb0);

    WFIFOHEAD(fd, len);
    WFIFOW(fd, 0) = 0xb0;
    WFIFOW(fd, 2) = type;   // Status type (SP_*, e.g., SP_HP)

    switch (type) {
        case SP_HP:
            WFIFOL(fd, 4) = sd->battle_status.hp;
            break;
        case SP_MAXHP:
            WFIFOL(fd, 4) = sd->battle_status.max_hp;
            break;
        case SP_SP:
            WFIFOL(fd, 4) = sd->battle_status.sp;
            break;
        // ... more cases
    }

    WFIFOSET(fd, len);
}
```

### Inventory Packets

```cpp
/// Item pickup acknowledgment
void clif_additem(map_session_data *sd, int32 n, int32 amount, unsigned char fail)
{
    int32 fd = sd->fd;

    PACKET_ZC_ITEM_PICKUP_ACK p = {};

    if (fail) {
        // Failed to pickup
        p.result = fail;
    } else {
        // Successful pickup - fill item data
        p.index = client_index(n);
        p.count = amount;
        p.nameid = client_nameid(sd->inventory.u.items_inventory[n].nameid);
        p.IsIdentified = sd->inventory.u.items_inventory[n].identify;
        p.IsDamaged = sd->inventory.u.items_inventory[n].attribute;
        p.refiningLevel = sd->inventory.u.items_inventory[n].refine;
        // ... fill more fields
        p.result = 0;  // Success
    }

    p.packetType = HEADER_ZC_ITEM_PICKUP_ACK;

    WFIFOHEAD(fd, sizeof(p));
    memcpy(WFIFOP(fd, 0), &p, sizeof(p));
    WFIFOSET(fd, sizeof(p));
}
```

### Skill Packets

```cpp
/// Update single skill information
void clif_skillinfo(map_session_data& sd, uint16 skill_id, int32 inf)
{
    uint16 idx = skill_get_index(skill_id);
    if (idx == 0)
        return;

    PACKET_ZC_SKILLINFO_UPDATE2 p = {};

    p.packetType = HEADER_ZC_SKILLINFO_UPDATE2;
    p.id = skill_id;
    p.level = sd.status.skill[idx].lv;
    p.sp = skill_get_sp(skill_id, sd.status.skill[idx].lv);
    p.range = skill_get_range2(&sd.bl, skill_id, sd.status.skill[idx].lv, false);
    p.upgradable = (sd.status.skill[idx].lv < skill_tree_get_max(skill_id, sd.status.class_));

    clif_send(&p, sizeof(p), &sd.bl, SELF);
}
```

### Chat Packets

```cpp
/// Broadcast message to all players
void clif_broadcast(block_list* bl, const char* mes, int32 len, int32 type, enum send_target target)
{
    PACKET_ZC_BROADCAST *packet = (PACKET_ZC_BROADCAST*)packet_buffer;

    packet->packetType = HEADER_ZC_BROADCAST;
    packet->packetLength = sizeof(PACKET_ZC_BROADCAST) + len;
    safestrncpy(packet->message, mes, len);

    clif_send(packet, packet->packetLength, bl, target);
}

/// Parse global chat message from client
void clif_parse_GlobalMessage(int32 fd, map_session_data* sd)
{
    char name[NAME_LENGTH], message[CHAT_SIZE_MAX];
    char output[CHAT_SIZE_MAX + NAME_LENGTH * 2];
    size_t length;

    // Validate and extract message
    if (!clif_process_message(sd, false, name, message, output))
        return;

    // Send to other players
    clif_GlobalMessage(*sd, output, sd->chatID ? CHAT_WOS : AREA_CHAT_WOC);

    // Echo back to sender
    length = strlen(output) + 1;
    WFIFOHEAD(fd, 4 + length);
    WFIFOW(fd, 0) = 0x8e;
    WFIFOW(fd, 2) = 4 + length;
    safestrncpy(WFIFOCP(fd, 4), output, length);
    WFIFOSET(fd, 4 + length);
}
```

### Trade Packets

```cpp
/// Send trade request
void clif_traderequest(map_session_data* sd, const char* name)
{
    int32 fd = sd->fd;

    WFIFOHEAD(fd, 30);
    WFIFOW(fd, 0) = 0xe5;
    safestrncpy(WFIFOCP(fd, 2), name, NAME_LENGTH);
    WFIFOSET(fd, 30);
}

/// Parse trade acknowledgment
void clif_parse_TradeAck(int32 fd, map_session_data *sd)
{
    uint8 response = RFIFOB(fd, packet_db[RFIFOW(fd, 0)].pos[0]);

    trade_tradeack(sd, response);
}
```

### Movement Packets

```cpp
/// Notify player of their own movement
void clif_walkok(map_session_data *sd)
{
    int32 fd = sd->fd;

    WFIFOHEAD(fd, 6);
    WFIFOW(fd, 0) = 0x87;
    WFIFOL(fd, 2) = (uint32)gettick();
    WFIFOSET(fd, 6);
}

/// Parse walk request from client
void clif_parse_WalkToXY(int32 fd, map_session_data *sd)
{
    int16 x, y;

    // Validate state
    if (pc_isdead(sd)) {
        clif_clearunit_area(*sd, CLR_DEAD);
        return;
    }

    if (pc_cant_act(sd))
        return;

    // Parse position
    RFIFOPOS(fd, packet_db[RFIFOW(fd, 0)].pos[0], &x, &y, nullptr);

    // Execute movement
    unit_walktoxy(&sd->bl, x, y, 4);
}
```

---

## 10. Security and Validation

Critical security practices for packet handling to prevent exploits and crashes.

### Input Validation Rules

**Always validate:**
1. Player state (alive, not in action, session active)
2. Packet length (for variable-length packets)
3. Array indices (inventory, skills, etc.)
4. String termination
5. Value ranges (amounts, IDs, etc.)

### Player State Validation

```cpp
void clif_parse_example(int32 fd, map_session_data *sd)
{
    // Check if player exists
    if (!sd)
        return;

    // Check if session is active
    if (!session_isActive(fd))
        return;

    // Check if player is in valid state
    if (!sd->bl.prev)  // Not on map
        return;

    // Check if player is dead
    if (pc_isdead(sd)) {
        clif_clearunit_area(*sd, CLR_DEAD);
        return;
    }

    // Check if player can act
    if (pc_cant_act(sd))
        return;

    // Process packet...
}
```

### Packet Length Validation

```cpp
void clif_parse_variable_packet(int32 fd, map_session_data *sd)
{
    uint16 packet_len = RFIFOW(fd, 2);  // Declared length
    uint16 expected_len;

    // Validate minimum length
    if (packet_len < 4) {
        ShowWarning("Invalid packet length: %u from %s\n",
                    packet_len, sd->status.name);
        return;
    }

    // Validate maximum length
    if (packet_len > 32768) {
        ShowWarning("Packet too large: %u from %s\n",
                    packet_len, sd->status.name);
        return;
    }

    // Check if full packet received
    if (RFIFOREST(fd) < packet_len) {
        return;  // Wait for more data
    }

    // Calculate expected length based on count
    uint16 count = RFIFOW(fd, 4);
    expected_len = 6 + (count * sizeof(struct item_data));

    if (packet_len != expected_len) {
        ShowWarning("Packet length mismatch: got %u, expected %u from %s\n",
                    packet_len, expected_len, sd->status.name);
        return;
    }

    // Process packet...
}
```

### Index Bounds Checking

```cpp
void clif_parse_UseItem(int32 fd, map_session_data *sd)
{
    struct s_packet_db* info = &packet_db[RFIFOW(fd, 0)];
    int32 index = RFIFOW(fd, info->pos[0]) - 2;  // Client index to server index

    // Validate index range
    if (index < 0 || index >= MAX_INVENTORY) {
        clif_useitemack(sd, 0, 0, 0);
        ShowWarning("clif_parse_UseItem: Invalid item index %d from %s\n",
                    index, sd->status.name);
        return;
    }

    // Validate item exists
    if (sd->inventory.u.items_inventory[index].nameid == 0) {
        clif_useitemack(sd, 0, 0, 0);
        return;
    }

    // Process item use
    pc_useitem(sd, index);
}
```

### String Validation

```cpp
bool clif_process_message(map_session_data *sd, bool whisperFormat,
                          char *out_name, char *out_message, char *out_output)
{
    char *input = (char*)RFIFOP(fd, 4);
    size_t inputLength = RFIFOW(fd, 2) - 4;
    size_t nameLength, messageLength;

    // Validate input length
    if (inputLength < 1) {
        ShowWarning("clif_process_message: Empty message from %s\n",
                    sd->status.name);
        return false;
    }

    if (whisperFormat) {
        // Name has fixed width
        if (inputLength < NAME_LENGTH + 1) {
            ShowWarning("clif_process_message: Malformed packet from %s\n",
                        sd->status.name);
            return false;
        }

        // Validate name is null-terminated
        nameLength = strnlen(input, NAME_LENGTH - 1);
        if (input[nameLength] != '\0') {
            ShowWarning("clif_process_message: Unterminated name from %s\n",
                        sd->status.name);
            return false;
        }

        safestrncpy(out_name, input, NAME_LENGTH);
        input += NAME_LENGTH;
    }

    // Validate message length
    messageLength = inputLength - (whisperFormat ? NAME_LENGTH : 0);
    if (messageLength > CHAT_SIZE_MAX - 1) {
        ShowWarning("clif_process_message: Message too long from %s\n",
                    sd->status.name);
        return false;
    }

#if PACKETVER < 20151001
    // Validate null termination
    if (input[messageLength - 1] != '\0') {
        ShowWarning("clif_process_message: Unterminated message from %s\n",
                    sd->status.name);
        return false;
    }
#endif

    safestrncpy(out_message, input, messageLength);
    return true;
}
```

### Value Range Validation

```cpp
void clif_parse_StatusUp(int32 fd, map_session_data *sd)
{
    uint16 status_type = RFIFOW(fd, 2);
    uint8 increase_amount = RFIFOB(fd, 4);

    // Validate status type
    if (status_type < SP_STR || status_type > SP_LUK) {
        ShowWarning("clif_parse_StatusUp: Invalid status type %u from %s\n",
                    status_type, sd->status.name);
        return;
    }

    // Validate increase amount
    if (increase_amount < 1 || increase_amount > 100) {
        ShowWarning("clif_parse_StatusUp: Invalid amount %u from %s\n",
                    increase_amount, sd->status.name);
        return;
    }

    // Process status increase
    pc_statusup(sd, status_type, increase_amount);
}
```

### Duplicate Action Prevention

```cpp
void clif_parse_TradeRequest(int32 fd, map_session_data *sd)
{
    map_session_data *target_sd;
    uint32 target_id = RFIFOL(fd, 2);

    // Check if already in trade
    if (sd->state.trading) {
        clif_tradestart(sd, 2);  // Already in trade
        return;
    }

    // Check if in other activities
    if (sd->npc_id || sd->state.vending || sd->state.buyingstore) {
        clif_tradestart(sd, 2);
        return;
    }

    // Validate target
    target_sd = map_id2sd(target_id);
    if (!target_sd || !target_sd->bl.prev) {
        clif_tradestart(sd, 1);  // Target not found
        return;
    }

    // Process trade request
    trade_traderequest(sd, target_sd);
}
```

### Session Validation

```cpp
void clif_example_send(map_session_data *sd)
{
    nullpo_retv(sd);

    int32 fd = sd->fd;

    // Always check session is active before sending
    if (!session_isActive(fd))
        return;

    // Check func_parse to ensure it's a player connection
    if (session[fd]->func_parse != clif_parse) {
        ShowError("clif_example_send: Invalid session type\n");
        return;
    }

    // Safe to send packet
    WFIFOHEAD(fd, packet_len);
    // ...
    WFIFOSET(fd, packet_len);
}
```

---

## 11. Debugging Packets

### Enable Packet Logging

**File:** `src/config/packets.hpp`

```cpp
// Uncomment to enable packet dumping
#define DUMP_UNKNOWN_PACKET     // Log unknown packets
#define DUMP_INVALID_PACKET     // Log invalid/malformed packets
```

### ShowDebug Packet Information

```cpp
void clif_parse_example(int32 fd, map_session_data *sd)
{
    // Log packet reception
    ShowDebug("clif_parse_example: Received from %s (AID:%d CID:%d)\n",
              sd->status.name, sd->status.account_id, sd->status.char_id);

    // Dump packet data
    uint16 packet_id = RFIFOW(fd, 0);
    uint16 packet_len = packet_db[packet_id].len;

    if (packet_len == -1)
        packet_len = RFIFOW(fd, 2);

    ShowDebug("Packet 0x%04x, Length: %u\n", packet_id, packet_len);

    // Hex dump
    int i;
    for (i = 0; i < packet_len; i++) {
        ShowDebug("%02X ", RFIFOB(fd, i));
        if ((i + 1) % 16 == 0)
            ShowDebug("\n");
    }
    ShowDebug("\n");
}
```

### Packet Viewer Function

```cpp
void clif_dump_packet(const unsigned char *packet, int32 length, const char *label)
{
    int i;

    ShowInfo("=== Packet Dump: %s ===\n", label);
    ShowInfo("Packet ID: 0x%04x\n", RBUFW(packet, 0));
    ShowInfo("Length: %d bytes\n", length);
    ShowInfo("Raw Data:\n");

    for (i = 0; i < length; i++) {
        printf("%02X ", packet[i]);
        if ((i + 1) % 16 == 0)
            printf("\n");
    }

    if (length % 16 != 0)
        printf("\n");

    ShowInfo("========================\n");
}

// Usage:
void clif_parse_custom(int32 fd, map_session_data *sd)
{
    clif_dump_packet(RFIFOP(fd, 0), packet_db[RFIFOW(fd, 0)].len, "Custom Packet");
    // Process packet...
}
```

### Wireshark Packet Capture

**Setup Wireshark Filter:**
```
tcp.port == 6900
```

**Ragnarok-Specific Dissector:**
1. Save Ragnarok packet definitions
2. Load as Wireshark dissector
3. View packets in human-readable format

**Common Filters:**
```
# Filter by packet ID
tcp.port == 6900 && data[0:2] == 8e:00   # 0x8e (chat)

# Filter by IP
ip.addr == 127.0.0.1 && tcp.port == 6900
```

### Debug Commands

```cpp
// In clif.cpp - add debug command
ACMD_FUNC(debugpacket)
{
    if (!message || !*message) {
        clif_displaymessage(fd, "Usage: @debugpacket <on|off>");
        return COMMAND_FAILURE;
    }

    if (strcmpi(message, "on") == 0) {
        sd->debug_packet = 1;
        clif_displaymessage(fd, "Packet debugging enabled.");
    } else {
        sd->debug_packet = 0;
        clif_displaymessage(fd, "Packet debugging disabled.");
    }

    return COMMAND_SUCCESS;
}

// In packet handlers
void clif_parse_example(int32 fd, map_session_data *sd)
{
    if (sd->debug_packet) {
        clif_dump_packet(RFIFOP(fd, 0), packet_db[RFIFOW(fd, 0)].len,
                        "clif_parse_example");
    }
    // Process packet...
}
```

### Logging Packet Flow

```cpp
// Add to src/map/log.cpp
void log_packet(map_session_data *sd, uint16 packet_id, bool incoming,
                const void *data, size_t len)
{
    if (!log_config.enable_packet_log)
        return;

    FILE *fp = fopen("log/packets.log", "a");
    if (!fp)
        return;

    time_t now = time(nullptr);
    struct tm *t = localtime(&now);

    fprintf(fp, "[%04d-%02d-%02d %02d:%02d:%02d] %s Packet 0x%04x (%u bytes) - %s (AID:%d)\n",
            t->tm_year + 1900, t->tm_mon + 1, t->tm_mday,
            t->tm_hour, t->tm_min, t->tm_sec,
            incoming ? "IN " : "OUT",
            packet_id, (uint32)len,
            sd->status.name, sd->status.account_id);

    fclose(fp);
}
```

### Runtime Packet Testing

```cpp
// Test packet sending in-game
ACMD_FUNC(testpacket)
{
    uint16 packet_id;

    if (!message || !*message || sscanf(message, "%hx", &packet_id) != 1) {
        clif_displaymessage(fd, "Usage: @testpacket <packet_id in hex>");
        return COMMAND_FAILURE;
    }

    // Example: send test packet
    WFIFOHEAD(fd, 10);
    WFIFOW(fd, 0) = packet_id;
    WFIFOW(fd, 2) = 10;
    WFIFOL(fd, 4) = 12345;
    WFIFOW(fd, 8) = 999;
    WFIFOSET(fd, 10);

    safesnprintf(atcmd_output, sizeof(atcmd_output),
                 "Sent test packet 0x%04x", packet_id);
    clif_displaymessage(fd, atcmd_output);

    return COMMAND_SUCCESS;
}
```

---

## 12. Real-World Examples

### Example 1: Item Drop System

```cpp
// From src/map/clif.cpp

/// Drop item acknowledgment
/// 00af <index>.W <amount>.W (ZC_ITEM_THROW_ACK)
void clif_dropitem(map_session_data *sd, int32 n, int32 amount)
{
    nullpo_retv(sd);

    int32 fd = sd->fd;

    if (!session_isActive(fd))
        return;

    WFIFOHEAD(fd, 6);
    WFIFOW(fd, 0) = 0xaf;
    WFIFOW(fd, 2) = client_index(n);
    WFIFOW(fd, 4) = (uint16)amount;
    WFIFOSET(fd, 6);
}

/// Request to drop an item
/// 00a2 <index>.W <amount>.W (CZ_ITEM_THROW)
void clif_parse_DropItem(int32 fd, map_session_data *sd)
{
    struct s_packet_db* info = &packet_db[RFIFOW(fd, 0)];
    int32 item_index = RFIFOW(fd, info->pos[0]) - 2;
    int32 item_amount = RFIFOW(fd, info->pos[1]);

    // Validate state
    if (pc_isdead(sd))
        return;

    if (pc_cant_act2(sd) || sd->npc_id)
        return;

    if (sd->state.storage_flag || sd->state.vending || sd->state.buyingstore)
        return;

    // Validate index
    if (item_index < 0 || item_index >= MAX_INVENTORY) {
        clif_dropitem(sd, 0, 0);
        return;
    }

    // Validate amount
    if (item_amount <= 0 || item_amount > sd->inventory.u.items_inventory[item_index].amount) {
        clif_dropitem(sd, 0, 0);
        return;
    }

    // Check if item can be dropped
    if (!pc_candrop(sd, &sd->inventory.u.items_inventory[item_index])) {
        clif_displaymessage(fd, msg_txt(sd, 263)); // This item cannot be dropped.
        return;
    }

    // Drop item
    pc_dropitem(sd, item_index, item_amount);
}
```

### Example 2: Skill System

```cpp
// From src/map/clif.cpp

/// Use skill on target
/// 0113 <level>.W <skill id>.W <target id>.L (CZ_USE_SKILL)
void clif_parse_UseSkillToId(int32 fd, map_session_data *sd)
{
    struct s_packet_db *info = &packet_db[RFIFOW(fd, 0)];
    uint16 skill_lv = RFIFOW(fd, info->pos[0]);
    uint16 skill_id = RFIFOW(fd, info->pos[1]);
    uint32 target_id = RFIFOL(fd, info->pos[2]);

    // Validate state
    if (pc_isdead(sd))
        return;

    if (pc_cant_act2(sd))
        return;

    // Validate skill
    if (skill_lv < 1)
        skill_lv = 1;

    uint16 skill_idx = skill_get_index(skill_id);
    if (skill_idx == 0 || skill_id >= GD_SKILLBASE)
        return;

    // Check if player has skill
    if (skill_lv > sd->status.skill[skill_idx].lv) {
        clif_skill_fail(sd, skill_id, USESKILL_FAIL_LEVEL, 0);
        return;
    }

    // Use skill
    unit_skilluse_id(&sd->bl, target_id, skill_id, skill_lv);
}

/// Skill use acknowledgment
/// 0110 <skill id>.W <btype>.L <damage>.W <target id>.L <result>.B (ZC_NOTIFY_SKILL)
void clif_skill_damage(block_list *src, block_list *dst, t_tick tick,
                       int32 sdelay, int32 ddelay, int64 damage, int32 div,
                       uint16 skill_id, uint16 skill_lv, int32 type)
{
    unsigned char buf[64];
    status_change *sc;

    // Build packet
    WBUFW(buf, 0) = 0x1de;
    WBUFW(buf, 2) = skill_id;
    WBUFL(buf, 4) = src->id;
    WBUFL(buf, 8) = dst->id;
    WBUFL(buf, 12) = (uint32)tick;
    WBUFL(buf, 16) = sdelay;
    WBUFL(buf, 20) = ddelay;

    // Clamp damage for client display
    if (damage > INT_MAX)
        damage = INT_MAX;
    else if (damage < INT_MIN)
        damage = INT_MIN;

    WBUFL(buf, 24) = (int32)damage;
    WBUFW(buf, 28) = skill_lv;
    WBUFW(buf, 30) = div;
    WBUFB(buf, 32) = (type > 0) ? type : skill_get_hit(skill_id);

    // Send to area
    clif_send(buf, 33, dst, AREA);
}
```

### Example 3: Chat System

```cpp
// From src/map/clif.cpp

/// Global message (Chat)
/// 008e <packet len>.W <message>.?B (ZC_NOTIFY_CHAT)
void clif_GlobalMessage(map_session_data& sd, const char *message, send_target target)
{
    size_t len = strlen(message) + 1;

    // Validate length
    if (len > CHAT_SIZE_MAX)
        len = CHAT_SIZE_MAX;

    // Build packet
    WFIFOHEAD(sd.fd, 4 + len);
    WFIFOW(sd.fd, 0) = 0x8e;
    WFIFOW(sd.fd, 2) = 4 + len;
    safestrncpy(WFIFOCP(sd.fd, 4), message, len);

    // Send based on target type
    if (target == SELF)
        WFIFOSET(sd.fd, 4 + len);
    else
        clif_send(WFIFOP(sd.fd, 0), 4 + len, &sd.bl, target);
}

/// Parse global message from client
/// 008c <packet len>.W <message>.?B (CZ_REQUEST_CHAT)
void clif_parse_GlobalMessage(int32 fd, map_session_data* sd)
{
    char name[NAME_LENGTH];
    char message[CHAT_SIZE_MAX];
    char output[CHAT_SIZE_MAX + NAME_LENGTH * 2];
    size_t length;

    // Validate and process message
    if (!clif_process_message(sd, false, name, message, output))
        return;

    // Check if in channel
    if (sd->gcbind && ((sd->gcbind->opt & CHAN_OPT_CAN_CHAT) ||
                       pc_has_permission(sd, PC_PERM_CHANNEL_ADMIN))) {
        channel_send(sd->gcbind, sd, message);
        return;
    }

    // Send to area
    clif_GlobalMessage(*sd, output, sd->chatID ? CHAT_WOS : AREA_CHAT_WOC);

    // Echo back to sender
    length = strlen(output) + 1;
    WFIFOHEAD(fd, 4 + length);
    WFIFOW(fd, 0) = 0x8e;
    WFIFOW(fd, 2) = 4 + length;
    safestrncpy(WFIFOCP(fd, 4), output, length);
    WFIFOSET(fd, 4 + length);

#ifdef PCRE_SUPPORT
    // Trigger NPC chat listeners
    map_foreachinallrange(npc_chat_sub, sd, AREA_SIZE, BL_NPC,
                          output, strlen(output), sd);
#endif
}
```

### Example 4: Banking System

```cpp
// From src/map/clif.cpp

/// Bank deposit request
/// 09a7 <account id>.L <money>.L (CZ_REQ_BANKING_DEPOSIT)
void clif_parse_BankDeposit(int32 fd, map_session_data* sd)
{
    const PACKET_CZ_REQ_BANKING_DEPOSIT *p =
        (PACKET_CZ_REQ_BANKING_DEPOSIT*)RFIFOP(fd, 0);

    int32 money = p->zeny;

    // Validate amount
    if (money <= 0 || money > sd->status.zeny) {
        clif_bank_deposit(sd, BDA_NO_MONEY);
        return;
    }

    // Check for overflow
    if (sd->status.bank_vault + money > MAX_BANK_ZENY) {
        clif_bank_deposit(sd, BDA_OVERFLOW);
        return;
    }

    // Process deposit
    if (pc_payzeny(sd, money, LOG_TYPE_BANK, nullptr) == 0) {
        sd->status.bank_vault += money;
        clif_bank_deposit(sd, BDA_SUCCESS);
    } else {
        clif_bank_deposit(sd, BDA_ERROR);
    }
}

/// Bank deposit result
/// 09a8 <reason>.W <money>.Q <balance>.L (ZC_ACK_BANKING_DEPOSIT)
void clif_bank_deposit(map_session_data *sd, enum e_BANKING_DEPOSIT_ACK reason)
{
    nullpo_retv(sd);

    int32 fd = sd->fd;

    WFIFOHEAD(fd, 16);
    WFIFOW(fd, 0) = 0x9a8;
    WFIFOW(fd, 2) = (uint16)reason;
    WFIFOQ(fd, 4) = sd->status.bank_vault;
    WFIFOL(fd, 12) = sd->status.zeny;
    WFIFOSET(fd, 16);
}
```

### Example 5: Variable-Length Inventory List

```cpp
// From src/map/clif.cpp

/// Send inventory list to client
void clif_inventorylist(map_session_data *sd)
{
    int i, n, ne, fd = sd->fd;
    PACKET_ZC_INVENTORY_ITEMLIST_NORMAL *normal = nullptr;

    // Count items
    for (i = 0, n = 0; i < MAX_INVENTORY; i++) {
        if (sd->inventory.u.items_inventory[i].nameid > 0 &&
            sd->inventory_data[i] &&
            !itemdb_isstackable2(sd->inventory_data[i]))
            n++;
    }

    // Calculate packet size
    int cmd = inventorylistnormalType;
    int packet_len = sizeof(PACKET_ZC_INVENTORY_ITEMLIST_NORMAL) +
                     (n * sizeof(struct NORMALITEM_INFO));

    // Allocate packet
    normal = (PACKET_ZC_INVENTORY_ITEMLIST_NORMAL*)aMalloc(packet_len);
    normal->packetType = cmd;
    normal->packetLength = packet_len;

    // Fill item data
    for (i = 0, n = 0; i < MAX_INVENTORY; i++) {
        if (sd->inventory.u.items_inventory[i].nameid <= 0 ||
            !sd->inventory_data[i] ||
            itemdb_isstackable2(sd->inventory_data[i]))
            continue;

        normal->items[n].index = client_index(i);
        normal->items[n].nameid = client_nameid(sd->inventory.u.items_inventory[i].nameid);
        normal->items[n].type = itemtype(sd->inventory.u.items_inventory[i].nameid);
        normal->items[n].amount = sd->inventory.u.items_inventory[i].amount;
        normal->items[n].location = pc_equippoint(sd, i);
        // ... fill more fields
        n++;
    }

    // Send packet
    clif_send(normal, packet_len, &sd->bl, SELF);
    aFree(normal);
}
```

---

## Summary

This reference covers the complete packet system in rAthena:

1. **Naming conventions** - Understand CZ_*/ZC_* prefixes for packet direction
2. **CLIF structure** - `clif_*` for sending, `clif_parse_*` for receiving
3. **Packet definitions** - Use `__attribute__((packed))` and proper structure
4. **PACKETVER** - Support multiple client versions with conditional compilation
5. **Registration** - Register packets in `clif_packetdb.hpp` with handlers
6. **WFIFO/RFIF macros** - Read and write binary packet data
7. **Custom packets** - Follow 8-step process for new features
8. **Common patterns** - Player data, inventory, skills, chat, movement
9. **Security** - Always validate input, indices, lengths, and state
10. **Debugging** - Use packet logging, Wireshark, and debug commands
11. **Real examples** - Study working code from clif.cpp

**Key Files:**
- `src/map/clif.cpp` - Implementation
- `src/map/clif.hpp` - Declarations
- `src/map/packets.hpp` - Packet structures
- `src/map/clif_packetdb.hpp` - Packet registration
- `src/config/packets.hpp` - PACKETVER settings
- `src/common/socket.hpp` - FIFO macros

**Best Practices:**
- Always use `__attribute__((packed))` on packet structures
- Validate all input from clients
- Check session state before sending
- Use proper WFIFOHEAD before writing
- Test with different PACKETVERs
- Log suspicious activity
- Follow existing patterns

**Next Steps:**
- Study real packets in clif.cpp
- Review packet structures in packets.hpp
- Test custom packets with different clients
- Monitor packet flow with debugging tools
- Contribute documentation for custom features

---

**Document Size:** ~22KB
**Last Updated:** 2025
**Maintained By:** rAthena Community
