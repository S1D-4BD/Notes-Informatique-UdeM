
![[ESP32_PINOUT.jpeg]]


### **1. Broches d'Alimentation (Power)**

- **5V** : Alimentation 5V pour le module.
- **3V3** : Alimentation 3.3V 
- **GND** : Masse 

---

### **2. Broches d’Entrée Analogique (ADC)**

Ces broches permettent de lire des valeurs de tension analogiques :

- **A0 (GPIO0)**
- **A1 (GPIO1)**
- **A2 (GPIO2)**
- **A3 (GPIO3)**
- **A4 (GPIO4)**
- **A5 (GPIO5)**

Ces broches sont utilisées pour mesurer des capteurs analogiques (==potentiomètres, capteurs de lumière, température==, etc.)

---

### **3. Broches de Communication SPI (Serial Peripheral Interface)**

Utilisé pour la communication rapide avec des périphériques comme des écrans, capteurs, mémoires :

- **SCK (Serial Clock, GPIO4)** : Horloge SPI
- **MISO (Master In Slave Out, GPIO5)** : Données du périphérique vers le microcontrôleur
- **MOSI (Master Out Slave In, GPIO6)** : Données du microcontrôleur vers le périphérique
- **SS (Slave Select, GPIO7)** : Sélection du périphérique SPI

---

### **4. Broches de Communication I2C (Inter-Integrated Circuit)**

Utilisé pour connecter plusieurs périphériques comme des capteurs, des ==**écrans OLED**==, etc. :

- **SDA (GPIO8)** : Ligne de données I2C
- **SCL (GPIO9)** : Ligne d’horloge I2C

---

### **5. Broches de Communication UART (Universal Asynchronous Receiver-Transmitter)**

Utilisé pour la communication série avec des modules comme un GPS, un module Bluetooth, un PC (via un adaptateur USB-TTL) :

- **RX (Réception, GPIO20)** : Réception des données série
- **TX (Transmission, GPIO21)** : Transmission des données série

---

### **6. Broches d’Entrée/Sortie Numérique (GPIO)**

Les GPIO (General Purpose Input Output) sont des broches polyvalentes qui peuvent être configurées comme entrées ou sorties :

- **GPIO0 - GPIO10 et GPIO20 - GPIO21**
    - Peuvent être utilisées pour contrôler des LEDs, des relais, des moteurs, ou lire des boutons, capteurs, etc.
    - Certaines de ces broches ont des fonctions secondaires (comme SPI, I2C, UART)