# Installation
## Installation of HeaterMeter
HeaterMeter is simply compiled using the Arduino IDE and uploaded to an AVR.  The source path is /arduino/ and it contains both the heatermeter source directory (open the pde file in the Arduino IDE) and the libraries needed.  The libraries may need to be copied / linked to your Arduino library directory depending on where you installed the source.  On Windows this is under My Documents/Arduino/Libraries, or %USERPROFILE%/Documents/Arduino/Libraries. 

It may be convenient to simply link the library directories using the Windows mklink command (Win7), which must be run as Administrator.  For example (substitute sourcepath with where your HeaterMeter source is)
    mklink /D (sourcepath)/arduino/libraries/ShiftRegLCD %USERPROFILE%/Documents/Arduino/Libraries/ShiftRegLCD

## Installation of LinkMeter
You can either build from source, use a pre-built OpenWrt image and add the needed packages, or use a pre-built LinkMeter OpenWrt image. LinkMeter currently follows OpenWrt trunk until their next release.  The pre-built image contains all the necessary prerequisites as well as the LinkMeter package, so this should be all that is needed to get up and running.  See [[OpenWrt Packages]] for more information about what is included.  
[LinkMeter OpenWrt Images](http://capnbry.net/linkmeter/snapshots/trunk/)

After you've installed the firmware image, the router will default to an IP address of 192.168.200.1 on the LAN ports.  A DHCP server is active on these ports so a client PC can be plugged in using a network cable to adjust the network settings on the router to your tastes. Navigate to <http://192.168.200.1/> to continue configuration.  The username is root and there is no password by default.

## Upgrading HeaterMeter
The HeaterMeter AVR firmware can be updated using the web interface to upload the HEX file for flashing.  This file is built by the Arduino IDE and is located in a randomly named folder in the temporary directory %TEMP%/buildXXXXXXXXXXX

## Upgrading LinkMeter
After installation of the prebuilt image, one can simply update the linkmeter package using the opkg utility until a new prerequisite is added.

Example upgrading the LinkMeter package (command line)

    opkg install http://capnbry.net/linkmeter/snapshots/trunk/packages/linkmeter_1_brcm47xx.ipk

Example upgrading the LinkMeter OpenWrt image, preserving configuration (command line)

    sysupgrade http://capnbry.net/linkmeter/snapshots/trunk/linkmeter-brcm47xx-squashfs.trx