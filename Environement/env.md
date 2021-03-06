# Environement

## VSCode

Extension :

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
- Turbo console log

---

## Architecture

Exemple pour une application bien structurée

```bash
.
├── README.md
├── .gitignore
├── .eslintrc
├── client
│   ├── package.json
│   ├── README.md
│   ├── docs
│   └── public
│      ├── images
│      └── src
│           ├── css
│           │   ├── reset.css
│           │   └── styles.css
│           ├── html
│           │   └── home.html
│           └── js
│               └── main.js
└── server
    ├── package.json
    ├── .env
    ├── .env.exemple
    ├── data
    │   ├── MCD.md
    │   ├── MLD.md
    │   ├── MPD.md
    │   ├── tables.sql
    │   ├── data.sql
    │   └── sqitch
    ├── docs
    ├── logs
    │   └── 2022-logs.txt
    └── api
        ├── tests
        ├── public
        │   ├── css
        │   ├── html
        │   └── js
        ├── index.js
        └── app
            ├── controllers
            │   └── index.js
            ├── services
            │   └── index.js
            ├── models
            │   ├── index.js
            │   └── config
            │       └── dbconnect.js
            ├── middleware
            │   ├── errors
            │   │   ├── 404.js
            │   │   └── 500.js
            │   ├── helpers
            │   │   └── loggers.js
            │   ├── validation
            │   │   └── schemas
            │   └── errorHandling.js
            └── route
                └── index.js
```

Exemple pour une application monolithique

```bash
.
├── package.json
├── .env
├── .env.exemple
├── .eslintrc
├── data
│   ├── MCD.md
│   ├── MLD.md
│   ├── MPD.md
│   ├── tables.sql
│   ├── data.sql
│   └── sqitch
├── docs
├── logs
├── tests
├── index.js
└── app
    ├── controllers
    │   └── index.js
    ├── models
    │   ├── index.js
    │   └── config
    │       └── dbconnect.js
    ├── views
    │   ├── components
    │   │   └── nav.ejs
    │   ├── errors
    │   │   └── 404.pug
    │   ├── partial
    │   │   └── header.pug
    │   └── index.html
    ├── middleware
    │   ├── errors
    │   │   ├── 404.js
    │   │   └── 500.js
    │   ├── helpers
    │   │   └── loggers.js
    │   ├── validation
    │   │   └── schemas
    │   └── errorHandling.js
    └── route
        └── index.js
```

---

## Bash

```bash
# Pour se balader dans les dossiers
cd / cd .. / cd <nom-du-dossier>

# Voir ou on se situe
pwd

# Voir tout les fichiers/dossiers même les cacher
ls -a

# Voir la place disponible sur la machine
df -h

# Voir le contenu du fichier
cat <nom-du-fichier>

# Modifier un fichier en ligne de commande
sudo nano <nom-du-fichier>

# Créer un fichier
touch <nom-du-fichier>

# Créer un dossier
mkdir <nom-du-dossier>

# Récupérer toutes les mises à jour disponibles
sudo apt-get update

# Effectuer les mise a jour
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

# Permet de récuperer un repo
git clone key-ssh-du-remote

# Permet de voir les modifs depuis le dernier commit
git status

# Permet de voir tout l'historique des commit
git log

# Permet de récuperer les changements depuis le repo
git pull

# Ajouter toute les modification
git add .

# Envelopper les modification et donner un titre
git commit-m "nom-du-commit"

# Envoyer le commit sur la branche master
git push

# Envoyer le commit sur une nouvelle branche
git push --set-upstream nom-new-branch

# Envoyer une branche sur un remote precis
git push nom-remote nom-branch

# Permet de voir toute les branches et remote connectés à ce fichier
git branch -a

# Créer une nouvelle branche et se placer dessus
git checkout nom-new-branch

# Permet de changer de branche
git switch nom-branch

# Permet de voir toute les connections du dossier
git remote -v

# Premet d'ajouter une connection
git remote add nom-remote key-ssh-du-remote
```

---

## Tree

Application **Linux** qui permet d'afficher l'architecture des fichiers/dossiers

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

## REGEX

Outils sympas pour écrire des regex [ici](https://regex101.com/)

La doc [ici](https://cheatography.com/davechild/cheat-sheets/regular-expressions/)

```js
// Exemple pour vérifier une plaque d'immatriculation française
'/^((?!(SS|WW))[^IOUa-z\d@&"()!_$*€£`+=\/;?#]{2})\-((?!000)\d{3})\-((?!SS)[^IOUa-z\d@&"()!_$*€£`+=\/;?#]{2})$/'

// Pour déclarer une regex
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

// Pour limiter la chaine de caracteres
'{2,3}' // Cette chaine de caracteres aura 2 ou 3 carac
'a*' // Donne rien ou aaaaaaaaaaaaaaaaa
'a+' // Donne un a ou aaaaaaaaaaaaaaaaa
'a?' // Donne un a ou rien
'.' // Accepte autant de caracter possible

// Pour regrouper des éléments (organisation)
'((?!b)[a-d]{3})' // = acd

// Pour regrouper tout les caractères
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

## Eslint

Eslint permet d'analyser le code écrit et de corriger les potentielles erreurs de syntaxe

Doc [ici](https://eslint.org/demo)

Pour l'installer en global sur sa machine 

```bash
npm i -g eslint
```

Installer l'extension vscode eslint

Pour un fichier config de base

```json
{
    "extends": "eslint:recommended",

    "parserOptions": {
        "ecmaVersion": 2020,
        "sourceType": "module"
    },

    "env": {
        "browser": true,
        "es6": true,
        "node": true
    },

    "rules": {
        "indent": ["error", 4],
        "quotes": ["error", "double"],
        "semi": ["error", "always"],
        "camelcase": "error",
        "no-var": "error",
        "no-multi-spaces": "error",
        "no-trailing-spaces": "error"
    }
}
```

---

## TypeScript

`TypeScript` est une version de `javaScript` typé

Les navigateurs ne lisent pas Ts il faut donc compiler ces fichiers pour les transformer en Js

Doc [ici](https://www.typescriptlang.org/docs/)

### TypeScript nécessite une configuration pour être utilisé

Il fait un `package.json` spécifique

```json
{
    "scripts": {
        "build": "tsc", // npm run build pour lancer la compilation
        "start": "node dist/index.js", // npm start pour demarer le server en déploiement
        "dev": "nodemon ./index.ts" // npm run dev nodemon compile ts sans passer par build
    },
    "dependencies": {
        "express": "^4.18.1",
        "typescript": "^4.7.2"
    },
    "devDependencies": {
        "@typescript-eslint/eslint-plugin": "^5.27.0",
        "@typescript-eslint/parser": "^5.27.0",
        "@types/express": "^4.17.13",
        "nodemon": "^2.0.16",
        "ts-node": "^10.8.0"
    }
}
```

Un `.eslint.json` qui lit TypeScript

```json
{
    "env": {
        "browser": true,
        "es6": true,
        "node": true
    },
    "parserOptions": {
        "ecmaVersion": 2020,
        "sourceType": "module"
    },
    "parser": "@typescript-eslint/parser",
    "plugins": ["@typescript-eslint"],
    "extends": [
        "eslint:recommended",
        "plugin:@typescript-eslint/recommended"
    ],
    "rules": {
        "@typescript-eslint/indent": ["error", 4],
        "quotes": ["error", "double"],
        "semi": ["error", "always"],
        "no-multi-spaces": "error",
        "no-trailing-spaces": "error"
    }
}
```

Un fichier `tsconfig.json` qui permet la compilation des fichiers ts en js

```json
{
    "compilerOptions": {
        "target": "es6",
        "module": "commonjs",
        "outDir": "dist", // les fichiers compilés seront mis dans un dossier "dist"
        "sourceMap": true
    },
    "files": [
        "./index.ts", // list des fichier ts à compiler
        "./app/router.ts",
    ],
    "exclude": [
        "node_modules"
    ]
}
```

Exemple pour un server de base

```js
import * as express from "express";

const app = express();


app.get("/", (req, res) => { 

    interface ReceivedMessage {
        content: string;
        pseudo: string;
    }

    async function saveMessage(message: ReceivedMessage) {
        const savedMessage = message;
        console.log("chat", savedMessage.content);
    }

    saveMessage({ content: "to", pseudo: "to" });


    res.send("trop hype");
});


const PORT = process.env.PORT ?? 8000;
app.listen(PORT, () => {
    console.log(`server start on http://localhost:${PORT}`);
});
```

---