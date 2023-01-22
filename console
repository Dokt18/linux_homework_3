[vagrant@Ubuntu ~]$ sudo pvcreate /dev/sdb
  Physical volume "/dev/sdb" successfully created.
[vagrant@Ubuntu ~]$ sudo vgcreate vg_root /dev/sdb
  Volume group "vg_root" successfully created
[vagrant@Ubuntu ~]$ sudo lvcreate -n lv_root -l +100%FREE /dev/vg_root
WARNING: ext4 signature detected on /dev/vg_root/lv_root at offset 1080. Wipe it? [y/n]: y
  Wiping ext4 signature on /dev/vg_root/lv_root.
  Logical volume "lv_root" created.
[vagrant@Ubuntu ~]$ sudo mkfs.xfs /dev/vg_root/lv_root
meta-data=/dev/vg_root/lv_root   isize=512    agcount=4, agsize=655104 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=0, sparse=0
data     =                       bsize=4096   blocks=2620416, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
log      =internal log           bsize=4096   blocks=2560, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
[vagrant@Ubuntu ~]$ mount /dev/vg_root/lv_root /mnt
mount: only root can do that
[vagrant@Ubuntu ~]$ sudo mount /dev/vg_root/lv_root /mnt
[vagrant@Ubuntu ~]$ sudo xfsdump -J - /dev/VolGroup00/LogVol00 | xfsrestore -J - /mnt
xfsrestore: using file dump (drive_simple) strategy
xfsrestore: version 3.1.7 (dump format 3.0)
xfsrestore: ERROR: unable to create /mnt/xfsrestorehousekeepingdir: Permission denied
xfsrestore: Restore Status: ERROR
xfsdump: using file dump (drive_simple) strategy
xfsdump: version 3.1.7 (dump format 3.0)
xfsdump: level 0 dump of Ubuntu:/
xfsdump: dump date: Sat Jan 21 21:06:50 2023
xfsdump: session id: 51590028-4d06-4079-8a82-2014613c0d87
xfsdump: session label: ""
xfsdump: ino map phase 1: constructing initial dump list
xfsdump: ino map phase 2: skipping (no pruning necessary)
xfsdump: ino map phase 3: skipping (only one dump stream)
xfsdump: ino map construction complete
xfsdump: estimated dump size: 840563584 bytes
xfsdump: creating dump session media file 0 (media 0, file 0)
xfsdump: dumping ino map
xfsdump: dumping directories
xfsdump: WARNING: write to stdio failed: 32 (Broken pipe)
xfsdump: ending media file
xfsdump: media file size 0 bytes
xfsdump: dump size (non-dir files) : 0 bytes
xfsdump: NOTE: dump interrupted: 0 seconds elapsed
xfsdump: Dump Status: INTERRUPT
[vagrant@Ubuntu ~]$ sudo bash -c 'xfsdump -J - /dev/VolGroup00/LogVol00 | xfsrestore -J - /mnt'
xfsrestore: using file dump (drive_simple) strategy
xfsrestore: version 3.1.7 (dump format 3.0)
xfsdump: using file dump (drive_simple) strategy
xfsdump: version 3.1.7 (dump format 3.0)
xfsdump: level 0 dump of Ubuntu:/
xfsdump: dump date: Sat Jan 21 21:08:03 2023
xfsdump: session id: 7580d503-a82b-4860-883d-d451530993c7
xfsdump: session label: ""
xfsrestore: searching media for dump
xfsdump: ino map phase 1: constructing initial dump list
xfsdump: ino map phase 2: skipping (no pruning necessary)
xfsdump: ino map phase 3: skipping (only one dump stream)
xfsdump: ino map construction complete
xfsdump: estimated dump size: 840563584 bytes
xfsdump: creating dump session media file 0 (media 0, file 0)
xfsdump: dumping ino map
xfsdump: dumping directories
xfsrestore: examining media file 0
xfsrestore: dump description: 
xfsrestore: hostname: Ubuntu
xfsrestore: mount point: /
xfsrestore: volume: /dev/mapper/VolGroup00-LogVol00
xfsrestore: session time: Sat Jan 21 21:08:03 2023
xfsrestore: level: 0
xfsrestore: session label: ""
xfsrestore: media label: ""
xfsrestore: file system id: b60e9498-0baa-4d9f-90aa-069048217fee
xfsrestore: session id: 7580d503-a82b-4860-883d-d451530993c7
xfsrestore: media id: 0e3aeba2-0f89-40a3-92c0-76d63dd93adf
xfsrestore: searching media for directory dump
xfsrestore: reading directories
xfsdump: dumping non-directory files
xfsrestore: 2694 directories and 23469 entries processed
xfsrestore: directory post-processing
xfsrestore: restoring non-directory files
xfsdump: ending media file
xfsdump: media file size 817818872 bytes
xfsdump: dump size (non-dir files) : 804720912 bytes
xfsdump: dump complete: 22 seconds elapsed
xfsdump: Dump Status: SUCCESS
xfsrestore: restore complete: 22 seconds elapsed
xfsrestore: Restore Status: SUCCESS
[vagrant@Ubuntu ~]$ ls /mnt
bin  boot  data  data-snap  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[vagrant@Ubuntu ~]$ for i in /proc/ /sys/ /dev/ /run/ /boot/;do mount --bind $i /mnt/$i;done
mount: only root can use "--bind" option
mount: only root can use "--bind" option
mount: only root can use "--bind" option
mount: only root can use "--bind" option
mount: only root can use "--bind" option
[vagrant@Ubuntu ~]$ sudo for i in /proc/ /sys/ /dev/ /run/ /boot/;do mount --bind $i /mnt/$i;done
-bash: syntax error near unexpected token `do'
[vagrant@Ubuntu ~]$ sudo bash -c 'for i in /proc/ /sys/ /dev/ /run/ /boot/;do mount --bind $i /mnt/$i;done'
[vagrant@Ubuntu ~]$ sudo chroot /mnt/
[root@Ubuntu /]# sudo grub2-mkconfig -o /boot/grub2/grub.cfg
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-3.10.0-862.2.3.el7.x86_64
Found initrd image: /boot/initramfs-3.10.0-862.2.3.el7.x86_64.img
done
[root@Ubuntu /]# cd /boot ; for i in `ls initramfs-*img`; do dracut -v $i `echo $i|sed "s/initramfs-//g;
> s/.img//g"` --force; done
Executing: /sbin/dracut -v initramfs-3.10.0-862.2.3.el7.x86_64.img 3.10.0-862.2.3.el7.x86_64 --force
dracut module 'busybox' will not be installed, because command 'busybox' could not be found!
dracut module 'crypt' will not be installed, because command 'cryptsetup' could not be found!
dracut module 'dmraid' will not be installed, because command 'dmraid' could not be found!
dracut module 'dmsquash-live-ntfs' will not be installed, because command 'ntfs-3g' could not be found!
dracut module 'mdraid' will not be installed, because command 'mdadm' could not be found!
dracut module 'multipath' will not be installed, because command 'multipath' could not be found!
dracut module 'busybox' will not be installed, because command 'busybox' could not be found!
dracut module 'crypt' will not be installed, because command 'cryptsetup' could not be found!
dracut module 'dmraid' will not be installed, because command 'dmraid' could not be found!
dracut module 'dmsquash-live-ntfs' will not be installed, because command 'ntfs-3g' could not be found!
dracut module 'mdraid' will not be installed, because command 'mdadm' could not be found!
dracut module 'multipath' will not be installed, because command 'multipath' could not be found!
*** Including module: bash ***
*** Including module: nss-softokn ***
*** Including module: i18n ***
*** Including module: drm ***
*** Including module: plymouth ***
*** Including module: dm ***
Skipping udev rule: 64-device-mapper.rules
Skipping udev rule: 60-persistent-storage-dm.rules
Skipping udev rule: 55-dm.rules
*** Including module: kernel-modules ***
Omitting driver floppy
*** Including module: lvm ***
Skipping udev rule: 64-device-mapper.rules
Skipping udev rule: 56-lvm.rules
Skipping udev rule: 60-persistent-storage-lvm.rules
*** Including module: qemu ***
*** Including module: resume ***
*** Including module: rootfs-block ***
*** Including module: terminfo ***
*** Including module: udev-rules ***
Skipping udev rule: 40-redhat-cpu-hotplug.rules
Skipping udev rule: 91-permissions.rules
*** Including module: biosdevname ***
*** Including module: systemd ***
*** Including module: usrmount ***
*** Including module: base ***
*** Including module: fs-lib ***
*** Including module: shutdown ***
*** Including modules done ***
*** Installing kernel module dependencies and firmware ***
*** Installing kernel module dependencies and firmware done ***
*** Resolving executable dependencies ***
*** Resolving executable dependencies done***
*** Hardlinking files ***
*** Hardlinking files done ***
*** Stripping files ***
*** Stripping files done ***
*** Generating early-microcode cpio image contents ***
*** No early-microcode cpio image needed ***
*** Store current command line parameters ***
*** Creating image file ***
*** Creating image file done ***
*** Creating initramfs image file '/boot/initramfs-3.10.0-862.2.3.el7.x86_64.img' done ***
[root@Ubuntu boot]# sudo vi /boot/grub2/grub.cfg
<pre>[vagrant@Ubuntu ~]$ sudo lvremove /dev/VolGroup00/LogVol00
Do you really want to remove active logical volume VolGroup00/LogVol00? [y/n]: y
  Logical volume &quot;LogVol00&quot; successfully removed
[vagrant@Ubuntu ~]$ sudo lvcreate -n VolGroup00/LogVol00 -L 8G /dev/VolGroup00
WARNING: xfs signature detected on /dev/VolGroup00/LogVol00 at offset 0. Wipe it? [y/n]: y
  Wiping xfs signature on /dev/VolGroup00/LogVol00.
  Logical volume &quot;LogVol00&quot; created.
[vagrant@Ubuntu ~]$ sudo mkfs.xfs /dev/VolGroup00/LogVol00
meta-data=/dev/VolGroup00/LogVol00 isize=512    agcount=4, agsize=524288 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=0, sparse=0
data     =                       bsize=4096   blocks=2097152, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
log      =internal log           bsize=4096   blocks=2560, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
[vagrant@Ubuntu ~]$ mount /dev/VolGroup00/LogVol00 /mnt
mount: only root can do that
[vagrant@Ubuntu ~]$ sudo mount /dev/VolGroup00/LogVol00 /mnt
[vagrant@Ubuntu ~]$ sudo bash -c &apos;xfsdump -J - /dev/vg_root/lv_root | xfsrestore -J - /mnt&apos;
xfsrestore: using file dump (drive_simple) strategy
xfsrestore: version 3.1.7 (dump format 3.0)
xfsdump: using file dump (drive_simple) strategy
xfsdump: version 3.1.7 (dump format 3.0)
xfsrestore: searching media for dump
xfsdump: level 0 dump of Ubuntu:/
xfsdump: dump date: Sat Jan 21 21:23:40 2023
xfsdump: session id: bc6e4a50-8dc8-4427-811e-1951bfe9e376
xfsdump: session label: &quot;&quot;
xfsdump: ino map phase 1: constructing initial dump list
xfsdump: ino map phase 2: skipping (no pruning necessary)
xfsdump: ino map phase 3: skipping (only one dump stream)
xfsdump: ino map construction complete
xfsdump: estimated dump size: 841352256 bytes
xfsdump: creating dump session media file 0 (media 0, file 0)
xfsdump: dumping ino map
xfsdump: dumping directories
xfsrestore: examining media file 0
xfsrestore: dump description: 
xfsrestore: hostname: Ubuntu
xfsrestore: mount point: /
xfsrestore: volume: /dev/mapper/vg_root-lv_root
xfsrestore: session time: Sat Jan 21 21:23:40 2023
xfsrestore: level: 0
xfsrestore: session label: &quot;&quot;
xfsrestore: media label: &quot;&quot;
xfsrestore: file system id: 2708d810-0d17-4d32-a59d-b7e81c190892
xfsrestore: session id: bc6e4a50-8dc8-4427-811e-1951bfe9e376
xfsrestore: media id: 3ba2d042-5aa6-4a4b-adc7-30b4e3bb0728
xfsrestore: searching media for directory dump
xfsrestore: reading directories
xfsdump: dumping non-directory files
xfsrestore: 2698 directories and 23476 entries processed
xfsrestore: directory post-processing
xfsrestore: restoring non-directory files
xfsdump: ending media file
xfsdump: media file size 818102928 bytes
xfsdump: dump size (non-dir files) : 804999960 bytes
xfsdump: dump complete: 29 seconds elapsed
xfsdump: Dump Status: SUCCESS
xfsrestore: restore complete: 29 seconds elapsed
xfsrestore: Restore Status: SUCCESS
[vagrant@Ubuntu ~]$ sudo bash -c &apos;for i in /proc/ /sys/ /dev/ /run/ /boot/; do mount --bind $i /mnt/$i; done&apos;
[vagrant@Ubuntu ~]$ sudo chroot /mnt/
[root@Ubuntu /]# sudo grub2-mkconfig -o /boot/grub2/grub.cfg
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-3.10.0-862.2.3.el7.x86_64
Found initrd image: /boot/initramfs-3.10.0-862.2.3.el7.x86_64.img
done
[root@Ubuntu /]# sudo bash -c &apos;cd /boot ; for i in `ls initramfs-*img`; do dracut -v $i `echo $i|sed &quot;s/initramfs-//g;
&gt; s/.img//g&quot;` --force; done&apos;
Executing: /sbin/dracut -v initramfs-3.10.0-862.2.3.el7.x86_64.img 3.10.0-862.2.3.el7.x86_64 --force
dracut module &apos;busybox&apos; will not be installed, because command &apos;busybox&apos; could not be found!
dracut module &apos;crypt&apos; will not be installed, because command &apos;cryptsetup&apos; could not be found!
dracut module &apos;dmraid&apos; will not be installed, because command &apos;dmraid&apos; could not be found!
dracut module &apos;dmsquash-live-ntfs&apos; will not be installed, because command &apos;ntfs-3g&apos; could not be found!
dracut module &apos;mdraid&apos; will not be installed, because command &apos;mdadm&apos; could not be found!
dracut module &apos;multipath&apos; will not be installed, because command &apos;multipath&apos; could not be found!
dracut module &apos;busybox&apos; will not be installed, because command &apos;busybox&apos; could not be found!
dracut module &apos;crypt&apos; will not be installed, because command &apos;cryptsetup&apos; could not be found!
dracut module &apos;dmraid&apos; will not be installed, because command &apos;dmraid&apos; could not be found!
dracut module &apos;dmsquash-live-ntfs&apos; will not be installed, because command &apos;ntfs-3g&apos; could not be found!
dracut module &apos;mdraid&apos; will not be installed, because command &apos;mdadm&apos; could not be found!
dracut module &apos;multipath&apos; will not be installed, because command &apos;multipath&apos; could not be found!
*** Including module: bash ***
*** Including module: nss-softokn ***
*** Including module: i18n ***
*** Including module: drm ***
*** Including module: plymouth ***
*** Including module: dm ***
Skipping udev rule: 64-device-mapper.rules
Skipping udev rule: 60-persistent-storage-dm.rules
Skipping udev rule: 55-dm.rules
*** Including module: kernel-modules ***
Omitting driver floppy
*** Including module: lvm ***
Skipping udev rule: 64-device-mapper.rules
Skipping udev rule: 56-lvm.rules
Skipping udev rule: 60-persistent-storage-lvm.rules
*** Including module: qemu ***
*** Including module: resume ***
*** Including module: rootfs-block ***
*** Including module: terminfo ***
*** Including module: udev-rules ***
Skipping udev rule: 40-redhat-cpu-hotplug.rules
Skipping udev rule: 91-permissions.rules
*** Including module: biosdevname ***
*** Including module: systemd ***
*** Including module: usrmount ***
*** Including module: base ***
*** Including module: fs-lib ***
*** Including module: shutdown ***
*** Including modules done ***
*** Installing kernel module dependencies and firmware ***
*** Installing kernel module dependencies and firmware done ***
*** Resolving executable dependencies ***
*** Resolving executable dependencies done***
*** Hardlinking files ***
*** Hardlinking files done ***
*** Stripping files ***
*** Stripping files done ***
*** Generating early-microcode cpio image contents ***
*** No early-microcode cpio image needed ***
*** Store current command line parameters ***
*** Creating image file ***
*** Creating image file done ***
*** Creating initramfs image file &apos;/boot/initramfs-3.10.0-862.2.3.el7.x86_64.img&apos; done ***
[vagrant@Ubuntu ~]$ sudo lvremove /dev/VolGroup00/LogVol00
Do you really want to remove active logical volume VolGroup00/LogVol00? [y/n]: y
  Logical volume "LogVol00" successfully removed
[vagrant@Ubuntu ~]$ sudo lvcreate -n VolGroup00/LogVol00 -L 8G /dev/VolGroup00
WARNING: xfs signature detected on /dev/VolGroup00/LogVol00 at offset 0. Wipe it? [y/n]: y
  Wiping xfs signature on /dev/VolGroup00/LogVol00.
  Logical volume "LogVol00" created.
[vagrant@Ubuntu ~]$ sudo mkfs.xfs /dev/VolGroup00/LogVol00
meta-data=/dev/VolGroup00/LogVol00 isize=512    agcount=4, agsize=524288 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=0, sparse=0
data     =                       bsize=4096   blocks=2097152, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
log      =internal log           bsize=4096   blocks=2560, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
[vagrant@Ubuntu ~]$ sudo mount /dev/VolGroup00/LogVol00 /mnt
[vagrant@Ubuntu ~]$ sudo bash -c 'xfsdump -J - /dev/vg_root/lv_root | xfsrestore -J - /mnt'
xfsrestore: using file dump (drive_simple) strategy
xfsrestore: version 3.1.7 (dump format 3.0)
xfsdump: using file dump (drive_simple) strategy
xfsdump: version 3.1.7 (dump format 3.0)
xfsrestore: searching media for dump
xfsdump: level 0 dump of Ubuntu:/
xfsdump: dump date: Sat Jan 21 21:23:40 2023
xfsdump: session id: bc6e4a50-8dc8-4427-811e-1951bfe9e376
xfsdump: session label: ""
xfsdump: ino map phase 1: constructing initial dump list
xfsdump: ino map phase 2: skipping (no pruning necessary)
xfsdump: ino map phase 3: skipping (only one dump stream)
xfsdump: ino map construction complete
xfsdump: estimated dump size: 841352256 bytes
xfsdump: creating dump session media file 0 (media 0, file 0)
xfsdump: dumping ino map
xfsdump: dumping directories
xfsrestore: examining media file 0
xfsrestore: dump description: 
xfsrestore: hostname: Ubuntu
xfsrestore: mount point: /
xfsrestore: volume: /dev/mapper/vg_root-lv_root
xfsrestore: session time: Sat Jan 21 21:23:40 2023
xfsrestore: level: 0
xfsrestore: session label: ""
xfsrestore: media label: ""
xfsrestore: file system id: 2708d810-0d17-4d32-a59d-b7e81c190892
xfsrestore: session id: bc6e4a50-8dc8-4427-811e-1951bfe9e376
xfsrestore: media id: 3ba2d042-5aa6-4a4b-adc7-30b4e3bb0728
xfsrestore: searching media for directory dump
xfsrestore: reading directories
xfsdump: dumping non-directory files
xfsrestore: 2698 directories and 23476 entries processed
xfsrestore: directory post-processing
xfsrestore: restoring non-directory files
xfsdump: ending media file
xfsdump: media file size 818102928 bytes
xfsdump: dump size (non-dir files) : 804999960 bytes
xfsdump: dump complete: 29 seconds elapsed
xfsdump: Dump Status: SUCCESS
xfsrestore: restore complete: 29 seconds elapsed
xfsrestore: Restore Status: SUCCESS
[vagrant@Ubuntu ~]$ sudo bash -c 'for i in /proc/ /sys/ /dev/ /run/ /boot/; do mount --bind $i /mnt/$i; done'
[vagrant@Ubuntu ~]$ sudo chroot /mnt/
[root@Ubuntu /]# sudo grub2-mkconfig -o /boot/grub2/grub.cfg
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-3.10.0-862.2.3.el7.x86_64
Found initrd image: /boot/initramfs-3.10.0-862.2.3.el7.x86_64.img
done
[root@Ubuntu /]# sudo bash -c 'cd /boot ; for i in `ls initramfs-*img`; do dracut -v $i `echo $i|sed "s/initramfs-//g;
> s/.img//g"` --force; done'
Executing: /sbin/dracut -v initramfs-3.10.0-862.2.3.el7.x86_64.img 3.10.0-862.2.3.el7.x86_64 --force
dracut module 'busybox' will not be installed, because command 'busybox' could not be found!
dracut module 'crypt' will not be installed, because command 'cryptsetup' could not be found!
dracut module 'dmraid' will not be installed, because command 'dmraid' could not be found!
dracut module 'dmsquash-live-ntfs' will not be installed, because command 'ntfs-3g' could not be found!
dracut module 'mdraid' will not be installed, because command 'mdadm' could not be found!
dracut module 'multipath' will not be installed, because command 'multipath' could not be found!
dracut module 'busybox' will not be installed, because command 'busybox' could not be found!
dracut module 'crypt' will not be installed, because command 'cryptsetup' could not be found!
dracut module 'dmraid' will not be installed, because command 'dmraid' could not be found!
dracut module 'dmsquash-live-ntfs' will not be installed, because command 'ntfs-3g' could not be found!
dracut module 'mdraid' will not be installed, because command 'mdadm' could not be found!
dracut module 'multipath' will not be installed, because command 'multipath' could not be found!
*** Including module: bash ***
*** Including module: nss-softokn ***
*** Including module: i18n ***
*** Including module: drm ***
*** Including module: plymouth ***
*** Including module: dm ***
Skipping udev rule: 64-device-mapper.rules
Skipping udev rule: 60-persistent-storage-dm.rules
Skipping udev rule: 55-dm.rules
*** Including module: kernel-modules ***
Omitting driver floppy
*** Including module: lvm ***
Skipping udev rule: 64-device-mapper.rules
Skipping udev rule: 56-lvm.rules
Skipping udev rule: 60-persistent-storage-lvm.rules
*** Including module: qemu ***
*** Including module: resume ***
*** Including module: rootfs-block ***
*** Including module: terminfo ***
*** Including module: udev-rules ***
Skipping udev rule: 40-redhat-cpu-hotplug.rules
Skipping udev rule: 91-permissions.rules
*** Including module: biosdevname ***
*** Including module: systemd ***
*** Including module: usrmount ***
*** Including module: base ***
*** Including module: fs-lib ***
*** Including module: shutdown ***
*** Including modules done ***
*** Installing kernel module dependencies and firmware ***
*** Installing kernel module dependencies and firmware done ***
*** Resolving executable dependencies ***
*** Resolving executable dependencies done***
*** Hardlinking files ***
*** Hardlinking files done ***
*** Stripping files ***
*** Stripping files done ***
*** Generating early-microcode cpio image contents ***
*** No early-microcode cpio image needed ***
*** Store current command line parameters ***
*** Creating image file ***
*** Creating image file done ***
*** Creating initramfs image file '/boot/initramfs-3.10.0-862.2.3.el7.x86_64.img' done ***
[root@Ubuntu /]# sudo pvcreate /dev/sdc /dev/sdd
  Physical volume "/dev/sdc" successfully created.
  Physical volume "/dev/sdd" successfully created.
[root@Ubuntu /]# sudo vgcreate vg_var /dev/sdc /dev/sdd
  Volume group "vg_var" successfully created
[root@Ubuntu /]# sudo lvcreate -L 950M -m1 -n lv_var vg_var
  Rounding up size to full physical extent 952.00 MiB
  Logical volume "lv_var" created.
[root@Ubuntu /]# sudo mkfs.ext4 /dev/vg_var/lv_var
mke2fs 1.42.9 (28-Dec-2013)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
60928 inodes, 243712 blocks
12185 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=249561088
8 block groups
32768 blocks per group, 32768 fragments per group
7616 inodes per group
Superblock backups stored on blocks: 
	32768, 98304, 163840, 229376

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done

[root@Ubuntu /]# sudo mount /dev/vg_var/lv_var /mnt
[root@Ubuntu /]# sudo cp -aR /var/* /mnt/
[root@Ubuntu /]# sudo mkdir /tmp/oldvar && mv /var/* /tmp/oldvar
[root@Ubuntu /]# sudo umount /mnt
[root@Ubuntu /]# sudo mount /dev/vg_var/lv_var /var
[root@Ubuntu /]# echo "`blkid | grep var: | awk '{print $2}'` /var ext4 defaults 0 0" >> /etc/fstab
sudo lvremove /dev/vg_root/lv_root
Do you really want to remove active logical volume vg_root/lv_root? [y/n]: y
  Logical volume "lv_root" successfully removed
[vagrant@ubuntu ~]$ sudo vgremove /dev/vg_root
  Volume group "vg_root" successfully removed
[vagrant@ubuntu ~]$ sudo vgs
  VG         #PV #LV #SN Attr   VSize    VFree   
  VolGroup00   1   2   0 wz--n-  <38.97g  <29.47g
  vg0          1   0   0 wz--n- 1020.00m 1020.00m
  vg_var       2   1   0 wz--n-    2.99g    1.12g
[vagrant@ubuntu ~]$ sudo pvremove /dev/sdb
  Labels on physical volume "/dev/sdb" successfully wiped.
[vagrant@ubuntu ~]$ sudo lvcreate -n LogVol_Home -L 2G /dev/VolGroup00
  Logical volume "LogVol_Home" created.
[vagrant@ubuntu ~]$ sudo mkfs.xfs /dev/VolGroup00/LogVol_Home
meta-data=/dev/VolGroup00/LogVol_Home isize=512    agcount=4, agsize=131072 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=0, sparse=0
data     =                       bsize=4096   blocks=524288, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
log      =internal log           bsize=4096   blocks=2560, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
[vagrant@ubuntu ~]$ sudo mount /dev/VolGroup00/LogVol_Home
mount: can't find /dev/VolGroup00/LogVol_Home in /etc/fstab
[vagrant@ubuntu ~]$ sudo mount /dev/VolGroup00/LogVol_Home /mnt/
[vagrant@ubuntu ~]$ sudo cp -aR /home/* /mnt/
[vagrant@ubuntu ~]$ sudo rm -rf /home/*
[vagrant@ubuntu ~]$ sudo umount /mnt/
[vagrant@ubuntu ~]$ sudo mount /dev/VolGroup00/LogVol_Home /home/
[vagrant@ubuntu ~]$ sudo vi /etc/fstab
[vagrant@ubuntu ~]$ sudo touch /home/file{1..20}
[vagrant@ubuntu ~]$ sudo lvcreate -L 100M -s -n home_snap /dev/VolGroup00/LogVol_Home
  Rounding up size to full physical extent 128.00 MiB
  Logical volume "home_snap" created.
[vagrant@ubuntu ~]$ sudo rm -f /home/file{11..20}
[vagrant@ubuntu ~]$ ls /home
file1  file10  file2  file3  file4  file5  file6  file7  file8  file9  vagrant
[vagrant@ubuntu ~]$ sudo umount /home
[vagrant@ubuntu ~]$ sudo lvconvert --merge /dev/VolGroup00/home_snap
  Merging of volume VolGroup00/home_snap started.
  VolGroup00/LogVol_Home: Merged: 100.00%
[vagrant@ubuntu ~]$ sudo mount /home
[vagrant@ubuntu ~]$ ls /home
file1  file10  file11  file12  file13  file14  file15  file16  file17  file18  file19  file2  file20  file3  file4  file5  file6  file7  file8  file9  vagrant

