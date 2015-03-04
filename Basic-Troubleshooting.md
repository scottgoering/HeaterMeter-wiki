These are some basic problems. For anything not covered here, go to the HeaterMeter online community on [The Virtual Weber Bulletin Board tvwbb.com](http://tvwbb.com/forumdisplay.php?85-LinkMeter-v2-Homebrew-BBQ-Controller).

For most troubleshooting, using the rPi USB power input is preferred in order to avoid the chance of subjecting the rPi to 12V which will definitely fry components on it.

### I built the whole thing, but nothing happened when I plugged it in.
* Start by ensuring you can connect to openwrt on your Raspberry Pi [See HeaterMeter 4.x Software](HeaterMeter 4.x Software#configuration)
* If you can connect to the Raspberry Pi, look at the system log (Configuration -> Status -> System Log) to see if your heatermeter was recognized.

### openwrt says my heatermeter wasn't found
* Verify that all necessary components are on the board and in the right place.
* Ensure sure you pushed solder through on every connection so that a connection is made on both sides of the board.