As a reminder, HeaterMeter refers to the ATmega (Arduino) based microcontroller board that runs the LCD, reads button and temperature probe inputs, and controls the blower motor. This document describes the configurations and design of the HeaterMeter board, which may optionally be installed into an OpenWrt-compatible router to become a LinkMeter.

Standard HeaterMeter hardware is built on a [HeaterMeter V3.2 PCB](http://capnbry.net/linkmeter/pcb/hm-3.2/)

* [Schematic Image](http://capnbry.net/linkmeter/pcb/hm-3.2/LinkMeterHM.png)
* EAGLE 5 [schematic](http://capnbry.net/linkmeter/pcb/hm-3.2/LinkMeterHM.sch) and [board](http://capnbry.net/linkmeter/pcb/hm-3.2/LinkMeterHM.brd)
* [External Connections probes/LCD](http://capnbry.net/linkmeter/pcb/hm-3.2/LinkMeterHM-External.png)
* [Button Board](http://capnbry.net/linkmeter/pcb/hm-3.2/LinkMeterHM-Button.png)
* DorkBot [cam job](http://capnbry.net/linkmeter/pcb/hm-3.2/LinkMeter-Dorkbot.cam) or [cam output](http://capnbry.net/linkmeter/pcb/hm-3.2/LinkMeterHM-V3.2-DorkBot.zip). Use cam output if you just want a board made with no modifications
* [README](http://capnbry.net/linkmeter/pcb/hm-3.2/README-V3.2.txt) description of files
* [ZIP containing all the above](http://capnbry.net/linkmeter/pcb/hm-3.2/hm-3.2.zip)

## Configurations 

There are two possible major HeaterMeter configurations.  Both designs are fully interchangeable but some components can omitted if not needed.

### Standalone HeaterMeter

Original HeaterMeter configuration for use without an OpenWrt router. Provides automatic grill control, and LCD display. Initial configuration is via serial commands. Set Point, manual fan mode, probe offsets, open lid detect and max fan speed configurable via buttons. There is integrated **no web access or graphs**, but there is a serial status output to allow you to roll your own solution.

Standalone HeaterMeter adds a barrel power jack and can omit the pinhead power jack, router serial output, and self-reset circuit.

### HeaterMeter for LinkMeter

The HM for LM (HM4LM) configuration doesn't need the barrel power jack, and adds a pinhead power jack, router serial output, and self-reset circuit. HM4LM still runs the ATmega microcontroller at 5V supply, however the design can be adapted for pure 3.3V supply, which runs off the 3.3V from the router. 5V is used for better ADC resolution and for use with a 5V LCD display, which seem to be more prevalent than their 3.3V counterparts.

## Parts List

### Parts Complete Build V3.2 PCB

|Qty|Value     |Device                |Parts|Link|
|---|----------|----------------------|-----|----|
1  |ATmega328P|AVR-MEGA8-PPTH        |IC2|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=ATMEGA328P-PUvirtualkey55650000virtualkey556-ATMEGA328P-PU)
1  |74HC595N  |74HC595N              |IC3|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=SN74HC595Nvirtualkey59500000virtualkey595-SN74HC595N)
1  |16Mz      |RESONATOR-PTH         |Y1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=AWCR-16.00MDvirtualkey52750000virtualkey815-AWCR-16.00MD)
1  |0         |R-US_0204/7           |R7|AKA a wire
1  |390       |R-US_0204/7           |BTN-R7|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MF1%2f4DC3900Fvirtualkey66000000virtualkey660-MF1%2f4DC3900F)
1  |680       |R-US_0204/7           |BTN-R8|[Mouser](http://www.mouser.com/ProductDetail/KOA-Speer/MF1-4DC6800F/?qs=sGAEpiMZZMu61qfTUdNhG0RUkTLGOdTMWpMLGFKzzSg%3d)
4  |1k        |R-US_0204/7           |R1, R3, R15, R19|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MF1%2f4DC1001Fvirtualkey66000000virtualkey660-MF1%2f4DC1001F)
1  |2.2k      |R-US_0204/7           |BTN-R9|[Mouser](http://www.mouser.com/ProductDetail/KOA-Speer/MF1-4DC2201F/?qs=sGAEpiMZZMu61qfTUdNhG2r2Nmyl%2fOMiJPrwMFCn50I%3d)
6  |4.7k      |R-US_0204/7           |R2, R13, R22, R23, R24, BTN-R11|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MF1%2f4DC4701Fvirtualkey66000000virtualkey660-MF1%2f4DC4701F)
5  |10k       |R-US_0204/7           |R20, R21, R25, R26, R27|Use %1 below
4  |10k 1%    |R-US_0204/7           |R5, R16, R17, R18|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MF1%2f4DC1002Fvirtualkey66000000virtualkey660-MF1%2f4DC1002F)
1  |10k       |TRIM_US-CT6           |R6|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=T73YE103KT20virtualkey61330000virtualkey72-T70YE-10K)
1  |10k       |THERMISTOR_R-2,5      |TR1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=NTCLE203E3103FB0virtualkey59420000virtualkey594-2381-640-55103)
1  |0.01u     |C-US025-025X050       |C7|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=K103K15X7RF53L2virtualkey59420000virtualkey594-K103K15X7RF53L2)
5  |0.1u      |C-US025-025X050       |C2, C3, C6, C9, C10|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=K104K15X7RF53L2virtualkey59420000virtualkey594-K104K15X7RF53L2)
1  |22u/6.3   |CPOL-USE2.5-6         |C8|[Mouser](http://www.mouser.com/ProductDetail/Nichicon/USA0J220MDD/?qs=62ecY7oL%252bWMOv1D%2fKxxjwQ%3d%3d)
1  |22u/25    |CPOL-USE2.5-6         |C1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=UPW1E220MDD6virtualkey64700000virtualkey647-UPW1E220MDD6)
1  |47u/10   |CPOL-USE2.5-6          |C5|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=UHC1A470MDDvirtualkey64700000virtualkey647-UHC1A470MDD)
1  |47u/25   |CPOL-USE2.5-6          |C4|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=UHC1E470MDDvirtualkey64700000virtualkey647-UHC1E470MDD)
2  |1N4001    |DIODE-DO41-7          |D1, D3|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=1N4001GP-E3%2f73virtualkey61370000virtualkey625-1N4001GP-E3%2f73)
1  |1N5817    |DIODE-DO41-7          |D4|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=VS-1N5817virtualkey61370000virtualkey844-1N5817)
1  |IRL510    |PMOSFET_NTO220BV      |Q1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=FDP7030BLvirtualkey51210000virtualkey512-FDP7030BL)
1  |RESET     |TAC_SWITCHPTH         |S1|[Mouser](http://www.mouser.com/ProductDetail/Mountain-Switch/101-TS6111T1602-EV/?qs=tOxFRg%2fqIe3Emt9e4hH6fA%3d%3d)
1  |TACTILE-4 |TACTILE-4             |S2|[Mouser](http://www.mouser.com/ProductDetail/ALPS/SKQUAAA010/?qs=oKW7zmyQiO62qWuFl5QVBw%3d%3d)
1  |BC337     |BC337                 |Q2|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=BC33725BUvirtualkey51210000virtualkey512-BC33725BU)
1  |7805      |7805TV                |Q3|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=KA7805AETUvirtualkey51210000virtualkey512-KA7805AETU)
1  |MCP1700-33|MCP1700TRI            |Q4|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MCP1700-3302E%2fTOvirtualkey57940000virtualkey579-MCP1700-3302E%2fTO)
1  |GRN       |LED3MM                |LED1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=WP7104GDvirtualkey60400000virtualkey604-WP7104GD)
1  |RFM12B    |RFM12B                |U$1|[ModernDevice](http://shop.moderndevice.com/products/rfm12b-radio) Extremely optional!
1  |LCD_16X2  |TUXGR_16X2_R2         |DIS1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=NHD-0216K1Z-NSW-FBW-Lvirtualkey66010000virtualkey763-0216K1Z-NSW-FBW)

### Interconnects

|Qty|Device                |Parts|Link|
|---|----------------------|-----|----|
1  |Male PINHD single row       |J1(LCD), J2(PROBE), J3(BTN), J4(BLW), J8(FTDI) |[Mouser](http://www.mouser.com/ProductDetail/FCI/68001-236HLF/?qs=sGAEpiMZZMtsLRyDR9nM14Vjyw4ze%252bjt57BsII4P7vM%3d) 0.23" mate/0.12" tail/15u gold
2  |CONHOUSE single row 6-pin |P1(LCD 2x)|[Pololu](http://www.pololu.com/catalog/product/1905) (or 6x 2-pins)
1  |CONHOUSE single row 5-pin |P2(PROBE)|[Pololu](http://www.pololu.com/catalog/product/1904)
2  |CONHOUSE single row 2-pin |P3(BTN),P4(BLW)|[Pololu](http://www.pololu.com/catalog/product/1901)
1  |Female PINHD 1X6/90       |P5(RTR)|[DigiKey](http://search.digikey.com/us/en/products/PPTC051LGBN-RC/S5441-ND/775899)
1  |Male PINHD 2x3             |J6(ICSP)|[Mouser](http://www.mouser.com/ProductDetail/3M/961206-6404-AR/?qs=A%252btsDZJT%252bi%2ft%2f4aaelvU3g%3d%3d)
1  |Male PINHD single row/90   |J7(POW), PX5(RTR External)|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=68016-236HLFvirtualkey64910000virtualkey649-68016-236HLF)
1  | Crimp pins female x100     | N/A | [Pololu](http://www.pololu.com/catalog/product/1930)
1  |2.1mm POWER_JACKPTH         |J9(POW)|[Mouser](http://www.mouser.com/ProductDetail/Kobiconn/163-7620-E/?qs=8xMK%252bwDsXhcfMNb%2fYnnwLQ%3d%3d)
4  |Mono 2.5mm female jack      |JP3(PIT), JP4(FOOD1), JP5(FOOD2), JP6(FOOD3/AMB)|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=161-0250-Evirtualkey11180000virtualkey161-0250-E)
1  |RCA Female jack             |JX4(BLOWER External)|[Mouser](http://www.mouser.com/ProductDetail/Kobiconn/161-2052/?qs=sGAEpiMZZMvlX3nhDDO4AKpXrDFhuRMhW4e%252blHGol2Q%3d)

### Probes and Fan
|Qty|Description|Link|
|---|-----------|----|
1 | Blower-style fan 12VDC 5-10CFM | [DigiKey](http://search.digikey.com/us/en/products/BFB0612H/603-1117-ND/1014448)
1-4 | Maverick BBQ Thermistor Probes (3ft or High Heat) | [Maverick](http://www.maverickhousewares.com/parts_and_service.htm)

[Mouser Project](http://www.mouser.com:80/ProjectManager/ProjectDetail.aspx?AccessID=675aef15ec) for all Mouser parts listed above $34.08

### Parts HeaterMeter Standalone

* Enclosure [Mouser](https://www.mouser.com/Search/ProductDetail.aspx?R=131-GRAYvirtualkey63500000virtualkey635-131-G)
* 12VDC/600mA power brick 5.5x2.1mm barrel jack. 500mA may be ok [Sparkfun](http://www.sparkfun.com/products/9442)

## Wireless Probe Support

To use wireless probes, a RFM12B receiver needs to be added to the design. These parts are included in the list above. The default code assumes a 915MHz transceiver, which is only legal in the United States, but a one-line code change facilitates using 433MHz or 868MHz bands to comply with other local regulations. In the Standalone HeaterMeter configuration, an additional 3.3V power supply needs to be added to power the transceiver. The 3.3V regulator is not needed in the HM4LM configuration.

If you do not wish to have wireless probe support you can omit a large number of parts: R22 through R27, U$1, Q4, C8 and C9. R15 and LED1 are also optional but recommended for debugging purposes because LED1 is blinked once before initialization and once after.