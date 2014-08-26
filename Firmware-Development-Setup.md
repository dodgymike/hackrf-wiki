Follow these instructions to set up a firmware development environment for HackRF.

# Toolchain

Install the GCC ARM toolchain from [https://launchpad.net/gcc-arm-embedded](https://launchpad.net/gcc-arm-embedded).  (Other toolchains exist. YMMV).  All you have to do is unpack the archive and add the bin directory to your PATH. The pre-compiled GCC ARM toolchain works with Ubuntu versions up to 10.x.

# libopencm3

Download and install from mossmann's fork: [https://github.com/mossmann/libopencm3](https://github.com/mossmann/libopencm3)

In the future, the LPC43xx support will hopefully be available upstream, but for now you will need the fork.

With your PATH set as above, simply do a make and make install.

# HackRF firmware

You should now be able to cd into one of the HackRF firmware directories (try blinky first) and type make.

The resulting .bin file can be programmed directly onto the SPI flash with a GoodFET or Bus Pirate, or you can use a debugger to load directly into RAM, or you can use USB DFU boot.

# IDE - Eclipse

If you prefer to work in an IDE, Eclipse can be configured for cross-compilation:

### Install CDT Master into Eclipse

Go to http://www.eclipse.org/cdt/downloads.php and find the p2 software repository URL that's appropriate for your platform.

Start Eclipse, go to Help/Install New Software... and add the URL to the 'Work with:' field.

Two targets should be fetched: 'CDT Main Features' and 'CDT Optional Features'. Install them both.

Once installation is complete, download the arm cross-compiler support package from http://sourceforge.net/projects/gnuarmeclipse/ and install as above, using the local zip file instead of a URL for the 'Work with:' field.

From Project Explorer you should now be able to import the HackRF source as 'C/C++ / Existing Code as Makefile Project' (you can normally select <none> for the toolchain as it's specified in the Makefile, but you will need to ensure your main window environment PATH includes the required cross-compilers if you are launching Eclipse from your desktop).
