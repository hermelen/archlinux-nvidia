# mupen64plus
## Core
```shell
yay -S mupen64plus
```
## Graphics Plugin
```shell
yay -S mupen64plus-video-angrylion-plus-git
```
## Front-End
```shell
yay -S m64py
```
## Configure Mupen64Plus
### Create Configuration Directory
```shell
yay -S m64py
```
## Generate Configuration File
Run Mupen64Plus with a ROM file to generate the default configuration file:
```shell
mupen64plus path/to/your/romfile.n64
```
This will create a mupen64plus.cfg file in ~/.config/mupen64plus/
## Edit Configuration File:
`~/.config/mupen64plus/mupen64plus.cfg`
## Run mupen64plus from m64py
Launcher available on arch or 
```shell
m64py
```
## Input
### Configuration
#### UI
Settings => Plugins => <your-input-plugin>.so => Configure
#### Config file
`~/.config/mupen64plus/mupen64plus.cfg` ex: 
```shell
plugged = True
plugin = 2
Mouse = False
# Example button mappings
A = "button(2)"
B = "button(1)"
L = "button(4)"
R = "button(5)"
Z = "button(8)"
Start = "button(9)"
DPad U = "button(13)"
DPad D = "button(14)"
DPad L = "button(15)"
DPad R = "button(16)"
```
### Default
On m64py:  
Settings => Plugins => mupen64plus-input-sdl.so => Configure
### Advanced
```shell
yay -S mupen64plus-input-raphnetraw
```


