### What port do I need to forward to access the web site from outside my network?

80 (http, no encryption) or 443 (https, encrypted)

### What other ports are accessible on the LinkMeter OpenWrt firmware?

Don't open holes in your firewall for all of these! To access the web site only port 80 or port 443 is needed.

* TCP
  * 22 - SSH (only once a password has been set)
  * 23 - Telnet (only before a password has been set)
  * 80 - http (web server)
  * 443 - https (secure web server with self-signed certificate)
* UDP
  * 5353 - mDNS (Bonjour service discovery)