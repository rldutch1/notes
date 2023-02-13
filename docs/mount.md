#Mounting and Unmounting a LUKS Encrypted USB Volume

### Use the following commands to view the disks/USB devices:

- blkid
- duf
- lsblk
- lsblk -a
- lsblk -o +UUID,PARTUUID
- lsblk -o +UUID,FSTYPE,PARTUUID
- ls -lF /dev/disk/by-id
- sudo lshw -short -C disk
- sudo udisksctl info -b /dev/??

### 01. USB drive has not been inserted (plugged in) yet.

`$ To see volumes type: lsblk`

![ Running lsblk shows what is currently mounted.](/img/x01.png "Running lsblk shows what is currently mounted.")

### 02. GUI password prompt when drive is plugged in (I clicked cancel to demonstrate mounting from commandline).

![ I clicked cancel to demonstrate mounting from commandline.](/img/x02.png "I clicked cancel to demonstrate mounting from commandline.")

### 03. USB drive inserted (plugged in) and showing as /dev/sdm1.

`$ To see volumes type: lsblk`

![ USB drive inserted (plugged in) and showing as /dev/sdm1.](/img/x03.png "USB drive inserted (plugged in) and showing as /dev/sdm1. Your volume name may be different than /dev/sdm1.")

### 04. udiskctl showing /dev/sdm1 as "crypto_LUKS"..

`$ Check the volume information type: sudo udisksctl info -b /dev/sdm1`

![ See the various commands above to view drive/volumes. Your volume name may be different than /dev/sdm1.](/img/x04.png "See the various commands above to view drive/volumes. Your volume name may be different than /dev/sdm1.")

### 05. Trying to mount the locked LUKS encrypted volume (Failed because volume is locked. Run cryptsetup first to unlock.).

![ See the various commands to view drive/volumes above.](/img/x05.png "See the various commands to view drive/volumes above.")

### 06. Running cryptsetup to unlock the encrypted volume (Assigning alias of "2T_SSD" to reference the unlocked volume. The alias can be whatever you want.).

`$ To open the encrypted filesystem type: sudo cryptsetup luksOpen /dev/sdm1 2T_SSD`

![ The alias name can be whatever you want.](/img/x06.png "The alias name can be whatever you want.")

### 07. Decrypted volume showing as 2T_SSD, but not yet mounted.

`$ To see the unlocked volume type: lsblk`

![ Decrypted volume showing the 2T_SSD alias, but not yet mounted.](/img/x07.png "Decrypted volume showing the 2T_SSD alias, but not yet mounted.")

### 08. Decrypted volume alias "2T_SSD" showing under /dev/mapper.

`$ Check /dev/mapper to see if your alias is there: ls -al /dev/mapper`

![ Decrypted volume alias "2T_SSD" showing under /dev/mapper.](/img/x08.png "Decrypted volume alias "2T_SSD" showing under /dev/mapper.")

### 09. Password prompt when using sudo to mount decrypted 2T_SSD volume to /dev/m.

`$ To mount your alias to a mount point type: sudo mount /dev/mapper/2T_SSD /mnt/m`

![ Password prompt when using sudo to mount decrypted 2T_SSD volume to the /dev/m mount point (The mount point can be whatever you want.](/img/x09.png "Password prompt when using sudo to mount decrypted 2T_SSD volume to the /dev/m mount point (The mount point can be whatever you want.")

### 10. Decrypted volume showing unlocked and mounted at /mnt/m.

`$ To see volumes type: lsblk`

![ Decrypted volume showing unlocked and mounted at /mnt/m.](/img/x10.png "Decrypted volume showing unlocked and mounted at /mnt/m.")

### 11. Unmounting /mnt/m.

`$ To unmount th volume type: /mnt/m`

![ Unmounting /mnt/m.](/img/x11.png "Unmounting /mnt/m.")

### 12. Closing cryptsetup session (Locking it).

`$ To close the volume type: sudo cryptsetup close 2T_SSD`

![ Closing cryptsetup session (Locking it).](/img/x12.png "Closing cryptsetup session (Locking it).")

### 13. USB drive unmounted and unplugged from system.

`$ To see volumes type: lsblk`

![ USB drive unmounted and unplugged from system.](/img/x13.png "USB drive unmounted and unplugged from system.")
