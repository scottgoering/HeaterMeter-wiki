After surface mount soldering the thermocouple amplifier and passive support components to the HeaterMeter PCB it is helpful to perform testing before completing the entire build.

Apply any voltage source (3V-36V), such as a 9V battery, to the through-holes shown above and measure the voltage output. The output voltage should be a within 0.1V of the input voltage.

[![Image](https://lh5.googleusercontent.com/-tzSIMYeJ5fc/U67YFVvNZoI/AAAAAAAAB5c/b1tfShFSBd4/s640/IMG_2178.JPG)](https://picasaweb.google.com/lh/photo/5j-yXLAi8KqRpkfs5NWmJdMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

Now short the two thermocouple input pins together with a piece of wire. The output should drop to room temperature (in Celsius) * 5mV or about 0.10V-0.15V. If the AD8495 is still warm from soldering, it will affect this reading slightly.

[![Image](https://lh3.googleusercontent.com/-0rt6xKf4kgE/U7FtumnXQvI/AAAAAAAAB90/Ow9Nng21Xak/s640/IMG_2178.JPG)](https://picasaweb.google.com/lh/photo/lzmhqbW1Ol1GYJtHS0wjINMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

If both these readings check out, your thermocouple amplifier is fully operational and you may continue HeaterMeter v4.2 Assembly.