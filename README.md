# Utilisation D'ArgoCD
Deux moyens simples de déployer avec ArgoCD

Ce TOS a pour objectif d'expliquer le fonctionnement d'ArgoCD et de présenter deux moyens différents pour déployer vos applications.

# ArgoCD : Introduction

ArgoCD est un outil de déploiement continu (CD) open source conçu pour automatiser le déploiement des applications Kubernetes. En tant que partie intégrante du paysage des outils DevOps, ArgoCD simplifie et sécurise le déploiement des applications sur des clusters Kubernetes en s'appuyant sur des définitions déclaratives stockées dans des dépôts Git.

![image](https://github.com/TheoVLT/TOS-ArgoCD/assets/148872577/d439fb3b-c256-481e-a562-1899c1723255)

## Utilité d'ArgoCD

- **Déploiement Automatisé :** ArgoCD automatise le processus de déploiement des applications sur des clusters Kubernetes, réduisant ainsi les erreurs manuelles et accélérant les déploiements.
  
- **Gestion Declarative :** Les configurations d'application sont déclarées dans des fichiers YAML et stockées dans des dépôts Git, offrant une gestion cohérente et reproductible des environnements.

- **Validation et Rollback :** ArgoCD effectue des validations en continu pour s'assurer que l'état déclaré correspond à l'état réel du cluster. En cas de problème, il permet des retours en arrière automatiques pour restaurer l'état précédent.

- **Interface Utilisateur Intuitive :** ArgoCD propose une interface utilisateur conviviale permettant de visualiser l'état des applications déployées, les différences entre l'état déclaré et l'état actuel, et de déclencher des actions manuelles si nécessaire.

- **Sécurité Renforcée :** ArgoCD intègre des fonctionnalités de sécurité telles que l'authentification basée sur les rôles (RBAC) et la prise en charge de l'intégration avec des systèmes d'authentification externes, garantissant un contrôle d'accès approprié aux ressources.

Utiliser ArgoCD simplifie le processus de déploiement et de gestion des applications sur Kubernetes, offrant ainsi une solution robuste et fiable pour les équipes DevOps.

## Comment déployer avec ArgoCD ?

Deux méthodes peuvent être utilisées :

- **Via l'interface graphique :** Il est possible de déployer directement via l'interface web d'ArgoCD. Mais en premier lieu il faudra créer une connection entre ArgoCD et le repo de l'application.

Pour ce faire, aller dans l'onglet Settings --> Repository --> Connect Repo

Il faudra alors renseigner :

- La méthode de connexion
- Le projet
- L'url du repo
- L'utilisateur de connexion au repo
- Le mot de passe lié à l'utilisateur

Le repo est connécté, nous pouvons maintenant déployer notre application !

Rendez vous dans l'onglet Applications --> New App

Renseignez les informations suivntes :

- Le nom du déploiement
- Le nom du projet
- La source du repo
- La branche sur laquelle la chart helm est stockée
- Le chemin jusqu'à la chart helm
- L'url du cluster kubernetes
- Le namespace (attention à noter le même que celui dans votre fichier !)

Créez votre application. Le déploiement va alors s'effectuer.

Vous pourrez alors accéder aux détails de l'application. Il est également possible de déployer plusieurs applications de cette manière.

- **Via l'infra as code :** Vous pouvez déployer vos applications directement depuis votre cluster kubernetes via un fichier yaml qui permettra le déploiement via ArgoCD.

Il faudra évidemment qu'une connexion soit effective entre ArgoCD et le repo afin de pouvoir permettre le déploiement. 

Pour connecter le repo à ArgoCD en CLI :
```shell
kubectl -n argocd get svc
```
On peut alors ajouter notre repo :
```shell
argocd  login  IPDUSERVICE:80
argocd  repo  add  LIEN DU REPO  --username  username  --password  password
```
