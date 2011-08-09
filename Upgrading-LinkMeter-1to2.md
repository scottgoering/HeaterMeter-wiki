# Upgrading LinkMeter v1 to v2
This document covers important changes to the LinkMeter package from v1 to v2.

## New architecture
To conserve resources, LinkMeter no longer runs in its own separate process (formerly linkmeterd).  LinkMeter now lives inside the LuCId process.  This removes the requirement of having uhttpd installed and running.  

### No init.d script
There's no longer /etc/init.d/linkmeterd to start and stop.  LinkMeter can be started and stopped via /etc/init.d/lucid start | stop.  This has the side effect of starting and stopping the web server as well.  If this is not desirable, you can start and stop the serial daemon using the LinkMeter Client

    # Stop the LinkMeter serial daemon
    lua /usr/lib/lua/lmclient.lua LMD0
    # Start the LinkMeter serial daemon 
    lua /usr/lib/lua/lmclient.lua LMD1

The daemon is will not start multiple instances if you call LMD1 multiple times.  See also [[LMClient Commands]]

### New config file
LinkMeter configuration is now stored in **/etc/config/lucid**. Your configuration will not be migrated. The option names have not changed. 

    config 'linkmeterd' 'linkmeter'
            option 'serial_device' '/dev/ttyS1'
            option 'rrd_file' '/tmp/hm.rrd'
            option 'serial_baud' '115200'
            option 'stashpath' '/root'

After upgrading, you may want to delete /etc/config/linkmeter as it is no longer used and may get confusing later.

### New socket path
The LinkMeter server communication socket is now /var/run/linkmeter.sock

### No PID file
The LinkMeter daemon no longer drops a pid file in /var/run/linkmeter/pid

#### For self-builders
If you build your own LinkMeter packages or image, note that there are new patches under openwrt/patches. The 3 200-level patches need to be copied into your wrt tree under feeds/luci/luci/patches. There is no directory there currently, you will need to create it. These address a critical memory leak in the LuCId server and a large performance increase to luci-lib-web on the whole. These patches will be removed as I work to get them accepted into the LuCI project, so if there aren't files matching 2??-luci-*.patch in the HeaterMeter git tree when you pull, they're already in LuCI.