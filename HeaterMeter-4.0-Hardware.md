As a reminder, HeaterMeter refers to the ATmega (Arduino) based microcontroller board that runs the LCD, reads button and temperature probe inputs, and controls the blower motor. This document describes the configurations and design of the HeaterMeter board, which may optionally be attached to a Raspberry Pi. For connecting directly to a Linksys router, use [[HeaterMeter 3.0 Hardware]].

Standard HeaterMeter hardware is built on a [HeaterMeter v4.0 PCB](http://capnbry.net/linkmeter/pcb/hm-4.0/)

* [Buy direct](http://store.oshpark.com/products/heatermeter-v4-0) from OSH Park
* [Schematic Image](http://capnbry.net/linkmeter/pcb/hm-4.0/HeaterMeterPI.png)
* EAGLE 5 [schematic](http://capnbry.net/linkmeter/pcb/hm-4.0/HeaterMeterPI.sch) and [board](http://capnbry.net/linkmeter/pcb/hm-4.0/HeaterMeterPI.brd)
* DorkBot/OSH Park [cam job](http://capnbry.net/linkmeter/pcb/hm-4.0/HeaterMeter-Dorkbot.cam) or [cam output](http://capnbry.net/linkmeter/pcb/hm-4.0/HeterMeter-v4.0-DorkBot.zip). Use cam output if you just want a board made with no modifications

## Configurations 

HeaterMeter can be built either as a standalone or for integration with a [Raspberry Pi](http://www.newark.com/raspberry-pi-accessories). The only difference between the two is the population of the Pi socket JP1. The 3.3V voltage regulator is not _required_ when connecting to the Pi, but it is when operating standalone. Both configurations provide automatic grill control, and LCD display. Set Point, manual fan mode, probe offsets, open lid detect and max fan speed configurable via buttons. The standalone requires initial configuration via serial commands. There is integrated **no web access or graphs** in standalone mode, but there is a serial status output to allow you to roll your own solution.

**Quick and Easy**: [Mouser parts](http://www.mouser.com/ProjectManager/ProjectDetail.aspx?AccessID=0dba74d92d). Does not include DigiKey-only parts 1x[Blower](http://search.digikey.com/us/en/products/BFB0612H/603-1117-ND/1014448) 1x[Socket](http://www.digikey.com/product-detail/en/PPPC132LFBN-RC/S7116-ND/810252) 4x[Jacks](http://www.digikey.com/product-detail/en/MJ-2508N/CP-2508N-ND/281260)

### Main Board
|Qty|Value     |Device                |Parts|Link|
|---|----------|----------------------|-----|----|
1|0|R-US_0204/7|R7|(wire)
4|390|R-US_0204/7|R2, R10, R12, R15|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MF1%2f4DC3900Fvirtualkey66000000virtualkey660-MF1%2f4DC3900F) [DigiKey](http://www.digikey.com/product-detail/en/CF14JT390R/CF14JT390RCT-ND/1830340)
1|680|R-US_0204/7|R8|[Mouser](http://www.mouser.com/ProductDetail/KOA-Speer/MF1-4DC6800F/?qs=sGAEpiMZZMu61qfTUdNhG0RUkTLGOdTMWpMLGFKzzSg%3d) [DigiKey](http://www.digikey.com/product-detail/en/CF14JT680R/CF14JT680RCT-ND/1830346)
3|1k|R-US_0204/7|R1, R3, R4|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MF1%2f4DC1001Fvirtualkey66000000virtualkey660-MF1%2f4DC1001F) [DigiKey](http://www.digikey.com/product-detail/en/CF14JT1K00/CF14JT1K00CT-ND/1830350)
2|2k2|R-US_0204/7|R9, R13|[Mouser](http://www.mouser.com/ProductDetail/KOA-Speer/MF1-4DC2201F/?qs=sGAEpiMZZMu61qfTUdNhG2r2Nmyl%2fOMiJPrwMFCn50I%3d) [DigiKey](http://www.digikey.com/product-detail/en/CF14JT2K20/CF14JT2K20CT-ND/1830358)
1|4k7|R-US_0204/7|R11|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MF1%2f4DC4701Fvirtualkey66000000virtualkey660-MF1%2f4DC4701F) [DigiKey](http://www.digikey.com/product-detail/en/CF14JT4K70/CF14JT4K70CT-ND/1830366)
1|10k|R-US_0204/7|R20|(use below)
4|10k 1%|R-US_0204/7|R5, R16, R17, R18|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MF1%2f4DC1002Fvirtualkey66000000virtualkey660-MF1%2f4DC1002F) [DigiKey](http://www.digikey.com/product-detail/en/RNF14FTD10K0/RNF14FTD10K0CT-ND/1975090)
1|10k|TRIM_US-CT6|R6|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=T73YE103KT20virtualkey61330000virtualkey72-T70YE-10K) [DigiKey](http://www.digikey.com/product-detail/en/3362P-1-103LF/3362P-103LF-ND/1088412)
3|0.1u|C-US025-025X050|C2, C3, C10|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=K104K15X7RF53L2virtualkey59420000virtualkey594-K104K15X7RF53L2) [DigiKey](http://www.digikey.com/product-detail/en/K104K15X7RF5TL2/BC1084CT-ND/286706)
1|22u/25|CPOL-USE2.5-6|C1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=UPW1E220MDD6virtualkey64700000virtualkey647-UPW1E220MDD6) [DigiKey](http://www.digikey.com/product-detail/en/UPW1E220MDD/493-1811-ND/589552)
2|100u/10|CPOL-USE2.5-6|C5, C6|[Mouser](http://www.mouser.com/ProductDetail/Nichicon/UPW1A101MDD/?qs=sGAEpiMZZMtZ1n0r9vR22S0KxkuIgpi%2fX1J5JW69KRs%3d) [DigiKey](http://www.digikey.com/product-detail/en/UPW1A101MDD/493-1736-ND/589477)
1|100u/25|CPOL-USE2.5-6|C4|[Mouser](http://www.mouser.com/ProductDetail/Nichicon/UPW1E101MED/?qs=sGAEpiMZZMtZ1n0r9vR22RH2kZvTh%252b0acPUJvx0bRqc%3d) [DigiKey](http://www.digikey.com/product-detail/en/UPW1E101MED/493-1820-ND/589561)
1|OKI-78SR-5|OKI-78SR-05H|IC1|[Mouser](http://www.mouser.com/ProductDetail/Murata-Power-Solutions/OKI-78SR-5-15-W36H-C/?qs=sGAEpiMZZMtwaiKVUtQsNa9RSQZ1iZ%2fUZeDy49qqIt4%3d) [DigiKey](http://www.digikey.com/product-detail/en/OKI-78SR-5%2F1.5-W36H-C/811-2692-ND/3438675)
2|1N4001|DIODE-DO41-7|D1, D3|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=1N4001GP-E3%2f73virtualkey61370000virtualkey625-1N4001GP-E3%2f73) [DigiKey](http://www.digikey.com/product-detail/en/1N4001/1N4001FSCT-ND/1532742)
1|ATmega328P|AVR-MEGA8-PPTH|IC2|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=ATMEGA328P-PUvirtualkey55650000virtualkey556-ATMEGA328P-PU) [DigiKey](http://www.digikey.com/product-detail/en/ATMEGA328P-PU/ATMEGA328P-PU-ND/1914589)
1|74HC595N|74LS595N|IC3|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=SN74HC595Nvirtualkey59500000virtualkey595-SN74HC595N) [DigiKey](http://www.digikey.com/product-detail/en/SN74HC595N/296-1600-5-ND/277246)
1|16MHz|RESONATORRESONATOR-PTH|Y1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=AWCR-16.00MDvirtualkey52750000virtualkey815-AWCR-16.00MD) [DigiKey](http://www.digikey.com/product-detail/en/ZTT-16.00MX/X908-ND/170095)
1|BC337|BC337|Q2|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=BC33725BUvirtualkey51210000virtualkey512-BC33725BU) [DigiKey](http://www.digikey.com/product-detail/en/BC33725BU/BC33725BU-ND/975529)
1|FDP7030BL|MOSFET-NTO220HS|Q1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=FDP7030BLvirtualkey51210000virtualkey512-FDP7030BL) [DigiKey](http://www.digikey.com/product-detail/en/FDP7030BL/FDP7030BLFS-ND/976591)
1|LCD|PINHD-1X16|J1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=NHD-0216K1Z-NSW-FBW-Lvirtualkey66010000virtualkey763-0216K1Z-NSW-FBW) [DigiKey](http://www.digikey.com/scripts/dksearch/dksus.dll?vendor=0&keywords=NHD-0216K1Z-NSW-FBW-L)
1|TACTILE-4|TACTILE-4|S2|[Mouser](http://www.mouser.com/ProductDetail/ALPS/SKQUAAA010/?qs=oKW7zmyQiO62qWuFl5QVBw%3d%3d)
1|TACTILE-4-CAP|TACTILE-4-CAP|S2-CAP|[Mouser Rnd](http://www.mouser.com/ProductDetail/Omron/B32-1610/?qs=%2fha2pyFadugTZwGy1pbX9lynsJkYTUxoixVgJzt2NHzmD2o0%252bVfIiw%3d%3d) [Mouser Sqr](http://www.mouser.com/ProductDetail/Omron/B32-1310/?qs=%2fha2pyFadugTZwGy1pbX9hpSGIzKezvIUacN5%252bFCuhNjpogdop5w7w%3d%3d)
1|ALARM|SPEAKER/AL11P|SP1|[Mouser](http://www.mouser.com/ProductDetail/TDK/PS1240P02BT/?qs=sGAEpiMZZMuNFJjvCI6tQria9NagYYusd%2fjnLlD6%252bxU%3d) [DigiKey](http://www.digikey.com/product-detail/en/PS1240P02BT/445-2525-1-ND/935930)
3|GRN|LED3MM|LED1, LED2, LED3|(any ~3mm LED, any colors you want) [MouserR](http://www.mouser.com/ProductDetail/Kingbright/WP710A10SRD-E/?qs=sGAEpiMZZMs4quMj8r4lmsjEjMC4bfpUeUpboelRnWU%3d) [MouserY](http://www.mouser.com/ProductDetail/Kingbright/WP710A10SYD/?qs=sGAEpiMZZMs4quMj8r4lmsjEjMC4bfpUUbW71NEUWBk%3d) [MouserG](http://www.mouser.com/ProductDetail/Kingbright/WP710A10SGD/?qs=sGAEpiMZZMs4quMj8r4lmsjEjMC4bfpUWqs%252bGoI7SdI%3d)
1|POW|POWER_JACKPTH|J9|[Mouser](http://www.mouser.com/ProductDetail/Kobiconn/163-7620E-E/?qs=%2fha2pyFaduipJSLWTjADy4YYaTeQAmrHvwEfLULTtmcjsFvpXHYyeA%3d%3d) [MouserAlt](http://www.mouser.com/ProductDetail/Kobiconn/163-179PH-EX/?qs=%2fha2pyFadujsO45cTDeafnb8UTTjqBiiaL9T7NPB7rV7ulYyk%2fdYxw%3d%3d)
1|PINHD|PINHD|J1 (LCD), J2 (PROBE), J4 (BLW), J8 (FTDI)|[Mouser](http://www.mouser.com/ProductDetail/FCI/68001-236HLF/?qs=sGAEpiMZZMtsLRyDR9nM14Vjyw4ze%252bjt57BsII4P7vM%3d)
1|DIP28|DIP28|IC2-SOCK|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=1-390261-9virtualkey57100000virtualkey571-1-390261-9)

### Power, Probes and Blower
|Qty|Description|Link|
|---|-----------|----|
1 | 12VDC/1A power brick 5.5x2.1mm barrel jack | [Generic](http://www.amazon.com/gp/product/B006GEPUYA/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B006GEPUYA&linkCode=as2&tag=httpcapnbrnet-20)
1 | Blower-style fan 12VDC 5-10CFM | [DigiKey](http://search.digikey.com/us/en/products/BFB0612H/603-1117-ND/1014448)
1-4 | Maverick BBQ Thermistor Probes for ET-72/ET-73 (3ft or High Heat) | [Maverick](http://maverickhousewares.bigcartel.com/) [Amazon](http://www.amazon.com/gp/product/B004W8B3PC/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B004W8B3PC&linkCode=as2&tag=httpcapnbrnet-20)

### Probe and Blower Connectors
These are the "built in" connectors, there is space on the PCB for them. External connectors can be used by attaching to the J2 and J4 pin headers.

|Qty|Value     |Device                |Parts|Link|
|---|----------|----------------------|-----|----|
1|RCAPOWER|RCAPOWER|J5|[Mouser](http://www.mouser.com/ProductDetail/Switchcraft/PJRAN1X1U01X/?qs=%2fha2pyFaduhA2dCbClozE0M8thHp4IZMpitol3BhLqRLppD9blRIxA%3d%3d) [DigiKey](http://www.digikey.com/product-detail/en/PJRAN1X1U01X/PJRAN1X1U01X-ND/1288632) or reuse rPi composite video jack
1|Pi|PINHD-2X13|JP1|[DigiKey](http://www.digikey.com/product-detail/en/PPPC132LFBN-RC/S7116-ND/810252) (alt [DigiKey](http://www.digikey.com/product-detail/en/PPTC132LFBN-RC/S7081-ND/810219)) (alt [Mouser](http://www.mouser.com/ProductDetail/TE-Connectivity/1-215307-3/?qs=%2fha2pyFadugJp%2f0oQpeWgdlLOqmXGnSXHAkr2wdKJgMBirFMB5SQuQ%3d%3d))
1-4|Probes|AUDIO-MONO|JP3, JP4, JP5, JP6|[DigiKey](http://www.digikey.com/product-detail/en/MJ-2508N/CP-2508N-ND/281260)

### Optional Parts
|Qty|Value     |Device                |Parts|Link|Reason|
|---|----------|----------------------|-----|----|------|
1|Ambient|THERMISTOR_R-2,5|TR1|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=NTCLE203E3103FB0virtualkey59420000virtualkey594-2381-640-55103)|Only if you want an onboard 'ambient' temperature sensor 
1|RFM12B|RFM12B|U$1|[ModernDevice](http://shop.moderndevice.com/products/rfm12b-radio)|Only if building wireless probes. 915MHz only (433MHz and 868MHz supported if you compile your own firmware). Surface mount, not the kind with pins and not one on any sort of breakout board.
1|MCP1700-33|MCP1700-33|IC4|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MCP1700-3302E%2fTOvirtualkey57940000virtualkey579-MCP1700-3302E%2fTO) [DigiKey](http://www.digikey.com/product-detail/en/MCP1700-3302E%2FTO/MCP1700-3302E%2FTO-ND/652680)|Only for standalone HeaterMeter
1|ICSP|PINHD-2X3|J6|[Mouser](http://www.mouser.com/ProductDetail/3M/961206-6404-AR/?qs=A%252btsDZJT%252bi%2ft%2f4aaelvU3g%3d%3d)|Only if flashing the AVR outside of the Pi