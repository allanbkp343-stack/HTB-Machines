# Facts — Hack The Box Writeup

> **Platform:** HTB

---

## Summary

Facts exposes 3 open ports.  vulnerabilities found (4 total). Foothold achieved as trivia via ssh. Privilege escalation to root successful. 2 flags captured.


---

## Kill Chain

**Reconnaissance**

- Ports: 3 open on 10
- OS profile 'Linux' loaded
- HTTP: 0 live URLs
- Vulns: 0 nuclei, 0 nikto, 0 service, 6 KB matches
- Recon complete on 10
- Recon complete on facts

**Exploitation**

- Camaleon CMS CVEs found: CVE-2024-46986 (arbitrary file write → RCE, <2
- Complete attack chain: CVE-2024-46987 path traversal → MinIO creds from DB → internal bucket contains trivia's SSH key (encrypted) → ssh2john + rockyou cracked 'dragonballz' → SSH as trivia → sudo fac


---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*