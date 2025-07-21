# Box
Name: Explosion
ID: 5
Difficulty: Very Easy 

## 🧠 Attacker Environment
- **Host OS**: Parrot Security OS (VM)

## 🛠️ Tools Used
  - `ping`
  - `nmap`
  - `xfreerdp`

## 🎯 Target Environment
- **Ip Address**: 10.129.85.244
- **OS**: Windows

## 🧠 Recon
Nmap Scan:
```bash
nmap -sV 10.129.85.244
```
## 🔍 Enumeration
Found an open port **135/tcp**, running **msrpc** service
Found an open port **139/tcp**, running **netbios-ssn** service.
Found an open port **445/tcp**, running **microsoft-ds** service.
Found an open port **3389/tcp**, running **ms-wbt-server** service.

## 💥 Exploitation
1. Installed xfreerdp to connect to RDP service
````bash
sudo-apt-get install freerdp2-x11
````
2. Logged into RDP as administrator
````bash
xfreerdp /v:10.129.85.244 
xfreerdp /v:10.129.85.244 /u:administrator /cert:ignore
````
## 🔐 Privilege Escalation
Not required

## 🧼 Cleanup & Lessons
- xfreerdp session closed cleanly
- **Key takeaways**: 
- Always read the help files to see what you can utilize to gain access
- Always try default credentials: root, user, and administrator as credentials 
