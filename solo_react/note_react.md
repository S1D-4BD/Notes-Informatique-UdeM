Adresse du serveur : http://localhost:5173/

Pour entrer: cd projet_path -> npm run dev

# UI - Composants simples

==**Composant** : Une fonction qui renvoie de l'interface user vers une App==

```javascript
function Header(){
    return(
        <header>
        <h1>Mon App</h1>
        <nav>
            <ul>
                <li><a>Home</a></li>
                <li><a>About</a></li>
                <li><a>Map</a></li>
            </ul>
        </nav>
        <hr></hr> //ligne simple
        </header>
    );
}
export default Header
```

- fonction est la **composante** (on parle de App)
- return est ce **qu'on voit** (la div, le header et le paragraphe)
- export default **Header** permet à React d'**utiliser** cette composante comme un lego dans **App** 

**App** : le main contrôleur, on **importe les composants** pour les afficher

```Typescript
import Header from "./Header"

function App() {
  return(
    <Header></Header>
  );
}
export default App
```

>[!NOTE]
>En React, on ne return qu'une seule balise; si je voulais afficher 2 composants, je doit les entourer d'une paire de balises vide <></>

>Pour ajouter du Javascript en React, on met les **script entre les balises { }**

---
# Props

permet de "personnaliser les composants" 

```typescript
composant
function Header(props){
    return(
        <header>
        <h1>Bonjour {props.name} !</h1> // mettre en param dans app le nom
        </header>
    );
}
export default Header
```

dans app

```typescript
...
<div className="wrapper">
      <Header name="Utilisateur"></Header> //le param name dans Header
      <div className = "cardHolder">
        <Cardholder></Cardholder>
      </div>
      <Footer></Footer>
    </div>
```

>[!note]
>On peut déstructurer les props en indiquant dans la fonction chaque paramètre entre { }


```typescript
function Header({name,surname}){ //props déstructuré
    return(
        <header>
        <h1>Bonjour {name} {surname} !</h1> //chaque param dans son {}
        </header>
    );
}
export default Header
```

```typescript
App
...
<Header name="Utilisateur" surname="One"></Header> //les params en question
```

>==ATTENTION, les props sont **immuables**==

---
# Arrays 

Mapping : une bijection entre 2 ensembles, le premier étant l'array original, et le deuxième étant la transformation
 on map les éléments de l'array fruit comme une Collection de binômes (valeur, clé)
=> veux dire "**pour chaque chose à gauche, tu fais ce qu'il y a à droite**"  chaque li aura comme valeur {fruit} l'élément à l'index égal à la clé retrouvée dans l'array


```typescript
const fruits = ['Pomme', 'Banane', 'Cerise'];

function ListeFruits() {
  return (
    <ul>
      {fruits.map((fruit, index) => (<li key={index}>{fruit}</li>))}
    </ul>
  );
}
```

---

# Conditionnels

pour afficher ou exécuter des éléments en fonction d'un booléen

>[!NOTE]
>C'est une mauvaise pratique de retourner plusieurs choses (avoir plus de 1 return statement), on utilise les **opérateurs ternaires**

```java
function Conditionnal(){
    const display = false;
    return  (display ? <h1>Oui</h1> : <h1> Non </h1>);
    /*si display == true -> affiche Oui, sinon affiche Non*/
}
export default Conditionnal
```