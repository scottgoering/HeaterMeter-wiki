# What is a bootloader?
The HeaterMeter bootloader is the bit of software that runs on the ATmega microcontroller before the HeaterMeter software does. A blank from the factory ATmega chip used can only be programmed via the SPI bus, generally using the ICSP header. Because most communication with the microcontroller takes place over the Serial UART, either via an FTDI USB Serial Converter or the Router's TTL Serial ports, a bootloader is usually added which adds the ability to flash a program over this Serial UART. Optiboot is a 512 byte bootloader which converts a serial variant of the stk500v1 protocol to the necessary page_fill()/page_write() commands to program the ATmega.

**Note:  Bootloader is not required with HeaterMeter 4.0 with Raspberry Pi**
When used with the RaspberryPi, the ATmega328P-PU without the bootloader is fine. The chip is programmed using the rPi's GPIO lines as an SPI programmer so any bootloader on it will actually be erased when HeaterMeter is flashed from the web interface / avrupdate. It's one of the bigger features of the new HM4+rPi platform; no ISP programmer / bootloader needed!

## Getting Optiboot on ATmega
Because we want to be able to flash programs over serial, we need to either get a chip with a bootloader on it or install it ourselves. There are a lot more ways to do this than are presented here. Our ultimate goal is to have a chip with the Optiboot 4.4 bootloader or above, which is the one included with Arduino-1.0. The Optiboot that ships with Arduino-0022 has a bug in it which can prevent HeaterMeter from fully booting properly.

### Buy a chip with the bootloader already installed
Chips which come from Mouser or DigiKey are completely blank, fresh from the factory. As a service to folks who are looking to use them in Arduino-style projects, hobbyist stores provide ATmega chips with the Optiboot bootloader on them already for a small markup. (~$3.50 Mouser cost, ~$4.30 Sparkfun cost, ~$5.50 Sparkfun preloded cost) This is usually the most economical solution for users who aren't going to be building a lot of projects.

[Sparkfun](http://www.sparkfun.com/products/10524)
[Virtuabotix](http://www.amazon.com/gp/product/B007SH0D0A/ref=oh_details_o01_s00_i00)

## Flash it yourself

### Terminology
 * **Target** the target chip/board is the device you want to put the bootloader on (i.e. the blank HeaterMeter ATmega)
 * **Host** a host board is a system which already has a bootloader or some means to upload code from your PC / the Arduino IDE. Usually an Arduino Uno, Duemilanove or Diecimila, Boardadino with FTDI cable, etc.

### Build an ICSP programmer
The next option is to build a specialized ICSP programmer capable of flashing any program to the ATmega chip, including a bootloader. There are literally hundreds of ICSP programming circuits all over the Internet. One circuit, designed for programming ATmegas is the [USBtinyISP](https://www.adafruit.com/products/46) ($22). This programmer has the advantage of being natively supported by the Arduino development environment. 

To burn the bootloader using USBtinyISP, assemble the HeaterMeter board and hook the USBtinyISP to the ICSP header. Do not have your HeaterMeter board plugged in to anything else! From the Arduino IDE, select:

1. Tools -> Board -> Arduino Uno
1. Tools -> Programmer -> USBtinyISP
1. Tools -> Burn Bootloader
1. Wait about 2 minutes

### Program from any ATmega (Optiloader)
If you have any other ATmega-based device you can upload sketches to, this is your preferred solution. Basically, you'll upload a sketch (Optiloader) to your working device, connect 6 wires to your target, and power up the host. Optiloader is a sketch that checks for a chip connected to it via the SPI bus, and flashes Optiboot on it.

1. Tools -> Board -> Select your host chip (the Duemilanove or Diecimila or Uno)
1. Upload the [Optiloader sketch](https://github.com/WestfW/OptiLoader)
1. Unplug the host board and assemble the appropriate flashing circuit, 6 wires: [Left](https://picasaweb.google.com/lh/photo/sIp0U6P-ymAEn20Szpws3dMTjNZETYmyPJy0liipFm0?feat=directlink) - [Right](https://picasaweb.google.com/115791887386052258127/HeaterMeter#5708097875420887186) - [Overview](https://picasaweb.google.com/lh/photo/ruAn7DhzuppVRDt6mVwCRtMTjNZETYmyPJy0liipFm0?feat=directlink) or use the [Arduino as ISP](http://arduino.cc/en/Tutorial/ArduinoISP) breadboard section.
1. Apply power. Optiloader will immediately begin flashing as soon as it powers up. You can open the Serial Monitor at 19200 baud to watch the progress.
1. Wait about 5 seconds. Optiloader will tell you when it is done. ```Type 'G' or hit RESET for next chip```

### Program from an Arduino
This technique is the traditional way to flash a bootloader using an Arduino Duemilanove or Diecimila (or possibly an Uno). Use the circuit above, except 5V on the target should run to 5V on the host. Additional circuit diagrams are shown on the  [Arduino as ISP](http://arduino.cc/en/Tutorial/ArduinoISP) page. This method is much slower than the "Program from any ATmega" method and may require additional capacitors to prevent reset, and gosh there's just so many things that can go wrong I can't imagine why anyone would want to use it. Still, it is the semi-official Arduino way [which is awful] so it is included here for academics.

1. Edit (your Arduino directory)/hardware/arduino/programmers.txt and change ```arduinoisp.speed=19200``` to ```arduinoisp.speed=9600```
1. Close all open Arduino windows, and restart the Arduino IDE
1. Tools -> Board -> Select your host chip (the Duemilanove or Diecimila)
1. File -> Examples -> ArduinoISP
1. Change ```Serial.begin(19200);``` to ```Serial.begin(9600);``` (around line 69)
1. Upload
1. Assemble the appropriate flashing circuit
1. Disable your host chip auto-reset feature by placing a 10u or higher capacitor between RESET and GND.
1. Tools -> Board -> Arduino Uno (**UNO, not the host board**)
1. Tools -> Programmer -> Arduino as ISP
1. Tools -> Burn Bootloader
1. Wait a couple minutes

Building the circuit can be simplified by using a shield designed for such a purpose, such as the [Evil Mad Science ISP Shield](http://evilmadscience.com/productsmenu/tinykitlist/253)