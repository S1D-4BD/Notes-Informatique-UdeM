Écrire un programme en langage C permettant de saisir les informations d’un patient sédentaire (moins actif) : - Son poids en nombre de kg (un réel) ; - Sa taille en mètre (un réel)

---



```c

#include <stdio.h>

// Celina Sid Abdelkader
// Aland Talib Ridha Barzani
int main() {
	
	
	float poids, taille, imc; // poids taille et imc
	char option; // variable pour continuer ou non
	int compteur = 0; // compteur pour le nombre de calcul d imc faits

	do {
		// demande au user d'entrer son poids en kilo
		printf("\n Entrez votre poids en kg : ");
		scanf("%f", &poids);
		
		// verifie si le poids entré est valide (pas negatif), sinon on redemande
		while (poids < 0) {
			printf("Poids invalide \n");
			printf("Entrez votre poids en kg (utiliser le point, pas de virgule) : \n");
			scanf("%f", &poids);
		}
		
		// user entre sa taille
		printf("Entrez votre taille en metres : ");
		scanf("%f", &taille);
		
		// validation aussi de la taille, sinon on redemande
		while (taille < 0) {
			printf("Taille invalide\n");
			printf("Entrez votre taille en metres : ");
			scanf("%f", &taille);
		}
		
		// calcul de l'imc
		imc = poids / (taille * taille);
		printf("Votre IMC : %.2f \n", imc);
		
		// Affichage du résultat selon l'IMC
		if(imc < 18.5) {
			printf("MAIGREUR, RISQUE ELEVE A ACCRU\n\n");
		} else if(imc < 25) {
			printf("POIDS NORMAL, RISQUE FAIBLE\n\n");
		} else if(imc < 30) {
			printf("EMBONPOINT, RISQUE ELEVE\n\n");
		} else {
			printf("OBESITE, RISQUE TRES ELEVE\n\n");
		}
		
		// On a calculé un imc valide donc on va augmenter le compteur
		compteur++;
		
		// demander au user sil veux continuer ou non
		printf("Calculer IMC encore? (o/n) : \n");
		scanf(" %c", &option);  

	} while(option == 'o' || option == 'O'); // si le user entre o ou O le programme continue

	// print le nombre total de cas calculés
	printf("Nombre total de cas calcules : %d\n", compteur);

	return 0;
	
	/*
	TESTS EXECUTION (CONSOLE)
			
				
		 Entrez votre poids en kg : 51
		Entrez votre taille en metres : 1.98
		Votre IMC : 13.01
		MAIGREUR, RISQUE ELEVE A ACCRU
		
		Calculer IMC encore? (o/n) :
		o
		
		 Entrez votre poids en kg : 69.4
		Entrez votre taille en metres : 1.63
		Votre IMC : 26.12
		EMBONPOINT, RISQUE ELEVE
		
		Calculer IMC encore? (o/n) :
		o
		
		 Entrez votre poids en kg : 60
		Entrez votre taille en metres : 1.65
		Votre IMC : 22.04
		POIDS NORMAL, RISQUE FAIBLE
		
		Calculer IMC encore? (o/n) :
		o
		
		 Entrez votre poids en kg : 100
		Entrez votre taille en metres : 1.72
		Votre IMC : 33.80
		OBESITE, RISQUE TRES ELEVE
		
		Calculer IMC encore? (o/n) :
		n
		Nombre total de cas calcules : 4
		
		--------------------------------
		Process exited after 49.17 seconds with return value 0
		Appuyez sur une touche pour continuer...
}

```


---

Dans un programme en langage C, un(e) étudiant(e) a écrit le code suivant : 
```c
//manque int main()
int rang; 
printf("Tapez le rang d’une journee entre 1 (dim) et 7 (sam) "); 
scanf("%d", &rang);
if rang < 1 ET rang > 7 then //then est faux
printf("Le rang de la journee est hors intervalles\n") ;
printf("On attend entre 1 (dimanche) et 7 (samedi)\n") ; //manque les accolades
else switch (rang) { case 1 || case 7 : printf("C’est la fin de semaine\n") ;  //manque {} au else, faire case 1 ou 7 est faux
case 2 à 4 : printf("Lu ou Ma ou Me\n") ; // le 2 a 4 marche pas
else : printf("Je ou Ve, la fin de semaine s’en vient!\n");
} 
```
Réécrivez le programme erroné en 3 blocs (3 parties), afin de corriger les erreurs commises :

résumé:
- il manque le int main()
- utilisation incorrecte du then
- il manque les accolades au premier if
- le switch est supposé être dans les accolades du else
- on ne peux pas faire case or case
- il manque les break
- pas de else pour le break, juste default

Code corrigé 

```C
#include <stdio.h>

//Celina Sid Abdelkader
//Aland Talib Ridha Barzani

//PETIT RESUME DES ERREURS DU CODE INITAL
/*
- il manque le int main(), et donc aussi le return 0 
- utilisation incorrecte du then
- erreur de logique, un chiffre n'est pas a la fois inferieur a 1 et superieur a 7 (OR REQUIS)
- il manque les accolades au premier if
- le switch etait supposé être dans les accolades du else
- on ne peux pas faire case or case, juste les faire succeder
- il manque les break
- pas de else pour le break d'un switch, juste default
*/
int main() {
    int rang; //jour quon traite
    char continuer; //char pour voir si on continue a traiter des cas
    int nbrCas = 0; // compteur de cas commence à 0

    do { //la boucle do while c'est pour traiter des cas tant qu'on entre O ou o
        
        printf("Tapez le rang d'une journee entre 1 (dimanche) et 7 (samedi) : ");
        scanf("%d", &rang);

        // Bloc 1 code fait avec des if et switch
        if (rang < 1 || rang > 7) { //on a corrigé le ET, c'est normalement && mais là c'est logiquement faux, on met un or
            printf("Le rang de la journee est hors intervalles\n");
            printf("On attend entre 1 (dimanche) et 7 (samedi)\n");
            nbrCas++; //on a traité un cas incorrect
        } else { //on a mit les accolades requises
            switch (rang) {
                case 1:
                case 7:
                    printf("C'est la fin de semaine\n");
                    break;
                case 2:
                case 3:
                case 4:
                    printf("Lu ou Ma ou Me\n"); //on a corrigé les successions de case
                    break;
                case 5:
                case 6:
                    printf("Je ou Ve, la fin de semaine s'en vient!\n");
                    break; //les breaks ont été mis
                default: // cas hors intervalles
                    printf("Le rang de la journee est hors intervalles\n");
                    printf("On attend entre 1 (dimanche) et 7 (samedi)\n");
                    break;
            }

            
            nbrCas++; // on a traite un cas correct
        }

        // Bloc 2 code fait juste avec des if 
        /*
        if (rang == 1 || rang == 7) {  //on verifie pour dimanche et samedi
    printf("C'est la fin de semaine\n");

		} else if (rang == 2 || rang == 3 || rang == 4) {  //pour lundi mardi mercredi
		    printf("Lu ou Ma ou Me\n");
		
		} else if (rang == 5 || rang == 6) {  // pour jeudi vendredi
		    printf("Je ou Ve, la fin de semaine s'en vient!\n");
		
		} else {  // là on verifie les cas hors intervalles
		    printf("Le rang de la journee est hors intervalles\n");
		    printf("On attend entre 1 (dimanche) et 7 (samedi)\n");
		}	
		
        // Bloc 3 code fait juste avec les switch
        
         switch (rang) {
            case 1:
            case 7:
                printf("C'est la fin de semaine\n");
                break;
            case 2:
            case 3:
            case 4:
                printf("Lu ou Ma ou Me\n");
                break;
            case 5:
            case 6:
                printf("Je ou Ve, la fin de semaine s'en vient!\n");
                break;
            default:  // cas hors intervalles
                printf("Le rang de la journee est hors intervalles\n");
                printf("On attend entre 1 (dimanche) et 7 (samedi)\n");
                break;
        }
        */

		/////////// VOIR SI LE USER VEUX CONTINUER DE TRAITER DES CAS  ///////////
		
        printf("\n continuer? (o/n) : ");
        scanf(" %c", &continuer);  

    } while (continuer == 'o' || continuer == 'O'); 

    // Afficher le nombre de cas traités, quils soient correct ou non
    printf("Nombre de cas traites : %d\n", nbrCas);

    return 0;
    
    /*TEST EXECUTION (CONSOLE)
    
		Tapez le rang d'une journee entre 1 (dimanche) et 7 (samedi) : 3
		Lu ou Ma ou Me
		
		 continuer? (o/n) : o
		Tapez le rang d'une journee entre 1 (dimanche) et 7 (samedi) : 12
		Le rang de la journee est hors intervalles
		On attend entre 1 (dimanche) et 7 (samedi)
		
		 continuer? (o/n) : o
		Tapez le rang d'une journee entre 1 (dimanche) et 7 (samedi) : 1
		C'est la fin de semaine
		
		 continuer? (o/n) : o
		Tapez le rang d'une journee entre 1 (dimanche) et 7 (samedi) : 7
		C'est la fin de semaine
		
		 continuer? (o/n) : o
		Tapez le rang d'une journee entre 1 (dimanche) et 7 (samedi) : 2
		Lu ou Ma ou Me
		
		 continuer? (o/n) : o
		Tapez le rang d'une journee entre 1 (dimanche) et 7 (samedi) : 5
		Je ou Ve, la fin de semaine s'en vient!
		
		 continuer? (o/n) : n
		Nombre de cas traites : 5
		
		--------------------------------
		Process exited after 21.26 seconds with return value 0
		Appuyez sur une touche pour continuer...
	
	*/
}


```
