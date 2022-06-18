# Modules

## Joi

C'est un module qui permet de verifier que les donnée envoyer par le Front sont conforme a ce qu'on attend en Back

On crée des schema de ce que l'on doit recevoir

> Un Objet avec une certaine key

> Un string de 3 lettres minimum

> Un number qui est entre 200 et 250

Doc [ici](https://www.npmjs.com/package/joi) et [la](https://joi.dev/api/?v=17.6.0)

```bash
# Init
npm i joi
```

Dans un fichier `schema`

```js
const Joi = require("joi");

const schema = Joi.object({
    name: Joi.string(),
    age: Joi.number(),
}).required().min(1).max(4);
// required oblige d'avoir un objet
// min et max indique le nombre de key minimum et maximum
```

Dans le `router`

```js
const validation = require("../service/validation");
router.get("/object", validation.request, controller.getOne);
```

Dans un fichier `service`

```js
// Si j'ai quelque chose dans query, je demande une validation
request(req, res, next) {
    if (Object.keys(req.query).length > 0) {
            const { error } = schema.validate(req.query);
            if (error) {
                console.error(error);
                return;
            }
    }
    next();
},
```

---

## Bcrypt

Bcrypt est un module qui permet de chiffrer les MDP

Le mdp est indechiffrable mais il reste comparable
> $2b$10$N7mFIT2CEKw/aypZ === $2b$10$N7mFIT2CEKw/aypZ

Doc [ici](https://github.com/kelektiv/node.bcrypt.js)

```bash
# Init
npm i bcrypt
```

```js
const bcrypt = require("bcrypt");

const password = "1234azerty";

const salt = await bcrypt.genSalt(10);
// On genere du "sel" (un nombre de caracter indechiffrable)

const hash = await bcrypt.hash(password, salt);
// On mellange le sel et le mdp

console.log(password)
// => $2a$12$N7oprj2MWp0K6xJe5.s4t.ciFCjG0l9cJ/L4tbtqgB386cKI1Yrtq
```

---

## Dayjs

Module pour afficher la date de differente maniere avec une doc **HORRIBLE**

Doc [ici](https://day.js.org/docs/en/installation/node-js)

```bash
# Init
npm i dayjs
```

```js
const dayjs = require("dayjs");

const date = dayjs().format("[Nous somme le] DD/MM/YYYY [et il est] HH:mm");

console.log(date)
// => Nous somme le 18/06/2022 et il est 22:05
```

---

## Jest

C'est un outils qui permet de faire des test sur tout ce qui entre et sort de l'app

Doc [ici](https://jestjs.io/fr/docs/getting-started)

```bash
# Init
npm i -D jest
```

Dans le `package.json`

```json
{
    "scripts": {
        "test": "jest"
    }
}
```

Dans un dossier `test`

```js
const newObject = require("../app/object");

const data = require("./data.json");

describe("On verifie les elements dans le json", () => {
    it("Names list contient 'toto'", () => {
        expect(data.names).toContain("toto");
    });

    it("Verbs list", () => {
        expect(data.verbs).toContain(newObject.verb);
    });

    it("Complements list", () => {
        expect(data.complements).toContain(newObject.complement);
    });

    it("Adjectives list", () => {
        expect(data.adjectives).toContain(newObject.adjective);
    });
});
```

---
