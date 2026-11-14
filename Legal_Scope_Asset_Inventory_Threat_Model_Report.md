# LEGAL SCOPE, ASSET INVENTORY & THREAT MODEL
## Authorized Security Assessment Report for RabTech Lab Training Infrastructure

**Document Reference:** SEC-REP-LAB-2026-001  
**Classification:** Confidential — Educational & Authorized Assessment Use Only  
**Prepared For:** RabTech Lab Security Review Board  
**Assessment Team:** Lead Security Assessor / Cybersecurity Educational Assessment Unit  
**Methodology:** NIST SP 800-115, PTES, OWASP WSTG v4.2, STRIDE Threat Modeling Framework  
**Engagement Date:** November 2026  
**Document Version:** 1.0 (Final Academic Release)  

---

## TABLE OF CONTENTS
1. [Executive Summary](#executive-summary)
2. [1.0 Introduction & Background](#10-introduction--background)
   - [1.1 Context and Educational Security Framework](#11-context-and-educational-security-framework)
   - [1.2 Threat Landscape Rationale](#12-threat-landscape-rationale)
   - [1.3 Methodological Standards Alignment](#13-methodological-standards-alignment)
3. [2.0 Engagement Objectives](#20-engagement-objectives)
   - [2.1 Pedagogical and Technical Objectives](#21-pedagogical-and-technical-objectives)
   - [2.2 Success Metrics and Deliverables](#22-success-metrics-and-deliverables)
4. [3.0 Written Authorization Statement (Letter of Attestation)](#30-written-authorization-statement-letter-of-attestation)
   - [3.1 Formal Grant of Authority & Consent](#31-formal-grant-of-authority--consent)
   - [3.2 Legal Boundaries & Statutory Disclaimers](#32-legal-boundaries--statutory-disclaimers)
   - [3.3 Authorization Signatories](#33-authorization-signatories)
5. [4.0 Scope Definition](#40-scope-definition)
   - [4.1 In-Scope Target Systems](#41-in-scope-target-systems)
   - [4.2 Explicit Out-of-Scope Infrastructure](#42-explicit-out-of-scope-infrastructure)
   - [4.3 Environmental Containment Safeguards](#43-environmental-containment-safeguards)
6. [5.0 Asset Inventory Table](#50-asset-inventory-table)
   - [5.1 Comprehensive Lab Asset Catalog](#51-comprehensive-lab-asset-catalog)
   - [5.2 Host, Network, and Virtualization Configurations](#52-host-network-and-virtualization-configurations)
7. [6.0 Data Classification Matrix](#60-data-classification-matrix)
   - [6.1 Information Classification Taxonomy](#61-information-classification-taxonomy)
   - [6.2 Lab Data Artifacts and Handling Controls](#62-lab-data-artifacts-and-handling-controls)
8. [7.0 Identity and Access Management (IAM) Inventory](#70-identity-and-access-management-iam-inventory)
   - [7.1 Role-Based Access Control Architecture](#71-role-based-access-control-architecture)
   - [7.2 Credential and Privilege Store](#72-credential-and-privilege-store)
9. [8.0 Trust Boundary Analysis](#80-trust-boundary-analysis)
   - [8.1 Trust Zones Demarcation](#81-trust-zones-demarcation)
   - [8.2 Inter-Zone Chokepoints and Transitions](#82-inter-zone-chokepoints-and-transitions)
10. [9.0 Data Flow Diagrams (DFD)](#90-data-flow-diagrams-dfd)
    - [9.1 Level-0 Context DFD](#91-level-0-context-dfd)
    - [9.2 Level-1 Detailed Process Flow DFD](#92-level-1-detailed-process-flow-dfd)
    - [9.3 Component-Level Data Flow Walkthrough](#93-component-level-data-flow-walkthrough)
11. [10.0 Attack Surface Analysis](#100-attack-surface-analysis)
    - [10.1 LAB-01 Web Application Surface](#101-lab-01-web-application-surface)
    - [10.2 LAB-02 Host-Only Virtual Machine Surface](#102-lab-02-host-only-virtual-machine-surface)
12. [11.0 STRIDE Threat Model](#110-stride-threat-model)
    - [11.1 Spoofing (S)](#111-spoofing-s)
    - [11.2 Tampering (T)](#112-tampering-t)
    - [11.3 Repudiation (R)](#113-repudiation-r)
    - [11.4 Information Disclosure (I)](#114-information-disclosure-i)
    - [11.5 Denial of Service (D)](#115-denial-of-service-d)
    - [11.6 Elevation of Privilege (E)](#116-elevation-of-privilege-e)
13. [12.0 Detailed Abuse Cases (2 per STRIDE Category)](#120-detailed-abuse-cases-2-per-stride-category)
14. [13.0 Risk Assessment Matrix (Likelihood × Impact)](#130-risk-assessment-matrix-likelihood--impact)
    - [13.1 Scoring Methodology and Qualitative Scales](#131-scoring-methodology-and-qualitative-scales)
    - [13.2 5×5 Matrix Mapping](#132-55-matrix-mapping)
    - [13.3 Consolidated Threat and Vulnerability Assessment Table](#133-consolidated-threat-and-vulnerability-assessment-table)
15. [14.0 Ranked Mitigation Recommendations](#140-ranked-mitigation-recommendations)
    - [14.1 Priority 1: High/Critical Mitigations](#141-priority-1-highcritical-mitigations)
    - [14.2 Priority 2: Medium Mitigations](#142-priority-2-medium-mitigations)
    - [14.3 Priority 3: Low/Hardening Mitigations](#143-priority-3-lowhardening-mitigations)
16. [15.0 Rules of Engagement (RoE)](#150-rules-of-engagement-roe)
    - [15.1 Testing Windows and Scheduling](#151-testing-windows-and-scheduling)
    - [15.2 Permitted Security Assessment Techniques](#152-permitted-security-assessment-techniques)
    - [15.3 Explicitly Prohibited Actions and Out-of-Bounds Exploits](#153-explicitly-prohibited-actions-and-out-of-bounds-exploits)
    - [15.4 Evidence Collection and Chain of Custody Protocols](#154-evidence-collection-and-chain-of-custody-protocols)
    - [15.5 Incident Escalation and Communication Pathways](#155-incident-escalation-and-communication-pathways)
    - [15.6 Safe Stopping Conditions and Circuit Breakers](#156-safe-stopping-conditions-and-circuit-breakers)
17. [16.0 Findings, Educational Reflection & Conclusions](#160-findings-educational-reflection--conclusions)
    - [16.1 Synthesis of Findings](#161-synthesis-of-findings)
    - [16.2 Academic Implications and Defensive Key Takeaways](#162-academic-implications-and-defensive-key-takeaways)
    - [16.3 Final Formal Conclusion](#163-final-formal-conclusion)
18. [Appendices](#appendices)
    - [Appendix A: Acronyms and Technical Glossary](#appendix-a-acronyms-and-technical-glossary)
    - [Appendix B: Standards Alignment Cross-Reference Matrix](#appendix-b-standards-alignment-cross-reference-matrix)

---

## EXECUTIVE SUMMARY

This document serves as the formal, authorized security assessment report, asset inventory catalog, and comprehensive STRIDE threat model for the RabTech Lab training ecosystem. Commissioned as an educational cybersecurity evaluation, this engagement was executed within a rigorously controlled, dual-target isolated laboratory consisting of a local training web application (**LAB-01**) bound exclusively to `127.0.0.1:8080`, and a deliberately vulnerable virtual machine (**LAB-02**) segregated on a private host-only virtual subnet at `192.168.56.20`.

The primary mandate of this assessment was not malicious exploitation or disruption, but rather the rigorous, academic deconstruction of system architecture, identification of trust boundary transitions, enumeration of the multi-tiered attack surface, and structured threat modeling utilizing the Microsoft STRIDE paradigm. 

Through formal threat modeling, twelve distinct abuse cases were formulated across all STRIDE threat categories. The evaluation identified key structural vulnerabilities typical of intentionally vulnerable training architectures:
1. **Application-Layer Exposures:** Insecure direct object references, cross-site scripting, and potential parameter tampering stemming from unvalidated user input processing on LAB-01.
2. **Network & Service-Layer Exposures:** Cleartext protocols, outdated local daemons, and permissive service configurations on LAB-02.
3. **Privilege Boundary Risks:** Excessive sudo privileges and SUID binary misconfigurations facilitating vertical privilege escalation on LAB-02.

Crucially, all assessment activities operated under a strict legal charter and well-defined Rules of Engagement (RoE). Defensive guardrails completely prohibited Denial of Service (DoS) testing, automated third-party cloud scanners, persistent backdoor installations, and outbound exfiltration attempts. By anchoring the assessment to the Penetration Testing Execution Standard (PTES) and NIST Special Publication 800-115, this project bridges defensive threat identification with proactive remediation engineering, offering a hardened blueprint for pedagogical enterprise computing.

---

## 1.0 INTRODUCTION & BACKGROUND

### 1.1 Context and Educational Security Framework
Modern cybersecurity education requires hands-on experiential exposure to authentic vulnerability profiles within risk-free, strictly contained computing enclaves. Theoretical understanding of security flaws—such as injection vectors, broken access controls, and protocol weaknesses—often fails to capture the intricate interdependencies between network topology, operating system configurations, and application source code. 

RabTech Lab has established a specialized training infrastructure consisting of heterogeneous systems designed to simulate modern web architectures and legacy networked server environments. To maximize pedagogical efficacy while ensuring zero collateral risk to external networks or underlying host machines, this engagement was structured as a white-box and gray-box pedagogical security assessment.

### 1.2 Threat Landscape Rationale
Enterprise environments routinely succumb to cyber attacks that exploit architectural omissions rather than zero-day vulnerabilities. Threat actors systematically map network perimeters, discover forgotten internal services, tamper with parameters, and escalate privileges along predictable vectors. By conducting a systematic threat modeling exercise on the RabTech Lab environment, students, instructors, and security engineers can systematically understand:
- How attacker personas navigate trust boundaries.
- How small misconfigurations (e.g., world-writable directories or predictable tokens) cascade into full system compromise.
- How structured threat modeling (STRIDE) enables security-by-design rather than reactive vulnerability patching.

### 1.3 Methodological Standards Alignment
This assessment and resulting documentation conform strictly to globally recognized cybersecurity frameworks:
- **NIST SP 800-115:** Technical Guide to Information Security Testing and Assessment (Target identification, threat evaluation, and vulnerability analysis).
- **PTES (Penetration Testing Execution Standard):** Pre-engagement interactions, intelligence gathering, threat modeling, vulnerability analysis, and reporting.
- **OWASP WSTG v4.2 & ASVS v4.0:** Web Security Testing Guide and Application Security Verification Standard guidelines for web-tier analysis.
- **Microsoft STRIDE Methodology:** Mnemonic-based threat categorization framework analyzing software architecture across data flows, processes, data stores, and external entities.

---

## 2.0 ENGAGEMENT OBJECTIVES

### 2.1 Pedagogical and Technical Objectives
The engagement was defined with dual objectives balancing academic learning outcomes with rigorous technical auditing:
1. **Establish Legal and Procedural Foundations:** Model real-world commercial security engagements by formalizing written authorizations, defining boundaries, and establishing non-negotiable Rules of Engagement.
2. **Comprehensive Asset Characterization:** Enumerate, catalog, and classify every hardware abstraction, virtual machine, daemon, port, and data flow within the target enclave.
3. **Data and Access Governance:** Map all information sensitivity tiers and examine identity and access management controls, auditing user permission boundaries.
4. **Deconstruct Trust Boundaries:** Visually and descriptively diagram the transit of data across logical and physical interfaces.
5. **Systematic Threat Modeling (STRIDE):** Systematically apply STRIDE to uncover vulnerabilities and architect at least two deeply articulated abuse cases per category.
6. **Risk Quantification and Remediation Prioritization:** Calculate qualitative risk scores using a $5 \times 5$ Likelihood $\times$ Impact risk matrix, outputting an actionable, phased remediation blueprint.

### 2.2 Success Metrics and Deliverables
The project deliverables comprise:
- A signed, legally binding Authorization Statement template.
- A fully populated Asset Inventory and Data Classification Matrix.
- Dual Data Flow Diagrams (ASCII and structured descriptive flow).
- A 12-factor abuse case repository spanning all STRIDE classes.
- A ranked, defense-in-depth mitigation roadmap.

---

## 3.0 WRITTEN AUTHORIZATION STATEMENT (LETTER OF ATTESTATION)

```
================================================================================
                    RABTECH LAB AUTHORIZATION TO TEST
                     FORMAL PERMISSION TO ASSESS
================================================================================

DOCUMENT REF: AUTH-2026-RABTECH-LAB-01/02
EFFECTIVE DATE: November 14, 2026
EXPIRATION DATE: November 30, 2026

1. GRANT OF AUTHORITY
RabTech Lab Directorate hereby grants authorized security assessors full, 
revocable permission to perform security audits, vulnerability scans, manual 
penetration tests, and threat modeling assessments upon the explicitly 
designated targets listed below:

   Target Designation 1: LAB-01 (Local Training Web Application)
   Binding Address: http://127.0.0.1:8080 (Loopback Interface)
   
   Target Designation 2: LAB-02 (Deliberately Vulnerable Virtual Machine)
   Binding Address: 192.168.56.20 (Host-Only Virtual Network)

2. COMPLIANCE & LEGAL SAFE HARBOR
The testing conducted under this authorization constitutes an authorized 
educational assessment. Provided that the assessors adhere strictly to the 
agreed Rules of Engagement (RoE):
   a. RabTech Lab waives any right to claim unauthorized access under the 
      Computer Fraud and Abuse Act (CFAA, 18 U.S.C. § 1030), the Computer 
      Misuse Act 1990, and applicable regional digital communications statutes.
   b. Assessors shall not be deemed in breach of lab computing policies for 
      probing or exploiting vulnerabilities contained strictly within the 
      In-Scope Assets.

3. MANDATORY OPERATIONAL CONSTRAINTS
This grant of authority is strictly conditional upon adherence to the following:
   - Prohibited from Denial-of-Service (DoS/DDoS) execution.
   - Prohibited from deploying commercial/cloud third-party scanners (e.g., 
     Qualys Cloud, Shodan, Nessus Cloud) that route data through external pipes.
   - Prohibited from establishing persistent backdoors or modifying underlying 
     hypervisor/host configurations.
   - Prohibited from initiating any network connection originating from LAB-02 
     directed outward toward the public Internet or local physical LAN.

4. AUTHORIZATION SIGNATURES

Authorized By:
_____________________________________      Date: November 14, 2026
Dr. A. Rab
Director of Information Security Research
RabTech Lab Academic Enclave

Acknowledged and Accepted By:
_____________________________________      Date: November 14, 2026
Lead Security Assessor / Student Lead
Cybersecurity Assessment & Threat Modeling Unit
================================================================================
```

### 3.1 Formal Grant of Authority & Consent
The above instrument establishes bilateral mutual agreement between RabTech Lab asset owners and the assessment team. In accordance with professional standards, no technical verification or testing activity was initiated prior to the execution and archival of this document.

### 3.2 Legal Boundaries & Statutory Disclaimers
This engagement occurred within a synthetic, sandboxed computer environment. Testing was explicitly engineered to prevent packet leakage into production networks. The assessors acknowledged that violating the boundary constraints—such as pivoting to the physical host's external network adapter—would instantly void legal immunity and terminate the engagement.

---

## 4.0 SCOPE DEFINITION

Clear scoping is the foundational pillar of ethical cybersecurity assessments. Inadvertent target sprawl can disrupt operational services, corrupt data, or trigger unintended law enforcement escalations.

```
+-----------------------------------------------------------------------------+
|                          ENGAGEMENT SCOPE SUMMARY                           |
+-----------------------------------------------------------------------------+
|  [ IN-SCOPE TARGETS ]                       [ OUT-OF-SCOPE TARGETS ]        |
|  - LAB-01: 127.0.0.1:8080                   - Host Physical OS (C:\, Host)  |
|    (Training Web App, API endpoints,          - Physical LAN (192.168.1.0/24) |
|     Application Backend & DB)                 - Default Gateway / ISP Routers |
|  - LAB-02: 192.168.56.20                    - Virtualization Hypervisor Core|
|    (Host-Only Linux VM, Local Services,       - Cloud / Third-Party Repos    |
|     Linux Kernel & File System)               - Any External Host / Domain   |
+-----------------------------------------------------------------------------+
```

### 4.1 In-Scope Target Systems
The scope of this engagement is strictly limited to the two targets defined in Table 4.1:

| Target ID | System Name | Network Identifier | Operating Environment | Allowable Testing Methodologies |
| :--- | :--- | :--- | :--- | :--- |
| **LAB-01** | Local Training Web App | `http://127.0.0.1:8080` | Localhost Loopback Interface | Manual HTTP tampering, OWASP Top 10 auditing, local source analysis, API fuzzing. |
| **LAB-02** | Deliberately Vulnerable VM | `192.168.56.20` | Host-Only Virtual Subnet (`vboxnet0`) | Port scanning, service banner grabbing, local privilege escalation, misconfiguration exploitation. |

### 4.2 Explicit Out-of-Scope Infrastructure
Any system, service, device, or network path not explicitly enumerated in Section 4.1 is **strictly Out-of-Scope**. The following entities are unequivocally protected:
1. **Physical Host Operating System:** The host workstation running Windows/macOS/Linux that hosts the virtualization software is off-limits. Attacks targeting the host file system (`C:\Windows`, `/root`), host registry, or host background services are prohibited.
2. **Virtualization Hypervisor:** Hypervisor hyper-calls, VM escape exploits (e.g., targeting VirtualBox/VMware memory allocations), and shared folder tampering with the host are forbidden.
3. **Physical Host Local Area Network (LAN):** All wireless (Wi-Fi) and wired (Ethernet) local subnets (e.g., `192.168.1.0/24`, `10.0.0.0/8`) connecting home/office workstations, printers, and IoT devices are out-of-scope.
4. **Upstream Network Infrastructure:** Physical edge routers, switches, DHCP servers, and ISP connections.
5. **Third-Party Internet Resources:** External APIs, public package repositories (NPM, PyPI, Ubuntu Archive), DNS root servers, and cloud security monitoring platforms.

### 4.3 Environmental Containment Safeguards
To enforce these boundaries technically:
- **Loopback Restriction for LAB-01:** The web server configuration is bound strictly to socket `127.0.0.1:8080` rather than `0.0.0.0:8080`, rendering it physically inaccessible to external network adapters.
- **Host-Only Adapter for LAB-02:** The hypervisor virtual network adapter is set to **Host-Only** mode without NAT port forwarding and without a bridged adapter. This creates an isolated virtual switch (`192.168.56.0/24`) with no routing table entry forwarding packets to the default gateway or public internet.

---

## 5.0 ASSET INVENTORY TABLE

### 5.1 Comprehensive Lab Asset Catalog
Table 5.1 details all functional components within the assessed ecosystem, documenting ownership, functional specifications, and environmental parameters.

| Asset Identifier | Asset Name & Category | Owner / Custodian | Host Environment & Network Placement | Primary Function & Technology Stack | Testing Authorization | Operational Constraints & Restrictions |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **LAB-01** | Local Training Web Application | RabTech Lab | Isolated Localhost (`127.0.0.1:8080`) | Multi-tier educational web app; Python/Node.js backend, SQLite/JSON datastore, HTML5/Bootstrap frontend. | **YES** | No Denial-of-Service attacks; No cloud-based scanners; No automated high-concurrency crawlers. |
| **LAB-02** | Deliberately Vulnerable Virtual Machine | RabTech Lab | Private Host-Only Subnet (`192.168.56.20` on `vboxnet0`) | Standalone Linux guest OS (Debian/Ubuntu derivative); vulnerable services (SSH, HTTP, FTP, MySQL). | **YES** | No persistence mechanisms (e.g., rootkits, immutable cronjobs); No outbound network beacons; No DoS. |
| **HOST-00** | Assessor Physical Host | Assessor / Lab Workstation | Physical Machine (`192.168.56.1` on Virtual Adapter) | Assessment platform executing local browser, curl, Burp Suite, Nmap, and hypervisor console. | **NO (Tooling Only)** | Must not target host processes, host network interfaces, or external peripherals. |
| **VSW-01** | Virtual Host-Only Switch | Hypervisor Subsystem | Software-defined virtual bridge (`192.168.56.0/24`) | Layer 2/3 virtual packet switching between Host and LAB-02 guest VM. | **NO** | No packet flooding, MAC exhaustion, or hypervisor memory manipulation. |

### 5.2 Host, Network, and Virtualization Configurations
- **LAB-01 Configuration Details:**
  - *Runtime Environment:* Node.js v18 LTS / Express.js or Python 3.10 Flask engine.
  - *Process Execution:* Runs under standard user context (`user_app`) on the local host loopback.
  - *Storage Tier:* Local flat-file SQLite database (`lab01_data.db`) located in the application backend directory.
- **LAB-02 Configuration Details:**
  - *Hypervisor Specs:* Oracle VM VirtualBox / VMware Workstation Player.
  - *Allocated Resources:* 1 vCPU, 2048 MB RAM, 20 GB dynamically allocated virtual disk.
  - *Network Adapter 1:* Host-Only Adapter (`VirtualBox Host-Only Ethernet Adapter`), MAC `08:00:27:AB:CD:20`, IP `192.168.56.20/24`, Default Gateway: None (Non-routable).
  - *Listening Daemons:* OpenSSH 7.2p2 (Port 22), Apache 2.4.18 (Port 80), ProFTPD 1.3.5 (Port 21), MySQL 5.7 (Port 3306).

---

## 6.0 DATA CLASSIFICATION MATRIX

### 6.1 Information Classification Taxonomy
To evaluate information disclosure threats accurately, the lab establishes a four-tier data classification model aligned with enterprise information security governance:
- **Public (Tier 1):** Unrestricted information intended for general consumption (e.g., training manuals, public login pages).
- **Internal (Tier 2):** Non-sensitive operational data intended for internal lab users (e.g., system banners, software release version strings).
- **Confidential (Tier 3):** Sensitive lab information requiring authorization (e.g., test user profiles, session identifiers, non-privileged student accounts).
- **Restricted / High Risk (Tier 4):** Highly sensitive administrative artifacts whose compromise represents total system loss (e.g., root credentials, private cryptographic keys, assessment audit logs, shadow password files).

### 6.2 Lab Data Artifacts and Handling Controls
Table 6.2 maps all data types resident within the target environment against this taxonomy:

| Data Asset Description | Resident System / Location | Sensitivity Classification | Integrity Requirement | Availability Requirement | Confidentiality Controls & Protection Guidelines |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Source Code & Templates** | LAB-01 (`/frontend`, `/backend`) | **Internal (Tier 2)** | Moderate | Low | Access restricted to host filesystem; no external code repository publishing. |
| **Application SQLite Database** | LAB-01 (`/database/lab01.db`) | **Confidential (Tier 3)** | High | Moderate | Synthetic data only; contains simulated student emails, hashed passwords, and training records. |
| **Session Cookies / Tokens** | LAB-01 (HTTP Headers & Memory) | **Confidential (Tier 3)** | High | Moderate | Ephemeral in-memory tokens; must be flagged `HttpOnly` and `SameSite` in target configurations. |
| **System Shadow Password File** | LAB-02 (`/etc/shadow`) | **Restricted (Tier 4)** | Critical | High | Readable only by root (`UID 0`); contains simulated password hashes for lab user personas. |
| **SSH Host Private Keys** | LAB-02 (`/etc/ssh/ssh_host_*_key`) | **Restricted (Tier 4)** | Critical | High | Strictly restricted permissions (`chmod 600`); ensures cryptographic identity of target VM. |
| **System Event & Audit Logs** | LAB-01 & LAB-02 (`/var/log/*`) | **Confidential (Tier 3)** | Critical | High | Append-only permissions; must record assessor IP, timestamps, and command execution. |
| **Assessment Notes & Captures** | Assessor Host (`/reports`) | **Confidential (Tier 3)** | High | High | Stored in encrypted directories; must not be published to unauthenticated repositories. |

---

## 7.0 IDENTITY AND ACCESS MANAGEMENT (IAM) INVENTORY

### 7.1 Role-Based Access Control Architecture
Identity and access governance across the lab targets reflects a segregated model distinguishing administrative supervisors, standard student/trainee personas, and autonomous background system daemons.

```
       [ Lab Administrator (Root/Admin) ]  <-- Full System / Kernel Control
                       |
       [ Faculty / Instructor Persona ]    <-- Lab Configuration & Grading
                       |
       [ Student / Auditor Persona ]       <-- In-Scope Application User
                       |
       [ Anonymous / External Visitor ]    <-- Unauthenticated Entry Point
```

### 7.2 Credential and Privilege Store
Table 7.2 outlines the identity profiles configured across LAB-01 and LAB-02:

| Principal / Identity | System / Realm | Privilege Level / Group Membership | Authentication Mechanism | Operational Role in Lab Assessment |
| :--- | :--- | :--- | :--- | :--- |
| `anonymous` | LAB-01 (Web) | None (Public/Guest) | None (Unauthenticated) | Initial attacker persona; tests registration, public routes, and input sanitization. |
| `trainee_user` | LAB-01 (Web) | Standard Application User | Username + Password (`trainee2026!`) | Standard authenticated persona; tests horizontal privilege escalation and IDOR. |
| `lab_admin` | LAB-01 (Web) | Portal Superuser | Form-based Login (`AdminPass987#`) | Target of vertical privilege escalation and session spoofing evaluations. |
| `ftpuser` | LAB-02 (OS/FTP) | Limited Shell (`/bin/sh`), Group `ftp` | Cleartext FTP Password (`ftpstudent`) | Evaluated for credential sniffing and service exploit vectors. |
| `student` | LAB-02 (Linux OS) | Standard Interactive User (`UID 1001`) | SSH Public Key or Password (`studentpass`) | Primary low-privilege initial shell persona for privilege escalation audits. |
| `www-data` | LAB-02 (Web Daemon) | Service Account (`UID 33`, `/bin/false`) | None (Daemon spawned by Apache) | Evaluated for web shell execution and restricted file system permissions. |
| `root` | LAB-02 (Linux OS) | Superuser / Kernel Master (`UID 0`) | Password (Restricted / Shadow hashed) | Ultimate target of local privilege escalation (LPE) analysis. |

---

## 8.0 TRUST BOUNDARY ANALYSIS

A trust boundary is any interface or architectural boundary where data or execution control transitions from one trust level to another. Vulnerabilities almost universally arise at trust boundary crossing points where sanitization, authentication, or authorization checks fail.

```
+------------------------------------------------------------------------------------+
|                               TRUST ZONES OVERVIEW                                 |
+------------------------------------------------------------------------------------+
|  [ TRUST ZONE 0: Untrusted / Assessor Execution Environment ]                     |
|  - Assessor Workstation, Penetration Testing Tools, Browser UI                     |
|  - Trust Level: Zero Trust (Untrusted Origin)                                      |
+------------------------------------------+-----------------------------------------+
                                           |
                    (Boundary 1: Loopback) | (Boundary 2: Virtual Switch)
                                           v
+------------------------------------------+-----------------------------------------+
|  [ TRUST ZONE 1: LAB-01 Execution Zone ] |  [ TRUST ZONE 2: LAB-02 Execution Zone ]|
|  - Host Loopback (127.0.0.1:8080)        |  - Host-Only Subnet (192.168.56.20)     |
|  - Express/Flask Web Engine              |  - Apache, OpenSSH, ProFTPD             |
|  - SQLite Datastore                      |  - Linux Kernel Space & Filesystem      |
|  - Trust Level: Semi-Trusted Training    |  - Trust Level: Deliberately Vulnerable |
+------------------------------------------+-----------------------------------------+
                                           |
                               (Boundary 3: Kernel Ring 0)
                                           v
+------------------------------------------------------------------------------------+
|  [ TRUST ZONE 3: Operating System Kernel & Root Space (LAB-02) ]                   |
|  - Memory Pages, Kernel Space, Hardware Emulation, Root Shell                      |
|  - Trust Level: Critical / Sovereign Core                                          |
+------------------------------------------------------------------------------------+
```

### 8.1 Trust Zones Demarcation
1. **Trust Zone 0 (Assessor Workspace / Tooling Context):** Represents the test harness where the assessor executes requests. Data originating from this zone must be treated by targets as completely untrusted, potentially hostile payload streams.
2. **Trust Zone 1 (LAB-01 Application Process Boundary):** Comprises the web runtime process, HTTP parsing engines, application business logic, and local database file handles. 
3. **Trust Zone 2 (LAB-02 Virtual Network & User-Space Boundary):** Comprises the virtual network stack, listening network service daemons (Apache, OpenSSH), and non-privileged user-space processes running under unprivileged UIDs.
4. **Trust Zone 3 (LAB-02 Privileged Kernel Core):** Comprises kernel memory, device drivers, raw filesystem devices (`/dev/sda*`), and processes running under `UID 0` (`root`).

### 8.2 Inter-Zone Chokepoints and Transitions
- **Trust Boundary 1 (Zone 0 $\rightarrow$ Zone 1 - Loopback HTTP Interface):** All incoming HTTP requests crossing `127.0.0.1:8080` must be treated as untrusted. Vulnerabilities occur if the application parser fails to sanitize headers, query parameters, or POST bodies prior to passing them to backend SQL queries or command execution APIs.
- **Trust Boundary 2 (Zone 0 $\rightarrow$ Zone 2 - Virtual Ethernet Interface):** Network frames passing over `vboxnet0` into `eth0` of LAB-02 must transition through the Linux network stack and service daemon parsers. Unauthenticated service endpoints represent primary entry vectors.
- **Trust Boundary 3 (Zone 2 $\rightarrow$ Zone 3 - System Call & SUID Boundary):** User-space programs executing system calls (`syscall`), interacting with setuid root binaries (`/bin/su`, custom SUID scripts), or leveraging `sudo` transitions cross this critical boundary. Any vulnerability here allows complete takeover of LAB-02.

---

## 9.0 DATA FLOW DIAGRAMS (DFD)

### 9.1 Level-0 Context DFD
The Level-0 Context Diagram illustrates the macro-level relationships between the external assessor entity and the two primary security boundaries.

```
+---------------------------------------------------------------------------------------+
|                              LEVEL-0 CONTEXT DIAGRAM                                  |
+---------------------------------------------------------------------------------------+

                        +--------------------------+
                        |                          |
                        |   Authorized Assessor    |
                        |   (Interactive Tester)   |
                        |                          |
                        +------------+-------------+
                                     |
               +---------------------+---------------------+
               | HTTP Requests /     |                     | TCP Packets /
               | Test Payloads       |                     | Raw Network Probes
               v                     |                     v
    +----------------------+         |          +----------------------+
    |                      |         |          |                      |
    |        LAB-01        |         |          |        LAB-02        |
    |  Local Training App  |         |          |   Vulnerable Linux   |
    |  (127.0.0.1:8080)    |         |          |   VM (192.168.56.20) |
    |                      |         |          |                      |
    +----------+-----------+         |          +----------+-----------+
               |                     |                     |
               | HTTP Responses /    |                     | Banner Returns /
               | HTML / JSON         |                     | Protocol Responses
               +---------------------+---------------------+
```

### 9.2 Level-1 Detailed Process Flow DFD
The Level-1 Data Flow Diagram breaks down the internal processes, data stores, and trust boundary crossings.

```
+---------------------------------------------------------------------------------------------------+
|                                 LEVEL-1 DETAILED DATA FLOW DIAGRAM                                |
+---------------------------------------------------------------------------------------------------+

 [ EXTERNAL ENTITY: Assessor Browser / Security Tools ]
          |
          |  [Data Flow 1: HTTP Request / Auth Tokens / Form Submissions]
          v
============================= TRUST BOUNDARY 1: Loopback HTTP =====================================
          |
          v
   (Process 1.0: Web Request Routing & Header Parser) <-----> [Data Store D1: Session Cache]
          |
          |  [Data Flow 2: Sanitized / Unsanitized Parameters]
          v
   (Process 2.0: Business Logic & Access Control Engine)
          |
          |  [Data Flow 3: Parameterized or Concatenated Queries]
          v
   (Process 3.0: Database Query Execution) <----------------> [Data Store D2: lab01_data.db]
          |
          |  [Data Flow 4: Record Sets / User Profiles]
          v
   (Process 4.0: Response Serialization & View Renderer)
          |
          |  [Data Flow 5: HTTP Response HTML/JSON]
          v
 [ EXTERNAL ENTITY: Assessor Browser ]

-----------------------------------------------------------------------------------------------------

 [ EXTERNAL ENTITY: Assessor Terminal / Port Scanner / Exploit Framework ]
          |
          |  [Data Flow 6: SYN Packets / Application Commands]
          v
============================= TRUST BOUNDARY 2: Virtual Network (Host-Only) ========================
          |
          v
   (Process 5.0: Network Daemon Listener: Apache/SSH/FTP)
          |
          |  [Data Flow 7: Daemon Child Fork / Process Execution]
          v
   (Process 6.0: Linux User-Space Shell / Command Parser) <-> [Data Store D3: Local Filesystem]
          |
          |  [Data Flow 8: Sudo Execution / SUID Binaries]
          v
============================= TRUST BOUNDARY 3: Kernel System Call (Ring 0) ========================
          |
          v
   (Process 7.0: Linux Kernel System Call Dispatcher) <-----> [Data Store D4: /etc/shadow & Disk]
```

### 9.3 Component-Level Data Flow Walkthrough
1. **Flow 1 & 2 (Web Layer Transit):** The assessor submits an HTTP request to `http://127.0.0.1:8080`. Process 1.0 unpacks HTTP headers and passes parameters to Process 2.0. If input validation is omitted, malicious payloads (e.g., SQL syntax or script tags) enter internal application state.
2. **Flow 3 & 4 (Database Layer Transit):** Process 2.0 constructs a database query. Data is retrieved from Datastore D1 (SQLite) and returned to the serialization engine. Unsafe string concatenation creates an immediate injection vulnerability.
3. **Flow 6 & 7 (Service Layer Transit):** Assessor initiates an SSH or FTP connection to `192.168.56.20`. Process 5.0 authenticates credentials against `/etc/passwd`. Upon authentication, a shell process (Process 6.0) is spawned with standard user permissions.
4. **Flow 8 (Privilege Escalation Transit):** An unprivileged process attempts to execute a binary carrying the SUID flag or invokes `sudo`. The call transitions across Trust Boundary 3 into Process 7.0 (Kernel Ring 0). Improper configuration allows unprivileged users to execute commands with root privileges.

---

## 10.0 ATTACK SURFACE ANALYSIS

### 10.1 LAB-01 Web Application Surface
LAB-01 is exposed via standard HTTP on loopback port 8080. Its attack surface comprises three primary tiers:

```
+-----------------------------------------------------------------------------+
|                        LAB-01 ATTACK SURFACE TIERS                          |
+-----------------------------------------------------------------------------+
| 1. HTTP Entry Endpoints:                                                    |
|    - GET /login, POST /api/login, GET /dashboard, GET /profile?id=          |
|    - POST /feedback, POST /uploads/avatar, GET /debug/status                |
| 2. Input Handling Vectors:                                                  |
|    - URL Query strings, JSON-encoded POST bodies, Multipart form uploads    |
|    - HTTP Cookie headers (session_id), HTTP Referer and User-Agent headers  |
| 3. Storage & State Interfaces:                                              |
|    - Local SQLite database queries (SQLi surface)                           |
|    - Server-side template rendering engines (SSTI surface)                  |
|    - Local file system inclusion/traversal interfaces (/files?file=)        |
+-----------------------------------------------------------------------------+
```

### 10.2 LAB-02 Host-Only Virtual Machine Surface
LAB-02 exposes an attack surface distributed across the TCP/IP stack and local operating system internals:

```
+-----------------------------------------------------------------------------+
|                        LAB-02 ATTACK SURFACE TIERS                          |
+-----------------------------------------------------------------------------+
| 1. Network Listener Ports (Host-Only Network 192.168.56.20):                |
|    - TCP 21: ProFTPD 1.3.5 (FTP command channel, mod_copy vector)          |
|    - TCP 22: OpenSSH 7.2p2 (Authentication banner, brute-force surface)     |
|    - TCP 80: Apache 2.4.18 (Web server, CGI scripts, directory indexes)     |
|    - TCP 3306: MySQL 5.7 (Database listener, remote root access checks)    |
| 2. Operating System User-Space:                                             |
|    - World-writable scripts in /var/www, /tmp, and /dev/shm                 |
|    - SUID/SGID binaries (/usr/bin/find, /usr/bin/pkexec, custom lab scripts)|
|    - Sudoers rules (/etc/sudoers NOPASSWD entries)                          |
| 3. Kernel & File System Layer:                                              |
|    - Outdated Linux kernel versions vulnerable to privilege escalation      |
|    - Unquoted service paths and unencrypted cronjobs executing as root      |
+-----------------------------------------------------------------------------+
```

---

## 11.0 STRIDE THREAT MODEL

The Microsoft STRIDE model classifies software vulnerabilities into six distinct categories: **S**poofing, **T**ampering, **R**epudiation, **I**nformation Disclosure, **D**enial of Service, and **E**levation of Privilege.

```
+------------------------------------------------------------------------------------+
|                         STRIDE THREAT MAPPING MATRIX                               |
+-------------------+---------------------------+------------------------------------+
| STRIDE Category   | Security Property Violated| Primary System Target Impacted     |
+-------------------+---------------------------+------------------------------------+
| Spoofing (S)      | Authenticity              | LAB-01 Session Tokens, LAB-02 SSH  |
| Tampering (T)     | Integrity                 | LAB-01 Database, LAB-02 Configs    |
| Repudiation (R)   | Non-repudiation           | LAB-01 Logs, LAB-02 Audit Records  |
| Info Disclosure (I)| Confidentiality          | LAB-01 Profiles, LAB-02 /etc/shadow|
| Denial of Svc (D) | Availability              | LAB-01 Loopback, LAB-02 RAM/CPU    |
| Elev. of Priv (E) | Authorization             | LAB-01 Admin IDOR, LAB-02 SUID/Root|
+-------------------+---------------------------+------------------------------------+
```

### 11.1 Spoofing (S)
Threat actors masquerade as valid users, systems, or processes by faking identity artifacts. In LAB-01, spoofing manifests via predictable session tokens or unauthenticated header spoofing. In LAB-02, it manifests through ARP spoofing or forged service authentication.

### 11.2 Tampering (T)
Unauthorized modification of data in transit, data at rest, or execution logic. On LAB-01, tampering involves altering hidden form fields, URL parameters, or performing SQL injection to modify database records. On LAB-02, tampering targets system configuration files (`/etc/passwd`, web root files).

### 11.3 Repudiation (R)
The ability of an actor to perform an unauthorized action without the system being able to prove who executed it. In both targets, inadequate audit logging, missing client IP verification, or unprivileged log modification allows attackers to deny malicious activity.

### 11.4 Information Disclosure (I)
The unauthorized exposure of confidential data to entities lacking clearance. LAB-01 risks exposing personal database records via SQL injection or verbose error messages. LAB-02 risks exposing password hashes, kernel memory dumps, or network packet data.

### 11.5 Denial of Service (D)
Disrupting authorized access to computing resources. Although DoS attacks are strictly prohibited from active execution during this assessment, threat modeling mandates analyzing architectural failure modes (e.g., regex algorithmic complexity, unbounded file uploads, and kernel resource exhaustion).

### 11.6 Elevation of Privilege (E)
An adversary with limited privileges gaining unauthorized higher-tier permissions. In LAB-01, this involves horizontal or vertical IDOR to reach administrative portals. In LAB-02, it encompasses exploiting SUID binaries or sudo misconfigurations to gain root access.

---

## 12.0 DETAILED ABUSE CASES (2 PER STRIDE CATEGORY)

To ensure comprehensive vulnerability coverage, exactly two detailed abuse cases have been structured for each STRIDE category (12 total), outlining actor motivations, preconditions, execution sequences, technical impacts, and precise mitigations.

---

### ABUSE CASE 01: Spoofing Identity (LAB-01)
- **Abuse Case ID:** `AC-S01`
- **Threat Category:** Spoofing (Authenticity Violation)
- **Target Asset:** LAB-01 Local Training Web Application (`http://127.0.0.1:8080`)
- **Threat Actor Persona:** Unauthenticated External Assessor / Untrusted Guest
- **Preconditions:** LAB-01 utilizes sequential, unencrypted, or weakly signed session cookies (e.g., `Cookie: session_id=1004`).
- **Attack Vector & Execution Sequence:**
  1. The assessor registers a test account (`trainee_user`) and observes the assigned cookie: `session_id=1001`.
  2. The assessor registers a second test account and receives `session_id=1002`.
  3. Deducing linear sequential incrementation, the assessor crafts an HTTP GET request to `/dashboard` replacing the cookie header with `session_id=1000` (the default administrative account).
  4. The application validates the cookie without cryptographic signature verification.
- **Technical Impact:** Complete identity impersonation of the lab administrator; unauthorized access to administrative features without credential possession.
- **Specific Mitigation:** Implement cryptographically secure, unpredictable session identifiers generated by a CSPRNG (e.g., 128-bit random tokens) and signed using HMAC-SHA256 with a secret server-side key.

---

### ABUSE CASE 02: Network Identity Spoofing (LAB-02)
- **Abuse Case ID:** `AC-S02`
- **Threat Category:** Spoofing (Authenticity Violation)
- **Target Asset:** LAB-02 Deliberately Vulnerable VM (`192.168.56.20`)
- **Threat Actor Persona:** Local Network Assessor on Host-Only Subnet (`192.168.56.1`)
- **Preconditions:** Unencrypted protocols (FTP, HTTP) active on LAB-02; absence of static ARP bindings.
- **Attack Vector & Execution Sequence:**
  1. Assessor initiates an ARP request across the virtual bridge `192.168.56.0/24`.
  2. Assessor generates gratuitous ARP replies associating the default interface with the assessor's MAC address.
  3. Client sessions connecting to LAB-02 FTP or HTTP daemons route packets through the assessor's interception proxy.
- **Technical Impact:** Interception of cleartext credentials; ability to masquerade as the legitimate host-only gateway or target server.
- **Specific Mitigation:** Enforce TLS encryption across all listening services (FTPS/HTTPS/SSH); configure static ARP entries and enable DHCP snooping/dynamic ARP inspection where supported.

---

### ABUSE CASE 03: Parameter Tampering & SQL Injection (LAB-01)
- **Abuse Case ID:** `AC-T01`
- **Threat Category:** Tampering (Integrity Violation)
- **Target Asset:** LAB-01 Local Training Web Application (`http://127.0.0.1:8080`)
- **Threat Actor Persona:** Authenticated Low-Privilege Trainee
- **Preconditions:** User input in the student profile query endpoint (`/profile?id=`) is concatenated directly into SQL execution strings.
- **Attack Vector & Execution Sequence:**
  1. Assessor navigates to the profile viewing tab and intercepts the request: `GET /profile?id=5 HTTP/1.1`.
  2. Assessor injects a SQL payload into the parameter: `GET /profile?id=5; UPDATE users SET role='admin' WHERE id=5;--`.
  3. The SQLite database engine executes the multi-statement payload, altering the underlying database records.
- **Technical Impact:** Direct compromise of database integrity; unauthorized role modification; persistent database record corruption.
- **Specific Mitigation:** Utilize parameterized queries / prepared statements with typed binding (e.g., using Sequelize/TypeORM or parameterized SQLite drivers); enforce strict input type validation rejecting non-integer characters.

---

### ABUSE CASE 04: System Configuration File Tampering (LAB-02)
- **Abuse Case ID:** `AC-T02`
- **Threat Category:** Tampering (Integrity Violation)
- **Target Asset:** LAB-02 Deliberately Vulnerable VM (`192.168.56.20`)
- **Threat Actor Persona:** Low-Privilege Shell User (`student`)
- **Preconditions:** Excessive file permissions configured on system initialization files (e.g., `/etc/crontab` or `/etc/rc.local` is world-writable: `chmod 777`).
- **Attack Vector & Execution Sequence:**
  1. Assessor obtains low-privilege interactive access as user `student`.
  2. Assessor inspects file permissions: `ls -la /etc/crontab` revealing `-rwxrwxrwx 1 root root`.
  3. Assessor appends a malicious command string: `echo "* * * * * root cp /bin/bash /tmp/rootbash; chmod +s /tmp/rootbash" >> /etc/crontab`.
  4. The cron daemon executes the modified file during the next scheduled cycle.
- **Technical Impact:** Permanent integrity compromise of operating system configuration; unauthorized injection of malicious instructions executing under root authority.
- **Specific Mitigation:** Re-establish strict POSIX permissions on all sensitive configuration files (`chmod 644 /etc/crontab`, owned by `root:root`); deploy file integrity monitoring (`AIDE` or `Tripwire`).

---

### ABUSE CASE 05: Log Disablement & Non-Attributable Requests (LAB-01)
- **Abuse Case ID:** `AC-R01`
- **Threat Category:** Repudiation (Non-Repudiation Violation)
- **Target Asset:** LAB-01 Local Training Web Application (`http://127.0.0.1:8080`)
- **Threat Actor Persona:** Authenticated Malicious Trainee
- **Preconditions:** The application logs actions using client-supplied headers without server-side timestamping or stores logs in an unauthenticated web directory.
- **Attack Vector & Execution Sequence:**
  1. Assessor executes a malicious profile alteration while forging client IP headers: `X-Forwarded-For: 10.254.254.254`.
  2. The application records the activity against the spoofed IP rather than the true socket connection (`127.0.0.1`).
  3. Assessor accesses an insecure log cleanup endpoint (`POST /admin/clear-logs`) that lacks CSRF tokens and access controls, deleting the transaction history.
- **Technical Impact:** Elimination of audit trails; inability to attribute security events or unauthorized modifications to a specific user account.
- **Specific Mitigation:** Enforce immutable, append-only logging; record true TCP socket connection metadata; forward audit logs to an external syslog server; implement strict access controls on log maintenance functions.

---

### ABUSE CASE 06: Process Action Repudiation via Shared Daemon (LAB-02)
- **Abuse Case ID:** `AC-R02`
- **Threat Category:** Repudiation (Non-Repudiation Violation)
- **Target Asset:** LAB-02 Deliberately Vulnerable VM (`192.168.56.20`)
- **Threat Actor Persona:** Anonymous Network Actor exploiting Service Daemons
- **Preconditions:** ProFTPD or Apache runs without detailed session accounting; auditd is disabled; multiple users share the generic `ftpuser` or `student` account.
- **Attack Vector & Execution Sequence:**
  1. Assessor logs in using shared credentials (`student` / `studentpass`).
  2. Assessor edits sensitive lab assignment files in `/var/lab/`.
  3. Assessor manually clears their interactive bash history (`history -c; unset HISTFILE`).
  4. System logs reflect only generic `student` logins without source MAC/IP binding or command-line auditing.
- **Technical Impact:** System administrators cannot prove which student or assessor executed unauthorized file modifications, nullifying non-repudiation.
- **Specific Mitigation:** Eliminate shared credentials; assign unique PKI-based SSH identities to each user; configure Linux `auditd` to capture system-level command execution (`-a always,exit -F arch=b64 -S execve`).

---

### ABUSE CASE 07: Sensitive Information Leakage via Path Traversal (LAB-01)
- **Abuse Case ID:** `AC-I01`
- **Threat Category:** Information Disclosure (Confidentiality Violation)
- **Target Asset:** LAB-01 Local Training Web Application (`http://127.0.0.1:8080`)
- **Threat Actor Persona:** Unauthenticated External Assessor
- **Preconditions:** LAB-01 implements a file-viewing utility (`/view?file=doc1.txt`) that concatenates user input directly into file open calls without canonicalization.
- **Attack Vector & Execution Sequence:**
  1. Assessor intercepts the file retrieval request.
  2. Assessor submits dot-dot-slash sequence payloads: `GET /view?file=../../../../etc/passwd HTTP/1.1` (or local Windows equivalent: `..\..\..\Windows\win.ini`).
  3. The backend file reader opens the relative path outside the designated web root and returns the target system file in the HTTP response body.
- **Technical Impact:** Disclosure of sensitive operating system files, local configuration secrets, and database connection strings to unauthorized actors.
- **Specific Mitigation:** Sanitize and whitelist allowable filenames; implement path canonicalization using path normalization libraries; verify that the resolved canonical path remains within the designated directory boundary.

---

### ABUSE CASE 08: Memory Scraping & Cleartext Protocol Sniffing (LAB-02)
- **Abuse Case ID:** `AC-I02`
- **Threat Category:** Information Disclosure (Confidentiality Violation)
- **Target Asset:** LAB-02 Deliberately Vulnerable VM (`192.168.56.20`)
- **Threat Actor Persona:** Assessor Positioned on Host-Only Network
- **Preconditions:** ProFTPD and HTTP services operate without transport layer security; weak file permissions on system process files.
- **Attack Vector & Execution Sequence:**
  1. Assessor initiates network packet capture on virtual interface `vboxnet0` using Wireshark/tcpdump.
  2. A simulated lab user initiates an FTP login session transmitting `USER ftpuser` and `PASS ftpstudent` in plaintext.
  3. Assessor extracts plaintext credentials directly from the captured TCP payload.
  4. Simultaneously, assessor reads `/proc/kcore` or world-readable process memory structures from an unprivileged shell to harvest secrets.
- **Technical Impact:** Direct exposure of administrative and user credentials, confidential network communications, and system memory contents.
- **Specific Mitigation:** Decommission unencrypted legacy protocols; enforce TLS 1.3 across all communication services; enforce `hidepid=2` mount options on `/proc` to prevent inter-process snooping.

---

### ABUSE CASE 09: Resource Starvation via Algorithmic Complexity (LAB-01)
- **Abuse Case ID:** `AC-D01`
- **Threat Category:** Denial of Service (Availability Violation)
- **Target Asset:** LAB-01 Local Training Web Application (`http://127.0.0.1:8080`)
- **Threat Actor Persona:** Malicious Web Client
- **Preconditions:** LAB-01 input validation routines utilize poorly structured regular expressions (Catastrophic Backtracking / ReDoS) or unbounded file processing.
- **Attack Vector & Execution Sequence:**
  1. Assessor analyzes the application's email or regex validation field on the registration form.
  2. The input parser uses an expression such as `^([a-zA-Z0-9]+)*$`.
  3. A crafted string of 30 repetitive alphanumeric characters followed by an exclamation mark is submitted: `aaaaaaaaaaaaaaaaaaaaaaaaaaaaaa!`.
  4. The regex engine enters catastrophic backtracking, consuming 100% of the single-threaded Node.js/Python event loop CPU capacity.
- **Technical Impact:** Server CPU saturation; complete unresponsiveness to legitimate training requests; denial of service across the entire loopback listener.
- **Specific Mitigation:** Deploy non-backtracking regular expression engines (e.g., Google RE2); implement strict input length constraints; enforce request timeout middlewares.

---

### ABUSE CASE 10: Daemon Crash via Kernel Memory / Fork Exhaustion (LAB-02)
- **Abuse Case ID:** `AC-D02`
- **Threat Category:** Denial of Service (Availability Violation)
- **Target Asset:** LAB-02 Deliberately Vulnerable VM (`192.168.56.20`)
- **Threat Actor Persona:** Unprivileged Shell User (`student`)
- **Preconditions:** Inadequate process and resource limits (`ulimit`) configured for non-root users in `/etc/security/limits.conf`.
- **Attack Vector & Execution Sequence:**
  1. Assessor executes a local shell on LAB-02.
  2. Assessor launches an unconstrained process recursion (e.g., standard educational shell fork sequence: `:(){ :|:& };:`).
  3. The Linux process table quickly exhausts all available PID slots (e.g., 32,768 processes).
  4. The operating system kernel freezes, panics, or locks out administrative logins via console and SSH.
- **Technical Impact:** Total operating system collapse; host-only VM requires hard hypervisor reset; data loss in volatile memory buffers.
- **Specific Mitigation:** Configure robust POSIX resource limits in `/etc/security/limits.conf` (e.g., restricting standard users to a maximum of 100 concurrent processes: `student hard nproc 100`); enable systemd cgroup process throttling.

---

### ABUSE CASE 11: Broken Object-Level Authorization / IDOR (LAB-01)
- **Abuse Case ID:** `AC-E01`
- **Threat Category:** Elevation of Privilege (Authorization Violation)
- **Target Asset:** LAB-01 Local Training Web Application (`http://127.0.0.1:8080`)
- **Threat Actor Persona:** Authenticated Low-Privilege Trainee (`trainee_user`)
- **Preconditions:** LAB-01 uses numeric identifier parameters to govern record access without validating session role ownership.
- **Attack Vector & Execution Sequence:**
  1. Assessor logs in as `trainee_user` (Account ID: `1005`).
  2. Assessor requests profile modification: `POST /api/user/update` with payload `{"id": 1005, "email": "trainee@lab.local"}`.
  3. Assessor alters the payload: `{"id": 1, "email": "pwned@lab.local", "role": "superadmin"}`.
  4. The backend controller processes the update without confirming whether the active session owns record ID 1.
- **Technical Impact:** Vertical privilege escalation from standard student to superadmin; arbitrary takeover of administrative accounts.
- **Specific Mitigation:** Implement robust server-side authorization checks verifying that the authenticated session identity strictly owns the targeted entity; replace sequential IDs with non-enumerable UUIDv4 values.

---

### ABUSE CASE 12: Local Privilege Escalation via SUID Binary Misconfiguration (LAB-02)
- **Abuse Case ID:** `AC-E02`
- **Threat Category:** Elevation of Privilege (Authorization Violation)
- **Target Asset:** LAB-02 Deliberately Vulnerable VM (`192.168.56.20`)
- **Threat Actor Persona:** Low-Privilege Shell User (`student`)
- **Preconditions:** The `find` utility or a custom Python script on LAB-02 has the SUID permission bit set and is owned by `root`: `-rwsr-xr-x 1 root root /usr/bin/find`.
- **Attack Vector & Execution Sequence:**
  1. Assessor enumerates SUID binaries: `find / -perm -u=s -type f 2>/dev/null`.
  2. Assessor discovers `/usr/bin/find` configured with root SUID permissions.
  3. Assessor executes the built-in command execution flag: `/usr/bin/find . -exec /bin/sh -p \; -quit`.
  4. The shell spawns with Effective User ID 0 (`euid=0(root)`).
- **Technical Impact:** Complete compromise of LAB-02; elevation to `root` authority; full control over all files, processes, and network configurations on the virtual machine.
- **Specific Mitigation:** Audit all SUID/SGID binaries using automated configuration checkers; strip unnecessary SUID bits (`chmod u-s /usr/bin/find`); mount user-writable partitions (`/tmp`, `/dev/shm`) with the `nosuid` flag.

---

## 13.0 RISK ASSESSMENT MATRIX (LIKELIHOOD × IMPACT)

### 13.1 Scoring Methodology and Qualitative Scales
Risk evaluation follows the standard qualitative risk assessment framework adapted from NIST SP 800-30 Rev. 1 and OWASP Risk Rating Methodology. Overall risk is calculated as the mathematical product of **Likelihood** and **Impact**:

$$\text{Risk Level} = \text{Likelihood} \times \text{Impact}$$

#### Likelihood Scale (1 to 5)
- **1 - Rare:** Highly complex attack vector requiring extensive internal knowledge, advanced tooling, and rare timing.
- **2 - Unlikely:** Technically feasible but requires non-standard conditions and moderate skill.
- **3 - Moderate:** Common vulnerability vector; automated tools or standard exploit scripts readily available.
- **4 - Likely:** Easy to exploit; requires minimal technical skill; widely documented misconfiguration.
- **5 - Almost Certain:** Completely unauthenticated, trivially discoverable, and immediately accessible via basic requests.

#### Impact Scale (1 to 5)
- **1 - Negligible:** Informational disclosure; zero operational disruption; no privilege compromise.
- **2 - Minor:** Minor data disclosure; localized configuration impact; non-sensitive system metadata exposed.
- **3 - Moderate:** Partial loss of integrity or confidentiality; standard user account compromise; localized service degradation.
- **4 - Major:** Sensitive data compromise (Tier 3/4); full user compromise or horizontal privilege escalation across multiple accounts.
- **5 - Catastrophic:** Complete compromise of root/administrator authority; arbitrary code execution; complete loss of data confidentiality, integrity, and availability.

### 13.2 5×5 Matrix Mapping

```
+-----------------------------------------------------------------------------------+
|                        5x5 RISK QUALITATIVE MATRIX                                |
+---------------+-------------------------------------------------------------------+
|               |                             IMPACT                                |
|  LIKELIHOOD   |  1: Negligible  2: Minor      3: Moderate   4: Major   5: Catastrophic|
+---------------+-------------------------------------------------------------------+
| 5: Almost Cert|  Medium (5)     High (10)     High (15)     Crit (20)  Crit (25)      |
| 4: Likely     |  Low (4)        Medium (8)    High (12)     High (16)  Crit (20)      |
| 3: Moderate   |  Low (3)        Medium (6)    Medium (9)    High (12)  High (15)      |
| 2: Unlikely   |  Low (2)        Low (4)       Medium (6)    Medium (8) High (10)      |
| 1: Rare       |  Low (1)        Low (2)       Low (3)       Low (4)    Medium (5)     |
+---------------+-------------------------------------------------------------------+
```

- **Critical (20–25):** Immediate remediation required; fundamental architectural flaw resulting in total system compromise.
- **High (10–16):** Severe risk; straightforward exploitation leading to substantial unauthorized access.
- **Medium (5–9):** Moderate risk; requires specific conditions or causes limited damage.
- **Low (1–4):** Minimal risk; informational or defense-in-depth improvement.

### 13.3 Consolidated Threat and Vulnerability Assessment Table
Table 13.3 maps all twelve analyzed abuse cases against the risk framework, ranking them by qualitative score:

| Case ID | Threat Category | Target | Description of Threat Scenario | Likelihood (1–5) | Impact (1–5) | Risk Score ($L \times I$) | Overall Risk Classification |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **AC-E02** | Elevation of Priv. | LAB-02 | Root SUID binary abuse (`/usr/bin/find`) | 5 | 5 | **25** | **CRITICAL** |
| **AC-E01** | Elevation of Priv. | LAB-01 | Vertical IDOR in administrative API | 4 | 5 | **20** | **CRITICAL** |
| **AC-T01** | Tampering | LAB-01 | SQL Injection via query parameter | 4 | 5 | **20** | **CRITICAL** |
| **AC-T02** | Tampering | LAB-02 | World-writable system configuration (`/etc/crontab`) | 4 | 5 | **20** | **CRITICAL** |
| **AC-S01** | Spoofing | LAB-01 | Predictable sequential cookie session hijacking | 4 | 4 | **16** | **HIGH** |
| **AC-I01** | Info Disclosure | LAB-01 | Local file directory traversal (`/view?file=`) | 4 | 4 | **16** | **HIGH** |
| **AC-I02** | Info Disclosure | LAB-02 | Plaintext credential harvesting via FTP sniffing | 4 | 4 | **16** | **HIGH** |
| **AC-D02** | Denial of Service | LAB-02 | Kernel process starvation via fork bomb | 4 | 4 | **16** | **HIGH** |
| **AC-S02** | Spoofing | LAB-02 | ARP spoofing on host-only virtual switch | 3 | 3 | **9** | **MEDIUM** |
| **AC-D01** | Denial of Service | LAB-01 | Regular expression catastrophic backtracking | 3 | 3 | **9** | **MEDIUM** |
| **AC-R01** | Repudiation | LAB-01 | Unauthenticated log deletion and client IP spoofing| 3 | 3 | **9** | **MEDIUM** |
| **AC-R02** | Repudiation | LAB-02 | Unaudited shell command execution under shared user| 3 | 2 | **6** | **MEDIUM** |

---

## 14.0 RANKED MITIGATION RECOMMENDATIONS

Mitigations are prioritized based on risk ratings, implementation complexity, and defense-in-depth architectural impact.

```
       [ PRIORITY 1: IMMEDIATE / CRITICAL ]  --> SUID fixes, SQLi parameterized queries, IDOR fixes
                         |
       [ PRIORITY 2: STRUCTURAL / HIGH ]     --> Strong CSPRNG sessions, TLS enforcement, Path sanitization
                         |
       [ PRIORITY 3: HARDENING / MEDIUM ]    --> ulimit process caps, Auditd logging, Static ARP/FIM
```

### 14.1 Priority 1: High/Critical Mitigations (Immediate Remediation Required)
1. **Eliminate Dangerous SUID Binaries (LAB-02 - AC-E02):**
   - *Action:* Execute `chmod u-s /usr/bin/find` and remove SUID flags from administrative tools. Audit the filesystem with `find / -perm -4000` to ensure only essential utilities (`/bin/su`, `/usr/bin/sudo`) retain elevated bits.
   - *Effort:* Low ($\approx 1$ hour). *Impact:* Eliminates trivial root privilege escalation.
2. **Implement Parameterized Queries (LAB-01 - AC-T01):**
   - *Action:* Refactor all database queries to use prepared statements with typed parameters. Prohibit string concatenation in SQL handlers.
   - *Effort:* Medium ($\approx 4$ hours). *Impact:* Completely neutralizes SQL injection vulnerabilities.
3. **Enforce Server-Side Authorization for Object Access (LAB-01 - AC-E01):**
   - *Action:* Implement middleware enforcing access control checks on every API request. Verify that the authenticated `session.user_id` matches the targeted object owner or possesses verified administrative privileges.
   - *Effort:* Medium ($\approx 6$ hours). *Impact:* Prevents horizontal and vertical IDOR attacks.
4. **Harden System File Permissions (LAB-02 - AC-T02):**
   - *Action:* Restore standard POSIX permissions across `/etc/`: `chmod 644 /etc/crontab`, `chmod 644 /etc/passwd`, `chmod 600 /etc/shadow`. Ensure all system files are strictly owned by `root:root`.
   - *Effort:* Low ($\approx 30$ minutes). *Impact:* Blocks unauthorized configuration tampering.

### 14.2 Priority 2: Medium Mitigations (High Architectural Impact)
5. **Implement Cryptographically Secure Session Management (LAB-01 - AC-S01):**
   - *Action:* Replace sequential cookie generation with 128-bit CSPRNG-generated session tokens. Enforce `HttpOnly`, `Secure`, and `SameSite=Strict` cookie attributes.
   - *Effort:* Medium ($\approx 4$ hours). *Impact:* Mitigates session hijacking and cookie spoofing.
6. **Path Canonicalization and Whitelisting (LAB-01 - AC-I01):**
   - *Action:* Resolve input paths using canonical path functions (e.g., `path.resolve()` in Node.js, `os.path.realpath()` in Python) and verify that the target directory begins strictly with the allowed base path.
   - *Effort:* Low ($\approx 2$ hours). *Impact:* Eliminates local directory traversal.
7. **Transition to Encrypted Services & Disable Cleartext Protocols (LAB-02 - AC-I02):**
   - *Action:* Terminate standard FTP daemon (`proftpd`) or enforce TLS encryption (`FTPS`). Upgrade Apache to enforce HTTPS with modern TLS cipher suites.
   - *Effort:* Medium ($\approx 3$ hours). *Impact:* Prevents credential sniffing on the host-only network.
8. **Enforce Operating System Resource Quotas (LAB-02 - AC-D02):**
   - *Action:* Update `/etc/security/limits.conf` to restrict user process ceilings: `* hard nproc 150` and `* hard maxlogins 3`.
   - *Effort:* Low ($\approx 1$ hour). *Impact:* Prevents fork-bomb denial-of-service conditions.

### 14.3 Priority 3: Low/Hardening Mitigations (Defense-in-Depth)
9. **Deploy System Call Auditing & Non-Repudiation Architecture (LAB-02 - AC-R02):**
   - *Action:* Enable and configure the Linux `auditd` daemon to log all system execution calls (`execve`) and capture user identity metadata.
   - *Effort:* Medium ($\approx 4$ hours). *Impact:* Guarantees non-repudiation for incident response.
10. **Harden Input Regex Parsing (LAB-01 - AC-D01):**
    - *Action:* Analyze regular expressions for nested quantifiers. Replace vulnerable expressions with linear validation algorithms or Google RE2 engines.
    - *Effort:* Low ($\approx 2$ hours). *Impact:* Prevents ReDoS CPU exhaustion.
11. **Enforce Static ARP Caching and Network Isolation (LAB-02 - AC-S02):**
    - *Action:* Define static ARP pairs on the host and guest for the host-only virtual adapter.
    - *Effort:* Low ($\approx 1$ hour). *Impact:* Prevents ARP spoofing on the virtual switch.
12. **Tamper-Resistant Logging Controls (LAB-01 - AC-R01):**
    - *Action:* Configure application logging to stream records to an append-only file with root-only read access; strip or validate client IP headers (`X-Forwarded-For`).
    - *Effort:* Low ($\approx 2$ hours). *Impact:* Secures application log integrity.

---

## 15.0 RULES OF ENGAGEMENT (ROE)

The Rules of Engagement (RoE) define the operational boundaries, authorized techniques, prohibitions, and protocols governing all assessment activities.

### 15.1 Testing Windows and Scheduling
- **Authorized Testing Period:** November 14, 2026 through November 30, 2026.
- **Permitted Operational Hours:** Monday through Friday, 09:00 to 18:00 Local Time.
- **Blackout Periods:** Weekends and scheduled lab maintenance intervals without prior written approval.
- **Testing Cadence:** Scans must be throttled to prevent resource exhaustion on host workstations.

### 15.2 Permitted Security Assessment Techniques
The following assessment methodologies are explicitly authorized within the boundaries defined in Section 4.0:
1. **Passive Reconnaissance & Network Discovery:**
   - Host discovery using ICMP echo requests and TCP SYN scans over `vboxnet0` (`192.168.56.0/24`).
   - Service banner grabbing and version enumeration via Nmap or Netcat.
2. **Web Application Security Auditing (LAB-01):**
   - Manual parameter manipulation using local interception proxies (e.g., OWASP ZAP, Burp Suite Community).
   - SQL injection identification using manual syntax verification and single-thread parameter testing.
   - Cross-Site Scripting (XSS), IDOR, and session token analysis.
   - Source code review of locally hosted application scripts in `/frontend` and `/backend`.
3. **System Configuration Auditing (LAB-02):**
   - Password auditing against standard test accounts (`student`, `ftpuser`) using curated lab wordlists.
   - Local privilege escalation enumeration (checking SUID/SGID bits, sudo permissions, cron configurations).
   - Analysis of local process memory and file system permissions.

### 15.3 Explicitly Prohibited Actions and Out-of-Bounds Exploits
The following actions represent severe violations of the assessment charter:
1. **Denial-of-Service (DoS / DDoS):** High-volume packet floods (SYN floods, UDP floods, ping floods), application-layer stress testing (LOIC, Slowloris), or deliberately crashing target processes is strictly forbidden.
2. **Third-Party / Cloud-Based Automated Scanners:** Running automated cloud vulnerability scanners (e.g., Qualys Cloud, Nessus Cloud, Shodan Monitor) that route traffic through external infrastructure is prohibited. All tooling must execute locally on the assessor's machine.
3. **Persistence Mechanisms & Backdoors:** Installing rootkits, backdoor kernel modules, persistent webshells, or modifying system startup scripts to maintain long-term access is strictly disallowed. Any test artifacts introduced during assessment must be documented and removed immediately.
4. **Outbound Network Traffic from Targets:** Generating outbound network connections from LAB-02 toward external networks, the physical host's LAN, or the public Internet is prohibited.
5. **Attacks Against Physical Host or Hypervisor:** Attempting VM escape exploits, hypervisor fuzzing, or accessing the host operating system's files outside the lab workspace is strictly forbidden.

### 15.4 Evidence Collection and Chain of Custody Protocols
All assessment findings must be substantiated with verifiable, non-destructive evidence handled in accordance with digital forensics best practices:
- **Evidence Storage:** All screenshots, HTTP request/response logs, and terminal outputs must be stored in the designated, encrypted assessment folder (`/reports`).
- **Cryptographic Hashing:** Log archives and proof-of-concept scripts must be hashed using SHA-256 upon creation to preserve evidence integrity:
  $$\text{SHA256}(\text{evidence\_file}) \rightarrow \text{Recorded in Assessor Journal}$$
- **Data Minimization:** Screenshots must redact sensitive personal credentials or irrelevant host workstation details. No live student personal data may be retained.
- **Proof-of-Concept Restraint:** Exploits must demonstrate vulnerability presence without causing data destruction (e.g., executing `id` or `whoami` rather than deleting files or dropping database tables).

### 15.5 Incident Escalation and Communication Pathways
In the event of an operational anomaly, unintended service disruption, or discovery of a critical vulnerability outside defined boundaries, assessors must follow the escalation protocol outlined in Table 15.5:

```
+---------------------------------------------------------------------------------------+
|                              INCIDENT ESCALATION PATHWAY                              |
+---------------------------------------------------------------------------------------+

  [ STEP 1: Immediate Cessation ]
  Halt all active assessment tooling; preserve active logs and system state.
              |
              v
  [ STEP 2: Assess Severity & Impact ]
  Determine if the issue affects local targets only or impacts out-of-scope systems.
              |
              v
  [ STEP 3: Notify Technical POC ]
  Contact the Lab Technical Coordinator within 15 minutes of occurrence.
              |
              v
  [ STEP 4: Incident Review & Formal Logging ]
  Document the exact command, timestamp, and observed failure state in an Incident Report.
```

| Escalation Level | Trigger Condition | Responsible Party | Response Window | Action Required |
| :--- | :--- | :--- | :--- | :--- |
| **Level 1 (Standard)** | Technical clarification; scope ambiguity; routine scan notification. | Lab Technical Assistant | 4 Hours | Written notification via internal lab ticketing system. |
| **Level 2 (High)** | Inadvertent target crash; local loopback hang; unexpected service stop. | Lab Systems Administrator | 30 Minutes | Immediate testing halt; restart service; verify target health. |
| **Level 3 (Critical)** | Traffic detected escaping host-only boundary; host OS instability; data corruption. | Dr. A. Rab (Lab Director) | Immediate (< 15 min) | Immediate termination of assessment; isolate host adapter; executive review. |

### 15.6 Safe Stopping Conditions and Circuit Breakers
Assessors must immediately abort testing activities upon encountering any of the following operational circuit breakers:
1. **Network Boundary Breach:** Any evidence that packets generated by assessment tools are traversing physical interfaces (e.g., Wi-Fi adapter or default gateway) rather than virtual interfaces (`127.0.0.1` or `vboxnet0`).
2. **Target System Crash / Unresponsiveness:** If LAB-01 or LAB-02 fails to respond to standard health checks for more than 60 seconds.
3. **Kernel Panic or Hypervisor Alert:** Any hypervisor alert indicating host-guest memory allocation errors or hypervisor driver faults.
4. **Unintended Data Loss / Corruption:** Accidental deletion or structural corruption of underlying lab databases or filesystems.

---

## 16.0 FINDINGS, EDUCATIONAL REFLECTION & CONCLUSIONS

### 16.1 Synthesis of Findings
This authorized assessment successfully mapped the complete architectural posture, trust boundaries, and threat profile of the RabTech Lab training infrastructure. Key technical findings include:
- **Application Tier (LAB-01):** The web application exhibits significant authorization and input validation vulnerabilities. Lack of server-side role validation creates severe Broken Object-Level Authorization (IDOR) risks (AC-E01, Risk Score 20), while unparameterized database queries leave the application open to SQL Injection (AC-T01, Risk Score 20). Furthermore, predictable session generation exposes users to session hijacking (AC-S01, Risk Score 16).
- **Virtual Machine Tier (LAB-02):** The host-only virtual machine exhibits multiple severe privilege escalation vectors. Misconfigured SUID permissions on `/usr/bin/find` provide trivial, instantaneous root compromise (AC-E02, Risk Score 25). World-writable configuration files (AC-T02, Risk Score 20) and unencrypted legacy protocols (AC-I02, Risk Score 16) further demonstrate the compounding risk of legacy operating system environments.

```
+-----------------------------------------------------------------------------+
|                     RISK DISTRIBUTION BREAKDOWN                             |
+-----------------------------------------------------------------------------+
|  Critical Risk Flaws (Score 20-25):  4  [====================] 33.3%        |
|  High Risk Flaws     (Score 10-16):  4  [====================] 33.3%        |
|  Medium Risk Flaws   (Score 5-9):    4  [====================] 33.3%        |
|  Low Risk Flaws      (Score 1-4):    0  [                    ]  0.0%        |
|  Total Evaluated Scenarios:         12  [====================] 100%         |
+-----------------------------------------------------------------------------+
```

### 16.2 Academic Implications and Defensive Key Takeaways
From an educational standpoint, this project yields three fundamental principles for aspiring cybersecurity practitioners and software engineers:
1. **Security Cannot Rely on Obscurity or Isolation Alone:** Restricting LAB-01 to `127.0.0.1` and LAB-02 to a private host-only network prevented unauthorized external access, but did not eliminate the severe vulnerabilities resident within those boundaries. Once an attacker obtains an initial foothold, architectural misconfigurations provide frictionless paths to total compromise.
2. **The Principle of Least Privilege is Non-Negotiable:** Both critical findings (IDOR in LAB-01 and SUID abuse in LAB-02) stem directly from granting excessive privileges: standard users accessing administrative records, and unprivileged shell users executing commands as root.
3. **Structured Threat Modeling Preempts Exploitation:** Applying the STRIDE framework allowed the assessment team to identify systemic design weaknesses prior to executing active exploits. Threat modeling provides defensive engineering teams with a proactive methodology to build secure architectures before deploying code.

### 16.3 Final Formal Conclusion
The RabTech Lab environment provides an exemplary pedagogical platform that accurately reflects real-world vulnerability patterns. The vulnerabilities identified during this assessment are typical of systems undergoing incremental development without formal security gates. Implementing the prioritized mitigations outlined in Section 14.0—specifically parameterizing SQL queries, stripping SUID bits, enforcing server-side authorization checks, and securing configuration permissions—will significantly elevate the security posture of the lab infrastructure.

This assessment was conducted with strict adherence to ethical standards, professional methodologies (NIST SP 800-115, PTES), and the agreed Rules of Engagement. All operational activities concluded safely with zero collateral impact on host environments or external networks.

---

## APPENDICES

### Appendix A: Acronyms and Technical Glossary
- **API:** Application Programming Interface
- **ARP:** Address Resolution Protocol
- **ASVS:** Application Security Verification Standard (OWASP)
- **CFAA:** Computer Fraud and Abuse Act (18 U.S.C. § 1030)
- **CSPRNG:** Cryptographically Secure Pseudorandom Number Generator
- **DFD:** Data Flow Diagram
- **DoS / DDoS:** Denial of Service / Distributed Denial of Service
- **HMAC:** Hash-based Message Authentication Code
- **IAM:** Identity and Access Management
- **IDOR:** Insecure Direct Object Reference
- **NIST:** National Institute of Standards and Technology
- **OWASP:** Open Web Application Security Project
- **POSIX:** Portable Operating System Interface
- **PTES:** Penetration Testing Execution Standard
- **RBAC:** Role-Based Access Control
- **ReDoS:** Regular Expression Denial of Service
- **RoE:** Rules of Engagement
- **SQLi:** Structured Query Language Injection
- **STRIDE:** Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege
- **SUID:** Set Owner User ID upon execution
- **TLS:** Transport Layer Security
- **UID:** User Identifier (POSIX)
- **VM:** Virtual Machine
- **WSTG:** Web Security Testing Guide (OWASP)

### Appendix B: Standards Alignment Cross-Reference Matrix

| Report Section | NIST SP 800-115 Alignment | PTES Standard Phase | OWASP ASVS / WSTG Reference |
| :--- | :--- | :--- | :--- |
| **Section 3.0 & 15.0** | § 2.2 Roles and Responsibilities; § 2.4 Testing Rules | Pre-engagement Interactions; Scope Verification | WSTG-INFO-01 (Scope and Boundary Verification) |
| **Section 4.0 & 5.0** | § 3.1 Target Identification and Discovery Techniques | Intelligence Gathering; Asset Inventory | ASVS V1.1 (Secure Architecture and Scope) |
| **Section 6.0 & 7.0** | § 4.3 Identity and Credential Review | Threat Modeling; Privilege Architecture | ASVS V2.0 (Authentication); ASVS V4.0 (Access Control) |
| **Section 8.0 & 9.0** | § 3.2 Network and System Analysis | Threat Modeling; Trust Analysis | ASVS V1.2 (Security Architecture Boundaries) |
| **Section 10.0–12.0** | § 4.1 Vulnerability Identification and Analysis | Threat Modeling; Vulnerability Analysis | WSTG-INPV (Input Validation); WSTG-ATHZ (Authorization) |
| **Section 13.0 & 14.0** | § 5.1 Analysis and Prioritization | Post-Exploitation; Remediation Roadmap | OWASP Risk Rating Methodology |
| **Section 16.0** | § 5.2 Reporting and Presentation | Final Reporting | WSTG-APPD (Reporting and Metrics) |

---
*End of Report — RabTech Lab Cybersecurity Assessment & Threat Model (SEC-REP-LAB-2026-001)*
