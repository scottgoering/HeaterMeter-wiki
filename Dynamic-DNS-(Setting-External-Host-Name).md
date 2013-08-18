## Overview
Dynamic DNS is a service that will associate your public ip address with a domain name.  Additional information on DDNS can be found [here](http://en.wikipedia.org/wiki/Dynamic_DNS).  The steps outlined below will get your HeaterMeter up and running with a configurable DDNS client that will keep your registered domain name updated with its current public ip address. All testing was performed using a Dyn DNS pro account, but there are free alternatives.

## Prerequisites
* In order for this to work you must have a domain name service that allows for dynamic updating.  There are pre-configured services in the software package we'll be adding that are supported out of the box. All testing was performed with [DynDNS](http://dyn.com/dns/). An outdated list of providers can be found [here](http://dnslookup.me/dynamic-dns/).
* A working HeaterMeter 4 with Raspberry Pi running most recent OpenWRT Packages.
* Network port forwarding configured as outlined [here](https://github.com/CapnBry/HeaterMeter/wiki/Network-ports).

## Installation
Within the HeaterMeter web interface click the configuration link and login.  On the system tab go to the software sub-tab.  On the software sub-tab click the button to update list.  Once updated type luci-app-ddns in the filter field and press the find package button. Click the available packages tab below that and then click the install link next to luci-app-ddns. The new software with all necessary prerequisites will be downloaded and installed.

## Configuration
Once installed the new Dynamic DNS configuration page can be found on the Services tab.  Check the box to enable DDNS.  Select the correct network interface to monitor; in most cases this will be wwan for wireless connections or lan if connected via ethernet cable.  Select the appropriate dynamic dns service provider from the pull-down list.  Enter hostname, username, and password in the appropriate fields.  Select URL from the source of ip address field and enter http://checkip.dyndns.com/ in the URL field.  The remaining fields can be left with their default values.  Press the save and apply button and wait for confirmation the changes were saved.  Reboot your HeaterMeter.  Once the monitored interface comes up your Dynamic DNS service provider will be contacted and update with your current ip address.  Verify through your providers management interfaces that the assigned ip address matches the ip address listed when going to the above [url](http://checkip.dyndns.com/) from a device on the same network as your HeaterMeter.
 