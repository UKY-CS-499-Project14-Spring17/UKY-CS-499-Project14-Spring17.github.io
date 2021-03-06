---
layout: post
tags: sparks
title: Week 1 Report
---

### Jan. 30, 2017

This week, we met with our customer (Dr. Dietz and Paul Eberhart) on Monday. The project centers around a laser engraver, the ancient Windows-only application that communicates with the engraver, and an unknown protocol. Paul has started to deconstruct the serial protocol between the software and the engraver, but there are still a lot of unknowns, so it seems like we may need to do a lot of tests to deconstruct the protocol. If the image being burned has two different segments that overlap in the y-direction, the laser will jump back and forth from one segment to the other; this slows it down substantially.

The goal is to create:

1. a portable (likely C/C++ application) that runs in the command line for communicating an image
2. greyscale support for multiple burn depths/intensities
3. support for multiple images isolated from one original image
4. some amount of a GUI that can handle image transfer a little more gracefully

### Feb. 01, 2017

Met with team again. We assigned tasks. I am going to take charge of:

* Web interface (should be done next week)
* Documentation (this will be long term)
* Setup repository for our team

My goal for this week it to set up this website (already mostly done!) and to setup an appropriate repository for storing our work. I suppose we'll be using github so long as Dr. Dietz is okay with the code base being published. That said, I expect that Dietz will likely want this to be open-source and I think that this will be good for the transparency of the project long-term.
