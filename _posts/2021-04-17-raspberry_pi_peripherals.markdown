---
layout: post
title:  "Connect the RasPi to the world"
date:   2021-04-17 19:02:06 +0200
categories: Raspberry Pi 4, USB-Hub
---
### More power to you

Once you connect more peripherals to your Raspberry Pi, you might sooner or later run into problems: The official power supply delivers only 15 Watts, which is not much. Say you want to deploy a mass storage device like a 2.5" harddisk drive: The starting current of these drives is often too much for the tiny power supply of the Raspberry Pi and the circuits on the board, resulting in a system crash most probably. Even SSDs sometimes draw too much power or, if you are using a combination of several USB devices you might overstrain the power supply.
These cases are rare, usually you can connect an SSD, a wifi-dongle for keyboard and pair a bluetooth mouse without problems, for instance. Yet there are uses cases where you will need another solution.

Some peripherals are faulty in itself: For instance, I have a power switch that connects to the USB-C port of the Raspi and enables a convenient way to turn on and off the SBC. However, this switch has a rather high electrical resistance in itself which leads to an unstable system once *any* device is connected to one of the USB ports!

### a powered USB 3.0 Hub

The solution is a powered USB-Hub. I've tested one from [atolla.us][atolla-us]: The [USB 3.0 Hub Set (204K)][model204k]. It has four ports, each with a seperate on/off switch, and a fifth port for charging other devices, like cellphones. The power adapter for this hub has 15 watts, which should be sufficient for powering hard drives, SSDs and whatever comes to your mind.

![atolla hub img](/images/atolla_hub01_scaled.jpg)

(picture © atolla  2021 used with kind permission) 


This provides an easy solution if you have power shortage problems. 
 
---

Created with [jekyll][jekyll-link]

[xfce.org]: https://www.xfce.org/
[jekyll-link]: https://jekyllrb.com/
[atolla-us]: https://atolla.us
[model204k]: https://atolla.us/products/atolla-powered-usb-3-0-hub-with-3ft-usb-3-extension-cable-204-k
