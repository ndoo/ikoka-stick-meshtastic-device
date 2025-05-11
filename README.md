# Ikoka Stick Meshtastic Device

## Ikoka! (行こか!)

“行こか?” or “行こか!” is [Kansai dialect](https://en.wikipedia.org/wiki/Kansai_dialect) for “shall we go?” or “let’s go!”.

I hope that building these long-range Meshtastic designs inspires you to go on your next [DXing](https://en.wikipedia.org/wiki/DXing) adventure.

## Features

- LoRa
  - Up to 33 dBm (2 W) output power
  - 410–493 MHz (433 MHz band) or 850–930 MHz (868/915/923 MHz band)
- Bluetooth 5 LE
- Wi-Fi 4 (2.4 GHz)
- Lithium-ion battery with charging
- 0.96" OLED display

Feature set above depends on part selection.

### Hardware

### Parts Selection

Several options are available depending on the feature set you need.

#### Microcontroller

- [Seeed Studio XIAO-nRF52840](https://www.seeedstudio.com/Seeed-XIAO-BLE-nRF52840-p-5201.html) - Bluetooth 5/LE
- [Seeed Studio XIAO-ESP32-S3](https://www.seeedstudio.com/XIAO-ESP32S3-p-5627.html) - Bluetooth 5/LE and Wi-Fi 4 (2.4 GHz)

#### LoRa Module

- [E22-400M22S](https://www.cdebyte.com/products/E22-400M22S) (410–493 MHz at 22 dBm)
- [E22-400M30S](https://www.cdebyte.com/products/E22-400M30S) (410–493 MHz at 30 dBm)
- [E22-400M33S](https://www.cdebyte.com/products/E22-400M33S) (410–493 MHz at 33 dBm)
- [E22-900M22S](https://www.cdebyte.com/products/E22-900M22S) (850–930 MHz at 22 dBm)
- [E22-900M30S](https://www.cdebyte.com/products/E22-900M30S) (850–930 MHz at 30 dBm)
- [E22-900M33S](https://www.cdebyte.com/products/E22-900M33S) (850–930 MHz at 33 dBm)

#### Lithium-ion Battery (4.2V charging termination, optional)

- 21700 Lithium-ion battery cell (4.2V charge termination; holder: [BeilaMoo PA21700*1-SMT](https://www.beilamoo.com/sdm/1074412/4/pd-5180803/21061576-2986071/ONE_21700_Battery_Holder_with_Surface_Mount_SMT.html)/[MYOUNG BH-21700-B1BJ001](https://jlcpcb.com/partdetail/Myoung-BH_21700B1BJ001/C20606791))
- Lithium-polymer pouch battery cell (4.2V charge termination; connector: Molex PicoBlade 1x02P, pitch 1.25mm)
- Do not use both a 21700 and LiPo battery simultaneously, they will be shorted together in parallel

##### Wiring for Battery Charging

You will need a PicoBlade Female-to-Pigtail cable assembly such as Molex [218112-0200](https://www.molex.com/en-us/products/part-detail/2181120200). A compatible cable ships with Heltec Wireless and LILYGO LoRa products so you probably have spares you can use. [Muzi Works](https://muzi.works/products/battery-cable-molex-picoblade) and [Rokland](https://store.rokland.com/products/battery-connector-cables-battery-wires-jst-1-25-5pcs-for-lilygo-and-heltec) also sell compatible cables.

1. Trim the pigtail length to around 5cm if it is longer
2. Strip 2mm of insulation from each pigtail, then twist and tin the wire strands
3. Solder the red pigtail (or pin 1) to the BAT+ pad on the back of the XIAO module
4. Solder the black pigtail (or pin 2) to the BAT- pad on the back of the XIAO module
5. Plug the cable into the XIAO Charger connector on the Ikoka Stick

In my previous design, the [Ikoka Nano](https://github.com/ndoo/ikoka-nano-meshtastic-device), the XIAO module was SMD soldered onto the board, while the BAT+ pad was soldered through a plated through-hole via. However, the actual solder joint is buried and couldn't be inspected for continuity, quality and ensuring the BAT+ pad was not shorted to the BAT- pad.

In the interest of ease-of-assembly and keeping the XIAO module interchangeable, while not wasting the built-in battery charging circuit on XIAO modules, this approach was chosen instead.

#### OLED Display (Optional)

- Generic SSD1306 0.96" OLED display modules with 2.54mm pin headers [https://www.aliexpress.com/item/1005008077705181.html]((AliExpress))

## Firmware

### GPIO Assignment

| XIAO Pin | Function | XIAO-nRF52840 | XIAO-ESP32-S3 |
|---|---|---|---|
| 1 (D0) | User button | 2 (P0.02) | 1 |
| 2 (D1) | EBYTE E22 - DIO1 | 3 (P0.03) | 2 |
| 3 (D2) | EBYTE E22 - RST | 28 (P0.28) | 3 |
| 4 (D3) | EBYTE E22 - BUSY | 29 (P0.29) | 4 |
| 5 (D4) | EBYTE E22 - SPI NSS | 4 (P0.04) | 5 |
| 6 (D5) | EBYTE E22 - RXEN | 5 (P0.05) | 6 |
| 7 (D6) | SSD1306 OLED - I2C SDA | 43 (P1.11) | 43 |
| 8 (D7) | SSD1306 OLED - I2C SCL | 44 (P1.12) | 44 |
| 9 (D8) | EBYTE E22 - SPI SCK | 45 (P1.13) | 7 |
| 10 (D9) | EBYTE E22 - SPI MISO | 46 (P1.14) | 8 |
| 11 (D10) | EBYTE E22 - SPI MOSI | 47 (P1.15) | 9 |
| 12 | SSD1306 OLED - 3.3V | 3V3 | 3V3 |
| 13 | GND | GND | GND |
| 14 | NC | 5V | 5V |

### Meshtastic Compatibility

The XIAO module is intended to be socketed with pin headers/pin sockets, to allow swapping out modules depending on what features are needed (Bluetooth, Wi-Fi, different power consumption profiles, etc.); Compatibility with official Meshtastic firmware depends on the inserted XIAO board.

#### XIAO-nRF52840

- EBYTE E22 LoRa
  - LoRa pins are identical to the officially-supported [Seeed Xiao NRF52840 Kit](https://www.seeedstudio.com/XIAO-nRF52840-Wio-SX1262-Kit-for-Meshtastic-p-6400.html) on [Meshtastic Web Flasher](https://flasher.meshtastic.org/)
  - LoRa will work out of the box on officially-supported firmware
  - Special consideration must be taken if using the E22-900M33S module
    - Set the transmit power to ≤ 9 dBm on first use (when setting the LoRa region)
    - **Transmit power must never be set greater than 9 dBm*- to avoid damaging the module's RF frontend
- SSD1306 OLED I2C
  - Pin D6/P1.11 and D7/P1.12 are [reserved for the L76K GPS module in the officially-supported variant](https://github.com/meshtastic/firmware/blob/152b8b1b0235bc461c6e4451fbcdac0987b8bf90/variants/seeed_xiao_nrf52840_kit/variant.h#L137-L138)
  - A custom firmware must be built to define these pins as I2C (TODO)
- User button
  - Pin D0/P0.02 is [reserved for the L76K GPS module in the officially supported variant](https://github.com/meshtastic/firmware/blob/152b8b1b0235bc461c6e4451fbcdac0987b8bf90/variants/seeed_xiao_nrf52840_kit/variant.h#L144)
  - A custom firmware must be built to define this pin as the user button (TODO)

### XIAO-ESP32-S3

- Pin definitions are different from the officially-supported [Seeed Xiao ESP32-S3 Kit](https://www.seeedstudio.com/Wio-SX1262-with-XIAO-ESP32S3-p-5982.html)
  - This is because Seeed uses GPIOs on the 30-pin board-to-board press-fit connector instead of the standard XIAO pins
  - A custom firmware must be built (TODO)

## PCB Renders

### PCB Top

![top](https://ndoo.github.io/ikoka-stick-meshtastic-device/top.png)

### PCB Bottom

![bottom](https://ndoo.github.io/ikoka-stick-meshtastic-device/bottom.png)

### Rotating GIF

![animation](https://ndoo.github.io/ikoka-stick-meshtastic-device/rotating.gif)

(Rendered with [kicad-render](https://github.com/linalinn/kicad-render).)