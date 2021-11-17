##Volume Group Quick Info: 

#### Volumegroup commands
	sudo vgs - Show volume groups and information about them.
	sudo vgscan - Show any volume group that is found. Encrypted volume groups will not show unless open by luks.
	sudo vgscan --mknodes (checks the LVM special files in /dev that are needed for active LVs and creates any missing ones and removes unused ones.)
	sudo vgdisplay - Show more detailed information about each volume group. (-v will show more verbose, -vv even more).
	sudo vgchange -ay  (VG change active yes)
	sudo pvs - Show information about the physical volumes.
	sudo pvscan - Show information about the physical volumes.
	sudo pvdisplay - Show more detailed information about each physical volume. (-v will show more verbose, -vv even more).
	sudo lvs - Show information about logical volumes.
	sudo lvscan - Show active/inactive logical volumes.
	sudo lvdisplay - Show detailed information about the logical volumes. (-v will show more verbose, -vv even more).
	sudo lvdisplay|grep "LV Path" 
	sudo lsblk -a  Show volumes and where they are mounted.
	gnome-disks --block-device=/dev/sdX - Opens the disk manager for the volume specified.
	sudo blkid |grep crypto - Show the encrypted volume IDs.
	sudo cryptsetup luksOpen /dev/sdX TheUUIDofTheDevice - Open the encrypted volume.
	sudo udisksctl dump - Show an insane amount of information about the volumes.

	Examples: 
	sudo mount /dev/volumegroupname/logicalvolumename /mnt/mountpoint 
	sudo mount /dev/vg_data/lv_data2 /mnt/data2
	sudo mount -a #Mount everything in /etc/fstab.
	https://github.com/rlholland/miscellaneous/blob/master/Linux/Logical_Volume_Manager.txt.
	https://evilshit.wordpress.com/2012/10/29/how-to-mount-luks-encrypted-partitions-manually..


#### Check information about storage devices:
Run fdisk -l to see information about storage devices.
The ones that show "Linux LVM" are logical volumes that haven't been created into physical volumes using (pvcreate).

	Type: pvcreate /dev/sda2 (Use -v to see verbose information. The more -v's the more information you will see.)
	Type: pvs to see the volume that was just created.
	Type: pvremove /dev/sda2

####Any time you can see all block devices that may be used as a PV, use the command:
	Type: lvmdiskscan
	This will show you the devices that "pvcreate" has been used on (LVM physical volume) and can be used as a physical volume. It also shows devices that pvcreate has not been used on (do not show up as LVM physical volume).

####Once the physical volume is created you need to add it to a Volume Group:
	Create the volume group and add the PV to it in one command:
	Type: vgcreate vgVolume_Group_Name /dev/sda2
	EX: vgcreate onevg /dev/sda2
	If you want more than one PV in your VG:
	EX: vgcreate onevg /dev/sda2 /dev/sda3
	Type: vgremove to delete it. Make sure there are no LV and no data before removing VG.
	EX: vgremove onevg

####To see information about the volume group:
	Type: pvs (Physical Volume Show)
	This will show you the physical volume(s), the volume group, format, physical size, and physical free

	You can also use another command to see information about the volume group:
	Type: vgs (Volume Group Show)
	EX: vgs -vv
	This will show you the attributes, extent size, physical volumes, logical volumes, serial number, volume size, volume free

	Display information about the physical volumes:
	Type: pvdisplay

####If you add another physical device you can add it to a volume group:
	Type: vgextend TheVolumeGroupName /dev/sda2
	EX: vgextend onevg /dev/sda2
	Type: vgreduce TheVolumeGroupName /dev/sda2 to remove it from the VG.
	EX: vgreduce onevg /dev/sda2

####Check for volume groups:
	Type: vgscan
	This command is run automatically when the system starts up.

####Split Volume Group:
	Type: vgsplit OriginalNamed_VG NewNamed_VG /dev/sda2
	EX: vgsplit onevg newvg /dev/sda2
	This command removes the physical volume named /dev/sda2 from the volume group onevg and adds it to a new volume group called newvg.

####Merge/Add a volume back to a Volume Group:
	Type: vgmerge -v VolumeGroupYouWantToKeep VolumeGroupYouWantToMerge
	This command merges VolumeGroupYouWantToMerge into VolumeGroupYouWantToKeep

####Rename a Volume Group:
	Type: vgrename OldVGName NewVGName
	EX: vgrename onevg newvg

####Create a logical volume inside of a Volume group:
	Type: lvcreate -L 500M -n TheNameOfLV TheNameOfVGTheLVWillBeCreatedIn
	EX: lvcreate -L 500M -n lvone onevg
	This command creates a physical volume named TheNameOfLV inside the volume group named TheNameOfVGTheLVWillBeCreatedIn

	Method 2 (example 1):
	Type: lvcreate -l 50%VG -n TheNameOfLV TheNameOfVGTheLVWillBeCreatedIn
	EX: lvcreate -l 50%VG -n lvtwo VGOne
	This command will use up 50% of the volume group to create a new logical volume named lvtwo

	Method 2 (example 2):
	Type: lvcreate -l 100%FREE -n TheNameOfLV TheNameOfVGTheLVWillBeCreatedIn
	EX: lvcreate -l 100%FREE -n lvthree onevg (This worked on Ubuntu)

	Remove the physical volume:
	Type: lvremove /dev/TheNameOfVG/TheNameOfPVlv
	EX: lvremove /dev/onevg/lvthree

	Method 3 (Create LV using Extents):
	Type: lvcreate -l 444 TheNameOfVG -n TheNameOfPV
	EX: lvcreate -l 444 onevg -n lvfour
	This command creates a physical volume of 444 extents named lvfour.

	Volume Groups are linear, meaning that if you have multiple PV's inside of your VG and you create an LV of any size, the first PV will be used by default then the second, third, etc.
	To change this behavior, you can create an LV on a PV that you specify.

	Type: lvcreate -L 500M -n NewNameOfLV TheNameOfVG /Name/of/PV
	EX: lvcreate -L 500M -n lvnew onevg /dev/sda9

	Method 4 (Create LV using Extents from two different PV's)
	Create a logical volume of 50 extents using 25 extents from two separate PV's:
	Type: lvcreate -l 50 -n lvone onevg /dev/sda6:0-25 /dev/sda7:0-25

	Method 5 (Create LV using non-contiguous Extents from one PV). Skipping using some Extents, skipping a few, and using the rest.
	Type: lvcreate -l 50 -n lvone onvg /dev/sda6:0-20:40-
	To remove two extents from the 50:
	Type: lvreduce -l -2 /dev/onevg/lvone

	This command creates the logical volume of 50 extents using the first 20 Extents then skipping to 40 and using everything after.

	Make the LV read only:
	Type: lvchange -pr /dev/onevg/lvone <--(The p means "permissions" and the r means "Read Only")
	Type: lvdisplay

	Grow an LV.
	Type: lvextend -L1g <--(Grow the logical volume by to 1G)
	Type: lvs to see the change.
	Type: lvextend -L+20M <--(grow the logical volume by 20 MB)
	Type: lvextend -l +100%FREE /dev/onevg/lvone <--(Use up all the free space)

####Adjust LVS (Logical Volume Show) output:
	lvs -v --segments  <--(will show linear, stripe, mirror, etc)

####Adjust the PVS (Physical Volume Show) output:
	pvs --separator =   <--(Use an = sign as the delimiter)
	pvs --separator = --aligned  <--(Make it neater looking)
	pvs -a  <--(Shows all devices so you can see what PV's are attached to VG's)
	pvs -o pv_name,pv_size,pv_free  <--(Shows the PV name, PV size, and PV free)
	pvs -o pv_name,pv_size,pv_free +O -pv_size  <--(sort by pv_size. Uppercase Letter +O)
	pvs -o pv_name,pv_size,pv_free -O -pv_size  <--(sort by pv_size. Uppercase Letter -O)
	pvs --units m  <--(Megabytes)
	pvs --units G  <--(Gigabytes)

####Adjust the VGS (Volume Groups Show) output:
    	vgs -o +pv_name  <--(Shows the PV and the VG)

####After I created the logical volume on Ubuntu I formatted them using ext4:
######I found the format path by typing "sudo lvdisplay" which showed me the LV path below:
    	sudo mkfs.ext4 /dev/vg_data/lv_data1
    	sudo mkfs.ext4 /dev/vg_data/lv_data2

####Show the filesystem type and other df information:
			df -Th

http://superuser.com/questions/116617/how-to-mount-an-lvm-volume
Find the logical volume that has your Fedora root filesystem (mine proved to be LogVol00):

    $ sudo lvs
    Create a mount point for that volume:
    
    $ sudo mkdir /mnt/fcroot
    Mount it:
    
    $ sudo mount /dev/VolGroup00/LogVol00 /mnt/fcroot -o ro,user
    You're done, navigate to /mnt/fcroot and copy the files and paste somewhere else.
    
    I changed the permissions on the new volume so that anyone in the sambashare group could read/write to it.
    	sudo chown -R root:sambashare /mnt/data1
    	sudo chmod o-rwx /mnt/data1 (remove access to anyone else).
    
    Make sure the group has access to the repository:
    	sudo chgrp -R sambashare /mnt/data1 (-R set the group ownership recursively).
    	sudo chmod g+rws /mnt/data1 (set the sticky bit so changes are owned by the group).
    	sudo chmod o-rwx /mnt/data1 (remove access for "other" so only group members can clone).


https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Administration/s1-LVMsetupnfs-HAAA.html

    Create the physical volume:
    	sudo pvcreate /dev/sdb1
    
    Create the volume group and add the physical volume to it:
    	sudo vgcreate my_vg /dev/sdb1
    
    Create 450MB logical volume in my_lv inside volume group my_vg:
    	sudo lvcreate -L450 -n my_lv my_vg
    
    Show the logical volumes:
    	sudo lvs
    
    Format the logical volume "my_lv" inside volume group "my_vg" with ext4 filesystem:
    	sudo mkfs.ext4 /dev/my_vg/my_lv
    
    
    I have extended the root filesystem from 15GB to 500GB using lvextend, however I cannot use the extra space because the file system is still formatted for 15GB. I have to use:
    resize2fs /dev/fedora/root to increase the size but the file system has to be unmounted for me to run resize2fs.

Ubuntu Link: https://help.ubuntu.com/community/UbuntuDesktopLVM

HTTP Links:
http://unix.stackexchange.com/questions/12040/what-mount-points-exist-on-a-typical-linux-system (Information)
https://help.1and1.com/servers-c37684/dedicated-server-linux-c37687/administration-c37694/increase-the-size-of-the-logical-volume-a756168.html (Guide)
http://www.computerhope.com/unix/umount.htm (Information)
https://www.ibm.com/support/knowledgecenter/SSNW54_1.1.1/com.ibm.kvm.v111.admin/resizingapartitionusingfdisk.htm (Guide)
https://www.youtube.com/watch?v=N22fweQjyQE (Logical Volume Manager - Deep Inside)
http://superuser.com/questions/116617/how-to-mount-an-lvm-volume

https://www.youtube.com/watch?v=SvOec_4QewE
https://www.youtube.com/watch?v=BysRGDgqtwY (Managing Storage with the Linux Logical Volume Manager (LVM))
http://www.microhowto.info/howto/increase_the_size_of_an_ext2_ext3_or_ext4_filesystem.html
