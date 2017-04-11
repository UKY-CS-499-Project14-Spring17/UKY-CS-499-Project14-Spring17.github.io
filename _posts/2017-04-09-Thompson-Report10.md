---
layout: post
tags: thompson
title: Week 10 Report
---

### Apr. 9, 2017

We made a big discovery on Monday. After messing around with the laser intensity and only getting slightly more success we discovered our pictures were not engraving as expected. The X we were printing looked okay so it wasn't until we engraved something less symmetrical that we found out the picture was not engraving right at all. It was getting chopped in a really strange manner. The full picture would be engraved but it would be shifted. For example we engraved a stick man and his face would be split down the middle with one side being cut off on the right edge and the other on the left.

We stayed very late on Monday trying to determine what was causing this very strange behavior. We finally figured it out at the end when we ran the same stick man through HTPOW's software and compared the commands it was sending to our program's. It turns out the least significant bits of the X and Y coordinates count in hex, but only to 64 and then it rolls over. The 2 least significant bits use hex to count to 100 in decimal and then roll over where we were using the full range of hex values.

By Wednesday we changed our code to count correctly and everything engraved perfectly. Since it was such a nice day we left early.
