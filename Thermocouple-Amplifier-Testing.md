**NOTE** Thermocouple support is optional

After surface mount soldering the thermocouple amplifier and passive support components to the HeaterMeter PCB it is helpful to perform testing before completing the entire build.

Before applying any power, check for shorts and good connections on the amplifier IC. 1 to 1, 2s to 2s, 4s are not connected to 5, and so on. N is not connected to anything.

[![Image](https://lh4.googleusercontent.com/-Kh_LT5hR6d0/U7LKnSV0zHI/AAAAAAAAB-M/4sOadQlmvtQ/s800/tctest.png)](https://picasaweb.google.com/lh/photo/zE9keGB7s7CKZ6AQei-xmdMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

Apply any voltage source (3V-36V), such as a 9V battery, to the through-holes shown above. Connect positive to 5 and ground to 2 and measure the voltage output at 4, or the big hole connected to 4. The output voltage should be a within 0.1V of the input voltage. Note: Do not apply more than 3.3V after completing assembly of the entire HeaterMeter, only the thermocouple assembly is tolerant of this voltage range!

[![Image](https://lh5.googleusercontent.com/-tzSIMYeJ5fc/U67YFVvNZoI/AAAAAAAAB5c/b1tfShFSBd4/s640/IMG_2178.JPG)](https://picasaweb.google.com/lh/photo/5j-yXLAi8KqRpkfs5NWmJdMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

Now short the two thermocouple input pins together with a piece of wire. The output should drop to room temperature (in Celsius) * 5mV or about 0.10V-0.15V. If the AD8495 is still warm from soldering, it will affect this reading slightly. Ignore the fact that this image says "Thermopcouple", I'm not re-making it.

[![Image](https://lh3.googleusercontent.com/-0rt6xKf4kgE/U7FtumnXQvI/AAAAAAAAB90/Ow9Nng21Xak/s640/IMG_2178.JPG)](https://picasaweb.google.com/lh/photo/lzmhqbW1Ol1GYJtHS0wjINMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

If both these readings check out, your thermocouple amplifier is fully operational and you may continue [[HeaterMeter 4.2 Assembly]].

## Initial Bootup

On the first boot of your HeaterMeter when the default configuration is flashed onto the AVR, you might be expecting to see `- No Pit Probe-` on the LCD. However, you'll be greeted with a boggling `Pit: 21F [ 0%]` message. Not to worry, the default configuration is for a thermistor probe. All that needs to be done is to switch Probe 0 in the webui config from "*Internal*" type to "*Thermocouple*" and save the config.

## Thermocouple Calibration

After your HeaterMeter is assembled and fully operational, calibrating the thermocouple input may marginally improve its accuracy. Because HeaterMeter does not use a precision analog voltage reference, there's an inherent error in the measurement. Luckily this error is relatively constant for a build so it an be calibrated out. A one point calibration is all that is needed to determine an accurate reference voltage.

**Step 1** In the configuration webui, set the thermocouple mV/C to the reference 5 mv/C and 0 degree offset.

**Step 2** Allow your HeaterMeter to warm up to operating temperature in its case for 10-15 minutes. If you don't have a case, this is optional as the temperature error is only 50 parts per million (ppm) per degree Celsius of ambient temerature.

**Step 3** Insert the thermocouple into boiling water and allow it to settle at temperature.

**Step 4** Calculate your error using the [boiling point of water for your altitude](http://www.engineeringtoolbox.com/boiling-points-water-altitude-d_1344.html). 5 * (heatermeter temperature / boiling point) = mv/C

**Step 5** Enter this new value into the configuration webui and verify that the temperature reported by HeaterMeter now matches the boiling point of water.