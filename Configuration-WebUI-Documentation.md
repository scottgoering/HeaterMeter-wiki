## PID Output Parameters

### PID Constant Settings
See the [[PID Controller Theory]] wiki page for definitions of the PID constants

### Blower Output Settings

* **Output Mode** Pulse / Voltage (v11 and above) - Pulse mode uses a continuous series of low speed (490Hz) 12V power pulses to regulate the blower speed. Voltage mode is available on HeaterMeter v4.2 hardware and enables step-down circuitry to produce a constant voltage on the output pin between 5V and 12.1V. Voltage mode is more precise with a linear output curve, and runs the blower more quietly than pulse mode. 

[![Image](https://lh6.googleusercontent.com/-SdXwvfwSjnY/U3d1ZIaiYnI/AAAAAAAABz0/8ZQ0GGs3368/s640/pulsevoltage.png)](https://picasaweb.google.com/lh/photo/SVenkUh3tFC6MGBx4Ll6Y9MTjNZETYmyPJy0liipFm0?feat=embedwebsite)

Attempting to use voltage mode on hardware without support for it will result in the blower turning on and off randomly! Also beware of using voltage mode in combination with a min blower speed which is below the operating voltage of your blower.

* **min** - Minimum blower speed. If the desired speed is below this, the output will be pulsed between OFF and MIN proportional to the desired speed over a 10 second period.
* **max** - Maximum blower speed. The PID output is scaled between 0 and MAX. For example, if the PID output is 100% and the MAX is set to 50, the blower output is 50%. The scaling is computed before comparing with MIN. That is, 10% MIN is always 10% blower speed and not affected by changing MAX.
* **Invert output** - Set the blower to be 100% output at 0% PID output and vice-versa. Use if using the HeaterMeter in a cooling mode rather than a heating mode.
* **On at max only** - Only use the blower when PID output is 100% (at which point the blower output will be set to MAX).

### Servo Output Settings
* **Pulse Duration** - Two values to represent the microseconds for the duration of the servo output pulse. The servo output is scaled linearly between these values based on the PID output percentage. Reducing or increasing the number will adjust how much the servo rotates in that direction before it stops. If a value is entered that is beyond the range of the servo movement, the servo may be damaged especially if left continuously running in this condition. See also [[Servo Mode]]
* **Invert output** - Swap the left and right endstops so the servo operates in the opposite direction.
* **Full open/close only** - Only operate the servo in two positions, fully closed (at 0% PID output) and fully open (at any PID output >0%)