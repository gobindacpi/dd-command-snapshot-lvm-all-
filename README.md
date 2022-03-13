# dd-command-snapshot-lvm-all-
~~~

Copy raw format os using dd command
we have created first lvm-os volume from vps-volume. Then copy raw image to lvm-os by dd command.
dd if=debian-10-buster.raw of=/dev/vps-volume/lvm-os bs=4M

create snapshot from lvm-os .
lvcreate -L 2GB -s -n lvm-os-snap1 /dev/vps-volume/lvm-os
lvcreate -L 5GB -s -n lvm-os-snap2 /dev/vps-volume/lvm-os
lvcreate -L 6GB -s -n lvm-os-snap3 /dev/vps-volume/lvm-os
lvcreate -L 7GB -s -n lvm-os-snap4 /dev/vps-volume/lvm-os


How to launch new vm from Snapshot?
ok first create new volume from vps-volume with same size of original vm.

lvcreate -L 50G -n data-restore-from-snap4 vps-volume

Now copy lvm-os-snap4 to data-restore-from-snap4
dd if=/dev/vps-volume/lvm-os-snap4 of=/dev/vps-volume/data-restore-from-snap4

and import from virt manager & and assign CPU and RAM .


LVM size extend command, Here we have extend 40GB with origina size.
lvextend -L +40G /dev/vps-volume/VM-Database-snap4


~~~
