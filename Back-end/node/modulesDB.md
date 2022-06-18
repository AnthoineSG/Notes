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

Facile, simple, efficace, mais nécessite de faire ses aggregation a la main pour obtenir les documents que l'on souhaite

Doc [ici](https://github.com/mongodb/node-mongodb-native)

```bash
# Init
npm i mongodb
```

Pour ce connecter

```js
const { MongoClient } = require("mongodb");

export async function connectDB() {
    const url = "mongodb://localhost:27017/";
    const client = new MongoClient(url);
    await client.connect();
    const db = client.db("nom-collection");
    return db;
}
```

Dans le router on peut passer la connection (pas obliger)

```js
const { connectDB } = require("./database");

router.get("/api/history", controllersFactory(db).getPixelHistory);
```

Dans un controller

```js
const { Db } require("mongodb");

function controllersFactory(db: Db) {
    return {
        async getPixelHistory(req, res) {
            const pixels = await db.collection("pixelStorage")
                .find()
                .sort({ createdAt: 1 })
                .project({ createdAt: 0, _id: 0 })
                .toArray();
            res.json(pixels);
        }
    };
}
```

---
