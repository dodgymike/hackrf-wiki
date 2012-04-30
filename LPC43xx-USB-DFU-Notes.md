# LPC43xx USB DFU Notes

The LPC4350/40/30/20 contain USB DFU bootloader support in their ROM. By selecting the appropriate boot mode (either USB0 or USB1), the device will come up on USB at power-up or reset, and implement the popular and well-documented [USB DFU protocol](http://www.usb.org/developers/devclass_docs/DFU_1.1.pdf).

It appears that the LPC43xx boot ROM will identify the available clock sources and frequencies, to some extent. Unfortunately, the current Jellybean prototype does not offer any high-precision clock source on-board, and the Si5351C (on Lemondrop) does not produce any clock signals by default. So we may not be able to use the USB DFU bootloader until we provide a accurate clock source at power-up. It's possible adding a 32.768KHz watch crystal would provide this without much additional BOM cost?

The April 16, 2012 Jellybean design has a voltage divider for VBUS that is fed to the LPC43xx to detect that a USB host is present. Measuring the divided voltage, the USB0_VBUS only reaches 0.4V, which fails to trip the USB bootloader code. It looks like NXP's intent is to directly connect VBUS to the USB0_VBUS. Indeed, when I shorted R10 with tweezers, the USB bootloader sprung into action. I would recommend changing R10 to 0 Ohms and R11 to DNP, or removing R10 and R11 altogether.

## Setup

### Boot Mode Jumpers

Set the boot mode jumpers to USB0: BOOT[0:3] = "1010". Jumper setting takes effect at the next power-on or reset. (I'll probably rig up a reset button to P2 "LPC_JTAG" or P14 "LPC_ISP".)

### USB DFU Utility
http://dfu-util.gnumonks.org/

