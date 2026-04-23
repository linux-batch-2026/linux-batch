
# 📦 Archiving and Compression 

## 📌 Difference Between Archiving and Compression
- **Archiving**: Process of combining multiple files and directories (of same or different sizes) into a single file.  
  - Commonly used for system backups or when moving data across systems.  
  - Example tool: `tar`  

- **Compression**: Process of reducing the size of a file or directory.  
  - Saves storage, speeds up file transfers, and reduces network/storage costs.  
  - Example tools: `gzip`, `bzip2`, `xz`

---
  

## 📁 Archiving Tools

* **tar (tape archive):** Used for creating archives.

  * `tar -cvf archive.tar file1 file2` → Create archive.
  * `tar -xvf archive.tar` → Extract archive.
  * `tar -tvf archive.tar` → List archive contents.


---

## 📦 `tar` Command
The `tar` (tape archive) command is one of the oldest and most commonly used commands for creating and working with backup archives.

**Syntax:**
```bash
tar <-options> <archive_filename>.tar <files_to_be_compressed>
````

### Options:

* `-c` → Create an archive
* `-f` → File name (**compulsory option**)
* `-v` → Verbose (show progress)
* `-t` → List contents of archive
* `-x` → Extract contents of archive
* `-P` → Preserve permissions when extracting
* `-C` → Extract to a specific directory

---

## 🗂 Examples

### 1. Archiving Files

```bash
# Check size of /etc directory
du –sh /etc
# Output: 34M /etc

# Create archive
tar -cvf /backup.tar /etc
# Output: tar: Removing leading '/' from member names

# Check archive size
du –sh /backup.tar
# Output: 30M /backup.tar

```
### 2. Listing Archive Contents

```bash
tar -tvf /backup.tar
```

### 3. Extracting Archive

```bash
# Extract in current directory
tar –xvf /backup.tar

# Extract in another directory
tar –xvf /backup.tar –C /demo/
```

---

## 📉 Compression Tools

* **gzip** → Compress files (`.gz`).

  * `gzip file` → Compress.
  * `gunzip file.gz` → Decompress.
* **bzip2** → Better compression (`.bz2`).

  * `bzip2 file` → Compress.
  * `bunzip2 file.bz2` → Decompress.
* **xz** → High compression ratio (`.xz`).

  * `xz file` → Compress.
  * `unxz file.xz` → Decompress.

---


## 🔗 Combined Usage

* `tar -czvf archive.tar.gz files/` → Create compressed archive with gzip.
* `tar -xvzf archive.tar.gz` → Extract gzip compressed archive.
* `tar -cjvf archive.tar.bz2 files/` → Create bzip2 archive.
* `tar -xjvf archive.tar.bz2` → Extract bzip2 archive.
* `tar -cJvf archive.tar.xz files/` → Create xz archive.
* `tar -xJvf archive.tar.xz` → Extract xz archive.

---

## 📉 Compression with `tar`

```bash
# Gzip
tar –czvf /backup1.tar.gz /etc
du –sh /backup1.tar.gz
# Output: 8.4M /backup1.tar.gz

# Bzip2
tar –cjvf /backup2.tar.bz2 /etc
du –sh /backup2.tar.bz2
# Output: 7.0M /backup2.tar.bz2

# XZ
tar –cJvf /backup3.tar.xz /etc
du –sh /backup3.tar.xz
# Output: 5.7M /backup3.tar.xz
```

---
## 📌 Other Tools

* **zip/unzip** → Cross-platform compression.

  * `zip archive.zip file1 file2` → Create zip.
  * `unzip archive.zip` → Extract zip.
* **7z (p7zip)** → Strong compression.

  * `7z a archive.7z files` → Create.
  * `7z x archive.7z` → Extract.

---

### Extraction

```bash
mkdir /gz_xtr /bz2_xtr /xz_xtr

# Gzip
tar –xvzf /backup1.tar.gz –C /gz_xtr

# Bzip2
tar –xvjf /backup2.tar.bz2 –C /bz2_xtr

# XZ
tar –xvJf /backup3.tar.xz –C /xz_xtr
```

---

## 📂 Compression with Commands Directly

### Using `gzip`

```bash
tar -cvf /etc.tar /etc
du -sh /etc.tar
# Output: 30M /etc.tar

gzip /etc.tar
ls /
# Output: etc.tar.gz

du -sh /etc.tar.gz
# Output: 8.4M /etc.tar.gz
```

### Using `bzip2`

```bash
tar -cvf /etc.tar /etc
du -sh /etc.tar
# Output: 30M /etc.tar

bzip2 /etc.tar
ls /
# Output: etc.tar.bz2

du -sh /etc.tar.bz2
# Output: 7.5M /etc.tar.bz2
```

### Using `xz`

```bash
tar -cvf /etc.tar /etc
du -sh /etc.tar
# Output: 30M /etc.tar

xz /etc.tar
ls /
# Output: etc.tar.xz

du -sh /etc.tar.xz
# Output: 5.8M /etc.tar.xz
```

---



















