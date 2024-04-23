Enable X11 on Server
```
Edit /etc/ssh/ssh_config
	ForwardX11 yes
	X11Forwarding yes
	Uncomment: X11DisplayOffset
```

On Client: (This is all I needed for Fedora).
Start Terminal and connect to the SSH server which is enabled X11 Forwarding with
```
ssh -XC username@hostname
```

For CentOS:
After connecting, input commands like follows.
$ eval `dbus-launch --sh-syntax`
$ export DBUS_SESSION_BUS_ADDRESS
$ export DBUS_SESSION_BUS_PID

