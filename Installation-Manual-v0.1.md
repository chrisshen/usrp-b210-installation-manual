# Installation:
Refer to the link:
https://kb.ettus.com/Building_and_Installing_the_USRP_Open-Source_Toolchain_(UHD_and_GNU_Radio)_on_Linux

1. Update OS (Ubuntu assumed)
    ```
    $ sudo apt-get update
    ```

2. Install dependencies

  * Ubuntu 16.04:

    ```bash
    $ sudo apt-get -y install git swig cmake doxygen build-essential libboost-all-dev 
    libtool libusb-1.0-0 libusb-1.0-0-dev libudev-dev libncurses5-dev libfftw3-bin 
    libfftw3-dev libfftw3-doc libcppunit-1.13-0v5 libcppunit-dev libcppunit-doc 
    ncurses-bin cpufrequtils python-numpy python-numpy-doc python-numpy-dbg python-scipy 
    python-docutils qt4-bin-dbg qt4-default qt4-doc libqt4-dev libqt4-dev-bin python-qt4 
    python-qt4-dbg python-qt4-dev python-qt4-doc python-qt4-doc libqwt6abi1 libfftw3-bin 
    libfftw3-dev libfftw3-doc ncurses-bin libncurses5 libncurses5-dev libncurses5-dbg 
    libfontconfig1-dev libxrender-dev libpulse-dev swig g++ automake autoconf libtool 
    python-dev libfftw3-dev libcppunit-dev libboost-all-dev libusb-dev libusb-1.0-0-dev 
    fort77 libsdl1.2-dev python-wxgtk3.0 git-core libqt4-dev python-numpy ccache python-opengl 
    libgsl-dev python-cheetah python-mako python-lxml doxygen qt4-default qt4-dev-tools 
    libusb-1.0-0-dev libqwt5-qt4-dev libqwtplot3d-qt4-dev pyqt4-dev-tools python-qwt5-qt4 
    cmake git-core wget libxi-dev gtk2-engines-pixbuf r-base-dev python-tk liborc-0.4-0 
    liborc-0.4-dev libasound2-dev python-gtk2 libzmq-dev libzmq1 python-requests python-sphinx 
    libcomedi-dev python-zmq python-setuptools
    ```

  * Ubuntu 18.04:

    ```bash
    $ sudo apt-get -y install git swig cmake doxygen build-essential libboost-all-dev 
    libtool libusb-1.0-0 libusb-1.0-0-dev libudev-dev libncurses5-dev libfftw3-bin 
    libfftw3-dev libfftw3-doc libcppunit-1.13-0v5 libcppunit-dev libcppunit-doc ncurses-bin 
    cpufrequtils python-numpy python-numpy-doc python-numpy-dbg python-scipy python-docutils 
    qt4-bin-dbg qt4-default qt4-doc libqt4-dev libqt4-dev-bin python-qt4 python-qt4-dbg 
    python-qt4-dev python-qt4-doc python-qt4-doc libqwt6abi1 libfftw3-bin libfftw3-dev 
    libfftw3-doc ncurses-bin libncurses5 libncurses5-dev libncurses5-dbg libfontconfig1-dev 
    libxrender-dev libpulse-dev swig g++ automake autoconf libtool python-dev libfftw3-dev 
    libcppunit-dev libboost-all-dev libusb-dev libusb-1.0-0-dev fort77 libsdl1.2-dev 
    python-wxgtk3.0 git-core libqt4-dev python-numpy ccache python-opengl libgsl-dev 
    python-cheetah python-mako python-lxml doxygen qt4-default qt4-dev-tools libusb-1.0-0-dev 
    libqwt5-qt4-dev libqwtplot3d-qt4-dev pyqt4-dev-tools python-qwt5-qt4 cmake git-core 
    wget libxi-dev gtk2-engines-pixbuf r-base-dev python-tk liborc-0.4-0 liborc-0.4-dev 
    libasound2-dev python-gtk2 libzmq-dev libzmq1 python-requests python-sphinx libcomedi-dev 
    python-zmq python-setuptools
    ```

3. Building and installing UHD from source code

  * Check the latest version of UHD for USRP device
  
  https://github.com/EttusResearch/uhd/tree/UHD-3.15.LTS
  
  * Make a folder for the source code of UHD
  ```bash
  $ cd ~
  $ sudo mkdir usrp
  $ cd usrp
  ```
  
  * Clone the repository and go to the directory
  ```bash
  $ git clone https://github.com/EttusResearch/uhd
  $ cd uhd
  ```
  
  * Checkout the desired UHD version. You can list full releases by:
  ```bash
  $ git tag -l
  ```
  
  * Select a verson of UHD, usually the latest released version (v3.15.0.0 at 2020/01/30):
  ```bash
  $ git checkout v3.15.0.0
  ```
  
  * Create a build folder
  ```bash
  $ cd host
  $ mkdir build
  $ cd build
  $ cmake ../
  $ make
  ```

  * Test the compiling
  ```bash
  $ make test
  ```

  * Install 
  ```bash
  $ sudo make install
  ```
  
  * update the system's shared library cache
  ```bash
  $ sudo ldconfig
  ```
  
  * Finally, make sure that the LD_LIBRARY_PATH environment variable is defined and includes the folder under which UHD was installed. Most commonly, you can add the line below to the end of your $HOME/.bashrc file:
  ```bash
  $ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
  ```
  
  * Open a new terminal for making the change effect, and run
  ```bash
  $ uhd_find_devices
  ```
  You will see `No UHD Devices Found`.
  
# Download the UHD FPGA Images

  1. You can now download the UHD FPGA Images for this installation. 
  ```bash
  $ sudo uhd_images_downloader
  ```
  You may see some successful information: `Images successfully installed to: /usr/local/share/uhd/images`
  
# Building and Installing GNU Radio from source code
  1. Make a fold and clone gnuradio from Github. The latest version of GNU Radio is 3.8.0.0 now (20200130).
  ```bash
  $ cd ~/usrp
  $ git clone --recursive https://github.com/gnuradio/gnuradio
  $ cd gnuradio
  $ git checkout 3.8.0.0
  $ git submodule update --init --recursive
  ```
  2. Build gnuradio
  ```bash
  $ mkdir build
  $ cd build
  $ cmake ../
  $ make
  ```
  3. After a long time, test the build
  ```bash
  $ make test
  ```
  4. Install the build
  ```bash
  $ sudo make install
  ```
  5. Update the system's shared library cache
  ```bash
  $ sudo ldconfig
  ```
  6. At this point, GNU Radio should be installed and ready to use. You can quickly test this, with no USRP device attached, by running the following quick tests.
  ```bash
  $ gnuradio-config-info --version
  $ gnuradio-config-info --prefix
  $ gnuradio-config-info --enabled-components
  ```  
  
  7. Simple test without USRP hardware: dialtone test.
  ```bash
  $ python $HOME/workarea/gnuradio/gr-audio/examples/python/dial_tone.py
  ```
  
  8. You can also try a GUI-based tool, called GNU Radio Companion (GRC).
  ```bash
  $ gnuradio-companion
  ```
  
# Configuring USB
  On Linux, udev handles USB plug and unplug events. The following commands install a udev rule so that non-root users may access the device. This step is only necessary for devices that use USB to connect to the host computer, such as the B200, B210, and B200mini. This setting should take effect immediately and does not require a reboot or logout/login. **Be sure that no USRP device is connected via USB when running these commands**.
  ```bash
   $ cd ~/usrp/uhd/host/utils
   $ sudo cp uhd-usrp.rules /etc/udev/rules.d/
   $ sudo udevadm control --reload-rules
   $ sudo udevadm trigger
  ```

# Connect the USRP
The installation of UHD and GNU Radio should now be complete. At this point, connect the USRP to the host computer.

If the interface is USB, then open a terminal window, and run **"lsusb"**. You should see the USRP listed on the USB bus with a VID of 2500 and PID of 0020, 0021, 0022, for B200, B210, B200mini, respectively.

Also try running **"uhd_find_devices"** and **"uhd_usrp_probe"**.

# Thread priority scheduling
When UHD spawns a new thread, it may try to boost the thread's scheduling priority. If setting the new priority fails, the UHD software prints a warning to the console, as shown below. This warning is harmless; it simply means that the thread will retain a normal or default scheduling priority.

To address this issue, non-privileged (non-root) users need to be given special permission to change the scheduling priority. This can be enabled by creating a group `usrp`, adding your user to it, and then appending the line `@usrp - rtprio 99` to the file `/etc/security/limits.conf`.
  ```bash
   $ sudo groupadd usrp
   $ sudo usermod -aG usrp $USER
  ```
 add the line below to the end of the file `/etc/security/limits.conf`
 ```bash
 @usrp - rtprio  99
 ```

You must log out and log back into the account for the settings to take effect. 

In most Linux distributions, a list of groups and group members can be found in the /etc/group file.
