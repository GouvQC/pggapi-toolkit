# Introduction

Ce document regroupe les étapes d'importation de la définition d'API Bonjour Québec (avec les versions Client Secret et WebSocket), la définition du produit associé ainsi que les étapes de configuration et de mise en place du pipeline de déploiement dans une instance de IBM API Connect en utilisant les gabarits (templates) pour Azure DevOps.

# Étapes de configuration et de mise en place

## Import des définitions dans les sources

Déposer les sources des définitions d'API et de produit dans le dossier [/src](../src) :
  - [org-acme-bonjour-quebec-api-definition.yaml](../src/org-acme-bonjour-quebec-api-definition.yaml)
  - [org-acme-bonjour-quebec-client-secret-api-definition.yaml](../src/org-acme-bonjour-quebec-client-secret-api-definition.yaml)
  - [org-acme-bonjour-quebec-websocket-api-definition.yaml](../src/org-acme-bonjour-quebec-websocket-api-definition.yaml)
  - [org-acme-bonjour-quebec-product-definition.yaml](../src/org-acme-bonjour-quebec-product-definition.yaml)
  - [org-acme-bonjour-quebec-ibm-configuration-definition.yaml](../src/org-acme-bonjour-quebec-ibm-configuration-definition.yaml)
  - [org-acme-bonjour-quebec-websocket-ibm-configuration-definition.yaml](../src/org-acme-bonjour-quebec-websocket-ibm-configuration-definition.yaml)

## Définition d'API

Exemple pour la définition d'API `org-acme-bonjour-quebec-api-definition.yaml`.
Utiliser la même logique pour les définitions d'API `org-acme-bonjour-quebec-client-secret-api-definition.yaml` et `org-acme-bonjour-quebec-websocket-api-definition.yaml`.

Mettre à jour la section `info:` :
  - compléter la `version: MAJOR.MINOR.PATCH`
  - ajouter le nom système `x-ibm-name:`
  - compléter les sections `termsOfService`, `contact`, `license`

```yaml
info:
  version: 1.0.1
  title: Définition d'API Bonjour Québec
  x-ibm-name: org-acme-bonjour-quebec-api-definition
```

Remplacer la section `servers:` avec une seule entrée correspondante au base path à utiliser :
```yaml
servers:
  - url: /bonjour-quebec/v1
```

Mettre à jour la section `ApiKeyAuth:` :
```yaml
components:
  securitySchemes:
    ApiKeyAuth:
      description: >-
        Jeton de type apiKey (clé API).
      in: header
      name: X-QC-Client-Id
      type: apiKey
      x-key-type: client_id
```

Mettre à jour la section `security:` :
```yaml
security:
  - ApiKeyAuth: []
```

Ajouter la section `x-ibm-configuration` à la fin du fichier :
```yaml
x-ibm-configuration:
  $ref: org-acme-bonjour-quebec-ibm-configuration-definition.yaml
```

## Définition de produit
Mettre à jour la section `info:` :
  - utiliser la même `version` que dans l'API
  - ajouter le nom système `name:`
  - compléter les sections `termsOfService`, `contact`, `license`

```yaml
info:
  version: 1.3.0
  title: Définition de Produit Bonjour Québec
  name: org-acme-bonjour-quebec-product-definition
```

Définir les plans et la référence vers les API :
```yaml
apis:
  org-acme-bonjour-quebec-api-definition_1.0.0:
    $ref: org-acme-bonjour-quebec-api-definition.yaml
  org-acme-bonjour-quebec-client-secret-api-definition_1.0.0:
    $ref: org-acme-bonjour-quebec-client-secret-api-definition.yaml
  org-acme-bonjour-quebec-websocket-api-definition_1.0.0:
    $ref: org-acme-bonjour-quebec-websocket-api-definition.yaml
```

## Pipeline de déploiement 

Créer le pipeline dans le dossier [/templates/pipelines](../templates/pipelines) :
  - [org-acme-bonjour-quebec-deploy-api-definition.yml](../templates/pipelines/org-acme-bonjour-quebec-deploy-api-definition.yml) utilise (extends) le gabarit (template) [pipeline-deploy-project-definitions.yml](../templates/pipelines/pipeline-deploy-project-definitions.yml)
  - ajuster le nombre des stages (environnements) `CICD_WORK_STAGES:`

```yaml
extends:
  template: /templates/pipelines/pipeline-deploy-project-definitions.yml
  parameters:
    CICD_WORK_STAGES:
      - 'op-dev'
      - 'op-acc'
```

## Environnements de déploiement dans Azure DevOps

Configurer les vérifications et les approbations (Approvals and checks) pour les environnements cibles.
  - `org-acme-env-op-dev`
  - `org-acme-env-op-acc`

## Variable de type secret dans la Library Azure DevOps

Création d'un groupe de variables `org-acme-acg-apiadmin` avec une variable de type secret `APIC_IAM_APIKEY` pour garder la clé d'authentification `apic` cible pour ce pipeline.

## Variables pour chaque environnement

Créer les fichiers de configuration contenant les variables et valeurs pour chaque environnement dans le dossier [/templates/variables](../templates/variables) :
  - [org-acme-bonjour-quebec-variables-env-op-dev.yml](../templates/variables/org-acme-bonjour-quebec-variables-env-op-dev.yml)
  - [org-acme-bonjour-quebec-variables-env-op-acc.yml](../templates/variables/org-acme-bonjour-quebec-variables-env-op-acc.yml)

## Constantes dans les catalogues d'API Manager

Il n'est pas nécessaire de configurer une propriété `org-acme-bonjour-quebec-catalog-property-backend-service` dans chaque catalogue (catalog property) avec la valeur `valeur_url_serveur_back_end` correspondante à cet environnement car cet API de démonstration s'exécute directement sur la passerelle (gateway) au lieu d'appeler un serveur backend.
