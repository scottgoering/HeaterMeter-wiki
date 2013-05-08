### The console on my RaspberryPi hangs after booting

When plugged into an HDMI monitor, boot messages are seen on the console but then the system appears to hang, the log ending with the following lines

```
[    5.565063] usbcore: registered new interface driver rtl8192cu
[    5.613492] usbcore: registered new interface driver usbhid
[    5.615532] usbhid: USB HID core driver
[   12.367977] cfg80211_rtw_del_virtual_intf
[   12.587224] cfg80211_rtw_del_virtual_intf
[   12.734974] cfg80211_rtw_add_virtual_intf, ifname=wlan0, type=2
[   12.736843] ndev=  (null)
[   17.854496] EXT4-fs (mmcblk0p4): warning: mounting unchecked fs, running e2fsck is recommended
[   17.880577] EXT4-fs (mmcblk0p4): mounted filesystem without journal. Opts: (null)
```

Your system is not hung, that is generally the last thing that appears in the kernel log unless there's a wifi adapter connecting.  If you look several lines before that you should see a line

```
Please press Enter to activate this console
```

To activate the console, press Enter. You'll need to use a USB HID keyboard, as that is the only keyboard driver included in the installation. Many Logitech wireless keyboards are not HID compliant.

#### What about the unchecked filesystem warning?

There's no 'shutdown' button on the device, so shutting down is a matter of pulling the plug. This means the filesystems are not cleanly unmounted, which the ext4 module will complain about. The partitions are not written to in the normal course of LinkMeter operation so not properly unmounting them shouldn't cause any issues. The filesystem is written:

* On OpenWrt configuration change
* On LinkMeter database "stash"
* On bootup, during the configuration backup process