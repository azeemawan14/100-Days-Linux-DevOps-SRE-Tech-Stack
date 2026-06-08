# Linux Administration Bootcamp
# Day-30/Day-31 – Directories, Paths and Files
## June 6/7, 2026

---

# Objective

By the end of this lab, students will be able to:

1. Display the current system date and time.
2. Check how long a Linux system has been running.
3. Determine their current location in the Linux filesystem.
4. Understand the difference between Absolute and Relative Paths.
5. Create directories using Absolute Paths.
6. Create directories using Relative Paths.
7. Create files using the `touch` command.
8. Verify directories and files using the `ls` command.

---

# Table of Contents

1. Introduction
2. Understanding Paths in Linux
3. Task 1 – Display Date and Time
4. Task 2 – Check System Uptime
5. Task 3 – Check Current Directory
6. Task 4 – Create Directories
   - Absolute Path
   - Relative Path
7. Task 5 – Create Files
8. Verification Checklist
9. Review Questions
10. Lab Summary

---

# Introduction

Linux stores everything inside a hierarchical filesystem structure.

Example:

```text
/
├── root
├── home
├── var
├── opt
├── etc
└── tmp
```

A user can navigate throughout the filesystem and create directories and files.

Two important concepts are:

- Absolute Path
- Relative Path

---

# Understanding Paths in Linux

## Absolute Path

An Absolute Path always starts from the root directory (`/`).

Example:

```bash
/var/opt/images
```

No matter where you are currently located, Linux can find this directory because the complete path is provided.

### Examples

```bash
/etc/passwd
/home/student
/var/log/messages
/var/opt/images
```

---

## Relative Path

A Relative Path starts from your current location.

Example:

```bash
projects
```

Linux creates or accesses the directory relative to where you are currently located.

### Examples

```bash
projects
documents
file1
images/photo.jpg
```

---

# Task 1 – Display Date and Time

## Objective

Display the current system date and time.

### Run

```bash
date
```

### Example Output

```text
Sat Jun 6 10:15:24 UTC 2026
```

### Notes

The `date` command is commonly used when:

- Creating logs
- Troubleshooting issues
- Verifying server time
- Checking timestamps

---

# Task 2 – Check System Uptime

## Objective

Determine how long the Linux system has been running.

### Run

```bash
uptime
```

### Example Output

```text
10:17:10 up 5 days, 4:22, 1 user, load average: 0.00, 0.01, 0.05
```

### Notes

The uptime command shows:

- Current time
- How long the machine has been running
- Number of logged-in users
- System load averages

### Discussion

Ask students:

- How long has your machine been running?
- How many users are logged in?
- What do the load averages mean?

---

# Task 3 – Check Current Directory

## Objective

Determine your current location in the filesystem.

### Run

```bash
pwd
```

### Example Output

```text
/root
```

### Notes

`pwd` stands for:

```text
Print Working Directory
```

It tells you exactly where you are currently located.

---

# Task 4 – Create Directories

---

## Part A – Using an Absolute Path

### Objective

Create a directory by specifying the complete path.

### Run

```bash
mkdir -p /var/opt/images
```

### Verify

```bash
ls -l /var/opt/
```

### Example Output

```text
drwxr-xr-x 2 root root 6 Jun 6 10:20 images
```

### Explanation

The directory was created regardless of where you were located because the complete path was specified.

```text
/var/opt/images
```

This is called an Absolute Path.

---

## Part B – Using a Relative Path

### Step 1 – Check Current Location

Run:

```bash
pwd
```

---

### Step 2 – Return to Home Directory

Run:

```bash
cd
```

Verify:

```bash
pwd
```

Expected Output:

```text
/root
```

---

### Step 3 – Move Into /var

Run:

```bash
cd /var
```

Verify:

```bash
pwd
```

Expected Output:

```text
/var
```

---

### Step 4 – Enter opt Directory

Run:

```bash
cd opt
```

Verify:

```bash
pwd
```

Expected Output:

```text
/var/opt
```

---

### Step 5 – Create a Directory

Run:

```bash
mkdir -p projects
```

---

### Step 6 – Verify

Run:

```bash
ls -l
```

Expected Output:

```text
images
projects
```

### Explanation

The directory `projects` was created relative to your current location:

```text
/var/opt
```

Therefore:

```text
projects
```

became:

```text
/var/opt/projects
```

This is called a Relative Path.

---

# Task 5 – Create Files

## Objective

Create files using the `touch` command.

---

### Step 1 – Verify Location

Run:

```bash
pwd
```

Expected Output:

```text
/var/opt
```

---

### Step 2 – Create a File

Run:

```bash
touch summary.txt
```

---

### Step 3 – Create Multiple Files

Run:

```bash
touch file{1..5}
```

This creates:

```text
file1
file2
file3
file4
file5
```

---

### Step 4 – Verify

Run:

```bash
ls -l
```

Example Output:

```text
-rw-r--r-- 1 root root 0 Jun 6 10:25 summary.txt
-rw-r--r-- 1 root root 0 Jun 6 10:25 file1
-rw-r--r-- 1 root root 0 Jun 6 10:25 file2
-rw-r--r-- 1 root root 0 Jun 6 10:25 file3
-rw-r--r-- 1 root root 0 Jun 6 10:25 file4
-rw-r--r-- 1 root root 0 Jun 6 10:25 file5
```

---

# Verification Checklist

Confirm that you have successfully completed the following:

- [ ] Ran the `date` command
- [ ] Ran the `uptime` command
- [ ] Ran the `pwd` command
- [ ] Created `/var/opt/images`
- [ ] Created `/var/opt/projects`
- [ ] Created `summary.txt`
- [ ] Created `file1`
- [ ] Created `file2`
- [ ] Created `file3`
- [ ] Created `file4`
- [ ] Created `file5`

---

# Review Questions

1. What does the `date` command display?
2. What information does the `uptime` command provide?
3. What does `pwd` stand for?
4. What is an Absolute Path?
5. What is a Relative Path?
6. Why is `/var/opt/images` considered an Absolute Path?
7. Why is `projects` considered a Relative Path?
8. What does the `mkdir -p` option do?
9. What command is used to create an empty file?
10. How can multiple files be created with a single command?

---

# Challenge Task

Create the following directory structure:

```text
/var/opt/linuxlab
├── docs
├── scripts
└── backups
```

### Commands

```bash
mkdir -p /var/opt/linuxlab/docs
mkdir -p /var/opt/linuxlab/scripts
mkdir -p /var/opt/linuxlab/backups
```

Verify:

```bash
ls -R /var/opt/linuxlab
```

---

# Lab Summary

In this lab you learned:

- How to display the current date and time.
- How to check system uptime.
- How to determine your current location in the filesystem.
- The difference between Absolute and Relative Paths.
- How to create directories using both methods.
- How to create files using the `touch` command.
- How to verify filesystem changes using the `ls` command.

These are foundational Linux administration skills that will be used throughout the remainder of the bootcamp.