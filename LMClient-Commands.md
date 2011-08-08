These are commands which can be passed to the linkmeter daemon over the UNIX socket. All commands begin with "$LM", however $ symbol is optional when using the lmclient.lua script.  If the script is called with no command, $LMSU is assumed.

* LMST,X,Y - Set command. Passes a /set?X=Y to the HeaterMeter. X and Y must *not* be URL encoded. Returns OK or ERR.
* LMSU - Request state update. Returns the last state update from the HeaterMeter, JSON-formatted. Includes UNIX timestamp and RF status when available.
* LMRF - Get RF status. Returns current RF node status information.  Last seen UNIX timestamp, battery level, and signal level.
* LMD0 - Stop the serial monitor daemon, the actual linkmeterd portion that receives and records data.
* LMD1 - Start the serial monitor daemon.

## Invocation

    lua /usrl/lib/lua/lmclient.lua [command]

### Examples

    root@lm54:~# lua /usr/lib/lua/lmclient.lua LMSU
    {"time":1312821641,"set":55,"lid":0,"fan":{"c":0,"a":0},"temps":[{"n":"Pit","c":81.4},
    {"n":"LUA Mem","c":null},{"n":"Batt Voltage","c":null},{"n":"Ambient","c":51.4,"rf":{"s":255,"b":1248}}]}
    
    root@lm54:~# lua /usr/lib/lua/lmclient.lua LMRF
    [{"id":"A","batt":3300,"rssi":255,"last":1312821661},{"id":"B","batt":1251,"rssi":255,"last":1312821651}]

    root@lm54:~# lua /usr/lib/lua/lmclient.lua LMST,sp,55
    OK
