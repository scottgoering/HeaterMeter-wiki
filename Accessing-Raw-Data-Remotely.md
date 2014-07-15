This list may not always be fully up to date. The JSON data is pretty self-explanitory so always refer to a live LinkMeter system for the most up-to-date parameter information.

## Discovery

LinkMeter includes support for autodiscovery of devices via the ZeroConf/mDNS/DNS-SD (Bonjour/Avahi) protocol. The service is advertised as an _http._tcp (Web Site) service with the name `LinkMeter BBQ Controller on %h` where %h is the hostname. The txt record contains a path key which is the URI of the LinkMeter webpage (always `/luci/lm` for now).

## Current Status

The current status (probe temperatures, etc) in JSON format can be fetched from the `/luci/lm/hmstatus` URI.

~~~
{
  "time":1405429467,
  "set":65,
  "lid":38,
  "fan":{"c":0,"a":13},
  "adc":[0,0,0,0,0,3],
  "temps":[
    {
      "n":"Probe 0",
      "c":78.6,
      "dph":1.3,
      "a":{"l":-40,"h":200,"r":null}
    },
    ...
  ]
}
~~~
|Field|Example|Description|
|-----|-------|-----------|
|time|1405429467|Current time (hopefully in UTC) in UNIX timestamp format (example is Tue, 15 Jul 2014 13:04:27 UTC). Might be incorrect if device has no Internet access.|
|set|65|PID Set Point (can be C or F but doesn't specify)|
|lid|38|Lid Open countdown timer. Number of seconds remaining in lid mode or 0 if lid mode is off|
|fan.c|0|Current PID output percentage|
|fan.a|13|Average PID output percentage over last few minutes|
|adc[]|0,0,0,0,0,3|ADC noise range indicator. Probe 0 is adc[5], Probe 1 is adc[4], etc. May be absent if not supported.|
|temps[X].n|Probe 0|Name assigned to probe|
|temps[X].c|78.6|Current probe temperature|
|temps[X].dph|1.3|Degrees per hour calculated (least squares linear fit). May be null if not enough data, or missing if not supported|
|temps[X].a.l|-40|Probe alarm low trigger. Negative numbers indicate alarm is disabled|
|temps[X].a.h|200|Probe alarm high trigger. Negative numbers indicate alarm is disabled|
|temps[X].a.r|null|Probe alarm ringing. "L" or "H" if the alarm is currently triggered or null if no alarm ringing|

## Streaming Status

The current status can also be streamed using the HTTP server-sent events protocol from the URI `/luci/lm/stream`. Updates are sent with between 1 and 5 seconds, depending on changes in the data.

~~~
Content-Type:text/event-stream

event: hmstatus
data: {"time":1405429467,"set":65,"lid":38,...}

event: hmstatus
data: {"time":1405429469,"set":65,"lid":36,...}

event: hmstatus
data: {"time":1405429471,"set":65,"lid":34,...}
~~~

|Event|Description|
|-----|-----------|
|hmstatus|Current Status update|
|log|Debugging log message|
|alarm|Alarm was just triggered|
|pidint|PID internals dump enabled by the user|

## Historical Data

Graph data is in CSV format and is accessible from the URI `/luci/lm/hist`. The fields are UNIX timestamp, Setpoint, Probe 0, Probe 1, Probe 2, Probe 3, Lid Open. Probe fields can be "nan" if no probe was inserted at the time. Requesting the data with no parameters will autoscale and return the best range of data to fit the amount stored in the database. Adding the `nancnt=X` parameter to the query can adjust the range.

|nancnt|Range|
|------|-----|
|460|1 hour|
|360|6 hours|
|240|12 hours|
|0|24 hours|

~~~
1405344600,65,94.043333333333,nan,44.475555555556,82.325555555556,0
1405344780,65,93.503333333333,nan,44.792222222222,82.635555555556,0
1405344960,65,93.166388888889,nan,45.036111111111,82.865,0
1405345140,65,92.903611111111,nan,45.281111111111,83.07,0
1405345320,65,92.672777777778,nan,45.592222222222,83.1,0
1405345500,65,92.414444444444,nan,45.794444444444,83.211111111111,0
1405345680,65,92.141111111111,nan,46.016666666667,83.473333333333,0
1405345860,65,92.037777777778,nan,46.314444444444,83.727222222222,0
1405346040,65,92.362222222222,nan,46.534444444444,83.935555555556,0
1405346220,65,92.021666666667,nan,46.795,84.147777777778,0
1405346400,65,91.818888888889,nan,46.982222222222,84.41,0
1405346580,65,91.867777777778,nan,47.156666666667,84.571111111111,0
1405346760,65,91.804444444444,nan,47.404444444444,84.6,0
1405346940,65,91.769444444444,nan,47.621111111111,84.626666666667,0
1405347120,65,91.727777777778,nan,47.796666666667,84.707777777778,0
1405347300,65,91.587222222222,nan,47.982222222222,84.888888888889,0
1405347480,65,91.707777777778,nan,48.182222222222,84.751111111111,0
~~~

## Changing Settings

Changing parameters (such as the setpoint) requires a valid login session. To log in, pass a valid `username=X` and `password=X` as parameters to any secure URI. The web server will return the cookie "sysauth" which must be used for subsequent access. The URL returned will also contain an "stok" token which must be inserted into requested secure URIs.

~~~
Request:
POST /luci/admin/lm HTTP/1.1

username=root
password=plaintextpassword

Response:
HTTP/1.1 200 OK
Set-Cookie:sysauth=9b735437932ce9486dccc6345ec18a0b; path=/luci/;stok=fc9434a4f4c06b0ecd73486cc1eb1e29
~~~

In the above example, secure URIs can now be accessed using the sysauth and stok pair

~~~
POST /luci/;stok=fc9434a4f4c06b0ecd73486cc1eb1e29/admin/lm/set HTTP/1.1
Cookie: sysauth=9b735437932ce9486dccc6345ec18a0b;

sp=225
~~~