# Pirate — Hack The Box Writeup

> **Platform:** HTB · **Target:** `Pirate`

---

## Summary

Target exposed 26 open ports. **1 flag captured**. **3 credentials recovered**. 9 vulnerabilit identified. 34 solver scripts available.

**Foothold:** gMSA_ADFS_prod$ via NTLM PTH via reverse SSH tunnel from DC01 to Kali (WinRM)

**Tooling:** ``exploit_commands.sh` (18 lines)`


---

## Kill Chain

**Reconnaissance**

- Rustscan full-range discovered 22 open ports on 10.129.244.95. Key indicators: 53(DNS), 80(HTTP), 88(Kerberos), 389(LDAP), 445(SMB), 636(LDAPS), 3268/3269(Global Catalog), 5985(WinRM), 9389(ADWS). This is a Windows Domain Controller. TTL=127 confirms Windows OS.
- Ports: 25 open on 10.129.244.95. 53:domain Simple D, 80:http Microsoft , 88:kerberos-sec Mi, 135:msrpc Microsoft, 139:netbios-ssn Mic
- OS profile 'Windows' loaded. Payload: exe. Skill: ad-specialist. Foothold vectors: SMB null/guest session, WinRM with creds, RDP brute force, IIS web exploitation, MSSQL xp_cmdshell RCE
- HTTP: 0 live URLs. CMS: none. Clues: none.
- Vulns: 0 nuclei, 0 nikto, 2 service, 8 KB matches
- Active Directory Certificate Services (ADCS) detected: pirate-DC01-CA. Potential for ADCS abuse (ESC1-ESC13). SSL cert issued by pirate-DC01-CA.
- Nmap scan complete: Windows Server 2019 DC (pirate.htb). Ports: 53(DNS), 80(IIS10), 88(Kerberos), 135(RPC), 139(NetBIOS), 389(LDAP), 445(SMB), 464(kpasswd), 593(RPC/HTTP), 636(LDAPS), 2179(vmrdp), 3268(GC LDAP), 3269(GC LDAPS), 5985(WinRM), 9389(ADWS) + high RPC ports. ADCS pirate-DC01-CA detected v
- Pirate (10.129.244.95) is Windows Server 2019 Domain Controller. Domain: pirate.htb, DC01.pirate.htb (internal 192.168.100.1). 23 open ports: DNS(53), IIS 10.0(80/443), Kerberos(88), SMB(445), LDAP(389/636/3268/3269), WinRM(5985), ADCS detected. SMB null session works (limited). LDAP anonymous bind
- Reset-IP validation: anonymous LDAP base query on 10.129.18.65 confirms dnsHostName DC01.pirate.htb and defaultNamingContext DC=pirate,DC=htb. DC identity and domain match prior findings.
- Pirate reset-IP validation on 10.129.18.65: targeted nmap and LDAP confirm DC01.pirate.htb / pirate.htb exposure is intact. Core services unchanged from prior findings: DNS 53, IIS 80, Kerberos 88, LDAP/LDAPS/GC 389/636/3268/3269, SMB 445, RPC/HTTP 593, WinRM 5985, ADWS 9389. LDAPS certificate issue
- Ports: 27 open on 10.129.18.65. 53:domain (generic, 80:http Microsoft , 88:kerberos-sec Mi, 135:msrpc Microsoft, 139:netbios-ssn Mic
- OS profile 'Windows' loaded. Payload: exe. Skill: ad-specialist. Foothold vectors: SMB null/guest session, WinRM with creds, RDP brute force, IIS web exploitation, MSSQL xp_cmdshell RCE
- HTTP: 0 live URLs. CMS: none. Clues: none.
- Vulns: 0 nuclei, 0 nikto, 2 service, 8 KB matches
- Session-start recon validation for Pirate at 10.129.244.95. HTB lab mode. Credentials: pentest/p3nt3st2025!&. Prior session was complete with different IP (10.129.18.65). Starting fresh validation on 10.129.244.95.
- Ports: 23 open on 10.129.244.95. udp/53:domain, udp/123:ntp
- OS profile 'Windows' loaded. Payload: exe. Skill: ad-specialist. Foothold vectors: SMB null/guest session, WinRM with creds, RDP brute force, IIS web exploitation, MSSQL xp_cmdshell RCE
- HTTP: 0 live URLs. CMS: none. Clues: none.
- Vulns: 0 nuclei, 0 nikto, 2 service, 2 KB matches
- Session start: Pirate box at 10.129.244.95 is alive (TTL 127). HTB VPN connected via tun0 (10.10.17.242). Credentials pentest/p3nt3st2025!& provided by user. Mandatory recon delegation to validate current state.
- Ports: 26 open on 10.129.244.95. 53:domain (generic, 80:http Microsoft , 88:kerberos-sec Mi, 135:msrpc Microsoft, 139:netbios-ssn Mic
- OS profile 'Windows' loaded. Payload: exe. Skill: ad-specialist. Foothold vectors: SMB null/guest session, WinRM with creds, RDP brute force, IIS web exploitation, MSSQL xp_cmdshell RCE
- HTTP: 0 live URLs. CMS: none. Clues: none.
- Vulns: 0 nuclei, 0 nikto, 2 service, 8 KB matches
- Session-start recon validation on 10.129.244.95 complete. 26 ports confirmed (23 core DC ports + 3 extra low ephemeral). Windows Server 2019 DC, pirate.htb domain. pentest creds valid for SMB/LDAP/WinRM. Kerberoast hash for a.white_adm obtained. gMSA hashes (ADCS_prod$, ADFS_prod$) preserved. ADCS p
- Recon validation complete. 26 ports confirmed on 10.129.244.95. Windows Server 2019 DC, pirate.htb. ADCS confirmed. 7 users enumerated. Kerberoast hash for a.white_adm. gMSA hashes preserved. No drift from prior state.

**Exploitation**

- Fresh exploit evidence: a.white_adm still has msDS-AllowedToDelegateTo HTTP/WEB01 on reset IP. Owned gMSA hashes no longer authenticate directly on DC01. ADCS re-validation shows pirate-DC01-CA present but web enrollment disabled/inaccessible and no vulnerable template path confirmed for pentest.
- Reset IP exploit revival: MS01$ still authenticates with password ms01 using local .venv getTGT.py against 10.129.18.65. TGT saved successfully. Follow-on Kerberos LDAP bind failed only because tooling still referenced stale KDC 10.129.244.95.
- MS01$ Kerberos path restored on reset IP: bloodyAD with MS01$.ccache and explicit KDC 10.129.18.65 successfully reads gMSA_ADFS_prod msDS-ManagedPassword and returns NT hash abad63faa669b6a4eddfd46432f7ca6c.
- ADFS local-database path on WEB01 succeeded: gMSA_ADFS_prod$ can query WID AdfsConfigurationV4 over named pipe, extract ServiceSettingsData, recover DKM container metadata, read DKM thumbnailPhoto keys from AD via Kerberos LDAP, and decrypt six EncryptedPfx blobs. Decrypted artifacts include ADFS Si
- ADFS federation metadata + WS-MEX WSDL extracted. WS-Trust endpoints identified including issuedtokenmixedasymmetricbasic256 for Golden SAML. SPN for a.white_adm is ADFS/a.white with constrained delegation to HTTP/WEB01. Hashcat cracking a.white_adm's kerberoast hash with rockyou+30000 rules (est 1+
- BloodHound analysis complete: DC01$ has unconstrained delegation. IT group (a.white_adm) has WriteSPN on ALL domain computers (DC01, WEB01, MS01, EXCH01). a.white_adm in IT group with constrained delegation to HTTP/WEB01. MachineAccountQuota=10 enables RBCD. Domain Admins = Administrator only. No do
- Full AD attack chain executed: Kerberoast (hash not cracked), BloodHound (DC01 unconstrained delegate + IT group WriteSPN on ALL computers + MAQ=10), gMSA validation (stale), computer account RBCDATTACK$ created for future RBCD exploitation. Key path forward: obtain a.white_adm password (longer hash
- Branch C (MS01$ pre2k) SUCCESS: MS01$ pre2k password ms01 works on current IP 10.129.244.95. Fresh TGT obtained. gMSA hashes extracted via bloodyAD Kerberos. Both gMSA_ADFS_prod$ and gMSA_ADCS_prod$ authenticate (Pwn3d!) via WinRM to DC01 on current IP. Neither account has admin rights on DC01 (SeMa
- BRANCH B (WEB01 lateral) SUCCESS: Reverse SSH tunnel from DC01 (gMSA_ADFS_prod$) to Kali established. WinRM PTH to WEB01 via tunnel confirmed. SMB on WEB01 accessible with custom NEMESIS share. Files discovered: flags.txt (USER: [REDACTED]), credentials.txt (l.wilson_adm:Pwn3d!

**Foothold**

- Pre-Windows 2000 compatible access exploited. MS01$ machine account password: ms01. TGT obtained. Next: gMSA hash extraction via LDAP.
- Fresh validation on reset IP: gMSA_ADFS_prod$ NT hash still grants WinRM Pwn3d! access to DC01 on 10.129.18.65.
- Fresh WEB01 foothold restored on reset IP: reverse SSH tunnel from DC01 exposes WEB01:5985 locally, and gMSA_ADFS_prod$ NTLM hash authenticates to WEB01 WinRM via PTH.
- User flag captured from WEB01: [REDACTED]. gMSA_ADCS_prod$ not in CS DCOM Access group (only Remote Management Users). ADCS DCOM path blocked. New creds discovered: l.wilson_adm:Pwn3d!2026 (WinRM). Reverse SSH tunnel from DC01 to Kali established.

**Privilege Escalation**

- WEB01 privesc/credential discovery from pirate\\gMSA_ADFS_prod$ WinRM: whoami /priv exposed only SeChangeNotifyPrivilege and SeIncreaseWorkingSetPrivilege. cmdkey returned none. Winlogon exposed DefaultUserName a.white without password. Scheduled task enumeration was mostly access denied with only s
- WEB01 privesc enumeration complete. gMSA_ADFS_prod$ has no exploitable privileges (only SeChangeNotifyPrivilege, SeIncreaseWorkingSetPrivilege). No SeImpersonatePrivilege. gMSA_ADFS_prod$ not in local Administrators group - only Remote Management Users. cmdkey empty. AlwaysInstallElevated not config


---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*