HackRF Jawbreaker ships with firmware on the SPI flash memory and with a bitstream programmed onto the CPLD.  You should be able to start using it with nothing more than a USB cable and host computer.

These instructions allow you to upgrade the firmware and CPLD bitstream in order to take advantage of new features or bug fixes.

# Updating the SPI Flash Firmware

To update the firmware on a working Jawbreaker, use the hackrf_spiflash program:
> hackrf_spiflash -l 14540 -w usb_performance_rom_to_ram.bin

Note that the length (-l option) of the .bin file must be specified.  FIXME: This should be determined automatically in the future.

When writing a firmware image to SPI flash, be sure to select firmware that is compiled with the "rom_to_ram" option.  (Without that option, the microcontroller will try to execute code directly from SPI flash without first copying the code to RAM.  This can cause performance problems and can result in future firmware update failures.)

After writing the firmware to SPI flash, unplug Jawbreaker and plug it back in to boot the new firmware.

# DFU Boot

The LPC4330 microcontroller on Jawbreaker is capable of booting from several different code sources.  By default, Jawbreaker boots from SPI flash memory (SPIFI).  By shorting two pins on one of the "BOOT" headers while power is first supplied, you can force Jawbreaker into DFU (USB) boot mode.  In DFU boot mode, Jawbreaker will enumerate over USB, wait for code to be delivered using the DFU (Device Firmware Update) standard over USB, and then execute that code from RAM.  The SPIFI is normally unused and unaltered in DFU mode.

The pins that must be shorted are pins 1 and 2 of header P32 on Jawbreaker.  Header P32 is labeled "P2_8" on most Jawbreakers but may be labeled "2" on prototype units.  Pin 1 is labeled "VCC".  Pin 2 is the center pin.  For a visual guide, see the
[Boot Mode document]( https://github.com/mossmann/hackrf/blob/master/doc/hardware/jawbreaker_boot_mode.pdf?raw=true).

When power is applied with pins shorted, you should see VCCLED illuminate and note that 1V8LED does not illuminate.  At this point Jawbreaker is ready to receive firmware over USB.

We use DFU mode to enable programming of the CPLD and to program SPI flash if the currently installed firmware is not working properly.

Developers: DFU mode is also very convenient for making rapid changes during firmware development.  If you leave a jumper in place, you can install new firmware by removing power from Jawbreaker, plugging it back in, and typing 'make program' in the firmware source directory.  Note that you should not load firmware compiled with the "rom_to_ram" option over DFU.

# Updating the CPLD

To update to the latest CPLD image, simply use DFU boot mode to load the cpldjtagprog firmware.  Follow the DFU instructions above to start Jawbreaker in DFU boot mode and then execute:
> cd firmware/cpldjtagprog

> make program

After a few seconds, three LEDs should start blinking.  This indicates that the CPLD has been programmed successfully.  You may now unplug Jawbreaker and reboot it normally.

If cpldjtagprog fails, LED2 should illuminate (and not blink).  If this happens, unplug Jawbreaker and try again.

# Recovering the SPI Flash Firmware

If the firmware installed in SPI flash has been damaged or if you are programming a home-made Jawbreaker for the first time, you will not be able to immediately use the hackrf_spiflash program as listed in the above procedure.  Follow these steps instead:

1. Follow the DFU Boot instructions to start the Jawbreaker in DFU boot mode.
2. Use 'make program' in the firmware/usb_performance directory to load the firmware into RAM and start it.
3. Follow the SPI flash firmware update procedure above to write the "rom_to_ram" firmware image to SPI flash.

FIXME: rename usb_performance