# Back

## Strapi

La doc [ici](https://docs.strapi.io/developer-docs/latest/developer-resources/database-apis-reference/rest-api.html#api-parameters)

Pour acompagner Strapi et meme lors de la creation de toute API il vaut mieux utiliser une app pour test ses routes simplement
- Insomia tres bien pour les petite API sans trop de request
- Postman bien adapter pour les plus gros projet


```bash
# Cree un role dans la BDD

# Commande pour cree un nouveau projet
npx create-strapi-app@latest "nom-du-projet"

# Suivre les idication dans le terminal

# Demarer le projet
npm run develop
```

---

## Sqitch

> Install sur windows (horible) => install `chocolatey` => install `stawberry perl` => install `sqitch`

> Install sur linux `sudo apt-get install sqitch`

Sqitch sert a `"simplifier"` la mise en place des BDD en fonction du déploiement

Il permet de lancé des script simple pour tout installer en BDD

```bash
# Pour installer sqitch dans un projet sous PSQL
sqitch init "nom-du-projet" --engine pg
# Cette ligne crée plusieur dossier et et fichier vide

# Pour ajouter une version 
sqitch add "nom-version" -n "description de la version"
# Cette ligne crée des fichier a remplire prioriser les noms 01-02-03-...

# Perso je prefere crée un fichier supplementaire ex: deploy.sh pour lancer mon script
export PGUSER="user-en-BDD"
export PGPASSWORD="MDP-de-la-BDD"

sqitch deploy db:pg:"nom-BDD"
# Ou aussi => sqitch deploy db:pg:"nom-BDD" "nom-version"
# Deploy est a changer en fonction de l'action voulu deploy/revert/verify
```

---

## Ejs

Ejs est utiliser pour les application monolithique, il est simple a utiliser mais pas très ergonomique

La doc [ici](https://ejs.co/#docs)

```html
<!-- Pour afficher une variable -->
<%= nom-varable %>

<!-- Pour afficher un partial ou un component -->
<%- include("path/..ejs") %>

<!-- Boucler sur un tableau -->
<% array.forEach(element => { %>
    <%= element %>
<% }); %>

<!-- Pour acceder a un objet -->
<%= objet.key %>
```

---
