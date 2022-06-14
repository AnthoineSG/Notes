# Modules pour BDD

## PG

PG est un module utiliser pour se connecter a une BDD postgreSQL

Utile pour un datamapper et aussi pour d'autre module qui l'utilise comme Sqitch, Sequelize, ...

Doc [ici](https://node-postgres.com/)

```bash
# Init
npm i pg
```

Expemple pour envoyer un json dans un BDD postgres :

```js
const { Client } = require("pg");

const data = require("./data.json");

const client = new Client();

( async () => {
    await client.connect();

    for (const object of data) {
        const queryText = { 
            text: `INSERT INTO "public"."categories" ("name", "age") VALUES ($1, $2)`,
            values: [object.name, object.age]
        };
        await client.query(queryText);
    }

    await client.end(); // je referme le canal
})();
```

---

## Mongodb

Doc [ici](https://github.com/mongodb/node-mongodb-native)

```js



```

---