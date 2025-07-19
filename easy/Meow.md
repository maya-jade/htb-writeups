# Box: Meow
Difficulty: Easy
OS: Linux

## 🛠️ Attacker Environment
- **Host OS**: Parrot Security OS (VM)
- **Tools Used**:
  - `nmap` — Network scanning and service detection
  - `telnet` — Manual service interaction (port 23)

---

## 🧠 Recon
**Nmap Scan:**
```bash
nmap -sV 10.129.222.196

## 🔍 Enumeration
Found an open port 23/tcp, running the telnet service

## 💥 Exploitation
Tried logging in with common usernames and no password:
admin — ❌
administrator — ❌
root — ✅ Success

Commands executed:
telnet 10.129.222.196
login: root
Password: [blank]
Gained shell access as root.

## 🔐 Privilege Escalation
Not required - root access via telnet

## 🧼 Cleanup & Lessons
N/A

