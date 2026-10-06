# Smarthire — Hack The Box Writeup

> **Platform:** HTB · **Target:** `10.129.245.215`

---

## Summary

Target exposed 2 open ports. **2 flags captured**. **1 credential recovered**. 2 vulnerabilit identified. 3 solver scripts available.

**Foothold:** svcweb via MLflow pickle RCE via artifact overwrite (?)

**Tooling:** ``poc_01_rce.py` (42 lines)`


---

## Kill Chain

**Reconnaissance**

- Ports: 4 open on 10.129.245.215. 22:ssh OpenSSH 8.9, 80:http nginx 1.18
- OS profile 'Linux' loaded. Payload: elf. Skill: privesc-specialist. Foothold vectors: SSH brute / default creds, Web RCE / file upload, SQLi -> RCE (outfile/UDF), LFI -> log poisoning -> RCE, Redis unauthenticated RCE
- HTTP: 0 live URLs. CMS: none. Clues: none.
- Vulns: 0 nuclei, 0 nikto, 0 service, 2 KB matches
- RECON COMPLETE: 2 ports (22/SSH, 80/HTTP). SmartHIRE web app with MLflow backend. Credentials found: admin:password for models.smarthire.htb (MLflow Basic Auth). MLflow artifact PUT endpoint confirmed vulnerable to pickle deserialization RCE. KB confirms exact attack chain for this HTB machine. Prim


---

## Findings

| Service | Type | Severity | Detail |
| ------- | ---- | -------- | ------ |
| ? | ? | critical |  |
| ? | ? | high |  |

---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*