# What is a bootloader?
The HeaterMeter bootloader is the bit of software that runs on the ATmega microcontroller before the HeaterMeter software does. A blank from the factory ATmega chip used can only be programmed via the SPI bus, generally using the ICSP header. Because most communication with the microcontroller takes place over the Serial UART, either via an FTDI USB Serial Converter or the Router's TTL Serial ports, a bootloader is usually added which adds the ability to flash a program over this Serial UART. Optiboot is a 512 byte bootloader which converts a serial variant of the stk500v1 protocol to the necessary page_fill()/page_write() commands to program the ATmega.

## Getting Optiboot on ATmega
Because we want to be able to flash programs over serial, we need to either get a chip with a bootloader on it or install it ourselves. There are a lot more ways to do this than are presented here. Our ultimate goal is to have a chip with the Optiboot 4.4 bootloader or above, which is the one included with Arduino-1.0. The Optiboot that ships with Arduino-0022 has a bug in it which can prevent HeaterMeter from fully booting properly.

### Buy a chip with the bootloader already installed
Chips which come from Mouser or DigiKey are completely blank, fresh from the factory. As a service to folks who are looking to use them in Arduino-style projects, hobbyist stores provide ATmega chips with the Optiboot bootloader on them already for a small markup. (~$3.50 Mouser cost, ~$4.30 Sparkfun cost, ~$5.50 Sparkfun preloded cost) This is usually the most economical solution for users who aren't going to be building a lot of projects.

[Sparkfun](http://www.sparkfun.com/products/10524)

### Build an ICSP programmer
The next option is to build a specialized ICSP programmer capable of flashing any program to the ATmega chip, including a bootloader. There are literally hundreds of ICSP programming circuits all over the Internet. One circuit, designed for programming ATmegas is the [USBtinyISP](https://www.adafruit.com/products/46) ($22). This programmer has the advantage of being natively supported by the Arduino development environment. 

To burn the bootloader using USBtinyISP, assemble the HeaterMeter board and hook the USBtinyISP to the ICSP header. Do not have your HeaterMeter board plugged in to anything else! From the Arduino IDE, select:

1. Tools -> Board -> Arduino Uno
1. Tools -> Programmer -> USBtinyISP
1. Tools -> Burn Bootloader
1. Wait about 2 minutes

### Program from an Arduino
This technique is most economical for people who already own an Arduino Duemilanove or Diecimila (or possibly an Uno). Set up the circuit as described in [Arduino as ISP](http://arduino.cc/en/Tutorial/ArduinoISP) breadboard section. You can either use a breadboard or an [assembled HeaterMeter board ICSP header](https://lh3.googleusercontent.com/-NJfXjitiqxA/Tx8G8kK9jvI/AAAAAAAAAoo/k9vy10KXHZI/s800/hm-icsp-pins.jpg). 

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

### Program from any ATmega
You can use the same circuit as above, but instead flash the host chip with the [Optiloader sketch](https://github.com/WestfW/OptiLoader). Optiloader is a sketch that checks for a chip connected to it via the SPI bus, and flashes Optiboot on it.

1. Tools -> Board -> Select your host chip (the Duemilanove or Diecimila or Uno)
1. Upload Optiloader
1. Assemble the appropriate flashing circuit
1. Apply power. Optiloader will immediately begin flashing as soon as it powers up. You can open the Serial Monitor at 19200 baud to watch the progress.
1. Wait about 5 seconds. Optiloader will tell you when it is done. ```Type 'G' or hit RESET for next chip```