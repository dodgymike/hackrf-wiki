# Purpose
This page describes the modifications required to get multiple HackRF hardware-level synchronisation working. Synchronisation is required for many applications where a single HackRF isn't sufficient:
* phase correlation
* oversampling using multiple devices
* 40MHz (or more) wifi

The HackRFs will start transmitting USB packets at the same time, which results in an inter-device offset of ~50 samples at a sample rate of 20MSps. Without this synchronisation, the offset is in the range of thousands to tens of thousands of samples. This is due to the USB start command being called sequentially for each device, along with USB buffering, OS-level timing etc. 

**BE WARNED** you will have to open your HackRFs, which is most likely going to destroy the plastic case it comes in. You will also be electrically connecting them together. If you do this incorrectly, there is a good chance one or all of the devices will be permanently destroyed.

# Requirements
For this to work you will need:
* at least two devices
* a clock sync cable
* some connecting cables (pin header-type)
* a breadboard

You will also need the standard requirements such as antenna and USB cable.

# Opening your HackRF
The HackRF case has small plastic clips holding it in place. These are usually **destroyed** when the case is opened. Please follow the instructions in [this video](https://www.youtube.com/watch?v=zuXJtpTSEJM) by [Jared Boone](https://twitter.com/sharebrained).

# Connect the clocks
Connecting the HackRF clocks together will force them to sample at precisely the same rate. The individual samples will most likely be sampled at slightly different time due to phase offsets in the clock ICs, but for most purposes this is acceptable.

Choose a **primary** HackRF, and connect the clock sync cable from the _clock out_ connector to the _clock in_ connector of the **second** HackRF. If you're using another HackRF, connect the **second** HackRF's _clock out_ to the **third** HackRF's _clock in_.

Your HackRFs should look like this:
[[https://raw.githubusercontent.com/dodgymike/hackrf-wiki/master/images/hackrf-clock-sync.jpg]]

# Identify the pin headers
Firstly, this has only been tested on official HackRF Ones. If you have a jawbreaker, HackRF blue or another HackRF-inspired device, you will have to figure out how to connect the devices correctly, using the schematics.

The hackrf has four pin headers, three of which are arranged in a 'C' shape. On the board these are marked as _P28_, _P22_ and _P20_. _P20_ is the header closest to the _clock in_/_clock out_ connectors. For this exercise we will only be discussing _P20_. The [hackrf schematics](https://github.com/mossmann/hackrf/tree/master/hardware/hackrf-one) are a very good reference for this activity. The relevant part can been seen in the following image:

[[https://raw.githubusercontent.com/dodgymike/hackrf-wiki/master/images/hackrf-pin-headers.jpg]]

This is the P20 schematic diagram:
[[https://raw.githubusercontent.com/dodgymike/hackrf-wiki/master/images/hackrf-pin-headers-p20.png]]


# Wire up the pin headers
As mentioned before **BE WARNED**, this step could easily result in **one or all** of your HackRFs being **permanently damaged**. If you care about your SDRs more than your cats/children/spouse (like I do), **don't do this**!

Now that's out of the way, let me describe what we're doing here. The first part of this exercise is to give both devices a common ground. This is really important for any inter-device electrical connections, as it prevents ICs from seeing slight differences in the respective GND levels as legitimate signals. As shown on the schematic, many of the pins in _P20_ are GND pins. We choose _P20-PIN19_ on both devices and connect them together like so:
[[https://raw.githubusercontent.com/dodgymike/hackrf-wiki/master/images/hackrf-pin-headers-p20-19-gnd.jpg]]

We then need a _positive_ (+5v) connection to 'fake' the _third_ hackrf if it's not present. We choose _Jxx_ from the **primary** hackrf for this, and bring it down to the breadboard. _primary:Jxx_ and _secondary:Jxx_ are _ready_ GPIO pins. Connect these to the breadboard _positive_ line. After this your setup should look like so:
[[images/hackrf-pin-headers-positive.png]]

Next we connect the _primary:Jxx_ _ready_ GPIO pin input to the _secondary:Jxx_ _ready_ GPIO pin output, and the _primary:Jxx_ _ack_ GPIO pin output to the _secondary:Jxx_ ack GPIO pin input. This is the final step, and should look as follows:
[[images/hackrf-pin-headers-ready-ack.png]]


# Upgrade
Now that the hardware is setup, you need to upgrade your HackRFs' firmware, and your _libhackrf_ to at least [v2017.02.1](https://github.com/mossmann/hackrf/releases/tag/v2017.02.1) as per [this wiki page](https://github.com/mossmann/hackrf/wiki/Updating-Firmware).

# Testing with _hackrf_transfer_
The latest version of _hackrf_transfer_ includes the '-H' flag, which will activate hardware synchronisation (via libhackrf via the firmware). Testing this way is a little tricky because _hackrf_transfer_ will time out if it hasn't received any data within one second, and it requires that **two** copies of _hackrf_transfer are running. My approach is to have two terminal windows with the relevant commands waiting, and quickly run them.

This test will fail if:
* your hackrf firmware or _libhackrf_ are out of date
* your connectors are incorrectly set up
* your timing is too slow when running _hackrf_transfer_

Run the following commands within one second of each other:
* `hackrf_transfer -d <device A> -r <filename-A> -H`
* `hackrf_transfer -d <device B> -r <filename-B> -H`

If the test runs correctly, you are 90% of the way there!