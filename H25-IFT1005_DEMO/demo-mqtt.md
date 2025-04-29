
**MQTT** (Message Queuing Telemetry Transport) est un protocole de communication très léger, fondé sur le modèle **publish/subscribe**. Il est principalement utilisé pour transmettre des messages de manière efficace et en temps réel entre des appareils connectés

Ce protocole est devenu un **standard dans l’Internet des Objets (IoT)**, surtout dans ces domaines  :

- **Smart Home : pour automatiser l’éclairage, le chauffage et autres tucs
- **Applications de messagerie mobile sans carte SIM**, comme Messenger ou Instagram, où MQTT est utilisé pour envoyer des messages, gérer les notifications ou afficher l’état de connexion en temps réel  (et oui, le statut "vu/read", c'est du MQTT...)
- **Domotique** : pour contrôler des objets connectés via Wi-Fi, comme des capteurs ou des interrupteurs intelligents (ou un ESP32)

---
# Pourquoi et comment marche MQTT pour cette démo

MQTT marche dans des conditions très précaire et donc la précarité ça ressemble à ... ça : 

- les appareils avec un wifi pas top (bande passante très bof)
- les appareils qui ont une batterie faible (capteurs téléphones)
- les systèmes embarqués (Raspberry pi, ESP32)
- les situations ou une surcharge d'information peut être catastrophique (lag, freeze, DOS)

#### Un petit exemple: 

Vous préparez du pain, et vous devez le surveiller. Vous êtes dans une salle à coté. Est ce que vous voudriez vraiment vous lever *chaque minute* pour savoir si votre pain a cramé ou non? C'est ainsi que marche **HTTP**, vous allez être fatigué (saturation). Il serait plus simple d'avoir quelqu'un qui surveille votre pain, et qui en informe un messager qui se déplacera à vous pour vous relayer l'information

<div style="page-break-after: always;"></div>


ici ; 
- vous êtes l'abonné au **topic** pain/cuisson
- la personne qui surveille le pain est celui qui **publie** l'information de cuisson (prêt ou non)
- la personne qui se déplace pour vous informer est le **Broker**

==ON **INTERROGE** RIEN , TOUT ARRIVE TOUT SEUL!==

On utilisera pour l'instant le broker **Mosquitto** pour s'envoyer de l'information d'un navigateur vers un terminal d'un autre ordinateur ! Sachez qu'il en existes d'autres par contre (HiveMQ par exemple)

---
## Installer Mosquitto pour windows

- Vous allez à : https://mosquitto.org/download/
- Installez la version **x64** (sinon x86 si vous marchez en 32bits)
- Pour l'utiliser vous devez vous rendre au répertoire `Program Files/mosquitto` via `cd`

Par la suite on configurera le fichier `mosquitto.conf`

```txt
listener 1883 
allow_anonymous true
log_type all

listener 9001
protocol websockets
allow_anonymous true
```

Ce que tout ça veux dire

- `listener 1883` : le Broker Mosquitto va écouter au port 1883
- `allow_anonymous` : permet des connexions sans authentifications (pour se simplifier la vie)
- `log_type all`: permet tout les logs (pas nécessairement vu ici, mais très utile en cas de problèmes)

#### ==Nous n'utiliserons **pas** ces ports pour l'instant, on utilisera un broker en ligne pour apprendre, ces configs sont pour vous si vous souhaitez utiliser votre propre **mosquitto** sur votre PC en local (et donc utiliser votre IP publique au lieu de test.mosquitto.org==
## Pour Mac...

Vous DEVEZ avoir Homebrew pour avoir l'option d'installer par le **terminal**

1) Installez homebrew : 

```bash 
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

- vérifiez que ça a marché en tapant :

```bash
brew --version
```

2) Par la suite tapez :

```bash
brew install mosquitto
```

et vous aurez les outils principaux pour travailler avec Mosquitto

# Démarrer le Broker Mosquitto


1) Vous ouvrez PowerShell et vous tapez `cd ..` puis `cd ..` afin de retourner au niveau du disque
2) Entrez `cd 'Program Files' ` puis entrez `cd mosquitto` afin de rentrer dans le répertoire de **mosquitto**
3) Démarrez le broker en tapant :
```bash
.\mosquitto.exe -c .\mosquitto.conf -v
```

ce que tout ça veux dire :
- `.\mosquitto.exe`  est un exécutable qui sert à démarrer le broker (le mettre prêt à l'écoute)
-  `-c` est le flag pour signaler que le next argument est le fichier de config
-  `.\mosquitto.conf` est le fichier config
- `-v` est le flag de *verbose*, pour écrire en détail sur le terminal ce qui est entrain de se faire (vous verrez sur quels ports vous écoutez par exemple)

- ***Pour Mac, entrez seulement ``mosquitto`` dans votre terminal***

<div style="page-break-after: always;"></div>


# Vous abonner à un topic pour voir sur le terminal

1) Ouvrez un autre terminal PowerShell et déplacez vous aussi dans le répertoire `Program Files/mosquitto`
2) cette fois tapez ```
```bash
.\mosquitto_sub.exe -h test.mosquitto.org -t test/phone -v 
```

Ce que tout ça veux dire :
- `.\mosquitto_sub.exe`  est un exécutable qui sert à s'abonner à un topic
-  `-h` est le flag pour donner l'ip du host
-  `test.mosquitto.org` est le host
- `-t` est le flag du topic (le sujet) ou on veux s'abonner

- ***Pour Mac entrez `mosquitto_sub -h test.mosquitto.org -t test/phone`***


# Publier à un topic pour voir sur le terminal

1) Ouvrez un autre terminal PowerShell et déplacez vous aussi dans le répertoire `Program Files/mosquitto`
2) cette fois tapez ```
```bash
.\mosquitto_pub.exe -h test.mosquitto.org -t test/phone -m 'coucou les zamis' -v -r
```

Ce que tout ça veux dire :
- `.\mosquitto_sub.exe`  est un exécutable qui sert à s'abonner à un topic
-  `-h` est le flag pour donner l'ip du host
-  `test.mosquitto.org` est le host
- `-t` est le flag du topic (le sujet) ou on veux s'abonner
- `-m` est le flag pour indiquer que le prochain argument est un **message**
- `-r` est le flag pour dire que les messages doivent être gardés par le broker et redistribué lorsque quelqu'un s'abonne au topic concerné (notion d'**historique**)

- ***Pour Mac entrez `mosquitto_sub -h test.mosquitto.org -t test/phone`***

---
# Faire un chat en classe

Vous aurez besoin de  3 terminaux 
- 1 broker
- 1 terminal pour écrire vos messages
- 1 terminal pour voir le contenu du chat

1) Démarrez le broker avec `.\mosquitto.exe -c .\mosquitto.conf -v`
2) Dans votre deuxième, déplacez vous dans `Program Files/mosquitto` et tapez `.\mosquitto_sub.exe -h ift1005.xyz -t '#' -v -r` afin de vous abonner **à tout topics** 
3) Dans le troisième, vous tapez cette fois ` .\mosquitto_pub.exe -h ift1005.xyz -t monNom -m 'message random' -r` pour envoyer en votre nom (le topic) un message

==Broker:==
![[broker.png|548x258]]

==publisher:==
![[publisher.png|548x61]]

<div style="page-break-after: always;"></div>


==subscriber:==
![[subscriber.png|571x240]]

# Nous pouvons simuler un Whatsapp avec une app et un panel MQTT!

Si jamais vous voulez texter à travers un **téléphone**, et pas faire ``mosquitto_pub`` sur un terminal, vous pouvez utiliser une app IoT ! 

- Installez une application **IoT MQTT DASH**
- Créez une connexion et appelez la ``DEMO-MQTT``
- Ne remplissez **que** les champ Broker Web/IP adress, Port et Network Protocol !
-  ``BrokerWeb/IP = test.mosquitto.org`` ou pour le cours `ift1005.xyz`
- ``Port = 1883``
- ``Network Protocol = TCP``
- Par la suite, ajoutez un **dashboard** et nomez le *SEND-MESSAGE* puis *Create*
- Ajoutez un panel pour décider de quel type de message que vous envoyez, choissisez text input et nommez le *TEXT-MESSAGE*
- Entrez comme topic ``test/phone``, puis *Create*


---
<div style="page-break-after: always;"></div>


# Gros problème sur navigateurs : HTTP est UNIDIRECTIONNEL et RÉPÉTITIF! 

Depuis le début on travaille sur terminal, mais sur navigateurs c'est comment? On se rappelle que les navigateurs **n'ont pas accès à tout les ports du routeur**, alors comment on peut établir une communication en continu à travers un navigateur?

**Rappel pour HTTP**: Dès qu'on émet une requête et qu'on reçoit la réponse du serveur, on **ferme** la connexion, ce n'est donc *pas permanent et pas idéal pour de la communication persistante!* On demande l'info sans cesse à **nouveau**

**Rappel pour SSH**: Ce n'est pas un port ouvert pour les navigateurs! C'est une faille de sécurité sinon, on ne peut pas utiliser SSH pour communiquer (et ce n'est même pas fait pour ça, c'est un protocole pour contrôler à distance un ordinateur, **trop lourd**)...

Ce qu'on cherche pour la connexion au fond, c'est le protocole *TCP* **, c'est un protocole de communication fiable... mais il n'est pas non plus permit par un navigateur! 
- Vous remarquerez que pour un navigateur, il n'y a pas de connexion **TCP brute**, il y a *toujours* un protocole autorisé sur navigateur juste devant; lorsque vous écrivez ``192.168.0.1`` en réalité le navigateur comprend `https://192.168.0.1` ! 

Il nous reste donc ==**WebSocket**!==
# Un peu de triche pour MQTT

Comme beaucoup de ports sont fermés aux navigateurs et qu'on a besoin d'une connexion persistante stable (comme **TCP**) qui n'est pas non plus possible, on va d'abord **faire une requête HTTP (autorisé) puis la transformer (upgrade) en connexion Web Socket par la suite!**

**Ce que tout ça veux dire :**

- Coucouuuu ! Je suis une requête HTTP classique (GET), tu me connais non ?  
- Oui oui, je connais, tu peux passer
- Alriiight, merci ! Maintenant que tu m’as ouvert la porte... est-ce que je peux discrètement **changer de protocole** pour devenir une connexion **WebSocket sécurisée** ?  
- Ahh bah... tu es déjà à l’intérieur, alors vas-y, **switch**
<div style="page-break-after: always;"></div>



On vois ce changement dans ``Networks -> WS`` de l'inspecteur, on remarquera que la requête HTTP était un simple ``GET/``, qui ne visait pas à récupérer quoi que ce soit, mais c'était juste un masque pour déguiser une connexion Web Socket en HTTP pour établir une connexion persistante par le navigateur !

L'url qu'on utilisera pour se connecter est `wss://test.mosquitto.org:8081`

---
# Dans notre site de VOTE PUBLIQUE

1)==Pour TOUT site qui utilise MQTT==, on **importe** le script pour les commandes MQTT (mqtt.connect, créer l'objet client etc...)
- `<script src="https://unpkg.com/mqtt/dist/mqtt.min.js"></script>`

```javascript
  <script>
	const client = mqtt.connect('wss://test.mosquitto.org:8081');
	    function vote(option) {
	      client.publish('test/phone', option);
	    }
  </script>
```

**Ce que tout ça veux dire :**

- on crée le client qui est tout simplement l'entité qui se connecte au broker Mosquitto ici au port 8081 par Secure WebSocket
- Puis, on défini la fonction ``vote()`` avec en paramètre l'option choisie. Le but est donc que notre client (analogie : celui qui surveillait le pain) **publie** l'information du vote choisi **dès** que quelqu'un **a voté une option X**

#### *Et si je voulais savoir combien de gens ont voté sur une catégorie?*

Rien nous empêche de faire une deuxième page qui est abonnée aussi au même topic! 
On aurait par exemple un site **local** (pour limiter les usagers, même si niveau sécurité c'est pas le mieux mais bon, pour plus tard tout ça)
<div style="page-break-after: always;"></div>


# Dans notre site de RÉSULTAT LOCAL

```javascript
<script>

    const clientadmin = mqtt.connect('wss://test.mosquitto.org:8081');
    const votes = {IFT1215: 0,MAT1400: 0,IFT1065: 0,MAT1600: 0};
    clientadmin.on('connect', () => { clientadmin.subscribe('test/phone');  });
    clientadmin.on('message', (topic, message) => {
	    const vote = message.toString();
	    if (votes[vote] !== undefined) {
	        votes[vote]++;
	        document.getElementById(vote).textContent = votes[vote];
	    }
    });
</script>
```

**Ce que tout ça veux dire :**

1) On crée l'entité ``clientadmin`` qui se connecte au broker ``test.mosquitto.org`` au port ``8081`

2) On crée le dictionnaire ``votes`` ou la clé est le nom de cours, pour chaque cours initie un compteur à 0 

3) Via le script MQTT importé, on utilise la méthode ``on()`` qui est la version MQTT du `àddEventListener()` (car on ne travaille pas juste avec le DOM/ éléments HTML, mais avec **un peu de back-end**) et à chaque fois qu'on se connectera (dès qu'on load la page ou qu'on rétabli le wifi), on s'abonnera au topic ``test/phone`` pour assurer la connexion 

4) On utilisera encore la méthode `on()` ! `reponse` est littéralement ce que le broker envois (le vote) au terminal abonné au `topic` en paramètre aussi. On utilisera `vote` qui est la version  *texte* de `reponse`. Si la publication est définie (pas nulle ou invalide), on recherche alors sa clé (contenu entre les \[ \] ) dans le dictionnaire des votes possibles et on incrémente le compteur concerné de 1

	==Attention, on utilise **textContent** et pas innerHTML!== On souhaite littéralement changer du texte, on ne voudrais pas rajouter des balises par inadvertance là



