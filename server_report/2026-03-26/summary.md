# Security Analysis Summary — 2026-03-26

## Critical Threats

### 1. **fast-xml-parser XSS (CRITICAL)**
- **Component:** fast-xml-parser 4.2.5
- **Issue:** Cross-Site Scripting via improper DOCTYPE entity handling
- **Fix:** Update to 4.5.4 or 5.3.5
  ```bash
  npm install fast-xml-parser@4.5.4
  ```

### 2. **Angular High-Severity Vulnerabilities (HIGH)**
- **Components:** @angular/compiler 14.2.0, @angular/core 14.2.0
- **Fix:** Update to ≥14.2.10
  ```bash
  npm update @angular/compiler @angular/core
  ```

### 3. **axios SSRF (HIGH)**
- **Component:** axios 1.6.2
- **Fix:** Update to ≥1.7.0
  ```bash
  npm install axios@1.7.0
  ```

### 4. **Rootkit Hunter Warnings**
- **Issue:** Suspicious timestamps on /usr/bin/awk, curl, which
- **Investigation:**
  ```bash
  dpkg -S /usr/bin/awk /usr/bin/curl /usr/bin/which
  debsums <package-name>
  # If mismatches, reinstall
  apt install --reinstall <package>
  ```

### 5. **SSH Root Login Enabled**
- **Fix:**
  ```bash
  sed -i 's/^PermitRootLogin yes/PermitRootLogin prohibit-password/' /etc/ssh/sshd_config
  systemctl restart sshd
  ```

### 6. **ClamAV Eicar Test File**
- **Location:** `/home/node/.openclaw/workspace/eicar.com`
- **Status:** Test file only — benign. No action needed.

## System Hardening

| Finding | Fix |
|---------|-----|
| TCP timestamps enabled | `net.ipv4.tcp_timestamps=0` in /etc/sysctl.conf |
| /tmp not mounted noexec | Add `noexec,nodev,nosuid` to /etc/fstab |
| Auditd not running | `apt install auditd && systemctl enable auditd` |
| IPv6 enabled (unused) | `net.ipv6.conf.all.disable_ipv6=1` |

## Priority Actions

1. **Immediate:** Update fast-xml-parser
2. **Today:** Update Angular and axios
3. **Today:** Disable root SSH login
4. **Today:** Investigate suspicious file timestamps
5. **This Week:** Apply system hardening

---
*Analysis by Scorpion 🦂*