---
title: Testing
---

# Testing

### Unit Testing

It is easy to see from the Module Descriptions and Data Flow section of the high level design that we only have about 4 different functional units to test. 

#### The Parser
The Parser code handles translating user input into a format the program can act on. The Parser can be tested on its own by entering in both good and bad input and confirming that it gives the correct error messages on bad input and converts the good input as expected. Since there are so many possible variations of input to the Parser it is one of the more laborious to test. Every single input parameter needs to be tested at least once, but should have several. All of the possible combinations of input parameters also needs to be tested; but, since that number is too large for practicality, strategic testing of parameters commonly used together will be done instead. Determination of several examples of good but unusual input, as well as bad input is key. Important edge cases to cover are to set settings out of their range, strange special characters (end of file, etc), invalid input (e.g. using both -bw and grayscale), a completely empty input, and a very long input (buffer overflow).

#### Image Magick
Image Magick is the section of code that reformats input images into a size and form the Streamer can send to the engraver. It is composed of 3 smaller units: Resizing, Greyscale Conversion, and Thresholding. 

Resizing an image can easily be tested by inputting a wide range of image sizes and making sure it always resizes as expected. For larger images they must always be scaled down, and images that are already the exact size for the engraver or smaller should not be changed at all.

Greyscale Conversion is checked in a similar way to resizing, except that the input has to consist of images of varying colors. Both full color images, greyscale images, and black and white images should be input to the unit and their outputs confirmed to be as expected. 

The Threshold unit changes every pixel into a black or white pixel based on a threshold value. This unit has more variability to test than the others since it needs to be tested with several images and several threshold values. The output from each unit's tests will have to be inspected manually for compliance. 

Once they are all put together in Image Magick, the testing is essentially the same. The same images will need to be run through again, but some additional images that are touched by every unit will also need to be selected to make sure that the combination of all 3 iterative changes works as expected. A few good edge cases for all of the units would be an image of size 0, an all white image, an all black image, and a non-image file.

#### Streamer
The Streamer is responsible for sending the right instructions to the engraver. The Streamer can be tested by manually giving it the type of input it is looking for and confirming that it sends the correct bytes for the instruction. Erroneous input should also be given to make sure the Streamer fails gracefully. The Streamer must also be tested to make sure it establishes the serial communication successfully every time. This can be tested by setting up an Arduino or another computer to mirror whatever information it receives and then make sure the Streamer can send and receive information.

#### Protocol Definitions
Protocol Definitions is literally just a header file that contains the constants for the program, including all of the op-code numbers for the instructions to the engraver. This can only really be checked manually, but since the Streamer relies on it for every instruction it will also be tested when testing the Streamer.


### Integration and System Testing
Once all 4 units are tied together the testing doesn't change much. Essentially the same tests that were done for the Parser need to be ran again, but this time they have to be confirmed to come out of the Streamer correctly. The images tested for the Image Magick unit must also be tested again, but again the correct output is checked out of the Streamer. Some extra tests that could be done at this point are to quit in the middle of execution or trying to input more while the program is already streaming instructions.

Once the program is actually connected to the engraver all of the same tests apply as in integration testing, but a few more can also be added. The case when the engraver is powered down or the communication connection pulled while the program is sending instructions.


### Customer Testing
Customer testing will be performed by our customer, Dr. Dietz, if he deems it necessary. We will walk him through all of our testing and he can ask us to perform more tests or test for himself at his discretion. We expect some basic functionality testing if nothing else to make sure the code meets requirements.

