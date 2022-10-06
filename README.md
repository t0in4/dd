# dd

26


I would do it like this (assuming that sdb is your stick):

Delete any previous partition table:

# dd if=/dev/zero of=/dev/sdb bs=512 count=1
Create the new ones:

# fdisk /dev/sdb
> n
> p
> 1
(+1GB)
> a
> 1
(toggles boot flag)
> t
> c
(filesystem type)
> n
> p
> 2
(defaults)
> t
(specify 2nd partition)
> c
(filesystem type)
> p
(prints current configuration)
> w
(write the new table and quit)

Create the filesystems:

# mkfs.vfat /dev/sdb1
# mkfs.vfat /dev/sdb2
