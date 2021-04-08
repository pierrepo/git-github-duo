---
title: Tutoriel Git / GitHub
author: Pierre Poulain
license: Creative Commons Attribution-ShareAlike (CC BY-SA 4.0)
---

# Partie 1 : Utilisation des clés privée et publique

🔑 La combinaison de clés privée et publique est un mécanisme très sécurisé pour accéder à un serveur distant. La connexion est authentifiée par l'utilisation conjointe de la clé privée stockée sur la machine de l'utilisateur et de la clé publique stockée sur le serveur distant.

## 1.1 Création des clés

Ouvrez un terminal Bash Ubuntu, puis entrez la commande suivante :

```bash
$ ssh-keygen -t rsa -b 4096 -C "connexion github duo"
```

🔔 Rappels :

- Ne tapez pas le `$` en début de ligne et faites attention aux majuscules et aux minuscules.
- Copiez / collez les commandes pour aller plus vite et faire moins d'erreur.

Validez en appuyant **4** fois sur la touche <kbd>Entrée</kbd>.

À la fin, vous devriez obtenir quelque chose du type :
```
The key's randomart image is:
+---[RSA 4096]----+
|==..  o          |
|.o+.o. o .       |
| o.+o = =        |
|o +  O . =       |
|.o o  = S +      |
|. . .o + =       |
|   +ooo =        |
|  +o+++o         |
| ..Eo++o.        |
+----[SHA256]-----+
```

Affichez maintenant le contenu du répertoire `~/.ssh/` :
```bash
$ ls ~/.ssh/
```

Vous devriez trouver :

- `id_rsa` : votre clé privée. À ne communiquer à personne ! Cette clé doit rester secrète.
- `id_rsa.pub` : votre clé privée, que vous allez déposer sur le site de GitHub.

Toujours dans votre terminal Bash Ubuntu, affichez à l'écran le contenu du fichier `id_rsa.pub` :
```bash
$ cat ~/.ssh/id_rsa.pub
```

Vous devriez obtenir une clé qui ressemble à cela :
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCjNrLoIXHG3NHp2eucFnOqicMz2b4I6FvjxVYMEwzO40syopxd
7YtQXzWp9EpuO7n9wWZnZ5uR6bXPqXp9VdN3MviI8PsvvjDbp4AfNz4Onunpy0mIjUarRL5evEPKI2iuqO7pUC9m
qV2tAPopsjfSuj+gBEcMAZU8gMK1o/eBqD+tpuGrNiE1Zq8PDQPOO7HStG09tZ3ABDPBSISun7GAC3ytbYJtL4A3
IEgUX1oCGbrzVGhIB0pK/xKVVpmG6KplVOjsSgYCivfOIJ05GJQk0LuizGWg1rKt4yYZgXjoMW4F+hz/+c9xnDuR
q8ZAQLBAm+NWU91Nczb5OzAfWYVY9BlES35YfcFRLuWP8ArXLHRtZJq48B7wIN39im72iYcKXcOzeyYRZQFKMb0z
9PuDrpZ6LpQZQw04i7CWJZca7Auwtd3yyC+PfuvyeuFhODqktP0rdKtTEQdrUTdaxb+K1k8FPmZMc/o91sBJ1u6d
ceccjpO1LTK/I1w9xmbQAxi0hLDCRN9hm/RUkOvzxZJed6kBzozvZ8vCi+Afv1BXjkv+jrezkkqsFl5YA01nLxyU
zo1LFBNZ41+wRHQXCQKENzsHnuVwZ0CcXRfFoZnDCn9Hs0L7kBH02O2JPbFlIVw/72XaZundqjczcp1w0gou0+Uq
TRTPvbaUnz17wffw== connexion github duo
```

Copiez cette clé, depuis `ssh-rsa` jusqu'à `connexion github duo` inclus.


## 1.2 Ajout de la clé publique dans GitHub

Ouvrez maintenant l'interface de gestion des clés de GitHub : <https://github.com/settings/keys>

*Authentifiez-vous si besoin.*

Cliquez sur le bouton vert « *New SSH key* ».

Indiquez comme titre « Connexion DUO » (sans les guillemets).

Collez votre clé dans le champ *Key* (tout depuis `ssh-rsa` jusqu'à `connexion github duo` inclus).

Enfin, cliquez sur le bouton vert « *Add SSH key* ».


## 1.3 Test de la connexion à GitHub

Pour tester si l'enregistrement de votre clé publique dans GitHub a bien fonctionné, tapez la commande suivante dans le terminal Bash Ubuntu de votre machine :
```bash
$ ssh -T git@github.com
```
Validez en tapant `yes` puis en appuyant sur <kbd>Entrée</kbd>.

Si votre clé privée a bien été enregistrée dans GitHub, vous devriez obtenir le message :
```
Hi <login>! You've successfully authenticated, but GitHub does not provide shell access.
```
Avec `<login>` l'identifiant de votre compte sur GitHub. 🎉


# Partie 2 : Premier dépôt
## 2.1 Création d'un nouveau dépôt sur GitHub

Dans l'interface de GitHub, tout en haut à droite, cliquez sur le symbole `+` puis sur « *New repository* » :

![](img/github_create_repo1.png)

Indiquez ensuite *duo-test* comme « *Repository name* » :

![](img/github_create_repo2.png)

Laissez tous les autres paramètres par défaut.

Puis cliquez sur le bouton vert « *Create repository* ».

Enfin, notez et copiez l'adresse de connexion de votre dépôt qui débute par `git@github...` :

![](img/github_create_repo3.png)

Vous en aurez besoin pour la suite.

⚠️ **Attention** ⚠️ Si l'adresse de votre dépôt ne débute pas par `git@github...` mais par `https://github...` alors cliquez sur le bouton gris « *SSH* » pour obtenir l'adresse qui débute par `git@github...`


## 2.2 Connexion du dépôt distant (sur GitHub) à votre machine locale

Ouvrez un terminal Bash Ubuntu, puis déplacez-vous dans le répertoire `/mnt/c/Users/omics/` :

```bash
$ cd /mnt/c/Users/omics/
```

Créez ensuite le répertoire `intro-git` et déplacez-vous à l'intérieur :
```bash
$ mkdir -p /mnt/c/Users/omics/intro-git
$ cd intro-git
```

Vérifiez avec la commande `pwd` que vous êtes dans le bon répertoire :
```bash
$ pwd
/mnt/c/Users/omics/intro-git
```

Exécutez ensuite la commande suivante pour cloner votre dépôt distant (qui est sur GitHub) sur votre machine locale :
```bash
$ git clone git@github...
```
Pour l'utilisateur `pierrepo`, la commande complète est : `git clone git@github.com:pierrepo/duo-test.git`

Remarque : git pourra éventuellement se plaindre avec le message `warning: You appear to have cloned an empty repository.` C'est tout à fait normal, le dépôt est vide pour le moment, mais nous allons rapidement y ajouter des fichiers.

Déplacez-vous maintenant dans le répertoire créé et qui correspond à votre dépôt git :
```bash
$ cd duo-test
```

Affichez le contenu du répertoire.

Ce répertoire ne contient rien. C'est normal, votre dépôt est vide. Mais ce répertoire est un peu particulier car il contient en fait un répertoire caché `.git`. Affichez ce répertoire avec la commande :
```bash
$ ls -al
```
C'est ce répertoire qui va contenir toute la mémoire du dépôt, donc tout l'historique du dépôt. 🧐 Ne le supprimez pas.


## 2.3 Configuration du dépôt local

Avant de commencer à créer et modifier des fichiers dans votre dépôt, il faut dire à git qui vous êtes :
```bash
$ git config --global user.name "Prénom Nom"
$ git config --global user.email "moi@mail.com"
```

*Attention, adaptez le prénom, le nom et l'adresse e-mail à votre cas.*

Remarque : ces commmandes `git config` ne sont à lancer qu'une seule fois sur votre machine (même si vous avez plusieurs dépôts).

## 2.4 Exploration des commandes de base

Toujours dans votre dépôt git, créez le fichier `test1.txt` et ajoutez-y du contenu. Vous pouvez faire cela avec l'éditeur de texte `nano` ou plus rapidement avec la commande suivante :
```bash
$ echo "une première ligne" > test1.txt
```

Si vous tapez maintenant la commande `git status` pour savoir ce qui se passe, vous devriez obtenir :
```
$ git status
Sur la branche master

Aucun commit

Fichiers non suivis:
  (utilisez "git add <fichier>..." pour inclure dans ce qui sera validé)
        test1.txt

aucune modification ajoutée à la validation mais des fichiers non suivis sont présents (utilisez "git add" pour les suivre)
```

Le fichier `test1.txt` existe bien mais il n'est pas encore pris en charge par git. Pour cela, il faut utiliser la commande `git add` :
```bash
$ git add test1.txt
```

Un nouveau `git status` renvoie :
```
$ git status
Sur la branche master

Aucun commit

Modifications qui seront validées :
  (utilisez "git rm --cached <fichier>..." pour désindexer)
        nouveau fichier : test1.txt
```

`test1.txt` est désormais pris en compte par git et ses modifications sont prêtes à être validées. Pour cela, nous allons créer un *commit*, c'est-à-dire une photo des fichiers :
```bash
$ git commit -m "Premier commit"
```

Vous devriez obtenir un résultat du type :
```bash
$ git commit -m "Premier commit"
[master (commit racine) a7b7006] Premier commit
 1 file changed, 1 insertion(+)
 create mode 100644 test1.txt
```

Parfait ! Il est maintenant temps d'envoyer ce premier *commit* sur GitHub :
```bash
$ git push
Énumération des objets: 3, fait.
Décompte des objets: 100% (3/3), fait.
Écriture des objets: 100% (3/3), 236 octets | 236.00 Kio/s, fait.
Total 3 (delta 0), réutilisés 0 (delta 0)
To github.com:pierrepo/duo-test.git
 * [new branch]      master -> master
```

Retournez maintenant sur votre navigateur internet et rafraichissez la page de votre dépôt sur GitHub (a priori `https://github.com/<login>/duo-test` avec `<login>` votre identifiant GitHub).

Vous devriez voir le fichier `test1.txt` ! 🥳

![](img/github_first_commit.png)


Depuis le terminal Bash Ubuntu, modifiez une seconde fois le fichier `test1.txt` :
```bash
$ echo "et hop une deuxième ligne !" >> test1.txt
```

Visualisez les différences par rapport au *commit* précédent avec la commande
```bash
$ git diff
```

Une nouvelle ligne est marquée par le symbole `+`. Une ligne supprimée est marquée par le symbole `-`. Les lignes modifiées apparaissent avec le symbole `+` et `-`.

Exemple de résultat :
```bash
$ git diff
diff --git a/test1.txt b/test1.txt
index 0d8e693..f9f2480 100644
--- a/test1.txt
+++ b/test1.txt
@@ -1 +1,2 @@
 une première ligne
+et hop une deuxième ligne !
```

Ajoutez (encore) le fichier modifié puis créez un nouveau *commit* :
```bash
$ git add test1.txt
$ git commit -m "Ajout d'un nouveau message"
```

Et envoyez ce nouveau *commit* sur Github :
```bash
$ git push
Énumération des objets: 5, fait.
Décompte des objets: 100% (5/5), fait.
Écriture des objets: 100% (3/3), 305 octets | 305.00 Kio/s, fait.
Total 3 (delta 0), réutilisés 0 (delta 0)
To github.com:pierrepo/duo-test.git
   404b6ff..5adb360  master -> master
```

Retournez sur GitHub pour observer ce nouveau *commit* :

![](img/github_second_commit.png)


Depuis le terminal Bash Ubuntu, affichez l'historique avec la commande `git log` :
```bash
$ git log
commit 5adb360b9682320e4fe32382d79d9b9454d657b3 (HEAD -> master, origin/master)
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Tue Apr 6 21:00:36 2021 +0200

    Ajout d'un nouveau message

commit 404b6ff031bd9ba0daa586c7a524eb8ef409ec1c
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Tue Apr 6 20:52:47 2021 +0200

    Premier commit
```

Si besoin, pressez la touche <kbd>q</kbd> pour quitter le journal de git.

Vous constatez que git mémorise :

- **qui** a créé le *commit* (par exemple : *Pierre Poulain <pierre.poulain@cupnet.net>*) ;
- **quand** le *commit* a été créé (par exemple : *Tue Apr 6 21:00:36 2021 +0200*) ;
- et **pourquoi** il a été créé (par exempe : *Ajout d'un nouveau message*).

Git mémorise aussi quels fichiers ont été modifiés. Nous verrons plus tard comment les retrouver.

De plus, git attribue un identifiant à chaque *commit* (ici : `404b6ff031bd9ba0daa586c7a524eb8ef409ec1c`). Cet identifiant est unique et permet de retrouver un *commit* particulier.

Depuis l'interface de GitHub, cliquez sur le bouton vert « *Add a README* »

Dans l'éditeur en ligne, ajoutez le texte suivant :
```
# duo-test

Dépôt git de test pour le **DU omiques**.
```

![](img/github_readme_1.png)

En bas de la page, indiquez comme titre de *commit* : « Création README.md » (sans les guillemets), puis cliquez sur le bouton vert « *Commit new file* ».

![](img/github_readme_2.png)

Bravo ! Vous avez créé un nouveau *commit*, mais cette fois dans l'interface de GitHub :

![](img/github_readme_3.png)


Retournez dans le terminal Bash Ubuntu et synchronisez votre dépôt git local avec GitHub :
```bash
$ git pull
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Dépaquetage des objets: 100% (3/3), 716 octets | 358.00 Kio/s, fait.
Depuis github.com:pierrepo/duo-test
   5adb360..4c65a31  master     -> origin/master
Mise à jour 5adb360..4c65a31
Fast-forward
 README.md | 3 +++
 1 file changed, 3 insertions(+)
 create mode 100644 README.md
```

Vérifiez que le fichier `README.md` est bien présent avec la commande `ls` puis affichez son contenu :
```bash
$ cat README.md
```

Vérifiez également que le *commit* créé sur GitHub est bien enregistré dans l'historique :
```bash
$ git log
```

Si besoin, pressez la touche <kbd>q</kbd> pour quitter le journal de git.

# Partie 3 : Un peu de spéléo

*Remarque : cette section est l'occasion d'explorer l'historique d'un dépôt git et d'aborder une nouvelle commande, `git show`.*

J'ai développé il y a quelques années [autoclasswrapper](https://github.com/pierrepo/autoclasswrapper), un wrapper Python pour le programme de classification bayesienne  [AutoClass C](https://ti.arc.nasa.gov/tech/rse/synthesis-projects-applications/autoclass/autoclass-c/).


Depuis votre terminal Bash Ubuntu, déplacez-vous dans le répertoire `/mnt/c/Users/omics/intro-git` :
```bash
$ cd /mnt/c/Users/omics/intro-git
```


Téléchargez l'intégralité du projet *autoclasswrapper* avec la commande :
```bash
$ git clone https://github.com/pierrepo/autoclasswrapper.git
```

puis déplacez-vous dans le répertoire du projet :
```bash
$ cd autoclasswrapper
```

### De quand date le dernier *commit* ?

Astuce : combinez les commandes `git log` et `head`.


### Quand a été créé le tout premier *commit* ?

Astuce : combinez les commandes `git log` et `tail`.


### Combien de *commits* ont été enregistrés jusqu'à présent ?

Astuce : combinez les commandes `git log`, `grep -c` et un mot-clé pertinent. Vérifiez cette valeur sur le site du dépôt : <https://github.com/pierrepo/autoclasswrapper>

### Trouvez dans quel *commit* j'ai ajouté la possibilité de construire un [dendrogramme](https://en.wikipedia.org/wiki/Dendrogram) ? 

Astuce : combinez les commandes `git log`, `grep -B4` et un mot-clé pertinent.


### Combien de fichiers ont été modifiés dans le *commit* correspondant ?

Utilisez pour cela la commande

```
$ git show --name-only <identifiant-du-commit>
```

avec `<identifiant-du-commit>` l'identifiant du *commit* intéressant. Aide : il commence par `2d1c`.

Notez la différence avec la commande :
```
$ git show <identifiant-du-commit>
```
Pressez la touche <kbd>q</kbd> pour quitter.


# Partie 4 : Utiliser les clés privée et publique pour une connexion en SSH au serveur de l'IFB

## 4.1 Enregistrement de la clé publique sur le serveur de l'IFB

La paire de clés que vous avez créée peut également être utile pour vous connecter rapidement sur le serveur de l'IFB, c'est-à-dire sans entrer votre mot de passe à chaque fois.

Pour cela, exécutez la commande suivante pour enregistrer votre clé publique sur le serveur de l'IFB :
```
$ ssh-copy-id -i ~/.ssh/id_rsa.pub <login>@core.cluster.france-bioinformatique.fr
```

avec `<login>` votre identifiant sur le serveur de l'IFB.

Entrez votre mot de passe lorsqu'il est demandé.

Exécutez ensuite la commande suivante :
```bash
$ ssh <login>@core.cluster.france-bioinformatique.fr
```
avec `<login>` votre identifiant sur le serveur de l'IFB.

Si la manipulation précédente avec `ssh-copy-id` s'est bien passée, vous devriez pouvoir vous connecter sur le serveur de l'IFB sans entrer de mot de passe. Pratique non ?


## 4.2 Copie de la paire de clés sur le serveur de l'IFB

On peut faire encore plus intéressant en copiant la paire de clés sur le serveur de l'IFB.

Déconnectez-vous du serveur de l'IFB en exécutant la commande `exit`.

Depuis le terminal Bash Ubuntu de votre machine locale, copiez votre paire de clés sur le serveur de l'IFB :
```bash
$ scp ~/.ssh/id_rsa* <login>@core.cluster.france-bioinformatique.fr:.ssh/
```
avec `<login>` votre identifiant sur le serveur de l'IFB.

Connectez-vous au serveur de l'IFB (normalement sans mot de passe) : 
```bash
$ ssh <login>@core.cluster.france-bioinformatique.fr
```

Puis clonez votre dépôt git depuis GitHub :

```bash
$ git clone git@github.com:<login>/duo-test.git
```

avec `<login>` votre identifiant GitHub (pas celui de l'IFB).

Déplacez-vous ensuite dans le nouveau répertoire créé :
```bash
$ cd duo-test
```

Vérifiez avec la commande `git log` que vous avez récupéré tout l'historique du projet.

Vous pouvez ainsi travailler dans votre dépôt depuis votre machine locale ou le serveur de l'IFB, à votre convenance. Pensez à envoyer sur GitHub (`git push`) ou à télécharger depuis GitHub (`git pull`) vos modifications régulièrement.

Essayez de modifier un fichier ou d'en créer un nouveau, de l'ajouter, de créer un nouveau *commit* puis de l'envoyer sur GitHub. Ammusez-vous !


# Partie 5 : Branches et collaboration
## 5.1 Les branches

Revisionez la vidéo « [Débuter avec Git et Github en 30 min](https://youtu.be/hPfgekYUKgk?t=634) » à partir de 10'34 sur les branches.

Depuis le terminal Bash Ubuntu de votre machine locale, revenez dans votre dépôt `duo-test` :
```bash
$ cd /mnt/c/Users/omics/intro-git/duo-test
```

Créez une nouvelle branche, par exemple *nouveau-fichier* et basculez sur cette branche :

```bash
$ git checkout -b nouveau-fichier
```

Créez un nouveau fichier `test2.txt` avec le texte qui vous convient :

```bash
$ echo "Nouveau fichier pour tester une branche" > test2.txt
```

Réalisez plusieurs *commits* en modifiant à chaque fois le fichier `test2.txt` :

```bash
$ git add test2.txt
$ git commit -m "Création d'un nouveau fichier"
$ echo "Une ligne supplémentaire" >> test2.txt
$ git add test2.txt
$ git commit -m "Ajout d'une ligne"
```

Revenez sur la branche *master* et vérifiez que le fichier `test2.txt` n'est **pas** présent :

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

Envoyez toutes vos modifications sur GitHub :

```bash
$ git push
```

Vérifiez que le dépôt sur GitHub a bien été mis à jour.


## 5.2 Collaboration avec GitHub

Revisionez la vidéo « [Débuter avec Git et Github en 30 min](https://youtu.be/hPfgekYUKgk?t=1058) » à partir de 17'38 sur le dépôt distant et GitHub.

Explorez le travail collaboratif avec une ou plusieurs autres personnes. 

Remarque : Comme votre dépôt est déjà sur GitHub, vous n'aurez pas besoin d'exécuter la commande `git remote add...`

