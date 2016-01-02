Major parts used in HackRF One:

* [MAX2837 2.3 to 2.7 GHz transceiver](http://www.maxim-ic.com/datasheet/index.mvp/id/5452/t/al)
  * [Datasheet](http://datasheets.maxim-ic.com/en/ds/MAX2837.pdf)
  * There's also a register map document that Mike received directly from Maxim. Send an email to Mike or submit a support request to Maxim if you want a copy.
* [MAX5864 ADC/DAC](http://www.maxim-ic.com/datasheet/index.mvp/id/3946/t/do)
  * [Datasheet](http://datasheets.maxim-ic.com/en/ds/MAX5864.pdf)
* [Si5351 clock generator](http://www.silabs.com/products/clocksoscillators/clock-generator/Pages/lvcmos-clocks-5-outputs.aspx)
  * [AN619: Manually Generating an Si5351 Register Map](http://www.silabs.com/Support%20Documents/TechnicalDocs/AN619.pdf)
  * [Datasheet](http://www.silabs.com/Support%20Documents/TechnicalDocs/Si5351.pdf) - this document is a mess of typos, and best used in conjunction with AN619, which has its own typos. Usually, you can reconcile what's true by comparison and a bit of thought.
  * [Other Documentation](http://www.silabs.com/products/clocksoscillators/clock-generators-and-buffers/Pages/clock+vcxo.aspx) - includes application notes, user guides, and white papers.
* CoolRunner-II CPLD
* [LPC43xx ARM Cortex-M4 microcontroller](http://www.nxp.com/products/microcontrollers-and-processors/arm-processors/lpc-arm-cortex-m-mcus/lpc-dual-core-cortex-m0-m4f/lpc4300:MC_1403790133078)
  * [User Manual](http://www.nxp.com/documents/user_manual/UM10503.pdf)
  * [Datasheet](http://www.nxp.com/documents/data_sheet/LPC4350_30_20_10.pdf)
  * [Other Documentation (LPC4330FBD144)](http://www.nxp.com/products/microcontrollers/cortex_m4/lpc4300/LPC4330FBD144.html#documentation) - includes errata and application notes.
  * [ARM-standard JTAG/SWD connector pinout](http://www.keil.com/support/man/docs/ulink2/ulink2_hw_connectors.htm)
  * [BSDL file for the LPC43xx (For boundary scan)](http://www.lpcware.com/system/files/LPC18xx_43xx%20BSDL%20files%2020121127_0.zip)
* [RFFC5072 mixer/synthesizer](http://www.rfmd.com/store/rffc5072-1.html)
  * [Datasheet](http://www.rfmd.com/CS/Documents/RFFC5071_2DS.pdf)
  * [Other Documentation](http://www.rfmd.com/store/rffc5072-1.html) ; click "Technical Documents" - includes programming guides and application notes.

Block Diagrams
==============

![HackRF Frontend and Baseband Block Diagram](https://raw.github.com/mossmann/hackrf/master/doc/wiki/images/hackrf_blockdiagram-frontend_baseband.png)

![HackRF Digital Stage Block Diagram](https://raw.github.com/mossmann/hackrf/master/doc/wiki/images/hackrf_blockdiagram-digital.png)