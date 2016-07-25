# IoT pHAT


## EEPROM

These are the steps to write the configuration to the EEPROM, change the current path to eeprom/bin first.

Step 1:

sudo dtc -@ -I dts -O dtb -o IoT_pHAT.dtb IoT_pHAT.dts ; sudo chown pi:pi IoT_pHAT.dtb

Step 2:

./eepmake eeprom_settings.txt IoT_pHAT-with-dt.eep IoT_pHAT.dtb

Step 3:

sudo ./eepflash.sh -f=IoT_pHAT-with-dt.eep -t=24c32 -w


## Reference

* Sense HAT

	https://www.raspberrypi.org/documentation/hardware/sense-hat/

* Howto: Raspi HAT EEPROM and device-tree

	https://www.raspberrypi.org/forums/viewtopic.php?f=29&t=108134
