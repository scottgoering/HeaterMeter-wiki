### Software TODO list

* Easier email / sms integration
    * User enters to address/name for email, (from address comes from msmtp), sms number, provider, then there's a bunch of checkboxes: Alarm 0 Low: AutoSilence, SMS, Email, UserScripts
    * Text boxes for SMS message to send, email text
    * Button to send test email
* Temperature ramp down mode. Select food probe as source and a percent to start at, then LERP down to it.
* Blower kickstart. When enabling the blower 0% to any%, set it to 100% for N milliseconds to allow it to spin up more reliably.
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
* Add new indicator LEDs to shift register 
    * Temperature OK (temp within x% of setpoint). Pit probe only or for any probe?
    * High load / low fuel (average fan speed > x%)
    * "Food OK". Not sure what this one was
* Touch-friendly setpoint setting using vertical ... spin ... grid
* Alarms
    * Chrome To Phone / C2DM / GCM message
    * Temperature Cut mode.  Option to have the pit temperature drop when food reaches done point
        * Can be an alarm option.  When AlarmRinging && !AlarmSilenced -> SetPoint = AlarmHigh, AlarmSilenced = true
    * Elaped time notify
* Unknown probe Steinhart calculations
    * LUA implementation of Levenberg–Marquardt algorithm for a 2-pass (rough estimate, refine) multi-iteration determination off coeffs
* Easier initial setup
    * Set initial wifi to AP mode. dnsmasq needs to run when in this configuration but not once in client mode. Can it switch automatically?
    * Captive portal if in AP mode.
    * eth0/wlan bridging. Needs 4addr support at the AP.
* Ability to set the colors of the LEDs in the web interface? Can store in uci file
* Ability to set light webpage to autorefresh. Javascript only?
* HeaterMeter configuration profiles. Defaults, A, B. Selectable from "Reset Config?" on HeaterMeter. A and B could be names?
* Remote node
* Optimize LuCI node() generation to speed page loads and reduce memory usage
    * Entire tree is generated on every page call, taking at least 300ms and peaking at 1.1MB of RAM per process

### HeaterMeter PCB

* No connectors on bottom
  * Rotate power plug to left side
  * Move Blower Out to right side
* Replace blower output RCA with 2.5mm barrel jack (used by commercial projects)
* Add servo output jack
  * Is there a way to make the blower output have a different function if set to servo mode?
* Add "AUX" port. Use the old SOFTRESET pin as an output that runs through a mosfet that can either supply 3.3V, 5V or 12V as one of the configurable LEDs
* Integrate switching power supply into PCB, the Murata is great but often out of stock
* Capacitors on analog inputs
* Drive alarm with 12V through transistor or mosfet (maybe not easily doable)
* Physical rPi switch to allow booting in multiple network configurations.
  * Maybe a button to load the default config backup?
* P-Channel MOSFET to drive blower to combine GND for servo
* AD8495 thermocouple footprint