---
layout: post
tags: hymer
title: Week 4 Report
---

### Feb. 20, 2017 

Today, I created three test cases (vertical line, horizontal line, stairstep) in Microsoft Paint and engraved them in with the SuperCarver software.
We saved the data and images so that we can start trying to understand the protocol.

### Feb. 22, 2017 
Today we focused on trying to decipher the protocol.
We think that we have identified a setup phase which defines the outer coordinates and instructs the carver to trace a box around this area.
Then, it issues a start command.
It then issues packets which appear to be of the format:
incremental identifier : 2 bytes of x-coordinates : 2 bytes of y-coordinates : 0x00 padding : 0xff

This command appears to be the command to move with the laser on.

Our testcases were all continuous lines without any breaks, so they consist of a bunch of these packets, all numbered sequentially.

We next need to see how the laser handles movement without carving.
