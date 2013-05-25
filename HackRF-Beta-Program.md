Welcome to the HackRF beta program!  This page is intended as a starting point for people participating in the beta.  If you have received a beta unit, please read this page.

## Beta Program Information

For background information about the beta program, see [Giving Away HackRF](http://ossmann.blogspot.com/2013/05/giving-away-hackrf.html).

The purpose of the beta program is to find bugs.  There will be bugs.  There may be hardware design bugs.  There may be firmware bugs.  There may be software bugs.  There may be manufacturing bugs.  With your help, we should be able to find the most important bugs, enabling better HackRF platforms in the future.

The primary goal of the HackRF project is to produce an open source hardware design for general purpose SDR.  With your help, we can ensure the quality of the design.

## Beta Hardware

The HackRF beta hardware platform is [Jawbreaker](https://github.com/mossmann/hackrf/wiki/Jawbreaker).  For an introduction to the device and information about how to prepare it for external antenna connection see the [Jawbreaker](https://github.com/mossmann/hackrf/wiki/Jawbreaker) page.

Jawbreaker is a development tool.  It has not been tested for compliance with regulations governing transmission and reception of radio signals.  You are responsible for operating Jawbreaker in a manner permitted by the laws of your country.

## Software

The primary software library required to work with Jawbreaker is [libhackrf](https://github.com/mossmann/hackrf/tree/master/host/libhackrf).  To use any software that supports HackRF, you must first install libhackrf.

Software known to support HackRF:

* [hackrf-tools](https://github.com/mossmann/hackrf/tree/master/host/hackrf-tools): command-line utilities for HackRF
* [gr-osmosdr](http://cgit.osmocom.org/gr-osmosdr/): source and sink blocks for GNU Radio supporting HackRF
* [SDR#](http://www.sdrsharp.com/): A graphical SDR receiver application

Notably absent from the above list is [GNU Radio](http://gnuradio.org/redmine/projects/gnuradio/wiki), THE open source SDR software framework.  GNU Radio support is provided by gr-osmosdr.  Install GNU Radio and libhackrf, then install gr-osmosdr to get them to work together.