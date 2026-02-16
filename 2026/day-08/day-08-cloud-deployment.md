# Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment

## 📌 Objective

Today’s goal was to deploy a real web server on the cloud and understand practical server management like a DevOps engineer.

In this hands-on lab, I:
- Launched a cloud EC2 instance
- Connected using SSH
- Installed Docker and Nginx
- Configured security group for HTTP access
- Extracted and downloaded Nginx logs
- Verified web access from browser

This was real-world infrastructure practice.

---

# 🌩 Part 1 – Launch Cloud Instance & SSH Access

## Step 1: Launch EC2 Instance

- Selected Ubuntu Server (AWS Free Tier)
- Instance type: t2.micro
- Created key pair (JOSH.pem)
- Allowed inbound ports:
  - 22 (SSH)
  - 80 (HTTP)

---

## Step 2: Connect via SSH

```bash
ssh -i JOSH.pem ubuntu@<your-instance-ip>
```

✅ Successfully connected to remote server.

Verified connection:
```bash
whoami
hostname
```

---

# 🐳 Part 2 – Install Docker & Nginx

## Step 1: Update System

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Step 2: Install Docker

```bash
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
sudo systemctl status docker
```

Verified Docker:
```bash
docker --version
```

---

## Step 3: Install Nginx

```bash
sudo apt install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
sudo systemctl status nginx
```

Verified Nginx:
```bash
curl localhost
```

---

# 🔐 Part 3 – Security Group Configuration

Modified Security Group:

- Allowed HTTP (Port 80) from 0.0.0.0/0
- SSH (Port 22) allowed from my IP

Tested in browser:

```
http://<your-instance-ip>
```

✅ Nginx Welcome Page Displayed Successfully

---

# 📄 Part 4 – Extract Nginx Logs

## Step 1: View Nginx Logs

```bash
sudo tail -n 50 /var/log/nginx/access.log
sudo tail -n 50 /var/log/nginx/error.log
```

---

## Step 2: Save Logs to File

```bash
sudo cp /var/log/nginx/access.log ~/nginx-logs.txt
```

Verified file:
```bash
ls -l ~/nginx-logs.txt
cat ~/nginx-logs.txt
```

---

## Step 3: Download Log File to Local Machine

From local terminal:

```bash
scp -i JOSH.pem ubuntu@<your-instance-ip>:~/nginx-logs.txt .
```

✅ Log file successfully downloaded.

---

# 🧰 Commands Used

- ssh
- apt update / upgrade
- apt install docker.io
- apt install nginx
- systemctl start/enable/status
- curl
- tail
- cp
- scp

---

# ⚠️ Challenges Faced

### 1️⃣ Nginx not accessible in browser
Issue: Security group did not allow port 80  
Solution: Added inbound rule for HTTP (80)

### 2️⃣ Permission denied while copying logs
Issue: Accessing logs without sudo  
Solution: Used sudo to copy logs to home directory

### 3️⃣ SCP File Not Found
Issue: File was not present in home directory  
Solution: Verified file location using `ls -l ~`

---

# 🎯 What I Learned

- How to launch and configure a cloud server
- How SSH works with key-based authentication
- How to install and manage services using systemctl
- Importance of security groups and firewall rules
- Location of Nginx logs (`/var/log/nginx`)
- How to securely transfer files using scp

---

# 🚀 Why This Matters in DevOps

This exercise simulates real production tasks:

- Provisioning infrastructure
- Deploying web servers
- Managing services
- Configuring security rules
- Troubleshooting access issues
- Handling logs for debugging

These are daily DevOps responsibilities in real companies.

---

# 🔥 Key Takeaway

> Infrastructure + Security + Logs = Core DevOps Foundation

---

#90DaysOfDevOps  
#DevOpsKaJosh  
#TrainWithShubham
