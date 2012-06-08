Fill in this page so that people know what you are working on:

# mossmann:
* Putting bvernoux's SSP driver and willcode4's MAX2837 driver together to build some test programs
* trying to get LPC43xx working with blackmagic debugger
* building Lollipops (PCBs to arrive any day now)
* LPC43xx register definitions in libopencm3 (mostly done but will add more as needed)

# bvernoux:
The draft/proposal will be in github.com/TitanMKD/hackrf and github.com/TitanMKD/libopencm3.
* Modify the actual project to use libopencm3 
* Add SCU PinMux function.
   * Configure all GPIO with SCU PinMux function in JellyBean Init Code => In progress
* Special Linker + Startup to Copy Code from SPIFI to SRAM at Boot and execute code in SRAM
   * Done see blinky_SPIFI_SRAM: Wait Feedback.
   * To be added in libopencm3.
* Driver SSP, SPI and USART (libopencm3).

# willcode4:
* MAX2837 driver

# Ideas:
* LPC43xx drivers(libopencm3):
  * SSP, SPI, I2C, USART.
  * Specialized driver SGPIO Logic Analyzer(not really linked to SDR stuff except for debug purpose).
* Lemondrop Drivers:
  * Proper driver for Si5351c (requires LPC43xx I2C driver).
  * Driver for MAX5864 (requires LPC43xx SPI/SSP driver).
* Boot through USB0 in HighSpeed Mode => Will require a PC software (maybe using libusb for Windows/Linux) to Upload Code in JellyBean.
  * would also require 12 MHz clock