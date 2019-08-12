---
tags: Arduino, cpp, DHT22
disqus: joerglohrer
---

# DHT22 Sensor am Arduino UNO

## <i class="fa fa-wrench fa-fw"></i> Aufbau
![](https://i.imgur.com/LBGz9AD.png)

## <i class="fa fa-code fa-fw"></i> Code
```cpp=
#include "DHT.h" //DHT Bibliothek laden

#define DHTPIN 2 //Der Sensor wird an PIN 2 angeschlossen    

#define DHTTYPE DHT22    // Es handelt sich um den DHT22 Sensor

DHT dht(DHTPIN, DHTTYPE); //Der Sensor wird ab jetzt mit „dth“ angesprochen

void setup() {
  Serial.begin(9600); //Serielle Verbindung starten

  dht.begin(); //DHT22 Sensor starten
}

void loop() {
  
  delay(2000); //Zwei Sekunden Vorlaufzeit bis zur Messung (der Sensor ist etwas träge)

  
  float Luftfeuchtigkeit = dht.readHumidity(); //die Luftfeuchtigkeit auslesen und unter „Luftfeuchtigkeit“ speichern
  
  float Temperatur = dht.readTemperature();//die Temperatur auslesen und unter „Temperatur“ speichern
  
  Serial.print("Luftfeuchtigkeit: "); //Im seriellen Monitor den Text und 
  Serial.print(Luftfeuchtigkeit); //die dazugehörigen Werte anzeigen
  Serial.println(" %");
  Serial.print("Temperatur: ");
  Serial.print(Temperatur);
  Serial.println(" Grad Celsius");

}
```
## <i class="fa fa-bullseye fa-fw"></i> Ergebnis
![](https://i.imgur.com/8nzOBfs.png)



## <i class="fa fa-bug fa-fw"></i> Mögliche Fehlerquellen: 
:::danger
**Baud-Rate des seriellen Monitors** 
* Im seriellen Monitor muss die gleiche Baudrate wie im Code eingestellt sein (hier: `Serial.begin(9600);`), damit die Ausgabe funktioniert:
![](https://i.imgur.com/5hPYz2b.png)
:::

## <i class="fa fa-link fa-fw"></i> Weitere Quellen:
* https://www.bastelgarage.ch/index.php?route=extension/d_blog_module/post&post_id=1
