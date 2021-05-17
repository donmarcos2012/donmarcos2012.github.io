---
layout: post
title:  "A premium fan"
date:   2021-05-16 12:28:06 +0200
categories: fan arm noctua
---
### A premium fan at a premium price

Some cheaper fans like the one included with the Icon Case are not very well suited to PWM-regulation. And if they run at full rpm, they are more or less noisy, mainly because they are rather small and run at high rpms.

Better fans are more expensive, and this is the _one_ drawback of the fan I'm going to review here, the price is around 15€ here in Europe. That is 1.5 times more expensive than the Icon Case that comes _with_ a fan!

It's the Noctua NF-A4x10 **5V Version** (yes, there is also a 12V version). The fan comes in a big package (for a 40mm fan) with a lot of cables and adapters:

![noctua_package image](/images/noctua01.jpg)

All of these cables and adapters are useless if you want to use this fan with a Raspberry Pi, you have to cut the power cable of the fan and solder it to the connectors. Noctua should think about that and sell the fan only, without accessories (the 5V version is more or less useless for conventional PCs - the fans there run at 12V, so you only need adapters for the 12V version in a PC).

However, lets install it into the Icon Case, it fits perfectly:

![noctua_icon_case image](/images/noctua02.jpg)
(yeah, the cables are too long, but some adhesive tape helps to fix everything :) )

You have to change the Python scripts to control the fan:

* the fan_speed variable's lowest value is 60! The fan will **not** run at lower values, and at values lower than 70 the rotation speed is way too slow!
* change the PWM_FREQ value to 50, the fan runs better then

Now to the premium qualities of this fan: It is **very** silent, at 80% you can barely hear the fan (only if you get very close to the case), and at 100% it is not even remotely annoying. The cooling efficiency is at least as good as the cheaper fan of the Icon Case.

Conclusion: Noctua holds their promises and sells a fan of excellent quality. The one drawback is the very high price tag (for a 40mm fan). They should cut the costs by selling the fan only, without unneccessary cables and adapters. 

Thanks for reading!

Created with [jekyll][jekyll-link]

[jekyll-link]: https://jekyllrb.com/
