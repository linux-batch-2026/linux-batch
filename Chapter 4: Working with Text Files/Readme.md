# Working with Text Files 

In Linux, text files are the most common way to store data, configurations, and scripts.
This guide covers different commands and examples to **create, view, edit, search, and manipulate text files**.

---

## 📌 1. Creating Text Files

You can create an empty text file or add content to it.

### Examples:

```bash
# Create an empty file
touch file.txt

# Create a file with content
echo "Hello World" > file.txt

# Append text to a file
echo "This is a new line" >> file.txt

# Create a file using cat
cat > notes.txt
This is a note.
Press CTRL+D to save and exit
```

---

## 📌 2. Viewing Text Files

There are different ways to view text files.

### Examples:

```bash
# Display entire file
cat file.txt

# Display file with line numbers
cat -n file.txt

# Show first 10 lines of file
head file.txt

# Show last 10 lines of file
tail file.txt

# View file in a scrolling mode
less file.txt
more file.txt
```

---

## 📌 3. Editing Text Files

You can edit text files using editors.

### Examples:

```bash
# Open file with nano editor
nano file.txt

# Open file with vi editor
vi file.txt

# Open file with vim editor
vim file.txt
```

---

## 📌 4. Searching in Text Files

The `grep` command is used for searching.

### Examples:

```bash
# Search for a word in file
grep "Hello" file.txt

# Search case-insensitive
grep -i "hello" file.txt

# Show line numbers with match
grep -n "line" file.txt

# Search in multiple files
grep "error" *.log
```

---

## 📌 5. Comparing Text Files

The `diff` and `cmp` commands help compare files.

### Examples:

```bash
# Compare two files line by line
diff file1.txt file2.txt

# Compare byte by byte
cmp file1.txt file2.txt
```

---

## 📌 6. Counting in Text Files

The `wc` command helps count lines, words, and characters.

### Examples:

```bash
# Count lines, words, and characters
wc file.txt

# Only count lines
wc -l file.txt

# Only count words
wc -w file.txt

# Only count characters
wc -m file.txt
```

---

## 📌 7. Sorting Text Files

The `sort` command sorts file contents.

### Examples:

```bash
# Sort alphabetically
sort file.txt

# Sort in reverse order
sort -r file.txt

# Remove duplicates
sort -u file.txt
```

---

## 📌 8. Combining Text Files

You can merge multiple files.

### Examples:

```bash
# Combine files into one
cat file1.txt file2.txt > merged.txt

# Append file2 to file1
cat file2.txt >> file1.txt
```

---

## 📌 9. Replacing and Editing Text

The `sed` command is used for editing text.

### Examples:

```bash
# Replace 'Hello' with 'Hi' in file
sed 's/Hello/Hi/' file.txt

# Replace all occurrences in file
sed 's/Hello/Hi/g' file.txt

# Delete a line (e.g., line 2)
sed '2d' file.txt
```

---

## 📌 10. Extracting Text

The `cut` and `awk` commands are used.

### Examples:

```bash
# Extract first 10 characters of each line
cut -c 1-10 file.txt

# Extract the first column (default delimiter is TAB)
cut -f1 file.txt

# Extract using delimiter (:)
cut -d ":" -f1 /etc/passwd

# Print specific column using awk
awk '{print $1}' file.txt
```

---

## 📌 11. Execute Multiple Commands

- `Semicolon (;)` – Executes two or more commands in same command line argument.

### Examples:

```bash
 touch /abc.txt ; mkdir /mydir ; cp –r /mnt /media
```

- `Pipe (|)` – It matches first command output to the second command and execute it

### Examples:

```bash
 dmidecode | less
```

---



