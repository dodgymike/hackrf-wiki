# Purpose
This page describes the modifications required to get multiple device hardware-level synchronisation working. Synchronisation is required for many applications where a single device isn't sufficient:
* phase correlation
* oversampling using multiple devices
* 40MHz (or more) wifi

The devices will start transmitting USB packets at the same time, which results in an inter-device offset of ~50 samples at a sample rate of 20MSps. Without this synchronisation, the offset is in the range of thousands to tens of thousands of samples. This is due to the USB start command being called separately on each device, along with USB buffering, OS-level timing etc. 

**BE WARNED** you will have to open your devices, and will be connecting them together. If you do this incorrectly, there is a good chance one or all of the devices will be permanently destroyed.

# Requirements
For this to work you will need at least two devices, a clock sync cable, some connecting wires and a breadboard, in addition to the obvious (antenna, USB cables).