## Our project requirements (in order by precedent):

#### Reverse engineer intitial handshaking and image transefer protocol

Our first requirement is to examine the HTPOW transfer protocol so we can send an image from the computer (from an image file) to the HTPOW engraver. Whether this is initially stored in the engraver's memory is not important.

#### Implement driver in portable software language (C/C++)

Next, we will develop a set of tools that can be used to send an image using the transfer protocol. These will be a set of files that can be #included, so that any C/C++ project can use our tools for transfering to the HTPOW.

#### Implement Command Line Interface (CLI) for driver

Lastly, we will develop a command line interface so that the tool can be directly run, and will not require any additional code wrapped around it. This will make the tool usable both as a driver (within your own code) or standalone (as a CLI).

## Additional goals (if time allows):

#### Reverse engineer settings/speed protocol

It is not known how the Windows tool controls the speed while streaming a file, but we are interested in investigating this. It may not be possible to effectively reproduce this behavior, but we will try to identify and replicate this protocol.

#### Reverse engineer images storage protocol

There is a seperate protocol on the HTPOW to capture and image from the computer without printing, storing it in memory so that it can be replicated many times without using a computer. This behavior would be nice to duplicate in our driver and CLI, if possible.

#### Pre-process raster image to minimize cutting time

The engraver will travel back and forth between two cutting spaces in a very inefficent manner. Imagine you want to cut the three rectangles shown below in this pattern.

![Image of three rectangles, the middle one seperates the outer two and is above them](/images/engraver-path-1.png)

If the three rectangles above were to be cut by the HTPOW without any guidance, it would choose this path, where the grey dotted lines shows wasted travel space.


![The black path crosses through the empty space without any rectangles repeatedly](/images/engraver-path-2.png)

If each rectangle is sent to the HTPOW seperately, it will only carve the space within the rectange, and will not travel much through the empty space.

![The black path does not cross through the empty spaces](/images/engraver-path-3.png)

We would like to examine methods for saving engraving time buy feeding the engraver only parts of the image at a time. By breaking one image into many, the process could be speed up dramatically.

