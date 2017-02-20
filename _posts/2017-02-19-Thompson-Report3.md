---
layout: post
tags: thompson
title: Week 3 Report
---

### Feb. 19, 2017

We met on Monday and Friday. We discovered Monday that my ID isn't able to open the ECE lab and that I needed a key fab. The rest of the day Monday was spent trying to connect the engraver to Lucian's laptop and make it work on the virtual machine. We got the control program to install on the virtual machine but it wouldn't connect to the engraver. The drivers for the engraver were not installing. Lucian tried to manually isntall some drivers and although they were installed it didn't fix the proble. We discovered that there were 2 versions of the control program. One was for wifi and one was for USB. It wasn't clear what version we had or whether the newest version was supposed to support wifi and USB or just wifi. We finished the meeting without being able to connect. I spent most of the meeting doing my best to troubleshoot with Lucian. 

On Friday Dr. Dietz had my key fab so I can now access the lab. He was also able to give us the other version of the control program that uses USB instead of wifi. I installed the control program on my laptop and so did Lucian. We hooked the engraver up to Lucian's laptop and worked on getting communication data from Wireshark. It wasn't too hard to start getting packets from Wireshark, but the communication looked funny. Most of the packets had a lot of USB overhead and then a single byte of data. We know the communication is serial to the engraver but it operates over USB which is not serial by default, so the USB exchanges packets back and forth and another part of the engraver must store the extra byte of information until it has enough for a command. We decided to break and work on coming up with some interesting pictures to engrave and captrue the communication so we can try and decipher it further. 

I haven't done much outside of the meetings on the project. I looked into communicating serial over USB in Linux, and unsurprising like most communication in Linux you just open a file and write/read to/from it. As far as pictures to engrave I think we should do a few simple symmetric shapes such as a circle and then the same picture but just the right or left half and then the same picture again but just the top or bottom half. We also need to run the same picture twice and see if the communication is any different. A plus sign might be better than a circle though. Straight lines are easier to carve and should complete faster.
