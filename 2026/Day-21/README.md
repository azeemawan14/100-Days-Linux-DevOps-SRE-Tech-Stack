# Linux Practice Lab – Directories and Files
> Day-21 (29th May, 2026)

### Objective:
>
> Students will learn how to:
>
> 1. Display the current date and time.
> 2. Check system uptime.
> 3. Identify their current location in the Linux filesystem.
> 4. Create directories using both Absolute and Relative Paths.
> 5. Create files using the `touch` command.

---

# Table of Contents

| Task | Description |
|--------|-------------|
| 1 | Display Current Date and Time |
| 2 | Check System Uptime |
| 3 | Check Current Location |
| 4 | Create Directories Using Absolute and Relative Paths |
| 5 | Create Files Using touch |

---

## Task 1 – Display Current Date and Time

### Objective

Display the current system date and time.

### Run:

```bash
date
```

### Questions

1. What date is displayed?
2. What time is displayed?
3. What timezone is your system using?

---

## Task 2 – Check System Uptime

### Objective

Determine how long the system has been running.

### Run:

```bash
uptime
```

### Questions

1. How long has the system been up?
2. How many users are currently logged in?
3. What is the system load average?

---

## Task 3 – Check Your Current Location

### Objective

Determine your current location in the Linux filesystem.

### Run:

```bash
pwd
```

### Questions

1. What directory are you currently in?
2. What does the `pwd` command stand for?

---

## Task 4 – Create Directories Using Absolute and Relative Paths

### Part A – Create a Directory Using an ABSOLUTE PATH

### Objective

Create a directory using the full filesystem path known as "ABSOLUTE PATH" - method

### Run:

```bash
mkdir -p /var/opt/images
```

### Verify the Directory Was Created

Run:

```bash
ls -l /var/opt/
```

### Questions

1. Do you see the directory named `images`?
2. Why is this called an Absolute Path?

---

### Part B – Create a Directory Using a RELATIVE PATH

### Check Your Current Location

Run:

```bash
pwd
```

---

### Return to Your Home Directory

Run:

```bash
cd
```

Verify:

```bash
pwd
```

Expected output (This is what you should see):k Please DO NOT paste the OUTPUT. Read carefully do not make mistakes and rush!

```bash
/root
```

---

### Change to the /var Directory

Run:

```bash
cd /var
```

Verify:

```bash
pwd
```

Expected output:

```bash
/var
```

---

### Enter the "opt" Directory RELATIVE to /var

Run:

```bash
cd opt
```

Verify:

```bash
pwd
```

Expected output:

```bash
/var/opt
```

---

### Create a Directory Using a RELATIVE PATH

Run:

```bash
mkdir -p projects
```

---

### Verify the Directory Was Created

Run:

```bash
ls -l
```

---

### Observation

You should now see:

```text
images
projects
```

---

### Questions

1. Which directory was created using an Absolute Path?
2. Which directory was created using a Relative Path?
3. What is the difference between Absolute and Relative Paths?

---

# Task 5 – Create Files Using the touch Command

## Objective

Create files inside the current directory.

### Verify Your Current Location

Run:

```bash
pwd
```

Expected output:

```bash
/var/opt
```

---

### Create a Summary File

Run:

```bash
touch summary.txt
```

---

### Create Multiple Files

Run:

```bash
touch file{1..5}
```

---

### Verify that the following Files Were Created

Run:

```bash
ls -l
```

---

### Observation

You should now see:

```text
summary.txt
file1
file2
file3
file4
file5
```

---

# Final Questions

1. What does the `date` command do?
2. What information does the `uptime` command provide?
3. What does `pwd` stand for?
4. What is an Absolute Path?
5. What is a Relative Path?
6. What does `mkdir -p` do?
7. What does the `touch` command do?
8. How can you create multiple files with a single command?

---

# Lab Summary

Write a short paragraph in markdown form explaining:

- What you learned in this lab.
- The difference between Absolute and Relative Paths.
- Which command was most useful.
- Which command was new to you.

# RESULTS
1. Go to your Local Repository Day 21. (Make sure it is initialized) and create a README.md (file)
2. Write the Lab Summary in Notepad or OneNote or Word (it does not matter)
3. Paste the "Lab Summary" you have written into "Chatgpt" and ask chatgpt to create a single markdown format of what you have written
4. Copy the markdown format from Chatgpt and paste into README.md
5. Cntrl+S to save 
6. Then Run -> git status -> git add . -> git commit -m "Linux Assignment" -> git push
7. Refresh your NIT Repo on github and refresh to check if this document has been pushed.
8. COPY the URL of your Repo and create a new POST on Linkdin and paste it with some notes to tell the audience what you have written. At the end of your post don't forget to put #NIT #NIT Houston #NIT Nigeria #NIT Pakistan

---