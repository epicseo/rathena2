# rAthena Compilation & Debugging Reference

## Table of Contents
1. [Build Systems](#build-systems)
2. [Dependencies](#dependencies)
3. [Build Options & Configuration](#build-options--configuration)
4. [Compilation Commands](#compilation-commands)
5. [GDB Debugging](#gdb-debugging)
6. [Visual Studio Debugging](#visual-studio-debugging)
7. [Memory Leak Detection](#memory-leak-detection)
8. [Profiling & Performance Analysis](#profiling--performance-analysis)
9. [Common Errors & Fixes](#common-errors--fixes)
10. [Continuous Integration Setup](#continuous-integration-setup)
11. [Optimization Flags](#optimization-flags)
12. [Real Debugging Scenarios](#real-debugging-scenarios)

---

## Build Systems

### CMake (Recommended - Cross-Platform)

**Directory Structure:**
```
rathena/
├── CMakeLists.txt           # Root CMake configuration
├── 3rdparty/
│   └── CMakeLists.txt       # Third-party dependencies
├── src/
│   ├── CMakeLists.txt       # Main source configuration
│   ├── common/CMakeLists.txt
│   ├── map/CMakeLists.txt
│   ├── char/CMakeLists.txt
│   └── login/CMakeLists.txt
└── build/                   # Build output directory
```

**Basic CMake Build Process:**
```bash
# Create build directory
mkdir build && cd build

# Configure (generate build files)
cmake ..

# Build
cmake --build . --parallel 4

# Install (optional)
cmake --install .
```

**Advanced CMake Configuration:**
```bash
# Debug build with all debug symbols
cmake -DCMAKE_BUILD_TYPE=Debug ..

# Release build with optimizations
cmake -DCMAKE_BUILD_TYPE=Release ..

# RelWithDebInfo (optimized with debug symbols)
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo ..

# MinSizeRel (optimized for size)
cmake -DCMAKE_BUILD_TYPE=MinSizeRel ..

# Custom install prefix
cmake -DCMAKE_INSTALL_PREFIX=/opt/rathena ..

# Enable Renewal mode
cmake -DRENEWAL=ON ..

# Set packet version
cmake -DPACKETVER=20211103 ..

# Set maximum level
cmake -DMAX_LEVEL=175 ..

# Enable PCRE support
cmake -DWITH_PCRE=ON ..

# Custom MySQL location
cmake -DMYSQL_INCLUDE_DIR=/usr/include/mysql \
      -DMYSQL_LIBRARY=/usr/lib/x86_64-linux-gnu/libmysqlclient.so ..

# Ninja generator (faster builds)
cmake -G Ninja ..
```

**CMake Cache Variables:**
```bash
# View all cache variables
cmake -LAH

# Clear cache
rm CMakeCache.txt

# Reconfigure from scratch
rm -rf CMakeFiles CMakeCache.txt
cmake ..
```

**Key CMakeLists.txt Sections:**
```cmake
# Minimum version
cmake_minimum_required(VERSION 3.10)

# Project definition
project(rAthena LANGUAGES C CXX)

# C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Build options
option(RENEWAL "Enable Renewal mode" ON)
option(WITH_PCRE "Enable PCRE support" ON)
option(BUILD_SERVERS "Build server executables" ON)
option(BUILD_TOOLS "Build tool executables" ON)

# Add subdirectories
add_subdirectory(3rdparty)
add_subdirectory(src/common)
add_subdirectory(src/map)
add_subdirectory(src/char)
add_subdirectory(src/login)

# Executable target
add_executable(map-server ${MAP_SOURCES})
target_link_libraries(map-server common ${MYSQL_LIBRARY} ${PCRE_LIBRARY})
```

### Configure Script (Legacy - Linux/Unix)

**Basic Usage:**
```bash
# Generate configure script (if from Git)
./autogen.sh

# Configure
./configure

# Build
make clean
make -j4

# Install
make install
```

**Configure Options:**
```bash
# Enable debug mode
./configure --enable-debug

# Enable Renewal
./configure --enable-renewal

# Custom packet version
./configure --enable-packetver=20211103

# Custom max level
./configure --enable-maxlevel=175

# Disable PCRE
./configure --without-pcre

# Custom MySQL path
./configure --with-mysql=/usr/local/mysql

# Install prefix
./configure --prefix=/opt/rathena

# All options
./configure --help
```

**Key Files:**
- `configure.ac` - Autoconf configuration
- `Makefile.in` - Makefile template
- `config.log` - Configuration log (check for errors)
- `config.status` - Configuration state

### Visual Studio (Windows)

**Project Structure:**
```
rathena.sln                  # Solution file
├── char-server.vcxproj      # Character server project
├── login-server.vcxproj     # Login server project
├── map-server.vcxproj       # Map server project
├── common.vcxproj           # Common library
└── 3rdparty/                # Dependencies
    ├── mysql/
    ├── pcre/
    └── zlib/
```

**Build Configurations:**
- **Debug**: No optimizations, full debug info, runtime checks
- **Release**: Full optimizations, no debug info
- **RelWithDebInfo**: Optimizations + debug symbols
- **MinSizeRel**: Optimize for size

**Project Properties:**
```
Configuration Properties
├── General
│   ├── Output Directory: $(SolutionDir)bin\$(Configuration)\
│   ├── Intermediate Directory: $(SolutionDir)obj\$(Configuration)\$(ProjectName)\
│   └── Configuration Type: Application (.exe)
├── C/C++
│   ├── General
│   │   └── Additional Include Directories
│   ├── Preprocessor
│   │   └── Preprocessor Definitions (PACKETVER, RENEWAL, etc.)
│   ├── Code Generation
│   │   └── Runtime Library: /MD or /MDd
│   └── Optimization
│       └── Optimization: /O2 (Release), /Od (Debug)
└── Linker
    ├── General
    │   └── Additional Library Directories
    └── Input
        └── Additional Dependencies (libmysql.lib, pcre.lib, etc.)
```

**Batch Building:**
```batch
REM Build all configurations
MSBuild rathena.sln /p:Configuration=Debug /m
MSBuild rathena.sln /p:Configuration=Release /m

REM Build specific project
MSBuild map-server.vcxproj /p:Configuration=Debug

REM Clean and rebuild
MSBuild rathena.sln /t:Clean,Build /p:Configuration=Release /m
```

---

## Dependencies

### MySQL/MariaDB

**Installation:**
```bash
# Ubuntu/Debian
sudo apt-get install libmariadb-dev libmariadb-dev-compat

# CentOS/RHEL
sudo yum install mysql-devel

# macOS
brew install mysql

# Windows
# Download MySQL Connector/C from mysql.com
# Extract to 3rdparty/mysql/
```

**Version Requirements:**
- MySQL 5.7+ or MariaDB 10.2+
- Connector/C or client library

**CMake Detection:**
```cmake
find_package(MySQL REQUIRED)
if(MYSQL_FOUND)
    include_directories(${MYSQL_INCLUDE_DIR})
    target_link_libraries(map-server ${MYSQL_LIBRARY})
endif()
```

**Common Issues:**
```bash
# MySQL not found
CMake Error: Could not find MySQL

# Fix: Set MySQL path manually
cmake -DMYSQL_INCLUDE_DIR=/usr/include/mysql \
      -DMYSQL_LIBRARY=/usr/lib/libmysqlclient.so ..

# Wrong MySQL library
# Fix: Ensure libmysqlclient, not libmysqld (embedded)
```

### PCRE (Perl Compatible Regular Expressions)

**Installation:**
```bash
# Ubuntu/Debian
sudo apt-get install libpcre3-dev

# CentOS/RHEL
sudo yum install pcre-devel

# macOS
brew install pcre

# Windows
# Download from https://www.pcre.org/
# Place in 3rdparty/pcre/
```

**Usage in Code:**
```cpp
// Script engine uses PCRE for pattern matching
#ifdef PCRE_SUPPORT
    pcre *re = pcre_compile(pattern, 0, &error, &erroffset, NULL);
    if (re && pcre_exec(re, NULL, str, strlen(str), 0, 0, ovector, 30) > 0) {
        // Match found
    }
#endif
```

**Build Without PCRE:**
```bash
cmake -DWITH_PCRE=OFF ..
# or
./configure --without-pcre
```

### zlib (Compression)

**Installation:**
```bash
# Ubuntu/Debian
sudo apt-get install zlib1g-dev

# CentOS/RHEL
sudo yum install zlib-devel

# macOS (usually pre-installed)
brew install zlib

# Windows
# Included in 3rdparty/zlib/
```

**Usage:**
- Packet compression
- Database compression
- Log file compression

### OpenSSL (Optional - For Encryption)

**Installation:**
```bash
# Ubuntu/Debian
sudo apt-get install libssl-dev

# CentOS/RHEL
sudo yum install openssl-devel

# macOS
brew install openssl
```

**Enable in Build:**
```bash
cmake -DWITH_OPENSSL=ON \
      -DOPENSSL_ROOT_DIR=/usr/local/opt/openssl ..
```

**Usage:**
- Login server password encryption
- Secure inter-server communication
- Web server integration

### Complete Dependency Install Scripts

**Ubuntu/Debian:**
```bash
#!/bin/bash
sudo apt-get update
sudo apt-get install -y \
    git \
    make \
    cmake \
    gcc \
    g++ \
    libmariadb-dev \
    libmariadb-dev-compat \
    libpcre3-dev \
    zlib1g-dev \
    libssl-dev
```

**CentOS/RHEL:**
```bash
#!/bin/bash
sudo yum install -y \
    git \
    make \
    cmake \
    gcc \
    gcc-c++ \
    mysql-devel \
    pcre-devel \
    zlib-devel \
    openssl-devel
```

---

## Build Options & Configuration

### PACKETVER (Client Version)

**What It Controls:**
- Client packet structures
- Available features per client version
- Packet encryption keys
- UI elements and display

**Setting PACKETVER:**
```cpp
// src/config/core.hpp
#define PACKETVER 20211103  // YYYYMMDD format

// CMake
cmake -DPACKETVER=20211103 ..

// Configure
./configure --enable-packetver=20211103
```

**Common Versions:**
```cpp
20211103  // 2021-11-03 (latest renewal)
20180620  // 2018-06-20 (popular stable)
20151104  // 2015-11-04 (pre-renewal compatible)
20120410  // 2012-04-10 (older stable)
```

**Version-Specific Code:**
```cpp
#if PACKETVER >= 20211103
    // New packet structure
    struct PACKET_ZC_NEW_ITEM {
        int16 packetType;
        uint32 itemId;
        // New fields...
    };
#else
    // Old packet structure
    struct PACKET_ZC_NEW_ITEM {
        int16 packetType;
        uint16 itemId;
        // Old fields...
    };
#endif
```

### RENEWAL Mode

**What It Changes:**
- Damage formulas
- Status point distribution
- Aspd calculations
- Monster stats and behavior
- Skill mechanics
- Experience tables

**Enabling RENEWAL:**
```cpp
// src/config/renewal.hpp
#define RENEWAL           // Enable all renewal features
#define RENEWAL_CAST      // Renewal cast system
#define RENEWAL_DROP      // Renewal drop rates
#define RENEWAL_EXP       // Renewal experience tables
#define RENEWAL_LVDMG     // Renewal level damage modifiers
#define RENEWAL_ASPD      // Renewal ASPD formula

// CMake
cmake -DRENEWAL=ON ..

// Configure
./configure --enable-renewal
```

**Conditional Compilation:**
```cpp
int battle_calc_damage(struct block_list *src, struct block_list *target) {
#ifdef RENEWAL
    // Renewal damage formula
    damage = (status_get_batk(src) + status_get_watk(src)) * skill_ratio / 100;
#else
    // Pre-renewal damage formula
    damage = status_get_batk(src) * skill_ratio / 100;
#endif
    return damage;
}
```

### MAX_LEVEL

**Configuration:**
```cpp
// src/config/core.hpp
#define MAX_LEVEL 99          // Base level cap
#define MAX_LEVEL_THIRD 175   // Third class level cap (Renewal)

// CMake
cmake -DMAX_LEVEL=175 ..

// Configure
./configure --enable-maxlevel=175
```

**Impact:**
```cpp
// Experience tables must match
// db/[pre-]re/exp_base.yml
// db/[pre-]re/exp_job.yml

// Status arrays sized accordingly
int status_point_table[MAX_LEVEL];
uint64 exp_table[MAX_LEVEL];
```

### Other Important Defines

**src/config/core.hpp:**
```cpp
// Inventory sizes
#define MAX_INVENTORY 100
#define MAX_STORAGE 600
#define MAX_CART 100

// Party/Guild
#define MAX_PARTY 12
#define MAX_GUILD 16+10*6  // 16 + 6 extension levels

// Skill limits
#define MAX_SKILL 5000
#define MAX_SKILL_LEVEL 20

// Chat/message
#define CHAT_SIZE_MAX 255
#define GLOBAL_REG_NUM 256

// Network
#define FIFOSIZE_SERVERLINK 512*1024
#define MAX_MAP_PER_SERVER 1500

// Security
#define MAX_ITEM_ID 65535
#define SECURE_NPCTIMEOUT
#define AUTOTRADE_PERSISTENCY

// Features
#define CELL_NOSTACK_LIMIT 1
#define OFFICIAL_WALKPATH
#define NEW_CARTS
#define SCRIPT_CALLFUNC_CHECK
```

**Feature Flags:**
```cpp
// Enable VIP system
#define VIP_ENABLE

// Enable bound item system
#define BOUND_ITEMS

// Enable banking system
#define BANK_VAULT

// Enable attendance system
#define ATTENDANCE_SYSTEM

// Enable item options (random options)
#define ITEM_OPTIONS

// Enable achievement system
#define ACHIEVEMENT_SYSTEM
```

---

## Compilation Commands

### Linux/Unix Full Build

**First-Time Build:**
```bash
#!/bin/bash
# Clone repository
git clone https://github.com/rathena/rathena.git
cd rathena

# Install dependencies (Ubuntu/Debian)
sudo apt-get update
sudo apt-get install -y git make cmake gcc g++ \
    libmariadb-dev libmariadb-dev-compat libpcre3-dev zlib1g-dev

# Create build directory
mkdir build && cd build

# Configure with CMake
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo \
      -DRENEWAL=ON \
      -DPACKETVER=20211103 \
      -DMAX_LEVEL=175 \
      ..

# Build (using all CPU cores)
cmake --build . --parallel $(nproc)

# Verify binaries
ls -lh map-server* char-server* login-server*
```

**Incremental Build:**
```bash
cd build

# Rebuild only changed files
cmake --build . --parallel $(nproc)

# Rebuild specific target
cmake --build . --target map-server

# Clean and rebuild
cmake --build . --target clean
cmake --build . --parallel $(nproc)
```

**Debug Build:**
```bash
# Configure for debugging
cmake -DCMAKE_BUILD_TYPE=Debug \
      -DCMAKE_C_FLAGS="-g3 -O0 -DDEBUG" \
      -DCMAKE_CXX_FLAGS="-g3 -O0 -DDEBUG" \
      ..

# Build with verbose output
cmake --build . --verbose

# Or with make
make VERBOSE=1 -j$(nproc)
```

### Windows Visual Studio Build

**Command Line (Developer Command Prompt):**
```batch
REM Open "Developer Command Prompt for VS 2019/2022"

REM Navigate to rAthena directory
cd C:\rathena

REM Build Debug configuration
MSBuild rathena.sln /p:Configuration=Debug /p:Platform=x64 /m

REM Build Release configuration
MSBuild rathena.sln /p:Configuration=Release /p:Platform=x64 /m

REM Build specific project
MSBuild map-server.vcxproj /p:Configuration=Debug /p:Platform=x64

REM Clean
MSBuild rathena.sln /t:Clean /p:Configuration=Debug /p:Platform=x64

REM Rebuild all
MSBuild rathena.sln /t:Rebuild /p:Configuration=Release /p:Platform=x64 /m
```

**IDE Build:**
1. Open `rathena.sln` in Visual Studio
2. Select configuration (Debug/Release) from toolbar
3. Select platform (x64/x86)
4. Build → Build Solution (Ctrl+Shift+B)
5. Build → Rebuild Solution (full rebuild)
6. Build → Build [specific project]

**Batch Script (build.bat):**
```batch
@echo off
setlocal

set VS_PATH="C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Current\Bin"
set SOLUTION=rathena.sln

echo Building Debug configuration...
%VS_PATH%\MSBuild.exe %SOLUTION% /p:Configuration=Debug /p:Platform=x64 /m /v:minimal
if errorlevel 1 (
    echo Debug build failed!
    exit /b 1
)

echo Building Release configuration...
%VS_PATH%\MSBuild.exe %SOLUTION% /p:Configuration=Release /p:Platform=x64 /m /v:minimal
if errorlevel 1 (
    echo Release build failed!
    exit /b 1
)

echo Build completed successfully!
```

### Build Verification

**Check Binary:**
```bash
# Verify executable
file map-server
# Output: map-server: ELF 64-bit LSB executable, x86-64, dynamically linked

# Check dependencies
ldd map-server
# Output shows linked libraries (mysql, pcre, etc.)

# Run with version flag
./map-server --version

# Check symbols (debug build)
nm map-server | grep -i "script_run"
```

**Test Run:**
```bash
# Quick syntax check
./map-server --help

# Test configuration loading
./map-server --load-plugin test
```

---

## GDB Debugging

### Setup & Basics

**Installing GDB:**
```bash
# Ubuntu/Debian
sudo apt-get install gdb

# CentOS/RHEL
sudo yum install gdb

# macOS (use LLDB instead)
# GDB available via brew but LLDB recommended
```

**Compile with Debug Symbols:**
```bash
cmake -DCMAKE_BUILD_TYPE=Debug \
      -DCMAKE_C_FLAGS="-g3 -O0" \
      -DCMAKE_CXX_FLAGS="-g3 -O0" \
      ..
cmake --build .
```

**Starting GDB:**
```bash
# Direct launch
gdb ./map-server

# Attach to running process
gdb -p $(pidof map-server)

# With arguments
gdb --args ./map-server --run-once

# With core dump
gdb ./map-server core.12345
```

### Essential GDB Commands

**Breakpoints:**
```gdb
# Set breakpoint at function
(gdb) break script_run
(gdb) b script_run

# Set breakpoint at file:line
(gdb) break script.cpp:1234
(gdb) b script.cpp:1234

# Conditional breakpoint
(gdb) break script_run if sd->status.account_id == 150000

# Breakpoint at address
(gdb) break *0x555555555234

# List breakpoints
(gdb) info breakpoints
(gdb) info b

# Enable/disable breakpoint
(gdb) disable 1
(gdb) enable 1

# Delete breakpoint
(gdb) delete 1
(gdb) clear script_run
```

**Execution Control:**
```gdb
# Run program
(gdb) run
(gdb) r

# Continue execution
(gdb) continue
(gdb) c

# Step (into functions)
(gdb) step
(gdb) s

# Next (over functions)
(gdb) next
(gdb) n

# Step instruction (assembly)
(gdb) stepi
(gdb) si

# Next instruction
(gdb) nexti
(gdb) ni

# Finish current function
(gdb) finish

# Until (run until line)
(gdb) until 1500
```

**Examining Variables:**
```gdb
# Print variable
(gdb) print sd
(gdb) p sd

# Print with type info
(gdb) ptype sd
# Output: type = struct map_session_data * {
#   ...
# }

# Print structure members
(gdb) p sd->status.name
(gdb) p sd->status.base_level

# Print array
(gdb) p sd->status.inventory[0]@10  # First 10 items

# Print in different formats
(gdb) p/x sd->status.account_id     # Hexadecimal
(gdb) p/d sd->status.account_id     # Decimal
(gdb) p/t sd->status.account_id     # Binary
(gdb) p/c variable                   # Character

# Print pointer dereferencing
(gdb) p *sd
(gdb) p sd->status

# Pretty printing
(gdb) set print pretty on
(gdb) p sd->status
```

**Watchpoints (Data Breakpoints):**
```gdb
# Watch for write
(gdb) watch sd->status.hp
# Hardware watchpoint 1: sd->status.hp

# Watch for read
(gdb) rwatch sd->status.hp

# Watch for read/write
(gdb) awatch sd->status.hp

# Conditional watchpoint
(gdb) watch sd->status.hp if sd->status.hp < 100
```

**Backtrace:**
```gdb
# Show call stack
(gdb) backtrace
(gdb) bt

# Full backtrace with locals
(gdb) bt full

# Show N frames
(gdb) bt 10

# Select frame
(gdb) frame 3
(gdb) f 3

# Move up/down frames
(gdb) up
(gdb) down

# Frame info
(gdb) info frame
(gdb) info locals
(gdb) info args
```

**Thread Debugging:**
```gdb
# List threads
(gdb) info threads

# Switch to thread
(gdb) thread 2

# Apply command to all threads
(gdb) thread apply all bt

# Break on thread
(gdb) break script.cpp:100 thread 3
```

**Memory Examination:**
```gdb
# Examine memory
(gdb) x/10x $sp           # 10 hex words at stack pointer
(gdb) x/10i $pc           # 10 instructions at program counter
(gdb) x/s 0x555556789     # String at address
(gdb) x/10wx sd           # 10 words in hex from sd

# Format: x/[count][format][size] address
# format: x(hex) d(decimal) u(unsigned) o(octal) t(binary)
#         a(address) c(char) s(string) i(instruction)
# size: b(byte) h(halfword) w(word) g(giant-8bytes)
```

### Advanced GDB Techniques

**GDB Script (.gdbinit):**
```gdb
# ~/.gdbinit or project .gdbinit
set print pretty on
set print array on
set print array-indexes on
set pagination off
set confirm off

# Custom commands
define print_player
    if $argc != 1
        help print_player
    else
        set $sd = (struct map_session_data *)$arg0
        printf "Player: %s\n", $sd->status.name
        printf "Level: %d/%d\n", $sd->status.base_level, $sd->status.job_level
        printf "HP: %d/%d\n", $sd->status.hp, $sd->status.max_hp
        printf "SP: %d/%d\n", $sd->status.sp, $sd->status.max_sp
    end
end

# Auto breakpoints
break main
break script_run
```

**Logging:**
```gdb
# Enable logging
(gdb) set logging on
(gdb) set logging file gdb.log
(gdb) set logging overwrite on

# Run commands
(gdb) bt full
(gdb) info registers

# Disable logging
(gdb) set logging off
```

**Reverse Debugging:**
```gdb
# Enable recording
(gdb) target record-full

# Reverse execution
(gdb) reverse-continue
(gdb) reverse-step
(gdb) reverse-next
(gdb) reverse-finish
```

**Core Dump Analysis:**
```bash
# Enable core dumps
ulimit -c unlimited

# Generate core dump from running process
gcore $(pidof map-server)

# Analyze core dump
gdb ./map-server core.12345

# Automatic backtrace
(gdb) bt full
(gdb) thread apply all bt full
```

---

## Visual Studio Debugging

### Basic Debugging Operations

**Starting Debug Session:**
- **F5** - Start Debugging
- **Ctrl+F5** - Start Without Debugging
- **F10** - Step Over (next line, don't enter functions)
- **F11** - Step Into (enter functions)
- **Shift+F11** - Step Out (exit current function)
- **Ctrl+Shift+F5** - Restart
- **Shift+F5** - Stop Debugging
- **Ctrl+Alt+Break** - Break All

**Breakpoints:**
- **F9** - Toggle breakpoint on current line
- **Ctrl+F9** - Enable/disable breakpoint
- **Ctrl+Shift+F9** - Delete all breakpoints

**Managing Breakpoints:**
```
Debug → Windows → Breakpoints (Ctrl+Alt+B)
```

**Breakpoint Actions:**
1. **Condition**: Break only when expression is true
   ```cpp
   sd->status.account_id == 150000
   ```

2. **Hit Count**: Break after N hits
   - Break always
   - Break when hit count equals N
   - Break when hit count is multiple of N
   - Break when hit count >= N

3. **Actions (Tracepoint)**: Print message without breaking
   ```
   Account ID: {sd->status.account_id}, Name: {sd->status.name}
   ```

4. **Filter**: Break only for specific process/thread

**Example Breakpoint Setup:**
```
Location: script.cpp, line 1523
Condition: strcmp(script->str_data[script->str_num].name, "OnPCDieEvent") == 0
Action: Script event triggered: {script->str_data[script->str_num].name}
```

### Watch Window & Data Inspection

**Watch Windows:**
- **Locals** (Alt+4): Variables in current scope
- **Autos** (Ctrl+Alt+V, A): Variables in current and previous statement
- **Watch 1-4** (Ctrl+Alt+W, 1-4): Custom watch expressions
- **Quick Watch** (Shift+F9): Evaluate expression

**Watch Expressions:**
```cpp
// Simple variable
sd->status.name

// Array range
sd->status.inventory[0], 10

// Complex expression
sd->status.hp * 100 / sd->status.max_hp

// Function call (may have side effects!)
strlen(sd->status.name)

// Type cast
(map_session_data*)bl

// Conditional
sd->status.hp > 0 ? "Alive" : "Dead"
```

**Format Specifiers:**
```cpp
sd->status.account_id, d      // Decimal
sd->status.account_id, x      // Hexadecimal
sd->status.account_id, b      // Binary
sd->status.name, s            // String
sd->status.name, s8           // UTF-8 string
sd, !                         // Type info
```

**Memory Window:**
```
Debug → Windows → Memory → Memory 1-4
```
- View raw memory at address
- Edit memory values
- Search for byte patterns

**Disassembly Window:**
```
Debug → Windows → Disassembly (Alt+8)
```
- View assembly code
- Step through assembly instructions
- Show source annotations

### Call Stack & Threads

**Call Stack Window:**
```
Debug → Windows → Call Stack (Ctrl+Alt+C)
```

**Features:**
- Double-click frame to navigate
- Right-click → "Show External Code" to see system calls
- Right-click → "Show Module Names" for DLL info
- Right-click → "Load Symbols" for missing symbols

**Threads Window:**
```
Debug → Windows → Threads (Ctrl+Alt+H)
```

**Thread Operations:**
- Double-click to switch to thread
- Right-click → Freeze to pause thread
- Right-click → Thaw to resume thread
- Flag important threads for tracking

### Advanced Visual Studio Debugging

**Data Breakpoints:**
```
Debug → New Breakpoint → Data Breakpoint
```
- Break when memory location changes
- Useful for tracking corruption
- Example: `&sd->status.hp` breaks when HP changes

**Function Breakpoints:**
```
Debug → New Breakpoint → Function Breakpoint
```
- Break on function name
- Example: `script_run`
- Supports wildcards: `script_*`

**Conditional Breakpoints for Performance:**
```cpp
// Only break for specific account
sd != nullptr && sd->status.account_id == 150000

// Only break when HP critical
sd != nullptr && sd->status.hp < (sd->status.max_hp / 10)

// Only break on error
return_value < 0
```

**Immediate Window:**
```
Debug → Windows → Immediate (Ctrl+Alt+I)
```

Execute commands during debugging:
```cpp
// Evaluate expression
? sd->status.name

// Call function
? strlen(sd->status.name)

// Modify variable
sd->status.hp = 5000

// Complex operations
? clif_displaymessage(sd->fd, "Debug message")
```

**Parallel Stacks & Tasks:**
```
Debug → Windows → Parallel Stacks
Debug → Windows → Parallel Tasks
```
- Visualize multi-threaded execution
- See all thread call stacks simultaneously
- Identify deadlocks

**Debugging Multi-Process (Multiple Servers):**
1. Debug → Attach to Process (Ctrl+Alt+P)
2. Select map-server, char-server, login-server
3. Click "Attach"
4. All servers now in same debug session

**IntelliTrace (Enterprise Edition):**
- Records execution history
- Step backwards through code
- See variable values at any point
- Save debug sessions for later analysis

---

## Memory Leak Detection

### Valgrind (Linux)

**Installation:**
```bash
# Ubuntu/Debian
sudo apt-get install valgrind

# CentOS/RHEL
sudo yum install valgrind
```

**Basic Leak Check:**
```bash
valgrind --leak-check=full \
         --show-leak-kinds=all \
         --track-origins=yes \
         --verbose \
         --log-file=valgrind.log \
         ./map-server
```

**Valgrind Options:**
```bash
--leak-check=full           # Detailed leak information
--show-leak-kinds=all       # Show all leak types
--track-origins=yes         # Track origin of uninitialized values
--verbose                   # Verbose output
--log-file=valgrind.log     # Log to file
--num-callers=30            # Stack trace depth
--suppressions=supp.txt     # Suppression file
--gen-suppressions=all      # Generate suppressions
```

**Leak Types:**
- **Definitely lost**: Memory leaked, no references
- **Indirectly lost**: Memory pointed to by leaked blocks
- **Possibly lost**: Pointers to middle of blocks
- **Still reachable**: Memory still referenced but not freed

**Example Output:**
```
==12345== HEAP SUMMARY:
==12345==     in use at exit: 1,024 bytes in 1 blocks
==12345==   total heap usage: 500 allocs, 499 frees, 102,400 bytes allocated
==12345==
==12345== 1,024 bytes in 1 blocks are definitely lost in loss record 1 of 1
==12345==    at 0x4C2FB0F: malloc (in /usr/lib/valgrind/vgpreload_memcheck-amd64-linux.so)
==12345==    by 0x123456: script_run (script.cpp:1234)
==12345==    by 0x234567: npc_scriptcont (npc.cpp:2345)
==12345==    by 0x345678: main (map.cpp:3456)
```

**Suppression File (valgrind.supp):**
```
{
   MySQL_Library_Leak
   Memcheck:Leak
   ...
   obj:*/libmysqlclient.so.*
}

{
   PCRE_JIT_Leak
   Memcheck:Leak
   ...
   fun:pcre_compile
}
```

**Usage with Suppression:**
```bash
valgrind --leak-check=full \
         --suppressions=valgrind.supp \
         ./map-server
```

### AddressSanitizer (ASan)

**Compile with ASan:**
```bash
cmake -DCMAKE_BUILD_TYPE=Debug \
      -DCMAKE_C_FLAGS="-fsanitize=address -fno-omit-frame-pointer -g" \
      -DCMAKE_CXX_FLAGS="-fsanitize=address -fno-omit-frame-pointer -g" \
      -DCMAKE_EXE_LINKER_FLAGS="-fsanitize=address" \
      ..
cmake --build .
```

**Run with ASan:**
```bash
# Direct run
./map-server

# With options
ASAN_OPTIONS=detect_leaks=1:log_path=asan.log ./map-server
```

**ASan Environment Variables:**
```bash
export ASAN_OPTIONS="\
detect_leaks=1:\
check_initialization_order=1:\
detect_stack_use_after_return=1:\
strict_init_order=1:\
log_path=asan.log:\
symbolize=1:\
halt_on_error=0"
```

**ASan Detects:**
- Heap buffer overflow
- Stack buffer overflow
- Use after free
- Use after return
- Use after scope
- Double free
- Memory leaks

**Example ASan Output:**
```
=================================================================
==12345==ERROR: AddressSanitizer: heap-use-after-free on address 0x60300000eff0
READ of size 8 at 0x60300000eff0 thread T0
    #0 0x555555558234 in script_run src/map/script.cpp:1234
    #1 0x555555559345 in npc_scriptcont src/map/npc.cpp:2345
    #2 0x55555555a456 in main src/map/map.cpp:3456

0x60300000eff0 is located 0 bytes inside of 1024-byte region [0x60300000eff0,0x60300000f3f0)
freed by thread T0 here:
    #0 0x7ffff7a12345 in free (/lib/x86_64-linux-gnu/libasan.so.5+0x12345)
    #1 0x555555557123 in script_free_code src/map/script.cpp:789

previously allocated by thread T0 here:
    #0 0x7ffff7a23456 in malloc (/lib/x86_64-linux-gnu/libasan.so.5+0x23456)
    #1 0x555555556012 in script_alloc_code src/map/script.cpp:456
```

### LeakSanitizer (LSan)

**Enable LSan (part of ASan):**
```bash
ASAN_OPTIONS=detect_leaks=1 ./map-server
```

**Standalone LSan:**
```bash
cmake -DCMAKE_C_FLAGS="-fsanitize=leak" \
      -DCMAKE_CXX_FLAGS="-fsanitize=leak" \
      ..
```

**LSan Suppressions (lsan.supp):**
```
leak:mysql_init
leak:pcre_compile
leak:ssl_init
```

**Run with Suppression:**
```bash
LSAN_OPTIONS=suppressions=lsan.supp ./map-server
```

### Visual Studio Memory Diagnostics

**Diagnostic Tools Window:**
```
Debug → Windows → Show Diagnostic Tools (Ctrl+Alt+F2)
```

**Features:**
- Memory usage graph
- CPU usage graph
- Events timeline
- Take memory snapshots

**Memory Snapshot:**
1. Start debugging (F5)
2. Click "Take Snapshot" in Diagnostic Tools
3. Perform operations
4. Take another snapshot
5. Compare snapshots to see leaks

**CRT Debug Heap:**
```cpp
// Enable CRT memory leak detection
#define _CRTDBG_MAP_ALLOC
#include <stdlib.h>
#include <crtdbg.h>

int main() {
    // Enable leak detection at exit
    _CrtSetDbgFlag(_CRTDBG_ALLOC_MEM_DF | _CRTDBG_LEAK_CHECK_DF);

    // Set breakpoint on specific allocation
    _CrtSetBreakAlloc(1234);  // Break on allocation #1234

    // Your code...

    // Dump leaks
    _CrtDumpMemoryLeaks();

    return 0;
}
```

---

## Profiling & Performance Analysis

### gprof (GNU Profiler)

**Compile with Profiling:**
```bash
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo \
      -DCMAKE_C_FLAGS="-pg" \
      -DCMAKE_CXX_FLAGS="-pg" \
      -DCMAKE_EXE_LINKER_FLAGS="-pg" \
      ..
cmake --build .
```

**Run and Generate Profile:**
```bash
# Run program (generates gmon.out)
./map-server

# Generate report
gprof ./map-server gmon.out > profile.txt

# View report
less profile.txt
```

**gprof Output Sections:**

1. **Flat Profile**:
```
  %   cumulative   self              self     total
 time   seconds   seconds    calls  ms/call  ms/call  name
 33.33      0.10     0.10    50000     0.00     0.00  battle_calc_damage
 16.67      0.15     0.05   100000     0.00     0.00  status_calc_misc
 11.11      0.18     0.03    75000     0.00     0.00  skill_castend_nodamage_id
```

2. **Call Graph**:
```
index % time    self  children    called     name
                0.10    0.05   50000/50000       battle_calc_attack [2]
[1]     50.0    0.10    0.05   50000         battle_calc_damage [1]
                0.03    0.00   50000/100000      status_calc_misc [3]
                0.02    0.00   50000/50000       battle_calc_defense [4]
```

### perf (Linux Performance Counter)

**Installation:**
```bash
# Ubuntu/Debian
sudo apt-get install linux-tools-common linux-tools-generic linux-tools-`uname -r`
```

**Basic Profiling:**
```bash
# Record performance data
sudo perf record -g ./map-server

# View report
sudo perf report

# Record with call graphs
sudo perf record -g --call-graph dwarf ./map-server

# Record specific events
sudo perf record -e cpu-clock,cache-misses ./map-server
```

**Real-time Monitoring:**
```bash
# Top-like interface
sudo perf top

# Monitor specific process
sudo perf top -p $(pidof map-server)

# Show call graphs
sudo perf top -g
```

**Advanced perf Commands:**
```bash
# CPU sampling
sudo perf stat -e cycles,instructions,cache-references,cache-misses ./map-server

# Annotate source code
sudo perf annotate

# Trace system calls
sudo perf trace -p $(pidof map-server)

# Memory access profiling
sudo perf mem record ./map-server
sudo perf mem report
```

**perf Output Example:**
```
Samples: 10K of event 'cpu-clock', Event count (approx.): 2500000000
Overhead  Command      Shared Object      Symbol
  33.45%  map-server   map-server         [.] battle_calc_damage
  18.23%  map-server   libc-2.31.so       [.] malloc
  12.67%  map-server   map-server         [.] script_run
   8.92%  map-server   map-server         [.] status_calc_misc
```

### Visual Studio Performance Profiler

**Start Profiling:**
```
Debug → Performance Profiler (Alt+F2)
```

**Profiling Tools:**
1. **CPU Usage**: Function-level CPU profiling
2. **Memory Usage**: Heap allocations and object lifetimes
3. **GPU Usage**: DirectX/graphics profiling
4. **Application Timeline**: UI responsiveness
5. **.NET Object Allocation**: .NET specific

**CPU Usage Profiling:**
1. Select "CPU Usage"
2. Click "Start"
3. Perform operations
4. Click "Stop Collection"
5. Analyze results

**Hot Path Analysis:**
- Shows most expensive call paths
- Flame graph visualization
- Filter by module, function
- Export to CSV

**Instrumentation:**
```cpp
#include <profileapi.h>

// Mark region
QueryPerformanceCounter(&start);
// ... code to profile ...
QueryPerformanceCounter(&end);

double elapsed = (double)(end.QuadPart - start.QuadPart) / frequency.QuadPart;
```

### Custom Profiling

**Simple Timer:**
```cpp
// Simple microsecond timer
class ProfileTimer {
    std::chrono::high_resolution_clock::time_point start_time;
    const char* name;
public:
    ProfileTimer(const char* n) : name(n) {
        start_time = std::chrono::high_resolution_clock::now();
    }

    ~ProfileTimer() {
        auto end_time = std::chrono::high_resolution_clock::now();
        auto duration = std::chrono::duration_cast<std::chrono::microseconds>(
            end_time - start_time
        ).count();
        ShowInfo("%s took %lld μs\n", name, duration);
    }
};

// Usage
void some_function() {
    ProfileTimer timer("some_function");
    // ... function code ...
}  // Automatically prints duration on exit
```

**Scoped Profiler with Accumulation:**
```cpp
struct ProfileStats {
    uint64 call_count;
    uint64 total_time_us;
    uint64 min_time_us;
    uint64 max_time_us;
};

std::unordered_map<std::string, ProfileStats> g_profile_stats;

class ScopedProfiler {
    std::string name;
    std::chrono::high_resolution_clock::time_point start;
public:
    ScopedProfiler(const char* n) : name(n) {
        start = std::chrono::high_resolution_clock::now();
    }

    ~ScopedProfiler() {
        auto end = std::chrono::high_resolution_clock::now();
        auto duration = std::chrono::duration_cast<std::chrono::microseconds>(
            end - start
        ).count();

        auto& stats = g_profile_stats[name];
        stats.call_count++;
        stats.total_time_us += duration;
        stats.min_time_us = (stats.call_count == 1) ? duration :
                             std::min(stats.min_time_us, (uint64)duration);
        stats.max_time_us = std::max(stats.max_time_us, (uint64)duration);
    }
};

// Print stats
void print_profile_stats() {
    ShowInfo("=== Profile Stats ===\n");
    for (const auto& [name, stats] : g_profile_stats) {
        ShowInfo("%s: calls=%llu avg=%llu min=%llu max=%llu total=%llu\n",
                 name.c_str(), stats.call_count,
                 stats.total_time_us / stats.call_count,
                 stats.min_time_us, stats.max_time_us, stats.total_time_us);
    }
}
```

---

## Common Errors & Fixes

### MySQL Not Found

**Error:**
```
CMake Error: Could not find MySQL
-- Could NOT find MySQL (missing: MYSQL_LIBRARY MYSQL_INCLUDE_DIR)
```

**Fix 1: Specify MySQL Path**
```bash
cmake -DMYSQL_INCLUDE_DIR=/usr/include/mysql \
      -DMYSQL_LIBRARY=/usr/lib/x86_64-linux-gnu/libmysqlclient.so \
      ..
```

**Fix 2: Install Development Package**
```bash
# Ubuntu/Debian
sudo apt-get install libmariadb-dev libmariadb-dev-compat

# CentOS/RHEL
sudo yum install mysql-devel

# Find MySQL manually
sudo find / -name "mysql.h" 2>/dev/null
sudo find / -name "libmysqlclient.so" 2>/dev/null
```

**Fix 3: Use pkg-config**
```bash
pkg-config --cflags --libs mysqlclient
# Use output in cmake command
```

### PCRE Missing

**Error:**
```
fatal error: pcre.h: No such file or directory
 #include <pcre.h>
```

**Fix 1: Install PCRE**
```bash
# Ubuntu/Debian
sudo apt-get install libpcre3-dev

# CentOS/RHEL
sudo yum install pcre-devel
```

**Fix 2: Disable PCRE**
```bash
cmake -DWITH_PCRE=OFF ..
```

**Fix 3: Specify PCRE Path**
```bash
cmake -DPCRE_INCLUDE_DIR=/usr/include \
      -DPCRE_LIBRARY=/usr/lib/libpcre.so \
      ..
```

### Linker Errors

**Error: Undefined Reference**
```
undefined reference to `mysql_init'
undefined reference to `pcre_compile'
```

**Fix: Check Link Order**
```cmake
# Ensure libraries linked correctly
target_link_libraries(map-server
    common
    ${MYSQL_LIBRARY}
    ${PCRE_LIBRARY}
    ${ZLIB_LIBRARY}
)
```

**Error: Multiple Definitions**
```
multiple definition of `status_calc_pc'
```

**Fix: Check Header Guards**
```cpp
// status.hpp
#ifndef STATUS_HPP
#define STATUS_HPP

// Declarations only (extern)
extern void status_calc_pc(struct map_session_data* sd);

#endif // STATUS_HPP
```

**Error: Cannot Find -lmysqlclient**
```
/usr/bin/ld: cannot find -lmysqlclient
```

**Fix:**
```bash
# Find library
sudo find / -name "libmysqlclient*" 2>/dev/null

# Create symlink if needed
sudo ln -s /usr/lib/x86_64-linux-gnu/libmariadb.so /usr/lib/x86_64-linux-gnu/libmysqlclient.so

# Or specify exact library
cmake -DMYSQL_LIBRARY=/usr/lib/x86_64-linux-gnu/libmariadb.so ..
```

### Runtime Errors

**Error: Segmentation Fault on Startup**
```
Segmentation fault (core dumped)
```

**Debug Steps:**
```bash
# Run with gdb
gdb ./map-server
(gdb) run
# When it crashes:
(gdb) bt full

# Check dependencies
ldd ./map-server
# Look for "not found"

# Run with valgrind
valgrind ./map-server
```

**Error: MySQL Connection Failed**
```
[Error]: Can't connect to MySQL server
```

**Fix:**
```bash
# Check MySQL running
sudo systemctl status mysql

# Test connection manually
mysql -h 127.0.0.1 -u ragnarok -p

# Check conf/import/inter_conf.txt
sql.db_hostname: 127.0.0.1
sql.db_port: 3306
sql.db_username: ragnarok
sql.db_password: password
sql.db_database: ragnarok

# Check firewall
sudo ufw allow 3306/tcp
```

**Error: Packet Version Mismatch**
```
[Warning]: Invalid packet version
[Warning]: Client disconnected
```

**Fix:**
```bash
# Verify PACKETVER matches client
grep "PACKETVER" src/config/core.hpp

# Rebuild with correct version
cmake -DPACKETVER=20211103 ..
cmake --build .
```

---

## Continuous Integration Setup

### GitHub Actions

**.github/workflows/build.yml:**
```yaml
name: Build rAthena

on:
  push:
    branches: [ master, develop ]
  pull_request:
    branches: [ master ]

jobs:
  build-linux:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        compiler: [gcc, clang]
        mode: [pre-renewal, renewal]

    steps:
    - uses: actions/checkout@v3

    - name: Install Dependencies
      run: |
        sudo apt-get update
        sudo apt-get install -y \
          cmake \
          ${{ matrix.compiler }} \
          libmariadb-dev \
          libmariadb-dev-compat \
          libpcre3-dev \
          zlib1g-dev

    - name: Configure
      run: |
        mkdir build && cd build
        cmake \
          -DCMAKE_BUILD_TYPE=RelWithDebInfo \
          -DCMAKE_C_COMPILER=${{ matrix.compiler == 'gcc' && 'gcc' || 'clang' }} \
          -DCMAKE_CXX_COMPILER=${{ matrix.compiler == 'gcc' && 'g++' || 'clang++' }} \
          -DRENEWAL=${{ matrix.mode == 'renewal' && 'ON' || 'OFF' }} \
          ..

    - name: Build
      run: |
        cd build
        cmake --build . --parallel $(nproc)

    - name: Test
      run: |
        cd build
        ctest --output-on-failure

    - name: Upload Artifacts
      uses: actions/upload-artifact@v3
      with:
        name: rathena-${{ matrix.compiler }}-${{ matrix.mode }}
        path: |
          build/map-server*
          build/char-server*
          build/login-server*

  build-windows:
    runs-on: windows-latest

    steps:
    - uses: actions/checkout@v3

    - name: Setup MSBuild
      uses: microsoft/setup-msbuild@v1

    - name: Build
      run: |
        MSBuild rathena.sln /p:Configuration=Release /p:Platform=x64 /m

    - name: Upload Artifacts
      uses: actions/upload-artifact@v3
      with:
        name: rathena-windows-x64
        path: |
          Release/*.exe
```

### Travis CI

**.travis.yml:**
```yaml
language: cpp

os:
  - linux
  - osx

compiler:
  - gcc
  - clang

env:
  - MODE=renewal PACKETVER=20211103
  - MODE=pre-renewal PACKETVER=20151104

addons:
  apt:
    packages:
      - cmake
      - libmariadb-dev
      - libmariadb-dev-compat
      - libpcre3-dev
      - zlib1g-dev

before_script:
  - mkdir build && cd build
  - cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo -DRENEWAL=${MODE == 'renewal'} -DPACKETVER=${PACKETVER} ..

script:
  - cmake --build . --parallel $(nproc)
  - ctest --output-on-failure

notifications:
  email:
    on_success: change
    on_failure: always
```

### Docker Build

**Dockerfile:**
```dockerfile
FROM ubuntu:22.04

# Install dependencies
RUN apt-get update && apt-get install -y \
    git \
    cmake \
    gcc \
    g++ \
    libmariadb-dev \
    libmariadb-dev-compat \
    libpcre3-dev \
    zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /rathena

# Copy source
COPY . .

# Build
RUN mkdir build && cd build && \
    cmake -DCMAKE_BUILD_TYPE=Release -DRENEWAL=ON .. && \
    cmake --build . --parallel $(nproc)

# Runtime stage
FROM ubuntu:22.04

RUN apt-get update && apt-get install -y \
    libmariadb3 \
    libpcre3 \
    zlib1g \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /rathena

# Copy built binaries
COPY --from=0 /rathena/build/map-server* ./
COPY --from=0 /rathena/build/char-server* ./
COPY --from=0 /rathena/build/login-server* ./
COPY conf ./conf/
COPY db ./db/
COPY npc ./npc/

EXPOSE 6121 6900 5121

CMD ["./map-server"]
```

**docker-compose.yml:**
```yaml
version: '3.8'

services:
  mysql:
    image: mariadb:10.6
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: ragnarok
      MYSQL_USER: ragnarok
      MYSQL_PASSWORD: ragnarok
    volumes:
      - ./sql-files:/docker-entrypoint-initdb.d
      - mysql_data:/var/lib/mysql
    ports:
      - "3306:3306"

  login-server:
    build: .
    command: ./login-server
    depends_on:
      - mysql
    ports:
      - "6900:6900"
    volumes:
      - ./conf:/rathena/conf

  char-server:
    build: .
    command: ./char-server
    depends_on:
      - mysql
      - login-server
    ports:
      - "6121:6121"
    volumes:
      - ./conf:/rathena/conf

  map-server:
    build: .
    command: ./map-server
    depends_on:
      - mysql
      - char-server
    ports:
      - "5121:5121"
    volumes:
      - ./conf:/rathena/conf
      - ./db:/rathena/db
      - ./npc:/rathena/npc

volumes:
  mysql_data:
```

---

## Optimization Flags

### GCC/Clang Optimization Levels

**-O0 (No Optimization)**
```bash
# For debugging only
cmake -DCMAKE_BUILD_TYPE=Debug \
      -DCMAKE_C_FLAGS="-O0 -g3" \
      -DCMAKE_CXX_FLAGS="-O0 -g3" \
      ..
```
- No optimizations
- Fastest compile time
- Largest binary size
- Slowest execution
- Best for debugging (variables not optimized away)

**-O1 (Basic Optimization)**
```bash
cmake -DCMAKE_C_FLAGS="-O1" \
      -DCMAKE_CXX_FLAGS="-O1" \
      ..
```
- Basic optimizations
- Reasonable compile time
- Better performance than -O0
- Variables may be optimized away

**-O2 (Recommended for Release)**
```bash
cmake -DCMAKE_BUILD_TYPE=Release \
      -DCMAKE_C_FLAGS="-O2" \
      -DCMAKE_CXX_FLAGS="-O2" \
      ..
```
- Most optimizations enabled
- Good balance of speed and size
- **Default for Release builds**
- May inline functions
- Loop optimizations
- Dead code elimination

**-O3 (Maximum Optimization)**
```bash
cmake -DCMAKE_C_FLAGS="-O3" \
      -DCMAKE_CXX_FLAGS="-O3" \
      ..
```
- All -O2 optimizations plus:
- Aggressive inlining
- Vectorization
- Loop unrolling
- May increase binary size
- Longer compile time
- May not always be faster than -O2

**-Os (Optimize for Size)**
```bash
cmake -DCMAKE_BUILD_TYPE=MinSizeRel \
      -DCMAKE_C_FLAGS="-Os" \
      -DCMAKE_CXX_FLAGS="-Os" \
      ..
```
- -O2 optimizations but favoring size
- Smaller binaries
- Good for embedded systems
- May reduce cache misses

**-Ofast (Fastest, Non-Standard)**
```bash
cmake -DCMAKE_C_FLAGS="-Ofast" \
      -DCMAKE_CXX_FLAGS="-Ofast" \
      ..
```
- -O3 plus non-standard optimizations
- Breaks strict standards compliance
- -ffast-math included (may affect precision)
- Use with caution

### Debug Symbols

**-g (Basic Debug Info)**
```bash
cmake -DCMAKE_C_FLAGS="-g" \
      -DCMAKE_CXX_FLAGS="-g" \
      ..
```
- Minimal debug information
- Line numbers, function names

**-g3 (Maximum Debug Info)**
```bash
cmake -DCMAKE_C_FLAGS="-g3" \
      -DCMAKE_CXX_FLAGS="-g3" \
      ..
```
- Includes macro definitions
- More detailed debug info
- Larger binary size

**-ggdb (GDB-Specific)**
```bash
cmake -DCMAKE_C_FLAGS="-ggdb3" \
      -DCMAKE_CXX_FLAGS="-ggdb3" \
      ..
```
- GDB-optimized debug info
- Most detailed for GDB

**RelWithDebInfo (Optimized + Debug)**
```bash
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo ..
```
- Equivalent to: -O2 -g -DNDEBUG
- **Recommended for production debugging**
- Good performance with stack traces

### Architecture-Specific Optimizations

**-march=native (CPU-Specific)**
```bash
cmake -DCMAKE_C_FLAGS="-O3 -march=native" \
      -DCMAKE_CXX_FLAGS="-O3 -march=native" \
      ..
```
- Optimizes for build machine's CPU
- May not work on different CPUs
- Enables AVX, SSE, etc. if available

**-mtune=native**
```bash
cmake -DCMAKE_C_FLAGS="-O3 -mtune=native" \
      -DCMAKE_CXX_FLAGS="-O3 -mtune=native" \
      ..
```
- Tunes for CPU but maintains compatibility
- Safer than -march=native

### Link-Time Optimization (LTO)

**Enable LTO:**
```bash
cmake -DCMAKE_BUILD_TYPE=Release \
      -DCMAKE_C_FLAGS="-O3 -flto" \
      -DCMAKE_CXX_FLAGS="-O3 -flto" \
      -DCMAKE_EXE_LINKER_FLAGS="-flto" \
      ..
```
- Optimizes across translation units
- Significantly improved performance (10-20%)
- Much longer compile/link time
- Requires AR/RANLIB with LTO support

**CMake LTO Support:**
```cmake
set(CMAKE_INTERPROCEDURAL_OPTIMIZATION TRUE)
```

### Recommended Configurations

**Development (Debug):**
```bash
cmake -DCMAKE_BUILD_TYPE=Debug \
      -DCMAKE_C_FLAGS="-O0 -g3 -Wall -Wextra" \
      -DCMAKE_CXX_FLAGS="-O0 -g3 -Wall -Wextra" \
      ..
```

**Testing (With Debug Info):**
```bash
cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo \
      -DCMAKE_C_FLAGS="-O2 -g" \
      -DCMAKE_CXX_FLAGS="-O2 -g" \
      ..
```

**Production (Maximum Performance):**
```bash
cmake -DCMAKE_BUILD_TYPE=Release \
      -DCMAKE_C_FLAGS="-O3 -march=native -flto" \
      -DCMAKE_CXX_FLAGS="-O3 -march=native -flto" \
      -DCMAKE_EXE_LINKER_FLAGS="-flto" \
      -DCMAKE_INTERPROCEDURAL_OPTIMIZATION=TRUE \
      ..
```

**Production (Portable):**
```bash
cmake -DCMAKE_BUILD_TYPE=Release \
      -DCMAKE_C_FLAGS="-O2" \
      -DCMAKE_CXX_FLAGS="-O2" \
      ..
```

---

## Real Debugging Scenarios

### Scenario 1: Server Crash on Player Login

**Symptoms:**
- Map server crashes when specific player logs in
- Other players can log in normally
- No error message, just segfault

**Investigation:**
```bash
# Step 1: Get core dump
ulimit -c unlimited
./map-server
# ... crash occurs ...

# Step 2: Analyze with GDB
gdb ./map-server core.12345

(gdb) bt full
#0  0x0000555555567890 in pc_authok (sd=0x7ffff0001234, ...) at pc.cpp:1234
#1  0x0000555555568901 in chrif_authok (fd=5) at chrif.cpp:567
...

(gdb) frame 0
(gdb) print sd
$1 = (struct map_session_data *) 0x7ffff0001234

(gdb) print *sd
$2 = {
  bl = {...},
  status = {
    account_id = 150000,
    char_id = 200000,
    name = "Player\000\000...",
    inventory = 0x0  # <-- NULL pointer!
  }
}

# Step 3: Find why inventory is NULL
(gdb) break pc.cpp:1200
(gdb) run
# When breakpoint hits:
(gdb) print sd->status.inventory
$3 = (struct item *) 0x0

# Step 4: Backtrace to see where it should be allocated
(gdb) bt
# Shows inventory allocation was skipped due to database error
```

**Root Cause:**
- Database query for inventory failed
- Code didn't check for NULL before dereferencing

**Fix:**
```cpp
// pc.cpp
int pc_authok(struct map_session_data *sd, ...) {
    // Load inventory
    if (!pc_load_inventory(sd)) {
        ShowError("pc_authok: Failed to load inventory for AID:%d\n", sd->status.account_id);
        clif_authfail_fd(sd->fd, 0);
        return 0;
    }

    // Add NULL check before use
    if (sd->status.inventory == NULL) {
        ShowError("pc_authok: Inventory is NULL for AID:%d\n", sd->status.account_id);
        return 0;
    }

    // ... rest of function ...
}
```

### Scenario 2: Memory Leak in Script Engine

**Symptoms:**
- Memory usage grows over time
- Server becomes slower after running for days
- Eventually crashes with out-of-memory

**Investigation with Valgrind:**
```bash
# Run with leak detection
valgrind --leak-check=full \
         --show-leak-kinds=all \
         --track-origins=yes \
         --log-file=valgrind.log \
         ./map-server

# After running for a while (or trigger with @reloadscript)
# Check valgrind.log

==12345== 10,485,760 bytes in 10,240 blocks are definitely lost
==12345==    at 0x4C2FB0F: malloc
==12345==    by 0x555555560123: script_alloc_state (script.cpp:2345)
==12345==    by 0x555555561234: run_script (script.cpp:3456)
==12345==    by 0x555555562345: npc_event (npc.cpp:4567)
```

**Investigation with GDB:**
```gdb
# Set breakpoint on allocation
(gdb) break script_alloc_state

# Run and trigger leak (e.g., @reloadscript)
(gdb) run

# Breakpoint hit, get address
(gdb) print $rax
$1 = 0x7ffff0123456

# Set watchpoint on this memory
(gdb) watch *(void**)0x7ffff0123456

# Continue - see if it's ever freed
(gdb) continue
# ... runs indefinitely, never freed!
```

**Finding the Leak:**
```gdb
# Search for where script states are stored
(gdb) grep -r "script_state" src/map/

# Found: Script states added to list but never removed on certain error paths
```

**Root Cause:**
```cpp
// script.cpp - Original code
struct script_state* run_script(const char* script, ...) {
    struct script_state* st = script_alloc_state();

    if (!script || !script[0]) {
        // ERROR: Early return without freeing st!
        return NULL;
    }

    // ... normal execution ...
    return st;
}
```

**Fix:**
```cpp
// script.cpp - Fixed code
struct script_state* run_script(const char* script, ...) {
    if (!script || !script[0]) {
        return NULL;  // Check BEFORE allocation
    }

    struct script_state* st = script_alloc_state();

    // ... normal execution ...
    return st;
}

// Also add cleanup in error paths
struct script_state* run_script(const char* script, ...) {
    struct script_state* st = script_alloc_state();

    if (some_error) {
        script_free_state(st);  // Clean up on error
        return NULL;
    }

    // ... normal execution ...
    return st;
}
```

### Scenario 3: Performance Problem - Slow Skill Casting

**Symptoms:**
- Players report laggy skill casting
- Skills sometimes take seconds to execute
- CPU usage spikes during mass skill usage

**Investigation with perf:**
```bash
# Record performance data during lag
sudo perf record -g -p $(pidof map-server)
# ... let it record during lag event ...
# Ctrl+C to stop

# Analyze
sudo perf report

# Output shows:
Overhead  Symbol
  45.67%  status_calc_pc
  23.45%  battle_calc_damage
  15.23%  map_foreachinrange
```

**Deep Dive with perf:**
```bash
# Annotate hot function
sudo perf annotate status_calc_pc

# Shows most time spent in:
  15.67%  for (i = 0; i < MAX_INVENTORY; i++) {
  12.34%      if (sd->status.inventory[i].card[0] == CARD0_CREATE) {
   8.90%          // Card bonus calculation
```

**Investigation with GDB:**
```gdb
# Break at slow function
(gdb) break status_calc_pc

# Run until break
(gdb) run

# Count loop iterations
(gdb) set pagination off
(gdb) set $count = 0
(gdb) break script.cpp:1234 if (++$count >= 100)
(gdb) commands
    silent
    printf "Iterations: %d\n", $count
    continue
end
(gdb) continue
```

**Profile with Custom Timer:**
```cpp
// Add to status.cpp
void status_calc_pc(struct map_session_data* sd, bool first) {
    auto start = std::chrono::high_resolution_clock::now();

    // ... existing code ...

    auto end = std::chrono::high_resolution_clock::now();
    auto duration = std::chrono::duration_cast<std::chrono::microseconds>(end - start).count();

    if (duration > 1000) {  // Log if > 1ms
        ShowWarning("status_calc_pc took %lld μs for AID:%d\n", duration, sd->status.account_id);
    }
}
```

**Root Cause:**
- `status_calc_pc` called every time any stat changes
- Recalculates ALL equipment bonuses every time
- Called hundreds of times during skill casting

**Fix - Add Caching:**
```cpp
// status.hpp
struct map_session_data {
    // ...
    struct {
        uint32 calc_flag;  // Dirty flags for what needs recalc
        tick_t last_calc;  // Last calculation time
    } status_cache;
};

// status.cpp
void status_calc_pc(struct map_session_data* sd, enum e_status_calc_flag flag) {
    // Check if recently calculated
    if (gettick() - sd->status_cache.last_calc < 100 &&
        !(sd->status_cache.calc_flag & flag)) {
        return;  // Use cached values
    }

    // Only recalculate what changed
    if (flag & SCF_EQUIP) {
        status_calc_pc_equipment(sd);
    }
    if (flag & SCF_BASE) {
        status_calc_pc_base(sd);
    }

    sd->status_cache.last_calc = gettick();
    sd->status_cache.calc_flag = 0;
}
```

**Result:**
- 90% reduction in `status_calc_pc` calls
- Skill casting lag eliminated
- CPU usage during mass skills reduced by 60%

### Scenario 4: Data Corruption - Items Duplicating

**Symptoms:**
- Players report items duplicating randomly
- Database shows duplicate inventory entries
- No obvious pattern

**Investigation:**
```bash
# Enable MySQL query logging
# In MySQL:
SET GLOBAL general_log = 'ON';
SET GLOBAL log_output = 'TABLE';

# Watch queries in real-time
mysql> SELECT * FROM mysql.general_log
       WHERE command_type = 'Query'
       AND argument LIKE '%inventory%'
       ORDER BY event_time DESC
       LIMIT 50;
```

**Add Debug Logging:**
```cpp
// pc.cpp - Add extensive logging
int pc_additem(struct map_session_data *sd, struct item *item_data, int amount, e_log_pick_type log_type) {
    ShowDebug("pc_additem: AID:%d adding item %d (amount:%d)\n",
              sd->status.account_id, item_data->nameid, amount);

    // ... existing code ...

    // Log inventory state
    for (int i = 0; i < MAX_INVENTORY; i++) {
        if (sd->status.inventory[i].nameid == item_data->nameid) {
            ShowDebug("  Slot %d: ID:%d Amount:%d\n",
                      i, sd->status.inventory[i].nameid, sd->status.inventory[i].amount);
        }
    }

    return 0;
}
```

**Found Race Condition:**
```cpp
// Original code - NOT thread-safe
int pc_additem(...) {
    // Find existing stack
    for (i = 0; i < MAX_INVENTORY; i++) {
        if (sd->status.inventory[i].nameid == item_data->nameid) {
            // Add to existing stack
            sd->status.inventory[i].amount += amount;
            intif_saveitem(&sd->status.inventory[i]);  // <-- ASYNC!
            return 0;
        }
    }

    // Add new item
    for (i = 0; i < MAX_INVENTORY; i++) {
        if (sd->status.inventory[i].nameid == 0) {
            memcpy(&sd->status.inventory[i], item_data, sizeof(struct item));
            sd->status.inventory[i].amount = amount;
            intif_saveitem(&sd->status.inventory[i]);  // <-- ASYNC!
            return 0;
        }
    }
}
```

**Problem:**
- Two calls to `pc_additem` in quick succession
- First call finds empty slot, starts async save
- Second call runs before first save completes
- Second call finds SAME empty slot (not yet marked as used)
- Both save to database with same slot number
- Result: Duplication

**Fix - Add Locking:**
```cpp
// pc.hpp
struct map_session_data {
    // ...
    std::mutex inventory_mutex;
    std::atomic<bool> inventory_saving;
};

// pc.cpp - Fixed code
int pc_additem(struct map_session_data *sd, struct item *item_data, int amount, e_log_pick_type log_type) {
    std::lock_guard<std::mutex> lock(sd->inventory_mutex);

    // Wait for any pending saves
    while (sd->inventory_saving.load()) {
        std::this_thread::sleep_for(std::chrono::milliseconds(1));
    }

    // Find existing stack
    for (i = 0; i < MAX_INVENTORY; i++) {
        if (sd->status.inventory[i].nameid == item_data->nameid) {
            sd->status.inventory[i].amount += amount;
            sd->inventory_saving.store(true);
            intif_saveitem(&sd->status.inventory[i], [sd]() {
                sd->inventory_saving.store(false);
            });
            return 0;
        }
    }

    // Add new item...
}
```

---

**Document Size: ~18KB**

This reference covers all essential compilation and debugging workflows for rAthena development, from basic builds to advanced debugging scenarios with real-world examples.
