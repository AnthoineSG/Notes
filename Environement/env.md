# Environement

## VSCode

Extension :

- Better Comments : commentaires de couleurs
- Indent-rainbow : indentations de couleurs
- VSCode-Icons : des icons differents
- Markdown Preview Github
- Code Runner
- Database Client
- Docker
- Live Server : serveur http pour des fichier statique
- Live Share : partage de code en direct
- GitLens : suivie des commit
- Turbo console log

---

## Docker

Bien differencier `image` et `conteneur`

Lancer une `image` créera un nouveau `conteneur`

Supprimer un `conteneur` ne supprimera pas l'`image`

Une `image` est unique mais peut être dans plusieur `conteneur`

```bash
# Voir toutes les images
docker images

# Pour voir les conteneur en fonctionnement
docker ps

# Pour voir les conteneur qui on été crée
docker ps -a

# Récuperer tout les id des conteneur actifs ou non
docker ps -aq

# Installer puis lancer une image
docker run "nom-de-l'image"

# Installer puis lancer une image et la supprimer dès qu'elle a fini
docker run --rm "nom-de-l'image"

# Pour exécuter une commande dans un conteneur
docker run --rm ubuntu:latest cat /etc/-os-release

# Le flag "-d" pour exécuter les conteneur en tache de fond
docker run --rm -d ubuntu:latest cat /etc/-os-release

# On exécute un conteneur dans le background, avec le flag "i-", il est toujours allumé.
docker run --rm -di ubuntu:latest /bin/bash

# Le flag `i` nous connecte à la machine, le flag `t` va permettre d'exécuter des commandes `bash`
docker exec -it "nom-du-conteneur" bash

# Pour demarer un conteneur
docker start "nom-conteneur"

# Pour arrêter un conteneur
docker stop "nom-conteneur"

# Supprimer une image
docker rmi "id-de-l'image"

# Pour supprimer un conteneur
docker rm "conteneur-id"

# Pour supprimer tout les conteneur inactifs
docker rm $(docker ps -aq)

# Pour suprimer tout les conteneur actifs ou non
docker rm -f $(docker ps -aq)

# Pour effacer tout ce qui sert à rien (ça fait un reset)
docker system prune

# Contruire une image avec un tagname json-server et sans le cache, pour avoir une image fraîche
docker build . --no-cache -t "nom-du-server"

# Pour exécuter notre image, en exposant le port 3000 du conteneur au port 3000 de la VM hôte.
# Le premier 3000 est le port de l'hôte.
docker run --rm -p 3000:3000 "nom-du-server"
```

### Sur un fichier `Dockfile`

Ce fichier doit être accompagneé de fichiers `.json` qui comprennent les données à export sur docker

```docker
# On installe une image et on la modifie pour créer notre image custom et la rendre dispo partout grâce à docker

# Cette image contient un OS avec nodejs et npm installés
FROM node:latest

# On indique le répertoire dans lequel nous allons travailler à l'intérieur du conteneur
WORKDIR /home/server

# On dit à notre conteneur d'installer json-server globalement
RUN npm install -g json-server

# On envoie les fichiers `db.json` et `db-copy.json` sur le conteneur
COPY db.json /home/server/db.json
COPY db-copy.json /home/server/db-copy.json

# Une fois lancé le conteneur exécute la commande ci-dessous
# Elle indique que le server sera sur les ports 0.0.0.0 et qu'il enverra ses données sur le port 3000
ENTRYPOINT ["json-server", "--port", "3000" ,"--host", "0.0.0.0"]

# Le conteneur exécute par défaut db.json
# Pour exécuter la copy il faut relancer le server et taper `docker run --rm -p 3000:3000 jsonserver db-copy.json`
CMD ["db.json"]
```

---
