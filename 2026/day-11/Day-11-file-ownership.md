# Day 11 – File Ownership Challenge (chown & chgrp)

## 📌 Objective

Today’s goal was to master file and directory ownership in Linux.

This challenge helped me understand:
- The difference between file owner and group
- How to change file ownership using `chown`
- How to change file group using `chgrp`
- How to apply recursive ownership changes
- Why ownership is critical in DevOps environments

---

# 🔍 Task 1 – Understanding Ownership

## Checked Ownership

```bash
ls -l
```

Example Output:
```
-rw-r--r-- 1 Ubuntu Ubuntu  0 Feb 10 devops-file.txt
```

Format:
```
-rw-r--r-- 1 owner group size date filename
```

### Difference Between Owner and Group

- **Owner** → The user who controls the file.
- **Group** → A collection of users who share access permissions.

Owner permissions apply to one specific user.  
Group permissions apply to all users inside that group.

---

# 🔹 Task 2 – Basic chown Operations

## Step 1: Create File

```bash
touch devops-file.txt
ls -l devops-file.txt
```

## Step 2: Change Owner to tokyo

```bash
sudo chown tokyo devops-file.txt
```

## Step 3: Change Owner to berlin

```bash
sudo chown berlin devops-file.txt
```

## Verification

```bash
ls -l devops-file.txt
```

Before:
```
Ubuntu Ubuntu
```

After:
```
berlin Ubuntu
```

---

# 🔹 Task 3 – Basic chgrp Operations

## Step 1: Create File

```bash
touch team-notes.txt
ls -l team-notes.txt
```

## Step 2: Create Group

```bash
sudo groupadd heist-team
```

## Step 3: Change Group

```bash
sudo chgrp heist-team team-notes.txt
```

## Verification

```bash
ls -l team-notes.txt
```

Group changed successfully to `heist-team`.

---

# 🔹 Task 4 – Combined Owner & Group Change

## Step 1: Create File

```bash
touch project-config.yaml
```

## Step 2: Change Owner & Group Together

```bash
sudo chown professor:heist-team project-config.yaml
```

## Step 3: Create Directory

```bash
mkdir app-logs
```

## Step 4: Change Ownership of Directory

```bash
sudo chown berlin:heist-team app-logs
```

## Verification

```bash
ls -l
```

---

# 🔹 Task 5 – Recursive Ownership

## Step 1: Create Directory Structure

```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans
touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```

## Step 2: Create Group

```bash
sudo groupadd planners
```

## Step 3: Recursive Ownership Change

```bash
sudo chown -R professor:planners heist-project/
```

## Verification

```bash
ls -lR heist-project/
```

All files and subdirectories successfully updated.

---

# 🔹 Task 6 – Practice Challenge

## Step 1: Create Users (if not already created)

```bash
sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m nairobi
```

## Step 2: Create Groups

```bash
sudo groupadd vault-team
sudo groupadd tech-team
```

## Step 3: Create Directory & Files

```bash
mkdir bank-heist
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

## Step 4: Set Different Ownership

```bash
sudo chown tokyo:vault-team bank-heist/access-codes.txt
sudo chown berlin:tech-team bank-heist/blueprints.pdf
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```

## Verification

```bash
ls -l bank-heist/
```

Ownership successfully configured.

---

# 🧰 Commands Used

- ls -l
- chown
- chgrp
- chown owner:group
- chown -R
- useradd
- groupadd
- mkdir -p
- touch

---

# 🎯 What I Learned

- File ownership determines who controls a file.
- `chown` changes owner, `chgrp` changes group.
- `chown owner:group` changes both in one command.
- `-R` applies ownership recursively to directories.
- Proper ownership prevents permission conflicts in production.

---

# 🚀 Why This Matters in DevOps

In real-world DevOps:

- Applications must run under specific users.
- Log files require correct ownership.
- CI/CD tools need controlled access.
- Incorrect ownership can break deployments.
- Containers rely heavily on correct file ownership.

Understanding ownership ensures secure, stable systems.

---

# 🔥 Key Takeaway

> Ownership + Permissions = Secure Linux Systems

---

#90DaysOfDevOps  
#DevOpsKaJosh  
#TrainWithShubham
