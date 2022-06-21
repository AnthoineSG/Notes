# Back

Pour acompagner une `API` il vaut mieux utiliser une application pour tester ses routes simplement

- Insomia très bien pour les petites API sans trop de request
- Postman bien adapté pour les plus gros projets

## Strapi

La doc [ici](https://docs.strapi.io/developer-docs/latest/developer-resources/database-apis-reference/rest-api.html#api-parameters)


```bash
# Créer un rôle dans la BDD

# Commande pour créer un nouveau projet
npx create-strapi-app@latest "nom-du-projet"

# Suivre les idications dans le terminal

# Démarrer le projet
npm run develop
```

---

## Sqitch

> Install sur windows (horrible) => install `chocolatey` => install `stawberry perl` => install `sqitch`

> Install sur linux `sudo apt-get install sqitch`

Sqitch sert à `"simplifier"` la mise en place des BDD en fonction du déploiement

Il permet de lancer des scripts simples pour tout installer en BDD

```bash
# Pour installer sqitch dans un projet sous PSQL
sqitch init "nom-du-projet" --engine pg
# Cette ligne crée plusieur dossier et fichier vide

# Pour ajouter une version 
sqitch add "nom-version" -n "description de la version"
# Cette ligne crée des fichier à remplir, prioriser les noms 01-02-03-...

# Perso je préfère créer un fichier supplémentaire ex: deploy.sh pour lancer mon script
export PGUSER="user-en-BDD"
export PGPASSWORD="MDP-de-la-BDD"

sqitch deploy db:pg:"nom-BDD"
# Ou aussi => sqitch deploy db:pg:"nom-BDD" "nom-version"
# Deploy est a changer en fonction de l'action voulu deploy/revert/verify
```

---

## Ejs

Ejs est utilisé pour les applications monolithiques, il est simple à utiliser mais pas très ergonomique

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

<!-- Pour accéder a un objet -->
<%= objet.key %>
```

---
