## Try Your HackRF with Pentoo Linux

The easiest way to get started with your HackRF and ensure that it works is to use Pentoo, a Linux distribution with full support for HackRF and GNU Radio.  Download the latest Pentoo .iso image from one of the mirrors listed at [http://pentoo.ch/download/](http://pentoo.ch/download/).  Then burn the .iso to a DVD or use [UNetbootin](http://unetbootin.sourceforge.net/) to install the .iso on a USB flash drive.  Boot your computer using the DVD or USB flash drive to run Pentoo.  Do this natively, not in a virtual machine.  (Unfortunately high speed USB operation invariably fails when people try to run HackRF from a virtual machine.)

Once Pentoo is running, type `startx` at the command line to launch the desktop environment.  Accept the "default config" in the first dialog box and then launch a Terminal Emulator window using the icon at the bottom of the screen.

At the time of writing, the current Pentoo .iso (2014.0-RC3) has a minor bug that you need to work around by typing `eselect lapack set 1` at the command line in the terminal window before trying to use GNU Radio.  You only need to do this once after starting up Pentoo, but you'll have to do it every time you boot an unmodified .iso.

To verify that your HackRF is detected, type `hackrf_info` at the command line.  It should produce a few lines of output including "Found HackRF board."  The 3V3, 1V8, RF, and USB LEDs should all be illuminated and are various colors.

Now you can use programs such as gnuradio-companion or gqrx to start experimenting with your HackRF.  Try the Examples below.  If you are new to GNU Radio, an excellent place to start is with the [guided tutorials](http://gnuradio.org/redmine/projects/gnuradio/wiki/Guided_Tutorials).

## Software Setup

As mentioned above, the best way to get started with HackRF is to use Pentoo Linux.  Eventually you may want to install software to use HackRF with your favorite operating system.

If your package manager includes the most recent release of libhackrf (2014.04.1 at the time of writing) and gr-osmosdr, then use it to install those packages in addition to GNU Radio.  Otherwise, the recommended way to install these tools is by using [PyBOMBS](http://gnuradio.org/redmine/projects/pybombs/wiki).

See the [Operating System Tips](https://github.com/mossmann/hackrf/wiki/Operating-System-Tips) page for information on setting up HackRF software on particular Operating Systems and Linux distributions.

If you have any trouble, make sure that things work when booted to Pentoo.  This will allow you to easily determine if your problem is being caused by hardware or software, and it will give you a way to see how the software is supposed to function.

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

## Getting Help

Please subscribe to the [HackRF-dev mailing list](http://nine.pairlist.net/mailman/listinfo/hackrf-dev).  This is the preferred place for questions about HackRF.  Be sure to check the [FAQ](https://github.com/mossmann/hackrf/wiki/FAQ) and other [documentation](https://github.com/mossmann/hackrf/wiki) before asking questions.  Additionally, you may want to join the #hackrf IRC channel on [freenode](http://freenode.net/).  Specific bugs and feature requests may be added to the [Issues List](https://github.com/mossmann/hackrf/issues?direction=desc&sort=updated&state=open) though they should probably be discussed on the mailing list or IRC first.