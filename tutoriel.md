---
title: Tutoriel Git / GitHub
author: Pierre Poulain
license: Creative Commons Attribution-ShareAlike (CC BY-SA 4.0)
---

# Utilisation des clés privée et publique

Le combinaison de clés privée et publique est une mécanisme très sécurisé à un serveur distant. La connexion est authentifiée par l'utilisation  conjointe de la clé privée stockée sur la machine de l'utilisateur et de la clé publique stockée sur le serveur distant.

## Création des clés

Ouvrez un terminal Bash Ubuntu, puis entrez la commande suivante :

```bash
$ ssh-keygen -t rsa -b 4096 -C "connexion github duo"
```

Validez en appuyant **4** fois sur la touche <kbd>Entrée</kbd>.

Affichez le contenu du répertoire `$HOME/.ssh/` :
```bash
$ ls $HOME/.ssh/
```

Vous devriez obtenir deux fichiers :

- `id_rsa` : votre clé privée. À ne communiquer à personne ! Cette clé doit rester secrète.
- `id_rsa.pub` : votre clé privée, que vous allez déposer sur le site de GitHub.

Toujours dans votre terminal Bash Ubuntu, affichez à l'écran le contenu du fichier `id_rsa.pub` :
```bash
cat $HOME/.ssh/id_rsa.pub
```

Vous devriez obtenir quelque chose du type :
```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCjNrLoIXHG3NHp2eucFnOqicMz2b4I6FvjxVYMEwzO40syopxd7YtQXzWp9EpuO7n9wWZnZ5uR6bXPqXp9VdN3MviI8PsvvjDbp4AfNz4Onunpy0mIjUarRL5evEPKI2iuqO7pUC9mqV2tAPopsjfSuj+gBEcMAZU8gMK1o/eBqD+tpuGrNiE1Zq8PDQPOO7HStG09tZ3ABDPBSISun7GAC3ytbYJtL4+A3IEgUX1oCGbrzVGhIB0pK/xKVVpmG6KplVOjsSgYCivfOIJ05GJQk0LuizGWg1rKt4yYZgXjoMW4F+hz/+c9xnDuRq8ZAQLBAm+NWU91Nczb5OzAfWYVY9BlES35YfcFRLuWP8ArXLHRtZJq48B7+wIN39im72iYcKXcOzeyYRZQFKMb0z9PuDrpZ6LpQZQw04i7CWJZca7Auwtd3yyC+PfuvyeuFhODqktP0rdKtTEQdrUTdaxb+K1k8FPmZMc/o91sBJ1u6dceccjpO1LTK/I1w9xmbQAxi0hLDCRN9hm/RUkOvzxZJed6kBzozvZ8vCi+Afv1BXjkv+jrezkkqsFl5YA01nLxyUzo1LFBNZ41+wRHQXCQKENzsHnuVwZ0CcXRfFoZnDCn9Hs0L7kBH02O2JPbFlIVw/72XaZundqjczcp1w0gou0+UqTRTPvbaUnz17wffw== connexion github duo
```

Copiez cette clé, depuis `ssh-rsa` jusqu'à `connexion github duo` inclus.


## Ajout de la clé dans GitHub

Ouvrez maintenant l'interface de gestion des clés de GitHub : <https://github.com/settings/keys>

*Authentifiez-vous si besoin.*

Cliquez sur le bouton vert « *New SSH key* ».

Indiquez comme titre « Connexion DUO ».

Collez votre clé dans le champ *Key* (tout depuis `ssh-rsa` jusqu'à `connexion github duo` inclus).

Enfin, cliquez sur le bouton vert « *Add SSH key* ».

Pour tester si cela a bien fonctionné, tapez la commande suivante dans le terminal Bash Ubuntu :
```bash
$ ssh -T git@github.com
```
Validez en tapant `yes` puis appuyant sur <kbd>Entrée</kbd>.

Si votre clé privée a bien été importée dans GitHub, vous devriez obtenir le message :
```
Hi <login>! You've successfully authenticated, but GitHub does not provide shell access.
```
Avec `<login> l'identifiant de votre compte sur GitHub.


# Création d'un nouveau dépôt sur GitHub

Dans l'interface de GitHub, tout en  haut à droite, cliquez sur le symbole **+* puis sur *New repository* :

![](img/github_create_repo1.png)

Indiquez ensuite *duo-test* comme « *Repository name* » :

![](img/github_create_repo2.png)

Laissez tous les autres paramètres par défaut.

Puis cliquez sur le bouton vert « *Create repository* ».

Enfin, notez et copiez l'adresse de connexion de votre dépôt qui débute par `git@github...` :

![](img/github_create_repo2.png)

Vous en aurez besoin pour la suite.


# Connexion du dépôt distant (sur GitHub) à votre machine locale

Ouvrez un terminal Bash Ubuntu, puis déplacez-vous dans le répertoire `/mnt/c/Users/omics/` :

```bash
$ cd /mnt/c/Users/omics/
```

Exécutez ensuite la commande suivante pour cloner votre dépôt distant (depuis GitHub) sur votre machine locale :
```bash
$ git clone git@github...
```

Déplacez-vous maintenant dans le répertoire créé et qui correspond à votre dépôt git :
```bash
$ cd duo-test
```

Affichez le contenu du répertoire.

Ce répertoire ne contient rien. C'est normal, votre dépôt est vite. Cependant, ce répertoire est un peu particulier car il contient un répertoire caché `.git`. Affichez ce répertoire avec la commande :
```bash
$ ls -al
```
C'est ce répertoire qui va contenir toute la mémoire du dépôt, donc tout l'historique du dépôt.


# Configuration du dépôt local

Avant de commencer à créer et modifier des fichiers dans votre dépôt, il faut dire à git qui vous êtes :
```bash
$ git config --global user.name "Prénom Nom"
$ git config --global user.email "moi@mail.com"
```

*Attention, adaptez le prénom, le nom et l'adresse e-mail à votre cas.*

# Exploration des commandes de base

Toujours dans votre dépôt git, créez le fichier `test1.txt` et ajoutez-y du contenu. Vous pouvez faire cela avec l'éditeur de texte `nano` ou plus rapidement avec la commande suivante :
```bash
$ echo "une première ligne" > test1.txt
```

Si vous tapez maintenant la commande `git status` pour savoir ce qui se passe, vous devriez obtenir :
```bash
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
```bash
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
vous devriez obtenir un résultat du type :
```bash
$ git commit -m "Premier commit"
[master (commit racine) a7b7006] Premier commit
 1 file changed, 1 insertion(+)
 create mode 100644 test1.txt
```

Parfait ! Il est maintenant temps d'envoyer ce premier *commit* sut GitHub :
```bash
$ git push
Énumération des objets: 3, fait.
Décompte des objets: 100% (3/3), fait.
Écriture des objets: 100% (3/3), 236 octets | 236.00 Kio/s, fait.
Total 3 (delta 0), réutilisés 0 (delta 0)
To github.com:pierrepo/duo-test.git
 * [new branch]      master -> master
```

Retournez maintenant sur votre navigateur internet et rafraichissez la page de votre dépôt sur GitHub (a priori `https://github.com/login/duo-test` avec *login* votre identifiant GitHub).

Vous devriez voir le fichier `test1.txt` !


---

Dans un terminal Bash Ubuntu :

- Déplacez-vous dans votre répertoire personnel Windows :
    ```bash
    $ cd /mnt/c/Users/omics
    ```
- Vérifiez que Git est bien installé avec la commande :
    ```bash
    $ git --version
    ```
- Définissez votre identité pour Git :
    ```bash
    $ git config --global user.name "Prénom Nom"
    $ git config --global user.email "moi@mail.com"
    ```

Reprenez les étapes de la vidéo « [Débuter avec Git et Github en 30 min](https://www.youtube.com/watch?v=hPfgekYUKgk) » à partir de 3'20 en modifiant un peu l'exemple :
- Le répertoire s'appellera `test-git` (à la place de `landingpage`).
- Le fichier s'appellera `script.R` (à la place de `index.html`). Vous l'éditerez avec `nano` et entrerez bien sûr le contenu qui vous intéresse (du code R par exemple).

Conseils :

- Juste après avoir créé un dépôt sur GitHub, au moment d'ajouter votre dépôt distant avec la commande `git remote add origin`, préférez la connexion **HTTPS** plutôt que SSH. Concrètement l'adresse de votre dépôt doit ressembler à `https://github.com/login/depot.git` (et pas `git@github.com:login/depot.git`).
- Si vous trouvez pénible d'entrer votre login / mot de passe à chaque fois que vous lancez les commande `git pull` ou `git push`, vous pouvez mettre en cache vos identifiants GitHub avec la commande :
    ```bash
    $ git config --global credential.helper "cache --timeout=3600"
    ``` 
    Ici, vos identifiants seront mis en cache (mémorisés) pendant 1 heure.


# Un peu de spéléo

*Remarque : cette section est l'occasion de découvrir des commandes qui n'ont pas encore été abordées jusqu'à présent. Notamment `git clone` et `git show`*

Je développe actuellement [autoclasswrapper](https://github.com/pierrepo/autoclasswrapper), un wrapper Python pour le programme de classification bayesienne  [AutoClass C](https://ti.arc.nasa.gov/tech/rse/synthesis-projects-applications/autoclass/autoclass-c/).

Depuis votre répertoire utilisateur Windows, téléchargez l'intégralité du projet avec la commande :
```bash
$ git clone https://github.com/pierrepo/autoclasswrapper.git
```

puis déplacez-vous dans le répertoire du projet :
```bash
$ cd autoclasswrapper
```

Quand a été créé le premier commit ?

Combien de commits ont été enregistrés jusqu'à présent ?

Trouvez dans quel commit j'ai ajouté la possibilité de construire un [dendrogramme](https://en.wikipedia.org/wiki/Dendrogram) ? Vous pourrez utilisez la commande `grep` avec l'option `-B4`.


Combien de fichiers ont été modifiés dans le commit correspondant ? Utilisez pour cela la commande

```bash
$ git show --name-only <identifiant-du-commit>
```

Notez la différence avec
```bash
$ git show  <identifiant-du-commit>
```

# Trucs et astuces
 
### Créer un compte sur GitHub

Créez un compte sur la plateforme de développement collaborative [GitHub](https://github.com/) en cliquant [ici](https://github.com/join).

- Entrez un login, une adresse e-mail et un mot de passe.
- Pensez à valider votre compte en cliquant sur le lien qui vous sera envoyé par e-mail par GitHub.

###  Gérer les fins de lignes

Sous Windows, si Git pose des problèmes avec les fin de lignes, utilisez la commande suivante (une seule fois) :
```bash
$ git config --global core.autocrlf true
```
