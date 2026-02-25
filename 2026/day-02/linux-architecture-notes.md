# Day 2 - Linux Architecture, Processes, and systemd

## 🏗 Core Components of Linux

- **Kernel**: The heart of the OS. It manages hardware (CPU, Memory, Disk) and acts as an intermediary between hardware and applications.

- **User Space**: The environment where user applications, libraries, and shells run. It communicates with the Kernel via System Calls.

- **Init System (systemd)**: The first process started by the kernel (PID 1). It is responsible for initializing the system and managing all other services/daemons.

## 🔄 Process Management & States

Every task in Linux is a process assigned a unique PID (Process ID). Processes move through different states:

- **Running (R):** Actively using the CPU.

- **Sleeping (S):** Waiting for an event or resource (Idle).

- **Stopped (T):** Suspended by a user or another process.

- **Zombie (Z):** A process that has completed execution but still has an entry in the process table because its parent hasn't acknowledged it.

## ⚙️ The Role of systemd

`systemd` is the modern init system and service manager. It:

- Starts services in parallel to speed up boot time.

- Tracks processes using control groups (cgroups).

- Provides `systemctl` to start, stop, and monitor services.

## 🛠 Essential Daily Commands

| Command              | Purpose |
|----------------------|---------|
| `top / htop`         | Real-time monitoring of system resources and processes |
| `ps aux`             | Lists all running processes with user details and resource usage |
| `systemctl status <name>` | Checks the health and logs of a specific service |
| `kill -15 <PID>`     | Gracefully terminates a process (SIGTERM) |
| `df -h`              | Displays disk space usage in human-readable format |

## 💡 Production Best Practices

- **Graceful Shutdowns:** Always use `kill -15` before `kill -9 `to allow applications to save data and close connections.

- **Resource Monitoring:** Use `htop `to identify "Zombie" or "Defunct" processes that might indicate a bug in the application's parent-child logic.

- **Log Analysis:** When a service fails, use `journalctl -u <service_name>` to view the specific logs managed by systemd.
