# IoT pHAT


## EEPROM (Experimental)

### Version

* v0.3

	- This version makes use the UART0 on GPIO 14 and 15 for the Bluetooth, but need to add `init_uart_clock=48000000` to the end of the `/boot/config.txt` file. This seems more stable than using UART1. We are also asking the RPi team if we can automate this part.
	
	- With this, you do not need to modify the script file from `/lib/systemd/system/hciuart.service`
	
		The original:
		
		```
		[Unit]
		Description=Configure Bluetooth Modems connected by UART
		ConditionPathIsDirectory=/proc/device-tree/soc/gpio@7e200000/bt_pins
		Before=bluetooth.service
		After=dev-serial1.device
	
		[Service]
		Type=forking
		ExecStart=/usr/bin/hciattach /dev/serial1 bcm43xx 921600 noflow -
	
		[Install]
		WantedBy=multi-user.target		
		```

### Prerequisites

* Add `dtparam=i2c_vc=on` to the /boot/config.txt file, this will enable the system to access to the I2C EEPROM, and then `reboot` your RPi.

* After all operations, remove that line, otherwise, it will affect you to use the camera module.
 
### If you just want to write the compiled configuration file

* Use this command:

	`$ sudo ./eepflash.sh -f=IoT_pHAT-with-dt.eep -t=24c32 -w`

### If you want to compile the configuration file yourself

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
