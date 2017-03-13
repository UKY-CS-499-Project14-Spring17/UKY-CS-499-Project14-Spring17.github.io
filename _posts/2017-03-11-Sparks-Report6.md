---
layout: post
tags: sparks
title: Week 6 Report
---

### Mar. 06, 2017

Procedural streaming works! We can duplicate any message sent to the engraver to cause it to engrave again. It's not yet able to compile an image to byte code, but this is a good first start to me. I think we should be able to demonstrate at least a little of the capabilities this week. Next week, during Spring Break, I want to focus on encoding data from an image to the "bytecode" sent to the streamer. I think we can pre-process the image into a pile of operations and send the instructions one at a time based on distance traveled.

Things to note:

* the laser cannot cut properly when engraved with a 0.02 second delay
* for constant wait time, the time must allow for the longest travel (0.002 to 0.1 sec)
* the engraving worked fine with a 0.07 second delay between commands

### Mar. 08, 2017

It didn't engrave for the presentation today, which is disappointing, but I think we'll be able to figure out the issue. As of now, we're not sure what caused this issue, but I'll keep looking. We've not been able to replicate this issue.
