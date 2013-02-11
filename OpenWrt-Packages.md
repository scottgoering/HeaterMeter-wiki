# OpenWrt Packages

## Essential Standard Packages
* **luci-lib-lucid-http** This pulls the necessary dependencies

## Custom Packages
Prebuilt custom packages from the development branch can be downloaded from  
<http://capnbry.net/linkmeter/snapshots/trunk/packages/>  
These are not necessary if installing the pre-built OpenWrt image as it already contains these packages.

* **rrdtool-1.4.5-LM*** and **librrd-1.4.5-LM*** Supplies the rrd lua bindings.  Note this package has had the graph components removed.
* **linkmeter-*** The LinkMeter daemon, web ui files, and hmdude AVR flash utility.
* 

## Included in Pre-built LinkMeter Image
* avrdude - 5.8-LM1
* base-files - 73-r27251
* blkid - 1.41.12-1
* block-mount - 0.2.0-6
* busybox - 1.18.4-1
* crda - 1.1.1-1
* dnsmasq - 2.57-2
* dropbear - 0.53.1-3
* hostapd-mini - 20110527-1
* hotplug2 - 1.0-beta-4
* iw - 0.9.22-2
* kernel - 2.6.37.6-1
* kmod-b43 - 2.6.37.6+2011-05-27-2
* kmod-broadcom-sdhc26 - 2.6.37.6-1
* kmod-cfg80211 - 2.6.37.6+2011-05-27-2
* kmod-crc-itu-t - 2.6.37.6-1
* kmod-crc16 - 2.6.37.6-1
* kmod-crc7 - 2.6.37.6-1
* kmod-crypto-aes - 2.6.37.6-1
* kmod-crypto-arc4 - 2.6.37.6-1
* kmod-crypto-core - 2.6.37.6-1
* kmod-diag - 2.6.37.6-10
* kmod-fs-ext4 - 2.6.37.6-1
* kmod-fs-mbcache - 2.6.37.6-1
* kmod-mac80211 - 2.6.37.6+2011-05-27-2
* kmod-switch - 2.6.37.6-4
* libblkid - 1.41.12-1
* libc - 0.9.32-73
* libgcc - linaro-73
* libiwinfo - 15
* liblua - 5.1.4-8
* libnl-tiny - 0.1-2
* librrd - 1.4.5-LM1
* libuci - 2011-03-27.2-1
* libuci-lua - 2011-03-27.2-1
* libusb - 0.1.12-2
* libuuid - 1.41.12-1
* linkmeter - 1
* lua - 5.1.4-8
* luci-i18n-english - 0.10+svn7193-1
* luci-lib-core - 0.10+svn7193-1
* luci-lib-ipkg - 0.10+svn7193-1
* luci-lib-lmo - 0.10+svn7193-1
* luci-lib-nixio - 0.10+svn7193-1
* luci-lib-sys - 0.10+svn7193-1
* luci-lib-web - 0.10+svn7193-1
* luci-mod-admin-core - 0.10+svn7193-1
* luci-mod-admin-full - 0.10+svn7193-1
* luci-sgi-cgi - 0.10+svn7193-1
* luci-theme-base - 0.10+svn7193-1
* luci-theme-openwrt - 0.10+svn7193-1
* mtd - 15
* nvram - 9
* opkg - 618-1
* rrdtool - 1.4.5-LM1
* swap-utils - 2.13.0.1-4
* uci - 2011-03-27.2-1
* uhttpd - 22
* wireless-tools - 29-4
* wpa-supplicant - 20110527-1
