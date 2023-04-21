# WW-mySHP - HB-UNI-Sen-TEMP-DS18B20

[Zurück zur Übersicht ...](../README.md)

### Projekt-Beschreibung
 Grundlage ist das 'Asksin++' Projekt 'HB-UNI-Sen-TEMP-DS18B20 - 8fach Universal-Temperatursensor für die Integration in HomeMatic' von Jérôme Pech:

[Original-Projekt zeigen ...](https://github.com/jp112sdl/HB-UNI-Sen-TEMP-DS18B20)

Beim Aufbau und dem Testen sind folgende Dinge aufgefallen:
- es kann bei der richtigen HM-Kanal Zuordnung  Identifikationsprobleme geben
- bei Sensorausfall wird immer der letzte Temperaturwert oder 0 gesendet
- die Offset-Werte werden IMMER aufaddiert - auch im Fehlerfall

### Änderungen
Im Wesentlichen geht es neben der Fehlerbereinigung um die Identifikation bzw. die (korrekte) Zuordnung der einzelnen DS18B20 Sensoren zu den 8 HM-Kanälen - dabei besteht jetzt per Compilerflag die Möglichkeit eine Reihenfolge der Sensoren IDs fest vorzugeben (oder wie gehabt, die Sensoren ohne Reihung vom 1-Wire Bus zu identifizieren).

Im Fehlerfall wird nun immer ''-999' als Fehlerwert zurückgegeben - Fehlerfall bedeutet z.B.: Sensor nicht vorhanden oder defekt.

Für eine einfache Konfiguration wurde zusätzlich noch eine '<HB-UNI-Sen-TEMP-DS18B20_ext.h>' angelegt, in der alle wesentlichen Konfigurationsparameter zusammengefasst sind - es braucht nun nicht mehr das Original INO File geändert werden.

### Realisierung
Die softwareseitige Änderung bzw. Erweiterung besteht aus drei Dateien:

- HB_UNI_Sen_TEMP_DS18B20_ext.h

  Zusammenfassung aller möglichen Konfigurationsparameter ausserhalb des INO-Files

- HB_UNI_Sen_TEMP_DS18B20_ext.ino

  Abgeänderte INO-Datei: es ist jetzt möglich, bestimmte Sensoren auf bestimmte Ports zu legen - dazu wird die ID des jeweiligen Sensor benutzt (#define cSENS_ID_ORDER in 'HB_UNI_Sen_TEMP_DS18B20_ext.h'). Beispiel: man kann das Modul mit 4 Ports konfigurieren (#define cANZ_SENSORS 4 in 'HB_UNI_Sen_TEMP_DS18B20_ext.h'), bei dem man aber nur für die Ports 3 und 4 die IDs einträgt, weil man erst später die Ports 1 und 2 mit Sensoren bestücken möchte. Angezeigt werden dann die Ports 1 ... 4, wobei die Ports 1 und 2 den Fehlerwert '-999' liefern (Sensorfehler). Wird das #define cSENS_ID_ORDER in 'HB_UNI_Sen_TEMP_DS18B20_ext.h' auskommentiert, verhält sich das Modul wie vorher: es werden alle IDs der angeschlossenen Sensoren in der Busreihenfolge ermittelt und dann auch in dieser Reihenfolge ausgegeben. Der Quelltextverlauf wurde insgesamt beibehalten und nur um die drei ID-Arrays erweitert.

- Ds18b20.h

  Erweiterung: 'init', 'measure' und 'read' Funktionen mit optionalen Aufrufparameter für String-Rückgabe der Sensor-IDs. Wird momentan lokal eingebunden - wäre möglich ohne Änderung in die Asksin-Lib zu übernehmen, dann globale Einbindung (-> Entfall hier ...).

### INO-Skript und Dateien
  [Download ...](./bin/HB_UNI_Sen_TEMP_DS18B20_ext_20200609.zip)

### Historie
- 2020-06-09 - INO-Skript - Fixing ID compare
- 2020-05-29 - INO-Skript - Fixing compiler warnings
- 2020-02-03 - Veröffentlichung an dieser Stelle
- 2019-11-19 - Änderungen
