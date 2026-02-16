# Day 10 – File Permissions & File Operations Challenge

## 📌 Objective

Today’s goal was to master file creation, reading, and permission management in Linux.

This challenge helped me understand:
- How to create and edit files
- How to read files using different commands
- How Linux permissions work (rwx model)
- How to modify permissions using chmod
- How permission errors occur and how to fix them

---

# 📂 Files Created

## 1️⃣ devops.txt
Created using:
```bash
touch devops.txt
```

## 2️⃣ notes.txt
Created using:
```bash
echo "Linux permissions practice" > notes.txt
```

## 3️⃣ script.sh
Created using:
```bash
vim script.sh
```

Content inside `script.sh`:
```bash
echo "Hello DevOps"
```

Verified files:
```bash
ls -l
```

---

# 📖 Reading Files

## Read notes.txt
```bash
cat notes.txt
```

## Open script.sh in read-only mode
```bash
vim -R script.sh
```

## First 5 lines of /etc/passwd
```bash
head -n 5 /etc/passwd
```

## Last 5 lines of /etc/passwd
```bash
tail -n 5 /etc/passwd
```

---

# 🔐 Understanding Permissions

Permission format:
```
rwxrwxrwx
|  |  |
U  G  O
```

- r = 4
- w = 2
- x = 1

Checked current permissions:
```bash
ls -l devops.txt notes.txt script.sh
```

Example Output:
```
-rw-r--r-- devops.txt
-rw-r--r-- notes.txt
-rw-r--r-- script.sh
```

Meaning:
- Owner: read & write
- Group: read only
- Others: read only
- No execute permission initially

---

# 🔧 Permission Changes

## 1️⃣ Make script.sh Executable

```bash
chmod +x script.sh
```

Run it:
```bash
./script.sh
```

Output:
```
Hello DevOps
```

Verified:
```bash
ls -l script.sh
```

Now:
```
-rwxr-xr-x
```

---

## 2️⃣ Make devops.txt Read-Only

```bash
chmod a-w devops.txt
```

Verified:
```bash
ls -l devops.txt
```

Now:
```
-r--r--r--
```

---

## 3️⃣ Set notes.txt to 640

```bash
chmod 640 notes.txt
```

Meaning:
- Owner: read + write
- Group: read
- Others: no access

Verified:
```bash
ls -l notes.txt
```

Now:
```
-rw-r-----
```

---

## 4️⃣ Create Directory project/ with 755

```bash
mkdir project
chmod 755 project
```

Verified:
```bash
ls -ld project
```

Now:
```
drwxr-xr-x
```

Meaning:
- Owner: full access
- Group: read & execute
- Others: read & execute

---

# 🧪 Testing Permissions

## 1️⃣ Try Writing to Read-Only File

```bash
echo "test" >> devops.txt
```

Error:
```
Permission denied
```

---

## 2️⃣ Try Executing Without Execute Permission

Before adding +x:
```bash
./script.sh
```

Error:
```
Permission denied
```

After adding +x → Works successfully.

---

# 🧰 Commands Used

- touch
- echo
- vim
- cat
- head
- tail
- chmod +x
- chmod 640
- chmod a-w
- mkdir
- ls -l
- ls -ld

---

# 🎯 What I Learned

- File permissions control system security.
- Execute permission is required to run scripts.
- Numeric permission model (755, 640) is efficient.
- Removing write permission makes file read-only.
- Directories require execute (x) permission to access.

---

# 🚀 Why This Matters in DevOps

In production:

- Scripts must have correct execute permissions.
- Configuration files must be protected.
- Incorrect permissions can cause deployment failures.
- Secure systems depend on proper access control.

Understanding permissions prevents:
- Security breaches
- Accidental file modifications
- Application crashes due to access issues

---

# 🔥 Key Takeaway

> Linux permissions are the foundation of system security and DevOps reliability.

---

#90DaysOfDevOps  
#DevOpsKaJosh  
#TrainWithShubham
