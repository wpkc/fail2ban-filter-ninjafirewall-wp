Fail2Ban Filter for Ninjafirewall WP
====================================

Note: _This will only work if you have full access to your web server's `/etc/fail2ban/` files._

How to use:

* Install [Ninjafirewall WP](https://wordpress.org/plugins/ninjafirewall/) to your WordPress web site.
* Enable brute force attack protection in Ninjafirewall ("Yes, if under attack" is the only setting that will generate brute-force attack log entries).
* Checkmark `Write the incident to the server Authentication log.`
* Copy [/filter.d/ninjafirewall.conf](https://github.com/wpkc/fail2ban-filter-ninjafirewall-wp/blob/master/filter.d/ninjafirewall.conf) from this repository to `/etc/fail2ban/filter.d/`
* Add a `[ninjafirewall]` section to the Jails section of your `/etc/fail2ban/jail.local` file...
```python
	[ninjafirewall]
	port = http,https
	filter = ninjafirewall
	logpath  = %(syslog_authpriv)s
	backend  = %(syslog_backend)s
	maxretry = 2
	enabled = true
```
* Restart Fail2Ban: `service fail2ban restart`


Additional Notes:

* Keep the maxretry override value low; 2 is good. Ninjafirewall is detecting automated brute-force attacks by bots, not accidental password errors by humans.
* If using CloudFlare on the web site, please see the [fail2ban-action-cloudflare-restv4](https://github.com/wpkc/fail2ban-action-cloudflare-restv4) repository for an updated CloudFlare action configuration file.

More info: <https://www.kazimer.com/fail2ban-filter-recipe-ninjafirewall/>
