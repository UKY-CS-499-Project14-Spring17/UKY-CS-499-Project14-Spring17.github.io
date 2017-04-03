---
layout: post
tags: sparks
title: Week 9 Report
---

### Apr. 03, 2017

I have made a simple ruby script `dummyUSB.rb` which can listen on a virtual tty port and respond as the engraver would be expected. This will help me test some of my commands without having to be around the engraver. Here's how to use it.

#### Install socat:

`sudo apt-get install socat`

#### Use socat to link to pty (fake tty ports):

```
$ socat -d -d pty,raw,echo=0 pty,raw,echo=0
2017/04/03 09:41:01 socat[7865] N PTY is /dev/pts/4
2017/04/03 09:41:01 socat[7865] N PTY is /dev/pts/5
2017/04/03 09:41:01 socat[7865] N starting data transfer loop with FDs [5,5] and [7,7]
```

#### Launch the port listener:

`lib/dummyUSB.rb /dev/pts/5`

#### Launch the htpewpew software:

`lib/htpewpew <image> -p /dev/pts/4`

