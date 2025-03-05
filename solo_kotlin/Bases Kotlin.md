==**Fonction basique**==
```kotlin
fun main() {
  println("Hello World")
  //commentaire explicatif
}
```

*fun* : déclaration de fonction
	entre crochets on met ce que fais la fonction
*main()*: nom de la fonction
	entre parenthèses on met les paramètres (si c'est le cas)
*{ println ("Hello World")}* :  affiche sur une ligne le string "Hello World"
	pas besoin de mettre le ; à la fin
*//*  : commentaire explicatif

**Exécution: fonction qui affiche en console "Hello World"**

---
==**Variables et Values**==

```kotlin
var nom = "sid"
val nbr = 22

var université: String = "UdeM" // String spécifié
val année: Int = 1975 // Int
```

*var*: déclaration de variable pouvant être changée
*var*: déclaration de valeur ne pouvant PAS être changée

*ATENTION* : on peut **INITIALISER** une variable puis assigner une valeur, mais lorsqu'on initialise il faut **SPÉCIFIER LE TYPE**

---
```kotlin
val name = "sid"
val salutation = "salut "
println(salutation + name)
```

ici, le `+` sert à faire la concaténation des strings
**Exécution: fonction qui affiche en console "salut sid"**

---
==**Data Types**==
```kotlin
val pi : Double = 3.14
val age : Short = 2
val taille : Byte = 100
```

*Double*: Nombres à virgule très grands
*Byte*: Nombres entiers très petits **(-128 à 127)**
*Short*: Nombres entiers grands
Int: Nombres entiers très grands

---
==**Opérateurs**==

| ==OP== | ==Calcul==     | ==Exo==     |
| ------ | -------------- | ----------- |
| +      | Addition       | x + y       |
| -      | Soustraction   | x - y       |
| *      | Multiplication | x * y       |
| /      | Division       | ==x / y==   |
| %      | Modulo         | x % y       |
| ++     | Incrémente     | ==**++x**== |
| --     | Décrémente     | ==**--x**== |
| +=     | Init. plus 3   | x = x + 3   |
| -=     | Init. moins 3  | x = x - 3   |
| *=     | Init. fois 3   | x = x * 3   |
| /=     | Init. div 3    | x = x / 3   |
| %=     | Init. mod 3    | x = x % 3   |

*ATTENTION:* il n'y a **PAS** de distinctions entre division entière et division classique 

---
==**Booléens**==

| OP  | Condition                                 | Exo              |
| --- | ----------------------------------------- | ---------------- |
| ==  | Equal to                                  | x == y           |
| !=  | Not equal                                 | x != y           |
| >   | Greater than                              | x > y            |
| <   | Less than                                 | x < y            |
| >=  | Greater than or equal to                  | x >= y           |
| <=  | Less than or equal to                     | x <= y           |
| &&  | True if ==both== statements are ==true==  | x < 5 &&  x < 10 |
| \|  | True if ==one== of the statements is true | x < 5 \|\| x < 4 |
| !   | Reverse the result                        | ---              |
**Note**: *Exactement* comme Python et Java

---
==**Boucles If Else**==
```kotlin
var statut: Boolean = False
var clic : Boolean = True

if ((statut==True && clic==False) == True) {
	println("accepté")
}
else{
	println("refusé")
}
```

**Exécution: fonction qui affiche en console "refusé"**

---
==**Boucles While**==

```kotlin
var x: Int = 5
	while (x > 2){
		println(x)
		x-=1
	}
```
**Exécution: fonction qui affiche la valeur de x tant que x est supérieur à 2 (5,4,3)"**

==**Boucles For**==

*ATTENTION*: La boucle for nécessite un **range** pour itérer (un peu comme **Python**)
mais le premier et denier élément du range sont ==inclus==

```kotlin
for (i in 1..5){
	println(i)
}
```

*i* : index du range d'itération (**itérateur**)
*range d'itération*: 1-2-3-4-5

**Exécution: va imprimer les nombre de 1 à 5 chacun sur sa ligne**

---
==**When / Switch Case**==

```kotlin
fun main(){
	val jour = 4
	
	val result = when (Jour) {
	  1 -> "Lundi"
	  2 -> "Mardi"
	  3 -> "Mercredi"
	  4 -> "Jeudi"
	  5 -> "Vendredi"
	  6 -> "Samedi"
	  7 -> "Dimanche"
	  else -> "Non."
	}
	println(result)
}
```

*val jour* : Le user a choisi *l'entrée 4*
	on veux savoir c'est quel jour de la semaine qui lui est associé
*val result* : result est la fonction qui nous retournera le nom du jour du user
	C'est l'association que fera la fonction when (Jour) 
*->* : Opérateur d'Association entre *jour*  et les strings (noms) de chaque jour
*else* : résultat par défaut si aucun cas correspond à l'entrée

==**Arrays**==

```kotlin
fun main() {  
    val cars = arrayOf("Volvo", "BMW", "Ford", "Mazda")  
    println(cars.size)  
  
    for (j in cars){  
        println(j)  
    }  
    for (i in 0..3){  
        println(cars[i])  
    }  
}
```