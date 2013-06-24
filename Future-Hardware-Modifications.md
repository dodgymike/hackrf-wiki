Things to consider for post-Jawbreaker hardware designs:

## Antenna

The PCB antenna on Jawbreaker was included to facilitate beta testing. Future designs likely will not include a PCB antenna.

If a PCB antenna is not included, a side-launch SMA antenna connector might be worth considering. It'd be much easier to pack up a connected HackRF if there wasn't a stiff coax cabls sticking out perpendicular to the board.

## CPLD

The CPLD could be removed, but some sort of multiplexer would be needed to meet the MAX5864 i/o requirements.  Depending on the particular LPC43xx part used, it might be possible to use the System Control Unit (SCU) for this.

## Clocking

The clock signal from the Si5351C to the LPC43xx's GP_CLKIN pin may need different passives, but the documentation on that clock input is thin (acceptable peak-to-peak voltage anyone?).

## Power Management

The MAX5864 appears to come up in "Tx" or "Rcvr" mode -- I have observed that the part will pass DA bus data to ID/QD without any SPI configuration. If we're worried about USB power and minimizing current consumption, it might be good to have this device on a power regulator with an ENABLE pin, or have a FET power switch.

## Miscellaneous

Any reason P28 (SD) pin 12 isn't grounded or doing something useful? Same goes for P25 (LPC_ISP) pin 3 -- maybe make it VCC, the signaling voltage for the ISP interface? The SPIFI connector could also use a reference voltage (GND?).