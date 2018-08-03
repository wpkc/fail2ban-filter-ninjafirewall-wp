# fail2ban-filter-ninjafirewall-wp

Fail2Ban Filter for Ninjafirewall WP
====================================

How to use:

* Install Ninjafirewall WP to you WordPress web site.
* Enable brute force attack protection in Ninjafirewall (recommended setting: "Always ON").
* Checkmark "Write the incident to the server Authentication log."
* Copy /filter.d/ninjafirewall.conf from this repository to /etc/fail2ban/filter.d/
* Add a [ninjafirewall] section to the Jails section of /etc/fail2ban/jail.local file...

	[ninjafirewall]
	port = http,https
	filter = ninjafirewall
	logpath  = %(syslog_authpriv)s
	backend  = %(syslog_backend)s
	maxretry = 2
	enabled = true
	
* Restart your Fail2Ban service.


Additional Notes:

* Keep the maxretry override value low. Ninjafirewall is detecting automated brute-force attacks, not accidental password errors by humans.
* If using CloudFlare on the web site, please see the fail2ban-action-cloudflare-restv4 repository for an updated CloudFlare action configuration file.

