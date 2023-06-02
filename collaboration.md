# Collaborer avec GitHub

```{hint}
Dans cette partie, vous allez travailler par équipe. Constituez des équipes de 2 ou 3 personnes.
```

## 1. Préparation

Revisionez la vidéo « [Débuter avec Git et Github en 30 min](https://youtu.be/hPfgekYUKgk?t=1058) » à partir de 17'38 sur le dépôt distant et GitHub.

Visionnez également la vidéo « [Démystifions Git, Github, Gitlab (2/3) : Travailler à plusieurs](https://www.youtube.com/watch?v=4xsd8jHyVpk) ».

GitHub est très utile pour du travail collaboratif car il va servir de plateforme centralisée pour organiser un projet.

## 2. Création d'un dépôt distant commun

```{warning}
Les manipulations indiquées dans cette rubrique ne sont à réaliser que par **UN SEUL** membre de l’équipe mais avec, bien sûr, le soutien et l’assistance des autres membres de l’équipe.
```

En reprenant les instructions de la partie « [Premier dépôt](premier_depot.md) » :

- Créez un nouveau dépôt sur GitHub qui porte le nom d'un projet fictif.
- Ajoutez une petite description
- Conservez tous les autres paramètres par défaut (n’initialisez pas le dépôt avec les fichiers proposés).

Cliquez ensuite le bouton gris *SSH* et copiez / collez quelque part l’adresse du dépôt. Par exemple :

```
git@github.com:pierrepo/mon_projet.git
```

Allez ensuite dans la rubrique *Settings* (en haut à droite) puis dans *Collaborators* (à gauche). Entrez votre mot de passe si GitHub vous le demande.

Dans la rubrique *Manage access*, cliquez sur le bouton vert *Add people*.

Entrez un par un le login GitHub (sans le caractère @ au début) des autres membres de l’équipe. Cliquez sur le bouton *Add XXXX to this repository* à chaque fois (voir [exemple](img/github_lucky-leucine_2.png)).

Toutes les personnes que vous avez ajoutées de cette manière recevront une invitation par e-mail qu’ils devront confirmer rapidement. Elles auront ensuite accès à ce dépôt sur GitHub et pourront le modifier.

```{warning}
Ne créez pas un premier fichier directement dans l’interface web de GitHub. Cela posera des problèmes par la suite.
```

## 2. Connexion du dépôt distant au JupyterLab IFB

```{note}
Les manipulations indiquées dans cette rubrique sont à réaliser par tous les membres de l’équipe.
Vérifiez ensemble que tous les membres de l'équipe ont réalisé les différente étapes.
```

Depuis un terminal, déplacez-vous dans votre répertoire de travail pour cette introduction à Unix :

```bash
$ cd /shared/projects/202304_duo/$USER/intro-git
```

Clonez le dépôt distant de votre projet (qui est sur GitHub) sur le JupyterLab de l'IFB :

```bash
$ git clone git@github...
```

où `git@github...` est l'adresse de votre dépôt distant que vous avez copiée précédemment.

Déplacez-vous ensuite dans le répertoire créé.

## 3. Premières modifications

Réalisez maintenant ces actions dans l’ordre en vous répartissant les différents rôles :

1. Un 1er membre de l’équipe crée un fichier `README.md` avec simplement le titre du projet. Il ajoute (`git add`), enregistre (`git commit`) puis envoie ses modifications sur GitHub (`git push`).
2. Vérifiez que les modifications sont bien sur GitHub.
3. Les autres membres de l’équipe récupèrent les modifications dans le JupyterLab (`git pull`).
4. Un 2e membre de l’équipe modifie le fichier `README.md`. Il ajoute (`git add`), enregistre (`git commit`) puis envoie ses modifications sur GitHub (`git push`).
5. Vérifiez que les modifications sont bien sur GitHub.
6. Les autres membres de l’équipe récupèrent les modifications dans le JupyterLab (`git pull`).
7. Un éventuel 3e membre de l’équipe modifie le fichier `README.md`. Il ajoute (`git add`), enregistre (`git commit`) puis envoie ses modifications sur GitHub (`git push`).
8. Vérifiez que les modifications sont bien sur GitHub.
9. Les autres membres de l’équipe récupèrent les modifications dans le JupyterLab (`git pull`).

Une règle pratique, qu’il est indispensable de respecter quand on travaille à plusieurs sur un même dépôt, est de **toujours** récupérer les modifications distantes (sur GitHub) localement (dans le JupyterLab). C’est à dire qu’il faut toujours lancer la commande `git pull` avant de modifier localement les fichiers et avant d’envoyer les modifications sur GitHub (`git push`).

Normalement, si vous avez respecté la séquence d’actions ci-dessus, tout s’est bien passé. 

## 4. Gestion des conflits

Habituellement, vous ne travaillez pas en alternance dans la même pièce. Il est donc tout à fait possible que deux personnes modifient le même fichier presque au même moment. Concrètement, si les co-équipiers 1 et 2 travaillent en même temps sur le même fichier, voici ce qui peut arriver :

1. Co-équipiers 1 et 2 font un `git pull` avant de travailler localement.
2. Co-équipiers 1 et 2 travaillent sur le même fichier, mais chacun sur leur machine.
3. Co-équipier 1 a terminé. Il ajoute et enregistre ses modifications. Il lance un `git pull` puis un `git push`.
4. Co-équipier 2 a terminé à son tour. Il ajoute et enregistre ses modifications. Il lance un `git pull` et obtient un message d’erreur lui indiquant un conflit. Le même fichier ayant été modifié, GitHub ne sait pas comment faire pour prendre en compte toutes les modifications.
5. Co-équipier 2 ouvre le fichier et choisit quelles modifications conserver, puis élimine les lignes débutant par `<<<<<<<`, `=======` et `>>>>>>>` (voir [procédure](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line)). Il ajoute et enregistre ses modifications. Il lance enfin un `git pull` puis un `git push`.

## 5. GitHub flow

Avec la méthode de travail précédente, tous les co-équipiers travaillent dans la même branche (*master*). Chacun modifie les fichiers qu’il veut sans que les autres soient nécessairement d’accord.

Il existe une méthodologie plus sophistiquée et plus inclusive appelée [GitHub flow](https://docs.github.com/en/get-started/quickstart/github-flow) qui permet de discuter des différentes modifications apportées.

À partir d’un unique dépôt GitHub, accessible à tous les participants du projets, ceux-ci vont :

- Créer une branche pour ajouter une fonctionnalité.
- Apporter des modifications dans cette branche (ajout, suppression ou modification de fichiers) par des *commits* successifs.
- Proposer un *pull request* depuis l’interface GitHub.
- Discuter de ce *pull request* et apporter d’éventuelles modifications supplémentaires. (voir un [exemple de discussion](https://github.com/patrickfuchs/buildH/pull/120))
- Accepter ce *pull request* en fusionnant puis supprimant la branche sur GitHub.
- Enfin, localement, récupérer les modifications depuis GitHub avec `git pull` et supprimer la branche fusionnée.

![](img/github-flow.png)
