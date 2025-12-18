# C/C++ x86_64 Reversing Lab Development Container

A comprehensive development environment for learning compilation, reverse engineering, and binary analysis of x86/x64 applications. This container provides all the essential tools for understanding low-level programming, debugging, and analyzing compiled binaries. It was originally created for studying the topic "Software Security", from [MSc in Cybersecurity and Privacy](https://www.uoc.edu/es/estudios/masters/master-universitario-ciberseguridad-privacidad), taught by [Universitat Oberta de Catalunya](https://uoc.edu) (UOC).

## 🎯 Purpose

This dev container is designed for:

- Learning assembly language (x86/x64)
- Understanding compilation processes and binary formats
- Reverse engineering compiled applications
- Binary analysis and exploitation research
- Low-level debugging and memory analysis
- Security research and vulnerability analysis

## 🛠️ Included Tools

### Compilers & Build Systems

- **GCC**: GNU Compiler Collection for C/C++
- **Clang**: LLVM-based C/C++ compiler
- **CMake**: Cross-platform build system
- **Ninja**: Fast build system
- **Make**: Classic build automation tool
- **gcc-multilib**: Support for 32-bit compilation on 64-bit systems

### Debugging & Analysis Tools

- **GDB**: GNU Debugger with full x86/x64 support
- **LLDB**: LLVM debugger
- **Valgrind**: Memory debugging and profiling
- **Binutils**: Binary analysis utilities (objdump, readelf, nm, strings, etc.)

### Code Quality Tools

- **Clang-Format**: Code formatting
- **Clang-Tidy**: Static analysis and linting
- **Doxygen**: Documentation generation

### Remote Debugging

- **OpenSSH Server**: Pre-configured for remote debugging sessions
- Port 2222 exposed for SSH connections
- Username: `vscode` / Password: `vscode`

## 📦 VS Code Extensions

### C/C++ Development
- **C/C++ Extension Pack**: IntelliSense, debugging, and code browsing
- **CMake Tools**: CMake project integration
- **Better C++ Syntax**: Enhanced syntax highlighting
- **Makefile Tools**: Makefile support

### Code Quality
- **Clang-Format**: Automatic code formatting
- **Doxygen Generator**: Generate documentation comments

### Productivity
- **GitLens**: Advanced Git integration
- **Todo Tree**: Track TODO comments
- **Bookmarks**: Mark important code locations
- **EditorConfig**: Consistent coding styles

## 🚀 Getting Started

### Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Setup Instructions

1. **Create your project structure**
   ```bash
   mkdir reversing-lab
   cd reversing-lab
   ```

2. **Add the dev container configuration**
   - Copy `.devcontainer` folder

3. **Create Docker network** (required for networking features)
   ```bash
   docker network create devnet
   ```

4. **Open in VS Code**
   ```bash
   code .
   ```

5. **Reopen in Container**
   - Press `F1` or `Ctrl+Shift+P` (Windows/Linux) / `Cmd+Shift+P` (Mac)
   - Select: `Dev Containers: Reopen in Container`
   - Wait for the container to build

## 💻 Usage Examples

### Compiling Simple Programs

**C Program:**
```bash
# Compile with debugging symbols
gcc -g -o program program.c

# Compile with optimizations disabled (easier to reverse)
gcc -O0 -g -o program program.c

# Compile 32-bit binary on 64-bit system
gcc -m32 -o program32 program.c
```

**C++ Program:**
```bash
# Compile with C++20 standard
g++ -std=c++20 -g -o program program.cpp

# Compile with Clang
clang++ -std=c++20 -g -o program program.cpp
```

### Disassembly and Analysis

**Using objdump:**
```bash
# Disassemble entire binary
objdump -d program

# Disassemble with source code intermixed
objdump -S program

# Display all headers
objdump -x program

# Show assembly with Intel syntax
objdump -M intel -d program
```

**Using readelf:**
```bash
# Display ELF header
readelf -h program

# Show section headers
readelf -S program

# Display symbol table
readelf -s program

# Show dynamic section
readelf -d program
```

**Using other binutils:**
```bash
# Extract printable strings
strings program

# List symbols
nm program

# Show file type and architecture
file program

# Display size of sections
size program
```

### Debugging with GDB

**Basic GDB commands:**
```bash
# Start GDB
gdb ./program

# Common GDB commands inside debugger:
(gdb) break main              # Set breakpoint at main
(gdb) run arg1 arg2           # Run with arguments
(gdb) disassemble main        # Disassemble function
(gdb) x/10i $rip              # Examine 10 instructions at RIP
(gdb) info registers          # Show all registers
(gdb) x/8xg $rsp              # Examine 8 quad-words at stack pointer
(gdb) stepi                   # Step one instruction
(gdb) continue                # Continue execution
```

**GDB with layout:**
```bash
gdb -tui ./program            # Start with TUI mode

# Inside GDB:
(gdb) layout asm              # Show assembly layout
(gdb) layout regs             # Show registers layout
(gdb) layout split            # Show source and assembly
```

### Memory Analysis with Valgrind

```bash
# Check for memory leaks
valgrind --leak-check=full ./program

# Detailed memory error detection
valgrind --track-origins=yes ./program

# Cache profiling
valgrind --tool=cachegrind ./program

# Call graph profiling
valgrind --tool=callgrind ./program
```

### Remote Debugging via SSH

The container runs an SSH server on port 2222 for remote debugging:

```bash
# From host machine, connect to container
ssh -p 2222 vscode@localhost
# Password: vscode

# Or use in GDB for remote debugging
gdb
(gdb) target remote localhost:2222
```

## 🏗️ Project Structure Example

```
reversing-lab/
├── .devcontainer/
│   ├── devcontainer.json
│   └── Dockerfile
├── src/
│   ├── main.c
│   ├── vulnerable.c
│   └── example.cpp
├── include/
│   └── header.h
├── build/
│   └── (compiled binaries)
├── scripts/
│   └── analyze.sh
├── CMakeLists.txt
├── Makefile
└── README.md
```

## 🔍 Learning Path

### Beginner

1. **Compile simple programs** with different optimization levels
2. **Use objdump** to see the assembly code
3. **Practice reading x86/x64 assembly**
4. **Use GDB** to step through program execution
5. **Examine memory** with GDB

### Intermediate

1. **Analyze stripped binaries** (no debug symbols)
2. **Understand calling conventions** (System V AMD64 ABI)
3. **Practice with position-independent code** (PIE)
4. **Learn stack frame analysis**
5. **Explore dynamic linking** and PLT/GOT

### Advanced

1. **Reverse engineer complex binaries**
2. **Analyze obfuscated code**
3. **Exploit development** (buffer overflows, ROP chains)
4. **Anti-debugging techniques**
5. **Binary patching and modification**

## 🔒 Security Considerations

**Important Notes:**

- This container runs with `SYS_PTRACE` capability for debugging
- `seccomp=unconfined` allows all system calls (required for some debugging scenarios)
- SSH is configured with password authentication (username: `vscode`, password: `vscode`)
- **Change default SSH password** for production or sensitive work
- This environment is for **learning and research purposes only**
- Do not use for production applications or sensitive data

### Changing SSH Password

```bash
# Inside the container
passwd
# Enter new password when prompted
```

## 📚 Recommended Resources

### Books
- "Practical Reverse Engineering" by Bruce Dang
- "The Art of Assembly Language" by Randall Hyde
- "Hacking: The Art of Exploitation" by Jon Erickson
- "Reversing: Secrets of Reverse Engineering" by Eldad Eilam

### Online Resources
- [x86/x64 Instruction Reference](https://www.felixcloutier.com/x86/)
- [GDB Documentation](https://sourceware.org/gdb/documentation/)
- [Intel 64 and IA-32 Architectures Software Developer Manuals](https://www.intel.com/content/www/us/en/developer/articles/technical/intel-sdm.html)
- [System V AMD64 ABI](https://wiki.osdev.org/System_V_ABI)

### Practice Platforms
- [Microcorruption](https://microcorruption.com/)
- [pwnable.kr](http://pwnable.kr/)
- [Exploit Education](https://exploit.education/)
- [Crackmes.one](https://crackmes.one/)

## 🐛 Troubleshooting

### Container won't start
- Ensure Docker network `devnet` exists: `docker network create devnet`
- Check Docker Desktop is running
- Try rebuilding: `Dev Containers: Rebuild Container`

### Permission denied errors
- The container runs as `vscode` user with sudo privileges
- Use `sudo` for commands requiring root access

### GDB not working properly
- Verify `SYS_PTRACE` capability is enabled
- Check `seccomp` is set to unconfined
- Try running GDB with sudo: `sudo gdb ./program`

### 32-bit compilation fails
- Ensure `gcc-multilib` is installed (included in Dockerfile)
- Install 32-bit libraries if needed: `sudo apt-get install libc6-dev-i386`

### SSH connection refused
- Verify SSH service is running: `sudo service ssh status`
- Start SSH if needed: `sudo service ssh start`
- Check port forwarding: Port 2222 should map to container port 22

## 🤝 Contributing

Suggestions for additional tools or improvements are welcome! Consider adding:
- More static analysis tools
- Additional debuggers or disassemblers
- Fuzzing tools
- Binary instrumentation frameworks

## ⚖️ Legal & Ethical Notice

This environment is intended for **educational and research purposes only**. Always ensure you have proper authorization before analyzing or reverse engineering any software. Unauthorized reverse engineering may violate:

- Software licenses and terms of service
- Copyright laws
- Computer fraud and abuse laws
- Export control regulations

**Use responsibly and ethically.**

## 📄 License

This dev container configuration is available under the MIT License.

---

**Happy Reversing!** 🔍🔧