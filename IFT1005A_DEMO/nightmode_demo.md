
# DOM : Mode Nuit persistant

le mode nuit consiste à 
- sélectionner les sections dont les couleurs doivent changer
- toggle la classe "dark" qui va override les attributs de jour ainsi que le bouton de toggle
- enregistrer l'état pour update les pages prochaines via event
- un EventListener va écouter chaque changement de page ( **DOMContentLoaded** ) afin d'appliquer l'état enregistré avant

#### Sélection du mode

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
### Toggle switch pour le mode nuit

Le principe d'un toggle provient du checkbox et de ses 2 états possibles : activé ou non. Pour chaque checkbox vient un label qui sert de récipient pour la question. Ici, on va jouer sur l'apparence du label pour le faire ressembler au socle d'une switch, et la checkbox comme switch elle-même

#### Initialisation du label : socle

```css
label { 
position: relative; 
width: 65px; 
height: 30px; 
border-radius: 100px; 
background: linear-gradient(180deg, rgb(235, 235, 235), rgb(203, 203, 203)); cursor: pointer; 
transition: 0.35s; 
}
```

C'est le conteneur de la bille qui servira de switch. On verra une bille se déplacer d'un coté à l'autre aux clic, et le background changera de couleur (à une vitesse de 0.35 secondes) en fonction du mode choisi.

position relative : on veux que la bille soit positionnée en fonction du socle

#### Initialisation d'un pseudo élément : bille de switch

```css
label::after{
    position: absolute;
    content:"";
    top: 2px;
    left:5px;
    width: 25px;
    height:25px;
    background: linear-gradient(180deg,rgb(255, 157, 0), rgb(206, 127, 0));
    border-radius:50% ;
    transition:0.35s ;

}
```


- Puisque la bille n'est pas dessinée via le HTML (on parle de CSS pur), on le qualifie de **pseudo élément**. Comme il est utilisé dans le label, on l'instancie via ``label::after``, after est utilisé puisqu'on veux quil soit positionné *après* notre label.

- position absolute puisque c'est la bille qui est contenue dans le socle

#### Input : élément de contrôle

c'est la checkbox, lui qui permet une vérification de l'état (est ce que c'est coché ou non?). Ici il doit être fonctionnel mais **non visible** (on ne veux pas voir une boite à cocher, juste la bille)

```css
input{
    width:0;
    height:0;
    visibility: hidden;
    display: none
}
```
#### éléments après toggle (checked)

Après clic, le socle et la bille doivent changer d'apparence. Comme c'est lorsque l'input est ``checked`` qu'on voit ce changement, on spécifie ``input : checked`` devant label et ``label :: after`` pour différencier les 2 situations

```css
input:checked +label{
    background: linear-gradient(180deg,rgb(112, 112, 112), rgb(34, 34, 34));
}
input:checked +label:after{
    background: linear-gradient(180deg,rgb(255, 225, 0), rgb(248, 239, 171));
    left:60px;
    transform: translateX(-100%);
}
```

#### Persistance du mode nuit

Lorsqu'on change de page, on souhaiterais que le toggle reste **pareil** entre les pages. C'est une nouvelle fonction qu'on ajoute

```javascript
function updateToggle(isDark) {
    let toggle = document.getElementById("toDarkmode");
    toggle.checked = isDark; // true pour "activé", false pour "désactivé"

}
```