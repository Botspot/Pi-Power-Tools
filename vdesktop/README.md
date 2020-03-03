# vdesktop
## Run a second instance of Raspbian inside Raspbian. 
![screenshot of Stretch running in buster](https://i.stack.imgur.com/oti6Z.png)  
This script is excellent in these situations:
 - Migrating to a clean install of Raspbian and want to compare the appearance of both OS'es at once.
 - Running two versions of software at the same time, one in the host, other in the guest.
 - Running something you might want to undo (such as compiling) and don't want your main OS modified.
 - "Switch" OSes without ever shutting down or swapping SD cards.
 - Run Raspbian Stretch on a Pi 4.

## Download the [disk image](https://drive.google.com/file/d/1cJbcNDnm4Zm8zeHlCp8JQT5pwacAZeCp/view?usp=sharing)
Ships with vdesktop installed, and a handy menu shortcut to boot a pre-downloaded Stretch img file.

## To download & make excecutable:  
`git clone https://github.com/Botspot/vdesktop`  
`chmod +x /home/pi/vdesktop/rc.local /home/pi/vdesktop/vdesktop`

## To run:  
`sudo ~/vdesktop/vdesktop`

## Usage:  
Boot from an image file:    `sudo ~/vdesktop/vdesktop /home/pi/Downloads/2018-07-09-pi-topOS.img`  
Or a block device:          `sudo ~/vdesktop/vdesktop /dev/sda`  
Or the guest's directory:   `sudo ~/vdesktop/vdesktop /home/pi/raspbian-stretch/`  

Once the container has booted, you have to log in with the guest's credentials. Then the guest's GUI will display in the Xephyr window.

## To do:
 - Write up a more comprehensive set of instructions, and add come CLI flags.
 - autologin to the guest, so the user doesn't have to do it manually.
 - auto-detect default desktop session profile to correctly boot pi-top OS and Raspbian that doesn't have raspberrypi-ui-mods installed.
 - Sync sound between host and guest, while avoiding pulseaudio.
 - display text at guest's default size instead of autoscaling to Xephyr's aspect ratio.
 - display guest's default mouse pointer instead of the fallback Adwaita.
