# Envoi de courriel lors de la publication d'une nouvelle version d'un produit

## Objectif

Permettre l'envoi automatique d'un courriel aux consommateurs abonnés à un produit API Connect lorsqu'une nouvelle version de ce produit est publiée.

La fonctionnalité s'appuie sur trois tâches :

    task-apic-notification-nouvelle-version-product-generation.yml

qui génère la liste des destinataires à partir des abonnements existants dans API Connect.

    task-apic-notification-nouvelle-version-product-courriel-message.yml

qui alimente les paramètres du gabarit du courriel du répertoire /email-templates pour construire le courriel à envoyer et boucle sur la liste de destinataires.

    task-apic-send-email.yml

qui envoie les courriels préparés a l'étape précédente.

# Paramètres à ajouter au pipeline

Ajouter le paramètre suivant afin de permettre l'activation ou la désactivation de l'envoi des notifications dans votre pipeline.

    - name: CICD_SEND_NOTIFICATION
    displayName: Envoyer les notifications consommateurs
    type: boolean
    default: false

# Condition pour l'envoi des courriels

L'étape d'envoi de courriel survient selon l'état de la case à cocher.

## Notification activée (coché)

    CICD_SEND_NOTIFICATION: true

Résultat :

- Génération de la liste des destinataires.
- Envoi des courriels.
- Journalisation des destinataires sélectionnés.

## Notification désactivée (décoché)

    CICD_SEND_NOTIFICATION: false

Résultat :

- N'execute aucune des tâches plus haut
- Aucune génération de la liste des destinataires.
- Aucune notification envoyée.
- Aucun impact sur le déploiement.

# Considérations

- Les destinataires correspondent aux propriétaires des organisations consommatrices ayant au moins une application abonnée au produit peut importe la version.
- Les adresses courriel sont dédupliquées avant l'envoi.
- S'assurer que la [configuration SMTP](../docs/configuration-smtp.md) est fontionnel pour l'envoie des courriels.