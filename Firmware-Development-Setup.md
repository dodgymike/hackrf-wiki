# Toolchain

Install the GCC ARM toolchain from [https://code.launchpad.net/gcc-arm-embedded](https://code.launchpad.net/gcc-arm-embedded).  (Other toolchains exist. YMMV).  All you have to do is unpack the archive and add the bin directory to your path.

# libopencm3

Download and install from mossmann's fork: [https://github.com/mossmann/libopencm3](https://github.com/mossmann/libopencm3)

In the future, the LPC43xx support will hopefully be available upstream, but for now you will need the fork.

With your PATH set as above, simply do a make and make install.

# HackRF firmware

You should now be able to cd into one of the HackRF firmware directories (try blinky first) and type make.

The resulting .bin file can be programmed directly onto the SPI flash with a GoodFET or Bus Pirate, or you can use a debugger.