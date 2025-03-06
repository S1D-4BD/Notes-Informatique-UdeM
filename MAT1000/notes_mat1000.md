
# 1.1 Écriture décimale

>**Définition**
>Un nombre est rationnel si et seulement s’il admet une écriture décimale **périodique ou finie**

Par définition les nombres rationnels font parti de l'ensemble Q tel que
$$Q= \{ \frac{p}{q} |\ p\in Z, q \in N^* \}$$
Montrons que $x = 12, 34 2021 2021$... est un rationnel

1)                                       $100x = 1234 , 20212021...$
2)                          $10000 * 100x = 12342021 , 2021...$
3)              $10000 * 100x - 100x = 12340787$
4)                                            $x = \frac{12340787}{999900} \in Q$

a faire : 
Montrer que la somme de deux rationnels est un rationnel. 
Montrer que le produit de deux rationnels est un rationnel. 
Montrer que l’inverse d’un rationnel non nul est un rationnel. ? 2. Écrire les nombres suivants sous forme d’une fraction :
- 0, 1212 ; 
- 0, 121212 ... ;
- 78, 33 456 456
Sachant p 2 ∈/ Q, montrer 2 − 3 sqrt(2) pas ∈ Q

---
# 1.2 Propriété des Réels

Malgré leur nature non dénombrable, les réels sont **ordonnés**

>Soit E un ensemble
>Une relation R sur E est un ==**sous-ensemble** du produit cartésien== $E \times E$. Pour un couple $(x,y) \in E \times E$, on dit que x est en relation avec y

Une relation R est une relation d’ordre si 
• R est réflexive : $\forall x ∈ E,\ \exists \ (x,x)$
• R est antisymétrique : si $\exists \ (x,y) \wedge \exists (y,x) \rightarrow x=y$ 
• R est transitive : $\forall x, y,z ∈ E, si \ \exists (x,y) \wedge (y,z) \rightarrow \exists (x,z)$.

**==On a en résumé l'ordre réel constitué ainsi==**

>$\forall x ∈ R, x ⩽ x$ 
>$\forall x, y ∈ R, \ \ si \ \ x ⩽ y \wedge y ⩽ x \rightarrow  \ x = y$
>$\forall x, y, z ∈ R \ \ si \ x ⩽ y \wedge \  y ⩽ z  \rightarrow \ x ⩽ z$

#### Partie entière 

Pour $(x,y) \in R^2$ on a que 
>$x ⩽ y ⇐⇒ y-x \in R^+$

Qui nous permet de définir intuitivement la **==partie entière d'un réel x==**, noté  $E(x)$ puisqu'il existe un entier naturel plus grand

$\forall x \in R,\ \exists ! \ E(x) \in N \ : \ E(x) \leq x \lt E(x)+1$

#### Valeur absolue

Pour $x \in R$ on a que 
> $-|x| \leq x \leq |x|$

Qui nous permet de définir **==la valeur absolue==** et montrer intuitivement les **inégalités triangulaires** de celles-ci

1)                                            $-|x| ⩽ x ⩽ |x|$
2)                                            $-|y| ⩽ y ⩽ |y|$
3)                                 $-|x| - |y| ⩽ x - y ⩽ |x|-|y|$
4)                                      $x-y = z \rightarrow z ⩽ |z|$
5)                                         $|x|-|y| = |z|$
6)                                           $|x - y| ⩽ |x|-|y|$
ADD #2
---
# 3. Densité de Q dans R

>**Définition**
>Un intervalle de $R$ est un sous-ensemble vérifiant la propriété: 
>	$\forall a,b \in I \ \forall x \in R \ (a⩽x ⩽b \rightarrow x \in I)$

- Par définition I = ∅ est un intervalle
- I = R est aussi un intervalle
### Tout intervalle **==contient un rationnel==** 

>Revient à prouver $r = \frac{p}{q} \in Q \rightarrow \exists r \ \forall a,b \in R : a⩽ r ⩽b$


 Soit la droite des réels, nous cherchons une grandeur de "saut" $\frac{1}{q}$ tel qu'un nombre $p$ de fois qu'on fait ce saut nous permettrai d'arriver dans l'intervalle $a,b$ (proche de $a$)

Si $\frac{1}{q}$ est supérieur à $b-a$, en partant de 0 c'est garanti de *rater*: 
- on choisi $\frac{1}{q} < b-a$ et donc $q < \frac{1}{b-a}$

On choisi alors un $p$ qui, un saut précédent, était inférieur à a et immédiatement après est plus grand
- on sait que $\frac{p-1}{q} < a < \frac{p}{q}$
- $p-1 < qa < p$
- On se rappelle que $p$ est un entier, si $x$ est compris entre cet entier et son suivant, alors la borne gauche de $x$ est **sa partie entière**, donc $E(qa)$

On fait la **synthèse**; soit $a < b, \ \in N$
- $\frac{1}{q} < b-a$ , $q < \frac{1}{b-a}$
 - $p-1 < qa < p$
 - En divisant par $q$ on en déduit que $\frac{p}{q} - \frac{1}{q} < a < \frac{p}{q}$  et est la même chose que  $\frac{p}{q} < a < \frac{p}{q} + \frac{1}{q}$
 - On sait déjà que $\frac{1}{q} < b-a$
 - On a $\frac{p}{q}⩽ a + (b-a)$
 -  $a⩽\frac{p}{q}⩽ b$

