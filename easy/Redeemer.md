# Box 
Name: Redeemer
ID:4
Difficulty: Easy

## 🧠 Attacker Environment
- **Host OS**: Parrot Security OS (VM)

## 🛠️ Tools Used
  - `ping`
  - `nmap`
  - `redis-cli`
  
## 🧠 Recon
Nmap Scan:
```bash
nmap -p- -sV 10.129.121.168 
nmap -p- -T4 10.129.121.168 (this one worked because I made the timing more aggressive)
```
## 🔍 Enumeration
Found an open port **6379/tcp**, running **redis** service.

## 💥 Exploitation
1. Installed redis-cli
2 Connected using `redis-cli` (no authentication needed):
  ```bash
  redis-cli -h 10.129.121.168
```
3. Ran basic commands:
info – server details
keys * – list all keys
get flag 

## 🔐 Privilege Escalation
Not required -redis ran as root

## 🧼 Cleanup & Lessons
- Not required
- **Key takeaways**: 
- Always check if a service runs as root, no authentication required
- Misconfigs are an easy win
