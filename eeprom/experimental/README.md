# IoT pHAT


## EEPROM

### Version

* v0.4

	- This version fixes a issue that RPi shutdown will cause kernel panic.
* v0.3

	- This version makes use the UART0 on GPIO 14 and 15 for the Bluetooth, but need to add `init_uart_clock=48000000` to the end of the `/boot/config.txt` file. This seems more stable than using UART1. We are also asking the RPi team if we can automate this part. Also, this reduce the SDIO clock for WiFi from 40 MHz to 20 MHz to make it more stable.
	
	- With this, you do not need to modify the script file from,
	
		 `$ nano /lib/systemd/system/hciuart.service`
	
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

	- Modify the file to set UART clock,
	
		`$ sudo nano /boot/config.txt`
		
		Add to the end,
		
		`init_uart_clock=48000000`

### Prerequisites

* Add `dtparam=i2c_vc=on` to the `/boot/config.txt` file, this will enable the system to access to the I2C EEPROM, and then `reboot` your RPi.

	The steps:
	- $ sudo nano /boot/config.txt
	- add dtparam=i2c_vc=on to the end
	- $ sudo reboot
	
* Download the EEPROM and script files (do this inside your RPi if you have WiFi connected already),

	`$ wget https://raw.githubusercontent.com/redbear/IoT_pHAT/master/eeprom/experimental/v0.4/IoT_pHAT-with-dt.eep`

	`$ wget https://raw.githubusercontent.com/redbear/IoT_pHAT/master/eeprom/experimental/v0.4/eepflash.sh`

* Change the flash tool mode to executable,

	`$ chmod +x eepflash.sh`

### If you just want to write the compiled configuration file

* Step 1 - Use this command to burn, answer `yes`:

	`$ sudo ./eepflash.sh -f=IoT_pHAT-with-dt.eep -t=24c32 -w`

* Step 2 - Reboot

	`$ sudo reboot`

### If you want to compile the configuration file yourself

* Step 1 - Compile the DTS file:

	`$ sudo dtc -@ -I dts -O dtb -o IoT_pHAT.dtb IoT_pHAT.dts ; sudo chown pi:pi IoT_pHAT.dtb`

* Step 2 - Combine the settings to the DTB:

	`./eepmake eeprom_settings.txt IoT_pHAT-with-dt.eep IoT_pHAT.dtb`

* Step 3 - Writing to the EEPROM:

	`$ sudo ./eepflash.sh -f=IoT_pHAT-with-dt.eep -t=24c32 -w`

* Step 4 - Reboot

	`$ sudo reboot`


### Note

* After all operations, remember to remove the line (`dtparam=i2c_vc=on`) in the /boot/config.txt file, otherwise, it will affect you to use the camera module.


## Reference

* Sense HAT

	https://www.raspberrypi.org/documentation/hardware/sense-hat/

* Howto: Raspi HAT EEPROM and device-tree

	https://www.raspberrypi.org/forums/viewtopic.php?f=29&t=108134
