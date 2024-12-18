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

