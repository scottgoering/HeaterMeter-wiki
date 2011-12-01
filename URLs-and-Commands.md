Both HeaterMeter and LinkMeter accept commands via URL-type form. 

### HeaterMeter URLs

* Received via serial
* No authentication
* Begin with a forward slash (/)
* End with CR or CR/LF
* Maximum length: 64 characters
* **Do not** URL encode parameters

### LinkMeter URLs

* Received via HTTP
* Authentication possible
* Begin with ``/luci/``
* URL encoded parameters OK

<table>
<tr><th>URL</th><th>Description</th><th>LM</th><th>HM</th></tr>
<tr><td><code>/lm/</code></td>
  <td>Main index or LinkMeter "home" page. Displays current temperature and fan status with graph.
<ul>
<li>rrd=file use file from stashpath instead of live</li>
</ul>
</td>
  <td>Y</td><td>N</td>
</tr>

<tr><td><code>/lm/hmstatus</code></td>
  <td>Get last HeaterMeter status update in JSON format.</td>
  <td>Y</td><td>N</td>

<tr><td><code>/lm/rfstatus</code></td>
  <td>Get last RF12 status update in JSON format</td>
  <td>Y</td><td>N</td>

<tr><td><code>/lm/hist</code></td>
  <td>Get HeaterMeter history in CSV format, which is used to generate the graph.
<ul>
<li>rrd=X use X for the database file instead of the default (may include full path)</li>
<li>nancnt=X specifies the range of the returned data. Values are subject to change but: Not Present=auto 460=1h 360=6h 240=12h else 24h</li>
</ul></td>
  <td>Y</td><td>N</td>

<tr><td><code>/lm/login</code></td>
  <td>Bounce to the LinkMeter login page for authentication.</td>
  <td>Y</td><td>N</td>

<tr><td><code>/lm/set</code></td>
  <td>Passed through to HeaterMeter one parameter at a time. See HeaterMeter Set Parameter list.</td>
  <td>A</td><td>Y</td>

<tr><td><code>/admin/lm/conf</code></td>
  <td>LinkMeter probe and behavior configuration. Front-end to <code>/lm/set</code></td>
  <td>A</td><td>N</td>

<tr><td><code>/admin/lm/home</code></td>
  <td>Bounce to <code>/lm/</code></td>
  <td>A</td><td>N</td>

<tr><td><code>/admin/lm/stashdb</code></td>
  <td>LinkMeter utility URL for managing databases
<ul>
<li>backup=1 backup to stashpath</li>
<li>restore=1 restore to active</li>
<li>reset=1 reset active</li>
<li>rrd=file use file instead of 'hm.rrd' for stashpath file</li>
</ul>
</td>
  <td>A</td><td>N</td>

<tr><td><code>/admin/lm/archive</code></td>
  <td>LinkMeter database archive. Front-end to <code>/admin/lm/stashdb</code></td>
  <td>A</td><td>N</td>

<tr><td><code>/admin/lm/fw</code></td>
  <td>LinkMeter Arduino / AVR firmware upgrade</td>
  <td>A</td><td>N</td>

<tr><td><code>/admin/lm/credits</code></td>
  <td>LinkMeter software credits page</td>
  <td>A</td><td>N</td>

<tr><td><code>/reboot</code></td>
  <td>HeaterMeter software reboot</td>
  <td>N</td><td>Y</td>

<tr><td><code>/config</code></td>
  <td>HeaterMeter dump configuration</td>
  <td>N</td><td>Y</td>

</table>

### HeaterMeter Set Parameters

The definitive source on HeaterMeter set parameters is the [HeaterMeter README](https://github.com/CapnBry/HeaterMeter/blob/master/arduino/heatermeter/README.txt). All set parameters are proceeded by ``/set?`` followed by the parameter name. HeaterMeter only supports one setting one parameter at a time, LinkMeter can set several parameters at once.

| Name | Description |
|------|-------------|
|``sp=A``|Set the setpoint to integer A|
|``pidA=B``|Tune PID parameter A to value float B. A can be b (bias), p (proportional), i (integral), or d (derivative)|
|``pnA=B``|Set probe name A to string B.|
|``poA=B``|Set probe offset A to integer B.|
|``pcN=A,B,C,R,TRM``|Set the probe coefficients and type for probe N.<br/>Any of A,B,C,R,TRM set to 0 will not be modified.<br/>A, B, and C are the Steinhart-Hart coeffieicents and R is the fixed side of the probe voltage divider.<br/>A, B, C and R are floating point and should be specified in scienfific noation, e.g. 0.00023067434 -> 2.3067434e-4.<br/>TRM is either the type of probe OR an RF map specifier. If TRM is an integer, it indicates a probe type.  Probe types are 1=Disabled, 2=Internal, 3=RFM12B.  If the first character of TRM is a capital letter A-Z followed by a single digit number 0-5, it is considered an RF Map item <rfSource (letter)><sourcePin>.<br/>e.g. a TRM of B0 sets this probe to use RF Source B pin 0.  If an RF map is present, the probe type is automatically switched to type RFM12B.|
|``lb=A``|Set the LCD backlight to A.  Range is 0 (off) to 255 (full)|
|``pnXXX``|Retrieve the current probe names (XXX is literally the string "XXX")|

|Probe Number|Description|
|--------------|-------------|
|0| Pit - This is the probe that controls the blower |
|1| Food Probe 1|
|2| Food Probe 2|
|3| Food Probe 3 / Ambient|

|Probe Type (URL)|Probe Type (Code)|Description|
|------------------|-------------------|-------------|
|0| (Undefined) | Do not change probe type |
|1| PROBETYPE_DISABLED (0) | Disabled. Do not measure or report a value for this probe |
|2| PROBETYPE_INTERNAL (1) | Internal. Probe connected directly to HeaterMeter via voltage divider / probe jack / thermistor |
|3| PROBETYPE_RF12 (2) | RFM12B. RF Wireless via RFM12B radio transciever. Probes of this type also require an RFMap item to map the appropriate source node and pin. |
