

**Serial Monitor : analogue à la console en JavaScript**
### Fonctions à utiliser pour le wifi

`WiFI.begin(ssid, password)` 
- Fonction qui va tenter d'établir une connexion par WIFI à un réseau avec le nom SSID en paramètres et le password

`WiFi.status()` : 
- Fonction qui vérifie l'état de la connexion (interrompu, établie ou échouée)

`WiFi.localIP()` : 
- Fonction qui récupère l'IP du esp32

### Fonctions à utiliser pour le Server WEB

`WiFiServer server(80)` 
- Créé un serveur au port 80

`server.begin()` : 

---

## Obtenir le MAC ADDRESS

```c++
#include <WiFi.h>

void setup() {

Serial.begin(115200);
delay(1000); // Pause pour éviter un affichage corrompu
  

WiFi.mode(WIFI_MODE_STA); // Active le mode Wi-Fi station 
Serial.print("Adresse MAC de l'ESP32-C3 : ");
Serial.println(WiFi.macAddress()); // obtenir et affiche l'adresse MAC
}

void loop() {

}
```

## Control led par wifi

```c++
#include <WiFi.h>

  

// 🔹 Remplace par ton réseau Wi-Fi

const char* ssid = "PATATUS"; // Nom du Wi-Fi
const char* password = "0MOZ0fn7X9@7$"; // Mot de passe


WiFiServer server(80); // Démarre un serveur Web sur le port 80
  

#define LED_PIN 8 // Définition de la pin de la LED

void setup() {
Serial.begin(115200);
pinMode(LED_PIN, OUTPUT);
digitalWrite(LED_PIN, LOW); // LED éteinte au démarrage

  

// Connexion au Wi-Fi

Serial.print("connexion a ");
Serial.println(ssid);
WiFi.begin(ssid, password);


// Attente de connexion
while (WiFi.status() != WL_CONNECTED) {
delay(1000);
Serial.print(".");
}

Serial.println("\n Connecte au Wi-Fi !");
Serial.print("Adresse IP : ");
Serial.println(WiFi.localIP()); // Affiche l'IP de l'ESP32-C3

server.begin(); // Lancement du serveur Web
}
  
void loop() {
WiFiClient client = server.available();
if (client) {

Serial.println("Client connecte ");
String request = "";

  
  

while (client.connected()) {
if (client.available()) {
	char c = client.read();
	request += c;
	if (c == '\n') 
		break;
	}
}

  

Serial.println("Requete recue : " + request);

  

if (request.indexOf("/ON") != -1) {

digitalWrite(LED_PIN, HIGH);

Serial.println("LED Off ");

}

if (request.indexOf("/OFF") != -1) {

digitalWrite(LED_PIN, LOW);

Serial.println("LED on !");

}

  

// Envoi de la page Web au navigateur

client.println("HTTP/1.1 200 OK");

client.println("Content-type:text/html");

client.println();

client.println("<html><head><title>ESP32 LED</title></head>");

client.println("<body style='font-family:Arial; text-align:center;'>");

client.println("<h1>TEST CONTROL</h1>");

client.println("<p><a href='/ON'><button style='font-size:20px;'>Allumer LED</button></a></p>");

client.println("<p><a href='/OFF'><button style='font-size:20px;'> Eteindre LED</button></a></p>");

client.println("</body></html>");

client.println();

  

client.stop(); // Déconnexion du client

Serial.println("Client déconnecté.");

}

}

```
