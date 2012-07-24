# TODO list
Items roughly in the order I may get to them

* Option to LuCId to reject X-Purpose|Purpose: preload to prevent Chrome from raping the server
* RF probe status information
    * Added voltage to tooltip.  Need a probe status / config page still (below)
* Optimize LuCI node() generation to speed page loads and reduce memory usage
    * Entire tree is generated on every page call, taking at least 300ms and peaking at 1.1MB of RAM per process
* Should modify to use old cookie after privilege escalation.
* avrupdate 
    * Better integration and update-from-web.  Part of larger automatic update process?
* Better interactivity with linkmeterd socket, ability to do actual query/response to HeaterMeter
* Allow archive, copy to / from archive.  Archive location defaults to SD card but can use /tmp for testing
    * GZIP it?
    * Only get CFs that are used?
    * Download / upload?
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
* Add new indicator LEDs to shift register 
    * Fan is on (fan percent > 0)
    * Temperature OK (temp within x% of setpoint) / Pit temperature reached
    * Lid is open
    * High load / low fuel (average fan speed > x%)
    * Alarm. One for Pit one for Food? Assignable?
    * "Food OK". Is that an Anti alarm? 
* Touch-friendly setpoint setting using vertical ... spin ... grid
* Alarms
    * Chrome To Phone / C2DM message
    * Temperature Cut mode.  Option to have the pit temperature drop when food reaches done point
        * Can be an alarm option.  When AlarmRinging && !AlarmSilenced -> SetPoint = AlarmHigh, AlarmSilenced = true
    * Elaped time notify
* Unknown probe Steinhart calculations
    * Set slave probes to mode "resist" where they just output their resistance. Add "raw" for raw ADC value, and "metric" for celcius output. Expand datatype / rename?
    * LUA implementation of Levenberg–Marquardt algorithm for a 2-pass (rough estimate, refine) multi-iteration determination off coeffs
* Remote node
    * 2.7V 8MHz internal clock?  Can be powered from solar path light
* New enclosure?
* RaspberryPi-based board
    * Must include 12V->5V regulator (buck)
    * SPI flashing procedure (no Optiboot)
    * Need usable WiFi device