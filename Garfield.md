# Garfield — Hack The Box Writeup

> **Platform:** HTB · **Target:** `10.129.34.82`

---

## Summary

Target exposed 22 open ports. **1 flag captured**. **2 credentials recovered**. 4 vulnerabilit identified. 6 solver scripts available.

**Foothold:** l.wilson_adm via scriptPath hijack -> l.wilson reverse shell -> ForceChangePassword on l.wilson_adm (WinRM)

**Tooling:** ``exploit_commands.sh` (6 lines)`


---

## Kill Chain

**Reconnaissance**

- Ports: 24 open on 10.129.34.82. 53:domain Simple D, 88:kerberos-sec Mi, 135:msrpc Microsoft, 139:netbios-ssn Mic, 389:ldap Microsoft
- OS profile 'Windows' loaded. Payload: exe. Skill: ad-specialist. Foothold vectors: SMB null/guest session, WinRM with creds, RDP brute force, IIS web exploitation, MSSQL xp_cmdshell RCE
- HTTP: 0 live URLs. CMS: none. Clues: none.
- Vulns: 0 nuclei, 0 nikto, 2 service, 8 KB matches
- Recon validation complete for 10.129.34.82 (Garfield). Confirmed Windows Server 2019 DC (DC01.garfield.htb). Domain: garfield.htb. j.arbuckle creds validated via SMB, LDAP, RDP. No WinRM access. 22 TCP ports open including typical DC services. 2 computers: DC01, RODC01. 8 users: Administrator, Guest

**Exploitation**

- Overwrote SYSVOL\garfield.htb\scripts\printerDetect.bat with payload: net user l.wilson_adm Pwn3d!2026 /domain. Scheduled task runs as l.wilson on DC01. Waiting for execution to reset l.wilson_adm password.
- Got reverse shell as l.wilson! Executing ForceChangePassword on l.wilson_adm via PowerShell ADSI, then WinRM access.

**Foothold**

- FOOTHOLD: Got WinRM as l.wilson_adm:Pwn3d!2026. Chain: scriptPath hijack -> l.wilson rev shell -> ADSI SetPassword on l.wilson_adm. Next: Add l.wilson_adm to RODC Administrators -> RBCD on RODC01$ -> tunnel to RODC01 -> krbtgt_8245 -> Golden Ticket -> DA


---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*