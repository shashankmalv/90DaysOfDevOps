# Day 07 – Linux File System Hierarchy & Scenario-Based Practice

## 📌 Objective

Today’s goal was to understand the Linux File System Hierarchy and practice real-world troubleshooting scenarios like a DevOps engineer.

This session helped me:
- Understand where important files live in Linux
- Identify logs, configs, binaries, and user data locations
- Follow structured troubleshooting steps
- Think logically during production incidents

---

# 🗂 Part 1 – Linux File System Hierarchy

## 1️⃣ `/` (Root Directory)

- The starting point of the entire file system.
- Everything in Linux begins from `/`.

**Command Run:**
```bash
ls -l /
```

**Observed:**
Directories like `home`, `etc`, `var`, `usr`, `bin`

**I would use this when:**  
Navigating the system structure or checking mounted directories.

---

## 2️⃣ `/home`

- Contains user home directories.
- Each normal user has a folder inside `/home`.

**Command Run:**
```bash
ls -l /home
```

**Observed:**
User directories like `shashank`

**I would use this when:**  
Managing user files or debugging user-level scripts.

---

## 3️⃣ `/root`

- Home directory for the root user.
- Only accessible with sudo privileges.

**Command Run:**
```bash
ls -l /root
```

**Observed:**
Root-specific configuration files

**I would use this when:**  
Working as system administrator or handling root-owned scripts.

---

## 4️⃣ `/etc`

- Contains system configuration files.
- Most service configs are stored here.

**Command Run:**
```bash
ls -l /etc
cat /etc/hostname
```

**Observed:**
Files like `hostname`, `hosts`, `passwd`

**I would use this when:**  
Editing service configs or checking system settings.

---

## 5️⃣ `/var/log` (Very Important)

- Stores system and application log files.
- Critical for DevOps troubleshooting.

**Command Run:**
```bash
du -sh /var/log/* 2>/dev/null | sort -h | tail -5
```

**Observed:**
Log directories like `syslog`, `journal`

**I would use this when:**  
Investigating production issues or service failures.

---

## 6️⃣ `/tmp`

- Stores temporary files.
- Often cleared on reboot.

**Command Run:**
```bash
ls -l /tmp
```

**I would use this when:**  
Debugging temporary script outputs.

---

## 7️⃣ `/bin`

- Essential system binaries.
- Basic commands like `ls`, `cp`, `mv`.

**I would use this when:**  
Verifying system command availability.

---

## 8️⃣ `/usr/bin`

- User-level command binaries.
- Most installed commands live here.

**I would use this when:**  
Checking installed applications.

---

## 9️⃣ `/opt`

- Optional or third-party applications.
- Custom software installations.

**I would use this when:**  
Installing enterprise applications manually.

---

# 🔥 Part 2 – Scenario-Based Practice

---

## ✅ Scenario 1 – Service Not Starting (myapp)

### Step 1:
```bash
systemctl status myapp
```
Why: Check if service is failed, inactive, or running.

### Step 2:
```bash
journalctl -u myapp -n 50
```
Why: Check last 50 log entries for error messages.

### Step 3:
```bash
systemctl is-enabled myapp
```
Why: Verify if service is enabled on boot.

### Step 4:
```bash
systemctl restart myapp
```
Why: Try restarting after checking logs.

**What I Learned:**  
Always check status → logs → enable state → restart.

---

## ✅ Scenario 2 – High CPU Usage

### Step 1:
```bash
top
```
Why: View live CPU usage.

### Step 2:
```bash
ps aux --sort=-%cpu | head -10
```
Why: Identify top CPU-consuming processes.

### Step 3:
```bash
kill -9 <PID>
```
Why: Stop problematic process if required.

**What I Learned:**  
Identify before killing. Never randomly stop processes.

---

## ✅ Scenario 3 – Finding Service Logs (docker)

### Step 1:
```bash
systemctl status docker
```
Why: Confirm service state.

### Step 2:
```bash
journalctl -u docker -n 50
```
Why: Check recent logs.

### Step 3:
```bash
journalctl -u docker -f
```
Why: Follow logs in real-time.

**What I Learned:**  
Systemd services use journald logs.

---

## ✅ Scenario 4 – File Permission Issue

### Step 1:
```bash
ls -l /home/user/backup.sh
```
Why: Check permission bits.

### Step 2:
```bash
chmod +x /home/user/backup.sh
```
Why: Add execute permission.

### Step 3:
```bash
./backup.sh
```
Why: Verify script execution.

**What I Learned:**  
Scripts require execute permission (`x`).

---

# 🚀 Key Learnings from Day 07

- Logs are usually in `/var/log`
- Config files live in `/etc`
- Services should be checked using `systemctl`
- Troubleshooting requires logical step-by-step thinking
- Never guess — always check logs

---

# 💡 Why This Matters in DevOps

In real DevOps environments:

- Production failures require fast log analysis
- High CPU issues must be identified quickly
- Permission errors break deployments
- Service misconfigurations cause downtime

Understanding file structure + troubleshooting flow makes incident handling faster and structured.

---

# 🔑 Most Important Habit I Learned

> Always check service status and logs before taking action.

---

#90DaysOfDevOps  
#DevOpsKaJosh  
#TrainWithShubham
