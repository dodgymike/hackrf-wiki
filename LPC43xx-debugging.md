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

(included with STM32F4DISCOVERY)

Jared has had some success.