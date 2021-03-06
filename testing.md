---
title: Testing
---

# Testing

### Unit Testing

It is easy to see from the Module Descriptions and Data Flow section of the high level design that we only have about 4 different functional units to test. 

#### The Parser
The Parser code handles translating user input into a format the program can act on. The Parser can be tested on its own by entering in both good and bad input and confirming that it gives the correct error messages on bad input and converts the good input as expected. Since there are so many possible variations of input to the Parser it is one of the more laborious to test. Every single input parameter needs to be tested at least once, but should have several. All of the possible combinations of input parameters also needs to be tested; since that number is too large for practicality, strategic testing of parameters commonly used together will be done instead. Determination of several examples of good but unusual input, as well as bad input is key. Important edge cases to cover are to set settings out of their range, strange special characters (end of file, etc), invalid input (e.g. using both -bw and grayscale), a completely empty input, and a very long input (buffer overflow).

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

System Testing will occur with computers running Ubuntu Linux 16.04 and 14.04, using an HTPOW 1000mW engraver.


### Customer Testing
Customer testing will be performed by our customer, Dr. Dietz, if he deems it necessary. We will walk him through all of our testing and he can ask us to perform more tests or test for himself at his discretion. We expect some basic functionality testing if nothing else to make sure the code meets requirements.



### Unit Tests

#### Image.c

| ID |Test Case| Action | Expected Output | Actual Output |
|---:|:-:|:-:|:-:|:-:|
|throw_wand_ exception_1| Input filename that does not exist. | Call `throw_wand_exception` method after entering a non-existent filename. | Message on stderr ```throw_wand_exception 32 unable to open image``` | Pass |
|throw_wand_ exception_2| Input correct filename. | Call `throw_wand_exception method` after entering a good filename. | No error is issued. Return value is 0. | Pass |
|resize_image_1| Input image with dimensions less than 489x489. | Call `resize_image` method. | Image should not be resized. | Pass |
|resize_image_2| Input image with dimensions greater than 489x489. | Call `resize_image` method. | Image should be scaled. Larger size should be 489px. | Pass |
|resize_image_3| Input image with X dimension only greater than 489. | Call `resize_image` method. | Image should be scaled so that the X dimension is 489px. | Pass |
|resize_image_4| Input image with Y dimension only greater than 489. | Call `resize_image` method. | Image should be scaled so that the Y dimension is 489px. | Pass |
|antialias_1| Input any image. | Call `antialias_image` method. | Line in image should be thickened. | Untested |
|greyscale_1| Input any non black and white image. | Call `greyscale_image` method. | Image should be converted to greyscale. | Untested |
|threshold_1| Input any non black and white image with 50% threshold value. | Call `threshold_image` method. | Image should be converted to black and white appropriately. | Pass |
|threshold_2| Input any non black and white image with 0% threshold value. | Call `threshold_image` method. | Image should be converted to all white. | Pass |
|threshold_3| Input any non black and white image with 100% threshold value. | Call `threshold_image` method. | Image should be converted to all black. | Pass |
|prepare_1| Input is not a file. | Call `prepare_image` method. | Message on stderr ```throw_wand_exception 32 unable to open image``` | Pass |
|prepare_2| Input is not an image file. | Call `prepare_image` method. | Message on stderr ```throw_wand_exception 32 unable to open image``` | Pass |
|prepare_3| threshold input equal to -1. | Call `prepare_image` method. | Calls greyscale on the image. | Pass |
|prepare_4| Outfile input. | Creates an output file at output.jpg. | Call `prepare_image` method. | Pass |
|prepare_5| No outfile input. | Call `prepare_image` method. | Does not create an output file. | Pass |
|cleanup_1| Input any wand. | Call `cleanup_image` method. | Deallocates wand. | (untested) |


#### cli.c

| ID |Test Case| Action | Expected Output | Actual Output |
|---:|:-:|:-:|:-:|:-:|
|cli_1| Make sure verbose and silent options can't be used at the same time. | Call verbose function followed by silent function. | Print error message to the user. | Pass
|cli_2| Make sure verbose and silent options can't be used at the same time. | Call silent function followed by verbose function. | Print error message to the user. | Pass
|cli_3| Make sure silent option silences messages. | Call silent function followed by fmsg function. | There should be no output. | Pass
|cli_4| Make sure silent option silences notes. | Call silent function followed by fnote function. | There should be no output. | Pass
|cli_5| Make sure verbose option activates notes. | Call verbose function followed by fnote function. | The fnote message should be printed with appropriate formatting. | Pass
|cli_6| Make sure fwarn prints to stderr with formatting. | Call fwarn function. | The fwarn message should be printed with appropriate formatting. | Pass
|cli_7| Make sure ferr prints to stderr with formatting. | Call ferr function. | The ferr message should be printed with appropriate formatting. | Pass


#### pixelator.c

| ID |Test Case| Action | Expected Output | Actual Output |
|---:|:-:|:-:|:-:|:-:|
|center_pixel_1| Call with NULL pixel pointer. | Call `center_pixel` method. | Call pixel_exception function to stop engraving and report error to user. | Pass |
|center_pixel_2| Call with pixel that is too big. | Call `center_pixel` method. | Call pixel_exception function to stop engraving and report error to user. | Fail (does not check bounds) |
|center_pixel_3| Call with a normal pixel. | Call `center_pixel` method. | Function executes normally by adjusting the pixel value appropriately. | Pass |
|get_pixel_ intensity_1| Input a white pixel. | Call `get_pixel_intensity` method. | Returns with an intensity value of 0. | Fail (antialiasing issue) |
|get_pixel_ intensity_2| Input a grey pixel. | Call `get_pixel_intensity` method. | Returns with an appropriate intensity value between 1 and 254. | Pass |
|get_pixel_ intensity_3| Input a black pixel. | Call `get_pixel_intensity` method. | Returns with an intensity value of 255. | Fail (antialiasing issue) |
|get_pixel_ intensity_4| Input with a NULL pixel pointer. | Call `get_pixel_intensity` method. | Call pixel_exception function to stop engraving and report error to user. | Pass |
|pixelator_ init_1| Call with NULL wand pointer. | Call `pixelator_init` method. | Call pixel_exception function to stop engraving and report error to user. | Pass |
|top_left_1| Call with NULL pixel_state pointer. | Call `get_top_left_pixel` method. | Call pixel_exception function to stop engraving and report error to user. | Pass |
|top_left_2| Call with NULL wand pointer. | Call `get_top_left_pixel` method. | Call pixel_exception function to stop engraving and report error to user. | Pass |
|top_left_3| Call with an all white image. | Call `get_top_left_pixel` method. | Returns the bottom right corner. | Pass |
|top_left_4| Call with normal image. | Call `get_top_left_pixel` method. | Returns correct top left pixel in image. | Pass |
|bottom_right_1| Call with NULL pixel_state pointer. | Call `get_bottom_right_pixel` method. | Call pixel_exception function to stop engraving and report error to user. | Pass |
|bottom_right_2| Call with NULL wand pointer. | Call `get_bottom_right_pixel` method. | Call pixel_exception function to stop engraving and report error to user. | Pass |
|bottom_right_3| Call with an all white image. | Call `get_bottom_right_pixel` method. | Returns the top left pixel. | Pass |
|bottom_right_4| Call with normal image. | Call `get_bottom_right_pixel` method. | Returns correct bottom right pixel in image. | Pass |
|get_next_1| Call with NULL pixel_state pointer. | Call `get_next_pixel` method. | Call pixel_exception function to stop engraving and report error to user. | Pass |
|get_next_2| Call with NULL wand pointer. | Call `get_next_pixel` method. | Call pixel_exception function to stop engraving and report error to user. | Pass |
|get_next_3| Call with NULL pixel pointer. | Call `get_next_pixel` method. | Completes normally by returning the next pixel. | Fail |
|get_next_4| Call with NULL iterator. | Call `get_next_pixel` method. | Completes normally by returning the next pixel. | Fail |
|get_next_5| Call with next pixel not being a white pixel. | Call `get_next_pixel` method. | Completes normally by returning the next pixel. | Fail |
|get_next_6| Call with next pixel being a white pixel. | Call `get_next_pixel` method. | Completes normally by setting pixel and iterator to NULL. | Pass |


#### main.c

| ID |Test Case| Action | Expected Output | Actual Output |
|---:|:-:|:-:|:-:|:-:|
|parse_veb_1| Make sure blank input doesn't error. | Call parse_verbose with blank input. | Print interactive shell message to user. | Pass
|parse_veb_2| Make sure verbose option enables fnotes. | Call parse_verbose with verbose option. | Print messages to stdout. | Pass
|parse_veb_3| Make sure silent option disables fnotes. | Call parse_verbose with silent option. | Print warning to stderr about silencing notes. | Pass
|parse_veb_4| Make sure verbose and silent can't be called at the same time. | Call parse_verbose with both silent and verbose options. | Print an error to stderr and exit the program. | Pass
|parse_opts_1| Make sure burn time is set correctly. | Call parse_opts with burn time option set to a positive value. | Value changed and note printed to user. | Pass
|parse_opts_2| Make sure burn times greater than 250 are caught. | Call parse_opts with burn time option out of positive range. | Print acceptable range to user and exit. | Pass
|parse_opts_3| Make sure burn times less than 1 are caught. | Call parse_opts with burn time option set to a negative value. | Print acceptable range to user and exit. | Pass
|parse_opts_4| Make sure dry run is enabled when used. | Call parse_opts with dry run option. | Prints enabled message. | Pass
|parse_opts_5| Make sure intensity is set correctly. | Call parse_opts with intensity option set to a positive value. | Value changed and note printed to user. | Pass
|parse_opts_6| Make sure intensity values greater than 10 are caught. | Call parse_opts with intensity option out of positive range. | Print acceptable range to user and exit. | Pass
|parse_opts_7| Make sure intensity values less than 1 are caught. | Call parse_opts with intensity option set to a negative value. | Print acceptable range to user and exit. | Pass
|parse_opts_8| Make sure output file name is set correctly. | Call parse_opts with output option. | Print a note to the user and set outfile. | Pass
|parse_opts_9| Make sure port is set correctly. | Call parse_opts with port option. | Print a note to the user and set port. | Pass
|parse_opts_10| Make sure threshold value is set correctly. | Call parse_opts with black and white option set to a positive value. | Print a note to the user and set the threshold value. | Pass
|parse_opts_11| Make sure threshold values out of range are caught. | Call parse_opts with black and white option out of positive range. | Print acceptable range to user and exit. | Pass
|parse_opts_12| Make sure threshold values less than 0 are caught. | Call parse_opts with black and white option set to a negative value. | Print acceptable range to user and exit. | Pass
|parse_opts_13| Make sure x-offset is set correctly. | Call parse_opts with x-offset option set to a positive value. | Print a note to the user and set the x-offset value. | Pass
|parse_opts_14| Make sure x-offset values greater than 250 are caught. | Call parse_opts with x-offset option out of positive range. | Print acceptable range to user and exit. | Pass
|parse_opts_15| Make sure x-offset values less than -250 are caught. | Call parse_opts with x-offset option out of negative range. | Print acceptable range to user and exit. | Pass
|parse_opts_16| Make sure y-offset is set correctly. | Call parse_opts with y-offset option set to a positive value. | Print a note to the user and set the y-offset value. | Pass
|parse_opts_17| Make sure y-offset values greater than 250 are caught. | Call parse_opts with y-offset option out of positive range. | Print acceptable range to user and exit. | Pass
|parse_opts_18| Make sure y-offset values less than -250 are caught. | Call parse_opts with y-offset option out of negative range. | Print acceptable range to user and exit. | Pass
|parse_opts_19| Make sure verbose option is skipped by parse_opts. | Call parse_opts with verbose option. | Nothing is printed. | Pass
|parse_opts_20| Make sure silent option is skipped by parse_opts. | Call parse_opts with silent option. | Nothing is printed. | Pass


#### streamer.c

|ID | Test Case | Action | Expected Output | Actual Output |
|---: | :-: | :-: | :-: | :-: |
|stream_1 | The pixelator is not initialized | Call with NULL pixelator_state pointer. | Error message on stderr | Error message on stderr 
|send_pixel_command_1 | There is no pixel to send | Call with NULL pixel pointer. | Warning message on stderr | Warning message on stderr 
|send_pixel_command_2 | The pixelator is not initialized | Call with NULL pixelator_state pointer. | Error message on stderr | Error message on stderr 
|send_pixel_command_3 | Normal operation | Call with a good pixel pointer. | Sends carve pixel command to streamer file handle | Sends carve pixel command to streamer file handle 
|get_next_pixel_count_1| The pixelator is not initialized | Call with NULL pixelator_state pointer. | Error message on stderr | Error message on stderr 
|get_next_pixel_count_2| The streamer is sending the first pixel (Normal operation) | Call with value 0x3d. | 0x3e | 0x3e 
|get_next_pixel_count_3| The streamer needs to reset the count | Call with value 0x78. | 0x3d | 0x3d 
|get_next_pixel_count_4| Called with an invalid pixel count | Call with value out of the range 0x3d - 0x78. | Error message on stderr | Error message on stderr 
|initialize_carver_1 | The pixelator is not initialized | Call with NULL pixelator_state pointer. | Error message on stderr | Error message on stderr 
|initialize_carver_2 | Normal operation | Call with valid pixelator_state pointer. | Sends initialization commands to streamer file handle | Sends initialization commands to streamer file handle
|carve_image_1 | The pixelator is not initialized | Call with NULL pixelator_state pointer. | Error message on stderr | Error message on stderr 
|carve_image_2 | There are no pixels to send | Call with NULL pixel pointer. | Warning message on stderr | Warning message on stderr 
|finalize_1 | The pixelator is not initialized | Call with NULL pixelator_state pointer. | Error message on stderr | Error message on stderr 
|finalize_2 | Normal operation | Call with valid pixelator_state pointer. | Sends initialization commands to streamer file handle | Sends initialization commands to streamer file handle
|init_serial_1 | Normal operation, no user supplied port | Call with NULL option set for the port. | Returns MODEMDEVICE filehandle | Returns MODEMDEVICE filehandle 
|init_serial_2 | Normal operation, user supplied port | Call with valid port set for the port option. | Returns positive integer (filehandle) | Returns positive integer (filehandle) 
|init_serial_3 | Invalid user supplied port | Call with invalid port set for the port option. | Error message on stderr | Error message on stderr 
|send_1 | The pixelator is not initialized | Call with NULL pixelator_state pointer. | Error message on stderr | Error message on stderr 
|send_2 | Bad command buffer pointer | Call with NULL buffer pointer. | Error message on stderr | Error message on stderr 
|wait_1 | The pixelator is not initialized | Call with NULL pixelator_state pointer. | Error message on stderr | Error message on stderr 
