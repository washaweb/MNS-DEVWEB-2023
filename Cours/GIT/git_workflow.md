# Principe
Chaque développeur travaille sur une branche, qui correspond à une fonctionnalité (feature)

# Processus
Une fois le développement terminé :
`git push` pour envoyer les dernières modifications au remote.

On crée la `pull request` depuis Github

2 options :
Soit la pull request peut être mergée automatiquement
Soit il y a des conflits

S'il y a des conflits :

1. git checkout master
2. git pull
3. git merge ma-branche
4. git status => Les fichiers qui comportent des conflits
5. Dans l'IDE, régler les conflits
6. git add => de chacun des fichiers qui ont été modifiés
7. git commit
8. Dans VIM : Sortir, en sauvegardant `:x` + `Enter`
9. Vérifier qu'on ne soit plus en mode (master|MERGING)
10. git push
11. Vérifier sur Github que la pull request soit validée