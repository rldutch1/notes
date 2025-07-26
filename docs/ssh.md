#SSH
Enable service to run at boot:
  <span style="color: #3366ff;">systemctl enable sshd.service</span><br />

Start the SSH service:
  <span style="color: #3366ff;">systemctl start sshd.service</span><br />

Offending ECDSA key in /home/someuser/.ssh/known_hosts:4<br />
  Remove with:<br />
  <span style="color: #3366ff;">ssh-keygen -f "/home/someuser/.ssh/known_hosts" -R "theservername.com"</span><br />

Copy SSH public key to remote computer:
  <span style="color: #3366ff;">ssh-copy-id -i ~/.ssh/id_rsa.pub user@hostname</span><br />

#### SSH: Broadcast message: The system will suspend now! client_loop: send disconnect: Broken pipe
You can display the current sleep/suspend settings with a command like this one:

<span style="color: #3366ff;">sudo -u gdm dbus-run-session gsettings list-recursively org.gnome.settings-daemon.plugins.power | grep sleep</span><br />

The problem of getting kicked out of the remote computer when the computer goes into hybernate mode was solved with the following:<br />
<span style="color: #3366ff;">systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target</span><br />
[Source:](https://pagure.io/fedora-workstation/issue/360)<br />

