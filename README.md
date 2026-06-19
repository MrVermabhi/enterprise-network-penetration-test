# Enterprise Network Penetration Test

## Overview

This project demonstrates a complete penetration testing engagement against a vulnerable Linux-based enterprise environment. The objective was to identify security weaknesses, validate exploitability, assess business impact, and provide remediation recommendations, and create a technical report.

The assessment followed a structured penetration testing methodology including:

* Reconnaissance
* Scanning
* Enumeration
* Vulnerability Assessment
* Exploitation
* Post-Exploitation
* Reporting

---

## Environment

### Attacker Machine

* Kali Linux

### Target Machine

* Linux Server
* IP Address: 192.168.100.10

---

## Tools Used

| Category                 | Tools                    |
| ------------------------ | ------------------------ |
| Reconnaissance           | Netdiscover, Whois       |
| Scanning                 | Nmap                     |
| Enumeration              | Enum4Linux, SMBClient    |
| Vulnerability Assessment | Nessus, Nikto, WhatWeb   |
| Exploitation             | Metasploit, Searchsploit |
| Password Analysis        | John The Ripper          |
| Operating System         | Kali Linux               |

---

## Methodology

Reconnaissance

↓

Scanning

↓

Enumeration

↓

Vulnerability Assessment

↓

Exploitation

↓

Post-Exploitation

↓

Reporting

---

## Network Discovery

Open services discovered during enumeration included:

| Port | Service    |
| ---- | ---------- |
| 21   | FTP        |
| 22   | SSH        |
| 23   | Telnet     |
| 25   | SMTP       |
| 53   | DNS        |
| 80   | HTTP       |
| 111  | RPCBind    |
| 139  | SMB        |
| 445  | SMB        |
| 3306 | MySQL      |
| 5432 | PostgreSQL |
| 5900 | VNC        |
| 6667 | IRC        |
| 8180 | Tomcat     |

---

## Vulnerability Assessment

### Nessus Scan

A Nessus assessment identified 69 vulnerabilities across the target environment.

#### Critical Findings

* Ubuntu Linux End-of-Life
* Weak VNC Configuration
* SSLv2 and SSLv3 Enabled

#### High Severity Findings

* Samba Badlock Vulnerability
* World Readable NFS Shares
* Insecure RSH and RLogin Services

---

## Web Application Findings

Nikto and WhatWeb identified:

* Apache 2.2.8
* PHP 5.2.4
* WebDAV Enabled
* phpMyAdmin Exposure
* Directory Listing Enabled
* TRACE Method Enabled
* Missing Security Headers

### Exposed Resources

* /phpinfo.php
* /phpMyAdmin/
* /test/
* /doc/
* /icons/

---

## SMB Enumeration

The target was running:

* Samba 3.0.20
* Anonymous SMB Access Enabled
* Writable Shares Exposed

Enumerated shares included:

* docs
* IPC$
* print$
* ADMIN$

Multiple user accounts were discovered including:

* root
* postgres
* mysql
* msfadmin

---

## Exploitation

### CVE-2011-2523 – VSFTPD Backdoor

Risk Level: Critical

The vulnerable FTP service allowed remote command execution resulting in root-level access.

Outcome:

* Remote Shell Obtained
* Root Privileges Achieved

---

### CVE-2010-2075 – UnrealIRCd Backdoor

Risk Level: Critical

A reverse shell was established through the vulnerable IRC service.

Outcome:

* Remote Command Execution
* Root Access

---

### CVE-2007-2446 – Samba Username Map Script

Risk Level: Critical

A vulnerable Samba configuration enabled remote command execution.

Outcome:

* Shell Access Obtained
* Full System Compromise

---

## Post Exploitation

### Privilege Verification

Commands used:

* whoami
* id
* uname -a

Root access was successfully verified.

---

### Password Analysis

Password hashes were extracted and analysed.

Recovered credentials included:

| User     | Password  |
| -------- | --------- |
| klog     | 123456789 |
| sys      | batman    |
| msfadmin | chester   |
| root     | chester   |

This demonstrated weak password policies and credential reuse.

---

## Business Impact

Successful exploitation allowed:

* Remote Code Execution
* Root-Level System Access
* Credential Compromise
* Persistence Opportunities
* Potential Lateral Movement
* Exposure of Sensitive Data

---

## Recommendations

### Immediate Actions

* Patch all legacy services
* Upgrade Samba
* Upgrade Apache
* Disable Telnet
* Disable RLogin
* Remove Anonymous SMB Access

### Security Improvements

* Enforce Strong Password Policies
* Implement MFA
* Regular Vulnerability Assessments
* Continuous Patch Management
* Network Segmentation
* Security Monitoring

---

## Skills Demonstrated

* Penetration Testing
* Vulnerability Assessment
* CVE Research
* Network Enumeration
* SMB Security Analysis
* Web Application Testing
* Exploit Validation
* Password Auditing
* Linux Administration
* Security Reporting

---

## Disclaimer

This project was conducted in a controlled lab environment for educational and security assessment purposes only.
