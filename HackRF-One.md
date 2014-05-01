HackRF One is the current hardware platform for the HackRF project.  It is a Software Defined Radio peripheral capable of transmission or reception of radio signals from 10 MHz to 6 GHz. Designed to enable test and development of modern and next generation radio technologies, HackRF One is an open source hardware platform that can be used as a USB peripheral or programmed for stand-alone operation.

## Features

* half-duplex transceiver
* operating freq: 10 MHz to 6 GHz
* supported sample rates: 8 Msps to 20 Msps (quadrature)
* resolution: 8 bits
* interface: High Speed USB (with USB Micro-B connector)
* power supply: USB bus power
* software-controlled antenna port power (max 50 mA at 3.3 V)
* SMA female antenna connector
* SMA female clock input and output for synchronization
* convenient buttons for programming
* pin headers for expansion
* portable
* open source

## Differences between Jawbreaker and HackRF One

Jawbreaker was the beta platform that preceded HackRF One.  HackRF One incorporates the following changes and enhancements:

* Antenna port: No modification is necessary to use the SMA antenna port on HackRF One.
* PCB antenna: Removed.
* Size: HackRF One is smaller at 120 mm x 75 mm (PCB size).
* Enclosure: The commercial version of HackRF One from Great Scott Gadgets ships with an injection molded plastic enclosure. HackRF One is also designed to fit other enclosure options.
* Buttons: HackRF One has a RESET button and a DFU button for easy programming.
* Clock input and output: Installed and functional without modification.
* USB connector: HackRF One features a new USB connector and improved USB layout.
* Expansion interface: More pins are available for expansion, and pin headers are installed on HackRF One.
* Real-Time Clock: An RTC is installed on HackRF One.
* LPC4320 microcontroller: Jawbreaker had an LPC4330.
* RF shield footprint: An optional shield may be installed over HackRF One's RF section.
* Antenna port power: HackRF One can supply up to 50 mA at 3.3 V DC on the antenna port for compatibility with powered antennas and other low power amplifiers.
* Enhanced frequency range: The RF performance of HackRF One is better than Jawbreaker, particularly at the high and low ends of the operating frequency range. HackRF One can operate at 10 MHz or even lower.

## Enclosure Options

The commercial version of HackRF One from Great Scott Gadgets ships with an injection molded plastic enclosure, but it is designed to fit two optional enclosures:

* Hammond 1455J1201: HackRF One fits this extruded aluminum enclosure and other similar models from Hammond Manufacturing.  In order to use the enclosure's end plates, you will have to drill them.  An end plate template can be found in the HackRF One KiCad layout.

* Acrylic sandwich: You can also use a laser cut acrylic enclosure in the "Sick of Beige" style with HackRF One.  This is a good option for access to the expansion headers.  A design can be found in the HackRF One hardware directory.  Use any laser cutting service.

## Using HackRF One's Buttons

The RESET button resets the microcontroller.  This is a reboot that should result in a USB re-enumeration.

The DFU button invokes a USB DFU bootloader located in the microcontroller's ROM.  This bootloader makes it possible to unbrick a HackRF One with damaged firmware because the ROM cannot be overwritten.

To invoke DFU mode: Press and hold the DFU button.  While holding the DFU button, reset the HackRF One either by pressing and releasing the RESET button or by powering on the HackRF One.  Release the DFU button.

The DFU button only invokes the bootloader during reset.  This means that it can be used for other functions by custom firmware.

## SMA, not RP-SMA

Some connectors that appear to be SMA are actually RP-SMA.  If you connect an RP-SMA antenna to HackRF One, it will seem to connect snugly but won't function at all because neither the male nor female side has a center pin.  RP-SMA connectors are most common on 2.4 GHz antennas and are popular on Wi-Fi equipment.  Adapters are available.

## Transmit Power

HackRF One's absolute maximum TX power varies by operating frequency:
* 10 MHz to 2150 MHz: 5 dBm to 15 dBm, generally increasing as frequency decreases
* 2150 MHz to 2750 MHz: 13 dBm to 15 dBm
* 2750 MHz to 4000 MHz: 0 dBm to 5 dBm, increasing as frequency decreases
* 4000 MHz to 6000 MHz: -10 dBm to 0 dBm, generally increasing as frequency decreases

Through most of the frequency range up to 4 GHz, the maximum TX power is between 0 and 10 dBm.  The frequency range with best performance is 2150 MHz to 2750 MHz.

Overall, the output power is enough to perform over-the-air experiments at close range or to drive an external amplifier.  If you connect an external amplifier, you should also use an external bandpass filter for your operating frequency.

Before you transmit, know your laws.  HackRF One has not been tested for compliance with regulations governing transmission of radio signals.  You are responsible for using your HackRF One legally.

## Receive Power

The maximum RX power of HackRF One is -5 dBm.  Exceeding -5 dBm can result in permanent damage!

In theory, HackRF One can safely accept up to 10 dBm with the front-end RX amplifier disabled.  However, a simple software or user error could enable the amplifier, resulting in permanent damage.  It is better to use an external attenuator than to risk damage.

## Expansion Interface

The HackRF One expansion interface consists of headers P9, P20, P22, and P28.  These four headers are installed on the commercial HackRF One from Great Scott Gadgets.

* P9 BASEBAND: A direct analog interface to the high speed dual ADC and dual DAC.
* P20 GPIO: GPIO, ADC, RTC, and power.
* P22 I2S: I2S, SPI, I2C, UART, GPIO, and clocks.
* P28 SD: SDIO, GPIO, clocks, and CPLD.

Refer to the schematics and component documentation for more information.

Additional unpopulated headers and test points are available for test and development, but they may be incompatible with some enclosure options.