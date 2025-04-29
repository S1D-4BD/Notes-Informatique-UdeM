# Cours 03 – Révision

## Chapitre 1 : Révisions de notions de base

### Tableaux

Un tableau est une séquence d’éléments (valeurs ou références) de même type. Les éléments sont numérotés à partir de 0 et peuvent être référencés par leur numéro grâce à l’opérateur d’index `[]`.

### Types primitifs vs Types références

- **Type primitif** : Une variable de type primitif stocke une valeur primitive (boolean, int, double, etc.).
- **Type référence** : Une variable de type référence stocke une référence sur la donnée, c'est-à-dire l'adresse (référence) d’un objet ou `null`.

### Création de tableaux

#### Tableau de valeurs `int`

int[] tabInt;
tabInt = new int[10];

>Tout est stocké dans le stack
#### Tableau de références `String`

String[] tabString = new String[10];

Représentation :

> Dans le stack on a seulement la référence, on aura null dans les autres adresses du stack

### Initialisation de tableaux lors de leur création

#### Tableau de références `String`

String[] tabString = new String[]{ "Roger", "Julien", "Marie" };

#### Tableau de valeurs `char`

char[] voyelles = {'A', 'E', 'I', 'O', 'U', 'Y'};

### Accès aux éléments d’un tableau

#### Exemple avec un tableau d’entiers

int[] tabInt = new int[10];
tabInt[3] = 12;
tabInt[9] = 24;

### Parcourir les éléments d’un tableau

#### Utilisation de la boucle `for` classique

String message = "";
for (int i = 0; i < tabNoms.length; i++) {
    message += tabNoms[i] + "\t";
}
System.out.println(message);

#### Utilisation de la boucle `for-each`

String message = "";
for (String nom : tabNoms) {
    message += nom + "\t";
}
System.out.println(message);

### Initialiser un tableau à l’aide d’une boucle `for`

double[] salaires = new double[6];
Scanner scan = new Scanner(System.in);
String saisie = "";

for (int i = 0; i < salaires.length; i++) {
    System.out.println("Entrer un salaire : ");
    saisie = scan.nextLine();
    salaires[i] = Double.parseDouble(saisie);
}

### Initialiser un tableau avec boîte de dialogue

double[] salaires = new double[6];
String saisie = "";

for (int i = 0; i < salaires.length; i++) {
    saisie = JOptionPane.showInputDialog("Entrer un salaire");
    salaires[i] = Double.parseDouble(saisie);
}

---

## Exercices formatifs : Laboratoire 04 – tableaux et boucles

---

## Chapitre 5 : Méthodes

### Déclaration d’une méthode

[Visibilité] [modificateur] [Type de retour] nomMethode(type param1, type param2, ...) {
    // Les instructions
}

- **Visibilité** : `public` ou `private`
- **Modificateur** : `static` ou pas - Méthode de classe ou d’instance
- **Type de retour** : `void`, type de base (int, double...), ou type référence

#### Exemple

public class Calcul {
    public int somme(int p1, int p2) {
        return p1 + p2;
    }
}

### Appel de méthode

public class Principale {
    public static void main(String[] args) {
        Calcul c = new Calcul();
        int nb1 = 12, nb2 = 34;
        int res = c.somme(nb1, nb2);
        System.out.println(res);  // Affichera le résultat
    }
}

### Passage des paramètres

En Java, les arguments sont passés par **valeur**, c'est-à-dire qu’une copie de l’argument est transmise à la méthode. Toute modification de cette copie n’aura pas d’incidence sur la valeur originale.
#### Exemple avec une méthode qui incrémente les paramètres

public static int mystere(int p1, int p2) {
    p1++;
    p2++;
    return p1 + p2;
}

#### Exemple avec méthode `swap`

public static void swap(int p1, int p2) {
    int temp = p1;
    p1 = p2;
    p2 = temp;
}

**Après l’appel**, les valeurs de `nb1` et `nb2` ne changent pas car elles sont passées par valeur.

---
### Passage d'une référence

#### Exemple avec `String`
```java
public class Principale { 
    public static void main(String[] args) { 
        String s = "Bienvenue"; 
        // appel de la méthode afficher
        afficher(s); 
    } 

		public static void afficher(String p) { 
        System.out.println(p); 
    }
}
```

>String : est un type référence, s est une instance String
		• lors de l’appel, la méthode afficher() reçoit une copie de la référence de l’argument s (par exemple @100) 
		• s et p feront référence au même objet

---
#### Exemple où la référence est modifiée

public static void traduire(String p) {
    p = "Hi";
}

Dans cet exemple, après l’appel, la valeur originale de `s` ne change pas.

#### Exemple avec retour de référence

public static String traduire(String p) {
    p = "Hi";
    return p;
}

Dans cet exemple, la valeur de `s` reste inchangée, mais la méthode retourne une nouvelle valeur.

---

### Tableau et passage par référence

Un tableau est un type référence. Lors de l’appel à une méthode avec un tableau, une copie de la référence du tableau est transmise, ce qui signifie que toute modification dans la méthode affecte le tableau original.

#### Exemple

```java
public class Principale {
    public static void main(String[] args) {
        double[] salaires = new double[6];
        // appel de la méthode remplir
        remplir(salaires);
        
        // Afficher les valeurs du tableau après l'appel à la méthode remplir
        for (double salaire : salaires) {
            System.out.println(salaire);
        }
    }

    public static void remplir(double[] tab) {
        for (int i = 0; i < tab.length; i++) {
            tab[i] = 100;
        }
    }
}
```

# Cours 13 – Héritage

## Chapitre 1 : Étape 3

### Relation entre les classes et notation UML

- **Association**
- **Agrégation**
- **Composition**
- **Héritage**

Exemples :
- Une voiture a 4 roues
- Une présentation PowerPoint est composée de diapositives
- Un dessin comprend un ensemble de figures géométriques
- Une équipe de recherche est constituée d’un ensemble de personnes

### Principe de l’héritage

- L’héritage permet de définir de nouvelles classes (sous-classes) à partir d'une classe déjà existante (superclasse).
- La superclasse contient les informations communes à ses sous-classes.

Exemples :
- **JFrame** → **Fenetre**
- **Compte** → **CompteCheque**, **CompteEpargne**
- **Véhicule** → **Voiture**, **Vélo**

#### Une sous-classe :
- Hérite des membres héritables de la superclasse.
- Peut étendre la superclasse avec de nouveaux attributs et de nouvelles méthodes (extension).
- Peut spécialiser certaines méthodes de sa superclasse (override).

```java
public class TestPoint {
    public static void main(String[] args){
        // pc1 est de type PointC
        PointC pc1 = new PointC (3, 10, "BLUE");

        // toString() redéfinie pour afficher un point coloré :
        System.out.println(pc1.toString());

        // pc2 est de type Point mais se comporte comme PointC
        Point pc2 = new PointC (2, 6, "ROUGE");

        // toString() redéfinie pour afficher un point coloré
        System.out.println(pc2.toString());
    }
}

```