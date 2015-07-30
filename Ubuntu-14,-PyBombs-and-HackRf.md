# Installing Pybombs

Some of the formatting is not compatible with this wiki, this document's master is maintained at: [Celestial Photographer](http://www.celestialphotographer.com/2014/09/17/pybombs-gnuradio/)

The general disclaimer...This technique/approach has worked for me various times, it is the method I prefer, it may not work for you. You might prefer other steps. I assume no liability.
HELPFUL/CONSTRUCTIVE criticism is always welcome. Pybombs is not perfect, some recipes do not work.

When you see the word `user` in my instructions, that refers to the user name you're using, ie,
`run /home/user/pybombs/src/uhd/host/build/utils/uhd_images_downloader.py`
and your user is steve, the line becomes
`run /home/steve/pybombs/src/uhd/host/build/utils/uhd_images_downloader.py`

For me, I had issues with the following packages:

* gr-rds (solution inlcuded)
* wireshark connectors (solution included)
* gr-ieeee802154 (solution included)
* gr-ieee80211 (solution included)
* gqrx (solution included)
* gr-fosphor (solution included)
* Ettus B200/B2100 (solution included)
* gr-extras (solution included)
* openlte (solution inlcuded)
* gr-as – is no longer maintained, last usable version was Gnuradio 3.6, it was replace by Pothos, instructions for Pothos installation are included
* pocsag-mpt – is no longer maintained, last usable version was Gnuradio 3.6
* gr-smartnet – is no longer maintained, last usable version was Gnuradio 3.6
* gr-bluetooth is no longer maintained, last usable version was Gnuradio 3.6

I've included one python script that will allow you to check your install. It contains only a hackrf (osmosdr) and a FFT display centered around the FM radio band.

I always start with a fresh Ubuntu load, this one is based on Ubuntu 14.04

After install, perform the typical:
	sudo apt-get update
	sudo apt-get dist-upgrade -y

Pybombs will by default try to install all dependencies, but I have found the install goes much smoother if I install some packages in advance:

	sudo apt-get -y install git-core cmake g++ python-dev swig pkg-config libfftw3-dev libcppunit-dev libgsl0-dev libusb-dev libsdl1.2-dev python-wxgtk2.8 python-numpy python-cheetah python-lxml doxygen libxi-dev python-sip libqt4-opengl-dev libqwt-dev libfontconfig1-dev libxrender-dev python-qwt5-qt4 python-sip python-sip-dev cmake xorg-dev libglu1-mesa-dev python-zmq pypy-zmq gedit

**Reboot Ubuntu**

Terminal (<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>T</kbd>) into your home directory

	git clone git://github.com/pybombs/pybombs
	cd pybombs
	./pybombs config

In the configuration setup you can press enter for every option, I changed the install prefix location because this helps prevent errors when I manually install non pybombs packages later on, if you are only going to use pybombs “recipes” leave the default location. If you change to `/usr/local` as I did, you'll have to run `sudo ./pybombs config` after the config files run

`sudo ./pybombs config`

	Initializing config file...
	Username for GIT access
	gituser [user]:
	Install Prefix prefix [/home/user/target]:/usr/local/
	Order in which to attempt installations when available, options are: src, rpm, deb satisfy_order [deb,src]:
	Comma seperated list of package names to assume are already installed forcepkgs []:
	Time the monitor thread waits (in seconds) before retrying downloads timeout [30]:
	CMAKE_BUILD_TYPE args to pass to cmake projects, options are: Debug, Release, RelWithDebInfo, MinSizeRel, cmakebuildtype [RelWithDebInfo]:
	Build doxygen while compiling packages? options are: ON, OFF builddocs [OFF]:
	C Compiler Executable [gcc, clang, icc, etc] cc [gcc]:
	C++ Compiler Executable [g++, clang++, icpc, etc] cxx [g++]:
	Concurrent make threads [1,2,4,8...] makewidth [4]:
	done
	Settled on prefix: /usr/local

	[Errno 13] Permission denied: '/usr/local/lib64'
	Error! Configured install prefix requires root privileges. Please re-run as sudo!

**This error is normal if you ran `./pybombs config`, rerun the config typing `sudo ./pybombs config`**

	Settled on prefix: /usr/local
	Initializing environmental variables...
	/usr/local//python/:/usr/local//lib/python2.6/site-packages/:/usr/local//lib64/python2.6/site-packages/:/usr/local//lib/python2.6/dist-packages/:/usr/local//lib64/python2.6/dist-packages/:/usr/local//lib/python2.7/site-packages/:/usr/local//lib64/python2.7/site-packages/:/usr/local//lib/python2.7/dist-packages/:/usr/local//lib64/python2.7/dist-packages/:/usr/local//python/:/usr/local//lib/python2.6/site-packages/:/usr/local//lib64/python2.6/site-packages/:/usr/local//lib/python2.6/dist-packages/:/usr/local//lib64/python2.6/dist-packages/:/usr/local//lib/python2.7/site-packages/:/usr/local//lib64/python2.7/site-packages/:/usr/local//lib/python2.7/dist-packages/:/usr/local//lib64/python2.7/dist-packages/
	no existing inventory found, creating an empty one...
	---------- loading recipes -------------------
	Loading recipes ...
	Loading recipes ... done
	---------- loading recipes finished ----------

	gituser = user
	prefix = /usr/local/
	satisfy_order = deb,src
	forcepkgs =
	timeout = 30
	cmakebuildtype = RelWithDebInfo
	builddocs = OFF
	cc = gcc
	cxx = g++
	makewidth = 4

From this point forward, you only need `sudo` if you installed into a custom directory instead of the default /home/user/target

	sudo ./pybombs install gnuradio

**THIS WILL TAKE A WHILE (About an hour on an i7-3770k with 16GB of RAM)**

When it is done `sudo ./app_store.py`

Click on the packages you want to install, you can only install one at a time. The app_store may go dark. You can monitor the progress in the terminal window that you launched app_store in. If everything installs correctly, the app_store will brighten and your terminal window will display `installation ok via: src` if it errored out, the app_store will close and your terminal window will have some information in RED.

I suggest starting with `gr-osmosdr` (<--- this will install many of your app_store blocks such as hackrf and osmosdr) and also the gr-pyqt recipe.

Click the "X" in the upper right hand corner of the app store to exit.

	sudo ./pybombs env

[!http://www.celestialphotographer.com/wp-content/uploads/2014/09/setupenv-300x35.jpg](http://www.celestialphotographer.com/wp-content/uploads/2014/09/setupenv.jpg)

Take note of the env output, you'll need this information next.
Here you have two options, option 1 is simpler but I have experienced problems with it.
Option 1 doesn't require you to edit your bash file after new recipes are installed. On occasion this has given me problems.
Option 2 is more complex, but I have never had problems. You also have to update your bash file when new recipe path locations have been added/changed.

## Option 1
cd to your home directory and type `sudo gedit .bashrc`
Scroll to the bottom of your .bashrc file, it will look like this:

[![http://www.celestialphotographer.com/wp-content/uploads/2014/09/bash-300x87.jpg]](http://www.celestialphotographer.com/wp-content/uploads/2014/09/bash.jpg)

**AFTER* the last **fi** press enter and type or paste the words between`run: "` and the last `"`, in this case it is `source /usr/local/setup_env.sh`

Save the file and exit.

	source ~/.bashrc

This should reload your bash file, `gnuradio-com` and press TAB. If the source file took correctly, Ubuntu should append the gnuradio-com to gnuradio-companion

Press <kbd>Enter</kbd> and gnruadio will run.

If not, reboot.

Again, `gnuradio-com` and press <kbd>TAB</kbd>. If the source file took correctly, Ubuntu should append the gnuradio-com to gnuradio-companion

Press <kbd>Enter</kbd> and gnruadio will run.

## Option 2
Using the Ubuntu file manager, navigate to the location listed after typing `./pybombs env`. Open setup_env.sh and copy everything below the following line:

[![http://www.celestialphotographer.com/wp-content/uploads/2014/09/clipboard-300x18.jpg](http://www.celestialphotographer.com/wp-content/uploads/2014/09/clipboard.jpg)

It should look similar to:

[![http://www.celestialphotographer.com/wp-content/uploads/2014/09/clipboard-2-300x133.jpg](http://www.celestialphotographer.com/wp-content/uploads/2014/09/clipboard-2.jpg)

In the termianl window, CD to your home directory
`sudo gedit .bashrc`
Scroll to the bottom of your .bashrc file, it will look like this:

[![http://www.celestialphotographer.com/wp-content/uploads/2014/09/bash-300x87.jpg]](http://www.celestialphotographer.com/wp-content/uploads/2014/09/bash.jpg)

AFTER the last **fi** press <kbd>enter</kbd> and **PASTE**

**Reboot**

You should generate the env file and check your `.bashrc` to see if you need to update the file after installing new recipes

## Updating libhackrf
	cd ~
	git clone https://github.com/mossmann/hackrf.git
	cd hackrf/host/libhackrf/
	mkdir build
	cd build
	cmake ..
	make
	sudo make install
	sudo ldconfig
	copy /home/hackrf/host/libhackrf/53-hackrf.rules to /etc/udev/rules.d
	sudo udevadm control --reload-rules

**Reboot**

	hackrf_info

You should see something SIMILAR to:

	Found HackRF board.
	Board ID Number: 2 (HackRF One)
	Firmware Version: git-44df9d1
	Part ID Number: 0xa000cb3c 0x004d4f3f
	Serial Number: 0x00000000 0x00000000 0x457863c8 0x2f1b511f

`gnuradio-companion` to run gnuradio

You should be good to go!

If you need to update the firmware, follow Mike's directions at:
https://github.com/mossmann/hackrf/wiki/Updating-Firmware

----

# Ettus B200
Go to your home directory
`/home/user/pybombs/src/uhd/host/build/utils/uhd_images_downloader.py`
copy the rules from
`/usr/local/lib/uhd/utils` to `/etc/udev/rules.d`
`sudo udevadm control --reload-rules`

**Reboot**

Before running packages you may have to run `uhd_find_devices` or `uhd_usrp_probe`

----

# gqrx

`cd ~`
Edit the `gqrx.lwr` file and remove only the `BOOST_SUFFIX=-mt` from the qmake line
If you've already tried to install, remove by typing `sudo ./pybombs clean gqrx`
`sudo ./app_store`
Re-install by clicking gqrx button

----

# gr-rds
	type sudo apt-get install libxml2 cmake libboost-all-dev libcppunit-dev liblog4cpp5-dev swig
	cd ~
	git clone https://github.com/bastibl/gr-rds
	cd gr-rds
	mkdir build
	cd build
	cmake ..
	make
	sudo make install
	sudo ldconfig

----

# Wireshark connectors
	cd ~
	git clone https://github.com/bastibl/gr-foo.git
	cd gr-foo
	mkdir build
	cd build
	cmake ..
	make
	sudo make install
	sudo ldconfig

----

# gr-ieee802-15-4
	cd ~
	git clone git://github.com/bastibl/gr-ieee802-15-4.git
	cd gr-ieee802-15-4
	mkdir build
	cd build
	cmake ..
	make
	sudo make install
	sudo ldconfig

The hierarchical block has to be installed separately:
Open `examples/ieee802_15_4_PHY.grc` in *gnuradio-companion* and generate the flow graph. This installs the hierarchical block in your home, where gnuradio-companion can find it (typically `~/.grc_gnuradio`).

----

# gr-ieee802-11
	sudo apt-get install liblog4cpp5-dev libitpp-dev
	cd ~
	git clone git://github.com/bastibl/gr-ieee802-11.git
	cd gr-ieee802-11
	mkdir build
	cd build
	cmake ..
	make
	sudo make install
	sudo ldconfig

The physical layer is encapsulated in a hierarchical block to allow for a clearer transceiver structure in GNU Radio Companion. This hierarchical block is not included in the installation process. You have to open `/examples/wifi_phy_hier.grc` with GNU Radio Companion and build it. This will install the block in `~/.grc_gnuradio/`.

----

# gr-fosphor
I only have Nvidia graphics cards, therefore my instructions do not cover Intel or AMD, going to the main site has some instructions [http://sdr.osmocom.org/trac/wiki/fosphor]

	sudo apt-get install opencl-headers
	sudo ./app_store

click fosphor

Then edit:

`/usr/local/lib/python2.7/dist-packages/gnuradio/fosphor/__init__.py`

below this line:

`from fosphor_swig import *`
`import sys`

save the file

because of dependency issues, do these seperately, in this order
	sudo apt-get install nvidia-libopencl1-331-updates
	sudo apt-get install nvidia-opencl-dev

**Reboot**

	sudo apt-get install pyopengl (freeglut3 will be installed too)

If you try to run fosphor and get an error about
glsl 1.5 not supported in Ubuntu, go to the "additional drivers" and load the Nvidia drivers.

----

# gr-openlte

	sudo apt-get install libpolarssl5 libpolarssl-runtime libpolarssl-dev
	sudo ./app_store.py

click the gr-openlte icon

----

# Pothos

	sudo apt-get install libnuma-dev cmake g++ libpython-dev python-numpy openjdk-7-jdk qtbase5-dev libqt5svg5-dev
	cd ~
	git clone https://github.com/pothosware/pothos.git
	cd pothos
	mkdir build
	cd build
	cmake ..
	make -j4
	sudo make install
	sudo ldconfig #needed on debian systems
	PothosUtil --self-tests
	PothosGui

# To integrate Pothos into Gnuradio

	cd ~
	sudo apt-get install python-ply python-cheetah
	git clone https://github.com/pothosware/gnuradio.git
	cd gnuradio
	git checkout pothos_support
	mkdir build
	cd build
	cmake ../ -DENABLE_PYTHON=OFF -DCMAKE_INSTALL_PREFIX=/usr/local
	make -j8
	sudo make install

----

# gr-extras

	cd ~
	https://github.com/guruofquality/grextras
	mkdir build
	cd build
	cmake ..
	make
	sudo make install
	sudo ldconfig

----

# A sample GRC written in Python.

This is to provide you an operational check of your install and your HackRf

When you make a flowgraph in python it saves it in two ways, a `.grc` and a `.py`

When you click save, you are saving the GRC. When you click Execute or Generate the flowgraph you are creating the python instructions as well as saving the flowgraph. You can bypass flowgraphs if you understand python. This python script was generated from a flowgraph and the link is only included to help you test your install. It doesn’t do much.

[Test Script](http://www.celestialphotographer.com/wp-content/uploads/downloads/2014/09/test.zip)

MD-5 of test.zip : `a356e0684c53b81da3fb0bf671b23ed7`

Unzip the file and save to your home directory.
Open a Terminal (<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>T</kbd>) and type `python test.py`
If everything worked a windows should pop up and you should see something similar to this:

[![FFT](http://www.celestialphotographer.com/wp-content/uploads/2014/09/fft-300x168.jpg)](http://www.celestialphotographer.com/wp-content/uploads/2014/09/fft.jpg)