Subject: Cyber Threat Intelligence — University of Technology Sydney
Team: Arpitha Srinivasa Murthy, Sushil Acharya, Muhammad Sherwani
Format: Professional Incident Response Report
Topics: Threat Actor Profiling, IR Planning, Containment, Recovery, Post-Incident Review

Note: Group project. My contributions covered the Impact Assessment (stakeholder, social, environmental, economic, and ethical impacts) and Incident Communication & Reporting sections.


Overview
This case study is a full incident response report written for a simulated ransomware attack on Sydney Virtual Hospital by the FIN12 threat group. 
FIN12 is a financially motivated threat actor known for targeting high-revenue organisations — particularly healthcare — with ransomware payloads delivered via initial access brokers. 
The report follows a complete IR lifecycle from technical analysis through to post-incident improvement.

Threat Actor — FIN12
FIN12 is a prolific ransomware-as-a-service affiliate group active since October 2018, responsible for a significant share of healthcare-targeted ransomware globally. 

Key characteristics:
Motivation: Financial — targets high-revenue organisations likely to pay large ransoms
Primary sector: Healthcare (20% of victims), with operations across business services, finance, government, and technology
Geography: 85% of victims in North America, with incidents also reported in Australia, Ireland, France, South Korea, and the UK
Initial access method: Phishing campaigns and purchased access via initial access brokers
Malware used: TRICKBOT, BAZARLOADER as droppers; Ryuk and Conti ransomware as payloads
TTPs: Lateral movement via stolen credentials, PowerShell-based execution, persistence via scheduled tasks and RATs, AES/RSA encryption of files


Technical Analysis
Initial Access: Phishing email campaign delivering a malicious document disguised as an invoice or medical report. On opening, embedded code executed in the background.
Lateral Movement: Credential theft to elevate privileges, exploitation of unpatched systems, and PowerShell scripts blended with legitimate traffic to avoid detection.
Exfiltration: Sensitive data including medical records, financial information, and PII was extracted prior to ransomware deployment — creating a double extortion scenario.
Data Encryption: RSA or AES encryption deployed across workstations, servers, and network drives. Ransom demanded in exchange for decryption keys.
Command & Control: Encrypted C2 communications routed through anonymising services to conceal attacker location.
Persistence: Backdoors and Remote Access Trojans (RATs) installed on compromised devices; registry modifications made to maintain access.
Evasion: Fileless malware and code obfuscation used to bypass antivirus and endpoint security tools.

Impact Assessment
Stakeholder Impact
Patients faced risks of identity theft, financial fraud, and disruption to healthcare delivery. Clinical staff were unable to access electronic health records, directly affecting patient care. 
Business partners and suppliers faced potential secondary breaches through shared systems.
Social Impact
Large-scale breaches of healthcare data erode public trust in digital health services — a particularly damaging outcome for a sector that relies on patient willingness to share sensitive information. 
The psychological impact on affected individuals and the broader community is significant and long-lasting.
Economic Impact
Direct costs included ransom demands, IR consultant fees, legal expenses, and increased cyber insurance premiums. Indirect costs encompassed reputational damage, loss of patients to competitor facilities, potential regulatory fines under
the Notifiable Data Breaches (NDB) Scheme, and operational disruption across billing, scheduling, and supply chain functions.
Ethical Impact
The decision of whether to pay a ransom involves a genuine ethical dilemma — balancing urgency of restoring patient care against the risk of funding criminal operations and incentivising future attacks.

Response & Recovery
Containment: Partial and full containment strategies were evaluated. Infected systems were isolated immediately; affected network segments were quarantined to prevent lateral spread. The balance between containment thoroughness and operational continuity was a key consideration given the hospital context.
Evidence Collection: Network traffic logs, malware samples (TRICKBOT, BAZARLOADER), forensic images of affected systems, and all attacker communications were preserved following proper chain of custody procedures.
Remediation: Malware removed via scanning and patching; systems restored from verified backups; validation scans conducted before reconnecting systems to the network.
Recovery Priority Order: EHR and medical devices → financial and billing systems → network infrastructure → administrative platforms.
Estimated Timeline: Containment within hours of detection → elimination within 1–3 days → critical systems restored within 3–5 days → full restoration within one week.

Legal & Regulatory Obligations (Australian Context)

Privacy Act 1988 & Australian Privacy Principles (APPs) — enforced by the OAIC
Notifiable Data Breaches (NDB) Scheme — mandatory reporting of breaches likely to cause harm
My Health Record Act — ADHA oversight of digital health record security
Health Records and Information Privacy Act (HRIPA) — state-level obligations in NSW
Australian Cyber Security Centre (ACSC) — guidance and incident reporting


Post-Incident Improvements

Implement proactive phishing simulations and vulnerability assessments
Enforce MFA and least-privilege access controls across all systems
Establish regular penetration testing and patch management cycles
Update and test the Cyber Incident Response Plan (CIRP) using tabletop exercises
Train clinical and administrative staff on IOC recognition, suspicious behaviour, and post-incident procedures
Pursue relevant certifications for IT/security staff: CISSP, GCIH, CISA


Skills Demonstrated
Threat Actor Profiling, Incident Response, MITRE ATT&CK, Ransomware Analysis, Healthcare Cybersecurity, Australian Regulatory Compliance, Impact Assessment, IR Documentation, Post-Incident Review, FIN12, TRICKBOT, BAZARLOADER.
