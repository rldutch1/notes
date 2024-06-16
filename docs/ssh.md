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

