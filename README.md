## 🐳 TP : Docker & Workflow Collaboratif avec GitHub Classroom
Ce projet est une assignation GitHub Classroom. L'objectif est de pratiquer le déploiement de conteneurs avec Docker, tout en apprenant à contribuer proprement à l'amélioration du sujet officiel (le dépôt du professeur).

## 📖 Le concept : Dépôt d'Assignation vs Dépôt Modèle
Dans le cadre de ce cours, nous utilisons deux types de dépôts :

Votre Dépôt d'Assignation : C'est votre copie personnelle et privée pour réaliser l'exercice.

Le Dépôt Modèle (Upstream) : C'est le dépôt original du professeur qui a servi à créer votre copie.

L'objectif collaboratif : Si vous détectez une erreur ou une amélioration possible dans ce README, vous allez apprendre à proposer une modification au professeur via une Pull Request.

## 🛠 Étape 1 : Configurer le lien avec le Dépôt Modèle (Upstream)
Pour pouvoir proposer des changements ou récupérer les mises à jour du professeur, votre ordinateur doit connaître l'adresse du dépôt d'origine.

Ouvrez votre terminal dans le dossier du projet et tapez :
```bash
# REMPLACEZ l'URL ci-dessous par l'URL du dépôt "Template" (celui du professeur)
git remote add upstream https://github.com/VOTRE_ORGANISATION/NOM_DU_REPOS_TEMPLATE.git

# Vérifiez que vous avez bien 'origin' (le vôtre) et 'upstream' (le prof)
git remote -v
```

## 🏗 Étape 2 : Travail technique (Votre Assignation)
1. Création de l'infrastructure
Dans votre dossier de projet, créez les deux fichiers suivants :

Fichier index.html :
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>TP Docker Classroom</title>
</head>
<body>
    <h1>Serveur Nginx de [Votre Nom/Prénom]</h1>
    <p>Déploiement Docker réussi via GitHub Classroom.</p>
</body>
</html>
```

Fichier docker-compose.yml :
```yaml
version: '3.8'
services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - ./index.html:/usr/share/nginx/html/index.html:ro
```

2. Validation et Sauvegarde
Lancez le service : docker-compose up -d

Vérifiez l'accès sur http://localhost:8080

Enregistrez votre travail sur votre branche principale :
```bash
git add index.html docker-compose.yml
git commit -m "feat: infrastructure docker opérationnelle"
git push origin main
```

## 📝 Étape 3 : Améliorer le sujet (README.md)
Vous allez maintenant enrichir la documentation de ce projet pour aider vos camarades.

1. **Modifier** ce fichier README.md sur votre ordinateur.
    - Tout en bas (après la checklist), créez une section intitulée **Guide de maintenance**.
    - Dans cette section, expliquer que pour arrêter les conteneurs et nettoyer les réseaux Docker, il faut utiliser la commande `docker-compose down`.

2. **Faire** un commit de cette modification sur votre branche main :
```bash
git add README.md
git commit -m "docs: ajout des consignes de maintenance"
git push origin main
```

🎓 Étape 4 : Proposer votre modification au Professeur
Comme GitHub Classroom ne crée pas un "vrai" fork, il faut forcer le lien pour proposer votre amélioration.

1. Créer une branche de contribution
On ne propose jamais une Pull Request à partir de sa branche de travail. On crée une branche propre basée sur le code du professeur.

```bash
git fetch upstream
git checkout -b contribution-readme upstream/main
git checkout main -- README.md
git add README.md
git commit -m "docs: proposition de guide de maintenance"
git push origin contribution-readme
```

2. Créer la Pull Request (Interface Web)
Pour que le bouton apparaisse, la méthode la plus fiable est de partir du dépôt du professeur :

Rendez-vous sur la page GitHub du Dépôt Modèle (celui du prof).

Cliquez sur l'onglet Pull Requests puis sur le bouton vert New Pull Request.

Cliquez sur le lien bleu "compare across forks".

Configurez les menus ainsi :

base repository : [Dépôt du Professeur] | base : main

head repository : [Votre Dépôt d'Assignation] | compare : contribution-readme

Vérifiez que seul le README.md apparaît dans les changements, puis cliquez sur Create Pull Request.

📥 Étape 5 : Récupérer les mises à jour du Professeur
Si le professeur accepte votre PR ou modifie le sujet :

Sur la page de votre dépôt GitHub, cliquez sur Sync fork puis Update branch.

En local, récupérez les changements : git pull origin main.

✅ Checklist de validation
[ ] Mon site est fonctionnel sur https://www.google.com/search?q=http://localhost:8080.

[ ] Le fichier docker-compose.yml est présent sur ma branche main.

[ ] Ma Pull Request vers le dépôt "Upstream" ne contient que les changements du README.


Guide de maintenance
Pour arrêter l'environnement Docker créé avec docker-compose up -d et nettoyer les ressources associées, il est essentiel d'utiliser la commande docker-compose down.

Rôle de la commande docker-compose down
Cette commande permet d'arrêter et de supprimer les ressources suivantes créées par votre fichier docker-compose.yml :

Arrêt des conteneurs : Elle arrête les conteneurs (ici, le conteneur web basé sur nginx) qui sont en cours d'exécution.

Suppression des conteneurs : Une fois arrêtés, les conteneurs sont supprimés.

Nettoyage des réseaux : Elle supprime le réseau par défaut créé par Docker Compose pour que les conteneurs puissent communiquer entre eux.