---

---

---
# 1.1 intro
Un système de communication est composée de **n** antennes alignées donnant un signal de 1 ou 0. Il existe **m** antennes possiblement défectueuses. Le système marchera seulement sil **n'y a pas 2 antennes défectueuses consécutives**. ==Soit n = 4  (antennes total) et m = 2 (antennes défectueuses avec **signal de 0**)<==

| n=1   | n=2   | n=3   | n=4   |
| ----- | ----- | ----- | ----- |
| 0     | 1     | 1     | 0     |
| 0     | 1     | 0     | 1     |
| 1     | 0     | 1     | 0     |
| ==0== | ==0== | ==1== | ==1== |
| ==1== | ==0== | ==0== | ==1== |
| ==1== | ==1== | ==0== | ==0== |

Dans les **3 derniers cas, le système ne marchera pas** et dans les 3 premiers il marchera. La **probabilité** que le système ne fonctionne pas est $\frac 3 6$ 

# 1.2 Dénombrement

#### Dénombrement : Soit une expérience faite en 2 étapes. Si l'étape 1 peut produire une issue parmi **m** issues possibles, et que pour chaque issue m nous avons **n** autres issues possibles possibles pour l'étape 2, alors il existe **n * m** résultats à considérer pour l'expérience complète

En version longue explicite on a la **matrice**: 

(1,1) (1,2) ... (1,n)
(2,1) (2,2) ... (2,n)
...
(m,1)(m,2)... (m,n)

##### Exemple paires homme-fils

*Soit 10 hommes, chacun ayant 3 fils. Si on doit choisir un homme et un fils comme "famille exemplaire", on pourrait choisir parmi combien de paires?*

>$$n = 10, m = 3 \rightarrow \\ n*m =30 \ choix$$

##### Exemple lettres plaques

*Combien de plaques d'immatriculation de 7 charactères on peut faire si les 3 premiers charactères sont des lettre et les 4 derniers des chiffres?*

>$$ 26*26*26*10*10*10*10 = 175\ 760\ 000$$

##### Exemple lettres plaques sans répétitions

*Combien de plaques d'immatriculation de 7 charactères on peut faire si les 3 premiers charactères sont des lettres et les 4 derniers des chiffres? et en inversant lettres et chiffres?*

> $$ 26*25*24*10*9*8*7 = 78\ 624\ 000$$
>  $$ 10*9*8*26*25*24*23 = 258\ 336\ 000$$

# 1.3 Permutations

##### 1.3.1 Permutation d'objets discernables

Les objets discernables sont des objets distinct ; on ne pourrait pas les confondre avec un autre objet. C'est comme avoir un verre et un plante, on ne pourrait pas se tromper si on les identifiait chacun avec une photo

#### **Permutations discernables** : Si on arrange les lettres **a, b et c** pour former un **mot de toutes les lettres**, on aurait 3 choix pour la première lettre, 2 pour la suivante et la dernière évidente. Pour ce cas d'objets **discernables**, on a **3!** permutations possibles

##### Exemple classement homme femme:
*Soit 6 hommes et 4 femmes classés par performance. C'est quoi les permutations possibles de ce classement si les hommes et les femmes sont confondus? Si **non confondus**?*

>$$Confondus \ :6+4 =10\ personnes \rightarrow 10! = 3\ 628\ 800 $$
>$$Non-confondus \ :6\ personnes,\ puis\ 4 \ personnes \rightarrow 6! +4! = 17\ 280 $$

##### 1.3.1 Permutation d'objets indiscernables

Les objets indiscernables sont des objets qu'on pourrait confondre avec un autre objet. C'est comme savoir qu'on a deux plantes, mais les détails concernant leurs espèces qui nous permettraient de les différencier nous sont **inconnues**

#### **Permutations indiscernables** Si on arrange les lettres {P,E,P,P,E,R} pour former un **mot de toutes les lettres**, on aurait des doublons si on considère les P et les E entre eux **indiscernables**

$P^1E^1P^2P^3E^2R = P^2E^1P^1P^3E^2R = P^3E^1P^2P^1E^2R...$ **là j'ai permuté les P entre eux et ça n'a rien changé**, on doit enlever toutes les permutations de **P entre eux** et **E entre eux**

on a 3! permutation de P, et 2! permutations de E

Le nombre correct de permutations est $\frac {n!} {n1!n2!...}$ = $\frac {6!} {3!2!}$

# 1.4 Combinaisons

Un combinaison est une sorte de permutation sans répétition (car ensemble) sur un groupe limité et inférieur à S

Soit un ensemble de 5 lettres : S = {A,B,C,D,E} et nous pourrions faires des combinaisons de 3 lettres parmi 5 (donc des ensembles de lettres). Initialement, et bêtement on se dit quil y a 5 * 4 * 3 façon d'arranger les 3 lettres si on considère l'ordre mais comme on s'en fout, on doit retirer les doublons de ces ensembles. 
{A,B,C} = {B,A,C} ={ACB}... jai échangé 3 lettres et **ça change rien à l'ensemble**

On aura alors  $\frac {n!} {(n-r)!r!}$

##### Exo : j'ai 5 femmes et 7 hommes, combien de comités de 2 femmes et 3 hommes je peux faire?

donc j'ai à faire des combinaisons de **2 femmes parmi 5**, 
- j'ai $\frac {5!} {(3)!2!} = \frac {5*4} {2}$ 
et des combinaisons de **
**, 
- j'ai $\frac {7!} {(4)!3!} = \frac {7*6*5} {6}$

Ensemble j'ai $10*35$ donc 350 combinaisons

##### Et si dans ces comités on on sait que 2 hommes sont ennemis, on fait combien de comités?

On calcule en soustrayant des comités **possibles** le nombre de comités ou ils sont **ensembles**

S'ils sont ensembles, ça veux dire quil reste 1 homme à choisir parmi 5 restants donc on calcule 1 homme parmi 5 = 5!/1!* 4! = 5. À ça on ajoute le choix des femmes, toujours 10 donc 50 comités interdits. On aura 300 comités valides sans eux 

#### Théorème du binôme 

#### 
Partitions

# 1.4 Partitions

---
# 2.1 Probabilités

On va considérer un expérience dont l'issue est imprévisible, une naissance par exemple. Toutefois, on sais a quelles issues s'attendre ; un gars ou une fille. 
#### **Univers S** : Si l'expérience est le genre à la naissance d'un bébé, alors l'univers S est l'ensemble {g, f}, soit les issues possibles et **attendues**

##### 2.1.1 Vecteurs
On a un Dénombrement  de  (n * m) **vecteurs** de forme (D1, D2, DX...) qui expriment en ordre les issues obtenues. Pour un tirage 2 fois de suite entre 1 et 3 avec répétition nous avons explicitement ~

(1,1) (1,2) (1,3)
(2,1) (2,2) (2,3)
(3,1) (3,2) (3,3)
vecteurs possibles

##### 2.1.2 Vecteurs non ordonnés
On a un **dénombrement partiel**  de  (n * m) **vecteurs** de forme (D1, D2) avec l'ajout de l'**équivalence**  (D1, D2) $\equiv$   (D2, D2), on retirera alors un des membres de l'équivalence
Pour un même tirage 2 fois de suite entre 1 et 3 sans répétition nous avons explicitement ~

(1,1) (1,2) (1,3)
~~(2,1)~~ (2,2) (2,3)
~~(3,1) (3,2)~~ (3,3)
Soit la **matrice triangulaire supérieure** du dénombrement initial et donc ==**n!** cas==

#### **Évènement E**: un ensemble de **divers résultats**  possibles et dont la réalisation est atteinte si **un ou plusieurs des résultats** de l'ensemble est **vérifié**. Si E = {(P,F)(F,P) (P,P)} alors on comprend que cet évènement est vérifié lorsqu'on "tire au moins une fois Pile"

Exemple 

# 2.2 Ensembles

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

# 2.1 Axiomes des proba

On parle de *mesure* de probabilité P(A) pour un évènement A. Pour tout évènement A, P(A) doit toujours

>- être **compris** entre **0 et 1** $\rightarrow$  0 >= P(a) >=1
>- P({}) = 0
>- P($S$) = 1
>- P(A $\cup$ B $\cup$ C ...) = P(A) + P(B) + P(C) ***si A, B, C sont des ensembles/ trucs disjoints***

*==Ce que la # 4 veux dire:==*
- Si j'ai *1/3* de chance de voir **de la pluie**, **du soleil** et **de la neige** respectivement, alors j'ai **3/3** de voir l'**évènement** "**il pleut OU neige OU fait soleil**" se produire

##### 3.2 Dérivées des axiomes :

##### exo 1 :
Soit $E$ et $E^c$ :
$$P(E \cup E^c) = P(S) = 1$$
Comme l'union des proba équivaut la proba des unions :
$$P(E \cup E^c) = P(E) \cup P(E^c)$$

$$1 = P(E) \cup P(E^c) \rightarrow 1- P(E) = P(E^c)$$


##### exo 2 :
**==La somme des unions = la somme des proba individuelles moins la somme des probas prises 2 à 2 plus la somme des probas prises 3 à 3  et ainsi de suite (on parle d'intersections)==**

ex. P(E $\cup$ F $\cup$ G) = P(E) + P(F) + P(G) - (P(E$\cap$F)+ P(F$\cap$G) + P(G$\cap$E))+ P(E$\cap$ F $\cap$ G)

---

# 3.1 Probabilité conditionnelles

On s'intéresse aux probabilité conditionnelles parce qu'il s'agit de comprendre une expérience avec une partie de l'information (donc conditionnelle en fonction de ce qu'on a).

1) Supposons l'univers S : S= {1,2,3,4,5,6}, avec deux ensembles, A et B où :
-  A = {2,4,6},  P(A) = $3/6$,
-  B = {2,3,4},  P(B) = $3/6$
-  P(A$\cap$B) = $2/6$.

Vu qu'on se concentre sur les  probabilité qui ont **déjà vérifié que B s'est produit** avant de regarder A, c'est comme si on **réduit l'univers à B**; on a maintenant |B| éléments, et on cherche combien de A est dans ce nouvel univers

- P($A∣B$) dit : **Parmi les cas où B s’est produit (B={2,3,4}), quelle est la proportion où A (A={2,4,6}) est aussi arrivé ?**
- On réduis S à B, puis on regardes la part de B qui appartient à A.

#### Généralisation

On a P($A∣B$) = $\frac {A\ est\ aussi\ arrivé} {parmis\ B\ cas\ vérifiés} = \frac {P(A \cap B)} {P(B)} = \frac {2/6} {3/6}$


---
Paradoxe monty hall