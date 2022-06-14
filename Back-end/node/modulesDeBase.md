# NodeJS

## NodeJS

C'est un gros truc qui permet de faire pas mal de choses

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

## Express

Facon simple de crée un server `http`

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

---

## Dotenv

Permet de paramétrer des variable d'environnement pour les rendre disponible partout dans le projet

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

Module de dev simple dedier au relancement du server a chaque save

Doc [ici](https://www.npmjs.com/package/nodemon)

```bash
# Installer nodemon 
npm i nodemon

# Lancer nodemon
npm run dev
```

```json
// Ligne a ajouter dans package.json
{
    "scripts": {
        "dev": "nodemon server.js",
    }
}
```

---

## JSDoc

Natif a js permet de commanter ses fonctions, methodes, const, ...

Doc [ici](https://jsdoc.app/)

```js
/**
 * Fonction qui fait rien de speciale
 * @param {*} req recupere les parametre dans l'url et l'affiche dans le terminal
 * @param {*} res renvoie un simple "hello"
 */
function toto(req, res) {
    /**
     * Recupere les parametre "/?name=..."
     */
    const params = req.params.name;
    console.log(params);
    res.send("hello");
}
```

---

## Swagger

Outils qui permet en quelques lignes de crée un back jolie et bien en forme (~ strapi mais c'est toi qui fait tout)

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

---

## Debug

Outils permetant de BUFFER les console.log

Permet de personnaliser ses log, d'avoir des infos supplementaire, d'avoir des couleurs, ...

Doc [ici](https://www.npmjs.com/package/debug)

```bash
# Init
npm i debug
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

// npm run dev = toto hello +0ms
```

---

## Jest

```js



```

---

## 

```js



```

---

## 

```js



```

---

## 

```js



```

---

## 

```js



```

---

## 

```js



```

---

## 

```js



```

---

## 

```js



```

---

## 

```js



```

---

## 

```js



```

---

## 

```js



```

---

## 

```js



```

---

## 

```js



```

---