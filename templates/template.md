# Box: Name
Difficulty: Easy
OS: Linux

## 🛠️ Attacker Environment
- **Host OS**: Parrot Security OS (VM)
- **Tools Used**:
  - `nmap` — Network scanning and service detection
  - `telnet` — Manual service interaction (port 23)

---
## 🧠 Recon
Nmap Scan:
```bash
nmap -sC -sV -oN nmap_initial.txt 10.10.10.X
```

## 🔍 Enumeration
Found a vulnerable service running on port XYZ...

## 💥 Exploitation
Used payload X to gain initial foothold.

## 🔐 Privilege Escalation
Escalated to root via...

## 🧼 Cleanup & Lessons
- Removed any uploaded shells
- Key takeaway: Always check for XYZ
