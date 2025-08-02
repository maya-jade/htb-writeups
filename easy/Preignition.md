# Box
Name: Preignition
ID: 7
Difficulty: (Easy)

## 🧠 Attacker Environment
- **Host OS**: Parrot Security OS (VM)

## 🛠️ Tools Used
  - `ping`
  - `nmap`

## 🎯 Target Environment
- **Ip Address**: 10.129.77.128
- **Web Server**: `nginx 1.14.2` (Port 80)  

## 🧠 Recon
Nmap Scan:
```bash
sudo nmap -sV 10.129.77.128
```
Found an open port **80**, running **nginx 1.14.2** service.
Nginx server default homepage was served, suggesting the web server might not be configured yet.

## 🔍 Enumeration
Steps:
1. Installed `gobuster` on attacker box and used it for directory brute-forcing.
2. Explored Help Options:
- `dir`: Directory busting mode  
- `-w`: Specify wordlist  
- `-u`: Target URL/IP  

3. Downloaded wordlist named common.txt from here:
https://github.com/danielmiessler/SecLists/raw/master/Discovery/Web-Content/common.txt 

4.Gobuster Command Used  
```bash
sudo gobuster dir -w /home/user/Shared/common.txt -u http://10.129.77.128
```
5. Found /admin.php

## 💥 Exploitation
1. Accessed `/admin.php`  
2. Tried default credentials:
```text
Username: admin  
Password: admin  
```
 **Login Successful**
3. Flag Obtained

## 🔐 Privilege Escalation
- Not needed

## 🧼 Cleanup & Lessons
- Not needed
- **Key takeaways**: 
- Always try the default credentials!
- GoBuster = directory busting tool
