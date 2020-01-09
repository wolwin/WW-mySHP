# WW-mySHP - SHP_Sens-Gar-118x

[Zurück zur Übersicht ...](../README.md)

#### Projekt-Beschreibung

Sensorplatine für GARDENA 118x Geräte zum Anschluß an 'HB-UNI-Sens-X' oder 'HB-UNI-Mini-X'. Eine Einbau- bzw. Montagemöglichkeit kann über vier 2 mm Platinen-Löcher realisiert werden.

Die Platine prüft alle 5 Minuten den Status von ein bzw. zwei angeschlossenen GARDENA 118x Sensoren (bzw. potential freien Schaltern). Über die Ausgangsports des ATtiny 24a wird ein Änderungsflag, der Sensorstatus ON / OFF und bei den GARDENA Sensoren der Leitungsstatus VERBUNDEN / UNTERBROCHEN ausgegeben.

#### Platine
- Platine 'Sens-Gar-118x' - [Zeigen ...](https://github.com/wolwin/WW-myPCB/blob/master/PCB_Sens-Gar-118x/README.md)
- Platine 'HB-UNI-Mini-X' - [Zeigen ...](https://github.com/wolwin/WW-myPCB/blob/master/PCB_HB-UNI-Mini-X/README.md)

#### Funktion
- Allgemeine Funktionsbeschreibung von Platine und ATtiny24a

      // Description:
      // - the ATtiny starts with an ON state on its PB0/PA5
      //   - the PB0/PA5 of the ATtiny is connected to a N-MOSFET which turns on
      //     GND when PB0/PA5 is HIGH (connect the GARDENA sensor(s) as a voltage
      //     divider to the ATtiny - details see below)
      // - the ATtiny checks the status of the connected GARDENA sensors and
      //   and sets the output ports to HIGH / LOW - if there is a status change
      //   the change output port is toogled.
      // - the error output port is set to HIGH if the GARDENA sensor is not
      //   (longer) connected.
      // - the ATtiny goes to sleep mode (5uA) for 300 seconds
      // - the status of the output/error ports remains LOW/HIGH in sleep mode.
      // - after sleep time has been expired the ATtiny starts again
      //
      // - tested with:
      //   - ATtiny13A => sleep    = 5uA,
      //                  no sleep = 2.3 mA (2.6 mA with MOSFET control)
      //   - ATtiny24A => sleep    = 5uA

- Funktion der GARDENA 118x Sensoren (z.B. mit einem GARDENA Bewässerungscomputer EasyControl)
      // GARDENA
      //
      // GARDENA - Bewässerungscomputer EasyControl - Art.-Nr. 1881
      // GARDENA - Regensensor electronic 1189-20
      // GARDENA - Bodenfeuchtesensor 1188-20
      // GARDENA - Kabelweiche, 165 cm lang - Ersatzteil-Nr. 01189-00.630.00
      //
      // - GARDENA - Bodenfeuchtesensor 1188-20
      //   = 10k Ohm  = trocken   -->  Bewaesserungscomputer = an
      //   =   0 Ohm  = feucht    -->  Bewaesserungscomputer = aus
      // - GARDENA - Regensensor electronic 1189-20
      //   = 10k Ohm  =  trocken  -->  Bewaesserungscomputer = an
      //   =   0 Ohm  =  nass     -->  Bewaesserungscomputer = aus
      // - GARDENA - Kabelweiche mit Bodenfeuchtesensor 1188-20 und Regensensor 1189-20
      //   -> (Widerstands-) Parallelschaltung der (beiden) Sensoren
      //      Feuchtesensor  10k Ohm (trocken) -->    0 Ohm  -->  Bewaesserungscomputer = aus
      //      Regensensor      0 Ohm (nass)    /
      //      Feuchtesensor  10k Ohm (trocken) -->   5k Ohm  -->  Bewaesserungscomputer = an
      //      Regensensor    10k Ohm (trocken) /
      //      Feuchtesensor    0 Ohm (feucht)  -->    0 Ohm  -->  Bewaesserungscomputer = aus
      //      Regensensor      0 Ohm (nass)    /
      //      Feuchtesensor    0 Ohm (feucht)  -->    0 Ohm  -->  Bewaesserungscomputer = aus
      //      Regensensor    10k Ohm (trocken) /


- ATtiny24a Anschlüsse und Programmiereinstellungen
      // ATMEL ATTINY 24a
      // ----------------
      //                        +-\/-+                                   ARDUINO Pro Mini
      //                  VCC  1|    |14  GND
      //                  PB0  2|    |13  PA0 ADC0  (Change_Toogle 0/1)   ----> o A1
      //                  PB1  3|    |12  PA1 ADC1  (PIN_OUT_1_Status)    ----> o A2
      //              RES PB3  4|    |11  PA2 ADC2  (PIN_OUT_2_Status)    ----> o A3
      //                  PB2  5|    |10  PA3 ADC3  (PIN_OUT_1_Error)     ----> o PD5
      // (ADC_IN_1)  ADC7 PA7  6|    |9   PA4 ADC4  (PIN_OUT_2_Error)     ----> o PD6
      // (ADC_IN_2)  ADC6 PA6  7|    |8   PA5 ADC5  (PIN_MOSFET)
      //                        +----+
      //
      // Recommended settings for this sketch: Arduino IDE > Tools ->
      // Board                     :  ATtiny24
      // Processor Version         :  ATtiny24a
      // Processor Speed           :  1MHz Internal Oscillator
      // Use Bootloader            :  No (ISP Programmer Upload)
      // Millis, Tone Support      :  Millis Avaible, No Tone
      // Millis Accuracy           :  Better Or Equal 1.666% Error (Default)
      // Print Support             :  Bin, Hex, Dec Supported
      // Serial Support            :  Half Duplex, Read+Write
      // Link Time Optimisation    :  LTO Disabled
      // Brown-out Detection Level :  Disabled
      // Override Clock Source     :  Standard
      // Override Frequency        :  Standard

      Remarks:
      // - the bootloader of the ATtiny13A (ATtiny24A) must be set first - if  
      //   not set, the power consumtion of 5uA could not be reached !
      // - the Brown out Detection Level of the board must be disabled !


#### ATtiny24a INO-Script
[Download ...](./bin/GARDENA_Sensor_118x_20191228.zip)

#### Bilder
- Übersicht - 'Sens-Gar-118x'
  - die GARDENA 118x Sensoren werden mit ihren Zuleitungskabeln über die Schraubklemmen verbunden (rechts)
    - Gerät 1 = Kabel 'Gar1 + GND'
    - Gerät 2 = Kabel 'Gar2 + GND'
  - die Ausgabe-Ports des ATtiny24a sind über eine JST-XH Buchse herausgeführt (oben mittig)
<br><br>
- Ansicht
<br><br>
![WW-mySHP - Sens-Gar-118x](./img/SHP_Sens-Gar-118x_01.jpg "Sens-Gar-118x")
<br><br>![WW-mySHP - Sens-Gar-118x](./img/SHP_Sens-Gar-118x_02.jpg "Sens-Gar-118x")
<br><br>



#### Historie
- 2020-01-10 - Erstveröffentlichung
