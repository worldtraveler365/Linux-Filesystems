# Linux-Filesystems
Creating Filesystems
Creating an LVM
n
p
Third section +1G
t
8e
p
w
lsblk

pvcreate /dev/sdb
pvs
pvdisplay

vgcreate vg /dev/sdb1
vgs
vgdisplay

lvcreate -n lv -L 800M vg
lvs
lvdisplay

mkfs -t ext4 /dev/mapper/vg-lv

mkdir /directory

vi /etc/fstab
/dev/mapper/vg-lv /directory ext4 defaults 0 0 

mount -a 
df -h
