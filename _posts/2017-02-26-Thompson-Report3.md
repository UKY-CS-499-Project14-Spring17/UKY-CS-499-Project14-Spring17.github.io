---
layout: post
tags: thompson
title: Week 4 Report
---

### Feb. 26, 2017

We met every day this week. On Monday we got our first runs of the engraver where we were able to capture the communication between the engraver and the control program. At first I was trying to capture data on my computer because Lucian was running late, but then he showed up and I let him do it because his computer is faster and he had already figured out how to trim the communication data to only what we needed to see. We decided to get an image of a horizontal line, vertical line, and stairstep line to start off with. I mostly observed and helped troubleshoot.

On Wednesday we began trying to see patterns in the communications to reverse engineer the protocol. I was able to figure out a lot about it while Grant built a parser to clean up the communications so they are easier to view. We now know that the first byte of the 7 byte string that is sent to the engraver is a counter that increments after each packet. The second and third bytes are X coordinates. The fourth and fifth bytes are Y coordinates. The sixth byte is still as yet unknown, but the seventh is a terminal byte that is always FF. The engraver will sometimes send a 4 byte packet back that is either 3e:01:ff:ff or 3e:02:ff:ff. It is sitll unclear when or why it is sending this but it appears to be either time based since they are always around .8secs apart or based on seeing a certain packet number since those packets tend to fall around when the packet incrment is either 3d or 5b. We need more images to study to get more information. We will capture more interesting images in the future.

On Friday we met and looked at the protocol again as well talked about what we wanted to do for the presentation and design report. Grant figured out before the meeting that the engraver increments after each engraving and is part of the information that it sends back at the end of the carving. Most of the meeting was spent discussing what we need to do moving forward and analyzing the protocol some more. We weren't able to discover much more other than it appears that the engraver dictates to the control program what packet number to start with. Next week we will capture more data and try to send some information to the engraver for additional testing.
