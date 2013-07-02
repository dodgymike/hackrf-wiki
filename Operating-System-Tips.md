Here are some software setup tips for particular Operating Systems and Linux distributions.

## Ubuntu 13.04

1. Prerequisites
```
sudo apt-get -y install build-essential cmake git-core autoconf automake  libtool g++ python-dev swig \
pkg-config libfftw3-dev libboost1.53-all-dev libcppunit-dev libgsl0-dev \
libusb-dev sdcc libsdl1.2-dev python-wxgtk2.8 python-numpy \
python-cheetah python-lxml doxygen python-qt4 python-qwt5-qt4 libxi-dev \
libqt4-opengl-dev libqwt5-qt4-dev libfontconfig1-dev libxrender-dev ia32-libs
```
```
sudo add-apt-repository ppa:terry.guo/gcc-arm-embedded
sudo apt-get update && sudo apt-get install gcc-arm-none-eabi
```
2. `libhackrf`
```
git clone git://github.com/mossmann/hackrf.git
cd hackrf/host
mkdir build && cd build
cmake ..
make
sudo make install
```
3. GNU Radio
(Note that this will install GNU Radio version 3.7.x which means that old flow graphs won't work due to renamings.)
```
git clone git://gnuradio.org/gnuradio.git
cd gnuradio
mkdir build && cd build
cmake ../
make -j4 // example build command to speed up compilation process when 4 cores are available
sudo make install
```
4. `gr-osmosdr`
```
git clone git://git.osmocom.org/gr-osmosdr
cd gr-osmosdr
mkdir build && cd build
cmake ../
make
sudo make install
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

Use [build-gnuradio](http://gnuradio.org/redmine/projects/gnuradio/wiki/InstallingGR#Using-the-build-gnuradio-script) to automatically compile and install libhackrf, gr-osmosdr, and GNU Radio from source.