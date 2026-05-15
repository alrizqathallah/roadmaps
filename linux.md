# 🐧 Linux, Bash Scripting & Networking Roadmap: Beginner to Advanced

> A comprehensive, structured, and practical guide to mastering Linux system administration, Bash scripting, and computer networking — with exercises, mini-projects, and large capstone projects at every stage.

---

## How to Use This Roadmap

- Follow stages **in order** — each builds directly on the last.
- Type every command yourself — never copy-paste during practice.
- Break things **intentionally** in a safe lab environment, then fix them.
- Keep a **personal command journal** — document every new command with an example.
- Commit all scripts and configs to **GitHub** from day one.

---

## 🛠️ Lab Environment Setup

A safe, resettable environment is essential. Use one or more of the following:

### Option 1 — Virtual Machines (Recommended for Beginners)
```bash
# Install VirtualBox (free) or VMware Workstation Player
# Download Ubuntu Server 24.04 LTS ISO from ubuntu.com/download/server
# Create a VM: 2 vCPUs, 2GB RAM, 20GB disk
# Create 2–3 VMs for networking labs
```

### Option 2 — WSL2 (Windows Users)
```powershell
wsl --install                        # Installs Ubuntu by default
wsl --install -d Ubuntu-24.04
wsl --list --verbose                 # List installed distros
```

### Option 3 — Multipass (Lightweight VMs)
```bash
brew install multipass               # macOS
multipass launch --name dev-lab --cpus 2 --memory 2G --disk 20G
multipass shell dev-lab
multipass delete dev-lab && multipass purge
```

### Option 4 — Cloud Labs (Zero local setup)
- **AWS Free Tier** — EC2 t2.micro instances
- **Google Cloud** — e2-micro (always free tier)
- **DigitalOcean** — $4/month droplets
- **KillerCoda** (killercoda.com) — Free browser-based Linux scenarios
- **Linux Journey** (linuxjourney.com) — Interactive browser exercises

### Essential First Commands After Setup
```bash
uname -a                             # Kernel and system info
lsb_release -a                       # Distro info
whoami                               # Current user
pwd                                  # Present working directory
ls -la                               # List files with details
df -h                                # Disk usage
free -h                              # Memory usage
uptime                               # System uptime and load
```

---

## Stage 1 — Linux Fundamentals (Weeks 1–3)

**Goal:** Navigate a Linux system confidently from the command line.

### The Shell & Terminal
- What is a shell? Bash vs. Zsh vs. Fish vs. sh
- Terminal emulators: `gnome-terminal`, `alacritty`, `iTerm2`
- Shell prompts: `$` (user) vs. `#` (root)
- Command structure: `command [options] [arguments]`
- `man` pages and `--help` flags
- `apropos` — search man pages by keyword
- `type`, `which`, `whereis` — find command locations
- Shell history: `history`, `!!`, `!n`, `Ctrl+R` (reverse search)
- Tab completion and keyboard shortcuts (`Ctrl+C`, `Ctrl+Z`, `Ctrl+D`, `Ctrl+L`)

### File System Navigation
```bash
# Linux Filesystem Hierarchy Standard (FHS)
/           # Root of the filesystem
/bin        # Essential user binaries
/sbin       # System administration binaries
/etc        # Configuration files
/home       # User home directories
/var        # Variable data (logs, spool, cache)
/tmp        # Temporary files (cleared on reboot)
/opt        # Optional/third-party software
/proc       # Virtual filesystem: kernel and process info
/sys        # Virtual filesystem: device and kernel info
/dev        # Device files
/mnt        # Mount points for temporary mounts
/media      # Removable media mount points
/usr        # User programs, libraries, documentation

# Navigation
pwd                                  # Print working directory
cd /etc                              # Absolute path
cd ..                                # Go up one level
cd ~                                 # Go to home directory
cd -                                 # Go to previous directory
ls -la /etc                          # Long listing with hidden files
ls -lhS                              # Sort by size, human-readable
ls -lt                               # Sort by modification time
tree /etc -L 2                       # Tree view, 2 levels deep
```

### File & Directory Operations
```bash
# Create
mkdir -p projects/linux/lab1         # Create with parents
touch file.txt                       # Create empty file
touch file{1,2,3}.txt               # Brace expansion

# Copy, Move, Delete
cp file.txt backup.txt               # Copy file
cp -r dir1/ dir2/                    # Recursive copy
mv file.txt /tmp/                    # Move file
mv oldname.txt newname.txt           # Rename
rm file.txt                          # Delete file
rm -rf directory/                    # Delete directory recursively (CAREFUL)
rmdir empty_dir                      # Remove empty directory

# View & Search
cat file.txt                         # Print file contents
less file.txt                        # Page through file (q to quit)
head -n 20 file.txt                  # First 20 lines
tail -n 20 file.txt                  # Last 20 lines
tail -f /var/log/syslog              # Follow log file live
wc -l file.txt                       # Count lines
wc -w file.txt                       # Count words

# Links
ln -s /etc/nginx/nginx.conf ~/nginx.conf   # Symbolic link
ln file.txt hardlink.txt             # Hard link
```

### Permissions & Ownership
```bash
# Permission structure: [type][owner][group][others]
# Example: -rwxr-xr-- 1 alice devs 4096 Jan 1 12:00 script.sh
#          d = directory, - = file, l = symlink
#          r=4, w=2, x=1

chmod 755 script.sh                  # rwxr-xr-x (numeric)
chmod u+x script.sh                  # Add execute for owner (symbolic)
chmod go-w file.txt                  # Remove write from group and others
chmod -R 644 /var/www/html           # Recursive chmod

chown alice file.txt                 # Change owner
chown alice:devs file.txt            # Change owner and group
chown -R www-data:www-data /var/www  # Recursive chown

# Special permissions
chmod +s script.sh                   # Setuid/setgid
chmod +t /tmp                        # Sticky bit

# Check permissions
ls -la
stat file.txt                        # Detailed file metadata
umask                                # Default permission mask
```

### Users & Groups
```bash
# User management
useradd -m -s /bin/bash -G sudo alice    # Add user
passwd alice                              # Set password
usermod -aG docker alice                  # Add to group (append)
userdel -r alice                          # Delete user and home dir
id alice                                  # Show user/group IDs
who                                       # Logged-in users
w                                         # Who is doing what
last                                      # Login history

# Group management
groupadd developers                       # Create group
groupdel developers                       # Delete group
groups alice                              # Show user's groups
cat /etc/passwd                           # User accounts
cat /etc/group                            # Group definitions
cat /etc/shadow                           # Password hashes (root only)

# Switching users
su - alice                                # Switch to user (login shell)
sudo command                              # Run as root
sudo -i                                   # Open root shell
sudo -u alice command                     # Run as specific user
visudo                                    # Safely edit sudoers file
```

### Text Manipulation
```bash
# Essential tools
grep "error" /var/log/syslog             # Search for pattern
grep -i "error" file.txt                 # Case-insensitive
grep -r "TODO" ./src/                    # Recursive search
grep -n "pattern" file.txt               # Show line numbers
grep -v "DEBUG" app.log                  # Invert match (exclude)
grep -E "error|warn" file.txt            # Extended regex (ERE)
grep -c "pattern" file.txt               # Count matching lines

sort file.txt                            # Sort alphabetically
sort -n numbers.txt                      # Numeric sort
sort -r file.txt                         # Reverse sort
sort -k2 data.txt                        # Sort by field 2
sort -u file.txt                         # Sort and deduplicate

uniq -c sorted.txt                       # Count consecutive duplicates
cut -d',' -f1,3 data.csv                 # Cut fields from CSV
cut -c1-20 file.txt                      # Cut by character range

tr 'a-z' 'A-Z' < file.txt               # Translate characters
tr -d '\r' < windows.txt > unix.txt      # Delete carriage returns
tr -s ' ' < file.txt                     # Squeeze repeated spaces

awk '{print $1, $3}' file.txt            # Print fields 1 and 3
awk -F',' '{print $2}' data.csv          # Set field separator
awk '{sum += $1} END {print sum}' nums.txt  # Sum a column
awk '$3 > 100 {print $0}' data.txt       # Conditional filter

sed 's/old/new/' file.txt                # Replace first occurrence per line
sed 's/old/new/g' file.txt               # Replace all occurrences
sed -i 's/foo/bar/g' file.txt            # In-place edit
sed '/^#/d' config.txt                   # Delete comment lines
sed -n '10,20p' file.txt                 # Print lines 10–20

# Combining tools — the Unix philosophy
cat /var/log/auth.log | grep "Failed" | awk '{print $11}' | sort | uniq -c | sort -rn | head -10
```

### Pipes, Redirection & I/O
```bash
# Redirection
command > file.txt                   # Redirect stdout (overwrite)
command >> file.txt                  # Redirect stdout (append)
command 2> errors.txt                # Redirect stderr
command 2>&1                         # Redirect stderr to stdout
command > /dev/null 2>&1             # Silence all output
command &> file.txt                  # Redirect both stdout and stderr

# Pipes
ls -la | grep "^d"                   # Pipe stdout to grep
ps aux | grep nginx | grep -v grep   # Multi-pipe
command | tee file.txt               # Write to file AND stdout

# Here documents
cat << EOF > config.txt
server_name=localhost
port=8080
EOF

# Process substitution
diff <(ls dir1) <(ls dir2)           # Compare output of two commands
```

### Exercises
1. Navigate to `/etc` and find all files modified in the last 7 days using `find`.
2. Create a directory structure `projects/{web,api,db}/{src,tests,docs}` using one command.
3. Write a pipeline that finds the 10 largest files in `/var/log`.
4. Use `awk` to calculate the total size of all `.log` files in a directory.
5. Parse `/etc/passwd` to list all users with their home directories and shells.
6. Use `sed` to comment out all lines containing "deprecated" in a config file.
7. Find all files owned by root with SUID bit set across the entire system.
8. Write a pipeline to show the top 10 most frequent words in a text file.

### 🔨 Mini-Projects
**1. System Snapshot Tool**
A script that collects: hostname, OS version, uptime, CPU info, RAM usage, disk usage per partition, top 5 processes by CPU/memory, and last 10 logins. Outputs a formatted report to a timestamped file.

**2. Log Analyzer**
Parse `/var/log/auth.log` or `/var/log/syslog` to report: failed login attempts with IP addresses, successful logins, sudo usage, and service restarts. Display results with counts, sorted by frequency.

---

## Stage 2 — System Administration (Weeks 4–6)

**Goal:** Manage processes, services, packages, storage, and scheduled tasks like a sysadmin.

### Process Management
```bash
# Viewing processes
ps aux                               # All processes, all users
ps aux | grep nginx                  # Find specific process
pgrep nginx                          # Get PID by name
pstree                               # Process tree
top                                  # Live process monitor
htop                                 # Enhanced live monitor (install separately)
pidof nginx                          # PID of running program

# Controlling processes
kill 1234                            # Send SIGTERM (graceful)
kill -9 1234                         # Send SIGKILL (force)
killall nginx                        # Kill by name
pkill -f "python app.py"             # Kill by pattern
kill -l                              # List all signals

# Signals reference
# SIGTERM (15) — graceful shutdown request
# SIGKILL (9)  — force kill, cannot be caught
# SIGHUP  (1)  — reload config (many daemons)
# SIGINT  (2)  — interrupt (Ctrl+C)
# SIGSTOP (19) — pause process
# SIGCONT (18) — resume process

# Background/foreground
command &                            # Run in background
Ctrl+Z                               # Suspend foreground job
bg %1                                # Resume job 1 in background
fg %1                                # Bring job 1 to foreground
jobs                                 # List current shell's jobs
nohup command &                      # Run immune to hangup
disown %1                            # Detach job from shell
```

### systemd & Service Management
```bash
# Service control
systemctl start nginx
systemctl stop nginx
systemctl restart nginx
systemctl reload nginx               # Reload config without restart
systemctl enable nginx               # Enable at boot
systemctl disable nginx
systemctl status nginx               # Detailed status
systemctl is-active nginx
systemctl is-enabled nginx

# System state
systemctl list-units --type=service  # List all services
systemctl list-units --failed        # Show failed services
systemctl daemon-reload              # Reload unit files after changes
systemctl reboot
systemctl poweroff

# Logs with journald
journalctl -u nginx                  # Logs for specific service
journalctl -u nginx -f               # Follow logs live
journalctl -u nginx --since "1 hour ago"
journalctl -p err                    # Error-level and above
journalctl -b                        # Logs since last boot
journalctl --disk-usage
journalctl --vacuum-time=7d          # Delete logs older than 7 days

# Writing a custom service unit
cat << 'EOF' > /etc/systemd/system/myapp.service
[Unit]
Description=My Python Application
After=network.target postgresql.service
Requires=postgresql.service

[Service]
Type=simple
User=appuser
WorkingDirectory=/opt/myapp
ExecStart=/opt/myapp/venv/bin/python app.py
ExecReload=/bin/kill -HUP $MAINPID
Restart=on-failure
RestartSec=5
StandardOutput=journal
StandardError=journal
Environment=APP_ENV=production

[Install]
WantedBy=multi-user.target
EOF
```

### Package Management
```bash
# APT (Debian/Ubuntu)
apt update                           # Refresh package lists
apt upgrade                          # Upgrade all packages
apt install nginx git curl           # Install packages
apt remove nginx                     # Remove package (keep config)
apt purge nginx                      # Remove package and config
apt autoremove                       # Remove unused dependencies
apt search nginx                     # Search available packages
apt show nginx                       # Show package details
apt list --installed                 # List installed packages
dpkg -l                              # List all dpkg packages
dpkg -L nginx                        # Files installed by package

# DNF/YUM (RHEL/CentOS/Fedora)
dnf update
dnf install nginx
dnf remove nginx
dnf search nginx
dnf info nginx

# Snap & Flatpak (universal packages)
snap install code --classic
snap list
flatpak install flathub com.spotify.Client
```

### Storage & Filesystems
```bash
# Disk information
lsblk                                # Block devices tree
lsblk -f                             # With filesystem info
fdisk -l                             # Partition tables (root)
blkid                                # UUIDs and filesystem types
df -h                                # Disk space usage
du -sh /var/log                      # Directory size
du -sh /* 2>/dev/null | sort -h      # Find large directories
ncdu /                               # Interactive disk usage

# Partitioning
fdisk /dev/sdb                       # Interactive partitioner (MBR)
gdisk /dev/sdb                       # For GPT disks
parted /dev/sdb                      # Advanced partitioner

# Filesystems
mkfs.ext4 /dev/sdb1                  # Format as ext4
mkfs.xfs /dev/sdb1                   # Format as XFS
mkfs.vfat /dev/sdb1                  # Format as FAT32

# Mounting
mount /dev/sdb1 /mnt/data            # Mount partition
mount -t nfs 192.168.1.10:/share /mnt/nfs  # Mount NFS
umount /mnt/data                     # Unmount
mount | grep sdb                     # Show mounts

# /etc/fstab — persistent mounts
# UUID=xxxx /mnt/data ext4 defaults,nofail 0 2
blkid /dev/sdb1                      # Get UUID for fstab

# LVM (Logical Volume Manager)
pvcreate /dev/sdb1                   # Physical volume
vgcreate vg_data /dev/sdb1           # Volume group
lvcreate -L 10G -n lv_data vg_data  # Logical volume
mkfs.ext4 /dev/vg_data/lv_data
lvextend -L +5G /dev/vg_data/lv_data  # Extend volume
resize2fs /dev/vg_data/lv_data       # Resize filesystem

# RAID (mdadm)
mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1
cat /proc/mdstat                     # RAID status
```

### Scheduled Tasks
```bash
# Cron syntax: MIN HOUR DOM MON DOW COMMAND
# *    *    *   *   *
# 0-59 0-23 1-31 1-12 0-7

crontab -e                           # Edit current user's crontab
crontab -l                           # List current crontab
crontab -u alice -e                  # Edit another user's crontab

# Examples
0 2 * * *     /opt/scripts/backup.sh          # Daily at 2 AM
*/5 * * * *   /opt/scripts/health-check.sh    # Every 5 minutes
0 0 * * 0     /opt/scripts/weekly-report.sh   # Weekly on Sunday
0 9 1 * *     /opt/scripts/monthly-invoice.sh # Monthly on 1st at 9 AM
@reboot       /opt/scripts/startup.sh         # On system boot
@daily        /opt/scripts/cleanup.sh         # Once per day

# systemd timers (modern alternative to cron)
cat << 'EOF' > /etc/systemd/system/backup.timer
[Unit]
Description=Daily Backup Timer

[Timer]
OnCalendar=daily
Persistent=true

[Install]
WantedBy=timers.target
EOF

systemctl enable --now backup.timer
systemctl list-timers
```

### Exercises
1. Write a systemd service unit for a Node.js application with auto-restart.
2. Create a cron job that archives `/var/log` entries older than 30 days to `/backup/logs`.
3. Use `ps`, `grep`, and `kill` to gracefully stop all Python processes.
4. Set up LVM on a new disk: create PV, VG, LV, format, and mount it persistently via fstab.
5. Find all services that are enabled at boot but currently stopped.
6. Write a script that monitors a process and restarts it if it dies (before learning systemd Restart=).
7. Use `journalctl` to extract all error-level events from the past 24 hours and save to a file.

### 🔨 Mini-Projects
**1. Server Health Monitor**
A cron-driven script (runs every 5 minutes) that checks: CPU usage, memory usage, disk usage, and key service status. Writes to a rolling log file and sends an alert email (using `mail` or `curl` to a webhook) if any threshold is breached.

**2. Package Audit Tool**
Script that inventories all installed packages, flags packages not updated in 90+ days, checks for security updates with `apt-get -s upgrade`, and produces a formatted HTML report.

---

## Stage 3 — Bash Scripting (Weeks 7–10)

**Goal:** Automate real system administration tasks with robust, production-quality Bash scripts.

### Script Foundations
```bash
#!/usr/bin/env bash
# Script header best practices
set -euo pipefail                    # Exit on error, undefined vars, pipe failures
set -E                               # Ensure ERR trap inherits in functions
IFS=$'\n\t'                          # Safer word splitting

# Script metadata
readonly SCRIPT_NAME="$(basename "$0")"
readonly SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
readonly TIMESTAMP="$(date +%Y%m%d_%H%M%S)"
readonly LOG_FILE="/var/log/${SCRIPT_NAME%.sh}.log"

# Logging function
log() {
    local level="$1"; shift
    echo "[$(date '+%Y-%m-%d %H:%M:%S')] [$level] $*" | tee -a "$LOG_FILE"
}
log INFO "Script started"
log ERROR "Something went wrong"
```

### Variables & Data Types
```bash
# Variables
name="Alice"
readonly PI=3.14159                  # Constant
export PATH="$HOME/bin:$PATH"        # Environment variable

# Arithmetic
count=0
((count++))
((count += 5))
result=$(( 10 * 5 + 3 ))
result=$(echo "scale=2; 22/7" | bc)  # Floating point with bc

# String operations
str="Hello, World!"
echo ${#str}                         # Length: 13
echo ${str:7:5}                      # Substring: World
echo ${str,,}                        # Lowercase
echo ${str^^}                        # Uppercase
echo ${str/World/Bash}               # Replace
echo ${str//l/L}                     # Replace all

# Default values
port="${PORT:-8080}"                  # Use 8080 if PORT unset
name="${1:?Error: name required}"     # Exit if arg 1 empty
output="${2:-/tmp/output.txt}"        # Default path

# Arrays
files=("app.py" "config.py" "utils.py")
files+=("tests.py")                  # Append
echo "${files[0]}"                   # First element
echo "${files[@]}"                   # All elements
echo "${#files[@]}"                  # Array length
echo "${files[@]:1:2}"              # Slice (elements 1 and 2)
for f in "${files[@]}"; do echo "$f"; done

# Associative arrays (Bash 4+)
declare -A config
config[host]="localhost"
config[port]="5432"
config[db]="myapp"
echo "${config[host]}"
for key in "${!config[@]}"; do echo "$key = ${config[$key]}"; done
```

### Control Flow
```bash
# Conditionals
if [[ "$status" -eq 0 ]]; then
    log INFO "Success"
elif [[ "$status" -eq 1 ]]; then
    log WARN "Warning"
else
    log ERROR "Failed with status $status"
fi

# Test operators
[[ -f "$file" ]]                     # File exists and is regular
[[ -d "$dir" ]]                      # Directory exists
[[ -r "$file" ]]                     # File is readable
[[ -w "$file" ]]                     # File is writable
[[ -x "$file" ]]                     # File is executable
[[ -z "$str" ]]                      # String is empty
[[ -n "$str" ]]                      # String is not empty
[[ "$a" == "$b" ]]                   # String equality
[[ "$a" != "$b" ]]                   # String inequality
[[ "$a" =~ ^[0-9]+$ ]]              # Regex match
[[ "$n" -gt 10 ]]                    # Numeric greater than
[[ "$n" -lt 10 && "$n" -gt 0 ]]     # Compound condition

# Case statement
case "$action" in
    start|up)
        start_service ;;
    stop|down)
        stop_service ;;
    restart)
        stop_service; start_service ;;
    status)
        check_status ;;
    *)
        echo "Usage: $0 {start|stop|restart|status}"
        exit 1 ;;
esac

# Loops
for i in {1..10}; do echo "$i"; done
for i in $(seq 1 5 100); do echo "$i"; done   # Step by 5

while IFS= read -r line; do
    process_line "$line"
done < input.txt

while true; do
    if check_condition; then break; fi
    sleep 5
done

until service_is_ready; do
    echo "Waiting..."; sleep 2
done

# Loop control
continue                             # Skip to next iteration
break                                # Exit loop
break 2                              # Exit 2 levels of loops
```

### Functions
```bash
# Function definition and best practices
check_dependency() {
    local cmd="$1"
    if ! command -v "$cmd" &>/dev/null; then
        log ERROR "Required command not found: $cmd"
        return 1
    fi
}

# Return values and output
get_ip() {
    local interface="${1:-eth0}"
    ip addr show "$interface" 2>/dev/null \
        | awk '/inet / {print $2}' \
        | cut -d/ -f1
}
ip_address="$(get_ip eth0)"

# Local variables (avoid polluting global scope)
calculate_percentage() {
    local part="$1"
    local total="$2"
    local result
    result=$(echo "scale=2; ($part / $total) * 100" | bc)
    echo "$result"
}

# Function libraries — source them in scripts
source "$SCRIPT_DIR/lib/logging.sh"
source "$SCRIPT_DIR/lib/utils.sh"
```

### Error Handling & Robustness
```bash
# Trap for cleanup on exit
cleanup() {
    local exit_code=$?
    log INFO "Cleaning up..."
    rm -f "$TEMP_FILE"
    [[ $exit_code -ne 0 ]] && log ERROR "Script exited with code $exit_code"
}
trap cleanup EXIT
trap 'log ERROR "Interrupted"; exit 130' INT TERM

# Temp files safely
TEMP_FILE="$(mktemp /tmp/myscript.XXXXXX)"
TEMP_DIR="$(mktemp -d /tmp/myscript.XXXXXX)"

# Error handling without set -e
run_command() {
    if ! "$@"; then
        log ERROR "Command failed: $*"
        return 1
    fi
}

# Retry logic
retry() {
    local max_attempts="$1"; shift
    local delay="${1:-5}"; shift
    local attempt=1
    until "$@"; do
        if (( attempt >= max_attempts )); then
            log ERROR "Command failed after $max_attempts attempts: $*"
            return 1
        fi
        log WARN "Attempt $attempt failed. Retrying in ${delay}s..."
        sleep "$delay"
        ((attempt++))
    done
}
retry 3 5 curl -sf "https://api.example.com/health"
```

### Input Validation & Argument Parsing
```bash
# Manual argument parsing
usage() {
    cat << EOF
Usage: $SCRIPT_NAME [OPTIONS] <input_file>

Options:
  -o, --output FILE    Output file (default: output.txt)
  -v, --verbose        Enable verbose output
  -n, --dry-run        Show what would be done, without doing it
  -h, --help           Show this help message

Examples:
  $SCRIPT_NAME -o /tmp/result.txt data.csv
  $SCRIPT_NAME --verbose --dry-run input.txt
EOF
}

# getopts (POSIX-compatible short options)
while getopts "o:vnh" opt; do
    case $opt in
        o) OUTPUT_FILE="$OPTARG" ;;
        v) VERBOSE=true ;;
        n) DRY_RUN=true ;;
        h) usage; exit 0 ;;
        *) usage; exit 1 ;;
    esac
done
shift $((OPTIND - 1))

# Validate positional argument
INPUT_FILE="${1:?$(usage; echo 'Error: input_file required')}"
[[ -f "$INPUT_FILE" ]] || { log ERROR "File not found: $INPUT_FILE"; exit 1; }
[[ -r "$INPUT_FILE" ]] || { log ERROR "File not readable: $INPUT_FILE"; exit 1; }

# Input validation functions
is_integer() { [[ "$1" =~ ^-?[0-9]+$ ]]; }
is_ip() { [[ "$1" =~ ^([0-9]{1,3}\.){3}[0-9]{1,3}$ ]]; }
is_port() { is_integer "$1" && (( $1 >= 1 && $1 <= 65535 )); }
```

### Advanced Bash Patterns
```bash
# Parallel execution
run_parallel() {
    local max_jobs="${1:-4}"; shift
    local job_count=0
    for item in "$@"; do
        process_item "$item" &
        ((job_count++))
        if (( job_count >= max_jobs )); then
            wait -n 2>/dev/null || wait
            ((job_count--))
        fi
    done
    wait
}

# Named pipes (FIFOs)
mkfifo /tmp/pipe
producer > /tmp/pipe &
consumer < /tmp/pipe

# Process substitution in loops
while IFS=',' read -r name email role; do
    create_user "$name" "$email" "$role"
done < <(grep -v '^#' users.csv)

# Here strings
while IFS=: read -r user _ uid gid _ home shell; do
    echo "User: $user, Shell: $shell"
done <<< "$(cat /etc/passwd)"

# Config file parsing
parse_config() {
    local config_file="$1"
    while IFS='=' read -r key value; do
        [[ "$key" =~ ^[[:space:]]*# ]] && continue   # Skip comments
        [[ -z "$key" ]] && continue                    # Skip empty lines
        key="${key// /}"                               # Remove spaces
        value="${value// /}"
        declare -g "CONFIG_${key^^}=$value"
    done < "$config_file"
}
```

### Exercises
1. Write a script that accepts a directory as argument and produces a report: total files, total size, file type breakdown, and 5 largest files.
2. Build a script that reads a CSV of server hostnames and checks SSH connectivity, HTTP response, and disk usage — producing a status table.
3. Write a backup script with retention: archive a directory, compress it, name it with a timestamp, and delete backups older than N days.
4. Create a `deploy.sh` script with `--dry-run` support that syncs files, restarts a service, and rolls back on failure.
5. Write a parallel log processor that splits a large log file and processes chunks concurrently.
6. Build a script with full `getopts` argument parsing, a help menu, and strict input validation.
7. Write a retry wrapper that re-runs a flaky command up to N times with exponential backoff.

### 🔨 Mini-Projects
**1. Automated Backup System**
Complete backup solution: `backup.sh` backs up specified directories to a local and remote destination (via `rsync`). Supports incremental backups, configurable retention, compression, checksums, email notification on failure, and a `restore.sh` counterpart. Fully logged, testable with `--dry-run`.

**2. User Provisioning System**
`provision_users.sh` reads a CSV (`name,email,role,group`) and: creates Linux users, sets random passwords, assigns groups, creates home directories with templated dotfiles, emails credentials, and logs all actions. Includes an `audit_users.sh` to detect accounts not in the CSV.

**3. Deployment Pipeline Script**
`deploy.sh` that: pulls latest code from Git, runs tests, backs up current version, deploys new version, verifies the app is healthy (HTTP check), and auto-rolls back if health check fails after 30 seconds. Supports `--env`, `--dry-run`, `--rollback` flags.

---

## Stage 4 — Networking Fundamentals (Weeks 11–14)

**Goal:** Understand how data moves across networks and diagnose connectivity issues.

### Networking Concepts

#### The OSI Model
| Layer | Name | Examples | Key Protocols |
|---|---|---|---|
| 7 | Application | Browser, curl | HTTP, FTP, SMTP, DNS, SSH |
| 6 | Presentation | SSL/TLS, encoding | TLS, JPEG, ASCII |
| 5 | Session | Authentication sessions | NetBIOS, RPC |
| 4 | Transport | TCP/UDP segments | TCP, UDP, QUIC |
| 3 | Network | IP routing | IP, ICMP, OSPF, BGP |
| 2 | Data Link | MAC frames, switches | Ethernet, Wi-Fi, ARP |
| 1 | Physical | Cables, signals | Copper, Fiber, Radio |

#### TCP/IP Model (Practical)
| Layer | Corresponds to OSI | Focus |
|---|---|---|
| Application | 5–7 | HTTP, DNS, SSH |
| Transport | 4 | TCP, UDP |
| Internet | 3 | IP, ICMP, routing |
| Network Access | 1–2 | Ethernet, Wi-Fi |

#### IP Addressing & Subnetting
```
IPv4: 32-bit address, dotted decimal: 192.168.1.100
IPv6: 128-bit address, hexadecimal: 2001:db8::1

CIDR Notation:
192.168.1.0/24   → 256 addresses, 254 usable hosts
192.168.1.0/25   → 128 addresses, 126 usable hosts
10.0.0.0/8       → 16,777,216 addresses

Private Ranges (RFC 1918):
10.0.0.0/8       → Class A private
172.16.0.0/12    → Class B private
192.168.0.0/16   → Class C private
127.0.0.0/8      → Loopback

Special:
0.0.0.0          → Any/all interfaces
255.255.255.255  → Broadcast
169.254.0.0/16   → Link-local (APIPA, no DHCP)

Subnetting quick reference:
/24 = 255.255.255.0   → 254 hosts
/25 = 255.255.255.128 → 126 hosts
/26 = 255.255.255.192 → 62 hosts
/27 = 255.255.255.224 → 30 hosts
/28 = 255.255.255.240 → 14 hosts
/30 = 255.255.255.252 → 2 hosts (point-to-point links)
```

#### TCP vs. UDP
| Feature | TCP | UDP |
|---|---|---|
| Connection | Connection-oriented (3-way handshake) | Connectionless |
| Reliability | Guaranteed delivery, ordered | Best-effort, no order guarantee |
| Error handling | Retransmission | None built-in |
| Speed | Slower (overhead) | Faster |
| Use cases | HTTP, SSH, FTP, SMTP | DNS, VoIP, video streaming, gaming |
| Flow control | Yes (sliding window) | No |

#### Common Ports to Memorize
```
20/21  — FTP (data/control)       22   — SSH
23     — Telnet                   25   — SMTP
53     — DNS                      67/68 — DHCP
80     — HTTP                     110  — POP3
143    — IMAP                     161  — SNMP
443    — HTTPS                    465  — SMTPS
587    — SMTP (submission)        993  — IMAPS
3306   — MySQL                    5432 — PostgreSQL
6379   — Redis                    27017 — MongoDB
8080   — HTTP alt                 8443 — HTTPS alt
```

### Linux Networking Commands
```bash
# Interface information
ip addr show                         # All interfaces with IPs
ip addr show eth0                    # Specific interface
ip link show                         # Link-layer info
ifconfig eth0                        # Legacy (deprecated)
hostname -I                          # All IP addresses

# Routing
ip route show                        # Routing table
ip route get 8.8.8.8                 # Which route will be used
route -n                             # Legacy routing table
traceroute 8.8.8.8                   # Trace path to host
tracepath 8.8.8.8                    # Like traceroute, no root needed
mtr 8.8.8.8                         # Live traceroute (my traceroute)

# DNS
dig google.com                       # Full DNS query
dig google.com A                     # A record only
dig google.com MX                    # Mail records
dig @8.8.8.8 google.com             # Query specific DNS server
dig +short google.com                # Just the IP
nslookup google.com                  # Interactive DNS lookup
host google.com                      # Simple DNS lookup
resolvectl status                    # systemd-resolved status
cat /etc/resolv.conf                 # DNS configuration
cat /etc/hosts                       # Local hostname resolution

# Connectivity
ping -c 4 8.8.8.8                   # ICMP ping (4 packets)
ping6 ::1                            # IPv6 ping
curl -I https://example.com          # HTTP headers only
curl -sv https://example.com         # Verbose (shows TLS handshake)
curl -o /dev/null -w "%{http_code} %{time_total}" https://example.com
wget --spider https://example.com    # Check URL without downloading

# Port & Socket Inspection
ss -tulnp                            # All listening sockets with PID
ss -s                                # Socket statistics
netstat -tulnp                       # Legacy equivalent
lsof -i :80                          # What's using port 80
lsof -i tcp                          # All TCP connections
nmap -sV localhost                   # Scan own host (service versions)
nmap -p 22,80,443 192.168.1.1       # Scan specific ports

# Network configuration (NetworkManager)
nmcli device status
nmcli connection show
nmcli connection add type ethernet ifname eth0
ip addr add 192.168.1.100/24 dev eth0     # Temporary IP
ip addr del 192.168.1.100/24 dev eth0
ip link set eth0 up
ip link set eth0 down

# Packet capture
tcpdump -i eth0                      # Capture on interface
tcpdump -i eth0 port 80              # Filter by port
tcpdump -i eth0 host 192.168.1.1    # Filter by host
tcpdump -i eth0 -w capture.pcap     # Write to file
tcpdump -r capture.pcap             # Read from file
wireshark capture.pcap               # Open in Wireshark GUI

# Bandwidth testing
iperf3 -s                            # Start iperf server
iperf3 -c 192.168.1.10              # Connect and test bandwidth
speedtest-cli                        # Internet speed test
```

### SSH & Remote Access
```bash
# Key-based authentication
ssh-keygen -t ed25519 -C "user@host" -f ~/.ssh/id_ed25519
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@remote-host
ssh-add ~/.ssh/id_ed25519            # Add to SSH agent

# Connection options
ssh -p 2222 user@host                # Custom port
ssh -i ~/.ssh/deploy_key user@host  # Specific key
ssh -L 8080:localhost:80 user@host  # Local port forward
ssh -R 9090:localhost:3000 user@host # Remote port forward
ssh -D 1080 user@host               # SOCKS proxy
ssh -N -f user@host -L ...          # Background, no command

# SSH config file (~/.ssh/config)
cat << 'EOF' >> ~/.ssh/config
Host prod-server
    HostName 203.0.113.10
    User deploy
    IdentityFile ~/.ssh/prod_key
    Port 2222
    ServerAliveInterval 60
    ServerAliveCountMax 3

Host bastion
    HostName 203.0.113.1
    User admin

Host internal
    HostName 10.0.0.5
    ProxyJump bastion
EOF
ssh prod-server                      # Use alias

# Hardening /etc/ssh/sshd_config
# PasswordAuthentication no
# PermitRootLogin no
# PubkeyAuthentication yes
# AllowUsers deploy admin
# MaxAuthTries 3
# ClientAliveInterval 300

# File transfer
scp file.txt user@host:/remote/path/
scp -r dir/ user@host:/remote/
rsync -avz --progress ./src/ user@host:/var/www/
rsync -avz --delete ./src/ user@host:/var/www/  # Mirror with deletion
```

### Firewall — UFW & iptables
```bash
# UFW (Uncomplicated Firewall — Ubuntu/Debian)
ufw enable
ufw disable
ufw status verbose
ufw allow ssh
ufw allow 80/tcp
ufw allow 443/tcp
ufw allow from 192.168.1.0/24
ufw allow from 10.0.0.5 to any port 5432
ufw deny 23
ufw delete allow 80/tcp
ufw reset

# iptables (direct — lower level)
iptables -L -n -v                    # List all rules with counters
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -j DROP           # Default deny
iptables -A INPUT -s 10.0.0.0/8 -j DROP  # Block subnet
iptables -A FORWARD -j DROP
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE  # NAT
iptables-save > /etc/iptables/rules.v4   # Persist rules

# nftables (modern replacement for iptables)
nft list ruleset
nft add table inet filter
nft add chain inet filter input { type filter hook input priority 0 \; }
nft add rule inet filter input tcp dport 22 accept
```

### Exercises
1. Subnet 192.168.10.0/24 into 4 equal subnets. List the network address, broadcast, and usable range for each.
2. Use `dig` to trace the full DNS resolution chain for `www.github.com` (A, CNAME, NS records).
3. Capture HTTP traffic on loopback with `tcpdump` while running `curl`. Inspect the request and response.
4. Set up SSH key-based auth between two VMs, configure `~/.ssh/config`, and disable password auth.
5. Use `ss` to list all services listening on your machine. Identify and document each one.
6. Configure UFW: allow SSH from a specific subnet only, allow 80/443 from anywhere, deny everything else.
7. Use `mtr` to measure packet loss and latency to 3 different destinations. Interpret the results.
8. Set up a SOCKS proxy via SSH and route browser traffic through it.

### 🔨 Mini-Projects
**1. Network Scanner**
A Bash script that takes a CIDR range, pings all hosts, checks common ports (22, 80, 443, 3306, 5432), performs reverse DNS lookups, and generates an HTML network map report.

**2. SSH Bastion Host Lab**
On 3 VMs: configure a bastion host that only accepts SSH from your workstation, configure internal servers only accessible via the bastion using `ProxyJump`, set up key forwarding, harden all SSH configs, and document the network topology.

---

## Stage 5 — Network Services & Protocols (Weeks 15–17)

**Goal:** Configure and operate core network services that power real infrastructure.

### DNS — Bind9 & systemd-resolved
```bash
# Install BIND9
apt install bind9 bind9utils

# /etc/bind/named.conf.local — zone definition
zone "example.local" {
    type master;
    file "/etc/bind/zones/db.example.local";
};

# /etc/bind/zones/db.example.local — zone file
$TTL 3600
@   IN  SOA ns1.example.local. admin.example.local. (
        2024010101 ; Serial
        3600       ; Refresh
        1800       ; Retry
        604800     ; Expire
        3600 )     ; Minimum TTL

@       IN  NS  ns1.example.local.
ns1     IN  A   192.168.1.10
www     IN  A   192.168.1.20
mail    IN  A   192.168.1.30
@       IN  MX  10 mail.example.local.

# Test
named-checkconf
named-checkzone example.local /etc/bind/zones/db.example.local
dig @localhost www.example.local
```

### DHCP — isc-dhcp-server
```bash
# /etc/dhcp/dhcpd.conf
default-lease-time 86400;
max-lease-time 172800;

subnet 192.168.1.0 netmask 255.255.255.0 {
    range 192.168.1.100 192.168.1.200;
    option routers 192.168.1.1;
    option domain-name-servers 192.168.1.10, 8.8.8.8;
    option domain-name "example.local";
}

# Static reservation (by MAC)
host printer {
    hardware ethernet aa:bb:cc:dd:ee:ff;
    fixed-address 192.168.1.50;
}
```

### Web Servers — Nginx & Apache
```nginx
# Nginx virtual host — /etc/nginx/sites-available/example.com
server {
    listen 80;
    server_name example.com www.example.com;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl http2;
    server_name example.com www.example.com;
    root /var/www/example.com;
    index index.html;

    ssl_certificate     /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers ECDHE-RSA-AES256-GCM-SHA512:...;

    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
    add_header X-Frame-Options DENY;
    add_header X-Content-Type-Options nosniff;

    location / {
        try_files $uri $uri/ =404;
    }

    location /api/ {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    access_log /var/log/nginx/example.access.log;
    error_log  /var/log/nginx/example.error.log;
}
```

### Email — Postfix & Dovecot (Overview)
```bash
# Postfix — MTA (sending)
apt install postfix
postconf -e 'myhostname = mail.example.com'
postconf -e 'mydomain = example.com'
postconf -e 'inet_interfaces = all'

# Test email sending
echo "Test" | mail -s "Test Subject" user@example.com
postqueue -p                         # View mail queue
postfix flush                        # Flush queue
mailq                                # Show queue

# Dovecot — IMAP/POP3 (receiving)
apt install dovecot-imapd dovecot-pop3d
```

### Monitoring — Prometheus & Grafana (Introduction)
```bash
# Node Exporter (system metrics)
wget https://github.com/prometheus/node_exporter/releases/download/v*/node_exporter-*.linux-amd64.tar.gz
# Expose metrics on :9100

# Prometheus config — prometheus.yml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'nodes'
    static_configs:
      - targets: ['localhost:9100', '192.168.1.11:9100']

# Grafana — connect to Prometheus as data source
# Import Node Exporter Full dashboard (ID: 1860)
```

### Exercises
1. Set up a local DNS server with BIND9. Create A records for 5 hostnames and verify resolution from other VMs.
2. Configure Nginx as a reverse proxy for 3 different backend services on different paths.
3. Obtain a TLS certificate with Certbot and configure Nginx with proper TLS settings. Verify with SSL Labs.
4. Set up a DHCP server on a VM network and verify other VMs receive addresses and correct DNS settings.
5. Write an Nginx access log parser in Bash that reports top IPs, status code distribution, and slowest endpoints.

### 🔨 Mini-Projects
**1. Local DNS + DHCP Lab**
Full internal network: BIND9 authoritative DNS for `lab.local`, DHCP server with static reservations for key hosts, all VMs using internal DNS, PTR (reverse DNS) records configured, and a Bash script to auto-update DNS when hosts join.

**2. Nginx Reverse Proxy with SSL**
Set up Nginx as a reverse proxy fronting 3 services (could be simple Python HTTP servers). Enforce HTTPS redirect, add security headers, configure rate limiting, set up custom error pages, and write a health-check script that monitors all backends.

---

## Stage 6 — Security Hardening (Weeks 18–20)

**Goal:** Apply defense-in-depth to protect Linux systems and networks.

### System Hardening
```bash
# Kernel parameters — /etc/sysctl.conf
net.ipv4.ip_forward = 0                    # Disable routing (unless router)
net.ipv4.conf.all.rp_filter = 1           # Reverse path filtering
net.ipv4.conf.all.accept_source_route = 0  # Ignore source-routed packets
net.ipv4.tcp_syncookies = 1               # SYN flood protection
net.ipv4.conf.all.log_martians = 1        # Log impossible packets
kernel.randomize_va_space = 2             # ASLR — full randomization
kernel.sysrq = 0                          # Disable magic SysRq key
fs.suid_dumpable = 0                      # No core dumps for SUID
sysctl -p                                  # Apply changes

# Disable unnecessary services
systemctl disable avahi-daemon
systemctl disable cups
systemctl disable bluetooth
systemctl disable rpcbind

# Remove unnecessary packages
apt purge telnet rsh-client ftp nis
apt autoremove

# Secure shared memory
echo "tmpfs /run/shm tmpfs defaults,noexec,nosuid 0 0" >> /etc/fstab

# PAM password policy — /etc/security/pwquality.conf
minlen = 14
dcredit = -1
ucredit = -1
lcredit = -1
ocredit = -1
maxrepeat = 3

# Account lockout — /etc/pam.d/common-auth
# auth required pam_tally2.so deny=5 unlock_time=900

# Login banner
echo "Authorized access only. All activity logged." > /etc/issue
echo "Authorized access only. All activity logged." > /etc/issue.net
```

### Audit & Intrusion Detection
```bash
# auditd — Linux Audit System
apt install auditd

# /etc/audit/rules.d/audit.rules
-w /etc/passwd -p wa -k identity
-w /etc/shadow -p wa -k identity
-w /etc/sudoers -p wa -k sudoers
-w /var/log/auth.log -p wa -k auth_log
-a always,exit -F arch=b64 -S execve -k exec_commands
-w /bin/su -p x -k privilege_escalation

auditctl -l                          # List active rules
ausearch -k identity                 # Search by key
ausearch -m EXECVE --start today     # Executables run today
aureport --summary                   # Audit summary
aureport --failed                    # Failed events

# Fail2ban — IP banning for repeated failures
apt install fail2ban

# /etc/fail2ban/jail.local
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
bantime = 3600
findtime = 600

[nginx-http-auth]
enabled = true
filter = nginx-http-auth
logpath = /var/log/nginx/error.log
maxretry = 5

fail2ban-client status
fail2ban-client status sshd
fail2ban-client unban 192.168.1.100

# AIDE — File integrity monitoring
apt install aide
aide --init                          # Initialize database
aide --check                         # Check for changes
```

### TLS/SSL & PKI
```bash
# Generate self-signed cert
openssl req -x509 -nodes -days 365 -newkey rsa:4096 \
    -keyout server.key -out server.crt \
    -subj "/C=US/ST=CA/O=Example/CN=example.com"

# Create a private CA
openssl genrsa -out ca.key 4096
openssl req -x509 -new -nodes -key ca.key -sha256 -days 3650 -out ca.crt \
    -subj "/CN=Internal CA"

# Sign a CSR with the CA
openssl genrsa -out server.key 2048
openssl req -new -key server.key -out server.csr -subj "/CN=server.example.local"
openssl x509 -req -in server.csr -CA ca.crt -CAkey ca.key -CAcreateserial \
    -out server.crt -days 825 -sha256

# Inspect certificates
openssl x509 -in server.crt -text -noout
openssl s_client -connect example.com:443 -servername example.com
openssl verify -CAfile ca.crt server.crt

# Let's Encrypt (Certbot)
apt install certbot python3-certbot-nginx
certbot --nginx -d example.com -d www.example.com
certbot renew --dry-run
```

### VPN — WireGuard
```bash
# Install WireGuard
apt install wireguard

# Generate key pair
wg genkey | tee /etc/wireguard/private.key | wg pubkey > /etc/wireguard/public.key
chmod 600 /etc/wireguard/private.key

# Server config — /etc/wireguard/wg0.conf
[Interface]
Address = 10.10.0.1/24
ListenPort = 51820
PrivateKey = <server_private_key>
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

[Peer]
PublicKey = <client_public_key>
AllowedIPs = 10.10.0.2/32

# Client config
[Interface]
Address = 10.10.0.2/32
PrivateKey = <client_private_key>
DNS = 10.10.0.1

[Peer]
PublicKey = <server_public_key>
Endpoint = server_public_ip:51820
AllowedIPs = 0.0.0.0/0
PersistentKeepalive = 25

wg-quick up wg0
wg show
```

### Exercises
1. Harden a fresh Ubuntu server: disable root login, enforce SSH keys, configure UFW, set up Fail2ban for SSH.
2. Set up auditd with rules to monitor all writes to `/etc`, `/bin`, and `/usr/bin`. Trigger an alert and review the logs.
3. Create an internal CA, sign certificates for 3 services, and configure NGINX to use them.
4. Set up WireGuard between two VMs. Verify encrypted traffic with `tcpdump`.
5. Run `lynis audit system` and address the top 10 hardening suggestions.
6. Configure Fail2ban to protect Nginx (too many 404s) with a custom filter and action.

### 🔨 Mini-Projects
**1. Server Hardening Checklist Automator**
`harden.sh` — idempotent hardening script that applies: SSH hardening, sysctl parameters, UFW rules, Fail2ban setup, auditd rules, unnecessary service removal, and CIS Benchmark items. Produces a before/after compliance report using `lynis`.

---

## Stage 7 — Capstone Projects (Weeks 21–28)

Large, portfolio-worthy projects integrating Linux, Bash, and networking skills.

---

### 🏗️ Capstone 1 — Production-Ready Web Server Stack

**Skills:** Nginx, SSL/TLS, systemd, UFW, Fail2ban, Bash automation, monitoring

**Description:** Build and automate a complete, hardened web server stack from a bare OS.

**Deliverables:**
- Fully automated setup script: `provision.sh` (runs on fresh Ubuntu, configures everything)
- Nginx serving 3 virtual hosts with TLS (Let's Encrypt or internal CA)
- Reverse proxy to application backends (Python/Node simple apps)
- UFW firewall with documented ruleset
- Fail2ban protecting SSH and Nginx
- Automated certificate renewal with pre/post hooks
- Log rotation configuration for all services
- Health check script with alerting
- Complete documentation with architecture diagram

---

### 🏗️ Capstone 2 — Automated Infrastructure Backup System

**Skills:** Bash scripting, rsync, cron/systemd timers, SSH, storage management, encryption

**Description:** A production-grade backup system for a multi-server environment.

**Deliverables:**
- `backup-agent.sh` installed on each server (backs up databases, files, configs)
- Encrypted transfer to a central backup server using `rsync` over SSH
- GPG encryption of backup archives at rest
- Configurable retention policies (daily/weekly/monthly tiers)
- Integrity verification with checksums after each backup
- `restore.sh` that can restore any component from any date
- `backup-report.sh` generating daily HTML reports with sizes, durations, status
- systemd timer for scheduling with logging to journald
- Alerting via email or webhook on failure

---

### 🏗️ Capstone 3 — Network Lab with Routing & Services

**Skills:** Networking, DHCP, DNS, routing, iptables/nftables, VPN, monitoring

**Description:** Build a multi-subnet virtualized network that mirrors a real-world small business network.

**Network Topology:**
```
Internet
    |
[Router VM] — UFW/iptables NAT gateway, WireGuard VPN endpoint
    |
[DMZ: 10.0.1.0/24]           [LAN: 10.0.2.0/24]
    |                               |
[Web VM]                  [DHCP/DNS VM] [App VM] [DB VM]
```

**Deliverables:**
- Router VM configured as NAT gateway with iptables
- BIND9 authoritative DNS for `lab.internal` with reverse zones
- DHCP server with static reservations for key hosts
- WireGuard VPN allowing remote access to LAN
- Nginx reverse proxy in DMZ forwarding to App VM in LAN
- Internal-only services (DB, App) unreachable from DMZ
- `network-audit.sh` verifying firewall rules and connectivity matrix
- Full network diagram with IP allocations
- All configs in Git with a `rebuild.sh` that recreates the entire lab

---

### 🏗️ Capstone 4 — System Monitoring & Alerting Platform

**Skills:** Bash scripting, networking, systemd, Prometheus, Grafana, log management

**Description:** Build a complete observability platform for a fleet of servers.

**Deliverables:**
- Custom metrics collector (`collect-metrics.sh`) exporting Prometheus-format metrics
- Node Exporter deployed on all VMs via a Bash provisioner
- Prometheus server with scrape configs for all targets
- Grafana dashboards: system overview, per-host detail, network traffic
- Alert rules: CPU > 90% for 5min, disk > 85%, service down, SSH brute force detected
- Alertmanager routing alerts to email and a webhook (Slack/Discord)
- Centralized log aggregation with `rsyslog` forwarding to a log server
- Log analysis script: daily digest email with top errors, anomalies, security events
- `deploy-monitoring.sh` — one-command setup across all hosts via SSH

---

## 📚 Learning Resources

### Books
| Title | Level | Focus |
|---|---|---|
| *The Linux Command Line* — William Shotts | Beginner | Shell and commands |
| *How Linux Works* — Brian Ward | Beginner/Intermediate | Internals |
| *Linux Administration Handbook* — Nemeth et al. | Intermediate | Sysadmin reference |
| *Bash Cookbook* — Carl Albing | Intermediate | Scripting recipes |
| *UNIX and Linux System Administration Handbook* — Nemeth | Advanced | Comprehensive reference |
| *Computer Networks* — Andrew Tanenbaum | All levels | Networking theory |
| *TCP/IP Illustrated Vol. 1* — W. Richard Stevens | Advanced | TCP/IP deep dive |

### Interactive Platforms
- **OverTheWire: Bandit** (overthewire.org) — Linux security challenges, perfect for beginners
- **Linux Journey** (linuxjourney.com) — Structured browser exercises
- **KillerCoda** (killercoda.com) — Free browser-based Linux/Kubernetes scenarios
- **HackTheBox / TryHackMe** — Practical Linux + networking challenges
- **Networking fundamentals** — Professor Messer's CompTIA Network+ (free, YouTube)
- **Cisco Packet Tracer** — Free network simulation tool

### Tools Reference
- **explainshell.com** — Paste any command, see each part explained
- **ShellCheck** (shellcheck.net) — Bash script linter, run it on every script
- **tldr.sh** — Simplified man pages with practical examples
- **ss64.com** — Quick command reference for all shells and OSes

---

## 🗓️ Suggested Weekly Schedule

| Weeks | Stage |
|---|---|
| 1–3 | Stage 1: Linux Fundamentals |
| 4–6 | Stage 2: System Administration |
| 7–10 | Stage 3: Bash Scripting |
| 11–14 | Stage 4: Networking Fundamentals |
| 15–17 | Stage 5: Network Services & Protocols |
| 18–20 | Stage 6: Security Hardening |
| 21–28 | Stage 7: Capstone Projects |

**Daily habit:**
- 20 min — Read a concept / man page / documentation
- 45 min — Practice in the lab (commands, scripts, configs)
- 15 min — Document what you learned in your command journal

---

## ✅ Progress Checklist

### Stage 1 — Linux Fundamentals
- [ ] Navigate the filesystem without using a GUI
- [ ] Manage files, permissions, and ownership fluently
- [ ] Use `grep`, `awk`, `sed`, `cut`, `sort`, and pipes in combination
- [ ] Redirect I/O and construct multi-stage pipelines
- [ ] Complete all 8 exercises
- [ ] Finish System Snapshot and Log Analyzer projects

### Stage 2 — System Administration
- [ ] Manage processes with signals and background jobs
- [ ] Control services with `systemctl` and `journalctl`
- [ ] Write a custom systemd unit file
- [ ] Manage packages, disks, and LVM
- [ ] Schedule tasks with cron and systemd timers
- [ ] Finish Server Health Monitor and Package Audit projects

### Stage 3 — Bash Scripting
- [ ] Write scripts with `set -euo pipefail` and `trap` cleanup
- [ ] Use arrays, associative arrays, and string operations
- [ ] Parse arguments with `getopts` and validate input
- [ ] Write functions with local scope and return values
- [ ] Complete all 7 exercises
- [ ] Finish Backup System, User Provisioning, and Deployment Pipeline

### Stage 4 — Networking Fundamentals
- [ ] Subnet a /24 into smaller networks by hand
- [ ] Use `ip`, `ss`, `dig`, `tcpdump`, and `curl` fluently
- [ ] Configure SSH keys, config file, and port forwarding
- [ ] Set up firewall rules with UFW and iptables
- [ ] Complete all 8 exercises
- [ ] Finish Network Scanner and Bastion Host Lab

### Stage 5 & 6
- [ ] Configure BIND9 DNS with A, MX, and PTR records
- [ ] Set up Nginx as a reverse proxy with TLS
- [ ] Harden a server with auditd, Fail2ban, and sysctl params
- [ ] Set up a WireGuard VPN between two machines
- [ ] Build internal CA and sign certificates

### Stage 7 — Capstones
- [ ] Complete at least 2 capstone projects
- [ ] All scripts pass `shellcheck` with no errors
- [ ] All configs committed to Git with clear documentation
- [ ] Each project has a working `README.md` with architecture diagram
- [ ] At least 1 project deployed on real cloud infrastructure

---

## 💡 Key Principles for Success

1. **Break things on purpose** — Spin up a VM, misconfigure it, fix it. Breaking safely is the fastest teacher.
2. **Use `man` before Google** — Man pages are authoritative, always available, and faster than Stack Overflow.
3. **Run `shellcheck` on every script** — Always. No exceptions. It will catch errors before your server does.
4. **Document your lab** — Maintain a `notes.md` of every command you discover. You will search it constantly.
5. **Build a home lab** — Even 2 VMs on your laptop are enough to practice everything in this roadmap.
6. **Learn subnetting cold** — Practice until you can subnet any CIDR range on paper in under 2 minutes.
7. **Read logs before Googling errors** — The answer is usually in `/var/log`. Train this reflex early.
8. **Automate repetitive tasks immediately** — The moment you do something twice, write a script.
9. **Never test on production** — Always have a lab environment. Always snapshot VMs before major changes.
10. **The Unix philosophy** — Write programs that do one thing well. Chain them together. It scales forever.

---

*Last updated: 2026 — Ubuntu 24.04 LTS and Debian 12 used throughout. Commands verified on Linux kernel 6.x.*