HeaterMeter v4.2 mates with a Raspberry Pi Model A+, but the extended 40 pin Pi connection tries to occupy the same space as the HeaterMeter alarm circuit. However there is plenty of room for it if mounted differently.

 * R3 1k resistor soldered to top instead of bottom of board
 * Q2 MOSFET soldered to top instead of bottom of board. Notice that it needs to be mirrored (flipped 180 degrees) to still have the correct polarity. It should be soldered with enough "leg" that it can be bent over face down after soldering.
 * Install piezo alarm at an angle so it doesn't interfere with the A+'s 40 pin connector.
 * Make sure the LCD pins don't contact the USB shield.
 * Be careful when installing the HeaterMeter to the Pi. There are only 26 pins on the Heatermeter connection and they should connect with the 26 pins furthest from the Pi's USB connector (Pins 1-26 not Pins 15-40).

## Top View

[![APlus Top](https://lh6.googleusercontent.com/-rFriHyTT6NE/VHVG8bOnFuI/AAAAAAAACwI/AktfbDFLDmA/s640/IMG_0361.JPG)](https://picasaweb.google.com/lh/photo/Hph_2QFAuKbnnqF58krK09MTjNZETYmyPJy0liipFm0?feat=embedwebsite)

## Bottom View

[![APlus Bottom](https://lh5.googleusercontent.com/-T5F0octCMcg/VHVG7Oabi9I/AAAAAAAACwE/x8Wu-tnOf0M/s640/IMG_0367.JPG)](https://picasaweb.google.com/lh/photo/leIbGrbHqWQbtfUCAzAbPNMTjNZETYmyPJy0liipFm0?feat=embedwebsite)

## A+ Mounted

[![APlus Mounted](https://lh4.googleusercontent.com/-1k43RuDA9wM/VHVG6TJNWII/AAAAAAAACv8/CYN1Ccck8Tg/s640/IMG_0365.JPG)](https://picasaweb.google.com/lh/photo/vSQygIx_2goQ659BBrA9LNMTjNZETYmyPJy0liipFm0?feat=embedwebsite)