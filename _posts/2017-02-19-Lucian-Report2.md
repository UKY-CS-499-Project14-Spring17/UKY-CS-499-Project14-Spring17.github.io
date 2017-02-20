---
layout: post
tags: hymer
title: Weeks 2-3 Report
---

### Feb. 19, 2017 

This week we were able to attain a working copy of the correct version of the software for our laser engraver.

I first installed wireshark using `sudo apt-get install wireshark` at the terminal.
Then, I launched my VM and opened up the laser engraver software. I used the menus at the top of the VM to enable the correct USB device.
Finally, with the correct version of the software, the laser engraver successfully connected.

To view the data being transferred between the two devices, I first had to figure out which USB device was being used.
I ran `lsusb` at the terminal and saw the QinHeng Serial Device was on bus 3, device 3. Therefore, I knew to use USB bus 3 in wireshark and look for device 3.
To get wireshark to work correctly, I have to run `sudo modprobe usbmon` each time I restart my terminal.

In order to extract data easier for future parsing, I wanted to get the output on the terminal.
I learned about tshark, which I installed with apt-get.
I used the -Y command to apply a read filter, and then requested the desired fields.
It appears that 'leftover data' is the data which is pertinent. The rest of the transferred data is just handling the usb protocol behind the serial connection.

Therefore, to get tshark working, install tshark and do the following:

1. Run `lsusb` and record the pertinent bus and device IDs.
2. Run `modprobe usbmon` to start the usb monitors.
3. Run `tshark -i usbmon<BUSID> -Y 'usb.addr contains "<BUSID>.<DEVID>"' -T fields -e frame.number -e usb.addr -e usb.data_len -e usb.capdata`

So, in my case with device 3.3, I ran:
`tshark -i usbmon3 -Y 'usb.addr contains "3.3"' -T fields -e frame.number -e usb.addr -e usb.data_len -e usb.capdata`

We should be able to easily capture and parse this data so we can start analysis.
