---
layout: post
tags: thompson
title: Week 11 Report
---

### Apr. 16, 2017

We got the testing table pretty much done on Monday and Lucian made progress on getting greyscale working in our program. We didn't meet except for Monday because Lucian and Grant were too busy with other classes/projects. I typed up what we had for the testing table in our testing page and added a lot of comments to all of our c files. I think I found an error in the resizing code that I need to discuss with Grant. I also think I might know the algorithm to use to do the anti-aliasing correctly, but we need to get a few more captures from the SuperCarver software so I can confirm. 

We didn't meet Friday but I went to the lab and worked some on my own. I created a few good images to run on the SuperCarver software to test thier anti-aliasing. I also tried to see if the engraver was able to give back any information about its position so that if someone started the engraving too far in one direction we could avoid running into the end of the range and grinding the gears. When you send the 1a 00 00 00 00 00 ff command the engraver sends back 70 bytes of information, but I could not tell what any of it meant. One seemed to be incrementing every time I sent the instruction but that wasn't always consistent. The rest of the bytes stayed the same no matter how I moved the engraver or anything. 
