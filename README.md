# Attack Surface Identification Lab

![Windows](https://img.shields.io/badge/Windows-Server-blue)
![Linux](https://img.shields.io/badge/Linux-Ubuntu-orange)
![PowerShell](https://img.shields.io/badge/PowerShell-Commands-blue)
![Bash](https://img.shields.io/badge/Bash-Terminal-green)
![Security](https://img.shields.io/badge/Cybersecurity-Lab-red)

---

## Description

This lab focuses on identifying elements that increase the attack surface on Windows and Linux systems.

The assessment includes:

- Running services
- Automatic startup services
- Open ports
- Process identification
- User enumeration
- Privileged accounts
- Initial hardening review
- Risk identification

---

## Lab Objectives

Identify services, ports and accounts that increase the attack surface of operating systems and understand potential security implications.

---

# Lab Methodology

The lab followed four stages:

1. Service enumeration
2. Port identification
3. User privilege analysis
4. Hardening and risk review

Detailed methodology:

[Methodology](docs/methodology.md)

---

# Windows Enumeration

## Running Services

Command:

```powershell
Get-Service | Where-Object {$_.Status -eq "Running"}
```

Screenshot:

![Running Services](screenshots/windows/running-services.png)

---

## Automatic Services

Command:

```powershell
Get-Service | Where-Object {$_.StartType -eq "Automatic"}
```

Screenshot:

![Automatic Services](screenshots/windows/automatic-services.png)

---

## Open Ports

Command:

```powershell
netstat -ano | findstr LISTENING
```

Screenshot:

![Listening Ports](screenshots/windows/listening-ports.png)

---

## User Enumeration

Commands:

```powershell
net user

net localgroup administrators
```

Screenshot:

![Users](screenshots/windows/users-admins.png)

---

# Linux Enumeration

## Running Services

```bash
systemctl list-units --type=service --state=running
```

![Services](screenshots/linux/running-services.png)

---

## Startup Services

```bash
systemctl list-unit-files --type=service | grep enabled
```

![Enabled Services](screenshots/linux/enabled-services.png)

---

## Open Ports

```bash
ss -tulnp
```

![Ports](screenshots/linux/ports.png)

---

## Privileged Users

```bash
cat /etc/passwd

getent group sudo
```

![Users](screenshots/linux/sudo-users.png)

---

# Hardening Review

Windows:

```powershell
net accounts

net localgroup administrators

Get-NetFirewallProfile
```

Linux:

```bash
ls -l /etc/shadow

ufw status
```

---

# Identified Risks

## Risk 1 — Unnecessary Services

Cause:

Services running without operational need.

Impact:

Expanded attack surface and possible unauthorized access.

---

## Risk 2 — Uncontrolled Open Ports

Cause:

Listening services without business justification.

Impact:

Remote exploitation possibilities.

---

## Risk 3 — Excessive Privileged Accounts

Cause:

Multiple users with elevated permissions.

Impact:

Unauthorized changes and larger impact during incidents.

---

# Lessons Learned

- Every running service increases attack surface.
- Open ports require operational justification.
- Least privilege should be enforced.
- Hardening reduces exposure.

---

# References

- CIS Benchmarks
- ISO/IEC 27001
- Microsoft Documentation
- Linux Documentation
