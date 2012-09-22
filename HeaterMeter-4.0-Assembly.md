## Tools

* Soldering Iron & Solder - I use 60/40 0.032” rosin core solder from Radio Shack
* Diagonal wire cuttters
* Needle nose pliers
* A computer with an SD card reader

## Parts

* Everything from the [Mouser project](http://www.mouser.com/ProjectManager/ProjectDetail.aspx?AccessID=0dba74d92d) *$31*
* Everything from DigiKey: 1x[Blower](http://search.digikey.com/us/en/products/BFB0612H/603-1117-ND/1014448) 1x[Socket](http://www.digikey.com/product-detail/en/PPPC132LFBN-RC/S7116-ND/810252) 4x[Jacks](http://www.digikey.com/product-detail/en/MJ-2508N/CP-2508N-ND/281260) *$19*
* A HeaterMeter v4.0 PCB - see below *$13*
* 12V 1A (or greater) power adapter with 2.1mm barrel jack (tip positive)
* [Maverick temperature probes](http://maverickhousewares.bigcartel.com/) (ET-72 or ET-73), minimum 1, up to 4 *$10ea*
* [RaspberryPi](http://www.raspberrypi.org/) Model B *$35*
* An old RCA cable, such as composite video (yellow) or stereo audio (red/white)
* Full sized SD card (not microSD or miniSD) 32MB (yes, megs) or larger
* [WiFi Adapater](http://www.amazon.com/Edimax-EW-7811Un-Wireless-Adapter-Wizard/dp/B005CLMJLU/ref=sr_1_1?ie=UTF8&qid=1346544740&sr=8-1&keywords=edimax+ew-7811un) (optional) *$10*
* [Optional components](https://github.com/CapnBry/HeaterMeter/wiki/HeaterMeter-4.0-Hardware) if desired
* Some sort of enclosure
* Some sort of fan-attaching mechanism for your grill

### HeaterMeter v4.0 PCB

This can be obtained either by finding someone who has an extra (they're usually ordered in 3s and you probably only need one) or by ordering your own set. To order your own set, use any online PCB fab service which supports gerber files. [OSH Park](http://oshpark.com) is the preferred online service for the U.S., due to their quick turnaround, impeccable output, friendly service, and reasonable prices. Just upload the "dorkbot" zip file to their service and pay them. You'll have boards in your hands in about two weeks.
[PCB 4.0 Snapshot](http://capnbry.net/linkmeter/pcb/hm-4.0/)

## Hardware Assembly

The HeaterMeter v4.0 PCB has two sides and components go on both sides. The silkscreen outlines indicate on which side components should be placed, but in general most of the components go on the underside of the board. The easiest way to assemble the board is to start with the flattest components and work your way to the larger pieces. 

### Bottom Components

All directions in this section refer to the board being bottom side up. That is, the side that does not say "HeaterMeter 4.0" on it. The "SP1 Alarm" marking should be furthest from you and the Pit/Food1/Food2/Food3 markings should be on the left.

Cut a piece off one one of your component leads and bend it to fit into the position marked "R7 0" and solder it into place. This is a "0 ohm resistor" needed for the LCD backlight. If you did not use the recommended New Haven Display LCD, you'd instead place the proper current-limiting resistor needed for your backlight here. The New Haven model is nice in that the current-limiting resistor is integrated into the display itself.

[![Image](https://lh4.googleusercontent.com/-5e8n0oD2Vto/UFCRNsaVsyI/AAAAAAAAA0M/_PkD5L0Y_oQ/s640/IMG_0971.JPG)](https://picasaweb.google.com/lh/photo/0PJ6XKXALFJnPrR6r93tFNMTjNZETYmyPJy0liipFm0?feat=embedwebsite "PHOTO52")

Solder the rest of the resistors. The orientation on these does not matter either side can go in either hole, as long as the body of the resistor is on the right side of the board. The placements are sized such that you should be able to fold the leads of the resistor against the body at a right angle and have them just fit into the holes. It is easiest to insert a couple resistors at a time and flip the whole board over, resting the board on the resistors to hold them in place while you solder them and clip the extra leads off. When you're done soldering all the resistors, it should look like this.

[![Image](https://lh6.googleusercontent.com/-QvB5LnnE4vM/UDlM2TB7NeI/AAAAAAAAAx0/HD79PBCa7vw/s640/IMG_1039.JPG)](https://picasaweb.google.com/lh/photo/dNrgmVi5mGaye0cJ5QpnfdMTjNZETYmyPJy0liipFm0?feat=embedwebsite "PHOTO39")

Ceramic capacitors (small yellow blobs) Again, the orientation does not matter as these have no polarity.

[![Image](https://lh4.googleusercontent.com/-AjujxSiUo3E/UDlM2nzkzfI/AAAAAAAAAx4/V5b1IFJVDes/s640/IMG_1042.JPG)](https://picasaweb.google.com/lh/photo/15AX-FiAwzHT4QSITQ9BgdMTjNZETYmyPJy0liipFm0?feat=embedwebsite "PHOTO40")

The diodes have a white line on them to indicate their polarity and should be installed so their white line matches the white line marking on the PCB. Then, solder the DIP-28 socket (IC2) and the DIP-16 74HC595 (IC3). Both of these parts have a notch on one side of them which indicates the direction they need to be placed. Do not install the ATmega328P chip into socket IC2 at this time. Q1 (the fan driver MOSFET) should also be placed. To form its leads, just insert it into the holes and bend it down into position so it stays inside the component outline and the holes match up then flip the board and solder it into place.

[![Image](https://lh3.googleusercontent.com/-sRlyyQJu6fw/UDlM3vFfdXI/AAAAAAAAAyA/xSWeagmbrPs/s640/IMG_1048.JPG)](https://picasaweb.google.com/lh/photo/Vejhy0c2FNbQ-8BVBCFh9dMTjNZETYmyPJy0liipFm0?feat=embedwebsite "PHOTO41")

Install the RaspberryPi GPIO header, piezo buzzer, and Q2 (LCD backlight driver). Q2 should be mounted so that the flat edge of the component matches the flat printing on the PCB.

[![Image](https://lh4.googleusercontent.com/-CdiY1y110cw/UDlM4O8iaqI/AAAAAAAAAyI/nK-JFdhkzoc/s640/IMG_1053.JPG)](https://picasaweb.google.com/lh/photo/mYz1gXbgZ6SPif7AClZcfNMTjNZETYmyPJy0liipFm0?feat=embedwebsite "PHOTO42")

Install the electrolytic capacitors (the "cans"). The capacitor is marked with a white line on its negative side and the PCB is marked with a teeny plus sign on the positive side. You want the white line on the capacitor to be opposite the hole marked with a plus sign on the PCB. If that's too confusing, the white line on all the capacitors should be closest to you when installed. Also install the 16MHz resonator (the larger yellow blob) in the unlabeled oval closest to you by the DIP socket.

[![Image](https://lh3.googleusercontent.com/-TcDFsuAvQRM/UDlM499CiaI/AAAAAAAAAyQ/aptmq7UZWjE/s640/IMG_1055.JPG)](https://picasaweb.google.com/lh/photo/QnSvdU9A24hLZHhw9aBuBNMTjNZETYmyPJy0liipFm0?feat=embedwebsite "PHOTO43")

Install the 5V regulator board, power barrel jack, and blower RCA jack in that order.

[![Image](https://lh3.googleusercontent.com/-nUFq78d0pa0/UDlM5iFHkpI/AAAAAAAAAyY/APgZS-CjHhw/s640/IMG_1059.JPG)](https://picasaweb.google.com/lh/photo/jpngljFHuPAeY3DAFAHYRdMTjNZETYmyPJy0liipFm0?feat=embedwebsite "PHOTO44")

We're now done with the bottom components aside from the probe jacks. Note that IC4 (3.3V regulator) is left unpopulated. If you're building a standalone HeaterMeter, populate that with the MCP1700-33 or else nothing will power up. If you're building this to interface with a Raspberry Pi, IC4 is not required. At this point the TOP of the board should look like this, no components on it yet.

[![Image](https://lh3.googleusercontent.com/-PvlTkiDz_LY/UDlM6YpMhRI/AAAAAAAAAyg/6jiGceHtDDY/s640/IMG_1063.JPG)](https://picasaweb.google.com/lh/photo/piiCnTQBcXM5fUOavWJUGdMTjNZETYmyPJy0liipFm0?feat=embedwebsite "PHOTO45")

Finally, install as many probe jacks as you'll have probes connected.

### Top Components

Install R6 (LCD contrast adjustment potentiometer). 

Snap off 16 pins from the 36 pin header strip and install them in J1. If you're going to connect the LCD with a ribbon cable of some sort, I'd recommend the short ends be installed into the PCB and leave the long ends sticking up. If you're going to mount the LCD directly, I'd recommend the opposite-- with the long ends through the PCB and the short ends left sticking up. 

**You might want to pause here**. Everything on the top of the board beyond this point needs to be installed at the height appropriate for whatever enclosure you're going to put this in. The LEDs, LCD and buttons will be easier to get their height right if you're soldering them in place while trial-fitting the system into a case.

At this point you can install your LEDs (LED1, LED2, LED3) but bear in mind that if you mount them flush with the board, they will be lower than the button and LCD face. You can either mount them with long leads, or mount them and bend them over to the left so they'd be exposed out the side of the case rather than on the front panel. The longer lead on the LED (the +/anode) is inserted into the hole closest to you. There's a little + sign to indicate this on LED1 but not the others, as that would get confusing with them all so close together.

Finally install the button into the large square position in the center of the board. This should only fit in one orientation, but I'm sure if you try really hard you can force it in the wrong way. Don't try that hard. To get my button height right, I straightened the pins on it and slid a 3mm spacer under the button before soldering it from the front.

[![Image](https://lh3.googleusercontent.com/-Os2j-rg-ya0/UDlM7KPVAfI/AAAAAAAAAyo/2fPX4qO6k0Y/s640/IMG_1066.JPG)](https://picasaweb.google.com/lh/photo/vTLgZ7ebgSrFBtmNq1O_JNMTjNZETYmyPJy0liipFm0?feat=embedwebsite "PHOTO46")

The LCD can now be installed by soldering all 16 pins in place on the lower of the two connectors on the LCD itself. The LCD extends away from you and hangs off the board.

Do not populate J2 (PROBE), J4 (BLW), J6 (ICSP), or J8 (FTDI) unless you need them. These are provided for users who don't use the integrated connectors.

At this point you can install the ATmega328P into the DIP-28 socket IC2.

[![Image](https://lh6.googleusercontent.com/-hEatntLaa_U/UDlM7wjlStI/AAAAAAAAAyw/6pRQdfjefdU/s640/IMG_1069.JPG)](https://picasaweb.google.com/lh/photo/VO7IJMtWG143LdyMFK620NMTjNZETYmyPJy0liipFm0?feat=embedwebsite "PHOTO47")
[![Image](https://lh6.googleusercontent.com/-aU5i6h41aDY/UDlM8v9WmII/AAAAAAAAAy4/pIjaHHqaMqU/s640/IMG_1074.JPG)](https://picasaweb.google.com/lh/photo/c_fSUT5iCas7D_CzBpk7b9MTjNZETYmyPJy0liipFm0?feat=embedwebsite "PHOTO48")
[![Image](https://lh4.googleusercontent.com/-7ipZyv5Hg8c/UDlM88zr7XI/AAAAAAAAAzA/5Pluii-uSW8/s640/IMG_1075.JPG)](https://picasaweb.google.com/lh/photo/D_kYvcoXWKFj6fpvRrtdFdMTjNZETYmyPJy0liipFm0?feat=embedwebsite "PHOTO49")

### Optional Components

**Ambient Temperature Thermistor** A thermistor can be attached to one of the probe jacks to allow for ambient temperature measurement when a probe is not inserted into the jack. When looking at the board from the top, solder the thermistor between the far right pin and the close pin of the jack. Remember, the probe coefficients in the configuration need to be set for the proper probe type connected. That is, when you have no probe inserted the configuration should be set for the thermistor coefficients and when a probe is inserted they should be set to match the probe type. This modification can be seen on the Food3 jack here

[![Image](https://lh5.googleusercontent.com/-llmS0PD7dMQ/UEKibZc5uuI/AAAAAAAAAz0/9msqKAfNfYo/s640/IMG_1094.JPG)](https://picasaweb.google.com/lh/photo/zpPmHbWERDCEXAi0YaRwLdMTjNZETYmyPJy0liipFm0?feat=embedwebsite "PHOTO51")

**Wireless Probe Support** HeaterMeter supports receiving ambient temperature from LaCrosse Technology IT+915 protocol weather stations as well as custom-built "lmremote" probe transmitters. If this is desired, install a RFM12B transceiver board. A short piece (78mm) of insulated solid-core wire should be installed into the hole marked ANT as an antenna.

## Software Installation

Download and unzip [Win32 Disk Imager](https://launchpad.net/win32-image-writer/+download) (binary)

Download and unzip [the OpenWrt firmware image](http://capnbry.net/linkmeter/snapshots/bcm2708/) (Temporary Home)

Insert your SD card into your computer, launch Win32 Disk Imager, select the SD card drive, browse for the openwrt IMG file (not the ZIP!), and hit the "Write" button. Writing to the SD card should take only a few seconds. 

Mount your HeaterMeter board onto the Raspberry Pi by mating the rPi's GPIO header with the HeaterMeter socket. It should mount with the RCA blower jack and power plug facing you. It will be a bit of a tight fit between the rPi's RCA jack and the 5V regulator board on the HeaterMeter. If needed the 5V regulator can be adjusted slightly sideways by holding your thumb against it and applying a little pressure while heating each of its pins on the other side with a soldering iron. The composite RCA jack can also be removed entirely from the rPi, which will allow for a much better fit overall.

[![Image](https://lh3.googleusercontent.com/-Sb53AI7UAUE/UDlM96xaU6I/AAAAAAAAAzI/_XwWe8WFUwo/s640/IMG_1078.JPG)](https://picasaweb.google.com/lh/photo/l2VPscp3eDhF20jcTcO53dMTjNZETYmyPJy0liipFm0?feat=embedwebsite "PHOTO50")

Insert the SD card into the Raspberry Pi and power it up using either the 12V barrel jack on the HeaterMeter board or the rPi micro USB power input. Do not hook up both at the same time! For the first boot, using the rPi USB power input is preferred to verify the operation of your assembled HeaterMeter board without the chance of subjecting the rPi to 12V which will definitely fry components on it. I know from experience.

If this is the first time you've booted the rPi using the prepared SD card, the HeaterMeter firmware will be installed automatically onto the ATmega238P.  Within 30 seconds of booting, the LCD should light up and display "-No Pit Probe-".

## Configuration

By default the rPi's ethernet is set to the IP address 192.168.1.1. The configuration website is available at http://192.168.1.1/ username "root" with no password. A monitor and keyboard can also be connected. If editing configuration via the console, network configuration is in /etc/config/network

## Wireless (WiFi)

The stock image includes a driver for any rtl8192cu-based USB wifi adapter. Most testing has occurred using an Edimax EW-7811Un model, [available from Amazon for $10](http://www.amazon.com/Edimax-EW-7811Un-Wireless-Adapter-Wizard/dp/B005CLMJLU/ref=sr_1_1?ie=UTF8&qid=1346544740&sr=8-1&keywords=edimax+ew-7811un)

The adapter should be recognized if inserted before booting and be shown in the System -> Network -> Wifi web configuration pages. At this time, only joining an existing wifi network is supported. AP mode is technically supported but the DHCP server is not included in the OpenWrt image yet, so you'll have to assign addresses manually.