# Investigation Timeline

| Step | Activity | Evidence |
|------|----------|----------|
| 1 | Collected system information | `hostnamectl` |
| 2 | Verified active user session | `who` |
| 3 | Reviewed current login activity and uptime | `w` |
| 4 | Examined recent login history | `sudo last \| head -10` |
| 5 | Reviewed authentication logs | `sudo grep "Failed password" /var/log/auth.log \| tail` |
| 6 | Enumerated active network services | `ss -tulpn` |
| 7 | Identified high CPU processes | `ps aux --sort=-%cpu \| head -15` |
| 8 | Collected recently modified system files | `sudo find /etc -type f -mtime -7` |
| 9 | Collected recently modified user files | `sudo find /home -type f -mtime -7` |
| 10 | Reviewed shell command history | `tail ~/.bash_history` |
| 11 | Correlated collected host artifacts | Authentication logs, processes, files, services |
| 12 | Completed Linux IOC investigation | Investigation findings documented |

---

# Investigation Flow

Investigation Started

↓

Collected Host Information

↓

Verified Logged-in Users

↓

Reviewed Login History

↓

Examined Authentication Logs

↓

Enumerated Running Processes

↓

Reviewed Active Network Services

↓

Collected Recently Modified System Files

↓

Collected Recently Modified User Files

↓

Reviewed Shell Command History

↓

Correlated All Collected Artifacts

↓

Validated System Integrity

↓

Investigation Completed

---

# Summary

This investigation followed a structured Linux IOC collection workflow using native Linux utilities. Multiple host artifacts—including system information, user sessions, authentication logs, running processes, network listeners, recently modified files, and shell history—were collected and correlated to assess the security posture of the system. The collected evidence indicated normal Ubuntu system activity, with no suspicious processes, unauthorized persistence mechanisms, or unexpected network services identified. This lab demonstrated how SOC analysts and DFIR investigators can build confidence in their findings by correlating evidence from multiple sources rather than relying on a single indicator.
