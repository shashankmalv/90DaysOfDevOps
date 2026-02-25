# Linux Troubleshooting Drill – Quick Revision Notes  
## Topic: Evidence-Based Troubleshooting & Runbooks

---

## 🔹 Goal of Today’s Drill
Build a **repeatable troubleshooting habit** by:
- Capturing system health (CPU, memory, disk, network)
- Checking logs before acting
- Writing clear next steps (runbook mindset)

---

## 🔹 What is a Runbook?
A **runbook** is a short checklist used during incidents that includes:
- Exact commands to run
- What you observed
- What to do next if the issue worsens

👉 Purpose: **Reduce panic, guesswork, and downtime**

---

## 🔹 Target Service Concept
- Pick **ONE service/process** (ssh / docker / web app)
- Stick to it for the entire drill
- Observe how system resources behave around it

---

## 🔹 Environment Basics (Baseline)

### Commands
- `uname -a`
- `lsb_release -a` or `cat /etc/os-release`

### Why
- Confirms OS, kernel, architecture
- Important for debugging kernel / OS-specific issues

---

## 🔹 Filesystem Sanity Check

### Commands
- `mkdir /tmp/runbook-demo`
- `cp /etc/hosts /tmp/runbook-demo/`
- `ls -l /tmp/runbook-demo`

### Why
- Confirms disk is writable
- Rules out permission or read-only filesystem issues

---

## 🔹 CPU & Memory Snapshot

### Commands
- `top` / `htop`
- `ps -o pid,pcpu,pmem,comm -p <pid>`
- `free -h`

### What to Look For
- High CPU spikes
- Memory pressure / low free memory
- Specific process consuming resources

---

## 🔹 Disk & IO Snapshot
![alt text](<Screenshot 2026-02-09 212955.png>)
### Commands
- `df -h`
- `du -sh /var/log`
- `vmstat` / `iostat`

### What to Look For
- Disk full conditions
- Rapid log growth
- IO wait indicating disk bottleneck

---

## 🔹 Network Snapshot

![alt text](<Screenshot 2026-02-09 213310.png>)

### Commands
- `ss -tulpn` or `netstat -tulpn`
- `curl -I <service-endpoint>`

### What to Look For
- Service listening on expected port
- Connection errors / timeouts
- Network reachability

---

## 🔹 Logs (Always Before Restart)

### Commands
- `journalctl -u <service> -n 50`
- `tail -n 50 /var/log/<file>.log`

### What to Look For
- Errors, warnings, crashes
- Pattern repeating over time
- Recent changes before failure

---

## 🔹 Troubleshooting Mindset

### Correct Order
1. Observe (CPU / memory / disk / network)
2. Check logs
3. Correlate symptoms
4. Act (restart / config change)

🚫 Restarting without logs = bad practice

---

## 🔹 “If This Worsens” – Next Steps Pattern

Examples:
- Restart service with controlled strategy
- Increase log verbosity
- Capture diagnostics (strace, debug logs)
- Escalate with evidence

---

## 🔹 Why This Matters for DevOps

- Incidents are noisy and time-critical
- A checklist saves minutes
- Evidence-first approach prevents blind restarts
- Builds trust during on-call situations

---

## 🧠 One-Line Interview Summary
> “I follow a runbook-based approach: capture system health, analyze logs, then take controlled action.”

---

## 📌 Must-Remember Commands

```bash
uname -a
top
ps
free -h
df -h
ss -tulpn
journalctl
tail
