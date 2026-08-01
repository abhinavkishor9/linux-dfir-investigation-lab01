# linux-dfir-investigation-lab01
## Overview

Linux incident response is rarely limited to examining a single artifact. Analysts must correlate authentication logs, running processes, persistence mechanisms, network activity, and host-based Indicators of Compromise (IOCs) to determine whether a system has been compromised.

In this hands-on Linux DFIR lab, a structured investigation was performed using native Linux utilities. The investigation covered authentication log analysis, suspicious process inspection, persistence hunting, and IOC collection to validate the integrity of the system and identify potential indicators of malicious activity.

---

# Executive Summary

This investigation demonstrates a complete Linux Digital Forensics and Incident Response (DFIR) workflow using built-in Linux utilities. The system was examined by reviewing authentication activity, validating running processes, inspecting persistence locations, collecting host-based IOCs, and verifying network activity.

The investigation followed the same methodology commonly used by SOC analysts during Linux incident response, where evidence from multiple system artifacts is correlated before determining whether suspicious activity is present.

---

# Investigation Objectives

- Identify basic Linux system information.
- Review user login activity.
- Analyze authentication logs.
- Investigate running processes.
- Inspect parent-child process relationships.
- Hunt for Linux persistence mechanisms.
- Collect host-based Indicators of Compromise (IOCs).
- Review active network services.
- Validate overall system integrity.
- Document investigation findings.

---

# Skills Demonstrated

- Linux DFIR Methodology
- Linux Log Analysis
- IOC Collection
- Authentication Log Investigation
- Process Investigation
- Persistence Hunting
- Linux System Enumeration
- Network Service Analysis
- Evidence Correlation
- Incident Documentation

---

# Tools Used

- Ubuntu 24.04 LTS
- Bash
- hostnamectl
- who
- w
- last
- grep
- ps
- pstree
- top
- crontab
- systemctl
- ss
- find
- lsof
- /proc Filesystem

---

# Lab Environment

| Component | Details |
|-----------|---------|
| Operating System | Ubuntu 24.04 LTS |
| Platform | WSL2 |
| Investigation Type | Linux Host-Based DFIR |
| Analysis Method | Native Linux Utilities |
| Primary Artifacts | Logs, Processes, Persistence, IOCs |
| Shell | Bash |
| Privileges | Standard User + sudo |

---

# Investigation Workflow

1. Identify the Linux system.
2. Review logged-in users and login history.
3. Analyze authentication logs.
4. Enumerate running processes.
5. Validate process relationships.
6. Inspect process metadata.
7. Hunt for persistence mechanisms.
8. Review scheduled tasks and services.
9. Collect host-based IOCs.
10. Review active network listeners.
11. Correlate collected evidence.
12. Document investigation findings.

---

# MITRE ATT&CK Mapping

| Technique | Description |
|-----------|-------------|
| T1082 | System Information Discovery |
| T1033 | System Owner/User Discovery |
| T1057 | Process Discovery |
| T1018 | Remote System Discovery |
| T1543 | Create or Modify System Process |
| T1053.003 | Scheduled Task / Cron |
| T1021.004 | SSH |
| T1049 | System Network Connections Discovery |
| T1083 | File and Directory Discovery |

---

# Evidence Collected

- Hostname and operating system details
- Logged-in user sessions
- Login history
- Authentication log entries
- Running process list
- Process hierarchy
- Process metadata
- Cron configuration
- Enabled systemd services
- SSH configuration
- Startup configuration files
- Listening network ports
- Recently modified files
- Shell command history

---

# Evidence Correlation

The investigation correlated multiple Linux artifacts to validate system activity:

- User sessions matched the observed login history.
- Authentication logs showed expected administrative activity.
- Running processes aligned with normal Ubuntu services.
- Persistence locations contained only legitimate configurations.
- Enabled systemd services matched standard operating system components.
- Network listeners exposed only expected services such as SSH and DNS.
- Recently modified files and shell history were consistent with the investigation activities.

---

# Investigation Findings

The investigation did not reveal evidence of malicious processes, unauthorized persistence mechanisms, or suspicious network services. Authentication records, running processes, cron configurations, startup files, enabled services, and collected IOCs were all consistent with normal Ubuntu system operation.

The lab demonstrates how multiple Linux artifacts can be correlated to determine the overall security posture of a host rather than relying on a single source of evidence.

---

# Key Takeaway

Effective Linux DFIR relies on correlating evidence from logs, running processes, persistence locations, network activity, and system artifacts instead of investigating them in isolation. By following a structured investigation workflow and validating observations across multiple data sources, analysts can accurately distinguish legitimate system activity from potential indicators of compromise.
