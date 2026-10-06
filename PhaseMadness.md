# PhaseMadness — Hack The Box Writeup

> **Platform:** HTB · **Target:** `154.57.164.67:30745`

---

## Summary

**1 flag captured**. 4 solver scripts available.

**Tooling:** ``solve_final.py` (151 lines)`


---

## Kill Chain

**Reconnaissance**

- Phase Madness HTB challenge - Quantum circuit with Qiskit. Flag bytes are encoded as rotation angles on qubits: RX(flag[i]*π/180) for i%3==0, RY(flag[i]*π/180) for i%3==1, H+RZ(flag[i]*π/180) for i%3==2. Recover by measuring each qubit's |1> probability and computing the inverse.

**Exploitation**

- Phase Madness solved. Recovered flag from quantum circuit by measuring each qubit's |1> probability. For RX/RY qubits used direct measurement (P1=sin²(θ/2)). For H+RZ qubits applied RY:-90 first to get same formula. Flag: HTB{70_ph453_bru73f0rc1ng_0r_n07_70_ph453_bru73f0rc1ng...7h475_7h3_qu35710n...


---

*All testing performed in an authorised Hack The Box lab environment. Full walkthroughs are published for retired machines only; flags and secrets are redacted.*