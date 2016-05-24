As a reminder, HeaterMeter refers to the ATmega (Arduino) based microcontroller board that runs the LCD, reads button and temperature probe inputs, and controls the servo and blower motor. This document describes the configurations and design of the HeaterMeter board, which may optionally be attached to a Raspberry Pi. This list is split into three sections

* Main HeaterMeter Board which contains the input power and probe connections, as well as the blower and servo output.
* LCD and Button Board which contains the drive circuitry for the 16x2 character LCD and buttons, as well as the 3 indicator LEDs. **Optional** if a local display and buttons are not desired.
* Thermocouple Addon, which are components added onto the Main Board to utilize a thermocouple control probe instead of the thermistor. The FOODx probes remain as thermistors. **Optional**

Standard HeaterMeter hardware is built on a HeaterMeter v4.3 PCB

* Surface Mount a PCB with the optional thermocouple parts already soldered and tested or the HeaterMeter kit
* Buy direct from OSH Park (minimum quantity 3), singles OSH Park or HeaterMeter
* Schematic Image
* EAGLE 5 schematic and board
* DorkBot/OSH Park cam job or cam output. Use cam output if you just want a board made with no modifications

**Quick and Easy**: Mouser parts. Does not include thermocouple or DigiKey-only parts 1xBlower 1xSocket. Alternatively, HeaterMeter kits are available from the HeaterMeter store which include all the Mouser and Digikey parts as well as a PCB.

### Main Board
|Qty|Value     |Device                |Parts|Link|
|---|----------|----------------------|-----|----|
3|  1k         | R-US_0204/7          | R1, R3, R21                       |[Mouser](https://www.mouser.com/Search/ProductDetail.aspx?R=291-1K-RCvirtualkey21980000virtualkey291-1K-RC) [DigiKey](http://www.digikey.com/product-detail/en/CF14JT1K00/CF14JT1K00CT-ND/1830350)
1|  2k2        | R-US_0204/7          | R14                               |[Mouser](https://www.mouser.com/Search/ProductDetail.aspx?R=291-2.2K-RCvirtualkey21980000virtualkey291-2.2K-RC) [DigiKey](http://www.digikey.com/product-detail/en/CF14JT2K20/CF14JT2K20CT-ND/1830358)
5|  10k 1%     | R-US_0207/7          | R5, R16, R17, R18, R20            |[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MF1%2f4DC1002Fvirtualkey66000000virtualkey660-MF1%2f4DC1002F) [DigiKey](http://www.digikey.com/product-detail/en/RNF14FTD10K0/RNF14FTD10K0CT-ND/1975090)
1|  22k        | R-US_0204/7          | R4                                |[Mouser](https://www.mouser.com/Search/ProductDetail.aspx?R=291-22K-RCvirtualkey21980000virtualkey291-22K-RC) [DigiKey](http://www.digikey.com/product-detail/en/CFM14JT22K0/S22KQCT-ND/2617712)
1|  68k        | R-US_0204/7          | R13                               |[Mouser](https://www.mouser.com/Search/ProductDetail.aspx?R=291-68K-RCvirtualkey21980000virtualkey291-68K-RC) [DigiKey](http://www.digikey.com/product-detail/en/RNMF14FTC68K0/S68KCACT-ND/2617527)
5|  100k       | R-US_0204/7          | R19, R22, R23, R28, R29           |[Mouser](https://www.mouser.com/Search/ProductDetail.aspx?R=291-100K-RCvirtualkey21980000virtualkey291-100K-RC) [DigiKey](http://www.digikey.com/product-detail/en/RNF14FTD100K/RNF14FTD100KCT-ND/1975158)
8|  0.1u       | C-US025-025X050      | C1, C2, C3, C7, C15, C16, C17, C18|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=K104K15X7RF53L2virtualkey59420000virtualkey594-K104K15X7RF53L2) [DigiKey](http://www.digikey.com/product-detail/en/K104K15X7RF5TL2/BC1084CT-ND/286706)
1|  100u/25    | CPOL-USE2.5-6        | C4                                |[Mouser](http://www.mouser.com/ProductDetail/Nichicon/UPW1E101MED/?qs=sGAEpiMZZMtZ1n0r9vR22RH2kZvTh%252b0acPUJvx0bRqc%3d) [DigiKey](http://www.digikey.com/product-detail/en/UPW1E101MED/493-1820-ND/589561)
2|  100u/10    | CPOL-USE2.5-5        | C5, C6                            |[Mouser](http://www.mouser.com/ProductDetail/Nichicon/UPW1A101MDD/?qs=sGAEpiMZZMtZ1n0r9vR22S0KxkuIgpi%2fX1J5JW69KRs%3d) [DigiKey](http://www.digikey.com/product-detail/en/UPW1A101MDD/493-1736-ND/589477)
1|  47u/25     | CPOL-USE2.5-5        | C12                               |[Mouser](http://www.mouser.com/ProductDetail/Nichicon/UPW1E470MDD/?qs=sGAEpiMZZMtZ1n0r9vR22RH2kZvTh%252b0aZAYBTdQVA9s%3d) [DigiKey](http://www.digikey.com/product-detail/en/UPW1E470MDD/493-1817-ND/589558)
1|  16MHz      | RESONATOR-PTH        | Y1                                |[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=AWCR-16.00MDvirtualkey52750000virtualkey815-AWCR-16.00MD) [DigiKey](http://www.digikey.com/product-detail/en/ZTT-16.00MX/X908-ND/170095)
2|  1N5819     | 1N5819               | D2, D3                            |[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=1N5819virtualkey51120000virtualkey511-1N5819) [Mouser Alt](http://www.mouser.com/ProductDetail/Fairchild-Semiconductor/1N5819/?qs=sGAEpiMZZMtQ8nqTKtFS%2fCJFZUIIOyzjQ1kqwoJUBVU%3d) [DigiKey](http://www.digikey.com/product-detail/en/1N5819/1N5819FSCT-ND/965482)
1|  220u       | INDUCTOR9MM          | L1                                |[Mouser](http://www.mouser.com/ProductDetail/Bourns/RLB9012-221KL/?qs=%2fha2pyFadujBRYZ98dwyHSd5PoMezoWpW69ZaH9jnX0DdcAyrTljqg%3d%3d) [MouserAlt](http://www.mouser.com/ProductDetail/ABRACON/AIUR-02H-221K/?qs=sGAEpiMZZMsg%252by3WlYCkU8J7Iu4O7azj7UsUy340R50%3d)
1|  ALARM      | SPEAKER/AL11P        | SP1                               |[Mouser](http://www.mouser.com/ProductDetail/TDK/PS1240P02BT/?qs=sGAEpiMZZMuNFJjvCI6tQria9NagYYusd%2fjnLlD6%252bxU%3d) [DigiKey](http://www.digikey.com/product-detail/en/PS1240P02BT/445-2525-1-ND/935930)
3|  BS170      | BS170                | Q1, Q2, Q5                        |[Mouser](http://www.mouser.com/ProductDetail/Fairchild-Semiconductor/BS170/?qs=sGAEpiMZZMshyDBzk1%2fWi9bHELEahoDnARtHPVtZEPQ%3d) [DigiKey](http://www.digikey.com/product-detail/en/BS170_D27Z/BS170_D27ZCT-ND/1532791)
1|  FQU11P06TU | MOSFET-P             | Q3                                |[Mouser](http://www.mouser.com/ProductDetail/Fairchild-Semiconductor/FQU11P06TU/?qs=%2fha2pyFaduiEiRTZzI6qLHjOfaLovEUv3u%2fBJwcExVo%3d) [DigiKey](http://www.digikey.com/product-search/en?x=-1022&y=-73&KeyWords=FQU11P06TU)
1|  OKI-78SR-5 | OKI-78SR-05H         | IC1                               |[Mouser](http://www.mouser.com/ProductDetail/Murata-Power-Solutions/OKI-78SR-5-15-W36H-C/?qs=sGAEpiMZZMtwaiKVUtQsNa9RSQZ1iZ%2fUZeDy49qqIt4%3d) [DigiKey](http://www.digikey.com/product-detail/en/OKI-78SR-5%2F1.5-W36H-C/811-2692-ND/3438675)
1|  ATmega328P | AVR-MEGA8-PPTH       | IC2                               |[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=ATMEGA328P-PUvirtualkey55650000virtualkey556-ATMEGA328P-PU) [DigiKey](http://www.digikey.com/product-detail/en/ATMEGA328P-PU/ATMEGA328P-PU-ND/1914589) [Mouser Non-P](http://www.mouser.com/ProductDetail/Atmel/ATMEGA328-PU/?qs=sGAEpiMZZMuHCAZ7U3Ea2vH90mYkP45F)
1|  MCP1700-33 | MCP1700-33           | IC4                               |[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=MCP1700-3302E%2fTOvirtualkey57940000virtualkey579-MCP1700-3302E%2fTO) [DigiKey](http://www.digikey.com/product-detail/en/MCP1700-3302E%2FTO/MCP1700-3302E%2FTO-ND/652680)
1|  PROBES     | AUDIO-MONO           | JP3, JP4, JP5, JP6                |[Mouser](http://www.mouser.com/ProductDetail/CUI-Inc/MJ-2508N/?qs=%2fha2pyFaduga%2fOxsLoZeddnX29ITbS93306kdE%252bHMeY%3d)[DigiKey](http://www.digikey.com/product-detail/en/MJ-2508N/CP-2508N-ND/281260)
1|  POW        | POWERJACKPTH         | J9                                |[Mouser](http://www.mouser.com/ProductDetail/Kobiconn/163-7620E-E/?qs=%2fha2pyFaduipJSLWTjADy4YYaTeQAmrHvwEfLULTtmcjsFvpXHYyeA%3d%3d) [MouserAlt](http://www.mouser.com/ProductDetail/Kobiconn/163-179PH-EX/?qs=%2fha2pyFadujsO45cTDeafnb8UTTjqBiiaL9T7NPB7rV7ulYyk%2fdYxw%3d%3d)
1|  RJ45-8     | RJ45-8               | JP2                               |[Mouser](http://www.mouser.com/ProductDetail/Amphenol-Commercial-Products/RJHSE-5080/?qs=sGAEpiMZZMvQhAhQbXdbBuidMRPVpG5q%252bZ1tFY96Whg%3d) [DigiKey](http://www.digikey.com/product-detail/en/RJHSE-5080/RJHSE-5080-ND/1242687)
1|  RPi        | PINHD-2X13           |  J1                               |[DigiKey](http://www.digikey.com/product-detail/en/PPPC132LFBN-RC/S7116-ND/810252) (alt [DigiKey](http://www.digikey.com/product-detail/en/PPTC132LFBN-RC/S7081-ND/810219)) (alt [Mouser](http://www.mouser.com/ProductDetail/TE-Connectivity/1-215307-3/?qs=%2fha2pyFadugJp%2f0oQpeWgdlLOqmXGnSXHAkr2wdKJgMBirFMB5SQuQ%3d%3d))

### LCD and Button Board
|Qty|Value     |Device                |Parts|Link|
|---|----------|----------------------|-----|----|
3|  390     |R-US_0204/7     | R10, R12, R15|[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=291-390-RCvirtualkey21980000virtualkey291-390-RC) [DigiKey](http://www.digikey.com/product-detail/en/CF14JT390R/CF14JT390RCT-ND/1830340)
1|  1k2     |R-US_0204/7     | R8           |[Mouser](http://www.mouser.com/ProductDetail/Xicon/291-12K-RC/?qs=sGAEpiMZZMu61qfTUdNhGzmcydQ1pJoa8vv7tbu1P6w%3d)
1|  1k8     |R-US_0204/7     | R11          |[Mouser](http://www.mouser.com/ProductDetail/Xicon/291-18-RC/?qs=tZuyTH1srTr%252b3mSLL5ed0A%3d%3d)
1|  3k9     |R-US_0204/7     | R2           |[Mouser](http://www.mouser.com/ProductDetail/Xicon/291-39-RC/?qs=g%252bmt%252bTSz0lYfQsKTnzZMRA%3d%3d)
1|  8k2     |R-US_0204/7     | R9           |[Mouser](http://www.mouser.com/ProductDetail/Xicon/291-82-RC/?qs=hfBUfrVtuhEpRc5G5DICCw%3d%3d)
1|  10k     |POTENTIOMETER   | R6           |[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=T73YE103KT20virtualkey61330000virtualkey72-T70YE-10K) [DigiKey](http://www.digikey.com/product-detail/en/3362P-1-103LF/3362P-103LF-ND/1088412)
1|  0.1u    |C-US025-025X050 | C10          |See above
1|  74HC595N|74LS595N        | IC3          |[Mouser](http://www.mouser.com/Search/ProductDetail.aspx?R=SN74HC595Nvirtualkey59500000virtualkey595-SN74HC595N) [DigiKey](http://www.digikey.com/product-detail/en/SN74HC595N/296-1600-5-ND/277246)
1|  BS170   |BS170           | Q4           |See above
1|  LCD     |PINHD-1X16 M    | J1, JP1M, JP8M|[Mouser](http://www.mouser.com/ProductDetail/FCI/68001-236HLF/?qs=sGAEpiMZZMtsLRyDR9nM14Vjyw4ze%252bjt57BsII4P7vM%3d)
2|  LCD1,LCD2| PINHD-1X5 F   |  JP1, JP8     |FEMALE PIN HEADER                                                                                                        
1|  BUTTONS |TACTILE-12MM    | S1, S2, S3, S4|[Mouser](http://www.mouser.com/ProductDetail/CK-Components/PTS125SM85-2-LFS/?qs=sGAEpiMZZMsgGjVA3toVBO5RbLO2OcOLbrsFSQPX4ZY%3d)                                            
1|  RED,YEL,GRN |LED3MM      | LED1, LED2, LED3 (any ~3mm LED, any colors you want)|[MouserR](http://www.mouser.com/ProductDetail/Kingbright/WP710A10SRD-E/?qs=sGAEpiMZZMs4quMj8r4lmsjEjMC4bfpUeUpboelRnWU%3d) [MouserY](http://www.mouser.com/ProductDetail/Kingbright/WP710A10SYD/?qs=sGAEpiMZZMs4quMj8r4lmsjEjMC4bfpUUbW71NEUWBk%3d) [MouserG](http://www.mouser.com/ProductDetail/Kingbright/WP710A10SGD/?qs=sGAEpiMZZMs4quMj8r4lmsjEjMC4bfpUWqs%252bGoI7SdI%3d) [MouserGAlt](http://www.mouser.com/ProductDetail/Kingbright/WP710A10GT/?qs=%2fha2pyFaduiSDnyyF%252bbBg7Q2NRL8uxAN9NekbnvC4Frh1v2fcaLdHw%3d%3d)
1|  LCD     |NEWHAVENLCD     |  LCD          |[[LCD Color Gallery]]

### Thermocouple Addon on Main PCB
Thermocouple support relies on surface mount soldering an 8 pin 3mm x 3mm chip and some 0805 passive components. Any 'ole capacitors (20%/16V) and resistors (10%/0.125W) will do fine. Mouser Project (does not include jack J4). If this is your first surface mount soldering experience, I recommend getting a couple extra of the cheap parts because they are easy to lose or destroy during soldering and you don't want to have to place another order for a 6 cent part.

|Qty|Value     |Device                |Parts|Link|
|---|----------|----------------------|-----|----|
1|  AD849X     | AD849X               | IC5                               |[Mouser](http://www.mouser.com/ProductDetail/Analog-Devices/AD8495ARMZ/?qs=sGAEpiMZZMucenltShoSnoiUfjKGVRv2eLdHM33a4xM%3d)
1|  PCC-SMP    | THERMOCOUPLE         | J4                                |[Newark](http://www.newark.com/newport-electronics/pcc-smp-k/thermocouple-connector-type-k/dp/01H0905)
1|  1k         | R-US_R0805           | R24                               |[Mouser](http://www.mouser.com/ProductDetail/Panasonic/ERJ-6GEYJ102V/?qs=%2fha2pyFaduiXHwl36i8QX1Is8RUpW4zS7XPMZn%2fLDmVYYw7P67RQlQ%3d%3d)
2|  10k        | R-US_R0805           | R25, R26                          |[Mouser](http://www.mouser.com/ProductDetail/Panasonic/ERJ-6GEYJ103V/?qs=sGAEpiMZZMu61qfTUdNhGzRxdwze5h8ZVHioc%2fD1YKQ%3d)
1|  10n (0.01 uF)|C-USC0805           | C9                                |[Mouser](http://www.mouser.com/ProductDetail/Vishay/VJ0805Y103JXJCW1BC/?qs=%2fha2pyFaduhF2nQ94KIYvTUaKx1TOqbuizaeJMhCalFkD8vCJYNgKQ%3d%3d)
2|  1n (1000 pF)|C-USC0805            | C8, C11                           |[Mouser](http://www.mouser.com/ProductDetail/Vishay/VJ0805Y102JXJCW1BC/?qs=%2fha2pyFaduhF2nQ94KIYvU%252bJKqcfKPRKfarNiDzeOaeA3G6BawyHMQ%3d%3d)
1|  0.1u       |  C-USC0805           | C13                               |[Mouser](http://www.mouser.com/ProductDetail/Vishay/VJ0805Y104MXXAC/?qs=%2fha2pyFaduhF2nQ94KIYvbBprhnZE5TJ67qQr3Q1WgZh0yiFLH%2fGlA%3d%3d)

### Power, Probes and Blower
|Qty|Description|Link|
|---|-----------|----|
1 | 12VDC/1A power brick 5.5x2.1mm barrel jack | [Generic](http://www.amazon.com/gp/product/B006GEPUYA/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B006GEPUYA&linkCode=as2&tag=httpcapnbrnet-20)
1 | Blower-style fan 12VDC 5-10CFM | [DigiKey60mm](http://search.digikey.com/us/en/products/BFB0612H/603-1117-ND/1014448) [DigiKey50mm](http://www.digikey.com/product-search/en?x=0&y=0&lang=en&site=us&KeyWords=603-1370-ND) [DifferentBlower](http://www.mouser.com/ProductDetail/ADDA/AB06012MB-250300-LF/?qs=UW%252b%252bp%2fVkpn%2fEQGl6BnSAug%3d%3d)
1-4 | Thermistor Probes -- ThermoWorks Pro-Series (Std or Needle) / Maverick ET-72/ET-73 (3ft or High Heat)| [Amazon-T-Std](http://www.amazon.com/dp/B00EZB8W0K/ref=as_li_ss_til?tag=httpcapnbrnet-20&camp=0&creative=0&linkCode=as4&creativeASIN=B00EZB8W0K&adid=03P1SGNDWFZ85JC5W569) [Amazon-T-Needle](https://www.amazon.com/dp/B00EZBB8AQ/ref=as_li_ss_til?tag=httpcapnbrnet-20&camp=0&creative=0&linkCode=as4&creativeASIN=B00EZBB8AQ&adid=0J280WDZFM7N5XZM4XF3&) [Amazon-M-3ft](http://www.amazon.com/gp/product/B004W8B3PC/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B004W8B3PC&linkCode=as2&tag=httpcapnbrnet-20) [Amazon-M-High](https://www.amazon.com/dp/B008OWZMMW?tag=httpcapnbrnet-20&camp=0&creative=0&linkCode=as4&creativeASIN=B008OWZMMW&adid=02TKF6EJVRJFR2HC0FXT&)
