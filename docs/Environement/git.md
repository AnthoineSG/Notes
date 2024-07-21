# Git Commandes

La gestion de cette outil est très importante car GitHub est avant tout un outil collaboratif donc un bon historique est primordial pour que :

- tout les utilisateurs puissent s'y retrouver facilement
- que la maintenence soit simple
- que la lecture soit agréable pour tous

---

### Renommer un les commit

Cette commande permet de changer les auteurs des commit en fonction la config global

```bash
git -c rebase.instructionFormat='%s%nexec GIT_COMMITTER_DATE="%cD" GIT_AUTHOR_DATE="%aD" git commit --amend --no-edit --reset-author' rebase -f --root
# possibiliter de changer --root par le sha ou HEAD~n
```

Pour `git rebase -i HEAD~100`

```bash
git config --global core.editor "code --wait"
```

Pour intaller les var d'environement de vsc

`cdm + shift + p` => Shell Command: Install 'code' command in PATH

---

## Mise en place

### Git config

Pour mettre en place une liaison entre Git et GitHub, la première étape est de configurer son environnement en liant Git à l'adresse mail du profil GitHub pour que les actions realisées soient associées aux profils :

```bash
git config --global user.email [valid-email]
# git config --global user.email totoDu33@toto.fr
```

Dans un même temps mettre en place le nom de l'utilisateur

```bash
git config --global user.name "[firstname lastname]"
# git config --global user.name "Toto Du33”
```

On peut en plus définir des fichiers que Git ignorera automatiquement

> ⚠️ _Toujours penser au `.gitignore` pour les autres utilisateurs_

```bash
git config --global core.excludesfile '[file]'
# git config --global core.excludesfile '~/.gitignore'
```

### Git init

Pour relier un nouveau projet à Git ce qui créera un dossier masqué `.git` qut contiendra toutes les informations (commit, branch, historique, ...)

```bash
git init
```

## Commande de gestion de projet

### Git clone

Pour **recuperer** un repo GitHub sur la machine local, je copie le chemin jusqu'à la racine du repo

```bash
git clone [url ou SSH]
# git clone git@github.com:Toto/Toto-projet.git
```

### Git add

Cette commande permet d'**ajouter des fichier** au repo GitHub

Pour ajouter `tout` les fichiers :

```bash
git add .
```

Pour ajouter `un/des` fichier(s) spécifique(s)

```bash
git add [my_file]
git add [my_file1] [my_file2] [...]
```

### Git commit

Apres avoir ajouté un ou plusieurs fichier(s) le commit permet de **créer un paquet** de ses fichier et d'ajouter un message de description

> Plus il y a de commit mieux c'est : l'historique GitHub est maintenu a jour

```bash
git commit –m "Description du commit"
# ou
git commit [my_file1] -m "Description du commit"
```

### Git push

Cette commande **permet d'envoyer** toute les modifications locales sur le repo GitHub

> habitude classique :
>
> - git add .
> - git commit -m "blabla"
> - git push

```bash
# pour créer une branche existante en local et envoyer son contenu sur un repo GitHub
git push --set-upstream [remote] [branch]

# pour envoyer le contenu sur une branche spécifique
git push [remote] [branch]

# une fois que les branches locales et GitHub sont reliés, un simple push suffit
git push
```

### Git pull

Pour **mettre à jour son repo** local avec toutes les modifications qui ont eu lieu sur GitHub

Cette commande met à jour toutes les branches et remote disponibles

> - branch A et B en local
> - branch C sur GitHub
> - git pull
>   - branch A, B et C disponibles en local
>
> Cette opération est à faire tres fréquemment quand on travaille en groupe sur un même repo pour ne pas avoir des differences d'historique (à combiner avec une bonne utilisation des branches)

```bash
git pull

# ou vers un autre remote
git pull [remote]
```

### Git branch

Les branches permettent de séparer le travail effectué et donc mieux s'**oganiser**

> - branch **A** je fais des truc
> - je crée une branche **B** depuis la branche**A**
> - je casse tout sur la branche **B**
>   - je me replace sur la branche **A**
>   - et je supprime la branche **B**
> - la branche **A** est restée intacte

Pour `voir` toutes les branches

```bash
# Les branches en local
git branch

# Toutes les branches et remotes reliées
git branch -a
```

Pour `créer` une nouvelle branche à partir de la branche actuelle

```bash
git branch [nom_branche]
# Donc à l'initiation branch A === branch B
```

Pour `supprimer` une branche

```bash
git branch –d [nom_branche]

# -D pour la supprimer de force
git branch -D [nom_branche]
```

### Git checkout

Comme la commande `git branch` cette commande permet une gestion des branches légèrement différente

Pour `cree` une nouvelle branche

```bash
git checkout [nom_branche]

```

Pour `cree` une nouvelle branche et se **placer dessus** directement

```bash
git checkout -b [nom_branche]
```

### Recap des branches Git

Personnelement j'ai pour habitude de séparer les commandes en fonction de ce que je veux faire

```bash
# voir toutes les branches et remotes
git branch -a

# crée et se placer sur une nouvelle branche
git checkout -b [nom_branch]

# changer de branche
git switch [nom_branch]

# supprimer une branche
git branch -d [nom_branch]

# merge sur GitHub directement
```

### Git merge

Cette opération permet de **fusionner** une branche sur une branche active

⚠️ _Cette opération à réaliser de préférence sur GitHub directement pour des raisons de lisibilité et d'historique plus clair_

> branch B est à merge sur branch A
>
> - placement sur branch A
> - git merge branch B
>
> branch A === branch A + branch B

```bash
git merge [branch]
```

### Git remote

Commande permettant d'**ajouter une connexion** a un repo distant

`Voir` toutes les connexions

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

## Commande précise

### Git diff

Cette commande permet de voir les différents **conflits** sur une branche ou entre plusieurs

Elle met en surbrillance les différences dans le terminal

Les options VSC permettent de les visualiser directement dans l'éditeur de texte

GitHub permet de voir l'historique des commit directement sur le repo et donne accès a des options supplementaires

Pour `voir` tout les conflits du projet

```bash
git diff
```

Pour `voir` les conflits d'un fichier précis

```bash
git diff --base [nom_file]
```

Pour `voir` les conflits de deux branches avant de les merge

```bash
git diff [branch_A] [branch_B]
```

Pour `voir` les conflits pas encore commit

```bash
git diff --staged
```

### Git log

Cette commande permet de connaître l'**historique des commit** d'un repo

Pour voir tous les commit d'une branche et d'obtenir les informatiosn liées (qui, où et quand)

GitHub propose la même option en plus détaillée

```bash
git log
```

Pour `voir` les commit differents entre deux branches

```bash
git log [branch_B] [branch_A]
```

Pour `voir` les commit qui ont concerné un fichier précis

```bash
git log --follow [mon_file]
```

Pour avoir `TOUTES` les informations des commit

```bash
git log --stat -M
```

### Git status

Pour connaître les fichiers qui ont été modifiés et qui ne sont **pas encore commit**

```bash
git status
```

### Gitk

Permet d'ouvir une **interface graphique** de l'arborescence du repo

```bash
gitk
```

### Git reset

⚠️ _ATTENTION COMMANDE TRES RISQUEE ET IRREVERSIBLE_

> il est préferable d'utiliser l'onglet "Source Control" de VSC

Cette commande permet de revenir à l'**état initial** à partir d'un commit ou du dernier commit

Pour `réinitialiser` toute l'arborescence à partir du **dernier commit**

```bash
git reset --hard HEAD
```

Pour `réinitialiser` un fichier à partir du **dernier commit**

```bash
git reset [nom_file]
```

Pour `réinitialiser` toute l'arborescence à partir d'**un commit** précis

```bash
git reset --hard [num_commit]
```

---

## Moins important

### Git tag

Cette commande permet de **gérer** les tag

Pour `voir` tout les tag

```bash
git tag
```

Pour `ajouter` un tag

```bash
git tag -a [v1.4] -m "Description du tag"
```

Pour `afficher` les informations liées à un tag

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

Cette commande permet d'**enregistrer les fichiers localement** sans les commit (pour garder un historique propre)

Pour `enregistrer` les changements

```bash
git stash
```

Pour `voir` la liste des changements

```bash
git stash
```

Pour `ecraser` les changements

```bash
git stash pop
```

Pour `supprimer` les changements avant de commit

```bash
git stash drop
```

### Git show

Pour `afficher` toutes les informations liées au fichier du repo

```bash
git show
```

Pour `voir` les informations d'un commit précis de façon lisible

```bash
git show [num_commit]
```

### Git ls-tree

Pour `afficher` l'arborescence du repo

```bash
git ls-tree HEAD
```

### Git grep

Moteur de recherche de Git pour `rechercher un mot ou une phrase` dans tout les fichiers

```bash
git grep "[mot_rechercher]"
```

---
