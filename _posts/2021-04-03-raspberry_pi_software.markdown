---
layout: post
title:  "Software for your Desktop"
date:   2021-04-03 17:42:06 +0200
categories: Raspberry Pi 4, Software
---
### Configuring your desktop

XFCE is a highly configurable desktop and I will show some of the customization options in this blog post.
You are encouraged to adapt this to your liking.

### Basic Settings

1. First you should set the desired screen resolution in case the Raspberry's auto-detection got it wrong: 
Right click somewhere on the empty desktop and select Applications -> Settings -> Display
2. Enable auto-login: Again right click somewhere on empty space and select Applications -> System -> Xfce Terminal. Start sudo raspi-config. Then Select "1 System Options -> S5 "Boot / Auto Login" -> "B4 Desktop Autologin"
3. You can see all available settings by launching "Applications -> Settings -> Settings Manager.
You can also launch applications with the Launcher in the upper left corner, but I suggest to replace this launcher with:

### The Whisker Menu

The default applications menu of XFCE seems a little old-fashioned. The Whisker Menu is more streamlined and is in itself customizable. It is easily activated: Right click on the top panel and select "Panel > Add new items". Scroll down the list and choose the Whisker Menu. Then right click on the whisker symbol and select Move to move it to the desired position in the panel. When that is done, right click on the Launcher and select "remove".
The Whisker Menu has many customization options, access them by right clicking and selecting "Properties".

### Customizing the look of Xfce

There are countless ways to change the look of the desktop environment. As an example, I will only show one way here to change the design of the desktop, as it is highly a subjective matter:
1.) Install the murrine-engine: sudo apt install gtk2-engines-murrine
2.) Download the Pro-Dark-Theme for Xfce: [PRO-Dark-XFCE-Edition](https://www.xfce-look.org/p/1207818/). Under Files you will want to select the "PRO-dark-XFCE-4.14.tar.xz" version (the latest).
3.) Create a hidden themes-folder in your home directory: mkdir ./themes
4.) Extract the contents of the package to ~/.themes/PRO-dark-XFCE-4.14
5.) Goto Settings -> Window Manager and select the style.
6.) Log out and back in.

### Essential software packages

There is not much software installed with the Xfce Desktop, not even a browser. Let's change this: Select the terminal window (or restart it). The command to install new packages is:
~~~
sudo apt install *package name*
~~~

Here are some suggestions:

1.) *chromium* - the Chromium browser. While there are many other alternatives, this browser has many patches from the Raspberry Foundation for better hardware support. This might change in the future, but for now it performs best on Raspberry OS.

2.) *geary* - is a lightweight email client, easy to use and has all the features you need for sending and receiving email. It is a perfect candidate to fulfill the [KISS principle](https://en.wikipedia.org/wiki/KISS_principle) in its entirety.

3.) *gimp* - the GNU Image Maniulation Program - the de facto standard image editing software in the open source world. It runs well on the Raspberry Pi.

4.) *libreoffice* - if you need a full office-suite this one is available on Raspberry OS.

5.) *pi-bluetooth* and *blueman* - packages to connect your bluetooth devices to the Raspi. Once installed you will see the Bluetooth-plugin in the top panel. Here you can pair and connect all kinds of bluetooth gear.
 
---

Created with [jekyll][jekyll-link]

[xfce.org]: https://www.xfce.org/
[jekyll-link]: https://jekyllrb.com/
