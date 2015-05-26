## Tools

* Soldering Iron & Solder - I use 60/40 0.032” rosin core solder and an [AOYUE 936 Soldering Station](http://www.amazon.com/gp/product/B000VINMRO/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B000VINMRO&linkCode=as2&tag=httpcapnbrnet-20) although even a cheapie soldering iron from Radio Shack should get the job done easily
* [Diagonal wire cuttters](https://www.amazon.com/dp/B0002BBZ4M/ref=as_li_ss_til?tag=httpcapnbrnet-20&camp=0&creative=0&linkCode=as4&creativeASIN=B0002BBZ4M&adid=1H33ADCNJ0HZ81ZGTBCX&)
* A computer with an SD card reader
* OPTIONAL: Small [Needle nose pliers](https://www.amazon.com/dp/B004UNFPZS/ref=as_li_ss_til?tag=httpcapnbrnet-20&camp=0&creative=0&linkCode=as4&creativeASIN=B004UNFPZS&adid=1NE6M88FKG6Z48WWHK7C&) 

## Parts

* Everything from the [Mouser project](http://www.mouser.com/ProjectManager/ProjectDetail.aspx?AccessID=405078cd39) *$35*
* Everything from DigiKey: 1x[Blower](http://search.digikey.com/us/en/products/BFB0612H/603-1117-ND/1014448) 1x[Socket](http://www.digikey.com/product-detail/en/PPPC132LFBN-RC/S7116-ND/810252) 4x[Jacks](http://www.digikey.com/product-detail/en/MJ-2508N/CP-2508N-ND/281260) *$19*
* A HeaterMeter v4.2 PCB - see below *$15*
* [12V 1A](http://www.amazon.com/s/ref=as_li_ss_tl?_encoding=UTF8&camp=1789&creative=390957&field-keywords=12v%20regulated%202.1mm&linkCode=ur2&rh=n%3A172282%2Ck%3A12v%20regulated%202.1mm&tag=httpcapnbrnet-20&url=search-alias%3Delectronics&linkId=DIH3GSYISX224HCY) (or greater) power adapter with 2.1mm barrel jack (tip positive) 
* [[HeaterMeter Probes]] minimum 1, up to 4 *$10-15 ea*
* [RaspberryPi](http://www.raspberrypi.org/)
  * Model A (no Ethernet, 1x USB) *$25*, or more accurately [closer to $35](https://www.amazon.com/dp/B00BC0ZL88/ref=as_li_ss_til?tag=httpcapnbrnet-20&camp=0&creative=0&linkCode=as4&creativeASIN=B00BC0ZL88&adid=0CWS9RQQA9Z6YJJ8PFF1&) shipped
  * Model B (with Wired Ethernet, 2x USB) *$35*, usually [closer to $50] (http://www.amazon.com/gp/product/B009SQQF9C/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B009SQQF9C&linkCode=as2&tag=httpcapnbrnet-20) shipped
  * **NOT** a Model B+ (not supported)
  * Model A+ (no Ethernet, 1x USB) *$20*, requires [[Pi APlus Modifications]] build [closer to $30](https://www.amazon.com/Raspberry-Pi-Model-A-256MB/dp/B00PEX05TO/ref=as_sl_pc_ss_til?tag=httpcapnbrnet-20&linkCode=w01&linkId=TH4ENGMP2GHQUQIJ&creativeASIN=B00PEX05TO) shipped
* Full sized SD card (not microSD or miniSD) 128MB or larger ([Raspberry Pi SD Compatibility](http://www.raspberry-pi.co.uk/2012/06/07/compatible-sd-cards/) )
* A [[supported WiFi Adapter|Wireless Adapters]]
* Phone or ethernet cable you won't mind cutting an end off of
* Some sort of fan-attaching mechanism for your grill
* Some sort of enclosure

### HeaterMeter v4.2 PCB

This can be obtained either by finding someone who has an extra (they're usually ordered in 3s and you probably only need one) or by ordering your own set. To order your own set, use any online PCB fab service which supports gerber files. [OSH Park](http://oshpark.com) is the preferred online service for the U.S., due to their quick turnaround, impeccable output, friendly service, and reasonable prices. Just upload the "dorkbot" zip file to their service and pay them. You'll have boards in your hands in about two weeks.
[PCB 4.2 Snapshot](http://capnbry.net/linkmeter/pcb/hm-4.2/)

Singles are also available in the [OSH Park](http://store.oshpark.com/products/heatermeter) and [HeaterMeter Store ](http://heatermeter.myshopify.com/products/heatermeter-v4-2-circuit-board-only)
 
## Prepare the PCB

The PCB may arrive with some scrap material around the edges where it has been de-panelized from other boards in the batch. In a few places, this excess material can cause clearance issues with other parts or the case so it is best to remove them prior to assembly. The most important place to clean up is above the LCD pins, where excess material can prevent the LCD from mating flush.

[![Image](https://lh4.googleusercontent.com/-8t3hKt3c7Mc/U67YD1Aa4QI/AAAAAAAAB5E/BU1tkkeXVR0/s640/IMG_2165.JPG)](https://picasaweb.google.com/lh/photo/187AmKNav39OeYAphwBDitMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

[![Image](https://lh5.googleusercontent.com/-YEMR6uAGVo0/U67YEdxFOLI/AAAAAAAAB5M/rThWHubdkVc/s640/IMG_2167.JPG)](https://picasaweb.google.com/lh/photo/NsK1badyyuQvFxc_2cC-UdMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

To remove the excess, simply snap off any of the larger bits with a pair of pliers then file or sand the edge lightly to smooth the area flat. An X-Acto knife or razor can also be used. The board material is pretty soft so this shouldn't take more than a few seconds.

[![Image](https://lh5.googleusercontent.com/-ExExPUe5DWE/U67YE_5Xv8I/AAAAAAAAB5U/_4RPryg_mvE/s640/IMG_2169.JPG)](https://picasaweb.google.com/lh/photo/gKcd-Cs-Q4Oe6KqmBW6cL9MTjNZETYmyPJy0liipFm0?feat=embedwebsite)

Do this to **all four edges** of the board to prevent any issues down the road. Once the components are installed it is difficult to trim these bits without damaging the hardware. Technically, only the LCD edge, left, and right sides need to be done if you want to save 30 seconds.

## Thermocouple Installation

If building the Thermocouple Pit Probe variant of the HeaterMeter, the surface mount components should be assembled and tested ([[Thermocouple Amplifier Testing]]) before starting the through-hole assembly. Note that you will not install the standard Pit jack (2.5mm audio) or the 10k 1% pullup resistor (R18) closest to the Pit jack.

## Hardware Assembly

The HeaterMeter v4.2 PCB has two sides and components go on both sides. The silkscreen outlines indicate on which side components should be placed, but in general most of the components go on the underside of the board. The easiest way to assemble the board is to start with the flattest components and work your way to the larger pieces. 

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
1|0|R-US_0204|R7|

**Step 1** This may sound a little confusing but the first part to install isn't a part at all. This '0 ohm resistor' connects the LCD backlight and allows for alternative LCDs with different backlight power circuitry. The standard HeaterMeter build does not use this so just clip a piece of lead off another component and solder it in the hole marked 0 on your PCB (0 marking not shown in photo, but is on the PCB)
[![Image](https://lh3.googleusercontent.com/-KerH2T_mBWE/U67YFvO60HI/AAAAAAAAB5k/kayadpswrbk/s640/IMG_2180.JPG)](https://picasaweb.google.com/lh/photo/GCjIEEJX6zypfM-2x47QedMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
4|390|R-US_0204|R2, R10, R12, R15
1|680|R-US_0204/7|R8
3|1k|R-US_0204|R1, R3 (**A+**), R21
2|2k2|R-US_0204|R9, R14
1|4k7|R-US_0204/7|R11
1|10k|R-US_0204|R20
1|100k|R-US_0204|R19
1|68k|R-US_0204|R13
1|22k|R-US_0204|R14

**Step 2** Horizontally-mounted resistors. The orientation on these does not matter either side can go in either hole, as long as the body of the resistor is on the right side of the board. The placements are sized such that you should be able to fold the leads of the resistor against the body at a right angle and have them just fit into the holes. It is easiest to insert a couple resistors at a time and flip the whole board over, resting the board on the resistors to hold them in place while you solder them and clip the extra leads off. All the standard resistors will have blue bodies, but the color bands should match what is seen here. You will have 4x 100k resistors and 4x 10k resistors left over to be used later.

**Raspberry Pi A+** Do not install R3 1k resistor at this time. See [[Pi APlus Modifications]]

[![Image](https://lh4.googleusercontent.com/-ozk2pNsWwvY/VDk1qdWxwcI/AAAAAAAACWg/1PV7Vlh6u18/s640/HeaterMeter424Kit-1.png)](https://picasaweb.google.com/lh/photo/gz28-yCSzQAFGd2XHTp_19MTjNZETYmyPJy0liipFm0?feat=embedwebsite)
[![Image](https://lh3.googleusercontent.com/-lUOCgxA-Y6Y/U67YGE90JnI/AAAAAAAAB5s/wPdvYmhag8Y/s640/IMG_2184.JPG)](https://picasaweb.google.com/lh/photo/lpNvfD7-fEVhoqr8FLwgu9MTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
9|0.1u|C-US025-025X050|C1, C2, C3, C7, C10, C15, C16, C17, C18

**Step 3** Ceramic capacitors. These are small yellow blobs and also have no polarity, so their orientation does not matter. There isn't enough room near the capacitors by the probe jacks (C15, C16, C17, C18) for the silkscreen so refer to the printed legend on the top of the board for information: 10k, 100k, 0.1u. This means the 0.1u capacitors go in the bottom holes of each three-component block.

[![Image](https://lh6.googleusercontent.com/-L9LYIBcubxI/U67YGpLZuSI/AAAAAAAAB50/m8jivB3hIVs/s640/IMG_2186.JPG)](https://picasaweb.google.com/lh/photo/k0w_9TNsYk_e7Bbn68u4W9MTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
1|1N4001|DIODE-DO41-7|D3
1|1N5819|DIODE-DO41-7|D2

**Step 4** Diodes. *There are two different diodes that look identical once installed so be sure to put the right diode in the right place.* The rectifier diodes have a white line on them to indicate their polarity and should be installed so their white line matches the white line marking on the PCB.

[![Image](https://lh6.googleusercontent.com/-759JrbdBLEw/U67YHDOHoVI/AAAAAAAAB54/PUwcf773v4M/s640/IMG_2187.JPG)](https://picasaweb.google.com/lh/photo/Cwv8LaaUEculV24xZQsvk9MTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
4|BS170|BS170|Q1, Q2 (**A+**), Q4, Q5
1|MCP1700-33|MCP1700-33|IC4

**Step 5** Signal MOSFETs and 3.3V regulator. These are the pieces that look like tiny black water towers with 3 legs. Bend the center lead back at a right angle to the body and then bend it down using your needle nose pliers. The flat front of these devices should be matched to the flat front on the silkscreen of the PCB.

**Raspberry Pi A+** Do not install Q2 at this time. See [[Pi APlus Modifications]]

[![Image](https://lh4.googleusercontent.com/-3kCmB7O2Odc/U68bJ77ZbWI/AAAAAAAAB7k/C1smNpcqQE8/s640/IMG_2204.JPG)](https://picasaweb.google.com/lh/photo/HLtZLpmOL5Sc5C0EPV6w4NMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
1|FQU11P06TU|MOSFET-P|Q3
1|74HC595N|74LS595N|IC3
1|DIP28|DIP28|IC2-SOCK

**Step 6** The power MOSFET Q3's leads can be easily formed to the right dimensions by simply inserting it into its hole then bending it down into position. Soldering the tab to the PCB is not required for the standard blower. Also install the 16 pin shift register (IC3) and the 28 pin DIP socket (IC2) for the microcontroller.  Both of these parts have a notch on one side of them which indicates the direction they need to be placed. Do not install the ATmega328P chip into socket IC2 at this time.

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
1|Pi|PINHD-2X13|JP1
1|ALARM|SPEAKER/AL11P|SP1 (**A+**)
1|OKI-78SR-5|OKI-78SR-05H|IC1
1|16MHz|RESONATORRESONATOR-PTH|Y1

**Step 7** Install these components in this order. The 26 pin RaspberryPi connector (PJ1), the piezo buzzer (SP1), the 5V regulator sub-board (IC1) and the larger 3 pin yellow blob 16MHz resonator. The orientation only matters on the 5V regulator.

**Raspberry Pi A+** Do not install SP1 at this time. See [[Pi APlus Modifications]]

[![Image](https://lh3.googleusercontent.com/-5Jthj9U9ehc/U68bKwB02cI/AAAAAAAAB70/_gTpsFh5QaE/s640/IMG_2211.JPG)](https://picasaweb.google.com/lh/photo/wBtPlrG5jtYI-P67PKRUGtMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
4|10k 1%|R-US_0204|R5, R16, R17, R18
4|100k|R-US_0204|R19, R22, R23, R28, R29

**Step 8** The leftover resistors from step 2 are installed now for each of the probe jacks. There isn't enough room on the PCB for the silkscreen, so again refer to the legend: 10k, 100k, 0.1u. The top pair of holes gets a 10k resistor in a vertical orientation, the middle pair of holes gets a 100k resistor in a vertical orientation, and the bottom pair of holes should already have a 0.1u capacitor in them. Do not install 10k resistor R18 in the pit jack if using a thermocouple.

[![Image](https://lh6.googleusercontent.com/-fIvAq_Di4uY/U68bLTPFP6I/AAAAAAAAB78/RSPokzz9oLs/s640/IMG_2214.JPG)](https://picasaweb.google.com/lh/photo/hO2_Eyr1LEdR-QSyS-lUjtMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
1|220u|INDUCTOR|L1
2|100u/10|CPOL-USE2.5-5|C5, C6
1|47u/25|CPOL-USE2.5-5|C12
1|100u/25|CPOL-USE2.5-6|C4

**Step 9** Power inductor and electrolytic capacitors. The inductor (L1) has no polarity, insert it in a haphazard manner. The capacitor "cans" have a line going down the side which indicates the negative side, the PCB has a teeny plus symbol to indicate the positive side. Use deductive reasoning to ascertain the correct orientation.

[![Image](https://lh5.googleusercontent.com/-GaAEl5HvPxM/U68bL1IeJaI/AAAAAAAAB8E/C_J6ydfnuwM/s640/IMG_2218.JPG)](https://picasaweb.google.com/lh/photo/xmHNuIZApxBk6k8dZ9_JUdMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
1|POW|POWER_JACKPTH|J9
1|RJ45-8|RJ45-8|JP2
1-4|Probes|AUDIO-MONO|JP3, JP4, JP5, JP6

**Step 10** Rounding out the bottom-side assembly are all the I/O jacks. You're in the home stretch now.

[![Image](https://lh3.googleusercontent.com/-na8IurIYOxg/U68bMr-RNQI/AAAAAAAAB8M/Z76l0QbJPiQ/s640/IMG_2220.JPG)](https://picasaweb.google.com/lh/photo/wk3zlvLTgNcYgoEaIrkghtMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
1|LCD|PINHD-1X16|J1
1|PINHD|PINHD|J1 (LCD), J2 (PROBE), J7 (ISCP), J8 (FTDI)

**Step 11** Preparing the LCD for attachment is involved enough that it has its own page: [[Preparing LCD for v4.2 Installation]]. Insert the LCD pins up through the bottom of the PCB and, just like in the LCD assembly, only solder pin 1. Check the alignment of the LCD: that its PCB is **flush** with the HeaterMeter PCB, and also **straight**. Touch the solder joint at pin 1 with the iron and adjust as necessary to perfection. 

### The LCD is installed facing the TOP side of the board, opposite of all the components installed so far

[![Image](https://lh4.googleusercontent.com/-n9I02ju_fb8/U68bMwtVwpI/AAAAAAAAB8U/vypn_sVephw/s640/IMG_2222.JPG)](https://picasaweb.google.com/lh/photo/RINxC6km6MyKr1A0xdm9S9MTjNZETYmyPJy0liipFm0?feat=embedwebsite)

Do the same procedure with soldering just pin 16 (and pin 1) to align the other side. Here is an example of what you **don't want it to look like**, to show how easy it is to fix because only pin 1 and 16 are soldered at this time

[![Image](https://lh5.googleusercontent.com/-OSCYMZqSR1U/U68bNXZgfsI/AAAAAAAAB8c/C1-wqTv5bWA/s640/IMG_2224.JPG)](https://picasaweb.google.com/lh/photo/H51bSeMeikaJbcuK9UsKgNMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

Just squeeze the two parts and touch pin 16 with the tip of the soldering iron and they'll pop right together. Straighten the LCD so it is flat and you're good to go with soldering the rest of the LCD pins.

[![Image](https://lh5.googleusercontent.com/-zRLJvfVPdrE/U68bOLG5jQI/AAAAAAAAB8k/QnZU6antWdU/s640/IMG_2228.JPG)](https://picasaweb.google.com/lh/photo/vk6G3fwlHihGnZlmQA0-ztMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
1|TACTILE-4|TACTILE-4|S1

**Step 12** Install the 4-way button on the top of the HeaterMeter PCB. The pins on this button are asymmetrical, which means it is designed to only go in one way. See how one set of pins is closer to one edge than the other? Make sure you put it in the PCB in the proper orientation.

[![Image](https://lh6.googleusercontent.com/-RIw3c32fwuA/U68bO1536OI/AAAAAAAAB8s/kG2k5T1f96s/s640/IMG_2230.JPG)](https://picasaweb.google.com/lh/photo/Cy4Wl0tAOz-Chibi0l8ggNMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
1|10k|TRIM_US-CT6|R6

**Step 13** The blue square LCD contrast potentiometer. Install this also on the top side of the board. Once the HeaterMeter software is installed on the AVR, you will need to adjust this until you can read the LCD. This corresponds to about 1.0V on pin 3 of the LCD connector. Aside from the LEDs, you're done soldering!

[![Image](https://lh6.googleusercontent.com/-Z1YfAiYhAAY/U68bPqHcgrI/AAAAAAAAB8w/OMmqVLMxxh8/s640/IMG_2233.JPG)](https://picasaweb.google.com/lh/photo/-6AqaKEpYogjr-OX4WBZAdMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
3|GRN|LED3MM|LED1, LED2, LED3

The LEDs need to be installed once you have a case ready. They are **not mounted flush with the PCB**. Insert the LEDs into the HeaterMeter case, place the PCB upside down on top of them, and solder. This guarantees they are the proper height with no measurement needed. The longer lead on the LED (the +/anode) is inserted into the hole closest to you. There's a little + sign to indicate this on LED1 but not the others, as that would get confusing with them all so close together.

The web UI has a red icon for LED1, yellow for LED2, green for LED3. Any arrangement can be used, but the web interface is fixed to displaying these colors.

***

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
1|ATmega328P|AVR-MEGA8-PPTH|IC2

Insert the ATmega328 into the IC2 socket by slightly bending all the legs against a flat surface then pressing into the socket. Be sure to match the direction using notch on the IC with the notch on the socket.

## Raspberry Pi A+ Finishing

If building for the Raspberry Pi Model A+, the steps at [[Pi APlus Modifications]] should be completed now.

## Preparing RaspberryPi for mating

The composite RCA jack on the RaspberryPi interferes with the HeaterMeter PCB in a way that is most unsatisfactory. It can be removed by desoldering it, but doing so chances damaging the nearby components with the amount of heat required to remove all the RCA jack solder. Simply clip the RCA jack off with wire cutters. It feels wrong to deface a brand new tiny computer like this but FFS, just save yourself the hassle. If you later decide you hate HeaterMeter and would rather have your composite video output (and you can find a display with composite in somehow), [Mouser carries RCA jacks in any color for 80 cents](http://www.mouser.com/ProductDetail/Switchcraft/PJRAN1X1U01X/?qs=%2fha2pyFaduhA2dCbClozE0M8thHp4IZMpitol3BhLqRLppD9blRIxA%3d%3d).

## Software Installation

Proceed to [[HeaterMeter 4.x Software]]