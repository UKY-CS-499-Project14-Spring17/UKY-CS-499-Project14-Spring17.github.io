---
layout: post
tags: hymer
title: Week 8 Report
---

### Mar. 22, 2017 

We figured out why our demo didn't work! We just weren't thinking straight and, instead of using the serial port as the output file, tried to redirect STDOUT to the serial port.
The parser handles the serial port protocol, so it didn't work right when it appeared to be writing to STDOUT.

Besides this, we tried drawing an [x pattern](https://github.com/UKY-CS-499-Project14-Spring17/htpewpew/blob/master/reverseEngineering/rawData/better/x.png) and we modified the parser to be able to display time differential between messages.
We suspected that the host program may have been interpolating how long it should wait to issue the next command based on the distance between points.
This did not prove to be the case.

However, while pursuing this route, we realized that the HTPOW appears to have a 30 instruction queue. It fills this queue, executes the instructions, and then issues a message requesting more data.
The SuperCarver host program will wait for this signal after every chunk of 30 instructions.
We modified our parser for similar behavior, and it appears to function much better. We believe that some instructions were being dropped before when the queue was full.
