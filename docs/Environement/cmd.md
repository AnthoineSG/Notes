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
