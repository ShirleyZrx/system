## pkg
### install pkg
apt-get update -y
apt-get install ${pkg}

### list pkg
dpkg -l
dpkg -l | grep ${key4pkg}

### pkg manage: aptitude
apt-get install aptitude

## system info
### cpu info
* detail
$ lscpu

* cpu simple info
$ cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c
    128  AMD EPYC 7742 64-Core Processor

### mem info
$ free -m
              total        used        free      shared  buff/cache   available
Mem:         515846        6205      503988          43        5651      507071
Swap:          8191           0        8191

### disk info
$ sudo fdisk -l | grep Disk
Disk /dev/loop0: 63.29 MiB, 66359296 bytes, 129608 sectors
Disk /dev/loop1: 49.86 MiB, 52260864 bytes, 102072 sectors
Disk /dev/loop2: 91.85 MiB, 96292864 bytes, 188072 sectors
Disk /dev/loop3: 63.97 MiB, 67051520 bytes, 130960 sectors
Disk /dev/loop4: 38.75 MiB, 40615936 bytes, 79328 sectors
Disk /dev/loop5: 63.97 MiB, 67051520 bytes, 130960 sectors
Disk /dev/loop6: 38.85 MiB, 40714240 bytes, 79520 sectors
Disk /dev/nvme0n1: 3.5 TiB, 3840755982336 bytes, 7501476528 sectors
Disk model: SAMSUNG MZQLB3T8HALS-00003
Disk /dev/sda: 893.14 GiB, 958999298048 bytes, 1873045504 sectors
Disk model: Logical Volume
Disklabel type: gpt
Disk identifier: CC9D6476-2D64-4623-85EC-569F5FDAD7B1

### list Disk type: type=disk
$ lsblk
NAME    MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0     7:0    0  63.3M  1 loop
loop1     7:1    0  49.9M  1 loop
loop2     7:2    0  91.9M  1 loop /snap/lxd/24061
loop3     7:3    0    64M  1 loop /snap/core20/2264
loop4     7:4    0  38.8M  1 loop /snap/snapd/21465
loop5     7:5    0    64M  1 loop /snap/core20/2318
loop6     7:6    0  38.8M  1 loop /snap/snapd/21759
sda       8:0    0 893.1G  0 disk
├─sda1    8:1    0     2G  0 part /boot/efi
├─sda2    8:2    0     2G  0 part /boot
├─sda3    8:3    0   100G  0 part /home
├─sda4    8:4    0   300G  0 part /var
└─sda5    8:5    0 489.1G  0 part /
nvme0n1 259:0    0   3.5T  0 disk /data

### disk category: 0 for SSD, 1 for SATA
$ cat /sys/block/nvme0n1/queue/rotational
0  # 0 for SSD，1 for SATA

$ cat /sys/block/sda/queue/rotational
0

### disk usage for each user
$ du -sh /home/*

