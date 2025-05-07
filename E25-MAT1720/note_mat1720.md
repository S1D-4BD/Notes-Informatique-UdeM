---

---

# **1. Principes de dénombrement**

## Additif

Règle **générale** : à utiliser si on compte des événements **qui ne peuvent pas arriver **en même temps**, donc des cas **mutuellement exclusifs**.

>***disjoint*** : "A ne se produit pas en même temps que B, ne se chevauchent pas"


==**exemple** : On choisi 7 questions parmi 10, mais on doit au moins prendre 3 parmi les 5 premières**==

Nous ne pouvons pas choisir en même temps 3,4 et 5 questions parmi les 5 premières; on doit additionner les cas

- cas 1) prendre 3 questions parmi 5, 4 dans les 5 restantes
- cas 2) prendre 4 questions parmi 5, 3 dans les 5 restantes
- cas 3) prendre 5 questions parmi 5, 2 dans les 5 restantes

OU à l'inverse, **retirer** de l'univers de tout les choix les cas inadmissibles possibles (complémentarité)

- de **tout** les choix, retirer le choix de prendre 2 questions parmis 5, prendre les 5 restantes

## Multiplicatif

Règle **générale** : Si j'ai n façons de choisir un A, et qu'il y a **m** choix possibles pour chaque choix de A, alors j'ai n * m choix possibles

>**il s'agit d'un arbre donc le premier niveau est les options de A, et le deuxième les options en B** on a donc pour **chaque branche de A toutes les options de B**

==**question** : choisir quel train entre A, B ou C prendre, puis quel bus entre 1, 2, 3 ou 4==

###### Exemple 1 : 
*Combien de plaques d'immatriculation de 7 charactères on peut faire si les 3 premiers charactères sont des lettre et les 4 derniers des chiffres?*

> Je prend successivement 7 lettres et chiffres, donc 26 * 26 * 26 * 10 * 10 * 10

##### Exemple 2:

*Combien de plaques d'immatriculation de 7 charactères on peut faire si les 3 premiers charactères sont des lettres et les 4 derniers des chiffres? et en inversant lettres et chiffres?*

> $$ 26*25*24*10*9*8*7 = 78\ 624\ 000$$
>  $$ 10*9*8*26*25*24*23 = 258\ 336\ 000$$

## Résumé additif multiplicatif :

>Choix entre différentes options? -> **==additif==**
>Choix entre des options successives? -> **==multiplicatif==**

## **Permutations (tout, ordonné ou non)**

Règle générale : si on tente de former **tout les mots possibles** composés de 3 lettres, on a 3 choix pour la première, 2 pour la deuxième et 1 pour la dernière; 
$$n(n-1)(n-2)(n-...) \rightarrow n!$$

>[!NOTE] 
>Astuce on forme un arbre dont le **nombre de branches diminue à chaque niveau**


*Exemple:* **9 personnes** doivent êtres assises dans une **rangée de 9 places**. Le **premier** possède **9 choix**; assis il retire son siège des choix. **Le deuxième à 8 choix**, le troisième, 7 etc...
>On a donc ==9! façons==

*Exemple:* On reprend le même exemple des **9 personnes** devant êtres assises dans une **rangée de 9 places**, mais nous savons que ***5 personnes en particulier doivent occuper les 5 premières places***, et les 4 restant se partagerons les 4 restantes.
>On a donc 5! façons pour les 5 premières places ET 4! pour le reste, donc ==5!4! façons==

==Cas pour retirer répétitions== : on **divise** par le $n!$ de l'existence de chaque catégories

## **Tirs/piges avec répétitions**

Règle générale : si on tente de former **tout les vecteurs résultats d'une séquence de n tirs en ne modifiant pas le nombre de choix à chaque tour**, on a 3 choix pour la première, 3 pour la deuxième, 3 pour la nième; 

>[!NOTE] 
>Astuce on forme un arbre dont le **nombre de branches reste le même à chaque niveau


## **Arrangements (partiel, ordonné)**

Un arrangement, ***c'est une permutation partielle***

Règle générale : si on tente de choisir k objets parmi n objets, c'est comme si on construisait l'arbre initial complet des n! choix , mais qu'on ne considérait que les k première branches ; on ignore alors (n-k)! conditions

>==On forme un arbre dont on ne compte que les **k premières branches** et **ignore les n-k restantes**==
- **Formule :** $A(n, k) = \frac{n!}{(n-k)!}$ 
- **Formule avec répétition :** $A(n, k) = n^r$
## **Combinaison (partiel, non ordonné)**

Règle générale : on tente de relier des choix entre eux

>On forme un graphe non orienté, ou le vecteur AB = BA

- **Formule :** $C(n, k) = \frac{n!}{k!(n-k)!}$

> On sélectionne n boules parmi r au total, les boules étant indiscernables entre elles

==attention, ce cas ne traite pas les doublons, c'est sans remise==
## **Partitions combinaisons avec répétitions/remises** 

Nous avons **k** bacs (ou groupes) et **n** objets à répartir.
- Les **objets** sont représentés par des étoiles ( * ).
- Les **séparateurs** entre les bacs sont des bâtons (**|**).
- Puisque nous avons **k** bacs, nous avons **k-1 bâtons**.

Comme les objets entre eux sont indiscernables, l'idée fondamentale est que **changer la position d'un bâton revient à modifier la répartition des objets entre les groupes** et c'est plus simple.

exemple : Je dois remplir 5 bacs avec 14 étoiles, mais **aucun** bac ne dois avoir plus de 6 balles

On pourrais avoir des distributions comme cela : 

- `**** | *** | *** | ** | **`
- `** | ***** | *** | ** | **`
- `**** | ****** | * | ** | *`
- `**** | ****** | * | *** |`

Comme on **échange de place un bâton avec une étoile** donc on fait :
- ==les COMBINAISONS des **bâtons** (bacs - 1) parmi les **bâtons + étoiles**==
- **Formule** ${n-k+1 \choose k+1} \ \rightarrow \ \frac{n!}{k!(n-k)!}$ 

---
#### Bâtons étoiles, cas classique 
  
soit $x1 + x2 + x3$ = 8 avec $x1​≥−2$,  $x2​≥−1$,  $x3​≥0$

chaque bac commence avec un déficit; on doit garantir de remplir jusqu'à atteindre 0

- **(--OO) OO | (-O) O | OOOOO** est acceptable

*La partie entre parenthèse est annulée*, on fait un changement de variable pour simplicité

- y1 = (x1+2) 
- y2 = (x2+1)
- y3 = (x3)
- 8 -> 8+2+1 = 11 ==On ajoute à la somme totale les bornes négatives==

donc on fait les combinaisons de 2 bâtons parmi 11 éléments soit 13!/11!2!

---
#### Bâtons étoiles, cas borne minimale : au moins m par bac

soit $x1 + x2 + x3$ = 8 avec $\forall xi \rightarrow xi>= 0$

- **OOOO | OO | OO** est acceptable
- **OOOOOO | OO |** l'est aussi

On a 2 bâtons a déplacer parmi (8+2) éléments totaux donc 45

---

soit $x1 + x2 + x3$ = 8 avec $\forall xi \rightarrow xi>= 1$

On doit garantir au moins 1 étoile par bac,  on a:

- X | X | XOOOOO** est acceptable
- XO | XO | XOOO** est acceptable

on est limités; on a au moins 3 étoiles qui ne bougent pas, on peut seulement bouger 5 étoiles et les 2 bâtons

On a  2 bâtons a déplacer parmi (5+2) éléments,  $7 \choose 2$  donc 7!/5!2! = 21



---
#### Bâtons étoiles cas de borne maximale : pas plus que m par bac

**==ATTENTION; FAUT FAIRE LE INCLUSION EXCLUSION==**

soit $x1 + x2 + x3+ x4+x5$ = 14 avec $\forall xi \rightarrow xi <7$

- OOOO | O | OOOO | OOO | OO est acceptable
- OOOOOO | **O | OO | OOO | OO** est INACCEPTABLE
- OOOOOO | **OOOOOO | OO |  |**  est INACCEPTABLE

Alors, comme nous avons une borne supérieur, nous devons calculer toutes les possibilités pour ensuite ==retirer les cas inacceptables avec le PIE==

XXXXXXX | **O | OO | OO | OO** est INACCEPTABLE
**XXXXXXX | XXXXXXX |  |  |**    est INACCEPTABLE
Nous avons ${14+4 \choose 4}$ possibilités de partitions sans restrictions
donc $\frac {18!}{14!4!}$

1) on retire tout les cas ou on trouve que **1 bac a 7 balles au minimum**, on se retrouve alors avec 7 balles et 4 bâtons à permuter, ce qui reviens à 
	- Calculer les combinaisons de 1 bac parmi 5 (choisir quel bac aura 7 balles)
	- Multiplier par les combinaisons de 4 bâtons parmi 11 éléments

2) on retire tout les cas ou on trouve que **2 bacs ont 7 balles au minimum**, on se retrouve alors avec 0 balles et 4 bâtons à permuter, ce qui reviens à 

	- Calculer les combinaisons de 2 bacs parmi 5 (choisir quels bac auront 7 balles)
	- Multiplier par les combinaisons de 4 bâtons parmi 0+4 éléments ${4 \choose 4}$


---
# **2. Ensembles**
Un ensemble est une liste **non ordonnée** d'éléments. ==***Un ensemble fait nécessairement parti d'un univers S***==

#### **Opérations**

>- Union $\cup$ : L'**addition** de tout les termes des ensembles A et B
>- Intersection $\cap$ : **Seulement** les éléments **communs** à A et B 
>- Complément $A^c$ : **Tout** les éléments de **S** qui ne **sont pas** dans A
>- Xor $\Delta$ : **Tout** les éléments de l'union de A et B, mais **pas dans l'intersection**,  (A $\cup$ B) / (A $\cap$ B)

##### Exemple univers et ensembles

Soit S = {0,1,2,3,4,5,6,7,8,9} l'univers des chiffres, A = {1,3,4,8}, et B = {0,2,4,6,8} alors :

A $\cup$ B =  {0,1,2,3,4,6,8}
A $\cap$ B = {4,8} 
$A^c$ = {0,2,5,6,7,9} 
$\Delta$ :  (A $\cup$ B) / (A $\cap$ B) = {0,1,2,3,4,6,8} - {4,8}  = {0,1,2,3,6}

# **3. ==Probabilités==**

#### Axiomes des probabilités

**Pour tout évènement A, P(A) doit toujours**
	- être **compris** entre **0 et 1** $\rightarrow$  $0 \leq P(a) \leq 1$
- P({}) = 0
- P($S$) = 1
- P(A $\cup$ B $\cup$ C ...) = P(A) + P(B) + P(C) ***si A, B, C sont des ensembles/ trucs disjoints***

*==Ce que la # 4 veux dire:==*
- Si j'ai *1/3* de chance de voir **de la pluie**, **du soleil** et **de la neige** respectivement, alors j'ai **3/3** chances que l'**évènement** "**il pleut OU neige OU fait soleil**" se produise



---
# **4. Probabilité conditionnelles**

 La probabilité que E se produise sachant que B s'est produit implique qu'on 
 - **restreint notre analyse à l’univers où B s’est forcément produit** (dénominateur)
 - et qu'on on évalue la fréquence de E **dans cet univers réduit (l'intersection)**.

>$$P(E|B) = \frac {P(E \cap B)} {P(B)}$$

On peux aussi généraliser que $P(E \cap B) = P(E|B)P(B)$

## Formules de Bayes 

**Intuition**

 - $P(E|B)$ = $\frac {P(E \cap B)} {P(B)}$ , $P(B|E)$ = $\frac {P(B \cap E)}{P(E)}$
 - $E \cap B = B \cap E$

Comme l'intersection est ==commutative==, on aura le droit d'assumer

 - $P(E \cap B)= P(B \cap E) \rightarrow P(E|B) P(B) = P(B|E) P(E)$   
 >$$P(E|B) = \frac {P(B|E) P(E)} {P(B)}$$

**Démonstration complète:**

Soit B et E des évènements non disjoints, on a le droit de dire qu'un évènement B est la somme entre **l'intersection avec un autre évènement E** et **l'intersection avec tout ce qui n'est pas E**

$$P(B) = P(B \cap E) +P(B \cap E^C) = P(B | E)P(E)+P(B | E^C)P(E^C)$$
-  Remarque : $P(E^C) = P(1-P(E))$ 

on aura la probabilité totale de E en fonction des conditionnelles

$$P(E) = P(B | E)P(E)+P(B | E^C)P(1-P(E))$$

ALORS

>$$P(E|B) = \frac {P(B|E) P(E)} {P(B | E)P(E)+P(B | E^C)P(E^C)}$$

c'est donc une moyenne pondéré, c'est l'union de la probabilité que $E$ se produise dans l'univers de B ou E s'Est produit et dans l'univers $F^c$ ou E s'est produit

Ratio (cote de l'évènement) :$\frac {P(A)} {P(A^C)}$

---

Trucs cool

P(A $\cap$ B) = P(A)P(B) **si A et B sont indépendants (A est disjoint de B)**
- avoir PILE lors d'un lancer de pièce et 6 lors d'un lancer de dé

P(A $\cap$ B) = P(A|B)P(B) **si A et B sont dépendants (on peut retrouver A dans B et vice versa)**

---
# **5. Variables Aléatoires**

Il arrive qu'on s'intéresse plus au résultat qu'au parties ayant contribué à ce résultat de plus près. On voudrait savoir la chance d'avoir un total de 7, pas qu'on a eu 1 et 6, 2 et 5 etc.

**==La valeur d'une variable aléatoire correspond à des évènements dans E==, c'est une fonction qui associe un nombre réel à chaque résultat d’une expérience aléatoire. En d’autres termes, elle transforme un événement aléatoire en une valeur numérique.

$X:S→R$

*Ex.* 
>Soit s un vecteur 3x1 $\in$ S : S = {FFF,FFP,FPF,FPP,PFF,PFP,PPF,PPP} 
 
- X(s) = le nombre de F dans la séquence, donc
- X(2) = {**FF**P, **F**P**F**,P**FF**}
## Fonction de masse 

C'est une fonction qui montre la probabilité de réalisation de chaque évènement possibles de la variable aléatoire

ex. 

Comme X(s) est un ensemble qui **peut se réaliser**, on peut calculer la probabilité px(x) en dénombrant pour chaque px(x) la probabilité P(s) dans S de l'ensemble équivalent

on a :

- px(0) = $1/8$ = P({PPP}) 
- px(1) = $3/8$ = P({FPP,PFP,PPF})
- px(2) = $3/8$ = P({FFP,FPF,FFP})
- px(3) = $1/8$ = P({FFF})

et la fonction ressemble à ça:

|   **X**   |  0  | 1   | 2   | 3   |
| :-------: | :-: | --- | --- | --- |
| **px(x)** | 1/8 | 3/8 | 3/8 | 1/8 |

---
## Fonction de masse conditionnelle



## Fonction de répartition

C'est une fonction qui permet de voir **l’accumulation des probabilités** jusqu’à une certaine valeur

>On peut répondre aux question du genre *combien de chance d'obtenir **au plus** 2 faces?*

---
##### Exemple

**Soit l'expérience de tirer 3 boules dans une urne en ayant 20, chacune distincte et numérotée. On parie qu'au moins une des 3 boules dans le tirage va être supérieure ou égale à 17.**

Soit ==X== une variable aléatoire qui agit comme *==une fonction qui retourne toujours le max des 3 boules pigées==*. On s'intéresse pour ce pari à 

- $X=(20)$,  $X=(19)$,  $X=(18)$,  $X=(17)$

Comme on cherche un **max**, l'ordre ne compte pas. On sait que **l'univers** va être les **COMBINAISONS** des piges sans remises ==partielles et non ordonné== de 3 boules parmi 20
$$Univers = \ {20 \choose 3} = $$
$X = (20)$ signifie que "*la boule 20 a été pigée*", et on doit alors faire les **COMBINAISONS** de **==2 boules non ordonnées parmi les 19 restantes==**
$$X(20) = \ \frac {\ {19 \choose 2}}{{20 \choose 3}} = 3/20$$
$X = (19)$ signifie que la boule 19 a été pigée, et on doit alors faire les **COMBINAISONS** de 2 boules non ordonnées parmi les 18 restantes **==car on ne peut pas choisir 20, ce serait l'évènement X(20)==** 
$$X(19) = \frac {\ {18 \choose 2}}{{20 \choose 3}} = 51/280$$
$$X(18) = \ 34/285$$
$$X(17) = 2/19$$

**La fonction de masse montre qu'on a plus de chances de voir que le max qu'on a pigé est 20 puisque l'univers**

|   **X**   |  17   | 18     | 19     | 20   |
| :-------: | :---: | ------ | ------ | ---- |
| **px(x)** | 2/19  | 34/285 | 51/280 | 3/20 |
|    dec    | 10.5% | 11.9%  | 13.4%  | 15%  |
On voit que observer 20 comme étant le max des 3 boules est plus probable d'arriver (simplement parce qu'il y a plus de combinaisons)

La fonction de répartition montre


|   **X**   | =< 17 | =< 18  | =<19   | =<20  |
| :-------: | :---: | ------ | ------ | ----- |
| **px(x)** | 2/19  | 34/285 | 51/280 | 3/20  |
|    dec    | 10.5% | 11.9%  | 13.4%  | 15%   |
|  $\sum$   | 10.5% | 22.4%  | 35.8%  | 50.8% |
donc, on gagne notre pari si on obtient la somme $P(X=17)+P(X=18)+P(X=19)+P(X=20)$ qui donne 50.8%

---
# **6. Variables aléatoires conjointes**

Soit l'expérience de tirer une pièce de monnaie 3 fois de suite

- S = {FFF,FFP,FPF,FPP,PFF,PFP,PPF,PPP} 
On pose 
- X(s) = nombre de F sans le vecteur s
- Y(s) = position du premier F dans s

On sait que X(s) a comme nombre de F possibles {0,1,2,3} et Y(s) a comme position du premier F possibles {0,1,2,3}

- px(0) = $1/8$ = P({PPP}) 
- px(1) = $3/8$ = P({FPP,PFP,PPF})
- px(2) = $3/8$ = P({FFP,FPF,FFP})
- px(3) = $1/8$ = P({FFF})

- py(0) = $1/8$ = P({PPP}) 
- py(1) = $4/8$ =P({FPP,FFP,FPF,FFF})
- py(2) = $2/8$ = P({PFF,PFP})
- py(3) = $1/8$ = P({PPF})

On doit comparer les ensembles de probabilités de chacun, et en retirer la probabilité commune (l'intersection) pour chaque Y et X

|           | y = 0 | y = 1 | y = 2 | y = 3 | px(x) |
| :-------: | :---: | ----- | ----- | ----- | ----- |
| **x = 0** |  1/8  | 0     | 0     | 0     | 1/8   |
| **x = 1** |   0   | 1/8   | 1/8   | 1/8   | 3/8   |
| **x = 2** |   0   | 2/8   | 1/8   | 0     | 3/8   |
| **x = 3** |   0   | 1/8   | 0     | 0     | 1/8   |
| **py(y)** |  1/8  | 4/8   | 2/8   | 1/8   | ==1== |

## vérifier l'indépendance

Tactique 1 : 
$P(X=x,Y=y) = P(X=x) * P(Y=y)$

Tactique 2 :
$Fxy(x,y) = Fx(x) * Fy(y)$

---

---
### **Loi binomiale**

Origine de Bernoulli : La loi binomiale va **décrire le nombre total de succès obtenus dans n expériences indépendantes** , où chaque essai avait **deux issues possibles** :

- **Succès** avec probabilité $p$
- **Échec** avec probabilité $1−p$

Soir X *la variable aléatoire* qui représente **le nombre total de succès** dans $n$ essais $\rightarrow$ On cherche donc à déterminer $P(X = k)$ c'est-à-dire **la probabilité d'obtenir exactement $k$ succès parmi $n$ essais**

Disons qu'on a une expérience répétée $n=100$ fois.  
Si la probabilité de succès est $p=0.70$ et la probabilité d’échec est $1−p=0.30$, on s'attend **en moyenne** à voir **70 réussites et 30 échecs**.

On cherche une probabilité $P(X=k)$, ==l'inconnue ici est le nombre de succès==, c’est simplement une façon de dire :

> **"Combien de succès vais-je obtenir en n<n essais ?"**

On aura des vecteurs du style : $P(X=2) = (R,P,P,R,R,R...)$

La probabilité **d'une séquence spécifique** où l’on obtient $k$ succès et $n−k$ échecs est :

$$p^k(1−p)^{n−k}$$
Comme l'ordre des succès **ne compte pas** (on va juste calculer les facons de disposer ces succès parmi les essais), on aurait donc une combinaisons de k succès parmi n essais, d'où la loi binomiale totale:
$${n \choose k}p^k(1−p)^{n−k}$$
### **Loi multinomiale**

C'est la même chose que la loi binomiale, mais au lieu d'avoir des vecteurs de 2 éléments (réussite ou échec) on se retrouve avec $k$ éléments

nous avons un vecteur $(k1,k1,k2,..,k …)$ avec

C’est comme dire :

> **Quelle est la probabilité que chaque catégorie i apparaisse exactement k fois après n essais ?**

La loi multinomiale suppose que **chaque tirage est indépendant**, donc on ne cherche pas **l’identité spécifique** des occurrences, juste **combien il y en a** dans chaque catégorie.

### **Loi géométrique**

C'est une binomiale réduite dans le sens que le succès est unique et apparait après un nombre d'échecs dans le vecteur, avec ==les échecs **indiscernables** entre eux==

C'est comme dire :

> **Combiens de ratés ont exactement précédé le premier succès d'une série indépendante de jets ?** 

Donc on a $$(1−p)^{n−1} p$$
Car on a $(1 - p)^{n-1}$ échecs précédent $p$, le succès. **On peux se poser 2 questions :**

> Proba d'avoir besoin d'**EXACTEMENT** n tirages 
	$\rightarrow$  $p^1(1−p)^{n−1}$
> Proba d'avoir besoin d'**AU MOINS** n tirages
	$\rightarrow$ $(1−p)^{n−1}$ (ou juste la proba d'avoir uniquement des échecs)

### **Loi binomiale négative**

>[!Quand l'utiliser]
>Lorsqu'on répète une expérience **jusqu’à obtenir un certain nombre de succès**. Le **nombre d’essais est inconnu**, et c'est **ce qu'on cherche**.
>ex. On tire des boules jusqu’à obtenir **3 boules rouges**. 
**Quelle est la probabilité que cela prenne exactement 7 tirages?**

Par *rapport à la binomiale*, ==l'inconnu qu'on cherche est le nombre d'essais totaux pour arriver à un nombre de réussites==

C'est comme dire:

> **Combien d’essais faut-il pour atteindre le dernier des succès voulus ?**

- Le fait qu'on s'**arrête** dès qu'on arrive au dernier succès implique que **le dernier tir est un succès**
- On doit donc faire des combinaisons des **r-1 succès précédents** (le dernier est confirmé) parmi les **k-1 essais précédent** (le dernier est aussi confirmé)
### **Loi hypergéométrique**

>[!Quand l'utiliser]
>Lorsqu'on effectue un **tirage sans remise**, Le **nombre d’essais est fixé**, mais les probabilités **changent après chaque tirage**
>ex. Quelle est la probabilité d’obtenir exactement **2 rouges** si on tire **4 cartes au hasard**, **sans remise**?

Dans ce cas, on parle d'une expérience dont l'**essai précédent a eu une influence sur l'essai présent**, qui aura lui aussi un impact sur le suivant

---
# ==**Fonction de masse/probabilité**== 

On s'intéresse à voir les probabilité de chacun des éléments de l'univers de la variable aléatoire X. C'est un plan dont les abscisses sont les différents évènements et en ordonnées les probabilités de 0 à 1

>On pourrait l'utiliser pour savoir quel évènement **à le plus de chances de se produire** par rapports aux autres évènements (diagramme à bandes)

### Distribution conjointe


# **Fonction de répartition**

On s'intéresse sur l'état de la probabilité cumulée en progressant dans les différentes valeurs d'une variable aléatoire 

>On regarde la **probabilité que la variable aléatoire X prenne une valeur inférieur ou = à un b** tel que $P(X<3) = \ ?$

- Elle est toujours croissante (bornée supérieurement par 1, inférieurement par 0)
- Elle est en escaliers de forme (point plein $\rightarrow$ point vide)
- $Fr(x)= \sum p(X=k)$



# **Espérance discrète:**

$$E(aX+bY) = aE(X) + bE(Y)$$

Si X et Y sont **indépendantes** :
$$E(XY)=E(X)E(Y)$$

| **Loi** | **Espérance \( E[X] \)** | **Interprétation** |
|---------|-------------------|--------------------|
| **Bernoulli** \( X \sim Bernoulli(p) \) | $$E(X) = p$$ | Probabilité de succès sur un essai |
| **Uniforme** \( X \sim U(a,b) \) | $$E[X] = \frac{a + b}{2}$$ | Milieu de l’intervalle |
| **Poisson** \( X \sim Poisson(\lambda) \) | $$E[X] = \lambda$$ | Nombre moyen d’événements sur une période donnée |
| **Binomiale** \( X \sim B(n, p) \) | $$E[X] = np$$ | Nombre moyen de succès attendus sur \( n \) essais |
| **Hypergéométrique** \( X \sim H(N, K, n) \) | $$E(X) = n \frac{K}{N}$$ | \( K/N \) est la proportion d'éléments "succès" dans la population totale |

---
# **Variance discrète :**
$$Var(X) = E(X^2) - (E(X))^2$$

Si X et Y sont **indépendantes** :        $Var(X+Y)=Var(X)+Var(Y)$

| **Loi**              | **Variance \( Var(X) \)** | **Interprétation**                                            |
| -------------------- | ------------------------- | ------------------------------------------------------------- |
| **Bernoulli**        | $$Var(X) = p(1 - p)$$     | Résultats très prévisibles si \( p \) proche de 0 ou 1        |
| **Uniforme**         | $$flemme$$                | Plus \( b - a \) est grand, plus la variance est élevée       |
| **Poisson**          | $$Var(X) = \lambda$$      | La variance est égale à l’espérance                           |
| **Binomiale**        | $$Var(X) = np(1 - p)$$    | C'est la somme de \( n \) Bernoulli                           |
| **Hypergéométrique** | $$flemme$$                | Similaire à la binomiale mais ajustée pour tirage sans remise |

# **Covariance discrète**

La **covariance** mesure **le lien linéaire** entre deux variables aléatoires \( X \) et \( Y \).  
Elle est définie par :

$$Cov(X, Y) = E[(X - E[X])(Y - E[Y])]$$

ou de manière équivalente :

$$Cov(X, Y) = E[XY] - E[X]E[Y]$$

**Interprétation** :
- $Cov(X, Y) > 0$ → **Relation positive** : Quand \( X \) augmente, \( Y \) a tendance à augmenter
- $Cov(X, Y) < 0$ → **Relation négative** : Quand \( X \) augmente, \( Y \) a tendance à diminuer
- $Cov(X, Y) = 0$ → **Aucune relation linéaire** (mais attention, cela ne signifie pas forcément indépendance)

---
## **Propriétés Importantes**
| **Propriété**                                | **Formule**                             | **Interprétation**                                                      |
| -------------------------------------------- | --------------------------------------- | ----------------------------------------------------------------------- |
| **Formule de base**                          | $$Cov(X, Y) = E[XY] - E[X]E[Y]$$        | Utilisée pour le calcul direct                                          |
| **Lien avec la variance**                    | $$Cov(X, X) = Var(X)$$                  | La covariance d'une variable avec elle-même est sa variance             |
| **Linéarité**                                | $$Cov(aX + b, Y) = a Cov(X, Y)$$        | Permet de sortir les constantes                                         |
| **Symétrie**                                 | $$Cov(X, Y) = Cov(Y, X)$$               | La covariance est **commutative**                                       |
| **Somme de covariances**                     | $$Cov(X+Z, Y) = Cov(X, Y) + Cov(Z, Y)$$ | La covariance est **additive**                                          |
| **Si \( X \) et \( Y \) sont indépendantes** | $$Cov(X, Y) = 0$$                       | L’indépendance implique une **covariance nulle** (mais pas l’inverse !) |

---
## **Covariance pour des Lois de Probabilité**
| **Loi**       | **Formule de la Covariance**                               | **Remarque**                                                    |
| ------------- | ---------------------------------------------------------- | --------------------------------------------------------------- |
| **Binomiale** | $$Cov(X, Y) = 0$$ si \( X \) et \( Y \) sont indépendantes | Les variables binomiales indépendantes ont une covariance nulle |
| **Poisson**   | $$Cov(X, Y) = 0$$ si indépendantes                         |                                                                 |
