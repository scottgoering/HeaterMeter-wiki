# TODO list
Items roughly in the order I may get to them

* Hardware Parts List to wiki
* Fix out-of-order firmware install messing up /etc/config/lucid
* Security
    * Still possibly getting silently logged out? Could be double-cookie. Should modify to use old cookie after privilege escalation.
* BUG: If the JSON update occurs while you have an in-place edit control open, you'll lose the ability to edit that item.
* Add current HM firmware version number available via /ver or something.
* Option to LuCId to reject X-Purpose|Purpose: preload to prevent Chrome from raping the server
* RF probe status information
    * Added voltage to tooltip.  Need a probe status / config page still (below)
* Optimize LuCI node() generation to speed page loads and reduce memory usage
    * Entire tree is generated on every page call, taking at least 300ms and peaking at 1.1MB of RAM per process
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
* Adjust order of items on tooltip?
* utils.html  config.html?  
    * Split one-time settings from common changed settings
* probe config 
    * Disposition=Disabled, Internal, Wireless
    * Wireless Mapping: Node (B-Z), Pin (0-5), Dest (Probe0-Probe3)
    * ProbeName, Offset, Rknown, steinhart[3]
    * /set?pc0=8.98053228e-4,2.49263324e-4,2.04047542e-7,022000,B6  = 60 bytes
    * Alarm High, Alarm Low, High Enabled, Low Enabled
* Touch-friendly setpoint setting using vertical ... spin ... grid
* Alarms
    * Serial notification
    * Chrome To Phone / C2DM message
    * Temperature Cut mode.  Option to have the pit temperature drop when food reaches done point
        * Can be an alarm option.  When AlarmRinging && !AlarmSilenced -> SetPoint = AlarmHigh, AlarmSilenced = true
* Use server-sent events for status updates instead of polling on supported browsers
* Unknown probe Steinhart calculations
    * Set slave probes to mode "resist" where they just output their resistance. Add "raw" for raw ADC value, and "metric" for celcius output. Expand datatype / rename?
    * LUA implementation of Levenberg–Marquardt algorithm for a 2-pass (rough estimate, refine) multi-iteration determination off coeffs
* Remote node
    * 2.7V 8MHz internal clock?  Can be powered from solar path light
* New enclosure?
* Inkject PCB printing
* BatchPCB / DorkbotPDX linkmeter design
* ASUS RT-N12 GPIO points/design
