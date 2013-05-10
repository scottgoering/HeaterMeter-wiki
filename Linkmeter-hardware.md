As a reminder, LinkMeter refers to a OpenWrt-compatible device which has a HeaterMeter controller board installed in it.

## Reference Hardware

* HeaterMeter v4.0 - **RaspberryPi Model A** or **Model B** with 256MB or 512MB RAM - referred to as bcm2708 target. No hardware modification is necessary but things fit together better if the composite video RCA jack is removed. It can be desoldered or just clipped off with wire cutters. As the rPi does not include a case, having one custom 3D printed is recommended. A standard RaspberryPi case will **not** fit the rPi with the HeaterMeter board mounted on it. Every dimension is different.
* HeaterMeter v3.0, v3.1, v3.2 - **Linksys WRT54GL** - referred to as bcm47xx target.  Minimal hardware modification is necessary-- most of the modification is to the plastic case to expose the probe/fan connectors, LCD, and buttons. 