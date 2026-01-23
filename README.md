# Introduction

Plateforme gouvernementale de gestion des API (PGGAPI).

Ce dépôt GIT contient la définition d'API Bonjour Québec, la définition du produit associé, le pipeline CI/CD et les fichiers de configurations nécessaires pour le déploiement et la publication de l'API Bonjour Québec dans les catalogues d'une organisation productrice d'IBM API Connect.

# Configuration et mise en place
- [Processus de déploiement d'une définition API et produit](docs/processus-deploy-ci-cd.md)
- [Importation de la définition d'API Bonjour Québec et de mise en place d'un pipeline de déploiement](docs/configuration-api-definition-pipeline-deploy.md)
- [Exemple d'utilisation de l'API Bonjour Québec](docs/exemple-utilisation-api.md)

# Version supportée et dépendances pour le fonctionnement des pipelines

Les gabarits des tâches sont développés pour la plateforme Azure DevOps Services (cloud-based) ou Azure DevOps Server (hosted). La version minimalement supportée pour la version hosted est : Azure DevOps Server 2022 Update 1 RC1.

Les agents doivent être capables d’exécuter les scripts Bash qui font partie des gabarits des tâches. Pour plus de détails et pour connaitre les prérequis sur un hôte Windows, consulter la page [Bash@3 - Tâche Bash v3 | Microsoft Learn](https://learn.microsoft.com/fr-ca/azure/devops/pipelines/tasks/reference/bash-v3?view=azure-pipelines).

Les scripts Bash utilisent les outils en ligne de commande suivants (nécessaires pour le fonctionnement des taches) :
- yq
- jq
- curl
- tee
- awk
- sed
- apic
- ibmcloud
- terraform
