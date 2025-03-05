
---
# Base 

Erreurs fréquemment commises sur les **identificateurs** :

- case sensitive
- `1ertp` Faux commence par un chiffre
- `tp#1` Faux “#” n’est ni une lettre, ni un chiffre
- `tp 1` Faux espace n’est ni une lettre, ni un chiffre
- variable en camelCase 
	- int salaire, boolean condition
- constante en UPPER_CASE
	- const int FACTEUR_CONV

**==Types de primitives==**

- int : Entier sur 32 bits (occupe 4 octets de mémoire)
- float : Réel sur 32 bits (occupe 8 octets de mémoire)
- char : Charactère ASCII
- boolean: vrai (ce qui n'est pas 0) ou faux (0)

>Respecter les priorités des opérations de gauche à droite, **toujours**

---
# Opérateurs logiques

`A && B` vaut vrai (1) <==> A et B sont “vrai simultanément”
`A || B` vaut vrai (1) <==> A ou B ou les deux sont “vrai”
`A == B` A vaut B ?
`A <= B` A inférieur ou égal à B?
 
---
# Affichage de données

```C
printf("format", liste d'informations à afficher);
printf("Le salaire est de %2.2f par heure", salaireHebdo)
```

<div style="page-break-after: always;"></div>

---
# Lecture de données

```C
scanf("codes format", liste des adresses des variables à lire);
scanf("%d%f", &age, &taille);

ex. Entrez l’age et la taille de la personne : 41 1.70
```

Il suffit de taper 2 valeurs séparées par au moins une espace suivie de la touche <Entrée>

---

==**Problème type**: Conversion de taille, entrer la taille en métrique et afficher le résultat en impérial==

1. **On fait quoi d'abord?**
*Découper le problème en 3 catégories*
- Quels sont les **données** et leur format?
	- Taille en pieds + pouces
	- Facteur de conversion (in -­­­­­> cm)
- Quelles formules utiliser?
	- ==*TailleImpériale = (**nbrPieds + nbrPouces**/12)*0.3048==
- Quels sont les **résultats** et leur format? 
	- Taille en centimètres
	- 
>==Attention==; toujours régler le problème jusqu'à la formule la plus **simple**/ **séries de formules successives** les plus simples

3. **Comment choisir le bon format de données?**
*Ca va dépendre de la nature de la donnée: variable qui peut être décimale, entière, un texte, un charactère etc...*
 - *TailleImpériale (float) = (**nbrPieds (int) + nbrPouces (int)**/12)*0.3048 (constant)
fin de la pseudo réflexion

<div style="page-break-after: always;"></div>

---
#TP_exemple_code_c

```C
#include <stdio.h> // pour avoir le scanf

int main(void)
{
	//Declaration donnees
	const float facteur = 0.3048;
	int nbrPieds, nbrPouces;
	float taille; 
		//Obtention des donnees (user input)
		printf("Entrez la taille en pieds et pouces");
		scanf("%d%d", &nbrPieds, &nbrPouces);
		//Formule
		taille = (nbrPieds + nbrPouces/12)*facteur
		printf("%d pieds %d pouces: %d cm", nbrPieds ,nbrPouces, taille)
	 return 0
}
```

petits tricks:

>%3d : Entier sur **3 digit**
>%6.2f : Réel avec **6 décimales** et **2 chiffres** après la virgule
>%c : Caractère **ASCII** OU ==getchar()==
>/t: **tabulation**, très bel espace 

==ULTRA MEGA IMPORTANT:==
==***& = REF ADDRESSE, JUSTE POUR SCAN***==

---

#TP_exercice_calcul_taxes_remise

```plaintext
Tapez le prix de l'article 2.78
TPS       0.14
TVQ       0.22
Prix avec taxes 3.14
Quel est le montant donne par le client ? 10.25
Montant remis parle client : 10.25
Monnaie a remettre : 7.11 $
Appuyez sur une touche pour continuer...
```

<div style="page-break-after: always;"></div>

**Input et prompt**
>printf("Tapez le prix de l'article")
>scanf("%.2f", &prix)

**Constantes**
>const TPS = 0.05
  const TPS =0.075

**Variables**
>tps = TPS(prix)
>tvq = TVQ (tps + prix)
>prixAvecTaxes = prix + tps + tvq

**Affichage**
>printf("TPS %.2f", &tps)
>printf("TVQ %.2f", &tvq)
>printf("Prix avec taxes %.2f $", &prixAvecTaxes)

****Partie 2****
**Input/prompt**
>scanf("Montant remis par le client : %.2f $", &montantRemis)

**Variables**:
>monnaie = montantRemis - prixAvecTaxes

**Affichage**
>printf("Monnaie remise : %.2f $", &monnaie)

<div style="page-break-after: always;"></div>

---
#exemple_taxes
```C
#include <stdio.h>
int main(void)
{
	//Declaration donnees
	const float TPS = 0.05;
	const float TVQ = 0.075;
	int tps,tvq,prixAvecTaxes,montantRemis,monnaie; 
	
	//prompt (user input)
	printf("Tapez le prix de l'article")
	scanf("%.2f", &prix)
		
	//variables part 1
	tps = TPS * (prix)
	tvq = TVQ * (tps + prix)
	prixAvecTaxes = prix + tps + tvq

	//Premier Affichage
	printf("TPS %.2f", tps)
	printf("TVQ %.2f", tvq)
	printf("Prix avec taxes %.2f $", prixAvecTaxes)

	//prompt
	scanf("Montant remis par le client : %.2f $", &montantRemis)

	//variables part 2
	monnaie = montantRemis - prixAvecTaxes
	
	//Affichage
	printf("Monnaie remise : %.2f $", monnaie)

	return 0 //execution normale, code exit
}
```

<div style="page-break-after: always;"></div>

---
**==Déclaration externe des variables==**

Il est possible de **déclarer** des constantes (aucune modification) en **dehors du main**

```C
#include <stdio.h> 

#define TPS = 0.05
#define age = 22

etc...
int main(void)
{...}
```

---

## **==Types de conditionnelles==**

il est possible de vérifier des conditions avec `ìf {...} elif {...} else` et avec le `switch case  {...} default`

### If - else
```C
if (genre == 'F' || genre == 'f'){ //si 'F' or 'f'
    printf("C'est une femme");
    nbFemmes = nbFemmes + 1 ;
} else {
    printf("C'est un homme");
    nbHommes = nbHommes + 1;
}
```

---
<div style="page-break-after: always;"></div>
### Switch - case

```C
# include <stdio.h>
# include <ctype.h> /* pour traiter les roles en char majuscule */

#define BONUS_A  500.00  /* bonus pour les analystes     */
#define BONUS_O 400.00  /* bonus pour les programmeurs  */
#define BONUS_P 400.00  /* bonus pour les operateurs  */    
#define BONUS_C  375.00  /* bonus pour les camionneurs   */
#etc...

printf("Entrez le poste et le salaire hebdomadaire : ");
scanf ("%c%f", &poste, &salHebdo);
poste = toupper(poste);
bonus= 0;
printf("Vous etes un ");

switch (poste){
case 'P': printf("Programmeur");
	bonus = BONUS_P;
	break;
case 'O': printf("Operateur");
	bonus = BONUS_O;
	break;
case 'C': printf("Camionneur");
	bonus = BONUS_C;
	break;
case 'R': 
case 'M': printf("Inutiles à la société");
	bonus = -400;
	break;

default: printf("Client");
}
printf(" vous aurez un bonus de %6.2f et un salaire de %6d" , bonus, salHebdo)
```

>==Notes:== on peut éviter de **répéter** les clauses (voir cas R et M) mais avec switch-case¸ ça ne marche qu'avec des cas de **char** et des **entiers**

<div style="page-break-after: always;"></div>

---
# Boucles de répétition


### While

while (**condition à vérifier**){
	*trucs à faire*
	changement d'un élément de la condition pour break
}

```C

#include <stdio.h>
void main()
{
   const int BORNE = 10;
   int n, nbFois = 0;

   FILE * aLire;  /* déclaration du fichier */

   /* Ouvrir le fichier en mode de lecture: "r" (de "reading") pour lire */
   aLire = fopen("entiers.dta", "r");

   printf("Les entiers lus dans le fichier :\n\n");

   /* La lecture, ligne par ligne  */
   while (!feof(aLire)){            /* Tant que pas fin du fichier */
      fscanf(aLire, "%d\n", &n);    //on lit un entier par ligne
      printf("%3d\n", n);

      if (n > BORNE)
         nbFois++;
   }
   /* Fermeture du fichier (fclose) */
   fclose(aLire);

   printf("Le nombre d'entiers supérieurs à %d est : %d\n", BORNE, nbFois);
}

```

>Note: 
>Si l'ouverture du fichier réussit, `aLire` devient un pointeur vers ce fichier. Si le fichier ne peut pas être ouvert, `fopen()` renverra `NULL`.

---
### Do While

```C
const int MAXI_AGE = 134;
int   age, valide; /* Oui ou Non la donnée est valide */

char  sexe;

/* saisir et valider le sexe */
do {
   printf("Entrez un caractere parmi f, F, m ou M :");
   scanf(" %c", &sexe);

   sexe = toupper(sexe);

   valide = (sexe == 'F' || sexe == 'M');

   if (!valide)     /* Si Pas valide  */
      printf("Erreur! Retapez S.V.P. \n");
} while (!valide);  /* tant que non valide */

/* saisir et valider l'âge */
do {
   printf("Entrez l'âge entre 1 et %d : ", MAXI_AGE);
   scanf("%d", &age);

   valide = (age >= 1 && age <= MAXI_AGE);

   if (!valide)
      printf("Erreur! Retapez S.V.P. \n");
} while (!valide);
```

---
### For

for (**init itérateur;  condition;  modification itérateur**){
	*trucs à faire*
}

````C
void main()
{
   int ligne, colonne;

   for (ligne = 1; ligne <= 5; ligne++){
      for (colonne = ligne; colonne <= 5; colonne++){
         printf("%d", colonne);
         printf("\n");
	    }
   }
   
````

### Statistiques

```C
/* Fichier Compteur1.C (introduction à la notion de compteur)
   Ce programme permet de saisir l’âge d’une personne tant que
   l’usager décide de continuer. On compte et affiche :
      - le nombre total de personnes traitées
      - le nombre total d’adultes traités
 */

#include <stdio.h>
#include <ctype.h>


int main()
{
  int age;
  char reponse;
  int  nbPers = 0, // le nombre total de personnes traitées 
       nbAdul = 0; /* le nombre total d'adultes traités */
       
  do { /* répéter la saisie */
  
     printf("Entrez l'age de la personne ");
     scanf("%d", &age);
     nbPers++; /* une personne de plus à traiter */
     
     if (age >= 18)
           nbAdul++; // un adulte de plus 
           
    printf("\nVoulez-vous continuer ? (o/n) ");
    scanf(" %c", &reponse);
     
  } while ( toupper(reponse) == 'O');
  printf("\n\n");
  printf("Le nombre total de personnes traitees : %d\n", nbPers);
  printf("Le nombre total d'adultes traites     : %d\n", nbAdul);
  
  return 0;
}
```

---

#### JAVA

"**TOUT EST UN OBJET**"

Personne = caractéristiques, des traits, des attributs, fait des actions
Fonction = paramètres, conditions etc.

Math calcul = new Math()



Math monchiffre = new Math(100

monchiffre.sqrt() ON FAIS PAS
Math.sqrt(100) ON LE FAIT

.afficher()
.direTonNom()
A={1,3,5,6,7}
B={1,4,5,9}

public class Ensemble(int[] nombres)

Ensemble A = new Ensemble ({1,3,5,6,7})
Ensemble B = new Ensemble ({1,4,5,9})

// Ensemble. intersection(A,B) //statique  -> appelle sur la Classe (param = Objets concernés)
// A. intersection(4)       //orienté-objet -> appelle sur l'Objet (param = l'autre objet OU des attributs)

POO = But est d'utiliser des Objets 

choix 1    choix 2
POO        Procédural
ici            ici
    | |
    | |

---
def calculer_perimetre(x):
	return 2 * pi * x

calculer_perimetre(45)     
calculer_perimetre(34)
calculer_perimetre(578)   

---

public calculerPerimetre(){
	return  this.rayon * 2 * pi* 
}


public Cercle(int e){ //constructeur
	this.rayon = e
}

Cercle moncercle = new Cercle(45) //instanciation de l'objet
rayon de moncercle = 45


Cercle moncercle2 = new Cercle(22)
rayon de moncercle2 = 22

---

public class Triangle{
	//je veux savoir ce qu'est un triangle...

return this . triangle;


}


---
Final

une variable qui ne peut pas être modifiée dans le code :

```java
for (int i = 0; i<5;i++){  
    pi = pi+1;  
    System.out.println(pi);  
}
```