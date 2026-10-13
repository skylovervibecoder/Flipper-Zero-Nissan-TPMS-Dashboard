# Flipper-Zero-Nissan-TPMS-Dashboard
Flipper Zero app for pairing receiving and transmitting TPMS sensors data on Nissan cars.
 
TESTED WITH MOMENTUM DEV FW

TESTED CAR 
NISSAN XTRAIL 2019

# Nissan TPMS Dashboard for Flipper Zero

An all-in-one TPMS (Tire Pressure Monitoring System) application for Flipper Zero designed for Nissan and Renault sub-GHz TPMS sensors operating at **433.92 MHz**.

This tool allows you to monitor tire pressure and temperature in real-time, transmit TPMS signals with customizable pressure levels, pair new sensors automatically, and manage profiles for multiple vehicles.

---

## Key Features

* **TPMS RX (Receiver):** Listens on 433.92 MHz and displays real-time tire pressure and temperature for all 4 wheels. The RGB LED flashes with changing colors upon receiving valid telemetry frames.
* **TPMS TX (Transmitter):** Transmits TPMS data frames with custom pressure values for individual wheels or all 4 wheels simultaneously.
* **TPMS PAIR (Auto-Pairing):** Sniffs surrounding TPMS sensors regardless of their ID, allowing manual assignment of detected sensors to specific wheels and saving the setup as a vehicle profile.
* **Vehicle Manager:** Save, load, and delete custom profiles for up to 12 vehicles on the SD card. Switch between saved vehicles directly from the main menu using quick key shortcuts.
* **Settings & Custom ID Editor:** Manually edit 6-digit hex sensor IDs for each wheel, reset parameters to defaults, and manage vehicle configurations.

---

## Technical Overview

* **Frequency:** 433.92 MHz
* **Modulation & Encoding:** FSK, Manchester Encoding (50 µs symbol duration)
* **Protocol Compatibility:** "Renault" TPMS protocol format (used across various Nissan and Renault vehicles)
* **Frame Structure (9 Bytes):**
  * `Byte 0`: Flags (bits 7..2) + Pressure High Bits (bits 1..0)
  * `Byte 1`: Pressure Low Bits (1 unit = 0.75 kPa)
  * `Byte 2`: Temperature in Celsius (+ 30°C offset)
  * `Bytes 3–5`: 3-Byte Sensor ID
  * `Bytes 6–7`: Status Bytes
  * `Byte 8`: CRC8 (Polynomial: `0x07`, Init: `0x00`)

---

## File Storage & Directories

All application configuration files are stored locally on the SD card:

```text
/ext/apps_data/nissan_dashboard/
├── config.txt                   # Stores the name of the last used vehicle profile
└── cars/                        # Vehicle profiles folder
    ├── MY_CAR.car               # Individual vehicle profile file
    └── FAMILY_CAR.car
