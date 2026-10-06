# VariaType — Hack The Box Writeup

> **Platform:** HTB

---

## Summary

VariaType exposes 2 open ports. 2 critical 1 high vulnerabilities found (4 total total). Foothold achieved as steve via SSH. Privilege escalation to root successful. 2 flags captured.


---

## Kill Chain

**Reconnaissance**

- Ports: 2 open on 10
- OS profile 'Linux' loaded
- HTTP: 0 live URLs
- Vulns: 0 nuclei, 0 nikto, 0 service, 5 KB matches
- New target: VariaType at 10
- Recon complete for VariaType (10
- Recon complete on Variatype 10

**Exploitation**

- RCE as www-data via CVE-2025-66034 on VariaType (10

**Foothold**

- RCE as www-data via CVE-2025-66034 - PHP webshell at shell_6pqwswmu
- Webshell confirmed: http://portal


---

## Findings

| Service | Type | Severity | Detail |
| ------- | ---- | -------- | ------ |
| ? | Information Disclosure | medium |  |

---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*