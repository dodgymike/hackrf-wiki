# Purpose
This page describes the modifications required to get multiple hackrf hardware-level synchronisation working. Synchronisation is required for many applications where a single hackrf isn't sufficient:
* phase correlation
* oversampling using multiple devices
* 40MHz (or more) wifi

The hackrfs will start transmitting USB packets at the same time, which results in an inter-device offset of ~50 samples at a sample rate of 20MSps. Without this synchronisation, the offset is in the range of thousands to tens of thousands of samples. This is due to the USB start command being called sequentially for each device, along with USB buffering, OS-level timing etc. 

**BE WARNED** you will have to open your hackrfs, which is most likely going to destroy the plastic case it comes in. You will also be electrically connecting them together. If you do this incorrectly, there is a good chance one or all of the devices will be permanently destroyed.

# Requirements
For this to work you will need:
* at least two devices
* a clock sync cable
* some connecting cables (pin header-type)
* a breadboard
You will also need the standard requirements such as antenna and USB cable.

# Opening your hackrf
The hackrf case has small plastic clips holding it in place. These are usually **destroyed** when the case is opened. Please follow the instructions in [this video](https://www.youtube.com/watch?v=zuXJtpTSEJM) by [Jared Boone](https://twitter.com/sharebrained).

# Connect the clocks
Connecting the hackrf clocks together will force them to sample at precisely the same rate. The individual samples will most likely be sampled at slightly different time due to phase offsets in the clock ICs, but for most purposes this is acceptable.

Choose a **primary** hackrf, and connect the clock sync cable from the _clock out_ connector to the _clock in_ connector of the **second** hackrf. If you're using another hackrf, connect the **second** hackrf's _clock out_ to the **third** hackrf's _clock in_.

Your hackrfs should look like this:
[[images/clock-sync-cables.png]]

# Identify the pin headers
Firstly, this has only been tested on official hackrfs. If you have a jawbreaker, or another hackrf-inspired device, you will have to figure out how to connect the devices correctly from the schematics.

The hackrf has four pin headers, three of which are arranged in a 'C' shape. On the board these are marked as _P28_, _P22_ and _P20_. _P20_ is the header closest to the _clock in_/_clock out_ connectors. For this exercise we will only be discussing _P20_. 

# Wire up the pin headers
As mentioned before **BE WARNED**, this step could easily result in **one or all** of your hackrfs being permanently damaged. If you care about your SDRs more than your cats/children/spouse (like I do), **don't do this**!

Now that's out of the way, let me describe what we're doing here. The first part of this exercise is to give both devices a common ground. This is really important for any inter-device electrical connections, as it prevents ICs from seeing slight differences in the negative values as legitimate signals.