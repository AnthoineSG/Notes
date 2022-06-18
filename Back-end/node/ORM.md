# ORM

Les ORM sont tres pratique mais demande beaucoups de resources

Il vaut mieux les utiliser sur des petites application

## Sequelize

C'est un ORM (Mapping objet-relationnel), en gros Sequelize s'occupe de crée lui meme les requete

On lui donne des models de notre BDD une adresse de connection et des choses a requeter

Doc [ici](https://sequelize.org/api/v6/)

```bash
# Init
npm i sequelize
```

Pour ce connecter a une DB avec `sequelize` :

```js
const Sequelize = require("sequelize");

function getConnexion() {  // 
    return new Sequelize(
        "postgres://user:password@localhost/database",
        {
            define: {
                createdAt: "created_at",
                updatedAt: "updated_at",
            },
            logging: true,
        }
    );
}

module.exports = getConnexion;
```

On fait les models des table de notre DB (pas la peine d'etre aussi precis mais c'est toujours mieux quand meme) :

```js
const { Model, DataTypes, literal } = require("sequelize");
const sequelize = require("./getConnexion")();

class Product extends Model {}

Product.init(
    {
        id: {
            type: DataTypes.INTEGER,
            unique: true,
            autoIncrement: true,
            primaryKey: true,
        },
        name: {
            type: DataTypes.STRING,
            allowNull: false,
        },
        created_at: {
            type: DataTypes.DATE,
            allowNull: false,
            defaultValue: literal("CURRENT_TIMESTAMP"),
        },
        updated_at: {
            type: DataTypes.DATE,
            allowNull: true,
        }
    },
    {
        sequelize: sequelize,
        tableName: "product",
        modelName: "Product",
    }
);

module.exports = Product;
```

Puis on indique les relation entre les table :

```js
const Product = require("./product");
const User = require("./user");

Product.belongsTo(User, {
    foreignKey: "user_id",
    as: "user",
});

User.hasMany(Product, {
    foreignKey: "user_id",
    as: "products",
});

module.exports = {
    Product,
    User,
};
```

Pour l'utilliser :

```js
const { Product } = require("../models");

async function getAllProduct(req, res) {
    try {
        const allProduct = await Product.findAll();

        res.render("product", {
            products: allProduct,
        });
    } catch (err) {
        console.error(err);
    }
}

module.exports = { getAllProduct, };
```

---

## Mongoose

Mongoose est un ORM qui utilise une base de donnée MongoDB, il marche comme `sequelize` et consomme tout autant

Doc [ici](https://mongoosejs.com/docs/guide.html)

```bash
npm i mongoose
```

Pour la connection avec mongoDB

```js
mongoose.connect('mongodb://localhost:27017/nom-BDD');
```

Crée un model

```js
const mongoose = require("mongoose");

const userSchema = new mongoose.Schema({
    name: {
        type: String,
        required: true,
    },
});

const User = mongoose.model("User", userSchema);

module.exports = User;
```

Pour requeter

```js
app.get("/users", async (req, res) => {
    const users = await userModel.find({});
    try {
        res.send(users);
    } catch (error) {
        res.status(500).send(error);
    }
});
```

---
