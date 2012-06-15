Based on testing with Jellybean/Lemondrop/Lollipop, here are some notes for future designs:

* A 12 MHz crystal should be attached to the LPC43xx in order to allow the built-in USB bootloader to run without having to somehow fire up the Si5351C first.
* Optionally, a clock signal from the Si5351C could be connected to the LPC43xx's GP_CLKIN pin, though the documentation on that pin is limited (acceptable peak-to-peak voltage anyone?).
* RSSI from MAX2837 should be connected to an ADC on the LPC43xx.
* Si5351C power sequencing: 1V8 must be applied before or at the same time as 3V3. This could be accomplished in various ways. Perhaps a FET controlling 3V3 for that part individually would be best.
* The various places where we have selectable 1V8/3V3 should all be fixed, probably mostly to 1V8.

# SGPIO issues

### SGPIO Clock Routing

It was a bad idea to run the SGPIO clock through the CPLD. In a future board rev, I recommend hooking one of SGPIO[8:11] directly to the same CLK_X2 signal going into the CPLD. In the interim, I modified my Jellybean (16 Apr 2012) to connect CPLD GCLK2 (at the via 1cm from the CPLD) to the LPC4330 P1_12 (at the via 3mm from the LPC4330):

![SGPIO GCLK2 reroute](https://github.com/jboone/hackrf/raw/master/doc/wiki/hardware/modifications/sgpio-gclk2-reroute.jpg)

And on the back side, I cut

![SGPIO P1_12 cut trace](https://github.com/jboone/hackrf/raw/master/doc/wiki/hardware/modifications/sgpio-p1_12-cut-trace.jpg)

I revised the clocking scheme of the Si5351C to:

* 10MHz via CLK1 to the MAX5864
* 10MHz via CLK2 to CPLD GCLK1 (assumed in-phase with CLK1 and the MAX5864)
* 20MHz via CLK3 to CPLD GCLK2 and LPC4330 P1_12 (SGPIO8) (assumed in-phase with CLK2 edges)
