Fill in this page so that people know what you are working on:

# mossmann:
* Testing Lollipop
* trying to get LPC43xx working with blackmagic debugger
* building (second rev) Lollipops (PCBs to be ordered shortly)
* designing Bubblegum (alternative wideband front-end design)

# bvernoux:
The draft/proposal will be in github.com/TitanMKD/hackrf and github.com/TitanMKD/libopencm3.
* Add SCU PinMux function.
   * Configure all GPIO with SCU PinMux function in JellyBean Init Code => In progress
* Special Linker + Startup to Copy Code from SPIFI to SRAM at Boot and execute code in SRAM
   * Done see blinky_SPIFI_SRAM: Wait Feedback.
   * To be added in libopencm3.
* Performance tests (nb MIPS) code executed from SPIFI and SRAM (done).
* Work on non documented features found in LPC43xx ROM (Init stuff, SPIFI internals, USB drivers, other stuff hidden, work in progress).
* Dual core M4 & M0 working in parallel (work fine on JellyBean, work in progress to include it in libopencm3).
* Driver SysTick+Interrupt (done), SSP (basic driver done), UART(basic driver done), DMA (in progress), SPI(todo low priority see SSP) (libopencm3).

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