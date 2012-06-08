Based on testing with Jellybean/Lemondrop/Lollipop, here are some notes for future designs:

* A 12 MHz crystal should be attached to the LPC43xx in order to allow the built-in USB bootloader to run without having to somehow fire up the Si5351C first.
* Optionally, a clock signal from the Si5351C could be connected to the LPC43xx's GP_CLKIN pin, though the documentation on that pin is limited (acceptable peak-to-peak voltage anyone?).
* RSSI from MAX2837 should be connected to an ADC on the LPC43xx.
* Si5351C power sequencing: 1V8 must be applied before or at the same time as 3V3. This could be accomplished in various ways. Perhaps a FET controlling 3V3 for that part individually would be best.
* The various places where we have selectable 1V8/3V3 should all be fixed, probably mostly to 1V8.