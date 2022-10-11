# Git Commandes

La gestion de cette outil est tres importante car GitHub est avant tout un outil colaboratif donc un bon historique est primordial pour que :

- tout les utilisateurs puisse si retrouver facilement
- que la maintenence soit simple
- que la lecture soit agreable pour tous

---

## Mise en place

### Git config

Pour mettre en place une liaison entre Git et GitHub, la premiere etape est de configurer son environement en liant git a l'adresse mail du profil GitHub pour que les actions realiser soit associée au profils :

```bash
git config --global user.email [valid-email]
# git config --global user.email totoDu33@toto.fr
```

Dans un meme temps metre en place le nom de l'utilisateur

```bash
git config --global user.name "[firstname lastname]"
# git config --global user.name "Toto Du33”
```

On peut en plus definir des fichier que git ignorera automatiquement

> ⚠️ _Toujours penser au `.gitignore` pour les autres utilisateurs_

```bash
git config --global core.excludesfile '[file]'
# git config --global core.excludesfile '~/.gitignore'
```

### Git init

Pour relier un nouveau projet a Git ce qui crera un dossier masquer `.git` qut contiendra toutes les informations (commit, branch, historique, ...)

```bash
git init
```

## Commande de gestion de projet

### Git clone

Pour **recuperer** un repo GitHub sur la machine local, je copie le chemin jusqu'a la racine du repo

```bash
git clone [url ou SSH]
# git clone git@github.com:Toto/Toto-projet.git
```

### Git add

Cette commande permet d'**ajouter des fichier** au repo GitHub

Pour ajouter `tout` les fichier :

```bash
git add .
```

Pour ajouter `un/des` fichiers specifique

```bash
git add [my_file]
git add [my_file1] [my_file2] [...]
```

### Git commit

Apres avoir ajouter un ou plusieur fichier le commit permet de **crée un paquet** de ses fichier et d'ajouter un message de description

> Plus il y a de commit mieux c'est : l'historique GitHub est maintenu a jour

```bash
git commit –m "Description du commit"
# ou
git commit [my_file1] -m "Description du commit"
```

### Git push

Cette commande **permet d'envoyer** toute les modification local sur le repo GitHub

> habitude classique :
>
> - git add .
> - git commit -m "blabla"
> - git push

```bash
# pour cree une branch existante en local et envoyer sont contenue sur un repo GitHub
git push --set-upstream [remote] [branch]

# pour envoyer le contenue sur une branch specifique
git push [remote] [branch]

# une fois que les branch local et GitHub sont relier un simple push suffit
git push
```

### Git pull

Pour **mettre a jour sont repo** local avec toutes les modification qui on eu lieu sur GitHub

Cette commande met ajour toutes les branch et remote disponible

> - branch A et B en local
> - branch C sur GitHub
> - git pull
>   - branch A, B et C disponible en local
>
> Cette operation est a faire tres frequament quand on travaille en groupe sur un meme repo pour ne pas avoir des difference d'historique (a combiner avec une bonne utilisation des branches)

```bash
git pull

# ou vers un autre remote
git pull [remote]
```

### Git branch

Les branch permette de separrer le travaille effectuer et donc mieux s'**oganiser**

> - branch **A** je fais des truc
> - je crée une branch **B** depuis la branch **A**
> - je casse tout sur la branch **B**
>   - je me replace sur la branch **A**
>   - et je suppime la branch **B**
> - la branch **A** est rester intacte

Pour `voir` toutes les branch

```bash
# Les branch en local
git branch

# Toutes les branch et remotes relier
git branch -a
```

Pour `crée` une nouvelle branch a partire de la branch actuel

```bash
git branch [nom_branche]
# Donc a l'initaition branch A === branch B
```

Pour `supprimer` une branch

```bash
git branch –d [nom_branche]

# -D pour la supprimer de force
git branch -D [nom_branche]
```

### Git checkout

Comme la commande `git branch` cette commande permet une gestion des branch legerement diferente

Pour `cree` une nouvelle branche

```bash
git checkout [nom_branche]

```

Pour `cree` une nouvelle branche et ce **placer dessus** directment

```bash
git checkout -b [nom_branche]
```

### Recap des branches Git

Personnelement j'ai pour habitude de separer les commande en fonction de ce que je veux faire

```bash
# voir toutes les branch et remotes
git branch -a

# crée et se placer sur une nouvelle branch
git checkout -b [nom_branch]

# changer de branch
git switch [nom_branch]

# supprimer une branch
git branch -d [nom_branch]

# merge sur GitHub directement
```

### Git merge

Cette operation permet de **fusionner** une branche sur une branche active

⚠️ _Cette operation a reliser de preference sur GitHub directement pour des raison de lisibiliter et d'historique plus claire_

> branch B est a merge sur branch A
>
> - placement sur branch A
> - git merge branch B
>
> branch A === branch A + branch B

```bash
git merge [branch]
```

### Git remote

Commande permetant d'**ajouter une connexion** a un repo distant

`Voir` toutes les connexion

```bash
git remote –v
```

`Ajouter` une nouvelle connexion

```bash
git remote add [nom_remote] [url]
# git remote add MON_REPO git@github.com:Toto/Toto-projet.git
```

`Supprimer` une connexion

```bash
git remote rm [nom_remote]
```

---

## Commande precise

### Git diff

Cette commande permet de voir les different **conflit** sur une branche ou entre plusieurs

Elle met en surbrilance les differences dans le terminal

Les options VSC permette les visualiser directement dans l'editeur de texte

GitHub permet de voir l'historique des commit directement sur le repo et donne acces a des options supplementaire

Pour `voir` tout les conflit du projet

```bash
git diff
```

Pour `voir` les conflit d'un fichier precis

```bash
git diff --base [nom_file]
```

Pour `voir` les conflit de deux branch avant de les merge

```bash
git diff [branch_A] [branch_B]
```

Pour `voir` les conflit pas encore commit

```bash
git diff --staged
```

### Git log

Cette commande permet de connaitre l'**historique des commit** d'un repo

Pour voir tout les commit d'une branch et obtenir les information lie (qui, ou et quand)

GitHub propose la meme option en plus detailler

```bash
git log
```

Pour `voir` les commit different entre deux branch

```bash
git log [branch_B] [branch_A]
```

Pour `voir` les commit qui on concerner un fichier precis

```bash
git log --follow [mon_file]
```

Pour avoir `TOUTES` les information des commit

```bash
git log --stat -M
```

### Git status

Pour connaitre les fichier qui on ete modifier et qui ne sont **pas encore commit**

```bash
git status
```

### Gitk

Permet d'ouvir une **interface graphique** de l'arborescence du repo

```bash
gitk
```

### Git reset

⚠️ _ATTENTION COMMANDE TRES RISQUER ET IRREVERSIBLE_

> il est preferer utiliser l'onglet "Source Control" de VSC

Cette commande permet de revenir a l'**etat initial** a partire d'un commit ou du dernier commit

Pour `réinitialiser` toute l'arborescence a partir du **dernier commit**

```bash
git reset --hard HEAD
```

Pour `réinitialiser` un fichier a partir du **dernier commit**

```bash
git reset [nom_file]
```

Pour `réinitialiser` toute l'arborescence a partir d'**un commit** precis

```bash
git reset --hard [num_commit]
```

---

## Moins important

### Git tag

Cette commande permet de **gerer** les tag

Pour `voir` tout les tag

```bash
git tag
```

Pour `ajouter` un tag

```bash
git tag -a [v1.4] -m "Description du tag"
```

Pour `afficher` les information lie a un tag

```bash
git show [v1.4]
```

Pour `supprimer` un tag

```bash
git tag -d [v1.4]
```

### Git rm

Pour `supprimer` un ficher du repo

```bahs
git rm [nom_file]
```

### Git stash

Cette commande permet d'**enregistrer les fichier localement** sans les commit (pour garder un historique propre)

Pour `enregistrer` les changement

```bash
git stash
```

Pour `voir` la liste des changement

```bash
git stash
```

Pour `ecraser` les changement

```bash
git stash pop
```

Pour `supprimer` les changement avant de commit

```bash
git stash drop
```

### Git show

Pour `afficher` toutes les informations lier au fichier du repo

```bash
git show
```

Pour `voir` les informations d'un commit precis de façon lisible

```bash
git show [num_commit]
```

### Git ls-tree

Pour `afficher` l'arborescence du repo

```bash
git ls-tree HEAD
```

### Git grep

Moteur de recherche de Git pour `rechercher un mot ou une phrase` dans tout les fichier

```bash
git grep "[mot_rechercher]"
```

---
