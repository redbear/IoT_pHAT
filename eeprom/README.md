# IoT pHAT


## EEPROM
<<<<<<< HEAD
=======

### Version

* Current version is 0.4

* Fixed the "Kernel Panic" issue when using command "poweroff" or "halt".
 
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
