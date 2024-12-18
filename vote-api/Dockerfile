# Étape 1 : Build
FROM golang:1.23 AS build
WORKDIR /app

# Copie des fichiers nécessaires pour gérer les dépendances
COPY go.mod go.sum ./
RUN go mod download

# Copie du code source
COPY . .

# Compilation du binaire
RUN go build -o vote-api

# Étape 2 : Production
FROM ubuntu:22.04
WORKDIR /app

# Installer les dépendances nécessaires
RUN apt-get update && apt-get install -y \
    libc6 \
    ca-certificates

# Copier le fichier binaire depuis l'étape de build
COPY --from=build /app/vote-api /app/vote-api

# S'assurer que le fichier est exécutable
RUN chmod +x /app/vote-api

# Exposer le port de l'application
EXPOSE 8080

# Commande de démarrage
CMD ["/app/vote-api"]