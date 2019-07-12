## Enable tapping on touchpad
Source: [Wiki debian](https://wiki.debian.org/SynapticsTouchpad)

Sometime you could not enable tapping on tuchpad through the setting menu. In this case, you can use terminal! Use 
`sudo nano /etc/X11/xorg.conf.d/40-libinput.conf` to open `.conf` file with Nano text editor on your terminal and add 
the following under the `libinput touchpad catchall` identifier.
```bash
`Option "Tapping" "on"` 
```
Save changes (`ctrl + s`) and close (`ctrl + x`) editor and then close the terminal. It should work now!
