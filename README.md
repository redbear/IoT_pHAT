# IoT_pHAT

RedBear IoT pHAT, designed for the Raspberry Pi Zero

This is for the hardware version 1.0 only, the EEPROM contains the information for automatically starting the WiFi and other settings.

## Plug & Play (currently for WiFi only)

Stack the IoT pHAT to your Pi Zero, after booting up, the Linu kernel will read the configuration from the onboard EEPROM, it will turn on the WiFi, so you can use the WiFi to connect to your wireless router or access point directly.


## Setup for Bluetooth

1. Edit /boot/config.txt, add init_uart_clock=64000000
2. Edit /boot/cmdline.txt, remove console=serial0,115200
3. Edit /lib/systemd/system/hciuart.service, change /dev/serial1 to /dev/serial0
4. Reboot the board with sudo reboot
5. You will see the Bluetooth is ready to use

* we are trying to automate the Bluetooth part, too.
