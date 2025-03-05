En Kotlin, 

==*array* devient *arrayOf*
*liste* devient *listOf*
*map* devient *mapOf*==

*Attention* : un array est **immuable** (change pas) alors qu'une liste non (on peut changer son nombre d'éléments) avec **mutableListOf**. mapOf implique une **clé** vers (to) une **valeur**

```kotlin
fun main(){
	val interestingThings = arrayOf("Js","C++","Kotlin")
}
```

```kotlin
fun main(){
	val interestingThings = listOf("Js","C++","Kotlin")
}
```

```kotlin
fun main(){
	val interestingThings = mapOf(
	1 to"Js",
	2 to "C++",
	3 to"Kotlin")
}
```
---
==**Méthodes de ArrayOf (à bâtir)**==

- **`size`**: Renvoie la taille de l'array.
```kotlin
val array = arrayOf(1, 2, 3) 
println(array.size) 
```
- **`get(index:Int)`**: Renvoie l'élément à l'index spécifié
```kotlin
println(array.get(1))
```
- **`set(index:Int, valeur: T)`**: Modifie l'élément à l'index en paramètre
```kotlin
array.set(1, 4)
```
- **`forEach`**: Exécute l'action spécifiée pour chaque élément de l'array.
```kotlin
val array = arrayOf(1, 2, 3) 
array.forEach { 
	println(it) //syntaxe de base
} // Sortie: 1 2 3

array.forEach{element -> 
	println(element) //syntaxe lambda
}
```
 **`forEachIndexed:
```kotlin
val array = arrayOf(1, 2, 3) 

array.forEachIndexed{index, element -> 
	println("$element est a l'index $index") //syntaxe lambda
}```

- **`map(transform: (T) -> R)`**`:
```kotlin
`val array = arrayOf(1, 2, 3) println(array.map { it * 2 }) // Sortie: [2, 4, 6]`
```

---
==**vararg**==

```kotlin

fun lireArray(vararg items:String){
	items.forEach{element->
		println("$array")
	}
}

fun main(){
	array = arrayOf("objet","verre","pot")
	lireArray(items = *array)
}

```