# création d'une application basique node js

# prende une image de base
FROM node:alpine

# créer un repertoire de travail
WORKDIR /app/node

# copier la liste de mes dépendances
COPY package*.json .

# installer les dépendances
RUN npm install

# Copie de mon application node js
COPY index.js .

# Ouvrir le port de mon application
EXPOSE 3333

# démarrer mon application
CMD ["npm", "start"]

# pour créer l'application Dockerfile dans le terminal. Il faut indiquer le chemin du Dockerfile ou lancer la commande en se situant dans le dossier du Dockerfile
#docker build -t node-app .
#pour lancer l'application
#docker run -d -p 3333:3333 node-app