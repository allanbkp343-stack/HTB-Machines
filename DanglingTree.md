# DanglingTree — Hack The Box Writeup

> **Platform:** HTB · **Target:** `10.129.13.203`

---

## Summary

Target exposed 25 open ports. **1 flag captured**. **5 credentials recovered**. 5 vulnerabilit identified. 15 solver scripts available.

**Foothold:** anderson.w via SMB IT share RoE PDF -> anderson.w creds -> WAC invokeCommand RCE (WAC 6600 RCE (CVE-2026-26119))

**Tooling:** ``exploit_commands.sh` (6 lines)`


---

## Kill Chain

**Reconnaissance**

- Recon validation complete. DC Windows Server 2025 danglingtree.htb. SMB IT share null-session leak -> RoE PDF -> anderson.w:R3dT3am@Acc3ss#01 (low-priv AD). WAC 6600 exposed. ADCS present. KB prior chain: WAC auth RCE, cert template ESC1 -> DA, SmarterMail svc_mail. Next: validate anderson.w via nxc

**Exploitation**

- WAC 6600 RCE confirmed as anderson.w (cve26119.py). SmarterMail API on 127.0.0.1:17017 returns 400 for force-reset-password and authenticate-user with both Nemesis123! and Pwned123!@#. 8443 https API also being probed. anderson.w cannot read noah.b flags directly. Need correct SmarterMail API body/p
- USER FLAG [REDACTED] captured via nxc smbexec as administrator (NTLM 8cacb3a97e460c65d105ca7cd9913925 from certipy auth PKINIT). Chain: SMB IT share -> anderson.w -> WAC 6600 RCE (CVE-2026-26119) -> chisel pivot 17017 -> SmarterMail force-reset svc_mail (CVE-2026-23760) -> noah


---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*