# Commandes

## Bash

```bash
# Pour se balader dans les dossiers
cd / cd .. / cd <nom-du-dossier>

# Voir ou on se situe
pwd

# Voir tout les fichiers/dossiers même les cacher
ls -a

# Voir la place disponible sur la machine
df -h

# Voir le contenu du fichier
cat <nom-du-fichier>

# Modifier un fichier en ligne de commande
sudo nano <nom-du-fichier>

# Créer un fichier
touch <nom-du-fichier>

# Créer un dossier
mkdir <nom-du-dossier>

# Récupérer toutes les mises à jour disponibles
sudo apt-get update

# Effectuer les mise a jour
sudo apt-get upgrade

# Pour insaller une application
sudo apt-get install <nom-du-logiciel>
```

---

## Git

La doc c'est [ici](https://education.github.com/git-cheat-sheet-education.pdf)

```bash
# Ajoute un .git a un dossier
git init

# Permet de récuperer un repo
git clone key-ssh-du-remote

# Permet de voir les modifs depuis le dernier commit
git status

# Permet de voir tout l'historique des commit
git log

# Permet de récuperer les changements depuis le repo
git pull

# Ajouter toute les modification
git add .

# Envelopper les modification et donner un titre
git commit-m "nom-du-commit"

# Envoyer le commit sur la branche master
git push

# Envoyer le commit sur une nouvelle branche
git push --set-upstream nom-new-branch

# Envoyer une branche sur un remote precis
git push nom-remote nom-branch

# Permet de voir toute les branches et remote connectés à ce fichier
git branch -a

# Créer une nouvelle branche et se placer dessus
git checkout nom-new-branch

# Permet de changer de branche
git switch nom-branch

# Permet de voir toute les connections du dossier
git remote -v

# Premet d'ajouter une connection
git remote add nom-remote key-ssh-du-remote
```

---

## Tree

Application **Linux** qui permet d'afficher l'architecture des fichiers/dossiers

```bash
# Pour intaller tree
apt-get install tree

# Pour afficher l'arborescence
tree

# Pour ignorer les node-module
tree -I node_modules

# Exemple pour ce repo
.
└── README.md
```

---
