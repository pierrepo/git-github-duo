---
title: Tutoriel Git / GitHub
author: Pierre Poulain
license: Creative Commons Attribution-ShareAlike (CC BY-SA 4.0)
---

# Exploration des commandes de base

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

Reprenez les étapes de la vidéo « Débuter avec Git et Github en 30 minutes » à partir de 3'20 en modifiant un peu l'exemple :
- Le répertoire s'appellera `test-git`
- Le fichier s'appellera `mon_script.R`. Vous l'éditerez avec `nano` et entrerez bien sûr le contenu qui vous intéresse (du code R par exemple).


# Un peu de spéléo

*Remarque : cette section est l'occasion de découvrir des commandes qui n'ont pas encore été abordées jusqu'à présent. Notamment `git clone` et `git show`*

Je développe actuellement [autoclasswrapper](https://github.com/pierrepo/autoclasswrapper), un wrapper Python pour le programme de classification bayesienne  [AutoClass C](https://ti.arc.nasa.gov/tech/rse/synthesis-projects-applications/autoclass/autoclass-c/).

Depuis votre répertoire Windows, téléchargez l'intégralité du projet avec la commande :
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


Combien de fichiers ont été modifiés dans le commit correspondant ?

Utilisez pour cela la commande

```bash
$ git show --name-only <identifiant-du-commit>
```

Notez la différence avec
```bash
$ git show  <identifiant-du-commit>
```

# Trucs et astuces
 
## Créer un compte sur GitHub

Créez un compte sur la plateforme de développement collaborative [GitHub](https://github.com/) en cliquant [ici](https://github.com/join).

- Entrez un login, une adresse e-mail et un mot de passe.
- Pensez à valider votre compte en cliquant sur le lien qui vous sera envoyé par e-mail par GitHub.

##  Gérer les fins de lignes

Sous Windows, si Git pose des problèmes avec les fin de lignes, utilisez la commande suivante (une seule fois) :
```bash
$ git config --global core.autocrlf true
```