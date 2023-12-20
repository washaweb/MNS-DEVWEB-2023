

master ----- master 
                \
                \ -- dev --- dev --- dev -------------------- dev ---------------------------- dev
                      \              \                       / \                                /
                      \--- mike ---  \  --- mike ---- mike ---  mike --                         /
                                                                \ --- abdou --- abdou --- abdou /                            

# abdou veut récupérer le travail de mike
# il faut que mike ait finit sont "Pull request" sur dev et fait le merge
    
// récupérer la dernière version de dev, il est sur la branche Abdou
    git pull --rebase origin dev

si il y a conflit, résoudre le conflit dans chaque fichier, puis vous ajouter les fichiers résoluts avec 
git add <nomdufichier>

    git rebase --continue

Là il termine la fusion.

git push ne fonctionne plus, il faut le forcer pour resynchroniser votre branche locale avec celle sur origin.

    git push origin <nomdevotrebranche> --force