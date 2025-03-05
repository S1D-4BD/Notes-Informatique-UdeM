
DÉNOMBREMENT: 

### Comment distinguer une **p-liste**, un **arrangement**, et une **combinaison** ?

#### **p-liste** :
- L’ordre **compte**.
- Les répétitions **sont autorisées**.
- **Exemple** : Si on a \( E = \{A,B,C\} \) et qu'on prend \( p = 2 \), on peut former :  
  $[(A,A), (A,B), (A,C), (B,A), (B,B), (B,C), (C,A), (C,B), (C,C)]$
- **Formule** pour compter le nombre de **p-listes** dans un ensemble de \( n \) éléments :
  $[n^p]$
- **Application** : On l’utilise lorsqu’on tire ==des éléments **avec remise**== (on peut répéter les éléments).

---

#### **Arrangement de p éléments parmi n** :
- L’ordre **compte**.
- Les répétitions **ne sont pas autorisées**.
- **Exemple** : Avec \( E = \{A,B,C\} \) et \( p = 2 \), on a :  
  \[  (A,B), (A,C), (B,A), (B,C), (C,A), (C,B)  \]
  mais **pas** \( (A,A), (B,B), (C,C) \) car les répétitions ne sont pas autorisées.
- **Formule** :
  $A_n^p = \frac{n!}{(n-p)!}$
- **Application** : On l’utilise lorsqu’on tire des éléments ==**sans remise**, et où **l'ordre COMPTE**==

---
#### **Combinaison de p éléments parmi n** :
- L’ordre **ne compte pas**.
- Les répétitions **ne sont pas autorisées**.
- **Exemple** : Avec \( E = \{A,B,C\} \) et \( p = 2 \), les combinaisons sont :  
  $[  \{A,B\}, \{A,C\}, \{B,C\}]$
  On ne distingue pas $( \{A,B\})$ et  $( \{B,A\})$, car **l’ordre ne compte pas**.
- **Formule** (coefficient binomial) :
  $C_n^p = \binom{n}{p} = \frac{n!}{p!(n-p)!}$  
- **Application** : On l’utilise lorsqu’on fait un tirage ==**simultané**== ou ==**sans remise**==, mais où ==**l'ordre ne compte pas**==

---
- combinaisons : tirage ==**sans remise**==, mais où ==**l'ordre ne compte *pas*
- arrangement : tirage **==sans remise==** où **==l'ordre *compte*==**
- permutations : tirage ==**avec remise**==
---
