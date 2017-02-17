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
Connecting the hackrf clocks together will force them to sample at precisely the same rate. The individual samples will most likely be sampled at slightly different time due to phase offsets in the clock, but for most purposes this is acceptable.

Choose a **primary** hackrf, and connect the clock sync cable from the __clock out__ connector to the __clock in__ connector of the **second** hackrf. If you're using another hackrf, connect the **second** hackrf's __clock out__ to the **third** hackrf's __clock in__
