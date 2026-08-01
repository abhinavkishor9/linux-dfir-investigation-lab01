# Investigation Notes

## Lab Summary

This investigation focused on performing a structured Linux DFIR investigation by correlating multiple host artifacts instead of relying on a single source of evidence.

The investigation reconstructed the overall system state by collecting system information, reviewing user activity, examining authentication logs, investigating running processes, hunting for persistence mechanisms, collecting Indicators of Compromise (IOCs), and validating active network services.

---

## Analyst Methodology

1. Collect system information.
2. Review logged-in users and login history.
3. Examine authentication logs.
4. Enumerate running processes.
5. Analyze process hierarchy.
6. Inspect process metadata.
7. Hunt for persistence mechanisms.
8. Review scheduled tasks and enabled services.
9. Collect host-based IOCs.
10. Review active network listeners.
11. Correlate collected evidence.
12. Document investigation findings.

---

## Investigation Scenario

The objective of this investigation was to determine whether the Linux host showed any signs of compromise by examining multiple forensic artifacts commonly reviewed during incident response.

The investigation aimed to determine:

- Whether the system identity matched expectations.
- Whether user login activity appeared legitimate.
- Whether authentication logs contained suspicious events.
- Whether any suspicious processes were running.
- Whether persistence mechanisms had been modified.
- Whether network services appeared normal.
- Whether recently modified files indicated suspicious activity.
- Whether collected artifacts suggested compromise.

---

## Evidence Collected

### Evidence 1 – System Information

Commands Used

```bash
hostnamectl
```

Collected:

- Hostname
- Operating system
- Kernel version
- Architecture
- Virtualization platform

Finding:

Verified that the investigation was performed on an Ubuntu 24.04 LTS system running under WSL2.

---

### Evidence 2 – User Login Activity

Commands Used

```bash
who
w
last
```

Collected:

- Active user sessions
- Login times
- Recent reboot history

Finding:

Only the expected user session was active, and the login history was consistent with normal system usage.

---

### Evidence 3 – Authentication Logs

Command Used

```bash
sudo grep "Failed password" /var/log/auth.log | tail
```

Collected:

- Recent authentication-related log entries

Finding:

The retrieved entries corresponded to the analyst's own sudo commands during the investigation rather than failed SSH login attempts.

---

### Evidence 4 – Running Processes

Command Used

```bash
ps aux --sort=-%cpu | head -15
```

Collected:

- Active processes
- CPU utilization
- Memory utilization

Finding:

Only expected operating system processes such as systemd, rsyslogd, unattended-upgrades, and bash sessions were observed.

---

### Evidence 5 – Persistence Mechanisms

Commands Used

```bash
crontab -l
sudo crontab -u root -l
cat /etc/crontab
systemctl list-unit-files --state=enabled
cat ~/.bashrc
cat ~/.ssh/authorized_keys
cat /etc/rc.local
```

Collected:

- User cron jobs
- Root cron jobs
- System cron configuration
- Enabled systemd services
- Shell startup configuration
- SSH authorized keys
- rc.local configuration

Finding:

No unauthorized persistence mechanisms were identified. Cron jobs, enabled services, and startup files matched expected Ubuntu defaults.

---

### Evidence 6 – Host-Based IOC Collection

Commands Used

```bash
find /etc -type f -mtime -7
sudo find /etc -type f -mtime -7
sudo find /home -type f -mtime -7
tail ~/.bash_history
```

Collected:

- Recently modified system files
- Recently modified user files
- Shell history

Finding:

Recently modified files corresponded to normal operating system activity and the analyst's investigation. No suspicious artifacts were identified.

---

### Evidence 7 – Network Services

Command Used

```bash
ss -tulpn
```

Collected:

- Listening TCP services
- Listening UDP services

Finding:

Only expected services such as SSH and DNS were listening. No unexpected ports or unauthorized services were detected.

---

## DFIR Analysis

The investigation followed a standard Linux DFIR methodology by correlating multiple independent artifacts rather than relying on a single indicator. System identity, user activity, authentication logs, running processes, persistence mechanisms, IOC collection, and network services all produced consistent findings.

Cross-validation of these artifacts indicated normal operating system behavior with no evidence of unauthorized persistence, suspicious processes, or unexpected network activity.

---

## MITRE ATT&CK Mapping

| Tactic | Technique | ID |
|---------|-----------|----|
| Discovery | System Information Discovery | T1082 |
| Discovery | System Owner/User Discovery | T1033 |
| Discovery | Process Discovery | T1057 |
| Persistence | Scheduled Task/Cron | T1053.003 |
| Discovery | System Network Connections Discovery | T1049 |
| Discovery | File and Directory Discovery | T1083 |

---

## Analyst Observations

- Host identification should be verified before beginning an investigation.
- User session information provides valuable context during incident response.
- Authentication logs help distinguish administrative activity from potential brute-force attempts.
- Process enumeration helps identify unexpected or malicious programs.
- Persistence locations should always be reviewed during Linux investigations.
- IOC collection becomes more valuable when multiple artifacts are correlated.
- Expected network listeners simplify identification of abnormal services.

---

## Conclusion

This investigation demonstrated a complete Linux host-based DFIR workflow using native Linux utilities. By systematically collecting and correlating evidence from authentication logs, running processes, persistence locations, IOC artifacts, and network services, the investigation confirmed normal system behavior while reinforcing the importance of structured evidence collection and forensic documentation.
