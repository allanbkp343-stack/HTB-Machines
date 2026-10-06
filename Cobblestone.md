# Cobblestone — Hack The Box Writeup

> **Platform:** HTB · **Target:** `http://127.0.0.1:25151`

---

## Summary

Target exposed 2 open ports. **2 flags captured**. **3 credentials recovered**. 5 vulnerabilit identified. 10 solver scripts available.

**Foothold:** cobble via Web app db creds + hash cracking -> SSH (SSH via password)

**Tooling:** ``exploit_commands.sh` (6 lines)`


---

## Kill Chain

**Reconnaissance**

- Ports: 4 open on 10.129.232.170. 22:ssh OpenSSH 9.2, 80:http Apache htt
- OS profile 'Linux' loaded. Payload: elf. Skill: privesc-specialist. Foothold vectors: SSH brute / default creds, Web RCE / file upload, SQLi -> RCE (outfile/UDF), LFI -> log poisoning -> RCE, Redis unauthenticated RCE
- HTTP: 0 live URLs. CMS: none. Clues: none.
- Vulns: 0 nuclei, 0 nikto, 0 service, 2 KB matches
- RECON COMPLETE: cobblestone.htb (10.129.232.170). Ports: 22(SSH), 80(HTTP). OS: Debian Linux. Apache 2.4.62. Three subdomains found: deploy.cobblestone.htb (under dev), vote.cobblestone.htb (login/register), mc.cobblestone.htb (Minecraft server). PHP application with login system on vote subdomain.
- Recon complete on cobblestone. Ports 22,80. Subdomains: deploy, vote, mc. vote.cobblestone.htb has PHP login panel - primary attack surface.


---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*