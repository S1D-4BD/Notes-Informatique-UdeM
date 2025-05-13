
---
1.0 parenthésage
1.0.1 pigeonnier
# **1.1 Les langages REPEAT**

Machines de type REPEAT sont des modélisations de langages **séquentiels** à itérations **finies**; nous devons **savoir combiens de tours de boucles** sont exécutées en tout temps, impliquant que le programme va toujours se terminer **(aucune boucle infinie)**. **==Tout est défini dans les *naturels*; les négatifs n'existent pas==**

> ==La récursivité est **simulée** par appels successifs== d'une même macro, mais cette macro ne définie pas le nombre de tours de boucle ; ==concept de primitives récursives==

### Formalités et opérations de bases

*Pour toute modélisation de machine, **le nombre de registres est non important** puisqu'il n'est **pas limité par le matériel***

1) $r_i \leftarrow r_j$ ; affecter le contenu de $rj$ dans $r0$
2) $inc(r_i)$; incrémenter de 1 le contenu de $r_i$
3) $REPEAT \ r_i \ [BLOC]$ ; répéter $r_i$ fois le bloc d'instruction en paramètre


>**==Attention; les booléennes classique (if-else, not etc..) ne sont pas définies nativement==**

### Propriétés structurelles et récursives

- Soit $R_p$ l'ensemble des programmes de type REPEAT 
- Soit $S_0$ l'ensemble des programmes atomiques (opérations de bases permises) tel que $$S_0 =\{(inc()) \cup (r_i \leftarrow r_j)\}$$avec $S_0 \subset R_P$$

**==On établie que:==**
- **la concaténation de deux instructions atomique est toujours élément d'un programme de type REPEAT**
- **La répétition d'un programme REPEAT renvoie aussi un programme REPEAT**

1) $\forall S_0, S_1, \ (S_0 \cdot S_1) \in R_p$ 
> l'ensemble des programmes de type REPEAT **==est clôturé pour la concaténation==**; la composition séquentielle est élément des $R_p$

2)  $S_0(S_1) \in R_p$ 
> L'ensemble est **stable par opération de répétition**; une ==opération atomique effectuée sur une autre opération atomique renvoie encore un programme== de l'ensemble des $R_p$

#### Programme d'addition:

```bash
r0 = DAT(0) #REGISTRE RÉPONSE
r1 = DAT(x) #param 1
r2 = DAT(y) #param 2

ro <- r1 //affecter param 1 à la réponse

répéter r2 fois[
	inc(r0) #on ajoute 1 à x "y fois" 
]
# retourne x + y(1)

```

#### Programme de multiplication:

```bash

r0 = DAT(0) #REGISTRE RÉPONSE
r1 = DAT(x) #param 1
r2 = DAT(y) #param 2

répéter r1 fois[ # pour tout n de 1 à r1 on éxécute..
	répéter r2 fois[ # 1 à r2 fois...
		inc[réponse] # l'incrementation de la réponse
	]
]
```

#### Programme d'exponentiation:

```bash
r0 = DAT(0) #REGISTRE RÉPONSE
r1 = DAT(a) #param 1 ; BASE
r2 = DAT(b) #param 2 ; PUISSANCE

r0 <- 1 
	répéter r2 fois[ # 1 à r2 fois on va...
		r0 <- MULT(r0,r1) #multiplier la réponse par la base
	]
]

```

#### Programme de décrémentation: ==important, négatifs non définis==

```bash
r0 = DAT(0) #REGISTRE RÉPONSE
r1 = DAT(x) #param à décrémenter
y = DAT(0) # incrémenteur delayed 

répéter r1 fois[
	r0 <- y # first step on a mis 0 dans 0, création d'un retard
	inc(y) # avec le retard, on incrémente de 0 à x-1 
]
```

### Programme de soustraction : utiliser DEC

```bash
r0 = DAT(0) #REGISTRE RÉPONSE
r1 = DAT(x) # param de base, x
r2 = DAT(y) # param y, ce quon doit retirer à x

r0 <- r1 # affecte x au registre
répéter r2 fois [ # on soustrait y fois "1" de x
	r0 <-dec(r0)
]
```

### Programme de factorielle:

```bash
r0 = DAT(0) #REGISTRE RÉPONSE
r1 = DAT(y) # base

#concept: on va faire
# 1 x (1+1) x (1+1+1) x...x (1+...+1)
# les parentheses sont présentes y fois 
# pour chaque parenthèse, le nombre d'addition est égale au numéro de la parenthese dans l'itération

répéter r1 fois 
	inc(y) # y augmente de 1 à chaque step
	r0 <- mult(r0,r1) # on multiplie x "y" fois
	
```

### Simulation des booléennes

Comme le ==typage n'est pas dans les opérations de base== (pas de string, char, booléens définis), on admet que **1 vaudra "vrai" et 0 vaudra "faux"**

> `si ri, alors[bloc]` deviendra `répéter ri fois [bloc]`

>C'est comme dire "==**fait la boucle encore une fois**==" lorsque $ri$ est mis à 1, sinon il s'arrête si c'est 0

### NOT logique: 

```bash
r0 = DAT(0 ou 1)
r0 <- MOINS(1,r0)
```

- "1" - 0 = 1
- "1" - 1 = 0
### AND logique: 

```bash
ro = DAT(0 or 1)
r1 = DAT(0 or 1)

r0 <- MULT(r0,r1)
```

- 0 * 0 = 0
- 0 * 1 = 0
- 1 * 0 = 0
- 1 * 1 = 1
### OU LOGIQUE ; 2 FAÇONS

>A REVOIR


### Plus Grand que

```bash
# Concept: si y est inférieur à x, la soustraction x-y renverras 0, et on entrera jamais dans répéter (false). Sinon, on continue de soustraire y (init r0 à vrai) et lorsquon aura soustrait le dernier facteur, on entrera pas dans la boucle, rendant le résultat définitif

GT(x,y)
	z <- MOINS(x,y)
	REPEAT z fois[
		r0 <- vrai
	]
```

Plus grand OU égal

```
Concept: soit x et y, on veux verifier si x >= y
x > = y :: NOT(y>x)

5>=5 = NOT(5>5), FAUX QUI DEVIENT VRAI
3>=1 = NOT (1>3), FAUX QUI DEVIENT VRAI
3>=8 = NOT(8>3), VRAI QUI DEVIENT FAUX

GTE(x,y)
z <- (y>x)
r0 <- NEG(z)

```
---
### Division:

```bash
#division de a/b
b = denominateur
a = numerateur
accumulateur = registre de sommation

#Concept: on va additionner "a" fois la base à l'accumulateur pour voir combien de fois cette base est requise pour que la somme atteigne "a" (on incrémente r0 comme compteur). 
#Pour chaque tour, un rigistre booleen "incomplet" est mis à jour avec la comparaison (accumulateur <= a?)

répéter a fois [
	accumul <- PLUS(accumul, b)
	incomplet <- (accumul <= a?)
	si incomplet alors [
		inc(r0)
	]
]
```

Modulo:

```
concept: x mod y, c'est trouver un r tel que x = q*y +r
1) q = x/y (quotient)
2) c = q*y (partie entiere)
3)x - c = r (restant)

q <- DIV(x,y)
c <- MULT(q,y)
r0 <- MOINS(x,c)
```

### Premier :

```
Concept: tester tout les candidats de division, si nous arrivons au nombre initial, alors on laisse faux, si a un moment le modulo donne 0, alors on revoie vrai

PRIME(x)

r0<-faux
si
```


---

## Codage de Gödel

Une façon de garder en mémoire un tableau sans structure concrète, consiste à encoder des valeurs séquentielles en le mettant comme puissances de nombres premiers successifs

> (5, 2, 3, 17, 13, 0, 0, 0, …) devient $2^{5}3^{2}5^{3}7^{17}11^{13}$

La profondeur du tableau est le niveau de puissance

>((1, 2, 3, 0, …), (4, 5, 0, …), (6, 7, 0, …), 0, …) devient $2^{(2^{1}3^{2}5^{3})}3^{(2^{4}3^{5})}5^{(2^{6}3^{7})}$

---

