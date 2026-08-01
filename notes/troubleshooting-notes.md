# Troubleshooting Notes

## Issue 1

Unable to read authentication logs.

### Cause

The `/var/log/auth.log` file requires elevated privileges.

### Resolution

Use:

```bash
sudo grep "Failed password" /var/log/auth.log | tail
```

---

## Issue 2

Permission denied while searching system files.

### Cause

Certain system directories such as `/etc/ssl/private`, `/etc/credstore`, and `/etc/polkit-1` are restricted to the root user.

### Resolution

Run the search with elevated privileges:

```bash
sudo find /etc -type f -mtime -7
```

---

## Issue 3

Unable to view the root user's scheduled tasks.

### Cause

Root crontab cannot be viewed as a standard user.

### Resolution

Use:

```bash
sudo crontab -u root -l
```

If the output displays:

```text
no crontab for root
```

then no user-specific cron jobs are configured for the root account.

---

## Issue 4

Unable to inspect SSH authorized keys.

### Cause

The `authorized_keys` file may not exist if SSH key-based authentication has never been configured.

### Resolution

Verify using:

```bash
cat ~/.ssh/authorized_keys
```

If the output is:

```text
No such file or directory
```

this indicates that no authorized SSH keys are configured for the user.

---

## Issue 5

Unable to locate `/etc/rc.local`.

### Cause

Modern Ubuntu systems often do not use the legacy `rc.local` startup mechanism.

### Resolution

Verify its existence:

```bash
cat /etc/rc.local
```

If the output is:

```text
No such file or directory
```

continue investigating persistence through cron jobs and enabled systemd services instead.

---

## Issue 6

Authentication log shows no failed password attempts.

### Cause

The system may not have experienced failed login attempts, or the retrieved entries may simply record the analyst's own `sudo` commands.

### Resolution

Review the latest authentication events:

```bash
sudo grep "Failed password" /var/log/auth.log | tail
```

Interpret the results carefully before concluding that a brute-force attack occurred.

---

## Issue 7

Unable to determine whether recently modified files are suspicious.

### Cause

Operating system updates and routine administrative activity can legitimately modify many system files.

### Resolution

Collect recently modified files first:

```bash
sudo find /etc -type f -mtime -7
sudo find /home -type f -mtime -7
```

Then correlate the results with system updates, user activity, and shell history before classifying them as suspicious.

---

## Issue 8

Unexpected network services appear during enumeration.

### Cause

Legitimate operating system services such as SSH, DNS, or system daemons may be listening on network ports.

### Resolution

Review active listeners using:

```bash
ss -tulpn
```

Validate each listening service against the expected system configuration before treating it as malicious.

---

## Issue 9

High CPU utilization observed during process investigation.

### Cause

Background services, software updates, or legitimate user processes may temporarily consume additional CPU resources.

### Resolution

Review the highest resource-consuming processes using:

```bash
ps aux --sort=-%cpu | head -15
```

Correlate process names, executable paths, and parent-child relationships before identifying a process as suspicious.

---

## Issue 10

Unable to distinguish legitimate persistence from malicious persistence.

### Cause

Ubuntu enables several services by default, which may appear suspicious to new analysts.

### Resolution

Review enabled services using:

```bash
systemctl list-unit-files --state=enabled
```

Compare the output with the default Ubuntu installation and investigate only unexpected or unfamiliar services.
