# TODO list
Items roughly in the order I may get to them

* Wiki pages
* Security
    * Still possibly getting silently logged out?
* Consider using LuCId as the HTTP server and linkmeterd
* RF probe status information
    * Added voltage to tooltip.  Need a probe status / config page still (below)
* avrupdate 
    * Better integration and update-from-web.  Part of larger automatic update process?
* linkmeterd socket to allow through read/write
* Allow archive, copy to / from archive.  Archive location defaults to SD card but can use /tmp for testing
    * GZIP it?
    * Only get CFs that are used?
    * Download / upload?
* Archive library.  Text file associated with each item
    * Date / Time, duration
    * Title 
    * Short description
    * Annotations
    * Keywords
* Adjust order of items on tooltip?
* utils.html  config.html?  
    * Split one-time settings from common changed settings
* probe config 
    * Disposition=Disabled, Internal, Wireless
    * Wireless Mapping: Node (B-Z), Pin (0-3), Dest (Probe0-Probe3)
    * ProbeName, Offset, Rknown, steinhart[3]
    * /set?pc0=8.98053228e-4,2.49263324e-4,2.04047542e-7,022000  = 57 bytes
    * Alarm High, Alarm Low, High Enabled, Low Enabled
* Alarms
    * Serial notification
    * Chrome To Phone / C2DM message
    * Temperature Cut mode.  Option to have the pit temperature drop when food reaches done point
        * Can be an alarm option.  When AlarmRinging && !AlarmSilenced -> SetPoint = AlarmHigh, AlarmSilenced = true
* Remote node
    * 2.7V 8MHz internal clock?  Can be powered from solar path light
* New enclosure?
* Inkject PCB printing
* BatchPCB linkmeter design
* ASUS RT-N12 GPIO points/design
