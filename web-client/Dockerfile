
FROM node:23 AS build
WORKDIR /app

COPY package*.json ./
RUN npm install --legacy-peer-deps

COPY . .
RUN npm run build

# Étape 2 : Production
FROM node:23-alpine

   
WORKDIR /app

# Copier les fichiers de la construction depuis l'étape précédente
COPY --from=build /app ./

# Exposer le port 3000 (si votre app écoute sur ce port en production)
EXPOSE 3000

# Définir la commande d'exécution du serveur Next.js en production
CMD ["npm", "start"]
