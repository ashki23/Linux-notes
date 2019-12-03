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

