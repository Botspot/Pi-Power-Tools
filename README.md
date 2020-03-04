![logo](https://github.com/Botspot/Pi-Power-Tools/blob/master/icons/logo-64.png?raw=true)  
# Pi Power Tools
## The ultimate Swiss Army Knife for Raspbian Disk Images and SD Cards.

### No other tool can do any of these:
 - **Boot** - Powered by [Vdesktop](https://github.com/Botspot/vdesktop). Runs the disk image in a virtual machine.
 - **Flash** - Flashes Raspbian directly from the Internet to the selected device.
 - **Mount** - Full control to manage loop devices and mountpoints.
 - **Edit** - Auto-creates a loop device for the disk image then opens it with Gparted.
 - **Resize** - Expand or shrink a disk image, thanks to RonR's [Image-utils](https://www.raspberrypi.org/forums/viewtopic.php?t=247568).

## To install:
#### Run this in the terminal:
`wget -O - https://raw.githubusercontent.com/Botspot/Pi-Power-Tools/master/update | bash`

After installing, you can run **Pi Power Tools** from either Menu --> Accessories or from the desktop:  
![desktop button](https://i.ibb.co/KzJ8cyX/desktop.png)  

# Instructions:
Pro tip: Most buttons display an explanation if you move your mouse over them.
## Tabs of the PPT Main Window:
 - **Home**  
![home page](https://i.ibb.co/NyFx4Sk/home.png)  
Nothing much to do here. Clicking that dark blue link brings you to this page.  

 - **USB Drive**  
![usb drive page](https://i.ibb.co/fDTRmWR/Screenshot-from-2020-03-03-16-28-50.png)  
Select a USB drive in the list, then click one of the action buttons on the bottom.  
*Please note that your Pi's root device (/dev/mmcblk0) cannot be flashed or booted.*  

 - **IMG File**  
![img file page](https://i.ibb.co/BPpQfk5/Screenshot-from-2020-03-03-16-29-07.png)  
Two ways to open a disk image:  
    • Paste the file's full path in the "Paste Path:" field.  
Find the path using the file manager:  
![pcmanfm copy paths](https://i.ibb.co/tX35Kpk/copy-paths.png)  
*Pro tip: click the arrow on the right to select previously used disk images.*
    • Or, click the button in the "Find one:" field to open a disk image.  
The two lower buttons each open tools that only apply to disk images.  


## Action buttons of the Main Window:  

 - **Refresh**  
![Refresh button](https://i.ibb.co/HDRyQyB/refresh.png)  
Click this if you plugged in a USB drive **after** starting Pi Power Tools.  

 - **Flash**  
*This is the only action button that does not require a device to be selected first.*  
First page:  
![Flash tool first page](https://i.ibb.co/82Ntr61/flash1.png)  
Select an input disk image and an output usb drive. Notice that the filesystem root device is not listed.  
Pro tip: *In the `From` field, you can paste the path to a ZIP file.*  
Click the arrow on the right to view all available flash-from devices.  
If you chose to Download, this window will appear next asking which download program you want.  
![Flash tool second page](https://i.ibb.co/gRWxsZ4/flash2.png)  
With a good Internet connection and a fast usb device, flashing Raspbian Full usually takes **300 seconds or less**.  
On the other hand, a slow usb device or Internet connection may take over **2000 seconds** to complete.  

 - **Boot**  
Select a device (img file or usb drive), then click Boot. With this handy button, you can customize a disk image before flashing it to your SD card.  
A Console will appear and display the boot text like this:  
![boot console](https://i.ibb.co/vVH4rdb/terminal.png)  
*Under certain circumstances, Vdesktop will ask permission to change a UUID or a machine-id. This rarely corrupts anything, so typing `y` is usually appropriate.*  
After it has booted, a window similar to VNC will open and display the desktop.  
![xephyr](https://i.ibb.co/8zFtZ9V/xephyr.png)  
*It is a known issue that the browser crashes with the `Aw, Snap!` error.*  

 - **View**  
Mounts the selected device to `/media/pi/pi-power-tools`.  
![](https://i.ibb.co/stnrpW0/view-dialog.png)  
When you close the above window, the selected device will be unmounted (ejected).  

 - **Edit**  
Lets you edit the partitions of the selected device.  
![gparted opening a disk image](https://i.ibb.co/C24p2HC/gparted.png)  
If Gparted is not already installed, you will be prompted to install it.  

## Image-specific tool buttons:  
![screenshot](https://i.ibb.co/r7Lrn05/image-specific-tools.png)  
 - **Image-Utils GUI**  
[RonR's image-utils](https://www.raspberrypi.org/forums/viewtopic.php?t=247568) wrapped in a graphical frontend.  
![home page](https://i.ibb.co/p4BQj0X/image-tools1.png)  
Paste in a location to a disk image, then click an action button. The **settings tab** lets you customize some aspects of the tools.  
![image-utils settings tab](https://i.ibb.co/KxPRVhP/image-utils2.png)  
 - **Advanced Mount**  
Fine-tune control over loop devices and mountpoints for disk images.  
Select the disk image you want:  
![image-utils settings tab](https://i.ibb.co/vLRQscg/advmount-page-1.png)  
If there are multiple loop devices associated with it, you will be prompted to choose one. You can also delete unwanted loop devices:  
![image-utils settings tab](https://i.ibb.co/LrrFLcJ/advmount-page-2.png)  
Now you can mount and unmount each partition where you want to:  
![image-utils settings tab](https://i.ibb.co/bFLTDnS/advmount-page-3.png)  
When you're finished, be sure to click **Delete** to detach the loop device.

## FAQ
 - Q: Unique logo. What inspired you?
A: It's a mishmash of BB-8, the RPi logo, and a saw blade to convey a power tool.
