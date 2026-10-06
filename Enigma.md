# Enigma — Hack The Box Writeup

> **Platform:** HTB · **Target:** `10.129.30.238`

---

## Summary

Target exposed 6 open ports. **2 flags captured**. **5 credentials recovered**. 5 vulnerabilit identified. 6 solver scripts available.

**Tooling:** ``poc_02_rce.py` (42 lines)`


---

## Kill Chain

**Reconnaissance**

- NFS share enumeration on port 2049 - mounted and found a PDF with credentials: kevin:Enigma2024!

**Exploitation**

- IMAP access with kevin creds - found sarah's email containing OpenSTAManager admin credentials: admin:Ne3s4rtars78s
- OpenSTAManager 2.9.8 P7M upload CVE-2025-69212 achieved www-data RCE

**Foothold**

- User flag captured: [REDACTED] from /home/haris/user.txt

**Privilege Escalation**

- MySQL enumeration via web config - found brollin:Fri3nds@9099 and haris bcrypt hash
- Cracked haris bcrypt hash: bestfriends - used SSH key injection via webshell to get SSH access
- Discovered OliveTin 3000.10.0 REST API on 127.0.0.1:1337 - found command injection in backup_database action via db_pass single-quote breakout


---

## Findings

| Service | Type | Severity | Detail |
| ------- | ---- | -------- | ------ |
| NFS | information_disclosure | high |  |
| nginx | rce | critical |  |
| MySQL | weak_credentials | high |  |
| SSH | weak_credentials | medium |  |
| OliveTin | command_injection | critical |  |

---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*