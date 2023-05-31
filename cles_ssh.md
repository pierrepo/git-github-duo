# Configurer une paire de clés SSH

La combinaison de clés SSH privée et publique est un mécanisme très sécurisé pour accéder à un serveur distant. La connexion est authentifiée par l'utilisation conjointe de la clé privée stockée sur la machine de l'utilisateur et de la clé publique stockée sur le serveur distant.

Depuis l’été 2021, GitHub interdit l’authentification par login / mot-de-passe et préconise l’utilisation de clés privée et publique.

## 1. Création des clés

Depuis l'interface JupyterLab de l'IFB, ouvrez un terminal Bash.

Créez un répertoire `intro-git` pour cette introduction à git puis déplacez-vous y :

```bash
$ mkdir -p /shared/projects/202304_duo/$USER/intro-git
$ cd /shared/projects/202304_duo/$USER/intro-git
```

```{admonition} Rappel
:class: tip
- Ne tapez pas le caractère `$` en début de ligne et faites bien attention aux majuscules et au minuscules.
-  Copiez / collez les commandes pour aller plus vite et faire moins d'erreur.
```

Entrez ensuite la commande suivante :

```bash
$ ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -N "" -C "Connexion GitHub DUO"
```

Validez en appuyant sur la touche <kbd>Entrée</kbd>.

Vous devriez obtenir quelque chose du type :

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


```{note}
Le symbole `~` en Bash désigne votre répertoire personnel, qui correspond à `/shared/home/LOGINIFB` où `LOGINIFB` est votre identifiant sur l'IFB. C'est une sorte de raccourci.
```

Dans ce répertoire `~/.ssh/`, vous devriez trouver :

- Le fichier `id_rsa` : votre clé privée. À ne communiquer à personne ! Cette clé doit rester secrète.
- Le fichier `id_rsa.pub` : votre clé publique, que vous allez déposer sur le site de GitHub.

Toujours dans votre terminal, affichez à l'écran le contenu du fichier `id_rsa.pub` :

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
TRTPvbaUnz17wffw== Connexion GitHub DUO
```

Copiez cette clé, depuis `ssh-rsa` jusqu'à `Connexion GitHub DUO` inclus.


## 2. Ajout de la clé publique dans GitHub

Ouvrez maintenant l'interface de gestion des clés de GitHub : <https://github.com/settings/keys>

*Authentifiez-vous si besoin.*

Cliquez sur le bouton vert « *New SSH key* ».

Indiquez comme titre « Connexion DUO » (sans les guillemets).

Collez votre clé dans le champ *Key* (tout depuis `ssh-rsa` jusqu'à `Connexion GitHub DUO` inclus).

Enfin, cliquez sur le bouton vert « *Add SSH key* ». Pour confirmer l’ajout de cette clé, GitHub vous demandera éventuellement votre mot de passe utilisateur.

L’ajout d’une clé publique dans votre profil est un moyen de vous authentifier sur GitHub. Cette opération est considérée comme sensible d’un point de vue de la sécurité. Vous recevrez donc également un e-mail de GitHub pour vous informer de l’ajout de cette nouvelle clé.


## 3. Test de la connexion à GitHub

Pour vérifier si l'enregistrement de votre clé publique dans GitHub a bien fonctionné, tapez la commande suivante dans le terminal :

```bash
$ ssh -T git@github.com
```

Validez en tapant `yes` puis en appuyant sur <kbd>Entrée</kbd>.

Si votre clé publique a bien été enregistrée dans GitHub, vous devriez obtenir le message :

```
Hi LOGINGITHUB! You've successfully authenticated, but GitHub does not provide shell access.
```
Avec `LOGINGITHUB` l'identifiant de votre compte sur GitHub.

Si c'est bien le cas, félicitation 🎉 Vous serez en mesure de partager votre dépôt git sur GitHub.
