---
title: Tutoriel Git / GitHub
author: Pierre Poulain
license: Creative Commons Attribution-ShareAlike (CC BY-SA 4.0)
---

# Exploration 

Dans un terminal Bash Ubuntu:

- Déplacez-vous dans votre répertoire personnel Windows :
    ```bash
    $ cd /mnt/c/Users/Omics
    ```


# Gérer les fins de lignes
$ git config --global core.autocrlf true



1. Vous créer un compte sur la plateforme de développement collaborative [GitHub](https://github.com/) en cliquant [ici](https://github.com/join).
    + Entrez un login, une adresse e-mail et un mot de passe.
    + Pensez à valider votre compte en cliquant sur le lien qui vous sera envoyé par e-mail par GitHub.


## Un peu de spéléo

Dans quel commit ai-je ajouté la possibilité de construire un [dendrogramme](https://en.wikipedia.org/wiki/Dendrogram)
dans mon programme [autoclasswrapper](https://github.com/pierrepo/autoclasswrapper) ?

```bash
$ git clone https://github.com/pierrepo/autoclasswrapper.git
$ cd autoclasswrapper
$ git log
$ ...
```

Combien de fichiers ont été modifiés dans le commit correspondant ?

```bash
$ git show xxxxx
$ ...
```
