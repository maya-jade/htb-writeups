# Box: 
Name: Meow
ID: 1
Difficulty: Very Easy

## 🛠️ Attacker Environment
- **Host OS**: Parrot Security OS (VM)

## 🛠️ Tools Used
  - `nmap` — Network scanning and service detection
  - `telnet` — Manual service interaction (port 23)

## 🎯 Target Environment
- **IP Address**: 10.129.222.196 
- **OS**: Linux

## 🧠 Recon
**Nmap Scan (Find Open Ports):**
```bash
nmap -sV 10.129.222.196
```
## 🔍 Enumeration
Found an open port **23/tcp**, running the **Telnet** service.

## 💥 Exploitation
Tried logging in with common usernames and no password:
- `admin` — ❌
- `administrator` — ❌
- `root` — ✅ **Success**

Commands executed:
```bash
telnet 10.129.222.196
login: root
Password: [blank]
```

## 🔐 Privilege Escalation
Not required - already had root access via telnet.

## 🧼 Cleanup & Lessons
- Telnet connection closed cleanly.
- **Key takeaways**:
- Always check for default credentials and blank passwords on public-facing services.
- Telnet is insecure and should never be exposed on the internet.
- Low-difficulty boxes often reinforce the importance of basic enumeration and common misconfigurations.
