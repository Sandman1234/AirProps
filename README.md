# Airsoft Props and Accessories

## Bomb

### Table of Contents

- [Bill of Materials](#bill-of-materials)
  - [Components and Modules](#components-and-modules-w-hestorehu-article-numbers)
  - [Price Calculation](#price-calculation-for-one-and-multiple-pieces)
- [Topology and Schematic](#topology-and-schematic)

## Bill of Materials

### Components and Modules w/ Hestore.hu Article Numbers

| Hestore.hu Article No. | Qty. | Component / Module |
|---|---:|---|
| `100.423.84` | 1 | SFN-1207PA5.0 |
| `100.385.19` | 1 | MAX7219-SLD |
| `100.497.85` | 1 | ESP32-D1-MINI-CP2104-C |
| `100.420.93` | 1 | TP4056-1A-USBC |
| `100.417.73` | 1 | KP-4X4/MEM |
| `100.403.31` | 1 | L-793GD |
| `100.201.10` | 1 | L-53 IT |
| `100.355.20` | 1 | RC522-MFRC |
| `100.375.86` | 1 | PAC-3V3-3P |
| `100.510.28` | 2 | ECEA0JKA101I |
| `100.510.27` | 1 | ECEA0JKA221B |
| `100.205.41` | 2 | 10 K 1% |
| `100.204.99` | 2 | 200 R 1% |

### Price Calculation for One and Multiple Pieces

| Number of Units | Total Price |
|---:|---:|
| 1 | 8,055 HUF |
| 5 | 31,769 HUF |
| 10 | 59,100 HUF |
> **Price reference:** These prices are in HUF and were recorded on **2026-10-06** and the prices only represent the electronical components only!.

## Topology and Schematic
![topology](https://raw.githubusercontent.com/Sandman1234/AirProps/refs/heads/main/Bomb/_readMe_media/architure.jpeg)
<sub>base topology to work the schematic around</sub>

## Detailed Sub-sections

The project is module based, so any component can be changed, to make the device as customizeable as possible.
the 5 main section is the following
- Main
- Feedback
- Input
- Admin
- Power unit

### Main

This section is just a carrier for the microcontroller unit. As was told before, this unit can also be changed to any other microcontroller based unit. The only condition is the main 3V3 input line.

Required Component:
- ESP32-D1-MINI-CP2104-C

### Feedback

This section is for the device's feedbacks. It is equipped with a MAX7219 based 8x7+DP segment led NUM display, 2 LEDs with their resistors (red and green w/ 200 R) and lastly with a 80dB (85dB and more can cause permanent hearing problems) piezo beeper.

Required Component:
- MAX7219-SLD
- L-793GD
- L-53 IT
- 200 R 1%
- SFN-1207PA5.0


### Admin

### Input

### Power unit

