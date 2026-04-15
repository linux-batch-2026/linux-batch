# 🧑‍💻 Linux Commands Guide

This guide covers essential Linux commands every beginner and intermediate user should know. It is divided into three main sections:

1. ✅ Basic Linux Commands  
2. 🔍 Commands to View System Information  
3. 📘 Getting Help with Commands  

---

## ✅ 1. Basic Linux Commands

These are the most commonly used commands for navigation, file manipulation, and managing the Linux environment.

| Command | Description |
|--------|-------------|
| `pwd` | Prints the current working directory |
| `ls` | Lists files and directories |
| `cd` | Changes the current directory |
| `touch` | Creates an empty file |
| `mkdir` | Creates a new directory |
| `rm -rf` | Deletes files and directories |
| `cp` | Copies files and directories |
| `mv` | Moves or renames files and directories |
| `echo` | Displays a line of text or variable value |
| `cat` | Displays contents of a file |
| `nano`, `vim` | Opens text editors in the terminal |
| `clear` | Clears the terminal screen |
| `history` | Shows previously executed commands |
| `exit` | Exits the terminal session |
| `date` | Displays the current date and time |
| `whoami` | Prints the currently logged-in user |
| `uname` | Shows system information (basic) |

---

## 🔍 2. Commands to View System Information

These commands help you check system hardware, kernel, memory, disk usage, and more.

### 🔧 Hardware & Kernel Info

| Command | Description |
|--------|-------------|
| `uname -a` | Detailed kernel and system architecture info |
| `hostname` | Displays the system's hostname |
| `arch` | Shows machine architecture |
| `lscpu` | Displays CPU architecture info |
| `lsblk` | Lists block devices (disks, partitions) |
| `lspci` | Lists PCI devices |
| `lsusb` | Lists USB devices |
| `dmidecode` | Displays BIOS and hardware details |

> ⚠️ `lspci`, `lsusb`, and `dmidecode` may require `sudo`.

---

### 💾 Memory, Disk & Storage

| Command | Description |
|--------|-------------|
| `free -h` | Shows RAM usage in a human-readable format |
| `df -h` | Shows disk space usage |
| `du -sh /path` | Shows size of a specific directory |
| `top` | Displays running processes in real-time |
| `htop` | Advanced process viewer (if installed) |
| `vmstat` | Displays memory, swap, and I/O info |

---

### 🌐 Network & Users

| Command | Description |
|--------|-------------|
| `ifconfig` or `ip a` | Displays IP addresses |
| `ping google.com` | Tests internet connectivity |
| `netstat -tulnp` | Shows network connections (needs `sudo`) |
| `who` | Shows who is logged in |
| `uptime` | Shows how long the system has been running |
| `users` | Displays currently logged-in users |

---

## 📘 3. Getting Help with Commands

Linux has built-in tools to help you understand how commands work, including their options and usage.

| Command | Description |
|--------|-------------|
| `man <command>` | Opens the manual page for a command |
| `command --help` | Shows a brief help guide for a command |
| `info <command>` | Displays a detailed info page (where available) |
| `whatis <command>` | Gives a one-line description of the command |
| `apropos <keyword>` | Finds all commands related to a keyword |

### 📝 Examples

```bash
man ls          # Opens the manual for 'ls'
ls --help       # Quick summary of 'ls' usage
whatis grep     # Description of 'grep'
apropos copy    # Lists commands related to copying
