As a reminder, LinkMeter refers to a OpenWrt-compatible device which has a HeaterMeter controller board installed in it.

## Reference Hardware

* HeaterMeter v4.0, v4.1, v4.2 - **RaspberryPi Model A, A+, B, B+, Zero** - referred to as bcm2708 target. The composite video RCA jack should be removed. It can be desoldered or just clipped off with wire cutters. As the rPi does not include a case, having one custom 3D printed is recommended. A standard RaspberryPi case will **not** fit the rPi with the HeaterMeter board mounted on it. Every dimension is different. The **Model B+, Pi 2, and Pi 3 are also not supported**, the physical footprint of these devices prevents the direct mating of the HeaterMeter board to the Pi.
* HeaterMeter v3.0, v3.1, v3.2 - **Linksys WRT54GL** - referred to as bcm47xx target.  Minimal hardware modification is necessary-- most of the modification is to the plastic case to expose the probe/fan connectors, LCD, and buttons. 