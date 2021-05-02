---
layout: post
title:  "(almost) silent cooling"
date:   2021-04-25 16:30:06 +0200
categories: Raspberry Pi 4, fancontrol
---
### Silent cooling

The Icon case comes with active cooling in the form of a fan, but, as with most other cases, there is no possibility to control the fan - it is running at full speed all the time (or not at all if you decide to not connect it). Some of these fans are quite noisy, so some people connect the fan to the 3.3V pin on the GPIO. However, this should not be done, as the power requirement for these fans is sometimes too high for the 3.3V regulator on the Raspi!

A more advanced approach to active cooling is to control the fan speed depending on the cpu temperature. This is easily accomplished as the Raspberry Pi has all the tools to control fans with PWM (pulse width modulation) and Python.

If you are interested in the details you can read more about that:
[RasPi.TV software PWM][raspi.tv]

And about the basics of controlling GPIO devices with Python:
[raspberrypi.org/gpio][raspberrygpio]

Well you do not have to read several books about Python programming or electronics in general. It is actually quite simple to control a 5V fan with the Raspi.

All we need to control a fan is a NPN-transistor used in open collector configuration, a resistor, a diode, some pins and wires.

The schematics for this circuit are very simple:

![pwm circuit img](/images/pwm_fan_circuit.jpg)

You can find an overview of the Rapi's pinout on a lot of sites, for instance here:

[Raspi Pinout][pinout]

Parts list:

* Q1: bipolar transistor SC 8050 40V 0.5A in TO-92 housing (or similar)
* diode: 1N4004G 400V, 1A (or 1N4001)
* R1: resistor 1k, 1 watt
* some pins and cables to connect to the GPIO pins on the Raspi
* a small prototype board

part cost: around 1€ / 1$

The actual circuit should be as small as possible or it will not fit into the Icon case:

![pwm soldered img](/images/pwm_circuit.jpg)

It's ugly, but it has to be as small as possible, and you won't see it, once it is installed :)

### Scripts for testing and controlling the fan

We need two short Python scripts, one is to test values for the specific fan, the other is for actually controlling the fan depending on the cpu temperature.

~~~
#!/usr/bin/python
import time
import RPi.GPIO as GPIO
import sys

FAN_PIN = 21
WAIT = 1
PWM_FREQ = 20

GPIO.setmode(GPIO.BCM)
GPIO.setup(FAN_PIN, GPIO.OUT)

fanc=GPIO.PWM(FAN_PIN,PWM_FREQ)
fanc.start(0);

try:
  while 1:
    fanSpeed=float(input("Choose fan speed: "))
    fanc.ChangeDutyCycle(fanSpeed)

except(KeyboardInterrupt):
  print("\nFancontrol ended\n")
  print("last value: {:02.0f}".format(fanSpeed))
  GPIO.cleanup()
  fanc.stop()
~~~

Enter a value between 0 and 100 and find the minimum value for the fan to engage (for most fans this is around 20.

The second script controls fan rpm depending on temperature:

~~~
#!/usr/bin/python

import RPi.GPIO as GPIO
import time
import sys

# Configuration
FAN_PIN = 21   # BCM pin used for PWM of transistor base
WAIT_TIME = 2  # refresh interval time
PWM_FREQ = 20  # Frequency of PWM; change if fan makes rattling noises

# Configurable temperature and fan speed steps, number of steps must be equal!

tempSteps = [55, 62, 70, 75]   # [ in degrees celsius ]
speedSteps = [0, 50, 70, 100]  # [ fan rpm in % ]

# Setup GPIO pin
GPIO.setmode(GPIO.BCM)
GPIO.setup(FAN_PIN, GPIO.OUT, initial=GPIO.LOW)
fanc = GPIO.PWM(FAN_PIN, PWM_FREQ)
fanc.start(0)

i = 0
steps = 0
cpuTemp = 0
fanSpeed = 0

# We must set a speed value for each temperature step
if len(speedSteps) != len(tempSteps):
  print("Number of temp steps and speed steps are not equal!")
  exit(0)

try:
  while 1:
    # Read CPU temperature
    cpuTempFile = open("/sys/class/thermal/thermal_zone0/temp", "r")
    cpuTemp = float(cpuTempFile.read()) / 1000
    cpuTempFile.close()

    steps = len(tempSteps) - 1
    
    for i in range(1, steps+1):
      if abs(cpuTemp) > tempSteps[i]:
        fanSpeed = speedSteps[i]
        
    if abs(cpuTemp) <= tempSteps[0]:
      fanSpeed = speedSteps[0]
    print("Fan speed = {:02.0f}".format(fanSpeed))
    print("Temp = {:02.0f}".format(cpuTemp))
    fanc.ChangeDutyCycle(fanSpeed)
    time.sleep(WAIT_TIME)

# If a keyboard interrupt occurs (ctrl + c), the GPIO is set to 0 and the program exits.
except KeyboardInterrupt:
  print("Fan ctrl interrupted by keyboard")
  GPIO.cleanup()
  sys.exit()
~~~

The script checks the temperature every two seconds, and sets the fan speed accordingly. You can adjust the values for temperature and fan speed with the values for tempSteps and speedSteps:

~~~
tempSteps  = [55, 62, 70, 75]
speedSteps = [0, 50, 70, 100]
~~~

The values work like this: Once the temperature reads 62° the fan speed is set to 50%.

If the temperature reaches 70° the fan speed is set to 70%, and if the temperature hits 75°, the fan will run at full speed (100%).

If the temperature drops to 55° the fan is disengaged.

You can set your own values, but the number of tempSteps and speedSteps has to match.

The frequency value PWM_FREQ determines how often the fan is turned on and off per second. Some fans will make a rattling noise, depending on the frequency, you can try to raise or lower the values, but you should stay within 10 Hz and 100Hz. 

The fan included in the Icon case always makes a slight rattling noise when turned on with rpm values below 100%. If that is annoying to you, you could set the temp- and speedSteps to either set the fan to 0 or 100% depending on the temperature. I think higher quality fans won't make noises when controlled by PWM. You would set tempSteps and speedSteps like this:

~~~
tempSteps  = [56, 65, 70, 75]
speedSteps = [0, 100, 100, 100]
~~~

With these values the fan turns on to full speed when the CPU reaches 65° and turns off, once it cools down to 56°. 
I have already ordered another fan which (hopefully) is better suited to PWM controlling and does not make rattling noised when throttled to values below 100%.

Thanks for reading!

---

Created with [jekyll][jekyll-link]

[jekyll-link]: https://jekyllrb.com/
[raspi.tv]: https://2013/rpi-gpio-0-5-2a-now-has-software-pwm-how-to-use-it
[raspberrygpio]: https://www.raspberrypi.org/documentation/usage/gpio/python/README.md
[pinout]: https://pinout.xyz/
