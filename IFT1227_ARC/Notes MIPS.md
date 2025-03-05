
Notions de base:
1 byte = 8 bits
1 halfword = 2 bytes (16 bits)
1 word = 4 bytes (32 bits)

Adresses et pointeurs:

La mémoire est comme un gros array, et les éléments ont comme index l'adresse à laquelle ils sont stockés

>==Langage machine != langage assembleur==. Le langage machine serait 1009018700000342 et en assembleur ce serait **add, $ a0, $ t0, $ t1**

---
#### Concept général

MIPS est un langage proche du matériel, la **complexité des opérations diminue** et le **nombre de lignes à coder augmente**

ex. "Prend une cuillère à soupe et mange ce plat" VS

"Prépare toi à tenir un objet : 
- L'objet est une cuillère  
Prend ta main droite: 
- "Tant que tu n'as pas touché la cuillère, avance" 
Si ta main touche, agrippe la cuillère:
- "tant que tu n'as pas touché le bol, avance" 
Si tu touches le bol avec la cuillère, plonge la cuillère: 
- "etc..."

---
#### Registres MIPS

**v0-v1** =  ==retournent== les valeurs des appels de fonctions ; si quelque chose est calculé, il est gardé dans v0 et v0+v1 si le résultat est sur 64 bits

**t0-t9** = registres qui ne sont ==pas sauvegardé==s et qui peuvent être réécris sans problème

**s0-s7** = registres dont la valeur est ==gardée== dans la pile (ne peuvent pas êtres directement changés)

**a0-a3** = registres servant d'arguments aux fonctions

---
### Exo 1 : Lire 2 input numériques, les additionner, imprimer la somme 

##### **Décortiquer le problème:**

1) *Préparer* le système à lire un int ($v0 <-5)
2) Syscall (lecture)
3) Déplacer le contenu de retour dans un registre ($t0 <- $v0)
4) Préparer le système à lire un autre int ($v0 <-5)
5) Syscall (lecture)
6)  Déplacer le contenu de retour dans un registre ($t1 <- $v0)
7) Additionner les valeurs des 2 registres dans un troisième registre (add $t2, $t1, $t0)
8) Déplacer le contenu du troisième registre dans une case destinée à l'affichage ($a0 <- $t2)
9) Faire comprendre au système qu'on veux imprimer un int $v0 <-1)
10) Call

##### **et maintenant en code :**

```MIPS
.data
.text
main:
	li      $v0,5
	syscall
	move    $t0,$v0
	
	li      $v0,5
	syscall
	move    $t1,$v0
	
	add     $t2,$t1,$t0
	
	move    $a0,$t2
	li      $v0,1
	syscall

```

---
### Exemple `larger.asm` : lire 2 input numériques, afficher le plus grand

Décortiquer le problème:

1) Préparer le système à lire un int #1 ( $v0 <- 5 )
2) Syscall (lecture)
3) Save dans un registre ($t0 <- $v0)
4) Préparer le système à lire un int #2 ( $v0 <- 5 ) 
5) Syscall (lecture)
6) Save dans un registre ($t0 <- $v0)
7) Branch on Greater Or Equal vers *t0_bigger* si input#1 > input#2
8) *t0_bigger* : 
	1) affecte t0 dans le registre "larger" $t2
	2) Branch à "*fin*" 
	3) sinon…
9) Save t1 dans le registre "larger" $t2
10) *fin* :
	1) Préparer le système à afficher un int ($v0 <- 1)
	2) Mettre dans le registre pour afficher la valeur de t2 ($a0 <- $t2 )
	3) Syscall

en code : 

```MIPS
.data
.text
main: 
	li $v0,5
	syscall
	move $t0, $v0
	
	li $v0,5
	syscall
	move $t1, $v0
	
	bgt $t0,$t1, t0_big #si  t0 > t1 on va à t0_big
	move $t2,t1         #sinon on continue
	b endif             #on saute a la fin du programme
t0_big:
	move $t2,t0
	# pas besoin de branch, on y va direct
endif:
	move $a0, $t2
	li $v0,1
	syscall
```

---
 >[!TRICKS]
 >.byte 0 : + 0 byte.
 >.ascii "\n"      # C **newline**. 
 >.asciiz            # \n en fin de ligne
 >.byte 0xA      # hex ASCII **newline**
 >.byte 0x0       # hex ASCII **NULL**
 
 ---
 Algorithme de multiplication **séquentielle**:

Une multiplication est une addition **successive**. On va ajoute un int B à un int A, et lorsqu'on  cette somme atteint le nombre 

Donc: pour 3* 4
1) Obtenir A de user (3)
2) Obtenir B de user (4, valeur)
3) Déclarer C (itérateur) C = A à init
4) Déclarer R (résultat) R = 0
5) si C >= 0 on branch à *multiplication*
6) *multiplication* : 
	2) ajoute B à R
	3) retire 1 de C
7) Si C=0, branch à *fin*
8) Sinon branch à *multiplication* (loop)
9) *fin*:
	1) Préparer la systeme à print R

Ici, A et B ne doivent **pas** changer, mais R et C doivent changer, ça veux dire que les registres utilisés pour A et B ne peuvent pas être de même type

A et B doivent êtres sauvegardés, tandis que C et R doivent êtres temporaires

```MIPS
.data
.text
main: 

#s0 = A (3)
#s1 = B (4)
#t0 = resultat
#t1 = compteur

li $v0,5     #lire A
syscall
move $s0,$v0 #save A

li $v0,5     #lire B
syscall
move $s1,$v0 #save B

li $t0,0     #initialise le résultat = 0
move $t1,$s0 #initialise le compteur = A


multiplication: 
	add $t0,$t0,$s1  #j'ajoute B au result
	addi $t1,$t1, -1 #j'enlève 1 à compteur (1 step faite)

beq $t1,$zero, fin   #si on a fini on saute à fin

b multiplication # sinon bah pas fini, on multiplie

fin:
	li $v0,1  #preparer a output un int
	move $a0,t0 #met le resultat dans boite à print
	syscall
	li $v0,10
	syscall

```

---
### String en MIPS

On déclare un string de cette façon:

---
#### Jump and Link, Return Adresse (instruction suivante)

**Exemple mathématique:**

On souhaite afficher à la fois la somme et la différence entre deux nombre, a et b avec les fonctions
$$
\begin{align*}
somme(a,b) = a+b \\
difference(a,b) = a-b \\
\end{align*}
$$

et exécuter l'affichage de somme(a,b) , affichage de somme(a,b) dans cet ordre

Soit a = 10, et b = 4

Nous savons que pour afficher les réponses correctes on doit calculer d'abord le retour des fonctions $somme(a,b)$ et $difference(a,b)$, garder en mémoire ces résultats sous $R1$ et $R2$, et ensuite afficher ces derniers. 

##### Étape 1) Arguments
On charge a et b comme arguments de fonctions (registres $ax$)
	a0 <- 10
	a1 <- 4
##### Étape 2) Somme(a,b)
on Jump And Link vers la fonction *somme*. Le jump implique qu'on mette dans $ra$ **l'instruction qu'on ferait si je savais ce que valais somme(10,6)**. Comme je ne le sais pas, je garde dans ra l'instruction "*sauvegarder le retour dans une variable temporaire*"

##### Étape 2.1) somme: 
dans *somme* j'additionne les contenu de a et b dans un registre de retour de valeur de type $vx$ et je **Jump Register à l'endroit où j'aurais continué l'exécution de la fonction englobante si j'avais les valeurs**. Cet endroit est l'adresse pointée par $ra$.   
	add v0, a, b   :   v0 <- 14
	jr $ra
Comme ra contenait l'instruction de *sauvegarder le retour dans une variable temporaire*, on le fait 

etc.

---
Traduction en Mips


```
.data
a: .word 10   # Premier nombre (a = 10)
b: .word 5    # Deuxième nombre (b = 5)
R1: .word 0   # Espace pour le résultat de la somme
R2: .word 0   # Espace pour le résultat de la différence

.text
main:
    
    lw $a0, a            #  a = 10 dans $a0
    lw $a1, b            #  b = 5 dans $a1

    jal sum  
    move $t0, $v0   

    jal difference  
    move $t1, $v0 

    li $v0, 10           
    syscall

sum:
    add $v0, $a0, $a1    # $v0 = $a0 + $a1
    jr $ra               # Retourner à l'appelant

difference:
    sub $v0, $a0, $a1    # $v0 = $a0 - $a1
    jr $ra               # Retourner à l'appelant


```


---

#### Récursion simple en MIPS

La fonction récursive de puissance est une fonction de 2 cas ; le cas récursif (elle s'appelle elle-même) et le cas de base (une valeur connue)

En général, on a 5 étapes pour un code impliquant de la récursion (excluant la fin)

1) Entrer dans la fonction (exécution du main)
2) Vérification du Cas de base
3) Jump récursif
4) Retourner à l'appelant
5) Cas de base

$$
\begin{equation}
    Puissance(b,e) =
    \begin{cases*}
	    b*Puissance(b,e-1) & si e > 0  \\
	      1        & si e = 0 \\
    \end{cases*}
  \end{equation}
$$
On récupère d'abord les paramètres de la fonction, donc b (base) et e (exposant)
Dans le main, **dès qu'on aura obtenu une valeur** on sauvegarde le résultat et on l'affiche (cette partie est après les étapes récursives)

```
.data
.text
main : 
	li a0, b
	li a1, e

	jal puissance

	move result ,a0
	li v0, 1
	move a0,result
	syscall
```

Le cas de base est une adresse particulière qui **retourne une valeur au dernier appel** si elle est vérifiée, et qui saute vers la récursion si elle n'est pas vérifiée

```
puissance:
	bne a1,zero,recursion #si pas = 0, on recurse
	li v0,1               #sinon valeur = 1
	jr ra                 # on remet ce result a l'étape 
	                      # qui aurait suivi si on avait un chiffre
```

Les étapes pré récursives consistent à allouer de l'espace pour le retour, les paramètres utiles et les modifier 

```
recursion:
	addi sp, sp -4   #laisser espace pour le retour
	sw ra,0(sp)      #stocker retour à la place réservée
	addi a1,a1,-1    #modifier le paramètre concerné
```

Le saut récursif consiste à jump à nouveau à l'étape de vérification du cas de base juste après les étapes pré récursives et garder à ra ce qu'on aurait fait si on avait déjà atteint le cas de base (qui est le calcul en lui même)

```
recursion:
	addi sp, sp -4   #
	sw ra,0(sp)      #
	addi a1,a1,-1    #
	jal cas_base     # on refait; pour next récursion
```

Dès qu'on aura atteint un premier retour de valeur (le jr suivant cas de base) on devra effectuer un calcul, qui est placé juste après le jal, puisque le ra note l'instruction qui aurait été faite si on avait une valeur pour calculer au lieu de sauter en récursion. Ca sera fait jusqu'à ce qu'on aura atteint le ra qui a stocké comme prochaine instruction "*terminer le programme*"

```
recursion:
	addi sp, sp -4  #
	sw ra,0(sp)     #
	addi a1,a1,-1   #
	jal cas_base    # on refait; pour next récursion
	
	mul v0, a0, v0  # le calcul lui meme
	lw ra, 0(sp)    # ce  quon aurait fait (frame précédent)
	addi sp, sp 4   # on vide le stack de cette instruction
	jr ra           # on y va
```

trick, avant le jal et après bah c'est la même chose, juste à l'inverse

```

.data
.text

main : 
	li a0, b
	li a1, e

	jal puissance    #sauter dans le cas de base
	move result ,a0
	li v0, 1
	move a0,result
	syscall
	
puissance:
	bne a1,zero,recursion #si pas = 0, on recurse
	li v0,1               #sinon valeur = 1
	jr ra                 # on remet ce result a l'étape 
	                      # qui aurait suivi si on avait un chiffre

recursion:
	addi sp, sp -4   #laisser espace pour le retour
	sw ra,0(sp)      #stocker le retour à l'appel antérieur
	addi a1,a1,-1    #modifier le paramètre concerné
	jal puissance    # next récursion
	
	mul v0, a0, v0  # le calcul lui meme
	lw ra, 0(sp)    # ce  quon aurait fait (frame précédent)
	addi sp, sp 4   # on vide le stack de cette instruction
	jr ra           # on va au call précédent
```

Évolution du code

| Instru                          | ra                         | a   | b   | v0 (resultat) |
| ------------------------------- | -------------------------- | --- | --- | ------------- |
| a0 = 5                          | -                          | 5   | -   | -             |
| a1 = 3                          | -                          | 5   | 3   | -             |
| jal puissance                   | -                          | 5   | 3   | -             |
| addi sp, sp -4                  | **imprimer**               | 5   | 3   | -             |
| ==sw ra,0(sp)==                 | imprimer                   | 5   | 3   | -             |
| addi a1,a1,-1                   | imprimer                   | 5   | 3   | -             |
| jal puissance                   | imprimer                   | 5   | 2   | -             |
| ~~bne a1,zero,recursion~~       | **mul v0, a0, v0**         | 5   | 2   | -             |
| addi sp, sp -4                  | mul v0, a0, v0             | 5   | 2   | -             |
| ==sw ra,0(sp)==                 | mul v0, a0, v0             | 5   | 2   | -             |
| addi a1,a1,-1                   | mul v0, a0, v0             | 5   | 2   | -             |
| jal puissance                   | mul v0, a0, v0             | 5   | 1   | -             |
| ~~bne a1,zero,recursion~~       | **mul v0, a0, v0**         | 5   | 1   | -             |
| addi sp, sp -4                  | mul v0, a0, v0             | 5   | 1   | -             |
| ==sw ra,0(sp)==                 | mul v0, a0, v0             | 5   | 1   | -             |
| addi a1,a1,-1                   | mul v0, a0, v0             | 5   | 1   | -             |
| jal puissance                   | mul v0, a0, v0             | 5   | 0   | -             |
| ==***bne a1,zero,recursion***== | **mul v0, a0, v0**         | 5   | 0   | -             |
| jr ra                           | mul v0, a0, v0             | 5   | 0   | 1             |
| mul v0, a0, v0                  | mul v0, a0, v0             | 5   | 0   | **5**         |
| lw ra, 0(sp)                    | mul v0, a0, v0             | 5   | 0   | **5**         |
| addi sp, sp 4                   | ==mul v0, a0, v0 # 3==     | 5   | 0   | **5**         |
| jr ra                           | ==mul v0, a0, v0 # 3==     | 5   | 0   | **5**         |
| ==mul v0, a0, v0 # 3==          | ==mul v0, a0, v0 # 3==     | 5   | 0   | **5**         |
| lw ra, 0(sp)                    | ==mul v0, a0, v0 # 3==     | 5   | 0   | **25**        |
| addi sp, sp 4                   | ==mul v0, a0, v0 # 2==<br> | 5   | 0   | **25**        |
| jr ra                           | ==mul v0, a0, v0 # 2==<br> | 5   | 0   | **25**        |
| ==mul v0, a0, v0 # 2==          | ==mul v0, a0, v0 # 2==<br> | 5   | 0   | **25**        |
| lw ra, 0(sp)                    | ==mul v0, a0, v0 # 2==<br> | 5   | 0   | 125           |
| addi sp, sp 4                   | ==imprimer # 1==           | 5   | 0   | 125           |
| jr ra                           | ==imprimer # 1==           | 5   | 0   | 125           |
| ==imprimer # 1==                | FIN                        |     |     |               |

| STACK                  |
| ---------------------- |
| ==imprimer # 1==       |
| ==mul v0, a0, v0 # 2== |
| ==mul v0, a0, v0 # 3== |

---
Exemple somme des chiffres

$$
\begin{equation}
    sommeChiffres(n) =
    \begin{cases*}
	    (n mod 10)+sommeChiffres(n // 10) & si n > 0  \\
	      0        & si n = 0 \\
    \end{cases*}
  \end{equation}
$$

```
.data
number: .word 123  #nombre de 4byte
result: .word 0   #la variable de résultat

.text
.globl main

main:
    lw $a0, number  #load param de fonction a0 (123)
    jal base        #vérif du cas de base
    sw $v0, result  #si on a atteint la fin des retours, on remplit le result
    move $a0, $v0
    li $v0, 1
    syscall
    li $v0, 10
    syscall

base:
    beq $a0, $zero, base_case #si est le cas de base, branch
    li $t0, 10                #sinon load 10 (le diviseur)
    div $a0, $t0              #diviser par 10
    mfhi $v1                  #recup l'entier
    mflo $t2                  #recup le modulo
    addi $sp, $sp, -8         #laisser de l espace pour 2 infos:
    sw $ra, 0($sp)            #stocker le retour
    sw $v1, 4($sp)            #stocker le modulo
    move $a0, $t2             #mettre l'entier comme nouveau param
    jal base                  #recurison: verif cas de base encore
    lw $v1, 4($sp)            #post-base: load le modulo
    lw $ra, 0($sp)            #post-base: load le précédent retour
    addi $sp, $sp, 8          # ... : vider le stack
    add $v0, $v0, $v1         # ... : add le modulo à result 
    jr $ra                    # add le prochain modulo au result en jump

base_case:
    li $v0, 0                #premiere valeur concrète
    jr $ra

```
