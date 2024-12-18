# Rapport de Projet

## Qu'est-ce que nous avons fait

Nous avons réalisé les tâches suivantes pour ce projet :

1. **Création des Dockerfiles :**
   - **docs** : Nous avons créé un Dockerfile pour le projet `docs` en utilisant une build multi-étapes pour optimiser la taille de l'image.
   - **vote-api** : Nous avons créé un Dockerfile pour le projet `vote-api` en utilisant une build multi-étapes pour optimiser la taille de l'image.
   - **web-client** : Nous avons créé un Dockerfile pour le projet `web-client` en utilisant une build multi-étapes pour optimiser la taille de l'image.

2. **Configuration de Docker Compose :**
   - Nous avons créé un fichier `docker-compose.yml` pour exécuter les applications `web-client` et `vote-api` avec une base de données PostgreSQL.

3. **Tests en local :**
   - Nous avons testé les applications en local en utilisant Docker Compose avec les liens suivants :
     - `docs` : [http://localhost:8081](http://localhost:8081)
     - `web-client` : [http://localhost:3000](http://localhost:3000)
     - `vote-api` : [http://localhost:8000](http://localhost:8000)

4. **Déploiement des applications :**
   - **docs** : Nous avons déployé l'application `docs` sur Netlify.
   - **vote-api** : Nous avons déployé l'application `vote-api` sur Render en utilisant une base de données PostgreSQL hébergée sur Neon.
   - **web-client** : Nous avons déployé l'application `web-client` sur Render.

5. **Mise en place du pipeline CI/CD :**
   - Nous avons configuré un pipeline CI/CD avec GitHub Actions pour automatiser le build, les tests et le déploiement des applications.

## Comment se déploie-t-il

### Déploiement de `docs`

L'application `docs` est déployée sur Netlify. Voici les étapes pour le déploiement :
1. Connectez-vous à Netlify et créez un nouveau site à partir de Git.
2. Choisissez votre fournisseur Git et autorisez Netlify à accéder à votre dépôt.
3. Sélectionnez votre dépôt et configurez les paramètres de build :
   - **Branch to deploy** : `main`
   - **Base directory** : `docs`
   - **Build command** : `npm run build`
   - **Publish directory** : `build`
4. Cliquez sur "Deploy site". Netlify va commencer le processus de build et déployer votre site.

### Déploiement de `vote-api`

L'application `vote-api` est déployée sur Render. Voici les étapes pour le déploiement :
1. **Inscription et connexion à Neon :**
   - Allez sur Neon et inscrivez-vous ou connectez-vous à votre compte.
   - Créez un nouveau projet et une nouvelle base de données.
   - Obtenez l'URL de connexion PostgreSQL.

2. **Créer un compte Render :**
   - Si vous n'avez pas encore de compte Render, inscrivez-vous sur Render.

3. **Créer un nouveau service :**
   - Connectez-vous à votre compte Render.
   - Cliquez sur "New" et sélectionnez "Web Service".
   - Connectez votre dépôt GitHub à Render.
   - Sélectionnez le dépôt contenant votre projet `vote-api` et la branche `main`.

4. **Configurer le service :**
   - **Name** : `vote-api`
   - **Environment** : `Docker`
   - **Build Command** : Laissez vide si vous utilisez un Dockerfile.
   - **Start Command** : Laissez vide si vous utilisez un Dockerfile.
   - Ajoutez la variable d'environnement `PG_URL` avec la valeur de l'URL de connexion PostgreSQL.

5. **Configurer le Dockerfile :**
   - Render détectera automatiquement votre Dockerfile si vous en avez un à la racine de votre projet ou dans le répertoire `vote-api`.

### Déploiement de `web-client`

L'application `web-client` est déployée sur Render. Voici les étapes pour le déploiement :
1. **Créer un compte Render :**
   - Si vous n'avez pas encore de compte Render, inscrivez-vous sur Render.

2. **Créer un nouveau service :**
   - Connectez-vous à votre compte Render.
   - Cliquez sur "New" et sélectionnez "Web Service".
   - Connectez votre dépôt GitHub à Render.
   - Sélectionnez le dépôt contenant votre projet `web-client` et la branche `main`.

3. **Configurer le service :**
   - **Name** : `web-client`
   - **Environment** : `Docker`
   - **Build Command** : Laissez vide si vous utilisez un Dockerfile.
   - **Start Command** : Laissez vide si vous utilisez un Dockerfile.
   - Ajoutez les variables d'environnement suivantes :
     - `NODE_ENV` : `production`
     - `VOTE_API_BASE_URL` : `https://vote-api-eh8g.onrender.com`
     - `PORT` : `3000`

4. **Configurer le Dockerfile :**
   - Render détectera automatiquement votre Dockerfile si vous en avez un à la racine de votre projet ou dans le répertoire `web-client`.

## Liens vers les images et applications déployées

- `web-client` : [https://td-projet-final.onrender.com](https://td-projet-final.onrender.com)
- `vote-api` : [https://vote-api-eh8g.onrender.com](https://vote-api-eh8g.onrender.com)
- `docs` : [https://tpfinale.netlify.app](https://tpfinale.netlify.app)

## Comment un nouvel utilisateur devrait-il contribuer au projet

Pour contribuer à ce projet, suivez les étapes ci-dessous :

1. **Forker le dépôt :**
   - Allez sur la page du dépôt et cliquez sur le bouton "Fork" pour créer une copie du dépôt dans votre compte GitHub.

2. **Cloner le dépôt forké :**
   - Clonez le dépôt forké sur votre machine locale :
     ```sh
     git clone https://github.com/votre-utilisateur/2024-TP-FINAL-DEVOPS.git
     cd 2024-TP-FINAL-DEVOPS
     ```

3. **Créer une branche pour votre fonctionnalité :**
   - Créez une nouvelle branche pour travailler sur votre fonctionnalité :
     ```sh
     git checkout develop
     git checkout -b feature/ma-fonctionnalite
     ```

4. **Faire des modifications et committer :**
   - Faites les modifications nécessaires et commitez-les en utilisant la convention Gitmoji :
     ```sh
     git add .
     git commit -m ":sparkles: Ajouter une nouvelle fonctionnalité"
     ```

5. **Pousser les modifications et créer une Pull Request :**
   - Poussez les modifications vers votre dépôt forké :
     ```sh
     git push origin feature/ma-fonctionnalite
     ```
   - Allez sur la page de votre dépôt forké sur GitHub et créez une Pull Request vers le dépôt original.

## Problèmes rencontrés et solutions

Si nous avons rencontré des problèmes lors de la réalisation du projet, nous les décrivons ici et expliquons comment nous les avons résolus. Si nous sommes toujours bloqués sur certains points, nous expliquons ce que nous avons essayé et ce qui a échoué.

---

### Soumission du rapport

1. **Créer une branche feature pour le rapport :**
   ```sh
   git checkout develop
   git checkout -b feature/rapport