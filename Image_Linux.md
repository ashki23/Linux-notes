# Install Linux images on MicroSD card
*[Ashkan Mirzaee](https://ashki23.github.io/index.html) - December 2019*

To install a Linux image on a MicroSD card, follow the seteps:
1. Download the Linux image
2. Use GParted to format the SD card (`Device > Create Partition Table`) and add a FAT32 partition (`Partition > New`). Or use `mkfs` in a terminal prompt by:
```
df ## to find SD card path (e.g./dev/sdb)
sudo umount /dev/sdb ## unmount the SD card
sudo mkfs.vfat -n 'linux_image' /dev/sdb ## Format drive with the FAT32 file system format
```

3. Use `dd` command to convert and copy of the Linux image to the SD card by:
```
dd if=<image path> of=<SD path>

## Example
dd if=/home/retropie-4.5.1-rpi2_rpi3.img of=/dev/sdb bs=4M status=progress
```

**Notes:**
- [Etcher](https://www.balena.io/etcher/) is a very common and useful tool to fash OS images to SD cards & USB drives
- To format a SD card to NTFS, use `sudo mkfs.ntfs /dev/sdb`

---
Copyright 2018-2019, [Ashkan Mirzaee](https://ashki23.github.io/index.html) | Content is available under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) | Sourcecode licensed under [GPL-3.0](https://www.gnu.org/licenses/gpl-3.0.en.html)