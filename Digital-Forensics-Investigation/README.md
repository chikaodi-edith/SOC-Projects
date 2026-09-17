# Digital Forensics Investigation

## Project Overview
This project contains four digital forensics investigations covering 
disk image analysis, Windows registry forensics, Windows memory 
forensics, and Linux memory forensics. Together they demonstrate a 
full range of DFIR skills — from static disk artifacts to live memory 
analysis of an active intrusion.

## Task 1: Disk Image Forensics (FTK Imager / Registry Explorer)

**Case:** Analysis of a forensic disk image (Horcrux.ad1) to reconstruct 
system configuration, user activity, and communications for the 
machine's administrator.

**What I did:**
- Loaded and browsed the forensic image using FTK Imager
- Extracted and analyzed Windows registry hives (SOFTWARE, SYSTEM, SAM) 
  using Registry Explorer
- Queried a Chrome browser history SQLite database using DB Browser 
  for SQLite
- Reviewed Outlook email archive (.ost) using SysTools OST Viewer

**Key Finding:** Identified the OS build, hostname, and confirmed the 
exact timestamp the administrator's password was last changed 
(via the SAM hive), while cross-referencing browser history to confirm 
independently which messaging application the user had installed.

**Tools:** FTK Imager, Registry Explorer, DB Browser for SQLite, SysTools 
OST Viewer

---

## Task 2: Windows Registry Forensics (TryHackMe)

**Room:** Introduction to Windows Registry Forensics

**What I did:**
- Studied registry hive structure, locations, and forensic artifacts 
  (UserAssist, ShimCache, AmCache, BAM/DAM, ShellBags)
- Completed a hands-on challenge investigating a suspected unauthorized 
  access incident on a research lab desktop

**Key Finding:** Using Registry Explorer on a KAPE triage collection, 
identified 3 user-created accounts (one never logged in), recovered a 
plaintext password hint from the SAM hive, and traced program execution 
back to a network drive (Z:) — confirming the system had been accessed 
via an external network path, with a USB device connection independently 
corroborating the timeline.

**Tools:** Registry Explorer (Eric Zimmerman), KAPE, AppCompatCacheParser

---

## Task 3: Windows Memory Forensics 

**Scenario:** Investigation of a Windows memory dump from a system 
suspected of Meterpreter infection.

**What I did:**
- Used Volatility 3 on Kali Linux to analyze a live memory capture
- Identified injected shellcode using the `malfind` plugin
- Traced network connections, persistence mechanisms, and an embedded 
  C2 domain from process memory

**Key Finding:** Reconstructed the full attack chain — a malicious 
Word macro spawned malware that used **Reflective DLL Injection** 
(MITRE T1055.001) to inject Meterpreter shellcode into a legitimate-looking 
process. The malware maintained persistence via the Windows Startup 
folder and communicated with a C2 server at `10.0.0.129`, with the 
embedded domain `kungfupandasa.com` found via string analysis of the 
process memory.

**Tools:** Volatility 3, Kali Linux

---

## Task 4: Linux Memory Forensics 

**Scenario:** Investigation of a compromised Ubuntu 20.04 system via 
a 4.29 GB memory dump.

**What I did:**
- Built a custom Volatility symbol profile for the target kernel version
- Used both Volatility 2 and Volatility 3 to extract bash history, 
  network connections, and filesystem artifacts directly from memory

**Key Finding:** Recovered a plaintext root password accidentally typed 
into bash history, traced a reverse shell connection to the attacker's 
infrastructure (`10.0.2.72:1337`), and extracted the attacker's 
persistence mechanism — a cronjob running every minute to overwrite 
`/root/.bashrc`, confirmed by pulling the malicious binary directly 
from the memory page cache and hashing it (MD5: 
`0511ccaad402d6d13ce801e1e9136ba2`).

**Tools:** Volatility 2, Volatility 3, Kali Linux

---

## Skills Demonstrated
Disk image forensics, Windows registry analysis, memory forensics, 
Volatility (2 & 3), reverse shell/C2 identification, process injection 
analysis, MITRE ATT&CK mapping, persistence mechanism identification, 
Linux forensics, forensic timeline reconstruction

## Project Evidence
The `Report` folder contains the detailed technical reports for all 
four tasks. The `Screenshots` folder contains supporting evidence.

**Note:** All investigations were conducted using simulated/training 
evidence files (TryHackMe rooms and course-provided disk/memory images). 
No real personal or organizational data is involved.
