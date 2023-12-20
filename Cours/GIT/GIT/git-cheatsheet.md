# Aide-mémoire pour utiliser Git

## Commandes courantes

### Repository
Créer un nouveau repository :
    `git init`

### Configuration
Changer la configuration globale :
    `git config --global user.name "Mon nom"`
    `git config --global user.email "Mon email"`

### Préparer et commiter
Ajouter des fichiers à l'index :
    `git add <file>`

Ajouter tous les fichiers à l'index :
    `git add .`

Créer un commit (avec les fichiers ajoutés à l'index) :
    `git commit -m "Message du commit"`

Afficher les fichiers qui ont changé depuis le dernier commit :
    `git status`

Modifier l'ancien commit :
    `git commit --amend`

Ajouter à l'index les fichiers modifiés, puis commiter d'un coup :
    `git commit -am "Message du commit"`

### Afficher le log
Afficher la liste des commits :
    `git log`

Afficher la liste des commits, une ligne par commit :
    `git log --oneline`

Afficher le graphique :
    `git log --graph`

### Branches
Créer une branche :
    `git branch ma-branche`

Se placer sur une branche :
    `git checkout ma-branche`

Créer et se placer sur la branche, en une commande :
    `git checkout -b ma-branche`

### Merge
Fusionner deux branches :
    `git merge autre-branche`

### Diff
Afficher les différences entre le Working directory et HEAD (dernier commit) :
    `git diff`

Afficher les différences entre deux branches :
    `git diff une-branche une-autre-branche`

### Tags
Ajouter un tag :
    `git tag -a NomDuTag <hash>`

Afficher les tags :
    `git tag`

Récupérer le working directory d'un tag :
    `git checkout NomDuTag`

Revenir au master après avoir fait cela :
    `git checkout master`
