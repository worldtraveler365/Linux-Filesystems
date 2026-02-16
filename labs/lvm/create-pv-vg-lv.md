**Disk Identification and Partitioning**

Before creating LVM structures, you must identify and partition the raw block devices.

**lsblk:** Lists information about all available or specified block devices (disks and partitions) in a tree-like format. It is the safest way to verify disk names.

**fdisk /dev/sdb:** Opens the fdisk utility to manage the partition table on the specific disk /dev/sdb.


**Partitioning Workflow (fdisk)**

Inside the fdisk interactive menu, use these keys in order to create an LVM-ready partition:

**n:** Create a new partition.

**p:** Set the partition type to primary.

**t:** Change the partition's system ID.

**8e:** The hexadecimal code for Linux LVM. This labels the partition so the OS knows it belongs to a Volume Group. In this example 8e will be the code I'll use.

**p:** Print the partition table to verify your changes before saving.

**w:** Write changes to disk and exit (this is the "point of no return").

**Physical Volume (PV) Layer**

The PV layer initializes the raw partition for LVM use.

**pvcreate /dev/sdb1:** Initializes /dev/sdb1 as a Physical Volume.

**pvs:** Provides a summary view of all Physical Volumes (concise).

**pvdisplay:** Provides a detailed report of PV attributes (UUID, size, and PE size).

**Volume Group (VG) Layer**

The VG acts as a storage pool, combining one or more PVs.

**vgcreate <vg_name> /dev/sdb1:** Creates a pool named <vg_name> using the specified PV.

**vgs:** Displays a summary of Volume Groups.

**vgdisplay:** Displays detailed information including free space and extent size.

**Logical Volume (LV) Layer**

**The LV is the "virtual partition" where your data actually lives.**

lvcreate -n <lv_name> -L <size> <vg_name>:

-n: Sets the Name of the logical volume.

-L: Sets the Logical size (absolute value).

Sizing (800M vs Company Needs): You place the size immediately after the -L flag. Use M for Megabytes, G for Gigabytes, or T for Terabytes. In a professional setting, you only allocate what is currently needed (e.g., 800M) because LVM allows you to grow the volume later as the company grows.

**lvs:** Displays a summary of Logical Volumes.

**lvdisplay:** Displays detailed status including the logical path.
