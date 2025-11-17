# Introduction

Ce document regroupe un exemple d'appel et un exemple de réponse à l'API Bonjour Québec.

# Exemple d'appel pour l'API Bonjour Québec

API Bonjour Québec sans Client Secret :
```bash
curl --request GET --header 'X-QC-Client-Id: ********************************' --url 'https://url-noeud-final/bonjour-quebec/v1/hello'
```

API Bonjour Québec avec Client Secret :
```bash
curl --request GET --header 'X-QC-Client-Id: ********************************' --header 'X-QC-Client-Secret: ********************************' --url 'https://url-noeud-final/bonjour-quebec-client-secret/v1/hello'
```

## Exemple de réponse

```json
{
    "message": "Bonjour Québec !",
    "transid": "12345678901234567890"
}
```
