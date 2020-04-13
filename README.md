# A shitty guide on how to setup Manjaro (or Arch-based linux distro) on MacBook Pro Retina (mid 2014)

My strategy for finding a way to install Linux and FOSS on a closed Mac is that of sticking my nose where it doesn't belong, where I have unsufficient knowledge. The strategy is definitely not pretty, but I guarantee that it is a very efficient way of learning. Stop caring so much about the clinically clean silver box that is your MacBook and go open source.  
No, I am not a developer, nor am I a decent programmer. I am an artist who likes to work with code and software and I have some basic knowledge about computers. 
But I am a trashcan programmer at best. 
So, be warned, if you choose to follow this guide, you are not following a perfect guide on how to get the OS you want. You are going on a messy and shitty journey of failing software and hardware. But there is a way. Open source.
This guide also covers how to create a basic partition on your HDD so that you can always go back to macOS if you desire (I also explain why this is the optimal way to do it). I learned the hard way that erasing the entire disk is not the solution that you want. 

I made the decision to switch from Mac and OS X to a Linux operating system out of frustration with the restrictions that usually comes with owning a Mac. As I do not have a ton of experience with installing a new OS, partitioning harddrives, configuring and compiling in C and so on, this repo is a way for me to collect the experiences gathered from this Linux journey.

I made this repo mainly for myself because I wanted to collect and gather my experiences with installing Manjaro on a MacBook instead of going back and forth. I will add config files and updates as I gain experience.  
Nevertheless, if you are as fed up with the restrictions of OS X and Mac in general, you might want to switch to a Linux based operating system. If that's the case, then I have bittersweet news: The good news is that your decision is excellent and Linux is a great choice. The bad news is that Mac and OS X is not very linux-friendly. I would in fact consider them linux-unfriendly. To make matters worse, you chose to install it on a laptop. But hey, there is a way and you just might get a better performing computer with better longevity out of this. If you care and spend the time to set things up properly.

Here is a short list of common problems that people are having when trying to install Linux on a MacBook just so you know (this will depend on which Mac you are installing on). Before reading this list you should know that some of these problems are very easy to fix (a single line of code will fix most of these, but some are more persistent). All these issues, except for the sound and camera, is adressed here. 

WiFi needs a new broadcom driver to work properly. This issue is easily fixed with a simple install of a package.

Sound doesn't work from the start. Same solution applies here.

Fans are going at max speed at all times. This issue is slightly more complicated but the solution is quite easy nevertheless.

CPU runs hot (even when idle). This issue is adressed in the guide and it is the most complicated on the list. For some the solution is to disable file indexing as a background service. For others it requires a close monitoring of what exaclty is eating your CPU. This guide will go through setting up CPU frequency scaling as well. Your solution may vary and may require research. 

#### FINAL WARNING: This is not a perfect guide and if you choose to erase your disk or fry an egg on your burning hot CPU, it's up to you to find new hardware and a way to restore macOS if you want. Choice of OS is your decision. As it should be. 

## Why Manjaro?

Manjaro is a beautiful distro of Linux which is Arch-based. An arch-based distro has the advantage of access to the Arch User Repository (AUR) which is an amazing community of people making open source software and packages. Installing Arch Linux could be an option for you, but Arch Linux is very difficult to install and requires quite a lot of effort. Arch Linux is cutting edge and if you want control over every aspect of your OS, it is the way to go. Manjaro is a lot easier to install and still reaps the benefits of access to the AUR while being friendly on new users.
Manjaro is a rolling release system, meaning that every update is sent out immediately. Personally, I love rolling release systems but if it is not for you, consider installing a Debian-based distro maybe. Ubuntu, Mint, Fedore.  
Where Apple seems to be asking "How much are you willing to spend?", Linux asks: "What is your flavour? Which type of OS fits you the best?"

## Desktop Environments

I will keep this short. I like the KDE desktop environment. It looks great and is highly customizable. If you want GNOME or whatever, go for it. In the end, if you don't like it, why not just install more than one and play around?

### Before following my instructions on installing the actual OS

The next sections are put together from a variety of sources. This guide mainly covers how to configure Manjaro post-installation. If you want to follow a different guide on installing the OS itself, skip the next 2 sections and I would recommend this guide: https://www.lifewire.com/dual-boot-linux-and-mac-os-4125733

## Creating an installer on a usb flash drive

Get yourself a basic usb flash drive of minimum 8 GB. I recommend using the program Etcher to format the disk. Get your preferred .iso from the official Manjaro website and flash the drive with Etcher. It's simple. 

## How do I create a partion, what is a partion and can I have a halfway chopped ASCII potato?

                                  ▒▒▒▒▒▒▒▒▒▒▒▒▒▒░░                    
                              ▓▓▓▓████████████████▓▓▓▓▒▒              
                          ▓▓▓▓████░░░░░░░░░░░░░░░░██████▓▓            
                        ▓▓████░░░░░░░░░░░░░░░░░░░░░░░░░░████          
                      ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██        
                    ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██      
                  ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██      
                ▓▓██░░░░░░▓▓██░░  ░░░░░░░░░░░░░░░░░░░░▓▓██░░  ░░██    
              ▓▓██░░░░░░░░██████░░░░░░░░░░░░░░░░░░░░░░██████░░░░░░██  
              ▓▓██░░░░░░░░██████▓▓░░░░░░██░░░░██░░░░░░██████▓▓░░░░██  
            ▓▓██▒▒░░░░░░░░▓▓████▓▓░░░░░░████████░░░░░░▓▓████▓▓░░░░░░██
          ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░██░░░░██░░░░░░░░░░░░░░░░░░░░██
          ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██
          ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██
        ░░▓▓▒▒░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██
        ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██
        ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██
        ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██
      ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██
      ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██
      ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██  
      ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██  
    ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██  
    ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██  
    ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██  
    ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██  
    ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██    
  ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██    
  ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██    
  ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██    
  ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██    
  ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██  
  ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██  
  ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██  
    ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██  
    ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██  
    ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██  
    ░░▓▓▓▓░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██  
      ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██░░  
        ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██    
          ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██      
          ▓▓██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██        
            ▓▓████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░██          
              ▓▓▓▓████████░░░░░░░░░░░░░░░░░░░░░░░░████████░░          
              ░░░░▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓░░░░░░░░            


Simply put, a partion on a disk is a part of the HDD that is separated. Partitions allow you to install multiple operating systems on the same HDD.  
In our case, this will be the way that we install Linux on a Mac. The reason why this is the recommended way of installing it, is because Mac sometimes do firmware updates and some of these firmware updates are crucial to the hardware on a low level. 
The other reason why we are going to partition the disk first is that if somehow we make a mistake, we can always put our blindfold back on and revert back to our sad OS X ways. 
This is not a problem though. We can configure it in a way so that we only boot OS X every once in a while for an update and the rest of the time when your computer turns on it will boot into Manjaro.  

To partition a disk on Mac see this short vid on YT: https://www.youtube.com/watch?v=n2xNDUqjbhU  

Remember to use MS-DOS(FAT) format. It's up to you how much space you want your new OS to have. But I would just recommend not going too extreme on either side. Leave a good amount of space for OS X for updates and shit and have enough space on your new OS to actually make it usable. 
After partioning the disk, you need to choose whether you want to use an external bootloader. You can do without it but if you have never dual booted I would recommend using one for convenience of switching between OS. 

## Disabling SIP

On later OS X versions you need to disable SIP, which prevents users from certain actions. 
To disable this, you should reboot and hold CMD-R to enter recovery mode. From there, go to /Applications/Terminal.  
`csrutil disable`    
Enter your password. 
`reboot`

## Installing rEFInd bootloader

rEFInd Boot Manager: https://www.rodsbooks.com/refind/  
To install the bootmanager, go to: https://sourceforge.net/projects/refind/ and download the zip.  
Unzip it, open the folder, drag the install to your terminal window. Install it. Done.  

Once you have done all these steps, you are ready to boot a live Manjaro environment. 
Reboot. rEFInd should present you with several options to boot now. Choose to boot from your flash drive.  
Before booting into the environment, you can now set the locale, time, language and keyboard layout to your liking. Just choose default keyboard layout. 

## First glance at Manjaro

Once inside the live environment of Manjaro, feel free to get a sense of the OS if this is your first time. 
When you are done, click Launch Installer.
Choose to install Manjaro with the settings you like but more importantly you need to choose "Replace a disk partition" to install it on the partition you made in OS X. 
Leave the bootloader option to its default setting. Boot managing is taken care of. 
Wait for installation... drink coffee... come back and reboot.

## Access to Wifi

To update pacman after initial install of manjaro, you need WiFi. Since the MacBook doesn't have an ethernet port, you need to share WiFi from your phone using either bluetooth or usb. Since this will depend on a number of factors I will leave it up to you. Find a way. It's WiFi. It's everywhere. 

## Update all packages for the first time, install firewall and reboot

`sudo pacman -Syu`  
`sudo pacman -S gufw`  
Open firewall configuration and enable with default settings. Reboot again.

 ## Installation of yay to install broadcom

 yay repo: https://github.com/Jguer/yay

Here is a link to a recent guide on how to install yay that you should follow: https://www.ostechnix.com/yay-found-yet-another-reliable-aur-helper/

A cheatsheet list of commands for yay to install packages:  
 Install: `yay -S PKG`  
 Search: `yay -Ss PKG`  
 Info about PKG in AUR: `yay -Si PKG`  
 Update pacman and yay packages: `yay -Syu`  
Search for package and print a list of options: `yay PKG`  
 Install without confirm: `yay -S --noconfirm PKG`  
 Print pakker that need updates: `yay -Pu`  
 Remove unnecessary dependencies: `yay -Yc`  
 Manual: `man yay`  

 ## Installation of broadcom driver

 Open System Settings/Kernel to see which kernel version you are running. This makes a difference for the installation of the broadcom driver for WiFi. 

 Searc for broadcom in yay: `yay broadcom`  
 Install the version that matches your kernel  
 Reboot  

 After rebooting, you should now be able to finally access WiFi and can unplug your whatever device. 
 
## Update mirrors for pacman for faster downloading of packages

The following command will ping all the servers and return a list that pacman will use to download packages from:  

 `sudo pacman-mirrors -g`  

 ## Installation of mbpfancontrol

 At this point you might have noticed that your fans are not working properly, so it is time for us to do some configurations to make the Mac hardware run smoothly.  
 First things, do `yay mbpfancontrol` and install the package from the AUR.  
 This package depends on 2 services, coretemp and applesmc. In order to make those services run on boot, do `sudo nano /etc/modules` and add coretemp and applesmc in 2 lines. Press CTRL+X to save. Reboot.  

 The mbpfancontrol package controls the fan and has a config file. To view the config file do: `sudo nano /etc/mbpfan.conf`. This is the file that we edit to make the fans not run at maximum RPM all day long.  
 Before doing so, you should do: `sensors_detect`. This will guide you through getting readings from the sensors in your laptop. Just answer yes to all the questions.  
 After doing this, you can type `sensors` to get readings of the temperature in your CPU cores and the RPM of each fan.  
 You can now read different settings from the applesmc module to figure out how your settings should be. You should now do a `cat /sys/devices/platform/applesmc.768/fan*_max`. Write down this value. This is your max_speed in /etc/mbpfan.conf.  
 IMPORTANT: It's not very clear that the min and max speed of /etc/mbpfan.conf have been commented out with #. But to put the variables to use uncomment them.  
 You should now be able to get the fans running at decent RPM at least. 

 ## Configuring CPU frequency scaling

 (coming soon)

 ## Configuring to HiDPI support to accommodate the retina display

 (coming soon)

 ## Swapping the opt and cmd key

We can swap the option and cmd key by typing this:
 `$ echo 1 | sudo tee /sys/module/hid_apple/parameters/swap_opt_cmd`  

 To make the changes permanent type:  
 `$ echo options hid_apple swap_opt_cmd=1 | sudo tee -a /etc/modprobe.d/hid_apple.conf`

 ## Installation of libraries for lightweight gaming in case you are lucky enough to have an nvidia graphics card

`sudo pacman -S lib32-libldap lib32-nvidia-utils lib32-nvidia-libgl lib32-alsa-lib 
lib32-alsa-plugins lib32-libpulse lib32-alsa-oss lib32-openal wine winetricks playonlinux`

PlayOnLinux is a front-end for wine basically and will allow you to play windows-only games through linux. PlayOnLinux is depite its deceiving name an excellent candidate for running Adobe applications through wine in a convenient front-end, in case that's something you are interested in (hint: use FOSS instead). Another option for this could be Lutris or creating your own wrappers for wine. I will leave that up to you.

 ## Convenient additions to your .bashrc 
Simple and convenient list additions to your .bashrc
`echo -e '\nalias ll="ls -lhF"' >> ~/.bashrc`  
`echo -e '\nalias la="ls -lahF"' >> ~/.bashrc`  