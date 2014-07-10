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

## Thermocouple Installation

If building the Thermocouple Pit Probe variant of the HeaterMeter, the surface mount components should be assembled and tested ([[Thermocouple Amplifier Testing]]) before starting the through-hole assembly. Note that you will not install the standard Pit jack (2.5mm audio) or the 10k 1% pullup resistor (R18) closest to the Pit jack.

## Software Installation

See: [[HeaterMeter 4.0 Software]]