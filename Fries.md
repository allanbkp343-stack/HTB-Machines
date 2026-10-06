# Fries — Hack The Box Writeup

> **Platform:** HTB · **Target:** `10.129.30.24`

---

## Summary

Target exposed 24 open ports. **2 flags captured**. **7 credentials recovered**. 20 vulnerabilit identified. 21 solver scripts available.

**Tooling:** ``poc_12_rce.py` (42 lines)`


---

## Kill Chain

**Reconnaissance**

- Ports: 27 open on 10.129.35.48. 22:ssh OpenSSH 8.9, 53:domain (generic, 80:http nginx 1.18, 88:kerberos-sec Mi, 135:msrpc Microsoft
- OS profile 'Windows' loaded. Payload: exe. Skill: ad-specialist. Foothold vectors: SMB null/guest session, WinRM with creds, RDP brute force, IIS web exploitation, MSSQL xp_cmdshell RCE
- HTTP: 0 live URLs. CMS: none. Clues: none.
- Vulns: 0 nuclei, 0 nikto, 2 service, 8 KB matches
- DC01.fries.htb (10.129.35.48) is a Windows Server 2019 Domain Controller (Build 17763) with nginx 1.18.0 (Ubuntu) reverse proxy. DNS reveals domain fries.htb with NS dc01.fries.htb. Full AD ports open: Kerberos (88), LDAP (389/636/3268/3269), SMB (445), WinRM (5985), ADWS (9389). PWM (Password Self

**Foothold**

- pgAdmin container RCE achieved via CVE-2025-2945. pgadmin user (UID 5050, gid=0 root). Hostname: cb46692a4590. IP: 172.18.0.4/16. PGADMIN_ADMIN_CREDS: admin@fries.htb:Friesf00Ds2025!!. Python 3.12.9 available, nc available, no psql. Docker: overlay2 at /var/lib/docker/overlay2/5e7826ee1a67440666bcea


---

## Findings

| Service | Type | Severity | Detail |
| ------- | ---- | -------- | ------ |
| ? | ? | MEDIUM |  |
| ? | ? | INFO |  |
| ? | ? | INFO |  |
| ? | ? | INFO |  |
| ? | ? | INFO |  |
| ? | ? | INFO |  |
| ? | ? | INFO |  |
| ? | ? | INFO |  |
| ? | ? | INFO |  |

---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*