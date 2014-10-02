### What is HeaterMeter Device Registration?

Simple answer: a list of all the HeaterMeters on your LAN, available at [http://heatermeter.com/devices/](http://heatermeter.com/devices/)

![HeaterMeter Device Manager](Images/hm-device-manager.png)

### Why?

To make it easy to find your new HeaterMeter!

Because of the interaction between the Raspberry Pi's ethernet jack and any wifi dongles installed, it may be difficult to determine what address to put in the browser's address bar. Using this bit of software, the device registers *all* of its network addresses and displays them on a web page, and the browser can programmatically determine which are valid from your browser. The addresses listed in the HeaterMeter online device manager are only accessible from your local area network.

### What am I looking at?

Each box represents a HeaterMeter device, labeled with the hostname as set in the webui. Each potential connection address gets its own line. The `Status` column indicates if data has ever been sent or received on the connection. `Address` is the IP address which might be accessible from your network. `Available` is the result of a query for HeaterMeter at that address. A HeaterMeter is available if it accepts the connection and responds with its version information. If the address is available, the address will become a link which can be clicked to take you to that HeaterMeter's home page.

### It says there are no HeaterMeter (sad nugget)

On a brand new fresh firmware install, it may take a few minutes before the HeaterMeter registers for the first time. If no HeaterMeter are found, the page will automatically refresh itself until a device is found. If nothing shows up after five minutes, there's almost certainly a problem with your HeaterMeter not getting on the network.

### Will the world be able to connect to my HeaterMeter?

No. The device addresses listed are the private addresses, accessible only from your local network. Some are so private they're not even accessible from your network!

There is no way for someone to query which HeaterMeter devices are on your network. The Device Manager only lists devices which match the requestor's address. This also means you won't see HeaterMeters on your LAN from your phone's browser if your phone is on cellular 3G/4G, only if it is on the same network as the HeaterMeter.

That's not to say that you can't make a hole in your firewall to access your HeaterMeter from the internet, but the HeaterMeter Device Manager will not list the publicly accessible address in the address list, even to you.

### How can I opt out?

In the webui, go to System -> Startup and in the `Local Startup` box enter the following line before the line "exit 0", Submit, and reboot. Your device will no longer register and will disappear from your site's device list in about a day.
~~~
uci set linkmeter.live.optout=1
~~~