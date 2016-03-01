## Software Installation

Download and unzip [the OpenWrt firmware image (ZIP file)](http://heatermeter.com/devel/release/bcm2708/13/) (v13)

* **Instructions for Windows**:  
 Download and unzip [Win32 Disk Imager](http://sourceforge.net/projects/win32diskimager/files/latest/download?source=files) (binary)

 Insert your SD card into your computer, launch Win32 Disk Imager, select the SD card drive, browse for the openwrt IMG file (not the ZIP!), and hit the "Write" button. Writing to the SD card should take only a few seconds. 

* **Instructions for Apple OSX**:  
 Download and install [ApplePi-Baker](http://www.tweaking4all.com/hardware/raspberry-pi/macosx-apple-pi-baker/)

 Insert your SD card into your computer, launch ApplePi-Baker, select the SD card on the left, under "Pi-Crust", on the right side, click on the empty box to the right of "IMG file" and browse for the openwrt IMG file and click on the "Restore Backup" button. Writing to the SD card should take only a few seconds. 


Insert the SD card into the Raspberry Pi and power it up using either the 12V barrel jack on the HeaterMeter board or the rPi micro USB power input. Do not hook up both at the same time! For the first boot, using the rPi USB power input is preferred to verify the operation of your assembled HeaterMeter board without the chance of subjecting the rPi to 12V which will definitely fry components on it. I know from experience.

If this is the first time you've booted the rPi using the prepared SD card, the HeaterMeter firmware will be installed automatically onto the ATmega238P.  Within 30 seconds of booting, the LCD should light up and display "-No Pit Probe-".  If you don't see anything on the LCD, but it lights up, try adjusting the contrast potentiometer with a small screwdriver.

## Configuration

Once the device boots, if it has internet access, simply use a browser to navigate to [http://heatermeter.com/devices/](http://heatermeter.com/devices/) and your HeaterMeter should be listed automatically. For more information about device registration see [[HeaterMeter Device Registration]]. If registration is not successful, continue reading.

By default the rPi's ethernet is set to both the IP address 192.168.200.1 and DHCP. If the device gets a DHCP address from your network, it will be displayed for 20 seconds on the HeaterMeter LCD. The configuration website is available at http://192.168.200.1/ (or the DHCP address) username "root" with no password. A monitor and keyboard can also be connected. If editing configuration via the console, network configuration is in /etc/config/network

## Wireless (WiFi)

The stock image includes drivers for any rtl8192cu-based or RT5370 USB wifi adapters. See [[Wireless Adapters]] for a more complete listing. The adapter should be recognized if inserted before booting and be shown in the System -> Network -> Wifi web configuration pages. Both AP and client mode are supported, and starting with LinkMeter v12 the device will be configured as an open Access Point with the name (SSID) "heatermeter", on IP address http://192.168.201.1/ or http://OpenWrt.local/ (only if connecting through the wifi!)

### Wireless Client Setup via config file step-by-step ( easiest method )

There's now an easy way to set your wifi configuration before you even boot the HeaterMeter for the first time.

**Step 1**: Insert your SD card back into your card writer / computer and edit the `config.txt` file located in the top level folder of the card. At the bottom of that file there's now a `## wifi configuration` section.
```
##
## wifi configuration
##
# SSID (network name)
#wifi_ssid=heatermeter
# Password for encryption
#wifi_password=password
# Encryption mode psk2 (WPA2-PSK default), psk, wep, none
#wifi_encryption=psk2
# Mode ap (Access Point) or sta (Client mode, default). Must be lowercase!
#wifi_mode=ap
# wifi channel, only used in AP mode
#wifi_channel=6
```

#### Regular wifi client mode with WPA2 security:
Just uncomment out (remove the # at the beginning of the line) for the `wifi_ssid` and `wifi_password` entries.
```
# SSID (network name)
wifi_ssid=MyHomeWireless
# Password for encryption
wifi_password=MyWirelessPassword
```
**Step 2**: Save the file, eject the SD card and insert it back into the Raspberry Pi

**Step 3**: Plug your USB wifi dongle into the Raspberry Pi

**Step 4**: Power up your HeaterMeter

The configuration takes place at the end of boot, after the network has already been initialized, so you'll see it pop up in the original mode first, then switch to the desired mode. This is because it needs to take place after the configuration restore has occurred (if it is going to). Once the wifi settings are loaded, it will automatically comment out all the wifi values in config.txt so it won't reset them again. 

**Note**: If your wifi SSID or password contains quotes (single ' or double ") then you're going to experience a nightmare trying to get this to work. E.g. your SSID is `"Bryan's Wifi"` = mal tiempo.

### Wireless Client Setup via Web Config step-by-step

**Step 1**: Use a web browser to go to http://ip-address-shown-on-heatermeter/ which should land you on the HeaterMeter home page. It's blue. It has flaaaaames. It's pretty American. (No photo, you'll know it when you see it)

**Step 2**: Click the configuration link on the bottom of the page then navigate to Network -> WiFi and click Scan. If there is no WiFi listed, either your WiFi adapter is not supported or you don't have a power supply capable of providing enough power to the wireless adapter.

![Image](http://capnbry.net/~bmayland/fi/bbq/hm-wifi-1.png)

**Step 3**: Find your wireless network and click Join. My name is lame. Yours I'm sure is hilarious and expresses your individuality.

![Image](http://capnbry.net/~bmayland/fi/bbq/hm-wifi-2.png)

**Step 4**: Enter your wireless password. I'm guessing it is "12345"!

![Image](http://capnbry.net/~bmayland/fi/bbq/hm-wifi-3.png)

**Step 5**: Don't touch a cotton pickin' thing on the page that comes up. You're not smarter than the defaults or else you wouldn't need this guide. Just press "Save and Apply"

![Image](http://capnbry.net/~bmayland/fi/bbq/hm-wifi-4.png)

**Step 6**: This is where you think things have gone wrong because the "Waiting for changes to be applied..." never goes away. I don't know what it is waiting for, perhaps a new pope to be elected. I've never waited that long. Just wait 15 seconds and move on.

![Image](http://capnbry.net/~bmayland/fi/bbq/hm-wifi-5.png)

**Step 7**: Navigate to Network -> Interfaces. You should see you're on your wifi network now and you can see the IP address on your home network you can use to see the LinkMeter site. *If your wifi never gets an IP address it's likely because you can't have both wired and wireless adapters on the same subnet. See [[Basic Troubleshooting]] for more.* I'm not good with numbers so I like to use a name. To use a name, click "Edit" on the wireless network

![Image](http://capnbry.net/~bmayland/fi/bbq/hm-wifi-6.png)

**Step 8**: Enter a name. I like short names "hm", "hmpi", or "bob". "Save and Apply" to commit the change. You'll get our old friend the "Waiting for changes..." pope-watcher but rest assured next time this puppy boots it will register on your home network with that name. Not all routers support named DHCP registration so if it doesn't work, use the IP address from the previous step 7.

![Image](http://capnbry.net/~bmayland/fi/bbq/hm-wifi-7.png)

**IMPORTANT** Once you configure your wifi to be a client on your network, you must reboot to switch from wired to wireless connectivity. That is, you can not boot with ethernet plugged in then configure the wifi and just unplug the ethernet cable. You must reboot after unplugging the ethernet cable for the wifi to be accessible.