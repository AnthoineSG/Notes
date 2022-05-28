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
INSERT INTO "nom-table" ("nom-champs", "nom-champs")
VALUES ('nom-value', 'nom-value');

# chercher un enregistrement
SELECT * FROM "nom-table";

# supprimer un enregistrement
DELETE FROM "nom-table" * WHERE "id" = 'enregistrement-a-supprimer';

# supprimer une table
DROP TABLE IF EXISTS "nom-table";
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

## React

```js

```
