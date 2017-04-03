---
layout: post
tags: hymer
title: Week 9 Report
---

### Mar. 29, 2017 

At the meeting today, we decided that Grant and I are going to split up the unit testing.
He's going to write the tests for the image processing, and I'll do the rest.

I'm also going to write the functions for the streamer.
These funcitons will call the pixelator to get pixel information, then process them into the final commands which will be sent to the engraver.

### Mar. 31, 2017 
I have the streamer functions written. 
After a brief code review, I realized I needed to fix a few things. For example, I needed to add some serial port reads in to wait for the carver.

It actually kind of all works with everything together!
I grabbed Grant's image stuff, and the serial port code that Patrick had been working on, and ran `make`.
It all compiled, and then I plugged in the carver and it worked on the first try!

The image is being carved too quickly, and we're not sure exactly why.
It may be dropping instructions, or the burn dwell time may be out of whack.

We suspect we may have altered a setting along the way by accident. We're going to use the SuperCarver software to try to set it back up correctly.
