# Branches et collaboration

Depuis un terminal sur le JupyterLab de l'IFB, déplacez-vous dans le répertoire de travail pour cette introduction à git :

```bash
$ cd /shared/projects/202304_duo/$USER/intro-git
```

```{admonition} Rappel
:class: tip
- Ne tapez pas le caractère `$` en début de ligne et faites bien attention aux majuscules et au minuscules.
-  Copiez / collez les commandes pour aller plus vite et faire moins d'erreur.
```

Vérifiez que vous êtes dans le bon répertoire :

```bash
$ pwd
/shared/projects/202304_duo/LOGINIFB/intro-git
```
## Les branches

Revisionez la vidéo « [Débuter avec Git et Github en 30 min](https://youtu.be/hPfgekYUKgk?t=634) » à partir de 10'34 sur les branches.

Depuis le terminal, revenez dans votre dépôt `duo-test` que vous avez créé précédemment :

```bash
$ cd /shared/projects/202304_duo/$USER/intro-git/duo-test
```

Vérifiez que votre dépôt est « propre », c’est-à-dire qu’il ne contient pas de fichier modifié non commité.

```bash
$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

Créez une nouvelle branche, par exemple *nouveau-fichier* :

```bash
$ git branch nouveau-fichier
```

Vérifiez que cette branche existe bien :

```bash
$ git branch
* master
  nouveau-fichier
```

Le symbole `*` à gauche de *master* indique que la branche courante est *master*.

Basculez maintenant sur la branche que vous venez de créer :

```bash
$ git checkout nouveau-fichier
```

Vérifiez que vous êtes désormais sur la bonne branche :

```bash
$ git branch
  master
* nouveau-fichier
```

Le symbole `*` à gauche de *nouveau-fichier* indique que la branche courante est *nouveau-fichier*.

Créez un nouveau fichier `test2.txt` avec le texte qui vous convient :

```bash
$ echo "Nouveau fichier pour tester une branche" > test2.txt
```

Demandez ensuite à git de prendre en compte votre nouveau fichier :

```bash
$ git add test2.txt
```

Puis réalisez un premier commit :

```bash
$ git commit -m "Création d'un nouveau fichier"
```

Réalisez plusieurs *commits* en modifiant à chaque fois le fichier `test2.txt`, par exemple :

```bash
$ echo "Une ligne supplémentaire" >> test2.txt
$ git add test2.txt
$ git commit -m "Ajout d'une ligne"
$ echo "Et encore une !" >> test2.txt
$ git add test2.txt
$ git commit -m "Ajout d'une dernière ligne"
```

Vous pouvez enfin envoyer votre branche sur GitHub. En utilisant la commande :

```bash
$ git push
```

Git va vous renvoyer un message d’erreur :

```
fatal: La branche courante nouveau-fichier n'a pas de branche amont.
```

et vous proposer une instruction plus complète du type :

```bash
$ git push --set-upstream origin nouveau-fichier
```

Utilisez cette instruction pour enfin envoyer votre branche sur GitHub.

```{note}
La commande `git push --set-upstream origin nouveau-fichier` est à utiliser uniquement la première fois que vous envoyez une branche sur GitHub. Par la suite, vous pourrez utiliser la commande `git push` seule.
```

Verifiez que votre branche `nouveau-fichier` est bien présente sur GitHub en cliquant sur branches dans le menu au dessus de l’aperçu du dépôt.


## 2. Fusionner les branches

Depuis votre terminal, revenez sur la branche *master* et vérifiez que le fichier `test2.txt` n'est **pas** présent :

```bash
$ git checkout master
$ ls
```

Fusionnez maintenant sur *master* la branche *nouveau-fichier* :

```bash
$ git merge nouveau-fichier
```

Vérifiez que le fichier `test2.txt` est présent et contient vos modifications :

```bash
$ ls
$ cat test2.txt
```

Supprimez l'ancienne branche *nouveau-fichier* :

```bash
$ git branch -d nouveau-fichier
```

Puis vérifiez qu'elle a bien été détruite :

```bash
$ git branch
* master
```

Enfin, envoyez toutes vos modifications sur GitHub :

```bash
$ git push
```

Vérifiez que le dépôt sur GitHub a bien été mis à jour.


## 5.2 Collaboration avec GitHub

Revisionez la vidéo « [Débuter avec Git et Github en 30 min](https://youtu.be/hPfgekYUKgk?t=1058) » à partir de 17'38 sur le dépôt distant et GitHub.

Explorez le travail collaboratif avec une ou plusieurs autres personnes. 

Remarque : Comme votre dépôt est déjà sur GitHub, vous n'aurez pas besoin d'exécuter la commande `git remote add...`

