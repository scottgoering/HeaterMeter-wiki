## Tools

* Soldering Iron & Solder - I use 60/40 0.032” rosin core solder and an [AOYUE 936 Soldering Station](http://www.amazon.com/gp/product/B000VINMRO/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B000VINMRO&linkCode=as2&tag=httpcapnbrnet-20) although even a cheapie soldering iron from Radio Shack should get the job done easily
* [Diagonal wire cuttters](https://www.amazon.com/dp/B0002BBZ4M/ref=as_li_ss_til?tag=httpcapnbrnet-20&camp=0&creative=0&linkCode=as4&creativeASIN=B0002BBZ4M&adid=1H33ADCNJ0HZ81ZGTBCX&)
* A computer with an SD card reader
* OPTIONAL: Small [Needle nose pliers](https://www.amazon.com/dp/B004UNFPZS/ref=as_li_ss_til?tag=httpcapnbrnet-20&camp=0&creative=0&linkCode=as4&creativeASIN=B004UNFPZS&adid=1NE6M88FKG6Z48WWHK7C&) 

## Parts

* Everything from the [Mouser project](http://www.mouser.com/ProjectManager/ProjectDetail.aspx?AccessID=405078cd39) *$35*
* Everything from DigiKey: 1x[Blower](http://search.digikey.com/us/en/products/BFB0612H/603-1117-ND/1014448) 1x[Socket](http://www.digikey.com/product-detail/en/PPPC132LFBN-RC/S7116-ND/810252) 4x[Jacks](http://www.digikey.com/product-detail/en/MJ-2508N/CP-2508N-ND/281260) *$19*
* A HeaterMeter v4.2 PCB - see below *$15*
* [12V 1A](http://www.amazon.com/gp/product/B006GEPUYA/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B006GEPUYA&linkCode=as2&tag=httpcapnbrnet-20) (or greater) power adapter with 2.1mm barrel jack (tip positive) 
* [[HeaterMeter Probes]] minimum 1, up to 4 *$10-15 ea*
* [RaspberryPi](http://www.raspberrypi.org/)
  * Model A (no Ethernet, 1x USB) *$25*, or more accurately [closer to $35](https://www.amazon.com/dp/B00BC0ZL88/ref=as_li_ss_til?tag=httpcapnbrnet-20&camp=0&creative=0&linkCode=as4&creativeASIN=B00BC0ZL88&adid=0CWS9RQQA9Z6YJJ8PFF1&) shipped
  * Model B (with Wired Ethernet, 2x USB) *$35*, usually [closer to $37] (http://www.amazon.com/gp/product/B009SQQF9C/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B009SQQF9C&linkCode=as2&tag=httpcapnbrnet-20) shipped
* Full sized SD card (not microSD or miniSD) 128MB or larger
* A [[supported WiFi Adapter|Wireless Adapters]]
* Phone or ethernet cable you won't mind cutting an end off of
* Some sort of fan-attaching mechanism for your grill
* Some sort of enclosure

### HeaterMeter v4.2 PCB

This can be obtained either by finding someone who has an extra (they're usually ordered in 3s and you probably only need one) or by ordering your own set. To order your own set, use any online PCB fab service which supports gerber files. [OSH Park](http://oshpark.com) is the preferred online service for the U.S., due to their quick turnaround, impeccable output, friendly service, and reasonable prices. Just upload the "dorkbot" zip file to their service and pay them. You'll have boards in your hands in about two weeks.
[PCB 4.2 Snapshot](http://capnbry.net/linkmeter/pcb/hm-4.2/)

OSH Park will soon have PCB board singles available in their store. [OSH Park PCB 4.2 Singles](http://store.oshpark.com/products/heatermeter-v4-2) (**not yet available**)

## Prepare the PCB

The PCB arrives with some scrap material around the edges where it has been de-panelized from other boards in the batch. In a few places, this excess material can cause clearance issues with other parts or the case so it is best to remove them prior to assembly. The most important place to clean up is above the LCD pins, where excess material can prevent the LCD from mating flush.

[![Image](https://lh4.googleusercontent.com/-8t3hKt3c7Mc/U67YD1Aa4QI/AAAAAAAAB5E/BU1tkkeXVR0/s640/IMG_2165.JPG)](https://picasaweb.google.com/lh/photo/187AmKNav39OeYAphwBDitMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

[![Image](https://lh5.googleusercontent.com/-YEMR6uAGVo0/U67YEdxFOLI/AAAAAAAAB5M/rThWHubdkVc/s640/IMG_2167.JPG)](https://picasaweb.google.com/lh/photo/NsK1badyyuQvFxc_2cC-UdMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

To remove the excess, simply snap off any of the larger bits with a pair of pliers then file or sand the edge lightly to smooth the area flat. An X-Acto knife or razor can also be used. The board material is pretty soft so this shouldn't take more than a few seconds.

[![Image](https://lh5.googleusercontent.com/-ExExPUe5DWE/U67YE_5Xv8I/AAAAAAAAB5U/_4RPryg_mvE/s640/IMG_2169.JPG)](https://picasaweb.google.com/lh/photo/gKcd-Cs-Q4Oe6KqmBW6cL9MTjNZETYmyPJy0liipFm0?feat=embedwebsite)

Do this to **all four edges** of the board to prevent any issues down the road. Once the components are installed it is difficult to trim these bits without damaging the hardware. Technically, only the LCD edge, left, and right sides need to be done if you want to save 30 seconds.

## Hardware Assembly

The HeaterMeter v4.2 PCB has two sides and components go on both sides. The silkscreen outlines indicate on which side components should be placed, but in general most of the components go on the underside of the board. The easiest way to assemble the board is to start with the flattest components and work your way to the larger pieces. 

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
1|0|R-US_0204|R7|

*Step 1* This may sound a little confusing but the first part to install isn't a part at all. This '0 ohm resistor' connects the LCD backlight and allows for alternative LCDs with different backlight power circuitry. The standard HeaterMeter build does not use this so just clip a piece of lead off another component and solder it in the hole marked 0 on your PCB (0 marking not shown in photo, but is on the PCB)
[![Image](https://lh3.googleusercontent.com/-KerH2T_mBWE/U67YFvO60HI/AAAAAAAAB5k/kayadpswrbk/s640/IMG_2180.JPG)](https://picasaweb.google.com/lh/photo/GCjIEEJX6zypfM-2x47QedMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
4|390|R-US_0204|R2, R10, R12, R15
1|680|R-US_0204/7|R8
3|1k|R-US_0204|R1, R3, R21
2|2k2|R-US_0204|R9, R14
1|4k7|R-US_0204/7|R11
1|10k|R-US_0204|R20
5|100k|R-US_0204|R19, R22, R23, R28, R29
1|68k|R-US_0204|R13
1|22k|R-US_0204|R14

*Step 2* Horizontally-mounted resistors. The orientation on these does not matter either side can go in either hole, as long as the body of the resistor is on the right side of the board. The placements are sized such that you should be able to fold the leads of the resistor against the body at a right angle and have them just fit into the holes. It is easiest to insert a couple resistors at a time and flip the whole board over, resting the board on the resistors to hold them in place while you solder them and clip the extra leads off. All the standard resistors will have blue bodies, but the color bands should match what is seen here.

[![Image](https://lh3.googleusercontent.com/-lUOCgxA-Y6Y/U67YGE90JnI/AAAAAAAAB5s/wPdvYmhag8Y/s640/IMG_2184.JPG)](https://picasaweb.google.com/lh/photo/lpNvfD7-fEVhoqr8FLwgu9MTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
9|0.1u|C-US025-025X050|C1, C2, C3, C7, C10, C15, C16, C17, C18

*Step 3* Ceramic capacitors. These are small yellow blobs and also have no polarity, so their orientation does not matter.

[![Image](https://lh6.googleusercontent.com/-L9LYIBcubxI/U67YGpLZuSI/AAAAAAAAB50/m8jivB3hIVs/s640/IMG_2186.JPG)](https://picasaweb.google.com/lh/photo/k0w_9TNsYk_e7Bbn68u4W9MTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
1|1N4001|DIODE-DO41-7|D3
1|1N5819|DIODE-DO41-7|D2

*Step 4* Diodes. The rectifier diodes have a white line on them to indicate their polarity and should be installed so their white line matches the white line marking on the PCB. There are two different diodes that look identical once installed so be sure to put the right diode in the right place.

[![Image](https://lh6.googleusercontent.com/-759JrbdBLEw/U67YHDOHoVI/AAAAAAAAB54/PUwcf773v4M/s640/IMG_2187.JPG)](https://picasaweb.google.com/lh/photo/Cwv8LaaUEculV24xZQsvk9MTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
4|BS170|BS170|Q1, Q2, Q4, Q5
1|MCP1700-33|MCP1700-33|IC4

*Step 5* Signal MOSFETs and 3.3V regulator. These are the pieces that look like tiny black water towers with 3 legs. Bend the center lead back at a right angle to the body and then bend it down using your needle nose pliers. The flat front of these devices should be matched to the flat front on the silkscreen of the PCB.

[![Image](https://lh4.googleusercontent.com/-3kCmB7O2Odc/U68bJ77ZbWI/AAAAAAAAB7k/C1smNpcqQE8/s640/IMG_2204.JPG)](https://picasaweb.google.com/lh/photo/HLtZLpmOL5Sc5C0EPV6w4NMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
1|FQU11P06TU|MOSFET-P|Q3
1|74HC595N|74LS595N|IC3
1|DIP28|DIP28|IC2-SOCK

*Step 6* The power MOSFET Q3's leads can be easily formed to the right dimensions by simply inserting it into its hole then bending it down into position. Soldering the tab to the PCB is not required for the standard blower. Also install the 16 pin shift register (IC3) and the 28 pin DIP socket (IC2) for the microcontroller.  Both of these parts have a notch on one side of them which indicates the direction they need to be placed. Do not install the ATmega328P chip into socket IC2 at this time.



## Thermocouple Installation

If building the Thermocouple Pit Probe variant of the HeaterMeter, the surface mount components should be assembled and tested ([[Thermocouple Amplifier Testing]]) before starting the through-hole assembly. Note that you will not install the standard Pit jack (2.5mm audio) or the 10k 1% pullup resistor (R18) closest to the Pit jack.

## Software Installation

See: [[HeaterMeter 4.0 Software]]