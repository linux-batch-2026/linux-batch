# ✏️ Text Editors 

Text editors are essential tools for working in a Linux environment. They are used for editing configuration files, writing scripts, coding programs, and general text processing.

This document provides a comprehensive overview of **command-line** and **GUI-based editors** available in Linux. 

---

## 📂 Types of Editors in Linux

### 1. 📟 Command-Line Editors
These editors work inside the terminal and are ideal for server environments or when working over SSH.

### 2. 🖥️ Graphical Editors
These editors require a desktop environment and provide a graphical user interface (GUI) with menus, buttons, and mouse interaction.

---

## 📟 Common Command-Line Editors

### 🔹 1. `nano` – Simple and User-Friendly

- Easy to use for beginners
- Displays shortcuts at the bottom
- Great for quick edits

#### ✅ Basic Commands:
| Command | Action |
|--------|--------|
| `nano filename` | Open or create a file |
| `Ctrl + O` | Save file |
| `Ctrl + X` | Exit nano |
| `Ctrl + K` | Cut a line |
| `Ctrl + U` | Paste a line |

---

### 🔹 2. `vim` – Powerful and Advanced

- Modal editor: Normal, Insert, Visual, Command modes
- Preferred by power users and sysadmins
- Extensive plugin and configuration options

#### ✅ Modes:
- `Normal`: For navigating and commands (default)
- `Insert`: For editing text (`i`, `a`, etc.)
- `Visual`: For selecting text
- `Command`: For executing `:` commands

#### ✅ Basic Commands:
| Command | Mode |
|--------|--------|
| `vim filename` | Open a file |
| `Esc` | Exit insert mode to normal mode |
| `dd` | Delete line |
| `yy` | Copy line |
| `p` | Paste |
| `G` | From Top to Bottom |
| `gg` | From Bottom to Top |
| `dw` | Delete a Word |
| `u` | Undo |
> To install: `sudo apt install vim`

---

| Insert | Mode |
|--------|--------|
| `vim filename` | Open a file |
| `i` | Enter into Insert mode |
| `A` | End at line |
| `O` | Create line Above present cursor position |
| `o` | Create line Below present cursor position |

---

| Execation | Mode |
|--------|--------|
| `:wq` | save and quit |
| `:w` | save |
| `:q` | quit |
| `:q!` | Forcefully quit |
| `:set nu` | set line numbers |
| `:set nonu` | remove line numbers |
| `:/<word>` | Highlight word/string/character |
| `:nohl` | Remove highlight |

---

| Visual | Mode |
|--------|--------|
| `v` | Select character by character |
| `V` | Select line by line |
| `ctrl+v` | Select block |
| `y,d,c` | For copy, delete, and cut selected area |

---


### 🔹 3. `vi` – The Original Visual Editor

- Lightweight and available on almost all Unix/Linux systems
- A precursor to `vim`, with more limited features

---

## 📂 Types of Read Operations in Linux

#### ✅ Basic Commands:
| Command | Mode |
|--------|--------|
| `cat` | view the file from Bottom |
| `less` | view content of file from Top  |
| `more` | view content of file from Top |
| `head` | Top 10 lines show |
| `tail` | Bottom 10 lines show |

---































