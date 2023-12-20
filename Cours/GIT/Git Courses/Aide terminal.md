# Aide terminal


## Variables d'environnement 

```
  $ export              # pour voir tout ce que tu as
  $ export foobar=1     # pour ajouter foobar dans les variables d'env
  $ export              # pour voir
  $ echo $foobar        # pour afficher une variable
  $ unset foobar        # pour retirer une variable d'env
```


## GIT

Bonne pratique de commit : https://github.com/stephane-klein/CONTRIBUTE-skeleton/blob/master/CONTRIBUTE.md#git-workflow

### squash et rebase

Rebase une branche avant de commencer le taf.
Voir : https://www.youtube.com/watch?v=Bjt72sbdD9s
et : https://www.ekino.com/articles/comment-squasher-efficacement-ses-commits-avec-git

```
  #shash des précédents commits en WIP
  git log
  git rebase -i HEAD~10
  # indiquer devant chaque commit à squasher la lettre `f` à la place de `pick`
  # `esc wq` pour sauvegarder
  git log
  
  # une fois le squash terminé, on peut rebase depuis origin
  git pull --rebase origin master

  # on met à jour sa branche distante en forçant :
  git push origin <nomdelabranche> --force
```

### branches 

Supprimer une branche locale :

```
  git branch -D 82-creer-la-page-https-www-spacefill-fr-fr-stockage-city
```

Ici le `-D` equivaut à `--delete --force`

Passer sur une branche :

```
  git checkout -b 82-creer-la-page-https-www-spacefill-fr-fr-stockage-city
```

