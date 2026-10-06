# DarkZeroReturns — Hack The Box Writeup

> **Platform:** HTB · **Target:** `10.129.76.248`

---

## Summary

Target exposed 2 open ports. **4 credentials recovered**. 3 vulnerabilit identified. 5 solver scripts available.

**Foothold:** darkzero (RCE) / josh (SSH) via Handlebars AST SSTI RCE on POST /character campaign_message (SSH as josh via Rangers1; RCE as darkzero via CVE-2026-33937)

**Tooling:** ``exploit_commands.sh` (9 lines)`


---

## Kill Chain

**Reconnaissance**

- Ports: 4 open on 10.129.76.248. 22:ssh OpenSSH 9.6, 80:http nginx 1.24
- OS profile 'Linux' loaded. Payload: elf. Skill: privesc-specialist. Foothold vectors: SSH brute / default creds, Web RCE / file upload, SQLi -> RCE (outfile/UDF), LFI -> log poisoning -> RCE, Redis unauthenticated RCE
- HTTP: 0 live URLs. CMS: none. Clues: none.
- Vulns: 0 nuclei, 0 nikto, 0 service, 2 KB matches

**Exploitation**

- RCE CONFIRMED 10.129.76.248: CVE-2026-33937 Handlebars AST type confusion via POST /character campaign_message. JSON AST: MustacheStatement path=log, BooleanLiteral value='{}, {hash: {}})) + process.mainModule.require(child_process).execSync(Buffer.from(<b64>,"base64").toString()) + Object(String(''

**Privilege Escalation**

- PRIOR-RUN NET MAP (10-129-59-153, same box): 172.16.20.1 = gateway (22/80/389/88/445/135/139), 172.16.20.2 = DC + GITEA:3000 (88/389/445/135/139/3000 open), 172.16.20.3 = SRV01 this box. DNS=172.16.20.2, domain darkzero.ext. act_runner svc-runner: kinit -kt /etc/gitea-runner/svc-runner.keytab, KRB5C
- svc-runner groups = domain users + servicehandler(780601114). find -group servicehandler AND repoaudit = NOTHING on fs. sudoers.d only README. .env = darkzero:C4ntFindMyDMpass!, SESSION_SECRET=DarkSession312#, no gitea token. BOX CRASHED Aug 6 ~07:45 UTC from RCE hammering (10 node workers + campaig


---

## Findings

| Service | Type | Severity | Detail |
| ------- | ---- | -------- | ------ |
| ? | ? | HIGH |  |
| ? | ? | LOW |  |

---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*