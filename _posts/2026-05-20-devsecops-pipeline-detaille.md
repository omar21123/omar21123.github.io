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

Ce projet documente en détail la conception, l'implémentation et le déploiement d'une infrastructure DevOps complète hébergeant deux applications en production : un site web vitrine pour le SecOps Club et une plateforme de compétition de cybersécurité (CTF). L'objectif était de maîtriser les pratiques modernes d'intégration et de déploiement continus (CI/CD) en s'appuyant exclusivement sur des technologies open-source et des services cloud professionnels.

## 1. Architecture de l'Infrastructure

L'architecture suit un modèle en couches permettant la séparation des responsabilités, l'isolation des services et une sécurité renforcée. Chaque requête entrante transite par Cloudflare avant d'atteindre notre serveur AWS EC2.

![Diagramme d'architecture complet de l'infrastructure](/assets/img/posts/devsecops/architecture-diagram.jpg)
_Figure 1 : Vue d'ensemble du flux réseau et du pipeline de déploiement._

Deux réseaux Docker distincts sont utilisés pour isoler les services:
* **`secops-net` (Bridge externe) :** Permet la communication entre le gateway Nginx, le frontend React, le proxy CTFd et Jenkins.
* **`internal` (Bridge interne isolé) :** Sécurise la base de données MariaDB et le cache Redis, qui n'ont aucun accès direct à Internet.

## 2. CI/CD : Automatisation avec GitHub et Jenkins

Le pipeline CI/CD de bout en bout permet des déploiements fluides. Le webhook GitHub est la pièce maîtresse de l'automatisation. À chaque push sur la branche `main` du dépôt, GitHub envoie une requête POST à Jenkins pour déclencher le pipeline.

![Pipeline Jenkins déclenché automatiquement par un push GitHub](/assets/img/posts/devsecops/jenkins-build.jpg)
_Figure 2 : Build Jenkins déclenché automatiquement suite à un commit "Update Footer.jsx"._

Le pipeline Jenkins (écrit de manière déclarative en Groovy) exécute les étapes suivantes :
1. **Check Tools :** Vérification de l'environnement (Git, Docker, Docker Compose).
2. **Deploy :** Récupération du code, build uniquement des services modifiés pour gagner du temps, et redémarrage des conteneurs cibles sans interruption de service globale. Le cycle complet s'exécute en moins d'une minute.

## 3. Sécurité (DevSecOps) avec Trivy

Dans une approche DevSecOps, la sécurité doit être intégrée directement dans le pipeline CI/CD ("shift left"). J'ai ajouté un stage de scan de vulnérabilités avec Trivy pour analyser automatiquement chaque image Docker construite.

![Rapport de scan de sécurité Trivy](/assets/img/posts/devsecops/trivy-scan.jpg)
_Figure 3 : Détection de 204 vulnérabilités sur une ancienne image de base Debian._

Lors des premiers tests, Trivy a détecté 204 vulnérabilités (dont 54 critiques) liées à l'image de base Debian utilisée par Node.js. La solution a consisté à migrer le Stage 1 du Dockerfile vers `node:18-alpine`, réduisant drastiquement la surface d'attaque.

## 4. Reverse Proxy, SSL et Déploiement

Le conteneur `secops-gateway` (Nginx) est le seul point d'entrée public. Il reçoit tout le trafic HTTPS et redirige vers le bon service interne (virtual hosting).

Cloudflare gère l'intégralité du DNS du domaine et génère un certificat SSL Origin spécifiquement pour chiffrer le tunnel entre Cloudflare and le serveur EC2. Les applications déployées sont :
* **Site Web SecOps Club :** Une application React compilée via un Dockerfile multi-stage (l'image finale avec Nginx ne pèse que ~25 MB).
* **Plateforme CTFd :** Accessible publiquement, adossée à MariaDB et Redis pour les performances.

## 5. Observabilité : Monitoring et Alertes

Un pipeline de production nécessite une observabilité en temps réel. J'ai déployé une stack de monitoring complète :
* **Node Exporter & cAdvisor :** Collectent les métriques du serveur hôte et l'I/O disque par conteneur.
* **Prometheus & Grafana :** Stockent et visualisent les métriques.

![Tableau de bord Grafana de l'infrastructure](/assets/img/posts/devsecops/grafana-dashboard.jpg)
_Figure 4 : Suivi en temps réel de la consommation CPU, RAM et I/O Disque du serveur EC2._

Enfin, pour garantir une réactivité rapide, un bot Telegram a été configuré. Le bloc `post` du `Jenkinsfile` notifie automatiquement l'équipe en cas de succès ou d'échec d'un déploiement.

![Notifications Telegram pour les déploiements Jenkins](/assets/img/posts/devsecops/telegram-bot.jpg)
_Figure 5 : Notifications en temps réel sur le canal Telegram de l'équipe._

## Conclusion

Ce projet a permis de concrétiser une architecture DevOps industrielle complète. Les compétences clés développées incluent l'orchestration avancée avec Docker Compose, l'automatisation CI/CD avec Jenkins, la gestion des reverse proxys avec Nginx, la sécurisation des images avec Trivy, et la surveillance proactive des systèmes de production.