# 📦 Managing Software 

Linux systems use package managers to install, update, and remove software. Package management varies based on the distribution family (Debian-based, Red Hat-based, etc.).

### 1. **Package Management Tools**

#### Debian/Ubuntu (APT – Advanced Package Tool)

*  `apt update` → Updates the package index.
*  `apt upgrade` → Upgrades all installed packages.
*  `apt install package_name` → Installs a new package.
* `apt remove package_name` → Removes a package.
*  `apt purge package_name` → Removes a package with configuration files.
*  `apt search package_name` → Search for a package.
*  `dpkg -i package.deb` → Install a `.deb` file manually.

---

**Example:**

```bash
sudo apt update
sudo apt install nginx -y
```

---

#### Red Hat/CentOS/Fedora (YUM/DNF)

* `yum install package_name` → Installs a package (older versions).
* `dnf install package_name` → Installs a package (newer versions).
* `yum remove package_name` → Removes a package.
* `yum update` → Updates all packages.
* `rpm -ivh package.rpm` → Installs an `.rpm` file manually.
* `dnf search package_name` → Search for a package.

---


**Example:**

```bash
sudo dnf install httpd -y
```

---



### 2. **Source Code Installation**

Sometimes software is not available in repositories and must be compiled from source.

**Steps:**

```bash
wget http://example.com/software.tar.gz
 tar -xvzf software.tar.gz
 cd software
 ./configure
 make
 sudo make install
```

---

### 3. **Snap Packages (Universal)**

* `snap install package_name` → Install snap package.
* `snap remove package_name` → Remove snap package.
* `snap list` → List installed snaps.

---

**Example:**

```bash
sudo snap install vlc
```

---

### 4. **Checking Installed Software**

* Debian/Ubuntu → `dpkg -l | grep package`
* RHEL/CentOS/Fedora → `rpm -qa | grep package`

---

### 5. **Upgrading and Removing Software**

* Debian/Ubuntu → `apt upgrade` / `apt remove package`
* RHEL/CentOS → `yum update` / `yum remove package`

---
