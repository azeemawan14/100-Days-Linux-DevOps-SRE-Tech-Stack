# PRACTICE LAB 
# Day 32 – Login Process, systemd, Shells and Initialization Files
## June 8TH, 2026

> Based on Class Notes and Slides by NIT Academy 

---

# Table of Contents

1. Introduction
2. Linux Login Process
3. Understanding PID and PPID
4. Task 1 – Verify systemd (PID 1)
5. Task 2 – Identify Your Shell
6. Task 3 – Understand Process Hierarchy
7. Login Shell vs Non-Login Shell
8. Initialization Files
9. Global vs User Initialization Files
10. Task 4 – Examine Initialization Files
11. PATH Variable
12. Task 5 – Examine PATH
13. Task 6 – Create a Global Command
14. Understanding .bash_logout
15. Task 7 – Test Login Initialization Files
16. Review Questions
17. Lab Summary

---

# Introduction

Question 1 - What is your kernel Version and Operating System Version?
Run:
uname -a
uname -r
/etc/os-release

Question 2: How do you know "Systemd" is running?
Run:
ps 1
ps -e 
Note: ps -e will show you that the PID 1 is systemd. This is Parent of all the child processes below it

Question 3: How do you know what Linux Shell you are using?
Run:
echo $SHELL

Question 4: Other than "echo $SHELL" how do you know what is the process ID of your shell?
ps $$
echo $$
echo $0

Question 5: Which Directory largely contains Configuration Directories and files?
Run:
ls -l /etc
cd /etc
ls

Question 6: The cofiguration Directory (/etc) has a file called "shells". How can you READ-ONLY (view) this file:
Run using absolute path:
cat /etc/shells

Run using relative path:
cd /etc
pwd
cat shells

Question 7: What does ping command teach us?
Run:
ping google.com
ping -C 5 google.com
ping 8.8.8.8
NOTE: press Cntrl + C to stop a process and Linux will immediately put you in your line command or prompt (old terminology)

Question 8: As a Linux System Admin you must know that whenever you solve a problem take the following stesp and THINK WHY?
Run:
date
uptime
hostname
whoami
pwd
cd ~

Question 9: What the the TWO major Global Initialization files?
Run:
cat /etc/profile
cat /etc/bashrc

Question 10: Before you DELETE of any critical configuration files take a backup
Run:
Let us make a backup using:
Absolute Path
cp -r /etc/profile /etc/profile_bak
cd /etc
ls
You should see
profile
profile_bak
You can Delete this Directory:
NOTE: DO NOT DELETE /etc/profile
rmdir /etc/profile_bak# PRACTICE LAB
# Day 32 – Login Process, systemd, Shells and Initialization Files
## June 8th, 2026

> Based on Class Notes and Slides by NIT Academy

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
| 1 | [Check Kernel and Operating System Version](#task-1---check-kernel-and-operating-system-version) |
| 2 | [Verify systemd is Running as PID 1](#task-2---verify-systemd-is-running-as-pid-1) |
| 3 | [Identify Current Linux Shell](#task-3---identify-current-linux-shell) |
| 4 | [Find the PID of Your Current Shell](#task-4---find-the-pid-of-your-current-shell) |
| 5 | [Explore the /etc Configuration Directory](#task-5---explore-the-etc-configuration-directory) |
| 6 | [Read the /etc/shells File](#task-6---read-the-etcshells-file) |
| 7 | [Practice the ping Command](#task-7---practice-the-ping-command) |
| 8 | [Basic Troubleshooting Commands](#task-8---basic-troubleshooting-commands) |
| 9 | [Identify Global Initialization Files](#task-9---identify-global-initialization-files) |
| 10 | [Backup a Critical Configuration File](#task-10---backup-a-critical-configuration-file) |
| 11 | [Final Review Questions](#final-review-questions) |
| 12 | [Lab Summary](#lab-summary) |

---

# Introduction

Linux login and shell behavior is controlled by several important components:

- `systemd`
- PID and PPID
- Bash shell
- Login shell
- Non-login shell
- Initialization files
- Global configuration files
- User configuration files

As a Linux System Administrator, you must know how to inspect the system, understand what shell you are using, and safely work with configuration files.

---

# Task 1 - Check Kernel and Operating System Version

## Question

What is your kernel version and operating system version?

---

## Run:

```bash
uname -a
```

```bash
uname -r
```

```bash
cat /etc/os-release
```

---

## Notes

| Command | Purpose |
|---------|----------|
| `uname -a` | Shows full system and kernel information |
| `uname -r` | Shows only the kernel version |
| `cat /etc/os-release` | Shows operating system release/version details |

---

## Student Observation

Write down:

```text
Kernel Version:
Operating System:
```

---

# Task 2 - Verify systemd is Running as PID 1

## Question

How do you know `systemd` is running?

---

## Run:

```bash
ps 1
```

```bash
ps -e
```

---

## Notes

`systemd` is usually the first process started by the Linux kernel.

It normally has:

```text
PID 1
```

`systemd` is the parent of many child processes below it.

---

## Student Observation

Answer:

1. What process has PID 1?
2. Why is PID 1 important?
3. What does `ps -e` show?

---

# Task 3 - Identify Current Linux Shell

## Question

How do you know what Linux shell you are using?

---

## Run:

```bash
echo $SHELL
```

---

## Example Output

```text
/bin/bash
```

---

## Notes

The shell is the command-line interface between the user and the Linux operating system.

Common shells include:

- `/bin/bash`
- `/bin/sh`
- `/bin/zsh`
- `/bin/ksh`

---

# Task 4 - Find the PID of Your Current Shell

## Question

Other than `echo $SHELL`, how do you know the Process ID of your shell?

---

## Run:

```bash
ps $$
```

```bash
echo $$
```

```bash
echo $0
```

---

## Notes

| Command | Purpose |
|---------|----------|
| `ps $$` | Shows the current shell process |
| `echo $$` | Prints the PID of the current shell |
| `echo $0` | Shows how the shell was started |

---

## Student Observation

Write down:

```text
Current Shell PID:
Shell Name:
```

---

# Task 5 - Explore the /etc Configuration Directory

## Question

Which directory largely contains configuration directories and files?

---

## Run:

```bash
ls -l /etc
```

```bash
cd /etc
```

```bash
ls
```

---

## Notes

The `/etc` directory contains important system-wide configuration files.

Examples include:

- `/etc/profile`
- `/etc/bashrc`
- `/etc/passwd`
- `/etc/shadow`
- `/etc/group`
- `/etc/shells`

---

# Task 6 - Read the /etc/shells File

## Question

The configuration directory `/etc` has a file called `shells`.

How can you view this file in read-only mode?

---

## Method 1 - Using Absolute Path

Run:

```bash
cat /etc/shells
```

---

## Method 2 - Using Relative Path

Run:

```bash
cd /etc
```

```bash
pwd
```

```bash
cat shells
```

---

## Notes

An absolute path starts from `/`.

Example:

```text
/etc/shells
```

A relative path starts from your current directory.

Example:

```text
shells
```

when you are already inside:

```text
/etc
```

---

# Task 7 - Practice the ping Command

## Question

What does the `ping` command teach us?

---

## Run:

```bash
ping google.com
```

```bash
ping -c 5 google.com
```

```bash
ping 8.8.8.8
```

---

## Important Note

To stop a running command such as continuous `ping`, press:

```text
Ctrl + C
```

This interrupts the process and returns you to the command line prompt.

---

## Notes

The `ping` command helps test:

- Network connectivity
- DNS resolution
- Internet access
- Packet response time
- Whether a remote host is reachable

---

# Task 8 - Basic Troubleshooting Commands

## Question

As a Linux System Administrator, whenever you solve a problem, run the following commands and think carefully about why each command is useful.

---

## Run:

```bash
date
```

```bash
uptime
```

```bash
hostname
```

```bash
whoami
```

```bash
pwd
```

```bash
cd ~
```

---

## Notes

| Command | Why It Is Useful |
|---------|------------------|
| `date` | Confirms current system date/time |
| `uptime` | Shows how long the system has been running |
| `hostname` | Shows the machine name |
| `whoami` | Shows which user you are logged in as |
| `pwd` | Shows your current directory |
| `cd ~` | Takes you to your home directory |

---

# Task 9 - Identify Global Initialization Files

## Question

What are the two major Global Initialization files?

---

## Run:

```bash
cat /etc/profile
```

```bash
cat /etc/bashrc
```

---

## Notes

| File | Purpose |
|------|----------|
| `/etc/profile` | Global login shell initialization file |
| `/etc/bashrc` | Global interactive non-login shell initialization file |

These files affect all users on the system.

---

# Task 10 - Backup a Critical Configuration File

## Question

What should you do before changing or deleting any critical configuration file?

---

## Answer

Always take a backup first.

---

## Create a Backup Using Absolute Path

Run:

```bash
cp -r /etc/profile /etc/profile_bak
```

---

## Verify Backup

Run:

```bash
cd /etc
```

```bash
ls
```

You should see:

```text
profile
profile_bak
```

---

## Important Warning

Do **NOT** delete:

```text
/etc/profile
```

This is a critical system configuration file.

---

## Delete the Backup File

Since `profile_bak` is a file, use:

```bash
rm /etc/profile_bak
```

---

## Important Correction

Do **not** use `rmdir` for `profile_bak` because it is a file, not a directory.

`rmdir` is used only for empty directories.

---

# Final Review Questions

1. What command shows the kernel version?
2. What command shows the operating system version?
3. What is PID 1?
4. Why is `systemd` important?
5. What command shows your current shell?
6. What command shows your current shell PID?
7. What is the purpose of `/etc`?
8. What is the difference between an absolute path and a relative path?
9. What does `ping` test?
10. How do you stop a running command like `ping`?
11. What are the two major global initialization files?
12. Why should you backup configuration files before changing them?
13. What is the difference between `rm` and `rmdir`?

---

# Lab Summary

In this lab, you practiced:

- Checking kernel version
- Checking operating system version
- Verifying `systemd` as PID 1
- Identifying your current shell
- Finding your shell PID
- Exploring `/etc`
- Reading `/etc/shells`
- Understanding absolute and relative paths
- Using `ping`
- Stopping a running process with `Ctrl + C`
- Running basic troubleshooting commands
- Reading global initialization files
- Backing up important configuration files safely

---

# Final Note

As a Linux System Administrator, always remember:

- Know where you are: `pwd`
- Know who you are: `whoami`
- Know what system you are on: `hostname`
- Know the time: `date`
- Know how long the system has been running: `uptime`
- Always backup configuration files before editing them

---