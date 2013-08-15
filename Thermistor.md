### My ambient temperature sensor is reading 270F!

Quick Answer: Set the 'coefficients' on the settings screen to the 'Vishay 10k' preset.

Long Version: After a new installation, it is normal for the Ambient sensor to read an incredibly wrong value. This is because HeaterMeter defaults all probes to be of the Maverick ET-72/73 type. To get a more accurate value, the probe type must be changed to match the thermistor type.

After changing the type, if you insert a probe into the jack the Ambient sensor is on, you'll get an incorrect reading from that probe now. This is because you need to change the probe type to be appropriate for the type you've just inserted. There's no way for HeaterMeter to detect the type of probe-- they must be changed manually.

### Ambient temperature reads high

The ambient sensor isn't all that great. If the sensor is mounted inside the HeaterMeter case it will always read hot because of the heat generated by the LCD, RasbperryPi, power MOSFETs, etc. Even if extended outside of the case, the thermistor is subject to some amount of self-heating and convection from the heat inside the case.

### I installed the thermistor without the probe jack and it doesn't work at all

The probe jack is required to complete the circuit that integrates the thermistor. If you do not install the probe jack you'll need to install it between the leftmost and rightmost pins on the jack footprint (not the pin that is on the side).