[[examen_ift1025_pratique02.pdf]]
---
# Introduction Java

==**Différences entre Java et Python**==

- Java est interprété et **compilé**, Python est **interprété**
- Typage **statique** pour Java, **dynamique** pour Python
- Java est axé **OO**, Python est procédural
- Utilisation **globale** pour Java, spécifique pour Python
- Python dépend de **librairies** 3rd-party, pas Java
- On doit spécifier le **type** en Java, et une fois fait **on ne peux qu'assigner ce type** de variable spécifiquement
­­
>Si je **change** une constante en Java, je dois **recompiler** via  *javac* puisque le byte code n'est pas modifié

**==Problème type: Un document Java simple==**

- Nommer le fichier .java avec le **même** nom que la classe qui y est codé dedans
- **Toujours** inclure la méthode main:
```java
public static void main(String[] args){
//code
}
```

- Fichier type: classe qui y est codé avec la méthode main **imbriquée** dedans

```java
public class maClasse { 
	//c'est le nom du fichier .java 
	public static void main(String[] args){
	//code
	}
}
```

**==Types de primitives==**

- long : Entier sur 64 bits
- double : Réel sur 64 bits
- int : Entier sur 32 bits
- float : Réel sur 32 bits
- char : Charactère ASCII
- short: Entier sur 16 bits
- byte : Entier sur 8 bits

>Attention, un **char** est écrit avec **'x'**, 
>mais un **String** est écrit avec **"x"**

**==Casting==**

>il existe 2 type de casting: vers le plus grand et vers le plus petit. Le premier est naturel pour Java (ex. 32 bits vers 64)

Wide Cast ==(Naturel)== :  
`byte` -> `short` -> `char` -> `int` -> `long` -> `float` -> `double '(le plus important)'`

Force Cast:
`double` -> `float` -> `long` -> `int` -> `char` -> `short` -> `byte (le plus forcee)`

---
**==Norme IEEE-754==**

>Norme de stockage et **écriture** des nombre flottants/*réels* **binaires**

#exemple_ieee-754

1) On met en binaire la partie **entière**
	- -45.625 : 45 en binaire =101101
2) On met en binaire la partie **fractionnaire**
	 - 0.625 : 0.101
3) Écrire le nombre au complet
	 - 101101.101
4) Déplacer la virgule ver le bit le plus **significatif**, compter les bonds (c'est l'exposant)
	- 101101.101 devient 1.01101101 (**exposant** = 5)
	- 01101101 est la **mantisse**
1) Ajouter l'exposant a 127 (car c'est la norme)
	- 5+127 = 132
2) Mettre 1 si le nombre est négatif

==GROSSOMODO: -45.625==

>1) Signe = 1 (négatif)
>2) exposant = 10000001
>3) mantisse = 011011010000000000000000000 
>**norme IEEE-754**:  11000000101101101000000000000000 ...

---
Exemple d'initialisation

```java
int age = 22
float solde = 20.5f
long soldeMusk = 9999999L
bool depression = true

```


**==C'est quoi static?==**
Static est le paradigme de programmation ou un attribut n'est pas propre à un objet ou qu'on ne **requiert** pas un objet pour utiliser les méthodes d'une classe


> [!NOTE] Note
> On n'instancie **pas** un objet de la classe **Math** pour utiliser la méthode add()


```java
public class Etudiant{
	private int age;
	private String name;
	private static int matricule = 0;

public Etudiant(age,name){
	this.age = age;
	this.name;
	this.matricule = Etudiant.matricule;
	Etudiant.matricule++;
	}
}
```
---
# Programmation Orientée Objet

==**Comment faire une classe avec constructeur?**==

>Le OOP permet d'instancier des **objets** ayant des **attributs d'instance** (qu'on différencie des autres objets de la même **classe**), des **attributs de classe** (que **tous** les objets partageront) et des **méthodes** propres a cette classe (des **actions**).  On vérifie si un objet est une instance de la classe via instanceOf.

On *crée* le **constructeur** en faisant:
- accesseur ==`public`==
- nom de la classe ==`Cat`==
- on suit classe des paramètres ==`(type arg1 type arg2...)`==
- On écrit les accolades =={}== et on écrit entre elles:
	- la référence directe (a l'objet)  ==`this.attribute = arg`==  pour associer a l'attribut de l'objet en question un des ==paramètres== 
	- d'autres méthodes qui doivent être exécutées si nécessaire ==des l'instanciation== de l'objet

>Note: les attributs sont définis **EN DEHORS** du constructeur

```Java
public class Cat
{
	//constructeur a 2 parametres (methode)
	public Cat(String name, int age) 
	{
		this.nameCat=name; //nameCat = le parametre name
		this.ageCat=age; // pour personaliser l objet
		System.out.println("Je suis ici :"+ this);
		//print la zone memoire de l objet (stack)
		System.out.println("Je suis " +this.nameCat)l
		//print la valeur de l attribut nameCat
	}
	//attributs
	private int ageCat;
	private String nameCat;
}
```

et maintenant le programme principal: 

```Java
public static void main (String[] args)
{
	Cat miaou = new Cat("Chtou", 7);
	Cat miaou2 = new Cat("Izane", 9);
	//un remet je suis un chat :0x6679
	//puis son nom
	//autre remet je suis un chat :0x9879
	//puis son nom
}
```

==**Comment créer une méthode?**==

Une méthode de classe est un bloc de code qui est exécuté dès l'appel

>Note: pour créer une méthode de classe, il faut la déclarer en **dehors** du main

```java
public class Compte{

private String account_holder;
private int balance;
private int score_credit;

	public Compte(String account_holder,int balance; int score_credit){
	this.account_holder=account_holder;
	this.balance=balance;
	this.score_credit=score_credit;
	}
    public int add(int x){ //2 int en param, retourne 1 int
        balance +=x;
        return balance; 
    }

    public int sub(int){
        balance -=x;
        return balance; 
    }

    public static void main(String[] args){
        Compte compte1 = new Compte("H",450,700);
        System.out.println(compte1.add(35));
        System.out.println(quiz.sub(15));
    }
}

```


Exemple d'une classe avec un ==attribut **statique**==

```Java
public class Etudiant {

public static int nextMatricule = 0; 
/*Cet attribut est partagé par tous les objets, 
peut importe comment il est construit
*/
public int matricule;      // matricule d'un étudiant 
public String prenom, nom; // prénom et nom d'un étudiant 


//Constructeur 
public Etudiant( String prenom, String nom ) { 
	this.prenom = prenom; 
	this.nom = nom; 
	this.matricule = Etudiant.nextMatricule; //met direct l'attribut de la classe Etudiant
	Etudiant.nextMatricule++; 
	/*des que la methode constructeur fini
	on incremente attribut prochainMatricule pour ne pas
	avoir a gerer manuellement les matricules (0,1,2,3...)
	*/
	} 
}
```

---
**==Getter==**

```Java
(...)
public int getMatricule(){
return this.matricule;
}
```
---
**==Setter==**

```java

(...)
public void setMatricule(int x){
	if (x<0){
		System.out.println("Matricule invalide"); //validation
	}
	else{
		this.matricule = x;
		return matricule;
	}
}

```


> [!NOTE] Note
> Les getters et surtout les setters permettent de **contrôler** la modification d'attributs propres à une classe en offrant la possibilité de faire une **validation** avant tout retour de données, ou même de vérifier une condition **user.hasAccess**.

---
### Tableaux

**==Comment créer un tableau et l'update (ex. ajouter des éléments, changer la longueur)==**

```java

import java.util.Scanner;
public class Liste{

	private int[] elements;
	private int longueur;
	
	//CONSTRUCTEUR, on crée un objet avec longueur de e elements
	public Liste(int e){
		this.longueur = e;
		this.elements = new int[e]; //super important le new int[]
	}
	
	//Getter pour récuperer la longueur d'un certain objet
	public int getLongueur(){
		return this.longueur;
	}
	
	//on add un int e à un index n de l'objet
	public void add(int e,int n){
	if (n>=0 && n< this.elements.length){
		this.elements[n] = e;
		}
	else{
		System.out.println("pas bon");
		}	
	}
	// On lit un input int "s", on itère tout les elements de l'objet
	// en dessous de la longueur. À chq itération on appelle add()
	// à l'index de l'itérateur. On retourne un objet Liste updated
	
	public void afficherTab(){
	int condition = this.getLongueur();
	for (int i = 0; i < condition; i++){
			System.out.println("Elements à index "+i +" "+ this.elements[i]);
		}
	}
	public Liste remplirTab() { 
	int condition = this.getLongueur(); 
	Scanner s = new Scanner(System.in); 
	for (int i = 0; i < condition; i++) {
		System.out.println("Entrez un entier pour l'index " + i + " :"); 
		this.add(s.nextInt(), i); 
		}
		return this;
	}
	//ajouter methodes removeElementAt() et pop()
}
```


---
# Modèle mémoire 

Le modèle mémoire de java consiste d'un **stack**, un **heap** et un data **segment**

Le stack est alloué de façon automatique par le **compilateur** et va contenir tout les pointeurs de fonctions (lorsqu'on entre dans une fonction, on exécute la fonction et puis on **jump à l'adresse stockée au stack** pour retourner au programme **principal**), les primitives etc. Il grossit du haut de la mémoire **vers le bas**.

dès qu'une fonction n'est plus utilisée, elle est supprimée de la pile en **FILO**

Le heap est **dynamique** dans le sens qu'on ajoute manuellement des éléments à cette mémoire après la compilation (dès qu'on **crée** un objet avec `new` dans le main **après** compilation) et peut être **imprévisible** (créer un array de 100 items est assez imprévisible pour le compilateur s'il sait juste qu'on peut créer un tableau de *Personnes* sans connaître le nombre exact d'éléments dedans). Il grossit du bas de la mémoire **vers le haut.**

Ex: Dans le stack, je vais avoir une **assiette** pour la fonction main qui demande de retourner un b (mais pas calculé encore), je crée une **autre** assiette pour la fonction *multiplier* qui elle va me **retourner un nombre pour b**, je retourne à l'adresse d'appel (je retire l'assiette multiplier, je vois **automatiquement** l'assiette main, et je transverse b à la fonction main (assiette complètement en bas)

si j'avais un objet, les infos de l'objet sont stockées dans le heap, don dans le stack j'aurais une assiette vide sauf pour un **post-it** qui indique ou est le contenu (le heap)

le data segment contient tout les trucs static, ce que je dois jamais perdre ni effacer par le garbage collector.

>Si j'assigne un espace mémoire (stack) qui fais une référence a un objet de type Avion, mais que je n'ai pas fait new, alors je reçois un ==null pointer== car dans le Heap, il n'y a aucune valeur concrète

---
# Héritage

Une classe mère **abstraite** ne peut pas être instanciée directement mais transmet ses attributs et méthodes aux sous-classes **spécialisées**. Elles pourront alors créer des objets concrets en héritant de ses fonctionnalités.

>[!NOTE] Note
>les méthodes qui doivent être **redéfinies** par les sous classes doivent avoir le modificateur **abstract** (public *abstract* …), dans le code de la sous-classes *@Override* doit être écrit **avant chaque méthode abstraite** pour les redéfinir, et pour accéder à une méthode **non abstraite** de la classe mère il faut **créer une nouvelle méthode** pour la sous-classe qui **elle** va appeler la méthode non abstraite via le modificateur **super**


```java 
public abstract class Human {

    String nom;
    int age;
    String genre;

    public Human (String nom,int age,String genre){
        this.nom = nom;
        this.age = age;
        this.genre = genre;
    }
    public void manger(){
        System.out.println("Je mange");
    }
    public abstract void dormir();
}
```

==sous-classe qui hérite :==

```java
public class Student extends Human {
    String university; //attribut propre à un Student
    
    public Student(String nom,int age,String genre, String university){
        super(nom,age,genre);
        this.university = university;
    }
    public void mangerRepas(){
	    super.manger();
    }
    @Override
    public void dormir(){
        System.out.println("0 sleep");
    }
}

```


>**==ATTENTION==**: Si j'instancie un objet de la classe mère avec le constructeur d'une sous classe, je peux seulement utiliser les  méthodes publiques de la classe mère, il faut transtyper pour utiliser les sous méthodes

```java
Question q = new Question(a,b,c);
Universitaire u = new Etudiant(nom);

q.saluer(u); // salutations de Universitaire
q.saluer((Etudiant) u) // salutation de Etudiant
```

> [!NOTE] Note
> On peut faire une classe **abstraite** qui fera hériter son contenu à des sous classes **dans des cas où il est illogique d'instancier la classe abstraite elle-même** (bizarre d'instancier une **machine**, mais pas si bizarre d'instancier une imprimante, un ordinateur, un bras mécanique etc). On peut faire aussi avec une classe régulière, mais il faut que la sous-classe soit considérée comme une "**spécialisation**" de la classe mère.

---
# Polymorphisme

Le polymorphisme est la capacité à une méthode d'être utilisée différemment dépendamment de l'objet/paramètres présents utilisés.

>[!NOTE] Note
>Le polymorphisme à la compilation permet de coder **2 méthodes ayant le même nom** mais pas les mêmes paramètres et de savoir, en **fonction des paramètres** laquelle utiliser.
>
>Le polymorphisme à l'exécution permet de **redéfinir** une méthode **abstraite** héritée d'une classe mère avec *@Override*

### Tableau de objets différents

Il suffit de faire des sous-classes d'une même classe abstraite, ils hériterons de ce qu'il faut, et le tableau sera une liste d'objets du même type que la classe abstraite

```java
public class Animaux{

	String nom;
	public Animaux(nom){
		this.nom=nom;
	}
public void abstract faireBruit();
}

```

Chien
```java
public class Chat extends Animaux{

	String nom;
	int nbrMoustaches;
	public Chat(int nbrMoustaches){
		super.Animaux()
		this.nbrMoustaches=nbrMoustaches;
	}
	
public void faireBruit(){
		Sysout("miii")
	};
}

```

# Interfaces

Une interface est une pseudo classe dont on ne pourra jamais instancier d'objet et dont les comportements (méthodes) pourrons êtres transmises aux classes qui les implémenterons


> [!NOTE] Note
> Une interface commence par **interface** et pas **public abstract XYZ**

Exemple: interface donnant la méthode de déplacement des vertébrés
```java
interface Vertebres{
	public void methodeDeplacement();
}
```

implémentation de la méthode déplacement pour des Mammifères et pour quelque chose qui n'est pas un vertébré
```java
public class Mammifere implements Vertebres;
	private String habitat;
	private String deplacement;
	
	public Mammifere(String habitat,String deplacement){
		this.habitat=habitat;
		this.deplacement=deplacement;
	}
	public void methodeDeplacement(String deplacement){
		System.out.println("je me deplace ainsi :"+ this.deplacement)
	}
public class Fungi implements Vertebres{
	private String type;
	private String deplacement;
	private boolean spores;
	public Fungi(String type, String deplacement, boolean plasmode){
		this.type= type;
		this.deplacement=deplacement;
		this.plasmode=plasmode;
	}

	public void methodeDeplacement(String deplacement){
		System.out.println("je me deplace ainsi "+ this.deplacement+ " car presence plasmodes : " +this.plasmode)
	}
}
	
```

---
# Algorithmes de tri et recherche

La recherche dans un tableau de données implique un tri si on ne veux pas perdre notre temps; on risque d'augmenter linéairement le temps de recherche si les données ne sont pas triées.

Une méthode instinctive est de comparer 2 à 2 chaque élément; si on a 128 éléments on compare chaque éléments aux autres, pour tout les éléments existants, donc 128 * 128 en pire cas. On aura alors $16384$ comparaisons. 

Mais, si on coupe en 2 le tableau, qu'on compare 64 éléments, on aura 64 * 64 comparaisons fois pour chaque sous liste. Les réorganiser implique de passer 1 fois a travers la liste car on comparera toujours les même index de chaque liste (on aura n comparaisons en les réunissant). On aura alors $2*4096 + 128 = 8320$ comparaisons.

Ca diminue, mais trier une liste de 2 éléments seulement c'est cool. 
$log_2(128) = 7$, c'est le nombre de divisions pour arriver à des groupes de 1 

- Si on commence avec n listes de 1 élément, on fusionne des listes adjacentes pour former des listes triées au niveau supérieur; on passe de 128 listes de 1 à 64 listes de 2.
- À chaque niveau, le **nombre de listes est divisé par 2**, passant de n à $n/2$, $n/4$, et ainsi de suite, tandis que **la taille des listes double **. 
- Au niveau $b$, il y a $n / (2^b)$ listes de taille $2^b$.
- Le total des comparaisons à chaque niveau reste constant car on a $(2^b) * n / (2^b)$ donc n. Le nombre de niveau est donné par $log_2(n) \rightarrow O(nlog_2(n))$ 

Une méthode de recherche dans un tableau trié est **la recherche dichotomique**

>dichotomie: recherche **en scindant en 2 un set** de data via un pivot; si la valeur est **supérieure** a ce pivot, on appelle **récursivement** la fonction pour **scinder en 2 le sous set créé**, de même si elle est inférieure.

```java
private static int binarySearch( int[] t, int x, int l, int r ) { 

//tab t
	if( r >= l ) { //si les extremitées sont pas égales
		int mid = l + ( r - l ) / 2; //alors on a un milieu
			if( t[mid] == x )        //si ce milieu = ce qu'on cherche, good
			return mid; 
	if( t[mid] > x ) 
		return binarySearch( t, x, l, mid - 1 ); 

	return binarySearch( t, x, mid + 1, r ); 
	} 
}
```

Dans ce cas la, le temps qu'on prend, en fct de la taille du tableau, **croit logarithmiquement** 
Pour augmenter de 1 seconde un programme qui cherche parmi 8 éléments en découpant par 2 la sélection, il faudrait **doubler la sélection

$$Log_{set}(selection) = temps $$

| **Situation**                           | **Tri recommandé**          | **Complexité moyenne** |
| --------------------------------------- | --------------------------- | ---------------------- |
| Tableau petit                           | Tri par insertion           | O(n²)                  |
| Presque trié                            | Tri par insertion           | O(n)                   |
| Performance générale                    | Quicksort                   | O(n log n)             |
| Pire cas stable                         | Merge Sort                  | O(n log n)             |
| Données uniformément réparties          | Bucket Sort                 | O(n)                   |
| Grands tableaux, mémoire limitée        | Merge Sort                  | O(n log n)             |
| En place, faible mémoire supplémentaire | Quicksort                   | O(n log n)             |
| Stabilité requise                       | Merge Sort ou Counting Sort | O(n log n), O(n + k)   |

---
# Structures de données : Abstraction vs implémentation

Une abstraction est un ensemble de méthodes redéfinies par une implémentation

>- Une Automobile est une implémentation des méthodes d'un Véhicule,
>- Un ArrayList est une implémentation de l'abstraction List

### Types abstraits de données

On défini le concept d'organisation, pas comment on le fait essentiellement 

>On peut accélérer dans un véhicule, mais une moto c'est par le guidon et une voiture par une pédale)

| **TYPE** | **Principe général**   |
| -------- | ---------------------- |
| List     | Éléments ordonnés      |
| Map      | Correspondance par clé |
| Pile     | First In Last Out      |
| File     | First In First Out     |
| Ensemble | Éléments pas ordonnés  |
### Ce que fais List en général

on peut 
- ajouter des éléments
- en supprimer
- trouver un en particulier
- trouver la taille du tableau etc...

==le contrat de List est en fait "je te donne les signatures de méthodes que tu dois redéfinir, débrouille toi"==

```java
public interface List<E> { 
	void add(E element);      // Ajout d’un élément E 
	void remove(int index);   // Suppression d’un élément 
	int get(int index);           // Récupération d’un élément 
	int size();               // Taille de la liste 
}
```

Voici une implémentation concrète par ArrayList

```java
public void add(E element) {
    if (size == elements.length) {
        // Si le tableau est plein, on le redimensionne
        resize();
    }
    elements[size++] = element; // Ajoute l'élément à la fin
}
```

et la même chose mais par LinkedList 

```java
public void add(E element) { 
	Node<E> newNode = new Node<>(element); // Créer un nouveau nœud avec l'élément 
	if (head == null) { // Si la liste est vide, nouveau nœud devient la tête 
		head = newNode; 
		tail = newNode; 
	} else {                 // Sinon, on ajoute le nœud à la fin 
		tail.next = newNode; // L'ancien dernier nœud pointe vers le nouveau
		tail = newNode;      // Le nouveau nœud devient la queue } 
		size++;              // Incrémente la taille de la liste }
```


| **Critère**              | **`ArrayList`**          | **`LinkedList`**                   |
| ------------------------ | ------------------------ | ---------------------------------- |
| **Accès aléatoire**      | O(1)  (très rapide)      | O(n)                               |
| **Ajout à la fin**       | O(1)                     | O(1)                               |
| **Ajout au début**       | O(n)                     | O(1)                               |
| **Suppression au début** | O(n)                     | O(1)                               |
| **Mémoire utilisée**     | Moins (tableau organisé) | Plus (références pour chaque nœud) |
| **Tri**                  | Très rapide              | Plus lent                          |
#### Liste
```java
import Noeud
public ListeChainee implements List{

	private Noeud premier;        //ATTRIBUT
	private Noeud dernier;        //ATTRIBUT
	
	public Liste(){               //CONSTRUCTEUR
		this.premier = null;
		this.dernier = null;
	}
	
	public setPremier(Noeud premier){
		this.premier=premier;
		
	}
	public setDernier(Noeud dernier){
		this.dernier=dernier;
	}
	
	private Noeud getNoeud( int idx ) {
		Noeud node = this.premier;
		for( int i = 0 ; i < idx; i++ ) 
			node = node.prochain; 
		return node; 
	}
	
	public void set( int i, int value ) { 
		getNoeud( i ).element = value; 
	}

	public int size() { 
		int size = 0; 
		Noeud node = this.premier; 
			while( node != null ) { 
				size++; node = node.prochain; 
				} 
			return size; 
	}
	
	public void print() { 
		Noeud node = this.premier; 
		while( node != null ) { 
			System.out.println( node.element ); 
			node = node.prochain; 
			} 
		}
//------------------------------------------------
public static void main (String[] args){

	liste.setPremier(new Noeud(1, new Noeud(2, new Noeud(3...))));
	
	}

}
}
```
#### Constructeur de noeud

```java
public class Noeud{

	public int valeur;
	public int prochain;
//----------------------------------------//
	public Noeud(int valeur, int prochain){
		this.valeur = valeur;
		this.prochain = prochain;
	}
//----------------------------------------//
private getNoeud(int idCondition){
	Noeud node = this.premier
	for(int i = 0, i< idCondition; i ++ ){
		node = node.getprochain();
	}
	return node;
}
//----------------------------------------//
public setProchain(int idProchain){
	this.prochain=idProchain;
}
public get(int id){
	return getNoeud(id);
}



public addAt(Noeud nouveau,int id){
	if (id == 0){
		addFirst(Noeud nouveau);
	}
	else{
		Noeud précédent = 
	}
}
///
public static void main (String[] args){

	Noeud dernier = new Noeud(3, null);
	Noeud premier = new Noeud(4, null);
	Noeud deuxieme = new Noeud(2,null);

	premier.setProchain(deuxieme);
	deuxieme.setProchain(dernier);
	
	}

}
```

---
#### Stack / Pile

L'abstraction de Pile est implémentée avec Vector pour le **push, pop, peek**

Soit l'arbre tel que 
1)             7
2)        {2} - {6}
3) {{4} {5}} - {{9} {1}}

pour **trouver** 9, si j'avais la liste {7,2,4,5,6,9,1} ça reviendrai à dire: 

>[!NOTE]
>Est ce que 9 est au **milieu** de {7,2,4,5,6,9,1}?
>- Non,
>	- il est au **milieu** de {6,9,1} ?
>	- Oui, STOP

#### Map

Un Map (ou Dictionnaire, ou Tableau associatif) est une structure de données qui permet d’associer des clés et des valeurs de **types arbitraires **: 
- <clé: Étudiant => valeur : String>

Déclaration avec diamond :

```java
// Façon longue : 
ArrayList<Étudiant> tab = new ArrayList(); 
ArrayList<Étudiant> tab = new ArrayList<Étudiant>(); 

ArrayList<> tab = new ArrayList<Étudiant>(); //FAUX
```
# Exceptions

==Servent à exécuter du code en cas de situation **anormale**==
- Entrée d'un périmètre négatif
- Un index non valide
- Un objet non existant ...
 
Dans le try, on insère le code qui peux potentiellement ne pas marcher (a cause d'une erreur humaine)
Dans le catch on spécifie l'erreur a attraper et on insère le code a exécuter en cas où

>Attention : les blocs catchs ne sont pas comme les switch-case, **dès que un est atteint, le reste est ignoré**. Il faut traiter les erreurs **enfant avant celle des parents**.
>-  Une ArithmeticException est un enfant de Exception, si on catch Exception avant ca ne marchera pas car on na pas l'occasion d'Attraper l'erreur, le programme crash


On inclus un bloc **finally** pour exécuter un code **peu importe** la situation

 
 ```java
import java.io.*;

public class MainApp {
    public static void main(String[] args) {
        try {
            lireFichier("inexistant.txt");
        } catch (IOException e) {
            System.out.println("Erreur lors de la lecture : " + e.getMessage());
        } finally { //facultatif
            System.out.println("Opérations terminées.");
        }
    }
// -----------------------------------------------------------------------//
    public static void lireFichier(String nomFichier) throws IOException {
        FileReader file = new FileReader(nomFichier);
        BufferedReader br = new BufferedReader(file);
        System.out.println(br.readLine());
        br.close();
    }
}
 ```


==On **throw** les **exceptions** possibles aux méthodes ; on les **catch** dans la méthode **main**==

```java
java.lang.Exception
    ├── java.lang.InterruptedException
    ├── java.lang.RuntimeException
        ├── java.lang.ArithmeticException
        ├── java.lang.ArrayStoreException
        ├── java.lang.ClassCastException
        ├── java.lang.EnumConstantNotPresentException
        ├── java.lang.IllegalArgumentException
            ├── java.lang.NumberFormatException
        ├── java.lang.IllegalThreadStateException
        ├── java.lang.IllegalMonitorStateException
        ├── java.lang.IllegalStateException
        ├── java.lang.IndexOutOfBoundsException
            ├── java.lang.ArrayIndexOutOfBoundsException
            ├── java.lang.StringIndexOutOfBoundsException

```

#### Utiliser des exceptions vérifiées si** :

- L’erreur est **anticipée** et **récupérable** par le programme.
- Exemple : ouvrir un fichier, établir une connexion à une base de données.

#### Utiliser des exceptions non vérifiées si** :

- L’erreur résulte d’un problème **logique ou de programmation**.
- Exemple : accès à un tableau hors des limites, division par zéro.

---
# Fichiers  : Lecture et Écriture

Un fichier = une séquence ordonnée de bytes

 ```java
import java.io.*;

public class LectureEtEcriture {
    public static void main(String[] args) throws IOException {
        String fichierSource = "source.txt"; // Fichier d'entrée
        String fichierDestination = "destination.txt"; // Fichier de sortie

        // Lecture du fichier source
        BufferedReader br = new BufferedReader(new FileReader(fichierSource));

        // Écriture dans le fichier destination
        BufferedWriter bw = new BufferedWriter(new FileWriter(fichierDestination));

        // Copie ligne par ligne
        String ligne;
        while ((ligne = br.readLine()) != null) {
            bw.write(ligne); // Écriture de la ligne lue
            bw.newLine();    // Saut de ligne
        }

        // Fermeture des ressources
        br.close();
        bw.close();

        System.out.println("Lecture et écriture terminées !");
    }
}
 ```

---
### Sérialisation

La **sérialisation** en Java est un processus qui convertit un objet en une séquence d'octets, ce qui permet de :

1. **Sauvegarder l'état d'un objet** dans un fichier ou une base de données.
2. **Transférer un objet** sur un réseau (par exemple, entre des systèmes distants).

```java
import java.io.*;

// Classe Etudiant implémentant Serializable
public class Etudiant implements Serializable {
		private String prenom, nom;
		private int matricule;

    // Constructeur
    public Etudiant(String prenom, String nom, int matricule) {
        this.prenom = prenom;
        this.nom = nom;
        this.matricule = matricule;
    }

    // Méthode principale pour sérialiser un objet
    public static void main(String[] args) {
        // Création de l'objet Etudiant
        Etudiant e = new Etudiant("Jimmy", "Whooper", 1239572);

        try {
            // Création d'un flux pour écrire dans le fichier
            FileOutputStream fileOs = new FileOutputStream("etudiant.dat");
            ObjectOutputStream os = new ObjectOutputStream(fileOs);

            // Sérialisation de l'objet
            os.writeObject(e);
            os.close(); // Fermeture du flux

            System.out.println("Objet sérialisé avec succès dans etudiant.dat");
        } catch (IOException ex) {
            System.out.println("Erreur à l'écriture");
        }
    }
}

```


---
# Serveurs/Client

Interface fonctionnelles

```java
import java.io.*;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.Date;

public class JavaServer {
    public static void main(String[] args) {
        try {
            // Création d'un serveur sur le port 1337, acceptant 1 client
            ServerSocket server = new ServerSocket(1337, 1);
            System.out.println("Serveur en attente de connexion sur le port 1337...");

            // Attente de connexion d'un client
            Socket client = server.accept();
            System.out.println("Connexion établie !");
            System.out.println("Client connecté : " + client);

            // Configuration des flux pour lire les données envoyées par le client
            InputStreamReader is = new InputStreamReader(client.getInputStream());
            BufferedReader reader = new BufferedReader(is);

            String line;
            // Boucle principale pour écouter les commandes du client
            while ((line = reader.readLine()) != null) {
                System.out.println("Reçu : " + line);

                // Découper la commande et les arguments
                String[] parts = line.split(" ");
                String commande = parts[0];
                String argument = String.join(" ", parts.length > 1 ?
                        java.util.Arrays.copyOfRange(parts, 1, parts.length) : new String[0]);

                // Traitement des commandes
                switch (commande) {
                    case "echo":
                        System.out.println(argument);
                        break;
                    case "reverse":
                        System.out.println(new StringBuilder(argument).reverse());
                        break;
                    case "date":
                        System.out.println(new Date());
                        break;
                    case "count":
                        System.out.println(argument.length());
                        break;
                    default:
                        System.out.println("Commande inconnue");
                        break;
                }
            }

            // Fermeture du serveur lorsqu'il n'y a plus de client
            System.out.println("Fin de la connexion");
            reader.close();
            client.close();
            server.close();
        } catch (IOException ex) {
            System.err.println("Erreur : " + ex.getMessage());
            ex.printStackTrace();
        }
    }
}

````


client


```java
import java.io.*;
import java.net.Socket;
import java.util.Scanner;

public class JavaClient {
    public static void main(String[] args) {
        // Adresse IP et port du serveur
        String serverAddress = "127.0.0.1"; // Adresse locale
        int serverPort = 1337;             // Port du serveur

        try (
            // Connexion au serveur
            Socket clientSocket = new Socket(serverAddress, serverPort);

            // Configuration des flux pour communiquer avec le serveur
            BufferedWriter writer = new BufferedWriter(
                new OutputStreamWriter(clientSocket.getOutputStream())
            );
            BufferedReader reader = new BufferedReader(
                new InputStreamReader(clientSocket.getInputStream())
            );

            // Scanner pour lire les commandes depuis la console
            Scanner scanner = new Scanner(System.in)
        ) {
            System.out.println("Connecté au serveur " + serverAddress + ":" + serverPort);
            System.out.println("Tapez vos commandes (Ctrl+C pour quitter) :");

            // Boucle principale pour envoyer des commandes et recevoir des réponses
            while (true) {
                System.out.print("> "); // Prompt
                String command = scanner.nextLine(); // Lire la commande de l'utilisateur

                // Envoyer la commande au serveur
                writer.write(command);
                writer.newLine(); // Ajouter un saut de ligne pour terminer la commande
                writer.flush();   // Envoyer immédiatement la commande
                System.out.println("Commande envoyée : " + command);

                // Lire la réponse du serveur
                String response = reader.readLine();
                if (response == null) {
                    System.out.println("Le serveur a fermé la connexion.");
                    break;
                }
                System.out.println("Réponse du serveur : " + response);
            }
        } catch (IOException ex) {
            System.err.println("Erreur : Impossible de se connecter au serveur");
            ex.printStackTrace();
        }
    }
}

```

---
### Event handler

Pattern d'attente d'évènement :
1) Création de la fct d'écoute listens; 

```java
public class Server { 
	private ServerSocket server; 
	public Server(int port) throws IOException { // Crée le serveur sur le port spécifié 
	this.server = new ServerSocket(port, 1); // Attends une connexion... 
	//on defini ce quon peut traiter
} 
public void listen() { // *** Boucle d'événements *** 
	while ((line = reader.readLine()) != null) { // Lire et exécuter la next cmd 
	this.process(line); 
	} 
}
```

ce qui implique qu'au server on call la méthode .listens()

```java
public static void main(String[] args){
	Server s = new Server(1337); // Démarre la boucle d'événements 
	s.listen();
}
```

Le *problème* c'est qu'**on devra définir dans la classe Server** chaque évènement possible; idéalement on devrait **traiter les cas dans la classe main**

On aurait :

```java
Server s = newServer("127.0.0.1", 1337);
s.addEventHandler(eventA);
s.addEventHandler(eventB);
s.addEventHandler(eventC);
//...
s.addEventHandler(eventRandomNumber);
```

C'est de la merde... genre je dois mettre chaque fucking évènement qui peut se produire à ce serveur

Si on à 30 événements à gérer => 30 classes définies dans 30 fichiers éparpillés dans le projet fuck

Option possible

```java
EventHandler dateHandler = new EventHandler() { 
@Override 
public void handle(String command, String argument) { 
	if (command.equals("date")) { 
		System.out.println(new Date()); 
		} 
	} 
};
```

Donc là on est entrain de créer un gestionnaire d'évènements (EventHandler) avec une **méthode de gestion (handle)** qui a en paramètres une commande et un argument.
On aurait tout de même besoin de faire 3467812903 "if" pour **vérifier le champ de commande.**

Donc fuck that, on prend EventHandler comme une interface

```java
@FunctionalInterface 
public interface EventHandler { 
	public void handle(String command, String argument); 
}
```
 
 Pour avoir 
 
```java
Server server = new Server(1337); // Définition + ajout d'un événement 

	server.addEventHandler((cmd, arg) -> {  //j'ajoute un event de cmd, arg
		if (cmd.equals("echo")) {  //si cmd = echo
			System.out.println(arg); //then je print arg
		} 
	});
```


---
### JAVAFX

### **Hiérarchie Parent-Enfant en JavaFX**

1. **`Stage` (Fenêtre)**
    - **Contient :** Une seule `Scene`.
    - **Rôle :** Représente la fenêtre principale ou une fenêtre secondaire de l'application.
    - **Exemple :**

```java
  Stage primaryStage = new Stage(); primaryStage.setTitle("Ma Fenêtre");
```

---

2. **`Scene` (Scène)**
    - **Contient :** Un **Root Node** (le nœud racine, généralement un conteneur comme `VBox` ou `Pane`).
    - **Rôle :** La scène agit comme un "contenant" qui gère tous les éléments affichés dans le `Stage`.
    - **Exemple :**

```java
Scene scene = new Scene(new VBox(), 400, 300); // Conteneur racine + larg et haut 
primaryStage.setScene(scene);
```

---

3. **`Root Node` (Conteneur)**
    - **Contient :** Des nœuds enfants (ou d'autres conteneurs imbriqués).
    - **Rôle :** Organise les nœuds enfants selon des dispositions spécifiques.
    - **Types principaux de conteneurs :**
        - **`VBox` :** Dispose les enfants verticalement.
            `VBox root = new VBox();`
            
        - **`HBox` :** Dispose les enfants horizontalement
            `HBox root = new HBox();`
            
        - **`Pane` :** Permet de positionner librement les enfants avec des coordonnées `(x, y)`.
            `Pane root = new Pane();`
---

4. **Nœuds enfants (Nodes)**
    - **Exemples :** `Label`, `Button`, `TextField`, `ImageView`, etc.
    - **Rôle :** Ce sont les éléments graphiques interactifs ou visuels ajoutés à l'interface utilisateur.
    - **Exemple :**

```java
Label label = new Label("Bonjour"); 
Button button = new Button("Cliquez-moi"); 
root.getChildren().addAll(label, button); //on add les enfants
```

---

### **Résumé illustré :**

1. **`Stage`** → Fenêtre de l'application.
2. **`Scene`** → Contient et gère le nœud racine.
3. **`Root Node` (Conteneur)** → Organise les éléments (vertical, horizontal, ou libre).
4. **Nœuds enfants (Nodes)** → Boutons, textes, images affichés dans le conteneur.

### **Différences clés à retenir avec pane :**

1. **Pane** :
    - Les éléments sont positionnés manuellement avec des coordonnées `(x, y)`.
    - Idéal pour des applications dynamiques ou interactives (exemple : animations, jeux).
2. **VBox / HBox** :
    - Dispose automatiquement les éléments dans un ordre **vertical** (VBox) ou **horizontal** (HBox).
    - Parfait pour des interfaces **statiques** et bien structurées (exemple : formulaires, menus).

exemple page simple 

```java
public class ExempleHierarchie extends Application {
    @Override
    public void start(Stage primaryStage) {
        // Création des nœuds enfants
        Label label = new Label("Bonjour, JavaFX!");
        Button button = new Button("Cliquez-moi!");

        // Création du Root Node (VBox)
        VBox root = new VBox();
        root.getChildren().addAll(label, button);

        // Création de la scène
        Scene scene = new Scene(root, 300, 200);

        // Ajout de la scène au stage
        primaryStage.setScene(scene);
        primaryStage.setTitle("Hiérarchie JavaFX");
        primaryStage.show();
    }
    public static void main(String[] args) {
        launch(args);
    }
}

```


## MVC

#### **1. Le Modèle (Model)**

C’est la partie **cerveau** de l’application.

- **Rôle** : Il gère les données et les calculs.
- Dans notre exemple, c’est la valeur du compteur et la logique pour l’incrémenter.

**Exemple :**
```JAVA
public class ModeleCompteur {
    private int valeur = 0; // Donnée : le compteur commence à 0

    public int getValeur() { // Lire la valeur actuelle
        return valeur;
    }
    public void incrementer() { // Ajouter 1 à la valeur
        valeur++;
    }
}
```
- Ici, **`valeur`** est la donnée importante.
- **`incrementer()`** fait le travail d'ajouter +1.

---
#### **2. La Vue (View)**

C’est la partie **écran** de l’application.
- **Rôle** : Elle montre les données à l'utilisateur et affiche des boutons ou champs de texte pour interagir.
- Dans notre exemple, la vue montre :
    - Un bouton "Incrémenter".
    - Une zone qui affiche la valeur actuelle.

```JAVA
import javafx.scene.control.Button;
import javafx.scene.control.Label;
import javafx.scene.layout.VBox;

public class VueCompteur extends VBox {
    public Label label = new Label("0"); // Montre la valeur
    public Button bouton = new Button("Incrémenter"); // Bouton pour ajouter +1

    public VueCompteur() {
        // Ajouter le label et le bouton à l'écran
        getChildren().addAll(label, bouton);
    }
}
```
- **`label`** affiche la valeur du compteur.
- **`bouton`** permet à l'utilisateur d'interagir.

---

### **3. Le Contrôleur (Controller)**

C’est la partie **chef d’orchestre**.

- **Rôle** : Il relie la vue et le modèle.
- Il écoute les actions de l’utilisateur (clics, saisies) et met à jour les données dans le modèle.
- Ensuite, il demande à la vue de s'actualiser.

```JAVA
public class ControleurCompteur {
    private ModeleCompteur modele;
    private VueCompteur vue;

    public ControleurCompteur(ModeleCompteur modele, VueCompteur vue) {
        this.modele = modele;
        this.vue = vue;

        // Action quand l'utilisateur clique sur le bouton
        vue.bouton.setOnAction(event -> {
            modele.incrementer(); // Ajoute +1 dans le modèle
            vue.label.setText(String.valueOf(modele.getValeur())); 
            // Met à jour l'affichage
        });    }    }

```

- Quand tu cliques sur le bouton :
    1. Le **modèle** ajoute +1 à la valeur.
    2. La **vue** met à jour le texte du label avec la nouvelle valeur.

---
# Multithreading

Le but du multithreading est de faire 2 choses différentes, mais en même temps, les rejoindre à la fin pour terminer le programme principal

ex.

| Processeur 1                      | Processeur 2                      |
| --------------------------------- | --------------------------------- |
| Additionner somme première moitié | Additionner somme deuxième moitié |
Ensuite on add les 2

#### Thread

Un thread = fils d'exécution d'instructions séquentielles (de base on en a toujours 1, le main)

Pour exécuter des threads on a besoin de quelque chose qui puisse les run, Runnable

```java
@FunctionalInterface 
public interface Runnable { public void run(); }
```

```java
Thread t = new Thread(() -> { 
	double total = 0; 
	for(int i=0;i < nbr.length/2; i++){
		total+= Math.sin(number[i]);
	}
	
}); 
t.start();
```

L'exécution est imprévisible. si je call le thread 1  puis le 2 je peux avoir des réponses très bizarres. 
.join()
On peut attendre la fin d'un thread pour 

On doit synchronise les thread

