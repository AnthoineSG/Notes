# Modules

## Joi

C'est un module qui permet de vérifier que les donnée envoyées par le Front sont conformes à ce qu'on attend en Back

On crée des schemas de ce que l'on doit recevoir

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
})
  .required()
  .min(1)
  .max(4);
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

Le mdp est indéchiffrable mais il reste comparable

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
// On génère du "sel" (un nombre de caractères indéchiffrables)

const hash = await bcrypt.hash(password, salt);
// On mélange le sel et le mdp

console.log(password);
// => $2a$12$N7oprj2MWp0K6xJe5.s4t.ciFCjG0l9cJ/L4tbtqgB386cKI1Yrtq
```

---

## Dayjs

Module pour afficher la date de différente manières avec une doc **HORRIBLE**

Doc [ici](https://day.js.org/docs/en/installation/node-js)

```bash
# Init
npm i dayjs
```

```js
const dayjs = require("dayjs");

const date = dayjs().format("[Nous somme le] DD/MM/YYYY [et il est] HH:mm");

console.log(date);
// => Nous sommes le 18/06/2022 et il est 22:05
```

---

## Jest

C'est un outils qui permet de faire des tests sur tout ce qui entre et sort de l'app

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

## Faker

Module utile pour générer des données aléatoire

> Utile notamment pour populer une base de donnée

Doc [ici](https://fakerjs.dev/guide/)

```bash
# Init
npm i @faker-js/faker
```

```js
const { faker } = require("@faker-js/faker");
faker.locale = "fr";
```

```js
const animaux = {
  chat: faker.animal.cat(),
  chien: faker.animal.dog(),
  poisson: faker.animal.fish(),
};
console.log(animaux);
```

```bash
# Resultat aléatoire a chaque lancement
{ chat: 'LaPerm', chien: 'Chien courant serbe', poisson: 'Tétraodon' }
```

```js
const dates = [];

for (let i = 0; i < 4; i++) {
  dates.push(faker.date.birthdate());
}
console.log(dates);
```

```bash
# Resultat aléatoire a chaque lancement
[
  1966-09-15T06:49:42.986Z,
  1978-10-26T21:18:16.831Z,
  1970-09-11T23:10:26.033Z,
  1951-07-17T05:11:33.832Z
]
```

---

## Cron

Cron est un module qui est utiliser pour effectuer une tache precise a une heure percise

> Comme effectuer une fonction a un moment donnée

> Recupere les log a une certaine heure

> Aller fetch une donnée sur une API externe

Doc [ici](https://github.com/kelektiv/node-cron)

```bash
# Init
npm i cron
```

```js
// const CronJob = require("cron");
import { CronJob } from "cron";

const job = new CronJob(
  "* * * * * *", // On gere la frequence a la quelle la fonction va ce declancher (ici a chaque seconde)
  function () {
    // On place une fonction qui est a repeter
    const newDate = new Date();
    console.log("Every second:", newDate); // Chaque seconde affiche la date dans le terminal
  }
);
job.start();
```

---

## Multer

Multer est un module permetent de recupere les information d'un formulaire (FormData)

Doc [ici](https://www.npmjs.com/package/multer)

```bash
# Init
npm i multer
```

Bien preciser dans le formulaire : `enctype="multipart/form-data"`

```html
<form action="/toto" method="post" enctype="multipart/form-data">
  <input type="text" name="toto" placeholder="text" />
  <input type="submit" value="valider" />
</form>
```

Multer rend le `body` disponible coté back

```js
// const multer = require("multer");
import multer from "multer";
const upload = multer();
app.use(upload.none()); // A placer dans l'index server pour le rendre disponible dans toute l'app

app.post("/toto", (req, res) => {
  const toto = req.body.toto;
  res.send(`Le resultat du formulaire est : ${toto}`);
});
```

---

## Formidable

Formidable est similaire a Multer mais est plus puissant

Il permet notamment de recuperer les resultat d'un formulaire et de les interpreter en format `json`

Doc [ici](https://www.npmjs.com/package/formidable)

```bash
# Init
npm i
```

Dans le html un formulaire classique suffit

```html
<form action="/toto" method="post">
  <input type="text" name="toto" placeholder="text" />
  <input type="submit" value="valider" />
</form>
```

Formidable recupere le `body` directement sur la route

```js
// const formidable = require("formidable");
import formidable from "formidable";

app.post("/toto", (req, res) => {
  const form = formidable(); // On recupere le body sur la route POST

  form.on("field", (field, value) => {
    // Pour gerer uniquement les champs d'un formulaire
    console.log(field, value);
  });

  form.parse(req, (err, fields, files) => {
    // Pour gerer les champs et les fichiers
    if (err) {
      next(err); // On peut gere les erreurs
      return;
    }
    res.json({ fields });
  });
});
```

---
