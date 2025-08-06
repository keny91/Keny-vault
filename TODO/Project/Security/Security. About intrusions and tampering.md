#security #tampering #intrusion

If your machine has been attacked, detecting the intrusion **and figuring out what was tampered with or exfiltrated** can be very hard — especially if it wasn't prepared **before the breach**.

But let's walk through what you can do **now**, **what might still be recoverable**, and how to **prepare better in the future**.

---

## 🚨 1. Signs of Intrusion (What to Look For Now)

Look for anomalies in these areas:

### 🧾 Logs

- **Check system logs**:
    
    - `/var/log/auth.log` (or `/var/log/secure` on RHEL): Look for failed/successful logins, new user creation
        
    - `/var/log/syslog`, `/var/log/messages`
        
- Look for:
    
    - Unknown users
        
    - SSH logins from odd IPs or at weird times
        
    - `sudo` attempts
        
    - Services restarting unexpectedly

```
grep "Accepted" /var/log/auth.log
grep "sudo" /var/log/auth.log
```

### 🧑‍💻 Running Processes

- Check for **weird or unknown processes** running:

```
ps aux --sort=-%cpu
```

- Look for suspicious names like `kworker`, `crond`, `update.sh`, or base64-encoded junk.
    

---

### 📁 File Integrity

- Check for recently modified files:

```
find /etc -type f -mtime -2
find /home -type f -mtime -2
```

- - `~/.bashrc`, `~/.ssh/authorized_keys`
        
    - `/etc/passwd`, `/etc/shadow`, `/etc/sudoers`
        
    - New scripts in `/etc/init.d`, `/usr/local/bin`, `/tmp`, `/var/tmp`
        

---

### 🔑 User Accounts

- Look for new or modified users:

```
cut -d: -f1 /etc/passwd
```

Or check for new `sudo` users:

```
grep '^sudo' /etc/group
```

### 📤 Suspicious Network Activity

- Connections to strange IPs:

```
ss -tunap
lsof -i
```

Use `iftop`, `nethogs`, or `tcpdump` if you suspect data exfiltration is ongoing.

## 🧪 2. Tools to Analyze the Breach

If you're still in control of the system:

### 🧰 Intrusion Detection Tools

- **chkrootkit / rkhunter**: Look for known rootkits.
    
- **Lynis**: Good overall system audit tool.
    
- **auditd**: Logs file access and system calls (if already enabled).
    
- **Tripwire / AIDE**: Check file integrity (needs baseline to be effective).
    

---

### 📦 Forensics Suite (Live or Post-Mortem)

- **Volatility**: Analyze memory dumps.
    
- **Autopsy/Sleuth Kit**: Examine file timelines and disk artifacts.
    
- **Tshark/tcpdump**: If you suspect live exfiltration.
    

---

## 🔎 3. Is It Possible to Know What Was Copied?

⚠️ **Usually not exactly** — unless:

- You had **auditd** or **inotify** running and logging file accesses.
    
- You had **full packet capture** or **proxy logs**.
    
- Or **file access logs** (e.g., via cloud storage / SFTP with auditing).


### 📁 What You _Can_ Check:

- Recently accessed files:
```
find /home -type f -atime -2
```

- Bash history (`~/.bash_history`, if not wiped)
    
- Commands executed:
```
lastcomm
history
journalctl _COMM=sudo
```

- Copy-like activity:
    
    - `scp`, `rsync`, `curl`, `wget`, `base64`, `nc`, `ncat`, `ftp`, etc.
        

Check `.bashrc`, `.bash_profile`, crontabs for persistent backdoors.


## 🧯 4. What to Do _Right Now_ if You Suspect a Breach

### 🔐 Short-Term

1. **Disconnect** from the network immediately if still ongoing.
    
2. **Do not reboot**, or you may lose RAM or tmp evidence.
    
3. **Take a forensic image** (e.g., `dd`, `dcfldd`, or `FTK Imager`).
    
4. Dump memory if possible (`LiME`, `avml`, `volatility` usage).
    

---

### 🧼 Long-Term (Post-Incident)

- **Wipe and reinstall**. If you're not 100% sure how deep they went, don’t trust the system anymore.
    
- **Reset all credentials**, tokens, SSH keys, cloud access, etc.
    
- **Check other devices** in the network — lateral movement is common.
    

---

## 🛡️ 5. How to Prepare for Next Time (Proactive Defenses)

|Tool / Technique|Purpose|
|---|---|
|**auditd**|Logs file access and execution|
|**Tripwire / AIDE**|File integrity verification|
|**Wazuh / OSSEC**|Real-time file monitoring + alerts|
|**Fail2Ban**|Block IPs with failed login attempts|
|**iptables/nftables**|Restrict access to only known hosts|
|**Tailscale / WireGuard**|VPN into your devices securely|
|**SSH Hardening**|Disable passwords, allow-list keys, use port knocking|
|**SIEM Tools**|Aggregate logs and detect patterns (e.g., Graylog, Splunk, ELK)|
|**Prometheus + Grafana + Loki**|Alert on anomalies in logs and system behavior|

#### 🔐 **You should load a forensic toolkit from a USB (or external medium) because you can’t trust the compromised system to tell the truth anymore.**

