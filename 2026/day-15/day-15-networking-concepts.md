# Day 15 – Networking Concepts: DNS, IP, Subnets & Ports

## 🎯 Objective

Today I strengthened my understanding of core networking building blocks required for DevOps:

- DNS resolution
- IP addressing (public vs private)
- CIDR & subnetting basics
- Ports and service mapping

This day focused on conceptual clarity and real-world relevance.

---

# 🌐 Task 1 – DNS: How Names Become IPs

## What Happens When I Type `google.com` in a Browser?

1. The browser checks local DNS cache.
2. If not found, it queries a DNS resolver.
3. The resolver contacts root → TLD → authoritative DNS server.
4. The DNS server returns the IP address (A record).
5. The browser connects to that IP over TCP (usually port 443 for HTTPS).

---

## Common DNS Record Types

- **A** – Maps domain name to IPv4 address.
- **AAAA** – Maps domain name to IPv6 address.
- **CNAME** – Alias of one domain to another.
- **MX** – Mail server for a domain.
- **NS** – Name server responsible for the domain.

---

## Command Run

```bash
dig google.com
```

### Observed:
- Found **A record** showing IPv4 address.
- TTL value displayed (time DNS record is cached).

Example:
```
google.com.    300    IN    A    142.250.x.x
```

TTL: 300 seconds

---

# 🌍 Task 2 – IP Addressing

## What is IPv4?

An IPv4 address is a 32-bit number written in dotted decimal format.

Example:
```
192.168.1.10
```

It consists of:
- Network portion
- Host portion

---

## Public vs Private IP

- **Public IP** → Routable on the internet  
  Example: `8.8.8.8`

- **Private IP** → Used inside internal networks  
  Example: `192.168.1.5`

---

## Private IP Ranges

- `10.0.0.0 – 10.255.255.255`
- `172.16.0.0 – 172.31.255.255`
- `192.168.0.0 – 192.168.255.255`

---

## Command Run

```bash
ip addr show
```

### Observation:
- Identified my system IP.
- Confirmed it belongs to a private IP range.

---

# 📊 Task 3 – CIDR & Subnetting

## What Does `/24` Mean?

`192.168.1.0/24` means:
- 24 bits are used for network.
- 8 bits are available for hosts.
- Subnet mask: 255.255.255.0

---

## Usable Hosts Calculation

Formula:
```
2^n - 2
```
(n = number of host bits)

---

## Why Do We Subnet?

- Improve security
- Reduce broadcast domains
- Better IP management
- Network segmentation

---

## CIDR Table

| CIDR | Subnet Mask       | Total IPs | Usable Hosts |
|------|-------------------|-----------|--------------|
| /24  | 255.255.255.0     | 256       | 254          |
| /16  | 255.255.0.0       | 65,536    | 65,534       |
| /28  | 255.255.255.240   | 16        | 14           |

---

# 🚪 Task 4 – Ports: The Doors to Services

## What is a Port?

A port is a logical communication endpoint that allows multiple services to run on the same IP address.

IP = Building  
Port = Door to a specific service

---

## Common Ports

| Port  | Service        |
|-------|---------------|
| 22    | SSH           |
| 80    | HTTP          |
| 443   | HTTPS         |
| 53    | DNS           |
| 3306  | MySQL         |
| 6379  | Redis         |
| 27017 | MongoDB       |

---

## Command Run

```bash
ss -tulpn
```

### Observed:
- SSH running on port 22
- System services listening on specific ports
- Confirmed active LISTEN state

---

# 🔗 Task 5 – Putting It Together

## Scenario 1:
`curl http://myapp.com:8080`

Concepts involved:
- DNS resolves `myapp.com` to IP
- TCP connection to port 8080
- HTTP request sent at Application layer
- IP routing handles packet delivery

---

## Scenario 2:
App can't reach database at `10.0.1.50:3306`

First checks:
- Is port 3306 open?
- Is MySQL service running?
- Is firewall blocking traffic?
- Is subnet routing configured correctly?

---

# 🧠 Key Learnings

1. DNS converts human-readable names into IP addresses.
2. CIDR determines network size and host capacity.
3. Ports allow multiple services to share one IP.
4. Private IPs are used internally; public IPs are internet-routable.
5. Networking troubleshooting follows layered logic.

---

# 🚀 Why This Matters in DevOps

Understanding DNS, IP, subnets, and ports helps with:

- Cloud networking (VPC, subnets)
- Kubernetes service communication
- Load balancer configuration
- Database connectivity troubleshooting
- Security group & firewall debugging

Strong networking fundamentals = faster incident resolution.

---

# 💻 Commands Used

```bash
dig google.com
ip addr show
ss -tulpn
```

---

# ✅ Final Summary

Today I connected DNS, IP addressing, subnetting, and ports into one complete networking picture.

This builds the foundation for:
- Cloud networking
- Kubernetes networking
- Service-to-service communication
- Production troubleshooting