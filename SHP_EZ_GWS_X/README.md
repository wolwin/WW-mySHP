# WW-mySHP - Ein Fazit zum Aufbau von Energiezählern für Gas, Wasser und Strom im Homematic Umfeld

[Zurück zur Übersicht ... ](../README.md)

### Projekt-Beschreibung
Ausgangspunkt war die 'Homematic Zählersensor-Sendeeinheit 'HM-ES-TX-WM', mit der Gas-, Wasser- und Stromzähler ausgelesen werden sollte. Jedoch war der 'HM-ES-TX-WM' über eine lange Zeit nicht lieferbar - auch der hohe Preis führte dazu, selbst aktiv zu werden und nicht auf eine 'Out of the box' Lösung zu setzen. So wurden für die drei Zählerarten jeweils zwei unterschiedliche Ansätze gewählt.

Im ersten Projekt wurde ein Asksin-Nachbau des 'HM-ES-TX-WM' mit unterschiedlichen Sensoren kombiniert. Diese Impulszähler lieferten direkt ihre Werte als 'Homematic-Gerät' in die CCU Zentrale:  

- [HM‑Energiezähler](../SHP_EZ_GWS/README.md "Zeigen ...") - Homematic Energiezähler für Gas, Wasser und Strom mit der 'Homematic Zählersensor-Sendeeinheit 'HM-ES-TX-WM'

Im zweiten Projekt wurden die Zählerwerte mit Hilfe einer ESP32 Kamera und der 'AI-on-the-edge-device' Software digitalisiert und per WLAN über das MQTT Protokoll an die CCU Zentrale vermittelt, wo das 'CCU-Jack' Addon für die Umsetzung der MQTT Topics in ein 'virtuelles Homematic-Gerät' vornahm.

- [AI‑Energiezähler](../SHP_EZ_GWS_AI/README.md "Zeigen ...") - 'AI-on-the-edge-device' Energiezähler für Gas, Wasser und Strom im Homematic Umfeld

Parallel zu den beiden Projekten wurde ein [Homematic Energiezähler-Skript mit 'universeller Konfiguration und Auswertung'](https://github.com/wolwin/WW-mySHT/blob/master/SHT_EZ-Script/README.md) entwickelt, damit die unterschiedlichen Projektansätze letztendlich doch in einer vergleichbaren Auswertung zusammenfinden.

### Allgemein
  - Mit dem 'HM‑Energiezähler' Projekt konnten relativ schnelle Umsetzerfolge erzielt werden. Auch die Einbindung in die Homematic Zentrale verlief problemlos. Zeitaufwändig sind jedoch die konstruktiven Anpassungen bzw. die Positionierung der Sensorik an den jeweiligen Zählertypen. Möchte man keinen 'fliegenden Aufbau' mit Klebeband o.ä., dann nimmt der Zeitaufwand mit Konstruktion und 3D-Druck natürlich zu. Bei allen drei Zählertypen konnten gut arbeitende Impulsgeber realisert werden, die zuverlässig mit der CCU zusammenarbeiten.

  - Bei dem 'AI‑Energiezähler' Projekt stand von Anfang an fest, dass der Zeitaufwand und die Komplexität deutlich höher sein würde - und dies hat sich dann auch bestätigt. Unabdingbar ist ein 3D-Drucker, um Gehäuse und angepaßte Befestigungen zu erstellen. Bei aller Hochachtung vor diesem Projekt, gibt es jedoch einige kritische Punkte, die eine zuverlässige Zahlenerkennung manchmal unmöglich machen.<br>
  Hier ist besonders die Spiegelung der internen bzw. externen LED-Beleuchtung zu nennen. Was bei der (runden) Wasseruhr durch Drehen der Ausleseeinheit minmiert werden kann, führt bei anderen Konstruktionen - besonders bei beengten Verhältnissen - zu manchmal 'unlösbaren' Problemen.<br>
  Bei der Wasseruhr funktioniert die Auslesung der analogen Zählerrädchen und die Auslesung der digitalen m3 Zahl problemlos (schwarze Ziffern auf weißem Hintergrund). Sobald jedoch Ziffernfolgen bei Gas- und Stromzähler ausgelesen werden sollen (weiße Ziffern auf schwarzem Hintergrund, manchmal spiegelnd), kommt es maßgeblich auf die Beleuchtung, die evtl. Spiegelung der Beleuchtung am (Plexi-) Glas und die Stellung der Ziffern an, die ja mit den hinterlegten Ziffern 'verglichen' werden.<br>
  So kann es auch vorkommen, dass die Ablesung lange ohne Fehler läuft, um dann plötzlich eine Ziffer (die sich nicht geändert hat) mit einem anderen Wert zu erkennen. Dies ist mehrfach vorgekommen, sodass ein spezielles Auswerteskript auf der Homematic die ankommenden MQTT Werte mit dem letzten übermittelten Wert vergleicht und dann evtl. (in Abhängigkeit von der verstrichenen Zeit) korrigiert.<br>
  Die Übernahme der vom 'AI-on-the-edge-device' gesendeten MQTT Werte durch das 'CCU-Jack' Addon und die Umsetzung über ein 'virtuelles Analogwertgerät' in die Homematic-Welt verlief zuverlässig und ohne jeglich Probleme.

### Detail-Vergleich

- <b>Gaszähler 'Pipersberg G4-RF1'</b>

  Nach einigen Versuchen konnte im 'HM‑Energiezähler' Projekt eine stabile Impulsauslesung mit einem magnetischen Hallsensor hergestellt werden. Die Funkverbindung vom Keller zur CCU Zentrale läuft mit 75 dB ohne Probleme. Der Asksin-Nachbau des 'HM-ES-TX-WM' wird über ein 5 Volt Steckernetzteil betrieben - bei einem Stromausfall überbrücken drei AA-Batterien den Ausfallzeitraum.

  Auf Grund beengter Verhältnisse mußte im 'AI‑Energiezähler' Projekt eine spezielle Tubus-Konstruktion mit einem 45 Grad geneigten Spiegel für die ESP32 Kamera gebaut werden. Wie schon geschrieben, wurde lange experimentiert, um eine konstant fehlerfreie Ablesung zu erhalten. Mit 76 dB WLAN Verbindung war der ESP32 erreichbar, aber nur mit einem Durchsatz von 10 Mbit/s - manchmal war die GUI Oberfläche nicht aufrufbar, obwohl die MQTT Sendungen ohne Problem versandt wurden.

  Da es jedoch beim 'AI-on-the-edge-device' immer wieder zu den besagten Fehlablesungen kam, wurde das Gerät zurückgebaut und wieder das 'HM-ES-TX-WM' Gerät mit dem Hallgeber-Sensor eingesetzt, bei dem der aktuelle Zählerstand jederzeit ablesbar bleibt.

- <b>Wasserzähler 'elster de-08-mi001-ptb 019'</b>

  Hier ist der Bauaufwand beim 'HM‑Energiezähler' Projekt mit einer LED-Lichtschranke höher als im 'AI‑Energiezähler' Projekt. Die Justierung des LED-Fokus auf das letzte Zählerrädchen wird konstruktiv unterstützt und ist innerhalb kurzer Zeit gemacht. Auch hier war die Funkverbindung vom Keller zur CCU Zentrale mit 75 dB ohne Probleme.D er Asksin-Nachbau des 'HM-ES-TX-WM' wird über ein 5 Volt Steckernetzteil betrieben - bei einem Stromausfall überbrücken drei AA-Batterien den Ausfallzeitraum.

  Beim 'AI‑Energiezähler' Projekt für den Wasserzähler merkt man, dass dies der Ausgangspunkt der Entwicklungsarbeit des 'AI-on-the-edge-device' war: alle analogen Zähler und auch die digitalen Ziffern werden korrekt ausgelesen und übermittelt. Mit 75 dB WLAN Verbindung ist der ESP32 erreichbar - aber auch hier ist die GUI Oberfläche wegen des geringen WLAN Durchsatzes von > 10 Mbit/s manchmal nicht aufrufbar, obwohl die MQTT Sendungen ohne Problem versandt wurden.

  Beide Lösungen sind für den Wasserzähler m.E. gleichwertig. Entscheidungskriterium kann vielleicht sein, dass der 'AI-on-the-edge-device' Aufbau auf Grund der Größe anfälliger für Berührung und Dejustage ist (hier: Trockenraum mit Wäsche). Trozdem bleibt der 'AI‑Energiezähler' erst einmal im Dauerbetrieb - der Zählerstand kann nur über GUI-Oberfläche visualisiert werden - eine Demontage des 'AI‑Energiezählers' würde eine Neujustage nötig machen.

- <b>Ferraris Tarifstromzähler 'Siemens Drehstromzähler'</b>

  Das 'HM‑Energiezähler' Projekt benutzt auch hier die schon bekannte LED-Lichtschranke, die zentriert über der Ferraris-Drehscheibe sitzt. Die beengten Verhältnisse in dem alten Schaltschrank zwingen zu einer aufwendigen Halterung - jedoch funktioniert der 'HM-ES-TX-WM' mit 77 dB Verbindung zur CCU Zentrale auch aus dem Schrank heraus. Da es sich um einen Tarifstromzähler handelt, wird die HT- und NT-Umschaltung nicht abgetastet, sondern die übermittelten Impulswerte werden per Skript und dort vorgegebenen Schaltzeiten zugewiesen.

  Das 'AI‑Energiezähler' Projekt benutzt hier die aufwändigste Konstruktion aller Varianten. Mit zwei extern angeordneten LED-Beleuchtungen werden sowohl HT- als auch NT-Zählwerk durch die ESP32 Kamera aufgenommen und ausgewertet. Es können so per MQTT die 'richtigen' beiden Zählerstände übermittelt werden. Trotz des technisch hohen Aufwands ist es nicht möglich, konsistente Ablesewerte zu übermitteln - siehe wie vor. Außerdem mußte in die Nähe des Zählerschranks ein WLAN-Repeater gesetzt werden, da das WLAN-Signal aus dem Metallschrank einfach zu gering war.

  Wegen der beim 'AI-on-the-edge-device' häufigen Fehlablesungen, aber letztlich jedoch auf Grund der deutlich niedrigeren Ableseauflösung ('AI‑Energiezähler': 0,1 kWh in 3 min zu 'HM‑Energiezähler': 1/75 kWh in 3 min) wurde das Gerät zurückgebaut und wieder das 'HM-ES-TX-WM' Gerät mit dem LED-Sensor eingesetzt, bei dem dann auch die beiden aktuellen Zählerstände jederzeit ablesbar bleiben.

### Fazit

  Sehr hoher Zeitaufwand - gut ... es ist ein Hobby ... !! Viel gelernt ... und eine triviale 'Weisheit' bestätigt: _'Wer einmal mißt, der mißt falsch ...'_

  Im Vergleich zu fertigen 'Kauflösungen' sind die 'Bastellösungen' vom Material her deutlich billiger - ca. 10-20% einer solchen Zusammenstellung von Sensor und Homematic Sendeeinheit. Dafür sind die 'Kauflösungen' (in der Regel, wenn verfügbar) direkt einsatzfähig. Aber auch hier bleibt oft die Anpassung an die jeweiligen Zählerarten zu berücksichtigen.

  Im Nachhinein ist nicht immer die auf dem Papier technisch beste Lösung auch die Lösung, die in der Praxis zuverlässig arbeitet. Für die Auswertung der drei Zählertypen sind die 'HM‑Energiezähler' Lösungen durchaus ausreichend. Sie funktionieren konstant und ohne weiteres Zutun. Die technisch anspruchsvollere 'AI‑Energiezähler' Lösung benötigt Aufmerksamkeit und Geduld. Wichtig ist in jedem Fall die Auswertung der Zählerablesungen - hier kann ein gutes Skript, das für zusammenfassende Übersichten sorgt, schon manche Erkenntnisse beim Nutzer bringen.

  Letztlich muß also jeder für sich entscheiden, wo er welche Präferenzen setzt.

### Historie
- 2023-04-16 - Erstveröffentlichung
