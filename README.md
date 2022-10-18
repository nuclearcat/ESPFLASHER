# ESPFLASHER
Inexpensive ESP32/ESP8266 programmer

This device implements a USB programmer for ESP32/ESP8266 devices with traditional programming pin management (EN/BOOT0) using [RTS DTR bridge][1].

It also differs from traditional USB-UART converters by a powerful LDO, which allows you to easily power the ESP32 / ESP8266 and related peripherals.
Design is verified in hardware, the device was ordered from JLCPCB and tested in the real world for programming various devices. (Gerbers, BOM and CPL included)

![image](https://raw.githubusercontent.com/nuclearcat/ESPFLASHER/main/docs/ESPFLASHER.png)

[1]: https://raw.githubusercontent.com/nodemcu/nodemcu-devkit/master/Documents/NODEMCU_DEVKIT_SCH.png "Also called Node-MCU auto-program circuit"
