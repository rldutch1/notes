[Source: ](https://www.server-world.info/en/note?os=CentOS_7&p=selinux&f=7)

###Places to search for AVC messages:
Messages via Rsyslog are generated with "kern" facility. CentOS default Rsyslog setting is written as "*.info;xxx /var/log/messages", so AVC Denial Log is recorded to /var/log/messages.

```
	grep "avc: .denied" /var/log/messages
```

Messages via Auditd are generated to /var/log/audit/audit.log.

```
	grep "avc: .denied" /var/log/audit/audit.log
```

For Messages via Auditd, it's possible to search them with ausearch command.

```
	ausearch -m AVC
```

For Messages via Auditd, it's possible to show summary reports with aureport command.

```
	aureport --avc --summary
```

STAT command to show SE_Linux status:

```
stat -c "%a %n %C" *
```

Allow apache to receive files to an uploads folder/directory:

```
sudo chown apache:apache -R /uploads
sudo chcon -Rv --type=httpd_sys_rw_content_t uploads/
```

```
With /srv/ as the base directory you must adjust the SELinux labels.
htdocs is where the index.php/html file goes.

[…]# /usr/sbin/semanage fcontext -a -t httpd_sys_content_t  -s system_u  "/srv/SITENAME/htdocs(/.*)?"
[…]# /sbin/restorecon -R -vF /srv/SITENAME/htdocs
Relabeled /srv/SITENAME/htdocs from unconfined_u:object_r:var_t:s0 to system_u:object_r:httpd_sys_content_t:s0
Source: https://docs.fedoraproject.org/en-US/fedora-server/services/httpd-basic-setup/#_installation
```

Change the SE Linux properties of a file: (Source: https://www.thegeekstuff.com/2017/07/chcon-command-examples/)
Example: this Test2a.php file was displaying "Access Denied" error on my website.

Check and change the SELinux properties:
```
	Check the current SELinux properties with: ls -Z
		The properties were: unconfined_u:object_r:user_home_t:s0 Test2a.php

	I changed the SELinux properties using:
		sudo chcon unconfined_u:object_r:httpd_user_content_t:s0 Test2a.php
```

If you want to copy the SE_Linux settings from one directory that is working to another:
```
	# semanage fcontext --add --equal /var/www/html /opt/www/html
	# restorecon -rv /opt/www/html
```

If you are using a non-standard directory for web files, like /opt/www/html, then you may not be able to use restorecon to automatically fix the SELinux context. You will have to set the context using chcon and save the change using semanage to make the change permanent:
```
	# chcon -R system_u:object_r:httpd_sys_content_t:s0 /opt/www
	# semanage fcontext -a -t httpd_sys_content_t "/opt/www(/.*)?"
	# restorecon -rv /opt/www
```

If you get "SQLSTATE[HY000] [2002] Permission denied" message. You need to enable the httpd service to network connect.
You must check in the SELinux if port 80 is managed in. You can check it by typing # semanage port -l | grep http_port_t for a list and check:
```
		semanage port -l | grep http_port_t
```

If you need to add the required port, just type:
```
		# semanage port -a -t http_port_t -p tcp 80
```

		Stop the httpd service set the SE_Linux permission and start the http service.

		Down the httpd service #
```
		service httpd stop
```
		Enable the httpd service to connect to the network:
```
		# setsebool -P httpd_can_network_connect 1
		# setsebool -P httpd_can_network_connect_db 1
```
		Check if the service is enabled:
```
		getsebool httpd_can_network_connect
		getsebool httpd_can_network_connect_db
```
		Up the httpd service # 
```
		service httpd start
```
