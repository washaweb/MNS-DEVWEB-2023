# GIT

## Introduction

- Inventé pour garder une trace des changements qui se produisent dans le code source de Linux
- Git est un protocole pour conserver le fichier et la modification qui lui est arrivée à travers le temps et les gens
- Github est une plateforme (récemment achetée par Microsoft)
     - Pour héberger des fichiers et utiliser le protocole git.
     - Point central de la communauté opensource pour obtenir et partager du code (suivre, aimer, bifurquer, regarder)
     - Grande visibilité en tant que développeur
     - Des sites Web similaires existent: GitLab, Bitbucket, le vôtre ?

Aide officiel Github : https://help.github.com/en

## Dépôts (Repositories)

Vous pouvez créer :
* un nouveau dépôt (en partant de zéro) `git init`
* à partir d'un travail existant existant `git clone`,
* ou à partir d'un autre dépôt git (fork) https://help.github.com/en/github/getting-started-with-github/fork-a-repo

## Processus principal

1. `git status` : donne un apperçu de l'état actuel du dépôt local par rapport aux fichiers modifés, nouveaux et supprimés
3. `git add` : Les fichiers locaux que vous souhaitez ajouter au suivi
3. `git commit -m "message"` : Une fois les changement indexés, envoyer la modification au dépôt local avec un message
4. `git push` : Collecte toutes les modifications qui ont été indexées dans le dépôt local et les envoie au dépôt distant `origin`
5. `git pull` : Tire toutes les modification du dépôt distant `origin` et les copie sur votre dépôt local

```bash
    # init un nouveau dépôt en local
    git init

    # clone le dépot distant en local
    git clone https://github.com/washaweb/TestGit

    # si on a initialisé un nouveau dépôt, on peut vouloir ajouter la référence vers un dépôt distant par la suite :
    git remote add origin https://github.com/washaweb/TestGit.git

    # donne des informations sur l'état courant du dépôt local
    git status

    # ajout des fichiers modifés au prochain envoi
    git add monfichier monfichier2 ...

    # vous pouvez aussi ajouter tous les fichiers d'un coup (déconseillé)
    git add --all

    # ou juste le dossier courant
    git add .
    
    # envoi vers le dépôt local avec un message
    git commit -m 'mon message exemple'

    # transfert de toutes les modifications locales vers le dépôt d'origin (distant)
    git push –u origin master 

    #la première fois, indiquer le dépot distant choisi et la branche, puis un simple git push suffit :
    git push

    # tirer la dernière version du dépôt distant en local (écrasera les fichier locaux non commités !)
    git pull
```

## Branches

Tous les référentiels peuvent avoir plusieurs branches et vous pouvez modifier / créer des branches à l'aide de la commande `checkout`.

À ce moment-là, plusieurs versions du même site Web existeront donc: celle de la branche "principale" `master` et celle de la "deuxième" branche du nom que vous décidez de lui donner.

Des conflits peuvent survenir si vous souhaitez **fusionner** (`merge`) les modifications des deux branches ensemble.

Par exemple, deux développeurs peuvent travailler sur la version mobile du site Web et l'un d'eux applique une couleur d'arrière-plan rouge et l'autre veut du bleu. Nous devrons décider quel changement sera finalement appliqué.
Il faut alors passer en revue le code conflictuel et choisir la bonne version de chaque ligne de code retenue.

Les différents types de branches fréquemment utilisées : 

* Feature branches
* Release branches
* Hotfix branches

> NOTE : Lors d'un travail à plusieurs, une **erreur de débutant** consiste souvent à **attendre trop longtemps avant de fusionner les branches** de chaque développeur. C'est une erreur qui peut coûter très cher en temps de revue du code, car bien souvent, le temps a passé **et plus personne ne sait réellement quel code il faut garder**...

```bash
    # Créer une branche
    git checkout -b branchTest

    # voir les différentes branches
    git branch

    # changer de branche
    git checkout master

    # fusioner la branche courante avec une autre branche
    git merge branchTest
```


### Les release

Avec git, il est aussi possible de publier des versions spécifiques de votre code. Une fois la release crée, la branche perd la possibilité de changer l’historique des commits. Pour publier une release on utilise des tags.
On va taguer des branches et c’est ce mécanisme qui permet de gérer simplement les releases.

```bash
    # créer un tag
    git tag -a v1.0 -m "Release 1.0"

    # affiche les tags:
    git tag

    # afficher les détails d'un tag
    git show v1.0
```

### Bonne(s) pratique(s)

Attention à ne pas versionner n’importe quoi !
C’est vous qui choisissez le(s) fichier(s) à versionner dans votre projet. Vous pouvez créer un fichier `.gitignore` pour empêcher l’ajout de fichiers indésirables.

```bash
    #exemple de gitignore
    .Ds_Store
    node_modules/*
    build
    *.zip

```

Il existe des modèles ou patterns de travail avec Git, chaque équipe choisi l'un ou l'autre en fonction de ses besoins, voir ce document pour aller plus loin : https://nvie.com/posts/a-successful-git-branching-model/


### Le process classique

1. Le développeur est invité à faire une fonctionnalité ou une correction de bogue
2. Il fait la modification du code source
3. Donnez à son commit un nom ou une référence à l'ID de bug / fonctionnalité
4. Il pousse une version de travail de toutes les modifications

### Le Process de travail collaboratif avec branches

Dans une grosse entreprise, pour éviter de "casser" un projet avec des mauvaises manipulations, on peut utiliser souvent un process plus complet.

Un projet comporte une branche principale nommée `master`.

Lorsqu'on développe de nouvelles fonctionnalités, on crée une nouvelle branche de développement. Dans cet exemple, nous la nommerons `develop`, mais généralement, on utilise un nom plus complexe qui représente la modification souhaitée.

1. Le développeur est invité à faire une fonctionnalité ou une correction de bogue
2. Une **"issue"** est ouverte dans le dépôt pour expliquer cette **"feature"**, on utlise les **"tags"** appropriés pour décrire cette issue: `bug, feature, enhancement`
2. Le développeur ouvre une **"merge request"** (MR) à partir de l'issue, dans le dépôt en ligne. Une nouvelle branche est alors crée, le développeur **"pull"** (tire) en local la version du code de la branche nouvellement crée et commence à travailler dans cette branche
3. Lorsqu'il soumet son travail, il donnez à chaque **commit** un nom ou une référence à l'ID de bug / fonctionnalité, ou à toute amélioration complémentaire qu'il exécute. **On essaye de bien garder des fonctionnalités qui correspondent à la branche en cours**
4. OPTIONNEL, mais fortement recommandé : Le développeur doit faire un **rebase** de master dans sa propre branche avant de pousser son code, cela évite qu'il y ait des conflits sur la branche `master`, il doit alors faire un **squash** de tous ses commits pour les regrouper tout en haut de la ligne temporelle (voir explications spécifiques pour ceux que ça intéresse)
5. Lorsque le travail est terminé, il **push** (pousse) ensuite ses commits nettoyés et mergés vers le dépôt de travail en commun (dans sa branche d'`origin`)
6. Le développeur responsable du dépôt initial peut ensuite intégrer les modifications de la branche `develop` dans la branche `master`
7. La **merge request** est automatiquement fermée lorsque le code a été intégré dans `master`.


## Mise en Pratique

### Github + Tools

1. Créer un compte Github ou Gitlab avec votre adresse email professionnelle

    [Construire des logiciels meilleurs, ensemble](https://github.com/)

2. Téléchargez l'application appelée **"Github Desktop"**. Cette application rendra le changement plus visuel au lieu d'utiliser l'interface de ligne de commande.

    [GitHub Desktop](https://desktop.github.com/)

3. Connectez-vous à l'application en utilisant vos informations d'identification.
4. Si nécessaire, téléchargez et installez le protocole git
5. Vous pouvez également ajouter ces extensions à VSCode qui permette une meilleure intégration de GIT dans l'éditeur :
    * GitLens
    * Git History
    * Gitlab Workflow
    * Project Manager
    * gitignore

**Votre travail en tant qu'équipe d'intégration:**

1. Obtenez et regroupez toutes les fonctionnalités et correction de bogues pour la prochaine version
2. Créez le site Web / l'application en fonction du code source modifié
     - Si un problème s'est produit là-bas, nous devons voir le code source COMPLET pour voir quel commit crée des conflits ensemble et revenir à l'étape 1
3. Si aucun problème, l'application / le site Web emballé est remis à l'équipe de test qui doit tester à nouveau TOUS le site Web pour être sûr que rien d'important / ou moins important ne s'est cassé

### Plongée dans un vrai projet

Dans le dépôt que je vous partage : le projet est un site Web contenant 7 pages. Vous formerez des groupes de 2 personnes et apprendrez à coder sur le même dépôt, chaque groupe aura :

* Un développeur
* Un mainteneur / testeur

Le **développeur** ne code que ce qu'on lui demande. Il n'a pas d'accès en écriture sur le dépôt, il sera donc obligé de faire valider son travail par le mainteneur
Le **mainteneur / testeur** doit gérer le projet depuis le dépôt, c'est lui qui a l'accès en écriture au dépôt et il doit correspondre avec son développeur pour lui communiquer des issues/features à développer et faire des test et des retours sur le travail du développeur

Le testeur dispose d'un cahier des charges afin de donner des instructions sur la prochaine étape à suivre et des commentaires au développeur.

Quand il peut / veut, le testeur peut télécharger le dépôt REMOTE et donner des commentaires à "son" développeur sur "son" code
> Attention: vous n'utiliserez **que le courrier électronique pour interagir**, **il ne sera pas autorisé de parler**. vous pouvez utiliser des captures d'écran d'une partie du site (pas la totalité), des dessins ...

A la fin de la journée, une version LIVE sera déployée.


## Intégration continue - (Continuous Integration - CI)

L’Intégration Continue (continuous integration) consiste à intégrer les changements apportés au code informatique d’un projet logiciel de façon continuelle, afin de détecter et de corriger immédiatement les éventuelles erreurs.

Chaque intégration est vérifiée et testée par un build automatisé, afin de détecter les erreurs d’intégration le plus rapidement possible. Cette approche permet généralement de réduire le nombre de problèmes d’intégration, et permet à une équipe de développer son logiciel plus rapidement.
the website. Don't hesite to propose solutions to global problems.

Process de l'intégration continue :

1. Faire un changement
2. Lancer une série de tests (automatisés)
3. Si le test passe, on peut passer au déploiement ou continuer à développer
4. Si le test ne passe pas, il faut corriger le code avant de pouvoir recommencer à l'étape 2


## Déploiement continu

Le déploiement continu (Continuous Deployment) et la livraison continue (Continuous Delivery) sont des pratiques directement liées à l’intégration continue. 

La livraison continue à automatiser le processus de  "relaxe" des changements apportés au logiciel/site web auprès des utilisateurs. 

Il est possible de choisir de livrer les changements de façon quotidienne, hebdomadaire, ou autre fréquence en fonction des besoins propres à l’entreprise et à sa clientèle.

On utilise des outils dédiés pour lancer les tests d'intégration, et publier le site en ligne.

* Jenkins
* TeamCity
* Travis CI
* Gitlab CI
* Go CD
* Bamboo
* GitLab CI
* Circle CI
* Codeship
* Codefresh

### Déploiement continu avec Netlify

Netlify vous permet de lier un référentiel GitHub, GitLab ou Bitbucket à un site pour un déploiement continu. Chaque fois que vous accédez à votre fournisseur Git, Netlify exécute une build avec l'outil de votre choix et déploie le résultat en ligne.

https://docs.netlify.com/configure-builds/get-started/#basic-build-settings



