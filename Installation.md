# Installation
## Installation of HeaterMeter
HeaterMeter is simply compiled using the Arduino IDE and uploaded to an AVR.  The source path is /arduino/ and it contains both the heatermeter source directory (open the pde file in the Arduino IDE) and the libraries needed.  The libraries may need to be copied / linked to your Arduino library directory depending on where you installed the source.  On Windows this is under My Documents/Arduino/Libraries, or %USERPROFILE%/Documents/Arduino/Libraries. 

It may be convenient to simply link the library directories using the Windows mklink command (Win7), which must be run as Administrator.  For example (substitute sourcepath with where your HeaterMeter source is)
    mklink /D (sourcepath)/arduino/libraries/ShiftRegLCD %USERPROFILE%/Documents/Arduino/Libraries/ShiftRegLCD

## Installation of LinkMeter
You can either build from source, use a pre-built OpenWrt image and add the needed packages, or use a pre-built LinkMeter OpenWrt image. LinkMeter currently follows OpenWrt trunk until their next release.  The pre-built image contains all the necessary prerequisites as well as the LinkMeter package, so this should be all that is needed to get up and running.  See [[OpenWrt Packages]] for more information about what is included.  
[LinkMeter OpenWrt Images](http://capnbry.net/linkmeter/snapshots/trunk/)

After you've installed the firmware image, the router will default to an IP address of 192.168.200.1 on the LAN ports.  Navigate to <http://192.168.200.1/> to continue configuration.  The username is root and there is no password by default.