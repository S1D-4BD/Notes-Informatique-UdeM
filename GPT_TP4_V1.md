
### Partie A

Deux joueurs participent à un jeu de collecte de cartes. Il y a une pile contenant 20 cartes, numérotées de 1 à 20. Chaque carte a une couleur :

- 10 cartes rouges, numérotées de 1 à 10
    
- 10 cartes bleues, numérotées de 11 à 20

Un arbitre tire successivement des cartes de la pile, jusqu'à obtenir un certain nombre de cartes rouges. L'objectif des joueurs est de déterminer si le nombre total de cartes tirées avant d'atteindre ce seuil est faible ou élevé.

Les joueurs peuvent obtenir des informations partielles par l'une des deux stratégies suivantes :

- **Stratégie 1** : Observer directement le nombre total de cartes tirées avant d'obtenir 5 cartes rouges.
- **Stratégie 2** : Observer le nombre de cartes bleues tirées avant la cinquième carte rouge.

Quelle stratégie choisiriez-vous?

1. On définit la variable aléatoire (v.a.) **X** donnant le nombre total de cartes tirées jusqu'à obtenir 5 cartes rouges. Donner l'univers de **X**, noté $$S_X$$et sa fonction de masse, notée $$p_X : S_X \to [0,1]$$
    
2. On définit l'événement **E** = {le nombre total de cartes tirées avant la cinquième carte rouge est supérieur à 10}. Exprimer **E** en termes de **X** et calculer **P(E)**.
    

On introduit deux autres v.a. :

- **Y** donne le nombre total de cartes tirées avant d'obtenir 5 cartes rouges (Stratégie 1).
    
- **Z** donne le nombre de cartes bleues tirées avant la cinquième carte rouge (Stratégie 2).
    

1. Donner les univers $S_Y$ et $S_Z$            redes v.a. **Y** et **Z**.
    

Cas particulier : on suppose à présent que **X = 8**, c'est-à-dire qu'il a fallu tirer 8 cartes pour obtenir 5 rouges.

2. Sachant que **X = 8**, déterminer les univers **S_Y** et **S_Z**.
    
3. Donner les probabilités des événements **{Y = 8}** et **{Y = 9}** sachant que **X = 8**.
    
4. Même question pour **Z**, i.e., donner la probabilité des événements **{Z = 3}** et **{Z = 4}** sachant que **X = 8**.


On généralise le raisonnement précédent en supposant que **X = x** pour un **x \in S_X** inconnu mais fixe.

5. Compléter le tableau suivant :

| P(Y = y\|X=x) | y = 5 | y = 6 | y = 7 | y = 8 | y = 9 | y = 10 |
| ------------- | ----- | ----- | ----- | ----- | ----- | ------ |
| x = 5         |       |       |       |       |       |        |
| x = 6         |       |       |       |       |       |        |
| x = 7         |       |       |       |       |       |        |
| x = 8         |       |       |       |       |       |        |

6. Compléter le tableau suivant pour **Z** :

| P(Z = z\|X= x) | z = 0 | z = 1 | z = 2 | z = 3 | z = 4 | z = 5 |
| -------------- | ----- | ----- | ----- | ----- | ----- | ----- |
| x = 5          |       |       |       |       |       |       |
| x = 6          |       |       |       |       |       |       |
| x = 7          |       |       |       |       |       |       |
| x = 8          |       |       |       |       |       |       |

Nous voulons maintenant prédire si **E** s'est produit en fonction des observations.

7. Justifier la formule suivante : et expliciter comment obtenir **P(X = x | Z = z)**.
    
8. Compléter les tableaux suivants :
    
| P(X = x  Y = y) | x = 5 | x = 6 | x = 7 | x = 8 | x = 9 | x = 10 |
| --------------- | ----- | ----- | ----- | ----- | ----- | ------ |
| y = 5           |       |       |       |       |       |        |
| y = 6           |       |       |       |       |       |        |
| y = 7           |       |       |       |       |       |        |

| P(X = x  Z = z) | x = 5 | x = 6 | x = 7 | x = 8 | x = 9 | x = 10 |
| --------------- | ----- | ----- | ----- | ----- | ----- | ------ |
| z = 0           |       |       |       |       |       |        |
| z = 1           |       |       |       |       |       |        |
| z = 2           |       |       |       |       |       |        |

9. Donner la règle de décision pour un joueur utilisant la Stratégie 1 et observant **Y = y** pour prédire si **E** s'est produit. Faire de même pour un joueur utilisant la Stratégie 2 et observant **Z = z**.
    
10. Justifier pourquoi comparer les probabilités permet de déterminer la stratégie optimale. Calculer **\alpha_1** et **\alpha_2**, puis conclure.
    

---