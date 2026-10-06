<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&height=230&color=0:0f172a,40:111827,75:2563eb,100:9FEF00&text=HTB%20Machines&fontColor=ffffff&fontSize=62&fontAlignY=36&desc=Lab%20walkthroughs%20%E2%80%A2%20methodology%20notes%20%E2%80%A2%20evidence-first%20learning&descSize=17&descAlignY=58&animation=fadeIn" alt="HTB Machines" width="100%">

[![Hack The Box](https://img.shields.io/badge/Hack%20The%20Box-Walkthroughs-9FEF00?style=for-the-badge&logo=hackthebox&logoColor=black)](https://www.hackthebox.com/) [![Focus](https://img.shields.io/badge/Focus-Offensive%20Security-2563EB?style=for-the-badge&logo=gnometer&logoColor=white)](https://github.com/allanbkp343-stack) [![Policy](https://img.shields.io/badge/Policy-Retired%20Boxes%20Only-7C3AED?style=for-the-badge)](https://github.com/allanbkp343-stack/HTB-Machines) [![Guides](https://img.shields.io/badge/Full%20Guides-23-22C55E?style=for-the-badge&logo=markdown&logoColor=white)](https://github.com/allanbkp343-stack/HTB-Machines)

</div>

### Lab walkthroughs, methodology notes, and clean-root learning.

Each guide documents more than the final exploit path: how enumeration was approached, what evidence mattered, which branches failed, why the working chain works, and what a defender should take from it.

> **Spoiler policy.** Full walkthroughs are published for **retired machines only**. Flags and secrets are redacted. No target IPs are treated as live. Work here is for education, documentation practice, and defensive learning.

---

## Repository Map

| # | Machine | Guide | OS | Main Theme |
| - | ------- | ----- | -- | ---------- |
| 1 | **Bedside** | [`Bedside.md`](./Bedside.md) | Unspecified | Full walkthrough |
| 2 | **CCTV** | [`CCTV.md`](./CCTV.md) | Unspecified | Full walkthrough |
| 3 | **Cobblestone** | [`Cobblestone.md`](./Cobblestone.md) | Unspecified | cobble via Web app db creds + hash cracking |
| 4 | **Cohort** | [`Cohort.md`](./Cohort.md) | Linux | Full walkthrough |
| 5 | **DanglingTree** | [`DanglingTree.md`](./DanglingTree.md) | Unspecified | anderson.w via SMB IT share RoE PDF |
| 6 | **DarkZeroReturns** | [`DarkZeroReturns.md`](./DarkZeroReturns.md) | Unspecified | darkzero (RCE) / josh (SSH) via Handlebars AST SSTI RCE on POST /chara |
| 7 | **Devarea** | [`Devarea.md`](./Devarea.md) | Linux | Full walkthrough |
| 8 | **DevHub** | [`DevHub.md`](./DevHub.md) | Unspecified | Full walkthrough |
| 9 | **Enigma** | [`Enigma.md`](./Enigma.md) | Unspecified | information_disclosure · rce · weak_credentials · command_injection |
| 10 | **Facts** | [`Facts.md`](./Facts.md) | Linux | Full walkthrough |
| 11 | **Fries** | [`Fries.md`](./Fries.md) | Windows | Full walkthrough |
| 12 | **Garfield** | [`Garfield.md`](./Garfield.md) | Unspecified | l.wilson_adm via scriptPath hijack |
| 13 | **Helix** | [`Helix.md`](./Helix.md) | Unspecified | Full walkthrough |
| 14 | **Low-Logic** | [`Low-Logic.md`](./Low-Logic.md) | Unspecified | Full walkthrough |
| 15 | **MakeSense** | [`MakeSense.md`](./MakeSense.md) | Linux | www-data via XSS via hardcoded AES-GCM key |
| 16 | **Nimbus** | [`Nimbus.md`](./Nimbus.md) | Unspecified | nimbus-web-role (IMDS) via SSRF |
| 17 | **Offlinea** | [`Offlinea.md`](./Offlinea.md) | Unspecified | Full walkthrough |
| 18 | **Paperwork** | [`Paperwork.md`](./Paperwork.md) | Linux | Source Code Disclosure · Information Disclosure |
| 19 | **PhaseMadness** | [`PhaseMadness.md`](./PhaseMadness.md) | Unspecified | Full walkthrough |
| 20 | **Pirate** | [`Pirate.md`](./Pirate.md) | Windows | gMSA_ADFS_prod$ via NTLM PTH via reverse SSH tunnel from DC01 to Kali  |
| 21 | **Silentium** | [`Silentium.md`](./Silentium.md) | Linux | Full walkthrough |
| 22 | **Smarthire** | [`Smarthire.md`](./Smarthire.md) | Unspecified | svcweb via MLflow pickle RCE via artifact overwrite (?) |
| 23 | **VariaType** | [`VariaType.md`](./VariaType.md) | Linux | Information Disclosure |

---

## Machine Index

### By platform

| Platform | Machines | Primary techniques |
| -------- | -------- | ------------------ |
| Windows / AD | Fries, Pirate | Identity, Kerberos, SMB, ADCS, credential work |
| Linux / services | Cohort, Devarea, Facts, MakeSense, Paperwork, Silentium, VariaType | Web RCE, injection, sudo/root paths |
| Unspecified / mixed | Bedside, CCTV, Cobblestone, DanglingTree, DarkZeroReturns, DevHub, Enigma, Garfield, Helix, Low-Logic, Nimbus, Offlinea, PhaseMadness, Smarthire | Enumeration, web workflows, local recon |

### By technique

| Technique | Machines |
| --------- | -------- |
| Active Directory / identity | DanglingTree, Garfield, MakeSense, Paperwork, Pirate |
| Web application | DanglingTree, DarkZeroReturns, Enigma, Garfield, MakeSense, Nimbus, Paperwork, Smarthire, VariaType |
| Command injection | Enigma, Paperwork |
| Credentials & reuse | Cobblestone, Enigma, Garfield |

---

## Writeup Format

| Section | What it contains |
| ------- | ---------------- |
| Summary | Target profile, services, and the shape of the chain |
| Kill Chain | Phase-tagged narrative: recon → exploitation → foothold → privesc |
| Walkthrough | Reproduction steps with evidence of what each command returned |
| Ports & Services | Service inventory observed during the assessment |
| Findings | Vulnerability classes and severities identified |

Every writeup follows one idea: **the path is part of the evidence.**

```
Recon → Hypothesis → Validation → Pivot → Escalate → Evidence → Lessons
```

---

## Skills Practiced

| Area | Examples |
| ---- | -------- |
| Reconnaissance | Nmap, service/version triage, HTTP fingerprinting, NFS/SMB enumeration |
| Web security | Injection, upload abuse, source disclosure, SSRF, auth boundaries |
| Active Directory | Enumeration, Kerberos abuse, ACLs, certificate services, delegation |
| Credential work | Recovery, cracking, reuse paths, pass-the-hash |
| Privilege escalation | Sudo/SUID, services, jobs, sockets, containers |
| Evidence handling | Command/output capture, decision trail, reproducibility |

---

## Toolkit

```
nmap        netexec / nxc     bloodhound      certipy      impacket
ffuf        feroxbuster       sqlmap          burp suite   nuclei
responder   hashcat           john            metasploit   python
smbclient   ldapsearch        chisel          socat        docker
```

---

## Coverage

| Category | Count |
| -------- | ----- |
| Full walkthroughs | 23 |
| Windows / AD boxes | 2 |
| Linux / services boxes | 7 |

---

## Disclosure & Ethics

- Work is performed in authorised lab environments only (Hack The Box and equivalents).
- Full solutions are published **after machines retire**; active boxes are never spoiled.
- Flags are never included. Credentials shown are fictional lab values.
- The purpose of this repository is education, documentation practice, and defensive learning.
- Do not use these techniques outside systems you own or are explicitly authorised to test.

---

## Connect

Found an error, a cleaner approach, or want to compare methodology? Open an issue.

[**Allan Kimani Wanjiku**](https://github.com/allanbkp343-stack) — offensive security · purple team · security automation

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&height=110&section=footer&color=0:9FEF00,50:2563eb,100:0f172a" alt="" width="100%">

</div>
