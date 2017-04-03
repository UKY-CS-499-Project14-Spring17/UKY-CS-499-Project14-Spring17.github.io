---
layout: post
tags: sparks
title: Week 8 Report
---

### Mar. 27, 2017

Today, we organized around the remaining tasks. We agreed on the protocol from within each component. I will be handling parsing out the image one point at a time, as a Pixel struct object for Lucian and Patrick to handle. This should handle the core of black & white and greyscale engraving. Patrick and I discovered that the canvas on the supercarver software is close to the overall travel maximum of our code, and is 1113 pixels (0x459) both directions.

### Mar. 29, 2017

We continued to work on code and test the limits of our engraver. Although our engraver can handle 0x500 pixels in both directions, we decided it was best to continue with the engraver's default settings, although we can make an experimental mode to override the maximum canvas size. The Pixelator code is nearly done, which will handle converting this MagickWand object image into an ordered set of pixels.

### Mar. 31, 2017

Let it be known that today, we engraved an image, beginning to end. `htpewpew` officially works! I suspect that some setting has been misconfigured from all our fumbling around the last few days, but it functionally works. I think we can have a lot of the issues ironed out next week. The image came up really weak, but the original software also is engraving weakly right now, so I think there's a setting that needs to be reset.
