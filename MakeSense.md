# MakeSense — Hack The Box Writeup

> **Platform:** HTB · **Target:** `https://10.129.34.190`

---

## Summary

**1 flag captured**. **2 credentials recovered**. 4 solver scripts available.

**Foothold:** www-data via XSS via hardcoded AES-GCM key -> REST API nonce extraction -> admin user creation -> plugin upload -> webshell (webshell via WordPress plugin)

**Tooling:** ``submit_xss.py` (81 lines)`


---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*