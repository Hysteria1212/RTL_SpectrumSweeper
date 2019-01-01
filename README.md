# RTL_SpectrumSweeper

rtl_power GUI to automate spectrum sweeping.  

Note: I'm still playing around with it. It is functional but filled with a lot of debugging statements.     

Screenshots
------------

![Screenshot](https://davesmotleyprojects.github.io/RTL_SpectrumSweeper/RTL_SpectrumSweeper_screenshot1.png)

Requirements
------------

- Python >= 3.3
- rtl_power 
- heatmap.py (see note)
- flatten.py (see note)

Note: The version of heatmap.py required must include the --nolabels option. (OR you could modify the  RTL_SpectrumSweeper 
to *not* use the --nolabels option when calling flatten.py) The correct version of heatmap.py can be found here:
(https://github.com/davesmotleyprojects/rtl-sdr-misc). I will also include them with the RTL_SpectrumSweeper application. 


Usage
-----

Start RTL_SpectrumSweeper by running    ``python RTL_SpectrumSweeper.py [opt1] [opt2] [FILENAME]``.

[opt1] includes all (or none) of the RTL_SpectrumSweeper option. These are:

> -a (set aspect ratio) valid values are [0,1,N] (integer) (default = 1). 
   - A value of 0 will allow the waterfall image to stretch/shrink to fill the waterfall image space. 
   - A value of 1 will force the waterfall image to fit the aspect ratio of the waterfall image space.
   - A value of N will force the waterfall image space to a height of N pixels.
 
> -s (set autostop value) valid values are [0,1,N] (integer) (default = 1).
   - A value of 0 will disable the autostop feature.  
   - A value of 1 will autostop the spectrum sweep when the waterfall image space is filled. 
   - A value of N will autostop the spectrum sweep when the number of sweeps performed = N. 

> -o (set the frequency offset value) valid values are integer values in Hz. (default = 0).
   - This value will rescale the x-axis frequency values. (that's it). This is useful when using an upconverter. 
     For example, when using a "Ham It Up" the correct value would be '-o -125000000'.    

[opt2] [FILENAME] are the options required for rtl_power. These options are un-modified. Enter values exactly as you would when using rtl_power from the command line.  


Examples
-----

> python RTL_SpectrumSweeper -i 3s -g 28 -f 88M:108M:10k test.csv

Will perform continuous sweeps of the FM broadcast spectrum from 88 MHz to 108 MHz. At 5kHz steps, this will result in 2048 FFT bins. Results are written to test.csv, with the waterfall image written to test.png. With no RTL_SpectrumSweeper options (the ones listed are for rtl_power) the default waterfall image will be forecd to the window aspect ratio (at 2048 bins this is about 675 pixels high). After the window fills, which will take a little over 30 minutes, it will stop.   

> python RTL_SpectrumSweeper.py -a 100 -s 250 -o -125000000 -i 3s -g 20 -f 132000k:132200k:100 test.csv 

(With a 125MHz upconverter connected) This will perform continuous sweeps of the 40 meter (7.000 MHz to 7.200 MHz) band. At 100Hz steps, this will result in 1024 FFT bins. Results are written to test.csv, with the waterfall image written to test.png. The '-a 100' option will start the waterfall image window at 100 pixels high, and the waterfall image will fill it from top to bottom. The '-s 250' option will cause the program to stop after 250 sweeps. The '-o -125000000' option will change the x-axis tick labels to be 7.000 MHz to 7.200 MHz. 


Installation
------------

Windows:
********

1. install the rtl_power application.
   
   (This bundled as part of Pothos SDR installer: (http://downloads.myriadrf.org/builds/PothosSDR/?C=M;O=D).
   This bundle also includes other great SDR apps like [CubicSDR] (http://cubicsdr.com), [GQRX] (http://gqrx.dk),
   [GNU Radio Companion] (https://gnuradio.org), [Zadig Drivers] (http://zadig.akeo.ie), and more. 
   
2. download the RTL_SpectrumSweeper files from GitHub
   (https://github.com/davesmotleyprojects/RTL_SpectrumSweeper)
   
3. add the path to rtl_power to the Environment Variables

4. place the heatmap.py and flatten.py files in the same directory as RTL_SpectrumSweeper. 

    (I'll include the files that I used with RTL_SpetrumSweeper 

5. open a command prompt window and launch the application

   (NOTE: using the Pothos SDR installer isn't the only way to install rtl_power. It just happens to be the way I did it. 
   feel free to find your own way. Whatever you choose, I would recommend trying rtl_power via command line first to make sure
   that the environment variables are setup correctly.)
   