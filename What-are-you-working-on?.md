Fill in this page so that people know what you are working on:

mossmann:
* LPC43xx register definitions in libopencm3
* Lollipop hardware design revisions (PCBs to be assembled soon)

bvernoux ideas:
* LPC43xx drivers(libopencm3):
  * SSP, SPI, I2C, USART.
  * Specialized driver SGPIO Logic Analyzer(not really linked to SDR stuff except for debug purpose).
* Lemondrop Drivers:
  * Driver for SI5351 (requires LPC43xx I2C driver).
  * Driver for MAX5864 (requires LPC43xx SPI driver).
  * Driver for MAX2837 (requires LPC43xx SPI driver).
* Boot through USB0 in HighSpeed Mode => Will require a PC software (maybe using libusb for Windows/Linux) to Upload Code in JellyBean.

bvernoux:
The draft/proposal will be in github.com/TitanMKD/hackrf and github.com/TitanMKD/libopencm3.
* Modify the actual project to use libopencm3 
* Add SCU PinMux function.
   * Configure all GPIO with SCU PinMux function in JellyBean Init Code.
   * To use 
* Special Linker + Startup to Copy Code from SPIFI to SRAM at Boot and execute code in SRAM
   * Modify Linker Script with section for .text Start section.
   * Modify startup to copy .text to SRAM.
* Driver SSP, SPI and USART (libopencm3).
