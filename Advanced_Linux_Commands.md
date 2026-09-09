# 🐧 Advanced Linux Commands Reference

A beginner-friendly reference for **Linux administration, troubleshooting, networking, storage, security, and DevOps**.

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
- [11. Logs & Troubleshooting](#11-Logs--Troubleshooting)
- [12. Date, Time & Scheduling](#12-date-time--scheduling)
- [13. Docker Basics](#13-docker-basics)
- [14. Compression & Archiving](#14-Compression--Archiving)
- [15. Permissions & Ownership](#15-Permissions--Ownership)
- [16. Useful System Information](#16-Useful-System-Information)
- [17. Safety Tips](#17-safety-tips)
- [18. Safe Practice Commands](#18-safe-practice-commands)

## 1. Advanced File & Text Commands

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `find /var/log -type f -size +100M -exec ls -lh {} \;` | Find files larger than 100 MB |
| `find / -type f -perm /4000 2>/dev/null` | Find files with SUID permission |
| `find / -type f -perm /2000 2>/dev/null` | Find files with SGID permission |
| `find . -type f -name "*.log" -mtime +30` | Find log files older than 30 days |
| `find . -type f -empty` | Find empty files |
| `find . -type d -empty` | Find empty directories |
| `grep -Rni "error" /var/log` | Search for "error" in logs |
| `grep -v "^#" /etc/ssh/sshd_config` | Show non-comment configuration lines |
| `grep -E "error|failed|warning" file.log` | Search for multiple patterns |
| `awk '{print $1}' access.log` | Print the first column |
| `awk '{print $NF}' file.txt` | Print the last column |
| `awk '$3 > 80 {print}' file.txt` | Show rows where column 3 is greater than 80 |
| `sed -n '1,20p' file.txt` | Show lines 1–20 |
| `sed -i 's/old/new/g' file.txt` | Replace text in a file |
| `sort file.txt | uniq -c` | Count duplicate lines |
| `cut -d: -f1 /etc/passwd` | Show usernames from `/etc/passwd` |
| `tr 'a-z' 'A-Z' < file.txt` | Convert lowercase text to uppercase |
| `xargs -n1 echo < file.txt` | Run a command for each input item |
| `diff file1.txt file2.txt` | Compare two files |
| `comm file1.txt file2.txt` | Compare sorted files line by line |

---

## 2. Advanced Process Management

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `ps aux --sort=-%cpu` | Show processes using the most CPU |
| `ps aux --sort=-%mem` | Show processes using the most memory |
| `ps -eo pid,ppid,cmd,%cpu,%mem --sort=-%cpu` | Show detailed processes sorted by CPU |
| `pgrep nginx` | Find the PID of nginx |
| `pkill nginx` | Stop processes by name |
| `pkill -9 nginx` | Force-kill processes by name |
| `kill 1234` | Stop process with PID 1234 |
| `kill -9 1234` | Force-kill a process |
| `renice 10 -p 1234` | Change process priority |
| `nice -n 10 command` | Start a command with lower priority |
| `jobs -l` | Show background jobs with PIDs |
| `bg %1` | Continue job 1 in background |
| `fg %1` | Bring job 1 to foreground |
| `nohup command &` | Keep a command running after logout |
| `watch -n 2 'ps aux --sort=-%cpu | head'` | Continuously monitor CPU-heavy processes |
| `pstree -p` | Show processes as a tree |
| `strace -p 1234` | Trace system calls of a process |
| `lsof -p 1234` | Show files opened by a process |
| `lsof -i :8080` | Find which process uses port 8080 |

---

## 3. Memory & CPU

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `free -h` | Show RAM and swap usage |
| `vmstat 2` | Monitor CPU, memory, and processes |
| `mpstat -P ALL 2` | Monitor CPU usage per core |
| `top` | Live process and resource monitor |
| `htop` | Interactive process monitor |
| `uptime` | Show system uptime and load |
| `nproc` | Show number of CPU cores |
| `lscpu` | Show CPU information |
| `cat /proc/cpuinfo` | Show detailed CPU information |
| `cat /proc/meminfo` | Show detailed memory information |
| `numactl --hardware` | Show NUMA hardware information |
| `dstat` | Monitor CPU, memory, disk, and network |
| `sar -u 2 5` | Monitor CPU usage |
| `sar -r 2 5` | Monitor memory usage |

---

## 4. Advanced Disk Commands

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `lsblk` | Show disks and partitions |
| `lsblk -f` | Show disks with filesystem information |
| `fdisk -l /dev/sda` | Show partition information for a disk |
| `blkid` | Show filesystem UUIDs and types |
| `df -hT` | Show disk usage and filesystem types |
| `du -sh *` | Show size of files and directories |
| `du -ah /var | sort -h | tail` | Find the largest files/directories |
| `ncdu /` | Interactive disk usage analyzer |
| `mount` | Show mounted filesystems |
| `findmnt` | Show mounted filesystem hierarchy |
| `mount /dev/sdb1 /mnt` | Mount a filesystem |
| `umount /mnt` | Unmount a filesystem |
| `sync` | Write cached data to disk |
| `iostat -xz 2` | Monitor disk I/O performance |
| `iotop` | Show processes doing disk I/O |
| `smartctl -a /dev/sda` | Show disk health information |
| `fsck /dev/sdb1` | Check and repair a filesystem |
| `tune2fs -l /dev/sda1` | Show ext filesystem information |

---

## 5. Advanced Networking

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `ip addr` | Show IP addresses |
| `ip link` | Show network interfaces |
| `ip route` | Show routing table |
| `ip neigh` | Show ARP/neighbour information |
| `ss -tulpn` | Show listening network ports |
| `ss -s` | Show network socket statistics |
| `lsof -i` | Show network connections |
| `curl -I https://example.com` | Show HTTP headers |
| `curl -v https://example.com` | Show detailed HTTP connection information |
| `wget -c URL` | Download and continue an interrupted download |
| `dig example.com` | Look up DNS information |
| `nslookup example.com` | Query DNS information |
| `host example.com` | Perform a simple DNS lookup |
| `traceroute example.com` | Show the network path to a host |
| `ping -c 4 example.com` | Send four ping requests |
| `mtr example.com` | Continuously test network path and latency |
| `nmap -sS -p 1-1000 example.com` | Scan ports 1–1000 on a host |
| `tcpdump -i eth0` | Capture network packets |
| `tcpdump -i eth0 port 80` | Capture HTTP traffic |
| `ethtool eth0` | Show network card information |
| `nmcli device status` | Show NetworkManager devices |

> ⚠️ Only scan or capture traffic on systems/networks you own or are authorized to test.

---

## 6. Firewall

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `ufw status` | Show firewall status |
| `ufw enable` | Enable UFW firewall |
| `ufw disable` | Disable UFW firewall |
| `ufw allow 22/tcp` | Allow SSH traffic |
| `ufw allow 80/tcp` | Allow HTTP traffic |
| `ufw deny 23/tcp` | Block Telnet traffic |
| `ufw delete allow 80/tcp` | Remove an allow rule |
| `iptables -L -n -v` | Show iptables rules |
| `iptables -S` | Show iptables rules as commands |
| `nft list ruleset` | Show nftables firewall rules |

---

## 7. SSH & Remote Administration

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `ssh user@server` | Connect to a remote server |
| `ssh -p 2222 user@server` | Connect using a custom SSH port |
| `ssh -i key.pem user@server` | Connect using an SSH private key |
| `scp file.txt user@server:/tmp/` | Copy a file to a server |
| `scp user@server:/tmp/file.txt .` | Copy a file from a server |
| `rsync -av file/ user@server:/backup/` | Sync files to a server |
| `rsync -av --delete source/ destination/` | Sync and remove deleted files |
| `ssh-keygen -t ed25519` | Generate an SSH key |
| `ssh-copy-id user@server` | Copy your SSH key to a server |
| `ssh-add ~/.ssh/id_ed25519` | Add an SSH key to the agent |
| `ssh -L 8080:localhost:80 user@server` | Create an SSH local port tunnel |
| `ssh -R 8080:localhost:80 user@server` | Create an SSH reverse tunnel |
| `sftp user@server` | Transfer files securely over SSH |

---

## 8. Package Management

### Debian / Ubuntu

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `apt update` | Refresh package information |
| `apt upgrade` | Upgrade installed packages |
| `apt install package` | Install a package |
| `apt remove package` | Remove a package |
| `apt purge package` | Remove package and configuration |
| `apt search package` | Search for a package |
| `apt show package` | Show package information |
| `dpkg -l` | List installed packages |
| `dpkg -S /path/to/file` | Find which package owns a file |

### RHEL / Fedora

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `dnf check-update` | Check for available updates |
| `dnf upgrade` | Upgrade packages |
| `dnf install package` | Install a package |
| `dnf remove package` | Remove a package |
| `dnf search package` | Search for packages |
| `rpm -qa` | List installed RPM packages |
| `rpm -qf /path/to/file` | Find which package owns a file |

---

## 9. Systemd & Services

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `systemctl status nginx` | Check nginx service status |
| `systemctl start nginx` | Start nginx |
| `systemctl stop nginx` | Stop nginx |
| `systemctl restart nginx` | Restart nginx |
| `systemctl reload nginx` | Reload nginx configuration |
| `systemctl enable nginx` | Start nginx automatically at boot |
| `systemctl disable nginx` | Disable automatic startup |
| `systemctl is-active nginx` | Check if a service is running |
| `systemctl is-enabled nginx` | Check if a service starts at boot |
| `systemctl list-units --type=service` | List active services |
| `systemctl list-unit-files --type=service` | List installed service definitions |
| `journalctl -u nginx` | Show nginx logs |
| `journalctl -u nginx -f` | Follow nginx logs live |
| `journalctl -b` | Show logs from current boot |
| `journalctl -p err -b` | Show errors from current boot |
| `systemctl daemon-reload` | Reload systemd configuration |

---

## 10. Users & Groups

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `whoami` | Show current username |
| `id` | Show user and group IDs |
| `who` | Show logged-in users |
| `w` | Show logged-in users and what they are doing |
| `last` | Show previous logins |
| `lastlog` | Show last login for each user |
| `useradd username` | Create a user |
| `usermod -aG group username` | Add user to a group |
| `userdel username` | Delete a user |
| `passwd username` | Change a user's password |
| `groupadd developers` | Create a group |
| `groupdel developers` | Delete a group |
| `groups username` | Show a user's groups |
| `getent passwd` | List system users |
| `getent group` | List system groups |
| `chage -l username` | Show password expiration information |

---

## 11. Logs & Troubleshooting

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `dmesg -T | tail -50` | Show the latest kernel messages |
| `journalctl -xe` | Show detailed recent system errors |
| `journalctl -f` | Follow system logs live |
| `journalctl --since "1 hour ago"` | Show logs from the last hour |
| `journalctl -p warning` | Show warning and higher-priority logs |
| `journalctl -b -1` | Show logs from the previous boot |
| `tail -f /var/log/syslog` | Follow the system log |
| `tail -f /var/log/auth.log` | Follow authentication logs |
| `grep -i "failed" /var/log/auth.log` | Search failed authentication attempts |
| `lsof +L1` | Find open files that were deleted |
| `fuser -v /path` | Show processes using a file or filesystem |
| `fuser -n tcp 8080` | Find the process using TCP port 8080 |
| `strace command` | Trace system calls made by a command |
| `strace -p 1234` | Trace an existing process |
| `dmesg | grep -i error` | Search kernel messages for errors |

---

## 12. Date, Time & Scheduling

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `date` | Show current date and time |
| `timedatectl` | Show system time settings |
| `timedatectl status` | Show time and timezone status |
| `timedatectl set-timezone Asia/Kolkata` | Set the system timezone |
| `hwclock` | Show hardware clock |
| `cal` | Show a calendar |
| `crontab -e` | Edit scheduled cron jobs |
| `crontab -l` | List cron jobs |
| `at 10:00` | Schedule a one-time command |
| `atq` | List scheduled `at` jobs |
| `atrm 1` | Remove an `at` job |
| `sleep 60` | Wait for 60 seconds |
| `watch -n 5 command` | Run a command repeatedly |

---

## 13. Docker Basics

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `docker ps` | Show running containers |
| `docker ps -a` | Show all containers |
| `docker images` | List Docker images |
| `docker pull nginx` | Download an image |
| `docker run nginx` | Start a container |
| `docker run -d nginx` | Start a container in background |
| `docker run -p 8080:80 nginx` | Map host port 8080 to container port 80 |
| `docker stop container` | Stop a container |
| `docker start container` | Start a stopped container |
| `docker restart container` | Restart a container |
| `docker rm container` | Remove a container |
| `docker rmi image` | Remove an image |
| `docker logs container` | Show container logs |
| `docker logs -f container` | Follow container logs |
| `docker exec -it container bash` | Open a shell inside a container |
| `docker inspect container` | Show detailed container information |
| `docker stats` | Show container resource usage |
| `docker system df` | Show Docker disk usage |
| `docker system prune` | Remove unused Docker resources |

---

## 14. Compression & Archiving

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `tar -czf backup.tar.gz folder/` | Create a gzip-compressed archive |
| `tar -xzf backup.tar.gz` | Extract a gzip archive |
| `tar -cjf backup.tar.bz2 folder/` | Create a bzip2 archive |
| `tar -xjf backup.tar.bz2` | Extract a bzip2 archive |
| `tar -cJf backup.tar.xz folder/` | Create an xz archive |
| `tar -xJf backup.tar.xz` | Extract an xz archive |
| `tar -tf backup.tar.gz` | List archive contents |
| `gzip file` | Compress a file |
| `gunzip file.gz` | Decompress a gzip file |
| `zip -r archive.zip folder/` | Create a ZIP archive |
| `unzip archive.zip` | Extract a ZIP archive |
| `zcat file.gz` | Read a compressed file without extracting it |

---

## 15. Permissions & Ownership

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `ls -l` | Show file permissions |
| `chmod 755 script.sh` | Give owner full access and others read/execute |
| `chmod 644 file.txt` | Give owner read/write and others read |
| `chmod +x script.sh` | Make a script executable |
| `chmod -R 755 directory/` | Change permissions recursively |
| `chown user file.txt` | Change file owner |
| `chown user:group file.txt` | Change owner and group |
| `chown -R user:group directory/` | Change ownership recursively |
| `chgrp developers file.txt` | Change file group |
| `umask` | Show default permission mask |
| `getfacl file.txt` | Show ACL permissions |
| `setfacl -m u:user:rwx file.txt` | Give a user specific ACL permissions |
| `lsattr file.txt` | Show special file attributes |
| `chattr +i file.txt` | Make a file immutable |

---

## 16. Useful System Information

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `uname -a` | Show kernel and system information |
| `hostnamectl` | Show hostname and OS information |
| `cat /etc/os-release` | Show Linux distribution information |
| `lshw` | Show hardware information |
| `lspci` | Show PCI devices |
| `lsusb` | Show USB devices |
| `lsmod` | Show loaded kernel modules |
| `modinfo module` | Show kernel module information |
| `sysctl -a` | Show kernel parameters |
| `dmesg` | Show kernel messages |
| `env` | Show environment variables |
| `printenv PATH` | Show a specific environment variable |
| `which command` | Show where a command is located |
| `type command` | Show what kind of command it is |
| `whereis command` | Find binary, source, and manual locations |

---

## 17. Shell & Command Utilities

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `history` | Show previously used commands |
| `history | grep ssh` | Search command history |
| `!!` | Run the previous command again |
| `sudo !!` | Run the previous command with sudo |
| `clear` | Clear the terminal |
| `alias ll='ls -lah'` | Create a shortcut for a command |
| `unalias ll` | Remove an alias |
| `command -v python` | Find which Python executable will run |
| `man command` | Open the manual for a command |
| `info command` | Open detailed command documentation |
| `help command` | Show Bash help for a built-in command |
| `echo $PATH` | Show the command search path |
| `source ~/.bashrc` | Reload Bash configuration |
| `export VAR=value` | Create an environment variable |
| `env VAR=value command` | Run a command with a temporary variable |

---

## 18. Important Safety Notes

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `rm -rf directory/` | ⚠️ Permanently delete a directory and its contents |
| `kill -9 PID` | ⚠️ Forcefully terminate a process |
| `pkill -9 name` | ⚠️ Forcefully terminate processes by name |
| `chmod -R ...` | ⚠️ Recursively change permissions |
| `chown -R ...` | ⚠️ Recursively change ownership |
| `fdisk` | ⚠️ Can modify disk partitions |
| `fsck` | ⚠️ Can modify filesystem structures |
| `iptables` / `nft` | ⚠️ Can change firewall rules |
| `dd` | ⚠️ Can overwrite disks or files if used incorrectly |
| `mkfs` | ⚠️ Creates a filesystem and can destroy existing data |

---

## 19. Quick Daily Commands

| **Command** | **Easy meaning** |
| ----------- | ---------------- |
| `pwd` | Show current directory |
| `ls -lah` | List all files with details |
| `cd /path` | Change directory |
| `mkdir folder` | Create a directory |
| `touch file.txt` | Create an empty file |
| `cp file1 file2` | Copy a file |
| `mv file1 file2` | Move or rename a file |
| `rm file.txt` | Delete a file |
| `cat file.txt` | Display a file |
| `less file.txt` | Read a file page by page |
| `head file.txt` | Show beginning of a file |
| `tail file.txt` | Show end of a file |
| `grep "text" file.txt` | Search for text |
| `find . -name "file.txt"` | Find a file |
| `df -h` | Check disk space |
| `free -h` | Check memory |
| `top` | Monitor processes |
| `ip addr` | Check IP addresses |
| `systemctl status service` | Check a service |
| `journalctl -xe` | Check recent system errors |

---

## 🐧 Happy Linux Learning!

**Linux · SysAdmin · Networking · DevOps**
