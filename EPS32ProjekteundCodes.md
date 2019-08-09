# EPS32 Projekte und Codes

## analogen Potentiometer auslesen
```
void setup() {
  Serial.begin(115200);
  pinMode(34, INPUT);
}

void loop() {
  Serial.println(analogRead(34));
  delay(100);

}
```

![](https://i.imgur.com/XcMYdMa.jpg)



## Built-in LED blinken lassen
### Code
```
#define LED_BUILTIN 1
 
void setup()
{
  pinMode(LED_BUILTIN, OUTPUT);
}
 
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(500);                        // wait for a second
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  delay(500);                        // wait for a second
}
```

![](https://i.imgur.com/Lpo3EBl.jpg)

## Accesspoint mit Webserver
Code von Idee von http://esp32-server.de/

```
#include <WiFi.h>
#include <WiFiClient.h>
#include <WebServer.h>
 
const char indexHTML[] PROGMEM = R"=====(
<!DOCTYPE html>
<html>
 <head>
  <title>Erstes Programm</title>
  <meta http-equiv="content-type" content="text/html; charset=UTF-8">
  <meta name=viewport content="width=device-width, initial-scale=1"> 
 </head>
 <body>
            <h1 style="text-align: center;">Willkommen in deiner CLOUD</h1>
 </body>
</html>
)=====" ;
 
WebServer server(80);
IPAddress apIP(192, 168, 1, 1);
 
void setup(void)
{
  Serial.begin(115200); //
  Serial.print("");
  WiFi.mode(WIFI_AP);
  WiFi.softAPConfig(apIP, apIP, IPAddress(255, 255, 255, 0));
  WiFi.softAP("Martin Router King", "ihaveastream"); // Name und Passwort des Wi-Fi netzes
  server.on("/", Ereignis_Index);
  server.onNotFound(handleNotFound);
  delay(500);          // Abwarten 0,5s
  server.begin();
  Serial.println("HTTP Server gestartet");
}
 
void Ereignis_Index()    // Wird ausgeführt wenn "http://<ip address>/" aufgerufen wurde
{
  server.send(200, "text/html", indexHTML);      //dann Index Webseite senden 
}
 
void handleNotFound()
{
  server.send(404, "text/plain", "File Not Found\n\n");
}
 
void loop(void) 
{
  server.handleClient();
}
```


## DHT 22 Sensor auslesen
https://circuits4you.com/2019/01/25/esp32-dht11-22-humidity-temperature-sensor-interfacing-example/


### Pin referenz
https://randomnerdtutorials.com/esp32-pinout-reference-gpios/


## 20+ ESP32 Projects and Tutorials
https://randomnerdtutorials.com/projects-esp32/
* ESP32 DHT11/DHT22 Web Server – Temperature and Humidity using Arduino IDE https://randomnerdtutorials.com/esp32-dht11-dht22-temperature-humidity-web-server-arduino-ide/
* https://funduino.de/nr-03-433mhz-funkverbindung
* https://circuits4you.com/2019/01/25/esp32-dht11-22-humidity-temperature-sensor-interfacing-example/
* http://esp32-server.de/
* https://randomnerdtutorials.com/alexa-echo-with-esp32-and-esp8266/
* 


# Ardublocky mit ESP32 auf MacOS:

Nun sollte der ESP unter ArduinoIDE anzusprechen sein [Ardublocky herunterladen](https://open.hpi.de/courses/mikrocontroller2019/items/7mYNCZVQuJhS6bUfs6e0F) 
- [macOS_Ardublockly.zip](https://drive.google.com/file/d/1qAXS3Zjnokmcj4SSpR4fH2hY3V5i9KZ1/view?usp=sharing)
- (bei mir kam auch erst eine Fehlermeldung von google)und entpacken Das Programm lässt sich standardmäßig nicht sofort installieren, weil es nicht von Apple verifiziert ist. Nach dem ersten Doppelklick kommt eine Fehlermeldung. In der Systemeinstellung vom Mac auf Sicherheit gehen und unter Allgemein die Installation des aus dem Web geladenen Programms trotzdem erlauben. Noch einmal Das Programm-Icon doppelklicken und auf öffnen gehen. Nun sollte das Programm starten. Das Programm in den (MAC)Programmordner verschieben. Ardublockly konfigurieren (Ardublockly -> Preferences Compiler location: Mac-Typisch den Pfad zum Programm ArduinoIDE unter Programme auswählen und die ArduinoIDE auswählen Arduino Board: ESP32 Dev Module COM Port: /dev/cu.SLAB_USBtoUART 
![](https://i.imgur.com/rnAagSO.png)