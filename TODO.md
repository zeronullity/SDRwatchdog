#TODO

- Push default digitalRecorder to digitalRecorderWav and use mbe files as default. 
This may change in the future, I'll keep support for it but may choose a different
container/compression format as default. 

- Create a command-line player for playing wav/mbe/archived files and/or buffering dsd output live.  Add talkgroups
and extra info to display such as date & time. 

- Add support to automatically compress & archive old databases into one file or multiple large split files. 

- Add feature to allow player to play files from archive without the need to uncompress files to disk.

- Create a GUI version of mbe player same as above.

- Add a GUI for recorder, pull in mbe/archive player and expand on default options. 

- Add support for multiple trunking systems & control channels.

- Add a possible scanner to scan for control channels. Scanner to support data/audio logging
of non-trunking signals with omission using radio signal fingerprinting.

- Add automatic tunning of RTLs similar to Kalibrate-RTL but using more accurate methods instead of relying
on only one frequency source.

- Possible port to Windows OS at a later date. Although releasing prebuilt binaries might infringe
on US patents from dvsinc that mbelib uses. Sort of a grey area.

-  ¿?Add decryption for known keys¿?  And the gray area gets darker..

- Support for live streaming to sites such as http://www.broadcastify.com/

## Bug Fixes

- Fix file locking issues with audio files.

- Suppress compiler warnings.

- Performance fixes, normal bug fixes, testing install on top 10 Linux Distros and other OSes in VM.


