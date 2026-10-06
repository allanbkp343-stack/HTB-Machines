# DevHub — Hack The Box Writeup

> **Platform:** HTB

---

## Summary

DevHub exposes 3 open ports.  vulnerabilities found (3 total). Foothold achieved as root via SSH as root via OPSMCP API dump of root SSH private key. Privilege escalation to root successful. 2 flags captured.


---

## Kill Chain

**Reconnaissance**

- Ports: 3 open on 10
- OS profile 'Linux' loaded
- HTTP: 0 live URLs
- Vulns: 0 nuclei, 0 nikto, 0 service, 8 KB matches
- RECON COMPLETE: DevHub (10
- CRITICAL: Port 6274 MCPJam Inspector - unauthenticated blind RCE via POST /api/mcp/connect

**Privilege Escalation**

- PRIVESC COMPLETE: mcp-dev -> analyst -> root via OPSMCP API dump


---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*