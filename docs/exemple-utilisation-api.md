# Introduction

Ce document regroupe un exemple d'appel et un exemple de réponse à l'API Bonjour Québec.

[[_TOC_]]

# Exemple d'appel

```bash
curl --request GET --header 'X-QC-Client-Id: ********************************' --url 'https://url-noeud-final/bonjour-quebec/v1/hello'
```

# Exemple de réponse

```json
{
    "message": "Bonjour Québec !",
    "transid": "12345678901234567890"
}
```
