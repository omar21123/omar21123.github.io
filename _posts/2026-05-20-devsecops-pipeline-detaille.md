---
title: "Building a Full DevSecOps Pipeline: From Git to Production"
date: 2026-05-20 14:00:00 +0100
categories: [Project]
tags: [devops, devsecops, docker, jenkins, aws, grafana, trivy]
image:
  path: /assets/img/posts/devsecops/image.png
  alt: "DevSecOps Pipeline Architecture"
---

This project documents the design, implementation, and deployment of a comprehensive DevOps infrastructure hosting two production applications: the official SecOps Club website and a cybersecurity competition platform (CTF). The objective was to master modern CI/CD practices using open-source technologies and professional cloud services.

## 1. Infrastructure Architecture
The architecture follows a layered model, ensuring separation of concerns, service isolation, and enhanced security. Incoming traffic is filtered through Cloudflare before reaching the AWS EC2 instance.

![Full Infrastructure Architecture Diagram](/assets/img/posts/devsecops/architecture-diagram.png)
*Figure 1: Overview of network traffic flow and deployment pipeline.*

Two distinct Docker networks are used to isolate services:
* **`secops-net` (External Bridge):** Enables communication between the Nginx gateway, React frontend, CTFd proxy, and Jenkins.
* **`internal` (Isolated Bridge):** Secures the MariaDB database and Redis cache, which have no direct internet access.

---

## 2. CI/CD: Automation with GitHub and Jenkins
The end-to-end CI/CD pipeline enables seamless deployments. The GitHub webhook is the core of this automation: every push to the `main` branch triggers a POST request to Jenkins to start the pipeline.

![Jenkins pipeline triggered by a GitHub push](/assets/img/posts/devsecops/jenkins-build.png)
*Figure 2: Jenkins build automatically triggered after an "Update Footer.jsx" commit.*

The Jenkins pipeline (written in declarative Groovy) executes these steps:
1. **Check Tools:** Environment verification (Git, Docker, Docker Compose).
2. **Deploy:** Source code retrieval, building only modified services to optimize time, and restarting target containers without downtime. The full cycle completes in under one minute.

---

## 3. DevSecOps with Trivy
In a DevSecOps approach, security must be integrated directly into the CI/CD pipeline ("shift left"). I added a vulnerability scanning stage using **Trivy** to automatically analyze every Docker image built.

![Trivy security scan report](/assets/img/posts/devsecops/trivy-scan.png)
*Figure 3: Detection of 204 vulnerabilities in an outdated Debian base image.*

During initial testing, Trivy detected 204 vulnerabilities (including 54 critical) linked to the Debian base image used by Node.js. The solution was to migrate the Dockerfile Stage 1 to `node:18-alpine`, drastically reducing the attack surface.

---

## 4. Reverse Proxy, SSL, and Deployment
The `secops-gateway` (Nginx) container acts as the sole public entry point. It receives all HTTPS traffic and redirects it to the appropriate internal service (virtual hosting).

Cloudflare manages the domain’s DNS and generates an Origin SSL certificate to encrypt the tunnel between Cloudflare and the EC2 server. Deployed applications include:
* **SecOps Club Website:** A React application compiled via a multi-stage Dockerfile (the final image with Nginx weighs only ~25 MB).
* **CTFd Platform:** Publicly accessible, backed by MariaDB and Redis for high performance.

---

## 5. Observability: Monitoring and Alerting
Production pipelines require real-time observability. I deployed a complete monitoring stack:
* **Node Exporter & cAdvisor:** Collects host server metrics and disk I/O per container.
* **Prometheus & Grafana:** Stores and visualizes the metrics.

![Grafana infrastructure dashboard](/assets/img/posts/devsecops/grafana-dashboard.png)
*Figure 4: Real-time monitoring of CPU, RAM, and disk I/O usage.*

Finally, to ensure rapid incident response, a **Telegram bot** was configured. The `post` block of the `Jenkinsfile` automatically notifies the team of deployment success or failure.

![Telegram notifications for Jenkins deployments](/assets/img/posts/devsecops/telegram-bot.png)
*Figure 5: Real-time notifications on the team's Telegram channel.*

---

## Conclusion
This project successfully implemented a complete industrial-grade DevOps architecture. Key skills developed include advanced orchestration with Docker Compose, CI/CD automation with Jenkins, reverse proxy management with Nginx, image hardening with Trivy, and proactive production system monitoring.