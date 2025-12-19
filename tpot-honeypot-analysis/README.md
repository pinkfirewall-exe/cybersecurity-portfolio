# TPOT Honeypot Deployment & Attack Analysis

Real-world attack analysis using a TPOT honeynet deployed on a cloud-hosted Linux system.

# Overview
This project documents the deployment of a TPOT honeynet and the analysis of real-world cyberattacks targeting exposed SSH services. The honeypot was deployed on a cloud instance in the New York region and monitored continuously for over one month, capturing more than one million attack events.

The analysis focuses primarily on Cowrie, TPOT’s high-interaction SSH/Telnet honeypot, due to its detailed visibility into attacker behaviour, commands, and persistence techniques.

# Objectives
- Observe real-world attacker behaviour against exposed systems
- Identify brute-force, scanning, and botnet activity
- Analyse post-authentication attacker actions
- Examine malware delivery and persistence techniques


# Tools & Technologies
- TPOT Honeypot Platform
- Cowrie (SSH/Telnet honeypot)
- Elastic Stack (Elasticsearch, Kibana)
- Suricata
- Linux (Ubuntu 22.04)
- Cloud-hosted VM (DigitalOcean)


# Deployment Summary
- Cloud-hosted Linux VM deployed in the NYC region
- SSH (port 22) intentionally exposed
- TPOT installed using official deployment scripts
- System monitored continuously for over one month
- Logs collected and analysed using Kibana and Elastic queries

The New York region was intentionally selected due to its high Internet traffic volume and attractiveness to global scanning and botnet activity.


# Key Findings

# 🔐 SSH Attack Volume
- 10,000+ SSH/Telnet session connections
- Thousands of brute-force login attempts
- Multiple successful authentications
- Attacks began within minutes of deployment

# Botnet Behaviour
- Highly automated attacks from rotating global IPs
- Coordinated attack timing across regions
- Identical command sequences across multiple attackers
- Reuse of identical malware file hashes

# Post-Authentication Behaviour
Successful attackers immediately executed:
- System reconnaissance (`uname -a`, `whoami`, `hostname`)
- Environment fingerprinting
- Persistence preparation

This behaviour strongly indicates automated exploitation frameworks rather than manual intrusion.


# Malware & Persistence Analysis

# SSH Key Injection
The most common persistence method observed was the upload of malicious SSH keys to:
- `/root/.ssh/authorized_keys`
- `/home/*/.ssh/authorized_keys`

This technique allows:
- Passwordless root access
- Persistence across reboots
- Evasion of password-based monitoring

## Malware Reuse
Two recurring SHA256 hashes were observed across dozens of unrelated IPs, strongly indicating shared malware infrastructure or coordinated botnet deployment.


# Attack Patterns Observed
- Persistent low-rate credential attacks
- High-speed burst scanning activity
- IoT-focused credential attempts
- Multi-honeypot scanning consistent with Mirai-style botnets


# Key Takeaways
- Internet-exposed SSH services are attacked almost immediately
- Most attacks are fully automated
- SSH remains one of the most targeted services globally
- SSH key-based persistence is a preferred attacker technique
- Honeypots provide valuable insight into real-world threat behaviour


# Security Recommendations
- Disable password-based SSH authentication
- Enforce SSH key authentication
- Restrict SSH access by IP where possible
- Monitor `authorized_keys` for unauthorized changes
- Deploy intrusion detection and centralized logging


# Screenshots
Screenshots from Kibana dashboards and Cowrie logs are included in the `screenshots/` directory to demonstrate attack volume and behaviour patterns.
