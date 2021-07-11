# Debugging

## Change screen backlight
We can use `xbackligh` package to change brightness of the screen through terminal. On a Debian based distro, use the following to install `xbackligh`:

```bash
sudo apt install xblacklight
```

To change backlight use:
```bash
xbacklight = <a number 1-100> # To set a value
xbacklight + <a number 1-100> # To increase
xbacklight - <a number 1-100> # To decrease
```

If you receive `No outputs have backlight property` error, then create a link to the driver to solve the issue. First, find the actual location of `intel_backlight` by:
```bash
sudo find /sys/ -type d -iname 'intel_backlight'
```
That should be look like `/sys/devices/pci0000:00/0000:00:02.0/drm/card0/card0-LVDS-1/intel_backlight`. Note that if the above command returned nothing, you might not have an Intel graphic device. Then try `find /sys/ -type f -iname '*brightness*'` instead of above command.

Now, create a link by:
```bash
sudo ln -s /sys/devices/pci0000:00/0000:00:02.0/drm/card0/card0-LVDS-1/intel_backlight /sys/class/backlight
```

Close the terminal and logout the computer and login again. Now, try `xbacklight = 20` to see the issue is solved or not. If not then we need to add a config file. To create the config file, use `sudo nano /etc/X11/xorg.conf` and insert:
```bash
  Section "Device"
          Identifier "Intel Graphics" 
          Driver "intel"
          Option "Backlight" "intel_backlight"
  EndSection
 ```
 
Note that if you could not find the "intel_backligh" directory before, change "intel_backlight" to the directory of your  backlight settings.
 
Now, again close the terminal, logout and login, and try `xbacklight = 20`. It should work! Note that changes in backlight level are temprary and the screen backlight will back to the default level after robooting. 
 
## Find an inserted SD card
If SD card is not recognized by default, we might be able to find it in terminal. The following commands show information about the inserted SD card:
```bash
df: report file system disk space usage
lsblk: list block devices
lsblk | grep -v loop: shows only hard/sd/usb drives
lsusb: list USB devices
lspci: list all PCI devices
fdisk: manipulate disk partition table
fdisk -l: shows list of disks
```
Use the following to unmount and eject SD cards:
```
mount/umount <path>: mount/unmount a filesystem
eject <path>: eject the SD card
```
By these command we can find name and directory of the SD card and try to mount it. But if the card still is unknown then your card might be dead. Check all errors in the `dmseg` command output to find more information. 

## Enable tapping on touchpad
Source: [Wiki debian](https://wiki.debian.org/SynapticsTouchpad)

Sometime we cannot enable tapping on tuchpad through the setting menu. In this case, we can use `sudo nano /etc/X11/xorg.conf.d/40-libinput.conf` to create the following file with Nano text editor - note that you should create the `/etc/X11/xorg.conf.d/` if it is not exist:

```bash
Section "InputClass"
        Identifier "libinput touchpad catchall"
        MatchIsTouchpad "on"
        MatchDevicePath "/dev/input/event*"
        Driver "libinput"
        Option "Tapping" "on"
EndSection 
```
Save changes (`ctrl + s`) and close (`ctrl + x`) editor and then close the terminal. It should work now!

## Connect to a WPA/WPA2 Wi-Fi network
Source: [Linux Commando](https://linuxcommando.blogspot.com/2013/10/how-to-connect-to-wpawpa2-wifi-network.html)

*If you have a **Raspberry Pi**, before using the following, open terminal and try `sudo raspi-config`. Select `Network Options` and enter network name and passphrase to connect to wifi.*

1- Find the wirless network's `Interface` name:
```bash
/sbin/iw dev
```

It is usually `wlan0`.

2- See if the `wlan0` is `UP` or not:
```bash
ip link show wlan0
```

This command will return some info inside the parentheses, if you connot see `UP` there, run the following to set it up.
```bash 
sudo ip link set wlan0 up
```

3- Check the connection status:
```bash
/sbin/iw wlan0 link
```

If it returns `Not connected` then go to the next step. For the next step you will need the wirless network's name and password. If you do not know the network's name you may run:
```bash
wpa_cli
> scan_results
```

To see all available networks and find the right one.

4- Add network's name and password (assume name is `netname` and password is `1234`):
```bash
wpa_passphrase netname >> /etc/wpa_supplicant/wpa_supplicant.conf
# type the password and hit enter
1234
```
5- Connect to the network:

first kill all running wpa instances:
```bash
sudo pkill wpa_supplicant
```

Then run:
```bash
sudo wpa_supplicant -B -D wext -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant.conf
```

Now check the connection again:
```bash
/sbin/iw wlan0 link
``` 
If the [NetworkManager](https://docs.ubuntu.com/core/en/stacks/network/network-manager/docs/) is installed (run `nmcli -v`) then you may follow these steps:

```bash
nmcli d # show the status
nmcli d wifi list $ shows wifi list
nmcli d wifi connect <wifi_name> password <password> # connect the access point
```

## Bluetooth audio
If your bluetooth device is paired but there is no sound from it then it can be fixed by `pavucontrol`. Use the following to install and update the required packages:

```bash
sudo apt update
sudo apt upgrade
sudo apt install pulseaudio pulseaudio-module-bluetooth pavucontrol bluez-firmware
```
Once you have installed these packages, it may be necessary to restart the bluetooth and pulseaudio services:

```bash
killall pulseaudio
service bluetooth restart
```

After that you need to open `pavucontrol` and go to the Configuration and change Profile setting for the Built-in Audio to off.   

## X11 forwarding

I had an issue with X11 forwarding to my MacBook. Issue was solved by editing `/etc/ssh/sshd_config`. You should open the file and uncomment/add the following and edit them such that:

```bash
X11Forwarding yes
X11DisplayOffset 10
XAuthLocation /opt/X11/bin/xauth
```

And then restart SSH by:

```bash
sudo launchctl unload /System/Library/LaunchDaemons/ssh.plist
sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist
```

Note that `XQuartz` should be installed in your Mac. 


## Keyboard delay and repeat speed in Ubuntu 
```bash
gsettings set org.gnome.desktop.peripherals.keyboard delay 250
gsettings set org.gnome.desktop.peripherals.keyboard repeat-interval 30

# To reset  
gsettings reset org.gnome.desktop.peripherals.keyboard delay
gsettings reset org.gnome.desktop.peripherals.keyboard repeat-interval
```
