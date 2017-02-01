---
layout: post
tags: sparks
---

# Week 1 Report #

### Feb. 01, 2017 ###

This week, we met with our customer (Dr. Dietz and Paul Eberhart) on Monday. The project centers around a laser engraver, the ancient Windows-only application that communicates with the engraver, and an unknown protocol. Paul has started to deconstruct the serial protocol between the software and the engraver, but there are still a lot of unknowns, so it seems like we may need to do a lot of tests to deconstruct the protocol. If the image being burned has two different segments that overlap in the y-direction, the laser will jump back and forth from one segment to the other; this slows it down substantially.

The goal is to create:

1. a portable (likely C/C++ application) that runs in the command line for communicating an image
2. greyscale support for multiple burn depths/intensities
3. support for multiple images isolated from one original image
4. some amount of a GUI that can handle image transfer a little more gracefully
