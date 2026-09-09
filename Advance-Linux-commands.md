# 🐧 Advanced Linux Commands Reference

A beginner-friendly reference for **Linux administration, troubleshooting, networking, storage, security, and DevOps**.

---

## 📚 Table of Contents

- [1. Advanced File & Text Commands](#1-advanced-file--text-commands)
- [2. Advanced Process Management](#2-advanced-process-management)
- [3. Memory & CPU](#3-memory--cpu)
- [4. Advanced Disk Commands](#4-advanced-disk-commands)
- [5. Advanced Networking](#5-advanced-networking)
- [6. Firewall](#6-firewall)
- [7. SSH & Remote Administration](#7-ssh--remote-administration)
- [8. Package Management](#8-package-management)
- [9. Systemd & Services](#9-systemd--services)
- [10. Users & Groups](#10-users--groups)
- [11. Advanced Troubleshooting](#11-advanced-troubleshooting)
- [12. Date, Time & Scheduling](#12-date-time--scheduling)
- [13. Docker Basics](#13-docker-basics)
- [14. Commands to Learn First](#14-commands-to-learn-first)
- [15. Easy Way to Remember](#15-easy-way-to-remember)
- [16. Quick Learning Path](#16-quick-learning-path)
- [17. Safety Tips](#17-safety-tips)
- [18. Safe Practice Commands](#18-safe-practice-commands)

---

# 1. Advanced File & Text Commands

### Find files larger than 100 MB

```bash
find /var/log -type f -size +100M
```

### Find empty files

```bash
find /tmp -type f -empty
```

### Find files with permission `777`

```bash
find /path -type f -perm 777
```

### Find files owned by root

```bash
find /path -type f -user root
```

### Search for `ERROR` recursively

Ignore `.log` files:

```bash
grep -RIn --exclude="*.log" "ERROR" /path
```

### Print column 1 using `awk`

```bash
awk '{print $1}' file
```

### Print usernames and UIDs

```bash
awk -F: '{print $1,$3}' /etc/passwd
```

### Replace text with `sed`

This prints the modified output without changing the original file:

```bash
sed 's/foo/bar/g' file
```

### Run a command once for each input item

```bash
xargs -n1 echo
```

### Display output and save it to a file

```bash
tee output.txt
```

### Example: Find large files and display their sizes

```bash
find /var/log -type f -size +100M -exec ls -lh {} \;
```

---

# 2. Advanced Process Management

### Find a process by name

```bash
pgrep nginx
```

### Stop processes by name

```bash
pkill nginx
```

> ⚠️ Use `pkill` carefully. It can terminate multiple processes.

### Show process IDs

```bash
pidof nginx
```

### Show processes as a tree

```bash
pstree
```

### Show background jobs

```bash
jobs
```

### Continue a stopped job in the background

```bash
bg
```

### Bring a background job to the foreground

```bash
fg
```

### Keep a command running after logout

```bash
nohup command &
```

### Run a command in the background

```bash
command &
```

### Stop a command after 30 seconds

```bash
timeout 30 command
```

### Example: Run a server in the background

```bash
nohup ./server.sh > server.log 2>&1 &
```

This runs the server in the background and redirects both standard output and errors to `server.log`.

---

# 3. Memory & CPU

### Show RAM usage

```bash
free -h
```

### Show uptime and load average

```bash
uptime
```

### Monitor CPU, memory, and processes

```bash
vmstat 1
```

### Monitor CPU and disk I/O

```bash
iostat
```

### Show CPU statistics

```bash
mpstat
```

### Show system activity statistics

```bash
sar
```

### Show CPU information

```bash
lscpu
```

### Show memory information

```bash
lsmem
```

### Show NUMA hardware information

```bash
numactl --hardware
```

> Some commands such as `iostat`, `mpstat`, `sar`, and `numactl` may require additional packages to be installed.

---

# 4. Advanced Disk Commands

### Show disks and filesystem information

```bash
lsblk -f
```

### Show filesystem UUIDs

```bash
blkid
```

### Show mounted filesystems

```bash
mount
```

### Display mounted filesystems clearly

```bash
findmnt
```

### Show disk usage one level deep

```bash
du -xhd1 /
```

### Monitor disk I/O by process

```bash
iotop
```

### Check disk health

```bash
sudo smartctl -a /dev/sda
```

### Flush filesystem buffers

```bash
sync
```

### Run TRIM on supported filesystems

```bash
sudo fstrim -av
```

> ⚠️ Be careful when working with disks, partitions, mounting, and filesystem commands.

---

# 5. Advanced Networking

### Show HTTP headers

```bash
curl -I https://example.com
```

### Download a file with `curl`

```bash
curl -O URL
```

### Download a file with `wget`

```bash
wget URL
```

### Test whether a port is reachable

```bash
nc -zv host 80
```

### Show socket statistics

```bash
ss -s
```

### Show the neighbor/ARP table

```bash
ip neigh
```

### Show network interfaces

```bash
ip link
```

### Show DNS configuration

```bash
resolvectl status
```

### Find mail servers

```bash
dig MX example.com
```

### Find TXT DNS records

```bash
dig TXT example.com
```

---

# 6. Firewall

## UFW

### Check firewall status

```bash
sudo ufw status
```

### Allow SSH

```bash
sudo ufw allow 22/tcp
```

### Block Telnet

```bash
sudo ufw deny 23/tcp
```

### Enable UFW

```bash
sudo ufw enable
```

## nftables

### Show the current nftables ruleset

```bash
sudo nft list ruleset
```

> ⚠️ **Important:** Be extremely careful when changing firewall rules, especially over SSH. Incorrect rules can lock you out of a remote server.

---

# 7. SSH & Remote Administration

### Connect to a remote Linux machine

```bash
ssh user@server
```

### Connect using a custom SSH port

```bash
ssh -p 2222 user@server
```

### Copy a file to a remote server

```bash
scp file user@server:/path
```

### Download a remote file

```bash
scp user@server:/path/file .
```

### Synchronize files with `rsync`

```bash
rsync -av /data/ user@server:/backup/
```

### Generate SSH keys

```bash
ssh-keygen
```

### Copy your SSH public key to a server

```bash
ssh-copy-id user@server
```

### Create an SSH local port forward

```bash
ssh -L 8080:localhost:80 user@server
```

This forwards local port `8080` to port `80` on the remote side.

---

# 8. Package Management

## Debian / Ubuntu

### Update package information

```bash
sudo apt update
```

### Upgrade installed packages

```bash
sudo apt upgrade
```

### Install a package

```bash
sudo apt install nginx
```

### Remove a package

```bash
sudo apt remove nginx
```

### Search for a package

```bash
apt search nginx
```

## RHEL / Fedora

### Update packages

```bash
sudo dnf update
```

### Install a package

```bash
sudo dnf install nginx
```

### Remove a package

```bash
sudo dnf remove nginx
```

### Search for a package

```bash
dnf search nginx
```

---

# 9. Systemd & Services

### Check service status

```bash
systemctl status nginx
```

### Start a service

```bash
sudo systemctl start nginx
```

### Stop a service

```bash
sudo systemctl stop nginx
```

### Restart a service

```bash
sudo systemctl restart nginx
```

### Reload configuration

```bash
sudo systemctl reload nginx
```

### Enable a service at boot

```bash
sudo systemctl enable nginx
```

### Disable automatic startup

```bash
sudo systemctl disable nginx
```

### List services

```bash
systemctl list-units --type=service
```

### View service logs

```bash
journalctl -u nginx
```

---

# 10. Users & Groups

### Show current username

```bash
whoami
```

### Show user and group IDs

```bash
id
```

### Show logged-in users

```bash
who
```

### Show logged-in users and activity

```bash
w
```

### Show login history

```bash
last
```

### Show user's groups

```bash
groups
```

### Create a user

```bash
sudo useradd username
```

### Change a user's password

```bash
sudo passwd username
```

### Add a user to a group

```bash
sudo usermod -aG group user
```

### Delete a user

```bash
sudo userdel username
```

> ⚠️ User and group administration generally requires root privileges.

---

# 11. Advanced Troubleshooting

### Show the last 50 kernel messages

```bash
dmesg -T | tail -50
```

### Show errors from the current boot

```bash
journalctl -p err -b
```

### Find failed services

```bash
systemctl --failed
```

### Find deleted files still held open

```bash
lsof +L1
```

### Trace system calls from a running process

```bash
sudo strace -p PID
```

### Identify a file type

```bash
file filename
```

### Show detailed file information

```bash
stat filename
```

---

# 12. Date, Time & Scheduling

## Cron

Edit your user's scheduled jobs:

```bash
crontab -e
```

### Run a backup every day at 2:00 AM

```cron
0 2 * * * /home/user/backup.sh
```

## `at`

Schedule a one-time command:

```bash
at 14:30
```

> `cron` is generally used for recurring jobs, while `at` is useful for one-time scheduled tasks.

---

# 13. Docker Basics

### Show running containers

```bash
docker ps
```

### Show all containers

```bash
docker ps -a
```

### Show Docker images

```bash
docker images
```

### Download an Nginx image

```bash
docker pull nginx
```

### Start an Nginx container

```bash
docker run nginx
```

### Stop a container

```bash
docker stop CONTAINER
```

### Delete a container

```bash
docker rm CONTAINER
```

### Show container logs

```bash
docker logs CONTAINER
```

### Open a shell inside a container

```bash
docker exec -it CONTAINER bash
```

> Depending on the image, `bash` may not exist. Alpine-based images commonly use `sh` instead.

---

# 14. Commands to Learn First

If you're new to Linux, start with these:

| Command | Purpose |
|---|---|
| `pwd` | Show current directory |
| `ls -lh` | List files with readable sizes |
| `cd /path` | Change directory |
| `find /path` | Find files |
| `grep "text" file` | Search text |
| `ps aux` | Show processes |
| `top` | Monitor the system |
| `free -h` | Check memory |
| `df -h` | Check disk space |
| `du -sh folder` | Check folder size |
| `ip -br a` | Show IP addresses |
| `ss -tuln` | Check listening ports |
| `systemctl status nginx` | Check a service |
| `journalctl -xe` | View system logs |

---

# 15. Easy Way to Remember

| Command | Remember It As |
|---|---|
| `find` | Find files |
| `grep` | Find text |
| `ps` / `top` | Check processes |
| `free` | Check memory |
| `df` / `du` | Check disk |
| `chmod` | Change permissions |
| `chown` | Change ownership |
| `ss` / `ip` | Check network |
| `tar` / `zip` | Compress files |
| `ssh` | Remote connection |
| `systemctl` | Manage services |
| `journalctl` | Check logs |
| `docker` | Manage containers |

---

# 16. Quick Learning Path

A practical Linux learning path:

1. **Basic Linux commands**
2. **Files and directories**
3. **`grep` / `awk` / `sed`**
4. **Processes**
5. **Permissions**
6. **Disk management**
7. **Networking**
8. **SSH**
9. **Systemd**
10. **Logs and troubleshooting**
11. **Firewall**
12. **Bash scripting**
13. **Docker**
14. **Linux administration**

---

# 17. Safety Tips

- Always double-check commands before using `sudo`.
- Be careful with `rm`, `kill`, `pkill`, `chmod`, `chown`, and disk-management commands.
- Do not blindly copy commands from the internet.
- Understand a command before executing it.
- Test destructive commands in a virtual machine first.
- Keep backups before major system changes.
- Only scan systems you own or have permission to test.
- Be careful when changing SSH or firewall settings.
- Verify paths before running commands with elevated privileges.
- Prefer testing potentially destructive commands without `sudo` first when possible.

---

# 18. Safe Practice Commands

These commands are generally useful for practicing basic system inspection:

```bash
pwd
ls -lh
free -h
df -h
du -sh .
ps aux | head
ip -br a
ss -tuln
systemctl --failed
```

---

## 🚀 Suggested Practice

Try answering these questions using only the commands in this guide:

1. What directory am I currently in?
2. How much RAM is available?
3. How much disk space is free?
4. Which processes are currently running?
5. Which ports are listening?
6. Which services have failed?
7. What is my current IP address?
8. Which files in `/var/log` are larger than 100 MB?
9. Which users are currently logged in?
10. What errors occurred during the current boot?

---

## ⚠️ Disclaimer

This reference is intended for **learning and authorized system administration**.

Always verify commands before executing them, especially commands involving:

- `sudo`
- Filesystem and disk operations
- Firewall configuration
- User management
- Process termination
- File permissions
- Remote systems

Only perform network scanning, testing, or administration on systems you own or have explicit permission to manage.

---

## 🐧 Happy Linux Learning!

**Linux · SysAdmin · Networking · DevOps**