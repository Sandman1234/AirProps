# Airsoft Props and Accessories

## Bomb

> HU / Magyar : [Magyar változat](#magyar-változat)

#### English version

### Table of Contents

- [Bill of Materials](#bill-of-materials)
  - [Components and Modules](#components-and-modules-w-hestorehu-article-numbers)
  - [Price Calculation](#price-calculation-for-one-and-multiple-pieces)
- [Topology and Schematic](#topology-and-schematic)
- [Detailed Sub-sections](#detailed-sub-sections)
  - [Main](#main)
  - [Feedback](#feedback)
  - [Admin](#admin)
  - [Input](#input)
  - [Power Unit](#power-unit)

---

## Bill of Materials

### Components and Modules w/ Hestore.hu Article Numbers

| Hestore.hu Article No. | Qty. | Component / Module | Sub-section name |
|---|---:|---|---|
| `100.423.84` | 1 | SFN-1207PA5.0 | Feedback |
| `100.385.19` | 1 | MAX7219-SLD | Feedback |
| `100.497.85` | 1 | ESP32-D1-MINI-CP2104-C | Main |
| `100.420.93` | 1 | TP4056-1A-USBC | Power unit |
| `100.417.73` | 1 | KP-4X4/MEM | Input |
| `100.403.31` | 1 | L-793GD | Feedback |
| `100.201.10` | 1 | L-53 IT | Feedback |
| `100.355.20` | 1 | RC522-MFRC | Admin |
| `100.375.86` | 1 | PAC-3V3-3P | Power unit |
| `100.510.28` | 2 | ECEA0JKA101I | Power unit |
| `100.510.27` | 1 | ECEA0JKA221B | Power unit |
| `100.205.41` | 2 | 10 K 1% | Main |
| `100.204.99` | 2 | 200 R 1% | Feedback |

### Price Calculation for One and Multiple Pieces

| Number of Units | Total Price |
|---:|---:|
| 1 | 8,055 HUF |
| 5 | 31,769 HUF |
| 10 | 59,100 HUF |

> **Price reference:** These prices are in HUF and were recorded on **2026-10-06**. The prices represent the electronic components only.

---

## Topology and Schematic

![Topology](https://raw.githubusercontent.com/Sandman1234/AirProps/refs/heads/main/Bomb/_readMe_media/architure.jpeg)

<sub>Base topology used as the foundation for the schematic.</sub>

---

## Detailed Sub-sections

The project is modular, allowing individual components or modules to be replaced to make the device as customizable as possible.

The project is divided into five main sections:

- Main
- Feedback
- Input
- Admin
- Power Unit

### Main

This section primarily acts as the carrier for the microcontroller unit.

As mentioned previously, this unit can be replaced with another microcontroller-based unit. The main requirement is compatibility with the **3.3 V main supply line** and the peripherals used by the project.

A voltage divider consisting of **2 × 10 K 1% resistors** is connected to the main battery line so that the microcontroller can monitor the battery voltage.

With a 1:1 voltage divider, the voltage presented to the analog input is half of the battery voltage.

At a fully charged voltage of approximately **4.2 V**, the analog input receives approximately **2.1 V**.

For this type of cell, approximately **3.5 V** can already be considered a mostly discharged state. The initial implementation will attempt to use **3.2 V** as the software-defined 0% point.

Approximately **2.7 V** is considered the lowest voltage at which the setup may still be able to operate, although the remaining usable battery capacity at this voltage is questionable.

The following table can be used as a reference for calculating the battery state from the analog input:

| Battery Voltage | Analog Voltage | Analog Value | Approx. Percentage |
|---:|---:|---:|---:|
| 4.2 V | 2.10 V | 2606 | 100% |
| 3.7 V | 1.85 V | 2296 | ~50% |
| 3.2 V | 1.60 V | 1985 | Safe 0% |

> **Note:** These percentage values are approximate. Li-Ion/Li-Po discharge curves are not linear, so the final percentage calculation should ideally be calibrated using the actual battery.

**Required Component(s):**

- ESP32-D1-MINI-CP2104-C
- 2 × 10 K 1%

Required Pin(s):
- 1 Anal IO

---

### Feedback

This section is responsible for providing feedback from the device to the player.

It is equipped with:

- A MAX7219-based **8-digit, 7-segment LED display with decimal points**
- One red LED
- One green LED
- 2 × 200 R current-limiting resistors
- An approximately 80 dB piezo buzzer

> **Warning:** Sound levels around 85 dB and above can contribute to permanent hearing damage, especially with prolonged or close-range exposure. Do not place the buzzer directly next to the ear.

**Required Component(s):**

- MAX7219-SLD
- L-793GD
- L-53 IT
- 2 × 200 R 1%
- SFN-1207PA5.0

Required Pin(s):
- 4 SPI (MISO, MOSI, SCLK, CE1 )
- 3 Dig IO ( -, -, PWM )

---

### Admin

This section provides the administrator interface for the device.

It currently uses an **RC522-MFRC RFID module**.

The RFID module can be used by an administrator to arm or disarm the airsoft prop and return it to its default state.

If supported by the selected microcontroller and software, administrator functions may also be controlled wirelessly.

**Required Component(s):**

- RC522-MFRC

Required Pin(s):

Required Pin(s):
- 4 SPI (MISO, MOSI, SCLK, CE2 )

---

### Input

This section is responsible for player input during the arming and disarming process.

It uses a **4 × 4 membrane matrix keypad** with the following characters:

- `0 - 9`
- `A - D`
- `*`
- `#`

**Required Component(s):**

- KP-4X4/MEM

Required Pin(s):
- 8 Dig IO (-, -, -, -, -, -, -, -)

---

### Power Unit

This section keeps the device operational without requiring a USB cable or another external power source.

The design can use different Li-Po or Li-Ion cells. The first prototype will be tested using a repurposed **ZTE battery**.

The battery parameters are:

| Parameter | Value |
|---|---:|
| Model | BL-38CYZTE |
| Rated Capacity | 3850 mAh |
| Typical Capacity | 4500 mAh |
| Nominal Voltage | 3.85 V |
| Specified Charge Voltage | 4.4 V |

> **Note:** The TP4056-based charger used in the initial design normally charges standard Li-Ion/Li-Po cells to approximately **4.2 V**. Therefore, when used with this 4.4 V-rated ZTE cell, the battery will not be charged to its full specified charge voltage.

**Required Component(s):**

- Li-Po or Li-Ion cell(s)
- TP4056-1A-USBC
- PAC-3V3-3P
- 2 × ECEA0JKA101I
- ECEA0JKA221B

---

#### Magyar változat

## Airsoft kellékek és kiegészítők

### Bomba

#### Tartalomjegyzék

- [Anyagjegyzék](#anyagjegyzék)
  - [Alkatrészek és modulok](#alkatrészek-és-modulok-hestorehu-cikkszámokkal)
  - [Árkalkuláció](#árkalkuláció-egy-és-több-darabra)
- [Topológia és kapcsolási rajz](#topológia-és-kapcsolási-rajz)
- [Részletes alrendszerek](#részletes-alrendszerek)
  - [Főegység](#főegység)
  - [Visszajelzés](#visszajelzés)
  - [Adminisztrátori egység](#adminisztrátori-egység)
  - [Bevitel](#bevitel)
  - [Tápellátás](#tápellátás)

---

## Anyagjegyzék

### Alkatrészek és modulok Hestore.hu cikkszámokkal

| Hestore.hu cikkszám | Menny. | Alkatrész / Modul | Alszekció neve |
|---|---:|---|---|
| `100.423.84` | 1 | SFN-1207PA5.0 | Visszajelzés |
| `100.385.19` | 1 | MAX7219-SLD | Visszajelzés |
| `100.497.85` | 1 | ESP32-D1-MINI-CP2104-C | Főegység |
| `100.420.93` | 1 | TP4056-1A-USBC | Tápellátás |
| `100.417.73` | 1 | KP-4X4/MEM | Bevitel |
| `100.403.31` | 1 | L-793GD | Visszajelzés |
| `100.201.10` | 1 | L-53 IT | Visszajelzés |
| `100.355.20` | 1 | RC522-MFRC | Admin |
| `100.375.86` | 1 | PAC-3V3-3P | Tápellátás |
| `100.510.28` | 2 | ECEA0JKA101I | Tápellátás |
| `100.510.27` | 1 | ECEA0JKA221B | Tápellátás |
| `100.205.41` | 2 | 10 K 1% | Főegység |
| `100.204.99` | 2 | 200 R 1% | Visszajelzés |

### Árkalkuláció egy és több darabra

| Darabszám | Teljes ár |
|---:|---:|
| 1 | 8 055 HUF |
| 5 | 31 769 HUF |
| 10 | 59 100 HUF |

> **Árinformáció:** Az árak forintban értendők, és **2026.10.06-án** kerültek rögzítésre. Az összegek kizárólag az elektronikai alkatrészek árát tartalmazzák.

---

## Topológia és kapcsolási rajz

![Topológia](https://raw.githubusercontent.com/Sandman1234/AirProps/refs/heads/main/Bomb/_readMe_media/architure.jpeg)

<sub>A kapcsolási rajz elkészítésének alapjául szolgáló topológia.</sub>

---

## Részletes alrendszerek

A projekt moduláris felépítésű, így az egyes alkatrészek és modulok cserélhetők, ezáltal az eszköz a lehető legnagyobb mértékben testreszabható.

A projekt öt fő egységre osztható:

- Főegység
- Visszajelzés
- Bevitel
- Adminisztrátori egység
- Tápellátás

### Főegység

Ez az egység elsősorban a mikrokontrollert tartalmazza.

A korábban említettek szerint ez az egység más mikrokontroller-alapú megoldásra is lecserélhető. A legfontosabb követelmény a **3,3 V-os fő tápvonallal**, valamint a projektben használt perifériákkal való kompatibilitás.

A fő akkumulátor-tápvonalra egy **2 × 10 K 1%-os ellenállásból álló feszültségosztó** kerül, amely lehetővé teszi, hogy a mikrokontroller mérje az akkumulátor feszültségét.

Az 1:1 arányú feszültségosztó miatt az analóg bemenetre az akkumulátorfeszültség fele jut.

Körülbelül **4,2 V-os** teljesen feltöltött állapotban az analóg bemeneten körülbelül **2,1 V** jelenik meg.

Az ilyen típusú celláknál körülbelül **3,5 V** már nagyrészt lemerült állapotnak tekinthető. A kezdeti megvalósításban **3,2 V** lesz a szoftveresen meghatározott 0%-os szint.

Körülbelül **2,7 V** tekinthető annak a legalacsonyabb feszültségnek, amely mellett a rendszer esetleg még működőképes lehet, azonban ezen a szinten a fennmaradó használható akkumulátorkapacitás már kérdéses.

Az alábbi táblázat referenciaértékként használható az akkumulátor töltöttségének analóg bemeneti értékből történő meghatározásához:

| Akkumulátor feszültsége | Analóg feszültség | Analóg érték | Becsült töltöttség |
|---:|---:|---:|---:|
| 4,2 V | 2,10 V | 2606 | 100% |
| 3,7 V | 1,85 V | 2296 | ~50% |
| 3,2 V | 1,60 V | 1985 | Biztonságos 0% |

> **Megjegyzés:** A százalékos értékek csak közelítő értékek. A Li-Ion/Li-Po akkumulátorok kisütési karakterisztikája nem lineáris, ezért a végleges töltöttségszámítást célszerű a ténylegesen használt akkumulátorhoz kalibrálni.

**Szükséges alkatrész(ek):**

- ESP32-D1-MINI-CP2104-C
- 2 × 10 K 1%

Szükséges Pin(ek):
- 1 Anal IO

---

### Visszajelzés

Ez az egység biztosítja az eszköz visszajelzéseit a játékos számára.

A következő elemekből áll:

- MAX7219-alapú **8 számjegyes, 7 szegmenses LED-kijelző tizedespontokkal**
- Egy piros LED
- Egy zöld LED
- 2 × 200 R áramkorlátozó ellenállás
- Körülbelül 80 dB hangerejű piezo hangjelző

> **Figyelmeztetés:** A körülbelül 85 dB-es vagy annál magasabb hangerő hozzájárulhat maradandó halláskárosodáshoz, különösen tartós vagy közeli kitettség esetén. A hangjelzőt ne helyezd közvetlenül a fül mellé.

**Szükséges alkatrész(ek):**

- MAX7219-SLD
- L-793GD
- L-53 IT
- 2 × 200 R 1%
- SFN-1207PA5.0

Szükséges Pin(ek):
- 4 SPI (MISO, MOSI, SCLK, CE1 )
- 3 Dig IO ( -, -, PWM )

---

### Adminisztrátori egység

Ez az egység biztosítja az eszköz adminisztrátori kezelőfelületét.

Jelenleg egy **RC522-MFRC RFID modult** használ.

Az RFID-modul segítségével az adminisztrátor aktiválhatja vagy deaktiválhatja az airsoft kelléket, illetve visszaállíthatja annak alapállapotát.

Amennyiben a kiválasztott mikrokontroller és a szoftver lehetővé teszi, az adminisztrátori funkciók vezeték nélkül is vezérelhetők.

**Szükséges alkatrész(ek):**

- RC522-MFRC

Szükséges Pin(ek):
- 4 SPI (MISO, MOSI, SCLK, CE2 )

---

### Bevitel

Ez az egység felelős a játékos által végzett bevitelért az aktiválási és deaktiválási folyamat során.

Egy **4 × 4-es membrános mátrix billentyűzetet** használ, amely az alábbi karaktereket tartalmazza:

- `0 - 9`
- `A - D`
- `*`
- `#`

**Szükséges alkatrész(ek):**

- KP-4X4/MEM

Szükséges Pin(ek):
- 8 Dig IO (-, -, -, -, -, -, -, -)

---

### Tápellátás

Ez az egység biztosítja, hogy az eszköz USB-kábel vagy más külső tápforrás nélkül is működhessen.

A kialakítás különböző Li-Po vagy Li-Ion cellákkal is használható. Az első prototípus tesztelése egy újrahasznosított **ZTE akkumulátorral** történik.

Az akkumulátor paraméterei:

| Paraméter | Érték |
|---|---:|
| Modell | BL-38CYZTE |
| Névleges kapacitás | 3850 mAh |
| Tipikus kapacitás | 4500 mAh |
| Névleges feszültség | 3,85 V |
| Előírt töltési végfeszültség | 4,4 V |

> **Megjegyzés:** A kezdeti kialakításban használt TP4056-alapú töltő szabványos Li-Ion/Li-Po cellákat általában körülbelül **4,2 V-ra** tölt. Emiatt ezzel a 4,4 V-os ZTE cellával használva az akkumulátor nem éri el a gyártó által megadott teljes töltési végfeszültséget.

**Szükséges alkatrész(ek):**

- Li-Po vagy Li-Ion cella/cellák
- TP4056-1A-USBC
- PAC-3V3-3P
- 2 × ECEA0JKA101I
- ECEA0JKA221B
