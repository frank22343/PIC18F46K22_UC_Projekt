# A.Projekt: LCD1602 Anzeige mit PIC18F46K22

![Screenshot 2025-05-30 113338](https://github.com/user-attachments/assets/62b7c14f-1afe-4dc4-9ca5-6959ea25c5c9)

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
---

## B.Projekt: MPU6050 Gyroskop & Beschleunigungssensor mit PIC18F46K22

### Beschreibung

Dieses Projekt demonstriert die Kommunikation zwischen einem **MPU6050-Modul (Gyroskop + Beschleunigungssensor)** und dem **PIC18F46K22 Mikrocontroller** über die **I²C-Schnittstelle**. Die ausgelesenen Beschleunigungswerte in X-, Y- und Z-Richtung werden auf einem **LCD1602 Display** angezeigt.

---

### Verwendete Komponenten

![IMG_20250531_201643](https://github.com/user-attachments/assets/3f4d9804-63d8-4d88-af39-409c565513b5)


* PIC18F46K22 Mikrocontroller
* MPU6050 Gyro-/Beschleunigungssensor
* LCD1602 (4-Bit-Modus)
* 5V Stromversorgung
* Pull-up-Widerstände für SDA & SCL (ca. 4.7kΩ)
* MPLAB X IDE + MCC + XC8 Compiler
* PIC Programmer (z. B. PICkit 4)

---

### Pinbelegung

| Komponente     | PIC18F46K22 Pin          |
| -------------- | ------------------------ |
| SDA            | RC4 (SDA1)               |
| SCL            | RC3 (SCL1)               |
| MPU6050 AD0    | GND (I2C-Adresse = 0x68) |
| INT (optional) | nicht verwendet          |
| LCD RS         | RA0                      |
| LCD EN         | RA1                      |
| LCD D4–D7      | RA2–RA5                  |

---

### Projektfunktionen

* Initialisiert den **MPU6050** über I²C.
* Liest periodisch die **Beschleunigungsdaten (X, Y, Z)**.
* Zeigt sie als G-Werte auf dem LCD an.
* Meldet **"MPU6050 READY"** bei erfolgreicher Initialisierung.
* Option: Zeigt „I2C Error“ bei Verbindungsfehlern.

---

### Mikrocontroller-Konfiguration (via MCC)

* Takt: **64 MHz (PLL aktiv, interner OSC)**
* I²C1: aktiviert, Standard-Mode 100 kHz oder Fast-Mode 400 kHz
* LCD: 4-Bit-Modus, manuell über PORTA gesteuert
* Pull-ups extern an SDA & SCL erforderlich

---

### Tipps zur Fehlersuche

* MPU6050 AD0 muss **an GND** für Adresse 0x68 (Standard).
* **SCL und SDA** benötigen **Pull-up-Widerstände**!
* Wenn auf LCD nur „MPU6050 READY“ erscheint, aber keine Werte:
  → Prüfe I2C-Adresse, Kabel, Versorgung (3.3 V / 5 V-kompatibel).
* Bei Fehlern: auf LCD erscheint „I2C Read Error“.

---

## C. Projekt: RTC DS1307 Echtzeituhr mit PIC18F46K22

![IMG_20250531_155511](https://github.com/user-attachments/assets/dd2e998c-bdaa-48a1-b87a-3472b43764c9)

### Projektübersicht

Dieses Projekt demonstriert die Kommunikation zwischen dem **DS1307 Echtzeituhr-Modul (RTC)** und dem **PIC18F46K22 Mikrocontroller** über die **I²C-Schnittstelle**. Die aktuelle Uhrzeit wird ausgelesen und auf einem **LCD1602 Display** angezeigt.

---

### Verwendete Komponenten

* **PIC18F46K22** Mikrocontroller
* **DS1307 RTC Modul** (mit CR2032 Knopfzelle)
* **LCD1602 Display** (4-Bit-Modus)
* **Pull-up-Widerstände** für SDA & SCL (\~4.7kΩ empfohlen)
* **5V Stromversorgung**
* **MPLAB X IDE + MCC + XC8 Compiler**
* **PICkit 4 oder vergleichbarer Programmer**

---

### Pinbelegung

![IMG_20250531_201502](https://github.com/user-attachments/assets/9b7b035f-7279-4f78-92e8-d0dd7d1b145a)


| Komponente | PIC18F46K22 Pin |
| ---------- | --------------- |
| SDA (RTC)  | RC4 (SDA1)      |
| SCL (RTC)  | RC3 (SCL1)      |
| LCD RS     | RA0             |
| LCD EN     | RA1             |
| LCD D4–D7  | RA2–RA5         |

---

### ⚙️ Projektfunktionen

* Initialisiert den **DS1307 RTC-Chip** über I²C.
* Liest die **Uhrzeit (Stunde, Minute, Sekunde)** im 24h-Format aus.
* Zeigt die Zeit auf dem **LCD1602** an

### Aufbau der RTC-Daten (DS1307)

* Register 0x00 – Sekunden (BCD)
* Register 0x01 – Minuten (BCD)
* Register 0x02 – Stunden (BCD, Bit 6 = 12/24h-Modus)

> Alle Werte sind im **BCD-Format** und müssen ggf. umgewandelt werden:

---
## Wichtige Hinweise

* **CR2032-Knopfzelle** muss eingelegt sein, damit die Zeit bei Stromverlust erhalten bleibt.
* **Pull-ups** auf SDA/SCL sind notwendig.
* Initiale Zeiteinstellung kann per Code erfolgen und dann dauerhaft deaktiviert werden.

---
### Erweiterungsmöglichkeiten
* **Alarm-Funktion** per Vergleich mit aktueller Uhrzeit

---
## D.Projekt: Sound Sensor Modul mit PIC18F46K22 & LCD1602

### Projektübersicht

In diesem Projekt wird ein **digitales und analoges Sound Sensor Modul** (z. B. KY-038 oder vergleichbar) mit dem **PIC18F46K22 Mikrocontroller** verwendet. Der analoge Pegel des Umgebungsgeräusches wird über den **ADC des Mikrocontrollers** eingelesen und auf einem **LCD1602** angezeigt. Gleichzeitig wird das **digitale Ausgangssignal (D0)** ausgewertet, um laute Geräusche wie Klatschen zu erkennen und visuell auf dem Display als `"LOUD!"` anzuzeigen.

---
### Verwendete Komponenten

* **PIC18F46K22 Mikrocontroller**
* **Sound Sensor Modul** 
* **LCD1602 Display** im 4-Bit-Modus
* **5V Stromversorgung**
* **MPLAB X IDE + MCC + XC8 Compiler**
* **Programmiergerät** (PICkit 3)

---
### Pinbelegung

| Funktion           | PIC18F46K22 Pin |
| ------------------ | --------------- |
| LCD RS             | RA0             |
| LCD EN             | RA1             |
| LCD D4–D7          | RA2–RA5         |
| Sound A0 (analog)  | RB3 (AN11)      |
| Sound D0 (digital) | RB5             |

---

### Anschluss des Sound Sensors

![IMG_20250531_201832](https://github.com/user-attachments/assets/52a6883e-fd46-41ee-a03c-f15a10f2167f)

| Sensor-Pin | Funktion          | Anschluss  |
| ---------- | ----------------- | ---------- |
| A0         | Analoger Ausgang  | RB3 (AN11) |
| D0         | Digitaler Ausgang | RB5        |
| GND        | Masse             | GND        |
| VCC        | +5 V              | VDD        |

---
### Vorschau / Bildvorschlag

Füge optional ein Bild deines Aufbaus oder ein LCD-Foto bei, z. B.:

![IMG_20250531_193036](https://github.com/user-attachments/assets/c99180d3-4ec9-4ffa-9187-b91a609b852b)


