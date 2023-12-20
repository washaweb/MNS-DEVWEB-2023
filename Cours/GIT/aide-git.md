# Git

Sur une branche (par exemple "master")
J'ai:

- Branche "locale": ma version sur mon ordi
- Branche "origin": la version sur le serveur (il peut y avoir plusieurs copies sur différents serveurs)

Savoir ou en est notre branche locale par rapport à la branche "origin" :

```sh
    git status
```

Enregistrer ses modifications dans sa branche (vous pouvez utiliser le controle de code source de visual studio):

```sh
    git add nomdufichier1 nomdufichier2...
    git add --all
    git commit -m 'ajouter un message de commit'
```

Je peux récupérer les modifications de la branche "origin":

```sh
    git pull
```

Attention, à chaque fois, ce n'est pas un écrasement des données, mais plutôt un mélange (merge)

Je peux envoyer mes données "locale"s" sur le serveur ("origin"):

```sh
    git push
```

## Les branches

Créer une branche (depuis la branche master):

```sh
    git checkout -b <nomdunebranche>
```

Passer d'une branche à l'autre :

```sh
    git checkout <nomdunebranche>
```

## Gérer les conflits

Lorsque vous travaillez sur votre branche, à un moment donné, vous devez fusionner vos modifications avec la branche master (ou une autre branche) :

Le mieux, c'est faire une rebase du code avant de faire une demande de pull request :

```sh
    git pull --rebase origin <nomdelabranche>
```

Si il n'y a pas de conflit continuer normalement.

S'il y a des conflits : résoudre les conflits éventuels dans votre branche locale
(Le logiciel va vous indiquer quels fichiers posent des confilts, vous devez choisir entre votre modification
locale ou celle qui provient du serveur).
Une fois tous les conflits résoluts, faire un commit de merge (le message de merge est généré automatiquement).

Une fois le rebase terminé, vous disposez du code le plus à jour (master + code de votre branche).
Vous pouvez à ce moment là, décider de faire un "Pull Request" sur le dépôt.
Pour cela il faut envoyer votre code sur le serveur, mais comme vous avez fait un rebase, il faudra forcer le push:

```sh
    git push origin <nomdelabranche> --force
```

Vous êtes alors en synchronisation sur origin avec votre branche, vous pouvez procéder au "Pull request" sur Github.


## la règle à garder en tête est la suivante

- à chaque fois que vous voulez faire un "pull request" sur master,
- OU à chaque fois que vous voulez récupérer la dernière version du code de master dans votre branche

Lancer la commande :

    git pull --rebase origin master

Si il y a conflit, les résoudre puis:

    git add <nomdufichierquiposeprobleme>  <nomdufichierquiposeprobleme2>
    git rebase --continue

Une fois que le rebase est terminer, vous devez resynchroniser votre branche avec origin:

    git push origin <nomdevotrebranche> --force

Une fois cette étape terminée, votre branche est à jour sur origin.
Vous pouvez faire le pull request et merge sur master.
