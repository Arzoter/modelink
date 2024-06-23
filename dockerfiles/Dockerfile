# Utiliser l'image Node officielle
FROM node:14-alpine

# Définir le répertoire de travail dans le conteneur
WORKDIR ../modelink_front/app

# Copier package.json et package-lock.json dans le répertoire de travail
COPY ../modelink_front/package*.json ./

# Installer les dépendances
RUN npm install

# Copier le reste des fichiers de l'application
COPY ../modelink_front/. .

# Construire l'application
RUN npm run build

# Exposer le port utilisé par l'application
EXPOSE 3000

# Commande pour démarrer l'application
CMD ["npm", "start"]
