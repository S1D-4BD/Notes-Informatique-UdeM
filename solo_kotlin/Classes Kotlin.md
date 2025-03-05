```kotlin

(PREMIER DOC)
class Person(var _firstName:String,var _lastName:String) {
	fun sayHello(){
		println("Hello $_firstName $_lastName")
	}
}

fun main() {
	val client = Person("Peter","Jackson")
	client.sayHello()
}

```

**Exécution: initialisation d'un ==(donc Peter Jackson)== puis appel de la fonction / méthode sayHello qui nous imprime "Hello Peter Jackson"**
