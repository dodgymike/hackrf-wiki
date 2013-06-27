HackRF Jawbreaker is the beta test hardware platform for the HackRF project.

## Features

* half-duplex transceiver
* operating freq: 30 MHz to 6 GHz
* supported sample rates: 8 Msps to 20 Msps (quadrature)
* resolution: 8 bits
* interface: High Speed USB
* power supply: USB bus power
* portable
* open source

## Set your Jawbreaker Free!

Jawbreaker has an SMA antenna connector but also includes a built-in PCB antenna intended for operation near 900 MHz.  It isn't a very good antenna.  Seriously.  A paperclip stuck into the SMA connector would probably be better.  You can free your Jawbreaker to operate with better antennas by cutting the PCB trace to the PCB antenna with a knife.  This enables the SMA connector to be used without interference from the PCB antenna.

The trace to be cut is between the two solder pads inside a box labeled R44 in the [assembly diagram](https://github.com/mossmann/hackrf/blob/master/doc/hardware/jawbreaker-assembly.pdf?raw=true).  There is an arrow pointing to it printed on the board.

Due to a manufacturing error, there is solder on R44.  R44 may appear as a single solder blob.  If you have a soldering iron and solder wick/braid, use a soldering iron and fine solder wick to remove as much solder as you can from the two R44 pads. Then, use a pen knife to gently cut away the area between the two R44 pads. Make multiple, gentle cuts, instead of one or two forceful cuts. As you cut, you'll break through the black solder mask, then the copper trace between the pads, and stop when you reach fiberglass. Remove the copper trace completely, so just the two R44 pads remain. Use a multimeter or continuity tester to verify that the two R44 pads are no longer connected.

If you don't have a soldering iron, you can cut through the copper trace and the solder blob all at once, but it requires a bit more effort.

The only reason not to do this is if you want to try Jawbreaker but don't have any antenna with an SMA connector (or adapter).

If you want to restore the PCB antenna for some reason, you can install a 10 nF capacitor or a 0 ohm resistor on the R44 pads or you may be able to simply create a solder bridge.

## SMA, not RP-SMA

Some connectors that appear to be SMA are actually RP-SMA.  If you connect an RP-SMA antenna to Jawbreaker, it will seem to connect snugly but won't function at all because neither the male nor female side has a center pin.  RP-SMA connectors are most common on 2.4 GHz antennas and are popular on Wi-Fi equipment.

## Transmit Power

The maximum TX power varies by operating frequency:
* 30 MHz to 100 MHz: 5 dBm to 15 dBm, increasing as frequency decreases
* 100 MHz to 2300 MHz: 0 dBm to 10 dBm, increasing as frequency decreases
* 2300 MHz to 2700 MHz: 10 dBm to 15 dBm
* 2700 MHz to 4000 MHz: -5 dBm to 5 dBm, increasing as frequency decreases
* 4000 MHz to 6000 MHz: -15 dBm to 0 dBm, increasing as frequency decreases

Overall, the output power is enough to perform over-the-air experiments at close range or to drive an external amplifier.  If you connect an external amplifier, you should also use an external bandpass filter for your operating frequency.

Before you transmit, know your laws.  Jawbreaker has not been tested for compliance with regulations governing transmission of radio signals.  You are responsible for using your Jawbreaker legally.