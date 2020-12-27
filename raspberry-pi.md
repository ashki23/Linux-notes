## Raspberry Pi

There is a great instruction at [Raspberry project](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up) 
website to help you to set up your Pi. As a quick reference to set up your Raspberry Pi you need:

- 8GB (or more) micro SD card
- USB mouse/keyboard
- HDMI monitor (your TV or computer monitor)
- +5V ~ 2.5A mini USB power supply (a suitable iPad/Android charger will do)

First, we need to write [Raspberry Pi OS](https://www.raspberrypi.org/downloads/) image to the SD card. Use Raspberry Pi Imager for an easy way to install Raspberry Pi OS to an SD card. See [here](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/2) for more details.

When SD card, mouse and HDMI cable are attached, we are ready to start. Turn on your Pi by attaching the mini USB charger. Then select the image and press install. It takes about 10 minuts to install Raspberry Pi OS (with desktop). Then finish the setup by selecting language and time zone, setting password, connecting to WiFi and updating software. 

To change the configuration from terminal, run `sudo raspi-config`: (Note: make all the following changes together and then reboot your Pi once)

- Full screen view: `Display Options > Undderscan: No` 
- Adjust the resolution: `Display Options > Resolution: Selece your display resolution`
- Enable SSH:  `Interface Options > SHH: Enable`
- Enable VNC: `Interface Options > VNC: Enable`
- Timezone/WLAN Country: `Localisation Options > Timezone/WLAN Country`
- WIFI network: `System Options > Wireless LAN`

After rebooting, we can easily connect to the Rasberry Pi through SSH or VNC using the IP address. To find the local IP address, run `hostname -I` on terminal or open the VNC Server from the Menu Bar. Now, we can detach monitor and mouse from Pi and use a desktop or laptop to concent Pi remotely.

To connect Pi through SSH open terminal in your computer and run `ssh pi@ip_address` or `ssh pi@raspberrypi.local`. To connect through VNC open [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/) on your computer and insert the IP address. To learn more check [establishing a direct connection](https://www.realvnc.com/en/connect/docs/raspberry-pi.html#raspberry-pi-connect-direct) and a [cloud connection](https://www.realvnc.com/en/connect/docs/raspberry-pi.html#raspberry-pi-connect-cloud) for VNC Connect.

If you are looking for booting a desktop Pi directly to the command-line, open `Main menu > Preferences > Raspberry Pi Configuration > System` and select Boot to CLI option. After rebooting Pi directly goes to the command-line mode. To go to the desktop mode run `startx`. 

---
Copyright 2018-2019, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
