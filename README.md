# Pi Power Tools ![logo](https://github.com/Botspot/Pi-Power-Tools/blob/master/icons/logo-64.png?raw=true)
[![badge](https://github.com/Botspot/pi-apps/blob/master/icons/badge.png?raw=true)](https://github.com/Botspot/pi-apps)  
## General Purpose Raspbian Image & SD Card Manager
Want to **build your own custom Raspbian SD card image**? Like enabling ssh, modifying `/boot/config.txt`, doing an `apt update`, enabling VNC, or installing something?  
Have a pile of sd cards and curious what's on them? (and don't want to boot them, one at a time, in a Pi?)  
Want to **run two versions of Raspbian** at once?  
Or, how about **running Raspbian Stretch on a Pi 4**?  
### No other tool can do any of these:
 - **Boot** - Powered by [Vdesktop](https://github.com/Botspot/vdesktop). Runs the Raspbian image in a virtual machine. It even shows the desktop!
 - **Flash** - Flashes Raspbian directly from the Internet to the selected device. Tuned for maximum speed, [proven by benchmarks](https://www.raspberrypi.org/forums/viewtopic.php?f=63&t=272365).
 - **Mount** - Full control to manage loop devices and mountpoints.
 - **Edit** - Auto-creates a loop device, then lets you mess up its partitions with Gparted.
 - **Resize** - Add or remove free space from a disk image with a single click. <-- This also repairs the image!

Sneak peek:  
![img mode](https://i.ibb.co/yQnT2sC/img-mode.png)  
Want to give it a spin? Great!  
## To download & install:
```
wget -O - https://raw.githubusercontent.com/Botspot/Pi-Power-Tools/master/update | bash
```
This clones the repository to `/home/pi/Pi-Power-Tools`, adds a menu button, clones my [vdesktop repo](https://github.com/Botspot/vdesktop), and asks permission before installing YAD. Nothing is modified outside of your home directory.
#### System requirements:
 - Raspberry Pi 3B, 3B+, or 4B (untested on older models)
 - Running Raspbian Buster or Stretch
 - Passwordless `sudo` ability for `pi` user
 - Internet connection (recommended for update checking & img downloading)
    
After installing, Pi Power Tools can be launched from the Menu:  
![menu](https://i.ibb.co/PQthp6N/menu.png)  

## To uninstall:
If it's not working for you, please [open an issue](https://github.com/Botspot/Pi-Power-Tools/issues/new).
```
sudo apt purge gparted yad systemd-container xserver-xephyr expect
rm -rf ${HOME}/Pi-Power-Tools ${HOME}/Pi-Power-Tools.old
rm ${HOME}/Desktop/ppt.desktop ${HOME}/.local/share/applications/ppt.desktop
```
---
# Instructions
### Table of Contents
 - [Home](#home)
   - [Settings](#settings)
 - [IMG Mode](#img-mode)
 - [USB Mode](#usb-mode)
 - [Flash](#flash)
 - [Button explanations](#explanations-for-some-buttons)
   - [Boot](#boot)
   - [View](#view)
   - [Edit](#edit)
   - [Advanced Mount](#advanced-mount)
 - [Under the hood](#under-the-hood)
   - [Directory Tree](#directory-tree)
 - [Q&A](#qa)
## Home
![home page](https://i.ibb.co/vz4yR40/home.png)  
The menu button opens this window by default. Enter [IMG Mode](https://github.com/Botspot/Pi-Power-Tools#img-mode) or [USB Mode](https://github.com/Botspot/Pi-Power-Tools#usb-mode) from here. The Update button will appear if an update is available.  
### Settings
![settings](https://i.ibb.co/Cz9YMDj/settings.png)  
Currently, you can change what the menu button opens by default - (Flash, IMG Mode, USB Mode, and Home), if the Boot Button launches the Desktop, whether or not to run `zerofree` when the Shrink Button is clicked, and how much free space to add when the 'X GB free' button is clicked.  


## IMG Mode
Customize Raspbian Images.  
![img mode](https://i.ibb.co/yQnT2sC/img-mode.png)    
Before you can see that above page, you first have to select an img.  
![img mode page 1](https://i.ibb.co/0sp9NMz/2020-11-27-092634-1920x1080-scrot.png)  
**4 ways** to select a Raspbian Image:
 1. **Click the arrow** on the right to see any previously used disk images:  
![arrow](https://i.ibb.co/tH9qLTQ/arrow.png)  
 1. **Drag-n-drop** a Raspbian image from File Manager to the text box:  
![drag and drop](https://i.ibb.co/PmFWQzh/dnd.png)  
 1. Click **Download New** to download & unzip a new Raspbian image:  
![download](https://i.ibb.co/XD8FgkN/download.png)
Download mode has been tuned for **maximum speed**.  
![benchmark](https://i.ibb.co/25KV76J/benchmark.png)
 1. Or create an img from your running Pi by clicking SD to IMG.  
![sd to img](https://i.ibb.co/pR2dH2N/snapshot.png)  

After a disk image has been selected, this main page appears:  
![img mode](https://i.ibb.co/yQnT2sC/img-mode.png)  
**Buttons**:
 - **Back**: Back to the image selection window.  
 - **Flash**: Copy everything from the selected img to a device. [Details](#flash)  
 - **Boot**: Attempt to "boot" the selected device using a virtual desktop. [Details](#boot)  
 - **View**: Mounts the image to `/media/pi/pi-power-tools` so you can modify the filesystem. [Details](#view)  
 - **Edit**: Modify the partitions using Gparted. [Details](#edit)  
 - **Reset PT**: This button *attempts* to fix the partitions if you messed them up somehow. It replaces the partition table with the one from Raspbian Buster Full. Your Mileage May Vary.  
 - **Advmount**: Control exactly where to mount each partition. In theory this will work for any kind of disk image, but has only been tested on Raspbian images. YMMV.  [Details](#advanced-mount)    
  - **Shrink**: Removes all free space from the selected image. If enabled in [Settings](#Settings), `zerofree` will run afterwards to remove unused blocks from the disk image. 
    - <ins>Though similar in function, the script used to do this is entirely different in design and does not utilize RonR's `image-utils` in any way.</ins>
 - **1 GB Free**: Adds one gigabyte of free space to the root partition. Customize how much free space in [Settings](https://github.com/Botspot/Pi-Power-Tools#settings).
   - It is **not accumulative**, so clicking it multiple times won't result in multiple gigabytes of free space.
## USB Mode
Manage storage devices connected to your Pi.  
![usb mode](https://i.ibb.co/vJ68mRY/usb.png)  
Select a drive in the list, then click an action button on the bottom.  
*Your Pi's internal SD Card (`/dev/mmcblk0`) cannot be flashed or booted.*  
**Buttons**:  
   - **Home**: Back to the [home window](#home).  
   - **Refresh**: Check for any newly inserted storage devices.  
   - **Flash**: Copy everything from an img to the selected device. [Details](#flash)  
   - **Boot**: Attempt to "boot" the selected device using a virtual desktop. [Details](#boot)  
   - **View**: Mounts the device to `/media/pi/pi-power-tools`. [Details](#view)  
*Intended for Raspbian devices only, as this button assumes there are 2 partitions. (and mounts partition 1 to `/media/pi/pi-power-tools/boot`)*  
   - **Edit**: Modify the partitions using Gparted. [Details](#edit)  
## Flash
![flash tool](https://i.ibb.co/YcrCspx/flash.png)  
Select an input disk image and an output usb drive. The filesystem root device (`/dev/mmcblk0`) cannot be flashed and so is not listed.  
In addition to any previously used img and zip files, there are **three download options**:
![flash download options](https://i.ibb.co/3RRfnrR/flash-dl-opts.png)  
If Download is selected, this window will appear next asking which download mode you want.  
![Flash tool second page](https://i.ibb.co/dmL3b7s/flash2.png)    
The first mode is much faster than the second one.
Breakdown of the pros and cons:
| Faster mode | Slower mode|
|--|--|
|For Pies that don't have sufficient free space to hold a large disk image|You keep the downloaded image for later.|
|Better for a single flash|Better for flashing multiple SD cards

Concerning speed, here are benchmarks made on a 4GB Pi 4:
||Faster Mode:|Slower mode:|
|--|--|--|
|Raspbian Full|387 seconds|816 seconds|
|Raspbian|205|393|
|Raspbian Lite|102|184|
---
# Explanations for some buttons:
## Boot
With this handy button, you can "test drive" your img/usb without needing to power down, switch sd cards, etc. Any changes made inside (`apt install`, change preferences, etc) will be preserved in the img/usb.

> Instead of a Virtual Machine, this technique runs at **100% native speed** (no emulation), because the guest runs the same kernel as the host device. Therefore, only booting Raspbian is supported, as **other OSes require other kernels**.  
> That means this method will still work just fine, *even if the whole boot partition is corrupted*!

First, the VM's Console will appear and display the boot text.
After the boot process has completed, and if "Boot to Desktop" is enabled in [Settings](#settings), a window similar to VNC will open and display the desktop.  
![animated boot button](https://github.com/Botspot/Pi-Power-Tools/blob/master/icons/boot_mode.gif?raw=true)  

> It is a [known issue](https://github.com/Botspot/vdesktop/issues/3) that the browser crashes with the `Aw, Snap!` error.

## View
Mounts the selected device/img to `/media/pi/pi-power-tools`.  
![view dialog](https://i.ibb.co/RgbKJff/view-files.png)  
When you close the `Viewing /dev/sdX` dialog window, the selected device will be unmounted (ejected).  

## Edit
Lets you edit the partitions of the selected device using `gparted`.  
![gparted opening a disk image](https://i.ibb.co/pww2C9h/gparted.png)  
  
## Advanced Mount
Fine-tune control over loop devices and mountpoints for disk images.    
If there are multiple loop devices associated with it, you will be prompted to select one and delete the others.  
Which one to delete? Usually you want to keep the top one on the list. (in this example, that's `/dev/loop0`)  

![image-utils settings tab](https://i.ibb.co/ftn0JXz/loop-select.png)    
Now you can mount each partition where you want to:  
![image-utils settings tab](https://i.ibb.co/PQXPL1M/advmount.png)    
When you're finished, be sure to **click Delete** to detach the loop device.

---
## Under the hood
Pro tip: *There are many comments in the shell scripts. Not only does this assist debugging, it also makes most of it self-explanatory.*  
### Directory Tree:

**Pi-Power-Tools/** - This is the main folder that stores everything.
> During an update, the old folder is renamed to Pi-Power-Tools.old/
 - Scripts:
   - **installgui** - This prompts for packages to be installed
   - **flash** - This is the [Flash tool](#flash)'s script.
   - **update** - This script is what installs/updates Pi Power Tools.
   - **home** - This is [Home](#home)'s script.
   - **img-mode** - This script is [IMG Mode](#img-mode).
   - **usb-mode** - This script is [USB Mode](#usb-mode).
 - Other files:
   - **installedpackages** - Keeps a record of what the update script installed.
   - **README.md** - You are reading [this](https://github.com/Botspot/Pi-Power-Tools/blob/master/README.md) right now.
 - Folders:
 - **functions/** - Stores sub-scripts that do certain things.
   - **advmount** - The [Advanced Mount](#advanced-mount) tool.
   - **buffer** - The secret sauce behind the fast download speeds. This ARMHF executable ships with Pi Power Tools, to prevent adding a dependency for installing `buffer`.
   - **edit** - A short bash script that opens a Raspbian image in `gparted`. It handles creating a loop device and deleting it when done.
   - **imglist-parser** - Bash script that parses `imglist`, deletes entries that don't exist on the filesystem, removes duplicate entries, and `echo`'s the resulting output.
   - **milliways-image-backup** - Fork of a fork of RonR's image-backup. I have made substancial changes to most of the script.
   - **restore-pt** - Short bash script to overwrite the specified disk image's partition table with `part-table.img`.
   - **terminal-run** - This simple script is used to run bash scripts in a terminal. It's a standardized workaround originally developed for [Pi-Apps](https://github.com/Botspot/pi-apps).
   - **image-shrink** - Botspot's version of `image-shrink`. Added a couple bug fixes and removed the interactive elements for better scripting usage.
   - **zerofree** - Another ARMHF executable for recognizing unused blocks and overwriting them with zeros. Shrinks a disk image even more. Only used if enabled in [Settings](#settings).
   - **zerofree_runner** - Wrapper bash script to interface with `zerofree`. Creates a loop device for the specified img, runs `zerofree`, runs `shrinkimage`, then removes the loop device.
 - **data/** - Stores configuration files
   - **home.conf** - Stores the configuration from the [Settings window](#settings).
   - **imglist** - Keeps track of what disk images have been used. 
   - **mirrors** - URLs, sizes, and names of download sites. Feel free to add your own.
   - **mountpoint** - Change where to mount to. Default is `/media/pi/pi-power-tools`.
   - **part-table.img** - The default partition table extracted from Raspbian Buster Full. Used by the Reset PT button in [IMG Mode](#img-mode).
   - **vdesktop.conf** - Stores the boot mode for `vdesktop`. Possible values are `gui`, `cli`, and `cli-login`.
   - **version** - The new location for the version file. Compared against the online version to check for updates.
   - **ziplist** - Exactly the same as `imglist`, but stores entries for previously used ZIP files instead. Currently only used by the [Flash tool](#flash).
 - **icons/** - Stores all the icons for the user interface.
 - **vdesktop/** - Ships empty, but `installgui` populates this folder with all files from the [Vdesktop repo](https://github.com/Botspot/vdesktop).

### Basic script design:
 - The scripts all use YAD to handle the user interface.* I found that Zenity was way too limited. (and didn't allow for multiple buttons, button icons, customized tooltips, or much else)
`*` Okay, `installgui` and `update` *do* use zenity because Raspbian does not include YAD by default.

## Q&A
 - Q: Unique logo.![logo](https://github.com/Botspot/Pi-Power-Tools/blob/master/icons/logo-64.png?raw=true)What inspired you?    
> It's a combination of BB-8, the RPi logo, and a saw blade. Also I think it looks a bit like like a pineapple, which is my favorite fruit.
 - What made you develop this tool?  
> I while back, I wanted to download Raspbian, uninstall all programming tools from it, do an `apt update` & `upgrade`, add a chrome extension to the browser, then flash it to a SD card. It took *several days* to fumble around with terminal commands. The action was so simple, but the process so hard that I realized a tool to do it was sorely needed.
 - Q: How long did it take to program this?  
> Several months. But it saved me enough time to be worth it. And I had a blast programming it all.
