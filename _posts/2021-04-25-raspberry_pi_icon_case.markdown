---
layout: post
title:  "Another case"
date:   2021-04-25 09:11:06 +0200
categories: Raspberry Pi 4, case
---
### More room for Raspi

I recently tried another case for my Raspberry Pi: [52pi Icon case][52pi-icon-case].

It has active cooling (more on that in the next blog entry), has a little more room than the genuine case and looks like a bonsai tower PC :)

It can also be deployed in different positions: flat, or upright in two variants. The upright position has an advantage: When the Raspi is vertically aligned it dissipates heat better than when horizontally aligned.

![icon case img](/images/icon_case.jpg)

Note that the rear ports of the Raspi are closed in the images above. You have the option of omitting the rear plate when assembling the case, but if you do not need the usb and network connections you can have a slightly higher level of protection with this case. The micro-SD-slot and the HDMI and power connectors are always accessible of course.

Included in the package is a 40mm fan, which is, compared to the small genuine fan from the Raspi-Foundation, less noisy, and is very effective in cooling the chips on the board. Also included are 4 heat sinks, but I did not install them, because I believe that heatsinks for very small chips are not very effective as they have to be glued on the chip with a thermal adhesive tape. This slows heat dissipation, but I admit I did not test that. However, bigger CPUs are cooled by placing the heat sink directly on the heat shield or the die with just a little thermal paste - this is more effective than adhesive tapes.
Once I get my hands on a high quality thermal adhesive tape, I might run some tests with and without heat sinks.

If the case is placed in an upright position and the Raspi does just some easy tasks (like running a text editor while I'm writing this blog entry) it does barely heat up: The temperature stays in the 60°C range without active cooling. 

For this reason I have tinkered a simple PWM-regulation for the fan and because the Icon case has more room than other cases, the tiny regulation circuit fits into the case. We will have a closer look at that in the next blog entry.

### Conclusion

If you do not have a case for your Raspberry Pi 4 yet, this is a good choice. It is reasonaby priced at around 10€ or 11$ and well made. Assembly is easy and quick, everything fits perfectly together. The red stripes are stickers, so you need some care and a pair of pincers when applying them to the case. There are two sets included, just in case you would mess up on the first try :)

If you need a case with active cooling this is probably a very good choice (I did not test any other cases yet), because it just works and has some options: Positioning, mounting the rear plate and the possibility to install a regulation for the fan. You could also replace the fan with another 40mm-fan with different specs.

The cooling power of the fan is also sufficient for overclocking the Raspi if you want to do that.

Thanks for reading!
 
---

Created with [jekyll][jekyll-link]

[jekyll-link]: https://jekyllrb.com/
[52pi-icon-case]: https://wiki.52pi.com/index.php/Icon_Case_For_RPi_4B_SKU:_ZP-0099
