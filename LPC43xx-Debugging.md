Various debugger options for the LPC43xx exist, but none of us has a fully working open source solution yet.

# blackmagic

[http://www.blacksphere.co.nz/main/blackmagic](http://www.blacksphere.co.nz/main/blackmagic)

mossmann is working with the blackmagic developer to try to make it work with the LPC43xx. So far it properly identifies the M4 core via SWD and both the M4 and M0 cores via JTAG but doesn't do anything more.

# openocd

mossman hates it. Anyone have any luck?

# LPC-Link

(included with LPCXpresso boards)

TitanMKD has had some success.
See the tutorial in hackrf/doc/LPCXPresso_Flash_Debug_Tutorial.pdf or .odt (PDF and OpenOffice document)
Doc Link [https://github.com/mossmann/hackrf/tree/master/doc)

# ST-LINK/V2

## Hardware Configuration

Start with an STM32F4-Discovery board. Remove the jumpers from CN3. Connect the target's SWD interface to CN2 "SWD" connector.

## Software Configuration

I'm using libusb-1.0.9.

### Install OpenOCD-0.6.0 dev

    # Cloned at hash a21affa42906f55311ec047782a427fcbcb98994
    git clone git://openocd.git.sourceforge.net/gitroot/openocd/openocd
    cd openocd
    ./bootstrap
    ./configure --enable-stlink --enable-buspirate --enable-jlink --enable-maintainer-mode
    make
    sudo make install

### OpenOCD configuration files

openocd.cfg

    #debug_level 3
    source [find interface/stlink-v2.cfg]
    source ./lpc4350.cfg

lpc4350.cfg

    set _CHIPNAME lpc4350
    set _M0_CPUTAPID 0x4ba00477
    set _M4_SWDTAPID 0x2ba01477
    set _M0_TAPID 0x0BA01477
    set _TRANSPORT stlink_swd

    transport select $_TRANSPORT

    stlink newtap $_CHIPNAME m4 -expected-id $_M4_SWDTAPID
    stlink newtap $_CHIPNAME m0 -expected-id $_M0_TAPID

    target create $_CHIPNAME.m4 stm32_stlink -chain-position $_CHIPNAME.m4
    #target create $_CHIPNAME.m0 stm32_stlink -chain-position $_CHIPNAME.m0

target.xml, nabbed from [an OpenOCD mailing list thread](http://www.mail-archive.com/openocd-development@lists.berlios.de/msg18182.html), to fix a communication problem between GDB and newer OpenOCD builds.

    <?xml version="1.0"?>
    <!DOCTYPE target SYSTEM "gdb-target.dtd">
    <target>
      <feature name="org.gnu.gdb.arm.core">
        <reg name="r0" bitsize="32" type="uint32"/>
        <reg name="r1" bitsize="32" type="uint32"/>
        <reg name="r2" bitsize="32" type="uint32"/>
        <reg name="r3" bitsize="32" type="uint32"/>
        <reg name="r4" bitsize="32" type="uint32"/>
        <reg name="r5" bitsize="32" type="uint32"/>
        <reg name="r6" bitsize="32" type="uint32"/>
        <reg name="r7" bitsize="32" type="uint32"/>
        <reg name="r8" bitsize="32" type="uint32"/>
        <reg name="r9" bitsize="32" type="uint32"/>
        <reg name="r10" bitsize="32" type="uint32"/>
        <reg name="r11" bitsize="32" type="uint32"/>
        <reg name="r12" bitsize="32" type="uint32"/>
        <reg name="sp" bitsize="32" type="data_ptr"/>
        <reg name="lr" bitsize="32"/>
        <reg name="pc" bitsize="32" type="code_ptr"/>
        <reg name="cpsr" bitsize="32" regnum="25"/>
      </feature>
      <feature name="org.gnu.gdb.arm.fpa">
        <reg name="f0" bitsize="96" type="arm_fpa_ext" regnum="16"/>
        <reg name="f1" bitsize="96" type="arm_fpa_ext"/>
        <reg name="f2" bitsize="96" type="arm_fpa_ext"/>
        <reg name="f3" bitsize="96" type="arm_fpa_ext"/>
        <reg name="f4" bitsize="96" type="arm_fpa_ext"/>
        <reg name="f5" bitsize="96" type="arm_fpa_ext"/>
        <reg name="f6" bitsize="96" type="arm_fpa_ext"/>
        <reg name="f7" bitsize="96" type="arm_fpa_ext"/>
        <reg name="fps" bitsize="32"/>
      </feature>
    </target>



### Run ARM GDB

Soon, I should dump this stuff into a .gdbinit file...

    arm-none-eabi-gdb -n
    target extended-remote localhost:3333
    set tdesc filename target.xml
    monitor reset init       # Not sure difference between init and halt...
    monitor reset halt
    monitor mww 0x40043100 0x10000000
    monitor mdw 0x40043100   # Verify 0x0 shadow register is set properly.
    file lpc4350-test.axf    # This is an ELF file.
    load                     # Place image into RAM.
    break main               # Set a breakpoint.
    continue                 # Run to breakpoint.
    continue                 # To continue from the breakpoint.
