# Introduction à Docker

pour lancer un container docker, il faut utiliser la commande `docker run` suivie du nom de l'image à lancer.  
ici, on lance l'image `hello-world` qui est une image de test.  
elle n'existe pas sur notre machine, donc docker va la télécharger depuis le hub docker.  
il va ensuite créer un container à partir de cette image et lancer le programme `hello-world` à l'intérieur.  
celui-ci va afficher un message de bienvenue et se terminer.  

```bash
docker run hello-world
```

pour lancer le docker getting started, il faut utiliser la commande `docker run` suivie du nom de l'image à lancer.

```bash
# -d : lance le container en arrière plan
# -p : mappe le port 80 du container sur le port 80 de la machine
docker run -d -p 80:80 docker/getting-started
```

le dockerfile est un fichier qui permet de décrire comment construire une image docker.
il contient une liste d'instructions qui seront exécutées les unes après les autres pour construire l'image.

```dockerfile
# syntaxe d'une instruction
# INSTRUCTION arguments
```

pour construire une image à partir d'un dockerfile, il faut utiliser la commande `docker build` suivie du chemin vers le dockerfile.

commandes utiles:

```bash
docker build # construit une image à partir d'un dockerfile
docker run # lance un container
docker ps # liste les containers en cours d'exécution
docker pull # télécharge une image depuis le hub docker
docker search # recherche une image sur le hub docker
docker help # affiche l'aide
docker rm # supprime un container
docker rmi # supprime une image
docker inspect # affiche les informations d'un container ou d'une image
docker images # liste les images
docker history # affiche l'historique de construction d'une image
docker container rename # renomme un container
```

pour demarrer un serveur ngnx, il faut utiliser la commande `docker pull` suivie du nom de l'image à lancer.

```bash
docker pull nginx # télécharge l'image nginx depuis le hub docker
docker run nginx # lance un container nginx
```

creation de 3 containers nginx sans les démarrer.

```bash
docker create -p 8080:80 nginx
docker create -p 8081:80 nginx
docker create -p 8082:80 nginx
```

changer leur nom avec la commande `docker container rename` suivie du nom du container et du nouveau nom.

```bash
docker container rename <container> <new_name>
```

demarrer les 3 containers d'un coup avec la commande `docker start` suivie du nom des containers.

```bash
docker start <container1> <container2> <container3>
```

regarder l'adresse ip de chaque container, sans les autres informations, avec la commande `docker inspect` suivie du nom du container.

```bash
docker inspect --format '{{ .NetworkSettings.IPAddress }}' <container1> <container2> <container3>
```

pour arrêter un container, il faut utiliser la commande `docker stop` suivie du nom du container.

```bash
docker stop <container1> <container2> <container3>
```

pour supprimer des containers

```bash
docker rm <container1> <container2> <container3>
```

pour supprimer tous les contenairs non utilisés

```bash
docker container prune [options]
```

créer un volume avec la commande `docker volume create` suivie du nom du volume.

```bash
docker volume create <volume>
docker run -it --name Ubu2 -v monvolume:/data ubuntu # créer un container avec un volume 
docker exec -it <nom ou id du container> bash # se connecter au container
ctrl + d # quitter le container
docker volume rm <volume> # supprimer un volume
docker run -dit --name Ub3 -v /monDossierlocal:/myLocalFolder ubuntu # créer un container avec un volume associé à un dossier local. Ici, le dossier local est /monDossierlocal et il est associé au dossier /myLocalFolder du container, donc tout ce qui est créé dans /monDossierlocal sera dans /myLocalFolder du container
```

pour créer un réseau avec la commande `docker network create` suivie du nom du réseau.

```bash
docker network create --driver <DRIVER TYPE> <NETWORK NAME>
# DRIVER TYPE : bridge, overlay, macvlan, none
# NETWORK NAME : nom du réseau, au choix de l'utilisateur
```

exo: créer un réseau de type bridge, créer 2 containers ubuntu, installer dans chaque docker iputils-ping + net-tools
ping entre les 2 containers + ping google

```bash
docker network create --driver bridge my-bridge-network # créer un réseau de type bridge
docker create -it --name Ubu1 ubuntu # créer un container Ubu1
docker create -it --name Ubu2 ubuntu # créer un container Ubu2
docker inspect --format '{{ .NetworkSettings.IPAddress }}' <container> # trouver l'ip d'un container
docker exec -it Ubu1 bash # se connecter au container Ubu1
apt-get update # mettre à jour les paquets
apt-get install iputils-ping # installer iputils-ping
apt-get install net-tools # installer net-tools
ping <ip du container Ubu2> -c 5 # ping le container Ubu2
docker exec -it Ubu2 bash # se connecter au container Ubu2
apt-get update # mettre à jour les paquets
apt-get install iputils-ping # installer iputils-ping
apt-get install net-tools # installer net-tools
ping <nom du container Ubu1> -c 5 # ping le container Ubu1
ping 8.8.8.8 -c 5 # ping google
```

pour envoyer une image sur le hub docker, il faut utiliser la commande `docker push` suivie du nom de l'image à envoyer.

```bash
docker push <image>
docker push <image>:<tag> <username>/<repository>:<tag> # envoyer une image avec un tag
```

pour récupérer une image depuis le hub docker, il faut utiliser la commande `docker pull` suivie du nom de l'image à récupérer.

```bash
docker pull <image>   
docker pull <username>/<repository>:<tag> # récupérer une image avec un tag
```