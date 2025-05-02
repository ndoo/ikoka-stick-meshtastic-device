# Ikoka Stick Meshtastic Device

## Pin Definitions

| XIAO Pin | Function | XIAO-nRF52840 | XIAO-ESP32-S3 |
|---|---|---|---|
| 1 | User button | 2 (P0.02) | 1 |
| 2 | EBYTE E22 DIO1 | 3 (P0.03) | 2 |
| 3 | EBYTE E22 RST | 28 (P0.28) | 3 |
| 4 | EBYTE E22 BUSY | 29 (P0.29) | 4 |
| 5 | EBYTE E22 SPI NSS | 4 (P0.04) | 5 |
| 6 | EBYTE E22 RXEN | 5 (P0.05) | 6 |
| 7 | OLED SSD1306 I2C SCL | 43 (P1.11) | 43 |
| 8 | OLED SSD1306 I2C SDA | 44 (P1.12) | 44 |
| 9 | EBYTE E22 SPI SCK | 45 (P1.13) | 7 |
| 10 | EBYTE E22 SPI MISO | 46 (P1.14) | 8 |
| 11 | EBYTE E22 SPI MOSI | 47 (P1.15) | 9 |
| 12 | OLED SSD1306 3.3V | 3V3 | 3V3 |
| 13 | GND | GND | GND |
| 14 | NC | 5V | 5V |

## Meshtastic Compatibility

Compatibility depends on the inserted XIAO board.

### XIAO-nRF52840

* Pin definitions are identical to the officially-supported [Seeed Xiao NRF52840 Kit](https://www.seeedstudio.com/XIAO-nRF52840-Wio-SX1262-Kit-for-Meshtastic-p-6400.html) on [Meshtastic Web Flasher](https://flasher.meshtastic.org/)
* Special considerations must be taken if using the E22-900M33S module
  * **Transmit power must never be set greater than 9 dBm** or the module's RF frontend will be damaged
  * Make sure you set the transmit power at or below 9 dBm **before** setting the LoRa region (which enables transmission)

### XIAO-ESP32-S3

* Pin definitions are different from the officially-supported [Seeed Xiao ESP32-S3 Kit](https://www.seeedstudio.com/Wio-SX1262-with-XIAO-ESP32S3-p-5982.html)
  * This is because Seeed uses GPIOs on the 30-pin board-to-board press-fit connector instead of the standard XIAO pins
  * A custom firmware must be built (TODO)

### Images
![top](https://ndoo.github.io/ikoka-stick-meshtastic-device/top.png)
![bottom](https://ndoo.github.io/ikoka-stick-meshtastic-device/bottom.png)
![animation](https://ndoo.github.io/ikoka-stick-meshtastic-device/rotating.gif)
rendered with [kicad-render](https://github.com/linalinn/kicad-render)