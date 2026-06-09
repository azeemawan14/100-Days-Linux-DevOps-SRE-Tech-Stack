# PRACTICE LAB
# Day 32 – Login Process, systemd, Shells and Initialization Files
## June 8th, 2026

> Based on Class Notes and Slides by NIT Academy :contentReference[oaicite:0]{index=0}

---

# Objective

In this practice lab, students will learn how to:

1. Check Linux kernel and operating system version.
2. Verify that `systemd` is running as PID 1.
3. Identify the current Linux shell.
4. Check the PID of the current shell.
5. Explore the `/etc` configuration directory.
6. Read the `/etc/shells` file using absolute and relative paths.
7. Use the `ping` command and stop a running process.
8. Run basic troubleshooting commands.
9. Identify global Bash initialization files.
10. Create a backup before modifying critical configuration files.

---

# Table of Contents

| Task | Title |
|------|--------|
| 1 | Check Kernel and Operating System Version |
| 2 | Verify systemd is Running as PID 1 |
| 3 | Identify Current Linux Shell |
| 4 | Find the PID of Your Current Shell |
| 5 | Explore the /etc Configuration Directory |
| 6 | Read the /etc/shells File |
| 7 | Practice the ping Command |
| 8 | Basic Troubleshooting Commands |
| 9 | Identify Global Initialization Files |
| 10 | Backup a Critical Configuration File |
| 11 | Final Review Questions |
| 12 | Lab Summary |

---

# Task 1 - Check Kernel and Operating System Version

## Question

What is your Kernel Version and Operating System Version?

### Run

~~~bash
uname -a
uname -r
cat /etc/os-release
~~~

### Student Observation

Write down:

~~~text
Kernel Version:
Operating System:
~~~

### Notes

- `uname -a` displays complete kernel information.
- `uname -r` displays only the kernel version.
- `cat /etc/os-release` displays operating system information.

---

# Task 2 - Verify systemd is Running as PID 1

## Question

How do you know that `systemd` is running?

### Run

~~~bash
ps 1
ps -e
~~~

### Notes

- `ps 1` displays the process with PID 1.
- `ps -e` displays all running processes.
- PID 1 is usually `systemd`.
- `systemd` is the parent process of most other processes.

### Student Observation

Answer the following:

1. Which process has PID 1?
2. Why is PID 1 important?
3. What does `ps -e` display?

---

# Task 3 - Identify Current Linux Shell

## Question

How do you know which Linux shell you are using?

### Run

~~~bash
echo $SHELL
~~~

### Example Output

~~~text
/bin/bash
~~~

### Student Observation

Write down:

~~~text
Current Shell:
~~~

### Notes

Common Linux shells include:

- Bash
- Sh
- Zsh
- Ksh

---

# Task 4 - Find the PID of Your Current Shell

## Question

Other than `echo $SHELL`, how do you determine the Process ID (PID) of your shell?

### Run

~~~bash
ps $$
echo $$
echo $0
~~~

### Student Observation

Write down:

~~~text
Shell PID:
Shell Name:
~~~

### Notes

| Command | Purpose |
|----------|----------|
| `ps $$` | Displays the current shell process |
| `echo $$` | Displays the shell PID |
| `echo $0` | Displays the shell name |

---

# Task 5 - Explore the /etc Configuration Directory

## Question

Which directory largely contains Linux configuration files?

### Run

~~~bash
ls -l /etc
cd /etc
ls
~~~

### Student Observation

Answer the following:

1. What types of files do you see?
2. Why is `/etc` important?

### Notes

Examples of important files:

~~~text
/etc/profile
/etc/bashrc
/etc/passwd
/etc/group
/etc/shadow
/etc/shells
~~~

---

# Task 6 - Read the /etc/shells File

## Question

How can you view the `/etc/shells` file in read-only mode?

### Method 1 - Absolute Path

#### Run

~~~bash
cat /etc/shells
~~~

---

### Method 2 - Relative Path

#### Run

~~~bash
cd /etc
pwd
cat shells
~~~

### Student Observation

Answer:

1. What shells are available on your system?
2. What is the difference between Absolute Path and Relative Path?

### Notes

Absolute Path Example:

~~~text
/etc/shells
~~~

Relative Path Example:

~~~text
shells
~~~

---

# Task 7 - Practice the ping Command

## Question

What does the `ping` command teach us?

### Run

~~~bash
ping google.com
ping -c 5 google.com
ping 8.8.8.8
~~~

### Important Note

To stop a running process:

~~~text
Ctrl + C
~~~

### Student Observation

Answer:

1. Was Google reachable?
2. What happens when you ping an IP address directly?
3. Why would a System Administrator use ping?

### Notes

Ping is commonly used to test:

- Network connectivity
- DNS resolution
- Internet access
- Response times
- Reachability of remote systems

---

# Task 8 - Basic Troubleshooting Commands

## Question

As a Linux System Administrator, whenever you troubleshoot a system, run the following commands and think about why each one is useful.

### Run

~~~bash
date
uptime
hostname
whoami
pwd
cd ~
~~~

### Student Observation

Complete the table:

| Command | Why Is It Useful? |
|----------|------------------|
| date | |
| uptime | |
| hostname | |
| whoami | |
| pwd | |
| cd ~ | |

---

# Task 9 - Identify Global Initialization Files

## Question

What are the two major Global Initialization Files?

### Run

~~~bash
cat /etc/profile
cat /etc/bashrc
~~~

### Student Observation

Answer:

1. Which file affects Login Shells?
2. Which file affects Non-Login Shells?
3. Why are these files important?

### Notes

| File | Purpose |
|--------|----------|
| `/etc/profile` | Global Login Shell Initialization File |
| `/etc/bashrc` | Global Interactive Shell Initialization File |

---

# Task 10 - Backup a Critical Configuration File

## Question

What should you always do before modifying or deleting a critical configuration file?

### Answer

Always create a backup.

### Run

~~~bash
cp -r /etc/profile /etc/profile_bak
cd /etc
ls
~~~

### Verify

You should see:

~~~text
profile
profile_bak
~~~

### Important Warning

Never delete:

~~~text
/etc/profile
~~~

This is a critical system file.

### Remove the Backup File

~~~bash
rm /etc/profile_bak
~~~

### Notes

- `rm` removes files.
- `rmdir` removes empty directories.
- `profile_bak` is a file, therefore `rm` must be used.

---

# Final Review Questions

1. What command shows the kernel version?
2. What command displays operating system information?
3. What is PID 1?
4. Why is systemd important?
5. What command displays your current shell?
6. What command displays your shell PID?
7. What is the purpose of the `/etc` directory?
8. What is the difference between an Absolute Path and a Relative Path?
9. What does the ping command test?
10. How do you stop a running process?
11. What are the two major Global Initialization Files?
12. Why should configuration files be backed up before modification?
13. What is the difference between `rm` and `rmdir`?

---

# Lab Summary

In this lab you practiced:

- Checking kernel information
- Checking operating system information
- Verifying systemd as PID 1
- Identifying your shell
- Finding your shell PID
- Exploring the `/etc` directory
- Reading `/etc/shells`
- Understanding Absolute and Relative Paths
- Using the ping command
- Stopping processes using Ctrl + C
- Running basic troubleshooting commands
- Reading Global Initialization Files
- Backing up critical configuration files

---

# Final Note

As a Linux System Administrator, always remember:

~~~bash
date
uptime
hostname
whoami
pwd
~~~

These commands provide valuable information during troubleshooting.

### Golden Rule

~~~text
BACKUP FIRST, CHANGE LATER
~~~

---
# End of Lab

🐧 Happy Learning Linux!