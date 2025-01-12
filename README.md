# LoRaSoundsensor

Dieses Projekt beschreibt den Aufbau eines Soundsensors auf der Basis des Projektes LoraSoundkit (https://github.com/meekm/LoRaSoundkit)

![alt text](https://github.com/CargoBikoMeter/LoRaSoundsensor/blob/main/AKIOT-Soundsensor--Balkon-02.jpeg)

Soundsensor Bauanleitung
========================
Update 12.01.2025: Die bisher verwendete CPU Heltec ESP32 LoRa V2 wurde gegen die CPU LILYGO® TTGO LoRa32 V2.1_1.6 Version 868 ersetzt, da die neue Heltec CPU ESP32 LoRa V3 wegen dem dort verwendeten LoRa-Modul SX1262 nicht von der LMIC Bibliothek unterstützt wird.
Teile:
- OBO T60 IP66 Abzweigdose 114x114x57 mm Art.Nr 315562 Emil Lux GmbH & Co KG (OBI Markt)
- Lochrasterplatine 5x7 cm 24x18 Raster mit Beschriftung 0-24/A-R
- 2 x 13er Pinheader, bei Bedarf längere Pin-Header kürzen, indem der 19. Pin herausgezogen und mit einem Seitenschneider an dieser Stelle abgeschnitten wird
- Schraube 3x10 mm zum Befestigen der Lochrasterplatine im Gehäuseboden
- Kabelklemmblock 4-polig blau für Leiterplattenmontage zum Fixieren der USB-Kabel
- optional zur 3V-Spannungsstabilisierung: 100µF/10V Elko, 100nF Kondensator
- Drahtbrücke, isoliert
- CPU: LILYGO® TTGO LoRa32 V2.1_1.6 Version 868
- MES-Sensor SPH0645 inkl. Dupont Jumperkabel (https://www.amazon.de/dp/B08218WSXH?psc=1&ref=ppx_yo2ov_dt_b_product_details)
- Stiftleiste 5-polig für MES-Sensor (https://www.berrybase.de/stiftleiste-1x-40-polig-rm-2-54-gewinkelt)
- 16mm Plastikrohr OBI-Baumarkt für MES-Sensor
- M25 x 1,5 (37,3 mm x 25 mm) IP68 Kabelverschraubung, Emil Lux GmbH (OBI-Baumarkt)
- UHU Plus Schnellfest 2-K-Expoxidharzkleber
- Mikrofonschutzmenbran 7 mm Durchmesser - LY-RN-AF04-700400-BD009 (Alibaba)
- 1 m USB-C Pigtail Kabel vieradrig mit Lötanschluss
- 30 cm USB Mikro Kabel vierpolig mit Winkelstecker und Lötanschluss
- Kabelverschraubung PG7 für das USB-C Stromkabel
- 12 mm Druckausgleichsschraube Plastik (https://www.rst.eu/de/produkte/druckausgleichsloesungen/produkt/dae-pa-kunststoff/11087512-1.html?no_cache=1)
- Soundlevel Meter Tadeto SL720 für Testsignalmessung/Evaluierung

Aufbau:
- Befestigungsloch 3 mm in Platine bei G23 bohren
- offenen Gehäuseboden so hinlegen, dass der einzelne Kabelausgang nach links zeigt
- Platine mit der Schraube im oberen mittigen Befestigungsloch festschrauben
- nun die 13er Pin-Headers auf die CPU stecken und die CPU ganz links und unten auf der Platine positionieren und Pin-Header anlöten
- Kabelklemmblock links hochkant über der CPU einstecken und anlöten
- von der gewinkelten Stiftleiste eine 5-polige Leiste abknipsen
- Stiftleiste mit dem kurzen Stift einlöten.
- 100nF Kondensator anlöten
- 100µF Elko in Pins anlöten
- vom 100µF-Elko alle Lötaugen in Richtung CPU verbinden 
- 5V Pin (1B) des Kabelklemmblockes mit dem 5V-Pin der CPU (5R) mit einer Drahtbrücke verbinden.


Es gilt folgende Belegung:

Stift  MES  CPU                        AZ-Delivery Kabel
=========================================================
 - GND                             Kabel: blau
 - VDD  (3V)                       Kabel: violett
 - SD   CPU Pin 3 (data_in_num)    Kabel: grau 
 - WS   CPU Pin 7 (ws_io_num)      Kabel: weiß
 - SCK  CPU Pin 9 (bck_io_num)     Kabel: schwarz
 - L/R  wird nicht verwendet und daher nicht beschaltet.
 
- den L/R-Anschluss am MES-Modul belöten, damit später keine Feuchtigkeit durch das leere Lötauge in das Rohr eindringen kann
- mit angelötetem und nicht auf ein Potential gelegtes Jumperkabel gibt es Messfehler, da dann über 90 dBA im ruhigen Raum gemessen werden
- Kabelverschraubung M25 in die linke mittige Öffnung nach Entfernen des Stopfens einschrauben.
- MES-Sensor an das Dupont-Kabel anlöten, dazu die Kabel auf der Steckerseite 16 cm Länge abschneiden, auf der anderen Seite müssen die Buchsen sein
- Buchsen auf die Steckerleiste und die Kabel durch das Platikrohr stecken, nun die Kabelenden 3mm abisolieren, fest verdrillen und am MES-Sensor anlöten 
- CPU auf den Sockel stecken, die Jumperkabel anstecken und mittels USB-Micro-Kabel an PC anschließen
- in Visual Studio Code den Parameter CYCLETIME 60 setzen, damit Testmessungen gemacht werden können.

Nun mit dem Soundlevel Meter und dem Online Sinus Generator (https://onlinetonegenerator.com/) Testmessungen machen.
Es wird nach der Einstellung eines Pegels jeweils mehrere Minuten lang gemessen.

Pegel Level Meter       Messwert auf Display
60 dBA:                   58,2 dBA
70 dBA:                   69,6 dBA
80 dBA:                   79,1 dBA
90 dBA:                   89,3 dBA

Test bestanden, die Abweichung ist nicht größer als 2 dBA.

Nun das Mikrofon in das Plasterohr mittels 2-Komponentenkleber mit 5 Minuten Verarbeitungszeit einkleben. Zum Schutz des außen liegenden Mikrofoneingangs vor externer Feuchtigkeit wird dieser mit einer runden Membran abgedeckt. Das Plasterohr vorne innen etwas aufrauen. Jeweils 3 cm Komponentenkleber mischen und in das Rohr einfüllen. Zum Schluss den MES-Sesor vorsichtig an den Jumperkabeln hineinziehen und das Rohr senkrecht 5 Minuten festhalten und danach senkrecht hinstellen, damit der Kleber nach unter läuft. Nach 20 Minuten ist der Kleber handfest ausgehärtet. 
  
Nun die Kabelverschraubung PG7 und die Druckausgleichsschraube in die beiden unteren Plastikstopfen des Gehäuses einbauen. Dazu mit einer heißen Nadel in die Stopfen passende Löcher ausstechen.  
Die Platine mit der 3 mm Schraube im Gehäuse befestigen und das USB-C Pigtail-Kabel mit dem Kabelklemmblock verbinden. Nach Trocknung des Komponentenklebers das Plasterohr mit dem MES-Sensor in die M25 Kabelverschraubung montieren und die Jumperkabel mit der Platine verbinden.

Zum Abschluss den finalen Test nochmals mit dem Soundlevel Meter durchführen.

Viel Spaß beim Basteln!

