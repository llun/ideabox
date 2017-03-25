# Wifi HomeControl

This somehow extends scope of [another project](wifi-router.md) and already have some prototype (the same as router)

## Features

- Upgradable Wifi (currently I'm using ac 3x3 MIMO card but router board I use is supported new SU-MIMO too, only problem is cost)
- 3 frequency bands, this is my personal requirement for connect my wifi router to another wifi router with wifi, I need this because doesn't have access to landlord router but to reduce the cost, this can be optional. (or if mesh is also required, I would suggest to use 3 bands too)
- Support modern linux (or atleast LEDE project)
- Nice UI, I still doesn't reach this part yet
- Transfer speed as higher as posible, this tested with latest MBP seems depend on configuration, antenna and the card itself.
- Control IoT devices and have automation configuration
- Some security and auditing system
- Log to external services
- Cloud control or in the old term, remote control with 2-factor authentication for cloud
- OpenVPN client, I don't mind to have OpenVPN server inside, but the gateway is better in the cloud and router connects to it
- Storage, USB is ok, internal with sata/m2 would be the best. I don't care raid support much, too advance for consumer use
- Mesh and redundant service, this is optional but would be nice if it can mirror the disk over 2 device (so technically not raid but kind of regional services). Mesh itself should smart in routing too
- Detail network information and graph
- Guest and finegrain client/user control

## Prototype Hardware

Router hardware

- [Compex WPQ864](http://www.compex.com.sg/product/wpq864/)
- [WLE900VX](http://www.compex.com.sg/product/wle900vx/) x 3, 1 2.4 GHz, 2 5 GHz
- [Taoglas FXP523.A.07.A.001 antenna](http://www.mouser.sg/ProductDetail/Taoglas/FXP523A07A001/?qs=sGAEpiMZZMu6TJb8E8Cjr7j%252bpfwlA7T%2fPxI0W26r0Bs%3d)

Tested IoT
- [SoundTouch 10](https://www.bose.com/en_us/products/speakers/wireless_speakers/soundtouch-10-wireless-system.html)

## Project links
- [HomeKit SoundTouch with golang](https://github.com/llun/hksoundtouch)
- [HomeBridge Sensibo](https://github.com/llun/homebridge-sensibo)
- [HomeBridge SoundTouch](https://github.com/llun/homebridge-soundtouch)
- [HomeBridge WifiPresence](https://github.com/llun/homebridge-wifipresence)
- [Other](https://gist.github.com/llun/652654f94992e8d8ce93dab61ba2f4c0)
