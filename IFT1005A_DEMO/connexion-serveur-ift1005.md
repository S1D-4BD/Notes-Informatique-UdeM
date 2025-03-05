# **Directives pour la connexion au serveur et le transfert de fichiers via SCP**

---
## Quelques commandes utiles

| **Commande**       | **Description**                                                        | **Exemple**                                                              |     |
| ------------------ | ---------------------------------------------------------------------- | ------------------------------------------------------------------------ | --- |
| `touch`            | Pour créer un fichier                                                  | `touch fichier.ext`                                                      |     |
| `mkdir`            | Pour creer un dossier                                                  | `mkdir dossier`                                                          |     |
| `cd`               | On entre dans le répertoire                                            | `cd /home/utilisateur/Documents`                                         |     |
| `ls`               | Liste les fichiers                                                     | `ls -l`                                                                  |     |
| `cp source target` | Copie un fichier ou un dossier                                         | `cp fichier.txt /home/utilisateur/Bureau/`                               |     |
| `mv source target` | Déplace ou renomme un fichier/dossier                                  | `mv ancien.txt nouveau.txt` ,                `mv fichier.txt /Documents` |     |
| `rm fichier`       | Pour supprime un fichier, fait récursivement avec `-r` pour un dossier | `rm -r dossier/`                                      `rm ficheier`      |     |
| `cat fichier.txt`  | Affiche le contenu d’un fichier complet                                | `cat fichier.txt`                                                        |     |
| ``nano fichier``   | Ouvre le contenu d'un fichier, permet de le modifier!                  | ----                                                                     |     |

**Pour les curieux, il existe un jeu pour apprendre Bash, GameShell**


<div style="page-break-after: always;"></div>


---
## Connexion au serveur de IFT1005

**==Alors premier truc, c'est que OneDrive ça va à la poubelle, une véritable plateforme cancérigène, un complexe ulcère oculaire==. Vos fichiers ne sont pas sauvegardés en local, ils sont sauvegardé chez Microsoft, vous n'avez que des "liens" à vos fichiers**

1. **Get la clé privée de Studium** :
   - Téléchargez votre clé privée depuis Studium, devrait s'appeler ``ift1005.pem``

2. **préparez un répertoire :**
   - Créez un dossier dédié au cours (par exemple: `IFT1005`)
   - Placez votre clé privée dans ce répertoire

3. **Ouvrez PowerShell :**
   - **Windows** : Lancez **PowerShell** en le recherchant dans le menu démarrer
   - **Mac/Linux** : à retravailler

4. **Naviguer vers le répertoire contenant la clé privée** :
   - Utilisez la commande `cd` (change directory) pour accéder au dossier
   - Exemple :  
```bash
C:\Users\DELL cd Documents           (je vais dans Documents à partir de DELL)
C:\Users\DELL\Documents\ cd IFT1005  (je vais dans IFT1005 à partir de Documents)
```

5. **Connexion au serveur :**
   - De là ou se trouve la clé écrivez cette commande pour vous connecter :
```bash
ssh -i ift1005.pem UNIP@ift1005.xyz
```

***Ce que tout ça veux dire :***
- **ssh**:  est le *protocole* de **connexion**
- **Le -i** : est un flag indiquant la façon comment on s'identifiera, dans notre cas on s'identifie avec une clé RSA (le .pem sur Studium)
- **clé.pem** : dans la commande vous devez le remplacer par le nom de votre fichier `.pem`
- **UNIP** : vous devez le remplacer dans la commande par votre identifiant UdeM


<div style="page-break-after: always;"></div>


---
## Comment déposer un travail vers le serveur

**==Vous devez vous déconnecter du serveur pour transférer ou copier un document==, tout se fait dans votre ordi en local** !!
### Déposer un fichier unique

1) Déposez votre travail dans le répertoire de travaux IFT1005, **vous devez voir la clé à ce niveau** 
2) Exécutez cette commande :
```bash
scp -i ift1005.pem NomDuFichier UNIP@ift1005.xyz:
```

***Ce que tout ça veux dire :***
- **scp**:  est le *protocole* de **copie**
- **Le -i** : est un flag indiquant la façon comment on s'identifiera, dans notre cas on s'identifie avec une clé RSA 
- **La structure** : vous déposez le premier argument dans le deuxième

### Déposer un folder de plusieurs fichiers

1) Déposez votre travail dans le répertoire de travaux IFT1005, vous devez voir la clé à ce niveau 
2) Exécutez cette commande :

```bash
scp -i ift1005.pem -r NomDuFichier UNIP@ift1005.xyz:
```

***Ce que tout ça veux dire :***
- **Le -r** : est un flag indiquant la façon comment on copiera le premier argument. Comme c'est un folder on veux copier de façon **RÉCURSIVE** tout son contenu
- **le " : " à la fin**  : c'est le target, le chemin ou va se trouver le fichier

---
## Copier un fichier de votre répertoire situé dans le serveur vers votre ordi

```bash
scp -i ift1005.pem zh77556@ift1005.xyz:fichier .
```

***Ce que tout ça veux dire :***
- **La structure** : vous copiez le premier argument dans le deuxième
- **Important** : le ==point== à la fin signifie que le **chemin du deuxième argument est là où vous êtes**
