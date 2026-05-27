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


---

## Automatic Services

Command:

```powershell
Get-Service | Where-Object {$_.StartType -eq "Automatic"}
```


---

## Open Ports

Command:

```powershell
netstat -ano | findstr LISTENING
```


---

## User Enumeration

Commands:

```powershell
net user

net localgroup administrators
```

---

# Linux Enumeration

## Running Services

```bash
systemctl list-units --type=service --state=running
```

---

## Startup Services

```bash
systemctl list-unit-files --type=service | grep enabled
```


---

## Open Ports

```bash
ss -tulnp
```


---

## Privileged Users

```bash
cat /etc/passwd

getent group sudo
```

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
