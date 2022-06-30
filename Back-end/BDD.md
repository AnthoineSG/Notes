# Base De Données

## PoqtgreSQL

Utiliser [PGadmin4](https://www.pgadmin.org/)

Toutes les autres options sont dispo [ici](https://www.postgresql.org/docs/current/index.html)

> Un "SGBD" permet d'acceder a une "BDD" qui contient des "Tables relationnelles ou non" qui contiennent des "Enregistrement"

### Commandes spéciales via le terminal

```bash
# Se connecter a psql
sudo -u postgres psql

# Se connecter à une BDD avec le rôle responsable
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

### Commandes disponibles via le terminal et PGAdmin

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

-- Créer un type personalisé utilisable partout dans la DB 
-- Permet d'avoir une column adress avec des sous column "postal_code" TEXT, "enter_code" INT, "city" TEXT, ...
CREATE TYPE "article" AS (
    "page" TEXT,
    "numero" INT
);

-- Crée un nouveau domaine pour vérifier les info qui rentrent en BDD (même utilisation que TEXT/INT/...)
CREATE DOMAIN nbr_supp_zero AS INT CHECK ( VALUE > 0 );
CREATE DOMAIN text_ok AS TEXT CHECK ( VALUE ~ '^\w{5}$' );
-- Ce domain est disponible partout dans la DB
-- On peut donc faire 
ALTER TABLE "tutu" ADD COLUMN "toto" text_ok NOT NULL;

-- Crée un index permet d'accélérer la vitesse de calcul de la BDD
-- Un index est placé sur une colonne
-- Il y a plusieurs types d'index :
-- => le HASH qui est utilisé pour les opérations [=]
-- => le B-TREE pour utilisé surtout pour les [< <= >= >]
-- => le BRIN qui fait tout mais est utilisé en particulier pour les très grosses bases de données
CREATE INDEX "nom-index" ON "nom-table" USING HASH ("nom-column");
```

#### Gestion des enregistrements

```sql
-- Inserer des enregistrements
INSERT INTO "nom-table"
("nom-champs-1", "nom-champs-2")
VALUES
('nom-value-1.1', 'nom-value-2.1'),
('nom-value-1.2', 'nom-value-2.2');

-- Chercher un enregistrement
SELECT * FROM "nom-table";

-- Joindre 2 tables et récuperer uniquement les data lier
SELECT * FROM "table-gauche" 
INNER JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Joindre 2 tables avec toutes les data de la table de gauche reliés à la table de droite
SELECT * FROM "table-gauche" 
LEFT JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Même chose mais récuperer toutes les data de la table de droite
SELECT * FROM "table-gauche" 
RIGHT JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Récupeérer toutes les data des 2 tables même les data non liés
SELECT * FROM "table-gauche" 
FULL OUTER JOIN "table-droite" ON "table-gauche"."table-droite-id" = "table-droite"."id";

-- Les sous-requêtes sont comme les JOIN mais récuperent uniquement les éléments de la 
-- table du premier SELECT en respectant les conditions des autres
-- Enfer à écrire mais très precis
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

-- HAVING est à utiliser avec GROUP BY et permet de grouper en suivant une certaine condition
SELECT "name", SUM("age") FROM "user" GROUP BY "name" HAVING SUM("age") > 35;

-- Supprimer un enregistrement précis
DELETE FROM "nom-table" * WHERE "id" = 'enregistrement-a-supprimer';

-- Vider une table de tous ses enregistrements
TRUNCATE TABLE "nom-table";
```

    fonction
    WITH
---

## MongoDB

Utiliser [MongoDB Compass](https://www.mongodb.com/fr-fr/products/compass)

Doc [ici](https://www.mongodb.com/developer/products/mongodb/cheat-sheet/)

Pour les aggrégations [ici](https://imgur.com/a/8hnrdOI)

MongoDB Compass MVP (trop bien, trop simple, trop totu)

> Un "SGBD" permet d'acceder a une "BDD" qui a des "collections" avec des "documents"

```bash
# Se connecter
mongosh

# Voir toutes les db
show dbs

# Entrer dans une db
use "nom-db"

# Voir toutes les collections
show collections

# Rename une collection
db."nom-collection".renameCollection("new-nom-collextion")

# Trouver un document
db."nom-collection".find()

# Trouver un document à un id
db."nom-collection".find({ id: 20 })

# Trouver un document avec un morceau de nom 
db."nom-collection".find({ name: /exe/i })
# Ici renvoie par exemple le document avec name = "exemple"

# Pour les aggregation (ALED)
db."nom-collection".aggregate([
    {
        # $match sert a rechercher des documents qui correspondent
        '$match': {
            # On récupere tout les documents qui on un type "Grass"
            'type': 'Grass',
            # On peut aussi recuperer plusieurs valeurs
            "type": {$in: ["Grass", "Poison"]},
            # On récupere tous les documents avec un nom qui contient les lettres "as"
            'name': new RegExp('as', 'i')
        }
    },
    {
        # $group permet de regrouper les valeurs sortantes
        '$group': {
            # On récupere l'id avec les value name ex = { _id: "toto" }
            '_id': '$name',
            # On récupere une valeur et on calcule sa moyenne ex = { spaw_chanve: 2 }
            'spawn_chance': {
                '$avg': '$spawn_chance'
            }
        }
    },
    {
        # $sort sert à trier les documents
        '$sort': {
            # Ici on trie de façon décroissante ( inverse = 1 )
            'spawn_chance': -1
        }
    },
    {
        # Limite simplement le nombre de documents en sortie
        '$limit': 10
    }
])
```

---
