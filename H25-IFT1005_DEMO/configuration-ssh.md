``config`` est un fichier outil personnel qui sert essentiellement à:

1) Simplifier la connexion via SSH
2) Raccourcir les commandes SCP
3) Implémenter une sécurité, que ce soit le fichier d'identité (clé) ou des options additionnelles pour le serveur 

# 1. init

Déplacez vous dans votre ordinateur **à partir du disque (C:)** et rendez-vous jusqu'au répertoire **User** (qui est le nom de vôtre ordinateur ou vous même )

Ça pourrait ressembler à ça:

```bash
C:\Users\DELL
C:\Users\LNV-GSM
C:\Users\Sid-Laptop
C:\Users\PC-de-Yasmine
```

# 2. Existence de .ssh ou non

Vous allez **vérifier** si vous avez déjà le répertoire `.ssh` 


1) S'il existe, faites la prochaine étape
2) S'il n'existe pas, créez simplement un répertoire et appelez le `.ssh`

# 3. Création de config

À partir de Visual studio Code, vous allez faire à partir de la barre de menu **File > Open Folder... >** et ouvrir le répertoire `.ssh`

*Il se peut que le répertoire ne soit pas vide pour certains*

De là vous allez cliquer sur l'icone de création de fichier, appelez le ``config`` et **==ne mettez pas d'extension .txt, c'est un fichier simple, pas texte==**
# 4. Setup de config

Toujours dans VS Code, vous allez spécifier
- alias (nickname du serveur)
- hostname (l'adresse du serveur)
- user (votre unip)
- IdentityFile (le chemin vers votre clé)

Ça pourrait ressembler à ça:

```bash
Host ift1005
	hostname ift1005.xyz
	User ab33444
	IdentityFile C:\Users\admin\Documents\IFT1005\ift1005.pem
```

Et vous avez fini

<div style="page-break-after: always;"></div>



---
Ce que vous pouvez maintenant faire

# Connexion avec config

Déplacez vous avec ``cd`` jusqu'à `.ssh` (et pas où se trouve votre clé), puis tapez `ssh alias-choisi`

Ça pourrait ressembler à ça :

```
ssh ift1005
```

Vous êtes connectés

# SCP local vers serveur

Déplacez vous avec ``cd`` jusqu'à `.ssh` (et pas où se trouve votre clé), puis tapez

```bash
scp chemin\du\fichier alias:
```

Ça pourrait ressembler à ça (**fichier ou répertoire**) :

```bash
scp C:\Users\admin\Documents\dv1.html ift1005:
```

```bash
scp -r C:\Users\admin\Documents\projet ift1005:
```

# SCP serveur vers local

Déplacez vous avec ``cd`` jusqu'à `.ssh` (et pas où se trouve votre clé), puis tapez. 

```bash
scp ift1005:exercice1/msg.txt ../Documents/IFT1005
```

Notez que le ``../`` est très important, il vous permet de "sortir" de ``.ssh`` et donc d'avoir le bon chemin relatif. 
- Par exemple, `Downloads` n'est pas accessible à partir de `.ssh`, il faudrait "reculer" dans ``Users`` pour le voir

```bash
scp -r ift1005:exercice1/projet ../Documents/IFT1005
```
