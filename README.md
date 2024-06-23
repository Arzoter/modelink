# Modelink Frontend

## Description

Ce projet est une landing page pour Modelink, développée avec Next.js et conteneurisée avec Docker.

## Prérequis

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Installation

1. Clonez le dépôt :
    ```bash
    git clone <URL_DU_DEPOT>
    cd modelink
    ```

2. Créez les fichiers Docker :

    **dockerfiles/Dockerfile** :
    ```Dockerfile
    # Utiliser l'image Node officielle
    FROM node:14-alpine

    # Définir le répertoire de travail dans le conteneur
    WORKDIR /app

    # Copier package.json et package-lock.json dans le répertoire de travail
    COPY ../modelink_front/package*.json ./

    # Installer les dépendances
    RUN npm install

    # Copier le reste des fichiers de l'application
    COPY ../modelink_front .

    # Construire l'application
    RUN npm run build

    # Exposer le port utilisé par l'application
    EXPOSE 3000

    # Commande pour démarrer l'application
    CMD ["npm", "start"]
    ```

    **docker-compose.yml** :
    ```yaml
    version: '3.7'
    services:
      app:
        build:
          context: .
          dockerfile: dockerfiles/Dockerfile
        ports:
          - '3000:3000'
        volumes:
          - ./modelink_front:/app
          - /app/node_modules
        environment:
          NODE_ENV: development
    ```

## Utilisation

1. Construisez et démarrez les conteneurs Docker :
    ```bash
    docker-compose up --build
    ```

2. Accédez à l'application dans votre navigateur à l'adresse suivante :
    ```
    http://localhost:3000
    ```

## Développement

- Toutes les modifications que vous apportez dans le dossier local `modelink_front` seront automatiquement reflétées dans le conteneur Docker grâce aux volumes montés.

- Pour installer une nouvelle dépendance, utilisez la commande suivante :
    ```bash
    docker-compose run app npm install <nom_de_la_dependance>
    ```


## Contact

Pour toute question ou assistance, veuillez contacter [CLOUX Arthur](mailto:arthur.cloux@gmail.com).
