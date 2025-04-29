
----
# 1. 
![[tp02_qst1.jpg]]

# 2.

![[tp02_qst2.jpg]]

j'ai rien capté à ce foutu exo la vérité, très bizarre...


![[tp02_qst3.jpg]]



---
# 4. 

![[tp02_qst4a.jpg]]
![[tp02_qst4b.jpg]]

**a)  Univers?**

$S$ = ensemble des 5 piges consécutives ordonnées de cartes uniques parmi 52 cartes : $$S = \{ (a1,a2,a3,a4,a5) \} | \ a1 \neq a2 \neq a3 \neq a4 \neq a5 $$
- Comme la pige est *partielle, ordonnée, non répétée* c'est un **arrangement** 
- $S$  = $A {52 \choose 5}$  = $\frac {52!}{(52-5)!}$ = $52 * 51 * 50 * 49 * 48$

b.1) **Exemple d'évènement ?**
Soit **f(n) $\rightarrow$ figure** une fonction surjective reliant chacune des 52 cartes à une des 13 figures du paquet tel que

$$
\begin{equation}
    f(n) =
    \begin{cases*}
	    (n-1) \% 13  \\
	      13        & si n-1 = 0 \\
    \end{cases*}
  \end{equation}
$$
On pourrait avoir $B =\{8, 21, 2,15,28\}$
puisque 
- f(8)  = f(21)= 8
- f(2) = f(15) = f(28) = 2

b.2) **Probabilité de B ?**

On demande la probabilité de B, sachant que B se produit ainsi 

==L'ordre est important entre la paire et le triple, mais pas entre les cartes à l'intérieur des paquets==
1) je choisi 2 carte parmi 4 pareilles -> j'ai 13 figures offrant ce choix
2) je choisi 3 cartes parmi 4 pareilles -> jai 12 figures offrant ce choix
3) je permute les cartes de la paire entre elle et les cartes du triplet entre elles (permutation = n!) -> 3! * 2!

donc je fait

${13 \choose 1}$ * ${4 \choose 2}$ * 3! * ${12 \choose 1}$ * ${4 \choose 3}$ * 2!

---
# 5.

![[tp02_qst5.jpg]]

#### a)  Toutes les variables $>$ 0 ?

Ça implique que la condition **toutes les variables $\geq$ 1** est valide aussi

Pour les 17 balles (O, on doit donc garantir 1 balle (X) dans chaque bac  et on a un schéma du style :

XOOO | XOOOOOOO | XOOOO ou
X | XOOOOOOOOOO | XOOOO

On a 3 zones à remplir (donc 2 murs à placer ) avec les 17-3 balles restantes et **l'ordre ne compte pas** (ajout au dénominateur de (r-1)! )
- on a une partition Pa ${n+r-1 \choose 2}$ = ${14+2 \choose r-1}$ = $\frac {16!} {14!2!}$ = 120

#### b)  Toutes les variables $\geq$ 0 ?

On a aucune restriction autre que la non négativité et on a un schéma du style :

OOOO | OOOOOOOO | OOOOO ou
OOOOOOOOOOOO |  | OOOOO

On a 3 zones à remplir (donc 2 murs à placer ) avec les 17 balles
- on a une partition Pa ${n+r-1 \choose 2}$ = ${17+2 \choose r-1}$ = $\frac {19!} {17!2!}$ = 120

#### c) $x1 \geq 1, x2 \geq 2, x3 \geq 3$

On a une condition pour chacune des variable, ==mais le plus important est le nombre de balles restantes==

Pour retourner à la condition de base ($\geq 0$) on change de variable pour ajuste le nombre de balles :

XOOO | XXOOOOOO | XXXOO ou
XOOOOOOOOO | XX | XXXOO

on a fait que $x1 = y1 + 1, 2 = y2 + 2, y3 + 3$, avec les constantes introduites on ajuste le nombre de balles -> 17- (1+2+3) = 11

On a 3 zones à remplir (donc 2 murs à placer ) avec les 11 balles restantes
- on a une partition Pa ${n+r-1 \choose 2}$ = ${11+2 \choose r-1}$ = $\frac {13!} {11!2!}$ = 78

---
# 6.

![[tp02_qst6.jpg]]

a) ex élément valide

soit l'univers de $n =4 : \{1..2n\} \rightarrow \{1,2,3,4,5,6,7,8\}$ , on pourrait avoir fait l'expérience et avoir eu $\{ \{3,5\} \{2,7\} \{1,4\} \{6,8\} \}$

b) Soit D un évenement avec la meme parité pour chaque élément.{{1,3}{2,4}{5,7}{6,8}} : 

Sois {}

---
# 7.

![[tp02_qst7.jpg]]

si je lance le d 1 fois, la somme varie de 1 .. 6 il y en a 6
si je lance le dé 2 fois, la somme varie de 2 ..12 il y en a 11
si je lance le dé n fois, la somme varie de n à 6n il y en a (6n - n) +1

a) l'univers dépendamment de n = {n... 6n} et |B| = 5n+1



