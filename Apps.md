# Apps

## Table of Contents
- [Apps](#apps)
  - [Table of Contents](#table-of-contents)
  - [Apps](#apps-1)
    - [Development](#development)
    - [Browsers](#browsers)
    - [Media \& Creative](#media--creative)
    - [Productivity](#productivity)
    - [System \& Utilities](#system--utilities)
    - [Communication](#communication)
    - [Gaming](#gaming)
    - [Other](#other)
  - [CLIs](#clis)
    - [Development \& Build Tools](#development--build-tools)
    - [Version Control \& Deployment](#version-control--deployment)
    - [Network \& System](#network--system)
    - [Text Processing \& Search](#text-processing--search)
    - [File Operations](#file-operations)
    - [Media](#media)
    - [Python](#python)
    - [Document Processing](#document-processing)
    - [Display Server](#display-server)
    - [Advanced CLI Tools](#advanced-cli-tools)



## Apps

### Development
- VS Code
- IntelliJ IDEA
- Git
- Github Desktop & CLI
- Docker Desktop
- Podman
- NodeJS
- Bun
- Python3
- Postman
- Terminal
- Copilot CLI
- MiKTeX

### Browsers
- Vivaldi
- Firefox
- DuckDuckGo
- Tor Browser

### Media & Creative
- Spotify
- OBS Studio
- Audacity
- MuseScore
- MuseHub
- Luminar Neo
- Inkscape
- VLC
- iThunes

### Productivity
- Obsidian
- Zotero
- Tropy
- TickTick
- PowerToys
- Oh My Posh
- Clink
- Rainmeter
- Everything

### System & Utilities
- TreeSize
- WinDirStat
- Explorer Patcher
- Winaero Tweaker
- Auto Dark Mode
- VcXsrv
- Tailscale
- VMware Workstation

### Communication
- WhatsApp
- iCloud
- Appareils Apple

### Gaming
- Epic Games Launcher
- Battle.net
- Steam

### Other
- Cisco Packet Tracer
- Sweet Home 3D
- LocalSend
- Jeex


&nbsp;  
&nbsp;  

## CLIs

### Development & Build Tools
- `gcc` / `g++` - GNU C/C++ compiler
- `cpp` - C preprocessor
- `cmake` - Cross-platform build system
- `mpicc` / `ompi` - MPI compiler wrappers
- `ocaml` - OCaml compiler
- `z3` - SMT solver

### Version Control & Deployment
- `git` - Version control system
- `docker` - Container platform
- `kubectl` - Kubernetes CLI

### Network & System
- `curl` - Transfer data with URLs
  ```bash
  curl https://api.example.com/data      # Fetch data from URL
  curl -X POST -H "Content-Type: application/json" -d '{"key":"value"}' URL  # POST request
  curl -o file.zip https://example.com/file.zip  # Download and save file
  ```
- `ping` - Test network connectivity
- `netstat` - Network statistics
  ```bash
  netstat -tuln                          # Show listening ports
  netstat -an | grep ESTABLISHED         # Show established connections
  netstat -r                             # Display routing table
  ```
- `ssh` - Secure shell client
  ```bash
  ssh user@hostname                      # Connect to remote server
  ssh -i ~/.ssh/key.pem user@host        # Connect with specific key
  ssh user@host "ls -la"                 # Execute remote command
  ```
- `tailscale` - VPN mesh network
  ```bash
  tailscale up                           # Connect to Tailscale network
  tailscale status                       # Show connection status
  tailscale ip -4                        # Show your Tailscale IPv4
  ```
- `openssl` - SSL/TLS toolkit

### Text Processing & Search
- `sed` - Stream editor
- `grep` - Pattern matching
- `vim` - Text editor
- `man` - Manual pages

### File Operations
- `unzip` - Extract ZIP archives
- `bzcmp` - Compare compressed files
  ```bash
  bzcmp file1.bz2 file2.bz2              # Compare two bzip2 files
  bzcmp file1.bz2 file2.txt              # Compare compressed with uncompressed
  bzcmp -s file1.bz2 file2.bz2           # Silent (exit code only)
  ```
- `cmp` - Compare files byte-by-byte
- `objdump` - Display object file info
  ```bash
  objdump -d binary                      # Disassemble executable
  objdump -h binary                      # Display section headers
  objdump -t binary                      # Display symbol table
  ```

### Media
- `ffmpeg` - Multimedia framework
  ```bash
  ffmpeg -i input.mp4 output.avi         # Convert video format
  ffmpeg -i video.mp4 -ss 00:00:10 -t 00:00:05 clip.mp4  # Extract 5s clip at 10s
  ffmpeg -i input.mp4 -vn -ar 44100 -ac 2 output.mp3  # Extract audio to MP3
  ```

### Python
- `python3` - Python interpreter
- `pip` - Python package manager

### Document Processing
- `prince` - HTML to PDF converter

### Display Server
- X11 / Wayland - Display server protocols


### Advanced CLI Tools
- `fzf` - fuzzy finder, for interactive filtering
  ```bash
  find . -type f | fzf                    # Fuzzy select files
  fzf --multi --preview 'head {}'         # Multi-select with preview
  git ls-files | fzf                      # Select from git-tracked files
  ```
- `fd` ou `fd-find` - Fast and user-friendly alternative to `find`
  ```bash
  fdfind report                           # Find files matching "report"
  fdfind --exact "notes.txt"                    # Exact filename match
  fdfind --query "pattern" -x grep -i "pattern" {} \;  # Search file contents
  fdfind -e md -t f                       # Find all markdown files
  fdfind -H -I pattern                    # Include hidden & ignored files
  ```
- `rg` - ripgrep, recursive search tool that respects .gitignore
  ```bash
  rg "pattern"                            # Search in current directory
  rg -i "pattern" -g "*.md"               # Case-insensitive in markdown files
  rg -l "pattern"                         # List filenames with matches
  ```

- `zoxide` - smart directory jumper that learns your habits. 
  Requires: `eval "$(zoxide init bash)"` in `.bashrc`.
  ```bash
  z project                               # Jump to most-used project directory
  zi                                      # Interactive directory selection
  zoxide query -l                         # List tracked directories
  ```
