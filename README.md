# Projekt: LCD1602 Anzeige mit PIC18F46K22

Natürlich! Hier ist eine klare und strukturierte Projektbeschreibung für dein **LCD1602-Projekt mit dem PIC18F46K22**, ideal für GitHub:

---

## Projekt: LCD1602 Anzeige mit PIC18F46K22

### Beschreibung

Dieses Projekt zeigt, wie man ein **LCD1602-Display im 4-Bit-Modus** mit einem **PIC18F46K22 Mikrocontroller** ansteuert. Zusätzlich wird ein analoges Signal (z. B. von einem Sound-Sensor-Modul) auf dem Display angezeigt. Optional kann auch ein Digitalpegel (z. B. bei Geräuscherkennung) ausgewertet und als „LOUD!“ angezeigt werden.

---

### Verwendete Komponenten

* PIC18F46K22 Mikrocontroller
* LCD1602 Modul (4-Bit Interface)
* Sound Sensor Modul (analog A0 + digital D0)
* Stromversorgung (z. B. 5 V USB oder Labornetzteil)
* Mikrocontroller-Programmer (z. B. PICkit 3/4 oder SNAP)
* MPLAB X IDE + XC8 Compiler
* (optional) Steckbrett und Jumper-Kabel

---

### Pinbelegung

| LCD1602 Pin | PIC18F46K22 Pin (PORTA) |
| ----------- | ----------------------- |
| RS          | RA0                     |
| EN          | RA1                     |
| D4          | RA2                     |
| D5          | RA3                     |
| D6          | RA4                     |
| D7          | RA5                     |

| Sensor-Pin | PIC18F46K22 Pin |
| ---------- | --------------- |
| A0         | RB3 (AN11)      |
| D0         | RB5 (Digital)   |
| VCC / GND  | 5V / GND        |

---

### Funktion

* **Zeile 1** des LCD zeigt den aktuellen analogen Pegel (0–1023) des Eingangssignals an.
* **Zeile 2** zeigt **„LOUD!“**, wenn D0 = High (z. B. Klatschen oder Knall).
* Wenn kein lautes Geräusch erkannt wurde, bleibt die zweite Zeile leer.

---

### Mikrocontroller-Konfiguration

* Taktfrequenz: **16 MHz (interner Oszillator)**
* ADC: **AN11 (RB3)** aktiviert
* D0: **RB5** als digitaler Eingang
* LCD läuft im **4-Bit-Modus**
* Kein Interrupt nötig

---

![IMG_20250531_165719](https://github.com/user-attachments/assets/499ef9bf-051b-4f1f-83a5-7d72884a2d08)


### Nützliche Hinweise

* Der ADC-Wert ändert sich bei leisen Geräuschen kaum – teste mit lauten Klatschen.
* Für den Schwellenwert kann alternativ `analog > 600` verwendet werden, um „LOUD!“ basierend auf analogem Wert zu zeigen.
* Bei Problemen mit dem ADC: Stelle sicher, dass **ANSELBbits.ANSB3 = 1** gesetzt ist und **RB3** als Eingang konfiguriert ist.


### Beispielanzeige
![IMG_20250531_193036](https://github.com/user-attachments/assets/c99180d3-4ec9-4ffa-9187-b91a609b852b)

