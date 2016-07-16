# IoT pHAT

RedBear IoT pHAT, designed for the Raspberry Pi Zero.

This is for the hardware version 1.0 only, the EEPROM contains the information for automatically starting the WiFi and other settings.

* Front View

	![image](docs/images/IoT_pHAT_front.png)

* Back View

	![image](docs/images/IoT_pHAT_back.png)


## Block Diagram
	
![image](docs/images/IoT_pHAT_blocks.png)


## Features

* AMPAK AP6212A Wireless Module (Broadcom BCM43438 A1 chip inside)
	- WiFi (802.11bgn / 2.4GHz)
	- Bluetooth (4.1) and BLE support
* Single antenna for concurrent WiFi and Bluetooth operations
	- Onboard PCB antenna
	- External antenna connector
 	- Antenna switch for extenal antenna
* 32 Kbit (4 KByte) EEPROM for DTOverlay configuration
* 40-pin connector
	- WiFi: SDIO v2.0 - up to 50 MHz clock rate
	- Bluetooth: UART (up to 4 Mbps)
* FCC/CE certified


## Pinout

![image](docs/images/IoT_pHAT_40-pin.png)


## Specification

### General

* Model Name			: IoT pHAT
* Product Description	: WiFi and Bluetooth connectivity add-on board for Raspberry Pi Zero
* Dimension				: (TBD)
* WiFi Interface		: SDIO v2.0
* Bluetooth Interface	: UART / PCM
* Operating voltage		: 3.3V
* Operating temperature	: -30˚C to 85˚C
* Storage template		: -40˚C to 85˚C
* Humidity				: Operating Humidity 10% to 95% Non-Condensing

### WiFi

* Data Rate
	- 802.11b: 1, 2, 5.5, 11 Mbps
	- 802.11g: 6, 9, 12, 18, 24, 36, 48, 54 Mbps


## How it works

* (To be written)


## How to play

### Prerequisite

* Raspberry Pi Zero or other model with 40 pin connector header
* SD Card with Raspian installed

### WiFi (Plug & Play)

Stack the IoT pHAT to your Pi Zero, after booting up, the Linux kernel will read the configuration from the onboard EEPROM, it will turn on the WiFi, so you can use the WiFi to connect to your wireless router or access point directly.

### Bluetooth (3 changes required)

1. Edit `/boot/config.txt`, add `init_uart_clock=64000000` to the end
2. Edit `/boot/cmdline.txt`, remove `console=serial0,115200`
3. Edit `/lib/systemd/system/hciuart.service`, change `/dev/serial1` to `/dev/serial0`
4. Reboot the board with `sudo reboot`
5. You will see the Bluetooth is ready to use

*** We are trying to automate the Bluetooth part, too.


## Limitations

* FM is not supported with the board
