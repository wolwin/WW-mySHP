# WW-mySHP - HB-UNI-Sens-X

[Zurück zur Übersicht ...](../README.md)

#### Projekt-Beschreibung

Universielle 'AskSin++' Platine mit verschiedenen Sensor Anschluß- und Konfigurationsmöglichkeiten im THT-Format. Eine Einbau- bzw. Montagemöglichkeit kann über vier 2 mm Platinen-Löcher realisiert werden.

Ziel des Projektes war, eine universielle Platine im THT-Format (=> 'Through Hole Technology') zu erstellen, bei der unterschiedliche Sensoren für unterschiedliche 'AskSin++' Projekte angeschlossen werden können. Gleichzeitig sollte hardwareseitig ein Batterie-Betrieb mit möglichst geringer Stromaufnahme sichergestellt werden - alternativ sollte auch der Betrieb an einer externen Festspannung (4-9 V) möglich sein.
Dabei fiel die Wahl auf einen 'Step-Down' LDO (Low Drop-Out) Spannungsregler, da dieser sowohl einen Batterie- als auch Festspannungsbetrieb möglich macht - ein größerer Raumbedarf für die Batterien / Akkus wurde dabei bewußt in Kauf genommen.

Eine ausführliche Darstellung dazu hier:



#### Platine
- Platine 'HB-UNI-Sens-X' - [Zeigen ...](https://github.com/wolwin/WW-myPCB/blob/master/PCB_HB-UNI-Sens-X/README.md)

#### Bilder
- Übersicht - 'HB-UNI-Sens-X'
  - Vollausstattung mit allen Optionen
  - I2C-Bus, 1-Wire und die freien Ports des 'Arduino Mini Pro' sind über JST-XH Buchsen herausgeführt (oben links und unten rechts)
  - Anschluß der Spannungsversorgung erfolgt ebenfalls über eine JST-XH Buchse (oben rechts - die Eingangsspannung ist hier für 4-9 V konfiguriert)
<br><br>
- 'HB-UNI-Sens-X' Draufsicht
<br><br>
![WW-mySHP - HB-UNI-Sens-X](./img/SHP_HB-UNI-Sens-X_01.jpg "HB-UNI-Sens-X")
<br><br>
- 'HB-UNI-Sens-X' mit gesockeltem Sendemodul
<br><br>
![WW-mySHP - HB-UNI-Sens-X](./img/SHP_HB-UNI-Sens-X_02.jpg "HB-UNI-Sens-X")
<br><br>

#### Historie
- 2020-01-10 - Erstveröffentlichung
