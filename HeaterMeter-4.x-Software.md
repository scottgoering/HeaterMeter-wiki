## Software Installation

Download and unzip [Win32 Disk Imager](http://sourceforge.net/projects/win32diskimager/files/latest/download?source=files) (binary)

Download and unzip [the OpenWrt firmware image](http://capnbry.net/linkmeter/release/bcm2708/12/) (v12)

Insert your SD card into your computer, launch Win32 Disk Imager, select the SD card drive, browse for the openwrt IMG file (not the ZIP!), and hit the "Write" button. Writing to the SD card should take only a few seconds. 

Insert the SD card into the Raspberry Pi and power it up using either the 12V barrel jack on the HeaterMeter board or the rPi micro USB power input. Do not hook up both at the same time! For the first boot, using the rPi USB power input is preferred to verify the operation of your assembled HeaterMeter board without the chance of subjecting the rPi to 12V which will definitely fry components on it. I know from experience.

If this is the first time you've booted the rPi using the prepared SD card, the HeaterMeter firmware will be installed automatically onto the ATmega238P.  Within 30 seconds of booting, the LCD should light up and display "-No Pit Probe-".  If you don't see anything on the LCD, but it lights up, try adjusting the contrast potentiometer with a small screwdriver.

## Configuration

Once the device boots, if it has internet access, simply use a browser to navigate to [http://heatermeter.com/devices/](http://heatermeter.com/devices/) and your HeaterMeter should be listed automatically. For more information about device registration see [[HeaterMeter Device Registration]]. If registration is not successful, continue reading.

By default the rPi's ethernet is set to both the IP address 192.168.200.1 and DHCP. If the device gets a DHCP address from your network, it will be displayed for 20 seconds on the HeaterMeter LCD. The configuration website is available at http://192.168.200.1/ (or the DHCP address) username "root" with no password. A monitor and keyboard can also be connected. If editing configuration via the console, network configuration is in /etc/config/network

## Wireless (WiFi)

The stock image includes drivers for any rtl8192cu-based or RT5370 USB wifi adapters. See [[Wireless Adapters]] for a more complete listing. The adapter should be recognized if inserted before booting and be shown in the System -> Network -> Wifi web configuration pages. Both AP and client mode are supported, and starting with LinkMeter v12 the device will be configured as an open Access Point with the name (SSID) "heatermeter", on IP address http://192.168.201.1/ or http://OpenWrt.local/ (only if connecting through the wifi!)

### Wireless Client Setup step-by-step

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

**Step 7**: Navigate to Network -> Interfaces. You should see you're on your wifi network now and you can see the IP address on your home network you can use to see the LinkMeter site. I'm not good with numbers so I like to use a name. To use a name, click "Edit" on the wireless network

![Image](http://capnbry.net/~bmayland/fi/bbq/hm-wifi-6.png)

**Step 8**: Enter a name. I like short names "hm", "hmpi", or "bob". "Save and Apply" to commit the change. You'll get our old friend the "Waiting for changes..." pope-watcher but rest assured next time this puppy boots it will register on your home network with that name. Not all routers support named DHCP registration so if it doesn't work, use the IP address from the previous step 7.

![Image](http://capnbry.net/~bmayland/fi/bbq/hm-wifi-7.png)

**IMPORTANT** Once you configure your wifi to be a client on your network, you must reboot to switch from wired to wireless connectivity. That is, you can not boot with ethernet plugged in then configure the wifi and just unplug the ethernet cable. You must reboot after unplugging the ethernet cable for the wifi to be accessible.