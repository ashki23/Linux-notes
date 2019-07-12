## Finding inserted SD card

If your device could not recognize the SD card you can try terminal to find what you can do for the poor SD 
card! The following commands show some information about the inserted SD card:
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
By these command you could find name and directory of the SD card and try to mount it. But if the card still is unknown then 
your card might be dead. Check all errorsin the `dmseg` command output to find more information. 

## Formating 
If you have a SD card that your device could recognize it, then you can use the following commnands to format the card:
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

You can find the SD card or USB drive path `lsblk` or `lsudb.
