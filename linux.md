## Increase LVM Logical Volume
Extend the size to use the entire drive

```
ubuntu@14900c:~$ df
Filesystem                        1K-blocks     Used Available Use% Mounted on
tmpfs                              12924848    16352  12908496   1% /run
efivarfs                                192      163        25  87% /sys/firmware/efi/efivars
/dev/mapper/ubuntu--vg-ubuntu--lv 102626232 90379972   6986996  93% /
tmpfs                              64624236       12  64624224   1% /dev/shm
tmpfs                                  5120       16      5104   1% /run/lock
tmpfs                                  1024        0      1024   0% /run/credentials/systemd-journald.service
tmpfs                                  1024        0      1024   0% /run/credentials/systemd-resolved.service
tmpfs                              64624240        8  64624232   1% /tmp
/dev/nvme1n1p2                      1992552   260036   1611276  14% /boot
/dev/nvme1n1p1                      1098632     6428   1092204   1% /boot/efi
tmpfs                                  1024        0      1024   0% /run/credentials/systemd-networkd.service
tmpfs                              12924844       72  12924772   1% /run/user/60578
tmpfs                              12924844       60  12924784   1% /run/user/1000
ubuntu@14900c:~$ sudo vgdisplay
[sudo: authenticate] Password: 
  --- Volume group ---
  VG Name               ubuntu-vg
  System ID             
  Format                lvm2
  Metadata Areas        1
  Metadata Sequence No  2
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                1
  Open LV               1
  Max PV                0
  Cur PV                1
  Act PV                1
  VG Size               <3.64 TiB
  PE Size               4.00 MiB
  Total PE              953080
  Alloc PE / Size       25600 / 100.00 GiB
  Free  PE / Size       927480 / <3.54 TiB
  VG UUID               cqRef7-lvRy-JvNF-B3sf-ZdzU-Tzh9-qb8ziR
   
ubuntu@14900c:~$ sudo lvextend --extents +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv
  Size of logical volume ubuntu-vg/ubuntu-lv changed from 100.00 GiB (25600 extents) to <3.64 TiB (953080 extents).
  Logical volume ubuntu-vg/ubuntu-lv successfully resized.
```
