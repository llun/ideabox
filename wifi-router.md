# Wifi router

After playing with a few routers and got some limitations, now I want a new one myself from the hardware that can
buy from a market which might be more powerful and cheaper. 

## Features

- Support latest wifi technology in the market (Currently is AC) and upgradable.
- Easily upgrade and fix software problem and can ssh in to see logs or configure logs to cloud logs system.
- Have a nice web user interface on both desktop and mobile.
- Reliable wifi with atleast 50 devices.
- Transfer speed as higher as posible.
- Can attach to storage and have file sharing service that can configure in web ui.

## Prototype Hardware specification

- [Intel NUC DN2820FYKH](http://www.amazon.com/gp/product/B00HVKLSVC/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1)
- [Cricial Ram 4GB 1.35V](http://www.amazon.com/gp/product/B005LDLV6S/ref=oh_aui_detailpage_o00_s00?ie=UTF8&psc=1)
- [Intel 520 SSD 120GB](http://www.amazon.com/gp/product/B006VCP7NQ/ref=oh_aui_detailpage_o00_s01?ie=UTF8&psc=1)
- [Linksys AE3000](http://www.amazon.com/Linksys-Dual-Band-Wireless-N-Adapter-AE3000/dp/B007ZLGXA8/ref=sr_1_1?s=electronics&ie=UTF8&qid=1419085435&sr=1-1&keywords=linksys+AE3000) (I choose this adapter because it has 3 MIMO wifi compare to other which normally has only 2 MIMO)
- [Asus AC56](http://www.amazon.com/Asus-USB-AC56-Dual-band-Wireless-AC1200-Adapter/dp/B00FB45USW/ref=sr_1_1?s=electronics&ie=UTF8&qid=1419085558&sr=1-1&keywords=Asus+AC56) 2 MIMO but supports AC

## Prototype Software

- Debian 7 Wheezy with backports kernel
- [Linksys AE3000 custom firmware](https://github.com/RD777/rt3573sta)
- [Asus AC56 custom firmware](https://github.com/abperiasamy/rtl8812AU_8821AU_linux)

## Instructions

- Install Debian and add backports repository to apt source.
- Update all packages and install kernel header and build-essentials tools.
- Add non-free repo to both backports and main apt repository.
- Install intel wifi firmware by apt, `aptitude install -t wheezy-backports firmware-iwlwifi`
- Clone Asus AC56 firmware from github repo above and run `make install` to install the driver.
- Install hostapd, iw and wireless-tools for configuring wifi.
- Set iw country with this command, `iw reg set SG` (In debian jessie, add country code in `/etc/default/crda` for permanent change.)
- Add hostapd configure to `/etc/network/interfaces`, make interface auto start as AP.

```
iface wlan0 inet static
hostapd /etc/hostapd/wlan0.conf
address 192.168.1.1
netmask 255.255.255.0
```

- And hostapd configuration for Asus AC56

```
interface=wlan0
ssid=<your ssid>
driver=nl80211
ieee80211n=1
ht_capab=HT40+
wmm_enabled=1
hw_mode=a
channel=<your channel that's not conflict with other wifi in your house.>
macaddr_acl=0
auth_algs=1
wpa=3
wpa_passphrase=<wifi password>
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
```

- Setup dhcp server and iptable firewall make main connection forward all traffic to this wifi. (can follow the first link in reference section.)

## Reference

- [Using Hostapd with dnsmasq to create Virtual Wifi Access Point in Linux](http://nims11.wordpress.com/2013/05/22/using-hostapd-with-dnsmasq-to-create-virtual-wifi-access-point-in-linux/)
- [Supported wireless driver](http://wireless.kernel.org/en/users/Drivers)
- [8 Linux Commands: To Find Out Wireless Network Speed, Signal Strength And Other Information](http://www.cyberciti.biz/tips/linux-find-out-wireless-network-speed-signal-strength.html)
- [RT5572 cfg80211.c source for updating RT3573 driver in newer kernel](https://github.com/boundarydevices/rt5572/blob/master/os/linux/cfg80211.c)
- [http://forum.doozan.com/read.php?2,6300](http://forum.doozan.com/read.php?2,6300)
- [Question: AP support in 5ghz?](https://github.com/abperiasamy/rtl8812AU_8821AU_linux/issues/10)
- [rt2800usb.c source](http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/drivers/net/wireless/rt2x00/rt2800usb.c)
- [rt2x00usb.c source](http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/drivers/net/wireless/rt2x00/rt2x00usb.c)
- [RPi USB Wifi Adapter](http://elinux.org/RPi_USB_Wi-Fi_Adapters)
