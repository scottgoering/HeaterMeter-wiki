# Building OpenWrt
If you don't want to use a the pre-built LinkMeter OpenWrt image, you can build it yourself from source.  LinkMeter is targeting the Attitude Adjustment release of OpenWrt, which is currently on trunk.  In these examples, it is assumed your heatermeter git repository lives at ~/heatermeter and you'll be building OpenWrt at ~/openwrt

    cd ~
    svn co svn://svn.openwrt.org/openwrt/trunk openwrt
    cd ~/heatermeter/openwrt
    ./install.sh ~/openwrt
    cd ~/openwrt
    make menuconfig (exit and save)
    make

The firmware image will be built to ~/openwrt/bin/brcm47xx/

## Building just the LinkMeter package
You'll still need the full OpenWrt build environment created from the above steps, but recompiling just the LinkMeter package can be done (from ~/openwrt)

    make package/linkmeter/compile

The package will be built to ~/openwrt/bin/brcm47xx/package/linkmeter_*_brcm47xx.ipk
    