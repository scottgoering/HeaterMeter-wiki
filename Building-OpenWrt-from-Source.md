# Building OpenWrt (for RaspberryPi)
If you don't want to use the pre-built LinkMeter OpenWrt image, you can build it yourself from source. LinkMeter is built on the Attitude Adjustment release of OpenWrt. In these examples, it is assumed your heatermeter git repository lives at ~/heatermeter and you'll be building OpenWrt at ~/openwrt

These packages are required to install on 64bit Ubuntu 14.04 (trusty)
```
sudo apt-get update
sudo apt-get -y install git-core build-essential libssl-dev libncurses5-dev unzip lua5.1 libxml-parser-perl subversion mercurial
```
This will compile everything

```
cd ~
git clone git://github.com/CapnBry/HeaterMeter.git heatermeter
svn co svn://svn.openwrt.org/openwrt/tags/attitude_adjustment_12.09 -r36422 openwrt
cd ~/heatermeter/openwrt
./install.sh BCM2708 ~/openwrt
cd ~/openwrt
make oldconfig
make V=s ; make package/mac80211/compile V=s ; make V=s
# The first make will error out on building incompat-wireless
# mac80211 has to be compiled on its own, then everything else
# will compile cleanly
```
    
The firmware image will be built to `~/openwrt/bin/brcm2708/openwrt-brcm2708-sdcard-vfat-ext4.img`

## Building just the LinkMeter package
You'll still need the full OpenWrt build environment created from the above steps, but recompiling just the LinkMeter package can be done (from ~/openwrt)

`make package/linkmeter/compile`

The package will be built to `~/openwrt/bin/brcm2708/package/linkmeter_*_brcm2708.ipk`

# Building OpenWrt (for WRT54GL)
The Linksys WRT54GL target had to be frozen during the OpenWrt development cycle. The release version of Attitude Adjustment requires too much memory to run in the 16MB available on the device. You can however build  it using the same method, however the platform and SVN source URL are different
```
cd ~
svn co svn://svn.openwrt.org/openwrt/trunk@29665 openwrt
cd ~/heatermeter/openwrt
./install.sh BCM47XX ~/openwrt
cd ~/openwrt
make oldconfig
make
```
The firmware image will be built to `~/openwrt/bin/brcm47xx/`.
