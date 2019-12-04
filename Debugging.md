# Debugging
*[Ashkan Mirzaee](https://ashki23.github.io/index.html) - July 2019*

## Changing screen backlight from terminal
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
        Identifier  "Intel Graphics" 
        Driver      "intel"
        Option      "Backlight"  "intel_backlight"
    EndSection
 ```
 
Note that if you could not find the "intel_backligh" directory before, change "intel_backlight" to the directory of your  backlight settings.
 
Now, again close the terminal, logout and login, and try `xbacklight = 20`. It should work! Note that changes in backlight level are temprary and the screen backlight will back to the default level after robooting. 
 
## Finding an inserted SD card
If SD card is not recognized by default, we might be able to find it in terminal. The following commands show some information about the inserted SD card:
```bash
lsblk: list block devices
lsblk | grep -v loop: shows only hard/sd/usb drives
lsusb: list USB devices
lspci: list all PCI devices
fdisk: manipulate disk partition table
fdisk -l: shows list of disks
mount/umount: mount/unmount a filesystem
dmseg: display message or driver message
```
By these command we can find name and directory of the SD card and try to mount it. But if the card still is unknown then 
your card might be dead. Check all errors in the `dmseg` command output to find more information. 

## Formating SD cards
To format a SD card, use the following commnands:
```bash
## FAT
sudo mkfs.vfat /dev/device_name

## NTFS
sudo mkfs.ntfs /dev/device_name

## EXT4
sudo mkfs.ext4 /dev/device_name
```
## Flash OS images
[Etcher](https://www.balena.io/etcher/) is a very common and useful tool to fash OS images to SD cards & USB drives. In Unix 
terminal you can use `dd` command to convert and copy a file (image) whithout any extra software. For example: 
```bash
dd if=<image.img path> of=<disk path i.e. /dev/mmcblk0> bs=4M status=progress conv=fsync
```

You can find the SD card or USB drive path `lsblk` or `lsudb`.

## Enable tapping on touchpad
Source: [Wiki debian](https://wiki.debian.org/SynapticsTouchpad)

Sometime we cannot enable tapping on tuchpad through the setting menu. In this case, we can use 
`sudo nano /etc/X11/xorg.conf.d/40-libinput.conf` to open `.conf` file with Nano text editor in terminal and add 
the following under the `libinput touchpad catchall` identifier.
```bash
`Option "Tapping" "on"` 
```
Save changes (`ctrl + s`) and close (`ctrl + x`) editor and then close the terminal. It should work now!

## Connect to a WPA/WPA2 Wi-Fi network
Source: [Linux Commando](https://linuxcommando.blogspot.com/2013/10/how-to-connect-to-wpawpa2-wifi-network.html)

*If you have a **Raspberry Pi**, before using the following, open terminal and try `sudo raspi-config`. Select 
`Network Options` and enter network name and passphrase to connect to wifi.*

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

If it returns `Not connected` then go to the next step. For the next step you will need the wirless network's name and 
password. If you do not know the network's name you may run:
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
If the [NetworkManager](https://docs.ubuntu.com/core/en/stacks/network/network-manager/docs/) is installed (run `nmcli -v`) 
then you may follow these steps:

```bash
nmcli d # show the status
nmcli d wifi list $ shows wifi list
nmcli d wifi connect <wifi_name> password <password> # connect the access point
```

---
Copyright 2018-2019, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)
