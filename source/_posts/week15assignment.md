---
title: Week 15 - Networking & Communications
date: 2016-05-23 16:55:10
tags:
---

![](http://7xjpra.com1.z0.glb.clouddn.com/week15.png)

<!--more-->

## Lecture Notes

I've updated Week15's lecture notes in [my gitbook](https://kidult00.gitbooks.io/00fabnotes/content/Week15/15_Networking&Communications.html) .

## Assignment

> design and build a wired &/or wireless network connecting at least two processors



I make two boards. One as bridge, one as node:

![](http://7xjpra.com1.z0.glb.clouddn.com/WeChat_1465550293.jpeg)


make -f hello.bus.45.make

sudo make -f hello.bus.45.make program-usbtiny

```
avr-objcopy -O ihex hello.bus.45.out hello.bus.45.c.hex;\
	avr-size --mcu=attiny45 --format=avr hello.bus.45.out
AVR Memory Usage
----------------
Device: attiny45

Program:     768 bytes (18.8% Full)
(.text + .data + .bootloader)

Data:          4 bytes (1.6% Full)
(.data + .bss + .noinit)


avrdude -p t45 -P usb -c usbtiny -U flash:w:hello.bus.45.c.hex

avrdude: AVR device initialized and ready to accept instructions

Reading | ################################################## | 100% 0.01s

avrdude: Device signature = 0x1e9206
avrdude: NOTE: "flash" memory has been specified, an erase cycle will be performed
         To disable this feature, specify the -D option.
avrdude: erasing chip
avrdude: reading input file "hello.bus.45.c.hex"
avrdude: input file hello.bus.45.c.hex auto detected as Intel Hex
avrdude: writing flash (768 bytes):

Writing | ################################################## | 100% 1.07s

avrdude: 768 bytes of flash written
avrdude: verifying flash memory against hello.bus.45.c.hex:
avrdude: load data flash data from input file hello.bus.45.c.hex:
avrdude: input file hello.bus.45.c.hex auto detected as Intel Hex
avrdude: input file hello.bus.45.c.hex contains 768 bytes
avrdude: reading on-chip flash data:

Reading | ################################################## | 100% 1.48s

avrdude: verifying ...
avrdude: 768 bytes of flash verified

avrdude: safemode: Fuses OK (H:FF, E:DF, L:62)

avrdude done.  Thank you.
```

Then connect the boards and fuse 

![](http://7xjpra.com1.z0.glb.clouddn.com/WeChat_1465550294.jpeg)

Strange thing happened. Just connet my bus board to TTl2USB, the led would turn on. It shouldn't because no vcc is conneted to it. So I spent a lot of time to debug. Finally, I fould that I had soldered one of the TTL pin with another line:

![](http://7xjpra.com1.z0.glb.clouddn.com/solderingproblem.jpg)

After solving this mistake, I ran term.py in terminal:

``python term.py /dev/tty.usbserial-A400gwhT 9600``

And the led on the boards turn on according to the keyboard signals:

![](http://7xjpra.com1.z0.glb.clouddn.com/WeChat_1465569383.jpeg)

Video:

{% youtube t6y-v9ZCXDY %}