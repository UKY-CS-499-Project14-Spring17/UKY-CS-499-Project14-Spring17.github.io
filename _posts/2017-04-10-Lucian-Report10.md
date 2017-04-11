---
layout: post
tags: hymer
title: Week 10 Report
---

### Apr. 3, 2017 

Today, we tried messing with our resizing and centering code. In the process, we realized that carvings were often not coming out correctly.
We tried carving an X, but it came out as a slanted double-cross.
To narrow down the problem, we carved a stickman.
We figured that if we could more easily identify the areas which were incorrect, we could figure out the problem.
The stickman came out carved in two halves, with what should have been the right half carved to the left.

By examining this and looking at the raw data transmitted by the SuperCarver software, we think we found the problem.
The lower byte wraps up to the higher byte at 0x63, not 0xff.
We're going to test this theory on Wednesday.

### Apr. 5, 2017 

Our suspicions were correct!
Luckily, I had made the maximum lower byte size a constant, so it was an easy fix.
The carver now carves as expected!
We didn't do a lot more today.
