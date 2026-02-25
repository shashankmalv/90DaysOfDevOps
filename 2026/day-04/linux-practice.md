# Linux Day 04 – Quick Revision Notes  
## Topic: Processes & Services (systemd)

---

## 🔹 Processes (What is running?)

### Important Commands
- `ps -ef` → Snapshot of all running processes
- `pgrep <name>` → Find PID of a process
- `top` → Live CPU & memory usage
- `htop` → (If installed) better interactive top

### Key Points
- Every process has a **PID**
- PID `1` = `systemd` (parent of all services)
- Use `pgrep` instead of `ps | grep` (cleaner)

### Interview Line
> “I use `ps` or `pgrep` to identify processes and `top` to analyze runtime resource usage.”

---

## 🔹 Services (systemd)

### Important Commands
- `systemctl status <service>` → Check health
- `systemctl start <service>` → Start service
- `systemctl stop <service>` → Stop service
- `systemctl restart <service>` → Restart service
- `systemctl list-units --type=service` → Running services

### Key Points
- Services are managed by **systemd**
- Service states: `active`, `inactive`, `failed`
- Most common services: `ssh`, `cron`, `docker`

### Interview Line
> “Linux services are managed by systemd using systemctl commands.”

---

## 🔹 Logs (Troubleshooting)

### Important Commands
- `journalctl -u <service>` → Service logs
- `journalctl -xe` → Recent errors
- `tail -n 50 /var/log/syslog` → System logs

### Key Points
- Logs show **why** a service failed
- Always check logs **before restarting**
- `journalctl` works only on systemd systems

### Interview Line
> “I always check journalctl logs to identify root cause before restarting a service.”

---

## 🔹 Basic Troubleshooting Flow

1. Check service status  
   `systemctl status <service>`
2. Check logs  
   `journalctl -u <service>`
3. Restart service if needed  
   `systemctl restart <service>`
4. Verify process  
   `pgrep <service>`

---

## 🔹 Why This Matters in DevOps

- Production issues need **fast diagnosis**
- Logs = root cause
- Restart without logs = bad practice

---

## 🧠 Memory Tip
**Status → Logs → Restart → Verify**

---

## 📌 Commands to Remember (Must-Know)

```bash
ps -ef
pgrep
top
systemctl status
journalctl
tail
