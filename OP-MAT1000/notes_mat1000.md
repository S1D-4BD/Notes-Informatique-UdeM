
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

---
### Intégrales

- $dx$ : un tout petit morceau de $x$
- $\int dx$ : la somme de tout les petits morceaux de $x$
- $Intégrale$ : reconstitution de $x$ par somme de ses morceaux

---
#### Variation
Intuition: Pensons à une quantité $x$ sur lequel on peux rajouter une petite quantité pour devenir $x+dx$. Le carré de ça est donc $x^2+2xdx+(dx)^2$. 

![[x_2xdx_x2.jpg|367x165]]

Si $dx$ est incroyablement petit, alors l'ajout de $(dx)^2$ est négligeable. Son taux de variation étant le carré agrandi moins l'initial, on trouve que la variation pertinente est $2x$ d'où la dérivée de $x^2 = 2x$  

#### Taux liés
1.1
Prenons un triangle de base $x$ et de hauteur $y$. Si l'angle de 30 est fixé et qu'on augmente la largeur de la base, la base devient $x + dx$ alors la hauteur va elle aussi changer pour devenir $y+dy$. Le ratio est le même puisque le petit triangle formé est proportionnel. Donc $dy/dx = y/x$

On comprend que y est en relation avec x de telle sorte quelle définie une fonction:
$$y=xtan(30)$$
1.2

Soit une échelle de 181 pouces dont la base est à x unités d'un mur, et le haut à y unités du sol. La longueur de l'échelle est **fixe**; lorsque x augmente et devient $x+dx$, y diminue en $y-dy$

Si initialement l'échelle est à 19 pouces du mur, et son sommet est à 180, si on éloigne la base de 1 pouce de combien change la hauteur.

la longueur est $$(19^2)+(180^2)=181^2$$ mais en augmentant x, on cherche le $dy$ associé
$$(20^2)+(y-dy)^2=181^2$$
$$y-dy= \sqrt{32361} = 179,89$$
donc, sachant la position de $y$ avant le changement $dx$

$$dy=179,89-180= -0,11 \ (descente)$$
$$y = \sqrt{l^2-x^2}$$

---
#### Cas trivial de dérivée 
Soit l'expression $y=x^2$. On garde en tête l'idée de grossir cette expression
$$y+dy=(x+dx)^2$$
$$y+dy=x^2+2xdx+(dx)^2$$
Ce $(dx)^2$ est tellement petit qu'on peut l'ignorer. Ce qu'on a présentement est la fonction initiale grossie, mais nous on veux le **grossissement**, on va retirer les termes de la fonction initiale
$$dy=2xdx \rightarrow \frac{dy}{dx} = 2x$$
Soit l'expression $y=x^3$. On garde en tête l'idée de grossir cette expression $$y+dy=(x+dx)^3$$$$y+dy=x^3+3x^2dx+3x(dx)^2 +(dx)^3$$Seul $dx$ compte, ses autres puissances sont négligeables:
$$dy=3x^2dx \rightarrow \frac{dy}{dx} = 3x^2$$
---

règle:

1.3 volume

---
#### Sommes produits et quotients

Pour l'addition, la règle est simple; **différencier chaque partie individuellement, les réunir**

Pour la multiplication, prenons $y = (x^{2}+c)\times(ax^{2}+b)$. Substituons pour obtenir $y = (u)\times(v)$ 
$$y + dy = (u+du)\times(v+dv)$$
$$y + dy = (uv +udv + vdu + dudv)$$
$dudv$ est négligeable, on peut retirer l'expression originale 
$$dy = (udv + vdu)$$$$\frac{dy}{dx} = (u\frac{dv}{dx} + v \frac{du}{dx})$$Pour la division, $$\frac{dy}{dx} = \frac{u\frac{dv}{dx} - v \frac{du}{dx}}{v^2}$$

---
#### Maximas - Minimas

Pour trouver un potentiel point *maximal ou minimal*, on doit trouver une valeur $x$ telle que **==son voisinage est strictement supérieur (minima) ou inférieur (maxima)==**. On cherche alors un point où la pente $\frac{dy}{dx}$ change de signe; **==elle est donc à 0 au moment du changement (maxima/minima)==**

Prenons $y=3x -x^2$, 
$$\frac{dy}{dx} =3-2x$$
$$3-2x=0 \rightarrow x=\frac{3}{2}$$
Pour savoir si ce point est un maximum ou minimum, il faudrait calculer pour les points voisins de part et d'autre et voir s'ils ont **tous deux un signe pareil** OU encore, voir la *variation* des pentes, ce qui revient a dériver une deuxième fois.

>La  dérivé première informe de la valeur de la tangente en un point P sur tout le domaine
>La dérivé seconde informe si la pente était croissante ou pas en tout point (négative/positive)

Dans le cas ou nous avons des signes alternés, c'est un point d'inflexion

---
Sinus cosinus

---
#### Intégrales

Prenons une dérivée $\frac{dy}{dx} =\frac{1}{5}x$, qui représente une droite  croissante de pente $\frac{1}{5}$, (pour chaque $x$, $y$ vaut $\frac{1}{5}x$. Chacun des changements peut être dessiné comme un triangle, et on peut essayer de reconstruire la courbe des variations à différents $x$

![[exp_02.jpg|292x238]]


Chaque triangle a comme base l'augmentation en $x$ et en hauteur l'augmentation en $y$, la valeur est le rapport du changement en $y$ par rapport au changement en $x$, et on **va les coller pointe à pointe un après l'autre (sommer les différences)**

![[exp_03.jpg|298x171]]


À n'importe quel point **P** , la valeur en $y$ est la somme de toutes les hauteurs $dy$ précédentes; mais $dy$ dépendait de $dx$. On sait que  $\int dy = y$. Chaque $dy = \frac{1}{5}x*dx$ qui reviens donc à calculer $\int \frac{1}{5}x*dx$

On remarque de $dx$ ne change pas, **mais $x$ (derrière la variation de y) change; il va de 0 à 5**. En partant de 0 jusqu'au point P, si on sommait les $dx$ on aurait la somme des n entiers naturels premiers et il faudrait donc **diviser cette distance par 2**. On aura

$$\frac{1}{5}\int x*dx = \frac{1}{5} (\frac{1}{2}) [?] $$

On remarque aussi que $dy$ variait toujours de façon linéaire, mais la valeur de $y$ à un point $P$, qui en est la somme, donne la somme à un $P$ pris $0+0,2+0,4+0,6 ... = P^2$ 

On a donc

$$\frac{1}{5}\int x*dx = \frac{1}{5} (\frac{1}{2}) x^2 = \frac{1}{10} x^2 +C $$

>[!important]
>$$\int_{a}^{b} x^{n}dx = \frac{x^{n+1}}{n+1}$$

==! Attention ! **Ne marche pas avec n = -1** car on diviserait par 0==

>[!important]
>$$\int_{a}^{b} e^{ax}dx = \frac{e^{ax}}{a}$$


---


## 4 tactiques fantastiqueuh

- **Substitution**:
	- On vois une fonction dans une fonction
	- les exponentielles, les racines
	- *u = ce qui est compliqué*
- **Intégration par parties** 
	- On vois un produit de fonctions: $xe^x, xln(x)$
	- u = *truc simple après avoir été dérivé*
- **Décomposition en fractions** (quand on divise par un polynôme)
- **Reconnaissance d’intégrales connues** (quand c’est une forme standard)

---
#### SUBSTITUTION

$$\int e^{2x} dx$$
- $2x$ est chiant, il dégage en $u$

$$\int e^{u} dx$$

---
#### IPP

$$\int_0^1 xe^{-2x} dx$$
Produit de $x$ et $e^{-2x}$, ==par partie==

|     |           |     |                          |
| --- | --------- | --- | ------------------------ |
| u   | x         | du  | 1                        |
| dv  | $e^{-2x}$ | v   | $$\frac{-1}{2} e^{-2x}$$ |

$$\int udv = uv - \int vdu$$


$$\frac{-1}{2} e^{-2x} - \int \frac{-1}{2} e^{-2x} dx$$






La primitive d'une fonction $I(x)$ est telle que sa **dérivée** nous redonne $I(x)$

>$G(x)' = I(x), \ F(x)' = I(x)$

Prenons une fonction définie comme étant la différence entre ces 2 fonctions primitives :
$$H(x) =G(x)- F(X)$$
La dérivée de $H(x)$ ressemble donc à $$H(x)' =G(x)' - F(X)' \rightarrow I(x)- I(x)$$
La différence entre $F(x)$ et $G(x)$ donne comme dérivée 0, c'est à dire que la seule chose qui restait après la différence des 2 est une constante $C$, d'où l'obligation de mettre + C

>Une intégrale de cos serait sin, mais sin +5 marcherait aussi


#### Intégrale d'une puissance

>[!important]
>$$\int_{a}^{b} x^{n}dx = \frac{x^{n+1}}{n+1}$$

==! Attention ! **Ne marche pas avec n = -1** car on diviserait par 0==
#### Intégrale d'une puissance $n = -1$

>[!important]
>$$\int_{a}^{b} \frac{1}{x}dx = log(x)$$

Intégrale d'une exponentielle

>[!important]
>$$\int_{a}^{b} e^{ax} = \frac{e^{ax}}{a}$$

