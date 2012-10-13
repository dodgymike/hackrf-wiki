If you are interested in helping with any of these tasks, coordinate with the person in parentheses.  Try IRC first, then email.

## Firmware

* complete USB/SGPIO implementation (jboone)
* rework libopencm3 header files with scripts and csv files (jboone)
* add more register field csv files to libopencm3 (mossmann)
* create various drivers for LPC43xx peripherals (jboone)
* add LPC43xx support to blackmagic debugger (gsmcmullin)
* improve the Si5351C driver (mossmann)

## Host Code

* clean up and automate USB DFU method for loading firmware (mossmann)
* create libhackrf (jboone)
  * depends on USB implementation in firmware
* create GNU Radio blocks (horizon)
  * depends on libhackrf
* osmosdr integration (horizon)
  * depends on GNU Radio blocks
* create command-line utilities (jboone)
  * depends on libhackrf

## Hardware

* fix RX baseband voltage drift (mossmann)
* build Jawbreakers for core developers (mossmann)
* initiate manufacturing of Jawbreakers for beta testers (mossmann)

## Documentation

* create user documenation (mossmann)