# Proprietary drivers for Nvidia GPU
## List your machine GPU/IGPU
```shell
lspci -k | grep -A 2 -E "(VGA|3D)"
```

## List available drivers for your GPU
```shell
mhwd -l
```
FYI, it display something like `0300:10de:11e2` and `0300` is the classId

## List installed drivers
```shell
mhwd -li
```

## Try install proprietary drivers
```shell
sudo mhwd -a/--auto <usb/pci> <free/nonfree> <classid>
```
ex
```shell
sudo mhwd -a pci nonfree 0300
```

## Resolve packages conflicts
On i3, conky use a package that have to be removed to install nvidia proprietary drivers
```shell
sudo pacman -R manjaro-i3-settings
sudo pacman -R conky-i3
sudo pacman -R conky
```

## Try again install proprietary drivers
```shell
sudo mhwd -a pci nonfree 0300
```
If something like: `target not found: linux65-nvidia-390xx`, it means that your current kernel does not have a `nvidia-390xx` driver for its version.

## Resolve kernel conflicts
### Display your installed kernels
```shell
mhwd-kernel -li
```
### Display your running kernels
```shell
uname -r
```
### Install a new kernel
Have to find a kernel that implements `nvidia-390xx` driver  
ex
```shell
sudo mhwd-kernel -i linux66
```

## Reboot
Grub will run the last installed kernel
### Remove old kernel
mhwd will try to install `nvidia-390xx` for each kernel installed you have, so you must remove the old kernel.  
ex
```shell
sudo mhwd-kernel -r linux65
```
## Reboot
### Check
```shell
mhwd-kernel -li
```
```shell
uname -r
```
### Remove old free drivers
```shell
sudo mhwd -r pci video-linux
```
### List installed drivers
```shell
mhwd -li
```
Only 390xx is displayed !
## Set your default screen
As you change video driver, screen names on arandr or xrandr change.  
Open ARandR and set your new screen as default screen

