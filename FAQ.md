## I can't seem to access my HackRF under Linux

### Q:
When running `hackrf_info` or any other command which tries to communicate with the HackRF, I get the following error message, altough the board seems to be enumerated properly by the Linux kernel:
```
hackrf_open() failed: HACKRF_ERROR_NOT_FOUND (-5)
```

### A:
A normal user under Linux doesn't have the permissions to access arbitrary USB devices because of security reasons. The first solution would be to run every command which tries to access the HackRF as root which is not recommended for daily usage, but at least shows you if your HackRF really works.

To fix this issue, you can write a so-called udev rule to instruct udev to set permissions for the device in a way that it can be accessed by any user on the system or in a specific group.

(The following things have been tested on Ubuntu 13.04 and my need to be adapted to other Linux distributions)  
To do that, you need to create a new rules file in the `/etc/udev/rules.d` folder. I called mine `52-hackrf.rules`. Here is the content:

```
ATTR{idVendor}=="1d50", ATTR{idProduct}=="604b", SYMLINK+="hackrf-%k", MODE="666", GROUP="plugdev"
```

The content of the file instructs udev to look out for a device with a Vendor- and Product-ID of 1d50:604b which, in this case, is the unique device identification of the HackRF Jawbreaker board. It then sets the UNIX permissions to `666` and the group to `plugdev` and creates a symlink in `/dev` to the device.

After creating the rules file you can either reboot or run the command `udevadm control --reload-rules` as root to instruct udev to reload all rule files. After replugging your HackRF board, you should be able to access the device with all utilities as a normal user.