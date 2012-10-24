If you are interested in helping with any of these tasks, coordinate with the person in parentheses.  Try IRC first, then email.

## Firmware

* complete USB/SGPIO implementation (jboone)
  * Initial pass complete, but interrupt-driven SGPIO performance will prevent us from reaching 20MSamples/sec. Plan is to rewrite as a tight loop running on the Cortex-M0.
* rework libopencm3 header files with scripts and csv files (jboone)
* add more register field csv files to libopencm3 (mossmann)
* create various drivers for LPC43xx peripherals (jboone)
* add LPC43xx support to blackmagic debugger (gsmcmullin)
* improve the Si5351C driver (mossmann)

## Host Code

* clean up and automate USB DFU method for loading firmware (mossmann)
  * May not be necessary if we avoid USB boot by default.
  * Automation in firmware/common/Makefile_inc.mk might be sufficient?
* create libhackrf (jboone)
  * created, but more API functions required to be considered complete.
* create GNU Radio blocks (horizon)
  * depends on libhackrf
* osmosdr integration (horizon)
  * depends on GNU Radio blocks
* create command-line utilities (jboone)
  * created, but more functions required to be considered complete.

## Hardware

* fix RX baseband voltage drift (mossmann)
* build Jawbreakers for core developers (mossmann)
* initiate manufacturing of Jawbreakers for beta testers (mossmann)

## Documentation

* create user documentation (mossmann)