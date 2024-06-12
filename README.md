# arch manual install guide
hello, this is a beginner friendly tutorial on how to install arch linux. dont forget to smash the like button, subscri-

**NOTE: THIS TUTORIAL IS AIMED AT DAILY PERSONAL USAGE, YOU CAN STILL USE IT FOR DIFFERENT PURPOSES BUT YOU WILL HAVE TO HAND PICK SOME PARTS TO SKIP IN THE LAST SECTION**

# the requirements
0. having a PC, a keyboard and a mouse (the mouse is optional for the install but used in a desktop interface)
1. a universal serial bus (USB) thumbdrive/pendrive/flashdrive and a port on your pc to go with that
2. knowing how to boot into your boot menu
3. enough space (75 is barely enough, 100 lasts a while (3 weeks, or more if ur careful) and 150-250 is reccomended)
4. an internet connection
5. PATIENCE
6. keeping calm (if something didnt work just browse the internet, the only thing that hasnt worked for me till now is rounded window borders in a window manager called i3 which i ignored and noehting bad has happened and will never happen)
7. another device to follow this tutorial
# tutorial starts... now!
## 1. getting into the install
### 1-1. getting the USB ready for the install
okay in this step you need a flash drive more than a gigabyte (a 4gb or an 8gb one works flawlessly)
and you need this program called balena etcher.
download the ``.iso`` file from the https://archlinux.org website (more than a gigabyte btw)
and then, open the balena etcher program and plug in your usb. select your USB driver and the ``.iso`` file and then its time to flash
now just wait, and after you are done, restart your pc.
### 1-2. getting into the install 
here comes "knowing how to boot into your boot menu", find ur laptop - or PC motherboard - model online and learn what button makes it go into the boot menu, also dont forget to keep your USB plugged in since it will boot off of that.
after you are done with your research, just press the button repetetively when the boot logo appears. aaaand if you did it right, you should be in the terminal!
## 2. the real deal (installing it)
**NOTE:** if your power goes out after the partitioning step, you will have to redo the install process after step 2 starts
### 2-1. getting the internet connected
okay so now you will have to use ethernet or use wifi, check the [archwiki IWD](https://wiki.archlinux.org/title/Iwd) page for more info for WIFI, ethernet works after plugging it in
you can do the command
```
ip link
```
to check if your router is up or not.
and to verify if your internet works, do the command
```
ping archlinux.org
```
### 2-2. getting time synced
time gets synced when you boot the live system from a USB, you can do the command
```
timedatectl
```
to check if its synced like usual.
### 2-3. paritioning time
**NOTE:** before you get into partitioning you have to know how have you booted into arch, run the command
```
cat /sys/firmware/efi/fw_platform_size
```
if the command returns 64, you are in normal UEFI and you need to follow the UEFI-specific parts of the tutorial to make your pc boot correctly and not break, if it returns 32, you are also running in UEFI, but you can only use systemd-boot or GRUB, for this tutorial, GRUB is highly reccomended because its easy to configure. but if it returns an error saying the file does not exist, you are booted in BIOS and your motherboard is in UEFI mode, you have to wipe it with rufus (use an empty image included in the program, and use GPT instead of MBR) and then, reflash it with balena etcher and reboot into the live image.

to have an overview over your disks, do the command
```
fdisk -l
```
or if the text is too big to see the whole thing, add a `` | less`` at the end like below
```
fdisk -l | less
```
the way partitioning works is that you have a disk (for example ``/dev/sda`` or /dev/sdb) and the partitions in it goes in a numerical order after the partition name, for example, ``/dev/sda1`` or ``/dev/sdb3``.

you will get a result like below as your disk:
```
Disk /dev/sda: 476.94 GiB, 512110190592 bytes, 1000215216 sectors
```
if you only want to see your disks do the command:
```
fdisk -l | grep Disk
```
**NOTE:** you can also add the `` | less``
you will get the disk name, disk model, the disklabel type and the disk identifier, we only need the name (``/dev/sda`` for example)

