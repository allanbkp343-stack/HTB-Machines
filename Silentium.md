# Silentium — Hack The Box Writeup

> **Platform:** HTB

---

## Summary

Silentium 1 exposes 2 open ports. Foothold achieved as root via local SUID root shell. Privilege escalation to root successful. 2 flags captured.


---

## Kill Chain

**Reconnaissance**

- Ports: 2 open on 10
- OS profile 'Linux' loaded
- HTTP: 0 live URLs
- Vulns: 0 nuclei, 0 nikto, 0 service, 4 KB matches
- RECON RESULTS: Target 10
- Recon complete: 2 ports open (22/SSH, 80/HTTP nginx 1
- Session-start validation on reset IP 10
- Ports: 2 open on 10
- OS profile 'Linux' loaded
- HTTP: 0 live URLs
- Vulns: 0 nuclei, 0 nikto, 0 service, 3 KB matches
- Session-start recon validation complete for reset host 10

**Exploitation**

- CRITICAL: Found staging
- CVE-2025-58434 exploit successful on staging
- SUCCESS: RCE verified via CVE-2025-59528
- CAPTCHA solved with ddddocr; created Gogs user u72602 and valid API token (stored in credentials state)

**Foothold**

- Validated SSH foothold on reset host using ben:r04D!!_R4ge; user flag retrieved at /home/ben/user

**Privilege Escalation**

- Root achieved on reset target 10


---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*