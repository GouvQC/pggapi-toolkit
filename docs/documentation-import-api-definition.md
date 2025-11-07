# Introduction
Ce document regroupe les étapes d'importation et de configuration des définitions d'API et de Produit.


# Étapes de configuration
## Étapes de configuration - définition d'API
Déposer les sources des définitions d'API et de Produit dans le dossier `src`.

Formater le fichier YAML de la définition d'API avec https://editor-next.swagger.io/ :
- Importation dans l'éditeur
- Conversion YAML -> JSON
- Conversion JSON -> YAML

Remplacer les caractères `’` par `'`.

Réorganiser les sections dans l'ordre suivant pour plus de lisibilité :
```yaml
openapi: 3.0.3
info:
servers:
components:
paths:
tags:
security:
x-ibm-configuration:
```

Mettre à jour la section `info:` :
  - `version: MAJOR.MINOR.PATCH`
  - ajouter le nom système `x-ibm-name: mcn-pggapi-bonjour-quebec-api-definition`
  - compléter les sections `termsOfService`, `contact`, `license`

Remplacer la section `servers:` avec une seule entrée correspondant au base path à utiliser :
```yaml
servers:
  - url: /bonjour-quebec/v1
```

Mettre à jour la section globale `ApiKeyAuth:` :
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

Mettre à jour la section globale `security:` :
```yaml
security:
  - ApiKeyAuth: []
```

Ajouter la section `x-ibm-configuration` à la fin du fichier :
```yaml
x-ibm-configuration:
  $ref: mcn-pggapi-bonjour-quebec-ibm-configuration-definition.yaml
```
## Étapes de configuration - définition d'API avec client secret
Déposer les sources des définitions d'API et de Produit dans le dossier `src`.

Formater le fichier YAML de la définition d'API avec https://editor-next.swagger.io/ :
- Importation dans l'éditeur
- Conversion YAML -> JSON
- Conversion JSON -> YAML

Remplacer les caractères `’` par `'`.

Réorganiser les sections dans l'ordre suivant pour plus de lisibilité :
```yaml
openapi: 3.0.3
info:
servers:
components:
paths:
tags:
security:
x-ibm-configuration:
```

Mettre à jour la section `info:` :
  - `version: MAJOR.MINOR.PATCH`
  - ajouter le nom système `x-ibm-name: mcn-pggapi-bonjour-quebec-client-secret-api-definition`
  - compléter les sections `termsOfService`, `contact`, `license`

Remplacer la section `servers:` avec une seule entrée correspondant au base path à utiliser :
```yaml
servers:
  - url: /bonjour-quebec-client-secret/v1
```

Mettre à jour la section globale `ApiKeyAuth:` :
```yaml
components:
  securitySchemes:
    ApiKeyAuth:
      description: Jeton de type apiKey (clé API).
      in: header
      name: X-QC-Client-Id
      type: apiKey
      x-key-type: client_id
    ClientSecretAuth:
      description: Jeton de type client secret
      in: header
      name: X-QC-Client-Secret
      type: apiKey
      x-key-type: client_secret
```

Mettre à jour la section globale `security:` :
```yaml
security:
  - ApiKeyAuth: []
    ClientSecretAuth: []
```

Ajouter la section `x-ibm-configuration` à la fin du fichier :
```yaml
x-ibm-configuration:
  $ref: mcn-pggapi-bonjour-quebec-ibm-configuration-definition.yaml
```
## Étapes de configuration - définition d'API avec WebSocket

**Remarque :** Il faut configurer la passerelle pour accepter les connexions WebSocket afin de pouvoir consommer l'API via WebSocket.

Déposer les sources des définitions d'API et de Produit dans le dossier `src`.

Formater le fichier YAML de la définition d'API avec https://editor-next.swagger.io/ :
- Importation dans l'éditeur
- Conversion YAML -> JSON
- Conversion JSON -> YAML

Remplacer les caractères `’` par `'`.

Réorganiser les sections dans l'ordre suivant pour plus de lisibilité :
```yaml
openapi: 3.0.3
info:
servers:
components:
paths:
tags:
security:
x-ibm-configuration:
```

Mettre à jour la section `info:` :
  - `version: MAJOR.MINOR.PATCH`
  - ajouter le nom système `x-ibm-name: mcn-pggapi-bonjour-quebec-client-websocket-api-definition`
  - compléter les sections `termsOfService`, `contact`, `license`

Remplacer la section `servers:` avec une seule entrée correspondant au base path à utiliser :
```yaml
servers:
  - url: /bonjour-quebec-websocket/v1
```

Mettre à jour la section globale `ApiKeyAuth:` :
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

Mettre à jour la section globale `security:` :
```yaml
security:
  - ApiKeyAuth: []
```

Ajouter la section `x-ibm-configuration` à la fin du fichier :
```yaml
x-ibm-configuration:
  $ref: mcn-pggapi-bonjour-quebec-websocket-ibm-configuration-definition.yaml
```

## Étapes de configuration - définition de Produit
Mettre à jour la section `info:` :
  - utiliser la même `version` que dans l'API
  - ajouter le nom système `name: mcn-pggapi-bonjour-quebec-product-definition`
  - compléter les sections `termsOfService`, `contact`, `license`

Définir les plans et la référence vers l'API.

## Étapes de configuration - Pipeline
Ajouter les fichiers de configuration avec les valeurs pour chaque environnement dans `templates\variables\mcn-pggapi-bonjour-quebec-variables-env-*.yml`

## Étapes de configuration - Console IBM
Il n'est pas nécessaire de configurer une propriété `mcn-pggapi-bonjour-quebec-catalog-property-backend-service` dans chaque catalogue (catalog property) avec la valeur `valeur_url_serveur_back_end` correspondante à cet environnement car cet API de démonstration s'exécute directement sur la passerelle au lieu d'appeler un serveur backend.
