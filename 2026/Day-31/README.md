# Linux Administration Bootcamp
# Day 30/31 – Login Process, systemd, Shells and Initialization Files
## June 6/7th, 2026

> Based on Class Notes and Slides by NIT Academy 

---

# Objective

By the end of this class students will be able to:

1. Understand what happens during the Linux login process.
2. Identify the first process running on a Linux system (PID 1).
3. Understand the relationship between PID and PPID.
4. Identify their current shell and shell PID.
5. Understand the difference between Login Shell and Non-Login Shell.
6. Understand how Bash initialization files work.
7. Identify Global and User initialization files.
8. Understand how the PATH variable works.
9. Create custom commands using PATH.
10. Understand the purpose of `.bash_logout`.

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

When a Linux system starts:

```text
Kernel
   │
   ▼
systemd (PID 1)
   │
   ▼
sshd
   │
   ▼
bash
   │
   ▼
Initialization Files
   │
   ▼
User Prompt
```

Every process in Linux has a parent process.

Processes do not appear automatically.

Almost every process is created (forked) by another process.

---

# Linux Login Process

When a user logs into Linux using:

- SSH
- Guacamole
- Console Login
- Virtual Terminal

Linux performs the following steps:

### Step 1

Linux Kernel starts.

### Step 2

Kernel starts:

```bash
systemd
```

which becomes:

```text
PID 1
```

### Step 3

systemd starts:

```bash
sshd
```

### Step 4

sshd authenticates the user.

### Step 5

sshd launches:

```bash
bash
```

### Step 6

bash reads initialization files.

### Step 7

User receives a prompt:

```bash
[root@server ~]#
```

---

# Understanding PID and PPID

## PID

PID means:

```text
Process ID
```

Every process has a unique number.

Example:

```text
PID 230948 = bash
```

---

## PPID

PPID means:

```text
Parent Process ID
```

This identifies which process launched another process.

Example:

```text
sshd --> bash
```

Therefore:

```text
sshd = PPID
bash = PID
```

---

# Task 1 – Verify systemd (PID 1)

## Objective

Verify the first process running on Linux.

### Run

```bash
ps 1
```

### Expected Output

```text
PID TTY      STAT   TIME COMMAND
1   ?        Ss     0:16 /usr/lib/systemd/systemd
```

---

## Discussion

Questions:

1. What is PID 1?
2. Why is systemd important?
3. What happens if PID 1 crashes?

---

# Task 2 – Identify Your Current Shell

## Objective

Determine which shell you are using.

### Run

```bash
echo $SHELL
```

Example:

```text
/bin/bash
```

---

### Check Login Shell Status

Run:

```bash
shopt login_shell
```

Example:

```text
login_shell on
```

---

### Check Your Shell PID

Run:

```bash
echo $$
```

Example:

```text
230948
```

---

### Verify Using ps

Run:

```bash
ps $$
```

Example:

```text
PID TTY      STAT TIME COMMAND
230948 pts/0 Ss   0:00 -bash
```

---

## Discussion

Questions:

1. What is your shell PID?
2. Why does bash appear with a "-" sign?

Example:

```text
-bash
```

---

# Task 3 – Understand Process Hierarchy

## Objective

View parent-child relationships.

### Check Parent Process

Run:

```bash
ps -fp $PPID
```

Example:

```text
sshd: root@pts/0
```

---

### Display Process Tree

Run:

```bash
pstree -p $PPID
```

Example:

```text
sshd
 └── sshd
      └── bash
           └── pstree
```

---

## Discussion

Questions:

1. Which process launched bash?
2. Which process launched sshd?
3. What launched systemd?

---

# Login Shell vs Non-Login Shell

## Login Shell

Created when Linux authenticates you.

Examples:

- SSH Login
- Console Login
- Guacamole Login

Files executed:

```text
/etc/profile
~/.bash_profile
~/.profile
```

---

## Non-Login Shell

Created when already logged in and starting another shell.

Example:

```bash
/bin/bash
```

or

```bash
bash
```

Files executed:

```text
/etc/bashrc
~/.bashrc
```

---

## Comparison

| Login Shell | Non-Login Shell |
|------------|----------------|
| Authentication required | Already authenticated |
| Reads /etc/profile | Does not read /etc/profile |
| Reads .bash_profile | Reads .bashrc |
| First shell after login | Additional shell |

---

# Initialization Files

Initialization files configure:

- PATH
- Prompt
- Aliases
- Functions
- Environment Variables

These files execute before the prompt appears.

---

# Global vs User Initialization Files

## Global Files

Affect all users.

Location:

```text
/etc/profile
/etc/bashrc
```

Only root should modify these files.

---

## User Files

Affect only one user.

Examples:

```text
~/.bash_profile
~/.bashrc
~/.bash_logout
```

Users can modify their own files.

---

# Task 4 – Examine Initialization Files

## Check Global Files

Run:

```bash
ls -l /etc/profile
ls -l /etc/bashrc
```

---

## Read Global Files

Run:

```bash
cat /etc/profile
cat /etc/bashrc
```

---

## View User Files

Run:

```bash
ls -la ~ | grep bash
```

---

## Discussion

Questions:

1. Which files affect all users?
2. Which files affect only one user?

---

# PATH Variable

PATH tells Linux where commands are located.

Run:

```bash
echo $PATH
```

Example:

```text
/root/.local/bin:/root/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin
```

---

# How PATH Works

When you type:

```bash
date
```

Bash searches directories from left to right.

Example:

```text
/root/bin
/usr/local/bin
/usr/sbin
/usr/bin
```

When it finds:

```text
/usr/bin/date
```

it executes the command.

---

# Task 5 – Examine PATH

## Display PATH

Run:

```bash
echo $PATH
```

---

## Locate Commands

Run:

```bash
whereis date
whereis uptime
whereis ls
whereis mkdir
whereis touch
```

---

## Discussion

Questions:

1. Where is the date command located?
2. Where is the ls command located?
3. What happens if a command is not found in PATH?

---

# Task 6 – Create a Custom Global Command

## Objective

Create your own Linux command.

### Create Directory

Run:

```bash
mkdir -p /getstuff/bin
```

---

### Create Script

Run:

```bash
echo -e '#!/bin/bash\necho "Success! The getstuff application is running!"' > /getstuff/bin/hello
```

---

### Make Executable

Run:

```bash
chmod +x /getstuff/bin/hello
```

---

### Test Command

Run:

```bash
hello
```

Expected:

```text
command not found
```

---

### Add Directory to PATH

Run:

```bash
echo 'PATH=$PATH:/getstuff/bin ; export PATH' >> ~/.bashrc
```

---

### Reload Bash Configuration

Run:

```bash
source ~/.bashrc
```

---

### Test Again

Run:

```bash
hello
```

Expected:

```text
Success! The getstuff application is running!
```

---

# Understanding .bash_logout

The file:

```text
~/.bash_logout
```

runs when a user exits a login shell.

Examples:

- Clear screen
- Display goodbye message
- Log logout time

---

# Task 7 – Test Initialization Files

## Create User

Run:

```bash
useradd john
passwd john
```

---

## Modify Global Login File

Run:

```bash
vi /etc/profile
```

Add:

```bash
echo "/etc/profile executed"
```

Save:

```text
:wq!
```

---

## Login as john

Observe:

```text
/etc/profile executed
```

---

## Discussion

Questions:

1. Which file displayed the message?
2. Why did all users see the message?
3. What would happen if the change was made in .bashrc instead?

---

# Review Questions

1. What is PID 1?
2. What is the role of systemd?
3. What is the difference between PID and PPID?
4. What is a Login Shell?
5. What is a Non-Login Shell?
6. What files are executed during login?
7. What is the purpose of .bashrc?
8. What is the purpose of .bash_profile?
9. What is the purpose of .bash_logout?
10. What is PATH?
11. Why does Linux search PATH from left to right?
12. What command displays your shell PID?
13. What command displays the current shell?
14. What command reloads .bashrc?
15. What command displays the process tree?

---

# Lab Summary

In this class you learned:

- Linux login process.
- Why systemd is PID 1.
- How sshd launches bash.
- Difference between PID and PPID.
- Difference between Login Shell and Non-Login Shell.
- Global and User initialization files.
- How PATH works.
- How to create custom commands.
- How .bash_logout works.
- How Linux builds a user environment before presenting the command prompt.

These concepts are fundamental for:

- RHCSA
- RHCE
- Linux Administration
- DevOps
- System Engineering
- Infrastructure Operations

---
# End of Lab