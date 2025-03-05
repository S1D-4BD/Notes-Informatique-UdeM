==**Fonction sans paramètres**==

```kotlin
fun getGreeting(): String{
	return "Hello Kotlin"
}
fun sayHello(): Unit{
	println("getGreeting")
}
fun main(){
	getGreeting()
	sayHello()
}
```

*fun getGreeting():String* :  Initialisation de la fonction getGreeting **sans** paramètres et qui **retourne** un String (donc **"Hello Kotlin"**) avec le ==:==
*fun sayHello(): Unit* : Initialisation de fonction sans paramètre qui ne **retourne rien** (Unit)


==**Fonction avec paramètres**==


```kotlin
fun sayHello(name:String){
	val msg = "Hello "+ name
	println(msg)
}
fun sayHelloBetter(name:String){
	val msg = "Hey $name"
}

fun sayHelloWithAge(name:String,age:Int){
	val msg = "Hey $name, you are $age years old"
}

fun main(){
	sayHello(name:"Sid")
	sayHelloBetter(name:"Sid")
	sayHelloWithAge(name:"Sid",age:22)
}

```