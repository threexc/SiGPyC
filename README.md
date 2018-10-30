# ANTS

ANTS (the Automated Networking Test Suite; formerly SiGPyC or the Signal Generator Python Control tool) is an app
written using Python 3 with PyQt5 to do the following:

1. Provide software triggers to a signal generator such as the E4438C, or wireless device(s) with the
use of the ```iperf``` utility;
2. Doing so while simultaneously controlling other measurement equipment such as software-defined radios;
3. Automating conversion and plotting of sensed data;
4. Testing such triggering tools locally using simple server scripts (where possible and/or appropriate).

The echo_server.py and echo_client.py scripts are based off of those found [here](https://pymotw.com/3/socket/tcp.html),
but they'll get improvements to be object-oriented as I go.

**Note**: This project is under heavy development, and a stable release branch has not yet been established.
The interface and functionality contained therein are not guaranteed to be consistent

## Intended Usage

1. Run the ants.py main script by typing "python3 ants/ants.py" from the project directory
2. Toggle devices on or off, providing IP addresses and filenames as necessary
3. (Temporary) Manually run iperf as a client on a device with wireless access
to generate the traffic to analyze
4. Collect the results

## What Works

- USRP option
- Converter option
- Plotter option
- iperf (server only; client option not yet functional)

## Requirements

ANTS was written and tested on systems running Fedora 28 and Ubuntu 16.04, but it should work on any modern Linux
operating system with the following installed:

1. Python 3 (written and tested on 3.6.5)
2. PyQt5
3. MATLAB (used R2018a for testing)
4. gnuradio (for the writeIQ script)

Note that the code relies on the availability of the Python MATLAB Engine (installation instructions below). If MATLAB is unavailable then ANTS should still work, but it will be limited to controlling the USRP, signal generator, and iperf controls.

## Setup and Install

1. ```pip3 install pyqt5```
2. ```sudo dnf install gnuradio```
3. Navigate to /usr/local/MATLAB/R20XXX/extern/engines/python and run ``` sudo python3 setup.py install ```
4. From the home directory (or wherever you want to store your copy of the project), ```git clone https://github.com/threexc/ANTS```

## To-Do List

1. Clean up the GUI and add more user-friendly features
2. Settings menus that allow the target devices to be configured (among other things), so that the USRP and signal generator parameters are not hard-coded as they are now
3. Replace MATLAB with a NumPy/Matplotlib alternative
4. Windows support (low-priority right now)

## Authors

* **Trevor Gamblin** - [threexc](https://github.com/threexc) - Primary developer
* **Ammar Alhosainy** - MATLAB and some Python tools
* **Kareem Attiah** - MATLAB and some Python tools

The lanio.c and getopt.c source files are close reproductions of sample code for the Keysight E4438C signal generator, specifically that found in document E4400-90505.
