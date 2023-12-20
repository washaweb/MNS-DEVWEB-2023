1. Récupérez le dossier `git-branches` et faites un `git log` pour en analyser l'historique
Créez une nouvelle branche `my-feature` et placez-vous dedans
2. Ajoutez un fichier feature.php qui affiche l'heure et commitez
3. Revenez dans master, ouvrez le dossier avec l'explorateur/finder : que s'est-il passé ?
4. Dans la branche master, modifiez le fichier index.php et commitez
5. Affichez l'historique de tous les commits sous forme de graphique : `git log --graph --all`
    L'ensemble : `--all`
    Sous forme de graphique : `--graph`

6. Revenez sur le master
7. Créez un fichier `page.php`, ajoutez-le et commitez
8. A quoi ressemble votre arbre maintenant ?

Pour aller plus loin, créons une nouvelle branche depuis la branche `my-feature`.
Elle s'appelera `sub-feature`.
Sur cette branche, ajoutez un fichier `contact.php`.
Commitez les nouvelles modifications.

9. Essayez de fusionner toutes les branches dans `master`.
L'ordre de merging sera le suivant :
`sub-feature` -> `my-feature`
`my-feature` -> `master`

Rappelez-vous de l'ordre des commandes :
Pour merger `B` dans `A` :

`git checkout A`
`git merge B`
