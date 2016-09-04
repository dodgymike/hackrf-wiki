Here are some software setup tips for particular Operating Systems and Linux distributions.

## Ubuntu

These instructions were written and tested for both Ubuntu 12.04LTS and Ubuntu 14.04LTS.  You will also need to be familiar with terminal use.  An unofficial [HackRF Ubuntu Setup](https://mborgerson.com/getting-started-with-the-hackrf-one-on-ubuntu-14-04) guide is also available.

#### Preparing Your System

First things first, make sure all your current software is up to date<br>
`$ sudo apt-get update`<br>
`$ sudo apt-get upgrade -y`


#### Installing using a package manager
Works on Ubuntu version 15.04 'Vivid' and later.<br>
This will install gnuradio, gnuradio-companion, gqrx as main programs and support for HackRF, USRP, RTL-stick. 
`$ sudo apt-get install gqrx-sdr`

#### Installing using PyBOMBS

1. Clone [PyBOMBS](http://gnuradio.org/pybombs) in your home directory and start the app store:<br>
     ```$ git clone https://github.com/pybombs/pybombs.git && cd pybombs && ./app_store.py```
2. You will be prompted for a dozen parameters (gituser, prefix, ...), press Enter to keep their default values.
3. The script will open the App Store GUI window. Install the `gnuradio` recipe by clicking on its icon. The window will freeze during compilation and installation. **Note:** This step may take a few hours to complete.
4. The script will end with the line `installation ok via: src` or `Writing "/home/<user>/.volk/volk_config"...`
5. Repeat the last step for the `hackrf` recipe.
6. After closing the app store run: ```$ ./pybombs env```<br>
7. The output tells you to run something similar to `source /home/<user>/target/setup_env.sh`, do it.
8. Add this same line to the end of your `/home/<user>/.bashrc` file.
9. Launch GRC: ```$ gnuradio-companion```

**Troubleshooting:** [GNU Radio Installation Instructions] (https://github.com/gnuberries/raspberry-radio/wiki/GNU-Radio-Installation-Instructions-(for-desktop-or-notebook))

#### Installing GNU Radio manually

Note: These instructions use the older build-gnuradio instead of the newer [PyBOMBS](http://gnuradio.org/pybombs). Either should work fine.

1. Create a directory to hold all the files needed to build the supporting software. In this example we will create a directory called **hackrf_files** under our home folder:<br>
`$ mkdir ~/hackrf_files`
2. Download a copy of Marcus D. Leech's fantastic GNU radio setup script.  You can find it here:<br> http://www.sbrac.org/files/build-gnuradio
3. Save the script to ~/hackrf_files/build-gnuradio.sh
4. Give the script execution permission<br>
`$ chmod 744 ~/hackrf_files/build-gnuradio.sh`
5. Execute the script using ~/hackrf_files/build-gnuradio.sh and follow the prompts<br>**WARNING: This step may very well take a few hours to complete!**

#### Installing HackRF Tools manually

If you used the above steps to install GNU Radio, simply do the following to build and install the HackRF tools:
```
cd ~/hackrf_files && git clone https://github.com/mossmann/hackrf.git
cd ~/hackrf_files/hackrf/host && mkdir build && cd build && cmake .. && make && sudo make install && sudo ldconfig
```
## OS X (10.5+) with MacPorts

```
sudo port install gr-osmosdr
```
## OS X (10.5+) using Homebrew
https://github.com/andresv/homebrew-gnuradio

## Gentoo Linux

```
emerge hackrf-tools
USE="hackrf" emerge gr-osmosdr
```

## Arch Linux

```
pacman -S gnuradio gnuradio-osmosdr
pacman -S gnuradio-companion
```

## other Linux distributions

If your distribution is based on RPM or DEB, then easiest is to use [PyBOMBS](http://gnuradio.org/pybombs) to automatically compile and install libhackrf, gr-osmosdr, and GNU Radio from source.