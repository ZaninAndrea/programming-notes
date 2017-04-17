# Chapter 3 
<!-- toc -->
## The boot process
skipping it for now

## Kernel
The kernel is loaded in the RAM and starts the most important processes as well as loads all the hardware components. Then the kernel runs the `/sbin/init` program. 
There are several alternatives for the `init` program: `SysVinit`, which is the traditionally used one, then came `upstart` and eventually `systemd`

We'll use `systemd` as it's the nowadays standard.
Some useful command line tasks:
* Starting, stopping, restarting a service (fooservice could be something like nfsd or the network) on a currently running system:

`$ sudo systemctl start/stop/restart fooservice`
* Enabling or disabling a system service from starting up at system boot:

`$ sudo systemctl enable/disable fooservice`

## Filesystem
A partition is a logical part of an hard disk.
A filesystem is a method of storing and finding files in a partition
A handy windows-linux comparison

| | Windows | Linux | 
|---|---|---|
| Partition | Disk1 | /dev/sda1 |
|Filesystem type | NTFS/VFAT |	EXT3/EXT4/XFS/BTRFS... |
|Mounting Parameters |	DriveLetter | MountPoint | 
| Base Folder where OS is stored | C:\ | / |

In linux all disks and partitions are mounted in the same filesystem: Removable media such as USB drives and CDs and DVDs will show up as mounted at `/run/media/yourusername/disklabel`

The files are organized in the same way in all distros:
![](https://d37djvu3ytnwxt.cloudfront.net/assets/courseware/v1/fff50dc5bde7ebaec7ef071b8bc0f7bf/asset-v1:LinuxFoundationX+LFS101x+1T2017+type@asset+block/chapter03_flowchart_scr05.jpg)

Partition are generally organized like this (you can customize those at installation-time):

 ![](https://d37djvu3ytnwxt.cloudfront.net/assets/courseware/v1/ae8955c30e5b10b2fd1cab2c79673555/asset-v1:LinuxFoundationX+LFS101x+1T2017+type@asset+block/LFS01_ch03_screen_34.jpg) 
## Choosing a distro
It's worth reading the [whole section](https://courses.edx.org/courses/course-v1:LinuxFoundationX+LFS101x+1T2017/courseware/6cee72d455c847e9b462efb4e2dbd2a7/0d5c853a5b0c4776881e6b27368237d6/)

