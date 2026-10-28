# 🛡️ Malware Analysis Report: Trojanized FileZilla & Adware Samples

## 📝 Executive Summary
This repository contains a comprehensive analysis report of multiple suspicious files masquerading as legitimate software (FileZilla) and unknown executables. All samples were downloaded from untrusted sources with aggressive advertising. The analysis reveals a progression from basic Adware to severe Trojan infections utilizing DLL hijacking and sandbox evasion techniques. Dynamic behavior analysis was performed within an isolated Virtual Machine (VM) environment.

---

## 🔬 Analysis 1: Blocked Trojan (Windows Defender)

### 📊 Sample Details
*   **Threat Name:** `Trojan:Win32/Malgent`
*   **Status:** Blocked and Removed by Windows Defender.
*   **Affected Item:** `C:\Users\lkurb\Downloads\Не подтверждено 390248.~`
*   **Behavior Description:** The antivirus flagged this dangerous program as one that executes attacker commands. This indicates a command-and-control (C2) backdoor or a downloader.

---

## 🔬 Analysis 2: The Adware Bundler

### 📊 Sample Details
*   **File Name:** `FileZilla_3.71.1_win32-setup.exe`
*   **Size:** 12.55 MB
*   **File Type:** PE32 executable (GUI)
*   **Digital Signature:** Present (Signed)
*   **HA-256:** `e4550793f6c7fb6363cd1fb2f58c9195743d88d792dc231056b3ab9ca0234624`

### 📈 Detection Results
*   **VirusTotal:** 8/66 security vendors flagged this file.
*   **Hatching Triage Score:** 7/10 (Suspicious).
*   **Threat Labels:** `adware.playanex/bundleinstaller`, `playanex`, `filezillasponsored`.

https://ibb.co/M448nz3

### ⚠️ Static Analysis Conclusion
Despite having a digital signature, this is **not** the official installer. The word "sponsored" indicates it attempts to install third-party Adware alongside the main program. Triage flagged it with `STEALER` and `SPYWARE` tags.

---

## 🔬 Analysis 3: The Trojanized Archive & DLL Hijacking

Further investigation on the same site revealed a much more dangerous threat hidden within a ZIP archive.

### 📊 Sample Details (ZIP Archive)
*   **File Name:** `FileZilla_3.69.5_win64.zip`
*   **Size:** 17.46 MB
*   **SHA-256:** `665cca285680df321b63ad5106b167db9169afe30c17d349d80682837edcc755`
*   **VirusTotal Detection:** **38/68** security vendors flagged this archive as malicious.
*   **Threat Labels:** `trojan.tedy/abapplication`, `spreader`, `trojan`
    665cca285680df321b63ad5106b167db9169afe30c17d349d80682837edcc755 — trojanized FileZilla archive (FileZilla_3.69.5_win64.zip)
    e4c6f8ee8c946c6bd7873274e6ed9e41dec97e05890fa99c73f4309b60fd3da4 — trojanized version.dll contained in the archive
https://ibb.co/PsGwwrns
### 📊 Sample Details (Extracted DLL)
Inside the archive, a highly malicious DLL was identified:
*   **File Name:** `version.dll`
*   **Size:** 353.50 KB
*   **SHA-256:** `e4c6f8ee8c946c6bd7873274e6ed9e41dec97e05890fa99c73f4309b60fd3da4`
*   **VirusTotal Detection:** **52/71** security vendors flagged this file as malicious.
*   **Popular Threat Label:** `trojan.tedy/usblep26`
*   **Threat Categories:** `trojan`, `adware`, `pua`
https://ibb.co/FbfVpnC9
### ⚠️ Technical Insights & Dynamic Analysis (VM Environment)

1.  **DLL Hijacking Mechanism:** The malicious file is named `version.dll`. This is a classic technique where attackers replace a legitimate Windows system library with a malicious one. When the user runs the legitimate `FileZilla.exe` from the same folder, it loads the malicious `version.dll` instead, executing the attacker's code silently.
2.  **Isolated VM Execution:** The sample was extracted and tested inside an isolated Virtual Machine (VM) to observe its behavior safely without risking the host system.
3.  **Sandbox/VM Evasion:** The `detect-debug-environment` tag indicates the malware actively checks if it is running in a virtual machine or analysis sandbox. It may remain dormant or delete itself if it detects analysis tools.
4.  **Spreading Capabilities:** The `spreader` tag suggests worm-like capabilities. The malware attempts to copy itself to removable drives (like USB flash drives) to infect other systems.
5.  **System Interaction:** Tags like `calls-wmi` and `checks-bios` show the malware interacts deeply with the OS and hardware, typical for advanced trojans trying to establish persistence.

---

## 🚨 Conclusion & Recommendations
The investigation shows a clear escalation in malicious tactics on untrusted download sites. What started as an adware bundler quickly turned into a severe Trojan infection disguised as a system file.

*   **Extreme Caution Required:** The ZIP file and `version.dll` are highly dangerous.
*   **Do Not Extract or Execute:** Never open these files on a host machine.
*   **Analysis Environment:** All samples must be handled in a fully isolated virtual machine with network adapters disconnected.
*   **Lesson Learned:** Always verify the source of your downloads. Official software is rarely distributed as ZIP archives containing loose DLL files alongside the executable. Download software ONLY from official developer websites.

## 🛡️ Security Note
All dynamic analyses were conducted in an isolated Virtual Machine (VM) with network adapters disconnected (Host-Only or Internal Network) to prevent the samples from communicating with Command and Control (C2) servers and to prevent real data leakage.       

