
13 juin intra 16H30 1140 AA(25%)
29 juillet final 15H30 1140 AA (30%) **(50% DS)**
2 Projets (20%) (25%)
feuilles de notes =
# Réseaux Informatiques début (?)

## Why un modèle en couches ?

Les réseaux informatiques utilisent un **modèle en couches** pour structurer la communication entre machines. Chaque couche a un rôle **précis**, **isolé**, et **complémentaire** aux autres

### Idée de base/ Intuition

Envoyer des données c’est une série d’actions coordonnées *spécialisées*

**Exemple : envoyer une lettre**
-  Écrire le message -> contenu
-  Le mettre dans une enveloppe -> encapsulation
-  Ajouter l’adresse -> routage
-  Le confier à un service postal -> transport

###  Avantages

- **Modularité/ logique en blocs** : on peut modifier une couche sans toucher aux autres
- **Compatibility** : différents systèmes peuvent fonctionner ensemble
- **Précis** : chaque couche = des responsabilités précises unique à elle

---

##  Le modèle OSI (OLD) vs TCP/IP (maybe good là)

| Couche OSI           | Fonction principale                          | TCP/IP équivalent  |
| -------------------- | -------------------------------------------- | ------------------ |
| 7 Application        | Dialogue avec l'utilisateur (ex: HTTP, SMTP) | Application        |
| 6 Présentation       | Encodage/décodage (ex: chiffrement)          | (souvent intégrée) |
| 5 Session            | Gestion de sessions (peu utilisée)           | (souvent intégrée) |
| 4 Transport          | Fiabilité (ex: TCP, UDP)                     | Transport          |
| 3Réseau              | Routage (ex: IP)                             | Internet           |
| 2 Liaison de données | Adresse MAC, commutation                     | Accès réseau       |
| 1 Physique           | Transmission électrique ou optique           | Physique           |

>  Le modèle **TCP/IP** est une ==simplification== pragmatique du modèle OSI

---

##  Accéder à une page web via HTTP (terminal style)

**JE veux accéder à une page web**

1.  **HTTP (application)** -> Le navigateur demande "je veux la page `/index.html`"
2.  **TCP (transport)** -> S’assure que les paquets arrivent complets et dans le bon ordre
3.  **IP (réseau)** -> Trouve l’adresse du serveur et le chemin pour y aller
4.  **Liaison + Physique** -> Transmission réelle (ondes, fibre, cable)

---
##  Couches et ports

Pour différencier les services qui tournent sur une même machine, on utilise des **ports (service)**

| Protocole | Port standard | Description                   |
| --------- | ------------- | ----------------------------- |
| HTTP      | 80            | Web pas wow                   |
| HTTPS     | 443           | Web sécurisé                  |
| SMTP      | 25            | Envoi de courriels            |
| IMAP      | 143           | Lecture distante de courriels |
| FTP       | 21            | Transfert de fichiers         |
| ==DNS==   | 53            | bref                          |

> **Les ports sont gérés par la couche transport (make it make sense, ports = service wtf**

---

##  URI, URL et HTTP

### URI (Uniform Resource Identifier)

C’est une **chaîne standardisée** pour identifier une ressource

**Exemple: isbn-9780131103627**
- Je peux nommer un livre comme ca dans une database
- Pas possible de right-click et de visiter la bibliothèque qui possède le livre
### URL (Uniform Resource Locator)

C’est une URI qui **localise** une ressource

**Exemple :**
 https://www.exemple.com/dossier/page?nom=toto#ancre = URL
- Pas utile dans une database
- On PEUT right-click et visiter la bibliothèque qui possède le livre

| Élément        | Fonction                                    |
|----------------|---------------------------------------------|
| `https`        | Protocole utilisé                           |
| `www.exemple.com` | Nom d’hôte (résolu via DNS)             |
| `/dossier/page` | Chemin vers la ressource                   |
| `?nom=toto`    | Paramètres                                 |
| `#ancre`       | Ancre dans la page                         |

---
## DNS – Trouver une adresse IP

Le **DNS (Domain Name System)** traduit un nom (ex: `www.iro.umontreal.ca`) en une **adresse IP**.

**Navigateur -> DNS -> IP -> Connexion TCP -> HTTP -> Réponse**
###  Processus de résolution

1.  Vérifie le cache DNS local
2.  Si absent, consulte :
   - Serveur racine (indique `.ca`)(A-M)
   - Serveur TLD `.ca` (indique `umontreal.ca`)
   - Serveur autoritatif `umontreal.ca` (donne l'IP)

>  Commandes utiles  pour trouver le serveur dns:
> - `scutil --dns` (Mac)
> - `ipconfig /all` (Windows)

Les noms de machine doivent être sous la forme de ***Fully Qualified Domain Name***
www.google.com.

il y a un point à la fin, lecture de droite à gauche
>www= nom de machine
  google = nom de domaine ou se trouve la machine
. com = nom de domaine plus haut niveau

DNS = système client/serveur
Serveur= ordinateur qui a une appli qui roule en permanence, et qui écoute sur un port
échanges d info sur TCP

Structure de recherche des domaines (TLD = top level domain)
.ca etc = tld

![[DNS_structure.png]]

- 13 serveurs racine (za3ma)
- évite trafic, mais plein
Pourquoi?

Alors si ces serveurs tombent en panne alors on évite la galère. Les TLD il contiennent la liste de tout les domaines de plus haut niveau ET C'EST QUI LE DNS QUI SOCCUPE DE CES IP

==chacun contient la liste des serveurs DNS qui contient les domaines en dessous de lui==

cira (.qc.ca.) ils ont dit "pour tout ce qui es termine par umontreal.ca allez voir ces 2 ordi la"
la délégation se lis de droite à gauche
- umontrea.ca s'occupe de iro.umontreal.ca
### domaine vs zone

domaine.com = fini en .com (juste un nom, otut ce qui termine pareil = meme domaine)
++zones dans 1 domaine

cira gère .ca
udem qui gère umontreal.ca
diro qui gère iro.umontreal.ca

**C'est un fichier texte qui est lu en permanence qui donne les ip et leur DNS**

pour que .ca délègue, on va avoir un glue record, qui va coller (les flèches colorées du diagramme)

des que jme connecte on me fourni des ip de dns, je vais ask un des x serveurs quon ma fourni

A = c est quoi ipv4?

DNS cache = DNS récursif (qui garde en mémoire aussi)
>requêtes récursives = je pose la question, débrouille toi pour me donner la bonne 
>requêtes itératives = il travaille jusqu'à donner la meilleure réponse possible pour aider (pas la bonne, mais une indication)

C'est un serveur qui ne connait que 13 serveurs racine et recherche dynamiquement les autres DNS : meme si on change un des adresse des DNS, il va s ajuster

`nslookup`

---
##  HTTP – Protocole de communication web

### Caractéristiques :

- **Sans état** : chaque requête est indépendante.
- **Simple** et **flexible**
- Gère les pages web, les API, etc.

### Exemple d’échange :

> **Requête :**
> GET / HTTP/1.1  
> Host: [www.google.ca](http://www.google.ca)


> **Réponse :** 
> HTTP/1.1 200 OK 
> Content-Type: text/html 
> Set-Cookie: id=42; path=/

---
## Méthodes HTTP

| Méthode | Action                      | A un body ? |
| ------- | --------------------------- | ----------- |
| GET     | Lire une ressource          | non         |
| POST    | Envoyer des données         | oui         |
| PUT     | Mettre à jour une ressource | oui         |

### Exemples avec `curl` :

```bash
# GET
curl https://jsonplaceholder.typicode.com/users

# POST
curl -v -d '{"title": "foo", "body": "bar"}' \
     -H 'Content-Type: application/json' \
     https://jsonplaceholder.typicode.com/posts

# PUT
curl -X PUT -v -d '{"id": 1, "title": "foo"}' \
     -H 'Content-Type: application/json' \
     https://jsonplaceholder.typicode.com/posts/1

```


- -d = flag pour post
- -v = flag pour verbose

Un **proxy** est un intermédiaire entre user et Internet

-  Il peut **stocker** les réponses (cache)
-  Réduire la latence (éviter d’aller en Californie)
-  Filtrer ou surveiller le trafic
---
/etc/hosts 
C:Windows/System32/drivers/etc/hosts

---

==Bonnes pratiques Ajax livre Christophe Porteneuve==
==Programming the world wide web==

