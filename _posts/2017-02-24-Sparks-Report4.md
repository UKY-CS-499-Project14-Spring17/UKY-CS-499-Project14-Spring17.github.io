---
layout: post
tags: sparks
title: Week 4 Report
---

### Feb. 20, 2017

Today, we launched wireshark and collected a lot of good data. Lucian developed 3 simple patterns and we ran those on the engraver. The format is really terrible to understand, but we're making some progress in understanding it. I'd like to make a parser so that we can remove all the null packets and such. There's a lot of stuff to parse though, so it might take some work. I worked on the High-Level Design while they continued to unpack the engraver protocol [(see an example here)](https://github.com/UKY-CS-499-Project14-Spring17/htpewpew/blob/188e7e8d1ea16d9267589e5794e88972809ea1f3/reverseEngineering/rawData/better/horizontal), but I'm afraid that the complexity reading the engraver port will overwhelm our ability to actually understand what it does.

### Feb. 22, 2017

I worked on the layout of the presentation today. The template is done, I just need more data, so I'm putting this on the back-burner until the weekend. Meanwhile, I've made a [crude parser](https://github.com/UKY-CS-499-Project14-Spring17/htpewpew/blob/master/reverseEngineering/parser.rb) (that needs some work!) that should help speed up the process of understanding the serial communication. It reduces file sizes to less than 1/10 of the raw size. Patrick has decided that every 7th byte is a ```0xff```, so it probably is a end-of-command bit. With this in mind, the parser groups bits sent into groups of 7 and prints them out.
