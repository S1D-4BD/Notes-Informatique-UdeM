```html
<!DOCTYPE html>

<head>
    <title>demo svg</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="fenetre">
        <svg class="monsvg" width="400" height="600" viewBox="-200 -300 400 600">
        <defs>
            <g id="arbre-droite">
                <rect width="50" height="100" x="-25" y="200" stroke="brown" fill="brown"/>
                <rect width="25" height="100" x="-25" y="200" stroke="#361b00" fill="#361b00"/>
                <polygon points="-100,250 100,250 0,0" stroke="#045000" fill="#045000"/>
                <polygon points="-100,200 100,200 0,-100" stroke="green" fill="green"/>
                <!--<use href="#boule" x="31.5" y="-2.5"/>
                <use href="#boule" x="-36.5" y="-2.5"/> -->
            </g>
            <g id="carreau">
            </g>
            <g id="arbre-gauche">

                <rect width="50" height="100" x="-25" y="200" stroke="brown" fill="brown"/>
                <rect width="25" height="100" x="0" y="200" stroke="#361b00" fill="#361b00"/>
                <polygon points="-100,250 100,250 0,0" stroke="#045000" fill="#045000"/>
                <polygon points="-100,200 100,200 0,-100" stroke="green" fill="green"/>
            </g>

            <g id="sol">
                <circle width="300" height="300" cx="150" cy="150" r="150" fill="beige"/>
            </g>

            <g id="boule">
                <circle width="3" height="3" cx="1.5" cy="1.5" r="1.5" fill="white" />
            </g>
        </defs>

        <circle width="400px" height="400px" cx="50" cy="50" r="25" fill="#ff6200"/>

        <use href="#carreau" />
        <use href="#sol" x="-150" y="4"transform="scale(10)" />
        <use href="#arbre-droite" transform="translate(-70,-10) scale(0.3)" />
        <use href="#arbre-droite" transform="translate(70,0) scale(0.2)" />
        <use href="#arbre-gauche" transform="translate(-10,10) scale(0.11)" />
        <use href="#arbre-gauche" transform="translate(190,10) scale(0.7)" />
        <use href="#arbre-droite" transform="translate(-190,-50) scale(1.2)" />

        <use href="#boule" transform="translate(-140,-170)" />
        <use href="#boule" transform="translate(-100,-190)" />
        <use href="#boule" transform="translate(-70,-190)" />    
        <use href="#boule" transform="translate(-35,-190)" />
        <use href="#boule" transform="translate(0,-150)"/>
        <use href="#boule" transform="translate(50,-230)"/>
        <use href="#boule" transform="translate(70,-180)"/>
        <!--<use href="#boule" x="185" y="-210" /> -->
    </svg>
        <!--<div class="coin-bd">
            <svg class="carreau"width="190" height="290" viewBox="-100 -150 200 300">
            </svg>
        </div>
        <div class="coin-bg">
            <svg class="carreau"width="190" height="290" viewBox="-100 -150 200 300">
            </svg>
        </div> -->
    </div>
</body>
</html>
```