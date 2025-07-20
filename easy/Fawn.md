# Box: Fawn
ID: 2
Difficulty: Easy

## 🛠️ Attacker Environment
- **Host OS**: Parrot Security OS (VM)

## 🛠️ Tools Used
  - `ping`
  - `nmap`
  - `ftp`

## 🎯 Target Environment
- **IP Address**: 10.129.93.123
- **OS**: Unix

## 🧠 Recon
### 1. Basic Network Check  
```bash
ping 10.129.93.123
```
### 2. Nmap Scan
```bash
nmap -sV 10.129.93.123
```
## 🔍 Enumeration
Found an open port **21/tcp**, running **FTP** - allowed anonymous login.

### 2. FTP Client Installation
```bash
sudo apt install ftp -y
```

### 2. FTP Login
```bash
ftp 10.129.93.123
```
**Credentials:**
- **Username:** anonymous  
- **Password:** anon123

**Notes:**  
- Able to list and download files from the server using anonymous credentials.

## 💥 Exploitation
- Used FTP anonymous access to retrieve flag.txt

## 🔐 Privilege Escalation
N/A 

## 🧼 Cleanup & Lessons
- No Cleanup Required
- **Key takeaway**: Always test for anonymous FTP login; low-hanging misconfigs can lead directly to flags.
