# Nimbus — Hack The Box Writeup

> **Platform:** HTB · **Target:** `10.129.245.218`

---

## Summary

Target exposed 2 open ports. **2 flags captured**. **1 credential recovered**. 4 vulnerabilit identified. 5 solver scripts available.

**Foothold:** nimbus-web-role (IMDS) via SSRF->IMDS creds->SQS worker->CodeBuild container escape (core_pattern) (SSRF->SQS->Worker->CodeBuild)

**Tooling:** ``poc_01_ssrf.py` (34 lines)`


---

## Kill Chain

**Reconnaissance**

- Ports: 4 open on 10.129.245.218. 22:ssh OpenSSH 9.6, 80:http nginx 1.24, udp/67:dhcps, udp/68:dhcpc, udp/69:tftp
- OS profile 'Linux' loaded. Payload: elf. Skill: privesc-specialist. Foothold vectors: SSH brute / default creds, Web RCE / file upload, SQLi -> RCE (outfile/UDF), LFI -> log poisoning -> RCE, Redis unauthenticated RCE
- HTTP: 0 live URLs. CMS: none. Clues: none.
- Vulns: 0 nuclei, 0 nikto, 0 service, 8 KB matches
- Recon complete for Nimbus (10.129.245.218). Open ports: 22 (SSH), 80 (HTTP). Web app: Nimbus Job Scheduler v1.4.2 on nginx 1.24.0. Key finding: SSRF confirmed in /jobs/preview with URL parameter — bypass security filter using 127.1 or 0.0.0.0. Internal LocalStack AWS services at aws.nimbus.htb. Unau

**Foothold**

- User flag: [REDACTED]. Worker container accessing S3 via boto3 works. Now sending CodeBuild job with BASH_FUNC_id%% override + core_pattern escape for root.


---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*