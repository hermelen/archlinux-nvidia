# Archlinux restore GRUB
## Linux (from chroot or on linux OS)
### Automatic restore
Identify bootable partition
```shell
sudo os-prober
```
Update grub with theses partitions 
```shell
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
```shell
reboot
```
### Manual 
```shell
sudo efibootmgr
```
Will show you the boot order.
Here the first boot partition is `Boot0000* Windows Boot Manager` BUT it is set to `\EFI\Manjaro\grubx64.efi`, so it's ok.  
You can set `Windows Boot Manager` on Windows section below.
```shell
BootCurrent: 0000
Timeout: 5 seconds
BootOrder: 0000,0001
Boot0000* Windows Boot Manager  HD(1,GPT,acc83e33-08e8-4be1-b1c7-d797078bd874,0x800,0x32000)/\EFI\Manjaro\grubx64.efi57494e444f5753000100000088000000780000004200430044004f0042004a004500430054003d007b00390064006500610038003600320063002d0035006300640064002d0034006500370030002d0061006300630031002d006600330032006200330034003400640034003700390035007d00000061000100000010000000040000007fff0400
Boot0001* Windows Boot Manager  HD(1,GPT,acc83e33-08e8-4be1-b1c7-d797078bd874,0x800,0x32000)/\EFI\Microsoft\Boot\bootmgfw.efi
```
If not ok, set grub as first boot partition  
ex (the first value is your boot partition ID, etc):
```shell
sudo efibootmgr --bootorder 0001,0000
```
#### Notes:
Devices ID seems to be 000* for EFI files, 200* for USB devices (maybe CD-ROM too, or it is 100*), 300* seems to be hard-disk volumes.  
Maybe adding some 2001, 3001 etc will display other bootable devices... Have to check.
## Windows
It is possible too to set Windows Boot Manager from Windows, but if linux `efibootmgr` is not ok, it will not be useful
```shell
bcdedit /set {bootmgr} path \EFI\Manjaro\grubx64.efi
```
