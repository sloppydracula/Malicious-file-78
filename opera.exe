---

# Malware Analysis Report 2: OperaGXSetup.exe
https://ibb.co/RGh1c6Qy
## 📌 General Information

*   **Target:** `OperaGXSetup.exe`
*   **Size:** 4.0 MB
*   **File Type:** MZ/PE (Windows Executable)
*   **SHA256:** `44b6d40a974e20f3eb253705eb2672c6862edfade3a05e380e978750bc6819a2`
*   **Score:** 8/10 (High Threat Level)

## 🚨 Sandbox Analysis
https://ibb.co/j9cd5sZK
### Threat Tags
*   **TROJAN**
*   **STEALER**
*   **SPYWARE**
*   **DEFENSE_EVASION**
*   **DISCOVERY**
https://ibb.co/jq1HGk4
### Behavioral Signatures (Based on Report)
*   **Downloads MZ/PE file** (1 IoCs)
*   **Executes dropped EXE** (6 IoCs)
*   **Loads dropped DLL** (4 IoCs)
*   **Reads user/profile data of web browsers** (3 TTPs) - *Infostealers often target stored browser data, which can include saved credentials.*
*   **Writes a Windows system DLL name to a user directory** (2 TTPs) - *Defense Evasion: A module named after a system DLL outside System32 can be loaded instead of the real one.*
*   **Enumerates connected drives** (3 TTPs) - *Discovery: Attempts to read the root path of hard drives.*
*   **Reads the TCP/IP host and domain name from the registry** (1 TTP) - *Discovery: Profiles a host before reporting in.*
