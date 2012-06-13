Various debugger options for the LPC43xx exist, but none of us has a fully working open source solution yet.

# blackmagic

[http://www.blacksphere.co.nz/main/blackmagic](http://www.blacksphere.co.nz/main/blackmagic)

mossmann is working with the blackmagic developer to try to make it work with the LPC43xx. So far it properly identifies the M4 core via SWD and both the M4 and M0 cores via JTAG but doesn't do anything more.

# openocd

mossman hates it. Anyone have any luck?

# LPC-Link

(included with LPCXpresso boards)

TitanMKD has had some success.

# ST-LINK/V2

## Hardware Configuration

Start with an STM32F4-Discovery board. Remove the jumpers from CN3. Connect the target's SWD interface to CN2 "SWD" connector.

## Software Configuration

I'm using libusb-1.0.9.

### Install OpenOCD-0.6.0 dev

    # Cloned at hash a21affa42906f55311ec047782a427fcbcb98994
    git clone git://openocd.git.sourceforge.net/gitroot/openocd/openocd
    cd openocd
    # If necessary, patch for GDB<->OpenOCD "packet reply is too long" errors.
    # http://stackoverflow.com/questions/7053067/arm-none-eabi-gdb-and-openocd-malformed-response-to-offset-query-qoffsets
    # http://pastebin.com/rdFF2eZd
    # This patch might cause other bugs (nonexistent register p19 or similar).
    ./bootstrap
    ./configure --enable-stlink --enable-buspirate --enable-jlink --enable-maintainer-mode
    make
    sudo make install

### OpenOCD configuration files

To be gist'ed momentarily.

### Run ARM GDB

    arm-none-eabi-gdb -n
    target extended-remote localhost:3333
    monitor reset init       # Not sure difference between init and halt...
    monitor reset halt
    monitor mww 0x40043100 0x10000000
    monitor mdw 0x40043100    # Verify 0x0 shadow register is set properly.
    file lpc4350-test.axf     # This is an ELF file.
    break main
    continue
    continue     # To continue from the breakpoint.
