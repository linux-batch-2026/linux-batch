# Linux File Management System Hierarchy

The Linux operating system follows a **hierarchical directory structure** that looks like an inverted tree. At the top is the **root directory `/`**, and all other files and directories branch out from it.

---

## 📂 Root Directory (`/`)

* The starting point of the filesystem.
* Every single file and directory starts from `/`.
* Only the root user has full permission here.

---

## 🔑 Important Directories under `/`

### 1. `/bin`

* Stands for **binary**.
* Contains essential user command binaries (like `ls`, `cp`, `mv`, `cat`).
* Needed for system booting and single-user mode.

### 2. `/sbin`

* Contains **system binaries**.
* Commands for system administration (e.g., `reboot`, `shutdown`, `fdisk`).

### 3. `/etc`

* Contains **system configuration files**.
* Examples: `passwd`, `hosts`, `fstab`.

### 4. `/dev`

* Stores **device files** (hardware access).
* Example: `/dev/sda` (hard disk), `/dev/tty` (terminals).

### 5. `/proc`

* Virtual filesystem containing **process and system information**.
* Example: `/proc/cpuinfo`, `/proc/meminfo`.

### 6. `/var`

* Variable data files.
* Logs (`/var/log`), spools, cache, lock files.

### 7. `/tmp`

* Temporary files.
* Cleared on reboot.

### 8. `/usr`

* User-related programs and data.
* Subdirectories:

  * `/usr/bin` → Non-essential user commands.
  * `/usr/sbin` → Non-essential system binaries.
  * `/usr/lib` → Libraries.
  * `/usr/share` → Shared data.

### 9. `/home`

* Home directories for users.
* Example: `/home/vaibhav`.

### 10. `/root`

* Home directory for the **root user**.

### 11. `/lib`

* Shared **libraries** needed by binaries in `/bin` and `/sbin`.

### 12. `/boot`

* Files required for booting Linux.
* Example: `vmlinuz` (kernel), `grub` (bootloader).

### 13. `/opt`

* Optional or third-party software packages.

### 14. `/mnt`

* Temporary mount point for filesystems.

### 15. `/media`

* Mount point for removable devices (USB, CD-ROM).

### 16. `/srv`

* Data for services (FTP, HTTP, etc.).

---

## 🗂 Filesystem Hierarchy Example

```
/
├── bin
├── boot
├── dev
├── etc
├── home
│   ├── user1
│   └── user2
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── sbin
├── srv
├── tmp
├── usr
│   ├── bin
│   ├── lib
│   └── share
└── var
```

---

## 📌 Key Points

* Linux filesystem is a **single tree structure** starting at `/`.
* Every device or partition is **mounted** into this tree.
* Configuration files are under `/etc`, user data in `/home`, executables in `/bin` & `/usr/bin`.
* `/proc` and `/sys` are **virtual filesystems** providing runtime system information.

---


