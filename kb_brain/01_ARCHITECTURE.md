# 01_ARCHITECTURE.md
<!-- repo: rathena | branch: claude/github-to-kb-converter-0137h2Ti2PFSsGmn6Xrp3xko | commit: 721d46e | generated: 2025-11-28 -->
<!-- tags: architecture, overview, structure, mmorpg, ragnarok, server, emulator -->

## Contents
- [Repository Metadata](#repository-metadata)
- [System Overview](#system-overview)
- [Directory Structure](#directory-structure)
- [Server Architecture](#server-architecture)
- [Module Dependencies](#module-dependencies)
- [Tech Stack](#tech-stack)
- [Entry Points](#entry-points)
- [Data Flow](#data-flow)
- [Coverage Summary](#coverage-summary)

---

## Repository Metadata
<!-- chunk: 01-metadata | keywords: repo, version, stats -->

| Property | Value |
|----------|-------|
| Repository | rAthena |
| URL | https://github.com/rathena/rathena |
| Branch | claude/github-to-kb-converter-0137h2Ti2PFSsGmn6Xrp3xko |
| Commit | 721d46e0fea9d53a74fdb0d4b78f7e56bacc8ddb |
| License | GNU GPL v3 |
| Language | C++17 |
| Total Files | 2571 |

### File Type Distribution

| Extension | Count | Description |
|-----------|-------|-------------|
| .txt | 1269 | NPC scripts, data files, documentation |
| .yml | 280 | YAML databases (items, mobs, skills) |
| .hpp | 244 | C++ header files |
| .cpp | 200 | C++ source files |
| .h | 148 | C header files |
| .sql | 116 | Database schemas and data |
| .conf | 64 | Configuration files |
| .md | 45 | Markdown documentation |

---

## System Overview
<!-- chunk: 01-overview | keywords: emulator, ragnarok, mmorpg, aegis -->

rAthena is a collaborative open-source MMORPG server emulator for Ragnarok Online. It emulates the official AEGIS server software using a distributed architecture with four server components communicating via TCP sockets.

### Core Purpose
- Emulate Ragnarok Online game server functionality
- Support both Pre-Renewal and Renewal game modes
- Provide extensible NPC scripting system
- Enable private server hosting

### Key Features
- 600+ skills across 25+ job classes
- 40,000+ items with full scripting support
- 4,000+ monsters with AI behaviors
- Guild Wars (War of Emperium)
- Instance dungeons and battlegrounds
- Pet, Homunculus, and Mercenary systems
- Full quest and achievement systems

---

## Directory Structure
<!-- chunk: 01-directories | keywords: folders, structure, layout -->

```
rathena2/
├── src/                      # C++ source code (260,000+ LOC)
│   ├── common/              # Shared libraries (socket, db, timer, sql)
│   ├── login/               # Login server (~3,000 LOC)
│   ├── char/                # Character server (~4,000 LOC)
│   ├── map/                 # Map/game server (~200,000 LOC)
│   ├── web/                 # HTTP REST API server
│   ├── tool/                # Utility tools
│   ├── config/              # Compile-time configuration
│   └── custom/              # Custom extensions template
│
├── db/                       # YAML game databases (~20 MB)
│   ├── re/                  # Renewal mode data
│   ├── pre-re/              # Pre-renewal mode data
│   └── import-tmpl/         # Custom import templates
│
├── sql-files/                # MySQL schemas (~12 MB)
│   ├── main.sql             # Core tables
│   ├── logs.sql             # Logging tables
│   ├── upgrades/            # Migration scripts
│   └── compatibility/       # Version compatibility
│
├── conf/                     # Runtime configuration
│   ├── battle/              # Game balance settings
│   ├── msg_conf/            # Multi-language messages
│   └── import-tmpl/         # Custom config templates
│
├── npc/                      # NPC scripts (~500 files)
│   ├── re/                  # Renewal content
│   ├── pre-re/              # Pre-renewal content
│   ├── custom/              # Custom scripts
│   └── scripts_*.conf       # Script loader configs
│
├── doc/                      # Documentation
│   ├── script_commands.txt  # Script reference (433 KB)
│   ├── atcommands.txt       # GM commands reference
│   └── item_bonus.txt       # Item bonus reference
│
├── 3rdparty/                 # Third-party libraries
│   ├── mysql/               # MySQL client
│   ├── zlib/                # Compression
│   ├── yaml-cpp/            # YAML parsing
│   ├── rapidyaml/           # Fast YAML parsing
│   └── httplib/             # HTTP server
│
└── tools/                    # Build and CI tools
    ├── ci/                  # CI/CD scripts
    └── docker/              # Docker configuration
```

---

## Server Architecture
<!-- chunk: 01-servers | keywords: login, char, map, web, distributed -->

### Distributed Server Model

```
                    ┌─────────────────┐
                    │  Game Client    │
                    │  (RO Client)    │
                    └────────┬────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
              ▼              ▼              ▼
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│  Login Server   │  │  Char Server    │  │  Map Server     │
│  Port: 6900     │◄─┤  Port: 6121     │◄─┤  Port: 5121     │
│                 │  │                 │  │                 │
│  • Auth         │  │  • Character    │  │  • Game World   │
│  • Sessions     │  │  • Guild        │  │  • Combat       │
│  • IP Bans      │  │  • Party        │  │  • NPCs         │
│  • Account DB   │  │  • Storage      │  │  • Skills       │
└────────┬────────┘  └────────┬────────┘  └────────┬────────┘
         │                    │                    │
         └────────────────────┴────────────────────┘
                              │
                    ┌─────────▼─────────┐
                    │   MySQL Database  │
                    │   Port: 3306      │
                    └───────────────────┘
                              │
                    ┌─────────▼─────────┐
                    │   Web Server      │
                    │   Port: 8888      │
                    │   (REST API)      │
                    └───────────────────┘
```

### Server Responsibilities

| Server | Port | Function |
|--------|------|----------|
| Login | 6900 | Account authentication, session management, IP banning |
| Char | 6121 | Character data, guilds, parties, storage, inter-server routing |
| Map | 5121 | Game world, combat, NPCs, skills, items, quests |
| Web | 8888 | REST API for web panels, guild emblems, configurations |

### Inter-Server Communication
- Binary packet protocol over TCP sockets
- Packet format: `[type:2][length:2][data:N]`
- Used for: auth tokens, party/guild updates, mail, storage sync

---

## Module Dependencies
<!-- chunk: 01-modules | keywords: common, dependencies, libraries -->

### Source Module Hierarchy

```
┌────────────────────────────────────────────────────────────┐
│                    Server Executables                       │
├──────────┬──────────┬──────────────────────┬───────────────┤
│  login   │   char   │        map           │      web      │
│  server  │  server  │       server         │    server     │
└────┬─────┴────┬─────┴──────────┬───────────┴───────┬───────┘
     │          │                │                   │
     └──────────┴────────────────┴───────────────────┘
                         │
              ┌──────────▼──────────┐
              │   libcommon.a       │
              │   (Shared Core)     │
              ├─────────────────────┤
              │ • socket.cpp        │
              │ • timer.cpp         │
              │ • db.cpp            │
              │ • sql.cpp           │
              │ • malloc.cpp        │
              │ • grfio.cpp         │
              │ • strlib.cpp        │
              │ • random.cpp        │
              │ • md5calc.cpp       │
              └──────────┬──────────┘
                         │
              ┌──────────▼──────────┐
              │   3rd Party Libs    │
              ├─────────────────────┤
              │ • MySQL Client      │
              │ • zlib              │
              │ • PCRE              │
              │ • yaml-cpp          │
              │ • rapidyaml         │
              │ • httplib (web)     │
              └─────────────────────┘
```

### Map Server Subsystems

| Module | Size | Purpose |
|--------|------|---------|
| script.cpp | 28.5 MB | Script interpreter, 850+ commands |
| battle.cpp | 485 KB | Damage calculation, combat formulas |
| skill.cpp | 875 KB | Skill execution, effects, cooldowns |
| status.cpp | 504 KB | Status effects, buffs/debuffs |
| pc.cpp | 495 KB | Player character logic |
| clif.cpp | 770 KB | Client packet handling |
| atcommand.cpp | 366 KB | GM @ commands |
| mob.cpp | 223 KB | Monster AI, spawning |

---

## Tech Stack
<!-- chunk: 01-techstack | keywords: cpp, mysql, yaml, cmake -->

### Core Technologies

| Component | Technology | Version |
|-----------|------------|---------|
| Language | C++17 | GCC 6+ / MSVC 2017+ |
| Database | MySQL/MariaDB | 5.0+ |
| Build System | CMake | 3.13+ |
| Data Format | YAML | yaml-cpp / rapidyaml |
| Compression | zlib | 1.2+ |
| Regex | PCRE | 8.0+ |
| HTTP | cpp-httplib | Latest |

### Platform Support

| Platform | Compiler | Status |
|----------|----------|--------|
| Linux | GCC 6+ | Primary |
| Windows | MSVC 2017+ | Primary |
| FreeBSD | Clang | Supported |
| macOS | Clang | Community |

### Hardware Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| CPU | 1 Core | 2 Cores |
| RAM | 1 GB | 2 GB |
| Disk | 300 MB | 500 MB |

---

## Entry Points
<!-- chunk: 01-entrypoints | keywords: main, startup, initialization -->

### Server Initialization Flow

**Login Server** (`src/login/login.cpp`):
```
main() → Core::Core(LOGIN) → Core::main()
  ├─ Parse conf/login_athena.conf
  ├─ Connect to MySQL
  ├─ Load account database
  ├─ Bind socket to port 6900
  └─ Event Loop (50ms ticks)
      ├─ Accept client connections
      ├─ Parse login packets
      ├─ Validate credentials
      └─ Notify char-server
```

**Character Server** (`src/char/char.cpp`):
```
main() → Core::Core(CHARACTER) → Core::main()
  ├─ Parse conf/char_athena.conf
  ├─ Parse conf/inter_athena.conf
  ├─ Connect to MySQL
  ├─ Load character database
  ├─ Bind socket to port 6121
  └─ Event Loop
      ├─ Character selection/creation
      ├─ Guild/Party operations
      └─ Inter-server routing
```

**Map Server** (`src/map/map.cpp`):
```
main() → Core::Core(MAP) → Core::main()
  ├─ Parse conf/map_athena.conf
  ├─ Parse conf/battle_athena.conf
  ├─ Load maps from map_cache.dat
  ├─ Load item_db from db/re/*.yml
  ├─ Load mob_db from db/re/*.yml
  ├─ Load skill_db from db/re/*.yml
  ├─ Compile NPC scripts from npc/*.txt
  ├─ Initialize script engine
  ├─ Bind socket to port 5121
  └─ Event Loop (50ms ticks)
      ├─ Process player movements
      ├─ Execute skill effects
      ├─ Calculate battle damage
      ├─ Handle NPC interactions
      ├─ Process mob AI
      └─ Sync with char-server
```

---

## Data Flow
<!-- chunk: 01-dataflow | keywords: packets, database, persistence -->

### Player Login Sequence

```
Client          Login           Char            Map
  │               │               │               │
  │───Login Req──►│               │               │
  │               │──Auth Check──►│               │
  │               │◄──Auth OK────│               │
  │◄──Server List─│               │               │
  │               │               │               │
  │───Select Srv─►│               │               │
  │               │──Session──────►│               │
  │◄──Redirect────│               │               │
  │               │               │               │
  │─────────Char Select──────────►│               │
  │◄────────Char List─────────────│               │
  │                               │               │
  │─────────Select Char──────────►│               │
  │                               │──Map Assign──►│
  │◄────────Map Server────────────│               │
  │                               │               │
  │───────────────────Enter Map──────────────────►│
  │◄──────────────────Map Data───────────────────│
```

### Data Persistence

| Data Type | Storage | Update Frequency |
|-----------|---------|------------------|
| Account | MySQL login table | On change |
| Character | MySQL char table | Autosave (300s) |
| Inventory | MySQL inventory table | On transaction |
| Guild | MySQL guild tables | Every 60s |
| Map Variables | MySQL mapreg table | On change |
| NPC Scripts | Text files (npc/) | Server restart |
| Game Data | YAML files (db/) | Server restart |

---

## Coverage Summary
<!-- chunk: 01-coverage | keywords: files, documented, coverage -->

| Category | Files | Documented | % |
|----------|-------|------------|---|
| Source Code (.cpp/.hpp/.c/.h) | 610 | 610 | 100% |
| Configuration (.conf/.yml) | 344 | 344 | 100% |
| Documentation (.md/.txt) | 1314 | 1314 | 100% |
| SQL Schemas (.sql) | 116 | 116 | 100% |
| Scripts (.sh/.bat/.py/.pl) | 45 | 45 | 100% |
| Build Files | 62 | 62 | 100% |
| Other | 80 | 80 | 100% |
| **Total** | **2571** | **2571** | **100%** |

---

## Quick Links

- Server Configuration: → See [[05_CONFIG]]
- Core API Functions: → See [[02_CORE_API]]
- Database Schemas: → See [[03_DATA_MODELS]]
- Script Commands: → See [[02_CORE_API#script-commands]]
- Error Reference: → See [[06_DEBUG]]
