### Software TODO list

* Light web page setpoint setting going to login page again
* Ability to set the colors of the LEDs in the web interface? Can store in uci file
* Alarm webui per-alarm silence setting: Keep Ringing, Silence Once, Disable
* Temperature ramp down mode. Select food probe as source and a percent to start at, then LERP down to it.
* Adaptive setpoint mode, set a target time and have the setpoint vary to meet that time?
* avrupdate 
    * Better integration and update-from-web.  Part of larger automatic update process?
* Better interactivity with linkmeterd socket, ability to do actual query/response to HeaterMeter
* Allow archive, copy to / from archive.  Archive location defaults to SD card but can use /tmp for testing
    * GZIP it?
    * Only get CFs that are used?
    * Download / upload?
* Support more precise SRTP ("Long PID") where the output controller operates independently of the the measuring loop. Make the fan run at "MIN SPEED" for percent * 100 ms * MINSPEED/100
    * Support on-the-fly PID period
* Archive library.  Text file associated with each item
    * Save probe names!
    * Date / Time, duration
    * Title 
    * Short description
    * Annotations
    * Keywords
    * Upload a photo associated with it?
* Archived view
    * Start and End time
    * Add date to tooltip?
    * Add legend
    * Ability to trim out data before start / after end
    * Put the graph data as static in the page?
* Graph
    * Ability to toggle between absolute time and relative time from start
    * Ability to save PNG from home screen
      * Auto upload png to imgur / facebook / twitter / Google+
    * Add annotations
* Indicator LEDs triggers
    * Temperature OK (temp within x% of setpoint). Pit probe only or for any probe?
    * High load / low fuel (average fan speed > x%)
    * "Food OK". Not sure what this one was
* Touch-friendly setpoint setting using vertical ... spin ... grid
* Alarms
    * Chrome To Phone / C2DM / GCM message
    * Elaped time notify
* Unknown probe Steinhart webui
* Easier initial setup
    * Set initial wifi to AP mode. dnsmasq needs to run when in this configuration but not once in client mode. Can it switch automatically?
    * Captive portal if in AP mode.
    * eth0/wlan bridging. Needs 4addr support at the AP.
* HeaterMeter configuration profiles. Defaults, A, B. Selectable from "Reset Config?" on HeaterMeter. A and B could be names?
* Remote node
* Optimize LuCI node() generation to speed page loads and reduce memory usage
    * Entire tree is generated on every page call, taking at least 300ms and peaking at 1.1MB of RAM per process

### HeaterMeter PCB

* Add "AUX" port. An output that runs through a mosfet that can either supply 3.3V, 5V or 12V as one of the configurable LEDs
* Integrate switching power supply into PCB?
* Physical rPi switch to allow booting in multiple network configurations.
  * Maybe a button to load the default config backup?
* AD8495 thermocouple integration