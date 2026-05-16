# 🐧 Linux Learning Roadmap: Beginner to Advanced
### Industry-Focused · Practical · Implementable

> **How to use this roadmap:** Follow phases sequentially. Every concept must be practiced in a real terminal — reading alone is not enough. Spin up a VM or use a cloud instance and break things intentionally; that is how Linux is learned. Estimated durations assume 1–2 hours of focused daily practice.

---

## 📍 Phase 0 — Environment Setup & Orientation
**Duration:** 1–2 days | **Goal:** Have a working Linux environment and understand the landscape

### Choose Your Learning Environment

| Option | Best For | How |
|--------|----------|-----|
| **WSL 2 (Windows)** | Windows users, zero friction | Enable WSL2, install Ubuntu from Microsoft Store |
| **VirtualBox / VMware** | Full desktop experience, safe sandbox | Download Ubuntu 24.04 LTS ISO, create VM |
| **Cloud VM** | Realistic server environment | AWS EC2 / GCP Compute / DigitalOcean free tier |
| **Dual Boot** | Daily driver commitment | Ubuntu / Fedora installer alongside Windows |
| **Raspberry Pi** | Hands-on hardware | Raspberry Pi OS (Debian-based) |

> 💡 **Recommended:** Start with WSL2 or a VirtualBox VM running **Ubuntu 24.04 LTS**. Graduate to a real cloud VPS by Phase 3.

### Choose Your Distribution
Understanding the Linux family tree helps you navigate any distro:

```
Linux
├── Debian family
│   ├── Ubuntu (recommended for learning)
│   ├── Debian (servers, stability)
│   └── Linux Mint (desktop newcomers)
├── Red Hat family
│   ├── RHEL (enterprise standard)
│   ├── Fedora (cutting-edge RHEL upstream)
│   └── Rocky / AlmaLinux (RHEL-compatible, free)
├── Arch family
│   ├── Arch Linux (advanced, rolling release)
│   └── Manjaro (Arch with guardrails)
└── SUSE family
    ├── openSUSE Leap (stable)
    └── SUSE Linux Enterprise (enterprise)
```

### Core Orientation Concepts
- What is the Linux kernel? What is a distribution?
- Linux in industry: servers, cloud, embedded, Android, supercomputers
- Open-source philosophy and licensing (GPL, MIT, Apache)
- The Unix philosophy: small tools, composable, text as interface
- GUI vs CLI — why the terminal is the real power interface
- The root user vs regular users — why this distinction matters immediately

---

## 🟢 Phase 1 — Command Line Foundations
**Duration:** 4–5 weeks | **Goal:** Navigate, manipulate, and understand a Linux system from the terminal

### 1.1 The Shell & Terminal
- What is a shell? Bash vs Zsh vs sh vs fish
- Terminal emulators: GNOME Terminal, Alacritty, Kitty, tmux panes
- The prompt anatomy: `user@hostname:~$`
- Command structure: `command [options] [arguments]`
- `man` pages — the built-in manual (learn to read these fluently)
- `--help` flag and `info` pages
- Tab completion — use it constantly
- Command history: `history`, `!!`, `!n`, `Ctrl+R` reverse search
- Keyboard shortcuts: `Ctrl+C`, `Ctrl+D`, `Ctrl+Z`, `Ctrl+L`, `Ctrl+A`, `Ctrl+E`

### 1.2 Navigating the Filesystem
- The Linux filesystem hierarchy standard (FHS):

```
/               Root — the top of everything
├── bin/        Essential user binaries
├── sbin/       System administration binaries
├── etc/        Configuration files
├── home/       User home directories
├── root/       Root user's home
├── var/        Variable data (logs, databases, mail)
├── tmp/        Temporary files (cleared on reboot)
├── usr/        User programs and libraries
├── lib/        Shared libraries
├── dev/        Device files
├── proc/       Virtual filesystem: kernel and process info
├── sys/        Virtual filesystem: hardware info
├── mnt/        Mount points for temporary mounts
└── opt/        Optional third-party software
```

- `pwd` — print working directory
- `ls` — list directory contents (`-l`, `-a`, `-h`, `-R`, `-t` flags)
- `cd` — change directory (`.`, `..`, `~`, `-`, absolute vs relative paths)
- `tree` — visual directory structure
- `find` — search for files and directories with conditions

### 1.3 Working with Files & Directories
- `touch` — create empty files / update timestamps
- `mkdir` — create directories (`-p` for nested)
- `cp` — copy files and directories (`-r`, `-v`, `-p`)
- `mv` — move and rename files
- `rm` — remove files (`-r`, `-f`) — understand the danger
- `ln` — hard links and symbolic links (`-s`)
- `file` — determine file type
- `stat` — detailed file metadata

### 1.4 Viewing & Editing File Contents
- `cat` — print file contents
- `less` / `more` — paginate through files (use `less` always)
- `head` / `tail` — first and last N lines; `tail -f` for live log following
- `wc` — word, line, character counts
- **Text editors:**
  - `nano` — beginner-friendly
  - `vim` — industry standard; learn the basics (modes, `:wq`, `:q!`, navigation)
  - `neovim` — modern vim
  - `emacs` — powerful alternative

### 1.5 The Power of the Shell: Pipes & Redirection
- Standard streams: stdin (0), stdout (1), stderr (2)
- Output redirection: `>` (overwrite), `>>` (append)
- Input redirection: `<`
- Stderr redirect: `2>`, `2>&1`
- Pipes: `|` — connect command output to command input
- `/dev/null` — discard output
- `tee` — write to stdout and file simultaneously
- Command substitution: `$(command)` and backticks

### 1.6 Essential Text Processing Tools
This is the heart of the Unix philosophy — small tools, chained together.

| Tool | Purpose | Key Options |
|------|---------|-------------|
| `grep` | Search text patterns | `-i`, `-r`, `-n`, `-v`, `-E`, `-l` |
| `sed` | Stream editor, find/replace | `s/old/new/g`, `-i` for in-place |
| `awk` | Pattern scanning and data extraction | `{print $1}`, field separators |
| `cut` | Cut fields from lines | `-d`, `-f` |
| `sort` | Sort lines | `-n`, `-r`, `-k`, `-u` |
| `uniq` | Remove/count duplicates | `-c`, `-d` |
| `tr` | Translate/delete characters | `tr 'a-z' 'A-Z'` |
| `xargs` | Build commands from stdin | `-I{}`, `-n`, `-P` |
| `diff` | Compare files | `-u` unified format |

### 1.7 File Permissions & Ownership
- Permission model: owner, group, others
- Permission types: read (r/4), write (w/2), execute (x/1)
- Reading `ls -l` output: `-rwxr-xr--`
- `chmod` — change permissions (numeric and symbolic modes)
- `chown` — change file owner and group
- `chgrp` — change group ownership
- Special bits: setuid, setgid, sticky bit
- `umask` — default permission mask

### 1.8 Package Management
**Debian/Ubuntu (apt):**
```bash
apt update && apt upgrade
apt install <package>
apt remove / apt purge
apt search <term>
apt show <package>
dpkg -l  # list installed packages
```

**Red Hat/Fedora (dnf/yum):**
```bash
dnf update
dnf install <package>
dnf remove <package>
dnf search <term>
rpm -qa  # list installed packages
```

**Universal package managers:**
- `snap` — containerized apps (Ubuntu-native)
- `flatpak` — distribution-agnostic
- `brew` (Linuxbrew) — developer tools
- Compiling from source: `./configure && make && make install`

### 📝 Exercises (Phase 1)
1. **Navigation Drill** — using only the terminal, navigate to `/etc`, list all `.conf` files, count how many there are, and display the first 20 lines of `/etc/os-release`
2. **Pipeline Challenge** — find the 10 most common words in `/var/log/syslog` (or any log file) using a pipeline of `grep`, `tr`, `sort`, `uniq`, and `head`
3. **Permissions Puzzle** — create a script file, set it executable for owner only, verify with `ls -l`, then make a symlink to it from `/tmp`
4. **sed/awk Practice** — given a CSV file, use `awk` to print only the 2nd and 4th columns, then use `sed` to replace all occurrences of a string in-place
5. **Log Analysis** — parse `/var/log/auth.log` to count failed SSH login attempts per IP address using a shell pipeline

### 🔨 Mini-Project 1: System Inventory Script
Write a Bash script that generates a complete system inventory report saved to a timestamped file:
- Hostname, OS version, kernel version
- CPU model and core count
- Total / used / free RAM and disk space
- List of all logged-in users
- Top 10 processes by CPU usage
- Network interfaces and their IP addresses
- Last 20 lines of the system log
- Output formatted clearly with section headers

---

## 🟡 Phase 2 — Shell Scripting & Automation
**Duration:** 5–6 weeks | **Goal:** Automate repetitive tasks and write production-quality shell scripts

### 2.1 Bash Scripting Fundamentals
- Shebang line: `#!/usr/bin/env bash`
- Script permissions and execution: `chmod +x script.sh`
- Variables: assignment, quoting rules, `${var}` syntax
- Environment variables: `export`, `env`, `printenv`
- Special variables: `$0`, `$1`–`$9`, `$#`, `$@`, `$*`, `$?`, `$$`, `$!`
- Single quotes vs double quotes vs no quotes — critical distinctions
- Command substitution: `$(...)` 
- Arithmetic: `$(( ))`, `let`, `bc` for floating point
- `read` — interactive user input
- `echo` vs `printf` — when each is appropriate

### 2.2 Control Flow
- `if` / `elif` / `else` / `fi`
- Test expressions: `[ ]` vs `[[ ]]` (prefer `[[ ]]` in bash)
- File tests: `-f`, `-d`, `-e`, `-r`, `-w`, `-x`, `-s`, `-z`
- String tests: `=`, `!=`, `-z`, `-n`
- Numeric tests: `-eq`, `-ne`, `-lt`, `-gt`, `-le`, `-ge`
- `case` statements — cleaner than long if/elif chains
- `for` loops: list iteration and C-style
- `while` and `until` loops
- `break` and `continue`
- `select` — simple interactive menus

### 2.3 Functions
- Defining and calling functions
- Local variables with `local`
- Return values and exit codes
- Passing arguments to functions
- Sourcing files: `. file.sh` / `source file.sh`

### 2.4 Error Handling & Robustness
- Exit codes: `0` = success, non-zero = failure
- `set -e` — exit on error
- `set -u` — exit on undefined variable
- `set -o pipefail` — catch pipe failures
- `set -x` — debug mode (trace execution)
- `trap` — handle signals and cleanup on exit
  - `trap 'cleanup' EXIT`
  - `trap 'echo Interrupted' INT TERM`
- Defensive scripting patterns
- Logging in scripts: timestamps, log levels, log files

### 2.5 String & Array Operations
- String slicing: `${var:offset:length}`
- String replacement: `${var/old/new}`, `${var//old/new}`
- String trimming: `${var#prefix}`, `${var%suffix}`
- Case conversion: `${var^^}`, `${var,,}`
- Arrays: declaration, indexing, iteration, `${array[@]}`
- Associative arrays (dictionaries): `declare -A`
- `mapfile` / `readarray` — read lines into arrays

### 2.6 Advanced Shell Features
- Here documents: `<<EOF ... EOF`
- Here strings: `<<< "string"`
- Process substitution: `<(command)`, `>(command)`
- Brace expansion: `{a,b,c}`, `{1..10}`, `{01..12}`
- Glob patterns: `*`, `?`, `[...]`, `**` (globstar)
- Regular expressions in `[[ =~ ]]`
- `getopts` — parsing command-line options in scripts

### 2.7 Scheduling & Automation
- `cron` — time-based job scheduler
  - Crontab syntax: `minute hour day month weekday command`
  - `crontab -e`, `crontab -l`, `crontab -r`
  - `/etc/cron.d/`, `/etc/cron.daily/` system cron directories
- `systemd timers` — modern alternative to cron (more reliable, better logging)
- `at` — one-time scheduled jobs
- `watch` — run a command repeatedly and display output

### 📝 Exercises (Phase 2)
1. **Robust Backup Script** — write a script that backs up a directory to a tar.gz archive with a timestamp, keeps only the last 7 backups, and logs success/failure
2. **User Input Validator** — script that prompts for an email address and validates its format using regex, retrying until valid
3. **Batch File Renamer** — rename all `.jpg` files in a directory to a numbered format (`photo_001.jpg`, `photo_002.jpg`...) with a dry-run option (`--dry-run`)
4. **Service Monitor** — check if a list of services are running; restart any that are stopped; log and email-notify on each restart (simulate email with `echo` to a file)
5. **Cron Log Cleaner** — schedule a cron job to delete log files older than 30 days from a directory, running daily at 2 AM

### 🔨 Mini-Project 2: Automated Server Setup Script
Write a fully automated server provisioning script for a fresh Ubuntu server:
- Accept arguments: `--hostname`, `--user`, `--packages`
- Update system packages
- Create a new sudo user with SSH key authentication
- Disable root SSH login and password authentication
- Configure `ufw` firewall (allow SSH, HTTP, HTTPS only)
- Install specified packages
- Set up `fail2ban` for brute-force protection
- Configure automatic security updates (`unattended-upgrades`)
- Set timezone, hostname, and locale
- Output a setup summary log with all actions taken
- Full error handling with `set -euo pipefail` and `trap` cleanup

---

## 🟠 Phase 3 — System Administration
**Duration:** 5–6 weeks | **Goal:** Administer, monitor, and troubleshoot Linux systems like a professional

### 3.1 Process Management
- What is a process? PID, PPID, process states
- `ps` — process status (`ps aux`, `ps -ef`)
- `top` / `htop` — interactive process monitors
- `pgrep` / `pkill` — find and signal processes by name
- `kill` — send signals to processes
  - `SIGTERM` (15) — graceful termination
  - `SIGKILL` (9) — force kill (no cleanup)
  - `SIGHUP` (1) — reload configuration
  - `SIGSTOP` / `SIGCONT` — pause and resume
- Background jobs: `&`, `jobs`, `fg`, `bg`, `nohup`, `disown`
- `nice` / `renice` — process priority (niceness -20 to 19)
- `strace` — trace system calls (debugging tool)
- `lsof` — list open files and sockets

### 3.2 systemd & Service Management
- What is init? From SysV init to systemd
- Units: service, socket, timer, target, mount
- `systemctl` commands:
  ```bash
  systemctl start|stop|restart|reload <service>
  systemctl enable|disable <service>    # boot persistence
  systemctl status <service>
  systemctl list-units --type=service
  systemctl daemon-reload               # after unit file changes
  ```
- `journalctl` — reading systemd logs:
  ```bash
  journalctl -u <service>               # logs for one service
  journalctl -f                         # follow live logs
  journalctl --since "1 hour ago"
  journalctl -p err                     # only errors and above
  ```
- Writing a custom systemd unit file
- Targets (runlevels): `multi-user.target`, `graphical.target`, `rescue.target`
- Boot process: BIOS/UEFI → bootloader (GRUB) → kernel → initramfs → systemd → target

### 3.3 User & Group Management
- `/etc/passwd`, `/etc/shadow`, `/etc/group` — understanding these files
- `useradd` / `adduser` — create users
- `usermod` — modify user properties
- `userdel` — delete users
- `groupadd`, `groupmod`, `groupdel`
- `passwd` — change passwords
- `su` — switch user
- `sudo` — execute as another user (usually root)
- `/etc/sudoers` and `visudo` — configuring sudo safely
- `who`, `w`, `last`, `lastlog` — login tracking
- PAM (Pluggable Authentication Modules) — overview

### 3.4 Storage & Filesystem Management
- Block devices: `/dev/sda`, `/dev/nvme0n1`, `/dev/vda`
- `lsblk` — list block devices
- `fdisk` / `parted` / `gdisk` — partition management
- Filesystem types: ext4, xfs, btrfs, zfs, tmpfs, FAT32
- `mkfs` — format partitions
- `mount` / `umount` — attach and detach filesystems
- `/etc/fstab` — persistent mount configuration
- `df` — disk space usage (`-h` for human-readable)
- `du` — directory disk usage (`-sh`, `--max-depth`)
- LVM (Logical Volume Manager):
  - Physical volumes (PV), volume groups (VG), logical volumes (LV)
  - `pvcreate`, `vgcreate`, `lvcreate`, `lvextend`, `resize2fs`
- Swap space: swap partition vs swap file
- `ncdu` — interactive disk usage explorer

### 3.5 Networking Fundamentals
- Network interfaces: `ip addr`, `ip link`, `ip route`
- `ifconfig` (legacy) vs `ip` (modern)
- DNS: `/etc/resolv.conf`, `/etc/hosts`, `dig`, `nslookup`, `host`
- `ping`, `traceroute` / `tracepath`, `mtr`
- `ss` / `netstat` — socket and connection statistics
- `curl` and `wget` — HTTP from the command line
- `nc` (netcat) — network debugging Swiss army knife
- Network configuration: Netplan (Ubuntu), NetworkManager, `/etc/network/interfaces`
- `hostname` and `/etc/hostname`
- Firewall with `ufw` (Uncomplicated Firewall):
  ```bash
  ufw enable / disable / status
  ufw allow 22/tcp
  ufw allow from 10.0.0.0/8
  ufw deny 80
  ufw delete allow 80
  ```
- `iptables` / `nftables` — low-level firewall rules (conceptual understanding)

### 3.6 Logging & Monitoring
- Log locations: `/var/log/syslog`, `/var/log/auth.log`, `/var/log/kern.log`, `/var/log/nginx/`
- `rsyslog` and `syslog-ng` — system logging daemons
- Log rotation: `logrotate` configuration
- `journalctl` for systemd logs (covered in 3.2)
- System monitoring tools:
  - `vmstat` — virtual memory statistics
  - `iostat` — I/O statistics (from `sysstat`)
  - `sar` — system activity reporter
  - `free` — memory usage
  - `uptime` and load averages explained
  - `dmesg` — kernel ring buffer (hardware/boot messages)
- `/proc` filesystem deep dive: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/loadavg`, `/proc/net/`

### 3.7 SSH — Secure Shell Mastery
- `ssh` client: connecting, options, verbosity (`-v`, `-vvv`)
- SSH key pairs: `ssh-keygen` (Ed25519 recommended)
- `ssh-copy-id` — deploying public keys
- `~/.ssh/config` — managing multiple hosts and identities
- SSH agent: `ssh-agent`, `ssh-add`
- `scp` and `rsync` — secure file transfer
  - `rsync -avz --progress source/ dest/` — efficient incremental sync
- SSH tunneling:
  - Local port forwarding: `ssh -L local:remote`
  - Remote port forwarding: `ssh -R`
  - Dynamic (SOCKS proxy): `ssh -D`
- Hardening `sshd_config`:
  - Disable root login
  - Disable password authentication
  - Change default port
  - `AllowUsers` restriction
  - `MaxAuthTries`, `ClientAliveInterval`

### 📝 Exercises (Phase 3)
1. **Process Investigation** — find the top 5 memory-consuming processes, then use `strace` on a simple command and interpret the output
2. **Custom Service** — write a systemd unit file for a simple Python HTTP server, enable it at boot, verify it restarts on failure
3. **Storage Lab** — create a new partition on a disk image (using a loopback device), format it as ext4, mount it persistently via `/etc/fstab`
4. **Network Diagnosis** — diagnose why a web service is unreachable: check the process, port binding, firewall rules, and DNS resolution step by step
5. **Log Analysis Pipeline** — write a script that parses Nginx access logs, extracts the top 10 IPs by request count, and auto-blocks them with `ufw`

### 🔨 Mini-Project 3: Linux Server Health Monitor
Build a comprehensive server monitoring tool that runs as a systemd service:
- Collects CPU, memory, disk, and network metrics every 60 seconds
- Appends metrics to a structured log file (CSV or JSON)
- Triggers alerts (logged to a separate file) when:
  - CPU > 80% for 5 consecutive readings
  - Memory > 90%
  - Disk > 85%
  - A critical service is not running
- Generates a daily HTML summary report
- Runs as a non-privileged user via a systemd unit with `Restart=always`
- Includes a companion script to view current status and recent alerts

---

## 🔴 Phase 4 — Networking, Security & Hardening
**Duration:** 4–5 weeks | **Goal:** Secure and harden Linux systems; understand networking at depth

### 4.1 Networking Deep Dive
- TCP/IP model layers and how they map to Linux tools
- IP addressing: IPv4, IPv6, CIDR notation, subnetting
- Routing: `ip route`, static routes, default gateway
- Network namespaces — the foundation of containers
- Bridges and virtual interfaces: `veth`, `bridge`, `tun/tap`
- `tcpdump` — capture and analyze network traffic:
  ```bash
  tcpdump -i eth0 port 80
  tcpdump -w capture.pcap
  tcpdump -r capture.pcap
  ```
- `Wireshark` — GUI packet analysis
- `nmap` — network discovery and port scanning
- `iperf3` — network bandwidth testing
- DNS deep dive: authoritative vs recursive resolvers, `dig +trace`

### 4.2 iptables & nftables
- Netfilter framework — how Linux firewall hooks work
- `iptables` chains: INPUT, OUTPUT, FORWARD
- Tables: filter, nat, mangle, raw
- Common rules: allow established connections, rate limiting, DNAT/SNAT
- `iptables-save` / `iptables-restore` — persisting rules
- `nftables` — the modern replacement: syntax and concepts
- Migrating from iptables to nftables

### 4.3 Linux Security Fundamentals
- Principle of least privilege — applied throughout
- `sudo` hardening: specific command allowlists in sudoers
- File integrity monitoring: `AIDE`, `tripwire`
- **SELinux** (Red Hat family):
  - Enforcing vs Permissive vs Disabled modes
  - Contexts, types, booleans
  - `getenforce`, `setenforce`, `audit2allow`
- **AppArmor** (Ubuntu/Debian):
  - Profiles and modes (enforce vs complain)
  - `aa-status`, `aa-enforce`, `aa-complain`
- `chroot` jails — isolating processes
- Capabilities (`capabilities(7)`) — fine-grained root powers
- `seccomp` — system call filtering
- `/proc/sys/kernel/` security settings: `dmesg_restrict`, `kptr_restrict`

### 4.4 SSH Hardening & Key Management
- Certificate-based SSH authentication (SSH CA)
- `HashKnownHosts`, `StrictHostKeyChecking`
- Two-factor authentication with Google Authenticator PAM
- `fail2ban` — automatic IP banning on repeated failures:
  - Jail configuration
  - Writing custom filters
  - `fail2ban-client status`
- Port knocking — security through obscurity layer
- Bastion hosts / jump hosts: `ssh -J jumphost destination`

### 4.5 System Hardening Checklist
- `lynis` — automated security auditing tool
- Remove unnecessary packages and services
- Kernel hardening via `sysctl.conf`:
  ```
  net.ipv4.tcp_syncookies = 1
  net.ipv4.conf.all.rp_filter = 1
  kernel.randomize_va_space = 2
  ```
- `auditd` — kernel audit framework for compliance
- CIS Benchmarks — industry-standard hardening guides
- `/etc/login.defs` — password policy settings
- `pam_pwquality` — password complexity enforcement
- Time synchronization with `chrony` / `ntpd`

### 4.6 Cryptography in Practice
- `openssl` command-line Swiss army knife:
  - Generating keys and CSRs
  - Self-signed certificates
  - Inspecting certificates: `openssl x509 -text`
  - Encrypting/decrypting files
- TLS/SSL concepts: certificates, chains of trust, CA
- Let's Encrypt and `certbot` — free TLS certificates
- GPG: `gpg --gen-key`, signing, encrypting, key management
- `age` — modern file encryption tool

### 📝 Exercises (Phase 4)
1. **tcpdump Lab** — capture HTTP traffic to a local server, identify the TCP handshake, request, and response in the pcap
2. **Firewall Ruleset** — write a complete `nftables` ruleset for a web server: allow SSH, HTTP, HTTPS; rate-limit SSH; drop everything else; persist across reboots
3. **Lynis Audit** — run `lynis audit system` on your lab VM, interpret the output, and fix the top 10 findings
4. **fail2ban Custom Jail** — write a custom fail2ban jail and filter for an application log format of your choice
5. **TLS Everything** — set up a local Nginx server with a self-signed certificate; then replace with a Let's Encrypt cert using `certbot` (use a real domain or DNS challenge)

### 🔨 Mini-Project 4: Hardened Bastion Host
Build and document a production-hardened bastion (jump) host from a fresh Ubuntu server:
- Automated setup via a hardening script
- SSH certificate authority: sign host and user keys
- `fail2ban` with custom jails for SSH and application logs
- Complete `nftables` firewall: only SSH in, all outbound allowed
- `auditd` configured to log all privilege escalations and file changes
- `lynis` score > 70 (document before/after)
- CIS Benchmark compliance for applicable controls
- All configuration managed as code (scripts + config files in a git repo)
- Runbook document: how to connect, rotate keys, add users, respond to alerts

---

## 🔵 Phase 5 — Advanced Topics
**Duration:** 6–8 weeks | **Goal:** Master internals, performance, and modern infrastructure tooling

### 5.1 Linux Kernel & Internals
- Kernel space vs user space
- System calls — the interface between them
- `/proc` and `/sys` — virtual filesystems as kernel APIs
- Kernel modules: `lsmod`, `modprobe`, `rmmod`, `modinfo`
- Writing a minimal kernel module (Hello World)
- Kernel compilation (overview — understand the process, not memorization)
- Control groups (cgroups v2) — resource limiting for processes
  - `systemd-cgls`, `systemd-cgtop`
  - CPU, memory, I/O limits
- Namespaces: pid, net, mnt, uts, ipc, user — the building blocks of containers
- eBPF — extended Berkeley Packet Filter (revolutionary observability tool):
  - `bpftool`, `bcc` tools: `execsnoop`, `opensnoop`, `tcptracer`
  - Overview of `bpftrace`

### 5.2 Performance Analysis & Tuning
- The USE Method (Utilization, Saturation, Errors) — Brendan Gregg's framework
- CPU performance:
  - `perf` — Linux performance analysis tool
  - `perf stat`, `perf record`, `perf report`
  - Flame graphs — visualizing CPU profiling
  - CPU affinity: `taskset`
  - NUMA awareness: `numactl`
- Memory performance:
  - `vmstat -sm`, `/proc/meminfo` deep read
  - Huge pages and transparent huge pages (THP)
  - OOM killer: `/proc/sys/vm/oom_score_adj`
  - `slab` cache: `slabtop`
- I/O performance:
  - `iostat -x 1`, `iotop`
  - `fio` — I/O benchmarking tool
  - I/O schedulers: mq-deadline, bfq, none
  - `blktrace` — block layer tracing
- Network performance:
  - `ethtool` — NIC tuning
  - TCP buffer tuning via `sysctl`
  - `ss -tin` — TCP socket internals
  - `nstat` — network statistics

### 5.3 Containers & Linux
- Docker as a Linux namespace + cgroup + overlay filesystem
- Building container images: Dockerfile best practices for Linux
- `podman` — daemonless, rootless containers
- `buildah` — container image building
- Linux container internals hands-on:
  ```bash
  # Create an isolated process manually:
  unshare --pid --fork --mount-proc /bin/bash
  ```
- `crun` / `runc` — OCI container runtimes
- Overlay filesystems: `overlayfs` in practice

### 5.4 Infrastructure as Code with Linux
- **Ansible** — agentless configuration management:
  - Inventory files
  - Playbooks, roles, handlers
  - Modules: `apt`, `service`, `copy`, `template`, `user`, `cron`
  - `ansible-vault` for secrets
  - Idempotency — the core principle
- **Terraform** fundamentals (Linux as the target):
  - Providers, resources, state
  - Provisioning Linux VMs on AWS/GCP/Azure
- Git for infrastructure: `gitops` principles
- **Packer** — building machine images programmatically

### 5.5 Observability Stack
- **Prometheus** + **Grafana** — the industry-standard metrics stack
  - `node_exporter` — Linux system metrics
  - Writing PromQL queries
  - Building dashboards
  - AlertManager — routing and notification
- **Loki** — log aggregation (Grafana's log solution)
- **OpenTelemetry** — unified observability standard
- **Netdata** — lightweight real-time monitoring
- Structured logging: why JSON logs beat plain text at scale

### 5.6 Advanced Storage
- ZFS on Linux: pools, datasets, snapshots, send/receive
- Btrfs: subvolumes, snapshots, RAID modes
- RAID: software RAID with `mdadm` (RAID 0, 1, 5, 6, 10)
- iSCSI and NFS — network storage
- `dm-crypt` / LUKS — full disk encryption
- `cryptsetup` — encrypted volume management
- Storage performance: SSD vs HDD tuning, `noatime`, `deadline` scheduler

---

## 🟣 Phase 6 — Specialized Tracks
**Duration:** 6–8 weeks | **Choose based on your target role**

---

### ☁️ Track A: Cloud & DevOps Engineering

#### Topics
- **Linux in the cloud:** EC2/GCP Compute/Azure VM lifecycle management
- **Cloud-init** — automated cloud instance initialization
- Immutable infrastructure: build images, never patch running servers
- **Kubernetes on Linux:**
  - Node OS requirements and hardening
  - `kubelet`, container runtime (`containerd`), CNI plugins
  - `kubeadm` cluster setup from scratch
  - Linux kernel tuning for Kubernetes nodes
- **CI/CD pipelines with Linux:**
  - GitHub Actions with Linux runners
  - GitLab CI self-hosted runners
  - Jenkins on Linux
- **Load balancing and reverse proxy:**
  - Nginx as reverse proxy and load balancer
  - HAProxy configuration
  - Keepalived for HA failover
- **Service mesh concepts:** Envoy, Istio (Linux networking implications)
- Cost optimization: rightsizing, spot instances, auto-scaling

#### 🔨 Capstone A: Production Kubernetes Cluster on Bare Linux
Deploy a fully production-grade Kubernetes cluster from scratch:
- 3-node cluster (1 control plane, 2 workers) on cloud VMs
- OS hardened per CIS Benchmark before joining the cluster
- `containerd` as the container runtime
- Calico CNI for network policy enforcement
- Nginx Ingress Controller with TLS termination (Let's Encrypt)
- Prometheus + Grafana monitoring with Linux node dashboards
- Persistent storage with local-path or NFS provisioner
- Automated cluster setup via Ansible playbooks
- Disaster recovery: etcd backup and restore procedure documented and tested

---

### 🔐 Track B: Security & Penetration Testing

#### Topics
- **Security-focused distros:** Kali Linux, Parrot OS, BlackArch
- **Reconnaissance:** `nmap` advanced scanning, `masscan`, OSINT tools
- **Vulnerability assessment:** `OpenVAS`, `Nessus` (concepts), CVE databases
- **Exploitation fundamentals (ethical/lab only):**
  - Buffer overflows on Linux (32-bit, basics)
  - `Metasploit Framework` on Linux
  - SUID/SGID binary abuse for privilege escalation
  - Cron job exploitation
  - PATH hijacking
  - Writable `/etc/passwd`
- **Post-exploitation:** maintaining access, pivoting via SSH tunnels
- **Linux forensics:**
  - Memory acquisition and analysis (`LiME`, `Volatility`)
  - Disk forensics: `The Sleuth Kit`, `Autopsy`
  - Log analysis for incident response
  - Rootkit detection: `rkhunter`, `chkrootkit`
- **CTF (Capture The Flag):** HackTheBox, TryHackMe Linux rooms
- **Defensive security:** SIEM integration, `auditd` → SIEM pipelines

#### 🔨 Capstone B: Home Lab Security Assessment
Build a home lab and conduct a full security assessment:
- Deploy a deliberately vulnerable Linux VM (Metasploitable, VulnHub)
- Conduct full reconnaissance with `nmap` and enumerate services
- Exploit at least 3 vulnerabilities (in the lab VM only)
- Escalate privileges using at least 2 different techniques
- Pivot to a second VM through the compromised host
- Write a professional penetration test report (executive summary, findings, CVSS scores, remediation recommendations)
- Harden the target based on your own findings and re-test

---

### 📊 Track C: Data Engineering & HPC

#### Topics
- **Linux for data pipelines:**
  - High-throughput file processing: `parallel`, `xargs -P`
  - `awk` and `datamash` for data transformation at scale
  - `sqlite3` from the command line
  - Named pipes (`mkfifo`) for streaming data between processes
- **Storage optimization for data:**
  - NFS and distributed filesystems (GlusterFS, CephFS concepts)
  - Compression: `gzip`, `bzip2`, `zstd`, `lz4` — tradeoffs
  - Columnar formats and Linux I/O patterns
- **HPC fundamentals:**
  - SLURM job scheduler: submitting, monitoring, and cancelling jobs
  - MPI (Message Passing Interface) basics on Linux
  - CPU affinity and NUMA for HPC workloads
  - GPU computing: CUDA, driver management, `nvidia-smi`
- **Workflow orchestration on Linux:**
  - Apache Airflow deployment on Linux
  - Luigi, Prefect — running on Linux servers
- **Containerized data workloads:** Spark on Docker/Kubernetes

#### 🔨 Capstone C: Parallel Data Processing Pipeline
Build a high-throughput data processing pipeline on Linux:
- Ingest large dataset (10GB+) via HTTP using `curl` with resume support
- Parallel preprocessing using `GNU parallel` across all CPU cores
- Stream processing with named pipes: decompress → parse → transform → load without temp files
- Data validation with custom `awk` scripts
- Results loaded into PostgreSQL via `COPY` for maximum throughput
- Systemd service with resource limits (cgroup): max 4 CPUs, 8GB RAM
- Benchmarked and profiled with `perf` and `iostat`
- Full observability: Prometheus metrics exposed, Grafana dashboard

---

## 📚 Curated Resources

### Essential Books
| Title | Level | Focus |
|-------|-------|-------|
| *The Linux Command Line* — William Shotts | Beginner | CLI foundations (free online) |
| *Linux Pocket Guide* — Daniel Barrett | Beginner | Quick reference |
| *How Linux Works* — Brian Ward | Intermediate | Internals and concepts |
| *The Linux Bible* — Christopher Negus | Intermediate | Comprehensive reference |
| *Linux System Programming* — Robert Love | Advanced | Kernel interfaces, syscalls |
| *Systems Performance* — Brendan Gregg | Advanced | Performance analysis |
| *Linux Observability with BPF* — Calavera & Fontana | Advanced | eBPF and modern observability |

### Online Platforms & Labs
- **OverTheWire: Bandit** — gamified CLI learning from zero (wargames.overthewire.org)
- **TryHackMe** — guided Linux rooms for security track
- **HackTheBox** — Linux machines for advanced security practice
- **Linux Journey** (linuxjourney.com) — structured beginner curriculum
- **Explain Shell** (explainshell.com) — paste any command, get explanations
- **TLDR Pages** (tldr.sh) — simplified man pages for quick reference
- **Brendan Gregg's Blog** (brendangregg.com) — the definitive performance resource
- **Arch Wiki** — the best Linux documentation on the internet (applies beyond Arch)

### Practice Environments
- **Killercoda** — free browser-based Linux labs
- **Play with Docker** — free Docker/Linux playground
- **Google Cloud Shell** — free cloud Linux terminal
- **LFS (Linux From Scratch)** — build Linux from source (advanced validation)

---

## 🗓️ Recommended Study Schedule

| Phase | Commitment | Timeline |
|-------|-----------|----------|
| Phase 0: Setup | 1–2 hrs/day | Week 1 |
| Phase 1: CLI Foundations | 1–2 hrs/day | Weeks 2–6 |
| Phase 2: Shell Scripting | 1.5–2 hrs/day | Weeks 7–12 |
| Phase 3: System Administration | 1.5–2 hrs/day | Weeks 13–18 |
| Phase 4: Networking & Security | 1.5–2 hrs/day | Weeks 19–23 |
| Phase 5: Advanced Topics | 2 hrs/day | Weeks 24–31 |
| Phase 6: Specialization Track | 2 hrs/day | Weeks 32–40 |

> 💡 **Tip:** Set up a dedicated lab environment early and *break it intentionally*. Recovering from mistakes — a corrupted fstab, a misconfigured firewall that locks you out, a runaway process — teaches more than any tutorial.

---

## 🧠 Linux Golden Rules (Internalize These)

1. **Read the man page first** — `man <command>` before Googling
2. **Never run untrusted scripts as root** — audit before executing
3. **Test destructive commands with `--dry-run` or `echo` first** — `rm -rf` has no undo
4. **Always have a console/out-of-band access before locking down SSH** — don't lock yourself out
5. **Use `set -euo pipefail` in every script** — fail loudly and early
6. **Keep a working backup before changing `/etc/fstab`** — a wrong entry prevents boot
7. **Prefer `ip` over `ifconfig`, `ss` over `netstat`** — use the modern tools
8. **`sudo !!`** — rerun last command with sudo (saves retyping long commands)
9. **Understand before you copy-paste** — every line of a script you run should make sense to you
10. **The Arch Wiki applies everywhere** — it's the best Linux documentation regardless of your distro

---

## ✅ Progress Tracker

- [ ] Phase 0 complete — Linux environment running, first command executed
- [ ] Phase 1 complete — System Inventory Script done
- [ ] Phase 2 complete — Automated Server Setup Script done
- [ ] Phase 3 complete — Server Health Monitor done
- [ ] Phase 4 complete — Hardened Bastion Host done
- [ ] Phase 5 complete — Advanced topics covered
- [ ] Phase 6 Track chosen: ___________
- [ ] Phase 6 Capstone complete — production-grade project shipped

---

*Roadmap version 1.0 · Ubuntu 24.04 LTS primary · Updated May 2026*