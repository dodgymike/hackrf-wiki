* Optionally, a clock signal from the Si5351C could be connected to the LPC43xx's GP_CLKIN pin, though the documentation on that pin is limited (acceptable peak-to-peak voltage anyone?).

# Power Management

The MAX5864 appears to come up in "Tx" or "Rcvr" mode -- I have observed that the part will pass DA bus data to ID/QD without any SPI configuration. If we're worried about USB power and minimizing current consumption, it might be good to have this device on a power regulator with an ENABLE pin, or have a FET power switch.