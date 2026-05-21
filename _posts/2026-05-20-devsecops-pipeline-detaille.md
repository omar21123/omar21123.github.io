---
title: "Mise en Place d'une Chaîne DevSecOps Complète : De Git à la Production"
date: 2026-05-20 14:00:00 +0100
categories: [Project]
tags: [devops, devsecops, docker, jenkins, aws, grafana, trivy]

# Correct Chirpy Cover Image Configuration:
image:
  path: /assets/img/posts/devsecops/image.png
  alt: "DevSecOps Pipeline Architecture"
---

[cite_start]Ce projet documente en détail la conception, l'implémentation et le déploiement d'une infrastructure DevOps complète hébergeant deux applications en production : un site web vitrine pour le SecOps Club et une plateforme de compétition de cybersécurité (CTF)[cite: 100, 102]. [cite_start]L'objectif était de maîtriser les pratiques modernes d'intégration et de déploiement continus (CI/CD) en s'appuyant exclusivement sur des technologies open-source et des services cloud professionnels[cite: 101, 102].

## 1. Architecture de l'Infrastructure

[cite_start]L'architecture suit un modèle en couches permettant la séparation des responsabilités, l'isolation des services et une sécurité renforcée[cite: 124]. [cite_start]Chaque requête entrante transite par Cloudflare avant d'atteindre notre serveur AWS EC2[cite: 125].

![Diagramme d'architecture complet de l'infrastructure](architecture-diagram.jpg)
[cite_start]_Figure 1 : Vue d'ensemble du flux réseau et du pipeline de déploiement[cite: 126]._

[cite_start]Deux réseaux Docker distincts sont utilisés pour isoler les services[cite: 135]:
* [cite_start]**`secops-net` (Bridge externe) :** Permet la communication entre le gateway Nginx, le frontend React, le proxy CTFd et Jenkins[cite: 136].
* **`internal` (Bridge interne isolé) :** Sécurise la base de données MariaDB et le cache Redis, qui n'ont aucun accès direct à Internet[cite: 136, 137].

## 2. CI/CD : Automatisation avec GitHub et Jenkins

Le pipeline CI/CD de bout en bout permet des déploiements fluides[cite: 127]. Le webhook GitHub est la pièce maîtresse de l'automatisation[cite: 208]. À chaque push sur la branche `main` du dépôt, GitHub envoie une requête POST à Jenkins pour déclencher le pipeline[cite: 148, 208].

![Pipeline Jenkins déclenché automatiquement par un push GitHub](jenkins-build.jpg)
_Figure 2 : Build Jenkins déclenché automatiquement suite à un commit "Update Footer.jsx"[cite: 223, 224]._

Le pipeline Jenkins (écrit de manière déclarative en Groovy) exécute les étapes suivantes[cite: 200, 202]:
1. **Check Tools :** Vérification de l'environnement (Git, Docker, Docker Compose)[cite: 202].
2. **Deploy :** Récupération du code, build uniquement des services modifiés pour gagner du temps, et redémarrage des conteneurs cibles sans interruption de service globale[cite: 202, 303]. Le cycle complet s'exécute en moins d'une minute[cite: 226].

## 3. Sécurité (DevSecOps) avec Trivy

Dans une approche DevSecOps, la sécurité doit être intégrée directement dans le pipeline CI/CD ("shift left")[cite: 311, 313]. J'ai ajouté un stage de scan de vulnérabilités avec Trivy pour analyser automatiquement chaque image Docker construite[cite: 312].

![Rapport de scan de sécurité Trivy](trivy-scan.jpg)
_Figure 3 : Détection de 204 vulnérabilités sur une ancienne image de base Debian[cite: 318, 319, 324]._

Lors des premiers tests, Trivy a détecté 204 vulnérabilités (dont 54 critiques) liées à l'image de base Debian utilisée par Node.js[cite: 319]. La solution a consisté à migrer le Stage 1 du Dockerfile vers `node:18-alpine`, réduisant drastiquement la surface d'attaque[cite: 323].

## 4. Reverse Proxy, SSL et Déploiement

Le conteneur `secops-gateway` (Nginx) est le seul point d'entrée public[cite: 173]. Il reçoit tout le trafic HTTPS et redirige vers le bon service interne (virtual hosting)[cite: 174].

Cloudflare gère l'intégralité du DNS du domaine et génère un certificat SSL Origin spécifiquement pour chiffrer le tunnel entre Cloudflare et le serveur EC2[cite: 182, 186]. Les applications déployées sont :
* [cite_start]**Site Web SecOps Club :** Une application React compilée via un Dockerfile multi-stage (l'image finale avec Nginx ne pèse que ~25 MB)[cite: 159, 162, 229].
* [cite_start]**Plateforme CTFd :** Accessible publiquement, adossée à MariaDB et Redis pour les performances[cite: 237, 241, 242].

## 5. Observabilité : Monitoring et Alertes

[cite_start]Un pipeline de production nécessite une observabilité en temps réel[cite: 326]. J'ai déployé une stack de monitoring complète :
* [cite_start]**Node Exporter & cAdvisor :** Collectent les métriques du serveur hôte et l'I/O disque par conteneur[cite: 330, 332].
* **Prometheus & Grafana :** Stockent et visualisent les métriques[cite: 333, 334].

![Tableau de bord Grafana de l'infrastructure](grafana-dashboard.jpg)
_Figure 4 : Suivi en temps réel de la consommation CPU, RAM et I/O Disque du serveur EC2[cite: 336, 338]._

Enfin, pour garantir une réactivité rapide, un bot Telegram a été configuré[cite: 347]. Le bloc `post` du `Jenkinsfile` notifie automatiquement l'équipe en cas de succès ou d'échec d'un déploiement[cite: 354, 356].

![Notifications Telegram pour les déploiements Jenkins](telegram-bot.jpg)
_Figure 5 : Notifications en temps réel sur le canal Telegram de l'équipe[cite: 359, 360]._

## Conclusion

Ce projet a permis de concrétiser une architecture DevOps industrielle complète[cite: 366]. Les compétences clés développées incluent l'orchestration avancée avec Docker Compose, l'automatisation CI/CD avec Jenkins, la gestion des reverse proxys avec Nginx, la sécurisation des images avec Trivy, et la surveillance proactive des systèmes de production[cite: 369, 370, 371, 374, 380].