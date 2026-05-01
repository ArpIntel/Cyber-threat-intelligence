Subject: Cyber Threat Intelligence — University of Technology Sydney
Tools Used: SIEM (Elastic/Kibana), MITRE ATT&CK Framework, O365 Security Logs
Topics: Ransomware Analysis, Cloud Security, Credential Compromise, Impossible Travel Detection

Overview
This final lab covered two separate real-world incident investigations — an Akira ransomware attack on an on-premises web server,and a cloud account compromise involving impossible travel and credential exposure in OneDrive. 
Both were investigated using SIEM alerts and mapped to the MITRE ATT&CK framework.

Investigation 1 — Akira Ransomware Attack
Attack Summary
An Akira ransomware variant was deployed on WebServer-01 following initial access via suspicious SMB activity from a known malicious IP (185.218.127.47). The attacker established persistence, moved laterally using PSEXEC, 
deleted volume shadow copies to prevent recovery, and deployed the ransomware payload. Interestingly, no data exfiltration was confirmed and the ransom note showed inconsistencies with known Akira TTPs, suggesting possible imitation 
rather than a direct Akira group operation.

ATT&CK Mapping
Phase             Technique          Observed Behaviour
Reconnaissance    T1592              Suspicious user activity on WebServer-01 from external host
Initial Access    T1659              Suspicious SMB login from malicious IP 185.218.127.47 via new device DESKTOP-QHSVA2H
Persistence       T1053.005          Scheduled task created on WebServer-01 for recurring malware execution
Discovery         T1518.001          Antivirus enumeration performed to identify defensive tools
Lateral Movement  T1021.002          PSEXEC remote execution from attacker's device to WebServer-01
Collection        T1005              Volume shadow copy listing performed prior to deletion
Command & Control T1219              AnyDesk (anydesk.exe) installed and executed for remote access
Exfiltration      T1020              Volume shadow copies deleted to prevent data recovery
Impact            T1485              Ransomware binary detected: 67afa125bf8812cd943abed2ed56ed6e07853600ad609b40bdf9ad4141e612b4.exe

Key IOCs
Malicious IP: 185.218.127.47
Attacker device: DESKTOP-QHSVA2H
Ransomware hash: 67afa125bf8812cd943abed2ed56ed6e07853600ad609b40bdf9ad4141e612b4
Remote access tool: anydesk.exe


Investigation 2 — O365 Account Compromise & Credential Exposure

Attack Summary
A user account (janette.richardson@ouptus.com.au) was accessed from Japan and then the United States within an impossibly short timeframe — a classic impossible travel indicator. 
Further investigation revealed credentials stored in plaintext in a OneDrive file (passwords-jr.xlsx), which the attacker accessed. Multiple lab systems went offline for extended periods following the breach, 
indicating significant operational impact.

ATT&CK Mapping
Phase           Technique            Observed Behaviour
Initial Access    T1078              O365 login from Japan — first time from this country
Persistence       T1098              Impossible travel detected — simultaneous logins from Tokyo and another location
Defense Evasion   T1548              Second login from United States shortly after Japan login
Credential Access T1555              Plaintext credentials file (passwords-jr.xlsx) accessed in OneDrive/SharePoint
Impact            T1485              Multiple lab systems (utscyberlab01, 02, 04, 05) down for 240–1440+ minutes

Compromised account: janette.richardson@ouptus.com.au
Credential file exposed: passwords-jr.xlsx, Database password.docx
Systems affected: utscyberlab01, utscyberlab02, utscyberlab04, utscyberlab05


Key Takeaways
Shadow copy deletion is a near-universal ransomware tactic — monitoring for VSS deletion commands should be a baseline detection rule in any SOC
Impossible travel alerts are high-signal indicators that should always be triaged quickly — in this case it confirmed a full account takeover
Storing credentials in plaintext files on cloud drives is one of the most common and preventable causes of cloud account compromise
AnyDesk and other legitimate remote access tools are increasingly abused by attackers — their presence alone warrants investigation in a server environment


Skills Demonstrated
Ransomware Investigation, Cloud Security, MITRE ATT&CK, SIEM Analysis, IOC Analysis, Impossible Travel Detection, Credential Exposure, Incident Response.
