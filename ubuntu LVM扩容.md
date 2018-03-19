# ubuntu LVM扩容

## 增加一块物理硬盘并格式化
    例如增加/dev/sdb:
    ```
    splin@splin-VirtualBox:~$ sudo fdisk /dev/sdb 

    Welcome to fdisk (util-linux 2.27.1).
    Changes will remain in memory only, until you decide to write them.
    Be careful before using the write command.

    Device does not contain a recognized partition table.
    Created a new DOS disklabel with disk identifier 0xcb2462b1.

    Command (m for help): p
    Disk /dev/sdb: 40 GiB, 42949672960 bytes, 83886080 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disklabel type: dos
    Disk identifier: 0xcb2462b1

    Command (m for help): n
    Partition type
       p   primary (0 primary, 0 extended, 4 free)
       e   extended (container for logical partitions)
    Select (default p): 

    Using default response p.
    Partition number (1-4, default 1): 
    First sector (2048-83886079, default 2048): 
    Last sector, +sectors or +size{K,M,G,T,P} (2048-83886079, default 83886079): 

    Created a new partition 1 of type 'Linux' and of size 40 GiB.

    Command (m for help): m

    Help:

      DOS (MBR)
       a   toggle a bootable flag
       b   edit nested BSD disklabel
       c   toggle the dos compatibility flag

      Generic
       d   delete a partition
       F   list free unpartitioned space
       l   list known partition types
       n   add a new partition
       p   print the partition table
       t   change a partition type
       v   verify the partition table
       i   print information about a partition

      Misc
       m   print this menu
       u   change display/entry units
       x   extra functionality (experts only)

      Script
       I   load disk layout from sfdisk script file
       O   dump disk layout to sfdisk script file

      Save & Exit
       w   write table to disk and exit
       q   quit without saving changes

      Create a new label
       g   create a new empty GPT partition table
       G   create a new empty SGI (IRIX) partition table
       o   create a new empty DOS partition table
       s   create a new empty Sun partition table


    Command (m for help): a
    Selected partition 1
    The bootable flag on partition 1 is enabled now.

    Command (m for help): d
    Selected partition 1
    Partition 1 has been deleted.

    Command (m for help): d
    No partition is defined yet!
    Could not delete partition 1

    Command (m for help): p

    Disk /dev/sdb: 40 GiB, 42949672960 bytes, 83886080 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disklabel type: dos
    Disk identifier: 0xcb2462b1

    Command (m for help): n
    Partition type
       p   primary (0 primary, 0 extended, 4 free)
       e   extended (container for logical partitions)
    Select (default p): 

    Using default response p.
    Partition number (1-4, default 1): 
    First sector (2048-83886079, default 2048): 
    Last sector, +sectors or +size{K,M,G,T,P} (2048-83886079, default 83886079): 

    Created a new partition 1 of type 'Linux' and of size 40 GiB.

    Command (m for help): p
    Disk /dev/sdb: 40 GiB, 42949672960 bytes, 83886080 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disklabel type: dos
    Disk identifier: 0xcb2462b1

    Device     Boot Start      End  Sectors Size Id Type
    /dev/sdb1        2048 83886079 83884032  40G 83 Linux

    Command (m for help): l

     0  Empty           24  NEC DOS         81  Minix / old Lin bf  Solaris        
     1  FAT12           27  Hidden NTFS Win 82  Linux swap / So c1  DRDOS/sec (FAT-
     2  XENIX root      39  Plan 9          83  Linux           c4  DRDOS/sec (FAT-
     3  XENIX usr       3c  PartitionMagic  84  OS/2 hidden or  c6  DRDOS/sec (FAT-
     4  FAT16 <32M      40  Venix 80286     85  Linux extended  c7  Syrinx         
     5  Extended        41  PPC PReP Boot   86  NTFS volume set da  Non-FS data    
     6  FAT16           42  SFS             87  NTFS volume set db  CP/M / CTOS / .
     7  HPFS/NTFS/exFAT 4d  QNX4.x          88  Linux plaintext de  Dell Utility   
     8  AIX             4e  QNX4.x 2nd part 8e  Linux LVM       df  BootIt         
     9  AIX bootable    4f  QNX4.x 3rd part 93  Amoeba          e1  DOS access     
     a  OS/2 Boot Manag 50  OnTrack DM      94  Amoeba BBT      e3  DOS R/O        
     b  W95 FAT32       51  OnTrack DM6 Aux 9f  BSD/OS          e4  SpeedStor      
     c  W95 FAT32 (LBA) 52  CP/M            a0  IBM Thinkpad hi ea  Rufus alignment
     e  W95 FAT16 (LBA) 53  OnTrack DM6 Aux a5  FreeBSD         eb  BeOS fs        
     f  W95 Ext'd (LBA) 54  OnTrackDM6      a6  OpenBSD         ee  GPT            
    10  OPUS            55  EZ-Drive        a7  NeXTSTEP        ef  EFI (FAT-12/16/
    11  Hidden FAT12    56  Golden Bow      a8  Darwin UFS      f0  Linux/PA-RISC b
    12  Compaq diagnost 5c  Priam Edisk     a9  NetBSD          f1  SpeedStor      
    14  Hidden FAT16 <3 61  SpeedStor       ab  Darwin boot     f4  SpeedStor      
    16  Hidden FAT16    63  GNU HURD or Sys af  HFS / HFS+      f2  DOS secondary  
    17  Hidden HPFS/NTF 64  Novell Netware  b7  BSDI fs         fb  VMware VMFS    
    18  AST SmartSleep  65  Novell Netware  b8  BSDI swap       fc  VMware VMKCORE 
    1b  Hidden W95 FAT3 70  DiskSecure Mult bb  Boot Wizard hid fd  Linux raid auto
    1c  Hidden W95 FAT3 75  PC/IX           bc  Acronis FAT32 L fe  LANstep        
    1e  Hidden W95 FAT1 80  Old Minix       be  Solaris boot    ff  BBT            

    Command (m for help): t
    Selected partition 1
    Partition type (type L to list all types): 8e
    Changed type of partition 'Linux' to 'Linux LVM'.

    Command (m for help): w
    The partition table has been altered.
    Calling ioctl() to re-read partition table.
    Syncing disks.
    ```
    
    splin@splin-VirtualBox:~$ sudo partprobe 
    splin@splin-VirtualBox:~$ sudo pvcreate /dev/sdb1
    Physical volume "/dev/sdb1" successfully created
    
    splin@splin-VirtualBox:~$ sudo pvscan 
      PV /dev/sda5   VG ubuntu-vg       lvm2 [9.52 GiB / 24.00 MiB free]
      PV /dev/sdb1                      lvm2 [40.00 GiB]
      Total: 2 [49.52 GiB] / in use: 1 [9.52 GiB] / in no VG: 1 [40.00 GiB]
     
    splin@splin-VirtualBox:~$ sudo vgdisplay 
      --- Volume group ---
      VG Name               ubuntu-vg
      System ID             
      Format                lvm2
      Metadata Areas        1
      Metadata Sequence No  3
      VG Access             read/write
      VG Status             resizable
      MAX LV                0
      Cur LV                2
      Open LV               2
      Max PV                0
      Cur PV                1
      Act PV                1
      VG Size               9.52 GiB
      PE Size               4.00 MiB
      Total PE              2437
      Alloc PE / Size       2431 / 9.50 GiB
      Free  PE / Size       6 / 24.00 MiB
      VG UUID               Q1uaBl-8Gec-8n6C-6vYE-0M9H-BzY4-o1txTl
       
    splin@splin-VirtualBox:~$ sudo vgextend ubuntu-vg /dev/sdb1
      Volume group "ubuntu-vg" successfully extended
      
    splin@splin-VirtualBox:~$ sudo pvscan 
      PV /dev/sda5   VG ubuntu-vg       lvm2 [9.52 GiB / 24.00 MiB free]
      PV /dev/sdb1   VG ubuntu-vg       lvm2 [40.00 GiB / 40.00 GiB free]
      Total: 2 [49.52 GiB] / in use: 2 [49.52 GiB] / in no VG: 0 [0   ]
      
    splin@splin-VirtualBox:~$ 
    splin@splin-VirtualBox:~$ 
    splin@splin-VirtualBox:~$ sudo lvdisplay 
      --- Logical volume ---
      LV Path                /dev/ubuntu-vg/root
      LV Name                root
      VG Name                ubuntu-vg
      LV UUID                7lmbxH-Vp3U-Xaya-9F2B-sdKE-dBRx-jEV5xd
      LV Write Access        read/write
      LV Creation host, time ubuntu, 2018-03-13 15:50:48 +0800
      LV Status              available
      # open                 1
      LV Size                5.50 GiB
      Current LE             1408
      Segments               1
      Allocation             inherit
      Read ahead sectors     auto
      - currently set to     256
      Block device           253:0
       
      --- Logical volume ---
      LV Path                /dev/ubuntu-vg/swap_1
      LV Name                swap_1
      VG Name                ubuntu-vg
      LV UUID                tHhK3I-J64u-V3vz-x5lG-7qto-nkSn-oWQgxh
      LV Write Access        read/write
      LV Creation host, time ubuntu, 2018-03-13 15:50:49 +0800
      LV Status              available
      # open                 2
      LV Size                4.00 GiB
      Current LE             1023
      Segments               1
      Allocation             inherit
      Read ahead sectors     auto
      - currently set to     256
      Block device           253:1
       
    splin@splin-VirtualBox:~$ sudo lvextend -L +40G /dev/ubuntu-vg/root
      Size of logical volume ubuntu-vg/root changed from 5.50 GiB (1408 extents) to 45.50 GiB (11648 extents).
      Logical volume root successfully resized.
      
    splin@splin-VirtualBox:~$ sudo resize2fs /dev/ubuntu-vg/root 
    resize2fs 1.42.13 (17-May-2015)
    Filesystem at /dev/ubuntu-vg/root is mounted on /; on-line resizing required
    old_desc_blocks = 1, new_desc_blocks = 3
    The filesystem on /dev/ubuntu-vg/root is now 11927552 (4k) blocks long.

    splin@splin-VirtualBox:~$ df -l
    Filesystem                  1K-blocks    Used Available Use% Mounted on
    udev                          1992940       0   1992940   0% /dev
    tmpfs                          403984    6200    397784   2% /run
    /dev/mapper/ubuntu--vg-root  46830544 4949020  39899108  12% /
    tmpfs                         2019900     216   2019684   1% /dev/shm
    tmpfs                            5120       4      5116   1% /run/lock
    tmpfs                         2019900       0   2019900   0% /sys/fs/cgroup
    /dev/sda1                      482922  127333    330655  28% /boot
    tmpfs                          403984      44    403940   1% /run/user/1000


    