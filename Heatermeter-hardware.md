(Still working on this page)

As a reminder, HeaterMeter refers to the ATmega (Arduino) based microcontroller board that runs the LCD, reads button and temperature probe inputs, and controls the blower motor. This document describes the configurations and design of the HeaterMeter board, which may optionally be installed into an OpenWrt-compatible router to become a LinkMeter.

Official hardware is still being determined pending sample circuit boards coming back from the PCB manufacturer (design sent 2011-9-26). The approximate design can be found in the git /eagle/ directory, however this will get a couple tweaks possibly. 

## Configurations

There are two possible major HeaterMeter configurations.  Both designs are fully interchangeable but some components can omitted if not needed.

### Standalone HeaterMeter 

Original HeaterMeter configuration for use without an OpenWrt router. Provides automatic grill control, and LCD display. Initial configuration is via serial commands. Set Point, manual fan mode, probe offsets, open lid detect and max fan speed configurable via buttons. There is integrated **no web access or graphs**, but there is a serial status output to allow you to roll your own solution.

Standalone HeaterMeter adds a barrel power jack and can omit the pinhead power jack, router serial output, and self-reset circuit.

### HeaterMeter for LinkMeter

The HM for LM (HM4LM) configuration doesn't need the barrel power jack, and adds a pinhead power jack, router serial output, and self-reset circuit. HM4LM still runs the ATmega microcontroller at 5V supply, however the design can be adapted for pure 3.3V supply, which runs off the 3.3V from the router. 5V is used for better ADC resolution and for use with a 5V LCD display, which seem to be more prevalent than their 3.3V counterparts.

## Wireless Probe Support

To use wireless probes, a RFM12B receiver needs to be added to the design. The default code assumes a 915MHz transceiver, which is only legal in the United States, but a one-line code change facilitates using 433MHz or 868MHz bands to comply with other local regulations. In the Standalone HeaterMeter configuration, an additional 3.3V power supply needs to be added to power the transceiver. The 3.3V regulator is not needed in the HM4LM configuration.

Qty|Value|Device|Parts
---|-----|------|-----
1|ATmega328P|AVR-MEGA8-PPTH|IC2
Some description||
