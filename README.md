# LoRaSoundsensor

Dieses Projekt beschreibt den Aufbau eines Soundsensors auf der Basis des Projektes LoraSoundkit (https://github.com/meekm/LoRaSoundkit)

![alt text](https://github.com/CargoBikoMeter/LoRaSoundsensor/blob/main/AKIOT-Soundsensor-2025--002.jpeg)

Soundsensor Bauanleitung
========================
Update 12.01.2025: Die bisher verwendete CPU Heltec ESP32 LoRa V2 wurde gegen die CPU LILYGO® TTGO LoRa32 V2.1_1.6 Version 868 ersetzt, da die neue Heltec CPU ESP32 LoRa V3 wegen dem dort verwendeten LoRa-Modul SX1262 nicht von der LMIC Bibliothek unterstützt wird.

Teile:
- OB T60 IP66 Abzweigdose 114x114x57 mm Art.Nr 315562 Emil Lux GmbH & Co KG (OBI Markt)
- Lochrasterplatine 5x7 cm 24x18 Raster
- 2 x 13er Pinheader, bei Bedarf längere Pin-Header kürzen, indem der 14. Pin herausgezogen und mit einem Seitenschneider an dieser Stelle abgeschnitten wird
- 2 x Kabelklemmblock 2-polig blau für Leiterplattenmontage zum Fixieren der USB-Kabel (z.B. Berrybase)
- optional zur 3V-Spannungsstabilisierung: 100µF/10V Elko, 100nF Kondensator
- 5 x Drahtbrücke, isoliert
- CPU: LILYGO® TTGO LoRa32 V2.1_1.6 Version 868 (https://lilygo.cc/products/lora3)
- MES-Sensor SPH0645 inkl. Dupont Jumperkabel (https://www.amazon.de/dp/B08218WSXH?psc=1&ref=ppx_yo2ov_dt_b_product_details)
- Stiftleiste 5-polig für MES-Sensor (https://www.berrybase.de/stiftleiste-1x-40-polig-rm-2-54-gewinkelt)
- 16 mm Plastikrohr OBI-Baumarkt für MES-Sensor 
- M25 x 1,5 (37,3 mm x 25 mm) IP68 Kabelverschraubung für 16 mm Rohr, Emil Lux GmbH (OBI-Baumarkt)
- UHU Plus Schnellfest 2-K-Expoxidharzkleber
- Mikrofonschutzmenbran 4 mm Durchmesser - LY-RN-AF04-700400-BD009 (Alibaba)
- 1 m USB-C Pigtail Kabel vieradrig mit Lötanschluss
- 30 cm Mikro USB Kabel vierpolig mit Winkelstecker und Lötanschluss
- Kabelverschraubung PG7 für das USB-C Pigtail Kabel
- 12 mm Druckausgleichsschraube Plastik (https://www.rst.eu/de/produkte/druckausgleichsloesungen/produkt/dae-pa-kunststoff/11087512-1.html?no_cache=1)
- Soundlevel Meter Tadeto SL720 für Testsignalmessung/Evaluierung

Aufbau:
- offenen Gehäuseboden so hinlegen, dass der einzelne Kabelausgang nach links zeigt
- Kabelverschraubung M25 in die linke mittige Öffnung nach Entfernen des Stopfens einschrauben, dabei vorher noch das störende Befestigungsloch im Boden etwas entfernen
- Kabelverschraubung PG7 unten links und die Druckausgleichsschraube unten rechts in die Plastikstopfen des Gehäuses einbauen. Dazu in die Stopfen passende Löcher schneiden.

- Platine bestücken
  - 13er Pin-Headers auf die CPU stecken und die CPU ganz links und unten auf der Platine positionieren und Pin-Header anlöten
  - Kabelklemmblock links hochkant über der CPU einstecken und anlöten
  - von der gewinkelten Stiftleiste eine 5-polige Leiste abknipsen
  - Stiftleiste mit dem kurzen Stift einlöten.
  - 100µF Elko in Pins anlöten, Minus an linken Stift (von oben gesehen), Plus an Stift rechts daneben
  - 100nF Kondensator parallel zum Elko anlöten

Es gilt folgende Belegung der Stiftleiste von oben gesehen, Stift 1 ist links:
- Stift - MES - CPU - Kabel 
- 1:  GND  GND      blau
- 2:  VDD  3.3V     violett
- 3:  SD   GPIO0    grau 
- 4:  WS   GPIO12   weiß
- 5:  SCK  GPIO35   schwarz


Der MES-Anschluss L/R wird nicht verwendet und daher nicht beschaltet.
- MES-Sensor: 
  - den L/R-Anschluss am MES-Modul belöten, damit später keine Feuchtigkeit durch das leere Lötauge in das Rohr eindringen kann
  - mit angelötetem und nicht auf ein Potential gelegtes Jumperkabel gibt es Messfehler, da dann über 90 dBA im ruhigen Raum gemessen werden
  - MES-Sensor an das Dupont-Kabel anlöten (siehe Stiftleistenbelegung oben), dazu die Kabel auf der Steckerseite 16 cm Länge abschneiden, auf der anderen Seite müssen die Buchsen sein (Mikrofonloch zeigt nach außen)

- das USB-C Pigtail Kabel durch die PG7-Kabelverschraubung stecken, die vier Adern mit dem Mikro-USB Pigtail Kabel verlöten und im Kabelklemmblock fixieren
- CPU auf den Sockel stecken, Mikro-USB-Winkelstecker in CPU einstecken, Jumperkabel des Mikrofonrohres anstecken und das USB-C-Kabel am PC anschließen
- in Visual Studio Code den Parameter CYCLETIME 60 setzen, damit Testmessungen gemacht werden können

Nun mit dem Soundlevel Meter und dem Online Sinus Generator (https://onlinetonegenerator.com/) Testmessungen machen.
Es wird nach der Einstellung eines Pegels jeweils mehrere Minuten lang gemessen.

- Pegel Level Meter:        Messwert auf Display
- 60 dBA:                   58,2 dBA
- 70 dBA:                   69,6 dBA
- 80 dBA:                   79,1 dBA
- 90 dBA:                   89,3 dBA

Test bestanden, die Abweichung ist nicht größer als 2 dBA.

Nun das Mikrofon in das Plastikrohr mittels 2-Komponentenkleber mit 5 Minuten Verarbeitungszeit einkleben. Zum Schutz des außen liegenden Mikrofoneingangs vor externer Feuchtigkeit wird dieser mit der runden Mikrofonschutzmenbran ( 4mm ) abgedeckt. Das Plastikrohr vorne innen etwas aufrauen. Jeweils 1 cm Komponentenkleber mischen und in das Rohr einfüllen. Zum Schluss den MES-Sensor vorsichtig an den Jumperkabeln hineinziehen und das Rohr senkrecht minimal 5 Minuten festhalten, damit der Kleber nach unter läuft. Vorsichtig etwas Expoxidharzkleber auf die Außenseite des Sensors auftragen, um die Leiterbahnen gegen Witterungseinflüsse zu versiegeln (BEACHTE: Kleber NICHT auf die Mikrofonschutzmenbran auftragen!)

Nach ca. 20 Minuten ist der Kleber handfest ausgehärtet. Kleber vollständig ausgehärten lassen, erst danach das Mikrofonrohr ins Gehäuse einbauen
  
Nach Trocknung des Komponentenklebers das Plastikrohr mit dem MES-Sensor in die M25 Kabelverschraubung montieren und die Jumperkabel mit der Platine verbinden. Zur Fixierung des Plastikrohres in der M25-Verschraubung am Ende des Rohres einen Ausgleichgummi in die Verschraubung einlegen bzw. um das Plastikrohr wickeln.

Zum Abschluss den finalen Test nochmals mit dem Soundlevel Meter durchführen.

Vor der Integration des Sensors in das TheThingsNetwork (TTN) den Parameter CYCLETIME 240 setzen, damit die Fair Use Policy des TTN nicht verletzt wird. Dadurch sendet der Sensor die Daten alle vier Minuten über das TTN. 

HINWEIS: Die obige Aufbauanleitung ist ohne Gewähr durch den Autor. 

Viel Spaß beim Basteln!

