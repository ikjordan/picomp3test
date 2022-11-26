# picomp3test
Minimal demonstration of picomp3lib on target.

Configured to run on the Cytron Maker Pico board https://github.com/CytronTechnologies/MAKER-PI-PICO 

If using another board, with a differently configured SD Card reader, then changes will need to be made to  `hw_config.c`

By default, the decoder will run for 30 seconds. This may result in the mp3 file being decoded multiple times. A wav file is created from the total decoded output. How much faster than real time the decode runs, is reported.

To decode the entire mp3 file once only, define `NO_LOOP`

Note: For an example off target, see the `test` sub-directory of `picomp3lib`

## To Build
`git clone https://github.com/ikjordan/picomp3test.git`  
`cd picomp3test`   
`git submodule update --init`  
`mkdir build`  
`cd build`  
`cmake ..`  
`make`

