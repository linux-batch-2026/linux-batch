
# 🔐 Linux File System Security & Permissions

Linux File System Security restricts users from accessing files and directories without proper permissions. Users require permissions to access files or directories.  
The `ls -l` or `ll` command can be used to check the security of any file or directory. These commands display contents of a directory along with security details.

---

## Checking File and Directory Permissions

Example:  

```bash
[root@ip-172-31-19-5 ~]# ll /root
total 8
-rw-------. 1 root root 6577 Aug 20 2025 pune.txt
````

To check the security of a directory:

```bash
[root@ip-172-31-19-5 ~]# ll -d /root
dr-xr-x---. 3 root root 181 Aug 5 10:46 /root
```

<img width="872" height="167" alt="image" src="https://github.com/user-attachments/assets/b2e12130-7974-431b-b5bf-1748389a3840" />



---

## File Permission Fields

The output of `ll` contains **10 fields**:

1. **File type**
2. **Owner Permissions**
3. **Group Permissions**
4. **Other User Permissions**
5. **Link Count**
6. **Owner of file/directory**
7. **Group owner of file/directory**
8. **File Size**
9. **Creation Date and Time**
10. **File/Directory Name**

---

## File Types in Linux

There are **seven types** of files in Linux:

| File Type             | Symbol | Example          |
| --------------------- | ------ | ---------------- |
| Normal/Regular File   | `-`    | `/etc/passwd`    |
| Directory             | `d`    | `/home`          |
| Link File             | `l`    | `/etc/grub.conf` |
| Block Device File     | `b`    | `/dev/vdb`       |
| Character Device File | `c`    | `/dev/pts/0`     |
| Socket File           | `s`    | `/dev/log`       |
| Named Pipe File       | `p`    | `/dev/initctl`   |

### Description:

* **Regular File**: Most common file type (text, images, binaries, libraries, etc.).
* **Directory**: Stores other files, created using `mkdir`.
* **Character Device File**: Communicates with devices (keyboard, mouse, etc.).
* **Block Device File**: Used for hardware like hard drives and memory.
* **Socket File**: Used for communication between processes (e.g., syslog, X Windows).
* **Named Pipe**: Communication between processes, created using `mknod`.
* **Symbolic Link**: Acts as a pointer to an original file.

---

## Link Count

* **Reference Count** = number of links to a file/directory.
* **Default Link Count**:

  * File → `1`
  * Directory → `2`

When a new directory is created, the parent directory’s link count increases by `1`.

---

## Hard Link vs Soft Link

| Feature                 | Hard Link                                    | Soft Link (Symbolic Link)              |
| ----------------------- | -------------------------------------------- | -------------------------------------- |
| **Inode Number**        | Same as original file                        | Different from original file           |
| **Content**             | Contains actual data                         | Contains path to original file         |
| **Size**                | Same as original file                        | Depends on path length                 |
| **Link Count Effect**   | Increases/decreases link count               | Does not affect link count             |
| **File Removal Effect** | Removing original file keeps hardlink intact | Removing original file breaks softlink |
| **Directory Support**   | Cannot create hardlink for directory         | Can create softlink for directory      |

### Syntax

```bash
# ln <original_file> <hardlink_name>      # Create hardlink
# ln -s <original_file> <softlink_name>   # Create softlink
```

### Example

```bash
[root@ip-172-31-19-5 ~]# touch hard.txt
[root@ip-172-31-19-5 ~]# ln hard.txt hardlink
[root@ip-172-31-19-5 ~]# touch soft.txt
[root@ip-172-31-19-5 ~]# ln -s soft.txt softlink
[root@ip-172-31-19-5 ~]# ll

total 4
-rw-r--r--. 2 root root 817 Aug 24 18:26 hardlink
lrwxrwxrwx. 1 root root 21 Aug 24 18:26 softlink -> soft.txt
```

---

## User and Group Ownership

* By default, the **user who creates a file/directory is the owner**.
* The **primary group of the user becomes the group owner**.
* Ownership is shown in the **6th and 7th fields** of the `ll` command output.

### Commands

```bash
# chown <user_name>:<group_name> <file/dir_name>   # Change owner and group
# chgrp <group_name> <file/dir_name>               # Change group ownership
```

### Examples

#### Change User Ownership

```bash
[root@server ~]# touch samplefile.txt
[root@server ~]# ll
-rw-r--r--. 1 root root 0 Aug 15 08:56 samplefile.txt

[root@server ~]# chown mahesh samplefile.txt
[root@server ~]# ll
-rw-r--r--. 1 mahesh root 0 Aug 15 08:57 samplefile.txt
```

#### Change Group Ownership

```bash
[root@server ~]# chgrp nagpur samplefile.txt
[root@server ~]# ll
-rw-r--r--. 1 mahesh nagpur 0 Aug 29 08:57 samplefile.txt
```

#### Change User and Group Ownership Together

```bash
[root@server ~]# chown vaihav:TCS samplefile.txt
[root@server ~]# ll
-rw-r--r--. 1 vaibhav TCS 0 Aug 15 08:57 samplefile.txt
```
---
# Managing Permissions in Linux

In Linux, file and directory access is controlled using permissions. The 2nd, 3rd, and 4th fields of file attributes represent permissions for:
- **Owner**
- **Group owner**
- **Other users**

Each field contains three basic permissions:
- **Read (r)**
- **Write (w)**
- **Execute (x)**

The effect of these permissions differs for files and directories.

---

## File and Directory Permissions

| Permission | Applied to Files | Applied to Directories | Symbol (Letter) | Number |
|------------|------------------|-------------------------|-----------------|--------|
| **Read**   | Open a file      | List contents of directory | `r` | 4 |
| **Write**  | Change contents of a file | Create, delete, and modify permissions on files | `w` | 2 |
| **Execute**| Run a program file | Change to the directory | `x` | 1 |

---

## Changing Permissions Using Symbols

**Syntax:**
```bash
chmod <u,g,o><+,-,=><r,w,x> <file_name>
````

**Symbols:**

| Symbol | Description            |
| ------ | ---------------------- |
| `u`    | Owner permission       |
| `g`    | Group permission       |
| `o`    | Other users permission |
| `+`    | Add permission         |
| `-`    | Remove permission      |
| `=`    | Assign permission      |
| `r`    | Read permission        |
| `w`    | Write permission       |
| `x`    | Execute permission     |

---

### Examples

**1. Give write permission to group**

```bash
mkdir /pune
chmod g+w /pune/
ls -ld /pune/
drwxrwxr-x. 2 root root 6 Aug 15 06:14 /pune/
```

**2. Remove read and execute permission for other users**

```bash
chmod o-rx /pune/
ls -ld /pune
drwxrwx---. 2 root root 6 Aug 15 06:14 /pune
```

**3. Assign read-only permission for group and other users**

```bash
chmod go=r /pune/
ls -ld /pune
drwxr--r--. 2 root root 6 Aug 15 06:14 /pune
```

**4. Give execute permission to owner of a file**

```bash
touch samplefile3.txt
chmod u+rwx samplefile3.txt
ll
-rwxr--r--. 1 root root 0 Aug 15 09:29 samplefile3.txt
```

**5. Remove read permission for group and assign read/write to others**

```bash
chmod g-r,o=rw samplefile3.txt
ls -l samplefile3.txt
-rwx---rw-. 1 root root 0 Aug 15 09:29 samplefile3.txt
```

---

## Changing Permissions Using Octal Numbers

**Syntax:**

```bash
chmod <permission_in_numbers> <file_name>
```

### Octal Permission Representation

| Octal No | Binary | Permission |
| -------- | ------ | ---------- |
| 0        | 000    | ---        |
| 1        | 001    | --x        |
| 2        | 010    | -w-        |
| 3        | 011    | -wx        |
| 4        | 100    | r--        |
| 5        | 101    | r-x        |
| 6        | 110    | rw-        |
| 7        | 111    | rwx        |

---

### Examples

**1. Apply octal permission 421**

```bash
mkdir /roshan
chmod 421 /roshan/
ls -ld /roshan/
dr---w---x. 2 root root 6 Aug 15 07:10 /roshan/
```

**2. Apply octal permission 732**

```bash
chmod 732 /roshan/
ls -ld /roshan/
drwx-wx-w-. 2 root root 6 Aug 15 07:10 /roshan/
```

**3. Apply octal permission 644**

```bash
chmod 644 /roshan/
ls -ld /roshan/
drw-r--r--. 2 root root 6 Aug 15 07:10 /roshan/
```

**4. Apply octal permission 755**

```bash
chmod 755 /roshan/
ls -ld /roshan/
drwxr-xr-x. 2 root root 6 Aug 15 07:10 /roshan/
```

---


# Default Permissions and Umask in Linux

## Default Permissions
When a user creates a file or directory in Linux, default permissions are assigned based on whether the user is **root** or a **standard user**. These default values are determined by the `umask`.

- **File (by default fully open: 666)**
- **Directory (by default fully open: 777)**

### Default Permissions for Root and Standard User

| User           | Directory | File |
|----------------|-----------|------|
| Root           | 755       | 644  |
| Standard User  | 775       | 664  |

---

## Calculating Permission with Umask

The **umask value masks** what is considered to be fully opened permissions.

- **For Directory** → 777 - umask  
- **For File** → 666 - umask  

### Example Calculation

| USER      | Type | Calculation | Permission |
|-----------|------|-------------|------------|
| Root      | Dir  | 777 - 022   | 755        |
| Root      | File | 666 - 022   | 644        |
| Standard  | Dir  | 777 - 002   | 775        |
| Standard  | File | 666 - 002   | 664        |

---

## Checking Default Umask

```bash
# Default umask for root user
[root@linux ~]# umask
0022

# Umask for standard user
[student@linux ~]$ umask
0002
````

---

## Changing Umask Value

### Temporary Change

```bash
[root@linux ~]# umask 000
[root@linux ~]# mkdir demo
[root@linux ~]# ll
drwxrwxrwx. 2 root root 6 Aug 15 12:34 demo
```

This change lasts until the session ends.

---

### Permanent Change

To make umask changes permanent, update `/etc/profile`.

```bash
[root@linux ~]# vim /etc/profile

59 if [ $UID -gt 199 ] && [ "`/usr/bin/id -gn`" = "`/usr/bin/id -un`" ]; then
60     umask 002   # change value for standard user (line 60)
61 else
62     umask 000   # change value for root (line 62)
63 fi

:wq
```

Reload profile and verify:

```bash
[root@linux ~]# source /etc/profile
[root@linux ~]# umask
0000
```

---

# ⭐ Special Permissions

In Linux, apart from the basic file permissions (read, write, execute), there are **three types of special permissions**:

- **SUID (Set User ID)**
- **SGID (Set Group ID)**
- **Sticky Bit**

---

## Permission Table

| Name       | Numeric Value | Relative Value | On Files                                         | Symbol |
|------------|--------------|----------------|-------------------------------------------------|--------|
| **SUID**   | 4            | `u+s`          | User executes file with permissions of file owner | `s`    |
| **SGID**   | 2            | `g+s`          | User executes file with permissions of group owner. Files created in directory get the same group owner. | `s`    |
| **Sticky Bit** | 1        | `o+t`          | Prevents users from deleting files of other users in a shared directory | `t`    |

---

## 1. SUID (Set User ID)

SUID is a special type of file permission given to a file. Normally in Linux/UNIX, when a program runs, it inherits access permissions from the logged-in user.  

With SUID enabled, a user can run the file **with the permissions of the file owner** (usually root).  

👉 In simple words: Users get the file owner’s permissions temporarily when executing a file/program.

### Syntax
```bash
chmod u+s <file_name>
````

### Example

```bash
# As user (without SUID permission)
[shubham@server ~]$ dmidecode
Permission denied

# As root, apply SUID
[root@server ~]# chmod u+s /sbin/dmidecode
[root@server ~]# ls -l /sbin/dmidecode
-rwsr-xr-x 1 root root 110608 Aug 20 2025 /sbin/dmidecode

# Now any user can run it
[shubham@server ~]$ dmidecode
Getting SMBIOS data from sysfs...
```

---

## 2. SGID (Set Group ID)

SGID can be applied to **directories**. When SGID is set on a directory:

* Files created inside the directory automatically **inherit the group ownership** of the directory, instead of the user's primary group.

### Syntax

```bash
chmod g+s <directory_name>
```

### Example

```bash
# Create directory and set group
[root@server ~]# mkdir /demo
[root@server ~]# chgrp TCS /demo
[root@server ~]# ls -ld /demo
drwxr-xr-x 2 root TCS 6 Aug 12 05:55 /demo

# Apply SGID
[root@server ~]# chmod g+s /demo
[root@server ~]# ls -ld /demo
drwxr-sr-x 2 root TCS 31 Aug 12 05:57 /demo

# Now files inside inherit group TCS
[root@server ~]# touch /demo/file1
[root@server ~]# ls -l /demo
-rw-r--r-- 1 root TCS 0 Aug 12 05:57 file1
```

---

## 3. Sticky Bit

Sticky Bit is used on **directories** to prevent users from deleting other users’ files.

If Sticky Bit is set on a directory:

* Only the **owner of the file** and the **root user** can delete the file.
* Other users cannot delete files they don’t own.

This is commonly used in **`/tmp` directory**.

### Syntax

```bash
chmod o+t <directory_name>
```

### Example

```bash
# Create shared directory
[root@server ~]# mkdir /demo
[root@server ~]# chmod 777 /demo

# Apply Sticky Bit
[root@server ~]# chmod o+t /demo
[root@server ~]# ls -ld /demo
drwxrwxrwt 2 root root 6 Aug 12 05:55 /demo

# User1 creates a file
[shubham@server ~]$ touch /demo/file.txt

# Another user tries to delete it
[mahesh@server ~]$ rm -f /demo/file.txt
rm: cannot remove '/demo/file.txt': Operation not permitted
```

---

## 📜 ACL (Access Control List)



## Introduction
**Access Control List (ACL)** is used to set permissions over files and directories for specific users or groups.  
Unlike traditional UNIX permissions (owner, group, others), ACL provides **fine-grained access control** by allowing you to assign multiple users or groups different permissions on the same file or directory.

👉 **Use case**: Suppose a user is not part of a group that owns a file, but you still want to give them read or write permissions. Instead of changing group ownership, you can use ACL.

---

## Commands

- **Set ACL (user)**  

```bash
  setfacl -m u:<username>:<permissions> <file/directory>
```

---


* **Set ACL (group)**

  ```bash
  setfacl -m g:<groupname>:<permissions> <file/directory>
  ```

  ---

  
* **Check ACL**

  ```bash
  getfacl <file/directory>
  ```

---

## Examples

### 1. User Perspective

```bash
# Create directory
mkdir /project
ll -d /project
# Output:
# drwxr-xr-x 2 root root 6 Aug 12 05:55 /project

# Create users
useradd amit
useradd sumit

# Apply ACL for user 'amit'
setfacl -m u:amit:rwx /project
getfacl /project

# Switch to user 'amit'
su - amit
touch /project/amit.txt   # ✅ Successfully creates file
exit

# Apply ACL for user 'sumit'
setfacl -m u:sumit:r-- /project
su - sumit
cd /project               # ❌ Permission denied
```

---

### 2. Group Perspective

```bash
# Create groups
groupadd TCS
groupadd WIPRO

# Create users and add them to groups
useradd -G TCS T1
useradd -G TCS T2
useradd -G WIPRO W1
useradd -G WIPRO W2
useradd -G WIPRO W3

# Check directory
ll -ld /project
# drwxr-xr-x 2 root root 6 Aug 12 05:55 /project

# Apply ACL for groups
setfacl -m g:TCS:rwx /project
setfacl -m g:WIPRO:--- /project

# Apply ACL for a specific user inside WIPRO group
setfacl -m u:W3:rwx /project
```

👉 In this example, the **WIPRO group** has no permissions, but **user `W3`** (member of WIPRO) still has **rwx** access due to ACL.

---

### 3. Copy ACL from One File to Another

```bash
# Create a new file
touch /abc.txt
getfacl /abc.txt

# Copy ACL from /project to /abc.txt
getfacl /project | setfacl --set-file=- /abc.txt

# Verify
getfacl /abc.txt
```

---

### 4. Remove ACL

* **Remove single user ACL**

  ```bash
  setfacl -x u:amit /project
  ```
* **Remove multiple users ACL**

  ```bash
  setfacl -x u:sumit,u:W3 /project
  ```
* **Remove single group ACL**

  ```bash
  setfacl -x g:IBM /project
  ```
* **Remove multiple groups ACL**

  ```bash
  setfacl -x g:WIPRO,g:TCS /project
  ```
* **Remove all ACL entries**

  ```bash
  setfacl -b /abc.txt
  ```

---


# 🛡️ SUDO Permissions

The **`sudo` (Super User DO)** command in Linux is generally used as a prefix to run commands that only the superuser is allowed to execute.  
When you prefix `sudo` with any command, it will run that command with **elevated privileges**, allowing a user with proper permissions to execute a command as another user, such as the superuser.  

This is the Linux equivalent of the **“Run as Administrator”** option in Windows.  
The option of `sudo` lets us have **multiple administrators** in the system.

---

## Requirements for Using `sudo`

- A user must be listed in the **`/etc/sudoers`** file.  
- Alternatively, the user should belong to the **wheel group**, which is the default group that allows users to use `sudo`.

---

## Syntax

```bash
sudo <command_line>
````

---

## Example

```bash
[root@ip-172-31-19-21 ~]# su – amit  

[amit@ip-172-31-19-21 ~]$ useradd shubham  
-bash: /usr/sbin/useradd: Permission denied  

[amit@ip-172-31-19-21 ~]$ sudo useradd shubham  
```
---
