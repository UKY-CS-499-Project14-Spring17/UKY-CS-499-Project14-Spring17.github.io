---
layout: post
tags: hymer
title: Week 5 Report
---

### Feb. 27, 2017 

I spent today trying to get data for the additional test cases we identified last week.
It was straightforward to get samples of horizontal and vertical lines with breaks.
It appears that there is not a separate 'move' command; the host sends the next coordinates without interrupt. This makes our job easier.

The greyscale image was not as easy. I drew solid boxes in varying shades of gray from white to black in Paint.
When we tried to engrave the image, the software and/or engraver kept crashing. We were unable to get it to work.

We eventually were able to create useful date by drawing just the outlines of boxes. Even this took a couple shots however, the engraver continued to crash.
We noticed that the engraver generally reports back it's status signal (well, we think it's a status signal) every 800ms. However when it crashes, the signal is reported every 100ms.

### Mar. 1, 2017

I didn't get a whole lot done today, I had other commitments. We worked on finalizing our design and presentation.


### Mar. 3, 2017

We talked to the engraver today! I used the `screen` program to connect while monitoring with `tshark`.
I identified the device by saving the output of `ls /dev/` with the engraver unplugged and diffing after plugging in the engraver. It was `/dev/ttyUSB0`.

I ran `screen /dev/ttyUSB0 115200`, where 115200 is the baud rate which Paul had identified.

I was able to issue the commands to set the bounds of the drawing, and then told the engraver to draw the box. It worked, and I was able to read the status commands.

This was complicated by the fact that we had to send raw hex data. We're going to need to find a better way to do it than this, although it does work. I'll document the procedure on the meetings page.
