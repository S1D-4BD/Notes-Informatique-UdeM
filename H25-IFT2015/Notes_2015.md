
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
---

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
Nombre de *catalan*: 
$$\frac {1}{n+1} {2n \choose n}$$
#### **Parcours préfixé:**

![[prefixe.jpg]]
<div style="page-break-after: always;"></div>

#### **Parcours postfixé:**

![[postfixe.jpg]]
#### **Parcours infixé:**

![[infixe.jpg]]

| PreFixé()                  | Infixé()                   | PostFixé()                 |
| -------------------------- | -------------------------- | -------------------------- |
| visite -> gauche -> droite | gauche -> visite -> droite | gauche -> droite -> visite |

**Arbre plein **
- ==**TOUT** les **nœuds INTERNES** ont **2** enfants==
**Arbre complet : **
- ==**TOUS** les niveaux sont **remplis**, sauf possiblement le dernier, qui est **rempli de gauche à droite** sans trou==

#### Représentation par tableau

| BSF                                                                                                                                                                                                                         | DSF                                                                                                         |
| :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------- |
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
<div style="page-break-after: always;"></div>

Distinction plein vs complet:

**Plein (Propre)** = tout les noeuds internes ont 2 enfants, feuilles en périphérie 
> S'il existe 1 enfant, bah il en faut 2

**Complet** = tout les niveaux sont pleins, sauf le derniers, et tassés à gauche, les feuilles en bas ou 1 niveau plus haut seulement
> S'il existe une feuille, elle est à gauche


---
# Arbres binaire de recherche AVL

Tout arbre binaire de recherche contient une clé de valeur minimale et maximale, ==ne sont pas nécessairement des feuilles== 
- Minimal implique qu'elle n'a pas d'enfant de gauche (inférieur)
- Maximal implique qu'elle n'a pas d'enfant de droite (supérieur)

**Règle de stockage**
$$cle(u)<cle(v)<cle(w)$$

Recherche: 

Soit une clé v recherché, on commence à la racine et on fait des comparaisons successives pour naviguer en O(log(n)) l'arbre 


```java
public NodeAVL recherche(int v){

	int key = v; //la clé quon cherche
	NodeAVL current = this.racine; //la node qu'on visite, init à racine
	if(current.key == v){
		return trouvé;
	}else if (current.key<v){
		recherche(current.left);
	}else if (current.key>v){
		recherche(current.right);
	}else{
		return null;
	}
}
```

### Balancement en AVL

Afin de garder la complexité de recherche en O(log(n)) il est important que la distribution des données soit à peut près égale de part et d'autre d'une racine R. On implique alors que la différence de hauteur pour toute racine R est $|1|$

On liste 4 cas de débalancement/ tactiques de rotation

**Simple gauche: **

```java
public NodeAVL SG(NodeAVL x){  
    NodeAVL y = x.right;  
    NodeAVL T2 = y.left;   
    
    y.left = x;  
    x.right = T2;  
    
    setHauteur(x);  
    setHauteur(y);  
    
    return y;  
}
```

![[simple_gauche.png|474x165]]

**Double gauche:**

![[double_gauche.png|598x157]]

**Simple droite**
``
```java
public NodeAVL SD(NodeAVL y){  
  
    NodeAVL x = y.left; // enfant gauche de y  
    NodeAVL T2 = x.right; //le S.A DROITE DE X  
  
    x.right = y; //x devient PARENT DE Y  
    y.left = T2; //MET LES ENFANTS SUP DE Y A GAUCHE DE Y (CAR INFERIEURS A Y )  
  
    setHauteur(y); //ON CALCULE HAUTEUR  ++PROFOND DES ENFATNS Y, ON FAIT +1  
    setHauteur(x);  
  
    return x;  
}
```

![[simple_droite 1.png|491x176]]

**Double droite**

![[double_droite.png|637x153]]

<div style="page-break-after: always;"></div>
### Ajout / Suppression en AVL

==Attention, la suppression peut causer plusieurs **débalancements**==

On doit aussi vérifier le débalancement de chaque Node, et les corriger des feuilles à la racine

ajouter info 

---
# Encodage de Huffman

Tourne autour de fréquence d'apparition d'une lettre/symbole. Aucune convention, il suffit de rester cohérent
# Exemple :

soit les fréquences :

| a    | b    | c   | d   | e    | f    | g    | h   |
| ---- | ---- | --- | --- | ---- | ---- | ---- | --- |
| 1/16 | 1/32 | 1/8 | 1/2 | 1/32 | 1/16 | 1/16 | 1/8 |

Qu'on change en

| a   | b   | c   | d   | e   | f   | g   | h   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 2   | 1   | 4   | 16  | 1   | 2   | 2   | 4   |

3) On additionne les noeuds plus faibles, et on met en avant le nouveau noeud créé jusquà créer une racine

| ==b== | ==e== | a   | f   | g   | c   | h   | d   |
| ----- | ----- | --- | --- | --- | --- | --- | --- |
| ==1== | ==1== | 2   | 2   | 2   | 4   | 4   | 16  |

| ==be== | ==a== | f   | g   | c   | h   | d   |
| ------ | ----- | --- | --- | --- | --- | --- |
| ==2==  | ==2== | 2   | 2   | 4   | 4   | 16  |

| abe | ==f== | ==g== | c   | h   | d   |
| --- | ----- | ----- | --- | --- | --- |
| 4   | ==2== | ==2== | 4   | 4   | 16  |

| ==abe== | ==fg== | c   | h   | d   |
| ------- | ------ | --- | --- | --- |
| ==4==   | ==4==  | 4   | 4   | 16  |

| abefg | ==c== | ==h== | d   |
| ----- | ----- | ----- | --- |
| 8     | ==4== | ==4== | 16  |

| ==abefg== | ==ch== | d   |
| --------- | ------ | --- |
| ==8==     | ==8==  | 16  |

| ==abecfgch== | ==d==  |
| ------------ | ------ |
| ==16==       | ==16== |

| ==ROOT== |
| -------- |
| ==32==   |

### reconstruire l'arbre

```c++
                    racine
                   /      \
             abecfgch      d
            /      \    
        abefg       ch
	    / \         /\
	 abe    fg     c   h
	 / \    /\        
    a  be  f  g   
       /\
      b  e
```

convention avec 1 à gauche:

| a    | b     | c   | d   | e     | f    | g    | h   |
| ---- | ----- | --- | --- | ----- | ---- | ---- | --- |
| 1111 | 11101 | 101 | 0   | 11100 | 1101 | 1100 | 100 |
la longueur pour coder ca en bits c'est **(nbr bits) * (fréquence)**

| a    | b    | c    | d     | e    | f    | g    | h    |
| ---- | ---- | ---- | ----- | ---- | ---- | ---- | ---- |
| 4(2) | 5(1) | 3(4) | 1(16) | 5(1) | 4(2) | 4(2) | 3(4) |
 -> (8+5+12+16+5+8+8+12 )/32 = **2.3125 bits**
 
---
# Arbres Splay

==Concept vu dans le cours de Operating System/Architecture des ordinateurs==: Politique de stockage de mémoire RAM/Cache en **Last Used At Top**, le dernier élément consulté est mis en ==racine== ***peu importe si l'arbre n'est plus parfaitement balancé***

- **Nouvelle opération par rapport aux arbres AVL/BST**: Splay, qui consiste à faire remonter en racine le Node cherché

### Cas de Splay, Recherche

- Si on **trouve** la Node, on la Splay
- Si on la trouve pas, on Splay la feuille ou on a arrêté de chercher (fin)
### Cas de Splay, Insertion

- On insère la Node en respectant la règle $cle(u)<cle(v)<cle(w)$ 
- On Splay cette Node

### Cas de Splay, Suppression

- On le remplace par son **précédent immédiat** (max du sous-arbre gauche)
- On Splay le parent du max du sous-arbre gauche qui sert maintenant de racine
easy
---
# Arbres 2-4

Concept vu en SQL, un arbre ou la clé de position n'est pas unique mais **multiple**; entre autre, une valeur n'est pas seulement inférieur égale ou supérieur à 1 seule clé mais peut être entre 2,3 ou 4 clés ou supérieur/inférieur à ces clés etc.

---
# Arbre rouge - noir

Comme l'arbre AVL, équilibré mais différemment, respecte 4 propriétés dans le graphe 

Soit $A$ un arbre
1) $\forall \ node \in A, couleur(x) \in \{Rouge, Noir\}$
2) $\exists \ racine \rightarrow \ couleur(racine) = Noir$
3) $\exists \ feuilles \rightarrow \ couleur(feuille) = Noir$
4) $node \in Rouge \rightarrow \ (node.left = node.right) \in Noir$
5) ==À partir de n'importe quelle node, tout les chemins possibles contiennent le même nombre de node Noir==

>Pour savoir quel cas traiter en insertion, c'est l'oncle qui va être primordial au choix, pour la suppression c'est le frère

# Règles

>==Si oncle n'est pas rouge== (donc noir ou inexistant)
>	- rotation
>	- **couleur de l'étage enfant échangée** (coulage de couleur)
>==Si oncle est rouge==
>	- grand-parent **switch** de couleur avec ses enfants

- on ajoute 12, 4 et 20 sans problèmes
- si on add 28, on tombe dans un **cas d'oncle rouge**
- Pour corriger, on fait "couler" la couleur de grand-père vers ses enfants

![[red-black-01.png|607x222]]

### Ajout de 35
- **Cas oncle pas rouge** 
	- Rotation gauche, 28 devient sous racine du sous-arbre problématique
	- On échange les couleurs du nouveau parent (28) et les enfants (28,35)

![[red-black-02.png|601x230]]


### Ajoute 32, 30
- **Cas oncle pas rouge** 
	- Rotation gauche, 32 devient sous racine du sous-arbre problématique
	- On échange les couleurs du nouveau parent (32) et les enfants (30,35)


![[red-black-03 1.png|595x233]]

==Cas spécial; on a **propagé** le problème vers le haut==
- **Cas oncle pas rouge** 
	- Rotation gauche, 28 devient racine
	- 12 devient enfant gauche de racine, 25 devient enfant droit de 12
	- On échange les couleurs du nouveau parent (28) et les enfants (12,32)
	- recoloration de la racine en noir

![[red-black-04.png|595x239]]

![[red-black-05.png|594x187]]

## Suppression

On va essayer de voir ça comme une dette qu'on va payer et rediriger vers un cas supérieur.
==le parent va TOUJOURS demander au frère d'aider==

- Une node double noir est une node endetté, il doit transférer sa dette
- Une node rouge est une node "pas content" de donner de l'argent/en a pas beaucoup pour aider le paiement de la dette
- Une node noir est neutre et sans problème

### Situation, 30 dies, leaf has big debt left

- le parent cheap demande à son autre enfant de donner l'argent pour aider son frère.
- Donc, la dette du leaf disparait, le parent a une dette car il a aidé son fils avec de l'argent emprunté, et le frère devient fâché (rouge) d'avoir donné de l'argent

![[red-black_sup01.png]]

- Le parent qui a hérité de la dette, va demander à son père 28 pour de l'aide, et 28 va déléguer la job à son autre fils 12
- 12 va être **fâché** de donner de l'argent au grand-père pour aider son frère, et le grand-pere hérite de la dette
 
![[red-black_sup02.png]]

Le grand-père il à la retraite, il demande de l'aide à personne, we are done cbon khlass, meme faché cpas grave

### Situation, 30 dies, leaf has big debt left, and brother already pauvre

- Si le frère de l'endetté  (35) est déjà pauvre, le parent (32) ne peut pas demander de l'aide à son enfant
- Le parent va donner de ses économies à l'endetté et va aider, le parent devient rouge
- Puisque le **frère a pour une fois pas été sollicité**, il a l'**occasion de faire des économie et redeviens normal (noir)**

![[red-black_sup03.png]]

- Le parent irresponsable sans économies, devient une **charge** pour son fils, ils échangent de place (**rotation vers problème**) en relation parent/enfant; le fils calme va s'occuper légalement de son père, qui s'occupera d'un des neveu en retour
- Le parent plein d'audace va demander à son **neveu** (33) de lui donner de l'argent pour aider la dette existante dans la famille; 33 est noir il peut aider, mais va devenir fâché/pauvre

![[red-black_sup04.png]]

- Le parent (32) est **déjà dans le rouge**, on va pas lui faire hériter de dette et on va ***oublier*** cette histoire, on arrête

<div style="page-break-after: always;"></div>
### Situation, 30 dies, leaf has big debt left, and brother's son pauvre

![[red-black_sup05.png]]

- 4 crève, problème. 12 va demander de l'argent a son fils 20 qui lui donne mais devient instable financièrement
- La dette est transféré à (12)
- 12 demande de l'aide à son père (28) qui demande à (35)
- MALHEUREUSEMENT le fils de35, donc (32) est déjà pauvre; (35) va préférer aider son fils avant son frère donner ses économie et finir sous sa charge après l'avoir sorti de la misère

![[red-black_sup06.png]]

- Cas spécial; **il faudrait faire échange de couleur entre le parent de 12 et son frère** donc (28) et (32) , ici ca change rien
- On effectue un shift vers le problème pour arranger les tensions 
- ---
# heap

PAS VOIR EXAM, voir cahiers exams

---
# Graphes

Un graphe est un **==réseau de sommets liés entre eux par des arrêtes==**. Un graphe est dit: 

- **Dense** s'il nombre d'arrêtes >> nombre de sommets
- **Éparse** s'il nombre d'arrêtes << nombre de sommets (n-1 au min pour éviter singleton)

### Types de graphes

- **Non orienté** : un graphe ou la direction n'est pas explicitement indiqué, le vecteur **AB = BA** ==(le graphe est symétrique par définition)==
- **Orienté** : les arrêtes ont des sens, le vecteur **AB != BA**

==Attention un chemin explicite comporte les sommets ET les arrêtes==

Un graphe peut être **cyclique** si un chemin entre certains sommet nous retourne à la case départ, si ce chemin est **orienté** il devient un **circuit**

### Définitions importantes

**Connexe**: pour 2 sommets quelconques, **il existe un chemin** (pas nécessairement le plus court, mais il existe) pour les lier

**Couvrant**: appliqué pour les sous-groupes de G, il implique que ce dernier **permet de rejoindre tout les sommets** à partir d'un sommet quelconque, ==mais avec **moins** d'arrêtes que son parent original G==


---
Le **graphe** est **ADT** utilisée pour modéliser des relations entre des entités. Il se compose d’un ensemble de **sommets** et d’un ensemble d’**arêtes** qui relient ces sommets. La file classique permet ces opérations :

- Création : Créer la structure vide initialement
- InsertVertex : Ajouter un sommet
- InsertEdge : Ajouter une arête
- Size : Retourne la longueur de la file
- degree : compte le nombre d arêtes entrantes ou sortantes d'un nœud

**3 structures populaires**

- **liste d'arêtes** : consiste a garder la liste de toutes les arêtes
- **liste d'adjacence** : pour tout sommet, on liste ses arêtes connectées
- **matrice d'adjacence** : matrice de **références**, qui détermine pour un croisement `int[u][v]` si une arête entre ces 2 sommets existe

---

# Parcours en profondeur DFS

```

Soit G un graphe/or arbre 
Soit P une pile

marquer s -> node verifiee 
empiler s

	TANTQUE pile non vide (algo non fini) alors
		u = sommet de pile
		SI u a un voisin v non marquee
			alors
				marquer v -> node verifiee (eviter doublon)
				empiler v
			//
		SINON
			dépiler u -> visitée (backtrack)
		//
	//

```

<div style="page-break-after: always;"></div>
# Parcours en largeur BFS

Algorithme

```
Soit G un graphe/arbre
Soit S une file

marquer s -> node verifiee (pour compter)
enfiler s

	TANTQUE file non vide (algo non fini) alors
		u = head de file
		POUR TOUT voisin v de s
			si v non marqué
				marquer v -> node verifiee
				enfiler v a la queue de file
		     //
		     si marqué skip (évite doublon)
		//
		défiler u de la tête -> visitée
	//		
	

```

<div style="page-break-after: always;"></div>

---
### **Arbre couvrant/minimal**

C'est une collection de **n-1 arrêtes** qui touche à tout les sommets, et minimal en terme de cout par arrete

### **Algorithme de Prim**

Consiste à choisir un sommet s random et , à partir de ce sommet, créer un nuage de sommets en sélectionnant à chaque fois l'arrête de cout la plus petite ne faisant pas parti du nuage. ==On peut commencer à partir de n'importe quel sommet du nuage==

```
Soit S = ensemble des sommets du nuage (initialisé à {s0})
Soit T arbre
TANT QUE S contient pas tous les sommets
    Trouver arrete de poids minimal (u,v) tq :
        u in S et v not in S
    Ajouter v a S
    Ajouter (u,v) a l arbre T

```


# Algorithme Kruskal

Focus sur les arrêtes, ajouter en éviter les cycles, ==toujours s'arreter à n-1 arrêtes==

```
TRI DES ARRETES PAR POIDS PRÉQREQUIS

Tant quon a pas formé de cycle/pas tout visité
	choisir arrete de plus bas niveau
	relier les sommets et former d'eventuels clusters
    == si on a (n-1) arretes -> stop ==
	
```

> ++ arrêtes, -- sommets = PRIM
> -- arrêtes, ++ sommets = KRUSKAL



