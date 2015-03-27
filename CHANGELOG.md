## 0.02
"Bug fixes":
Added -pthread to CMakeLists.txt to prevent compile errors for most users.

"Features": 
Fixed rtl device string so you could select which RTL device you want to use, using rtl="device index" or rtl="device serial number"
Your not limited to RTL settings you can use other settings that osmosdr supports for other devices I just use RTL as an example because it's the cheapest most common option.
Check out http://sdr.osmocom.org/trac/wiki/GrOsmoSDR for more information on supported devices and settings. Also check config.json & README.md for examples.









