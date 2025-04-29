# ALGO

La recherche dans un tableau de données **implique un tri** si on ne veux pas perdre notre temps; on risque d'augmenter linéairement le temps de recherche si les données ne sont pas triées.

Une méthode instinctive est de comparer 2 à 2 chaque élément; **si on a 128 éléments on compare chaque éléments aux autres**, pour tout les éléments existants, donc 128 * 128 en pire cas. On aura alors $16384$ comparaisons. 

- **Division récursive du tableau**
    - Le tableau est divisé en deux moitiés à chaque étape, jusqu’à obtenir des listes de 1 élément (automatiquement triées).
    - Le nombre de divisions nécessaires est $log2​(n)$, car chaque division divise la taille par 2.
- **Fusion des listes triées**
    - Les sous-listes triées sont fusionnées deux par deux à chaque niveau.
    - Chaque fusion nécessite n comparaisons au total pour ce niveau, car chaque élément est traité exactement une fois.
- **Total des comparaisons**
    - Avec $log_2(n)$ niveaux de division et n comparaisons par niveau, le tri fusion effectue  $nlog_2(n)$ comparaisons au total.

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

| **Situation**                           | **Tri recommandé**          | **Complexité moyenne** | **Description (Comment ça fonctionne)**                                                                                  |
| --------------------------------------- | --------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Tableau petit                           | Tri par insertion           | O(n²)                  | Parcourt chaque élément, insère chaque nouvel élément à sa position correcte dans la partie déjà triée du tableau.       |
| Presque trié                            | Tri par insertion           | O(n)                   | Fonctionne bien car les déplacements nécessaires sont minimaux dans un tableau presque trié.                             |
| Performance générale                    | Quicksort                   | O(n log n)             | Divise le tableau en deux parties autour d’un pivot, trie chaque partie récursivement, puis les combine.                 |
| Pire cas stable                         | Merge Sort                  | O(n log n)             | Divise récursivement le tableau en deux jusqu'à obtenir des sous-listes de 1 élément, puis fusionne en ordre croissant.  |
| Données uniformément réparties          | Bucket Sort                 | O(n)                   | Répartit les éléments dans des "paniers" selon une plage de valeurs, trie chaque panier, puis les concatène.             |
| Grands tableaux, mémoire limitée        | Merge Sort                  | O(n log n)             | Divise en sous-listes triées, puis les fusionne. Peut être implémenté pour utiliser moins de mémoire via des buffers.    |
| En place, faible mémoire supplémentaire | Quicksort                   | O(n log n)             | Ne nécessite pas de tableau auxiliaire : tout est trié directement dans le tableau d’origine en partitionnant.           |
| Stabilité requise                       | Merge Sort ou Counting Sort | O(n log n), O(n + k)   | Merge Sort est stable et trie récursivement. Counting Sort compte les occurrences des éléments, adapté pour des entiers. |

<div style="page-break-after: always;"></div>


---

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

| **Critère**              | **`List`** | **`ArrayList`**          | **`LinkedList`**                   |
| ------------------------ | ---------- | ------------------------ | ---------------------------------- |
| **Accès aléatoire**      | Oui        | O(1)  (très rapide)      | O(n)                               |
| **Ajout à la fin**       | Oui        | O(1)                     | O(1)                               |
| **Ajout au début**       | Oui        | O(n)                     | O(1)                               |
| **Suppression au début** | Oui        | O(n)                     | O(1)                               |
| **Mémoire utilisée**     | -          | Moins (tableau organisé) | Plus (références pour chaque nœud) |
| **Tri**                  | -          | Très rapide              | Plus lent                          |

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


<div style="page-break-after: always;"></div>


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
		this.dernier=dernier;	}
	private Noeud getNoeud( int idx ) {
		Noeud node = this.premier;
		for( int i = 0 ; i < idx; i++ ) 
			node = node.prochain; 
		return node; 	}
	
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
	}}}
```

<div style="page-break-after: always;"></div>


#### Constructeur de noeud

```java
public class Noeud{

	public int valeur;
	public int prochain;
//----------------------------------------//
	public Noeud(int valeur, int prochain){
		this.valeur = valeur;
		this.prochain = prochain;	}
//----------------------------------------//
private getNoeud(int idCondition){
	Noeud node = this.premier
	for(int i = 0, i< idCondition; i ++ ){
		node = node.getprochain();
	}	return node;
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
}

public static void main (String[] args){

	Noeud dernier = new Noeud(3, null);
	Noeud premier = new Noeud(4, null);
	Noeud deuxieme = new Noeud(2,null);
	premier.setProchain(deuxieme);
	deuxieme.setProchain(dernier);
	}}
```



---
#### Stack / Pile

L'abstraction de Pile est implémentée avec Vector pour le **push, pop, peek**

Soit l'arbre tel que 
1)             7
2)        {2} - {6}
3) {{4} {5}} - {{9} {1}}

pour **trouver** 9, si j'avais la liste {7,2,4,5,6,9,1} ça reviendrai à dire: 

>Est ce que 9 est au **milieu** de {7,2,4,5,6,9,1}?
>- Non,
>	- il est au **milieu** de {6,9,1} ?
>	- Oui, STOP

<div style="page-break-after: always;"></div>


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

==Servent à exécuter du code en cas de situation **anormale**==
- Entrée d'un périmètre négatif
- Un index non valide
- Un objet non existant ...
 
Dans le try, on insère le code qui peux potentiellement ne pas marcher (a cause d'une erreur humaine)
Dans le catch on spécifie l'erreur a attraper et on insère le code a exécuter en cas où

>Attention : les blocs catchs ne sont pas comme les switch-case, **dès que un est atteint, le reste est ignoré**. Il faut traiter les erreurs **enfant avant celle des parents**. Une ArithmeticException est un enfant de Exception, si on catch Exception avant ca ne marchera pas car on na pas l'occasion d'Attraper l'erreur, le programme crash

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
        }    }
// -----------------------------------------------------------------------//
    public static void lireFichier(String nomFichier) throws IOException {
        FileReader file = new FileReader(nomFichier);
        BufferedReader br = new BufferedReader(file);
        System.out.println(br.readLine());
        br.close();
    }     }
 ```

# exceptions

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

<div style="page-break-after: always;"></div>


#### Utiliser des exceptions vérifiées si** :

- L’erreur est **anticipée** et **récupérable** par le programme.
- Exemple : ouvrir un fichier, établir une connexion à une base de données.

#### Utiliser des exceptions non vérifiées si** :

- L’erreur résulte d’un problème **logique ou de programmation**.
- Exemple : accès à un tableau hors des limites, division par zéro.

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

<div style="page-break-after: always;"></div>


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

Le *problème* c'est qu'**on devra définir dans la classe Server** chaque évènement possible; idéalement on devrait **traiter les cas dans la classe main** On aurait :

```java
Server s = newServer("127.0.0.1", 1337);
s.addEventHandler(eventA);
s.addEventHandler(eventB);
s.addEventHandler(eventC);
//...
s.addEventHandler(eventRandomNumber);
```

Si on à 30 événements à gérer => 30 classes définies dans 30 fichiers éparpillés dans le projet fuck

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

<div style="page-break-after: always;"></div>


---
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

<div style="page-break-after: always;"></div>



```java
public class ExempleHierarchie extends Application {
    @Override
    public void start(Stage primaryStage) {      
        Label label = new Label("Bonjour, JavaFX!");  // Création des nœuds enfants
        Button button = new Button("Cliquez-moi!");
        VBox root = new VBox(); //Root Node (VBox)
        root.getChildren().addAll(label, button);
        
        Scene scene = new Scene(root, 300, 200); // Création de la scène
        primaryStage.setScene(scene);         // Ajout de la scène au stage
        primaryStage.setTitle("Hiérarchie JavaFX");
        primaryStage.show();
    }
    public static void main(String[] args) {
        launch(args);    }}

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

| Processeur 1                      | Processeur 2                      |
| --------------------------------- | --------------------------------- |
| Additionner somme première moitié | Additionner somme deuxième moitié |
#### Thread

Un thread = fils d'exécution d'instructions séquentielles (de base on en a toujours 1, le main)
Pour exécuter des threads on a besoin de quelque chose qui puisse les run, Runnable et des méthodes que les threads peuvent faire.

```java
@FunctionalInterface 
public interface Runnable { public void run(); }
```

```java
Thread t = new Thread(() -> { calculateSinusSum(numbers); })
t.start(); }                // Méthode appelée par le thread 
public static void sinusFirtPart(double[] numbers) { 
	double total = 0; 
	for (int i = 0; i < numbers.length / 2; i++) { 
	total += Math.sin(numbers[i]); 
} 
```

L'exécution est imprévisible. ils vont me calculer la somme, mais moche

<div style="page-break-after: always;"></div>


**Problème 1 : non synchronisation**
- **Solution :** Utiliser `thread.join()` pour mettre en pause le thread actuel jusqu'à la fin du thread spécifié.
- **Exemple :** Afficher "HeWo" après que les threads `he` et `wo` aient terminé.

```java
Runnable hello = () -> {
    System.out.print("H");    System.out.print("e");
};

Runnable world = () -> {
    System.out.print("W");    System.out.print("o");
};
public static void main(String[] args) {
    Thread t1 = new Thread(he);
    Thread t2 = new Thread(wo);
    t1.start();
    t2.start();

    try {
        t1.join(); // Attend que t1 finisse
        t2.join(); // Attend que t2 finisse
    } catch (InterruptedException e) {
        System.out.println("Interruption");
    }
}
```

**Problème 2 : interférences
- **Solution :** on utilise un **verrou (`lock`)** avec **`synchronized`** pour s'assurer qu'un seul thread peut exécuter un bloc de code critique à la fois.
-  Avant d'exécuter le code dans ce bloc, le thread doit **acquérir le verrou `lock`**.
    - Une fois qu'un thread entre dans ce bloc, les autres threads doivent **attendre** que le verrou soit libéré.
- **Exemple :** soustraire 1, puis add 1 (pour un total de 0)

```java
public void increment() { 
synchronized (lock) { c++; } 
}
```

**Problème 3: deadlock
- **Solution :** on utilise un pas juste 1**verrou (`lock`)** mais on en instancie plusieurs 
- private final Object lockC1 = new Object(); 
- private final Object lockC2 = new Object();