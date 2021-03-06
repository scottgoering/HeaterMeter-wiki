# HTTP Basic Realm Authentication

** WARNING: ** This is a tremendous security risk as it allows someone to perform [Cross-Site Request Forgery](http://en.wikipedia.org/wiki/Cross-site_request_forgery) using login information stored in your browser while visiting another site. Use at your own risk!

By default LuCI uses an interstitial login page to pass from the public LinkMeter home page to the authenticated area where configuration changes may be made. Some may prefer restricting access via a "basic realm authentication" username / password popup. You must disable cookies for this to work more than once.

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

  * Set a login password using the default website.
  * SSH into the LinkMeter
  * Edit the /etc/config/lucid configuration adding a new handler section
```
config LuciWebPublisher 'luciwebauth'
        option name 'LinkMeter Authentication'
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

## NO COOKIES!

If you're not getting the basic realm authentication prompt or you get the authentication prompt followed by the interstitial login page, you must delete the LinkMeter site's "sysauth" cookie from your web browser. The sysauth cookie can muck up the logic determining which login method is to be used.