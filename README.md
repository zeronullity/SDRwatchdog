***UNDER CONSTRUCTION***
- Currently only supports SMARTNET/P25 trunk recording with multiple SDR devices on a single trunking system.

SDR watchdog
=================

###Requirements
 - GNURadio >= 3.7
 - DSD
 - OP-25

##Compile
- cd SDRwatchdog
- cmake .
- make -j (number of threads)


##Configure

config file:  **config.json**

Here are the different arguments:
 - **sources** - an array of JSON objects that define the different SDRs available and how to configure them
   - **center** - the center frequency in Hz to tune the SDR to
   - **rate** - the sampling rate to set the SDR to, in samples / second
   - **error** - the tuning error for the SDR in Hz. This is the difference between the target value and the actual value. So if you wanted to recv 856MHz but you had to tune your SDR to 855MHz to actually recieve it, you would set this to -1000000. You should also probably get a new SDR.
   - **gain** - the RF gain to set the SDR to. Use a program like GQRX to find a good value.
   - **ifGain** - [hackrf only] sets the ifgain.
   - **bbGain** - [hackrf only] sets the bbgain.
   - **antenna** - [usrp] lets you select which antenna jack to user on devices that support it
   - **digitalRecorders** - the number of Digital Recorders to have attached to this source. This is essentaully the number of simultanious call you can record at the same time in the frequency range that this SDR will be tuned to. It is limited by the CPU power of the machine. Some experimentation might be needed to find the appropriate number. It will use DSD or OP25 to decode the P25 CAI voice.
   - **analogRecorders** - the number of Analog Recorder to have attached to this source. This is the same as Digital Recorders except for Analog Voice channels.
   - **driver** - the GNURadio block you wish to use for the SDR. The options are *usrp* & *osmosdr*.
   - **device** - For RTL devices or other gr-osmosdr supported devices. For RTL use rtl="index number" or rtl="device serial number" (you can use rtl_eeprom in the rtl-sdr package to program RTL serial numbers)
 
*Note you can also add other gr-osmosdr settings such as buflen= which may be needed for multiple usb devices. (getting a good signal, lots of cpu power, but still gettings garbled voice only when using multiple usb devices)  config.json example:  device="rtl=0,buflen=2048"  or device="rtl=0,buffers=32,buflen=2048" buflen must be in multiples of 512. If you get any usb errors try unplugging your usb rtl devices and then retry after you plug them back in.  Your not limited to RTL settings you can use other settings that osmosdr supports for other devices I just use RTL as an example because it's the cheapest most common option. 

Check out http://sdr.osmocom.org/trac/wiki/GrOsmoSDR for more information on supported devices and settings.

- **system** - This object defines the trunking system that will be recorded
   - **control_channels** - an array of the control channel frequencies for the system, in Hz. Right now, only the first value is used.
   - **type** - the type of trunking system. The options are *smartnet* & *p25*.
 - **talkgroupsFile** - this is a CSV file that provides information about the talkgroups. It determines whether a talkgroup is analog or digital, and what priority it should have. 

**ChanList.csv**

This file provides info on the different talkgroups in a trunking system. A lot of this info can be found on the Radio Reference website. You need to be a site member to download the table for your system. If you are not, try clicking on the "List All in one table" link, selecting everything in the table and copying it into Excel or a spreadsheet.

You will have to add an additional column that adds a priority for each talkgroup. You need that number of recorders available to record a call at that priority. So, 1 is the highest, you would need 2 recorders available to record a priority 2, 3 record for a priority 3 and so on.

The Trunk Record program really only uses the priority information and the Dec Talkgroup ID. The Website uses the same file though to help display information about each talkgroup.

Here are the column headers and some sample data:

| DEC |	HEX |	Mode |	Alpha Tag	| Description	| Tag |	Group | Priority |
|-----|-----|------|-----------|-------------|-----|-------|----------|
|101	| 065	| D	| DCFD 01 Disp	| 01 Dispatch |	Fire Dispatch |	Fire | 1 |
|2227 |	8b3	| D	| DC StcarYard	| Streetcar Yard |	Transportation |	Services | 3 | 


