### What is HeaterMeter Device Registration?

Simple answer: a list of all the HeaterMeters on your LAN, available at [http://heatermeter.com/devices/](http://heatermeter.com/devices/)

### Why?

Because of the interaction between the Raspberry Pi's ethernet jack and any wifi dongles installed, it may be difficult to determine what address to put in the browser's address bar. Using this bit of software, the device registers *all* of its network addresses and displays them on a web page, and the browser can programmatically determine which are valid from your browser. The addresses listed in the HeaterMeter online device manager are only accessible from your local area network.

### 

### How can I opt out?

In the webui, go to System -> Startup and in the `Local Startup` box enter the following line before the line "exit 0", Submit, and reboot. Your device will no longer register and will disappear from your site's device list in about a day.
~~~
uci set linkmeter.live.optout=1
~~~