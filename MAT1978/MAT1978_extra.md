# 1 Principes de dénombrement


## 1.1 Additif

Règle **générale** : Si j'ai ***n*** façons de choisir un A, ***m*** façons de choisir une tache B et que je ne peux pas choisir les 2 en même temps, alors j'ai n + m choix

>***disjoint*** implique "A ne se produit pas en même temps que B, ne se chevauchent pas"

>**Il s'agit de 2 arbres cotes à cote**s, et on additionne le nombre de branches

==**exemple** : choisir entre prendre le **train A, B ou C** ou prendre le **bus 1, 2, 3 ou 4**==

Je ne peux pas être dans le train et le bus en même temps, mon choix est dans l'ensemble de choix $C = \{ A,B,C,1,2,3,4 \}$

## 1.2 Multiplicatif

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

## résumé additif multiplicatif :

>[!note]
>choix entre différentes options? -> **==additif==**
>choix entre des options successives? -> **==multiplicatif==**

---

## 1.3 Permutations (tout, ordonné)

Règle générale : si on tente de former **tout les mots possibles** composés de 3 lettres, on a 3 choix pour la première, 2 pour la deuxième et 1 pour la dernière; ==n(n-1)(n-2) on a donc n! choix==

>on forme un arbre dont le **nombre de branches diminue à chaque niveau**

## 1.4 Arrangements (partiel, ordonné)

Règle générale : si on tente de choisir k objets parmi n objets, c'est comme si on construisait l'arbre initial complet de n! choix , mais qu'on ne considérait que les k première branches ; on ignore alors (n-k)! conditions

>on forme un arbre dont on ne compte que les **k premières branches** et **ignore les n-k restantes**

- **Formule :** $A(n, k) = \frac{n!}{(n-k)!}$ 
 
## 1.5 Combinaison (partiel, non ordonné)

Règle générale : on tente de relier des choix entre eux

>c'est comme un graphe non orienté, ou le vecteur AB= BA

- **Formule :** $C(n, k) = \frac{n!}{k!(n-k)!}$

## 1.6 Partitions

**Méthode des bâtons et étoiles** : le point important est de retenir que nous avons k bacs avec k-1 **bâtons**. L’ordre des étoiles dans les bacs **ne compte pas, c'est une combinaison particulière** .

exemple : Je dois remplir 5 bacs avec 14 étoiles, mais aucun bac ne dois avoir plus de 6 balles

On pourrais avoir des distributions comme cela : 
- OOOO | OOO | OOO | OO | OO
- OO | OOOOO | OOO | OO | OO
- OOOO | OOOOOO | O | OO | O
- OOOO | OOOOOO | O | OOO | 

au fond, on **échange de place un bâton avec une étoile** donc on fait :
- ==les COMBINAISONS des **bâtons** parmi les **bâtons + étoiles**== soit 
- formule $C(n-k+1, k+1) = \ ajusté \ \frac{n!}{k!(n-k)!}$
#### cas 1 borne minimale : au moins m par bac

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
#### Cas classique 
  
soit $x1 + x2 + x3$ = 8 avec $x1​≥−2, x2​≥−1, x3​≥0$

chaque bac commence avec un déficit; on doit garantir de remplir jusqu'à atteindre 0

- (--OO) OO | (-O) O | OOOOO** est acceptable

La partie entre parenthèse est annulée, on fait un changement de variable pour simplicité

- y1 = (x1+2) 
- y2 = (x2+1)
- y3 = (x3)
- 8 -> 8+2+1 = 11 ==On ajoute à la somme totale avec des bornes négatives==

donc on fait les combinaisons de 2 bâtons parmi 11 éléments soit 13!/11!2!

---
#### cas 2 borne maximale : pas plus que m par bac

==ATTENTION; FAUT FAIRE LE INCLUSION EXCLUSION==

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
### ensembles
Un ensemble est une liste **non ordonnée** d'éléments. ==***Un ensemble fait nécessairement parti d'un univers S***==

**Opérations**

>- Union $\cup$ : L'**addition** de tout les termes des ensembles A et B
>- Intersection $\cap$ : **Seulement** les éléments **communs** à A et B 
>- Complément $A^c$ : **Tout** les éléments de **S** qui ne **sont pas** dans A
>- Xor $\Delta$ : **Tout** les éléments de l'union de A et B, mais **pas dans l'intersection**,  (A $\cup$ B) / (A $\cap$ B)

Exemple univers et ensembles

Soit S = {0,1,2,3,4,5,6,7,8,9} l'univers des chiffres

A = {1,3,4,8}, et B = {0,2,4,6,8} alors

A $\cup$ B =  {0,1,2,3,4,6,8}
A $\cap$ B = {4,8} 
$A^c$ = {0,2,5,6,7,9} 
$\Delta$ :  (A $\cup$ B) / (A $\cap$ B) = {0,1,2,3,4,6,8} - {4,8}  = {0,1,2,3,6}

## 2.1 Probabilités

#### Axiomes des probabilités

**Pour tout évènement A, P(A) doit toujours**
	- être **compris** entre **0 et 1** $\rightarrow$  $0 \leq P(a) \leq 1$
- P({}) = 0
- P($S$) = 1
- P(A $\cup$ B $\cup$ C ...) = P(A) + P(B) + P(C) ***si A, B, C sont des ensembles/ trucs disjoints***

*==Ce que la # 4 veux dire:==*
- Si j'ai *1/3* de chance de voir **de la pluie**, **du soleil** et **de la neige** respectivement, alors j'ai **3/3** chances que l'**évènement** "**il pleut OU neige OU fait soleil**" se produise

---


3.1 Probabilité conditionnelles







---

Trucs cool

P(A $\cap$ B) = P(A)P(B) **si A et B sont indépendants (A est disjoint de B)**
- avoir PILE lors d'un lancer de pièce et 6 lors d'un lancer de dé

P(A $\cap$ B) = P(A|B)P(B) **si A et B sont dépendants (on peut retrouver A dans B et vice versa)**
- <
- 