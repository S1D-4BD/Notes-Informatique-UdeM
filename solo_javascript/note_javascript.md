---

---

---
# Introduction

Javascript est un langage puissant capable de rajouter des réactions à des évènements
- ==const== : pour les valeurs qui ne **changent pas**
- ==let== : pour les valeurs qui **changent (variables) **

>Attention, on **initialise 1 seule fois une variable avec let**, on ne **peux pas utiliser la variable avant** de l'avoir initialisé

#### Types

| Type      | Syntaxe                            |
| --------- | ---------------------------------- |
| String    | entre `" "` ou `' '`               |
| Number    | Nombre entier/décimal              |
| Boolean   | `true` ou `false`                  |
| Bigint    | `12345678901234567890n`            |
| Object    | `{ key: value, key2: value2 ... }` |
| Symbol    | `Symbol('description')`            |
| Null      | `null`                             |
| Undefined | `undefined`                        |

---
### Opérateurs logiques

`A && B` vaut vrai <==> A et B sont “vrai simultanément”
`A || B` vaut vrai <==> A ou B ou les deux sont “vrai”
`A == B` A vaut B ?
`A <= B` A inférieur ou égal à B?
`A===B` A = B ET sont de **même** type?
`condition? A:B` condition vérifiée? Retourne a si vrai, b si faux
`result = A ?? B` retourne B si A est **null**

> "2"<"12" est **faux** car alphabétiquement le "1" de "12" vient avant "2"

| Type            | Syntaxe                                           |
| --------------- | ------------------------------------------------- |
| A && B          | A et B sont “vrai simultanément”                  |
| A \| \| B       | A ou B ou les deux sont “vrai”                    |
| A == B          | A vaut B ?                                        |
| A <= B          | A inférieur ou égal à B?                          |
| A === B         | A = B ET sont de **même** type?                   |
| condition? A:B  | condition vérifiée? Retourne a si vrai, b si faux |
| result = A ?? B | retourne B si A est **null**<br>                  |

---
# Structure d'une fonction

**Une fonction est un bloc d'instructions paramétrées ou non exécutée à l'appel**

```javascript
function(param){
	directive1;
	directive2;
	return reponse;
}
```

**Exemple :**

```javascript
function multiplyBySeven(b) {
	let a = 7
	return a*b
}
function add(a, b) {
	return a+b
}
```



---
# Arrays
# Méthodes de print

On peut imprimer une constante ou une variable via la méthode `console.log(const ou variable)` en faisant un print formatté 
#### Print formaté

```javascript
console.log (' ${variable} texte ${autre variable}')
```

```javascript
let name = "Bob";
let age = 34;

console.log("${name} a ${age} ans")
//Bob a 34 ans
```

---
# if-else/ switch

Structure du if-else :

```javascript
if(a>b){
	console.log("pas egaux");
}
else if(b>a){
	console.log("pas egaux")
}
else{
	console.log("egaux");
}
```

ou sinon en plus court

```javascript

if((a>b)||(b>a)){
	console.log("pas egaux");
else{
	console.log("egaux");
}
```

#### switch

```javascript
switch(case a verif){
	case 1://truc
		break;
	case 2:
	case 3://truc pour 2 et 3
		break;
	default://truc de base
}
```

>Pas besoin du break à la fin, et default peux ne pas nécessairement être à la fin du switch

---
# LOOPS

#### for
```javascript
for (let i = 0; i<condition; i++){
	console.log("eille");
}
```

#### for in
```javascript
let txt = "";
const myarray = [1,2,3,4];
for (let value in array){
	txt+= myarray[value];
}
```

>à ne pas utiliser si l'ordre est important
#### while
```
while()
```
---



---
# DOM

Le DOM  est la structure en arbre servant de modèle d'une page web; on dessine la "carte" du site, les pages qu'on peux visiter a partir d'une, les pages enfants, les pages parents etc...

**Méthodes DOM** : actions qu'on peut faire sur des éléments HTML
**Propriétés DOM** : valeurs des éléments HTML (modifiables)

**==Dans le DOM, on souhaiterai pouvoir accéder à des éléments, accéder à leur contenu puis appliquer des transformations==**

### Sélection d’éléments

Il existe **quatre** méthodes pour sélectionner des éléments du DOM :

- `getElementById`    ( via #, est unique)
- `getElementsByTagName` (via balise HTML)
- `getElementsByClassName` (via "class")
- `querySlector` et `querySelectorAll` (spécial)

```javascript
const a = document.getElementById("form1");
const b = document.getElementByTagName("body");
const c = document.getElementByClassName("my-class"); /*tout ces classes*/
const d = document.querySelector("my-class span"); /* premier spans dans my-class
```

### Parcourir les éléments:

- `parentNode`
- `childNodes`
- `firstChild`, `lastChild`
- `nextSibling`, `previousSibling

```javascript
const lien = document.querySelector('div p a');
const leSpan = lien.parentNode;
```

## Lire le contenu

3 méthodes pour lire du contenu :
- `innerText`
- `innerHTML`
- `textContent`


On programme avec le paradigme Orienté Objet ; on **call** des méthodes avec le " . " en cascade sur un "objet" et on **set** des propriété

#### exemple : changement de contenu dans une balise

```java
<p id ="demo">"Salut"</p>

...

<script>
document.getElementById("demo").innerHTML = "Hello";
</script>

...
```

On **récupère** le paragraphe avec l'id demo via la méthode getElementById, puis on **set** le contenu du paragraphe avec l'id = "démo" via innerHTML au string "Hello"

>getElementById = méthode
>innerHTML = propriété

truc cool : localStorage

---

### **1. Sélection des éléments**

| **Méthode**             | **Description**                                      | **Exemple**                              |
| ----------------------- | ---------------------------------------------------- | ---------------------------------------- |
| `getElementById()`      | Sélectionne un élément par son ID.                   | `document.getElementById('demo');`       |
| `querySelector()`       | Sélectionne le premier élément = à un sélecteur CSS. | `document.querySelector('.myClass');`    |
| `querySelectorAll()`    | Sélectionne tous les éléments = à un sélecteur CSS.  | `document.querySelectorAll('div');`      |
| `getElementByClassName` | Via classe name                                      | `document.getElementByClassName('col');` |
### **2. Modifier le contenu des éléments**

| **Méthode/Propriété** | **Description**                                  | **Exemple**                                     |
| --------------------- | ------------------------------------------------ | ----------------------------------------------- |
| `innerHTML`           | Modifie ou obtient le contenu HTML d’un élément. | `element.innerHTML = '<strong>Hello</strong>';` |
| `textContent`         | Modifie ou obtient le texte brut d’un élément.   | `element.textContent = 'Hello';`                |
| `parseInt`            | Change le innerHTML en int pour des calculs      |                                                 |
### **3. Modifier les classes des éléments**

| **Méthode**          | **Description**                                                | **Exemple**                              |
| -------------------- | -------------------------------------------------------------- | ---------------------------------------- |
| `classList.add()`    | Ajoute une classe à un élément.                                | `element.classList.add('newClass');`     |
| `classList.remove()` | Supprime une classe d’un élément.                              | `element.classList.remove('oldClass');`  |
| `classList.toggle()` | Ajoute ou supprime une classe selon qu’elle est déjà présente. | `element.classList.toggle('highlight');` |
### **4. Modifier les attributs**

|**Méthode**|**Description**|**Exemple**|
|---|---|---|
|`setAttribute()`|Définit ou modifie un attribut d’un élément.|`element.setAttribute('class', 'newClass');`|
|`getAttribute()`|Récupère la valeur d’un attribut d’un élément.|`const src = element.getAttribute('src');`|
|`removeAttribute()`|Supprime un attribut d’un élément.|`element.removeAttribute('class');`|
### **5. Ajouter, supprimer ou remplacer des éléments**

|**Méthode**|**Description**|**Exemple**|
|---|---|---|
|`createElement()`|Crée un nouvel élément HTML.|`const div = document.createElement('div');`|
|`appendChild()`|Ajoute un élément enfant à un parent.|`parent.appendChild(child);`|
|`remove()`|Supprime un élément directement (sans parent).|`element.remove();`|
|`replaceChild()`|Remplace un élément enfant par un autre.|`parent.replaceChild(newChild, oldChild);`|
### **6. Gérer les événements**

| **Méthode**             | **Description**                                    | **Exemple**                                                         |
| ----------------------- | -------------------------------------------------- | ------------------------------------------------------------------- |
| `addEventListener()`    | Ajoute un gestionnaire d’événement à un élément.   | `element.addEventListener('click', () => console.log('Clicked!'));` |
| `removeEventListener()` | Supprime un gestionnaire d’événement d’un élément. | `element.removeEventListener('click', callback);`                   |
### **7. Autres utilisées**

| **Méthode**               | **Description**                                      | **Exemple**                                     |
| ------------------------- | ---------------------------------------------------- | ----------------------------------------------- |
| `focus()`                 | Met le focus sur un élément (comme un champ texte).  | `input.focus();`                                |
| `blur()`                  | Retire le focus d’un élément.                        | `input.blur();`                                 |
| `getBoundingClientRect()` | Retourne les dimensions et la position d’un élément. | `const rect = element.getBoundingClientRect();` |

---

#### Exemple : Compteur 

```javascript
<script>
    function add(){
        let a = parseInt(document.getElementById("count").innerHTML);
        let b = a + 1 ;
        document.getElementById("count").innerHTML = b ;
    }
    function sub(){
        let a = parseInt(document.getElementById("count").innerHTML);
        let b = a - 1 ;
        document.getElementById("count").innerHTML = b ;
    }
    function reset(){
        document.getElementById("count").innerHTML = 0;
    }
</script>
```

HTML: 

```html
<div class="container">

    <div class="reponse">
        <p id="count">0</p>
    </div>
    <div class = "container_button">
        <button onclick="sub()"> - 1 </button> <!--au click on call  sub()-->
        <button onclick="add()"> + 1 </button> <!--au click on call  add()-->
    </div>    
    
</div>
```


>![NOTE]
>Choses à add dans mes notes :
>- DomEvents
>- css var
>- linear gradient
>- css place-item
>- drag and drop
>-  ... operateur
# Évènements: bonus


# DOM : Mode Nuit persistant

le mode nuit consiste à 
- sélectionner les sections dont les couleurs doivent changer
- toggle la classe "dark" qui va override les attributs de jour
- enregistrer l'état pour update les pages prochaines via event
- un EventListener va écouter chaque changement de page ( **DOMContentLoaded** ) afin d'appliquer l'état enregistré avant

#### Sélection

```javascript
function darkMode() {

/*
- body = section dont la couleur va changer
- button = celui qui call la fonction (et informe du mode présent)
- isDark = booleenne qui sert d'état (nuit ou jour)
*/

    let body = document.querySelector("body");
    let isDark = body.classList.toggle("container_dark"); 
    updateDarkModeButton(isDark); 
    //appel de fct de changement de texte
    
    localStorage.setItem("etat", isDark);
    //on garde l'etat dans le local storage en tant que tuple

}

```

```javascript
/*
- bouton
*/

 function updateDarkModeButton(isDark) {

    let button = document.getElementById("toDarkmode");
    switch (isDark) {
        case true:
            button.innerHTML = "Mode Jour";
            break;
        default:
            button.innerHTML = "Mode Nuit";
            break;
    }
}
```
EventListener 

```javascript

/*
- a chaque page load, on va verifier si l etat est true (mode nuit)
- on va add dans les classes du body "container_dark"
- on call le changement de texte du bouton
*/
document.addEventListener("DOMContentLoaded", () => {
    if (localStorage.getItem("etat") === "true") { 
        document.body.classList.add("container_dark");
    }
    updateDarkModeButton(document.body.classList.contains("container_dark"));
});
```

#### Ajout personnel : garder le compte dans différentes pages après chaque clic de bouton

```javascript 
function keepCount(){

    let a = document.getElementById("count");
    let b = a.innerHTML;
    localStorage.setItem("countUpdate", b);
}

document.addEventListener("DOMContentLoaded", () =>
{
    let reponse = document.getElementById("count");
    let update = localStorage.getItem("countUpdate");

    if (update !== null) {
        reponse.innerHTML = update; // Mise à jour correcte
    }
}
);
```


# Asynchrone
# API