# A trashcan programmers guide on how to setup Manjaro (or Arch-based Linux distro) on Mac

## 0.0 Introductory statement and important information
My strategy for finding a way to install Linux and FOSS on a closed Mac is that of sticking my nose where it doesn't belong, where I have unsufficient knowledge. The strategy is not pretty, but I guarantee that it is a very efficient way of learning.  
I am not a developer, nor am I a decent programmer. I am an artist who likes to work with code and software and I have some basic knowledge about computers. 
But I am a trashcan programmer at best.   
So, be warned, if you choose to follow this guide, you are not following a perfect guide on how to get the OS you want. You are going on a messy journey of debugging software and hardware. But there is a way to get your freedom back. Open source.   
I wish to point out as well that even though this guide was made for a MacBook Pro Retina (mid 2014) a lot of these issues are shared across different Mac computers and often the solutions are the same.  
This guide also covers how to create a basic partition on your HDD so that you can always go back to macOS if you desire (I also explain why this is the optimal way to do it). I learned the hard way that erasing the entire disk is not the solution that you want. 

### 0.1 Motivation for this repo
As I do not have a ton of experience with installing a new OS, partitioning harddrives, configuring and compiling in C and so on, this repo is a way for me to collect the experiences gathered from this Linux journey.
I made this repo mainly for myself because I wanted to collect and gather my experiences with installing Manjaro on a MacBook instead of going back and forth. I will add config files and updates as I gain experience.  
Anyway, if you are as fed up with the restrictions of OS X and Mac in general, you might want to switch to a Linux based operating system. If that's the case, then I have good news and bad news for you:  
The good news is that your decision is excellent and Linux is a great choice. The bad news is that Mac and OS X is not very linux-friendly. I would in fact consider them linux-unfriendly. To make matters worse, you chose to install it on a laptop. But hey, there is a way and you just might get a better performing computer with better longevity out of this. If you care and spend the time to set things up properly.

### 0.2 Why Manjaro?

Manjaro is a beautiful distro of Linux which is Arch-based. An arch-based distro has the advantage of access to the Arch User Repository (AUR) which is a great community of people making open source software and packages. Installing Arch Linux could be an option for you, but Arch Linux is somewhat difficult to install and requires quite a lot of effort. Arch Linux is cutting edge and if you want control over every aspect of your OS, it is the way to go. Manjaro on the other hand is a lot easier to install and still gets the benefits of access to the AUR while being friendly on new users.
Manjaro is a rolling release system, meaning that every update is sent out immediately. Personally, I love rolling release systems but if it is not for you, consider installing a Debian-based distro maybe. Ubuntu, Mint, Fedora. Whatever you like.

### 0.3 A list of common problems/bugs that you might need to deal with

Here is a short list of common problems that people are having when trying to install Linux on a Mac just so you know (this will depend on which Mac you are installing on). Before reading this list you should know that some of these problems are very easy to fix (a single line of code will fix most of these, but some are more persistent). All these issues, except for the camera, is adressed here. 

* WiFi needs a new broadcom driver to work properly. This issue is easily fixed with a simple install of a package.

* Fans are going at max speed at all times. This issue is slightly more complicated but the solution is quite easy nevertheless.

* Camera is not working out of the box. Personally I don't care about having a camera on my laptop in general. But this issue should be easy to fix by installing the facetime package from the arch user repository.

* CPU runs hot (even when idle). This issue is adressed in the guide and it is the most complicated on the list. For some the solution is to disable file indexing as a background service. For others it requires a close monitoring of what exaclty is eating your CPU. This guide will go through setting up CPU frequency scaling and debugging firmware interrupts as well. Your solution may vary and may require research. 

##### FINAL WARNING: This is not a perfect guide and if you choose to erase your disk or fry an egg on your burning hot CPU, it's up to you to find new hardware and a way to restore your OS if you want. Choice of OS is your decision. As it should be. 

## 1.0 Installing Manjaro
This sections are put together from a variety of sources. This guide mainly covers how to configure Manjaro post-installation. And so this section is kept brief and short because there are a million different, good guides on how to dual boot OS X and Linux. If you want to follow a different guide on installing the OS, skip this section and go to 2.0 and I would recommend this guide for the actual installation: https://www.lifewire.com/dual-boot-linux-and-mac-os-4125733

### 1.1 Desktop Environments
I will keep this short. I like the KDE desktop environment. It looks great and is highly customizable. If you want GNOME or whatever, go for it. In the end, if you don't like it, why not just install more than one and play around? You can use multiple different desktop environments on the same OS. Welcome to Linux!s

### 1.2 Creating an installer on a usb flash drive
Get yourself a basic usb flash drive of minimum 8 GB. I recommend using the program Etcher to format the disk. Get your preferred .iso from the official Manjaro website that matches your desktop environment preference and flash the drive with Etcher. It's simple. 

### 1.3 How do I create a partion and what even is a partion?
Simply put, a partion on a disk is a part of the HDD that is separated. Partitions allow you to install multiple operating systems on the same HDD.  
In our case, this will be the way that we install Linux on a Mac. The reason why this is the recommended way of installing it, is because Mac sometimes does firmware updates and some of these firmware updates are crucial to the hardware on a low level. You do not want to miss those. If this was not the case we would be in a position to install Linux only on the Mac. But at this point in time I consider it too risky. 
The other reason why we are going to partition the disk first is that if somehow we make a mistake, we can always put our blindfold back on and revert back to our OS X ways. 
This is not a problem though. We can configure it in a way so that we only boot OS X every once in a while for an update and the rest of the time when your computer turns on it will boot into Manjaro.  

To partition a disk on Mac see this short vid on YT: https://www.youtube.com/watch?v=n2xNDUqjbhU  

Remember to use MS-DOS(FAT) format. It's up to you how much space you want your new OS to have. But I would just recommend not going too extreme on either side. Leave a good amount of space for OS X for updates and shit and have enough space on your new OS to actually make it usable. 
After partioning the disk, you need to choose whether you want to use an external bootloader. You can do without it but if you have never dual booted I would recommend using one for convenience of switching between OS. 

### 1.4 Disabling SIP
On later OS X versions you need to disable SIP, which prevents users from certain actions. 
To disable this, you should reboot and hold CMD-R to enter recovery mode. From there, go to /Applications/Terminal.  
`$ csrutil disable`  
Enter your password.  
`$ reboot`  

### 1.5 Installing rEFInd bootloader

You can do without this convenient external bootloader but if this is your first time dual booting I would recommend using this. GRUB (the default bootloader for Manjaro) can be tricky for newbs like us.

rEFInd Boot Manager: https://www.rodsbooks.com/refind/  
To install the bootmanager, go to: https://sourceforge.net/projects/refind/ and download the zip.  
Unzip it, open the folder, drag the install to your terminal window. Install it. Done.  

Once you have done all these steps, you are ready to boot a live Manjaro environment. 
Reboot. rEFInd should present you with several options to boot now. Choose to boot from your flash drive.  
Before booting into the environment, you can now set the locale, time, language and keyboard layout to your liking. Just choose default keyboard layout. 
If you have an nvidia card that you want to control (i.e. different drivers), choose the nonfree option. If you have an intel gpu like me, choose free and Manjaro will figure out the driver for you (intel open sources it's drivers so it's not a problem).

### 1.6 First glance at Manjaro

Once inside the live environment of Manjaro, feel free to get a sense of the OS if this is your first time. 
When you are done, click Launch Installer.
Choose to install Manjaro with the settings you like but more importantly you need to choose "Replace a disk partition" to install it on the partition you made in OS X. The name might be different but you can probably guess which partition it is based on the size in that case.
Leave the bootloader option to its default setting. Boot managing is taken care of by rEFInd.
Wait for installation... drink coffee... come back and reboot.

## 2.0 Updating packages and configuration of package managers

### 2.1 Access to Wifi
To update pacman after initial install of manjaro, you need WiFi. Since the MacBook doesn't have an ethernet port, you need to share WiFi from your phone using either bluetooth or usb. Since this will depend on a number of factors I will leave it up to you. Find a way. 

### 2.2 Update all packages for the first time, install firewall and reboot
Open a terminal by pressing ctrl+alt+t, type the following and press enter:    
`$ sudo pacman -Syu`  
`$ sudo pacman -S gufw`  
Open firewall configuration through the default application launcher in the bottom left window and enable with default settings. Reboot again.

### 2.3 Update mirrors for pacman for faster downloading of packages
The following command will ping all the servers and return a list that pacman will use to download packages from. This will make downloading packages faster for you.   
 `$ sudo pacman-mirrors -g`  

 ### 2.4 Installation of yay to install broadcom
yay is an AUR helper, which means it is a program written in the GO language designed to make it easier for you to install packages from the Arch User Repository. We will be using yay to install packages that help us fix WiFi, controlling the fans and configuring the CPU. You can do without AUR helpers but they do make installation easier for you and at the time of writing this guide, yay is generally considered the best one. Below you will see a small cheatsheet for a list of commands to use with yay if you need to refer back to it for the rest of this guide.
  
 Install: `$ yay -S <PKG>`  
 Search: `$ yay -Ss <PKG>`  
 Info about PKG in AUR: `$ yay -Si <PKG>`  
 Update pacman and yay packages: `$ yay -Syu`  
Search for package and print a list of options: `$ yay <PKG>`  
 Install without confirm: `$ yay -S --noconfirm <PKG>`  
 Print a list of packages that need updates: `$ yay -Pu`  
 Remove unnecessary dependencies: `$ yay -Yc`  
 Manual: `$ man yay`  

 Here is a link to a recent article on yay and AUR helpers in general if you are interested in reading more about it: https://www.ostechnix.com/yay-found-yet-another-reliable-aur-helper/

 ### 2.5 Adding color and additional information to package management
 By now you might be frustrated with the bland wall of text that comes from searching for a package with yay or listing installed packages with pacman. We can fix this by adding color and highlighting in the config file for pacman.  
 `$ sudo nano /etc/pacman.conf`  
 Around line 25-35 you should see a line that says `#Color` and another line that says `#VerbosePkgLists`. Remove the hash from both of these lines to uncomment them. The next time you run a pacman or yay command, you shuld be able to see the difference. If you don't like the verbose package list info, go into the config file again and uncomment that shit.

## 3.0 Configuration of hardware and drivers

 ### 3.1 Installation of broadcom driver
 Open System Settings and go to Kernel to see which kernel version you are running. This makes a difference for the installation of the broadcom driver for WiFi. 

 Searc for broadcom in yay: `$ yay broadcom`  
 Install the version that matches your kernel  
 Reboot  

 After rebooting, you should now be able to finally access WiFi and can unplug your whatever device. 

### 3.2 Installing necessary intel drivers
Do the following to install some drivers for intel that do not come out of the box:  
`$ pacman -S xf86-video-intel mesa-libgl libva-intel-driver libva`

 ### 3.3 Getting your fans to work properly using mbpfancontrol
Section 3.3 and 3.4 are connected as they both deal with the same problem: Temperature. In this section we will fix your fans running at max RPM but just know that even when fixed they might still run at max RPM if the temperature of your CPU is extremely high (that's what they're supposed to do). The fix for this comes in 3.3, so the result of this section might not be immediately visible for you.  
 I would highly advise you to revisit this section and reconfigure the values for mbpfancontrol after you have done the necessary configurations for your CPU in section 3.3 to make sure the temperature is good and that frequency scaling is working. 

 At this point you might have noticed that your fans are not working properly, so it is time for us to do some configurations to make the Mac hardware run smoothly.  
 First things, do:  
 `$ yay mbpfancontrol`  
 Install the package from the AUR.  
 This package depends on 2 services: coretemp and applesmc. In order to make those services run on boot, do the following:   
 `$ sudo nano /etc/modules`  
 Add ´coretemp´ and ´applesmc´ in the first 2 lines. Press ctrl+x to save. Reboot.  
 What you have just done is that you have added the coretemp and applesmc to the modules that are running as soon as you boot into Manjaro. Both of these modules will help us get readings of temperatures and the speed at which the fans in your Mac is going along with other things.

 The mbpfancontrol package controls the fan and has a config file. To view the config file:   
 `$ sudo nano /etc/mbpfan.conf`  
 This is the file that we edit to make the fans not run at maximum RPM all day long.  
 Before doing so, you should detect the temperature sensors in your Mac:   
 `$ sensors_detect`  
 This will guide you through getting readings from the sensors in your laptop. Just answer yes to all the questions.  
 After doing this, you can use the sensors package to get readings of the temperature in your CPU cores and the RPM of each fan:  
 `$ sensors`  
Don't be too alarmed if the temperature of your CPU is high as well as the RPM of your fans. This is exactly what we are fixing in the next section 3.3. For now, you can shutdown the computer if you see the temperature going above 80-90 degrees celsius and come back to this guide when it has cooled down a bit. 

 You can now read different settings from the applesmc module to figure out how your settings should be. You should now read the different settings for your hardware and add these to the config file for mbpfan.  
`$ cat /sys/devices/platform/applesmc.768/fan*_max`  
Write down this value. This is your max_speed in /etc/mbpfan.conf. The same thing can be applied for obtaining the minimum RPM or your fans. Just change the last ´max´ to ´min´. 

 IMPORTANT: It's not very clear that the min and max speed of /etc/mbpfan.conf have been commented out with #. But to put the variables to use uncomment them.  
 You should now be able to get the fans running at decent RPM at least. 

 ### 3.4 Configuring and debugging the CPU
We need 2 packages to configure the cpu. Thermald to adjust the CPU and cpupower to avoid unnecessary boosting. First, install thermald:  
`$ yay thermald`  

Thermald will help us keep the temperature low automatically and adjust settings accordingly.  
To enable thermald:  
`$ systemctl enable thermald.service`  

If you at any point need to check whethter a service is still running:  
`$ systemctl status <SEVICEYOUWANTTOCHECK>`  
The service should have a status of Active (running).  

To install cpupower:  
`$ yay cpupower`   

To edit the config file of cpupower:  
`$ sudo nano /etc/default/cpupower`  

Now you can change the max frequency that your cpu will run at and the governor. The governor is what determines how cpupower will adjust the frequencies. I recommend using powersave as a governor. Your CPU will still blast through but it won't ramp up unless it needs to.  
You will need to know the frequency your CPU normally runs at and what it can boost to. My MacBook Pro Retina (mid 2014 normally runs at 2.6 GHz and can boost to at least 3.0).
Adjust the two settings with your own frequency number like so:
`governor='powersave'`  
`max_freq="2.6GHz"`  

If you feel like it, come back to this configuration file and adjust the settings and the governor to potentially get more power from your CPU.

At this point you should close all your open programs, give your computer a break for 10-15 mins and come back to do another sensors reading:  
`$ sensors`  
Look at the temperature of all CPU cores. Now you need to make a judgment whether you still consider this to be too high. As an example my MacBook Pro's CPU at this point was running at around 70 degrees celsius even when it was idling. This is clearly too much. Do some research to figure out what the normal idling temperature is for your CPU and whether you consider the numbers to be alarming. If it is, then it is time for us to debug what is causing the high temperature.  

A common problem that you will see a lot of Mac users struggling with is ACPI interrupts. ACPI interrupts come from the firmware reacting strangely to the OS. To find out if this is a problem for you as well you should do this:  
`$ grep . -r /sys/firmware/acpi/interrupts/gpe*`  
This command will use grep to print a list for you with potentially runaway ACPI interrups which indicate that something is not working the way it should.  
As an example, when I ran this command the first time I found that ´gpe06´ had a logging of 3.2 million interrupts and the computer had been running only 40 mins. That is an alarming amount of intertupts. If you see a gpe that has around 50k interrupts this might still be considered normal if the computer has been running a bit of time.  
The fix for a runaway gpe is to disable it. We are going to do this by making our own service that runs on boot and disables the gpe you are having trouble with. 
To create the service do the following and change the ´*´ to the number of gpe that you are disabling:  
`$ sudo nano /etc/systemd/system/disable_gpe*.service`  

Add the following in the file and remember to change the number to the exact gpe you want to disable:  
[Unit]
Description=Disable GPE06 interrupts

[Service]
Type=oneshot
ExecStart=/bin/bash -c 'echo "disable" > /sys/firmware/acpi/interrupts/gpe06'

[Install]
WantedBy=multi-user.target

Now we enable it to run on boot:  
`$ sudo systemctl enable disable_gpe*.service`    
To make the service run in the current session you are in:    
`$ sudo systemctl start disable_gpe*.service`  

Now, disabling this service may or may not cause problems for you. Some people experience problems suspending the computer after disabling a service. But most of the time it will be fine. If not, please report back to me. 
As a final remark on the debugging of the CPU I wish to point out that you should always do your own monitoring of temperatures and of processes that are requiring an alarming amount of CPU power. To keep tracks of these processes you can run a package called htop.  
To install htop:  
`$ sudo pacman -S htop`    
To run htop, simply type:  
`$ htop`  
This will provide you with an interface in your terminal showing processes taking power from your CPU. 

### 3.6 Configuring the battery power and power consumption
Powertop is a package that will help us manage the power consumption if you are on a laptop.   
`$ yay powertop`  

To calibrate power (you want the laptop on battery power for this):  
`$ powertop --calibrate`  

We can turn power into a service that runs automatically every time you boot into Manjaro:  
`$ sudo nano /etc/systemd/system/powertop.service`    

Add the following to the file:  

[Unit]
Description=Powertop tunings

[Service]
Type=oneshot
ExecStart=/usr/bin/powertop --auto-tune

[Install]
WantedBy=multi-user.target

To make powertop run automatically when you boot:  
`$ systemctl enable powertop.service`  

 ### 3.7 Configuring to HiDPI support to accommodate the retina display
 Configuring Manjaro to take advantage of the Retina display will ultimately depend on your desktop environment as well. If you decide to go for a tiling window manager like i3, bspwm or dwm, you will need to have a .Xresources file with certain settings. If you don't have ~/.Xresources file, just create it and enter the following in the file:  

`Xft.dpi: <dpi>  `

Note that the number you put in works best if it is a multiple of 96. For example, a MacBook Pro 11,2 15" has a native PPI of 220 at full retina and so in this case i would use the number 192.  
If you ever want to see your current PPI of an X session you can use the following command:  

`$ xdpyinfo | grep -B 2 resolution`  

Fonts in certain applications might be scaled too much now. To counter this, we can scale down the fonts by 50% by creating a .profile file:  

`$ touch ~/.profile`  

Add "export GDK_DPI_SCALE=0.5" to the file and sav it. To see the effects type this in the terminal and reopen the application that has been scaled too much:  

`$ source .profile`  
 
 If you have chosen KDE plasma as DE like me, then you will find the settings you need by opening System Settings and going to the Monitor section. Here you will be able to change the resolution as well as the scale. My MacBook Pro Retina 15" for example is running at a resolution of 2800x1800 and as a result I have scaled the desktop to 150% of it's normal size. Now you can take advantage of the crisp HiDPI text and still have decent size of text and windows.

 ### 3.8 Keyboard adjustments

We can swap the option and cmd key by typing this:  
 `$ echo 1 | sudo tee /sys/module/hid_apple/parameters/swap_opt_cmd`    

 To make the changes permanent type:    
 `$ echo options hid_apple swap_opt_cmd=1 | sudo tee -a /etc/modprobe.d/hid_apple.conf`

 Change the 1 to 0 to revert back. This is the same file that we edit if we want to change the way that the FN key works. On some Apple Keyboards when running a Linux distro, the media keys fuck up everything below F5 (functions included), so if you want to have your brighness function on F1 and F2 back, you might need to edit this file. To edit this file, do the following:  

 `$ sudo nano /etc/modprobe.d/hid_apple.conf`  

 In the file you should see the swap_opt cmd if you chose to add this. On a new line enter the following:  

 `options hid_apple fnmode= <NUMBER>`  

 The number that you choose to enter into this line will change how the keyboard uses the function key. By default it should be 0. If you want to only use the function keys, it should be 1 and if you want the keys to default to F1-F12 and functions whenever you hold FN, then change the number to 2. I recommend 2.  

 ### 3.9 Installation of libraries for lightweight gaming in case you are lucky enough to have an nvidia graphics card
This oneliner will install a lot of packages and libraries that are needed for playing games on Manjaro. It will also install PlayOnLinux, Wine and Winetricks but you can just omit it from the command if you don't care about it. 

`$ sudo pacman -S lib32-libldap lib32-nvidia-utils lib32-nvidia-libgl lib32-alsa-lib lib32-alsa-plugins lib32-libpulse lib32-alsa-oss lib32-openal wine winetricks playonlinux`

PlayOnLinux is a front-end for wine basically and will allow you to play windows-only games through linux. PlayOnLinux is depite its deceiving name an excellent candidate for running Adobe applications through wine in a convenient front-end, in case that's something you are interested in (hint: use FOSS instead). Another option for this could be Lutris or creating your own wrappers for wine. I will leave that up to you.