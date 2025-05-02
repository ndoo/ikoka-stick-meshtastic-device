# Ikoka Stick Meshtastic Device

## Pin Definitions

| XIAO Pin | Function | XIAO-nRF52840 | XIAO-ESP32-S3 |
|---|---|---|---|
| 1 (D0) | User button | 2 (P0.02) | 1 |
| 2 (D1) | EBYTE E22 - DIO1 | 3 (P0.03) | 2 |
| 3 (D2) | EBYTE E22 - RST | 28 (P0.28) | 3 |
| 4 (D3) | EBYTE E22 - BUSY | 29 (P0.29) | 4 |
| 5 (D4) | EBYTE E22 - SPI NSS | 4 (P0.04) | 5 |
| 6 (D5) | EBYTE E22 - RXEN | 5 (P0.05) | 6 |
| 7 (D6) | SSD1306 OLED - I2C SCL | 43 (P1.11) | 43 |
| 8 (D7) | SSD1306 OLED - I2C SDA | 44 (P1.12) | 44 |
| 9 (D8) | EBYTE E22 - SPI SCK | 45 (P1.13) | 7 |
| 10 (D9) | EBYTE E22 - SPI MISO | 46 (P1.14) | 8 |
| 11 (D10) | EBYTE E22 - SPI MOSI | 47 (P1.15) | 9 |
| 12 | SSD1306 OLED - 3.3V | 3V3 | 3V3 |
| 13 | GND | GND | GND |
| 14 | NC | 5V | 5V |

## Battery

Powered by, and charges, a single 4.2V Lithium-ion battery, with the option of:

* 21700 battery (holder: [BeilaMoo PA21700*1-SMT](https://www.beilamoo.com/sdm/1074412/4/pd-5180803/21061576-2986071/ONE_21700_Battery_Holder_with_Surface_Mount_SMT.html)/[MYOUNG BH-21700-B1BJ001](https://jlcpcb.com/partdetail/Myoung-BH_21700B1BJ001/C20606791))
* LiPo pouch cell (connector: Molex PicoBlade 1X02P, P=1.25mm)

Do not connect a 21700 battery and LiPo battery simultaneously, there is no protection and the batteries will be shorted together in parallel.

### Charging

Solder a 2-circuit Molex PicoBlade (1.25mm pitch) pigtail to the back of the XIAO module, then plug it into the XIAO connector on the PCB, ensuring correct polarity.

In my previous design, the [Ikoka Nano](https://github.com/ndoo/ikoka-nano-meshtastic-device), I used a plated through-hole pad to solder through to the XIAO-nRF52840's SMD battery pad. However, because the solder joint cannot be inspected, it is hard to tell if the soldered connection was successful or reliably, or worse yet, if the battery pads are shorted together.

I toyed with the idea of doing an internal castellated via in a cutout (similar to modchips), but I decided it was more reliable to make the XIAO module socketable, and solder a Molex PicoBlade 1.25mm pigtail to the XIAO module in order to plug the battery connection into the Ikoka Stick board.

This avoids wasting the charging circuit on the XIAO board, while also making use of the many 1.25mm battery wires I have leftover from Heltec purchases.

## Meshtastic Compatibility

The XIAO module is intended to be socketed with pin headers/pin sockets, to allow swapping out modules depending on what features are needed (Bluetooth, Wi-Fi, different power consumption profiles, etc.); Compatibility with official Meshtastic firmware depends on the inserted XIAO board.

### XIAO-nRF52840

* EBYTE E22 LoRa
  * LoRa pins are identical to the officially-supported [Seeed Xiao NRF52840 Kit](https://www.seeedstudio.com/XIAO-nRF52840-Wio-SX1262-Kit-for-Meshtastic-p-6400.html) on [Meshtastic Web Flasher](https://flasher.meshtastic.org/)
  * LoRa will work out of the box on officially-supported firmware
  * Special consideration must be taken if using the E22-900M33S module
    * Set the transmit power to ≤ 9 dBm on first use (when setting the LoRa region)
    * **Transmit power must never be set greater than 9 dBm** to avoid damaging the module's RF frontend
* SSD1306 OLED I2C
  * Pin D6/P1.11 and D7/P1.12 are [reserved for the L76K GPS module in the officially-supported variant](https://github.com/meshtastic/firmware/blob/152b8b1b0235bc461c6e4451fbcdac0987b8bf90/variants/seeed_xiao_nrf52840_kit/variant.h#L137-L138)
  * A custom firmware must be built to define these pins as I2C (TODO)
* User button
  * Pin D0/P0.02 is [reserved for the L76K GPS module in the officially supported variant](https://github.com/meshtastic/firmware/blob/152b8b1b0235bc461c6e4451fbcdac0987b8bf90/variants/seeed_xiao_nrf52840_kit/variant.h#L144)
  * A custom firmware must be built to define this pin as the user button (TODO)

### XIAO-ESP32-S3

* Pin definitions are different from the officially-supported [Seeed Xiao ESP32-S3 Kit](https://www.seeedstudio.com/Wio-SX1262-with-XIAO-ESP32S3-p-5982.html)
  * This is because Seeed uses GPIOs on the 30-pin board-to-board press-fit connector instead of the standard XIAO pins
  * A custom firmware must be built (TODO)

### Images
![top](https://ndoo.github.io/ikoka-stick-meshtastic-device/top.png)
![bottom](https://ndoo.github.io/ikoka-stick-meshtastic-device/bottom.png)
![animation](https://ndoo.github.io/ikoka-stick-meshtastic-device/rotating.gif)
rendered with [kicad-render](https://github.com/linalinn/kicad-render)