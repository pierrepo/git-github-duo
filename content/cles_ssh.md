# Configurer une paire de clés SSH

La combinaison de clés SSH privée et publique est un mécanisme très sécurisé pour accéder à un serveur distant. La connexion est authentifiée par l'utilisation conjointe de la clé privée stockée sur la machine de l'utilisateur (ici le serveur de l'IFB) et de la clé publique stockée sur le serveur distant (ici GitHub).

```{note}
Depuis l’été 2021, GitHub interdit l’authentification par login / mot-de-passe et préconise l’utilisation de clés privée et publique.
```

## Création des clés

Depuis l'interface JupyterLab de l'IFB, ouvrez un terminal Bash.

Créez un répertoire `intro-git` pour cette introduction à git puis déplacez-vous dans ce nouveau répertoire :

```bash
$ mkdir -p /shared/projects/2501_duo/$USER/intro-git
$ cd /shared/projects/2501_duo/$USER/intro-git
```

```{admonition} Rappel
:class: tip
- Ne tapez pas le caractère `$` en début de ligne et faites bien attention aux majuscules et au minuscules.
-  Copiez / collez les commandes pour aller plus vite et faire moins d'erreur.
```

```{note}
Pour information : la [documentation de GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) pour la création de clés SSH.
```

Entrez ensuite la commande suivante :

```bash
$ ssh-keygen -t ed25519 -f ~/.ssh/id_ed25519 -N "" -C "Connexion GitHub DUO"
```

Validez en appuyant sur la touche <kbd>Entrée</kbd>.

Vous devriez obtenir quelque chose du type :

```
The key's randomart image is:
+--[ED25519 256]--+
|                 |
|        .        |
|       . .       |
|      o . . o . o|
|     = =S  ..o +.|
|    o =o*.o. +o O|
|   ..o.o.*o.= oB=|
|    Eoo..  =o. .+|
|  .oo+o.  ...o...|
+----[SHA256]-----+
```

Affichez maintenant le contenu du répertoire `~/.ssh/` :

```bash
$ ls ~/.ssh/
```


```{note}
Le caractère `~` en Bash désigne votre répertoire personnel, qui correspond à `/shared/home/LOGINIFB` où `LOGINIFB` est votre identifiant sur l'IFB. C'est une sorte de raccourci.
```

Dans ce répertoire `~/.ssh/`, vous devriez trouver :

- Le fichier `ed25519` : votre clé privée. À ne communiquer à personne ! Cette clé doit rester secrète.
- Le fichier `ed25519.pub` : votre clé publique, que vous allez déposer sur le site de GitHub.

Toujours dans votre terminal, affichez à l'écran le contenu du fichier `ed25519.pub` :

```bash
$ cat ~/.ssh/id_rsa.pub
```

Vous devriez obtenir une clé qui ressemble à cela :

```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIM7dqRXTCVfdurr1+DqADdTFMNz
5CG9HJCyr65pHL+uz Connexion GitHub DUO
```

Copiez cette clé, depuis `ssh-ed25519` jusqu'à `Connexion GitHub DUO` inclus.


## Ajout de la clé publique dans GitHub

Ouvrez maintenant l'interface de gestion des clés de GitHub : <https://github.com/settings/keys>

```{warning}
Authentifiez-vous si besoin avec vos identifiants GitHub.
```

Cliquez sur le bouton vert « *New SSH key* ».

Indiquez comme titre « Connexion IFB DUO » (sans les guillemets).

Collez votre clé dans le champ *Key* (tout depuis `ssh-ed25519` jusqu'à `Connexion GitHub DUO` inclus).

Enfin, cliquez sur le bouton vert « *Add SSH key* ». Pour confirmer l’ajout de cette clé, GitHub vous demandera éventuellement votre mot de passe utilisateur.

L’ajout d’une clé publique dans votre profil est un moyen de vous authentifier sur GitHub. Cette opération est considérée comme sensible d’un point de vue de la sécurité. Vous recevrez donc également un e-mail de GitHub pour vous informer de l’ajout de cette nouvelle clé.


## Test de la connexion à GitHub

Pour vérifier si l'enregistrement de votre clé publique dans GitHub a bien fonctionné, tapez la commande suivante dans le terminal :

```bash
$ ssh -T git@github.com
```

Validez en tapant `yes` puis en appuyant sur <kbd>Entrée</kbd>.

Si votre clé publique a bien été enregistrée dans GitHub, vous devriez obtenir le message :

```
Hi LOGIN-GITHUB! You've successfully authenticated, but GitHub does not provide shell access.
```
Avec `LOGIN-GITHUB` l'identifiant de votre compte sur GitHub.

Si c'est bien le cas, félicitation. 🎉 Vous serez en mesure de partager votre dépôt git sur GitHub.
