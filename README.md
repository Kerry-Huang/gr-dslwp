# gr-dslwp
---------------------------------------
GNU Radio OOT Module for the amateur radio payload of DSLWP-A/B (formal name is Longjiang-1/2, and Oscar number LO-93/94), a lunar microsatellite mission led by Harbin Institute of Technology.

DSLWP means Discovering the Sky at the Longest Wavelengths Pathfinder, as the main payload of the microsatellites are low frequency receivers for radio astronomy operating on 1~30 MHz band. 

Papers about this project: 

[1]  Wei M, Hu C, Estévez D, et al. Design and flight results of the VHF/UHF communication system of Longjiang lunar microsatellites[J/OL]. Nature Communications, 2020, 11(1): 3425[2020-07-09]. https://doi.org/10.1038/s41467-020-17272-8.

[2]  韦明川，胡超然，阎敬业，等. 首颗自主地月转移微卫星“龙江二号”[J]. 宇航学报，2020，41(6)：790-799. http://www.yhxb.org.cn/CN/10.3873/j.issn.1000-1328.2020.06.016.


## Install
---------------------------------------
 $ mkdir build 
 $ cd build 
 $ cmake ../ 
 $ make 
 $ sudo make install 
 $ sudo ldconfig 

GRC hier blocks are included in the hier folder. To install, please open the .grc files, press the "Generate flow graph" botton and restart GRC.


## Important Before Running
---------------------------------------
Please edit the path in Program Tracking CC in all the demod GRCs to the correct program tracking file. Currently gr-dslwp/examples/ 
program_tracking_dslwp-a_20180520_window1.txt for the first launch window.

As the bandwidth of the downlink signal is quite small, please calibrate your receiver frequency within 500 Hz. Warming up your receiver for at least 15 minutes, then transmit with a precise frequency, and edit the value of f_offset in frontend GRCs in Hz.


## Demod GRCs
---------------------------------------
6 different demod GRCs are provided for differnet frequencies and modes.
After sepration, the following GRCs should be used:
- demod_dslwp_gmsk_a0_500bps_0.25_dpd.grc (Satellite A Radio 0, 500 bps GMSK with 1/4 Turbo code)
- demod_dslwp_gmsk_a1_250bps_0.5_coherent.grc (Satellite A Radio 1, 250 bps GMSK with 1/2 Turbo code and precoder)
- demod_dslwp_gmsk_b0_500bps_0.25_dpd.grc (Satellite B Radio 0, 500 bps GMSK with 1/4 Turbo code) 
- demod_dslwp_gmsk_b1_250bps_0.5_coherent.grc (Satellite B Radio 1, 250 bps GMSK with 1/2 Turbo code and precoder)
It is recommanded to generate the .py files first, then run them in different terminals to distinguish the messages from different channels. 


## About TLE
---------------------------------------
A TLE was provided on http://lilacsat.hit.edu.cn/tle/dslwp.txt. It is not a precise way to describe a lunar transfer orbit, but can be used for antenna pointing during lunar transferring. After lunar injection, TLE is no longer useful.


## Telemetry Display 
---------------------------------------
Decoded telemetry will be displayed here, if uploaded with the proxy: http://lilacsat.hit.edu.cn/dashboard/pages_en/telemetry-a.html and http://lilacsat.hit.edu.cn/dashboard/pages_en/telemetry-b.html
These pages will also be used as a proof of applying QSL cards and awards. 


## About TLE
---------------------------------------
A TLE was provided on http://lilacsat.hit.edu.cn/tle/dslwp.txt. It is not a precise way to describe a lunar transfer orbit, but can be used for antenna pointing during lunar transferring. After lunar injection, TLE is no longer useful.


## Sample File to Work with Replay GRC
---------------------------------------
https://1drv.ms/u/s!Av6J6WjI3UbMhHWVF5N2PY_tgPRn


## Linux Live CD
---------------------------------------
https://1drv.ms/u/s!Av6J6WjI3UbMhHm8gwMr4Z_keqWH


## Coherent GMSK Demodulator
---------------------------------------
A GMSK demodulator under development, with OQPSK type PLL, sync word detection and Turbo codes.
In the examples folder:
- test_turbo_gmsk_selfloop.grc for software simulation. Try differnet ebn0, ebn0_threshold, pll_loop_bw, etc. for evaluation. 
- test_turbo_gmsk_tx.grc and test_turbo_gmsk_rx.grc can be used for a test with real channel with 2 USRPs.

Thanks to Gianluna for the turbo encoder / decoder: https://github.com/geeanlooca/deepspace-turbo
