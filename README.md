# Tasmota-VINDSTYRKA
Integration to Tasmota and VINDSTYRKA

I recently picked up two of the IKEA VINDSTYRKA for use in my home...
So, obviously, I wanted to integrate the devices into my home monitoring system.

Searching the web, I found a references on disassembling the VINDSTYRKA, inside was a Sensirion SEN54 sensor
and a circuit board with an LCD controller chip and a Silicon Lab MGM210L22F ZigBee chip.

The first place to look for help was in Tasmota, and yes a driver was available for the SEN54 sensor used in the VINDSTYRKA

The SEN54 was connected via I2C to the ZigBee CPU chip. Also noted on the board were pads for 3.3v, GND, SCL, and SDA
So I soldered one end of an Adafruit QT (JST-SH) cable to the board and then to a mini Adafruit QT ESP32.
(The Adafruit device was selected over the SEEED XIAO version, as it has an internal antenna and buttons for booting)

Loaded the development version 13.1.0.2 Tasmota to the ESP32 via web installer, set the SDA pin to 22, and SCL to 19,
Rebooted and Tasmota was reading sensor values from the VINDSTYRKA. But there was an issue, Two Master and one slave
on I2C has issues in many case, and we were now getting erratic reading on the display from time to time...

Search the Tasmota source code, I found a reference to Option156, which put the SEN54 drive​r in ​I2C listen​ mode.
I open the Tasmota console, and set Option156 1, to enable.

Issues resolved.

Some photos of my installation are included here for reference.

Reference:


~~~
https://www.ikea.com/us/en/p/vindstyrka-air-quality-sensor-smart-30498239/
https://hackaday.com/tag/vindstyrka/
https://www.sensirion.com/products/catalog/SEN54
https://www.silabs.com/wireless/zigbee/efr32mg21-series-2-modules/device.mgm210la22jnf?tab=specs
https://www.adafruit.com/product/4210
https://www.adafruit.com/product/5395
https://tasmota.github.io/install/
~~~
