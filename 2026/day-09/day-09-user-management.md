# Day 09 – Linux User & Group Management Challenge

## 📌 Objective

Today’s goal was to practice Linux user and group management through hands-on challenges.

This lab helped me understand:
- How to create users with home directories
- How to create and manage groups
- How to assign users to multiple groups
- How to configure shared directories with proper permissions

User and permission management is critical in production servers for security and collaboration.

---

# 👥 Users & Groups Created

## Users:
- tokyo
- berlin
- professor
- nairobi

## Groups:
- developers
- admins
- project-team

---

# 🔹 Task 1 – Create Users

### Commands Used:

```bash
sudo useradd -m tokyo
sudo passwd tokyo

sudo useradd -m berlin
sudo passwd berlin

sudo useradd -m professor
sudo passwd professor
```

### Verification:

```bash
cat /etc/passwd | grep tokyo
ls -l /home/
```

✅ Confirmed home directories were created.

---

# 🔹 Task 2 – Create Groups

### Commands Used:

```bash
sudo groupadd developers
sudo groupadd admins
```

### Verification:

```bash
cat /etc/group | grep developers
cat /etc/group | grep admins
```

---

# 🔹 Task 3 – Assign Users to Groups

### Commands Used:

```bash
sudo usermod -aG developers tokyo

sudo usermod -aG developers berlin
sudo usermod -aG admins berlin

sudo usermod -aG admins professor
```

### Verification:

```bash
groups tokyo
groups berlin
groups professor
```

✅ Verified correct group memberships.

---

# 🔹 Task 4 – Shared Directory Setup

### Step 1: Create Directory

```bash
sudo mkdir -p /opt/dev-project
```

### Step 2: Change Group Owner

```bash
sudo chgrp developers /opt/dev-project
```

### Step 3: Set Permissions

```bash
sudo chmod 775 /opt/dev-project
```

### Step 4: Test File Creation

```bash
sudo -u tokyo touch /opt/dev-project/test1.txt
sudo -u berlin touch /opt/dev-project/test2.txt
```

### Verification:

```bash
ls -ld /opt/dev-project
ls -l /opt/dev-project
```

✅ Both users successfully created files.

---

# 🔹 Task 5 – Team Workspace Challenge

### Step 1: Create User

```bash
sudo useradd -m nairobi
sudo passwd nairobi
```

### Step 2: Create Group

```bash
sudo groupadd project-team
```

### Step 3: Add Users to Group

```bash
sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo
```

### Step 4: Create Workspace Directory

```bash
sudo mkdir -p /opt/team-workspace
sudo chgrp project-team /opt/team-workspace
sudo chmod 775 /opt/team-workspace
```

### Step 5: Test File Creation

```bash
sudo -u nairobi touch /opt/team-workspace/work.txt
```

### Verification:

```bash
ls -ld /opt/team-workspace
ls -l /opt/team-workspace
groups nairobi
```

✅ Confirmed correct group access and permissions.

---

# 🧰 Commands Used

- useradd -m
- passwd
- groupadd
- usermod -aG
- groups
- chgrp
- chmod 775
- mkdir -p
- sudo -u
- ls -ld

---

# ⚠️ Challenges Faced

### 1️⃣ Permission Denied
Cause: Incorrect directory permissions  
Solution: Adjusted group ownership and used chmod 775

### 2️⃣ User Not Getting Group Access Immediately
Cause: Group membership requires new session  
Solution: Logged out and logged back in

---

# 🎯 What I Learned

- Users must belong to correct groups to access shared resources
- chmod 775 allows group collaboration
- chgrp changes group ownership
- usermod -aG safely adds users to multiple groups
- Proper permission setup is critical for secure production systems

---

# 🚀 Why This Matters in DevOps

In real DevOps environments:

- Teams need shared access to deployment directories
- CI/CD users need controlled permissions
- Production servers must enforce strict user separation
- Incorrect permissions can cause downtime or security risks

Understanding user & group management ensures secure and structured server environments.

---

# 🔥 Key Takeaway

> Security and collaboration in Linux are controlled by Users, Groups, and Permissions.

---

#90DaysOfDevOps  
#DevOpsKaJosh  
#TrainWithShubham
