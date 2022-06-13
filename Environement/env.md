# Environement

## VSCode

Extention :

- Better Comments
- Indent-rainbow
- VSCode-Icons
- Markdown Preview Github
- Code Runner
- Database Client
- Docker
- Live Server
- Live Share
- GitLens

---

## Bash

```bash
# Pour se balader dans les dossier
cd / cd .. / cd <nom-du-dossier>

# Voir ou on ce situe
pwd

# Voir tout les fichier/dossier meme les cacher
ls -a

# Voir la place dispo sur la machine
df -h

# Voir le contenu du fichier
cat <nom-du-fichier>

# Modifier un fichier en ligne de commande
sudo nano <nom-du-fichier>

# Cree un fichier
touch <nom-du-fichier>

# Cree un dossier
mkdir <nom-du-dossier>

# Recupere toutes les mise a jour disponible
sudo apt-get update

# Effectue les mise a jour
sudo apt-get upgrade

# Pour insaller une application
sudo apt-get install <nom-du-logiciel>
```

---

## Git

La doc c'est [ici](https://education.github.com/git-cheat-sheet-education.pdf)

```bash
# Ajoute un .git a un dossier
git init

# Permet de recuperer un repo
git clone key-ssh-du-remote

# Permet de voir les modif depuis le dernier commit
git status

# Permet de voir tout l'historique des commit
git log

# Permet de recuperer les changement depuis le repo
git pull

# Ajoute toute les modification
git add .

# Enveloppe les modification et donne un titre
git commit-m "nom-du-commit"

# Envoie le commit sur la branche master
git push

# Envoie le commit sur une nouvelle branche
git push --set-upstream nom-new-branch

# Envoie une branche sur un remote precis
git push nom-remote nom-branch

# Permet de voir toute les branches et remote connecter a ce fichier
git branch -a

# Cree une nouvelle branche et se place dessus
git checkout nom-new-branch

# Permet de changer de branche
git switch nom-branch

# Permet de voir toute les connection du dossier
git remote -v

# Premet d'ajouter une connection
git remote add nom-remote key-ssh-du-remote
```

---

## Tree

Application qui permet d'afficher l'architecture des fichier/dossier

```bash
# Pour intaller tree
apt-get install tree

# Pour afficher l'arborescence
tree

# Pour ignorer les node-module
tree -I node_modules

# Exemple pour ce repo
.
└── README.md
```

---

## Docker

Bien differencier `image` et `conteneur`

Lancer une `image` creera un nouveau `conteneur`

Supprimer un `conteneur` se supprimera pas l'`image`

Une `image` est unique mais peut etre dans plusieur `conteneur`

```bash
# Voir toutes les images
docker images

# Pour voir les conteneur en fonctionnement
docker ps

# Pour voir les conteneur qui on ete cree
docker ps -a

# Recuperer tout les id des conteneur actif ou non
docker ps -aq

# Installer puis lancer une image
docker run "nom-de-l'image"

# Installer puis lancer une image et la supprimer des quelle a fini
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

# Pour arreter un conteneur
docker stop "nom-conteneur"

# Supprimer une image
docker rmi "id-de-l'image"

# Pour suprimer un conteneur
docker rm "conteneur-id"

# Pour suprimer tout les conteneur inactif
docker rm $(docker ps -aq)

# Pour suprimer tout les conteneur actif ou non
docker rm -f $(docker ps -aq)

# Pour effacer tout ce qui sert à rien (ça fait un reset)
docker system prune

# Contruire une image avec un tagname jsonserver et sans le cache, pour avoir une image fraiche
docker build . --no-cache -t "nom-du-server"

# Pour exécuter notre image, en exposant le port 3000 du conteneur au port 3000 de la VM hote.
# Le premier 3000 est le port de l'hote.
docker run --rm -p 3000:3000 "nom-du-server"
```

### Sur un fichier `Dockfile`

Ce fichier doit etre acompagner de fichier `.json` qui comprennent les donnée a export sur docker

```docker
# On installe une image et on la modifie pour créer notre image custom et la rendre dispo partout grace a docker

# Cette image contient un OS avec nodejs et npm installés
FROM node:latest

# On indique le répertoire dans lequel nous allons travailler à l'intérieur du conteneur
WORKDIR /home/server

# On dit à notre conteneur d'installer json-server globalement
RUN npm install -g json-server

# On envoie les fichier `db.json` et `db-copy.json` sur le conteneur
COPY db.json /home/server/db.json
COPY db-copy.json /home/server/db-copy.json

# Une fois lancé le conteneur execute la commande ci-dessous
# Elle indique que le server sera sur les port 0.0.0.0 et qu'il envera ses données sur le port 3000
ENTRYPOINT ["json-server", "--port", "3000" ,"--host", "0.0.0.0"]

# Le conteneur execute par default db.json
# Pour executer la copy il faut relancé le server et taper `docker run --rm -p 3000:3000 jsonserver db-copy.json`
CMD ["db.json"]
```

---

## REGEX

Outils simpas pour ecrire des regex [ici](https://regex101.com/)

La doc [ici](https://cheatography.com/davechild/cheat-sheets/regular-expressions/)

```js
// Exemple pour verifier une plaque d'immatriculation française
'/^((?!(SS|WW))[^IOUa-z\d@&"()!_$*€£`+=\/;?#]{2})\-((?!000)\d{3})\-((?!SS)[^IOUa-z\d@&"()!_$*€£`+=\/;?#]{2})$/'

// Pour declarer une regex
'^ $'

// Pour interdire quelque chose
'(?!k)' // Interdit la lettre k en minuscule
'(?!(k|L))' // Interdit la lettre k minuscule ou la lettre L majuscule

// Pour interdire plusieur choses
'[^Abc!§]'

// Pour forcer un caractere
'\-'
'\.'
'\?'

// Pour limiter la chaine de caractere
'{2,3}' // Cette chaine de caractere aura 2 ou 3 carac
'a*' // Donne rien ou aaaaaaaaaaaaaaaaa
'a+' // Donne un a ou aaaaaaaaaaaaaaaaa
'a?' // Donne un a ou rien
'.' // Accepte autant de caracter possible

// Pour regrouper des element (organisation)
'((?!b)[a-d]{3})' // = acd

// Pour regrouper tout les caractere
'[a-z]' // = a, b, c, ... , z
'[A-Z]' // = A, B, C, ... , Z
'[0-9]' // = 0, 1, 2, ... , 9
'\w' // = [a-zA-Z0-9_]
'\d' // = [0-9]

// Petits plus
'\s' // sauter une ligne
'\b' // fin d'un mots
```

---
