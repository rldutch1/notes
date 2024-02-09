# Managing a tape device

- [ Source: Managing tape devices ](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/managing_storage_devices/managing-tape-devices_managing-storage-devices#tape-commands_managing-tape-devices "")
- mt -f /dev/st0 status
- 

#### Types of tape devices
    The following is a list of the different types of tape devices:
    /dev/st0 is a rewinding tape device.
    /dev/nst0 is a non-rewinding tape device. Use non-rewinding devices for daily backups. 

#### Install the mt-st tool  (Tape drive management tool)
     Install the mt-st package:
```
    # dnf -y install mt-st
```

#### Tape commands:
Erases the entire tape.
```
 mt -f /dev/st0 erase
```	

Rewinds the tape device.
```
mt -f /dev/st0 rewind
```	

Switches the tape head to the forward record. Here, n is an optional file count. If a file count is specified, tape head skips n records.
```
mt -f /dev/st0 fsf n <--(n is the count (see man mt))
```	

Switches the tape head to the previous record.
```
mt -f /dev/st0 bsfm n
```	

Switches the tape head to the end of the data. 
```
mt -f /dev/st0 eod
```	

