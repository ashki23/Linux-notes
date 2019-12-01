# Make a bootable Windows USB
To create a Windows bootable USB follow the seteps in [here](https://www.onetransistor.eu/2014/09/make-bootable-windows-usb-from-ubuntu.html?m=1). 
Very briefly:
1. Download [Windows 10 image](https://www.microsoft.com/en-us/software-download/windows10ISO)
2. Use GParted to format the USB and create a NTFS partition (remember the `drive-lable`)
3. Open Windows 10 `ios` file with `Disck Image Mounter` and copy all files into the USB
4. Install `grub-pc-bin` package with:
```bash
sudo apt install grub-pc-bin
grub-install
```
5. Use the following to make the USB bootable:
```bash
sudo grub-install --target=i386-pc --boot-directory="/media/<username>/<drive_label>/boot" /dev/<sdX>
```
Update `username`, `drive_lable` and USB drive name (e.g. `/dev/sdb`).

6. Create `boot/gru/grub.cfg` file including:
```bash
default=1  
timeout=15
color_normal=light-cyan/dark-gray
menu_color_normal=black/light-cyan
menu_color_highlight=white/black
 
menuentry "Start Windows Installation" {
    insmod ntfs
    insmod search_label
    search --no-floppy --set=root --label <drive_label> --hint hd0,msdos1
    ntldr /bootmgr
    boot
}

menuentry "Boot from the first hard drive" {
    insmod ntfs
    insmod chain
    insmod part_msdos
    insmod part_gpt
    set root=(hd1)
    chainloader +1
    boot
}
```
Update `drive-lable`.
