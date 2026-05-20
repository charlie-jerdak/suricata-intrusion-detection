# suricata-intrusion-detection

# Network Security & Event Monitoring: Deploying Suricata IDS for Traffic Analysis

**Date:** May 20, 2026  
**Host Platform:** Kali Linux Development Environment  
**Core Tooling:** Suricata IDS Engine (v8.0.4), TCPdump Packet Analyzer  
**Objective:** Engineer, test, and validate custom behavioral rules to intercept structural network reconnaissance signature patterns.

---

## 1. Tactical Challenge & Interface Optimization
During initial local loopback (`lo`) interface testing, modern Linux kernel network optimizations silently bypassed standard TCP/IP network socket layer stacks to save CPU cycles. This process optimization masked raw packet frames from traditional network sniffers. 

To achieve high-fidelity visibility, the testing pipeline was shifted to an offline **PCAP (Packet Capture) Forensic Analysis** workflow utilizing `tcpdump` to capture raw network states on the active outbound interface (`eth0`), bypassing socket filtering.

---

## 2. Signature Engineering
A custom signature was engineered to monitor for the foundational reconnaissance footprints used by scanning tools (such as Nmap) during host-discovery or TCP Connect phases (`-sT`).

The signature was successfully compiled into `/etc/suricata/rules/local.rules`:
```text
alert tcp any any -> any any (msg:"NMAP Scan Connection Attempt"; flags:S; sid:1000002; rev:1;)
