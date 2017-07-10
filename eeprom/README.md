# IoT pHAT


## EEPROM

### Version

* Current version is 0.5 (updated for NOOBS 2.4.1)

* v0.5

	- This version fixes an issue that Bluetooth does not work with 21-06-2017 version of Raspbian that is installed by NOOBS v2.4.1.
 
### If you just want to write the compiled configuration file

* Change the current path to eeprom/bin first.

* Use this command:

	`$ sudo ./eepflash.sh -f=IoT_pHAT-with-dt.eep -t=24c32 -w`

### If you want to compile the configuration file yourself

* Change the current path to eeprom/src first.

* Step 1 - Compile the DTS:

	`$ sudo dtc -@ -I dts -O dtb -o IoT_pHAT.dtb IoT_pHAT.dts ; sudo chown pi:pi IoT_pHAT.dtb`

* Step 2 - Combine the settings to the DTB:

	`./eepmake eeprom_settings.txt IoT_pHAT-with-dt.eep IoT_pHAT.dtb`

* Step 3 - Writing to the EEPROM:

	`$ sudo ./eepflash.sh -f=IoT_pHAT-with-dt.eep -t=24c32 -w`


## Reference

* Sense HAT

	https://www.raspberrypi.org/documentation/hardware/sense-hat/

* Howto: Raspi HAT EEPROM and device-tree

	https://www.raspberrypi.org/forums/viewtopic.php?f=29&t=108134
