# Adversary Simulation & Penetration Testing Lab

A virtualized offensive security lab designed to simulate enterprise network security architecture, perform penetration testing against intentionally vulnerable applications, and document attack paths, security findings, and remediation recommendations.

![Security](https://img.shields.io/badge/Focus-Offensive%20Security-red)
![Platform](https://img.shields.io/badge/Platform-VirtualBox%20%2F%20VMware-blue)
![Linux](https://img.shields.io/badge/Linux-Kali%20%7C%20Ubuntu-orange)
![Firewall](https://img.shields.io/badge/Firewall-pfSense-green)
![Status](https://img.shields.io/badge/Status-Completed-success)

---

## 📌 Project Overview

This project focuses on building and operating an isolated penetration-testing environment using pfSense, Kali Linux, DVWA, Wireshark, Metasploit, Nmap, and Linux-based virtual machines.

The lab simulates an enterprise network with separate attacker and target segments. It enables controlled security assessments, network traffic analysis, vulnerability exploitation, and documentation of security risks.

The primary objective is to understand how attackers identify vulnerabilities, exploit weaknesses, analyze attack impact, and how defenders can reduce those risks through network segmentation, firewall rules, monitoring, and remediation.

> ⚠️ All testing was performed in an isolated lab environment against intentionally vulnerable systems. No unauthorized systems were targeted.

---

## 🎯 Objectives

- Design and deploy a virtualized offensive security lab.
- Configure pfSense as a perimeter firewall and router.
- Implement network segmentation using VLANs and firewall rules.
- Configure NAT, routing, and traffic filtering.
- Perform reconnaissance and service enumeration.
- Identify and exploit common web application vulnerabilities.
- Analyze network traffic using Wireshark.
- Document attack paths and exploitation evidence.
- Map attack techniques to the MITRE ATT&CK framework.
- Prepare VAPT findings with risk severity and remediation.

---

## 🏗️ Lab Architecture

```text
                         INTERNET
                             |
                             |
                      [ Virtual NAT ]
                             |
                             |
                     +----------------+
                     |    pfSense     |
                     | Firewall/Router|
                     |                |
                     | NAT / VLANs    |
                     | Firewall Rules |
                     +----------------+
                       |            |
                       |            |
              ATTACKER NETWORK   TARGET NETWORK
                  VLAN 10           VLAN 20
                       |            |
              +----------------+  +----------------+
              |   Kali Linux   |  |  Ubuntu/Linux  |
              |                |  |                |
              | Nmap           |  | DVWA           |
              | Metasploit     |  | Web Server     |
              | Burp Suite     |  | Vulnerable App |
              | Wireshark      |  |                |
              +----------------+  +----------------+
                       |
                       |
                 [ Monitoring ]
                       |
                  Wireshark
```

### Network Segmentation

| Component | Example Configuration |
|---|---|
| Firewall | pfSense |
| Attacker VM | Kali Linux |
| Target VM | Ubuntu/Linux |
| Vulnerable Application | DVWA |
| Attacker Network | VLAN 10 |
| Target Network | VLAN 20 |
| Firewall | Custom filtering rules |
| Traffic Analysis | Wireshark |
| Virtualization | VirtualBox / VMware |

> Replace the example VLANs, IP addresses, and interface names with your actual lab configuration.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| pfSense | Firewall, router, NAT, VLAN segmentation |
| Kali Linux | Penetration testing and security assessment |
| DVWA | Intentionally vulnerable web application |
| Nmap | Network reconnaissance and service enumeration |
| Metasploit | Controlled exploitation and validation |
| Burp Suite | HTTP request interception and web testing |
| Wireshark | Packet capture and network traffic analysis |
| Linux | Server administration and target environment |
| VirtualBox / VMware | Virtualized lab deployment |
| MITRE ATT&CK | Attack technique mapping |

---

## 🔧 Lab Setup

### 1. Virtualization Environment

Create the required virtual machines:

- pfSense firewall/router
- Kali Linux attacker machine
- Ubuntu/Linux target machine
- DVWA web application

Configure the virtual network adapters so that attacker and target systems communicate through pfSense.

### 2. pfSense Configuration

Configure pfSense with:

- WAN and LAN interfaces
- Internal routing
- NAT rules
- VLAN segmentation
- Custom firewall rules
- Traffic filtering between attacker and target networks

Example network design:

```text
VLAN 10 - Attacker Network
10.10.10.0/24

VLAN 20 - Target Network
10.10.20.0/24

pfSense Gateway
10.10.10.1
10.10.20.1
```

These are example addresses only.

### 3. Kali Linux

Install and configure:

- Nmap
- Metasploit Framework
- Burp Suite
- Wireshark
- SQLmap
- Other authorized penetration-testing tools

### 4. DVWA Deployment

Deploy DVWA on the target Linux machine and configure the web server and database.

DVWA provides an intentionally vulnerable environment for practicing web application security testing.

---

## 🔍 Penetration Testing Methodology

The assessment followed a structured VAPT workflow.

```text
Reconnaissance
      |
      v
Service Enumeration
      |
      v
Vulnerability Identification
      |
      v
Exploitation
      |
      v
Post-Exploitation Analysis
      |
      v
Evidence Collection
      |
      v
Risk Assessment
      |
      v
Remediation Recommendations
```

### Phase 1: Reconnaissance

Identify available hosts, open ports, and exposed services within the authorized lab network.

Tools:

- Nmap
- Network discovery utilities

Example:

```bash
nmap -sV -sC <TARGET_IP>
```

### Phase 2: Service Enumeration

Analyze discovered services and determine potential attack surfaces.

Activities:

- Port scanning
- Service version detection
- HTTP enumeration
- Web application discovery

### Phase 3: Vulnerability Identification

Assess DVWA and exposed services for common vulnerabilities.

### Phase 4: Exploitation

Validate vulnerabilities using controlled exploitation techniques.

Tools:

- Metasploit
- Burp Suite
- SQLmap
- Manual testing

### Phase 5: Post-Exploitation Analysis

Within the authorized lab, analyze the impact of successful exploitation.

Activities:

- Confirming access
- Identifying affected assets
- Reviewing permissions
- Collecting exploitation evidence

### Phase 6: Reporting

Document:

- Vulnerability description
- Affected asset
- Attack path
- Evidence
- Risk severity
- Remediation recommendation

---

## 🧪 Web Application Vulnerabilities Tested

### 1. SQL Injection

**Description:**  
SQL Injection occurs when untrusted input is incorporated into database queries without proper validation or parameterization.

**Testing:**

- Identify injectable parameters.
- Analyze database error behavior.
- Validate impact in DVWA.
- Recommend parameterized queries.

**Remediation:**

- Use prepared statements.
- Apply input validation.
- Use least-privilege database accounts.
- Avoid exposing database errors.

---

### 2. Cross-Site Scripting (XSS)

**Description:**  
XSS allows malicious scripts to execute in a victim's browser through vulnerable web application input.

**Testing:**

- Identify reflected or stored input points.
- Validate script execution in DVWA.
- Analyze affected requests and responses.

**Remediation:**

- Context-aware output encoding.
- Input validation.
- Content Security Policy.
- Secure cookie configuration.

---

### 3. Cross-Site Request Forgery (CSRF)

**Description:**  
CSRF abuses an authenticated user's browser to submit unauthorized requests.

**Testing:**

- Identify state-changing requests.
- Review request parameters.
- Validate CSRF protections in the lab.

**Remediation:**

- Anti-CSRF tokens.
- SameSite cookie attributes.
- Origin and Referer validation where appropriate.

---

### 4. Command Injection

**Description:**  
Command Injection occurs when user-controlled input reaches operating system commands.

**Testing:**

- Identify vulnerable application functionality.
- Validate command execution within DVWA.
- Document affected functionality.

**Remediation:**

- Avoid shell execution where possible.
- Use allowlists.
- Apply least privilege.
- Validate and sanitize inputs.

---

### 5. File Inclusion

**Description:**  
File Inclusion vulnerabilities allow unintended local or remote file access through vulnerable application parameters.

**Testing:**

- Identify file path parameters.
- Analyze application behavior.
- Validate impact in the isolated lab.

**Remediation:**

- Use allowlisted file mappings.
- Avoid user-controlled file paths.
- Apply proper access controls.
- Disable unnecessary remote inclusion features.

---

## 📡 Network Traffic Analysis

Wireshark was used to inspect and analyze network traffic generated during penetration testing.

### Activities

- Capture HTTP requests and responses.
- Analyze TCP connections.
- Identify DNS and network communication.
- Observe traffic between attacker and target segments.
- Validate firewall filtering.
- Review attack-related network activity.

### Example Filters

```text
http
```

```text
tcp
```

```text
dns
```

```text
ip.addr == <TARGET_IP>
```

> Use the actual target IP address from your lab when analyzing traffic.

---

## 🧱 pfSense Security Configuration

The firewall was configured to simulate enterprise network security controls.

### Implemented Controls

- Network segmentation
- Inter-VLAN traffic filtering
- NAT configuration
- Custom firewall rules
- Restricted access between network segments
- Controlled communication between attacker and target VMs

### Security Validation

The configuration was tested by verifying:

- Reachability between authorized segments.
- Blocked traffic based on firewall rules.
- NAT behavior.
- Access to intended services.
- Network traffic observed through packet capture.

---

## 🧭 MITRE ATT&CK Mapping

The following techniques are relevant to the activities performed in this type of lab.

| Technique | ID | Lab Activity |
|---|---|---|
| Network Service Scanning | T1046 | Nmap reconnaissance |
| Exploitation of Public-Facing Application | T1190 | Vulnerable web application testing |
| Command and Scripting Interpreter | T1059 | Command execution validation |
| Exploitation for Client Execution | T1203 | Only if applicable to tested client-side vulnerabilities |
| Valid Accounts | T1078 | Only if authorized account testing was performed |

> Technique mapping should be finalized using the exact actions and evidence recorded during your assessment. Not every technique applies to every lab.

---

## 📊 VAPT Reporting

Each vulnerability was documented using a structured format.

### Finding Template

| Field | Description |
|---|---|
| Finding ID | Unique vulnerability identifier |
| Vulnerability | Name of the vulnerability |
| Affected Asset | Target IP / application |
| Severity | Informational / Low / Medium / High / Critical |
| Description | Technical explanation |
| Attack Path | Steps leading to exploitation |
| Evidence | Screenshots, requests, logs |
| Impact | Potential security consequences |
| Remediation | Recommended fix |
| References | Relevant security references |

### Risk Severity

Severity should be assigned based on the observed impact, exploitability, affected assets, and applicable risk methodology.

---

## 📁 Project Structure

```text
Adversary-Simulation-Penetration-Testing-Lab/
│
├── README.md
│
├── Architecture/
│   ├── network-topology.png
│   ├── lab-design.drawio
│   └── ip-addressing.md
│
├── pfSense/
│   ├── firewall-rules.md
│   ├── nat-configuration.md
│   ├── vlan-configuration.md
│   └── screenshots/
│
├── Reconnaissance/
│   ├── nmap-scans/
│   └── enumeration-notes.md
│
├── Exploitation/
│   ├── SQL-Injection/
│   ├── XSS/
│   ├── CSRF/
│   ├── Command-Injection/
│   └── File-Inclusion/
│
├── Network-Analysis/
│   ├── wireshark-captures/
│   └── traffic-analysis.md
│
├── Reports/
│   ├── VAPT-Report.pdf
│   ├── findings.md
│   └── remediation.md
│
└── Screenshots/
    ├── lab-setup.png
    ├── pfsense-dashboard.png
    ├── kali-linux.png
    ├── dvwa.png
    └── exploitation-evidence.png
```

---

## 📸 Evidence & Screenshots

Add screenshots demonstrating your actual work:

- [ ] Virtual lab topology
- [ ] pfSense dashboard
- [ ] Firewall rules
- [ ] VLAN configuration
- [ ] Kali Linux environment
- [ ] DVWA application
- [ ] Nmap scan results
- [ ] Metasploit exploitation evidence
- [ ] Burp Suite HTTP requests
- [ ] Wireshark packet captures
- [ ] VAPT report findings

---

## 🔐 Security & Ethics

This project was conducted in a controlled and isolated environment.

- Only authorized systems were tested.
- DVWA was used as an intentionally vulnerable target.
- No real-world systems were targeted.
- Exploitation was performed for educational and defensive security purposes.
- Network access was restricted to the lab environment.

---

## 📚 References

- [pfSense Documentation](https://docs.netgate.com/pfsense/en/latest/)
- [Kali Linux Documentation](https://www.kali.org/docs/)
- [DVWA](https://github.com/digininja/DVWA)
- [Nmap Documentation](https://nmap.org/docs.html)
- [Metasploit Framework](https://github.com/rapid7/metasploit-framework)
- [Wireshark Documentation](https://www.wireshark.org/docs/)
- [MITRE ATT&CK](https://attack.mitre.org/)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)

---

## 👨‍💻 Author

**Gaurav Kalra**

Cybersecurity Enthusiast | Penetration Testing | Network Security | VAPT

---

## ⭐ Project Highlights

- Designed a virtualized enterprise-style security lab.
- Configured pfSense firewall, routing, NAT, and segmentation.
- Performed controlled penetration testing against DVWA.
- Analyzed common web vulnerabilities.
- Used Nmap, Metasploit, Burp Suite, and Wireshark.
- Documented findings using a structured VAPT methodology.
- Applied MITRE ATT&CK mapping to relevant attack techniques.
