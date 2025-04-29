# DEMO 2

#### Votre objectif est de remettre en place un site web en total désordre.

#### Vous devrez explorer les fichiers, corriger des erreurs dans le code, et réorganiser les ressources

Vous allez pouvoir comprendre comment organiser vos travaux,
et si possible, garder les bonnes pratiques de travail :)


----------------------------------------------------------------------------------------------------------
### Problème # 1 :

**Il y a une erreur dans le projet à remettre, on a une page qui est mal nommée**

- Trouvez ou est cette mauvaise page
- Renommez la `contact` avec l'astuce `mv`
- Note : *elle doit être au même niveau que index.html et accueil.html*
### Problème # 2:

**Le fichier style ne stylise rien... car il n'est pas au bon endroit (et est donc illisible par nos pages)**
- Trouvez le fichier style.css
- Déplacez style.css dans le répertoire css/ avec `mv`
### Problème # 3:

**J'ai gardé une image, `photo.jpg`, dans backups, mais comme on doit l'utiliser, elle doit être dans le répertoire images/, lui-même *dans* ressources/**

- Travaillez avec les chemins relatifs pour utiliser correctement `mv`
- Note: Si vous avez de la difficulté avec les chemins relatifs,
  utilisez `pwd` pour savoir où vous êtes actuellement

| ****  | **signification**                                 |
| ----- | ------------------------------------------------- |
| `pwd` | Donne le chemin pour arriver là où on esr         |
| `.`   | Répertoire courant                                |
| `..`  | Répertoire parent                                 |
| `../` | Te ramène au répertoire parent                    |
| `./`  | Pour accéder à un folder à partir de là où on est |
| `~/`  | Est la même chose que `/home/unip/`               |

### Problème # 4:

**Dans la page mal nommée du problème # 1, il manque aussi son "titre" (le nom de la page)**

- Utilisez `nano fichier.html` afin d'éditer cette page
- Écrivez le nom de cette page **entre les balises** < titre > < /titre >
- ex . < titre > TITRE DE LA PAGE< /titre >  

<div style="page-break-after: always;"></div>




### Problème # 5:

**Il y a 3 textes cryptés dans le projet, 1 seul d'entre eux contient la séquence "udem"... et on veux garder seulement celui-là**

- avec `grep "mot" fichier.html` , trouvez quel fichier contenait "udem" caché dedans
- Supprimez les autres fichiers inutiles avec `rm`
### Problème # 6: 

**Vous n'avez plus besoin de test, ni même du contenu à l'intérieur

- Supprimez récursivement `test` avec `rm -r` et le **flag approprié**

### Problème # 7:

**Là que le projet est en ordre, vous devez copier via SCP seulement le répertoire projet/**

- Utilisez le protocol `scp` depuis votre terminal local
  et utilisez les bons arguments pour la copie

---
