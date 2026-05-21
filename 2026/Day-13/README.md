# Practice Lab — Understanding Linux Inodes
> NIT Academy Linux Practice Lab  
> Topic: Inodes, Metadata, and Directory Structure

---

# Table of Contents

| Task | Title |
|------|--------|
| 1 | [Checking Inodes with `ls -li`](#task-1---checking-inodes-with-ls--li) |
| 2 | [Understanding Directory Metadata with `ls -ld`](#task-2---understanding-directory-metadata-with-ls--ld) |
| 3 | [Comparing `ls -l` vs `ls -ld`](#task-3---comparing-ls--l-vs-ls--ld) |
| 4 | [Checking Filesystem Inode Usage](#task-4---checking-filesystem-inode-usage) |
| 5 | [Creating Files and Watching Inodes Change](#task-5---creating-files-and-watching-inodes-change) |
| 6 | [Important Concepts Explained](#task-6---important-concepts-explained) |

---

# Introduction
A Linux filesystem separates:
| Component       | Stores What?            |
| --------------- | ----------------------- |
| **Inode**       | Metadata about the file |
| **Data Blocks** | Actual file contents    |

## Simple Explanation
Think of it like this:
| Real Life Example    | Linux Equivalent |
| -------------------- | ---------------- |
| Library catalog card | Inode            |
| Actual book pages    | Data blocks      |
The catalog card tells you:
- who owns the book
- size
- location
- timestamps
- permissions

But the actual text of the book is stored elsewhere.

In Linux, every file and directory has an **inode**.
An inode is a special data structure that stores:

- File permissions
- Owner
- Group
- File size
- Timestamps
- Pointers to data blocks

> ⚠️ Important:
>
> Inodes DO NOT store the filename itself.

- The filename exists inside the **directory entry**, which points to an inode number.

The filename exists inside the directory entry.

Example:
| Filename   | Inode   |
| ---------- | ------- |
| report.txt | 3470012 |

The directory maps:
```
report.txt  → inode 3470012
```
Then Linux reads inode 3470012, which points to the actual datablocks.

## Practice Task
Run the following command:
```bash
echo "hello" > file1
```

Linux creates:\
Directory Entry
| Filename | Inode |
| -------- | ----- |
| file1    | 5001  |

Inode 5001 now Stores the following:
```
Owner: root
Permissions: rw-r--r--
Size: 6 bytes
Data block pointer: 9021
Data Block 9021
```
Data Block 9021 Contains:
```
hello
```
At this stage you should be very clear in your understanding of inodes. Let us now Run commands and Practice
# Task 1 - Checking Inodes with `ls -li`

Run the following command:

```bash
ls -li /var
```

Example Output:

```bash
3470012 drwxr-xr-x. 20 root root 4096 May 20 10:00 log
3470013 drwxr-xr-x.  2 root root 4096 May 20 10:00 tmp
3470014 drwxr-xr-x.  5 root root 4096 May 20 10:00 spool
```

---

## Explanation

| Field | Meaning |
|---|---|
| 3470012 | Inode number |
| d | Directory |
| rwxr-xr-x | Permissions |
| root | Owner |
| root | Group |
| 4096 | Size |
| log | Filename |

---

## Key Learning

Linux first reads the directory contents:

```bash
cd /var
ls -l
```

The directory contains:

| Filename | Inode |
|---|---|
| log | 3470012 |
| tmp | 3470013 |
| spool | 3470014 |

Linux then uses the inode number to locate the metadata and file blocks on disk.

---

# Task 2 - Understanding Directory Metadata with `ls -ld`

Run:

```bash
ls -ld /
```

Example Output:

```
dr-xr-xr-x. 22 root root 287 Jul 28 01:23 /
```

---

# What Does "287" Mean?

It means:
```
The '/' - root directory currently needs 287 bytes to store its list of filenames and inode mappings.
```
It DOES NOT mean:

- total size of all files inside `/`
- filesystem size
- used disk space

---

# Simple Explanation

Think of a directory like a:

📒 **Phone Book**

The directory only stores:

- filenames
- inode numbers

Example:

| Filename | Inode |
|---|---|
| etc | 1200 |
| var | 1201 |
| home | 1202 |

The actual file data exists elsewhere on disk.

---

# Important Clarification

Linux filesystems use different block sizes:

- 1 KB
- 2 KB
- 4 KB
- sometimes larger

You can check block size using:

```bash
stat -f /
```

or

```bash
dumpe2fs /dev/sdaX | grep "Block size"
```

---

# Better Explanation

The value:

```text
287
```

simply means:

> The directory metadata currently occupies 287 bytes.

As more files/directories are added inside `/`, this directory size can grow.

---

# Task 3 - Comparing `ls -l` vs `ls -ld`

## Command 1

```bash
ls -l /
```

This shows:

✅ Metadata of CONTENTS INSIDE `/`

---

## Command 2

```bash
ls -ld /
```

This shows:

✅ Metadata of the `/` directory ITSELF

---

## Command 3

```bash
ls -li /
```

Shows:

✅ Inode numbers + metadata

---

## Command 4

```bash
ls -ild /
```

Shows:

✅ Inode number of `/` itself

---

# Task 4 - Checking Filesystem Inode Usage

Run:

```bash
df -i
```

Example:

```bash
Filesystem      Inodes  IUsed   IFree IUse% Mounted on
/dev/sda1      655360 655360       0  100% /
```

---

# INTERVIEW QUESTIONS: 
When a user checks a VM's Linux file system (Hint: Using df -h) it shows the user that 20G of Disk Space is Available. When the user tries to create a new file (Hint: using 'touch' command) the system is not able to create a new file. What is the root cause of this problem?

Run this command to show free disk space:

```bash
df -h
```

shows free disk space:

```bash
20G available
```

Why are users unable to ceate files.

Because:

❌ All inodes are used.

---

# Very Important Concept

A filesystem has:

| Resource | Purpose |
|---|---|
| Disk blocks | Store actual file data |
| Inodes | Store metadata for files/directories |

You need BOTH available:

- ✅ Free blocks
- ✅ Free inodes

---

# Example

Imagine:

- You create 5 million tiny log files
- Each file is only 1 byte

Result:

- Very little disk space used
- BUT millions of inodes consumed

Eventually:

```bash
No space left on device
```

even though:

```bash
df -h
```

shows free space.

---

# Task 5 - Creating Files and Watching Inodes Change

Create practice directory:

```bash
mkdir ~/inode_lab
cd ~/inode_lab
```

Create files:

```bash
touch file1
touch file2
touch file3
```

Check inode numbers:

```bash
ls -li
```

Example:

```bash
3475001 file1
3475002 file2
3475003 file3
```

---

# Delete a File

```bash
rm file2
```

Create another:

```bash
touch newfile
```

Check again:

```bash
ls -li
```

Observe:

✅ Linux may reuse freed inode numbers.

---

# Task 6 - Important Concepts Explained

# Are Inodes Fixed?

✅ YES.

When a filesystem is created:

```bash
mkfs.ext4
```

Linux pre-allocates a fixed number of inodes.

---

# Why?

Because Linux must reserve space for inode tables ahead of time.

---

# Can You Increase Inodes Later?

Usually:

❌ No (not easily)

You normally recreate the filesystem with different inode settings.

---

# Where Are Inodes Stored?

Inodes are stored in special filesystem structures called:

```text
inode tables
```

These are created when the filesystem is formatted.

---

# Key Commands Summary

| Command | Purpose |
|---|---|
| `ls -li` | Show inode numbers |
| `ls -ld` | Show directory metadata |
| `df -i` | Show inode usage |
| `df -h` | Show disk usage |
| `stat file` | Detailed inode metadata |
| `find / -inum NUMBER` | Search by inode |

---

# Final Summary

| Concept | Meaning |
|---|---|
| Inode | Stores metadata |
| Filename | Stored in directory entry |
| Directory | Maps names to inode numbers |
| Disk Blocks | Store actual data |
| `df -h` | Shows block usage |
| `df -i` | Shows inode usage |
| No free inodes | Cannot create files |
| `ls -ld /` | Shows metadata of `/` itself |

---

# Practice Questions

1. What does an inode store?
2. Does an inode store the filename?
3. What is the difference between `ls -l /` and `ls -ld /`?
4. Why can a system run out of inodes?
5. What command shows inode usage?
6. Why can `df -h` show free space but file creation still fail?

---

# Final Summary

Run:

```bash
stat /etc/passwd
```

Identify:

- inode number
- timestamps
- permissions
- size
- owner
Post the results of your findings on LinkedIn
---
