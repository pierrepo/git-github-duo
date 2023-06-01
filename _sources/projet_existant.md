# Explorer un projet existant

```{note}
Cette section est l'occasion d'explorer l'historique d'un dépôt git et d'utiliser les commandes `git log` et `git show`.
```

J'ai développé il y a quelques années le logiciel [autoclasswrapper](https://github.com/pierrepo/autoclasswrapper), un wrapper Python pour le programme de classification bayesienne  [AutoClass C](https://ti.arc.nasa.gov/tech/rse/synthesis-projects-applications/autoclass/autoclass-c/). Ce travail a été publié dans *The Journal of Open Source Software* en [2019](https://joss.theoj.org/papers/10.21105/joss.01390).

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

où `LOGINIFB` est votre identifiant IFB.

## 1. Téléchargement du projet

Téléchargez l'intégralité du projet *autoclasswrapper* avec la commande :

```bash
$ git clone https://github.com/pierrepo/autoclasswrapper.git
```

puis déplacez-vous dans le répertoire du projet :

```bash
$ cd autoclasswrapper
```

La commande `git clone` ne télécharge pas seulement les fichiers du projet mais aussi tout son historique de dévelopement. Vous allez maintenant utiliser différentes commandes git pour explorer ce projet et répondre aux questions suivantes.

## 2. Exploration de l'historique du projet

### De quand date le dernier *commit* ?

Astuce : combinez les commandes `git log` et `head`.


### Quand a été créé le tout premier *commit* ?

Astuce : combinez les commandes `git log` et `tail`.


### Combien de *commits* ont été enregistrés jusqu'à présent ?

Astuce : combinez les commandes `git log`, `grep -c` et un mot-clé pertinent.

Vérifiez cette valeur sur le site du dépôt : <https://github.com/pierrepo/autoclasswrapper>

### Trouvez dans quel *commit* j'ai ajouté la possibilité de construire un dendrogramme

Astuces : 

- Combinez les commandes `git log`, `grep -B4` et un mot-clé pertinent.
- Utilisez le mot dendrogramme en Anglais (voir la page [Wikipédia](https://en.wikipedia.org/wiki/Dendrogram)).


### Combien de fichiers ont été modifiés dans le *commit* correspondant ?

Utilisez pour cela la commande

```bash
$ git show --name-only IDENTIFIANT-DU-COMMIT
```

avec `IDENTIFIANT-DU-COMMIT` l'identifiant du *commit* intéressant. 

**Aides :** 

- L'identifiant du commit débute par `2d1c`.
- Vous n'avez pas besoin d'entrer l'identifiant complet, les 6 premiers caractères devraient suffire.

Notez la différence avec la commande :

```bash
$ git show IDENTIFIANT-DU-COMMIT
```

Pressez la touche <kbd>q</kbd> pour quitter.

