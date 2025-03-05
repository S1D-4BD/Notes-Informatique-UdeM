
###

```C
float prixAPayer(float prix)
{
   /* déclarations locales :  */
   const float TAUX_TPS = 0.06,
               TAUX_TVQ = 0.075;
   float tps, tvq;

   /* calcul du prix total à payer : prix + les 2 taxes */
   tps = prix * TAUX_TPS;
   tvq = (prix+TPS) * TAUX_TVQ;
   return prix + tps + tvq;
}
```
### **Structure de base d’un programme Java**

```java
public class Main {
    public static void main(String[] args) {
        // Votre code ici
        System.out.println("Bonjour, Java !");
    }
}
```
---
### **Types de données**

| Type      | Taille  | Exemple                    |
| --------- | ------- | -------------------------- |
| `int`     | 32 bits | `int x = 42;`              |
| `double`  | 64 bits | `double y = 3.14;`         |
| `float`   | 32 bits | `float z = 3.14f;`         |
| `char`    | 16 bits | `char lettre = 'A';`       |
| `boolean` | 1 bit   | `boolean actif = true;`    |
| `long`    | 32 bits | `long grand = 123456789L;` |
| `short`   | 16 bits | `short petit = 100;`       |
| `byte`    | 8 bit   | `byte b = 127;`            |
| `String`  | Classe  | `String texte = "Salut";`  |

---
<div style="_page-break_-after: always;"></div>

<div style="page-break-after: always;"></div>


### **DÉclarer Variables**

```java
final int
final double racineDeDeux = 1.414 //la racine de 2 est 1.414 ... ne dois pas changer
int x = 8;                  //declaration simple
int a = 5, b = 10, c = 15;  //declaration de plusieurs

//blablabla
int x = 37  //autorisé
int x = 7.9 //pas bon, car pas le meme type

racineDeDeux= 6 //INTERDIT !!! FINAL = CHANGE PAS
```



---
### **opéreurs**

| Catégorie     | Opérateurs                       | Exemple            |
| ------------- | -------------------------------- | ------------------ |
| Arithmétiques | `+`, `-`, `*`, `/`, `%`          | `int res = 5 + 3;` |
| Relationnels  | `==`, `!=`, `<`, `>`, `<=`, `>=` | `x > y`            |
| Logiques      | `&&`, `                          |                    |
| Affectation   | `=`, `+=`, `-=`, `*=`            | `x += 2;`          |

### Priorité des opérateurs:

| **priorit.** | **Type d'Opérateurs**      | **Opérateurs**                    |
| ------------ | -------------------------- | --------------------------------- |
| 1            | Multiplication et Division | `*`, `/`, `%`                     |
| 2            | Addition et Soustraction   | `+`, `-`                          |
| 3            | Supériotité                | <, >, <=, >=                      |
| 4            | Égalité                    | `==`, `!=`                        |
| 5            | AND logique                | &&                                |
| 6            | OR logique                 | \| \|                             |
| 7            | Ternaire                   | `? :`                             |
| 8            | Affectation                | `=`, `+=`, `-=`, `*=`, `/=`, `%=` |

<div style="page-break-after: always;"></div>


Exemple 

```java
int a = 5, b = 10, c = 2; 
boolean result = a + b > c * 5 && b / c == 5 || a % c == 1; //tres mechant
-----------------------------------------------------------
1:    (a + b) > (c * 5) &&   (b / c) == 5 ||  (a % c) == 1;
      (15)    >   (10)  &&       (5) == 5 ||      (1) == 1;
   
2:  ((a + b) > (c * 5)) && ((b / c) == 5) || ((a % c) == 1);
	      (true)        &&       (true)   ||      (true);
	      
3:(((a + b) > (c * 5))) && ((b / c) == 5) || ((a % c) == 1);
	                           (true)     ||    (true); donc result =true
```
---

###  Cast explicite (conversion des types)**

Tu fais ca lorsqu'on passe d'un type **plus grand ou plus précis** vers un type **plus petit ou moins précis**.
- Exemple : `double` (64) ou `float` (64) vers `int` (32),  ou
- `long` (32) vers `short` (16)

```java
double a = 3.14; int b = (int) a; // Affiche  3
```


---
## **Scanner**

```JAVA

import java.util.Scanner; 
public class Main { 
	public static void main(String[] args) { 
		Scanner scanner = new Scanner(System.in); 
		System.out.print("Entrez votre nom : "); 
		String nom = scanner.nextLine(); 
		System.out.println("Bonjour, " + nom + " !"); 
		} }
```

## Formatter affichage 

```java
System.out.printf("Bonjour %s, vous avez %d ans.\n", "Alice", 25);
//%s =string %d = nbr
```
---

<div style="page-break-after: always;"></div>


### **Conditions**

- if / else :

    ```java
    if (age >= 18) {     
	    System.out.println("Adulte"); } 
	else {
		System.out.println("Mineur"); 
	}```
    
- switch :
    
```java
switch (jour) {
    case 1: System.out.println("Lundi"); 
	    break;
    case 2: System.out.println("Mardi"); 
	    break;
    default: System.out.println("Inconnu");
	    break;
}
```

---
### **boucles**

- **Boucle `for`** :
```java
for (int i = 0; i < 5; i++) { //init. (=) i à 0; condition pour rester; changement
    System.out.println("i = " + i); //ce qu'on fait 
}

```

 - **Boucle `while`** :

```java
int i = 0; //ATTENTION ; INIT i EN DEHORS DU WHILE (SINON BOUCLE INFINIE)
while (i < 5) { //SEULEMENT LA CONDITION
    System.out.println("i = " + i);
    i++; //ICI LE CHANGEMENT
}
```

- **Boucle `do-while`** :

```java
int i = 0;
do {
    System.out.println("i = " + i);
    i++;
} while (i < 5);

```
 ---

<div style="page-break-after: always;"></div>


### **Tableaux** 

==DES QUE TU CREE UN TABLEAU, SA TAILLE NE CHANGE PAS==

>**Pour les array ( int[], String[], double[]) add, remove, pop ca n'existe pas**

```Java
//CREER UN ARRAY EN JAVA (TABLEAU [])
//type = primitif ou objet c'est correct
//2 facon d'en créer une : 
int[] nomTableau = {1,2,4,35,67}; // 1) je cite la liste au complet
// [1,2,4,35,67]
String[] nomPays = {"Canada","Algerie"}; // 1) je cite la liste au complet

int[] nomTableau = new int[5]; //2) cite la taille (mais elle est vide au debut)
// [null,null,null,null,null] 
-----------------------------------------------------
//ex. {1,2,4,35,67}
nomTableau[3] = 35    //remplacement d'un element (je met 35 dans [3])
int x = nomTableau[0] //recupere un element (je met [0] dans variable)

nomTableau.length() = 5 //ATTENTION PYTHON C'EST .len
-----------------------------------------------------
//STRING = TABLEAU DE CHAR
String nom = "Salut" 
			=> ['S','a','l','u','t']

nom.charAt(0) = 'S' //c'est utile a savoir
```

### **Listes**

==LISTE = TAILLE DYNAMIQUE==

```JAVA
//structure générale
//type = primitif ou objet c'est correct
//List<type> nomListe = new ArrayList<type>() // A RETENIR

1) List<int> nbr = new ArrayList<int>();                         //TYPE = primitif
2) List<String> pays = new ArrayList<String>();                  //TYPE = Objet
3) List<Calculatrice> listeCalc = new ArrayList<Calculatrice>(); //TYPE = Objet

nbr.add(3) 
//[3]
nbr.add(5)
//[3,5]
nbr.size() //ATTENTION CE N'EST PAS .LENGTH()
//2
nbr.add(4)
//[3,5,4]
nbr.indexOf(5) //element
//index 1
nbr.remove(0)
//[5,4]
nbr.set(1)= 12
//[5,12]

```

---

<div style="page-break-after: always;"></div>


### **Méthodes static** 

``
```java
public class Calculatrice {

    // Méthode statique
    public static int addition(int a, int b) { //public int = retour c'est un int
        int c = a + b //type = int
        return c; 
    //PAS DE CONSTRUCTEUR !! CAR ON A PAS BESOIN D'OBJET
    }
}
```

```JAVA
public class Main {
    public static void main(String[] args) {        //méhode de démarrage
        // Appel direct de la méthode statique via le nom de la classe
        int resultat = Calculatrice.addition(3, 5); //J'UTILISE LA CLASSE
        System.out.println("Résultat (static) : " + resultat); // Affiche : 8
		
		//Ce qui n'est pas fait!!!//
		/*Calculatrice casio = new Calculatrice(param) 
		casio.addition(3, 5) PAS STATIC CAR ON UTILISE UN OBJET -> NON-STATIQUE */
    }
}
```

JE N'AI PAS EU BESOIN D'APPELLR  NEW CALCULATRICE( ) POUR UTILISER LA MÉTHODE ; ==TU UTILISE LA CLASSE ELLE-MÊME==

---
### **11. Constructeurs + programmation orientée objet**

```java
public class Personne {
    String nom; //ATTRIBUT

    // Constructeur car on CREE DES OBJETS
    public Personne(String nom) { // /!\ METTRE TYPE
        this.nom = nom; //ASSOCIATION:  ATTRIBUT <= PARAMETRE
    }

    public void saluer() { //methode pour print attribut nom, RETOURNE RIEN
        System.out.println("Bonjour, " + this.nom + " !"); 
        /* this.nom = attribut de l'objet en question
    }
}
```

```java
public class Main {
    public static void main(String[] args) {

    Personne obj1 = new Personne("Bob")    // obj1.saluer() ->  "Bonjour, Bob !"
    Personne obj2 = new Personne("Alice")  //  obj2.saluer() ->  "Bonjour, Alice !"
        //Je n'écris pas return 
    }
```

---

<div style="page-break-after: always;"></div>



```java
public class Livre {
	private String titre, auteur;   //attribut
	private Boolean disponible = false; //attribut
	
	public Livre(String t, String a, Boolean d) {
		this.titre = t;    //le tire d'un livre = param t
		this.auteur = a;   //auteur d'un livre = param a
		this.disponible = d; //la dispo d'un livre = param d
	}
	
	public String toString() {
		String dispo = (this.disponible)?"disponible":"non disponible"; 
		//est ce que dispo = true? si OUI, String dispo =  "disponible"
		//                         si NON, String dispo =  "non disponible"
		return "Titre : " + this.titre + "\n Auteur : " + this.auteur
				+ "\n est " + dispo;
	}
	
	public String getTitre() {
		return this.titre; //te donne le titre de l'objet
	}
	
	public Boolean getDispo() {
		return this.disponible; //te donne le booleen disponibilite de l'objet
	}
	
	public Boolean setDispo(Boolean b) {
		if(this.disponible == b)
			return false; //change le booleen par le param b
		else {
			this.disponible = b;
			return true;
		}	
	}
}

```

<div style="page-break-after: always;"></div>


```java
import java.util.*; // Importe les classes nécessaires pour utiliser les collections, comme List

// Classe représentant une bibliothèque
public class Biblio {
    private List<Livre> livres; // Une liste d'objets de type Livre 

    // Constructeur : init la bibliothèque avec une liste de livres donnée (l)
    public Biblio(List<Livre> l) {
        this.livres = l; // La liste de livres est passée en param
    }

    // Méthode pour afficher tous les livres de la bibliothèque
    public void afficherLivres() {
        // Parcourt la liste de livres et affiche chaque livre
        for (int i = 0; i < this.livres.size(); i++) {
            System.out.println(livres.get(i)); // Affiche le livre à l'index i
        }
    }

    // Méthode pour emprunter un livre en fonction de son titre
    public Boolean emprunterLivre(String t) {
        // Parcourt tous les livres pour
        // trouver celui qui correspond au titre donné
        for (int i = 0; i < this.livres.size(); i++) {
            if (this.livres.get(i).getTitre() == t) { 
            // Vérifie si le titre correspond
                if (this.livres.get(i).getDispo()) { 
                // Vérifie si le livre est disponible
                    return this.livres.get(i).setDispo(false); 
                    // Marque le livre comme emprunté
                }
            }
        }
        return false; // Retourne false si le livre n'a pas pu être emprunté
    }

    // Méthode pour retourner un livre emprunté, basé sur son titre
    public Boolean retournerLivre(String t) {
        // Parcourt tous les livres pour 
        // trouver celui qui correspond au titre donné
        for (int i = 0; i < this.livres.size(); i++) {
            if (this.livres.get(i).getTitre() == t) { 
            // Vérifie si le titre correspond
                if (!this.livres.get(i).getDispo()) { 
                // Vérifie si le livre est emprunté
                    return this.livres.get(i).setDispo(true); 
                    // Marque le livre comme disponible
                }
            }
        }
        return false; // Retourne false si le livre n'a pas pu être retourné
    }
}

```

<div style="page-break-after: always;"></div>


```java
import java.util.*;

public class UseBiblio {
	public static void main(String[] args) {
		Livre l1 = new Livre("Harry Potter à l'école des sorciers", "J.K. Rowling", true);
		Livre l2 = new Livre("Le Seigneur des anneaux", "J.R.R. Tolkien", false);
		Livre l3 = new Livre("1984", "George Orwell", true);
		Livre l4 = new Livre("Orgueil et préjugés", "Jane Austen", false);
		Livre l5 = new Livre("L'Alchimiste", "Paulo Coelho", false);
		Livre l6 = new Livre("Le Petit Prince", "Antoine de Saint-Exupéry", true);
		
		List<Livre> listeLivre = new ArrayList<Livre>();
		listeLivre.add(l1); //ajout
		listeLivre.add(l2);
		listeLivre.add(l3);
		listeLivre.add(l4);
		listeLivre.add(l5);
		listeLivre.add(l6);
		
		Biblio bib = new Biblio(listeLivre);
		
		bib.afficherLivres();
		System.out.println("#########################################");
		bib.emprunterLivre("1984");
		bib.afficherLivres();
		System.out.println("#########################################");
		bib.retournerLivre("1984");
		bib.afficherLivres();
	}
}
```