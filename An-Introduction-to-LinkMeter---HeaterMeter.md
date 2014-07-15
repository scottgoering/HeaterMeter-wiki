# An Introduction to LinkMeter / HeaterMeter
**HeaterMeter** (HM) is an AVR / Arduino microcontroller-based automatic BBQ controller.  Temperature data read from a standard "[Maverick](http://www.maverickhousewares.com/)" thermistor probe is used to adjust the speed of a blower fan motor mounted to the BBQ grill to maintain a specific set temperature point (setpoint).  Additional probes are used to monitor food and ambient temperatures, and these are displayed on a 16x2 LCD attached to the unit.  Buttons or serial commands can be used to adjust configuration of the device including adjustment of the setpoint or manually regulating fan speeds.

HeaterMeter can also refer to the project as a whole, including all the software and hardware to build a whole device.

[![Image](https://lh6.googleusercontent.com/-zNWDU0QO2_k/UWlyI-Jh_hI/AAAAAAAABJE/dRAlgRWU_-4/s640/IMG_1534.JPG)](https://picasaweb.google.com/lh/photo/17mo9yJedPl_wEQmEzimmNMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

**LinkMeter** (LM) extends the functionality of the HeaterMeter by mounting the microcontroller inside an OpenWrt-compatible SoC device.  The OpenWrt software provides a web server for monitoring and configuration as well as the storage necessary to provide history data in the form of a CSV log, or a javascript-generated graph. Host systems include:
*  RaspberryPi computer (HeaterMeter v4.0 - v4.2) Easiest, smallest, and most powerful current solution. Recommended for all new builds.
*  Linksys WRT54GL router (HeaterMeter v3.0 - v3.2) Original concept, still supported but difficult to set up, requires extra hardware to flash chips, and not enough RAM/storage to incorporate new features.

**LinkMeter Remote** (LMR) is an additional external device comprised of one or more temperature probes, a ATmega microcontroller, and an RFM12B 434/868/915MHz wireless transmitter. LMR transmits temperature data back to a HeaterMeter which has been built with the optional RFM12B receiver section. The temperature information replaces an internal HeaterMeter probe. This is useful for transmitting the temperature of a rotisserie (where  a cabled sensor would just get tangled up) or receiving the ambient temperature from a LaCrosse IT+ Wireless Weather Station.

## Cost

Cost for a pretty standard build with RaspberryPi (LinkMeter), SD card, wifi, power, fan, character LCD, and one probe (although you probably want more than that, one is required for reading Pit temperature). Other addons include thermocouple support (~$15 parts/shipping), RF receiver (~$10-15 PCB/parts/shipping), Servo for damper and damper parts (depends on your design).

|Description|Cost|
|-----------|----|
|Mouser Parts|$35+$5 shipping|
|DigiKey Parts|$19+$5 shipping|
|HeaterMeter PCB|$15|
|RaspberryPi|$37|
|4GB SD Card|$5|
|Wifi Adapter|$9|
|At least one probe|$15|
|12V Power adapter|$6|
|Ethernet cable|$1|
|Case|$25+$5 shipping (or 3D print your own)|
|Total|$182|