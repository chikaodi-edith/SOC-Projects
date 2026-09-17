# Operation Hollow Crown — Multi-Stage Intrusion Investigation

## Project Overview
This capstone project investigated a simulated multi-stage cyber intrusion 
against a fictional FinTech organization (NovaPay Financial Technologies) 
over a 14-day period. The attack chain progressed from an initial phishing 
email, through a drive-by exploit kit infection, endpoint ransomware 
deployment (Akira), and culminated in full Domain Administrator compromise 
enabling a Business Email Compromise (BEC) campaign.

This was completed as a GiSOC Bootcamp final capstone project (Team 4, 
6 analysts). All organization names, employee details, and infrastructure 
in this report are part of a simulated training scenario.

## Investigation Scope
The investigation was conducted across three phases:
- **Phase 1:** Cyber Threat Intelligence & Phishing Analysis
- **Phase 2:** Network Traffic & Exploit Kit Analysis (PCAP)
- **Phase 3:** Endpoint Malware Analysis (Akira ransomware)

## My Contribution
As a member of Team 4, I participated in the investigation and analysis 
across the phishing, network traffic, and malware phases — including 
IOC extraction, MITRE ATT&CK mapping, and evidence documentation 
consolidated into the final report.

## Key Findings

### Phase 1 — Phishing & Email Analysis
- Phishing email failed all three authentication checks (SPF, DKIM, DMARC) 
  but still reached the inbox — pointing to a misconfigured email gateway
- Used a classic HTTPS-display/HTTP-redirect trick to disguise the real 
  malicious destination
- Sending infrastructure abused a trusted CDN (GitHub Inc.) to evade 
  reputation-based detection — a reminder that "clean" IP reputation 
  doesn't rule out malicious use
- Mapped to MITRE ATT&CK: T1566 (Phishing), T1566.002 (Spearphishing Link), 
  T1204 (User Execution)

### Phase 2 — Network Traffic & Exploit Kit Analysis
- Identified a drive-by download attack chain using Wireshark PCAP analysis
- Traced the exploit kit's delivery mechanism to `sploitme.com.cn/fg/load.php`, 
  serving a payload (`video.exe`) that exploited **CVE-2005-2127** 
  (msdds.dll vulnerability)
- Identified geo-fingerprinting behavior (redirect to a French Google 
  endpoint) and deobfuscated the exploit kit's tracking JavaScript
- Extracted the payload's MD5 hash and confirmed the compiler toolchain 
  (mingw-gcc 3.4.5) used to build the malware

### Phase 3 — Endpoint Malware Analysis (Akira Ransomware)
- Confirmed Akira ransomware behavior via static/dynamic analysis, aligned 
  to NIST SP 800-86 methodology
- VirusTotal confirmed high-confidence malicious classification (63/71 
  engines)
- **Key Finding:** The ransomware communicated over TOR 
  (`akira2iz6a7qgd3.onion`) for command and control, combining file 
  encryption with active anti-analysis/defense evasion techniques
- Mapped to MITRE ATT&CK: T1486 (Data Encrypted for Impact), T1027 
  (Obfuscated Files), T1090 (Proxy/TOR usage), T1083 (File and Directory 
  Discovery)

## Consolidated Indicators of Compromise (IOCs)

| Type | Indicator | Confidence |
|------|-----------|------------|
| Domain | fintech-services-support.example | HIGH |
| Domain | sploitme.com.cn | HIGH |
| Domain | shop.honeynet.sg | HIGH |
| Domain | rapidshare.com.eyu32.ru | HIGH |
| URL | http://sploitme.com.cn/fg/load.php | HIGH |
| IP (Victim) | 10.0.5.15 | HIGH |
| MD5 Hash | 5231b2db96c7f2cf030e0350e78873f791 | HIGH |
| CVE | CVE-2005-2127 | HIGH |
| TOR C2 | akira2iz6a7qgd3.onion | HIGH |
| Malware Family | Akira Ransomware | HIGH |

*Full IOC table with all 18+ indicators is available in the report.*

## Tools & Methodology
Wireshark (PCAP analysis), VirusTotal, AbuseIPDB, MXToolbox, static/dynamic 
malware analysis (isolated VM), MITRE ATT&CK framework, NIST SP 800-86 
forensic methodology

## Skills Demonstrated
Multi-phase incident investigation, phishing/email forensics, network 
traffic analysis, exploit kit deobfuscation, ransomware analysis, MITRE 
ATT&CK mapping, threat actor profiling, IOC consolidation for SIEM/threat 
intel sharing

## Project Evidence
The `Report` folder contains the full technical report. The `Screenshots` 
folder contains supporting evidence referenced throughout the investigation.

**Note:** This was a simulated/training SOC investigation conducted as a 
GiSOC Bootcamp capstone project. All organizational and personal details 
are fictional.
