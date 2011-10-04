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

## Parts List

### Parts Complete Build

|Qty|Value     |Device                |Parts|
|---|----------|----------------------|-----|
1  |ATmega328P|AVR-MEGA8-PPTH        |IC2
1  |74HC164N  |74HC164N              |IC1
1  |16Mz      |RESONATOR-PTH         |Y1
1  |0         |R-US_0204/7           |R7
1  |390       |R-US_0204/7           |BTN-R7   
1  |680       |R-US_0204/7           |BTN-R8
5  |1k        |R-US_0204/7           |R1, R3, R4, R15, R19
3  |2.2k      |R-US_0204/7           |R8, R9, BTN-R9
6  |4.7k      |R-US_0204/7           |R2, R13, R22, R23, R24, BTN-R11
5  |10k       |R-US_0204/7           |R20, R21, R25, R26, R27
4  |10k 1%    |R-US_0204/7           |R5, R16, R17, R18
1  |10k       |TRIM_US-CT6           |R6
1  |10k       |THERMISTOR_R-2,5      |TR1
1  |0.01u     |C-US025-025X050       |C7
5  |0.1u      |C-US025-025X050       |C2, C3, C6, C9, C10
1  |22u/6.3   |CPOL-USE2.5-6         |C8
1  |22u/25    |CPOL-USE2.5-6         |C1
1  |100u/10   |CPOL-USE2.5-6         |C5
1  |100u/25   |CPOL-USE2.5-6         |C4
2  |1N4001    |DIODE-DO41-7          |D1, D2, D3
1  |1N5817    |DIODE-DO41-7          |D4
1  |IRL510    |PMOSFET_NTO220BV      |Q1
1  |RESET     |TAC_SWITCHPTH         |S1
1  |TACTILE-4 |TACTILE-4             |S2
1  |BC337     |BC337                 |Q2
1  |7805      |7805TV                |Q3
1  |MCP1700-33|MCP1700TRI            |Q4
1  |GRN       |LED3MM                |LED1
1  |RFM12B    |RFM12B                |U$1
1  |LCD_16X2  |TUXGR_16X2_R2         |DIS1
1  |LCD       |PINHD-1X16            |J1
1  |LCD       |PINHD-1X16            |P1
1  |PROBE     |PINHD-1X5             |J2
1  |PROBE     |PINHD-1X5             |P2
1  |BTN       |PINHD-1X2             |J3
1  |BTN       |PINHD-1X2             |P3
1  |BLW       |PINHD-1X2             |J4
1  |BLW       |PINHD-1X2             |P4
1  |RTR       |PINHD-1X5/90          |P5
1  |ICSP      |PINHD-2X3             |J6
1  |POW       |PINHD-1X2/90          |J7
1  |FTDI      |PINHD-1X6             |J8
1  |POW       |POWER_JACKPTH         |J9
1  |PIT       |DCJ0202               |JP3
1  |FOOD1     |DCJ0202               |JP4
1  |FOOD2     |DCJ0202               |JP5
1  |FOOD3/AMB |DCJ0202               |JP6

### Parts HeaterMeter Standalone

* Enclosure [Mouser](https://www.mouser.com/Search/ProductDetail.aspx?R=131-GRAYvirtualkey63500000virtualkey635-131-G)
* 12VDC/600mA power brick 5.5x2.1mm barrel jack. 500mA may be ok [Sparkfun](http://www.sparkfun.com/products/9442)
