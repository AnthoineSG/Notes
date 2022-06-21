# Base De Données

## PoqtgreSQL

Utiliser [PGadmin4](https://www.pgadmin.org/)

Toutes les autres options sont dispo [ici](https://www.postgresql.org/docs/current/index.html)

> Un "SGBD" permet d'acceder a une "BDD" qui contient des "Tables relationnel ou non" qui contiennent des "Enregistrement"

### Commande special via le terminal

```bash
# Se connecter a psql
sudo -u postgres psql

# Se connecter a une BDD avec le role responsable
\c "nom-database" "nom-role"

# Liste les tables
\dt

# Liste les relations
\d

# Liste les BDD
\l

# Liste les roles
\du

# Crée un utilisateur avec logging (-l) et password (-W)
createuser "nom-user" -l -W

# Crée une DATABASE owner un user (-o ...)
createdb "nom-DB" -o "nom-user"
```

### Commandes disponible via le terminal et PGAdmin

#### Gestion de la DB

```sql
-- Crée un nouveau user === CREATE ROLE mais ROLE oblige l'option LOGIN
CREATE USER "nom-role" WITH PASSWORD 'mdp';

-- Crée une nouvelle BDD
CREATE DATABASE "nom-DB" OWNER "nom-role";

-- Crée une table
CREATE TABLE IF NOT EXISTS "nom-table" (
    "nom-champ" OPTION (INT/VARCHAR/...),
);

-- Supprimer une table
DROP TABLE IF EXISTS "nom-table";

-- Crée un type personaliser utilisable partout dans la DB 
-- Permet d'avoir une column adress avec des sous column "postal_code" TEXT, "enter_code" INT, "city" TEXT, ...
CREATE TYPE "article" AS (
    "page" TEXT,
    "numero" INT
);

-- Crée un nouveau domaine pour verifier les info qui rentre en BDD (meme utilisation que TEXT/INT/...)
CREATE DOMAIN nbr_supp_zero AS INT CHECK ( VALUE > 0 );
CREATE DOMAIN text_ok AS TEXT CHECK ( VALUE ~ '^\w{5}$' );
-- Ce domain est disponible partout dans la DB
-- On peut donc faire 
ALTER TABLE "tutu" ADD COLUMN "toto" text_ok NOT NULL;

-- Crée un index permet d'accelere la vitesse de calcule de la BDD
-- Un index est placer sur une colonne
-- Il y a plusieurs type d'index :
-- => le HASH qui est utiliser pour les operations [=]
-- => le B-TREE pour utiliser surtout pour les [< <= >= >]
-- => le BRIN qui fait tout
CREATE INDEX "nom-index" ON "nom-table" USING HASH ("nom-column");
```

#### Gestion des enregistrements

```sql
-- Inserer des enregistrement
INSERT INTO "nom-table"
("nom-champs-1", "nom-champs-2")
VALUES
('nom-value-1.1', 'nom-value-2.1'),
('nom-value-1.2', 'nom-value-2.2');

-- Chercher un enregistrement
SELECT * FROM "nom-table";

-- Joindre 2 table et recupere uniquement les data lier
SELECT * FROM "table-gauche" 
INNER JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Joindre 2 table avec toutes les data de la table de gauche relier a la table de droite
SELECT * FROM "table-gauche" 
LEFT JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Meme chose mais recupere toutes les data de la table droite
SELECT * FROM "table-gauche" 
RIGHT JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Recupere toutes les data des 2 tables meme les data non lier
SELECT * FROM "table-gauche" 
FULL OUTER JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Les sous-requetes sont comme les JOIN mais recupere uniquement les element de la 
-- table du premier SELECT en respectant les conditions des autres
-- Enfer a ecrire mais tres precis
SELECT "name"
FROM "user"
WHERE "user"."id" IN(
    SELECT "user_id"
    FROM "age"
    WHERE "age"."id" IN (
        SELECT "age_id"
        FROM "argent"
        GROUP BY "age_id"
        HAVING avg("money") > 102.5
    )
);

-- HAVING est a utiliser avec GROUP BY et permet de grouper en suivant une condition
SELECT "name", SUM("age") FROM "user" GROUP BY "name" HAVING SUM("age") > 35;

-- Supprimer un enregistrement precis
DELETE FROM "nom-table" * WHERE "id" = 'enregistrement-a-supprimer';

-- Vide une table de tous ses enregistrements
TRUNCATE TABLE "nom-table";
```

    fonction
---

## MongoDB

Utiliser [MongoDB Compass](https://www.mongodb.com/fr-fr/products/compass)

Doc [ici](https://www.mongodb.com/developer/products/mongodb/cheat-sheet/)

Pour les aggregations [ici](https://imgur.com/a/8hnrdOI)

MongoDB Compass MVP (trop bien, trop simple, trop totu)

> Un "SGBD" permet d'acceder a une "BDD" qui a des "collections" avec des "documents"

```bash
# Se connecter
mongosh

# Voir toutes les db
show dbs

# Entrer dans une db
use "nom-db"

# Voir toutes les collection
show collections

# Rename une collection
db."nom-collection".renameCollection("new-nom-collextion")

# Trouver un document
db."nom-collection".find()

# Trouver un document a un id
db."nom-collection".find({ id: 20 })

# Trouver un document avec un morceau de nom 
db."nom-collection".find({ name: /exe/i })
# Ici renvoie par exemple le document avec name = "exemple"

# Pour les aggregation (ALED)
db."nom-collection".aggregate([
    {
        # $match sert a rechercher des documents qui corresponde
        '$match': {
            # On recupere tout les documents qui on un type "Grass"
            'type': 'Grass',
            # On peut aussi recuperer plusieur valeur
            "type": {$in: ["Grass", "Poison"]},
            # On recupere tout les document avec un nom qui contient les lettres "as"
            'name': new RegExp('as', 'i')
        }
    },
    {
        # $group permet de regrouper les valeur sortante
        '$group': {
            # On recupere l'id avec les value name ex = { _id: "toto" }
            '_id': '$name',
            # On recupere une valeur et on calcule sa moyenne ex = { spaw_chanve: 2 }
            'spawn_chance': {
                '$avg': '$spawn_chance'
            }
        }
    },
    {
        # $sort sert a trier les documents
        '$sort': {
            # Ici on trie de façon décroissant ( inverse = 1 )
            'spawn_chance': -1
        }
    },
    {
        # Limite simplement le nombre de document en sortie
        '$limit': 10
    }
])
```

---
