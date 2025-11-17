---
kb_id: KB_REF_026
title: "Compilation and Debugging rAthena"
category: Source Code
keywords: [compilation, debugging, cmake, gdb, visual_studio, valgrind, memory_leaks, compilation_errors, makefile, build_errors, debugging_techniques]
related_files: [
  "CMakeLists.txt",
  "configure",
  "Makefile.in",
  "rathena-vs##.sln",
  "src/"
]
difficulty: intermediate
use_case: "Compiling rAthena from source and debugging code issues"
version: rAthena 2024
last_updated: 2024-01-15
---

# Compilation and Debugging rAthena

## Quick Reference

### **Compile (Linux - CMake)**
```bash
cd rathena
mkdir build && cd build
cmake ..
make -j$(nproc)
make install
```

### **Compile (Linux - Configure)**
```bash
cd rathena
./configure
make clean
make -j$(nproc)
```

### **Debug with GDB**
```bash
gdb ./map-server
(gdb) run
(gdb) bt              # Backtrace on crash
(gdb) print variable  # Inspect variable
(gdb) break pc_heal   # Set breakpoint
```

### **Check Memory Leaks (Valgrind)**
```bash
valgrind --leak-check=full --show-leak-kinds=all ./map-server
```

---

## Table of Contents
1. [Compilation Methods](#compilation-methods)
2. [Linux Compilation (CMake)](#linux-compilation-cmake)
3. [Linux Compilation (Configure)](#linux-compilation-configure)
4. [Windows Compilation (Visual Studio)](#windows-compilation-visual-studio)
5. [Common Compilation Errors](#common-compilation-errors)
6. [Debugging with GDB (Linux)](#debugging-with-gdb-linux)
7. [Debugging with Visual Studio (Windows)](#debugging-with-visual-studio-windows)
8. [Memory Leak Detection](#memory-leak-detection)
9. [Performance Profiling](#performance-profiling)
10. [Best Practices](#best-practices)

---

## Compilation Methods

### **3 Compilation Systems**

| Method | Platform | Build Tool | Difficulty |
|--------|----------|------------|------------|
| **CMake** | Linux, Windows, macOS | cmake + make | Easy |
| **Configure** | Linux, macOS, Cygwin | autoconf + make | Medium |
| **Visual Studio** | Windows | MSBuild | Easy |

### **Which Method to Use?**

**CMake** (Recommended):
- ✅ Cross-platform
- ✅ Fast parallel builds
- ✅ Easy IDE integration (CLion, VS Code)
- ✅ Clean build directory separation

**Configure**:
- ✅ Traditional UNIX method
- ✅ Fine-grained control
- ⚠️ Requires autoconf tools

**Visual Studio**:
- ✅ Windows GUI debugging
- ✅ Integrated development environment
- ⚠️ Windows-only

---

## Linux Compilation (CMake)

### **Requirements**

```bash
# Ubuntu/Debian
sudo apt-get update
sudo apt-get install -y \
    git gcc g++ make cmake \
    libmysqlclient-dev zlib1g-dev libpcre3-dev

# CentOS/RHEL
sudo yum install -y \
    git gcc gcc-c++ make cmake \
    mysql-devel zlib-devel pcre-devel

# Arch Linux
sudo pacman -S \
    git gcc make cmake \
    mariadb-libs zlib pcre
```

---

### **Step-by-Step Compilation**

**1. Clone Repository**
```bash
git clone https://github.com/rathena/rathena.git
cd rathena
```

**2. Create Build Directory**
```bash
mkdir build
cd build
```

**3. Configure with CMake**
```bash
cmake .. \
    -DCMAKE_BUILD_TYPE=RelWithDebInfo \
    -DINSTALL_TO_SOURCE=ON

# Build types:
# - Debug: Full debug symbols, no optimization (-g -O0)
# - Release: Full optimization, no debug symbols (-O3)
# - RelWithDebInfo: Optimization + debug symbols (-O2 -g)
# - MinSizeRel: Optimize for size (-Os)
```

**4. Compile**
```bash
# Use all CPU cores
make -j$(nproc)

# Or specify core count manually
make -j4  # 4 cores
```

**5. Install**
```bash
make install
```

**6. Run Servers**
```bash
cd ..
./login-server &
./char-server &
./map-server
```

---

### **CMake Options**

```bash
cmake .. \
    -DCMAKE_BUILD_TYPE=RelWithDebInfo \
    -DINSTALL_TO_SOURCE=ON \
    -DENABLE_PACKETVER=20180620 \
    -DENABLE_RENEWAL=ON \
    -DENABLE_PRERE_MODE=OFF \
    -DWITH_PCRE=ON \
    -DCMAKE_C_FLAGS="-Wall -Wextra" \
    -DCMAKE_CXX_FLAGS="-Wall -Wextra"

# Options:
# ENABLE_PACKETVER: Client packet version
# ENABLE_RENEWAL: Renewal mode (ON/OFF)
# ENABLE_PRERE_MODE: Pre-Renewal mode (ON/OFF)
# WITH_PCRE: Enable Perl-compatible regex
```

---

### **Clean Build**

```bash
# Clean build directory
cd build
rm -rf *
cmake ..
make -j$(nproc)

# Or rebuild from scratch
cd ..
rm -rf build
mkdir build
cd build
cmake ..
make -j$(nproc)
```

---

## Linux Compilation (Configure)

### **Requirements**

```bash
# Install autoconf tools
sudo apt-get install -y autoconf automake

# Other requirements same as CMake
sudo apt-get install -y \
    git gcc g++ make \
    libmysqlclient-dev zlib1g-dev libpcre3-dev
```

---

### **Step-by-Step Compilation**

**1. Generate Configure Script** (if needed)
```bash
autoconf configure.in > configure
chmod +x configure
```

**2. Run Configure**
```bash
./configure \
    --enable-packetver=20180620 \
    --enable-renewal \
    --with-pcre

# Options:
# --enable-packetver=YYYYMMDD
# --enable-renewal
# --enable-prere
# --with-pcre
# --enable-debug
```

**3. Compile**
```bash
make clean
make -j$(nproc)
```

**4. Run Servers**
```bash
./login-server &
./char-server &
./map-server
```

---

### **Configure Options**

```bash
./configure --help  # Show all options

# Common options:
./configure \
    --enable-debug \              # Enable debug mode
    --enable-renewal \            # Enable Renewal
    --enable-packetver=20180620 \ # Set packet version
    --with-pcre \                 # Enable PCRE
    --with-mysql=/usr/bin/mysql_config  # Specify MySQL path
```

---

## Windows Compilation (Visual Studio)

### **Requirements**

- **Visual Studio 2019 or 2022** (Community Edition is free)
- **MySQL Connector/C** (libmysql)
- **Git for Windows**

---

### **Step-by-Step Compilation**

**1. Install Visual Studio**
- Download from https://visualstudio.microsoft.com/
- Select "Desktop development with C++"
- Include: MSVC, Windows SDK, CMake tools

**2. Install MySQL Connector**
```powershell
# Download MySQL Connector/C from:
# https://dev.mysql.com/downloads/connector/c/

# Install to default path or update project settings
```

**3. Clone Repository**
```powershell
git clone https://github.com/rathena/rathena.git
cd rathena
```

**4. Open Solution**
- Open `rathena-vs19.sln` (VS 2019) or `rathena-vs22.sln` (VS 2022)
- Select **Build Configuration**:
  - **Debug**: For debugging (slow, full symbols)
  - **Release**: For production (fast, optimized)

**5. Build**
- Right-click solution → **Rebuild Solution**
- Or: `Ctrl+Shift+B`
- Executables will be in: `build/bin/RelWithDebInfo/` or `build/bin/Debug/`

**6. Copy Files**
```powershell
# Copy executables to root
copy build\bin\RelWithDebInfo\*.exe .

# Copy MySQL DLL
copy "C:\Program Files\MySQL\MySQL Connector C 6.1\lib\libmysql.dll" .
```

**7. Run Servers**
```powershell
start login-server.exe
start char-server.exe
start map-server.exe
```

---

## Common Compilation Errors

### **Error 1: MySQL Not Found**

**Error**:
```
CMake Error: Could not find MySQL
```

**Fix (Linux)**:
```bash
# Ubuntu/Debian
sudo apt-get install libmysqlclient-dev

# CentOS/RHEL
sudo yum install mysql-devel

# Arch
sudo pacman -S mariadb-libs

# If installed but not found, specify path:
cmake .. -DMYSQL_INCLUDE_DIR=/usr/include/mysql \
         -DMYSQL_LIBRARY=/usr/lib/x86_64-linux-gnu/libmysqlclient.so
```

**Fix (Windows)**:
- Download MySQL Connector/C
- Install to `C:\Program Files\MySQL\MySQL Connector C 6.1`
- Update Visual Studio project settings:
  - Right-click project → **Properties**
  - **C/C++** → **Additional Include Directories** → Add MySQL include path
  - **Linker** → **Additional Library Directories** → Add MySQL lib path

---

### **Error 2: PCRE Not Found**

**Error**:
```
error: pcre.h: No such file or directory
```

**Fix (Linux)**:
```bash
# Ubuntu/Debian
sudo apt-get install libpcre3-dev

# CentOS/RHEL
sudo yum install pcre-devel

# Arch
sudo pacman -S pcre
```

**Fix (Windows)**:
- PCRE is bundled with rAthena source (`3rdparty/pcre/`)
- Should work out of the box
- If issues, check project include paths

---

### **Error 3: Zlib Not Found**

**Error**:
```
fatal error: zlib.h: No such file or directory
```

**Fix (Linux)**:
```bash
# Ubuntu/Debian
sudo apt-get install zlib1g-dev

# CentOS/RHEL
sudo yum install zlib-devel

# Arch
sudo pacman -S zlib
```

---

### **Error 4: Undefined Reference Errors**

**Error**:
```
undefined reference to `function_name'
```

**Causes**:
1. Missing source file in CMakeLists.txt
2. Function declared but not implemented
3. Linking order issue

**Fix**:
```bash
# Clean and rebuild
make clean
make -j$(nproc)

# If using custom files, add to CMakeLists.txt:
# src/map/CMakeLists.txt
set( MAP_SOURCES
    # ... existing files ...
    ${MAP_SOURCE_DIR}/myfile.cpp
)
```

---

### **Error 5: C++11/14/17 Errors**

**Error**:
```
error: 'auto' was not declared in this scope
error: 'nullptr' was not declared in this scope
```

**Fix**:
```bash
# Update CMakeLists.txt to require C++17
cmake .. -DCMAKE_CXX_STANDARD=17

# Or edit src/CMakeLists.txt:
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
```

---

### **Error 6: Packet Version Mismatch**

**Error**:
```
error: 'packet_struct_name' was not declared
```

**Fix**:
```bash
# Set correct packet version for your client
cmake .. -DENABLE_PACKETVER=20180620

# Common packet versions:
# 20180620 - 2018-06-20 client
# 20200401 - 2020-04-01 client
# 20211103 - 2021-11-03 client
```

---

## Debugging with GDB (Linux)

### **Install GDB**

```bash
# Ubuntu/Debian
sudo apt-get install gdb

# CentOS/RHEL
sudo yum install gdb

# Arch
sudo pacman -S gdb
```

---

### **Compile with Debug Symbols**

```bash
# CMake
cmake .. -DCMAKE_BUILD_TYPE=Debug
make -j$(nproc)

# Configure
./configure --enable-debug
make -j$(nproc)
```

---

### **Basic GDB Commands**

**Start GDB**:
```bash
gdb ./map-server

# Or attach to running process
gdb -p <process_id>
```

**Common Commands**:
```gdb
(gdb) run                       # Start program
(gdb) run --run-once            # Run with arguments

# When crashed:
(gdb) bt                        # Backtrace (call stack)
(gdb) bt full                   # Backtrace with local variables
(gdb) frame 3                   # Switch to frame 3
(gdb) info locals               # Show local variables
(gdb) print sd->status.name     # Print variable value
(gdb) print *sd                 # Print entire struct

# Breakpoints:
(gdb) break pc_heal             # Break at function
(gdb) break pc.cpp:1234         # Break at line
(gdb) break pc_heal if hp < 0   # Conditional breakpoint
(gdb) info breakpoints          # List breakpoints
(gdb) delete 1                  # Delete breakpoint 1

# Execution control:
(gdb) continue                  # Continue execution
(gdb) next                      # Step over
(gdb) step                      # Step into
(gdb) finish                    # Step out of function

# Watchpoints:
(gdb) watch sd->status.hp       # Break when variable changes
(gdb) rwatch sd->status.hp      # Break when variable is read

# Other:
(gdb) quit                      # Exit GDB
```

---

### **Example Debug Session**

**Scenario**: Server crashes in `pc_heal` function

```bash
$ gdb ./map-server
(gdb) run

# ... server crashes ...

Program received signal SIGSEGV, Segmentation fault.
0x000055555557a3b2 in pc_heal (sd=0x0, hp=500, sp=0, type=0) at pc.cpp:6234
6234        if (sd->status.hp + hp > sd->status.max_hp) {

(gdb) bt
#0  pc_heal (sd=0x0, hp=500, sp=0, type=0) at pc.cpp:6234
#1  0x00005555555b1234 in buildin_heal (st=0x7ffff0000000) at script.cpp:12345
#2  0x00005555555c5678 in run_script_main (st=0x7ffff0000000) at script.cpp:5678
#3  0x00005555555c9abc in run_script (script=0x..., pos=0, rid=150000, oid=0) at script.cpp:1234

(gdb) print sd
$1 = (struct map_session_data *) 0x0

# Issue: sd is NULL!

(gdb) frame 1
#1  0x00005555555b1234 in buildin_heal (st=0x7ffff0000000) at script.cpp:12345
12345       pc_heal(sd, amount, 0, 0);

(gdb) print sd
$2 = (struct map_session_data *) 0x0

# Check where sd came from:
(gdb) list
12340   BUILDIN(heal)
12341   {
12342       struct map_session_data *sd = script_rid2sd(st);
12343       int amount = script_getnum(st, 2);
12344
12345       pc_heal(sd, amount, 0, 0);  // BUG: No null check!
12346       return 0;
12347   }

# Fix: Add null check before pc_heal
```

**Fix in code**:
```cpp
BUILDIN(heal)
{
    struct map_session_data *sd = script_rid2sd(st);
    if (!sd) {  // Add null check
        return 1;
    }

    int amount = script_getnum(st, 2);
    pc_heal(sd, amount, 0, 0);
    return 0;
}
```

---

### **GDB with Core Dumps**

**Enable core dumps**:
```bash
ulimit -c unlimited

# Run server
./map-server

# On crash, core dump is generated
# Load core dump in GDB:
gdb ./map-server core

(gdb) bt
# ... analyze crash ...
```

---

## Debugging with Visual Studio (Windows)

### **Enable Debug Build**

1. Open solution in Visual Studio
2. Select **Debug** configuration (top toolbar)
3. Build → **Rebuild Solution**

---

### **Set Breakpoints**

1. Open source file (e.g., `src/map/pc.cpp`)
2. Click left margin on line number → **Red dot appears**
3. Or: `F9` on desired line

---

### **Start Debugging**

1. Right-click `map-server` project → **Set as Startup Project**
2. Press **F5** or **Debug → Start Debugging**
3. Execution pauses at breakpoints

---

### **Debug Controls**

| Key | Action |
|-----|--------|
| **F5** | Continue |
| **F10** | Step Over |
| **F11** | Step Into |
| **Shift+F11** | Step Out |
| **Shift+F5** | Stop Debugging |
| **F9** | Toggle Breakpoint |

---

### **Inspect Variables**

- **Autos Window**: `Debug → Windows → Autos`
- **Locals Window**: `Debug → Windows → Locals`
- **Watch Window**: `Debug → Windows → Watch`
- **Hover over variable** to see value

**Example**:
```cpp
int pc_heal(struct map_session_data *sd, int hp, int sp, int type) {
    // Set breakpoint here
    int max_hp = sd->status.max_hp;  // Hover over sd to inspect

    // Add to Watch window:
    // sd->status.hp
    // sd->status.max_hp
}
```

---

### **Call Stack**

- **Call Stack Window**: `Debug → Windows → Call Stack`
- Shows function call hierarchy
- Double-click to jump to frame

---

### **Conditional Breakpoints**

1. Right-click breakpoint → **Conditions**
2. Enter condition: `sd->status.hp < 0`
3. Breakpoint only triggers when condition is true

---

## Memory Leak Detection

### **Method 1: Valgrind (Linux)**

**Install**:
```bash
# Ubuntu/Debian
sudo apt-get install valgrind

# CentOS/RHEL
sudo yum install valgrind

# Arch
sudo pacman -S valgrind
```

**Run**:
```bash
# Basic leak check
valgrind --leak-check=full ./map-server

# Detailed leak check
valgrind \
    --leak-check=full \
    --show-leak-kinds=all \
    --track-origins=yes \
    --verbose \
    --log-file=valgrind-output.txt \
    ./map-server
```

**Example Output**:
```
==12345== 100 bytes in 1 blocks are definitely lost in loss record 1 of 1
==12345==    at 0x4C2B3F8: malloc (in /usr/lib/valgrind/vgpreload_memcheck-amd64-linux.so)
==12345==    by 0x4E9A12B: aMalloc (malloc.cpp:123)
==12345==    by 0x5123ABC: my_function (myfile.cpp:456)
==12345==    by 0x5134DEF: another_function (myfile.cpp:789)

# Fix: Free allocated memory with aFree()
```

---

### **Method 2: AddressSanitizer (Linux/Windows)**

**Compile with ASan**:
```bash
# CMake
cmake .. \
    -DCMAKE_BUILD_TYPE=Debug \
    -DCMAKE_C_FLAGS="-fsanitize=address -fno-omit-frame-pointer" \
    -DCMAKE_CXX_FLAGS="-fsanitize=address -fno-omit-frame-pointer"

make -j$(nproc)

# Run normally - ASan will report leaks automatically
./map-server
```

**Example Output**:
```
=================================================================
==12345==ERROR: LeakSanitizer: detected memory leaks

Direct leak of 100 byte(s) in 1 object(s) allocated from:
    #0 0x7f8b... in malloc
    #1 0x5555... in aMalloc malloc.cpp:123
    #2 0x5555... in my_function myfile.cpp:456
    #3 0x5555... in main main.cpp:100

# Fix the leak by freeing memory
```

---

### **Method 3: Visual Studio Memory Diagnostics**

1. **Debug → Windows → Show Diagnostic Tools**
2. **Memory Usage** tab
3. **Take Snapshot** at different points
4. Compare snapshots to find leaks

---

### **Common Memory Leak Pattern**

```cpp
// ❌ LEAK - Allocated but never freed
char *str = (char*)aMalloc(100);
strcpy(str, "Hello");
return;  // str is leaked!

// ✅ FIXED - Properly freed
char *str = (char*)aMalloc(100);
strcpy(str, "Hello");
aFree(str);  // Free memory
return;

// ✅ BETTER - Use aStrdup for strings
char *str = aStrdup("Hello");
// ... use str ...
aFree(str);
```

---

## Performance Profiling

### **Method 1: gprof (Linux)**

**Compile with profiling**:
```bash
cmake .. -DCMAKE_C_FLAGS="-pg" -DCMAKE_CXX_FLAGS="-pg"
make -j$(nproc)
```

**Run and analyze**:
```bash
./map-server
# ... let it run for a while, then stop ...

# Generate report
gprof ./map-server gmon.out > analysis.txt

# View report
less analysis.txt
```

---

### **Method 2: perf (Linux)**

**Install**:
```bash
sudo apt-get install linux-tools-common linux-tools-generic
```

**Profile**:
```bash
# Record performance data
perf record -g ./map-server

# View report
perf report

# Annotate source code
perf annotate
```

---

### **Method 3: Visual Studio Profiler**

1. **Debug → Performance Profiler**
2. Select **CPU Usage**
3. **Start**
4. Let server run
5. **Stop Collection**
6. Analyze hot spots

---

## Best Practices

### **1. Always Compile with Warnings**

```bash
cmake .. -DCMAKE_C_FLAGS="-Wall -Wextra -Werror"
```

**Fix ALL warnings before pushing code!**

---

### **2. Use Debug Builds for Development**

```bash
# Debug: Full symbols, assertions enabled
cmake .. -DCMAKE_BUILD_TYPE=Debug

# Release: For production only
cmake .. -DCMAKE_BUILD_TYPE=Release
```

---

### **3. Test Memory Leaks Regularly**

```bash
# Run with Valgrind weekly
valgrind --leak-check=full ./map-server
```

---

### **4. Use Version Control**

```bash
# Commit working changes frequently
git add src/map/myfile.cpp
git commit -m "Fixed memory leak in pc_heal"

# Create branch for experimental changes
git checkout -b feature/custom-system
```

---

### **5. Automate Testing**

```bash
#!/bin/bash
# build_and_test.sh

mkdir -p build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Debug
make -j$(nproc) || exit 1

echo "Running server for 30 seconds..."
timeout 30s ./map-server || echo "Server crashed!"
```

---

## Related References

- **Source Code Structure**: [KB_REF_SourceCodeStructure.md]
- **Custom System**: [KB_REF_PluginSystem.md]
- **Best Practices**: [KB_REF_SourceCodeBestPractices.md]
- **Database Work**: [KB_REF_DatabaseCPP.md]

---

**End of KB_REF_026 - Compilation and Debugging rAthena**
