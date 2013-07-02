Here are some software setup tips for particular Operating Systems and Linux distributions.

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