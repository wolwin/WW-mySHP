# WW-mySHP - SHP_HB-SCI-4-O-Gar118x

[Zurück zur Übersicht ...](../README.md)

#### Projekt-Beschreibung

Anschluß von GARDENA Bodenfeuchte- und Regensensor 118x an eine Homematic Zentrale mit 'AskSin++' Modul 'HB-UNI-Mini-X' (oder 'HB-UNI-Sens-X') und der Sensorplatine 'Sens-Gar-118x'. Es können auch statt der GARDENA Geräte potentialfreie Schalter angeschlossen werden.

  - GARDENA - Bodenfeuchtesensor 1188-20 [(Bedienungsanleitung)](./bin/GARDENA_Anleitung_1188-20_Feuchtesensor.pdf)
<br><br>
![WW-mySHP - HB-SCI-4-O-Gar118x](./img/Gardena_1188-20_pic.jpg "GARDENA - Bodenfeuchtesensor 1188-20")
<br><br>
  - GARDENA - Regensensor electronic 1189-20 [(Bedienungsanleitung)](./bin/GARDENA_Anleitung_1189-20_Regensensor.pdf)
<br><br>
![WW-mySHP - HB-SCI-4-O-Gar118x](./img/Gardena_1189-20_pic.jpg "GARDENA - Regensensor electronic Gardena_1189-20")

Alle 5 Minuten wird der Status der angeschlossenen GARDENA 118x Sensoren (bzw. potential freien Schaltern) überprüft (feucht / trocken und Leitungsstatus) und bei Änderung an die Homematic Zentrale geschickt. Eine Ruhestromaufnahme von nur 11 uA mit 3 AA Batterien soll eine langfristige Laufzeit garantieren.

#### Aufbau
Das Gerät besteht aus zwei Teilen: der Sensor-Platine 'Sens-Gar-118x' (Platinenbestückung incl. Spannungsversorgung 4 - 9 V) und dem 'AskSin++' Modul (minimale Bestückung):
  - SHP-Projekt 'Sens-Gar-118x' - [Zeigen ...](https://github.com/wolwin/WW-mySHP/blob/master/SHP_Sens-Gar-118x/README.md "Zeigen ...")
  - SHP-Projekt 'HB-UNI-Mini-X' - [Zeigen ...](https://github.com/wolwin/WW-mySHP/blob/master/SHP_HB-UNI-Mini-X/README.md "Zeigen ...")

#### Konfiguration

#### INO-Script

#### 3D-Print
- 3D-Druck Projekte für 'HB-SCI-4-O-Gar118x' - [Zeigen ...](https://github.com/wolwin/WW-my3DP/blob/master/README.md)

#### Bilder

#### Historie
- 2020-01-10 - Erstveröffentlichung
