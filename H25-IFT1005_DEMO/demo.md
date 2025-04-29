

# Hamburger Menu

Le hamburger menu est une façon compacte d'afficher le menu dans un contexte ou le user est sur mobile (très fréquent de nos jours)

Il consiste à
- être caché en mode ordi / visible sur mobile
- faire apparaitre / disparaitre des options du menu

>Astuce : nativement on mettra 2 menu sur la page, on ne fera que manipuler une media query pour le logo

# mettre main qui change!!!




```javascript
function dropMenu(){
    let options = document.getElementById("drop-links");
    options.classList.toggle("hidden");
}
```

> trick pour aligner le texte au centre de la case : baliser les options du menu d'une div, elle aura `display: table` et les li `display:table-cell; vertical-align:middle`


# DOM : Mode Nuit persistant

Le mode nuit consiste à 

- **Sélectionner** ce qui doit changer de couleur (par exemple body)
- **Toggle** une classe qui écrasera le style défini par défaut
- **Enregistrer l'état** pour le garder persistant sur d'autres pages

#### Changement de mode

```javascript
function nightMode() {
/*
- background = section dont la couleur va changer
- nuit = booleenne qui sert d'etat (nuit ou jour)
*/
    let background = document.querySelector("body");
    background.classList.toggle("nuit");
    let nuit = background.classList.contains("nuit"); //v f
    localStorage.setItem("etat",nuit); //
    nightButton();
```

#### Event pour s'assurer de la persistance

```javascript
/*
- a chaque PAGE LOAD, on va verifier si l etat est true (mode nuit)
- si yep, on va add dans les classes du body le "nuit"
- on call le changement de texte du bouton
*/
document.addEventListener("DOMContentLoaded", () => {

    let background = document.querySelector("body");
    let estNuit = localStorage.getItem("etat")==="true";
    if (estNuit){
       background.classList.add("nuit");
    }
    nightButton(); //premier update du bouton au dem
    } 

);
```

#### Update du bouton (pour la cohérence, optionnel) 

```javascript
function nightButton() {

    let bouton = document.getElementById("nightmode-button");
    let nuit = document.body.classList.contains("nuit");
    if (nuit){
        bouton.innerHTML = "jour";
    }
    else{
        bouton.innerHTML ="nuit";
    }
}
```

