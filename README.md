# LoRaSoundsensor

Dieses Projekt beschreibt den Aufbau eines Soundsensors auf der Basis des Projektes [LoraSoundkit](https://github.com/meekm/LoRaSoundkit)

![alt text](https://github.com/CargoBikoMeter/LoRaSoundsensor/blob/main/AKIOT-Soundsensor-2025--002.jpeg)

Soundsensor Bauanleitung
========================
Update 12.01.2025: Die bisher verwendete CPU Heltec ESP32 LoRa V2 wurde gegen die CPU LILYGO® TTGO LoRa32 T3_V1.6.1 ersetzt, da die neue Heltec CPU ESP32 LoRa V3 wegen dem dort verwendeten LoRa-Modul SX1262 nicht von der LMIC Bibliothek unterstützt wird.

Teile:
- OB T60 IP66 Abzweigdose 114x114x57 mm Art.Nr 315562 Emil Lux GmbH & Co KG (OBI Markt)
- Lochrasterplatine 5x7 cm 24x18 Raster
- 2 x 13er Pinheader, bei Bedarf längere Pin-Header kürzen, indem der 14. Pin herausgezogen und mit einem Seitenschneider an dieser Stelle abgeschnitten wird
- 2 x Kabelklemmblock 2-polig blau für Leiterplattenmontage zum Fixieren der USB-Kabel (z.B. Berrybase)
- optional zur 3V-Spannungsstabilisierung: 100µF/10V Elko, 100nF Kondensator
- 5 x Drahtbrücke, isoliert
- CPU: LILYGO® TTGO LoRa32 T3_V1.6.1
- MEMS-Mikrofon: INMP441
- Dupont Jumperkabel - BerryBase DUPK-40-FM-20 (wird auf 14 cm gekürzt)
- Stiftleiste 5-polig für MEMS-Mikrofon - BerryBase 1 x 40 polig, PINH-1X40P-90
- 16 mm Plastikrohr OBI-Baumarkt für MES-Sensor (Stück mit 10 cm Länge abschneiden) 
- M25 x 1,5 (37,3 mm x 25 mm) IP68 Kabelverschraubung für 16 mm Rohr, Emil Lux GmbH (OBI-Baumarkt)
- UHU Plus Schnellfest 2-K-Expoxidharzkleber, 5 Minuten transparent
- Mikrofonschutzmenbran 7 mm Durchmesser - LY-RN-AF04-700400-BD009 (Alibaba)
- 1 m USB-C Pigtail Kabel vieradrig mit Lötanschluss
- 30 cm Mikro USB Kabel vierpolig mit Winkelstecker und Lötanschluss
- Kabelverschraubung PG7 für das USB-C Pigtail Kabel
- 12 mm Druckausgleichsschraube Plastik, schwarz - Reichelt, DELOCK 60479
- 3 m USB-C Flachbandkabel, damit Kabel durch Fenster/Balkontür geführt werden kann (Amazon Itramax Flachbandkabelset)
- USB-C Adpater Buchse/Buchse zum Verbinden von USB-C Pigtail Kabel und USB-C Flachbandkabel
- USB-Steckernetzteil 1 W, BerryBase,  8013930 
- Soundlevel Meter Tadeto SL720 für Testsignalmessung/Evaluierung

Aufbau:
- offenen Gehäuseboden so hinlegen, dass der einzelne Kabelausgang nach links zeigt
- Kabelverschraubung M25 in die linke mittige Öffnung nach Entfernen des Stopfens einschrauben, dabei vorher noch das störende Befestigungsloch im Boden etwas entfernen
- Kabelverschraubung PG7 unten links und die Druckausgleichsschraube unten rechts in die Plastikstopfen des Gehäuses einbauen. Dazu in die Stopfen passende Löcher schneiden.

- Platine bestücken
  - 13er Pin-Headers auf die CPU stecken und die CPU im dritten Pin links und unten auf der Platine positionieren und Pin-Header anlöten
  - beide Kabelklemmblöcke mit der Nut zusammenstecken und links hochkant über der CPU mit den Kabelöffnungen nach außen einstecken und anlöten
  - von der gewinkelten Stiftleiste eine 5-polige Leiste abknipsen
  - Stiftleiste mit dem kurzen Stift in der neunten Reihe von links und dritten Reihe von oben einlöten
  - 100µF Elko in Pins anlöten, Minus an linken Stift (von oben gesehen), Plus an Stift rechts daneben
  - 100nF Kondensator parallel zum Elko anlöten

Es gilt folgende Belegung der Stiftleiste von oben gesehen, Stift 1 ist links, CPU-PIN (1.OL: erster Pin von oben links bei Antenne rechts oben gesehen, analog OR, UL und UR):
| Stift | MEMS    | CPU    |  PIN  |
|-------|---------|--------|-------|
|   1   | GND/L/R | GND    |  2UR  |
|   2   | VDD     | 3.3V   |  3UR  |
|   3   | SD      | GPIO0  |  5OL  | 
|   4   | WS      | GPIO12 |  7OL  |
|   5   | SCK     | GPIO35 |  3OR  |

Der MEMS-Mikrofon-Anschluss L/R wird direkt am MEMS-Mikrofon mit GND verbunden.

MEMS-Mikrofon verkabeln: 
  - den L/R-Anschluss am MEMS-Mikrofon mit GND verbinden
  - MEMS-Mikrofon an das gekürzte Dupont-Kabel anlöten (siehe Stiftleistenbelegung oben), dazu das Kabel von der Buchsenseite aus auf die Länge von 14 cm Länge kürzen (Hinweis: Mikrofonloch zeigt nach außen)

USB-C Pigtail Kabel durch die PG7-Kabelverschraubung stecken, die vier Adern mit dem Mikro-USB Pigtail Kabel verlöten und im Kabelklemmblock fixieren
CPU auf den Sockel stecken, Mikro-USB-Winkelstecker in CPU einstecken, Jumperkabel des Mikrofonrohres anstecken
USB-C Pigtail Kabel mittels USB-C-Adapter mit USB-C-Flachbandkabel verbinden am PC anschließen

Tip: Um die korrekte Funktion der angelöteten Mikrofonkabel zu testen, können die Jumper direkt auf die jeweiligen PINs der CPU gesteckt werden.

Test:
  - in PlatformIO den Parameter CYCLETIME 60 setzen, damit Testmessungen gemacht werden können
  - Code übersetzen und in das ESP32 Board laden
  - beim Start wird auf dem OLED-Display in der vorletzten Zeile die DEVEUI angezeigt, alternativ wird die DEVEUI im Log der PlatformIO-Konsole angezeigt
  - zusammen mit der in der Datei config.h definierten Werte APPEUI und APPKEY kann der Sensor nun im TTN registriert werden
  - Hinweis: Der Test kann nur durchgeführt werden, wenn sich der Sensor erfolgreich mit dem TTN verbinden kann!

Nun mit dem Soundlevel Meter und dem [Online Sinus Generator](https://onlinetonegenerator.com/) Testmessungen machen.
Es wird nach der Einstellung eines Pegels jeweils mehrere Minuten lang gemessen.

| Pegel Level Meter | Messwert auf Display |
|-------------------|----------------------|
|  60 dBA           |     58,2 dBA         |
|  70 dBA           |     69,6 dBA         |        
|  80 dBA           |     79,1 dBA         |
|  90 dBA           |     89,3 dBA         |

Test bestanden, die Abweichung ist nicht größer als 2 dBA.

Mikrofon im Rohr einkleben:

Nun das MEMS-Mikrofon in das 10 cm lange Plastikrohr mittels 2-Komponentenkleber mit 5 Minuten Verarbeitungszeit einkleben. Zum Schutz des außen liegenden Mikrofoneingangs vor externer Feuchtigkeit wird dieser mit der runden Mikrofonschutzmenbran ( 7 mm ) abgedeckt. Das Plastikrohr vorne innen etwas aufrauen. Jeweils 1 cm Komponentenkleber mischen und in das Rohr am Rand einfüllen. Das MEMS-Mikrofon vorsichtig an den Jumperkabeln hineinziehen. Vorsichtig etwas Expoxidharzkleber auf die Außenseite des Sensors auftragen, um die Leiterbahnen gegen Witterungseinflüsse zu versiegeln (BEACHTE: Kleber NICHT auf die Mikrofonschutzmenbran auftragen!). Das Rohr senkrecht minimal 5 Minuten festhalten, damit der Kleber nach unter läuft. 

Nach ca. 5 Minuten ist der Kleber handfest ausgehärtet. Kleber vollständig aushärten lassen, erst danach das Mikrofonrohr ins Gehäuse einbauen
  
Nach Trocknung des Komponentenklebers das Plastikrohr mit dem MEMS-Mikrofon in die M25 Kabelverschraubung montieren und die Jumperkabel mit der Platine verbinden. Zur Fixierung des Plastikrohres in der M25-Verschraubung am Ende des Rohres einen Ausgleichgummi in die Verschraubung einlegen bzw. um das Plastikrohr wickeln.

Zum Abschluss den finalen Test nochmals mit dem Soundlevel Meter durchführen.

Vor der Integration des Sensors in das TheThingsNetwork (TTN) den Parameter CYCLETIME 240 setzen, damit die [Fair Use Policy](https://www.thethingsnetwork.org/forum/t/fair-use-policy-explained/1300) des TTN nicht verletzt wird. Dadurch sendet der Sensor die Daten alle vier Minuten über das TTN. 

Die Beschreibung der TTN-Konfiguration und Weiterleitung der Messdaten zu openSenseMap.org erfolgt demnächst hier.

HINWEIS: Die obige Aufbauanleitung ist ohne Gewähr!

Viel Spaß beim Basteln!

