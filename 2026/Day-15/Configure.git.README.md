# Practice Lab – Connecting Local Host (Laptop) to GitHub Repository
> May 13th, 2026 - Day 15

This Practice Lab will guide students on how to connect their Local Host (Laptop/Desktop) to a remote GitHub Repository using SSH Keys.

---

# Table of Contents

| Task | Title |
|------|--------|
| 1 | [Generate SSH Keys](#task-1---generate-ssh-keys) |
| 2 | [Start the SSH Agent](#task-2---start-the-ssh-agent) |
| 3 | [Add the SSH Private Key](#task-3---add-the-ssh-private-key) |
| 4 | [Copy the Public SSH Key](#task-4---copy-the-public-ssh-key) |
| 5 | [Add SSH Key to GitHub](#task-5---add-ssh-key-to-github) |
| 6 | [Final Note](#final-note) |

---

# Task 1 - Generate SSH Keys

## Objective

Generate SSH public and private keys for GitHub authentication.

---

## Run the Following Command

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

> NOTE: Replace `"your_email@example.com"` with your actual email address.

---

## Example

```bash
ssh-keygen -t rsa -b 4096 -C "nadeem.siddiqi@nit.academy"
```

---

## Verify Your Git Username

Run:

```bash
git config user.name
```

## Example Output

```bash
mike.mill
```

---

## Another Example

```bash
ssh-keygen -t rsa -b 4096 -C "mike.mill@adptech.com"
```

---

# Task 2 - Start the SSH Agent

## Objective

Start the SSH authentication agent in the background.

---

## Run:

```bash
eval "$(ssh-agent -s)"
```

## Example Output

```bash
Agent pid 459
```

---

# Task 3 - Add the SSH Private Key

## Objective

Add your SSH private key to the SSH agent.

---

## Run:

```bash
ssh-add ~/.ssh/id_rsa
```

## Example Output

```bash
Identity added: /c/Users/nsidd/.ssh/id_rsa (mike.mill@adptech.com)
```

---

## IMPORTANT NOTE

If your SSH private key file has a different name such as `id_ed25519`, replace `id_rsa` with your actual key filename.

Example:

```bash
ssh-add ~/.ssh/id_ed25519
```

---

# Task 4 - Copy the Public SSH Key

## Objective

Copy the SSH public key so it can be added to GitHub.

---

## Run:

```bash
clip < ~/.ssh/id_rsa.pub
```

---

## Next Steps

1. Open **Notepad**
2. Press:

```text
Ctrl + V
```

3. Verify that your SSH public key has been pasted successfully.

---

# Task 5 - Add SSH Key to GitHub

## Objective

Add your SSH public key to your GitHub account.

---

## Follow the Steps Below

### Step 1

Click on the **Top Right Profile Icon** in GitHub.

---

### Step 2

Select:

```text
Settings
```

---

### Step 3

Click:

```text
SSH and GPG Keys
```

---

### Step 4

Click:

```text
New SSH Key
```

---

## Fill in the Required Information

### 1. Add Title

Example:

```text
My Laptop SSH Key
```

---

### 2. Add Description (Optional)

Example:

```text
Windows Laptop GitHub SSH Access
```

---

### 3. Paste the SSH Public Key

Press:

```text
Ctrl + V
```

---

### 4. Click:

```text
Add SSH Key
```

---

# Final Note

Congratulations!

You are now ready to:

- Push code to GitHub
- Pull repositories from GitHub
- Clone repositories securely using SSH
- Connect your Local PC to a Remote GitHub Repository

---

# Recommended Practice

## Test Your GitHub SSH Connection

Run:

```bash
ssh -T git@github.com
```

## Expected Output

```bash
Hi username! You've successfully authenticated...
```

---

# Final Reflection Questions

1. What is the purpose of SSH keys?
2. Why is SSH more secure than passwords?
3. What does the SSH Agent do?
4. Difference between Public Key and Private Key?
5. Why do developers use GitHub SSH authentication?

---