# Make a bootable Windows 10 USB
To create a Windows bootable USB follow the seteps in here. Very briefly:
1. Download [Windows 10 image](https://www.microsoft.com/en-us/software-download/windows10ISO)
2. Use GParted to format the USB and create **two** partitions, one that is FAT32 (64 MB) and will hold an EFI bootloader and the other is NTFS (>6 GB) and holds Windows installation files
3. Open Windows 10 `ios` file with `Disk Image Mounter` and copy all files into the NTFS partiotion
4. Download [uefi-ntfs.img](https://github.com/pbatard/rufus/tree/master/res/uefi) deriver
5. Open `img` file with `Disk Image Mounter` and copy entire **EFI** folder to the FAT32 partition to make the USB bootable 

Also, we can use WoeUSB to creat Windows images. Use the following to install it: 
```bash
sudo add-apt-repository ppa:nilarimogard/webupd8
sudo apt update
sudo apt install woeusb
``` 

**Note:** on HP laptops you might need to enable `legacy support` in `Boot Options` under `System Configuration` in Boot Option Menu. To access to the Boot Option Menu restart the computer and press `Ecs` untill the boot menu shows up. Also, you might change the GRUB menu in your linux computer to access boot menu at boot-time. To do that, open `/etc/default/grub` file and change `GRUB_TIMEOUT` from 0 seconds to 5 seconds. Save changes and `run sudo update-grub` to apply changes. 
