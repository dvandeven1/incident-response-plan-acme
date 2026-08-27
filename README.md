# incident-response-plan-acme
Simulated IR plan for a fictional sports tech company
# Incident Response Plan | ACME Athletics

**Prepared by:** Dante Vandeven
**Project Type:** Simulated Cybersecurity Project
**Version:** 1.1

> This is a self directed cybersecurity project created to demonstrate my understanding of incident response procedures, Linux administration, network security tools, documentation, and security operations. ACME Athletics is a fictional sports technology company created for this simulation.

## 1. Overview

This Incident Response Plan outlines a structured approach ACME Athletics would use to identify, contain, eradicate, and recover from cybersecurity incidents.

ACME Athletics is a fictional sports technology company that handles athlete performance data and internal analytics platforms. This environment was created to simulate realistic security incidents and response procedures.

## 2. Objectives

* Detect and contain security incidents quickly
* Minimize operational downtime and data loss
* Protect sensitive athlete and partner information
* Maintain clear incident documentation
* Establish repeatable response and escalation procedures
* Use lessons learned to improve future security practices

## 3. Scope

This simulated plan applies to digital assets including:

* Internal servers and endpoints
* Athlete tracking systems and cloud databases
* Company email and mobile devices
* Communication platforms
* Partner facing APIs
* Vendor systems
* Network infrastructure

## 4. Incident Response Roles

| Role                   | Responsibility                                                   |
| ---------------------- | ---------------------------------------------------------------- |
| Incident Response Lead | Coordinates incident handling, escalation, and documentation     |
| System Administrator   | Assists with infrastructure isolation, remediation, and recovery |
| Communications         | Coordinates internal and external incident communication         |
| Legal Liaison          | Reviews potential legal and reporting obligations                |

For this simulation, I performed the planning and documentation responsibilities of the Incident Response Lead.

## 5. Incident Response Lifecycle

### A. Identification

Potential security incidents would be identified through monitoring of:

* System logs such as `journalctl` and `auth.log`
* Network traffic using Wireshark and tcpdump
* Authentication activity
* User reported security concerns
* Unusual system or network behavior

Potential indicators include:

* Repeated failed login attempts
* Logins from unusual locations or times
* Unexpected network connections
* Suspicious processes
* Unexpected data transfers
* Phishing reports

### B. Containment

The immediate goal of containment is to prevent an identified threat from spreading while preserving information needed for investigation.

Example Linux response actions:

```bash
# Lock a potentially compromised user account
sudo usermod -L compromised_user

# Identify a suspicious process
ps aux | grep suspicious_process

# Terminate the process if appropriate
sudo kill -9 [PID]

# Isolate a system from the network
ifconfig eth0 down
```

Network level containment could include blocking a known malicious IP address:

```bash
sudo iptables -A INPUT -s 192.168.88.66 -j DROP
```

Evidence should be preserved when appropriate before destructive remediation actions are performed.

Example forensic imaging command:

```bash
sudo dd if=/dev/sda of=/mnt/forensics/host_image.img bs=1M
```

### C. Eradication

After containment, the source of the incident would be investigated and removed.

Possible actions include:

* Removing malicious files or software
* Patching exploited vulnerabilities
* Rotating compromised passwords
* Rotating API keys and credentials
* Reviewing Identity and Access Management permissions
* Reviewing firewall rules
* Correcting insecure configurations

Example malware scan:

```bash
sudo apt-get install clamav
clamscan -r /home/
```

Example system update:

```bash
sudo apt-get update
sudo apt-get upgrade
```

### D. Recovery

Following eradication, affected systems would be returned to normal operation in a controlled manner.

Recovery procedures include:

* Restore systems from known clean backups when necessary
* Verify security patches and configuration changes
* Gradually return affected systems to production
* Monitor systems closely for signs of recurring compromise
* Confirm expected network services and connections

Example network checks:

```bash
netstat -tulpn
lsof -i
```

Additional network scanning could be performed using Nmap to verify exposed services.

### E. Lessons Learned

Following resolution:

* Conduct a team debrief
* Document the incident timeline
* Record containment and recovery actions
* Identify gaps in detection or escalation
* Determine the root cause when possible
* Update procedures based on findings
* Preserve relevant documentation for future reference

## 6. Incident Reporting Template

**Incident Name:**
**Date and Time Detected:**
**Detected By:**
**Systems Affected:**
**Indicators of Compromise:**
**Incident Severity:**
**Actions Taken:**
**Escalations:**
**Time to Containment:**
**Time to Recovery:**
**Root Cause:**
**Post Incident Summary:**
**Recommended Improvements:**

## 7. Sample Log Analysis

Example authentication log:

```log
Jun 17 14:22:53 server sshd[3421]: Failed password for root from 192.168.1.45 port 55874 ssh2
```

This entry represents a failed Secure Shell authentication attempt.

Repeated failed attempts from the same source could indicate a brute force attack and would warrant additional investigation.

A defensive response could include blocking the offending IP address through Fail2ban:

```bash
sudo fail2ban-client set sshd banip 192.168.1.45
```

The event and response would then be documented as part of the incident record.

## 8. Tools Explored in This Project

| Tool       | Purpose                                                  |
| ---------- | -------------------------------------------------------- |
| Wireshark  | Network packet capture and analysis                      |
| tcpdump    | Command line packet capture                              |
| Nmap       | Network and service discovery                            |
| iptables   | Linux firewall configuration                             |
| Fail2ban   | Automated blocking of suspicious authentication activity |
| ClamAV     | Malware scanning                                         |
| journalctl | Linux system log review                                  |
| dd         | Disk imaging                                             |
| netstat    | Network connection inspection                            |
| lsof       | Open file and network connection inspection              |

## 9. Skills Demonstrated

This project was created to develop and demonstrate familiarity with:

* Incident identification and classification
* Incident containment
* Escalation procedures
* Linux system administration
* Network traffic analysis
* Security logging and monitoring
* Evidence preservation
* System recovery
* Incident documentation
* Post incident review

## Disclaimer

ACME Athletics is a fictional organization. This repository is a simulated personal cybersecurity project and does not represent incident response work performed for an actual employer or client.
