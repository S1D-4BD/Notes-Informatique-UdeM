

C'est un **breakpoint** dans **l'exécution de f**  que je dois noter afin de prendre le temps de calculer $g(h(4))$ avant de continuer mon calcul. Naturellement, **si je savais** ce que valais $g(h(4))$ j'aurais fait  
$$Y= f(RetourG) $$
C'est à **cette instruction** que je dois retourner pour continuer mon calcul principal; mon return address est donc l'**instruction** où je calcule le retour de  $f(RetourG)$, nommé "RetourMain"
$$ Retour Main= f(RetourG) $$
Premier breakpoint : le calcul de  RetourG
$$RetourG = g(h(4))$$
Or à ce stade je ne connais pas ce que vaut $h(4)$ C'est un **breakpoint** dans **l'exécution de RetourG que je dois prendre afin de prendre le temps de calculer $h(4)$ avant de continuer mon calcul. Naturellement, **si je savais** ce que valais $h(4)$ j'aurais fait

$$RetourG = g(RetourH)$$

C'est à **cet autre instruction** que je dois retourner; mon second return address est donc le **l'instruction** où je calcule et retourne $h(4)$, nommé $RetourH$

Deuxième breakpoint: le calcul de $RetourH$
 $$RetourH = h(4) $$
 À ce stade, j'arrive à une fonction **connue**. Je dois noter un dernier breakpoint afin de me retrouver avec *une valeur concrète qui servira aux cas antérieurs* nommée "h(4)".
 
Troisième breakpoint: le calcul **direct** de $h(4)$ :
$$h(4) = 4^2 $$

***ICI, C'EST L'ORDRE DU CODE MIPS PUISQUE NOUS TRAVAILLONS AVEC DES VALEURS***. À ce stade *je ne NOTE plus de BREAKPOINT* pour calculer le résultat d'une fonction imbriquée encore, je peux calculer h(4) directement comme étant $4^2$ (le label de la fonction h -> h(x))
Ainsi, je sais que $$h(x) -> h(4) = 16$$J'ai terminé le calcul du troisième breakpoint $h(4)$, celle prise pour calculer la valeur la plus imbriquée. Alors je retourne au stade ayant causé la prise de la pause la plus récente (ici $h(4)$).

Le stade où on avait pris la pause $h(4)$ était  $$RetourH = h(4) $$Je sais ce que vaut $h(4)$, le retour attendu $RetourH$ devient $$RetourH = 16$$
Jai encore en mémoire une pause ayant été prise avant $RetourH$, soit la pause $RetourG$ qui était $$RetourG = g(RetourH)$$ Je sais ce que vaut $RetourH$, à ce stade $RetourG$ devient
$$RetourG = g(16)$$
Or à ce stade je ne prend pas de pause pour calculer une fonction imbriquée encore, je peux calculer g(16) directement comme étant $16^3$
Ainsi, je sais que  
$$RetourG = 4096$$
J'arrive à la fonction initiale (qui était mon calcul voulu avant de prendre toutes les pauses) qui était 
$$Y= f(RetourG) $$
Je sais ce que vaut $RetourG$, à ce stade $Y$ devient 
$$Y= f(4096) $$
À ce stade je *ne prend pas de pause* pour calculer une fonction imbriquée encore, je peux calculer $f(4096)$ directement comme étant $\sqrt{4096}$

Ainsi, je sais que le $Main$ (qui est donc le retour attendu de Y) est
$$Main =\sqrt{4096} = 64 $$

En **résumé** on calcule 
1) h(4) =>   jal label h(x), on calcule et on retourne à l'instruction qui aurait suivit qui est:
2) g(R1) => jal label g(x), on calcule et on retourne à l'instruction qui aurait suivit qui est:
3) f(R2) =>  jal label f(x), on a terminé le calcul
