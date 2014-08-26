Here are some software setup tips for particular Operating Systems and Linux distributions.

## Ubuntu

These instructions were written and tested for both Ubuntu 12.04LTS and Ubuntu 14.04LTS.  You will also need to be familiar with terminal use.

**Preparing Your System**

First things first, make sure all your current software is up to date<br>
`$sudo apt-get update`<br>
`$sudo apt-get upgrade -y`

**Installing GNU Radio**

Note: These instructions use the older build-gnuradio instead of the newer [PyBOMBS](http://gnuradio.org/pybombs). Either should work fine, but it would be nice if someone were to test PyBOMBS and update these instructions so that they will remain valid in the future.

1. Create a directory to hold all the files needed to build the supporting software. In this example we will create a directory called **hackrf_files** under our home folder:<br>
`$mkdir ~/hackrf_files`
2. Download a copy of Marcus D. Leech's fantastic GNU radio setup script.  You can find it here:<br> http://www.sbrac.org/files/build-gnuradio
3. Save the script to ~/hackrf_files/build-gnuradio.sh
4. Give the script execution permission<br>
`$chmod 744 ~/hackrf_files/build-gnuradio.sh`
5. Execute the script using ~/hackrf_files/build-gnuradio.sh and follow the prompts<br>**WARNING: This step may very well take a few hours to complete!**

**Installing HackRF Tools**

If you used the above steps to install GNU Radio, simply do the following to build and install the HackRF tools:
```
cd ~/hackrf_files && git clone https://github.com/mossmann/hackrf.git
cd ~/hackrf_files/hackrf/host/hackrf-tools && mkdir build && cd build && cmake .. && make && sudo make install
```

## OS X (10.5+) with MacPorts

```
sudo port install gr-osmosdr +full
```

## Gentoo Linux

```
emerge hackrf-tools
USE="hackrf" emerge gr-osmosdr
```

## other Linux distributions

Use [PyBOMBS](http://gnuradio.org/pybombs) to automatically compile and install libhackrf, gr-osmosdr, and GNU Radio from source.