# Processus technique de déploiement d'une définition API et produit

Processus de déploiement d'une définition API et produit dans une instance de IBM API Connect à partir de sa spécification OpenAPI 3.0.

## Étapes CI - Build et Tests
Étapes du CI :
 - Vérification de la syntaxe
 - Vérification de la définition OpenAPI 3.0
 - Vérification avec outil apic validate
 - Extraction de nom système et version SemVer
 - Création d'artefact immuable - utilisation dans les stages de déploiement CD

## Étapes CD - Déploiement
Étapes du CD (pour chaque stage d'environnement) :
 - Authentification auprès de l'API Manager
 - Extraction de nom système et version SemVer
 - Importation des définitions YAML en mode staging
 - Publication des définitions YAML sur la passerelle (gateway)
