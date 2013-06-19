## Software Installation

Download and unzip [Win32 Disk Imager](http://sourceforge.net/projects/win32diskimager/files/latest/download?source=files) (binary)

Download and unzip [the OpenWrt firmware image](http://capnbry.net/linkmeter/snapshots/bcm2708/) (Temporary Home)

Insert your SD card into your computer, launch Win32 Disk Imager, select the SD card drive, browse for the openwrt IMG file (not the ZIP!), and hit the "Write" button. Writing to the SD card should take only a few seconds. 

Insert the SD card into the Raspberry Pi and power it up using either the 12V barrel jack on the HeaterMeter board or the rPi micro USB power input. Do not hook up both at the same time! For the first boot, using the rPi USB power input is preferred to verify the operation of your assembled HeaterMeter board without the chance of subjecting the rPi to 12V which will definitely fry components on it. I know from experience.

If this is the first time you've booted the rPi using the prepared SD card, the HeaterMeter firmware will be installed automatically onto the ATmega238P.  Within 30 seconds of booting, the LCD should light up and display "-No Pit Probe-".  If you don't see anything on the LCD, but it lights up, try adjusting the contrast potentiometer with a small screwdriver.

## Configuration

By default the rPi's ethernet is set to the IP address 192.168.200.1. The configuration website is available at http://192.168.200.1/ username "root" with no password. A monitor and keyboard can also be connected. If editing configuration via the console, network configuration is in /etc/config/network

## Wireless (WiFi)

The stock image includes a driver for any rtl8192cu-based USB wifi adapter. Most testing has occurred using an [Edimax EW-7811Un](https://www.amazon.com/dp/B003MTTJOY/ref=as_li_ss_til?tag=httpcapnbrnet-20&camp=0&creative=0&linkCode=as4&creativeASIN=B003MTTJOY&adid=12GCAFY5NMYZX003C6ED&) model, but the [Airlink AWLL5099](https://www.amazon.com/dp/B006ZZUK5Y/ref=as_li_ss_til?tag=httpcapnbrnet-20&camp=0&creative=0&linkCode=as4&creativeASIN=B006ZZUK5Y&adid=0PSWHJ1WNA3GS17W0WW7&) also works. Both around $11.

The adapter should be recognized if inserted before booting and be shown in the System -> Network -> Wifi web configuration pages. At this time, only joining an existing wifi network is supported. Access point mode is technically supported but the DHCP server is not included in the OpenWrt image yet, so you'll have to assign addresses manually.