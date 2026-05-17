# ESP-12F I2C Multi-Sensor IoT Node

A compact 2-layer IoT sensor node PCB built around the ESP-12F (ESP8266),
integrating three sensors and an OLED display over a shared I2C bus.

![3D Render](https://github.com/user-attachments/assets/d5d31e32-e57d-4f6c-950c-daff0e87a096)

## Features

- **MCU:** ESP-12F (ESP8266, WiFi-enabled)
- **IMU:** MPU-6050 — 3-axis accelerometer + 3-axis gyroscope (I2C)
- **Environment:** BME280 — temperature, humidity, barometric pressure (I2C)
- **Display:** 0.96" OLED (DM-OLED096-636) — 128×64 pixels (I2C)
- **I2C Pull-ups:** 4.7kΩ on SDA and SCL lines
- **Programming:** TTL header (RX, TX, RST, EN, 3.3V, GND)
- **Mounting:** 4 mounting holes for enclosure/standoffs
- **Antenna:** Keep-out zone for ESP-12F RF clearance
- **Ground Plane:** Full GND fill on both layers
- **Layers:** 2-layer PCB
- **DRC:** 0 errors, 0 warnings
- **Unrouted Nets:** 0
- **Form Factor:** Stackup — sensor board + OLED display board

## PCB Screenshots

| Front Copper | Back Copper | 3D Front | 3D Back |
|---|---|---|---|
| ![](https://github.com/user-attachments/assets/c50260da-0f61-479b-a5d7-6cea6b24e4f4) | ![](https://github.com/user-attachments/assets/715448ce-3086-4714-9f86-c46dab084f9b) | ![](https://github.com/user-attachments/assets/520d872e-60be-49a9-8ece-e96a042e7bbb) | ![](https://github.com/user-attachments/assets/6c234891-cf5a-4771-a411-28d04914ac6b) |

## Schematic Overview

| Block | Components |
|---|---|
| MCU | ESP-12F with decoupling cap (0.1µF) |
| IMU | MPU-6050 with FSYNC/CLKIN and AUX_DA/CL pins |
| Environment Sensor | BME280 with 0.1µF VDDIO decoupling, CSB pulled high |
| Display | DM-OLED096-636 via I2C |
| I2C Bus | Shared SDA/SCL with 4.7kΩ pull-up resistors (R1, R2) |
| Programming | 6-pin TTL header |

![Schematic](https://github.com/user-attachments/assets/83d28084-4d1b-4f44-a60d-424134208a4c)

## I2C Bus Design

All 3 peripherals (MPU-6050, BME280, OLED) share a single I2C bus:

| Device | Default I2C Address |
|---|---|
| MPU-6050 | 0x68 (AD0 = GND) |
| BME280 | 0x76 (SDO = GND) |
| OLED | 0x3C |

4.7kΩ pull-up resistors on SDA and SCL ensure proper signal levels
for all devices. Decoupling capacitors placed close to each IC power pin.

## Design Decisions

| Decision | Reason |
|---|---|
| Shared I2C bus | Reduces pin count; all 3 devices have different addresses |
| 4.7kΩ pull-ups | Standard value for 3.3V I2C at typical speeds |
| Antenna keep-out zone | Prevents copper interference with 2.4GHz RF |
| GND fill both layers | Noise reduction for sensitive sensor readings |
| Stackup form factor | Separates sensor PCB from display for flexible mounting |
| 4 mounting holes | Allows secure enclosure or standoff mounting |

## Files

| File/Folder | Description |
|---|---|
| `https://github.com/user-attachments/files/27865789/gerber_i2c.zip` | Production-ready Gerber files |
| `schematic.pdf` | Full KiCad schematic |
| `bom.csv` | Bill of materials |
| `*.kicad_pcb` | KiCad PCB file |
| `*.kicad_sch` | KiCad schematic file |

## Fabrication Specs

- **Layers:** 2
- **Min trace:** 0.25 mm
- **Via drill:** 0.8 mm
- **Board dimensions:** ~55 × 30 mm (sensor board)

## Tools

- KiCad 8.x
- MPU-6050, BME280, ESP-12F datasheets

## Author

**Simhadri Dharahaas** — ECE Undergraduate | PCB Design & Embedded Systems
[LinkedIn](https://linkedin.com/in/dharahaassimhadri-b17b4b358) | [GitHub](https://github.com/Sdharahaas54)
