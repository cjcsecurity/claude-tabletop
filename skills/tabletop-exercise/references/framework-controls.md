# Framework controls — TTX-relevant subset

This file is a curated working set of compliance and security framework controls that frequently surface in tabletop exercises. It is **not exhaustive**. Each framework has hundreds of controls; this document focuses on the 15-25 per framework most likely to be touched by a realistic incident-response, detection, communications, recovery, escalation, or vendor-management scenario. Controls that a tabletop almost never exercises directly — physical security, HR onboarding, deep cryptographic key management, low-level network segmentation engineering — are intentionally omitted.

The runbook generator uses this file **only** when the user passes `--frameworks <list>`. In that mode the generator tags injects with the most-applicable control IDs from the requested frameworks and emits a coverage matrix at the end of the runbook. If you need full coverage for an audit, consult the official framework documentation directly — these are control IDs as they appear in the standards, but the descriptions here are TTX-flavored summaries, not authoritative control text.

When in doubt about a control ID's exact spelling, defer to the closest correct identifier rather than fabricating one. The point of the matrix is that an auditor or compliance reader can take an inject and trace it back to the source standard.

---

## NIST Cybersecurity Framework (CSF) 2.0

Released February 2024 by NIST. A voluntary framework of cybersecurity outcomes organized into six Functions: **GOVERN (GV)**, **IDENTIFY (ID)**, **PROTECT (PR)**, **DETECT (DE)**, **RESPOND (RS)**, **RECOVER (RC)**. Each Function decomposes into Categories (e.g. `RS.MA`) and Subcategories (e.g. `RS.MA-01`). Used by US federal contractors, critical infrastructure, and as a generic baseline by many private-sector security programs. Highly TTX-friendly because the entire RS and RC functions read like an exercise script — the 2.0 revision pulled supply-chain and governance into first-class functions, both of which surface in modern scenarios. Use this when the audience is security leadership, federal-adjacent, or doing program-level maturity work.

| Control ID | Title | What an inject testing this looks like |
|---|---|---|
| GV.RR-02 | Roles, responsibilities, and authorities for cybersecurity are established | Mid-incident an exec asks "who actually has authority to take the prod database offline?" and nobody can answer |
| GV.SC-08 | Relevant suppliers and third parties are included in incident planning, response, and recovery | Vendor's status page goes red; team must escalate per a contract nobody has read |
| ID.RA-08 | Processes for receiving, analyzing, and responding to vulnerability disclosures are established | Anonymous email arrives describing an unauth IDOR; team must triage without panicking |
| ID.IM-02 | Improvements are identified from security tests and exercises, including those done in collaboration with suppliers and third parties | (Meta-control — the existence of this exercise satisfies it) |
| PR.AA-05 | Access permissions, entitlements, and authorizations are defined, managed, and enforced | An ex-employee's still-active token shows up in audit logs hours into the incident |
| PR.IR-04 | Adequate resource capacity to ensure availability is maintained | Auto-scaler hits the cloud account quota during a traffic spike caused by the incident |
| DE.CM-01 | Networks and network services are monitored to find potentially adverse events | First inject: "this Datadog monitor just paged" — does the team treat it as signal or noise? |
| DE.CM-03 | Personnel activity and technology usage are monitored to find potentially adverse events | Insider-threat scenario: an admin's session shows unusual command history |
| DE.CM-09 | Computing hardware and software, runtime environments, and their data are monitored to find potentially adverse events | EDR alert on a developer laptop in the middle of a release |
| DE.AE-02 | Potentially adverse events are analyzed to better understand associated activities | Team has 3 alerts, must decide which is the lead, which are noise, which are related |
| DE.AE-03 | Information is correlated from multiple sources | SIEM, application logs, and a customer support ticket all show pieces of the same incident |
| DE.AE-04 | The estimated impact and scope of adverse events are understood | Forced to put a number on "how many customers affected" within 30 minutes |
| DE.AE-06 | Information on adverse events is provided to authorized staff and tools | Who gets paged, when, on which channel — and does the on-call actually see it |
| DE.AE-07 | Cyber threat intelligence and other contextual information are integrated into the analysis | A CISA advisory dropped this morning; is that the same CVE the team is seeing exploited? |
| RS.MA-01 | The incident response plan is executed in coordination with relevant third parties once an incident is declared | Forces explicit "we are now declaring an incident" moment and IR plan retrieval |
| RS.MA-02 | Incident reports are triaged and validated | First-responder must distinguish a real incident from a flapping monitor |
| RS.MA-03 | Incidents are categorized and prioritized | Severity-call inject: SEV1, SEV2, or SEV3? Team must justify |
| RS.MA-04 | Incidents are escalated or elevated as needed | Scope expands; team must decide whether to wake up the CEO at 2am |
| RS.AN-03 | Analysis is performed to establish what has taken place during an incident and the root cause | Whodunit moment — what process actually led to the data exposure |
| RS.AN-06 | Actions performed during an investigation are recorded, and the records' integrity and provenance are preserved | Decision-log discipline test; can the team reconstruct timeline an hour after the fact |
| RS.AN-07 | Incident data and metadata are collected, and their integrity and provenance are preserved | Forensic-evidence inject: somebody nukes the affected EC2 instance "to be safe" |
| RS.CO-02 | Internal and external stakeholders are notified of incidents | Comms call: customer email, status page, regulator, board — in what order, with what message |
| RS.CO-03 | Information is shared with designated internal and external stakeholders | A reporter calls the support line claiming to have sources inside; what does support say |
| RS.MI-01 | Incidents are contained | Containment trade-off: take a service down (customer impact) or leave it up (broader compromise risk) |
| RS.MI-02 | Incidents are eradicated | Eradication-vs-evidence tension: rebuild the host now, or preserve it for IR/legal |
| RC.RP-01 | The recovery portion of the incident response plan is executed once initiated by the incident response process | Trigger the recovery plan; does anybody actually have the runbook |
| RC.RP-02 | Recovery actions are selected, scoped, prioritized, and performed | Forced ordering: restore payments first, or restore the auth service first |
| RC.RP-04 | Critical mission functions and cybersecurity risk management are considered to establish post-incident operational norms | "When is this incident over" decision — premature all-clear vs over-cautious |
| RC.CO-03 | Recovery activities and progress in restoring operational capabilities are communicated to designated internal and external stakeholders | Status-page update cadence; "we are still investigating" loop trap |

---

## SOC 2 (Trust Services Criteria 2017, with 2022 points of focus)

The AICPA's Trust Services Criteria, used to scope SOC 2 Type I/II audits. Five criteria: **Security** (Common Criteria, mandatory), **Availability**, **Processing Integrity**, **Confidentiality**, **Privacy**. Common Criteria (CC) numbering follows COSO categories: CC1 (control environment), CC2 (communication), CC3 (risk assessment), CC4 (monitoring), CC5 (control activities), CC6 (logical/physical access), CC7 (system operations), CC8 (change management), CC9 (risk mitigation). SaaS companies with US enterprise customers almost always have or want a SOC 2 report. Highly TTX-relevant because auditors specifically look for evidence of incident response testing, and CC7.x maps cleanly onto IR exercises.

| Control ID | Title | What an inject testing this looks like |
|---|---|---|
| CC2.2 | Internal communication of information necessary to support functioning of internal control | An on-call engineer doesn't know how to reach legal at 3am — surface the gap |
| CC2.3 | Communication with external parties on matters affecting the functioning of internal control | Customer ABM calls asking for an update; what does the AE say without making it worse |
| CC3.2 | Identification and analysis of risks to achieve objectives | "We never planned for this" moment — risk register coverage check |
| CC4.1 | Selection, development, and operation of evaluations to ascertain whether internal controls are present and functioning | The exercise itself satisfies this |
| CC4.2 | Evaluation and communication of internal control deficiencies | Hotwash gap-capture flows into the next quarter's roadmap |
| CC5.2 | Establishment of activities through policies and procedures | Forced lookup: "where is the IR runbook actually stored, and is it current" |
| CC6.1 | Logical and physical access controls restrict unauthorized access | Compromised credential inject; how is the blast radius scoped |
| CC6.2 | Prior to issuing system credentials, registers and authorizes new internal and external users | Forgotten contractor account is the entry vector |
| CC6.3 | Authorizes, modifies, or removes access to data and software based on roles and responsibilities | Just-in-time access review during the incident |
| CC6.6 | Logical access security measures protect against external threat | WAF/CDN config question: what's actually in front of prod |
| CC6.7 | Restricts the transmission, movement, and removal of information | Data-exfil scenario: did egress controls catch it |
| CC6.8 | Implements controls to prevent or detect and act upon the introduction of unauthorized or malicious software | Supply-chain compromise inject: a popular npm package gets backdoored |
| CC7.1 | Detection and monitoring procedures to identify changes to configurations | Unauthorized prod config change shows up in audit logs |
| CC7.2 | Monitors system components and the operation of those components for anomalies | First-line monitoring: who sees the alert, how fast |
| CC7.3 | Evaluates security events to determine whether they could or have resulted in a failure to meet its objectives | Triage inject: is this an incident or not |
| CC7.4 | Responds to identified security incidents by executing a defined incident response program | The whole exercise |
| CC7.5 | Identifies, develops, and implements activities to recover from identified security incidents | Recovery phase coverage |
| CC8.1 | Authorizes, designs, develops or acquires, configures, documents, tests, approves, and implements changes to infrastructure, data, software, and procedures | Emergency change during incident — does it follow change-control or skip it |
| CC9.1 | Identifies, selects, and develops risk mitigation activities | Did the previous risk assessment cover this scenario; if not, why |
| CC9.2 | Assesses and manages risks associated with vendors and business partners | Third-party SaaS goes down; is there a contractual SLA, who calls them |
| A1.1 | Maintains, monitors, and evaluates current processing capacity and use of system components | Capacity/scaling failure inject |
| A1.2 | Authorizes, designs, develops or acquires, implements, operates, approves, maintains, and monitors environmental protections, software, data backup processes, and recovery infrastructure | Backup-restore drill: when did we last test the restore path |
| A1.3 | Tests recovery plan procedures supporting system recovery | DR/BCP exercise component |
| C1.1 | Identifies and maintains confidential information to meet its objectives related to confidentiality | Data-classification gap during a leak |
| C1.2 | Disposes of confidential information to meet its objectives related to confidentiality | Old data lying around in a backup blast-radius extension |

---

## PCI DSS v4.0

Payment Card Industry Data Security Standard, version 4.0 (released March 2022, full mandatory enforcement March 2025). Applies to any entity that stores, processes, or transmits cardholder data, plus their service providers. Twelve top-level requirements; in TTX context Requirements 6 (secure development), 10 (logging and monitoring), 11 (testing), and 12 (security policies, including IR) carry most of the weight. Requirement 12.10 in particular specifies an incident response plan, IR testing at least annually, and incident communication — that subsection is essentially the PCI checklist for "did this exercise happen."

| Control ID | Title | What an inject testing this looks like |
|---|---|---|
| 6.3.3 | All system components are protected from known vulnerabilities by installing applicable security patches/updates | Unpatched library exploited mid-exercise |
| 6.4.1 | For public-facing web applications, address new threats and vulnerabilities on an ongoing basis | WAF rule lag during active exploitation |
| 6.5.1 | Changes to all system components are managed | Emergency change goes around change control |
| 10.2.1 | Audit logs capture all individual user access to cardholder data | Investigator asks for the log; team finds the log doesn't capture what was promised |
| 10.2.2 | Audit logs capture all actions taken by any individual with administrative access | Admin-action gap: what privileged user did what when |
| 10.3.1 | Audit log contents meet specified requirements (user, event type, date/time, success/failure, origination, affected resource) | Forensic completeness — can we actually reconstruct what happened |
| 10.4.1 | Audit logs are reviewed at least daily for all system components that store, process, or transmit cardholder data | Detection-lag question: how stale was the last log review |
| 10.7.1 | Failures of critical security control systems are detected, alerted, and addressed promptly | The IDS itself is offline — who would know |
| 11.4.1 | A penetration testing methodology is defined, documented, and implemented | Outcome of last pentest gets dusted off mid-exercise |
| 11.5.1 | Intrusion-detection and/or intrusion-prevention techniques are used to detect and/or prevent intrusions into the network | IDS alerted but nobody saw it |
| 11.5.2 | A change-detection mechanism (e.g. file integrity monitoring) is deployed | FIM alert during the incident |
| 12.6.1 | A formal security awareness program is implemented | Phish-simulation tie-in: user clicks the link in the inject |
| 12.6.3 | Personnel are aware of incident response procedures | Random participant asked "what's our IR phone number" |
| 12.10.1 | An incident response plan exists and is ready to be activated in the event of a suspected or confirmed security incident | Plan activation inject: who calls the activation, on what evidence |
| 12.10.2 | At least once every 12 months, the incident response plan is reviewed, updated, and tested | (The exercise satisfies this) |
| 12.10.3 | Specific personnel are designated to be available on a 24/7 basis to respond to suspected or confirmed security incidents | After-hours incident; who actually picks up |
| 12.10.4 | Personnel responsible for responding to suspected and confirmed security incidents are appropriately and periodically trained | Tested by the exercise itself |
| 12.10.5 | The IR plan addresses monitoring and responding to alerts from all required security monitoring systems | Alert-from-an-unfamiliar-tool inject: nobody knows what to do with a Wiz finding |
| 12.10.6 | The IR plan is modified and evolved according to lessons learned and to incorporate industry developments | Hotwash → AAR → plan update loop |
| 12.10.7 | IR procedures are in place that include actions in case of suspected or confirmed Primary Account Number storage in unintended locations | PAN found in a log file: declare? notify card brands? |
| 12.5.2 | The PCI DSS scope is documented and confirmed by the entity at least once every 12 months | Scope-creep mid-incident: is this even in PCI scope |
| 3.2.1 | Account Data storage is kept to a minimum | Discovered cache of historical PANs from a long-deprecated feature |

---

## ISO/IEC 27001:2022

ISO/IEC 27001 specifies requirements for an Information Security Management System (ISMS). The 2022 revision restructured Annex A from 114 controls into 93 controls organized in four themes: **A.5 Organizational**, **A.6 People**, **A.7 Physical**, **A.8 Technological**. Compared to the 2013 version, incident management is consolidated under A.5.24-A.5.28 and continuity under A.5.29-A.5.30. Used globally, especially outside the US — common in EU, UK, Asia-Pacific. The certification cycle includes mandatory IR-plan testing, so a tabletop exercise generates documentary evidence that auditors expect to see.

| Control ID | Title | What an inject testing this looks like |
|---|---|---|
| A.5.2 | Information security roles and responsibilities | Role-confusion moment: who declares the incident, who runs comms |
| A.5.7 | Threat intelligence | A CTI feed item from this morning is the inject's seed |
| A.5.19 | Information security in supplier relationships | Third-party SaaS vendor compromise |
| A.5.20 | Addressing information security within supplier agreements | Contract pull — what does the MSA say about breach notification |
| A.5.21 | Managing information security in the ICT supply chain | npm/PyPI package poisoning scenario |
| A.5.22 | Monitoring, review and change management of supplier services | Vendor's incident impacts your service; how is it tracked |
| A.5.23 | Information security for use of cloud services | Cloud-provider control-plane outage |
| A.5.24 | Information security incident management planning and preparation | Plan-existence and plan-retrieval check |
| A.5.25 | Assessment and decision on information security events | Triage decision: is this an event, or a real incident |
| A.5.26 | Response to information security incidents | The exercise main loop |
| A.5.27 | Learning from information security incidents | Hotwash + AAR satisfy this |
| A.5.28 | Collection of evidence | Forensic-preservation inject (don't nuke the host) |
| A.5.29 | Information security during disruption | BCP integration — IR happening alongside outage |
| A.5.30 | ICT readiness for business continuity | Recovery-time and recovery-point objective conversation |
| A.5.31 | Legal, statutory, regulatory and contractual requirements | Multi-jurisdictional notification timing puzzle |
| A.5.34 | Privacy and protection of PII | PII-in-scope sub-incident |
| A.6.3 | Information security awareness, education and training | Random participant tested on basic IR steps |
| A.6.8 | Information security event reporting | Junior eng spots the anomaly — what's the reporting channel |
| A.8.8 | Management of technical vulnerabilities | CVE-of-the-day exploited live |
| A.8.15 | Logging | Log-coverage gap during forensics |
| A.8.16 | Monitoring activities | Did the SOC see it; was the SOC even staffed |
| A.8.23 | Web filtering | Phishing-domain block timing |
| A.8.25 | Secure development life cycle | Vulnerability traced back to SDL gap |
| A.8.32 | Change management | Emergency-change discipline mid-incident |

---

## HIPAA Security Rule + Breach Notification Rule

The HIPAA Security Rule (45 CFR §164.302-318) establishes administrative, physical, and technical safeguards for electronic Protected Health Information (ePHI). For TTX purposes the relevant subsection is **§164.308 — Administrative Safeguards**, especially the contingency plan and security incident procedures. Layered on top is the HITECH-modified Breach Notification Rule (45 CFR §164.400-414) which requires notice to affected individuals within 60 days, notice to HHS (immediately for breaches ≥500 individuals, annually for smaller breaches), and notice to media for breaches ≥500 individuals in a state/jurisdiction. Health-tech, payer, provider, clearinghouse, and Business Associate scenarios all live here.

| Control ID | Title | What an inject testing this looks like |
|---|---|---|
| §164.308(a)(1)(ii)(A) | Risk Analysis | "We never assessed this risk" gap |
| §164.308(a)(1)(ii)(B) | Risk Management | Mitigation-decision call during incident |
| §164.308(a)(1)(ii)(D) | Information System Activity Review | Audit log review pace |
| §164.308(a)(2) | Assigned Security Responsibility | "Who is the Security Official" — fill in the blank |
| §164.308(a)(3)(ii)(C) | Termination Procedures | Departed employee's still-active access surfaces |
| §164.308(a)(5)(ii)(B) | Protection from Malicious Software | Malware in clinical workstation scenario |
| §164.308(a)(5)(ii)(C) | Log-in Monitoring | Brute-force on a portal account |
| §164.308(a)(6)(i) | Security Incident Procedures (standard) | Plan-retrieval and execution test |
| §164.308(a)(6)(ii) | Response and Reporting | Internal reporting chain — who tells the Privacy Officer |
| §164.308(a)(7)(i) | Contingency Plan (standard) | BCP/DR component |
| §164.308(a)(7)(ii)(A) | Data Backup Plan | Restore-from-backup drill |
| §164.308(a)(7)(ii)(B) | Disaster Recovery Plan | Site-failover scenario |
| §164.308(a)(7)(ii)(C) | Emergency Mode Operation Plan | Operating without ePHI access for N hours |
| §164.308(a)(7)(ii)(D) | Testing and Revision Procedures | (The exercise satisfies this) |
| §164.308(a)(8) | Evaluation | Periodic evaluation of safeguards |
| §164.308(b)(1) | Business Associate Contracts and Other Arrangements | BAA pull — what does it require during an incident |
| §164.310(d)(2)(i) | Disposal | Disposed-but-not-wiped device discovered |
| §164.312(a)(1) | Access Control | RBAC failure inject |
| §164.312(b) | Audit Controls | Audit log gap |
| §164.312(c)(1) | Integrity | Data-integrity question (was the record altered) |
| §164.312(e)(1) | Transmission Security | Unencrypted transmission discovered |
| §164.404 | Notification to Individuals (Breach Notification Rule) | 60-day clock starts ticking — when |
| §164.406 | Notification to the Media (≥500 individuals in a state) | PR call: do we notify; when; through which channel |
| §164.408 | Notification to the Secretary (HHS) | Reportable-now vs end-of-year reporting decision |
| §164.410 | Notification by a Business Associate | If you ARE the BA, what does the covered entity contract say |

---

## GDPR (EU 2016/679)

Strictly speaking GDPR is a regulation, not a controls framework. For TTX purposes the operative articles are around incident notification, security of processing, and processor obligations. The supervisory-authority notification window (**72 hours** under Article 33) is one of the highest-pressure mechanical clocks in any tabletop. Applies to any processing of personal data of EU/EEA data subjects, regardless of where the controller/processor sits. Often co-applicable with UK GDPR (post-Brexit) which mirrors the structure but reports to the ICO instead.

| Article | Title | What an inject testing this looks like |
|---|---|---|
| Art. 5(1)(f) | Integrity and confidentiality (security principle) | Data-exposure inject; was processing "appropriately" secured |
| Art. 5(2) | Accountability | "Document why you decided X" — was it documented |
| Art. 24 | Responsibility of the controller | Controller-vs-processor confusion mid-incident |
| Art. 25 | Data protection by design and by default | Feature shipped without DPIA, now vulnerable |
| Art. 28 | Processor | Processor obligations clause: must "assist" controller during incident |
| Art. 28(3)(f) | Processor must assist controller in ensuring compliance with Art. 32-36 obligations | Sub-processor calls; you're the processor; the controller wants info now |
| Art. 30 | Records of processing activities | Pull the RoPA mid-incident; is it accurate |
| Art. 32 | Security of processing | Was the technical/organizational measure "appropriate" |
| Art. 33 | Notification of personal data breach to the supervisory authority (within 72 hours) | The 72-hour clock — when does it start, who calls it |
| Art. 33(3) | Required content of supervisory-authority notification | Drafting the notification with incomplete information |
| Art. 33(5) | Documentation of all personal data breaches | "Show me the breach register" |
| Art. 34 | Communication of personal data breach to the data subject | Customer-facing comms decision: notify, with what message, on what timeline |
| Art. 34(3) | Exceptions to data-subject notification (encryption, mitigation, disproportionate effort) | Encryption-defense argument — does it hold up |
| Art. 35 | Data Protection Impact Assessment | Was a DPIA done for the affected processing |
| Art. 37-39 | Data Protection Officer | DPO loop-in timing |
| Art. 44-50 | Transfers to third countries | Cross-border-transfer wrinkle (e.g. data is in a US region that fell over) |
| Art. 82 | Right to compensation and liability | Class-action reality check |
| Art. 83 | General conditions for imposing administrative fines | Worst-case-fine framing for the leadership pressure beat |

---

## MITRE ATT&CK

Curated knowledge base of adversary tactics, techniques, and procedures (TTPs) maintained by MITRE. Organized as a matrix: **tactics** (the why — e.g. Initial Access, Execution, Persistence, Privilege Escalation, Defense Evasion, Credential Access, Discovery, Lateral Movement, Collection, Command and Control, Exfiltration, Impact) cross-referenced with **techniques** (the how — e.g. T1566 Phishing). Used heavily by red teams, blue teams, threat intel, and detection engineering. In TTX context, ATT&CK provides the vocabulary for "what is the adversary actually doing" — useful for coloring injects with realism and for mapping detection coverage gaps. The full enterprise matrix has 200+ techniques and ~600 sub-techniques; this is a curated 25-30 most likely to surface in cybersec tabletops.

| Technique ID | Title (Tactic) | What an inject testing this looks like |
|---|---|---|
| T1566 | Phishing (Initial Access) | Spearphish lands; user clicks the link |
| T1566.001 | Spearphishing Attachment (Initial Access) | Macro-laden document detonates on a finance user's box |
| T1566.002 | Spearphishing Link (Initial Access) | Credential-harvest page mimics SSO portal |
| T1190 | Exploit Public-Facing Application (Initial Access) | Unauth RCE in a public web app — first sign is anomalous outbound traffic |
| T1133 | External Remote Services (Initial Access) | Compromised VPN credentials used outside business hours |
| T1078 | Valid Accounts (Initial Access / Persistence / Defense Evasion) | "It looks like a valid login because it IS a valid login" |
| T1059 | Command and Scripting Interpreter (Execution) | Suspicious PowerShell / bash -c invocation in EDR |
| T1059.001 | PowerShell (Execution) | Encoded PowerShell command on a Windows endpoint |
| T1053 | Scheduled Task/Job (Persistence / Execution) | Cron job appears that nobody created |
| T1098 | Account Manipulation (Persistence) | New IAM access key issued for a service account at 3am |
| T1136 | Create Account (Persistence) | Unfamiliar user account in Okta |
| T1068 | Exploitation for Privilege Escalation (Privilege Escalation) | Local privesc via known kernel CVE |
| T1548 | Abuse Elevation Control Mechanism (Privilege Escalation) | sudo abuse / setuid binary discovery |
| T1110 | Brute Force (Credential Access) | Login flood from one ASN against a portal |
| T1110.003 | Password Spraying (Credential Access) | One password tried across many accounts |
| T1555 | Credentials from Password Stores (Credential Access) | Browser credential store dump on a compromised endpoint |
| T1003 | OS Credential Dumping (Credential Access) | LSASS dump observed on a domain controller |
| T1083 | File and Directory Discovery (Discovery) | Recon commands observed (find, ls -la /etc, etc.) |
| T1018 | Remote System Discovery (Discovery) | Internal port scan from a compromised host |
| T1021 | Remote Services (Lateral Movement) | RDP / SSH / WMI use between hosts that don't normally talk |
| T1021.001 | Remote Desktop Protocol (Lateral Movement) | RDP from a workstation into a server tier |
| T1021.004 | SSH (Lateral Movement) | SSH from a developer laptop directly into prod |
| T1071 | Application Layer Protocol (Command and Control) | Beacon traffic over HTTPS to an unfamiliar domain |
| T1071.001 | Web Protocols (Command and Control) | C2 over plain HTTP/S to a CDN-fronted endpoint |
| T1568 | Dynamic Resolution (Command and Control) | DGA-like outbound queries |
| T1567 | Exfiltration Over Web Service (Exfiltration) | Large upload to a paste site or unfamiliar SaaS |
| T1041 | Exfiltration Over C2 Channel (Exfiltration) | Beacon channel suddenly carries volume |
| T1567.002 | Exfiltration to Cloud Storage (Exfiltration) | Mass S3/GCS/Azure-Blob writes to an external account |
| T1486 | Data Encrypted for Impact (Impact) | Ransomware trigger across a file share |
| T1485 | Data Destruction (Impact) | Wiper malware / mass-delete of S3 objects |
| T1490 | Inhibit System Recovery (Impact) | Backups deleted before encryption — the "double-tap" |
| T1531 | Account Access Removal (Impact) | Attacker locks out admins by rotating the break-glass account |
| T1657 | Financial Theft (Impact) | BEC / wire fraud as the actual end goal |
