# Notes

Ce document est realiser via ***linux***

Les app de dev que j'utilise sont:

- VSCode
- Pour acompagner Strapi et meme lors de la creation de toute API il vaut mieux utiliser une app pour test ses routes simplement
  - insomia tres bien pour les petite API sans trop de request
  - postman bien adapter pour les plus gros projet
- DBeaver

---

## Bash

```bash
# se balader ans les dossier
cd / cd .. / cd <nom-du-dossier>

# voir ou on est
pwd

# voir tout les fichier/dossier meme les cacher
ls -a

# voir la place dispo sur la machine
df -h

# voir le contenu du fichier
cat <nom-du-fichier>

# modifier un fichier en ligne de commande
sudo nano <nom-du-fichier>

# cree un fichier
touch <nom-du-fichier>

# cree un dossier
mkdir <nom-du-dossier>

# recupere toutes les mise a jour disponible
sudo apt-get update

# effectue les mise a jour
sudo apt-get upgrade

# pour insaller une application
sudo apt-get install <nom-du-logiciel>
```

---

## Git

La doc c'est [ici](https://education.github.com/git-cheat-sheet-education.pdf)

```bash
# ajoute un .git a un dossier
git init

# permet de recuperer un repo
git clone key-ssh-du-remote

# permet de voir les modif depuis le dernier commit
git status

# permet de voir tout l'historique des commit
git log

# permet de recuperer les changement depuis le repo
git pull

# ajoute toute les modification
git add .

# enveloppe les modification et donne un titre
git commit-m "nom-du-commit"

# envoie le commit sur la branche master
git push

# envoie le commit sur une nouvelle branche
git push --set-upstream nom-new-branch

# envoie une branche sur un remote precis
git push nom-remote nom-branch

# permet de voir toute les branches et remote connecter a ce fichier
git branch -a

# cree une nouvelle branche et se place dessus
git checkout nom-new-branch

# permet de changer de branche
git switch nom-branch

# permet de voir toute les connection du dossier
git remote -v

# premet d'ajouter une connection
git remote add nom-remote key-ssh-du-remote
```

---

## Tree

Application qui permet d'afficher l'architecture des fichier/dossier

```bash
# pour intaller tree
apt-get install tree

# pour afficher l'arborescence
tree

# pour ignorer les node-module
tree -I node_modules

# exemple pour ce repo
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

                    <iframe src="#" width="200" height="200">TRUC A IMPRIMER</iframe>
                    <img src="#" alt="description"> <!-- IMAGE -->

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
/* selectionner une balise */
body {
    --color-red: red;

    display: flex;
    flex-flow: column wrap;
    align-items: center;
    justify-content: space-around;
}

/* selection par une class */
.class {
    width: 1vw;
    height: 1vh;
    font-size: 1rem;
}

/* selection par un id */
#id {
    color: var(--color-red);
}

/* selection d'un input avec une valeur precise */
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
# ajoute un fichier pakage.json qui permet de rendre les modules disponible dans l'application
npm init -y

# permet d'installer des module
npm i nom-du-module

# intalle un module dispo uniquement lors du developpement de l'app
npm i -D nom-du-module

# desinstalle un module
npm uninstall nom-du-module
```

---

## PSQL

Beaucoup d'autre option sont dispo [ici](https://docs.postgresql.fr/11/)

```sql
# se connecter a psql
sudo -u postgres psql

# liste les BDD
\l

# liste les roles
\du

# cree un nouveau role
CREATE ROLE "nom-role" WITH LOGIN PASSWORD 'mdp';

# cree une nouvelle BDD
CREATE DATABASE "nom-DB" OWNER "nom-role";

# se connecter a une BDD avec le role responsable
\c "nom-database" "nom-role"

# liste les tables
\dt

# liste les relations
\d

# cree une table
CREATE TABLE IF NOT EXISTS "nom-table" (
    "nom-champ" OPTION (INT/VARCHAR/...),
); 

# inserer des enregistrement
INSERT INTO "nom-table" ("nom-champs-1", "nom-champs-2")
VALUES ('nom-value-1', 'nom-value-2');

# chercher un enregistrement
SELECT * FROM "nom-table";

# Joindre 2 table et recupere uniquement les data lier
SELECT * FROM "table-gauche" INNER JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

# Joindre 2 table avec toutes les data de la table de gauche relier a la table de droite
SELECT * FROM "table-gauche" LEFT JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

# Meme chose mais recupere toutes les data de la table droite
SELECT * FROM "table-gauche" RIGHT JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

# Recupere toutes les data des 2 tables meme les data non lier
SELECT * FROM "table-gauche" FULL OUTER JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

# supprimer un enregistrement
DELETE FROM "nom-table" * WHERE "id" = 'enregistrement-a-supprimer';

# supprimer une table
DROP TABLE IF EXISTS "nom-table";
```

---

## MongoDB

Doc [ici](https://www.mongodb.com/developer/products/mongodb/cheat-sheet/)

MongoDB Compass MVP (trop bien trop simple trop totu)

```bash
# se connecter
mongosh

# voir toutes les db
show dbs

# entrer dans une db
use "nom-db"

# voir toutes les collection
show collections

# rename une collection
db."nom-collection".renameCollection("new-nom-collextion")

# trouver un document
db."nom-collection".find()

# trouver un document a un id
db."nom-collection".find({ id: 20 })

# trouver un document avec un morceau de nom 
db."nom-collection".find({ name: /exe/i })
# ici renvoie par exemple le document avec name = "exemple"









```

---

## Strapi

La doc [ici](https://docs.strapi.io/developer-docs/latest/developer-resources/database-apis-reference/rest-api.html#api-parameters)

```bash
# cree un role dans la BDD

npx create-strapi-app@latest "nom-du-projet"

# suivre les idication dans le terminal

npm run develop
```

---

## Docker

Bien differencier `image` et `conteneur`

Lancer une `image` creera un nouveau `conteneur`

Supprimer un `conteneur` se supprimera pas l'`image`

Une `image` est unique mais peut etre dans plusieur `conteneur`

```bash
# voir toutes les images
docker images

# pour voir les conteneur en fonctionnement
docker ps

# pour voir les conteneur qui on ete cree
docker ps -a

# recuperer tout les id des conteneur actif ou non
docker ps -aq

# installer puis lancer une image
docker run "nom-de-l'image"

# installer puis lancer une image et la supprimer des quelle a fini
docker run --rm "nom-de-l'image"

# pour exécuter une commande dans un conteneur
docker run --rm ubuntu:latest cat /etc/-os-release

# le flag "-d" pour exécuter les conteneur en tache de fond
docker run --rm -d ubuntu:latest cat /etc/-os-release

# on exécute un conteneur dans le background, avec le flag "i-", il est toujours allumé.
docker run --rm -di ubuntu:latest /bin/bash

# le flag `i` nous connecte à la machine, le flag `t` va permettre d'exécuter des commandes `bash`
docker exec -it "nom-du-conteneur" bash

# pour demarer un conteneur
docker start "nom-conteneur"

# pour arreter un conteneur
docker stop "nom-conteneur"

# supprimer une image
docker rmi "id-de-l'image"

# pour suprimer un conteneur
docker rm "conteneur-id"

# pour suprimer tout les conteneur inactif
docker rm $(docker ps -aq)

# pour suprimer tout les conteneur actif ou non
docker rm -f $(docker ps -aq)

# pour effacer tout ce qui sert à rien (ça fait un reset)
docker system prune

# Contruire une image avec un tagname jsonserver et sans le cache, pour avoir une image fraiche
docker build . --no-cache -t "nom-du-server"

#Pour exécuter notre image, en exposant le port 3000 du conteneur au port 3000 de la machine hote. Le premier 3000 est le port de l hote.
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

# une fois lancé le conteneur execute la commande ci-dessous
# elle indique que le server sera sur les port 0.0.0.0 et qu'il envera ses données sur le port 3000
ENTRYPOINT ["json-server", "--port", "3000" ,"--host", "0.0.0.0"]

# le conteneur execute par default db.json
# pour executer la copy il faut relancé le server et taper `docker run --rm -p 3000:3000 jsonserver db-copy.json`
CMD ["db.json"]
```

## React

```js





```
