## Backlight problem

One day, your laptop keyboard decides to not change the backlight of your screen! What we can do? On Linux`xbackligh` let us 
change the brigness of the screen through terminal. On a Debian based distro, use the following to install `xbackligh`:

```bash
sudo apt install xblacklight
```

To chnge the brihtness use:

```bash
xbacklight = <a number 1-100> # To set a value
xbacklight + <a number 1-100> # To increase
xbacklight - <a number 1-100> # To decrease
```
If you got "No outputs have backlight property" error, then you should crate a link to the deriver to solve the issue. 
First let's find the actual location of "intel_backlight":

```bash
sudo find /sys/ -type d -iname 'intel_backlight'
```
That should be look like `/sys/devices/pci0000:00/0000:00:02.0/drm/card0/card0-LVDS-1/intel_backlight`. Note that if the above 
command returned nothing, you might not have an Intel graphic device, let's try `find /sys/ -type f -iname '*brightness*'`.

Now, let's make a link by:

```bash
sudo ln -s /sys/devices/pci0000:00/0000:00:02.0/drm/card0/card0-LVDS-1/intel_backlight /sys/class/backlight
```

Close the thermnal and logout your computer and login again. Now, try `xbacklight = 20` to see the issue is solved or not. 
If not then you need to add a config file. Use `sudo nano /etc/X11/xorg.conf` to make the file and insert:

```bash
  Section "Device"
        Identifier  "Intel Graphics" 
        Driver      "intel"
        Option      "Backlight"  "intel_backlight"
    EndSection
 ```
 
 Note that if you could not find the "intel_backligh" directory before, change "intel_backlight" to the directory of your 
 backlight settings.
 
 Now, again close the terminal, logout and login, and try `xbacklight = 20`. It should work! Know that these changes are 
 temprary and the screen brightness will back to the default level after robooting. 
 
 
