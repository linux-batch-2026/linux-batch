# Linux User and Group Management

Managing users and groups is an essential part of Linux system administration. It allows administrators to control access, security, and resource usage across the system.

---

## 👤 Users in Linux

A **user** represents an account that can log into the system and execute processes.

### Types of Users

1. **Super User (Root)**

   * UID = 0
   * Full administrative privileges.
   * Home directory: `/root`.
   * Use `sudo` for safer administration.

2. **System Users**

   * Created automatically by the system or applications.
   * Run background services (e.g., `mysql`, `www-data`).
   * Usually have no login shell.

3. **Standard Users**

   * Regular accounts for real people.
   * Limited privileges.
   * Home directory: `/home/username`.
---

## 📌 UID and GID

* **UID (User ID):** Unique ID for each user.

  * Root → UID 0
  * System users → UID 1–999
  * Standard users → UID 1000+
* **GID (Group ID):** Unique ID for each group.

---

## 📂 Important Files for User Management

* `/etc/passwd` → Stores user account information.
* `/etc/shadow` → Stores encrypted user passwords.
* `/etc/group` → Stores group information.
* `/etc/gshadow` → Secure group account information.

---


## 📂 Important Files

### 📌 `/etc/passwd`

* Stores user account information.
* Each line represents a user.
* Format:

  ```
  username:x:UID:GID:comment:home_directory:shell
  ```
* Example:

  ```
  vaibhav:x:1001:1001:This is linux batch:/home/vaibhav:/bin/bash
  ```

   ---

### 📌 `/etc/group`

* Stores group information.
* Format:

  ```
  group_name:x:GID:user_list
  ```
* Example:

  ```
  devops:x:1002:vaibhav,rahul
  ```

   ---

### 📌 `/etc/shadow`

* Stores encrypted user passwords and password policies.
* Only accessible by root.
* Format:

  ```
  username:encrypted_password:last_change:min:max:warn:inactive:expire
  ```
* Example:

  ```
  vaibhav:$6$Qk9as..:19344:0:99999:7:::
  ```

  ---
  

### 📌 `/etc/gshadow`

* Stores secure group information (encrypted passwords for groups).
* Format:

  ```
  group_name:password:admin_list:member_list
  ```
* Example:

  ```
  devops:!:vaibhav:rahul
  ```

---

## Skeleton Files (`/etc/skel`)

* Default files copied to a new user's home directory.
* Example:

  ```bash
  ls /etc/skel
  .bashrc  .profile  .bash_logout
  ```

  - `.bash_logout` => If this file is missing, user will unable to logout from the system.
  - `.bash_profile` => If this file is missing, home directory will not be assigned to the new user.
  - `.bashrc` => If this file is missing, user will unable to login to the system.

---

## Switching Between Users

### Switch User

```bash
su - vaibhav
```

### Switch to Root User

```bash
su -
sudo -i
```

---


## ➕ Adding a New User

* `useradd username` → Create a new user.
* `passwd username` → Assign password to user.
* `usermod -aG groupname username` → Add user to a group.
* `adduser username` (Debian/Ubuntu) → Interactive user creation.

---

# 🔐 Password Management  (`passwd` Command)

Password management in Linux is an essential part of **user and group administration**. It ensures system security by controlling how user passwords are created, stored, and maintained.

* `passwd username` → Change a user’s password.
* `passwd -e username` → Force password change on next login.
* `chage -l username` → View password aging policy.
* `chage -M 60 username` → Set password validity (60 days).

### View & Change Password Policy

* `cat /etc/login.defs` → View default password policy.
* `vim /etc/pam.d/common-password` → Configure password complexity rules.

---

The **password** is a secret phrase used to log in to the system.  
The `passwd` command is used to assign or change the password of any user.

- **Root user** can change the password of any user.
- **Local users** can change only their own password.
- Passwords are stored in `/etc/shadow` file in encrypted format.

---

## Password Rules
- Must be at least **8 characters long**  
- Should **not contain the username**  
- Cannot reuse the **old password**  
- **Dictionary words** are not allowed  
- Should not be **too simplistic**

---

## Syntax
```bash
# passwd             # Change current user's password
# passwd <username>  # Assign or change another user's password (root only)
````

---

## Examples

### 1. Changing root user’s password

```bash
[root@ip-172-31-19-5 ~]# passwd
Changing password for user root.
New password:
BAD PASSWORD: The password is shorter than 8 characters
Retype new password:
passwd: all authentication tokens updated successfully.
```

---

### 2. Changing a local user’s password by root

```bash
[root@ip-172-31-19-5 ~]# passwd vaibhav
Changing password for user vaibhav.
New password:
BAD PASSWORD: The password is shorter than 8 characters
Retype new password:
passwd: all authentication tokens updated successfully.
```

---

### 3. Changing current user’s password (self-change)

```bash
[vaibhav@ip-172-31-19-5 ~]$ passwd
Changing password for user vaibhav.
Changing password for vaibhav.
(current) UNIX password:
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```

---

### 4. Trying to change another user’s password (without root privilege)

```bash
[vaibhav@ip-172-31-19-5 ~]$ passwd ubuntu
passwd: Only root can specify a user name.
```

---

## Password Storage in `/etc/shadow`

Passwords are stored in encrypted format inside `/etc/shadow`.

Example:

```bash
[root@ip-172-31-19-5 ~]# tail -1 /etc/shadow
vaibhav:$6$S59rUkc4$iIusUTs6TPb2ueLMty3/2kvShejrTVctesfLYyUwTa78kDQQ/O/f954EuyomO6nBwwiPyqPt4hAij5OxiQIQ5.:18206:0:99999:7:::
```


---

## 📌 Key Files for Password Management

1. **`/etc/passwd`**

   * Stores basic user account information.
   * Password field is usually `x` (actual passwords are kept in `/etc/shadow`).
   * Example entry:

     ```
     vaibhav:x:1001:1001:this is linux batch:/home/vaibhav:/bin/bash
     ```
     
     ---

2. **`/etc/shadow`**

   * Stores **hashed passwords** and password aging information.

   * Only accessible by the root user.

   * Example entry:

     ```
     vaibhav:$6$2Wf...$abcd123:19453:0:90:7:14:19600:
     ```

   * Fields:

     * **Username**
     * **Encrypted Password**
     * **Last Password Change** (days since Jan 1, 1970)
     * **Min Days** (before password can be changed again)
     * **Max Days** (validity of password)
     * **Warning Days** (before expiration)
     * **Inactive Days** (after expiration)
     * **Expiration Date**
     * **For Future use**

3. **`/etc/login.defs`**

   * Contains **default password policy** and user account settings.
   * Example parameters:

     ```
     PASS_MAX_DAYS   90   # Max password age
     PASS_MIN_DAYS   0    # Min password age
     PASS_WARN_AGE   7    # Warn user before expiry
     ```

4. **`/etc/pam.d/`**

   * Contains **PAM (Pluggable Authentication Modules)** configurations for enforcing password complexity and authentication.
   * Example: `/etc/pam.d/common-password`

---



## 📌 Password Policies

### 1. Password Aging Policy (`/etc/login.defs`)

* **PASS\_MAX\_DAYS** → Maximum days password is valid.
* **PASS\_MIN\_DAYS** → Minimum days before user can change password.
* **PASS\_WARN\_AGE** → Warning days before password expires.

Example:

```bash
PASS_MAX_DAYS   90
PASS_MIN_DAYS   7
PASS_WARN_AGE   14
```

### 2. Password Complexity Policy (via PAM)

Edit `/etc/pam.d/common-password` (Debian/Ubuntu) or `/etc/pam.d/system-auth` (RHEL/CentOS).

Example rule:

```bash
password requisite pam_pwquality.so retry=3 minlen=8 ucredit=-1 lcredit=-1 dcredit=-1 ocredit=-1
```

* **minlen=8** → Minimum 8 characters
* **ucredit=-1** → At least 1 uppercase letter
* **lcredit=-1** → At least 1 lowercase letter
* **dcredit=-1** → At least 1 digit
* **ocredit=-1** → At least 1 special character

---

## 📌 Examples

# Password Policy Management using `chage`

The `chage` (**change age**) command is used to **view or modify the password policy** of a user in Linux.

---

## Syntax
```bash
chage <option> <parameter> <username>
````

---

## Options

| Option | Description                                       |
| ------ | ------------------------------------------------- |
| `-l`   | List / view password policy                       |
| `-m`   | Minimum days between password changes             |
| `-M`   | Maximum days between password changes             |
| `-W`   | Number of days of warning before password expires |
| `-I`   | Number of inactivation days after password expiry |
| `-E`   | Expiry date of user account                       |
| `-d`   | Force user to change password immediately         |

---

## Examples

### 1. View Password Policies

```bash
[root@server ~]# chage -l vaibhav
Last password change                                    : Aug 10, 2025
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 0
Maximum number of days between password change          : 99999
Number of days of warning before password expires       : 7
```

---

### 2. Change Minimum Age

```bash
[root@server ~]# chage -m 30 vaibhav
[vaibhav@server ~]$ chage -l vaibhav

Last password change                                    : Aug 10, 2025
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 30
Maximum number of days between password change          : 99999
Number of days of warning before password expires       : 7
```

---

### 3. Change Maximum Age

```bash
[root@server ~]# chage -M 45 vaibhav
[vaibhav@server ~]$ chage -l vaibhav

Last password change                                    : Aug 10, 2025
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 30
Maximum number of days between password change          : 45
Number of days of warning before password expires       : 7
```

---

### 4. Change Warning Days

```bash
[root@server ~]# chage -W 2 vaibhav
[vaibhav@server ~]$ chage -l vaibhav

Last password change                                    : Aug 10, 2025
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 30
Maximum number of days between password change          : 45
Number of days of warning before password expires       : 2
```

---

### 5. Change Expiry Date of User Account

```bash
[root@server ~]# chage -E "10 Oct 2025" vaibhav
[root@server ~]# su - vaibhav
[vaibhav@server ~]$ chage -l vaibhav

Last password change                                    : Aug 10, 2025
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : Oct 10, 2025
Minimum number of days between password change          : 30
Maximum number of days between password change          : 45
Number of days of warning before password expires       : 2
```

---

### 6. Force User to Change Password Immediately

```bash
[root@server ~]# chage -d 0 amit
[vaibhav@server ~]$ chage -l amit

Last password change                                    : password must be changed
Password expires                                        : password must be changed
Password inactive                                       : password must be changed
Account expires                                         : Oct 10, 2025
Minimum number of days between password change          : 30
Maximum number of days between password change          : 45
Number of days of warning before password expires       : 2
```

---


## 👥 Group Administration/Management

* `groupadd groupname` → Create a new group.
* `groupdel groupname` → Delete a group.
* `groups username` → Show groups for a user.
* `gpasswd -a username groupname` → Add user to group.
* `gpasswd -d username groupname` → Remove user from group.

---

1. **Primary Group**
   - Every user must belong to one **primary group**.
   - A user can only have **one primary group**.
   - When creating files, the **primary group** becomes the group owner of these files.
   - Primary group membership is defined in `/etc/passwd`.

2. **Secondary (or Supplementary) Groups**
   - Users can belong to one or more **secondary groups**.
   - Secondary groups are important for granting additional file access.
   - If the group a user belongs to has access to certain files, the user gains access as well.
   - Group membership is stored in the `/etc/group` file.

---

## 📌 `/etc/group` File
The `/etc/group` file contains all group-related information.  
Each line has four fields separated by colons (`:`):




1. **Group Name** → Name of the group.  
2. **Group Password (Optional)** → Rarely used nowadays. A temporary password could allow users to join groups.  
3. **Group ID (GID)** → Unique numeric ID assigned to the group.  
4. **List of Members** → Users who are members of the group as a **secondary group**.  

   - Users with this group as their **primary group** will not be listed here.

---

## Group Management Commands

### 1. Create a Group
The `groupadd` command is used to add a group in the system. Group information is stored in `/etc/group`.

**Syntax:**
```bash
# groupadd <groupname>
````

**Example:**

```bash
[root@server ~]# groupadd IBM
[root@server ~]# tail -1 /etc/group
IBM:x:1005:
```

---

### 2. Create Group with Custom Settings

You can customize group creation using options.

**Syntax:**

```bash
# groupadd <option> <parameter> <groupname>
```

**Options:**

* `-g` → Assign a specific **Group ID (GID)**
* `-o` → Allow **non-unique GID**
* `-f` → Force creation

**Example:**

```bash
[root@server ~]# groupadd -g 2005 TCS
[root@server ~]# tail -1 /etc/group
TCS:x:2005:
```

---

### 3. Modify Existing Group

The `groupmod` command is used to modify an existing group.

**Syntax:**

```bash
# groupmod <option> <parameter> <groupname>
```

**Options:**

* `-g` → Change **Group ID (GID)**
* `-n` → Change **Group Name**
* `-o` → Allow **non-unique GID**

---

#### Example 1: Change Group ID

```bash
[root@server ~]# groupmod -g 5903 IBM
[root@server ~]# tail -1 /etc/group
IBM:x:5903:
```

#### Example 2: Change Group Name

```bash
[root@server ~]# groupmod -n TATA TCS
[root@server ~]# tail -2 /etc/group
TATA:x:2005:
```

---

## 👨‍💻 User Administration/Management

* `id username` → Show UID, GID, and group membership.
* `usermod -d /new/home username` → Change user’s home directory.
* `usermod -s /bin/bash username` → Change user’s login shell.
* `usermod -L username` → Lock user account.
* `usermod -U username` → Unlock user account.

---


# User Management – `useradd` Command

## Creating a New User Account
The `useradd` command is used to create a new user account.

**Syntax:**
```bash
# useradd <username>
````

**Example:**

```bash
[root@ip-172-31-19-5 ~]# useradd shubham
```

---

## `/etc/passwd` File

The `/etc/passwd` file stores user profile information. It contains **7 fields**, separated by `:`.

**Format:**

```
vaibhav:x:1001:1001:This is linux Batch:/home/vaibhav:/bin/bash
```

---


### Fields Description


---

## Fields Explanation

1. **Username**  
   - Login name of the user (unique).  
   - Example: `vaibhav`

2. **Password Placeholder**  
   - Contains `x` if the encrypted password is stored in `/etc/shadow`.  
   - Older systems used to store passwords here (insecure).  
   - Example: `x`

3. **UID (User ID)**  
   - Numerical ID assigned to the user.  
   - `0` → root user  
   - `1–999` → system users  
   - `1000+` → normal users  
   - Example: `1001`

4. **GID (Group ID)**  
   - Primary group ID of the user (defined in `/etc/group`).  
   - Example: `1001`

5. **Comment / GECOS Field**  
   - Stores user description or full name.  
   - Can also include phone number, office, etc.  
   - Example: `This is linux Batch`

6. **Home Directory**  
   - The absolute path to the user’s home directory.  
   - Example: `/home/vaibhav`

7. **Shell**  
   - The program that runs after login (default: `/bin/bash`).  
   - Example: `/bin/bash`


---

## Adding Users with Customized Settings

**Syntax:**

```bash
# useradd <username>
```

### Options

| Option | Description         |
| ------ | ------------------- |
| `-u`   | User ID             |
| `-g`   | Primary group       |
| `-c`   | Comment             |
| `-d`   | Home directory      |
| `-s`   | Login shell         |
| `-G`   | Secondary group     |
| `-r`   | System user         |
| `-e`   | Account expiry date |
| `-o`   | Non-unique UID      |

---
### Modify User with Customized Settings

* `useradd -m -d /custom/home -s /bin/zsh customuser`
  → Create user with custom home and shell.
* `usermod -c "Developer User" username`
  → Add a comment (user description).

---

# User Modification (`usermod` Command)

The `usermod` command in Linux is used to modify an existing user's settings.

---

## Syntax
```bash
usermod <option> <parameters> <username>
````

---

## Common Options

| Option | Description                           |
| ------ | ------------------------------------- |
| `-u`   | Change user ID                        |
| `-g`   | Change primary group                  |
| `-c`   | Add/modify comment                    |
| `-d`   | Change home directory                 |
| `-s`   | Change login shell                    |
| `-G`   | Assign secondary/supplementary groups |
| `-l`   | Change login name                     |
| `-L`   | Lock user password                    |
| `-U`   | Unlock user password                  |
| `-m`   | Move/modify directories               |

---

## Examples

### 1. Change User ID

```bash
# usermod -u 7766 sumit
# tail -1 /etc/passwd
sumit:x:7766:6021::/home/sumit:/bin/bash
```

---

### 2. Change Comment

```bash
# usermod -c "windows" sumit
# tail -1 /etc/passwd
sumit:x:7766:6021:windows:/home/sumit:/bin/bash
```

---

### 3. Change Home Directory

```bash
# usermod -m -d /home/amit sumit
# tail -1 /etc/passwd
sumit:x:7766:6021:windows:/home/amit:/bin/bash
```

---

### 4. Change Login Shell

```bash
# usermod -s /bin/bash sumit
# tail -1 /etc/passwd
sumit:x:7766:6021:windows:/home/amit:/bin/bash
```

---

### 5. Assign Secondary/Supplementary Group

```bash
# usermod -G TCS suresh
# tail -1 /etc/group
TCS:x:6023:suresh
```

---

### 6. Change User Login Name

```bash
# usermod -l suresh ritesh
# tail -1 /etc/passwd
suresh:x:2214:2214::/home/ritesh:/bin/bash
```

---

### 7. Change Account Expiry Date

```bash
# usermod -e '14 dec 2025' ritesh
# chage -l ritesh
Last password change                                    : Aug 15, 2025
Password expires                                        : never
Password inactive                                       : never
Account expires                                         : Dec 14, 2025
Minimum number of days between password change          : 0
Maximum number of days between password change          : 99999
Number of days of warning before password expires       : 7
```

---

### 8. Lock and Unlock User Password

#### Lock Password

```bash
# tail -1 /etc/shadow
vaibhav:$6$lblryj7X$jDt1EWzSANqKVrW/KS4VSEBU/GTFFgUmfCNZJxBjV4kTUJWgirNaNKsHIg79YgUIPXO.VT50vQuNnu4ik64ZM/:18209:0:99999:7:::

# usermod -L vaibhav
# tail -1 /etc/shadow
vaibhav:!$6$lblryj7X$jDt1EWzSANqKVrW/KS4VSEBU/GTFFgUmfCNZJxBjV4kTUJWgirNaNKsHIg79YgUIPXO.VT50vQuNnu4ik64ZM/:18209:0:99999:7:::
```

#### Unlock Password

```bash
# usermod -U vaibhav
# tail -1 /etc/shadow
vaibhav:$6$lblryj7X$jDt1EWzSANqKVrW/KS4VSEBU/GTFFgUmfCNZJxBjV4kTUJWgirNaNKsHIg79YgUIPXO.VT50vQuNnu4ik64ZM/:18209:0:99999:7:::
```

---


---


## ❌ Remove User from System

* `userdel username` → Delete user account.
* `userdel -r username` → Delete user account with home directory.

---


## Remove User from System

The `userdel` command is used to remove or delete a user account from the system.  

**Syntax:**
```bash
# userdel <username>
````

**Examples:**

* Delete user account:

```bash
[root@ip-172-31-19-5 ~]# userdel vaibhav
```

* Delete user account along with its home directory and mail account:

```bash
[root@ip-172-31-19-5 ~]# userdel -r vaibhav
```

---

## `/etc/gshadow` File

The `/etc/gshadow` file is used to store the **password of groups**, along with the admin and member list of groups.
It contains **four fields**:

1. **Group name**
2. **Encrypted Password**
3. **Admin of group**
4. **Member list**

---

## `gpasswd` Command

The `gpasswd` command is used to manage group passwords. It can also be used to **add members** and **assign admins** to groups.

**Syntax:**

```bash
# gpasswd <option> <parameter> <groupname>
```

**Options:**

* `-a` : Add members in group
* `-M` : Set list of members in group (replace old list)
* `-A` : Assign user as group admin

---

### Examples of `gpasswd`

**1. Assign or Change Group Password**

```bash
[root@ip-172-31-19-5 ~]# gpasswd TCS
Changing the password for group TCS
New Password:
Re-enter new password:

[root@ip-172-31-19-5 ~]# tail -1 /etc/gshadow
TCS:$6$b4a1sbtiZDy$arjapZjNWW2u.EE2D49ZI2k8VtT7WNZ3zRNkmg0ByFIrJrXbjMZe8fQ0U0RQfTG/RrXOKAukFC5ganx0k00MO1::
```

**2. Add Existing User in Group using `gpasswd`**

```bash
[root@ip-172-31-19-5 ~]# gpasswd -a mahesh TCS
Adding user mahesh to group TCS

[root@ip-172-31-19-5 ~]# tail -1 /etc/group
TCS:x:2218:mahesh
```

**3. Add Existing User in Group using `usermod`**

```bash
[root@ip-172-31-19-5 ~]# usermod -G TCS suresh
[root@ip-172-31-19-5 ~]# tail -1 /etc/group
TCS:x:2218:mahesh,suresh
```

**4. Add New User in Group During Creation**

```bash
[root@ip-172-31-19-5 ~]# useradd -G TCS vaibhav
[root@ip-172-31-19-5 ~]# tail -2 /etc/group
TCS:x:2218:mahesh,suresh,vaibhav
vaibhav:x:2219:
```

**5. Set List of Members in Group (replaces old list)**

```bash
[root@ip-172-31-19-5 ~]# gpasswd -M suresh,ramesh TCS
[root@ip-172-31-19-5 ~]# tail -2 /etc/group
TCS:x:2218:suresh,ramesh
vaibhav:x:2219:
```

**6. Assign User as Group Admin**

```bash
[root@ip-172-31-19-5 ~]# gpasswd -A amit TCS
[root@ip-172-31-19-5 ~]# tail -2 /etc/gshadow
TCS:$6$b4a1sbtiZDy$arjapZjNWW2u.EE2D49ZI2k8VtT7WNZ3zRNkmg0ByFIrJrXbjMZe8fQ0U0RQfTG/RrXOKAukFC5ganx0k00MO1:vaibhav:suresh,ramesh
vaibhav:!::
```

---




