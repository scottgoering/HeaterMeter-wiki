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

|Qty|Value     |Device                |Parts|Link|
|---|----------|----------------------|-----|----|
1  |ATmega328P|AVR-MEGA8-PPTH        |IC2|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=ATMEGA328P-PUvirtualkey55650000virtualkey556-ATMEGA328P-PU)
1  |74LS164N  |74LS164N              |IC1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=SN74LS164Nvirtualkey59500000virtualkey595-SN74LS164N)
1  |16Mz      |RESONATOR-PTH         |Y1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=AWCR-16.00MDvirtualkey52750000virtualkey815-AWCR-16.00MD)
1  |0         |R-US_0204/7           |R7|AKA a wire
1  |390       |R-US_0204/7           |BTN-R7|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MF1%2f4DC3900Fvirtualkey66000000virtualkey660-MF1%2f4DC3900F)
1  |680       |R-US_0204/7           |BTN-R8|[Mouser](http://www.mouser.com/ProductDetail/KOA-Speer/MF1-4DC6800F/?qs=sGAEpiMZZMu61qfTUdNhG0RUkTLGOdTMWpMLGFKzzSg%3d)
5  |1k        |R-US_0204/7           |R1, R3, R4, R15, R19|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MF1%2f4DC1001Fvirtualkey66000000virtualkey660-MF1%2f4DC1001F)
3  |2.2k      |R-US_0204/7           |R8, R9, BTN-R9|[Mouser](http://www.mouser.com/ProductDetail/KOA-Speer/MF1-4DC2201F/?qs=sGAEpiMZZMu61qfTUdNhG2r2Nmyl%2fOMiJPrwMFCn50I%3d)
6  |4.7k      |R-US_0204/7           |R2, R13, R22, R23, R24, BTN-R11|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MF1%2f4DC4701Fvirtualkey66000000virtualkey660-MF1%2f4DC4701F)
5  |10k       |R-US_0204/7           |R20, R21, R25, R26, R27|Use %1 below
4  |10k 1%    |R-US_0204/7           |R5, R16, R17, R18|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MF1%2f4DC1002Fvirtualkey66000000virtualkey660-MF1%2f4DC1002F)
1  |10k       |TRIM_US-CT6           |R6|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=T73YE103KT20virtualkey61330000virtualkey72-T70YE-10K)
1  |10k       |THERMISTOR_R-2,5      |TR1|xxx
1  |0.01u     |C-US025-025X050       |C7|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=K103K15X7RF53L2virtualkey59420000virtualkey594-K103K15X7RF53L2)
5  |0.1u      |C-US025-025X050       |C2, C3, C6, C9, C10|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=K104K15X7RF53L2virtualkey59420000virtualkey594-K104K15X7RF53L2)
1  |22u/6.3   |CPOL-USE2.5-6         |C8|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=UMR0J220MCD2virtualkey64700000virtualkey647-UMR0J220MCD2)
1  |22u/25    |CPOL-USE2.5-6         |C1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=UPW1E220MDD6virtualkey64700000virtualkey647-UPW1E220MDD6)
1  |47u/10   |CPOL-USE2.5-6          |C5|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=UHC1A470MDDvirtualkey64700000virtualkey647-UHC1A470MDD)
1  |47u/25   |CPOL-USE2.5-6          |C4|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=UHC1E470MDDvirtualkey64700000virtualkey647-UHC1E470MDD)
3  |1N4001    |DIODE-DO41-7          |D1, D2, D3|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=1N4001GP-E3%2f73virtualkey61370000virtualkey625-1N4001GP-E3%2f73)
1  |1N5817    |DIODE-DO41-7          |D4|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=VS-1N5817virtualkey61370000virtualkey844-1N5817)
1  |IRL510    |PMOSFET_NTO220BV      |Q1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=FDP7030BLvirtualkey51210000virtualkey512-FDP7030BL)
1  |RESET     |TAC_SWITCHPTH         |S1|[Mouser](http://www.mouser.com/ProductDetail/Mountain-Switch/101-TS6111T1602-EV/?qs=tOxFRg%2fqIe3Emt9e4hH6fA%3d%3d)
1  |TACTILE-4 |TACTILE-4             |S2|[Mouser](http://www.mouser.com/ProductDetail/ALPS/SKQUAAA010/?qs=oKW7zmyQiO62qWuFl5QVBw%3d%3d)
1  |BC337     |BC337                 |Q2|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=BC33725BUvirtualkey51210000virtualkey512-BC33725BU)
1  |7805      |7805TV                |Q3|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=KA7805AETUvirtualkey51210000virtualkey512-KA7805AETU)
1  |MCP1700-33|MCP1700TRI            |Q4|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MCP1700-3302E%2fTOvirtualkey57940000virtualkey579-MCP1700-3302E%2fTO)
1  |GRN       |LED3MM                |LED1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=WP7104GDvirtualkey60400000virtualkey604-WP7104GD)
1  |RFM12B    |RFM12B                |U$1|[ModernDevice](http://shop.moderndevice.com/products/rfm12b-radio)
1  |LCD_16X2  |TUXGR_16X2_R2         |DIS1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=NHD-0216K1Z-NSW-FBW-Lvirtualkey66010000virtualkey763-0216K1Z-NSW-FBW)

|Qty|Device                |Parts|Link|
|---|----------------------|-----|----|
1  |Male PINHD single row       |J1(LCD), J2(PROBE), J3(BTN), J4(BLW), J8(FTDI) |[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=68016-236HLFvirtualkey64910000virtualkey649-68016-236HLF)
3  |CONHOUSE single row 5-pin |P1(LCD 2x),P2(PROBE)|[Pololu](http://www.pololu.com/catalog/product/1904)
2  |CONHOUSE single row 2-pin |P3(BTN),P4(BLW)|[Pololu](http://www.pololu.com/catalog/product/1901)
1  |Female PINHD 1X6/90       |P5(RTR)|xxx
1  |Male PINHD 2x3             |J6(ICSP)|[Mouser](http://www.mouser.com/ProductDetail/3M/961206-6404-AR/?qs=A%252btsDZJT%252bi%2ft%2f4aaelvU3g%3d%3d)
1  |Male PINHD single row/90   |J7(POW)|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=68423-236virtualkey64910000virtualkey649-68423-236)
1  |2.1mm POWER_JACKPTH         |J9(POW)|xxx
4  |Mono 2.5mm female jack      |JP3(PIT), JP4(FOOD1), JP5(FOOD2), JP6(FOOD3/AMB)|xxx
1  | Crimp pins female x100     | N/A | [Pololu](http://www.pololu.com/catalog/product/1930)

[Mouser Project](http://www.mouser.com:80/ProjectManager/ProjectDetail.aspx?AccessID=17a758cf63) for all Mouser parts listed above $26.44

### Parts HeaterMeter Standalone

* Enclosure [Mouser](https://www.mouser.com/Search/ProductDetail.aspx?R=131-GRAYvirtualkey63500000virtualkey635-131-G)
* 12VDC/600mA power brick 5.5x2.1mm barrel jack. 500mA may be ok [Sparkfun](http://www.sparkfun.com/products/9442)
