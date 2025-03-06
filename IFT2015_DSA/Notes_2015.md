

---
attente = file
retour arriere =pile
hierarchie= arbre

---

# Piles

L'abstraction de donnée sert à spécifier les données utilisées, les opérations possibles et les possibles erreurs (ex. la pile défini les données stockées, le push le pop et défini l erreur du stackOverFlow). ==C'est utile pour la réutilisation et la modification==
# **Structures de données linéaires**

Ce sont des collections d'éléments **organisés séquentiellement** tel:

- **Les piles (Stacks)** : LIFO (Last In, First Out)
- **Les tableaux (Array)** : Accès rapide mais taille fixe
- **Les listes chaînées (Linked List)** : Taille dynamique, mais accès plus len
- **Les files (Queues)** : FIFO (First In, First Out)
## 1. Piles

**Concept: Last in First Out**

>[!Trick] 
>Lorsqu'on veut faire un **retour arrière**, on utilise une **pile**


**Notation post-fixée** : Format d'expressions mathématiques qui facilite l'interprétation des opérations, ==pas besoin des parenthèse==. L'**empilement** consiste à **entrer des valeurs**, le **dépilement** consiste à effectuer une **opération** lorsqu'on croise un opérateur



Exemple: 1 2 3 + 4 5 6 * - 7 * + - 8 9 * +

|       | ==*==   |           |                |              |               |              |       |              |
| ----- | ------- | --------- | -------------- | ------------ | ------------- | ------------ | ----- | ------------ |
|       | 6       | ==-==     | ==*==          |              |               |              |       |              |
| ==+== | 5       | 5* 6 = 30 | 7              | ==+==        |               | ==*==        |       |              |
| 3     | 4       | 4         | ==4-30 = -26== | -26*7 = -182 | ==-==         | 9            | ==+== |              |
| 2     | 2+3 = 5 | 5         | 5              | 5            | 5 -182 = -177 | 8            | 72    | $$$          |
| 1     | 1       | 1         | 1              | 1            | 1             | 1 + 177 =178 | 178   | 178+72 = 250 |

---


=======
Exemple: 1 2 3 + 4 5 6 * - 7 * + - 8 9 * +

|       |         |           |                |              |               |              |       |              |
| :---: | :-----: | :-------: | :------------: | :----------: | :-----------: | :----------: | :---: | :----------: |
|       |  ==*==  |           |                |              |               |              |       |              |
|       |    6    |   ==-==   |     ==*==      |              |               |              |       |              |
| ==+== |    5    | 5* 6 = 30 |       7        |    ==+==     |               |    ==*==     |       |              |
|   3   |    4    |     4     | ==4-30 = -26== | -26*7 = -182 |     ==-==     |      9       | ==+== |              |
|   2   | 2+3 = 5 |     5     |       5        |      5       | 5 -182 = -177 |      8       |  72   |     $$$      |
|   1   |    1    |     1     |       1        |      1       |       1       | 1 + 177 =178 |  178  | 178+72 = 250 |

Opérations : pop push top isEmpty

<div style="page-break-after: always;"></div>


---
## **2. Listes**

**Les listes ordonnent leurs datas et permettent ces opérations :**

- Création 
- Ajout
- Suppression
- Remplacement
- Recherche
### Liste : Tableau Statique

Un tableau ==a **une taille initiale et un système d'indexation**==

>ces propriétés sont ==toujours **connues**== à la demande :  $O(1)$ 

La **recherche** d'un élément nécessite de traverser les index **jusqu'à trouver la valeur voulue**, on aura 
- `O(1) si c'est le premier`
- `O(n) si c'est le dernier`

> L'**insertion** implique de vérifier **sil y a assez de place** pour le nouvel élément sinon on **agrandi** le tableau. Si on insère au début, on doit reculer tout les éléments de 1 places, donc O(n), si on insère à la fin et que le tableau n'est pas vide, c'est
- `O(1)`

> L'**agrandissement** implique de copier tout le tableau A vers un tableau B de taille généralement doublée, puis de réaffecter la référence de A au tableau doublé B
- `O(n)`

### Liste : Simplement Chaînée

Une liste chainée n'a ==pas de système d'**indexation**==; les éléments **==ne sont pas cotes à cotes==**, ils possèdent chacun un **pointeur** vers l'adresse du prochain nœud.

Une **liste simplement chaînée** est une collection de **nœuds**. Chaque nœud contient :

- **Une valeur** (donnée stockée)
- **Un pointeur** vers le nœud suivant

<div style="page-break-after: always;"></div>


**Opérations principales :**

- `size()`: Nbr d'éléments dans la liste
	- `while next != null`
	- `count++`
- `isEmpty()`: Vérifie si la liste est vide 
	- `reutrn (head==null)
- `addFirst(e)`: Ajoute un élément en début de liste 
	- `e.next = head`
	- `head = e`
- `addLast(e)`: Ajoute un élément en fin de liste
	- `tail.next = e`
	- `e.next = null`
	- `e =tail`
- `removeFirst()`: Supprime et **retourne** le premier élément

> L'accès à un élément et la recherche d'un élément vont demander de traverser chaque node et pointeur (via `next`) jusqu'à trouver l'élément ayant la valeur qu'on cherche `O(n)`

### Liste : Doublement Chaînées

Dans la **liste doublement chaînée**, chaque nœud a **deux pointeurs** :

- **Une valeur** (donnée stockée)
- Un pointeur vers le **nœud précédent**
- Un pointeur vers le **nœud suivant**

**Avantages :** Accès plus rapide aux nœuds (avec les **précédents**)
**Désavantage**: Lourd espace mémoire

### Listes : Circulaires

Une **liste circulaire** est une liste chaînée où le dernier pointe vers le premier `tail.next = head`
### Liste : Positionnelles 

truc cool ça, va régler les problèmes des listes chainées qui sont que :

- l'accès vraiment pas vite aux éléments (O(n)) on dois toujours les chercher même si on a déjà fais un recherche précédente
- insertion/suppression on joue trop avec les pointeurs direct des éléments (même avec tail)

<div style="page-break-after: always;"></div>



**==GROS AJOUT DES LISTES POSITIONNELLES : POSITION==**

***Soit une banque avec des gens qui sont en attente***

Dans un **tableau**, chaque client se tient **sur une case numérotée au sol**.

>**Problème :**
- Si un **nouveau client veut entrer au milieu**, il faut **faire reculer tout le monde** d’une place.
- C'est **lent** car chaque personne doit bouger.

dans la liste doublement chainée **les clients ne sont pas sur des cases**, ils connaissent juste leur voisin :

- A sait qu’il est devant B.
- B sait qu’il est entre A et C.
- C sait qu’il est derrière B.

>**Problème :**
- Si on veut insérer quelqu'un **avant B**, il faut **compter les têtes** pour savoir où est B.
- C'est plus flexible que le tableau, mais il faut chercher la position

>==Mais, si j'organisait  un **système de tickets numérotés** dès l'arrivée, j'aurais pas besoin de chercher==

- Si je veux retrouver un client, **je regarde son ticket**, pas besoin de compter les têtes
- L’accès est **instantané** (O(1)) car chaque ticket **est un pointeur direct vers la personne**.

**Exemple :**

1. **A arrive**, il reçoit le ticket `#001`, et la banque garde un **lien direct vers A**.
2. **B arrive**, il reçoit `#002`, et on garde un **lien direct vers B**.
3. **C arrive** et doit être avant B. On regarde le ticket `#002` en mémoire et on insère C avant B.
4. Si **B part**, son **ticket** `#002` ne peut pas être réutilisé, **on le jette**

> **Avec un système de tickets, on peut insérer quelqu’un à la bonne place sans "parcourir la file"** $\rightarrow$ O(n)

<div style="page-break-after: always;"></div>


#### Méthodes positionnelles

| method()              |                                  | O()    |
| --------------------- | -------------------------------- | ------ |
| **`size()`**          | return nombre d’éléments         | `O(1)` |
| **`isEmpty()`**       | si la liste est vide             | `O(1)` |
| **`first()`**         | return la première **position**  | `O(1)` |
| **`last()`**          | return la dernière **position**  | `O(1)` |
| **`before(p)`**       | return la **position** avant `p` | `O(1)` |
| **`after(p)`**        | return la **position** après `p` | `O(1)` |
| **`addFirst(e)`**     | Add un élément au debut          | `O(1)` |
| **`addLast(e)`**      | Add un élément à la fin          | `O(1)` |
| **`addBefore(p, e)`** | Insere un élément avant `p`      | `O(1)` |
| **`addAfter(p, e)`**  | Insere un élément après `p`      | `O(1)` |
| **`set(p, e)`**       | Remplace la valeur a `p`         | `O(1)` |
| **`remove(p)`**       | Supprime l’élément à `p`         | `O(1)` |
<div style="page-break-after: always;"></div>

## **3. Listes généralisées**

![[liste_gen.jpg]]


<div style="page-break-after: always;"></div>


---
## **4. Files**

>[!Trick]
>Lorsqu'on veut avoir en première position le plus ancien élément et donc respecter un ordre **chronologique**, on utilise une **file**

La file est une ADT respectant l'ordre **FIFO** (l'élément en tête de file est retiré en premier, l'ajout le plus récent est mis en queue de file). La file classique permet ces opérations :

- Création : Créer la structure vide initialement
- Enqueu : Ajouter en queue de file un nouvel élément
- Dequeue : Retirer l'élément en tête de file
- Size : Retourne la longueur de la file
- VérifVide : Booléenne pour vérifier la saturation **

**Opérations principales :**

- `enqueue(e)`: Ajoute un élément à la fin.
    - `tail.next = e; tail = e` (si `tail` est `null`, `head = e` aussi)
- `dequeue()`: Retire un élément au début.
    - `if head == null, return null` (file vide)
    - `temp = head; head = head.next; return temp`
- `isEmpty()`: Vérifie si la file est vide.
    - `return head == null`


## Implémentations

Dans tous les cas, l’accès aux **deux extrémités** se fait en **O(1)** :

- **FRONT** : Accès au premier élément
- **REAR** : Accès au dernier élément
<div style="page-break-after: always;"></div>


#### File classique

>Va gaspiller de l'espace si on a pas un début se trouvant toujours à la case 0, décalage lourd
#### File circulaire 

>Optimise l'espace en effectuant des retours au début (cyclique comme un modulo N.

==**La taille d'une file circulaire dépend de la position cyclique du FRONT et REAR**==

>**Taille cyclique**:   $(rear - front + N + 1) \% N$
>**File vide**:  $r = f - 1$ (sinon elle est juste saturée)

#### File 2 cotés (Double Ended Queue)
Soit le problème d'un impatient **dernier client qui veux quitter la file**, il aurait le droit de quitter la file même s'il n'est pas en avant; même chose pour un **client prioritaire qui dépasserait tout le monde**

On va ajouter la possibilité de
- dequeue en avant : **deleteFirst()** 
- enqueue à la fin : **addLast()**

<div style="page-break-after: always;"></div>


---
# **Structures de données non linéaires**
# 5. Arbres

Un arbre est une structure de donnée **non linéaire** (on ne peut pas tracer une flèche unique qui relierait tout les éléments un à un) fonctionnant par relation parent/enfant. Chaque arbre contient :

- **Nœud**: élément ayant une valeur et une ref vers ses enfants
- **Racine**: Nœud originel, aucun parent
- **Feuille**: Nœud n'ayant aucun enfant
- **Nœud Interne**: Nœud ayant 1 parent et au minimum 1 enfant
- **Ancêtre**: Tout nœud dans le chemin allant de la racine jusqu'à un nœud en particulier
- **Hauteur**: de profondeur 0 à profondeur de la feuille la plus loin de la racine

Permutations des noeuds d'un arbre à n noeuds
Nombre de catalan: 
$$\frac {1}{n+1} {2n \choose n}$$
#### **Parcours préfixé:**

![[prefixe.jpg]]
<div style="page-break-after: always;"></div>

#### **Parcours postfixé:**

![[postfixe.jpg]]
#### **Parcours infixé:**

![[infixe.jpg]]

| PreFixé()         | Infixé()          | PostFixé()        |
| ----------------- | ----------------- | ----------------- |
| visite()          | traverse.gauche() | traverse.gauche() |
| traverse.gauche() | visite()          | traverse.droite() |
| traverse.droite() | traverse.droite() | visite()          |

Arbre plein 
- ==**TOUT** les **nœuds INTERNES** ont **2** enfants==
Arbre complet : 
- ==**TOUS** les niveaux sont **remplis**, sauf possiblement le dernier, qui est **rempli de gauche à droite** sans trou==

#### Représentation par tableau

| BSF                                                                                                                                                                                                                         | DSF                                                                                                         |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| <br>Si c'est pas la racine<br>	return<br>creer la file []<br><br>tant que la file pas vide<br>	défile val<br>	print val<br>	si val.gauche existe <br>		push dans file<br>	si val.droite existe<br>		push dans file<br>	<br> | <br>préfixé()<br>si gauche existe<br>	visite préfixé(gauche)<br>si droite existe<br>	visite prefixe(droite) |
#### Représentation par tableau (conversion)

Soit un **nœud v** :
- **La racine est toujours à l'index 0** :

| Relation          | Formule                    |
| ----------------- | -------------------------- |
| **Enfant gauche** | `index = (2 * parent) + 1` |
| **Enfant droit**  | `index = 2 * parent + 2`   |
| **Parent**        | `index = (enfant - 1) / 2` |
| **Feuille?**      | `si 2i > n`                |

---
# Arbres de recherche

Tout arbre contient une clé de valeur minimale et maximale, ==ne sont pas nécessairement des feuilles== 
- Minimal implique qu'elle n'a pas d'enfant de gauche (inférieur)
- Maximal implique qu'elle n'a pas d'enfant de droite (supérieur)

>>>>>>> f2c841a (notes update)
