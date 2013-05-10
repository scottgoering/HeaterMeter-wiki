# OpenWrt Packages

## Essential Standard Packages
* **luci-lib-lucid-http** This pulls the necessary dependencies

## Custom Packages
Prebuilt custom packages from the development branch can be downloaded from  

* Linksys WRT54GL - http://capnbry.net/linkmeter/snapshots/trunk/packages/
* RasberryPi - http://capnbry.net/linkmeter/snapshots/brcm2708/packages/

These are not necessary if installing the pre-built OpenWrt image as it already contains these packages.

* **rrdtool-1.4.5-LM*** and **librrd-1.4.5-LM*** Supplies the rrd lua bindings.  Note this package has had the graph components removed.
* **linkmeter-*** The LinkMeter daemon, web ui files, and hmdude AVR flash utility.
