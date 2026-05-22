---
title: "Multi-Honeypot Platform with Containment & ELK Stack Analysis"
date: 2025-11-20 14:00:00 +0100
categories: [Project]
tags: [honeypot, python, docker, elk-stack, elasticsearch, kibana, flask, paramiko, cowrie, apparmor, seccomp, cybersecurity]
image:
  path: /assets/img/posts/honeypot/architecture-overview.png
  alt: "Multi-Honeypot Platform Architecture"
---



This project documents the design, implementation, and deployment of a multi-honeypot platform capable of luring attackers across three protocols (SSH, HTTP, FTP), containing compromised services at the kernel level, and centralizing all captured events in a full ELK stack for real-time analysis.

---

## 1. Architecture of the Platform
The architecture separates responsibilities into two distinct layers: the host machine running custom honeypots and a Docker Compose stack handling log ingestion.

| Port | Service |
| :--- | :--- |
| 5000 | HTTP Honeypot (Flask / E-Shop Pro) |
| 2222 | SSH Honeypot (Paramiko) |
| 2121 | FTP Honeypot |
| 2223 | Cowrie SSH/Telnet |
| 5601 | Kibana |
| 9200 | Elasticsearch |

---

## 2. HTTP E-Commerce Application
`app.py` simulates **E-Shop Pro**, an intentionally vulnerable store built with Flask.

![E-Shop Pro Homepage](/assets/img/posts/honeypot/http-homepage.png)
*Figure 2: The E-Shop Pro entry point.*

### Implemented Vulnerabilities
| Vulnerability | Severity | Impact |
| :--- | :--- | :--- |
| SQL Injection | Critical | DB dump / deletion |
| Unrestricted File Upload | Critical | RCE / malware staging |
| Stored & Reflected XSS | High | Session theft |
| Insecure Flask session | High | Account impersonation |

---

## 3. SSH & FTP Honeypots
*   **SSH (Paramiko):** Port 2222. Intercepts authentication and provides a fake shell.
*   **FTP:** Port 2121. Full dialogue support with an in-memory fake filesystem.
*   **Cowrie:** Port 2223. Interactive TTY recording.

![SSH Connection Failure](/assets/img/posts/honeypot/ssh-paramiko-connection.png)
*Figure 3: SSH connection behavior on port 2222.*

![FTP Manual Login](/assets/img/posts/honeypot/ftp-manual-connection.png)
*Figure 4: Manual FTP interaction on port 2121.*

![Cowrie Session](/assets/img/posts/honeypot/cowrie-ssh-session.png)
*Figure 5: Interactive Cowrie session on port 2223.*

---

## 4. Containment: AppArmor & Seccomp
We apply kernel-level hardening to prevent pivot attacks:
*   **AppArmor:** Limits directory access to only the project root.
*   **Seccomp:** Blacklists `execve` and `ptrace` for the HTTP service, preventing RCE-spawned shells.

---

## 5. Log Collection with ELK
![ELK Indices](/assets/img/posts/honeypot/elk-cat-indices.png)
*Figure 6: Confirmed log ingestion via `_cat/indices`.*

![Kibana Discover](/assets/img/posts/honeypot/kibana-discover.png)
*Figure 8: Live event monitoring in Kibana.*

---

## 6. Attack Campaign Highlights
We validated the platform using standard offensive techniques:

![Nmap Recon](/assets/img/posts/honeypot/nmap-scan-detailed.png)
*Figure 11: Service fingerprinting with Nmap.*

![XSS Attack](/assets/img/posts/honeypot/xss-stored.png)
*Figure 14: Stored XSS injection in the comments section.*

![Session Hijacking](/assets/img/posts/honeypot/flask-secret-bruteforce.png)
*Figure 20: Brute-forcing the Flask `secret_key` to forge admin cookies.*

---

## 7. Future Perspectives
*   **New Protocols:** Add RDP, SMB, and Redis support.
*   **Automation:** Implement automated cross-protocol correlation alerts (e.g., via Telegram).
*   **Threat Intel:** Integrate ASN and GeoIP enrichment.

---
