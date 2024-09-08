https://www.server-world.info/en/note?os=CentOS_7&p=selinux&f=7

1. Messages via Rsyslog are generated with "kern" facility. CentOS default Rsyslog setting is written as "*.info;xxx /var/log/messages", so AVC Denial Log is recorded to /var/log/messages.
	grep "avc: .denied" /var/log/messages

2. Messages via Auditd are generated to /var/log/audit/audit.log.
	grep "avc: .denied" /var/log/audit/audit.log

3. For Messages via Auditd, it's possible to search them with ausearch command.
	ausearch -m AVC

4. For Messages via Auditd, it's possible to show summary reports with aureport command.
	aureport --avc --summary

STAT command to show SE_Linux status: stat -c "%a %n %C" *


