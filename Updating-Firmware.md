HackRF devices ship with firmware on the SPI flash memory and with a bitstream programmed onto the CPLD.  The firmware can be updated with nothing more than a USB cable and host computer.

These instructions allow you to upgrade the firmware and CPLD bitstream in order to take advantage of new features or bug fixes.

If you have any difficulty making this process work from your native operating system, you can [use Pentoo or the GNU Radio Live DVD](https://github.com/mossmann/hackrf/wiki/Getting-Started-with-HackRF-and-GNU-Radio#try-your-hackrf-with-pentoo-linux) to perform the updates.

## Updating the SPI Flash Firmware

To update the firmware on a working HackRF One, use the hackrf_spiflash program:

    hackrf_spiflash -w hackrf_one_usb_rom_to_ram.bin

You can find the firmware binary (hackrf_one_usb_rom_to_ram.bin) in the firmware-bin directory of the latest [release package](https://github.com/mossmann/hackrf/releases/latest) or you can compile your own from the [source](https://github.com/mossmann/hackrf/tree/master/firmware).  For Jawbreaker, use hackrf_jawbreaker_usb_rom_to_ram.bin.  If you compile from source, the file will be called hackrf_usb_rom_to_ram.bin.

The hackrf_spiflash program is part hackrf-tools.

When writing a firmware image to SPI flash, be sure to select firmware that is compiled with the "rom_to_ram" option.  (Without that option, the microcontroller will try to execute code directly from SPI flash without first copying the code to RAM.  This can cause performance problems and can result in future firmware update failures.)  If you are compiling your own firmware, see firmware/README for instructions.

After writing the firmware to SPI flash, reset the HackRF device by pressing the RESET button or by unplugging it and plugging it back in.

If you get an error that mentions HACKRF_ERROR_NOT_FOUND, check out the [FAQ](https://github.com/mossmann/hackrf/wiki/FAQ#i-cant-seem-to-access-my-hackrf-under-linux). It's often a permissions problem that can be quickly solved.

## Updating the CPLD

To update to the latest CPLD image, first update the SPI flash firmware, libhackrf, and hackrf-tools.
Then:

    hackrf_cpldjtag -x firmware/cpld/sgpio_if/default.xsvf

After a few seconds, three LEDs should start blinking.  This indicates that the CPLD has been programmed successfully.  Reset the HackRF device by pressing the RESET button or by unplugging it and plugging it back in.

## DFU Boot

DFU boot mode is normally only needed if the firmware is not working properly or has never been installed.

The LPC4330 microcontroller on HackRF is capable of booting from several different code sources.  By default, HackRF boots from SPI flash memory (SPIFI).  It can also boot HackRF in DFU (USB) boot mode.  In DFU boot mode, HackRF will enumerate over USB, wait for code to be delivered using the DFU (Device Firmware Update) standard over USB, and then execute that code from RAM.  The SPIFI is normally unused and unaltered in DFU mode.

To start up HackRF One in DFU mode, hold down the DFU button while powering it on or while pressing and releasing the RESET button.  Release the DFU button after the 3V3 LED illuminates.  The 1V8 LED should remain off.  At this point HackRF One is ready to receive firmware over USB.

To start up Jawbreaker in DFU mode, short two pins on one of the "BOOT" headers while power is first supplied.  The pins that must be shorted are pins 1 and 2 of header P32 on Jawbreaker.  Header P32 is labeled "P2_8" on most Jawbreakers but may be labeled "2" on prototype units.  Pin 1 is labeled "VCC".  Pin 2 is the center pin.  After DFU boot, you should see VCCLED illuminate and note that 1V8LED does not illuminate.  At this point Jawbreaker is ready to receive firmware over USB.

Developers: DFU mode is also very convenient for making rapid changes during firmware development.  If you leave a jumper in place, you can install new firmware by removing power from Jawbreaker, plugging it back in, and typing `make program` in the firmware source directory.  Note that you should not load firmware compiled with the "rom_to_ram" option over DFU.  On HackRF One, you can simply use the DFU and RESET buttons.

## Recovering the SPI Flash Firmware

If the firmware installed in SPI flash has been damaged or if you are programming a home-made HackRF for the first time, you will not be able to immediately use the hackrf_spiflash program as listed in the above procedure.  Follow these steps instead:

1. Follow the DFU Boot instructions to start the HackRF in DFU boot mode.
2. Type `dfu-util --device 1fc9:000c --alt 0 --download hackrf_one_usb_ram.dfu` to load firmware from a release package into RAM.  If you have a Jawbreaker, use hackrf_jawbreaker_usb_ram.dfu instead.  Alternatively, use `make -e BOARD=HACKRF_ONE RUN_FROM=RAM program` in the firmware/hackrf_usb directory to load the firmware into RAM and start it.
3. Follow the SPI flash firmware update procedure above to write the "rom_to_ram" firmware image to SPI flash.


## Obtaining DFU-Util
On fresh installs of your OS, you may need obtain a copy of DFU-Util. The canonical reference can be found [here on the dfu-util source forge build page](http://dfu-util.sourceforge.net/build.html).

	cd ~
	sudo apt-get build-dep dfu-util
	sudo apt-get install libusb-1.0-0-dev
	git clone git://git.code.sf.net/p/dfu-util/dfu-util
	cd dfu-util
	./autogen.sh
	./configure
	make
	sudo make install

Now you will have the current version of DFU Util installed on your system.