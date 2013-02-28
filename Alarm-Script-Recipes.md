LinkMeter on the RaspberryPi has the ability to fire off user scripts when an alarm goes off. This is in addition to beeping the piezo buzzer. This requires some degree of Linux shell scripting expertise, but using some of these recipes might make things a little easier to understand.

# A Note About Alarm Arming
To prevent alarms from turning on and off every time the temperature bounces back and forth across the alarm point there is a _hysteresis_. This means that the temperature must be outside of the alarm range by more than 1 degree before the alarm will "arm" and be capable of sounding.

Example: Your current temperature is 99.9, and you set the high alarm for 100 at this time. Your alarm is not armed yet and will not arm until is is a degree from the alarm threshold, that is below 99, say 98.9. Even if the temperature rises to 500 the alarm will not go off, as it was never armed.

Now assume the current temperature is 98.9, and you set the high alarm for 100. When it hits 100, the alarm will fire. Even if it drops back below 100, it will keep ringing until silenced. Silencing the alarm only silences the alarm. If the temperature drops below 99 again, the alarm will rearm, and then goes back over 100, the alarm fires again.

Action | Will Ring Again? | Must Re-Arm?
-------|------------------|-------------
Press any button on HeaterMeter unit | Yes | Yes
Unplug the alarming probe | Yes | Yes
Clicking 'Silence' on web popup | Yes | Yes
Open the lid until lid detect activates | Yes | No
Un-ticking Alarm 'On' in web config page | No | Yes
Setting the trigger point negative with al_set | No | Yes

## Editing Scripts
### Via Web
From the LinkMeter configuration website navigate to LinkMeter -> Alarm Scripts. Each script has its own reset / save button! Do not try to edit multiple scripts without saving each in between. The script will only run if the "Execute on alarm" box is checked at the time the alarm goes off (currently ringing alarms have no effect).

### Manually
First of all, alarm scripts are located in /usr/share/linkmeter/. Do not edit the script named "alarm", as this file will be replaced every time LinkMeter is upgraded and you will lose all changes. Instead, create new files for your scripts. The system first looks for alarm-all, and executes that. If the return value of that script is zero (the default), the system looks for a file named alarm-{probeidx}{alarmtype}. To not execute the alarm-specific script, exit alarm-all with a non-zero return code (e.g. `exit 1`).

For example if the Pit probe high alarm is going off, it will look for alarm-0H. These files can be a shell scripts, lua scripts, or a regular ARM ELF binaries. These recipes can be used for either an alarm-specific or alarm-all file. The files must be executable, i.e. `chmod +x` or they will not be run.

There are many variables available to use in your scripts. From a command prompt execute `lmclient LMCF` for a list. In addition, the alarm system adds al_probe, al_type, al_thresh, pn (alarm probe name), pcurr (alarm probe current value) variables. The `al_set` function can be used to change the value of the current alarm.

## Recipes
### All scripts
~~~
#!/bin/sh
# The first line of any shell script must begin with the above #! line 
# Comments begin with #
~~~

### Turn the alarm off
~~~
# Silence this alarm, it will ring again if re-armed
al_set 0
~~~
or
~~~
# Disable this alarm, it will not ring again
al_set -$al_thresh
~~~

### Sending an Email
This requires that /etc/msmtprc be configured with the proper email server information. Note that many ISPs will block regular email traffic (on port 25) so you'll probably need to use SMTP over SSL on port 465.
~~~
sendmail bmayland@myemail.net << EOF
From: Bryan Mayland <bmayland@myemail.net>
To: Bryan Mayland <bmayland@myemail.net>
Subject: [HM] $pn Alert

Alarm $al_type outside threshold $al_thresh, currently $pcurr.

$pn0: $pcurr0
$pn1: $pcurr1
$pn2: $pcurr2
$pn3: $pcurr3

--
http://your.heatermeter.address/luci/lm/
EOF
~~~

### SMS Message
SMS relies on going through your cell provider's email to SMS gateway so, again, the /etc/msmtprc must be configured for proper email delivery.
~~~
echo "$pn Alert -- $pcurr \($al_type\)" | sendmail 2125551212@messaging.sprintpcs.com
~~~
#### Provider SMS Email Gateways
A full list of global SMS gateways can be found at Wikipedia's [List of SMS gateways](http://en.wikipedia.org/wiki/List_of_SMS_gateways).

Provider | Address 
-----|-----
AT&T | phonenumber@txt.att.net
Nextel | phonenumber@messaging.nextel.com 
Sprint | phonenumber@messaging.sprintpcs.com
T-Mobile | phonenumber@tmomail.net
Verizon | phonenumber@vtext.com
Virgin Mobile | phonenumber@vmobl.com

### HeaterMeter Control - Shutdown
Often you want to turn off the Pit when your food is done. This is easily done using lmclient to send a command to HeaterMeter to change the setpoint.
~~~
# Lower the setpoint to 100
lmclient LMST,sp,100
~~~

### HeaterMeter Control - Ramp Down
You can do more complicated setpoint control with a ramp down script.
~~~
case $al_thresh in
  180) NEWSP=215; NEWAL=190; ;;
  190) NEWSP=205; NEWAL=200; ;;
  200) NEWSP=100; NEWAL=0; ;;
esac

lmclient LMST,sp,$NEWSP
al_set $NEWAL
~~~

### HeaterMeter Control - Super Ramp Down
10 degrees too much? That's ok you can ramp down one degree for every degree the meat climbs if you like
~~~
if [ "$al_thresh" -gt 199 ] ; then
  # done
  lmclient LMST,sp,100
  exit
fi

NEWSP=$((sp-1)
NEWAL=$((al_thresh+1))
lmclient LMST,sp,$NEWSP
al_set $NEWAL
~~~

### Time Delays (UNTESTED)
Often you may not want be notified when the alarm happens but some time after it happens. Cron can be used. Note cron only has per-minute resolution so don't try to make things happen every N seconds.
~~~
# If no parameter, this is a regular alarm
if [ -z "$1" ] ; then
  NOW=`date +%s`
  # Set target for 1 hour from now 3600=seconds
  WHEN=$((NOW+3600))

  TARGET=`date -D "%s" -d $WHEN +"%M %H %d %m"`
  echo "$TARGET * /usr/share/linkmeter/alarm-all RING${al_probe}" | crontab -
else
  # This is the cron callback
  # Don't fire again
  crontab -r

  # Do whatever you want here, using another recipe
fi
~~~

## MSMTP Configuration
The mail transfer agent "msmtp" must be configured before any of the sendmail (email/SMS) commands will work. Edit `/etc/msmtprc` with the information appropriate for your mail server

### SMTP over SSL / Gmail
~~~
account default
host smtp.gmail.com
port 465
auth on
tls on
tls_certcheck off
tls_starttls off
from yourname@gmail.com
user yourname@gmail.com
password password
~~~

### Hotmail / Windows Live Mail
~~~
account default
host smtp.live.com
port 587
tls on
tls_certcheck off
auth on
from yourname@hotmail.com
user yourname@hotmail.com
password password
~~~