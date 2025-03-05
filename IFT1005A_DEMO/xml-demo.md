
---
### Différences fondamentales à noter entre HTML et XML :

- **XML** met l'emphase sur la ==description des données et son transport==
- **HTML** met l'emphase sur ==ce à quoi ressembleront ces données==
### Analogie : Magasin

- XML serait l'ensemble des *articles* d'un magasin
	- Il renseigne sur les noms des article, leur localisation et le cout 
	- Il est destiné aux **managers**
	- Il est **fonctionnel**
	- Un client aurait de la **difficulté** à comprendre le XML en raison de la quantité d'informations qui ne **lui sont pas nécessairement utiles**

>[!Exemple conceptuel]
>- Item #35: 
>- nom : tcf_ampoule_800923
>- prix : 4
>- localisation : R4
>- quantité en stock : 80

- HTML est le site web **présenté aux clients**
	- Il est destiné à être **compris par le client** 
	- Il est **esthétique**
	- Un manager ne **pourrait pas gérer le magasin** seulement avec une présentation esthétique

>[!Exemple conceptuel]
> **Addison Électronique**     | **accueil | menu | contact**
>- ---
>- **Ampoule**
>- 4.00$ 
>*disponible*

---
### Quelques règles à retenir

- **Commencez toujours par un ==prologue**== via ==`<?xml version="1.0" encoding="UTF-8"?>`==, c'est ainsi que vous allez assurer une cohérence dans la version de xml et l'encodage 
- **Respectez la structure XML**, ça veux dire des ==balises qui ne se **chevauchent pas** et qui sont **fermées correctement** ==
- **Privilégiez une ==hiérarchie générale -> spécifique==** avec des noms de balises simples à comprendre
- **Ajoutez des commentaires** pour expliquer votre fichier via ==``<!-- blabla -->`==
- ==**Encodez** les caractères spéciaux==, même si l'encodage est UTF-8, c'est par sécurité
### Exemple: Code XML, organiser les données d'un magasin

>[!Hiérarchie général/spécifique]
> - magasin (racine) -> articles
> - article -> [nom + prix + rangée + stock]


```XML
<?xml version="1.0" encoding="UTF-8"?>
<magasin>  
    <article id="35"> <!-- c'est quoi ce truc?? -->
        <nom>Ampoule</nom> 
        <prix>4</prix>
        <rangee>4</rangee>
        <stock>0</stock>
    </article>

	<article id="36">
	    <nom>Moteur électrique</nom>
	    <prix>30</prix>
	    <rangee>9</rangee>
	    <stock>500</stock>
	</article>
</magasin>

```

>[!Remarque]
> C'était quoi l'id mentionné plus haut? C'est ce qu'on appelle un ***attribut***, pour nous permettre de **différencier des balises de même nom mais dont l'information contenue est différente**

Nous avons un ``<magasin>`` ayant 2 ``<articles>``, chacun contenant le **même type de données**, soit le ``<nom>`` , ``<prix>``,  ``<rangee>``,  ``<stock>``, mais ==dont **les valeurs des données** est *différent*==
 
Avec ==l'attribut id== (ça aurait pu être un autre nom que **id**) nous savons que c'est l'article de nom `Ampoule` qui est indisponible en stock 

---
### Code XML/XSLT: magasin d'articles
#### XSLT : afficher XML sous forme de page HTML

Comme on souhaiterait que les clients puissent consulter les articles **clairement**, XML doit être stylisé en une page HTML compréhensible via XSLT

>**Attention :** En XSLT, vous ne faites que fournir les **directives** de mise en forme et d’apparence à travers des ==templates==. Si un template est défini pour une section répétée, **il suffit de le référencer une seule fois**. Avec ==`match`==, XSLT chargera automatiquement **toutes les données associées**

#### Structure de début pour le fichier XSLT (style.xsl) :  

```XML
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <!-- ici on va mettre notre code-->
</xsl:stylesheet>

```

>**Attention**: Il est important de comprendre que nous codons en templates; un template s'occupe d'une balise

#### Template du magasin

Soit un magasin avec un titre et des articles. On indique dans le template qu'on stylise le contenu de magasin comme ceci: 

==``xsl:template match="magasin">``==
	`structure du magasin, on se soucie pas de la structure des articles`
``</xsl:template>``

**On indique dans le code aussi que les ``articles`` seront stylisé selon un autre template**

Pour **==référer==** à un template imbriqué dans un template parent (comme on remarque pour magasin et article) on procède comme ceci:

==``xsl:template match="magasin">``==
	`structure du magasin
		==`<xsl:apply-templates select="article" />==
``</xsl:template>``

>On a **fermé** la balise de référence à un template enfant avec **un slash en fin de nom de balise**

```XML
<xsl:template match="magasin"> <!-- template:magasin-->
	<html>
		<body>
		   <header> Addison Électronique</header>
		   <xsl:apply-templates select="article" /> <!-- REF de template:article-->
		</body>
	</html>
</xsl:template>
```
#### Template d'un article 

Soit la présentation voulu allant ainsi : 
- un titre en gras pour le nom de l'article
- le prix écrit en paragraphe simple

Pour accéder au **contenu d'une balise**, nous suivons la syntaxe comme ceci : 
==`<xsl:value-of select="balise-contenant-linfo" />`==

```XML
<xsl:template match="article">
	<div>
		<h1> 
			<b><xsl:value-of select="name" /></b> 
		</h1>
		<p> 
			<xsl:value-of select="prix" />
		</p>
	</div>
</xsl:template>
```

>Attention: **value-of** vous donnera le texte pur contenu dans la balise, si vous avez des balises imbriquées elle ne seront pas affichées
#### Lier XSLT et XML

Avant d'en finir, vous devez référencer le fichier XSLT dans le fichier XML entant que "stylesheet". Cette référence permet à votre browser (Chrome, Firefox, Brave etc.) de lire les données XML et d'utiliser le fichier XSLT pour générer la page HTML stylisée.

Dans le fichier XML vous allez écrire juste après le prolog :
`<?xml-stylesheet type="text/xsl" href="nom-fichier-xsl.xsl"?> `

---
