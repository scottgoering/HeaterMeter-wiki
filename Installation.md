# Installation
## Installation of HeaterMeter

### HeaterMeter bootloader
The ATmega328P chip **must have a bootloader** in order to load the HeaterMeter software via the serial interface. See [[HeaterMeter Bootloader]] for more information on installing a microcontroller bootloader.

### HeaterMeter software
HeaterMeter is simply compiled using the Arduino IDE and uploaded to an AVR.  The source path is /arduino/ and it contains both the heatermeter source directory (open the pde file in the Arduino IDE) and the libraries needed.  The libraries may need to be copied / linked to your Arduino library directory depending on where you installed the source.  On Windows this is under %USERPROFILE%/Documents/Arduino/Libraries. 

It may be convenient to simply link the library directories using the Windows mklink command (Win7), which must be run as Administrator.  For example (substitute sourcepath with where your HeaterMeter source is)

    mklink /D %USERPROFILE%\Documents\Arduino\Libraries\ShiftRegLCD (sourcepath)\arduino\libraries\ShiftRegLCD

If you don't know what elevated command prompts and softlinks are, just skip it and use the step-by-step method.

### HeaterMeter software step by step (Windows)
The greatest thing (sarcasm) about Windows is a a step-by-step guide is a bunch of descriptions of vaguely how things progress from action to action instead of a concise list of steps.

You'll need two things: the Arduino IDE and the HeaterMeter source.  The Arduino IDE contains everything needed to cross-compile an application for the Arduino / AVR as well as GUI editor but it **does require Java** be installed already.  Download it from [their site](http://www.arduino.cc/en/Main/Software).  Extract it and launch the editor (arduino-1.0/Arduino.exe) to verify you've got an acceptable version of Java.

> A word about "Documents": The directory / folder "Documents" used below is your personal My Documents folder, not *"C:\Documents\"*.  Where Documents is and what it is called varies based on your Windows version.

* Windows 7 and Vista: *C:\Users\username\Documents*
* Windows XP: *C:\Documents and Settings\username\My Documents*

HeaterMeter source code can be downloaded in a zip file from github.  Extract it to a heatermeter directory in your Documents folder so you'll end up with the top level README file in *Documents/heatermeter/README*.  Now copy the folder *Documents/heatermeter/Arduino* into just *Documents* so you should have *Documents/Arduino* with the folders Libraries, HeaterMeter, and LMRemote in it.

If you still have the Arduino IDE open, close it and re-open it.  Now under File -> Sketchbook select HeaterMeter.  If you don't see HeaterMeter in the list, verify from file explorer that you've got *Documents/Arduino/heatermeter/heatermeter.pde* and a bunch of *.h and *.cpp files in that directory.

Connect your Arduino / AVR and select the proper model from Tools -> Board. If you bought a current ATmega328PU with Optiboot, that is an "Arduino Uno".  Note than an ATmega328 is not the same thing as an "Arduino Mega", which is actually an ATmega2560. Also make sure the proper serial port from Tools -> Serial Port is selected.  If you have multiple serial devices, it may be hard to tell which is which, but it doesn't hurt to try them all (unless you happen to have another serial device which is an ATMega with Optiboot in which case you're going to reprogram that instead).  Select File -> Upload and the code should compile in 30 seconds or so then upload to the microcontroller.

If you get errors about missing files, verify you have *Documents/Arduino/libraries* with the folders Ports, RF12, and ShiftRegLCD and each of those contains .cpp and .h files.

### Installing HeaterMeter from the router
If you have your ATmega328P with a bootloader and don't have an FTDI USB cable to load HeaterMeter from the Arduino IDE, you can load it from the router once it is connected.  The first time you load HeaterMeter, you can't use the web interface though so telnet/SSH into the router:

```
wget -O /tmp/hm.hex http://capnbry.net/linkmeter/snapshots/trunk/heatermeter.cpp.hex
avrupdate
```

Before you press enter on the ```avrupdate``` line, press and hold the RESET button on the HeaterMeter board, and press enter.  After you see ```Starting sync (release RESET now)...``` release the RESET button. Avrdude needs to start within about half a second of release of the RESET button. It make take a couple times of running ```avrupdate``` with the RESET button to get the timing right.

## Installation of LinkMeter
You can either build from source, use a pre-built OpenWrt image and add the needed packages, or use a pre-built LinkMeter OpenWrt image. LinkMeter currently follows OpenWrt trunk until their next release.  The pre-built image contains all the necessary prerequisites as well as the LinkMeter package, so this should be all that is needed to get up and running.  See [[OpenWrt Packages]] for more information about what is included.  
[LinkMeter OpenWrt Images](http://capnbry.net/linkmeter/snapshots/trunk/)

After you've installed the firmware image, the router will default to an IP address of 192.168.200.1 on the LAN ports.  A DHCP server is active on these ports so a client PC can be plugged in using a network cable to adjust the network settings on the router to your tastes. Navigate to <http://192.168.200.1/> to continue configuration.  The username is root and there is no password by default.

## Upgrading HeaterMeter
The HeaterMeter AVR firmware can be updated using the web interface to upload the HEX file for flashing.  This file is built by the Arduino IDE and is located in a randomly named folder in the temporary directory %TEMP%/buildXXXXXXXXXXX

## Upgrading LinkMeter
After installation of the prebuilt image, one can simply update the linkmeter package using the opkg utility until a new prerequisite is added.

Example upgrading the LinkMeter package (command line)

    opkg install http://capnbry.net/linkmeter/snapshots/trunk/packages/linkmeter_2_brcm47xx.ipk

Example upgrading the LinkMeter OpenWrt image, preserving configuration (command line)

    sysupgrade http://capnbry.net/linkmeter/snapshots/trunk/linkmeter-brcm47xx-squashfs.trx