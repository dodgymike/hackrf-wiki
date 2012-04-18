# Preparations

Board draws approximately 24mA from +3V3 when power is applied. This seems a bit high, but may be expected if not all parts are capable of low-power mode, or aren't configured for low power at power-on. I need to review the schematic and datasheets and see what can be done.

When I put my finger on the MAX2837, current consumption goes up. This suggests there may be floating nodes in that region of the circuit.

# Si5351 I2C

### Connections

* Bus Pirate GND to P7 pin 1
* Bus Pirate +3V3 to P7 pin 2 (through multimeter set to 200mA range)
* Bus Pirate CLK to P7 pin 3
* Bus Pirate MOSI to P7 pin 5

### Bus Pirate

    # set mode
    m
    # I2C mode
    4
    # ~100kHz speed
    3
    # power supplies ON
    W
    # macro 1: 7-bit address search
    (1)
    Searching I2C address space. Found devices at:
    0xC0(0x60 W) 0xC1(0x60 R) 

I2C A0 address configuration pin (not available on QFN20 package) is apparently forced to "0".
