# Flipper-Zero-Nissan-TPMS-Dashboard
Flipper Zero app for pairing receiving and transmitting TPMS sensors data on Nissan cars.
TESTED WITH MOMENTUM DEV FW

TESTED CAR 
NISSAN XTRAIL 2019

Nissan TPMS Dashboard (Flipper Zero)

A Flipper Zero app to receive, transmit and manage tire pressure monitoring system (TPMS) signals at 433.92 MHz (FSK, Manchester, 9-byte frames with CRC8).

App category: Sub-GHz

Disclaimer

Please read carefully before using the app.

Lawful and responsible use. 
This app is intended for study, lab testing and experiments on your own vehicle and your own sensors.
Radio regulations. Transmitting at 433.92 MHz is subject to the rules of your country (power, transmission time, permitted use). The app only checks that the firmware allows transmission on that frequency: compliance with the law remains your responsibility.
Road safety. TPMS is a safety system. Sending false pressure values can hide a tire that is actually underinflated or damaged. Do not use the app to mask faults, and do not use it while driving on public roads. Always check the real pressure with a gauge.
No warranty. The software is provided "as is", without warranties of any kind. The author is not liable for damage to people, vehicles, sensors or devices, or for legal consequences arising from use of the app. You use it entirely at your own risk.
No affiliation. This project is independent and is not affiliated with, endorsed by or sponsored by Nissan, Renault or any vehicle or sensor manufacturer. Brand and protocol names are used only to describe compatibility.
Data and IDs. Sensor IDs are stored on your SD card. Do not share your .car files if you do not want your sensor IDs to become public.

How to use

Installation

Build the app (application.fam + nissan_dashboard.c + icon nissan_dashboard.png) or copy the .fap file to your Flipper.
Put it in the /ext/apps/Sub-GHz/ folder on the SD card.
Open it from Apps → Sub-GHz → Nissan Dashboard.
Main menu
Item	What it does
TPMS RX	Listens and shows pressure and temperature of the 4 sensors
TPMS TX	Transmits TPMS frames with the pressure you choose for each wheel
TPMS PAIR	Receives nearby sensors and assigns them to wheels
Settings	Edit IDs, save/load/delete cars
About	Version and author

In the app itself the menu entries read "TPMS RX", "TPMS TX", "TPMS PAIR", "Impostazioni" (Settings) and "About".

Controls: Up/Down select the item, OK enters, Back exits the app. If a car is active, its name appears in the title and Left/Right switch to the previous/next car.

Wheels are always in the order ANT SX (front left), ANT DX (front right), POST SX (rear left), POST DX (rear right).

First launch: setting up your sensors

At first the IDs are placeholders (00 00 01 … 00 00 04). To use your own sensors you have two options:

A) With TPMS PAIR (recommended)

Enter TPMS PAIR: the app listens at 433.92 MHz.
Wake the sensors (with a TPMS activation tool, or by slightly inflating/deflating the tire): they appear in the list.
Up/Down select a sensor, Left/Right assign the wheel (ASx, ADx, PSx, PDx, --).
When all 4 wheels are assigned, press OK: the app asks for the car name and saves it.
Long-press OK clears the list.

B) Manually from Settings

Enter Settings and choose the wheel.
In the ID editor: Left/Right select the digit, Up/Down change the value, OK confirms, Back cancels.
Use Salva auto (Save car) or Salva con nome... (Save as...) to store the configuration.
TPMS RX
Left/Right choose the wheel to highlight.
On every valid frame the LED blinks and changes color.
Long-press OK resets the displayed values.
Back returns to the menu.
TPMS TX
Left/Right choose the wheel (ANT SX, ANT DX, POST SX, POST DX, RESET).
Up/Down change the pressure by 1 kPa (5 kPa when held).
OK sends the selected wheel.
Long-press OK applies the chosen pressure to all wheels and sends them.
RESET + OK: front 230 kPa, rear 210 kPa, then sends all.
Back returns to the menu.

When entering TX, the app also reads TPMS-Editor .tpms profiles (in /ext/apps_data/tpms_editor, including subfolders) and, if the ID matches, takes flags, status bytes and temperature from them. Without a profile it uses provisional values.

Settings
Up/Down select the entry, OK opens or runs it.
Salva auto (Save car): updates the active car. A * in the title means unsaved changes.
Salva con nome... (Save as...): saves as a new car.
Carica auto (Load car): list of saved cars (max 12). OK loads, Left deletes.
Predefiniti (Defaults): restores the placeholder IDs.
Where data is stored
Path	Contents
/ext/apps_data/nissan_dashboard/cars/<NAME>.car	One configuration per car (ID, flags, status bytes, temperature, pressure of each wheel)
/ext/apps_data/nissan_dashboard/config.txt	Name of the last used car, reloaded at startup
Troubleshooting
RX shows nothing: TPMS sensors transmit only briefly (e.g. when the car moves or when activated); use a TPMS activation tool or change the pressure. Check that the IDs in Settings match your sensors, or use TPMS PAIR.
TX does not transmit: your firmware may not allow transmission at 433.92 MHz in your region.
Car name will not save: maximum 10 characters; the limit is 12 saved cars.
