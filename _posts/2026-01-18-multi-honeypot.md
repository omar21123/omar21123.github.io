---
title: Multi-Honeypot Platform & ELK Analysis
date: 2026-01-18 10:00:00 +0100
categories: [Cybersecurity, Network]
tags: [honeypot, elk-stack, defense, logging]
---

## Goal
Deploy and analyze decoy systems to understand attack patterns and strengthen network defense.

## Description
A comprehensive platform deploying multiple honeypots (HTTP, SSH, FTP) to attract and analyze malicious traffic.

### Key Features
- **Honeypot Deployment**: Simulated services for HTTP, SSH, and FTP.
- **Log Centralization**: Integrated with **ELK Stack (Elasticsearch, Logstash, Kibana)** for real-time log analysis and visualization.
- **System Hardening**: Secured using **AppArmor** and **Seccomp** filters.
- **Attack Analysis**: Identified and analyzed campaigns including Brute force, XSS/SQLi, and session compromise attempts.

### Technologies
- ELK Stack
- Linux Hardening (AppArmor, Seccomp)
- Python
