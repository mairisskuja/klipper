# Klipper + Fluidd setup guide for hopeless dummies (like myself)

`// Work in progress //`

1. Start with downloading a pi image with Klipper, Moonraker and Fluidd pre-installed.

* Go to the FluidPi repo and download latest version which contains the necessary code to generate the distribution from an existing Raspbian lite distro image.
Download latest version of FluidPi: https://github.com/fluidd-core/FluiddPI/releases/latest

`Read first (not mandatory but might be useful): https://github.com/fluidd-core/FluiddPI`

2. Prepare Micro SD card

* Choose Micro SD card with reasonable size as later you will use it not only as "disk" where your Klipper, Moonraker and Fluidd runs but as 'virtual CD card' as well replacing your SD card slot on Control Board.*

`SD card minimum size can be 4Gb, 16 - 64Gb is recommended as you will later store print files on this card. Never cheap out on build parts, that includes quality SD card as well.`

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
  * If you can not access using local domain name — use local IP address of your pi connected tp WiFi instead. There are multiple ways how to understand which address is set for pi via Dynamic Host Configuration Protocol (DHCP). The easiest way would be to connect tp your WiFi roter and look into device list in your WiFi network.
  * It's not a bad idea to set Static DHCP lease for pi running Fluidd. This is supported my most modern WiFi routers. Info though how to achieve this very depends on a specific router and it's integrated software. 

`If everything is OK, you will see Fluidd UI with error message — 'Unable to open config file /home/pi/klipper_config/printer.cfg' which is as expected.`

6. Update Fluidd

* Go to Settings / General, find Software Updates panel and update all what allows you to do so.

7. Building and flashing the micro-controller Unit (MCU)

* Connect Raspberry Pi to printer Main Board and boot up.

* Launch any terminal software of your choice and connect to your Rpi using SSH.
  * For Win, download Putty (https://www.putty.org/)
  * For Mac launch Terminal.
 
`Connection commands wil be as such:

shh -l pi fluidd.local (or something like shh -l pi 192.168.1.10 using local IP)
accept key (for the first time)
login using password you set in step 4.`

* When you are connected to pi console, use the followimng coomands:

To compile the micro-controller code, start by running these commands on the Raspberry Pi:

`~/cd/klipper
make menuconfig
`

If you have the following (or similar) error message:

`locale.Error: unsupported locale setting
make: *** [Makefile:112: menuconfig] Error 1`

Run the following command:

`export LC_ALL=en_GB.UTF-8
make menuconfig`

If all is ok you should see Klipper Firmware Configuration UI which looks like this: https://cln.sh/P088ts

* Select the appropriate micro-controller and review any other options provided.
 
* This part is tricky one and is not device afnostic. The configuration below is for BTT SKR E3 V1.2 and 2.0.
  * Set **STM32F103** with a **28KiB bootloader** and **USB communication**.
  * Also,select **Enable extra low-level configuration options**" and configure **GPIO pins to set at micro-controller startup** to **!PC13**.

* Once configured, run:

`make`

If MCU firmware compiled correctly you should see klipper.bin in /klipper/out

8. Flashing MCU via SD card

For this step you will need another SD card (1Gb or even smaller will be more than enough).

* Open or Download and install file manager able to connect to remote host via SFTP

Win: Download or use any SFTP software of your choice. i.e. - WinSCP (https://winscp.net/
Mac: Download or use any SFTP software of your choice. i.e. https://filezilla-project.org/

* Connect using the same access credentials you are used for accessing pi via Terminal.

* Copy /klipper/out/klipper.bin file to SD card.

* Rename file on SD to 'firmware.bin'.

`You are ready to flash MCU at this point.`

* Remove SD card from computer, shut down pi (this is not necessary if pi is not connected to printer PSU or separate PSU (i.e Mean Well RS-25-5 PSU) connected to printer Main switch), shut down printer, insert SD card in respective MCU's SD card slot and switch printer on.

`If you are able to see MCU card you should see 'Status' diode flashing rapildy and then stop. Usually the while process takes seconds.
`
`You can check IF firmeare is actially flashed by removing SD card from printer and view it's contents via computer. If flash was successful file is renamed to 'firmware.cur'
`

--- to be continued ----
