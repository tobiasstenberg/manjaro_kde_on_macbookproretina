# A guide on how to setup Manjaro (or Arch-based linux distro) on MacBook Pro Retina (mid 2014)

## Access to Wifi

To update pacman after initial install of manjaro, you need WiFi. Since the MacBook doesn't have an ethernet port, you need to share WiFi from your phone using either bluetooth or usb.

## Update all packages for the first time, install firewall and reboot

`sudo pacman -Syu`  
`sudo pacman -S gufw`  
Open firewall configuration and enable with default settings. Reboot again.

 ## installation af yay til at installere broadcom driver til WiFi

 yay repo: https://github.com/Jguer/yay

 link til guide (2019): https://www.ostechnix.com/yay-found-yet-another-reliable-aur-helper/

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

PlayOnLinux is a front-end for wine basically and will allow you to play windows-only games through linux. Another option for this could be Lutris or creating your own wrappers for wine. I will leave that up to you.

