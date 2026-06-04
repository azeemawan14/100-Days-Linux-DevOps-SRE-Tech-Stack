# Linux Lab 22 – Deleting Directories and Files
> May 30th 2026 (30th May)

## Objective

In this lab, you will learn how to:

1. Continue from the previous lab (Day 21).
2. Check directories and files that were created.
3. Delete empty directories.
4. Delete files and non-empty directories.
5. Delete all contents under a directory.

---

# Task 1 – Check Directories and Files

## Objective

Display all directories and files created in the previous lab.

### Run:

```bash
ls -l /var/opt/
```

### Questions

- What directories do you see?
- What files do you see?
- Which items were created in the previous lab?

---

# Task 2 – Delete an Empty Directory Using `rmdir`

## Objective

Delete an empty directory.

### Important Note

The `rmdir` command can only remove **empty directories**.

If a directory contains files or subdirectories, `rmdir` will fail and display an error.

### Run:

```bash
rmdir /var/opt/images
```

### Verify:

```bash
ls -l /var/opt/
```

---

## Create a File Inside the Projects Directory

Now let us place a file inside the projects directory and test whether `rmdir` still works.

### Change Directory

```bash
cd /var/opt/projects
```

### Verify Current Location

```bash
pwd
```

### Verify Directory is Empty

```bash
ls -l
```

There should be no files inside the directory.

### Create a File

```bash
touch contacts.css
```

### Verify

```bash
ls -l
```

You should now see:

```text
contacts.css
```

### Return to Home Directory

```bash
cd
```

### Attempt to Remove the Directory

```bash
rmdir /var/opt/projects
```

### Expected Result

You should receive an error similar to:

```text
rmdir: failed to remove '/var/opt/projects': Directory not empty
```

### Observation

`rmdir` cannot remove directories that contain files.

---

# Task 3 – Delete a Non-Empty Directory

## Objective

Delete a directory and all files inside it.

### First Confirm Your Current Location

```bash
cd
pwd
```

### View Contents of Home Directory

```bash
ls -l
```

### Deleting Using an Absolute Path

To remove a directory and everything inside it:

```bash
rm -r
```

To force removal without prompts:

```bash
rm -rf
```

### Run:

```bash
rm -rf /var/opt/projects
```

### Verify

```bash
ls -l /var/opt/
```

### Observation

The directory and all files inside it should now be removed.

---

# Task 4 – Create and Delete a Directory Using a Relative Path

## Objective

Create and remove a directory using a Relative Path.

### Verify Current Location

```bash
pwd
```

### Return to Root's Home Directory

```bash
cd
pwd
```

Expected location:

```text
/root
```

### Change to the `/var/opt` Directory

```bash
cd /var/opt
```

### Verify

```bash
pwd
```

Expected location:

```text
/var/opt
```

### Create a New Directory

```bash
mkdir -p docs
```

### Verify

```bash
ls -l
```

You should now see:

```text
docs
```

### Delete Using a Relative Path

Since you are already inside `/var/opt`, you can delete the directory using its relative name.

### Run:

```bash
rm -rf docs
```

### Verify

```bash
ls -l
```

### Note

We did **not** run:

```bash
rm -rf /var/opt/docs
```

because we were already located inside `/var/opt`.

This is an example of using a **Relative Path**.

---

# Task 5 – Delete Everything Under `/var/opt`

## Objective

Remove all files and directories located inside `/var/opt`.

### Warning

This command removes everything inside `/var/opt` but leaves the `/var/opt` directory itself intact.

### Run:

```bash
rm -rf /var/opt/*
```

### Verify

```bash
ls -la /var/opt
```

### Observation

All files and directories inside `/var/opt` should now be removed.

---

# Review Questions

1. What is the difference between `rmdir` and `rm -rf`?
2. Why did `rmdir` fail when the directory contained a file?
3. What is an Absolute Path?
4. What is a Relative Path?
5. Why was `rm -rf docs` considered a Relative Path command?
6. What does the `-r` option do?
7. What does the `-f` option do?
8. What command removes all contents inside `/var/opt` while keeping the `/var/opt` directory itself?

---
## Lab Summary

Write a short paragraph explaining:

- What you learned in this lab.
- The difference between `rmdir` and `rm -rf`.
- Which command was most useful.
- Which command was new to you.