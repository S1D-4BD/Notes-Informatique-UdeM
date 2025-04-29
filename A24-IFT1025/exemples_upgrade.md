#util_random

L'outil random consiste a importer la classe Random, instancier un objet (disons randomiser) pour appeller via cet objet les methodes de random

```java
import java.util.Random;

public class demoRandom {

    public static void main(String[] args){

        Random random = new Random();

        int x = random.nextInt(6)+1;
        double y = random.nextDouble(4);
        boolean z = random.nextBoolean();

        System.out.println(x);
        System.out.println(y);
        System.out.println(z);

    }

}
```

#exemple_ArrayList

L'outil ArrayList permet de travailler avec une table dynamique (plus de méthodes, taille redimensionnable), mais ne peut prendre que des objets en éléments (pas de int, mais plutôt Integers)

```java
ArrayList<String> food = new Arraylist<String>();
food.add("mouloukhia");
food.add("hamburger");
food.add("bradwurst");

food.set(0,"sushi");
food.remove(2);
//food.clear();

for(int i =0; i<food.size; i++{
	System.out.println(food,get(i));
}
```


**Liste des méthodes les plus cool:**

>1) ==add(e)==
>2) ==add(index, e)==
>3) ==get(index)==
>4) ==set(index)==
>5) remove(index)
>6) ==size()==
>7) contains(e)
>8) isEmpty()
>9) ==clear()==
>10) indexOf()
>11) lastIndexOf()
>12) clone()


#exemple_commandes

Problème de base
On a des commandes qui doivent être faites pour un client, et **dans chaque commande** nous avons des articles qui peuvent avoir un prix et une identité différente

---
Étape 1: créer une classe Commande

```java
```


#exemple_recreate_Array

voici ce qu'on veux:

****Input:****  
	Array1 = [“a”, “b”, “c”, “d”, “e”, “f”],   
	Array2 = [“b”, “d”, “e”, “h”, “g”, “c”]  
****Output:****
	[a, f ]

1) **Comprendre le problème:**
	 On doit itérer les 2 Arrays pour retirer les éléments de b dans a
2) Quelles actions doivent êtres faites?
	1) On doit construire un nouvel array qui sera a - b
	2) Pour tout élément de a, si cet élément ne figure dans dans b alors on va l'insérer dans le nouvel array
	3) Ca implique une complexité de $O(n^2)$ puisqu'on itère tout les éléments de b pour chaque a

```java
package Exo;

import java.util.Scanner;

public class Ensemble{
   
    public int[] elements;
    public int capacite;
    public String name;

    /*Constructeur qui donne un nom et une capacité en param, et qui creer une liste de "capacité" élements*/

    public Ensemble(String name, int capacite){
        this.capacite = capacite;
        this.name=name;
        this.elements= new int[capacite];
    }
/*Cette methode prend en input rien


*/
    public int[] remplirTab(){
        Scanner scanner = new Scanner(System.in);
        int i = 0;
        System.out.println("Veuillez entrer " + capacite + " entiers :");
        while (i < capacite){
            int x = scanner.nextInt();
            elements[i] = x;
            i++;
        }
        i=0;
        return elements;
    }
    public void afficherTab(){
    System.out.println(name);
    for (int j = 0; j < capacite;j++){
        System.out.print(elements[j]);
        if (j < elements.length - 1) {
            System.out.print("-");
        }
        }
        System.out.println(" ");
    }
    public int[] add(int e){

        int longueur = elements.length;
        int[] temp = new int[longueur+1];
        for (int i = 0; i < longueur; i++){
            temp[i] = elements[i];
        }
        temp[longueur] = e;
        elements = temp;
        capacite++;
        return temp;
    }
	public int[] pop(){

        int longueur = elements.length;
        int[] temp = new int[longueur-1];
        for (int i = 0; i < (longueur-1); i++){
            temp[i] = elements[i];
        }
        elements = temp;
        capacite--;
        return elements;

    }
   public int[] replace(int index, int e){
        int longueur = elements.length;
        int[] temp = new int[longueur];
        for (int i = 0; i < (longueur); i++){
            temp[i] = elements[i];
            if (i == index){
                temp[i]= e;
            }
        }
        elements = temp;
        return elements;
    }

public int[] remove(int index){
        int longueur = elements.length;
        int[] temp = new int[(longueur-1)];
        for (int i = 0; i < (longueur-1); i++){
            temp[i] = elements[i];
            if (i == index){
                i++;
            }
        }

        //elements = temp;
        return temp;
        

    }

    public static void main(String[] args){

        //String nom;
        //int taille;

        Scanner s = new Scanner(System.in);

        Ensemble ensemble = new Ensemble("A",4);
        ensemble.remplirTab();
        System.out.println("Ensemble: "+ensemble.name);
        ensemble.afficherTab();
        Ensemble ensemble2 = new Ensemble("B",4);
        ensemble2.remplirTab();
        System.out.println("Ensemble: "+ensemble2.name);
        ensemble2.afficherTab();

  

        ensemble.add(5);

        ensemble.afficherTab();
        //System.out.println("Apres ajout de 5");
        ensemble2.add(6);
        ensemble2.afficherTab();
        s.close();

  

    }

}
```

---
iterateurs
```java
package Matrice;  
import java.util.ArrayList;  
import java.util.Iterator;  
  
/**  
 * Une implémentation de l'interface {@link MatriceCarree} en utilisant la classe * {@link ArrayList}. * *  
 * @param <E> le type de chose stocké dans la matrice.  
 */public class ArrayListMatriceCarree<E> implements MatriceCarree<E>, Iterable<E> {  
  
    private ArrayList<ArrayList<E>> lignes; //on crée un arraylist darraylist qui contien des val E  
    private int dimension;  
  
    /**  
     * Crée une matrice de dimension 0.     */    public ArrayListMatriceCarree() {  
       this(0);  
    }  
  
    /**  
     * Crée une matrice carée, avec une dimension donnée. Les cases de la matrice     * sont initialisées à {@code null}.     ** @param dim - la dimension de la matrice à créer.  
     */    public ArrayListMatriceCarree(int dim) {  
       this.dimension = dim;  
       this.lignes = new ArrayList<ArrayList<E>>(this.dimension);  
       for (int i = 0; i < this.dimension; i++) {  
          ArrayList<E> nouvelleLigne = new ArrayList<E>(this.dimension);  
          for (int j = 0; j < this.dimension; j++)  
             nouvelleLigne.add(null);  
          this.lignes.add(nouvelleLigne);  
       }  
    }  
  
    /**  
     * O=Methode pour retourner la dimension de la matrice     * @return     */    @Override  
    public int dim() {  
       return this.dimension;  
    }  
  
    /**  
     * Appelle mon vérificateur d'index,     * si le vérificateur retourne true, on retourne l'élément j de la ligne i sinon on throw une exception     * @param i - nombre de ligne  
     * @param j - nombre de colonne  
     * @return     * @throws MatriceIndexOutOfBoundsException     */    @Override  
    public E get(int i, int j) throws MatriceIndexOutOfBoundsException {  
       //FAIT//  
       verificateurIndex(i,j);  
       return this.lignes.get(i).get(j);  
    }  
  
    /**  
     *  Appelle mon vérificateur d'index,     *     si le vérificateur retourne true, on set l'élément j de la ligne i sinon on throw une exception     * @param i   - nombre de ligne  
     * @param j   - nombre de colonne  
     * @param val - la valeur à ajouter  
     * @throws MatriceIndexOutOfBoundsException     */    @Override  
    public void set(int i, int j, E val) throws MatriceIndexOutOfBoundsException {  
       if (verificateurIndex(i, j)) {  
          throw new MatriceIndexOutOfBoundsException();  
       }  
       this.lignes.get(i).set(j, val);  
       //FAIT//  
    }  
  
    @Override  
    public void ajoute(E val) throws MatricePleineException {  
       //FAIT  
  
       if (verificateurEstPlein()){  
          throw new MatricePleineException();  
       }  
  
       MatriceIterator<E> it = new MatriceIterator<>(this);  
       while (it.hasNext()) {  
          E n = it.next();  
          if (n == null) {  
             it.remplace(val);  
             break;  
          }  
       }  
    }  
  
    @Override  
    public Iterator<E> iterator() {  
       return new MatriceIterator<E>(this);  
    }  
  
    @Override  
    public String toString() {  
       String ret = "---\n";  
       for (var ligne : this.lignes) {  
          ret += ligne.toString() + "\n";  
       }  
       ret += "---\n";  
       return ret;  
    }  
  
    /**  
     * Vérifie si les index sont valides dans notre matrice<br>.     *     * Si i ou j est supérieur à la condition (ou juste pas possible, genre négatif) de dimension, pas bon     * @param i ligne  
     * @param j colonne  
     * @return     */    public boolean verificateurIndex(int i, int j){  
       if ((i < 0) || (i >= dimension) || (j < 0) || (j >= dimension)) {  
          return true; //  indices sont pas bons  
       } else {  
          return false; // il n y a aucun problème  
       }  
    }  
  
    /**  
     * Methode qui va itérer chaque élément de la matrice <br>     * Si on trouve 1 élément null, la matrice est pas pleine (false) , sinon pleine (true)     * @return     */    public boolean verificateurEstPlein(){  
       int condition = this.dimension;  
       for (int i=0; i<condition; i++){  
          for (int j=0; j<condition; j++){  
             if (this.lignes.get(i).get(j)==null){  
                return false;  
             }  
          }  
       }  
       return true;  
    }  
  
}
```

```
package Matrice;  
import java.util.Iterator;  
  
/**  
 * Un iterateur qui permet de parcourir un matrice ligne par ligne. * </br> * Par exemple, la matrice suivante sera parcourue * comme suit: 0,1,3,4,5,6,7,8.  
 * <pre> * --- * [0, 1, 2] * [3, 4, 5] * [6, 7, 8] * --- * </pre> * *  
 * @param <E>  
 */  
public class MatriceIterator<E> implements Iterator<E> {  
  
    private MatriceCarree<E> m;  
    private int iCourant, jCourant;  
    private int iPrecedent, jPrecedent;  
    private int max;  
  
    /**  
     * Crée un MatriceIterator pour une MatriceCarree donnée.     ** @param m - la MatriceCaree à itérer  
     */    public MatriceIterator(MatriceCarree<E> m) {  
       this.m = m;  
       this.iCourant = 0;  
       this.jCourant = 0;  
       this.max = m.dim();  
       this.iPrecedent = 0;  
       this.jPrecedent = 0;  
    }  
  
    /**  
     * Si on est au dernier index, il n'a nécéssairement pas de suivant     * @return     */    @Override  
    public boolean hasNext() {  
       return (iCourant < max) && (jCourant < max);  
    }  
  
    @Override  
    public E next() {  
  
       iPrecedent = iCourant;  
       jPrecedent = jCourant;  
  
       E ret = this.m.get(iCourant, jCourant);  
  
       if (jCourant < max - 1) {  
          jCourant++;  
       } else {  
          iCourant++;   //on est a la fin de la ligne donc on change de ligne i  
          jCourant = 0; //on retourne au premier element j  
  
       }  
  
       return ret;  
  
    }  
  
  
    /**  
     * Remplace le dernier élément visité par un autre élément. Ce méthode ne fait     * pas avancer l'itérateur. </br>     * Le dernier élément visité est le dernier élément rétourné par un appel à     * {@code next()}. Si {@code next()} n'a jamais été appelé, cette méthode     * remplace le premier élément de la matrice.     *     * Il est acceptable si une {@link MatriceIndexOutOfBoundsException} est générée  
     * si on essaie de remplacer un élément dans une matrice vide (dont la dimension     * est 0).     ** @param e - le nouveau élément  
     */    public void remplace(E e) {  
       this.m.set(iPrecedent, jPrecedent, e);  
    }  
  
  
    public int[] getPosition(E e){  
       for (int i = 0; i < m.dim(); i++) {  
          for (int j = 0; j < m.dim(); j++) {  
             if (m.get(i, j) != null && m.get(i, j).equals(e)) {  
                return new int[] { i, j }; // Retourne la position trouvée  
             }  
          }  
       }  
       return null; // Retourne null si l'élément n'est pas trouvé  
    }  
}
```

```package Matrice;  
/**  
 * Une Matrice carrée. Par exemple, un MatriceCaree de dimension 3: * * <pre>  
 * --- * [0, 1, 2] * [3, 4, 5] * [6, 7, 8] * --- * </pre> * *  
 * @param <E> le type de chose stocké dans la matrice.  
 */public interface MatriceCarree<E> extends Iterable<E> {  
  
    /**  
     * Retourne la dimension de la matrice.     *     * @return la dimension  
     */    public int dim();  
  
    /**  
     * Retourne l'élément à la position (i,j).     ** @param i - nombre de ligne  
     * @param j - nombre de colonne  
     * @return l'élément     * @throws IndexOutOfBoundsException si {@code i} ou {@code j} sont égales ou     *                                   supérieures de la dimension du matrice.     *                                   (NB: il s'agit d'une     *                                   {@link RuntimeException})     */    public E get(int i, int j) throws MatriceIndexOutOfBoundsException;  
  
    /**  
     * Met la valeur {@code val} à la position (i,j).     ** @param i   - nombre de ligne  
     * @param j   - nombre de colonne  
     * @param val - la valeur à ajouter  
     * @throws IndexOutOfBoundsException si {@code i} ou {@code j} sont égales ou     *                                   supérieures de la dimension du matrice.     *                                   (NB: il s'agit d'une     *                                   {@link RuntimeException})     */    public void set(int i, int j, E val) throws MatriceIndexOutOfBoundsException;  
  
    /**  
     * Ajoute la valeur {@code val} à la première position disponible de la Matrice.     * Une position est considerée «disponible» si son valeur est {@code null}. Si     * (0,0) est null, c'est celle la première position disponible. Si deux     * positions différentes (x1,y1) et (x2,y2) sont disponibles, et x1&lt;x2, nous     * préférons (x1,y1). Si deux positions différentes (x1,y1) et (x1,y2) sont     * disponibles, et y1&lt;y2,nous préférons (x1,y1). </br>     *     * Par exemple, prennez la matrice M:  
     *     * <pre>  
     * ---     * [0, 1, 2]     * [null, 4, null]     * [6, null, 8]     * ---     * </pre>     *     * M.ajoute(100) nous donnera:  
     *     * <pre>  
     * ---     * [0, 1, 2]     * [100, 4, null]     * [6, null, 8]     * ---     * </pre>     *     * Si ensuite on fait M.ajoute(200), cela nous donnera:  
     *     * <pre>  
     * ---     * [0, 1, 2]     * [100, 4, 200]     * [6, null, 8]     * ---     * </pre>     *     * Si ensuite on fait M.ajoute(300), cela nous donnera:  
     *     * <pre>  
     * ---     * [0, 1, 2]     * [100, 4, 200]     * [6, 300, 8]     * ---     * </pre>     *     * </br>  
     * Autrement dit, la matrice suivante peut être créée avec la boucle: {@code     *        for(int x=0; x<3; x++)     *           M.ajoute(x);     * }     *     * <pre>  
     * ---     * [0, 1, 2]     * [3, 4, 5]     * [6, 7, 8]     * ---     * </pre>     *     *   
     *   
* @param val - la valeur à ajouter  
     * @throws MatricePleineException si la matrice n'a pas de case disponible     *                                (c'est à dire, aucune case de la matrice n'a     *                                pas la valeur {@code null}).     */    public void ajoute(E val) throws MatricePleineException;  
  
}
```

```
package Matrice;  
  
public class Main {  
  
    public static void main(String[] args) {  
        // test matrice 3p3  
        ArrayListMatriceCarree<Integer> maMatrice = new ArrayListMatriceCarree<>(3); //ma matrice de Integer pk Integer est un objet  
  
  
        System.out.println("je remplis la matrice");  
        maMatrice.set(0, 0, 1);  
        maMatrice.set(0, 1, 5);  
        maMatrice.set(0, 2, 3);  
        maMatrice.set(1, 0, 4);  
        maMatrice.set(1, 1, 35);  
        maMatrice.set(1, 2, 0);  
        maMatrice.set(2, 0, 7);  
        maMatrice.set(2, 1, 18);  
        maMatrice.set(2, 2, 23);  
        System.out.println(maMatrice);  
  
  
        System.out.println("elem (1,1) =  " + maMatrice.get(1, 1));  
        System.out.println("ajout 10");  
        try {  
            maMatrice.ajoute(10);  
        } catch (MatricePleineException e) {  
            System.out.println("matrice plein");  
        }  
  
        System.out.println("getPosition");  
        Integer a = 5;  
        int[] position = new MatriceIterator<>(maMatrice).getPosition(a);  
        if (position != null) {  
            System.out.println(a + " : "+ position[0] + ", " + position[1]);  
        } else {  
            System.out.println("existe pas");  
        }  
        //itereteur  
        System.out.println("iteration");  
        MatriceIterator<Integer> monIterateur = new MatriceIterator<>(maMatrice);  
        while (monIterateur.hasNext()) {  
            System.out.print(monIterateur.next() + " ");  
        }  
        System.out.println();  
        System.out.println("remplace");  
        monIterateur.remplace(711);  
        System.out.println(maMatrice);  
    }```
wvew 