Major parts selected so far (subject to change):

* MAX2837 2.3 to 2.7 GHz transceiver
* MAX5864 ADC/DAC
* Si5351 clock generator
  * [AN619: Manually Generating an Si5351 Register Map](http://www.silabs.com/Support%20Documents/TechnicalDocs/AN619.pdf)
  * [Datasheet](http://www.silabs.com/Support%20Documents/TechnicalDocs/Si5351.pdf) - this document is a mess of typos, and best used in conjunction with AN619, which has its own typos. Usually, you can reconcile what's true by comparison and a bit of thought.
  * [Other Documentation](http://www.silabs.com/products/clocksoscillators/clock-generators-and-buffers/Pages/clock+vcxo.aspx) - includes application notes, user guides, and white papers.
* CoolRunner-II CPLD (considering switch to MAX V)
* LPC43xx ARM Cortex-M4 microcontroller
  * [User Manual](http://www.nxp.com/documents/user_manual/UM10503.pdf)
  * [Datasheet](http://www.nxp.com/documents/data_sheet/LPC4350_30_20_10.pdf)
  * [Other Documentation (LPC4330FBD144)](http://www.nxp.com/products/microcontrollers/cortex_m4/lpc4300/LPC4330FBD144.html#documentation) - includes errata and application notes.
* RFFC5072 mixer/synthesizer