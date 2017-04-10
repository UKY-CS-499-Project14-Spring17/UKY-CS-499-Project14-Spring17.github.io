---
layout: post
tags: thompson
title: Week 9 Report
---

### Apr. 4, 2017
We made a lot of progress this week. Monday we went over the testing in preparation for what we have to write up for the website. We also came up with a general structure for how we want each model to be written and how they would communicate with each other, and divided up the work amongst ourselves.

On Wednesday I had my part of the serial communication code ready to test. Grant and Lucian had brought me an Arduino as a surrogate for the engraver to test with. It simply echoed back whatever was sent to it. I could get my code to work on the Arduino but I could not get my computer to see with the engraver. It turns out that Macs handle devices differently and don't just give them all a /dev file automatically, so I couldn't get the engraver to show up on my virtual machine. Grant tried the code on his machine with the engraver hooked up, but it did not work. I resolved to buy a computer and put Ubuntu on it so I could be more productive.

On Thursday I bought my new computer and put Ubuntu on it. I was able to figure out that my code wasn't working all the time because it tried to write out too quickly. The program did not give enough time after initialization before trying to write and then read so the blocking read would never see anything. I added a 2 second sleep (1 second wasn't enough) and it works everytime now.

On Friday we met again and integrated our code. Suprisingly the code ran the first try after connecting to the engraver. It didn't actually engraver, but it moved and was firing. We tweaked a lot on the code and we think that the power of the laser has gotten turned down so we will try and turn it back up in our next meeting.

I also looked into the beginning protocol of the engraving again after Grant said he didn't think my assessment in my March 12th post was correct. It turns out he was right.

New information has shown that what I thought before about the software sending 90 commands and then waiting is incorrect. The software does a read every 30 instructions to wait and make sure it is not overloading the engraver. Our data captures show the engraver sending a message to the software while the software is still sending instructions during the first 90 instructions. This made it appear as though the software was not looking for messages from the engraver for the first 90 instructions. Some of the data captures, however, showed the software waiting on the engraver after 60 instructions. 

When you look more closely at the timings of the messages you can see that the software was sending messages faster in the captures where it waited after 60 instructions. The message that the engraver sends to the software is a message letting the software know that it is ready for more data, or that its buffer is empty. If the software is sending messages too slowly, or the engraver is able to empty its buffer too quickly then it will send the signal before the software has a chance to wait for the signal. Then when the software reads to look for the signal after 30 instructions, the signal is already in the read buffer and the software doesn't have to wait for it. This makes it look like the software doesn't wait for the message, when in reality it does. This can be seen easiest by comparing the times between the 30 instructions. In the data captures where the software obviously waits after 60 instructions, the time to send those 60 instructions was much less than the time to send the first 60 instructions in the data captures where the software doesn't appear to wait until after 90 instructions. One data capture breaks this trend, the X shape, but when you take into account the shape it is clear that although the instructions weren't sent any faster the engraver couldn't process them as fast due to the extra travel time in the X shape so it couldn' clear its buffer quickly and the software had to wait for a message after 60 instructions.
