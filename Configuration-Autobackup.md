As of LinkMeter v7, your OpenWrt configuration is automatically backed up on every successful boot. When a fresh default image is flashed to the SD card, using Win32DiskImager or dd, configuration is restored from this area to return your configuration.

### Where is it stored?
The `/etc/init.d/config_restore` script creates a new 64MB partition (partition 4) at the end of your SD card. This partition is mounted and the system is backed up to `/mnt/mmcblk0p4/backup.tar.gz`.

### How often is it stored?
The backup is created near the end of every boot. If you make any configuration changes, be sure to boot OpenWrt with these changes at least once before reimaging (i.e. don't change configuration and the image in a single boot)

### How does my configuration survive getting wiped by the disk imager?
When a default image is flashed, the partition table (the first 512 bytes of the device) is reset to the original state. However, the data is still there because the disk imaging utility only writes to the first ~40MB. On any boot where there isn't a partition 4 defined, the config_restore script will create one exactly 64MB from the end of the device and attempt to check the filesystem located there. If the check succeeds, and there's a backup.tar.gz there, then this configuration will be restored and OpenWrt will reboot. 

### What if my SD card is from the 1970s and isn't large enough to hold an additional 64MB?
The partition will only be created if there is at least 64MB of sectors on the device

### I've extended my ext4 partition to the end of the device already, will it be overwritten?
The partition creation script will only create a partition if there's not already a partition which extends to the end of the device.

### I've booted a fresh flash and it doesn't look to be doing anything
There's nothing output to the screen between the ethernet initialization and the configuration backup/restore, which is about a minute long on a first boot. If you've waited 2 minutes and nothing has happened, odds are nothing will. (shrug)

### What files are backed up?
The same files you get when you do a backup from the web interface. This includes network and mail server configuration, ssh keys, user password, and linkmeter alarm scripts.
```
etc/nixio/rsa_main.der
etc/nixio/cert_main.der
usr/share/linkmeter/alarm-all
usr/share/linkmeter/alarm-0H
usr/share/linkmeter/alarm-0L
etc/sysupgrade.conf
etc/sysctl.conf
etc/shells
etc/shadow
etc/rc.local
etc/profile
etc/passwd
etc/msmtprc
etc/inittab
etc/hosts
etc/group
etc/dropbear/dropbear_rsa_host_key
etc/dropbear/dropbear_dss_host_key
etc/config/wireless
etc/config/upnpd
etc/config/ucitrack
etc/config/system
etc/config/network
etc/config/lucid
etc/config/luci
etc/config/dropbear
```

### What about my LinkMeter database stash!
The stash data files are not included in the backup. It is safe for you to move your stashpath to the safe partition by moving your rrd files to a directory under `/mnt/mmcblk0p4/` for example `/mnt/mmcblk0p4/stash`. Then set the linkmeter stashpath to that directory.
```
uci set lucid.linkmeter.stashpath=/mnt/mmcblk0p4/stash
uci commit lucid
```