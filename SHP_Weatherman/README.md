# WW-mySHP - STALL-Weatherman

[Zurück zur Übersicht ...](../README.md)

### Projekt-Beschreibung
Beim 'STALL-Weatherman' handelt es sich um eine Selbstbau Wetterstation, die sich über eine WLAN Verbindung in die eigene Heimautomation einbinden läßt.

['STALL-Weatherman' Original-Projekt zeigen ...](https://www.stall.biz/project/weatherman-die-perfekte-wetterstation-fuer-die-hausautomation)

Support Unterstützung für den 'STALL-Weatherman' kann man im 'HomeMatic FHZ-Forum' finden:

[Thread im 'HomeMatic FHZ-Forum' zeigen ...](https://homematic-forum.de/forum/viewtopic.php?t=38485)

### Hardware
Dr. Eugen Stall vertreibt über seinen Web-Shop einen Bausatz für den 'STALL-Weatherman'. Zusätzlich sind noch weitere Komponenten zu beschaffen, die auf der Projekt-Seite des Weatherman und in der Bauanleitung aufgeführt sind.

[Bausatz mit allen Teilen im Webshop 'www.stall.biz' ... und dort befindet sich auch der Link zur aktuellen Bauanleitung ...](https://www.stall.biz/produkt/weatherman-controller)

### Konfiguration und Inbetriebnahme
Bei dem Aufbau des 'STALL-Weatherman' sollte man sich grundsätzlich eng an die in der Bauanleitung vorgegebenen Empfehlungen halten. Bei Schwierigkeiten kann man versuchen, über das FHZ-Forum Hilfe zu bekommen.

Die Inbetriebnahme des 'STALL-Weatherman' ist auf der Weatherman Projektseite beschrieben.

### Erfahrungen und Bewertungen
Bei mir ist der 'STALL-Weatherman' seit über zwei Jahren in Betrieb. Der Erstaufbau erfolgte 'peinlich genau' entsprechend der Bauanleitung - außerdem wurden (Material-) Tipps aus dem FHZ-Forum (u.a. von Dr. Stall) direkt berücksichtigt. Von Beginn an habe ich den Aufbau und Betrieb bzw. die später vorgenommenen Hardware-Änderungen für mich dokumentiert. Zu Beginn war ich von der 'Einfachheit / Klarheit' des Konzeptes - das man relativ preiswert umsetzen konnte - begeistert. Auch die bereitgestellte Firmware tat, was sie sollte - schnell und unauffällig standen die 'Wetterdaten' über WLAN zur Verfügung. Kleine Fehler oder JSON-Protokoll Erweiterungen - die man im FHZ-Forum melden konnte - wurden vom Autor verifiziert und beseitigt.
<br><br>
Alles gut also? Leider nicht ganz ...
<br>
- <b>Punkt 1</b> - Schwachpunkt ABS-Gehäuse:<br>
Für die Hardware kann ich nach zwei Jahren sagen, dass das 'integrative' Konzept der Sensoren in dem RND ABS-Gehäuse ohne weitere Maßnahmen zur Verhinderung von Feuchtigkeitsbildung im Gehäuse nicht funktioniert. Kabel ohne Kabeldurchführungen, hohe Temperaturunterschiede im Glas für den Sonnensensor und die Heizung der Regensensorplatine sehe ich persönlich als primäre Quellen der Feuchtigkeitsbildung. Ein zeitgleich aufgesetzter Feinstaub-Sensor in einem 'OBO-Betterman' T60 Gehäuse, das mit PTFE-Gehäuseschrauben und Kabeldurchführungen versehen wurde, weist nach zwei Jahren keine Feuchtigkeitsspuren auf! Weiter sind die Verklebungen der Weatherman Befestigungsschrauben zum RND Gehäuse alle abgelöst, obwohl der empfohlene 2-Komponentenkleber benutzt wurde. Die Verklebungen der Regensensorplatine und des Glases hatte ich sicherheitshalber schon nach einem Betriebsjahr mit UV-beständigem Silikon gesichert ...

- <b>Punkt 2</b> - Firmware:<br>
Aus meiner Sicht war das Konzept von Hardware und Software bis zur Firmware 67 stimmig, in der noch KEIN Datenlogger integriert war. Mit dem Einzug des Datenloggens, der Speicherung und Auswertung wurden Features eingebracht, die für ein solches System nicht geeignet sind. Es wurde damit kein Mehrwert geschaffen - stattdessen zieht es sich wie ein roter Faden durch viele Kommentare im Weatherman-Thread des FHZ-Forums: Schwierigkeiten den Weatherman anzusprechen ... reagiert zeitweise nicht ... Verzögerungen ... Systemabstürze, Schwierigkeiten bei der WEB-Abfrage, usw. Ich selber benutze seit 04-2019 die Firmware 107, da leider in der Firmware 67 (ohne Datenlogger) im JSON-Protokoll ein Parameter für meine NodeRed Umsetzung fehlt. Meine Rezensionen bzw. Kritik zu diesem Thema (... und ich war nicht der einzige, der diese Meinung vertrat ...) wurden von Dr. Stall dankend entgegengenommen - aber das war es dann auch. Inzwischen läuft die Feature-Manie weiter - derzeitiger Stand: 02.06.2020 - Firmware 147 ... für Leute, die experimentieren möchten eine reine Freude! Anwender, die verläßliche eigene Wetterdaten geliefert bekommen möchten, indiskutabel!

- <b>Punkt 3</b> - Dokumentation:<br>
Mit der größte Schwachpunkt ist jedoch, dass es keine Dokumentation darüber gibt, WAS geändert wurde oder WIE sich bestimmte Parameter-Einstellungen verhalten. Teilweise wurden Parameter-Einstellungen 'unter laufendem Rad' von der einen zur anderen Firmware-Version 'optimiert' - erfahren hat man das manchmal nur über Nachfragen der User im FHZ-Forum - quasi 'reverse engineering by observation' für jede neue Firmware. Auch: eine Liste der unterstützten Sensoren fehlt ... ab welcher Firmware ... welcher Sensor???

- <b>Punkt 4</b> - Kommunikation:<br>
Vielleicht kann man noch über einige Dinge der Punkte 2 und 3 hinwegsehen und einfach an den Stellen optimieren, die man selber beeinflußen kann - es ist schließlich eine HOBBY-Anwendung. Jedoch hat mich folgende Aussage von Dr. Stall doch zweifeln lassen:

  - [Zitat - Link dazu ...](https://homematic-forum.de/forum/viewtopic.php?f=31&t=38485&hilit=jp112sdl&start=2940#p579895) : <br>
  <i>'Unsozial wie ich bin mache ich nur das was ich möchte und was mir Spaß macht und nicht, was andere von mir wollen!! :mrgreen: :mrgreen: :mrgreen:<br>
  ... und wenn andere Bastler die Module auch genauso wie ich haben wollen, dann können sie diese Teile gerne nachbauen.<br>
  Die aber was anderes haben wollen, sollen eben was anderes nachbauen oder, besser noch, selbst entwickeln.<br>
  Ist doch ganz einfach!</i><br><br>

- <b>Zusammenfassung:</b><br>
Das Projekt läuft unter dem Titel 'WEATHERMAN … die perfekte Wetterstation für die Hausautomation'. Das sehe ich SO nicht - ich denke, die Kritikpunkte sprechen für sich. Vor zwei Jahren war der Weg zu verläßlichen eigenen Wetterinformationen für die Heimautomation aus meiner Sicht fast vollständig erreicht - die Optimierung von wenigen Dingen hätten einen sehr guten Stand gebracht. Leider hat der Entwickler Dr. Stall einen anderen Weg eingeschlagen.

### Änderungen und Realisierung
Um meinem Weatherman neues Leben einzuhauchen, habe ich mir die Punkte 'Gehäuse und Feuchtigkeit' vorgenommen. Über Stage 1, Stage 2 und Stage 3 habe ich drei unterschiedliche Lösungsansätze für den 'STALL-Weatherman' konstruiert: in allen drei Versionen wird das Weatherman Gehäuse und die Gehäuse für den Lichtsensor und die Regensensorplatine separiert und voneinander unabhängig betrieben, sowie mit Hilfe von PTFE-Ventilationsschrauben belüftet.

Die maximal integrierte Version des 'STALL-Weatherman' (Stage 3) ist das OBO T60 Gehäuse mit Wetterkappe aus der ['YAWS-Toolbox' mit der 'STALL-Weatherman' Option](https://github.com/wolwin/WW-mySHP/blob/master/SHP_YAWS/README.md).

Da die Nachfrage für eine OpenSource Version des Weatherman-Codes von Dr. Stall abgelehnt wird, kann leider eine Integration eines GEREGELTEN Lüfters in der 'YAWS-Wetterkappe' nicht (direkt) realisiert werden.

- <b>Stage 0</b> - Grundplatten zur mechanischen Befestigung des 'STALL-Weatherman' in den RND-Gehäusen 'RND 455-00223' und 'RND 455-00144' bzw. den OBO-Gehäusen 'OBO-T40' und 'OBO-T60'.
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Baseplate_01.jpg "Weatherman Grundplatte")
<br><br>
- <b>Stage 1</b> - 'STALL-Weatherman' im RND-Gehäuse (RND 455-00223 oder RND 455-00144) mit abgesetztem AddOn Gehäuse für Lichtsensor BH1750 / NTC und Regensensor
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_RND_01.jpg "AddOn RND-Gehäuse 455-00223")
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_RND_02.jpg "AddOn RND-Gehäuse 455-00223")
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_RND_03.jpg "AddOn RND-Gehäuse 455-00144")
<br><br>
  - Detailansichten des RND AddOn Gehäuses für Lichtsensor BH1750 / NTC und Regensensor
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_RND-Case_01.jpg "AddOn für RND-Gehäuse")
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_RND-Case_02.jpg "AddOn für RND-Gehäuse")
<br><br>
- <b>Stage 2</b> - 'STALL-Weatherman' im OBO T40 oder OBO T60 Gehäuse mit separaten Gehäusen für Lichtsensor BH1750 / NTC, Regensensor und Wetterkappe aus der 'YAWS-Toolbox'
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_OBO-Case_01.jpg "OBO T40-Gehäuse")
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_OBO-Case_02.jpg "Module für OBO T40 und T60 Gehäuse")
<br><br>
  - Detailansichten der Gehäuse für Lichtsensor BH1750 / NTC und Regensensor
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Case-Sun_01.jpg "Sensor Gehäuse für BH1750 und NTC")
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Case-Rain_01.jpg "Regensensor Gehäuse")
<br><br>
- <b>Stage 3</b> - 'STALL-Weatherman' im OBO T60 Gehäuse und Wetterkappe aus der 'YAWS-Toolbox' mit der 'STALL-Weatherman' Option
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_OBO-Case_03.jpg "OBO T60-Gehäuse mit YAWS 'STALL-Weatherman' Option")
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_OBO-Case_05.jpg "OBO T60-Gehäuse mit YAWS 'STALL-Weatherman' Option")
<br><br>
- Kombinationsmöglichkeiten für den 'STALL-Weatherman' in Verbindung mit der 'YAWS-Toolbox'
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_OBO_Combi_01.jpg "Weatherman - OBO T60-Gehäuse - Kombinationen")
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_OBO_Combi_02.jpg "Weatherman - OBO T60-Gehäuse  - Kombinationen")

### 3D-Print
- 3D-Druck Projekt für Gehäuse-Erweiterungen der Wetterstation 'STALL-Weatherman' - [Zeigen ...](https://github.com/wolwin/WW-my3DP/blob/master/3DP_Weatherman/README.md)
- 3D-Druck Projekt der 'YAWS-Toolbox' - [Zeigen ...](https://github.com/wolwin/WW-my3DP/blob/master/3DP_YAWS/README.md)

### Langzeit-Erfahrungen (Hardware)
- Nach zweijährigem Betrieb wurde der Weatherman zur Revision abgebaut. Das RND-Gehäuse ist deutlich von den Umwelteinflüssen gezeichnet.
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Rev_01.jpg "Weatherman - Revision")
<br><br>
- Die zusätzlich aufgebrachten Silikon Abdichtungen sind nach anderthalb Jahren in sehr gutem Zustand. Die Regensensorplatine ist trotz seiner Goldkontakte angegriffen, aber voll funktionsfähig. Das Glas ist ebenfalls unversehrt und wie im Neuzustand.
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Rev_02.jpg "Weatherman - Revision")
<br><br>
- Nach dem Öffnen des Gehäuses sind die schon oben benannten Schwachpunkte sofort ersichtlich: die Verklebungen mit dem ABS-Gehäuse sind teilweise nicht von Dauer - Sonneneinstrahlung und Temperaturunterschiede tun dabei ihr übriges ... die verklebten Schrauben zur Befestigung der Weatherman Platine sind alle abgelöst.
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Rev_03.jpg "Weatherman - Revision")
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Rev_04.jpg "Weatherman - Revision")
<br><br>
- Die Problematik wird deutlich bei der Verklebung der Regensensorplatine - Wasserflecken auf Gehäuse und BH1750 Sensor sind vorhanden. Dieser Schaden trat schon nach einem 1/2 Jahr im Betrieb auf. Daraufhin wurde mit UV-beständigem Silikon (LUGATO Wetterschutz-Slicon (transparent) WIE GUMMI 310 ml - EAN 4009071098233) die Platine und das Lichtsensorglas (erfolgreich) abgedichtet. Der zusätzliche Einsatz von Kabeldurchführungen im RND-Gehäuse verhinderte Schlimmeres im Langzeitbetrieb.
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Rev_05.jpg "Weatherman - Revision")
<br><br>
- Zeitgleich wurde mit dem Weatherman auch ein Feinstaubsensor im 'OBO-T60' Gehäuse mit Kabeldurchführungen und Belüftung aufgestzt und in Betrieb genommen. Nach zwei Betriebsjahren ist diese Einheit in einem DEUTLICH besseren Zustand als der Weatherman im RND-Gehäuse.
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Rev_06.jpg "Weatherman - Revision")
<br><br>
- Beim Feinstaubgehäuse wurden zwei Belüftungen über Kabeldurchführungen mit PTFE-Druckausgleichsmembranen (B+B Sensors -  Druckausgleich-Membran Ø10,2/5,5 VPE, Art.Nr.: SHOP DAM-AD10) eingebaut. Jedoch lösten sich beide Membranen von ihren Verklebungen - wahrscheinlich durch die gelbe Farbe angelockt - erledigten Insekten dann den Rest ...
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Rev_07.jpg "Weatherman - Revision")
<br><br>
- Über das Thema BME280 wurde schon an anderer Stelle viel geschrieben ... insgesamt versagten VIER BME280 im Weatherman ihren Dienst. Alle Maßnahmen einer 'Kapselung' versagten: weder Plastik-Versiegelung, aktive Belüftung mit Lüfter, noch zusätzliche PTFE-Membran über dem Sensor (Auflösungserscheinung der Membran u.a. durch Insekten) halfen langfristig ...
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Rev_08.jpg "Weatherman - Revision")
<br><br>
- Außerdem diente ein BME280 den Spinnen als Basis zum Überwintern ihrer Brut ...
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Rev_09.jpg "Weatherman - Revision")
<br><br>
- Der VENTUS W132 tat bis heute zuverläßig seinen Dienst. Wichtig beim Zusammenbau ist der Einbau der Dioden D4 und D5 im W132, damit dieser zusätzlich mit Batterien betrieben werden Kann. Hintergrund: der W132 speichert beim Einschalten der Versorgungsspannung die aktuelle Windfahnenposition als Nordrichtung ab. Bei Netzunterbrechung 'vergisst' die Windfahne die Nordrichtung und muss dann manuell wieder neu eingestellt werden (siehe Bauanleitung). Als Batterien habe ich zwei 'Energizer Batterien AA, Ultimate Lithium' (ASIN: B000IWW1G6) eingesetzt.
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Rev_10.jpg "Weatherman - Revision")
<br><br>
- Ärgerlich beim VENTUS W132 ist die billig lackierte Rohrschelle, die zu äußerst unschönen Roststellen führt - links im Bild ist eine Rohrschellenhalterung zu sehen (gleich alt), wie es sein sollte ... also: man sollte beim Neuaufbau den VENTUS W132 mit besserem Material befestigen.
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Rev_11.jpg "Weatherman - Revision")
<br><br>
- Der Regenmesser WS-280 arbeitete unauffällig und gut. Direkt zu Anfang wurde er mit einem 'Vogel- und Blätterabwehrgitter' versehen (nicht schön, aber wirksam). Bei Sturzregen konnte beobachtet werden, dass eine große Regenmenge das Gerät überforderte: die Auffanghöhe ist schlicht zu niedrig - das Regenwasser schwappte über den zu niedrigen Rand. Auf Thingiverse gibt es eine Randerhöhung für den WS-280 (Einbau siehe Bild), der diese Problem deutlich mildert:<br>
'Rain Gauge Funnel  Extension for WS-280' https://www.thingiverse.com/thing:2551621
<br><br>
![WW-mySHP - Weatherman](./img/SHP_WM_Rev_12.jpg "Weatherman - Revision")

### Fazit - Langzeit-Erfahrungen (Hardware)
- Die Langzeit-Erfahrungen mündeten letztlich in zwei großen eigenen Projekten:
  <br><br>
  - WW-mySHP - STALL-Weatherman (dieses Projekt)
  - [WW-mySHP - YAWS - 'Yet Another Weather Shield' - Toolbox - Version 3](https://github.com/wolwin/WW-mySHP/blob/master/SHP_YAWS/README.md)
<br><br>
- mit den zugehörigen 3D-Print Projekten:
  <br><br>
  - [WW-my3DP - Gehäuse-Erweiterungen der Wetterstation 'STALL-Weatherman'](https://github.com/wolwin/WW-my3DP/blob/master/3DP_Weatherman/README.md)
  - [WW-my3DP - YAWS - Yet Another Weather Shield - Toolbox - Version 3](https://github.com/wolwin/WW-my3DP/blob/master/3DP_YAWS/README.md)
<br><br>
- Maximal integrierte Version des 'STALL-Weatherman' (Stage 3) mit 'OBO-T60' Gehäuse und Wetterkappe aus der ['YAWS-Toolbox' mit der 'STALL-Weatherman' Option](https://github.com/wolwin/WW-mySHP/blob/master/SHP_YAWS/README.md).
  <br><br>
  - Mittels PTFE-Membran belüftetes 'OBO-T60' Gehäuse mit Kabelverschraubungen für den Weatherman
  - Getrennte Gehäuse für Regen- und Lichtsensor / NTC - Belüftung der Gehäuse über PTFE-Membran
  - Aufwändig konstruierte Wetterkappe für den BME280
<br><br>
- Weatherman - Stand 06-2020
  <br><br>
  ![WW-mySHP - Weatherman](./img/SHP_WM_New_W.jpg "Weatherman")
  <br><br>
- Feinstaubsensor - Stand 06-2020
  <br><br>
  ![WW-mySHP - Weatherman](./img/SHP_WM_New_F.jpg "Feinstaubsensor")

### Historie
- 2020-07-02 - Dokumentation Langzeit-Erfahrungen (Hardware)
- 2020-06-16 - Stage 0 - Grundplatten
- 2020-06-07 - Erstveröffentlichung
