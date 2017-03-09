---
layout: post
tags: thompson
title: Week 6 Report
---

### Mar. 12, 2017

After studying and comparing several of our data captures of different images I believe I have finally figured out the remaining question about the protocol the control program uses with the engraver. First it sends the usual 5 set up commands then waits for a response from the engraver. After it gets a response it starts sending the image data with the starting number dependant on which response the engraver sent. If the engraver sent 3e:01:ff:ff the numbering starts at 5b. If it sent 3e:02:ff:ff the numbering starts from 3d. After waiting for this first response so it knows where to begin numbering the software then sends 90 7 byte instructions and waits on a response from the engraver. The engraver will usually respond twice in the middle of the 90 command sending, but the software ignores them. After the initial 90 commands the software waits for a response from the engraver and then sends 30 more commands and waits for a response. From here on the software continously sends 30 commands and waits for a response until done. Until we captured a larger image this pattern could not be seen because the smaller images only took around 130 or so commands to complete.
