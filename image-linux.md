# Install Linux images on MicroSD cards

To install a Linux image on a MicroSD card, follow the seteps:
1. Download the Linux image
2. On a Linux machine, use GParted to format the SD card (`Device > Create Partition Table`) and add a FAT32 partition (`Partition > New`). Or use `mkfs` in a terminal prompt by:

```bash
df ## to find SD card filesystem (e.g./dev/sdb)
sudo umount /dev/sdb ## unmount the SD card
sudo mkfs.vfat /dev/sdb ## format drive with the FAT32 file system format
sudo fatlabel /dev/sdb <label> ## add label

# To re-mount the drive:
sudo mount <filesystem> <mount on> ## e.g. /dev/sdb /media/$USER 
```

For another method, we can use `diskutil` tool in a terminal by:

```bash
diskutil eraseDisk FORMAT NEW_NAME /MOUNT_POINT
# Note: FORMAT and NAME should be capital

# Example
diskutil eraseDisk FAT32 RETROPEI /dev/disk2

# To find mount point:
diskutil list

# To unmount:
diskutil unmountDisk /MOUNT_POINT
```

3. Use `dd` command to convert and copy of the Linux image to the SD card by:

```bash
dd if=<image path> of=<SD path>

## Example
dd if=/home/retropie-4.5.1-rpi2_rpi3.img of=/dev/sdb bs=4M status=progress
```

**Notes:**
- [Etcher](https://www.balena.io/etcher/) is a very useful tool to flash OS images to SD cards & USB drives
- Use `-n` flag to add lables when formating a partion for example `sudo mkfs.vfat -n 'label' /dev/sdb` 
- To format a SD card to NTFS, use `sudo mkfs.ntfs /dev/sdb`
