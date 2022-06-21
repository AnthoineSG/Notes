# NodeJs Modules

## NodeJS

C'est un gros truc qui permet de faire pas mal de choses

Possibilité d'ajouter des modules de façon très simple aussi via le terminal

La doc c'est [ici](https://www.npmjs.com/)

```bash
# Ajoute un fichier pakage.json qui permet de rendre les modules disponibles dans l'application
npm init -y

# Permet d'installer des modules
npm i nom-du-module

# Intaller un module dispo uniquement lors du développement de l'app
npm i -D nom-du-module

# Désinstaller un module
npm uninstall nom-du-module
```

---

## Express

Façon simple de créer un serveur `http`

La doc c'est [ici](https://nodejs.org/fr/)

```bash
npm i express
```

```js
const express = require("express");
const app = express();

app.set("views", "./app/views"); // On set les vues ejs pour qu'elles soient à la racine
app.set("view engine", "ejs"); // On dit à express d'utliliser ejs

app.use(express.static("./public")); // Les fichiesr static seront directement à la racine "/"

app.use(express.urlencoded({ extended: false })); // Urlencoded permet de se servir de req.body (tout se qui est dans l'url (?toto=tata....))

app.get("/", (req, res) => {
    res.render("homePage");
});

app.use("*", (req, res) => {
    res.send("404 Not Found");
});

app.listen(8080, () => {
    console.log("Server start on http://localhost:8080");
});
```

---

## Dotenv

Permet de paramétrer des variables d'environnement pour les rendre disponibles partout dans le projet

Doc [ici](https://www.npmjs.com/package/dotenv)

```bash
# Init
npm i dotenv
```

Dans un fichier `.env`

```env
PORT=3000
```

Dans le `index.js`

```js
require('dotenv').config();

const port = process.env.PORT ?? 5000;

console.log(port); // 3000
```

---

## Nodemon

Module de dev simple dédié au relancement du serveur à chaque save

Doc [ici](https://www.npmjs.com/package/nodemon)

```bash
# Installer nodemon 
npm i nodemon

# Lancer nodemon
npm run dev
```

Ligne a ajouter dans `package.json`

```json
{
    "scripts": {
        "dev": "nodemon server.js",
    }
}
```

---

## JSDoc

Natif à js permet de commanter ses fonctions, methodes, const, ...

Doc [ici](https://jsdoc.app/)

```js
/**
* Fonction qui fait rien de special
* @param {*} req récupere les paramètres dans l'url et l'affiche dans le terminal
* @param {*} res renvoie un simple "hello"
*/
function toto(req, res) {
    /**
    * Recupere les parametres "/?name=..."
    */
    const params = req.params.name;
    console.log(params);
    res.send("hello");
}
```

---

## Swagger

Outils qui permet en quelques lignes de crée un back jolie et bien en forme (~ strapi mais c'est toi qui fait tout)

:warning: Attention il y a beaucoup de versions npm de swagger, il faut bien faire attention à la version que l'on installe : `express-jsdoc-swagger`

C'est une [OpenAPI](https://en.wikipedia.org/wiki/OpenAPI_Specification), la doc c'est [ici](https://github.com/brikev/express-jsdoc-swagger) ou [la](https://swagger.io/specification/)

Le rendu final est plus ou moins comme [ça](https://petstore.swagger.io/)

```bash
# Init
npm i express-jsdoc-swagger
```

```js
const express = require("express");
const app = express();

const expressJSDocSwagger = require("express-jsdoc-swagger");

const options = {
    info: {
        version: "1.0.0", // version a personnaliser
        title: "nom-du-projet",
        license: {
            name: "MIT",
        },
    },
    security: {
        BasicAuth: {
            type: "http",
            scheme: "basic",
        },
    },
    swaggerUIPath: "/tata&toto", // url où se trouve la doc
    baseDir: __dirname,
    filesPattern: "./**/*.js",
};

expressJSDocSwagger(app)(options);
```

Dans le router créer une JSDoc adapté à swagger

```js
/**
* Une categories
* @typedef {Object} Categories
* @property {number} id - id
* @property {string} category - Description d'une categorie
*/

/**
* GET /api/categories
* @summary Get all categories
* @tags GET
* @return {[Category]} 200 - success response - application/json
* @return {object} 400 - Bad request response
*/
router.get("/categories", categoriesController.getAll);

/**
 * POST /api/categories/{id}
 * @summary Add one catégorie in DB
 * @tags POST
 * @return {Categories} 200 - success response - application/json
 * @return {object} 400 - Bad request response
 */
router.post("/categories/:id", categoriesController.addOne);
```

---

## Debug

Outils permetant de `BUFFER` les console.log

Permet de personnaliser ses log, d'avoir des infos supplementaires, d'avoir des couleurs, ...

Doc [ici](https://www.npmjs.com/package/debug)

```bash
# Init
npm i -D debug
```

Dans un fichier random :

```js
const debug = require("debug")("nomFichier");

function sayHello(toto) {
    debug(toto);
}

sayHello("hello");
```

Dans le `teminale` :

```bash
DEBUG='nomFichier' node toto.js
# result = toto hello +0ms
```

Ou dans le `package.json`

```json
"scripts": {
    "dev": "DEBUG='toto, nomFichier, tata' node server.js"
},
```

Resultat :

```bash
$ npm run dev

toto hello +0ms
```
---

## Session

```bash
# Init
npm i express-session
```

On set la session dans l'index du server

```js
app.use(session({ // on se sert des sessions pour appeller un cookie qui va suivre le visiteur
    secret: "le secret est secret il peut être placé dans le .env", // on mets un secret au piff
    resave: false,
    saveUninitialized: true,
    cookie: {
        secure: false, // false = http true = https
    }
}));

app.use((req, res, next) => { // on defini ce qui se trouve dans l'objet de session
    if (!req.session.idSearch) {
        req.session.idSearch = 0;
    }
    next();
});
```

---

## 

```js



```

---
