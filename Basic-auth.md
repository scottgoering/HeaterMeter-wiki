# HTTP Basic Realm Authentication

By default LuCI uses an interstitial login page to pass from the public LinkMeter home page to the authenticated area where configuration changes may be made. Some may prefer restricting access via a "basic realm authentication" username / password popup.

## Enabling on the default site

  * Set a login password using the default website. If a password is not set you will no longer be able to log in once basic auth is enabled!
  * SSH into the LinkMeter
  * Add "root" to the list of restricted users of the luci virtual host
```
uci add_list lucid.luciweb.exec=root
uci commit lucid
/etc/init.d/lucid restart
```

## Enabling on a secondary site

It may be preferred to retain the default interstitial login site but add a secondary site which uses basic realm authentication. 

  * Set a login password using the default website. If a password is not set you will no longer be able to log in once basic auth is enabled!
  * SSH into the LinkMeter
  * Edit the /etc/config/lucid configuration adding a new handler section
```
config LuciWebPublisher 'luciwebauth'
        list virtual '/luci-auth'
        list exec 'root'
```
  * Add the publisher to the existing http and http sections of the lucid configuration
```
config daemon 'http'
        list publisher 'luciwebauth'

config daemon 'https'
        list publisher 'luciwebauth'
```
  * Restart lucid for the changes to take effect `/etc/init.d/lucid restart`