# Managing a tape device

- [ Source: Managing tape devices ](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/managing_storage_devices/managing-tape-devices_managing-storage-devices#tape-commands_managing-tape-devices "")
- mt -f /dev/st0 status
-

#### I started using bacula but I am going to keep the "mt" tape commands below for future reference.

```
To run bacula from the command line type: bconsole
You can also run it from Webmin once you get it installed.
The main configuration files for bacula are located in /etc/bacula and /usr/libexec/bacula.
There is a bacula log file located here /var/log/bacula/bacula.log.
If you download the bacula tar.gz package, it contains an example folder that has some pretty good examles that can be modified.
```

#### Types of tape devices
    The following is a list of the different types of tape devices:
    /dev/st0 is a rewinding tape device.
    /dev/nst0 is a non-rewinding tape device. Use non-rewinding devices for daily backups.

#### Install the mt-st tool  (Tape drive management tool)
     Install the mt-st package:
```
		dnf -y install mt-st
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

Ejects the tape.
```
		mt -f /dev/st0 eject
```

```

https://unix.stackexchange.com/questions/564146/simple-tools-to-read-write-tapes-on-linux
We used to store multiple tar archives on a single tape, on Solaris with QIC tapes.

To manage the physical tape, there is the mt(1) command. Specifically, this lets you space forward and back using tape marks, using either absolute or relative numbering. Confusingly, the terminology uses "files" in the sense of multiple sub-files separated by tape marks. A complete tar archive would correspond to a "file".

The mt command has a binary and a man page on my Linux Mint 18.1. Tapes are pretty non-standard -- some types of deck won't have all the commands, but tapemarks are pretty fundamental.

Standard tape devices usually rewind by default before and after each use, thereby destroying any pre-positioning you do. Typically, each deck has a designator like /dev/rmt0, and an additional device for the same physical unit like /dev/nrmt0 where the n says "no rewind".

So you embed your append tar command in a script that does something like:

		mt -f /dev/nrmt0 rewind
		mt -f /dev/nrmt0 eod
		tar -f /dev/nrmt0 ...
		mt -f /dev/rmt0 offline

You would need to keep a catalogue of which archives are on which tape and which subfile, and your retrieval would be like:

		mt -f /dev/nrmt0 rewind
		mt -f /dev/nrmt0 fsf 17
		tar -f /dev/nrmt0 ...

Breaking your archives into many smaller sections, and skipping between them, would be a significant optimisation for retrieving small numbers of files.
```

