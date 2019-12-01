# Make a bootable Windows 10 USB
To create a Windows bootable USB follow the seteps in [here](https://www.onetransistor.eu/2015/09/uefi-ntfs-bootable-windows-usb-linux.html). 
Very briefly:
1. Download [Windows 10 image](https://www.microsoft.com/en-us/software-download/windows10ISO)
2. Use GParted to format the USB and create **two** partitions,  one that is FAT32 (64 MB) and will hold an EFI bootloader and the other is NTFS (>6 GB) and holds Windows installation files 
3. Open Windows 10 `ios` file with `Disk Image Mounter` and copy all files into the NTFS partiotion
4. Download [uefi-ntfs.img](https://github.com/pbatard/rufus/tree/master/res/uefi) deriver
5. Open `img` file with `Disk Image Mounter` and copy entire **EFI** folder to the FAT32 partition to make the USB bootable  
