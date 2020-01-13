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
Das Gerät besteht aus zwei Teilen: der Sensor-Platine 'Sens-Gar-118x' (Platinenbestückung incl. Spannungsversorgung 4 - 9 V) und dem 'AskSin++' Modul (minimale Platinenbestückung):
  - SHP-Projekt 'Sens-Gar-118x' - [Zeigen ...](https://github.com/wolwin/WW-mySHP/blob/master/SHP_Sens-Gar-118x/README.md "Zeigen ...")
  - SHP-Projekt 'HB-UNI-Mini-X' - [Zeigen ...](https://github.com/wolwin/WW-mySHP/blob/master/SHP_HB-UNI-Mini-X/README.md "Zeigen ...")

Zwischen den Platinen müssen noch folgende Kabelverbindungen hergestellt werden:

  | **Sens-Gar-118x** | **HB-UNI-Mini-X** |
  | --- | --- |
  | GND | GND |
  | PA0 | A1 |
  | PA1 | A2 |
  | PA2 | A3 |
  | PA3 | PD5 |
  | PA4 | PD6 |
  | VCC | VCC |

#### Konfiguration

Die Anschlußkonfiguration und das Erscheinungsbild in der Homematic Zentrale (Anzahl / Bedeutung der Schalter) wird mit Hilfe der Jumper J1 und J2 auf der Sensor-Platine 'Sens-Gar-118x' und in der Datei 'HB-SCI-4-O-Gar118x.h' über die Defines 'CHANNEL_COUNT', 'CHANNEL_PINS' und 'CHANNEL_DEBUG' festgelegt.

  - Als Default-Einstellung ist der Anschluß von zwei GARDENA Geräten voreingestellt:

        Variante 2 - mit Fehler-Kanal (default)
        Platine
        Jumper  : J1 = OFF  J2 = OFF
        Inp-Gar1: Gardena 1188-20 (Feuchte)
        Inp-Gar2: Gardena 1189-20 (Regen)

- Übersicht Anschluß-Varianten 'Sens-Gar-118x' - [Zeigen ...](./bin/HB-SCI-4-O-Gar118x_Varianten.pdf "Zeigen ...")
- Detail Anschluß-Varianten 'Sens-Gar-118x' - [Zeigen ...](./bin/HB-SCI-4-O-Gar118x_Varianten.txt "Zeigen ...")

#### INO-Script
[Download ...](./bin/HB-SCI-4-O-Gar118x_20191228.zip)

#### Inbetriebnahme
- Zur Inbetriebnahme werden im ersten Schritt _keine_ Geräte an das 'Sens-Gar-118x' Sensor-Modul angeschlossen.
- Über den Punkt 'HM Gerät anlernen' wird der Anlernprozeß in der WebUI der Homematic Zentrale gestartet - auf dem 'AskSin++' Modul wird dann der Taster S1 kurz gedrückt. Nach dem erfolgreichen Anmelden findet sich das neue Gerät im Posteingang zur Übernahme.
<br><br>
![WW-mySHP - HB-SCI-4-O-Gar118x](./img/SHP_HB-SCI-4-O-Gar118x_Betrieb_01.jpg "HB-SCI-4-O-Gar118x")
<br><br>
- Nach der Übernahme  wird unter 'Einstellungen / Geräte' in der WebUI das 'HM-SCI-3-FM GAR118X-01' Gerät gesucht und zur Konfiguration aufgeklappt:
<br><br>
![WW-mySHP - HB-SCI-4-O-Gar118x](./img/SHP_HB-SCI-4-O-Gar118x_Betrieb_02.jpg "HB-SCI-4-O-Gar118x")
<br><br>
- Für jeden Kanal muß nun der Übertragungsmodus auf 'Standard' eingestellt werden:
<br><br>
![WW-mySHP - HB-SCI-4-O-Gar118x](./img/SHP_HB-SCI-4-O-Gar118x_Betrieb_03.jpg "HB-SCI-4-O-Gar118x")
![WW-mySHP - HB-SCI-4-O-Gar118x](./img/SHP_HB-SCI-4-O-Gar118x_Betrieb_04.jpg "HB-SCI-4-O-Gar118x")
<br><br>
- Nun muß das 'AskSin++' Modul neu gestartet werden (Spannung kurz unterbrechen). Unter 'Status und Bedienung / Geräte' in der WebUI zeigt das Gerät 'HM-SCI-3-FM GAR118X-01' die folgenden Kanal-Stellung an - da ja noch nichts angeschlossen ist, zeigen die beiden Fehler-Kanäle 'Offen' an:
<br><br>
![WW-mySHP - HB-SCI-4-O-Gar118x](./img/SHP_HB-SCI-4-O-Gar118x_Betrieb_07.jpg "HB-SCI-4-O-Gar118x")
<br><br>
- Mit dem Anschluß der Gardena Geräte ist die Grundeinstellung abgeschlossen: der Leitungsstatus wechselt auf 'ok' (='verschlossen') und der Gardena 118x Status wird angezeigt.

#### Gardena 118x Status
- Die Gardena 118x Sensoren unterscheiden zwischen 'trocken' und 'feucht' - hier eine Übersicht:
<br><br>
![WW-mySHP - HB-SCI-4-O-Gar118x](./img/SHP_HB-SCI-4-O-Gar118x_Betrieb_08.jpg "HB-SCI-4-O-Gar118x")
![WW-mySHP - HB-SCI-4-O-Gar118x](./img/SHP_HB-SCI-4-O-Gar118x_Betrieb_09.jpg "HB-SCI-4-O-Gar118x")
![WW-mySHP - HB-SCI-4-O-Gar118x](./img/SHP_HB-SCI-4-O-Gar118x_Betrieb_10.jpg "HB-SCI-4-O-Gar118x")
![WW-mySHP - HB-SCI-4-O-Gar118x](./img/SHP_HB-SCI-4-O-Gar118x_Betrieb_11.jpg "HB-SCI-4-O-Gar118x")

#### 3D-Print
- 3D-Druck Projekte für 'HB-SCI-4-O-Gar118x' - [Zeigen ...](https://github.com/wolwin/WW-my3DP/blob/master/3DP_OBO_T40_HB/README.md)

#### Bilder
- Testaufbau ['Sens-Gar-118x'](https://github.com/wolwin/WW-mySHP/blob/master/SHP_Sens-Gar-118x/README.md) mit ['HB-UNI-Sens-X'](https://github.com/wolwin/WW-mySHP/blob/master/SHP_HB-UNI-Sens-X/README.md) auf ['OBO-T40-HB-Sockel'](https://github.com/wolwin/WW-my3DPP/blob/master/3DP_OBO_T40_HB/README.md).
<br><br>
![WW-mySHP - HB-SCI-4-O-Gar118x](./img/SHP_HB-SCI-4-O-Gar118x_01.jpg "HB-UNI-Sens-X und Sens-Gar-118x")
<br><br>

#### Historie
- 2020-01-10 - Erstveröffentlichung
