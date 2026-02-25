# Day 14 – Networking Fundamentals & Hands-on Checks

## 🎯 Objective

Today I revised core networking fundamentals and practiced essential troubleshooting commands used in real DevOps environments.

I focused on:
- Understanding OSI vs TCP/IP models
- Running connectivity and port checks
- Performing a mini network health check on trainwithshubham.com

---

# 🌐 Networking Concepts (In My Words)

## OSI vs TCP/IP Model

### OSI Model (7 Layers)
1. Physical  
2. Data Link  
3. Network  
4. Transport  
5. Session  
6. Presentation  
7. Application  

### TCP/IP Model (4 Layers)
1. Link  
2. Internet  
3. Transport  
4. Application  

### Mapping Example

- IP → Internet Layer  
- TCP/UDP → Transport Layer  
- HTTP/HTTPS → Application Layer  
- DNS → Application Layer  

Example:

`curl https://trainwithshubham.com`  
= Application (HTTP) → Transport (TCP) → Internet (IP) → Link

---

# 🔍 Hands-on Networking Checks

## 1️⃣ Identity Check

```bash
hostname -I
```

### Observation:
- Confirmed my system IP address.
- Verified that the machine is correctly connected to the network.

---

## 2️⃣ Reachability Test

```bash
ping trainwithshubham.com
```

### Observation:
- Received successful replies.
- Latency observed (varies depending on location).
- 0% packet loss (network working properly).

---

## 3️⃣ Path Check

```bash
traceroute trainwithshubham.com
```

### Observation:
- Multiple hops across ISP routers.
- Identified network path to destination.
- No major timeouts observed.

---

## 4️⃣ Listening Ports

```bash
ss -tulpn
```

### Observation:
- Found SSH running on port 22.
- Service bound to 0.0.0.0:22 (listening on all interfaces).

---

## 5️⃣ DNS Resolution

```bash
dig trainwithshubham.com
```

### Observation:
- Domain resolved successfully to public IP address.
- DNS service functioning correctly.

---

## 6️⃣ HTTP Check

```bash
curl -I https://trainwithshubham.com
```

### Observation:
- HTTP status received (e.g., 200 OK).
- Response headers confirmed server accessibility.
- Application layer functioning correctly.

---

## 7️⃣ Connections Snapshot

```bash
netstat -an | head
```

### Observation:
- Observed LISTEN and ESTABLISHED states.
- LISTEN = waiting for connections.
- ESTABLISHED = active communication.

---

# 🧪 Mini Task: Port Probe & Interpretation

Identified SSH running on port 22.

Tested locally:

```bash
nc -zv localhost 22
```

### Result:
- Connection successful.
- Port is reachable.

If unreachable, next checks would be:
- `systemctl status ssh`
- `ufw status` or `iptables -L`
- Check firewall or cloud security group rules.

---

# 🧠 Key Learnings

1. Networking troubleshooting follows a layered approach.
2. `ping` gives the fastest connectivity signal.
3. `ss -tulpn` quickly shows listening services and ports.
4. DNS failures relate to Application layer issues.
5. HTTP errors (like 500) usually indicate backend/server problems.

---

# 🚀 Why This Matters in DevOps

These commands are essential during:

- Website downtime
- DNS resolution issues
- Port accessibility problems
- Firewall misconfiguration
- Cloud server connectivity troubleshooting

Quick diagnostics reduce downtime and improve incident response.

---

# 🔎 Reflection

### Which command gives the fastest signal?

`ping` – immediate confirmation of reachability.

---

### If DNS fails, which layer to inspect?

Application Layer  
Check:
- DNS server
- `/etc/resolv.conf`
- Network connectivity

---

### If HTTP 500 appears?

Application Layer first  
Then check:
- Web server logs
- Backend service status
- Database connectivity

---

### Two follow-up checks during a real incident:

1. `journalctl -xe`
2. `systemctl status <service>`

---

# 💻 Commands Used

```bash
hostname -I
ping trainwithshubham.com
traceroute trainwithshubham.com
ss -tulpn
dig trainwithshubham.com
curl -I https://trainwithshubham.com
netstat -an | head
nc -zv localhost 22
```

---

# ✅ Final Verification

- Network reachable
- DNS resolving
- HTTP responding
- SSH listening and reachable
- No packet loss observed

Networking fundamentals reinforced successfully.