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