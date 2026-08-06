# WW-mySHP - HB-LxR-THT – 'AskSin++' Platinen mit bistabilen Relais (THT)

[Zurück zum Projekt 'HB-LxR-THT' ...](README.md)

## Firmware

Die Firmware besteht aus zwei Dateien:

```
HB-LxR-THT/
├── HB-LxR-THT.ino
└── HB-LxR-THT_ext.h
```

### `HB-LxR-THT.ino`

Enthält die komplette Firmwarelogik:

- AskSin++-Initialisierung
- Relaissteuerung
- EEPROM-Verwaltung
- Boot-Synchronisation
- Tasterlogik
- Funkkommunikation

### `HB-LxR-THT_ext.h`

Enthält ausschließlich die gerätespezifische Konfiguration.

Das Hauptprogramm bindet die Konfiguration über

```cpp
#include "HB-LxR-THT_ext.h"
```

ein.

Dadurch bleibt die Firmware selbst unverändert und alle Anpassungen erfolgen zentral in der Konfigurationsdatei.

---

## Konfiguration (`HB-LxR-THT_ext.h`)

Vor dem Kompilieren wird das gewünschte Gerät in `HB-LxR-THT_ext.h` eingestellt.

### Kanalanzahl

```cpp
#define CHANNEL_ANZ 2
```

- `1` → HB-L1R-THT (HM-LC-Sw1-Pl)
- `2` → HB-L2R-THT (HM-LC-Sw2-FM)

---

### Boot-Synchronisation

```cpp
#define cRELAY_BOOT_SYNC 1
```

Verfügbare Modi:

| Modus | Verhalten |
|------:|-----------|
| `0` | minimale Relaisbetätigung |
| `1` | Relais beim Booten immer auf EEPROM-Zustand synchronisieren (empfohlen) |
| `2` | Verhalten nahe am originalen HM-LC-Sw2-FM |

---

### Relaisimpuls

```cpp
#define RELAY_PULSE_MS 50
```

Impulsdauer für SET- und RESET-Ansteuerung.

---

### Pinbelegung

In `HB-LxR-THT_ext.h` werden alle verwendeten Pins definiert, unter anderem:

- CC1101
- Relais
- lokale Taster
- Geräte-LED
- Konfigurationstaster

---

### Geräteparameter

Die Datei enthält außerdem:

- Geräte-ID
- Seriennummer
- Firmware-Version
- HomeMatic-Gerätemodell
- LED-Modus
- Modus des Konfigurationstasters

Dadurch können unterschiedliche Gerätevarianten erstellt werden, ohne Änderungen am eigentlichen Firmwarecode vorzunehmen.

---

## Boot-Synchronisation

Die Firmware unterstützt drei unterschiedliche Strategien zur Synchronisation des bistabilen Relais nach einem Neustart.

### Modus 0 – minimale Relaisbetätigung

Der EEPROM-Inhalt wird als gültiger Relaiszustand übernommen.

| CCU-Einstellung | EEPROM | Relais nach Boot |
|----------------|--------|------------------|
| keine | AUS | AUS |
| keine | AN | AN |
| kurzer Tastendruck | AUS | AN |
| kurzer Tastendruck | AN | AN |

Es wird nur geschaltet, wenn bei **„kurzen Tastendruck simulieren“** ein Einschaltimpuls erforderlich ist.

---

### Modus 1 – maximale Synchronisationssicherheit (Standard)

Das Relais wird beim Booten immer auf den Zielzustand synchronisiert.

| CCU-Einstellung | EEPROM | Relais nach Boot |
|----------------|--------|------------------|
| keine | AUS | RESET |
| keine | AN | SET |
| kurzer Tastendruck | AUS | SET |
| kurzer Tastendruck | AN | SET |

Vorteile:

- EEPROM
- mechanischer Relaiszustand
- interner AskSin-Zustand
- CCU-Anzeige

bleiben nach jedem Neustart garantiert synchron.

Dieser Modus wird für **bistabile Relais ohne Rückmeldekontakt empfohlen**.

---

### Modus 2 – Verhalten nahe am Original HM-LC-Sw2-FM

Nur bei **„kurzen Tastendruck simulieren“** wird immer ein SET-Impuls erzeugt.

Bei **„keine“** wird das Relais nicht betätigt.

---

## Lokale Taster

Jeder Kanal besitzt einen eigenen lokalen Taster.

Merkmale:

- Flankenerkennung
- Entprellung über AskSin-Alarm
- Toggle-Funktion
- vollständig unabhängig vom Anlerntaster

Die Taster wirken direkt auf den jeweiligen Kanal und aktualisieren:

- Relais
- EEPROM
- HomeMatic-Status

---

## EEPROM

Für jeden Kanal wird der Schaltzustand gespeichert.

Gespeichert wird nur bei tatsächlicher Zustandsänderung.

Dadurch werden unnötige EEPROM-Schreibvorgänge vermieden.

---

## Anlernen

Der Anlernmodus erfolgt über

```cpp
CONFIG_BUTTON_PIN
```

Je nach Konfiguration unterstützt die Firmware:

- kurzen Tastendruck
- langen Tastendruck

---

## HomeMatic-Kompatibilität

### 1 Kanal

Gerät:

```
HM-LC-Sw1-Pl
```

### 2 Kanäle

Gerät:

```
HM-LC-Sw2-FM
```

Unterstützt werden unter anderem:

- Schalten
- Statusrückmeldung
- interne Peerings
- Aktion bei Spannungszufuhr
- Parametrierung über die CCU

---

## Kompilieren

Benötigte Bibliotheken:

- AskSin++
- EnableInterrupt
- LowPower

Die Konfiguration erfolgt ausschließlich über

```
HB-LxR-THT_ext.h
```

Danach kann `HB-LxR-THT.ino` direkt kompiliert und auf den ATmega328P übertragen werden.

---

## Empfohlene Einstellungen

Für die meisten Anwendungen:

```cpp
#define CHANNEL_ANZ 2
#define cRELAY_BOOT_SYNC 1
#define RELAY_PULSE_MS 50
```

---

## Vorteile der ausgelagerten Konfiguration

Die Trennung von Firmware und Konfiguration bietet mehrere Vorteile:

- **einfachere Anpassung** an verschiedene Hardwarevarianten,
- **übersichtlicheres Hauptprogramm**,
- **geringere Fehlergefahr** bei Firmware-Updates,
- **einfache Verwaltung** unterschiedlicher Gerätekonfigurationen,
- **bessere Wiederverwendbarkeit** der Firmware für HB-L1R-THT und HB-L2R-THT.

Für eine neue Gerätevariante muss in der Regel nur die Datei `HB-LxR-THT_ext.h` angepasst werden, während `HB-LxR-THT.ino` unverändert bleibt.

---

## Lizenz

Creative Commons **CC BY-NC-SA 3.0 DE**

Sie dürfen das Projekt teilen und bearbeiten unter folgenden Bedingungen:

- Namensnennung
- nicht kommerziell
- Weitergabe unter gleichen Bedingungen

<http://creativecommons.org/licenses/by-nc-sa/3.0/de/>