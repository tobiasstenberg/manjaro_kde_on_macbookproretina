# A guide on how to setup Manjaro KDE (or Arch-based linux distro) on MacBook Pro Retina 15"

## access to Wifi
to update pacman after initial install of manjaro, you need WiFi. Since the MacBook doesn't have an ethernet port, you need to share WiFi from your phone using either bluetooth or usb.

## update all packages for the first time, install firewall and reboot
`sudo pacman -Syu`  
`sudo pacman -S gufw`  
`reboot`  

 ## installation af yay til at installere broadcom driver til WiFi

 yay repo: https://github.com/Jguer/yay

 link til guide (2019): https://www.ostechnix.com/yay-found-yet-another-reliable-aur-helper/

 install: `yay -S PKG`
 søgning: `yay -Ss PKG`
 info om PKG i AUR: `yay -Si PKG`
 opdatering af pacman pakker og yay pakker: `yay -Syu`
 søg efter pakker og servér som muligheder for installation: `yay PKG`
 installation uden confirm: `yay -S --noconfirm PKG`
 print pakker som skal opdateres: `yay -Pu`
 fjern unødvendige dependencies: `yay -Yc`
 manual: `man yay`

 ## installation af broadcom driver

 åbn system settings -> kernel og se, hvilken kernel version, du kører i øjeblikket. For mig lige nu er det 5.4, men måske kører du en anden. Skriv nummeret ned.

 søg efter broadcom drivere med yay: `yay broadcom`
