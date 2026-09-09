# Configuration SMTP

L'envoi des notifications utilise curl (protocole SMTP natif).

## Groupe de variables

Le pipeline charge automatiquement le groupe de variables suivant défini dans la librairie :

    group: acme-ses-smtp

Ce groupe contient les informations sensibles nécessaires à l'authentification SMTP.

Variables utilisées :

    SES_SMTP_USERNAME
    SES_SMTP_PASSWORD


## Template de configuration SMTP

Le pipeline charge automatiquement le template :

    - template: /templates/variables/smtp-config.yml

Ce template fournit les paramètres de configuration SMTP communs :

    smtp_server
    smtp_port
    mail_from

## Transmission des informations SMTP

Les informations SMTP sont automatiquement transmises aux stages de déploiement :

    CICD_SMTP_USERNAME: $(SES_SMTP_USERNAME)
    CICD_SMTP_PASSWORD: $(SES_SMTP_PASSWORD)

Aucune configuration supplémentaire n'est nécessaire lors de l'exécution du pipeline.
