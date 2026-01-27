# Day 3: Linux Command Cheat Sheet for DevOps

## 📊 Process & Resource Management

- `top`: Displays real-time system resource usage and active processes.

- `htop`: Interactive process viewer (more user-friendly than top).

- `ps aux`: Shows a detailed snapshot of all running processes.

- `kill -9 <PID>`: Forcefully terminates a process using its ID.

- `lsof -i :80`: Shows which process is using port 80 (crucial for web servers).

- `free -m`: Displays used and free RAM in Megabytes.

- `uptime`: Shows how long the system has been running and the load average.

## 📂 File System & Navigation

- `ls -lah`: Lists all files (including hidden) with human-readable sizes.

- `pwd`: Prints the current working directory path.

- `cd ..`: Moves one level up in the directory structure.

- `mkdir -p /path/to/dir`: Creates nested directories in one go.

- `cp -r`: Copies directories and their contents recursively.

- `mv`: Moves or renames files and directories.

- `rm -rf`: Forcefully and recursively removes files/folders (Use with caution!).

- `find / -name "app.log"`: Searches for a specific file starting from the root.

- `du -sh *`: Summarizes disk usage of each folder in the current directory.

- `df -h`: Shows disk space usage across all mounted file systems.

- `grep -i "error" log.txt`: Searches for the string "error" inside a file (case-insensitive).

- `tail -f /var/log/syslog`: Watches a log file in real-time as new entries are added.

- `chmod 644 file.txt`: Sets standard read/write permissions for a file.

## 🌐 Networking Troubleshooting

- `ping <host>`: Checks basic connectivity between your machine and a server.

- `ip addr show`: Displays IP addresses and network interface details.

- `curl -I <url>`: Fetches the HTTP header of a website (great for debugging 404/500 errors).

- `dig <domain>`: Performs a DNS lookup to check domain-to-IP mapping.

- `netstat -tulpn`: Lists all listening ports and the programs using them.

- `ssh user@ip`: Securely connects to a remote server.