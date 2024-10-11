﻿# Repair your kernel
## Create a archlinux Live USB
From another computer, create a Live USB with your favorite tool (Rufus, SUSE Image Writer...)
## Step 1: Boot into a Live Environment and mount partitions
Check your destop key to boot on USB.  
### Troubleshooting
If it does not work, ckeck your BIOS config:
- FastBoot must be disabled
- SecureBoot must be disabled
- Maybe other settings must be mandatory, Google is your best friend (after ChatGPT)  
Sometimes, need to change BIOS boot order if boot key does not boot.
### Identify your root partition:
```shell
sudo lsblk
```
Look for the partition that has your Linux installation, typically something like /dev/sda1 or /dev/nvme0n1p1.

### Mount the root partition:
```shell
sudo mount /dev/sdXn /mnt
```

### Mount other necessary filesystems:
```shell
sudo mount --bind /dev /mnt/dev
sudo mount --bind /proc /mnt/proc
sudo mount --bind /sys /mnt/sys
```

## Step 2: Run mounted partitions:
### Chroot mounted partitions
```shell
sudo chroot /mnt
```

### List files in /boot
```shell
ls /boot
```
If the file vmlinuz-linux or a similar kernel image is missing or not, anyway, have to install or reinstall it to repair.

### Reinstall the Kernel

#### Update package lists:
```shell
pacman -Syu
```

#### Reinstall the kernel package:
```shell
pacman -S linux
```
or specify
```shell
pacman -S linux610
```

## Exit and reboot
## Exit chroot and unmount filesystems:
```shell
exit
sudo umount /mnt/dev
sudo umount /mnt/proc
sudo umount /mnt/sys
sudo umount /mnt
```

## Reboot:
```shell
reboot
```

Must be OK now, but maybe your GRUB is broken if you have dual boot
## Update the Bootloader
Once your kernel is repaired, open a terminal on your desktop.  
[restore-grub}](./restore-grub.md)