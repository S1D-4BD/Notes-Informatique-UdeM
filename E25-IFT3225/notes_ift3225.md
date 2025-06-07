
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

Le **DNS (Domain Name System)** fait la liaison bidirectionnelle entre un nom canonique (ex: `www.iro.umontreal.ca`) en une **adresse IP**.

**Navigateur -> DNS -> IP -> Connexion TCP -> HTTP -> Réponse**
###  Processus de résolution

- **Vérification du cache local DNS**
    - Ton système ou navigateur garde en mémoire les résolutions précédentes.
- **Contact d’un résolveur DNS (souvent : 127.0.0.53, 8.8.8.8, ou FAI)**
    - C’est un **serveur récursif** : il va chercher la réponse complète pour toi.
- **Étapes du résolveur récursif :**
    - Demande aux **serveurs racine** (`.`) de A-M : "Qui gère `.ca` ?"
    - Obtiens réponse partielle "C'est lui"
    - Puis interroge le **serveur + haut (Top Level Domain)** (`.ca`) : "Qui gère `umontreal.ca` ?"
    - Ensuite, demande au **serveur autoritatif** de `umontreal.ca` : "Quelle est l’IP de `www.iro.umontreal.ca` ?"

>  **Commandes utiles  pour trouver le serveur dns:**
> - cat /etc/resolv.conf 
> - `ipconfig /all` (Windows)

==Pratique get le dns:==


 ```bash
sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ cat /etc/resolv.conf 
# # 
# #
nameserver 127.0.0.53 #c'est lui mo DNS
```

==Pratique: demander explicitement à mon DNS une adresse IP==

```bash
sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ dig @127.0.0.53 www.iro.umontreal.ca

; <<>> DiG 9.18.30-0ubuntu0.24.04.2-Ubuntu <<>> @127.0.0.53 www.iro.umontreal.ca
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 52384
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;www.iro.umontreal.ca.		IN	A

;; ANSWER SECTION:
www.iro.umontreal.ca.	3366	IN	CNAME	tartan.iro.umontreal.ca.
tartan.iro.umontreal.ca. 3366	IN	A	132.204.26.36

;; Query time: 23 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue May 20 21:42:57 EDT 2025
;; MSG SIZE  rcvd: 86

```

- `i server found`, je n ai que 1 seul DNS
- - `opcode: QUERY` : type de requête DNS (ici une simple requête standard)
- `status: NOERROR` : pas d’erreur
- `id: 52384` : id de la requête

- `qr` : query response (c’est une **réponse**, pas une requête)
- `rd` : recursion desired (** SI PAS MANUEL, alors une résolution récursive**)
- `ra` : recursion available (le serveur **supporte la récursion, NORMAL BREF**
- 
- `QUERY: 1` → 1 question posée 
- `ANSWER: 2` → 2 réponses reçues (une Canonimmal NAME et une A )
- `AUTHORITY: 0` → pas d’info sur les serveurs autoritatifrenvoyée

- Nom demandé : `www.iro.umontreal.ca.`
- `IN` = classe Internet
- `A` = on veut l’adresse **IPv4**

- Ligne 1 :
    - `www.iro.umontreal.ca` est un **alias** (CNAME)
    - C’est un nom canonique qui pointe vers `tartan.iro.umontreal.ca`
    - **3366** = TTL (Time To Live) : la réponse est **valide 3366 secondes** dans le cache 
        
- Ligne 2 :
    - `tartan.iro.umontreal.ca` est résolu avec un enregistrement `A`
    - Sa vraie adresse IPv4 est `132.204.26.36`
    - ==si je tape ça, j'aurais le même site==

| Type    | Usage                         | exempel                             |
| ------- | ----------------------------- | ----------------------------------- |
| `A`     | Adresse IPv4                  | `dig -t A www.iro.umontreal.ca`     |
| `AAAA`  | Adresse IPv6                  | `dig -t AAAA www.umontreal.ca`      |
| `MX`    | Mail                          | `dig -t MX www.umontreal.ca`        |
| `NS`    | Get Serveurs autoritatifs     | `dig -t NS umontreal.ca`            |
| `CNAME` | Alias canonique               | `dig -t CNAME www.iro.umontreal.ca` |
| `PTR`   | Résolution inverse (pas type) | `dig -x 132.204.26.36`              |
| `TXT`   | Infos textuelles              | `dig -t TXT umontreal.ca`\|`        |
| `AXFR`  | Transfert de zone             | `dig @ns1.example.com -t AXFR `     |


Les noms de machine doivent être sous la forme de ***Fully Qualified Domain Name***
www.google.com.

il y a un point à la fin, lecture de droite à gauche
>www= nom de machine
  google = nom de domaine ou se trouve la machine
. com = nom de domaine plus haut niveau

### DNS, système client/serveur

**Serveur** : ordinateur qui a une application qui roule en permanence et qui écoute sur un port, souvent en échanges d'info sur TCP ou UDP au port 53

*Structure de recherche des domaines 
![[DNS_structure.png]]

- 13 serveurs racine , ne reconnaissent que les TLD at this point
- évite trafic via des délégations, permet une hiérarchie de recherche récursive

>Alors si ces serveurs tombent en panne alors on évite la galère. Les TLD il contiennent la liste de tout les domaines de plus haut niveau ET C'EST QUI LE dns QUI SOCCUPE DE CES IP

==chacun contient la liste des serveurs DNS qui contient les domaines en dessous de lui==

- Le serveur racine (`.`) indique :  
    "Pour `.ca`, va voir les serveurs du TLD `.ca`" 
- Le serveur du TLD `.ca` (ex : géré par **CIRA**) dit :  
    "Pour `umontreal.ca`, interroge ces serveurs autoritaires"
- Le serveur de `umontreal.ca` délègue :  
    "Pour `iro.umontreal.ca`, voici les serveurs qui ont la réponse"

### domaine vs zone

domaine est un nom qui identifie une hierarchie logique sur le web (ex. umontreal.ca, google.com)

> Tout ce qui partage le même suffixe fait partie du même domaine

**C'est un fichier texte qui est lu en permanence qui donne les IP et leur DNS**

Zone DNS est une portion déléguée de la gestion d'un domain, géré par un DNS autoritaire
==Le domaine `umontreal.ca` peut être **géré en plusieurs zones DNS** ==
- `.ca` : zone gérée par **CIRA** (l’organisme qui gère les domaines canadiens)
- `umontreal.ca` : zone gérée par l’**Université de Montréal**
- `iro.umontreal.ca` : zone gérée par le **DIRO**


Pour que `.ca` délègue à un autre serveur, on va avoir un glue record, qui va coller (les flèches colorées du diagramme) le serveur délégué au NS (serveur autpritaire qui s'en occupe)

>requêtes récursives = je pose la question, débrouille toi pour me donner la bonne 
>requêtes itératives = travaille 1 zone du domaine, répond pas la bonne, mais donne une indication de qui s'en occupe

C'est un serveur qui ne connait que 13 serveurs racine et recherche dynamiquement les autres DNS : même si on change un des adresse des DNS, il va s'ajuster

==Commandes pour interroger DNS==
`cat /etc/resolv.conf`
``dig @DNSIP www.example.com

## exemple itératif:

```bash
sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ cat /etc/resolv.conf 
# This is /run/systemd/resolve/stub-resolv.conf managed by man:systemd-resolved(8).
# Do not edit.
#
# This file might be symlinked as /etc/resolv.conf. If you're looking at
# /etc/resolv.conf and seeing this text, you have followed the symlink.
#
# This is a dynamic resolv.conf file for connecting local clients to the
# internal DNS stub resolver of systemd-resolved. This file lists all
# configured search domains.
#
# Run "resolvectl status" to see details about the uplink DNS servers
# currently in use.
#
# Third party programs should typically not access this file directly, but only
# through the symlink at /etc/resolv.conf. To manage man:resolv.conf(5) in a
# different way, replace this symlink by a static file or a different symlink.
#
# See man:systemd-resolved.service(8) for details about the supported modes of
# operation for /etc/resolv.conf.

nameserver 127.0.0.53
options edns0 trust-ad
search umontreal.ca
sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ dig @127.0.0.53 www.iro.umontreal.ca
```

==On voit que le DNS fourni est le 127.0.0.53==

```bash
sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ dig @127.0.0.53 www.iro.umontreal.ca 
; <<>> DiG 9.18.30-0ubuntu0.24.04.2-Ubuntu <<>> @127.0.0.53 www.iro.umontreal.ca
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 15975
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;www.iro.umontreal.ca.		IN	A

;; ANSWER SECTION:
### www.iro.umontreal.ca.	3600	IN	CNAME	tartan.iro.umontreal.ca.
### tartan.iro.umontreal.ca. 3600	IN	A	132.204.26.36

;; Query time: 15 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue May 13 12:55:05 EDT 2025
;; MSG SIZE  rcvd: 86

```

donne ``

```bash
### www.iro.umontreal.ca.	3600	IN	CNAME	tartan.iro.umontreal.ca.
### tartan.iro.umontreal.ca. 3600	IN	A	132.204.26.36
```


## exemple itératf :

```bash
sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ dig .

; <<>> DiG 9.18.30-0ubuntu0.24.04.2-Ubuntu <<>>
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 57989
;; flags: qr rd ra; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 27

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;.				IN	NS

;; ANSWER SECTION:
.			7189	IN	NS	b.root-servers.net.
.			7189	IN	NS	k.root-servers.net.
.			7189	IN	NS	i.root-servers.net.
.			7189	IN	NS	h.root-servers.net.
.			7189	IN	NS	j.root-servers.net.
.			7189	IN	NS	e.root-servers.net.
.			7189	IN	NS	f.root-servers.net.
.			7189	IN	NS	m.root-servers.net.
.			7189	IN	NS	c.root-servers.net.
.			7189	IN	NS	g.root-servers.net.
.			7189	IN	NS	a.root-servers.net.
.			7189	IN	NS	d.root-servers.net.
.			7189	IN	NS	l.root-servers.net.

;; ADDITIONAL SECTION:
c.root-servers.net.	7189	IN	AAAA	2001:500:2::c
d.root-servers.net.	7189	IN	AAAA	2001:500:2d::d
f.root-servers.net.	7189	IN	A	    192.5.5.241
h.root-servers.net.	7189	IN	A	    198.97.190.53 #####JE PREND LUI
b.root-servers.net.	7189	IN	AAAA	2801:1b8:10::b
i.root-servers.net.	7189	IN	A	    192.36.148.17
e.root-servers.net.	7189	IN	AAAA	2001:500:a8::e
m.root-servers.net.	7189	IN	A	    202.12.27.33
c.root-servers.net.	7189	IN	A	    192.33.4.12
g.root-servers.net.	7189	IN	AAAA	2001:500:12::d0d
h.root-servers.net.	7189	IN	AAAA	2001:500:1::53
a.root-servers.net.	7189	IN	A	    198.41.0.4
i.root-servers.net.	7189	IN	AAAA	2001:7fe::53
g.root-servers.net.	7189	IN	A	    192.112.36.4
d.root-servers.net.	7189	IN	A    	199.7.91.13
f.root-servers.net.	7189	IN	AAAA	2001:500:2f::f
j.root-servers.net.	7189	IN	A	    192.58.128.30
e.root-servers.net.	7189	IN	A	    192.203.230.10
l.root-servers.net.	7189	IN	A	    199.7.83.42
a.root-servers.net.	7189	IN	AAAA	2001:503:ba3e::2:30
j.root-servers.net.	7189	IN	AAAA	2001:503:c27::2:30
l.root-servers.net.	7189	IN	AAAA	2001:500:9f::42
b.root-servers.net.	7189	IN	A	    170.247.170.2
k.root-servers.net.	7189	IN	AAAA	2001:7fd::1
m.root-servers.net.	7189	IN	AAAA	2001:dc3::35
k.root-servers.net.	7189	IN	A	    193.0.14.129

;; Query time: 1 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue May 20 22:37:27 EDT 2025
;; MSG SIZE  rcvd: 811


```

ON voit que ya beaucoup de serveurs racines 

Si on interroge un des serveurs racines quon connait pour www.umontreal.ca

```bash
dig @198.97.190.53 www.iro.umontreal.ca

; <<>> DiG 9.18.30-0ubuntu0.24.04.2-Ubuntu <<>> @198.97.190.53 www.iro.umontreal.ca
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 27446
;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 4, ADDITIONAL: 9
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;www.iro.umontreal.ca.		IN	A

;; AUTHORITY SECTION:
ca.			172800	IN	NS	c.ca-servers.ca.
ca.			172800	IN	NS	d.ca-servers.ca.
ca.			172800	IN	NS	j.ca-servers.ca.
ca.			172800	IN	NS	any.ca-servers.ca.

;; ADDITIONAL SECTION:
c.ca-servers.ca.	172800	IN	A	185.159.196.2
d.ca-servers.ca.	172800	IN	A	45.142.220.101
j.ca-servers.ca.	172800	IN	A	198.182.167.1
any.ca-servers.ca.	172800	IN	A	199.4.144.2
c.ca-servers.ca.	172800	IN	AAAA	2620:10a:8053::2
d.ca-servers.ca.	172800	IN	AAAA	2a0e:dbc0::101
j.ca-servers.ca.	172800	IN	AAAA	2001:500:83::1
any.ca-servers.ca.	172800	IN	AAAA	2001:500:a7::2

;; Query time: 54 msec
;; SERVER: 198.97.190.53#53(198.97.190.53) (UDP)
;; WHEN: Tue May 20 22:40:35 EDT 2025
;; MSG SIZE  rcvd: 302

```


On a 4 serveurs qui gèrent `.ca.` on en prend 1 random

```bash
sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ dig @185.159.196.2 www.iro.umontreal.ca

; <<>> DiG 9.18.30-0ubuntu0.24.04.2-Ubuntu <<>> @185.159.196.2 www.iro.umontreal.ca
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 32081
;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 4, ADDITIONAL: 5
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;www.iro.umontreal.ca.		IN	A

;; AUTHORITY SECTION:
umontreal.ca.		86400	IN	NS	ns1.risq.qc.ca.
umontreal.ca.		86400	IN	NS	ns2.risq.qc.ca.
umontreal.ca.		86400	IN	NS	dnsp1.dit.umontreal.ca.
umontreal.ca.		86400	IN	NS	dnsp2.dit.umontreal.ca.

;; ADDITIONAL SECTION:
dnsp1.dit.umontreal.ca.	86400	IN	A	132.204.8.131
dnsp2.dit.umontreal.ca.	86400	IN	A	132.204.8.141
ns1.risq.qc.ca.		86400	IN	A	192.26.210.111
ns2.risq.qc.ca.		86400	IN	A	206.167.244.111

;; Query time: 22 msec
;; SERVER: 185.159.196.2#53(185.159.196.2) (UDP)
;; WHEN: Tue May 20 22:46:01 EDT 2025
;; MSG SIZE  rcvd: 211

```


On a 4 serveurs qui gèrent `umontreal.ca.` on en prend 1 random

```bash
sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ dig @132.204.8.131 www.iro.umontreal.ca

; <<>> DiG 9.18.30-0ubuntu0.24.04.2-Ubuntu <<>> @132.204.8.131 www.iro.umontreal.ca
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 36532
;; flags: qr aa rd; QUERY: 1, ANSWER: 2, AUTHORITY: 2, ADDITIONAL: 3
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1220
; COOKIE: a7c018737917bf0601000000682d3e95f711531f54ee63f2 (good)
;; QUESTION SECTION:
;www.iro.umontreal.ca.		IN	A

;; ANSWER SECTION:
www.iro.umontreal.ca.	3600	IN	CNAME	tartan.iro.umontreal.ca.
tartan.iro.umontreal.ca. 3600	IN	A	132.204.26.36

;; AUTHORITY SECTION:
iro.umontreal.ca.	3600	IN	NS	typhon.iro.umontreal.ca.
iro.umontreal.ca.	3600	IN	NS	tabata.iro.umontreal.ca.

;; ADDITIONAL SECTION:
tabata.iro.umontreal.ca. 3600	IN	A	132.204.24.69
typhon.iro.umontreal.ca. 3600	IN	A	132.204.24.66

;; Query time: 30 msec
;; SERVER: 132.204.8.131#53(132.204.8.131) (UDP)
;; WHEN: Tue May 20 22:46:45 EDT 2025
;; MSG SIZE  rcvd: 188


```

On a trouvé qui gèrent `iro.umontreal.ca.` on en prend 1 random

### Sécurité

ils doivent tous être au moins en **double** sinon en cas de pannes  gros problèmes

SI on modifie une addresse ip, on modifie sur un primaire, qui va donner au primaire par réplication automatique. Panne -> un secondaire devient primaire

réplication = transfert de zone dig @dns server -t AXFR {ZONE}

### type enregistrement

A = IPV4
AAAA = IPV6
TXT
PTR = DNS INVERSE
CNAME= CANONICAL NAME
SRV = pour définir serveur assurant d un service



```bash
sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ dig -t MX umontreal.ca

; <<>> DiG 9.18.30-0ubuntu0.24.04.2-Ubuntu <<>> -t MX umontreal.ca
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 15040
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;umontreal.ca.			IN	MX

;; ANSWER SECTION:
umontreal.ca.		3600	IN	MX	0 umontreal-ca.mail.protection.outlook.com.

;; Query time: 12 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue May 13 13:22:12 EDT 2025
;; MSG SIZE  rcvd: 97

```


```bash
sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ dig -t A iro.umontreal.ca

; <<>> DiG 9.18.30-0ubuntu0.24.04.2-Ubuntu <<>> -t A iro.umontreal.ca
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 41150
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;iro.umontreal.ca.		IN	A

;; ANSWER SECTION:
iro.umontreal.ca.	3600	IN	A	132.204.26.36

;; Query time: 4 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue May 13 13:23:54 EDT 2025
;; MSG SIZE  rcvd: 61

```


#### dns spoofing

DNS n est pas sécurisé, imaginons un pirate vas renvoyer une fausse réponse en permanence, lors d une requete récursive . Le faux site ressemble exactement au site original, mais lui va voler tes datas

corrigé avec DNSSEC

---


```bash
#### dans le fichier etc/named.conf


zone "ift3225.ca" IN {
	type master;
	file "ift3225.ca"; # le fichier des data de cette zone est ce fichier<
	allow-transfer { 192.168.230.132 } #transfert vers zone esclave
};

zone "230.168.168.192.in-addr-arpa" IN {
	type slave; #recup la zone depuis maitre
	file "mazoneinversee"; 
	masters { 192.168.230.131; }; #correspond au dns
};
```

```bash
# dans le repertoire var/named, creer si pas là
# la c est pour .ca


$TL 3H #Durees de 3h
@    IN SOA @ admin.umontreal.ca. (# mettre un point à la fin
							0   ; serial
							1D  ; refresh 
							1H  ; retry
							1W  ; expire
							3H) ; minimum
		NS @ 
		A       127.0.0.1
		AAAA    ::1 # Uun seul ipv4 pour ca

www     A       10.10.10.10 
toto    cname www
titi    A       10.0.2.3
```


```bash
# le fichier mazoneinversee
$TTL 3H 
@      IN SOA @ admin.too.ca. (
							0   ;
							1D  ; refresh 
							1H  ; retry
							1W  ; expire
							3H) ; minimum
							3H) ; minimum
		NS @ 
		A       127.0.0.1
		AAAA    ::1 # Uun seul ipv4 pour ca
		
131     PTR machine1.ift3225.ca. # LE 230 devient ca
)
```


### recherche récursive avec DNS de GOOGLE 

```bash
sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ dig @8.8.8.8 www.fraise.com

; <<>> DiG 9.18.30-0ubuntu0.24.04.2-Ubuntu <<>> @8.8.8.8 www.fraise.com
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 23518
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;www.fraise.com.			IN	A

;; ANSWER SECTION:
www.fraise.com.		300	IN	CNAME	57935.sedoparking.com.
57935.sedoparking.com.	3600	IN	A	64.190.63.136

;; Query time: 152 msec
;; SERVER: 8.8.8.8#53(8.8.8.8) (UDP)
;; WHEN: Fri May 16 13:50:32 EDT 2025
;; MSG SIZE  rcvd: 91

```

TEST AVEC UMONTREAL ITERATIF

```bash

sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ dig @192.33.4.12 www.iro.umontreal.ca

; <<>> DiG 9.18.30-0ubuntu0.24.04.2-Ubuntu <<>> @192.33.4.12 www.iro.umontreal.ca
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 15143
;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 4, ADDITIONAL: 9
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 32bdb32ee0915fd2010000006827b391c99cea41d0b352f0 (good)
;; QUESTION SECTION:
;www.iro.umontreal.ca.		IN	A

;; AUTHORITY SECTION:
ca.			172800	IN	NS	any.ca-servers.ca.
ca.			172800	IN	NS	d.ca-servers.ca.
ca.			172800	IN	NS	c.ca-servers.ca.
ca.			172800	IN	NS	j.ca-servers.ca.

;; ADDITIONAL SECTION:
any.ca-servers.ca.	172800	IN	A	199.4.144.2
j.ca-servers.ca.	172800	IN	A	198.182.167.1
d.ca-servers.ca.	172800	IN	A	45.142.220.101
c.ca-servers.ca.	172800	IN	A	185.159.196.2
any.ca-servers.ca.	172800	IN	AAAA	2001:500:a7::2
j.ca-servers.ca.	172800	IN	AAAA	2001:500:83::1
d.ca-servers.ca.	172800	IN	AAAA	2a0e:dbc0::101
c.ca-servers.ca.	172800	IN	AAAA	2620:10a:8053::2

;; Query time: 21 msec
;; SERVER: 192.33.4.12#53(192.33.4.12) (UDP)
;; WHEN: Fri May 16 13:52:18 EDT 2025
;; MSG SIZE  rcvd: 334

```


```bash
sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ dig @199.4.144.2 www.iro.umontreal.ca

; <<>> DiG 9.18.30-0ubuntu0.24.04.2-Ubuntu <<>> @199.4.144.2 www.iro.umontreal.ca
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 56991
;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 4, ADDITIONAL: 5
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;www.iro.umontreal.ca.		IN	A

;; AUTHORITY SECTION:
umontreal.ca.		86400	IN	NS	ns1.risq.qc.ca.
umontreal.ca.		86400	IN	NS	ns2.risq.qc.ca.
umontreal.ca.		86400	IN	NS	dnsp1.dit.umontreal.ca.
umontreal.ca.		86400	IN	NS	dnsp2.dit.umontreal.ca.

;; ADDITIONAL SECTION:
dnsp1.dit.umontreal.ca.	86400	IN	A	132.204.8.131
dnsp2.dit.umontreal.ca.	86400	IN	A	132.204.8.141
ns1.risq.qc.ca.		86400	IN	A	192.26.210.111
ns2.risq.qc.ca.		86400	IN	A	206.167.244.111

;; Query time: 15 msec
;; SERVER: 199.4.144.2#53(199.4.144.2) (UDP)
;; WHEN: Fri May 16 13:53:26 EDT 2025
;; MSG SIZE  rcvd: 211

```


```bash
sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ dig @192.26.210.111 www.iro.umontreal.ca

; <<>> DiG 9.18.30-0ubuntu0.24.04.2-Ubuntu <<>> @192.26.210.111 www.iro.umontreal.ca
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 13258
;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 4, ADDITIONAL: 3
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 28aa4d04515f9949010000006827b42d0fcfeeccf2272f5a (good)
;; QUESTION SECTION:
;www.iro.umontreal.ca.		IN	A

;; AUTHORITY SECTION:
iro.umontreal.ca.	28800	IN	NS	typhon.iro.umontreal.ca.
iro.umontreal.ca.	28800	IN	NS	dnsp1.dit.umontreal.ca.
iro.umontreal.ca.	28800	IN	NS	dnsp2.dit.umontreal.ca.
iro.umontreal.ca.	28800	IN	NS	tabata.iro.umontreal.ca.

;; ADDITIONAL SECTION:
typhon.iro.umontreal.ca. 28800	IN	A	132.204.24.66
tabata.iro.umontreal.ca. 28800	IN	A	132.204.24.69

;; Query time: 7 msec
;; SERVER: 192.26.210.111#53(192.26.210.111) (UDP)
;; WHEN: Fri May 16 13:54:54 EDT 2025
;; MSG SIZE  rcvd: 207

```

On fini avec  `132.204.24.69`


**Retrouver l'inverse **

```bash
sid@sid-ThinkBook-14s-Yoga-G3-IRU:~$ dig @1.1.1.1 -x 132.204.24.66

; <<>> DiG 9.18.30-0ubuntu0.24.04.2-Ubuntu <<>> @1.1.1.1 -x 132.204.24.66
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 2908
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;66.24.204.132.in-addr.arpa.	IN	PTR

;; ANSWER SECTION:
66.24.204.132.in-addr.arpa. 3600 IN	PTR	typhon.iro.umontreal.ca.

;; Query time: 265 msec
;; SERVER: 1.1.1.1#53(1.1.1.1) (UDP)
;; WHEN: Fri May 16 13:59:26 EDT 2025
;; MSG SIZE  rcvd: 92
```


```bash
dig @(authoritary server) -t AXFR iro.umontreal.ca
dig @(authoritary server) -t AXFR 230.168.192.in-addr.arpa


systemctl stop firewalld
systemctl disable firewalld
```

---

##  HTTP – Protocole de communication web

### Caractéristiques :

- **Sans état** : chaque requête est indépendante (ne se rappellera **pas** d'un login)
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

| Méthode | Action                      | A un body ?            |     |
| ------- | --------------------------- | ---------------------- | --- |
| GET     | Lire une ressource          | non (visible dans URL) |     |
| POST    | Envoyer des données         | oui                    |     |
| PUT     | Mettre à jour une ressource | oui                    |     |


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


- -d = **flag pour post**
- -v = flag pour verbose

Un **proxy** est un intermédiaire entre user et Internet

-  Il peut **stocker** les réponses (cache)
-  Réduire la latence (éviter d’aller en Californie)
-  Filtrer ou surveiller le trafic
---
/etc/hosts 
C:Windows/System32/drivers/etc/hosts

---
# SMTP

Fonctionne sur le port TCP 25 (SMTPS recommandé sur 465 en TLS ou 587 en SSL)

je vais envoyer a qqun sur umontreal email va contacter serv courriel gmail, avec smtp 
pour lire c est 2 autres protocoles POP3 et IMAC tres utilisé
On consulte souvent les email ,on les télécharge pas restent sur serveur

![[Screenshot from 2025-05-20 11-39-07.png]]

1 ) je demande a trouver mon DNS
2) il me répond
3) j'envoie via SMTP un mail dans un serveur qui le traitera
4) Ce serveur cherche son DNS
5) il lui répond
6) il est stocké dans un serveur Mail Xchange et IMAP pour consultation

Pour trouver un serveur un serveur de messagerie d'un domaine distant, le serveur SMTP recherche
l'enregistrement MX du domaine distant. Puis une requête A pour obtenir l’adresse IP.
Le serveur MX du domaine distant, va effectuer une vérification pour éviter de recevoir du courriel de spam.Il va faire une requête DNS pour obtenir le PTR correspondant au nom qu'il a reçu lors de la session SMTP. Si l'enregistrement PTR n'existe pas, le courriel pourrait être rejeté. L'enregistrement PTR exclut les serveurs SMTP ayant une adresse IP dynamique (souvent utilisés par les spammers

---
# PHP


```
used for form handling
$_GET = DATA append to url (not secure)
$_POST = DATA packaged inside the body of the HTTP request

```

```php
isset() = //retourn TRUE si variable déclarée et non nulle
empty() = //retourn TRUE si variable NON déclarée, nulle, FALSE etc.
```

case get 

```html

.php file = form-exo.php
<!DOCTYPE html>
...

<body>
    <form action="form-exo.php" method="get">
        <label >username: </label> <br>
        <input type="text" name="username"><br>
        <label >password: </label><br>
        <input type="text" name="password"><br>
        <input type="submit">
    </form>
</body>
</html>


<?php
    echo $_GET["username"] . "<br>";
    echo "{$_GET["password"]} <br>";
?>
```


==url donne : http://localhost/demo_php/form-exo.php?username=ss&password=sss==
problème on voit les infos
mais bon pour page search


exemples post 
```html
<html>
<body>
...<form action="form-exo.php" method="post">

        <label >username : </label>
        <input type="text" name="username"><br>
        <label >password : </label>
        <input type="password" name="password"><br>
        <input type="submit" name="login" value="Log In">
    </form>
    </body>
</html>

<?php
    if(isset($_POST["login"])){
        $username = $_POST["username"];
        $password = $_POST["password"];
  

        if(empty($username)){
            echo "please log in";
        }
        else{
            echo "you tried to log in as {$username}";
        }
?>
    }
```


exemple radio button

```html


```
- TOUJOURS vérifier si `$_POST["login"]`  est `isset()` ou est `!empty()`; sinon on aura `undefined`

---

# SESSION()


----
# Login projet PDO

https://www.youtube.com/watch?v=3-5DpAiCHy8
Consiste à créer une database qu'on interrogera via des `$query`


### Concept de PDO (PHP Data Object)

Le but est de 

| DB                              |
| ------------------------------- |
| base de données *nom* : website |
| website *table* persons         |
| persons : id, email, password   |

| PHP         |
| ----------- |
| connect.php |
| index.php   |
| login.php   |
| logout.php  |


CHEATSHEET PDO 

| PDO                          |                                                         |
| ---------------------------- | ------------------------------------------------------- |
| `$result = $db->query($sql)` | Exécute une requête définie `$sql` sur la database `db` |
|                              |                                                         |

important, en PDO on parle en statements `$stmt` et results `$result`

| Prepared Statement                                             |                                        |
| -------------------------------------------------------------- | -------------------------------------- |
| `$stmt = $db->prepare($sql);`                                  | Prépare le statement SQL               |
| ```$stmt->bindParam(num$variable);```                          | Lier variable PHP à paramètre SQL      |
| `$stmt->execute();`                                            | Exécute ``stmt`` (pas sur ``db``)      |
| `$result = $stmt->fetch();` <br>`$result = $stmt->fetchAll();` | Récupère 1 ``row``/ toutes les ``row`` |
| `$numRows=$result->rowCount();`                                |                                        |




binParam() exemple 

```php
$query = "INSERT INTO users (name, email) VALUES (:name, :email)";
$stmt = $db->prepare($query);

$name = "Alice";
$email = "alice@example.com";

$stmt->bindParam(':name', $name);
$stmt->bindParam(':email', $email);

$stmt->execute();

```


1) Établir une connexion avec la base de donnéees (PDO version)

```php
<?php

try{
    $db= new PDO("mysql:host=localhost;dbname=website;charset=utf8","sid","1227");
}
catch(PDOException $e){
    echo $e->getMessage();
}
?>

```


2) Login AVANT d'accéder à la page Index

```php

//code php en début de doc

<?php


session_start();
include "connect.php";
if (isset($_POST["login"])){

    if( empty($_POST["username"]) || empty($_POST["email"]) || empty($_POST["password"]) ){
        echo "<h1> incomplete credentials </h1>";
    }
    else{
      $username = strip_tags(trim($_POST["username"]));
      $email = trim($_POST["email"]);
      $password = strip_tags(trim($_POST["password"]));
        
      $query =$db->prepare("SELECT * FROM persons WHERE email=? AND password =?");

        $query->execute(array($email,$password));
        $control=$query->fetch(PDO::FETCH_OBJ);

        if($control){
            $_SESSION["username"] = $username;
            header("Location:index.php");
            exit();
        }
        else {
            echo "<h1>Incorrect password or email</h1>";
        }
    }
}
?>


```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Login page</title>
</head>

<body>
<form method="POST">
	<label for="">Username : </label> <input type="text" name="username"> <br>
	<label for="">Email : </label> <input type="email" name="email"> <br>
	<label for="">Password : </label> <input type="password" name="password"> <br>
	<input type="submit" name="login">
 </form>

</body>

</html>
```

3) Control réussi, redirection vers index.php
	1) SI ON A FORCÉ LA VISITE SANS AUTHENTIFICATION

``` PHP
<?php

session_start();    
if (!isset($_SESSION["username"])) {
    header("Location:login.php") ;
}
else{
}

?>
```


4) Éventuel logout 

```php
<?php

session_start();
session_destroy();
header("Location:login.php");

?>
```

---
