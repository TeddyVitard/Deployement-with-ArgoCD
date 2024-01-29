# Utilisation D'ArgoCD
Deux moyens simples de déployer avec ArgoCD

Ce TOS a pour objectif d'expliquer le fonctionnement d'ArgoCD et de présenter deux moyens différents pour déployer vos applications.

# ArgoCD : Introduction

ArgoCD est un outil de déploiement continu (CD) open source conçu pour automatiser le déploiement des applications Kubernetes. En tant que partie intégrante du paysage des outils DevOps, ArgoCD simplifie et sécurise le déploiement des applications sur des clusters Kubernetes en s'appuyant sur des définitions déclaratives stockées dans des dépôts Git.

![ArgoCD](data:image/png;base64,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)

## Utilité d'ArgoCD

- **Déploiement Automatisé :** ArgoCD automatise le processus de déploiement des applications sur des clusters Kubernetes, réduisant ainsi les erreurs manuelles et accélérant les déploiements.
  
- **Gestion Declarative :** Les configurations d'application sont déclarées dans des fichiers YAML et stockées dans des dépôts Git, offrant une gestion cohérente et reproductible des environnements.

- **Validation et Rollback :** ArgoCD effectue des validations en continu pour s'assurer que l'état déclaré correspond à l'état réel du cluster. En cas de problème, il permet des retours en arrière automatiques pour restaurer l'état précédent.

- **Interface Utilisateur Intuitive :** ArgoCD propose une interface utilisateur conviviale permettant de visualiser l'état des applications déployées, les différences entre l'état déclaré et l'état actuel, et de déclencher des actions manuelles si nécessaire.

- **Sécurité Renforcée :** ArgoCD intègre des fonctionnalités de sécurité telles que l'authentification basée sur les rôles (RBAC) et la prise en charge de l'intégration avec des systèmes d'authentification externes, garantissant un contrôle d'accès approprié aux ressources.

Utiliser ArgoCD simplifie le processus de déploiement et de gestion des applications sur Kubernetes, offrant ainsi une solution robuste et fiable pour les équipes DevOps.

