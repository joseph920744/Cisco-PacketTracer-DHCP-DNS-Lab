# 🌐 DHCP & DNS Home Lab — Cisco Packet Tracer

![Lab](https://img.shields.io/badge/Tool-Cisco%20Packet%20Tracer-blue) ![Status](https://img.shields.io/badge/Status-Completed-brightgreen) ![Level](https://img.shields.io/badge/Level-Beginner-orange) ![Series](https://img.shields.io/badge/Series-SOC%20Home%20Labs-blueviolet)

---

## 📋 Overview

This lab demonstrates the configuration and validation of **DHCP** (Dynamic Host Configuration Protocol) and **DNS** (Domain Name System) services in a simulated LAN environment using Cisco Packet Tracer. These are foundational network services that SOC analysts encounter in almost every security investigation — from IP attribution in incidents to DNS-based threat hunting.

---

## 🎯 Objectives

- Configure a 2911 Router as the default gateway for a LAN
- Set up a Server with a static IP providing both DHCP and DNS services
- Verify automatic IP assignment to DHCP client PCs
- Validate DNS name resolution using `nslookup` and `ping` by domain name

---

## 🖧 Network Topology

```
           [2911 Router0]
                 |
           [2960 Switch0]
          /      |        \
   [Server0]  [PC0]     [PC1]
  192.168.1.10
```

| Device | Role | IP Address |
|--------|------|------------|
| Router0 (2911) | Default Gateway | 192.168.1.1 |
| Server0 (Server-PT) | DHCP + DNS Server | 192.168.1.10 (Static) |
| PC0 | DHCP Client | 192.168.1.100 (DHCP) |
| PC1 | DHCP Client | 192.168.1.101 (DHCP) |

---

## ⚙️ Configuration

### Router (GigabitEthernet0/0)
```
enable
configure terminal
interface gig0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```

### Server — Static IP
- IP: `192.168.1.10`
- Subnet Mask: `255.255.255.0`
- Gateway: `192.168.1.1`

### DHCP Pool (serverPool)
| Parameter | Value |
|-----------|-------|
| Default Gateway | 192.168.1.1 |
| DNS Server | 192.168.1.10 |
| Start IP | 192.168.1.100 |
| Subnet Mask | 255.255.255.0 |
| Max Users | 50 |

### DNS Record
| Name | Type | Address |
|------|------|---------|
| www.testlab.com | A Record | 192.168.1.10 |

---

## ✅ Test Results

| Test | Command | Result |
|------|---------|--------|
| PC0 DHCP Assignment | — | 192.168.1.100 ✅ |
| PC1 DHCP Assignment | — | 192.168.1.101 ✅ |
| Ping by IP | `ping 192.168.1.10` | 4/4 packets, 0% loss ✅ |
| DNS Resolution | `nslookup www.testlab.com` | Resolved → 192.168.1.10 ✅ |
| Ping by Domain | `ping www.testlab.com` | 4/4 packets, 0% loss ✅ |

---

## 🔍 SOC Analyst Relevance

| Protocol | Why It Matters in SOC |
|----------|----------------------|
| **DHCP** | DHCP logs map IP addresses to devices — essential for attributing malicious activity to a specific host during incident response |
| **DNS** | DNS logs are critical for threat hunting — C2 beacons, malware staging, and data exfiltration commonly use DNS (as seen in the Wireshark PCAP lab) |
| **Rogue DHCP** | Attackers can deploy rogue DHCP servers to redirect gateway/DNS settings and intercept traffic |
| **DNS Spoofing** | Manipulating A records to redirect users to malicious IPs — understanding legitimate DNS is the baseline for detecting anomalies |

---

## 📁 Lab Files

| File | Description |
|------|-------------|
| `DHCP_DNS_Lab_Report.docx` | Full professional lab report with screenshots |
| `README_DHCP_DNS_Lab.md` | This file |

---

## 🧰 Tools Used

- **Cisco Packet Tracer** — Network simulation
- **2911 Router** — Default gateway configuration
- **2960-24TT Switch** — Layer 2 switching
- **Server-PT** — DHCP and DNS services
- **PC Command Prompt** — `ping` and `nslookup` testing

---

## 🔗 Related Labs

| Lab | Description |
|-----|-------------|
| [Splunk SIEM Lab](../Splunk-SIEM-Lab) | SSH brute-force detection with SPL queries |
| [Wazuh SOC Lab](../Wazuh-SOC-Lab) | Custom rules, MITRE ATT&CK T1110 mapping |
| [SOC PCAP Analysis](../SOC-PCAP-Analysis-Labs) | Wireshark C2 beacon detection |

---

## 👤 Author

**Paulson K Babu (Jude)**
MCA Graduate — APJ Abdul Kalam Technological University, Kerala

[![LinkedIn](https://img.shields.io/badge/LinkedIn-paulson--babu-blue)](https://linkedin.com/in/paulson-babu-472563215)
[![GitHub](https://img.shields.io/badge/GitHub-joseph920744-black)](https://github.com/joseph920744)
