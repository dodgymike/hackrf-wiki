## I can't seem to access my HackRF under Linux

### Q:
When running `hackrf_info` or any other command which tries to communicate with the HackRF, I get the following error message, although the board seems to be enumerated properly by the Linux kernel:
```
hackrf_open() failed: HACKRF_ERROR_NOT_FOUND (-5)
```

### A:
First make sure that you are running the latest version of libhackrf and hackrf-tools. HackRF One, for example, is only supported by release 2014.04.1 or newer.  Then check to see if `hackrf_info` is successful when running as root.  If it is, then your other user is lacking permission.

A normal user under Linux doesn't have the permissions to access arbitrary USB devices because of security reasons. The first solution would be to run every command which tries to access the HackRF as root which is not recommended for daily usage, but at least shows you if your HackRF really works.

To fix this issue, you can write a udev rule to instruct udev to set permissions for the device in a way that it can be accessed by any user on the system who is a member of a specific group.

(The following things have been tested on Ubuntu 13.04 and may need to be adapted to other Linux distributions)  
To do that, you need to create a new rules file in the `/etc/udev/rules.d` folder. I called mine `52-hackrf.rules`. Here is the content:

```
ATTR{idVendor}=="1d50", ATTR{idProduct}=="604b", SYMLINK+="hackrf-jawbreaker-%k", MODE="660", GROUP="plugdev"
ATTR{idVendor}=="1d50", ATTR{idProduct}=="6089", SYMLINK+="hackrf-one-%k", MODE="660", GROUP="plugdev"
ATTR{idVendor}=="1fc9", ATTR{idProduct}=="000c", SYMLINK+="hackrf-dfu-%k", MODE="660", GROUP="plugdev"
```

The content of the file instructs udev to look out for devices with Vendor ID and Product ID matching HackRF devices. It then sets the UNIX permissions to `660` and the group to `plugdev` and creates a symlink in `/dev` to the device.

After creating the rules file you can either reboot or run the command `udevadm control --reload-rules` as root to instruct udev to reload all rule files. After replugging your HackRF board, you should be able to access the device with all utilities as a normal user.  If you still can't access the device, make sure that you are a member of the plugdev group.

## hackrf_set_sample_rate fails

### Q:

I'm trying to run `hackrf_transfer` and hackrf_set_sample_rate fails. The libusb_control_transfer call in hackrf_set_sample_rate_manual is returning with LIBUSB_ERROR_PIPE.

### A:

Follow the instructions to [update your firmware](https://github.com/mossmann/hackrf/wiki/Updating-Firmware).

## What is this big spike in the center of my received spectrum?

### Q:

I see a large spike in the center of my FFT display regardless of the frequency my HackRF is tuned to.  Is there something wrong with my HackRF?

### A:

You are seeing a DC offset (or component or bias).  The term "DC" comes from "Direct Current" in electronics.  It is the unchanging aspect of a signal as opposed to the "alternating" part of the signal (AC) that changes over time.  Take, for example, the signal represented by the digital sequence:
```
-2, -1, 1, 6, 8, 9, 8, 6, 1, -1, -2, -1, 1, 6, 8, 9, 8, 6, 1, -1, -2, -1, 1, 6, 8, 9, 8, 6, 1, -1
```
This periodic signal contains a strong sinusoidal component spanning from -2 to 9.  If you were to plot the spectrum of this signal, you would see one spike at the frequency of this sinusoid and a second spike at 0 Hz (DC).  If the signal spanned from values -2 to 2 (centered around zero), there would be no DC offset.  Since it is centered around 3.5 (the number midway between -2 and 9), there is a DC component.

Samples produced by HackRF are measurements of radio waveforms, but the measurement method is prone to a DC bias introduced by HackRF.  It's an artifact of the measurement system, not an indication of a received radio signal.  DC offset is not unique to HackRF; it is common to all quadrature sampling systems.

There was a bug in the HackRF firmware (through release 2013.06.1) that made the DC offset worse than it should have been.  In the worst cases, certain Jawbreakers experienced a DC offset that drifted to a great extreme over several seconds of operation.  This bug has been fixed.  The fix reduces DC offset but does not do away with it entirely.  It is something you have to live with when using any quadrature sampling system like HackRF.

## How do I deal with the DC offset?

### Q:

Okay, now that I understand what that big spike in the middle of my spectrum is, how do I handle it?

### A:

There are a few options:

1. Ignore it.  For many applications it isn't a problem.  You'll learn to ignore it.

2. Avoid it.  The best way to handle DC offset for most applications is to use offset tuning; instead of tuning to your exact frequency of interest, tune to a nearby frequency so that the entire signal you are interested in is shifted away from 0 Hz but still within the received bandwidth.  If your algorithm works best with your signal centered at 0 Hz (many do), you can shift the frequency in the digital domain, moving your signal of interest to 0 Hz and your DC offset away from 0 Hz.  HackRF's high maximum sampling rate can be a big help as it allows you to use offset tuning even for relatively wideband signals.

3. Correct it.  There are various ways of removing the DC offset in software.  However, these techniques may degrade parts of the signal that are close to 0 Hz.  It may look better, but that doesn't necessarily mean that it is better from the standpoint of a demodulator algorithm, for example.  Still, correcting the DC offset is often a good choice.

## Purchasing HackRF

### Q:
Where can I buy HackRF?

### A:
HackRF is designed and manufactured by Great Scott Gadgets.  Please see [http://greatscottgadgets.com/hackrf/](http://greatscottgadgets.com/hackrf/) for availability.  HackRF is open source hardware, so you could also build your own.

## Making sense of gain settings

### Q:
What gain controls are provided by HackRF?

### A:
HackRF (both Jawbreaker and One) provides three different analog gain controls on RX and two on TX.  The three RX gain controls are at the RF (0 or 14 dB), IF (0 to 40 dB in 8 dB steps), and baseband (0 to 62 dB in 2 dB steps) stages.  The two TX gain controls are at the RF (0 or 14 dB) and IF (0 to 47 dB in 1 dB steps) stages.

### Q:
Why is the RF gain setting restricted to two values?

### A:
HackRF has two RF amplifiers close to the antenna port, one for TX and one for RX.  These amplifiers have two settings: on or off.  In the off state, the amps are completely bypassed.  They nominally provide 14 dB of gain when on, but the actual amount of gain varies by frequency.  In general, expect less gain at higher frequencies.  For fine control of gain, use the IF and/or baseband gain options.

### Q:
How should I set the gain controls for RX?

### A:
A good default setting to start with is RF=0 (off), IF=16, baseband=16.  Increase or decrease the IF and baseband gain controls roughly equally to find the best settings for your situation.  Turn on the RF amp if you need help picking up weak signals.  If your gain settings are too low, your signal may be buried in the noise.  If one or more of your gain settings is too high, you may see distortion (look for unexpected frequencies that pop up when you increase the gain) or the noise floor may be amplified more than your signal is.

## System requirements

### Q:
What are the minimum system requirements for using HackRF?

### A:
The most important requirement is that you supply 500 mA at 5 V DC to your HackRF via the USB port.  If your host computer has difficulty meeting this requirement, you may need to use a powered USB hub.

Most users will want to stream data to or from the HackRF at high speeds.  This requires that the host computer supports Hi-Speed USB.  Some Hi-Speed USB hosts are better than others, and you may have multiple host controllers on your computer.  If you have difficulty operating your HackRF at high sample rates (10 Msps to 20 Msps), try using a different USB port on your computer.  If possible, arrange things so that the HackRF is the only device on the bus.

There is no specific minimum CPU requirement for the host computer, but SDR is generally a CPU-intensive application.  If you have a slower CPU, you may be unable to run certain SDR software or you may only be able to operate at lower sample rates.

### Q:
Why doesn't HackRF work properly with a virtual machine (VM)?

### A:
HackRF requires the ability to stream data at very high rates over USB.  Unfortunately VM software typically has problems with continuous high speed USB transfers.

There are some known bugs with the HackRF firmware's USB implementation.  It is possible that fixing these bugs will improve the ability to operate HackRF with a VM, but there is a very good chance that operation at higher sample rates will still be limited.