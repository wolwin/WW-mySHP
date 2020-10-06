# WW-mySHP - HM-LC-SW1-BA-PCB-GAR1251

[Zurück zur Übersicht ...](../README.md)

#### Projekt-Beschreibung

 Grundlage ist das 'Asksin++' Projekt 'Umbau GARDENA Bewässerungsventil (1251-20) 9V auf HomeMatic' von Gelegenheitsbastler:

[Original-Projekt zeigen ...](https://homematic-forum.de/forum/viewtopic.php?f=76&t=49719&p=498577&hilit=HomeMatic+Gardena+Ventil)

Bei der Inbetriebnahme der fertig aufgebauten Platine und dem Testen sind folgende Dinge aufgefallen:
- es findet keine durchgreifende Überprüfung der Batteriespannung statt ([siehe AskSin++ 'Dauersender / Babbling Idiot'](https://asksinpp.de/Grundlagen/FAQ/babbling_idiot.html))
- Einstellparameter aus der CCU werden nicht alle vom Modul übernommen

#### Änderungen
Beim Platinen-Design V2.1 wurde zusätzlich ein Spannungsteiler aufgelötet, der zusammen mit einer erweiterten Firmware dafür sorgt, dass bei Unterschreitung der Batteriespannung das Modul mit CCU Meldung sich selbst deaktiviert. In der Platinen-Version 4.x ist die Spannungsüberwachung direkt im Platinen-Layout integriert ([siehe Projekt Mitteilung](https://homematic-forum.de/forum/viewtopic.php?f=76&t=49719&hilit=HomeMatic+Gardena+Ventil&start=90#p584848)).

#### Realisierung
Die bisherige Firmware 'Gardena_Ventil' wurde komplett überarbeitet. Die softwareseitige Änderung bzw. Erweiterung besteht aus drei Dateien:

- HM_LC_SW1_BA_PCB_GAR1251.ino - geänderte Firmware
- HM_LC_SW1_BA_PCB_GAR1251.h - Zusammenfassung aller möglichen Konfigurationsparameter
- tmBattery.h - ([siehe Tom Major - 'Schutz vor 'Babbling Idiot'](https://github.com/TomMajor/SmartHome/tree/master/Info/Babbling%20Idiot%20Protection/))

Von der Struktur her ist die Firmware an das eigentliche Ursprungsscript 'HM-LC-SW1-BA-PCB' angelehnt worden und wurde daher auch entsprechend umbenannt: 'HM_LC_SW1_BA_PCB_GAR1251'. Alle Konfigurationsmöglichkeiten sind jetzt in eine Konfigurationsdatei ausgelagert - d.h.: möchte man die Konfiguration ändern, kann man dies in der Konfigurationsdatei machen, ohne das eigentlich INO Script anfassen zu müssen. Welche Einstellungen man ändern kann, ist dort ausführlich in den Kommentaren dokumentiert.

 Folgende CCU-Einstellungen funktionieren jetzt: minimaler Batterie-Schwellwert (man kann sich jetzt bei Falscheingabe der minimalen Batteriespannung nicht mehr selbst aussperren, da die Falscheingabe nicht vom Modul übernommen wird) und Geräte-LED. Weiter kann bei der 'AskSin++' Konfiguration die Art des Batterieüberprüfung, die CC1101 Frequenz und der Modus des Anlernbuttons festgelegt werden. 'Alle' Funktionen wurden ausprobiert und auf Funktion geprüft - vom Aufspielen bis zum Schalttest am Gardena-Ventil ...

 - _Nur für Experten_:<br>Wichtig in diesem Zusammenhang ist natürlich, dass auch die 'Fuse Bits'
 des AVRs richtig gesetzt sind: das 'High Fuse' Bit muss für 'AskSin++' unbedingt auf '0xD2' gesetzt werden, damit z.B. für das Abspeichern der Frequenzeinstellung des CC1101 Sendemodul ein EEPROM Speicherbereich zur Verfügung gestellt wird ([siehe CC1101 Frequent Test](https://asksinpp.de/Grundlagen/FAQ/Fehlerhafte_CC1101.html)).<br><br>
 'HM-LC-SW1-BA-PCB-GAR1251' Fuses:<br>
   | **Fuse** | **Wert** | **Bemerkung** |
   | --- | --- | --- |
   | Low Fuse | 0xE2 | !! _Nicht_ auf 'AskSin++'-Wert '0xFF' ändern !! |
   | High Fuse | 0xD2 | für CC1101 Frequenz im EEPROM Speicherbereich |
   | Extended Fuse | 0xFF | Brown-out detection disabled (BODLEVEL=111) |

   Hier ein sehr guter Erklärungs-Link dazu:
   [Engbedded Atmel AVR Fuse Calculator](http://www.engbedded.com/fusecalc?P=ATmega328P&V_LOW=0xE2&V_HIGH=0xD2&V_EXTENDED=0xFF&O_HEX=Apply+values)

#### INO-Script
  [Download ...](./bin/HM_LC_SW1_BA_PCB_GAR1251_20200529.zip)

#### 3D-Print
  - 3D-Druck Projekt für 'GARDENA EasyControl' mit 'HM-LC-SW1-BA-PCB-GAR1251' - [Zeigen ...](https://github.com/wolwin/WW-my3DP/blob/master/3DP_GARDENA_EasyControl/README.md)

#### Hardware
- Für das Platinen-Layout Version 2.1 kann eine Hardware-Modifikation vorgenommen werden, falls eine Batteriespannungsmessung über Spannungsteiler durchgeführt werden soll.
  - Schaltung Spannungsteiler
<br><br>
![WW-mySHP - HM-LC-SW1-BA-PCB-GAR1251](./img/SHP_HM-LC-SW1-BA-PCB-GAR1251_01.jpg "HM-LC-SW1-BA-PCB-GAR1251 - Spannungsteiler")
<br><br>
  - Beispiel - fliegender Aufbau:
<br><br>
![WW-mySHP - HM-LC-SW1-BA-PCB-GAR1251](./img/SHP_HM-LC-SW1-BA-PCB-GAR1251_02.jpg "HM-LC-SW1-BA-PCB-GAR1251 - Platine")
<br><br>
- Für das Platinen-Layout Version 4.x ist keine Hardware-Modifikation mehr notwendig, da der Spannungsteiler integriert wurde.
<br><br>
![WW-mySHP - HM-LC-SW1-BA-PCB-GAR1251](./img/SHP_HM-LC-SW1-BA-PCB-GAR1251_04.jpg "HM-LC-SW1-BA-PCB-GAR1251 - Platine")

#### Konfiguration und Inbetriebnahme
Das INO-Script hier herunterladen und in 'HM_LC_SW1_BA_PCB_GAR1251.h' die Konfigurationsparameter evtl. anpassen:

- für Platinen-Layout Version 4.x - mit integriertem Spannungsteiler:
    - '#define BAT_SENSOR_MODE 3' => 'Batteriespannungsmessung unter Last'
    - => voreingestellter Wert


- für Platinen-Layout Version 2.1 - ohne Spannungsteiler:
  - '#define BAT_SENSOR_MODE 1' => 'keine Batteriespannungsmessung'


- für Platinen-Layout Version 2.1 - mit nachgerüstetem Spannungsteiler:
  - '#define BAT_SENSOR_MODE 2' => 'Batteriespannungsmessung über Spannungsteiler'

Dann weiter, wie gewohnt das INO Script kompilieren und über den 6-poligen ISP Anschluß auf der Platine hochladen - [siehe AskSin++ - 'Software flashen' - 'FTDI Adapter'](https://asksinpp.de/Grundlagen/02_software.html#anschluss-des-ftdi-adapters).

!! ACHTUNG !! - vorher das CC1101 Sendemodul aus dem Sockel entfernen - [siehe Tom Major - 'Warnung vor dem Flashen von 3,3V Geräten mit USBasp Klones'](https://github.com/TomMajor/SmartHome/tree/master/Info/Warnung_Flashen_33_USBasp_Klones/).
<br><br>
Mit Anlernen an der Zentrale die Platine in Betrieb nehmen.
<br><br>
![WW-mySHP - HM-LC-SW1-BA-PCB-GAR1251](./img/SHP_HM-LC-SW1-BA-PCB-GAR1251_03.jpg "HM-LC-SW1-BA-PCB-GAR1251 - CCU")

#### Historie
- 2020-06-19 - Aktualisierung Platinen-Layout Angaben
- 2020-05-30 - Aktualisierung Platinen-Layout und INO-Script
- 2020-02-23 - Veröffentlichung an dieser Stelle
