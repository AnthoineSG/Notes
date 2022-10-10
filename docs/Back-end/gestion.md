# Back

Pour acompagner une `API` il vaut mieux utiliser une application pour tester ses routes simplement

- Insomia très bien pour les petites API sans trop de request
- Postman bien adapté pour les plus gros projets

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
