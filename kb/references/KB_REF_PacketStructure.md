---
kb_id: KB_REF_027
title: "Packet Structure and Client-Server Communication"
category: Source Code
keywords: [packets, clif, client_server, network, packet_structure, PACKETVER, clif_cpp, packet_obfuscation, custom_packets, network_security]
related_files: [
  "src/map/clif.cpp",
  "src/map/clif.hpp",
  "src/map/packets.hpp",
  "src/map/packets_struct.hpp",
  "src/map/clif_packetdb.hpp",
  "src/config/packets.hpp"
]
difficulty: expert
use_case: "Understanding and modifying client-server packets"
version: rAthena 2024
last_updated: 2024-01-15
---

# Packet Structure and Client-Server Communication

## Quick Reference

### **Basic Packet Structure**
```cpp
struct PACKET_ZC_NOTIFY_CHAT {
    int16 packetType;    // Packet ID (e.g., 0x8e)
    int16 PacketLength;  // Total packet length
    uint32 GID;          // Game ID (who sent it)
    char Message[];      // Variable-length message
} __attribute__((packed));
```

### **Send Packet to Client**
```cpp
// Method 1: Direct send
PACKET_ZC_NOTIFY_CHAT p;
p.packetType = 0x8e;
p.PacketLength = sizeof(p) + strlen(message);
p.GID = sd->bl.id;
strcpy(p.Message, message);
clif->send(&p, p.PacketLength, &sd->bl, SELF);

// Method 2: Helper function
clif_displaymessage(sd->fd, "Hello World!");
```

### **Parse Incoming Packet**
```cpp
void clif_parse_MyCustomPacket(int fd, struct map_session_data *sd) {
    struct PACKET_CZ_MY_CUSTOM *p = (struct PACKET_CZ_MY_CUSTOM*)RFIFOP(fd, 0);

    int value = p->value;
    const char *text = p->text;

    // Process packet data...
}
```

---

## Table of Contents
1. [Packet System Overview](#packet-system-overview)
2. [Packet Structure Basics](#packet-structure-basics)
3. [Packet Naming Convention](#packet-naming-convention)
4. [clif.cpp - Client Interface](#clifcpp-client-interface)
5. [Sending Packets to Client](#sending-packets-to-client)
6. [Receiving Packets from Client](#receiving-packets-from-client)
7. [Adding Custom Packets](#adding-custom-packets)
8. [Packet Version (PACKETVER)](#packet-version-packetver)
9. [Packet Obfuscation](#packet-obfuscation)
10. [Security Considerations](#security-considerations)
11. [Debugging Packets](#debugging-packets)

---

## Packet System Overview

### **What are Packets?**

**Packets** are structured data exchanged between:
- **Client** (Ragnarok Online game client)
- **Server** (rAthena map-server, char-server, login-server)

**Packet Flow**:
```
Client → Network → Server: CZ_* packets (Client to Zone)
Server → Network → Client: ZC_* packets (Zone to Client)

Example:
1. Player clicks on NPC → Client sends PACKET_CZ_CONTACTNPC
2. Server processes NPC dialog → Server sends PACKET_ZC_SAY_DIALOG
3. Player clicks "Next" → Client sends PACKET_CZ_NPC_NEXT_CLICKED
4. And so on...
```

---

### **Packet Directions**

| Prefix | Direction | Description |
|--------|-----------|-------------|
| **CZ** | Client → Zone (map-server) | Client requests or sends data |
| **ZC** | Zone → Client | Server sends data to client |
| **CA** | Client → Account (login-server) | Login requests |
| **AC** | Account → Client | Login responses |
| **CH** | Client → Character (char-server) | Character selection |
| **HC** | Character → Client | Character list, creation |
| **AH** | Account → Character | Inter-server (login to char) |
| **HA** | Character → Account | Inter-server (char to login) |
| **HZ** | Character → Zone | Inter-server (char to map) |
| **ZH** | Zone → Character | Inter-server (map to char) |

---

### **Key Files**

| File | Purpose |
|------|---------|
| `src/map/clif.cpp` | Main packet handling (20,000+ lines) |
| `src/map/clif.hpp` | Function prototypes for clif.cpp |
| `src/map/packets.hpp` | Packet ID definitions (HEADER_*) |
| `src/map/packets_struct.hpp` | Packet structure definitions |
| `src/map/clif_packetdb.hpp` | Packet registration (packet() macro) |
| `src/config/packets.hpp` | PACKETVER configuration |

---

## Packet Structure Basics

### **Fixed-Length Packet**

```cpp
// Example: PACKET_CZ_REQ_EMOTION (client sends emotion)
struct PACKET_CZ_REQ_EMOTION {
    int16 packetType;    // 0x00bf (2 bytes)
    uint8 type;          // Emotion type (1 byte)
} __attribute__((packed));

// Total size: 3 bytes (always)
```

---

### **Variable-Length Packet**

```cpp
// Example: PACKET_ZC_NOTIFY_CHAT (chat message)
struct PACKET_ZC_NOTIFY_CHAT {
    int16 packetType;    // 0x8e (2 bytes)
    int16 PacketLength;  // Total packet length (2 bytes)
    uint32 GID;          // Sender ID (4 bytes)
    char Message[];      // Variable-length message (N bytes)
} __attribute__((packed));

// Total size: 8 + strlen(Message) + 1 (for null terminator)
```

**Variable-Length Indicator**:
```cpp
// In clif_packetdb.hpp:
packet(0x8e, -1);  // -1 means variable-length
```

---

### **Packet Alignment**

**Important**: Use `__attribute__((packed))` to prevent compiler padding!

```cpp
// ❌ WRONG - Compiler may add padding
struct PACKET_WRONG {
    int16 packetType;  // 2 bytes
    uint8 value1;      // 1 byte
    uint32 value2;     // 4 bytes (may be aligned to 4-byte boundary → 1 byte padding!)
};
// Size: might be 8 bytes instead of 7!

// ✅ CORRECT - No padding
struct PACKET_CORRECT {
    int16 packetType;
    uint8 value1;
    uint32 value2;
} __attribute__((packed));
// Size: exactly 7 bytes
```

---

## Packet Naming Convention

### **Naming Pattern**

```
PACKET_<Direction>_<Purpose>

Examples:
- PACKET_CZ_REQ_WEAR_EQUIP      // Client requests to equip item
- PACKET_ZC_ACK_WEAR_EQUIP      // Server acknowledges equip
- PACKET_CZ_CONTACTNPC          // Client clicks on NPC
- PACKET_ZC_SAY_DIALOG          // Server sends NPC dialog
```

---

### **Common Keywords**

| Keyword | Meaning |
|---------|---------|
| **REQ** | Request (client asks for something) |
| **ACK** | Acknowledge (server confirms) |
| **NOTIFY** | Notification (informational) |
| **ADD** | Add/Create |
| **DEL** | Delete/Remove |
| **ENTER** | Enter (map, room, etc.) |
| **LEAVE** | Leave/Exit |
| **STATUS** | Status update |

---

## clif.cpp - Client Interface

### **Overview**

**clif.cpp** is the largest file in rAthena (~20,000 lines):
- **Sends** packets to clients (`clif_*` functions)
- **Receives** and parses packets from clients (`clif_parse_*` functions)
- **Handles** all client-server communication

**Location**: `src/map/clif.cpp`

---

### **Function Types**

**1. Sending Functions** (`clif_*`):
```cpp
// Send chat message to client
void clif_displaymessage(int fd, const char* mes);

// Send item list to client
void clif_inventorylist(struct map_session_data *sd);

// Send skill cast notification
void clif_skillcasting(struct block_list* bl, int src_id, int dst_id,
                       int dst_x, int dst_y, uint16 skill_id, int element,
                       uint32 casttime);
```

**2. Parsing Functions** (`clif_parse_*`):
```cpp
// Parse client request to equip item
void clif_parse_EquipItem(int fd, struct map_session_data *sd);

// Parse client request to use skill
void clif_parse_UseSkillToId(int fd, struct map_session_data *sd);

// Parse client chat message
void clif_parse_GlobalMessage(int fd, struct map_session_data *sd);
```

---

### **Common clif Functions**

```cpp
// Chat & Messages
clif_displaymessage(fd, "message");        // Send message to player
clif_GlobalMessage(&sd->bl, message);      // Broadcast chat
clif_broadcast(&bl, message, len, type, area);  // Area broadcast

// Items
clif_additem(sd, n, amount, result);       // Add item to inventory
clif_dropitem(sd, n, amount);              // Drop item
clif_inventorylist(sd);                    // Send full inventory

// Skills
clif_skillcasting(&bl, src_id, dst_id, x, y, skill_id, element, casttime);
clif_skill_nodamage(&src->bl, &dst->bl, skill_id, heal, result);

// Status
clif_updatestatus(sd, SP_HP);              // Update HP
clif_updatestatus(sd, SP_SP);              // Update SP

// Movement
clif_fixpos(&bl);                          // Fix position (anti-teleport hack)
clif_slide(&bl, x, y);                     // Slide to position

// Effects
clif_specialeffect(&bl, effect_id, area);  // Play visual effect
clif_emotion(&bl, emotion_type);           // Show emotion

// NPC
clif_scriptmes(sd, npc_id, message);       // NPC dialog
clif_scriptmenu(sd, npc_id, menu);         // NPC menu
clif_scriptclose(sd, npc_id);              // Close NPC dialog
```

---

## Sending Packets to Client

### **Method 1: Direct Packet Send**

```cpp
void send_custom_message(struct map_session_data *sd, const char *message) {
    struct PACKET_ZC_NOTIFY_CHAT p;

    p.packetType = 0x8e;
    p.PacketLength = sizeof(p) + strlen(message) + 1;
    p.GID = sd->bl.id;
    strcpy(p.Message, message);

    clif->send(&p, p.PacketLength, &sd->bl, SELF);
}
```

---

### **Method 2: Using WFIFO Macros**

```cpp
void send_custom_packet(struct map_session_data *sd, int value) {
    int fd = sd->fd;

    WFIFOHEAD(fd, 10);                    // Reserve 10 bytes in send buffer
    WFIFOW(fd, 0) = 0x1234;               // Packet ID (2 bytes)
    WFIFOL(fd, 2) = value;                // Value (4 bytes)
    WFIFOL(fd, 6) = sd->status.char_id;   // Char ID (4 bytes)
    WFIFOSET(fd, 10);                     // Finalize and send
}
```

**WFIFO Macros**:
- `WFIFOHEAD(fd, size)` - Reserve space in send buffer
- `WFIFOB(fd, pos)` - Write 1 byte at position
- `WFIFOW(fd, pos)` - Write 2 bytes (short) at position
- `WFIFOL(fd, pos)` - Write 4 bytes (long) at position
- `WFIFOQ(fd, pos)` - Write 8 bytes (quad) at position
- `WFIFOSET(fd, size)` - Finalize and send packet

---

### **Method 3: Using Helper Functions**

```cpp
// Much easier and safer!
clif_displaymessage(sd->fd, "Hello World!");

// Instead of manually building PACKET_ZC_NOTIFY_CHAT
```

---

### **Send Targets**

```cpp
// Send to specific player
clif->send(&p, len, &sd->bl, SELF);

// Send to all players
clif->send(&p, len, &sd->bl, ALL_CLIENT);

// Send to party
clif->send(&p, len, &sd->bl, PARTY);

// Send to guild
clif->send(&p, len, &sd->bl, GUILD);

// Send to area around player (AREA_SIZE radius)
clif->send(&p, len, &sd->bl, AREA);

// Send to area except self
clif->send(&p, len, &sd->bl, AREA_WOS);

// Send to chat room
clif->send(&p, len, &sd->bl, CHAT);
```

---

## Receiving Packets from Client

### **Parse Function Template**

```cpp
/**
 * Client sends custom data
 * Packet: 0x1234 (CZ_MY_CUSTOM_PACKET)
 */
void clif_parse_MyCustomPacket(int fd, struct map_session_data *sd) {
    // Read packet data using RFIFOP macro
    struct PACKET_CZ_MY_CUSTOM *p = (struct PACKET_CZ_MY_CUSTOM*)RFIFOP(fd, 0);

    // Validate player session
    if (!sd || !sd->bl.prev) {
        return;
    }

    // Extract packet fields
    int value1 = p->value1;
    int value2 = p->value2;
    const char *text = p->text;

    // Validate input
    if (value1 < 0 || value1 > 100) {
        clif_displaymessage(fd, "Invalid value!");
        return;
    }

    // Process packet...
    ShowInfo("Player %s sent: value1=%d, value2=%d, text=%s\n",
             sd->status.name, value1, value2, text);

    // Send response to client
    clif_displaymessage(fd, "Packet received!");
}
```

---

### **RFIF Macros**

```cpp
// Read packet data from receive buffer
RFIFOB(fd, pos)   // Read 1 byte
RFIFOW(fd, pos)   // Read 2 bytes (short)
RFIFOL(fd, pos)   // Read 4 bytes (long)
RFIFOQ(fd, pos)   // Read 8 bytes (quad)
RFIFOP(fd, pos)   // Read pointer to position

// Example:
int fd = sd->fd;
int16 packet_id = RFIFOW(fd, 0);     // Packet ID at offset 0
int32 value = RFIFOL(fd, 2);         // Value at offset 2
char *text = (char*)RFIFOP(fd, 6);   // Pointer to text at offset 6
```

---

## Adding Custom Packets

### **Complete Example: Add Custom Packet**

**Goal**: Add a custom packet that lets the client send a number to the server, and the server responds with double that number.

---

### **Step 1: Define Packet Structures**

**In src/map/packets_struct.hpp** (around line 4000+):

```cpp
/**
 * Custom Packet: Client sends a number
 * Packet ID: 0xF001 (choose unused packet ID > 0xF000 for custom)
 */
struct PACKET_CZ_CUSTOM_SEND_NUMBER {
    int16 packetType;    // 0xF001
    int32 number;        // Number to send
} __attribute__((packed));

/**
 * Custom Packet: Server responds with doubled number
 * Packet ID: 0xF002
 */
struct PACKET_ZC_CUSTOM_DOUBLE_NUMBER {
    int16 packetType;    // 0xF002
    int32 result;        // Doubled number
} __attribute__((packed));
```

---

### **Step 2: Define Packet Headers**

**In src/map/packets.hpp** (around line 3000+):

```cpp
// Custom packet headers
#define HEADER_CZ_CUSTOM_SEND_NUMBER 0xF001
#define HEADER_ZC_CUSTOM_DOUBLE_NUMBER 0xF002
```

---

### **Step 3: Register Packet**

**In src/map/clif_packetdb.hpp** (at the end, before `#endif`):

```cpp
// Register custom packet
// Format: parseable_packet(packet_id, size, parse_function, field_offsets...)
parseable_packet(HEADER_CZ_CUSTOM_SEND_NUMBER,
                 sizeof(struct PACKET_CZ_CUSTOM_SEND_NUMBER),
                 clif_parse_CustomSendNumber, 0);
```

---

### **Step 4: Implement Parse Function**

**In src/map/clif.cpp** (around line 18000+):

```cpp
/**
 * Parse custom packet from client
 * Packet: 0xF001 (HEADER_CZ_CUSTOM_SEND_NUMBER)
 */
void clif_parse_CustomSendNumber(int fd, struct map_session_data *sd) {
    struct PACKET_CZ_CUSTOM_SEND_NUMBER *p =
        (struct PACKET_CZ_CUSTOM_SEND_NUMBER*)RFIFOP(fd, 0);

    // Validate session
    if (!sd || !sd->bl.prev) {
        return;
    }

    int number = p->number;

    ShowInfo("Player %s sent number: %d\n", sd->status.name, number);

    // Calculate double
    int result = number * 2;

    // Send response
    clif_custom_double_number(sd, result);
}

/**
 * Send doubled number to client
 * Packet: 0xF002 (HEADER_ZC_CUSTOM_DOUBLE_NUMBER)
 */
void clif_custom_double_number(struct map_session_data *sd, int result) {
    struct PACKET_ZC_CUSTOM_DOUBLE_NUMBER p;

    p.packetType = HEADER_ZC_CUSTOM_DOUBLE_NUMBER;
    p.result = result;

    clif->send(&p, sizeof(p), &sd->bl, SELF);

    ShowInfo("Sent doubled number to %s: %d\n", sd->status.name, result);
}
```

---

### **Step 5: Add Function Prototype**

**In src/map/clif.hpp** (around line 1000+):

```cpp
// Custom packet functions
void clif_parse_CustomSendNumber(int fd, struct map_session_data *sd);
void clif_custom_double_number(struct map_session_data *sd, int result);
```

---

### **Step 6: Compile and Test**

```bash
cd build
cmake ..
make -j$(nproc)
make install

# Run server
cd ..
./map-server
```

---

### **Step 7: Client-Side Implementation**

**Note**: You need to modify the **client** to send packet 0xF001 and receive 0xF002. This requires:
1. Client-side packet hooking (not covered in this KB)
2. Or using existing packet IDs (modify existing packets)
3. Or using packet interceptor tools

---

## Packet Version (PACKETVER)

### **What is PACKETVER?**

**PACKETVER** defines which **client version** the server supports. Different client dates have different packet structures.

**Example**:
- Client 2018-06-20 → `PACKETVER 20180620`
- Client 2021-11-03 → `PACKETVER 20211103`

---

### **Set PACKETVER**

**Linux (CMake)**:
```bash
cmake .. -DENABLE_PACKETVER=20211103
make -j$(nproc)
```

**Linux (Configure)**:
```bash
./configure --enable-packetver=20211103
make -j$(nproc)
```

**Windows (defines_pre.hpp)**:
```cpp
// In src/custom/defines_pre.hpp
#define PACKETVER 20211103
```

---

### **Version-Specific Packets**

**Example from packets_struct.hpp**:

```cpp
#if PACKETVER < 20080102
    int16 authokType = 0x73;
#elif PACKETVER < 20141022
    int16 authokType = 0x2eb;
#elif PACKETVER < 20160330
    int16 authokType = 0xa18;
#else
    int16 authokType = 0x2eb;
#endif
```

This means the "auth ok" packet changes depending on client version!

---

### **Conditional Compilation**

```cpp
// Use different packet structure based on version
#if PACKETVER >= 20150513
    struct PACKET_ZC_ITEM_ENTRY {
        int16 packetType;
        uint32 ITAID;           // New field in newer clients
        t_itemid nameid;
        // ... more fields
    } __attribute__((packed));
#else
    struct PACKET_ZC_ITEM_ENTRY {
        int16 packetType;
        t_itemid nameid;        // Old format
        // ... fewer fields
    } __attribute__((packed));
#endif
```

---

## Packet Obfuscation

### **What is Packet Obfuscation?**

**Packet obfuscation** encrypts packet IDs to prevent:
- Packet sniffing
- Bot detection
- Packet injection attacks

**Enabled for**: PACKETVER >= 20110817

---

### **Enable Obfuscation**

**In src/config/packets.hpp**:

```cpp
#if PACKETVER >= 20110817
    #define PACKET_OBFUSCATION

    // Set encryption keys (get from your client)
    #define PACKET_OBFUSCATION_KEY1 0x12345678
    #define PACKET_OBFUSCATION_KEY2 0xABCDEF12
    #define PACKET_OBFUSCATION_KEY3 0x98765432
#endif
```

---

### **Find Obfuscation Keys**

1. **Decompile client** (e.g., using IDA Pro)
2. **Search** for encryption functions
3. **Extract** 3 keys used in packet encryption
4. **Add** to `src/custom/defines_pre.hpp`

**Example**:
```cpp
// In src/custom/defines_pre.hpp
#define PACKET_OBFUSCATION_KEY1 0x7E241DE0
#define PACKET_OBFUSCATION_KEY2 0x33B1114C
#define PACKET_OBFUSCATION_KEY3 0x5F830391
```

---

## Security Considerations

### **1. Always Validate Input**

```cpp
// ❌ WRONG - No validation
void clif_parse_MyPacket(int fd, struct map_session_data *sd) {
    struct PACKET_CZ_MY *p = (struct PACKET_CZ_MY*)RFIFOP(fd, 0);
    int item_id = p->item_id;

    // What if item_id is negative? Or doesn't exist?
    struct item_data *item = itemdb_search(item_id);
    // CRASH if invalid!
}

// ✅ CORRECT - Validate input
void clif_parse_MyPacket(int fd, struct map_session_data *sd) {
    struct PACKET_CZ_MY *p = (struct PACKET_CZ_MY*)RFIFOP(fd, 0);
    int item_id = p->item_id;

    // Validate item ID
    if (item_id < 0 || !itemdb_exists(item_id)) {
        clif_displaymessage(fd, "Invalid item!");
        return;
    }

    struct item_data *item = itemdb_search(item_id);
    // Safe to use
}
```

---

### **2. Check Session State**

```cpp
// ✅ ALWAYS check session state
void clif_parse_MyPacket(int fd, struct map_session_data *sd) {
    if (!sd || !sd->bl.prev) {
        return;  // Player not fully loaded or disconnected
    }

    // Safe to proceed
}
```

---

### **3. Prevent Packet Exploits**

```cpp
// ❌ WRONG - No rate limiting
void clif_parse_RequestBuff(int fd, struct map_session_data *sd) {
    // Player can spam this packet thousands of times per second!
    pc_addspiritball(sd, 100000, 10);
}

// ✅ CORRECT - Rate limiting
void clif_parse_RequestBuff(int fd, struct map_session_data *sd) {
    static std::unordered_map<uint32, t_tick> last_use;

    t_tick now = gettick();
    if (now - last_use[sd->status.account_id] < 1000) {
        clif_displaymessage(fd, "Please wait 1 second.");
        return;
    }

    last_use[sd->status.account_id] = now;
    pc_addspiritball(sd, 100000, 10);
}
```

---

### **4. Sanitize String Input**

```cpp
// ✅ ALWAYS sanitize strings
void clif_parse_CustomMessage(int fd, struct map_session_data *sd) {
    struct PACKET_CZ_CUSTOM *p = (struct PACKET_CZ_CUSTOM*)RFIFOP(fd, 0);

    // Ensure null termination
    p->message[sizeof(p->message) - 1] = '\0';

    // Check length
    if (strlen(p->message) > 100) {
        clif_displaymessage(fd, "Message too long!");
        return;
    }

    // Escape special characters for SQL (if storing)
    char escaped[200];
    SQL->EscapeString(map->mysql_handle, escaped, p->message);

    // Now safe to use
}
```

---

## Debugging Packets

### **Method 1: Enable Packet Dumps**

**In src/config/packets.hpp**:

```cpp
#define DUMP_UNKNOWN_PACKET  // Dump unhandled packets
#define DUMP_INVALID_PACKET  // Dump malformed packets
```

**Output**:
```
[Info]: Unknown packet 0x1234 (length 10) from player 'TestPlayer'
[Info]: Packet dump: 34 12 00 00 00 00 64 00 00 00
```

---

### **Method 2: Add Debug Logging**

```cpp
void clif_parse_MyPacket(int fd, struct map_session_data *sd) {
    struct PACKET_CZ_MY *p = (struct PACKET_CZ_MY*)RFIFOP(fd, 0);

    ShowDebug("clif_parse_MyPacket: player=%s, value=%d\n",
              sd->status.name, p->value);

    // ... rest of function ...
}
```

**Enable debug messages** in `src/common/showmsg.cpp` or compile with `-DDEBUG`.

---

### **Method 3: Packet Sniffing Tools**

**Wireshark**:
- Capture network traffic
- Filter by port (default 6900 for map-server)
- Analyze packet contents

**RO Packet Logger**:
- Specialized tools for RO packets
- Can decode packet structures
- Show packet flow

---

## Related References

- **Source Code Structure**: [KB_REF_SourceCodeStructure.md]
- **Script Command Creation**: [KB_REF_ScriptCommandCreation.md]
- **Customization System**: [KB_REF_PluginSystem.md]
- **Best Practices**: [KB_REF_SourceCodeBestPractices.md]

---

**End of KB_REF_027 - Packet Structure and Client-Server Communication**
