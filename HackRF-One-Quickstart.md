## Summary
This document will step you through the process of setting up a HackRF One device with your computer.  A few examples follow to get you pointed in the right direction.

## Setup
The first thing you will need is a computer with a recent version of Linux.  These instructions were written and tested for both Ubuntu 12.04LTS and Ubuntu 14.04LTS.  You will also need to be familiar with terminal use.

**Preparing Your System**

First things first, make sure all your current software is up to date<br>
`$sudo apt-get update`<br>
`$sudo apt-get upgrade -y`

**Installing GNU Radio**

1. Create a directory to hold all the files needed to build the supporting software. In this example we will create a directory called **hackrf_files** under our home folder:<br>
`$mkdir ~/hackrf_files`
2. Download a copy of Marcus D. Leech's fantastic GNU radio setup script.  You can find it here:<br> http://www.sbrac.org/files/build-gnuradio
3. Save the script to ~/hackrf_files/build-gnuradio.sh
4. Give the script execution permission<br>
`$chmod 744 ~/hackrf_files/build-gnuradio.sh`
5. Execute the script using ~/hackrf_files/build-gnuradio.sh and follow the prompts<br>**WARNING: This step may very well take a few hours to complete!**

**Installing HackRF Tools**

If you used the above steps to install GNU Radio, simply do the following to build and install the HackRF tools:<br>
`$cd ~/hackrf_files/hackrf/host/hackrf-tools && mkdir build && cd build && cmake .. && make && sudo make install`

## Examples
**Testing the HackRF**

1. Plug in the HackRF
2. run the hackrf_info command<br>
`$hackrf_info`

If everything is OK, you should see something similar to the following:

> Found HackRF board.<br>
> Board ID Number: 2 (HackRF One)<br>
> Firmware Version: git-#######<br>
> Part ID Number: 0x######## 0x########<br>
> Serial Number: 0x######## 0x######## 0x######## 0x########<br>

**FM Radio Example**

This Example was derived from the following works:
* [RTL-SDR FM radio receiver with GNU Radio Companion](http://www.instructables.com/id/RTL-SDR-FM-radio-receiver-with-GNU-Radio-Companion/) 
* [How To Build an FM Receiver with the USRP in Less Than 10 Minutes](https://www.youtube.com/watch?v=KWeY2yqwVA0)
<br><br>

1. [Download the FM Radio Receiver python file here](https://raw.githubusercontent.com/rrobotics/hackrf-tests/master/fm_radio/fm_radio_rx.py)
2. Run the file <br>
`$python ./fm_radio_rx.py`
3. [You can find the GNU Radio Companion source file here](https://raw.githubusercontent.com/rrobotics/hackrf-tests/master/fm_radio/fm_radio_rx.grc)

For more information please refer to the [Getting Started with HackRF and GNU Radio](https://github.com/mossmann/hackrf/wiki/Getting-Started-with-HackRF-and-GNU-Radio) wiki page.

