# ANTS

ANTS, the Automated Networking Test Suite, is a tool designed to streamline the analysis of compliance of commercial WiFi networking devices to the IEEE 802.11 standard. The metric for this compliance output is developed by Ammar Alhosainy *et al.* at Carleton University, in parternship with Ericsson's Ottawa and international offices. The purpose of the ANTS tool is to simplify this process by providing an easy-to-use graphical interface for configuring and running tests against these devices. In order to maximize its accessibility, ANTS continues to be designed exclusively with open-source and freely-available software, particularly that which is available on modern Linux operating systems.

![alt text](docs/images/gui_example.jpg "The ANTS User Interface")

**Note**: This project is under active development, and a stable release branch has not yet been established.
The ```master``` branch is where the most stable version can be found, but interface and functionality contained therein are not yet guaranteed to be consistent or fully operational.

## Hardware Requirements

The following is a list of essential components for using ANTS in its current form:

* One or more wireless networking devices, known as the Unit(s) Under Test (UUTs) with USB and/or Gigabit Ethernet LAN connectivity
* One or two modern computers with USB 3.0 and Gigabit Ethernet ports (see Installation and Test Setup for the single-machine method)
* A software-defined radio capable of transmitting and receiving on the same wireless bands as the UUTs
* An anechoic chamber, or alternatively a series of shielded cabling to connect the devices in use

ANTS was originally developed and tested using the [Ettus Research B200](https://www.ettus.com/product/details/UB200-KIT) software-defined radio device, which is the core measurement tool that senses the wireless channel and collects the data for further processing. No other devices are currently supported (although additional devices are on the roadmap). The (UUT) in a typical test setup is a either a commercially-available USB WiFi device, or a wireless router.

Below is a diagram showing an example test setup previously used at the Carleton Broadband Networks Laboratory:

![alt text](docs/images/sample_test_setup.jpg "Example ANTS Test Setup")

## Software Requirements

ANTS was written and tested on systems running Fedora 28 and Ubuntu 16.04, but it should work on any modern Linux operating system with the following installed:

* Python 3 (written and tested on 3.6.5 and later 3.7.x)
* PyQt5
* gnuradio (for the core writeIQ script)

Additionally, one script (```utils/writeIQ.py```) is currently written in Python 2, but will be updated as part of the project goals.

Early versions of the tool relied upon the use of the [MATLAB Engine for Python](https://www.mathworks.com/help/matlab/matlab-engine-for-python.html); however a significant effort was undertaken by the members of the Carleton University Broadband Networks Laboratory to rewrite the prototypical scripts in Python 3. Copies of the original MATLAB code are contained in the ```matlab``` folder for reference.

## Installation and Test Setup

Due to the size of the raw data files created, it is recommended that a significant amount of storage space (120GB or more) is allocated for the ANTS suite to operate. For a fresh installation of Ubuntu 16.04, the following must be performed in order to make ANTS operational:

1. ```sudo apt install git python3-numpy python3-matplotlib python3-pip gnuradio iperf python3-dev```
2. ```pip3 install pyqt5 netifaces``` (this may need to be run with sudo)
3. Run ```uhd_images_downloader``` to prepare the FPGA binary for use with the USRP
4. From the home directory (or wherever you want to store your copy of the project), ```git clone https://github.com/CarletonWirelessLab/ANTS```
5. Run ANTS by typing ```sudo python3 ants/ants``` from the main ANTS directory;
6. Set test parameters - particularly the access point IP address - and press "Run";
7. Collect the results.

Depending on the Ubuntu version (i.e. 18.04 or later) you may need to additionally install ```ifconfig``` and related legacy test tools.

When using a laptop as the test machine, the internal wireless card should be disabled **unless** it is the device under test, otherwise the test sequence may not perform as expected. The ANTS tool will try to automatically perform this operation for you (provided you have checked the automatic routing box), but if it fails it will need to be done manually.

An attenuator of 30dB (50 Ohms) is recommended between the access point and the splitter.

The majority of the current testing has been performed using an ASUS USB-AC56 USB WiFi device. Note that the driver for this device for Ubuntu 16.04 is located [here](https://github.com/abperiasamy/rtl8812AU_8821AU_linux).

The following is a diagram showing how to connect the test hardware for testing without an anechoic chamber:

![alt text](docs/images/single_machine_setup.jpg "Single Machine Configuration")

## Test Outputs

By default, ANTS will provide six outputs in a time-stamped folder matching the name of the test given by the user and the access category (i.e. "voice", "video", "best effort", or "background"). These files are:

1. A histogram detailing the interframe spacing of the measured data packets;
2. A second histogram showing the transmission opportunity durations measured by the software-defined radio;
3. A third histogram showing the compliance thresholds of the data via bin probabilities;
4. A plot of the raw signal data (currently non-interactive, used mainly to verify that the wireless medium is appropriately saturated);
5. A text file containing the resultant statistics of the collected data;
6. The raw data file with the extension ```.bin```.

## Known Configuration Details for Devices

| #   | Device    | Power Level | UUT Attenuator | CD Attenuator |
|:---:|:-----------:|:-----------:|:--------------:|:-------------:|
| 1   | Asus RT-AC68U     | MIN | 20 dB | 20 dB |
| 2   | BelAir 20E-11R | MAX      | 20 dB      | 20 dB |
| 3   | TP Link Archer C50  | MAX        | 0 dB      | 0 dB |
| 4   | Ericsson AP6321 | MAX     | 0 dB      | 0 dB |

## To-Do List

* Increase test customization by enabling more parameters for the software-defined radio and ```iperf``` to be set via the GUI;
* Better diagnostics and self-analysis of network performance while running;
* Build an alternative command-line interface for scripting tests;
* Add support for additional software-defined radios and other testing devices;
* Provide interactive documentation in the form of descriptive tool-tips in the GUI;
* Increase comment completeness in the code;
* Remove mixed dependence on legacy and modern networking tools;
* Windows support (low-priority right now).

## Authors

* **Trevor Gamblin** - [threexc](https://github.com/threexc)
* **Ammar Alhosainy**
* **Kareem Attiah**
* **Shady Elkamhawy**
* **Ahmad Al-Talabi**
* **Xinrui Zhang**
