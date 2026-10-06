# Helix — Hack The Box Writeup

> **Platform:** HTB

---

## Summary

Helix exposes 2 open ports. 1 critical 1 high vulnerabilities found (2 total total). Foothold achieved as nifi via NiFi ExecuteProcess RCE. Privilege escalation to root successful. 2 flags captured.


---

## Kill Chain

**Reconnaissance**

- Ports: 2 open on 10
- OS profile 'Linux' loaded
- HTTP: 0 live URLs
- Vulns: 0 nuclei, 0 nikto, 0 service, 3 KB matches
- Recon complete: Helix (10

**Privilege Escalation**

- ROOT PRIVESC COMPLETE: The maintenance window condition requires (Temp≥295°C OR Pressure≥73 bar) while NOT in trip


---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*