# Notes

Ce document est realiser pour ***linux*** et ***Windows***

- **Environement**
    - [VSCode](#vscode)
    - [Bash](#bash)
    - [Git](#git)
    - [Docker](#docker)
    - [Regex](#html)
    - [Tree](#tree)
- **Front**
    - [HTML](#html)
    - [CSS](#css)
    - [JSVanilla](#js-vanilla)
    - [React](#html)
- **Back**
    - [NodeJS](#html)
        - Express
    - [Ejs](#ejs)
    - [Sqitch](#html)
    - [Strapi](#html)
        - Pour acompagner Strapi et meme lors de la creation de toute API il vaut mieux utiliser une app pour test ses routes simplement
            - Insomia tres bien pour les petite API sans trop de request
            - Postman bien adapter pour les plus gros projet
    - **BDD**
        - [PostgresQL](#html)
            - PGadmin4
        - [MongoDB](#html)
            - MongoDB Compass

---

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

## HTML

Plus d'info [ici](https://htmlcheatsheet.com/)

```html
<!DOCTYPE html>
<html lang="fr">
    <head>
        <title>TITRE DANS L'ONGLET</title>
        <link rel="stylesheet" href="style.css">
        <script src="main.js"></script>
    </head>

    <body>
        <header>
            <h1>TITRE</h1>
            <h2>SOUS-TITRE</h2>
        </header>

        <main>
            <article>
                <section>
                    <p id="" class="">TEXT</p>
                    <a href="#">LIENS</a>
                    <ul>
                        <li>LISTE</li>
                    </ul>
                    <br>
                    <strong>BOLD</strong>
                    <em>ITALIC</em>
                    <img src="#" alt="description">

                    <iframe src="#" width="200" height="200">TRUC A IMPRIMER</iframe>

                    <form action="/" method="post">
                        <fieldset>
                            <legend>NOM DU FORMULAIRE</legend>
                            <label for="">NOM DU CHAMPS</label>
                            <input type="text" id="" value="">
                            <select name="">
                                <option value="">LISTE DEROULANTE</option>
                            </select>
                        </fieldset>
                        <textarea cols="20" name="" rows="5">ZONE DE TEXT</textarea>
                        <button type="submit">VALIDATION DU FORMULAIRE</button>
                    </form>
                </section>
            </article>
        </main>

        <footer>
            <div>PAS DE VALEUR CONTEXTUEL</div>
            <span>PAS DE VALEUR CONTEXTUEL</span>
        </footer>
    </body>
</html>
```

---

## CSS

Plus d'info [ici](https://www.reveillere.fr/M2WEB/sheets/css.pdf) ou [la](https://htmlcheatsheet.com/css/)

```css
/* Selectionner une balise */
body {
    --color-red: red;

    display: flex;
    flex-flow: column wrap;
    align-items: center;
    justify-content: space-around;
}

/* Selection par une class */
.class {
    width: 1vw;
    height: 1vh;
    font-size: 1rem;
}

/* Selection par un id */
#id {
    color: var(--color-red);
}

/* Selection d'un input avec une valeur precise */
input[value="toto"] {
    background-color: antiquewhite;
}
```

---

## JS vanilla

La bible c'est la [MDN](https://developer.mozilla.org/fr/)

```js
// Les variable
const toto = true;
let tata = 10;
tata = "string";

// Les fonction
async function faiDesTruc(toto) {
    const attend = await truc;
    return attend
}
faiDesTruc(toto);

// Les array
const tableau = [1, 2, 3, 4, 5, 6];

for (const nbr of tableau) {
    console.log(nbr);
}

tableau.forEach(nbr => {
    console.log(nbr);
});

const trouver = tableau.find(nbr => nbr = 4);

const pourChaque = tableau.map(nbr => nbr / 3); // [3, 6, 9, ...]

const filtre = tableau.filter(nbr => nbr <= 2); // [1, 2]

tableau.sort(); // range le tableau par ordre alphabétique ou numerique

// Les objet
const obj = {
    key: "value",
    fonction(params) {
        return params;
    },
}
console.log(obj.fonction(toto));
```

---

## Nodejs

Facon simple de cree un server http
La doc c'est [ici](https://nodejs.org/fr/)

```js
const express = require("express");
const app = express();

app.get("/", (req, res) => {
    res.send("hello");
});

app.use("*", (req, res) => {
    res.send("404 Not Found");
});

app.listen(8080, () => {
    console.log("Server start on http://localhost:8080");
});
```

Possibiliter d'ajouter des modules de facon tres simple aussi via le terminal
La doc c'est [ici](https://www.npmjs.com/)

```bash
# Ajoute un fichier pakage.json qui permet de rendre les modules disponible dans l'application
npm init -y

# Permet d'installer des module
npm i nom-du-module

# Intalle un module dispo uniquement lors du developpement de l'app
npm i -D nom-du-module

# Desinstalle un module
npm uninstall nom-du-module
```

---

## PSQL

Beaucoup d'autre option sont dispo [ici](https://docs.postgresql.fr/11/)

> Un "SGBD" permet d'acceder a une "BDD" qui contient des "Tables" "relationnel ou non" qui contiennent des "Enregistrement"

```sql
-- Se connecter a psql
sudo -u postgres psql

-- Liste les BDD
\l

-- Liste les roles
\du

-- Cree un nouveau role
CREATE ROLE "nom-role" WITH LOGIN PASSWORD 'mdp';

-- Cree une nouvelle BDD
CREATE DATABASE "nom-DB" OWNER "nom-role";

-- Se connecter a une BDD avec le role responsable
\c "nom-database" "nom-role"

-- Liste les tables
\dt

-- Liste les relations
\d

-- Cree une table
CREATE TABLE IF NOT EXISTS "nom-table" (
    "nom-champ" OPTION (INT/VARCHAR/...),
); 

-- Inserer des enregistrement
INSERT INTO "nom-table" ("nom-champs-1", "nom-champs-2")
VALUES ('nom-value-1', 'nom-value-2');

-- Chercher un enregistrement
SELECT * FROM "nom-table";

-- Joindre 2 table et recupere uniquement les data lier
SELECT * FROM "table-gauche" INNER JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Joindre 2 table avec toutes les data de la table de gauche relier a la table de droite
SELECT * FROM "table-gauche" LEFT JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Meme chose mais recupere toutes les data de la table droite
SELECT * FROM "table-gauche" RIGHT JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Recupere toutes les data des 2 tables meme les data non lier
SELECT * FROM "table-gauche" FULL OUTER JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Supprimer un enregistrement
DELETE FROM "nom-table" * WHERE "id" = 'enregistrement-a-supprimer';

-- Supprimer une table
DROP TABLE IF EXISTS "nom-table";

-- Crée un type personaliser utilisable partout dans la DB
CREATE TYPE "article" AS (
    "page" TEXT,
    "numero" INT
);

-- Crée un nouveau domaine pour verifier les info qui rentre en BDD
CREATE DOMAIN nbr_supp_zero AS INT CHECK ( VALUE > 0 );
CREATE DOMAIN text_ok AS TEXT CHECK ( VALUE ~ '^\w{5}$' );
-- Ce domain est disponible partout dans la DB
-- On peut donc faire 
ALTER TABLE "tutu" ADD COLUMN "toto" text_ok NOT NULL;


```

---

## MongoDB

Doc [ici](https://www.mongodb.com/developer/products/mongodb/cheat-sheet/)

Pour les aggregations [ici](https://imgur.com/a/8hnrdOI)

MongoDB Compass MVP (trop bien, trop simple, trop totu)

> Un "SGBD" permet d'acceder a une "BDD" qui a des "collections" avec des "documents"

```bash
# Se connecter
mongosh

# Voir toutes les db
show dbs

# Entrer dans une db
use "nom-db"

# Voir toutes les collection
show collections

# Rename une collection
db."nom-collection".renameCollection("new-nom-collextion")

# Trouver un document
db."nom-collection".find()

# Trouver un document a un id
db."nom-collection".find({ id: 20 })

# Trouver un document avec un morceau de nom 
db."nom-collection".find({ name: /exe/i })
# Ici renvoie par exemple le document avec name = "exemple"

# Pour les aggregation (ALED)
db."nom-collection".aggregate([
    {
        # $match sert a rechercher des documents qui corresponde
        '$match': {
            # On recupere tout les documents qui on un type "Grass"
            'type': 'Grass',
            # On peut aussi recuperer plusieur valeur
            "type": {$in: ["Grass", "Poison"]},
            # On recupere tout les document avec un nom qui contient les lettres "as"
            'name': new RegExp('as', 'i')
        }
    },
    {
        # $group permet de regrouper les valeur sortante
        '$group': {
            # On recupere l'id avec les value name ex = { _id: "toto" }
            '_id': '$name',
            # On recupere une valeur et on calcule sa moyenne ex = { spaw_chanve: 2 }
            'spawn_chance': {
                '$avg': '$spawn_chance'
            }
        }
    },
    {
        # $sort sert a trier les documents
        '$sort': {
            # Ici on trie de façon décroissant ( inverse = 1 )
            'spawn_chance': -1
        }
    },
    {
        # Limite simplement le nombre de document en sortie
        '$limit': 10
    }
])
```

---

## Strapi

La doc [ici](https://docs.strapi.io/developer-docs/latest/developer-resources/database-apis-reference/rest-api.html#api-parameters)

```bash
# Cree un role dans la BDD

# Commande pour cree un nouveau projet
npx create-strapi-app@latest "nom-du-projet"

# Suivre les idication dans le terminal

# Demarer le projet
npm run develop
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

## Sqitch

> Install sur windows (horible) => install `chocolatey` => install `stawberry perl` => install `sqitch`

> Install sur linux `sudo apt-get install sqitch`

Sqitch sert a `"simplifier"` la mise en place des BDD en fonction du déploiement

Il permet de lancé des script simple pour tout installer en BDD

```bash
# Pour installer sqitch dans un projet sous PSQL
sqitch init "nom-du-projet" --engine pg
# Cette ligne crée plusieur dossier et et fichier vide

# Pour ajouter une version 
sqitch add "nom-version" -n "description de la version"
# Cette ligne crée des fichier a remplire prioriser les noms 01-02-03-...

# Perso je prefere crée un fichier supplementaire ex: deploy.sh pour lancer mon script
export PGUSER="user-en-BDD"
export PGPASSWORD="MDP-de-la-BDD"

sqitch deploy db:pg:"nom-BDD"
# Ou aussi => sqitch deploy db:pg:"nom-BDD" "nom-version"
# Deploy est a changer en fonction de l'action voulu deploy/revert/verify
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
```

---

## Ejs

Ejs est utiliser pour les application monolithique, il est simple a utiliser mais pas très ergonomique

La doc [ici](https://ejs.co/#docs)

```html
<!-- Pour afficher une variable -->
<%= nom-varable %>

<!-- Pour afficher un partial ou un component -->
<%- include("path/..ejs") %>

<!-- Boucler sur un tableau -->
<% array.forEach(element => { %>
    <%= element %>
<% }); %>

<!-- Pour acceder a un objet -->
<%= objet.key %>
```

---

## React

```js





```

---

## React

```js





```

---

## React

```js





```

---

## React

```js





```

---

## React

```js





```

---

## React

```js





```

---

## React

```js





```
