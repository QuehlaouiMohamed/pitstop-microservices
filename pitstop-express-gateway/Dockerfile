# Stage 1: Build
FROM node:20.13-alpine AS build

# Créer un répertoire de travail
WORKDIR /usr/src/app

# Copier package.json et package-lock.json avant les autres fichiers pour optimiser le cache
COPY package*.json ./

# Installer les dépendances
RUN npm install

# Copier le reste des fichiers de l'application
COPY . .

# Stage 2: Run
FROM node:20.13-alpine

# Définir l'environnement de production
ENV NODE_ENV=production

# Créer un utilisateur et un groupe non-root
RUN addgroup -S workgroup && adduser -S workuser -G workgroup

# Créer un répertoire de travail et donner les permissions à l'utilisateur non-root
WORKDIR /usr/src/app
RUN chown -R workuser:workgroup /usr/src/app

# Copier uniquement les fichiers nécessaires de l'étape de build
COPY --from=build /usr/src/app /usr/src/app

# Installer uniquement les dépendances nécessaires pour la production
RUN npm ci --only=production

# Changer d'utilisateur

USER workuser

# Exposer le port
EXPOSE 8080

# Commande pour démarrer l'application
CMD ["node", "server.js"]