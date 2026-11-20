 # Lab 01: Network Reconnaissance & Vulnerability Assessment
## Objective
Conduct active network reconnaissance, OS fingerprinting, network sniffer detection, and automated vulnerability scanning across an 8VM simulated enterprise network.

> Disclaimer: All testing was performed strictly within an isolated, locally hosted virtual lab environment for educational purposes.

## 1. NetworkWide OS Fingerprinting via ICMP TTL Analysis
 Method: Sent ICMP Echo Requests (`ping`) across 8 virtual machines to map active hosts and infer underlying operating systems based on default TimeToLive (TTL) values.

|  | Local IP Address | Observed TTL | Inferred OS Family |
| : | : | : | : |
| 1 | `10.10.1.19` (Windows Server 2019) | `128` | Windows |
| 2 | `10.10.1.22` (Windows Server 2022) | `128` | Windows |
| 3 | `10.10.1.11` | `128` | Windows |
| 4 | `10.10.1.30` | `128` | Windows |
| 5 | `10.10.1.40` | `128` | Windows |
| 6 | `10.10.1.9` | `64` | Linux / Android |
| 7 | `10.10.1.13` | `64` | Linux / Android |
| 8 | `10.10.1.14` | `64` | Linux / Android |

 ## 2. Promiscuous Mode & Sniffer Detection (Nmap NSE)
 Target: Windows Server 2019 (`10.10.1.19`)
 Command Used: 
  ```bash
  nmap sV script=snifferdetect 10.10.1.19
  ```
 Takeaway: Used Nmap NSE scripts to audit network interfaces for unauthorized packet sniffing drivers (Npcap/WinPcap).



 ## 3. Enterprise Vulnerability Scanning (OpenVAS)
 * Target: Windows Server 2022 (`10.10.1.22`)
 *  Key Findings: Identified medium-severity exposures including DCE/RPC and MSRPC Services Enumeration Reporting and Cleartext Transmission of Sensitive Information via HTTP.
 *  Remediation: Restrict RPC endpoint access via host firewalls, enforce HTTPS/TLS encryption, and apply the latest Windows Server cumulative updates.
