## Reboot Linux in firware-setup mode to get bios settings F2/F12/Delete
sudo systemctl reboot --firmware-setup
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

not picked up yet
ubuntu@14900c:~/wse_github/obrienlabsdev/biometric-backend/biometric-nbi/src/kubernetes$ lsblk
NAME                      MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0                       7:0    0     4K  1 loop /snap/bare/5
loop1                       7:1    0    74M  1 loop /snap/core22/2411
loop2                       7:2    0  66.8M  1 loop /snap/core24/1643
loop3                       7:3    0    74M  1 loop /snap/core22/2437
loop4                       7:4    0 531.5M  1 loop /snap/gnome-42-2204/263
loop5                       7:5    0 531.4M  1 loop /snap/gnome-42-2204/247
loop6                       7:6    0 614.5M  1 loop /snap/gnome-46-2404/164
loop7                       7:7    0  66.8M  1 loop /snap/core24/1587
loop8                       7:8    0 260.8M  1 loop /snap/firefox/8819
loop9                       7:9    0  91.7M  1 loop /snap/gtk-common-themes/1535
loop10                      7:10   0 261.1M  1 loop /snap/firefox/8803
loop11                      7:11   0  50.1M  1 loop /snap/snapd/27591
loop12                      7:12   0   395M  1 loop /snap/mesa-2404/1165
loop13                      7:13   0 606.1M  1 loop /snap/gnome-46-2404/153
loop14                      7:14   0 221.1M  1 loop /snap/thunderbird/1228
loop15                      7:15   0   402M  1 loop /snap/mesa-2404/1839
loop16                      7:16   0  50.1M  1 loop /snap/snapd/27710
loop17                      7:17   0 219.9M  1 loop /snap/thunderbird/1201
sda                         8:0    0  10.9T  0 disk 
├─sda1                      8:1    0    16M  0 part 
└─sda2                      8:2    0  10.9T  0 part 
nvme1n1                   259:0    0   3.6T  0 disk 
├─nvme1n1p1               259:4    0     1G  0 part /boot/efi
├─nvme1n1p2               259:5    0     2G  0 part /boot
└─nvme1n1p3               259:6    0   3.6T  0 part 
  └─ubuntu--vg-ubuntu--lv 252:0    0   3.6T  0 lvm  /
nvme0n1                   259:1    0   3.6T  0 disk 
├─nvme0n1p1               259:2    0    16M  0 part 


ubuntu@14900c:~/wse_github/obrienlabsdev/biometric-backend/biometric-nbi/src/kubernetes$ df --human-readable
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                               13G   17M   13G   1% /run
efivarfs                           192K  163K   25K  87% /sys/firmware/efi/efivars
/dev/mapper/ubuntu--vg-ubuntu--lv   98G   87G  6.7G  93% /
tmpfs                               62G   12K   62G   1% /dev/shm
tmpfs                              5.0M   16K  5.0M   1% /run/lock
tmpfs                              1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
tmpfs                              1.0M     0  1.0M   0% /run/credentials/systemd-resolved.service
tmpfs                               62G  8.0K   62G   1% /tmp
/dev/nvme1n1p2                     2.0G  254M  1.6G  14% /boot
/dev/nvme1n1p1                     1.1G  6.3M  1.1G   1% /boot/efi
tmpfs                              1.0M     0  1.0M   0% /run/credentials/systemd-networkd.service
tmpfs                               13G   72K   13G   1% /run/user/60578
tmpfs                               13G   60K   13G   1% /run/user/1000


run resize2fs for ext4
ubuntu@14900c:~$ df -hPT
Filesystem                        Type      Size  Used Avail Use% Mounted on
tmpfs                             tmpfs      13G   17M   13G   1% /run
efivarfs                          efivarfs  192K  163K   25K  87% /sys/firmware/efi/efivars
/dev/mapper/ubuntu--vg-ubuntu--lv ext4       98G   87G  6.5G  94% /
tmpfs                             tmpfs      62G   12K   62G   1% /dev/shm
tmpfs                             tmpfs     5.0M   16K  5.0M   1% /run/lock
tmpfs                             tmpfs     1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
tmpfs                             tmpfs     1.0M     0  1.0M   0% /run/credentials/systemd-resolved.service
/dev/nvme0n1p2                    ext4      2.0G  254M  1.6G  14% /boot
tmpfs                             tmpfs      62G  8.0K   62G   1% /tmp
/dev/nvme0n1p1                    vfat      1.1G  6.3M  1.1G   1% /boot/efi
tmpfs                             tmpfs     1.0M     0  1.0M   0% /run/credentials/systemd-networkd.service
tmpfs                             tmpfs      13G   68K   13G   1% /run/user/60578
tmpfs                             tmpfs      13G   60K   13G   1% /run/user/1000
ubuntu@14900c:~$ sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
resize2fs 1.47.2 (1-Jan-2025)
Filesystem at /dev/mapper/ubuntu--vg-ubuntu--lv is mounted on /; on-line resizing required
old_desc_blocks = 13, new_desc_blocks = 466
The filesystem on /dev/mapper/ubuntu--vg-ubuntu--lv is now 975953920 (4k) blocks long.

ubuntu@14900c:~$ df -hPT
Filesystem                        Type      Size  Used Avail Use% Mounted on
tmpfs                             tmpfs      13G   17M   13G   1% /run
efivarfs                          efivarfs  192K  163K   25K  87% /sys/firmware/efi/efivars
/dev/mapper/ubuntu--vg-ubuntu--lv ext4      3.6T   87G  3.4T   3% /
tmpfs                             tmpfs      62G   12K   62G   1% /dev/shm
tmpfs                             tmpfs     5.0M   16K  5.0M   1% /run/lock
tmpfs                             tmpfs     1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
tmpfs                             tmpfs     1.0M     0  1.0M   0% /run/credentials/systemd-resolved.service
/dev/nvme0n1p2                    ext4      2.0G  254M  1.6G  14% /boot
tmpfs                             tmpfs      62G  8.0K   62G   1% /tmp
/dev/nvme0n1p1                    vfat      1.1G  6.3M  1.1G   1% /boot/efi
tmpfs                             tmpfs     1.0M     0  1.0M   0% /run/credentials/systemd-networkd.service
tmpfs                             tmpfs      13G   68K   13G   1% /run/user/60578


## OS version
```
cat /etc/os-release
```
tmpfs                             tmpfs      13G   60K   13G   1% /run/user/1000
```
