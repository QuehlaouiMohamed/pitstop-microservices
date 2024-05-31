# Utilisation d'une image de base légère et adaptée à votre application
FROM node:16-alpine

# Définition du répertoire de travail dans le conteneur
WORKDIR /app

# Copie des fichiers de configuration
COPY package.json package-lock.json ./

# Installation des dépendances
RUN npm install --production

# Copie du reste des fichiers de votre application
COPY . .

# Exposition du port sur lequel l'application écoute
EXPOSE 3000

# Définition de la commande par défaut pour démarrer votre application
CMD ["npm", "start"]
