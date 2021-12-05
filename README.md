# FluiddPI setup guide for dummies

`// Work in progress //`

1. Start with downloading a pi image with Klipper, Moonraker and Fluidd pre-installed.

* Go to the FluidPi repo and download latest version which contains the necessary code to generate the distribution from an existing Raspbian lite distro image.
Download latest version of FluidPi: https://github.com/fluidd-core/FluiddPI/releases/latest

`Read first (not mandatory but might be useful): https://github.com/fluidd-core/FluiddPI`

2. Prepare Micro SD card

* Choose Micro SD card with reasonable size as later you will use it not only as "disk" where your Klipper, Moonraker and Fluidd runs but as 'virtual CD card' as well replacing your SD card slot on Control Board. 4Gb will be OK-ish.

`I recommend using 8Gb (or more) and choose quality vs price. CD cards have limited time span. Even good ones. Your time on earth is limited as well. It is too short to cheap out on hardware.`

* Format SD card to FAT.

  * OS X: Launch 'Disk Utility', select mounted SD card, click on 'Erase' button and you are good to go.

  * Windows 10: Locate your SD card partition and right-click on it. Choose “Format” from the context menu. Make sure that the “Perform a quick format” option is checked. Choose FAT file system.

  * OtherOS: Most likelly, you do not need this part of the guide if you are running any other OS :)

3. Download Raspberry Pi imager (if you do not have it already)

* Download Raspberry Pi imager it here: https://www.raspberrypi.com/software/

`There are multiple other ways how to install custom pi OS versions on pi, i.e. balenaEtcher (https://www.balena.io/etcher/) and other tools. I recommend to use native Raspberry Pi imager as it allows to pre-configure multiple settings (i.e. WiFi SSID (name) and Password prior to installation start. No need to change config files later - just install, boot and you are ready to go.`

4. Launch Raspberry Pi imager and start installation.

* As Operation System / Choose OS, select 'Use custom' and select latest version of FluidPi (which you downloaded in Step 1). Do not worry .ZIP file is OK, it will work the same way as .IMG file.

`Important: Press ‘Ctrl-Shift-X’ (Win) or ‘CMD-Shift-X’ (OS X) and configure advanced settings.`

* Write in your WiFi access credentials, specify name — i.e. fluidd.local in Advanced settings

* Press 'Write' and wait for disk image writing to complete and verify. That can take some time.

5. Put SD card in Raspberry Pi and boot up for the first time.

`You should see green diode blinking on startup. Proceed to further steps when it stop blinking.`

* Open browser access the name you set in step 4. As most of the modern browsers will force https:// over http:// and you do not have secure connection write in local domain name as http://fluidd.local (or other if you set different).

`If everything is OK, you will see Fluidd UI with error message — 'Unable to open config file /home/pi/klipper_config/printer.cfg' which is as expected.`

6. Update Fluidd

* Go to Settings / General, find Software Updates panel and update all what allows you to do so.

7. Connect Raspberry Pi to printer Main Board.

* _To be continued..._
