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

<tr><td><code>/lm/stream</code></td>
  <td>Get streaming HeaterMeter status updates in HTTP server-sent events format. The individual events are in JSON format.</td>
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
<li>rrd=file use file instead of 'hm.rrd' for stashpath file (do not include path)</li>
<li>delete=1 delete stashpath file and any metadata</li>
</ul>
</td>
  <td>A</td><td>N</td>

<tr><td><code>/admin/lm/alarms</code></td>
  <td>LinkMeter simple alarm script editor</code></td>
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
|``sp=AU``|Set the setpoint to integer A with optional units U. Supported Units are (F)ahrenheit , (C)elcius, and (R)esistance|
|``pidA=B``|Tune PID parameter A to value float B. A can be b (bias), p (proportional), i (integral), or d (derivative)|
|``pnA=B``|Set probe name A to string B.|
|``poA=B``|Set probe offset A to integer B.|
|``pcN=A,B,C,R,TRM``|Set the probe coefficients and type for probe N.  A, B, and C are the Steinhart-Hart coeffieicents and R is the fixed side of the probe voltage divider.  A, B, C and R are floating point and can be specified in scienfific noation, e.g. 0.00023067434 -> 2.3067434e-4.  TRM is either the type of probe OR an RF map specifier.  If TRM is less than 128, it indicates a probe type.  Probe types are 0=Disabled, 1=Internal, 2=RFM12B.  Probe types of 128 and above are implicitly of type RFM12B and indicate the transmitter ID of the remote node (0-63) + 128. e.g. Transmitter ID 2 would be passed as 130. The value of 255 (transmitter ID 127) means "any" transmitter and can be used if only one transmitter is used.  Any of A,B,C,R,TRM set to blank will not be modified. Probe numbers are 0=pit 1=food1 2=food2 3=ambient|
|``lb=A,B``|Set the LCD backlight to A.  Range is 0 (off) to 255 (full). B sets the home screen mode. 255 for two-line display, or probe number (0-30 for bignum display |
|``ld=A,B,C``|Set the offset of the Lid Open autodetect in % of set point to A. Set the duration of the Lid Open timer in seconds to B. You can not set the duration to less than LIDOPEN_MIN_AUTORESUME. Max is 65535 seconds. C is used to enable or disable a currently running lid detect mode. Non-zero will enter lid open mode, zero will disable lid open mode|
|``al=L,H[,L,H...]``|Set probe alarms thresholds. Setting to a negative number will disable the alarm, setting to 0 will force the current set value negative (disabling the alarm but retaining the set value)|
|``fn=L,H,I``|Set the fan output parameters. L = min fan speed before "long PID" mode, H = max fan speed, I = Invert PWM polarity so that 100% actually outputs 0% and 0% outputs 100%|
|``tt=XXX[,YYY]``|Display a "toast" message on the LCD which is temporarily displayed over any other menu and is cleared either by timeout or any button press. XXX and YYY are the two lines to displau and can be up to 16 characters each.|

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