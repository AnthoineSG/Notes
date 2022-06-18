# Base De Données

## PoqtgreSQL

Utiliser [PGadmin4](https://www.pgadmin.org/)

Beaucoup d'autre option sont dispo [ici](https://docs.postgresql.fr/11/)

> Un "SGBD" permet d'acceder a une "BDD" qui contient des "Tables" "relationnel ou non" qui contiennent des "Enregistrement"

```sql
-- Se connecter a psql
sudo -u postgres psql

-- Liste les BDD
\l

-- Liste les roles
\du

-- Cree un nouveau role
CREATE ROLE "nom-role" WITH LOGIN PASSWORD 'mdp';

-- Cree une nouvelle BDD
CREATE DATABASE "nom-DB" OWNER "nom-role";

-- Se connecter a une BDD avec le role responsable
\c "nom-database" "nom-role"

-- Liste les tables
\dt

-- Liste les relations
\d

-- Cree une table
CREATE TABLE IF NOT EXISTS "nom-table" (
    "nom-champ" OPTION (INT/VARCHAR/...),
); 

-- Inserer des enregistrement
INSERT INTO "nom-table" ("nom-champs-1", "nom-champs-2")
VALUES ('nom-value-1', 'nom-value-2');

-- Chercher un enregistrement
SELECT * FROM "nom-table";

-- Joindre 2 table et recupere uniquement les data lier
SELECT * FROM "table-gauche" INNER JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Joindre 2 table avec toutes les data de la table de gauche relier a la table de droite
SELECT * FROM "table-gauche" LEFT JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Meme chose mais recupere toutes les data de la table droite
SELECT * FROM "table-gauche" RIGHT JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Recupere toutes les data des 2 tables meme les data non lier
SELECT * FROM "table-gauche" FULL OUTER JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Supprimer un enregistrement
DELETE FROM "nom-table" * WHERE "id" = 'enregistrement-a-supprimer';

-- Supprimer une table
DROP TABLE IF EXISTS "nom-table";

-- Crée un type personaliser utilisable partout dans la DB
CREATE TYPE "article" AS (
    "page" TEXT,
    "numero" INT
);

-- Crée un nouveau domaine pour verifier les info qui rentre en BDD
CREATE DOMAIN nbr_supp_zero AS INT CHECK ( VALUE > 0 );
CREATE DOMAIN text_ok AS TEXT CHECK ( VALUE ~ '^\w{5}$' );
-- Ce domain est disponible partout dans la DB
-- On peut donc faire 
ALTER TABLE "tutu" ADD COLUMN "toto" text_ok NOT NULL;
```

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
