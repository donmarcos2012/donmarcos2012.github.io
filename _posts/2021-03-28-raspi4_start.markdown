---
layout: post
title:  "Raspberry Pi 4B desktop PC"
date:   2021-03-28 17:29:06 +0200
categories: Raspberry Pi 4
---
#### bargain Desktop Computer?

![raspberry image](/images/raspi.jpg)

The Raspberry Pi is a very popular SBC since its introduction in 2012 especially for enthusiasts and tech-hobbyists. The newest Model Pi 4B is the subject of this blog entry and you will often read that the Raspi could replace a full desktop PC (with certain limitations). Well, that is probably true, with the emphasis on _certain limitations_. The model 4B's advantages over the older generations are:

1. It has USB 3.0 ports which are significantly faster than the older generation 2.0 ports. This allows to connect high speed flash drives, used on "real" desktop computers and circumvent the slow bottleneck of the micro SD port. This is a major step up to previous generations and brings the Raspi closer to "real" desktops.

2. It is available with 2, 4 or even 8 Gigs of RAM. This is a _huge_ advantage compared to the older models. With that amount of RAM you can install and _run_ many typical desktop applications. They will run fluently and much faster than on the old models. Often you won't feel a difference to more powerful computers.

3. The gigabit ehternet port is no longer connected to the USB-bridge and thus is almost three times faster.

4. Other differences are minor, but still improvements: 
* LPDDR4 RAM instead of LPDDR2
* Bluetooth 5.0 (old versions: 4.2)
* ARM Cortex-A72 CPU, around two times faster per clock cycle than the older Cortex A-53
* slighty higher clock speed (1.5 GHz vs 1.4 GHz on the 3B+)
* better GPU (VideoCore VI vs VideoCore IV): allows H.265 4Kp60 vs H.264 1080p30

5. everything has itzs price, and improvements in some aspects also mean drawbacks in other aspects:
* its more expensive, especially the 4 and 8 Gig versions
* higher power requirements
* heats up very quickly and needs good cooling to prevent throttling
* changes to the board layout means not all accessories are compatible


There are still many differences between a Raspi and "standard" desktop PCs: It starts with the assembly of the tiny computer, and there is a lot to install and configure. Many things do not work "out of the box". Also, many web pages and how-tos for the raspi are already outdated, many tips and suggestions do no longer work with the newest Software for the Raspberry Pi.
This blog entry is up-to-date and I will try to keep it up-to-date as good as I can. 

Furthermore, the Raspi is similar to the chicken or the egg dilemma, because to get a budget desktop system you will need a desktop system in the first place to install the Raspi! (Unless you buy a full kit with preinstalled OS on a memory card, but even then you might run into problems and need another PC with a card reader sooner or later). 

In the following "project" I will write instructions on how to install a Raspberry Pi 4B as an (almost) complete desktop PC, what hardware you need, and what the total cost will be.
As you will see, it is not really a "budget desktop", but more on that later.

#### What you need (for my recommended setup):

* Raspberry Pi 4B with 4 Gigs of RAM: 60€
* genuine power supply (5 Volts, 3 Amperes): 8€
* genuine case: 8€
* genuine Raspberry Pi 4 Case Fan: 5€
* 16 Gigs micro SDHC card: 6€
* genuine micro HDMI to standard HDMI cable: 6€

The 4 Gigs-version is fully sufficient for a lot of desktop applications. If you have software which _needs_ more than 4 Gigs of RAM you probably should not run it on a Raspi 4, because the machine is just too weak for powerful tasks. Even the 2 Gigs version is useful for many tasks: I'm writing this blog entry on a Raspi with Chromium browser running in the background on a XFCE-desktop and only 380 Megs of main memory are in use. Furthermore: As long as you install a 32 bit operating system a single application may only allocate a maximum of 3 Gigs of RAM. Only a 64 bit system can make full use of more than 4 GB.

I strongly recommend to buy the original power supply from the Raspberry Foundation, as it delivers enough power for the demands of the Raspberry Pi 4. Do not use cellphone chargers or cheap power supplies! They often have voltage fluctuations/oscillations resulting in the Raspi clocking down very often or even crashing! Your power supply should also deliver at least 3 amperes (the genuine one does that) if you plan to connect a SSD to the Raspi, otherwise you might run into a power shortage, causing slowdowns and crashes.

The genuine case is best for the money: It gets the job done (protect the SBC sufficiently) and is cheap. 
While there are many cases from third-party suppliers, I have found only a few which convinced me, and all of them are more expensive, or for special uses.

The Pi gets hot very quick, and therefore you should install the fan, as it fits perfectly into the genuine case to prevent the CPU from reaching 80°C, when it would clock down (and get very slow). The fan is rather loud and annoying, but with the right settings it engages very rarely and stays silent most of the time.

The genuine HDMI cable is your best bet, because its cheap, 100% compatible and supports 4K resolutions. I advise against HDMI adapters as you might easily damage the tiny and fragile port on the Raspberry. Last but not least we need a memory card to install the operating system and to update the firmware on the Pi. A cheap card with 16 Gigs is sufficient.

But we are not done yet. For a "real" workstation we need fast mass-storage, because memory cards are rather slow, and they will fail after a while of continuous use. I recommend a SATA-SSD, they are fast and rather cheap to get, for instance:

* Kingston A400 SSD 120 Gigs: 24€
* JSAUX USB 3.0 SATA adapter: 10€

As you see, you obviously need an adapter or a case for the SATA-drive, but be wary: A lot of cheap adapters and cases will have problems with the Raspberry Pi: The Pi wants to use the UAS-protocol (USB attached SCSI) when accessing drives on the USB 3 port, while many controllers do not support this. If your controller does not support UASP, you will have to use a workaround and you won't get the full performance of the high speed USB-port on your Raspberry. More on that later.

It's best to buy a UAS-compatible adapter in the first place, a compatibility list can be found here for instance:

[jamesachambers.com][compatible-drives]

You might also deploy an M.2 NVMe drive, but they are no (or only marginally) faster then SATA drives on the USB port and more expensive.
Another, even less costy solution, would be a classic hard disk drive, if you have one left over. _But_ these drives usually have higher power consumption and if you are unlucky the power supply of the Raspi is not sufficient enough. In that case you would need a powered USB hub. Also, hard drives are quite slow compared to SSD's. If you plan to store huge amounts of data a HDD would be a good second drive. In that case you will need a powered hub or a HDD-case with a separate power supply

We are not finished yet with our shopping list, because a desktop PC needs a keyboard, mouse and display:

* wireless brand-name keyboard: around 30€ (2.4 GHz wifi or bluetooth)
* wireless mouse: about 10€ (again 2.4 GHz or bluetooth)
* full-HD 24" display: 100€

You do not really need wireless input devices, but with conventional keyboards and mice you will have a lot of cables on your desktop, something I do not like. The bluetooth connected keyboards and mice have a disadvantage though: They are useless to install the operating system - you need cabled backup for this (well, you could configure everything from a remote terminal, but that is very cumbersome in my humble opinion).

All in all, thats almost 240€ (or dollars). This isn't low budget. In fact, if you don`t already own any piece of hardware and want a budget PC for daily use, you could buy a used business notebook for less: It would be more powerful than a Raspberry, would also have at least 4 Gigs of RAM, is portable(!) and the installation would be much simpler. The disadvantages would be the smaller display and broken or dead batteries (which does not matter if you use it stationary).

However, if you already own a keyboard, a mouse and a display and need just a replacement for your very outdated desktop system the cost for the Raspberry hardware would be only 93€. That is low budget.

In the next chapter we will install an operating system on the Pi.

Thanks for reading!

---

Created with [jekyll][jekyll-link]

[compatible-drives]: https://jamesachambers.com/raspberry-pi-4-usb-boot-config-guide-for-ssd-flash-drives/
[jekyll-link]: https://jekyllrb.com/
