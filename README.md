# A guide on how to setup Manjaro (or Arch-based linux distro) on MacBook Pro Retina (mid 2014)

My strategy for finding a way to install Linux and FOSS on a closed Mac is that of sticking my nose where it doesn't belong, where I have unsufficient knowledge. At times that strategy is definitely not pretty, but I guarantee that it is a very efficient way of learning. Stop caring so much about the clinicallly white and closed silver box that is your MacBook and go open source.  
NO, I am not a developer, nor am I a decent programmer. I am an artist who likes to work with code and software and I have some basic knowledge about computer. 
But I am a trashcan programmer at best. 
So, be warned, if you choose to follow this guide, you are not following a perfect guide on how to get the OS you want. You are going on a messy and shitty journey of failing software and hardware. But there is a way. Open source.
This guide covers how to create a basic partition on your HDD so that you can always go back to macOS if you desire (I also explain why this is the optimal way to do it). I learned the hard way that erasing the entire disk is not the solution that you want. 

I made the decision to switch from Mac and OS X to a Linux operating system out of frustration with the restrictions that usually follow Mac around. As I do not have a ton of experience with installing a new OS, partitioning harddrives, configuring and compiling in c and so on, this repo is a way for me to collect the experiences gathered from this Linux journey.

I made this repo mainly for myself because I wanted to collect and gather my experiences with installing Manjaro on a MacBook instead of going back and forth. I will add config files and updates as I gain experience.  
Nevertheless, if you are as fed up with the restrictions of OS X and Mac in general, you might want to switch to a Linux based operating system. If that's the case, then I have bittersweet news: The good news is that your decision is excellent and Linux is a great choice. The bad news is that Mac and OS X is not very linux-friendly. I would in fact consider them linux-unfriendly. To make matters worse, you chose to install it on a laptop. But hey, there is a way and you just might get a better performing computer with better longevity out of this. If you care and spend the time to set things up properly.

Here is a short list of common problems that people are having when trying to install Linux on a MacBook just so you know (this will depend on which Mac you are installing on). Before reading this list you should know that some of these problems are very easy to fix (a single line of code will fix most of these, but some are more persistent). All these issues, except for the sound and camera, is adressed here. 

WiFi needs a new broadcom driver to work properly. This issue is easily fixed with a simple install of a package.

Sound doesn't work from the start. Same solution applies here.

Fans are going at max speed at all times. This issue is slightly more complicated but the solution is quite easy nevertheless.

CPU runs hot (even when idle). This issue is adressed in the guide and it is the most complicated on the list. For some the solution is to disable file indexing as a background service. For others it requires a close monitoring of what exaclty is eating your CPU. This guide will go through setting up CPU frequency scaling as well. Your solution may vary and may require research. 

FINAL WARNING: This is not a perfect guide and if you choose to erase your disk or fry an egg on your burning hot CPU, it's up to you to find new hardware and a way to restore macOS if you want. Choice of OS is your decision. As it should be. 

## Why Manjaro?

## How do I create a partion, what is a partion and do you have an ASCII potato?

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



The first two questions are easy. A partion 

## Access to Wifi

To update pacman after initial install of manjaro, you need WiFi. Since the MacBook doesn't have an ethernet port, you need to share WiFi from your phone using either bluetooth or usb.

## Update all packages for the first time, install firewall and reboot

`sudo pacman -Syu`  
`sudo pacman -S gufw`  
Open firewall configuration and enable with default settings. Reboot again.

 ## Installation of yay to install broadcom

 yay repo: https://github.com/Jguer/yay

Here is a link to a recent guide on yay: https://www.ostechnix.com/yay-found-yet-another-reliable-aur-helper/

A cheatsheet list of commands for yay to install packages:  
 Install: `yay -S PKG`  
 Search: `yay -Ss PKG`  
 Info about PKG in AUR: `yay -Si PKG`  
 Update pacman and yay packages: `yay -Syu`  
Search for package and print a list of options: `yay PKG`  
 Install without confirm: `yay -S --noconfirm PKG`  
 print pakker som skal opdateres: `yay -Pu`  
 Remove unnecessary dependencies: `yay -Yc`  
 Manual: `man yay`  

 ## Installation of broadcom driver

 Open System Settings -> Kernel to see which kernel version you are running. This makes a difference for the installation of the broadcom driver for WiFi. 

 Searc for broadcom in yay: `yay broadcom`  
 Install the version that matches your kernel  
 Reboot  

 After rebooting, you should now be able to finally access WiFi and can unplug your whatever device. 
 
## Update mirrors for pacman for faster downloading of packages

The following command will ping all the servers and return a list that pacman will use to download packages from:  

 `sudo pacman-mirrors -g`  

 ## Installation of libraries for lightweight gaming in case you are lucky enough to have an nvidia graphics card

`sudo pacman -S lib32-libldap lib32-nvidia-utils lib32-nvidia-libgl lib32-alsa-lib 
lib32-alsa-plugins lib32-libpulse lib32-alsa-oss lib32-openal wine winetricks playonlinux`

PlayOnLinux is a front-end for wine basically and will allow you to play windows-only games through linux. PlayOnLinux is depite its deceiving name an excellent candidate for running Adobe applications through wine in a convenient front-end, in case that's something you are interested (hint: use FOSS instead). Another option for this could be Lutris or creating your own wrappers for wine. I will leave that up to you.

