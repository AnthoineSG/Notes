# NodeJS

## Express

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

## JSDoc

[ici](https://jsdoc.app/)

```js



```

---

## Swagger

[ici](https://swagger.io/specification/)

[la](https://www.npmjs.com/package/express-jsdoc-swagger)

[oula](https://en.wikipedia.org/wiki/OpenAPI_Specification)

```js



```

---

## Joi

[ici](https://www.npmjs.com/package/joi)

[la](https://joi.dev/api/?v=17.6.0)

```js



```

---

## 

```js



```

---