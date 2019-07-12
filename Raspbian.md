## Raspberry Pi

There is a great instruction at [Raspberry project](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up) 
website to help you to set up your Pi. As a quick reference to set up your Raspberry Pi you need:
- 8GB (or more) micro SD card
- USB mouse
- HDMI monitor (your TV or computer monitor)
- +5V ~ 2.5A mini USB power supply (a suitable iPad/Android charger will do)

Before start you need to download [NOOBS](https://www.raspberrypi.org/downloads/) and unzip the downloaded file and paste in 
your micro SD card (make sure SD card is formated to FAT 32). Please see [here](https://projects.raspberrypi.org/en/projects/raspberry-pi-setting-up/3) 
for more details.

When you attached SD card, mouse and HDMI cable your system is ready. To turn on your Pi just attach the mini USB charger. 
Then select the NOOBS image and press install. It takes about 10 minuts to install the Raspbian. Then finish the setup by 
selecting language and time zone, setting password, connecting to WiFi and updating software. 

To change some configuration go `Main menu > Preferences > Raspberry Pi Configuration`: (Note: made all the following changes 
together and then reboot your Pi once)   
- Full screen view: `System > Overscan: Disable` 
- Adjust the resolution: `System > Resolution: Selece your display resolution`
- Enable SSH:  `Interfaces > SHH: Enable` 
- Enable VNC: `Interfaces > VNC: Enable`

After rebooting you can easily connect to your Rasberry Pi through SSH or VNC. To find the IP address, open the VNC Server 
from the Menu Bar. Now, you may detach monitor and mouse from your Pi and use your desktop or laptop to concent to your Pi.

To connect Pi through SSH open a terminal prompt in your computer and run `ssh pi@ip_address`. To connect through VNC open 
[VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/) on your computer and insert the IP address 
that you can find on the VNC Server main page. To learn more check [establishing a direct connection](https://www.realvnc.com/en/connect/docs/raspberry-pi.html#raspberry-pi-connect-direct)
and a [cloud connection](https://www.realvnc.com/en/connect/docs/raspberry-pi.html#raspberry-pi-connect-cloud) for VNC Connect.

Last configuration that you might need is changing the defualt console size which is more important if you are looking for 
connecting Pi through VNC. For doing that open a terminal command prompt on your Raspberry Pi and run `sudo raspi-config`, 
navigate to Advanced Options > Resolution and choose an option (as an alternative way you can use `sudo nano /boot/config.txt` 
to open `config.txt` file and uncomment framebuffer width and height to force a console size). For a regular Full HD displays 
set the width and height values for 1920 and 1080.
