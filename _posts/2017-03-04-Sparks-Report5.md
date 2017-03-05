---
layout: post
tags: sparks
title: Week 5 Report
---

### Feb. 27, 2017

Lucian and Patrick explored some of the protocol for the engraver and I'm going to publish a page about it tonight. Hopefully, we can crack enough of this to really show it off next week, but we'll see. I'm going to work on seeing if I can handle image processing in the meantime. That's kind of a compartmentalized task, so I have hope that I can figure out the ImageMagick library without being dependent on to many other things.

### Feb. 28, 2017

I worked some on my own this evening and got image parsing. Long story short, image.c can take an image as input and either convert it to greyscale or put it through a threshold routine, but I'm not quite sure how the threshold (b&w processing) works. The good news about ImageMagick is that it can do a whole bunch of images, so we're not limited to manually parsing `.bmp` files anymore.

### Mar. 01, 2017

Tightened up the main CLI parser and handling a bit, moving the parser to its own file. It passes a struct over to the image system, which does its magick! The threshold routine uses a value called QuantumDepth as it's max. On my machine it's 2^16, but we can't rely on that. The image.c now collects the user's QuantumDepth and adjusts the threshold out of 100% of that depth.

### Mar. 03, 2017

WE ARE SO CLOSE TO PROCEDURAL STREAMING TO THE ENGRAVER. Lucian can do it manually, but I can't quite get my bytecode to go in a way that the engraver is happy with. I worked on making the ruby parser read out hex to the engraver, and the hex part seems to work, but it's not quite there yet...

### Mar. 04, 2017

I added a debug mode to the parser (segfaults, what can I say?) and moved the option parsing over from my homebrew parser to the <argp.h> library, which is pretty fantastic and WAY easier to read. So that's good.
