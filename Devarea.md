# Devarea — Hack The Box Writeup

> **Platform:** HTB

---

## Summary

Devarea exposes 6 open ports.  vulnerabilities found (6 total). Foothold achieved as dev_ryan via reverse_tcp. Privilege escalation to root successful. 1 flag captured.


---

## Kill Chain

**Reconnaissance**

- Ports: 0 open on 10
- OS profile 'Linux' loaded
- HTTP: 0 live URLs
- Vulns: 0 nuclei, 0 nikto, 0 service, 0 KB matches
- Port scan complete: 21/ftp, 22/ssh, 80/http, 8080/http-proxy, 8500/fmtp, 8888/sun-answerbook on Devarea 10
- Recon complete on Devarea

**Exploitation**

- HoverFly credentials leaked via CXF SSRF: admin:O7IJ27MyyXiU

**Foothold**

- ROOT FLAG CAPTURED: [REDACTED] via dual symlink chain (sneaky->/root/root


---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*