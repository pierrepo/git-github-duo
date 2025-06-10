# Explorer un projet existant

```{note}
Cette section est l'occasion d'explorer l'historique d'un dépôt git et d'utiliser les commandes `git log` et `git show`.
```

J'ai développé il y a quelques années le logiciel [autoclasswrapper](https://github.com/pierrepo/autoclasswrapper), un *wrapper* Python pour le programme de classification bayesienne  [AutoClass C](https://ti.arc.nasa.gov/tech/rse/synthesis-projects-applications/autoclass/autoclass-c/). Ce travail a été publié dans *The Journal of Open Source Software* en [2019](https://joss.theoj.org/papers/10.21105/joss.01390).

Depuis un terminal dans JupyterLab, déplacez-vous dans le répertoire de travail pour cette introduction à git :

```bash
$ cd /shared/projects/2501_duo/$USER/intro-git
```

```{admonition} Rappel
:class: tip
- Ne tapez pas le caractère `$` en début de ligne et faites bien attention aux majuscules et au minuscules.
-  Copiez / collez les commandes pour aller plus vite et faire moins d'erreur.
```

Vérifiez que vous êtes dans le bon répertoire :

```bash
$ pwd
/shared/projects/2501_duo/LOGINIFB/intro-git
```

où `LOGINIFB` est votre identifiant IFB.


## Téléchargement du projet

Téléchargez l'intégralité du projet *autoclasswrapper* avec la commande :

```bash
$ git clone https://github.com/pierrepo/autoclasswrapper.git
```

puis déplacez-vous dans le répertoire du projet :

```bash
$ cd autoclasswrapper
```

La commande `git clone` ne télécharge pas seulement les fichiers du projet, mais aussi tout son historique de développement. Vous allez maintenant utiliser différentes commandes git pour explorer ce projet et répondre aux questions suivantes.


## Exploration de l'historique du projet

### De quand date le dernier *commit* ?

Aide : combinez les commandes `git log` et `head`.

````{admonition} Cliquez pour afficher la solution
:class: dropdown

Le caractère `|` (obtenu avec la combinaison de touches <kbd>AltGr</kbd> + <kbd>6</kbd>) est le *pipe* qui permet de chainer deux commandes Unix.

```bash
$ git log | head
commit af43dd833e5586386098d1793a59332e968069da
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Fri Jul 26 00:23:54 2019 +0200

    Add JOSS badge

commit 304556ecb2b7811d8b3b2cc54c91b015620b435e
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Thu Jul 25 23:48:20 2019 +0200
```

Par défaut, `head` affiche uniquement les 10 premières lignes.

Ici, le dernier *commit* est celui qui commence par `af43dd8` et date du 26 juillet 2019.

```bash
commit af43dd833e5586386098d1793a59332e968069da
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Fri Jul 26 00:23:54 2019 +0200

    Add JOSS badge
```

Chaque *commit* comporte un identifiant unique (`af43dd8`), un auteur (`Author:`), une date (`Date:`) et un message (`Add JOSS badge`).
````

### Quand a été créé le tout premier *commit* ?

Aide : combinez les commandes `git log` et `tail`.

````{admonition} Cliquez pour afficher la solution
:class: dropdown

De la même manière que précédemment :

```bash
$ git log | head
commit af43dd833e5586386098d1793a59332e968069da
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Fri Jul 26 00:23:54 2019 +0200

    Add JOSS badge

commit 304556ecb2b7811d8b3b2cc54c91b015620b435e
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Thu Jul 25 23:48:20 2019 +0200

[ppoulain@cpu-node-22 autoclasswrapper]$ git log | tail
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Thu Jan 25 22:54:06 2018 +0100

    Fix typo

commit 6a1010f0797412743408e58ca28db4a5308e668a
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Fri Jan 19 14:08:19 2018 +0100

    Initial commit
```

Le tout premier *commit* est celui qui commence par `6a1010f` et date du 19 janvier 2018.

````

### Combien de *commits* ont été enregistrés jusqu'à présent ?

Aide : combinez les commandes `git log`, `grep -c` et un mot-clé pertinent.

Vérifiez cette valeur sur le site du dépôt : <https://github.com/pierrepo/autoclasswrapper>

````{admonition} Cliquez pour afficher la solution
:class: dropdown

Réexaminons la structure d'un *commit* (par exemple le tout dernier) :

```bash
commit af43dd833e5586386098d1793a59332e968069da
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Fri Jul 26 00:23:54 2019 +0200

    Add JOSS badge
```

On peut essayer de compter le nombre de fois que le mot « *commit* » apparait dans le `git log` pour obtenir le nombre total de *commits* pour ce projet :

```bash
$ git log | grep -c commit
307
```

Mais la nombre de *commits* visibles sur le [dépôt GitHub](https://github.com/pierrepo/autoclasswrapper) du projet est 306. Effectivement, le tout premier *commit* contenant dans le message associé aussi le mot « *commit* ». Ce n'est donc pas la bonne stratégie.

On peut plutôt compter le nombre de fois que l'expression « `Author:` » (avec la majuscule et les deux points) :

```bash
$ git log | grep -c "Author:"
306
```

````


### Trouvez dans quel *commit* j'ai ajouté la possibilité de construire un dendrogramme

Aide : 

- Combinez les commandes `git log`, `grep -B4` et un mot-clé pertinent.
- Utilisez le mot dendrogramme en anglais (voir la page [Wikipédia](https://en.wikipedia.org/wiki/Dendrogram)).

````{admonition} Cliquez pour afficher la solution
:class: dropdown

Un dendrogramme se dit en anglais « *dendrogram* ». C'est donc ce mot-clé que nous allons rechercher avec `grep`.

L'option `-B4` de `grep` affiche la ligne qui contient le motif recherché ainsi que les 4 lignes précédentes (`B` pour *before*).

```bash
$ git log | grep -B4 dendrogram
commit 193d1a6bbaae7e423b02617a50a14a1778032a32
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Thu Dec 27 15:38:54 2018 +0100

    Fix wrong/missing margin in dendrogram
--
commit 4910ffec7ced9216241ddea263b3e6f2418b6e66
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Thu Dec 27 11:50:37 2018 +0100

    Rewrite dendrogram method
--
commit 2d1c40b7146eeae098b99d8414bcdbb7de599e29
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Thu Jul 12 19:12:31 2018 +0200

    Build dendrogram of classes/clusters
```

Les différentes réponses sont séparées par `--`. Trois *commits* sont concernés par l'implémentation du dendrogramme. Le premier *commit* (avec comme identifiant `2d1c40b7146eeae098b99d8414bcdbb7de599e29`) est  :

```bash
commit 2d1c40b7146eeae098b99d8414bcdbb7de599e29
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Thu Jul 12 19:12:31 2018 +0200

    Build dendrogram of classes/clusters
```

````


### Combien de fichiers ont été modifiés dans le *commit* correspondant ?

Utilisez pour cela la commande

```bash
$ git show --name-only IDENTIFIANT-DU-COMMIT
```

avec `IDENTIFIANT-DU-COMMIT` l'identifiant du *commit* intéressant. 

Aide :

- L'identifiant du commit débute par `2d1c`.
- Vous n'avez pas besoin d'entrer l'identifiant complet, les 6 premiers caractères devraient suffire.

````{admonition} Cliquez pour afficher la solution
:class: dropdown

L'identifiant du *commit* concerné est `2d1c40b7146eeae098b99d8414bcdbb7de599e29`.

```bash
$ git show --name-only 2d1c40
commit 2d1c40b7146eeae098b99d8414bcdbb7de599e29
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Thu Jul 12 19:12:31 2018 +0200

    Build dendrogram of classes/clusters
    
    - based on hierarchical clustering of classes
    - requires scipy and matplotlib dependencies

CHANGELOG.md
Pipfile
Pipfile.lock
autoclasswrapper/output.py
```

Les fichiers modifiés dans ce *commit* sont `CHANGELOG.md`, `Pipfile`, `Pipfile.lock` et `autoclasswrapper/output.py`, soit **4** fichiers.

````

Notez la différence avec la commande :

```bash
$ git show IDENTIFIANT-DU-COMMIT
```

Pressez la touche <kbd>q</kbd> pour quitter.

````{admonition} Cliquez pour afficher la solution
:class: dropdown

La commande `git show` sans l'option `--name-only` affiche le contenu des fichiers modifiés dans le *commit*.

```bash
$ git show 2d1c40
commit 2d1c40b7146eeae098b99d8414bcdbb7de599e29
Author: Pierre Poulain <pierre.poulain@cupnet.net>
Date:   Thu Jul 12 19:12:31 2018 +0200

    Build dendrogram of classes/clusters
    
    - based on hierarchical clustering of classes
    - requires scipy and matplotlib dependencies

diff --git a/CHANGELOG.md b/CHANGELOG.md
index 42e20f5..6a65232 100644
--- a/CHANGELOG.md
+++ b/CHANGELOG.md
@@ -3,6 +3,7 @@
 - output class probability for every gene/protein
 - simplify the calculation of cluster stats
 - class/cluster numbering starts at 1 (0-based in autoclass output)
+- add dendrogram of classes
 
 **0.1.12**
 - update write_cluster_stats() methods with mean/std column
diff --git a/Pipfile b/Pipfile
index b04bf2a..996b3d0 100644
--- a/Pipfile
+++ b/Pipfile
@@ -7,6 +7,8 @@ verify_ssl = true
 numpy = "*"
 pandas = "*"
 chardet = "*"
+scipy = "*"
+matplotlib = "*"
[...]
```

````
