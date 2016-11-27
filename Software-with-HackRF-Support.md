# Software with HackRF Support
This is intended to be a list of software known to work with the HackRF. There are three sections, GNU Radio Based software, those that have support directly, and those that can work with data from the HackRF.

## GNU Radio Based
GNU Radio Mode-S/ADS-B - https://github.com/bistromath/gr-air-modes

GQRX - http://gqrx.dk/

## Direct Support
SDR# (Windows only) - http://sdrsharp.com/
  * Only nightly builds currently support HackRF One - http://sdrsharp.com/downloads/sdr-nightly.zip

SDR_Radio.com V2 - http://v2.sdr-radio.com/Radios/HackRF.aspx

Universal Radio Hacker - https://github.com/jopohl/urh

## Can use HackRF data

Inspectrum https://github.com/miek/inspectrum
  * Capture analysis tool with advanced features

Baudline http://www.baudline.com/  (Can view/process HackRF data, e.g. hackrf_transfer)

## HackRF Tools
In addition to third party tools that support HackRF, we provide some commandline tools for interacting with HackRF.  For information on how to use each tool look at the help information provided (e.g. ```hackrf_transfer -h```) or the [manual pages](http://manpages.ubuntu.com/manpages/utopic/man1/hackrf_info.1.html).

The first two tools (```hackrf_info``` and ```hackrf_transfer```) should cover most usage. The remaining tools are provided for debugging and general interest; beware, they have the potential to damage HackRF if used incorrectly.

 * **hackrf_info** Read device information from HackRF such as serial number and firmware version.

 * **hackrf_transfer** Send and receive signals using HackRF. Input/output can be 8bit signed quadrature files or wav files.

 * **hackrf_max2837** Read and write registers in the Maxim 2837 transceiver chip.  For most tx/rx purposes hackrf_transfer or other tools will take care of this for you.

 * **hackrf_rffc5071** Read and write registers in the RFFC5071 mixer chip.  As above, this is for curiosity or debugging only, most tools will take care of these settings automatically.

 * **hackrf_si5351c** Read and write registers in the Silicon Labs Si5351C clock generator chip. This should also be unnecessary for most operation.

 * **hackrf_spiflash** A tool to write new firmware to HackRF. This is mostly used for [[Updating Firmware]].

 * **hackrf_cpldjtag** A tool to update the CPLD on HackRF. This is also sometimes used when [[Updating Firmware]].