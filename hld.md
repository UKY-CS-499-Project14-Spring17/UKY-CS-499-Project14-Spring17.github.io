---
title: Software Design
---

# Portable Laser Engravers Interface Design

### Overview
<!-- This can be taken from the requirements and modified as necessary. For a design document you can assume the reader has a technical background. For your projects assume a background of a class member. -->

The [HTPOW brand](https://www.amazon.com/HTPOW-Engraver-Printer-Handicraft-Engraving/dp/B01G36Q558) of laser engravers have a (somewhat) unique protocol for communicating between the computer and the engraver. There is software available for using the engravers, but it only runs on Windows and is not compatible with [Wine](https://www.winehq.org/). Our goal is to examine and replicate the features of this Windows software in a command-line interface so that engraving can be better automated and will work nicely in Linux, Windows, and Mac environments.

### Environment

<!-- List any requirements (operating system, database products, execution environment (Java, Perl, etc.). -->

Our engraving software is written in C/C++ and needs a gcc compiler. It has been tested in Ubuntu 14.04 and 16.04, gcc version 5.2.1 and 5.4.0. Although not guaranteed, this code should be able to compile on any Linux/Unix system with a gcc compiler, possibly including Mac OS X.

This software depends on the following libraries, which are linked or available through the GNU Standard Library: <!-- TODO -->

* ARGP (part of the GNU Standard Library)
* [ImageMagick](https://www.imagemagick.org/script/download.php)

### Module Descriptions and Data Flow

<!--Include a diagram showing the modules and data flow between them. Give a high level description of the function of each module. A pseudo-code format is often used:

Describe the data going into and out of the modules, using structures as necessary. -->

![An image showing the relationships of code modules and external modules](/images/modules.png)

Overall the program accepts 2 kinds of data, pictures to carve and user command line input to interpret. The CLI Parser module, short for Command Line Input Parser, handles parsing the user's input so the program can interpret the commands the user wants to execute. The CLI Parser takes in user input and from it determines what options to set for the image and what image to carve. The Resize Image module resizes the input image to the size that the engraver can print. Then the Convert to Greyscale module converts the image to greyscale so that color images can be engraved. The last image manipulation module is the Threshold module which converts the greyscale pixels to black and white pixels only, based on the threshold value the user entered. If no threshold value was entered then the engraver engraves the greyscale image. The Protocol Definitions module is a library of protocol definitions that the Streamer will reference to send the right instructions to the engraver. The Streamer module is what brings it all together and determines how to break down the image and options into the correct protocol to send to the engraver.

```
	Interpret CLI options
	Read in image file
  Alter image (resize, greyscale, and threshold)
	<< Enhancement: Analyze image for contiguous regions >>
	Test connection to serial port
	Activate engraver
	while( there are regions to engrave ) do
		while( there are pixels to engrave in this region ) do
			<< Enhancement: Greyscale settings: Set laser intensity >>
			Move laser to next pixel
		end
		Travel to next region
		Alert user, bitmap complete
	end
```

<!-- TODO #### G-code (.mpt) Format -->

### User Screens

<!-- Include user screens with description of function and use. -->
```
$ htpewpew.new --help
Usage: htpewpew.new [OPTION...] infile
htpewpew: a CLI for serial communication to a HTPOW laser engraver
NOTE: If no file is supplied, htpewpew will enter interactive shell mode.

 ENGRAVER PARAMETERS:
  -b, --burn-time=burn       Set maximum burn time (default = 60 ms)
  -d, --dry-run              Edit image, show engraving area, and quit
  -i, --intensity=intensity  Set the laser intensity (default = 5)
  -o, --output=outfile       Output to OUTFILE instead of to standard output
  -p, --port=port            Location of USB serial port
  -t, --threshold[=threshold], --bw[=threshold]
                             Use a threshold (0-100%) for black and white
                             (default = 50%)
  -x, --x-offset=x           Automatically offset x location (-250-250)
  -y, --y-offset=y           Automatically offset y location (-250-250)

 INTERFACE PARAMETERS:
  -s, --silent               Supress all standard messages
  -v, --verbose              Enables additional debugging notes

  -?, --help                 Give this help list
      --usage                Give a short usage message
  -V, --version              Print program version
```

### User Scenarios (Use Cases)


A user will start the program from the command line, entering any options they want to change as the program is called. In most cases the user will start by calling the program with the -d option to see the cutting area of the laser on the media they wish to cut. Then the user can adjust the location of the cutting area with the -x and -y options. Once the laser is in the correct location on the media the user would then call the program with any of the cutting settings (-b, -i) or image settings (-t) they want to change from default values and the engraving will begin automatically.

**Display Help Options**

Call the program from the terminal with `htpewpew -?` or `htpewpew --help`.

**See the Engraving Area**

Call the program from the terminal with `htpewpew -p <engraver port> -d` to have the laser outline the current area where the picture will be engraved on the media.`-p /dev/ttyUSB0` is probably the option you want, unless you have a lot of USB devices attached.

**Move the Engraving Area**

Call the program with `htpewpew -p <engraver port> -x <how much to move the area horizontally (negative values are left and positive values are right)> -y <how much to move the area vertically (negative values are down and positive values are up)>`.

**Engrave a Greyscale Image**

Call the program from the terminal with `htpewpew <image file> -p <engraver port>`.

**Change How Long the Laser Burns Each Pixel**

Call the program from the terminal with `htpewpew -p <engraver port> -b <time in milliseconds to spend on each pixel>`.

**Change the Intensity or Power Output of the Laser**

Call the program from the terminal with `htpewpew -p <engraver port> -i <power output (0 to 10)>`.

**Output the Finale Image Sent to the Engraver**

Call the program from the terminal with `htpewpew <image file> -p <engraver port> -o <directory to save the image file>`.

**Engrave an Image Only in Black and White Not Greyscale**

Call the program from the terminal with `htpewpew <image file> -p <engraver port> -t <percent of white/black range to change to black>`. 

<!-- I may misunderstand how we intend to do this program but based on what it looks like right now I think we should change it. I feel like we should call the program with a serial port passed to it and then the program sits and waits for user input until it gets an image and the go to start engraving. Once the engraving has begun the user can't send anymore commands. Once its done the program spits out a completion status and goes back to waiting for an image to cut and accept changes to settings. -->

### Design Considerations

<!-- List any considerations that affected your design, for example functions you considered but cannot do because of time or system limitations, design decisions made because of customer requirements, etc. -->

The most important requirement was that the program work in Linux. This affected our design decision to code in C++ since it works well in Linux and will be more portable across all its distributions. C++ is also the language we as a team have the most experience programming in, which further affected our decision to write the program in C++. 

We chose not to make a graphical user interface for the program. One reason we made this decision was because none of us have any experience in making GUIs, so we would have to put a lot of time into making one which could spent adding more features instead. Also our customer is very familiar with terminal based programs and not having a GUI in favor of more options in the program is an acceptable trade. 

We have also considered adding more functionality than what the current Super Carver program does. Currently the engraver starts at the top left of the image and engraves left to right moving down. There is no real optimization of the cutting path. Depending on how much time remains after we deliver all of the base functionalities we may looking at adding options to optimize the cutting path. The important thing to note is that there is unlikely to be a one size fits all algorithm for optimization, so the idea would be to offer a few different options for optimization and the user can experiment to see what works best for their image.

### Sizing Estimate

Based on the modules in the above data flow diagram we estimated how many lines of code each module will require.

#### Size in Lines of Code

150 Command Line Parser

100 Protocol Definitions

300 Image Preparation

* 100 Resize
* 100 Greyscale
* 100 Threshold for Monochrome

500 Streamer
<hr/>
1050 Total Lines of Code
