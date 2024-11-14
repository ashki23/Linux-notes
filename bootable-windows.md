# Make a bootable Windows 10 USB

To create a Windows bootable USB, follow the seteps:
1. Download [Windows 10 image](https://www.microsoft.com/en-us/software-download/windows10ISO)
2. Use GParted to format the USB (`Device > Create Partition Table`) and add a NTFS partition (`Partition > New`) 
3. Install WoeUSB by: 
```bash
sudo add-apt-repository ppa:nilarimogard/webupd8
sudo apt update
sudo apt install woeusb
```
4. Open WoeUSB and copy the Windows image to the USB drive  

**Note:** if you access to a Windows PC, you can use [Rufus](https://rufus.ie/) to creat the bootable USB.

**HP users:** On HP laptops you need to enable `legacy support` in `Boot Options` under `System Configuration`. To access to the Boot Option Menu restart the computer and press `Ecs` untill the boot menu shows up.

**GRUB:** You can change the GRUB settings in your Linux computer to access boot menu at the boot-time. To do that, open `/etc/default/grub` file and change `GRUB_TIMEOUT` from 0 seconds to 5 seconds. Save changes and `run sudo update-grub` to apply changes.
