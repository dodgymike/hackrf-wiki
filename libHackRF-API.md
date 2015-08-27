libHackRF API
=============

This document describes the functions, data structures and constants that
libHackRF provides. It should be used as a refenrece for using libHackRF and the
HackRF hardware.

If you are writing a generic SDR application, i.e. not tied to the HackRF
hardware, we strongly recommend that you use either gr-osmosdr or SoapySDR to
provide support for the broadest possible range of software defined radio
hardware.

##Setup, Initialization and Shutdown

###HackRF Init
Initialize libHackRF, including global libUSB context to support multiple HackRF
hardware devices.

**Syntax:** `int hackrf_init()`

**Returns:**
A value from the hackrf_error constants listed below.


###HackRF Open

**Syntax:** `int hackrf_open(hackrf_device** device)`

**Returns:**
A value from the hackrf_error constants listed below.


###HackRF Device List
Retrieve a list of HackRF devices attached to the system. This function finds
all devices, regardless of permissions or availability of the hardware.

**Syntax:** `hackrf_device_list_t* hackrf_device_list()`

**Returns:**
A pointer to a hackrf_device_list_t struct, a list of HackRF devices attached to
the system. The contents of the hackrf_device_list_t struct are decribed in the
data structures section below.


###HackRF Device List Open
Open and acquire a handle on a device from the 

**Syntax:** `int hackrf_device_list_open(hackrf_device_list_t* list, int idx, hackrf_device** device)`

**Params:**

`list` - A pointer to a hackrf_device_list_t returned by `hackrf_device_list()`

`idx` - The list index of the HackRF device to open

`device` - Output location for hackrf_device pointer. Only valid when return
value is HACKRF_SUCCESS.

**Returns:**
A value from the hackrf_error constants listed below.


###HackRF Device List Free

**Syntax:** `void hackrf_device_list_free(hackrf_device_list_t* list)`

**Params:**

`list` - A pointer to a hackrf_device_list_t returned by `hackrf_device_list()`


###HackRF Open By Serial

**Syntax:** `int hackrf_open_by_serial(const char* const desired_serial_number, hackrf_device** device)`

**Returns:**

###HackRF Close

**Syntax:** `int hackrf_close(hackrf_device* device)`

**Returns:**
A value from the hackrf_error constants listed below.

###HackRF Exit
Cleanly shutdown libHackRF and the underlying USB context. This does not stop in
progress transfers or close the HackRF hardware. ```hackrf_close()``` should be
called before this to clceanly close the connection to the hardware.

**Syntax:** `int hackrf_exit()`

**Returns:**
A value from the hackrf_error constants listed below.

##Using the Radio

###int hackrf_start_rx(hackrf_device*, hackrf_sample_block_cb_fn, void* rx_ctx)


**Returns:**
A value from the hackrf_error constants listed below.

###int hackrf_stop_rx(hackrf_device*)


**Returns:**
A value from the hackrf_error constants listed below.

###int hackrf_start_tx(hackrf_device*, hackrf_sample_block_cb_fn, void* tx_ctx)

**Returns:**
A value from the hackrf_error constants listed below.

###int hackrf_stop_tx(hackrf_device*)

**Returns:**
A value from the hackrf_error constants listed below.


###int hackrf_set_baseband_filter_bandwidth(hackrf_device*, const uint32_t bandwidth_hz)

**Returns:**
A value from the hackrf_error constants listed below.


###uint32_t hackrf_compute_baseband_filter_bw_round_down_lt(const uint32_t bandwidth_hz)
Compute nearest freq for bw filter (manual filter)

**Returns:**
A valid baseband filter width available from the Maxim max2837 frontend used by
the radio.

###uint32_t hackrf_compute_baseband_filter_bw(const uint32_t bandwidth_hz)
Compute best default value depending on sample rate (auto filter)

**Returns:**
A valid baseband filter width available from the Maxim max2837 frontend used by
the radio.


/* range 0-40 step 8d, IF gain in osmosdr  */
###int hackrf_set_lna_gain(hackrf_device* device, uint32_t value);

/* range 0-62 step 2db, BB gain in osmosdr */
###int hackrf_set_vga_gain(hackrf_device* device, uint32_t value);

/* range 0-47 step 1db */
###int hackrf_set_txvga_gain(hackrf_device* device, uint32_t value);

/* antenna port power control */
###int hackrf_set_antenna_enable(hackrf_device* device, const uint8_t value);

###int hackrf_set_freq(hackrf_device* device, const uint64_t freq_hz);
###int hackrf_set_freq_explicit(hackrf_device* device, const uint64_t if_freq_hz, const uint64_t lo_freq_hz, const enum rf_path_filter path);

/* currently 8-20Mhz - either as a fraction, i.e. freq 20000000hz divider 2 -> 10Mhz or as plain old 10000000hz (double)
	preferred rates are 8, 10, 12.5, 16, 20Mhz due to less jitter */
###int hackrf_set_sample_rate_manual(hackrf_device* device, const uint32_t freq_hz, const uint32_t divider);
###int hackrf_set_sample_rate(hackrf_device* device, const double freq_hz);

/* external amp, bool on/off */
###int hackrf_set_amp_enable(hackrf_device* device, const uint8_t value);

/* return HACKRF_TRUE if success */
###int hackrf_is_streaming(hackrf_device* device);


##Reading and Writing Registers

###int hackrf_max2837_read(hackrf_device* device, uint8_t register_number, uint16_t* value)


**Returns:**

###int hackrf_max2837_write(hackrf_device* device, uint8_t register_number, uint16_t value)
 

**Returns:**

###int hackrf_si5351c_read(hackrf_device* device, uint16_t register_number, uint16_t* value)


**Returns:**

###int hackrf_si5351c_write(hackrf_device* device, uint16_t register_number, uint16_t value)


**Returns:**
 
###int hackrf_rffc5071_read(hackrf_device* device, uint8_t register_number, uint16_t* value)


**Returns:**

###int hackrf_rffc5071_write(hackrf_device* device, uint8_t register_number, uint16_t value)


**Returns:**
 
##Updating Firmware

/* device will need to be reset after hackrf_cpld_write */
###int hackrf_cpld_write(hackrf_device* device, unsigned char* const data, const unsigned int total_length)

###int hackrf_spiflash_erase(hackrf_device\* device)


**Returns:**


###int hackrf_spiflash_write(hackrf_device\* device, const uint32_t address, const uint16_t length, unsigned char\* const data)

**Returns:**


###int hackrf_spiflash_read(hackrf_device\* device, const uint32_t address, const uint16_t length, unsigned char\* data);


**Returns:**


##Board Identifiers

###int hackrf_board_id_read(hackrf_device\* device, uint8_t* value);


**Returns:**


###int hackrf_version_string_read(hackrf_device\* device, char\* version, uint8_t length);


**Returns:**


###int hackrf_board_partid_serialno_read(hackrf_device\* device, read_partid_serialno_t\* read_partid_serialno);


**Returns:**


##Miscellaneous
###const char\* hackrf_error_name(enum hackrf_error errcode)


**Returns:**


###const char\* hackrf_board_id_name(enum hackrf_board_id board_id)


**Returns:**


###const char\* hackrf_usb_board_id_name(enum hackrf_usb_board_id usb_board_id)

**Returns:**


###const char\* hackrf_filter_path_name(const enum rf_path_filter path)

**Returns:**


##Data Structures

`typedef struct hackrf_device hackrf_device`

```
typedef struct {
	hackrf_device* device;
	uint8_t* buffer;
	int buffer_length;
	int valid_length;
	void* rx_ctx;
	void* tx_ctx;
} hackrf_transfer;
```

```
typedef struct {
	uint32_t part_id[2];
	uint32_t serial_no[4];
} read_partid_serialno_t;
```

```
typedef struct {
	char **serial_numbers;
	enum hackrf_usb_board_id *usb_board_ids;
	int *usb_device_index;
	int devicecount;
	
	void **usb_devices;
	int usb_devicecount;
} hackrf_device_list_t;
```

`typedef int (*hackrf_sample_block_cb_fn)(hackrf_transfer* transfer)`


##Enumerations

###Supported board versions

These values identify the board type of the connected hardware. This value can
be used as an indicator of capabilities, such as frequency range, bandwidth or
antenna port power.

Board      | Frequency range | Bandwidth | Antenna port power
HackRF One | 1MHz - 6Ghz     | 20MHz     | Yes
Jawbreaker | 10MHz - 6GHz    | 20MHz     | No
Rad1o      | 50MHz - 4GHz    | 20MHz     | Unknown
Jellybean  | N/A             | 20MHz     | No

Most boards will identify as HackRF One, Jawbreaker or Rad1o. Jellybean was a
pre-production revision of HackRF. No hardware device should intentionally
report itself with an invalid board ID.

```
enum hackrf_board_id {
	BOARD_ID_JELLYBEAN  = 0,
	BOARD_ID_JAWBREAKER = 1,
	BOARD_ID_HACKRF_ONE = 2,
	BOARD_ID_RAD1O = 3,
	BOARD_ID_INVALID = 0xFF,
};
```

###USB Product IDs

```
enum hackrf_usb_board_id {
	USB_BOARD_ID_JAWBREAKER = 0x604B,
	USB_BOARD_ID_HACKRF_ONE = 0x6089,
	USB_BOARD_ID_RAD1O = 0xCC15,
	USB_BOARD_ID_INVALID = 0xFFFF,
};
```

###Tranceiver Mode
HackRF can operate in three main transceiver modes, Receive, Transmit and Signal
Source. There is also a CPLD update mode which is used to write firmware images
to the CPLD.

Receive mode is used to stream samples from the radio to the host system. The
centre frequency and bandwidth are set using 
```
enum transceiver_mode_t {
	TRANSCEIVER_MODE_OFF = 0,
	TRANSCEIVER_MODE_RX = 1,
	TRANSCEIVER_MODE_TX = 2,
	TRANSCEIVER_MODE_SS = 3,
	TRANSCEIVER_MODE_CPLD_UPDATE = 4
};
```

###Function return values
```
enum hackrf_error {
	HACKRF_SUCCESS = 0,
	HACKRF_TRUE = 1,
	HACKRF_ERROR_INVALID_PARAM = -2,
	HACKRF_ERROR_NOT_FOUND = -5,
	HACKRF_ERROR_BUSY = -6,
	HACKRF_ERROR_NO_MEM = -11,
	HACKRF_ERROR_LIBUSB = -1000,
	HACKRF_ERROR_THREAD = -1001,
	HACKRF_ERROR_STREAMING_THREAD_ERR = -1002,
	HACKRF_ERROR_STREAMING_STOPPED = -1003,
	HACKRF_ERROR_STREAMING_EXIT_CALLED = -1004,
	HACKRF_ERROR_OTHER = -9999,
};
```

###RF Filter Path

```
enum rf_path_filter {
	RF_PATH_FILTER_BYPASS = 0,
	RF_PATH_FILTER_LOW_PASS = 1,
	RF_PATH_FILTER_HIGH_PASS = 2,
};
```
